---
title: Conector do Lookout MTD com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Saiba mais sobre como integrar o Intune com o Lookout Mobile Threat Defense (Defesa Contra Ameaças para Dispositivos Móveis) para controlar o acesso de dispositivos móveis aos seus recursos empresariais.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17b120faa0021a1fc044d7831b4b81ea88f404a7
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79526585"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Conector de segurança de ponto de ponta móvel lookout com Intune

Pode controlar o acesso dos dispositivos móveis a recursos da empresa, com base na avaliação de riscos realizada pelo Lookout, uma solução de Defesa Contra Ameaças para Dispositivos Móveis integrada no Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos através do serviço Lookout, incluindo:
- Vulnerabilidades do sistema operativo
- Aplicações maliciosas instaladas
- Perfis de rede maliciosos

Pode configurar políticas de Acesso Condicional com base na avaliação de risco da Lookout, ativada através de políticas de conformidade intune para dispositivos matriculados, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em ameaças detetadas. Para dispositivos não matriculados, pode utilizar políticas de proteção de aplicações para impor um bloco ou limpeza seletiva com base em ameaças detetadas.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Como é que a Intune e a Lookout Mobile Endpoint Security ajudam a proteger os recursos da empresa?

A aplicação móvel da Lookout, **Lookout for work,** está instalada e executada em dispositivos móveis. Esta aplicação captura o sistema de ficheiros, a pilha de rede e a telemetria de dispositivos e aplicações sempre que estiverem disponíveis e, em seguida, envia-os para o serviço Lookout na cloud para avaliar o risco do dispositivo relativamente a ameaças móveis. Pode alterar as classificações dos níveis de risco das ameaças na consola do Lookout para atender às suas necessidades.

- **Suporte para dispositivos matriculados** - A política de conformidade do dispositivo Intune inclui uma regra para a Defesa de Ameaças Móveis (MTD), que pode utilizar informações de avaliação de risco do Lookout para o trabalho. Quando a regra MTD está ativada, intune avalia o cumprimento do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientação da app Detrabalho para trabalho instalada nos seus dispositivos para resolver o problema e recuperar o acesso aos recursos corporativos. Para apoiar a utilização do Lookout para o trabalho com dispositivos matriculados:
  - [Adicione aplicativos MTD aos dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Criar uma política de conformidade de dispositivos que suporte o MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Ativar o conector de MTD no Intune](../protect/mtd-connector-enable.md)

- **Suporte para dispositivos não matriculados** - Intune pode utilizar os dados de avaliação de risco da aplicação Lookout para trabalho em dispositivos não matriculados quando utilizar as políticas de proteção de aplicações Intune. Os administradores podem usar esta combinação para ajudar a proteger os dados corporativos dentro de uma [aplicação protegida](../apps/apps-supported-intune-apps.md)microsoft Intune , os Administradores também podem emitir um bloco ou uma limpeza seletiva para dados corporativos nesses dispositivos não matriculados. Para apoiar a utilização do Lookout para o trabalho com dispositivos não matriculados:
  - [Adicione a aplicação MTD a dispositivos não matriculados](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Criar uma política de proteção de aplicações de defesa de ameaças móveis](../protect/mtd-app-protection-policy.md)
  - [Ativar o conector MTD em Intune para dispositivos não matriculados](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Plataformas suportadas

O Lookout suporta as seguintes plataformas, quando inscritas no Intune:

- **Android 4.1 e posterior**  
- **iOS 8 e posterior**  

Para obter informações adicionais sobre plataforma e suporte linguístico, visite o [site do Lookout.](https://personal.support.lookout.com/hc/articles/114094140253)  

## <a name="prerequisites"></a>Pré-requisitos

- Subscrição empresarial do Lookout Mobile Endpoint Security  
- Subscrição do Microsoft Intune
- Azure Active Directory Premium
- Mobilidade e Segurança Empresarial (EMS) E3 ou E5, com licenças atribuídas aos utilizadores.  

Para mais informações, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>Cenários de exemplo

Aqui estão os cenários comuns ao usar mobile endpoint security com Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode impedir os dispositivos de fazer o seguinte até a ameaça ser resolvida:

- Ligar ao e-mail empresarial
- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work
- Aceder às aplicações da empresa

*Bloquear quando as aplicações maliciosas forem detetadas:*

> [!div class="mx-imgBorder"]
> ![Imagem conceptual da política que bloqueia o acesso devido a aplicações maliciosas](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![Imagem conceptual mostrando acesso a dispositivos após reparação](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças à rede, tal como ataques man-in-the-middle, e proteja o acesso a redes Wi-Fi com base no risco do dispositivo.

*Bloquear o acesso à rede através de Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Imagem mostrando o bloqueio do acesso Wi-Fi com base em ameaças de rede](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![Imagem conceptual do Acesso Condicional que permite o acesso após remediação](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques Man-in-the-middle e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

*Block SharePoint Online quando são detetadas ameaças de rede:*

> [!div class="mx-imgBorder"]
> ![Imagem conceptual de bloquear o acesso ao SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![Imagem conceptual de permitir o acesso após a ameaça da rede é remediada](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controlar o acesso a dispositivos não matriculados com base em ameaças de aplicações maliciosas

Quando a solução de Defesa de Ameaças Móveis Lookout considera um dispositivo infetado:
> [!div class="mx-imgBorder"]
> ![Blocos de política de proteção de aplicações devido a malware detetado](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

O acesso é concedido na reparação:

> [!div class="mx-imgBorder"]
> ![Acesso à reparação da política de proteção de aplicações](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Passos seguintes

Seguem-se os principais passos que tem de efetuar para implementar esta solução:

- [Configurar a sua integração do Lookout](lookout-mtd-connector-integration.md)
- [Ativar a segurança do ponto final móvel em Intune](mtd-connector-enable.md)
- [Adicionar e voltar a assinar aplicação Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurar a política de conformidade do dispositivo do Lookout](mtd-device-compliance-policy-create.md)
- [Criar uma política de proteção de aplicações MTD](mtd-app-protection-policy.md)
