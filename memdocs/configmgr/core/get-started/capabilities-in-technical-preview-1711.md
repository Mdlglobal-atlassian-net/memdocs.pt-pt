---
title: Antevisão Técnica 1711 / Microsoft Docs
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1711 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721291"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1711 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1711. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **Suporte para Windows 10, versão 1709 (também conhecida como Atualização**de Criadores de outono) .  A partir deste lançamento do Windows, os meios de comunicação windows incluem várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou imagem do sistema operativo, certifique-se de selecionar uma [edição que seja suportada para utilização pelo Select Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **A atualização para uma nova versão de pré-visualização falha quando tiver um servidor de site em modo passivo**. Quando executar uma versão de pré-visualização que tenha um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)tem de desinstalar o servidor do site do modo passivo antes de poder atualizar com sucesso o seu site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site do modo passivo depois de o site completar a atualização.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola, vá para **a Administração** > **Resumo** > servidores de**configuração** > do site**e funções**do sistema do site, e, em seguida, selecione o servidor de site de modo passivo.
  2. No painel de funções do **Sistema do Site,** clique à direita na função **do servidor do Site** e, em seguida, escolha remover **a função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Melhorias na sequência de tarefas de execução
<!-- 1261338 -->

Esta pré-visualização técnica melhorará o passo da sequência de tarefas de execução. As melhorias incluem os seguintes itens:

- Suporte para todos os cenários de implementação do sistema operativo a partir do Software Center, PXE e meios de comunicação.
- Melhorias nas ações de consola, tais como cópia, importação, exportação e aviso durante a eliminação do objeto.
- Suporte para o assistente de **conteúdo pré-estágio Criar.**
- Integração com verificação de implantação.
- O passo da sequência de tarefas de execução pode agora ser usado em vários níveis de sequências de tarefas, e não apenas numa única relação pai-filho. As relações a vários níveis aumentam a complexidade, por isso, use com cuidado. Estas relações ainda são verificadas para referências circulares.

### <a name="try-it-out"></a>Experimente!  

Tente completar as seguintes tarefas e, em seguida, envie-nos **feedback** do separador **Home** da Fita para nos informar como funcionava:

1. No editor de sequência de tarefas, clique em **Adicionar**, selecione **General**, e clique na sequência de **tarefas executar**.
2. Clique em **Navegar** para selecionar a sequência de tarefas infantis.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Permitir a interação do utilizador ao instalar uma aplicação <!-- 1356976 -->

Com esta pré-visualização, pode permitir que um utilizador final interaja com uma instalação de aplicação durante o funcionamento da sequência de tarefas. Por exemplo, executar um processo de configuração que indique o utilizador final para várias opções. Alguns instaladores de aplicações não podem ter solicitações do utilizador silenciadas, ou o processo de instalação pode exigir valores de configuração específicos apenas conhecidos do utilizador. Esta funcionalidade permite-lhe lidar com estes cenários de instalação.

### <a name="try-it-out"></a>Experimente!

Tente completar as seguintes tarefas e, em seguida, envie **feedback** do separador **Home** da fita para nos informar como funcionava:

1.  Criar ou editar uma aplicação. Para mais informações, consulte [Criar aplicações com 'Gestor de Configuração'.](../../apps/deploy-use/create-applications.md)

    a. Escolha o separador **User Experience** no **Instalador do Windows (ficheiro\*Msi) Propriedades**.

    b. **Selecione Instalar para o sistema** para instalar o **comportamento**.

    c. Selecione **Se um utilizador está ou não ligado** para iniciar **sessão no requisito**.

    d. Selecione **Normal** para a visibilidade do programa de **instalação**. Pode selecionar entre três opções: **Minimizado,** **Normal**ou **Maximizado**.

    e. Selecione os utilizadores permitir em interagir com a caixa de **instalação do programa.**

2.  Criar ou editar uma sequência de tarefas para instalar a aplicação utilizando o passo de instalação da **aplicação.** Para mais informações, consulte instalar a [Aplicação](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) nos passos da [sequência de tarefas](../../osd/understand/task-sequence-steps.md).

    a. Sequência de tarefas de imagem após o passo de Configuração Windows e Configuração Manager.

    b. Sequência de tarefas de atualização no local no grupo pós-processamento.

3.  Desloque a sequência de tarefas a um cliente.
4.  Instale a sequência de tarefas no Centro de Software.

Durante o progresso da sequência de tarefas, a interface de instalação da aplicação aparece no dispositivo de utilizador final do alvo. O progresso da sequência de tarefas pausa até que o utilizador final complete o fluxo de trabalho de instalação da aplicação.

### <a name="install-using-the-wizard"></a>Instale utilizando o assistente

Também pode utilizar esta funcionalidade ao implementar uma aplicação utilizando o assistente.

1. Criar ou editar uma aplicação.
2. Implemente a aplicação a um cliente.
3. Instale a aplicação no Centro de Software. A interface de instalação da aplicação deve aparecer. O utilizador final deve seguir o assistente de instalação da aplicação e a aplicação será instalada com sucesso.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
