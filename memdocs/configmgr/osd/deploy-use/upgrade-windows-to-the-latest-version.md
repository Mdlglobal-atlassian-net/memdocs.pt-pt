---
title: Atualizar para o Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Gestor de Configuração para atualizar um SISTEMA do Windows 7 ou mais tarde para o Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8bfb45ba835851c33d6017f7f0a884bd2c1e9421
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429330"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Atualize o Windows para a versão mais recente com O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece os passos no Gestor de Configuração para atualizar o SISTEMA num computador. Pode escolher de entre vários métodos de implementação diferentes, como um suporte de dados autónomo ou o Centro de Software. O cenário de atualização no local tem as seguintes funcionalidades:  

- Atualiza o SO para windows 10, ou Windows Server 2016 e mais tarde

- Mantém as aplicações, configurações e dados do utilizador no computador

- Não tem dependências externas, como o Windows ADK

- É mais rápido e mais resistente do que as tradicionais implantações de SO

> [!Note]  
> A sequência de tarefas de upgrade do Windows 10 no local suporta a implementação de clientes baseados na Internet geridos através do portal de [gestão](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)da nuvem . Esta capacidade permite que os utilizadores remotos atualizem mais facilmente para o Windows 10 sem necessidade de se ligarem à intranet. Para mais informações, consulte [a atualização do Windows 10 no local via CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Versões suportadas

### <a name="upgrade-version"></a>Versão de upgrade

Apenas crie pacotes de upgrade de OS para atualizar para as seguintes versões de SO:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Versão original

Os dispositivos devem executar uma das seguintes versões de OS para direcionar uma sequência de tarefas de atualização do OS:

#### <a name="windows-client"></a>Cliente Windows

- Windows 7
- Windows 8.1
- Uma versão anterior do Windows 10. Por exemplo, pode atualizar o Windows 10, versão 1809 para windows 10, versão 1903.  

Para mais informações, consulte os caminhos de [upgrade do Windows 10.](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths)

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Uma versão anterior do Windows Server 2016
- Uma versão anterior do Windows Server 2019

Para obter mais informações sobre os caminhos de upgrade suportados pelo Windows Server, consulte o [Windows Server 2016 suportado por caminhos](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) de upgrade e [o Windows Server Upgrade Center](https://aka.ms/upgradecenter).


## <a name="plan"></a><a name="BKMK_Plan"></a>Plano  

### <a name="task-sequence-requirements-and-limitations"></a>Requisitos e limitações de sequência de tarefas

Reveja os seguintes requisitos e limitações para a sequência de tarefas para atualizar um Sistema operativo para se certificar de que satisfaz as suas necessidades:  

- Adicione apenas passos de sequência de tarefas relacionados com a tarefa principal de atualizar o Sistema Operativo. Estes passos incluem principalmente a instalação de pacotes, aplicações ou atualizações. Utilize também passos que executem linhas de comando, PowerShell ou definir variáveis dinâmicas.  

- Reveja os controladores e aplicações que são instalados em computadores. Antes de implementar a sequência de tarefas de atualização, certifique-se de que os controladores são compatíveis com o Windows 10.  

As seguintes tarefas não são compatíveis com a atualização no local. Exigem que utilize as tradicionais implementações de SO:  

- Alterar a adesão ao domínio do computador ou atualizar o grupo de Administradores locais.  

- Implementação de uma alteração fundamental no computador, tais como:

  - Alterando divisórias de disco
  - Mudar a arquitetura do sistema de x86 para x64
  - Implementação da UEFI. (Para obter mais informações sobre uma possível opção, consulte [Converter de BIOS para UEFI durante uma atualização no local](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - Modificação da linguagem base do OS  

- Tem requisitos personalizados, incluindo a utilização de uma imagem de base personalizada, utilizando encriptação de discos de terceiros, ou requeira operações offline winPE.  

### <a name="infrastructure-requirements"></a>Requisitos de infraestrutura  

O único pré-requisito para o cenário de atualização é ter um ponto de distribuição disponível. Distribua o pacote de atualização do OS e quaisquer outros pacotes que inclua na sequência de tarefas. Para mais informações, consulte [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a>Configurar  

### <a name="prepare-the-os-upgrade-package"></a>Prepare o pacote de upgrade do OS  

O pacote de atualização do Windows 10 contém os ficheiros de origem necessários para atualizar o SISTEMA no computador de destino. O pacote de upgrade deve ser a mesma edição, arquitetura e linguagem que os clientes que você atualiza. Para mais informações, consulte [gerir pacotes](../get-started/manage-operating-system-upgrade-packages.md)de upgrade do OS .  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Criar uma sequência de tarefas para atualizar o SO  

Utilize os passos em Criar uma sequência de [tarefas para atualizar um SISTEMA](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do SISTEMA.  

> [!NOTE]  
> Para criar uma sequência de tarefas para atualizar um SISTEMA para o Windows 10, normalmente utiliza os passos em Criar uma sequência de [tarefas para atualizar um OS](create-a-task-sequence-to-upgrade-an-operating-system.md). A sequência de tarefas inclui o passo **de upgrade do OS,** bem como passos e grupos recomendados adicionais para lidar com o processo de atualização de ponta a ponta.
>
> Pode criar uma sequência de tarefas personalizada e adicionar o passo [de Upgrade OS.](../understand/task-sequence-steps.md#BKMK_UpgradeOS) Este passo é o único necessário para atualizar o S para o Windows 10. Se escolher este método, para completar a atualização, adicione também o passo [do Computador restart](../understand/task-sequence-steps.md#BKMK_RestartComputer) após o passo de upgrade do **SISTEMA.** Certifique-se de que utiliza a definição **do sistema operativo predefinido atualmente instalada** para reiniciar o computador no SISTEMA instalado e não no Windows PE.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a>Implantação  

Para implantar o Sistema operativo, utilize um dos seguintes métodos de implantação:  

- [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

- [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > Quando utilizar meios autónomos, deve incluir uma imagem de arranque na sequência de tarefas. Esta configuração disponibiliza a sequência de tarefas no Assistente de Mídia da Sequência de Tarefas.


## <a name="monitor"></a>Monitorizar  

Para monitorizar a implementação da sequência de tarefas para atualizar o SISTEMA, consulte [as implementações do Monitor OS](monitor-operating-system-deployments.md).  
