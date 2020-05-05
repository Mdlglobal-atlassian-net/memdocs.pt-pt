---
title: Monitorizar o estado do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como monitorizar a Proteção de Pontos Finais na sua hierarquia do Gestor de Configuração.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722278"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Como monitorizar o estado de proteção do ponto final

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode monitorizar a Proteção de Pontos Finais na hierarquia do Microsoft Configuration Manager utilizando o nó de **proteção** do ponto final sob **segurança** no espaço de trabalho de **monitorização,** o nó **de proteção de pontofinal** no espaço de trabalho **de Ativos e Compliance** e utilizando relatórios.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a>Como monitorizar a proteção do ponto final utilizando o nó de proteção do ponto final  

1. Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2. No espaço de trabalho **de monitorização,** expanda **a Segurança** e, em seguida, clique no Estado de **Proteção**do Ponto Final .  

3. Na lista **de Recolha,** selecione a recolha para a qual pretende visualizar informações sobre o estado.  

   > [!IMPORTANT]
   >  As coleções estão disponíveis para seleção nos seguintes casos:  
   > 
   > - Quando selecionar, ver esta recolha no painel de **proteção endpoint** no separador **Alertas** da caixa de diálogo<nome de <em>\>recolha</em>**Propriedades.**  
   >   -   Quando implementa uma política antimalware Endpoint Protection para a recolha.  
   >   -   Quando ativa e implementa as definições do cliente endpoint Protection para a recolha.  

4. Reveja as informações que são exibidas nas secções do Estado de **Segurança** e **do Estado Operacional.** Pode clicar em qualquer ligação de estado para criar uma coleção temporária no nó **Dispositivos** da área de trabalho **Ativos e Compatibilidade** . A coleção temporária contém os computadores com o estatuto selecionado.  

   > [!IMPORTANT]  
   >  A informação que é exibida no nó de Status de **Proteção** do Ponto Final baseia-se nos últimos dados que foram resumidos na base de dados do Gestor de Configuração e que podem não estar presentes. Se pretender obter os dados mais recentes, no separador **Home Page** , clique em **Executar Resumo**ou clique em **Agendar Resumo** para ajustar o intervalo de resumo.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a>Como monitorizar a Proteção de Pontos Finais no Espaço de Trabalho de Ativos e Conformidade  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  No espaço de trabalho **de Ativos e Compliance,** realize uma das seguintes ações:  

    -   Clique em **Dispositivos**. Na lista **Dispositivos** , selecione um computador e, em seguida, clique no separador **Detalhe de Software Maligno** .  

    -   Clique em **Coleções de Dispositivos**. Na lista **Coleções de Dispositivos** , selecione a coleção que contém o computador que pretende monitorizar e, em seguida, no separador **Home Page** , no grupo **Coleção** , clique em **Mostrar Membros**.  

3.  Na lista *de\> nomes de recolha<,* selecione um computador e clique no separador **Malware Detail.**  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a>Como monitorizar a proteção de pontos finais utilizando relatórios  
 Utilize os seguintes relatórios para o ajudar a ver informações sobre a Proteção de Pontofinal na sua hierarquia. Também pode utilizar estes relatórios para ajudar a resolver problemas de proteção de pontos finais. Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte Introdução a [ficheiros](../../core/plan-design/hierarchy/log-files.md)de [reporte](../../core/servers/manage/introduction-to-reporting.md) e registo . Os relatórios de proteção do ponto final estão na pasta Endpoint Protection.  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de Atividade Antimalware**|Apresenta uma descrição geral da atividade antimalware de uma coleção específica.|  
|**Computadores Infetados**|Apresenta uma lista de computadores nos quais seja detetada uma ameaça especificada.|  
|**Principais Utilizadores Por Ameaças**|Apresenta uma lista de utilizadores com o maior número de ameaças detetadas.|  
|**Lista de Ameaças**|Apresenta uma lista de ameaças que foram encontradas numa conta de utilizador especificada.|  

## <a name="malware-alert-levels"></a>Níveis de alerta de malware  
 Utilize a tabela seguinte para identificar os diferentes níveis de alerta de proteção de pontos finais que podem ser apresentados em relatórios ou na consola Do Gestor de Configuração.  

|Nível de alerta|Descrição|  
|-----------------|-----------------|  
|**Falhou**|Endpoint Protection não conseguiu remediar o malware. Verifique os seus registos para obter detalhes do erro.<br /><br /> **Nota:** Para obter uma lista de ficheiros de registo de Configuração e De proteção de pontos finais, consulte a secção "Proteção do Ponto Final" no tópico dos [ficheiros de registo.](../../core/plan-design/hierarchy/log-files.md)|  
|**Removido**|Endpoint Protection removeu com sucesso o malware.|  
|**Em quarentena**|Endpoint Protection moveu o malware para um local seguro e impediu-o de funcionar até o remover ou permitir que este funcionasse.|  
|**Limpo**|O software maligno foi limpo no ficheiro infetado.|  
|**Permitido**|Um utilizador administrativo optou por permitir a execução do software que contém o software maligno.|  
|**Nenhuma ação**|Endpoint Protection não tomou nenhuma ação sobre o malware. Esta situação pode ocorrer se o computador for reiniciado depois de o software maligno ser detetado e o software maligno já não é detetado; por exemplo, se uma unidade de rede mapeada na qual seja detetado software maligno não for religada quando o computador é reiniciado.|  
|**Bloqueado**|Endpoint Protection bloqueou o malware de funcionar. Esta situação pode ocorrer se for encontrado um processo no computador que contém software maligno.|
