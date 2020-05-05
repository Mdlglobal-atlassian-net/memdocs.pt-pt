---
title: Proteger os dados e a infraestrutura do site
titleSuffix: Configuration Manager
description: Aprenda a proteger os recursos da sua organização contra exposição ou ataque malicioso com o Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723916"
---
# <a name="protect-data-and-site-infrastructure"></a>Proteger os dados e a infraestrutura do site

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pretende que os seus utilizadores acedam de forma segura aos recursos da sua organização. Proteja tanto a sua infraestrutura como os seus dados contra exposição ou ataque malicioso. Utilize o Gestor de Configuração para permitir o acesso e ajudar a proteger os recursos da sua organização.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) permite-lhe gerir as seguintes políticas do Microsoft Defender para computadores clientes:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Proteção Avançada Contra Ameaças do Microsoft Defender
  - Microsoft Defender Exploit Guard
  - Guarda de aplicações do Microsoft Defender
  - Controlo de aplicações do Microsoft Defender

  > [!TIP]
  > Para gerir a proteção de pontos finais em dispositivos windows 10 cogeridos utilizando o serviço de cloud Microsoft Endpoint Manager, altere a carga de trabalho de [ **Proteção de Ponto** ](../../comanage/workloads.md#endpoint-protection) final para Intune. Para mais informações, consulte a [proteção Endpoint para o Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Proteja os dados armazenados no local Clientes windows com encriptação BitLocker Drive (BDE). O Gestor de Configuração fornece uma gestão completa do ciclo de vida BitLocker que pode substituir a utilização da Microsoft BitLocker Administration and Monitoring (MBAM). Para mais informações, consulte [Plan for BitLocker management](../plan-design/bitlocker-management.md).

- Em vez de senhas tradicionais, ative métodos alternativos de entrada em dispositivos Windows 10 utilizando o Windows Hello for Business. Para mais informações, consulte [as definições do Windows Hello for Business](../deploy-use/windows-hello-for-business-settings.md).

- Minimize os esforços dos seus utilizadores para se conectar em recursos, permitindo a conectividade VPN utilizando perfis VPN. Para mais informações, consulte [perfis VPN](../deploy-use/vpn-profiles.md).  

- Os perfis Wi-Fi fornecem um conjunto de ferramentas e recursos para ajudá-lo a gerir as definições de rede sem fios em dispositivos da sua organização. Ao implementar estas definições, minimiza o esforço que os utilizadores finais necessitam para se ligarem a redes sem fios. Para mais informações, consulte [perfis Wi-fi](../deploy-use/create-wifi-profiles.md).  

- Dispositivos de fornecimento com os certificados que os utilizadores precisam de ligar aos recursos. Para mais informações, consulte [os perfis do Certificado](../deploy-use/introduction-to-certificate-profiles.md).  
