---
title: Referência técnica de descarregamento de aplicações
titleSuffix: Configuration Manager
description: Referência técnica de descarregamento de aplicações de resolução de problemas para O Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709811"
---
# <a name="application-download-in-configuration-manager"></a>Download de aplicação em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de continuar, consulte os componentes do cliente de implementação de [aplicações](client-components-technical-reference.md) para entender o processamento de trabalho do DCM e do Ci Agent.

## <a name="download-initiation"></a>Iniciar o download

O download de conteúdo de aplicação é iniciado pelo componente do Agente CI no cliente durante a fase **StateDownloadingContents.** Este processo é o mesmo, independentemente de a aplicação ser implementada para uma Coleção de Dispositivos ou uma coleção de Utilizadores.

- Para implementações **disponíveis,** o conteúdo da aplicação é descarregado quando o utilizador inicia a instalação da aplicação a partir do Software Center.
- Para as implementações **necessárias,** o conteúdo da aplicação é descarregado quando a atribuição é ativada e a aplicação é encontrada Aplicável após avaliação. Para entender quando a atribuição é ativada, consulte a Implementação da [Aplicação para Coleções](device-deployment-technical-reference.md) de Dispositivos ou Implementação de [Aplicações para artigos](user-deployment-technical-reference.md) de Recolha de Utilizadores.

Quando o Agente CI inicia o download de conteúdo, cria uma tarefa que é tratada pelo componente ci Task Manager. O CI Task Manager inicia então o download de conteúdos. Esta atividade pode ser rastreada no **log CITaskMgr** utilizando o ID exclusivo do tipo de implementação.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Localização do ponto de distribuição

Todas as tarefas de descarregamento são tratadas pela componente Content Access, que é responsável pela gestão da cache do cliente. Após a criação da tarefa de descarregamento, o componente content Access verifica se o conteúdo já está disponível na cache do cliente. Se o conteúdo não estiver disponível, cria um pedido de localização para obter uma lista de Pontos de Distribuição de onde o conteúdo pode ser obtido. Esta atividade pode ser rastreada em **CAS.log** e **LocationServices.log** no cliente usando o ID Exclusivo de Conteúdo.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Embora o componente de Serviços de Localização trate dos pedidos de localização, não solicita diretamente localizações a partir do Ponto de Gestão. Todos os pedidos para o Ponto de Gestão normalmente passam pela componente de Mensagens CCM, que regista o **CcmMessaging.log**.

Resposta de localização XML contém a lista de pontos de distribuição com base no grupo de fronteira do cliente. Esta lista é analisada e persistiu no IMC sobre o cliente de acordo com a [Prioridade fonte](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority)de conteúdo . Esta atividade pode ser vista em **ContentTransferManager.log,** utilizando `Persisted location`o ID exclusivo do conteúdo e procurando por . 

Se a resposta de localização XML não contiver quaisquer `Received empty location update` pontos de distribuição, **contentTransferManager.log** mostraria e o cliente pode ficar preso a 0% ao descarregar a aplicação. Esta resposta pode ocorrer normalmente devido a problemas de configuração de grupo sem limites. Para mais informações, consulte [falhas de download](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Download de conteúdos

Uma vez obtidas as localizações do Ponto de Distribuição, o componente de Acesso ao Conteúdo cria um trabalho de Transferência de Conteúdo. Esta atividade pode ser rastreada no **CAS.log** utilizando o ID Exclusivo de Conteúdo.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

O Gestor de Transferência de Conteúdos cria então um trabalho de Serviço de Transferência de Dados para fazer o download de conteúdos. Esta atividade pode ser rastreada em **ContentTransferManager.log** no cliente usando o ID Exclusivo de Conteúdo.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Esta entrada de registo pode ser utilizada para identificar os ID de trabalho CTM e DTS, que podem ser utilizados para acompanhar o progresso da Transferência de Conteúdos em **ContentTransferManager.log** e **DataTransferService.log,** respectivamente.

O Serviço de Transferência de Dados realiza o download do conteúdo da aplicação criando um trabalho de Serviço de Transferência Inteligente de Fundo (BITS) e aguardando que o download seja concluído. Esta atividade pode ser rastreada em **DataTransferService.log** no cliente utilizando o ID de trabalho dTS obtido a partir de **ContentTransferService.log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Após o download estar concluído, o componente content Access é notificado. A componente de Acesso ao Conteúdo verifica então o conteúdo descarregado para garantir que o conteúdo não foi alterado durante o download. Esta atividade pode ser rastreada no **CAS.log** utilizando o ID Exclusivo de Conteúdo.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Finalmente, após a verificação do conteúdo, o Agente CI recebe a notificação completa da tarefa e o trabalho do Agente CI passa para a fase seguinte.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Passos Seguintes

- [Instalação de Aplicações](deployment-install-technical-reference.md)
