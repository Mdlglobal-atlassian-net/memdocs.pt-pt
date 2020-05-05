---
title: Ativar a segurança da camada de transporte (TLS) 1.2 visão geral
titleSuffix: Configuration Manager
description: Visão geral de como ativar tLS 1.2 para Gestor de Configuração.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720521"
---
# <a name="how-to-enable-tls-12"></a>Como ativar o TLS 1.2

*Aplica-se a: Gestor de Configuração (Ramo Atual)*

A Segurança da Camada de Transporte (TLS), tal como a Secure Sockets Layer (SSL), é um protocolo de encriptação destinado a manter os dados seguros quando são transferidos para uma rede. Estes artigos descrevem as etapas necessárias para garantir que a comunicação segura do Gestor de Configuração utilize o protocolo TLS 1.2. Estes artigos também descrevem os requisitos de atualização para componentes comumente usados e problemas comuns de resolução de problemas.

## <a name="enabling-tls-12"></a>Habilitação TLS 1.2

O Gestor de Configuração baseia-se numa série de componentes diferentes para uma comunicação segura. O protocolo que é usado para uma determinada ligação depende das capacidades dos componentes relevantes tanto do lado do cliente como do servidor. Se algum componente estiver desatualizado ou não estiver devidamente configurado, a comunicação poderá utilizar um protocolo mais antigo e menos seguro. Para ativar corretamente o Gestor de Configuração para suportar o TLS 1.2 para todas as comunicações seguras, deve ativar o TLS 1.2 para todos os componentes necessários. Os componentes necessários dependem do seu ambiente e do Gestor de Configuração que utiliza.

> [!IMPORTANT]
> Inicie este processo com os clientes, especialmente versões anteriores do Windows. Antes de ativar o TLS 1.2 e desativar os protocolos mais antigos nos servidores do Gestor de Configuração, certifique-se de que todos os clientes suportam TLS 1.2. Caso contrário, os clientes não podem comunicar com os servidores e podem ficar órfãos.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Tarefas para clientes do Gestor de Configuração, servidores de site e sistemas de site remoto

Para ativar o TLS 1.2 para componentes de que o Gestor de Configuração depende para uma comunicação segura, terá de fazer várias tarefas tanto nos clientes como nos servidores do site.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Ativar TLS 1.2 para clientes do Gestor de Configuração

- [Atualizar Windows e WinHTTP no Windows 8.0, Windows Server 2012 (não-R2) e anteriormente](enable-tls-1-2-client.md#bkmk_winhttp)
- [Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo](enable-tls-1-2-client.md#bkmk_protocol)
- [Atualizar e configurar a .NET Framework para suportar TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Ativar o TLS 1.2 para servidores de site do Gestor de Configuração e sistemas de site remoto

- [Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo](enable-tls-1-2-server.md#bkmk_protocol)
- [Atualizar e configurar a .NET Framework para suportar TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [Atualizar o Servidor SQL e o Cliente Nativo SQL](enable-tls-1-2-server.md#bkmk_sql)
- [Atualizar os Serviços de Atualização do Servidor do Windows (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Características e dependências de cenários

Esta secção descreve as dependências para funcionalidades e cenários específicos do Gestor de Configuração. Para determinar os próximos passos, localize os itens que se aplicam ao seu ambiente.

|Recurso ou cenário|Atualizar tarefas|
|--- |--- |
|Servidores do site (central, primário ou secundário)| - [Quadro de atualização .net](enable-tls-1-2-server.md#bkmk_net)<br/> - Verificar configurações fortes de criptografia|
|Servidor da base de dados do site|[Atualizar o Servidor SQL e os seus componentes de cliente](enable-tls-1-2-server.md#bkmk_sql)|
|Servidores de sites secundários|[Atualizar o SQL Server e os seus componentes de cliente](enable-tls-1-2-server.md#bkmk_sql) para uma versão conforme do SQL Express|
|Funções do sistema de sites| - [Atualizar .NET Enquadramento](enable-tls-1-2-server.md#bkmk_net) e verificar configurações de criptografia fortes <br/> - [Atualizar o SQL Server e os seus componentes de cliente](enable-tls-1-2-server.md#bkmk_sql) em funções que o exijam, incluindo o Cliente Nativo do Servidor [SQL](enable-tls-1-2-server.md#bkmk_sql-client)|
|Ponto do Reporting Services|- [Atualização .NET Quadro](enable-tls-1-2-server.md#bkmk_net) no servidor do site, nos servidores sql reporting services e em qualquer computador com a consola<br/> - Reiniciar o serviço de SMS_Executive conforme necessário|
|Ponto de atualização de software|[Atualizar wSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Gateway de gestão da cloud|[Impor TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Consola do Configuration Manager| - [Quadro de atualização .net](enable-tls-1-2-client.md#bkmk_net)<br/> - Verificar configurações fortes de criptografia|
|Cliente de Gestor de Configuração com funções de sistema de site HTTPS|[Atualizar o Windows para suportar TLS 1.2 para comunicações de servidor de clientes utilizando o WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Centro de Software| - [Quadro de atualização .net](enable-tls-1-2-client.md#bkmk_net)<br/> - Verificar configurações fortes de criptografia|
|Clientes do Windows 7| *Antes* de ativar o TLS 1.2 em quaisquer componentes do servidor, atualize o [Windows para suportar o TLS 1.2 para comunicações de servidores](enable-tls-1-2-client.md#bkmk_winhttp)de clientes utilizando o WinHTTP . Se ativar primeiro o TLS 1.2 nos componentes do servidor, pode órfã versões anteriores dos clientes.|

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="why-use-tls-12-with-configuration-manager"></a>Porquê utilizar o TLS 1.2 com o Gestor de Configuração?

TLS 1.2 é mais seguro do que os protocolos criptográficos anteriores, tais como SSL 2.0, SSL 3.0, TLS 1.0 e TLS 1.1. Essencialmente, o TLS 1.2 mantém os dados transferidos através da rede mais seguros.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Onde é que o Gestor de Configuração utiliza protocolos de encriptação como o TLS 1.2?

Existem basicamente cinco áreas que o Gestor de Configuração utiliza protocolos de encriptação como o TLS 1.2:

- Comunicações do cliente para funções de servidor de site baseados no IIS quando a função é configurada para usar HTTPS. Exemplos destas funções incluem pontos de distribuição, pontos de atualização de software e pontos de gestão.
- Ponto de gestão, SMS Executive e SMS Provider comunicações com a SQL. O Gestor de Configuração encripta sempre as comunicações SQL.
- Site Server para comunicações WSUS se wSUS estiver configurado para usar HTTPS.
- A consola do Gestor de Configuração para os Serviços de Relato SQL (SSRS) se a SSRS estiver configurada para utilizar HTTPS.
- Quaisquer ligações a serviços baseados na Internet. Exemplos incluem o gateway de gestão de nuvem (CMG), a sincronização do ponto de ligação ao serviço e sincronização de metadados de atualização a partir do Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>O que determina qual o protocolo de encriptação que é usado?

Https negociará sempre a versão de protocolo mais alta que é suportada tanto pelo cliente como pelo servidor numa conversa encriptada. Ao estabelecer uma ligação, o cliente envia uma mensagem ao servidor com o seu protocolo mais elevado disponível. Se o servidor suportar a mesma versão, envia uma mensagem utilizando essa versão. Esta versão negociada é a que é usada para a ligação. Se o servidor não suportar a versão apresentada pelo cliente, a mensagem do servidor especificará a versão mais alta que pode utilizar. Para obter mais informações sobre o protocolo de aperto de mão TLS, consulte [o Estabelecimento de uma Sessão Segura utilizando o TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>O que determina qual a versão protocolar que o cliente e o servidor podem usar?

Geralmente, os seguintes itens podem determinar qual a versão protocolada utilizada:

- A aplicação pode ditar quais versões específicas de protocolo para negociar.
  - As melhores práticas ditam evitar versões de protocolo específicas de codificação dura ao nível da aplicação e seguir a configuração definida ao nível do protocolo do componente e do sistema operativo.
  - O Gestor de Configuração segue as melhores práticas.
- Para as aplicações escritas com o Quadro .NET, as versões de protocolo padrão dependem da versão do quadro em que foram compiladas.  
  - As versões .NET antes de 4.6.3 não incluíam TLS 1.1 e 1.2 na lista de protocolos de negociação, por defeito.
- As aplicações que utilizam o WinHTTP para comunicações HTTPS, como o cliente do Gestor de Configuração, dependem da versão do sistema operativo, do nível de patch e da configuração para suporte à versão protocolar.


## <a name="additional-resources"></a>Recursos adicionais

- [Referência técnica de controlos criptográficos](cryptographic-controls-technical-reference.md)
- [As melhores práticas de segurança da camada de transporte (TLS) com o Quadro .NET](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Suporte TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Passos seguintes

- [Enable TLS 1.2 on clients (Ativar o TLS 1.2 nos clientes)](enable-tls-1-2-client.md)
- [Ativar TLS 1.2 nos servidores do site](enable-tls-1-2-server.md)
