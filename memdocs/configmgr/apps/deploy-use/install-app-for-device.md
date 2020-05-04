---
title: Instalar aplicações para um dispositivo
titleSuffix: Configuration Manager
description: Utilize o Gestor de Configuração para instalar imediatamente uma aplicação num dispositivo sem uma recolha.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710224"
---
# <a name="install-applications-for-a-device"></a>Instalar aplicações para um dispositivo

<!--4402180-->

A partir da versão 1906, a partir da consola 'Gestor de Configuração' pode instalar aplicações num dispositivo em tempo real. Esta funcionalidade pode ajudar a reduzir a necessidade de coleções separadas para cada aplicação.

## <a name="prerequisites"></a>Pré-requisitos

- Ativar a [funcionalidade opcional](../../core/servers/manage/install-in-console-updates.md#bkmk_options) Aprove os pedidos de **aplicação para utilizadores por dispositivo**.  

- [Implemente a aplicação](deploy-applications.md) como *Disponível* para uma recolha de dispositivos.  

    - Na página **definições** de implementação do assistente de implementação, selecione a seguinte opção: **Um administrador deve aprovar um pedido para esta aplicação no dispositivo**.  

        > [!Note]  
        > Com estas definições de implementação, nenhuma política é enviada ao cliente. A aplicação não é mostrada como disponível no Software Center, e um utilizador não pode instalar a aplicação com esta implementação. Depois de utilizar esta ação para instalar a aplicação, o utilizador pode executá-la e ver o seu estado de instalação no Software Center.

- A sua conta de utilizador necessita das seguintes permissões:

    - **Pedido**: Ler, Aprovar

    - **Recolha**: Ler, Ler Recurso, Modificar Recurso, Ver Arquivo Recolhido

    Por exemplo, o papel incorporado do Administrador de **Aplicação** tem estas permissões.

> [!TIP]
> Numa hierarquia, aguarde que as informações de aplicação e implementação se reproduzam no local principal a que o cliente-alvo é atribuído.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Processo

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Dispositivos.** Selecione o dispositivo alvo e, em seguida, selecione a ação de **aplicação Instalar** na fita.

1. Selecione uma ou mais aplicações da lista. A lista apenas mostra aplicações que já implementou com as definições pré-requisitos.

Esta ação desencadeia a instalação das aplicações pré-implantadas selecionadas no dispositivo.

Para ver o estado do pedido de aprovação, no espaço de trabalho da Biblioteca de **Software,** expandir a Gestão de **Aplicações,** e selecionar o nó de Pedidos de **Aplicação.**

Monitorize a instalação da aplicação da mesma forma habitual no nó de **Implantação** do espaço de trabalho **monitoramento.**


## <a name="see-also"></a>Consulte também

[Aprovar aplicações](app-approval.md)
