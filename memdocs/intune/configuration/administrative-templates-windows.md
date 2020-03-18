---
title: Utilizar modelos para dispositivos Windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Utilize modelos administrativos no Microsoft Intune para criar grupos de definições para dispositivos Windows 10. Utilize estas definições num perfil de configuração do dispositivo para controlar os programas do Office, microsoft Edge, funcionalidades seguras no Internet Explorer, controlar o acesso ao OneDrive, utilizar funcionalidades remotas de ambiente de trabalho, ativar a Reprodução automática, definir definições de gestão de energia, utilizar impressão HTTP, utilize diferentes sintetizadores de utilizador em opções e controle o tamanho do registo do evento.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1d11d54b2421ff523b8b429af231ea55fe21210c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332401"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Utilize os modelos do Windows 10 para configurar as definições de política de grupo no Microsoft Intune

Ao gerir dispositivos na sua organização, pretende criar grupos de configurações que se aplicam a diferentes grupos de dispositivos. Por exemplo, tem vários grupos de dispositivos. Para o GrupoA, pretende atribuir um conjunto específico de definições. Para o GrupoB, pretende atribuir um conjunto diferente de configurações. Também deseja uma visão simples das definições que pode configurar.

Pode completar esta tarefa utilizando **modelos administrativos** no Microsoft Intune. Os modelos administrativos incluem centenas de configurações que controlam funcionalidades na versão 77 do Microsoft Edge e posteriormente, O Internet Explorer, programas do Microsoft Office, desktop remoto, OneDrive, palavras-passe e PINs, e muito mais. Estas configurações permitem aos administradores do grupo gerir as políticas do grupo utilizando a nuvem.

As definições do Windows são semelhantes às definições da política de grupo (GPO) no Diretório Ativo (AD). Estas definições são incorporadas no Windows, e são [configurações apoiadas por ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) que usam XML. As definições do Office e do Microsoft Edge são ingeridas por ADMX e utilizam as definições ADMX nos ficheiros de [modelos administrativos do Office](https://www.microsoft.com/download/details.aspx?id=49030) e nos ficheiros de [modelos administrativos do Microsoft Edge](https://www.microsoftedgeinsider.com/enterprise). Mas os modelos Intune são 100% baseados em nuvens. Oferecem uma forma simples e direta de configurar as definições e encontrar as definições que deseja.

**Os modelos administrativos** são incorporados em Intune, e não requerem nenhuma personalização, incluindo a utilização de OMA-URI. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições de modelo como uma loja de balcão único para gerir os seus dispositivos Windows 10.

Este artigo lista os passos para criar um modelo para dispositivos Windows 10 e mostra como filtrar todas as definições disponíveis em Intune. Quando cria o modelo, cria um perfil de configuração do dispositivo. Pode então atribuir ou implementar este perfil para dispositivos Windows 10 na sua organização.

## <a name="before-you-begin"></a>Antes de começar

- Algumas destas definições estão disponíveis a partir da versão 1703 (RS2) do Windows 10. Algumas definições não estão incluídas em todas as edições do Windows. Para a melhor experiência, sugere-se a utilização da versão 1903 (19H1) do Windows 10 Enterprise e mais recente.

- As definições do Windows utilizam [CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)de política do Windows . Os CSPs trabalham em diferentes edições do Windows, tais como Home, Professional, Enterprise, e assim por diante. Para ver se um CSP funciona numa edição específica, vá aos [CSPs de política do Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-a-template"></a>Criar um modelo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome para o perfil.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Tipo de perfil**: Selecionar **modelos administrativos**.

4. Selecione **Criar**. Na nova janela, selecione a lista de drop-down e selecione **Todos os produtos**. A partir da lista, também pode filtrar as definições para apenas mostrar as definições **do Windows,** apenas mostrar as definições **do Office,** ou apenas mostrar as definições **da versão Edge 77 ou posteriores:**

    > [!div class="mx-imgBorder"]
    > ![Filtrar a lista para mostrar todas as definições do Windows ou de todas as definições do Office em modelos administrativos em Intune](./media/administrative-templates-windows/administrative-templates-choose-windows-office-all-products.png)

    > [!NOTE]
    > As definições do Microsoft Edge aplicam-se a:
    >
    > - Microsoft Edge versão 77 e mais recente. Para configurar a versão 45 do Microsoft Edge e anteriormente, consulte [as definições](device-restrictions-windows-10.md#microsoft-edge-browser)de restrição do dispositivo do Microsoft Edge Browser .
    > - Windows 10 RS4 e mais recente com [KB 4512509](https://support.microsoft.com/kb/4512509) instalado
    > - Windows 10 RS5 e mais recente com [KB 4512534](https://support.microsoft.com/kb/4512534) instalado
    > - Windows 10 19H1 e mais recente com [KB 4512941](https://support.microsoft.com/kb/4512941) instalado

5. Todas as definições estão listadas e pode utilizar as setas antes e as próximas para ver mais definições:

    > [!div class="mx-imgBorder"]
    > ![Ver uma lista de definições e utilizar botões anteriores e seguintes](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

    > [!TIP]
    > As definições do Windows em Intune correlacionaram-se com o percurso político do grupo no local que vê no Editor de Política do Grupo Local (`gpedit`).

6. Selecione qualquer definição. Por exemplo, filtrar no **Office**, e selecionar **Ativar a navegação restrita**. É mostrada uma descrição detalhada da definição. Escolha **ativado,** **desativado,** ou deixe a definição como **Não configurada** (predefinido). A descrição detalhada também explica o que acontece quando escolhe **Ativado,** **Desativado**ou **Não configurado**.
7. Selecione **OK** para guardar as alterações.

Continue a analisar a lista de definições e configure as definições que deseja no seu ambiente. Aqui estão alguns exemplos:

- Utilize a definição de Definições de **Notificação Macro VBA** para lidar com macros VBA em diferentes programas do Microsoft Office, incluindo Word e Excel.
- Utilize a definição de transferências de **ficheiros Permitir** ou impedir transferências do Internet Explorer.
- Utilização **Requerer uma palavra-passe quando um computador acordar (ligado)** para solicitar aos utilizadores uma palavra-passe quando os dispositivos acordarem do modo de sono.
- Utilize a definição de **controlos ActiveX não assinados** para impedir que os utilizadores descarreguem controlos ActiveX não assinados do Internet Explorer.
- Utilize a definição de **desligação** do sistema para permitir ou evitar que os utilizadores executem uma restauração do sistema no dispositivo.
- Utilize a definição de permitir a **importação de favoritos** para permitir ou bloquear os utilizadores de importar em outro navegador os favoritos para o Microsoft Edge.
- E muito mais...

## <a name="find-some-settings"></a>Encontre algumas definições

Existem centenas de configurações disponíveis nestes modelos. Para facilitar a procura de configurações específicas, utilize as características incorporadas:

- No seu modelo, selecione as colunas **Definições**, **Estado**, **Definição**ou **Caminho** para classificar a lista. Por exemplo, selecione a coluna **Path** e utilize a seta seguinte para ver as definições no caminho `Microsoft Excel`:

  > [!div class="mx-imgBorder"]
  > ![Clique no caminho para mostrar todas as definições agruparadas pela política do grupo ou pelo caminho ADMX em modelos administrativos em Intune](./media/administrative-templates-windows/path-filter-shows-excel-options.png)

- No seu modelo, utilize a caixa **de pesquisa** para encontrar configurações específicas. Pode pesquisar por definição ou caminho. Por exemplo, procure `copy`. Todas as definições com `copy` são mostradas:

  > [!div class="mx-imgBorder"]
  > ![Procurar cópia para mostrar todas as definições do Windows e Office em modelos administrativos em Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  Noutro exemplo, procure `microsoft word`. Veja todas as definições que pode definir para o programa Microsoft Word. Procure por `explorer` para ver todas as definições do Internet Explorer que pode adicionar ao seu modelo.

## <a name="next-steps"></a>Próximos passos

O modelo é criado, mas ainda não está a fazer nada. Em seguida, [atribuir o modelo, também chamado de perfil](device-profile-assign.md) e monitorizar o seu [estado](device-profile-monitor.md).

[Atualizar o Office 365 utilizando modelos administrativos](administrative-templates-update-office.md).

[Tutorial: Use a nuvem para configurar a política de grupo em dispositivos Windows 10 com modelos ADMX e Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
