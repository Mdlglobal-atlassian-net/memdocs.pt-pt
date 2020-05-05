---
title: Questões comuns ao permitir a segurança da camada de transporte (TLS) 1.2
titleSuffix: Configuration Manager
description: Descreve questões comuns ao permitir a segurança da camada de transporte (TLS) 1.2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720528"
---
# <a name="common-issues-when-enabling-tls-12"></a>Common issues when enabling TLS 1.2 (Problemas comuns ao ativar o TLS 1.2)

Este artigo fornece conselhos para questões comuns que ocorrem quando ativa o suporte TLS 1.2 no Gestor de Configuração.

## <a name="unsupported-platforms"></a>Plataformas não suportadas

As seguintes plataformas de clientes são suportadas pelo Gestor de Configuração, mas não são suportadas num ambiente TLS 1.2:

- Windows CE
- Apple OS X
- Dispositivos do Windows 10 geridos com MDM no local

## <a name="reports-dont-show-in-the-console"></a>Os relatórios não aparecem na consola.

Se os relatórios não aparecerem na consola do Gestor de Configuração, certifique-se de atualizar o computador no qual está a executar a consola. [Atualize o .NET Framework](enable-tls-1-2-client.md#bkmk_net)e permita uma criptografia forte.

## <a name="fips-security-policy-enabled"></a>Política de segurança fips ativada

Se ativar a definição de política de segurança FIPS para o cliente ou para um servidor, a negociação do Secure Channel (Canal Seguro) pode fazê-los utilizar o TLS 1.0. Este comportamento acontece mesmo que desative o protocolo no registo.

Para investigar, ative o registo de eventos do Secure Channel e, em seguida, reveja os eventos do Canal da Mancha no registo do sistema. Para mais informações, consulte [Como restringir o uso de certos algoritmos criptográficos e protocolos em Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>Falha de comunicação do Servidor SQL

Se a comunicação do SQL Server falhar e devolver um erro **de Erro de Erro de Segurança,** verifique as seguintes definições:

- [Atualização .NET Framework](enable-tls-1-2-server.md#bkmk_net), e permitir uma criptografia forte em cada máquina
- Atualizar o [Servidor SQL](enable-tls-1-2-server.md#bkmk_sql) no servidor de anfitriões
- [Atualize os componentes do cliente SQL](enable-tls-1-2-server.md#bkmk_sql-client) em todos os sistemas que comunicam com a SQL. Por exemplo, os servidores do site, o fornecedor de SMS e os servidores de funções do site.

## <a name="configuration-manager-client-communication-failures"></a>Falhas de comunicação do cliente do Gestor de Configuração

Se o cliente do Gestor de Configuração não comunicar com as funções do site, verifique se [atualizou o Windows](enable-tls-1-2-client.md#bkmk_winhttp) para suportar o TLS 1.2 para comunicação cliente-servidor utilizando o WinHTTP. As funções comuns do site incluem pontos de distribuição, pontos de gestão e pontos de migração do Estado.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Ponto de serviços de reporte falha e devolve um erro esperado

Se o ponto de serviços de reporte não configurar relatórios, verifique o **SRSRP.log** para obter a seguinte entrada de erro:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para resolver este problema, siga estes passos:

1. [Atualização .NET Framework](enable-tls-1-2-client.md#bkmk_net), e permitir uma encriptação forte em todos os computadores relevantes.

1. Depois de instalar quaisquer atualizações, reinicie o serviço SMS_Executive.

## <a name="application-catalog-doesnt-initialize"></a>Catálogo de aplicações não rubrica

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [funcionalidades removidas e depreciadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Se o catálogo de aplicações não rubricar, verifique o ficheiro **ServicePortalWebSite.svclog** para obter a seguinte entrada de erro:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para resolver este problema, siga estes passos:

1. [Atualização .NET Framework](enable-tls-1-2-client.md#bkmk_net), e permitir uma encriptação forte em todos os computadores relevantes.

1. Na `%WinDir%\System32\InetSrv` pasta do servidor de catálogo de aplicações, crie um ficheiro **W2SP.exe.config** com os seguintes conteúdos:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Este ficheiro é o ficheiro predefinido que é criado se a aplicação foi construída utilizando a .NET Framework 4.6.3.

1. Utilize a segurança de transporte HTTPS para funções de catálogo de aplicações.

    > [!Important]
    > Quando utiliza a segurança da mensagem HTTP para funções de catálogo de aplicações, o WCF é codificado para utilizar apenas SSL 3.0 e TLS 1.0. Isto impede a utilização de TLS 1.2.

1. Se tiver feito alterações, reinicie o computador.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Centro de Software ou navegador não comunica com o catálogo de aplicações

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [funcionalidades removidas e depreciadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

O melhor método para fazer o Software Center trabalhar para aplicações disponíveis no utilizador num site ativado por TLS 1.2, remova a função de catálogo de aplicações. Em seguida, deixe o Software Center comunicar diretamente com um ponto de gestão. Para mais informações, consulte [Remova o catálogo de aplicações](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Se necessitar de resolver falhas de comunicação entre o catálogo de aplicações e o Centro de Software, verifique as seguintes condições:

- [Atualização .NET Framework](enable-tls-1-2-client.md#bkmk_net), e permitir uma criptografia forte em cada computador.

- Depois de efazer as alterações, reinicie todos os computadores afetados.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Falhas de carregamento do ponto de ligação de serviço

Se o ponto de ligação ao serviço não fizer o upload de dados para o SCCMConnectedService, [atualize a .NET Framework](enable-tls-1-2-server.md#bkmk_net), e ative uma encriptação forte em cada computador. Depois de efazer as alterações, lembre-se de reiniciar os computadores.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>A consola do Gestor de Configuração apresenta uma caixa de diálogo de embarque intune

Se a caixa de diálogo de onboarding Intune aparecer quando a consola tentar ligar-se ao portal Intune, [atualize a .NET Framework](enable-tls-1-2-client.md#bkmk_net), e ative uma encriptação forte em cada computador. Depois de efazer as alterações, lembre-se de reiniciar os computadores.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Consola de Gestor de Configuração apresenta falha no insessão no Azure

Quando tentar criar aplicações no Azure Ative Directory (Azure AD), se a caixa de diálogo de bordo dos Serviços Azure falhar imediatamente após selecionar **o Signin in**, [atualize o .NET Framework](enable-tls-1-2-server.md#bkmk_net)e ative uma encriptação forte. Depois de efazer as alterações, lembre-se de reiniciar os computadores.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Serviços de nuvem de gestor de configuração e TLS 1.2

As máquinas virtuais Azure utilizadas pelo portal de gestão da nuvem e pelos pontos de distribuição em nuvem suportam o TLS 1.2. As versões suportadas do cliente utilizam automaticamente o TLS 1.2.

O **sMSAdminui.log** pode conter um erro semelhante ao seguinte exemplo:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

No System EventLog, o SChannel EventID 36874 pode ser registado com a seguinte descrição:`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Recursos adicionais

- [As melhores práticas de segurança da camada de transporte (TLS) com o Quadro .NET](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Suporte TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Referência técnica de controlos criptográficos](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Passos seguintes

- [Enable TLS 1.2 on clients (Ativar o TLS 1.2 nos clientes)](enable-tls-1-2-client.md)
- [Ativar o TLS 1.2 nos servidores do site e sistemas de site remoto](enable-tls-1-2-server.md)

