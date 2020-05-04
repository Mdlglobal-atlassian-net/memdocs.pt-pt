---
title: Dicas de resolução de problemas para implementações de aplicações
titleSuffix: Configuration Manager
description: Dicas para problemas de implementação de aplicações em 'Gestor de Configuração'
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710588"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Dicas de resolução de problemas para implementações de aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os problemas típicos com as implementações de aplicações enquadram-se numa das seguintes categorias:

- Falhas no download de aplicações

- Conformidade de implementação de aplicações presa a 0%

Se experimentar qualquer uma destas questões, este artigo fornece alguns passos que pode usar para resolver problemas. Para uma resolução mais aprofundada de problemas, consulte a referência técnica de [implementação de aplicações de resolução de problemas](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>Falhas de descarregamento

As falhas de descarregamento de aplicações incluem os seguintes problemas:

- O cliente está preso a descarregar uma aplicação

- O cliente não consegue descarregar o conteúdo da aplicação

- O cliente fica preso a 0% ao descarregar a aplicação

A primeira coisa a verificar quando experimenta falhas de descarregamento de aplicações é para limites e grupos de fronteira sem acordo ou mal configurados. Por exemplo, se o cliente estiver na intranet e não estiver configurado para a gestão de clientes apenas na Internet, a sua localização de rede deve estar num limite configurado. Deve também haver um grupo de limites atribuído a este limite para o cliente descarregar conteúdo. Para mais informações, consulte Definir os limites do [site e os grupos de fronteira.](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)

Se não conseguir configurar um limite para um cliente, ou se um grupo de fronteira específico não pode ser membro de outro grupo de fronteiras:

1. Na consola 'Gestor de Configuração', abra as propriedades do Tipo de **Implementação**.  

1. Mude para o separador **Conteúdo.**

1. Na secção para utilizar um ponto de distribuição de um grupo de fronteira sinuoso ou do grupo de fronteira do site predefinido, altere as **opções** de Implementação para **descarregar conteúdo a partir do ponto de distribuição e executar localmente**. (Por defeito, esta definição é **Não descarregue o conteúdo**.)

Se o cliente não conseguir descarregar o conteúdo da aplicação, certifique-se de que está distribuído para um ponto de distribuição. Para verificar esta configuração, utilize as funcionalidades na consola para monitorizar a distribuição de conteúdos nos pontos de distribuição. Para mais informações, consulte o [monitor de conteúdos que distribuiu](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Conformidade presa a 0%

Quando a conformidade de implementação da aplicação for de 0%, verifique o estado de implantação da aplicação no espaço de trabalho de **Monitorização** sob o nó de **Implantações.**

- **In Progress**: O cliente pode estar preso [a descarregar conteúdo](#download-failures)

- **Error**: Para obter mais informações sobre como resolver este problema, consulte a seguinte publicação do blog: [Dicas e Truques: Como Tomar medidas sobre ativos que reportam uma implementação falhada](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Desconhecido**: Este estado geralmente significa que o cliente não recebeu a apólice. Refresque manualmente a política do cliente para ver se o cliente a recebe. Para mais informações, consulte [Iniciar a recuperação de políticas para um cliente do Gestor de Configuração](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Se estas ações não resolverem o problema, verifique o estado do cliente. Pode haver um problema mais profundo subjacente com o cliente. Para mais informações, consulte [Como monitorizar os clientes](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Passos seguintes

- [Monitorizar aplicações](monitor-applications-from-the-console.md)
- [Implementar aplicações](deploy-applications.md)
- [Tarefas de gestão de candidaturas](management-tasks-applications.md)
- [Referência técnica de implementação de aplicações de resolução de problemas](../understand/app-deployment-technical-reference.md)
