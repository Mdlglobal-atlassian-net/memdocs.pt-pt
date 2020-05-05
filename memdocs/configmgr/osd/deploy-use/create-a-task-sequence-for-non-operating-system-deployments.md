---
title: Criar uma sequência de tarefas para implementações não pertencentes ao SO
titleSuffix: Configuration Manager
description: Criar sequências de tarefas que não sejam para implementar um SISTEMA, como distribuir software ou automatizar tarefas
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 583a90452fe077057b93150e9cb635fe9269de5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724245"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Criar uma sequência de tarefas para implementações não pertencentes ao SO

*Aplica-se a: Gestor de Configuração (ramo atual)*

As sequências de tarefas no Gestor de Configuração são usadas para automatizar diferentes tipos de tarefas dentro do seu ambiente. Estas tarefas são principalmente concebidas e testadas para implementar sistemas operativos. O Gestor de Configuração tem muitas outras funcionalidades que devem ser a tecnologia primária que utiliza para os seguintes cenários:

- [Instalação de aplicações](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > A partir da versão 2002, instale aplicações complexas utilizando sequências de tarefas através do modelo de aplicação. Adicione um tipo de implementação a uma aplicação que é uma sequência de tarefas, quer para instalar ou desinstalar a aplicação. Para mais informações, consulte [Create Windows aplicações](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Instalação de atualizações de software](../../sum/understand/software-updates-introduction.md)

- [Configuração de definição](../../compliance/understand/ensure-device-compliance.md)

Considere também outras tecnologias de automação do Microsoft System Center, como [orchestrator](https://docs.microsoft.com/system-center/orchestrator/) e automação de [gestão](https://docs.microsoft.com/system-center/sma/)de serviços.  

O poder das sequências de tarefas reside na sua flexibilidade e na forma como as utiliza. Podem configurar as definições do cliente, distribuir software, atualizar controladores, editar estados de utilizador e fazer outras tarefas independentes da implementação do OS. Pode criar uma sequência de tarefas personalizada para adicionar qualquer número de tarefas. A utilização de sequências de tarefas personalizadas para implementação não-S é suportada no Gestor de Configuração. No entanto, se uma sequência de tarefas resultar em resultados indesejados ou inconsistentes, procure formas de simplificar a operação:

- Use passos mais simples
- Divida as ações em várias sequências de tarefas
- Tome uma abordagem faseada para criar e testar a sequência de tarefas

Os seguintes passos são suportados para utilização numa sequência de tarefas personalizadas de implementação não-S:  

- [Verificar Disponibilidade](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Ligar à pasta da rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Transferir Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Instalar Aplicação](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Instalar Pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Instalar Atualizações de Software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Reiniciar Computador](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Linha de Comando executar](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Executar Script do PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Executar sequência de tarefas](../understand/task-sequence-steps.md#child-task-sequence)  

- [Definir Variáveis Dinâmicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Definir Variável da Sequência de Tarefas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
