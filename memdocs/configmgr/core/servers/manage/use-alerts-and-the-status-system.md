---
title: Alertas e o sistema de estado
titleSuffix: Configuration Manager
description: Configure os alertas e utilize o sistema de estado para se manter informado sobre o estado da implementação do seu Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720717"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Utilize alertas e o sistema de estado para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Configure alertas e utilize o Sistema de Estado incorporado para se manter informado sobre o estado da implementação do seu Gestor de Configuração.  


##  <a name="status-system"></a><a name="bkmk_Status"></a>Sistema de estado  
 Todos os componentes do site principal geram mensagens de estado que fornecem comentários sobre as operações de site e de hierarquia.    Estas informações podem mantê-lo informado sobre o estado de funcionamento dos diferentes processos do site. Pode otimizar o sistema de alerta para ignorar o ruído de problemas conhecidos, ao aumentar a visibilidade inicial para outros problemas que poderão requerer a sua atenção.  

 Por predefinição, o sistema de estado do Gestor de Configuração funciona sem configuração utilizando configurações adequadas para a maioria dos ambientes. No entanto, é possível configurar o seguinte:  

-   **Summarizers de estado:** é possível editar os summarizers de estado em cada site para controlar a frequência das mensagens de estado que geram uma alteração do indicador de estado para os quatro summarizers seguintes:  

    -   Summarizer de Implementação da Aplicação  

    -   Summarizer de Estatísticas da Aplicação  

    -   Status Summarizer de Componentes  

    -   Summarizer de Estado do Sistema de Sites  

-   **Regras do Filtro de Estado:** é possível criar novas regras do filtro de estado, modificar a prioridade de regras, desativar ou ativar regras e eliminar regras não utilizadas em cada site.  

    > [!NOTE]  
    >  As regras do filtro de estado não suportam a utilização de variáveis de ambiente para executar comandos externos.  

-   **Relatório de Estado:** Pode configurar relatórios de componentes de servidor e cliente para modificar a forma como as mensagens de estado são reportadas ao sistema de estado do Gestor de Configuração e especificar para onde as mensagens de estado são enviadas.  

    > [!WARNING]  
    >  Uma vez que as predefinições dos relatórios são adequadas para a maior parte dos ambientes, altere-as com cuidado. Ao aumentar o nível de reporte de estado, optando por reportar todos os detalhes do estado, pode aumentar a quantidade de mensagens de estado a processar, o que aumenta a carga de processamento no site do Gestor de Configuração. Se diminuir o nível dos relatórios de estado, poderá limitar a utilidade dos summarizers de estado.  

Uma vez que o sistema de estado mantém configurações separadas para cada site, é necessário editar cada site individualmente.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Procedimentos para configurar o sistema de estado  

##### <a name="to-configure-status-summarizers"></a>Para configurar summarizers de estado  

1.  Na consola do Gestor de Configuração, navegue para**sites**de**configuração** >do site **da administração** > e, em seguida, selecione o site para o qual pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Summarizers de Estado**.  

3.  Na caixa de diálogo **Summarizers de Estado** , selecione o summarizer que pretende configurar e clique em **Editar** para abrir as propriedades desse summarizer. Se estiver a editar os summarizers Implementação da Aplicação ou Estatísticas da Aplicação, avance para o passo 5. Se estiver a editar o Estado do Componente, avance para o passo 6. Se estiver a editar o summarizer Estado do Sistema de Sites, avance para o passo 7.  

4.  Utilize os passos seguintes depois de abrir a página de propriedades do Summarizer de Implementação da Aplicação ou do Summarizer de Estatísticas da Aplicação:  

    1.  No separador **Geral** da página de propriedades dos summarizers, configure os intervalos de resumo e clique em **OK** para fechar a página de propriedades.  

    2.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

5.  Utilize os passos seguintes depois de abrir as páginas de propriedades do Summarizer de Estado do Componente:  

    1.  No separador **Geral** da página de propriedades dos resumos configura os valores de replicação e período de limiar.  

    2.  No separador **Limiares** , selecione o **Tipo de mensagem** que pretende configurar e clique no nome de um componente na lista **Limiares** .  

    3.  Na caixa de diálogo **Propriedades do Limiar de Estado** , edite os valores dos limiares de aviso e crítico e, em seguida, clique em **OK**.  

    4.  Repita os passos 6.b e 6.c conforme necessário e, quando tiver terminado, clique em **OK** para fechar as propriedades do summarizer.  

    5.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

6.  Utilize os passos seguintes depois de abrir as páginas de propriedades do Summarizer de Estado do Sistema de Sites:  

    1.  No separador **Geral** da página de propriedades dos resumos configura risa os valores de replicação e programação.  

    2.  No separador **Limiares** , especifique os valores dos **Limiares predefinidos** para configurar limiares predefinidos para a apresentação dos estados críticos e de aviso.  

    3.  Para editar os valores de **Objetos de armazenamento**específicos, selecione o objeto na lista **Limiares específicos** e, em seguida, clique no botão **Propriedades** para aceder e editar os limiares de aviso e crítico dos objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos de armazenamento.  

    4.  Para criar um novo objeto de armazenamento, clique no botão **Criar Objeto** e especifique os valores dos objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos.  

    5.  Para eliminar um objeto de armazenamento, selecione o objeto e clique no botão **Eliminar** .  

    6.  Repita os passos 7.b até 7.e se necessário. Quando tiver terminado, clique em **OK** para fechar as propriedades do summarizer.  

    7.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

##### <a name="to-create-a-status-filter-rule"></a>Para criar uma regra do filtro de estado  

1.  Na consola do Gestor de Configuração, navegue para**sites**de**configuração** >do site **da administração** > e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Regras do Filtro de Estado**. É aberta a caixa de diálogo **Regras do Filtro de Estado** .  

3.  Clique em **Criar**.  

4.  No **Assistente de Criação de Regra de Filtro de Estado**, na página **Geral** , especifique um nome para a nova regra do filtro de estado e os critérios de correspondência de mensagens para a regra e, em seguida, clique em **Seguinte**.  

5.  Na página **Ações** , especifique as ações a executar quando uma mensagem de estado corresponde à regra de filtro e clique em **Seguinte**.  

6.  Na página **Resumo** , reveja os detalhes da nova regra e, em seguida, conclua o assistente.  

    > [!NOTE]  
    >  O Gestor de Configuração apenas requer que a nova regra do filtro de estado tenha um nome. Se a regra for criada mas não forem especificados quaisquer critérios para processar mensagens de estado, a regra do filtro de estado não terá qualquer efeito. Este comportamento permite criar e organizar regras antes de configurar os critérios do filtro de estado para cada regra.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Para modificar ou eliminar uma regra do filtro de estado  

1.  Na consola do Gestor de Configuração, navegue para**sites**de**configuração** >do site **da administração** > e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Regras do Filtro de Estado**.  

3.  Na caixa de diálogo **Regras do Filtro de Estado** , selecione a regra que pretende modificar e execute uma das seguintes ações:  

    -   Clique em **Aumentar Prioridade** ou em **Diminuir Prioridade** para alterar a ordem de processamento da regra do filtro de estado. Em seguida, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Desativar** ou em **Ativar** para alterar o estado da regra. Depois de alterar o estado da regra, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Eliminar** se pretender eliminar a regra do filtro de estado deste site e, em seguida, clique em **Sim** para confirmar a ação. Depois de eliminar uma regra, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Editar** se pretender alterar os critérios para a regra da mensagem de estado e avance para o passo 5 deste procedimento.  

4.  No separador **Geral** da caixa de diálogo das propriedades da regra do filtro de estado, modifique a regra e os critérios de correspondência de mensagens.  

5.  No separador **Ações** , modifique as ações a executar quando uma mensagem de estado corresponde à regra de filtro.  

6.  Clique em **OK** para guardar as alterações.  

7.  Clique em **OK** para fechar a caixa de diálogo **Regras do Filtro de Estado** .  

##### <a name="to-configure-status-reporting"></a>Para configurar relatórios de estado  

1.  Na consola do Gestor de Configuração, navegue para**sites**de**configuração** > do site **da administração** > e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e selecione **Relatórios de Estado**.  

3.  Na caixa de diálogo **Propriedades do Componente de Relatórios de Estado** , especifique as mensagens de estado do componente de servidor e de cliente que pretende comunicar ou registar:  

    1.  Configure **o Relatório** para enviar mensagens de estado para o sistema de mensagens de estado do Gestor de Configuração.  

    2.  Configurar **Registo** para escrever o tipo e a gravidade das mensagens de estado para o registo de eventos do Windows.  

4.  Clique em **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a>Monitorize o sistema de estado do Gestor de Configuração  
 **O estado** do sistema no Gestor de Configuração fornece uma visão geral das operações gerais dos sites e operações de servidor esporáceos da sua hierarquia. Pode revelar problemas operacionais para servidores ou componentes do sistema do site, e pode utilizar o estado do sistema para rever detalhes específicos para diferentes operações do Gestor de Configuração. Monitoriza o estado do sistema a partir do nó do Estado do **Sistema** do espaço de trabalho de **monitorização** na consola 'Gestor de Configuração'.  

 A maioria das funções e componentes do sistema do Site do Gestor de Configuração geram mensagens de estado. Os detalhes das mensagens de estado são registados no registo operacional de cada cliente, mas também são enviados para a base de dados do site, onde são resumidos e apresentados num rollup geral do estado de funcionamento de cada componente ou sistema de sites. Estes rollups de mensagens de estado fornecem detalhes de informações de operações regulares, avisos e detalhes de erros. Pode configurar os limiares em que os avisos ou erros são ativados e otimizar o sistema para assegurar que a informação de rollup ignora problemas conhecidos que não sejam relevantes para si e chama a atenção para problemas graves nos servidores ou para operações de componentes que pretenda investigar.  

 O estado do sistema é replicado para outros sites numa hierarquia como dados do site, não como dados globais. Isto significa que só pode ver o estado do site ao qual a consola do Gestor de Configuração se conecta e quaisquer sites infantis abaixo desse site. Por isso, considere ligar a consola do Gestor de Configuração ao site de alto nível da sua hierarquia quando visualizar o estado do sistema.  

 Utilize a tabela seguinte para identificar as diferentes vistas de estado do sistema e quando utilizar cada uma delas.  

|Nó|Mais informações|  
|----------|----------------------|  
|Estado do Site|Utilize este nó para ver um rollup do estado de cada sistema de sites para rever o estado de funcionamento de cada servidor do sistema de sites. O estado de funcionamento do sistema de sites é determinado por limiares configurados para cada site no **Summarizer de Estado do Sistema de Sites**.<br /><br /> É possível ver as mensagens de estado de cada sistema de sites, definir limiares para mensagens de estado e gerir a operação dos componentes nos sistemas de sites através do **Gestor do Serviço do Configuration Manager**.|  
|Estado do Componente|Utilize este nó para visualizar um rollup do estado de cada componente do Gestor de Configuração para rever a saúde operacional do componente. O estado de funcionamento do componente do site é determinado por limiares configurados para cada site no **Summarizer de Estado do Componente**.<br /><br /> É possível ver as mensagens de estado de cada componente, definir limiares para mensagens de estado e gerir a operação de componentes através do **Gestor do Serviço do Configuration Manager**.|  
|Registos em Conflito|Utilize este nó para ver mensagens de estado sobre clientes que poderão ter registos em conflito.<br /><br /> O Gestor de Configuração usa o ID de hardware para tentar identificar clientes que podem ser duplicados e alertá-lo para os registos contraditórios. Por exemplo, se tiver de reinstalar um computador, o ID de hardware seria o mesmo, mas o GUID que o Gestor de Configuração utiliza pode ser alterado.|  
|Consultas de Mensagens de Estado|Utilize este nó para consultar mensagens de estado de eventos específicos e detalhes relacionados. É possível utilizar consultas de mensagens de estado para localizar as mensagens de estado relacionadas com eventos específicos.<br /><br /> Muitas vezes pode utilizar consultas de mensagem de estado para identificar quando um objeto específico de componente, operação ou Gestor de Configuração foi modificado, e a conta que foi usada para fazer a modificação. Por exemplo, pode executar a consulta incorporada para **Coleções Criadas, Modificadas ou Eliminadas** para identificar quando uma coleção específica foi criada e a conta de utilizador utilizada para criar a coleção.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Gerir o estado do site e o estado do componente  
 Utilize as informações seguintes para gerir o estado do site e o estado do componente:  

-   Para configurar limiares para o sistema de estado, consulte [Procedimentos para configurar o sistema de estado](#bkmk_configstatus).  

-   Para gerir componentes individuais no Gestor de Configuração, utilize o Gestor de Serviço de Gestor de **Configuração**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Ver mensagens de estado  
 É possível ver as mensagens de estado para componentes e servidores de sistema de sites individuais.  

 Para visualizar as mensagens de estado na consola do Gestor de Configuração, selecione um servidor ou componente específico do sistema do site e, em seguida, clique em **Mostrar Mensagens**. Ao visualizar mensagens, é possível selecionar a visualização de tipos de mensagens específicos ou mensagens de um período de tempo específico, bem como filtrar os resultados com base em detalhes das mensagens de estado.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a>Alertas  
 Os alertas do Gestor de Configuração são gerados por algumas operações quando ocorre uma condição específica.  

- Normalmente, os alertas são gerados quando ocorre um erro que é necessário resolver  

- Os alertas podem também ser gerados para o avisar de que existe uma condição, para que possa continuar a monitorizar a situação  

- Alguns alertas são configurados por si, tais como alertas para o Endpoint Protection e o estado do cliente , enquanto outros alertas são configuradas automaticamente  

- Pode configurar subscrições de alertas, que podem então enviar detalhes por e-mail, melhorando a deteção de problemas chave  

  Utilize a tabela seguinte para encontrar informações sobre como configurar alertas e alertar subscrições no Gestor de Configuração:  


|Ação|Mais Informações|  
|------------|----------------------|  
|Configure alertas de proteção de endpoint para uma coleção|Ver **como configurar alertas para proteção de pontos finais no gestor** de configuração na configuração da proteção de [pontofinal](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Configurar alertas de estado do cliente para uma coleção|Ver [Como configurar o estado](../../../core/clients/deploy/configure-client-status.md)do cliente .|  
|Gerir alertas de Gestor de Configuração|Consulte a secção [Management tasks for alerts](#BKMK_Manage) deste tópico.|  
|Configurar subscrições de e-mail para alertas|Consulte as tarefas de gestão da secção [para alertas](#BKMK_Manage) neste tópico..|  
|Monitorizar alertas|Consulte a secção [Monitorizar alertas](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Para gerir alertas gerais  

1. Na consola do Gestor de Configuração, navegue para **monitorizar** > **alertas**e, em seguida, selecione uma tarefa de gestão.  

   Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|  
    |---------------------|-------------|  
    |**Configurar**|Abre o * &lt;nome*\>de alerta Caixa de diálogo**Propriedades** onde pode modificar o nome, gravidade e limiares para o alerta selecionado. Se alterar a gravidade do alerta, esta configuração afeta a forma como os alertas são apresentados na consola 'Gestor de Configuração'.|  
    |**Editar Comentário**|Introduza um comentário para os alertas selecionados. Estes comentários exibem com o alerta na consola 'Gestor de Configuração'.|  
    |**Adiar**|Suspende a monitorização do alerta até que a data especificada seja atingida. Nessa altura, o estado do alerta é atualizado.<br /><br /> Só é possível adiar um alerta quando o mesmo está ativado.|  
    |**Criar subscrição**|Abre a caixa de diálogo **Nova Subscrição** , onde pode criar uma subscrição de e-mail para o alerta selecionado.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Para configurar alertas de estado do cliente para uma coleção  

1.  Na consola 'Gestor de Configuração', clique em **Recursos e** >   **Recolhas de Dispositivos**de Conformidade .  

2.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

    > [!NOTE]  
    >  Não é possível configurar alertas de coleções de utilizadores.  

3.  No separador **Alertas** da\> **Add** * &lt;* caixa de diálogo Collection Name**Properties,** clique em Adicionar .  

    > [!NOTE]  
    >  O separador **Alertas** só está visível se a função de segurança a que o utilizador está associado tiver permissões para alertas.  

4.  Na caixa de diálogo **Adicionar Novos Alertas da Coleção** , escolha os alertas que pretende que sejam gerados quando os limites do estado do cliente são inferiores a um valor específico e, em seguida, clique em **OK**.  

5.  Na lista **Condições** do separador **Alertas** , selecione cada um dos alertas do estado do cliente e especifique as informações seguintes.  

    -   **Nome do alerta** - Aceite o nome predefinido ou introduza um novo nome para o alerta.  

    -   **Severidade de alerta** - A partir da lista de lançamentos, escolha o nível de alerta que será exibido na consola Do Gestor de Configuração.  

    -   **Aumentar o alerta** - Especifique a percentagem de limiar para o alerta.  

6.  Clique **em OK** para fechar a caixa de\> * &lt;* diálogo Collection Name**Properties.**  

##### <a name="to-configure-email-notification-for-alerts"></a>Para configurar notificações por e-mail para os alertas  

1.  Na consola do Gestor de Configuração navegar para **monitorizar** > as subscrições de**alertas.** > **Subscriptions**  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Configurar Notificação por Correio Eletrónico**.  

3.  Na caixa de diálogo **Propriedades do Componente de Notificação por E-mail** , especifique as seguintes informações:  

    -   **Ativar a notificação de e-mail para alertas**: Selecione esta caixa de verificação para permitir ao Gestor de Configuração utilizar um servidor SMTP para enviar alertas de e-mail.  

    -   **FQDN ou endereço IP do servidor SMTP para enviar alertas por e-mail**: introduza o nome de domínio completamente qualificado (FQDN) ou o endereço IP e a porta SMTP do servidor de e-mail que pretende utilizar para estes alertas.  

    -   Conta de ligação ao **servidor SMTP**: Especifique o método de autenticação para o Gestor de Configuração utilizar para ligar o servidor de e-mail.  

    -   **Endereço do remetente para enviar alertas por e-mail**: especifique o endereço de e-mail a partir da qual são enviados e-mails de alerta.  

    -   **Testar Servidor SMTP**: envia um e-mail de teste para o endereço de e-mail especificado em **Endereço do remetente para enviar alertas por e-mail**.  

4.  Clique em **OK** para guardar as definições e fechar a caixa de diálogo **Propriedades dos Componentes das Definições de E-mail** .  

##### <a name="to-subscribe-to-email-alerts"></a>Para subscrever alertas por e-mail  

1.  Na consola do Gestor de Configuração navegar para **monitorizar** > **alertas**.  

2.  Selecione um alerta e, em seguida, no separador **Home Page** , no grupo **Subscrição** , clique em **Criar subscrição**.  

3.  Na caixa de diálogo **Nova Subscrição** , especifique as seguintes informações:  

    -   **Nome**: introduza um nome para identificar a subscrição de e-mail. Pode utilizar até 255 carateres.  

    -   **Endereço de e-mail**: introduza os endereços de e-mail para os quais pretende que o alerta seja enviado. Pode separar os vários endereços de e-mail com ponto e vírgula.  

    -   **Idioma do e-mail**: na lista, especifique o idioma do e-mail.  

4.  Clique em **OK** para fechar a caixa de diálogo **Nova Subscrição** e para criar a subscrição de e-mail.  

    > [!NOTE]  
    >  Pode eliminar e editar subscrições na área de trabalho **Monitorização** , expandindo o nó **Alertas** e, em seguida, clique no nó **Subscrições** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> Monitorizar alertas  
 Para ver alertas, utilize o nó **Alertas** da área de trabalho **Monitorização** . Os alertas têm um dos seguintes estados de alerta:  

- **Nunca ativado**: a condição do alerta não foi cumprida.  

- **Ativo**: a condição do alerta foi cumprida.  

- **Cancelado**: a condição de um alerta ativo já não é cumprida. Este estado indica que a condição que causou o alerta está agora resolvida.  

- **Adiado**: Um utilizador administrativo configurou o Gestor de Configuração para avaliar o estado do alerta mais tarde.  

- **Desativado**: o alerta foi desativado por um utilizador administrativo. Quando um alerta está neste estado, o Gestor de Configuração não atualiza o alerta mesmo que o estado do alerta se mude.  

  Pode tomar uma das seguintes ações quando o Gestor de Configuração gera um alerta:  

- Resolver a condição que causou o alerta, por exemplo, resolver um problema de rede ou um problema de configuração que gerou o alerta. Depois de o Gestor de Configuração detetar que o problema já não existe, o estado de alerta altera-se para **cancelar**.  

- Se o alerta é um problema conhecido, pode adiar o alerta durante um período de tempo específico. Nessa altura, o Gestor de Configuração atualiza o alerta para o seu estado atual.  

   Apenas é possível adiar um alerta quando está ativo.  

- Pode editar o **Comentário** de um alerta para que outros utilizadores administrativos possam ver que tem conhecimento do alerta. Por exemplo, pode identificar no comentário a forma de resolver a condição, fornecer informações sobre o estado atual da condição ou explicar por que motivo adiou o alerta.  
