---
title: Capturar e restaurar o estado do utilizador
titleSuffix: Configuration Manager
description: Utilize as sequências de tarefas do Gestor de Configuração para capturar e restaurar os dados do estado do utilizador em cenários de implementação do SISTEMA.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 93a39ba21b9e7d6cacfe59f763756aeef3736d52
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723041"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar o estado do utilizador no Gestor de Configuração

 *Aplica-se a: Gestor de Configuração (ramo atual)*

 Utilize as sequências de tarefas do Gestor de Configuração para capturar e restaurar os dados do estado do utilizador em cenários de implementação do SISTEMA. Nestes cenários, pretende manter o estado de utilizador do sistema operativo atual. Consoante o tipo de sequência de tarefa que criar, os passos de captura e restauro podem ser adicionados automaticamente como parte da sequência de tarefas. Noutros cenários, poderá ser necessário adicionar os passos de captura e restauro manualmente à sequência de tarefas. Este artigo fornece os passos que deve adicionar a uma sequência de tarefas existente para capturar e restaurar os dados do estado do utilizador.  



## <a name="task-sequence-steps"></a>Passos de sequência de tarefas  

Para capturar e restaurar o estado do utilizador, adicione os seguintes passos na sequência de tarefas:  

- [Solicite a State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore): Se armazenar o estado de utilizador no ponto de migração do Estado, precisa deste passo.  

- [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState): Este passo captura os dados do estado do utilizador. Em seguida, armazena os dados sobre o ponto de migração do Estado ou o disco local usando hardlinks.  

- [Restaurar Estado do Utilizador](../understand/task-sequence-steps.md#BKMK_RestoreUserState): este passo restaura os dados de estado do utilizador no computador de destino. Pode recuperar os dados de um ponto de migração estatal ou se estiver ligado no disco local.  

- [Loja do Estado de lançamento](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): Se armazenar o estado de utilizador no ponto de migração do Estado, precisa deste passo. Este passo remove os dados do ponto de migração do Estado.  


 Utilize os seguintes procedimentos para adicionar os passos de sequência de tarefas necessários para capturar e restaurar o estado do utilizador. Para obter mais informações sobre a criação de uma sequência de tarefas, consulte Gerir sequências de [tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Capturar o estado de utilizador  

 Para adicionar passos de sequência de tarefas para capturar o estado do utilizador, utilize os seguintes passos:

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se estiver a utilizar um ponto de migração estatal para armazenar o estado do utilizador, adicione o passo **da Loja do Estado de Pedido** à sequência de tarefas. No **Editor**de Sequência de Tarefas, clique em **Adicionar**. Aponte para o **Estado do Utilizador**, e, em seguida, clique em Request State **Store**. Configure as propriedades e opções para este passo e, em seguida, clique em **Aplicar**. Para mais informações sobre as definições disponíveis, consulte [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Adicione o passo **Capturar Estado do Utilizador** à sequência de tarefas. No **Editor**de Sequência de Tarefas, clique em **Adicionar**. Aponte para o **Estado do Utilizador**, e, em seguida, clique em Capturar estado de **utilizador**. Configure as propriedades e opções para este passo e, em seguida, clique em **Aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Quando adicionar este passo à sua sequência de tarefas, também detetete a variável de sequência de tarefas **OSDStateStorePath** para especificar onde armazenar os dados do estado do utilizador. Se armazenar o estado do utilizador localmente, não especifique uma pasta de raiz, pois isso pode fazer com que a sequência de tarefas falhe. Ao armazenar os dados do utilizador localmente, utilize sempre uma pasta ou subpasta. Para obter mais informações sobre esta variável, consulte variáveis de sequência de [tarefas.](../understand/task-sequence-variables.md#OSDStateStorePath)  

4.  Se estiver a utilizar um ponto de migração estatal, adicione o passo da **Loja do Estado** de Lançamento à sequência de tarefas. No **Editor**de Sequência de Tarefas, clique em **Adicionar**. Aponte para o **Estado do Utilizador**, e, em seguida, clique em Lançamento da State **Store**. Configure as propriedades e opções para este passo e, em seguida, clique em **Aplicar**. Para mais informações sobre as definições disponíveis, consulte [a Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas que funciona antes do passo da **Loja do Estado** de Lançamento deve ser bem sucedida antes do início do passo da Loja do Estado de **Lançamento.**  


 Implemente esta sequência de tarefas para capturar o estado do utilizador num computador de destino. Para obter informações sobre como implementar sequências de tarefas, consulte [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Restaurar o estado de utilizador  

 Para adicionar passos de sequência de tarefas para restaurar o estado do utilizador, utilize os seguintes passos:

1. Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2. Adicione o passo **Restore User State** à sequência de tarefas. No **Editor**de Sequência de Tarefas, clique em **Adicionar**. Aponte para o **Estado do Utilizador**, e, em seguida, clique em Restaurar o Estado do **Utilizador**. Este passo estabelece uma ligação ao ponto de migração do Estado, se necessário. Configure as propriedades e opções para este passo e, em seguida, clique em **Aplicar**. Para obter mais informações sobre as definições disponíveis, consulte restaurar o [Estado do Utilizador](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  Quando utilizar o passo do Estado do [Utilizador de Captura](../understand/task-sequence-steps.md#BKMK_CaptureUserState) com a opção de capturar todos os perfis do utilizador com **opções padrão,** deve selecionar a definição de **perfis de utilizador de computador local** restaurar na etapa do Estado do **Utilizador restaurar.** Caso contrário, a sequência de tarefas falhará.  

   > [!Note]  
   > Se armazenar o estado de utilizador utilizando hardlinks locais e o restauro não for bem sucedido, pode eliminar manualmente os hardlinks que foram criados para armazenar os dados. A sequência de tarefas pode executar a ferramenta USMTUtils para automatizar esta ação com um passo de Linha de [Comando de Execução.](../understand/task-sequence-steps.md#BKMK_RunCommandLine) Se utilizar usMTUtils para eliminar o hardlink, adicione um passo [de Computador Restart](../understand/task-sequence-steps.md#BKMK_RestartComputer) depois de executar USMTUtils.  

3. Se estiver a utilizar um ponto de migração estatal para armazenar o estado do utilizador, adicione o passo da **Release State Store** à sequência de tarefas. No **Editor**de Sequência de Tarefas, clique em **Adicionar**. Aponte para o **Estado do Utilizador**, e, em seguida, clique em Lançamento da State **Store**. Configure as propriedades e opções para este passo e, em seguida, clique em **Aplicar**. Para mais informações sobre as definições disponíveis, consulte [a Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  A ação de sequência de tarefas que funciona antes do passo da **Loja do Estado** de Lançamento deve ser bem sucedida antes do início do passo da Loja do Estado de **Lançamento.**  


 Implemente esta sequência de tarefas para restaurar o estado do utilizador num computador de destino. Para mais informações sobre a implementação de sequências de tarefas, consulte [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Passos seguintes

[Monitorizar a implementação da sequência de tarefas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
