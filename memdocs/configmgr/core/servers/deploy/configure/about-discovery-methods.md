---
title: Métodos de descoberta
titleSuffix: Configuration Manager
description: Conheça os métodos de descoberta disponíveis para encontrar dispositivos na sua rede, a partir do Ative Directory, ou Azure Ative Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: af35d5a941d5fd9bde2f87c8fb700b9d85e10b00
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078656"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Sobre métodos de descoberta para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os métodos de descoberta do Gestor de Configuração encontram diferentes dispositivos na sua rede, dispositivos e utilizadores do Ative Directory, ou utilizadores do Azure Ative Directory (Azure AD). Para utilizar de forma eficiente um método de descoberta, deve compreender as suas configurações e limitações disponíveis.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a>Descoberta florestal de diretório ativo  
 **Configurável:** Sim, é o que  

 **Ativado por defeito:** Não  

 **Contas** que pode usar para executar este método:  

-   **Conta de Descoberta Florestal do Diretório Ativo** (utilizador definido)  

-   **Conta** de computador do servidor do site  

Ao contrário de outros métodos de descoberta de Diretório Ativo, ative Directory Forest Discovery não descobre recursos que você pode gerir. Em vez disso, este método descobre localizações de rede que estão configuradas no Diretório Ativo. Pode converter esses locais em limites para ser usado em toda a sua hierarquia.  

Quando este método funciona, procura a floresta de Diretório Ativo local, cada floresta de confiança, e cada floresta adicional que configura no nó de Ative **Directory Forests** da consola De Configuração Manager.  

Utilize a Descoberta Florestal do Diretório Ativo para:  

-   Descubra sites e subnets de Diretório Ativo e, em seguida, crie limites de Gestor de Configuração com base nesses locais de rede.  

-   Identifique as superredes que são atribuídas a um site de Diretório Ativo. Converta cada supernet num limite de alcance de endereço IP.  

-   Publique para Ative Directory Domain Services (AD DS) numa floresta ao publicar para aquela floresta está ativado. A conta florestal de diretório ativo especificada deve ter permissões para aquela floresta.  

Pode gerir o Ative Directory Forest Discovery na consola Do Gestor de Configuração. Vá ao espaço de trabalho da **Administração** e expanda a **Configuração da Hierarquia.**   

-   **Métodos de Descoberta**: Permitir que a Ative Directory Forest Discovery corra no local de alto nível da sua hierarquia. Também pode especificar um simples horário para executar a descoberta. Configure-o para criar automaticamente limites a partir das subredes IP e sites de Diretório Ativo que descobre. A Ative Directory Forest Discovery não pode ser executada num local primário infantil ou num local secundário.  

-   **Florestas**de Diretório Ativo : Configure as florestas adicionais para descobrir, especificar cada Conta Florestal do Diretório Ativo e configurar a publicação em cada floresta. Monitorize o processo de descoberta. Adicione subredes IP e sites de Diretório Ativo como limites de Gestor de Configuração e membros de grupos de fronteira.  

Para configurar a publicação de florestas de Diretório Ativo para cada site da sua hierarquia, ligue a consola do Gestor de Configuração ao local de alto nível da sua hierarquia. O separador **Publishing** na caixa de diálogo **Propriedades** do site Ative Directy só pode mostrar o site atual e os seus sites infantis. Quando a publicação está habilitada para uma floresta, e o esquema dessa floresta é estendido para O Gestor de Configuração, são publicadas as seguintes informações para cada site que está habilitado a publicar para aquela floresta de Diretório Ativo:  

-    **Código do site&lt;SMS-Site>**

-   **SMS-MP-&lt;código de&lt;site>- nome do servidor do site>**  

-   **SMS-SLP-&lt;código de&lt;site>- nome do servidor do site>**  

-   **SMS-&lt;código local&lt;>- Nome ou sub-site de diretório ativo>**  

> [!NOTE]  
>  Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory. Se pretender que os sites secundários publiquem no Ative Directory, certifique-se de que a conta de computador do servidor do site secundário tem permissões para publicar no Ative Directory. Um site secundário não pode publicar dados para uma floresta não confiável.  

> [!CAUTION]  
>  Quando desverificar a opção de publicar um site para uma floresta de Diretório Ativo, todas as informações anteriormente publicadas para esse site, incluindo as funções disponíveis do sistema do site, são removidas do Ative Directory.  

As ações para Ative Directory Forest Discovery são registadas nos seguintes registos:  

-   Todas as ações, com exceção das ações relacionadas com a publicação, são registadas no ficheiro **ADForestDisc.Log** na pasta ** &lt;InstallationPath>\Logs** no servidor do site.  

-   As ações de publicação ative Directory Forest Discovery são registadas nos ficheiros **hman.log** e **sitecomp.log** na pasta ** &lt;InstallationPath>\Logs** no servidor do site.  

Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a>Descoberta do Grupo de Diretório Ativo  
**Configurável:** Sim, é o que  

**Ativado por defeito:** Não  

**Contas** que pode usar para executar este método:  

-   Conta de Descoberta do **Grupo de Diretório Ativo** (utilizador definido)  

-   **Conta** de computador do servidor do site  

> [!TIP]  
>  Além das informações nesta secção, consulte [as características comuns do Ative Directory Group, System e User Discovery](#bkmk_shared).  

Utilize este método para pesquisar Serviços de Domínio de Diretório Ativo para identificar:  

-   Grupos de segurança locais, globais e universais.  

-   A adesão de grupos.  

-   Informações limitadas sobre computadores e utilizadores membros de um grupo, mesmo quando outro método de descoberta não descobriu previamente esses computadores e utilizadores.  

Este método de descoberta destina-se a identificar grupos e as relações de grupo de membros de grupos. Por padrão, apenas grupos de segurança são descobertos. Se também quiser encontrar a adesão aos grupos de distribuição, deve consultar a caixa para obter a opção **Descubra a adesão de grupos de distribuição** no separador **Option** na caixa de diálogo **Ative Directory Group Discovery Properties.**  

A Ative Directory Group Discovery não suporta os atributos de Diretório Ativo alargados que podem ser identificados utilizando a Ative Directory System Discovery ou ative Directory User Discovery. Como este método de descoberta não está otimizado para descobrir recursos de computador e utilizador, considere executar este método de descoberta depois de executar Ative Directory System Discovery e Ative Directory User Discovery. Esta sugestão é porque este método cria um registo completo de dados de descoberta (DDR) para grupos, mas apenas um DDR limitado para computadores e utilizadores que são membros de grupos.  

Pode configurar os seguintes âmbitos de descoberta que controlam a forma como este método procura informações:  

-   **Localização**: Utilize um local se pretender pesquisar um ou mais recipientes de Diretório Ativo. Esta opção de âmbito suporta uma pesquisa recursiva dos recipientes de Diretório Ativo especificados. Este processo procura cada recipiente para crianças sob o recipiente que especifica. Continua até que não se encontremais contentores para crianças.  

-   **Grupos**: Utilize grupos se pretender pesquisar um ou mais grupos de Diretório Ativo específicos. Pode configurar o Domínio de **Diretório Ativo** para utilizar o domínio padrão e a floresta, ou limitar a pesquisa a um controlador de domínio individual. Além disso, pode especificar um ou mais grupos para pesquisar. Se não especificar pelo menos um grupo, todos os grupos encontrados na localização especificada do **Domínio do Diretório Ativo** são pesquisados.  

> [!CAUTION]  
>  Quando configurar um âmbito de descoberta, escolha apenas os grupos que deve descobrir. Esta recomendação é porque o Ative Directory Group Discovery tenta descobrir cada membro de cada grupo no âmbito da descoberta. A descoberta de grandes grupos pode exigir uma utilização extensiva da largura de banda e dos recursos do Diretório Ativo.  

> [!NOTE]  
>  Antes de poder criar coleções baseadas em atributos de Diretório Ativo alargados e garantir resultados precisos de descoberta para computadores e utilizadores, executar Ative Directory System Discovery ou Ative Directory User Discovery, dependendo do que pretende descobrir.  

As ações para ative directory Group Discovery são registadas no ficheiro **adsgdis.log** na pasta ** &lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Descoberta do sistema de diretório ativo  
**Configurável:** Sim, é o que  

**Ativado por defeito:** Não  

**Contas** que pode usar para executar este método:  

-   Conta de descoberta do sistema de **diretório ativo** (utilizador definido)  

-   **Conta** de computador do servidor do site  

> [!TIP]  
>  Além das informações nesta secção, consulte [as características comuns do Ative Directory Group, System e User Discovery](#bkmk_shared).  

Utilize este método de descoberta para pesquisar as localizações especificadas dos Serviços de Domínio do Diretório Ativo para obter recursos informáticos que possam ser usados para criar coleções e consultas. Também pode instalar o cliente Do Gestor de Configuração num dispositivo descoberto utilizando a instalação push do cliente.  

Por padrão, este método descobre informações básicas sobre o computador, incluindo os seguintes atributos:  

-   Nome do computador  

-   Sistema operativo e versão  

-   Nome do recipiente de diretório ativo  

-   Endereço IP  

-   Site do Active Directory  

-   Carimbo de tempo do último logon  

Para criar com sucesso um DDR para um computador, o Ative Directory System Discovery deve ser capaz de identificar a conta do computador e, em seguida, resolver com sucesso o nome do computador para um endereço IP.  

Na caixa de diálogo Ative **Directory System Discovery Properties,** no separador **Ative Directory Atributos,** pode ver a lista completa de atributos de objetos padrão que descobre. Também pode configurar o método para descobrir atributos adicionais (estendidos).  

As ações para ative directory system Discovery são registadas no ficheiro **adsysdis.log** na pasta ** &lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a>Descoberta de utilizador de diretório ativo  
**Configurável:** Sim, é o que  

**Ativado por defeito:** Não  

**Contas** que pode usar para executar este método:  

-   Conta de descoberta de utilizadores de **diretório ativo** (utilizador definido)  

-   **Conta** de computador do servidor do site  

> [!TIP]  
>  Além das informações nesta secção, consulte [as características comuns do Ative Directory Group, System e User Discovery](#bkmk_shared).  

Utilize este método de descoberta para pesquisar Serviços de Domínio de Diretório Ativo para identificar contas de utilizador e atributos associados. Por padrão, este método descobre informações básicas sobre a conta do utilizador, incluindo os seguintes atributos:  

-   Nome de utilizador  

-   Nome único do utilizador (inclui nome de domínio)  

-   Domain  

-   Nomes de contentores de diretório ativo  

Na caixa de diálogo **Ative Directory User Discovery Properties,** no separador **Ative Directory Atributos,** pode ver a lista completa de atributos de objetoque descobre. Também pode configurar o método para descobrir atributos adicionais (estendidos).

As ações para a Ative Directory User Discovery são registadas no ficheiro **adusrdis.log** na pasta ** &lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Descoberta de utilizador de diretório ativo Azure

Utilize o Azure Ative Directory (Azure AD) User Discovery para pesquisar a subscrição do Azure AD para utilizadores com uma identidade na nuvem moderna. A descoberta do utilizador da AD Azure pode encontrar os seguintes atributos:

- objectId
- displayName
- correio
- mailApelido
- onPremisesSecurityIdentifier
- userPrincipalName
- Inquilino da AAD
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistintoNome

Este método suporta a sincronização completa e delta dos atributos dos utilizadores da Azure AD. Estas informações podem então ser utilizadas juntamente com os dados de descoberta que recolhe dos outros métodos de descoberta.

As ações para a descoberta do utilizador da AD Azure são registadas no ficheiro **SMS_AZUREAD_DISCOVERY_AGENT.log** no servidor de topo da hierarquia.

Para configurar a descoberta do utilizador da AD Azure, consulte o [Configure Azure Services](azure-services-wizard.md) for Cloud Management. Para obter informações sobre como configurar este método de descoberta, consulte [Configure Azure AD User Discovery](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Descoberta do grupo de utilizadores do Diretório Ativo Azure
<!--3611956-->
*(Introduzido como uma [funcionalidade de pré-lançamento](../../manage/pre-release-features.md) na versão 1906)*

Pode descobrir grupos de utilizadores e membros desses grupos do diretório Azure Ative (Azure AD). A descoberta do grupo de utilizadores Da Azure AD pode encontrar os seguintes atributos:

- objectId
- displayName
- mailApelido
- onPremisesSecurityIdentifier
- Inquilino da AAD

As ações para a descoberta do grupo de utilizadores Da Azure AD são registadas no ficheiro **SMS_AZUREAD_DISCOVERY_AGENT.log** no servidor de topo da hierarquia. Para obter informações sobre como configurar este método de descoberta, consulte a descoberta do grupo de utilizadores da [AD Configure Azure](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a>Descoberta do Batimento Cardíaco  
**Configurável:** Sim, é o que  

**Ativado por defeito:** Sim, é o que  

**Contas** que pode usar para executar este método:  

-   **Conta** de computador do servidor do site  

A Descoberta do Batimento Cardíaco difere de outros métodos de descoberta do Gestor de Configuração. É ativado por padrão e funciona em cada cliente de computador (em vez de num servidor de site) para criar um DDR. Para os clientes de dispositivos móveis, este DDR é criado pelo ponto de gestão que o cliente do dispositivo móvel está a usar. Para ajudar a manter o registo da base de dados dos clientes do Gestor de Configuração, não desative a Heartbeat Discovery. Além de manter o registo da base de dados, este método pode forçar a descoberta de um computador como um novo registo de recursos. Também pode repovoar o registo da base de dados de um computador que foi apagado da base de dados.  

Heartbeat Discovery corre numa programação configurada para todos os clientes da hierarquia. O horário padrão para a Descoberta do Batimento Cardíaco está definido para cada sete dias. Se alterar o intervalo de descoberta do batimento cardíaco, certifique-se de que funciona com mais frequência do que a tarefa de manutenção do local **Eliminar Dados de Descobertas Envelhecidas**. Esta tarefa elimina os registos inativos dos clientes da base de dados do site. Só é possível configurar a tarefa Eliminar Dados **de Descobertas Envelhecidas** apenas para sites primários. 

Também pode invocar manualmente a Heartbeat Discovery num cliente específico. Executar o Ciclo de Recolha de **Dados discovery** no separador **Action** do painel de controlo do Gestor de Configuração de um cliente.  

Quando a Heartbeat Discovery funciona, cria um DDR que tem a informação atual do cliente. Em seguida, o cliente copia este pequeno ficheiro (cerca de 1 KB em tamanho) para um ponto de gestão para que um site primário possa processá-lo. O ficheiro tem as seguintes informações:  

-   Localização da rede  

-   Nome NetBIOS  

-   Versão do agente cliente  

-   Detalhes do estado operacional  

Heartbeat Discovery é o único método de descoberta que fornece detalhes sobre o estado de instalação do cliente. Fá-lo atualizando o atributo do cliente de recursos do sistema para definir um valor igual ao **Sim**.  

> [!NOTE]  
>  Mesmo quando a Heartbeat Discovery é desativada, os DDRs ainda são criados e submetidos para clientes de dispositivos móveis ativos. Este comportamento garante que a tarefa de eliminar dados de **descobertas envelhecidas** não afeta dispositivos móveis ativos. Quando a tarefa Eliminar Dados **de Descobertas Envelhecidas** elimina um registo de base de dados para um dispositivo móvel, também revoga o certificado do dispositivo. Esta ação impede o dispositivo móvel de ligar-se a pontos de gestão.  

As ações para a Heartbeat Discovery estão registadas nos seguintes locais:  

-   Para os clientes de computador, as ações da Heartbeat Discovery são registadas no cliente no ficheiro **InventoryAgent.log** na pasta *%Windir%\CCM\Logs.*  

-   Para os clientes de dispositivos móveis, as ações da Heartbeat Discovery são registadas no ficheiro **DMPRP.log** na pasta *%\CCM\Logs* do ponto de gestão que o cliente do dispositivo móvel utiliza.  

Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a>Descoberta da Rede  
**Configurável:** Sim, é o que  

**Ativado por defeito:** Não  

**Contas** que pode usar para executar este método:  

-   **Conta** de computador do servidor do site  

Utilize este método para descobrir a topoologia da sua rede e para descobrir dispositivos na sua rede que tenham um endereço IP. A Network Discovery procura a sua rede por recursos ip-enabled consultando as seguintes entidades: 
- Servidores que executam uma implementação da Microsoft do DHCP
- Caches do Protocolo de Resolução de Endereços (ARP) em routers de rede
- Dispositivos ativados por SNMP
- Domínios de Diretório Ativo  

Antes de poder utilizar a Descoberta da Rede, deve especificar o *nível* de descoberta a ser executado. Também configura um ou mais mecanismos de descoberta que permitem ao Network Discovery consultar segmentos de rede ou dispositivos. Também pode configurar configurações que ajudam a controlar as ações de descoberta na rede. Finalmente, define um ou mais horários para quando a Network Discovery corre.  

Para que este método descubra com sucesso um recurso, a Network Discovery deve identificar o endereço IP e a máscara de sub-rede do recurso. São utilizados os seguintes métodos para identificar a máscara de sub-rede de um objeto:  

-   **Cache ARP do router:** A Network Discovery consulta a cache ARP de um router para encontrar informações de sub-rede. Normalmente, os dados numa cache ARP do router têm um curto tempo de vida. Portanto, quando a Network Discovery questiona a cache ARP, a cache ARP pode deixar de ter informações sobre o objeto solicitado.  

-   **DHCP:** O Network Discovery consulta cada servidor DHCP que especifica para descobrir os dispositivos para os quais o servidor DHCP forneceu um aluguer. O Network Discovery suporta apenas servidores DHCP que executam a implementação da Microsoft do DHCP.  

-   **Dispositivo SNMP:** A Network Discovery pode consultar diretamente um dispositivo SNMP. Para que a Network Discovery questione um dispositivo, o dispositivo deve ter um agente SNMP local instalado. Configure também a Network Discovery para usar o nome comunitário que o agente SNMP está a usar.  

Quando a descoberta identifica um objeto endereço IP e pode determinar a máscara de sub-rede do objeto, cria um DDR para esse objeto. Como diferentes tipos de dispositivos se ligam à rede, o Network Discovery descobre recursos que não suportam o cliente do Gestor de Configuração. Por exemplo, os dispositivos que podem ser descobertos mas não geridos incluem impressoras e routers.  

A Network Discovery pode devolver vários atributos como parte do registo de descoberta que cria. Estes atributos incluem:  

-   Nome NetBIOS  

-   Endereços IP  

-   Domínio de recursos  

-   Funções do sistema  

-   Nome comunitário SNMP  

-   Endereços MAC  

A atividade da Discovery da Rede é registada no ficheiro **Netdisc.log** no * &lt;\>InstallationPath \Logs* no servidor do site que executa a descoberta.  

 Para obter mais informações sobre como configurar este método de descoberta, consulte métodos de [descoberta configure](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Redes complexas e ligações de baixa largura de banda podem fazer com que a Network Discovery corra lentamente e gere tráfego significativo de rede. Como uma boa prática, executar a Network Discovery apenas quando os outros métodos de descoberta não encontrarem os recursos que você tem que descobrir. Por exemplo, utilize o Network Discovery se tiver de descobrir computadores de grupo de trabalho. Outros métodos de descoberta não descobrem computadores de grupo de trabalho.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a>Níveis de Descoberta da Rede  
Ao configurar a Discovery da Rede, especifice um dos três níveis de descoberta:  

|Nível de descoberta|Detalhes|  
|------------------------|-------------|  
|Topologia|Este nível descobre routers e subredes, mas não identifica uma máscara de sub-rede para objetos.|  
|Topologia e cliente|Além da topologia, este nível descobre potenciais clientes como computadores, e recursos como impressoras e routers. Este nível de descoberta tenta identificar a máscara de sub-rede de objetos que encontra.|  
|Topologia, cliente e sistema operativo de cliente|Além da topologia e potenciais clientes, este nível tenta descobrir o nome e versão do sistema operativo do computador. Este nível utiliza chamadas de Rede Windows Browser e Windows.|  

 A cada nível incremental, a Network Discovery aumenta a sua atividade e a utilização da largura de banda da rede. Considere o tráfego de rede que pode ser gerado antes de ativar todos os aspetos da Descoberta da Rede.  

 Por exemplo, quando utilizar pela primeira vez o Network Discovery, pode começar apenas com o nível de topologia para identificar a sua infraestrutura de rede. Em seguida, reconfigurar a Rede Discovery para descobrir objetos e seus sistemas operativos de dispositivos. Também pode configurar configurações que limitam o Discovery da Rede a uma gama específica de segmentos de rede. Dessa forma, descobre-se objetos em locais de rede que necessita e evita o tráfego desnecessário da rede. Este processo também permite descobrir objetos de routers de borda ou de fora da sua rede.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a>Opções de Descoberta de Rede  
Para permitir que a Network Discovery procure dispositivos endereçoIP, configure uma ou mais destas opções.  

> [!NOTE]  
>  A Discovery da Rede corre no contexto da conta de computador do servidor do site que executa a descoberta. Se a conta de computador não tiver permissões para um domínio não confiável, as configurações do servidor de domínio e DHCP podem não conseguir descobrir recursos.  

#### <a name="dhcp"></a>DHCP  

Especifique cada servidor DHCP que deseja que o Network Discovery faça consulta. (A Network Discovery suporta apenas servidores DHCP que executam a implementação da Microsoft do DHCP.)  

-   O Network Discovery recupera informações utilizando chamadas de procedimento remoto para a base de dados do servidor DHCP.  

-   O Network Discovery pode consultar os servidores DHCP de 32 bits e 64 bits para uma lista de dispositivos que estão registados em cada servidor.  

-   Para que a Discovery da Rede questione com sucesso um servidor DHCP, a conta de computador do servidor que executa a descoberta deve ser um membro do grupo de Utilizadores DHCP no servidor DHCP. Por exemplo, este nível de acesso existe quando uma das seguintes declarações é verdadeira:  

    -   O servidor DHCP especificado é o servidor DHCP do servidor que executa a descoberta.  

    -   O computador que executa a descoberta e o servidor DHCP estão no mesmo domínio.  

    -   Existe uma confiança bidirecional entre o computador que executa a descoberta e o servidor DHCP.  

    -   O servidor do site é um membro do grupo de Utilizadores DHCP.  

-   Quando o Network Discovery enumera um servidor DHCP, nem sempre descobre endereços IP estáticos. A Network Discovery não encontra endereços IP que façam parte de uma gama excluída de endereços IP no servidor DHCP. Também não descobre endereços IP reservados para atribuição manual.  

#### <a name="domains"></a>Domínios  

Especifique cada domínio que pretende que a Descoberta da Rede faça consulta.  

-   A conta de computador do servidor do site que executa a descoberta deve ter permissões para ler os controladores de domínio em cada domínio especificado.  

-   Para descobrir computadores a partir do domínio local, deve ativar o serviço browser de computador em pelo menos um computador. Este computador deve estar na mesma sub-rede que o servidor do site que executa o Network Discovery.  

-   O Network Discovery pode descobrir qualquer computador que possa visualizar a partir do seu servidor de site quando navega na rede.  

-   A Network Discovery recupera o endereço IP. Em seguida, utiliza um pedido de eco do Protocolo de Mensagem de Controlo de Internet (ICMP) para abater cada dispositivo que encontra. O comando **de ping** ajuda a determinar quais os computadores que estão atualmente ativos.  

#### <a name="snmp-devices"></a>Dispositivos SNMP  

Especifique cada dispositivo SNMP que pretende que a Descoberta da Rede faça consulta.  

-   A Network Discovery recupera o valor ipNetToMediaTable de qualquer dispositivo SNMP que responda à consulta. Este valor devolve matrizes de endereços IP que são computadores clientes ou outros recursos, como impressoras, routers ou outros dispositivos endereçoIP.  

-   Para consultar um dispositivo, deve especificar o endereço IP ou o nome NetBIOS do dispositivo.  

-   Configure a Discovery da Rede para utilizar o nome comunitário do dispositivo, ou o dispositivo rejeita a consulta baseada em SNMP.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a>Limitação da descoberta da rede  
Quando o Network Discovery questiona um dispositivo SNMP na borda da sua rede, pode identificar informações sobre subredes e dispositivos SNMP que estão fora da sua rede imediata. Utilize as seguintes informações para limitar a Descoberta da Rede configurando os dispositivos SNMP com os quais a descoberta pode comunicar e especificando os segmentos de rede para consulta.  

#### <a name="subnets"></a>Sub-redes  

Configure as subredes que a Network Discovery questiona quando utiliza as opções SNMP e DHCP. Estas duas opções procuram apenas as subredes ativadas.  

Por exemplo, um pedido de DHCP pode devolver dispositivos de locais de toda a sua rede. Se pretender descobrir apenas dispositivos numa sub-rede específica, especifique e ative essa sub-rede específica no separador **Subnets** na caixa de diálogo **Network Discovery Properties.** Quando especifica e ativa as subredes, limita futuras tarefas de descoberta de DHCP e SNMP a essas subredes.  

> [!NOTE]  
>  As configurações de sub-rede não limitam os objetos que a opção de descoberta de **Domínios** descobre.  

#### <a name="snmp-community-names"></a>Nomes comunitários sNMP  

Para permitir que a Network Discovery questione com sucesso um dispositivo SNMP, configure a Discovery da Rede com o nome comunitário do dispositivo. Se o Network Discovery não estiver configurado utilizando o nome comunitário do dispositivo SNMP, o dispositivo rejeita a consulta.  

#### <a name="maximum-hops"></a>Lúpulo máximo  

Quando configura o número máximo de saltos de router, limita o número de segmentos de rede e routers que o Network Discovery pode consultar utilizando o SNMP.  

O número de lúpulos que configura limita o número de dispositivos adicionais e segmentos de rede que o Network Discovery pode consultar.  

Por exemplo, uma descoberta apenas topologia com **0** (zero) saltos de router descobre a subrede na qual reside o servidor originário. Inclui quaisquer routers na sub-rede.  

O diagrama seguinte mostra o que uma consulta de Descoberta de Rede só de topologia encontra quando funciona no Servidor 1 com 0 saltos de router especificados: subnet D e Router 1.  

 ![Imagem de descoberta com salto de router zero](media/Disc-0.gif)  

 O diagrama seguinte mostra o que uma consulta de topologia e cliente Network Discovery encontra quando funciona no Servidor 1 com 0 saltos de router especificados: subnet D e Router 1, e todos os potenciais clientes na subnet D.  

 ![Imagem de descoberta com um salto de router](media/Disc-1.gif)  

 Para ter uma ideia melhor de como o saltos de router adicionais pode aumentar a quantidade de recursos de rede que são descobertos, considere a seguinte rede:  

 ![Imagem de descoberta com dois saltos de router](media/Disc-2.gif)  

 Executar uma Descoberta de Rede só de topologia a partir do Servidor 1 com um router hop descobre as seguintes entidades:  

-   Router 1 e subnet 10.1.10.0 (encontrado sem lúpulo zero)  

-   Sub-redes 10.1.20.0 e 10.1.30.0, subnet A e Router 2 (encontrado saqueado no primeiro salto)  

> [!WARNING]  
>  Cada aumento para o número de saltos de router pode aumentar significativamente o número de recursos descobriveis e aumentar a largura de banda da rede que o Network Discovery utiliza.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a>Descoberta do Servidor  
**Configurável:** Não  

Além dos métodos de descoberta configuráveis pelo utilizador, o Gestor de Configuração utiliza um processo chamado **Server Discovery** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Este método de descoberta cria registos de recursos para computadores que são sistemas de sites, como um computador que é configurado como um ponto de gestão.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a>Características comuns da Descoberta do Grupo de DirectórioActivo, Descoberta do Sistema e Descoberta de Utilizadores  
Esta secção fornece informações sobre funcionalidades que são comuns aos seguintes métodos de descoberta:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

> [!NOTE]  
>  A informação nesta secção não se aplica à Ative Directory Forest Discovery.  

Estes três métodos de descoberta são semelhantes na configuração e operação. Podem descobrir computadores, utilizadores e informações sobre membros do grupo de recursos armazenados em Serviços de Domínio de Diretório Ativo. O processo de descoberta é gerido por um agente de descoberta. O agente executa no servidor do site em cada site onde a descoberta está configurada para ser executada. Pode configurar cada um destes métodos de descoberta para pesquisar um ou mais locais de Diretório Ativo como instâncias de localização na floresta local ou florestas remotas.  

Quando a descoberta procura recursos numa floresta não confiável, o agente de descoberta deve ser capaz de resolver o seguinte para ser bem sucedido:  

-   Para descobrir um recurso informático utilizando a Ative Directory System Discovery, o agente de descoberta deve ser capaz de resolver o FQDN do recurso. Se não conseguir resolver o FQDN, tenta então resolver o recurso pelo seu nome NetBIOS.  

-   Para descobrir um utilizador ou recurso de grupo utilizando a Ative Directory User Discovery ou ative Directory Group Discovery, o agente de descoberta deve ser capaz de resolver o FQDN do nome do controlador de domínio que especifica para a localização do Diretório Ativo.  

Para cada local que especifica, pode configurar opções individuais de pesquisa, como permitir uma pesquisa recursiva dos contentores de crianças Do Diretório Ativo do local. Também pode configurar uma conta única para usar quando pesquisa esse local. Esta conta proporciona flexibilidade na configuração de um método de descoberta num site para pesquisar vários locais de Diretório Ativo em várias florestas. Não é preciso configurar uma única conta que tenha permissões para todos os locais.  

Quando cada um destes três métodos de descoberta funciona num site específico, o servidor do site do Gestor de Configuração desse site contacta o controlador de domínio mais próximo na floresta de Diretório Ativo especificada para localizar recursos de Diretório Ativo. O domínio e a floresta podem estar em qualquer modo Ative Directy suportado. A conta que atribui a cada instância de localização deve ter a **permissão de** acesso de Leitura para as localizações específicas do Diretório Ativo.

A Discovery procura nos locais especificados por objetos e tenta recolher informações sobre esses objetos. Um DDR é criado quando podem ser identificadas informações suficientes sobre um recurso. A informação necessária varia consoante o método de descoberta que está a ser utilizado.  

Se configurar o mesmo método de descoberta para executar em diferentes sites do Gestor de Configuração para tirar partido da consulta de servidores locais do Ative Directory, pode configurar cada site com um conjunto único de opções de descoberta. Como os dados de descoberta são partilhados com cada site na hierarquia, evite sobreposição entre estas configurações para descobrir eficientemente cada recurso uma única vez.

Para ambientes mais pequenos, considere executar cada método de descoberta em apenas um local da sua hierarquia. Esta configuração reduz a sobrecarga administrativa e o potencial para múltiplas ações de descoberta para redescobrir os mesmos recursos. Ao minimizar o número de sites que executam a descoberta, reduz-se a largura de banda da rede global que a descoberta utiliza. Também pode reduzir o número total de DDRs que são criados e devem ser processados pelos servidores do seu site.  

Muitas das configurações do método de descoberta são autoexplicativas. Utilize as seguintes secções para obter mais informações sobre as opções de descoberta que possam necessitar de informações adicionais antes de as configurar.  

As seguintes opções estão disponíveis para utilização com múltiplos métodos de descoberta de Diretório Ativo:  

-   [Descoberta Delta](#bkmk_delta)  

-   [Filtrar registos de computador estonteantes por logon de domínio](#bkmk_stalelogon)  

-   [Registos de filtro stale por senha de computador](#bkmk_stalepassword)  

-   [Pesquisar atributos de Diretório Ativo personalizados](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a>Descoberta Delta  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

A Delta Discovery não é um método de descoberta independente, mas uma opção disponível para os métodos de descoberta aplicáveis. A Delta Discovery procura atributos específicos do Ative Directory para as alterações que foram feitas desde o último ciclo completo de descoberta do método de descoberta aplicável. As alterações de atributo são submetidas à base de dados do Gestor de Configuração para atualizar o registo de descoberta do recurso.  

Por defeito, a Delta Discovery corre num ciclo de cinco minutos. Este horário é muito mais frequente do que o horário típico para um ciclo de descoberta completo. Este ciclo frequente é possível porque a Delta Discovery utiliza menos recursos de servidores e rede do que um ciclo de descoberta completo. Quando utilizar o Delta Discovery, pode reduzir a frequência do ciclo de descoberta seleção para esse método de descoberta.  

Seguem-se as alterações mais comuns que a Delta Discovery deteta:  

-   Novos computadores ou utilizadores adicionados ao Diretório Ativo  

-   Alterações à informação básica do computador e do utilizador  

-   Novos computadores ou utilizadores que são adicionados a um grupo  

-   Computadores ou utilizadores que são removidos de um grupo  

-   Alterações aos objetos do grupo do sistema  

Embora a Delta Discovery possa detetar novos recursos e alterações na adesão ao grupo, não consegue detetar quando um recurso foi eliminado do Ative Directory. Os DDRs criados pela Delta Discovery são processados da mesma forma que os DDRs que são criados por um ciclo de descoberta completo.  

Configura a Delta Discovery no separador Agenda de **Sondagens** nas propriedades para cada método de descoberta.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a>Filtrar registos de computador estonteantes por logon de domínio  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a descoberta para excluir computadores com um registo de computador estonteante. Esta exclusão baseia-se no último logon de domínio do computador. Quando esta opção está ativada, o Ative Directory System Discovery avalia cada computador que identifica. Ative Directory Group Discovery avalia cada computador que é membro de um grupo que é descoberto.  

Para utilizar esta opção:  

-   Os computadores devem ser configurados para atualizar o último atributo **LogonTimeStamp** nos Serviços de Domínio do Diretório Ativo.  

-   O nível funcional do domínio Ative Diretório deve ser definido para o Windows Server 2003 ou posteriormente.  

Quando estiver a configurar o tempo após o último logon que pretende utilizar para esta definição, considere o intervalo para a replicação entre controladores de domínio.  

Configura a filtragem no separador **Option** nas propriedades de descoberta do sistema de **diretório ativo** e nas caixas de diálogo **do Grupo DeSonio** Ative Group Discovery Properties. Escolha **apenas descobrir computadores que tenham iniciado um registo num domínio num determinado período de tempo**.  

> [!WARNING]  
>  Quando configurar este filtro e **filtrar registos por palavra-passe de computador,** a descoberta exclui computadores que satisfaçam os critérios de qualquer um dos filtros.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a>Registos de filtro stale por senha de computador  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a descoberta para excluir computadores com um registo de computador estonteante. Esta exclusão baseia-se na última atualização de palavra-passe da conta de computador pelo computador. Quando esta opção está ativada, o Ative Directory System Discovery avalia cada computador que identifica. Ative Directory Group Discovery avalia cada computador que é membro de um grupo que é descoberto.  

Para utilizar esta opção:  

-   Os computadores devem ser configurados para atualizar o atributo **pwdLastSet** em Serviços de Domínio de Diretório Ativo.  

Quando estiver a configurar esta opção, considere o intervalo para atualizações a este atributo. Considere também o intervalo de replicação entre controladores de domínio.  

Configura a filtragem no separador **Option** nas propriedades de descoberta do sistema de **diretório ativo** e nas caixas de diálogo **do Grupo DeSonio** Ative Group Discovery Properties. Escolha **apenas descobrir computadores que tenham atualizado a sua palavra-passe**de conta de computador num determinado período de tempo .  

> [!WARNING]  
>  Quando configurar este filtro e **filtrar registos de stale por logon**de domínio, a descoberta exclui computadores que satisfaçam os critérios de qualquer um dos filtros.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a>Pesquisar atributos de Diretório Ativo personalizados  
 Disponível para:  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

Cada método de descoberta suporta uma lista única de atributos do Diretório Ativo que podem ser descobertos.  

Pode visualizar e configurar a lista de atributos personalizados no separador **Ative Directory Atributos** nas propriedades de discovery properties do sistema de **diretório ativo** e nas caixas de diálogo **do Utilizador Discovery Properties.**  
