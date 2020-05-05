---
title: Requisitos de acesso à Internet
titleSuffix: Configuration Manager
description: Conheça os pontos finais da Internet para permitir a funcionalidade completa das funcionalidades do Gestor de Configuração.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58afaf564a8afaba4569755575fcc7c1757c5529
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110139"
---
# <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

Algumas funcionalidades do Gestor de Configuração dependem da conectividade da Internet para a funcionalidade completa. Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, certifique-se de permitir estes pontos finais.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Ponto de ligação de serviço

Estas configurações aplicam-se ao computador que acolhe o ponto de ligação de serviço e quaisquer firewalls entre esse computador e a internet. Ambos devem permitir comunicações através da porta de saída **TCP 443** para HTTPS e porta de saída **TCP 80** para HTTP para os locais abaixo da Internet.

O ponto de ligação de serviço suporta a utilização destes locais por procuração (com ou sem autenticação) para utilizar estes locais. Para mais informações, consulte o [suporte do servidor Proxy](proxy-server-support.md).

Para obter mais informações sobre o ponto de ligação ao serviço, consulte sobre o ponto de [ligação ao serviço](../../servers/deploy/configure/about-the-service-connection-point.md).

Outras funcionalidades do Gestor de Configuração podem requerer pontos finais adicionais do ponto de ligação ao serviço. Para mais informações, consulte as outras secções deste artigo.

> [!TIP]  
> O ponto de ligação ao serviço utiliza `go.microsoft.com` o `manage.microsoft.com`serviço Microsoft Intune quando se conecta a ou . Há um problema conhecido em que o conector Intune experimenta problemas de conectividade se o Certificado de Raiz de Baltimore CyberTrust não for instalado, expirar ou for corrompido no ponto de ligação de serviço. Para mais informações, consulte [KB 3187516: O ponto](https://support.microsoft.com/help/3187516)de ligação ao serviço não descarrega atualizações .  

A partir da versão 2002, se o site do Gestor de Configuração não ligar aos pontos finais necessários para um serviço na nuvem, eleva uma mensagem de estado crítico ID 11488. Quando não consegue ligar-se ao serviço, o SMS_SERVICE_CONNECTOR o estado do componente muda para crítico. Ver estado detalhado no nó de [Estado do Componente](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) da consola 'Gestor de Configuração'.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/>Atualizações e manutenção

Para obter mais informações sobre esta função, consulte [Atualizações e manutenção para O Gestor](../../servers/manage/updates.md)de Configuração .

> [!Tip]  
> Ative estes pontos finais para a regra de insight de [gestão,](../../servers/manage/management-insights.md) **Ligue o site à nuvem da Microsoft para atualizações**do Gestor de Configuração .

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Serviço do Windows 10

Para obter mais informações sobre esta função, consulte [Gerir o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Serviços do Azure

Para obter mais informações sobre esta função, consulte os [serviços Configure Azure para utilização com o Gestor](../../servers/deploy/configure/azure-services-wizard.md)de Configuração .

- `management.azure.com`  

## <a name="co-management"></a>Cogestão

Se inscrever os dispositivos do Windows 10 no Microsoft Intune para cogestão, certifique-se de que estes dispositivos podem aceder aos pontos finais exigidos pela Intune. Para mais informações, consulte [os pontos finais da Rede para o Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Loja Microsoft para Empresas

Se integrar o Gestor de Configuração com a [Microsoft Store for Business,](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)certifique-se de que o ponto de ligação ao serviço e os dispositivos direcionados podem aceder ao serviço de cloud. Para mais informações, consulte a [configuração da Microsoft Store para proxy de negócios](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Serviços em nuvem

<!-- SCCMDocs-pr #3402 -->

Esta secção cobre as seguintes características:

- Gateway de gestão de nuvem (CMG)
- Ponto de distribuição em nuvem (CDP)
- Integração do Diretório Ativo Azure (Azure AD)
- Descoberta baseada em AD Azure

Para a implantação do serviço CMG/CDP, o ponto de **ligação** ao serviço necessita de acesso a:

- Os pontos finais específicos do Azure são diferentes por ambiente, dependendo da configuração. O Gestor de Configuração armazena estes pontos finais na base de dados do site. Consulta da tabela **AzureEnvironments** no SQL Server para a lista de pontos finais do Azure.  

O ponto de **ligação CMG** necessita de acesso aos seguintes pontos finais de serviço:

- Ponto final da Gestão de Serviços:`https://management.core.windows.net/`  

- Ponto final `<name>.blob.core.windows.net` de armazenamento: e`<name>.table.core.windows.net`

    Onde `<name>` está o nome de serviço na nuvem do seu CMG ou CDP. Por exemplo, se o `GraniteFalls.CloudApp.Net`seu CMG for, então o primeiro ponto final de armazenamento a permitir é `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

Para a recuperação de token Azure AD pela consola de **Configuração Manager** e **cliente:**

- ActiveDirectoryEndpoint`https://login.microsoftonline.com/`  

Para a descoberta do utilizador da AD Azure, o ponto de **ligação** ao serviço necessita de acesso a:

- Versão 1810 e anterior: Ponto final do Gráfico AD Azure`https://graph.windows.net/`  

- Versão 1902 e mais tarde: Microsoft Graph endpoint`https://graph.microsoft.com/`

O sistema de ponto de ligação do ponto de ligação (CMG) suporta o sistema de pontos de ligação da web. Para obter mais informações sobre a configuração desta função para um proxy, consulte o [suporte do servidor Proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). O ponto de ligação CMG só precisa de ligar aos pontos finais do serviço CMG. Não precisa de acesso a outros pontos finais do Azure.

Para mais informações sobre o CMG, consulte [Plano para CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

Permitir que o ponto de atualização de software ativo aceda aos seguintes pontos finais para que as Atualizações WSUS e Automáticas possam comunicar com o serviço cloud da Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Para obter mais informações sobre atualizações de software, consulte [Plan para atualizações de software](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Firewall intranet

Você pode precisar adicionar pontos finais a uma firewall que está entre dois sistemas de site nos seguintes casos:

- Se os sites infantis tiverem um ponto de atualização de software
- Se houver um ponto de atualização de software baseado na Internet ativa remota num site

#### <a name="software-update-point-on-the-child-site"></a>Ponto de atualização de software no site subordinado

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Gerir o Office 365

> [!NOTE]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

Se utilizar o Gestor de Configuração para implementar e atualizar as Aplicações Microsoft 365 para a empresa, permita os seguintes pontos finais:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`para sincronizar o ponto de atualização de software para as Aplicações Microsoft 365 para atualizações de clientes empresariais

- `config.office.com`para criar configurações personalizadas para aplicações microsoft 365 para implementações empresariais

## <a name="configuration-manager-console"></a>Consola do Configuration Manager

Os computadores com a consola 'Gestor de Configuração' exigem acesso aos seguintes pontos finais da Internet para funcionalidades específicas:

### <a name="in-console-feedback"></a>Feedback na consola

- `http://petrol.office.microsoft.com`

Para obter mais informações sobre esta funcionalidade, consulte o feedback do [Produto.](../../understand/find-help.md#product-feedback)

### <a name="community-workspace-documentation-node"></a>Espaço de trabalho comunitário, nó de documentação

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Para obter mais informações sobre este nó de consola, consulte [Utilizar a consola do Gestor de Configuração](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Monitorização do espaço de trabalho, nó da hierarquia do site

Se utilizar a **Vista Geográfica,** permita o acesso ao seguinte ponto final:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Análise de Computadores

Para obter mais informações sobre os pontos finais necessários para o serviço de cloud Desktop Analytics, consulte A partilha de [dados enable](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Endereços IP públicos da Microsoft

Para obter mais informações sobre as gamas de endereços IP da Microsoft, consulte [o Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Estes endereços atualizam-se regularmente. Não há granularidade por serviço, qualquer endereço IP nestas gamas poderia ser usado.

## <a name="see-also"></a>Consulte também

- [Portas utilizadas no Gestor de Configuração](../hierarchy/ports.md)

- [Suporte do servidor proxy no Gestor de Configuração](proxy-server-support.md)
