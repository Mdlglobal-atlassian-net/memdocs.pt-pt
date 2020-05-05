---
title: Consola do Configuration Manager
titleSuffix: Configuration Manager
description: Aprenda a navegar através da consola De Configuração Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 58b66639094a602206114cd75a724504618ad38c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110037"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Como utilizar a consola 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os administradores utilizam a consola Do Gestor de Configuração para gerir o ambiente do Gestor de Configuração. Este artigo aborda os fundamentos da navegação na consola.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Abra a consola

A consola 'Gestor de Configuração' está sempre instalada em todos os servidores do site. Também pode instalá-lo noutros computadores. Para mais informações, consulte [Instalar a consola 'Gestor de Configuração'.](../deploy/install/install-consoles.md)

O método mais simples para abrir a consola **Start** num computador `Configuration Manager console`Windows 10, prima Iniciar e começar a escrever . Pode não precisar de escrever toda a corda para o Windows encontrar a melhor correspondência.

Se navegar no menu Iniciar, procure o ícone da consola Do Gestor de **Configuração** no grupo **Microsoft Endpoint Manager.**

![Ícones de menu inicial do Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> O caminho do menu Iniciar mudou na versão 1910. Na versão 1906 e anterior, o nome da pasta é **System Center**. Quando atualizar o Gestor de Configuração para a versão 1910 ou mais tarde, certifique-se de atualizar qualquer documentação interna que mantenha para incluir esta nova localização.

## <a name="connect-to-a-site-server"></a>Ligar a um servidor de site

A consola liga-se ao servidor do site da administração central ou aos servidores do seu site principal. Não é possível ligar uma consola de Configuração a um site secundário. Durante a instalação, especificou o nome de domínio totalmente qualificado (FQDN) do servidor do site ao qual a consola se liga.

Para se ligar a um servidor de site diferente, utilize os seguintes passos:

1. Selecione a seta na parte superior da [fita](#ribbon)e escolha **Ligar a um Novo Local**.  

    ![Ligue a consola a um novo site](media/connect-to-a-new-site.png)  

2. Digite o FQDN do servidor do site. Se tiver ligado previamente ao servidor do site, selecione o servidor a partir da lista de lançamentos.  

    ![Janela de ligação ao site, introduza o FQDN do servidor do site](media/site-server-fqdn.png)  

3. Selecione **Ligar**.  

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. Para mais informações, consulte [Plan for the SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Navegação

Algumas áreas da consola podem não ser visíveis dependendo da sua função de segurança atribuída. Para obter mais informações sobre papéis, consulte [os fundamentos da administração baseada no papel.](../../understand/fundamentals-of-role-based-administration.md)

### <a name="workspaces"></a>Áreas de Trabalho

A consola De Configuração Manager tem quatro **espaços de trabalho:**  

- **Ativos e Conformidade**  

- **Biblioteca de Software**  

- **Monitorização**  

- **Administration**  

![Espaços de trabalho do Gestor de Configuração com menu de contexto](media/configuration-manager-workspaces.png)  

Reencomende os botões do espaço de trabalho selecionando a seta para baixo e escolhendo opções de painel de **navegação**. Selecione um item para **mover-se para cima** ou **para baixo**. Selecione **Reset** para restaurar a ordem de botão predefinida.  

![Janela de opções de painel de navegação para reordenar espaços de trabalho](media/navigation-pane-options.png)  

Minimize um botão espaço de trabalho selecionando **mostrar menos botões**. O último espaço de trabalho na lista é minimizado primeiro. Selecione um botão minimizado e escolha **botões Mostrar Mais** para restaurar o botão ao seu tamanho original.

![Espaços de trabalho minimizados na consola do Gestor de Configuração](media/workspace-buttons.png)  

### <a name="nodes"></a>Nós

Espaços de trabalho são uma coleção de **nódosos.** Um exemplo de um nó é o nó de Grupos de **Atualização** de Software no espaço de trabalho da Biblioteca de **Software.**

Uma vez no nó, pode selecionar a seta para minimizar o painel de navegação.  

![Nó exemplo e destaque minimizar seta](media/software-update-groups-node.png)  

Utilize a barra de **navegação** para se deslocar em torno da consola quando minimizar o painel de navegação.  

![Gestor de Configuração minimizou o painel de navegação](media/minimized-navigation-pane.png)  

Na consola, os nós são por vezes organizados em pastas. Quando seleciona a pasta, normalmente apresenta um índice de **navegação** ou um **dashboard**.  

![O software do Gestor de Configuração atualiza o índice de navegação](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Fita

A fita está no topo da consola Do Gestor de Configuração. A fita pode ter mais do que uma lingueta e pode ser minimizada usando a seta à direita. Os botões da fita mudam com base no nó. A maioria dos botões da fita também estão disponíveis nos menus de contexto.  

![Fita de exemplo, realçando vários separadores e minimizando a seta](media/ribbon.png)

### <a name="details-pane"></a>Painel de detalhes

Pode obter informações adicionais sobre itens revendo o painel de detalhes. O painel de detalhes pode ter um ou mais separadores. As linguetas variam consoante o nó.  

![Painel de detalhes do exemplo do Gestor de Configuração](media/details-pane.png)

### <a name="columns"></a>Colunas

Pode adicionar, remover, reencomendar e redimensionar colunas. Estas ações permitem-lhe mostrar os dados que prefere. As colunas disponíveis variam consoante o nó. Para adicionar ou remover uma coluna da sua vista, clique à direita numa rubrica de coluna existente e selecione um item. Reordenar colunas arrastando a coluna onde gostaria que estivesse.  

![Gestores de configuração adicionar coluna](media/add-columns.png)  

Na parte inferior do menu de contexto da coluna, pode classificar ou agrupar por uma coluna. Além disso, pode ordenar por uma coluna selecionando o seu cabeçalho.  

![Grupo de gestor de configuração por coluna](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a>Recuperar o bloqueio para editar objetos

<!--4786915-->

Se a consola do Gestor de Configuração deixar de responder, pode ser bloqueado para não fazer mais alterações até que o bloqueio expire após 30 minutos. Esta fechadura faz parte do sistema SEDO (Edição Serializada de Objetos Distribuídos). Para mais informações, consulte [O Gestor de Configuração SEDO](../../../develop/core/understand/sedo.md).

A partir da versão atual do [ramo 1906,](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)pode limpar o bloqueio numa sequência de tarefas. A partir da versão 1910, pode limpar o bloqueio de qualquer objeto na consola 'Gestor de Configuração'.

Esta ação aplica-se apenas à sua conta de utilizador que tenha o cadeado e no mesmo dispositivo a partir do qual o site concedeu o bloqueio. Quando tentar aceder a um objeto bloqueado, pode agora **descartar alterações**e continuar a editar o objeto. Estas alterações perder-se-iam quando o cadeado expirasse.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>Ver consolas recentemente conectadas

<!--3699367-->
A partir da versão 1902, podes ver as ligações mais recentes para a consola Do Gestor de Configuração. A vista inclui ligações ativas e as ligações que recentemente ligaram. Verá sempre a sua ligação de consola atual na lista e só verá ligações a partir da consola 'Gestor de Configuração'. Não verá a PowerShell ou outras ligações baseadas em SDK ao Fornecedor SMS. O site remove instâncias da lista com mais de 30 dias.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a>Pré-requisitos para visualizar consolas conectadas

- A sua conta precisa da permissão **de leitura** no objeto **SMS_Site**

- Configure o serviço de administração REST API. Para mais informações, consulte [o que é o serviço de administração?](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>Ver consolas conectadas

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.**  

2. Expandir **a Segurança** e selecionar o nó de Ligações de **Consola.**  

3. Ver as ligações recentes, com as seguintes propriedades:  

    - Nome de utilizador
    - Nome da máquina
    - Código de site conectado
    - Versão consola
    - Última vez ligada: Quando o utilizador *abriu* pela última vez a consola
    - A partir da versão 1910, a coluna **Heartbeat da Última Consola** substituiu a coluna Last Connected **Time.** <!--4923997-->
       - Uma consola aberta em primeiro plano envia um batimento cardíaco a cada 10 minutos.

![Ver ligações de consola do Gestor de Configuração](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a>Iniciar o Chat das equipas da Microsoft a partir de ligações de consola
<!--4923997-->
*(Introduzido na versão 1910)*

A partir da versão 1910, pode enviar mensagens a outros administradores do Gestor de Configuração a partir do nó de **Ligações** de Consola utilizando as Microsoft Teams. Quando escolhe **iniciar** o Microsoft Teams Chat com um administrador, o Microsoft Teams é lançado e abre-se um chat com o utilizador.

### <a name="prerequisites"></a>Pré-requisitos

- Para iniciar uma conversa com um administrador, a conta com que pretende conversar tem de ser descoberta com a [Azure AD ou a AD User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- As Microsoft Teams instalaram-se no dispositivo a partir do qual executas a consola.
nota
- Todos os [pré-requisitos para visualizar consolas conectadas](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Iniciar o Chat das Equipas da Microsoft

1. Vá para**as ligações**de consola de**segurança** > da **administração.** > 
1. Clique à direita na ligação de consola de um utilizador e selecione **Start Microsoft Teams Chat**.
    - Se o Nome Principal do Utilizador não for encontrado para o administrador selecionado, o **Start Microsoft Teams Chat** está acinzentado.
    - Uma mensagem de erro, incluindo um link de descarregamento, aparece se o Microsoft Teams não estiver instalado no dispositivo a partir do qual executa a consola.
    - Se o Microsoft Teams estiver instalado no dispositivo a partir do qual executa a consola, abrirá um chat com o utilizador.

### <a name="known-issues"></a>Problemas conhecidos

A mensagem de erro que notifica que as Equipas Microsoft não estão instaladas não será exibida se não existir a seguinte tecla de Registo:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Para contornar o problema, crie manualmente a chave do Registo.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a>Notificações de consola do Gestor de Configuração

<!--3556016, fka 1318035-->
A partir da versão 1902 do Gestor de Configuração, a consola notifica-o para os seguintes eventos:

- Quando uma atualização está disponível para o próprio Gestor de Configuração
- Quando ocorrem eventos de ciclo de vida e manutenção no ambiente

Esta notificação é uma barra na parte superior da janela da consola abaixo da fita. Substitui a experiência anterior quando as atualizações do Gestor de Configuração estão disponíveis. Estas notificações na consola ainda apresentam informações críticas, mas não interferem com o seu trabalho na consola. Não pode descartar notificações críticas. A consola apresenta todas as notificações numa nova área de notificação da barra de títulos.

![Barra de notificação e bandeira na consola](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configure um site para mostrar notificações não críticas

Pode configurar cada site para apresentar notificações não críticas nas propriedades do site.

1. No espaço de trabalho da **Administração,** expandir a Configuração do **Site,** em seguida, selecione o nó **de Sites.**
1. Selecione o site que pretende configurar para notificações não críticas.
1. Na fita, selecione **Propriedades**.
1. No separador **Alertas,** selecione a opção de ativar notificações de **consola para alterações não críticas**na saúde do site .
   - Se ativar esta definição, todos os utilizadores da consola vêem notificações críticas, de aviso e informações. Esta definição está ativada por predefinição.  
   - Se desativar esta definição, os utilizadores da consola apenas vêem notificações críticas.  

A maioria das notificações de consola são por sessão. A consola avalia as consultas quando um utilizador a lança. Para ver alterações nas notificações, reinicie a consola. Se um utilizador rejeitar uma notificação não crítica, notifica novamente quando a consola reinicia se ainda for aplicável.

As seguintes notificações reavaliam de cinco em cinco minutos:

- O site está em modo de manutenção  
- Site está em modo de recuperação  
- Site está em modo de upgrade  

As notificações seguem as permissões da administração baseada em papéis. Por exemplo, se um utilizador não tiver permissões para ver atualizações do 'Gestor de Configuração', não verá essas notificações.

Algumas notificações têm uma ação relacionada. Por exemplo, se a versão da consola não corresponder à versão do site, selecione **Instalar a nova versão da consola**. Esta ação lança o instalador de consolas.

As seguintes notificações são mais aplicáveis ao serviço técnico de pré-visualização:  

- A versão de avaliação é no prazo de 30 dias após a expiração (Aviso): a data atual é no prazo de 30 dias a contar da data de validade da versão de avaliação  
- A versão de avaliação está caducada (Crítica): a data atual já passou da data de validade da versão de avaliação  
- Desajuste da versão da consola (Crítico): a versão da consola não corresponde à versão do site  
- Atualização do site está disponível (Aviso): há um novo pacote de atualização disponível  

Para obter mais informações e assistência para resolução de problemas, consulte o ficheiro **SmsAdminUI.log** no computador da consola. Por predefinição, este ficheiro de `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`registo encontra-se no seguinte caminho: .


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a>Painel de documentação na consola

<!--3556019 FKA 1357546-->
Começando na versão 1902 do Gestor de Configuração, há um nó de **Documentação** no novo espaço de trabalho **comunitário.** Este nó inclui informações atualizadas sobre documentação do Gestor de Configuração e artigos de suporte. Inclui as seguintes secções:  

### <a name="product-documentation-library"></a>Biblioteca de documentação de produtos

- **Recomendado:** uma lista manualmente curada de artigos importantes.
- **Tendência**: os artigos mais populares do último mês.
- **Recentemente atualizado**: artigos revistos no mês passado.

### <a name="support-articles"></a>Artigos de suporte

- **Artigos de resolução de problemas**: passeios guiados para ajudar na resolução de problemas componentes e funcionalidades do Gestor de Configuração.
- **Artigos de apoio novos e atualizados**: artigos novos ou atualizados nos últimos dois meses.

### <a name="troubleshooting-connection-errors"></a>Erros de ligação de resolução de problemas
O nó **documentação** não tem configuração de procuração explícita. Utiliza qualquer proxy definido por OS no painel de controlo de **Opções** de Internet applet. Para voltar a tentar após um erro de ligação, refresque o nó **documentação.**


## <a name="command-line-options"></a>Opções da linha de comandos

A consola 'Gestor de Configuração' tem as seguintes opções de linha de comando:

|Opção|Descrição|  
|------------|-----------------|  
|`/sms:debugview=1`|Um DebugView está incluído em todos os ResultadoS Que especificam uma vista. DebugView mostra propriedades cruas (nomes e valores).|  
|`/sms:NamespaceView=1`|Mostra a vista do espaço de nome na consola.|  
|`/sms:ResetSettings`|A consola ignora os estados de ligação e visão persistentes pelo utilizador. O tamanho da janela não é reposto.|  
|`/sms:IgnoreExtensions`|Desativa quaisquer extensões do Gestor de Configuração.|  
|`/sms:NoRestore`|A consola ignora a navegação no nó anterior.|  


## <a name="tips"></a>Sugestões

### <a name="general"></a>Geral

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Melhorias na pesquisa de consolas
<!--4640570-->
*(Introduzido na versão 1910)*

- Pode utilizar a opção de pesquisa **de Todas as Subpastas** a partir dos nós de Pacotes e **Consultas** de **Condutor.**<!--2841181,5424892--> A partir da versão 2002, utilize também esta opção a partir dos nós de **Configuração** e Planos de Base de **Configuração.**<!--5891241-->

- Quando uma pesquisa retorna mais de 1.000 resultados, selecione o botão **OK** na barra de aviso para visualizar mais resultados.<!--4640570-->

    ![Screenshot da barra de aviso para muitos resultados de pesquisa](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > O limite padrão dos resultados da pesquisa é de 1.000. Pode alterar este valor predefinido. Na consola 'Gestor de Configuração', vá ao separador **De Pesquisa** da fita. No grupo **Opções,** selecione **Definições de Pesquisa**. Alterar o valor **dos Resultados** de Pesquisa. Um maior número de resultados de pesquisa pode demorar mais tempo a ser exibido.
    >
    > Por padrão, o limite máximo máximo é de 100.000. Para alterar este limite, detete o valor DWORD **QueryResultCountMaximum** na seguinte tecla de registo:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > A definição na consola corresponde ao valor **QueryResultCountLimit** na mesma tecla. Um administrador pode configurar estes valores na colmeia HKLM para todos os utilizadores do dispositivo. O valor DA HKCU sobrepõe-se à definição de HKLM.

#### <a name="role-based-administration-for-folders"></a>Administração baseada em funções para pastas
<!--3600867-->
*(Introduzido na versão 1906)*

Pode definir os âmbitos de segurança nas pastas. Se tiver acesso a um objeto na pasta ou não tiver acesso à pasta, não poderá ver o objeto. Da mesma forma, se tiver acesso a uma pasta, mas não a um objeto dentro dela, não verá esse objeto. Clique na direita numa pasta, escolha **Definir Âmbitos**de Segurança e, em seguida, escolha os âmbitos de segurança que pretende aplicar.

#### <a name="views-sort-by-integer-values"></a>Vistas classificam-se por valores inteiros

*(Introduzido na versão 1902)*

Fizemos melhorias na forma como várias visualizações classificam dados. Por exemplo, no nó de **implantação** do espaço de trabalho de **monitorização,** as seguintes colunas classificam agora como números em vez de valores de cadeia:  

- Erros de número
- Número em curso
- Número outro
- Sucesso de Números
- Número Desconhecido  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Mova o aviso para um grande número de resultados

*(Introduzido na versão 1902)*

Quando seleciona um nó na consola que devolve mais de 1.000 resultados, o Select Manager apresenta o seguinte aviso:

> O Gestor de Configuração devolveu um grande número de resultados. Pode reduzir os seus resultados utilizando a pesquisa. Ou, clique aqui para ver um máximo de 100000 resultados.

Há agora espaço em branco adicional entre este aviso e o campo de busca. Este movimento ajuda a evitar selecionar inadvertidamente o aviso para apresentar mais resultados.

#### <a name="send-feedback"></a>Enviar comentários

*(Introduzido na versão 1806)*
<!--1357542-->

Envie feedback do produto a partir da consola.  

- **Envie um sorriso**: Envie feedback sobre o que gostou  

- **Envie uma franja**: Envie feedback sobre o que não gostou  

- **Envie uma sugestão**: Leva-o ao UserVoice para partilhar a sua ideia  

Para mais informações, consulte [o Feedback do Produto](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Espaço de trabalho de Ativos e Compliance

#### <a name="real-time-actions-from-device-lists"></a>Ações em tempo real a partir de listas de dispositivos
<!--4616810-->
*(Introduzido na versão 1906)*

Existem várias formas de apresentar uma lista de dispositivos sob o nó de **Dispositivos** no espaço de trabalho **De Ativos e Compliance.**

- No espaço de trabalho **De Ativos e Compliance,** selecione o nó de **Recolha de Dispositivos.** Selecione uma coleção de dispositivos e escolha a ação para **mostrar aos membros**. Esta ação abre um subnódoo do nó dos **Dispositivos** com uma lista de dispositivos para essa recolha.  

  - Ao selecionar o subnódoo da coleção, pode agora iniciar a **CMPivot** do grupo Coleção da fita.  

- No espaço de trabalho **de monitorização,** selecione o nó de **Implantação.** Selecione uma implementação e escolha a ação **'Ver Status'** na fita. No painel de estado de implantação, clique duas vezes no total dos ativos para perfurar uma lista de dispositivos.  

  - Quando selecionar um dispositivo nesta lista, pode agora iniciar **cmPivot** e **executar scripts** do grupo dispositivo da fita.  


#### <a name="collections-tab-in-devices-node"></a>Separador de coleções no nó dos dispositivos
<!--4616810-->
*(Introduzido na versão 1906)*

No espaço de trabalho **de Ativos e Compliance,** vá ao nó dos **Dispositivos** e selecione um dispositivo. No painel de detalhes, mude para o novo separador **Coleções.** Este separador lista as coleções que incluem este dispositivo. 

> [!Note]  
> - Este separador não está atualmente disponível a partir de um subnódoo de dispositivos sob o nó de **Recolha de Dispositivos.** Por exemplo, quando seleciona a opção de **mostrar aos membros** numa coleção.
> - Este separador pode não povoar como esperado para alguns utilizadores. Para ver a lista completa de coleções a que pertence um dispositivo, deve ter a função de segurança **do Administrador Completo.** Este é um problema conhecido. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Adicione a coluna SMBIOS GUID aos nódosos de recolha de dispositivos e dispositivos

*(Introduzido na versão 1906)*

<!--4526580-->
Tanto nos nós de **Recolha de Dispositivos** como **de Dispositivos,** pode agora adicionar uma nova coluna para **smbios GUID**. Este valor é o mesmo que a propriedade **BIOS GUID** da classe Recursos do Sistema. É um identificador único para o hardware do dispositivo.

#### <a name="search-device-views-using-mac-address"></a>Pontos de vista do dispositivo de pesquisa usando endereço MAC

<!--3600878-->
*(Introduzido na versão 1902)*

Pode procurar um endereço MAC numa visão do dispositivo da consola 'Gestor de Configuração'. Esta propriedade é útil para administradores de implementação de OS enquanto resolução de implementações baseadas em PXE. Quando visualizar uma lista de dispositivos, adicione a coluna **Mac Address** à vista. Utilize o campo de pesquisa para adicionar os critérios de pesquisa do **Endereço MAC.**

#### <a name="view-users-for-a-device"></a>Ver utilizadores para um dispositivo

A partir da versão 1806, as seguintes colunas estão disponíveis no nó dos **Dispositivos:**  

- **Utilizadores primários(s)** <!--1357280-->  

- **Atualmente registado no utilizador** <!--1358202-->  

    > [!NOTE]  
    > Ver o atualmente registado no utilizador requer a descoberta do [utilizador](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) e [a afinidade](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .  

Para obter mais informações sobre como mostrar uma coluna não predefinida, consulte [Colunas](#columns).

#### <a name="improvement-to-device-search-performance"></a>Melhoria do desempenho da pesquisa do dispositivo

<!-- 3614690 -->
A partir da versão 1806, quando se procura numa coleção de dispositivos, não procura a palavra-chave contra todas as propriedades do objeto. Quando não é específico sobre o que procurar, procura pelas quatro propriedades seguintes:

- Nome
- Utilizadores primários(s)
- Atualmente registado no utilizador
- Último nome de utilizador de logon

Este comportamento melhora significativamente o tempo que leva para procurar pelo nome, especialmente em um ambiente grande. As pesquisas personalizadas por critérios específicos não são afetadas por esta alteração.


### <a name="software-library-workspace"></a>Espaço de trabalho da Biblioteca de Software

#### <a name="order-by-program-name-in-task-sequence"></a>Ordem por nome de programa na sequência de tarefas
<!--4616810-->
*(Introduzido na versão 1906)*

No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.** Editar uma sequência de tarefas e selecionar ou adicionar o passo ['Pacote instalação'.](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) Se um pacote tem mais de um programa, a lista de abandono supor agora os programas alfabeticamente.

#### <a name="task-sequences-tab-in-applications-node"></a>Separador de sequências de tarefas no nó de aplicações
<!--4616810-->
*(Introduzido na versão 1906)*

No espaço de trabalho da Biblioteca de **Software,** expandir gestão de **aplicações,** ir ao nó de **Aplicações** e selecionar uma aplicação. No painel de detalhes, mude para o novo separador de **sequências de tarefas.** Este separador lista as sequências de tarefas que referem esta aplicação.

#### <a name="drill-through-required-updates"></a>Perfurar através de atualizações necessárias
<!--4224414-->
*(Introduzido na versão 1906)*

1. Vá a um dos seguintes lugares na consola Do Gestor de Configuração:

   - **Software** > da Biblioteca de**Software atualiza** > **todas as atualizações de software**
   - **Biblioteca de** > software**Windows 10 A servir** > **todas as atualizações do Windows 10**
   - **Software Library** > Gabinete de Biblioteca de Software**365 Gabinete** > de Gestão de Clientes**365 Atualizações**

1. Selecione qualquer atualização que seja necessária por pelo menos um dispositivo.
1. Olhe para o separador **Resumo** e encontre o gráfico de tartes em **estatísticas.**
1. Selecione a hiperligação necessária para **ver** junto ao gráfico de tartes para aprofundar a lista do dispositivo.
1. Esta ação leva-o a um nó temporário em **Dispositivos** onde pode ver os dispositivos que necessitam da atualização. Você também pode tomar ações para o nó, como criar uma nova coleção a partir da lista.

> [!NOTE]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

#### <a name="maximize-the-browse-registry-window"></a>Maximizar a janela de registo de navegação

<!--3594151 includes all MMS 1902 console changes-->
*(Introduzido na versão 1902)*

1. No espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**
1. Selecione uma aplicação que tenha um tipo de implementação com um método de deteção. Por exemplo, um método de deteção do Instalador do Windows.
1. No painel de detalhes, mude para o separador Tipos de **Implementação.**
1. Abra as propriedades de um tipo de implementação e mude para o separador Método de **Deteção.** Selecione **Cláusula de Adição**.
1. Altere o Tipo de **Definição** para **O Registo** e selecione **Procurar** para abrir a janela **'Registo de navegação'.** Agora pode maximizar esta janela.  

#### <a name="edit-a-task-sequence-by-default"></a>Editar uma sequência de tarefas por padrão

*(Introduzido na versão 1902)*

No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.** **Editar** é agora a ação padrão ao abrir uma sequência de tarefas. Anteriormente, a ação padrão era **a Properties**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Vá à coleção a partir de uma implementação de aplicação

*(Introduzido na versão 1902)*

1. No espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**
1. Selecione uma aplicação. No painel de detalhes, mude para o separador **De implantação.**
1. Selecione uma implementação e, em seguida, escolha a nova opção **Coleção** na fita no separador Implementação. Esta ação muda a vista para a coleção que é o alvo da implantação.
   - Esta ação também está disponível a partir do menu de contexto do clique direito na implementação nesta vista.


### <a name="monitoring-workspace"></a>Monitorização do espaço de trabalho

#### <a name="correct-names-for-client-operations"></a>Nomes corretos para operações de clientes
<!--4616810-->
*(Introduzido na versão 1906)*

No espaço de trabalho **de Monitorização,** selecione **Operações de Cliente.** A operação para mudar para o próximo Ponto de **Atualização** de Software está agora devidamente nomeada.

#### <a name="show-collection-name-for-scripts"></a>Mostrar nome de coleção para scripts
<!--4616810-->
*(Introduzido na versão 1906)*

No espaço de trabalho **de monitorização,** selecione o nó do Estado do **Script.** Agora lista o **Nome de Recolha** para além do ID.

#### <a name="remove-content-from-monitoring-status"></a>Remover o conteúdo do estado de monitorização

*(Introduzido na versão 1902)*

1. No espaço de trabalho **de monitorização,** expanda o **Estado de Distribuição**e selecione O Estado do **Conteúdo**.
1. Selecione um item na lista e escolha a opção **'Ver Status'** na fita.
1. No painel de detalhes do ativo, clique num ponto de distribuição e selecione a nova opção **Remover**. Esta ação remove este conteúdo do ponto de distribuição selecionado.

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalhes em visualizações de monitorização

*(Introduzido na versão 1806)*
<!--1357856-->
Copiar informações do painel de detalhes do **ativo** para os seguintes nódosos de monitorização:  

- **Estado de distribuição de conteúdo**  

- **Estado de implantação**  

![Visualização do Estado de Implementação, copiar detalhes do ativo](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Espaço de trabalho de administração

<!--4223683-->
A partir da versão 1906, pode permitir que alguns nós sob o nó de **Segurança** utilizem o serviço de administração. Esta alteração permite que a consola comunique com o Fornecedor SMS em HTTPS em vez de via WMI. Para mais informações, consulte [Configurar o serviço](../../../develop/adminservice/set-up.md#bkmk_console)de administração .

## <a name="next-steps"></a>Passos seguintes

[Funções de acessibilidade](../../understand/accessibility-features.md)

[Editor de sequência de tarefas](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
