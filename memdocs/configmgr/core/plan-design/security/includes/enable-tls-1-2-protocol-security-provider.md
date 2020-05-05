---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720535"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 é ativado por predefinição. Por conseguinte, não é necessária qualquer alteração a estas chaves para a permitir. Pode fazer alterações para `Protocols` desativar TLS 1.0 e TLS 1.1 depois de ter seguido o resto da orientação nestes artigos e verificou que o ambiente funciona quando apenas TLS 1.2 está ativado.

Verifique `\SecurityProviders\SCHANNEL\Protocols` a definição de sub-chave do registo, como mostra as melhores práticas de segurança da camada de [transporte (TLS) com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

