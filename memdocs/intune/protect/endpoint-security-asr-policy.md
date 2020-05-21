---
title: Gerir as definições de redução de superfície de ataque com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com definições de política de redução de superfície de ataque de segurança final no Microsoft Intune
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
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431243"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Política de redução de superfície de ataque para segurança de ponto final em Intune

Quando o antivírus Defender estiver a ser utilizado nos seus dispositivos Windows 10, pode utilizar políticas de segurança de ponto final Intune para a redução da superfície de Ataque para gerir essas definições para os seus dispositivos.

As políticas de redução da superfície de ataque ajudam a reduzir as suas superfícies de ataque, minimizando os locais onde a sua organização é vulnerável a ameaças cibernéticas e ataques. Para mais informações, consulte a [visão geral da redução da superfície de ataque]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) na documentação de proteção contra ameaças do Windows.

Encontre as políticas de segurança de ponto final para a redução da superfície de ataque sob *o "Manage* in the **Endpoint security** node" do centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Cada *perfil* de redução de superfície de ataque gere as definições para uma área específica de um dispositivo Windows 10.

Ver [definições para perfis](../protect/endpoint-security-asr-profile-settings.md)de redução de superfície de ataque .

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Pré-requisitos para perfis de redução de superfície de ataque

- Windows 10 ou mais tarde
- O antivírus defensor deve ser o antivírus primário no dispositivo

## <a name="attack-surface-reduction-profiles"></a>Perfis de redução da superfície de ataque

**Perfis do Windows 10:**

- **App e isolamento de navegador** – Gerencie as definições para o Windows Defender Application Guard (Application Guard), como parte do Defender ATP. Application Guard ajuda a prevenir ataques antigos e recém-emergentes e pode isolar sites definidos pela empresa como não confiáveis, ao mesmo tempo que define quais sites, recursos em nuvem e redes internas são confiáveis.

  Para saber mais, consulte application [Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) na documentação ATP do Microsoft Defender.

- **Proteção web** – Configurações que pode gerir para a proteção web na proteção atp do Microsoft Defender configuram a proteção da rede para proteger as suas máquinas contra ameaças web. Ao integrar-se com o Microsoft Edge e navegadores de terceiros populares como o Chrome e firefox, a proteção web para as ameaças web sem um proxy web e pode proteger as máquinas enquanto estão fora ou no local. A proteção web impede o acesso a:
  - Sites de phishing
  - Vetores de malware
  - Explorar sites
  - Sites de reputação não confiáveis ou de baixa reputação
  - Sites que bloqueou na sua lista de indicadores personalizados.

  Para saber mais, consulte a [proteção web](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) na documentação ATP do Microsoft Defender.

- **Controlo de aplicações** - As definições de controlo de aplicações podem ajudar a mitigar ameaças de segurança, restringindo as aplicações que os utilizadores podem executar e o código que funciona no Núcleo do Sistema (kernel). Gerencie as definições que podem bloquear scripts e MSIs não assinados e restringir o Windows PowerShell a ser executado no Modo Idioma Constrangido.

  Para saber mais, consulte o Controlo de [Aplicações](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) na documentação ATP do Microsoft Defender.

- Regras de **redução de superfície** de ataque – Configure as definições para regras de redução de superfície de ataque que visam comportamentos que malware e aplicações maliciosas normalmente usam para infetar computadores, incluindo:
  - Ficheiros e scripts executáveis utilizados em aplicações do Office ou correio web que tentam descarregar ou executar ficheiros
  - Scripts obfuscados ou de outra forma suspeitos
  - Comportamentos que as aplicações normalmente não começam durante o trabalho normal do dia-a-dia Reduzir a superfície do ataque significa oferecer aos atacantes menos formas de realizar ataques.

  Para saber mais, consulte as regras de [redução](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) de superfície do Ataque na documentação ATP do Microsoft Defender.

- **Controlo do dispositivo** – Com as definições para o controlo do dispositivo, pode configurar os dispositivos para uma abordagem em camadas para fixar meios amovíveis. O Microsoft Defender ATP fornece múltiplas funcionalidades de monitorização e controlo para ajudar a evitar que ameaças em periféricos não autorizados comprometam os seus dispositivos.

  Para saber mais, consulte [como controlar dispositivos USB e outros meios amovíveis utilizando](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) o Microsoft Defender ATP na documentação ATP do Microsoft Defender.

- **Explore a proteção** - Explorar as definições de proteção pode ajudar a proteger contra malwares que utilizam explorações para infetar dispositivos e espalhar. A proteção de exploração consiste numa série de mitigações que podem ser aplicadas tanto ao sistema operativo como às aplicações individuais.

  Para saber mais, consulte [A proteção de explorar ativar](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) na documentação ATP do Microsoft Defender.

## <a name="next-steps"></a>Próximos passos

[Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
