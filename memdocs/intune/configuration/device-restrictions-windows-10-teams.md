---
title: Restrições de dispositivos team Surface Hub Windows 10 no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Utilize o Intune para adicionar ou configurar as definições de dispositivos Surface Hub que executam o Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429681"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Definições da equipa do Windows 10 para permitir ou restringir funcionalidades em dispositivos Surface Hub utilizando Intune

Este artigo mostra-lhe as definições de restrições do dispositivo Microsoft Intune que pode configurar para dispositivos que executam o Windows 10 Team, incluindo os dispositivos Surface Hub.

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil do dispositivo](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Aplicações e experiência

Estas definições utilizam o [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Ecrã de despertar quando alguém na sala**: O **bloco** impede que o ecrã acorde automaticamente quando o sensor deteta alguém na sala. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Informações de reunião exibidas no ecrã de boas-vindas**: Escolha as informações mostradas no azulejo do ecrã welcome. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Organizador e só tempo**
  - **Organizador, tempo e assunto (assunto escondido para reuniões privadas)**
- URL de imagem de fundo de **ecrã de acolhimento**: Introduza o URL de uma imagem .png que deseja como um fundo personalizado no ecrã **welcome** nos dispositivos da Equipa do Windows 10. A imagem deve estar em formato PNG, e o URL deve começar com `https://` .
- **Auto-lançamento Connect**: **O bloco** impede que a aplicação Connect abra automaticamente quando uma projeção é iniciada. Se bloqueados, os utilizadores podem lançar manualmente a aplicação Connect a partir das definições do Hub. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Sugestões de início**de sessão : **O bloco** desativa o preenchimento automático do diálogo de início de sessão com convites de reuniões agendadas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Minhas reuniões e ficheiros**: **Bloco** desativa a funcionalidade **Minhas reuniões e ficheiros** no menu Iniciar. Esta funcionalidade mostra as reuniões e ficheiros do utilizador inscrito saqueado do Office 365. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="azure-operational-insights"></a>Informações operacionais do Azure

- **Azure Operational Insights**: **Enable** recolhe, armazena e analisa dados de registo de dispositivos da Equipa Windows 10 com Insights Operacionais Azure. O Azure Operational Insights faz parte da suite do Microsoft Operations Manager. Introduza o ID do **espaço de trabalho** e a chave **workspace** para ligar aos insights operacionais do Azure.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode não recolher estes dados.

## <a name="maintenance"></a>Manutenção

Estas definições utilizam o [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Janela de manutenção para atualizações**: **Ativar** cria uma janela de manutenção quando as atualizações podem ser instaladas. Introduza a janela de manutenção Hora de **início**, e a **duração em horas**, de 1 a 5 horas.

  Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="session"></a>Sessão

Estas definições utilizam o [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Volume**: Introduza o valor de volume predefinido para uma nova sessão, de 0 a 100. Quando deixada em branco, intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode definir o volume para 45.
- **Tempo de**paragem do ecrã : Introduza o número de minutos até o ecrã hub se desligar.
- Horário da **sessão**: Introduza o número de minutos até que a sessão se estime.
- **Tempo**de repouso : Introduza o número de minutos até o Centro entrar no modo de sono.
- Resumo da **sessão**: **O bloco** impede os utilizadores de retomarem uma sessão quando a sessão se esgotar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="wireless-projection"></a>Projeção sem fios

Estas definições utilizam o [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **PIN para projeção sem fios**: **Exija que** os utilizadores introduzam um PIN antes de utilizar as funcionalidades de projeção sem fios no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Projeção sem fios Miracast**: **O bloco** impede a utilização de dispositivos com miracast para projetar. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Canal de projeção sem fios Miracast**: Selecione o canal Miracast para estabelecer a ligação.

## <a name="next-steps"></a>Próximos passos

Para mais informações, consulte [Como configurar as definições](device-restrictions-configure.md)de restrição do dispositivo .

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).
