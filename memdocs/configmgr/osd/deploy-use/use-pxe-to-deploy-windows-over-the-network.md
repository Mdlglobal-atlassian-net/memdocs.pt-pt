---
title: Use O PXE para OSD sobre a rede
titleSuffix: Configuration Manager
description: Utilize implementações de OS iniciadas pelo PXE para atualizar o sistema operativo de um computador ou para instalar uma nova versão do Windows num novo computador.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11045ff31dc3832ac97d62f491561b3cf989813c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079353"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Utilize o PXE para implementar o Windows sobre a rede com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As implementações de Sistema soinuos (PXE) iniciadas pelo PReboot no Gestor de Configuração permitem aos clientes solicitar e implantar sistemas operativos em toda a rede. Neste cenário de implementação, envia a imagem de OS e as imagens de arranque para um ponto de distribuição ativado por PXE.

> [!NOTE]  
> Quando criar uma implementação de SO que visa apenas os computadores X64 BIOS, tanto a imagem de arranque x64 como a imagem de arranque x86 devem estar disponíveis no ponto de distribuição.

Pode utilizar implementações de SO iniciadas pelo PXE nos seguintes cenários:

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

Complete os passos num dos cenários de implantação do SO e, em seguida, use as secções deste artigo para se preparar para implementações iniciadas pelo PXE.

> [!WARNING]
> Se utilizar as implementações pXE e configurar o hardware do dispositivo com o adaptador de rede como o primeiro dispositivo de arranque, estes dispositivos podem iniciar automaticamente uma sequência de tarefas de implementação de SISTEMAS sem interação do utilizador. A verificação de implementação não gere esta configuração. Embora esta configuração possa simplificar o processo e reduzir a interação do utilizador, coloca o dispositivo em maior risco de reimagem acidental.

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE

Para implementar sistemas operativos para clientes do Gestor de Configuração que fazem pedidos de arranque PXE, deve configurar um ou mais pontos de distribuição para aceitar pedidos de PXE. Uma vez configurado o ponto de distribuição, ele responde aos pedidos de arranque pXE e determina as medidas de implementação apropriadas a tomar. Para mais informações, consulte [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

> [!NOTE]  
> Ao configurar um único ponto de distribuição ativado por PXE para suportar várias subredes, não é suportado para utilizar opções de DHCP. Configure os ajudantes IP nos routers para permitir que os pedidos de PXE sejam encaminhados para os seus pontos de distribuição ativados pXE.
>
> Na versão 1810, não é suportado para usar o resposta PXE sem WDS em servidores que também estão executando um servidor DHCP.
>
> A partir da versão 1902, quando ativa um xeque PXE num ponto de distribuição sem o Windows Deployment Service, pode agora estar no mesmo servidor que o serviço DHCP.<!--3734270, SCCMDocs-pr #3416--> Adicione as seguintes definições para suportar esta configuração:  
>
> - Defina o valor DWord **DoNotListenOnDhcpPort** `1` na `HKLM\Software\Microsoft\SMS\DP`seguinte tecla de registo: .
> - Definir a opção DHCP 60 para `PXEClient`.  
> - Reiniciar os serviços SCCMPXE e DHCP no servidor.  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE

Para utilizar o PXE para implementar um OS, deve ter imagens de arranque ativadas por X86 e X64 PXE distribuídas por um ou mais pontos de distribuição ativados por PXE. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:

- Para ativar o PXE numa imagem de arranque, selecione Implementar esta imagem de arranque a partir do ponto de **distribuição ativado pelo PXE** a partir do separador **Data Source** nas propriedades da imagem de arranque.

- Se alterar as propriedades para a imagem de arranque, atualize e redistribua a imagem de arranque para pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Gerir identificadores de hardware duplicados

O Gestor de Configuração pode reconhecer vários computadores como o mesmo dispositivo se tiverem atributos SMBIOS duplicados ou utilizar um adaptador de rede partilhado. Atenuar estes problemas gerindo identificadores de hardware duplicados em definições de hierarquia. Para mais informações, consulte [Gerir identificadores de hardware duplicados](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE

> [!Note]  
> Em algumas circunstâncias, o processo de Gestão de [identificadores de hardware duplicados](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) pode ser mais fácil.<!-- SCCMDocs issue 802 -->
>
> Os comportamentos de cada um podem causar resultados diferentes em alguns cenários. A lista de exclusão nunca enche um cliente com o endereço MAC listado, não importa o que aconteça.
>
> A lista de id duplicado não usa o endereço MAC para encontrar a política de sequência de tarefas para um cliente. Se corresponder ao ID SMBIOS, ou se houver uma política de sequência de tarefas para máquinas desconhecidas, o cliente ainda arranca.

Ao implementar sistemas operativos com PXE, pode criar uma lista de exclusão em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusão dos computadores que pretende que o ponto de distribuição ignore. Os computadores listados não recebem as sequências de tarefas de implementação que o Gestor de Configuração utiliza para a implementação do PXE.

### <a name="process-to-create-the-exclusion-list"></a>Processo para criar a lista de exclusão

1. Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.  

2. Utilize um editor de texto simples, como o Notepad, e adicione os endereços MAC dos computadores para serem ignorados pelo ponto de distribuição ativado pelo PXE. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`  

3. Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O ficheiro de texto pode ser guardado em qualquer local do servidor.  

4. Editar o registo do ponto de distribuição ativado por PXE para criar uma chave de registo **MACIgnoreListFile.** Adicione o valor de cadeia do caminho completo para o ficheiro de texto no servidor do sistema de pontode distribuição ativado pelo PXE. Utilize o caminho de registo seguinte:  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > Se utilizar o Editor de Registo sem complicações, poderá causar problemas graves que podem exigir que reinstale o Windows. A Microsoft não pode garantir que pode resolver problemas que resultem da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

5. Reinicie o serviço WDS ou o serviço de resposta PXE depois de fazer esta alteração de registo. Não precisas de reiniciar o servidor.<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>Tamanho do bloco RamDisk TFTP e tamanho da janela

Pode personalizar o bloco RamDisk TFTP e os tamanhos das janelas para pontos de distribuição ativados por PXE. Se personalizar a sua rede, um grande bloco ou tamanho da janela pode fazer com que o download da imagem de arranque falhe com um erro de tempo. As personalizações do bloco RamDisk TFTP e do tamanho da janela permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os seus requisitos de rede específicos. Para determinar qual a configuração mais eficiente, teste as definições personalizadas no seu ambiente. Para obter mais informações, consulte [Personalizar o tamanho do bloco RamDisk TFTP e o tamanho da janela nos pontos de distribuição ativados pelo PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurar definições de implementação

Para utilizar uma implementação de Os iniciado pelo PXE, configure a implementação para disponibilizar o OS para pedidos de boot PXE. Configure os sistemas operativos disponíveis no separador Definições de **Implementação** nas propriedades de implementação. Para o **Disponibilizar para a seguinte** definição, selecione uma das seguintes opções:

- Clientes, meios de comunicação e PXE do Gestor de Configuração

- Apenas suportes de dados e PXE

- Apenas suportes de dados e PXE (oculto)

## <a name="option-82-during-pxe-dhcp-handshake"></a>Opção 82 durante o aperto de mão PXE DHCP
Começando com a versão 1906, a opção 82 durante o aperto de mão PXE DHCP é suportada com o resposta PXE sem WDS. Se for necessária a opção 82, certifique-se de utilizar o responsado PXE sem WDS. A opção 82 não é suportada com a WDS.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implementar a sequência de tarefas

Desloque o SO para uma coleção de alvos. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.

- **Implementação necessária**: As implementações necessárias utilizam o PXE sem qualquer intervenção do utilizador. O utilizador não pode contornar a bota PXE. No entanto, se o utilizador cancelar a bota PXE antes da resposta do ponto de distribuição, o SISTEMA não está implantado.

- **Implementação disponível**: As implementações disponíveis requerem que o utilizador esteja presente no computador de destino. Um utilizador deve premir a tecla **F12** para continuar o processo de arranque PXE. Se um utilizador não estiver presente para premir **F12,** as botas do computador no sistema operativo atual ou a partir do próximo dispositivo de arranque disponível.

Pode reimplantar uma implementação PXE necessária, limpando o estado da última implementação pXE atribuída a uma coleção de Gestor de Configuração ou a um computador. Para obter mais informações sobre a ação **de Implementações PXE claras,** consulte [Gerir clientes](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) ou [gerir coleções](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Esta ação repõe o estado dessa implementação e reinstala as mais recentes implementações necessárias.

> [!IMPORTANT]  
> O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, como num centro de dados para impedir o acesso não autorizado ao seu site.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Como a imagem de arranque é selecionada para PXE

Quando um cliente arranca com PXE, o Gestor de Configuração fornece ao cliente uma imagem de arranque para usar. O Gestor de Configuração usa uma imagem de arranque com uma correspondência exata de arquitetura. Se uma imagem de arranque com a arquitetura exata não estiver disponível, o Gestor de Configuração usa uma imagem de arranque com uma arquitetura compatível.

A lista seguinte fornece detalhes sobre como uma imagem de arranque é selecionada para clientes que iniciam com PXE:  

1. O Gestor de Configuração procura na base de dados do site o registo do sistema que corresponde ao endereço MAC ou SMBIOS do cliente que está a tentar arrancar.  

    > [!NOTE]  
    > Se um computador que é atribuído a um site botas para PXE para um site diferente, as políticas não são visíveis para o computador. Por exemplo, se um cliente já está designado para o site A, o ponto de gestão e ponto de distribuição do site B não é capaz de aceder às políticas do site A. O cliente não consegue arrancar pXE com sucesso.  

2. O Gestor de Configuração procura sequências de tarefas que são implementadas para o registo do sistema encontrado no passo 1.  

3. Na lista de sequências de tarefas encontradas no passo 2, o Gestor de Configuração procura uma imagem de arranque que corresponda à arquitetura do cliente que está a tentar arrancar. Se uma imagem de bota for encontrada com a mesma arquitetura, essa imagem de arranque é usada.  

    Se encontrar mais do que uma imagem de arranque, utiliza o ID de implementação de sequência de *tarefas mais elevado* ou mais recente. No caso de uma hierarquia multi-site, o site de letras *mais alto* teria precedência nessa comparação de cordas. Por exemplo, se ambos estiverem combinados de outra forma, uma implantação com um ano de idade do site ZZZ é selecionada sobre a implantação de ontem do site AAA.<!-- SCCMDocs issue 877 -->  

4. Se uma imagem de arranque não for encontrada com a mesma arquitetura, o Gestor de Configuração procura uma imagem de arranque compatível com a arquitetura do cliente. Está na lista de sequências de tarefas encontradas no passo 2. Por exemplo, um cliente BIOS/MBR de 64 bits é compatível com imagens de botas de 32 bits e 64 bits. Um cliente BIOS/MBR de 32 bits é compatível com apenas imagens de arranque de 32 bits. Os clientes UEFI só são compatíveis com a arquitetura correspondente. Um cliente UEFI de 64 bits é compatível com apenas 64 imagens de boot e um cliente UEFI de 32 bits é compatível com apenas imagens de botas de 32 bits.
