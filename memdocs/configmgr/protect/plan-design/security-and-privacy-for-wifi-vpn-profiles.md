---
title: Wi-Fi e VPN segurança e privacidade do perfil
titleSuffix: Configuration Manager
description: Conheça as recomendações de segurança para gerir perfis Wi-Fi e VPN para dispositivos em 'Gestor de Configuração'.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722068"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Segurança e privacidade para perfis Wi-Fi e VPN em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

## <a name="security-recommendations"></a>Recomendações de segurança

Utilize as seguintes práticas de segurança quando gere perfis Wi-Fi e VPN para dispositivos.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Escolha as opções mais seguras que a sua infraestrutura Wi-Fi e VPN e sistemas operativos de clientes podem suportar

Os perfis Wi-Fi e VPN fornecem um método conveniente para distribuir e gerir centralmente as definições de Wi-Fi e VPN que os seus dispositivos já suportam. O Gestor de Configuração não adiciona funcionalidade wi-fi ou VPN. Identifique, implemente e siga quaisquer recomendações de segurança para os seus dispositivos e infraestruturas.

## <a name="privacy-information"></a>Informações de privacidade

Pode utilizar perfis Wi-Fi e VPN para configurar dispositivos de cliente para se ligar aos servidores Wi-Fi e VPN. Em seguida, utilize o Gestor de Configuração para avaliar se esses dispositivos ficam conformes após a aplicação dos perfis. O ponto de gestão envia as informações de compatibilidade para o servidor do site e as informações são armazenadas na base de dados do site. A informação é encriptada quando os dispositivos a enviam para o ponto de gestão, mas não é armazenada em formato encriptado na base de dados do site. A base de dados conserva as informações até que sejam eliminadas pela tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** . O intervalo de eliminação predefinido é 90 dias, mas pode alterá-lo. As informações de conformidade não são enviadas para a Microsoft.

Por padrão, os dispositivos não avaliam os perfis de Wi-Fi e VPN. Além disso, deve configurar os perfis e, em seguida, implementá-los para os utilizadores.  

Antes de configurar perfis Wi-Fi ou VPN, considere os seus requisitos de privacidade.  
