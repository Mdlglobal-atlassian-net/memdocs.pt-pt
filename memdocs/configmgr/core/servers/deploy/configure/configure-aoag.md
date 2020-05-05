---
title: Configure grupos de disponibilidade
titleSuffix: Configuration Manager
description: Configurar e gerir o Servidor SQL sempre em grupos de disponibilidade com O Gestor de Configuração
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721081"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configure o servidor SQL sempre em grupos de disponibilidade para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para configurar e gerir os grupos de disponibilidade que utiliza com o Gestor de Configuração.

Antes de começar:  

- Esteja familiarizado com as informações do Prepare para utilizar o [Servidor SQL Sempre em grupos de disponibilidade com o Gestor](sql-server-alwayson-for-a-highly-available-site-database.md)de Configuração .
- Conheça a documentação do SQL Server que cobre o uso de grupos de disponibilidade e procedimentos relacionados. Essa informação é necessária para completar os seguintes cenários.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a>Criar e configurar um grupo de disponibilidade

Utilize o seguinte procedimento para criar um grupo de disponibilidade e, em seguida, mover uma cópia da base de dados do site para esse grupo de disponibilidade.

1. Utilize o seguinte comando para parar o site do Gestor de Configuração:

    `preinst.exe /stopsite`

    Para mais informações, consulte a ferramenta de manutenção da [Hierarquia.](../../manage/hierarchy-maintenance-tool-preinst.exe.md)

2. Altere o modelo de backup para a base de dados do site de **SIMPLE** a **FULL:**

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Os grupos de disponibilidade suportam apenas o modelo full backup. Para mais informações, consulte [Ver ou alterar o modelo de recuperação de uma base de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Utilize o Servidor SQL para criar uma cópia de segurança completa da base de dados do seu site. Selecione uma das seguintes opções:

    - **Será membro do seu grupo de disponibilidade**: Se utilizar este servidor como membro principal da réplica inicial do grupo de disponibilidade, não precisa de restaurar uma cópia da base de dados do site para este servidor ou outra no grupo. A base de dados já está em vigor na réplica primária. O SQL Server replica a base de dados para as réplicas secundárias durante um passo posterior.  

    - **Não será membro do grupo de disponibilidade**: Restaurar uma cópia da base de dados do site no servidor que irá acolher a réplica primária do grupo.

    Para mais informações, consulte os seguintes artigos na documentação do Servidor SQL:

    - [Criar uma cópia de dados completa](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Restaurar uma cópia de segurança da base de dados utilizando SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Se planeia passar de um grupo de disponibilidade para autónomo numa réplica existente, primeiro remova a base de dados do grupo de disponibilidade.

4. No servidor que irá acolher a réplica primária inicial do grupo, use o [novo assistente](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) do grupo de disponibilidade para criar o grupo de disponibilidade. No assistente:

    - Na página **'Base** de Dados Select', selecione a base de dados para o site do Gestor de Configuração.  

    - Na página **Especificar Réplicas** , configure:

        - **Réplicas:** Especifique os servidores que irão acolher réplicas secundárias.

        - **Ouvinte:** Especifique o **nome DNS** do ouvinte `<listener_server>.fabrikam.com`como um nome DNS completo, por exemplo . Quando configura o Configuro Gestor de Configuração para utilizar a base de dados no grupo de disponibilidade, utiliza este nome.

    - Na página **Selecionar Sincronização de Dados Inicial** , selecione **Completa**. Depois de o assistente criar o grupo de disponibilidade, o assistente confirma a base de dados primária e o registo de transações. Em seguida, o assistente restaura-os em cada servidor que acolhe uma réplica secundária.

        > [!Note]  
        > Se não utilizar este passo, devolva uma cópia da base de dados do site a cada servidor que acolhe uma réplica secundária. Em seguida, junte-se manualmente a essa base de dados ao grupo.

5. Verifique a configuração de cada réplica:

    1. Certifique-se de que a conta de computador do servidor do site é membro do grupo **de Administradores locais** em cada computador que é membro do grupo de disponibilidade.  

    2. Execute o script de [verificação](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) para confirmar que a base de dados do site em cada réplica está corretamente configurada.

    3. Se for necessário definir configurações em réplicas secundárias, antes de continuar, falha manualmente sobre a réplica primária para a réplica secundária. Só é possível configurar a base de dados de uma réplica primária. Para mais informações, consulte [Executar uma falha manual planeada de um grupo de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do Servidor SQL.

6. Depois de todas as réplicas satisfazerem os requisitos, o grupo de disponibilidade está pronto para ser utilizado com o Gestor de Configuração.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a>Configure um site para usar o grupo de disponibilidade

Depois de [criar e configurar o grupo](#bkmk_create)de disponibilidade, utilize a manutenção do site do Gestor de Configuração para configurar o site para utilizar a base de dados que o grupo de disponibilidade acolhe.

Não é suportado para instalar um novo site com a sua base de dados num grupo de disponibilidade. Por exemplo, se utilizar os meios de base, instale o site utilizando uma única instância do Servidor SQL. Depois de o site instalar, em seguida, mover a base de dados do site para o grupo de disponibilidade.

1. Configuração do Gestor `\BIN\X64\setup.exe` de Configuração de **Execução**: da pasta de instalação do site do Gestor de Configuração.

2. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este site**, e, em seguida, selecione **Next**.

3. Selecione Modificar a **configuração do Servidor SQL**, e, em seguida, selecione **Next**.

4. Reconfigurar as seguintes definições para a base de dados do site:

    - **Nome do Servidor SQL**: Introduza o nome virtual para o *ouvinte*do grupo de disponibilidade . Configurou o ouvinte quando criou o grupo de disponibilidade. O nome virtual deve ser um `<Listener_Server>.fabrikam.com`nome DNS completo, como .  

    - **Exemplo:** Para especificar a instância predefinida para o *ouvinte* do grupo de disponibilidade, este valor deve estar em branco. Se a base de dados do site atual for em uma instância nomeada, limpe a instância atual nomeada.

    - **Base de dados:** deixe o nome, tal como é apresentado. Este nome é a base de dados do site atual.

5. Depois de fornecer as informações para a nova localização da base de dados, complete a configuração com o seu processo e configurações normais.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a>Membros de réplica sincronizada  

Quando a base de dados do seu site estiver alojada num grupo de disponibilidade, utilize os seguintes procedimentos para adicionar ou remover membros de réplicasincronizados. Para obter mais informações sobre o tipo suportado e o número de réplicas, consulte [as configurações do grupo Disponibilidade](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a>Adicione um novo membro de réplica sincronizado

<!--3127336-->
A partir da versão 1906, executar configuração do Gestor de Configuração para adicionar um novo membro de réplica sincronizado.

1. Adicione uma réplica secundária utilizando os procedimentos do Servidor SQL.

    1. [Adicione uma réplica secundária a um Grupo Sempre Disponível](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Observe o estado no Estúdio de Gestão SQL. Aguarde que o grupo de disponibilidade regresse à saúde plena.

1. Executar configuração do Gestor de Configuração e selecionar a opção de modificar o site.

1. Especifique o nome do ouvinte do grupo de disponibilidade como nome da base de dados. Se o ouvinte utilizar uma porta de rede não normalizada, especifique-a também. Esta ação faz com que a configuração garanta que cada nó está devidamente configurado. Também inicia um processo de recuperação da base de dados.

A configuração do Gestor de Configuração utiliza a operação de movimento de movimento da base de dados SQL e certifica-se de que os nós estão corretamente configurados.

Para obter mais informações sobre como fazer este processo manualmente na versão 1902 ou mais cedo, consulte [ConfigMgr 1702: Adicionar um novo nó (Réplica Secundária) a um SQL AO AG existente.](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960)

### <a name="remove-a-replica-member"></a>Remover um membro da réplica

A partir da versão 1906, pode utilizar a configuração do 'Gestor de Configuração' para remover um membro da réplica. Use o mesmo processo para [adicionar um novo membro de réplica sincronizado](#bkmk_sync-add).

Para obter mais informações sobre como fazer este processo manualmente na versão 1902 ou mais cedo, consulte [Remover uma réplica secundária de um grupo de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a>Réplicas assíncronas

Pode utilizar uma réplica assíncrona no grupo de disponibilidade que utiliza com o Gestor de Configuração. Não é necessário executar os scripts de configuração necessários para configurar uma réplica sincronizada, porque uma réplica assíncrona não é suportada para a base de dados do site.

### <a name="configure-an-asynchronous-commit-replica"></a>Configure uma réplica de compromisso assíncrono

Para mais informações, consulte [Adicionar uma réplica secundária a um grupo de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Use a réplica assíncrona para recuperar o seu site

Use a réplica assíncrona para recuperar a base de dados do site.

1. Pare o site primário ativo para evitar escritos adicionais na base de dados do site. Para parar o local, utilize a ferramenta de manutenção da [Hierarquia:](../../manage/hierarchy-maintenance-tool-preinst.exe.md)`preinst.exe /stopsite`

1. Depois de parar o site, utilize a réplica assíncrona em vez de uma base de [dados recuperada manualmente](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a>Pare de usar um grupo de disponibilidade

Utilize o procedimento seguinte quando já não pretender alojar a base de dados do site num grupo de disponibilidade. Com este processo, irá mover a base de dados do site de volta para uma única instância do Servidor SQL.

1. Pare o site do Gestor de `preinst.exe /stopsite`Configuração utilizando o seguinte comando: . Para mais informações, consulte a ferramenta de manutenção da [Hierarquia.](../../manage/hierarchy-maintenance-tool-preinst.exe.md)

2. Utilize o SQL Server para criar uma cópia de segurança completa da sua base de dados do site a partir da réplica primária. Para mais informações, consulte [Criar uma cópia de segurança completa da base de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Utilize o SQL Server para restaurar a cópia de segurança da base de dados do site para o servidor que irá aloja a base de dados do site. Para mais informações, consulte [Restaurar uma cópia de segurança utilizando SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Se o servidor de réplica primária para o grupo de disponibilidade alojar a única instância da base de dados do site, ignore este passo.

4. No servidor que irá alojar a base de dados do site, altere o modelo de backup para a base de dados do site de **FULL** para **SIMPLE**. Para mais informações, consulte [Ver ou alterar o modelo de recuperação de uma base de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Configuração do Gestor `\BIN\X64\setup.exe` de Configuração de **Execução**: da pasta de instalação do site do Gestor de Configuração.

6. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este site**, e, em seguida, selecione **Next**.  

7. Selecione Modificar a **configuração do Servidor SQL**, e, em seguida, selecione **Next**.  

8. Reconfigurar as seguintes definições para a base de dados do site:

    - **Nome do SQL Server:** introduza o nome do servidor que aloja agora a base de dados do site.

    - **Exemplo:** Especifique a instância nomeada que acolhe a base de dados do site. Se a base de dados estiver na instância predefinida, deixe este campo em branco.

    - **Base de dados:** deixe o nome, tal como é apresentado. Este nome é a base de dados do site atual.

9. Depois de fornecer as informações para a nova localização da base de dados, complete a configuração com o seu processo e configurações normais. Quando a configuração estiver concluída, o site reinicia e começa a utilizar a nova localização da base de dados.

10. Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um grupo de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).
