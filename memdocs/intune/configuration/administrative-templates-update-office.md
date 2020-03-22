---
title: Update Office 365 utilizando modelos administrativos no Microsoft Intune - Azure  Microsoft Docs
description: Utilize modelos administrativos no Microsoft Intune para atualizar as aplicações do Office 365 para a versão mais recente e escolher a frequência com que o Office verifica as atualizações. Consulte as teclas de registo do dispositivo que são atualizadas quando é aplicada uma política intune para a atualização do Office.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235fabd5f184117e680c44b87e5eab4334596e1c
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083885"
---
# <a name="use-update-channel-and-target-version-settings-to-update-office-365-with-microsoft-intune-administrative-templates"></a>Utilize as definições do Canal de Atualização e da Versão target para atualizar o Office 365 com modelos administrativos intune da Microsoft

Em Intune, pode utilizar [os modelos do Windows 10 para configurar as definições](administrative-templates-windows.md)de política do grupo . Este artigo mostra-lhe como atualizar o Office 365 usando um modelo administrativo em Intune. Também dá orientações sobre a confirmação da aplicação das suas políticas com sucesso. Esta informação também ajuda na resolução de problemas.

Neste cenário, cria um modelo administrativo em Intune que atualiza o Office 365 nos seus dispositivos.

Para obter mais informações sobre os modelos administrativos, consulte [os modelos do Windows 10 para configurar as definições](administrative-templates-windows.md)de política do grupo .

Aplica-se a:

- Windows 10 e posterior
- Office 365

## <a name="prerequisites"></a>Pré-requisitos

Certifique-se de [ativar as Atualizações Automáticas Do Office365 ProPlus](https://docs.microsoft.com/deployoffice/configure-update-settings-for-office-365-proplus) para as suas aplicações do Office. Pode fazê-lo usando a política de grupo, ou o modelo INTune Office 2016 ADMX:

![No modelo administrativo intune, defina a definição de atualizações automáticas ativas para o Office](./media/administrative-templates-update-office/admx-enable-automatic-updates.png)

## <a name="set-the-update-channel-in-the-intune-administrative-template"></a>Defina o Canal de Atualização no modelo administrativo Intune

1. No seu [modelo administrativo Intune,](administrative-templates-windows.md#create-a-template)vá à definição do **Canal de Atualização** e introduza o canal que deseja. Por exemplo, escolha `Semi-Annual Channel`:

    ![No modelo administrativo intune, defina a definição do Canal de Atualização para o Office](./media/administrative-templates-update-office/admx-enable-update-channel-setting.png)

    > [!NOTE]
    > É aconselhável atualizar com mais frequência. Semi-anualmente só é usado como exemplo.

2. Certifique-se de [atribuir a apólice](device-profile-assign.md) aos seus dispositivos Windows 10. Para testar a sua política mais cedo, também pode sincronizar a política:

    - [Sincronizar a política em Intune](../remote-actions/device-sync.md)
    - [Sincronizar manualmente a política do dispositivo](https://docs.microsoft.com/mem/intune/user-help/sync-your-device-manually-windows#sync-from-settings-app)

## <a name="check-the-intune-registry-keys"></a>Verifique as teclas de registo Intune

Depois de atribuir a apólice e os sincronizados do dispositivo, pode confirmar a aplicação da política:

1. No dispositivo, abra a aplicação **Registry Editor.**
2. Vá ao caminho político intune: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`.

    > [!TIP]
    > O `<Provider ID>` na chave do registo muda. Para encontrar o ID do fornecedor para o seu dispositivo, abra a aplicação **Registry Editor** e vá para `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\AdmxInstalled`. O ID do fornecedor é mostrado.

    Quando a apólice é aplicada, consulte as seguintes teclas de registo:

    - `L_UpdateBranch`
    - `L_UpdateTargetVersion`

    Olhando para o exemplo seguinte, vê-se `L_UpdateBranch` tem um valor semelhante ao `<enabled /><data id="L_UpdateBranchID" value="Deferred" />`. Este valor significa que está definido para o Canal Semi-Anual:

    ![Modelo administrativo L_Updatebranch exemplo chave do registo](./media/administrative-templates-update-office/admx-update-branch-registry-key.png)

    > [!TIP]
    > Gerir o [Office 365 ProPlus com O Gestor](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) de Configuração lista os valores e o que significam. Os valores do registo baseiam-se no canal de distribuição selecionado:
    >
    >- Canal Mensal - valor="Corrente"
    >- Canal mensal (Direcionado) - valor="Corrente"
    >- Canal Semi-Anual - valor="Corrente"
    >- Canal Semi-Anual (Direcionado) - valor="FirstReleaseDeferred"
    >- Insider Fast - value="InsiderFast"

Neste momento, a política Intune é aplicada com sucesso ao dispositivo.

## <a name="check-the-office-registry-keys"></a>Verifique as chaves do registo do Escritório

1. No dispositivo, abra a aplicação **Registry Editor.**
2. Ir para o caminho político do Escritório: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`.

    Veja as seguintes chaves de registo:

    - `UpdateChannel`: Uma chave dinâmica que muda, dependendo das definições configuradas.
    - `CDNBaseUrl`: Configurado quando o Office 365 instalar no aparelho.

3. Olhe para o valor `UpdateChannel`. O valor diz-lhe com que frequência o Office é atualizado. Gerir o [Office 365 ProPlus com O Gestor](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) de Configuração lista os valores e o que estão definidos.

    Olhando para o seguinte exemplo, vê-se `UpdateChannel` está definido para `http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60`, que é **mensalmente:**

    ![Modelo administrativo Office UpdateChannel exemplo de chave de registo](./media/administrative-templates-update-office/admx-update-channel-office-registry-key.png)

    Este exemplo significa que a política ainda não foi aplicada, uma vez que ainda está definida para **mensalmente**, em vez de **semi-anual**.

Esta chave de registo é atualizada quando o Programador de **Tarefas** > **Atualizações Automáticas do Office 2.0,** ou quando um utilizador entra no dispositivo. Para confirmar, abra as **Atualizações Automáticas do Office 2.0** tarefa > **Triggers**. Dependendo dos seus gatilhos, pode demorar pelo menos um dia e mais até que a chave de registo `UpdateChannel` seja atualizada.

## <a name="force-office-automatic-updates-to-run"></a>Atualizações automáticas do Force Office para executar

Para testar a sua política, pode forçar as definições de política no dispositivo. Os seguintes passos atualizam o registo. Como sempre, tenha cuidado ao atualizar o registo.

1. Limpe a chave do registo:

    1. Aceda a `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates`.
    2. Selecione duas vezes a tecla `UpdateDetectionLastRunTime`, elimine os dados de valor > **OK**.

2. Executar a tarefa de Atualizações Automáticas do Office:

    1. Abra a aplicação **'Agendar de Tarefas'** no dispositivo.
    2. Expandir a Biblioteca do Programador de **Tarefas** > **Microsoft** > **Office**.
    3. Selecione **Atualizações Automáticas de Escritório 2.0** > **Executar:**

        ![Agenda de tarefas abertas e executar atualizações automáticas do Office](./media/administrative-templates-update-office/admx-task-scheduler-office-automatic-updates.png)

        Aguarde a tarefa para terminar, o que pode levar alguns minutos.

3. Na aplicação **Registry Editor,** vá a `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration`. Verifique o valor `UpdateChannel`.

    Deve ser atualizado com o valor estabelecido na política. No nosso exemplo, o valor deve ser fixado para `http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114`.

Neste ponto, o canal de atualização do Office é alterado com sucesso no dispositivo. Pode abrir uma aplicação office 365 para um utilizador que recebe esta atualização para verificar o estado.

## <a name="force-the-office-synchronization-to-update-account-information"></a>Forçar a sincronização do Office a atualizar a informação da conta  

Se quiser fazer mais, pode forçar o Office a obter a mais recente atualização da versão. Os seguintes passos só devem ser feitos como confirmação, ou se precisar dos dispositivos para obter a mais recente atualização da versão a partir desse canal rapidamente. Caso contrário, deixe o Office fazer o seu trabalho e atualize automaticamente.

### <a name="step-1-force-the-office-version-to-update"></a>Passo 1: Forçar a versão do Office a atualizar

1. Confirme que a versão do Office suporta o canal de atualização que está a escolher. [Atualizar o histórico para o Office 365 ProPlus](https://docs.microsoft.com/officeupdates/update-history-office365-proplus-by-date) lista os números de construção que suportam os diferentes canais de atualização.

2. No seu [modelo administrativo Intune,](administrative-templates-windows.md#create-a-template)vá à definição da **Versão Target** e introduza a versão pretendida.

    A definição da **versão Target** é semelhante à seguinte definição:

    ![No modelo administrativo intune, defina a definição de versão-alvo para o Office](./media/administrative-templates-update-office/admx-enable-target-version-setting.png)

> [!IMPORTANT]
>
> - Certifique-se de atribuir a apólice.
> - Se alterar uma política existente, as suas alterações afetam todos os utilizadores designados.
> - Se estiver a testar esta funcionalidade, é aconselhável criar uma política de teste e atribuir a política a um grupo de utilizadores de teste.

### <a name="step-2-check-the-office-version"></a>Passo 2: Verifique a versão do Office

Considere utilizar estes passos para testar a sua política antes de implementar a política para todos os utilizadores.

1. Na aplicação **Registry Editor,** vá a `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`

2. Olhe para o valor `L_UpdateTargetVersion`. Uma vez que a apólice se aplique, o valor é definido para a versão que introduziu, como `<enabled /><data id="L_UpdateTargetVersionID" value="16.0.10730.20344" />`.

    Neste momento, a política Intune é aplicada com sucesso ao dispositivo.

3. Em seguida, pode forçar o Office a atualizar. Abra uma aplicação do Office, como o Excel. Opte por atualizar agora (possivelmente no menu **Conta).**

    A atualização leva vários minutos. Pode confirmar que o Office está a tentar obter a versão em que entra:

      1. No aparelho, vá para `C:\Program Files (x86)\Microsoft Office\Updates\Detection\Version`.
      2. Abra o ficheiro `VersionDescriptor.xml` e vá para a secção `<Version>`. A versão disponível deve ser a mesma versão que inscreveu na política Intune, tais como:

          ![Verifique a secção de versão no ficheiro descritor do Office XML](./media/administrative-templates-update-office/office-version-descriptor-xml-example.png)

4. Após a instalação da atualização, a aplicação do Office deve mostrar a nova versão (por exemplo, no menu **Conta)**

## <a name="next-steps"></a>Próximos passos

[Atualizar os valores dos canais para os clientes do Office 365](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel)

[Visão geral do serviço de política de nuvem do Office para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)

[Utilize os modelos do Windows 10 para configurar as definições de política de grupo (modelos ADMX) no Microsoft Intune](administrative-templates-windows.md)
