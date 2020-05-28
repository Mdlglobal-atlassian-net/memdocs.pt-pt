---
title: Implementar aplicações virtuais App-V
titleSuffix: Configuration Manager
description: Veja quais as considerações que deve ter em conta quando cria e implementa aplicações virtuais.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df6f550b21523e365055f6a4cdafadca7603c4bf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906374"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Implementar aplicações virtuais App-V com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando utiliza o Gestor de Configuração para gerir aplicações virtuais, ganha os seguintes benefícios:  

-   Uma única infraestrutura de gestão  

-   Funcionalidades de escalabilidade, implementação e distribuição de conteúdos, como coleções e afinidade de dispositivos de utilizador  

-   Funcionalidades avançadas de gestão de aplicações  

-   Implementação do sistema operativo, inventário de software e hardware, medição de software e inteligência de ativos para apoiar aplicações virtuais  

Para obter mais informações sobre como criar e sequenciar aplicações com a Virtualização de Aplicações microsoft (App-V), consulte a documentação de [Virtualização da Aplicação 4](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v4/).  

Para além dos outros requisitos e procedimentos do Gestor de Configuração para a criação de uma aplicação, deve ter em conta as seguintes considerações quando cria e implementa aplicações virtuais:

-   Para implementar aplicações virtuais em computadores, tem de ter o cliente do Gestor de Configuração e o Cliente App-V instalados nos seus computadores. Os dispositivos cliente podem incluir computadores de secretária e portáteis e clientes VDI (Infraestrutura de Ambiente de Trabalho Virtual). O Gestor de Configuração e o software do Cliente App-V trabalham em conjunto para entregar, localizar e lançar pacotes de aplicações virtuais. O cliente do Gestor de Configuração gere a entrega de pacotes de aplicações virtuais ao Cliente App-V. O Cliente de App-V executa a aplicação virtual no cliente.  

-   Para implementar uma aplicação virtual, terá de criar primeiro a aplicação virtual utilizando o Sequenciador do Application Virtualization (App-V). O sequenciador monitoriza o processo de instalação e configuração para uma aplicação e regista a informação que é necessária para que a aplicação seja executada num ambiente virtual. Também pode utilizar o sequenciador para definir quais ficheiros e configurações se aplicam a todos os utilizadores e quais as configurações que os utilizadores podem personalizar.  

-   Quando sequenciar uma aplicação, deve guardar o pacote para um local a que o Gestor de Configuração pode aceder. Em seguida, pode criar uma implementação da aplicação que contém esta aplicação virtual.  

-   O Gestor de Configuração não suporta a utilização da funcionalidade de cache partilhada apenas de leitura do App-V 4.6.  

-   O Gestor de Configuração suporta a funcionalidade Da Loja de Conteúdos Partilhados no App-V 5.  

-   Quando cria um tipo de implementação para uma aplicação virtual, o Gestor de Configuração cria o tipo de implementação utilizando o conteúdo do ficheiro manifesto da aplicação. Este é um ficheiro XML que tem informações sobre a aplicação virtual. Adicionalmente, o Gestor de Configuração cria requisitos para o tipo de implementação com base no conteúdo do ficheiro App-V .osd que possui informações sobre os sistemas operativos suportados para a aplicação virtual.  

-   Para implementar aplicações virtuais no Gestor de Configuração, os computadores clientes devem ter, no mínimo, o App-V 4.6 SP1 ou uma versão posterior do cliente instalado.  

-   Antes de poder implementar com sucesso aplicações virtuais, atualize o cliente App-V com o mais recente hotfix. Para mais informações, consulte a [lista atual das versões de ficheiros App-V 4.5 e App-V 4.6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).

-   Quando utiliza grupos de ligação no App-V 5.0, as suas aplicações virtuais implementadas podem partilhar o mesmo sistema de ficheiros e o registo em computadores clientes. Contrariamente às aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Além disso, os grupos de ligação preservam as definições do utilizador para as aplicações que contêm. Ambientes virtuais App-V em Configuração Manager são usados para configurar grupos de ligação em computadores clientes. Os ambientes virtuais são criados ou alterados em computadores cliente quando a aplicação é instalada ou quando os clientes avaliam as aplicações instaladas. Pode atribuir prioridades a estas aplicações para que, quando várias aplicações tentam alterar o valor de um sistema ou registo de ficheiros, tenha precedência a aplicação com a prioridade mais alta. Para mais informações, consulte [Create App-V ambientes virtuais](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a> Versões do App-V suportadas  
 O Gestor de Configuração suporta as seguintes versões do App-V:  

-   **App-V 4.6**: Para utilizar aplicações virtuais no Gestor de Configuração, os computadores clientes devem ter instalado o Cliente App-V 4.6 SP1, App-V 4.6 SP2 ou App-V 4.6 SP3.  

     Antes de poder implementar com sucesso aplicações virtuais, atualize o cliente App-V 4.6 com o mais recente hotfix. Para mais informações, consulte a [lista atual das versões de ficheiros App-V 4.5 e App-V 4.6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3 e App-V 5.1**: Para app-V 5.0 SP2, deve instalar o [Hotfix Package 5](https://support.microsoft.com/help/2963211) ou utilizar o App-V 5.0 SP3.  
-   **App-V 5.2**: Isto é incorporado no Windows 10 Education (1607 e mais tarde), Windows 10 Enterprise (1607 e mais tarde) e Windows Server 2016.

Para mais informações sobre o App-V no Windows 10, consulte os seguintes tópicos:

- [O que há de novo no App-V](https://docs.microsoft.com/windows/application-management/app-v/appv-about-appv)
- [Começar com app-V para windows 10](https://docs.microsoft.com/windows/application-management/app-v/appv-getting-started)
- [Upgrade para App-V para Windows 10 a partir de uma instalação existente](https://docs.microsoft.com/windows/application-management/app-v/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Passos para gerir aplicações virtuais App-V  
 Para gerir aplicações virtuais App-V, siga estes passos:  

1.   **Sequência**: Sequenciação é o processo de conversão de uma aplicação numa aplicação virtual utilizando o sequenciador App-V.

2.   **Criar**: Utilize o Assistente do Tipo de Implementação criar para importar a aplicação sequenciada para um tipo de implementação do Gestor de Configuração que possa adicionar a uma aplicação. Também pode criar ambientes virtuais que permitam a partilha de definições por várias aplicações virtuais.

3.   **Distribute :** Distribuição é o processo de disponibilização de aplicações App-V nos pontos de distribuição do Gestor de Configuração.

4.   **Implementação**: A implementação é o processo de disponibilização da aplicação nos computadores dos clientes. Isto chama-se publicação e streaming numa infraestrutura completa da App-V.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Métodos de entrega de aplicações virtuais do Configuration Manager  
O Gestor de Configuração suporta dois métodos para a entrega de aplicações virtuais aos clientes: entrega em streaming e entrega local (download e execução).

Quando estiver a decidir qual o método de entrega a utilizar, compare o requisito de espaço reduzido para a entrega em streaming com a disponibilidade garantida de aplicações App-V na entrega local. O maior espaço em disco necessário no cliente para a entrega local poderá ser preferível para a transmissão em fluxo da entrega, para que os utilizadores tenham sempre a aplicação disponível a partir de qualquer localização.  

###  <a name="streaming-delivery"></a>Fornecimento por transmissão em fluxo
Quando utiliza o Gestor de Configuração para gerir o Cliente App-V, suporta o streaming de aplicações virtuais através de HTTP ou HTTPS a partir de um ponto de distribuição. O streaming através de HTTP ou HTTPS está ativado por padrão e está configurado na caixa de diálogo para propriedades de pontos de distribuição. Quando implementa uma aplicação virtual para computadores clientes e um utilizador executa a aplicação virtual, o cliente do Gestor de Configuração contacta um ponto de gestão para determinar qual o ponto de distribuição a utilizar. Em seguida, a aplicação é transmitida a partir do ponto de distribuição.  

Utilize as informações nesta tabela para ajudá-lo a decidir se a entrega em streaming é o melhor método de entrega para si:

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|Este método utiliza protocolos de rede padrão para a transmissão em fluxo de conteúdo de pacotes a partir de pontos de distribuição.<br /><br /> Os atalhos de programa para aplicações virtuais invocam uma ligação ao ponto de distribuição para que o fornecimento da aplicação virtual seja a pedido.<br /><br /> Este método funciona bem para clientes com ligações de banda larga aos pontos de distribuição.<br /><br /> As aplicações virtuais atualizadas distribuídas por toda a empresa são disponibilizadas quando os clientes recebem a política que os informa de que a versão atual foi substituída e os clientes transferem apenas as alterações relativamente à versão anterior.<br /><br /> As permissões de acesso são definidas no ponto de distribuição para impedir que os utilizadores acedam a aplicações ou pacotes não autorizados.|As aplicações virtuais não são transmitidas em fluxo até que o utilizador execute a aplicação pela primeira vez. Neste cenário, um utilizador pode receber atalhos de programa para aplicações virtuais e, em seguida, desligar da rede antes de executar as aplicações virtuais pela primeira vez. Se o utilizador tentar executar a aplicação virtual enquanto o cliente estiver offline, o utilizador vê um erro e não pode executar a aplicação virtualizada porque um ponto de distribuição do Gestor de Configuração não está disponível para transmitir a aplicação. A aplicação não estará disponível até o utilizador voltar a ligar à rede e executar a aplicação.<br /><br /> Para evitar isto, pode utilizar o método de entrega local para entregar aplicações virtuais a clientes ou pode ativar a gestão de clientes baseada na Internet para a entrega por transmissão em fluxo.|  

###  <a name="local-delivery-download-and-execute"></a>Fornecimento local (transferir e executar)  
O download e execução é a abordagem mais comum quando se utiliza o Gestor de Configuração porque esta abordagem imita de perto como outros formatos de aplicação são entregues com o Gestor de Configuração. Quando utiliza o método de entrega local, o cliente do Gestor de Configuração transfere primeiro todo o pacote de aplicações virtuais para a cache do cliente do Gestor de Configuração. O Gestor de Configuração instrui então o Cliente App-V a transmitir a aplicação a partir da cache do Gestor de Configuração para a cache App-V. Se implementar uma aplicação virtual para computadores clientes e o seu conteúdo não estiver na cache App-V, o Cliente App-V transmite o conteúdo da aplicação a partir da cache do cliente do Gestor de Configuração para a cache App-V e, em seguida, executa a aplicação. Depois de a aplicação ser executado com sucesso, pode definir o cliente Do Gestor de Configuração para eliminar quaisquer versões mais antigas do pacote no próximo ciclo de eliminação, ou para perstiná-las na cache do cliente do Gestor de Configuração. O conteúdo persistente localmente pode tirar partido de métodos de otimização de entrega de conteúdo de pacote, tais como BranchCache e PeerCache.

Utilize as informações nesta tabela para ajudá-lo a decidir se a entrega local é o melhor método de entrega para si:   

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|A funcionalidade de ponto de distribuição padrão é utilizada para transferir o pacote utilizando o Serviço de Transferência Inteligente em Segundo Plano (BITS).<br /><br /> Os conteúdos do pacote de aplicações virtuais são entregues localmente ao cliente. Isto significa que os utilizadores podem executá-los quando o seu computador não está ligado à rede.<br /><br /> Este método é adequado para ligações de rede lentas ou pouco fiáveis e para computadores que ligam à rede ocasionalmente.<br /><br /> O Gestor de Configuração utiliza a Compressão Diferencial Remota (RDC) para enviar aos clientes apenas os bytes dentro dos ficheiros que mudaram quando o conteúdo do pacote de aplicações virtual é atualizado. O cliente do Gestor de Configuração utiliza o RDC para construir uma nova versão de um pacote de aplicações virtuais com base na versão atual do pacote e quaisquer alterações enviadas ao cliente.<br /><br /> Este método proporciona aplicações resilientes a utilizadores móveis ou utilizadores desligados. Os administradores podem optar por persistir o pacote na cache do Gestor de Configuração após a entrega se a aplicação virtual foi implementada com uma ação de instalação. O pacote no cache do cliente do Gestor de Configuração serve como uma fonte de streaming local e fiável para o Cliente App-V puxar o pacote para a sua cache.|O espaço do disco que equivale a até o dobro do tamanho do pacote de aplicação virtual é exigido no cliente quando a aplicação virtual é persistida na cache do Gestor de Configuração.|  

###  <a name="deployment-from-an-image"></a>Implantação a partir de uma imagem

Também é possível pré-instalar aplicações virtuais num computador e, em seguida, criar uma imagem desse computador para implementação noutros. Mas se o pacote de aplicações virtuais foi criado num site diferente, a replicação delta binária não será usada para descarregar atualizações para a aplicação. Esta opção pode ser útil numa infraestrutura de ambiente de trabalho virtual, quando pretender que as aplicações estejam disponíveis imediatamente em vez de as transferir após o utilizador iniciar sessão.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a> Migrar de uma infraestrutura de App-V para uma infraestrutura do Configuration Manager e de App-V  
Utilize a tabela seguinte para o ajudar a planear uma migração de uma infraestrutura App-V existente para a gestão de aplicações virtuais com o Gestor de Configuração.  

|Passo|Mais informações|  
|----------|----------------------|  
|Examine as suas aplicações virtuais atuais para escolher as aplicações que pretende migrar para a sua infraestrutura de Gestor de Configuração.|Não existem informações adicionais.|  
|Avaliar os utilizadores e os dispositivos em que as aplicações virtuais serão implementadas.|Crie coleções do Gestor de Configuração para agrupar os utilizadores e dispositivos para os quais pretende implementar as aplicações virtuais. Ver [Introdução às coleções.](../../core/clients/manage/collections/introduction-to-collections.md)|  
|Migrar grupos de ligação App-V 5 para ambientes virtuais do Gestor de Configuração.|Consulte os grupos de [ligação App-V 5 migratórios para a](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) secção de ambientes virtuais do Gestor de Configuração neste tópico.|  
|Investigue para saber se alguma das suas aplicações virtuais existem como aplicações completas na sua infraestrutura de Gestor de Configuração.|Para facilitar a gestão, pode adicionar a aplicação virtual como um novo tipo de implementação à aplicação completa existente. Ver [Criar aplicações](../../apps/deploy-use/create-applications.md).|  
|Criar aplicações para substituir os pacotes de App-V existentes.|Ver [Introdução à gestão de aplicações](../understand/introduction-to-application-management.md) e [criar aplicações.](../../apps/deploy-use/create-applications.md)|  
|O Gestor de Configuração começa a gerir aplicações virtuais num cliente após a primeira implementação de uma aplicação virtual. Depois disso, o Gestor de Configuração deve gerir todas as aplicações App-V no computador.|Não existem informações adicionais.|  
|Distribuir o conteúdo pelos pontos de distribuição adequados para ativar o fornecimento local de aplicações.|Ver Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)|  
|Implemente a aplicação para clientes do Gestor de Configuração.<br /><br /> Se a aplicação App-V foi criada com uma versão anterior do sequenciador que não cria um ficheiro XML manifesto, pode abri-la e guardá-la numa versão mais recente do sequenciador para criar o ficheiro. Este ficheiro é necessário para implementar aplicações virtuais com o Gestor de Configuração.<br /><br /> App-V suporta os pacotes de aplicações virtuais que são criados com as versões SoftGrid 4.1 SP1 ou 4.2 do sequenciador.<br /><br /> Se as aplicações já tiverem sido instaladas localmente, terá de desinstalá-las antes de implementar uma versão virtual da aplicação.|Ver [Aplicações de implantação](../../apps/deploy-use/deploy-applications.md).|  
|O Gestor de Configuração já não suporta a utilização de pacotes e programas que contenham aplicações virtuais. Quando migra do Gerente de Configuração 2007 para o Gerente de Configuração, o Gestor de Configuração converte estes pacotes em aplicações.<br /><br /> Os anúncios do Gestor de Configuração 2007 são convertidos nos seguintes tipos de implementação:<br /><br /> - Pacotes App-V migratórios sem publicidade: Um tipo de implementação que utiliza as definições do tipo de implementação predefinida.<br /><br /> - Pacotes App-V migratórios com um anúncio: Um tipo de implementação que utiliza as mesmas definições que o <br />                Anúncio de Gerente de Configuração 2007.<br /><br /> - Pacotes App-V migratórios com vários anúncios: Um tipo de implementação, para cada <br />                Anúncio de Configuração Manager 2007, que utiliza as definições para esse anúncio.|Consulte [o Planeamento para a migração de objetos para o ramo atual do Gestor de Configuração](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrating App-V 5 connection groups to Configuration Manager virtual environments  
Os ambientes virtuais app-V no Gestor de Configuração permitem aplicações virtuais que implementou para partilhar o mesmo sistema de ficheiros e registo em computadores clientes. Isto significa que, contrariamente às aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Os ambientes virtuais são criados ou alterados em computadores cliente quando a aplicação é instalada ou quando os clientes avaliam as aplicações instaladas. Ambientes virtuais são semelhantes a grupos de conexão em App-V 5 autónomo.  

Ao migrar grupos de ligação de ambientes virtuais de App-V 5 autónomos para ambientes virtuais do Gestor de Configuração, deve garantir que o Gestor de Configuração gere corretamente os grupos de ligação que já existem nos computadores dos clientes e que o ambiente do utilizador dentro desses grupos de ligação é preservado.  

Para converter grupos de ligação App-V 5 para ambientes virtuais do Gestor de Configuração:  

1.  Crie aplicações de Gestor de Configuração para todas as aplicações que existiram no App-V.  

2.  Implemente as aplicações para utilizadores e dispositivos com um objetivo de implementação de **Necessário**. As implementações para os utilizadores devem ser implementadas para os mesmos utilizadores que utilizaram a aplicação na App-V. As implementações para computadores devem ser implantadas para os mesmos computadores que tinham a aplicação na App-V.  

3.  Após a implementação, crie ambientes virtuais que correspondam aos grupos de ligação que são publicados em App-V autónomo. O ambiente virtual deve ter os mesmos pacotes (especificamente, tipos de implementação App-V 5) na mesma ordem.  

Para obter informações sobre como criar um ambiente virtual App-V, consulte [como criar ambientes virtuais App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Em alternativa, pode eliminar todos os grupos de ligação do Cliente App-V antes de começar a implementar aplicações com o Gestor de Configuração. No eão as definições que os utilizadores possam ter guardado em grupos de ligação App-V.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a> Dynamic Suite Composition no App-V 4.6  
Dynamic Suite Composition é uma funcionalidade que permite definir um pacote de aplicação virtual como tendo uma dependência de outro pacote de aplicações virtuais. Quando a aplicação é executada, o Cliente de App-V aloja o pacote primário e o pacote dependente no mesmo ambiente virtual para a aplicação.  

Para que utilize esta funcionalidade com o Gestor de Configuração, ambos os pacotes devem ser implementados e registados no Cliente App-V. Para garantir que o conteúdo do pacote dependente é hospedado localmente no computador cliente, configure a implementação da aplicação para entrega local (descarregamento e execução).  

Para mais informações sobre o Dynamic Suite Composition no App-V, consulte a documentação do App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a> Converter aplicações App-V 4.6 em aplicações App-V 5  
O formato do pacote de aplicações foi alterado entre App-V 4.6 e App-V 5. As aplicações sequenciadas ao utilizar o App-V 4.6 já não são suportadas. Mas o App-V 5 tem uma ferramenta de conversor de pacotes que pode utilizar para converter aplicações. Para mais informações, consulte [Como converter um pacote criado numa versão anterior do App-V](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/how-to-convert-a-package-created-in-a-previous-version-of-app-v).  

Utilize os seguintes passos para converter aplicações App-V 4.6 em aplicações App-V 5:  

1.  Converter ou reseqüência dos pacotes App-V 4.6 no formato App-V 5.  

2.  Implemente o Cliente de App-V 5 em computadores da hierarquia.  

3.  Crie novas aplicações que contêm tipos de implementação para as aplicações App-V 5 e crie regras de substituição para substituir as aplicações 4.6 App-V.  

4.  Crie ambientes virtuais conforme necessário.  

5.  Implemente as novas aplicações App-V 5 nos computadores.  

##  <a name="user-and-deployment-configuration-files"></a> Ficheiros de configuração de utilizadores e de implementação  
Os ficheiros de configuração do utilizador e da implementação têm definições que controlam o funcionamento de uma aplicação. Pode utilizar estes ficheiros para alterar as definições de aplicação sem resequenciar a aplicação.  

Uma aplicação App-V 5 normal pode conter os seguintes ficheiros:  

-   Um pacote de aplicação (.appv) ficheiro  

-   Um ficheiro de configuração do utilizador  

-   Um ficheiro de configuração de implementação  

O ficheiro de configuração do utilizador tem definições que se aplicam apenas ao utilizador ligado. Pode, por exemplo, editar os ficheiros de configuração para alterar as informações sobre o atalho da aplicação que serão implementadas aos utilizadores. Também pode criar uma aplicação De Configuração Manager com vários tipos de implementação. Cada tipo de implementação pode conter um ficheiro de configuração do utilizador diferente e regras de requisitos de utilização para garantir que estes estão instalados para os utilizadores relevantes.  

O ficheiro de configuração de implementação tem definições que se aplicam ao computador, como as definições de registo. O ficheiro também pode ter definições de utilizador, que são aplicadas a todos os utilizadores.  

Se pretender implementar aplicações virtuais App-V 5 com 'Gestor de Configuração', os três ficheiros devem estar presentes na mesma pasta quando criar o tipo de implementação App-V 5. Se houver vários ficheiros na pasta, o 'Gestor de Configuração' utilizará o mais recente.  

Para mais informações, consulte a sua [configuração dinâmica Sobre app-V 5.0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/about-app-v-50-dynamic-configuration).  

##  <a name="app-v-local-interaction"></a>Interação local de App-V  
Em alguns cenários de implementação de aplicações, as aplicações são instaladas localmente em computadores clientes, e outras aplicações são implementadas como aplicações virtuais para o mesmo computador cliente. Por predefinição, as aplicações que foram instaladas localmente não conseguem ver nem comunicar diretamente com aplicações virtualizadas. Este é o comportamento pretendido do isolamento da aplicação que o App-V proporciona. A interação local é uma funcionalidade do Cliente App-V que pode permitir que cada aplicação permita que aplicações instaladas localmente que funcionam num computador cliente para ver e comunicar com aplicações virtualizadas. O Gestor de Configuração e o App-V suportam totalmente a interação local.  

Para obter mais informações sobre a funcionalidade de interação local App-V, consulte a documentação do App-V.  

##  <a name="app-v-5-shared-content-store"></a> Arquivo de Conteúdo Partilhado do App-V 5  
O Gestor de Configuração suporta a funcionalidade App-V 5 Shared Content Store. Para mais informações, consulte [Planear a Loja de Conteúdo Partilhado (SCS) do App-V 5.0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/planning-for-the-app-v-50-sequencer-and-client-deployment#planning-for-the-app-v-50-shared-content-store-scs).  

##  <a name="monitoring-virtual-applications"></a>Monitorizar aplicações virtuais  

### <a name="virtual-application-reports"></a>Relatórios de aplicações virtuais  
Pode utilizar os seguintes relatórios para monitorizar o App-V no ambiente do Gestor de Configuração:  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|Resultados do Ambiente Virtual de App-V|Mostra informações sobre um ambiente virtual selecionado que se encontra em estado especificado para uma coleção selecionada (apenas App-V 5).|  
|Resultados do Ambiente Virtual de App-V Para Ativo|Mostra informações sobre um ambiente virtual selecionado para um ativo especificado e quaisquer tipos de implementação para o ambiente virtual selecionado (apenas App-V 5).|  
|Estado do Ambiente Virtual de App-V|Mostra informações de conformidade para um ambiente virtual selecionado para uma coleção selecionada. A coluna **Retida** neste relatório mostra os ativos em que um ambiente virtual que foi previamente criado já não é aplicável, mas é mantido para persistir as definições de utilizador em aplicações que funcionam no ambiente virtual (apenas app-V 5).|  
|Computadores com uma aplicação virtual específica|Mostra um resumo de computadores que têm o atalho app-V especificado que o Sequenciador de Gestão de Virtualização de Aplicações criou (apenas app-V 4.6).|  
|Computadores com um pacote específico de aplicação virtual|Mostra uma lista de computadores que têm o pacote de aplicações App-V especificado instalado (apenas App-V 4.6).|  
|Contar todas as instâncias de pacotes de aplicação virtual|Mostra uma contagem de todos os pacotes de aplicações App-V detetados (apenas App-V 4.6).|  
|Contar todas as instâncias de aplicações virtuais|Mostra uma contagem de todas as aplicações app-V detetadas (apenas App-V 4.6).|  

### <a name="log-files"></a>Ficheiros de registo  
O Gestor de Configuração regista informações sobre implementações de aplicações virtuais em ficheiros de registo. Para obter informações sobre os ficheiros de registo que as aplicações virtuais e a gestão da aplicação do Gestor de Configuração utilizam, consulte [ficheiros de registo](../../core/plan-design/hierarchy/log-files.md).  

Para o Windows 8.1, encontre registos para o cliente App-V em C:\ProgramData\Microsoft\Application Virtualization Client.  
