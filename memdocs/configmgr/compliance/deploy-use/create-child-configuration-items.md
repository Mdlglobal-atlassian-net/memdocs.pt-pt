---
title: Criar itens de configuração subordinados
titleSuffix: Configuration Manager
description: Crie itens de configuração para crianças no Gestor de Configuração.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d194d9e80c037a13dde3d694793b695dfa5902e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712870"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Como criar itens de configuração para crianças no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Itens de configuração para crianças no Gestor de Configuração são cópias de itens de configuração que mantêm uma relação com o item de configuração original, na forma como herdam a configuração original a partir do item de configuração dos pais.  

Quando visualiza as propriedades de um item de configuração infantil na consola do Gestor de Configuração, não pode editar os objetos e configurações herdados com os seus critérios de validação. No entanto, pode adicionar e, em seguida, editar os critérios de validação adicionais para o item de configuração subordinado e também pode adicionar novos objetos e definições ao item de configuração subordinado.
Um exemplo para criar e editar um item de configuração infantil é aperfeiçoar o item de configuração original para satisfazer os seus requisitos de negócio.  

> [!NOTE]  
>  Só pode criar itens de configuração subordinados a partir de itens de configuração do tipo **Windows Desktops and Servers (personalizado)**.  

## <a name="to-create-a-child-configuration-item"></a>Para criar um item de configuração subordinado  

1.  Na consola do Gestor de Configuração, clique em Itens de Configuração de**Configuração**de > **Definições**de Conformidade de **Ativos e Conformidade.** >   

3.  Na lista **Itens de Configuração** , selecione o item de configuração para o qual pretende criar um item de configuração subordinado e, em seguida, no separador **Início** , no grupo **Item de Configuração** , clique em **Criar Item de Configuração Subordinado**.  

4.  Na página **Geral** página do **Assistente de Criação de Item de Configuração Subordinado**, pode escolher uma revisão específica do item de configuração principal para utilizar para criar o item subordinado. Os outros passos deste assistente são idênticos aos passos que utiliza para criar um item de configuração padrão. Para mais informações, consulte [como criar itens de configuração personalizados para computadores de ambiente](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)de trabalho e servidores do Windows .  

5.  Conclua o assistente. O novo item de configuração subordinado é apresentado na lista **Itens de Configuração** .  
