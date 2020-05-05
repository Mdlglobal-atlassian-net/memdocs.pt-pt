---
title: Suporte para o servidor proxy
titleSuffix: Configuration Manager
description: Saiba como os servidores do sistema do Gestor de Configuração utilizam servidores proxy.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5581214dd786bdefd29d0e4d2626de536ad26ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718715"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Suporte do servidor proxy no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Alguns servidores do sistema do Gestor de Configuração requerem ligações à internet. Se o seu ambiente necessitar de tráfego de internet para utilizar um servidor proxy, configure estas funções do sistema do site para usar o proxy.  

- Um computador que acolhe um servidor de sistema de site suporta uma configuração de servidor proxy única. Todas as funções do sistema do site nesse computador partilham esta mesma configuração de procuração. Se necessitar de servidores proxy separados para diferentes funções ou instâncias de uma função, coloque essas funções em servidores separados do sistema do site.  

- Quando configura novas definições de servidor proxy para um servidor de sistema de site que já tem uma configuração de servidor proxy, a configuração original é sobreescrita.  

- Por predefinição, as ligações ao proxy utilizam a conta **System** do computador que acolhe a função do sistema do site.  

- Se a conta de computador não conseguir autenticar, o servidor do sistema do site pode armazenar credenciais de utilizador para se ligar ao servidor proxy. Estas credenciais são a conta de servidor proxy do **sistema de site**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Funções do sistema do site que usam um proxy

As seguintes funções do sistema do site conectam-se à internet e, se necessário, podem utilizar um servidor proxy:  

### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence

Esta função do sistema do site liga-se à Microsoft e utiliza uma configuração de servidor proxy no computador que acolhe o ponto de sincronização da Inteligência de Ativos.  

### <a name="cloud-distribution-point"></a>Ponto de distribuição em nuvem

A função do ponto de distribuição na nuvem é no Microsoft Azure. Não configura este papel do sistema do site para usar um representante. Detete a configuração proxy no servidor do site primário que gere o ponto de distribuição da nuvem.  

Para esta configuração, o servidor do site primário:  

- Deve ser capaz de ligar ao Microsoft Azure para configurar, monitorizar e distribuir conteúdo para o ponto de distribuição da nuvem.  

- Por predefinição, utiliza a conta **System** do computador para efazer a ligação. Também pode utilizar a conta proxy do sistema do site, se necessário.  

- Utiliza APIs do navegador web do Windows.  

### <a name="distribution-point"></a>Ponto de distribuição

<!-- 5856396 -->

A partir da versão 2002, se ativar um ponto de distribuição do Gestor de Configuração para o Microsoft Connected Cache, pode comunicar através de um servidor proxy não autenticado para acesso à Internet. Para mais informações, consulte [o Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>Conector do Exchange Server

Esta função do sistema do site liga-se a um Servidor de Intercâmbio. Utiliza uma configuração de servidor proxy no computador que acolhe o conector Exchange Server.  

### <a name="service-connection-point"></a>Ponto de ligação de serviço

Esta função do sistema do site liga-se ao serviço cloud do Gestor de Configuração para descarregar atualizações de versão para O Gestor de Configuração. Usa um servidor proxy configurado no computador que acolhe o ponto de ligação de serviço.  

### <a name="software-update-point"></a>Ponto de atualização de software

Esta função do sistema do site utiliza o proxy quando se conecta ao Microsoft Update para descarregar patches e sincronizar informações sobre atualizações. Como todas as outras funções do sistema do site, primeiro configurar as definições de proxy do sistema do site. Em seguida, configure as seguintes opções específicas ao ponto de atualização do software:  

- **Utilizar um servidor proxy para sincronizar atualizações de software**  

- **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática**  

    > [!NOTE]
    > Embora esteja disponível para utilização, esta definição não é utilizada por pontos de atualização de software em sites secundários.  

Estas definições estão no **separador Proxy e Definições** de Conta das propriedades do ponto de atualização do software.  

> [!NOTE]
> Por padrão, quando as regras de implementação automática saem, a conta **System** no servidor do site em que foi criada uma regra de implementação automática é usada para ligar à internet e descarregar atualizações de software. Em alternativa, configure e utilize a conta de servidor proxy do sistema do site. 
>
> Quando esta conta não consegue aceder à internet, as atualizações de software não conseguem descarregar. A seguinte entrada é registada para **ruleengine.log:**  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a>Outras funcionalidades que usam o proxy para um servidor de sistema de site

*(Introduzido na versão 2002)*

A partir da versão de 2002 do Gestor de Configuração, as seguintes funcionalidades utilizam o proxy do sistema de site que acolhe a função de ponto de ligação ao [serviço:](#service-connection-point) <!--5913817-->

- [Descoberta de utilizadores do Azure Ative Directory (Azure AD)](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Descoberta do grupo de utilizadores da AD Azure](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Sincronização de resultados de adesão à coleção para grupos de Diretórios Ativos Azure](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Configure o proxy para um servidor de sistema de site  

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **configuração**do site e, em seguida, selecionar o nó de **Funções de Servidores e Do Sistema do Site.**  

2. Selecione o servidor do sistema do site que pretende editar. No painel de detalhes, clique à direita na função do **sistema do Site** e selecione **Propriedades**.  

3. No sistema do Site Propriedades, mude para o **separador Proxy.** Configure as seguintes definições de procuração:  

    - **Utilize um servidor proxy ao sincronizar informações a partir da internet**: Selecione esta opção para permitir que o servidor do sistema do site utilize um servidor proxy.  

    - **Nome**do servidor proxy : Especifique o nome de anfitrião ou FQDN do servidor proxy no seu ambiente.  

    - **Porta**: Especifique a porta de rede para comunicar com o servidor proxy. Por defeito, utiliza a porta **80**.  

    - **Utilize credenciais para se ligar ao servidor proxy**: Muitos servidores proxy requerem que um utilizador autentime. Por padrão, o servidor do sistema do site utiliza a sua conta de computador para se ligar ao servidor proxy. Se necessário, ative esta opção, clique em **Definir**, e depois escolha uma **Conta Existente** ou especifique uma **Nova Conta**. Estas credenciais são a conta de servidor proxy do **sistema de site**.  Para mais informações, consulte [contas utilizadas no Gestor](../hierarchy/accounts.md)de Configuração .  

4. Escolha **OK** para salvar a nova configuração do servidor proxy.  
