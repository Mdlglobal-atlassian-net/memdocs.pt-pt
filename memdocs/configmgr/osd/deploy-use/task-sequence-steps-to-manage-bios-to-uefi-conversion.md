---
title: Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI
titleSuffix: Configuration Manager
description: Aprenda a personalizar uma sequência de tarefas de implementação do sistema operativo para preparar uma partição FAT32 para a transição para o UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079370"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI
O Windows 10 fornece muitas novas funcionalidades de segurança que requerem dispositivos ativados pela UEFI. Pode ter computadores windows modernos que suportam o UEFI, mas estão a usar BIOS legados. A conversão de um dispositivo para UEFI obrigou-o a ir a cada PC, a repartipartição do disco rígido e a reconfigurar o firmware. Ao utilizar sequências de tarefas no Diretor de Configuração, pode preparar um disco rígido para a conversão BIOS para a UEFI, converter de BIOS para UEFI como parte do processo de atualização no local e recolher informações da UEFI como parte do inventário de hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações da UEFI
A partir da versão 1702, uma nova classe de inventário de hardware **(SMS_Firmware**) e propriedade **(UEFI**) estão disponíveis para ajudá-lo a determinar se um computador começa no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** está definida para **TRUE**. Isto é ativado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../../core/clients/manage/inventory/configure-hardware-inventory.md)de hardware .

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Crie uma sequência de tarefas personalizada para preparar o disco rígido para a conversão DE BIOS para a UEFI
A partir da versão 1610 do Gestor de Configuração, pode agora personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, tSUEFIDrive, para que o passo **do Restart Computer** prepare uma partição FAT32 no disco rígido para a transição para o UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para a conversão BIOS para A UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Numa sequência de tarefas existente para instalar um sistema operativo, irá adicionar um novo grupo com passos para fazer o BIOS à conversão UEFI.

1. Crie um novo grupo de sequência de tarefas após os passos para capturar ficheiros e configurações, e antes dos passos para instalar o sistema operativo. Por exemplo, crie um grupo após o grupo **De captura de Ficheiros e Definições** denominado **BIOS-to-UEFI**.
2. No separador **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **_SMSTSBootUEFI** não é **igual** a **verdadeiro**. Isto impede que os passos do grupo sejam funcionados quando um computador já se encontra no modo UEFI.

   ![BIOS para o grupo UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Sob o novo grupo, adicione o passo da sequência de tarefas **restart Computer.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada** para iniciar o computador no Windows PE.  
4. No separador **Opções,** adicione uma variável de sequência de tarefas como uma condição em que **_SMSTSInWinPE é igual a falso**. Isto impede que este passo seja decorrido se o computador já estiver no Windows PE.

   ![Reiniciar passo do computador](../../core/get-started/media/restart-in-windows-pe.png)
5. Adicione um passo para iniciar a ferramenta OEM que converterá o firmware de BIOS para UEFI. Este será normalmente um passo de sequência de tarefa de Linha de **Comando de Execução** com uma linha de comando para iniciar a ferramenta OEM.
6. Adicione o passo de sequência de tarefas do Formato e do Disco de Partição que irá dividir e formatar o disco rígido. No passo, faça o seguinte:
   1. Crie a partição FAT32 que será convertida para UEFI antes da instalação do sistema operativo. Escolha **GPT** para **o tipo de disco**.
    ![Passo do disco de formato e divisória](../media/format-and-partition-disk.png)
   2. Vá para as propriedades para a partição FAT32. Introduza **o TSUEFIDrive** no campo **Variável.** Quando a sequência de tarefas detetar esta variável, preparar-se-á para a transição UEFI antes de reiniciar o computador.
    ![Propriedades de partição](../../core/get-started/media/partition-properties.png)
   3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para salvar o seu estado e armazenar ficheiros de registo.
7. Adicione o passo da sequência de tarefas **do Computador Restart.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada** para iniciar o computador no Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
A Atualização de Criadores do Windows 10 introduz uma ferramenta de conversão simples que automatiza o processo de repartição do disco rígido para hardware ativado pela UEFI e integra a ferramenta de conversão no processo de atualização do Windows 7 para o Windows 10. Quando combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para a Atualização de Criadores do Windows 10.

**Requisitos:**
- Atualização de Criadores do Windows 10
- Computadores que suportam o UEFI
- Ferramenta OEM que converte o firmware do computador de BIOS para UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Para converter de BIOS para UEFI durante uma atualização no local
1. Crie uma sequência de tarefas de atualização do sistema operativo que execute uma atualização no local para a Atualização de Criadores do Windows 10.
2. Editar a sequência de tarefas. No **grupo pós-processamento,** adicione os seguintes passos de sequência de tarefas:
   1. Do General, adicione um passo da Linha de **Comando de Execução.** Irá adicionar a linha de comando para a ferramenta MBR2GPT que dissimula um disco de MBR a GPT sem modificar ou apagar dados do disco. Na linha comando, escreva o seguinte: **MBR2GPT /converter /disco:0 /Permitir FullOs**. Também pode optar por executar o MBR2GPT. Ferramenta EXE quando no Windows PE em vez de em todo o sistema operativo. Pode fazê-lo adicionando um passo para reiniciar o computador ao WinPE antes do passo para executar o MBR2GPT. Ferramenta EXE e remoção da opção /Permitir FullOS da linha de comando. Para mais detalhes sobre a ferramenta e opções disponíveis, consulte [MBR2GPT. EXE.](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt)
   2. Adicione um passo para iniciar a ferramenta OEM que converterá o firmware de BIOS para UEFI. Este será normalmente um passo de sequência de tarefa de Linha de Comando de Execução com uma linha de comando para iniciar a ferramenta OEM.
   3. Do General, adicione o passo **restart Computer.** Para especificar o que executar após o reinício, selecione **O sistema operativo predefinido atualmente instalado**.
3. Implante a sequência de tarefas.
