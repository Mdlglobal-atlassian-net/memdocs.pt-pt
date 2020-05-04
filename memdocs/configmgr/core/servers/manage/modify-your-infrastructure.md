---
title: Modificar a infraestrutura
titleSuffix: Configuration Manager
description: Faça alterações ou tome ações que afetem a sua infraestrutura de Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713675"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Modifique a sua infraestrutura de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de instalar um ou mais sites, poderá ter de modificar configurações ou tomar ações que afetem a sua infraestrutura.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a>Gerir o fornecedor de SMS

O fornecedor SMS fornece o ponto de contacto administrativo para uma ou mais consolas do Gestor de Configuração. Ao instalar vários fornecedores de SMS, pode fornecer redundância para pontos de contacto para administrar o seu site e hierarquia.

Em cada site do Gestor de Configuração, pode reexecutar a configuração para:

- Adicione uma instância adicional do fornecedor de SMS. Cada instância adicional do fornecedor de SMS deve estar num computador separado.

- Remova uma instância do fornecedor de SMS. Para remover o último fornecedor de SMS para um site, tem de desinstalar o site.

Monitorize a instalação ou remoção do fornecedor SMS visualizando o **registo ConfigMgrSetup na** pasta raiz do servidor do site em que executa a configuração.

Antes de modificar o fornecedor de SMS num site, consulte [plan para o fornecedor de SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Gerir a configuração do fornecedor SMS para um site  

1. Executar **Configuração** do `\BIN\X64\setup.exe` Gestor de Configuração a partir da pasta de instalação do Site do Gestor de Configuração.

1. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este site**.

1. Na página de Manutenção do **Site,** selecione Modificar a configuração do **fornecedor SMS**.

1. Na página **de fornecedores de SMS de Gestão,** selecione uma das seguintes opções:

    - Adicione um novo fornecedor de **SMS**: Especifique o FQDN para um computador para hospedar o fornecedor SMS que não o acolhe atualmente.

    - **Desinstale o fornecedor de SMS especificado**: Selecione o nome do computador a partir do qual pretende remover o fornecedor de SMS.

    > [!TIP]  
    > Para mover o fornecedor de SMS entre dois computadores, instale-o primeiro no novo computador. Em seguida, retire-o do local original. Não há opção de mover o fornecedor de SMS entre computadores.

Após o acabamento do assistente de configuração, a configuração do fornecedor SMS está completa. No site **Propriedades**, no separador **Geral,** verifique os computadores que têm um fornecedor de SMS instalado para um site.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>Gerir a consola de Gestor de Configuração

As seguintes tarefas ajudam-no a gerir a consola Do Gestor de Configuração:

- Para modificar o idioma que exibe na consola 'Gestor de Configuração', consulte a secção de idiomas de [consola do Manage Configuration Manager.](#BKMK_ManageConsoleLanguages)

- Para instalar consolas adicionais, consulte as [consolas 'Instalar ' Gestor de Configuração.'](../deploy/install/install-consoles.md)

- Para configurar permissões DCOM para ativar as consolas que estão afastadas do servidor do site, consulte as [permissões do DCOM configurar para](#BKMK_ConfigDCOMforRemoteConsole) a secção de consolas do Gestor de Configuração remota.

- Para modificar permissões administrativas para limitar o que os utilizadores podem ver e fazer na consola, consulte [Modificar o âmbito administrativo de um utilizador administrativo](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>Gerir o idioma da consola do Gestor de Configuração

Durante a instalação do servidor do site, os ficheiros de instalação `\Tools\ConsoleSetup` da consola do Gestor de Configuração e os pacotes de idiomas suportados para o site são copiados para a subpasta do caminho de instalação do Gestor de Configuração no servidor do site.

- Quando inicia a instalação da consola Do Gestor de Configuração a partir desta pasta no servidor do site, ele copia a consola do Gestor de Configuração e suporta ficheiros de pack de idiomas para o computador.

- Quando um pacote de idiomas está disponível para a definição de idioma atual no computador, a consola 'Gestor de Configuração' abre nesse idioma.

- Se o pacote de idiomas associado não estiver disponível para a consola 'Gestor de Configuração', a consola abre em inglês (Estados Unidos).

Por exemplo, instala a consola 'Gestor de Configuração' a partir de um servidor de site que suporta inglês, alemão e francês. Se abrir a consola Do Gestor de Configuração num computador com uma definição de idioma configurada de francês, a consola abre em francês. Se abrir a consola Do Gestor de Configuração num computador com um idioma configurado de japonês, a consola abre em inglês porque o pacote de idiomas japonês não está disponível.  

Cada vez que a consola do Gestor de Configuração abre:

- Tt determina as definições de idioma configuradas para o computador
- Verifica se um pacote de idiomas associado está disponível para a consola 'Gestor de Configuração'
- Abre a consola utilizando o pacote de idiomas apropriado

Quando pretender abrir a consola 'Gestor de Configuração' em inglês, independentemente das definições de idioma configuradas no computador, remova ou mude o nome dos ficheiros do pack de idiomas no computador.

Utilize os seguintes procedimentos para iniciar a consola 'Gestor de Configuração' em inglês, independentemente da definição configurada do local no computador.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Instale uma versão apenas em Inglês da consola 'Gestor de Configuração' em computadores  

1. No Windows Explorer, `\Tools\ConsoleSetup\LanguagePack` navegue até ao caminho de instalação do Gestor de Configuração.

1. Mude o nome dos ficheiros **.msp** e **.mst**. Por exemplo, pode alterar ** &lt;o nome\>do ficheiro . MSP** ** &lt;para\>arquivar nome . MSP.desativado**.

1. Instale a consola 'Gestor de Configuração' no computador.

    > [!IMPORTANT]
    > Quando os novos idiomas do servidor estiverem configurados para o servidor do site, os ficheiros .msp e .mst são recocopiados para a pasta **IdiomPack,** e deve repetir este procedimento para instalar novas consolas do Gestor de Configuração apenas em inglês.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Desative temporariamente uma linguagem de consola numa instalação de consola existente do Gestor de Configuração

1. No computador que está a executar a consola 'Gestor de Configuração', feche a consola do Gestor de Configuração.

1. No Windows Explorer, &lt;navegue até *consoleinstallationPath*>\Bin\ no computador de consola do Gestor de Configuração.  

1. Mude o nome da pasta de idiomas apropriada para o idioma que se encontra configurado no computador. Por exemplo, se as definições de idioma do computador tiverem sido definidas para alemão, poderá mudar o nome da pasta **de** para **de.disabled**.  

1. Para abrir a consola 'Gestor de Configuração' no idioma configurado para o computador, mude o nome da pasta para o nome original. Por exemplo, mude o nome **de.disabled** para **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a>Configure permissões dCOM para consolas remotas

A conta de utilizador que executa a consola Do Gestor de Configuração requer permissão para aceder à base de dados do site utilizando o fornecedor SMS. No entanto, um utilizador administrativo que utiliza uma consola remote Configuration Manager também requer permissões dCOM de **ativação remota** em:

- O computador do servidor do site

- Cada computador que acolhe uma instância do fornecedor de SMS

O grupo de segurança chamado **SMS Admins** concede acesso ao fornecedor de SMS num computador, e também pode ser usado para conceder as permissões dCOM necessárias. Este grupo é local para o computador quando o fornecedor sMS executa num servidor membro. É um grupo local de domínio quando o fornecedor de SMS funciona num controlador de domínio.

> [!IMPORTANT]
> A consola 'Gestor de Configuração' utiliza o WMI para se ligar ao fornecedor SMS, e o WMI utiliza internamente o DCOM. Se a consola do Gestor de Configuração for executado num computador que não seja o computador fornecedor sms, requer permissões para ativar um servidor DCOM no computador fornecedor sms. Por predefinição, a Ativação Remota só é concedida aos membros do grupo de Administradores incorporados.
>
> Se permitir que o grupo SMS Admins tenha permissão de Ativação Remota, um membro deste grupo pode tentar ataques de DCOM contra o computador fornecedor sMS. Esta configuração também aumenta a superfície de ataque do computador. Para atenuar esta ameaça, monitorize cuidadosamente os membros do grupo Admins de SMS.

Utilize o seguinte procedimento para configurar cada site de administração central (CAS), servidor de site primário e cada computador onde o fornecedor SMS está instalado para conceder acesso remoto à consola do Gestor de Configuração para utilizadores administrativos.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Configure permissões dCOM para ligações remotas de consola do Gestor de Configuração

1. Como administrador no computador-alvo, corra `Dcomcnfg.exe` para abrir os **Serviços de Componentes.**

1. Expandir **Serviços de Componentes,** expandir **Computadores,** e depois selecionar **o Meu Computador.** No menu **Ação,** selecione **Propriedades**.

1. Na janela **My Computer Properties,** mude para o separador **de segurança COM.** Na secção **de Permissões de Lançamento e Ativação,** selecione Limites de **Edição**.

1. Na janela **de permissões de lançamento e ativação,** selecione **Adicionar**.

1. Nas **janelaS De Utilizadores, Computadores, Contas de Serviço ou Grupos,** `SMS Admins`na janela Enter the object para **selecionar** campo, escrever, e depois selecionar **OK**.

   > [!TIP]
   > Para localizar o grupo SMS Admins, poderá ter de alterar a definição: **A partir deste Local**. Este grupo é local para o computador quando o fornecedor SMS funciona num servidor membro, e é um grupo local de domínio quando o fornecedor sms executa em um controlador de domínio.

1. Nas Permissões para a secção **SMS Admins,** para permitir a ativação remota, selecione a coluna **Permitir** a linha **de ativação remota.**

1. Selecione **OK** para guardar alterações e fechar todas as janelas.

O seu computador está agora configurado para permitir o acesso remoto à consola do Gestor de Configuração aos membros do grupo SMS Admins.

Repita este procedimento em cada computador fornecedor de SMS que suporta as consolas do Gestor de Configuração remota.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>Modificar a configuração da base de dados do site

Depois de instalar um site, pode modificar a configuração da base de dados do site e do servidor de base de dados do site. Executar configuração do Gestor de Configuração num servidor CAS ou servidor de site primário para fazer alterações. Pode mover a base de dados do site para uma nova instância do SQL Server no mesmo computador, ou para outro computador que execute uma versão suportada do SQL Server. Estas alterações não são suportadas para a configuração da base de dados em sites secundários.

Para obter mais informações sobre os limites do suporte, veja [Política de suporte para alterações manuais da base de dados num ambiente do Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Quando modifica a configuração da base de dados para um site, o Gestor de Configuração reinicia ou reinstala os serviços do Gestor de Configuração no servidor do site e servidores de sistemas de site remoto que comunicam com a base de dados.

### <a name="modify-the-database-configuration"></a>Modificar a configuração da base de dados

Executar configuração do Gestor de Configuração no servidor do site e selecionar a opção Executar a manutenção do **site ou redefinir este site**. Em seguida, selecione a opção de **configuração do Servidor SQL modificar.** Pode alterar as seguintes configurações de bases de dados do site:

- O servidor baseado no Windows que acolhe a base de dados.

- A instância do SQL Server utilizada num servidor que aloja a base de dados do SQL Server.

- O nome da base de dados.

- Porta do Servidor SQL em uso pelo Gestor de Configuração.

- Porta de corretor de serviço sql server em uso pelo Gestor de Configuração.

### <a name="move-the-site-database"></a>Mova a base de dados do site

Se mover a base de dados do site, consulte também as seguintes configurações:

- Quando mover a base de dados do site para um novo computador, adicione a conta de computador do servidor do site ao grupo **de Administradores locais** no computador que executa o Servidor SQL. Se utilizar um cluster do SQL Server para a base de dados do site, adicione a conta de computador ao grupo de **Administradores locais** de cada computador de cluster do Windows Server.

- Quando mover a base de dados para uma nova instância no SQL Server, ou para um novo computador SQL Server, ative a integração do tempo de execução do idioma comum (CLR). Utilize o Estúdio de Gestão de **Servidores SQL** para se ligar à instância do SQL Server que acolhe a base de dados do site. Em seguida, executar o seguinte procedimento armazenado como uma consulta:`sp_configure 'clr enabled',1; reconfigure`

- Certifique-se de que o novo Servidor SQL tem acesso à localização de reserva. Quando utilizar um UNC para armazenar a cópia de segurança da base de dados do seu site, depois de passar a base de dados para um novo servidor, certifique-se de que a conta de computador do novo Servidor SQL tem permissões de **escrita** para a localização da UNC. Esta configuração inclui quando se muda para um grupo de disponibilidade sQL Server AlwaysOn ou um cluster de Servidor SQL.

> [!IMPORTANT]
> Antes de mover uma base de dados que tenha uma ou mais réplicas de base de dados para pontos de gestão, primeiro remova as réplicas da base de dados. Após concluir a mudança da base de dados, poderá reconfigurar as réplicas de base de dados. Para mais informações, consulte réplicas de Base de [Dados para pontos](../deploy/configure/database-replicas-for-management-points.md)de gestão .

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>Gerir o SPN para o servidor de base de dados do site

Pode escolher a conta que executa os serviços SQL para a base de dados do site:

- Quando os serviços são executados com a conta do sistema de computadores, regista automaticamente o nome principal do serviço (SPN) para si.

- Quando os serviços forem executados com uma conta de utilizador local de domínio, registe manualmente o SPN. O SPN permite que clientes SQL e outros sistemas de sites se autentiquem com a Kerberos. Sem autenticação Kerberos, a comunicação com a base de dados poderá falhar.

Para obter mais informações sobre as ligações SPNs e Kerberos, consulte Registar um nome principal de [serviço para ligações Kerberos](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Registe um SPN para a conta de serviço SQL Server do servidor de base de dados do site utilizando a ferramenta **Setspn.** Execute setspn como administrador de domínio num computador no mesmo domínio que o Servidor SQL.

Os seguintes procedimentos são exemplos de como gerir o SPN para a conta de serviço SQL Server. Para mais informações sobre Setspn, consulte a visão geral de [Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Criar manualmente um utilizador de domínio SPN para a conta de serviço SQL Server

1. Abra uma linha de comandos como administrador.

1. Insira um comando válido para criar o SPN tanto para o nome NetBIOS como para o FQDN:

    > [!IMPORTANT]
    > Quando criar um SPN para um Servidor SQL agrupado, especifique o nome virtual do cluster Do Servidor SQL como o nome do computador SQL Server.

    - Nome NetBIOS:`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Por exemplo: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN:`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Por exemplo: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > O comando para registar um SPN para uma instância nomeada pelo SQL Server é o mesmo que utiliza quando regista um SPN para uma instância predefinida. A única exceção é que o número da porta deve corresponder à porta que a instância nomeada utiliza.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Verifique se o utilizador de domínio SPN está registado corretamente

1. Abra uma linha de comandos como administrador.

1. Insira o seguinte comando:`setspn -L <domain\SQL service account>`

    Por exemplo: `setspn -L contoso\sqlservice`

1. Reveja o **Nome principal**do serviço registado . Certifique-se de que criou um SPN válido para o Servidor SQL.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Alterar a conta de serviço SQL Server do sistema local para uma conta de utilizador de domínio

1. Crie ou selecione a conta de utilizador de domínio ou de sistema local que pretende utilizar como a conta de serviço do SQL Server.

1. Abra o **Gestor de Configuração do SQL Server**.

1. Selecione **Serviços de Servidor EsqL**e abra o NOME **&lt;\>** DA INSTÂNCIA DO Servidor SQL .

1. Mude para o **separador Iniciar.** Selecione **esta conta**e introduza o nome de utilizador e a palavra-passe para a conta de utilizador do domínio a partir do passo 1.

1. Confirme a alteração da conta de serviço e reinicie o serviço SQL Server.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>Executar um reset do site

Quando um reset do site corre num CAS ou no local primário, o site:

- Reaplica o ficheiro padrão do Gestor de Configuração e as permissões de registo

- Reinstala todos os componentes do site e todas as funções do sistema do site

Os sites secundários não suportam o reset do site.

Pode repor manualmente um site. Também podem ser executados automaticamente depois de modificar a configuração do site. Por exemplo:

- Se tiver havido uma alteração nas contas utilizadas pelos componentes do Gestor de Configuração, considere um reset manual do site. Esta ação garante que os componentes do site atualização para usar os novos detalhes da conta.

- Se modificar os idiomas do cliente ou do servidor num site, o Gestor de Configuração executa automaticamente um reset do site. O site requer um reset para usar as novas línguas.

> [!NOTE]
> Um reset do site não repõe permissões de acesso a objetos do Gestor de Não Configuração.

### <a name="what-happens-during-a-site-reset"></a>O que acontece durante um reset do site

Quando uma reposição do site é executada:

1. A configuração para e reinicia o serviço **de SMS_SITE_COMPONENT_MANAGER** e os componentes de fio do serviço **SMS_EXECUTIVE.**

1. A configuração remove e recria a pasta de partilha do sistema do site e o componente **SMS Executive** no computador local e em computadores do sistema de sites remotos.

1. A configuração reinicia o serviço **SMS_SITE_COMPONENT_MANAGER,** que instala os **serviços de SMS_EXECUTIVE** e **SMS_SQL_MONITOR.**

O reset do local restaura os seguintes objetos:

- As chaves de registo **SMS** ou **NAL**, bem como outras subchaves predefinidas sob destas chaves.

- A árvore de diretório de ficheiros do Gestor de Configuração e quaisquer ficheiros ou subdiretórios padrão nesta árvore de diretório de ficheiros.

### <a name="prerequisites-for-site-reset"></a>Pré-requisitos para reset do site

A conta que utiliza para repor um site deve ter as seguintes permissões:

- Para redefinir o CAS:

  - Um **administrador** local no servidor CAS

  - Privilégios equivalentes ao papel de segurança da administração baseado em funções de **Administrador Completo**

- Para repor um local primário:

  - Um **administrador** local no servidor do site primário

  - Privilégios equivalentes ao papel de segurança da administração baseado em funções de **Administrador Completo**
  
  - Se o site principal estiver numa hierarquia com um CAS, esta conta também deve ser um **Administrador** local no servidor CAS.

### <a name="limitations-for-a-site-reset"></a>Limitações para um reset do site

Se a hierarquia estiver configurada para suportar atualizações de [clientes de teste numa recolha de pré-produção,](../../clients/manage/upgrade/test-client-upgrades.md)não pode utilizar um reset do site para alterar os pacotes de idiomas de servidor ou cliente nos sites.

### <a name="run-a-site-reset"></a>Executar uma reposição do site

1. Iniciar a configuração do Gestor de Configuração no servidor do site utilizando um dos seguintes métodos:

    - No menu **Iniciar,** selecione Configuração do Gestor de **Configuração**.

    - No diretório para os meios de `\SMSSETUP\BIN\X64\setup.exe`instalação do Gestor de *Configuração,* aberto. Certifique-se de que esta versão é a mesma que a versão do site.

    - No diretório onde o Gestor de `\BIN\X64\setup.exe`Configuração está *instalado,* aberto.

1. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este site**.

1. Na página de Manutenção do **Site,** selecione **reset site sem alterações de configuração**.

1. Selecione **Sim** para iniciar o reset do site.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>Gerir pacotes de idiomas num site

Depois de um site instalar, pode alterar os pacotes de idioma do servidor e cliente que estão em uso.

### <a name="server-language-packs"></a>Pacotes de idiomas do servidor

*Aplica-se a: Instalações de consolas Do Gestor de Configuração, novas instalações de funções do sistema de site aplicáveis*

Depois de atualizar os pacotes de idiomas do servidor num site, pode adicionar suporte para os packs de idiomas às consolas do Gestor de Configuração.

Para adicionar suporte para um pacote de idiomas de servidor a uma consola de Configuração Manager, instale a consola do Gestor de Configuração a partir da pasta **ConsoleSetup** num servidor de site que inclui o pacote de idiomas que pretende utilizar. Se a consola Do Gestor de Configuração já estiver instalada, tem primeiro de desinstalá-la para permitir que a nova instalação identifique a lista atual de pacotes de idiomas suportados.

### <a name="client-language-packs"></a>Pacotes de linguagem cliente

As alterações aos pacotes de idioma do cliente atualizam os ficheiros de origem de instalação do cliente. Novas instalações e upgrades de clientes adicionam suporte para a lista atualizada de idiomas de clientes.

Depois de atualizar os pacotes de idiomas do cliente num site, instale cada cliente que utilizará os packs de idiomas utilizando ficheiros de origem que incluam os pacotes de idioma do cliente.

Para obter mais informações sobre os idiomas do cliente e do servidor que o Gestor de Configuração suporta, consulte ['Packs' de Idiomas](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Modificar os pacotes de idiomas suportados num site

1. Iniciar a configuração do Gestor de Configuração no servidor do site utilizando um dos seguintes métodos:

    - No menu **Iniciar,** selecione Configuração do Gestor de **Configuração**.

    - No diretório para os meios de `\SMSSETUP\BIN\X64\setup.exe`instalação do Gestor de *Configuração,* aberto. Certifique-se de que esta versão é a mesma que a versão do site.

    - No diretório onde o Gestor de `\BIN\X64\setup.exe`Configuração está *instalado,* aberto.

1. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este Site**.

1. Na página de Manutenção do **Site,** selecione Modificar a configuração do **idioma**.

1. Na página **Pré-Requisitos,** selecione uma das seguintes opções:

    - **Descarregue os ficheiros necessários**: Adquira atualizações para pacotes de idiomas.

    - **Utilize ficheiros previamente descarregados**: Utilize ficheiros previamente descarregados que incluam as embalagens de idiomas que pretende adicionar ao site.

1. Na página de Seleção de Idiomas do **Servidor,** selecione os idiomas do servidor que este site suporta.

1. Na página de Seleção de **Idiomas do Cliente,** selecione os idiomas do cliente que este site suporta.

1. Complete o assistente para modificar o suporte linguístico no site.

    > [!NOTE]
    > O Gestor de Configuração inicia um reset do site que também reinstala todas as funções do sistema do site no site.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>Modificar o limiar de alerta do servidor de base de dados

Por padrão, o Gestor de Configuração gera alertas quando o espaço de disco gratuito num servidor de base de dados do site é baixo:

- Gere um aviso quando há 10 GB ou menos de espaço em disco livre
- Gere um alerta crítico quando há 5 GB ou menos de espaço em disco livre

Pode modificar estes valores ou desativar alertas para cada site:

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**

1. Selecione o site que pretende configurar. Na fita, selecione **Propriedades**.

1. Mude para o separador **Alerta** e, em seguida, edite as definições.

## <a name="uninstall-sites-and-hierarchies"></a>Desinstalar sites e hierarquias

Poderá ser necessário desinstalar uma função, site ou hierarquia do sistema do Site do Gestor de Configuração. Para mais informações, consulte [Desinstalar funções, sites e hierarquias.](../deploy/install/uninstall-sites-and-hierarchies.md)

A partir da versão 2002, também pode remover o CAS de uma hierarquia, mas manter o local principal. Para mais informações, consulte [Remova o CAS](../deploy/install/remove-central-administration-site.md).
