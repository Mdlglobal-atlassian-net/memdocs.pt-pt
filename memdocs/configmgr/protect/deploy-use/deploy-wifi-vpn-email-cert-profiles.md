---
title: Implementar perfis de acesso a recursos
titleSuffix: Configuration Manager
description: Saiba como implementar perfis de Wi-Fi, VPN e certificados no Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724518"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Implementar perfis de acesso a recursos no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de criar um dos seguintes perfis de acesso a recursos, desemposte-o para uma ou mais coleções:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certificado](create-certificate-profiles.md)

Ao implementar estes perfis, especifice a recolha do alvo e especifique com que frequência o cliente avalia o perfil para a conformidade.  

## <a name="deploy-a-profile"></a>Implementar um perfil

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Expandir **as Definições**de Conformidade, expandir o Acesso aos **Recursos da Empresa**e, em seguida, escolher o nó de perfil apropriado. Por exemplo, **Perfis Wi-Fi**.

1. Na lista de perfis, selecione o perfil que pretende implementar. Em seguida, no separador **Home** da fita, no grupo **de implantação,** selecione **Deploy**.  

1. Na janela de perfil de implantação, especifique as seguintes informações:  

    - **Recolha**: Selecione a coleção onde pretende implementar o perfil.

    - **Gerar um alerta**: Ative esta opção para configurar um alerta. O site gera este alerta se a conformidade do perfil for inferior à percentagem especificada pela data e hora especificadas. Também pode selecionar se pretende que seja enviado um alerta para o System Center Operations Manager.

    - **Atraso aleatório (horas)**: Para perfis de certificado que contenham definições do Protocolo de Inscrição de CertificadoS Simples (SCEP), especifique uma janela de atraso para evitar o processamento excessivo no Serviço de Inscrição de Dispositivos de Rede (NDES). O valor `64` padrão é de horas.  

    - **Especifique o calendário de avaliação de conformidade para este... perfil**: Especificar com que frequência o cliente avalia a conformidade com este perfil. Selecione um **simples horário** ou configure um **horário personalizado**. Por padrão, o horário `12` simples é a cada hora.

1. Selecione **OK** para fechar a janela e criar a implementação.

## <a name="delete-a-deployment"></a>Eliminar uma implantação

Se pretender eliminar uma implementação, selecione-a a partir da lista. No painel de detalhes, mude para o separador **De implantação.** Selecione a implementação e, em seguida, no **separador de implantação** da fita, selecione **Delete**.

> [!IMPORTANT]
> Ao remover uma implementação de perfil VPN, o Gestor de Configuração não remove o perfil VPN do Windows. Se pretender remover o perfil dos dispositivos, retire-o manualmente.

## <a name="next-steps"></a>Passos seguintes

[Monitorize perfis wi-fi e VPN](monitor-wifi-email-vpn-profiles.md)

[Monitorizar perfis de certificado](monitor-certificate-profiles.md)
