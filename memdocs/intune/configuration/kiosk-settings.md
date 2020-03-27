---
title: Definições de quiosque para Windows e dispositivos holográficos no Microsoft Intune - Azure Microsoft Docs
description: Configure o seu Windows 10 (e mais tarde) e o Windows Holographic para dispositivos Empresariais como quiosques de aplicações únicas e multi-aplicações, personalize o menu inicial, adicione apps, mostre a barra de tarefas e configure um navegador web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 778ce3e6d069347522a98977da65d651e059e41c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327387"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Windows 10 e Windows Holographic para configurações de dispositivos empresariais funcionam como um quiosque dedicado usando Intune

Nos dispositivos Windows 10, utilize o Intune para executar dispositivos como um quiosque, por vezes conhecido como um dispositivo dedicado. Um dispositivo em modo quiosque pode executar uma aplicação, ou executar muitas aplicações. Você pode mostrar e personalizar um menu inicial, adicionar diferentes aplicações, incluindo aplicações Win32, adicionar uma página inicial específica a um navegador web, e muito mais. 

Esta funcionalidade aplica-se a:

- Windows 10 e posterior
- Windows Holographic for Business

Para criar perfis de quiosque para outras plataformas, consulte o administrador de [dispositivos Android,](device-restrictions-android.md#kiosk) [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)e [iOS/iPadOS.](device-restrictions-ios.md#kiosk)

O Intune suporta um perfil de quiosque por dispositivo. Se precisar de vários perfis de quiosque num só dispositivo, poderá utilizar um [OMA-URI personalizado](custom-settings-windows-10.md).

Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, empurre ou implemente estas definições para grupos da sua organização.

Este artigo mostra-lhe como criar um perfil de configuração do dispositivo. Para obter uma lista de todas as definições e o que fazem, consulte as definições do [quiosque do Windows 10](kiosk-settings-windows.md) e o Windows [Holographic para as definições](kiosk-settings-holographic.md)do quiosque de negócios .

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
   - **Plataforma**: selecione **Windows 10 e posterior**
   - **Tipo de perfil**: Selecione **Quiosque**

4. Em **Definições,** selecione um **modo de quiosque**. O **modo de quiosque** identifica o tipo de modo de quiosque suportado pela política. As opções incluem:

    - **Não configurado** (predefinição): a política não ativa o modo de quiosque.
    - **Quiosque de uma aplicação de ecrã inteiro**: o dispositivo é executado como uma única conta de utilizador e bloqueia-a para uma única aplicação da Loja. Quando o utilizador inicia sessão, é iniciada uma aplicação específica. Este modo também impede que o utilizador abra novas aplicações ou mude a aplicação em execução.
    - **Quiosque de várias aplicações**: o dispositivo executa várias aplicações da Loja, aplicações Win32 ou aplicações do Windows da caixa de entrada através do ID do Modelo de Utilizador da Aplicação (AUMID). Apenas as aplicações que adicionar estarão disponíveis no dispositivo.

        A vantagem de um quiosque de várias aplicações ou dispositivos de objetivo fixo é o facto de proporcionar uma experiência fácil de compreender pelos utilizadores através do acesso às aplicações de que precisam. E, removendo também da sua visão as aplicações de que não precisam.

    Para uma lista de todas as configurações, e o que fazem, veja:
      - [Definições de quiosque do Windows 10](kiosk-settings-windows.md)
      - [Windows Holographic para configurações de quiosque de negócios](kiosk-settings-holographic.md)

5. Assim que terminar, selecione **OK** > **Criar** para guardar as alterações.

O perfil é criado e mostrado na lista de perfis. Em seguida, [atribua](device-profile-assign.md) o perfil.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Pode criar perfis de quiosque para dispositivos que executem as seguintes plataformas:

- [Administrador de dispositivos Android](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)
- [iOS/iPadOS](device-restrictions-ios.md#kiosk)
- [Windows 10 e posterior](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
