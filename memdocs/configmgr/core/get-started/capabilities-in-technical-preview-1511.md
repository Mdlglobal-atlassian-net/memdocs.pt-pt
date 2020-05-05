---
title: Capacidades na Pré-visualização Técnica 1511
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f32eaffe673324699e20fc7c579ea1ac9b38c479
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076344"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1511 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1511. Esta versão é uma instalação de base para a pré-visualização técnica que pode utilizar instalar um novo site de pré-visualização técnica ou para atualizar a partir de uma versão anterior da pré-visualização técnica.   Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a>Integração com Atualização do Windows para Negócios no Windows 10  
 O Gestor de Configuração tem agora a capacidade de diferenciar um computador Windows 10 que está diretamente ligado através do Windows Update for Business (WUfB) contra os ligados ao WSUS para obter atualizações e atualizações do Windows 10.  Para computadores ligados via WUfB, as atualizações e atualizações podem ser geridas na cadência definida por um utilizador administrativo através de políticas de grupo ou de MDM e estas atualizações/atualizações podem ser instaladas diretamente a partir do WUfB.    
Para computadores ligados via WUfB, o Gestor de Configuração não poderá reportar o estado de conformidade (incluindo atualizações do Windows ou Atualizações de Definição). Também o Gestor de Configuração não será capaz de implementar atualizações do Microsoft Updates ou 3ª parte para estes computadores.  

 **Pré-requisitos para este cenário:**  

-   Windows 10 Desktop Pro ou Windows 10 Enterprise Edition versão 1511 ou posterior  

-   Computadores a serem geridos através [do Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Experimente!  
 Tente completar a seguinte tarefa e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionou:  

1.  Desative o Agente do Windows Update para que não faça análises no WSUS, se tiver sido ativado previamente.   
    A chave de registo **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** pode ser definida para indicar se o computador está a analisar o WSUS ou o Windows Update.  Quando o valor é 2, não é digitalização contra a WSUS.  

2.  Tome nota do novo atributo **UseWUServer,** sob o nó **de Atualização do Windows** no Explorador de Recursos do Gestor de Configuração.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição de agente de cliente para desativar o fluxo de trabalho de atualização de software e implemente-a na coleção de computadores ligados diretamente ao WUfB.  

5.  Os computadores que são geridos via WUfB apresentarão **Desconhecido** no estado de conformidade e não serão contados como parte da percentagem de conformidade global.  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a>Managing Office 365 ProPlus Client Update através de Gestor de Configuração  
 O Gestor de Configuração tem agora a capacidade de gerir as atualizações de clientes do Office 365 usando o fluxo de trabalho de Gestão de Atualização de Software do Gestor de Configuração.    
Quando a Microsoft publicar uma nova atualização do cliente do Office 365 para o Windows Server Updates Services (WSUS), o Gestor de Configuração poderá sincronizar a atualização para o seu catálogo se a atualização do Office 365 estiver configurada para fazer parte da sincronização do catálogo.  O servidor do site do Gestor de Configuração irá descarregar as atualizações do cliente do Office 365 e distribuir o pacote para pontos de distribuição do Gestor de Configuração.  O cliente do Gestor de Configuração informará então os clientes do Office 365 onde obter as atualizações e quando iniciar o processo de instalação da atualização.  

**Pré-requisitos para este cenário:**  

### <a name="try-it-out"></a>Experimente!  
 Tente completar a seguinte tarefa e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionou:  

1. Pode sincronizar as atualizações do Office 365 no servidor do site do Gestor de Configuração e vê-las a partir da consola do Gestor de Configuração.  

2. Pode aprovar e implementar com sucesso as atualizações do Office 365.  

3. Pode descarregar e obter com sucesso as atualizações do Office 365 para os clientes.  

4. Pode verificar a conformidade com as atualizações do Office 365 utilizando monitorização ou relatórios na consola.  

   Para obter passos detalhados, consulte [a Manage Office 365 atualizações de clientes com pré-visualização técnica do Gestor](https://technet.microsoft.com/library/mt628083.aspx)de Configuração .  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a>Suporte para SQL Server AlwaysOn para bases de dados altamente disponíveis  
 O Gestor de Configuração agora suporta a utilização de um sQL Server AlwaysOn grupos de disponibilidade para hospedar a base de dados do site.  Ao instalar um novo site, pode dirigir a configuração para utilizar o grupo de disponibilidade em vez de uma instância normal do SQL Server.  

> [!NOTE]  
>  A configuração bem sucedida e a utilização de grupos de disponibilidade requer que se sinta confortável com a configuração de grupos de disponibilidade do Servidor SQL, e conta com documentação e procedimentos fornecidos na biblioteca de documentação do Servidor SQL.  

O processo de alto nível para configurar e utilizar grupos de disponibilidade inclui:  

1.  Configure o grupo de disponibilidade no Servidor SQL.  

2.  Instale um novo site do Gestor de Configuração e durante a Configuração direcione o site para utilizar o grupo de disponibilidade especificando os grupos Endpoint.  

**Pré-requisitos para este cenário:**  

-   Requer uma versão do Servidor SQL suportada pela pré-visualização técnica do Gestor de Configuração  

-   Tem de criar e configurar o Grupo de Disponibilidade do Servidor SQL antes de instalar o Gestor de Configuração  

-   O grupo de disponibilidade tem de ter uma réplica primária e pode ter até duas réplicas secundárias síncronas  

-   O grupo de disponibilidade deve ter pelo menos um Ponto Final  

-   Deve ter uma localização de rede a que cada Servidor SQL no Grupo de Disponibilidade pode aceder. Esta localização é utilizada por Configuração ao configurar o Grupo de Disponibilidade e pode ser removida após a configuração completa.  

**Questões conhecidas para este lançamento:**  

-   Não é possível adicionar com sucesso um novo membro réplica a um Grupo de Disponibilidade que já está a ser utilizado como base de dados do site. Em vez disso, deve reinstalar o site depois de adicionado o novo membro da réplica.  

-   Para este cenário poderá ser necessário instalar o **cliente nativo Do SQL Server 2012** ([a partir do Pacote de Funcionalidades SQL Server 2012](https://www.microsoft.com/download/details.aspx?id=29065)) no servidor de ponto de gestão. Isto evita erros de ligação SQL (que estão registados no **mp_getauth.log** no servidor do ponto de gestão).  

### <a name="try-it-out"></a>Experimente!  
Tente completar as seguintes tarefas e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionavam:  

-   Posso instalar um site primário que usa um servidor de base de dados configurado para Grupos de Disponibilidade SQL AlwaysOn  

-   Consegui falhar com o meu Grupo de Disponibilidade SQL AlwaysOn para uma nova réplica no grupo e o local principal ainda está operacional.  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configurar o servidor SQL AlwaysOn para o Gestor de Configuração  
 Utilize os seguintes procedimentos para criar e configurar primeiro o grupo de disponibilidade e, em seguida, instalar um novo site do Gestor de Configuração que utiliza o grupo de disponibilidade.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Para criar um grupo de disponibilidade sQL Server AlwaysOn  
O processo para criar um grupo de disponibilidade do [Servidor SQL](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) está documentado na biblioteca de documentação do Servidor SQL.  Ao criar o grupo de disponibilidade, certifique-se de que os seguintes requisitos de utilização com o Gestor de Configuração são cumpridos:  

-   Um máximo de três membros:  

    -   Uma réplica primária e até duas réplicas secundárias  

    -   As réplicas secundárias devem ser sincronizadas.  

        > [!TIP]  
        >  Recomendamos que as réplicas secundárias sejam configuradas apenas para serem lidas. Isto permite-lhe usar uma réplica secundária para funções como reportar, mantendo o desempenho da réplica primária para operações no local.  

-   Pelo menos um ponto final. O nome virtual deste ponto final será utilizado quando instalar o site do Gestor de Configuração.  

    > [!TIP]  
    >  Embora o grupo possa conter vários Pontos Finais, o Gestor de Configuração só pode utilizar um.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Para instalar um site de Gestor de Configuração que utiliza o grupo de disponibilidade  
Para instalar um site que utiliza um grupo de disponibilidade do Servidor SQL:  

1.  Substitua o seguinte quando solicitado pela Configuração do Gestor de Configuração:  

    -   **Nome do Servidor SQL**: Introduza o nome virtual para o Ponto Final que configurado ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como ** &lt;\>endpointServer .fabrikam.com**.  

    -   **Caso**: Este valor deve permanecer em branco. Não há nenhum caso nesta configuração.  

    -   **Base de dados**: Introduza o nome da base de dados criada na réplica primária do grupo de disponibilidade.  

2.  Em seguida, deve fornecer uma localização de rede a que cada Servidor SQL do grupo pode aceder:  

    -   A conta de computador e a conta de serviço de cada Servidor SQL requerem acesso total ao controlo a esta localização.  

    -   Esta localização só é utilizada durante a configuração e pode ser não partilhada ou eliminada após a configuração estar concluída e o site estiver instalado.  

3.  Depois de fornecer esta informação, complete a configuração com o seu processo normal e configurações.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a>Serviço de um cluster de servidor  
Agora pode criar uma coleção que contenha servidores num cluster e, em seguida, configurar as definições de cluster para utilizar quando implementa atualizações para o cluster. Pode controlar a percentagem de servidores que estão online a qualquer momento, bem como configurar scripts PowerShell pré-implantação e pós-implementação para executar ações personalizadas.  

**Questões conhecidas para este lançamento:**  

-   O relatório não está disponível para verificar o estado da implementação de atualizações de software para servidores de cluster.  

-   A opção de sequência de manutenção na página **Definições** de Cluster está desativada e não está disponível nesta versão.  

### <a name="try-it-out"></a>Experimente!  
Tente completar a seguinte tarefa e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionou:  

-   Posso criar uma coleção que represente um conjunto de servidores. Para este teste, pode configurar as suas regras de adesão para ter 2 máquinas nesta coleção.  

-   Posso especificar que apenas 50% dos servidores do cluster podem estar offline em qualquer ponto da manutenção do cluster. Utilize as scripts da amostra no procedimento para especificar os scripts de pré-implantação e pós-implantação.  

-   Implemente uma atualização para esta coleção. Reveja os ficheiros start.txt e end.txt em C:\temp e verifique os tempos de início e fim para a implementação nos servidores do cluster. Reveja o ficheiro UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Para criar uma coleção para um cluster de servidores  

1.  [Crie uma coleção](https://technet.microsoft.com/library/gg712295.aspx) de dispositivos que contenha os servidores do cluster.  

2.  No espaço de trabalho **de Ativos e Compliance,** clique em Coleções de **Dispositivos,** clique à direita na recolha que contém os servidores no cluster e, em seguida, clique em **Propriedades**.  

3.  No separador **Geral,** selecione **Todos os dispositivos fazem parte do mesmo cluster do servidor**e, em seguida, clique em **Definições**.  

4.  Na página Definições do **Cluster,** selecione a percentagem de servidores que podem ser desligados ao mesmo tempo para ter atualizações de software instaladas. Um servidor de cluster pode ser desligado de cada vez, independentemente da percentagem que fornece. O Gestor de Configuração irá arredondar ao selecionar quantos servidores serão reparados de uma só vez. Por exemplo, se escolher 51% e houver 4 servidores no cluster, 2 servidores serão desligados ao mesmo tempo.  

5.  Especifique se utilizar á função de um script pré-implantação (drenagem do nó) ou de uma script pós-implantação (resumo do nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar em testes para scripts de pré-implantação e pós-implantação que escrevam o tempo atual num ficheiro de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Para implementar atualizações de software para o cluster do servidor  

1.  [Implemente atualizações](https://technet.microsoft.com/library/gg712304.aspx) de software para a coleção de clusters do servidor.  

2.  [Monitorize a implementação da atualização do software](https://technet.microsoft.com/library/gg712304.aspx).  
