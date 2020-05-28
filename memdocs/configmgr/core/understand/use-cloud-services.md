---
title: Utilizar serviços cloud
titleSuffix: Configuration Manager
description: Provisão de recursos em nuvem para o Gestor de Configuração para complementar a sua infraestrutura no local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84cb878de3eea56dc68180a83fd4b6a32b2d1073
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906431"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Utilizar serviços em nuvem com o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta várias opções baseadas na nuvem. Estes podem complementar a sua infraestrutura no local, e podem ajudar a resolver problemas de negócio como:  

-   Como gerir o BYOD (utilizando o Intune para a gestão de dispositivos móveis).  

-   Como fornecer recursos de conteúdo a clientes ou recursos isolados na intranet, fora da sua firewall corporativa (utilizando pontos de distribuição baseados na nuvem).  

-   Como escalar a infraestrutura quando o hardware físico não está disponível, ou não está logicamente posicionado para suportar as suas necessidades (utilizando máquinas virtuais Do Microsoft Azure).  

Embora o fornecimento de recursos em nuvem não seja algo que deve fazer antes de implementar o Gestor de Configuração, pode ser benéfico compreender estas opções antes de progredir demasiado num plano de design de hierarquia. O uso de recursos em nuvem pode poupar-lhe dinheiro e tempo, enquanto resolve problemas de negócios que a infraestrutura no local não pode.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos baseados em nuvem que pode usar com O Gestor de Configuração  
 Uma vez que cada opção tem requisitos diferentes, investigue cada um mais detalhadamente para compreender os pré-requisitos exclusivos, limitações e possibilidade de custos adicionais com base na utilização.  

-   Para obter informações sobre pontos de distribuição baseados na nuvem, consulte [Instale pontos de distribuição baseados na nuvem](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).

-   Para mais informações sobre o Azure, veja [o que é Azure?](https://azure.microsoft.com/overview/what-is-azure/)

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuais Azure (para infraestruturas baseadas em nuvem)  
 O Gestor de Configuração suporta a utilização de computadores que funcionam em máquinas virtuais no Azure, tal como acontece quando são executados no local dentro da sua rede corporativa física. Pode utilizar máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Gestor de Configuração numa máquina virtual e usá-lo para gerir clientes instalados noutras máquinas virtuais.  

-   **Cenário 2:** Pode executar o Gestor de Configuração numa máquina virtual e usá-lo para gerir clientes que não estejam a funcionar no Azure.  

-   **Cenário 3:** Pode executar diferentes funções do sistema de configuração em máquinas virtuais, enquanto executa outras funções na sua rede corporativa física (com conectividade de rede adequada para comunicações).  

Os mesmos requisitos para redes, sistemas operativos e requisitos de hardware que se aplicam à instalação do Gestor de Configuração na sua rede corporativa física aplicam-se também à instalação de 'Gestor de Configuração' no Azure.  

É necessária uma subscrição Azure para utilizar máquinas virtuais Azure. Incorre em cargas com base no número de máquinas virtuais que utiliza, na sua configuração e na utilização de recursos baseados na nuvem.  

Adicionalmente, os sites e clientes do Gestor de Configuração que funcionam em máquinas virtuais Azure estão sujeitos aos mesmos requisitos de licença que as instalações no local.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Serviços Azure (para pontos de distribuição baseados na nuvem)  
 Você pode usar um serviço Azure para hospedar um ponto de distribuição de Gestor de Configuração, que é chamado um ponto de distribuição baseado na nuvem. Pode [utilizar um ponto de distribuição baseado na nuvem com o Gestor](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) de Configuração ao lado de pontos de distribuição no local e pontos de distribuição implantados em máquinas virtuais Azure.  

 Isto é diferente de utilizar uma máquina virtual do Azure, na qual implementa uma função de sistema de sites. Pontos de distribuição baseados na nuvem:  

-   Funcionar como um serviço em Azure, não numa máquina virtual.  

-   Escala automaticamente para atender a pedidos de conteúdo acrescidos dos clientes.  

-   Apoiar os clientes na Internet e na intranet.  

É necessária uma subscrição Azure para utilizar o Azure para acolher pontos de distribuição. Incorre em encargos com base na quantidade de dados que transfere de e para o serviço.  

### <a name="additional-configuration-manager-capabilities"></a>Capacidades adicionais do Configuration Manager  
 Algumas capacidades do Gestor de Configuração podem ligar-se a serviços baseados na nuvem, como:  

-   Serviços de atualização do servidor do Windows (WSUS).  

-   A nuvem de serviço do Gestor de Configuração, para descarregar atualizações para O Gestor de Configuração.  

Estas capacidades adicionais não requerem que tenha uma subscrição Azure. Não é preciso configurar ligações específicas, certificados ou serviços na nuvem. Em vez disso, são geridos automaticamente pelo Gestor de Configuração para si. Tudo o que precisa fazer é garantir que os sistemas e dispositivos do site aplicáveis podem aceder aos URLs baseados na Internet.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a>Segurança para serviços baseados na nuvem  
 O Gestor de Configuração utiliza certificados para fornecer e aceder ao seu conteúdo no Azure, e gerir os serviços que utiliza. O Gestor de Configuração encripta os dados que armazena no Azure, mas não introduz controlos adicionais de segurança ou dados para além daqueles que o Azure fornece.  

 Para mais informações, consulte os detalhes para os diferentes cenários de recursos baseados na nuvem. Consulte também uma [introdução à segurança azure.](https://docs.microsoft.com/azure/security/fundamentals/overview)
