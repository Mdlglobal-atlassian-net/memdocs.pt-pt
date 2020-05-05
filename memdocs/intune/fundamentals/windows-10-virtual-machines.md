---
title: Utilização de máquinas virtuais do Windows 10 com o Microsoft Intune
titleSuffix: ''
description: Diretrizes para utilizar máquinas virtuais do Windows 10 com microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 944b3d98dc59dcae69f72fef5dfdb1793701f67a
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126182"
---
# <a name="using-windows-10-virtual-machines-with-intune"></a>Utilização de máquinas virtuais do Windows 10 com Intune

O Intune suporta a gestão de máquinas virtuais que executam o Windows 10 Enterprise com determinadas limitações. A gestão intune não depende, nem interfere com a gestão do Ambiente de Trabalho Virtual do Windows da mesma máquina virtual.

Ao gerir os VMs do Windows 10 com intune, tenha em mente os seguintes pontos:

- O Windows 10 Enterprise Multi Session (Enterprise for Virtual Devices) usado no Windows Virtual Desktop não suporta atualmente a gestão intune.

## <a name="enrollment"></a>Inscrição
- Não recomendamos gerir máquinas virtuais a pedido e anfitriãs de sessões com intune. Cada VM deve ser matriculado quando é criado. Além disso, a apagar regularmente VMs deixará registos de dispositivos órfãos em Intune até que sejam [limpos](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules). 
- Os tipos de auto-implementação do Windows Autopilot e de implementação de luvas brancas não são suportados porque necessitam de um Módulo de Plataforma Fidedigna físico (TPM). 
- A inscrição fora da Box Experience (OOBE) não é suportada em VMs que só podem ser acedidos utilizando RDP (como VMs que estão hospedados no Azure). Esta restrição significa:
    - O Windows Autopilot e o Commercial OOBE não são suportados.
    - As opções da Página de Estado de Inscrição para políticas de contexto do dispositivo não são suportadas.


## <a name="configuration"></a>Configuração
A Intune não suporta qualquer configuração que utilize um Módulo de Plataforma Fidedigna ou gestão de hardware, incluindo:
- [Definições bitLocker](../configuration/device-profiles.md#endpoint-protection)
- [Definições de interface de configuração de firmware do dispositivo](../configuration/device-profiles.md#device-firmware-configuration-interface)

## <a name="reporting"></a>Relatórios
Intone automaticamente as máquinas virtuais e reporta-as como "Máquina Virtual" em **Dispositivos** > **Todos os dispositivos** > escolher um dispositivo > campo **Overview** > **Model.** 

As máquinas virtuais deallocatedas podem contribuir para relatórios de dispositivos não conformes porque não conseguem [fazer o check-in com o serviço Intune](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="retirement"></a>Extinção
Se tiver apenas acesso rdp, não utilize a [ação Wipe](../remote-actions/devices-wipe.md#wipe). A ação Wipe eliminará as definições de RDP da máquina virtual e impedirá que volte a ligar-se.


