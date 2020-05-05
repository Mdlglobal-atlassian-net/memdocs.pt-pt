---
title: Atribuir clientes a um site
titleSuffix: Configuration Manager
description: Atribuir clientes a um site em 'Gestor de Configuração'.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075749"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Como atribuir clientes a um site em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de instalado um cliente do Gestor de Configuração, deve juntar-se a um site primário do Gestor de Configuração antes de o poder gerir. O site a que um cliente se junta chama-se o seu *site atribuído.* Os clientes não podem ser atribuídos a um site de administração central ou a um site secundário.  

O processo de atribuição ocorre depois de o cliente ser instalado com sucesso e determina qual o site que gere o computador cliente. Pode atribuir diretamente o cliente a um site, ou pode utilizar a atribuição automática do site onde o cliente encontre automaticamente um site apropriado com base na sua localização atual da rede ou num site de recuo que tenha sido configurado para a hierarquia.

Quando instala o cliente do dispositivo móvel durante a inscrição do Gestor de Configuração, o dispositivo é sempre automaticamente atribuído a um site. Quando instala o cliente num computador, pode escolher se atribui ou não o cliente a um site. No entanto, se o cliente estiver instalado mas não atribuído, permanecerá não gerido até a atribuição de site ser concluída com êxito.  
 

> [!NOTE]  
>  Atribua sempre clientes a sites que executam a mesma versão do Gestor de Configuração. Evite atribuir um cliente de Gestor de Configuração a partir de um lançamento mais recente para um site a partir de um lançamento mais antigo.   Se necessário, atualize o site principal para a mesma versão do Gestor de Configuração que está a utilizar para os clientes.  

Após o cliente ser atribuído a um site, permanecerá atribuído a esse site mesmo que o cliente altere o respetivo endereço IP ou faça roaming para outro site. Apenas um administrador pode atribuir manualmente o cliente a outro site ou remover a atribuição do cliente.  

> [!WARNING]  
>  A exceção à permanência da atribuição de um cliente a um site verifica-se quando o cliente é atribuído num dispositivo Windows Embedded enquanto os filtros de escrita estão ativados. Se não desativar em primeiro lugar os filtros de escrita que atribuiu ao cliente, o estado de atribuição de site do cliente regressará ao estado original durante o próximo reinício do dispositivo.  
>   
>  Por exemplo, se o cliente estiver configurado para a atribuição automática de sites, a reatribuição será feita durante o arranque e poderá resultar na atribuição a um site diferente. Se o cliente não estiver configurado para a atribuição automática do site, mas necessitar da atribuição manual do site, terá de reatribuir manualmente o cliente após o arranque antes de poder gerir novamente este cliente utilizando o Gestor de Configuração.  
>   
>  Para evitar este comportamento, desative os filtros de escrita antes de atribuir o cliente em dispositivos incorporados e, em seguida, ative os filtros de escrita após ter confirmado que a atribuição do site foi concluída com êxito.  

Se a atribuição do cliente falhar, o software do cliente permanece instalado, mas não será gerido. Um cliente é considerado não gerido quando é instalado, mas não atribuído a um site, ou quando é atribuído a um site mas não consegue comunicar com um ponto de gestão.  

##  <a name="using-manual-site-assignment-for-computers"></a>Utilizar a atribuição manual de sites a computadores  
 Pode atribuir manualmente computadores cliente a um site utilizando os dois métodos seguintes:  

-   Utilize uma propriedade de instalação de cliente que especifique o código do site.  

-   Em **Configuration Manager**do Painel de Controlo, especifique o código do site.  

> [!NOTE]  
>  Se atribuir manualmente um computador cliente a um código de site do Gestor de Configuração que não existe, a atribuição do site falha.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a>Utilização automática da atribuição do site para computadores  
 A atribuição automática de site pode ocorrer durante a implementação do cliente ou quando clica na opção **Procurar Site** do separador **Avançadas** das **Propriedades do Configuration Manager** no Painel de Controlo. O cliente do Gestor de Configuração compara a sua própria localização de rede com os limites configurados na hierarquia do Gestor de Configuração. Quando a localização de rede do cliente reside num grupo de limites que está ativada para atribuição de sites, ou a hierarquia está configurada para um site de contingência, o cliente é automaticamente atribuído a esse site sem que o operador precise de especificar um código de site.  

 Pode configurar limites utilizando um ou mais dos seguintes procedimentos:  

-   Sub-rede IP  

-   Site do Active Directory  

-   Prefixo IP v6  

-   Intervalo de endereços IP  

> [!NOTE]  
>  Se um cliente do Gestor de Configuração tiver vários adaptadores de rede e, portanto, tiver vários endereços IP, o endereço IP utilizado para avaliar a atribuição do site do cliente é atribuído aleatoriamente.  

 Para obter informações sobre como configurar grupos de limites para a atribuição do site e como configurar um site de backback para atribuição automática do site, consulte definir os limites do [site e os grupos de fronteira para O Gestor](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)de Configuração .  

 Os clientes do Gestor de Configuração que usam a tarefa automática do site tentam encontrar grupos de limites do site que são publicados nos Serviços de Domínio do Diretório Ativo. Se isso falhar (por exemplo, o esquema de Diretório Ativo não é estendido para O Gestor de Configuração, ou os clientes são computadores de grupo de trabalho), os clientes podem obter informações de grupo de limites a partir de um ponto de gestão.  

 Pode especificar um ponto de gestão para ser utilizado pelos computadores cliente após serem instalados ou os clientes podem localizar um ponto de gestão utilizando a publicação de DNS ou WINS.  

 Se o cliente não conseguir encontrar um site que esteja associado a um grupo de limites que contenha a respetiva localização de rede e caso a hierarquia não disponha de um site de contingência, o cliente tentará novamente de 10 em 10 minutos até conseguir ser atribuído a um site.  

 Os computadores clientes do Gestor de Configuração não podem ser automaticamente atribuídos a um site se algum dos seguintes se aplicar, e então devem ser atribuídos manualmente:  

-   Estão atualmente atribuídos a um site.  

-   Encontram-se na Internet ou configurados como clientes apenas de Internet.  

-   A respetiva localização de rede não coincide com nenhum dos grupos de limites configurados na hierarquia do Configuration Manager e não existe nenhum site de contingência para a hierarquia.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>A concluir a atribuição de site através da verificação da compatibilidade do site  
 Depois de um cliente ter encontrado o seu site atribuído, a versão e o sistema operativo do cliente são verificados para garantir que um site do Gestor de Configuração o possa gerir. Por exemplo, o Gestor de Configuração não pode gerir clientes do Gestor de Configuração 2007, clientes do System Center 2012, ou clientes que estão a executar o Windows 2000.  

 A atribuição do site falha se atribuir um cliente que executa o Windows 2000 num site do Gestor de Configuração. Ao atribuir um cliente de Configuração 2007 ou um cliente do System Center 2012 para um site de Gestor de Configuração (filial atual), a atribuição do site consegue suportar a atualização automática do cliente. No entanto, até que os clientes de geração mais velha sejam atualizados para um cliente de Gestor de Configuração (filial atual), o Gestor de Configuração não pode gerir este cliente utilizando configurações, aplicações ou atualizações de software do cliente.  

> [!NOTE]  
>  Para apoiar a atribuição do site de um Gestor de Configuração 2007 ou de um cliente do System Center 2012 para um site de Gestor de Configuração (filial atual), deve configurar o upgrade automático do cliente para a hierarquia. Para mais informações, consulte como [atualizar os clientes para computadores Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

O Gestor de Configuração também verifica se atribuiu o cliente do Gestor de Configuração (filial atual) a um site que o suporta. Os seguintes cenários podem ocorrer durante a migração de versões anteriores do Gestor de Configuração.  

- Cenário: Utilizou a atribuição automática do site e os seus limites sobrepõem-se aos definidos numa versão anterior do Gestor de Configuração.  

   Neste caso, o cliente tenta automaticamente encontrar um site de Gestor de Configuração (filial atual).  

   O cliente verifica primeiro os Serviços de Domínio do Diretório Ativo e se encontrar um site de Gestor de Configuração (filial atual) publicado, a atribuição do site é bem sucedida. Se isso falhar (por exemplo, o site do Gestor de Configuração não é publicado ou o computador é um cliente de grupo de trabalho), o cliente verifica então as informações do site a partir do seu ponto de gestão atribuído.  

  > [!NOTE]  
  >  Pode atribuir um ponto de gestão ao cliente durante a instalação do cliente utilizando a propriedade Client.msi **&lt;SMSMP= server_name>**.  

   Se ambos estes métodos falharem, a atribuição do site não terá êxito e deverá atribuir manualmente o cliente.  

- Cenário: Atribuiu o cliente do Gestor de Configuração (filial atual) utilizando um código de site específico em vez de uma atribuição automática do site, e especificou erradamente um código de site para uma versão do Gestor de Configuração mais cedo do que o System Center 2012 R2 Configuration Manager.  

   Neste caso, a atribuição do site falha e tem de reatribuir manualmente o cliente a um site do Gestor de Configuração (filial atual).  

  A verificação de compatibilidade do site requer uma das seguintes condições:  

- O cliente consegue aceder às informações do site publicadas nos Serviços de Domínio do Active Directory.  

- O cliente consegue comunicar com um ponto de gestão do site.  

  Se a verificação de compatibilidade do site não terminar com sucesso, a atribuição do site falha e o cliente permanece ingerido até que a verificação de compatibilidade do site volte a ser e tenha sucesso.  

  A exceção à realização da verificação de compatibilidade do site ocorre quando um cliente se encontra configurado para um ponto de gestão baseado na Internet. Neste caso, não é feita qualquer verificação de compatibilidade do site. Se estiver a atribuir clientes a um site que contém sistemas de sites baseados na Internet e especificar um ponto de gestão baseado na Internet, certifique-se de que está a atribuir o cliente ao site correto. Se atribuir erradamente o cliente a um site do Gestor de Configuração de 2007, a um site do System Center 2012 Configuration Manager ou a um site do Gestor de Configuração que não tenha funções de sistema de site baseados na Internet, o cliente será desgerido.  

##  <a name="locating-management-points"></a>Localizar pontos de gestão  
 Quando um cliente é atribuído com êxito a um site, localiza um ponto de gestão nesse site.  

 Os computadores clientes descarregam uma lista de pontos de gestão aos quais podem ligar-se no site. Isto acontece sempre que o cliente reinicia, ou a cada 25 horas, ou se o cliente detetar uma mudança de rede, como desligar e reconectar o computador na rede ou receber um novo endereço IP. A lista inclui os pontos de gestão na intranet e a indicação de que aceitam ligações de cliente através de HTTP ou HTTPS. Quando o computador cliente está na Internet e o cliente ainda não tem uma lista de pontos de gestão, ele conecta-se ao ponto de gestão baseado na Internet especificado para obter uma lista de pontos de gestão. Se o cliente dispuser de uma lista de pontos de gestão para o respetivo site atribuído, selecionará um ponto para estabelecer a ligação:  

-   Quando o cliente se encontra na intranet e dispõe de um certificado PKI válido que pode utilizar, o cliente escolhe os pontos de gestão HTTPS antes dos pontos de gestão HTTP. Em seguida, localiza o ponto de gestão mais próximo, com base na respetiva associação de floresta.  

-   Quando o cliente está na Internet, escolhe aleatoriamente um dos pontos de gestão baseados na Internet.  

Os clientes de dispositivos móveis que são matriculados pelo Gestor de Configuração apenas se conectam a um ponto de gestão no seu site atribuído e nunca se ligam a pontos de gestão em sites secundários. Estes clientes ligam-se sempre através de HTTPS e o ponto de gestão tem de ser configurado para aceitar ligações de cliente através da Internet. Quando há mais de um ponto de gestão para clientes de dispositivos móveis no site principal, o Gestor de Configuração escolhe aleatoriamente um destes pontos de gestão durante a atribuição e o cliente de dispositivomóvel continua a usar o mesmo ponto de gestão.  

Se o cliente tiver transferido a política de cliente a partir de um ponto de gestão do site, o cliente torna-se um cliente gerido.  

##  <a name="downloading-site-settings"></a>A transferir as definições do site  
 Após a atribuição do site com êxito e o cliente ter encontrado um ponto de gestão, um computador cliente que utilize os Serviços de Domínio do Active Directory para a respetiva verificação de compatibilidade com um site transfere as definições de site relacionadas com o cliente para o respetivo site atribuído. Estas definições incluem os critérios de seleção de certificado de cliente, de utilização de uma lista de revogação de certificados e os números de porta para pedidos de cliente. O cliente continuará a verificar periodicamente estas definições.  

 Quando os computadores cliente não conseguem obter as definições a partir dos Serviços de Domínio do Active Directory, transferem-nos a partir do respetivo ponto de gestão. Os computadores clientes também podem obter as definições do site quando são instaladas utilizando o impulso do cliente, ou pode especificá-las manualmente utilizando propriedades de instalação CCMSetup.exe e cliente. Para mais informações sobre as propriedades de instalação do cliente, consulte sobre as propriedades de [instalação do cliente.](../../../core/clients/deploy/about-client-installation-properties.md)  

##  <a name="downloading-client-settings"></a>A transferir as definições do cliente  
 Todos os clientes transferem a política de predefinições de cliente, bem como outras políticas personalizadas de definições de cliente aplicáveis. O Centro de Software baseia-se nestas políticas de configuração de clientes para os computadores com Windows e notificará os utilizadores de que não será possível executar o Centro de Software com êxito enquanto estas informações de configuração estiverem a ser transferidas. Dependendo das definições de cliente configuradas, a transferência inicial das definições de cliente poderão demorar algum tempo e algumas tarefas de gestão de clientes poderão não ser executadas até que este processo esteja concluído.  

##  <a name="verifying-site-assignment"></a>Verificar a atribuição de sites  
 Pode verificar o sucesso da atribuição do local por qualquer um dos seguintes métodos:  

-   Para os clientes dos computadores Windows, utilize o Gestor de Configuração no Painel de Controlo e verifique se o código do site está corretamente apresentado no separador **Site.**  

-   Para computadores clientes, no espaço de trabalho **de Ativos e Compliance** > Nó de **Dispositivos,** verifique se o computador exibe **Sim** para a coluna **Cliente** e o código de site primário correto para a coluna Código do **Site.**  

-   Para clientes de dispositivos móveis, na área de trabalho **Ativos e Compatibilidade** , utilize a coleção **Todos os Dispositivos Móveis** para verificar se o dispositivo móvel apresenta **Sim** na coluna **Cliente** e o código do site primário correto na coluna **Código do Site** .  

-   Utilize os relatórios para a atribuição de clientes e a inscrição do dispositivo móvel.  

-   Para computadores cliente, utilize o ficheiro LocationServices.log no cliente.  

##  <a name="roaming-to-other-sites"></a>Itinerância para outros sites  
 Quando os computadores cliente da intranet são atribuídos a um site primário, mas a localização da rede é alterada para ficarem incluídos num grupo de limites configurado para outro site, estes foram movidos para outro site. Quando este site é um site secundário do respetivo site atribuído, os clientes podem utilizar um ponto de gestão no site secundário para transferir a política de cliente e carregar dados do cliente, o que evita o envio destes dados através de uma rede potencialmente lenta. Porém, se estes clientes se moverem para os limites de outro site primário ou de um site secundário que não é um site subordinado do respetivo site atribuído, estes clientes utilizam sempre um ponto de gestão no seu site atribuído para transferir a política de cliente e carregar dados para o respetivo site.  

 Estes computadores cliente que se movem para outros sites (todos os sites primários e todos os sites secundários) podem sempre utilizar pontos de gestão noutros sites para pedidos de localização de conteúdo. Os pontos de gestão do site atual podem proporcionar aos clientes uma lista dos pontos de distribuição que possuem o conteúdo solicitados pelos clientes.  

 Para computadores clientes que estejam configurados para gestão de clientes apenas na Internet, e para dispositivos móveis e computadores Mac que estão matriculados pelo Gestor de Configuração, estes clientes apenas comunicam com pontos de gestão no seu site designado. Estes clientes nunca comunicam com pontos de gestão de sites secundários nem com pontos de gestão de outros sites primários.  
