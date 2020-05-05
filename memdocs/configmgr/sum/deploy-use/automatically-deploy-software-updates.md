---
title: Implementar automaticamente atualizações de software
titleSuffix: Configuration Manager
description: Implemente automaticamente atualizações de software utilizando regras de implementação automáticas (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: eca3227a023561a099804ef0928bfee7a7aff2c6
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110445"
---
#  <a name="automatically-deploy-software-updates"></a>Implementar automaticamente atualizações de software  

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize uma regra de implementação automática (ADR) em vez de adicionar novas atualizações a um grupo de atualização de software existente. Normalmente, utiliza ADRs para implementar atualizações mensais de software (também conhecidas como atualizações "Patch Tuesday") e para gerir atualizações de definição de definição de Proteção de Pontofinal. Se precisar de ajuda para determinar qual o método de implementação certo para si, consulte as atualizações de [software de implementação](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a>Criar uma regra de implementação automática (ADR)  
Aprove e implemente automaticamente atualizações de software utilizando um ADR. A regra pode adicionar atualizações de software a um novo grupo de atualização de software cada vez que a regra corre, ou adicionar atualizações de software a um grupo existente. Quando uma regra é executado e adiciona atualizações de software a um grupo existente, a regra remove todas as atualizações do grupo. Em seguida, adiciona ao grupo as atualizações que satisfazem os critérios que define. 

> [!WARNING]  
>  Antes de criar um ADR pela primeira vez, verifique se o site completou a sincronização de atualizações de software. Este passo é importante quando executa o Gestor de Configuração com uma língua não inglesa. As classificações de atualização de software são apresentadas em inglês antes da primeira sincronização e, em seguida, exibidas nas línguas localizadas após a sincronização da atualização de software. As regras que cria antes de sincronizar atualizações de software podem não funcionar corretamente após a sincronização, porque a cadeia de texto pode não corresponder.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a>Processo para criar um ADR  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e selecione o nó de Regras de **Implementação Automática.**  

2.  Na fita, clique em Criar regra de **implementação automática**.  

3.  Na página **geral** do Assistente de Regra de Implementação Automática, configure as seguintes definições:  

    -   **Nome**: especifique o nome para a ADR. O nome deve ser único, ajudar a descrever o propósito da regra, e identificá-lo de outros no site do Gestor de Configuração.  

    -   **Descrição**: especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implantação e de outras informações relevantes que ajudem a diferenciar a regra dos outros. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Modelo**: Selecione um modelo de implementação para especificar se aplicar configurações ADR previamente guardadas. Configure um modelo de implementação contendo múltiplas propriedades comuns de implementação de atualizações que pode usar ao criar ADRs adicionais. Estes modelos poupam tempo e ajudam a garantir a consistência em implementações semelhantes. Selecione entre um dos seguintes modelos de implementação de atualização de software incorporado:  

         - O modelo **Patch Terça** fornece definições comuns a utilizar quando implementa atualizações de software num ciclo mensal.  

         - O modelo de Atualizações de **Clientes do Office 365** fornece configurações comuns para usar quando implementa atualizações para clientes Do Office 365 Pro Plus.
             > [!Note]
             > A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Se os seus ADRs dependerem da propriedade "Title", terá de editá-lo a partir de 9 de junho de 2020. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)`é um exemplo do novo título. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).

         - O modelo **de atualizações antivírus SCEP e Windows Defender** fornece configurações comuns para usar quando implementa atualizações de definição de proteção de pontofinal.  

    -   **Coleção**: especifica a coleção de destino a utilizar na implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   Especifique se pretende adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, opte por criar um novo grupo de atualização de software quando o ADR funciona. Se a regra for de acordo com um horário mais agressivo, poderá optar por utilizar um grupo existente. Por exemplo, se executar a regra diariamente para atualizações de definição, então poderá adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Ativar a implementação após a execução desta regra**: especifique se pretende ativar a implementação da atualização de software após a execução da ADR. Considere as seguintes opções para esta definição:  

        -   Quando ativa a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo da atualização de software é descarregado conforme necessário. O conteúdo é copiado para os pontos de distribuição especificados, e as atualizações são implementadas para os clientes na coleção-alvo.  

        -   Quando não permite a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de implementação de atualização de software é descarregado, se necessário, e distribuído para os pontos de distribuição especificados. O site cria uma implementação desativada no grupo de atualização de software para evitar que as atualizações sejam implementadas para os clientes. Esta opção proporciona tempo para se preparar para implementar as atualizações, verificar se as atualizações que satisfaçam os critérios são adequadas e, em seguida, ativar a implementação.  

4.  Na página Definições de **Implementação,** configure as seguintes definições:  

    -   **Use o Wake on LAN para acordar os clientes para as implementações necessárias**: Especifica se permite ativar o Wake On LAN no prazo. Wake On LAN envia pacotes de despertar para computadores que requerem uma ou mais atualizações de software na implementação. O site acorda todos os computadores que estão em modo de sono no prazo de instalação para que a instalação possa iniciar. Os clientes que estão em modo de sono que não necessitam de atualizações de software na implementação não foram iniciados. Por predefinição, esta definição não está ativada. Antes de utilizar esta opção, configure computadores e redes para Wake On LAN. Para mais informações, consulte [Como configurar Wake On LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens estatais de execução de atualização que são reportadas pelos clientes.  

        > [!IMPORTANT]  
        >  Quando implementar atualizações de definição, detete o nível de detalhe para **O Erro apenas** para que o cliente reporte uma mensagem de estado apenas quando uma atualização de definição falhar. Caso contrário, o cliente relata um grande número de mensagens estatais que podem afetar o desempenho do servidor do site.  
        
        > [!NOTE]  
        > O nível de erro **apenas** não envia as mensagens de estado de execução necessárias para rastrear reboots pendentes.

    -   **Definição de termos de licenciamento**: especifique se pretende implementar automaticamente as atualizações de software com termos de licenciamento associados. Algumas atualizações de software incluem termos de licença. Quando implementa automaticamente atualizações de software, os termos da licença não são apresentados e não existe uma opção para aceitar os termos da licença. Opte por implementar automaticamente todas as atualizações de software independentemente de um termo de licença associado, ou apenas implementar atualizações que não tenham termos de licença associados.  

         - Para rever os termos da licença para uma atualização de software, selecione a atualização de software no nó all **software Updates** do espaço de trabalho da Biblioteca de **Software.** Na fita, clique na **Licença de Revisão**.    

         - Para encontrar atualizações de software com termos de licença associados, adicione a coluna Termos de **Licença** ao painel de resultados no nó **de Todas as Atualizações** de Software. Clique na rubrica para a coluna ordenar pelas atualizações de software com termos de licença.  

5.  Na página de Atualizações de **Software,** configure os critérios para as atualizações de software que o ADR recupera e adiciona ao grupo de atualização de software.  

     - O limite para as atualizações de software na ADR é de 1000 atualizações de software.  

     - Se necessário, filtre no tamanho do conteúdo para atualizações de software em regras de implementação automáticas. Para mais informações, consulte o Gestor de [Configuração e o Serviço Simplificado do Windows em sistemas operativos de nível inferior](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).  

     - A partir da versão 1910, pode utilizar **o Deploy como** filtro de atualização para as suas regras de implementação automática. Este filtro ajuda a identificar novas atualizações que possam ter de ser implementadas para as suas coleções piloto ou de teste. O filtro de atualização de software também pode ajudar a evitar a reimplementação de atualizações mais antigas. 
         - Ao utilizar **o Deploy como** filtro, tenha em ação de que já tenha implementado a atualização para outra recolha, como um piloto ou uma recolha de testes. <!--4852033-->
     - A partir da versão 1806, um filtro de propriedade para **Arquitetura** já está disponível. Use este filtro para excluir arquiteturas como Itanium e ARM64 que são menos comuns. Lembre-se que existem aplicações e componentes de 32 bits (x86) em execução em sistemas de 64 bits (x64). A menos que tenha certeza de que não precisa de x86, também o ative quando escolher x64.<!--1322266-->  

    > [!NOTE]  
    > **O Windows 10, a versão 1903 e mais tarde** foi adicionado ao Microsoft Update como seu próprio produto, em vez de fazer parte do produto **do Windows 10** como versões anteriores. Esta alteração fez com que fizesse uma série de passos manuais para garantir que os seus clientes vêem estas atualizações. Ajudamos a reduzir o número de passos manuais que tem de tomar para o novo produto na versão 1906 do Gestor de Configuração. Para mais informações, consulte [produtos de Configuração para versões do Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) <!--4682946-->


6. Na página Agenda de **Avaliação,** especifique se permite que o ADR seja executado num horário. Se estiver ativada, clique em **Personalizar** para definir a agenda periódica.  

    - A configuração do tempo de início para a programação baseia-se na hora local do computador que executa a consola Do Gestor de Configuração.  

    - A avaliação da ADR pode ser executada, no máximo, três vezes por dia.  

    - Nunca detetete o calendário de avaliação com uma frequência que exceda o calendário de sincronização das atualizações de software. Esta página apresenta o calendário de sincronização do ponto de atualização do software para ajudá-lo a determinar a frequência de horário de avaliação.  

    - Para executar manualmente o ADR, selecione a regra no nó de regra de **implementação automática** da consola e, em seguida, clique em **Run Now** na fita.  

    - A partir da versão 1802, os ADRs podem ser programados para avaliar o offset de um dia base. Por exemplo, se o Patch Tuesday realmente cair na quarta-feira para si, estabeleça o calendário de avaliação para a segunda terça-feira do mês compensado por um dia.<!--1357133-->  
        - Ao agendar a avaliação com uma compensação durante a última semana do mês, se escolher uma contrapartida que continue até ao próximo mês, o site marca a avaliação para o último dia do mês.<!--506731-->  
        ![Calendário de avaliação personalizada aDR compensado do dia base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Na página 'Agenda de **Implementação',** configure as seguintes definições:  

    -   **Avaliação do horário**: Especifique o tempo que o Gestor de Configuração avalia os prazos de tempo e de instalação disponíveis. Opte por utilizar o Tempo Universal Coordenado (UTC) ou a hora local do computador que executa a consola Do Gestor de Configuração.  

          - Quando selecionar a **hora local do Cliente** aqui e, em seguida, selecionar o mais rápido **possível** para o **tempo disponível**do Software , o tempo atual no computador que executa a consola do Gestor de Configuração é usado para avaliar quando as atualizações estão disponíveis. Este comportamento é o mesmo com o prazo de **instalação** e o momento em que as atualizações são instaladas num cliente. Se o cliente estiver num fuso horário diferente, estas ações ocorrem quando o tempo do cliente atinge o tempo de avaliação.  

    -   **Hora de disponibilização do software**: selecione uma das seguintes definições para especificar o momento em que as atualizações de software são disponibilizadas aos clientes:  

        -   **O mais rapidamente possível**: Disponibiliza as atualizações de software na implementação aos clientes o mais rapidamente possível. Quando cria a implementação com esta definição selecionada, o Gestor de Configuração atualiza a política do cliente. No próximo ciclo de sondagens de política de clientes, os clientes ficam cientes da implementação e as atualizações de software estão disponíveis para instalação.  

        -   **Hora específica**: Disponibiliza atualizações de software incluídas na implementação aos clientes numa data e hora específicas. Quando cria a implementação com esta definição ativada, o Gestor de Configuração atualiza a política do cliente. No próximo ciclo de sondagens de política de clientes, os clientes ficam cientes da implantação. No entanto, as atualizações de software na implementação só estão disponíveis para instalação após a data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações do software na implementação:  

        -   **Logo que possível**: selecione esta definição para instalar automaticamente as atualizações de software o mais rapidamente possível.  

        -   **Hora específica**: selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas. O Gestor de Configuração determina o prazo para instalar atualizações de software adicionando o intervalo de **tempo específico** configurado ao **tempo disponível**do Software .  

             - O prazo de tempo de instalação real é o prazo de entrega apresentado mais um tempo aleatório até duas horas. A randomização reduz o impacto potencial dos clientes na recolha de atualizações de instalação na implementação ao mesmo tempo.  

             - Para desativar o atraso de aleatoriedade de instalação para atualizações de software necessárias, configure a definição do cliente para **desativar a aleatoriedade** de prazos no grupo **Agente Informático.** Para mais informações, consulte [as definições](../../core/clients/deploy/about-client-settings.md#computer-agent)do cliente do Agente Informático .  

    -  Atrasar a **execução desta implementação de acordo com as preferências do utilizador, até ao período de carência definido nas definições**do cliente : Permitir que esta definição dê mais tempo aos utilizadores para instalarem as atualizações de software necessárias para além do prazo.  

        - Este comportamento é normalmente necessário quando um computador é desligado por muito tempo, e precisa de instalar muitas atualizações ou aplicações de software. Por exemplo, quando um utilizador regressa de férias, tem de esperar muito tempo enquanto o cliente instala implementações vencidas.  

        - Configure este período de carência com o período de graça da propriedade para execução após prazo de **implementação (horas)** nas definições do cliente. Para mais informações, consulte a secção de [agente informático.](../../core/clients/deploy/about-client-settings.md#computer-agent) O período de carência de execução aplica-se a todas as implementações com esta opção ativada e direcionada a dispositivos aos quais também implementou a definição do cliente.  

        - Após o prazo, o cliente instala as atualizações de software na primeira janela não-empresarial, que o utilizador configurava, até este período de carência. No entanto, o utilizador ainda pode abrir o Software Center e instalar as atualizações de software a qualquer momento. Uma vez expirado o período de graça, a aplicação reverte para o comportamento normal para implementações em atraso.  

8. Na página Experiência do **Utilizador,** configure as seguintes definições:  

    -   **Notificações**do utilizador : Especifique se deve apresentar notificação no Centro de Software no **tempo disponível**do Software configurado . Esta definição também controla se notifica os utilizadores dos clientes.  

    -   **Comportamento do prazo**: Especifique os comportamentos quando a implementação da atualização de software atingir o prazo fora de quaisquer janelas de manutenção definidas. As opções incluem a instalação das atualizações de software e a realização de um reinício do sistema após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  
        
        > [!Note]
        > Isto só se aplica quando a janela de manutenção estiver configurada para o dispositivo cliente. Se não for definida uma janela de manutenção no dispositivo, a atualização da instalação e do reinício acontecerá sempre após o prazo.

    -   Comportamento de **reinício**do dispositivo : Especifique se deve suprimir um reinício do sistema nos servidores e estações de trabalho se for necessário um reinício para completar a instalação da atualização.  

        > [!WARNING]  
        >  Suprimir o sistema de reinício pode ser útil em ambientes de servidores, ou quando não quer que os computadores-alvo reiniciem por padrão. No entanto, fazê-lo pode deixar os computadores num estado inseguro. Permitir um reinício forçado ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    -   **Escreva o manuseamento do filtro para dispositivos Incorporados**do Windows : Esta definição controla o comportamento de instalação em dispositivos Incorporados do Windows que estão ativados com um filtro de escrita. Escolha a opção de cometer alterações no prazo de instalação ou durante uma janela de manutenção. Quando selecionar esta opção, é necessário reiniciar e as alterações persistem no dispositivo. Caso contrário, a atualização é instalada, aplicada à sobreposição temporária, e comprometida posteriormente.  

           -  Quando implementar uma atualização de software para um dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

    - **Software atualiza comportamento de reavaliação de implementação após o reinício**: Selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de conformidade de atualizações de software imediatamente após um cliente instalar atualizações de software e reiniciar. Esta definição permite ao cliente verificar se há atualizações adicionais que se tornam aplicáveis após o reinício do cliente e, em seguida, instala-as durante a mesma janela de manutenção.  

9. Na página **Alerts,** configure como o Gestor de Configuração gera alertas para esta implementação. Reveja os recentes alertas de atualizações de software do Diretor de Configuração no nó de **Atualizações** de Software do espaço de trabalho da Biblioteca de **Software.** Se também estiver a utilizar o System Center Operations Manager, configure também os seus alertas.  

10. Na página Definições de **Descarregamento,** configure as seguintes definições:  

    - Especifique se os clientes devem descarregar e instalar as atualizações quando utilizam um ponto de distribuição de um vizinho ou dos grupos de fronteira do site predefinido.  

    - Especifique se os clientes devem descarregar e instalar as atualizações a partir de um ponto de distribuição no grupo de limites padrão do site, quando o conteúdo para as atualizações de software não estiver disponível a partir de um ponto de distribuição nos grupos de fronteira atuais ou vizinhos.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para mais informações, consulte [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partir da versão 1802, a BranchCache está sempre ativada nos clientes. Esta definição é removida, uma vez que os clientes utilizam a BranchCache se o ponto de distribuição o suportar.  

    - **Se as atualizações de software não estiverem disponíveis no ponto de distribuição em grupos atuais, vizinhos ou de fronteiras do site, descarregue o conteúdo do Microsoft Updates**: Selecione esta definição para ter atualizações de software de transferência de clientes ligados à intranet a partir do Microsoft Update se as atualizações não estiverem disponíveis nos pontos de distribuição. Os clientes baseados na Internet vão sempre ao Microsoft Update para obter conteúdo de atualizações de software.  

    - Especifique se permite que os clientes descarreguem após um prazo de instalação quando utilizam ligações à Internet medidos. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que enviam e recebem quando estão numa ligação com medido.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de descarregamento depende de como configurao o ponto de distribuição, o pacote de implementação e as definições nesta página.   

11. Na página pacote de **implementação,** selecione uma das seguintes opções:  

    - **Selecione um pacote de implementação**: Adicione estas atualizações a um pacote de implementação existente.  

    - **Criar um novo pacote**de implementação : Adicione estas atualizações a um novo pacote de implementação. Configure as seguintes definições adicionais:  

        -  **Nome**: especifique o nome do pacote de implementação. Use um nome único que descreva o conteúdo do pacote. Está limitado a 50 caracteres.  

        -  **Descrição**: especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional está limitada a 127 caracteres.  

        -  **Origem do pacote**: especifica a localização dos ficheiros de origem de atualização de software. Digite um caminho de rede para `\\server\sharename\path`a localização de origem, por exemplo, ou clique **em Navegar** para encontrar a localização da rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de passar para a página seguinte.  

            - Não pode utilizar a localização especificada como fonte de outro pacote de implementação de software.  

            - Pode alterar a localização da fonte do pacote nas propriedades do pacote de implementação após o Gestor de Configuração criar o pacote de implementação. Se o fizer, copie primeiro o conteúdo da fonte original do pacote para a nova localização de origem do pacote.  

            -  A conta de computador do Fornecedor SMS e do utilizador que está a executar o assistente para descarregar as atualizações de software deve ter permissões **de Escrita** para o local de descarregamento. Restrinja o acesso ao local de descarregamento. Esta restrição reduz o risco de os atacantes adulterarem os ficheiros de origem da atualização de software.  

        -  **Prioridade de envio**: especifique a prioridade de envio para o pacote de implementação. O Gestor de Configuração utiliza esta prioridade quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem prioritária: alto, médio ou baixo. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver atrasos, o pacote processa imediatamente, independentemente da sua prioridade.  

        - Ativar a **replicação diferencial binária**: Ative esta definição para minimizar o tráfego de rede entre os locais. A replicação diferencial binária (BDR) apenas atualiza o conteúdo que mudou no pacote, em vez de atualizar todo o conteúdo do pacote. Para obter mais informações, consulte a [replicação diferencial binária](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Sem pacote de implementação**: A partir da versão 1806, implemente atualizações de software para dispositivos sem primeiro descarregar e distribuir conteúdo para pontos de distribuição. Esta definição é benéfica quando se lida com conteúdos de atualização extremamente grandes. Use-o também quando sempre deseja que os clientes obtenha conteúdo do serviço de cloud Microsoft Update. Os clientes neste cenário também podem descarregar conteúdos de pares que já tenham os conteúdos necessários. O cliente do Gestor de Configuração continua a gerir o download de conteúdos, podendo assim utilizar a funcionalidade de cache de pares do Gestor de Configuração, ou outras tecnologias, como a Otimização de Entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Gestor de Configuração, incluindo atualizações do Windows e do Office.<!--1357933-->  

        > [!Note]  
        > Uma vez selecionada esta opção e aplicar as definições, esta não pode mais ser alterada. As outras opções estão acinzentadas.<!--SCCMDocs-pr issue 3003-->  

12. Na página pontos de **distribuição,** especifique os pontos de distribuição ou os grupos de pontos de distribuição para alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  
  

13. Na página **Descarregamento,** especifique se deve descarregar os ficheiros de atualização de software a partir da internet ou da sua rede local. Configure as seguintes definições:  

    -   **Descarregue as atualizações de software a partir da internet**: Selecione esta definição para descarregar as atualizações de software a partir de uma localização especificada na internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta partilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode descarregar preliminarmente as atualizações de software. Em seguida, guarde-os num local da rede local acessível a partir do computador que executa o assistente.  

14. Na página de Seleção de **Idiomas,** selecione os idiomas para os quais o site descarrega as atualizações de software selecionadas. O site só descarrega estas atualizações se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não são específicas do idioma são sempre descarregadas. Por padrão, o assistente seleciona os idiomas configurados nas propriedades do ponto de atualização do software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Quando seleciona apenas idiomas que uma atualização de software não suporta, o download falha na atualização.  

15. Na página **Resumo,** reveja as definições. Para guardar as definições para um modelo de implementação, clique em **Guardar Como Modelo**. Introduza um nome e selecione as definições que pretende incluir no modelo e, em seguida, clique em **Guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    -  O nome do modelo pode consistir em caracteres `\` Alphanuméricos `'` ASCII, bem como (backslash) ou (marca única de citação).  

16. Clique em **Seguinte** para criar a ADR.  

Depois de completar o assistente, o ADR corre. Adiciona as atualizações de software que cumprem os critérios especificados a um grupo de atualização de software. Em seguida, o ADR descarrega as atualizações para a biblioteca de conteúdos no servidor do site e distribui-as para os pontos de distribuição configurados. O ADR implementa então o grupo de atualização de software para os clientes na recolha de alvos.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a>Adicione uma nova implementação a um ADR existente  

Depois de criar um ADR, adicione implementações adicionais à regra. Esta ação ajuda-o a gerir a complexidade de implementar diferentes atualizações para diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Processo para adicionar uma nova implantação a um ADR existente  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software, selecione o nó de Regras de **Implementação Automática** e, em seguida, selecione a regra desejada.  

2.  Na fita, clique em **Adicionar Implementação**.   

3.  Na página de **Recolha** do Assistente de Implementação de Adicionar, configure as definições disponíveis da mesma forma que a página **geral** do Assistente de Regra de Implementação Automática Create. Para mais informações, consulte a secção anterior sobre o [Processo para criar um ADR](#bkmk_adr-process). O resto do Assistente de Implantação de Adicionar inclui as seguintes páginas, que também correspondem a descrições detalhadas acima:  

     - Definições de implementação
     - Agenda de Implantação
     - Experiência do Utilizador
     - Alertas
     - Definições de Transferência  

As implementações também podem ser adicionadas programáticamente utilizando cmdlets Windows PowerShell. Para obter uma descrição completa da utilização deste método, consulte [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)
