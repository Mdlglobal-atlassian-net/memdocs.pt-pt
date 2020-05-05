---
title: Criar uma imagem de um OEM de fábrica ou um depósito local
titleSuffix: Configuration Manager
description: Utilize implementações de meios pré-encenados para reduzir o tráfego de rede enquanto implementa um sistema operativo para um computador que não está totalmente provisionado.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722999"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Crie uma imagem para um OEM em fábrica ou um depósito local com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As implementações de meios pré-encenados no 'Gestor de Configuração' permitem-lhe implementar um sistema operativo para um computador que não esteja totalmente provisionado. O suporte pré-encenado é um ficheiro De formato de imagem do Windows (WIM) que pode ser instalado num computador de metal nu pelo fabricante (OEM) ou num centro de encenação empresarial que não esteja ligado ao ambiente do Gestor de Configuração. Mais tarde, no ambiente do Gestor de Configuração, o computador começa por utilizar a imagem de arranque fornecida pelos meios de comunicação, uma verificação de hash é executada nos meios pré-encenados para se certificar de que é válida, e depois o computador liga-se ao ponto de gestão do site para sequências de tarefas disponíveis que completam o processo de descarregamento.


Este método de implementação pode reduzir o tráfego de rede porque a imagem de arranque e a imagem do sistema operativo já estão no computador de destino. Pode especificar aplicações, pacotes e pacotes de controladores para incluir no suporte de dados pré-configurado. Depois de o sistema operativo estar instalado no computador, a cache da sequência de tarefas local é verificada primeiro em relação às aplicações, pacotes ou pacotes de controladores e, se não for possível localizar o conteúdo ou este tiver sido revisto, o conteúdo é transferido a partir de um ponto de distribuição configurado no suporte de dados pré-configurado e, em seguida, instalado.  

 Pode utilizar meios pré-encenados nos seguintes cenários de implementação do sistema operativo:  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

  Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para se preparar e criar o suporte de dados pré-configurado.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Quando utilizar suportes de dados pré-configurados para iniciar o processo de implementação do sistema operativo, tem de configurar a implementação para disponibilizar o sistema operativo nos suportes. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** das propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:  

-   **Clientes do Configuration Manager, suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE (oculto)**  

## <a name="create-the-prestaged-media"></a>Criar o suporte de dados pré-configurado  
 Crie o ficheiro de suporte de dados pré-configurado para enviar ao OEM ou depósito local. Para mais informações, consulte [Criar meios pré-encenados com o Gestor](create-prestaged-media.md)de Configuração .  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Enviar o ficheiro de suporte de dados pré-configurado ao OEM ou depósito local  
 Envie o suporte de dados ao OEM ou depósito local para pré-configurar os computadores. O ficheiro de suporte de dados pré-configurado é aplicado a um disco rígido formatado no computador.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Iniciar o computador para instalar o sistema operativo  
 O ficheiro de suporte de dados pré-configurado é aplicado aos computadores. Quando o computador for iniciado pela primeira vez, é iniciado o processo de instalação do sistema operativo.  
