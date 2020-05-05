---
title: Preparar implementações de computadores desconhecidos
titleSuffix: Configuration Manager
description: Aprenda a implementar sistemas operativos para computadores que não são geridos pelo Gestor de Configuração no ambiente do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724070"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Prepare-se para implementações de computador desconhecidas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize a informação neste tópico para implementar sistemas operativos em computadores desconhecidos no ambiente do Gestor de Configuração. Um computador desconhecido é um computador que não é gerido pelo Gestor de Configuração. Isto significa que não há registo destes computadores na base de dados do Gestor de Configuração. Os computadores desconhecidos incluem o seguinte:  

- Um computador onde o cliente do Gestor de Configuração não está instalado  

- Um computador que não é importado para O Gestor de Configuração  

- Um computador que não foi descoberto pelo Gestor de Configuração  

  Pode implementar sistemas operativos em computadores desconhecidos com os seguintes métodos de implementação:  

- [Utilizar o PXE para implementar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Utilizar suportes de dados de arranque para implementar um sistema operativo](../deploy-use/create-bootable-media.md)  

- [Utilizar suportes de dados pré-configurados para implementar um sistema operativo](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Fluxo de trabalho da implementação em computadores desconhecidos  
 É apresentado a seguir o fluxo de trabalho básico para implementar um sistema operativo num computador desconhecido:  

-   Selecione um objeto de computador desconhecido para utilizar na implementação. Pode implementar o sistema operativo num dos objetos de computador desconhecido na coleção **Todos os Computadores Desconhecidos** ou adicionar os objetos da coleção **Todos os Computadores Desconhecidos** a outra coleção. O Gestor de Configuração fornece dois objetos de computador desconhecidos na coleção **All Unknown Computers.** Um dos objetos destina-se a computadores x86 e outro a computadores x64.  

    > [!NOTE]  
    >  O objeto **Computador Desconhecido x86** destina-se a computadores que apenas são compatíveis com x86. O objeto **Computador Desconhecido x64** destina-se a computadores que apenas são compatíveis com x86 e x64. Por outras palavras, estes objetos descrevem a arquitetura do computador de destino. Não descrevem o sistema operativo que pretende implementar no computador de destino.  

-   Configure um suporte de dados ou um ponto de distribuição ativado para PXE ou crie um suporte de dados para suportar implementações em computadores desconhecidos.  

-   Implemente a sequência de tarefas para instalar o sistema operativo.  

## <a name="unknown-computer-installation-process"></a>Processo de Instalação de Computador Desconhecido  
 Quando um computador é iniciado a partir de PXE ou de meios de comunicação, o Gestor de Configuração verifica se existe um registo desse computador na base de dados do Gestor de Configuração. Se houver um registo, o Gestor de Configuração verifica então para ver se existem sequências de tarefas implantadas para o registo. Se não houver um registo, o Gestor de Configuração verifica se existem sequências de tarefas implementadas num objeto de computador desconhecido. Em qualquer dos casos, o Gestor de Configuração executa uma das seguintes ações:  

- Se houver uma sequência de tarefas disponível, o Gestor de Configuração solicita ao utilizador que execute a sequência de tarefas.  

- Se houver uma sequência de tarefas necessária, o Gestor de Configuração executa automaticamente a sequência de tarefas.  

- Se uma sequência de tarefas não for implementada para o registo, o Gestor de Configuração gera um erro de que não existe uma sequência de tarefas implementada para o computador de destino.  

  Quando um computador desconhecido é iniciado, o Gestor de Configuração reconhece o computador como um computador não provisionado em vez de um computador desconhecido. Isto significa que o computador pode agora receber as sequências de tarefas que foram implementadas no objeto de computador desconhecido. A sequência de tarefas implementada instala então uma imagem do sistema operativo que deve incluir o cliente do Gestor de Configuração.  

  Após a instalação do cliente do Gestor de Configuração, é criado um registo para o computador e o computador está listado na coleção de Gestor de Configuração apropriada. Se o computador não instalar a imagem do sistema operativo ou o cliente do Gestor de Configuração, é criado um registo "Desconhecido" para o computador e o computador aparece na coleção **All Systems.**  

> [!NOTE]  
>  Durante a instalação da imagem do sistema operativo, a sequência de tarefas pode obter as variáveis de coleção mas não as variáveis de computador deste computador.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Ativar o Suporte para Computadores Desconhecidos  
 Utilize o seguinte para ativar o suporte para computadores desconhecidos quando implementar um sistema operativo através de PXE, suportes de dados de arranque e suportes de dados pré-configurados.  

-   **PXE**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** no separador **PXE** para um ponto de distribuição ativado para PXE. Para obter mais informações, veja [Configurar pontos de distribuição para aceitar pedidos PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Suporte de dados de arranque**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** na página **Segurança** do Assistente de Criação de Suporte de Dados da Sequência de Tarefas. Para mais informações, consulte os pontos de [distribuição de Configuração para aceitar pedidos pXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) e [utilizar o PXE para implementar o Windows sobre a rede com o Gestor](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)de Configuração .  

-   **Suportes de dados de pré-configuração**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** na página **Segurança** do Assistente de Criação de Suporte de Dados da Sequência de Tarefas. Para mais informações, consulte [Criar meios pré-encenados com o Gestor](../deploy-use/create-prestaged-media.md)de Configuração .  
