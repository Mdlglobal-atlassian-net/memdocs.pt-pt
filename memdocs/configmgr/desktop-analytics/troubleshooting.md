---
title: Resolver problemas da Análise de Computadores
titleSuffix: Configuration Manager
description: Detalhes técnicos para ajudá-lo a resolver problemas com desktop Analytics.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 46a320f4c6e32b57dc11beb325c34c300536381f
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693339"
---
# <a name="troubleshoot-desktop-analytics"></a>Resolver problemas da Análise de Computadores

Utilize os detalhes deste artigo para ajudá-lo a resolver problemas com desktop Analytics integrado com o Gestor de Configuração.

## <a name="confirm-prerequisites"></a>Confirmar pré-requisitos

Muitas questões comuns são causadas pela falta de pré-requisitos. Primeiro confirme as seguintes configurações:

- [Pré-requisitos](overview.md#prerequisites)  

- [Atualizações de componentes do Windows](enroll-devices.md#update-devices)  

- [Como permitir a partilha de dados,](enable-data-sharing.md)que abrange os seguintes tópicos:  

  - Pontos finais da Internet aos quais os clientes precisam de se conectar  

  - Autenticação do servidor proxy  

  - Níveis de dados de diagnóstico  

## <a name="monitor-connection-health"></a>Estado de funcionamento da ligação do monitor

Utilize o painel de **conexão Health** no Gestor de Configuração para reduzir as categorias pela saúde do dispositivo. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o nó de manutenção desktop **Analytics** e selecione o painel de assistência à saúde de **ligação.**  

Para mais informações, consulte [Monitor de saúde](monitor-connection-health.md)de ligação .

> [!NOTE]
> A ligação do Gestor de Configuração ao Desktop Analytics baseia-se no ponto de ligação do serviço. Quaisquer alterações na função do sistema do site podem ter impacto na sincronização com o serviço de nuvem. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

A partir da versão 2002, se o site do Gestor de Configuração não ligar aos pontos finais necessários para um serviço na nuvem, eleva uma mensagem de estado crítico ID 11488. Quando não consegue ligar-se ao serviço, o SMS_SERVICE_CONNECTOR o estado do componente muda para crítico. Ver estado detalhado no nó de [Estado do Componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) da consola 'Gestor de Configuração'.<!-- 5566763 -->

## <a name="log-files"></a>Ficheiros de registo

Para mais informações, consulte [ficheiros de registo para Desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

Começando na versão 1906 do Gestor de Configuração, utilize a ferramenta **DesktopAnalyticsLogsCollector.ps1** do diretor de instalação do Gestor de Configuração para ajudar a resolver o desktop Analytics. Executa alguns passos básicos de resolução de problemas e recolhe os registos relevantes num único diretório de trabalho. Para mais informações, consulte o colecionador de [Registos.](log-collector.md)

### <a name="enable-verbose-logging"></a>Ativar registo verboso

1. No ponto de ligação ao serviço, vá à seguinte chave de registo:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Definir o valor **loggingLevel** para`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Aplicações da AD Azure

O Desktop Analytics adiciona as seguintes aplicações ao seu Anúncio Azure:

- **Microserviço do Gestor de Configuração:** Conecta o Gestor de Configuração com desktop Analytics. Esta aplicação não tem requisitos de acesso.  

- **MALogAnalyticsReader**: Monitoriza o seu espaço de trabalho Azure Log Analytics para garantir que o instantâneo diário foi copiado com sucesso. Para mais informações, consulte a [função de aplicação MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- Administrador do **cliente Office365**: Permite a recuperação do Gestor de Configuração de informações do plano de implementação e o estado de prontidão do dispositivo a partir do Desktop Analytics.

Se precisar de fornecer estas aplicações depois de concluir a configuração, vá ao painel de **serviços Connected.** **Selecione Configure utilizadores e apps acedam**e disponibilizem as aplicações.  

- **Aplicativo Azure AD para Gestor**de Configuração . Se precisar de fornecer ou resolver problemas de ligação após completar a configuração, consulte a [aplicação Create and import para O Gestor](#create-and-import-app-for-configuration-manager)de Configuração . Esta aplicação requer **a Escrita de Dados** de Recolha cm e leia os dados de recolha de **CM** na API do Serviço de Gestor **de Configuração.**  

### <a name="create-and-import-app-for-configuration-manager"></a>Criar e importar aplicativo para Gestor de Configuração

Se não conseguir criar a aplicação Azure AD para Configuração do assistente do Serviço Configure Azure, ou se quiser reutilizar uma aplicação existente, precisa criá-la e importar manualmente. Depois de concluir o [embarque inicial](set-up.md#initial-onboarding) no portal Desktop Analytics, utilize os seguintes passos:

#### <a name="create-app-in-azure-ad"></a>Criar app em Azure AD

1. Abra o [portal Azure](https://portal.azure.com) como utilizador com permissões *Global Admin,* vá ao **Azure Ative Directory,** e selecione registos de **Aplicações.** Em seguida, selecione **Nova inscrição**.  

2. No painel **Criar,** configure as seguintes definições:  

    - **Nome**: um nome único que identifica a aplicação, por exemplo:`Desktop-Analytics-Connection`  

    - Tipos de **conta suportada**: **Contas apenas neste diretório organizacional (Contoso)**

    - **Redirecionar URI (opcional)**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selecione **Registar**.  

3. Selecione a aplicação, note o ID da **Aplicação (cliente)** e **o Id do Diretório (inquilino).** Os valores são GUIDs que são usados para configurar a ligação do Gestor de Configuração.  

4. No menu **Gerir,** selecione **Certificados & segredos.** Selecione **Novo segredo do cliente**. Introduza uma **Descrição,** especifique uma duração de validade e, em seguida, **selecione Adicionar**. Copie o **Valor** da chave, que é usada para configurar a ligação 'Gestor de Configuração'.

    > [!Important]  
    > Esta é a única oportunidade para copiar o valor-chave. Se não o copiaragora, tem de criar outra chave.  
    >
    > Guarde o valor-chave num local seguro.  

5. No menu **Gerir,** selecione **permissões API**.  

    1. No painel de **permissões DaPI,** selecione **Adicionar uma permissão**.  

    2. No painel **de permissões Request API,** mude para APIs que **a minha organização utiliza.**  

    3. Procure e selecione a API microserviço do Gestor de **Configuração.**  

    4. Selecione o grupo de **permissões de aplicação.** Expandir **cmCollectionData**, e selecionar ambas as seguintes permissões: Escrever dados de **recolha cm** e ler dados de recolha **cm**.  

    5. **Selecione Adicionar permissões**.  

6. No painel de **permissões da API,** selecione **grant administrador consentimento...**. Selecione **Sim**.  

#### <a name="import-app-in-configuration-manager"></a>App de importação em Gestor de Configuração

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** **Selecione Configure Azure Services** na fita.  

2. Na página de **Serviços Azure** do Assistente de Serviços Azure, configure as seguintes definições:  

    - Especifique um **nome** para o objeto no Gestor de Configuração.  

    - Especifique uma **Descrição** opcional para o ajudar a identificar o serviço.  

    - Selecione **Desktop Analytics** da lista de serviços disponíveis.  
  
   Selecione **Seguinte**.  

3. Na página da **App,** selecione o **ambiente Azure**apropriado . Em seguida, selecione **Import** para a aplicação web. Configure as seguintes definições na janela **Aplicações de Importação:**  

    - Nome do **inquilino Azure AD**: Este nome é como é nomeado em Gerente de Configuração  

    - **Id do Inquilino Azure AD**: A ID do **Diretório** que copiou da Azure AD  

    - **ID do cliente**: O ID de **aplicação** que copiou da aplicação Azure AD  

    - **Chave Secreta**: O **valor** chave que copiou da aplicação Azure AD  

    - **Expiração da chave secreta**: A mesma data de validade da chave  

    - **Id da aplicação URI**: Esta definição deve povoar automaticamente com o seguinte valor:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verificar**e, em seguida, selecione **OK** para fechar a janela Aplicações de Importação. Selecione **Next** na página da App do Assistente de Serviços Azure.  

Para continuar o resto do assistente na página de Dados de **Diagnóstico,** consulte [Ligar ao serviço](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>App de resolução de problemas no Gestor de Configuração

Se tiver problemas em criar ou importar a app, verifique primeiro **o SMSAdminUI.log** para o erro específico. Em seguida, verifique as seguintes configurações:

- Inscreveu com sucesso o inquilino no serviço desktop Analytics. Para mais informações, consulte [Como configurar desktop Analytics](set-up.md).

- Todos os pontos finais necessários são acessíveis. Para mais informações, consulte [Pontos Finais](enable-data-sharing.md#endpoints).

- Certifique-se de que o utilizador que faz o insígnio tem as permissões corretas. Para mais informações, consulte [os pré-requisitos.](overview.md#prerequisites)

- Certifique-se de que o utilizador pode iniciar sessão no Azure em geral. Esta ação determina se existem problemas gerais de autenticação da AD Azure.

- Verifique as mensagens de estado do componente **SMS_SERVICE_CONNECTOR** relativamente ao trabalhador desktop *Analytics*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a>Função de aplicação MALogAnalyticsReader

Quando configurar o Desktop Analytics, consinta em nome da sua organização. Este consentimento é atribuir à aplicação MALogAnalyticsReader a função Log Analytics Reader para o espaço de trabalho. Esta função de aplicação é exigida pelo Desktop Analytics.

Se houver algum problema com este processo durante a configuração, utilize o seguinte processo para adicionar manualmente esta permissão:

1. Vá ao [portal Azure](https://portal.azure.com)e selecione **Todos os recursos.** Selecione o espaço de trabalho do tipo **Log Analytics**.  

2. No menu espaço de trabalho, selecione **o controlo de acesso (IAM)** e, em seguida, selecione **Adicionar**.  

3. No painel **adicionar permissões,** configure as seguintes definições:  

    - **Função**: **Leitor**  

    - **Atribuir acesso a:** **Utilizador, grupo ou aplicação Azure AD**  

    - **Selecione**: **MALogAnalyticsReader**  

4. Selecione **Guardar**.

O portal mostra uma notificação de que acrescentou a atribuição do papel.

## <a name="data-latency"></a>Latência de dados

<!-- 3846531 -->
Quando configurar pela primeira vez o Desktop Analytics, inscrever novos clientes ou configurar novos planos de implementação, os relatórios no Configurmanager e no portal Desktop Analytics podem não mostrar imediatamente os dados completos. Pode levar 2 a 3 dias para que os seguintes passos ocorram:

- Dispositivos ativos enviam dados de diagnóstico para o serviço Desktop Analytics
- O serviço processa os dados
- O serviço sincroniza com o site do Gestor de Configuração

Ao sincronizar as coleções de dispositivos da hierarquia do Gestor de Configuração para desktop Analytics, pode demorar até uma hora para que essas coleções apareçam no portal Desktop Analytics. Da mesma forma, quando se cria um plano de implementação no Desktop Analytics, pode demorar até uma hora para que as novas coleções associadas ao plano de implementação apareçam na hierarquia do Gestor de Configuração. Os sites primários criam as coleções, e o site da administração central sincroniza com desktop Analytics. O Gestor de Configuração pode demorar até 24 horas a avaliar e atualizar a adesão à recolha. Para acelerar este processo, atualize manualmente a adesão à recolha.<!-- 4984639 -->

> [!Note]
> Para que as atualizações de recolha manual reflitam alterações, o componente SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker primeiro precisa de sincronizar. Pode levar até uma hora para este processo funcionar. Para mais informações, consulte o **M365ADeploymentPlanWorker.log**.

Dentro do portal Desktop Analytics, existem dois tipos de dados: Dados do **administrador** e **dados de diagnóstico:**

- **Os dados do administrador** referem-se a quaisquer alterações que então faça à configuração do espaço de trabalho. Por exemplo, quando muda a **Decisão** ou **Importância** de um ativo, está a alterar os dados do administrador. Estas alterações têm frequentemente um efeito de compostagem, uma vez que podem alterar o estado de prontidão de um dispositivo com o ativo em questão instalado.

- **Os dados** de diagnóstico referem-se aos metadados do sistema enviados de dispositivos clientes para a Microsoft. Estes dados são potenciados pelo Desktop Analytics. Inclui atributos como o inventário do dispositivo, segurança e estado de atualização de funcionalidades.

Por padrão, todos os dados do portal Desktop Analytics são automaticamente atualizados diariamente. Esta atualização inclui alterações nos dados de diagnóstico e quaisquer alterações que faça na configuração (dados do administrador). Deve estar visível no seu portal Desktop Analytics até às 08:00 UTC todos os dias.

Ao efazer alterações aos dados do administrador, pode desencadear uma atualização a pedido dos dados do administrador no seu espaço de trabalho. A partir de qualquer página do portal Desktop Analytics, abra o flyout da moeda de dados:

![Screenshot do separador flyout da moeda de dados no portal Desktop Analytics](media/data-currency-flyout.png)

Em seguida, selecione **Alterações de aplicação:**

![Screenshot da moeda de dados expandida voa para fora no portal Desktop Analytics](media/data-currency-flyout-expand.png)

Este processo geralmente demora entre 15 a 60 minutos. O tempo depende da dimensão do seu espaço de trabalho e do âmbito das alterações que precisam de processos. Quando solicita uma atualização de dados a pedido, não resulta em alterações nos dados de diagnóstico.  Para mais informações, consulte o [Desktop Analytics FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se não estiver a ver alterações atualizadas dentro dos prazos acima indicados, aguarde mais 24 horas para a próxima atualização diária. Se vir atrasos mais longos, verifique o painel de saúde do serviço. Se o serviço for saudável, contacte o suporte da Microsoft.<!-- 3896921 -->

> [!IMPORTANT]
> A opção Desktop Analytics para **ver dados recentes** é depreciada. Esta ação será removida num futuro lançamento do serviço Desktop Analytics. Para mais informações, consulte [as funcionalidades deprecatadas.](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)<!--7080949-->  
