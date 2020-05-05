---
title: Selecionar métodos de deteção
titleSuffix: Configuration Manager
description: Analisar considerações sobre quais os métodos a utilizar e em que sites as executar.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718351"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Selecione métodos de descoberta para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para utilizar com sucesso e eficiência a descoberta para o Gestor de Configuração, deve considerar quais os métodos a utilizar e em que sites os executar.  

 Como a descoberta pode gerar um grande volume de tráfego de rede, e os consequentes registos de dados de descoberta (DDRs) podem usar recursos CPU significativos durante o processamento, usar apenas os métodos de descoberta que você precisa para cumprir os seus objetivos. Você pode começar usando apenas um ou dois métodos de descoberta, e depois permitir métodos adicionais de forma controlada para alargar o nível de descoberta no seu ambiente. A informação neste tópico pode ajudá-lo a tomar decisões informadas.  

 Para obter informações sobre os diferentes métodos de descoberta, consulte [sobre métodos](../../../../core/servers/deploy/configure/about-discovery-methods.md)de descoberta para O Gestor de Configuração .  

## <a name="select-methods-to-discover-different-things"></a>Selecione métodos para descobrir coisas diferentes  
 Para descobrir potenciais computadores clientes do Gestor de Configuração ou recursos do utilizador, deve ativar os métodos de descoberta adequados. Você pode usar diferentes combinações de métodos de descoberta para localizar diferentes recursos, e descobrir informações adicionais sobre esses recursos. Os métodos de descoberta que utiliza determinam o tipo de recursos que são descobertos e quais os serviços e agentes do Gestor de Configuração que são utilizados no processo de descoberta. Também determinam o tipo de informação sobre os recursos que pode descobrir.  

### <a name="discover-computers"></a>Descubra computadores   
Quando quiser descobrir computadores, pode utilizar a **Ative Directory System Discovery** ou a Network **Discovery**.  

 Por exemplo, se quiser descobrir recursos que possam instalar o cliente do Gestor de Configuração antes de utilizar a instalação push do cliente, poderá executar o Ative Directory System Discovery. Utilizando este método, não só descobre o recurso, como também descobre informações básicas até estendidas a partir dos Serviços de Domínio do Diretório Ativo. Estas informações podem ser úteis na construção de consultas e coleções complexas para utilizar para a atribuição de configurações de clientes ou implementação de conteúdos.

Em alternativa, poderá executar o Network Discovery e utilizar as suas opções para descobrir o sistema operativo de recursos (necessário utilizar posteriormente a instalação push do cliente). A Network Discovery fornece-lhe informações sobre a sua topologia de rede que não é capaz de adquirir com outros métodos de descoberta. Este método não lhe fornece, no entanto, qualquer informação sobre o seu ambiente de Diretório Ativo.

 Há também um método chamado **Heartbeat Discovery**. É possível utilizar apenas a Heartbeat Discovery para forçar a descoberta de clientes que instalou por métodos que não a instalação de impulso do cliente. No entanto, ao contrário de outros métodos de descoberta, a Heartbeat Discovery não pode descobrir computadores que não tenham um cliente ative De Configuração Manager. Devolve um conjunto limitado de informações, destinadas a manter um registo de base de dados existente em vez de ser a base desse registo. As informações submetidas pela Heartbeat Discovery podem não ser suficientes para construir consultas ou coleções complexas.  

 Se utilizar o **Ative Directory Group Discovery** para descobrir a adesão de um grupo especificado, pode descobrir informações limitadas sobre sistemas ou computadores. Isto não substitui uma descoberta completa de computadores, mas pode fornecer informações básicas. Esta informação é insuficiente para a instalação de impulso do cliente.  

### <a name="discover-users"></a>Descubra os utilizadores   
Quando pretender descobrir informações sobre os utilizadores, utilize a **Ative Directory User Discovery**. Semelhante ao Ative Directory System Discovery, este método descobre utilizadores do Ative Directory. Inclui informações básicas, para além de informações alargadas sobre o Diretório Ativo. Pode utilizar esta informação para construir consultas e coleções complexas semelhantes às dos computadores.  

### <a name="discover-group-information"></a>Descubra informações de grupo   
Quando quiser descobrir informações sobre grupos e membros do grupo, utilize a **Ative Directory Group Discovery**. Este método de descoberta cria registos de recursos para grupos de segurança.  

 Pode utilizar este método para pesquisar um grupo específico de Diretório Ativo para identificar os membros desse grupo, além de quaisquer grupos aninhados dentro desse grupo. Também pode utilizar este método para pesquisar um local de Diretório Ativo para grupos, e procurar recursivamente cada recipiente de crianças desse local em Serviços de Domínio de Diretório Ativo.  

 Este método de descoberta também pode pesquisar a adesão de grupos de distribuição. Isto pode identificar as relações de grupo tanto de utilizadores como de computadores.  

 Quando descobre um grupo, também pode descobrir informações limitadas sobre os seus membros. No entanto, isto não substitui o sistema de Diretório Ativo ou os métodos de descoberta do utilizador. É geralmente insuficiente para construir consultas e coleções complexas, ou servir como base de uma instalação push do cliente.  

### <a name="discover-infrastructure"></a>Descubra infraestrutura   
Existem dois métodos que pode usar para descobrir infraestruturas de rede, **Ative Directory Forest Discovery** e Network **Discovery.**  

 Utilize a Ative Directory Forest Discovery para pesquisar uma floresta de Diretório Ativo para obter informações sobre subredes e configurações de site de Diretório Ativo. Estas configurações podem então ser automaticamente inseridas no Gestor de Configuração como localizações de limites.  

 Quando quiser descobrir a sua topologia de rede, utilize a Network Discovery. Enquanto outros métodos de descoberta devolvem informações relacionadas com os Serviços de Domínio do Diretório Ativo, e podem identificar a localização atual da rede de um cliente, não fornecem informações de infraestrutura com base nas subredes e na topologia do router da sua rede.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a>Os dados da descoberta são partilhados entre sites  
 Após o Gestor de Configuração adicionar dados de descoberta a uma base de dados, é rapidamente partilhado entre todos os sites da hierarquia. Como normalmente não há benefício em descobrir a mesma informação em vários sites da sua hierarquia, considere criar uma única instância de cada método de descoberta que você usa para executar em um único site. É uma boa ideia fazer isto em vez de executar vários casos de um único método em diferentes sites.  

 No entanto, para alguns ambientes, pode ser útil atribuir o mesmo método de descoberta para executar em vários sites, cada um com uma configuração e horário separados. Por exemplo, ao utilizar o Network Discovery, é melhor direcionar cada site para descobrir a sua rede local, em vez de tentar descobrir todos os locais da rede através de um WAN.

Se configurar várias instâncias dos mesmos métodos de descoberta para executar em diferentes sites, planeje cuidadosamente a configuração de cada site. Pretende evitar que dois ou mais sites descubram os mesmos recursos da sua rede ou Diretório Ativo. Isto pode consumir largura de banda de rede adicional e criar DDRs duplicados.

A tabela que se segue identifica quais os locais onde pode configurar os diferentes métodos de descoberta.  

|Método de descoberta|Locais apoiados|  
|----------------------|-------------------------|  
|Deteção de Florestas do Active Directory|Site de administração central<br /><br /> Site primário|  
|Deteção de Grupos do Active Directory|Site primário|  
|Deteção de Sistemas do Active Directory|Site primário|  
|Deteção de Utilizadores do Active Directory|Site primário|  
|Descoberta do Batimento Cardíaco<sup>1</sup>|Site primário|  
|Deteção de Redes|Site primário<br /><br /> Site Secundário|  

 <sup>1</sup> Os sites secundários não podem configurar a Heartbeat Discovery, mas podem receber o DDR heartbeat de um cliente.  

 Quando os sites secundários executam a Network Discovery, ou recebem DDRs da Descoberta do Batimento Cardíaco, transferem o DDR por replicação baseada em ficheiros para o seu local primário principal. Isto porque apenas os locais primários e os locais da administração central podem processar DDRs. Para obter mais informações sobre como os DDRs são processados, consulte [sobre os registos](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs)de dados da descoberta .  

## <a name="considerations-for-different-discovery-methods"></a>Considerações para diferentes métodos de descoberta  
 Como cada servidor do site e ambiente de rede é diferente, é uma boa ideia limitar as suas configurações iniciais para descoberta. Em seguida, monitorize de perto cada servidor do site pela sua capacidade de processar os dados de descoberta que são gerados.  

Quando utiliza um método de descoberta de **Diretório ativo** para sistemas, utilizadores ou grupos:  

-   Execute a descoberta num site que tenha uma ligação rápida de rede aos seus controladores de domínio.  

-   Considere a topologia de replicação de Diretório Ativo para garantir que a descoberta pode aceder às informações mais recentes.  

-   Considere o âmbito da configuração da descoberta e limite a descoberta apenas para aqueles locais e grupos de Diretório Ativo que você tem que descobrir.  

Se utilizar a **Descoberta da Rede:**  

-   Utilize uma configuração inicial limitada para identificar a topografia da sua rede.  

-   Depois de identificar a topografia da rede, configura a Network Discovery para executar em sites específicos que são centrais para as áreas de rede que pretende descobrir de forma mais completa.  

Como a **Heartbeat Discovery** não funciona num local específico, não é preciso considerá-la no planeamento geral para onde executar a descoberta.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a>Boas práticas para a descoberta  
Para obter os melhores resultados com descoberta, recomendamos o seguinte:

- **Executar A Descoberta do Sistema de Diretório Ativo e a Descoberta do Utilizador de Diretório Ativo antes de executar a Ative Directory Group Discovery.**  

  Quando o Ative Directory Group Discovery identifica um utilizador ou computador anteriormente não descoberto como membro de um grupo, tenta descobrir detalhes básicos para o utilizador ou computador. Como o Ative Directory Group Discovery não está otimizado para este tipo de descoberta, este processo pode fazer com que seja executado lentamente. Além disso, o Ative Directory Group Discovery identifica apenas os detalhes básicos sobre os utilizadores e computadores que descobre, e não cria um registo completo de descobertade utilizador ou computador. Quando executa a Ative Directory System Discovery e ative Directory User Discovery, os atributos adicionais do Ative Directory para cada tipo de objeto estão disponíveis. Como resultado, ative Directory Group Discovery funciona de forma mais eficiente.  

- **Quando configurar o Ative Directory Group Discovery, apenas especifique grupos que utiliza com o Gestor de Configuração.**  

  Para ajudar a controlar a utilização de recursos pela Ative Directory Group Discovery, especifique apenas os grupos que utiliza com o Gestor de Configuração. Isto porque o Ative Directory Group Discovery procura recursivamente cada grupo que descobre para utilizadores, computadores e grupos aninhados. A procura de cada grupo aninhado pode expandir o âmbito do Ative Directory Group Discovery e reduzir o desempenho. Além disso, quando configuraa a descoberta delta para ative directory group Discovery, o método de descoberta monitoriza cada grupo para alterações. Isto reduz ainda mais o desempenho quando o método deve procurar grupos desnecessários.  

- **Estabeleça métodos de descoberta com um intervalo mais longo entre a descoberta completa, e um período mais frequente de descoberta delta.**  

  Como a descoberta delta usa menos recursos do que um ciclo de descoberta completo, e pode identificar recursos novos ou modificados no Ative Directory, você pode reduzir a frequência de ciclos de descoberta completos para executar semanalmente (ou menos). A descoberta da Delta para ative directory system discovery, Ative Directory User Discovery e Ative Directory Group Discovery identifica quase todas as mudanças de objetos de Diretório Ativo, e pode manter dados precisos de descoberta para recursos.  

- **Executar métodos de descoberta de Diretório Ativo num local primário que tenha uma localização de rede mais próxima do seu controlador de domínio Ative Directory.**  

  Para melhorar o desempenho da descoberta do Ative Directory, é uma boa ideia executar descobrir num site primário que tem uma ligação rápida de rede aos seus controladores de domínio. Se executar o mesmo método de descoberta de Diretório Ativo em vários locais, configurar cada método de descoberta para evitar sobreposição. Ao contrário de versões anteriores do Gestor de Configuração, os dados de descoberta são partilhados entre sites. Portanto, não é necessário descobrir a mesma informação em vários sites. Para mais informações, consulte os [dados do Discovery partilhados entre sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Executar Ative Directory Forest Discovery em apenas um site quando planeia criar automaticamente limites a partir dos dados de descoberta.**  

  Se executar a Ative Directory Forest Discovery em mais de um site numa hierarquia, é uma boa ideia permitir que as opções criem automaticamente limites num único site. Isto porque quando o Ative Directory Forest Discovery corre em cada local e cria limites, o Gestor de Configuração não pode fundir esses limites num único objeto de fronteira. Quando configurar o Ative Directory Forest Discovery para criar automaticamente limites em vários sites, o resultado pode ser duplicado de objetos de fronteira na consola do Gestor de Configuração.  
