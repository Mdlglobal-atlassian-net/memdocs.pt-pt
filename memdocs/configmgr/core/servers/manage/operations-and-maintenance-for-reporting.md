---
title: Operações e manutenção dos relatórios
titleSuffix: Configuration Manager
description: Conheça os detalhes da gestão de relatórios e reporte subscrições no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713717"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Operações e manutenção para reporte no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de a infraestrutura estar em vigor para reporte no Gestor de Configuração, existem várias operações que normalmente faz para gerir relatórios e reportar subscrições.

> [!NOTE]
> Este artigo centra-se em relatórios nos Serviços de Reporte de Servidores SQL. A partir da versão 2002, pode integrar relatórios com o Power BI Report Server. Para mais informações, consulte [Integrar com o Power BI Report Server](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Executar um relatório dos Serviços de Reportagem

O Gestor de Configuração armazena os seus relatórios nos Serviços de Reporte de Servidores SQL. O relatório recupera dados da base de dados do Site Do Gestor de Configuração. Pode aceder a relatórios na consola Do Gestor de Configuração ou utilizando o Report Manager através de um navegador web. Abram relatórios de um navegador web em qualquer computador que possa aceder ao ponto de serviços de reporte, e o utilizador tem direitos suficientes para visualizar os relatórios. Para executar relatórios, precisa de ler direitos de **leitura** para a permissão do **Site** e a permissão **do Relatório de Execução** para objetos específicos.

Quando executa um relatório, exibe o título, descrição e categoria do relatório na língua do sistema operativo local. Para mais informações, consulte [idiomas para obter informações.](configuring-reporting.md#-languages-for-reports)

> [!NOTE]  
> Report Manager é uma ferramenta de acesso e gestão de relatórios baseado na web. Pode usá-lo para administrar uma única instância de servidor de relatório sobre uma ligação HTTPS. Utilize o Gestor de Relatórios para tarefas operacionais: ver relatórios, modificar propriedades de relatórios e gerir subscrições de relatórios associadas. Este artigo fornece os passos para ver um relatório e modificar as propriedades do relatório no Report Manager. Para mais informações sobre outras opções no Report Manager, consulte [o que é report manager?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode)

Utilize os seguintes procedimentos para executar um relatório do Gestor de Configuração.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Executar um relatório na consola do Gestor de Configuração

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir **relatórios,** e, em seguida, selecionar **Relatórios**. Este nó lista os relatórios disponíveis.

    > [!TIP]
    > Se este nó não listar quaisquer relatórios, verifique se o ponto de serviços de reporte está instalado e configurado. Para mais informações, consulte [o relatório Configure](configuring-reporting.md).

1. Selecione o relatório que pretende executar. No separador **Home** da fita, na secção **Grupo relatório,** selecione **Executar** para abrir o relatório.

1. Se existirem parâmetros necessários, especifique-os e, em seguida, selecione **'Ver Relatório**' .

### <a name="run-a-report-in-a-web-browser"></a>Executar um relatório em um navegador web

1. No seu navegador web, vá ao URL `https://Server1/Reports`do Report Manager, por exemplo, . Encontre este endereço na página URL do Gestor de **Relatórios** no Gestor de Configuração de Serviços de Reporte.

1. No Report Manager, selecione a pasta de relatório para O Gestor de Configuração, por exemplo, **ConfigMgr_CAS**.

    > [!TIP]
    > Se o Gestor de Relatórios não listar quaisquer relatórios, verifique se o ponto de serviços de reporte está instalado e configurado. Para mais informações, consulte [o relatório Configure](configuring-reporting.md).

1. Selecione a categoria de relatório para o relatório que pretende executar e, em seguida, selecione o relatório específico. O relatório abre no Relatório Manager.

1. Se existirem parâmetros necessários, especifique-os e, em seguida, selecione **'Ver Relatório**' .

## <a name="modify-the-properties-of-a-report"></a>Modificar as propriedades de um relatório

As propriedades do relatório incluem o nome e descrição do relatório. Pode visualizar as propriedades para um relatório na consola Do Gestor de Configuração.

Para alterar as propriedades, utilize o Report Manager:

1. No seu navegador web, vá ao URL `https://Server1/Reports`do Report Manager, por exemplo, .

1. No Report Manager, selecione a pasta de relatório para O Gestor de Configuração, por exemplo, **ConfigMgr_CAS**.

1. Selecione a categoria de relatório e, em seguida, selecione o relatório específico. O relatório abre no Relatório Manager.

1. Selecione o separador **Propriedades.** Modificar o nome e a descrição do relatório e, em seguida, selecionar **Aplicar**.

O Gestor de Relatórios guarda as propriedades do relatório no servidor de relatórios. A consola Do Gestor de Configuração mostra as propriedades atualizadas do relatório para o relatório.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a>Editar um relatório

Quando um relatório de Gestor de Configuração existente não recuperar a informação que deseja, edite-a no Report Builder. Também pode utilizar o Report Builder para alterar o layout ou o desenho do relatório. Enquanto pode editar diretamente um relatório predefinido, o melhor é cloná-lo. Abra o relatório para editar e, em seguida, selecione **Save As**.

Para editar um relatório, precisa de permissão **de Modificação do Site** e **modificação** de permissões de relatório sobre os objetos específicos do relatório.

> [!IMPORTANT]
> As atualizações do site preservam relatórios incorporados. Se modificar um relatório padrão, quando o site atualiza, rebatiza`_`o relatório com um prefixo de sublinhado ( ). Este comportamento garante que a atualização do site não substitui o relatório modificado pelo relatório padrão.
>
> Se modificar relatórios predefinidos, antes de instalar uma atualização do site, faça o recorpo nos seus relatórios personalizados. Após a atualização, restaure o relatório nos Serviços de Informação. Se fizer alterações significativas num relatório predefinido, crie um novo relatório. Novos relatórios que cria antes de atualizar um site não são substituídos.

Utilize o seguinte procedimento para editar as propriedades para um relatório do Gestor de Configuração.

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir **relatórios**e, em seguida, selecionar o nó **relatório.**

1. Selecione o relatório que pretende modificar. No separador **Home** da fita, na secção **Grupo relatório,** selecione **Editar**. Pode instá-lo a introduzir credenciais. Se o Report Builder não estiver instalado no computador, o Gestor de Configuração pede-lhe para o instalar. O Construtor de Relatórios é obrigado a modificar e criar relatórios.

1. No Report Builder, modifique as definições de relatório apropriadas. Selecione **Guardar** para guardar o relatório para o servidor de relatório.

## <a name="create-reports"></a>Crie relatórios

Existem dois tipos de relatórios que pode criar:

- Um **relatório baseado em modelos** permite-lhe selecionar interativamente os itens que pretende incluir no seu relatório. Para obter mais informações sobre a criação de modelos de relatório personalizados, consulte Criar modelos de relatório personalizados para o Gestor de [Configuração nos Serviços de Relato do Servidor SQL](creating-custom-report-models-in-sql-server-reporting-services.md).

- Um **relatório baseado em SQL** permite-lhe recuperar dados baseados numa declaração sql de relatório.

> [!IMPORTANT]
> Para criar um novo relatório, a sua conta necessita de permissão **de Modificação do Site.** Só é possível criar um relatório em pastas para as quais tem permissões **de Relatório modificado.**

### <a name="create-a-model-based-report"></a>Criar um relatório baseado em modelos

Utilize o seguinte procedimento para criar um relatório de Gestor de Configuração baseado em modelos.

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.**

1. No separador **Casa** da fita, na secção **Criar,** selecione **Criar Relatório**. Esta ação abre o Assistente de **Relatório criar.**

1. Na página **Informação,** configure as seguintes definições:

    - **Tipo**: Selecione **Relatório baseado em modelos**.

    - **Nome**: Especificar um nome para o relatório.

    - **Descrição**: Especificar uma descrição do relatório.

    - **Servidor**: Mostra o nome do servidor de relatório onde cria este relatório.

    - **Caminho**: **Selecione Navegar** para especificar uma pasta na qual armazenar o relatório.

1. Na página De **Seleção** de Modelos, selecione um modelo disponível na lista para criar este relatório. A secção **Preview** exibe as vistas e entidades do SQL Server que estão disponíveis neste modelo de relatório.

1. Complete o Assistente de Relatório Criar.

1. Open Report Builder para configurar as definições do relatório. Para mais informações, consulte [editar um relatório do Gestor de Configuração](#bkmk_edit).

1. No Report Builder, crie o layout do relatório, selecione dados nas vistas disponíveis do SQL Server e adicione parâmetros ao relatório.

1. Selecione **Executar** para executar o seu relatório. Verifique se o relatório fornece as informações que espera. Se necessário, selecione **Design** para modificar ainda mais o relatório.

1. Selecione **Guardar** para guardar o relatório para o servidor de relatório.

### <a name="create-a-sql-based-report"></a>Criar um relatório baseado em SQL

Quando criar uma declaração SQL para um relatório personalizado, não faça referência diretamente às tabelas do SQL Server. Referência sempre a reportar visualizações do SQL Server suportadas pela base de dados do site. Estas opiniões têm `v_`nomes que começam com. Para mais informações, consulte [criar relatórios personalizados utilizando as vistas do Servidor SQL no Gestor](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)de Configuração .

Pode também fazer referência aos procedimentos armazenados públicos a partir da base de dados do site. Estes procedimentos armazenados têm `sp_`nomes que começam com.

Utilize o seguinte procedimento para criar um relatório de Configuração baseado em SQL.

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.**

1. No separador **Casa** da fita, na secção **Criar,** selecione **Criar Relatório**. Esta ação abre o Assistente de **Relatório criar.**

1. Na página **Informação,** configure as seguintes definições:

    - **Tipo**: Selecione **Relatório baseado em SQL**.

    - **Nome**: Especificar um nome para o relatório.

    - **Descrição**: Especificar uma descrição do relatório.

    - **Servidor**: Mostra o nome do servidor de relatório onde cria este relatório.

    - **Caminho**: **Selecione Navegar** para especificar uma pasta na qual armazenar o relatório.

1. Complete o Assistente de Relatório Criar.

1. Open Report Builder para configurar as definições do relatório. Para mais informações, consulte [editar um relatório do Gestor de Configuração](#bkmk_edit).

1. No Report Builder, forneça a declaração da SQL para o relatório. Também pode construir a declaração SQL utilizando colunas em vistas disponíveis. Se necessário, adicione parâmetros ao relatório.

1. Selecione **Executar** para executar o seu relatório. Verifique se o relatório fornece as informações que espera. Se necessário, selecione **Design** para modificar ainda mais o relatório.

1. Selecione **Guardar** para guardar o relatório para o servidor de relatório.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>Gerir as subscrições de relatórios

Reporte subscrições nos Serviços de Relato de Servidores SQL permitem configurar a entrega automática de relatórios especificados por e-mail ou para uma partilha de ficheiros em intervalos programados. Para configurar as subscrições de relatório, utilize o Assistente de **Subscrição Criar** no Gestor de Configuração.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Criar uma subscrição de relatório para entregar um relatório a uma parte de ficheiro

Quando cria uma subscrição de relatório para entregar um relatório a uma parte de ficheiro, os Serviços de Informação copiam o relatório no formato especificado para a partilha de ficheiros que especifica. Pode subscrever e solicitar a entrega de apenas um relatório de cada vez.

Quando criar uma subscrição que utilize uma partilha de ficheiros, especifique uma pasta partilhada existente como destino. O servidor de relatório não cria a pasta ou a partilha da rede. Quando especificar a pasta de destino numa subscrição, utilize um caminho unc`\`e não inclua recuos na trajetória das pastas. O exemplo seguinte é um caminho cNU `\\server\reportfiles\operations\2001`válido para a pasta de destino: .

> [!NOTE]
> Ao criar a subscrição, especifice um nome de utilizador e uma palavra-passe. Esta conta precisa de acesso a esta partilha com permissões **de Escrita** para a pasta de destino.

Os Serviços de Informação podem apresentar relatórios em diferentes formatos de ficheiros. Por exemplo, MHTML ou Excel. Selecione o formato quando criar a subscrição. Embora possa selecionar qualquer formato de renderização suportado, alguns formatos funcionam melhor do que outros quando renderizam um ficheiro.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Limitações para subscrições de relatório saem a uma parte de ficheiro

A lista seguinte inclui as limitações das assinaturas de relatórios a uma parte de ficheiro:

- Ao contrário dos relatos que acolhe e gere num servidor de relatório, os Serviços de Informação entregam relatórios a uma pasta partilhada como ficheiros estáticos.

- As características interativas do relatório não funcionam para relatórios armazenados como ficheiros. O relatório representa quaisquer características interativas como elementos estáticos.

- Se o relatório incluir gráficos, utiliza a apresentação predefinida.

- Se o relatório se ligar a outro relatório, torna o link como texto estático.

Se quiser manter as funcionalidades interativas num relatório entregue, utilize a entrega de e-mail. Para mais informações, consulte Criar uma subscrição de [relatório para entregar um relatório por e-mail](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Processo para criar uma subscrição de relatório para uma partilha de ficheiros

Utilize o seguinte procedimento para criar uma subscrição de relatório para entregar um relatório a uma parte de ficheiro.  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.**

1. Selecione uma pasta de relatório e, em seguida, selecione o relatório a que pretende subscrever. No separador **Home** da fita, na secção **Grupo relatório,** selecione **Criar Subscrição**. Esta ação abre o Assistente de **Subscrição Create**.

1. Na página de Entrega de **Assinaturas,** configure as seguintes definições:  

    - **Relatório entregue por**: Selecione **Windows File Share**.

    - **Nome do ficheiro**: Especifique o nome do ficheiro para o relatório. Por defeito, o ficheiro de relatório não inclui uma extensão de nome de ficheiro. **Selecione Adicionar extensão de ficheiro quando criado** para adicionar automaticamente uma extensão de nome de ficheiro com base no formato.

    - **Caminho**: Especifique um caminho unc para uma pasta existente onde pretende entregar este relatório. Por exemplo, `\\server\reportfiles\operations`.

    - **Formato render :** Selecione um dos seguintes formatos para o ficheiro de relatório:

      - **Ficheiro XML com dados do relatório**
      - **CSV (vírem delimitada)**
      - **Ficheiro TIFF**
      - **Arquivo Acrobat (PDF)**
      - **HTML 4.0**
        > [!NOTE]
        > Se o seu relatório tiver imagens, o formato HTML 4.0 não as inclui.
      - **MHTML (arquivo web)**
      - **RPL Renderer** (Layout da página de relatório)
      - **Excel**
      - **Word**

    - **Nome do utilizador**: Especifique uma conta de utilizador do Windows com permissões de *escrita* para o **caminho**especificado .

    - **Palavra-passe**: Especifique a palavra-passe para a conta de utilizador do Windows acima.

    - **Opção de sobreescrita**: Selecione uma das seguintes opções para configurar o comportamento quando existe um ficheiro com o mesmo nome na pasta de destino:

      - **Sobrepor um ficheiro existente com uma versão mais recente**
      - **Não sobrepor um ficheiro existente**
      - **Incremente os nomes de ficheiros como versões mais recentes :** Esta opção anexa um número ao nome de ficheiro do novo relatório para distingui-lo de versões anteriores.

    - **Descrição**: Opcionalmente, especifique informações adicionais sobre esta subscrição do relatório.

1. Na página **'Agenda** de Assinaturas', selecione uma das seguintes opções de calendário de entrega para a subscrição do relatório:

    - **Utilizar a programação partilhada**: Um horário partilhado é um calendário previamente definido que pode ser usado por outras subscrições de relatório. Quando selecionar esta opção, selecione também um horário partilhado. Se não houver horários partilhados, selecione a opção de criar um novo horário.

    - **Criar um novo horário**: Configure o horário em que este relatório corre. O horário inclui o intervalo, a hora e a data de início e a data de fim para esta subscrição. Por padrão, uma nova subscrição cria um novo horário para ser executado a cada hora a partir da data e hora atuais.

1. Na página **Desclassificação** de Parâmetros de Subscrição, especifique quaisquer parâmetros que este relatório exija executar sem vigilância. Se o relatório não tiver parâmetros, o assistente não apresenta esta página.

1. Conclua o assistente.

1. Verifique se o Gestor de Configuração criou com sucesso a subscrição do relatório. Selecione o nó **de Subscrições** para visualizar e modificar as subscrições do relatório.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>Criar uma subscrição de relatório para entregar um relatório por e-mail

Quando cria uma subscrição de relatório para entregar um relatório por e-mail, os Serviços de Informação enviam um e-mail aos destinatários que configura. O e-mail inclui o relatório como anexo. O servidor de relatório não valida endereços de e-mail nem os obtém de um servidor de e-mail. Pode enviar por email a informação sobre qualquer conta de e-mail válida dentro ou fora da sua organização.

> [!NOTE]
> Para ativar a opção de subscrição de **email,** precisa configurar as definições de e-mail nos Serviços de Informação. Para mais informações, consulte a [entrega por e-mail nos serviços de reporte.](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services)

Pode selecionar uma ou ambas as seguintes opções de entrega de e-mail:

- Envie uma notificação com um link para o relatório gerado.

- Envie um relatório incorporado ou anexo. O formato de renderização e o navegador determinam se incorpora ou anexa o relatório.

  - Se o seu navegador suportar HTML 4.0 e MHTML, e selecionar o formato **MHTML (arquivo web),** o e-mail incorpora o relatório na mensagem.
  - Todos os outros formatos fornecem relatórios como anexos.
  - Os Serviços de Informação não verificam o tamanho do anexo ou mensagem antes de enviar o relatório. Se o anexo ou mensagem exceder o limite máximo permitido pelo seu servidor de correio, o relatório não é entregue.

Utilize o seguinte procedimento para criar uma subscrição de relatório para entregar um relatório através do e-mail.  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.**

1. Selecione uma pasta de relatório e, em seguida, selecione o relatório a que pretende subscrever. No separador **Home** da fita, na secção **Grupo relatório,** selecione **Criar Subscrição**. Esta ação abre o Assistente de **Subscrição Create**.

1. Na página de Entrega de **Assinaturas,** configure as seguintes definições:  

    - **Relatório entregue por**: Selecione **E-mail**.

    - **Para:** Especificar um endereço de e-mail válido como destinatário.

        > [!NOTE]
        > Para introduzir vários destinatários, separe cada`;`endereço de e-mail com um ponto evívia ( ).

    - **Cc**: Opcionalmente, especifique um endereço de e-mail para receber uma cópia deste relatório.

    - **Bcc**: Opcionalmente, especifique um endereço de e-mail para receber uma cópia cega deste relatório.

    - **Resposta Para**: Especificar o endereço de resposta. Se o destinatário responder à mensagem de e-mail, a resposta vai para este endereço.

    - **Objeto**: Especificar uma linha de assunto para a mensagem de e-mail de subscrição.

    - **Prioridade**: Selecione a bandeira prioritária para esta mensagem de e-mail: **Low,** **Normal**ou **High**. O Microsoft Exchange utiliza esta bandeira para indicar a importância da mensagem de e-mail.

    - **Comentário**: Especificar texto para o corpo da mensagem de e-mail de subscrição.

    - **Descrição**: Opcionalmente, especifique informações adicionais sobre esta subscrição do relatório.

    - **Incluir Link**: Incluir o URL para este relatório no corpo da mensagem de e-mail.

    - **Incluir relatório**: Anexar o relatório à mensagem de e-mail. Utilize a opção **Render Format** para especificar o formato do relatório a anexar.

    - **Formato render :** Selecione um dos seguintes formatos para o ficheiro de relatório anexo:

      - **Ficheiro XML com dados do relatório**
      - **CSV (vírem delimitada)**
      - **Ficheiro TIFF**
      - **Arquivo Acrobat (PDF)**
      - **MHTML (arquivo web)**
      - **Excel**
      - **Word**

1. Na página **'Agenda** de Assinaturas', selecione uma das seguintes opções de calendário de entrega para a subscrição do relatório:

    - **Utilizar a programação partilhada**: Um horário partilhado é um calendário previamente definido que pode ser usado por outras subscrições de relatório. Quando selecionar esta opção, selecione também um horário partilhado. Se não houver horários partilhados, selecione a opção de criar um novo horário.

    - **Criar um novo horário**: Configure o horário em que este relatório corre. O horário inclui o intervalo, a hora e a data de início e a data de fim para esta subscrição. Por padrão, uma nova subscrição cria um novo horário para ser executado a cada hora a partir da data e hora atuais.

1. Na página **Desclassificação** de Parâmetros de Subscrição, especifique quaisquer parâmetros que este relatório exija executar sem vigilância. Se o relatório não tiver parâmetros, o assistente não apresenta esta página.

1. Conclua o assistente.

1. Verifique se o Gestor de Configuração criou com sucesso a subscrição do relatório. Selecione o nó **de Subscrições** para visualizar e modificar as subscrições do relatório.
