---
title: 'Guia de Início Rápido: inscrever o seu dispositivo Windows 10 Desktop no Microsoft Intune'
description: 'Guia de Início Rápido: utilizar o Portal da Empresa para inscrever o seu dispositivo Windows 10 Desktop no Microsoft Intune'
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f70c8487d9cb30b2a7cced63e6e019541f73704
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327060"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Guia de Início Rápido: inscrever o seu dispositivo com o Windows 10

Neste guia de início rápido, irá assumir a função de utilizador do Intune e inscrever o seu dispositivo com o Windows 10 no Microsoft Intune. Em seguida, você vai voltar a Intune e confirmar o dispositivo matriculado.

A inscrição dos seus dispositivos no Microsoft Intune permite que os seus dispositivos Windows 10 tenham acesso aos dados seguros da sua organização, incluindo e-mails, ficheiros e outros recursos. Isto aplica-se a computadores com o Windows 10 e a dispositivos móveis com o Windows 10 Mobile. A inscrição dos dispositivos ajuda a proteger o seu acesso e o da sua organização e ajuda a manter os dados de trabalho separados dos seus dados pessoais.

> [!TIP]
> Descubra o que acontece quando [inscreve o seu dispositivo no Intune](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md) e o que isso significa para as [informações no dispositivo](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Pré-requisitos

- Subscrição do Microsoft Intune – [inscreva-se numa conta de avaliação gratuita](../fundamentals/free-trial-sign-up.md).
- Para concluir este guia de início rápido, tem de concluir os passos para [configurar a inscrição automática no Intune](quickstart-setup-auto-enrollment.md).

## <a name="confirm-your-windows-10-desktop-version"></a>Confirmar a versão do Windows 10 Desktop

Antes de inscrever o seu dispositivo Windows 10 Desktop, tem de confirmar a versão do Windows que instalou.

1. Clique com o botão direito do rato no ícone **Iniciar** do Windows e selecione **Definições** para apresentar as opções de Definições do Windows.

   ![Captura de ecrã a mostrar as Definições do Windows – Sistema](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Selecione **Sistema** > **Acerca de**. 

   ![Captura de ecrã a mostrar as suas definições de sistema](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Também pode escrever a expressão "Sobre o seu PC" na **barra de pesquisa** e, em seguida, selecionar **Sobre o seu PC**.

3. Na janela **Definições**, verá uma lista com as **especificações do Windows** do seu PC. Nessa lista, localize a **Versão**.

4. Confirme se a **Versão** do Windows 10 é a **1607 ou superior**.

    > [!IMPORTANT]
    > Os passos apresentados neste guia de início rápido aplicam-se à versão **1607 ou superior** do Windows 10. Se a sua versão for a **igual ou inferior à 1511**, prossiga a partir [destes passos](../user-help/enroll-windows-10-device.md).  

## <a name="enroll-windows-10-desktop"></a>Inscrever o Windows 10 Desktop

1. Regresse às Definições do Windows e selecione **Contas**.

   ![Captura de ecrã a mostrar as suas definições de sistema – Contas](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Selecione **Aceder a profiss./escolar** > **Ligar**.

    ![Selecione Contas, Aceder a profiss./escolar](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Inicie sessão no Intune com a sua conta profissional ou escolar e, em seguida, selecione **Seguinte**. Se seguiu a criação de [um utilizador e atribuía uma licença](../fundamentals/quickstart-create-user.md) de arranque rápido, pode iniciar sessão com a conta de utilizador que criou.

    > [!NOTE]
    > Se estiver a configurar uma conta ".onmicrosoft.com", a conta de utilizador apresentará o domínio **.onmicrosoft.com** como parte do respetivo endereço. 

   ![Introduza a sua conta escolar ou profissional](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    Verá uma mensagem indicando que a sua empresa ou escola está a registar o seu dispositivo.

4. Quando vires o **"Estás pronto"!** selecione **Concluído**. Acabou-se.

5. Agora verá a conta adicionada como parte das definições **Aceder a profiss./escolar** no seu Ambiente de Trabalho do Windows.

   ![Captura de ecrã a mostrar a conta recentemente adicionada](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Se seguiu os passos anteriores, mas ainda não consegue aceder à sua conta de e-mail de trabalho ou escola e ficheiros, siga os passos em passos de resolução de [problemas a seguir se vir o trabalho de acesso ou a escola](../user-help/troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school).

## <a name="confirm-your-device-enrollment-in-intune"></a>Confirmar a inscrição do dispositivo no Intune

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como administrador global ou administrador de serviço intune.
2. Selecione **Dispositivos** > **Todos os dispositivos** para visualizar os dispositivos matriculados no Intune.
3. Verifique se tem um dispositivo adicional inscrito no Intune.

   ![Captura de ecrã a mostrar dispositivos inscritos no Intune](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Limpar recursos

Para anular a inscrição do seu dispositivo Windows, veja [Remover o seu dispositivo Windows da gestão](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Próximos passos

Neste guia de início rápido, aprendeu como inscrever um dispositivo com o Windows 10 no Intune. Pode aprender outras formas de inscrição de dispositivos em todas as plataformas. Para obter mais informações sobre como utilizar dispositivos com o Intune, veja [Utilizar dispositivos geridos para trabalhar](../user-help/use-managed-devices-to-get-work-done.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: definir um comprimento da palavra-passe obrigatório para dispositivos Android](../protect/quickstart-set-password-length-android.md)
