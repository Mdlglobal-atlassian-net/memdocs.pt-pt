---
title: Azure AD authentication workflow (Fluxo de trabalho da autenticação do Azure AD)
titleSuffix: Configuration Manager
description: Detalhes do processo de instalação do cliente do Gestor de Configuração num dispositivo Windows 10 com autenticação de Diretório Ativo Azure
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714123"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD authentication workflow (Fluxo de trabalho da autenticação do Azure AD)

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo é uma referência técnica para o processo de instalação do cliente do Gestor de Configuração num dispositivo Windows 10 que se juntou ao Azure Ative Directory (Azure AD). Detalha o processo de fluxo de trabalho para a autenticação do dispositivo e instalação do cliente.  
 

## <a name="azure-ad-token-request-workflow"></a>Fluxo de trabalho de pedido de solicitação de adsípede da Azure AD

![Diagrama de fluxo de trabalho Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Pedido de ficha da AD Azure

Um cliente com domínio do Windows 10 Azure usa parâmetros Azure AD para solicitar um sinal. As seguintes entradas são registadas em **ccmsetup.log:**

- Solicitação ficha do dispositivo Azure AD:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Se não conseguir obter um token do dispositivo, solicita um token de utilizador da AD Azure:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Um cliente deve obter um certificado de adesão ao local de trabalho (WPJ) quando aderir à Azure AD. Se não for encontrado um certificado de adesão ao local de trabalho, o cliente não tenta criar o pedido utilizando o canal de comunicação security Token Service (CCM_STS). Este comportamento é porque o cliente não pode adicionar um token Azure AD ao pedido. O dispositivo normalmente não tem este certificado quando o cliente não está devidamente aderido à Azure AD.
>
> Além disso, se o token não for válido, o gateway de gestão de nuvem (CMG) não reencaminha o pedido para as funções internas do site. O símbolo pode ser inválido se o inquilino não estiver registado como um serviço de gestão de nuvem no Gestor de Configuração.


### <a name="2-configuration-manager-client-token-request"></a>2. Pedido de ficha do cliente do Gestor de Configuração

Uma vez que o cliente tenha um token Azure AD, solicita um token de Gestor de Configuração (CCM).

As seguintes entradas são registadas em **ccmsetup.log** da máquina virtual CMG:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG recebe pedido

As seguintes entradas são registadas no **IIS.log:**

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG remeo pedido ao ponto de ligação CMG

As seguintes entradas são registadas em **CMGService.log:**

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 CMG ponto de ligação transforma pedido de cliente CMG ao pedido de cliente de ponto de gestão

As seguintes entradas são registadas em **SMS_CLOUD_PROXYCONNECTOR.log:**

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 Ponto de gestão verifica ficha do utilizador na base de dados do site

As seguintes entradas são registadas em **CCM_STS.log:**

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Pedido de localização de conteúdo

Assim que o cliente obtém uma resposta com o token CCM, ele caches e usa-o para solicitar informações do site e localização de conteúdo através da CMG. As seguintes entradas são registadas em **ccmsetup.log:**

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Instalação do cliente

O dispositivo descarrega o conteúdo do cliente e inicia a instalação.

### <a name="communication-validation"></a>Validação da comunicação

- A CMG valida o token do cliente através da CMG, do ponto de ligação CMG e do PEDIDO de base de dados de pontos de gestão.
- Cliente verifica certificado de serviço CMG ou certificado de gestão
- PKI para certificado de serviço CMG: Cliente requer autoridade de certificado de raiz (CA) do certificado CMG na loja local
- Certificado de serviço CMG de terceiros: Os clientes validam automaticamente um certificado com a sua raiz CA publicada na internet


## <a name="common-issues"></a>Problemas comuns

- Raiz CA não presente
- Verificação CRL ativada: publique CRL na internet ou use a opção **/NoCRLcheck** na linha de comando
- Certificado WPJ não encontrado: cliente está registado na Azure AD, mas não se juntou à Azure AD

Utilizar /NoCRLCheck só é bom para a armadilha de botas ccmsetup. Para que os clientes estejam totalmente funcionais, deve publicar o CRL na internet. Como suposições, pode desativar a verificação do CRL na configuração de comunicação do cliente do site. Caso contrário, após as definições de segurança serem renovadas pelo serviço de localização, os clientes deixam de comunicar com o servidor.


## <a name="client-registration"></a>Registo do cliente

![Diagrama de fluxo de trabalho de registo azure AD](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Registo de pedido de cliente do Gestor de Configuração

As seguintes entradas são registadas no **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Gestor de Configuração solicita ficha da AD Azure para registar cliente

As seguintes entradas são registadas no **ADALOperationProvider.log:**

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Cliente do Gestor de Configuração está registado  

As seguintes entradas são registadas no **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Durante o registo do cliente, a validação do certificado corre sempre. Este processo acontece mesmo que esteja a utilizar o método de autenticação Azure AD para registar o cliente.


### <a name="3-configuration-manager-client-token-request"></a>3. Pedido de ficha do cliente do Gestor de Configuração

Assim que o site regista o cliente, o cliente solicita um token CCM. O token CCM é encriptado para a conta do Sistema local (S-1-5-18) e cacheed durante oito horas. Após oito horas, o símbolo expira, e o cliente pede renovação simbólica.

As seguintes entradas são registadas no **ClientIDManagerStartup.log**:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG recebe pedido

As seguintes entradas são registadas no **IIS.log:**

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG remeo pedido ao ponto de ligação CMG

As seguintes entradas são registadas em **CMGService.log:**

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>Ponto de ligação 3.3 CMG transforma pedido de cliente cmg ao pedido de cliente de ponto de gestão

As seguintes entradas são registadas em **SMS_CLOUD_PROXYCONNECTOR.log:**

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 Ponto de gestão verifica ficha do utilizador na base de dados do site

As seguintes entradas são registadas em **CCM_STS.log:**

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
