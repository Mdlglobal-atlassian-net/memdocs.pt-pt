---
title: Painel de instrumentos de ciclo de vida do produto
titleSuffix: Configuration Manager
description: Consulte a Política de Ciclo de Vida da Microsoft com o painel de instrumentos de ciclo de vida do produto no Gestor de Configuração.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714242"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gerir a política do ciclo de vida da Microsoft com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A partir da versão 1806, pode utilizar o painel de instrumentos de ciclo de vida do Produto Configuração Manager para visualizar a Política de Ciclo de Vida da Microsoft. O dashboard mostra o estado da Política de Lifecycle da Microsoft para os produtos microsoft instalados em dispositivos geridos com O Gestor de Configuração. Também lhe fornece informações sobre produtos da Microsoft no seu ambiente, estado de suporte e datas finais de suporte. Utilize o painel de instrumentos para compreender a disponibilidade de suporte para cada produto. Esta informação ajuda-o a planear quando atualizar os produtos da Microsoft que utiliza antes de ser atingido o seu suporte atual.  

Para mais informações, consulte a Política de [Ciclo de Vida](https://support.microsoft.com/lifecycle)da Microsoft .

A partir da versão 1810, o dashboard inclui informações para system center 2012 Configuration Manager e posteriormente.<!--1358702-->  



## <a name="prerequisites"></a>Pré-requisitos 

 Para ver os dados no painel de instrumentos de vida do produto, são necessários os seguintes componentes:  

- O Internet Explorer 9 ou mais tarde deve ser instalado no computador que executa a consola Do Gestor de Configuração.  

- Uma função de ponto de ligação de serviço deve ser instalada e configurada. Para obter atualizações para os dados deste dashboard, o ponto de ligação de serviço deve estar on-line ou sincronizado regularmente se estiver offline. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../../../servers/deploy/configure/about-the-service-connection-point.md).

- É necessário um ponto de serviço de reporte para a funcionalidade de hiperligação no painel de instrumentos. O dashboard liga-se aos relatórios sQL Server Reporting Services (SSRS). Para mais informações, consulte [Introdução a relatórios.](../../../servers/manage/introduction-to-reporting.md)  

- O ponto de sincronização da inteligência do ativo deve ser configurado e sincronizado. O dashboard usa o catálogo de inteligência de ativos como metadados para títulos de produto. Os metadados são comparados com os dados de inventário na sua hierarquia. Para mais informações, consulte [a inteligência do ativo Configure no Gestor de Configuração](configuring-asset-intelligence.md).  
  - Se estiver a configurar o ponto de serviço de inteligência de ativos pela primeira vez, certifique-se de ativar as classes de inventário de hardware de inteligência de [ativos.](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) O painel de instrumentos de ciclo de vida depende das aulas de inventário de hardware de inteligência de ativos. O painel de instrumentos não apresentará dados até que os clientes tenham digitalizado e devolvido o inventário de hardware.  
  - Para visualizar informações sobre atualizações de segurança estendidas (ESU) neste dashboard, ative a classe de inventário de hardware **Software Licensing Product - Asset Intelligence (SoftwareLicensingProduct)**. Para mais informações, consulte [Enable asset intelligence hardware classes](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Utilize o painel de instrumentos de ciclo de vida do produto

Com base em dados de inventário que o site recolhe de dispositivos geridos, o dashboard exibe informações sobre todos os produtos atuais. No entanto, as informações apresentadas para sistemas operativos e SQL Server estão limitadas às seguintes versões:

- Windows Server 2008 e mais tarde
- Windows XP e mais tarde
- SQL Server 2008 e mais tarde

Para aceder ao painel de instrumentos de ciclo de vida na consola do Gestor de Configuração, vá ao espaço de trabalho **De Ativos e Compliance,** expanda a Inteligência de **Ativos**e selecione o nó de ciclo de vida do **produto.**

> [!NOTE]  
> Os dados no painel de instrumentos baseiam-se no site a que a consola do Gestor de Configuração se conecta. Se a consola se ligar ao seu site de topo, verá dados para toda a hierarquia. Quando ligadoa a um local primário infantil, apenas os dados desse site mostram.

### <a name="product-lifecycle-dashboard"></a>Painel de instrumentos de ciclo de vida do produto

![Screenshot do painel de vida do produto na consola](media/product-lifecycle-dashboard.png)

Altere a vista selecionando uma das seguintes opções da lista de **categorias do Produto:**  
- **Tudo**: Ver todos os produtos juntos  
- **Cliente windows**: Ver verversões do Cliente Windows OS  
- **Windows Server**: Ver versões DO SERVIDOR do Windows  
- **Base de Dados**: Ver versões do Servidor SQL  
- **Gestor de Configuração**: A partir da versão 1810, verver versões de Gestor de Configuração 
- **Microsoft Office**: A partir da versão 1902, veja informações para versões instaladas do Office 2003 através do Office 2016 <!--3556026-->

O dashboard tem os seguintes mosaicos:  

- **Top cinco produtos passados**em fim de vida : Este azulejo é uma visão consolidada de dados de produtos encontrados no seu ambiente para além do seu fim de vida. O gráfico mostra software instalado que expirou quando comparado com o ciclo de vida de suporte para sistemas operativos e produtos de servidorEs SQL.  

- **Os cinco principais produtos que se aproximam do fim de vida**: Este azulejo é uma visão consolidada dos produtos encontrados no seu ambiente que se aproximam do fim de vida nos próximos 18 meses. O gráfico mostra software instalado que está dentro de 18 meses de fim de vida quando comparado com o ciclo de vida de suporte para sistemas operativos e produtos de servidorEs SQL.  

- Dados do ciclo de **vida para produtos instalados**: Este azulejo dá-lhe uma ideia geral de quando um produto passa de suportado para o estado expirado. O gráfico fornece uma repartição do número de clientes onde o produto está instalado, o estado de disponibilidade de suporte e um link para saber mais sobre os próximos passos a tomar. As seguintes informações estão incluídas na tabela:     
    - Tempo de apoio restante
    - Número no ambiente 
    - Data final de suporte mainstream
    - Data final de suporte alargada
    - Passos seguintes  

> [!IMPORTANT]  
> As informações mostradas neste dashboard são fornecidas para a sua conveniência e apenas para uso interno dentro da sua empresa. Não deve confiar apenas nesta informação para confirmar o cumprimento. Certifique-se de verificar a exatidão das informações que lhe são fornecidas, juntamente com a disponibilidade de informações de suporte visitando a Política de Ciclo de Vida da [Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Relatórios

Estão também disponíveis relatórios adicionais. Na consola De Configuração Manager, vá ao espaço de trabalho **de Monitorização,** expanda **reporte,** e expanda **Relatórios**. Os seguintes novos relatórios são adicionados na categoria **Asset Intelligence:**  

- **Lifecycle 01A - Computadores com um produto de software específico**: Ver uma lista de computadores nos quais é detetado um produto especificado.  

- **Lifecycle 02A - Lista de máquinas com produtos expirados na organização**: Ver computadores que tenham expirado produtos neles. Pode filtrar este relatório pelo nome do produto.

- **Lifecycle 03A - Lista de produtos expirados encontrados na organização**: Veja detalhes sobre produtos no seu ambiente que tenham expirado datas de ciclo de vida.  

- **Lifecycle 04A - Visão geral**do ciclo de vida do produto : Veja uma lista de ciclos de vida do produto. Filtre a lista pelo nome do produto e dias até à expiração.  

- **Lifecycle 05A - Painel de instrumentos**de ciclo de vida do produto : A partir da versão 1810, este relatório inclui informações semelhantes às do painel de instrumentos na consola. Selecione uma categoria para ver a contagem de produtos no seu ambiente e os dias de apoio restantes.  

Para mais informações, consulte [a Lista de Relatórios](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
