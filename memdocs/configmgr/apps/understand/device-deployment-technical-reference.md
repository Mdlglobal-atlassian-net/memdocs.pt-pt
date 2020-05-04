---
title: Implementação de aplicativos para recolha de dispositivos referência técnica
titleSuffix: Configuration Manager
description: Implementações de aplicações de resolução de problemas para recolhade dispositivos referência técnica para Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709762"
---
# <a name="application-deployment-for-device-collections"></a>Implementação de aplicações para coleções de dispositivos

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando uma aplicação é implementada para uma coleção de Dispositivos, a política é direcionada a todos os dispositivos da recolha, independentemente do propósito de implementação. Este artigo explica o processamento de descarregamento e implementação de políticas no cliente.

> [!TIP]
> Todas as informações necessárias para rever os registos do cliente podem ser obtidas executando a consulta SQL referenciada na secção [Antes de iniciar.](app-deployment-technical-reference.md#before-you-begin)

## <a name="policy-download"></a>Download de Política

Depois de a política de implementação da aplicação ser direcionada ao cliente, o cliente descarregaria a apólice no próximo ciclo de sondagens. Quando o cliente descarrega a apólice, descarrega políticas relacionadas para além da política de implementação. Estas políticas relacionadas incluem a política de aplicação, tipo de implantação, condições globais, etc. A atividade de descarregamento de políticas pode ser rastreada no **PolicyAgent.log** no cliente, utilizando o Id Exclusivo de Aplicação ou Atribuição.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Após o download das políticas no cliente, o componente Scheduler cria horários para ativação e execução de implementação.

## <a name="deployment-activation"></a>Ativação de implementação

A avaliação da aplicação é iniciada quando a implementação é ativada. O componente do programador cria um calendário para ativar a atribuição no Tempo Disponível configurado na implementação. Esta atividade pode ser rastreada em **Scheduler.log** no cliente usando o ID Exclusivo de Atribuição de Aplicações.

- Para as implementações **necessárias,** o calendário de ativação é criado, mas tem um atraso de até duas horas para evitar a contenção de recursos nos Servidores do Site e pontos de distribuição. O atraso ajuda a evitar a contenção, uma vez que o conteúdo da aplicação pode ser descarregado durante a avaliação se a aplicação for aplicável com base nas Regras de Requisitos definidas.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Para as implementações **disponíveis,** o calendário de ativação é criado para ser disparado no tempo disponível configurado na Implantação.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Quando a hora do horário chegar, o componente Scheduler envia a mensagem de ativação ao Agente DCM para efetuar a avaliação da aplicação.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

O Agente DCM recebe a mensagem de ativação e cria um trabalho para avaliar a aplicação.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Execução de destacamento

A instalação da aplicação é iniciada quando a implementação é executada.

- Para implementações **necessárias,** o Scheduler cria um prazo após o download da política para fazer cumprir a aplicação no prazo de implementação. O prazo não é aleatório por defeito. O comportamento de aleatoriedade para a ativação pode ser controlado pela definição do cliente de desativação do cliente de [aleatoriedade.](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization)

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    No prazo, a componente Scheduler envia a mensagem de prazo ao Agente DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    O Agente DCM recebe a mensagem de prazo e cria um trabalho para fazer cumprir a aplicação.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Para implementações com prazo no passado, a aplicação é ativada e executada imediatamente pelo mesmo trabalho do DCM Agent que realiza as ações de avaliação, descarregamento e instalação.

- Para implementações **disponíveis,** não há prazo sinuoso uma vez que a execução ocorre quando a instalação da aplicação é iniciada pelo utilizador do Software Center. Quando o utilizador inicia uma instalação, é criado um trabalho de Agente DCM para realizar avaliação de aplicação, download e instalação. Esta atividade pode ser rastreada em **DCMAgent.log** no cliente.

## <a name="next-steps"></a>Passos Seguintes

- [Compreender componentes do cliente de implementação de aplicações](client-components-technical-reference.md)
