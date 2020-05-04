---
title: Configure as portas de comunicação do cliente
titleSuffix: Configuration Manager
description: Detete as portas de comunicação do cliente no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713115"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Como configurar as portas de comunicação do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode alterar os números de porta de pedido que os clientes do Gestor de Configuração usam para comunicar com sistemas de site que utilizam HTTP e HTTPS para comunicação. Embora http ou HTTPS seja mais propenso a estar já configurado para firewalls, a notificação do cliente que utiliza HTTP ou HTTPS requer mais utilização e memória de CPU no computador do ponto de gestão do que se utilizar um número de porta personalizado. Também pode especificar o número da porta do site a utilizar se acordar clientes utilizando pacotes tradicionais de despertar.  

 Quando especificar as portas de pedido HTTP e HTTPS, pode especificar tanto um número de porta por defeito como um número de porta alternativo. Os clientes experimentam automaticamente a porta alternativa depois de a comunicação falhar com a porta padrão. Pode especificar definições para a comunicação de dados HTTP e HTTPS.  

 Os valores predefinidos para as portas de pedido de cliente são **80** para tráfego HTTP e **443** para tráfego HTTPS. Mude-os apenas se não quiser utilizar estes valores predefinidos. Um cenário típico para usar portas personalizadas é quando você usa um site personalizado no IIS em vez do site padrão. Se alterar os números de porta padrão para o website predefinido no IIS e outras aplicações também utilizarem o website predefinido, é provável que falhem.  

> [!IMPORTANT]
>  Não altere os números de porta no Gestor de Configuração sem compreender as consequências. Exemplos:  
> 
> - Se alterar os números de porta dos serviços de pedido do cliente como configuração do site e os clientes existentes não forem reconfigurados para utilizar os novos números de porta, estes clientes ficarão desgeridos.  
>   -   Antes de configurar um número de porta não predefinido, certifique-se de que as firewalls e todos os dispositivos de rede intervenientes podem suportar esta configuração e reconfigurá-las conforme necessário. Se gere os clientes na Internet e altera o número de porta HTTPS padrão de 443, os routers e firewalls na Internet podem bloquear esta comunicação.  

 Para garantir que os clientes não se desgerem depois de alterar os números da porta de pedido, os clientes devem ser configurados para utilizar os novos números de porta de pedido. Quando altera as portas de pedido num local primário, quaisquer sites secundários anexados herdam automaticamente a mesma configuração de porta. Utilize o procedimento neste tópico para configurar as portas de pedido no local principal.  

> [!NOTE]  
>  Para obter informações sobre como configurar as portas de pedido para clientes em computadores que executam linux e UNIX, consulte [Configure Request Ports for the Client for Linux e UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Quando o site do Gestor de Configuração for publicado para Ative Directory Domain Services, clientes novos e existentes que possam aceder a esta informação serão automaticamente configurados com as definições da porta do site e não precisa de tomar mais medidas. Os clientes que não conseguem aceder a esta informação publicada nos Serviços de Domínio do Diretório Ativo incluem clientes de grupode saem, clientes de outra floresta de Diretório Ativo, clientes que estão configurados apenas para internet, e clientes que estão atualmente na Internet. Se alterar os números de porta padrão após a instalação destes clientes, reinstale-os e instale novos clientes utilizando um dos seguintes métodos:  

- Reinstale os clientes utilizando o Assistente de Instalação de Impulso do Cliente. A instalação push do cliente confunde automaticamente os clientes com a configuração da porta do site atual. Para obter mais informações sobre como utilizar o Assistente de Instalação push do cliente, consulte como instalar clientes de gestor de [configuração utilizando](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)o Push do Cliente .  

- Reinstale os clientes utilizando ccMSetup.exe e as propriedades de instalação cliente.msi da CCMHTTPPORT e CCMHTTPSPORT. Para mais informações sobre estas propriedades, consulte sobre as propriedades de [instalação do cliente.](../../../core/clients/deploy/about-client-installation-properties.md)  

- Reinstale os clientes utilizando um método que pesquisa Serviços de Domínio de Diretório Ativo para propriedades de instalação de clientes do Gestor de Configuração. Para mais informações, consulte sobre as propriedades de [instalação do cliente publicadas nos Serviços de Domínio de Diretório Ativo.](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)  

  Para reconfigurar os números de porta dos clientes existentes, também pode utilizar o script PORTSWITCH. VBS que é fornecido com os meios de instalação na pasta SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  Para clientes existentes e novos que estão atualmente na Internet, deve configurar os números de porta não predefinidos utilizando as propriedades CCMSetup.exe client.msi da CCMHTTPPORT e CCMHTTPSPORT.  

 Depois de alterar as portas de pedido no site, novos clientes que são instalados utilizando o método de instalação push do cliente em todo o site serão automaticamente configurados com os números de porta atuais para o site.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Para configurar os números da porta de comunicação do cliente para um site  

1. Na consola do Configuration Manager, clique em **Administração**.  

2. No espaço de trabalho da **Administração,** expandir a Configuração do **Site,** clicar **em Sites,** e selecionar o site principal para configurar.  

3. No separador **Casa,** clique em **Propriedades**, e, em seguida, clique no separador **Portas.**  

4. Selecione qualquer um dos itens e clique no ícone Propriedades para exibir a caixa de diálogo De detalhes da **porta.**  

5. Na caixa de diálogo De pormenor da **porta,** especifique o número da porta e a descrição do artigo **e,** em seguida, clique OK .  

6. Selecione Utilize o **site personalizado** se utilizar o nome de site personalizado do **SMSWeb** para sistemas de site que executam o IIS.  

7. Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  

   Repita este procedimento para todos os sites primários da hierarquia.
