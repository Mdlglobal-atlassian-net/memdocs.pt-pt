---
title: Definições de quiosque para Windows e dispositivos holográficos no Microsoft Intune - Azure Microsoft Docs
description: Configure o seu Windows 10 (e mais tarde) e o Windows Holographic para dispositivos Empresariais como quiosques de aplicações únicas e multi-aplicações, personalize o menu inicial, adicione apps, mostre a barra de tarefas e configure um navegador web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a56aa9f1953a1886b0736c5a3d1c0bfbd10853a1
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401540"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Windows 10 e Windows Holographic para configurações de dispositivos empresariais funcionam como um quiosque dedicado usando Intune

Nos dispositivos Windows 10, utilize o Intune para executar dispositivos como um quiosque, por vezes conhecido como um dispositivo dedicado. Um dispositivo em modo quiosque pode executar uma aplicação, ou executar muitas aplicações. Você pode mostrar e personalizar um menu inicial, adicionar diferentes aplicações, incluindo aplicações Win32, adicionar uma página inicial específica a um navegador web, e muito mais. 

Esta funcionalidade aplica-se a:

- Windows 10 e posterior
- Windows Holographic for Business

Para criar perfis de quiosque para outras plataformas, consulte o administrador de [dispositivos Android,](device-restrictions-android.md#kiosk) [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)e [iOS/iPadOS.](device-restrictions-ios.md#kiosk)

O Intune suporta um perfil de quiosque por dispositivo. Se precisar de vários perfis de quiosque num só dispositivo, poderá utilizar um [OMA-URI personalizado](custom-settings-windows-10.md).

Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, empurre ou implemente estas definições para grupos da sua organização.

Este artigo mostra-lhe como criar um perfil de configuração do dispositivo. Para obter uma lista de todas as definições e o que fazem, consulte as definições do [quiosque do Windows 10](kiosk-settings-windows.md) e o Windows [Holographic para as definições](kiosk-settings-holographic.md)do quiosque de negócios .

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

   - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
   - **Perfil**: Selecione **Quiosque**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Em **configurações de configuração**  >  **Selecione um modo de quiosque,** escolha o tipo de modo de quiosque suportado pela apólice. As opções incluem:

    - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição. A apólice não permite o modo de quiosque.
    - **Quiosque de uma aplicação de ecrã inteiro**: o dispositivo é executado como uma única conta de utilizador e bloqueia-a para uma única aplicação da Loja. Quando o utilizador inicia sessão, é iniciada uma aplicação específica. Este modo também impede que o utilizador abra novas aplicações ou mude a aplicação em execução.
    - **Quiosque de várias aplicações**: o dispositivo executa várias aplicações da Loja, aplicações Win32 ou aplicações do Windows da caixa de entrada através do ID do Modelo de Utilizador da Aplicação (AUMID). Apenas as aplicações que adicionar estarão disponíveis no dispositivo.

        A vantagem de um quiosque de várias aplicações ou dispositivos de objetivo fixo é o facto de proporcionar uma experiência fácil de compreender pelos utilizadores através do acesso às aplicações de que precisam. E, removendo também da sua visão as aplicações de que não precisam.

    Para uma lista de todas as configurações, e o que fazem, veja:

      - [Definições de quiosque do Windows 10](kiosk-settings-windows.md)
      - [Windows Holographic para configurações de quiosque de negócios](kiosk-settings-holographic.md)

8. Selecione **Seguinte**.

9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupo de utilizadores que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

Da próxima vez que cada dispositivo entrar, a apólice é aplicada.

## <a name="next-steps"></a>Passos seguintes

Depois de atribuído o [perfil,](device-profile-assign.md) [monitorize o seu estado](device-profile-monitor.md).

Pode criar perfis de quiosque para dispositivos que executem as seguintes plataformas:

- [Administrador de dispositivos Android](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 e posterior](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
