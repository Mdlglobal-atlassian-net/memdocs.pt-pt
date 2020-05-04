---
title: Preparar servidores windows
titleSuffix: Configuration Manager
description: Certifique-se de que um computador cumpre os pré-requisitos para ser usado como servidor de site ou servidor de sistema de site para O Gestor de Configuração.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8889c0ee306eaaf682563b2e8e72d5482054d1c7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710791"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Preparar Servidores do Windows para suportar o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de poder utilizar um computador Windows como servidor de sistema de configuração, o computador deve cumprir os pré-requisitos para a sua utilização pretendida como servidor de servidor de site ou servidor de sistema de site.  

- Estes pré-requisitos incluem frequentemente uma ou mais funcionalidades ou funções do Windows, que são ativadas através do Gestor de Servidores dos computadores.  

- Uma vez que o método para ativar as funcionalidades e funções do Windows difere entre as versões DE, consulte a documentação para a sua versão OS para obter informações detalhadas sobre como configurar o SISTEMA que utiliza.  

As informações deste artigo fornecem uma visão geral dos tipos de configurações do Windows que são necessárias para suportar os sistemas de site do Gestor de Configuração. Para obter detalhes de configuração para funções específicas do sistema do site, consulte os [pré-requisitos](../configs/site-and-site-system-prerequisites.md)do sistema do Site e do site.

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a>Funcionalidades e funções do Windows  
Quando configura risse as funcionalidades e funções do Windows num computador, poderá ser necessário reiniciar o computador para completar essa configuração. Portanto, é uma boa ideia identificar computadores que irão hospedar funções específicas do sistema do site antes de instalar um site de Configuração ou servidor de sistema de site.

### <a name="features"></a>Funcionalidades  
As seguintes funcionalidades do Windows são necessárias em determinados servidores do sistema do site e devem ser configuradas antes de instalar uma função do sistema de instalação nesse computador.  

- **.NET Framework**: Incluindo  

    - ASP.NET  
    - Ativação HTTP  
    - Ativação não HTTP  
    - Serviços da Fundação de Comunicação do Windows (WCF)  

    Diferentes funções do sistema de site requerem versões diferentes do .NET Framework.  

    Uma vez que o .NET Framework 4.0 e mais tarde não é compatível com o retrocesso para substituir versões 3.5 e anteriores, quando diferentes versões são listadas conforme necessário, planeie permitir cada versão no mesmo computador.  

- **Serviços de Transferência Inteligente de Fundo (BITS)**: Os pontos de gestão requerem BITS (e opções automaticamente selecionadas) para apoiar a comunicação com dispositivos geridos.  

- **BranchCache**: Os pontos de distribuição podem ser criados com a BranchCache para apoiar os clientes que utilizam a BranchCache.  

- **Deduplicação de dados**: Os pontos de distribuição podem ser criados e beneficiar da duplicação de dados.  

- **Compressão diferencial remota (RDC)**: Cada computador que acolhe um servidor de site ou um ponto de distribuição requer RDC. O RDC é utilizado para gerar assinaturas de pacote e efetuar comparações de assinaturas.  

### <a name="roles"></a>Funções  
As seguintes funções do Windows são necessárias para suportar funcionalidades específicas, como atualizações de software e implementações de OS, enquanto o IIS é exigido pelas funções mais comuns do sistema do site.  

- **Serviço de Inscrição** de Dispositivos de Rede (em serviços de certificadode diretório ativo): Esta função do Windows é um pré-requisito para utilizar perfis de certificado sinuosos no Gestor de Configuração.  

- **Servidor web (IIS)**: Incluindo:  
    - Funcionalidades HTTP comuns  
          - Redireccionamento de HTTP  
    - Desenvolvimento de Aplicações  
          - Extensibilidade .NET  
          - ASP.NET  
          - Extensões ISAPI  
          - Filtros ISAPI  
    - Ferramentas de Gestão  
          - Compatibilidade de Gestão do IIS 6  
          - Compatibilidade com Metabase do IIS 6  
          - Compatibilidade com a instrumentação de gestão do IIS 6 Windows (WMI)  
    - Segurança  
          - Filtragem de Pedidos  
          - Autenticação do Windows  

  As seguintes funções do sistema do site utilizam uma ou mais configurações do IIS listadas:  
  - Ponto de serviço Web do Catálogo de Aplicações  
  - Ponto de Web site do Catálogo de Aplicações  
  - Ponto de distribuição  
  - Ponto de inscrição  
  - Ponto proxy de registo  
  - Ponto de estado de contingência  
  - Ponto de gestão  
  - Ponto de atualização de software  
  - Ponto de Migração de Estado     

  A versão mínima do IIS que é necessária é a versão fornecida com o SISTEMA do servidor do site.  

  Além destas configurações IIS, poderá ser necessário configurar a filtragem de [pedidos IIS para pontos](#BKMK_IISFiltering)de distribuição .  

- **Serviços**de Implementação do Windows : Esta função é utilizada com a implementação de SO.  

- **Serviços**de Atualização do Servidor do Windows : Esta função é necessária para atualizações de software.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a>IIS solicita filtragem para pontos de distribuição  
Por predefinição, o IIS utiliza a filtragem de pedidos para bloquear várias extensões de nomes de ficheiros e localizações de pastas contra o acesso por comunicação HTTP ou HTTPS. Num ponto de distribuição, isto impede os clientes de descarregar pacotes que tenham bloqueado extensões ou localizações de pastas.  

Quando os ficheiros de origem do pacote tiverem extensões bloqueadas no IIS pela configuração de filtragem do pedido, tem de configurar a filtragem do pedido para as permitir. Isto é feito [editando a funcionalidade](https://technet.microsoft.com/library/hh831621.aspx) de filtragem de pedidos no IIS Manager nos seus computadores de ponto de distribuição.  

Além disso, as seguintes extensões de nome de ficheiro são utilizadas pelo Gestor de Configuração para pacotes e aplicações. Certifique-se de que as configurações de filtragem do seu pedido não bloqueiam estas extensões de ficheiros:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Por exemplo, os ficheiros de origem para uma implementação de software podem incluir uma pasta chamada **bin** ou ter um ficheiro que tenha a extensão do nome do ficheiro **.mdb.**  

- Por predefinição, o IIS solicita filtrar blocos de acesso a estes elementos **(o caixote** do lixo está bloqueado como um Segmento Oculto e **.mdb** é bloqueado como uma extensão de nome de ficheiro).  

- Quando utiliza a configuração padrão do IIS num ponto de distribuição, os clientes que utilizam O BITS não conseguem descarregar esta implementação de software a partir do ponto de distribuição e indicam que estão à espera de conteúdo.  

- Para permitir que os clientes descarreguem este conteúdo, em cada ponto de distribuição aplicável, edite a **Filtragem de Pedidos** no Gestor IIS para permitir o acesso às extensões de ficheiros e pastas que estão nos pacotes e aplicações que implementa.  

> [!IMPORTANT]  
> As edimas para o filtro de pedido podem aumentar a superfície de ataque do computador.  
> 
> - As edificações que faz estoirar ao nível do servidor aplicam-se a todos os websites do servidor.   
>     - As edimas que faz em sites individuais aplicam-se apenas a esse website.  
> 
> A melhor prática de segurança é executar o Gestor de Configuração num servidor web dedicado. Se tiver de executar outras aplicações no servidor web, utilize um website personalizado para 'Gestor de Configuração'. Para obter informações, consulte [websites para servidores do sistema](websites-for-site-system-servers.md)do site .  

## <a name="http-verbs"></a>Verbos HTTP
**Pontos de gestão:** Para garantir que os clientes podem comunicar com sucesso com um ponto de gestão, no servidor de ponto de gestão garantir que os seguintes verbos HTTP são permitidos:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Pontos de distribuição:** Os pontos de distribuição exigem que os seguintes verbos HTTP, conforme permitido:
- GET
- HEAD
- PROPFIND

Para mais informações, consulte a filtragem do [pedido de configuração no IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs). 
