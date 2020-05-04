---
title: Referência técnica de componentes de aplicação de componentes de cliente
titleSuffix: Configuration Manager
description: Componentes do cliente utilizados para a implementação de aplicações de resolução de problemas no Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709804"
---
# <a name="understanding-application-deployment-client-components"></a>Compreender componentes do cliente de implementação de aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

As operações de avaliação e execução de aplicações são tratadas pelos componentes do Agente DCM e do Agente CI no cliente. Este artigo explica como funciona um trabalho típico de DCM e CI Agent.

## <a name="dcm-agent"></a>Agente DCM

O Agente DCM é o componente cliente de alto nível responsável pela avaliação de itens de configuração, que inclui aplicações. Quando uma implementação é ativada ou executada, é criado um trabalho de Agente DCM que lê a política de atribuição e determina as ações que devem ser executadas. Esta atividade pode ser rastreada no **DCMAgent.log** no cliente usando o DCM Agent Job ID, que pode ser identificado procurando o ID Exclusivo aplicação.

### <a name="device-deployments"></a>Implementações de dispositivos

- Para as implementações **necessárias,** o DCMAgent.log mostraria as ações aplicáveis. Estas ações podem diferir consoante o prazo de implantação já tenha passado.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Para as implementações **disponíveis,** dCMAgent.log mostra que a implementação `is not mandatory`. Para estas implementações, a avaliação da aplicação é feita, mas a aplicação é ignorada a menos que o utilizador tenha iniciado a instalação.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Implementações de utilizadores

- Para as implementações **necessárias,** o DCMAgent.log mostraria as ações aplicáveis. Estas ações podem diferir consoante o prazo de implantação já tenha passado.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Para as implementações **disponíveis,** os postos de trabalho do Agente DCM são criados para avaliação e execução quando a instalação da aplicação é iniciada pelo utilizador.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>Agente CI

O Agente CI é o componente cliente responsável pela avaliação e remediação de itens de configuração. O Agente DCM lê a política de atribuição e cria um trabalho para o componente do Agente CI realizar as ações solicitadas. **DCMAgent.log** registra o ID de trabalho do agente ci, que é útil para rastrear a atividade do agente CI no **CIAgent.log** no cliente.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Um trabalho típico do Agente CI passa por várias fases, que podem ser identificadas filtrando **o CIAgent.log** no ID de trabalho do agente ci e, em seguida, procurando `TransitionState`. Algumas das fases-chave para um trabalho de agente ci de implementação de aplicações são:

- **DownloadCIs**
  - Durante esta fase, os metadados da aplicação necessários para avaliar a aplicação são descarregados. Os metadados incluem método de deteção, regras de requisitos, condições globais, etc. Esta atividade pode ser rastreada em **CIDownloader.log** e **DataTransferService.log**. Para as implementações **disponíveis,** este processo ocorre durante a primeira avaliação da aplicação. No entanto, para as implementações **necessárias,** este processo ocorre imediatamente após o download da apólice.

- **Invocar o Método de Invocar**
  - Durante esta fase, o método de deteção da aplicação é utilizado para verificar se a aplicação está instalada e o estado desejado é determinado. Esta atividade pode ser rastreada em **AppDiscovery.log** e **AppIntentEval.log**. Para mais informações sobre esta fase, consulte Avaliação de [Aplicações.](deployment-evaluation-technical-reference.md)

- **StateDownloadingConteúdos**
  - Durante esta fase, o conteúdo da aplicação é descarregado se necessário. Esta atividade pode ser rastreada em **CAS.log**, **ContentTransferManager.log,** **LocationServices.log**e **DataTransferService.log**. Para mais informações sobre esta fase, consulte O Download de [Aplicações](deployment-download-technical-reference.md).

- **Estatal**
  - Durante esta fase, inicia-se a instalação da aplicação. Esta atividade pode ser rastreada em **AppEnforce.log**. Para mais informações sobre esta fase, consulte instalação de [aplicação.](deployment-install-technical-reference.md)

- **Relatórios estatais**
  - Durante esta fase, o estado de instalação da aplicação é registado para reporte ao Ponto de Gestão. Esta atividade pode ser rastreada em **StateMessage.log**.

Embora o trabalho do Agente ci passa por todas as fases, salta a fase se não for necessário. Como exemplo, para as implementações **disponíveis,** os conteúdos de transferência de estado e as fases stateenforcingCIs são ignorados até que o utilizador tente instalar a aplicação a partir do Software Center. No entanto, para as implementações **necessárias,** a fase StateDownloadingContents descarrega o conteúdo da aplicação (se necessário) quando a atribuição é ativada, mas a fase stateenforcingCIs é ignorada se o prazo for no futuro. Este comportamento pode ser observado no log CIAgent.filtrando o ID `Skipping policy`de trabalho do agente ci e procurando .

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Passos Seguintes

- [Avaliação de Candidaturas](deployment-evaluation-technical-reference.md)
- [Download de aplicações](deployment-download-technical-reference.md)
- [Instalação de Aplicações](deployment-install-technical-reference.md)
