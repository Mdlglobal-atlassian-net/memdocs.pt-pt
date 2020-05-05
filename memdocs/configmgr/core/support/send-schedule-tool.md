---
title: Ferramenta de Envio de Agendamento
titleSuffix: Configuration Manager
description: Utilize a Ferramenta de Agenda de Envio para desencadear um horário num cliente do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723125"
---
# <a name="send-schedule-tool"></a>Ferramenta de Envio de Agendamento

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Ferramenta de Agenda de Envio é uma das ferramentas do Gestor de [Configuração.](tools.md) Use-o para desencadear um horário num cliente ou desencadear a avaliação de uma linha de base de configuração especificada. Funciona para o computador local ou para um cliente remoto.  

Por exemplo, utilize a ferramenta para desencadear um calendário de inventário ou avaliação de conformidade. Se alguns clientes do Gestor de Configuração não reportaram recentemente o estado de inventário ou conformidade, execute a ferramenta para iniciar o horário necessário em cada cliente.



## <a name="usage"></a>Utilização

Executar **SendSchedule.exe** como administrador. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Depois de acionar uma mensagem (GUID), consulte **SMSClientMethodProvider.log**. Para obter mais informações sobre guiDs de mensagem disponível, consulte [IDs de mensagem](#bkmk_sendschedule-guids).

Depois de iniciar a avaliação de uma linha de base de configuração (DCM UID), consulte **DCMAgent.log**.



## <a name="command-line-options"></a>Opções da linha de comandos


### <a name="option-l"></a>Opção:`/L` 
Enumerar todos os DCM UID de Mensagem disponíveis para envio. Mostrar o nome significativo das mensagens na tabela de dados para cada uma delas. Se o nome do computador estiver ausente, utiliza o computador local. Se especificar uma mensagem sem um nome de máquina, envia a mensagem para a máquina local. 



## <a name="examples"></a>Exemplos

#### <a name="list-the-available-messages-on-the-local-machine"></a>Listar as mensagens disponíveis na máquina local 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Lista rine as mensagens disponíveis no MyPC do cliente: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Desencadear o inventário de hardware na máquina local
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Desencadear o inventário de hardware no MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Desencadear a avaliação de uma linha de base de configuração específica no MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a>IDs de mensagem

|ID da mensagem  |Nome a Apresentar  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventário de Hardware|
|{00000000-0000-0000-0000-000000000002}|Inventário de Software|
|{00000000-0000-0000-0000-000000000003}|Inventário de Descobertas|
|{00000000-0000-0000-0000-000000000010}|Coleção de Ficheiros|
|{00000000-0000-0000-0000-000000000011}|Coleção IDMIF|
|{00000000-0000-0000-0000-000000000021}|Solicitar Tarefas de Máquinas|
|{00000000-0000-0000-0000-000000000022}|Avaliar políticas de máquinas|
|{00000000-0000-0000-0000-000000000023}|Atualizar tarefa de MP padrão|
|{00000000-0000-0000-0000-000000000024}|LS (Serviço de Localização) Tarefa de atualização de locais|
|{00000000-0000-0000-0000-000000000025}|LS Timeout Refresh Task|
|{00000000-0000-0000-0000-000000000026}|Atribuição de Pedido de Agente de Política (Utilizador)|
|{00000000-0000-0000-0000-000000000027}|Atribuição de Avaliação de Agente de Política (Utilizador)|
|{00000000-0000-0000-0000-000000000031}|Relatório de utilização geradora de medição de software|
|{00000000-0000-0000-0000-000000000032}|Mensagem de atualização de fonte|
|{00000000-0000-0000-0000-000000000037}|Limpar a cache de definições de procuração|
|{00000000-0000-0000-0000-000000000040}|Limpeza do agente de política da máquina|
|{00000000-0000-0000-0000-000000000041}|Limpeza do agente de política do utilizador|
|{00000000-0000-0000-0000-000000000042}|Política agente de política validar política / atribuição|
|{00000000-0000-0000-0000-000000000043}|Agente de política validar política de utilizador / atribuição|
|{00000000-0000-0000-0000-000000000051}|Certificados de reexperimentação/refrescante em AD em MP|
|{00000000-0000-0000-0000-000000000061}|Relatório de Estado do DP peer|
|{00000000-0000-0000-0000-000000000062}|Peer DP Pendente agenda de verificação de pacotes|
|{00000000-0000-0000-0000-000000000063}|Atualizações de SUM instalam horário|
|{00000000-0000-0000-0000-000000000101}|Ciclo de recolha de inventário de hardware|
|{00000000-0000-0000-0000-000000000102}|Ciclo de recolha de inventário de software|
|{00000000-0000-0000-0000-000000000103}|Ciclo de recolha de dados discovery|
|{00000000-0000-0000-0000-000000000104}|Ciclo de recolha de ficheiros|
|{00000000-0000-0000-0000-000000000105}|Ciclo de recolha idmif|
|{00000000-0000-0000-0000-000000000106}|Ciclo de relatório de utilização de medição de software|
|{00000000-0000-0000-0000-000000000107}|Ciclo de atualização da lista de fontes do instalador do Windows|
|{00000000-0000-0000-0000-000000000108}|Software atualiza software action software atualiza ciclo de avaliação de atribuições|
|{00000000-0000-0000-0000-000000000109}|Tarefa de manutenção do ponto de distribuição do ponto de distribuição do ponto de manutenção do PDP|
|{00000000-0000-0000-0000-000000000110}|Política dCM|
|{00000000-0000-0000-0000-000000000111}|Enviar Mensagem estatal não enviada|
|{00000000-0000-0000-0000-000000000112}|Limpeza de cache de política do sistema estatal|
|{00000000-0000-0000-0000-000000000113}|Atualizar a política de origem|
|{00000000-0000-0000-0000-000000000114}|Atualizar a política da loja|
|{00000000-0000-0000-0000-000000000115}|A granel da política do sistema estatal envia alto|
|{00000000-0000-0000-0000-000000000116}|A granel da política do sistema estatal envia baixo|
|{00000000-0000-0000-0000-000000000121}|Ação política do gestor de aplicações|
|{00000000-0000-0000-0000-000000000122}|Ação política de utilizador do gestor de aplicações|
|{00000000-0000-0000-0000-000000000123}|Ação de avaliação global do gestor de aplicações|
|{00000000-0000-0000-0000-000000000131}|Resumo de arranque de gestão de energia|
|{00000000-0000-0000-0000-000000000221}|Reavaliar a implementação do ponto final|
|{00000000-0000-0000-0000-000000000222}|Reavaliar a política do ponto final AM|
|{00000000-0000-0000-0000-000000000223}|Deteção externa de eventos|



