---
title: Gerir a encriptação do disco com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com a política de encriptação de discos de segurança final no Microsoft Endpoint Manager.
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
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431311"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Política de encriptação de disco para segurança de ponto final em Intune

Os perfis de encriptação do disco de segurança endpoint focam-se apenas nas definições que são relevantes para um método de encriptação incorporado em dispositivos, como fileVault ou BitLocker. Este foco facilita a gestão de configurações de encriptação do disco sem ter de navegar por uma série de configurações não relacionadas.

Embora possa configurar as definições do mesmo dispositivo utilizando perfis de *proteção* de ponto final para a configuração do dispositivo, os perfis de configuração do dispositivo incluem categorias adicionais de definições. Estas definições adicionais não estão relacionadas com a encriptação do disco e podem complicar a tarefa de configurar apenas a encriptação do disco.

Encontre as políticas de segurança de ponto final para as políticas de encriptação do disco no *âmbito do Manage* in the **Endpoint security** node do centro de administração do Microsoft [Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Pré-requisitos para a política de encriptação do disco

- **macOS** - macOS 10.13 ou posterior
- **Windows** - Windows 10 ou mais tarde

## <a name="disk-encryption-profiles"></a>Perfis de encriptação do disco

**perfis macOS:**

- **FileVault** - FileVault fornece encriptação full-in de disco incorporado para dispositivos macOS.

  Gerir [as definições do FileVault](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) para macOS.

  Para criar um perfil FileVault, consulte a encriptação do [disco Use FileVault para macOS](../protect/encrypt-devices-filevault.md).

**Perfis do Windows 10:**

- **BitLocker** - BitLocker Drive Encryption é uma funcionalidade de proteção de dados que se integra com o sistema operativo e aborda as ameaças de roubo de dados ou exposição de computadores perdidos, roubados ou inadequadamente desativados

  [Gerencie as definições bitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) para o Windows 10.

  Para criar um perfil BitLocker, consulte a encriptação do [disco Use BitLocker para windows 10](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Gerir a encriptação do dispositivo

Depois de implementar a política para encriptar um disco de dispositivo, consulte os seguintes artigos para obter informações sobre a gestão da encriptação:

- [Gerir o BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Gerir fileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Monitor device encryption (Monitorizar encriptação de dispositivos)](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Próximos passos

- [Para criar um perfil FileVault](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [Para criar um perfil BitLocker](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
