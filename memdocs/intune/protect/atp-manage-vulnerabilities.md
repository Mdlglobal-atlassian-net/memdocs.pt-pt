---
title: Utilizar intune para remediar vulnerabilidades encontradas pelo Microsoft Defender ATP - Azure Microsoft Docs
description: Veja como gerir as tarefas de segurança a partir e Threat & vulnerabilidade Management, parte da Microsoft Defender Advanced Threat Protection (ATP) a partir da consola Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5464e70d915dceb9cf2c6a3b2385419cfc11e38b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077840"
---
# <a name="use-intune-to-remediate-vulnerabilities-identified-by-microsoft-defender-atp"></a>Utilizar o Intune para remediar vulnerabilidades identificadas pelo Microsoft Defender ATP

Quando integrar o Intune com a Microsoft Defender Advanced Threat Protection (ATP), pode tirar partido da ATPs Threat & Vulnerability Management (TVM) e utilizar o Intune para remediar a fraqueza do ponto final identificada pela TVM. Esta integração traz uma abordagem baseada no risco para a descoberta e priorização de vulnerabilidades que podem melhorar o tempo de resposta à reparação em todo o seu ambiente.

[A Threat & Vulnerability Management](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/next-gen-threat-and-vuln-mgt) faz parte da Proteção avançada de ameaças do [Microsoft Defender.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection)

## <a name="how-integration-works"></a>Como funciona a integração

Depois de ligar intune à Microsoft Defender Advanced Threat Protection, o ATP recebe detalhes de ameaças e vulnerabilidades de dispositivos geridos.

Na consola do Microsoft Defender Security Center, a ATP admins analisa dados sobre vulnerabilidades de ponto final. Os administradores usam então um clique único para criar tarefas de segurança que sinalizem os dispositivos vulneráveis para remediação. As tarefas de segurança são imediatamente passadas para a consola Intune onde os administradores intune podem vê-las. A tarefa de segurança identifica o tipo de vulnerabilidade, prioridade, estado e os passos a tomar para remediar a vulnerabilidade. O administrador intune opta por aceitar ou rejeitar a tarefa.

Quando uma tarefa é aceite, o administrador intune age então para remediar a vulnerabilidade embora Intune, utilizando a orientação fornecida como parte da tarefa de segurança.

As ações comuns de reparação incluem:

- **Bloqueie** uma aplicação de ser executada
- **Implemente** uma atualização do sistema operativo para atenuar a vulnerabilidade.
- **Modificar** o valor do registo.
- **Desative** ou **ative** uma configuração que afete a vulnerabilidade.
- **A Necessidade de Atenção** alerta o administrador para a ameaça quando não há uma recomendação adequada a fornecer.

Exemplo de fluxo de trabalho:

- Dentro do Microsoft Defender ATP, é descoberta uma vulnerabilidade para uma aplicação chamada Contoso Media Player v4 e um administrador cria uma tarefa de segurança para atualizar essa aplicação. O jogador da Contoso Media é uma aplicação não gerida que foi implementada com o Intune.

  Esta tarefa de segurança aparece na consola Intune com um estatuto de Pendente:

  ![Ver a lista de tarefas de segurança na consola Intune](./media/atp-manage-vulnerabilities/temp-security-tasks.png)

- O administrador intune seleciona a tarefa de segurança para visualizar detalhes sobre a tarefa.  O administrador seleciona **então Aceitar**, que atualiza o estado em Intune, e em ATP a *aceitar*.

  ![Aceitar ou rejeitar uma tarefa de segurança](./media/atp-manage-vulnerabilities/temp-accept-task.png)

- O administrador remedia então a tarefa com base nas orientações fornecidas. A orientação varia dependendo do tipo de reparação que é necessário. Quando disponível, a orientação de reparação inclui links que abrem os quadros relevantes para configurações em Intune.

  Como o leitor de meios de comunicação neste exemplo não é uma aplicação gerida, intune só pode fornecer instruções de texto. Se a aplicação fosse gerida, a Intune poderia fornecer instruções para descarregar uma versão atualizada e fornecer um link para abrir a implementação da aplicação para que os ficheiros atualizados possam ser adicionados à implementação.

- Após a conclusão da reparação, o administrador Intune abre a tarefa de segurança e seleciona **a Tarefa Completa**.  O estado de reparação é atualizado para intune e em ATP, onde os administradores de segurança confirmam o estado revisto para a vulnerabilidade.

## <a name="prerequisites"></a>Pré-requisitos  

**Assinaturas:**

- Microsoft Intune  
- Microsoft Defender Advanced Threat Protection[(Inscreva-se para um teste gratuito](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-main-abovefoldlink).)

**Configurações insintonizadas para ATP:**

- Configure um serviço de ligação ao serviço com o Microsoft Defender ATP.
- Implemente uma política de configuração do dispositivo com um tipo de perfil de **Microsoft Defender ATP (Windows 10 Desktop)** para dispositivos que terão um risco avaliado pelo ATP.

  Para obter informações sobre como configurar intune para trabalhar com atp, consulte [Enforce compliance for Microsoft Defender ATP with Conditional Access in Intune](advanced-threat-protection.md#enable-microsoft-defender-atp-in-intune).

## <a name="work-with-security-tasks"></a>Trabalhar com tarefas de segurança

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione > **tarefas**de **segurança endpoint**.

3. Selecione uma tarefa da lista para abrir uma janela de recursos que apresente detalhes adicionais para essa tarefa de segurança.

   Ao visualizar a janela de recursos de tarefade segurança, pode selecionar links adicionais:

   - APPS GERIDAS - Veja a aplicação que está vulnerável. Quando a vulnerabilidade se aplica a várias aplicações, verá uma lista filtrada de aplicações.
   - DISPOSITIVOS - Veja uma lista dos *dispositivos Vulneráveis,* a partir do qual pode ligar-se a uma entrada com mais detalhes sobre a vulnerabilidade nesse dispositivo.
   - REQUESTOR - Utilize o link para enviar correio ao administrador que submeteu esta tarefa de segurança.
   - NOTAs - Leia as mensagens personalizadas enviadas pelo solicitador ao abrir a tarefa de segurança.

4. Selecione **Aceitar** ou **Rejeitar** enviar notificação para atp para a sua ação planeada. Quando aceitar ou rejeitar uma tarefa, pode enviar notas, que são enviadas para ATP.

5. Depois de aceitar uma tarefa, reabra a tarefa de segurança (se fechou) e siga os detalhes da REMEDIATION para remediar a vulnerabilidade. As instruções fornecidas pela ATP nos detalhes da tarefa de segurança variam consoante a vulnerabilidade envolvida.

   Quando é possível fazê-lo, as instruções de reparação incluem links que abrem os objetos de configuração relevantes na consola Intune.

6. Depois de completar os passos de reparação, abra a tarefa de segurança e selecione **Complete Task**.  Esta ação atualiza o estado da tarefa de segurança tanto no Intune como no ATP.

Após a reparação ser bem sucedida, a pontuação de exposição ao risco em ATP pode cair, com base em novas informações dos dispositivos remediados.

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre Intune e [Microsoft Defender ATP](advanced-threat-protection.md).

Reveja a [Intune Mobile Threat Defense](mobile-threat-defense.md).

Reveja o dashboard de Gestão de [Vulnerabilidades & Ameaça](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/tvm-dashboard-insights) no ATP do Microsoft Defender.
