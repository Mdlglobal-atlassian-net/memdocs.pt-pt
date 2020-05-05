---
title: Configurar relatórios
titleSuffix: Configuration Manager
description: Como configurar relatórios na hierarquia do Gestor de Configuração, incluindo informações sobre os Serviços de Reporte de Servidores SQL.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ba67fee260867494302e49b7c9d3a97480e236b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723762"
---
# <a name="configure-reporting-in-configuration-manager"></a>Configure relatórios no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de poder criar, modificar e executar relatórios na consola do Gestor de Configuração, existem várias tarefas de configuração para serem completadas. Utilize este artigo para o ajudar a configurar relatórios na hierarquia do Gestor de Configuração.  

Antes de instalar e configurar os Serviços de Reporte de Servidores SQL na sua hierarquia, reveja os seguintes artigos de relatório do Gestor de Configuração:  

- [Introdução aos relatórios](introduction-to-reporting.md)  

- [Planear relatórios](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services é uma plataforma de reporte baseada em servidores que fornece uma funcionalidade de reporte abrangente para diferentes tipos de fontes de dados. O ponto de serviços de reporte no Gestor de Configuração comunica com os Serviços de Reporte de Servidores SQL para:

- Copy Configuration Manager reporta a uma pasta de relatório especificada
- Configurar as definições dos Serviços de Reporte
- Configurar as definições de segurança dos Serviços de Reporte

Quando executa um relatório, o componente de Serviços de Informação liga-se à base de dados do site do Gestor de Configuração para recuperar dados.  

Antes de poder instalar o ponto de serviços de reporte num site do Gestor de Configuração, instale e configure os Serviços de Relato do Servidor SQL no sistema de site alvo. Para mais informações, consulte instalar os Serviços de [Reporte do Servidor SQL](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>Verifique a instalação de Serviços de Reporte de Servidores SQL

Utilize o procedimento seguinte para verificar se o SQL Server Reporting Services está instalado e em execução sem problemas.

1. Vá ao menu **Iniciar** no sistema do site e abra o Gestor de Configuração de **Serviços de Reporte.** Pode encontrá-lo na secção **Ferramentas** de Configuração do grupo **Microsoft SQL Server.**

2. Na janela de ligação de configuração de **serviços** de reporte, introduza o nome do servidor que acolhe serviços de reporte de servidores SQL. Selecione a instância do Servidor SQL em que instalou serviços de reporte SQL. Em seguida, selecione **Connect** para abrir o Gestor de Configuração de Serviços de Reporte.  

3. Na página de Estado do **Servidor de Relatório,** verifique se o **Estado do Serviço de Relatório** está **iniciado**. Se não estiver neste estado, selecione **Iniciar**.  

4. Na página URL do **Serviço Web,** selecione o URL em **URLs**do Serviço Web do Serviço de Relatório . Esta ação testa a ligação à pasta do relatório. O navegador pode pedir-lhe credenciais. Certifique-se de que a página Web é aberta com êxito.

5. Na página Base de **Dados,** verifique se o **modo de servidor** de relatório está definido para **Nativo**.  

6. Na página URL do Gestor de **Relatórios,** selecione o URL no **Report Manager Identificação**do Site . Esta ação testa a ligação ao diretório virtual para Report Manager. O navegador pode pedir-lhe credenciais. Certifique-se de que a página Web é aberta com êxito.

    > [!NOTE]  
    > Reportar no Gestor de Configuração não requer Relatório de Relatório de Serviços de Reporte. Só precisa dele se quiser executar relatórios no navegador ou gerir relatórios utilizando o Report Manager.  

7. Selecione **Exit** para fechar o Gestor de Configuração de Serviços de Reporte.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Configure relatórios para usar Report Builder 3.0

1. No computador que executa a consola do Gestor de Configuração, abra o Editor do Registo do Windows.  

2. Navegue para `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Abra a chave **ReportBuilderApplicationManifestName** para editar os dados de valor.  

4. Mude o `ReportBuilder_3_0_0_0.application`valor para , e, em seguida, selecione **OK** para guardar.

5. Feche o Editor de Registo do Windows.  

## <a name="install-a-reporting-services-point"></a> Instalar um ponto do Reporting Services

Para gerir os relatórios no site, instale o ponto de serviços de reporte. Os serviços de reporte apontam:

- Cópias reportam pastas e relatórios aos Serviços de Reporte de Servidores SQL
- Aplica a política de segurança para os relatórios e pastas
- Define as definições de configuração nos Serviços de Reporte

### <a name="requirements-and-limitations"></a>Requisitos e limitações

Antes de poder visualizar ou gerir relatórios na consola Do Gestor de Configuração, precisa de um ponto de serviço de reporte. Configure a função do sistema do site num servidor com os Serviços de Relato do Servidor Microsoft SQL. Para mais informações, consulte [os pré-requisitos para reportar](prerequisites-for-reporting.md).  

- Quando selecionar um site para instalar o ponto de serviços de reporte, os utilizadores que acederem aos relatórios devem estar no mesmo âmbito de segurança que o site onde instala a função.  

- Depois de instalar um ponto de serviços de reporte num sistema de site, não altere o URL para o servidor de relatório.

    Por exemplo, cria-se o ponto de serviços de reporte. Em seguida, modifica o URL para o servidor de relatório no Gestor de Configuração de Serviços de Reporte. A consola 'Gestor de Configuração' continua a utilizar o URL antigo. Não pode executar, editar ou criar relatórios a partir da consola.

    Se precisar de alterar o URL do servidor de relatório, remova primeiro o ponto de serviços de reporte existente. Mude o URL e, em seguida, reinstale o ponto de serviços de reporte.  

- Quando instalar um ponto de serviços de reporte, especifique uma [conta de ponto de ponto de reporte](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)de serviços . Para que os utilizadores de um domínio diferente executem um relatório, criem uma confiança bidirecional entre domínios. Caso contrário, o relatório não corre.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" />Instale o ponto de serviços de reporte num sistema de site  

Para obter mais informações sobre a configuração dos sistemas do site, consulte [instalar as funções](../deploy/configure/install-site-system-roles.md)do sistema do site .  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó de Funções de **Servidores e Derôs.**  

1. Adicione os serviços de reporte apontar para um servidor de sistema de site novo ou existente:  

    - *Novo sistema*de site : No separador **Home** da fita, no grupo **Criar,** selecione **Criar servidor de sistema**de site . É aberto o **Assistente para Criar Servidor do Sistema de Sites** .  

    - *Sistema de site existente*: Selecione o servidor alvo. No separador **Home** da fita, no grupo **Servidor,** selecione **Adicionar função**do sistema do site . É aberto o **Assistente para Adicionar Funções ao Sistema de Sites** .  

1. Na página **Geral** , especifique as definições gerais para o servidor de sistema de sites. Quando adicionar os serviços de reporte apontar para um servidor existente, verifique os valores que configurapreviamente.  

1. Na página **de Seleção** de Funções do Sistema, selecione ponto de **serviços de reporte** na lista de funções disponíveis e, em seguida, selecione **Next**.  

1. Na página de ponto de ponto de **serviços de Report,** configure as seguintes definições:  

    - **Nome**do servidor da base de dados do site : Especifique o nome do servidor que acolhe a base de dados do site do Gestor de Configuração. O assistente normalmente recupera o nome de domínio totalmente qualificado (FQDN) para o servidor. Para especificar uma instância de &lt;base de dados, utilize o *nome*>\&do servidor de formato lt; nome> de *nome.* Por exemplo, `sqlserver\named1`.

    - **Nome da base de dados**: Especifique o nome da base de dados do site do Gestor de Configuração. Selecione **Verificar** se confirma se o assistente tem acesso à base de dados do site.  

        > [!IMPORTANT]  
        > A conta de utilizador que utiliza para criar o ponto de serviços de reporte deve ter **acesso** à base de dados do site. Se o teste de ligação falhar, é apresentado um ícone de aviso vermelho. O texto de hover contextual no ícone tem os detalhes da falha. Corrija a falha e, em seguida, selecione **Test** novamente.  

    - **Nome**da pasta : Especifique o nome da pasta para criar e utilizar para relatórios do Gestor de Configuração nos Serviços de Informação.  

    - **Instância do servidor de Serviços de Informação**: Selecione a instância do Servidor SQL para serviços de reporte. Se esta página não listar quaisquer instâncias, verifique se os Serviços de Reporte do Servidor SQL estão instalados, configurados e iniciados.  

        > [!IMPORTANT]  
        > O Gestor de Configuração faz uma ligação no contexto do utilizador atual ao WMI no sistema de site selecionado. Utiliza esta ligação para recuperar a instância do Servidor SQL para serviços de reporte. O utilizador atual deve ter **lido** o acesso ao WMI no sistema do site, ou o assistente não pode obter as instâncias dos Serviços de Informação.  

    - **Conta de ponto de ponto de serviços de reporte**: Selecione **Definir**, e, em seguida, selecione uma conta para usar. Os Serviços de Relato do Servidor SQL no ponto de serviços de reporte utilizam esta conta para se conectarem à base de dados do site do Gestor de Configuração. Esta ligação é para recuperar os dados para um relatório. Selecione **a conta existente** para especificar uma conta de utilizador do Windows que configuraprevia previamente como uma conta de 'Gestor de Configuração'. Selecione **Nova conta** para especificar uma conta de utilizador do Windows que não esteja configurada para utilização. O Gestor de Configuração concede automaticamente o acesso especificado ao utilizador à base de dados do site.  

        A conta que executa os Serviços de Informação deve pertencer ao grupo de segurança local de domínio **Windows Authorization Access Group**. Também precisa da permissão **Read tokenGroupsGlobalAndUniversal** para **permitir**. Os utilizadores num domínio diferente do que a conta ponto de serviços de reporte precisam de uma confiança bidirecional entre os domínios para executar relatórios com sucesso.

        A conta de utilizador e palavra-passe do Windows especificadas são encriptadas e armazenadas na base de dados do Reporting Services. O Reporting Services obtém os dados para relatórios na base de dados do site utilizando esta conta e palavra-passe.  

        > [!IMPORTANT]  
        > A conta que especifica deve ter a permissão **local** no servidor que acolhe a base de dados dos Serviços de Informação.  

1. Conclua o assistente.

Após o completo do assistente, o Gestor de Configuração cria as pastas de relatório nos Serviços de Reporte. Em seguida, copia os seus relatórios para as pastas de relatório especificadas.  

> [!TIP]  
> Para listar apenas os sistemas de site que acolhem a função de ponto de ponto de serviços de reporte, clique direito **servidores e funções**do sistema do site, e selecione ponto de **serviços de reporte**.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" />Línguas para relatórios

<!-- SCCMDocs#1067 -->

Quando o Gestor de Configuração cria pastas de relatório e copia relatórios para o servidor de relatório, determina o idioma apropriado para os objetos.

- Criar pastas de relatório, copiar relatórios

  - Criar objetos usando o local do servidor do site OS

  - Se o pacote de idiomas específico não estiver disponível, padrão para inglês (ENU)

- Ver relatórios em um navegador web

  - Nomes de pastas e relatórios: o mesmo local que o servidor do site
  
  - Conteúdo do relatório: dinâmico com base no local do navegador

- Ver relatórios na consola Do Gestor de Configuração

  - Nomes de pastas e relatórios: dinâmico com base no local da consola
  
  - Conteúdo do relatório: dinâmico com base no local da consola

Quando instala um ponto do Reporting Services num site sem pacotes de idiomas, os relatórios são instalados em inglês. Se instalar um pacote de idiomas depois de instalar o ponto do Reporting Services, terá de desinstalar e reinstalar o ponto do Reporting Services para que os relatórios sejam disponibilizados no idioma adequado do pacote de idiomas.  

Para mais informações, consulte [pacotes de idioma.](../deploy/install/language-packs.md)

### <a name="file-installation-and-report-folder-security-rights"></a>Instalação de ficheiros e direitos de segurança da pasta de relatórios

O Gestor de Configuração faz as seguintes ações para instalar o ponto de serviços de reporte e configurar os Serviços de Reporte:  

> [!IMPORTANT]  
> O site faz estas ações no contexto da conta que está configurada para o serviço SMS_Executive. Normalmente, esta conta é a conta do sistema local do servidor do site.  

- Instale a função de ponto de ponto dos serviços de reporte.  

- Crie a fonte de dados nos Serviços de Informação com as credenciais armazenadas que especificou no assistente. Esta conta é a conta de utilizador do Windows e a palavra-passe que os Serviços de Informação utilizam para se ligarem à base de dados do site quando executa relatórios.  

- Crie a pasta raiz do Gestor de Configuração nos Serviços de Reporte.  

- Adicione as funções de segurança dos utilizadores de **relatório configmgr** e dos administradores de **relatório configmgr** nos Serviços de Informação.  

- Crie subpastas e, em `%ProgramFiles%\SMS_SRSRP` seguida, implemente relatórios do Gestor de Configuração a partir do servidor do site para Serviços de Reporte.  

- Adicione a função de Utilizadores do **Relatório ConfigMgr** nos Serviços de Relato às pastas-raiz de todas as contas de utilizador no Gestor de Configuração que tenham direitos de Leitura do **Site.**  

- Adicione a função de Administradores de **Relatório configmgr** nos Serviços de Reporte às pastas-raiz de todas as contas de utilizador no Gestor de Configuração que tenham direitos **de Modificação do Site.**  

- Recupere o mapeamento entre as pastas de relatório e os tipos de objetos seguros do Gestor de Configuração. O Gestor de Configuração mantém este mapa na base de dados do site.  

- Configure os seguintes direitos para os utilizadores administrativos no Gestor de Configuração para pastas específicas de relatório em Serviços de Report:  

  - Adicione aos utilizadores e atribua a função de Utilizadores do **Relatório ConfigMgr** à pasta de relatório associada para utilizadores administrativos que tenham permissões do **Relatório de Execução** para o objeto do Gestor de Configuração.  

  - Adicione os utilizadores e atribua a função de Administradores de **Relatório configMgr** à pasta de relatório associada para utilizadores administrativos que tenham permissões **modificadas** do Relatório para o objeto do Gestor de Configuração.  

O Gestor de Configuração conecta-se aos Serviços de Informação e define as permissões para os utilizadores nas pastas raiz do Gestor de Configuração e dos Serviços de Report e nas pastas específicas do relatório. Após a instalação inicial do ponto de serviços de reporte, o Gestor de Configuração conecta-se aos Serviços de Informação a cada 10 minutos para verificar se os direitos de utilizador configurados nas pastas do relatório são os direitos associados que estão definidos para os utilizadores do Gestor de Configuração. Quando os utilizadores são adicionados ou os direitos dos utilizadores são modificados na pasta do relatório utilizando o Report Manager de Relatórios de Serviços de Reporte, o Gestor de Configuração substitui essas alterações utilizando as atribuições baseadas em papéis armazenadas na base de dados do site. O Gestor de Configuração também remove utilizadores que não têm direitos de reporte no Gestor de Configuração.  

### <a name="reporting-services-security-roles"></a>Funções de segurança de Serviços de Reporte

Quando o Gestor de Configuração instala o ponto de serviços de reporte, adiciona as seguintes funções de segurança nos Serviços de Reporte:  

- Utilizadores do **Relatório ConfigMgr**: Os utilizadores afetados com esta função de segurança só podem executar relatórios do Gestor de Configuração.  

- Administradores de **Relatório ConfigMgr**: Os utilizadores designados com esta função de segurança podem fazer todas as tarefas relacionadas com reporte no Gestor de Configuração.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a>Verificar a instalação

Verifique a instalação do ponto de serviços de reporte, analisando mensagens de estado específicas e entradas de ficheiros de registo. Utilize o procedimento seguinte para verificar se a instalação do ponto do Reporting Services foi bem-sucedida.  

> [!Note]  
> Se vir relatórios na subpasta **reporte** do nó **reporte** na área de **monitorização** na consola Do Gestor de Configuração, pode ignorar este procedimento.

### <a name="verify-installation-by-status-message"></a>Verificar a instalação por mensagem de estado

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o **Estado do Sistema**e selecione o nó de Estado do **Componente.**  

1. Selecione o componente **SMS_SRS_REPORTING_POINT.**  

1. No separador **Casa** da fita, no grupo **Componente,** selecione **Mostrar Mensagens,** e depois escolha **All**.  

1. Especifique uma data e hora por um período antes de instalar o ponto de serviços de reporte e, em seguida, selecione **OK**.  

1. Verifique o ID da mensagem de estado **1015**. Esta mensagem de estado indica que o ponto de serviços de reporte foi instalado com sucesso.

### <a name="verify-installation-by-log-file"></a>Verificar a instalação por ficheiro de registo

Abra o ficheiro **Srsrp.log,** localizado no diretório de **Registos** do caminho de instalação do Gestor de Configuração. Procure a `Installation was successful`corda.

Intereace este ficheiro de registo a partir do momento em que o ponto de serviços de reporte foi instalado com sucesso. Verifique se as pastas de relatórios foram criadas, se os relatórios foram implementados e se a política de segurança de cada pasta foi confirmada. Depois da última linha de confirmações da `Successfully checked that the SRS web service is healthy on server`política de segurança, procure a corda.  

## <a name="configure-a-certificate-to-author-reports"></a>Configure um certificado para relatórios de autor

Existem muitas opções para você para autor de relatórios em SQL Server Reporting Services. Quando cria ou edita relatórios na consola do Gestor de Configuração, o Gestor de Configuração abre o Report Builder para usar como ambiente de autoria. Independentemente da forma como é autor dos relatórios do Seu Gestor de Configuração, precisa de um certificado auto-assinado para autenticação do servidor no servidor de base de dados do site.

> [!NOTE]  
> Para obter mais informações sobre relatórios de autoria com os Serviços de Relato de Servidores SQL, consulte o ambiente de [autor do Report Builder](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

O Gestor de Configuração instala automaticamente o certificado no servidor do site e quaisquer funções do Fornecedor SMS. Pode criar ou editar relatórios a partir da consola 'Gestor de Configuração' quando os executa a partir de um destes servidores.

Quando criar ou modificar relatórios de uma consola do Gestor de Configuração num computador diferente, exporte o certificado a partir do servidor do site. O nome amigável do certificado específico é o FQDN do servidor do site na loja de **certificados Pessoas Fidedignas** para o computador local. Adicione este certificado à loja de **certificados Pessoas Fidedignas** no computador que executa a consola Do Gestor de Configuração.  

## <a name="modify-reporting-services-point-settings"></a>Modificar as definições de ponto de ponto de serviços de reporte

Depois de instalar esta função, pode modificar as definições de ligação e autenticação da base de dados do site nas propriedades de ponto de ponto de serviços de reporte.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó de Funções de **Servidores e Derôs.**  

    > [!TIP]  
    > Para listar apenas os sistemas de site que acolhem o ponto de serviços de reporte, clique no nó de Funções de **Servidores e Derôs** o site e selecione ponto de **serviços de reporte**.  

1. Selecione o sistema de site que acolhe o ponto de serviços de reporte. Em seguida, selecione as funções do sistema de ponto de ponto de **reporte** no painel de detalhes.

1. No separador **Role site** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

1. Pode modificar as seguintes definições nas Propriedades pontos de **reporte:**  

    - **Nome do servidor da base de dados do site**

    - **Nome da base de dados**

    - **Conta de utilizador**

1. Selecione **OK** para guardar as alterações e fechar as propriedades.  

Para obter mais informações sobre estas definições, consulte as descrições na secção para instalar o ponto de serviços de [reporte num sistema de site](#bkmk_install).

## <a name="power-bi-report-server"></a>Power BI Report Server

A partir da versão 2002, pode integrar relatórios com o Power BI Report Server. Para obter mais informações sobre a configuração, consulte [Integrar com o Power BI Report Server](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>Upgrade SQL Server

Para atualizar os Serviços de Reporte do Servidor SQL e sQL, remova primeiro o ponto de serviços de reporte do site. Depois de atualizar o SQL Server, reinstale o ponto de serviços de reporte no 'Gestor de Configuração'.

Se não seguir este processo, verá erros quando executar ou editar relatórios da consola Do Gestor de Configuração. Pode continuar a executar e editar relatórios com sucesso a partir de um navegador web.  

## <a name="configure-report-options"></a> Configurar opções de relatórios

Pode selecionar o ponto de serviços de reporte predefinido que utiliza para gerir relatórios. O site pode ter mais de um ponto de serviçode reporte, mas apenas utiliza o servidor predefinido para gerir relatórios. Utilize o procedimento seguinte para configurar opções de relatórios para o site.  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e, em seguida, selecione o nó **reporte.**  

1. No separador **Casa** da fita, no grupo **Definições,** selecione **Opções**de Relatório .  

1. Selecione o servidor de relatório predefinido na lista e, em seguida, selecione **OK**.

Se não mostrar servidores, verifique se instalou e configura um ponto de serviçode reporte no site. Para mais informações, consulte Verificar a [instalação](#bkmk_verify).

Certifique-se de que o seu computador executa uma versão do SQL Server Report Builder que corresponde à versão do Servidor SQL que utiliza para o seu servidor de relatórios. Caso contrário, verá um erro, o servidor de relatório predefinido não salvará e não poderá criar ou editar relatórios.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Passos seguintes

[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)
