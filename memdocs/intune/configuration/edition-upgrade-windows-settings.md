---
title: Atualização do Windows 10 e definições de modo S no Microsoft Intune - Azure Microsoft Docs
description: Consulte uma lista de todas as definições e o que fazem ao atualizar uma edição do Windows 10 num dispositivo, ou ativar o modo S num dispositivo utilizando um perfil de configuração do dispositivo no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ab94c3cc8bb9009d49a6b301d9a67fa6ffc5f1a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333085"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Definições do dispositivo Windows 10 (e mais recentes) para atualizar edições ou ativar o modo S em Intune

O Microsoft Intune inclui muitas definições para ajudar a gerir e proteger os seus dispositivos. Este artigo lista e descreve as definições para atualizar edições ou ativar o modo S nos dispositivos Windows 10. Estas definições são criadas num perfil de configuração de upgrade em Intune que são empurrados ou implantados para dispositivos.

Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para controlar as opções de edição e modo S para os seus dispositivos Windows 10.

Para mais informações sobre esta funcionalidade, consulte [as edições do Upgrade Windows 10 ou ativar](edition-upgrade-configure-windows-10.md)o modo S .

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](edition-upgrade-configure-windows-10.md#create-the-profile)

## <a name="edition-upgrade"></a>Atualização de edição

- **Edição a atualizar**: selecione a edição Windows 10 para a qual está a atualizar. Os dispositivos visados por esta política são atualizados para a edição que escolher.
- **Chave de Produto**: introduza a chave de produto que recebeu da Microsoft. Depois de criar a política que contém a chave de produto, a chave não pode ser atualizada e é ocultada por motivos de segurança. Para alterar a chave de produto, introduza novamente a chave completa.
- **Ficheiro de Licença**: para **Windows 10 Holographic for Business** ou **Edição Windows 10 Mobile**, selecione **Procurar** para selecionar o ficheiro de licença que recebeu da Microsoft. Este ficheiro de licença inclui informações de licença para as edições para as quais está a atualizar os dispositivos.

## <a name="mode-switch"></a>Interruptor de modo

- **Sem configuração**: Um dispositivo de modo S permanece no modo S. Um utilizador final pode retirar o dispositivo do modo S.
- **Manter no modo S**: não permite ao utilizador final retirar o dispositivo do modo S.
- **Alterar**: retira o dispositivo do modo S.

## <a name="next-steps"></a>Passos seguintes

O perfil é criado, mas pode ainda não estar a fazer nada. Certifique-se de [atribuir o perfil](device-profile-assign.md)e monitorizar [o seu estado](device-profile-monitor.md).

Também pode criar perfis de upgrade de edição para [dispositivos Windows Holographic para](holographic-upgrade.md) dispositivos Business.
