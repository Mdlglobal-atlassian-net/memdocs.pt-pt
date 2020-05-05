---
title: Escolher uma solução de gestão de dispositivos
titleSuffix: Configuration Manager
description: Conheça as soluções que a Microsoft oferece para gerir Computadores, servidores e dispositivos.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719268"
---
# <a name="choose-a-device-management-solution"></a>Escolher uma solução de gestão de dispositivos

A Microsoft oferece diferentes soluções para a gestão de Computadores, servidores e dispositivos. Estas soluções estão disponíveis no local, baseadas em nuvem, ou uma combinação de ambas. Escolha a solução que é certa para os requisitos de negócio da sua organização. Baseie a sua decisão nas plataformas do dispositivo que precisa de gerir e na funcionalidade de gestão de que necessita.

## <a name="overview"></a>Descrição geral

Existem várias soluções Microsoft que podem funcionar melhor para si em diferentes cenários. Não precisas de escolher apenas um.

- Para uma pequena organização, uma ferramenta como o centro de administração do Windows pode ser um ótimo ajuste.
- Aproximadamente 75% das organizações de TI usam o Gestor de Configuração para gerir os seus dispositivos.
- O Microsoft Azure fornece várias soluções a partir da nuvem ou no local com o Azure Stack que visa principalmente a gestão do servidor.
- A Microsoft Intune fornece a gestão na nuvem dos clientes.
- Pode combinar O Gestor de Configuração e insintonização com a cogestão.

Utilize a tabela seguinte para ajudar a comparar estas tecnologias de gestão:

|  | Apenas cloud | Ligado à nuvem | Local | Desligado |
|---------|---------|---------|---------|---------|
| **Anfitrião Hyper-V** | Não aplicável | - Pilha Azure<br/> - Windows Admin Center<br/> - Gestor de Máquinas Virtuais | - Pilha Azure<br/> - Windows Admin Center<br/> - Gestor de Máquinas Virtuais | - Pilha Azure<br/> - Windows Admin Center<br/> - Gestor de Máquinas Virtuais |
| **Windows Server** | - Gestão azure<br/> - Gestor de Configuração | - Gestão azure<br/> - Gestor de Configuração | - Gestão azure<br/> - Gestor de Configuração | Gestor de configuração |
| **Servidor Linux** | Gestão do Azure | Gestão do Azure | Gestão do Azure |  |
| **Windows 10** | - Insintonizado<br/> - Gestor de Configuração | - Insintonizado<br/> - Gestor de Configuração | - Insintonizado<br/> - Gestor de Configuração | Gestor de configuração |
| **Windows 7 ou 8.1** | Gestor de configuração | Gestor de configuração | Gestor de configuração | Gestor de configuração |
| **Windows Virtual Desktop** | Gestor de configuração | Não aplicável | Não aplicável | Não aplicável |

Para obter mais informações, veja os artigos seguintes:

- [O que é o Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [O que é o Windows Admin Center?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [O que é o Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Produtos de gestão Azure](https://docs.microsoft.com/azure/)
- [O que é o Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview)

Para obter mais informações sobre o Gestor de Configuração e as soluções Intune, continue para a secção seguinte.

## <a name="client-management"></a>Gestão de clientes

Esta secção compara as seguintes quatro soluções de gestão de clientes:

- [Cliente do Gestor de Configuração](#bkmk_sccm)
- [Gestão de dispositivos móveis no local (MDM) com Gestor de Configuração](#bkmk_opmdm)
- [Cogestão com a Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Podem utilizar estas soluções por si sós ou em combinação entre si. Por exemplo, utilize a abordagem de gestão baseada no cliente para gerir os computadores e servidores da sua organização, e também use a cogestão para gerir computadores portáteis baseados na Internet. Ao combinar abordagens desta forma, pode cobrir todas as necessidades de gestão do seu dispositivo.  

Há também duas tabelas que comparam as soluções de gestão pelos seguintes fatores:

- [Comparar por plataformas suportadas](#bkmk_comp1)
- [Comparar pela funcionalidade de gestão](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a>Cliente do Gestor de Configuração  

Esta opção requer a instalação do cliente do Gestor de Configuração em dispositivos. Fornece mais funcionalidades para gerir Computadores, servidores e outros dispositivos no seu ambiente.

Para mais informações, consulte os métodos de [instalação do Cliente.](../clients/deploy/plan/client-installation-methods.md)  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a>NO LOCAL MDM  

Esta opção utiliza as capacidades de gestão do dispositivo incorporadas no Windows 10. Embora não tão destacado como a gestão baseada no cliente, o MDM no local fornece uma abordagem mais leve à gestão. Utiliza recursos do Gestor de Configuração no local para gerir dispositivos.  

Para mais informações, consulte [Gerir dispositivos móveis com infraestrutura no local.](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a>Cogestão com a Microsoft Intune

A cogestão é uma das principais formas de anexar a implementação do seu Gestor de Configuração existente à nuvem Microsoft 365. Permite-lhe gerir simultaneamente os dispositivos do Windows 10 utilizando tanto o 'Configuração Manager' como o Microsoft Intune. A cogestão permite-lhe anexar o seu investimento existente em 'Gestor de Configuração', adicionando novas funcionalidades.

Para mais informações, veja [o que é a cogestão?](../../comanage/overview.md)  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a>Intercâmbio microsoft  

Esta opção utiliza o conector Do Servidor de Câmbio para ligar vários servidores de troca ao Gestor de Configuração. Centraliza a gestão de dispositivos que podem ligar-se ao Exchange ActiveSync. Pode configurar as funcionalidades de gestão de dispositivos móveis Exchange a partir da consola 'Gestor de Configuração'. As funcionalidades do exemplo incluem a limpeza remota do dispositivo e o controlo de definições para vários servidores de Troca.

Para mais informações, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a>Comparar soluções por plataformas suportadas  

|Plataforma|Cliente do Gestor de Configuração|On-premises MDM (MDM no local)|Gestor de configuração com troca| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Sim| Sim |
|iOS| | |Sim| Sim |
|Mac OS X|Sim| |Sim| Sim |
|Windows 10|Sim|Sim|Sim| Sim |
|Windows 10 Mobile| |Sim|Sim| Sim |
|Windows (versões anteriores)|Sim| |Sim|  |
|Windows Server|Sim| |Sim|  |
|Windows Embedded|Sim| | |  |

Para obter uma lista completa de plataformas suportadas, consulte os seguintes artigos:

- [Sistemas operativos suportados para clientes e dispositivos para Gestor de Configuração](configs/supported-operating-systems-for-clients-and-devices.md)
- [Configurações suportadas intune](https://docs.microsoft.com/intune/supported-devices-browsers)

A Microsoft recomenda a utilização de Dispositivos móveis Android, iOS e Windows 10. Para mais informações, consulte [o que é microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a>Comparar soluções por funcionalidade de gestão  

|Funcionalidade de gestão|Cliente do Gestor de Configuração|On-premises MDM (MDM no local)|Gestor de configuração com troca|  
|--------|----------------------------|---------------|-----------------------------------|  
|Autenticação mútua baseada em certificado|Sim|Sim| |
|Instalação do cliente|Sim| | |
|Suporte através da internet|Sim| | |
|Deteção|Sim| |Sim|
|Inventário de Hardware|Sim|Sim|Sim|
|Inventário de software|Sim| |Sim|
|Definições|Sim|Sim|Sim|
|Implementação de software|Sim|Sim| |
|Gestão de atualizações de software|Sim| | |
|Implementação de SO|Sim| | |
|Bloco do Gestor de Configuração|Sim|Sim| |
|Quarentena e bloqueio do Servidor de Intercâmbio (e Gestor de Configuração)| | |Sim|
|Eliminação remota| |Sim|Sim|
