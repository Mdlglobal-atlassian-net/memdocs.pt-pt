---
title: Implemente muitos perfis OEMConfig para dispositivos Zebra usando o Microsoft Intune - Azure [ Microsoft Docs
description: Utilize o Microsoft Intune para criar e implementar vários perfis de configuração de dispositivos OEMConfig em dispositivos Zebra que executam o Android Enterprise. Use as ações e passos da Zebra para encomendar os seus perfis.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988686"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Implemente vários perfis oEMConfig para dispositivos Zebra no Microsoft Intune

No Microsoft Intune, utilize o OEMConfig para personalizar as definições específicas do OEM para dispositivos Android Enterprise. Estas definições são específicas para o fabricante do dispositivo e implementadas utilizando perfis de configuração em Intune.

Nos dispositivos Zebra, pode implementar ou atribuir vários perfis ao mesmo dispositivo. Os perfis oemconfig existentes podem utilizar esta funcionalidade da próxima vez que os dispositivos sincronizarem com intune.

Esta funcionalidade aplica-se a:

- Dispositivos zebra que executam a Android Enterprise

Para saber mais sobre a OEMConfig, incluindo o que faz, e como usá-lo, consulte o perfil de [configuração OEMConfig](android-oem-configuration-overview.md).

Este artigo descreve a implementação de múltiplos perfis oEMConfig para dispositivos Zebra, descreve a encomenda e utiliza as funcionalidades de reporte no Microsoft Intune.

## <a name="prerequisites"></a>Pré-requisitos

Criar um perfil de [configuração OEMConfig](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Use vários perfis

Nos dispositivos Zebra, pode ter muitos perfis em cada dispositivo simultaneamente. Esta funcionalidade permite-lhe dividir as definições da Zebra OEMConfig em perfis mais pequenos. O esquema OEMConfig da Zebra também usa **Ações.** As ações são operações que funcionam no dispositivo. Não configuram nenhuma definição. Use estas ações para desencadear um download de ficheiros, limpar a área de transferência e muito mais. Para obter uma lista completa das ações apoiadas, consulte a [documentação da Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (abre o site da Zebra).

Por exemplo, cria-se um perfil Zebra OEMConfig que aplica algumas definições ao dispositivo. Outro perfil zebra OEMConfig inclui uma ação que limpa a prancheta. Atribui o primeiro perfil a um grupo de dispositivos Zebra. Mais tarde, tens de limpar a prancheta desses dispositivos. Atribui o segundo perfil ao mesmo grupo de dispositivos, sem alterar o primeiro perfil. A área de segurança do dispositivo é desobstruída sem reenviar ou afetar as definições de configuração criadas no primeiro perfil.

Noutro exemplo, atribuiu um perfil OEMConfig que configurava algumas definições do dispositivo Zebra. Recentemente, os utilizadores estão a reportar problemas com uma aplicação específica, e você quer limpar o cache da aplicação. Crie um novo perfil OEMConfig que inclua apenas a ação "cache clara". Atribuir o perfil aos dispositivos que dele necessitem.

## <a name="ordering"></a>Ordenação

Com vários perfis em cada dispositivo, a ordem que os perfis são implementados não está garantida. Este comportamento é uma limitação do Google Play. Para executar operações em sequência, pode utilizar a funcionalidade de [Transação da Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (abre o site da Zebra). Vejamos um exemplo.

Há dois perfis:

- **Perfil 1:** Liga bluetooth. Este perfil é atribuído na segunda-feira ao grupo **All Devices.**
- **Perfil 2**: Configura qualquer outra definição. Este perfil é atribuído na terça-feira ao grupo **All Devices.**

Bluetooth deve ser ligado antes da outra definição estar configurada.

Na quarta-feira, matricula-se 10 novos dispositivos Zebra com o Intune. O perfil 1 e o perfil 2 são atribuídos ao grupo **All Devices.** Depois de os novos dispositivos sincronizarem com intune, recebem os perfis. Estes dispositivos podem obter o Perfil 2 antes do perfil 1.

Utilize a função **Steps** no esquema da Zebra para confirmar que as operações são executadas em sequência. Neste caso, cria-se um perfil que tem duas Etapas de Transação. O primeiro passo inclui as definições Bluetooth, e o segundo passo configura a outra definição. Quando a aplicação OEMCong da Zebra recebe o perfil, executa os passos em ordem, garantidos pela Zebra.

Para mais informações, consulte [os passos de transação da Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (abre o site da Zebra).

## <a name="enhanced-reporting"></a>Relatórios melhorados

Implementa um perfil e é executado pela aplicação Zebra OEMConfig no dispositivo. A aplicação Zebra OEMConfig reporta o estado do perfil ao Intune. No centro de administração do Endpoint Manager, pode ver o estado dos perfis oEMConfig implantados e quaisquer erros ou avisos.

1. Abra o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione o seu perfil **Monitor**Zebra OEMConfig >  >  **estado do dispositivo**monitor . Esta opção mostra os dispositivos que têm o seu perfil OEMConfig atribuído.
3. Selecione um dispositivo > **Configuração** do dispositivo > Selecione o seu perfil Zebra OEMConfig. Esta opção mostra as definições de perfil que foram bem sucedidas ou fracassadas.

    Selecione uma linha falhada. São mostrados detalhes que têm mais informações sobre o porquê de ter falhado.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre os perfis de [configuração da OEMConfig](android-oem-configuration-overview.md).
- No administrador de dispositivos Android, configure extensões de [mobilidade (MX)](android-zebra-mx-overview.md).
- [Monitorize o estado do perfil](device-profile-monitor.md).
