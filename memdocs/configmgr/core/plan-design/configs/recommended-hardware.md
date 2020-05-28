---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenha recomendações de hardware para ajudá-lo a escalar o seu ambiente de Gestor de Configuração para além de uma implementação básica.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428788"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware recomendado para o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

As seguintes recomendações são orientações para ajudá-lo a escalar o seu ambiente de Gestor de Configuração para suportar mais do que uma implementação muito básica de sites, sistemas de sites e clientes. Não se destinam a cobrir todas as configurações possíveis do site e da hierarquia.  

Utilize as informações nas seguintes secções como guia para o ajudar a planear hardware. Certifique-se de que o seu hardware pode atender as cargas de processamento para clientes e sites que utilizam as funcionalidades disponíveis do Gestor de Configuração.

Para mais informações, consulte o desempenho do Gestor de Configuração e a escala de [orientação whitepaper](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Sistemas de site

Esta secção fornece configurações de hardware recomendadas para sistemas de configuração do gestor. Utilize estas recomendações para suportar o número máximo de clientes e utilize a maioria ou todas as funcionalidades do Gestor de Configuração. Se o seu ambiente suporta menos do que o número máximo de clientes, e não utilizar todas as funcionalidades disponíveis, pode exigir menos recursos. Em geral, os seguintes factores-chave limitam o desempenho do sistema global:

1. Desempenho da E/S do disco

2. Memória disponível

3. CPU

Para um melhor desempenho, utilize configurações RAID 10 para todas as unidades de dados e uma rede Ethernet de 1-Gbps.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Servidores do site

|Configuração do site|CPU (núcleos)|Memória (GB)|Atribuição de memória para O Servidor SQL (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de site primário autónomo com uma função de site de base de dados no mesmo servidor <sup> [Note 1](#bkmk_note1)</sup>|16|96|80|  
|Servidor de site primário autónomo com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário autónomo|16|72|90|  
|Servidor de site da administração central com uma função de site de base de dados no mesmo servidor <sup> [Note 1](#bkmk_note1)</sup>|20|128|80|  
|Servidor de site de administração central com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota de um site de administração central|16|96|90|  
|Site primário infantil com uma função de site de base de dados no mesmo servidor|16|96|80|  
|Servidor de site primário subordinado com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário subordinado|16|72|90|  
|Servidor do Site Secundário|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a>Nota 1: SQL collocalizado

Quando instala o servidor do site e o Servidor SQL no mesmo computador, a implementação suporta os números máximos de [dimensionamento e escala](size-and-scale-numbers.md) para sites e clientes. Esta configuração pode limitar [opções de alta disponibilidade,](../../servers/deploy/configure/high-availability-options.md)como usar um cluster SQL Server. Se tiver um ambiente maior, devido aos requisitos de I/S mais elevados para suportar ambas as funções no mesmo computador, considere utilizar um Servidor SQL remoto.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Servidores de sistema de site remoto

A seguinte orientação é para computadores que detêm uma única função do sistema do site. Planeie ajustar-se quando instalar várias funções do sistema do site no mesmo computador.

|Função do sistema de sites|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Ponto de gestão|4|8|50|  
|Ponto de distribuição|2|8|Conforme exigido pelo S e para armazenar conteúdo que implementa|  
|Ponto de atualização de software <sup> [Nota 2](#bkmk_note2)</sup>|8|16|Conforme exigido pelo SO e para armazenar atualizações que implementa|  
|Todas as outras funções do sistema de sites|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a>Nota 2: Configurações wSUS

O computador que acolhe um ponto de atualização de software requer as seguintes configurações para piscinas de aplicações IIS:  

- Aumente o comprimento da **fila WsusPool** para **2000**.  

- Aumente o **limite de Memória Privada WsusPool** em quatro vezes, ou coloque-o em **0** (ilimitado).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Espaço em disco para sistemas de sites

A locação e configuração do disco contribuem para o desempenho do Gestor de Configuração. Como cada ambiente do Gestor de Configuração é diferente, os valores que implementa podem variar a partir da seguinte orientação.

Para obter o melhor desempenho, coloque cada objeto num volume RAID separado e dedicado. Para todos os volumes de dados para O Gestor de Configuração e os seus ficheiros de base de dados, utilize o RAID 10 para o melhor desempenho.

|Utilização de dados|Espaço mínimo em disco|25 000 clientes|50 000 clientes|100 000 clientes|150 000 clientes|700.000 clientes (site da administração central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Aplicação de Gestor de Configuração e ficheiros de registo|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Ficheiro .mdf da base de dados do site|75 GB para cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Ficheiro .ldf da base de dados do site|25 GB para cada 25 000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Ficheiros da base de dados temporária (.mdf e .ldf)|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|  

Para o disco do sistema Windows, consulte a orientação de dimensionamento para a versão OS instalada.

Para conteúdo em pontos de distribuição, depende das suas implementações. Esta orientação não inclui o espaço de disco necessário para a biblioteca de conteúdos no servidor do site ou pontos de distribuição. Para mais informações, consulte a biblioteca de [conteúdos.](../../../core/plan-design/hierarchy/the-content-library.md)

Quando planeia requisitos de espaço em disco, considere as seguintes orientações adicionais:

- Cada cliente requer aproximadamente 5-10 MB de espaço na base de dados. Este número depende do tipo de hierarquia, da configuração e do número de clientes. O tamanho é geralmente menor para ambientes maiores. Sites menores têm maior uso de base de dados por cliente.<!-- SCCMDocs#1048 -->

- Para a base de dados temporária do site primário, planeie um tamanho combinado que seja de 25% a 30% da base de dados do site .ficheiro mdf. O tamanho real pode ser menor ou maior. Depende do desempenho do servidor do site e do volume de dados de entrada durante períodos de tempo curtos e longos.

  > [!NOTE]
  > Quando tiver 50.000 ou mais clientes num site, planeie utilizar quatro ou mais ficheiros de base de dados temporárias .mdf.

- O tamanho da base de dados temporária para um site de administração central é tipicamente muito menor do que para um site primário.

- Se utilizar o SQL Server Express para a base de dados do site secundário, limita o tamanho da base de dados a 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>Clientes

Esta secção fornece configurações de hardware recomendadas para computadores que gere utilizando o software cliente do Gestor de Configuração.

### <a name="client-for-windows-computers"></a>Cliente para computadores Windows

Os seguintes requisitos mínimos são para computadores baseados no Windows que gere utilizando o Gestor de Configuração, incluindo edições incorporadas:

- **Processador e memória:** Consulte os requisitos do processador e ram para o Os.

- **Espaço em disco:** 500 MB de espaço de disco disponível, com 5 GB recomendados para a cache do cliente do Gestor de Configuração. Se utilizar configurações personalizadas para instalar o cliente do Gestor de Configuração, é necessário menos espaço em disco.

  - Utilize a propriedade cliente.msi **SMSCACHESIZE** para definir um tamanho de cache inferior ao padrão de 5120 MB. O tamanho mínimo é de 1 MB. O exemplo seguinte cria uma cache de 2 MB:`CCMSetup.exe SMSCACHESIZE=2`

    Para mais informações, consulte sobre as propriedades de [instalação do cliente.](../../../core/clients/deploy/about-client-installation-properties.md)

    > [!TIP]
    > Instalar o cliente com um espaço em disco mínimo é útil para os dispositivos Windows Embedded que, geralmente, têm um espaço em disco menor do que os computadores Windows padrão.

Os seguintes requisitos mínimos de hardware são para funcionalidade opcional no Gestor de Configuração:

- **Implantação do OS:** Pelo menos 384 MB de RAM

- **Centro de Software:** Pelo menos um processador de 500 MHz

- **Controlo Remoto:** Para uma experiência ideal, pelo menos um Pentium 4 Hyper-Threaded 3 GHz (núcleo único) ou CPU comparável, com pelo menos 1-GB de RAM.

### <a name="client-for-linux-and-unix"></a>Cliente para Linux e UNIX

Os seguintes requisitos mínimos são para os servidores Linux e UNIX que gere com o Gestor de Configuração.

|Requisito|Detalhes|  
|-----------------|-------------|  
|Processador e memória|Consulte os requisitos do processador e ram para o SISTEMA do computador.|  
|Espaço em disco|500 MB de espaço de disco disponível, com 5 GB recomendados para a cache do cliente do Gestor de Configuração.|  
|Conectividade de rede|Os computadores clientes do Gestor de Configuração devem ter conectividade de rede com os sistemas de site do Gestor de Configuração para permitir a gestão.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Consola de Gestor de Configuração

Aplicam-se os seguintes requisitos mínimos de hardware a cada computador que executa a consola Do Gestor de Configuração:

- Intel i3 ou CPU comparável  

- 2 GB de RAM  

- 2 GB de espaço em disco  

|Definição PPP|Resolução mínima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Implementações de laboratórios

Utilize as seguintes recomendações mínimas de hardware para implementações laboratoriais e de teste do Diretor de Configuração. Estas recomendações aplicam-se a todos os tipos de site, até 100 clientes:  

|Função|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor do site e da base de dados|2 - 4|8 - 12|100|  
|Servidor do sistema de sites|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
