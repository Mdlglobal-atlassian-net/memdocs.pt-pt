---
title: Websites para sistemas de sites
titleSuffix: Configuration Manager
description: Saiba mais sobre sites padrão e personalizados para servidores de sistema de site no Gestor de Configuração.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 344ba7f6a6b0ee7683c3ac7661338f01be601a10
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718694"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Websites para servidores de sistema de site em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Várias funções do sistema do site Do Gestor de Configuração requerem a utilização dos Serviços de Informação da Microsoft internet (IIS) e utilizam o website IIS padrão para hospedar serviços do sistema do site. Quando tiver de executar outras aplicações web no mesmo servidor e as definições não são compatíveis com o Gestor de Configuração, considere utilizar um website personalizado para O Gestor de Configuração.  

> [!TIP]  
>  Uma boa prática de segurança é dedicar um servidor para os sistemas de site do Gestor de Configuração que requerem IIS. Quando executa outras aplicações num sistema de site do Gestor de Configuração, aumenta a superfície de ataque desse computador.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a>O que saber antes de escolher usar websites personalizados  
 Por predefinição, as funções do sistema de sites utilizam o **Site Predefinido** no IIS. Isto é configurado automaticamente quando a função do sistema do site se instala. No entanto, nos sites primários, pode optar por utilizar sites personalizados como alternativa. Quando utilizar Web sites personalizados:  

-   Os websites personalizados estão ativados para todo o site em vez de para servidores ou funções individuais do sistema de sites.  

-   Nos sites primários, cada computador que irá acolher uma função de sistema de site aplicável deve ser configurado com um site personalizado chamado **SMSWEB**. Até criar este site e configurar funções de sistema de site nesse computador para usar o website personalizado, os clientes podem não ser capazes de comunicar com as funções do sistema do site nesse computador.  

-   Como os sites secundários são configurados automaticamente para usar um website personalizado quando o seu site principal é configurado para fazê-lo, você também deve criar sites personalizados no IIS em cada servidor de sistema de site secundário que requer IIS.  


  **Pré-requisitos para utilizar Web sites personalizados:**  

 Antes de ativar a opção para utilizar Web sites personalizados num site, tem de:  

-   Criar um Web site personalizado denominado **SMSWEB** no IIS em cada servidor de sistema de sites que requer o IIS. Pode fazê-lo no site primário e em quaisquer sites secundários.  

-   Configurar o website personalizado para responder à mesma porta que criou para a comunicação do cliente do Gestor de Configuração (porta de pedido do cliente).  

-   Para cada website personalizado ou predefinido que utilize uma pasta personalizada, coloque uma cópia do tipo de documento predefinido que utiliza na pasta raiz que acolhe o website. Por exemplo, num computador R2 do Windows Server 2008 que tem configurações padrão, **iisstart.htm** é um dos vários tipos de documentos predefinidos que estão disponíveis. Pode encontrar este ficheiro na raiz do website predefinido e, em seguida, colocar uma cópia deste ficheiro (ou uma cópia do tipo de documento predefinido que utiliza) na pasta raiz que acolhe o website personalizado SMSWEB. Para mais informações sobre os tipos de documentos predefinidos, consulte o [predefinido do &lt;\> Documento predefinido para iIS](https://www.iis.net/configreference/system.webserver/defaultdocument).  

**Sobre os requisitos do IIS:**
**As seguintes funções do sistema do site requerem o IIS e um website para acolher os serviços do sistema do site:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado  

Considerações adicionais:  

-   Quando um site primário tem websites personalizados ativados, os clientes que são atribuídos a esse site são direcionados para comunicar com os websites personalizados em vez dos sites padrão nos servidores do sistema do site aplicáveis  

-   Se utilizar websites personalizados para um site primário, considere sites personalizados para todos os sites primários da sua hierarquia para garantir que os clientes possam vaguear com sucesso dentro da hierarquia. (Roaming é quando move um computador cliente para um novo segmento de rede gerido por um site diferente. Roaming pode afetar recursos que um cliente pode aceder localmente em vez de através de uma ligação WAN).  

-   As funções do sistema do site que usam o IIS mas não aceitam ligações ao cliente, como o ponto de serviços de reporte, também usam o website SMSWEB em vez do website predefinido.  

-   Os websites personalizados exigem que você atribua números de porta que diferem dos que o site padrão do computador utiliza. Um site predefinido e um site personalizado não podem ser executados em simultâneo se ambos tentarem utilizar as mesmas portas TCP/IP.  

-   As portas TCP/IP que configura no IIS para o website personalizado devem corresponder às portas de pedido do cliente para o site.  

## <a name="switch-between-default-and-custom-websites"></a>Alternar entre sites padrão e personalizados  
Embora possa verificar ou desmarcar a caixa para utilizar websites personalizados num local primário a qualquer momento (a caixa está no separador Geral das Propriedades do site), planeie cuidadosamente antes de fazer esta alteração. Quando esta configuração se alterar, todas as funções do sistema do site aplicável no local primário e os locais secundários infantis devem desinstalar e, em seguida, reinstalar:  

As seguintes funções **são reinstaladas automaticamente**:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de atualização de software  

-   Ponto de estado de contingência  

-   Ponto de Migração de Estado  

As seguintes funções têm de ser **reinstaladas manualmente**:  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de inscrição  

-   Ponto proxy de registo  

Além disso,  

-   Quando muda do website predefinido para utilizar um website personalizado, o Gestor de Configuração não remove os antigos diretórios virtuais. Se pretender remover os ficheiros que o Gestor de Configuração utilizou, tem de eliminar manualmente os diretórios virtuais que foram criados no website predefinido.  

-   Se alterar o site para utilizar websites personalizados, os clientes que já estão atribuídos ao site devem ser reconfigurados para utilizar as novas portas de pedido de cliente para os websites personalizados. Ver [Como configurar as portas](../../../core/clients/deploy/configure-client-communication-ports.md)de comunicação do cliente .  

## <a name="set-up-custom-websites"></a>Configurar sites personalizados  
Uma vez que os passos para criar um site personalizado variam consoante as versões do sistema operativo, consulte a documentação da versão do seu sistema operativo para obter os passos exatos, mas utilize as seguintes informações quando for aplicável:  

-   O nome do site deve ser: **SMSWEB**.  

-   Quando configurar HTTPS, deve especificar um certificado SSL antes de poder guardar a configuração.  

-   Depois de criar o website personalizado, remova as portas personalizadas do site que utiliza de outros websites no IIS:  

    1.  Editar as **Ligações** dos outros websites para remover portas que correspondam às que são atribuídas ao website da **SMSWEB.**  

    2.  Inicie o site da **SMSWEB.**  

    3.  Reinicie o serviço **SMS_SITE_COMPONENT_MANAGER** no servidor do site.  
