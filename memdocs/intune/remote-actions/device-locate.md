---
title: Encontre dispositivos iOS/iPadOS perdidos com a Microsoft Intune - Azure Microsoft Docs
description: Localize dispositivos iOS/iPadOS perdidos ou roubados utilizando a funcionalidade de localizar o dispositivo no Microsoft Intune. Obtenha detalhes sobre as informações de segurança e privacidade ao utilizar a ação Localizar dispositivo.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3e544286-12ad-4a3a-86f8-d2cf16940b1f
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 825105fb11c37293285638e8d86514aae4ba8303
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989877"
---
# <a name="locate-lost-or-stolen-iosipados-devices-with-intune"></a>Localizar dispositivos iOS/iPadOS perdidos ou roubados com Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Para obter a localização de um dispositivo iOS/iPadOS perdido ou roubado num mapa, utilize a ação do **dispositivo Localizar.** O dispositivo tem de estar no modo supervisionado. Antes de utilizar esta ação, certifique-se de que o dispositivo está no [modo perdido](device-lost-mode.md).

## <a name="supported-platforms"></a>Plataformas suportadas

- iOS/iPadOS 9.3 e mais tarde

Esta funcionalidade não é suportada para os seguintes sistemas: 
- Windows
- Windows Phone
- macOS
- Android

## <a name="locate-a-lost-or-stolen-device"></a>Localizar um dispositivo perdido ou roubado

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecione **Dispositivos** e, em seguida, selecione **Todos os dispositivos**.
4. A partir da lista de dispositivos que gere, escolha um dispositivo iOS/iPadOS e **escolha... Mais.** Em seguida, selecione a ação remota **Localizar dispositivo**.
5. Após localizar o dispositivo, a localização dele é apresentada em **Localizar dispositivo**.
    ![Captura de ecrã da localização de um dispositivo com o Intune no Azure](./media/device-locate/locate-device.png)


## <a name="activate-lost-mode-sound-alert-on-an-ios-device"></a>Ativar o alerta de som do modo perdido num dispositivo iOS

Se alguém tiver perdido o seu dispositivo iOS/iPadOS 9.3 ou posterior, pode acionar remotamente o dispositivo para reproduzir um som de alerta para que o utilizador o encontre. O dispositivo tem de estar no [modo perdido](device-lost-mode.md).

No [Intune no portal Azure,](https://aka.ms/intuneportal)escolha **Dispositivos**  >  **Todos os dispositivos** > selecione um dispositivo iOS/iPadOS > som do modo **Overview**  >  **Overview More**  >  **Play Lost (apenas supervisionar)**.

O som continuará a reproduzir até que o utilizador desative o som no dispositivo ou o dispositivo seja removido do modo perdido.


## <a name="security-and-privacy-information-for-lost-mode-and-locate-device-actions"></a>Informações de segurança e privacidade para o modo perdido e ações de localização do dispositivo
- Nenhuma informação de localização do dispositivo é enviada para o Intune até ativar esta ação.
- Ao utilizar a ação Localizar dispositivo, as coordenadas de latitude e longitude do dispositivo podem ser obtidas através da Graph API.
- Os dados são armazenados durante 24 horas e, em seguida, são removidos. Não pode remover manualmente os dados de localização.
- Os dados de localização são encriptados quando são armazenados e, igualmente, quando estão a ser transmitidos.
- Ao configurar o modo perdido, pode personalizar uma mensagem que é apresentada no ecrã de bloqueio. Nesta mensagem, para ajudar a pessoa que encontrar o dispositivo, certifique-se de que inclui detalhes específicos sobre como devolver o dispositivo perdido.

## <a name="next-steps"></a>Passos seguintes

Para ver o estado de ativação da ação Localizar Dispositivo, aceda a **Dispositivos** e selecione **Ações do dispositivo**.
