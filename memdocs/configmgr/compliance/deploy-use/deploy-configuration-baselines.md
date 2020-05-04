---
title: Implementar linhas de base da configuração
titleSuffix: Configuration Manager
description: Desloque as linhas de base de configuração para definir as implementações de base de configuração e para adicionar ou remover as linhas de base de configuração das implementações.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712338"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Como implementar linhas de base de configuração no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As linhas de base de configuração no Gestor de Configuração devem ser implementadas para uma ou mais coleções de utilizadores ou dispositivos antes que os dispositivos do cliente nessas coleções possam avaliar o seu cumprimento com a linha de base de configuração.  

Utilize a caixa de diálogo **Implementar Linhas de Base de Configuração** para definir implementações da linha de base de configuração, que inclui adicionar ou remover linhas de base de configuração de implementações, além de especificar o agendamento de avaliação.  

## <a name="deploy-a-configuration-baseline"></a>Implementar uma linha de base de configuração  

1.  Na consola do Gestor de Configuração, clique em **Ativos e** > **Definições** > de Conformidade **.**  

3.  Na lista **Perfis de E-mail** , selecione o perfil de e-mail que pretende implementar e, em seguida, no separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

4.  Na caixa de diálogo **Implementar Linhas de Base de Configuração** , selecione as linhas de base de configuração que pretende implementar na lista **Linhas de base de configuração disponíveis** . Clique em **Adicionar** para adicioná-las à lista **Linhas de base de configuração selecionadas** .  

    > [!IMPORTANT]  
    >  Se alterar um item de configuração adicionado a uma linha de base de configuração implementada, o item de configuração revisto só é avaliado em termos de conformidade depois da próxima hora de avaliação agendada.  

5.  Especifique as seguintes informações adicionais:  

    -   **Remediar regras não conformes quando suportadas** – Remedia automaticamente quaisquer regras que não estejam em conformidade com a Instrumentação de Gestão do Windows (WMI), o registo, scripts e todas as definições para dispositivos móveis que estejam inscritos pelo Gestor de Configuração.  

    -   **Permitir remediação fora da janela de manutenção** – Se uma janela de manutenção tiver sido configurada para a coleção onde pretende implementar a linha de base de configuração, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Gerar um alerta** – Configura um alerta que é gerado se a conformidade da linha de base de configuração for inferior a uma percentagem especificada por uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

7.  **Coleção** - Clique em **Procurar** para selecionar a coleção na qual pretende implementar a linha de base de configuração.  

8.  **Especifique o calendário de avaliação de conformidade para esta linha de base de configuração** Especifica o calendário pelo qual a linha de base de configuração implementada é avaliada em computadores clientes. Pode ser um agendamento simples ou personalizado.  

    > [!NOTE]  
    >  Se a linha de base de configuração for implementada num computador, esta é avaliada em termos de conformidade duas horas após a hora de início agendada. Se for implementado num utilizador, é avaliada em termos de compatibilidade quando o utilizador inicia sessão.  

9. Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação. Para obter mais informações sobre como monitorizar a implementação, consulte [as definições](monitor-compliance-settings.md)de conformidade do Monitor .  
