---
title: Gerir o LTSC
titleSuffix: Configuration Manager
description: Diferenças de gestão para o LTSB do System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722705"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gerir o Ramo de Manutenção a Longo Prazo do Gestor de Configuração

*Aplica-se a: System Center Configuration Manager (Ramo de Manutenção a Longo Prazo)*

Quando utiliza o Ramo de Manutenção a Longo Prazo (LTSB) do System Center Configuration Manager, o seguinte pode ajudá-lo a compreender mudanças importantes que afetam a forma como gere a sua infraestrutura.

Como o LTSB é equivalente à versão 1606 do Current Branch (com algumas exceções como integração Intune e funcionalidades relacionadas com a nuvem), a maioria das tarefas que utiliza para planeamento, implementação, configuração e gestão do dia-a-dia são as mesmas.

Por exemplo, o LTSB suporta o mesmo número de sites, tipos de site, clientes e infraestruturas gerais que o Ramo Atual. Portanto, você usa a orientação encontrada no site e tópicos de planeamento e design de hierarquia para o Ramo Atual. Da mesma forma, para funcionalidades com o LTSB que são suportadas por ambas as agências, como atualizações de software ou implementação do sistema operativo, utilize as orientações encontradas nas secções da documentação do Ramo Atual com as ressalvas de não ter acesso às alterações de funcionalidade introduzidas após a versão 1606 da Atual Sucursal.

As seguintes secções fornecem informações sobre tarefas de gestão que não são semelhantes.

## <a name="updates-and-servicing"></a>Atualizações e manutenção
Apenas são disponibilizadas atualizações críticas de segurança como atualizações na consola no LTSB.  

As informações sobre as atualizações regulares para as seguintes versões do Current Branch são visíveis na consola, mas não são disponibilizadas ao LTSB. Não são descarregados e não podem ser instalados.

Para suportar atualizações na consola para correções de segurança críticas, um site LTSB requer a utilização do ponto de [ligação de serviço](../servers/deploy/configure/about-the-service-connection-point.md). Pode configurar este papel do sistema de site no modo offline ou online, como é feito para o Ramo Atual. O LTSB recolhe e submete os mesmos dados de telemetria e utilização que o Ramo Atual.

O LTSB suporta a utilização do Instalador hotfix e da ferramenta de registo de atualização, conforme documentado para o Ramo Atual.

Para obter informações gerais sobre atualizações e manutenção, consulte [Atualizações para Gestor de Configuração](../servers/manage/updates.md).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Alterações para a expansão do site e o CD. Última pasta
Quando executa o LTSB e está a expandir um site primário autónomo instalando um novo site de administração central, deve utilizar o Setup e os ficheiros de origem a partir dos meios de base da versão 1606. Para o Ramo Atual, executa a Configuração e utiliza ficheiros de origem a partir do CD. Última pasta.

Embora não execute a Configuração para a expansão do site a partir do CD. Última pasta, continua a usar o CD. Última pasta para recuperação do site, e para instalar um novo site primário infantil quando o seu primeiro site LTSB foi um site de administração central.

Para obter mais informações sobre a expansão do site, consulte [Expandir um site primário autónomo](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). Para mais informações sobre o CD. Última pasta, consulte [o CD. Última pasta.](../servers/manage/the-cd.latest-folder.md)


## <a name="recovery"></a>Recuperação
Quando recuperar um site, deve restaurar a base de dados do site ou do site no seu ramo original. Não é possível recuperar uma base de dados do site da Filial Atual para uma instalação LTSB, ou vice-versa.
