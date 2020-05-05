---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720542"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Determinar a versão .NET

Primeiro, determine as versões .NET instaladas. Para mais informações, consulte como determinar quais as [versões e níveis de pacote de serviços do Microsoft .NET Framework](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Instalar atualizações .NET

Instale as atualizações .NET para que possa ativar uma encriptação forte. Algumas versões do .NET Framework podem necessitar de atualizações para permitir uma encriptação forte. Utilize estas orientações:

- Quadro LÍQUIDO 4.6.2 e posteriormente suporta TLS 1.1 e TLS 1.2. Confirme as definições do registo, mas não são necessárias alterações adicionais.

- Atualizar o Quadro NET 4.6 e versões anteriores para suportar TLS 1.1 e TLS 1.2. Para obter mais informações, consulte [versões e dependências .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Se estiver a utilizar .NET Framework 4.5.1 ou 4.5.2 no Windows 8.1 ou Windows Server 2012, as atualizações e detalhes relevantes também estão disponíveis no Centro de [Descarregamento.](https://www.microsoft.com/download/details.aspx?id=42883)


### <a name="configure-for-strong-cryptography"></a>Configurar para uma criptografia forte

Configure .NET Quadro para apoiar uma encriptação forte. Defina `SchUseStrongCrypto` a definição de registo para `DWORD:00000001`. Este valor desativa a cifra de fluxo RC4 e requer um reinício. Para mais informações sobre esta definição, consulte [o Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Certifique-se de que define as seguintes teclas de registo em qualquer computador que comunique através da rede com um sistema tLS 1.2 ativado. Por exemplo, clientes do Gestor de Configuração, funções de sistema de site remoto não instaladas no servidor do site e no servidor do próprio site.

Para aplicações de 32 bits que estão em execução em OSs de 32 bits e para aplicações de 64 bits que estão em execução em OSs de 64 bits, atualize os seguintes valores sub-chave:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Para aplicações de 32 bits que estão em execução em OSs de 64 bits, atualize os seguintes valores sub-chave:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> A `SchUseStrongCrypto` definição permite que .NET utilize TLS 1.1 e TLS 1.2. A `SystemDefaultTlsVersions` definição permite que a rede .NET utilize a configuração DO. Para mais informações, consulte [as melhores práticas do TLS com o .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).
