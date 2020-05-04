---
title: Políticas de Firewall do Windows para proteção de pontofinal
titleSuffix: Configuration Manager
description: Saiba como criar e implementar políticas de firewall para proteção de pontos finais no System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715495"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Criar e implementar políticas de firewall do Windows para proteção de pontos finais no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As políticas de firewall para a Proteção de Pontofinal no Gestor de Configuração permitem-lhe executar tarefas básicas de configuração e manutenção do Windows Firewall em computadores clientes na sua hierarquia. Pode utilizar as políticas de Firewall do Windows para efetuar as seguintes tarefas:  

-   Controlar se a Firewall do Windows está ativada ou desativada.  

-   Controlar se as ligações recebidas têm permissões para computadores cliente.  

-   Controlar se os utilizadores são avisados quando a Firewall do Windows bloqueia um programa novo.  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  No espaço de trabalho **de Ativos e Compliance,** expanda a **Proteção do Ponto Final**e, em seguida, clique em Políticas de Firewall do **Windows**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Política de Firewall do Windows**.  

4.  Na página **Geral** do **Assistente da Criação da Política de Firewall do Windows**, especifique um nome e uma descrição opcional para esta política de firewall e, em seguida, clique **Seguinte**.  

5.  Na página **Definições de Perfil** do assistente, configure as seguintes definições para cada perfil de rede:  

    > [!NOTE]  
    >  Para mais informações sobre perfis de rede, consulte a documentação do Windows.  

    -   **Ativar a Firewall do Windows**  

        > [!NOTE]  
        >  Se **Ativar a Firewall do Windows** não estiver ativado, as outras definições nesta página do assistente ficam indisponíveis.  

    -   **Bloquear todas as ligações recebidas, incluindo as que se encontram na lista de programas permitidos**  

    -   **Notificar o utilizador quando a Firewall do Windows bloquear um programa novo**  

6.  Na página **Resumo** do assistente, reveja as ações a executar e conclua o assistente.  

7.  Certifique-se de que a nova política de Firewall do Windows é apresentada na lista **Políticas de Firewall do Windows** .  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Para implementar uma política de Firewall do Windows  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  No espaço de trabalho **de Ativos e Compliance,** expanda a **Proteção do Ponto Final**e, em seguida, clique em Políticas de Firewall do **Windows**.  

3.  Na lista **Políticas de Firewall do Windows** , selecione a política de Firewall do Windows que pretende implementar.  

4.  No separador **Home Page**, no grupo **Implementação**, clique em **Implementar**.  

5.  Na caixa de diálogo **Implementar Política de Firewall do Windows** , especifique a coleção à qual pretende atribuir esta política de Firewall do Windows e especifique um agendamento de atribuição. A política de Firewall do Windows avalia a compatibilidade, utilizando este agendamento e as definições de Firewall do Windows nos clientes para reconfigurar, de modo a corresponder à política de Firewall do Windows.  

6.  Clique em **OK** para fechar a caixa de diálogo **Implementar Política de Firewall do Windows** e para implementar a política de Firewall do Windows.  

    > [!IMPORTANT]  
    >  Ao implementar uma política de Firewall do Windows numa coleção, esta política é aplicada a computadores numa ordem aleatória durante um período de 2 horas, para evitar sobrecarregar a rede.
