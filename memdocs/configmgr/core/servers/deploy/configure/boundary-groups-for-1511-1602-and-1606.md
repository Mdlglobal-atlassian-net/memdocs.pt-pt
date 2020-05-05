---
title: Grupos de fronteira para 1511, 1602 e 1606
titleSuffix: Configuration Manager
description: Utilize grupos de limites com as versões 1511, 1602 e 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721109"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Grupos de limites para configuração manager versão 1511, 1602 e 1606

*Aplica-se a: Gestor de Configuração (ramo atual)*
<!-- This topic drops from TOC with the release of version 1706 -->

A informação neste tópico é específica para usar grupos de fronteira com as versões 1511, 1602 e 1606 do Gestor de Configuração.
Se utilizar a versão 1610 ou mais tarde, consulte os grupos de [fronteira configure](boundary-groups.md) para obter informações sobre como utilizar os grupos de fronteira redesenhados.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a>Grupos de fronteira  
 Pode criar grupos de limites para agrupar logicamente as localizações de rede relacionadas (limites) para facilitar a gestão da sua infraestrutura. Para poder utilizar o grupo de limites, tem de atribuir os limites a grupos de limites. Os clientes utilizam a configuração do grupo de limites para:  

-   Atribuição automática de site  

-   Localização de conteúdo  

-   Pontos de gestão preferenciais

    Se utilizar pontos de gestão preferidos, deve ativar esta opção para a hierarquia e não a partir da configuração do grupo de limites. Consulte o *Procedimento de Pontos de Gestão preferenciais* mais tarde neste tópico.  

Quando se cria grupos de fronteira, adiciona-se um ou mais limites ao grupo de fronteiras. Em seguida, configura configura configurar configurações adicionais para utilização por clientes que estão localizados nesses limites.  

#### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  

1.  Na consola de Configuração Manager, escolha >  **Grupos de Limite**de Configuração da Hierarquia da **Administração** > **Hierarchy Configuration**.  

2.  No separador **Home,** no grupo **Criar,** escolha **Criar O Grupo Limite**.  

3.  Na caixa de diálogo do **Grupo Criar** Limites, escolha o separador **Geral** e, em seguida, introduza um **Nome** para este grupo de fronteira.  

4.  Escolha **OK** para salvar o novo grupo de fronteiras.  

#### <a name="to-set-up-a-boundary-group"></a>Para criar um grupo de fronteiras  

1.  Na consola de Configuração Manager, escolha >  **Grupos de Limite**de Configuração da Hierarquia da **Administração** > **Hierarchy Configuration**.  

2.  Escolha o grupo de fronteiras que quer mudar.  

3.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

4.  Na caixa de diálogo **Properties** para o grupo de fronteira, escolha o separador **Geral** para alterar os limites que são membros deste grupo de fronteira:  

    -   Para adicionar limites, escolha **Adicionar,** verifique a caixa de verificação por um ou mais limites e, em seguida, escolha **OK**.  

    -   Para remover os limites, selecione o limite e, em seguida, escolha **Remover**.  

5.  Escolha o separador **Referências** para alterar a atribuição do site e a configuração do servidor do servidor do site associado:  

    -   Para permitir que este grupo de limites seja utilizado pelos clientes para a atribuição do site, verifique a caixa de verificação para **utilizar este grupo de limites para a atribuição**do site, e, em seguida, escolha um site da caixa de dropdown do site **atribuído.**  

    -   Para configurar os servidores do sistema de site disponíveis que estão associados a este grupo de fronteira:  

    1.  Escolha **adicionar**e, em seguida, verifique se a caixa de verificação tem um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limites. Só estão disponíveis os servidores que têm a função de sistema de sites instalada.  

        > [!NOTE]  
        >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Os sistemas de sites selecionados são listados no separador **Sistemas de Sites** nas propriedades de cada limite que seja membro deste grupo de limites.  

    2.  Para remover um servidor deste grupo de limites, escolha o servidor e, em seguida, escolha **Remover**.  

        > [!NOTE]  
        >  Para parar a utilização deste grupo de limites para associar sistemas de site, deve remover todos os servidores listados como servidores de sistema de site associados.  

    3.  Para alterar a velocidade de ligação da rede para um servidor de sistema de site para este grupo de fronteira, escolha o servidor e, em seguida, escolha **change Connection**.  

         Por predefinição, a velocidade de ligação de cada sistema de site é **Rápida,** mas pode alterar a velocidade para **Slow**. A velocidade da ligação de rede e a configuração de uma implementação determinam se um cliente pode transferir conteúdo do servidor.  

6.  Escolha **OK** para fechar as propriedades do grupo de fronteira e salvar a configuração.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para associar um servidor de implementação de conteúdo ou ponto de gestão a um grupo de limites  

1.  Na consola de Configuração Manager, escolha >  **Grupos de Limite**de Configuração da Hierarquia da **Administração** > **Hierarchy Configuration**.  

2.  Escolha o grupo de fronteiras que quer mudar.  

3.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

4.  Na caixa de diálogo **Properties** para o grupo de limites, escolha o separador **Referências.**  

5.  Em **seletos servidores**do sistema do site, escolha **Adicionar,** verifique a caixa de verificação dos servidores do sistema do site que pretende associar a este grupo de limites e, em seguida, escolha **OK**.  

6.  Escolha **OK** para fechar a caixa de diálogo e guardar a configuração do grupo de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para ativar a utilização de pontos de gestão preferenciais  

1.  Na consola do Gestor de Configuração, escolha**os Sites**de**Configuração** > do Site **da Administração** > e, em seguida, no separador **Home,** escolha **definições de hierarquia**.  

2.  No separador **Geral** das **Definições**da Hierarquia, escolha **clientes que prefiram utilizar pontos de gestão especificados em grupos de fronteiras**.  

3.  Escolha **OK** para fechar a caixa de diálogo e guardar a configuração.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Para criar um site de backback para atribuição automática do site  

1. Na consola de Gestor de Configuração, escolha**sites**de**configuração** >  do site **da administração** > .  

2. No separador **Home,** no grupo **Sites,** escolha **Definições de Hierarquia**.  

3. No separador **Geral,** verifique a caixa de verificação para **utilizar um site**de recuo e, em seguida, escolha um site na lista de drop-down do site **Fallback.**  

4. Escolha **OK** para salvar a configuração.  

   As secções seguintes fornecem detalhes adicionais sobre as configurações de grupos de limites.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a>Sobre a atribuição do site  
 Pode configurar cada grupo de fronteiracom um site atribuído aos clientes.  

-   Um cliente recém-instalado que utiliza a atribuição automática do site juntar-se-á ao site atribuído de um grupo de fronteira que tem a localização atual da rede do cliente.  

-   Um cliente que é atribuído a um site não altera a sua atribuição do site quando o cliente muda a sua localização de rede. Por exemplo, se o cliente vaguear por uma nova localização de rede que é representada por um limite num grupo de fronteira seletiva que tem uma atribuição de site diferente, o site designado pelo cliente permanecerá inalterado.  

-   Quando a Deteção de Sistemas do Active Directory deteta um novo recurso, as informações de rede do recurso detetado são comparadas com os limites dos grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  

-   Quando um limite é membro de vários grupos de fronteira que têm diferentes sites atribuídos, os clientes selecionam aleatoriamente um dos sites.  

-   As alterações ao site atribuído a um grupo de fronteira aplicam-se apenas a novas ações de atribuição do site. Os clientes que foram previamente atribuídos a um site não avaliam novamente a sua atribuição do site com base em alterações na configuração de um grupo de fronteira (ou na sua própria localização de rede).  

Para mais informações sobre a atribuição do site do cliente, consulte [a utilização da Atribuição Automática de Sites para Computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Acerca da localização de conteúdo  
 Você pode configurar cada grupo de fronteiracom um ou mais pontos de distribuição e pontos de migração do Estado, e você pode associar os mesmos pontos de distribuição e pontos de migração do estado com vários grupos de fronteira.  

-   **Durante a distribuição de software**, os clientes solicitam uma localização para o conteúdo de implementação. O Gestor de Configuração envia ao cliente uma lista de pontos de distribuição que estão associados a cada grupo de fronteiras que inclui a localização atual da rede do cliente.  

-   **Durante a implantação do sistema operativo,** os clientes solicitam um local para enviar ou receber as suas informações de migração do Estado. O Gestor de Configuração envia ao cliente uma lista de pontos de migração do Estado que estão associados a cada grupo de fronteiras que inclui a localização atual da rede do cliente.  

Este comportamento permite ao cliente selecionar o servidor mais próximo a partir do qual transferir o conteúdo ou informações de migração do Estado.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Acerca dos pontos de gestão preferenciais  
 Os pontos de gestão preferenciais permitem que um cliente identifique um ponto de gestão que esteja associado à sua localização atual de rede (limite).  

-   Um cliente tenta utilizar um ponto de gestão preferido do seu site designado antes de utilizar um ponto de gestão do seu site designado que não está configurado como preferido.  

-   Para utilizar esta opção, deve ensiá-la para a hierarquia e criar grupos de fronteira em locais primários individuais para incluir os pontos de gestão que devem ser associados aos limites associados desse grupo de fronteiras  

-   Quando são criados pontos de gestão preferenciais e um cliente organiza a sua lista de pontos de gestão, o cliente coloca os pontos de gestão preferidos no topo da sua lista de pontos de gestão atribuídos, que inclui todos os pontos de gestão do site designado pelo cliente.  

> [!NOTE]  
>  Quando um cliente vagueia, como quando um portátil viaja para um local de escritório remoto e muda a sua localização de rede, pode utilizar um ponto de gestão (ou ponto de gestão de procuração) do site local na sua nova localização antes de tentar utilizar um ponto de gestão a partir do seu site designado (que inclui os pontos de gestão preferidos).  [Veja como os clientes encontram recursos e serviços](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) do site para O Gestor de Configuração para mais informações.  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a>Sobre sobrepor fronteiras  
 O Gestor de Configuração suporta configurações de limites sobrepostas para a localização do conteúdo:  

-   **Quando um cliente solicita conteúdo**, e a localização da rede de clientes pertence a vários grupos de limites, o Gestor de Configuração envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  

-   **Quando um cliente solicita a um servidor que envie ou receba as suas informações**de migração do Estado , e a localização da rede de clientes pertence a vários grupos de fronteira, o Gestor de Configuração envia ao cliente uma lista de todos os pontos de migração do Estado que estão associados a um grupo de fronteiras que inclui a localização atual da rede do cliente.  

Este comportamento permite ao cliente selecionar o servidor mais próximo a partir do qual transferir o conteúdo ou informações de migração do Estado.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a>Sobre a velocidade de ligação da rede  
 Pode definir a velocidade de ligação da rede para cada servidor do sistema de site num grupo de limites. Esta definição aplica-se a clientes que se ligam a um sistema de site com base na configuração deste grupo de fronteira. O mesmo servidor do sistema de sites pode ter uma velocidade de ligação diferente definida em diferentes grupos de limites.  

 Por predefinição, a velocidade de ligação da rede está definida para **Fast**, mas pode mudá-la para **Slow**. A velocidade de ligação da rede e a configuração de implementação verificam se um cliente pode descarregar conteúdo a partir de um ponto de distribuição quando o cliente está num grupo de limites associado.  

 Para saber mais sobre como a configuração da velocidade de ligação à rede afeta a forma como os clientes obtêm conteúdo, consulte [cenários](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md)de localização de fonte de conteúdo .  
