---
title: Versões SQL Server suportadas
titleSuffix: Configuration Manager
description: Obtenha a versão sQL Server e os requisitos de configuração para hospedar uma base de dados do site do Gestor de Configuração.
ms.date: 04/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24c3a72eacea6446fb82785a25b0318d8cad0471
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711596"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Versões de Servidor SQL suportadas para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Cada site do Gestor de Configuração requer uma versão e configuração suportadas do SQL Server para alojar a base de dados do site.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Instâncias e localizações do SQL Server

### <a name="central-administration-site-and-primary-sites"></a>Site da administração central e locais primários

A base de dados do site deve utilizar uma instalação completa do Servidor SQL.  

O Servidor SQL pode ser localizado em:  

- O computador do servidor do site.  
- Um computador que está afastado do servidor do site.  

São suportadas as seguintes instâncias:  

- A instância padrão ou nomeada do Servidor SQL.  
- Configurações de várias instâncias.  
- Um cluster de servidor SQL. Consulte [Utilize um cluster do Servidor SQL para alojar a base de dados do site](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- Um grupo de disponibilidade sQL Server AlwaysOn. Para mais informações, consulte [o SQL Server AlwaysOn para obter uma base de dados de site altamente disponível](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>Sítios secundários

A base de dados do site pode utilizar a instância padrão de uma instalação completa do SQL Server ou do SQL Server Express.  

O Servidor SQL deve estar localizado no computador do servidor do site.  

### <a name="limitations-to-support"></a>Limitações ao apoio

As seguintes configurações não são suportadas:

- Um cluster de servidor SQL numa configuração de cluster de equilíbrio de carga de rede (NLB)
- Um cluster de servidor SQL em um volume partilhado cluster (CSV)
- Base de dados SQL Server espelhando tecnologia e replicação peer-to-peer

A replicação transacional do SQL Server é suportada apenas para replicar objetos em pontos de gestão configurados para utilizar [réplicas](../../servers/deploy/configure/database-replicas-for-management-points.md)de bases de dados .  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a>Versões suportadas do Servidor SQL

Numa hierarquia com vários sites, diferentes sites podem usar diferentes versões do SQL Server para alojar a base de dados do site. Desde que os seguintes itens sejam verdadeiros:

- O Gestor de Configuração suporta as versões do SQL Server que utiliza.
- As versões SQL Server que utiliza permanecem no suporte pela Microsoft.
- O SQL Server suporta a replicação entre as duas versões do Servidor SQL. Para mais informações, consulte a [replicação do SQL Server para trás](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility).

Para o SQL Server 2016 e anterior, o suporte para cada versão E pacote de serviçoS SQL segue a Política de [Lifecycle da Microsoft](https://aka.ms/sqllifecycle). O suporte para um pacote de serviço sQL Server específico inclui atualizações cumulativas, a menos que quebrem a compatibilidade para trás com a versão do pacote de serviço base. A partir do SQL Server 2017, os pacotes de serviços não serão lançados uma vez que segue um [modelo de manutenção moderno.](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/) A equipa do SQL Server recomenda a instalação contínua e [proactiva de atualizações cumulativas](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/) à medida que se tornam disponibilizadas.

Salvo especificação em contrário, as seguintes versões do SQL Server são suportadas com todas as versões ativas do Gestor de Configuração. Se for adicionado suporte para uma nova versão do SQL Server, a versão 'Gestor de Configuração' que adiciona esse suporte é notada. Da mesma forma, se o suporte for depreciado, procure detalhes sobre as versões afetadas do Gestor de Configuração.

> [!IMPORTANT]  
> Quando utiliza o SQL Server Standard para a base de dados no site da administração central, limita-se o número total de clientes que uma hierarquia pode suportar. Consulte [Dimensionamento e números da escala](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard, Enterprise

A partir da versão 1910 do Configuration Manager, pode utilizar esta versão com qualquer atualização cumulativa, desde que a sua versão de atualização cumulativa seja suportada pelo ciclo de vida SQL.

Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um site de administração central
- Um local primário
- Um local secundário

#### <a name="known-issue-with-sql-server-2019"></a>Problema conhecido com O Servidor SQL 2019

Há uma questão conhecida.<!--6436234--> com a nova funcionalidade [de inlining scalar UDF](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) no SQL 2019. Para contornar este problema e desativar o forro uDF, execute o seguinte script no servidor SQL 2019:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

Embora nem sempre seja necessário, poderá ter de reiniciar o servidor SQL depois de executar este script. Para mais informações, consulte [Desativar a UDF Scalar Inlining sem alterar o nível](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level)de compatibilidade .

Pode desativar com segurança esta funcionalidade SQL para o servidor de base de dados do site, uma vez que o Gestor de Configuração não a utiliza.

Se não desativar a inserção da UDF em SQL 2019, o servidor do site falhará aleatoriamente em consultar a base de dados do site. Por exemplo, verá os seguintes erros em **hman.log:**

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

Pode ver erros semelhantes noutros registos, tais como **SmsAdminUI.log**.

A versão SQL Server 2019 regista o seguinte erro:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

Também verá despejos de`.mdump` crash (ficheiros) da SQL no seu `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`diretório de registo, que por padrão é .

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise

Pode utilizar esta versão com a versão 2 ou superior da [atualização cumulativa,](https://support.microsoft.com/help/4052574) desde que a sua versão de atualização cumulativa seja suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um site de administração central  
- Um local primário  
- Um local secundário  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
<!--514985-->
Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um site de administração central  
- Um local primário  
- Um local secundário  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard, Enterprise

Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um site de administração central  
- Um local primário  
- Um local secundário

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard, Enterprise

Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um site de administração central  
- Um local primário  
- Um local secundário  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Pode utilizar esta versão com a versão 2 ou superior da [atualização cumulativa,](https://support.microsoft.com/help/4052574) desde que a sua versão de atualização cumulativa seja suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um local secundário
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um local secundário

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um local secundário  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Pode utilizar esta versão com o pacote de serviço mínimo e a atualização cumulativa suportada pelo ciclo de vida SQL. Esta versão do SQL pode ser utilizada para os seguintes sites:

- Um local secundário  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configurações necessárias para o SQL Server

As seguintes configurações são exigidas por todas as instalações do SQL Server que utiliza para uma base de dados do site, incluindo o SQL Server Express. Quando o Gestor de Configuração instala o SQL Server Express como parte de uma instalação secundária do site, cria automaticamente estas configurações.  

### <a name="sql-server-architecture-version"></a>Versão de arquitetura SQL Server

O Gestor de Configuração requer uma versão de 64 bits do SQL Server para alojar a base de dados do site.  

### <a name="database-collation"></a>Colagem de bases de dados

Em cada site, tanto a instância do SQL Server que é utilizada para o site como a base de dados do site devem utilizar a seguinte colagem: **SQL_Latin1_General_CP1_CI_AS**.  

O Gestor de Configuração suporta duas exceções a esta colagem para a norma China GB18030. Para mais informações, consulte [o apoio internacional.](../hierarchy/international-support.md)  

### <a name="database-compatibility-level"></a>Nível de compatibilidade da base de dados

O Gestor de Configuração requer que o nível de compatibilidade para a base de dados do site não seja inferior à versão SQL Server suportada mais baixa para a sua versão De configuração Manager. Por exemplo, a partir da versão 1702, é necessário ter um [nível](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) de compatibilidade na base de dados superior ou igual a 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>Características do Servidor SQL

Só é necessária a funcionalidade **Serviços de Motor da Base de Dados** para cada servidor do site.  

A replicação da base de dados do Gestor de Configuração não requer a funcionalidade de replicação do **Servidor SQL.** No entanto, esta configuração do Servidor SQL é necessária quando utiliza réplicas de [base de dados para pontos](../../servers/deploy/configure/database-replicas-for-management-points.md)de gestão .  

### <a name="windows-authentication"></a>Autenticação do Windows

O Gestor de Configuração requer **a autenticação do Windows** para validar as ligações à base de dados.  

### <a name="sql-server-instance"></a>Instância do Servidor SQL

Utilize uma instância dedicada do Servidor SQL para cada site. A instância pode ser uma **instância nomeada** ou a **instância padrão**.  

### <a name="sql-server-memory"></a>Memória do Servidor SQL

Reserve a memória para o Servidor SQL utilizando o Estúdio de Gestão de Servidores SQL. Defina a definição mínima de memória do **servidor** em funções das **opções**de memória do servidor . Para obter mais informações sobre como configurar esta definição, consulte as opções de configuração do servidor de [memória Do Servidor SQL](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Para um servidor**de base de dados que instala no mesmo computador que o servidor do site : Limite a memória do Servidor SQL a 50 a 80% da memória do sistema endereçada disponível.  

- **Para um servidor**de base de dados dedicado que esteja afastado do servidor do site : Limite a memória do Servidor SQL para 80 a 90 por cento da memória do sistema endereçado disponível.  

- Para uma reserva de **memória para o conjunto tampão de cada instância do Servidor SQL em uso:**  

  - Para um site de administração central: Desempor um mínimo de 8 GB.  
  - Para um local primário: Desloque um mínimo de 8 GB.  
  - Para um local secundário: Desempor um mínimo de 4 GB.  

### <a name="sql-nested-triggers"></a>Gatilhos aninhados SQL

Osacionadores aninhados SQL têm de estar ativados. Para mais informações, consulte Configurar a opção de configuração do [servidor de gatilhos aninhada](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>Integração de CLR do SQL Server

A base de dados de sites necessita do tempo de execução de idioma comum (CLR) do SQL Server para ser ativada. Esta opção é ativada automaticamente quando o Gestor de Configuração instala. Para obter mais informações sobre o CLR, consulte [Introdução à Integração CLR do Servidor SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>Corretor de Serviço sql Server (SSB)

O Corretor de Serviço sQL Server é necessário tanto para a replicação interlocal como para um único local primário.

### <a name="trustworthy-setting"></a>Definição fidedigna

O Gestor de Configuração ativa automaticamente a propriedade de base de dados SQL [TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). Esta propriedade é exigida pelo Gestor de Configuração para estar **ON**.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configurações necessárias para o SQL Server

As seguintes configurações são opcionais para cada base de dados que utiliza uma instalação completa do SQL Server.  

### <a name="sql-server-service"></a>Serviço SQL Server

Pode configurar o serviço do SQL Server para executar utilizando:  

- Uma conta de utilizador de *domínio de baixos direitos:*  

  - Esta configuração é uma boa prática e pode exigir que você registe manualmente o nome principal do serviço (SPN) para a conta.  

- A conta do **sistema local** do computador que executa o Servidor SQL:  

  - Utilize a conta de sistema local para simplificar o processo de configuração.  
  - Quando utiliza a conta do sistema local, o Gestor de Configuração regista automaticamente o SPN para o serviço SQL Server.  
  - Usar a conta do sistema local para o serviço SQL Server não é uma boa prática do SQL Server.  

Quando o computador que executa o SQL Server não utilizar a sua conta de sistema local para executar o serviço SQL Server, configure o SPN da conta que executa o serviço SQL Server em Serviços de Domínio de Diretório Ativo. (Quando a conta do sistema é utilizada, o SPN é automaticamente registado para si.)

Para obter informações sobre SPNs para a base de dados do site, consulte [Gerir o SPN para o servidor](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN)de base de dados do site .  

Para obter informações sobre como alterar a conta que é utilizada pelo serviço SQL Server, consulte [SCM Services - Alterar a conta de arranque de serviço](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Os Serviços de Informação do Servidor SQL são necessários para instalar um ponto de serviços de reporte que lhe permite executar relatórios. O Gestor de Configuração suporta as mesmas versões do SQL Server para reportar como faz para a base de dados do site.

Para mais informações, consulte [os pré-requisitos para reportar no Gestor](../../servers/manage/prerequisites-for-reporting.md)de Configuração .

> [!IMPORTANT]  
> Depois de atualizar o SQL Server de uma versão anterior, poderá ver o seguinte erro: O Construtor de *Relatórios não existe*.  
> Para resolver este erro, deve reinstalar a função do sistema de pontos de ponto de serviços de reporte.  

### <a name="data-warehouse-service-point"></a>Ponto de serviço de armazém de dados

O armazém de dados usa uma base de dados separada. Pode ser hospedado no servidor de base de dados do site ou num Servidor SQL separado. Para mais informações, consulte o ponto de serviço do armazém de [dados para O Gestor de Configuração](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>Portas do Servidor SQL

Para comunicação ao motor de base de dados Do Servidor SQL e à replicação inter-local, pode utilizar as configurações de porta padrão do Servidor SQL ou especificar portas personalizadas:  

- **As comunicações inter-locais** utilizam o Corretor de Serviços de Servidor EsqL, que utiliza a porta TCP 4022 por padrão.  
- **As comunicações intra-locais** entre o motor de base de dados do Servidor SQL e várias funções do sistema do site do Gestor de Configuração utilizam a porta TCP 1433 por padrão. As seguintes funções do sistema de sites comunicam diretamente com a base de dados do SQL Server:  

  - Ponto de gestão  
  - Computador do Fornecedor de SMS  
  - Ponto do Reporting Services  
  - Servidor do site  

Quando um computador que executa o SQL Server acolhe uma base de dados de mais de um site, cada base de dados deve utilizar uma instância separada do Servidor SQL. Além disso, cada instância deve ser configurada para utilizar um conjunto único de portas.  

> [!WARNING]  
> O Gestor de Configuração não suporta portas dinâmicas. Uma vez que, por predefinição, as instâncias nomeadas de SQL Server utilizam portas dinâmicas para ligações ao motor da base de dados, quando utilizar uma instância nomeada tem de configurar manualmente a porta estática que pretende utilizar para comunicação entre sites.  

Se tiver uma firewall ativada no computador que está a executar o SQL Server, certifique-se de que está configurada para permitir as portas que estão a ser utilizadas pela sua implementação e em quaisquer localizações da rede entre computadores que comunicam com o Servidor SQL.  

Para um exemplo de como configurar o SQL Server para utilizar uma porta específica, consulte [configurar um servidor para ouvir uma porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Opções de upgrade para SQL Server

Se necessitar de atualizar a sua versão do SQL Server, utilize um dos seguintes métodos, de fácil a mais complexo:  

- [Atualize o Servidor SQL no local](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (recomendado)  

- Instale uma nova versão do SQL Server num novo computador e, em seguida, [use a opção](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) de movimento de base de dados da configuração do Gestor de Configuração para apontar o servidor do seu site para o novo Servidor SQL  

- Utilize [cópias de segurança e recuperação.](../../servers/manage/backup-and-recovery.md) É suportado o uso de backup e recuperação para um cenário de upgrade SQL. Pode ignorar o requisito de versão SQL ao rever [considerações antes](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site)de recuperar um site .
