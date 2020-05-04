---
title: Replicar a base de dados do monitor
titleSuffix: Configuration Manager
description: Saiba como monitorizar a replicação do Servidor SQL na sua hierarquia do Gestor de Configuração.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 96cce5d4aaa352177b1c24ff78cf15e90ea6e823
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713710"
---
# <a name="monitor-database-replication"></a>Replicar a base de dados do monitor

*Aplica-se a: Gestor de Configuração (ramo atual)*

Monitorize detalhes para a replicação da base de dados com o nó de **replicação** da base de dados no espaço de trabalho de **Monitorização** da consola 'Gestor de Configuração'. Pode monitorizar o estado das ligações de replicação entre os sites. Também mostra a inicialização e replicação de grupos de replicação para o site ao qual se conecta.  

> [!TIP]  
> Embora um nó de **replicação** de base de dados também apareça sob o nó de **Configuração da Hierarquia** no espaço de trabalho **da Administração,** não é possível ver o estado de replicação para ligações de replicação de bases de dados a partir desse local.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Estado da ligação de replicação  

A replicação da base de dados entre sites envolve a replicação de vários conjuntos de informação, *chamados grupos*de replicação . Cada grupo de replicação envia e recebe dados com diferentes prioridades. Por padrão, não é possível modificar os dados contidos num grupo de replicação e a frequência de replicação.  

Quando uma ligação de replicação está ativa, e o seu estado não é falhado ou degradado, todos os grupos replicam-se rapidamente. Se um ou mais grupos não completarem a replicação no período de tempo esperado, o link apresenta-se como *degradado*. As ligações degradadas ainda podem funcionar, mas deve monitorizá-las para se certificar de que voltam ao estado ativo. Investigue-os para garantir que falhas adicionais de degradação ou replicação não ocorram.  

Para cada ligação de replicação, especifique o número de vezes que um grupo reproduz sem sucesso. Após este número de repetições, o site define o estado do link para degradado ou falhado. Mesmo que todos, menos um grupo, se reproduzam com sucesso, o site define o estado do link para degradado ou falhado. Estabelece este estatuto porque o grupo de replicação não consegue completar a replicação no número especificado de tentativas. Para obter mais informações, consulte os limiares de [replicação da Base](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)de Dados .  

Utilize as seguintes informações para compreender o estado das ligações de replicação que possam exigir uma investigação mais aprofundada:  

### <a name="link-is-active"></a>A ligação está ativa

Não foram detetados problemas e existe comunicação através da ligação.

Enquanto um site de pais está a atualizar para uma nova versão, e você vê o estado de ligação do site da criança, o estado de ligação mostra-se ativo. Após a atualização, até que o site da criança esteja na mesma versão do site dos pais, o estado de ligação apresenta-se como ativo quando visualizado a partir do site dos pais. Quando visualizado a partir do site da criança, apresenta-se como sendo configurado.  

### <a name="link-is-degraded"></a>A ligação está degradada

A replicação funciona, mas pelo menos um objeto ou grupo de replicação está atrasado. Monitorize as ligações que estão neste estado. Reveja as informações de ambos os sites no link para obter indicações de que o link pode falhar.

Uma ligação também pode apresentar um estado degradado quando o site que recebe dados replicados não consegue consolidar rapidamente os dados na base de dados. Este comportamento acontece quando grandes volumes de dados se replicam. Por exemplo, implementa uma atualização de software para um grande número de computadores. O site-mãe no link pode levar algum tempo para processar este volume de dados replicados. Um atraso de processamento no site-mãe resulta na definição do estado de ligação para degradar-se até que possa processar com sucesso o atraso dos dados.

### <a name="link-has-failed"></a>A ligação falhou

A replicação não é funcional. É possível que uma ligação de replicação possa recuperar sem mais ações. Para investigar e ajudar a remediar a replicação neste link, utilize o Analisador de Ligações de Replicação (RLA).

Este estado também pode indicar um problema na rede física entre o site principal e o subordinado na ligação de replicação.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a>Monitorizar estado de replicação

Utilize o nó de **replicação** da base de dados no espaço de trabalho **de monitorização** para ver o estado de uma ligação de replicação. Consulte os detalhes sobre a base de dados de cada site no link de replicação. Também pode ver detalhes sobre grupos de replicação. Para visualizar estes detalhes, selecione uma ligação de replicação e, em seguida, selecione o separador apropriado para o estado de replicação que pretende ver.

As seguintes secções dão detalhes sobre os diferentes separadores para o estado de replicação:

### <a name="summary"></a>Resumo

Veja informações de alto nível sobre a replicação de dados do site e dados globais entre os dois sites num link.  

Selecione **Ver relatórios para dados históricos** de tráfego para ver um relatório que mostra detalhes sobre a largura de banda da rede usada por replicação através do link.  

### <a name="parent-site"></a>Site Principal

Relativamente ao site principal de uma ligação de replicação, veja detalhes sobre a base de dados, incluindo:  

- Portas da firewall para o SQL Server  

- Espaço livre em disco  

- Localizações de ficheiros de base de dados  

- Certificados  

### <a name="child-site"></a>Site Subordinado

Relativamente ao site subordinado de uma ligação de replicação, veja detalhes sobre a base de dados, incluindo:  

- Portas da firewall para o SQL Server  

- Espaço livre em disco  

- Localizações de ficheiros de base de dados  

- Certificados  

### <a name="initialization-detail"></a>Detalhes da Inicialização

Veja o estado de inicialização dos grupos que se replicam em toda a ligação. Estas informações podem ajudar a identificar se a inicialização de dados de replicação está em curso ou falhou.  

Utilize estas informações para identificar quando um site pode estar no *modo de interoperabilidade*. O modo de interoperabilidade é quando o site infantil não executa a mesma versão do Gestor de Configuração que o site principal.  

### <a name="replication-detail"></a>Detalhes da Replicação

Veja o estado de replicação de cada grupo que se replica através do link. Utilize estas informações para ajudar a identificar problemas ou atrasos para a replicação de dados específicos. Pode ajudar a determinar os limiares de replicação adequados para esta ligação. Para mais informações, consulte os limiares de [replicação da Base](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)de Dados .  

> [!TIP]  
> Os grupos de replicação de dados do site são enviados apenas do site subordinado para o site principal. Os grupos de replicação de dados globais são replicados em ambas as direções.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a>Analisador de ligação de replicação

O Gestor de Configuração inclui o Analisador de Ligações de **Replicação** (RLA), que utiliza para analisar e reparar problemas de replicação. Utilize o RLA para remediar falhas de ligação quando a replicação falhar. Também é útil quando a replicação deixa de funcionar, mas o site ainda não o reportou como falhado.

Utilize o RLA para remediar problemas de replicação entre os seguintes computadores da hierarquia:  

- Entre um servidor de site e o servidor de base de dados do site  

- Entre o servidor de base de dados de um site e o servidor de base de dados de outro site, também conhecido como replicação intersite  

> [!Note]  
> A direção da falha de replicação não importa.

Executar rLA na consola do Gestor de Configuração ou num pedido de comando:  

- Para correr na consola Do Gestor de Configuração: Vá ao espaço de trabalho **de monitorização** e selecione o nó de replicação da Base de **Dados.** Selecione a ligação de replicação que pretende analisar e, em seguida, na fita, selecione **Replication Link Analyzer**.  

- Para correr a uma solicitação de comando, digite o seguinte comando:`%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

Ao executar rLA, deteta problemas utilizando uma série de regras de diagnóstico e verificações. Vê os problemas que a ferramenta identifica. Quando tem instruções para resolver um problema, exibe-as. Se a RLA conseguir remediar automaticamente um problema, apresenta-lhe essa opção.

Quando o RLA termina, guarda os resultados no seguinte relatório baseado em XML e num ficheiro de registo no ambiente de trabalho do utilizador que executa a ferramenta:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

A RLA para os seguintes serviços enquanto remedia alguns problemas. Reinicia estes serviços quando a reparação está concluída:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Se a RLA não concluir a reparação, reinicie estes serviços no servidor do site, se necessário.  

A RLA regista todas as ações de investigação e remediação para fornecer detalhes adicionais que não exibe no assistente.  

### <a name="rla-prerequisites"></a>Pré-requisitos do RLA

A conta que utiliza para executar RLA deve ter as seguintes permissões:

- Direitos de administrador local em cada computador envolvido na ligação de replicação.

- Direitos de sisadmina em cada base de dados do SQL Server que está envolvido na ligação de replicação.  

> [!Note]  
> A conta não requer uma função específica de segurança da administração baseada em funções de Administração do Gestor de Configuração. Um utilizador administrativo com acesso ao nó de **replicação** da Base de Dados pode executar a ferramenta na consola 'Gestor de Configuração'. Um administrador de sistema com direitos suficientes para cada computador pode executar a ferramenta num pedido de comando.  

### <a name="rla-known-issue"></a>RLA conhecida edição

O RLA gera erros de certificado sQL Server Service Broker (SSB) para sites primários que foram atualizados a partir do System Center 2012 Configuration Manager. Este problema deve-se a alterações nos nomes dos certificados na filial atual do Gestor de Configuração. Pode ignorar com segurança estes erros.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a>Replicação da base de dados de monitorização  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Monitorize o estado de replicação da base de dados site-site-site de alto nível

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.**  

2. Selecione o nó **da Hierarquia** do Local para abrir a vista do Diagrama da **Hierarquia.**  

3. Passe o ponteiro do rato na linha entre os dois locais. Veja o estado da replicação global e de dados do site para estes sites.  

### <a name="monitor-the-status-of-a-replication-link"></a>Monitorizar o estado de uma ligação de replicação

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.**  

2. Selecione o nó de **replicação** da base de dados e, em seguida, selecione a ligação de replicação que pretende monitorizar. Em seguida, selecione o separador apropriado para ver diferentes detalhes sobre o estado de replicação para esse link.  
