---
title: Adicionar definições personalizadas para dispositivos Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Adicione ou crie um perfil personalizado para utilizar as definições OMA-URI para dispositivos com o Windows 10 no Microsoft Intune. Utilize um perfil personalizado para adicionar definições personalizadas.
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
ms.openlocfilehash: 5b6646c67f9425d395bbec1e33c03f6f29b6af7e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332353"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Utilizar definições personalizadas para dispositivos Windows 10 no Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos Windows 10 com "perfis personalizados". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Windows 10 utilizam definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar as funcionalidades no dispositivo. 

O Windows 10 disponibiliza diversas definições do Fornecedor de Serviços de Configuração (CSP), tal como o [Fornecedor de Serviços de Configuração de Políticas (CSP de Políticas)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers).

Se estiver à procura de uma definição específica, lembre-se de que o [perfil de restrição de dispositivos Windows 10](device-restrictions-windows-10.md) inclui várias definições incorporadas. Por isso, poderá não ter de introduzir valores personalizados.

Este artigo apresenta o seguinte:

- Como criar um perfil personalizado para dispositivos Windows 10
- Uma lista de definições OMA-URI recomendadas
- Um exemplo de um perfil personalizado que abre uma ligação VPN

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil personalizado do Windows 10**.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    - **Nome** – introduza um nome exclusivo para a definição OMA-URI para o ajudar a identificá-la na lista de definições.
    - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
    - **OMA-URI** (sensível a maiúsculas e minúsculas): introduza a definição OMA-URI que pretende utilizar.
    - Tipo de **dados:** Selecione o tipo de dados que utilizará para esta definição OMA-URI. As opções são:

        - Cadeia
        - Cadeia (ficheiro XML)
        - Data e Hora
        - Número inteiro
        - Vírgula flutuante
        - Booleano
        - Base64 (ficheiro)

    - **Valor**: introduza o valor de dados que pretende associar à definição OMA-URI que introduziu. O valor depende do tipo de dados que selecionou. Por exemplo, se selecionar **Data e Hora,** selecione o valor de um apanhador de datas.

    Depois de adicionar algumas definições, pode selecionar **Exportar**. A opção **Exportar** cria uma lista de todos os valores que adicionou num ficheiro de valores separados por vírgulas (.csv).

5. Selecione **OK** para guardar as alterações. Continue a adicionar mais definições conforme necessário.
6. Quando terminar, selecione **OK** > **Criar** para criar o perfil Intune. Quando estiver concluído, o seu perfil é mostrado na lista de perfis de configuração - **Configuração.**

## <a name="example"></a>Exemplo

No seguinte exemplo, a definição **Conectividade/PermitirVPNAtravésDeRedeMóvel** está ativada. Esta definição permite que um dispositivo com o Windows 10 abra uma ligação VPN através de uma rede móvel.

![Exemplo de uma política personalizada que contém as definições de VPN](./media/custom-settings-windows-10/custom-policy-example.png)

## <a name="find-the-policies-you-can-configure"></a>Encontrar as políticas que pode configurar

Está disponível uma lista completa de todos os fornecedores de serviços de configuração (CSPs) suportados pelo Windows 10 na [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração).

Nem todas as definições são compatíveis com todas as versões do Windows 10. O artigo [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração) indica-lhe que versões são suportadas para cada CSP.

Além disso, o Intune não suporta todas as definições apresentadas na [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (Referência de fornecedores de serviços de configuração). Para saber se o Intune suporta a definição que pretende, abra o artigo referente a essa definição. Cada página de definição mostra a respetiva operação suportada. Para trabalhar com intune, a definição deve suportar as operações **Add,** **Replace**e **Get.** Se o valor devolvido pela operação **Get** não corresponder ao valor fornecido pelas operações **Add** ou **Replace,** então intune reporta um erro de conformidade.

## <a name="next-steps"></a>Próximos passos

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
