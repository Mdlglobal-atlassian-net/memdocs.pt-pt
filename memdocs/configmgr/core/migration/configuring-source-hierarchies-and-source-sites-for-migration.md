---
title: Hierarquias de fontes de migração
titleSuffix: Configuration Manager
description: Configure uma hierarquia de origem e sites de origem para que possa migrar dados para o ambiente atual do seu Gestor de Configuração.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718925"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Configure hierarquias de origem e locais de origem para migração para o ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para permitir a migração de dados para o ambiente atual do seu Gestor de Configuração, deve configurar uma hierarquia de fonte de fonte de Gestor de Configuração suportada e um ou mais sites de origem nessa hierarquia que contenham dados que pretende migrar.  

> [!NOTE]  
>  As operações de migração são executadas no local de alto nível da hierarquia de destino. Se configurar a migração quando utilizar uma consola de Configuração Manager que esteja ligada a um site primário para crianças, deve dar tempo para que a configuração se reproduza para o site da administração central, inicie e, em seguida, reproduza o estado de volta ao local principal ao qual está ligado.  

 Utilize as informações e procedimentos nas seguintes secções para especificar a hierarquia de origem e adicionar locais de origem adicionais. Depois de terminar estes procedimentos, pode criar empregos de migração e começar a migrar dados da hierarquia de origem para a hierarquia de destino.  

-   [Especificar uma hierarquia de origem para a migração](#BKBM_ConfigSrcHierarchy)  

-   [Identificar locais de origem adicionais da hierarquia de origem](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a>Especificar uma hierarquia de origem para a migração  
 Para migrar dados para a sua hierarquia de destino, deve especificar uma hierarquia de origem suportada que tenha os dados que pretende migrar. Por padrão, o local de alto nível dessa hierarquia torna-se um local de origem da hierarquia de origem. Se migrar de uma hierarquia do Gestor de Configuração de 2007, poderá então criar locais de origem adicionais para migração após a recolha de dados a partir do site de origem inicial. Se migrar de um Gestor de Configuração do System Center 2012 ou da hierarquia atual do gestor de configuração, não precisa de configurar sites de origem adicionais para migrar dados da hierarquia de origem. Isto porque estas versões do Gestor de Configuração utilizam uma base de dados partilhada que está disponível no site de alto nível da hierarquia de origem. A base de dados partilhada tem toda a informação que pode migrar.  

 Utilize os seguintes procedimentos para especificar uma hierarquia de origem para migração e para identificar locais de origem adicionais numa hierarquia do Gestor de Configuração de 2007.  

 Executar este procedimento com uma consola de Gestor de Configuração que esteja ligada à hierarquia de destino:  

### <a name="to-configure-a-source-hierarchy"></a>Para configurar uma hierarquia de origem   

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3. No separador **Home,** no grupo **Migração,** clique em **Especificar hierarquia de origem**.  

4. Na caixa de diálogo **especificada da hierarquia de origem,** para a **Hierarquia fonte,** selecione **Nova hierarquia de origem**.  

5. Para o servidor do **site do Gestor de Configuração de nível Superior,** introduza o nome ou endereço IP do site de alto nível de uma hierarquia de origem suportada.  

6. Especifique as contas de acesso ao site de origem que tenham as seguintes permissões:  

   - Conta de Sítio fonte: **Leia** a permissão ao Fornecedor SMS para o site de alto nível especificado na hierarquia de origem. A partilha e atualizações de pontos de distribuição requerem **permissões modificadas** e **apagadas** para o site na hierarquia de origem.

   - Conta de base de dados do site fonte: **Leia** e **execute** a permissão para a base de dados do Servidor SQL para o site de alto nível especificado na hierarquia de origem.  

     Se especificar a utilização da conta de computador, o Gestor de Configuração utiliza a conta de computador do site de alto nível da hierarquia de destino. Para esta opção, certifique-se de que esta conta é membro do grupo de segurança **Distribuídos Utilizadores com o domínio** onde reside o site de alto nível da hierarquia de origem.  

7. Para partilhar pontos de distribuição entre as hierarquias de origem e destino, selecione a partilha do ponto de distribuição Enable para a caixa de verificação **do servidor do site de origem.** Se não permitir a partilha de pontos de distribuição neste momento, pode fazê-lo editando as credenciais do site de origem após a recolha de dados.  

8. Clique **em OK** para salvar a configuração. Isto abre a caixa de diálogo do **Estado de Recolha** de Dados e a recolha de dados começa automaticamente.  

9. Quando a recolha de dados terminar, clique em **Fechar** a caixa de diálogo do **Estado de Recolha** de Dados e completar a configuração.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a>Identificar locais de origem adicionais da hierarquia de origem  
 Quando configura uma hierarquia de origem suportada, o site de alto nível dessa hierarquia é automaticamente configurado como um site de origem, e os dados são automaticamente recolhidos a partir desse site. A próxima ação que tomar depende da versão do Gestor de Configuração que é gerida pela hierarquia de origem:  

-   Para uma hierarquia de origem do Gestor de Configuração de 2007, pode iniciar a migração a partir desse site de origem inicial ou configurar sites de origem adicionais a partir da hierarquia de origem após a recolha de dados para o local de origem inicial. Para migrar dados que só estão disponíveis a partir de um site infantil, criar sites de origem adicionais para uma hierarquia do Gestor de Configuração de 2007. Por exemplo, pode configurar sites de origem adicionais para recolher dados sobre conteúdos que pretende migrar quando é criado num site infantil na hierarquia de origem e não está disponível no site superior da hierarquia de origem.  

-   Para um System Center 2012 Configuration Manager ou Configuração Manager hierarquia de fonte de filial, você não precisa configurar sites de origem adicionais. Isto porque estas versões do Gestor de Configuração utilizam uma base de dados partilhada que está disponível no site de alto nível da hierarquia de origem. A base de dados partilhada tem toda a informação que pode migrar de todos os sites da hierarquia de origem. Isto disponibiliza os dados que pode migrar do local de alto nível da hierarquia de origem.  

Quando configurar sites de origem adicionais para uma hierarquia de origem do Gestor de Configuração de 2007, deve configurar os sites de origem adicionais desde o topo da hierarquia de origem até ao fundo. Deve configurar um site-mãe como um site de origem antes de configurar qualquer um dos seus sites infantis como sites de origem.  

Utilize o seguinte procedimento para configurar locais de origem adicionais para as hierarquias de origem do Gestor de Configuração de 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar locais de origem adicionais na hierarquia de origem 

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Escolha o site que pretende configurar como um site de origem.  

4.  No separador **Home Page** , no grupo **Site de Origem** , clique em **Configurar**.  

5.  Na caixa de diálogo **Source Site Credenciais,** para as contas de acesso ao site de origem, especifique contas que tenham as seguintes permissões:  

    -   Conta de Sítio fonte: **Leia** a permissão ao Fornecedor SMS para o site de alto nível especificado na hierarquia de origem. A partilha e atualizações de pontos de distribuição requerem **permissões modificadas** e **apagadas** para o site na hierarquia de origem.  

    -   Conta de base de dados do site fonte: **Leia** e **execute** a permissão para a base de dados do Servidor SQL para o site de alto nível especificado na hierarquia de origem.  

    Se especificar a utilização da conta de computador, o Gestor de Configuração utiliza a conta de computador do site de alto nível da hierarquia de destino. Para esta opção, certifique-se de que esta conta é membro do grupo de segurança **Distribuídos Utilizadores com o domínio** onde reside o site de alto nível da hierarquia de origem.  

6.  Para partilhar pontos de distribuição entre as hierarquias de origem e destino, selecione a partilha do ponto de distribuição Enable para a caixa de verificação **do servidor do site de origem.** Se não permitir a partilha de pontos de distribuição neste momento, pode fazê-lo editando as credenciais para o site de origem após a recolha de dados.  

7. Clique **em OK** para salvar a configuração. Isto abre a caixa de diálogo do **Estado de Recolha** de Dados e a recolha de dados começa automaticamente.  

8.  Quando a recolha de dados terminar, clique **em Fechar** para completar a configuração.  
