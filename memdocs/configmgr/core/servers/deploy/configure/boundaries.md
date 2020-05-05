---
title: Definir limites
titleSuffix: Configuration Manager
description: Compreenda como definir as localizações da rede na sua intranet que podem conter dispositivos que pretende gerir.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721116"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Defina as localizações da rede como limites para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os limites do Gestor de Configuração são localizações na sua rede que contêm dispositivos que pretende gerir. O limite em que um dispositivo se encontra é equivalente ao site Ative Directory, ou endereço IP de rede identificado pelo cliente Do Gestor de Configuração que está instalado no dispositivo.
- Pode criar manualmente limites individuais. No entanto, o Gestor de Configuração não suporta a entrada direta de uma supernet como um limite. Em vez disso, utilize o tipo de limite de intervalo de endereços IP.
- Pode configurar o método [Ative Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) para descobrir e criar limites para cada Subnet IP e Ative Directory Site que descobre. Quando o Ative Directory Forest Discovery identifica uma supernet que é atribuída a um site de Diretório Ativo, o Gestor de Configuração converte a supernet num limite de alcance de endereçoIP.  

Não é incomum que um dispositivo utilize um endereço IP que o administrador do Gestor de Configuração não tenha conhecimento. Quando a localização da rede de um dispositivo estiver em dúvida, confirme o que o dispositivo reporta como a sua localização utilizando o comando **IPCONFIG** no dispositivo.  

Quando cria um limite, este recebe automaticamente um nome baseado no tipo e no âmbito do limite. Não é possível modificar este nome. Em vez disso, pode especificar uma descrição para ajudar a identificar o limite na consola do Gestor de Configuração.  

Cada limite está disponível para ser usado por todos os sites da sua hierarquia. Depois de criado um limite, pode modificar as suas propriedades para fazer o seguinte:  
- Adicionar o limite a um ou mais grupos de limites.  
- Alterar o tipo ou o âmbito do limite.  
- Consulte o separador **Sistemas de Sites** dos limites para verificar que servidores do sistema de sites (pontos de distribuição, pontos de migração de estado e pontos de gestão) estão associados ao limite.  

## <a name="to-create-a-boundary"></a>Para criar um limite  

1.  Na consola de Gestor de Configuração, clique nos**limites** de**configuração** > da hierarquia da **administração** >   

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Boundary**.  

3.  No separador **Geral** da caixa de diálogo Criar Limites, é possível especificar uma **Descrição** para identificar o limite através de um nome amigável ou de uma referência.  

4.  Selecione um **Tipo** para este limite:  

    - Se selecionar **Sub-rede IP**, tem de especificar um **ID de Sub-rede** para este limite.  
      > [!TIP]  
      > Pode especificar a **Rede** e a **Máscara de sub-rede** para que o **ID de Sub-rede** seja especificado automaticamente. Ao guardar o limite, apenas é guardado o valor do ID de Sub-rede.  

    - Se selecionar **site do Active Directory**, tem de especificar ou **Procurar** um site do Active Directory na floresta local do servidor do site.  
        
      - Quando especifica um site do Active Directory para um limite, o limite inclui cada Sub-rede de IP que é membro desse site do Active Directory. Se a configuração do site Active Directory for alterada no Active Directory, as localizações de rede incluídas neste limite também são alteradas.  

      - Os limites do site Ative Directy não funcionam para clientes azureAd puros. Se vaguearem no local, não cairão em qualquer limite se apenas forem definidos através de Sites AD.

    - Se selecionar **prefixo IPv6**, tem de especificar um **Prefixo** no formato de prefixo IPv6.  

    - Se selecionar **Intervalo de endereços IP**, tem de especificar um **Endereço IP inicial** e um **Endereço IP final** que incluam parte de uma Sub-rede de IP ou várias Sub-redes IP.    

5.  Clique em **OK** para guardar o novo limite.  

## <a name="to-configure-a-boundary"></a>Para configurar um limite  

1.  Na consola de Gestor de Configuração, clique nos**limites** de**configuração** > da hierarquia da **administração** >   

2.  Selecione o limite que pretende modificar.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do limite, selecione o separador **Geral** para editar a **Descrição** ou o **Tipo** do limite. Também pode alterar o âmbito de um limite, editando as suas localizações de rede. Por exemplo, para o limite de um site do Active Directory, pode especificar um novo nome de site do Active Directory.  

5.  Selecione o separador **Sistemas de Sites** para visualizar os sistemas de sites associados a este limite. Não é possível alterar esta configuração a partir das propriedades de um limite.  

    > [!TIP]  
    > Para que um servidor do sistema de sites seja apresentado como um sistema de sites para um limite, o servidor do sistema de sites tem de estar associado como um servidor do sistema de sites a, pelo menos, um grupo de limites que inclua este limite. Isto é configurado no separador **Referências** de um grupo de limites.  

6.  Selecione o separador **Grupos de Limites** para modificar a associação do grupo de limites para este limite:  

    - Para adicionar este limite a um ou mais grupos de limites, clique em **Adicionar**, selecione a caixa de verificação de um ou mais grupos de limites e clique em **OK**.  

    - Para remover este limite de um grupo de limites, selecione o grupo de limites e clique em **Remover**.  

7.  Clique em **OK** para fechar as propriedades do limite e guardar a configuração.  
