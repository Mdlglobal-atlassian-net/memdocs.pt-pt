---
title: Portas utilizadas para ligações
titleSuffix: Configuration Manager
description: Conheça as portas de rede necessárias e personalizáveis que o Gestor de Configuração utiliza para ligações.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b75ebe7e768080a1239e817c514b634cdcf64179
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587176"
---
# <a name="ports-used-in-configuration-manager"></a>Portas utilizadas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo lista as portas de rede que o Gestor de Configuração utiliza. Algumas ligações utilizam portas que não são configuráveis e algumas portas personalizadas de suporte que especifica. Se utilizar qualquer tecnologia de filtragem da porta, verifique se as portas necessárias estão disponíveis. Estas tecnologias de filtragem de portas incluem firewalls, routers, servidores proxy ou IPsec.

> [!NOTE]  
> Se apoiar clientes baseados na Internet utilizando a ponte SSL, para além dos requisitos da porta, poderá também ter de permitir que alguns verbos e cabeçalhos HTTP atravessem a sua firewall.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Portas que pode configurar

O Gestor de Configuração permite-lhe configurar as portas para os seguintes tipos de comunicação:  

- Site do Catálogo de Aplicações aponta para ponto de serviço web do Catálogo de Aplicações  

- Ponto proxy de registo com o ponto de registo  

- Sistemas cliente-a-site que executam o IIS  

- Cliente para internet (como configurações do servidor proxy)  

- Atualização de software aponta para a internet (como configurações do servidor proxy)  

- Ponto de atualização de software com o servidor WSUS  

- Servidor do site com o servidor da base de dados do site  

- Servidor do site para servidor de base de dados WSUS

- Pontos do Reporting Services  

  > [!NOTE]  
  > As portas que estão a ser utilizadas para a função do sistema de pontos de reporte de serviços de reporte estão configuradas nos Serviços de Reporte de Servidores SQL. Estas portas são então utilizadas pelo Gestor de Configuração durante as comunicações ao ponto de serviços de reporte. Certifique-se de que revê estas portas que definem as informações do filtro IP para as políticas do IPsec ou para configurar firewalls.  

Por padrão, a porta HTTP que é utilizada para a comunicação do sistema cliente-a-site é a porta 80, e a porta HTTPS padrão é 443. As portas para comunicação do sistema cliente-a-site sobre HTTP ou HTTPS podem ser alteradas durante a configuração ou nas propriedades do site para o seu site de Gestor de Configuração.  

As portas que estão a ser utilizadas para a função do sistema de pontos de reporte de serviços de reporte estão configuradas nos Serviços de Reporte de Servidores SQL. Estas portas são então utilizadas pelo Gestor de Configuração durante as comunicações ao ponto de serviços de reporte. Certifique-se de que revê estas portas quando estiver a definir as informações do filtro IP para as políticas do IPsec ou para configurar firewalls.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Portas não configuráveis  

O Gestor de Configuração não lhe permite configurar portas para os seguintes tipos de comunicação:  

- Site para site  

- Servidor do site com o sistema de sites  

- Consola de Gestor de Configuração para Fornecedor SMS  

- Consola de Gestor de Configuração para a internet  

- Ligações a serviços na nuvem, como microsoft Intune e pontos de distribuição na nuvem  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Portas utilizadas por clientes e sistemas de sites do Configuration Manager  

As seguintes secções detalham as portas que são utilizadas para a comunicação no Gestor de Configuração. As setas do título da secção mostram a direção da comunicação:  

- -> indica que um computador inicia a comunicação e o outro responde sempre  

- &lt;-> indica que qualquer computador pode iniciar a comunicação  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a>Ponto de sincronização da Inteligência de Ativos --> Microsoft  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a>Ponto de sincronização da Inteligência de Ativos --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a>Ponto de serviço web do catálogo de aplicações --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a>Ponto de site do catálogo de aplicações --> ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a>Ponto de site do catálogo de aplicações do cliente -->  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a>Cliente --cliente >  

Wake-up proxy também usa mensagens de pedido de eco do ICMP de um cliente para outro cliente. Os clientes usam esta comunicação para confirmar se o outro cliente está acordado na rede. O ICMP é por vezes referido como comandos de ping. O ICMP não tem um número de protocolo UDP ou TCP, pelo que não está listado na tabela abaixo. No entanto, as firewalls baseadas no anfitrião existentes nestes computadores cliente ou em dispositivos de rede intervenientes na sub-rede devem permitir o tráfego ICMP para que a comunicação de proxy de reativação tenha êxito.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|<sup> [9 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  
|Proxy de reativação|25536 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  
|Transmissão de cache Windows PE Peer|8004|--|  
|Download de cache windows PE Peer|--|8003|  

Para mais informações, consulte [O Windows PE Peer Cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a>Módulo de política do Serviço de Inscrição de Dispositivos de Configuração (NDES) do Cliente --> Gestor de Configuração

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a>Cliente --> ponto de distribuição cloud  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para mais informações, consulte [Portos e fluxo de dados.](use-a-cloud-based-distribution-point.md#bkmk_dataflow)

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a>Cliente --> Gateway de gestão da Nuvem (CMG)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para mais informações, consulte [as Portas CMG e o fluxo de dados.](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a>Cliente -> Ponto de Distribuição, tanto padrão como puxar  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|
|Atualizações expressas|--|8005 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Utilize as definições do cliente para configurar a porta alternativa para atualizações expressas. Para mais informações, consulte o [Porto que os clientes usam para receber pedidos de conteúdo delta.](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content)

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a>Cliente -> Ponto de distribuição configurado para multicast, standard e pull  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Protocolo multicast|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a>Cliente --> Ponto de distribuição configurado para PXE, tanto padrão como puxar  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 e 68|--|  
|TFTP|<sup> [69 Nota 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> Se ativar uma firewall baseada no hospedeiro, certifique-se de que as regras permitem que o servidor envie e receba nestas portas. Quando ativa um ponto de distribuição para o PXE, o 'Gestor de Configuração' pode ativar as regras de entrada (receber) na Firewall do Windows. Não configura as regras de saída (enviar).<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a>Cliente -- ponto de estado de recuo >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a>Cliente --> controlador de domínio de catálogo Global

Um cliente do Gestor de Configuração não contacta um servidor de catálogo global quando é um computador de grupo de trabalho ou quando está configurado para comunicação apenas à Internet.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Catálogo global LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a>Cliente -> Ponto de Gestão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Notificação de cliente (comunicação predefinida antes de reverter para HTTP ou HTTPS)|--|10123 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a>Cliente --> ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup> [Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [Nota 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a>Cliente -- ponto de migração do Estado >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a>Ponto de ligação CMG --> serviço de nuvem CMG  

O Gestor de Configuração utiliza estas ligações para construir o canal CMG. Para mais informações, consulte [as Portas CMG e o fluxo de dados.](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (preferido)|--|10140-10155|  
|HTTPS (recuo com um VM)|--|443|  
|HTTPS (recuo com dois ou mais VMs)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a>Ponto de ligação CMG --> Ponto de Gestão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para mais informações, consulte [as Portas CMG e o fluxo de dados.](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a>Ponto de ligação CMG --> ponto de atualização de software  

A porta específica depende da configuração do ponto de atualização do software.

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Para mais informações, consulte [as Portas CMG e o fluxo de dados.](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a>Consola de Gestor de Configuração --Cliente >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Controlo Remoto (controlo)|--|2701|  
|Assistência Remota (RDP e RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a>Consola de Gestor de Configuração --Internet >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

A consola 'Gestor de Configuração' utiliza acesso à Internet para as seguintes ações:

- Descarregando atualizações de software a partir do Microsoft Update para pacotes de implementação.
- O artigo de feedback na fita.
- Links para documentação dentro da consola.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a>Consola de Gestor de Configuração --> ponto de serviços de reporte  

|Descrição|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a>Consola de Gestor de Configuração --> servidor do Site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (ligação inicial ao WMI para localizar o sistema do fornecedor)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a>Consola de Gestor de Configuração --fornecedor de SMS >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a>Módulo de política do Serviço de Inscrição de Dispositivos de Configuração (NDES) --> ponto de registo de certificado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a>Ponto de serviço de armazém de dados --> SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a>Ponto de distribuição, tanto standard como pull --> Ponto de Gestão

Um ponto de distribuição comunica com o ponto de gestão nos seguintes cenários:  

- Para relatar o estado do conteúdo pré-encenado  

- Para reportar dados de resumo de utilização  

- Para reportar validação de conteúdo  

- Para reportar o estado dos downloads de pacotes (apenas ponto de distribuição de puxar)

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a>Ponto de proteção do ponto final -- internet >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a>Ponto de proteção de pontofinal --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a>Ponto de procuração de matrículas --> ponto de matrícula  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a>Ponto de inscrição --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a>Conector de servidor de troca --> troca online  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a>Conector de servidor de troca --> servidor de troca no local  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a>Computador Mac --> ponto de procuração de matrícula  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a>Ponto de gestão -- controlador de domínio >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|LDAP seguro (LDAPS, para assinatura e encadernação)|636|636|  
|Catálogo global LDAP|--|3268|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a>Ponto &lt;de gestão --servidor do Site >

<sup>[Nota 5](#bkmk_note5)</sup>

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a>Ponto de gestão --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a>Dispositivo móvel --> ponto de procuração de matrícula  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a>Ponto de serviços de reporte -- > Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a>Ponto de ligação ao serviço --> Azure (CMG)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS para implementação de serviço CMG|--|443|

Para mais informações, consulte [as Portas CMG e o fluxo de dados.](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a>Site &lt;server --> Ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a>Site &lt;server --> ponto do site do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a>Servidor &lt;do site --> ponto de sincronização da Inteligência de Ativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a>Servidor do site --cliente >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|<sup> [9 Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a>Servidor do site --> ponto de distribuição cloud  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para mais informações, consulte [Portos e fluxo de dados.](use-a-cloud-based-distribution-point.md#bkmk_dataflow)

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a>Servidor do site --> ponto de distribuição, tanto padrão como puxar

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a>Servidor do site --controlador de domínio >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|
|LDAP seguro (LDAPS, para assinatura e encadernação)|636|636|
|Catálogo global LDAP|--|3268|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a>Ponto &lt;de registo do servidor do site -->  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a>Servidor &lt;do site --> ponto de ligação CMG

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a>Servidor &lt;do site --> ponto de proteção do ponto final  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a>Servidor &lt;do site --> ponto de inscrição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a>Servidor &lt;do site --> ponto de procuração de inscrição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a>Servidor &lt;do site --> ponto de estado do Fallback

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a>Servidor do site --internet >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a>Servidor &lt;do site --autoridade de certificação emissora de > (CA)

Esta comunicação é utilizada na implementação de perfis de certificado, utilizando o ponto de registo de certificados. A comunicação não é usada para todos os servidores do site na hierarquia. Em vez disso, é usado apenas para o servidor do site no topo da hierarquia.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC (DCOM)|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a>Servidor do site --> Server hospedando partilha de biblioteca de conteúdo remoto

Pode mover a biblioteca de conteúdos para outro local de armazenamento para libertar espaço de disco rígido na sua administração central ou servidores de sites primários. Para mais informações, consulte [Configure uma biblioteca de conteúdos remotos para o servidor do site](the-content-library.md#bkmk_remote).

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a>Ponto &lt;de ligação do servidor do site -->

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a>Ponto &lt;de serviços de reporte do servidor do site -->

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a>Servidor &lt;do site --servidor do site >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a>Servidor do site --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

Durante a instalação de um site que utiliza um Servidor SQL remoto para alojar a base de dados do site, abra as seguintes portas entre o servidor do site e o Servidor SQL:  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a>Servidor do site --> Servidor SQL para WSUS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 3 Porta](#bkmk_note3) alternativa disponível</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a>Servidor de site --> Fornecedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|<sup> [Nota](#bkmk_note6) DINÂMICA 6</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a>Site &lt;server --> ponto de atualização de software

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|HTTP|--|80 ou 8530 <sup> [Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [Nota 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a>Servidor &lt;do site --> ponto de migração do Estado

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a>Provedor SMS --> Servidor SQL  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a>Ponto de atualização de software --internet >  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|<sup> [80 Nota 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a>Ponto de atualização de software --> servidor WSUS upstream  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup> [Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [Nota 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

A replicação da base de dados intersite requer que o Servidor SQL num só site se comunique diretamente com o Servidor SQL no seu site principal ou infantil.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Serviço SQL Server|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|SQL Server Service Broker|--|4022 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

> [!TIP]  
> O Gestor de Configuração não requer o Navegador servidor SQL, que utiliza a porta UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a>Ponto de migração do Estado --> SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [Nota 2](#bkmk_note2) Porta alternativa disponível</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Notas relativas às portas utilizadas por clientes e sistemas de sites do Configuration Manager  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a>Nota 1: Porta do servidor proxy

Esta porta não pode ser configurada, mas pode ser encaminhada através de um servidor proxy configurado.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a>Nota 2: Porta alternativa disponível

Pode definir uma porta alternativa no Gestor de Configuração para este valor. Se definir uma porta personalizada, utilize essa porta personalizada na informação do filtro IP para as políticas do IPsec ou para configurar firewalls.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a>Nota 3: Serviços de Atualização do Servidor do Windows (WSUS)

A WSUS pode ser instalada para utilizar as portas 80/443 ou as portas 8530/8531 para comunicação do cliente. Quando executa o WSUS no Windows Server 2012 ou no Windows Server 2016, o WSUS está configurado por padrão para utilizar a porta 8530 para HTTP e a porta 8531 para HTTPS.  

Após a instalação, é possível alterar a porta. Não é preciso usar o mesmo número de porta em toda a hierarquia do site.  

- Se a porta HTTP for 80, a porta HTTPS tem de ser 443.  

- Se a porta HTTP for outra coisa, a porta HTTPS deve ser 1 ou superior, por exemplo, 8530 e 8531.

    > [!NOTE]  
    >  Quando configura o ponto de atualização de software para utilizar HTTPS, a porta HTTP também tem de estar aberta. Os dados não encriptados, como o EULA para atualizações específicas, utilizam a porta HTTP.

- O servidor do site faz uma ligação ao servidor SQL que acolhe o SUSDB quando ativa as seguintes opções para a limpeza wSUS:
  - Adicione índices não agrupados à base de dados wSUS para melhorar o desempenho da limpeza wSUS
  - Remova atualizações obsoletas da base de dados wSUS
  
  Se a porta padrão do Servidor SQL for alterada para uma porta alternativa com o SQL Server Configuration Manager, certifique-se de que o servidor do site pode ligar-se utilizando a porta definida. O Gestor de Configuração não suporta portas dinâmicas. Por padrão, as instâncias nomeadas pelo SQL Server utilizam portas dinâmicas para ligações ao motor de base de dados. Quando utilizar uma instância nomeada, configure manualmente a porta estática.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a>Nota 4: FtP trivial (TFTP) Daemon

O serviço de sistema Daemon Trivial FTP (TFTP) não requer um nome de utilizador ou senha e é parte integrante dos Serviços de Implementação do Windows (WDS). O serviço Trivial FTP Daemon implementa suporte para o protocolo TFTP definido pelos seguintes RFCs:  

- RFC 1350: TFTP  

- RFC 2347: Extensão de opção  

- RFC 2348: Opção de tamanho do bloco  

- RFC 2349: Intervalo de tempo e opções de tamanho de transferência  

A TFTP foi concebida para suportar ambientes de arranque sem discos. Os Daemons TFTP escutam a porta UDP 69 mas respondem a partir de uma porta alta alocada dinamicamente. Se ativar esta porta, o serviço TFTP pode receber pedidos TFTP, mas o servidor selecionado não pode responder a esses pedidos. Não é possível ativar o servidor selecionado para responder aos pedidos TFTP de entrada, a menos que configure o servidor TFTP para responder a partir da porta 69.  

O ponto de distribuição ativado pelo PXE e o cliente no Windows PE selecionam portas altas dinamicamente atribuídas para transferências TFTP. Estas portas são definidas pela Microsoft entre 49152 e 65535. Para mais informações, consulte a visão geral do [serviço e os requisitos](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows) da porta de rede para windows

No entanto, durante a bota PXE real, o cartão de rede no dispositivo seleciona a porta alta dinamicamente atribuída que utiliza durante a transferência do TFTP. O cartão de rede do dispositivo não está ligado às portas altas dinamicamente atribuídas definidas pela Microsoft. Só está ligado às portas definidas no RFC 1350. Este porto pode ser de 0 a 65535. Para obter mais informações sobre as portas altas dinamicamente atribuídas que o cartão de rede utiliza, contacte o fabricante de hardware do dispositivo.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a>Nota 5: Comunicação entre o servidor do site e os sistemas do site

Por padrão, a comunicação entre o servidor do site e os sistemas do site é bidirecional. O servidor do site inicia a comunicação para configurar o sistema do site e, em seguida, a maioria dos sistemas do site conectam-se de volta ao servidor do site para enviar informações de estado. Os pontos de serviço de reporte e os pontos de distribuição não enviam informações sobre o estado. Se selecionar **Exigir que o servidor do site inicie ligações a este sistema** de site nas propriedades do sistema do site após a instalação do sistema do site, o sistema do site não iniciará a comunicação com o servidor do site. Em vez disso, o servidor do site inicia a comunicação. Utiliza a conta de instalação do sistema do site para autenticação no servidor do sistema do site.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a>Nota 6: Portas dinâmicas

As portas dinâmicas utilizam uma gama de números de porta definidos pela versão S. Estes portos também são conhecidos como portos efémeros. Para mais informações sobre os intervalos de portas predefinidos, consulte [Descrição geral do serviço e requisitos de portas de rede para o Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a>Listas adicionais de portos  

As seguintes secções fornecem informações adicionais sobre as portas que o Gestor de Configuração utiliza.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Partilhas de cliente para servidor

Os clientes utilizam o Bloco de Mensagens de Servidor (SMB) sempre que ligam a partilhas UNC. Por exemplo:

- Instalação manual do cliente que especifica o CCMSetup.exe **/fonte:** propriedade de linha de comando  

- Clientes endpoint Protection que descarregam ficheiros de definição de um caminho unc

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a>Ligações ao Microsoft SQL Server

Para comunicação com o motor de base de dados do SQL Server e para replicação entre sites, pode utilizar a porta predefinida do SQL Server ou especificar portas personalizadas:  

- As comunicações entre sites utilizam:  

  - SQL Server Service Broker, que utiliza por predefinição a porta TCP 4022.  

  - Serviço SQL Server, que se incorre na porta TCP 1433.  

- A comunicação intra-local entre o motor de base de dados do Servidor SQL e várias funções do sistema do site do Gestor de Configuração falha na porta TCP 1433.  

- O Gestor de Configuração utiliza as mesmas portas e protocolos para comunicar com cada réplica do Grupo de Disponibilidade SQL que acolhe a base de dados do site como se a réplica fosse uma instância autónoma do Servidor SQL.

Quando utilizar o Azure e a base de dados do site estiver por trás de um equilibrador de carga interno ou externo, configure os seguintes componentes:

- Exceções de firewall em cada réplica
- Regras de equilíbrio de carga

Configure as seguintes portas:

- SQL sobre TCP: TCP 1433
- Corretor de serviço sql server: TCP 4022
- Bloco de mensagens de servidor (SMB): TCP 445
- Mapper de ponto final RPC: TCP 135

> [!WARNING]  
> O Gestor de Configuração não suporta portas dinâmicas. por padrão, o SQL Server nomeou instâncias que utilizam portas dinâmicas para ligações ao motor de base de dados. Quando utilizar uma instância nomeada, configure manualmente a porta estática para comunicação intralocal.  

As seguintes funções do sistema de sites comunicam diretamente com a base de dados do SQL Server:  

- Ponto de serviço Web do Catálogo de Aplicações  

- Função de ponto de registo de certificados  

- Função de ponto de registo  

- Ponto de gestão  

- Servidor do site  

- Ponto do Reporting Services  

- Fornecedor de SMS  

- Servidor SQL --> Servidor SQL  

Quando um Servidor SQL acolhe uma base de dados de mais de um site, cada base de dados deve utilizar uma instância separada do Servidor SQL. Configure cada instância com um conjunto único de portas.  

Se ativar uma firewall baseada no hospedeiro no servidor SQL, configure-a para permitir as portas corretas. Configure também firewalls de rede entre computadores que comunicam com o servidor SQL.  

Para um exemplo de como configurar o SQL Server para utilizar uma porta específica, consulte [configurar um servidor para ouvir uma porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Descoberta e publicação

O Gestor de Configuração utiliza as seguintes portas para a descoberta e publicação de informações do site:

- Protocolo de Acesso ao Diretório Leve (LDAP): 389
- LDAP seguro (LDAPS, para assinatura e encadernação): 636
- Catálogo global LDAP: 3268
- Mapper de ponto final RPC: 135
- RPC: Portas TCP altas dinamicamente atribuídas
- TCP: 1024: 5000
- TCP: 49152: 65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Ligações externas efetuadas pelo Configuration Manager

No local, os clientes ou sistemas de site do Gestor de Configuração podem efendo as seguintes ligações externas:  

- [Ponto de sincronização da&gt; Inteligência de Ativos -- Microsoft](#BKMK_PortsAI)  

- [Ponto de proteção&gt; de pontofinal - Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Cliente --&gt; Controlador global de domínio de catálogo](#BKMK_PortsClient-GCDC)  

- [Consola de Gestor&gt; de Configuração -- Internet](#BKMK_PortsConsole-Internet)  

- [Ponto de&gt; gestão -- Controlador de domínio](#BKMK_PortsMP-DC)  

- [Servidor do&gt; site -- Controlador de domínio](#BKMK_PortsSite-DC)  

- [Autoridade &lt;  -- &gt; de Certificação emissora de servidor estoque (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Ponto de atualização de software --&gt; Internet](#BKMK_PortsSUP-Internet)  

- [Ponto de atualização de software --&gt; Upstream WSUS Server](#BKMK_PortsSUP-WSUS)  

- [Ponto de ligação de serviço --> Azure](#bkmk_scp-cmg)  

- [Ponto de ligação CMG --> serviço de nuvem CMG](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a>Requisitos de instalação para sistemas de sites que suportam clientes baseados na Internet

> [!Note]  
> Esta secção aplica-se apenas à gestão de clientes baseadona na Internet (CMI). Não se aplica ao portal de gestão de nuvens. Para mais informações, consulte [Gerir clientes na internet.](../../clients/manage/manage-clients-internet.md)  

Pontos de gestão baseados na Internet, pontos de distribuição que suportam clientes baseados na Internet, o ponto de atualização de software e o ponto de estado de recuo utilizam as seguintes portas para instalação e reparação:  

- Servidor do site --> sistema do Site: Mapper de ponto final RPC utilizando a porta UDP e TCP 135.  

- Servidor do site --> Sistema do Site: Portas TCP dinâmicas RPC  

- Servidor &lt; do site --> sistema de site: Blocos de mensagens do servidor (SMB) utilizando a porta TCP 445

As instalações de aplicações e pacotes em pontos de distribuição exigem as seguintes portas RPC:  

- Servidor do site --> Ponto de distribuição: mapper de ponto final rPC utilizando a porta UDP e TCP 135

- Servidor do site --> Ponto de distribuição: portas TCP dinâmicas RPC  

Utilize o IPsec para ajudar a proteger o tráfego entre o servidor do site e os sistemas de sites. Se tiver de restringir as portas dinâmicas utilizadas com RPC, pode utilizar a ferramenta de configuração Do RPC da Microsoft (rpccfg.exe). Utilize a ferramenta para configurar uma gama limitada de portas para estes pacotes RPC. Para mais informações, consulte [Como configurar o RPC para utilizar certas portas e como ajudar a proteger essas portas utilizando o IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Antes de instalar estes sistemas de site, certifique-se de que o serviço de registo remoto está a funcionar no servidor do sistema do site e que especificou uma conta de instalação do sistema de site se o sistema do site estiver numa floresta de Diretório Ativo diferente sem uma relação de confiança. Por exemplo, o serviço de registo remoto é utilizado em servidores que executam sistemas de sites, tais como pontos de distribuição (puxar e standard), servidores SQL remotos e o Catálogo de Aplicações.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Portas utilizadas pela instalação do cliente do Configuration Manager

As portas que o Gestor de Configuração utiliza durante a instalação do cliente dependem do método de implantação.

- Para obter uma lista de portas para cada método de implementação de clientes, consulte [Portas utilizadas durante](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment) a implementação do cliente do Gestor de Configuração  

- Para obter mais informações sobre como configurar o Windows Firewall no cliente para instalação de clientes e comunicação pós-instalação, consulte as [definições do Windows Firewall e da porta para os clientes](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Portas utilizadas pela migração

O servidor do site que executa a migração utiliza várias portas para se conectar aos sites aplicáveis na hierarquia de origem. Para mais informações, consulte [as configurações necessárias para a migração](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a>Portas utilizadas pelo Windows Server

A tabela seguinte lista algumas das portas-chave utilizadas pelo Windows Server.

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 e 68|--|  
|Resolução de Nomes NetBIOS|137|--|  
|Serviço de Datagrama NetBIOS|138|--|  
|Serviço de Sessão NetBIOS|--|139|  
|Autenticação Kerberos|--|88|

Para obter mais informações, veja os artigos seguintes:

- [Visão geral do serviço e requisitos de porta de rede para o sistema Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Como configurar uma firewall para domínios e fidedignidades](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
