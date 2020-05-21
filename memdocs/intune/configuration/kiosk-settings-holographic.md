---
title: Definições de quiosque para Windows Holographic para Negócios na Microsoft Intune - Azure Microsoft Docs
description: Configure o seu Windows Holographic para dispositivos Empresariais como quiosques de aplicação única e multi-aplicações, personalize o menu inicial, adicione aplicações, mostre a barra de tarefas e configure um navegador web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556103"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Windows Holographic para configurações de dispositivos empresariais para funcionar como um quiosque em Intune

Em dispositivos com o Windows Holographic for Business, pode configurar estes dispositivos para serem executados em modo de quiosque de uma aplicação ou modo de quiosque de várias aplicações. Algumas funcionalidades não são suportadas no Windows Holographic for Business.

Este artigo lista e descreve as diferentes definições que pode controlar no Windows Holographic para dispositivos Business. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para configurar o seu Windows Holographic para dispositivos Empresariais funcionarem no modo quiosque.

Como administrador intune, pode criar e atribuir estas definições aos seus dispositivos.

Para saber mais sobre a funcionalidade do quiosque Windows em Intune, consulte as definições do [quiosque configurar](kiosk-settings.md).

## <a name="before-you-begin"></a>Antes de começar

- [Crie um perfil](kiosk-settings.md#create-the-profile)de configuração do dispositivo de quiosque do Windows 10 .

  Quando cria um perfil de configuração do dispositivo de quiosque do Windows 10, existem mais configurações do que as listadas neste artigo. As definições deste artigo são suportadas no Windows Holographic para dispositivos Empresariais.

- Este perfil de quiosque está diretamente relacionado com o perfil de restrições do dispositivo que cria utilizando as [definições](device-restrictions-windows-holographic.md#microsoft-edge-browser)do quiosque do Microsoft Edge . Em resumo:

  1. Crie este perfil de quiosque para executar o dispositivo no modo quiosque.
  2. Crie o perfil de restrições do dispositivo e configure [funcionalidades](device-restrictions-windows-holographic.md#microsoft-edge-browser)e definições específicas permitidas no Microsoft Edge.

> [!IMPORTANT]
> Certifique-se de atribuir este perfil de quiosque aos mesmos dispositivos que o seu [perfil Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Aplicativo único, quiosque de ecrã completo

Executa apenas uma aplicação no dispositivo. Quando um utilizador inicia sessão, uma aplicação específica é iniciada. Este modo também impede que o utilizador abra novas aplicações ou mude a aplicação em execução.

- Tipo de início de **sessão do utilizador:** Selecione o tipo de conta que executa a aplicação. As opções são:

  - **Auto logon (Windows 10 versão 1803 e mais recente)**: Não suportado no Windows Holographic for Business.
  - **Conta de utilizador local**: introduza a conta de utilizador local (para o dispositivo). Ou, insira uma conta da Conta Microsoft (MSA) associada à aplicação do quiosque. A conta que introduz entra entra no quiosque.

    Para quiosques em ambientes virados para o público, deve utilizar-se um tipo de utilizador com menos privilégios.

- **Tipo de aplicação**: Selecione **a aplicação Adicionar Loja**.

  - **App para funcionar no modo quiosque**: Selecione uma aplicação da lista.

    Não tem aplicações listadas? Adicione algumas através dos passos indicados em [Aplicações de Cliente](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Quiosque multi-aplicativo

As aplicações neste modo estão disponíveis no menu Iniciar. Estas aplicações são as únicas aplicações que o utilizador pode abrir. Se uma aplicação tem uma dependência de outra aplicação, ambas devem ser incluídas na lista de aplicações permitidas.

- **Target Windows 10 em dispositivos de modo S**: Selecione **No**. O modo S não é suportado no Windows Holographic para Negócios.

- **Tipo de início de sessão do utilizador**: adicione uma ou mais contas de utilizador que poderão utilizar as aplicações que adicionar. As opções são:

  - **Auto logon (Windows 10 versão 1803 e mais recente)**: Não suportado no Windows Holographic for Business.
  - **Contas de utilizador local**: **adicione** a conta de utilizador local (para o dispositivo). A conta que introduz entra entra no quiosque.
  - **Utilizador ou grupo do Microsoft Azure AD (Windows 10, versão 1803 e posterior)**: requer credenciais de utilizador para iniciar sessão no dispositivo. Selecione **Adicionar** para escolher os utilizadores ou grupos do Microsoft Azure AD na lista. Pode selecionar vários utilizadores e grupos. Escolha **Selecionar** para guardar as alterações.
  - **Visitante do HoloLens**: A conta de visitante é uma conta de convidado que não necessita de credenciais ou de autenticação do utilizador, como está descrito em [Shared PC mode concepts (Conceitos de modo de PC partilhado)](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Navegador e Aplicações**: Adicione as aplicações para executar no dispositivo do quiosque. Lembre-se de que pode adicionar várias aplicações.

  - **Navegadores**
    - **Adicione o Microsoft Edge**: O Microsoft Edge é adicionado à grelha de aplicações e todas as aplicações podem ser executadas neste quiosque. Selecione o tipo de modo de quiosque Microsoft Edge:

      - **Modo normal (versão completa do Microsoft Edge)**: Executa uma versão completa do Microsoft Edge com todas as funcionalidades de navegação. Os dados e o estado do utilizador são guardados entre sessões.
      - **Navegação pública (InPrivate)**: Executa uma versão multi-tab do Microsoft Edge InPrivate com uma experiência personalizada para quiosques que funcionam em modo de ecrã completo.

      Para obter mais informações sobre estas opções, consulte [o modo de quiosque do Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Esta definição permite o navegador Microsoft Edge no dispositivo. Para configurar as definições específicas do Microsoft Edge, crie um perfil de restrições de dispositivos **(os**perfis de configuração do dispositivo  >  **Configuration profiles**  >  **Criam o perfil**Windows  >  **10** para a plataforma > restrições de **dispositivos**  >  **Microsoft Edge Browser**). [O Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser) lista os navegadores e descreve o Holographic disponível para configurações de Negócios.

    - **Adicionar navegador de quiosque**: Não suportado no Windows Holographic for Business.

  - **Aplicações**
    - **Adicionar aplicativo de loja**: Selecione uma aplicação existente que adicionou ou implementou para Intune como [Aplicações de Cliente](../apps/apps-add.md), incluindo aplicações LOB. Se não tiver nenhuma aplicação listada, intune suporta muitos tipos de [aplicações](../apps/apps-add.md) que [adiciona ao Intune](../apps/store-apps-windows.md).
    - **Adicionar aplicação Win32**: não suportado no Windows Holographic for Business.
    - **Adicionar por AUMID**: utilize esta opção para adicionar aplicações do Windows de caixa de entrada, como o Bloco de notas ou a Calculadora. Introduza as seguintes propriedades:

      - **Nome da aplicação**: obrigatório. Introduza um nome para a aplicação.
      - **ID do modelo de utilizador da aplicação (AUMID)**: obrigatório. Introduza o ID do modelo de utilizador da aplicação (AUMID) da aplicação Windows. Para obter este ID, veja [Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Localizar o ID do Modelo de Utilizador da Aplicação de uma aplicação instalada).

    - **Lançamento automático**: Opcional. Depois de adicionar as suas aplicações e navegador, selecione uma aplicação ou navegador para abrir automaticamente quando o utilizador fizer a sua investida. Apenas uma única aplicação ou navegador pode ser lançado automaticamente.
    - **Tamanho do mosaico**: obrigatório. Depois de adicionar as suas apps, selecione um tamanho de azulejo sinuoso, pequeno, médio, largo ou grande.

- **Utilize o layout de início alternativo**: Selecione **Sim** para introduzir um ficheiro XML que descreva como as aplicações aparecem no menu inicial, incluindo a ordem das aplicações. Utilize esta opção se precisar de uma personalização adicional no menu Iniciar. O artigo [Customize and export start layout (Personalizar e exportar o esquema do menu Iniciar)](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) dá algumas orientações e inclui um ficheiro XML específico para dispositivos com o Windows Holographic for Business.

- **Barra de tarefas do Windows**: não suportada no Windows Holographic for Business.
- **Permitir o acesso à pasta de downloads**: Não suportado no Windows Holographic for Business.
- **Especificar Janela de Manutenção para Reiniciações**de Aplicações : Não suportado no Windows Holographic for Business.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de quiosque para [Android,](device-restrictions-android.md#kiosk) [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)e Windows 10 e dispositivos [posteriores.](kiosk-settings-windows.md)
