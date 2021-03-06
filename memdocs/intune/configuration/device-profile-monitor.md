---
title: Ver perfis de dispositivo com o Microsoft Intune – Azure | Microsoft Docs
description: Veja e faça a gestão dos detalhes do perfil de configuração do dispositivo no Microsoft Intune para ver um gráfico do número de dispositivos atribuídos a um perfil e que dispositivos têm perfis atribuídos ou implementados. Também pode resolver problemas de perfis com definições em conflito.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7
ms.reviewer: karthib
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3de0b0a6302bd53384bd492aaf9377c0e5653384
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988448"
---
# <a name="monitor-device-profiles-in-microsoft-intune"></a>Monitorizar perfis de dispositivos no Microsoft Intune



Intune inclui algumas funcionalidades para ajudar a monitorizar e gerir os perfis de configuração do seu dispositivo. Por exemplo, pode verificar o estado de um perfil, ver que dispositivos estão atribuídos e atualizar as propriedades de um perfil.

## <a name="view-existing-profiles"></a>Ver perfis existentes

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**.

Todos os perfis existentes estão listados e incluem detalhes como a plataforma e se o perfil está atribuído a algum dispositivo.

## <a name="view-details-on-a-profile"></a>Ver detalhes de um perfil

Depois de criar o perfil do dispositivo, o Intune disponibiliza gráficos. Estes gráficos apresentam o estado de um perfil, como a atribuição com êxito a dispositivos ou se o perfil mostra um conflito.

1. Selecione um perfil existente. Por exemplo, selecione um perfil do macOS.
2. Selecione o separador **Descrição Geral**.

    O gráfico gráfico superior mostra o número de dispositivos atribuídos ao perfil do dispositivo. Por exemplo, se o perfil de configuração do dispositivo se aplicar a dispositivos iOS, o gráfico apresentará a contagem de dispositivos macOS.

    Também mostra o número de dispositivos de outras plataformas que são atribuídos ao mesmo perfil do dispositivo. Por exemplo, mostra a contagem de dispositivos não macOS.

    ![Ver o número de dispositivos atribuídos ao perfil do dispositivo](./media/device-profile-monitor/device-configuration-profile-graphical-chart.png)

    O gráfico gráfico inferior mostra o número de utilizadores atribuídos ao perfil do dispositivo. Por exemplo, se o perfil de configuração do dispositivo se aplicar a utilizadores do macOS, o gráfico apresentará a contagem de utilizadores do macOS.

3. Selecione o círculo no gráfico na parte superior. O **Estado do dispositivo** é apresentado.

    São listados os dispositivos atribuídos ao perfil, além de indicar se o perfil foi implementado com êxito. Note também que apenas lista os dispositivos com a plataforma específica (por exemplo, macOS).

    Feche os detalhes do estado do **Dispositivo.**

4. Selecione o círculo no gráfico na parte inferior. O **Estado do utilizador** é apresentado. 

    São indicados os utilizadores atribuídos ao perfil, além de indicar se o perfil foi implementado com êxito. Note também que apenas indica os utilizadores com a plataforma específica (por exemplo, macOS).

    Feche os detalhes do **Estado do utilizador**.

5. Novamente na lista **Perfis**, selecione um perfil específico. Também pode alterar as propriedades existentes:
    - **Propriedades**: altere o nome ou atualize as definições existentes.
    - **Atribuições**: inclua ou exclua dispositivos que a política deve aplicar. Escolha **Grupos Selecionados** para escolher grupos específicos.
    - **Estado do dispositivo**: são listados os dispositivos atribuídos ao perfil, além de indicar se o perfil foi implementado com êxito. Pode selecionar um dispositivo específico para obter ainda mais detalhes, incluindo as aplicações instaladas.
    - **Estado do utilizador**: Lista os nomes dos utilizadores com dispositivos afetados por este perfil e se o perfil for implementado com sucesso. Pode selecionar um utilizador específico para obter ainda mais detalhes.
    - **Estado por definição**: filtra os resultados ao mostrar as definições individuais no perfil e mostra se a definição foi aplicada com êxito.

## <a name="view-conflicts"></a>Ver os conflitos

Em **Dispositivos**  >  **Todos os dispositivos,** pode ver quaisquer configurações que estejam a causar um conflito. Quando há um conflito, você também vê todos os perfis de configuração que contêm esta configuração. Os administradores podem utilizar esta funcionalidade para ajudar a resolver problemas e corrigir discrepâncias com os perfis.

1. Em Intune, selecione **Todos**  >  **os Dispositivos** > selecione um dispositivo existente na lista. Um utilizador final pode obter o nome do dispositivo a partir da aplicação Portal da Empresa.
2. Selecione **Configuração do dispositivo**. É apresentada uma lista de todas as políticas de configuração que se aplicam ao dispositivo.
3. Selecione a política. São apresentadas todas as definições existentes nessa política que se aplicam ao dispositivo. Se um dispositivo apresentar o estado **Conflito**, selecione essa linha. Na nova janela, pode ver todos os perfis e os nomes dos perfis que têm a definição a causar o conflito.

Agora que já sabe qual é a definição em conflito e as políticas que incluem essa definição, deverá ser mais fácil resolver o conflito. 

## <a name="device-firmware-configuration-interface-profile-reporting"></a>Relatório de perfil de interface de configuração de firmware do dispositivo

> [!WARNING]
> Está atualmente a ser criado um controlo dos perfis dFCI. Enquanto o DFCI estiver em pré-visualização pública, os dados de monitorização podem estar em falta ou incompletos.

Os perfis DFCI são relatados numa base por definição, tal como outros perfis de configuração do dispositivo. Dependendo do suporte do fabricante ao DFCI, algumas definições podem não se aplicar.

Com as definições de perfil dFCI, pode ver os seguintes estados:

- **Conformidade:** Este estado mostra quando um valor de definição no perfil corresponde à regulação do dispositivo. Este estado pode acontecer nos seguintes cenários:

  - O perfil DFCI conseguiu configurar a definição no perfil.
  - O dispositivo não tem a função de hardware controlada pela definição, e a definição de perfil é **desativada**.
  - A UEFI não permite que o DFCI desative a funcionalidade e a definição de perfil está **ativada**.
  - O dispositivo carece do hardware para desativar a funcionalidade e a definição de perfil está **ativada**.

- **Não Aplicável**: Este estado mostra quando um valor de definição no perfil está **ativado**, e a definição correspondente no dispositivo não é encontrada. Este estado pode acontecer se o hardware do dispositivo não tiver a funcionalidade.

- **Não conforme:** Este estado mostra quando um valor de definição no perfil não corresponde à regulação do dispositivo. Este estado pode acontecer nos seguintes cenários:

  - A UEFI não permite que o DFCI desative uma definição, e a definição de perfil é **desativada**.
  - O dispositivo carece do hardware para desativar a funcionalidade e a definição de perfil é **desativada**.
  - O dispositivo não tem a mais recente versão do firmware DFCI.
  - O DFCI foi desativado antes de ser matriculado em Intune utilizando um controlo local de "opt-out" no menu UEFI.
  - O dispositivo foi matriculado em Intune fora da matrícula do Piloto Automático.
  - O dispositivo não foi registado em Autopilot por um CSP da Microsoft, nem registado diretamente pelo OEM.

## <a name="next-steps"></a>Passos seguintes

[Questões comuns, questões e resoluções com perfis de dispositivos](device-profile-troubleshoot.md)  
[Políticas e perfis de resolução de problemas e em Intune](troubleshoot-policies-in-microsoft-intune.md)
