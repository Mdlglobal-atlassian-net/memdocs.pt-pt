---
title: Coexistência de MDM de terceiros
titleSuffix: Configuration Manager
description: Saiba mais sobre a utilização de um serviço de MDM de terceiros com o Gestor de Configuração
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710826"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Coexistência de MDM de terceiros com Gestor de Configuração

Quando gere simultaneamente dispositivos Do Windows 10 com o Gestor de Configuração e o Microsoft Intune, esta funcionalidade [chama-se co-management](overview.md). Quando gere dispositivos com 'Gestor de Configuração' e se inscreve num serviço DEMDM de terceiros, esta funcionalidade chama-se *coexistência*. Ter duas autoridades de gestão para um único dispositivo pode ser um desafio se não devidamente orquestrado entre os dois. Com cogestão, Configuração Manager e Intune equilibram as [cargas de trabalho](workloads.md) para garantir que não há conflitos. Esta interação não existe com serviços de terceiros, pelo que existem limitações com as capacidades de gestão da coexistência.

O cliente do Gestor de Configuração pode coexistir com um serviço DE MDM de terceiros num dispositivo que executa a versão 1709 do Windows 10 ou mais tarde, e que se juntou ao Diretório Ativo azure. O dispositivo pode ser um dos seguintes tipos:

- [Azure AD só se juntou.](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) (Este tipo é por vezes referido como "cloud domínio-joined")  

- [Híbrido-filiado ao domínio,](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)onde o dispositivo está unido ao seu Diretório Ativo no local e registado com o seu Diretório Ativo Azure.  

> [!Note]  
> Não suporta [dispositivos pessoais.](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device)  

Quando o cliente do Gestor de Configuração deteta que um serviço DEMDM de terceiros também está a gerir o dispositivo, desativa automaticamente determinadas cargas de trabalho no Gestor de Configuração. Este comportamento permite que o serviço DEMD assuma estas funções. Também evita configurações contraditórias no cliente que possam afetar negativamente o dispositivo e a experiência do utilizador. As seguintes cargas de trabalho no Gestor de Configuração são desativadas neste caso:

- Políticas de acesso a recursos para definições de VPN, Wi-Fi, e-mail e certificado
- Gestão de aplicações, incluindo pacotes legados
- Digitalização e instalação de atualização de software
- Proteção endpoint, o conjunto Windows Defender de funcionalidades de proteção antimalware
- Política de conformidade para acesso condicional
- Configuração do dispositivo
- Gestão click-to-run do office

O cliente do Gestor de Configuração evita o conflito com a autoridade de gestão de terceiros, prosseguindo as seguintes operações de leitura:

- Inventário de hardware e software
- Asset Intelligence
- Medição de software
- Relatórios de gestão de energia

Para obter mais informações sobre os benefícios da cogestão com o Gestor de Configuração e insina, consulte [os benefícios de cogestão.](overview.md#benefits)
