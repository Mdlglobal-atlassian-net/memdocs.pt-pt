---
title: Alterações de auditoria e eventos no Microsoft Intune - Azure Microsoft Docs
description: Saiba como rever os registos de auditoria que registam as atividades do Microsoft Intune.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 923a7c192121530d84ca2034b2ca8a4be3cc32d6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990754"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Utilize registos de auditoria para monitorizar e monitorizar eventos no Microsoft Intune

Os registos de auditoria incluem um registo de atividades que geram uma mudança no Microsoft Intune. Criar, atualizar (editar), excluir, atribuir e remotas ações criam eventos de auditoria que os administradores podem rever para a maioria das cargas de trabalho intune. Por predefinição, a auditoria está ativada para todos os clientes. Não pode ser desativado.

> [!NOTE]
> Os eventos de auditoria começaram a ser gravados no lançamento da funcionalidade de dezembro de 2017. Eventos anteriores não estão disponíveis.

## <a name="who-can-access-the-data"></a>Quem pode aceder aos dados?

Os utilizadores com as seguintes permissões podem rever os registos de auditoria:

- Administrador Global
- Administrador de Serviços do Intune
- Administradores designados para um papel intune com **dados de auditoria**  -  **Ler** permissões

## <a name="audit-logs-for-intune-workloads"></a>Registos de auditoria das cargas de trabalho do Intune

Pode rever os registos de auditoria no grupo de monitorização para cada carga horária intune:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione registos de auditoria **da administração do arrendatário**  >  **Audit logs**.
3. Para filtrar os resultados, selecione **Filter** e refine os resultados utilizando as seguintes opções.
    - **Categoria**: tais como **Conformidade,** **Dispositivo**e **Função**.
    - **Atividade**: as opções aqui enumeradas são restritas pela opção escolhida na **categoria**.
    - **Intervalo**de datas: pode escolher registos para o mês, semana ou dia anteriores.
4. Escolha **Aplicar**.
4. Selecione um item na lista para ver os detalhes da atividade.

## <a name="route-logs-to-azure-monitor"></a>Rota logs para Monitor Azure

Os registos de auditoria e os registos operacionais também podem ser encaminhados para o Monitor Azure. Nos **registos de auditoria,** selecione Definições de **Dados de Exportação:**

![Exportar dados de registo para o monitor Azure selecionando as definições de dados de exportação em Intune](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Para obter mais informações sobre esta funcionalidade e rever os pré-requisitos para a sua utilização, consulte o envio de dados de [registo para armazenamento, centros](review-logs-using-azure-monitor.md)de eventos ou análise de registo .

> [!NOTE]
> **Iniciado por (ator)** inclui informações sobre quem dirigia a tarefa, e para onde era executado. Por exemplo, se executar a atividade em Intune no portal Azure, então a **Aplicação** lista sempre a extensão do **portal Microsoft Intune** e o ID da **aplicação** usa sempre o mesmo GUID.
>
> A secção **Target(s)** lista vários alvos e as propriedades que foram alteradas.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Utilizar a Graph API para obter eventos de auditoria

Para mais detalhes sobre a utilização do gráfico API para chegar a um ano de eventos de auditoria, consulte a [auditoria da ListaEventos](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Passos seguintes

[Envie dados de registo para armazenamento, centros de eventos ou análise de registo.](review-logs-using-azure-monitor.md)

[Reveja os registos](../apps/app-protection-policy-settings-log.md)de proteção de aplicativos do cliente .
