---
title: Cenários para implementar sistemas operativos empresariais
titleSuffix: Configuration Manager
description: Conheça vários cenários para implementar sistemas operativos empresariais com o Gestor de Configuração.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723769"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Cenários para implantar sistemas operativos empresariais com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os seguintes cenários de implementação do OS estão disponíveis no Gestor de Configuração:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Atualizar o Windows para a versão mais recente
Este cenário atualiza o SISTEMA em computadores que atualmente executam o Windows 7, Windows 8.1 ou Windows 10. O processo de atualização mantém as aplicações, configurações e dados do utilizador no computador. Não existem dependências externas, como o Windows ADK. Este processo pode ser mais rápido e mais resistente do que as implementações tradicionais de SO.  

Para mais informações, consulte [o Upgrade Windows para a versão mais recente.](upgrade-windows-to-the-latest-version.md)


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para os dispositivos existentes
<!--3607717, fka 1358333-->
A partir da versão 1810, o Windows Autopilot para dispositivos existentes está disponível com a versão 1809 do Windows 10 ou posterior. Esta funcionalidade permite-lhe reimagem e fornecer um dispositivo Windows 7 para o modo de utilização do Windows Autopilot utilizando uma única sequência de tarefas do Gestor de Configuração.

Para obter mais informações, veja [Windows Autopilot for existing devices](windows-autopilot-for-existing-devices.md) (Windows Autopilot para dispositivos existentes).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Atualizar um computador existente com uma nova versão do Windows
Este cenário partições e formatos (toalhetes) um computador existente e instala um novo SISTEMA no computador. Pode migrar as definições e os dados do utilizador após a instalação do SISTEMA.  

Para mais informações, consulte [Refresh um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Instalar uma nova versão do Windows num novo computador (bare-metal)
Este cenário instala um SISTEMA num novo computador. É uma nova instalação do SISTEMA e não inclui nenhuma definição ou migração de dados do utilizador.  

Para mais informações, consulte [Instale uma nova versão do Windows num novo computador (metal nu)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Substituir um computador existente e transferir definições
Este cenário instala um SISTEMA num novo computador. Opcionalmente, é possível migrar as definições e dados do utilizador do computador antigo para o novo computador.  

Para mais informações, consulte [Substituir um computador existente e configurações de transferência](replace-an-existing-computer-and-transfer-settings.md).


