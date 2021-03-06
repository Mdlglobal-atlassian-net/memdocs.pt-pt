---
title: Opções de inscrição para dispositivos geridos pelo Microsoft Intune
titleSuffix: ''
description: Uma lista de opções de inscrição que os administradores podem definir para dispositivos geridos pelo Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/31/2017
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cf4ad6d4-423f-4826-ab8d-6eb7a7cfb559
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11dba32ea6b8cc9e7851ebb789776d1121e1d7ce
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990534"
---
# <a name="enrollment-options-for-devices-managed-by-intune"></a>Opções de inscrição para dispositivos geridos pelo Intune

Enquanto administrador do Intune, pode configurar a inscrição de dispositivos para ajudar os utilizadores e ativar as funcionalidades do Intune.  O Intune inclui as seguintes opções de inscrição:

## <a name="terms-and-conditions"></a>Termos e condições

Pode exigir que os utilizadores aceitem os termos e condições da sua empresa antes de poderem utilizar o Portal da Empresa para inscrever os dispositivos e aceder a recursos como aplicações e e-mail da empresa. A configuração dos termos e condições é opcional. Saiba mais sobre os [termos e condições](terms-and-conditions-create.md).

## <a name="enrollment-restrictions"></a>Restrições de inscrição

Pode optar por restringir a inscrição de dispositivos por:
- Plataforma de dispositivo
- Número de dispositivos por utilizador
- Bloqueio de dispositivos pessoais

Saiba mais sobre as [restrições de inscrição](enrollment-restrictions-set.md).

## <a name="enable-apple-device-enrollment"></a>Ativar a inscrição de dispositivos Apple

É necessário um certificado de push MDM para a inscrição do iOS/iPadOS e do dispositivo macOS. Saiba mais sobre os [certificados Push de MDM](apple-mdm-push-certificate-get.md).

## <a name="corporate-identifiers"></a>Identificadores empresariais

Pode listar os números de série e números do Identificador de Equipamento Móvel Internacional (IMEI) para identificar os dispositivos da empresa. Saiba mais sobre [identificadores empresariais](corporate-identifiers-add.md).
## <a name="multi-factor-authentication"></a>Multi-factor authentication

Pode exigir que os utilizadores utilizem um método de verificação adicional, como um telemóvel, PIN ou dados biométricos, quando estes inscrevem um dispositivo. Saiba mais sobre a [autenticação multifator](multi-factor-authentication.md).

## <a name="device-enrollment-manager"></a>Gestor de inscrição de dispositivos
Pode transformar os utilizadores em gestores de inscrição de dispositivos.  Os utilizadores DEM podem inscrever um grande número de dispositivos móveis com uma única conta de utilizador. A conta do gestor de inscrição de dispositivos (DEM) pode inscrever até 1000 dispositivos. Saiba mais sobre os [gestores de inscrição de dispositivos](device-enrollment-manager-enroll.md).

## <a name="device-categories"></a>Categorias de dispositivos

Pode utilizar categorias de dispositivos para adicionar automaticamente dispositivos a grupos com base nas categorias que definir. Organizar dispositivos em grupos facilita a gestão desses dispositivos. Saiba mais sobre [categorias de dispositivos](device-group-mapping.md).
