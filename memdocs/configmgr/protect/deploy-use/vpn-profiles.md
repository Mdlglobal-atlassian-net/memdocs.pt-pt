---
title: Perfis VPN
titleSuffix: Configuration Manager
description: Saiba como utilizar perfis VPN no Gestor de Configuração para implementar definições vpn para utilizadores na sua organização.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722257"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Perfis VPN no Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1283610-->
Para implementar as definições vpN para os utilizadores da sua organização, utilize perfis VPN no Gestor de Configuração. Ao implementar estas definições, estará a minimizar o esforço do utilizador final para se ligar aos recursos na rede da empresa.  

Por exemplo, pretende configurar todos os dispositivos do Windows 10 com as definições necessárias para se ligar a uma partilha de ficheiros na rede interna. Crie um perfil VPN com as definições necessárias para ligar à rede interna. Em seguida, implemente este perfil para todos os utilizadores que tenham dispositivos que executem o Windows 10. Estes utilizadores vêem a ligação VPN na lista de redes disponíveis e podem conectar-se com pouco esforço.

Ao criar um perfil VPN, pode incluir uma vasta gama de definições de segurança. Estas definições incluem certificados para validação do servidor e autenticação do cliente que você disponibiliza com perfis de certificado de Gestor de Configuração. Para mais informações, consulte [os perfis do Certificado](introduction-to-certificate-profiles.md).

> [!Note]
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Plataformas suportadas

A tabela seguinte descreve os perfis VPN que pode configurar para várias plataformas de dispositivos.

|Tipo de ligação|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Sim|Não|Sim|Sim|
|**F5 Edge Client**|Sim|Não|Sim|Sim|
|**Dell SonicWALL Mobile Connect**|Sim|Não|Sim|Sim|
|**VPN Móvel do Ponto de Verificação**|Sim|Não|Sim|Sim|
|**Microsoft SSL (SSTP)**|Sim|Sim|Sim|Não|
|**Microsoft Automatic**|Sim|Sim|Sim|Não|
|**IKEv2**|Sim|Sim|Sim|Não|
|**PPTP**|Sim|Sim|Sim|Não|
|**L2TP**|Sim|Sim|Sim|Não|

## <a name="next-step"></a>Passo seguinte

> [!div class="nextstepaction"]
> [Como criar perfis VPN](create-vpn-profiles.md)

## <a name="see-also"></a>Consulte também

- [Pré-requisitos para perfis VPN](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Segurança e privacidade para perfis VPN](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
