---
title: Configurar a descoberta
titleSuffix: Configuration Manager
description: Configure métodos de descoberta para encontrar recursos para gerir a partir da sua rede, Ative Directory e Azure Ative Directory.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721046"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configure métodos de descoberta para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Configure métodos de descoberta para encontrar recursos para gerir a partir da sua rede, Ative Directory e Azure Ative Directory (Azure AD). Primeiro, ative e, em seguida, configure cada método que pretende utilizar para pesquisar o seu ambiente. Também pode desativar um método utilizando o mesmo procedimento que utiliza para o ativar. As únicas exceções a este processo são a Heartbeat Discovery e a Server Discovery:  

- Por predefinição, a **Heartbeat Discovery** já está ativada quando instala um site primário do Gestor de Configuração. Está configurado para funcionar com um horário básico. Mantenha a Descoberta do Batimento Cardíaco ativada. Certifica-se de que os registos de dados de descoberta (DDRs) para dispositivos estão atualizados. Para mais informações sobre heartbeat discovery, consulte [About Heartbeat Discovery](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Server Discovery** é um método de descoberta automática. Encontra computadores que usas como sistemas de site. Não pode configurá-lo ou desativá-lo.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a>Descoberta florestal de diretório ativo  

Para terminar a configuração do Ative Directory Forest Discovery, configure as definições nos seguintes locais da consola De Configuração Manager:  

- No nó dos **Métodos de Descoberta:**

  - Ative este método de descoberta.  

  - Estabeleça um horário de votação.  

  - Selecione se a descoberta cria automaticamente limites para os sites e subredes do Diretório Ativo que descobre.  

- No nó **Ative Directory Forests:**

  - Adicione florestas que quer descobrir.  

  - Permitir a descoberta de sítios e subredes de Diretório Ativo naquela floresta.  

  - Configure configurações que permitem aos sites do Gestor de Configuração publicar as informações do seu site para a floresta.  

  - Atribuir uma conta para usar como Conta Florestal de Diretório Ativo para cada floresta.  

Utilize os seguintes procedimentos para permitir a Ative Directory Forest Discovery e para configurar as florestas individuais para utilização com ative directory Forest Discovery.  

### <a name="configure-active-directory-forest-discovery"></a>Configure Descoberta Florestal de Diretório Ativo  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó **discovery Methods.**  

2. Selecione o método Ative Directory Forest Discovery para o local onde pretende configurar a descoberta.  

3. No separador **Casa** da fita, selecione **Propriedades**.  

4. No separador **Geral** das propriedades, configure as seguintes definições:  

    - Ativar o método de descoberta.

    - Especifique as opções para criar limites do site para locais descobertos.  

    - Especifique um horário para quando a descoberta correr.  

5. Selecione **OK** para salvar a configuração.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configure uma floresta para Ative Directory Forest Discovery  

1. No espaço de trabalho **da Administração,** expanda a **Configuração da Hierarquia,** e selecione o nó **Ative Directory Forests.** Se a Deteção de Florestas do Active Directory tiver sido executada anteriormente, as florestas detetadas serão apresentadas no painel de resultados. Quando este método de descoberta funciona, descobre a floresta local e quaisquer florestas de confiança. Adicione manualmente florestas não confiáveis.  

    - Para configurar uma floresta previamente descoberta, selecione a floresta no painel de resultados. Na fita, selecione **Propriedades** para abrir as propriedades da floresta.

    - Para configurar uma nova floresta que não esteja listada, no separador **Home** da fita, no grupo **Criar,** selecione **Add Forest**. Esta ação abre a caixa de diálogo **Add Forests.**

2. No separador **Geral,** termine as configurações para a floresta que pretende descobrir e especifique a Conta Florestal do **Diretório Ativo**. Para obter mais informações sobre esta conta, consulte [Contas](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > A Deteção de Florestas do Active Directory requer uma conta global para detetar e publicar em florestas não fidedignas. Se não utilizar a conta de computador do servidor do site, só pode selecionar uma conta global.  

3. Se planeia deixar os sites publicarem dados do site para esta floresta, no separador **Publishing,** termine as configurações para publicação nesta floresta.  

    > [!NOTE]  
    > Se deixar os sites publicarem para uma floresta, estenda o esquema de Diretório Ativo dessa floresta para O Gestor de Configuração. A Conta Florestal do Diretório Ativo deve ter permissões de controlo total para o contentor do Sistema naquela floresta.  

4. Selecione **OK** para salvar a configuração.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a>Descoberta de Diretório Ativo para computadores, utilizadores ou grupos  

Para configurar a descoberta de computadores, utilizadores ou grupos, comece com estes passos comuns:

1. Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó **discovery Methods.**  

2. Selecione o método para o site onde pretende configurar a descoberta.  

3. No separador **Casa** da fita, selecione **Propriedades**.  

4. No separador **Geral** das propriedades, selecione a caixa de verificação para permitir a descoberta. Ou pode configurar a descoberta agora, e depois voltar para permitir a descoberta mais tarde.  

Em seguida, utilize as informações nas seguintes secções para configurar os métodos específicos de descoberta:  

- [Deteção de Grupos do Active Directory](#bkmk_config-adgd)  

- [Deteção de Sistemas do Active Directory](#bkmk_config-adgd)  

- [Deteção de Utilizadores do Active Directory](#bkmk_config-adud)  

> [!NOTE]  
> A informação nesta secção não se aplica à Ative Directory Forest Discovery.  

Embora cada um destes métodos de descoberta seja independente dos outros, eles partilham opções semelhantes. Para obter mais informações sobre estas opções de configuração, consulte [opções partilhadas para a descoberta de grupos, sistemas e utilizadores](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> A sondagem do Diretório Ativo por cada um destes métodos de descoberta pode gerar tráfego significativo de rede. Considere agendar cada método de descoberta para executar numa altura em que este tráfego de rede não afeta negativamente os usos empresariais da sua rede.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a>Configure Ative Directory Group Discovery  

1. No separador **Geral** da janela Ative Directory Group Discovery Properties, selecione **Adicionar** para configurar um âmbito de descoberta. Selecione **grupos** ou **localização**. Em seguida, termine as seguintes configurações nos **Grupos Add** ou adicione a caixa de diálogo de **localização de diretório ativo:**  

    1. Especifique um **nome** para este âmbito de descoberta.  

    2. Especifique um Domínio ou **Localização** **de Diretório Ativo** para pesquisar:  

        - Se escolher **Grupos,** especifique um ou mais grupos de Diretórios Ativos para descobrir.  

        - Se escolheu **o Local,** especifique um recipiente de Diretório Ativo como local para descobrir. Também pode permitir uma pesquisa recursiva de recipientes para crianças do Diretório Ativo para esta localização.  

    3. Especifique a Conta de Descoberta do **Grupo de Diretório Ativo** que o site utiliza para pesquisar este âmbito de descoberta. Para mais informações, consulte [Contas](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Selecione **OK** para salvar a configuração de alcance de descoberta.  

2. Repita os passos anteriores para cada âmbito adicional de descoberta que pretende definir.  

3. No separador **Agenda de Sondagens,** configure tanto o calendário completo de sondagens de descoberta como a descoberta delta.

4. No separador **Opções,** configure as definições para filtrar ou excluir registos de computador estonteantes da descoberta. Configure também a descoberta da adesão aos grupos de distribuição.  

    > [!NOTE]  
    > Por padrão, o Ative Directory Group Discovery descobre apenas a adesão a grupos de segurança.  

5. Selecione **OK** para salvar a configuração.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a>Configure descoberta do sistema de diretório ativo  

1. No separador **Geral** da janela Ative Directory System Discovery Properties, selecione o **novo** ícone Novo ícone para especificar um novo recipiente de ![ ](media/Disc_new_Icon.gif) Diretório Ativo. Na caixa de diálogo ative **Directory Container,** termine as seguintes configurações:  

    1. Digite ou navegue para um local para o **Caminho**. Este valor é um caminho LDAP válido para um contentor ou unidade organizacional (OU). O site questiona este caminho para recursos. Por exemplo, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Especifique opções que alterem o comportamento de pesquisa:  

        - **Descubra objetos dentro dos grupos Ative Directy**: O site também olha para a adesão de grupos neste caminho.  

        - **Pesquisa recursivamente recipientes para crianças do Diretório Ativo**: Se ativar esta opção, o site procura quaisquer recipientes ou OUs adicionais dentro do caminho acima referido. Se desativar esta opção, o site apenas procura recursos no caminho específico.  

          A partir da versão 1806, selecione subrecipientes para excluir desta pesquisa recursiva. Esta opção ajuda a reduzir o número de objetos descobertos. Selecione **Adicionar** para escolher os recipientes sob o caminho acima. Na caixa de diálogo Select New Container, selecione um recipiente para crianças para excluir. Selecione **OK** para fechar a caixa de diálogo Select New Container.<!--1358143-->

          > [!Tip]  
          > A lista de recipientes de Diretório Ativo na janela Ative Directory System Discovery Properties inclui uma coluna **Has Exclusions**. Quando seleciona recipientes para excluir, este valor é **Sim**.  

    3. Para cada local, especifique a conta a utilizar como conta de descoberta de **diretório ativo**. Para mais informações, consulte [Contas](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Para cada local especificado, pode configurar um conjunto de opções de descoberta e uma conta única de descoberta de diretório ativo.  

    4. Selecione **OK** para guardar a configuração do recipiente Ative Directy.  

2. No separador **Agenda de Sondagens,** configure tanto o calendário completo de sondagens de descoberta como a descoberta delta.  

3. No separador **Ative Directory Atributos,** configure atributos adicionais do Diretório Ativo para computadores que pretende descobrir. Este separador lista os atributos padrão do objeto.  

    > [!Tip]  
    > Por exemplo, a sua organização utiliza o atributo **descrição** na conta do computador em Diretório Ativo. Selecione **Custom**e adicione `Description` como atributo personalizado. Após a duração deste método de descoberta, este atributo mostra no separador Propriedades do dispositivo na consola 'Gestor de Configuração'.<!--513948-->  

4. No separador **Opções,** configure as definições para filtrar ou excluir registos de computador estonteantes da descoberta.  

5. Selecione **OK** para salvar a configuração.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a>Configure a descoberta do utilizador do diretório ativo  

1. No separador **Geral** da janela Ative Directory User Discovery Properties, selecione o **novo** ![ ícone Novo ícone para especificar um novo recipiente ](media/Disc_new_Icon.gif) de Diretório Ativo. Na caixa de diálogo ative **Directory Container,** termine as seguintes configurações:  

    1. Especifique um ou mais locais para procurar.  

    2. Para cada local, especifique opções que alterem o comportamento de pesquisa.  

    3. Para cada local, especifique a conta a utilizar como conta de descoberta de **diretório ativo**. Para mais informações, consulte [Contas](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Para cada local especificado, pode configurar um conjunto único de opções de descoberta e uma conta única de descoberta de diretório ativo.  

    4. Selecione **OK** para guardar a configuração do recipiente Ative Directy.  

2. No separador **Agenda de Sondagens,** configure tanto o calendário completo de sondagens de descoberta como a descoberta delta.  

3. No separador **Ative Directory Atributos,** configure atributos adicionais do Diretório Ativo para computadores que pretende descobrir. Este separador lista os atributos padrão do objeto.  

4. Selecione **OK** para salvar a configuração.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Descoberta de utilizador de Anúncios Azure

A Descoberta do Utilizador de AD Azure não está ativada ou configurada da mesma forma que outros métodos de descoberta. Configure-o quando embarcar no site do Gestor de Configuração para o Azure AD.

Para mais informações, consulte a Descoberta do [Utilizador da AD Azure](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Pré-requisitos

Para ativar e configurar este método de descoberta, [configure os serviços Azure](azure-services-wizard.md) para gestão de **nuvem.**

Se utilizar o Gestor de Configuração para *criar* a aplicação Azure, ele confunde a aplicação com as permissões necessárias.

Se criar a aplicação em Azure primeiro e *depois importá-la* para O Gestor de Configuração, terá de configurar manualmente a aplicação. Esta configuração inclui a concessão da permissão da aplicação do servidor para ler dados de diretório.

1. Abra o [portal Azure](https://portal.azure.com) como utilizador com permissões *Global Admin.* Vá ao **Diretório Ativo Azure**e selecione registos de **Aplicativos.** Mude para **Todas as aplicações,** se necessário.

1. Selecione a aplicação alvo.

1. No menu **Gerir,** selecione **permissões API**.  

    1. No painel de **permissões DaPI,** selecione **Adicionar uma permissão**.  

    2. No painel **de permissões Request API,** mude para APIs que **a minha organização utiliza.**  

    3. Procure e selecione a API do **Microsoft Graph.**  

        > [!Tip]
        > Na versão 1810 e anterior, utilize o **Azure Ative Directory Graph** API.

    4. Selecione o grupo de **permissões de aplicação.** Expandir **o Diretório**, e selecionar **Diretório.Read.All**.  

    5. **Selecione Adicionar permissões**.  

1. No painel de **permissões da API,** na secção de consentimento do **Grant,** selecione **grant administrador consentimento...**. Selecione **Sim**.  

### <a name="configure-azure-ad-user-discovery"></a>Configure Descoberta de Utilizador aD Azure

Ao configurar o serviço **Cloud Management** Azure:

- Na página **Discovery** do assistente, selecione a opção para ativar a descoberta do **utilizador ativo do Diretório Azure**.
- Selecione **Definições**.
- Na caixa de diálogo De definições de Definições de Definições de Descoberta de Utilizadores De AD Azure, configure um horário para quando ocorrer a descoberta. Também pode permitir a descoberta delta, que apenas verifica contas novas ou alteradas em Azure AD.

> [!Note]  
> Se o utilizador tiver uma identidade federada ou sincronizada, deve utilizar a descoberta do [utilizador Ative Directory](about-discovery-methods.md#bkmk_aboutUser) do Directory do Directory do Gestor de Configuração, bem como a descoberta do utilizador da AD Azure. Para obter mais informações sobre identidades híbridas, consulte Definir uma estratégia híbrida de [adoção](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)de identidade.<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Descoberta do grupo de utilizadores da AD Azure

<!--3611956-->
> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1906 como uma [funcionalidade de pré-lançamento.](../../manage/pre-release-features.md) Começando com a versão 2002, já não é uma funcionalidade de pré-lançamento.  

Pode descobrir grupos de utilizadores e membros desses grupos a partir de Azure AD. Quando o site encontra utilizadores em grupos De AD Azure que ainda não foi descoberto anteriormente, adiciona-os como novos recursos de utilizador no Gestor de Configuração. É criado um registo de recursos do grupo de utilizadores quando o grupo é um grupo de segurança.

### <a name="prerequisites"></a>Pré-requisitos

- Serviço Cloud Management [Azure](azure-services-wizard.md)
- Permissão para ler e pesquisar grupos DaD Azure

### <a name="limitations"></a>Limitações

A descoberta da Delta para a descoberta do grupo de utilizadores da AD Azure está atualmente desativada.

### <a name="log-files"></a>Ficheiros de registo

Utilize o registo SMS_AZUREAD_DISCOVERY_AGENT.log para resolução de problemas. Este registo também é partilhado com a descoberta do utilizador da AD Azure. Para mais informações, consulte [ficheiros De registo](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Ativar a descoberta do grupo de utilizadores da AD Azure

Para permitir a descoberta de um serviço Azure de **Cloud Management:**

1. Vá ao espaço de trabalho da **Administração,** expanda os **Serviços cloud,** em seguida, selecione o nó dos **Serviços Azure.**
1. Selecione um dos seus serviços Azure e, em seguida, selecione **Propriedades** na fita.
1. No separador **Discovery,** verifique a caixa para ativar a Descoberta do Grupo de **Directórioactivo Azure**e, em seguida, selecione **Definições**.
1. **Selecione Adicionar** sob o separador **Discovery Scopes.**
    - Pode modificar a Agenda de **Sondagens** no outro separador.
1. Selecione um ou mais grupos de utilizadores. Pode **pesquisar** pelo nome e escolher se quiser ver **apenas grupos de segurança**.
    - Será solicitado a iniciar sessão no Azure quando selecionar **Search** pela primeira vez.
1. Selecione **OK** quando terminar de selecionar grupos.
1. Assim que a descoberta terminar a correr, pode navegar nos grupos de utilizadores da AD Azure no nó **dos Utilizadores.**

Para permitir a descoberta ao configurar um novo serviço **Cloud Management** Azure:

- Na página **Discovery** do assistente, selecione a opção para ativar a Descoberta do Grupo de **DirectórioActivo Azure**.
- Selecione **Definições**.
- Na caixa de diálogo Azure AD Group Discovery Settings, configure o seu âmbito de descoberta e um horário para quando ocorrer a descoberta.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a>Descoberta do Batimento Cardíaco

O Gestor de Configuração ativa o método Heartbeat Discovery quando instala um site primário. Se quiser usar o horário padrão de cada sete dias, não há mais nada para configurar. Caso contrário, basta configurar a programação para a frequência com que os clientes enviam o registo de dados da Heartbeat Discovery para um ponto de gestão.  

> [!NOTE]  
> Se ativar tanto a instalação de impulso do cliente como a tarefa de manutenção do site para **a Clear Install Flag** no mesmo local, detetete a programação da Heartbeat Discovery para ser inferior ao período de **redescoberta** do cliente da tarefa de manutenção do site **Clear Install Flag.** Para obter mais informações sobre as tarefas de manutenção do site, consulte [as tarefas](../../manage/maintenance-tasks.md)de manutenção.  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Configure o calendário da Descoberta do Batimento Cardíaco  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó **discovery Methods.**  

2. Selecione o método **Heartbeat Discovery** para o site onde pretende configurar a Descoberta do Batimento Cardíaco.  

3. No separador **Casa** da fita, selecione **Propriedades**.  

4. Configure a frequência com que os clientes submetem um registo de dados de descoberta de batimentos cardíacos. Em seguida, selecione **OK** para salvar a configuração.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a>Descoberta da Rede  

Antes de configurar a Descoberta da Rede, compreenda os seguintes tópicos:  

- Níveis disponíveis de Descoberta de Rede  

- Opções disponíveis de Descoberta de Rede  

- Limitando a Descoberta da Rede na rede  

Para mais informações, consulte sobre a Descoberta da [Rede.](about-discovery-methods.md#bkmk_aboutNetwork)  

As seguintes secções fornecem informações sobre configurações comuns para o Network Discovery. Pode configurar uma ou mais destas configurações para utilização durante a mesma execução de descoberta. Se utilizar várias configurações, planeje as interações que podem afetar os resultados da descoberta.  

Por exemplo, descobre todos os dispositivos Simple Network Management Protocol (SNMP) que utilizam um nome comunitário SNMP específico. Para a mesma descoberta, desativa-se a descoberta numa subnetespecífica específica. Quando a descoberta é concluída, a Network Discovery não descobre os dispositivos SNMP com o nome comunitário especificado na subnet que desativou.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a>Determine a sua topologia de rede  

Pode usar uma descoberta só de topologia para mapear a sua rede. Este tipo de descoberta não descobre potenciais clientes. A Topologia-Só-A Descoberta da Rede depende do SNMP.  

Quando estiver a mapear a sua topologia de rede, configure o máximo de **lúpulo** no separador **SNMP** na caixa de diálogo **Network Discovery Properties.** Apenas alguns lúpulos podem ajudar a controlar a largura de banda da rede que é usada quando a descoberta corre. À medida que descobre mais da sua rede, aumente o número de lúpulos para obter uma melhor compreensão da sua topologia de rede.  

Depois de compreender a sua topologia de rede, configure propriedades adicionais para o Network Discovery. Estas propriedades ajudam a descobrir potenciais clientes e seus sistemas operativos. Configure também o Network Discovery para limitar os segmentos de rede que pode pesquisar.  

Para mais informações, consulte [Como determinar a sua topologia](#bkmk_proc-top) de rede

### <a name="network-discovery-search-options"></a>Opções de pesquisa de Descoberta de Rede

O Gestor de Configuração suporta os seguintes métodos para pesquisar a rede:

- [Limitar as pesquisas utilizando subredes](#BKMK_LimitBySubnet)
- [Pesquisar um domínio específico](#BKMK_SearchByDomain)
- [Limite as pesquisas utilizando nomes comunitários sNMP](#BKMK_LimitBySNMPname)
- [Pesquise um servidor DHCP específico](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a>Limitar as pesquisas utilizando subredes  

Pode configurar o Network Discovery para pesquisar subredes específicas durante uma execução de descoberta. Por padrão, a Network Discovery procura a subnet do servidor que executa a descoberta. Quaisquer subredes adicionais que configure e ative se apliquem apenas às opções de pesquisa sNMP e DHCP. Quando o Network Discovery procura domínios, não é limitado por configurações para subredes.  

Se especificar uma ou mais subredes no separador **Subnets** na caixa de diálogo **Network Discovery Properties,** apenas pesquisa as subredes que marca como **Ativada**.  

Quando desativa uma sub-rede, o site exclui-a da descoberta, e aplicam-se as seguintes condições:  

- As consultas baseadas no SNMP não funcionam na sub-rede.  

- Os servidores DHCP não respondem com uma lista de recursos localizados na subnet.  

- Consultas baseadas em domínios podem descobrir recursos que estão localizados na subnet.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a>Pesquisar um domínio específico  

Pode configurar o Network Discovery para pesquisar um domínio ou conjunto de domínios específicos durante uma execução de descoberta. Por padrão, a Network Discovery procura o domínio local do servidor que executa a descoberta.  

Se especificar um ou mais domínios no separador **Domínios** na caixa de diálogo **Network Discovery Properties,** apenas pesquisa os domínios que marca como **Ativado**.  

Quando desativa um domínio, o site exclui-o da descoberta, e aplicam-se as seguintes condições:  

- A Network Discovery não consulta controladores de domínio nesse domínio.  

- As consultas baseadas em SNMP ainda podem ser executadas em subredes no domínio.  

- Os servidores DHCP ainda podem responder com uma lista de recursos localizados no domínio.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a>Limite as pesquisas utilizando nomes comunitários sNMP  

Configura a Network Discovery para pesquisar uma comunidade específica de SNMP ou um conjunto de comunidades durante uma descoberta. Por padrão, o método confunde o nome da comunidade **pública.**  

O Network Discovery utiliza nomes comunitários para aceder a routers que são dispositivos SNMP. Um router pode fornecer a Network Discovery com informações sobre outros routers e subredes que estão ligados ao primeiro router.  

> [!NOTE]  
> Os nomes da comunidade SNMP assemelham-se a senhas. A Network Discovery só pode obter informações a partir de um dispositivo SNMP para o qual especificou um nome comunitário. Cada dispositivo SNMP pode ter o seu próprio nome comunitário, mas muitas vezes o mesmo nome comunitário é partilhado entre vários dispositivos. Além disso, a maioria dos dispositivos SNMP tem um nome de comunidade padrão de **público**. Mas algumas organizações apagam o nome da comunidade **pública** dos seus dispositivos como uma precaução de segurança.  

Se incluir mais de uma comunidade SNMP no separador **SNMP** na caixa de diálogo **Network Discovery Properties,** ele procura-os na ordem em que são mostrados. Certifique-se de que os nomes mais utilizados estão no topo da lista. Esta configuração ajuda a minimizar o tráfego de rede que o site gera quando tenta contactar um dispositivo utilizando diferentes nomes.

> [!NOTE]  
> Juntamente com o nome da comunidade SNMP, pode especificar o endereço IP ou o nome resolúvel de um dispositivo SNMP específico. Faz esta ação no separador **Dispositivos SNMP** na caixa de diálogo **Network Discovery Properties.**  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a>Pesquise um servidor DHCP específico  

Pode configurar o Network Discovery para utilizar um servidor DHCP específico ou vários servidores para descobrir clientes DHCP durante uma execução de descoberta.  

O Network Discovery procura cada servidor DHCP que especifica no separador **DHCP** na caixa de diálogo **Network Discovery Properties.** Se o servidor que está a executar a descoberta aloca o seu endereço IP a partir de um servidor DHCP, pode configurar a descoberta para pesquisar aquele servidor DHCP. Ative este comportamento com a opção **de incluir o servidor DHCP que o servidor do site está configurado para usar**.  

> [!NOTE]  
> Para configurar com sucesso um servidor DHCP no Discovery da Rede, o seu ambiente deve suportar o IPv4. Não é possível configurar o Network Discovery para utilizar um servidor DHCP num ambiente nativo IPv6.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a>Como configurar a Descoberta da Rede  

Utilize os seguintes procedimentos para descobrir primeiro apenas a sua topologia de rede e, em seguida, para configurar a Network Discovery para descobrir potenciais clientes utilizando uma ou mais opções disponíveis de Network Discovery.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a>Como determinar a sua topologia de rede  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó **discovery Methods.**  

2. Selecione o método **De seleção de Network Discovery** para o site onde pretende descobrir recursos de rede.  

3. No separador **Casa** da fita, selecione **Propriedades**.  

    - No separador **Geral,** selecione a opção de ativar a **descoberta da rede**. Em seguida, selecione **Topologia** a partir do tipo de opções **de descoberta.**  

    - No separador **Subnets,** selecione a opção **Procurar subredes locais.**  

      > [!TIP]  
      > Se conhecer as subredes específicas que constituem a sua rede, desmarque a caixa de verificação **de sub-redes local Search.** Em seguida, selecione o **novo** ![ ícone Novo ](media/Disc_new_Icon.gif) ícone, e adicione as subredes específicas que pretende pesquisar. Para grandes redes, procure apenas uma ou duas subredes de cada vez para minimizar o uso da largura de banda da rede.  

    - No separador **Domínios,** selecione a opção de **procurar domínio local**.  

    - No separador **SNMP,** selecione uma opção na lista de lançamentos de **lúpulo máximo.** Esta opção especifica quantos routers hops Network Discovery pode levar para mapear a sua topologia.  

      > [!TIP]  
      > Quando mapear pela primeira vez a topologia da rede, configure apenas alguns saltos de router para minimizar o uso da largura de banda da rede.  

4. No separador **'Agendar',** selecione o **novo** ![ ícone Novo ícone e ](media/Disc_new_Icon.gif) detetete um calendário para a descoberta em execução.  

    > [!NOTE]  
    > Não é possível atribuir uma configuração de descoberta diferente aos horários separados da Discovery da Rede. Cada vez que a Rede Discovery corre, utiliza a configuração de descoberta atual.  

5. Selecione **OK** para aceitar as configurações. A Descoberta da Rede funciona na hora programada.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a>Como configurar a Descoberta da Rede  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da **Administração,** expanda a **Configuração da Hierarquia**e selecione o nó **discovery Methods.**  

2. Selecione o método **De seleção de Network Discovery** para o site onde pretende descobrir recursos de rede.  

3. No separador **Casa** da fita, selecione **Propriedades**.  

4. No separador **Geral,** selecione a opção de ativar a **descoberta da rede**.  

    - Selecione entre as opções de descoberta do **tipo de** descoberta que pretende executar.  

    - Ative a opção de **rede Slow** para o Gestor de Configuração para fazer ajustes automáticos para redes de largura de banda baixa.  

5. Para configurar a descoberta para pesquisar subredes, mude para o separador **Subnets.** Em seguida, configure uma ou mais das seguintes opções:  

    - Para executar a descoberta em subredes locais para o computador que executa a descoberta, permita a opção de **pesquisar subredes locais**.  

    - Para pesquisar uma sub-rede específica, certifique-se de que a sub-rede está listada em **Subnets para pesquisar** e tem um valor de **Pesquisa** de **Ativado:**  

      1. Se a sub-rede não estiver listada, selecione o **novo** ![ ícone Novo ícone ](media/Disc_new_Icon.gif) . Na caixa de diálogo **New Subnet Assignment,** introduza as informações **de Subnet** e **Máscara** e, em seguida, selecione **OK**. Por padrão, uma nova sub-rede está ativada para pesquisa.  

      2. Para alterar o valor **de Pesquisa** de uma sub-rede listada, selecione-o na lista. Em seguida, selecione o ícone **Alternar** para mudar o valor entre **Desativado** e **Ativado**.  

6. Para configurar a descoberta para pesquisar domínios, mude para o separador **Domínios.** Em seguida, configure uma ou mais das seguintes opções:  

    - Para executar a descoberta no domínio do computador que executa a descoberta, permita a opção de procurar o **domínio local**.  

    - Para pesquisar um domínio específico, certifique-se de que o domínio está listado em **Domínios** e tem um valor de **Pesquisa** de **Habilitado:**  

      1. Se o domínio não estiver listado, selecione o **novo** ![ ícone Novo ícone ](media/Disc_new_Icon.gif) . Na caixa de diálogo **Domain Properties,** introduza as informações do **Domínio** e, em seguida, selecione **OK**. Por padrão, um novo domínio está ativado para pesquisa.  

      2. Para alterar o valor **de Pesquisa** de um domínio listado, selecione-o na lista. Em seguida, selecione o ícone **Alternar** para mudar o valor entre **Desativado** e **Ativado**.  

7. Para configurar a descoberta para pesquisar nomes específicos da comunidade SNMP para dispositivos SNMP, mude para o separador **SNMP.** Em seguida, configure uma ou mais das seguintes opções:  

    - Para adicionar um nome comunitário SNMP à lista de **nomes comunitários SNMP,** selecione o **novo** ![ ícone Novo ícone ](media/Disc_new_Icon.gif) . Na nova caixa de diálogo **SNMP Community Name,** especifique o **nome** da comunidade SNMP e, em seguida, selecione **OK**.  

    - Para remover um nome de comunidade SNMP, selecione o nome da comunidade e, em seguida, selecione o ícone **Eliminar** ![ ](media/Disc_delete_Icon.gif) .  

    - Para ajustar a ordem de pesquisa dos nomes da comunidade SNMP, selecione um nome comunitário da lista. Em seguida, selecione o ícone **move item up move** up ícone ou o ícone move ![ ](media/Disc_moveUp_Icon.gif) **item down** Move Down Icon ![ ](media/Disc_moveDown_Icon.gif) . Quando a descoberta corre, os nomes da comunidade são procurados por uma ordem de alto a baixo. 

    - Para configurar o número máximo de saltos de router para utilização por pesquisas SNMP, selecione o número de lúpulo da lista de **lançamentos máximos de lúpulo.**  

8. Para configurar um dispositivo SNMP, mude para o separador **Dispositivos SNMP.** Se o dispositivo não estiver listado, selecione o **novo** ![ ícone Novo ícone ](media/Disc_new_Icon.gif) . Na caixa de diálogo do **Novo Dispositivo SNMP,** especifique o endereço IP ou o nome do dispositivo do dispositivo SNMP e, em seguida, selecione **OK**.  

    > [!NOTE]  
    > Se especificar um nome de dispositivo, o Gestor de Configuração deve ser capaz de resolver o nome NetBIOS num endereço IP.  

9. Para configurar a descoberta para consultar servidores DHCP específicos, mude para o separador **DHCP.** Em seguida, configure uma ou mais das seguintes opções:  

    - Para consultar o servidor DHCP no computador que está a ser descoberto, ative a opção de **utilizar sempre o servidor DHCP do servidor do servidor do site**.  

      > [!NOTE]  
      > Para utilizar esta opção, o servidor deve alugar o seu endereço IP a partir de um servidor DHCP e não pode utilizar um endereço IP estático.  

    - Para consultar um servidor DHCP específico, selecione o **novo** ![ ícone Novo ícone ](media/Disc_new_Icon.gif) . Na nova caixa de diálogo **do Servidor DHCP,** especifique o endereço IP ou o nome do servidor do servidor DHCP e, em seguida, selecione **OK**.  

      > [!NOTE]  
      > Se especificar um nome de servidor, o Gestor de Configuração deve ser capaz de resolver o nome NetBIOS num endereço IP.  

10. Para configurar quando a descoberta for executado, mude para o separador **'Agendar'.** Em seguida, selecione o **novo** ícone Novo ícone para definir uma programação para executar o Discovery da ![ ](media/Disc_new_Icon.gif) Rede. Pode configurar vários horários recorrentes e vários horários que não têm recorrência.  

    > [!NOTE]  
    > Se o separador **Schedule** mostrar mais de um horário ao mesmo tempo, o Network Discovery corre para todos os horários, tal como está configurado no momento indicado na programação. Este comportamento também é verdade para horários recorrentes.  

11. Selecione **OK** para guardar as suas configurações.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a>Como verificar se a Network Discovery terminou  

O tempo que a Network Discovery requer para terminar pode variar dependendo de um ou mais dos seguintes fatores:  

- O tamanho da sua rede  

- A topologia da sua rede  

- O número máximo de lúpulo que estão configurados para encontrar routers na rede  

- O tipo de descoberta que está sendo executado  

A Network Discovery não cria mensagens para o alertar quando estiver terminado. Utilize o seguinte procedimento para verificar quando a descoberta tiver terminado:  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir **o Estado do Sistema**e, em seguida, selecionar o nó de perguntas de mensagem de **estado.**  

2. Selecione a consulta **de Todas as Mensagens** de Estado.  

3. No separador **Home** da fita, no grupo 'Perguntas de **Mensagem de Estado',** selecione **Mostrar Mensagens**.  

4. Na janela All Status Messages, selecione um valor a partir da lista de data e de entrega de **tempo Select** que inclua há quanto tempo a descoberta começou. Em seguida, selecione **OK** para abrir o Visualizador de Mensagem de Estado do Gestor de **Configuração**.  

    > [!TIP]  
    > Também pode utilizar a opção **de data e hora especificada** para selecionar uma determinada data e hora que executou a descoberta. Esta opção é útil quando executou o Network Discovery numa dada data e quer recuperar mensagens a partir dessa data.  

5. Para validar que a Discovery da Rede terminou, procure uma mensagem de estado que tenha os seguintes detalhes:  

    - ID da mensagem: **502**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descrição: **Este componente parou**  

    Se esta mensagem de estado não estiver presente, a Network Discovery ainda não terminou.  

6. Para validar quando a Network Discovery começou, procure uma mensagem de estado que tenha os seguintes detalhes:  

    - ID da mensagem: **500**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descrição: **Este componente começou**  

    Esta informação verifica que a Network Discovery começou. Se esta informação não estiver presente, remarque a Descoberta da Rede.  
