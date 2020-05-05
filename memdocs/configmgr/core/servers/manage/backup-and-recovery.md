---
title: Sites de backup
titleSuffix: Configuration Manager
description: Aprenda a fazer o backup dos seus sites antes do caso de falha ou perda de dados no Gestor de Configuração.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 824eaeb939249e1bcc2ed21d5815a0a72dc54797
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717868"
---
# <a name="back-up-a-configuration-manager-site"></a>Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Prepare abordagens de backup e recuperação para evitar a perda de dados. Para sites de Gestor de Configuração, uma abordagem de backup e recuperação pode ajudá-lo a recuperar sites e hierarquias mais rapidamente, e com a menor perda de dados.  

As secções deste artigo podem ajudá-lo a fazer o back-up dos seus sites. Para recuperar um site, consulte [Recovery for Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> Os dois métodos de backup suportados para a recuperação do site do Gestor de Configuração são:
>
> - Uma cópia de segurança bem sucedida da tarefa de manutenção do Servidor do Servidor do **Site de Backup**
> - Uma cópia de segurança da base de dados do site recuperada manualmente


## <a name="considerations-before-creating-a-backup"></a>Considerações antes de criar um backup  

-   Se utilizar um grupo de disponibilidade do SQL Server Always On para alojar a base de dados do site: Modifique os seus planos de backup e recuperação conforme descrito no [Prepare-se para utilizar o Servidor SQL Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   O Gestor de Configuração pode recuperar a base de dados do site a partir da tarefa de backup do Gestor de Configuração. Também pode utilizar uma cópia de segurança da base de dados do site que cria com outro processo.   

     Por exemplo, pode restaurar a base de dados do site a partir de uma cópia de segurança que é criada como parte de um plano de manutenção do Microsoft SQL Server. Também pode utilizar uma cópia de segurança criada utilizando o Gestor de Proteção de Dados para fazer backup na base de dados do site.  

-   Começando com a versão 1806, instale um servidor de site adicional em modo *passivo.* O servidor do site em modo passivo é além do servidor do site existente no modo *ativo.* Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Para mais informações, consulte a elevada disponibilidade do [servidor do Site](../deploy/configure/site-server-high-availability.md). Embora esta função não remova a necessidade de planear e praticar operações de backup e recuperação, reduz significativamente o esforço para recuperar um site quando necessário.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site
Pode utilizar o System Center Data Protection Manager (DPM) para fazer o backup na base de dados do site do Gestor de Configuração.

Crie um novo grupo de proteção em DPM para o computador de base de dados do site. Na página **Select Group Members** do Create New Protection Group Wizard, selecione o serviço SMS Writer da lista de fontes de dados. Em seguida, selecione a base de dados do site como um membro apropriado. Para mais informações sobre a utilização do DPM, consulte a biblioteca de documentação [do Gestor de Proteção](https://docs.microsoft.com/system-center/dpm) de Dados.  

> [!IMPORTANT]  
>  O Gestor de Configuração não suporta a cópia de segurança do DPM para um cluster sQL Server que utiliza uma instância nomeada. Suporta a cópia de segurança DPM num cluster do Servidor SQL que utiliza a instância padrão do Servidor SQL.  

Depois de restaurar a base de dados do site, siga os passos na configuração para recuperar o site. Para utilizar a base de dados do site que fez o backback com o Data Protection Manager, selecione a opção de recuperação para utilizar uma base de dados do **site que tenha sido recuperada manualmente**.  



## <a name="backup-maintenance-task"></a>Tarefa de manutenção de cópias de segurança
Pode automatizar a cópia de segurança para os sites do Gestor de Configuração, agendando a tarefa de manutenção predefinida do Servidor do Servidor do Site de Backup. Esta tarefa tem as seguintes funcionalidades:

-   É executada de acordo com um agendamento
-   Faz uma cópia de segurança da base de dados do site
-   Faz uma cópia de segurança de chaves de registo específicas
-   Faz uma cópia de segurança de pastas e ficheiros específicos
-   Apoia o [CD. Última pasta](the-cd.latest-folder.md)   

Planeie executar a tarefa de backup do site predefinido no mínimo de cinco em cinco dias. Este horário é porque o Gestor de Configuração utiliza um período de retenção de rastreamento de alterações do *Servidor SQL* de cinco dias. Para mais informações, consulte o período de retenção de rastreio do [SQL Server](recover-sites.md#sql-server-change-tracking-retention-period).

Para simplificar o processo de backup, pode criar um ficheiro **AfterBackup.bat.** Este script executa automaticamente ações pós-cópia seletivas após a tarefa de backup completar com sucesso. Utilize o ficheiro AfterBackup.bat para arquivar o instantâneo de reserva para um local seguro. Também pode utilizar o ficheiro AfterBackup.bat para copiar ficheiros para a sua pasta de backup ou para iniciar outras tarefas de backup.  

Pode fazer o apoio a um site da administração central e ao local principal. Sites secundários ou servidores do sistema de site não têm tarefas de backup.

Quando o serviço de backup do Gestor de Configuração funciona, segue as instruções definidas no ficheiro de controlo de cópia de segurança: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. É possível modificar o ficheiro de controlo da cópia de segurança para alterar o comportamento do serviço de cópia de segurança.  
> [!NOTE]
> As modificações de **Smsbkup.ctl** serão aplicadas após o reinício do serviço SMS_SITE_VSS_WRITER no Servidor do Site.

As informações de estado da cópia de segurança do site são escritas no ficheiro **Smsbkup.log** . Este ficheiro é criado na pasta de destino que especifica nas propriedades da tarefa de manutenção do Servidor do Servidor do Site de Backup.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para ativar a tarefa de cópia de segurança de manutenção do site  
1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2.  Selecione o site para o qual pretende ativar a tarefa de manutenção de backup do site.  

3.  Clique em **Tarefas** de Manutenção do Site na fita.  

4.  Selecione a tarefa do Servidor do Servidor do **Site de Backup** e clique em **Editar**.  

5.  Selecione a opção para **ativar esta tarefa**. Clique em **Definir Caminhos** para especificar o destino de reserva. Existem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a impedir a adulteração dos ficheiros de cópia de segurança, armazenar os ficheiros numa localização segura. O caminho de backup mais seguro é para uma unidade local, para que possa definir permissões de ficheiro NTFS na pasta. O Gestor de Configuração não encripta os dados de backup armazenados no caminho de reserva.  

    -   **Unidade local no servidor do site para dados**do site e base de dados : Especifica que a tarefa armazena os ficheiros de backup para o site e base de dados do site no caminho especificado na unidade de disco local do servidor do site. Crie a pasta local antes da tarefa de reserva ser executado. A conta do Sistema Local no servidor do site deve ter permissões de ficheiro **sinuosas** da Write NTFS para a pasta local para a cópia de segurança do servidor do site. A conta do Sistema Local no computador que está **Write** a executar o SQL Server deve ter permissões de NNTFS para a pasta para a cópia de segurança da base de dados do site.  

    -   **Trajetória de rede (nome UNC) para dados do site e base**de dados : Especifica que a tarefa armazena os ficheiros de backup para o site e base de dados do site na trajetória de rede especificada. Crie a parte antes que a tarefa de reserva corra. A conta de computador do servidor do site deve ter **Write** NTFS e partilhar permissões na pasta de rede partilhada. Se o Servidor SQL estiver instalado noutro computador, a conta de computador do Servidor SQL deve ter as mesmas permissões.  

    -   **Unidades locais no servidor do site e No Servidor SQL**: Especifica que a tarefa armazena os ficheiros de backup para o site no caminho especificado na unidade local do servidor do site. A tarefa armazena os ficheiros de backup para a base de dados do site no caminho especificado na unidade local do servidor de base de dados do site. Crie as pastas locais antes da tarefa de reserva ser executado. A conta de computador do servidor de site tem de ter permissões de **Escrita** de NTFS na pasta que criar no servidor de site. A conta de computador do SQL Server tem de ter permissões de **Escrever** de NTFS na pasta que criar no servidor de base de dados do site. Esta opção só está disponível quando a base de dados do site não estiver instalada no servidor do site.  

    > [!NOTE]  
    > A opção de navegar para o destino de backup só está disponível quando especificar o caminho de rede do destino de backup.  
    >  
    > O nome da pasta ou nome de partilha que é usado para o destino de backup não suporta o uso de caracteres Unicode.  

6.  Configure um horário para a tarefa de backup do site. Considere um horário de reserva que esteja fora do horário de trabalho ativo. Se tem uma hierarquia, considere um horário que corre pelo menos duas vezes por semana. Se o site falhar, este horário garante a máxima conservação de dados.  

    Quando executa a consola Do Gestor de Configuração no mesmo servidor de site que está a configurar para a cópia de segurança, a tarefa de backup utiliza a hora local para a programação. Quando executa a consola do Gestor de Configuração a partir de outro computador, a tarefa de backup utiliza o Tempo Universal Coordenado (UTC) para a programação.  

7.  Escolha se cria um alerta se a tarefa de backup do site falhar. Quando selecionado, o Gestor de Configuração cria um alerta crítico para a falha de cópia de segurança. Pode rever estes alertas no nó alerta **do** espaço de trabalho **monitoramento.**  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Verifique se a tarefa de manutenção do Servidor do Servidor do Site de Backup está em execução  

-   Verifique a marca de tempo nos ficheiros da pasta de destino de reserva que a tarefa criou. Verifique se o carimbo de tempo atualiza o momento em que a tarefa foi programada pela última vez.  

-   Vá ao nó do Estado do **Componente** do espaço de trabalho **de monitorização.** Reveja as mensagens de estado para **SMS_SITE_BACKUP**. Quando a cópia de segurança do site completa com sucesso, vê o ID da mensagem **5035**. Esta mensagem indica que a cópia de segurança do site foi concluída sem erros.  

-   Quando configurar a tarefa de backup para criar um alerta quando falha, procure alertas de falha de cópia de segurança no nó de **Alertas** do espaço de trabalho **monitoramento.**  

-   Abra o Windows Explorer no servidor `<ConfigMgrInstallationFolder>\Logs`do site e navegue para . Reveja **smsbkup.log** para avisos e erros. Quando a cópia de segurança do `Backup completed` site `STATMSG: ID=5035`completa com sucesso, o registo mostra com id de mensagem .  

    > [!TIP]  
    >  Quando a tarefa de manutenção de reserva falhar, reinicie a tarefa de backup parando e reiniciando o **serviço SMS_SITE_BACKUP** Windows.  



## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo de backup  
A tarefa de reserva cria uma imagem de reserva na primeira vez que corre. Pode utilizar este instantâneo para recuperar o servidor do seu site se falhar. Quando a tarefa de reserva volta a ser programada, cria-se um novo instantâneo de backup que substitui o instantâneo anterior. Como resultado, o site tem apenas uma única foto de backup, e você não tem como recuperar uma foto de backup anterior.  

Mantenha vários arquivos do instantâneo de cópia de segurança pelas seguintes razões:  

-   É comum os meios de comunicação não conseguirem, ficarem deslocados ou incluirem apenas um reforço parcial. Recuperar um site primário autónomo em falha a partir de uma cópia de segurança mais antiga é melhor do que recuperar sem qualquer cópia de segurança. Para um servidor de site numa hierarquia, a cópia de segurança deve estar no período de retenção de mudança de servidor SQL, ou a cópia de segurança não é necessária.  

-   Determinados danos no site podem não ser detetados durante vários ciclos de cópia de segurança. Talvez tenhas de usar uma fotografia de reserva antes do site ficar corrompido. Esta razão aplica-se a um site primário autónomo e a sites numa hierarquia onde a cópia de segurança está no período de retenção de localização de alterações do Servidor SQL.  

-   O site pode não ter nenhuma foto de reserva. Por exemplo, se a tarefa de manutenção do Servidor do Servidor do Site de Backup falhar. Uma vez que a tarefa de backup remove o instantâneo de cópia de segurança anterior antes de começar a fazer cópias de segurança dos dados atuais, não haverá um instantâneo de cópia de segurança válido.  



## <a name="using-the-afterbackupbat-file"></a>Utilizar o Ficheiro AfterBackup.bat  
Depois de ter conseguido fazer o backup do site, a tarefa de backup tenta executar automaticamente um script chamado **AfterBackup.bat**. Crie manualmente o ficheiro AfterBackup.bat `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`no servidor do site em . Se existir um ficheiro AfterBackup.bat na pasta correta, funciona automaticamente após a conclusão da tarefa de cópia de segurança.

O ficheiro AfterBackup.bat permite-lhe arquivar o instantâneo de cópia de segurança no final de cada operação de backup. Pode executar automaticamente outras tarefas pós-cópia de segurança que não fazem parte da tarefa de manutenção do Servidor do Servidor do Site de Backup. O ficheiro AfterBackup.bat integra o arquivo e as operações de cópia de segurança, assegurando que cada novo instantâneo de cópia de segurança é arquivado.

Se o ficheiro AfterBackup.bat não estiver presente, a tarefa de reserva ignora-o sem efeito na operação de backup. Para verificar se a tarefa de backup executou com sucesso este script, vá ao nó **do Estado do Componente** no espaço de trabalho de **Monitorização** e reveja as mensagens de estado para **SMS_SITE_BACKUP**. Quando a tarefa inicia com sucesso o ficheiro de comando AfterBackup.bat, vê a mensagem ID **5040**.  

> [!TIP]  
>  Para arquivar os ficheiros de backup do servidor do seu site com AfterBackup.bat, tem de utilizar uma ferramenta de comando de cópia no ficheiro do lote. Uma dessas ferramentas é a [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) no Windows Server. Por exemplo, crie o ficheiro AfterBackup.bat com o seguinte comando:`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Embora a utilização pretendida do AfterBackup.bat seja para arquivar imagens de backup, pode criar um ficheiro AfterBackup.bat para executar tarefas adicionais no final de cada operação de backup.  



##  <a name="supplemental-backup-tasks"></a>Tarefas suplementares de cópia de segurança  
A tarefa de manutenção do Servidor do Site de Backup fornece uma imagem de backup para os ficheiros do servidor do site e base de dados do site. Há outros itens que não devem ter em conta quando criar em conjunto a sua estratégia de backup. Utilize estas secções para o ajudar a completar a sua estratégia de backup do Gestor de Configuração.  

### <a name="back-up-custom-reports"></a>Relatórios personalizados de back-up   
Se modificar relatórios personalizados pré-definidos ou criados nos Serviços de Relato do Servidor SQL, crie uma cópia de segurança para os ficheiros de base de dados do servidor de relatórios. A cópia de segurança do servidor de relatório deve incluir os seguintes componentes:
- Os ficheiros de origem para relatórios e modelos
- Chaves de encriptação
- Conjuntos ou extensões personalizadas
- Ficheiros de configuração
- Vistas personalizadas do SQL Server usadas em relatórios personalizados
- Procedimentos armazenados sob medida  

> [!IMPORTANT]  
>  Quando o Gestor de Configuração atualiza para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, certifique-se de que faz o back-up do relatório e, em seguida, restaurá-lo nos Serviços de Informação.  

Para obter mais informações sobre o backup dos seus relatórios personalizados nos Serviços de Reportagem, consulte operações de [backup e restauro para serviços de reporte](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Back up ficheiros de conteúdo  
A biblioteca de conteúdos em 'Gestor de Configuração' é o local onde todos os ficheiros de conteúdo são armazenados para todas as implementações de software. A biblioteca de conteúdos está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção do Servidor do Servidor do Site de Backup não faz cópia de segurança da biblioteca de conteúdos ou dos ficheiros de origem de pacotes. Quando um servidor de site falha, a informação sobre a biblioteca de conteúdos é restaurada na base de dados do site, mas deve restaurar a biblioteca de conteúdos e os ficheiros de fonte de pacote.  

-   A biblioteca de conteúdos deve ser restaurada antes de poder redistribuir o conteúdo para pontos de distribuição. Quando inicia a redistribuição de conteúdos, o Gestor de Configuração copia os ficheiros da biblioteca de conteúdos do servidor do site para os pontos de distribuição. Para mais informações, consulte a biblioteca de [conteúdos.](../../plan-design/hierarchy/the-content-library.md)  

-   Os ficheiros de origem do pacote devem ser restaurados antes de poder atualizar o conteúdo nos pontos de distribuição. Quando inicia uma atualização de conteúdo, o Gestor de Configuração copia ficheiros novos ou modificados da fonte do pacote para a biblioteca de conteúdos. Em seguida, copia os ficheiros para pontos de distribuição associados. Execute a seguinte consulta do SQL Server contra a base de dados `SELECT * FROM v_Package`do site para encontrar a localização de origem do pacote para todos os pacotes e aplicações: . Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Quando restaurar os ficheiros de origem do pacote, devem ser restaurados no mesmo local onde estavam antes da falha.  

Verifique se inclui tanto a biblioteca de conteúdos como os ficheiros de fonte de pacote no seu sistema de ficheiros de reserva para o servidor do site.  

### <a name="back-up-custom-software-updates"></a>Cópia de segurança de atualizações de software personalizadas  
System Center Updates Publisher é uma ferramenta autónoma que permite gerir atualizações de software personalizadas. Updates Publisher usa uma base de dados local para o seu repositório de atualização de software. Quando utilizar o Updates Publisher para gerir atualizações de software personalizadas, determine se deve incluir a base de dados do Updates Publisher no seu plano de backup. Para mais informações, consulte [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Utilize o procedimento seguinte para fazer o backup da base de dados da Editora de Atualizações.  

#### <a name="back-up-the-updates-publisher-database"></a>Volte a ser a base de dados da Editora de Atualizações  

1.  No computador que executa atualizações Editora, navegue para a base de `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`dados Da Empresa de Atualizações Editora **scupdb.sdf** em . Há um ficheiro de base de dados diferente para cada utilizador que executa o Updates Publisher.  

2.  Copie o ficheiro de base de dados para o destino de cópia de segurança. Por exemplo, se o `E:\ConfigMgr_Backup`seu destino de backup for `E:\ConfigMgr_Backup\SCUP`, pode copiar o ficheiro de base de dados da Atualizações Publisher para .  

    > [!TIP]  
    >  Quando houver mais de um ficheiro de base de dados num computador, considere armazenar o ficheiro numa subpasta que indique o perfil do utilizador associado ao ficheiro base de dados. Por exemplo, pode ter um `E:\ConfigMgr_Backup\SCUP\User1` ficheiro de `E:\ConfigMgr_Backup\SCUP\User2`base de dados e outro ficheiro de base de dados em .  



## <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
Pode utilizar sequências de tarefas do Gestor de Configuração para capturar e restaurar os dados do estado do utilizador em cenários de implementação do SISTEMA. As propriedades do ponto de migração do Estado listam as pastas que armazenam os dados do estado do utilizador. Estes dados não são apoiados como parte da tarefa de manutenção de backup do servidor do site. Como parte do seu plano de cópia de segurança, tem de copiar manualmente as pastas que especificar para armazenar os dados de migração de estado do utilizador.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Determine as pastas utilizadas para armazenar dados de migração do estado do utilizador  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione o nó de Funções de **Servidores e Derôs.**  

2.  Selecione o sistema de site que acolhe o papel de migração do Estado. Em seguida, selecione o ponto de **migração do Estado** no painel de funções do sistema do **site.**  

3.  Clique em **Propriedades** na fita.  

4.  As pastas que armazenam os dados de migração de estado do utilizador são listadas na secção **Detalhes da pasta** , no separador **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o Serviço de Cópia de Sombra de Volume do Windows (VSS) durante o processo de backup. O serviço SMS Writer deve estar a funcionar para o site do Gestor de Configuração de volta para ser concluído com sucesso.  

### <a name="process"></a>Processo  
1. O SMS Writer é registado junto do serviço VSS, ligando-se às respetivas interfaces e eventos. 
2. Quando o VSS difunde eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação adequada. 
3. O SMS Writer lê o ficheiro de controlo de cópia `<ConfigMgrInstallationPath>\inboxes\smsbkup.box`de segurança **smsbkup.ctl** localizado em , e determina os ficheiros e dados para fazer backup. 
4. O SMS Writer constrói metadados, que consistem em vários componentes, incluindo dados específicos da chave de registo SMS e subchaves. 
    a. Envia os metadados para o VSS quando é solicitado. 
    b. O VSS envia então os metadados para a aplicação de pedido, o Gestor de Backup do Gestor de Configuração. 
5. O Gestor de Backup seleciona os dados para fazer backup e envia estes dados para o SMS Writer via VSS. 
6. O SMS Writer executa os passos adequados para preparar a cópia de segurança. 
7. Mais tarde, quando o VSS estiver pronto para tirar a fotografia: a. Envia um evento b. O SMS Writer para todos os serviços de Gestor de Configuração c. Garante que as atividades do Gestor de Configuração estão congeladas enquanto o instantâneo é criado. 
8. Após a conclusão do instantâneo, o SMS Writer reiniciará os serviços e atividades.

O serviço SMS Writer é instalado automaticamente. Tem de estar em execução quando a aplicação VSS solicita uma cópia de segurança ou restauro.  

### <a name="writer-id"></a>ID do escritor  
O writer ID para o SMS Writer é **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer tem de ser executado sob a conta do Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópia Sombra de Volumes  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de cópias de segurança de volume enquanto as aplicações do sistema continuam a escrever nos volumes. O VSS fornece uma interface consistente que permite coordenar as aplicações de utilizador que atualizam dados no disco (o serviço SMS Writer) com as que efetuam cópias de segurança das aplicações (o serviço Backup Manager). Para mais informações, consulte o Serviço de Cópia de [Sombra de Volume](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Passos seguintes
Depois de criar um backup, pratique a [recuperação](recover-sites.md) do site com esse backup. Esta prática pode ajudá-lo a familiarizar-se com o processo de recuperação antes de ter de confiar nele. Também pode ajudar a confirmar que o backup foi bem sucedido para o seu propósito.  
