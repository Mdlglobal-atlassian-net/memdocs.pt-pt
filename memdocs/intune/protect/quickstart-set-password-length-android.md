---
title: Quickstart - Política de conformidade com palavra-passe para dispositivos Android
titleSuffix: Microsoft Intune
description: Neste arranque rápido, utilizará o Microsoft Intune para definir o comprimento da palavra-passe necessária para dispositivos Android.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 81b4fa08-5333-4c54-9f49-8db5f6984ed2
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7330f50c61679ab91b5f364f718cefcc456435f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329073"
---
# <a name="quickstart-create-a-password-compliance-policy-for-android-devices"></a>Guia de Início Rápido: criar uma política de conformidade de palavra-passe para dispositivos Android

Neste arranque rápido, utilizará o Microsoft Intune para exigir que os utilizadores Android da sua força de trabalho introduzam uma palavra-passe de um comprimento específico antes de o acesso ser concedido a informações sobre os seus dispositivos Android.

Uma política de conformidade de dispositivos do Intune especifica as regras e definições que os dispositivos têm de cumprir para serem considerados conformes. Pode utilizar políticas de conformidade com acesso condicional para permitir ou bloquear o acesso aos recursos da empresa. Também pode obter relatórios de dispositivos e agir relativamente a situações de não conformidade.

> [!IMPORTANT]
> Além das definições da palavra-passe, deve também considerar outras definições de segurança do sistema para proteger a sua força de trabalho. Para obter mais informações, veja [Definições de segurança do sistema](compliance-policy-create-android-for-work.md).

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) como [administrador global](../fundamentals/users-add.md#types-of-administrators) ou administrador de [serviço](../fundamentals/users-add.md#types-of-administrators)intune .

## <a name="create-a-device-compliance-policy"></a>Criar uma política de conformidade do dispositivo

Crie uma política de conformidade com o dispositivo para exigir que os utilizadores Android da sua força de trabalho introduzam uma palavra-passe de um comprimento específico antes de o acesso ser concedido a informações nos seus dispositivos Android.

1. Em Intune, selecione **Dispositivos** > Políticas de **Conformidade** > **Criar Política**.

2. Adicione **Conformidade do Android** como o **Nome**. Adicione também uma **Descrição**.

3. Em **Plataforma**, selecione **Android Enterprise**.

4. Para **o tipo de perfil,** selecione Perfil de **trabalho**.

5. Selecione **Definições** > **Segurança do Sistema** para apresentar o painel **Segurança do Sistema** Android.

6. Para **Palavra-passe obrigatória para desbloquear os dispositivos móveis**, selecione **Exigir**.

7. Para o **tipo de palavra-passe requerida,** selecione **Pelo menos numérico**.

8. Para o comprimento mínimo da **palavra-passe**, introduza **6**.

    ![Captura de ecrã da criação de um grupo no Microsoft Intune](./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png)

9. Quando terminar, selecione **OK** > **OK** > **Criar** para criar a política.

Quando se cria com sucesso a política, aparece na sua lista de políticas de complice do dispositivo.

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não for necessária, elimine a política. Para tal, selecione a política de conformidade e clique em **Eliminar**.

## <a name="next-steps"></a>Próximos passos

Neste início rápido, utilizou o Intune para criar uma política de conformidade para os dispositivos Android da sua força de trabalho para exigir uma palavra-passe de, pelo menos, seis carateres de comprimento. Para obter mais informações sobre a criação de políticas de conformidade, veja [Introdução às políticas de conformidade de dispositivos no Intune](device-compliance-get-started.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: enviar notificações para dispositivos não conformes](quickstart-send-notification.md)
