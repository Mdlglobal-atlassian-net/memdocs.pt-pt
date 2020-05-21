---
title: Adicionar definições personalizadas para dispositivos Windows Phone 8.1 no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Adicione ou crie um perfil personalizado para utilizar as definições OMA-URI para dispositivos com o Windows Phone 8.1 no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce8433ee87c0f5e4b397003b78c0ceb751eb46b7
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556273"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Utilizar definições personalizadas para dispositivos Windows Phone 8.1 no Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos Windows Phone 8.1 com "perfis personalizados". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Windows Phone 8.1 utilizam definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar as funcionalidades no dispositivo. [A documentação do protocolo do Windows Phone 8.1 MDM](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) lista as definições.

Este artigo mostra-lhe como criar um perfil personalizado para dispositivos Windows Phone 8.1. 

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil personalizado do Windows Phone 8.1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Definições oMA-URI personalizadas

- **Definições OMA-URI**: **Adicione** as seguintes definições:

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

## <a name="example"></a>Exemplo

No exemplo seguinte, os dispositivos telefónicos do Windows 8.1 estão impedidos de mudar as redes celulares quando viajam fora da área de cobertura da transportadora.

- **Nome**: Permitir roaming de dados celulares
- **Descrição**: Permitir ou proibir o roaming de dados celulares
- **OMA-URI** (sensível a casos): ./Fornecedor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Tipo**de dados : Inteiro
- **Valor**: 0

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Criar um [perfil personalizado nos dispositivos windows 10](custom-settings-windows-10.md).
