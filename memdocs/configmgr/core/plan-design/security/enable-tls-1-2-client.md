---
title: Como ativar a Segurança da Camada de Transporte (TLS) 1.2 nos clientes
titleSuffix: Configuration Manager
description: Informações sobre como ativar os clientes TLS 1.2 para os clientes do Gestor de Configuração.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720556"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Como ativar o TLS 1.2 nos clientes

*Aplica-se a: Gestor de Configuração (Ramo Atual)*

Ao ativar o TLS 1.2 para o ambiente do Seu Gestor de Configuração, comece por garantir que os clientes são capazes e devidamente configurados para utilizar o TLS 1.2 antes de ativar o TLS 1.2 e desativar os protocolos mais antigos nos servidores do site e sistemas de site remoto. Existem três tarefas para permitir o TLS 1.2 nos clientes:

- Atualizar Windows e WinHTTP
- Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo
- Atualizar e configurar a .NET Framework para suportar TLS 1.2

Para obter mais informações sobre dependências para funcionalidades e cenários específicos do Gestor de Configuração, consulte sobre a possibilidade de [tLS 1.2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a>Atualizar Windows e WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 e versões posteriores do Windows suportam de forma nativa o TLS 1.2 para comunicações de servidores de clientes sobre o WinHTTP. 

As versões anteriores do Windows, como o Windows 7 ou o Windows Server 2012, não permitem o TLS 1.1 ou TLS 1.2 por padrão para comunicações seguras utilizando o WinHTTP. Para estas versões anteriores do Windows, instale o [Update 3140245](https://support.microsoft.com/help/3140245) para ativar o valor de registo abaixo, que pode ser definido para adicionar TLS 1.1 e TLS 1.2 à lista de protocolos seguros predefinidos para winHTTP. Com o patch instalado, crie os seguintes valores de registo:

> [!IMPORTANT]
> Ative estas definições em todos os clientes que executam versões anteriores do Windows *antes* de ativar o TLS 1.2 e desativar os protocolos mais antigos nos servidores do Gestor de Configuração. Caso contrário, podes ilegalmente órfãs deles.

Verifique o valor `DefaultSecureProtocols` da definição de registo, por exemplo:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Se alterar este valor, reinicie o computador.

O exemplo acima mostra `0xAA0` o valor `DefaultSecureProtocols` da definição WinHTTP. [KB 3140245: Atualização para ativar TLS 1.1 e TLS 1.2 como protocolos de segurança predefinidos no WinHTTP no Windows](https://support.microsoft.com/help/3140245) lista o valor hexadecimal para cada protocolo. Por predefinição no `0x0A0` Windows, este valor é para ativar SSL 3.0 e TLS 1.0 para WinHTTP. O exemplo acima mantém estes incumprimentos, e também permite TLS 1.1 e TLS 1.2 para WinHTTP. Esta configuração garante que a alteração não quebra qualquer outra aplicação que ainda possa depender de SSL 3.0 ou TLS 1.0. Só pode utilizar `0xA00` o valor de ativar apenas tLS 1.1 e TLS 1.2. O Gestor de Configuração suporta o protocolo mais seguro que o Windows negoceia entre ambos os dispositivos.

 Se pretender desativar completamente o SSL 3.0 e o TLS 1.0, utilize a definição de protocolos desativados do SChannel no Windows. Para mais informações, consulte [Como restringir o uso de certos algoritmos criptográficos e protocolos em Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Certifique-se de que o TLS 1.2 está ativado como um protocolo para o SChannel ao nível do sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Atualizar e configurar a .NET Framework para suportar TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Passos seguintes

- [Ativar o TLS 1.2 nos servidores do site e sistemas de site remoto](enable-tls-1-2-server.md)
- [Common issues when enabling TLS 1.2 (Problemas comuns ao ativar o TLS 1.2)](enable-tls-1-2-troubleshoot.md)

