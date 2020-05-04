---
title: Referência técnica de instalação de aplicação
titleSuffix: Configuration Manager
description: Instalações de aplicações de resolução de problemas referência técnica para Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709783"
---
# <a name="application-installation"></a>Instalação de Aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de continuar, consulte os componentes do cliente de implementação de [aplicações](client-components-technical-reference.md) para entender o processamento de trabalho do DCM e do Ci Agent.

A instalação da aplicação é realizada por componentes do Agente DCM e do Agente CI quando a implementação é executada. O tempo de execução difere para as implementações disponíveis e necessárias. Para entender quando a atribuição é executada, consulte a Implementação de [Aplicações para Recolha de Dispositivos](device-deployment-technical-reference.md) ou Implementação de [Aplicações para artigos](user-deployment-technical-reference.md) de Recolha de Utilizadores.

## <a name="enforcement-initiation"></a>Iniciação de Execução

A instalação da aplicação é iniciada pelo componente do Agente CI no cliente durante a fase **StateEnforcingCIs.** Este processo é o mesmo, independentemente de a aplicação ser implementada para uma Coleção de Dispositivos ou uma coleção de Utilizadores.

- Para implementações **disponíveis,** a aplicação é instalada quando o utilizador inicia a instalação da aplicação a partir do Software Center.
- Para as implementações **necessárias,** a aplicação é instalada no prazo de implementação. No entanto, o utilizador pode iniciar a instalação a partir do Software Center antes do prazo.

Quando o agente CI inicia a instalação da aplicação, cria uma tarefa que é tratada pelo componente ci Task Manager. O Ci Task Manager inicia então a instalação. Esta atividade pode ser rastreada no **log CITaskMgr** utilizando o ID exclusivo do tipo de implementação.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Aplicação da aplicação

Após o início da aplicação, o cliente realiza novamente a deteção da aplicação para garantir que a aplicação ainda não está instalada. Uma vez determinado que a aplicação não está instalada, a instalação da aplicação é iniciada. Esta atividade pode ser rastreada no **AppEnforce.log** no cliente utilizando o ID Exclusivo do Tipo de Implementação.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Verificação de instalação

Após a instalação da aplicação, o método de deteção da aplicação é novamente utilizado para garantir que a aplicação foi detetada conforme instalada.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Finalmente, após a execução estar concluída, o Agente CI recebe a notificação completa da tarefa e o trabalho do Agente CI passa para a fase seguinte.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Passos Seguintes

[Implementações de aplicações de resolução de problemas](../deploy-use/troubleshoot-application-deployment.md)
