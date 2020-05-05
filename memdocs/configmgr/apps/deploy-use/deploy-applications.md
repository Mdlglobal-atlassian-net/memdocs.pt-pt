---
title: Implementar aplicações
titleSuffix: Configuration Manager
description: Criar ou simular uma implementação de uma aplicação para um dispositivo ou recolha de utilizadores
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075341"
---
# <a name="deploy-applications-with-configuration-manager"></a>Implementar aplicações com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Criar ou simular uma implementação de uma aplicação para um dispositivo ou recolha de utilizadores no Gestor de Configuração. Esta implementação dá instruções ao cliente do Gestor de Configuração sobre como e quando instalar o software.

Antes de poder implementar uma aplicação, crie pelo menos um tipo de implementação para a aplicação. Para mais informações, consulte [Criar aplicações](create-applications.md).

A partir da versão 1906, pode criar um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação. Para mais informações, consulte [Criar grupos](create-app-groups.md)de aplicação .

Também pode simular a implementação de uma aplicação. Esta simulação testa a aplicabilidade de uma implementação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implantação e reporta os resultados no nó de **implantação** do espaço de trabalho **de monitorização.** Para mais informações, consulte [Simular implementações de aplicações](simulate-application-deployments.md).

> [!Note]
> Só pode simular a implementação de aplicações necessárias, mas não pacotes ou atualizações de software.
>
> Os dispositivos matriculados no MDM não suportam implementações simuladas, experiência do utilizador ou definições de agendamento.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a>Implementar uma aplicação

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione o nó de Aplicações ou **Grupos** de **Aplicações.**

2. Selecione um grupo de aplicação ou aplicação da lista para implementar. Na fita, clique em **Implementar**.  

> [!Note]  
> Quando vê as propriedades de uma implantação existente, as seguintes secções correspondem aos separadores da janela de propriedades de implantação:  
>
> - [General](#bkmk_deploy-general)
> - [Conteúdo](#bkmk_deploy-content)
> - [Definições de implementação](#bkmk_deploy-settings)
> - [Agendamento](#bkmk_deploy-sched)
> - [Experiência do Utilizador](#bkmk_deploy-ux)
> - [Alertas](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>Informação **geral** de implantação

Na página **geral** do assistente de software de implantação, especifique as seguintes informações:  

- **Software**: Este valor exibe a aplicação a implementar. Clique em **Navegar** para selecionar uma aplicação diferente.  

- **Recolha**: Clique em **Navegar** para selecionar a coleção para implementar a aplicação para.  

- Utilize grupos de pontos de **distribuição predefinidos associados a esta recolha**: Guarde o conteúdo da aplicação no grupo de pontos de distribuição predefinido da coleção. Se não associou a coleção selecionada a um grupo de pontos de distribuição, esta opção está cinzenta.  

- **Distribua automaticamente o conteúdo para dependências**: Se algum dos tipos de implementação na aplicação tiver dependências, então o site também envia conteúdo de aplicação dependente para pontos de distribuição.  

    >[!Note]  
    > Se atualizar a aplicação dependente após a implementação da aplicação principal, o site não distribui automaticamente nenhum conteúdo novo para a dependência.  

- **Comentários (opcional)**: Opcionalmente, insira uma descrição para esta implementação.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a>Opções **de Conteúdo** de Implementação

Na página **de Conteúdo,** clique em **Adicionar** para distribuir o conteúdo desta aplicação a um ponto de distribuição ou a um grupo de pontos de distribuição.

Se selecionou a opção de utilizar pontos de **distribuição predefinidos associados a esta recolha** na página Geral, então esta opção é automaticamente povoada. Apenas um membro da função de segurança do Administrador de **Aplicação** pode modificá-lo.

Se o conteúdo da aplicação já estiver distribuído, então aparecem aqui.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Definições de implementação**

Na página definições de **implementação,** especifique as seguintes informações:  

- **Ação**: Da lista de desabitadas, escolha se esta implementação é para **instalar** ou **desinstalar** a aplicação.  

    > [!NOTE]  
    > Se criar uma implementação para **instalar** uma aplicação e outra implementação para **desinstalar** a mesma aplicação no mesmo dispositivo, a implementação **de Instalação** tem prioridade.  

    Não podes mudar a ação de um destacamento depois de a criares.  

- **Objetivo**: na lista pendente, escolha uma das seguintes opções:  

  - **Disponível**: O utilizador vê a aplicação no Centro de Software. Podem instalá-lo a pedido.  

  - **Requerido**: O cliente instala automaticamente a aplicação de acordo com o horário que definiu. Se a aplicação não estiver oculta, um utilizador pode rastrear o seu estado de implementação. Também podem usar o Software Center para instalar a aplicação antes do prazo.  

    > [!NOTE]  
    > Quando definir a ação de implantação para **desinstalar,** o objetivo de implantação é automaticamente definido para **O Necessário**. Não podes mudar este comportamento.  

- **Permitir que os utilizadores finais tentem reparar esta aplicação**: A partir da versão 1810, se tiver criado a aplicação com uma linha de comando de reparação, ative esta opção. Os utilizadores vêem uma opção no Centro de Software para **reparar** a aplicação.<!--1357866-->  

- **Pré-implementação do software para o dispositivo principal do utilizador**: Se a implementação for para um utilizador, selecione esta opção para implementar a aplicação no dispositivo principal do utilizador. Esta definição não requer que o utilizador faça o início antes da implementação. Se o utilizador tiver de interagir com a instalação, não selecione esta opção. Esta opção só está disponível quando a implementação for **necessária**.  

- **Enviar pacotes de despertar**: Se a implementação for **necessária,** o Gestor de Configuração envia um pacote de despertar para computadores antes de o cliente eexecutá-lo. Este pacote acorda os computadores no prazo de instalação. Antes de utilizar esta opção, os computadores e as redes devem ser configurados para Wake On LAN. Para mais informações, consulte [Plan como acordar os clientes.](../../core/clients/deploy/plan/plan-wake-up-clients.md)  

- **Permitir que os clientes numa ligação à Internet medido descarreguem conteúdos após o prazo de instalação, o que pode incorrer em custos adicionais**: Esta opção só está disponível para implementações com o propósito de **Exigir**.  

- **Atualize automaticamente qualquer versão supersed desta aplicação**: O cliente atualiza qualquer versão supersed da aplicação com a aplicação de superseding.

    > [!Note]  
    > Esta opção funciona independentemente da aprovação do administrador. Se um administrador já aprovou a versão supersed, não precisa também aprovar a versão de superseding. A aprovação é apenas para novos pedidos, não para superseding upgrades.<!--515824-->  
    >
    > Para a instalação **disponível,** pode ativar ou desativar esta opção. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a>Definições de aprovação

O comportamento de aprovação da aplicação depende se ativa a funcionalidade opcional recomendada, aprovar pedidos de **aplicação para utilizadores por dispositivo**.

- **Um administrador deve aprovar um pedido para esta aplicação no dispositivo**: Se ativar a funcionalidade opcional, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes de o utilizador poder instalá-la no dispositivo solicitado. Se o administrador aprovar o pedido, o utilizador só poderá instalar a aplicação nesse dispositivo. O utilizador deve submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é cinzenta quando o objetivo de implementação é **necessário**, ou quando você implementa a aplicação para uma recolha de dispositivos.

- **Requerer a aprovação do administrador se os utilizadores solicitarem esta aplicação**: Se não ativar a funcionalidade opcional, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes de o utilizador poder instalá-la. Esta opção é cinzenta quando o objetivo de implementação é **necessário**, ou quando você implementa a aplicação para uma recolha de dispositivos.  

Para mais informações, consulte [Aprovar aplicações.](app-approval.md)


#### <a name="deployment-properties-deployment-settings"></a>Implementação de propriedades de **implementação Definições**

Quando visualiza as propriedades de uma implementação, se suportada pela tecnologia do tipo de implementação, aparece no separador Definições de **Implementação:**

**Feche automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa de diálogo**de propriedades do tipo de implementação . Para mais informações, consulte a execução de [ficheiros executáveis antes](#bkmk_exe-check)de instalar uma aplicação .



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a>Definições **de agendamento de implementação**

Na página **de Agendamento,** delineie o momento em que esta aplicação é implementada ou disponível para dispositivos clientes.

Por predefinição, o Gestor de Configuração disponibiliza imediatamente a política de implementação aos clientes. Se quiser criar a implementação, mas não a disponibilizar aos clientes até uma data posterior, configure a opção de **Agendar a aplicação para estar disponível**. Em seguida, selecione a data e a hora, incluindo se é baseado na UTC ou na hora local do cliente.

Se a implantação for **necessária,** especifique também o **prazo de instalação**. Por defeito, este prazo é o mais rápido possível.

Por exemplo, é necessário implementar uma nova aplicação de linha de negócio. Todos os utilizadores precisam de o instalar por um determinado tempo, mas pretende dar-lhes a opção de optar em início. Também precisa de se certificar de que o site distribuiu o conteúdo para todos os pontos de distribuição. Agende a candidatura dentro de cinco dias a partir de hoje. Este horário dá-lhe tempo para distribuir o conteúdo e confirmar o seu estado. Em seguida, estabelece o prazo de instalação para um mês a partir de hoje. Os utilizadores vêem a aplicação no Software Center quando está disponível em cinco dias. Se não fizerem nada, o cliente instala automaticamente a aplicação no prazo de instalação.

Se a aplicação que está a implementar substituir outra aplicação, estabeleça o prazo de instalação quando os utilizadores receberem a nova aplicação. Detete o Prazo de **Instalação** para atualizar os utilizadores com a aplicação supersed.


#### <a name="delay-enforcement-with-a-grace-period"></a>Adiar a aplicação da lei com um período de carência

É melhor dar mais tempo aos utilizadores para instalarem as aplicações necessárias para *além* dos prazos que definirem. Este comportamento é normalmente necessário quando um computador é desligado por um longo período de tempo, e precisa de instalar muitas aplicações. Por exemplo, quando um utilizador regressa de férias, tem de esperar muito tempo enquanto o cliente instala implementações vencidas. Para ajudar a resolver este problema, defina um período de carência de execução.

- Em primeiro lugar, configure este período de carência com o período grace da propriedade para execução após prazo de **implementação (horas)** em configurações do cliente. Para mais informações, consulte o grupo de [agentes](../../core/clients/deploy/about-client-settings.md#computer-agent) informáticos. Especifique um valor entre **1** e **120** horas.  

- Na página de **Agendamento** de uma implementação de aplicação necessária, permita a opção de atrasar a **execução desta implementação de acordo com as preferências do utilizador, até ao período de carência definido nas definições**do cliente . O período de carência de execução aplica-se a todas as implementações com esta opção ativada e direcionada a dispositivos aos quais também implementou a definição do cliente.

Após o prazo, o cliente instala a aplicação na primeira janela não-empresarial, que o utilizador configurava, até este período de carência. No entanto, o utilizador ainda pode abrir o Software Center e instalar a aplicação a qualquer momento. Uma vez expirado o período de graça, a aplicação reverte para o comportamento normal para implementações em atraso.

![Diagrama da linha do tempo do período de graça](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> Na maior parte das vezes, esta funcionalidade aborda o cenário quando o dispositivo é desligado enquanto o utilizador está fora do escritório. Tecnicamente, o período de carência começa quando o cliente obtém a apólice após o prazo de implantação. O mesmo comportamento acontece se parar o serviço de cliente do Gestor de Configuração (CcmExec) e reiniciá-lo em algum momento após o prazo de implementação.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a>Definições de **experiência do utilizador** de implementação

Na página **User Experience,** especifique informações sobre como os utilizadores podem interagir com a instalação da aplicação.

- **Notificações**do utilizador : Especifique se deve apresentar notificação no Centro de Software no momento disponível configurado. Esta definição também controla se notifica os utilizadores nos computadores dos clientes. Para as implementações disponíveis, não é possível selecionar a opção de Ocultar no Centro de **Software e todas as notificações.**  

    - **Quando forem necessárias alterações de software, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torradas**<!--3555947-->: A partir da versão 1902, selecione esta opção para alterar a experiência do utilizador para ser mais intrusiva. Aplica-se apenas às implementações necessárias. Para mais informações, consulte [Plan for Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Instalação de software** e **reinício**do sistema : Configure apenas estas definições para as implementações necessárias. Especificam os comportamentos quando a implementação atinge o prazo fora de quaisquer janelas de manutenção definidas. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Escreva o manuseamento do filtro para dispositivos Incorporados**do Windows : Esta definição controla o comportamento de instalação em dispositivos Incorporados do Windows que estão ativados com um filtro de escrita. Escolha a opção de cometer alterações no prazo de instalação ou durante uma janela de manutenção. Quando selecionar esta opção, é necessário reiniciar e as alterações persistem no dispositivo. Caso contrário, a aplicação é instalada na sobreposição temporária, e comprometida posteriormente.  

    - Quando implementar uma atualização de software para um dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção e dispositivos Incorporados pelo Windows, consulte [Create Windows Embedded aplicações](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>**Alertas** de Implantação

Na página **Alerts,** configure como o Gestor de Configuração gera alertas para esta implementação. Se também estiver a utilizar o System Center Operations Manager, configure também os seus alertas. Só é possível configurar alguns alertas para as implementações necessárias. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a>Criar uma implantação faseada

<!--1358147-->
A partir da versão 1806, criar uma implementação faseada para uma aplicação. As implementações faseadas permitem-lhe orquestrar um lançamento coordenado e sequenciado de software com base em critérios e grupos personalizáveis. Por exemplo, implemente a aplicação para uma coleção piloto e, em seguida, continue automaticamente o lançamento com base em critérios de sucesso.

Para obter mais informações, veja os artigos seguintes:  

- [Criar uma implementação faseada](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerir e monitorizar as implementações faseadas](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a>Eliminar uma implantação

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione o nó de Aplicações ou **Grupos** de **Aplicações.**  

2. Selecione a aplicação ou grupo de aplicação que inclui a implementação que pretende eliminar.  

3. Mude para o separador **de implementação** do painel de detalhes e selecione a implementação.  

4. Na fita, no separador **De implantação** e no grupo **de implantação,** clique em **Eliminar**.  

Ao eliminar uma implementação de aplicação, quaisquer casos da aplicação que os clientes já instalaram não são removidos. Para remover estas aplicações, implemente a aplicação para computadores para **desinstalar**. Se eliminar uma implementação de aplicação ou remover um recurso da recolha para a qual está a implementar, a aplicação já não é visível no Software Center.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a>Notificações dos utilizadores para implementações necessárias

Quando os utilizadores recebem o software necessário, e selecione o **Snooze e lembre-me** a definição, eles podem escolher entre as seguintes opções:  

- **Posteriormente**: Especifica que as notificações são agendadas com base nas definições de notificação configuradas nas definições do cliente.  

- **Tempo fixo**: Especifica que a notificação está programada para ser exibida novamente após a hora selecionada. Por exemplo, se selecionar 30 minutos, a notificação volta a ser exibida em 30 minutos.  

![Grupo de agente de computador nas definições padrão do cliente](media/ComputerAgentSettings.png)

O tempo máximo de soneca é sempre baseado nos valores de notificação configurados nas definições do cliente em cada momento ao longo da linha temporal de implementação. Por exemplo:  

- Configura o prazo de implantação superior a **24 horas, lembre os utilizadores de todas as (horas)** de definição na página do Agente **Informático** durante 10 horas.  

- O cliente exibe o diálogo de notificação mais de 24 horas antes do prazo de implementação.  

- O diálogo mostra opções de soneca até, mas nunca superiores a 10 horas.  

- À medida que o prazo de implementação se aproxima, o diálogo mostra menos opções. Estas opções são consistentes com as configurações relevantes do cliente para cada componente da linha temporal de implementação.  

Para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é mais intrusiva. Em vez de uma notificação transitória da barra de tarefas, uma caixa de diálogo como os seguintes ecrãs cada vez que é notificado de que é necessária uma manutenção crítica do software:

![O diálogo de software necessário o notifica da manutenção crítica do software](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a>Verifique se executa ficheiros executáveis

Configure uma implementação para verificar se determinados ficheiros executáveis estão a ser executados no cliente. Utilize esta opção para verificar se há processos que possam perturbar a instalação da aplicação. Se um destes ficheiros executáveis estiver em execução, o cliente bloqueia a instalação do tipo de implementação. O utilizador deve fechar o ficheiro executável em execução antes de o cliente poder instalar o tipo de implementação. Para implementações com o propósito necessário, o cliente pode fechar automaticamente o ficheiro executável em execução.

1. Abra a caixa de diálogo **Properties** para o tipo de implantação.  

2. Mude para o separador **'Instalar Comportamento'** e clique em **Adicionar**.  

3. Na caixa de diálogo **Add Executable File,** introduza o nome do ficheiro executável do alvo. Opcionalmente, insira um nome amigável para a aplicação para ajudá-lo a identificá-lo na lista.  

4. Clique **OK**e, em seguida, clique em **OK** para fechar a janela de propriedades do tipo de implementação.  

5. Quando implementar a aplicação, selecione a opção de **fechar automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa**de diálogo do tipo de implementação . Esta opção está no separador Definições de **Implementação** das propriedades de implementação.  

> [!Note]
> Se configurar uma aplicação para verificar se executa ficheiros executáveis e incluí-lo na etapa de sequência de tarefas [de instalação,](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) a sequência de tarefas não o instalará. Se não configurar este passo de sequência de tarefas para continuar com o erro, então toda a sequência de tarefas falha.

### <a name="client-behaviors-and-user-notifications"></a>Comportamentos do cliente e notificações dos utilizadores

Após a receção dos clientes, aplica-se o seguinte comportamento:  

- Se implementou a aplicação como **disponível**, e um utilizador tentar instalá-la, o cliente solicita ao utilizador que feche os ficheiros executáveis de execução especificados antes de prosseguir com a instalação.  

- Se implementou a aplicação como **necessário,** e especificado para **fechar automaticamente quaisquer executáveis de execução especificados no separador de comportamento de instalação da caixa**de diálogo de propriedades do tipo de implementação, então o cliente apresenta uma notificação. Informa o utilizador de que os ficheiros executáveis especificados são automaticamente fechados quando o prazo de instalação da aplicação é atingido.  

    - Agende estes diálogos no grupo de definições do cliente do **Agente Informático.** Para mais informações, consulte [o agente informático.](../../core/clients/deploy/about-client-settings.md#computer-agent)  

    - Se não quiser que o utilizador veja estas mensagens, selecione a opção de ocultar no Centro de **Software e todas as notificações** no separador User **Experience** das propriedades da implementação. Para mais informações, consulte [as definições](#bkmk_deploy-ux)da Experiência do Utilizador de Implementação .  

- Se implementou a aplicação como **necessário**, e não especificou para **fechar automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa**de diálogo de propriedades do tipo de implementação, então a instalação da aplicação falha se uma ou mais das aplicações especificadas estiverem em execução.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implementar aplicações disponíveis para utilizadores em dispositivos ligados à AD Azure

<!-- 1322613 -->
Se implementar aplicações como disponível para os utilizadores, podem navegar e instalá-las através do Software Center nos dispositivos Azure Ative Directory (Azure AD).  

### <a name="prerequisites"></a>Pré-requisitos

- Ativar HTTPS no ponto de gestão  

- Integrar o site com [AD Azure](../../core/servers/deploy/configure/azure-services-wizard.md) para **gestão** de nuvem  

    - Configure [Descoberta de Utilizador aD Azure](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Implementar uma aplicação disponível para uma coleção de utilizadores da Azure AD  

- Distribua qualquer conteúdo de aplicação para um ponto de [distribuição na nuvem](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- Ativar a definição do cliente **Utilize o novo Centro** de Software no grupo de agentes [informáticos](../../core/clients/deploy/about-client-settings.md#computer-agent)  

- O cliente OS deve ser o Windows 10, e juntou-se ao Azure AD. Quer como puramente cloud-joined domínio, ou híbrido Azure AD-joined.  

- Para apoiar clientes baseados na Internet:  

    - [Gateway de gestão da cloud](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - Ativar a definição do cliente: **Ativar pedidos de política de utilizador de clientes da Internet** no grupo Política de [Clientes](../../core/clients/deploy/about-client-settings.md#client-policy)  

- Para apoiar os clientes na intranet:  

    - Adicione o ponto de distribuição da nuvem a um grupo de fronteira saturado utilizado pelos clientes  

    - Os clientes devem resolver o nome de domínio totalmente qualificado (FQDN) do ponto de gestão ativado por HTTPS  



## <a name="next-steps"></a>Passos seguintes

- [Monitorizar aplicações](monitor-applications-from-the-console.md)
- [Resolver problemas de implementação de aplicações](troubleshoot-application-deployment.md)
- [Tarefas de gestão de candidaturas](management-tasks-applications.md)
- [Manual do utilizador do Software Center](../../core/understand/software-center.md)
