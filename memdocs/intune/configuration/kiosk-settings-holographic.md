---
title: Definições de quiosque para Windows Holographic para Negócios na Microsoft Intune - Azure Microsoft Docs
description: Configure o seu Windows Holographic para dispositivos Empresariais como quiosques de aplicação única e multi-aplicações, personalize o menu inicial, adicione aplicações, mostre a barra de tarefas e configure um navegador web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18de92792582d4c6753bc8657c56d73fa1509788
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359145"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Windows Holographic para configurações de dispositivos empresariais para funcionar como um quiosque em Intune

Em dispositivos com o Windows Holographic for Business, pode configurar estes dispositivos para serem executados em modo de quiosque de uma aplicação ou modo de quiosque de várias aplicações. Algumas funcionalidades não são suportadas no Windows Holographic for Business.

Este artigo lista e descreve as diferentes definições que pode controlar no Windows Holographic para dispositivos Business. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para configurar o seu Windows Holographic para dispositivos Empresariais funcionarem no modo quiosque.

Como administrador intune, pode criar e atribuir estas definições aos seus dispositivos.

Para saber mais sobre a funcionalidade do quiosque Windows em Intune, consulte as definições do [quiosque configurar](kiosk-settings.md).

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](kiosk-settings.md#create-the-profile)

## <a name="single-full-screen-app-kiosks"></a>Quiosques de uma aplicação em ecrã inteiro

Ao escolher o modo de quiosque de uma aplicação, introduza as seguintes definições:

- **Tipo de início de sessão de utilizador**: selecione **Conta de utilizador local** para introduzir a conta de utilizador local (no dispositivo) ou a Conta Microsoft associada à aplicação de quiosque. Os tipos de conta de utilizador de **início de sessão automático** não são suportados pelo Windows Holographic for Business.

- **Tipo de aplicação**: selecione **Aplicação da Loja**.

- **Aplicação a executar no modo de quiosque**: escolha **Adicionar uma aplicação da loja** e selecione uma aplicação na lista.

    Não tem aplicações listadas? Adicione algumas através dos passos indicados em [Aplicações de Cliente](../apps/apps-add.md).

    Selecione **OK** para guardar as alterações.

## <a name="multi-app-kiosks"></a>Quiosques de várias aplicações

As aplicações neste modo estão disponíveis no menu Iniciar. Estas aplicações são as únicas aplicações que o utilizador pode abrir. Ao escolher o modo de quiosque de várias aplicações, introduza as seguintes definições:

- **Dispositivos Windows 10 no modo S de destino**: escolha **Não**. O modo S não é suportado no Windows Holographic para Negócios.

- **Tipo de início de sessão do utilizador**: adicione uma ou mais contas de utilizador que poderão utilizar as aplicações que adicionar. As opções são: 

  - **Início de sessão automático**: não suportado no Windows Holographic for Business.
  - **Contas de utilizador local**: **adicione** a conta de utilizador local (para o dispositivo). A conta que introduzir serve para iniciar sessão no quiosque.
  - **Utilizador ou grupo do Microsoft Azure AD (Windows 10, versão 1803 e posterior)** : requer credenciais de utilizador para iniciar sessão no dispositivo. Selecione **Adicionar** para escolher os utilizadores ou grupos do Microsoft Azure AD na lista. Pode selecionar vários utilizadores e grupos. Escolha **Selecionar** para guardar as alterações.
  - **Visitante do HoloLens**: A conta de visitante é uma conta de convidado que não necessita de credenciais ou de autenticação do utilizador, como está descrito em [Shared PC mode concepts (Conceitos de modo de PC partilhado)](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Aplicações**: adicione as aplicações que quer executar no dispositivo de quiosque. Lembre-se de que pode adicionar várias aplicações.

  - **Adicionar aplicativos Store**: Selecione uma aplicação existente que adicionou ou implementou para Intune como [Aplicações de Cliente](../apps/apps-add.md), incluindo aplicações LOB. Se não tiver nenhuma aplicação listada, intune suporta muitos tipos de [aplicações](../apps/apps-add.md) que [adiciona ao Intune](../apps/store-apps-windows.md).
  - **Adicionar aplicação Win32**: não suportado no Windows Holographic for Business.
  - **Adicionar por AUMID**: utilize esta opção para adicionar aplicações do Windows de caixa de entrada. Introduza as seguintes propriedades: 

    - **Nome da aplicação**: obrigatório. Introduza um nome para a aplicação.
    - **ID do modelo de utilizador da aplicação (AUMID)** : obrigatório. Introduza o ID do modelo de utilizador da aplicação (AUMID) da aplicação Windows. Para obter este ID, veja [Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Localizar o ID do Modelo de Utilizador da Aplicação de uma aplicação instalada).
    - **Tamanho do mosaico**: obrigatório. Escolha um tamanho de mosaico da aplicação: Pequeno, Médio, Largo ou Grande.

- **Definições do browser do quiosque**: não suportado no Windows Holographic for Business.

- **Utilizar o esquema do menu Iniciar alternativo**: escolha **Sim** para introduzir um ficheiro XML que descreva como as aplicações são apresentadas no menu Iniciar, incluindo a ordem das aplicações. Utilize esta opção se precisar de uma personalização adicional no menu Iniciar. O artigo [Customize and export start layout (Personalizar e exportar o esquema do menu Iniciar)](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) dá algumas orientações e inclui um ficheiro XML específico para dispositivos com o Windows Holographic for Business.

- **Barra de tarefas do Windows**: não suportada no Windows Holographic for Business.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de quiosque para [Android,](device-restrictions-android.md#kiosk) [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)e Windows 10 e dispositivos [posteriores.](kiosk-settings-windows.md)
