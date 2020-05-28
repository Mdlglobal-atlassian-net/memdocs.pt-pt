---
title: Procedimentos recomendados para atualizações de software
titleSuffix: Configuration Manager
description: Utilize estas boas práticas para atualizações de software no Gestor de Configuração.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: eb9a675970abb581a793208c73506e1e94cc6f63
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906693"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Boas práticas para atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo inclui as melhores práticas para atualizações de software no Gestor de Configuração. A informação está classificada nas melhores práticas para a instalação inicial e para operações em curso.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a>Instalação de boas práticas  

Utilize as seguintes boas práticas quando instalar atualizações de software no 'Gestor de Configuração'.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a>Utilize uma base de dados WSUS partilhada para pontos de atualização de software  

Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. Se partilhar a mesma base de dados, atenua significativamente, mas não elimina completamente, o cliente e o impacto de desempenho da rede que poderá experimentar quando os clientes mudam para um novo ponto de atualização de software. Uma varredura delta ainda ocorre quando um cliente muda para um novo ponto de atualização de software que partilha uma base de dados com o antigo ponto de atualização de software, mas o scan é muito menor do que seria se o servidor WSUS tiver a sua própria base de dados. Para obter mais informações sobre a comutação de pontos de atualização de software, consulte a comutação de pontos de [atualização](plan-for-software-updates.md#BKMK_SUPSwitching)do Software .  

> [!IMPORTANT]  
>  Partilhe também as pastas de conteúdo wSUS locais quando utilizar uma base de dados WSUS partilhada para pontos de atualização de software.  

Para obter mais informações sobre a partilha da base de dados da WSUS, consulte as seguintes publicações de blog:  

- [Como implementar um SUSDB partilhado para pontos de atualização de software do Gestor de Configuração](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Considerações para vários casos wSUS que partilham uma base de dados](https://docs.microsoft.com/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb)de conteúdo ao utilizar o Gestor de Configuração .


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a>Quando o Gestor de Configuração e o WSUS utilizarem o mesmo Servidor SQL, configure um para usar uma instância nomeada e a outra para usar a instância predefinida  

Quando as bases de dados do Gestor de Configuração e da WSUS partilham a mesma instância do Servidor SQL, não é possível determinar facilmente o uso de recursos entre as duas aplicações. Utilize diferentes instâncias do Servidor SQL para O Gestor de Configuração e WSUS. Esta configuração facilita a resolução de problemas e o diagnóstico de problemas de utilização de recursos que podem ocorrer para cada aplicação.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a>Especifique a definição "Armazenar atualizações localmente"  

Quando instalar o WSUS, selecione a definição para **armazenar atualizações localmente**. Esta definição faz com que a WSUS descarregue os termos de licença que estão associados a atualizações de software. Descarrega os termos durante o processo de sincronização e armazena-os no disco rígido local para o servidor WSUS. Se não selecionar esta definição, os computadores clientes podem falhar as scans de conformidade para atualizações de software que tenham termos de licença. O componente **do WSUS Synchronization Manager** do ponto de atualização de software verifica que esta definição está ativada a cada 60 minutos, por padrão.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a>Boas Práticas Operacionais  

Utilize as seguintes melhores práticas quando utilizar atualizações de software:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a>Limite as atualizações de software para 1000 numa única implementação de atualização de software  

Limite o número de atualizações de software para 1000 em cada implementação de atualização de software. Quando criar uma regra de implementação automática, verifique se os critérios especificados não resultam em mais de 1000 atualizações de software. Se implementar manualmente atualizações de software, não selecione mais de 1000 atualizações.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a>Crie um novo grupo de atualização de software cada vez que um ADR corre para "Patch Tuesday" e para implementações gerais  

Há um limite de 1000 atualizações de software numa implementação. Quando criar uma regra de implementação automática (ADR), especifice se utiliza um grupo de atualização existente ou cria um novo grupo de atualização sempre que a regra for executado. Se especificar critérios num ADR que resultem em várias atualizações de software, e a regra for executado numa programação recorrente, crie um novo grupo de atualização de software sempre que a regra for executado. Este comportamento impede que a implementação ultrapasse o limite de 1000 atualizações de software por implementação.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a>Utilize um grupo de atualização de software existente para ADRs para atualizações de definição de proteção de pontofinal  

Quando utilizar um ADR para implementar atualizações de definição de proteção de pontos finais frequentemente, utilize sempre um grupo de atualização de software existente. Caso contrário, o ADR potencialmente cria centenas de grupos de atualização de software ao longo do tempo. Os editores de atualização de definição normalmente definem atualizações de definição para expirar quando são substituídos por quatro atualizações mais recentes. Portanto, o grupo de atualização de software criado pelo ADR nunca contém mais do que quatro atualizações de definição para a editora: uma ativa e três supersed.  



## <a name="see-also"></a>Veja também  
 [Plano para atualizações de software](plan-for-software-updates.md)
