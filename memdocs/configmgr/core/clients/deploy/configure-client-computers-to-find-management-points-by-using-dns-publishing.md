---
title: Configure clients to use DNS publishing (Configurar clientes para utilizarem publicações por DNS)
titleSuffix: Configuration Manager
description: Configure os computadores clientes do Gestor de Configuração para encontrar pontos de gestão utilizando a publicação de DNS.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713101"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Configure os computadores dos clientes para encontrar pontos de gestão utilizando a publicação do DNS

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os clientes do Gestor de Configuração devem localizar um ponto de gestão para completar a atribuição do site e como um processo em curso para permanecer gerido. Os Serviços de Domínio do Active Directory fornecem o método mais seguro para que os clientes da intranet consigam localizar pontos de gestão. Porém, se os clientes não puderem utilizar este método de localização do serviço (por exemplo, não expandiu o esquema do Active Directory ou os clientes pertencem a um grupo de trabalho), utilize a publicação de DNS como método de localização do serviço alternativo preferido.  

> [!NOTE]  
>  Quando instala o cliente no Linux e UNIX, tem de especificar um ponto de gestão para utilizar como um ponto inicial de contacto. Para obter informações sobre como instalar o cliente para linux e UNIX, consulte [como implementar clientes para servidores UNIX e Linux](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Antes de utilizar a publicação de DNS em pontos de gestão, certifique-se de que os servidores DNS da intranet possuem registos de recursos de localização do serviço (SRV RR) e registos de recursos de anfitrião correspondente (A ou AAA) para os pontos de gestão do site. Os registos de recursos de localização de serviço podem ser criados automaticamente pelo Gestor de Configuração ou manualmente, pelo administrador do DNS que cria os registos em DNS.  

 Para obter mais informações sobre a publicação do DNS como um método de localização de serviço para clientes do Gestor de Configuração, consulte [como os clientes encontram recursos e serviços](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)do site para O Gestor de Configuração .  

 Por predefinição, os clientes procuram o DNS para pontos de gestão no respetivo domínio de DNS. No entanto, se não houver pontos de gestão publicados no domínio dos clientes, deve configurar manualmente os clientes com um sufixo DNS de ponto de gestão. Pode configurar este sufixo DNS nos clientes durante ou após a instalação do cliente:  

-   Para configurar os clientes com um sufixo de ponto de gestão durante a instalação do cliente, configure as propriedades do CCMSetup Client.msi.  

-   Para configurar os clientes com um sufixo de ponto de gestão após a instalação do cliente, no Painel de Controlo, configure as **Propriedades do Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Para configurar os clientes com um sufixo de ponto de gestão durante a instalação do cliente  

- Instale o cliente com a seguinte propriedade do CCMSetup Client.msi:  

  - Domínio do ponto de gestão **DNSSUFFIX=** * &lt;\>*  

     Se o site tiver mais que um ponto de gestão e estes estiverem em mais de um domínio, especifique apenas um domínio. Quando os clientes estabelecem ligação a um ponto de gestão deste domínio, transferem uma lista de pontos de gestão disponíveis que inclui os pontos de gestão de outros domínios.  

    Para obter mais informações sobre as propriedades da linha de comando CCMSetup, consulte as propriedades de [instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Para configurar os clientes com um sufixo de ponto de gestão após a instalação do cliente  

1.  No Painel de Controlo do computador cliente, aceda a **Configuration Manager**e faça duplo clique em **Propriedades**.  

2.  No separador **Site** , especifique o sufixo DNS de um ponto de gestão e clique em **OK**.  

     Se o site tiver mais que um ponto de gestão e estes estiverem em mais de um domínio, especifique apenas um domínio. Quando os clientes estabelecem ligação a um ponto de gestão deste domínio, transferem uma lista de pontos de gestão disponíveis que inclui os pontos de gestão de outros domínios.
