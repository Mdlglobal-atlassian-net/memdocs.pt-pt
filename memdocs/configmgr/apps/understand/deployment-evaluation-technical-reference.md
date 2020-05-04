---
title: Referência técnica de avaliação de candidaturas
titleSuffix: Configuration Manager
description: Referência técnica de avaliação de aplicações de resolução de problemas para O Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709797"
---
# <a name="application-deployment-evaluation"></a>Avaliação de Implementação de Aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de continuar, consulte os componentes do cliente de implementação de [aplicações](client-components-technical-reference.md) para entender o processamento de trabalho do DCM e do Ci Agent.

A avaliação da aplicação é realizada pelos componentes do Agente DCM e do Agente CI quando a implementação é ativada. Para entender quando a atribuição é ativada, consulte a Implementação da [Aplicação para Coleções](device-deployment-technical-reference.md) de Dispositivos ou Implementação de [Aplicações para artigos](user-deployment-technical-reference.md) de Recolha de Utilizadores.

## <a name="application-detection-and-evaluation"></a>Deteção e Avaliação de Aplicações

A avaliação da candidatura é realizada durante a fase invocando O Método **invocando** um trabalho de agente de CI. Esta fase é onde o cliente avalia o método de deteção definido para a aplicação para determinar se a aplicação está instalada no dispositivo. Esta atividade pode ser rastreada em **AppDiscovery.log** utilizando o id exclusivo do tipo de implementação ou nome do tipo de implementação.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> O exemplo acima mostra a deteção de uma aplicação MSI onde a deteção é feita verificando se o Código do Produto MSI está instalado no dispositivo. Para aplicações que utilizem métodos de deteção alternativos, o método de deteção adequado é utilizado para verificar se a aplicação está instalada.

Em seguida, o cliente avalia o estado desejado da aplicação com base no Objetivo de Implantação. Este passo passa também por detetar se a aplicação tem alguma dependência ou regras de supersedência que devem ser honradas para a aplicação. Esta atividade pode ser rastreada em **AppIntentEval.log** utilizando o ID exclusivo do tipo de aplicação e implementação.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

Na entrada de registo acima, o **Estado Atual** indica se a aplicação está atualmente instalada no dispositivo. **A aplicabilidade** indica se a aplicação é aplicável com base em regras de exigência definidas. **O Estado Resolvido** indica o estado desejado da aplicação com base no objetivo de implantação.

> [!TIP]
> Utilize a Ferramenta de Monitorização de [Implementação](../../core/support/deployment-monitoring-tool.md) para visualizar o estado de aplicação, o estado de aplicabilidade e as violações de requisitos.

## <a name="next-steps"></a>Passos Seguintes

- [Download de aplicações](deployment-download-technical-reference.md)
