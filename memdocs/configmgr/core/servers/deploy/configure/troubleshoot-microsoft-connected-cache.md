---
title: Cache conectado de resolução de problemas
titleSuffix: Configuration Manager
description: Detalhes técnicos para a Microsoft Connected Cache para ajudá-lo a resolver problemas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a8c975798c506339a981e8648003387dc1e9838
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878104"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Problemas de resolução de cache conectados da Microsoft no gestor de configuração

Este artigo fornece detalhes técnicos sobre o Microsoft Connected Cache no Gestor de Configuração. Use-o para ajudar a resolver problemas que possa ter no seu ambiente. Para obter mais informações sobre como funciona e como usá-lo, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](../../../plan-design/hierarchy/microsoft-connected-cache.md)

> [!NOTE]
> A partir da versão 1910, esta funcionalidade chama-se **Microsoft Connected Cache**. Anteriormente era conhecido como Delivery Optimization In-Network Cache.

## <a name="verify"></a>Verificar

Quando instala corretamente o servidor de cache de Otimização de Entregas e configura corretamente os clientes, eles descarregam a partir do servidor de cache instalado no seu ponto de distribuição e não na internet.

Verifique este comportamento [num cliente](#bkmk_verify-client) ou [no servidor](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a>Verifique um cliente

1. No cliente que executa o Windows 10, versão 1809 ou mais tarde, descarregue conteúdo gerido pela cloud. Para obter mais informações sobre os tipos de conteúdo que a Connected Cache suporta, consulte [Verificar A Cache Conectada](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Abra a PowerShell e execute o seguinte comando:`Get-DeliveryOptimizationStatus`

Por exemplo:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Note que o `BytesFromCacheServer` atributo não é zero.

Se o cliente não estiver configurado corretamente, ou se o servidor cache não estiver instalado corretamente, o cliente de Otimização de Entrega recai para a fonte original da nuvem. Em seguida, o atributo BytesFromCacheServer será zero.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a>Verifique no servidor

Primeiro, verifique se as propriedades do registo estão corretamente configuradas: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` . Por exemplo, a localização da cache de acionamento `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` é, onde `PrimaryDrivesInput` podem ser múltiplas unidades, tais como `C,D,E` .

Em seguida, utilize o seguinte método para simular um pedido de descarregamento de cliente para o servidor com os cabeçalhos obrigatórios.

1. Abra uma janela PowerShell de 64 bits como administrador.
2. Executar o seguinte comando e substituir o nome ou endereço IP do seu servidor `<DoincServer>` para:

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

A saída é semelhante ao seguinte exemplo:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Os seguintes atributos indicam sucesso:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Ficheiros de registo

- Diário de conjunto ARR:`%temp%\arr_setup.log`

- Registo de configuração do servidor de cache DO: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` no ponto de distribuição e no servidor do `DistMgr.log` site

- Registos operacionais IIS: Por defeito,`%SystemDrive%\inetpub\logs\LogFiles`

- Registo operacional do servidor de cache DO:`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Entre outras utilizações, este log pode ajudá-lo a identificar problemas de conectividade com a nuvem da Microsoft.

## <a name="setup-error-codes"></a>Códigos de erro de configuração

Quando o Gestor de Configuração instala o componente 'Cache Connected' no ponto de distribuição, a tabela seguinte lista os possíveis códigos de erro que podem ocorrer:

| Código de erro | Descrição do erro |
|------------|-------------------|
| 0x00000000 | Êxito |
| 0x000000BC2 | Sucesso, reinicialização necessária |
| 0x00000643 | Falha de instalação genérica |
| 0x00D00001 | A configuração de Cache conectada só pode ser executada se os Serviços de Informação da Internet (IIS) forem instalados |
| 0x00D000002 | A configuração de Cache conectada só pode ser executada se existir um 'Web Site predefinido' no servidor |
| 0x00D00003 | Não é possível instalar cache conectado se o pedido de pedido de pedido de encaminhamento (ARR) já estiver instalado |
| 0x00D00004 | A configuração de Cache conectada só pode ser executada se o Pedido de Pedido de Pedido de Pedido de Pedido de Pedido de Pedido de Aplicação (ARR) tiver sido instalado pelo script Install.ps1 |
| 0x00D00005 | Configuração de Cache Conectada requer uma sessão powerShell em execução como Administrador |
| 0x00D00006 | A configuração de Cache conectada só pode ser executada a partir de um ambiente PowerShell de 64 bits |
| 0x00D000007 | A configuração de Cache conectada só pode ser executada num Servidor windows |
| 0x00D00008 | Falha: O número de unidades de cache especificadas deve corresponder ao número de percentagens de tamanho de unidade de cache especificadas |
| 0x00D00009 | Falha: Deve ser fornecido um ID válido do nó de cache |
| 0x00D0000A | Falha: Deve ser fornecido um conjunto de unidade de cache válido |
| 0x00D0000B | Falha: Deve ser fornecido um conjunto de tamanho por cento de unidade de cache válido |
| 0x00D0000C | Falha: Deve ser fornecido um conjunto de tamanho de unidade de cache válido ou tamanho de unidade de cache em GB |
| 0x00D0000D | Falha: Um conjunto de tamanho de unidade de cache válido e tamanho de unidade de cache em GB não pode ser fornecido |
| 0x00D0000E | Falha: O número de unidades de cache especificadas deve corresponder ao número de tamanho da unidade de cache em GB especificado |
| 0x00D0000F | Falha: Não conseguiu fazer o backup o ficheiro applicationhost.config de $AppHostConfig a $AppHostConfigDestinationName |
| 0x00D00010 | Failure: Couldn't back up the Default Web Site web.config file from $WebsiteConfigFilePath to $WebConfigDestinationName |
| 0x00D00011 | Falha: Ocorreu uma exceção em SetupARRWebFarm.ps1 |
| 0x00D00012 | Falha: Ocorreu uma exceção em SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Falha: Ocorreu uma exceção em SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Falha: Ocorreu uma exceção em ConfiguraçãoAllowableServerVariables.ps1 |
| 0x00D00015 | Falha: Ocorreu uma exceção em SetupFirewallRules.ps1 |
| 0x00D00016 | Falha: Ocorreu uma exceção em SetupAppPoolProperties.ps1 |
| 0x00D00017 | Falha: Ocorreu uma exceção em SetupARROutboundRules.ps1 |
| 0x00D00018 | Falha: Ocorreu uma exceção em SetupARRDiskCache.ps1 |
| 0x00D00019 | Falha: Ocorreu uma exceção em SetupARRProperties.ps1 |
| 0x00D0001A | Falha: Ocorreu uma exceção em SetupARRHealthProbes.ps1 |
| 0x00D0001B | Falha: Ocorreu uma exceção em CheckIISSItesStarted.ps1 |
| 0x00D0001C | Falha: Ocorreu uma exceção em SetDrivesToHealthy.ps1 |
| 0x00D0001D | Falha: Ocorreu uma exceção em CheckCacheNodeSetup.ps1 |
| 0x00D0001E | Não pode instalar a Cache Conectada se o Web Site padrão não estiver na porta 80 |
| 0x00D0001F | Falha: A atribuição da unidade de cache em percentagem não pode exceder 100 |
| 0x00D00020 | Falha: A atribuição da unidade de cache em GB não pode exceder o espaço livre da unidade |
| 0x00D00021 | Falha: A atribuição da unidade de cache em percentagem deve ser superior a 0 |
| 0x00D00022 | Falha: A atribuição da unidade de cache em GB deve ser superior a 0 |
| 0x00D00023 | Falha: Ocorreu uma exceção em RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Falha: Ocorreu uma exceção em RegisterScheduledTask_Maintenance |
| 0x00D00025 | Falha: Ocorreu uma exceção que estabelece as regras de reescrita para a quinta HTTPS: $FarmName |
| 0x00D00026 | Falha: Ocorreu uma exceção que estabelece as regras de reescrita para a exploração HTTP: $FarmName |
| 0x00D00027 | Não é possível instalar a Cache Conectada porque o software dependente "Request Request Routing (ARR)" não foi instalado. Consulte o ficheiro de registo localizado em %temporário%\arr_setup.log |

## <a name="iis-configurations"></a>Configurações iIS

A instalação do servidor de cache DO faz várias modificações na configuração IIS no ponto de distribuição.

### <a name="application-request-routing"></a>Encaminhamento de pedido de pedido

O servidor de cache DO instala e configura o Encaminhamento de Pedido de Pedido de Pedido de Pedido de Aplicação IIS [(ARR)](https://www.iis.net/downloads/microsoft/application-request-routing). Para evitar potenciais conflitos, o ponto de distribuição já não pode ter este componente instalado.

### <a name="allowed-server-variables"></a>Variáveis permitidas do servidor

Depois de instalar o servidor de cache DO, o web site predefinido tem as seguintes variáveis do servidor *local:*

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>Reescrever regras

O servidor cache DO adiciona as seguintes regras de reescrita:

#### <a name="inbound-rewrite-rules"></a>Regras de reescrita de entrada

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Regras de reescrita de saída

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Gerir os recursos do servidor

O espaço de disco necessário para cada servidor de cache DO pode variar, de acordo com os requisitos de atualização da sua organização. 100 GB deve ser espaço suficiente para cache o seguinte conteúdo:

- Uma atualização de funcionalidade
- Dois a três meses de atualizações de qualidade e escritório
- Aplicações Microsoft Intune e aplicativos de caixa de entrada Windows

O servidor de cache DO não deve consumir muita memória do sistema ou tempo de processador. Depois de instalar o servidor de cache DO, se notar um processo significativo ou consumo de recursos de memória, analise os ficheiros de registo IIS e ARR.

Se os ficheiros de registo IIS e ARR ocuparem demasiado espaço no servidor, existem vários métodos que pode utilizar para gerir os ficheiros de registo. Para mais informações, consulte [Managing IIS Log File Storage](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Consulte também

[Cache conectado da Microsoft no gestor de configuração](../../../plan-design/hierarchy/microsoft-connected-cache.md)
