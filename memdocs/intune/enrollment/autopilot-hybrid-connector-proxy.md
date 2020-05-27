---
title: Configure as definições de procuração para o Conector Intune para Diretório Ativo
description: Cobre como configurar o Conector Intune para Diretório Ativo para trabalhar com servidores proxy existentes no local.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: b26bf4910e6745a60634a2b313a37beeb33192d3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986891"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Trabalhar com servidores proxy existentes no local

Este artigo explica como configurar o Conector Intune para o Diretório Ativo para trabalhar com servidores proxy de saída. Destina-se a clientes com ambientes de rede que tenham proxies existentes.

Por predefinição, o Conector Intune para Diretório Ativo tentará localizar automaticamente um servidor proxy na rede utilizando o Web Proxy Auto-Discovery (WPAD). Se isto tiver sido configurado na sua rede, pode não ser necessária uma configuração adicional.  Se forem necessárias alterações, as seguintes secções descrevem como anular as definições predefinidas, aproveitando [as capacidades padrão .NET Framework para configurar as definições](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)de procuração .  Opções adicionais são descritas nessa documentação.

Para obter mais informações sobre como funcionam os conectores, consulte [conectores de proxy de aplicação ad azure](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Contornar completamente os proxies de saída

Pode configurar o conector para contornar o seu proxy no local para garantir que utiliza conectividade direta com os serviços Azure. Recomendamos esta abordagem, desde que a sua política de rede o permita, porque significa que tem menos uma configuração para manter.

Para desativar a utilização de proxy de saída para o conector, edite o ficheiro "\Program Files\Microsoft Intune\ODJConnectorUI\ODJConnectorUI.exe.config" e adicione o endereço proxy e a porta proxy na secção mostrada nesta amostra de código:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Para garantir que o serviço de atualização do Conector também contorna o proxy, faça uma alteração semelhante a C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc\ODJConnectorSvc.exe.cofig.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Certifique-se de que faz cópias dos ficheiros originais, caso precise de voltar aos ficheiros predefinidos .config.

Uma vez modificados os ficheiros de configuração, terá de reiniciar o serviço Intune Connector. 

1. Serviços **abertos.msc**.
2. Encontre e selecione o **Serviço Intune ODJConnector**.
3. Selecione **Reiniciar**.

![Screenshot do reinício do serviço](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Especificando um servidor de procuração alternativo

Se um servidor de procuração diferente (por exemplo, um que contorna a autenticação) tiver de ser utilizado com o Conector Intune para Diretório Ativo, este pode ser especificado de forma semelhante. Para tal, edite o ficheiro "\Program Files\Microsoft Intune\ODJConnectorUI\ODJConnectorUI.exe.config" e adicione o endereço proxy e a porta proxy na secção mostrada nesta amostra de código:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Para garantir que o serviço de atualização do Conector também contorna o proxy, faça uma alteração semelhante a C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc\ODJConnectorSvc.exe.cofig.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Certifique-se de que faz cópias dos ficheiros originais, caso precise de voltar aos ficheiros predefinidos .config.

Uma vez modificados os ficheiros de configuração, terá de reiniciar o serviço Intune Connector. 

1. Serviços **abertos.msc**.
2. Encontre e selecione o **Serviço Intune ODJConnector**.
3. Selecione **Reiniciar**.

![Screenshot do reinício do serviço](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Passos seguintes

[Faça a gestão dos seus dispositivos](../remote-actions/device-management.md)
