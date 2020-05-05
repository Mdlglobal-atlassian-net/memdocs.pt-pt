---
title: Noções básicas de sites e hierarquias
titleSuffix: Configuration Manager
description: Obtenha informações básicas sobre sites e hierarquias do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722817"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Fundamentos de sites e hierarquias para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Uma implementação do Gestor de Configuração deve ser instalada num domínio de Diretório Ativo. A fundação desta implantação inclui um ou mais sites de Gestor de Configuração que formam uma hierarquia de sites. Desde um único site a uma hierarquia de vários sites, o tipo e a localização dos sites que instala proporcionam a capacidade de aumentar verticalmente a implementação quando necessário, bem como fornecer serviços principais a utilizadores e dispositivos geridos.

## <a name="hierarchies-of-sites"></a>Hierarquias de sites
Quando instala o Gestor de Configuração pela primeira vez, o primeiro site do Gestor de Configuração que instala determina o âmbito da sua hierarquia. O primeiro site do Gestor de Configuração é a fundação a partir da qual irá gerir dispositivos e utilizadores na sua empresa. Este primeiro site deve ser um site de administração central ou um local primário autónomo.  

 Um site de *administração central* é adequado para implantações em larga escala, fornece um ponto central de administração, e fornece a flexibilidade para apoiar dispositivos que são distribuídos por uma infraestrutura global de rede. Depois de instalar um site de administração central, terá de instalar um ou mais locais primários como locais infantis. Esta configuração é necessária porque um site de administração central não suporta diretamente a gestão dos dispositivos, que é a função de um site primário. Um site da administração central apoia vários locais primários para crianças. Os locais primários para crianças são utilizados para gerir diretamente os dispositivos e para controlar a largura de banda da rede quando os seus dispositivos geridos estão em diferentes locais geográficos.  

 Um *local primário autónomo* é adequado para implementações menores, e pode ser usado para gerir dispositivos sem ter que instalar sites adicionais. Embora um site primário autónomo possa limitar o tamanho da sua implantação, ele suporta um cenário para expandir a sua hierarquia mais tarde, instalando um novo site de administração central. Com este cenário de expansão do site, o seu site primário autónomo torna-se um site primário para crianças, e pode instalar sites adicionais de primárias para crianças abaixo do seu novo site de administração central. Em seguida, pode expandir a sua implementação inicial para o crescimento futuro da sua empresa.  

> [!TIP]  
>  Um local primário autónomo e um local primário para crianças são realmente o mesmo tipo de site: um local primário. A diferença no nome baseia-se na relação hierárquica que é criada quando utiliza também um site de administração central. Esta relação de hierarquia também pode limitar a instalação de determinadas funções do sistema do site que alargam a funcionalidade do Gestor de Configuração. Esta limitação de funções ocorre porque certas funções do sistema do site só podem ser instaladas no local de topo da hierarquia, um site de administração central ou um local primário autónomo.  

 Depois de instalar o primeiro site, pode instalar sites adicionais. Se o seu primeiro site foi um site de administração central, então pode instalar um ou mais sites primários para crianças. Depois de instalar um local primário (autónomo ou primário de crianças), pode então instalar um ou mais locais secundários.  

 Um *site secundário* só pode ser instalado como site subordinado abaixo de um site primário. Este tipo de sites aumentam o alcance de um site primário para gerir dispositivos em locais com ligação de rede lenta ao site primário. Apesar de um site secundário alargar o site principal, o site principal gere todos os clientes. O site secundário fornece suporte para dispositivos no local remoto. Fornece suporte comprimindo e gerindo a transferência de informação através da sua rede que envia (implementar) para os clientes, e que os clientes enviam de volta para o site.  

 Os diagramas seguintes mostram alguns exemplos de estruturas de sites.  

 ![Exemplos de hierarquia](media/Hierarchy_examples.png)  

 Para obter mais informações, consulte os seguintes tópicos:  

-   [Introdução ao Configuration Manager](../../core/understand/introduction.md)  

-   [Desenhe uma hierarquia de sites para Gestor de Configuração](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Instalar sites do Gestor de Configuração](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Servidores do sistema de sites e funções do sistema de sites  
 Cada site do Gestor de Configuração instala *funções* do sistema do site que suportam operações de gestão. As seguintes funções são instaladas por predefinição quando instala um site:

-   A função do servidor do site é atribuída ao computador onde instala o site.

-   A função do servidor de base de dados do site é atribuída ao Servidor SQL que acolhe a base de dados do site.

Outras funções do sistema do site são opcionais, e só são usadas quando pretende utilizar a funcionalidade que está ativa numa função do sistema do site. Qualquer computador que aloje uma função de sistema de sites é referido como um servidor de sistema de sites.  

 Para uma implementação menor do Gestor de Configuração, pode inicialmente executar todas as funções do sistema do seu site diretamente no computador do servidor do site. Depois, à medida que o seu ambiente gerido e as suas necessidades crescem, pode instalar servidores adicionais do sistema do site para hospedar funções adicionais do sistema do site para melhorar a eficiência do site na prestação de serviços a mais dispositivos.  

 Para obter informações sobre as diferentes funções do sistema do site, consulte [as funções](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) do sistema do Site no Plano para servidores do sistema do [site e funções](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)do sistema do site para O Gestor de Configuração .

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicação de informações de sites nos Serviços de Domínio do Active Directory  
 Para simplificar a gestão do Gestor de Configuração, pode estender o esquema de Diretório Ativo para suportar detalhes que são utilizados pelo Gestor de Configuração e, em seguida, ter sites a publicar as suas informações-chave para Serviços de Domínio de Diretório Ativo (AD DS). Em seguida, os computadores que pretende gerir podem recuperar de forma segura informações relacionadas com o site a partir da fonte fidedigna de DS AD. As informações que os clientes podem obter identificam sites disponíveis, servidores do sistema de sites e os serviços que esses servidores de sistema de sites fornecem.  

 *O alargamento do esquema* de Diretório Ativo é feito apenas uma vez para cada floresta, e pode ser feito antes ou depois de instalar o Gestor de Configuração.   Ao estender o esquema, deve criar um novo recipiente ative diretório chamado System Management em cada domínio. O recipiente contém um site do Gestor de Configuração que publicará dados para os clientes encontrarem. Para mais informações, consulte Prepare o [Diretório Ativo para a publicação](../../core/plan-design/network/extend-the-active-directory-schema.md)do site.  

 *A publicação de dados* do site melhora a segurança da hierarquia do seu Gestor de Configuração e reduz as despesas administrativas, mas não é necessária para a funcionalidade básica do Gestor de Configuração.  
