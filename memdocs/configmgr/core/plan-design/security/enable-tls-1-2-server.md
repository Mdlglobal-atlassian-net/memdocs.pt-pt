---
title: Ativar a Segurança da Camada de Transporte (TLS) 1.2 nos servidores do site e sistemas de site remoto
titleSuffix: Configuration Manager
description: Informações sobre como ativar o TLS 1.2 para servidores do site do Gestor de Configuração.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720549"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Como ativar o TLS 1.2 nos servidores do site e sistemas de site remoto

*Aplica-se a: Gestor de Configuração (Ramo Atual)*

Ao ativar o TLS 1.2 para o ambiente do seu Gestor de Configuração, comece por [permitir o TLS 1.2 para os clientes](enable-tls-1-2-client.md) primeiro. Em seguida, ative tLS 1.2 nos servidores do site e sistemas de site remoto em segundo lugar. Finalmente, teste as comunicações do cliente para o site antes de potencialmente desativar os protocolos mais antigos do lado do servidor. São necessárias as seguintes tarefas para permitir o TLS 1.2 nos servidores do site e nos sistemas de sites remotos:

- Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo
- Atualizar e configurar a .NET Framework para suportar TLS 1.2
- Atualizar os componentes do Servidor SQL e do cliente
- Atualizar os Serviços de Atualização do Servidor do Windows (WSUS)

Para obter mais informações sobre dependências para funcionalidades e cenários específicos do Gestor de Configuração, consulte sobre a possibilidade de [tLS 1.2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Atualizar e configurar a .NET Framework para suportar TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a>Atualizar os componentes do Servidor SQL e do cliente

Microsoft SQL Server 2016 e posteriormente suporte TLS 1.1 e TLS 1.2. Versões anteriores e bibliotecas dependentes podem necessitar de atualizações. Para mais informações, consulte [kB 3135244: Suporte TLS 1.2 para microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Os servidores de sites secundários precisam de utilizar pelo menos o SQL Server 2016 Express com o Service Pack 2 (13.2.50.26) ou mais tarde.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a>Cliente nativo do servidor SQL

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) também descreve requisitos para componentes de clientes Do Servidor SQL.

Certifique-se de atualizar também o SQL Server Client Nativo para pelo menos a versão SQL 2012 SP4 (11.*.7001.0). A partir da versão 1810, este requisito é uma [verificação pré-requisito (advertência)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

O Gestor de Configuração utiliza o Cliente Nativo do Servidor SQL nas seguintes funções do sistema do site:

- Servidor da base de dados do site
- Servidor do site: site da administração central, site primário ou site secundário
- Ponto de gestão
- Ponto de gestão de dispositivos
- Ponto de Migração de Estado
- Fornecedor de SMS
- Ponto de atualização de software
- Ponto de distribuição com multicast ativado
- Ponto de serviço de atualização de Inteligência de Ativos
- Ponto do Reporting Services
- Serviço web de catálogo de aplicações
- Ponto de inscrição
- Ponto de Endpoint Protection
- Ponto de ligação de serviço
- Ponto de registo de certificados
- Ponto de serviço de armazém de dados


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a>Atualizar os Serviços de Atualização do Servidor do Windows (WSUS)

Para suportar o TLS 1.2 em versões anteriores do WSUS, instale a seguinte atualização no servidor WSUS:

- Para o servidor WSUS que está a executar o Windows Server 2012, instale a [atualização 4022721](https://support.microsoft.com/help/4022721) ou uma atualização posterior de rollup.
- Para o servidor WSUS que está a executar o Windows Server 2012 R2, instale a [atualização 4022720](https://support.microsoft.com/help/4022720) ou uma atualização posterior de rollup.

A partir do Windows Server 2016, o TLS 1.2 é suportado por predefinição para wSUS.  As atualizações TLS 1.2 só são necessárias nos servidores WSUS do Windows Server 2012 e Do Windows Server 2012.

## <a name="next-steps"></a>Passos seguintes

- [Common issues when enabling TLS 1.2 (Problemas comuns ao ativar o TLS 1.2)](enable-tls-1-2-troubleshoot.md)
