---
title: Configurar definições de e-mail no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Crie um perfil de e-mail no Microsoft Intune e implemente este perfil para o administrador de dispositivos Android, Android Enterprise, iOS, iPadOS e dispositivos Windows. Utilize perfis de e-mail para configurar definições comuns de e-mail, incluindo um servidor de e-mail e métodos de autenticação para se conectar a e-mails corporativos em dispositivos que gere.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9657353dd877b380d506e588934e3f6fd29b51c1
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587031"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Adicionar definições de e-mail a dispositivos com o Intune

O Microsoft Intune inclui várias definições de e-mail que pode implementar em dispositivos da sua organização. Um administrador de TI cria perfis de e-mail com configurações específicas para ligar a um servidor de correio, como o Office 365 e o Gmail. Os utilizadores finais conectam-se, autenticam e sincronizam as suas contas de email organizacionais nos seus dispositivos móveis. Ao criar e implementar um perfil de e-mail, pode confirmar que as definições são padrão em muitos dispositivos. Além disso, pode ajudar a reduzir os pedidos de suporte de utilizadores finais que não sabem quais são as definições de e-mail corretas.

Pode utilizar os perfis de e-mail para configurar as definições de e-mail incorporadas dos seguintes dispositivos:

- Administrador de dispositivos Android na Samsung Knox Standard 4.0 e mais recente
- Android Enterprise
- iOS 8.0 e mais recente
- iPadOS 13.0 e mais recente
- Windows Phone 8.1 e mais recente
- Windows 10 (desktop) e Windows 10 Mobile

Este artigo mostra-lhe como criar um perfil de e-mail no Microsoft Intune. Também inclui ligações para definições mais específicas das diferentes plataformas.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:  

        - **Administrador de dispositivos Android** (apenas Samsung Android Knox Standard)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 e posterior**
        - **Windows Phone 8.1**

    - **Perfil**: Selecione **Email**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **Windows 10: Definições de e-mail para todos os dispositivos Windows 10**.
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

    - [Administrador de dispositivos Android (Samsung Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)
    - [Windows Phone 8.1](email-settings-windows-phone-8-1.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para `US-NC IT Team` `JohnGlenn_ITDepartment`filtrar o perfil a grupos de TI específicos, tais como ou . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="remove-an-email-profile"></a>Remover um perfil de e-mail

Os perfis de e-mail são atribuídos a grupos de dispositivos e não a grupos de utilizadores. Existem diferentes formas de remover um perfil de e-mail de um dispositivo, mesmo quando existe apenas um perfil de e-mail no dispositivo:

- **Opção 1**: Abra o perfil de e-mail **(Perfis** > de configuração de**dispositivos** > selecione o seu perfil) e escolha **Atribuições**. O separador **Incluir** apresenta os grupos atribuídos ao perfil. Clique com o botão direito do rato no grupo e selecione **Remover**. Não se esqueça de **Guardar** as alterações.

- **Opção 2**: [elimine ou extinga o dispositivo](../remote-actions/devices-wipe.md). Pode utilizar estas ações para remover dados e definições de forma seletiva ou na totalidade.

## <a name="secure-email-access"></a>Proteger o acesso ao e-mail

Pode ajudar a proteger os perfis de e-mail através das seguintes opções:

- **Certificados**: quando cria o perfil de e-mail, seleciona um perfil de certificado criado anteriormente no Intune. Este certificado é conhecido como certificado de identidade. Autentica-se contra um perfil de certificado de confiança ou um certificado de raiz para confirmar que o dispositivo do utilizador está autorizado a ligar-se. O certificado fidedigno é atribuído ao computador que autentica a ligação de e-mail. Normalmente, este computador é o servidor de e-mail nativo.

  Se utilizar a autenticação baseada em certificados para o seu perfil de e-mail, implemente o perfil de e-mail, perfil de certificado e perfil de raiz fidedigno para os mesmos grupos para garantir que cada dispositivo pode reconhecer a legitimidade da sua autoridade de certificado.

  Para obter mais informações sobre como criar e utilizar perfis de certificado no Intune, veja [How to configure certificates with Intune (Como configurar certificados com o Intune)](../protect/certificates-configure.md).

- **Nome e palavra-passe**do utilizador : O utilizador final autentica-se no servidor de correio nativo, inserindo um nome de utilizador e uma palavra-passe. A palavra-passe não existe no perfil de e-mail. Assim, o utilizador final introduz a palavra-passe ao ligar-se ao e-mail.

## <a name="how-intune-handles-existing-email-accounts"></a>Como o Intune processa as contas de e-mail existentes

Se o utilizador já tiver configurado uma conta de e-mail, o perfil de e-mail será atribuído de forma diferente consoante a plataforma.

- **iOS/iPadOS**: É detetado um perfil de e-mail duplicado existente com base no nome do anfitrião e no endereço de e-mail. O perfil de e-mail duplicado impede a atribuição de um perfil do Intune. Neste caso, a aplicação Portal da Empresa notifica o utilizador de que não está em conformidade e solicita ao utilizador final que remova manualmente o perfil configurado. Para ajudar a prevenir este cenário, informe os utilizadores finais para se inscreverem *antes* de instalarem um perfil de e-mail, o que permite ao Intune configurar o perfil.

- **Windows**: um perfil de e-mail duplicado existente é detetado com base no nome de anfitrião e no endereço de e-mail. Intune substitui o perfil de e-mail existente criado pelo utilizador final.

- **Android Samsung Knox Standard**: Um perfil de e-mail duplicado existente é detetado com base no endereço de e-mail, e substitui-o com o perfil Intune. O Android não utiliza o nome do anfitrião para identificar o perfil. Não crie múltiplos perfis de e-mail com o mesmo endereço de e-mail em diferentes anfitriões. Os perfis sobressaem uns aos outros.

- **Perfis**de trabalho android : Intune fornece dois perfis de email de trabalho Android: um para a aplicação Gmail e outro para a aplicação Nine Work. Estas aplicações estão disponíveis na Google Play Store e são instaladas no perfil de trabalho do dispositivo. Estas aplicações não criam perfis duplicados. Ambas as aplicações suportam ligações ao Exchange. Para utilizar a conectividade de e-mail, implemente uma destas aplicações de e-mail nos dispositivos dos seus utilizadores. Em seguida, crie e implemente o perfil de e-mail adequado. Pode utilizar perfis de configuração de email do Gmail e nove que funcionarão tanto para os tipos de registo de Perfil de Trabalho como para os tipos de inscrição do Proprietário do Dispositivo, incluindo a utilização de perfis de certificado em ambos os tipos de configuração de email. Quaisquer políticas do Gmail ou Nove que tenha criado no âmbito da Configuração do Dispositivo para Perfis de Trabalho continuarão a aplicar-se ao dispositivo e não é necessário movê-las para as políticas de configuração de apps. As aplicações de e-mail como o Nine Work podem não ser gratuitas. Reveja os dados de licenciamento da aplicação ou contacte a empresa de aplicações com quaisquer questões. 

## <a name="changes-to-assigned-email-profiles"></a>Alterações a perfis de e-mail atribuídos

Se fizer alterações a um perfil de e-mail atribuído anteriormente, os utilizadores finais poderão ver uma mensagem a pedir que aprovem a reconfiguração das definições de e-mail.

## <a name="next-steps"></a>Passos seguintes

O perfil não estará ativo assim que for criado. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
