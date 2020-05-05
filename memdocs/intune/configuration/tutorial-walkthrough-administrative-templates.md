---
title: Walkthrough - Criar modelo administrativo no Microsoft Intune - Azure [ Microsoft Docs
description: Este tutorial ou walkthrough utiliza o Microsoft Intune para configurar os modelos De Office, Windows e Microsoft Edge ADMX no Windows 10 e dispositivos mais recentes.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/31/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41a2dce895761053e482fe029e4599819a099ac6
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254865"
---
# <a name="tutorial-use-the-cloud-to-configure-group-policy-on-windows-10-devices-with-admx-templates-and-microsoft-intune"></a>Tutorial: Use a nuvem para configurar a política de grupo em dispositivos Windows 10 com modelos ADMX e Microsoft Intune

> [!NOTE]
> Este tutorial foi criado como um workshop técnico para a Microsoft Ignite. Tem mais pré-requisitos do que os tutoriais típicos, uma vez que compara a utilização e configuração de políticas ADMX em Intune e no local.

Os modelos administrativos da política do grupo, também conhecidos como modelos ADMX, incluem configurações que pode configurar em dispositivos Windows 10, incluindo Computadores. As definições do modelo ADMX estão disponíveis por diferentes serviços. Estas definições são utilizadas por fornecedores de Gestão de Dispositivos Móveis (MDM), incluindo o Microsoft Intune. Por exemplo, pode ligar ideias de design no PowerPoint, definir uma página inicial no Microsoft Edge, bloquear controlos ActiveX no Internet Explorer e muito mais.

Os modelos ADMX estão disponíveis para os seguintes serviços:

- **Microsoft Edge**: Descarregue no [ficheiro de política do Microsoft Edge](https://www.microsoftedgeinsider.com/en-us/enterprise).
- **Office**: Download at [Microsoft 365 Apps, Office 2019, and Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).
- **Janelas**: Incorporado no Sistema Operativo Windows 10.

Para obter mais informações sobre as políticas da ADMX, consulte [a compreensão das políticas apoiadas pela ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies).

Estes modelos são incorporados no Microsoft Intune, e estão disponíveis como perfis de **modelos administrativos.** Neste perfil, configura as definições que pretende incluir e, em seguida, "atribui" este perfil aos seus dispositivos.

Neste tutorial, irá:

> [!div class="checklist"]
> * Ser apresentado ao centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
> * Crie grupos de utilizadores e crie grupos de dispositivos.
> * Compare as definições em Intune com as definições ADMX no local.
> * Crie diferentes modelos administrativos e configure as configurações que visam os diferentes grupos.

No final deste laboratório, terá as habilidades para começar a usar Intune e Microsoft 365 para gerir os seus utilizadores e implementar modelos administrativos.

Esta funcionalidade aplica-se a:

- Windows 10 versão 1709 e mais recente

## <a name="prerequisites"></a>Pré-requisitos

- Uma subscrição Microsoft 365 E3 ou E5, que inclui o prémio Intune e Azure Ative Directory (AD). Se não tiver uma assinatura E3 ou E5, [experimente de graça.](https://docs.microsoft.com/office365/admin/try-or-buy-microsoft-365?view=o365-worldwide)

  Para obter mais informações sobre o que obtém com as diferentes licenças da Microsoft 365, consulte [Transform your Enterprise com o Microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans).

- O Microsoft Intune está configurado como **intune MDM Authority**. Para mais informações, consulte Definir a autoridade de [gestão de dispositivos móveis](../fundamentals/mdm-authority-set.md).

  > [!div class="mx-imgBorder"]
  > ![Defina a autoridade do MDM para a Microsoft Intune no seu estatuto de inquilino](./media/tutorial-walkthrough-administrative-templates/tenant-status.png)

- Num controlador de domínio ative diretório no local (DC):

  1. Copie os seguintes modelos de Office e Microsoft Edge para a [Central Store (pasta sysvol)](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra):

      - [Modelos administrativos de escritório](https://www.microsoft.com/download/details.aspx?id=49030)
      - [Modelos administrativos do Microsoft Edge > Ficheiro de Política](https://www.microsoftedgeinsider.com/en-us/enterprise)

  2. Crie uma política de grupo para empurrar estes modelos para um computador administrador da Empresa Windows 10 no mesmo domínio que o DC. Neste tutorial:

      - A política de grupo que criamos com estes modelos chama-se **OfficeandEdge**. Verá este nome nas imagens.
      - O computador administrador da Empresa Windows 10 que utilizamos chama-se **computador Admin**.

      Em algumas organizações, um administrador de domínio tem duas contas:  
        - Uma conta de trabalho de domínio típica
        - Uma conta de administrador de domínio diferente usada apenas para tarefas de administrador de domínio, como a política do grupo

      O objetivo deste **computador Admin** é que os administradores assinem com a sua conta de administrador de domínio, e ferramentas de acesso concebidas para gerir a política do grupo.

- Neste **computador De administração:**

  - Inscreva-se numa conta de Administrador de Domínio.

  - Instalar o **RSAT: Ferramentas**de Gestão de Políticas do Grupo:

    1. Abra a aplicação **Definições** > **Apps** > **Opcionais Funcionalidades Adicionais.** > **Add feature**
    2. Selecione **RSAT:** > **Instalação**de ferramentas de gestão de políticas de grupo .

        Espere enquanto o Windows instala a funcionalidade. Quando estiver concluído, acaba por aparecer na aplicação **Windows Administrative Tools.**

        > [!div class="mx-imgBorder"]
        > ![Aplicativos de Ferramentas Administrativas do Windows, incluindo app de Gestão de Políticas de Grupo](./media/tutorial-walkthrough-administrative-templates/windows-administrative-tools-app.png)

  - Certifique-se de que tem acesso à Internet e direitos de administrador da subscrição microsoft 365, que inclui o centro de administração do Endpoint Manager.

## <a name="open-the-endpoint-manager-admin-center"></a>Abra o centro de administração do Endpoint Manager

1. Abra um navegador web de crómio, como a versão 77 do Microsoft Edge e mais tarde.
2. Vá ao centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Inscreva-se com a seguinte conta:

    **Utilizador**: Insira a conta de administrador da sua subscrição de inquilino Microsoft 365.  
    **Palavra-passe**: Introduza a sua palavra-passe.

Este centro de administração está focado na gestão de dispositivos, e inclui serviços Azure, como Azure AD e Intune. Pode não ver o **Diretório Ativo Azure** e a marca **Intune,** mas está a usá-los.

Também pode abrir o centro de administração endpoint manager do centro de administração Microsoft [365:](https://admin.microsoft.com)

1. Vai [https://admin.microsoft.com](https://admin.microsoft.com)para.
2. Inscreva-se na conta de administrador da sua subscrição de inquilino Microsoft 365.
3. Sob **os centros de Administração,** selecione Todos os centros > de **administração****Endpoint management**. O centro de administração do Endpoint Manager abre.

    > [!div class="mx-imgBorder"]
    > ![Veja todos os centros de administração do centro de administração da Microsoft 365](./media/tutorial-walkthrough-administrative-templates/microsoft365-admin-centers.png)

## <a name="create-groups-and-add-users"></a>Criar grupos e adicionar utilizadores

As políticas no local são aplicadas na ordem LSDOU - local, local, domínio e unidade organizacional (OU). Nesta hierarquia, as políticas da Usobres a política local, as políticas de domínio sobreporem as políticas do site, e assim por diante.

Intune, as políticas são aplicadas aos utilizadores e grupos que cria. Não há uma hierarquia. Se duas políticas atualizarem a mesma definição, então a definição mostra-se como um conflito. Se duas políticas de conformidade estiverem em conflito, então aplica-se a política mais restritiva. Se dois perfis de configuração estiverem em conflito, então a definição não é aplicada. Para obter mais informações, consulte [questões comuns, questões e resoluções com políticas e perfis de dispositivos.](device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied)

Nestes próximos passos, você vai criar grupos de segurança, e adicionar utilizadores a estes grupos. Pode adicionar um utilizador a vários grupos. Por exemplo, é normal que um utilizador tenha vários dispositivos, como um Surface Pro para trabalho, e um dispositivo móvel Android para pessoal. E é normal uma pessoa aceder a recursos organizacionais a partir destes múltiplos dispositivos.

1. No centro de administração do Endpoint Manager, selecione **Grupos** > **Novo grupo**.

2. Introduza as seguintes definições:

    - **Tipo de grupo**: Selecione **Segurança**.
    - **Nome do grupo**: Insira **todos os dispositivos estudantis do Windows 10**.
    - **Tipo de membro**: Selecione **Atribuído**.

3. Selecione **Membros**e adicione alguns dispositivos.

    Adicionar dispositivos é opcional. O objetivo é praticar a criação de grupos e saber adicionar dispositivos. Se está a usar este tutorial num ambiente de produção, então esteja ciente do que está a fazer.

4. **Selecione** > **Criar** para guardar as suas alterações.

    Não vê o seu grupo? Selecione **Refresh**.

5. Selecione **Novo grupo**e introduza as seguintes definições:

    - **Tipo de grupo**: Selecione **Segurança**.
    - **Nome do grupo**: Introduza **todos os dispositivos Windows**.
    - **Tipo de membro**: Selecione **Dispositivo Dinâmico**.
    - **Membros do dispositivo dinâmico**: Selecione **Adicionar consulta dinâmica,** e configurar a sua consulta:

        - **Propriedade**: Selecione **dispositivoOSType**.
        - **Operador**: Selecione **Iguais**.
        - **Valor**: Introduza **janelas**.

        1. Selecione **Adicionar expressão**. A sua expressão é mostrada na **sintaxe**da regra:

            > [!div class="mx-imgBorder"]
            > ![Crie uma consulta dinâmica e adicione expressão no modelo administrativo Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/dynamic-group-query.png)

            Quando os utilizadores ou dispositivos cumprem os critérios em que entra, são automaticamente adicionados aos grupos dinâmicos. Neste exemplo, os dispositivos são automaticamente adicionados a este grupo quando o sistema operativo é windows. Se está a usar este tutorial num ambiente de produção, então tenha cuidado. O objetivo é praticar a criação de grupos dinâmicos.

        2. **Guarde** > a**Create** para salvar as suas alterações.

6. Crie o grupo **All Teachers** com as seguintes definições:

    - **Tipo de grupo**: Selecione **Segurança**.
    - **Nome do grupo**: Insira **Todos os Professores**.
    - **Tipo de membro**: Selecione **Utilizador Dinâmico**.
    - **Membros dinâmicos do utilizador**: Selecione **Adicionar consulta dinâmica,** e configurar a sua consulta:

      - **Propriedade**: Selecione **departamento**.
      - **Operador**: Selecione **Iguais**.
      - **Valor**: Entrar **professores**.

        1. Selecione **Adicionar expressão**. A sua expressão é mostrada na **sintaxe**da Regra.

            Quando os utilizadores ou dispositivos cumprem os critérios em que entra, são automaticamente adicionados aos grupos dinâmicos. Neste exemplo, os utilizadores são automaticamente adicionados a este grupo quando o seu departamento é Professores. Pode entrar no departamento e outras propriedades quando os utilizadores forem adicionados à sua organização. Se está a usar este tutorial num ambiente de produção, então tenha cuidado. O objetivo é praticar a criação de grupos dinâmicos.

        2. **Guarde** > a**Create** para salvar as suas alterações.

### <a name="talking-points"></a>Pontos de conversa

- Grupos dinâmicos são uma característica no Azure AD Premium. Se não tem O Azure AD Premium, então está licenciado para criar apenas grupos atribuídos. Para obter mais informações sobre grupos dinâmicos, consulte:

  - [Associação dinâmica do grupo no Diretório Ativo Azure (Parte 1)](https://blogs.technet.microsoft.com/pauljones/2017/08/28/dynamic-group-membership-in-azure-active-directory-part-1/)
  - [Associação dinâmica do grupo no Diretório Ativo Azure (Parte 2)](https://blogs.technet.microsoft.com/pauljones/2017/08/29/dynamic-group-membership-in-azure-active-directory-part-2/)

- O Azure AD Premium inclui outros serviços que são comumente utilizados na gestão de apps e dispositivos, incluindo [a autenticação de vários fatores (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) e [o acesso condicional.](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- Muitos administradores perguntam quando usar grupos de utilizadores e quando usar grupos de dispositivos. Para obter alguma orientação, consulte [grupos de utilizador vs. grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).

- Lembre-se, um utilizador pode pertencer a vários grupos. Considere alguns dos outros grupos dinâmicos de utilizador e dispositivo que pode criar, tais como:

  - Todos os Alunos
  - Todos os dispositivos Android
  - Todos os dispositivos iOS/iPadOS
  - Marketing
  - Recursos Humanos
  - Todos os empregados da Charlotte
  - Todos os empregados redmond
  - Administradores de TI da costa oeste
  - Administradores de TI da costa leste

Os utilizadores e grupos criados também são vistos no centro de administração da [Microsoft 365,](https://admin.microsoft.com)Azure AD no portal Azure, e [Microsoft Intune no portal Azure](https://go.microsoft.com/fwlink/?linkid=2090973). Você pode criar e gerir grupos em todas estas áreas para a sua subscrição de inquilino. **Se o seu objetivo é a gestão do dispositivo, utilize o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)**.

### <a name="review-group-membership"></a>Rever associação ao grupo

1. No centro de administração do Endpoint Manager, selecione **Utilizadores** > selecionar o nome de qualquer utilizador existente.

    > [!div class="mx-imgBorder"]
    > ![No centro de administração do Endpoint Manager, selecione Utilizadores](./media/tutorial-walkthrough-administrative-templates/select-users-endpoint-manager-admin-center.png)

2. Reveja algumas das informações que pode adicionar ou alterar. Por exemplo, veja as propriedades que pode configurar, tais como Job Title, Department, City, Office location, e muito mais. Você pode usar estas propriedades em suas consultas dinâmicas ao criar grupos dinâmicos.
3. Selecione **Grupos** para ver a adesão deste utilizador. Também pode remover o utilizador de um grupo.
4. Selecione algumas das outras opções para ver mais informações e o que pode fazer. Por exemplo, veja a licença atribuída, os dispositivos do utilizador e muito mais.

### <a name="what-did-i-just-do"></a>O que acabei de fazer?

No centro de administração do Endpoint Manager, criou novos grupos de segurança e adicionou utilizadores e dispositivos existentes a estes grupos. Usaremos estes grupos em etapas posteriores neste tutorial.

## <a name="create-a-template-in-intune"></a>Criar um modelo em Intune

Nesta secção, criamos um modelo administrativo em Intune, olhamos para algumas configurações na **Gestão de Políticas**de Grupo, e comparamos a mesma configuração em Intune. O objetivo é mostrar um cenário na política de grupo, e mostrar o mesmo cenário em Intune.

1. No centro de administração do Endpoint Manager, selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
2. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Perfil**: Selecionar **modelos administrativos**.

3. Selecione **Criar**.
4. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, introduza o **modelo De Administrador - Dispositivos estudantis do Windows 10**.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

5. Selecione **Seguinte**.
6. Nas definições de **configuração,** as definições aplicam-se aos dispositivos **(configuração do computador)** e as definições aplicam-se aos utilizadores **(configuração do utilizador):**

    > [!div class="mx-imgBorder"]
    > ![Aplicar as definições do modelo ADMX aos utilizadores e dispositivos no Microsoft Intune Endpoint Manager](./media/tutorial-walkthrough-administrative-templates/administrative-templates-choose-computer-user-configuration.png)

7. Expandir **a configuração do** > computador**Microsoft Edge** > selecione **as definições do SmartScreen**. Note o caminho para a apólice e todas as definições disponíveis:

    > [!div class="mx-imgBorder"]
    > ![Consulte as definições de política do Microsoft Edge SmartScreen nos modelos ADMX no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-path.png)

8. Em busca, insira **o download**. Note que as definições de política são filtradas:

    > [!div class="mx-imgBorder"]
    > ![Filtrar as definições de política do Microsoft Edge SmartScreen no modelo INTune ADMX da Microsoft](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-search-download.png)

### <a name="open-group-policy-management"></a>Gestão de Políticas de Grupo Aberto

Nesta secção, mostramos uma política em Intune e a sua política de correspondência no Editor de Gestão de Políticas de Grupo.

#### <a name="compare-a-device-policy"></a>Compare uma política de dispositivos

1. No **computador DaAdministração,** abra a app de Gestão de Políticas do **Grupo.**

    Esta aplicação é instalada com **RSAT: Ferramentas**de Gestão de Políticas de Grupo, que é uma funcionalidade opcional que instala no Windows. [Os pré-requisitos](#prerequisites) (neste artigo) listam os passos para instalá-lo.

2. Expandir **domínios** > selecione o seu domínio. Por exemplo, selecione **contoso.net**.
3. Clique à direita na política **do OfficeandEdge** > **Editar**. A aplicação Group Policy Management Editor abre.

    > [!div class="mx-imgBorder"]
    > ![Clique na política do grupo Office e Microsoft Edge ADMX e selecione Editar](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management.png)

    **OfficeandEdge** é uma política de grupo que inclui os modelos Office e Microsoft Edge ADMX. Esta política é descrita em [pré-requisitos](#prerequisites) (neste artigo).

4. Expandir políticas de **configuração** > do computador**Políticas** > de**controlo** > de**modelos administrativos** > **Personalização**do Painel de Controlo . Repare nas definições disponíveis.

    > [!div class="mx-imgBorder"]
    > ![Expandir a Configuração de Computador estoque em Editor de Gestão de Políticas de Grupo, e ir para personalização](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management-editor-admx-policy.png)

    Clique duas vezes Para prevenir a câmara de **bloqueio,** e ver as opções disponíveis:

    > [!div class="mx-imgBorder"]
    > ![Consulte as opções de definição de configuração do Computador na política do grupo](./media/tutorial-walkthrough-administrative-templates/prevent-enabling-lock-screen-camera-admx-policy.png)

5. No centro de administração do Endpoint Manager, vá ao seu **modelo de dispositivos de estudante do Windows 10.**
6. Selecione**Personalização**do**Painel** > de Controlo de **Configuração** > do Computador . Note as definições disponíveis:

    > [!div class="mx-imgBorder"]
    > ![O caminho de definição da política de personalização no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/computer-configuration-control-panel-personalization-path.png)

    O tipo de definição é **Dispositivo,** e o caminho é **/Painel de Controlo/Personalização**. Este caminho é semelhante ao que acabou de ver no Editor de Gestão de Políticas do Grupo. Se abrir a definição de câmara de **ecrã de bloqueio Prevent,** verá as mesmas opções **Não configuradas**, **Ativadas**e **Desativadas** que vê no Editor de Gestão de Políticas do Grupo.

#### <a name="compare-a-user-policy"></a>Compare uma política de utilizador

1. No seu modelo de administração, selecione **configuração** > do computador**Todas as definições,** e procure a **navegação inprivada**. Reparem no caminho.

    Faça o mesmo para **a configuração do Utilizador**. Selecione **todas as definições**e procure **navegação inprivada**.

2. No Editor de **Gestão de Políticas**do Grupo, encontre as definições correspondentes do utilizador e do dispositivo:

    - Dispositivo: Expandir políticas de **configuração** > do computador**Modelos** > **administrativos** > **Windows components** > Componentes do Windows**Internet Explorer** > **Privacidade** > **desligue a navegação privada**.
    - Utilizador: Expandir políticas de **configuração** > do utilizador**Modelos** > **administrativos** > **Windows components** > Componentes do Windows**Internet Explorer** > **Privacidade** > **desligue a navegação privada**.

    > [!div class="mx-imgBorder"]
    > ![Desligue a navegação privada no Internet Explorer usando o modelo ADMX](./media/tutorial-walkthrough-administrative-templates/group-policy-turn-off-inprivate-browsing.png)

> [!TIP]
> Para ver as políticas incorporadas do Windows, também pode utilizar o GPEdit ( App de política de**grupo Editar).**

#### <a name="compare-an-edge-policy"></a>Compare uma política edge

1. No centro de administração do Endpoint Manager, vá ao seu **modelo de dispositivos de estudante do Windows 10.**
2. Expanda a **configuração** > do computador**Microsoft Edge** > **Startup, página inicial e nova página de separadores**. Repare nas definições disponíveis.

    Faça o mesmo para **a configuração do Utilizador**.

3. No Editor de Gestão de Políticas do Grupo, encontre estas definições:

    - Dispositivo: Expandir políticas de **configuração** > de computador**Modelos** > **Administrativos** > **Microsoft Edge** > **Startup, página inicial e nova página de separador**.
    - Utilizador: Expandir**as políticas** > de **configuração** > do utilizador**Modelos Administrativos** > **Microsoft Edge** > **Startup, página inicial e nova página de separador**

### <a name="what-did-i-just-do"></a>O que acabei de fazer?

Criou um modelo administrativo em Intune. Neste modelo, analisámos algumas definições de ADMX e analisámos as mesmas definições de ADMX na Gestão de Políticas de Grupo.

## <a name="add-settings-to-the-students-admin-template"></a>Adicione as definições ao modelo de administração dos Estudantes

Neste modelo, configuramos algumas definições do Internet Explorer para bloquear dispositivos partilhados por vários alunos.

1. No seu **modelo de Administrador - Dispositivos de estudante do Windows 10,** expandir a **configuração do Computador,** selecionar **todas as definições**e procurar **desativar a navegação privada:**

    > [!div class="mx-imgBorder"]
    > ![Desligue a política de dispositivos de navegação privada em modelo administrativo no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/turn-off-inprivate-browsing-administrative-template.png)

2. Selecione a definição de **desligação de navegação privada.** Nesta janela, repare na descrição e valores que pode definir. Estas opções são semelhantes às que se vê na política de grupo.
3. Selecione **Enabled** > **OK** para guardar as suas alterações.
4. Configure também as seguintes definições do Internet Explorer. Certifique-se de que seleciona **OK** para guardar as suas alterações.

    - **Permitir ficheiros de arrastar e largar ou copiar e colar**
      - **Tipo**: Dispositivo
      - **Caminho**: \Windows Components\Internet Explorer\Internet Control Panel\Security Page\Internet Zone
      - **Valor**: Deficiente

    - **Evite ignorar erros de certificado**
      - **Tipo**: Dispositivo
      - **Caminho**: \Windows Components\Internet Explorer\Internet Control Panel
      - **Valor**: Habilitado

    - **Desativar as definições da página inicial**
      - **Tipo**: Utilizador
      - **Caminho**: \Windows Components\Internet Explorer
      - **Valor**: Habilitado
      - **Página inicial**: Introduza `contoso.com`um URL, como .

5. Limpe o filtro de pesquisa. Note que as definições configuradas estão listadas no topo:

    > [!div class="mx-imgBorder"]
    > ![As definições configuradas estão listadas no topo no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/configured-settings-administrative-template.png)

### <a name="assign-your-template"></a>Atribuir o seu modelo

1. No seu modelo, selecione **Next** até chegar às **Atribuições**. Escolha **selecionar grupos para incluir:**

    > [!div class="mx-imgBorder"]
    > ![Selecione o seu perfil de modelo administrativo na lista de perfis de configuração do dispositivo no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/filter-administrative-template-device-configuration-profiles-list.png)

2. É apresentada uma lista de utilizadores e grupos existentes. Selecione o grupo de **dispositivos estudantis All Windows 10** que criou anteriormente > **Select**.

    Se você está usando este tutorial em um ambiente de produção, então considere adicionar grupos que estão vazios. O objetivo é praticar a atribuição do seu modelo.

3. Selecione **Seguinte**. Em **Rever + criar**, selecione **Criar** para guardar as suas alterações.

Assim que o perfil é guardado, aplica-se aos dispositivos quando fazem o check-in com o Intune. Se os dispositivos estiverem ligados à internet, pode acontecer imediatamente. Para obter mais informações sobre os tempos de atualização da política, veja quanto tempo leva para os [dispositivos obterem uma política, perfil ou app depois](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)de atribuídos .

Ao atribuir políticas e perfis rigorosos ou restritivos, não se tranque. Considere criar um grupo que esteja excluído das suas políticas e perfis. A ideia é ter acesso a problemas. Monitorize este grupo para confirmar que está a ser usado como pretendido.

### <a name="what-did-i-just-do"></a>O que acabei de fazer?

No centro de administração do Endpoint Manager, criou um perfil de configuração de modelo administrativo e atribuiu este perfil a um grupo que criou.

## <a name="create-a-onedrive-template"></a>Criar um modelo OneDrive

Nesta secção, cria-se um modelo de administração OneDrive em Intune para controlar algumas definições. Estas configurações específicas são escolhidas porque são comumente usadas pelas organizações.

1. Criar outro perfil **(Perfis** > de configuração de**dispositivos** > **Criar perfil).**

2. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Perfil**: Selecione **modelos administrativos**.

3. Selecione **Criar**.
4. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza **o modelo De Administrador - As políticas OneDrive que se aplicam a todos os utilizadores do Windows 10**.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

5. Selecione **Seguinte**.
6. Nas definições de **Configuração,** configure as seguintes definições. Certifique-se de selecionar **OK** para guardar as suas alterações.:

    - **Configuração do** > computador**Todas as definições:**
      - **Inscreva-se silenciosamente nos utilizadores do cliente sincronizado OneDrive com as suas credenciais Windows**
        - **Tipo**: Dispositivo
        - **Valor**: Habilitado
      - **Use ficheiros OneDrive a pedido**
        - **Tipo**: Dispositivo
        - **Valor**: Habilitado

    - **Configuração do** > utilizador**Todas as definições**:
      - **Impedir que os utilizadores sincroniem contas pessoais do OneDrive**
        - **Tipo**: Utilizador
        - **Valor**: Habilitado

As suas definições são semelhantes às seguintes definições:

> [!div class="mx-imgBorder"]
> ![Criar um modelo administrativo OneDrive no Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/one-drive-administrative-template.png)

Para obter mais informações sobre as definições do cliente OneDrive, consulte [a Política de Grupo use para controlar as definições do cliente sincronizado do OneDrive](https://docs.microsoft.com/onedrive/use-group-policy).

### <a name="assign-your-template"></a>Atribuir o seu modelo

1. No seu modelo, selecione **Next** até chegar às **Atribuições**. Escolha **selecionar grupos para incluir:**
2. É apresentada uma lista de utilizadores e grupos existentes. Selecione o grupo **de dispositivos All Windows** que criou anteriormente > **Select**.

    Se você está usando este tutorial em um ambiente de produção, então considere adicionar grupos que estão vazios. O objetivo é praticar a atribuição do seu modelo.

3. Selecione **Seguinte**. Em **Rever + criar**, selecione **Criar** para guardar as suas alterações.

Neste ponto, criou alguns modelos administrativos e atribuiu-os a grupos que criou. O próximo passo é criar um modelo administrativo utilizando o Windows PowerShell e o Microsoft Graph API para Intune.

## <a name="optional-create-a-policy-using-powershell-and-graph-api"></a>Opcional: Criar uma política utilizando a PowerShell e a API de gráfico

Esta secção utiliza os seguintes recursos. Vamos instalar estes recursos nesta secção.

- [Intune PowerShell SDK](https://github.com/microsoft/Intune-PowerShell-SDK)
- [Microsoft Graph API para Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)

1. No **computador Admin,** abra o **Windows PowerShell** como administrador:

    1. Na sua barra de pesquisa, introduza **powershell**.
    2. Clique no **Windows PowerShell** > **Run como administrador**.

    > [!div class="mx-imgBorder"]
    > ![Executar o Windows PowerShell como administrador](./media/tutorial-walkthrough-administrative-templates/run-windows-powershell-administrator.png)

2. Pegue e estabeleça a política de execução.

    1. Insira:`get-ExecutionPolicy`

        Escreva o que está definido, o que pode **restringir.** Quando terminar com o tutorial, volte ao seu valor original.

    2. Insira:`Set-ExecutionPolicy -ExecutionPolicy Unrestricted`

    3. Insira `Y` para mudá-lo.

    A política de execução da PowerShell ajuda a prevenir a execução de scripts maliciosos. Para mais informações, consulte as Políticas de [Execução.](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)

3. Insira:`Install-Module -Name Microsoft.Graph.Intune`

    Insira `Y` se:

    - Solicitado para instalar o fornecedor NuGet
    - Solicitado para instalar os módulos a partir de um repo não confiável

    Pode levar vários minutos para ser completado. Quando terminada, é mostrada uma solicitação semelhante à seguinte solicitação:

    > [!div class="mx-imgBorder"]
    > ![Pedido do Windows PowerShell após instalar um módulo](./media/tutorial-walkthrough-administrative-templates/powershell-prompt.png)

4. No seu navegador web, vá ao [https://github.com/Microsoft/Intune-PowerShell-SDK/releases](https://github.com/Microsoft/Intune-PowerShell-SDK/releases)ficheiro **Intune-PowerShell-SDK_v6.1907.00921.0001.zip.**

    1. Selecione **Guardar como**, e selecione uma pasta de que se lembrará. `c:\psscripts`é uma boa escolha.
    2. Abra a pasta, clique à direita no ficheiro .zip > **Extrair todos os** > **extratos**. A sua estrutura de pasta é semelhante à seguinte pasta:

        > [!div class="mx-imgBorder"]
        > ![Estrutura de pasta SDK PowerShell Intune após ser extraído](./media/tutorial-walkthrough-administrative-templates/psscripts-directory.png)

5. No separador **Ver,** verifique as extensões de **nome do ficheiro:**

    > [!div class="mx-imgBorder"]
    > ![Selecione extensões de nome de ficheiro no separador visualização no explorador](./media/tutorial-walkthrough-administrative-templates/file-names-extension.png)

6. Na sua pasta, `c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471`e vá para . Clique à direita em cada .dll > **Propriedades** > **Desbloquear**.

    > [!div class="mx-imgBorder"]
    > ![Desbloquear os DLLs](./media/tutorial-walkthrough-administrative-templates/unblock-dll.png)

7. Na sua aplicação **Windows PowerShell,** introduza:

    ```powershell
    Import-Module c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471\Microsoft.Graph.Intune.psd1
    ```

    Entre `R` se for solicitado a fugir do editor não confiável.

8. Os modelos administrativos insinados utilizam a versão beta do Graph:

    1. Insira:`Update-MSGraphEnvironment -SchemaVersion 'beta'`

    2. Insira:`Connect-MSGraph -AdminConsent`

    3. Quando solicitado, inscreva-se na mesma conta de administrador da Microsoft 365. Estes cmdlets criam a política na sua organização de inquilinos.

        **Utilizador**: Insira a conta de administrador da sua subscrição de inquilino Microsoft 365.  
        **Palavra-passe**: Introduza a sua palavra-passe.

    4. Selecione **Aceitar**.

9. Crie o perfil de configuração de configuração do **teste.** Introduza:

    ```powershell
    $configuration = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations -Content '{"displayName":"Test Configuration","description":"A test configuration created through PS"}' -HttpMethod POST
    ```

    Quando estes cmdlets têm sucesso, o perfil é criado. Para confirmar, vá ao centro de administração do Endpoint Manager > Perfis de **Configuração**. O seu perfil de **Configuração** de Teste deve ser listado.

10. Obtenha todas as Definições de Definição. Introduza:

    ```powershell
    $settingDefinitions = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions -HttpMethod GET
    ```

11. Encontre o ID de definição utilizando o nome de visualização de definição. Introduza:

    ```powershell
    $desiredSettingDefinition = $settingDefinitions.value | ? {$_.DisplayName -Match "Silently sign in users to the OneDrive sync client with their Windows credentials"}
    ```

12. Configure uma definição. Introduza:

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues" -Content ("{""enabled"":""true"",""configurationType"":""policy"",""definition@odata.bind"":""https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions('$($desiredSettingDefinition.id)')""}") -HttpMethod POST
    ```

    ```powershell
    Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -Content ("{""enabled"":""false""}") -HttpMethod PATCH
    ```

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -HttpMethod GET
    ```

### <a name="see-your-policy"></a>Consulte a sua política

1. No centro de administração do Endpoint Manager > > **Atualização**de Perfis de **Configuração**.
2. Selecione o seu perfil de **configuração** de teste > **Definições**.
3. Na lista de lançamentos, selecione **Todos os produtos**.

Verá o **sessão silenciosa de utilizadores no cliente sincronizado oneDrive com** a definição de credenciais do Windows configurada.

## <a name="policy-best-practices"></a>Boas práticas políticas

Ao criar políticas e perfis no Intune, existem algumas recomendações e boas práticas a ter em conta. Para mais informações, consulte [as melhores práticas políticas e de perfil.](device-profile-create.md#recommendations)

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não for necessário, pode:

- Elimine os grupos que criou:

  - **Todos os dispositivos estudantis do Windows 10**
  - **Todos os dispositivos Windows**
  - **Todos os Professores**

- Elimine os modelos de administração que criou:

  - **Modelo de administrador - Dispositivos estudantis do Windows 10**
  - **Modelo de administrador - Políticas OneDrive que se aplicam a todos os utilizadores do Windows 10**
  - **Configuração do teste**

- Derete a política de execução do Windows PowerShell de volta ao seu valor original. O exemplo que se segue define a política de execução para restrições:

  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Restricted
  ```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, você se familiariza mais com o centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)usou o construtor de consultas para criar grupos dinâmicos, e criou modelos administrativos em Intune para configurar [as definições do ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies). Também comparou a utilização de modelos ADMX no local e na nuvem com Intune. Como bónus, usaste cmdlets PowerShell para criar um modelo administrativo.

Para obter mais informações sobre os modelos administrativos em Intune, consulte:

> [!div class="nextstepaction"]
> [Utilize os modelos do Windows 10 para configurar as definições de política de grupo em Intune](administrative-templates-windows.md)
