---
title: Categorizar automaticamente os dispositivos em coleções
titleSuffix: Configuration Manager
description: Categorize automaticamente os dispositivos em coleções.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714312"
---
# <a name="automatically-categorize-devices-into-collections"></a>Categorizar automaticamente os dispositivos em coleções

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode criar categorias de dispositivos, que podem ser usados para colocar automaticamente dispositivos nas coleções dos dispositivos quando estiver a utilizar o 'Configuração Manager' com o Microsoft Intune. Os utilizadores têm então de escolher uma categoria de dispositivo quando matriculam um dispositivo em Intune. Pode alterar uma categoria de dispositivo da consola 'Gestor de Configuração'.

> [!IMPORTANT]
>  Esta capacidade funciona com o lançamento de junho de **2016** do Microsoft Intune e mais tarde. Certifique-se de que foi atualizado para esta libertação antes de experimentar estes procedimentos.

## <a name="create-device-categories"></a>Criar categorias de dispositivos

1.  Ir para Recolhas de**Dispositivos**de**Visão Geral** >  **de Ativos e Conformidade.** > 
2.  No separador **Home,** no grupo De recolha de **dispositivos,** escolha **Categorias de Dispositivos de Gestão**.
3.  Criar, editar ou remover categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo

Quando associar uma coleção a uma categoria de dispositivo, todos os dispositivos desta categoria serão adicionados à recolha. Não é possível adicionar uma regra de categoria de dispositivo a uma coleção incorporada como **a All Systems**.

1.  No separador Regras de **Associação** da caixa de diálogo **Properties** para uma recolha de dispositivos, escolha regra de categoria**de dispositivo**de regra > de **adição**.
2.  Na caixa de diálogo **Select Device Categories,** selecione uma ou mais categorias de dispositivos que serão aplicadas a todos os dispositivos da recolha.

## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  Em**Dispositivos**de**Visão Geral** > de **Ativos e Conformidade,** > selecione um dispositivo da lista de **Dispositivos.**
2.  No separador **Home,** no grupo **Dispositivo,** escolha **a categoria de alteração**.
3.  Escolha uma categoria e escolha **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver a que categoria um dispositivo pertence

Em**Dispositivos**de**Visão Geral** > de **Ativos e Conformidade,** > na lista de **Dispositivos,** a categoria é apresentada na coluna **categoria de dispositivos.**

Se a coluna **da categoria de dispositivo** não for apresentada, clique na direção de uma das colunas da lista de **Dispositivos** (como **nome),** e selecione **a categoria de dispositivo**.

Se atribuir um dispositivo a uma categoria e, posteriormente, excluir a categoria, a **lista de relatórios de dispositivos matriculados por utilizador no Microsoft Intune** apresentará um GUID na coluna **categoria de dispositivo,** em vez de um nome de categoria.
