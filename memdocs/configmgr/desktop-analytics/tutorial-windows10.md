---
title: Tutorial - Implementar o Windows 10
titleSuffix: Configuration Manager
description: Um tutorial sobre a utilização do Desktop Analytics e do Gestor de Configuração para implementar o Windows 10 num grupo piloto.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2456f530444fa5d9514247edd77cbe7b02f62c38
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126009"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Implementar o Windows 10 para piloto

Este tutorial utiliza desktop Analytics e Configuração Manager para implementar o Windows 10 num grupo piloto. Destaca a integração do serviço na nuvem para fornecer insights para implementar o Windows com o produto no local. Utilize o Desktop Analytics para determinar os melhores dispositivos para colocar num grupo piloto. Em seguida, utilize o Gestor de Configuração para se apresente com o Windows.

Neste tutorial, ficará a saber como:  

> [!div class="checklist"]  
> * Configurar desktop analytics no portal Azure  
> * Conecte configurar o gestor de configurações e configurar as definições do dispositivo  
> * Criar um plano de implementação desktop Analytics para o Windows 10  
> * Utilize o Gestor de Configuração para implementar o Windows 10 no grupo piloto  

Se não tiver uma subscrição Azure, crie uma [conta gratuita](https://azure.microsoft.com/free) antes de começar. Quando configurado corretamente, a utilização do Desktop Analytics não incorre em nenhum custo Azure.

O Desktop Analytics utiliza um espaço de *trabalho de Log Analytics* na subscrição do Azure. Uma área de trabalho é essencialmente um contentor que inclui informações da conta e informações de configuração simples para a conta. Para mais informações, consulte Gerir espaços de [trabalho.](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)



## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, certifique-se de que tem os seguintes pré-requisitos:  

- Uma subscrição ativa do Azure, com permissões [**da Global Admin**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)  

    Para mais informações, consulte os [pré-requisitos do Desktop Analytics.](overview.md#prerequisites)

- Gestor de Configuração, versão 1902 com rollup de atualização (4500571) ou mais tarde, com função **de administrador completo**  

- Meios de instalação para a versão mais recente do Windows 10

- Pelo menos um dispositivo Windows 10 com as seguintes configurações:  

    - Windows 10, versão 1709 ou mais tarde, mas menos do que a versão dos meios de instalação que pretende utilizar

    - A mais recente atualização de qualidade cumulativa do Windows 10  

    - Versão cliente do Gestor de Configuração 1902 com rollup de atualização (4500571) ou posterior  

- Aprovação de negócios para configurar o nível de dados de diagnóstico do Windows para **Melhorado (Limitado)** nos dispositivos piloto  

    Para mais informações, consulte a [privacidade desktop Analytics](privacy.md).

- Conectividade da rede do dispositivo para os seguintes pontos finais da Internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net`(apenas na função do servidor do Gestor de Configuração)
    - `https://*.manage.microsoft.com`(apenas na função do servidor do Gestor de Configuração)

    Para mais informações, consulte Como permitir a partilha de [dados para desktop Analytics](enable-data-sharing.md#endpoints).  

> [!Important]  
> Estes pré-requisitos são para efeitos deste tutorial. Para obter mais informações sobre os pré-requisitos gerais para desktop Analytics com Configuração Manager, consulte [pré-requisitos](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurar a Análise de Computadores

Utilize este procedimento para iniciar sessão no Desktop Analytics e configurá-lo na sua subscrição. Este procedimento é um processo único para configurar desktop Analytics para a sua organização.  

1. Abra o [portal Desktop Analytics](https://aka.ms/desktopanalytics) na Microsoft 365 Device Management como um utilizador com permissões Global **Admin.** Selecione **Iniciar**.  

2. Na página do contrato de **serviço Aceitar,** reveja o contrato de serviço e selecione **Aceitar**.  

3. Na página confirmar a **sua subscrição,** a lista de licenças de qualificação necessárias é para funcionalidades de saúde do dispositivo Windows do Desktop Analytics. Selecione **Seguinte** para continuar.  

4. Na página de acesso dos **utilizadores Dar:**

    - Permitir que o Desktop Analytics gere as funções de **Diretório em seu nome:** Desktop Analytics atribui automaticamente aos Proprietários do Espaço de **Trabalho** a função de Administrador de Análise de **Desktop.** Se esses grupos já são um **Administrador Global,** não há mudança.  

        Caso não selecione esta opção, o Desktop Analytics continua a adicionar utilizadores como membros do grupo de segurança. Um **Administrador Global** precisa atribuir manualmente a função de Administrador de Análise de **Desktop** para os utilizadores.  

        Para obter mais informações sobre a atribuição de permissões de funções de administrador no Diretório Ativo do Azure e as permissões atribuídas aos Administradores de Análise de **Desktop,** consulte [permissões de funções de administrador no Diretório Ativo do Azure](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics reconfigura o grupo de segurança **Workspace Owners** no Azure Ative Directory para criar e gerir espaços de trabalho e planos de implementação. 

        Para adicionar um utilizador ao grupo, escreva o seu nome ou endereço de e-mail na secção **'Nome De entrada'.** Quando terminar, selecione **Next**.

5. Na página para **configurar o seu espaço de trabalho:**  

    > [!Note]  
    > Para completar este passo, o utilizador necessita de permissões **do Proprietário do Workspace** e acesso adicional à subscrição e Grupo de Recursos Azure. Para mais informações, consulte [os pré-requisitos.](overview.md#prerequisites)  

    - Selecione a sua subscrição do Azure.  

    - Para utilizar um espaço de trabalho existente para desktop Analytics, selecione-o e continue com o próximo passo.  

    - Para criar um espaço de trabalho para desktop Analytics, **selecione Adicionar espaço de trabalho**.  

        1. Introduza um **nome Workspace**.  

        2. Selecione a lista de drop-down para Selecionar o nome de **subscrição Azure para este espaço**de trabalho , e escolha a subscrição Azure para este espaço de trabalho.  

        3. **Criar novos** Grupo de recursos ou **Utilização existente**.  

        4. Selecione a **Região** da lista e, em seguida, selecione **Adicionar**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione set como espaço de **trabalho desktop Analytics**.  Em seguida, selecione **Continuar** no diálogo **de acesso confirmar e conceder** acesso.  

7. No novo separador de navegador, escolha uma conta para usar para iniciar sessão. Selecione a opção de **Consentimento em nome da sua organização** e selecione **Aceitar**.  


    > [!Note]  
    > Este consentimento é atribuir à aplicação MALogAnalyticsReader a função Log Analytics Reader para o espaço de trabalho. Esta função de aplicação é exigida pelo Desktop Analytics. Para mais informações, consulte a [função de aplicação MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Volte à página para **configurar o seu espaço de trabalho,** selecione **Next**.  

9. Na página **dos últimos passos,** selecione **Ir para desktop Analytics**. O portal Azure mostra a página **inicial** do Desktop Analytics Home.  



## <a name="connect-configuration-manager"></a>Ligar Gestor de Configuração

Utilize este procedimento para atualizar o Gestor de Configuração, ligar-se ao Desktop Analytics e configurar as definições do dispositivo. Este procedimento é um processo único para anexar a sua hierarquia ao serviço de nuvem.  

### <a name="update-configuration-manager"></a>Gestor de configuração de atualização

Instale o rollup de atualização do Gestor de Configuração de 1902 (4500571) para apoiar a integração com o Desktop Analytics. Para mais informações sobre esta atualização, consulte [o rollup atualizado para o atual ramo do Gestor de Configuração, versão 1902](https://support.microsoft.com/help/4500571).

1. Atualize o site com a atualização rollup para a versão 1902. Para mais informações, consulte [Instalar atualizações na consola](../core/servers/manage/install-in-console-updates.md).  

2. Atualizar clientes. Para simplificar este processo, considere utilizar a atualização automática do cliente. Para mais informações, consulte [os clientes de Upgrade](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Ligue-se ao serviço

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** **Selecione Configure Azure Services** na fita.  

2. Na página de **Serviços Azure** do Assistente de Serviços Azure, configure as seguintes definições:  

    - Especifique um **nome** para o objeto no Gestor de Configuração  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço  

    - Selecione **Desktop Analytics** da lista de serviços disponíveis  
  
   Selecione **Seguinte**.  

3. Na página da **App,** selecione o **ambiente Azure**apropriado . Em seguida, selecione **Browse** para a aplicação web.

4. Selecione **Criar** para adicionar facilmente uma aplicação Azure AD para a ligação Desktop Analytics.

5. Configure as seguintes definições na janela **Create Server Application:**  

    - **Nome da aplicação**: Um nome amigável para a aplicação em Azure AD.

    - **URL homePage**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por predefinição, este valor é `https://ConfigMgrService`.  

    - **App ID URI**: Este valor tem de ser único no seu inquilino Azure AD. Está no sinal de acesso usado pelo cliente do Gestor de Configuração para solicitar o acesso ao serviço. Por predefinição, este valor é `https://ConfigMgrService`.  

    - **Período**de validade da chave secreta : escolha 1 **ano** ou **2 anos** da lista de abandono. Um ano é o valor padrão.  

    Selecione **Iniciar sessão**. Depois de autenticar com sucesso o Azure, a página mostra o Nome de **Inquilino AD Azure** para referência.

    > [!Note]  
    > Complete este passo como **administrador global.** Estas credenciais não são guardadas pelo Diretor de Configuração. Esta persona não requer permissões no Gestor de Configuração, e não precisa de ser a mesma conta que gere o Assistente de Serviços Azure.  

    Selecione **OK** para criar a aplicação web em Azure AD e fechar o diálogo create server application. No diálogo da Aplicação servidor, selecione **OK**. Em seguida, selecione **Next** na página da App do Assistente de Serviços Azure.  

6. Na página dados de **diagnóstico,** configure as seguintes definições:  

    - **ID Comercial**: este valor deve povoar automaticamente com o ID da sua organização  

    - **Nível de dados de diagnóstico do Windows 10:** selecione pelo menos **Melhorado (Limitado)**  

    - **Permitir o nome do dispositivo em dados de diagnóstico:** selecione **Enable**  
  
   Selecione **Seguinte**. A página de **funcionalidades disponíveis** mostra a funcionalidade Desktop Analytics que está disponível com as definições de dados de diagnóstico da página anterior. Selecione **Seguinte**.  

7. Na página **Coleções,** configure as seguintes definições:  

    - **Nome do ecrã**: O portal Desktop Analytics apresenta esta ligação de Gestor de Configuração utilizando este nome. Use-o para diferenciar entre diferentes hierarquias. Por exemplo, laboratório de *teste* ou *produção.*  

    - **Recolha do alvo**: Esta recolha inclui todos os dispositivos que o Gestor de Configuração configura com as definições de ID comerciais e dados de diagnóstico. É o conjunto completo de dispositivos que o Gestor de Configuração liga ao serviço Desktop Analytics.  

    - **Os dispositivos na recolha do alvo utilizam um proxy autenticado**pelo utilizador para comunicação de saída : Por defeito, este valor é **Nº**. Se necessário no seu ambiente, **deponha-se**a Sim.  

    - **Selecione coleções específicas para sincronizar com desktop Analytics**: Selecione **Adicionar** para incluir coleções adicionais. Estas coleções estão disponíveis no portal Desktop Analytics para agrupar com planos de implementação. Certifique-se de incluir coleções de exclusão de pilotos e pilotos.  

        Estas coleções continuam a sincronizar-se à medida que a sua adesão muda. Por exemplo, o seu plano de implementação utiliza uma coleção com uma regra de adesão ao Windows 7. À medida que estes dispositivos atualizam para o Windows 10, e o Gestor de Configuração avalia a adesão à recolha, esses dispositivos abandonam o plano de recolha e implementação.  

8. Conclua o assistente.  

O Gestor de Configuração cria uma política de definições para configurar dispositivos na Coleção Target. Esta política inclui as definições de dados de diagnóstico para permitir que os dispositivos enviem dados para a Microsoft. Por padrão, os clientes atualizam a política a cada hora. Depois de receber as novas definições, pode demorar várias horas a mais até que os dados estejam disponíveis no Desktop Analytics.

> [!Note]  
> Para obter mais informações sobre estas definições, consulte [as definições do Windows](enroll-devices.md#windows-settings).  

Monitorize a configuração dos seus dispositivos para Desktop Analytics. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o nó de manutenção desktop **Analytics** e selecione o painel de assistência à saúde de **ligação.**  

O Gestor de Configuração sincroniza as suas coleções no prazo de 60 minutos após a criação da ligação. No portal Desktop Analytics, vá ao **Global Pilot**e consulte as coleções do seu dispositivo De Configuração Manager. Pode levar dois a três dias para o resto do portal mostrar dados completos. Para mais informações, consulte [a latência de Dados](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Criar um plano de implementação de Desktop Analytics

Utilize este procedimento para criar um plano de implementação no Desktop Analytics.

1. Abra o [portal Desktop Analytics](https://aka.ms/desktopanalytics). Utilize credenciais que tenham pelo menos permissões de Colaboradores do **Espaço de Trabalho.**  

2. Selecione **Planos de Implantação** no grupo Gerir.  

3. No painel de Planos de **Implantação,** selecione **Criar**.  

4. No painel do **plano de implementação Criar,** configure as seguintes definições:  

    - **Nome**: Um nome único para o plano de implantação, por exemplo`Windows 10 pilot`  

    - **Produtos e versões**: Selecione o produto **Windows** e a versão recomendada mais recente disponível. Por exemplo, **Windows 10, versão 1809 (recomendado)**.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos do separador 'Gestor de Configuração' e, em seguida, selecione **set como Grupos-Alvo**. Estes grupos são coleções sincronizadas do Gestor de Configuração.  

    - **Regras de prontidão**: Estas regras ajudam a determinar quais os dispositivos que se qualificam para a atualização. Selecione **WIndows OS** e configure as seguintes definições:  

        - **Os meus computadores obtêm automaticamente os controladores a partir do Windows Update**: A definição predefinida está **desligada**, o que é recomendado ao ser implementado com o 'Gestor de Configuração'.  

        - **Defina um limiar de contagem de instalação baixo para as suas aplicações**: A definição predefinida é `2%`. As aplicações abaixo deste limiar são automaticamente definidas para *a contagem de instalações low*. O Desktop Analytics não valida estes add-ins durante o piloto.  

            Se uma aplicação for instalada numa percentagem mais elevada de computadores do que este limiar, o plano de implementação marca a aplicação como *Noteworthy*. Depois pode decidir a sua importância para testar durante a fase piloto.  

    - **Data de conclusão**: Escolha a data pela qual o Windows deve ser totalmente implantado em todos os dispositivos visados.  

5. Selecione **Criar**. O novo plano aparece na lista de planos de implantação enquanto está a ser processado. Para acelerar o processamento, solicite uma atualização de dados a pedido. Para mais informações, consulte [desktop Analytics FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Abra o plano de implementação selecionando o seu nome.  

7. No menu do plano de implementação, no grupo **Preparar,** selecione **Identificar a importância**.  

    1. No separador **Apps,** selecione para mostrar apenas ativos **não revistos.**  

    2. Selecione cada aplicação e, em seguida, **selecione Editar**. Pode selecionar mais do que uma aplicação para editar ao mesmo tempo.  

    3. Escolha um nível de importância na lista **de Importância.** Se pretender que o Desktop Analytics valide a aplicação durante o piloto, selecione **Critical** ou **Important**. Não valida aplicações marcadas como **Não Importantes.** Avalie a sua [compatibilidade](compat-assessment.md) e outros conhecimentos de plano ao atribuir níveis de importância.  

        Ao atribuir níveis de importância, também pode escolher a decisão de Upgrade.  

    4. Selecione **Guardar** quando estiver completo.  

8. No menu do plano de implementação, no grupo **Preparar,** selecione **Identificar o piloto**.  

    1. Reveja os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **Adicionar ao Piloto**. Se não concordar com a recomendação, **selecione Substitua**.  

        Para obter mais informações sobre como o Desktop Analytics faz estas recomendações, selecione o ícone de informação no canto superior direito do painel **piloto identificar.**



## <a name="deploy-windows-10-in-configuration-manager"></a>Implementar o Windows 10 no Gestor de Configuração

Utilize este procedimento para implementar o Windows 10 no Gestor de Configuração para o grupo piloto.

- Se ainda não tem um, crie primeiro um pacote de [upgrade de OS para o Windows 10](#bkmk_create-package)  

- Se ainda não tiver uma, [crie uma sequência de tarefas de upgrade de OS para o Windows 10](#bkmk_create-ts)  

- [Implementar a sequência de tarefas](#bkmk_deploy-ts) utilizando o plano de implementação do Desktop Analytics  

- [Instale a sequência](#bkmk_install-ts) de tarefas do Centro de Software num dispositivo direcionado  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a>Criar um pacote de upgrade para o Windows 10

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de pacotes de atualização do **sistema operativo.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Adicionar pacote de **atualização**do sistema operativo . Esta ação inicia o Assistente de Atualização do Sistema Operativo Add.  

3. Na página Fonte de **Dados,** especifique o **Caminho** da rede para os ficheiros de origem de instalação do pacote de atualização DOS. Por exemplo, `\\server\share\path`.  

    > [!NOTE]  
    > Os ficheiros de origem de instalação contêm configuração.exe e outros ficheiros e pastas para instalar o SISTEMA.  

4. Na página **Geral,** especifique um **nome** único para o pacote de upgrade do SO.  

5. Complete o assistente de atualização do sistema operativo Add.  

#### <a name="distribute-content"></a>Distribuir conteúdo

Em seguida, distribua o pacote de upgrade do SO para pontos de distribuição.  

1. Selecione o pacote de atualização do OS na lista. No separador **Home** da fita, no grupo **De implantação,** selecione **Distribute Content**. O Assistente de Conteúdo distribuído abre.  

2. Na página **Geral,** verifique se o conteúdo listado é o conteúdo que pretende distribuir e, em seguida, selecione **Next**.  

3. Na página destino de **conteúdo,** selecione **Adicionar**, e escolha ponto de **distribuição**. Selecione um ponto de distribuição existente e, em seguida, selecione **OK**. Quando terminar de adicionar destinos de conteúdo, selecione **Next**.  

4. Complete o Assistente de Conteúdo distribuído.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a>Criar uma sequência de tarefas de upgrade de OS para o Windows 10

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione sequências de **tarefas**.  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas**.  

3. Na página Criar uma nova sequência de **tarefas** do Assistente de Sequência de Tarefas, selecione Atualizar um sistema operativo a partir de um pacote de **atualização**, e, em **seguida,** selecione Next .  

4. Na página **informação** da sequência de tarefas, especifique um nome de sequência de **tarefas** que identifique a sequência de tarefas.  

5. Na **página 'Actualizar' a** página do Sistema Operativo Windows, especificar as seguintes definições e, em seguida, selecionar **Seguinte:**  

    - **Pacote de atualização**: Especifique o pacote de atualização que contém os ficheiros de origem de atualização do SO.  

    - **Índice de edição**: Se houver vários índices de edição de OS disponíveis no pacote, selecione o índice de edição pretendido. Por predefinição, o assistente seleciona o primeiro índice.  

    - **Chave do produto**: Especifique a chave do produto Windows para o SISTEMA instalar. Especifique as chaves de licença de volume codificadas ou as chaves padrão do produto. Se utilizar uma chave de produto padrão, separe cada grupo de cinco caracteres por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX .* Quando a atualização é para uma edição de licença de volume, a chave do produto pode não ser necessária.  

        > [!Note]  
        > Esta chave do produto pode ser uma chave de ativação múltipla (MAK), ou uma chave genérica de licenciamento de volume (GVLK). Um GVLK também é referido como uma chave de configuração de cliente de serviço de gestão (KMS). Para mais informações, consulte [Plano de ativação](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)de volume . Para obter uma lista das teclas de configuração do cliente KMS, consulte o [apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server.

6. Na página **Incluir Atualizações,** selecione **Next** para não instalar quaisquer atualizações de software.  

7. Na página **'Instalar Aplicações',** selecione **Next** para não instalar quaisquer aplicações.

8. Complete o Assistente de Sequência de Tarefas Criar.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a>Implementar a sequência de tarefas utilizando o plano de implementação do Desktop Analytics

1. Na consola do Gestor de Configuração, vá à Biblioteca de **Software,** expanda a manutenção do **Desktop Analytics**e selecione o nó de Planos de **Implementação.**  

2. Selecione o seu plano de implementação piloto do Windows 10 e, em seguida, selecione Detalhes do Plano de **Implementação** na fita.  

3. No azulejo do **estado do piloto,** escolha a **sequência de tarefas** a partir da lista de lançamento e, em seguida, selecione **Deploy**.  

4. Na página **geral** do Assistente de Software de Implementação, selecione **Navegar** ao lado do campo **software.** Selecione a sequência de tarefas de atualização do Windows 10 no local e selecione **Next**.  

    > [!Note]  
    > Com a integração do Desktop Analytics, o Gestor de Configuração cria automaticamente coleções piloto e de produção para o plano de implementação. Antes de as poder utilizar, pode levar algum tempo para estas coleções sincronizarem. Para mais informações, consulte [Troubleshoot - Latência](troubleshooting.md#data-latency)de dados .<!-- 4984639 -->
    >
    > Esta coleção está reservada para dispositivos de plano de implementação desktop Analytics. Alterações manuais nesta coleção não são suportadas.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Na página **'Conteúdo',** selecione **Adicionar**, e, em seguida, selecione ponto de **distribuição**. Selecione um ponto de distribuição disponível para alojar o conteúdo de instalação e selecione **OK**. Em seguida, selecione **Seguinte**.  

6. Na página Definições de **Implementação,** selecione **Next** para aceitar as definições predefinidas. (Uma instalação disponível.)  

7. Na página **de Agendamento,** selecione **Next** para aceitar as definições predefinidas. (Disponível o mais rapidamente possível.)  

8. Na página Experiência do **Utilizador,** selecione **Next** para aceitar as definições predefinidas. (Exibição no Centro de Software e apenas mostrar notificações para reiniciar computador.)  

9. Na página **Alertas,** selecione **Next** para aceitar as definições predefinidas.  

10. Conclua o assistente.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a>Instale a sequência de tarefas do Centro de Software

1. Inscreva-se num dispositivo que seja membro do plano de implantação do piloto.  

2. Open **Software Center** e instale o sistema operativo disponível para o Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Passos seguintes

Avance para o próximo artigo para saber mais sobre os planos de implementação do Desktop Analytics.
> [!div class="nextstepaction"]  
> [Planos de implementação](about-deployment-plans.md)
