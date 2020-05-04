---
title: Planear e configurar as definições de conformidade
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos e tarefas de configuração para trabalhar com as definições de conformidade no 'Gestor de Configuração'.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712156"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>Planeie e configure as definições de conformidade no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de começar a trabalhar com as definições de conformidade do Gestor de Configuração, existem alguns pré-requisitos que precisa de saber e algumas tarefas de configuração que terá de executar.  

## <a name="prerequisites-for-compliance-settings"></a>Pré-requisitos para definições de compatibilidade  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Os clientes do Gestor de Configuração do Windows devem ser ativados e configurados para avaliação de conformidade.|Veja abaixo|  
|Se pretender executar relatórios, tem de configurar relatórios para o seu site.|[Introdução aos relatórios](../../core/servers/manage/introduction-to-reporting.md)|  
|Necessárias permissões de segurança.|A função de segurança **do Compliance Settings Manager** inclui as permissões necessárias para gerir as definições de conformidade, itens de configuração de dados do utilizador e perfis de perfis de perfis de ligação remota.<br /><br /> [Configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Ativar e configurar as definições de conformidade (apenas para Computadores windows)  

Este procedimento configura as predefinições de cliente para definições de compatibilidade e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar definições de compatibilidade. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte [como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Outros tipos de dispositivo não requerem nenhuma configuração específica para avaliar definições de compatibilidade.  

1.  Na consola 'Gestor de Configuração', clique em**Definições** > **predefinidas**do Cliente **de Administração** > .  
2.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
3.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  
4.  Configure as seguintes definições do cliente para as definições de compatibilidade:
    - **Ativar a avaliação** de conformidade dos clientes - set to **True** se quiser avaliar a conformidade com os dispositivos do cliente.
    - **Agendar avaliação** de conformidade - **Clique em Agendar** se pretender modificar o calendário de avaliação de conformidade predefinido nos dispositivos do cliente.
    - **Ativar os dados e perfis** do utilizador - Ative esta opção se pretender criar e implementar itens de configuração de dados e perfis para computadores Windows. Para mais detalhes, consulte Criar dados do utilizador e itens de [configuração](../deploy-use/create-remote-connection-profiles.md)de perfis .
5. Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente.  
