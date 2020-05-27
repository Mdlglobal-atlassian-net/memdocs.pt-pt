---
title: Mover dispositivos Android de administrador de dispositivo para gestão de perfis de trabalho
titleSuffix: Microsoft Intune
description: Mova os dispositivos Android do administrador do dispositivo para a gestão de perfis de trabalho em Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd9741cfa8cf9edd03d723e63ed1936e1c986d08
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989064"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Mover dispositivos Android de administrador de dispositivo para gestão de perfis de trabalho

Pode ajudar os utilizadores a mover os seus dispositivos Android do administrador do dispositivo para a gestão de perfis de trabalho, utilizando a definição de conformidade para **dispositivos Block geridos com o administrador**do dispositivo . Esta definição permite-lhe tornar os dispositivos incompatíveis se forem geridos com o administrador do dispositivo. 

Quando os utilizadores virem que estão fora de conformidade por esta razão, podem tocar no **Resolve**. Serão levados para uma lista de verificação que os guiará através de:
1. Não se matriculando na gestão do administrador de dispositivos
2. Matricular-se na gestão do perfil de trabalho
3. Resolver quaisquer problemas de conformidade. 

## <a name="prerequisites"></a>Pré-requisitos

- Os utilizadores devem ter [dispositivos inscritos](android-enroll-device-administrator.md) para administrador de dispositivos Android com a versão 5.0.4720.0 do Portal da Empresa Android.
- Configurar a gestão do perfil de trabalho android [ligando a sua conta de inquilino Intune à sua conta Android Enterprise](connect-intune-android-enterprise.md).
- [Detete](android-work-profile-enroll.md) a inscrição no perfil de trabalho do Android Enterprise para o grupo de utilizadores que estão a mudar-se para o perfil de trabalho android.
- Considere aumentar os limites do seu dispositivo de utilizador. Ao não inscrever dispositivos da gestão do administrador do dispositivo, os registos do dispositivo podem não ser imediatamente removidos. Para fornecer almofada durante este período, poderá ser necessário aumentar a capacidade limite do dispositivo para que os utilizadores possam inscrever-se na gestão do perfil de trabalho.
  - [Configure as definições](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) do dispositivo de Diretório Ativo Azure para o número máximo de dispositivos por utilizador.
  - Ajuste as restrições de limitação do [dispositivo Intune,](enrollment-restrictions-set.md#create-a-device-limit-restriction) estabelecendo o limite do Dispositivo. 

## <a name="create-device-compliance-policy"></a>Criar a política de conformidade do dispositivo

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione As políticas de conformidade dos **dispositivos**criam políticas de  >  **Compliance policies**  >  **Policies**  >  **criação de políticas**.

    ![Criar política](./media/android-move-device-admin-work-profile/create-policy.png)

2. Na página **Criar uma página de política,** definir **Plataforma** para administrador **de dispositivos Android**  >  **Criar**.
3. Na página **Basics,** digite o **nome** e **a descrição**  >  **seguinte**.

    ![Página básica](./media/android-move-device-admin-work-profile/basics.png)
    
4. Na página de definições de **Conformidade,** na secção Saúde do **Dispositivo,** delineie **os dispositivos Block geridos com o administrador** do dispositivo para **Yes**  >  **Next**.

    ![Dispositivos de bloco](./media/android-move-device-admin-work-profile/block-devices.png)

5. Na página **Locais,** pode adicionar localizações se quiser > **Seguinte**.

6. No separador **Ações para o incumprimento,** pode configurar as [ações disponíveis para o incumprimento](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) para personalizar a experiência final do utilizador para este fluxo.

    ![Ações de incumprimento](media/android-move-device-admin-work-profile/noncompliance-actions.png)

    Estas são algumas ações a considerar:

    - **Marque**o dispositivo sem conformidade : Por defeito, esta ação está definida para zero (0) dias, marcando os dispositivos como não conformes imediatamente. A alteração desta situação para um maior número de dias proporciona aos utilizadores um período de carência no qual podem ver o fluxo para passar para a gestão do perfil de trabalho sem ainda serem marcados como incompatíveis. Por exemplo, defini-lo para 14 dias daria aos utilizadores duas semanas para passarem de administrador de dispositivo para gestão de perfil de trabalho sem o risco de perder o acesso aos recursos.
    - **Envie notificação push ao utilizador final**: Configure isto para enviar notificações push para os dispositivos de administrador do dispositivo. Quando um utilizador seleciona a notificação, lançará o Portal da Empresa Android para a página de **definições** do dispositivo Update onde pode iniciar o fluxo para passar para a gestão de perfis de trabalho.
    - **Envie e-mail para o utilizador final**: Configure isto para enviar e-mails aos utilizadores sobre a mudança do administrador do dispositivo para a gestão do perfil de trabalho. No e-mail, pode incluir o URL abaixo , que quando selecionado, lançará o Portal da Empresa Android para a página de definições do dispositivo Update onde podem iniciar o fluxo para passar para a gestão de perfis de trabalho.
      - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
      - Para o governo dos EUA, pode utilizar este link: `https://portal.manage.microsoft.us/UpdateSettings.aspx` .
  
    > [!NOTE]
    > - Claro que pode utilizar hipertexto simesmo para os links na sua comunicação com os utilizadores. No entanto, não utilize os encurtadores de URL porque as ligações podem não funcionar se alteradas dessa forma.
    > - Se o Portal da Empresa Android estiver aberto e em segundo plano, quando um utilizador toca no link, pode ir para a última página que tinha aberto.
    > - Os utilizadores devem tocar no link num dispositivo Android. Se, em vez disso, o colarem num navegador, não lançará o Portal da Empresa Android. 

    Escolha **Seguinte**.

7. Na página de **tags Scope,** selecione quaisquer etiquetas de âmbito que pretenda incluir.
8. Na página **de Atribuição,** atribua a política a um grupo que tenha dispositivos matriculados com a gestão do administrador do dispositivo > **Next**.
9. Na página **Review + criar,** confirmar todas as definições e, em seguida, selecionar **Criar**.

## <a name="troubleshooting"></a>Resolução de problemas

O fluxo final do utilizador para passar para novos guias de gestão de [dispositivos](../user-help/move-to-new-device-management-setup.md) guia os utilizadores através da desinscrição da gestão do administrador do dispositivo e da configuração com a gestão do perfil de trabalho. Os utilizadores devem ter [dispositivos inscritos](android-enroll-device-administrator.md) para administrador de dispositivos Android com a versão 5.0.4720.0 do Portal da Empresa Android.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Utilizador vê um erro depois de tocar no Resolve
Se os utilizadores virem um erro depois de tocarem no botão **Resolver,** é provável que seja por causa de uma destas razões:
- A inscrição no perfil de trabalho não está corretamente configurada (ou uma conta Android Enterprise não está ligada ou as restrições de inscrição estão definidas para bloquear a inscrição no perfil de trabalho).
- O dispositivo está a executar o Android 4.4 ou mais cedo, o que não suporta a inscrição no perfil de trabalho. 
- O fabricante do dispositivo não suporta a inscrição do perfil de trabalho no modelo do dispositivo.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>O botão de resolução não aparece no dispositivo do utilizador
O botão **Resolve** não aparecerá no dispositivo do utilizador se o utilizador se inscrever na gestão do administrador do dispositivo depois de ter sido direcionado com a política de conformidade do dispositivo explicada acima.

Para que o botão **Resolve** apareça, o utilizador deve adiar a configuração e reiniciar o processo a partir da notificação.

Para evitar esta condição, utilize restrições de inscrição para bloquear a inscrição na gestão do administrador do dispositivo.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>O utilizador vê um erro depois de tocar no URL para atualizar a página de definições do dispositivo
Os utilizadores podem ver uma página de erro no navegador quando tocarem no URL na página de **definições** do dispositivo Update do Portal da Empresa Android. Este erro pode ser causado por um dos seguintes:
- O dispositivo não é um Android.
- O dispositivo Android não tem a aplicação Portal da Empresa.
- A versão Portal da Empresa Android é superior a 5.0.4720.0.
- O dispositivo Android utiliza o Android 6 ou mais cedo. 

## <a name="next-steps"></a>Passos seguintes
[Ver o fluxo](../user-help/move-to-new-device-management-setup.md) 
 de utilizador final [Gerir dispositivos](android-enterprise-overview.md) de perfil de trabalho Android com Intune
