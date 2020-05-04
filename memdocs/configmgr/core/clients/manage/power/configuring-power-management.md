---
title: Configure a gestão de energia
titleSuffix: Configuration Manager
description: Configurar a gestão de energia no Gestor de Configuração.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715243"
---
# <a name="configure-power-management-in-configuration-manager"></a>Configure a gestão de energia no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo explica como configurar a gestão de energia no Gestor de Configuração.

## <a name="enable-and-configure-client-settings"></a>Ativar e configurar as definições do cliente

Este procedimento configura as *definições padrão* do cliente para a gestão de energia. Aplica-se a todos os computadores da sua hierarquia.

Se pretender aplicar estas definições apenas a alguns computadores, crie uma *definição personalizada*do cliente do dispositivo . Em seguida, atribua-o a uma coleção que contém os computadores para a gestão de energia. Para mais informações, consulte [Como configurar as definições do cliente](../../deploy/configure-client-settings.md).  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **da Administração,** selecione o nó de **Definições** do Cliente e selecione **Definições padrão do cliente**.

1. No separador **Casa** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

1. Selecione o grupo **Power Management.**  

1. Ative a definição do cliente para permitir a **gestão de energia dos dispositivos**.

1. Configure as definições adicionais do cliente que necessita. Para mais informações, consulte [sobre as definições do cliente - Power Management](../../deploy/about-client-settings.md#power-management).  

Os clientes configuram estas configurações quando descarregam a próxima política do cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Como gerir os clientes.](../manage-clients.md#BKMK_PolicyRetrieval)  

## <a name="exclude-computers"></a>Excluir computadores

Pode impedir que as coleções de computadores recebam definições de gestão de energia. Se um computador for membro de *qualquer* coleção que exclua das definições de gestão de energia, esse computador não aplica definições de gestão de energia. Este comportamento aplica-se mesmo que seja um membro de outra coleção que aplica configurações de gestão de energia.  

É melhor excluir computadores da gestão de energia pelas seguintes razões:  

- Tem um requisito comercial para os computadores estarem sempre ligados.  

- Tem uma coleção de computadores de controlo em que não pretende aplicar definições de gestão de energia.  

- Alguns dos computadores não podem aplicar definições de gestão de energia.  

- Pretende excluir computadores que executem o Windows Server da gestão de energia.  

> [!NOTE]  
> Se configurar a definição do cliente para **permitir que os utilizadores excluam o seu dispositivo da gestão de energia,** os utilizadores podem excluir os seus próprios computadores da gestão de energia utilizando o Software Center.  

Para descobrir quais os computadores excluídos da gestão de energia, execute o relatório **Computadores Excluídos**. Para obter mais informações sobre este relatório consulte [como monitorizar e planear a gestão de energia.](monitor-and-plan-for-power-management.md#BKMK_Excluded)  

> [!IMPORTANT]  
> Excluir um computador da gestão de energia faz com que todas as definições de energia sejam revertidas para os seus valores originais. Não é possível reverter as definições de energia individuais para os valores originais.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Como excluir uma coleção de computadores da gestão de energia  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de Recolhas de **Dispositivos.**  

1. Selecione a coleção que pretende excluir da gestão de energia. No separador **Casa** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

1. Mude para o separador **Power Management** e selecione Nunca aplique as definições de gestão de energia **para computadores nesta recolha**.  

## <a name="next-steps"></a>Passos seguintes

[Como criar e aplicar esquemas de energia](create-and-apply-power-plans.md)

[Como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md)
