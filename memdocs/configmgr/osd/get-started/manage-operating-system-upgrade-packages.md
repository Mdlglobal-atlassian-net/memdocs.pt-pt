---
title: Gerir pacotes de atualização do SO
titleSuffix: Configuration Manager
description: Saiba como gerir os pacotes de upgrade do OS em 'Configuração Manager'.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc50fc60601b63bca7b4a4b01ba3fb4a39fd8b91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724105"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gerir pacotes de upgrade do OS com OGestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Um pacote de atualização do OS no 'Gestor de Configuração' contém os ficheiros de origem de configuração do Windows para atualizar um SISTEMA existente num computador. Este artigo descreve como adicionar, distribuir e servir um pacote de upgrade de SO.

> [!NOTE]
> Os pacotes de upgrade do OS também podem ser usados para novas instalações do Windows. No entanto, depende que os condutores sejam compatíveis com este método. Ao executar novas instalações do Windows a partir de um pacote de upgrade de OS, os controladores são instalados enquanto ainda estão no Windows PE versus simplesmente serem injetados enquanto estão no Windows PE. Alguns condutores não são compatíveis com a instalação do Windows PE. Se os controladores não forem compatíveis com a instalação do Windows PE, utilize uma [imagem de OS](manage-operating-system-images.md), como **instalar.wim.**

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a>Adicione um pacote de upgrade de OS  

Antes de poder utilizar um pacote de upgrade de OS, adicione-o primeiro ao site do Gestor de Configuração.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de pacotes de atualização do **sistema operativo.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Adicionar pacote de **atualização**do sistema operativo . Esta ação inicia o Assistente de Atualização do Sistema Operativo Add.  

3. Na página Fonte de **Dados,** especifique as seguintes definições:

    - O **caminho** da rede para os ficheiros de origem de instalação do pacote de atualização sO. Por exemplo, `\\server\share\path`.  

        > [!NOTE]  
        >  Os ficheiros de origem de instalação contêm configuração.exe e outros ficheiros e pastas para instalar o SISTEMA.  

        > [!IMPORTANT]  
        >  Limite o acesso a estes ficheiros de origem de instalação para evitar adulterações indesejadas.  

    - Extrair um índice de **imagem específico do ficheiro install.wim do pacote de atualização selecionado** e, em seguida, selecione um índice de imagem da lista.<!--4931110--> A partir da versão 1910, esta opção importa automaticamente um único índice em vez de todos os índices de imagem no ficheiro. A utilização desta opção resulta num ficheiro de imagem mais pequeno e numa manutenção offline mais rápida. Também suporta o processo de otimização do [serviço de imagem,](#bkmk_resetbase)para um ficheiro de imagem menor após a aplicação de atualizações de software.  

        > [!IMPORTANT]  
        > O Gestor de Configuração substitui a instalação existente.wim no pacote de atualização do OS. Extrai o índice de imagem para um local temporário, e depois move-o para o diretório de origem original. Antes de importar um pacote de upgrade de OS e ativar esta opção, certifique-se de fazer backup dos ficheiros de origem originais.

    - Se quiser pré-cache conteúdo num cliente, especifique a **Arquitetura** e **A Linguagem** da imagem. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).  

4. Na página **Geral,** especifique as seguintes informações. Estas informações são úteis para fins de identificação quando você tem mais do que um pacote de upgrade de SO.  

    - **Nome**: Um nome único para o pacote de upgrade de OS.  

    - **Versão**: Um identificador de versão opcional. Esta propriedade não precisa ser a versão sodo do pacote de upgrade. É frequentemente a versão da sua organização para o pacote.  

    - **Comentário**: Uma breve descrição opcional.  

5. Conclua o assistente.  

Em seguida, distribua o pacote de upgrade do SO para pontos de distribuição.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a>Distribuir conteúdo para um ponto de distribuição  

Distribua pacotes de upgrade de OS para pontos de distribuição iguais aos de outros conteúdos. Antes de implementar a sequência de tarefas, distribua o pacote de atualização de SO para pelo menos um ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Passos seguintes

[Criar uma sequência de tarefas para atualizar um SO](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
