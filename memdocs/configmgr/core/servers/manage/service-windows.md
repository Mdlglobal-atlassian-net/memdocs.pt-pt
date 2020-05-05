---
title: Janelas de serviço
titleSuffix: Configuration Manager
description: Utilize as janelas de serviço para controlar quando os sites do Gestor de Configuração instalarem atualizações.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719114"
---
#  <a name="service-windows-for-site-servers"></a>Janelas de manutenção para servidores do site

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode configurar janelas de serviço em sites de administração central e sites primários para controlar quando as atualizações na consola podem instalar..  Pode configurar várias janelas, com a janela permitida para instalar atualizações sendo determinada por uma combinação de todas as janelas de serviço para esse servidor do site.

Quando nenhuma janela de serviço estiver configurada:
- **No seu site de topo** (um site de administração central ou site primário autónomo) escolhe quando iniciar a instalação da atualização.
- Num local primário para crianças, a atualização **instala-se**automaticamente após a atualização concluir a instalação no site da administração central.
- **Num site secundário,** as atualizações nunca começam automaticamente. Em vez disso, tem de iniciar manualmente a instalação da atualização a partir da consola, depois de o local principal dos pais ter instalado a atualização.

Quando uma janela de serviço está configurada:
- **No seu site de topo,** não poderá iniciar a instalação de qualquer nova atualização a partir da consola 'Gestor de Configuração'. Mesmo com uma janela de serviço configurada, o site descarrega automaticamente as atualizações para que estejam prontas a instalar.  
- **Num site primário infantil,** as atualizações que instalaram num site da administração central serão transferidas para o site principal, mas não arrancam automaticamente. Não é possível iniciar manualmente a instalação de uma atualização durante um período que seja bloqueado através da utilização de uma janela de serviço. Numa altura em que as janelas de serviço já não bloqueiam a instalação da atualização, a atualização é instalada automaticamente.
- **Os sites secundários** não suportam janelas de serviço e não instalam automaticamente atualizações. Depois do site principal de um site secundário instalar uma atualização, pode iniciar a atualização do site secundário a partir da consola.

## <a name="to-configure-a-service-window"></a>Para configurar uma janela de serviço

1.  No Configurmanager, a consola abra**os Sites**de**Configuração** > do Site da **Administração,** > e, em seguida, selecione o servidor do site onde pretende configurar uma janela de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione o separador **Período de Administração** , onde pode configurar um ou mais períodos de administração para esse servidor do site.  
