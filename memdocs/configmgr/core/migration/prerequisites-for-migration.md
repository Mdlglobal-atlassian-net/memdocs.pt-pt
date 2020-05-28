---
title: Pré-requisitos de migração
titleSuffix: Configuration Manager
description: Compreenda as versões suportadas do Gestor de Configuração, idiomas de site de origem suportados e configurações necessárias para a migração.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e62ea5198824a6b3466853cdbcfc3057d1829e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428730"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Pré-requisitos para a migração em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para migrar de uma hierarquia de origem suportada, deve ter acesso a cada site de origem do Gestor de Configuração aplicável, e permissões dentro do site de destino do Gestor de Configuração para configurar e executar operações de migração.  

 Utilize as informações nas seguintes secções para ajudá-lo a compreender as versões do Gestor de Configuração que são suportadas para a migração e as configurações necessárias.  

-   [Versões do Configuration Manager que são suportadas para migração](#BKMK_SupportedMigrationVersions)  

-   [Línguas do site de origem que são apoiadas para a migração](#BKMK_SorceSiteLanguage)  

-   [Configurações necessárias para a migração](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a>Versões do Gestor de Configuração que são suportadas para a migração  
 Pode migrar dados de uma hierarquia de origem que executa qualquer uma das seguintes versões do Gestor de Configuração:  

- Configuração Gestor 2007 SP2 (Para efeitos de migração, O Gestor de Configuração 2007 R2 ou R3 no site de origem não são uma consideração. Enquanto o site de origem for executado SP2, os sites com o add-on R2 ou R3 instalados são suportados para migração para o ramo atual do Gestor de Configuração).  

- System Center 2012 Diretor de Configuração SP2 ou System Center 2012 R2 Diretor de Configuração SP1.  

  > [!TIP]  
  >  Além da migração, pode utilizar um upgrade em local de sites que executam o System Center 2012 Configuration Manager para configuração manager atual.  

- Uma hierarquia do Gestor de Configuração da mesma versão ou menor do Gestor de Configuração.  

  Por exemplo, se tiver uma hierarquia de destino que gere o atual ramo 1606 do Gestor de Configuração, pode utilizar a migração para copiar dados de uma hierarquia de origem que executa a versão 1606 ou 1602. No entanto, não foi possível migrar dados de uma hierarquia de origem que funciona em 1610.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> Idiomas do site de origem que são suportados para migração  
 Quando migra dados entre hierarquias do Gestor de Configuração, os dados são armazenados na hierarquia de destino no formato neutro linguístico para O Gestor de Configuração. Uma vez que o Gestor de Configuração 2007 não armazena dados num formato neutro em termos linguísticos, o processo de migração deve converter objetos para este formato durante a migração do Gestor de Configuração de 2007. Portanto, apenas os sites de origem do Gestor de Configuração 2007 que são instalados com as seguintes línguas são suportados para migração:  

-   Inglês  

-   Francês  

-   Alemão  

-   Japonês  

-   Coreano  

-   Russo  

-   Chinês Simplificado  

-   Chinês Tradicional  

Quando migra dados de um System Center 2012 Configuration Manager ou configuração da hierarquia atual do ramo, não existem limitações de linguagem do site de origem. Os objetos da base de dados do site de origem já estão num formato independente de idiomas.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a>Configurações necessárias para a migração  
São necessárias configurações para a utilização de operações de migração e migração:  

- **Para configurar, executar e monitorizar a migração na consola do Gestor de Configuração:**  

   No site de destino, deve ser atribuída à sua conta a função de segurança de administração baseada em funções do **Administrador de Infraestrutura**. Esta função de segurança concede permissões para gestão de todas as operações de migração, incluindo a criação de tarefas de migração, limpeza e monitorização e a ação de partilhar e atualizar pontos de distribuição.  

- **Recolha de dados:**  

   Para ativar o site de destino para a recolha de dados, é necessário configurar as duas contas de acesso ao site de origem indicadas a seguir para utilização com cada site de origem:  

  -   **Conta do Site de Origem:** esta conta é utilizada para aceder ao Fornecedor de SMS do site de origem.  

      -   Para um site de origem SP2 de Configuração 2007, esta conta requer **a permissão de Leitura** para todos os objetos do site de origem.  

      -   Para um Site de fonte de fonte de gestão de configuração do System Center 2012, esta conta requer **a permissão de Leitura** para todos os objetos do site de origem, concede esta permissão à conta utilizando a administração baseada em papéis. Para obter informações sobre como usar a administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Conta de Base de Dados do Site de Origem:** esta conta é utilizada para aceder à base de dados do SQL Server do site de origem e precisa das permissões de **Ligar**, **Executar**e **Selecionar** para a base de dados do site de origem.  

  Pode configurar estas contas durante a configuração de uma nova hierarquia de origem, a recolha de dados de um site de origem adicional ou a reconfiguração das credenciais de um site de origem. Estas contas podem utilizar uma conta de utilizador de domínio ou o utilizador pode especificar a conta de computador do site de nível superior da hierarquia de destino.  

  > [!IMPORTANT]  
  >  Se utilizar a conta de computador do Gestor de Configuração para uma das contas de acesso, certifique-se de que esta conta é membro do grupo de segurança **Utilizadores com com** no domínio onde reside o site de origem.  

  Durante a recolha de dados, são utilizados os protocolos de rede e as portas seguintes:  

  - NetBIOS/SMB - 445 (TCP)  

  - RPC (WMI) - 135 (TCP & UDP)  

  - RPC dinâmico. As portas dinâmicas utilizam uma gama de números de porta que são definidos pela versão S. Estes portos também são conhecidos como portos efémeros. Para mais informações sobre os intervalos de portas predefinidos, consulte [Descrição geral do serviço e requisitos de portas de rede para o Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).<!-- SCCMDocs#1053 -->

  - SQL Server - As portas TCP utilizadas pelas bases de dados dos sites de origem e de destino.  

- **Migrar Atualizações de Software:**  

   Para poder migrar as atualizações de software, é necessário configurar a hierarquia de destino com um ponto de atualização de software. Para obter mais informações, veja [Planear a migração de atualizações de software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Partilhar pontos de distribuição:**  

   Para partilhar pontos de distribuição com sucesso a partir de um site de origem, pelo menos um site primário ou o site de administração central da hierarquia de destino deve utilizar os mesmos números da porta que os do site de origem para os pedidos do cliente. Para obter informações sobre as portas de pedido do cliente, consulte [Como configurar as portas](../../core/clients/deploy/configure-client-communication-ports.md) de comunicação do cliente  

   Em cada site de origem, são partilhados apenas os pontos de distribuição que estão instalados em servidores do sistema de sites configurados com um FQDN.  

   Além disso, para partilhar um ponto de distribuição de um System Center 2012 Configuração Manager ou site de fonte de sucursal do Gestor de Configuração, a **Conta Fonte site** (que acede ao Fornecedor SMS para o servidor do site fonte), deve ter permissões **modificadas** para o objeto **do Site** no site de origem. Esta permissão é concedida à conta utilizando a administração baseada em funções. Para obter informações sobre como usar a administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Atualizar ou reatribuir pontos de distribuição:**  

   A **Conta de Acesso ao Site de Origem** configurada para recolher dados a partir de um Fornecedor de SMS do site de origem tem de ter as seguintes permissões:  

  - Para atualizar um ponto de distribuição do Gestor de Configuração 2007, a conta requer **leitura,** **execução**e **excluir** permissões à classe **Site** no servidor de site Do Gestor de Configuração2007 para remover com sucesso o ponto de distribuição do site de origem do Gestor de Configuração2007  

  - Para reatribuir um Gestor de Configuração do System Center 2012 ou ponto de distribuição atual do ramo do Gestor de Configuração, a conta deve ter **permissão modificada** para o objeto **do Site** no site de origem. Esta permissão é concedida à conta utilizando a administração baseada em funções. Para obter informações sobre como usar a administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  

    Para atualizar ou reatribuir com sucesso um ponto de distribuição a uma nova hierarquia, as portas configuradas para pedidos de cliente no site que efetua a gestão do ponto de distribuição na hierarquia de origem devem ser iguais às portas configuradas para pedidos de cliente no site de destino que efetuará a gestão do ponto de distribuição. Para obter informações sobre as portas de pedido do cliente, consulte [Como configurar as portas](../../core/clients/deploy/configure-client-communication-ports.md)de comunicação do cliente .  
