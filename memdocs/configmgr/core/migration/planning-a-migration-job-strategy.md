---
title: Planeamento de empregos migratórios
titleSuffix: Configuration Manager
description: Utilize trabalhos de migração para configurar dados que pretende migrar para o seu ambiente de ramificação atual do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719674"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Planeie uma estratégia de trabalho de migração em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize trabalhos de migração para configurar os dados específicos que pretende migrar para o seu ambiente de ramificação atual do Gestor de Configuração. Os trabalhos de migração identificam os objetos que planeiamigrar, e eles correm no local de alto nível na sua hierarquia de destino. Pode criar um ou mais trabalhos migratórios por site de origem. Isto permite migrar todos os objetos de uma só vez ou subconjuntos limitados de dados com cada trabalho.  

 Pode criar trabalhos de migração depois de o Gestor de Configuração ter recolhido com sucesso dados de um ou mais sites da hierarquia de origem. É possível migrar dados em qualquer sequência a partir dos sites de origem que recolheram dados. Com um site de origem do Gestor de Configuração de 2007, só é possível migrar dados a partir do site onde foi criado um objeto. Com sites de origem que executam o System Center 2012 Configuration Manager ou mais tarde, todos os dados que você pode migrar estão disponíveis no site de alto nível da hierarquia de origem.  

 Antes de migrar clientes entre hierarquias, certifique-se de que os objetos que os clientes utilizam foram migrados e de que esses objetos estão disponíveis na hierarquia de destino. Por exemplo, quando se migra de uma hierarquia de origem SP2 de 2007, poderá ter um anúncio de conteúdo que seja implantado numa coleção personalizada que tenha um cliente. Neste cenário, recomendamos que emigra a coleção, o anúncio e o conteúdo associado antes de migrar o cliente. Estes dados não podem ser associados ao cliente na hierarquia de destino se o conteúdo, recolha e publicidade não forem migrados antes de o cliente migrar. Se um cliente não estiver associado aos dados relacionados com o anúncio e conteúdo de uma execução anterior, pode ser oferecido ao cliente o conteúdo para a instalação na hierarquia de destino, o que talvez seja desnecessário. Quando o cliente migra após a migração dos dados, o cliente é associado a este conteúdo e anúncio e, a menos que o anúncio seja recorrente, não lhe é oferecido novamente este conteúdo para o anúncio migrado.  

 Alguns objetos requerem mais do que a migração de dados da hierarquia de origem para a hierarquia de destino. Por exemplo, para migrar com sucesso atualizações de software para os seus clientes para a sua hierarquia de destino, você deve implementar um ponto de atualização de software ativo, configurar o catálogo de produtos e sincronizar o ponto de atualização de software com o Windows Server Update Services (WSUS) na hierarquia de destino.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a>Tipos de empregos migratórios  
 O Gestor de Configuração suporta os seguintes tipos de trabalhos migratórios. Cada tipo de trabalho é projetado para ajudar a definir os objetos que pode incluir nesse trabalho.  

 **Migração** de recolha (apenas suportada quando migrar do Gestor de Configuração 2007 SP2): Migrar objetos que estejam relacionados com coleções que selecione. Por padrão, a migração da recolha inclui todos os objetos que estão associados aos membros da coleção. Quando utiliza uma tarefa de migração de coleção, pode excluir instâncias de objetos específicas.  

 **Migração de objetos**: Migrar objetos individuais que selecione. Selecione apenas os dados específicos que pretende migrar.  

 **Migração de objetos anteriormente migrados**: Migrar objetos que já emigrou quando foram atualizados na hierarquia de origem depois de terem sido migrados pela última vez.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a>Objetos que pode migrar  
 Nem todos os objetos podem ser migrados através de um tipo específico de tarefa de migração. A lista seguinte identifica o tipo de objetos que é possível migrar com cada tipo de tarefa de migração.  

> [!NOTE]  
>  Os trabalhos de migração de recolha só estão disponíveis quando se migram objetos de uma hierarquia de origem SP2 de 2007.  

 **Tipos de trabalho que pode usar para migrar cada objeto**  

-   **Anúncios** (disponíveis para migrar de sites de origem suportados do Gestor de Configuração 2007)  

    -   Migração de coleção  


-   **Catálogo de Inteligência de Ativos**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Requisitos de hardware do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Lista de software do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Limites**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Linhas de base de configuração**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Itens de configuração**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Janelas de manutenção**  

    -   Migração de coleção  


-   **Imagens de arranque de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de controladores de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Controladores de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Imagens de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de distribuição de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Regras de medição de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implementação de atualização de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Modelos de implementação de atualização de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Implementações de atualizações de software**  

    -   Migração de coleção  


-   **Listas de atualização de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Sequências de tarefas**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de aplicações virtuais**  

    -   Migração de coleção  

    -   Migração de objeto  

    > [!IMPORTANT]  
    >  Embora possa migrar um pacote de aplicação virtual através da migração de objetos, os pacotes não podem ser migrados através do tipo de tarefa de migração **Migração de Objetos Migrados Anteriormente**. Em vez disso, é necessário eliminar o pacote de aplicação virtual migrado no site de destino e, em seguida, criar uma nova tarefa de migração para migrar a aplicação virtual.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Planeamento geral para todos os postos de trabalho migratórios  
 Use o assistente de emprego de migração para criar um trabalho de migração para migrar objetos para a sua hierarquia de destino. O tipo da tarefa de migração criada determina quais os objetos que estão disponíveis para migrar. Pode criar e utilizar vários trabalhos de migração para migrar dados do mesmo site de origem ou de vários locais de origem. A utilização de um tipo de tarefa de migração não bloqueia a utilização de um tipo de tarefa de migração diferente.  

 Após a execução bem-sucedida de uma tarefa de migração, o estado desta é apresentado como **Concluída** e não pode ser executada novamente. No entanto, é possível criar uma nova tarefa de migração para criar qualquer um dos objetos migrados pela tarefa original e a nova tarefa de migração pode igualmente incluir outros objetos. Quando se criam trabalhos de migração adicionais, os objetos que foram previamente migrados mostram o estado de **migração.** Pode selecionar estes objetos para os migrar novamente, mas a menos que o objeto tenha sido atualizado na hierarquia de origem, migrar estes objetos novamente não é necessário. Se o objeto tiver sido atualizado na hierarquia de origem após a migração original, é possível identificá-lo quando utiliza o tipo de tarefa de migração **Objetos modificados após migração**.  

 É possível eliminar uma tarefa de migração antes da sua execução. No entanto, após o fim de um trabalho de migração, permanece visível na consola do Gestor de Configuração e não pode ser eliminada. Cada trabalho de migração que tenha terminado ou ainda não tenha executado permanece visível na consola do Gestor de Configuração até que termine o processo de migração e limpe os dados de migração.  

> [!NOTE]  
>  Depois de ter terminado a migração utilizando a ação **Clean Up Migration Data,** pode reconfigurar a mesma hierarquia que a atual hierarquia de origem para restaurar a visibilidade dos objetos que emigraram anteriormente.  

 Pode visualizar os objetos contidos em qualquer trabalho de migração na consola do Gestor de Configuração, selecionando o trabalho de migração e, em seguida, escolhendo o separador **Objetos em Trabalho.**  

 Utilize as informações das secções seguintes para o ajudar a planear todas as tarefas de migração.  

### <a name="data-selection"></a>Seleção de dados  
 Ao criar uma tarefa de migração de coleção, é necessário selecionar uma ou mais coleções. Depois de selecionar as coleções, o assistente Create Migration Job mostra os objetos que estão associados às coleções. Por padrão, todos os objetos associados às coleções selecionadas são migrados, mas pode desverificar os objetos que não pretende migrar com esse trabalho. Quando desverifica um objeto que tem objetos dependentes, esses objetos dependentes também não são verificados. Todos os objetos não verificados são adicionados a uma lista de exclusão. Os objetos de uma lista de exclusão são removidos da seleção automática para futuras tarefas de migração. Tem de editar manualmente a lista de exclusão para remover os objetos que pretende que sejam selecionados automaticamente para migração em tarefas de migração que criar no futuro.  

### <a name="site-ownership-for-migrated-content"></a>Propriedade do site para conteúdo migrado  
 Ao migrar conteúdo para implementações,necessita de atribuir o objeto do conteúdo a um site da hierarquia de destino. Em seguida, este site torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de nível superior da hierarquia de destino seja o site que efetivamente migra os metadados do conteúdo, será o site atribuído que irá aceder aos ficheiros de origem originais para obter os conteúdos de toda a rede.  

 Para minimizar a largura de banda da rede que é utilizada durante a migração, considere a transferência da propriedade do conteúdo para o site disponível mais próximo. Como a informação sobre o conteúdo é partilhada globalmente no Gestor de Configuração, estará disponível em todos os sites.  

 A informação sobre o conteúdo é partilhada em todos os sites da hierarquia de destino utilizando a replicação da base de dados. No entanto, qualquer conteúdo que atribua a um site primário e, em seguida, implemente para pontos de distribuição em outros sites primários transfere usando replicação baseada em ficheiros. Esta transferência é encaminhada através do site de administração central e, em seguida, para cada site primário adicional. Ao centralizar pacotes que planeia distribuir para vários sites primários antes ou durante a migração quando atribua um site como proprietário de conteúdo, pode reduzir as transferências de dados através de redes de baixa largura de banda.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Âmbitos de segurança da administração baseados em funções para dados migrados  
 Quando migra dados para uma hierarquia de destino, deve atribuir um ou mais âmbitos de segurança da administração baseados em papéis aos objetos cujos dados são migrados. Este procedimento assegura que apenas os utilizadores administrativos apropriados têm acesso a estes dados após a sua migração. Os âmbitos de segurança especificados são definidos pela tarefa de migração e aplicados a cada objeto que é migrado por essa tarefa. Se necessitar de diferentes âmbitos de segurança para ser aplicado em diferentes conjuntos de objetos e quiser atribuir esses âmbitos durante a migração, deve migrar os diferentes conjuntos de objetos utilizando diferentes trabalhos de migração.  

 Antes de configurar um trabalho de migração, reveja como funciona a administração baseada em papéis no Gestor de Configuração. Se necessário, instale um ou mais âmbitos de segurança para os dados que migra para controlar quem terá acesso aos objetos migrados na hierarquia do destino.  

 Para mais informações sobre âmbitos de segurança e administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Rever ações de migração  
 Ao configurar um trabalho de migração, o assistente create migration job mostra uma lista de ações que deve tomar para garantir uma migração bem sucedida e uma lista de ações que o Gestor de Configuração toma durante a migração dos dados selecionados. Reveja atentamente esta informação para verificar o resultado esperado.  

### <a name="schedule-migration-jobs"></a>Agendar empregos de migração  
 Por predefinição, uma tarefa de migração é executada imediatamente após a sua criação. No entanto, pode especificar quando o trabalho de migração funciona quando se cria o trabalho ou editando as propriedades do trabalho. Pode agendar o trabalho de migração da seguinte forma:  

-   Executar a tarefa agora  

-   Executar a tarefa a uma hora de início específica  

-   Não executar a tarefa  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Especificar a resolução de conflitos para dados migrados  
 Por padrão, os trabalhos de migração não sobrepostam dados na base de dados de destino, a menos que configure o trabalho de migração para ignorar ou substituir dados que foram previamente migrados para a base de dados de destino.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a>Plano para recolha de empregos migratórios  
 Os trabalhos de recolha de migração só estão disponíveis quando se migram dados de uma hierarquia de origem que executa uma versão apoiada do Gestor de Configuração 2007. Tem de especificar uma ou mais coleções para migrar quando migra por coleção. Para cada coleção especificada, a tarefa de migração seleciona automaticamente todos os objetos relacionados para migração. Por exemplo, se selecionar uma coleção específica de utilizadores, são em seguida identificados os membros da coleção e pode migrar as implementações associadas a esta coleção. Opcionalmente, pode selecionar outros objetos de implementação para migrar que estão associados a estes membros. Todos estes itens selecionados são adicionados à lista de objetos que podem ser migrados.  

 Quando migra uma coleção, o Gestor de Configuração também migra as definições de recolha, incluindo janelas de manutenção e variáveis de recolha, mas não pode migrar as definições de recolha para o fornecimento de clientes AMT.  

 Utilize a informação nas seguintes secções para saber sobre configurações adicionais que podem aplicar-se a trabalhos migratórios baseados na recolha.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Excluir objetos de trabalhos de recolha de migração  
 Pode excluir objetos específicos de uma tarefa de migração de coleções. Quando se exclui um objeto específico de um trabalho de migração de recolha, esse objeto é adicionado a uma lista de exclusão global que tem todos os objetos que excluiu dos empregos migratórios criados para qualquer local de origem na atual hierarquia de origem. Os objetos na lista de exclusão ainda estão disponíveis para migração em empregos futuros, mas não são automaticamente incluídos quando se cria um novo trabalho de migração baseado na recolha.  

 Pode editar a lista de exclusão para remover objetos que excluiu anteriormente. Após a remoção de um objeto da lista de exclusão, este é selecionado automaticamente quando uma coleção associada é especificada durante a criação de uma nova tarefa de migração.  

### <a name="unsupported-collections"></a>Coleções não suportadas  
 O Gestor de Configuração pode migrar qualquer uma das coleções padrão de utilizadores, coleções de dispositivos e a maioria das coleções personalizadas de uma hierarquia de fonte do Gestor de Configuração de 2007. No entanto, o Gestor de Configuração não pode migrar coleções que contenham utilizadores e dispositivos na mesma coleção.  

 Não é possível migrar as seguintes coleções:  

-   Uma coleção que tem utilizadores e dispositivos.  

-   Uma coleção que tem uma referência a uma coleção de um tipo de recurso diferente. Por exemplo, uma coleção baseada em dispositivos que tenha uma sub-coleção ou uma ligação a uma coleção baseada no utilizador. Neste exemplo, apenas a coleção de alto nível migra.  

-   Uma coleção que tem uma regra para incluir computadores desconhecidos. A coleção migra, mas a regra para incluir computadores desconhecidos não migra.  

### <a name="empty-collections"></a>Coleções vazias  
 Uma coleção vazia é uma coleção se recursos associados. Quando o Gestor de Configuração migra uma coleção vazia, converte a coleção para uma pasta organizacional que não tem utilizadores ou dispositivos. Esta pasta é criada com o nome da coleção vazia sob o nó de **Recolhas** de Utilizadores ou Recolhas de **Dispositivos** no espaço de trabalho **De Ativos e Compliance** na consola 'Gestor de Configuração'.  

### <a name="linked-collections-and-subcollections"></a>Coleções ligadas e subcoleções  
 Quando migra coleções que estejam ligadas a outras coleções ou que tenham subcoleções, o Gestor de Configuração cria uma pasta sob o nó de **Coleções** de Utilizadores ou Recolhas de **Dispositivos,** para além das coleções e subcoleções ligadas.  

### <a name="collection-dependencies-and-include-objects"></a>Dependências de coleções e inclusão de objetos  
 Quando especifica uma coleção para migrar no assistente create migration job, quaisquer coleções dependentes são automaticamente selecionadas para serem incluídas no trabalho. Este comportamento garante que todos os recursos necessários estão disponíveis após a migração.  

 Por exemplo: Seleciona uma coleção para dispositivos que executam o Windows 10 e tem o nome **de Win_10**. Esta coleção está limitada a uma coleção que tem todos os seus sistemas operativos do seu cliente e tem o nome **de All_Clients**. A recolha **All_Clients** será automaticamente selecionada para migração.  

### <a name="collection-limiting"></a>Limitação de coleções  
 Com o ramo atual do Gestor de Configuração, as coleções são dados globais e são avaliadas em cada site da hierarquia. Por conseguinte, planeie a forma de limitar o âmbito de uma coleção após a respetiva migração. Durante a migração, pode identificar uma coleção da hierarquia de destino a utilizar para limitar o âmbito da coleção que está a migrar de modo a que a coleção migrada não contenha membros inesperados.  

 Por exemplo, no Gestor de Configuração de 2007, as coleções são avaliadas no site que as cria e em sites infantis. Um anúncio pode ser implementado apenas num site subordinado, o que pode limitar o âmbito desse anúncio a esse site subordinado. Em comparação, com o gerente de configuração atual, as coleções são avaliadas em cada site e os anúncios associados são então avaliados para cada site. A limitação da coleção permite-lhe refinar os membros da coleção com base noutra coleção para evitar a adição de membros inesperados da coleção.  

### <a name="site-code-replacement"></a>Substituição do código do site  
 Quando se migra uma coleção que tenha critérios que identifiquem um site de Configuração 2007, deve especificar um site específico na hierarquia do destino. Isto garante que a coleção migrada permaneça funcional na sua hierarquia de destino e não aumente o âmbito.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Especificar o comportamento de anúncios migrados  
 Por padrão, os empregos de migração baseados na recolha desativam os anúncios que migram para a hierarquia do destino. Isto inclui todos os programas que estão associados ao anúncio. Ao criar um trabalho de migração baseado em recolha que tenha anúncios, você vê os **programas Enable para implementação em 'Gestor de Configuração' depois** de um anúncio ser opção migrada na página de **Definições** do assistente create migration job. Se selecionar esta opção, os programas associados aos anúncios são ativados após terem sido migrados. Como uma boa prática, não selecione esta opção. Em vez disso, ative os programas depois de migrarem quando puder verificar os clientes que os receberão.  

> [!NOTE]  
>  Você vê os **programas Enable para implementação em Configuração Manager depois de um anúncio é opção migrada** apenas quando você está criando um trabalho de migração baseado em coleção e o trabalho de migração contém anúncios.  

 Para ativar um programa após a migração, limpe **este programa em computadores onde é anunciado** no separador **Avançado** das propriedades do programa.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a>Plano para empregos de migração de objetos  
 Ao contrário da migração de coleções, deve selecionar cada objeto e instância do objeto que pretende migrar. Pode selecionar os objetos individuais (como anúncios de uma hierarquia do Gestor de Configuração de 2007 ou uma publicação de um System Center 2012 Configuration Manager ou hierarquia de ramificação do Gestor de Configuração) para adicionar à lista de objetos para migrar para um trabalho específico de migração. Todos os objetos que não forem adicionados à lista de migração não serão migrados para o site de destino pela tarefa de migração de objetos.  

 Os postos de trabalho em migração baseados em objetos não dispõem de configurações adicionais para planear para além dos aplicáveis a todos os postos de trabalho migratórios.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a>Plano para empregos de migração de objetos anteriormente migrados  
 Quando um objeto já migrado para a hierarquia de destino é atualizado na hierarquia de origem, pode migrá-lo novamente utilizando o tipo de tarefa **Objetos modificados após migração**. Por exemplo, quando rebatiza ou atualiza os ficheiros de origem para um pacote na hierarquia de origem, a versão do pacote aumenta na hierarquia de origem. Após a incrementação da versão do pacote, este pode ser identificado para migração por este tipo de tarefa.  

 Este tipo de tarefa é semelhante ao tipo de migração de objeto, com a exceção de que, quando seleciona objetos para migrar, apenas os objetos atualizados após a migração por uma tarefa de migração anterior poderão ser selecionados.   

 Ao selecionar este tipo de trabalho, o comportamento de resolução de conflitos na página **Definições** do assistente create migration job está configurado para substituir objetos anteriormente migrados. Esta definição não pode ser alterada.  

> [!NOTE]  
>  Esta tarefa de migração pode identificar objetos que são atualizados automaticamente pela hierarquia de origem e objetos atualizados por um utilizador administrativo.  
