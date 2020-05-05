---
title: Operações de migração
titleSuffix: Configuration Manager
description: Crie e gere empregos para migrar dados e clientes para a filial atual do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720920"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Operações para migrar para o gerente de configuração atual sucursal

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para a migração em 'Gestor de Configuração', pode migrar dados e clientes depois de recolher com sucesso dados de um site de origem numa hierarquia de origem suportada. Utilize a informação nas seguintes secções para criar e executar postos de trabalho migratórios para migrar dados e clientes e, em seguida, terminar o processo de migração.  

-   [Criar e editar empregos migratórios](#Create_Edit_migration_Jobs)  

-   [Executar empregos migratórios](#Run_Migration_Jobs)  

-   [Atualizar ou reatribuir um ponto de distribuição partilhada](#BKMK_ProcUpgrdSS)  

-   [Monitorizar a atividade migratória no espaço de trabalho migratório](#Monitor_MIgration)  

-   [Clientes migrados](#BKMK_MigrateClients)  

-   [Terminar a migração](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Criar e editar tarefas de migração  
 Utilize os seguintes procedimentos para criar empregos de migração de dados, editar a lista de exclusão para empregos migratórios baseados na recolha, criar pontos de distribuição partilhados e editar horários de trabalho de migração.  

> [!NOTE]  
>  O seguinte procedimento para a criação de um trabalho migratório que migra por coleções aplica-se apenas às hierarquias de origem que executam uma versão suportada do Gestor de Configuração 2007. O tipo de trabalho de migração baseado na recolha não está disponível quando se migra de um System Center 2012 Configuration Manager ou configuração do gestor atual da hierarquia de fonte de filial.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Criar um trabalho de migração para migrar por coleções  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  No separador **Home,** no grupo **Criar,** escolha **Criar Trabalho de Migração**.  

4.  Na página **geral** do assistente create migration job, configura risado o seguinte e, em seguida, escolha **OK:**  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de coleção**.  

5.  Na página **'Recolhas Selecionadas',** configura rume o seguinte e, em seguida, escolha **a seguir:**  

    -   Selecione as coleções que pretende migrar.  

    -   Se quiser migrar apenas coleções e não os objetos associados a essas coleções, desmarque **os objetos migrados que estejam associados às coleções especificadas.** Se desverificar esta opção, não há objetos associados migrados neste trabalho e pode saltar os passos 6 e 7.  

6.  Na página **'Selecionar Objectos',** desmarque quaisquer tipos de objetos ou objetos disponíveis específicos que não pretenda migrar. Por predefinição, são selecionados todos os tipos de objetos associados e objetos disponíveis. Escolha **Seguinte**.  

7.  Na página De Propriedade de **Conteúdo,** atribua a propriedade de conteúdos de cada site de origem listado a um site na hierarquia de destino, e depois escolha **Next**.  

8.  Na página de Âmbito de **Segurança,** selecione um ou mais âmbitos de segurança da administração baseados em papéis para atribuir aos objetos para migrar neste trabalho de migração, e depois escolher **Next**.  

9. Na página **Limiting** collection, criar uma coleção da hierarquia de destino para limitar o âmbito de cada coleção listada, e depois escolher **Next**. Se não houver coleções listadas, escolha **Next**.  

10. Na página de Substituição do Código do **Site,** atribua um código de site da hierarquia de destino para substituir o código de site do Gestor de Configuração de 2007 para cada coleção listada e, em seguida, escolha **Next**. Se não houver coleções listadas, escolha **Next**.  

11. Na página informações de **revisão,** escolha **Guardar para arquivar** para guardar as informações exibidas para posterior visualização. Quando estiver pronto para continuar, escolha **Next**.  

12. Na página **Definições,** configura-se quando o trabalho de migração funcionará, escolha quaisquer configurações adicionais que necessite para este trabalho de migração e, em seguida, escolha **Next**.  

13. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Criar um Trabalho de migração para migrar por objetos  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  No separador **Home,** no grupo **Criar,** escolha **Criar Trabalho de Migração**.  

4.  Na página **geral** do assistente create migration job, crie o seguinte e, em seguida, escolha **seguinte:**  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de objeto**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  Na página De Propriedade de **Conteúdo,** atribua a propriedade de conteúdos de cada site de origem listado a um site na hierarquia de destino, e depois escolha **Next**. Se não estiverem listados sites de origem, escolha **Next**.  

7.  Na página **'Âmbito** de Segurança', selecione um ou mais âmbitos de segurança da administração baseados em funções para atribuir aos objetos neste trabalho de migração e, em seguida, escolha **Next**.  

8.  Na página informações de **revisão,** escolha **Guardar para arquivar** para guardar as informações exibidas para posterior visualização. Quando estiver pronto para continuar, escolha **Next**.  

9. Na página **Definições,** configura-se quando o trabalho de migração funcionará e escolha quaisquer configurações adicionais que necessite para este trabalho de migração. Em seguida, escolha **Next**.  

10. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Criar um trabalho de migração para migrar objetos mudados  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  No separador **Home,** no grupo **Criar,** escolha **Criar Trabalho de Migração**.  

4.  Na página **geral** do assistente create migration job, configura risa do seguinte e, em seguida, escolha **a seguinte:**  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista de abandono do **tipo Job,** selecione **Objetos modificados após a migração**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  Na página De Propriedade de **Conteúdo,** atribua a propriedade de conteúdos de cada site de origem listado a um site na hierarquia de destino, e depois escolha **Next**. Se não estiverem listados sites de origem, escolha **Next**.  

7.  Na página **'Âmbito** de Segurança', selecione um ou mais âmbitos de segurança da administração baseados em funções para atribuir aos objetos neste trabalho de migração e, em seguida, escolha **Next**.  

8.  Na página informações de **revisão,** escolha **Guardar para arquivar** para guardar as informações exibidas para posterior visualização. Quando estiver pronto para continuar, escolha **Next**.  

9. Na página **Definições,** configura-se quando o trabalho de migração funcionare escolha quaisquer configurações adicionais que necessite para este trabalho de migração. Ao contrário dos outros tipos de trabalho de migração, este trabalho de migração deve substituir os objetos anteriormente migrados na base de dados do Gestor de Configuração. Escolha **Seguinte**.  

10. Confirme as definições e, em seguida, termine o assistente.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a>Modificar a lista de exclusão para a migração  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** escolha **migração** para ter acesso à lista de exclusão. Também pode aceder à lista de exclusão a partir dos nós **Hierarquia de Origem** ou **Tarefas de Migração** .  

3.  No separador **Home,** no grupo **Migração,** escolha lista de exclusão de **edição**.  

4.  Na caixa de diálogo Editar Lista de **Exclusão,** selecione o objeto excluído que pretende remover da lista de exclusão e, em seguida, escolha **Remover**.  

5.  Escolha **OK** para guardar as alterações e terminar a edição. Para cancelar as alterações atuais e restaurar todos os objetos que removeu, escolha **Cancelar**, e depois escolher **Nº**. Este procedimento irá cancelar a remoção dos objetos e fechar a caixa de diálogo **Editar Lista de Exclusão** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Pontos de distribuição de ações da hierarquia de origem  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expanda a **Migração,** escolha a **Hierarquia Fonte,** e depois selecione o site de origem que pretende criar.  

3.  No separador **Home,** no grupo **Source Site,** escolha **Configure**.  

4.  Na caixa de diálogo **Source Site Credenciais,** selecione Ativar a partilha de pontos de distribuição para o servidor do **site de origem,** e, em seguida, escolha **OK**.  

5.  Quando a recolha de dados terminar, escolha **Fechar**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Alterar o horário de um trabalho de migração  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  Escolha o trabalho de migração que quer mudar. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

4.  Nas propriedades do trabalho de migração, selecione o separador **Definições,** altere o tempo de execução para o trabalho de migração e, em seguida, escolha **OK**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Executar tarefas de migração  
 Utilize o procedimento seguinte para executar uma tarefa de migração que ainda não foi iniciada.  


1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  Escolha o trabalho de migração que quer gerir. No separador **Home,** no grupo **Trabalho de Migração,** escolha **Iniciar**.  

4.  Escolha **sim** para começar o trabalho de migração.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Atualizar ou reatribuir um ponto de distribuição partilhado  
 Você pode atualizar um ponto de distribuição suportado que é partilhado a partir de um site de origem de Configuração 2007 (ou reatribuir um ponto de distribuição suportado que é partilhado a partir de um site de origem do Gestor de Configuração) para ser um ponto de distribuição na hierarquia de destino.  

> [!IMPORTANT]  
>  Antes de atualizar um ponto de distribuição de sucursais do Gestor de Configuração de 2007, deve desinstalar o software cliente Do Gestor de Configuração 2007 a partir do computador do ponto de distribuição de agências. Se o software cliente do Gestor de Configuração 2007 for instalado quando tentar atualizar o ponto de distribuição, a atualização falha e o conteúdo que foi previamente implementado para o ponto de distribuição do ramo é removido do computador.  

> [!CAUTION]  
>  Quando atualiza ou reatribui um ponto de distribuição partilhado, a função do sistema de site de pontode distribuição e o computador do sistema do site são removidos do site de origem e adicionados como ponto de distribuição para o site na hierarquia de destino que seleciona.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a> Atualizar ou reatribuir um ponto de distribuição partilhado  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a Migração,** e depois escolher a **Hierarquia Fonte.**  

3.  Selecione o site que detém o ponto de distribuição que pretende atualizar, escolha o separador **Pontos** de Distribuição Partilhada e selecione o ponto de distribuição elegível que pretende atualizar ou reatribuir.  

4.  No separador **Ponto de Distribuição,** no grupo Ponto de **Distribuição,** escolha **Reassign**.  

5.  Especifique as definições no assistente do Ponto de Distribuição Partilhada Reassigno como se estivesse a instalar um novo ponto de distribuição para a hierarquia de destino, com a seguinte adição:  

    -   Na página de Conversão de **Conteúdos,** reveja as orientações sobre o espaço necessário para converter o conteúdo existente. Em seguida, na página de **Definições** de Unidade do assistente, certifique-se de que a unidade do computador de ponto de distribuição selecionado tem a quantidade necessária de espaço de disco gratuito.  

6.  Confirme as definições e, em seguida, termine o assistente.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Monitorizar a atividade de migração na área de trabalho Migração  
 Utilize a consola 'Gestor de Configuração' para monitorizar a migração.  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a migração,** e depois escolher **empregos migratórios.**  

3.  Escolha o trabalho de migração que pretende monitorizar.  

4.  Visualize os detalhes e o estado da tarefa de migração selecionada nos separadores **Resumo** e **Objetos na Tarefa**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrar clientes  
 Depois de migrar dados para clientes entre hierarquias, mas antes de terminar a migração, planeie migrar clientes para a hierarquia de destino. A migração de clientes entre hierarquias envolve desinstalar o software cliente do Gestor de Configuração a partir de computadores que são atribuídos à hierarquia de origem e, em seguida, instalar o software cliente do Gestor de Configuração a partir da hierarquia de destino. Quando instala o cliente na hierarquia de destino, também atribui o cliente a um site primário nessa hierarquia. Para saber mais sobre clientes migradores, consulte O Planeamento de uma estratégia de [migração de clientes.](../../core/migration/planning-a-client-migration-strategy.md)  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a>Terminar a migração  
 Utilize este procedimento para terminar a migração da hierarquia de origem.  

1.  Na consola De Configuração, escolha **Administração**.  

2.  No espaço de trabalho da **Administração,** expandir **a Migração,** e depois escolher a **Hierarquia Fonte.**  

3.  Para uma hierarquia de origem de 2007, selecione um site de origem que esteja no nível inferior da hierarquia de origem. Para um System Center 2012 Configuration Manager ou Configuração Manager hierarquia de fonte de filial, selecione o site de origem disponível.  

4.  No separador **Home,** no grupo **Clean Up,** escolha **Parar de recolher dados**.  

5.  Selecione **Sim** para confirmar a ação.  

6.  Para uma hierarquia de origem de 2007, antes de continuar para o passo seguinte, repita os passos 3, 4 e 5. Passe por estes degraus em cada local da hierarquia, desde o fundo da hierarquia até ao topo. Para um System Center 2012 Configuration Manager ou Configuração Manager atual hierarquia de fonte de filial, continue para o passo seguinte.  

7.  No separador **Home,** no grupo **Clean Up,** escolha Dados de **Migração Clean Up**.  

8.  Na caixa de diálogo **Clean Up Migration Data,** da lista de drop-down da **hierarquia Source,** selecione o código do site e servidor do site do site de alto nível da hierarquia de origem e, em seguida, escolha **OK**.  

9. Escolha **Sim** para terminar o processo de migração para a hierarquia de origem.  
