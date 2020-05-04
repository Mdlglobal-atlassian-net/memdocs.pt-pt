---
title: Quickstart - Criar um perfil de dispositivo de e-mail para dispositivos iOS/iPadOS
titleSuffix: Microsoft Intune
description: Saiba como usar o Microsoft Intune para criar um perfil de dispositivo de e-mail para que os dispositivos iOS/iPadOS possam ligar-se de forma segura ao e-mail da empresa.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af7657eb89df14e8429a81616e76d81a5a9ac5c1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327428"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Quickstart: Criar um perfil de dispositivo de e-mail para iOS/iPadOS

Neste arranque rápido, você verá como criar um perfil de dispositivo de e-mail para dispositivos iOS/iPadOS. Este perfil especifica as definições necessárias para que a aplicação de e-mail incorporada no dispositivo iOS/iPadOS se conectem ao e-mail da empresa. Os perfis de dispositivo de e-mail ajudam a padronizar as definições em vários dispositivos e permitem que os utilizadores finais acedam ao e-mail da empresa nos respetivos dispositivos pessoais sem precisarem de realizar qualquer configuração. Para salvaguardar ainda mais o seu e-mail, pode utilizar um perfil de e-mail para determinar se os dispositivos estão em conformidade e, em seguida, configurar o Acesso Condicional para permitir apenas dispositivos compatíveis para aceder a emails. Para obter detalhes sobre perfis de e-mail, veja [Como configurar definições de e-mail no Microsoft Intune](email-settings-configure.md).

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como administrador global ou administrador de serviço intune. Se criou uma Subscrição de Avaliação do Intune, a conta com a qual criou a subscrição é de Administrador global.

## <a name="create-an-iosipados-email-profile"></a>Criar um perfil de e-mail iOS/iPadOS

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione e vá aos perfis de**configuração** > de **dispositivos** > **Criar perfil**.
   ![Criar um perfil de e-mail para iOS/iPadOS em Intune](./media/quickstart-email-profile/ios-create-profile.png)

3. Introduza as seguintes propriedades:
   - **Plataforma**: Selecione **iOS/iPadOS**
   - **Perfil**: **Selecione E-mail**
  
4. Selecione **Criar**.

5. No Básico, insira as **seguintes**propriedades:
   - **Nome**: introduza um nome descritivo para o novo perfil. Neste exemplo, introduza **O iOS necessita de um e-mail de trabalho**.
   - **Descrição**: Enter **Require iOS/iPadOS dispositivos para usar e-mail de trabalho**


        ![Criar um perfil de e-mail para utilização com dispositivos iOS/iPadOS em Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

6. Selecione **Seguinte**.

7. Nas definições de **Configuração,** introduza as seguintes definições (deixe as predefinições para outras definições):
   - **Servidor de e-mail**: neste início rápido, introduza **outlook.office365.com**. Esta definição especifica a localização de Troca (URL) do servidor de e-mail que a aplicação de correio iOS/iPadOS utilizará para se ligar ao e-mail.
   - **Nome da conta**: introduza o **E-Mail da Empresa**.
   - **Atributo de nome de utilizador do AAD**: este nome é o atributo que o Intune obtém do Azure Active Directory (Azure AD). O Intune gera dinamicamente o nome de utilizador para este perfil através deste nome. Para este arranque rápido, assumimos que queremos que o **Nome Principal** do Utilizador seja user1@contoso.comusado como nome de utilizador para o perfil (por exemplo, ).
   - **Atributo de endereço de e-mail do AAD**: esta definição é o endereço de e-mail do Azure AD que será utilizado para iniciar sessão no Exchange. Neste início rápido, selecione **Nome Principal de Utilizador**.
   - **Método de autenticação**: neste início rápido, selecione **Nome de utilizador e palavra-passe**. (Também pode escolher **Certificado** se já tiver configurado um certificado para Intune.)

8. Selecione **Seguinte**.

9. Nas **etiquetas de âmbito** (opcional), Selecione **Seguinte**. Não usaremos uma etiqueta de mira para este perfil.

10. Em **Atribuições,** utilize a entrega para **Atribuir** e selecione todos os utilizadores e todos **os dispositivos**.  Em seguida, selecione **Next**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. 

## <a name="clean-up-resources"></a>Limpar recursos

Se não pretender utilizar o perfil que criou para tutoriais ou testes adicionais, pode apagá-lo agora.

1. Em Intune, selecione**configuração do dispositivo** > de**dispositivos**.
2. Selecione o perfil de teste que criou, **o iOS/iPadOS requer e-mail**de trabalho e, em seguida, selecione **Delete**. 

## <a name="next-steps"></a>Passos seguintes

Neste arranque rápido, criou um perfil de e-mail para dispositivos iOS/iPadOS. Agora pode utilizar este perfil para determinar se um dispositivo iOS/iPadOS está em conformidade, criando uma política de conformidade que marca como não conforme qualquer dispositivo iOS/iPadOS que não corresponda ao perfil. Para maior proteção, pode criar uma política de Acesso Condicional que bloqueie dispositivos iOS/iPadOS não conformes de aceder a e-mails. Para saber mais sobre as políticas de conformidade de dispositivos, veja [Introdução às políticas de conformidade de dispositivos no Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Tutorial – Proteger o e-mail do Exchange Online em dispositivos geridos](../protect/tutorial-protect-email-on-enrolled-devices.md)
