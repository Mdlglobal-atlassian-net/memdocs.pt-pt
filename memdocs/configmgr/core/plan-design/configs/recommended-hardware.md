---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenha recomendações de hardware para ajudá-lo a escalar o seu ambiente de Gestor de Configuração para além de uma implementação básica.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719163"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware recomendado para o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

As seguintes recomendações são orientações para ajudá-lo a escalar o seu ambiente de Gestor de Configuração para suportar mais do que uma implementação muito básica de sites, sistemas de sites e clientes. Estas recomendações não pretendem abranger todas as configurações de sites e hierarquias possíveis.  

Utilize as informações nas seguintes secções como um guia para ajudá-lo a planear hardware que possa atender as cargas de processamento para clientes e sites que usam as funcionalidades do Gestor de Configuração disponíveis com as configurações padrão.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Sistemas de site  
Esta secção fornece configurações de hardware recomendadas para sistemas de site do Gestor de Configuração para implementações que suportam o número máximo de clientes e utilizam a maioria ou todas as funcionalidades do Gestor de Configuração. As implementações que suportam menos do que o número máximo de clientes e não utilizam todas as funcionalidades disponíveis podem requerer menos recursos informáticos. Em geral, os principais fatores que limitam o desempenho do sistema global incluem o seguinte, por ordem:  

1.  Desempenho da E/S do disco  

2.  Memória disponível  

3.  CPU  

Para um melhor desempenho, utilize configurações RAID 10 para todas as unidades de dados e uma rede Ethernet de 1-Gbps.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Servidores do site  

|Configuração do site|CPU (núcleos)|Memória (GB)|Atribuição de memória para O Servidor SQL (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de site primário autónomo com uma função de site de base de dados no mesmo servidor<sup>1</sup>|16|96|80|  
|Servidor de site primário autónomo com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário autónomo|16|72|90|  
|Servidor de site da administração central com uma função de site de base de dados no mesmo servidor<sup>1</sup>|20|128|80|  
|Servidor de site de administração central com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota de um site de administração central|16|96|90|  
|Site primário infantil com uma função de site de base de dados no mesmo servidor|16|96|80|  
|Servidor de site primário subordinado com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário subordinado|16|72|90|  
|Servidor do Site Secundário|8|16|-|  

<sup>1</sup> Quando o servidor do site e o Servidor SQL são instalados no mesmo computador, a implementação suporta os números máximos de [dimensionamento e escala](size-and-scale-numbers.md) para sites e clientes. Mas esta configuração pode limitar opções de alta disponibilidade para O Gestor de [Configuração,](../../servers/deploy/configure/high-availability-options.md)como usar um cluster De SQL Server. Além disso, devido aos requisitos de I/S mais elevados que são necessários para suportar tanto o Servidor SQL como o servidor do site do Gestor de Configuração quando estiver a executar ambos no mesmo computador, é uma boa ideia considerar a utilização de uma configuração com uma máquina de servidor SQL remota se tiver uma implementação maior.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Servidores de sistema de site remoto  
A seguinte orientação é para computadores que detêm uma única função do sistema do site. Planeie efetuar ajustes quando instalar várias funções de sistema de sites no mesmo computador.  

|Função do sistema de sites|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Ponto de gestão|4|8|50|  
|Ponto de distribuição|2|8|Conforme exigido pelo sistema operativo e para armazenar conteúdo que implementa|  
|Ponto de atualização de software<sup>1</sup>|8|16|Conforme exigido pelo sistema operativo e para armazenar atualizações que implementa|  
|Todas as outras funções do sistema de sites|4|8|50|  

<sup>1</sup> O computador que acolhe um ponto de atualização de software requer as seguintes configurações para piscinas de aplicações IIS:  

- Aumente o comprimento da **fila WsusPool** para **2000**.  

- Aumente o **limite de Memória Privada WsusPool** em quatro vezes, ou coloque-o em **0** (ilimitado).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Espaço em disco para sistemas de sites  
A atribuição e configuração do disco contribui para o desempenho do Gestor de Configuração. Como cada ambiente do Gestor de Configuração é diferente, os valores que implementa podem variar a partir da seguinte orientação.  

Para obter o melhor desempenho, coloque cada objeto num volume RAID separado e dedicado. Para todos os volumes de dados (Gestor de Configuração e seus ficheiros de base de dados), utilize RAID 10 para o melhor desempenho.  

|Utilização de dados|Espaço mínimo em disco|25 000 clientes|50 000 clientes|100 000 clientes|150 000 clientes|700.000 clientes (site da administração central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema operativo|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|  
|Aplicação de Gestor de Configuração e ficheiros de registo|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Ficheiro .mdf da base de dados do site|75 GB para cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Ficheiro .ldf da base de dados do site|25 GB para cada 25 000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Ficheiros da base de dados temporária (.mdf e .ldf)|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|  
|Conteúdo (partilhas de ponto de distribuição)|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|  

<sup>1</sup> A orientação espacial do disco não inclui o espaço necessário para conteúdos que se encontram na biblioteca de conteúdos no servidor do site ou pontos de distribuição. Para obter informações sobre o planeamento da biblioteca de conteúdos, veja [A biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).  

Além das orientações anteriores, considere as seguintes diretrizes quando planear os requisitos de espaço em disco:  

- Cada cliente necessita de cerca de 5 MB de espaço.  

- Quando planeia o tamanho da base de dados Temp para um site primário, planeie um tamanho combinado que seja de 25% a 30% da base de dados do site .ficheiro mdf. O tamanho real pode ser significativamente menor ou maior - depende do desempenho do servidor do site e do volume de dados de entrada durante períodos de tempo curtos e longos.  

  > [!NOTE]  
  >  Quando tiver 50.000 ou mais clientes num site, planeie utilizar quatro ou mais ficheiros de base de dados Temp .mdf.  

- O tamanho da base de dados Temp para um site de administração central é tipicamente muito menor do que para um site primário.  

- A base de dados do site secundário tem as seguintes limitações de tamanho:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a>Clientes  
Esta secção fornece configurações de hardware recomendadas para computadores que gere utilizando o software cliente do Gestor de Configuração.  

### <a name="client-for-windows-computers"></a>Cliente para computadores Windows  
Seguem-se os requisitos mínimos para computadores baseados no Windows que gere utilizando o 'Gestor de Configuração', incluindo sistemas operativos incorporados:  

- **Processador e memória:** Consulte os requisitos do processador e da RAM para o sistema operativo do computador.  

- **Espaço em disco:** espaço de 500 MB disponível em disco, com 5 GB recomendado para a cache do cliente do Gestor de Configuração. Menos espaço em disco é necessário se utilizar configurações personalizadas para instalar o cliente do Gestor de Configuração:  

    - Utilize a propriedade SMSCACHESIZE do Client.msi para definir um ficheiro de cache que seja menor do que o predefinido de 5120 MB. O tamanho mínimo é de 1 MB. Por exemplo, `CCMSetup.exe SMSCachesize=2` cria uma cache de 2 MB de tamanho.  

    Para obter mais informações sobre estas definições de instalação do cliente, consulte as propriedades de [instalação do cliente.](../../../core/clients/deploy/about-client-installation-properties.md)  

    > [!TIP]  
    > Instalar o cliente com um espaço em disco mínimo é útil para os dispositivos Windows Embedded que, geralmente, têm um espaço em disco menor do que os computadores Windows padrão.  

Seguem-se requisitos mínimos de hardware adicionais para funcionalidade opcional no 'Gestor de Configuração'.  

- **Implantação do sistema operativo:** 384 MB de RAM  

- **Centro de Software:** processador de 500 MHz  

- **Controlo Remoto:** Pentium 4 Hiper-Roscado 3 GHz (núcleo único) ou CPU comparável, com pelo menos 1 GB de RAM para uma experiência ideal  

### <a name="client-for-linux-and-unix"></a>Cliente para Linux e UNIX  
Seguem-se os requisitos mínimos para os servidores Linux e UNIX que gere com o Gestor de Configuração.  

|Requisito|Detalhes|  
|-----------------|-------------|  
|Processador e memória|Consulte os requisitos do processador e da RAM para o sistema operativo do computador.|  
|Espaço em disco|Espaço de disco disponível de 500 MB, com 5 GB recomendado para a cache do cliente do Gestor de Configuração.|  
|Conectividade de rede|Os computadores clientes do Gestor de Configuração devem ter conectividade de rede com os sistemas de site do Gestor de Configuração para permitir a gestão.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Consola de Gestor de Configuração  
Os requisitos na tabela seguinte aplicam-se a cada computador que executa a consola 'Gestor de Configuração'.  

**Configuração mínima de hardware:**  

- Intel i3 ou CPU comparável  

- 2 GB de RAM  

- 2 GB de espaço em disco  

|Definição PPP|Resolução mínima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

**Suporte para o PowerShell:**  

Quando instalar suporte para powerShell num computador que executa a consola Do Gestor de Configuração, pode executar cmdlets PowerShell nesse computador para gerir o Gestor de Configuração.

- PowerShell 3.0 ou mais tarde é suportado

Além do PowerShell, a versão 3.0 ou posterior do Windows Management Framework (WMF) é suportada.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Implementações de laboratórios  
Utilize as seguintes recomendações mínimas de hardware para implementações laboratoriais e de teste do Diretor de Configuração. Estas recomendações aplicam-se a todos os tipos de site, até 100 clientes:  

|Função|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor do site e da base de dados|2 - 4|8 - 12|100|  
|Servidor do sistema de sites|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
