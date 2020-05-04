---
title: Adicionar definições personalizadas para dispositivos Windows Phone 8.1 no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Adicione ou crie um perfil personalizado para utilizar as definições OMA-URI para dispositivos com o Windows Phone 8.1 no Microsoft Intune.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1bea9047d65faf449c77e1a677000d32e883a76
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333153"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Utilizar definições personalizadas para dispositivos Windows Phone 8.1 no Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos Windows Phone 8.1 com "perfis personalizados". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Windows Phone 8.1 utilizam definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar as funcionalidades no dispositivo. [A documentação do protocolo do Windows Phone 8.1 MDM](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) lista as definições.

Este artigo mostra-lhe como criar um perfil personalizado para dispositivos Windows Phone 8.1. 

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil personalizado do Windows Phone**.
    - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
    - **Plataforma**: Selecione **Windows Phone 8.1**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    - **Nome** – introduza um nome exclusivo para a definição OMA-URI para o ajudar a identificá-la na lista de definições.
    - **Descrição**: introduza uma descrição geral da definição e quaisquer outras informações relevantes para o ajudar a localizar o perfil.
    - **OMA-URI** (sensível a maiúsculas e minúsculas): introduza a definição OMA-URI que pretende utilizar.
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

## <a name="example"></a>Exemplo

No exemplo seguinte, os dispositivos telefónicos do Windows 8.1 estão impedidos de mudar as redes celulares quando viajam fora da área de cobertura da transportadora.

- **Nome**: Permitir roaming de dados celulares
- **Descrição**: Permitir ou proibir o roaming de dados celulares
- **OMA-URI** (sensível a casos): ./Fornecedor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Tipo**de dados : Inteiro
- **Valor**: 0

## <a name="next-steps"></a>Passos seguintes

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Criar um [perfil personalizado nos dispositivos windows 10](custom-settings-windows-10.md).
