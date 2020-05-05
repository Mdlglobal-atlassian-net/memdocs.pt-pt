---
title: Inscrever dispositivos para MDM no local
titleSuffix: Configuration Manager
description: Conheça os métodos de inscrição de dispositivos para a gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720675"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Inscreva dispositivos para MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para gerir os dispositivos com a gestão de dispositivos móveis do Gestor de Configuração (MDM), é necessário matriculá-los primeiro. Em seguida, o Gestor de Configuração pode comunicar com os dispositivos para tarefas de gestão. O Gestor de Configuração fornece dois métodos para inscrever dispositivos:

- **Inscrição**do utilizador : Os utilizadores iniciam o processo de inscrição no seu dispositivo. Para que a inscrição do utilizador tenha sucesso, instale o certificado raiz fidedigno no dispositivo e provisão do utilizador para inscrição nas definições do cliente. Para inscrever um dispositivo, o utilizador apenas precisa de introduzir as suas credenciais.

    Para mais informações, consulte [como os utilizadores matriculam os dispositivos](user-enroll-devices-on-premises-mdm.md).

- **Inscrição**a granel : O utilizador do dispositivo não inicia a inscrição. Cria um pacote de inscrição a granel no Gestor de Configuração. Ao abra-o no dispositivo, a embalagem fornece as informações necessárias para inscrever o dispositivo.

    Para mais informações, consulte [Como inscrever em massa dispositivos](bulk-enroll-devices-on-premises-mdm.md).

Para obter mais informações sobre as versões OS que o Gestor de Configuração suporta para a inscrição de dispositivos no MDM no local, consulte [configurações suportadas](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
