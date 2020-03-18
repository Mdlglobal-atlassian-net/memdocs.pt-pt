---
title: Política do Microsoft Intune para permitir/bloquear aplicações do Samsung Knox
titleSuffix: ''
description: Crie um perfil personalizado para permitir e bloquear aplicações para dispositivos Samsung Knox Standard.
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
ms.openlocfilehash: e558d0fe2f6112f522420d51cad4943e819b4fb0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331981"
---
# <a name="use-custom-policies-in-microsoft-intune-to-allow-and-block-apps-for-samsung-knox-standard-devices"></a>Utilizar políticas personalizadas no Microsoft Intune para permitir e bloquear aplicações para dispositivos Samsung Knox Standard 

Utilize o procedimento neste artigo para criar uma política personalizada do Microsoft Intune que crie um dos seguintes casos:

- Uma lista de aplicações que estão bloqueadas de executar no dispositivo. A execução das aplicações nesta lista está bloqueada, mesmo se já tiverem sido instaladas quando a política foi aplicada.
- Uma lista de aplicações que os utilizadores do dispositivo estão autorizados a instalar a partir da loja Google Play. Apenas as aplicações na lista podem ser instaladas. Mais nenhuma outra aplicação pode ser instalada a partir da loja.

Estas definições só podem ser utilizadas por dispositivos com o Samsung Knox Standard.

## <a name="create-an-allowed-or-blocked-app-list"></a>Criar uma lista de aplicações permitidas ou bloqueadas

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes definições:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **perfil personalizado do Windows Phone**.
    - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
    - **Plataforma**: Selecione **Android**.
    - **Tipo de perfil**: Selecione **Personalizado**.

4. Em **Definições OMA-URI Personalizadas**, selecione **Adicionar**. Introduza as seguintes definições:

    Para uma lista de aplicações que estão impedidas de executar no dispositivo:

    - **Nome**: Enter **PreventStartPackages**.
    - **Descrição**: introduza uma descrição geral da definição e quaisquer outras informações relevantes para o ajudar a localizar o perfil. Por exemplo, introduza **lista de aplicações que estão bloqueadas de executar**.
    - **OMA-URI** (sensível a casos): Insira **./Fornecedor/MSFT/PolicyManager/My/ApplicationManagement/PreventStartPackages**.
    - **Tipo de dados**: Selecione **String**.
    - **Valor**: Insira uma lista dos nomes do pacote da aplicação que pretende permitir. Pode utilizar `;`, `:`ou `|` como delimitador. Por exemplo, introduza `package1;package2;`.

   Para uma lista de aplicações que os utilizadores têm permissão para instalar a partir da Google Play Store, excluindo todas as outras aplicações:

    - **Nome**: Enter **allowinstallPackages**.
    - **Descrição**:Introduza uma descrição que dê uma visão geral da definição e quaisquer outras informações relevantes para ajudá-lo a localizar o perfil. Por exemplo, introduza **a Lista de aplicações que os utilizadores podem instalar a partir do Google Play**.
    - **OMA-URI** (sensível a casos): Insira **./Fornecedor/MSFT/PolicyManager/My/ApplicationManagement/AllowInstallPackages**.
    - **Tipo de dados**: Selecione **String**.
    - **Valor**: Insira uma lista dos nomes do pacote da aplicação que pretende permitir. Pode utilizar `;`, `:`ou `|` como delimitador. Por exemplo, introduza `package1;package2;`.

5. Selecione **OK** para guardar as alterações.
6. Quando terminar, selecione **OK** > **Criar** para criar o perfil Intune. Quando estiver concluído, o seu perfil é mostrado na lista de perfis de configuração - **Configuração.**

>[!TIP]
> Pode localizar o ID do pacote de uma aplicação ao navegar para a aplicação na Google Play Store. O ID do pacote está contido no URL da página da aplicação. Por exemplo, o ID do pacote da aplicação Microsoft Word é **com.microsoft.office.word**.

Da próxima vez que cada dispositivo direcionado verificar, as definições da aplicação são aplicadas.

## <a name="next-steps"></a>Próximos passos

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
