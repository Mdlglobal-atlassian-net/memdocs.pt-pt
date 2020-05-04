---
title: Simular implementações de aplicações
titleSuffix: Configuration Manager
description: Avalie o método de deteção, requisitos e dependências para um tipo de implementação sem instalar a aplicação.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710595"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Simular implementações de aplicações com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar implementações simuladas para testar uma implementação de aplicação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implantação. Reporta os resultados no nó de **implantação** do espaço de trabalho **de monitorização.** Utilize o procedimento neste tópico para simular uma implementação de aplicação no Gestor de Configuração.  

> [!NOTE]  
> Não é possível utilizar implementações simuladas em coleções de dispositivos móveis.  
>   
> Não é possível implementar uma aplicação com um objetivo de implementação de **Desinstalar** se estiver ativa uma implementação simulada da mesma aplicação.  

## <a name="configure-a-simulated-application-deployment"></a>Configure uma implementação simulada de aplicação

1.  Na consola 'Gestor de Configuração', selecione um dos seguintes:  
    -   Uma coleção de utilizadores.  
    -   Uma coleção de dispositivos.  
    -   Uma aplicação de Gestor de Configuração.  

2.  No separador **Home,** no grupo **de implantação,** escolha **Simulate Deployment**.  

3.  No Assistente de Implementação de Aplicações simulada, detete os seguintes detalhes para a sua implementação simulada:  

    -   **Aplicação**. Escolha **o Browse**e, em seguida, selecione a aplicação para a qual pretende criar uma implementação simulada.  

    -   **Coleção**. Escolha **o Browse**e, em seguida, selecione a coleção que pretende utilizar para a implementação simulada.  

    -   **Ação.** A partir da lista de lançamentos, selecione se pretende simular a instalação ou a desinstalação da aplicação selecionada.  

    -   **Implemente automaticamente com ou sem login**do utilizador . Se esta opção for verificada, os clientes avaliam a implementação simulada se os clientes estão ou não a iniciar sessão.  

4.  Clique em **Seguinte,** reveja as informações na página **Resumo** e, em seguida, termine o assistente para criar a implementação simulada da aplicação.  

5.  As aplicações simuladas aparecem no nó de **implantação** do espaço de trabalho de **monitorização,** com o objetivo de **Simular**. Para obter mais informações sobre como monitorizar as implementações de aplicações, consulte [as aplicações monitoradas a partir da consola Do Gestor de Configuração](../../apps/deploy-use/monitor-applications-from-the-console.md).  
