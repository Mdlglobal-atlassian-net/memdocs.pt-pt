---
title: Conector de MTD Zimperium com o Intune
titleSuffix: Intune on Azure
description: Saiba como integrar o Intune com a solução de Defesa Contra Ameaças do Zimperium para controlar o acesso aos recursos empresariais a partir de dispositivos móveis.
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed623abeb602e599866af7b7249756edd87d5a29
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328437"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Conector Zimperium Mobile Threat Defense com o Intune

Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pela Zimperium, uma solução de Defesa de Ameaças Móveis (MTD) que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos a executar a aplicação Zimperium.

Pode configurar políticas de acesso condicional com base na avaliação de risco zimperium ativada através de políticas de conformidade de dispositivos inscritos no intune, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em dispositivos detetados ameaças. Para dispositivos não matriculados, pode utilizar políticas de proteção de aplicações para impor um bloco ou limpeza seletiva com base em ameaças detetadas.

## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.1 e posterior**

- **iOS 8 e posterior**

## <a name="prerequisites"></a>Pré-requisitos

- Azure Active Directory Premium

- Subscrição do Microsoft Intune

- Subscrição do Zimperium Mobile Threat Defense

  - Para mais informações, consulte [o site da Zimperium.](https://www.zimperium.com/zips-mobile-ips)

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Como é que o Intune e o Zimperium ajudam a proteger os recursos da empresa?

A aplicação Zimperium para Android e iOS/iPadOS captura sistema de ficheiros, stack de rede, dispositivo e telemetria de aplicações sempre que disponível, envia depois os dados de telemetria para o serviço de nuvem Zimperium para avaliar o risco do dispositivo para ameaças móveis.

- **Suporte para dispositivos matriculados** - A política de conformidade do dispositivo Intune inclui uma regra para a Defesa de Ameaças Móveis (MTD), que pode usar informações de avaliação de risco da Zimperium. Quando a regra MTD está ativada, intune avalia o cumprimento do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientações da aplicação Zimperium instalada nos respetivos dispositivos para resolver o problema e recuperar o acesso a recursos empresariais. Para apoiar a utilização do Zimperium com dispositivos matriculados:
  - [Adicione aplicativos MTD aos dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Criar uma política de conformidade de dispositivos que suporte o MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Ativar o conector MTD em Intune](../protect/mtd-connector-enable.md)

- **Suporte para dispositivos não matriculados** - Intune pode utilizar os dados de avaliação de risco da app Zimperium em dispositivos não matriculados quando utilizar as políticas de proteção de aplicações Intune. Os administradores podem usar esta combinação para ajudar a proteger os dados corporativos dentro de uma [aplicação protegida](../apps/apps-supported-intune-apps.md)microsoft Intune , os Administradores também podem emitir um bloco ou uma limpeza seletiva para dados corporativos nesses dispositivos não matriculados. Para apoiar a utilização do Zimperium com dispositivos não matriculados:
  - [Adicione a aplicação MTD a dispositivos não matriculados](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Criar uma política de proteção de aplicações de defesa de ameaças móveis](../protect/mtd-app-protection-policy.md)
  - [Ativar o conector MTD em Intune para dispositivos não matriculados](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Cenários de exemplo

Veja abaixo alguns cenários que ocorrem quando integra o Zimperium com o Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode bloquear os dispositivos até a ameaça ser resolvida:

- Ligar ao e-mail empresarial

- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work

- Aceder às aplicações da empresa

*Bloquear quando as aplicações maliciosas forem detetadas:*

> [!div class="mx-imgBorder"]
> ![imagem conceptual de apps maliciosas detetadas](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![imagem conceptual de acesso concedida após remediação](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças como **Man-in-the-middle** na rede e proteja o acesso às redes Wi-Fi com base no risco do dispositivo.

*Bloquear o acesso à rede através de Wi-Fi:*

> [!div class="mx-imgBorder"]
> acesso à rede ![Block através de](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png) Wi-Fi

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> acesso ![concedido no](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png) de reparação

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças na rede, tais como ataques **Man-in-the-middle**, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

*Bloquear o SharePoint Online quando forem detetadas ameaças à rede:*

> [!div class="mx-imgBorder"]
> ![Block SharePoint Online quando as ameaças de rede são detetadas](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![Acesso concedido em reparação por exemplo de](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controlar o acesso a dispositivos não matriculados com base em ameaças de aplicações maliciosas

Quando a solução de Defesa de Ameaças Móveis zimperium considera um dispositivo infetado:

> [!div class="mx-imgBorder"]
> ![blocos de políticas de proteção de apps devido a](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png) de malware detetados

O acesso é concedido na reparação:

> [!div class="mx-imgBorder"]
> ![Acesso é concedido na reparação de](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png) política de proteção de aplicações

## <a name="next-steps"></a>Próximos passos

- [Integrar o Zimperium com o Intune](zimperium-mtd-connector-integration.md)

- [Configurar aplicações do Zimperium](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Criar a política de conformidade de dispositivos do Zimperium](mtd-device-compliance-policy-create.md)

- [Ativar o conector Zimperium MTD](mtd-connector-enable.md)

- [Criar uma política de proteção de aplicações MTD](../protect/mtd-app-protection-policy.md)
