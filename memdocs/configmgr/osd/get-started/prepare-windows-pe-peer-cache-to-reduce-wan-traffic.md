---
title: Preparar a cache ponto a ponto do Windows PE para reduzir o tráfego WAN
titleSuffix: Configuration Manager
description: O Windows PE Peer Cache trabalha no Windows PE para obter conteúdo de um colega local e minimizar o tráfego wan quando não há ponto de distribuição local.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724042"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Prepare a cache de pares do Windows PE para reduzir o tráfego de WAN no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando implementa um novo sistema operativo no 'Gestor de Configuração', os computadores que executam a sequência de tarefas podem utilizar o Windows PE Peer Cache para obter conteúdo a partir de um par local (uma fonte de cache de pares) em vez de descarregar conteúdo a partir de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local.  

 O Windows PE Peer Cache é semelhante ao [Windows BranchCache,](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)mas funciona no Ambiente de Pré-Instalação do Windows (Windows PE). Os termos seguintes são utilizados para descrever os clientes que utilizam a Cache Ponto a Ponto do Windows PE:  

-   Um **cliente de cache ponto a ponto** é um computador que está configurado para utilizar a Cache Ponto a Ponto do Windows PE.  

-   Uma **origem de cache ponto a ponto** é um cliente que está configurado para a cache ponto a ponto e que fornece conteúdo a outros clientes de cache ponto a ponto que pedem esse conteúdo.  

Utilize as seguintes secções para gerir o Peer Cache.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> Objetos armazenados numa origem de Cache Ponto a Ponto  
 Uma sequência de tarefas configurada para utilizar a Cache Ponto a Ponto do Windows PE pode obter os seguintes objetos de conteúdos durante a execução no Windows PE:  

- Imagem do sistema operativo  

- Pacote de controladores  

- Pacotes e Programas (Quando o cliente continua a executar a sequência de tarefas em todo o sistema operativo, o cliente obtém este conteúdo a partir de uma fonte de cache de pares se a sequência de tarefas foi originalmente configurada para cache de pares quando está em execução no Windows PE.)  

- Imagens de arranque adicionais  

  Os objetos de conteúdos seguintes nunca são transferidos com a cache ponto a ponto. Em vez disso, são transferidos de um ponto de distribuição ou pelo Windows BranchCache se tiver configurado o Windows BranchCache no seu ambiente:  

- Aplicações  

- Atualizações de software  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a>Como funciona o Windows PE Peer Cache?  
 Considere um cenário onde uma sucursal não tem um ponto de distribuição mas tem vários clientes ativados para utilizar a Cache Ponto a Ponto do Windows PE. Implementa a sequência de tarefas configurada para utilizar a cache ponto a ponto em vários clientes que estão configurados para fazer parte da origem da cache ponto a ponto. O primeiro cliente a executar a sequência de tarefas difunde um pedido para um elemento com o conteúdo. Se não encontrar nenhum elemento, obtém o conteúdo a partir de um ponto de distribuição na WAN. O cliente instala a nova imagem e, em seguida, armazena o conteúdo na sua cache de cliente De Configuração Manager para que possa funcionar como uma fonte de cache de pares para outros clientes. Quando o cliente seguinte executar a sequência de tarefas, difunde um pedido na sub-rede para uma origem de cache ponto a ponto e o primeiro cliente responde e torna o seu conteúdo na cache disponível.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Determinar os clientes que vão fazer parte da origem da Cache Ponto a Ponto do Windows PE  
 Para ajudar a determinar quais os computadores a selecionar como origem da Cache Ponto a Ponto do Windows PE, deve considerar vários aspetos:  

-   A origem da Cache Ponto a Ponto do Windows PE deve ser um computador de secretária sempre ligado e disponível para os clientes da cache ponto a ponto.  

-   A Cache Ponto a Ponto do Windows PE tem um tamanho de cache de cliente suficiente para armazenar as imagens.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Requisitos para um cliente utilizar uma origem de Cache Ponto a Ponto do Windows PE  
 Para os clientes utilizarem uma origem de Cache Ponto a Ponto do Windows PE, têm de cumprir os seguintes requisitos:  

-   O cliente do Gestor de Configuração deve poder comunicar através das seguintes portas da sua rede:  

    -   Porta para a difusão de rede inicial, para encontrar uma origem de cache ponto a ponto. Por padrão, esta é a porta UDP 8004.  

    -   Porta para download de conteúdos a partir de uma fonte de cache de pares (HTTP e HTTPS). Por padrão, esta é a porta TCP 8003.  
    
        Para mais informações, consulte [as Portas utilizadas para ligações](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  Os clientes utilizarão HTTPS para transferir conteúdos, quando estiverem disponíveis. No entanto, é utilizado o mesmo número de porta para HTTP ou HTTPS.  

-   [Configure a Cache de Cliente dos Clientes do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) nos clientes para se certificar de que os mesmos têm espaço suficiente para manter e armazenar as imagens que implementa. A Cache Ponto a Ponto do Windows PE não afeta a configuração ou nem comportamento da cache do cliente.  

-   As opções de implementação para a implementação da sequência de tarefas têm de estar configuradas como Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a>Configure Windows PE Peer Cache  
 Pode utilizar os métodos seguintes para aprovisionar um cliente com conteúdo de cache ponto a ponto, para que possa servir como uma origem de cache ponto a ponto:  

- Um cliente de cache ponto a ponto que não consegue encontrar uma origem de cache ponto a ponto com o conteúdo irá transferir o mesmo de um ponto de distribuição.  Se o cliente recebe as definições de cliente que permitem uma cache ponto a ponto e a sequência de tarefas estiver configurada para preservar o conteúdo da cache, o cliente torna-se numa origem de cache ponto a ponto.  

- Um cliente de cache de pares pode obter conteúdo de outro cliente de cache peer (uma fonte de cache de pares).  Como o cliente está configurado como uma cache ponto a ponto, quando executa uma sequência de tarefas que está configurada para preservar os conteúdos em cache, o cliente torna-se numa origem de cache ponto a ponto.  

- Um cliente executa uma sequência de tarefas que inclui o passo opcional [Transferir Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), que é utilizado para pré-configurar o conteúdo relevante que está incluído na sequência de tarefas da Cache Ponto a Ponto do Windows PE. Quando utiliza este método:  

  -   O cliente não necessita de instalar a imagem que está a ser implementada.  

  -   Além da opção **Transferir Conteúdo do Pacote** , a sequência de tarefas tem também de utilizar a opção **Cache do cliente do Configuration Manager** . O utilizador utiliza esta opção para armazenar conteúdo na cache do cliente para que o cliente possa funcionar como uma origem de cache ponto a ponto para outros clientes de cache ponto a ponto.  

  Os seguintes procedimentos ajudá-lo-ão a configurar a Cache Ponto a Ponto do Windows PE em clientes e a configurar as sequências de tarefas que suporta a cache ponto a ponto.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Para configurar os computadores de origem da Cache Ponto a Ponto do Windows PE  

1. Na consola de Configuração Manager, navegue para**as Definições**do Cliente **de Administração** > e, em seguida, crie uma nova **Definição** de Dispositivo Personalizado do Cliente ou edite um objeto de definições existente. Também pode configurar estas opções para o objeto **Predefinições de Cliente** .  

   > [!TIP]  
   >  Utilize um objeto de definições personalizado para gerir que clientes recebem esta configuração. Por exemplo, é aconselhável evitar esta configuração nos portáteis dos utilizadores que frequentemente trabalham em viagem. Um sistema com elevada mobilidade pode ser uma origem fraca para fornecer conteúdo a outros clientes de cache ponto a ponto.  
   >   
   >  Lembre-se também de que quando configura esta definição como parte das **Predefinições de Cliente**, a configuração aplica-se a todos os clientes do seu ambiente.  

2. Em definições de **cache do cliente,** detete o cliente do Gestor de **Configuração ativa em todo o SISTEMA para partilhar conteúdo** para **Sim**.  

   -   Por predefinição, apenas está ativado HTTP. Se quer permitir que clientes transfiram conteúdo através de HTTPS, defina **Permitir HTTPS para comunicação entre elementos de rede do cliente** como **Sim**.  

   -   Por predefinição, a porta que difunde está definida como a porta 8004 e a porta para transferência de conteúdo está definida como a porta 8003. Pode alterar ambas.  

3. Guarde e implemente as Definições de Cliente nos clientes que selecionou como origem de cache ponto a ponto.  

   Depois de um dispositivo estar configurado com este objeto de definições, o mesmo está configurado para agir como uma origem de cache ponto a ponto. Estas definições devem ser implementadas em potenciais clientes de cache ponto a ponto para configurar as portas e protocolos necessários.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a>Configure uma sequência de tarefas para Windows PE Peer Cache  
 Quando configurar uma sequência de tarefas, utilize as seguintes variáveis de sequência de tarefas como Variáveis da Coleção na coleção onde pretende que seja implementada a sequência de tarefas:  

- **SMSTSPeerDownload**  

   Valor: VERDADEIRO  

   Isto permite ao cliente utilizar a Cache Ponto a Ponto do Windows PE.  

- **SMSTSPeerRequestPort**  

   Valor: número de porta <\>  

   Quando não utilizar a porta predefinida configurada nas Definições do Cliente (8004), deve configurar esta variável com um valor personalizado da porta de rede para utilizar para a transmissão inicial.  

- **SMSTSPreserveContent**  

   Valor: VERDADEIRO  

   Isto sinaliza o conteúdo na sequência de tarefas a reter na cache do cliente do Gestor de Configuração após a implantação. Isto é diferente de utilizar o SMSTSPersisContent que apenas preserva o conteúdo durante a duração da sequência de tarefas e utiliza a cache da sequência de tarefas, e não a cache do cliente do Gestor de Configuração.  

  Para obter mais informações, consulte variáveis de sequência de [tarefas](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a>Validar o sucesso da utilização da cache de pares do Windows PE  
 Depois de utilizar a cache ponto a ponto do Windows PE para implementar e instalar uma sequência de tarefas, pode confirmar que a cache ponto a ponto foi utilizada no processo visualizando o **smsts.log** no cliente que executou a sequência de tarefas.  

 No registo, localize uma entrada semelhante à seguinte onde <*SourceServerName*> identifica o computador a partir do qual o cliente obteve o conteúdo. Este computador deve ser uma origem de cache ponto a ponto e não um servidor de ponto de distribuição. Outros detalhes irão variar com base no seu ambiente e configurações locais.  

-   *<! [LOG[Ficheiro descarregado de http:// <\>SourceServerName :8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" data="06-26-2015" componente="ApplyOperatingSystem" contexto="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
