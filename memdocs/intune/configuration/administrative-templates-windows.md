---
title: Utilizar modelos para dispositivos Windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Utilize modelos administrativos no Microsoft Intune e Endpoint Manager para criar grupos de definições para dispositivos Windows 10. Utilize estas definições num perfil de configuração do dispositivo para controlar os programas do Office, microsoft Edge, funcionalidades seguras no Internet Explorer, controlar o acesso ao OneDrive, utilizar funcionalidades remotas de ambiente de trabalho, ativar o Auto-Play, definir definições de gestão de energia, utilizar a impressão HTTP, utilizar diferentes opções de entrada do utilizador e controlar o tamanho do registo do evento.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
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
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254899"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Utilize os modelos do Windows 10 para configurar as definições de política de grupo no Microsoft Intune

Ao gerir dispositivos na sua organização, pretende criar grupos de configurações que se aplicam a diferentes grupos de dispositivos. Por exemplo, tem vários grupos de dispositivos. Para o GrupoA, pretende atribuir um conjunto específico de definições. Para o GrupoB, pretende atribuir um conjunto diferente de configurações. Também deseja uma visão simples das definições que pode configurar.

Pode completar esta tarefa utilizando **modelos administrativos** no Microsoft Intune. Os modelos administrativos incluem centenas de configurações que controlam funcionalidades na versão 77 do Microsoft Edge e posteriormente, O Internet Explorer, programas do Microsoft Office, desktop remoto, OneDrive, palavras-passe e PINs, e muito mais. Estas configurações permitem aos administradores do grupo gerir as políticas do grupo utilizando a nuvem.

Esta funcionalidade aplica-se a:

- Windows 10 e mais recente

As definições do Windows são semelhantes às definições da política de grupo (GPO) no Diretório Ativo (AD). Estas definições são incorporadas no Windows, e são [configurações apoiadas por ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) que usam XML. As definições do Office e do Microsoft Edge são ingeridas por ADMX e utilizam as definições ADMX nos ficheiros de [modelos administrativos do Office](https://www.microsoft.com/download/details.aspx?id=49030) e nos ficheiros de [modelos administrativos do Microsoft Edge](https://www.microsoftedgeinsider.com/enterprise). E, os modelos Intune são 100% baseados em nuvens. Oferecem uma forma simples e direta de configurar as definições e encontrar as definições que deseja.

**Os modelos administrativos** são incorporados em Intune, e não requerem nenhuma personalização, incluindo a utilização de OMA-URI. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições de modelo como uma loja de balcão único para gerir os seus dispositivos Windows 10.

Este artigo lista os passos para criar um modelo para dispositivos Windows 10 e mostra como filtrar todas as definições disponíveis em Intune. Quando cria o modelo, cria um perfil de configuração do dispositivo. Pode então atribuir ou implementar este perfil para dispositivos Windows 10 na sua organização.

## <a name="before-you-begin"></a>Antes de começar

- Algumas destas definições estão disponíveis a partir da versão 1709 do Windows 10 (RS2/build 15063). Algumas definições não estão incluídas em todas as edições do Windows. Para a melhor experiência, sugere-se a utilização da versão 1903 do Windows 10 Enterprise (19H1/build 18362) e mais recente.

- As definições do Windows utilizam [CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)de política do Windows . Os CSPs trabalham em diferentes edições do Windows, tais como Home, Professional, Enterprise, e assim por diante. Para ver se um CSP funciona numa edição específica, vá aos [CSPs de política do Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Criar o modelo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Perfil**: Selecionar **modelos administrativos**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é modelo de Administrador: modelo de **administração do Windows 10 que configura as definições de xyz no Microsoft Edge**.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **configuração,** configure as definições que se aplicam ao dispositivo ( configuração do**computador)** e as definições que se aplicam aos utilizadores **(configuração do utilizador):**

    > [!div class="mx-imgBorder"]
    > ![Aplicar as definições do modelo ADMX aos utilizadores e dispositivos no Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Quando selecionar a configuração do **Computador,** as categorias de definição são mostradas. Pode selecionar qualquer categoria para ver as definições disponíveis.

    Por exemplo, selecione **a configuração** > do Computador**Windows Aplicações** > **Internet Explorer** para ver todas as definições do dispositivo que se aplicam ao Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Consulte todas as definições do dispositivo que se aplicam ao Internet Explorer no Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. Também pode selecionar **Todas as definições** para ver todas as definições do dispositivo. Desloque-se para baixo para utilizar as setas antes e as próximas para ver mais definições:

    > [!div class="mx-imgBorder"]
    > ![Consulte uma lista de definições de amostrae use botões anteriores e próximos](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Selecione qualquer definição. Por exemplo, filtrar no **Office**, e selecionar **Ativar a navegação restrita**. É mostrada uma descrição detalhada da definição. Escolha **ativado,** **desativado,** ou deixe a definição como **Não configurada** (predefinido). A descrição detalhada também explica o que acontece quando escolhe **Ativado,** **Desativado**ou **Não configurado**.

    > [!TIP]
    > As definições do Windows em Intune correlacionaram-se com o caminho`gpedit`de política do grupo no local que você vê no Editor de Política do Grupo Local ( )

11. Selecione **OK** para guardar as alterações.

    Continue a analisar a lista de definições e configure as definições que deseja no seu ambiente. Eis alguns exemplos:

    - Utilize a definição de Definições de **Notificação Macro VBA** para lidar com macros VBA em diferentes programas do Microsoft Office, incluindo Word e Excel.
    - Utilize a definição de transferências de **ficheiros Permitir** ou impedir transferências do Internet Explorer.
    - Utilização **Requerer uma palavra-passe quando um computador acordar (ligado)** para solicitar aos utilizadores uma palavra-passe quando os dispositivos acordarem do modo de sono.
    - Utilize a definição de **controlos ActiveX não assinados** para impedir que os utilizadores descarreguem controlos ActiveX não assinados do Internet Explorer.
    - Utilize a definição de **desligação** do sistema para permitir ou evitar que os utilizadores executem uma restauração do sistema no dispositivo.
    - Utilize a definição de permitir a **importação de favoritos** para permitir ou bloquear os utilizadores de importar em outro navegador os favoritos para o Microsoft Edge.
    - E muito mais...

12. Selecione **Seguinte**.
13. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para `US-NC IT Team` `JohnGlenn_ITDepartment`filtrar o perfil a grupos de TI específicos, tais como ou . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](..//fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

14. Em **Atribuições,** selecione o utilizador ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Se o perfil for atribuído aos grupos de utilizadores, as definições de ADMX configuradas aplicam-se a qualquer dispositivo que o utilizador inscreva e instem. Se o perfil for atribuído a grupos de dispositivos, as definições de ADMX configuradas aplicam-se a qualquer utilizador que assine nesse dispositivo. Esta atribuição acontece se a definição`HKEY_LOCAL_MACHINE`ADMX for uma`HKEY_CURRENT_USER`configuração de computador ( ou uma configuração do utilizador ). Com algumas definições, uma definição de computador atribuída a um utilizador também pode ter impacto na experiência de outros utilizadores nesse dispositivo.
    
    Para mais informações, consulte [grupos de utilizadores vs. grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).

    Selecione **Seguinte**.

15. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

Da próxima vez que o dispositivo verificar as atualizações de configuração, as definições configuradas são aplicadas.

## <a name="find-some-settings"></a>Encontre algumas definições

Existem centenas de configurações disponíveis nestes modelos. Para facilitar a procura de configurações específicas, utilize as características incorporadas:

- No seu modelo, selecione as colunas **Definições**, **Estado**, **Definição**ou **Caminho** para classificar a lista. Por exemplo, selecione a coluna **Path** e utilize `Microsoft Excel` a seta seguinte para ver as definições no caminho:

- No seu modelo, utilize a caixa **de pesquisa** para encontrar configurações específicas. Pode pesquisar por definição ou caminho. Por exemplo, procure `copy`. Todas as `copy` definições com são mostradas:

  > [!div class="mx-imgBorder"]
  > ![Procure cópia para mostrar todas as definições do dispositivo em modelos administrativos em Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  Noutro exemplo, `microsoft word`procure. Veja as definições que pode definir para o programa Microsoft Word. Procure `explorer` ver as definições do Internet Explorer que pode adicionar ao seu modelo.

## <a name="next-steps"></a>Passos seguintes

O modelo é criado, mas pode ainda não estar a fazer nada. Em seguida, [atribuir o modelo (também chamado de perfil)](device-profile-assign.md) e [monitorizar o seu estado](device-profile-monitor.md).

Atualizar [o Office 365 utilizando modelos administrativos](administrative-templates-update-office.md).

[Tutorial: Use a nuvem para configurar a política de grupo em dispositivos Windows 10 com modelos ADMX e Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
