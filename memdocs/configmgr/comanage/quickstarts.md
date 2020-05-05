---
title: Cloud conectando-se com cogestão
titleSuffix: Configuration Manager
description: A cogestão oferece valor imediato quando o habilita.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ca960ddd6a4057da10341063f0b14a7f1d104d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075817"
---
# <a name="cloud-connecting-with-co-management"></a>Cloud conectando-se com cogestão

![Banner da série Blastoff](media/blastoff-banner.png)

A cogestão adiciona uma nova funcionalidade à implementação do Gestor de Configuração existente, sem alterar a forma como já funciona. Quando permite a cogestão, começa imediatamente a beneficiar da nuvem. Pode aplicar esse valor à sua infraestrutura e processos de gestão existentes.

Nesta série de arranque rápido de cogestão, veja como pode rapidamente impulsionar um novo valor de gestão. A cogestão foi construída para criar funcionalidades e ferramentas que pode usar agora.

No seguinte vídeo, o vice-presidente corporativo da Microsoft, Brad Anderson, apresenta esta série de cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| Valor imediato | Introdução |
|-----------------|-----------------|
| - [Acesso condicional](#bkmk_ca)<br> - [Ações remotas de Intune](#bkmk_remote)<br> - [Saúde do cliente](#bkmk_client-health)<br> - [Anúncio Híbrido Azure](#bkmk_hybrid-aad)<br> - [Piloto automático do Windows](#bkmk_autopilot) | - [Caminhos para a cogestão](#bkmk_paths)<br> - [Configurar anúncio híbrido Azure](#bkmk_setup-hybrid-aad)<br> - [Upgrade para windows 10](#bkmk_upgrade-win10)<br> - [Obtenha ajuda do FastTrack](#bkmk_fasttrack) |

## <a name="immediate-value"></a>Valor imediato

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Acesso condicional com conformidade do dispositivo** | Controlar o acesso dos utilizadores aos recursos corporativos com base nas regras de conformidade da Intune | [![Miniatura de vídeo de acesso condicional](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Ações remotas de Intune** | Executar ações remotas a partir de Intune para dispositivos cogeridos. Por exemplo, limpar e repor um dispositivo e manter a inscrição e conta | [![Miniatura de vídeo de ações remotas](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Saúde do cliente do Gestor de Configuração** | Manter a visibilidade da saúde cliente do Gestor de Configuração a partir do Intune on Azure portal | [![Miniatura de vídeo de saúde do cliente](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Diretório Ativo Azure (Azure AD)** | Com o Azure AD pode aproveitar a melhoria da produtividade dos seus utilizadores e segurança para os seus recursos, tanto em ambientes cloud como on-prem | [![Miniatura de vídeo híbrido Azure AD](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Piloto automático do Windows** | Reduzir o tempo, os recursos e a complexidade associados à implantação, gestão e dereformação ou reciclagem de dispositivos. O autopiloto também cria uma melhor experiência para os utilizadores finais. | [![Miniatura do vídeo do Piloto Automático do Windows](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>Introdução

Se quiser permitir a cogestão, comece aqui a desbloquear as preocupações técnicas que possa ter.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Caminhos para a cogestão** | Há duas formas primárias de criar a cogestão, e é importante entender os pré-requisitos para cada caminho.  Cada caminho requer alguma combinação de Azure AD, ConfigMgr, Intune e Windows client. | [![Miniatura de caminhos de cogestão deslizam](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurar anúncio híbrido Azure** | Se o seu ambiente tiver atualmente dispositivos Windows 10 unidos pelo domínio, configurar o Azure AD híbrido antes de poder ativar a cogestão | [![Miniatura de anúncio híbrido Azure configura vídeo](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Upgrade para windows 10** | Windows 10 versão 1709 ou mais tarde é necessário para cogestão | [![Miniatura do vídeo do Windows 10](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**Obtenha ajuda do FastTrack** | A organização FastTrack é um grande grupo de engenheiros da Microsoft especializados em ajudar todos os tipos de organizações a implementar aplicações microsoft 365, incluindo a criação de cogestão. | [![Miniatura de vídeo FastTrack](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
