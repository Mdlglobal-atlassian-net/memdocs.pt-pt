---
title: Introdução às atualizações de software
titleSuffix: Configuration Manager
description: Saiba o básico das atualizações de software no Gestor de Configuração.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: c857997bdbeed51286e874dcbecf00b414dfe6a0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717644"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Introdução a atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As atualizações de software no Gestor de Configuração fornecem um conjunto de ferramentas e recursos que podem ajudar a gerir a complexa tarefa de rastrear e aplicar atualizações de software a computadores clientes na empresa. É necessário um processo de gestão de atualizações de software eficaz para manter a eficiência operacional, ultrapassar problemas de segurança e manter a estabilidade da infraestrutura de rede. No entanto, devido à natureza evolutiva da tecnologia e ao aparecimento contínuo de novas ameaças de segurança, a gestão eficiente das atualizações de software exige uma atenção consistente e contínua.  

Para um cenário de exemplo que mostra como pode implementar atualizações de software no seu ambiente, consulte o [cenário exemplo para implementar atualizações](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md)de software de segurança .  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a>Sincronização de atualizações de software  
 As atualizações de software sincronizam-se no 'Gestor de Configuração' conecta-se ao Microsoft Update para recuperar metadados de atualizações de software. O site de alto nível (site de administração central ou site primário autónomo) sincroniza com o Microsoft Update numa programação ou quando começa manualmente a sincronização a partir da consola do Gestor de Configuração. Quando o Gestor de Configuração termina as atualizações de software no site de alto nível, as atualizações de software iniciam sincronização em sites infantis, caso existam. Quando a sincronização estiver concluída em todos os sites primários ou secundários, será criada uma política ao nível do site que fornecerá aos computadores cliente a localização dos pontos de atualização de software.  

> [!NOTE]  
>  As atualizações de software estão ativadas por predefinição nas definições de cliente. No entanto, se definir a definição de cliente **Ativar atualizações de software nos clientes** para **Não** para desativar as atualizações de software numa coleção ou nas predefinições, a localização dos pontos de atualização de software não é enviada aos clientes associados. Para mais detalhes, consulte as definições do cliente de atualizações de [software.](../../core/clients/deploy/about-client-settings.md#software-updates)  

 Após o cliente receber a política, o cliente inicia uma verificação da compatibilidade das atualizações de software e escreve as informações no Windows Management Instrumentation (WMI). As informações de compatibilidade são depois enviadas para o ponto de gestão que, por sua vez, as envia para o servidor do site. Para mais informações sobre a avaliação de compatibilidade, consulte a secção [Software updates compliance assessment](#BKMK_SUMCompliance) deste tópico.  

 Pode instalar vários pontos de atualização de software num site primário. O primeiro ponto de atualização de software instalado é configurado como origem de sincronização. Isto sincroniza a partir do Microsoft Update ou de um servidor WSUS que não está na hierarquia do Gestor de Configuração. Os outros pontos de atualização de software do site utilizam o primeiro ponto de atualização de software como origem de sincronização.  

> [!NOTE]  
>  Quando o processo de sincronização de atualizações de software estiver concluído no site de nível superior, os metadados de atualizações de software são replicados para os sites subordinados através de replicação de base de dados. Quando liga uma consola do Gestor de Configuração ao site infantil, o Gestor de Configuração apresenta os metadados de atualizações de software. No entanto, até instalar e configurar um ponto de atualização de software no site, os clientes não procurarão a conformidade com as atualizações de software, os clientes não reportarão informações de conformidade ao Gestor de Configuração e não poderá implementar com sucesso atualizações de software.  

### <a name="synchronization-on-the-top-level-site"></a>Sincronização no site de nível superior  
 O processo de sincronização de atualizações de software no site de nível superior obtém no Microsoft Update os metadados de atualizações de software que satisfazem os critérios especificados nas propriedades do Componente do Ponto de Atualização de Software. Os critérios são configurados apenas no site de nível superior.  

> [!NOTE]  
>  Pode especificar um servidor WSUS existente que não esteja na hierarquia do Gestor de Configuração em vez de Microsoft Updates como fonte de sincronização.  

 A lista seguinte descreve os passos básicos do processo de sincronização no site de nível superior:  

1.  A sincronização de atualizações de software é iniciada.  

2.  O Gestor de Sincronização WSUS envia um pedido ao WSUS em execução no ponto de atualização de software para iniciar a sincronização com o Microsoft Update.  

3.  Os metadados de atualizações de software são sincronizados a partir do Microsoft Update e as alterações são inseridas ou atualizadas na base de dados do WSUS.  

4.  Quando a WSUS terminar a sincronização, o WSUS Synchronization Manager sincroniza os metadados de atualizações de software da base de dados wSUS para a base de dados do Gestor de Configuração, e quaisquer alterações após a última sincronização são inseridas ou atualizadas na base de dados do site. Os metadados de atualizações de software são armazenados na base de dados do site como um item de configuração.  

5.  Os itens de configuração de atualizações de software são enviados aos sites subordinados através de replicação de base de dados.  

6.  Quando a sincronização tiver sido concluída com sucesso, o Gestor de Sincronização do WSUS cria a mensagem de estado 6702.  

7.  O Gestor de Sincronização WSUS envia um pedido de sincronização a todos os sites subordinados.  

8.  O Gestor de Sincronização WSUS envia um pedido de cada vez para o WSUS em execução noutros pontos de atualização de software no site. Os servidores WSUS nos outros pontos de atualização de software estão configurados para serem réplicas dos WSUS em execução no ponto de atualização de software predefinido do site.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Sincronização em sites primários e secundários subordinados  
 Durante o processo de sincronização de atualizações de software no site de nível superior, os itens de configuração de atualizações de software são replicados para sites subordinados através de replicação de base de dados. No final do processo, o site de nível superior envia um pedido de sincronização ao site subordinado e este inicia a sincronização do WSUS. A lista seguinte fornece os passos básicos para o processo de sincronização num site primário ou secundário subordinado:  

1.  O Gestor de Sincronização WSUS recebe um pedido de sincronização do site de nível superior.  

2.  A sincronização de atualizações de software é iniciada.  

3.  O Gestor de Sincronização WSUS envia ao WSUS em execução no ponto de atualização de software um pedido para iniciar a sincronização.  

4.  O WSUS em execução no ponto de atualização de software no site subordinado sincroniza os metadados de atualizações de software a partir do WSUS em execução no ponto de atualização de software com o site principal.  

5.  Quando a sincronização tiver sido concluída com sucesso, o Gestor de Sincronização do WSUS cria a mensagem de estado 6702.  

6.  A partir de um site primário, o Gestor de Sincronização WSUS envia um pedido de sincronização a qualquer site secundário subordinado. O site secundário inicia a sincronização de atualizações de software com o site primário principal. O site secundário está configurado como uma réplica do WSUS em execução no site principal.  

7.  O Gestor de Sincronização WSUS envia um pedido de cada vez para o WSUS em execução noutros pontos de atualização de software no site. Os servidores WSUS nos outros pontos de atualização de software estão configurados para serem réplicas dos WSUS em execução no ponto de atualização de software predefinido do site.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Antes de implementar atualizações de software para computadores clientes no 'Gestor de Configuração', inicie uma digitalização para atualizações de software em computadores clientes. Para cada atualização de software, é criada uma mensagem de estado que contém o estado de compatibilidade da atualização. As mensagens de estado são enviadas em massa para o ponto de gestão e depois para o servidor do site, onde o estado de compatibilidade é introduzido na base de dados do site. O estado de conformidade para atualizações de software é apresentado na consola 'Gestor de Configuração'. É possível implementar e instalar atualizações de software em computadores que necessitem das atualizações. As secções seguintes fornecem informações sobre os estados de compatibilidade e descrevem o processo de análise de compatibilidade das atualizações de software.  

### <a name="software-updates-compliance-states"></a>Estados de compatibilidade das atualizações de software  
 As seguintes listas e descreve cada estado de conformidade que é apresentado na consola Do Gestor de Configuração para atualizações de software.  

-   **Necessário**  

     Especifica que a atualização de software é aplicável e necessária no computador cliente. Qualquer uma das seguintes condições poderá ser verdadeira quando o estado de atualização de software for **Necessária**:  

    -   A atualização de software não foi implementada para o computador cliente.  

    -   A atualização de software foi instalada no computador cliente. No entanto, a mensagem de estado mais recente ainda não foi inserida na base de dados do servidor do site. O computador cliente volta a analisar a atualização após a conclusão da instalação. Pode existir um atraso máximo de dois minutos para que o cliente envie o estado atualizado para o ponto de gestão, que depois reencaminha o estado atualizado para o servidor do site.  

    -   A atualização de software foi instalada no computador cliente. No entanto, a instalação da atualização de software necessita de um reinício do computador para que a atualização seja concluída.  

    -   A atualização de software foi implementada no computador cliente, mas ainda não foi instalada.  

-   **Não Necessária**  

     Especifica que a atualização de software não é aplicável no computador cliente. Por conseguinte, a atualização de software não é necessária.  

-   **Instalada**  

     Especifica que a atualização de software é aplicável no computador cliente e que o computador cliente já tem a atualização de software instalada.  

-   **Desconhecido**  

     Especifica que o servidor do site não recebeu uma mensagem de estado do computador cliente, normalmente por um dos seguintes motivos:  

    -   O computador cliente não analisou com sucesso a compatibilidade das atualizações de software.  

    -   A análise foi concluída com sucesso no computador cliente. No entanto, a mensagem de estado ainda não foi processada no servidor do site, possivelmente devido a uma mensagem de estado pendente.  

    -   A análise foi concluída com sucesso no computador cliente, mas a mensagem de estado não foi recebida do site subordinado.  

    -   A análise foi concluída com sucesso no computador cliente, mas o ficheiro de mensagem de estado estava danificado de alguma forma e não pôde ser processado.  

### <a name="scan-for-software-updates-compliance-process"></a>Análise do processo de compatibilidade de atualizações de software  
 Quando o ponto de atualização do software é instalado e sincronizado, é criada uma política de máquinas a nível do site que informa os computadores clientes de que as atualizações de software do Gestor de Configuração foram ativadas para o site. Quando um cliente recebe a política de computador, é agendada uma análise da avaliação da compatibilidade para ser iniciada aleatoriamente nas duas horas seguintes. Quando a análise é iniciada, um processo do Agente de Cliente de Atualizações de Software limpa o histórico de análise, envia um pedido para localizar o servidor WSUS que deve ser utilizado na análise e atualiza a Política de Grupo local com a localização do servidor WSUS.  

> [!NOTE]  
>  Os clientes baseados na Internet devem ligar ao servidor WSUS utilizando SSL.  

 Um pedido de análise é transmitido ao Windows Update Agent (WUA). O WUA liga-se à localização do servidor WSUS listada na política local, obtém os metadados de atualizações de software que foram sincronizados no servidor WSUS e analisa o computador cliente para a existência de atualizações. Um processo do Agente de Cliente de Atualizações de Software deteta que a análise da compatibilidade terminou e cria mensagens de estado para cada atualização do software que sofreu uma mudança no estado de compatibilidade após a última análise. As mensagens de estado são enviadas para o ponto de gestão em massa, em 15 minutos. Em seguida, o ponto de gestão reencaminha as mensagens de estado para o servidor local, onde as mensagens de estado são inseridas na base de dados do servidor de sites.  

 Depois da análise inicial da compatibilidade das atualizações de software, a análise é iniciada de acordo com o agendamento configurado da análise. No entanto, se o cliente tiver realizado uma análise para a compatibilidade das atualizações de software dentro do prazo temporal indicado pelo valor tempo restante (TTL - Time to Live), o cliente utiliza os metadados de atualizações de software armazenados a nível local. Quando a última análise se situa fora do TTL, o cliente tem de se ligar ao WSUS em execução no ponto de atualização de software e atualizar os metadados de atualizações de software armazenados no cliente.  

 Incluindo o agendamento da análise, a análise para a compatibilidade das atualizações de software pode ser iniciada das seguintes formas:  

-   **Agendamento da análise de atualização de software**: a análise de compatibilidade das atualizações de software inicia-se de acordo com o agendamento da análise configurado nas definições do Agente do Cliente de Atualizações de Software. Para obter mais informações sobre como configurar as definições do cliente de Software Updates, consulte as definições do cliente de atualizações de [software.](../../core/clients/deploy/about-client-settings.md#software-updates)  

-   **Ação Propriedades do Configuration Manager**: o utilizador pode iniciar a ação **Ciclo de pesquisa de atualizações de software** ou a ação **Ciclo de avaliação da implementação de atualizações de software** no separador **Ação** da caixa de diálogo **Propriedades do Configuration Manager** no computador cliente.  

-   **Agendamento de reavaliação da implementação**: a avaliação da implementação e a análise de compatibilidade das atualizações de software iniciam-se de acordo com o agendamento de reavaliação da implementação configurado, o qual está configurado nas definições do Agente do Cliente de Atualizações de Software. Para obter mais informações sobre as definições do cliente de Software Updates, consulte as definições do cliente de atualizações de [software.](../../core/clients/deploy/about-client-settings.md#software-updates)  

-   **Antes da transferência de ficheiros de atualização**: quando um computador cliente recebe uma política de atribuição para uma nova implementação necessária, o Agente do Cliente de Atualizações de Software transfere os ficheiros de atualização de software para a cache do cliente local. Antes de transferir os ficheiros de atualização de software, o agente de cliente inicia uma análise para verificar se a atualização de software é ainda necessária.  

-   **Antes da instalação da atualização de software**: imediatamente antes da instalação da atualização de software, o Agente do Cliente de Atualizações de Software inicia uma análise para verificar se as atualizações de software ainda são necessárias.  

-   **Depois da instalação da atualização de software**: imediatamente depois da instalação de uma atualização de software estar concluída, o Agente do Cliente de Atualizações de Software inicia uma análise para verificar se as atualizações de software deixaram de ser necessárias e cria uma nova mensagem de estado que indica que a atualização de software está instalada. Quando a instalação estiver terminada, mas se for necessário um reinício, a mensagem de estado indica um reinício pendente no computador cliente.  

-   **Após o reinício do sistema**: quando um reinício do sistema no computador cliente está pendente para a instalação da atualização de software terminar, o Agente do Cliente de Atualizações de Software inicia uma análise após o reinício para verificar se a atualização de software deixou de ser necessária e cria uma mensagem de estado que indica que a atualização de software está instalada.  

#### <a name="time-to-live-value"></a>Valor de TTL  
 Os metadados de atualizações de software que são necessários para a análise da compatibilidade das atualizações de software são armazenados no computador cliente local e, por predefinição, são relevantes até um máximo de 24 horas. Este valor é conhecido como o tempo restante (TTL).  

#### <a name="scan-for-software-updates-compliance-types"></a>Análise dos tipos de compatibilidade de atualizações de software  
 O cliente analisa a compatibilidade de atualizações de software utilizando uma análise online ou offline e uma análise forçada ou não forçada, dependendo do modo como a análise da compatibilidade das atualizações de software é iniciada. O seguinte descreve quais os métodos para iniciar a varredura online ou offline e se a varredura é forçada ou não forçada.  

-   **Programação** de atualizações de software (digitalização online não forçada)  

     No agendamento configurado da análise, o cliente liga-se ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software apenas quando a última análise se situou fora do valor TTL.  

-   **Software Updates Scan Cycle** ou **Software Updates Deployment Evaluation Cycle** (varredura on-line forçada)  

     O computador cliente liga-se sempre ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software antes de o computador cliente analisar a compatibilidade das atualizações de software. Uma vez concluída a análise, o contador TTL é reposto. Por exemplo, se o TTL corresponder a 24 horas, após um utilizador iniciar uma análise para a compatibilidade das atualizações de software, o TTL é reposto para 24 horas.  

-   **Programa de reavaliação** de implementação (varredura online não forçada)  

     No agendamento configurado de reavaliação da implementação, o cliente liga-se ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software apenas quando a última análise se situou fora do valor TTL.  

-   **Antes de descarregar ficheiros** de atualização (digitalização online não forçada)  

     Antes de o cliente poder transferir ficheiros de atualização nas implementações necessárias, o cliente liga-se ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software apenas quando a última análise se situou fora do valor TTL.  

-   **Antes da instalação de atualização de software** (digitalização on-line não forçada)  

     Antes de o cliente instalar atualizações de software nas implementações necessárias, o cliente liga-se ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software apenas quando a última análise se situou fora do valor TTL.  

-   **Após a instalação de atualização de software** (exame offline forçado)  

     Depois da instalação de uma atualização de software, o Agente de Cliente de Atualizações de Software inicia uma análise utilizando os metadados locais. O cliente nunca se liga ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software.  

-   **Após o reinício do sistema** (exame offline forçado)  

     Depois da instalação de uma atualização de software e do reinício do computador, o Agente de Cliente de Atualizações de Software inicia uma análise utilizando os metadados locais. O cliente nunca se liga ao WSUS em execução no ponto de atualização de software para obter os metadados de atualizações de software.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Pacotes de implementação de atualização de software  
 Um pacote de implementação de atualização de software é o veículo utilizado para transferir atualizações de software para uma pasta de rede partilhada e copiar os ficheiros de origem de atualização de software para a biblioteca de conteúdos em servidores de sites e em pontos de distribuição que estão definidos na implementação. Utilizando o Assistente para Transferir Atualizações, pode transferir atualizações de software e adicioná-las a pacotes de implementação antes de implementá-las. Este assistente permite-lhe aprovisionar atualizações de software em pontos de distribuição e verificar se esta parte do processo de implementação é bem-sucedida antes de implementar as atualizações de software em clientes.  

 Quando implementa atualizações de software transferidas utilizando o Assistente para Implementar Atualizações de Software, a implementação utiliza automaticamente o pacote de implementação que contém as atualizações de software. Quando são implementadas atualizações de software que não foram transferidas, terá de especificar um pacote de implementação novo ou existente no Assistente para Implementar Atualizações de Software, e as atualizações de software são transferidas quando o assistente termina.  

> [!IMPORTANT]  
>  Tem de criar manualmente a pasta de rede partilhada para os ficheiros de origem do pacote de implementação antes de especificá-la no assistente. Cada pacote de implementação tem de utilizar uma pasta de rede partilhada diferente.  

> [!IMPORTANT]  
>  A conta de computador do Fornecedor de SMS e o utilizador administrativo que transfere verdadeiramente as atualizações de software requerem ambos permissões de **Escrita** para a origem do pacote. Restrinja o acesso à origem do pacote para reduzir o risco de um intruso adulterar os ficheiros de origem das atualizações de software na origem do pacote.  

 Quando é criado um novo pacote de implementação, a versão do conteúdo é definida para 1 antes de serem transferidas quaisquer atualizações de software. Quando os ficheiros de atualização do software são transferidos utilizando o pacote, a versão do conteúdo é aumentada para 2. Portanto, todos os novos pacotes de implementação começam com a versão de conteúdo 2. Sempre que o conteúdo é alterado num pacote de implementação, a versão de conteúdo é aumentada em 1. Para mais informações, consulte [conceitos fundamentais para a gestão de conteúdos.](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)  

 Os clientes instalam atualizações de software numa implementação através da utilização de qualquer ponto de distribuição que tenha as atualizações de software disponíveis, independentemente do pacote de implementação. Mesmo se um pacote de implementação for eliminado para uma implementação ativa, os clientes podem ainda instalar as atualizações de software na implementação desde que cada atualização tenha sido transferida para pelo menos um outro pacote de implementação e esteja disponível num ponto de distribuição ao qual se pode aceder a partir do cliente. Quando é eliminado o último pacote de implementação que contém uma atualização de software, os computadores cliente não conseguem obter a atualização de software até a atualização ser transferida novamente para um pacote de implementação. As atualizações de software aparecem com uma seta vermelha na consola Do Gestor de Configuração quando os ficheiros de atualização não estão em nenhum pacote de implementação. As implementações aparecem com uma seta dupla vermelha se contiverem quaisquer atualizações nesta condição.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a>Fluxos de trabalho de implementação de atualização de software  
 Existem dois cenários principais para implementar atualizações de software no seu ambiente, implementação manual e implementação automática. Normalmente, implementa manualmente as atualizações de software para criar uma linha base para computadores cliente e, de seguida, gere as atualizações de software em clientes utilizando a implementação automática. As secções seguintes fornecem um resumo do fluxo de trabalho para a implementação manual e automática para atualizações de software.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implementação manual de atualizações de software  
 A implementação manual de atualizações de software é o processo de seleção de atualizações de software na consola do Gestor de Configuração e iniciar manualmente o processo de implementação. Normalmente, utiliza este método de implementação para garantir a atualização dos computadores cliente com atualizações de software necessárias antes de criar regras de implementação automática para gerir implementações mensais em curso de atualização de software, e para implementar requisitos de atualização de software fora de banda. A lista seguinte apresenta o fluxo de trabalho geral para a implementação manual de atualizações de software:  

1.  Filtre para atualizações de software que utilizam requisitos específicos. Por exemplo, pode fornecer critérios que obtém todas as atualizações de software de segurança ou críticas que são necessárias em mais de 50 computadores clientes.  

2.  Crie um grupo de atualização de software que contém as atualizações de software.  

3.  Transfira o conteúdo das atualizações de software no grupo de atualização de software.  

4.  Implemente manualmente o grupo de atualização de software.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Implementação automática de atualizações de software  
 A implementação automática de atualizações de software é configurada utilizando uma regra de implementação automática (ADR). Normalmente, utiliza este método de implementação para as atualizações de software mensais (geralmente conhecidas como Patch de Terça-feira) e para gerir atualizações de definição. Quando a regra é executada, as atualizações de software são removidas do grupo de atualização de software (se utilizar um grupo existente), as atualizações de software que cumprem os critérios especificados (por exemplo, todas as atualizações de software de segurança lançadas na última semana) são adicionadas a um grupo de atualização de software, os ficheiros de conteúdos das atualizações de software são transferidos e copiados para pontos de distribuição e as atualizações de software são implementadas em computadores cliente na coleção de destino. A lista seguinte apresenta o fluxo de trabalho geral para a implementação automática de atualizações de software:  

1. Crie uma ADR que especifique as definições de implementação, tais como as seguintes:  

   -   Coleção de destino  

   -   Decida se pretende ativar a implementação ou um relatório sobre a compatibilidade das atualizações de software para os computadores cliente na coleção de destino  

   -   Critérios de atualizações de software  

   -   Agendas de avaliação e implementação  

   -   Experiência de utilizador  

   -   Transferir propriedades  

2. As atualizações de software são adicionadas a um grupo de atualização de software.  

3. O grupo de atualização de software é implementado nos computadores cliente da coleção de destino, se for especificada.  

   Tem de determinar qual a estratégia de implementação a utilizar no seu ambiente. Por exemplo, poderá criar a ADR e ter por alvo uma coleção de clientes de teste. Depois de verificar se as atualizações de software estão instaladas no grupo de teste, pode adicionar uma nova implementação à regra ou alterar a coleção na implementação automática para uma coleção de destino que inclua um conjunto maior de clientes. Os objetos de atualização de software que são criados pelas ADRs são interativos.  

- As atualizações de software que foram implementadas através da utilização de uma ADR são implementadas automaticamente em novos clientes adicionados à coleção de destino.  

- Novas atualizações de software adicionadas a um grupo de atualização de software são implementadas automaticamente aos clientes na coleção de destino.  

- Pode ativar ou desativar implementações em qualquer altura para a ADR.  

  Depois de criar uma ADR, pode adicionar mais implementações à regra. Isto pode ajudá-lo a gerir a complexidade da implementação de diferentes atualizações em diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação e cada nova implementação que adiciona:  

- Utiliza o mesmo grupo e pacote de atualização que é criado com as Regras de Implementação Automática são executadas pela primeira vez  

- Pode especificar uma coleção diferente  

- Suporta propriedades de implementação exclusivas, incluindo:  

  -   Hora de ativação  

  -   Prazo  

  -   Mostra ou oculta experiência do utilizador final  

  -   Separa alertas para esta implementação  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a>Processo de implementação de atualização de software  
 Depois de implementar atualizações de software ou quando uma regra de implementação automática é executada e implementa atualizações de software, é adicionada uma política de atribuição de política à política da máquina para o site. As atualizações de software são transferidas da localização de transferência, Internet ou pasta de rede partilhada, para a origem do pacote. As atualizações de software são copiadas da origem do pacote para a biblioteca de conteúdos no servidor de sites e, em seguida, copiadas para a biblioteca de conteúdos no ponto de distribuição.  

 Quando um computador cliente na coleção de destino da implementação recebe a política da máquina, o Agente do Cliente de Atualização de Software inicia uma pesquisa de avaliação. O agente cliente descarrega o conteúdo para atualizações de software necessárias de um ponto de distribuição para a cache do cliente local no **software disponível** para a implementação e, em seguida, as atualizações de software estão disponíveis para instalar. As atualizações de software de implementações opcionais (implementações que não tenham um prazo de instalação) não são transferidas até que um utilizador inicie manualmente a instalação.  

 Após o prazo configurado, o Agente do Cliente de Atualizações de Software executa uma verificação para verificar se as atualizações de software ainda são necessárias. Em seguida, verifica a cache local do computador cliente para verificar se os ficheiros de origem de atualização de software ainda estão disponíveis. Por fim, o cliente instala as atualizações de software. Se o conteúdo tiver sido eliminado da cache do cliente para criar espaço para outra implementação, o cliente volta a transferir as atualizações de software a partir do ponto de distribuição para a cache do cliente. As atualizações de software são sempre transferidas para a cache do cliente, independentemente do tamanho máximo de cache configurado no cliente. Após a conclusão da instalação, o agente do cliente confirma se as atualizações de software já não são necessárias e, em seguida, envia ao ponto de gestão uma mensagem de estado a indicar que as atualizações de software estão atualmente instaladas no cliente.  

### <a name="required-system-restart"></a>Reinício de sistema necessário  
 Por predefinição, quando as atualizações de software necessárias de uma implementação são instaladas no computador cliente e é necessário um reinício do sistema para concluir a instalação, o reinício do sistema é iniciado. No caso de atualizações de software que tenham sido instaladas antes do prazo, o reinício automático do sistema é adiado até à data limite, a menos que o computador seja, por algum motivo, reiniciado antes dessa data. No caso de servidores e estações de trabalho, o reinício do sistema pode ser suprimido. Estas definições são configuradas na página **Experiência do Utilizador** do Assistente de Implementação de Atualização de Software ou do Assistente de Criação de Regra de Atualizações Automáticas.  

### <a name="deployment-reevaluation-cycle"></a>Ciclo de reavaliação de implementações  
 Por predefinição, os computadores cliente iniciam um ciclo de reavaliação de implementações com intervalos de 7 dias. Durante este ciclo de avaliação, o computador cliente verifica a existência de atualizações de software que tenham sido anteriormente implementadas e instaladas. Se existirem atualizações de software em falta, as atualizações de software serão reinstaladas a partir da cache local. Se uma atualização de software já não estiver disponível na cache local, será transferida a partir de um ponto de distribuição e, em seguida, instalada. Pode configurar a agenda de reavaliação na página **Atualizações de Software** das definições de cliente do site.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a>Suporte para dispositivos incorporados windows que usam filtros de escrita  
 Ao implementar atualizações de software em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar se pretende desativar o filtro de escrita no dispositivo durante a implementação e reiniciar o dispositivo após a implementação. Se o filtro de escrita não estiver desativado, o software será implementado numa sobreposição temporária e deixará de ser instalado quando o dispositivo for reiniciado, a menos que outra implementação force a persistência das alterações.  

> [!NOTE]  
>  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Desta forma, poderá gerir a desativação e a ativação do filtro de escrita, bem como o reinício do dispositivo.  

 A definição de experiência de utilizador que controla o comportamento do filtro de escrita consiste numa caixa de verificação designada **Confirmar alterações dentro do prazo ou durante a janela de manutenção (requer reinicialização)**.  

 Para obter mais informações sobre como o Gestor de Configuração gere dispositivos incorporados que utilizam filtros de escrita, consulte o Planeamento para a implementação do [cliente em dispositivos Incorporados](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)pelo Windows .  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Expandir atualizações de software no Configuration Manager  
 Utilize o System Center Updates Publisher para gerir atualizações de software que não estão disponíveis a partir do Microsoft Update. Depois de publicar as atualizações de software no servidor de atualizações e sincronizar as atualizações de software no 'Gestor de Configuração', pode implementar as atualizações de software para clientes do Gestor de Configuração. Para mais informações sobre updates Publisher, consulte [Updates Publisher 2011](https://go.microsoft.com/fwlink/p/?LinkId=252947).  

## <a name="next-steps"></a>Passos seguintes
[Plano para atualizações de software](../plan-design/plan-for-software-updates.md)
