---
title: Converter BIOS para UEFI
titleSuffix: Configuration Manager
description: Aprenda a personalizar uma sequência de tarefas de implementação de OS para preparar uma partição FAT32 para a transição para a UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0118dd448520a6f0c21bfeea5f8509bd8e49fd46
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429409"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI

O Windows 10 fornece muitas novas funcionalidades de segurança que requerem dispositivos ativados pela UEFI. Pode ter dispositivos Windows mais recentes que suportam o UEFI, mas estão a utilizar bios legados. Anteriormente, a conversão de um dispositivo para UEFI exigia que fosse a cada dispositivo, repartipartipartia o disco rígido e reconfigurasse o firmware.

Com o Gestor de Configuração pode automatizar as seguintes ações:

- Prepare um disco rígido para bios para conversão UEFI
- Converter de BIOS para UEFI como parte do processo de atualização no local
- Recolher informações da UEFI como parte do inventário de hardware

## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações da UEFI

A classe de inventário de hardware **(SMS_Firmware)** e propriedade **(UEFI**) estão disponíveis para ajudá-lo a determinar se um computador começa no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** está definida para **TRUE**. O inventário de hardware permite esta classe por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../../core/clients/manage/inventory/configure-hardware-inventory.md)de hardware .

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Crie uma sequência de tarefas personalizada para preparar o disco rígido

Pode personalizar uma sequência de tarefas de implementação de OS com a variável **TSUEFIDrive.** O passo **Restart Computer** prepara uma partição FAT32 no disco rígido para a transição para a UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para fazer esta ação.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Prepare a partição FAT32 para a conversão para UEFI

Numa sequência de tarefas existente para instalar um SISTEMA, adicione um novo grupo com passos para fazer o BIOS à conversão UEFI.

1. Crie um novo grupo de sequência de tarefas após os passos para capturar ficheiros e definições, e antes dos passos para instalar o SISTEMA. Por exemplo, crie um grupo após o grupo **De captura de Ficheiros e Definições** denominado **BIOS-to-UEFI**.

1. No separador **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como condição. Definir **_SMSTSBootUEFI não é igual verdade.** Com esta condição, a sequência de tarefas apenas executa estes passos em dispositivos BIOS.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Condição do BIOS para o grupo UEFI":::

1. Sob o novo grupo, adicione o passo da sequência de tarefas **restart Computer.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada**. Esta ação reinicia o computador no Windows PE.

1. No separador **Opções,** adicione uma variável de sequência de tarefacomo condição. Definir **_SMSTSInWinPE é igual a falso.** Com esta condição, a sequência de tarefas não corre este passo se o computador já estiver no Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Condição no passo do computador de reinício":::

1. Adicione um passo para iniciar uma ferramenta OEM para converter o firmware de BIOS para UEFI. Este passo é tipicamente executar linha de **comando,** com o comando para executar a ferramenta OEM.

1. Adicione o passo de sequência de tarefas do **Formato e do Disco de Partição.** Neste passo, configure as seguintes opções:

    1. Crie a partição FAT32 para converter para UEFI antes da instalação do SISTEMA. Para **o tipo de disco,** escolha **GPT**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Configuração do formato e passo do disco de partição":::

    1. Vá para as propriedades para a partição FAT32. No campo **Variável,** insira `TSUEFIDrive` . Quando a sequência de tarefas deteta esta variável, prepara a partição para a transição UEFI antes de reiniciar o computador.

        :::image type="content" source="media/partition-properties.png" alt-text="Configuração de propriedades de partição FAT32":::

    1. Crie uma partição NTFS que a sequência de tarefas utiliza para salvar o seu estado e armazenar ficheiros de registo.

1. Adicione mais um passo de sequência de tarefas **do Computador Restart.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada** para iniciar o computador no Windows PE.

    > [!TIP]
    > Por padrão, o tamanho da divisória EFI é de 500 MB. Em alguns ambientes, a imagem de arranque é muito grande para armazenar nesta divisória. Para contornar esta questão, aumente o tamanho da partição da EFI. Por exemplo, coloque-o em 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a>Converter de BIOS para UEFI durante a atualização no local

O Windows 10 inclui uma simples ferramenta de conversão, **MBR2GPT**. Automatiza o processo de repartição do disco rígido para hardware ativado pela UEFI. Pode integrar a ferramenta de conversão no processo de atualização no local para o Windows 10. Combine esta ferramenta com a sua sequência de tarefas de atualização e a ferramenta OEM que converte o firmware de BIOS para UEFI.

### <a name="requirements"></a>Requisitos

- Uma versão suportada do Windows 10
- Computadores que suportam o UEFI
- Ferramenta OEM que converte o firmware do computador de BIOS para UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Processo de conversão de BIOS para UEFI durante uma sequência de tarefas de atualização no local

1. [Criar uma sequência de tarefas para atualizar um SO](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Editar a sequência de tarefas. No grupo **pós-processamento,** enumere as seguintes alterações:

    1. Adicione o passo **da Linha de Comando de Execução.** Especifique a linha de comando da ferramenta MBR2GPT. Quando executar o sistema operativo completo, configure-o para dissimular o disco de MBR a GPT sem modificar ou apagar dados. Na **linha de comando,** insira o seguinte comando:`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > Também pode optar por executar o MBR2GPT. Ferramenta EXE quando no Windows PE em vez de em todo o SISTEMA. Adicione um passo para reiniciar o computador ao Windows PE antes do passo para executar o MBR2GPT. Ferramenta EXE. Em seguida, retire a opção **/Permitir FullOS** da linha de comando.

    Para mais informações sobre a ferramenta e opções disponíveis, consulte [MBR2GPT. EXE.](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)

    1. Adicione um passo para executar a ferramenta OEM que converte o firmware de BIOS para UEFI. Este passo é tipicamente executar linha de **comando,** com uma linha de comando para executar a ferramenta OEM.

    1. Adicione o passo **restart Computer** e selecione O sistema **operativo predefinido atualmente instalado**.

1. Implante a sequência de tarefas.
