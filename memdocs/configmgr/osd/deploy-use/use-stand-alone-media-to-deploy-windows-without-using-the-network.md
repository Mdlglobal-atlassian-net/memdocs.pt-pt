---
title: Utilize meios autónomos para implementar o Windows
titleSuffix: Configuration Manager
description: Utilize suportes autónomos no Gestor de Configuração para implementar o Windows onde a largura de banda é limitada como uma opção para atualizar, instalar ou atualizar computadores.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724224"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os meios autónomos no Gestor de Configuração contêm tudo o que é necessário para implementar um sistema operativo num computador. Isto inclui a imagem de arranque, a imagem do sistema operativo e a sequência de tarefas para instalar o sistema operativo, incluindo aplicações, controladores, etc. As implementações com suportes de dados autónomos permitem implementar sistemas operativos nas seguintes condições:  

-   Em ambientes onde não é prático copiar uma imagem de sistema operativo ou outros pacotes grandes através da rede.  

-   Em ambientes sem conectividade de rede ou uma conectividade de rede com largura de banda reduzida.  

Pode utilizar suportes de dados autónomos nos seguintes cenários de implementação do sistema operativo:  

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

  Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para se preparar e criar suportes de dados autónomos.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Ações de sequência de tarefas não suportadas ao utilizar suportes de dados autónomos  
 Se executou os passos num dos cenários de implementação de sistema operativo suportados, a sequência de tarefas para implementar, ou atualizar, o sistema operativo foi criada e todo o conteúdo associado foi distribuído para um ponto de distribuição. Quando utiliza suportes de dados autónomos, as seguintes ações não são suportadas na sequência de tarefas:  

-   O passo Aplicar Controladores Automaticamente na sequência de tarefas. A aplicação automática de controladores de dispositivo a partir do catálogo de controladores não é suportada, mas pode escolher o passo Aplicar Pacote de Controlador para disponibilizar um conjunto especificado de controladores à Configuração do Windows.  

-   Instalação de atualizações de software.  

-   Instalação de software antes de implementar o sistema operativo.  

-   Associação de utilizadores ao computador de destino para suportar a afinidade dispositivo/utilizador.  

-   O pacote dinâmico é instalado através da tarefa Instalar Pacotes.  

-   A aplicação dinâmica é instalada através da tarefa Instalar Aplicação.  

> [!NOTE]  
>  Se a sequência de tarefas para implementar um sistema operativo incluir o passo [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) e criar o suporte de dados autónomo num site de administração central, poderá ocorrer um erro. O site de administração central não possui as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a execução da sequência de tarefas. O erro seguinte pode ser apresentado no ficheiro CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  No caso de suportes de dados autónomos que incluem um passo **Instalar Pacote** , tem de criar o suporte de dados autónomo num site primário com o agente de distribuição de software ativado ou adicionar um passo [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) após o passo [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e antes do primeiro passo **Instalar Pacote** na sequência de tarefas. O passo **Executar Linha de Comandos** executa um comando WMIC para ativar o agente de distribuição de software antes da execução do primeiro passo Instalar Pacote. Pode utilizar o seguinte no passo da sequência de tarefas **Executar Linha de Comandos** :  
>   
>  **Linha de Comandos**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Quando utilizar suportes de dados autónomos para iniciar o processo de implementação do sistema operativo, tem de configurar a implementação para disponibilizar o sistema operativo nos suportes. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** das propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:  

-   **Clientes do Configuration Manager, suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE (oculto)**  

## <a name="create-the-stand-alone-media"></a>Criar o suporte de dados autónomo  
 Pode especificar se o suporte de dados autónomo é uma pen USB ou um conjunto CD/DVD. O computador que vai iniciar o suporte de dados tem de suportar a opção que escolher como unidade de arranque. Para mais informações, consulte [Criar meios de comunicação autónomos.](create-stand-alone-media.md)  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Instalar o sistema operativo a partir de suportes de dados autónomos  
 Insira o suporte de dados autónomo numa unidade de arranque no computador e ligue-o para instalar o sistema operativo.  
