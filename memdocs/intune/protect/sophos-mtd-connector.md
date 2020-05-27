---
title: Use Sophos Mobile com Intune
titleSuffix: Intune on Azure
description: Como utilizar a solução Sophos Mobile com a Microsoft Intune para controlar o acesso de dispositivos móveis aos seus recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: be5cf3d0ba83fe1027dcec9dcde50257e30b7c47
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988208"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Conector de Defesa de Ameaças Móveis Sophos com Intune
Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando acesso condicionado com base na avaliação de risco realizada pela Sophos Mobile, uma solução de Defesa de Ameaças Móveis (MTD) que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida a partir de dispositivos que executam a aplicação Sophos Mobile.
Pode configurar políticas de acesso condicional com base na avaliação de risco móvel Sophos ativada através de políticas de conformidade de dispositivos Intune, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em ameaças detetadas.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="supported-platforms"></a>Plataformas suportadas

- Android 5.0 e mais tarde
- iOS 11.0 e posterior

## <a name="prerequisites"></a>Pré-requisitos

- Azure Active Directory Premium
- Subscrição do Microsoft Intune
- Assinatura de Sophos Mobile Threat Defense

Para mais informações, consulte o site da [Sophos.](https://www.sophos.com/products/mobile-control.aspx)

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>Como é que a Intune e a Sophos Mobile ajudam a proteger os recursos da sua empresa?

A aplicação Sophos Mobile para Android e iOS/iPadOS captura sistema de ficheiros, pilha de rede, dispositivo e telemetria de aplicações sempre que disponível, e depois envia os dados de telemetria para o serviço de nuvem Sophos Mobile para avaliar o risco do dispositivo para ameaças móveis.

A política de conformidade do dispositivo Intune inclui uma regra para a Sophos Mobile Threat Defense, que se baseia na avaliação de risco móvel sophos. Quando esta regra está ativada, o Intune avalia a conformidade do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientação da aplicação Sophos Mobile instalada nos seus dispositivos para resolver o problema e recuperar o acesso aos recursos corporativos.  

## <a name="sample-scenarios"></a>Cenários de exemplo

Seguem-se alguns cenários comuns.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode impedir os dispositivos de fazer as seguintes ações até a ameaça ser resolvida:

- Ligar ao e-mail empresarial
- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work
- Aceder às aplicações da empresa

*Bloqueie quando forem detetadas aplicações maliciosas:*

![Imagem conceptual de aplicações maliciosas detetada](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Acesso concedido à reparação:*  
![Imagem conceptual de acesso concedida após remediação](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças à rede, tal como ataques Man-in-the-middle, e proteja o acesso a redes Wi-Fi com base no risco do dispositivo.  

*Bloquear o acesso à rede através do Wi-Fi:*  
![Bloquear o acesso à rede através do Wi-Fi](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Acesso concedido à reparação:*   
![Acesso concedido na reparação](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques Man-in-the-middle, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.  

*Block SharePoint Online quando as ameaças de rede são detetadas:*

![Bloquear o SharePoint Online quando forem detetadas ameaças à rede](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Acesso concedido à reparação:*

![Exemplo de acesso concedido na remediação para o SharePoint](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passos seguintes

- [Integrar Sofos com Intune](sophos-mtd-connector-integration.md)
- [Configurar aplicativos Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Criar a política de conformidade do dispositivo Sophos](mtd-device-compliance-policy-create.md)
- [Ativar o conector Sophos MTD](mtd-connector-enable.md)
