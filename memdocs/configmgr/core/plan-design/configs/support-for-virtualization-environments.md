---
title: Apoio à virtualização
titleSuffix: Configuration Manager
description: Os requisitos para instalar funções de cliente e sistema de site do Gestor de Configuração num ambiente de virtualização.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709594"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Suporte para ambientes de virtualização com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta a instalação das funções do sistema de cliente e site em sistemas operativos suportados que funcionam como uma máquina virtual nos ambientes de virtualização neste artigo. Este suporte existe mesmo quando o hospedeiro virtual da máquina (ambiente de virtualização) não é suportado como um cliente ou servidor de site.  

Por exemplo, utiliza o Microsoft Hyper-V Server 2012 para alojar uma máquina virtual que executa o Windows Server 2012. Pode instalar as funções do cliente ou do sistema do site na máquina virtual que executa o Windows Server 2012. Não é possível instalar o cliente no anfitrião que executa o Microsoft Hyper-V Server 2012.  

## <a name="virtualization-environments"></a>Ambientes de virtualização

- Windows Server 2019  
- Windows Server 2016 <sup> [Nota 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Nota 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a>Nota 1: Virtualização aninhada

O Gestor de Configuração não suporta a [virtualização aninhada](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), que é novidade com o Windows Server 2016.

### <a name="virtualization-environment-support"></a>Suporte ambiental de virtualização

Cada computador virtual precisa dos mesmos ou maiores requisitos de hardware e software que utilizaria para um computador de Configuração Física.  

Para validar que o seu ambiente de virtualização é suportado para O Gestor de Configuração, utilize o Programa de Validação de Virtualização do Servidor. Inclui um Assistente de Política de Apoio ao Programa de Virtualização online. Para mais informações, consulte o Programa de [Validação de Virtualização](https://www.windowsservercatalog.com/svvp.aspx)do Servidor do Windows .  

> [!NOTE]  
> O Gestor de Configuração não suporta sistemas operativos de pc virtual ou servidor virtual que funcionam em computadores Mac.  

O Gestor de Configuração não consegue gerir máquinas virtuais se estiverem offline. Uma imagem de máquina virtual offline não pode ser atualizada nem o inventário pode ser recolhido utilizando o cliente Do Gestor de Configuração no computador anfitrião.  

Não existem considerações especiais para as máquinas virtuais. Por exemplo, o Gestor de Configuração pode não determinar se uma atualização tem de ser reaplicada a uma imagem de máquina virtual se a máquina virtual tiver sido interrompida e reiniciada sem salvar o estado da máquina virtual à qual a atualização foi aplicada.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  

O Gestor de Configuração pode funcionar em máquinas virtuais em Azure, assim como funciona no local dentro do seu centro de dados. Utilize o Gestor de Configuração com máquinas virtuais Azure nos seguintes cenários:  

- **Cenário 1**: Executar O Gestor de Configuração numa máquina virtual Azure. Use-o para gerir clientes em outras máquinas virtuais Azure.  

- **Cenário 2**: Executar O Gestor de Configuração numa máquina virtual Azure. Usa-o para gerir clientes que não estão a funcionar no Azure.  

- **Cenário 3**: Executar diferentes funções do sistema do site do Gestor de Configuração em máquinas virtuais Azure. Execute outras funções no seu centro de dados no local, devidamente ligado ao Azure.  

Os mesmos requisitos do Gestor de Configuração para redes, configurações suportadas e requisitos de hardware que se aplicam à instalação no local também se aplicam à instalação em máquinas virtuais Azure.  

Para mais informações, consulte [O Gestor de Configuração no Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> Sites e clientes do Gestor de Configuração que funcionam em máquinas virtuais Azure estão sujeitos aos mesmos requisitos de licença que as instalações no local.  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[O Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) é uma funcionalidade de pré-visualização do Microsoft Azure e do Microsoft 365. A partir da versão 1906, utilize o Gestor de Configuração para gerir estes dispositivos virtuais que executam o Windows em Azure. Para mais informações, consulte [sistemas operativos suportados para clientes e dispositivos.](supported-operating-systems-for-clients-and-devices.md)
