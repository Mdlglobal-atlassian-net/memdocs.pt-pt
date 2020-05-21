---
title: Gerir as definições de firewall com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com a política de firewall de segurança de endpoint no Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f98d7a30d219aee63e38a63a74d8f1713deb198a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431295"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Política de firewall para segurança de ponto final em Intune

Utilize a política de firewall de segurança de ponto final em Intune para configurar uma firewall incorporada para dispositivos que executam macOS e Windows 10. As firewalls incorporadas incluem o BitLocker para dispositivos Windows e FileVault para macOS.

Embora possa configurar as mesmas definições de firewall utilizando perfis de proteção de ponto final para a configuração do dispositivo, os perfis de configuração do dispositivo incluem categorias adicionais de definições. Estas definições adicionais não estão relacionadas com firewalls e podem complicar a tarefa de configurar apenas as definições de firewall para o seu ambiente.

Encontre as políticas de segurança de ponto final para firewalls sob *o "Manage* in the **Endpoint security** node de segurança do centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)".

Ver [definições para perfis de Firewall](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Pré-requisitos para perfis de Firewall

- Windows 10 ou mais tarde
- Qualquer versão suportada do macOS

## <a name="firewall-profiles"></a>Perfis de firewall

**perfis macOS:**

- **firewall macOS** – Ative e configure as definições para a firewall incorporada no macOS.

**Perfis do Windows 10:**

- **Microsoft Defense Firewall** – Configurar as definições para firewall do Windows Defense com Segurança Avançada. O Windows Defender Firewall fornece filtragem de tráfego de rede de duas vias baseada no hospedeiro para um dispositivo e pode bloquear o tráfego de rede não autorizado que flui para dentro ou para fora do dispositivo local.

- **Regras** do Microsoft Defender Firewall *(Pré-visualização)* - Defina as regras de firewall granular, incluindo portas específicas, protocolos, aplicações e redes, e permitir ou bloquear o tráfego da rede. Cada instância deste perfil suporta até 150 regras personalizadas.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Fusões de regras de firewall e conflitos políticos

Plano para as políticas de Firewall a aplicar a um dispositivo usando apenas uma política. A utilização de um único exemplo de política e do tipo de política ajuda a evitar que duas políticas separadas apliquem configurações diferentes na mesma configuração, o que cria conflitos. Quando existe um conflito entre dois casos políticos ou tipos de política que gerem a mesma configuração com valores diferentes, a definição não é enviada para o dispositivo.

- Esta forma de conflito de políticas aplica-se ao perfil **do Microsoft Defender Firewall,** que pode entrar em conflito com outros perfis do Microsoft Defender Firewall, ou uma configuração de firewall que é entregue por um tipo de política diferente, como a configuração do dispositivo.

  Os perfis do Microsoft *Defender Firewall* não entram em conflito com os perfis das regras do Microsoft Defender *Firewall.*

Quando utiliza perfis de **regras do Microsoft Defender Firewall,** pode aplicar vários perfis de regras no mesmo dispositivo. No entanto, quando existem regras diferentes para a mesma coisa com configurações diferentes, ambas são enviadas para o dispositivo e criam um conflito, nesse dispositivo.

- Por exemplo, se uma regra bloquear *teams.exe* através da firewall e uma segunda regra permitir *Teams.exe*, ambas as regras são entregues ao cliente. Este resultado é diferente dos conflitos criados através de outras políticas para configurações de Firewall.

Quando as regras de perfis de várias regras não entram em conflito entre si, os dispositivos fundem as regras de cada perfil para criar uma configuração combinada de regras de firewall no dispositivo. Este comportamento permite-lhe implementar mais do que as 150 regras que cada perfil individual suporta num dispositivo.

- Por exemplo, tem dois perfis de regras do Microsoft Defender Firewall. O primeiro perfil permite que *as Equipas.exe* através da firewall. O segundo perfil permite o *Outlook.exe* através da firewall. Quando um dispositivo recebe ambos os perfis, o dispositivo é configurado para permitir ambas as aplicações através da firewall.

## <a name="next-steps"></a>Próximos passos

[Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
