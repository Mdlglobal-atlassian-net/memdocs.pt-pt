---
title: Listas de verificação de migração
titleSuffix: Configuration Manager
description: Utilize listas de verificação de administradores para o ajudar a planear uma estratégia de migração para o ramo atual do Gestor de Configuração.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718946"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Listas de verificação de administradores para planeamento de migração em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as seguintes listas de verificação de administradores para o ajudar a planear a sua estratégia de migração para o ramo atual do Gestor de Configuração.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a>Lista de verificação de administrador para planeamento de migração  
 Utilize a seguinte lista de verificação para as etapas de planeamento pré-migração.  

-   **Avalie o ambiente atual:**  

     Identifique as necessidades empresariais existentes que são satisfeitas pela hierarquia de origem e desenvolva planos para continuar a satisfazer essas necessidades na hierarquia de destino.  

-   **Reveja a funcionalidade e as alterações que estão disponíveis com a versão do Gestor de Configuração que utiliza, e utilize estas informações para o ajudar a projetar a sua hierarquia de destino:**  

    Para mais informações, consulte [Fundamentos de Gestor de Configuração](../../core/understand/fundamentals.md) e [Novidades.](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)  


-   **Determinar o modelo de segurança administrativa a utilizar para a administração baseada em funções:**  

    Para mais informações, consulte [Os Fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Avalie a sua rede e topologia de Diretório Ativo:** Reveja a estrutura de domínio existente e a topologia da rede e considere como isso influencia as suas tarefas de design e migração da hierarquia.  

-   **Finalize a estrutura da hierarquia de destino:**  

    Decida o posicionamento de um site de administração central, sites primários, sites secundários e opções de distribuição de conteúdo.  

-   **Mapeie a hierarquia para os computadores que pretende utilizar para sites e servidores do site da hierarquia de destino:**  

    Identifique os computadores que os sites e servidores do sistema de sites irão usar na hierarquia de destino e, em seguida, certifique-se de que eles têm capacidade suficiente para satisfazer os requisitos operacionais existentes e futuros.  

-   **Planeie a estratégia de migração de objetos:**  

    Planeie utilizar os trabalhos de migração disponíveis para migrar diferentes objetos, incluindo limites do site, coleções, anúncios e implantações. Para mais informações, consulte [tipos de empregos migratórios](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) no Planeamento de uma estratégia de [emprego migratório](../../core/migration/planning-a-migration-job-strategy.md)  

    O Gestor de Configuração migra apenas os objetos que seleciona. Quaisquer objetos que não sejam migrados e que sejam necessários na hierarquia de destino devem ser recriados na hierarquia do destino.  

    Os objetos que podem migrar são apresentados quando configurar as tarefas de migração.  

-   **Planeie a estratégia de migração de clientes:**  

    Planeie a migração dos clientes utilizando uma abordagem controlada que limita a largura de banda da rede e os requisitos de processamento do servidor quando migra os clientes para a hierarquia de destino. Para mais informações sobre o planeamento de uma estratégia de migração de clientes, consulte o Planeamento de uma estratégia de [migração de clientes.](../../core/migration/planning-a-client-migration-strategy.md)  

-   **Planeie os dados de inventário e de compatibilidade:**  

    O Gestor de Configuração não suporta o inventário de hardware migratório, o inventário de software ou os dados de conformidade de conformidade de gestão de configuração desejados para atualizações de software ou clientes.  

    Em vez disso, após a migração do cliente para o novo site na hierarquia de destino e após ter recebido a política dessas configurações, o cliente envia as informações para o site atribuído. Esta ação preenche a base de dados do site de destino com os dados atuais de inventário e de compatibilidade.  

-   **Planeie a conclusão da migração a partir da hierarquia de origem:**  

    Decida quando deverão ser migrados os clientes e os objetos. Depois de concluída a migração, pode optar por desativar os servidores do site na hierarquia de origem.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a>Lista de verificação de administrador para a migração da hierarquia  
Utilize a lista de verificação seguinte para planear uma hierarquia de destino antes de iniciar a migração.  

-   **Identifique os computadores a utilizar na hierarquia de destino:**  

    O Gestor de Configuração não suporta uma atualização em vigor da infraestrutura do Gestor de Configuração 2007. Em vez disso, utiliza a migração para mover dados do Diretor de Configuração 2007 para o ramo atual do Gestor de Configuração. Isto requer que utilize uma implementação lado a lado e instale o Gestor de Configuração em novos computadores.  

    Da mesma forma, quando se migra de outra hierarquia do Gestor de Configuração, tem de instalar uma nova hierarquia de destino que seja uma implantação lado a lado para a sua hierarquia de origem.  

-   **Crie a hierarquia de destino:**  

    Para preparar a migração, instale e configure uma hierarquia de destino do Gestor de Configuração que inclua um local primário. Por exemplo:  

    -   Instale um site de administração central e, em seguida, instale pelo menos uma criança primária.  

    -   Instale uma primária autónoma se não pretender utilizar um site de administração central.  

-   **Se pretender migrar informações relacionadas com atualizações de software, configure um ponto de atualização de software na hierarquia de destino e sincronize as atualizações de software:**  

    Tem de configurar e sincronizar atualizações de software na hierarquia de destino para poder migrar informações de atualizações de software a partir da hierarquia de origem.  


-   **Instale e configure funções adicionais do sistema de sites na hierarquia de destino:**  

    Configure funções adicionais do sistema do site e sistemas de site que necessite.  

-   **Verifique a funcionalidade operacional na hierarquia do destino:**  

    Verifique o seguinte:  

    -   Se a hierarquia de destino incluir vários sites, certifique-se de que a replicação da base de dados está a funcionar entre sites. A replicação da base de dados não é aplicável a sites primários autónomos.  

    -   Verifique se todas as funções do sistema de instalação instaladaestão operacional.  

    -   Verifique se os clientes do Gestor de Configuração que instala na hierarquia de destino podem comunicar com sucesso com o seu site atribuído.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a>Lista de verificação de administrador para migração  
Utilize a lista de verificação seguinte para migrar dados da hierarquia de origem para a hierarquia de destino.  

-   **Ative a migração na hierarquia de destino:**  

    Configure uma hierarquia de origem especificando o local de alto nível da hierarquia de origem. Para mais informações sobre a especificação do site de origem, consulte o Planeamento de uma estratégia de [hierarquia de origem.](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   **Quando a hierarquia de origem executa o Configurmanager 2007 SP2, selecione e configure sites adicionais na hierarquia de origem:**  

    Para cada site adicional na hierarquia de origem SP2 2007 do Gestor de Configuração que pretende recolher dados, tem de configurar credenciais para recolha de dados. Quando configura cada site de origem, o processo de recolha de dados começa imediatamente e continua durante todo o período de migração até que pare a recolha de dados para esse site. A recolha de dados garante que pode migrar objetos da hierarquia de origem que são atualizados ou adicionados após um processo anterior de recolha de dados.

    > [!NOTE]  
    >  Quando a hierarquia de origem gere o System Center 2012 Configuration Manager ou mais tarde, não precisa de configurar sites de origem adicionais.  

-   **Configure a partilha do ponto de distribuição:**  

    Pode partilhar pontos de distribuição entre as duas hierarquias para disponibilizar o conteúdo dos objetos migrados para os clientes da hierarquia de destino. Isto garante que o mesmo conteúdo permanece disponível para clientes em ambas as hierarquias e que pode manter este conteúdo até parar de recolher dados e terminar a migração.  

    Para obter informações sobre pontos de distribuição partilhados, consulte pontos de [distribuição de partilha entre as hierarquias](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) de origem e destino no Planeamento de uma estratégia de migração de implementação de [conteúdos.](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   **Crie e execute tarefas de migração para migrar os objetos associados a clientes da hierarquia de origem:**  

    Crie tarefas de migração para migrar objetos entre hierarquias. As configurações necessárias a cada tarefa de migração podem variar consoante os dados migrados pela tarefa.  

    Por exemplo, quando efetua a migração do conteúdo, independentemente da tarefa de migração utilizada, tem de atribuir a gestão desse conteúdo a um site da hierarquia de destino. O site atribuído terá acesso à localização original do ficheiro de origem para obter o conteúdo, sendo responsável pela distribuição desse conteúdo pelos pontos de distribuição da hierarquia de destino.  

    Para obter mais informações, consulte [Criar e editar trabalhos de migração para O Gestor](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) de Configuração em Operações para migrar para o Gerente de [Configuração.](../../core/migration/operations-for-migration.md)  

-   **Migre os clientes para a hierarquia de destino:**  

    O processo de migração dos clientes depende do cenário de migração:  

    -   Quando migra clientes que tenham uma versão cliente que não seja a mesma que a hierarquia de destino, tem de atualizar o software do cliente. A atualização requer a remoção do cliente atual do Gestor de Configuração, seguido da instalação da nova versão cliente que corresponde ao site de destino.  

    -   Quando migrar clientes que possuem uma versão do cliente que corresponde à versão da hierarquia de destino, o cliente não é atualizado nem reinstalado. Em vez disso, é reatribuído a um site primário da hierarquia de destino.  

    Quando migrar um cliente para a hierarquia de destino, este é associado aos respetivos dados migrados anteriormente para esta hierarquia de destino.  

    Para mais informações, consulte O Planeamento de uma estratégia de [migração de clientes.](../../core/migration/planning-a-client-migration-strategy.md)  

-   **Atualize ou reatribua pontos de distribuição partilhados:**  

    Quando já não tiver de apoiar clientes na sua hierarquia de origem, pode atualizar pontos de distribuição partilhados a partir de um site de origem do Gestor de Configuração de 2007 ou reatribuir pontos de distribuição partilhados a partir de um Site de Fonte de Fonte de Gestão de Configuração do System Center 2012. Se atualizar ou reatribuir um ponto de distribuição, a função do sistema de sites é transferida para um site primário da hierarquia de destino e o ponto de distribuição é removido do site de origem da hierarquia de origem. Ao atualizar ou reatribuir um ponto de distribuição partilhado, o conteúdo permanece no computador do ponto de distribuição e não precisa de recolocar o conteúdo em novos pontos de distribuição na hierarquia de destino.  

    Também pode atualizar um ponto de distribuição que está co-localizado num servidor de site secundário do Gestor de Configuração 2007. Esta operação remove o site secundário e conserva apenas um ponto de distribuição na hierarquia de destino.  

    Para obter informações sobre pontos de distribuição partilhados, consulte pontos de [distribuição de partilha entre as hierarquias](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) de origem e destino no Planeamento de uma estratégia de migração de implementação de [conteúdos.](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   **Terminar a migração:**  

    Depois de ter migrado dados e clientes de todos os sites da hierarquia de origem e ter atualizado os pontos de distribuição aplicáveis, pode terminar a migração. Para terminar a migração, pare de recolher dados para cada site de origem na hierarquia de origem. Em seguida, pode remover as informações de migração de que não necessita e encerrar a infraestrutura da hierarquia de origem. Para mais informações, consulte [Planeamento para completar a migração.](../../core/migration/planning-to-complete-migration.md)  
