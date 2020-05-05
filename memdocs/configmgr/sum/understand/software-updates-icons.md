---
title: Ícones utilizados para atualizações de software
titleSuffix: Configuration Manager
description: A consola 'Gestor de Configuração' contém ícones que indicam um estado para a atualização sincronizada ou grupo de atualização de software.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3843dd4ab4fe5a9aecaae8e6f207c3d037fc1950
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717714"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Ícones utilizados para atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As atualizações de software sincronizadas são apresentadas na consola Do Gestor de Configuração, e a primeira coluna para cada atualização de software contém um ícone que indica um estado específico. Os grupos de atualizações de software também são representados por um ícone que fornece informações sobre o estado das atualizações de software contidas no grupo. Esta secção fornece informações sobre os ícones de atualizações de software e o que cada ícone representa.  

## <a name="icons-for-software-updates"></a>Ícones de Atualizações de Software  
 As atualizações de software sincronizadas são representadas por um dos seguintes ícones.  

### <a name="normal-icon"></a>Ícone Normal  
 ![ícone](../media/Normal.jpg "Ícone normal") O ícone com a seta verde representa uma atualização normal de software.  

 **Description:**  

 As atualizações de software normais foram sincronizadas e estão disponíveis para implementação de software.  

 **Preocupações Operacionais:**  

 Não existem preocupações operacionais.  

### <a name="expired-icon"></a>Ícone de Expirada  
 ![ícone](../media/Expired.jpg "Ícone expirado") O ícone com o X preto representa uma atualização de software expirada. Também pode identificar atualizações de software expiradas visualizando a coluna **Expirada** para a atualização de software quando se apresentar na consola 'Gestor de Configuração'.  

 **Description:**  

 As atualizações de software expiradas eram anteriormente implementáveis nos computadores cliente mas, assim que uma atualização de software expira, já não podem ser criadas novas implementações para as atualizações de software. As atualizações de software expiradas são removidas de implementações ativas e deixarão de ser disponibilizadas aos clientes.  

 **Preocupações Operacionais:**  

 Não existem preocupações operacionais.

### <a name="superseded-icon"></a>Ícone de Substituída  
 ![ícone](../media/Superseded.jpg "Ícone substituído") O ícone com a estrela amarela representa uma atualização de software substituído. Também pode identificar atualizações de software supersed, visualizando a coluna **Supersed ed ida** para a atualização de software quando se apresentar na consola Do Gestor de Configuração.  

 **Description:**  

 As atualizações de software foram substituídas por versões mais recentes da atualização de software. Tipicamente, uma atualização de software que substitui outra atualização de software faz uma ou mais das seguintes coisas:  

- Melhora, atualiza ou adiciona a correção fornecida por uma ou mais atualizações de software publicadas anteriormente.  

- Melhora a eficiência do pacote de ficheiros de atualização de software, que o cliente instala se a atualização de software for aprovada para instalação. Por exemplo, a atualização de software substituído pode conter ficheiros que já não são relevantes para a correção ou para os sistemas operativos agora suportados pela nova atualização de software, pelo que esses ficheiros não estão incluídos no pacote de ficheiros da atualização de software de superseding.  

- Atualiza as versões mais recentes de um produto ou, por outras palavras, já não é aplicável a versões ou configurações antigas de um produto. As atualizações de software também podem substituir outras atualizações de software, se tiverem sido efetuadas modificações para expandir o suporte de idiomas. Por exemplo, uma versão mais recente de uma atualização de produto do Microsoft Office poderá remover o suporte para um sistema operativo antigo, mas poderá acrescentar suporte adicional para novos idiomas na versão de atualização de software inicial.  

  No separador Regras de Substituição das propriedades do Componente do Ponto de Atualização de Software, pode especificar como gerir atualizações de software substituídas. Para mais informações, consulte [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Preocupações Operacionais:**  

  Sempre que possível, implemente a atualização de software de substituição em computadores cliente, em vez da atualização de software substituída. Pode visualizar uma lista das atualizações de software que substituem a atualização de software no separador **Informações de Substituição** nas propriedades de atualização de software.  

### <a name="invalid-icon"></a>Ícone de Inválida  
 ![ícone](../media/Invalid.jpg "Ícone inválido") O ícone com o X vermelho representa uma atualização de software inválida.  

 **Description:**  

 As atualizações de software inválidas estão numa implementação ativa, mas por alguma razão o conteúdo (ficheiros de atualização de software) não está disponível. Seguem-se cenários em que pode ocorrer este estado:  

- A atualização de software é implementada com êxito, mas o ficheiro de atualização de software é removido do pacote de implementação e já não está disponível.  

- Cria-se uma implementação de atualização de software num site e o objeto de implementação é replicado com sucesso para um site infantil, mas o pacote de implementação não foi replicado com sucesso para o site da criança.  

  **Preocupações Operacionais:**  

  Quando o conteúdo estiver em falta numa atualização de software, os clientes não conseguem instalar a atualização de software até o conteúdo ficar disponível num ponto de distribuição. Pode redistribuir o conteúdo para pontos de distribuição, utilizando a ação **Redistribuir** . Quando o conteúdo está em falta numa atualização de software numa implementação criada num site principal, a atualização de software tem de ser replicada ou redistribuída para o site subordinado. Para obter mais informações sobre a redistribuição de conteúdos, consulte [Gerir o conteúdo que distribuiu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Ícone de Apenas de Metadados
 ![ícone](../media/MetadataOnly.png "Ícone só de metadados") O ícone com a seta azul representa uma atualização de software apenas de metadados.

 **Description:**  

 As atualizações de software apenas para metadados estão disponíveis na consola do Gestor de Configuração para reportagem. Não é possível implementar ou descarregar atualizações de software apenas com metadados porque um ficheiro de atualização de software não está associado aos metadados de atualizações de software.  

 **Preocupações Operacionais:**  

 As atualizações de software apenas com metadados estão disponíveis para efeitos de reporte e não se destinam à implementação de atualizações de software.  

## <a name="icons-for-software-update-groups"></a>Ícones de Grupos de Atualização de Software  
 Os grupos de atualização de software são representados por um dos seguintes ícones.  

### <a name="normal-icon"></a>Ícone Normal  
 ![ícone](../media/Normal.jpg "Ícone normal") O ícone com a seta verde representa um grupo de atualização de software que contém apenas atualizações normais de software.  

 **Preocupações Operacionais:**  

 Não existem preocupações operacionais.  

### <a name="expired-icon"></a>Ícone de Expirada  
 ![ícone](../media/Expired.jpg "Ícone expirado") O ícone com o X preto representa um grupo de atualização de software que contém uma ou mais atualizações de software expiradas.  

 **Preocupações Operacionais:**  

 Remova ou substitua as atualizações de software expiradas no grupo de atualizações de software sempre que possível.  

### <a name="superseded-icon"></a>Ícone de Substituída  
 ![ícone](../media/Superseded.jpg "Ícone substituído") O ícone com a estrela amarela representa um grupo de atualização de software que contém uma ou mais atualizações de software substituídos.  

 **Preocupações Operacionais:**  

 Substitua a atualização de software substituída no grupo de atualizações de software pela atualização de software de substituição, sempre que possível.  

### <a name="invalid-icon"></a>Ícone de Inválida  
 ![ícone](../media/Invalid.jpg "Ícone inválido") O ícone com o X vermelho representa um grupo de atualização de software que contém uma ou mais atualizações de software inválidas.  

 **Preocupações Operacionais:**  

 Quando o conteúdo estiver em falta numa atualização de software, os clientes não conseguem instalar a atualização de software até o conteúdo ficar disponível num ponto de distribuição. Pode redistribuir o conteúdo para pontos de distribuição, utilizando a ação **Redistribuir** . Quando faltam conteúdos para uma atualização de software numa implementação criada num site-mãe, a atualização do software precisa de ser replicada ou redistribuída para o site da criança. Para obter mais informações sobre a redistribuição de conteúdos, consulte [Gerir o conteúdo que distribuiu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Passos seguintes 

[Plano para atualizações de software](../plan-design/plan-for-software-updates.md)