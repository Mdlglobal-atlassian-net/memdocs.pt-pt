---
title: Sobre a atualização de versão, atualização e instalação
titleSuffix: Configuration Manager
description: Saiba a diferença entre os termos Instalar, Atualizar e Atualizar, ao gerir a infraestrutura do Gestor de Configuração.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722600"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Sobre a atualização de versão, atualização e instalação da infraestrutura de hierarquia e site

*Aplica-se a: Gestor de Configuração (ramo atual)*

Ao gerir os sites do Gestor de Configuração e a infraestrutura da hierarquia, os termos *de atualização,* *atualização*e *instalação* são usados para descrever três conceitos distintos.

## <a name="upgrade"></a>Atualizar

*Upgrade* ou *upgrade no local*, é usado na conversão do site ou hierarquia do Gestor de Configuração de 2012 para um que executa o ramo atual do Gestor de Configuração.

Quando atualiza o System Center 2012 Configuration Manager para o 'Configuração Manager' atual, continua a utilizar os mesmos servidores para hospedar os seus sites e servidores de sites, e mantém os dados e configurações existentes para O Gestor de Configuração.  Isto é diferente do [Migration,](../migration/migrate-data-between-hierarchies.md) que é uma forma de reter as suas configurações e dados sobre dispositivos geridos enquanto utiliza novos sites de sucursais do Gestor de Configuração instalados em novos hardware.

Para mais detalhes, consulte Upgrade para 'Gestor de [Configuração'.](../servers/deploy/install/upgrade-to-configuration-manager.md)



## <a name="update"></a>Atualizar
*A atualização* é utilizada para instalar atualizações na consola para O Gestor de Configuração e para atualizações fora da banda que são atualizações que não podem ser entregues a partir da consola Do Gestor de Configuração. As atualizações na consola podem modificar a versão do seu site da Secção Atual (ou site de pré-visualização técnica) para que execute uma versão mais elevada. Por exemplo, se o seu site for executado na versão 1806, pode instalar uma atualização para a versão 1810. As atualizações também podem instalar correções para um problema conhecido, sem modificar a versão do site.      

Normalmente, as atualizações adicionam correções de segurança, melhorias de qualidade e novas funcionalidades à sua implementação existente. Se utilizar o ramo de Pré-visualização Técnica, uma atualização pode instalar uma versão mais recente da Pré-visualização Técnica.
- Escolhe quando instalar a atualização na consola, a partir do site de topo da sua hierarquia.
- Pode instalar qualquer atualização que esteja disponível a partir da consola. Por exemplo, se o seu site executa a versão 1802 e os 1806 e 1810 são oferecidos, deve considerar a instalação da versão 1810 porque cada versão inclui as funcionalidades que foram disponibilizadas pela primeira vez em versões previamente lançadas.
- Depois de uma nova atualização concluir a instalação no seu site de topo, os sites primários infantis iniciam automaticamente o processo de atualização. No entanto, pode definir o [Service Windows](../servers/manage/service-windows.md) para controlar o tempo das atualizações.
- Os sites secundários não instalam automaticamente atualizações. Em vez disso, inicia manualmente a atualização a partir da consola 'Gestor de Configuração'.

Para mais informações, consulte [atualizações para Gestor](../servers/manage/updates.md)de Configuração e [Pré-visualização Técnica para Gestor](../get-started/technical-preview.md)de Configuração .



## <a name="install"></a>Instalar
*A instalação* é usada na criação de uma nova hierarquia do Gestor de Configuração a partir do zero, ou adicionando sites adicionais a uma hierarquia existente.  

Quando instala um novo site primário ou site de administração central, a localização do setup.exe e os seus ficheiros de origem relacionados que utiliza dependem do cenário de instalação.

Para mais informações, consulte [Prepare-se para instalar locais](../servers/deploy/install/prepare-to-install-sites.md).
