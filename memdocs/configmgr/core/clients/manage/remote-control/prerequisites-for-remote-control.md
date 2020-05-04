---
title: Pré-requisitos de controlo remoto
titleSuffix: Configuration Manager
description: Obtenha os pré-requisitos para o controlo remoto no 'Gestor de Configuração'.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715117"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Pré-requisitos para controlo remoto no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O controlo remoto no Gestor de Configuração tem dependências e dependências externas no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Controlador de placa de vídeo do computador|Certifique-se de que tem instalado o controlador de vídeo mais atualizado nos computadores cliente para assegurar um excelente desempenho do controlo remoto.|  

 Os dispositivos que executam o Windows Embedded, Windows Embedded para o Ponto de Serviço (POS) e o Windows Fundamentals para Computadores Legados não são compatíveis com o visualizador de controlo remoto, mas suportam o cliente de controlo remoto.  

 O controlo remoto do Gestor de Configuração não pode ser utilizado para administrar remotamente computadores clientes que executam o Systems Management Server 2003 ou o Gestor de Configuração 2007.  

> [!NOTE]  
>  Não são necessários serviços do Windows como dependência externa para o controlo remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos suportados para o visualizador de controlo remoto  
O visualizador de controlo remoto é suportado em todos os sistemas operativos que são suportados para a consola 'Gestor de Configuração'. Para obter informações, consulte [configurações suportadas para consolas de Configuração Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O controlo remoto deve estar ativado para os clientes|Por predefinição, o telecomando não está ativado quando instala o 'Gestor de Configuração'. Para obter informações sobre como ativar e configurar o telecomando, consulte o [controlo remoto de configuração](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para controlo remoto. Para mais informações, consulte [Introdução a relatórios.](../../../servers/manage/introduction-to-reporting.md)|  
|Permissões de segurança para gerir o controlo remoto|Para aceder aos recursos de recolha e iniciar uma sessão de controlo remoto a partir da consola do Gestor de Configuração: **Ler**, **Ler Recursos**e Autorização de **Controlo Remoto** para o objeto **de recolha.**<br /><br /> A função de segurança do Operador de **Ferramentas Remotas** inclui estas permissões que são necessárias para gerir o controlo remoto no Gestor de Configuração.<br /><br /> Para mais informações, consulte a [configuração da administração baseada em funções para o Gestor de Configuração](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Além disso, os espectadores autorizados devem ser autorizados a usar o controlo remoto adicionando estes utilizadores aos **espectadores permitidos de Controlo Remoto e Lista** de Assistência Remota nas definições do cliente das **Ferramentas Remotas.**
