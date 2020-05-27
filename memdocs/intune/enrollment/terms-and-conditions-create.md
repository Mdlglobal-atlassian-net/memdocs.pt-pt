---
title: Definir termos e condições no Microsoft Intune
titleSuffix: ''
description: Defina os termos e condições que os utilizadores veem no Portal da Empresa do Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/20/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4a3a11a8-9c0c-4334-8c6b-6fea4d0a2efb
ms.reviewer: amyro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 66bc3db54ebefe814a14f564abbad42dc226aefe
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988984"
---
# <a name="terms-and-conditions-for-user-access"></a>Termos e condições do acesso dos utilizadores

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Enquanto administrador do Intune, pode exigir que os utilizadores aceitem os termos e condições da sua empresa antes de utilizarem o Portal da Empresa para:
- inscrever dispositivos
- aceder a recursos como aplicações e e-mail da empresa.

A configuração dos termos e condições é opcional.

Pode criar vários conjuntos de termos e atribuí-los a diferentes grupos, tal como para suportar outros idiomas.

Existem duas formas de criar os termos e condições da sua empresa:
- com o Intune, conforme descrito neste artigo.
- utilizando a [funcionalidade de utilização do Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/governance/active-directory-tou)

Para saber qual o melhor método para si, confira a [solução de Termos certos para a sua publicação](https://go.microsoft.com/fwlink/?linkid=2010506&clcid=0x409)de blog da organização. 

## <a name="create-terms-and-conditions"></a>Criar termos e condições
Conclua estes passos para criar os termos e condições. O nome a apresentar e a descrição são para utilização administrativa enquanto as propriedades dos termos são apresentadas aos utilizadores no Portal da Empresa.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha termos e condições da **administração do Arrendatário**  >  **Terms and Conditions**.
2. Escolha **Criar**.
3. Na página **Basics,** especifique as seguintes informações:

   - **Nome**: O nome dos termos no portal Azure. Os utilizadores não veem este nome.
   - **Descrição**: detalhes opcionais que ajudam a identificar este conjunto de termos no Portal do Azure.

    ![Screenshot do portal Azure mostrando a página Basics para termos e condições](./media/terms-and-conditions-create/terms-basics-page.png)

4. Escolha **A Seguir** para ir à página **Termos** e fornecer as seguintes informações:

   - **Título**: o nome dos termos que os utilizadores veem no Portal da Empresa acima do **Resumo**.
   - **Termos e Condições**: os termos e condições que os utilizadores veem e devem aceitar ou rejeitar.
   - **Resumo dos Termos**: texto que explica o que significa quando os utilizadores aceitam os termos. Por exemplo, "Ao inscrever o dispositivo, aceita os termos de utilização definidos pela Contoso. Leia atentamente os termos antes de continuar”.

5. Escolha **O Próximo** para ir à página de **tags Scope.**

6. Escolha etiquetas de **âmbito,** selecione as etiquetas de âmbito que pretende atribuir a estes termos e condições e, em seguida, escolha **Selecionar**. 

7. Escolha **O Próximo** para ir à página de **Atribuições** e escolha uma das seguintes opções para **Atribuir para:**
    - **Todos os utilizadores**: Escolha esta opção para atribuir estes termos e condições a todos os utilizadores.
    - **Selecione grupos**: Escolha esta opção para atribuir estes termos e condições a todos os grupos que identifica, escolhendo **grupos Select para incluir**.

8. Escolha **Next**  >  **Create**.

## <a name="see-how-terms-are-displayed-to-your-users"></a>Ver como os termos são apresentados para os utilizadores
O exemplo a seguir mostra o **Título** e o **Resumo de Termos** na consola de administração e no Portal da Empresa.

![Captura de ecrã do Título e do Resumo dos Termos na consola de administração e no Portal da Empresa.](./media/terms-and-conditions-create/terms-summary-terms.png)

O exemplo a seguir mostra os termos e as condições na consola de administração e no Portal da Empresa.

![Captura de ecrã dos termos e das condições na consola de administração e no Portal da Empresa.](./media/terms-and-conditions-create/terms-properties-terms.png)


## <a name="monitor-terms-and-conditions"></a>Monitorizar os termos e as condições

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha termos e condições da **administração do Arrendatário**  >  **Terms and Conditions**.
2. Na lista de termos e condições, selecione os termos cuja aceitação pretende ver > **Relatórios de Aceitação**.

## <a name="work-with-multiple-versions-of-terms-and-conditions"></a>Trabalhar com múltiplas versões de termos e condições
Pode editar os seus termos e condições e gerir as respetivas versões. Sempre que fizer uma alteração significativa aos seus termos e condições, deve:
- aumentar o número da versão.
- exigir que os utilizadores aceitem os novos termos e condições

Mantenha o número da versão atual se, por exemplo, estiver a corrigir tipografias ou a mudar de formatação.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha termos e condições da **administração do Inquilino**> escolha os termos e  >  **Terms and Conditions** condições que pretende modificar > **Propriedades**.

2. No painel **Propriedades**, selecione **Termos e Condições** e, em seguida, modifique o **Título**, **Resumo dos Termos** e **Termos e Condições**, conforme necessário. Se os utilizadores tiverem de voltar a aceitar os novos termos devido às alterações que fez, selecione **Exigir que os utilizadores voltem a aceitar e incrementem o número da versão para**

3. Escolha **OK**  >  **Guardar**.

Os utilizadores só precisam de aceitar os termos e as condições atualizados uma vez. Os utilizadores com vários dispositivos não precisam de aceitar os termos e condições em cada dispositivo.
