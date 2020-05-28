---
title: Painel de instrumentos de dispositivo de superfície
titleSuffix: Configuration Manager
description: Reveja as informações sobre os dispositivos Surface utilizando o painel de instrumentos.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: f9b9c49bde16754b7a60112905f14da2cd5e48eb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906280"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Painel de instrumentos de dispositivo de superfície no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A partir da versão 1802, o painel do dispositivo Surface dá-lhe informações sobre dispositivos Surface encontrados no seu ambiente num único olhar. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abra o painel do dispositivo Surface

Para abrir o painel do dispositivo Surface, utilize os seguintes passos: 

1. Abra a consola do Configuration Manager. 
2. Clique no nó **de monitorização.** 
3. Para carregar o painel de instrumentos, clique em **Dispositivos de Superfície**.

**Painel de instrumentos de** 
 ![ dispositivo de superfície Painel de instrumentos de dispositivo de superfície](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Revisão de informações no painel de instrumentos do dispositivo Surface

O painel do dispositivo Surface mostra três gráficos para o seu ambiente. 

- **Por cento dos dispositivos Surface** -Dá-lhe a percentagem de dispositivos Surface em todo o seu ambiente.

    ![Por cento do gráfico de dispositivos surface](media/Percent-Surface-Devices.PNG)
- **Modelos** de superfície - Mostra o número de dispositivos por modelo Surface. 
  - Pairar sobre uma secção de gráfico supor-lhe-á a percentagem de dispositivos Surface que são o modelo selecionado. 

       ![Gráfico de modelos de superfície](media/Surface-Models-Hover.PNG)
  - Clicar numa secção de gráfico supor á lista de dispositivos para o modelo. 
      ![Lista de dispositivos de modelo de superfície](media/Surface-Model-Device-List.PNG)

- **Top 5 versões firmware**- Exibe um gráfico com os cinco melhores modelos de firmware no seu ambiente. 
  - Pairar sobre uma secção de gráfico supor-lhe-á o número de dispositivos Surface que são a versão firmware selecionada. Começando na versão 1806 do Gestor de Configuração, clicar numa secção de gráfico apresenta uma lista de dispositivos relevantes. <!--1358654-->
     ![Lista de dispositivos de modelo de superfície](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mais informações

Para obter mais informações sobre os dispositivos Surface, consulte o site [surface.](https://www.microsoft.com/surface)

Para obter mais informações sobre a implementação de atualizações de firmware surface no Gestor de Configuração, consulte [como gerir as atualizações](https://support.microsoft.com/help/4098906)do controlador do Surface .




