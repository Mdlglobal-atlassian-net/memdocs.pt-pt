---
title: 'Gerir o estado do utilizador '
titleSuffix: Configuration Manager
description: O Gestor de Configuração utiliza a Ferramenta de Migração do Estado do Utilizador para capturar e restaurar os dados do Estado do utilizador em cenários de implementação do sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70c15fb3a108b22ffacad69d6a67bef3b2d29952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724077"
---
# <a name="manage-user-state-in-configuration-manager"></a>Gerir o estado do utilizador no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar sequências de tarefas do Gestor de Configuração para capturar e restaurar os dados do estado do utilizador em cenários de implementação do sistema operativo onde pretende manter o estado de utilizador do sistema operativo atual. Por exemplo:  

- Implementações em que pretenda capturar o estado do utilizador de um computador para o restaurar noutro.  

- Implementações de atualizações em que pretenda capturar e restaurar o estado do utilizador no mesmo computador.  

O Gestor de Configuração utiliza a Ferramenta de Migração do Estado do Utilizador (USMT) 10.0 para gerir a migração de dados do Estado do utilizador de um computador de origem para um computador de destino após o fim da instalação do sistema operativo. Para obter mais informações sobre cenários comuns de migração para a USMT 10.0, consulte  [Cenários Comuns de Migração](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Utilize as seguintes secções para ajudá-lo a capturar e restaurar os dados dos utilizadores.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a>Armazenar dados do estado do utilizador

 Quando capturar o estado do utilizador, pode armazenar os dados de estado do utilizador no computador de destino ou num ponto de migração de estado. Para armazenar o estado do utilizador num ponto de migração do estado do utilizador, deve utilizar um servidor de sistema de configuração do site manager que acolhe a função do sistema de pontode migração do estado. Para armazenar o estado do utilizador no computador de destino, terá de configurar a sequência de tarefas para armazenar os dados localmente utilizando ligações.

> [!NOTE]
> As ligações utilizadas para armazenar localmente o estado do utilizador são referidas como ligações fixas. As ligações fixas constituem uma funcionalidade da USMT 10.0 que verifica a existência de ficheiros e definições de utilizador no computador, criando um diretório de ligações fixas para esses ficheiros. As ligações fixas são então utilizadas para restaurar os dados do utilizador após a implementação do novo sistema operativo.

> [!IMPORTANT]
> Não é possível utilizar em simultâneo um ponto de migração de estado e ligações fixas para armazenar os dados de estado do utilizador.

Quando as informações de estado de utilizador são capturadas, podem ser armazenadas de uma das seguintes formas:  

- Pode armazenar os dados de estado de utilizador remotamente através da configuração de um ponto de migração de estado. A sequência de tarefas **Captura** envia os dados para o ponto de migração de estado. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas **Restauro** obtém os dados e restaura o estado de utilizador no computador de destino.  

- Pode armazenar os dados de estado de utilizador localmente numa localização específica. Neste cenário, a sequência de tarefas **Captura** copia os dados de utilizador para uma localização específica no computador de destino. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas **Restauro** obtém os dados de utilizador a partir dessa localização.  

- Pode especificar ligações fixas que podem ser utilizadas para restaurar os dados de utilizador na localização original. Neste cenário, os dados de estado de utilizador permanecem na unidade quando o sistema operativo anterior é removido. Em seguida, depois de o novo sistema operativo ser implementado, a sequência de tarefas **Restauro** utiliza as ligações fixas para restaurar os dados de estado do utilizador para a localização original.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Armazenar dados de utilizador num ponto de migração de estado

 Para armazenar os dados de estado do utilizador num ponto de migração de estado, terá de efetuar o seguinte:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) para armazenar os dados de estado do utilizador.  

1. [Create a computer association](#BKMK_ComputerAssociation) entre o computador de origem e o computador de destino. Terá de criar esta associação antes de capturar o estado do utilizador no computador de origem.  

1. [Crie uma sequência de tarefas para capturar e restaurar o estado do utilizador](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, deve adicionar os seguintes passos de sequência de tarefas para capturar os dados dos utilizadores a partir de um computador, armazenar a data do utilizador num ponto de migração do Estado e restaurar os dados do utilizador num computador:  

    - [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) para solicitar acesso a um ponto de migração de estado ao capturar o estado de um computador ou ao restaurar o estado para um computador.  

    - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do utilizador no ponto de migração de estado.  

    - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar o estado do utilizador no computador de destino ao obter os dados a partir de um ponto de migração de estado do utilizador.  

    - [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) para informar o ponto de migração de estado de que a ação de captura ou de restauro está concluída.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a>Armazenar dados do utilizador localmente

 Para armazenar os dados de estado do utilizador localmente, terá de efetuar o seguinte:  

- [Crie uma sequência de tarefas para capturar e restaurar o estado do utilizador](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, deve adicionar os seguintes passos de sequência de tarefas para capturar os dados dos utilizadores a partir de um computador e restaurar os dados do utilizador num computador utilizando ligações duras;

  - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do utilizador para uma pasta local utilizando ligações fixas.  

  - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar o estado do utilizador no computador de destino ao obter os dados utilizando ligações fixas.  

    > [!NOTE]
    > Os dados de estado do utilizador a que as ligações fixas fazem referência permanecem no computador depois de a sequência de tarefas remover o sistema operativo anterior. Estes dados serão utilizados para restaurar o estado do utilizador aquando da implementação do novo sistema operativo.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a>Configure um ponto de migração estatal

O ponto de migração de estado armazena os dados de estado do utilizador que são capturados num computador e, em seguida, restaurados noutro. No entanto, quando captura definições de utilizador para a implementação de um sistema operativo no mesmo computador, como uma implementação em que atualiza o sistema operativo no computador de destino, pode armazenar os dados no mesmo computador através de ligações fixas ou num ponto de migração de estado. Para algumas implementações de computador, quando cria a loja estatal, o Gestor de Configuração cria automaticamente uma associação entre a loja do Estado e o computador de destino. Poderá utilizar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do utilizador:  

- Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

- Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

  Ao utilizar estes assistentes, será solicitado que forneça as seguintes informações sobre o ponto de migração de estado:  

- As pastas em que os dados de estado do utilizador serão armazenados.  

- O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

- O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

- A política de eliminação da função. Poderá especificar que os dados de estado do utilizador sejam eliminados imediatamente ou um número de dias especificado após serem restaurados num computador.  

- Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Se ativar esta opção, não será possível utilizar o ponto de migração de estado para armazenar os dados de estado do utilizador.  

  Para obter mais informações sobre o ponto de migração de estado e os passos para configurá-lo, consulte [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a>Criar uma associação informática

Crie uma associação de computadores para definir uma relação entre um computador de origem e um computador de destino quando instala um sistema operativo em novo hardware e pretende capturar e restaurar as definições de dados do utilizador. O computador de origem é um computador existente que o Gestor de Configuração gere. Ao implementar o novo sistema operativo no computador de destino, o computador de origem contém o estado de utilizador que é migrado para o computador de destino.  

> [!NOTE]  
> Não é suportado para criar uma associação informática entre computadores localizados num site do Gestor de Configuração com computadores localizados num site infantil. As Associações informáticas são específicas do site e não se replicam.  

### <a name="to-create-a-computer-association"></a>Para criar uma associação de computadores

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

1. Na área de trabalho **Ativos e Compatibilidade** , clique em **Migração de Estado de Utilizador**.  

1. No separador **Home Page** , no grupo **Criar** , clique em **Criar Associação de Computadores**.  

1. No separador **Associação de Computadores** da caixa de diálogo **Propriedades da Associação de Computadores** , especifique o computador de origem que possui o estado de utilizador a capturar e o computador de destino em que pretende restaurar os dados de estado do utilizador.  

1. No separador **Contas de Utilizador** , especifique as contas de utilizador a migrar para o computador de destino. Especifique uma das seguintes definições:  

    - **Capturar e restaurar todas as contas de utilizador**: esta definição captura e restaura todas as contas de utilizador. Utilize esta definição para criar várias associações ao mesmo computador de origem.  

    - **Capturar todas as contas de utilizador e restaurar contas especificadas**: esta definição captura todas as contas de utilizador no computador de origem e restaura apenas as contas que especificar no computador de destino. Além disso, poderá utilizar esta definição quando pretender criar várias associações ao mesmo computador de origem.  

    - **Capturar e restaurar as contas de utilizador especificadas**: esta definição captura e restaura apenas as contas que especificar. Se selecionar esta definição, não será possível criar várias associações ao mesmo computador de origem.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> Restaurar os dados de estado do utilizador quando a implementação do sistema operativo falha

Se a implementação do sistema operativo falhar, utilize a funcionalidade LoadState da USMT 10.0 para obter os dados de estado do utilizador que foram capturados durante o processo de implementação. Isto inclui dados armazenados num ponto de migração de estado ou dados que são guardados localmente no computador de destino. Para obter mais informações sobre esta funcionalidade USMT, consulte [LoadState Syntax (Sintaxe LoadState)](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
