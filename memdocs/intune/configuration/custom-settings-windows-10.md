---
title: Adicionar definições personalizadas para dispositivos Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Adicione ou crie um perfil personalizado para utilizar as definições OMA-URI para dispositivos com o Windows 10 no Microsoft Intune. Utilize um perfil personalizado para adicionar definições personalizadas.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96074f4bea22b7468b1f210d631f0912eeafe7b5
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428997"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Utilizar definições personalizadas para dispositivos Windows 10 no Intune

Este artigo lista e descreve todas as diferentes definições personalizadas que pode controlar no Windows 10 e em dispositivos mais recentes. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para configurar configurações que não estejam incorporadas no Intune.

Para obter mais informações sobre perfis personalizados, consulte [Criar um perfil com configurações personalizadas](custom-settings-configure.md).

Estas definições são adicionadas a um perfil de configuração do dispositivo em Intune e, em seguida, atribuídas ou implantadas para os seus dispositivos Windows 10.

Esta funcionalidade aplica-se a:

- Windows 10 e mais recente

Os perfis personalizados do Windows 10 utilizam definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar as funcionalidades no dispositivo.

O Windows 10 disponibiliza diversas definições do Fornecedor de Serviços de Configuração (CSP), tal como o [Fornecedor de Serviços de Configuração de Políticas (CSP de Políticas)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers).

Se estiver à procura de uma definição específica, lembre-se de que o [perfil de restrição de dispositivos Windows 10](device-restrictions-windows-10.md) inclui várias definições incorporadas. Por isso, poderá não ter de introduzir valores personalizados.

## <a name="before-you-begin"></a>Antes de começar

[Criar um perfil personalizado do Windows 10.](custom-settings-configure.md#create-the-profile)

## <a name="oma-uri-settings"></a>Definições OMA-URI

**Adicionar**: Introduza as seguintes definições:

- **Nome** – introduza um nome exclusivo para a definição OMA-URI para o ajudar a identificá-la na lista de definições.
- **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
- **OMA-URI** (sensível a maiúsculas e minúsculas): introduza a definição OMA-URI que pretende utilizar.
- Tipo de **dados:** Selecione o tipo de dados que utilizará para esta definição OMA-URI. As opções são:

  - Base64 (ficheiro)
  - Booleano
  - Cadeia (ficheiro XML)
  - Data e hora
  - String
  - Vírgula flutuante
  - Número inteiro

- **Valor**: introduza o valor de dados que pretende associar à definição OMA-URI que introduziu. O valor depende do tipo de dados que selecionou. Por exemplo, se selecionar **Data e Hora,** selecione o valor de um apanhador de datas.

Depois de adicionar algumas definições, pode selecionar **Exportar**. A opção **Exportar** cria uma lista de todos os valores que adicionou num ficheiro de valores separados por vírgulas (.csv).

## <a name="find-the-policies-you-can-configure"></a>Encontrar as políticas que pode configurar

Está disponível uma lista completa de todos os fornecedores de serviços de configuração (CSPs) suportados pelo Windows 10 na [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração).

Nem todas as definições são compatíveis com todas as versões do Windows 10. O artigo [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração) indica-lhe que versões são suportadas para cada CSP.

Além disso, o Intune não suporta todas as definições apresentadas na [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração). Para saber se o Intune suporta a definição que pretende, abra o artigo referente a essa definição. Cada página de definição mostra a respetiva operação suportada. Para trabalhar com intune, a definição deve suportar as operações **Add,** **Replace**e **Get.** Se o valor devolvido pela operação **Get** não corresponder ao valor fornecido pelas operações **Add** ou **Replace,** então intune reporta um erro de conformidade.

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

[Saiba mais sobre perfis personalizados em Intune](custom-settings-configure.md).
