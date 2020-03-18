---
title: Emigrar acesso condicional ao portal Azure
titleSuffix: Microsoft Intune
description: Reatribua as políticas de Acesso Condicional que criou anteriormente no portal clássico Intune para o portal Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/02/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 301159ad-5f7e-4fcc-86c7-f72a71701ff4
ms.reviewer: chrisgree
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e28ca9e9b8ed77cdd01b415761fd90308d5b7017
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329529"
---
# <a name="reassign-conditional-access-policies-from-intune-classic-portal-to-the-azure-portal"></a>Reatribuir políticas de acesso condicional do portal clássico Intune para o portal Azure

A partir do novo portal Azure, o Acesso Condicional oferece suporte para múltiplas políticas por aplicação, juntamente com mais personalizabilidade. Se já criou políticas de Acesso Condicional no portal clássico Intune, pode migrar para o portal Azure. 

## <a name="before-you-begin"></a>Antes de começar

Se estiver pronto para se mudar para o portal Azure, siga os passos deste tópico para reatribuir as políticas de Acesso Condicional que criou anteriormente no portal clássico Intune:

- Reúna as políticas de Acesso Condicional anteriormente criadas, para que saiba quais as definições que precisa de reatribuir mais tarde.

- Siga os passos neste tópico para recriar estas políticas no portal do Azure.

- Desative as políticas condicionais no portal clássico do Intune após ter verificado que as novas políticas funcionam conforme esperado no portal do Azure.
<br /><br />
  - **Antes de desativar** as políticas de Acesso Condicional no portal clássico Intune, planeje como irá mover os utilizadores para a nova política. Existem duas abordagens:
<br /><br />
    - **Utilize o mesmo grupo de inclusão para aplicar políticas criadas no portal do Azure e crie um novo grupo de isenção para utilizar com as políticas aplicadas pelo portal clássico do Intune**.
      - Migre gradualmente alguns utilizadores para o grupo de isenção especificado no portal clássico. Esta ação impede que as políticas direcionadas pelo portal clássico do Intune sejam aplicadas. As políticas criadas e direcionadas para o mesmo grupo de utilizadores no portal do Azure são aplicadas para além das aplicadas no portal clássico do Intune. 
<br /><br />
    - Criar um novo grupo para direcionar as políticas de **Acesso Condicional no portal Azure.** Se escolher esta abordagem, tem de fazer o seguinte:
      - Remova gradualmente os utilizadores dos grupos de segurança que têm políticas de Acesso Condicional direcionadas para eles no portal clássico Intune.
      - Após confirmar que a nova política está a funcionar para estes utilizadores, pode desativar a política no portal clássico do Intune. 
<br /><br />
- Se tiver as definições da política de Acesso Condicional configuradas para utilizar o Exchange ActiveSync (EAS) no portal clássico Intune, consulte as [instruções deste tópico](#reassign-intune-device-based-conditional-access-policies-for-eas-clients) para reatribuir as definições da política de acesso condicional da **EAS no portal Azure**.

### <a name="to-verify-your-device-based-conditional-access-policies-in-the-intune-classic-portal"></a>Para verificar as suas políticas de acesso condicional baseadas no dispositivo no portal clássico Intune

1. Aceda ao [portal clássico do Intune](https://manage.microsoft.com) e inicie sessão com as suas credenciais.

2. Selecione **Política** no menu à esquerda.

3. Escolha **o Acesso Condicional**e, em seguida, selecione o serviço de nuvem microsoft (por exemplo, Exchange Online ou SharePoint Online) para o qual criou uma política de Acesso Condicional.

4. Tome nota das definições de Acesso Condicional e consulte-as quando criar as mesmas políticas de Acesso Condicional no portal Azure.

### <a name="app-and-device-based-conditional-access-policies-working-together"></a>Políticas de acesso condicional baseadas em aplicativos e dispositivos que trabalham em conjunto

O painel **Proteção de Aplicações do Intune** no portal do Azure permite que os administradores definam regras condicionais com base na aplicação para que apenas as aplicações que suportam as políticas de proteção de aplicações do Intune tenham permissão para aceder aos recursos empresariais. Pode optar por sobrepor-se a estas políticas de Acesso Condicional baseadas em aplicações utilizando políticas de acesso condicional baseadas em dispositivos. Pode combinar as políticas condicionais com base na aplicação e no dispositivo (E lógico) ou pode fornecer qualquer uma das opções (OU lógico). Se os seus requisitos de política de acesso condicional forem para:

- Exigir um dispositivo em conformidade **E** utilizar a aplicação aprovada.
  - Deverá definir a sua política de acesso condicional utilizando a lâmina de acesso condicional do [Diretório Ativo Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) e a [lâmina de proteção de aplicações Intune](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0).
<br /><br />
- Exigir um dispositivo em conformidade **OU** utilizar a aplicação aprovada.
  - Deve definir a sua política de Acesso Condicional utilizando o [portal clássico Intune](https://manage.microsoft.com) e a [lâmina de proteção de aplicações Intune](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0).

> [!TIP] 
> Este tópico fornece capturas de ecrã que comparam a experiência do utilizador no portal clássico do Intune e no portal do Azure.

## <a name="reassign-intune-device-based-conditional-access-policies"></a>Reatribuir políticas de acesso condicional baseadas em dispositivos

1. Aceda ao [Acesso Condicional no portal Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)e inscreva-se com as suas credenciais.

2. Selecione **Nova política**.

3. Forneça um nome para a política.

4. No âmbito da **secção de Atribuiçãos,** escolha **Utilizadores e grupos** para direcionar a nova política de Acesso Condicional.

    ![Imagem que compara o grupo de utilizadores UI entre os portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-1.png)

    > [!IMPORTANT] 
    > A seleção que fizer no portal do Azure deve corresponder à seleção feita no portal clássico. Por exemplo, se tiver selecionado todos os utilizadores no portal clássico do Intune, selecione **Todos os utilizadores** no portal do Azure. Além disso, se tiver selecionado a opção **Grupos isentos** no portal clássico do Intune, tem de excluir esses grupos selecionados no portal do Azure.

5. Após escolher o seu grupo, clique em **Selecionar** e, em seguida, clique em **Concluído**.

6. Na secção **Atribuições**, selecione **Aplicações na cloud**.

7. No painel **Aplicações na cloud**, selecione **Selecionar aplicações**.

8. Escolha a aplicação a que pretende aplicar a nova política de Acesso Condicional e clique em **Select**.

9. Clique em **Concluir**.

    ![Imagem de uma comparação de UI da aplicação em nuvem entre os portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-3.png)

    > [!TIP] 
    > Se tiver múltiplas aplicações com a mesma política, pondere consolidá-las numa única política no portal do Azure.

10. Na secção **Atribuições**, selecione **Condições**.

11. No painel **Condições**, selecione **Plataformas de dispositivos** e, em seguida, selecione as plataformas de dispositivos aplicáveis.

12. Quando terminar de selecionar as plataformas de dispositivos, clique em **Concluído** duas vezes.

    ![Imagem que compara a plataforma de dispositivos UI dos portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-4.png)

    > [!TIP] 
    > Se tiver selecionado plataformas individuais no portal clássico do Intune, selecione as plataformas individuais no portal do Azure.

    > [!NOTE] 
    > Pode especificar as opções de conformidade ou associação a um domínio para o Windows mais tarde.

13. Na secção **Atribuições**, selecione **Condições**.

14. No painel **Condições**, selecione **Aplicações cliente** e, em seguida, selecione a aplicação cliente aplicável.

15. Após selecionar a aplicação cliente, clique em **Concluído** duas vezes.

    ![Imagem que compara aplicações de clientes UI entre os portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-6.png)

16. Se tiver escolhido as definições do browser no portal clássico do Intune, selecione **Browser** e **Aplicações móveis e clientes de ambiente de trabalho** no portal do Azure. No caso de não ter escolhido as definições do browser no portal clássico do Intune, selecione apenas **Aplicações móveis e clientes de ambiente de trabalho**. 

17. Na secção **Controlos de acesso**, selecione **Conceder**.

18. Em **Conceder Controlos de Acesso**, selecione **Pedir que o dispositivo seja marcado como compatível** e, em seguida, clique em **Selecionar**.

19. Se tiver uma política para exigir dispositivos Windows associados a um domínio e também permitir dispositivos Windows em conformidade e inscritos no Intune, selecione **Requerer dispositivo associado ao domínio** e **Pedir que o dispositivo seja marcado como compatível**, juntamente com **Exigir um dos controlos selecionados**.

20. Se não permitir dispositivos Windows em conformidade e inscritos no Intune, exclua a política do Windows da política atual. Em seguida, crie uma política separada com a opção **Plataformas de dispositivos** definida para **Windows**, inclua outras condições conforme definido acima e selecione **Requerer dispositivo associado ao domínio** em **Conceder Controlos de Acesso**.

21. Na **lâmina** da nova política de acesso condicional, ligue a **toggle** da política Enable e, em seguida, clique em **Criar**.

    ![Compare a política de acesso condicional Entre Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-11.png)

## <a name="reassign-intune-device-based-conditional-access-policies-for-eas-clients"></a>Reatribuir políticas de acesso condicional baseadas em dispositivos intune para clientes DaEAs

Se configurar as definições do Exchange ActiveSync como parte de uma política Exchange Online no portal clássico Intune, precisa de criar uma segunda política de Acesso Condicional no portal Azure.

1. Aceda ao [Acesso Condicional no portal Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)e inscreva-se com as suas credenciais.

2. Selecione **Nova política**.

3. Forneça um nome para a política.

4. No âmbito da secção **de Atribuiçãos,** escolha **Utilizadores e grupos** para direcionar a nova política de Acesso Condicional.

    ![Imagem mostrando uma comparação de UI do grupo de utilizadores entre os portais Azure e Intune](./media/conditional-access-intune-reassign/reassign-ca-12.png)

    > [!IMPORTANT] 
    > A seleção que fizer no portal do Azure deve corresponder à seleção feita no portal do Intune. Por exemplo, se tiver selecionado todos os utilizadores no portal clássico do Intune, selecione **Todos os utilizadores** no portal do Azure. Além disso, se tiver selecionado a opção **Grupos isentos** no portal clássico do Intune, tem de excluir esses grupos selecionados no portal do Azure.

5. Após escolher o seu grupo, clique em **Selecionar** e, em seguida, clique em **Concluído**.

6. Na secção **Atribuições**, selecione **Aplicações na cloud**.

7. No painel **Aplicações na cloud**, clique em **Selecionar aplicações** e selecione **Exchange Online**. Em seguida, clique em **Selecionar** e **Concluído**.

    ![Imagem de uma nuvem apps UI comparação entre os portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-14.png)

    > [!IMPORTANT] 
    > As políticas de acesso condicional para clientes EAS não podem incluir outras aplicações na cloud.

8. No painel **Condições**, selecione **Aplicações cliente** e, em seguida, selecione a aplicação cliente aplicável. Se tiver optado por bloquear clientes que não sejam suportados pelo Intune, utilize a opção **Aplicar política apenas a plataformas suportadas**.

    ![Imagem mostrando uma comparação de aplicativos de cliente UI entre os portais Azure e Intune](./media/conditional-access-intune-reassign/reassign-ca-15.png)

9. Após selecionar a aplicação cliente, clique em **Concluído** duas vezes.

10. Na secção **Controlos de acesso**, selecione **Conceder**.

11. Em **Conceder Controlos de Acesso**, selecione **Pedir que o dispositivo seja marcado como compatível** e, em seguida, clique em **Selecionar**.

    ![Imagem que compara AI de acesso ao Grant entre os portais Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-16.png)

12. Na **lâmina** da nova política de acesso condicional, ligue a **toggle** da política Enable e, em seguida, clique em **Criar**.

    ![Comparação da política de acesso condicional Viabilizado UI entre Intune e Azure](./media/conditional-access-intune-reassign/reassign-ca-17.png)

> [!NOTE]
> Se configurar **Plataformas de dispositivos**, guardar a política irá falhar com o erro "A configuração de política não é suportada". O Exchange ActiveSync não consegue identificar a plataforma a ser utilizada pelo dispositivo de ligação. Por conseguinte, a configuração de plataformas de dispositivos específicas não é suportada quando criar uma política para dispositivos do Exchange ActiveSync.

## <a name="disable-conditional-access-policies-in-the-intune-classic-portal"></a>Desativar políticas de acesso condicional no portal clássico Intune

Depois de ter reatribuído as suas políticas de Acesso Condicional no portal Azure, é importante desativar gradualmente as políticas de Acesso Condicional anteriormente criadas no portal clássico Intune. Além disso, poderá ser necessário utilizar o mesmo grupo de segurança para aplicar as políticas de Acesso Condicional criadas no portal Azure.

> [!NOTE]
> Antes de desativar as suas políticas de Acesso Condicional no portal clássico Intune, consulte a secção Antes de [iniciar](#before-you-begin) no início deste tópico.

### <a name="to-disable-the-conditional-access-policies"></a>Para desativar as políticas de acesso condicional

Desde que o MDM foi removido do Portal Clássico Intune, foi fornecido o seguinte link para visualizar/desativar estas políticas clássicas:

[https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies](https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies)

## <a name="see-also"></a>Veja também

- [Formas comuns de usar o Acesso Condicional com Intune](conditional-access-intune-common-ways-use.md)
- [acesso condicional baseado em aplicativos com Intune](app-based-conditional-access-intune.md)
- [Acesso Condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)
