---
title: Configure políticas de proteção de aplicações durante a migração
titleSuffix: Microsoft Intune
description: Este artigo fornece os passos necessários para configurar as políticas de proteção de aplicações durante uma migração do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 93cda587-bf56-4d41-b123-9fe203fad788
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: d033c83865c19638ab9b1d34b9b77ae146d28133
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331301"
---
# <a name="configure-app-protection-policies-optional"></a>Configurar políticas de proteção de aplicações (opcional)


As políticas de proteção de aplicações permitem-lhe:
* Encriptar aplicações
* Definir um PIN quando a aplicação for acedida
* Impedir que as aplicações sejam executadas em dispositivos desbloqueados por jailbreak ou por rooting e muitas outras proteções.

Se o telemóvel do utilizador for perdido ou roubado, pode apagar remotamente os dados empresariais de forma seletiva e manter os dados pessoais intactos.

As políticas de proteção de aplicações aplicam a segurança ao nível da aplicação e não precisam da inscrição de dispositivos. Pode utilizá-las com dispositivos que estejam ou não inscritos no Intune. Além disso, pode aplicar estas políticas a dispositivos inscritos num fornecedor de MDM de terceiros.

## <a name="app-protection-policies-with-lob-apps"></a>Políticas de proteção de aplicações com aplicações LOB

Também pode alargar as políticas de proteção de aplicações móveis às suas aplicações de linha de negócio (LOB), utilizando o [Microsoft Intune App SDK](../developer/app-sdk-get-started.md) ou a Ferramenta de Embrulho de Aplicações Intune microsoft para as plataformas iOS/iPadOS e Android. Para obter mais informações, veja [Ferramenta de Encapsulamento de Aplicações para iOS](../developer/app-wrapper-prepare-ios.md) e [Ferramenta de Encapsulamento de Aplicações para Android](./../developer/app-wrapper-prepare-android.md). Além disso, veja [Preparar aplicações LOB para a proteção de aplicações](../developer/apps-prepare-mobile-application-management.md).

## <a name="how-do-app-protection-policies-help-during-migration"></a>Como é que as políticas de proteção de aplicações ajudam durante a migração?

Numa migração, tem de remover dispositivos do fornecedor de MDM antigo e inscrevê-los no Intune. Deve planear esta situação e incentivar os utilizadores finais a deixarem o fornecedor de MDM antigo e a inscreverem-se imediatamente no Intune. No entanto, durante a migração podem existir utilizadores que atrasam a conclusão do processo de inscrição e cujos dispositivos não são geridos por qualquer fornecedor de MDM.

Este período pode deixar a sua organização mais vulnerável a roubos de dispositivos e perda de dados empresariais caso o acesso a recursos empresariais ainda seja permitido. Também poderá levar à redução de produtividade do utilizador caso o acesso a recursos empresariais esteja impedido.

Intune pode oferecer proteções de dados corporativos durante a migração para que você ainda possa ter cobertura de segurança para os seus dados corporativos quando não há gestão ao nível do dispositivo.

Uma vez que desativa o Acesso Condicional no antigo fornecedor de MDM, os utilizadores ainda podem ser produtivos enquanto você a bordo para Intune.

## <a name="task-list-for-app-protection-policies"></a>Lista de tarefas das políticas de proteção de aplicações

- [Como criar e atribuir políticas de proteção de aplicações](../apps/app-protection-policies.md)

## <a name="next-steps"></a>Passos seguintes

[Considerações especiais sobre a migração](migration-guide-considerations.md)
