---
title: Publicar dados do site
titleSuffix: Configuration Manager
description: Saiba como publicar sites do Gestor de Configuração para Serviços de Domínio de Diretório Ativo.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718365"
---
# <a name="publish-site-data-for-configuration-manager"></a>Publicar dados do site para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de estender o esquema de Diretório Ativo para Gestor de Configuração, pode publicar sites do Gestor de Configuração para Serviços de Domínio de Diretório Ativo (AD DS). Isto permite que os computadores Ative Directy recuperem de forma segura informações do site a partir de uma fonte fidedigna. Embora a publicação de informações do site para AD DS não seja necessária para a funcionalidade básica do Gestor de Configuração, pode reduzir as despesas administrativas para o fazer.  

-   **Quando um site está configurado para publicar em AD DS,** os clientes do Gestor de Configuração podem encontrar automaticamente pontos de gestão através da publicação de Ative Directory. Usam uma consulta LDAP para um servidor de catálogo global.  

-   **Quando um site não publica no AD DS**, os clientes precisarão de um mecanismo alternativo para localizar o respetivo ponto de gestão predefinido.  

Para obter informações sobre como os clientes encontram um ponto de gestão, consulte Entenda como os clientes encontram recursos e serviços do site para O Gestor de [Configuração.](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sites para publicar no AD DS  
 Seguem-se os passos de nível superior:  

-   Deve estender o esquema de [Diretório Ativo para Gestor](../../../../core/plan-design/network/extend-the-active-directory-schema.md) de Configuração em cada floresta onde publicará os dados do site. Certifique-se também de que o recipiente de Gestão de **Sistemas** está presente.  

-   Deve conceder a conta de computador de cada site primário que publicará o **controlo total** dos dados para o recipiente de Gestão de **Sistemas** e todos os seus objetos infantis.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para permitir que um site do Gestor de Configuração publique informações do site para a floresta de Diretório Ativo

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho da **Administração,** expanda a **Configuração**do Site e clique em **Sites**. Selecione o site que pretende ter publicados os dados do site. Em seguida, no separador **Casa,** no grupo **Propriedades,** clique em **Propriedades**.  

3.  No separador **Editorial** das propriedades do site, selecione as florestas para as quais este site publicará os dados do site.  

4.  Clique **em OK** para salvar a configuração.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Para criar florestas de Diretório Ativo para publicação  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** expanda a **Configuração da Hierarquia,** clique em **Florestas de Diretório Ativo.** Se a Deteção de Florestas do Active Directory tiver sido executada anteriormente, as florestas detetadas serão apresentadas no painel de resultados. A floresta local e quaisquer florestas fidedignas são detetadas quando a Deteção de Florestas do Active Directory é executada. Apenas é necessário adicionar manualmente as florestas não fidedignas.  

    -   Para criar uma floresta previamente descoberta, selecione a floresta no painel de resultados. Em seguida, no separador **Home,** no grupo **Propriedades,** clique em **Propriedades** para abrir as propriedades da floresta. Continue com o passo 3.  

    -   Para criar uma nova floresta que não esteja listada, no separador **Home,** no grupo **Create,** clique em **Adicionar Floresta** para abrir a caixa de diálogo **Add Forests.** Continue com o passo 3.  

3.  No separador **Geral,** configurações completas para a floresta que pretende descobrir, e especificar a Conta Florestal do **Diretório Ativo**.  

    > [!NOTE]  
    >  A Deteção de Florestas do Active Directory requer uma conta global para detetar e publicar em florestas não fidedignas. Se não utilizar a conta de computador do servidor do site, só pode selecionar uma conta global.  

4.  Se pretende permitir que os sites publiquem dados do site nesta floresta, conclua as configurações para publicação nesta floresta no separador **Publicação** .  

    > [!NOTE]  
    >  Se permitir que os sites publiquem para uma floresta, deve estender o esquema de Diretório Ativo dessa floresta para Gestor de Configuração. A Conta Florestal do Diretório Ativo deve ter permissões de controlo total para o contentor do Sistema naquela floresta.  

5.  Quando concluir a configuração desta floresta para ser utilizada com a Deteção de Florestas do Active Directory, clique em **OK** para guardar a configuração.  
