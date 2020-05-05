---
title: Referência para tarefas de manutenção
titleSuffix: Configuration Manager
description: Detalhes para cada uma das tarefas de manutenção do site do Gestor de Configuração
ms.date: 03/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9964834bf3a6bfa8e5c0a0bb70039554134490ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723874"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Referência para tarefas de manutenção no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo lista os detalhes para cada uma das tarefas de manutenção do site do Gestor de Configuração. Cada entrada especifica os tipos do site onde a tarefa está disponível e se está ativada por padrão.

Para mais informações, consulte [Configurar tarefas](maintenance-tasks.md#set-up-maintenance-tasks)de manutenção .  

## <a name="tasks"></a>Tarefas

### <a name="backup-site-server"></a>Servidor do Site de Reserva

Utilize esta tarefa para criar uma cópia de segurança das suas informações críticas para restaurar um site e a base de dados do Gestor de Configuração. Para mais informações, consulte [o site 'Gestor de Configuração'.](backup-and-recovery.md)  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Não ativado|
|Site Secundário|Não disponível|

### <a name="check-application-title-with-inventory-information"></a>Ver título de candidatura com informações de inventário

Use esta tarefa para manter a consistência dos títulos de software entre o inventário de software e o catálogo de Inteligência de Ativos. Para mais informações, consulte Introdução à Inteligência de [Ativos.](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|Site primário|Não disponível|
|Site Secundário|Não disponível|

### <a name="clear-undiscovered-clients"></a>Clientes Claros Não Descobertos

> [!Tip]
> Também pode ver esta tarefa na consola chamada **Clear Install Flag**.

Utilize esta tarefa para remover a bandeira instalada para clientes que não apresentem um registo da Heartbeat Discovery durante o período de Redescoberta do **Cliente.** A bandeira instalada impede a instalação automática de empurrar o cliente para um computador que possa ter um cliente ativo do Gestor de Configuração.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Não ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-application-request-data"></a>Eliminar dados de pedido de pedido de pedido de pedido de pedido de pedido de pedido de

Utilize esta tarefa para eliminar pedidos de aplicação envelhecidos da base de dados. Para mais informações, consulte [Criar e implementar uma aplicação](../../../apps/get-started/create-and-deploy-an-application.md).  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-application-revisions"></a>Eliminar revisões de candidaturas envelhecidas

Utilize esta tarefa para eliminar as revisões de aplicações que já não são referenciadas. Para mais informações, consulte [Como rever e substituir aplicações.](../../../apps/deploy-use/revise-and-supersede-applications.md)

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-client-download-history"></a>Eliminar histórico de descarregamento de clientes envelhecidos

Utilize esta tarefa para eliminar dados históricos sobre a fonte de descarregamento utilizada pelos clientes. O site utiliza informações de fonte de descarregamento para povoar o [dashboard Fontes](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)de Dados do Cliente .

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-client-operations"></a>Eliminar Operações de Cliente Desatualizadas

Utilize esta tarefa para eliminar da base de dados do site todos os dados envelhecidos para operações de clientes. Por exemplo, estes dados incluem as seguintes operações:

- Notificações de clientes envelhecidos ou expirados, como pedidos de descarregamento para máquina ou política de utilizador
- Proteção de Pontofinal, como pedidos de um utilizador administrativo para que os clientes executem uma varredura ou descarreguem definições atualizadas

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-client-presence-history"></a>Eliminar histórico de presença de cliente envelhecido
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Utilize esta tarefa para eliminar informações de histórico sobre o estado online dos clientes registados através da notificação do cliente. Elimina informações para clientes com estatuto mais antigo do que o tempo especificado. Para mais informações, consulte [Como monitorizar os clientes](../../clients/manage/monitor-clients.md).

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Eliminar dados de tráfego de gateway de gestão de nuvem envelhecida

Utilize esta tarefa para eliminar a partir da base de dados do site todos os dados envelhecidos sobre o tráfego que passa através do gateway de [gestão](../../clients/manage/cmg/plan-cloud-management-gateway.md)da nuvem . Estes dados incluem:

- O número de pedidos
- Total de bytes de pedido
- Bytes de resposta total
- Número de pedidos falhados
- Número máximo de pedidos simultâneos

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-cmpivot-results"></a>Eliminar resultados da CMPivot envelhecida

Utilize esta tarefa para eliminar a partir da base de dados do site informações envelhecidas de clientes em consultas CMPivot. Para mais informações, consulte a [CMPivot para obter dados em tempo real](cmpivot.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-collected-files"></a>Eliminar ficheiros recolhidos envelhecidos

Utilize esta tarefa para eliminar a partir da base de dados informações envelhecidas sobre ficheiros recolhidos. Esta tarefa também elimina os ficheiros recolhidos da estrutura de pastas do servidor de site no site selecionado. Por padrão, as cinco cópias mais recentes dos ficheiros recolhidos são armazenadas no servidor do site no **inbox\sinv.box\FileCol** diretório. Para mais informações, consulte [Introdução ao inventário de software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-computer-association-data"></a>Eliminar dados da Associação informática envelhecida

Utilize esta tarefa para eliminar a partir da base de dados dados de dados de dados de associação informática de implementação de SISTEMAS. Estas informações são utilizadas ao restaurar o estado do utilizador durante uma sequência de tarefas. Para mais informações, consulte Gerir o [estado do utilizador](../../../osd/get-started/manage-user-state.md).  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-console-connection-data"></a>Eliminar dados de ligação à consola envelhecida

Esta tarefa elimina dados da base de dados do site sobre as ligações das consolas ao site.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-delete-detection-data"></a>Eliminar dados de deteção envelhecidos

Utilize esta tarefa para eliminar dados envelhecidos da base de dados criada por pontos de vista de extração. Elimina informações antigas sobre a alteração de dados utilizadas por sistemas externos que extraem dados da base de dados.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-device-wipe-record"></a>Eliminar o registo de limpeza de dispositivos envelhecidos

Utilize esta tarefa para eliminar a partir da base de dados dados de dados sobre as ações de limpeza de dispositivos móveis. Para mais informações, consulte [Proteja os dados com limpeza remota, bloqueio ou reset](../../../mdm/deploy-use/wipe-lock-reset-devices.md)da código de acesso .  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-discovery-data"></a>Eliminar Dados de Deteção Desatualizados

Utilize esta tarefa para eliminar dados de descobertas envelhecidos da base de dados. Estes dados podem incluir registos de:

- Descoberta do batimento cardíaco
- Deteção de rede
- Métodos de descoberta de Diretório ativo: Sistema, Utilizador e Grupo

Esta tarefa também remove dispositivos envelhecidos marcados como desativados. Quando esta tarefa é executada num site, os dados associados a esse site são eliminados e essas alterações são replicadas para outros sites. Para mais informações, consulte [a Descoberta de Run.](../deploy/configure/run-discovery.md)

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-distribution-point-usage-stats"></a>Eliminar estatísticas de utilização de pontos de distribuição envelhecidos

Utilize esta tarefa para eliminar da base de dados dados envelhecidos para pontos de distribuição que foram armazenados há mais tempo do que um tempo especificado.  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-enrolled-devices"></a>Eliminar dispositivos matriculados envelhecidos

Utilize esta tarefa para eliminar da base de dados do site os dados envelhecidos sobre dispositivos móveis que não reportaram qualquer informação ao site durante um determinado tempo.

Esta tarefa aplica-se a dispositivos que estão matriculados com o Gestor de Configuração [no local MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md). Para obter mais informações sobre estes dispositivos, consulte [sistemas operativos suportados para clientes e dispositivos.](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Não ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-ep-health-status-history-data"></a>Eliminar dados do histórico do estado de saúde do EP envelhecido

Utilize esta tarefa para eliminar da base de dados informações sobre o estado envelhecido para proteção de pontos finais (EP). Para mais informações, consulte [Como monitorizar a Proteção do Ponto Final](../../../protect/deploy-use/monitor-endpoint-protection.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-exchange-partnership"></a>Eliminar parceria de intercâmbio de idosos

> [!Tip]
> > Também pode ver esta tarefa na consola denominada **Eliminar Dispositivos Envelhecidos Geridos pelo Conector do Servidor de Troca**.

Utilize esta tarefa para eliminar dados envelhecidos sobre dispositivos móveis geridos pelo conector Exchange Server. O site elimina estes dados de acordo com os **dispositivos móveis Ignore que estão inativos por mais de (dias)** definindo no separador **Discovery** das propriedades do conector Do Servidor de Câmbio. Para mais informações, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-inventory-history"></a>Eliminar histórico de inventário envelhecido

Utilize esta tarefa para eliminar dos dados de inventário da base de dados que foram armazenados há mais tempo do que um tempo especificado. Para mais informações, consulte [Como utilizar o Resource Explorer para visualizar](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)o inventário de hardware .

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-log-data"></a>Eliminar dados de registo envelhecidos

Utilize esta tarefa para eliminar a partir da base de dados de dados de dados de registo seleções utilizadas para resolução de problemas. Estes dados não estão relacionados com as operações de componentes do Gestor de Configuração.  

> [!IMPORTANT]  
> Por predefinição, esta tarefa é executada diariamente em cada site. Num site de administração central e sites primários, a tarefa elimina dados com mais de 30 dias. Quando utilizar o SQL Server Express num site secundário, certifique-se de que esta tarefa funciona diariamente e elimina dados que estão inativos durante sete dias.  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|**Site secundário**|Ativado|

### <a name="delete-aged-metering-data"></a>Eliminar dados de medição envelhecida

Utilize esta tarefa para eliminar da base de dados dados envelhecidos para a medição de software que tenha sido armazenada por mais tempo do que um tempo especificado. Para mais informações, consulte a [medição do Software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-metering-summary-data"></a>Eliminar dados sumários de medição envelhecidos

Utilize esta tarefa para eliminar a partir da base de dados dados de dados de resumo envelhecido para a medição de software que tenha sido armazenada por mais tempo do que um tempo especificado. Para mais informações, consulte a [medição do Software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-notification-server-history"></a>Eliminar histórico de servidor de notificação envelhecido

Esta tarefa elimina o histórico de presença de clientes envelhecidos.

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-notification-task-history"></a>Eliminar histórico de tarefas de notificação envelhecida

Utilize esta tarefa para eliminar a partir da base de dados do site informações sobre as tarefas de notificação do cliente. Esta tarefa aplica-se a dados que não foram atualizados há um tempo especificado. Para mais informações, consulte [notificações do Cliente](../../clients/manage/client-notification.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-passcode-records"></a>Eliminar Registos de Código saqueado

Utilize esta tarefa no site de alto nível da sua hierarquia para eliminar dados de reset de código de acesso envelhecidos para dispositivos Windows Phone. Os dados de reset da código de acesso são encriptados, mas incluem o PIN para dispositivos. Por padrão, esta tarefa está ativada e elimina dados que sejam mais antigos do que um dia.  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-replication-data"></a>Eliminar dados de replicação envelhecidos

Utilize esta tarefa para eliminar a partir da base de dados dados de dados sobre a replicação da base de dados entre os sites do Gestor de Configuração. Quando alterar a configuração desta tarefa de manutenção, a configuração é aplicada a cada site aplicável da hierarquia. Para mais informações, consulte [a replicação da base de dados Monitor](monitor-replication.md).  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|**Site secundário**|Ativado|

### <a name="delete-aged-replication-summary-data"></a>Eliminar dados resumos de replicação envelhecida

Utilize esta tarefa para eliminar a partir da base de dados do site dados resumos de replicação envelhecidos quando não foi atualizado por um tempo especificado. Para mais informações, consulte [a replicação da base de dados Monitor](monitor-replication.md).  

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|**Site secundário**|Ativado|

### <a name="delete-aged-status-messages"></a>Eliminar Mensagens de Estado Envelhecido

Utilize esta tarefa para eliminar a partir da base de dados dados de dados de dados de mensagens de estado envelhecidos, tal como configurado nas regras do filtro de estado. Para mais informações, consulte [Monitorize o sistema de estado do Gestor de Configuração](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-threat-data"></a>Eliminar dados de ameaça seleto

Utilize esta tarefa para eliminar a partir da base de dados dados de dados de dados de dados de dados de ameaça de proteção de pontos finais que foram armazenados por mais tempo do que um tempo especificado. Para mais informações, consulte [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-unknown-computers"></a>Eliminar computadores desconhecidos envelhecidos

Utilize esta tarefa para eliminar informações sobre computadores desconhecidos da base de dados do site quando não for atualizada durante um determinado período de tempo. Para mais informações, consulte [Prepare-se para implementações de computadordesconhecidas](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-aged-user-device-affinity-data"></a>Eliminar dados de afinidade do dispositivo de utilizador envelhecido

Utilize esta tarefa para eliminar dados envelhecidos da Affinity do Utilizador da base de dados. Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-duplicate-system-discovery-data"></a>Eliminar dados duplicados de descoberta do sistema

Utilize esta tarefa para eliminar da base de dados do site quaisquer registos duplicados gerados pela descoberta do sistema.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Site de administração central**|Ativado|
|Site primário|Não disponível|
|Site Secundário|Não disponível|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Eliminar registos de pacotes de inscrição a granel expirados do MDM

Utilize esta tarefa para eliminar antigos certificados de inscrição a granel e perfis correspondentes após a expiração do certificado de inscrição. Para mais informações, consulte [Criar perfis](../../../protect/deploy-use/create-certificate-profiles.md)de certificado .

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-inactive-client-discovery-data"></a>Eliminar dados de descoberta de clientes inativos

Utilize esta tarefa para eliminar a partir dos dados de descoberta da base de dados para clientes inativos. O site marca os clientes como inativos quando o cliente é sinalizado como obsoleto e por configurações que são feitas para o estado do cliente.

Esta tarefa opera apenas em recursos que são clientes do Gestor de Configuração. É diferente da tarefa eliminar dados de **descobertas envelhecidas,** que elimina qualquer registo de dados de descoberta seleções envelhecidas. Quando esta tarefa é executada num site, remove os dados da base de dados em todos os sites numa hierarquia. Para mais informações, consulte [Como configurar o estado do cliente](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Quando estiver ativado, configure esta tarefa a um intervalo maior do que o calendário da Descoberta do **Batimento Cardíaco.** Esta configuração permite que os clientes ativos enviem um disco da Heartbeat Discovery para marcar o seu registo de clientes como ativo para que esta tarefa não os elimine.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Não ativado|
|Site Secundário|Não disponível|

### <a name="delete-obsolete-alerts"></a>Eliminar alertas obsoletos

Utilize esta tarefa para eliminar dos alertas expirados da base de dados que tenham sido armazenados há mais tempo do que um tempo especificado. Para mais informações, consulte [Alertas de Utilização e o sistema de estado](use-alerts-and-the-status-system.md).

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-obsolete-client-discovery-data"></a>Eliminar dados obsoletos de descoberta de clientes

Utilize esta tarefa para eliminar registos de clientes obsoletos da base de dados. Um registo que é marcado como obsoleto foi geralmente substituído por um novo recorde para o mesmo cliente. O novo recorde torna-se o registo atual do cliente. Para obter informações sobre a descoberta, consulte [a Descoberta de Run.](../deploy/configure/run-discovery.md)

> [!IMPORTANT]  
> Quando estiver ativado, configure esta tarefa a um intervalo maior do que o calendário da Descoberta do Batimento Cardíaco. Esta configuração permite ao cliente enviar um registo de Heartbeat Discovery que define corretamente o estado obsoleto.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Não ativado|
|Site Secundário|Não disponível|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Eliminar locais e subnets obsoletos de descobertas florestais

Utilize esta tarefa para eliminar dados sobre sites de Directórioactivo, subredes e domínios. Remove dados que o site não descobriu pelo método Ative Directory Forest Discovery nos últimos 30 dias. Esta tarefa remove os dados da descoberta, mas não afeta os limites que cria a partir destes dados de descoberta. Para mais informações, consulte [a Descoberta de Run.](../deploy/configure/run-discovery.md)

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="delete-orphaned-client-deployment-state-records"></a>Eliminar registos estatais de implantação de clientes órfãos

Utilize esta tarefa para expurgar periodicamente a tabela que contém informações do Estado de implantação do cliente. Esta tarefa limpa os registos associados a dispositivos obsoletos ou desativados.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="evaluate-collection-members"></a>Avaliar membros da coleção

Configura a Avaliação de Membros da Coleção como componente do site. Para mais informações, consulte [os componentes do Site.](../deploy/configure/site-components.md)

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="monitor-keys"></a>Teclas de monitor

Utilize esta tarefa para monitorizar a integridade das chaves primárias da base de dados do Gestor de Configuração. Uma chave primária é uma coluna ou uma combinação de colunas que identifica unicamente uma linha. A chave distingue a linha de qualquer outra linha numa tabela de bases de dados do Microsoft SQL Server.

|||
|---------|---------|
|**Site de administração central**|Ativado|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="rebuild-indexes"></a>Índices de Reconstrução

Utilize esta tarefa para reconstruir os índices de base de dados do Gestor de Configuração. Um índice é uma estrutura de base de dados que é criada numa tabela de bases de dados para acelerar a recuperação de dados. Por exemplo, pesquisar uma coluna indexada é muitas vezes muito mais rápido do que procurar uma coluna que não está indexada.

Para melhorar o desempenho, os índices de base de dados do Gestor de Configuração são frequentemente atualizados para permanecer sincronizados com os dados em constante mudança que estão armazenados na base de dados. Esta tarefa:

- Cria índices em colunas de base de dados que são pelo menos 50 por cento únicos
- Quedas de índices em colunas que são menos de 50 por cento únicas
- Reconstrói todos os índices existentes que cumprem os critérios de singularidade dos dados

|||
|---------|---------|
|**Site de administração central**|Não ativado|
|**Site primário**|Não ativado|
|**Site secundário**|Não ativado|

### <a name="summarize-file-usage-metering-data"></a>Resumir dados de medição de utilização de ficheiros

Utilize esta tarefa para resumir os dados de vários registos para a utilização de ficheiros de medição de software num único registo geral. A resumição de dados pode comprimir a quantidade de dados armazenados na base de dados do Gestor de Configuração.

Para resumir os dados de medição de software e conservar o espaço do disco na base de dados, utilize esta tarefa com a tarefa de dados mensais de utilização mensal de medidores de **software Da Resumida.** Para mais informações, consulte a [medição do Software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="summarize-installed-software-data"></a>Resumo dados de software instalados

Use esta tarefa para resumir os dados de informações recolhidas de software de inteligência de ativos através do inventário de hardware para fundir vários registos num único registo geral. A resumição de dados pode comprimir a quantidade de dados armazenados na base de dados do Gestor de Configuração. Para mais informações, consulte as tarefas de manutenção da [Configure Asset Intelligence](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="summarize-monthly-usage-metering-data"></a>Resumo dados mensais de medição de utilização

Utilize esta tarefa para resumir os dados de vários registos para a medição mensal de software num único registo geral. A resumição de dados pode comprimir a quantidade de dados armazenados na base de dados do Gestor de Configuração.

Para resumir os dados de medição de software e para conservar o espaço na base de dados, utilize esta tarefa com a tarefa de utilização de ficheiros de medição de **software Da Sumânida.** Para mais informações, consulte a [medição do Software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="update-application-available-targeting"></a>Atualização aplicação Disponível Targeting

Utilize esta tarefa para que o Gestor de Configuração recalcule o mapeamento de políticas e implementações de aplicações para recursos em coleções. Quando implementa políticas ou aplicações para uma coleção, o Gestor de Configuração cria um mapeamento inicial entre os objetos que implementa e os membros da coleção.

Estes mapeamentos são armazenados numa tabela para referência rápida. Quando uma associação de coleções muda, o site atualiza estes mapeamentos armazenados para refletir essas alterações. No entanto, é possível que estes mapeamentos caiam fora de sincronização. Por exemplo, se o site não processar corretamente um ficheiro de notificação, essa alteração pode não se refletir numa alteração aos mapeamentos. Esta tarefa atualiza esse mapeamento com base na adesão à coleção atual.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|

### <a name="update-application-catalog-tables"></a>Atualizar tabelas de catálogo de aplicações

Utilize esta tarefa para sincronizar o cache de base de dados do site do Catálogo de Aplicações com as informações mais recentes sobre a aplicação. Quando muda a configuração desta tarefa de manutenção, aplica-se a todos os locais primários da hierarquia.  

|||
|---------|---------|
|Site de administração central|Não disponível|
|**Site primário**|Ativado|
|Site Secundário|Não disponível|


## <a name="see-also"></a>Consulte também

[Tarefas de manutenção](maintenance-tasks.md)
