---
title: Manutenção das atualizações de software
titleSuffix: Configuration Manager
description: Para manter atualizações no 'Gestor de Configuração', pode agendar a tarefa de limpeza wSUS, ou pode executá-la manualmente.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719786"
---
# <a name="software-updates-maintenance"></a>Manutenção das atualizações de software

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode agendar e executar tarefas de limpeza wSUS a partir da consola do Gestor de Configuração a partir das propriedades do Componente de Ponto de Atualização de Software. Quando selecionar pela primeira vez para executar a tarefa de limpeza WSUS, irá funcionar após a sincronização das próximas atualizações de software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para agendar e executar a tarefa de limpeza do WSUS

Agende o trabalho de limpeza wSUS executando os seguintes passos:

1. Na consola de Configuração Manager, navegue para**os sites**de**configuração** > do site de**visão geral** > da **administração.** > 
2. Selecione o site no topo da hierarquia do Gestor de Configuração.

3. Clique em **Configurar Componentes do Site** no grupo **Definições** e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.  

4. Reveja o comportamento da **Supersedence.** Modifique o comportamento, se necessário.

   ![screenshot comportamento de supersedência](media/supersedence-behavior.png)

5. Clique no separador Regras de **Supersedência,** selecione Executar o assistente de **limpeza WSUS**. Na versão 1806, a opção é renomeada para **run WSUS cleanup após sincronização**.

6. Clique **em OK** (Clique em **Fechar** se estiver a executar a versão 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamento de limpeza wSUS na versão 1802 e anterior

Antes da versão 1806 do Gestor de Configuração, a opção de limpeza WSUS executa o seguinte item:

- A opção de **atualizações expiradas** do assistente de limpeza WSUS apenas no servidor WSUS do site de topo.

  ![WSUS expirada imagem de limpeza de atualização](media/wsus-cleanup-expired.PNG)

- Uma limpeza para itens de configuração de atualização de software na base de dados do Gestor de Configuração ocorre de sete em sete dias e remove atualizações desnecessárias da consola.
  - Esta limpeza não removerá as atualizações expiradas da consola do Gestor de Configuração se estiverem atualmente implementadas.

Ainda é necessária uma manutenção adicional na base de dados wsus de alto nível e em todas as outras bases de dados wSUS no ambiente. Para mais informações e instruções, consulte o guia completo para o [Microsoft WSUS e](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) o blog de manutenção SUP do Gestor de Configuração.

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamento de limpeza wSUS a partir da versão 1806

A partir da versão 1806, a opção de limpeza WSUS ocorre após cada sincronização e faz os seguintes itens de limpeza:
<!--1357898 -->

- A opção de **atualizações expiradas** para servidores WSUS no CAS e nos principais sites.
  - Os servidores WSUS para sites secundários não executam a limpeza WSUS para atualizações expiradas.
- O Gestor de Configuração constrói uma lista de atualizações supersed a partir da sua base de dados. A lista baseia-se no comportamento da supersedência nas propriedades dos componentes do Software Update Point.
  - Os itens de configuração da atualização que satisfaçam os critérios de comportamento da supersedência expiram na consola do Gestor de Configuração.
  - As atualizações são recusadas no WSUS para cas e locais primários, mas não para sites secundários.
- Uma limpeza para itens de configuração de atualização de software na base de dados do Gestor de Configuração ocorre de sete em sete dias e remove atualizações desnecessárias da consola.
  - Esta limpeza não removerá as atualizações expiradas da consola do Gestor de Configuração se estiverem atualmente implementadas.

> [!NOTE]
> Os "Meses para esperar até que uma atualização supersed seja expirada" baseiam-se na data de criação da atualização de superseding. Por exemplo, se utilizar 2 meses para esta definição, as atualizações que foram substituídos serão recusadas no WSUS e expiradas no Gestor de Configuração quando a atualização de superceding tiver 2 meses.

Toda a manutenção da WSUS tem de ser executada manualmente nas bases de dados do Site Secundário WSUS. As seguintes opções do Assistente de Limpeza do **Servidor WSUS** não são executadas no CAS e nos sites primários:

- Atualizações não utilizadas e revisões de atualizações
- Computadores que não contactam o servidor
- Ficheiros de atualização desnecessários

  Para mais informações e instruções, consulte o guia completo para o [Microsoft WSUS e](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) o blog de manutenção SUP do Gestor de Configuração.

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Comportamento de limpeza wSUS a partir da versão 1810

A partir da versão 1810, pode especificar regras de supersedência para atualizações de funcionalidades separadamente de atualizações não-funcionalidades nas propriedades dos componentes do Software Update Point. A opção de limpeza WSUS ocorre após cada sincronização e faz os seguintes itens de limpeza:
<!--2839349,3098809, 2977644-->

- A opção de **atualizações expiradas** para servidores WSUS em cas, sites primários e secundários.
- O Gestor de Configuração constrói uma lista de atualizações supersed a partir da sua base de dados. A lista baseia-se no comportamento da supersedência nas propriedades dos componentes do Software Update Point.
  - Os itens de configuração da atualização que satisfaçam os critérios de comportamento da supersedência expiram na consola do Gestor de Configuração.
  - As atualizações são recusadas no WSUS para sites CAS, primários e secundários.
- Uma limpeza para itens de configuração de atualização de software na base de dados do Gestor de Configuração ocorre de sete em sete dias e remove atualizações desnecessárias da consola.
  - Esta limpeza não removerá as atualizações expiradas da consola do Gestor de Configuração se estiverem atualmente implementadas.

> [!NOTE]
> Os "Meses para esperar até que uma atualização supersed seja expirada" baseiam-se na data de criação da atualização de superseding. Por exemplo, se utilizar 2 meses para esta definição, as atualizações que foram substituídos serão recusadas no WSUS e expiradas no Gestor de Configuração quando a atualização de superceding tiver 2 meses.

As seguintes opções de Assistente de Limpeza do **Servidor WSUS** não são executadas nos sites CAS, primários e secundários:

- Atualizações não utilizadas e revisões de atualizações
- Computadores que não contactam o servidor
- Ficheiros de atualização desnecessários

  Para mais informações e instruções, consulte o guia completo para o [Microsoft WSUS e](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) o blog de manutenção SUP do Gestor de Configuração.

## <a name="wsus-cleanup-starting-in-version-1906"></a>Limpeza wSUS a partir da versão 1906
<!--41101009-->

 Tem tarefas adicionais de manutenção wSUS que o Gestor de Configuração pode executar para manter pontos de atualização de software saudáveis. Além de declinar atualizações expiradas no WSUS, o Gestor de Configuração pode adicionar índices não agrupados às bases de dados wSUS e remover atualizações obsoletas das bases de dados wSUS. A manutenção wSUS ocorre após cada sincronização.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Declínio expirado atualizações no WSUS de acordo com as regras de supersedência

As atualizações em declínio no WSUS melhoram o desempenho removendo essas atualizações dos catálogos enviados aos clientes. As atualizações em declínio que o Gestor de Configuração marca como substituído minimiza ainda mais os catálogos e melhora o desempenho.

1. Na consola de Configuração Manager, navegue para**os sites**de**configuração** > do site de**visão geral** > da **administração.** > 
2. Selecione o site no topo da hierarquia do Gestor de Configuração.
3. Clique em **Configurar Componentes do Site** no grupo Definições e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.
4. No separador **de manutenção WSUS,** selecione **As atualizações expiradas do Declínio no WSUS**de acordo com as regras de supersedência .

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Adicione índices não agrupados à base de dados wSUS para melhorar o desempenho da limpeza wSUS

A adição de índices não agrupados melhora o desempenho de limpeza wSUS que o Gestor de Configuração faz.

1. Na consola de Configuração Manager, navegue para**os sites**de**configuração** > do site de**visão geral** > da **administração.** > 
2. Selecione o site no topo da hierarquia do Gestor de Configuração.
3. Clique em **Configurar Componentes do Site** no grupo Definições e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.
4. No separador **de manutenção WSUS,** selecione **Adicionar índices não agrupados à base de dados wSUS**.
5. Em cada SUSDB utilizado pelo Gestor de Configuração, os índices são adicionados às seguintes tabelas:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>SQL permissões para criar índices

Quando a base de dados WSUS estiver num servidor SQL remoto, poderá ser necessário adicionar permissões no SQL para criar índices. A conta usada para se ligar à base de dados wSUS e criar os índices pode variar. Se especificar uma Conta de Ligação ao [Servidor WSUS nas propriedades do ponto de atualização do software,](../get-started/install-a-software-update-point.md#wsus-server-connection-account)certifique-se de que a conta de ligação tem as permissões SQL. Se não especificar uma Conta de Ligação ao Servidor WSUS, então a conta de computador do servidor do site necessita das permissões SQL.

- A criação `ALTER` de um índice requer permissão na mesa ou na vista. A conta deve ser `sysadmin` um membro da `db_ddladmin` `db_owner` função de servidor fixo ou das funções de base de dados fixas. Para obter mais informações sobre a criação e índice e permissões, consulte [CREATE INDEX (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- A `CONNECT SQL` permissão do servidor deve ser concedida à conta. Para mais informações, consulte [grant server Permissions (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

> [!NOTE]  
>  Se a base de dados WSUS estiver num servidor SQL remoto utilizando uma porta não predefinida, os índices podem não ser adicionados. Pode criar um pseudónimo de servidor utilizando o [SQL Server Configuration Manager](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) para este cenário. Uma vez adicionado o pseudónimo e o Gestor de Configuração pode fazer uma ligação à base de dados wSUS, os índices serão adicionados.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Remova atualizações obsoletas da base de dados wSUS

Atualizações obsoletas são atualizações não utilizadas e atualizações na base de dados wSUS. De um modo geral, uma atualização é considerada obsoleta uma vez que já não está no Catálogo de [Atualizações](https://www.catalog.update.microsoft.com/) da Microsoft e não é necessária por outras atualizações como pré-requisito ou dependência.

1. Na consola de Configuração Manager, navegue para**os sites**de**configuração** > do site de**visão geral** > da **administração.** > 
2. Selecione o site no topo da hierarquia do Gestor de Configuração.
3. Clique em **Configurar Componentes do Site** no grupo Definições e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.
4. No separador **de manutenção WSUS,** selecione **Remova atualizações obsoletas da base de dados WSUS**.
   - A remoção obsoleta da atualização será permitida durante um máximo de 30 minutos antes de ser interrompida. Recomeçará depois da próxima sincronização ocorrer.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>SQL permissões para remover atualizações obsoletas

Quando a base de dados WSUS está num servidor SQL remoto, a conta de computador do servidor do site necessita das seguintes permissões SQL:

- As `db_datareader` `db_datawriter` funções de base de dados fixas. Para mais informações, consulte [funções de nível de base de dados](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- A `CONNECT SQL` permissão do servidor deve ser concedida à conta de computador do servidor do site. Para mais informações, consulte [grant server Permissions (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

#### <a name="wsus-cleanup-wizard"></a>Assistente de limpeza WSUS

A partir da versão 1906, as seguintes opções do Assistente de Limpeza do **Servidor WSUS** não são executadas nos sites CAS, primários e secundários:

- Computadores que não contactam o servidor
- Ficheiros de atualização desnecessários

  Para mais informações e instruções, consulte o guia completo para o [Microsoft WSUS e](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) o blog de manutenção SUP do Gestor de Configuração.


### <a name="known-issues-for-version-1906"></a>Questões conhecidas para a versão 1906

Considere o seguinte cenário:
<!--5418148-->
- Está a usar a versão 1906 do Gestor de Configuração
- Tem pontos de atualização de software remoto usando uma base de dados interna do Windows
- Nas propriedades do componente de ponto de **atualização**de software, tem qualquer uma das seguintes opções selecionadas sob o separador **de manutenção WSUS:**
   - Adicione índices não agrupados à base de dados wSUS
   - Remova atualizações obsoletas da base de dados wSUS

Neste cenário, o Gestor de Configuração não consegue executar as tarefas de manutenção do WSUS acima para os pontos de atualização remotas de software utilizando uma base de dados interna do Windows. Este problema ocorre porque a Base de Dados Interna do Windows não permite ligações remotas. Verá os seguintes erros `WSyncMgr.log` no servidor do site:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Para resolver o problema, pode automatizar a manutenção wSUS para os pontos de atualização de software remoto utilizando uma Base de Dados Interna do Windows. Para mais informações e etapas detalhadas, consulte o guia completo para a [manutenção sup do Microsoft WSUS e do Gestor](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)de Configuração .

## <a name="updates-cleanup-log-entries"></a>Atualizações entradas de registo de limpeza

Pode verificar esta limpeza revendo o wsyncmgr.log para as seguintes entradas:

- O declínio das atualizações sobresedidas no WSUS está completo quando vê esta entrada de registo:`Cleanup processed <number> total updates and declined <number>`
- A limpeza wSUS começa quando vir esta entrada:`Calling WSUS Cleanup.`
- A limpeza wSUS para atualizações expiradas está completa quando vir esta entrada:`Successfully completed WSUS Cleanup.`
- O Gestor de Configuração expirou actualizaa a limpeza de itens de configuração está a começar quando vir esta entrada:`Deleting old expired updates...`
- O Gestor de Configuração expirou actualizaa a limpeza de itens de configuração está completa quando vir esta entrada:`Deleted <number> expired updates total`
