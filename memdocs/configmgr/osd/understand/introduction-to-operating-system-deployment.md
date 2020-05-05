---
title: Introdução à implementação de sistemas operativos
titleSuffix: Configuration Manager
description: Compreenda os conceitos antes de implementar sistemas operativos no ambiente do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720388"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Introdução à implementação do sistema operativo no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar o Gestor de Configuração para implementar sistemas operativos de várias maneiras diferentes. Utilize as informações nesta secção para entender como implementar sistemas operativos e automatizar tarefas. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> Processo de implementação do sistema operativo  
 O Gestor de Configuração fornece vários métodos que pode utilizar para implementar um sistema operativo. Existem várias ações que deverá efetuar, independentemente do método de implementação que utilizar:  

-   Identificar os controladores de dispositivo do Windows necessários para executar a imagem de arranque ou a imagem do sistema operativo que tem de implementar.  

-   Identificar a imagem de arranque que pretende utilizar para iniciar o computador de destino.  

-   Utilizar uma sequência de tarefas para capturar uma imagem do sistema operativo que pretende implementar. Em alternativa, pode utilizar uma imagem predefinida do sistema operativo.  

-   Distribuir a imagem de arranque, a imagem de sistema operativo e qualquer conteúdo relacionado a um ponto de distribuição.  

-   Criar uma sequência de tarefas com os passos para implementar a imagem de arranque e a imagem do sistema operativo.  

-   Implementar a sequência de tarefas numa coleção de computadores.  

-   Monitorizar a implementação.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Cenários de implementação do sistema  
 Existem muitos cenários de implementação do sistema operativo no Gestor de Configuração que pode escolher dependendo do seu ambiente e da finalidade para a instalação do sistema operativo.  Por exemplo, pode particionar e formatar um computador existente com uma nova versão do Windows ou atualizar o Windows para a versão mais recente. Para ajudá-lo a determinar o método de implementação que satisfaz as suas necessidades, reveja [cenários para implementar sistemas operativos empresariais.](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)  Pode escolher de entre os seguintes cenários de implementação do sistema operativo:  

-   [Atualizar o Windows para a versão mais recente](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Atualizar um computador existente com uma nova versão do Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Métodos para implementar sistemas operativos  
 Existem vários métodos que pode utilizar para implementar sistemas operativos para computadores clientes do Gestor de Configuração.  

- **Implementações iniciadas por PXE**: as implementações iniciadas por PXE permitem aos computadores cliente pedir uma implementação através da rede. Neste método de implementação, a imagem de sistema operativo e uma imagem de arranque do Windows PE são enviadas para um ponto de distribuição configurado para aceitar pedidos de arranque PXE. Para mais informações, consulte [o Use PXE para implementar o Windows sobre a rede com o Gestor](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)de Configuração .  

- **Disponibilizar sistemas operativos no Centro de Software**: pode implementar um sistema operativo e disponibilizá-lo no Centro de Software. Os clientes do Gestor de Configuração podem iniciar a instalação do sistema operativo a partir do Centro de Software. Para mais informações, consulte [Substituir um computador existente e configurações de transferência](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Implementações multicast**: as implementações multicast poupam a largura de banda da rede ao enviarem dados simultaneamente para vários clientes em vez de enviarem uma cópia dos dados para cada cliente através de uma ligação independente. Neste método de implementação, a imagem de sistema operativo é enviada para um ponto de distribuição. Este, por sua vez, implementa a imagem quando os computadores cliente pedem a implementação. Para mais informações, consulte [Utilizar o Multicast para implementar o Windows sobre a rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Implementações com suportes de dados de arranque**: as implementações com suportes de dados de arranque permitem implementar o sistema operativo quando o computador de destino for iniciado. Quando o computador de destino é iniciado, obtém a sequência de tarefas, a imagem do sistema operativo e outro conteúdo necessário a partir da rede. Como esse conteúdo não está incluído no suporte de dados, pode atualizar o conteúdo sem ter de recriar o suporte de dados. Para mais informações, consulte [Criar meios de sapateado.](../deploy-use/create-bootable-media.md)  

- **Implementações com suportes de dados autónomos**: as implementações com suportes de dados autónomos permitem implementar sistemas operativos nas seguintes condições:  

  - Em ambientes onde não é prático copiar uma imagem de sistema operativo ou outros pacotes grandes através da rede.  

  - Em ambientes sem conectividade de rede ou uma conectividade de rede com largura de banda reduzida.  

    Para mais informações, consulte [Criar meios de comunicação autónomos.](../deploy-use/create-stand-alone-media.md)  

- **Implementações com suportes de dados pré-configurados**: as implementações com suportes de dados pré-configurados permitem implementar um sistema operativo num computador que não esteja totalmente aprovisionado. O suporte pré-encenado é um ficheiro de formato de imagem do Windows (WIM) que pode ser instalado num computador de metal nu pelo fabricante ou num centro de encenação empresarial que não esteja ligado ao ambiente do Gestor de Configuração.  

   Mais tarde, no ambiente do Gestor de Configuração, o computador começa por utilizar a imagem de arranque fornecida pelos meios de comunicação e, em seguida, conecta-se ao ponto de gestão do site para sequências de tarefas disponíveis que completam o processo de descarregamento. Este método de implementação pode reduzir o tráfego de rede porque a imagem de arranque e a imagem do sistema operativo já estão no computador de destino. Pode especificar aplicações, pacotes e pacotes de controladores para incluir no suporte de dados pré-configurado. Para mais informações, consulte [Criar meios pré-encenados.](../deploy-use/create-prestaged-media.md)  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a>Imagens de arranque  
 Uma imagem de arranque no Gestor de Configuração é uma imagem do Windows PE (WinPE) que é usada durante uma implementação do sistema operativo. As imagens de arranque são utilizadas para iniciar um computador no WinPE, que é um sistema operativo minimalista com componentes e serviços limitados que preparam o computador de destino para a instalação do Windows. O Gestor de Configuração fornece duas imagens de boot: uma para suportar plataformas x86 e outra para suportar plataformas x64. Estas são consideradas imagens de arranque predefinidas. As imagens de arranque que cria e adiciona ao Gestor de Configuração são consideradas imagens personalizadas. As imagens de boot predefinidas podem ser substituídas automaticamente quando actualizao o 'Gestor de Configuração'. Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Imagens de sistema operativo  
 As imagens de sistema operativo no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM) e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para todos os cenários de implementação do sistema operativo, tem de selecionar uma imagem do sistema operativo. Pode utilizar a imagem predefinida do sistema operativo ou compilar a imagem do sistema operativo a partir de um computador de referência que configurar. Para mais informações, consulte [Gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a>Pacotes de atualização do sistema operativo  
 Os pacotes de atualização do sistema operativo são utilizados para atualizar um sistema operativo e são implementações do sistema operativo iniciadas pela configuração. Importa pacotes de atualização do sistema operativo para O Gestor de Configuração a partir de um DVD ou ficheiro ISO montado. Para mais informações, consulte Gerir pacotes de [atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a>Meios de comunicação para implantar sistemas operativos  
 Pode criar vários tipos de suportes de dados que podem ser utilizados para implementar sistemas operativos. Isto inclui suportes de dados de captura, que são utilizados para capturar imagens de sistema operativo, e suportes de dados de arranque pré-configurados e autónomos, que são utilizados para implementar um sistema operativo. Ao utilizar meios de comunicação, pode implementar sistemas operativos em computadores que não tenham uma ligação de rede ou que tenham uma ligação de largura de banda baixa ao site do Seu Gestor de Configuração. Para obter mais informações sobre como usar os meios de comunicação, consulte Criar meios de sequência de [tarefas](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Controladores de dispositivos  
 Pode instalar controladores de dispositivo em computadores de destino sem os incluir na imagem do sistema operativo que está a ser implementada. O Gestor de Configuração fornece um catálogo de controladores que contém referências a todos os controladores de dispositivos que importa para O Gestor de Configuração. O catálogo de controladores está localizado na área de trabalho **Biblioteca de Software** e é composto por dois nós: **Controladores** e **Pacotes de Controladores**. O nó **Controladores** lista todos os controladores que importou para o catálogo de controladores. Pode utilizar este nó para saber os detalhes de cada controlador importado, para alterar o pacote de controladores ou a imagem de arranque a que um controlador pertence, para ativar ou desativar um controlador, etc. Para mais informações, consulte [Gerir os condutores](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Guardar e restaurar estado do utilizador  
 Quando implementa sistemas operativos, pode guardar o estado de utilizador do computador de destino, implementar o sistema operativo e, em seguida, restaurar o estado de utilizador, após a implementação do sistema operativo. Este processo é normalmente utilizado quando instala o sistema operativo num computador cliente do Gestor de Configuração.  

 As informações de estado de utilizador são capturadas e restauradas utilizando sequências de tarefas. Quando as informações de estado de utilizador são capturadas, podem ser armazenadas de uma das seguintes formas:  

- Pode armazenar os dados de estado de utilizador remotamente através da configuração de um ponto de migração de estado. A sequência de tarefas de captura envia os dados para o ponto de migração de estado. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro obtém os dados e restaura o estado de utilizador no computador de destino.  

- Pode armazenar os dados de estado de utilizador localmente numa localização específica. Neste cenário, a sequência de tarefas de captura copia os dados de utilizador para uma localização específica no computador de destino. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro obtém os dados de utilizador dessa localização.  

- Pode especificar ligações fixas que podem ser utilizadas para restaurar os dados de utilizador na localização original. Neste cenário, os dados de estado de utilizador permanecem na unidade quando o sistema operativo anterior é removido. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro utiliza as ligações fixas para restaurar os dados de estado de utilizador na localização original.  

  Para mais informações [Gerencie](../get-started/manage-user-state.md)o estado do utilizador .  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Implementar em computadores desconhecidos  
 Pode implantar um sistema operativo em computadores que não são geridos pelo Gestor de Configuração. Não há registo destes computadores na base de dados do Diretor de Configuração. Estes computadores são designados por computadores desconhecidos. Os computadores desconhecidos incluem o seguinte:  

- Um computador onde o cliente do Gestor de Configuração não está instalado  

- Um computador que não é importado para O Gestor de Configuração  

- Um computador que não é descoberto pelo Gestor de Configuração  

  Para mais informações, consulte [Prepare-se para implementações de computadordesconhecidas](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Associar utilizadores a um computador  
 Quando implementa um sistema operativo, pode associar utilizadores ao computador de destino para suportar ações de afinidade dispositivo/utilizador. Quando associa um utilizador ao computador de destino, posteriormente, o utilizador administrativo poderá efetuar ações em qualquer computador que esteja associado a esse utilizador, como implementar uma aplicação no computador de um utilizador específico. No entanto, quando implementa um sistema operativo, não é possível implementar o sistema operativo no computador de um utilizador específico. Para mais informações, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino.  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a>Utilize sequências de tarefas para automatizar passos  
 Pode criar sequências de tarefas para executar uma variedade de tarefas dentro do ambiente do Gestor de Configuração. As ações da sequência de tarefas são definidas nos passos individuais da sequência. Quando a sequência de tarefas é executada, as ações de cada passo são efetuadas ao nível da linha de comandos, sem necessidade de intervenção do utilizador. Pode utilizar sequências de tarefas para o seguinte:  

-   [Criar uma sequência de tarefas para instalar um sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Criar uma sequência de tarefas de implementações não pertencentes ao sistema operativo](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Criar uma sequência de tarefas para capturar um sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Criar uma sequência de tarefas para capturar e restaurar o estado do utilizador](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Criar uma sequência de tarefas personalizada](../deploy-use/create-a-custom-task-sequence.md)  
