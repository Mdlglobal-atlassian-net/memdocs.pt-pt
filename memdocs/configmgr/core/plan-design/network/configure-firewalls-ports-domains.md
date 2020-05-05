---
title: Infraestrutura de rede
titleSuffix: Configuration Manager
description: Configurar firewalls, portas e domínios para preparar as comunicações do Gestor de Configuração.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719842"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Considerações de infraestrutura de rede para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para preparar a sua rede para suportar o Gestor de Configuração, poderá ser necessário configurar alguns componentes de infraestrutura. Por exemplo, abrir portas de firewall para passar as comunicações utilizadas pelo Gestor de Configuração.  

## <a name="ports-and-protocols"></a>Portos e protocolos

Diferentes funcionalidades do Gestor de Configuração utilizam diferentes portas de rede. Algumas portas são necessárias, e algumas pode personalizar.

A maioria das comunicações do Gestor de Configuração utilizam portas comuns como a porta 80 para HTTP ou 443 para HTTPS. Algumas funções do sistema do site suportam o uso de websites personalizados e portas personalizadas. Para mais informações, consulte [websites para servidores](websites-for-site-system-servers.md)do sistema do site .

Antes de implementar o Gestor de Configuração, identifique as portas que pretende utilizar e instale firewalls conforme necessário.

Depois de instalar o 'Gestor de Configuração', caso precise de alterar uma porta, não se esqueça de atualizar as firewalls nos dispositivos e na rede. Altere também a configuração da porta em 'Gestor de Configuração'.

Para obter mais informações, veja os artigos seguintes:

- [Como configurar portas de comunicação de cliente](../../clients/deploy/configure-client-communication-ports.md)
- [Portas utilizadas no Gestor de Configuração](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

Algumas funcionalidades do Gestor de Configuração dependem da conectividade da Internet para a funcionalidade completa. Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, certifique-se de que permite os pontos finais necessários.

Para mais informações, consulte [os requisitos de acesso à Internet](internet-endpoints.md)


## <a name="proxy-servers"></a>Servidores proxy

Pode especificar servidores proxy separados para diferentes servidores e clientes do sistema de sites. Faz estas configurações quando instala uma função de sistema de site ou cliente, ou muda-as mais tarde, se necessário.

Para mais informações, consulte o [suporte do servidor Proxy](proxy-server-support.md).
