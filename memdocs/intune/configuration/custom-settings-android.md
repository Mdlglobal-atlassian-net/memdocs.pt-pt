---
title: Adicionar definições personalizadas a dispositivos Android no Microsoft Intune – Azure | Microsoft Docs
description: Adicionar ou criar um perfil personalizado para dispositivos Android para criar um perfil Wi-Fi com uma chave pré-partilhada, criar um perfil de VPN por aplicação ou permitir/bloquear aplicações para dispositivos Samsung Knox Standard no Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 494b3892-916e-4b40-9b67-61adec889bdf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 77f0df858f94f3d0b8d6c3a4ee2b251e6b917da6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333177"
---
# <a name="use-custom-settings-for-android-devices-in-microsoft-intune"></a>Utilizar definições personalizadas para dispositivos Android no Microsoft Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos Android com um "perfil personalizado". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Android utilizam as definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades em dispositivos Android. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar essas funcionalidades.

A utilização de um perfil personalizado permite configurar e atribuir as seguintes definições do Android. As seguintes definições não estão incorporadas no Intune:

- [Criar um perfil Wi-Fi com uma chave pré-partilhada](/intune/wi-fi-profile-shared-key)
- [Criar um perfil VPN por app](/intune/android-pulse-secure-per-app-vpn)
- [Permitir e bloquear aplicações para dispositivos Samsung Knox Standard](/intune/samsung-knox-apps-allow-block)

>[!IMPORTANT]
> Apenas as definições apresentadas podem ser configuradas por um perfil personalizado. Os dispositivos Android não expõem uma lista completa das definições OMA-URI que pode configurar. Se quiser ver mais definições, contribua com o seu voto para a adição de mais definições no [site do UserVoice do Intune](https://microsoftintune.uservoice.com/forums/291681-ideas).

Este artigo mostra-lhe como criar um perfil personalizado para dispositivos Android.

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil personalizado Android**.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **Android**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    - **Nome**: introduza um nome exclusivo para a definição OMA-URI, para poder encontrá-la facilmente.
    - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
    - **OMA-URI**: introduza o OMA-URI que quer utilizar como uma definição.
    - Tipo de **dados:** Selecione o tipo de dados que utilizará para esta definição OMA-URI. As opções são:

      - String
      - Cadeia (ficheiro XML)
      - Data e hora
      - Número inteiro
      - Vírgula flutuante
      - Booleano
      - Base64 (ficheiro)

    - **Valor**: introduza o valor de dados que pretende associar à definição OMA-URI que introduziu. O valor depende do tipo de dados que selecionou. Por exemplo, se selecionar **Data e Hora,** selecione o valor de um apanhador de datas.

    Depois de adicionar algumas definições, pode selecionar **Exportar**. A opção **Exportar** cria uma lista de todos os valores que adicionou num ficheiro de valores separados por vírgulas (.csv).

5. Selecione **OK** para guardar as alterações. Continue a adicionar mais definições conforme necessário.
6. Quando terminar, selecione **OK** > **Criar** para criar o perfil Intune. Quando estiver concluído, o seu perfil é mostrado na lista de perfis de configuração - **Configuração.**

## <a name="next-steps"></a>Passos seguintes

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Crie um [perfil personalizado em dispositivos Android Enterprise](custom-settings-android-for-work.md).
