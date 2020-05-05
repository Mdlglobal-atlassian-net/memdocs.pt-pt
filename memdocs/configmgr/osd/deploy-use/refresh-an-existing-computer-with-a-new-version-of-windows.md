---
title: Atualizar o sistema operativo de um computador existente
titleSuffix: Configuration Manager
description: Pode utilizar vários métodos no 'Gestor de Configuração' para dividir e formatar um computador existente e instalar um novo SISTEMA no computador.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723783"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Atualizar um computador existente com uma nova versão do Windows

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o Gestor de Configuração para a partilha e forme um computador existente e, em seguida, instale um novo SISTEMA. Este processo é por vezes chamado *de reimaging* ou *wipe and load*. Para este cenário, escolha entre muitos métodos de implementação diferentes, como PXE, suportes de arranque ou Centro de Software. Também pode usar um ponto de migração estatal para armazenar configurações e, em seguida, restaurá-las para o novo SISTEMA.

Para escolher o cenário de implementação correto do SISTEMA, consulte [Cenários para implantar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a>Plano  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Plano e implementação de requisitos de infraestruturas

Existem vários requisitos de infraestrutura que devem estar em vigor antes de poder implementar um Sistema Operativo. Alguns destes requisitos incluem o Windows ADK, a Ferramenta de Migração do Estado do Utilizador (USMT) e os Serviços de Implementação do Windows (WDS). Para obter mais informações, consulte [os requisitos de infraestrutura para a implantação do OS](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Instale um ponto de migração do Estado

Se pretender capturar as definições de um computador existente e, em seguida, restaurar as definições para o novo SISTEMA, considere utilizar um ponto de migração estatal. Para mais informações, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a>Configurar  

### <a name="prepare-a-boot-image"></a>Preparar uma imagem de arranque

As imagens de arranque iniciam um computador num ambiente Windows PE. O Windows PE é um Sistema operativo mínimo com componentes e serviços limitados. A partir do Windows PE, o Gestor de Configuração pode então instalar um Sistema Operativo Windows completo no computador.

Para obter mais informações, veja os artigos seguintes:

- [Gerir imagens de arranque](../get-started/manage-boot-images.md)

- [Personalizar imagens de arranque](../get-started/customize-boot-images.md)

- [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Preparar uma imagem de OS

A imagem de OS contém os ficheiros necessários para instalar o SISTEMA no computador de destino.

Para obter mais informações, veja os artigos seguintes:

- [Gerir imagens do SO](../get-started/manage-operating-system-images.md)

- [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Utilize uma sequência de tarefas para automatizar a instalação do Sistema Operativo. Consoante o método de implementação que escolher, poderão existir outras considerações relativamente à sequência de tarefas.

Para obter mais informações, veja os artigos seguintes:

- [Criar uma sequência de tarefas para instalar um SO](create-a-task-sequence-to-install-an-operating-system.md)

- [Gerir o estado do utilizador](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a>Implantação

- Utilize um dos seguintes métodos de implantação para implantar o Sistema Operativo:  

  - [Utilizar o PXE para implementar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Utilizar multicast para implementar o Windows na rede](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Criar uma imagem de um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitorizar  

Para mais informações, consulte [as implementações do Monitor OS](monitor-operating-system-deployments.md).  

> [!Note]
> Ao reimagem de um dispositivo UEFI, o Windows Boot Manager cria uma nova entrada no carregador de arranque. Este comportamento é mais percetível quando reimagem repetidamente um dispositivo, como num ambiente de teste ou num laboratório de estudantes. Geralmente não afeta o desempenho ou o uso do dispositivo. Se a lista ficar demasiado grande, alguns dispositivos de hardware específicos podem encontrar problemas funcionais. Por exemplo, não iniciar uma unidade USB externa, ou não ser capaz de selecionar a entrada de arranque atual da lista. Utilize o comando **Windows bcdedit** para limpar as entradas de botas não utilizadas. Para mais informações, consulte [BCDEdit /deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
