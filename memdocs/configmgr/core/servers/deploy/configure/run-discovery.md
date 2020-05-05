---
title: Descubra os recursos do dispositivo e do utilizador
titleSuffix: Configuration Manager
description: Leia uma visão geral do processo de descoberta e dos registos de dados de descoberta.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718372"
---
# <a name="run-discovery-for-configuration-manager"></a>Executar descoberta para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utiliza um ou mais métodos de descoberta no Gestor de Configuração para encontrar dispositivos e recursos de utilizador que possa gerir. Também pode usar a descoberta para identificar infraestruturas de rede no seu ambiente. Existem vários métodos diferentes que pode usar para descobrir coisas diferentes, e cada método tem as suas próprias configurações e limitações.  

## <a name="overview-of-discovery"></a>Descrição geral do processo de deteção  
 Discovery é o processo pelo qual o Gestor de Configuração aprende sobre as coisas que pode gerir. Seguem-se os métodos de deteção disponíveis:  

-   Deteção de Florestas do Active Directory  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

-   Deteção de Heartbeat  

-   Deteção de Redes  

-   Deteção de Servidores  

> [!TIP]  
>  Você pode aprender sobre os métodos de descoberta individuais em [métodos de descoberta para configuração manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Para obter assistência na seleção de quais os métodos a utilizar e em que sites da sua hierarquia, consulte Métodos de descoberta Select para utilizar para O Gestor de [Configuração](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para utilizar a maioria dos métodos de descoberta, deve ativar o método num site e instalá-lo para pesquisar localizações específicas de rede ou Diretório Ativo. Quando funciona, consulta a localização especificada para obter informações sobre dispositivos ou utilizadores que o Gestor de Configuração pode gerir. Quando um método de descoberta encontra com sucesso informações sobre um recurso, coloca essa informação num ficheiro chamado registo de dados de descoberta (DDR). Este ficheiro é então processado por um site de administração primária ou central. O processamento de um DDR cria um novo registo na base de dados do site para os recursos detetados recentemente ou atualiza os registos existentes com as novas informações.  

 Alguns métodos de descoberta podem gerar um grande volume de tráfego de rede, e os DDRs que produzem podem resultar numa utilização significativa dos recursos cpu durante o processamento. Por isso, planeie usar apenas os métodos de descoberta que precisa para cumprir os seus objetivos. Pode utilizar apenas um ou dois métodos de deteção e, posteriormente, ativar métodos adicionais de forma controlada para expandir o nível de deteção no ambiente.  

 Após a descoberta da informação ser adicionada à base de dados do site, a informação replica-se então a cada site na hierarquia, independentemente do local onde foi descoberta ou processada. Portanto, enquanto você pode configurar diferentes horários e configurações para métodos de descoberta em diferentes sites, você pode executar um método de descoberta específico em apenas um único site. Isto reduz o uso da largura de banda da rede através de ações de descoberta duplicadas, e reduz o processamento de dados de descoberta redundantes em vários sites.  

 Você pode usar dados de descoberta para criar coleções e consultas personalizadas que logicamente agrupam recursos para tarefas de gestão. Por exemplo:  

-   Empurrando as instalações dos clientes, ou melhorando.  

-   Implementação de conteúdos para utilizadores ou dispositivos.  

-   Implementando as configurações do cliente e configurações relacionadas.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a>Sobre os registos de dados de descoberta  
 DDRs são ficheiros criados por um método de descoberta. Contêm informações sobre um recurso que pode gerir no Gestor de Configuração, como computadores, utilizadores e, em alguns casos, infraestrutura de rede. São processados em sites primários ou em sites de administração central. Após a entrada da informação sobre os recursos no DDR na base de dados, o DDR é eliminado e a informação replica-se como dados globais para todos os sites da hierarquia.  

 O site onde um DDR é processado depende das informações que contém:  

-   Os DDRs para recursos recém-descobertos que não estão na base de dados são processados no local de alto nível da hierarquia. O site de alto nível cria um novo registo de recursos na base de dados, e atribui-lhe um identificador único. Os DDRs transferem-se por replicação baseada em ficheiros até chegarem ao site de alto nível.  

-   Os DDR de objetos detetados anteriormente são processados em sites primários. Os sites primários subordinados não transferem DDRs para o site de administração central quando o DDR contém informações sobre um recurso que já se encontra na base de dados.  

-   Os sites secundários não processam DDRs e transferem-nos sempre por replicação baseada em ficheiros para o seu local primário principal.  

Os ficheiros DDR são identificados pela extensão .ddr e têm um tamanho típico de cerca de 1 KB.  

## <a name="get-started-with-discovery"></a>Introdução ao processo de deteção:  
 Antes de utilizar a consola Do Gestor de Configuração para configurar a descoberta, deve compreender as diferenças entre os métodos, o que podem fazer e, para alguns, as suas limitações.  

Os seguintes tópicos podem construir uma fundação que o ajudará a usar métodos de descoberta com sucesso:  

-   [Sobre métodos de descoberta para Gestor de Configuração](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selecione métodos de descoberta para o Gestor de Configuração](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Depois, quando compreender os métodos que pretende utilizar, encontre orientações para configurar cada método em métodos de [deteção de Configuração para O Gestor](../../../../core/servers/deploy/configure/configure-discovery-methods.md)de Configuração .  
