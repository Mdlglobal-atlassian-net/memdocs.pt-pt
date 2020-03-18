---
title: Conector Better Mobile Threat Defense com o Intune
titleSuffix: Intune on Azure
description: Configure o conector Better Mobile Threat Defense com o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329909"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Conector Better Mobile Threat Defense com o Intune

Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pela Better Mobile, uma solução de Defesa de Ameaças Móveis (MTD) que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos a executar a aplicação Better Mobile.

Pode configurar políticas de acesso condicional com base na avaliação de risco melhor móvel ativada através de políticas de conformidade de dispositivos intune para dispositivos matriculados, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em detetados ameaças. Para dispositivos não matriculados, pode utilizar políticas de proteção de aplicações para impor um bloco ou limpeza seletiva com base em ameaças detetadas.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Como é que o Intune e o Better Mobile ajudam a proteger os recursos da empresa?

A aplicação Better Mobile está instalada e em execução nos dispositivos móveis. Esta aplicação captura o sistema de ficheiros, a pilha de rede e a telemetria de dispositivos e aplicações sempre que estiverem disponíveis e, em seguida, envia os dados para o serviço Better Mobile na cloud para avaliar o risco do dispositivo relativamente a ameaças móveis.

- **Suporte para dispositivos matriculados** - A política de conformidade do dispositivo Intune inclui uma regra para a Defesa de Ameaças Móveis (MTD), que pode utilizar informações de avaliação de risco da Better Mobile. Quando a regra MTD está ativada, intune avalia o cumprimento do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientações da aplicação Better Mobile instalada nos respetivos dispositivos para resolver o problema e recuperar o acesso a recursos empresariais. Para apoiar a utilização de Better Mobile com dispositivos matriculados:
  - [Adicione aplicativos MTD aos dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Criar uma política de conformidade de dispositivos que suporte o MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Ativar o conector MTD em Intune](../protect/mtd-connector-enable.md)

- **Suporte para dispositivos não matriculados** - Intune pode utilizar os dados de avaliação de risco da aplicação Better Mobile em dispositivos não matriculados quando utilizar as políticas de proteção de aplicações Intune. Os administradores podem usar esta combinação para ajudar a proteger os dados corporativos dentro de uma [aplicação protegida](../apps/apps-supported-intune-apps.md)microsoft Intune , os Administradores também podem emitir um bloco ou uma limpeza seletiva para dados corporativos nesses dispositivos não matriculados. Para apoiar a utilização de Better Mobile com dispositivos não matriculados:
  - [Adicione a aplicação MTD a dispositivos não matriculados](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Criar uma política de proteção de aplicações de defesa de ameaças móveis](../protect/mtd-app-protection-policy.md)
  - [Ativar o conector MTD em Intune para dispositivos não matriculados](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.1 e posterior**

- **iOS 8.0 e posterior**

## <a name="prerequisites"></a>Pré-requisitos

- Azure Active Directory Premium

- Subscrição do Microsoft Intune

- Subscrição do Better Mobile Threat Defense

  - Para obter mais informações, veja o [site do Better Mobile](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Cenários de exemplo

Seguem-se alguns cenários comuns.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode impedir os dispositivos de fazer as seguintes ações até a ameaça ser resolvida:

- Ligar ao e-mail empresarial

- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work

- Aceder às aplicações da empresa

Bloqueie quando forem detetadas aplicações maliciosas:

![Imagem que mostra aplicações maliciosas detetadas](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

O acesso é concedido na reparação:

![Acesso concedido a aplicações maliciosas detetadas](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças à rede, tal como ataques **Man-in-the-middle**, e proteja o acesso a redes Wi-Fi com base no risco do dispositivo.

Bloquear o acesso à rede através do Wi-Fi:

![Bloquear o acesso à rede através de Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

O acesso é concedido na reparação:

![Imagem que mostra acesso concedido na reparação](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques **Man-in-the-middle**, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

Block SharePoint Online quando são detetadas ameaças de rede:

![Bloquear o SharePoint Online quando forem detetadas ameaças à rede](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Acesso concedido na remediação:

![Exemplo de acesso concedido na remediação para o SharePoint](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controlar o acesso a dispositivos não matriculados com base em ameaças de aplicações maliciosas

Quando a solução BETTER Mobile Threat Defense considera um dispositivo infetado: ![blocos de política de proteção de aplicações devido a malware detetado](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

O acesso é concedido na reparação:

![Acesso à reparação da política de proteção de aplicações](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Próximos passos

- [Integrar o Better Mobile com o Intune](better-mobile-mtd-connector-integration.md)

- [Configurar aplicações do Better Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Criar a política de conformidade de dispositivos do Better Mobile](mtd-device-compliance-policy-create.md)

- [Ativar o conector Better Mobile MTD](mtd-connector-enable.md)

- [Criar uma política de proteção de aplicações MTD](mtd-app-protection-policy.md) 
