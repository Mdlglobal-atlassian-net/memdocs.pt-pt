---
title: Capacidades na Pré-visualização Técnica 1704
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721410"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1704 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1704. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configure aplicativos Android com políticas de configuração de aplicações
Pode utilizar políticas de configuração de aplicações no 'Gestor de Configuração' para distribuir definições que podem ser necessárias quando um utilizador executa uma aplicação no Android for Work devices. As políticas de configuração de aplicações Android estão disponíveis apenas em dispositivos que executam o Android para o Trabalho e aplicam-se a aplicações aprovadas a partir da play for Work store.

### <a name="try-it-out"></a>Experimente                 

Na consola de Configuração Manager, escolha políticas de configuração de aplicações de**gestão** > de**aplicações** de **biblioteca** > de software e escolha criar a política de configuração de **aplicações.** Na página **geral** do assistente, pode agora selecionar um tipo de política de **configuração**. Especifique a plataforma visada pela política de configuração da aplicação: política de **configuração para aplicações Android for Work**. Em seguida, pode **especificar nomes e pares** de valor ou navegar para um ficheiro **JSON da lista de propriedades**. A nova política de configuração de aplicações é mostrada no espaço de trabalho da Biblioteca de **Software,** no nó de Políticas de Configuração de **Aplicações.** Para associar uma política de configuração de aplicações com a implementação de uma aplicação Android for Work, implemente a aplicação como normalmente faria utilizando o procedimento no tópico de [aplicações de Implement.](../../apps/deploy-use/deploy-applications.md)

## <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de Botas Seguras
O inventário de hardware agora recolhe informações sobre se o Secure Boot está ativado nos clientes. Esta informação é armazenada na classe **SMS_Firmware** (introduzida na versão 1702) e ativada no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../clients/manage/inventory/configure-hardware-inventory.md)de hardware .

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicione sequências de tarefas infantis a uma sequência de tarefas
Nesta versão, pode adicionar um novo passo de sequência de tarefas que executa outra sequência de tarefas, que cria uma relação pai/filho entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode reutilizar.  

Considere o seguinte quando adicionar uma sequência de tarefas para crianças a uma sequência de tarefas:

- As sequências de tarefas dos pais e das crianças são efetivamente combinadas numa única política que o cliente executa.
- Não é suportado para adicionar uma sequência de tarefas para crianças que é um pai de outra sequência de tarefas.
- O ambiente é global. Por exemplo, se uma variável for definida pela sequência de tarefas dos pais e depois alterada pela sequência de tarefas da criança, a variável permanece alterada para avançar. Da mesma forma, se a sequência de tarefas da criança criar uma nova variável, a variável está disponível para os passos restantes na sequência de tarefas dos pais.
- As mensagens de estado são enviadas normalmente para uma única operação de sequência de tarefas.
- As sequências de tarefas escrevem entradas para o ficheiro smsts.log, com novas entradas de registo que deixam claro quando uma sequência de tarefas infantil começa.
- Na Pré-visualização técnica para o Gestor de Configuração, versão 1704, se a tarefa infantil se qerizar qualquer pacote e executar a sequência de tarefas dos pais a partir do Software Center, o cliente não encontrará o conteúdo do pacote quando a sequência de tarefas da criança for executada. Neste cenário, deve executar a sequência de tarefas a partir de meios de comunicação (boot media, PXE, etc.).  

    Se a sequência de tarefas para crianças utilizar passos como Linha de **Comando executar** (sem qualquer referência de pacote), **Formato,** **BitLocker**, etc., então a sequência de tarefas será executada com sucesso a partir do Centro de Software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas para crianças a uma sequência de tarefas
1. No editor de sequência de tarefas, clique em **Adicionar**, selecione **General**, e clique na sequência de **tarefas executar**.
2. Clique em **Navegar** para selecionar a sequência de tarefas infantis.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Recarregar imagens de boot com a versão atual do Windows PE
Quando executa Pontos de Distribuição de **Atualização** numa imagem de arranque selecionada, pode agora optar por recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. A página **geral** do assistente fornece informações sobre a versão ADK do Windows instalada no servidor do site, a versão ADK do Windows a partir da qual o Windows PE foi utilizado na imagem de arranque e a versão do cliente do Gestor de Configuração. Pode utilizar esta informação para o ajudar a decidir se recarrega a imagem do arranque. Além disso, foi adicionada uma nova coluna (**Versão cliente)** quando vê imagens de arranque no nó **boot Images** para saber qual a versão do cliente do Gestor de Configuração que cada imagem de arranque utiliza.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Para recarregar uma imagem de boot com a versão atual do Windows PE

1. Na consola do Gestor de Configuração, vá a**Imagens**de Arranque de > **Sistemas Operativos** > da Biblioteca de **Software.**
2. Selecione uma imagem de arranque e clique em Pontos de **Distribuição de Atualização**.
3. Na página **Geral** do assistente, selecione recarregar a imagem de **arranque utilizando a versão atual do Windows PE a partir do Windows ADK instalado**.

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Fizemos as seguintes melhorias na implementação do sistema operativo, que foram o resultado do feedback de voz do utilizador.

- [Nova coluna **de versão OS** para imagens do sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): Adicionámos uma nova coluna chamada VERSÃO **OS** para exibir a versão do sistema operativo para a imagem quando visualizainformações nos nós de atualização do **sistema operativo.** **Operating System Upgrade Packages** Apenas a versão do primeiro índice no . A WIM é exibida. Vá ao separador **Details** para a imagem rever as versões do sistema operativo para outros índices.

- [Registo mais eficiente em Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): A partir desta versão, já não estamos a escrever entradas para o ficheiro smsts.log para CCM_CIVersionInfo.PolicyID. Antes desta versão, poderia haver muitas entradas com esta informação, o que dificultou a descoberta de informações mais relevantes no ficheiro de registo.
