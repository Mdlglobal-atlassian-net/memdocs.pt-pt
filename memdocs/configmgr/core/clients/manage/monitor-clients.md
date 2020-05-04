---
title: Monitorizar clientes
titleSuffix: Configuration Manager
description: Obtenha orientações detalhadas sobre como monitorizar os clientes no Gestor de Configuração
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1f31ac96f29fc302e601b8da071b1486f4e7df90
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715348"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Como monitorizar os clientes no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Assim que instalar o cliente do Gestor de Configuração nos dispositivos Windows no seu site, monitorize a sua saúde e atividade na consola 'Gestor de Configuração'.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> Sobre o estado do cliente

O Gestor de Configuração fornece os seguintes tipos de informação como estado do cliente:  

- **Estado on-line**do cliente : O site considera um dispositivo como **on-line** se estiver ligado ao seu ponto de gestão atribuído. Para indicar que o cliente está online, envia mensagens semelhantes a ping para o ponto de gestão. Se o ponto de gestão não receber uma mensagem em cinco minutos, o site considera o cliente **offline**.  

- **Atividade do cliente**: O site considera o cliente **ativo** se tiver comunicado com o Gestor de Configuração nos últimos sete dias. O site considera o cliente **inativo** se não tiver feito as seguintes ações em sete dias:  

    - Atualização de política solicitada  
    - Enviei uma mensagem de batimento cardíaco  
    - Enviado inventário de hardware  

- **Verificação**do cliente : O estado da avaliação periódica que o cliente do Gestor de Configuração executa no dispositivo. A avaliação verifica o dispositivo e pode remediar alguns dos problemas que encontra. Para mais informações, consulte os controlos de [saúde do Cliente.](#BKMK_ClientHealth)  

     Nos dispositivos que executam o Windows 7, a verificação do cliente funciona como uma tarefa agendada. Nas versões posteriores do SISTEMA, a verificação do cliente é de si automática durante a janela de manutenção do Windows.  

     Pode configurar a reparação para não executar em dispositivos específicos, por exemplo, um servidor crítico de negócios. Se houver itens adicionais que pretende avaliar, utilize as definições de conformidade do Gestor de Configuração para monitorizar configurações adicionais. Para obter mais informações sobre as definições de conformidade, consulte [plan para e configure as definições](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)de conformidade .  

- **Desativado**: O site marcou o registo do dispositivo para a eliminação. Este comportamento pode acontecer quando um novo registo para o mesmo dispositivo atribui ao mesmo ou a um local primário diferente numa hierarquia. O site elimina estes dispositivos da próxima vez que executa a tarefa de manutenção do site **Eliminar Dados de DescobertaS Envelhecidas**.<!-- SCCMDocs issue #1418 -->  

- **Obsoleto**: O site descobriu um novo registo de dispositivos com o mesmo ID de hardware, por isso marca o antigo recorde como obsoleto. Os relatórios não contam registos obsoletos do mesmo dispositivo várias vezes. Ainda pode visar políticas para dispositivos obsoletos. Se o site não receber batimentos cardíacos para um registo obsoleto após 90 dias de inatividade, remove o dispositivo obsoleto quando executa a tarefa de manutenção do site **Eliminar Dados obsoletos**de Descoberta de Clientes .


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a>Monitorizar clientes individuais

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Selecione o nó dos **Dispositivos** ou escolha uma coleção em **Coleções de Dispositivos**.  

    Os ícones no início de cada linha indicam o estado on-line do dispositivo:  

    |||  
    |-|-|  
    |![ícone de estado online dos clientes](../../../core/clients/manage/media/online-status-icon.png)|O dispositivo está online|  
    |![ícone de estado offline dos clientes](../../../core/clients/manage/media/offline-status-icon.png)|Dispositivo está offline|  
    |![ícone de estado desconhecido dos clientes](../../../core/clients/manage/media/unknown-status-icon.png)|O estado online é desconhecido|  
    |![cliente não instalado](../../../core/clients/manage/media/client-not-installed.png)|Cliente não está instalado no dispositivo|  

2. Para um estado online mais detalhado, adicione as informações de estado on-line do cliente à vista do dispositivo. Clique no cabeçalho da coluna e selecione os campos de estado on-line que pretende adicionar:

    - **Estado Online**do Dispositivo : Indica se o cliente está atualmente online ou offline. (Este estado é a mesma informação dada pelos ícones.)  

    - **Última Hora Online**: Indica quando o estado online do cliente mudou para online  

    - **Última hora offline** indica quando o estado mudou para offline  

3. Selecione um cliente individual no painel da lista para ver mais estado no painel de detalhes. Estas informações incluem atividade do cliente e estado de verificação do cliente.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a>Painel de saúde do cliente

<!--3599209-->
Implementa atualizações de software e outras aplicações para ajudar a proteger o seu ambiente, mas estas implementações apenas atingem clientes saudáveis. Os clientes do Gestor de Configuração Pouco Saudável afetam negativamente a conformidade geral. Determinar a saúde do cliente pode ser um desafio dependendo do denominador: quantos dispositivos totais devem estar no seu âmbito de gestão? Por exemplo, se descobrir todos os sistemas do Ative Directy, mesmo que alguns desses registos sejam para máquinas aposentadas, este processo aumenta o seu denominador.

A partir da versão 1902, veja um dashboard com informações sobre a saúde dos clientes do Gestor de Configuração no seu ambiente. Veja a saúde do seu cliente, a saúde do cenário e os erros comuns. Filtre a vista por vários atributos para ver eventuais problemas por versões DE SO e cliente.

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir o **estado do Cliente**e selecionar o nó do dashboard de **saúde do Cliente.**

![Screenshot do painel de saúde do cliente](media/3599209-client-health-dashboard.png)

> [!Tip]  
> Não há alterações na ccmeval.  

Por padrão, o dashboard de saúde do cliente mostra clientes online, e clientes ativos nos últimos três dias. Portanto, você pode ver diferentes números neste dashboard do que em outras fontes históricas de saúde do cliente. Por exemplo, outros nós no **Estatuto do Cliente,** ou relatórios na categoria de estado do cliente.

### <a name="filters"></a>Filtros

Na parte superior do painel de instrumentos, há um conjunto de filtros para ajustar os dados apresentados no painel de instrumentos.

- **Recolha**: Por padrão, o painel de instrumentos exibe dispositivos na coleção **All Systems.** Selecione uma recolha de dispositivos da lista para ver a vista para um subconjunto de dispositivos numa coleção específica.  

- **Online/offline**: Por padrão, o painel de instrumentos exibe apenas clientes online. Este estado vem do canal de notificação do cliente que atualiza o estado de um cliente a cada cinco minutos. Para mais informações, consulte sobre o [estado do cliente](monitor-clients.md#bkmk_about).  

- **Dias \# ativos**: Por padrão, o painel de instrumentos exibe clientes que estão ativos nos últimos três dias.  

- **Falha apenas**: Consulte a vista apenas para dispositivos que reportem uma falha de saúde do cliente.  

    > [!Tip]  
    > Utilize este filtro juntamente com a versão cliente e os azulejos da versão OS. Para mais informações, consulte [os azulejos da Versão.](#version-tiles)

### <a name="client-health-percentage"></a>Percentagem de saúde do cliente

Este azulejo mostra a saúde geral do cliente na sua hierarquia.

Um cliente saudável do Gestor de Configuração tem as seguintes propriedades:

- Online  
- Envio ativo de dados  
- Passa todos os controlos de avaliação de saúde do cliente  

Para mais informações, consulte sobre o [estado do cliente](monitor-clients.md#bkmk_about).

Um cliente saudável comunica com sucesso com o site. Informa todos os dados com base nos horários definidos nas definições do cliente.

Selecione um segmento deste gráfico para perfurar até uma visão da lista de dispositivos.

### <a name="version-tiles"></a>Telhas de versão

Existem dois azulejos que mostram a saúde do cliente pela versão cliente do Gestor de Configuração e versão S. Estes azulejos são úteis quando se faz alterações nos filtros, como **apenas falha**. Podem ajudar a realçar se quaisquer problemas são consistentes numa versão específica. Utilize estas informações para ajudá-lo a tomar decisões de upgrade.

Selecione um segmento destes gráficos para perfurar até uma visão da lista de dispositivos.

### <a name="scenario-health"></a>Saúde do cenário

Este gráfico de barras mostra a saúde geral para os seguintes cenários fundamentais:

- Política do cliente
- Descoberta do batimento cardíaco
- Inventário de Hardware
- Inventário de software
- Mensagens de estado

Utilize os seletores para ajustar o foco em cenários específicos na tabela.

Os seguintes dois bares são sempre mostrados:

- **Combinado (Todos)**: a combinação de todos os cenários (E)  
- **Combinado (Qualquer)**: pelo menos um dos cenários (OR)

> [!Tip]  
> A saúde do cenário não se mede a partir da configuração das configurações do cliente. Estes valores podem variar com base no conjunto de políticas resultantes por dispositivo. Utilize os seguintes passos para ajustar os períodos de avaliação para a saúde do cenário:
>
> - Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Status do Cliente.**  
> - Na fita, selecione **Definições**de Estado do Cliente .  
>
> Por predefinição, se um cliente não enviar dados específicos do cenário em **7 dias,** o Gestor de Configuração considera-o pouco saudável para esse cenário.

### <a name="top-10-client-health-failures"></a>Top 10 falhas de saúde dos clientes

Este gráfico lista as falhas mais comuns no seu ambiente. Estes erros vêm do Windows ou do Gestor de Configuração.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a>Monitorize o estado de todos os clientes

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Status do Cliente.** Reveja as estatísticas globais da atividade do cliente e verificação de clientes em todo o site. Altere o âmbito da informação escolhendo uma coleção diferente.  

2. Para aprofundar os detalhes sobre as estatísticas relatadas, escolha o nome das informações reportadas. Por exemplo, clientes Ativos que tenham passado a **verificação do cliente ou sem resultados.** Em seguida, reveja a informação sobre os clientes individuais.  

3. Selecione **Atividade do Cliente** para ver gráficos que mostrem a atividade do cliente no seu site de Configuração.  

4. Selecione **Verificação de Clientes** para ver gráficos que mostrem o estado das verificações do cliente no seu site do Gestor de Configuração.  

    Configure os alertas para notificá-lo quando os resultados do cliente verificarem ou a atividade do cliente descer abaixo de uma percentagem especificada. O site também pode alertá-lo quando a reparação falhar numa percentagem especificada de clientes. Para mais informações, consulte [Como configurar o estado do cliente](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a>Verificações de saúde dos clientes

A verificação do cliente executa as seguintes verificações e reparações:  

|Verificação do Cliente|Ação de remediação|Mais informações|  
|------------------|------------------------|----------------------|  
|Verificar se a verificação do cliente foi executada recentemente|Executar verificação do cliente|Verifica se a verificação do cliente foi executada pelo menos uma vez nos últimos três dias.|  
|Verificar se os pré-requisitos de cliente estão instalados|Instalar os pré-requisitos de cliente|Verifica se os pré-requisitos de cliente estão instalados. Lê o ficheiro ccmsetup.xml na pasta de instalação do cliente para detetar os pré-requisitos.|  
|Teste de integridade do repositório de WMI|Reinstalar o cliente do Gestor de Configuração|Verifica se as entradas de clientes do Gestor de Configuração estão presentes no WMI.|  
|Verificar se o serviço de cliente está em execução|Iniciar o serviço de cliente (Anfitrião de Agente do SMS)|Não existem informações adicionais|  
|Teste do Event Sink de WMI.|Reiniciar o serviço de cliente|Verifique se o sumidouro relacionado com o Evento WMI relacionado com o Gestor de Configuração está perdido|  
|Verificar se o serviço Windows Management Instrumentation (WMI) existe|Sem remediação|Não existem informações adicionais|  
|Verificar se o cliente foi instalado corretamente|Reinstalar o cliente|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço antimalware é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço antimalware está em execução|Iniciar o serviço antimalware|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Windows Update é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço de cliente (Anfitrião de Agente do SMS) é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço Windows Management Instrumentation (WMI) está em execução.|Iniciar o serviço Windows Management Instrumentation|Não existem informações adicionais|  
|Verificar se a base de dados do Microsoft SQL CE está em bom estado de funcionamento|Reinstalar o cliente do Gestor de Configuração|Não existem informações adicionais|  
|Teste de Integridade do WMI do Microsoft Policy Platform|Reparar o Microsoft Policy Platform|Não existem informações adicionais|  
|Verificar que o Microsoft Policy Platform Service existe|Reparar o Microsoft Policy Platform|Não existem informações adicionais|  
|Verificar que o tipo de arranque do Microsoft Policy Platform Service é manual|Repor o tipo de arranque do serviço em manual|Não existem informações adicionais|  
|Verificar se o Serviço de Transferência Inteligente em Segundo Plano existe|Sem remediação|Não existem informações adicionais|  
|Verificar se o tipo de arranque do Serviço de Transferência Inteligente em Segundo Plano é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o tipo de arranque do Serviço de Inspeção de Rede é manual|Repor o tipo de arranque do serviço em manual se estiver instalado|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Windows Management Instrumentation (WMI) é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verifique se o tipo de arranque do serviço Windows Update nos dispositivos Windows 8 é automático ou manual|Repor o tipo de arranque do serviço em manual|Não existem informações adicionais|  
|Verificar se o serviço de cliente (Anfitrião de Agente do SMS) existe.|Sem remediação|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Controlo Remoto do Configuration Manager é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço Controlo Remoto do Configuration Manager está em execução|Iniciar o serviço de controlo remoto|Não existem informações adicionais|  
|Verificar se o serviço proxy de reativação (Proxy de Reativação do ConfigMgr) está em execução|Iniciar o serviço Proxy de Reativação do ConfigMgr|Esta verificação de cliente é executada apenas se a definição de cliente **Gestão de Energia**: **Ativar proxy de reativação** estiver definida como **Sim** em sistemas operativos cliente suportados.|  
|Verificar se o tipo de arranque do serviço proxy de reativação (Proxy de Reativação do ConfigMgr) é automático|Repor o tipo de arranque do serviço Proxy de Reativação do ConfigMgr em automático|Esta verificação de cliente é executada apenas se a definição de cliente **Gestão de Energia**: **Ativar proxy de reativação** estiver definida como **Sim** em sistemas operativos cliente suportados.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Ficheiros de registo de implementação de clientes

Para obter mais informações sobre os ficheiros de registo utilizados pelas operações de implementação e gestão do cliente, consulte [ficheiros De registo](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
