---
title: Cluster do servidor SQL
titleSuffix: Configuration Manager
description: Utilize um cluster de servidor SQL para hospedar a base de dados do site do Gestor de Configuração
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d035e6fbd776a03ce38a4cd0fc12755100b60c91
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643251"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Utilize um cluster de servidor SQL para a base de dados do site

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar um cluster SQL Server Failover para alojar a base de dados do site do Gestor de Configuração. Um cluster fornece suporte de failover e melhora a fiabilidade da base de dados do site. No entanto, não fornece benefícios adicionais de processamento ou de equilíbrio de carga. Além disso, um cluster SQL Server Failover utiliza armazenamento partilhado e introduz um único ponto de falha. A degradação do desempenho pode ocorrer, porque o servidor do site deve encontrar o nó ativo do cluster Do Servidor SQL antes de se ligar à base de dados do site.  

> [!IMPORTANT]  
> A configuração bem sucedida de clusters Do Servidor SQL baseia-se na documentação e procedimentos fornecidos na biblioteca de documentação do Servidor SQL.  


Antes de instalar o Gestor de Configuração, prepare o cluster do Servidor SQL para suportar o Gestor de Configuração. Para mais informações, consulte [Prepare uma instância de Servidor SQL agrupada](#bkmk_prepare).

Durante a configuração do Gestor de Configuração, o escritor do Serviço de Cópia sinuosa do Windows Volume Shadow instala em cada nó de computador físico do cluster do Microsoft Windows Server. Este serviço suporta a tarefa de manutenção do Servidor do Servidor do **Site de Backup.**  

Após a instalação do site, o Gestor de Configuração verifica se há alterações no nó de cluster a cada hora. O Gestor de Configuração gere automaticamente quaisquer alterações que afetem as instalações do seu componente. Por exemplo, um nó failover, ou a adição de um novo nó ao cluster SQL Server.  



## <a name="supported-options"></a>Opções suportadas

As seguintes opções são suportadas para clusters de failover do Servidor SQL utilizados como base de dados do site:

- Um aglomerado de instância única  

- Configurações de várias instâncias  

- Vários nós ativos  

- Tanto um nome como uma instância padrão  



## <a name="prerequisites"></a>Pré-requisitos

Esteja atento aos seguintes pré-requisitos:  

- A base de dados do site tem de ser remota em relação ao servidor do site. O cluster não pode incluir o servidor do sistema do site.  

    > [!Note]  
    > A partir da versão 1810, o processo de configuração do Gestor de Configuração já não bloqueia a instalação da função do servidor do site num computador com a função Windows para o Clusterfailover. Anteriormente, não conseguia saqueá-lo na base de dados do site no servidor do site. Com esta alteração, pode criar um site altamente disponível com menos servidores utilizando um cluster SQL e um servidor de site em modo passivo. Para mais informações, consulte [Opções de Alta Disponibilidade](high-availability-options.md). <!--3607761, fka 1359132-->  

- Adicione a conta de computador do servidor do site ao grupo de **Administradores locais** de cada servidor no cluster.  

- Para suportar a autenticação kerberos, ative o protocolo de comunicação de rede **TCP/IP** para a ligação de rede de cada nó de cluster do Servidor SQL. O protocolo **de tubos nomeados** não é necessário, mas pode ser usado para resolver problemas de autenticação kerberos. As definições do protocolo de rede estão configuradas no Gestor de Configuração do **Servidor SQL,** sob a configuração da **rede do servidor SQL**.  

- Existem requisitos específicos de certificado quando utiliza um cluster SQL Server para a base de dados do site. Para obter mais informações, veja os artigos seguintes:
  - [Instale um certificado numa configuração de cluster de failover SQL](https://docs.microsoft.com/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [Requisitos de certificado PKI para o Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > Se não fornecer um certificado no SQL, o Gestor de Configuração cria e disponibiliza um certificado auto-assinado para a SQL.<!-- 7099499 -->

## <a name="limitations"></a>Limitações

Considere as seguintes limitações:  


### <a name="installation-and-configuration"></a>Instalação e configuração

- Sites secundários não podem usar um cluster de Servidor SQL.  

- Quando especifica um cluster do Servidor SQL, a opção de especificar localizações de ficheiros não predefinidos para a base de dados do site não está disponível.  


### <a name="sms-provider"></a>Fornecedor de SMS

Não é possível instalar uma instância do Fornecedor SMS num cluster de servidor SQL. Também não é suportado num computador que funciona como um nó de Servidor SQL agrupado.  


### <a name="data-replication-options"></a>Opções de replicação de dados

Se utilizar **pontos de vista distribuídos,** não pode utilizar um cluster do Servidor SQL para alojar a base de dados do site.  


### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação

O Gestor de Configuração não suporta a cópia de segurança do Gestor de Proteção de Dados (DPM) para um cluster de Servidor SQL que utiliza uma instância nomeada. Suporta a cópia de segurança DPM num cluster do Servidor SQL que utiliza a instância padrão do Servidor SQL.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a>Preparar uma instância de Servidor SQL agrupada  

Aqui estão as principais tarefas a completar para preparar a base de dados do seu site:

- Crie o cluster virtual do SQL Server para alojar a base de dados do site num ambiente de cluster do Windows Server existente. Para obter passos específicos para instalar e configurar um cluster SQL Server, consulte a documentação específica da sua versão do Servidor SQL. Para mais informações, consulte Criar um novo Cluster de Falha do [Servidor SQL](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- Em cada computador do cluster Do Servidor SQL, coloque um ficheiro na pasta raiz de cada unidade onde não pretenda que o Gestor de Configuração instale componentes do site. Dê o nome `NO_SMS_ON_DRIVE.SMS` ao ficheiro. Por predefinição, o Gestor de Configuração instala alguns componentes em cada nó físico, para suportar operações como backup.  

- Adicione a conta de computador do servidor do site ao grupo de **Administradores locais** de cada computador de cluster do Windows Server.  

- Na instância virtual do Servidor SQL, atribuir a função de Servidor **SQL sysadmin** à conta de utilizador que executa a configuração do Gestor de Configuração.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site utilizando um SQL Server em cluster  

Para instalar um site que utilize uma base de dados de site agrupada, executar configuração do Gestor de Configuração seguindo o seu processo normal para instalar um site, com a seguinte alteração:  

- Na página **Informações da Base de Dados** , especifique o nome da instância virtual do cluster do SQL Server que irá alojar a base de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    > Quando introduzir o nome da instância virtual do cluster Do Servidor SQL, não introduza o nome virtual do Windows Server criado pelo cluster do Windows Server. Se utilizar o nome virtual do Windows Server, a base de dados do site instala-se no disco rígido local do nó de cluster do Windows Server ativo. Isto impede a ativação pós-falha bem sucedida se esse nó falhar.  
