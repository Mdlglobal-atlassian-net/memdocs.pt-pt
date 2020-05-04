---
title: Implementar manualmente atualizações de software
titleSuffix: Configuration Manager
description: Crie manualmente implementações de software para atualizar os seus clientes com as atualizações de software necessárias ou para implementar atualizações fora da banda.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717091"
---
# <a name="manually-deploy-software-updates"></a>Implementar manualmente atualizações de software  

*Aplica-se a: Gestor de Configuração (ramo atual)*

Uma implementação manual de atualização de software é o processo de seleção de atualizações de software a partir da consola Do Gestor de Configuração e iniciar manualmente o processo de implementação. Ou adicione atualizações de software selecionadas a um grupo de atualização e, em seguida, implemente manualmente o grupo de atualização. Normalmente, utiliza implementações manuais para atualizar os seus clientes com as atualizações de software necessárias. Em seguida, utiliza regras de implementação automática (ADR) para gerir as implementações mensais de atualizações de software em curso. Utilize também este método manual para implementar atualizações de software fora da banda. Para obter mais informações sobre qual o método de implementação certo para si, consulte [a implementação](deploy-software-updates.md)de atualizações de software .



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a> Passo 1: Especificar critérios de pesquisa para atualizações de software  

Dependendo das combinações de produtos e classificações que o seu site sincroniza, existem potencialmente milhares de atualizações de software exibidas na consola Do Gestor de Configuração. O primeiro passo no fluxo de trabalho para implementar manualmente atualizações de software consiste em identificar as atualizações de software que pretende implementar. Por exemplo, mostre todas as atualizações de software necessárias em mais de 50 dispositivos de cliente com classificação **De Segurança** ou **Crítica.**  

> [!IMPORTANT]  
>  Uma única implementação de atualização de software tem um limite de 1000 atualizações de software.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Processo para especificar critérios de pesquisa para atualizações de software  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e clique em **Todas as Atualizações de Software**. Este nó apresenta todas as atualizações de software sincronizadas.  

    > [!NOTE]  
    >  O nó **all Software Updates** apenas apresenta atualizações de software com uma classificação **de Critical** and **Security** que foram lançadas nos últimos 30 dias.  

2.  No painel de pesquisa, filtre para identificar as atualizações de software de que necessita. Utilize uma ou ambas as seguintes opções:  

    -   Na caixa de texto de pesquisa, digite uma cadeia de pesquisa que filtra as atualizações do software. Por exemplo, digite o artigo ou id do boletim para uma atualização específica do software. Ou introduza uma cadeia que aparece no título de várias atualizações de software.  

    -   Clique em **Critérios de Adição**e selecione os critérios para filtrar as atualizações de software. Clique em **Adicionar**e, em seguida, forneça os valores para os critérios.  

3.  Clique em **Procurar** para filtrar as atualizações de software.  

    > [!TIP]  
    >  Guarde os critérios de filtro frequentemente utilizados. Na fita, clique na opção para guardar a **procura corrente**. Recupere pesquisas anteriores clicando em **Pesquisas Guardadas**.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a>Passo 2: Criar um grupo de atualização de software que contenha as atualizações de software   

Os grupos de atualização de software permitem-lhe organizar atualizações de software em preparação para a implementação. Utilize o seguinte procedimento para adicionar manualmente atualizações de software a um novo grupo de atualização de software.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Processo para adicionar atualizações de software manualmente a um novo grupo de atualizações de software  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software** e selecione Atualizações de **Software.** Selecione as atualizações de software desejadas.  

2.  Clique em Criar grupo de **atualização** de software na fita.  

3.  Especifique o nome para o grupo de atualizações de software e, opcionalmente, forneça uma descrição. Utilize um nome e descrição que forneçam informações suficientes para que determine que tipo de atualizações estão no grupo de atualização de software. Clique em **Criar**.  

4.  Selecione o nó dos Grupos de **Atualização** de Software e selecione o novo grupo de atualização de software. Para apresentar a lista de atualizações no grupo, clique em **Mostrar Membros** na fita.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a>Passo 3: Descarregue o conteúdo para o grupo de atualização de software  

Antes de implementar as atualizações de software, descarregue o conteúdo para as atualizações de software no grupo de atualização de software. Este passo permite verificar se o conteúdo está disponível nos pontos de distribuição antes de implementar as atualizações do software. Também o ajuda a evitar quaisquer problemas inesperados com a distribuição de conteúdos. Se saltar este passo, como parte do processo de implementação, o site descarrega o conteúdo e distribui para os pontos de distribuição. Utilize o seguinte procedimento para transferir o conteúdo para atualizações de software no grupo de atualizações de software.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Processo para descarregar conteúdo para o grupo de atualização de software
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Processo para monitorizar o estado do conteúdo
1. Para monitorizar o estado do conteúdo das atualizações de software, vá ao espaço de trabalho de **Monitorização** na consola 'Gestor de Configuração'. Expandir **o Estado de Distribuição**e, em seguida, selecionar o nó de Estado do **Conteúdo.**  

2. Selecione o pacote de atualização de software que identificou anteriormente para transferir as atualizações de software do grupo de atualização de software.  

3. Clique no **Estado de visualização** na fita.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a>Passo 4: Implementar o grupo de atualização de software  

Depois de determinar as atualizações que pretende implementar e adicioná-las a um grupo de atualização de software, implemente manualmente o grupo de atualização de software.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Processo para implementar manualmente as atualizações de software num grupo de atualização de software  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e selecione o nó de Grupos de Atualização de **Software.**  

2. Selecione o grupo de atualização de software que pretende implementar. Clique em **colocar** na fita.   

3. Na página **geral** do Assistente de Atualizações de Software de Implementação, configure as seguintes definições:  

   -   **Nome**: especifique o nome da implementação. A implantação deve ter um nome único que descreva o seu propósito, e o diferencia de outras implementações no site. Este campo de nome tem um limite de 256 caracteres. Por predefinição, o Gestor de Configuração fornece automaticamente um nome para a implementação no seguinte formato:`Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Descrição**: especifique uma descrição para a implementação. A descrição é opcional, mas fornece uma visão geral da implantação. Inclua qualquer outra informação relevante que ajude a identificá-la e diferenciar entre outras pessoas no site. O campo de descrição tem um limite de 256 caracteres, e tem um valor em branco por padrão.  

   -   Grupo de **atualização de software/atualização**de software : Verifique se o grupo de atualização de software ou atualização de software apresentado está correto.  

   -   **Selecionar Modelo de Implementação**: especifique se pretende aplicar um modelo de implementação anteriormente guardado. Configure um modelo de implementação para guardar propriedades comuns de implementação de atualizações de software. Em seguida, aplique o modelo quando implementar atualizações de software no futuro. Estes modelos poupam tempo e ajudam a garantir a consistência em implementações semelhantes.  

   -   **Recolha**: Especifique a recolha para a implantação. Os dispositivos da coleção recebem as atualizações de software nesta implementação.  

4. Na página Definições de **Implementação,** configure as seguintes definições:  

   -   **Tipo de implementação**: especifique o tipo de implementação para a implementação da atualização de software.  

       > [!IMPORTANT]  
       >  Depois de criar a implementação da atualização de software, não pode alterar o tipo de implementação.  

        - Selecione **Necessário** para criar uma implementação obrigatória de atualização de software. As atualizações de software são automaticamente instaladas nos clientes antes do prazo de instalação que configura.  

        - Selecione **Disponível** para criar uma implementação opcional de atualização de software. Esta implementação está disponível para os utilizadores instalarem a partir do Software Center.  

       > [!NOTE]  
       >  Quando implementa um grupo de atualização de software conforme **necessário,** os clientes descarregam o conteúdo em segundo plano e honram as definições bits, se configurados.  
       > 
       > Para grupos de atualização de software implementados como **disponíveis,** os clientes descarregam o conteúdo em primeiro plano e ignoram as definições bits.  

   -   Utilize o **Wake-on-LAN para acordar os clientes para as implementações necessárias**: Especifica se permite ativar o Wake On LAN no prazo. Wake On LAN envia pacotes de despertar para computadores que requerem uma ou mais atualizações de software na implementação. O site acorda todos os computadores que estão em modo de sono no prazo de instalação para que a instalação possa iniciar. Os clientes que estão em modo de sono que não necessitam de atualizações de software na implementação não foram iniciados. Por predefinição, esta definição não está ativada. Só está disponível para implementações **necessárias.** Antes de utilizar esta opção, configure computadores e redes para Wake On LAN. Para mais informações, consulte [Como configurar Wake On LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens do Estado que os clientes reportam ao site.  

5. Na página **de Agendamento,** configure as seguintes definições:  

   -   **Avaliação do horário**: Especifique o tempo que o Gestor de Configuração avalia os prazos de tempo e de instalação disponíveis. Opte por utilizar o Tempo Universal Coordenado (UTC) ou a hora local do computador que executa a consola Do Gestor de Configuração.  

       - Quando selecionar a **hora local do Cliente** aqui e, em seguida, selecionar o mais rápido **possível** para o **tempo disponível**do Software , o tempo atual no computador que executa a consola do Gestor de Configuração é usado para avaliar quando as atualizações estão disponíveis. Este comportamento é o mesmo com o prazo de **instalação** e o momento em que as atualizações são instaladas num cliente. Se o cliente estiver num fuso horário diferente, estas ações ocorrem quando o tempo do cliente atinge o tempo de avaliação.  

   -   **Hora de disponibilização do software**: selecione uma das seguintes definições para especificar o momento em que as atualizações de software são disponibilizadas aos clientes:  

       -   **O mais rapidamente possível**: Disponibiliza as atualizações de software na implementação aos clientes o mais rapidamente possível. Quando cria a implementação com esta definição selecionada, o Gestor de Configuração atualiza a política do cliente. No próximo ciclo de sondagens de política de clientes, os clientes ficam cientes da implementação e as atualizações de software estão disponíveis para instalação.  

       -   **Hora específica**: Disponibiliza atualizações de software incluídas na implementação aos clientes numa data e hora específicas. Quando cria a implementação com esta definição ativada, o Gestor de Configuração atualiza a política do cliente. No próximo ciclo de sondagens de política de clientes, os clientes ficam cientes da implantação. No entanto, as atualizações de software na implementação só estão disponíveis para instalação após a data e hora configuradas.  

   -   **Prazo de instalação**: Estas opções só estão disponíveis para implementações **necessárias.** Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações de software na implementação  

       -   **Logo que possível**: selecione esta definição para instalar automaticamente as atualizações de software o mais rapidamente possível.  

       -   **Hora específica**: selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas.  

           - O prazo de tempo de instalação real é o prazo de entrega apresentado mais um tempo aleatório até duas horas. A randomização reduz o impacto potencial dos clientes na recolha de atualizações de instalação na implementação ao mesmo tempo.   

           - Para desativar o atraso de aleatoriedade de instalação para atualizações de software necessárias, configure a definição do cliente para **desativar a aleatoriedade** de prazos no grupo **Agente Informático.** Para mais informações, consulte [as definições](../../core/clients/deploy/about-client-settings.md#computer-agent)do cliente do Agente Informático .  

   -  Atrasar a **execução desta implementação de acordo com as preferências do utilizador, até ao período de carência definido nas definições**do cliente : Permitir que esta definição dê mais tempo aos utilizadores para instalarem as atualizações de software necessárias para além do prazo.  

       - Este comportamento é normalmente necessário quando um computador é desligado por muito tempo, e precisa de instalar muitas atualizações ou aplicações de software. Por exemplo, quando um utilizador regressa de férias, tem de esperar muito tempo enquanto o cliente instala implementações vencidas.  

       - Configure este período de carência com o período de graça da propriedade para execução após prazo de **implementação (horas)** nas definições do cliente. Para mais informações, consulte a secção de [agente informático.](../../core/clients/deploy/about-client-settings.md#computer-agent) O período de carência de execução aplica-se a todas as implementações com esta opção ativada e direcionada a dispositivos aos quais também implementou a definição do cliente.  

       - Após o prazo, o cliente instala as atualizações de software na primeira janela não-empresarial, que o utilizador configurava, até este período de carência. No entanto, o utilizador ainda pode abrir o Software Center e instalar as atualizações de software a qualquer momento. Uma vez expirado o período de graça, a aplicação reverte para o comportamento normal para implementações em atraso.  

6. Na página Experiência do **Utilizador,** configure as seguintes definições:  

   -   **Notificações**do utilizador : Especifique se deve apresentar notificação no Centro de Software no **tempo disponível**do Software configurado . Esta definição também controla se notifica os utilizadores nos computadores dos clientes. Para implementações **disponíveis,** não é possível selecionar a opção de Ocultar no Centro de **Software e todas as notificações**.  

   -   **Comportamento do prazo**: Esta definição é apenas configurável para implementações **necessárias.** Especifique os comportamentos quando a implementação da atualização de software atingir o prazo fora de quaisquer janelas de manutenção definidas. As opções incluem a instalação das atualizações de software e a realização de um reinício do sistema após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > Isto só se aplica quando a janela de manutenção estiver configurada para o dispositivo cliente. Se não for definida uma janela de manutenção no dispositivo, a atualização da instalação e do reinício acontecerá sempre após o prazo.

   -   **Comportamento de reinício**do dispositivo : Esta definição é apenas configurável para as implementações **necessárias.** Especifique se deve suprimir um reinício do sistema em servidores e estações de trabalho se for necessário um reinício para completar a instalação da atualização.  

       > [!WARNING]  
       >  Suprimir o sistema de reinício pode ser útil em ambientes de servidores, ou quando não quer que os computadores-alvo reiniciem por padrão. No entanto, fazê-lo pode deixar os computadores num estado inseguro. Permitir um reinício forçado ajuda a garantir a conclusão imediata da instalação da atualização de software.  

   -   **Escreva o manuseamento do filtro para dispositivos Incorporados**do Windows : Esta definição controla o comportamento de instalação em dispositivos Incorporados do Windows que estão ativados com um filtro de escrita. Escolha a opção de cometer alterações no prazo de instalação ou durante uma janela de manutenção. Quando selecionar esta opção, é necessário reiniciar e as alterações persistem no dispositivo. Caso contrário, a atualização é instalada, aplicada à sobreposição temporária, e comprometida posteriormente.  

       -  Quando implementar uma atualização de software para um dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

   - **Software atualiza comportamento de reavaliação de implementação após o reinício**: Selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de conformidade de atualizações de software imediatamente após um cliente instalar atualizações de software e reiniciar. Esta definição permite ao cliente verificar se há atualizações adicionais que se tornam aplicáveis após o reinício do cliente e, em seguida, instala-as durante a mesma janela de manutenção.  

7. Na página **Alerts,** configure como o Gestor de Configuração gera alertas para esta implementação. Reveja os recentes alertas de atualizações de software do Diretor de Configuração no nó de **Atualizações** de Software do espaço de trabalho da Biblioteca de **Software.** Se também estiver a utilizar o System Center Operations Manager, configure também os seus alertas. Apenas configure alertas para as implementações **necessárias.**  

8. Na página Definições de **Descarregamento,** configure as seguintes definições:  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de descarregamento depende de como configurao o ponto de distribuição, o pacote de implementação e as definições nesta página.  

    - Especifique se os clientes devem descarregar e instalar as atualizações quando utilizam um ponto de distribuição de um vizinho ou dos grupos de fronteira do site predefinido.  

    - Especifique se os clientes devem descarregar e instalar as atualizações a partir de um ponto de distribuição no grupo de limites padrão do site, quando o conteúdo para as atualizações de software não estiver disponível a partir de um ponto de distribuição nos grupos de fronteira atuais ou vizinhos.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para mais informações, consulte [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partir da versão 1802, a BranchCache está sempre ativada nos clientes. Esta definição é removida, uma vez que os clientes utilizam a BranchCache se o ponto de distribuição o suportar.  

    - **Se as atualizações de software não estiverem disponíveis no ponto de distribuição em grupos atuais, vizinhos ou de fronteiras do site, descarregue o conteúdo do Microsoft Updates**: Selecione esta definição para ter atualizações de software de transferência de clientes ligados à intranet a partir do Microsoft Update se as atualizações não estiverem disponíveis nos pontos de distribuição. Os clientes baseados na Internet vão sempre ao Microsoft Update para obter conteúdo de atualizações de software.

    - Especifique se permite que os clientes descarreguem após um prazo de instalação quando utilizam ligações à Internet medidos. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que enviam e recebem quando estão numa ligação com medido.  

9. Na página pacote de **implementação,** selecione uma das seguintes opções:  

    > [!Note]  
    > Se já executou [o Passo 3: Descarregue o conteúdo para o grupo](#BKMK_3DownloadContent)de atualização de software, então o assistente não apresenta o Pacote de **Implementação,** **Pontos de Distribuição**e Páginas de **Seleção de Idiomas.** Passe para a página [resumo](#bkmk_summary) do assistente.  
    > 
    >  As atualizações de software que foram previamente descarregadas para a biblioteca de conteúdos do servidor do site não são novamente descarregadas. Este comportamento é verdadeiro mesmo quando cria um novo pacote de implementação para as atualizações de software. Se todas as atualizações de software já tiverem sido descarregadas, o assistente salta para a página [Sumária.](#bkmk_summary)  

    - **Selecione um pacote de implementação**: Adicione estas atualizações a um pacote de implementação existente.  

    - **Criar um novo pacote**de implementação : Adicione estas atualizações a um novo pacote de implementação. Configure as seguintes definições adicionais:  

        -  **Nome**: especifique o nome do pacote de implementação. Use um nome único que descreva o conteúdo do pacote. Está limitado a 50 caracteres.  

        -  **Descrição**: especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional está limitada a 127 caracteres.  

        -  **Origem do pacote**: especifique a localização dos ficheiros de origem de atualização de software. Digite um caminho de rede para `\\server\sharename\path`a localização de origem, por exemplo, ou clique **em Navegar** para encontrar a localização da rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de continuar na página seguinte.  

            - Não pode utilizar a localização especificada como fonte de outro pacote de implementação de software.  

            - Pode alterar a localização da fonte do pacote nas propriedades do pacote de implementação após o Gestor de Configuração criar o pacote de implementação. Se o fizer, copie primeiro o conteúdo da fonte original do pacote para a nova localização de origem do pacote.  

            -  A conta de computador do Fornecedor SMS e do utilizador que está a executar o assistente para descarregar as atualizações de software deve ter permissões **de Escrita** para o local de descarregamento. Restrinja o acesso ao local de descarregamento. Esta restrição reduz o risco de os atacantes adulterarem os ficheiros de origem da atualização de software.  

        -  **Prioridade de envio**: especifique a prioridade de envio para o pacote de implementação. O Gestor de Configuração utiliza esta prioridade quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem prioritária: alto, médio ou baixo. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver atrasos, o pacote processa imediatamente, independentemente da sua prioridade.  

        - Ativar a **replicação diferencial binária**: Ative esta definição para minimizar o tráfego de rede entre os locais. A replicação diferencial binária (BDR) apenas atualiza o conteúdo que mudou no pacote, em vez de atualizar todo o conteúdo do pacote. Para obter mais informações, consulte a [replicação diferencial binária](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Sem pacote de implementação**: A partir da versão 1806, implemente atualizações de software para dispositivos sem primeiro descarregar e distribuir conteúdo para pontos de distribuição. Esta definição é benéfica quando se lida com conteúdos de atualização extremamente grandes. Use-o também quando sempre deseja que os clientes obtenha conteúdo do serviço de cloud Microsoft Update. Os clientes neste cenário também podem descarregar conteúdos de pares que já tenham os conteúdos necessários. O cliente do Gestor de Configuração continua a gerir o download de conteúdos, podendo assim utilizar a funcionalidade de cache de pares do Gestor de Configuração, ou outras tecnologias, como a Otimização de Entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Gestor de Configuração, incluindo atualizações do Windows e do Office.<!--1357933-->  

10. Na página pontos de **distribuição,** especifique os pontos de distribuição ou os grupos de pontos de distribuição para alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Se já executou [o Passo 3: Descarregue o conteúdo para o grupo](#BKMK_3DownloadContent)de atualização de software, então o assistente não apresenta o Pacote de **Implementação,** **Pontos de Distribuição**e Páginas de **Seleção de Idiomas.** Passe para a página [resumo](#bkmk_summary) do assistente.  

11. Na página **Descarregamento,** especifique se deve descarregar os ficheiros de atualização de software a partir da internet ou da sua rede local. Configure as seguintes definições:  

    -   **Descarregue as atualizações de software a partir da internet**: Selecione esta definição para descarregar as atualizações de software a partir de uma localização especificada na internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta partilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode descarregar preliminarmente as atualizações de software. Em seguida, guarde-os num local da rede local acessível a partir do computador que executa o assistente.  

12. Na página de Seleção de **Idiomas,** selecione os idiomas para os quais o site descarrega as atualizações de software selecionadas. O site só descarrega estas atualizações se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não são específicas do idioma são sempre descarregadas. Por padrão, o assistente seleciona os idiomas configurados nas propriedades do ponto de atualização do software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Quando seleciona apenas idiomas que uma atualização de software não suporta, o download falha na atualização.  

    > [!Note]  
    > Se já executou [o Passo 3: Descarregue o conteúdo para o grupo](#BKMK_3DownloadContent)de atualização de software, então o assistente não apresenta o Pacote de **Implementação,** **Pontos de Distribuição**e Páginas de **Seleção de Idiomas.** Passe para a página [resumo](#bkmk_summary) do assistente.  

13. <a name="bkmk_summary"></a>Na página **Resumo,** reveja as definições. Para guardar as definições para um modelo de implementação, clique em **Guardar Como Modelo**. Introduza um nome e selecione as definições que pretende incluir no modelo e, em seguida, clique em **Guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    -  O nome do modelo pode consistir em caracteres `\` Alphanuméricos `'` ASCII, bem como (backslash) ou (marca única de citação).  

14. Clique em **Seguinte** para implementar a atualização de software.  

    Depois de completar o assistente, o Gestor de Configuração descarrega as atualizações de software para a biblioteca de conteúdos no servidor do site. Em seguida, distribui o conteúdo para os pontos de distribuição configurados e implementa o grupo de atualização de software para os clientes na coleção de alvos. Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)
