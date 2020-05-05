---
title: Configurar serviços do Azure
titleSuffix: Configuration Manager
description: Conecte o ambiente do Gestor de Configuração com os serviços Azure para gestão de nuvem, Microsoft Store para Negócios e Log Analytics.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f36da59c6924f6d2f71d882f601c6dd563840d73
ms.sourcegitcommit: fb84a87e46f9fa126c1c24ddea26974984bc9ccc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/22/2020
ms.locfileid: "82022539"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configure serviços Azure para utilização com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o **Assistente de Serviços Azure** para simplificar o processo de configuração dos serviços de nuvem Azure que utiliza com o Gestor de Configuração. Este assistente proporciona uma experiência de configuração comum utilizando registos de aplicações web Azure Ative Directory (Azure AD). Estas aplicações fornecem detalhes de subscrição e configuração e autenticam comunicações com a AD Azure. A aplicação substitui a entrada desta mesma informação sempre que configura um novo componente ou serviço do Gestor de Configuração com o Azure.


## <a name="available-services"></a>Serviços disponíveis

Configure os seguintes serviços Azure utilizando este assistente:  

- **Cloud Management**: Este serviço permite que o site e os clientes autentiquem utilizando a Azure AD. Esta autenticação permite outros cenários, tais como:  

    - [Instalar e atribuir clientes do Gestor de Configuração do Windows 10 utilizando a AD Azure para autenticação](../../../clients/deploy/deploy-clients-cmg-azure.md)  

    - [Configure Descoberta de Utilizador aD Azure](configure-discovery-methods.md#azureaadisc)  

    - [Configure Azure AD User Group Discovery](configure-discovery-methods.md#bkmk_azuregroupdisco)

    - Apoiar certos cenários de [gateway de gestão](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios) de nuvem  

    - [Notificações de e-mail de aprovação de aplicativos](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics Connector**: [Ligue-se ao Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Sync dados de recolha para Log Analytics.  

    > [!Note]  
    > Este artigo refere-se ao *Conector De Log Analytics,* anteriormente chamado de *Conector OMS*. Não há diferença funcional. Para mais informações, consulte [A Gestão Azure - Monitorização](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store for Business**: Connect to the [Microsoft Store for Business](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Obtenha aplicativos de loja para a sua organização que você pode implementar com O Gestor de Configuração.  

### <a name="service-details"></a>Detalhes do serviço

A tabela seguinte lista detalhes sobre cada um dos serviços.  

- **Inquilinos**: O número de instâncias de serviço que pode configurar. Cada instância deve ser um inquilino azure distinto.  

- **Nuvens**: Todos os serviços suportam a nuvem azure global, mas nem todos os serviços suportam nuvens privadas, como a nuvem do Governo dos EUA Azure.  

- **Aplicação web**: Se o serviço utiliza uma aplicação Azure AD de tipo *Web app / API,* também referida como uma aplicação de servidor no Gestor de Configuração.  

- **Aplicação nativa**: Se o serviço utiliza uma aplicação Azure AD de tipo *Nativo,* também referida como uma aplicação de cliente no Gestor de Configuração.  

- **Ações**: Se pode importar ou criar estas aplicações no Assistente de Serviços Do Gestor de Configuração Azure.  

|Serviço  |Inquilinos  |Nuvens  |Aplicação Web  |Aplicação nativa  |Ações  |
|---------|---------|---------|---------|---------|---------|
|Gestão de nuvem com<br>Descoberta da AD Azure | Vários | Público, Privado | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | Importar, Criar |
|Conector de análise de log | Um | Público, Privado | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar |
|Microsoft Store para<br>Empresa | Um | Público | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar, Criar |

### <a name="about-azure-ad-apps"></a>Sobre aplicativos Azure AD

Diferentes serviços Azure requerem configurações distintas, que você faz no portal Azure. Além disso, as aplicações para cada serviço podem exigir permissões separadas aos recursos do Azure.  

Pode utilizar uma única aplicação para mais de um serviço. Só há um objeto a gerir no Diretor de Configuração e no Anúncio Azure. Quando a chave de segurança da aplicação expirar, só tem de renovar uma tecla.

Quando cria serviços Azure adicionais no assistente, o Gestor de Configuração é projetado para reutilizar informações que são comuns entre serviços. Este comportamento ajuda-o a não inserir a mesma informação mais de uma vez.

Para obter mais informações sobre as permissões e configurações de aplicações necessárias para cada serviço, consulte o artigo de Gestor de Configuração relevante nos [serviços disponíveis.](#available-services)

Para mais informações sobre as aplicações do Azure, comece com os seguintes artigos:

- [Autenticação e autorização no Serviço de Aplicações do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Visão geral das Aplicações Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [Bases do Registo de Uma Candidatura em Azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Registe a sua candidatura com o seu inquilino do Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)


## <a name="before-you-begin"></a>Antes de começar

Depois de decidir o serviço a que pretende ligar, consulte a tabela em detalhes de [Serviço](#service-details). Esta tabela fornece informações necessárias para completar o Assistente de Serviço Azure. Tenha uma discussão antecipada com o seu administrador da AD Azure. Decida qual das seguintes ações a tomar:

- Crie manualmente as aplicações com antecedência no portal Azure. Em seguida, importe os detalhes da aplicação para O Gestor de Configuração.  

- Utilize o Gestor de Configuração para criar diretamente as aplicações em Azure AD. Para recolher os dados necessários da Azure AD, reveja as informações nas outras secções deste artigo.  

Alguns serviços exigem que as aplicações DaD Azure tenham permissões específicas. Reveja as informações de cada serviço para determinar as permissões necessárias. Por exemplo, antes de poder importar uma aplicação web, um administrador azure deve criá-la primeiro no [portal Azure](https://portal.azure.com).

Ao configurar o Conector Log Analytics, forneça *ao* seu colaborador de aplicações web recentemente registado no grupo de recursos que contenha o espaço de trabalho relevante. Esta permissão permite ao Gestor de Configuração aceder a esse espaço de trabalho. Ao atribuir a permissão, procure o nome do registo da aplicação na área de **Adicionar utilizadores** do portal Azure. Este processo é o mesmo que ao fornecer ao Gestor de [Configuração permissões para registar o Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Um administrador azure deve atribuir estas permissões antes de importar a app para o Gestor de Configuração.


## <a name="start-the-azure-services-wizard"></a>Inicie o assistente dos Serviços Azure

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.**  

2. No separador **Home** da fita, no grupo **Serviços Azure,** selecione **Serviços Configure Azure**.  

3. Na página dos **Serviços Azure** do Assistente de Serviços Azure:  

    1. Especifique um **nome** para o objeto no Gestor de Configuração.  

    2. Especifique uma **Descrição** opcional para o ajudar a identificar o serviço.  

    3. Selecione o serviço Azure que pretende ligar ao Gestor de Configuração.  

4. Selecione **Next** para continuar na página de propriedades da [aplicação Azure](#azure-app-properties) do Assistente de Serviços Azure.  


## <a name="azure-app-properties"></a>Propriedades de aplicativos Azure

Na página da **App** do Assistente de Serviços Azure, primeiro selecione o **ambiente Azure** da lista. Consulte a tabela em detalhes do [Serviço](#service-details) para o qual o ambiente está atualmente disponível para o serviço.

O resto da página da App varia consoante o serviço específico. Consulte a tabela em detalhes do [Serviço](#service-details) para saber qual o tipo de aplicação que o serviço utiliza e que ação pode utilizar.

- Se a aplicação apoiar tanto a importação como criar ações, **selecione Browse**. Esta ação abre o diálogo da [aplicação Server](#server-app-dialog) ou o diálogo da [Aplicação cliente.](#client-app-dialog)  

- Se a aplicação apenas apoiar a ação de importação, selecione **Import**. Esta ação abre o diálogo de [Aplicações de Importação (servidor)](#import-apps-dialog-server) ou o diálogo de [Aplicações de Importação (cliente)](#import-apps-dialog-client).

Depois de especificar as aplicações nesta página, selecione **Next** para continuar na página de [Configuração ou Descoberta](#configuration-or-discovery) do Assistente de Serviços Azure.

### <a name="web-app"></a>Aplicação Web

Esta aplicação é a *aplicação Web / API*do tipo AD Azure, também referida como uma aplicação de servidor no Gestor de Configuração.

#### <a name="server-app-dialog"></a>Diálogo de aplicativo do servidor

Quando selecionar **Browse** para a **aplicação Web** na página da App do Assistente de Serviços Azure, abre o diálogo da aplicação Server. Exibe uma lista que mostra as seguintes propriedades de quaisquer aplicações web existentes:

- Nome amigável do inquilino
- Nome amigável da aplicação
- Tipo de Serviço

Existem três ações que pode tomar a partir do diálogo da aplicação Server:

- Para reutilizar uma aplicação web existente, selecione-a a partir da lista.
- Selecione **Importar** para abrir o diálogo de [aplicações de importação](#import-apps-dialog-server).
- Selecione **Criar** para abrir o diálogo create [server application](#create-server-application-dialog).

Depois de selecionar, importar ou criar uma aplicação web, selecione **OK** para fechar o diálogo da aplicação Server. Esta ação regressa à página da [App](#azure-app-properties) do Assistente de Serviços Azure.

#### <a name="import-apps-dialog-server"></a>Diálogo de aplicativos de importação (servidor)

Quando seleciona **Import** a partir do diálogo da aplicação Server ou da página da App do Assistente de Serviços Azure, abre o diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação web Azure AD que já está criada no portal Azure. Importa metadados sobre aquela aplicação web para O Gestor de Configuração. Especifique as seguintes informações:

- **Nome do inquilino azure AD**
- **ID de Inquilino do Azure AD**
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID do cliente**
- **Chave Secreta**
- **Expiração da chave secreta**: Selecione uma data futura do calendário.
- **App ID URI**: Este valor tem de ser único no seu inquilino Azure AD. Está no sinal de acesso utilizado pelo cliente do Gestor de Configuração para solicitar o acesso ao serviço. Por predefinição, este valor é `https://ConfigMgrService`.  

Depois de introduzir as informações, selecione **Verificar**. Em seguida, selecione **OK** para fechar o diálogo de aplicações importadas. Esta ação regressa à página da [App](#azure-app-properties) do Assistente de Serviços Azure ou ao diálogo da [aplicação Server](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Criar o diálogo da aplicação do servidor

Quando seleciona **Criar** a partir do diálogo da aplicação Server, abre o diálogo da Aplicação Create Server. Esta página automatiza a criação de uma aplicação web em Azure AD. Especifique as seguintes informações:

- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL homePage**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por predefinição, este valor é `https://ConfigMgrService`.  
- **App ID URI**: Este valor tem de ser único no seu inquilino Azure AD. Está no sinal de acesso utilizado pelo cliente do Gestor de Configuração para solicitar o acesso ao serviço. Por predefinição, este valor é `https://ConfigMgrService`.  
- **Período**de validade da chave secreta : escolha 1 **ano** ou **2 anos** da lista de abandono. Um ano é o valor padrão.

Selecione **Iniciar sessão** para autenticar o Azure como utilizador administrativo. Estas credenciais não são guardadas pelo Diretor de Configuração. Esta persona não requer permissões no Gestor de Configuração, e não precisa de ser a mesma conta que gere o Assistente de Serviços Azure. Depois de autenticar com sucesso o Azure, a página mostra o Nome de **Inquilino AD Azure** para referência.

Selecione **OK** para criar a aplicação web em Azure AD e fechar o diálogo create server application. Esta ação regressa ao diálogo da [aplicação Server](#server-app-dialog).

> [!NOTE]
> Se tiver uma política de Acesso Condicional Azure AD definida e aplicável a **todas as aplicações Cloud** - deve excluir desta política a aplicação do Servidor criada. Para obter mais informações sobre como excluir aplicações específicas, consulte a Documentação de [Acesso Condicional da AD Azure.](https://docs.microsoft.com/azure/active-directory/conditional-access/)

### <a name="native-client-app"></a>Aplicativo Cliente Nativo

Esta aplicação é do tipo Azure AD *Native,* também referida como uma aplicação de cliente no Gestor de Configuração.

#### <a name="client-app-dialog"></a>Diálogo da Aplicação cliente

Quando seleciona **Browse** para a **aplicação Cliente Nativo** na página da App do Assistente de Serviços Azure, abre o diálogo da App do Cliente. Exibe uma lista que mostra as seguintes propriedades de quaisquer aplicações nativas existentes:

- Nome amigável do inquilino
- Nome amigável da aplicação
- Tipo de Serviço

Existem três ações que pode tomar a partir do diálogo da App do Cliente:

- Para reutilizar uma aplicação nativa existente, selecione-a a partir da lista. 
- Selecione **Importar** para abrir o diálogo de [aplicações de importação](#import-apps-dialog-client).
- Selecione **Criar** para abrir o [diálogo Create Client Application](#create-client-application-dialog).

Depois de selecionar, importar ou criar uma aplicação nativa, escolha **OK** para fechar o diálogo da App do Cliente. Esta ação regressa à página da [App](#azure-app-properties) do Assistente de Serviços Azure.

#### <a name="import-apps-dialog-client"></a>Diálogo de aplicativos de importação (cliente)

Ao selecionar **Import** a partir do diálogo da App cliente, abre o diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação nativa azure AD que já está criada no portal Azure. Importa metadados sobre aquela aplicação nativa para O Gestor de Configuração. Especifique as seguintes informações:

- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID do cliente**

Depois de introduzir as informações, selecione **Verificar**. Em seguida, selecione **OK** para fechar o diálogo de aplicações importadas. Esta ação regressa ao diálogo da [App do Cliente.](#client-app-dialog)

#### <a name="create-client-application-dialog"></a>Criar diálogo de aplicação de cliente

Quando seleciona **Criar** a partir do diálogo da App cliente, abre o diálogo da Aplicação Criar cliente. Esta página automatiza a criação de uma app nativa em Azure AD. Especifique as seguintes informações:

- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL de resposta**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por predefinição, este valor é `https://ConfigMgrService`.

Selecione **Iniciar sessão** para autenticar o Azure como utilizador administrativo. Estas credenciais não são guardadas pelo Diretor de Configuração. Esta persona não requer permissões no Gestor de Configuração, e não precisa de ser a mesma conta que gere o Assistente de Serviços Azure. Depois de autenticar com sucesso o Azure, a página mostra o Nome de **Inquilino AD Azure** para referência.

Selecione **OK** para criar a app nativa em Azure AD e fechar o diálogo Create Client Application. Esta ação regressa ao diálogo da [App do Cliente.](#client-app-dialog)

## <a name="configuration-or-discovery"></a>Configuração ou Descoberta

Depois de especificar as aplicações web e nativas na página apps, o Assistente de Serviços Azure procede a uma página de **Configuração** ou **Discovery,** dependendo do serviço ao qual está a ligar. Os detalhes desta página variam de serviço para serviço. Para mais informações, consulte um dos seguintes artigos:  

- **Serviço de Gestão de Nuvem,** página **Discovery:** [Configure Azure AD User Discovery](configure-discovery-methods.md#azureaadisc)  

- Serviço de **Conector De Log Analytics,** página **de configuração:** [Configure a ligação ao Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- **Microsoft Store para** serviço de negócios, página de **configurações:** [Configure Microsoft Store para sincronização de negócios](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Por fim, complete o Assistente de Serviços Azure através das páginas Resumo, Progresso e Conclusão. Completou a configuração de um serviço Azure em 'Gestor de Configuração'. Repita este processo para configurar outros serviços Azure.


## <a name="renew-secret-key"></a><a name="bkmk_renew"></a>Renovar a chave secreta

> [!Note]
> Para renovar a chave secreta de uma aplicação Azure na versão 1802 e anterior, precisa de recriar a app.

### <a name="renew-key-for-created-app"></a>Renovar a chave para a aplicação criada

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud,** e selecione o nó de **Inquilinos de Diretório Ativo Azure.**

1. No painel Details, selecione o inquilino Azure AD para a aplicação.

1. Na fita, **selecione Renovar a Chave Secreta**. Introduza as credenciais do proprietário da aplicação ou de um administrador da AD Azure.

### <a name="renew-key-for-imported-app"></a>Renovar a chave para app importada

Se importou a aplicação Azure em 'Gestor de Configuração', utilize o portal Azure para renovar. Repare na nova chave secreta e data de validade. Adicione esta informação sobre o assistente da **Chave Secreta Renovar.**  

> [!Note]  
> Guarde a chave secreta antes de fechar as propriedades da aplicação Azure **Página** chave. Esta informação é removida quando fecha a página.


## <a name="view-the-configuration-of-an-azure-service"></a>Ver a configuração de um serviço Azure

Consulte as propriedades de um serviço Azure que configurapara utilização. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud,** e selecione **Serviços Azure.** Selecione o serviço que pretende visualizar ou editar e, em seguida, selecione **Propriedades**.

Se selecionar um serviço e, em seguida, escolher **Apagar** na fita, esta ação elimina a ligação no 'Gestor de Configuração'. Não remove a aplicação em Azure AD. Peça ao seu administrador Azure para apagar a aplicação quando já não for necessária. Ou executar o Assistente de Serviço Azure para importar a app.<!--483440-->


## <a name="cloud-management-data-flow"></a>Fluxo de dados de gestão de nuvem

O diagrama seguinte é um fluxo de dados conceptual para a interação entre O Gestor de Configuração, AD Azure e serviços de nuvem conectados. Este exemplo específico utiliza o serviço **Cloud Management,** que inclui um cliente Windows 10, e aplicações de servidor estoque e cliente. Os fluxos para outros serviços são semelhantes.

![Diagrama de fluxo de dados para gestor de configuração com AD Azure e Gestão de Nuvem](media/aad-auth.png)

1. O administrador do Gestor de Configuração importa ou cria as aplicações de cliente e servidor em Azure AD.  

2. O método de descoberta do utilizador da AD do Gestor de Configuração Azure funciona. O site utiliza a aplicação do servidor Azure AD para consultar o Microsoft Graph para obter objetos de utilizador.  

3. O site armazena dados sobre os objetos do utilizador. Para mais informações, consulte a Descoberta do [Utilizador da AD Azure](about-discovery-methods.md#azureaddisc).  

4. O cliente do Gestor de Configuração solicita o token do utilizador Azure AD. O cliente faz a reclamação usando o ID de aplicação da aplicação de cliente Azure AD, e a aplicação do servidor como o público. Para mais informações, consulte [Reclamações em Fichas de Segurança da AD Azure](/azure/active-directory/develop/authentication-scenarios#security-tokens).  

5. O cliente autentica com o site apresentando o token Azure AD ao gateway de gestão de nuvem e no local https-habilitado ponto de gestão.  

Para obter informações mais detalhadas, consulte o fluxo de trabalho de [autenticação da Azure AD](../../../clients/manage/azure-ccmsetup.md).
