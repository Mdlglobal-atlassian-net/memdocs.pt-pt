---
title: Configure o cumprimento do dispositivo e da aplicação durante uma migração intune
titleSuffix: Microsoft Intune
description: Este artigo fornece os passos necessários para configurar as políticas de gestão de aplicações e de conformidade do dispositivo durante uma migração do Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0062d08e-e5b3-4f73-8b64-5ad95adbe945
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cefc43aa4c1e5031bc1b755a244df54f6442137
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079999"
---
# <a name="configure-device-compliance-and-app-management-policies-when-migrating-to-microsoft-intune"></a>Configurar políticas de gestão de aplicações e de conformidade do dispositivo durante uma migração para o Microsoft Intune

O objetivo principal durante a migração para o Intune é ter todos os dispositivos inscritos no Intune e em conformidade com as políticas. As políticas de dispositivo não só o ajudam a gerir dispositivos de utilizador único pertencentes à empresa, como também dispositivos pessoais (BYOD) e partilhados, tais como quiosques, máquinas de pontos de venda, tablets partilhados por múltiplos estudantes numa sala de aula ou dispositivos sem utilizador (apenas iOS).

Cada plataforma do dispositivo poderá oferecer definições diferentes, mas as políticas de dispositivos do Intune trabalham com cada plataforma do dispositivo ao proporcionar as seguintes capacidades de gestão de dispositivos móveis:

- Regular o número de dispositivos que cada utilizador inscreve.

- Gerir as definições dos dispositivos (por exemplo, a encriptação ao nível do dispositivo, o comprimento da palavra-passe, a utilização da câmara).

- Disponibilizar aplicações, perfis de e-mail, perfis da VPN, etc.

- Avaliar os critérios ao nível do dispositivo das políticas de conformidade de segurança.

> [!IMPORTANT]
> As políticas de gestão de dispositivos não são atribuídas diretamente aos dispositivos ou utilizadores individuais, mas, em vez disso, são atribuídas a grupos de utilizadores. As políticas podem ser aplicadas diretamente a um grupo de utilizadores (e, portanto, também ao dispositivo do utilizador) ou podem ser aplicadas a um grupo de dispositivos (e, portanto, também aos membros do grupo).

## <a name="task-list-for-device-compliance-policies"></a>Lista de tarefas das políticas de conformidade de dispositivo

### <a name="task-1-add-device-groups-optional"></a>Tarefa 1: Adicionar grupos de dispositivos (opcional)

Pode criar grupos de dispositivos quando tiver de realizar tarefas administrativas com base na identidade do dispositivo em vez da identidade do utilizador.

Os grupos de dispositivos são úteis para a gestão de dispositivos que não têm utilizadores dedicados, tais como dispositivos de local público, dispositivos partilhados por trabalhadores de turnos ou dispositivos atribuídos a uma localização específica.

Ao configurar grupos de dispositivos antes da inscrição de dispositivos, pode utilizar as categorias de dispositivos para os associar automaticamente a grupos após a inscrição. Em seguida, receberão automaticamente as políticas de dispositivos do seu grupo. [Começar com grupos.](groups-get-started.md)

### <a name="task-2-use-resource-access-profiles-wi-fi-vpn-and-email-certificates"></a>Tarefa 2: Utilizar perfis de acesso a recursos (certificados de e-mail, Wi-Fi e VPN)

Certificados de fornecimento dos perfis de acesso a recursos e configurações de acesso a dispositivos inscritos. Se estiver a utilizar a autenticação baseada em certificados, [configure os certificados](../protect/certificates-configure.md).

### <a name="task-3-create-and-deploy-device-configuration-profiles"></a>Tarefa 3: Criar e implementar perfis de configuração de dispositivos

Tem de criar um perfil de configuração de dispositivos para impor definições ao nível do dispositivo, por exemplo: desativar a câmara, a loja de aplicações, configurar o modo de aplicação única, o ecrã principal, etc. Saiba mais sobre os [perfis de dispositivo](../configuration/device-profiles.md).

#### <a name="directly-import-iosipados-configuration-profiles-optional"></a>Importar diretamente perfis de configuração iOS/iPadOS (opcional)

- **Perfis apple configurator iOS (iOS 7.1 e posterior):** Se a sua solução MDM existente utilizar perfis Apple Configurator (.ficheiros mobileconfig), intune pode importá-los diretamente como políticas de configuração personalizadas.

- Políticas de configuração de **aplicações móveis iOS:** Se a sua solução MDM existente utilizar as políticas de configuração de aplicações móveis iOS/iPadOS, a Intune pode importá-las diretamente desde que cumpram o formato XML especificado pela Apple para listas de propriedades.

- Saiba como adicionar uma política personalizada para [iOS](../configuration/custom-settings-ios.md).

### <a name="task-4-create-and-deploy-device-compliance-policies-optional"></a>Tarefa 4: Criar e implementar políticas de conformidade do dispositivo (opcional)

As políticas de conformidade do dispositivo avaliam as definições dedicadas à segurança e disponibilizam relatórios que mostram se os dispositivos estão ou não em conformidade com os padrões empresariais. Tais definições incluem:

- Comprimento do PIN

- Estado Jailbreak

- Versão do SO

Veja recursos adicionais para as definições de conformidade do dispositivo:

- Saiba mais sobre as [políticas de conformidade do dispositivo](../protect/device-compliance-get-started.md).

### <a name="task-5-publish-and-deploy-apps"></a>Tarefa 5: Publicar e implementar aplicações

Ao utilizar o Intune MDM, pode fornecer aplicações ao exigir a sua instalação automática ou ao disponibilizá-las no Portal da Empresa.

- [Como adicionar aplicações](../apps/apps-add.md).

- [Como implementar aplicações.](../apps/apps-deploy.md)

### <a name="task-6-enable-device-enrollment"></a>Tarefa 6: Ativar a inscrição de dispositivos

A inscrição de dispositivos é necessária para gerir o dispositivo. Saiba [como se preparar para inscrever dispositivos pessoais do utilizador pertencentes à empresa](../enrollment/device-enrollment.md).

## <a name="next-steps"></a>Passos seguintes

Configure as políticas de proteção de [aplicações (opcional)](../apps/app-protection-policies.md).
