---
title: Capacidades na Pré-visualização Técnica 1603
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076225"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1603 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1603. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Alternadamente, quando utiliza a Pré-visualização Técnica do System Center 5, esta versão instala-se como uma versão de base da Pré-visualização Técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 **Questões Conhecidas para esta Pré-visualização Técnica:**  

- Esta versão inclui atualizações para funcionalidades previamente lançadas, mas não introduz novas funcionalidades. Portanto, a página de Funcionalidades do Assistente de Atualização ficará vazia se tiver atualizado para 1602 e ativar todas as funcionalidades incluídas em 1602.  

- Após as atualizações do servidor do site para a Pré-visualização Técnica 1603, os clientes não podem utilizar quaisquer funcionalidades de controlo remoto até atualizarem também para a versão 1603.  

  **Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a>Melhorias no Centro de Software  

### <a name="new-tiled-view-for-apps"></a>Nova vista de azulejos para apps  
 Os utilizadores finais podem agora escolher entre uma lista de aplicações, ou uma visão em azulejo das aplicações no separador **aplicações** do Software Center.  

### <a name="select-multiple-updates-in-software-center"></a>Selecione várias atualizações no Centro de Software  
 No separador **Atualizações** do Software Center, pode agora selecionar várias atualizações ou selecionar **Atualizações Para** começar a instalar várias atualizações simultaneamente.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a>Melhorias no controlo remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limite o acesso partilhado à pasta numa sessão de controlo remoto  
 Agora pode ativar as novas ferramentas remotas de configuração do cliente Prompt user para a permissão de transferência de **ficheiros partilhadopara** limitar o acesso à área de transferência partilhada numa sessão de controlo remoto.  

 Quando ativado, o utilizador final que partilha uma sessão remota deve conceder permissões ao espectador dessa sessão antes que o espectador possa transferir ficheiros da sessão para a sua máquina local através da área partilhada.  

 Isto adiciona uma camada de proteção para o utilizador final como anteriormente, se o espectador recebesse o controlo total do computador do utilizador final, seria capaz de utilizar a pasta partilhada para transferir ficheiros da sessão para o seu computador local de uma forma totalmente transparente para o utilizador final.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>Personalize o tamanho do bloco RamDisk TFTP e o tamanho da janela em pontos de distribuição ativados por PXE  
 Na Pré-visualização Técnica de 1603, pode personalizar o tamanho do bloco RamDisk TFTP e o tamanho da janela para pontos de distribuição ativados por PXE. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos.   
Terá de testar as definições personalizadas no seu ambiente para determinar o que é mais eficiente.  

-   **Tamanho do bloco TFTP**: o tamanho do bloco consiste no tamanho dos pacotes de dados que são enviados pelo servidor para o cliente que está a transferir o ficheiro (conforme referido em RFC 2347). Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, tamanhos de bloco maiores resultam em pacotes fragmentados, não suportados pela maioria das implementações de cliente PXE.  

-   **Tamanho da janela de TFTP**: o TFTP precisa de um pacote de confirmação (ACK) para cada bloco de dados enviado. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. O sistema baseado em janelas do TFTP é uma funcionalidade dos Serviços de Implementação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. O aumento do tamanho desta janela reduz o número de atrasos no percurso de ida e volta entre o cliente e o servidor, e diminui o tempo global que é necessário para transferir uma imagem de arranque.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar as seguintes tarefas e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionava:  

-   Posso personalizar o tamanho da janela RamDisk TFTP no ponto de distribuição ativado pelo PXE.  

-   Posso personalizar o tamanho do bloco RamDisk TFTP no ponto de distribuição ativado pelo PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela de TFTP do disco de RAM  

- Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

   **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPWindowSize  

   **Tipo**: REG_DWORD  

   **Valor** &lt;: tamanho personalizado da janela\>  

  O valor predefinido é 1 (1 bloco de dados preenche a janela)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco de TFTP do disco de RAM  

- Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

   **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPBlockSize  

   **Tipo**: REG_DWORD  

   **Valor** &lt;: tamanho personalizado do bloco\>  

  O valor predefinido é 4096 (4k).  
