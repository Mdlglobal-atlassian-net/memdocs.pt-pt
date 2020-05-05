---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Plano para usar um servidor SQL sempre em grupo de disponibilidade com Gestor de Configuração
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9e2e4e85d9fb6a1ab34af8760e0ac61d6e4fab4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718302"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Prepare-se para usar o Servidor SQL sempre em grupos de disponibilidade com O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize este artigo para preparar o Gestor de Configuração para utilizar o Servidor SQL sempre em grupos de disponibilidade. Esta funcionalidade fornece uma solução de alta disponibilidade e recuperação de desastres para a base de dados do site.  

O Gestor de Configuração suporta a utilização de grupos de disponibilidade:

- Nos locais primários e no local da administração central.
- No local, ou no Microsoft Azure.

Quando utiliza grupos de disponibilidade no Microsoft Azure, pode aumentar ainda mais a disponibilidade da base de dados do seu site utilizando conjuntos de *disponibilidade do Azure*. Para obter mais informações sobre Conjuntos de Disponibilidade do Azure, veja [Gerir a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
> Antes de continuar, sinta-se confortável com a configuração de grupos de disponibilidade do SQL Server e do SQL Server. A informação que segue refere a biblioteca e procedimentos de documentação do Servidor SQL.


## <a name="supported-scenarios"></a>Cenários suportados

Os seguintes cenários são suportados para a utilização de grupos de disponibilidade com O Gestor de Configuração. Para obter mais informações e procedimentos para cada cenário, consulte os grupos de [disponibilidade do Configure para O Gestor](configure-aoag.md)de Configuração .

- [Criar um grupo de disponibilidade para uso com o Gestor de Configuração](configure-aoag.md#bkmk_create)  
- [Configure um site para usar o grupo de disponibilidade](configure-aoag.md#bkmk_configure)  
- [Adicione ou remova membros de réplica sincronizados de um grupo de disponibilidade que acolhe uma base de dados do site](configure-aoag.md#bkmk_sync)  
- [Configure ou recupere um site de uma réplica assíncrona](configure-aoag.md#bkmk_async)  
- [Mova uma base de dados do site de um grupo de disponibilidade para uma instância padrão ou nomeada de um Servidor SQL autónomo](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos aplicam-se a todos os cenários. Se os pré-requisitos adicionais se aplicarem a um cenário específico, são detalhados com esse cenário.

### <a name="configuration-manager-accounts-and-permissions"></a>Contas e permissões do Gestor de Configuração

#### <a name="installation-account"></a>Conta de instalação

A conta que utiliza para executar a configuração do Gestor de Configuração deve ser:

- Um membro do grupo de **administradores locais** em cada computador que é membro do grupo de disponibilidade.
- Uma **sisadmina** em cada instância do SQL Server que acolhe a base de dados do site.

#### <a name="site-server-to-replica-member-access"></a>Servidor do site para replicar acesso a membro

A conta de computador do servidor do site deve ser um membro do grupo **de Administradores locais** em cada computador que seja membro do grupo de disponibilidade.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Versão

Cada réplica do grupo de disponibilidade deve executar uma versão do SQL Server que é suportada pela sua versão de 'Gestor de Configuração'. Quando suportados pelo SQL Server, diferentes nós de um grupo de disponibilidade podem executar diferentes versões do SQL Server. Para mais informações, consulte [as versões Suportadas Do Servidor SQL para O Gestor](../../../plan-design/configs/support-for-sql-server-versions.md)de Configuração .<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edição

Utilize uma edição *enterprise* do SQL Server.

#### <a name="account"></a>Conta

Cada instância do SQL Server pode ser executada sob uma conta de utilizador de domínio (conta de**serviço)** ou uma conta não-domínio. Cada réplica de um grupo pode ter uma configuração diferente.

- Use uma conta com as mais baixas permissões possíveis. Para mais informações, consulte [considerações de segurança para uma instalação do Servidor SQL](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Para obter mais informações sobre a configuração de contas de serviço e permissões para o Servidor SQL, consulte [as contas e permissões](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)do serviço Do Windows Configurar .  

- Para utilizar uma conta não-domínio, deve utilizar certificados. Para mais informações, consulte [Os certificados de utilização para um ponto final espelhado na base de dados (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Para mais informações, consulte [Criar uma base de dados espelhando o ponto final para sempre em grupos de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Base de Dados

#### <a name="configure-the-database-on-a-new-replica"></a>Configure a base de dados sobre uma nova réplica

Configure a base de dados de cada réplica com as seguintes definições:  

- Ativar a **integração clr:**

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Para mais informações, consulte a [integração do CLR.](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling)  

- Definir **tamanho de repl de texto Max** para: `2147483647`  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Desloque o proprietário da base de dados para a *conta SA*. Não precisas de ativar esta conta.

- LIGUE **ON** a definição **de FIABILIDADE:**

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Para mais informações, consulte a propriedade de base de [dados FIDeDIGNO](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).

- Ativar o Corretor de **Serviços:**  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Não é possível ativar a opção Service Broker numa base de dados que já faz parte de um grupo de disponibilidade. Tem de ativar essa opção antes de a adicionar ao grupo de disponibilidade.<!-- SCCMDocs#1432 -->

- Configure a prioridade do Corretor de Serviços:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Só faça estas configurações numa réplica primária. Para configurar uma réplica secundária, primeiro falhe sobre a primária para a secundária. Esta ação faz do secundário a nova réplica primária.

#### <a name="database-verification-script"></a>Script de verificação de base de dados

Executar o seguinte script SQL para verificar configurações de base de dados para réplicas primárias e secundárias. Antes de conseguir resolver um problema numa réplica secundária, mude a réplica secundária para ser a réplica principal.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade

#### <a name="replica-members"></a>Membros da réplica

- O grupo de disponibilidade deve ter uma réplica primária.  

- Utilize o mesmo número e tipo de réplicas num grupo de disponibilidade que a sua versão do SQL Server suporta.

- Podes usar uma réplica assíncrona para recuperar a tua réplica sincronizada. Para mais informações, consulte as opções de [recuperação da base de dados](../../manage/recover-sites.md#site-database-recovery-options)do site.  

    > [!Warning]  
    > O Gestor de Configuração não suporta a falha de *utilização* da réplica de compromisso assíncrono como base de dados do site. Para mais informações, consulte [os modos Failover e Failover (sempre em grupos de disponibilidade)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

O Gestor de Configuração não valida o estado da réplica assíncrona para confirmar a sua corrente. A utilização de uma réplica de compromisso assíncrono, uma vez que a base de dados do site pode colocar em risco a integridade do seu site e dados. Esta réplica pode estar dessincronizada por design. Para mais informações, consulte a [visão geral do Servidor SQL Sempre em grupos de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Cada membro da réplica deve ter a seguinte configuração:

- Utilize a *instância predefinida* ou uma *instância nomeada*  

- A definição de **Funções Primárias é** **Permitir todas as ligações**  

- O cenário **secundário legível** é **sim**  

- Ativado para **falha manual**

    > [!Note]
    > Na versão 1902 e anterior, você precisa configurar todos os grupos de disponibilidade no Servidor SQL para falha manual. Esta configuração é necessária mesmo que não seja hospedada na base de dados do site.
    >
    > A partir da versão 1906, o Gestor de Configuração suporta a utilização de réplicas sincronizadas do grupo de disponibilidade quando definida para **Falha Automática**. Definir **falha manual** quando:
    >
    > - Executa a configuração do Gestor de Configuração para especificar a utilização da base de dados do site no grupo de disponibilidade.  
    > - Instale qualquer atualização no 'Gestor de Configuração'. (Não apenas atualizações que se aplicam à base de dados do site).  

- Todos os membros precisam do mesmo modo de [sementem.](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)<!-- SCCMDocs-pr#3899 --> A configuração do Gestor de Configuração inclui uma verificação pré-requisito para verificar esta configuração ao criar uma base de dados através da instalação ou recuperação.

    > [!Note]  
    > Quando a configuração cria a base de dados e configura a sementeautomática **automática,** o grupo de disponibilidade deve ter permissões para criar a base de dados. Este requisito aplica-se tanto a uma nova base de dados como a uma recuperação. Para obter mais informações, consulte [a sementeira automática para réplica secundária](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Localização do membro da réplica

Ou hospeda todas as réplicas num grupo de disponibilidade no local, ou hospeda-as todas no Microsoft Azure. Um grupo que inclui um membro no local e um membro em Azure não é apoiado.

A configuração do Gestor de Configuração tem de se ligar a cada réplica. Quando configurar um grupo de disponibilidade em Azure, e o grupo estiver por trás de um equilibrador de carga interna ou externa, abra as seguintes portas padrão:

- Mapper de ponto final RPC: **TCP 135**

- Corretor de serviço sql server: **TCP 4022**  

- SQL sobre TCP: **TCP 1433**

Após a configuração concluída, as seguintes portas devem permanecer abertas para O Gestor de Configuração:  

- Corretor de serviço sql server: **TCP 4022**  

- SQL sobre TCP: **TCP 1433**  

Pode utilizar portas personalizadas para estas configurações. Utilize as mesmas portas personalizadas até ao ponto final e em todas as réplicas do grupo de disponibilidade.

#### <a name="listener"></a>Serviço de Escuta

O grupo de disponibilidade tem de ter, pelo menos, um *serviço de escuta do grupo de disponibilidade*. Quando configura o Gestor de Configuração para utilizar a base de dados do site no grupo de disponibilidade, utiliza o nome virtual deste ouvinte. Embora um grupo de disponibilidade possa conter vários ouvintes, o Gestor de Configuração só pode fazer uso de um. Para mais informações, consulte Criar ou configurar um ouvinte do [grupo de disponibilidade do SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Caminhos de arquivo

Quando executa a configuração do Gestor de Configuração para configurar um site para utilizar a base de dados num grupo de disponibilidade, cada servidor de réplica secundária deve ter um ficheiro SQL Server idêntico ao caminho de ficheiro si para os ficheiros da base de dados do site na réplica primária atual. Se não existir um caminho idêntico, a configuração não consegue adicionar a instância para o grupo de disponibilidade como a nova localização da base de dados do site.  

A conta de serviço SQL Server local deve ter permissão de **Controlo Total** para esta pasta.

Os servidores de réplica secundários só requerem este caminho de ficheiro enquanto está a utilizar a configuração do 'Gestor de Configuração' para especificar a instância de base de dados no grupo de disponibilidade. Depois de completar a configuração da base de dados do site no grupo de disponibilidade, pode eliminar o caminho não utilizado a partir de réplicas secundárias.

Por exemplo, considere os seguintes cenários:

- Cria um grupo de disponibilidade que utiliza três Servidores SQL.  

- O servidor de réplica primária é uma nova instalação do SQL Server 2014. Por padrão, armazena a base de dados. MDF e. Ficheiros LDF em `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Atualizou ambos os seus servidores de réplica secundária para SQL Server 2014 a partir de versões anteriores. Com a atualização, estes servidores mantêm o `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`caminho original do ficheiro para armazenar ficheiros de base de dados: .  

- Antes de mover a base de dados do site para este grupo `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`de disponibilidade, em cada servidor de réplica secundária, crie o seguinte caminho de ficheiro: . Este caminho é uma duplicação do caminho em uso na réplica primária, mesmo que as réplicas secundárias não utilizem esta localização de ficheiros.  

- Em seguida, concede a conta de serviço SQL Server em cada réplica secundária de acesso total ao controlo completo da localização do ficheiro recém-criada nesse servidor.  

- Agora pode executar com sucesso a configuração do Gestor de Configuração para configurar o site para utilizar a base de dados do site no grupo de disponibilidade.  

#### <a name="multi-subnet-failover"></a>Falha de rede multi-subnet

<!-- SCCMDocs-pr#3734 -->
A partir da versão 1906, pode ativar a palavra-chave de linha de [ligação MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) no Servidor SQL. Também é necessário adicionar manualmente os seguintes valores ao Registo do Windows no servidor do site:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> A utilização da [alta disponibilidade](site-server-high-availability.md) do servidor do site e do Servidor SQL Always On com falha multi-subnet não fornece as capacidades completas de falha automática para cenários de recuperação de desastres.

Se precisar de criar um grupo de disponibilidade com um membro num local remoto, priorize com base na latência de rede mais baixa. A alta latência da rede pode causar falhas de replicação.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

As seguintes limitações aplicam-se a todos os cenários.

### <a name="unsupported-sql-server-options-and-configurations"></a>Opções e configurações do Servidor SQL não suportados

- **Grupos básicos**de disponibilidade : Introduzido sQL Server 2016 Edição Standard, os grupos básicos de disponibilidade não suportam o acesso a réplicas secundárias. A configuração requer este acesso. Para mais informações, consulte [os grupos básicos](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017)de disponibilidade do Servidor SQL .  

- Caso de **cluster failover**: As instâncias de cluster failover não são suportadas para uma réplica que utiliza com o Gestor de Configuração. Para mais informações, consulte [o SQL Server Always On On failover casos de cluster](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: Na versão 1902 e anterior, não é suportado para utilizar um grupo de disponibilidade com o Gestor de Configuração numa configuração multi-sub-rede. Também não pode utilizar a cadeia de ligação de palavras-chave [MutliSubnetFailover.](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)

    Para suportar esta configuração, atualize o 'Configuração', para versão 1906 ou posterior. Para obter mais informações, consulte o pré-requisito de falha da [multi-sub-rede.](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)

### <a name="sql-servers-that-host-additional-availability-groups"></a>Servidores SQL que acolhem grupos de disponibilidade adicionais

<!--SCCMDocs issue 649-->
Quando o Servidor SQL acolhe um ou mais grupos de disponibilidade para além do grupo que utiliza para o Gestor de Configuração, necessita de configurações específicas no momento em que executa a configuração do Gestor de Configuração. Estas definições também são necessárias para instalar uma atualização para O Gestor de Configuração. Cada réplica de cada grupo de disponibilidade deve ter as seguintes configurações:

- Manual Failover  
- Permitir qualquer ligação apenas para leitura  

> [!Note]
> Na versão 1902 e anterior, você precisa configurar todos os grupos de disponibilidade no Servidor SQL para falha manual. Esta configuração é necessária mesmo que não seja hospedada na base de dados do site.
>
> A partir da versão 1906, o Gestor de Configuração suporta a utilização de réplicas sincronizadas do grupo de disponibilidade quando definida para **Falha Automática**. Definir **falha manual** quando:
>
> - Executa a configuração do Gestor de Configuração para especificar a utilização da base de dados do site no grupo de disponibilidade.  
> - Instale qualquer atualização no 'Gestor de Configuração'. (Não apenas atualizações que se aplicam à base de dados do site).  

### <a name="unsupported-database-use"></a>Utilização não suportada da base de dados

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>O Gestor de Configuração suporta apenas a base de dados do site num grupo de disponibilidade

As seguintes bases de dados não são suportadas pelo Gestor de Configuração num grupo de disponibilidade do SQL Server Always On:  

- Base de dados de relatórios  
- Base de dados do WSUS  

#### <a name="pre-existing-database"></a>Base de dados pré-existente

Não podes usar uma nova base de dados criada na réplica. Quando configurar um grupo de disponibilidade, restaure uma cópia de uma base de dados existente do Gestor de Configuração para a réplica primária.  

#### <a name="distributed-views"></a>Vistas distribuídas

<!-- SCCMDocs-pr#3792 -->
Na versão 1902 e anterior, se hospedar a base de dados do site num grupo de disponibilidade do SQL Server Always On, não é possível ativar [vistas distribuídas](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) para replicação de bases de dados. Para suportar esta configuração, atualize para a versão 1906 ou mais tarde.


### <a name="setup-errors-in-configmgrsetuplog"></a>Erros de configuração em ConfigMgrSetup.log

Quando executa a configuração do Gestor de Configuração para mover uma base de dados do site para um grupo de disponibilidade, tenta processar funções de base de dados nas réplicas secundárias do grupo de disponibilidade. O ficheiro **ConfigMgrSetup.log** mostra o seguinte erro:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Estes erros são seguros de ignorar.

### <a name="site-expansion"></a>Expansão do site

<!--SCCMDocs issue 568-->
Se configurar a base de dados do site para um site primário autónomo para utilizar o SQL Always On, não pode expandir o site para incluir um site de administração central. Se tentar este processo, falha. Para expandir o site, remova temporariamente a base de dados do site primário do grupo de disponibilidade.

Não é necessário fazer alterações na configuração ao adicionar um site secundário.


## <a name="changes-for-site-backup"></a>Alterações para backup do site

### <a name="backup-database-files"></a>Ficheiros de base de dados de backup
  
Quando uma base de dados do site utiliza um grupo de disponibilidade, execute a tarefa de manutenção do servidor do site de **backup** incorporado para fazer backup das definições e ficheiros comuns do Gestor de Configuração. Não use o. MDF ou . Ficheiros LDF criados por essa cópia de segurança. Em vez disso, faça cópias de segurança diretas destes ficheiros de base de dados utilizando o SQL Server.

### <a name="transaction-log"></a>Registo de transações  

Desloque o modelo de recuperação da base de dados do site para **Full**. Esta configuração é um requisito para a utilização do Gestor de Configuração num grupo de disponibilidade. Planeie monitorizar e manter o tamanho do registo de transações da base de dados do site. No modelo de recuperação completo, as transações não são endurecidas até que faça uma cópia de segurança completa da base de dados ou do registo de transações. Para mais informações, consulte [O Back up e restaure as bases de dados do SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Alterações para recuperação do site

Se pelo menos um nó do grupo de disponibilidade ainda estiver funcional, utilize a opção de recuperação do site para saltar a recuperação da base de **dados (Utilize esta opção se a base**de dados do site não tiver sido afetada) .

A partir da versão 1906, a recuperação do site pode recriar a base de dados num grupo SQL Always On. Este processo funciona com sementeção manual e automática.<!-- SCCMDocs-pr#3846 -->

Na versão 1902 ou mais cedo, quando perde todos os nós de um grupo de disponibilidade, antes de poder recuperar o site, recrie primeiro o grupo de disponibilidade. O Gestor de Configuração não pode reconstruir ou restaurar o nó de disponibilidade. Recrie o grupo, restaure a cópia de segurança e reconfigure o SQL. Em seguida, utilize a opção de recuperação do site para saltar a **recuperação da base de dados (Utilize esta opção se a base**de dados do site não tiver sido afetada) .

Para mais informações, consulte [Backup e recuperação.](../../manage/backup-and-recovery.md)


## <a name="changes-for-reporting"></a>Alterações para reporte

### <a name="install-the-reporting-service-point"></a>Instale o ponto de serviço de reporte

O ponto de serviços de reporte não suporta o uso do nome virtual do ouvinte do grupo de disponibilidade. Também não suporta hospedar a sua base de dados num grupo de disponibilidade SQL Server Always On.  

- Por predefinição, a instalação de pontos de ponto de serviços de reporte define o nome do servidor de base de **dados do Site** para o nome virtual especificado como ouvinte. Altere esta definição para especificar um nome de computador e instância de uma réplica no grupo de disponibilidade.  

- Para descarregar relatórios e aumentar a disponibilidade quando um nó de réplica estiver offline, considere instalar pontos adicionais de serviços de reporte em cada nó de réplica. Em seguida, configure cada serviço de reporte apontar para usar o seu próprio nome de computador. Ao instalar um ponto de serviço de reporte em cada réplica do grupo de disponibilidade, o relatório pode sempre ligar-se a um servidor de pontode reporte ativo.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Altere o ponto de serviços de reporte utilizado pela consola

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.**

1. Na fita, selecione **Opções**de Relatório .  

1. Na caixa de diálogo Report Options, selecione o ponto de serviços de reporte que pretende utilizar.  


## <a name="next-steps"></a>Passos seguintes

Este artigo descreve os pré-requisitos, limitações e alterações às tarefas comuns que o Gestor de Configuração necessita quando utiliza grupos de disponibilidade. Para que os procedimentos configuram e configurem o seu site para utilizar grupos de disponibilidade, consulte grupos de [disponibilidade configure](configure-aoag.md).
