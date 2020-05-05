---
title: Recuperação do local
titleSuffix: Configuration Manager
description: Aprenda a recuperar os seus sites no Gestor de Configuração.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14f319cfa1d09cf21cc5da5ed4a9fde9b9b9799b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723867"
---
# <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Executar uma recuperação do site do Gestor de Configuração depois de um site falhar ou a perda de dados ocorrer na base de dados do site. Reparar e ressincronizar dados são as tarefas principais de uma recuperação de site e são necessárias para evitar a interrupção das operações.

As secções deste artigo podem ajudá-lo a recuperar um site do Gestor de Configuração. Para criar uma cópia de segurança, consulte backup para 'Gestor de [Configuração'.](backup-and-recovery.md)

## <a name="considerations-before-recovering-a-site"></a>Considerações antes de recuperar um site

> [!Important]  
> Esta informação aplica-se apenas aos cenários de recuperação do site. Quando estiver a atualizar a sua infraestrutura no local e não recuperar ativamente um site falhado, reveja a informação nos seguintes artigos:
>
> - [Atualizar infraestrutura no local](upgrade-on-premises-infrastructure.md)
> - [Modificar a infraestrutura](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Preparar o hardware do servidor

<!-- 2841893 -->

Certifique-se de que as configurações existentes não estão presentes no servidor do site. Quaisquer configurações anteriores podem causar conflitos durante o processo de recuperação do site. Utilize uma das seguintes opções para o hardware do servidor:

- Utilize um novo servidor que satisfaça os requisitos gerais e de recuperação.

- Forforte os discos e reinstale o SISTEMA no servidor existente. Certifique-se de que satisfaz os requisitos gerais e de recuperação.

- Reutilizar um servidor existente que limpou

Utilize um dos seguintes procedimentos para limpar um servidor existente:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Limpe um servidor existente apenas para a recuperação do servidor do site

1. Eliminar as teclas de registo SMS:`HKLM\Software\Microsoft\SMS`
2. Eliminar quaisquer entradas de `SMS` `HKLM\System\CurrentControlSet\Services`registo a partir de . Por exemplo:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Desinstalar a consola do Gestor de Configuração
4. Reiniciar o servidor
5. Confirme que todas as chaves de registo acima referidas são eliminadas.

O servidor está agora pronto para o procedimento de restauro do Gestor de Configuração.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Limpe um servidor existente apenas para recuperação da base de dados do site

1. Volte para a base de dados do site. Também apoie quaisquer outras bases de dados de suporte, como a WSUS.
2. Certifique-se de notar o nome do servidor SQL e o nome da instância
3. Excluir manualmente a base de dados do site do Servidor SQL
4. Reiniciar o Servidor SQL

O servidor está agora pronto para o procedimento de restauro do Gestor de Configuração.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Limpe um servidor existente para a recuperação total

1. Volte para a base de dados do site. Também apoie quaisquer outras bases de dados de suporte, como a WSUS.
2. Faça uma cópia da biblioteca de conteúdos
3. Excluir manualmente a base de dados do site do Servidor SQL
4. Desinstalar o site do Gestor de Configuração
5. Elimine manualmente a pasta de instalação do Gestor de Configuração e quaisquer outras pastas do Gestor de Configuração
6. Reiniciar o servidor
7. Restaurar a biblioteca de conteúdos e outras bases de dados como o WSUS

O servidor está agora pronto para o procedimento de restauro do Gestor de Configuração.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Use uma versão suportada e mesma edição do SQL Server

<!-- SCCMDocs#751 -->

Se possível, utilize a mesma versão do Servidor SQL. No entanto, é suportado para restaurar uma base de dados para uma versão mais recente.

Não mude a edição do SQL Server. Restaurar uma base de dados do site da edição Standard para a edição enterprise não é suportado.

Requisitos adicionais de configuração do Servidor SQL:

- O Servidor SQL não pode ser definido para o **modo de utilizador único**.
- Certifique-se de que os ficheiros MDF e LDF são válidos. Quando se recupera um site, não há verificação do estado dos ficheiros.  

### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidade Always On do SQL Server

Se utilizar o Servidor SQL Always On grupos de disponibilidade para alojar a base de dados do site, modifique os seus planos de recuperação conforme descrito no [Prepare-se para utilizar o Servidor SQL Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Réplicas de bases de dados

Depois de restaurar uma base de dados do site que configurapara réplicas de bases de dados, reconfigure cada réplica. Antes de poder utilizar as réplicas da base de dados, recrie as publicações e as subscrições.

## <a name="determine-your-recovery-options"></a>Determinar as opções de recuperação

Existem duas áreas principais a considerar para o servidor do site primário do Gestor de Configuração e recuperação do site central de administração (CAS): o servidor do **site** e a base de dados do **site**.
As seguintes secções podem ajudá-lo a selecionar as melhores opções para o seu cenário de recuperação.

> [!NOTE]  
> Quando a configuração do Gestor de Configuração deteta um site existente no servidor, pode iniciar uma recuperação do site, mas as opções de recuperação para o servidor do site são limitadas. Por exemplo, se executar o Programa de Configuração num servidor de site existente, quando escolher a recuperação, poderá recuperar o servidor de base de dados do site, mas a opção de recuperação do servidor de site é desativada.

### <a name="site-server-recovery-options"></a>Opções de recuperação do servidor do site

Iniciar a configuração do Gestor de Configuração a partir de uma cópia do **CD. Última** pasta que criou fora da pasta de instalação do Gestor de Configuração.  

- Se executar a configuração a partir do menu **Iniciar** no servidor do site, a opção **Recuperar uma opção** de site não está disponível.  

- Se instalou alguma atualização a partir da consola 'Gestor de Configuração' antes de fazer a sua cópia de segurança, não poderá reinstalar o site utilizando a configuração a partir dos seguintes locais:

  - Meios de instalação
  - O caminho de instalação do Gestor de Configuração

Em seguida, selecione a opção **recuperar uma opção** de site. Tem as seguintes opções de recuperação para o servidor de site falhado:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Recuperar o servidor do site usando uma cópia de segurança existente

Utilize esta opção quando tiver uma cópia de segurança do 'Gestor de Configuração' do servidor do site antes da falha do site. O site cria esta cópia de segurança como parte da tarefa de manutenção do Servidor do Servidor do **Site de Backup.** O site é reinstalado e as definições do site são configuradas com base no site que foi apoiado.  

#### <a name="reinstall-the-site-server"></a>Reinstalar o servidor do site

Utilize esta opção quando não tiver uma cópia de segurança do servidor do site. O servidor do site é reinstalado e deve especificar as definições do site como faria durante uma instalação inicial.  

- Utilize o mesmo código de site e o nome da base de dados do site que utilizou quando o site falhado foi instalado pela primeira vez.  

- Pode reinstalar o site num novo computador que executa uma nova versão S.  

- O servidor deve utilizar o mesmo nome de anfitrião e o nome de domínio totalmente qualificado (FQDN) do servidor original do site.

### <a name="site-database-recovery-options"></a>Opções de recuperação da base de dados do site

Ao executar a configuração do Gestor de Configuração, tem as seguintes opções de recuperação para a base de dados do site:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Recuperar a base de dados do site usando um conjunto de backup

Utilize esta opção quando tiver uma cópia de segurança do Gestor de Configuração da base de dados do site antes da falha na base de dados. O site cria esta cópia de segurança como parte da tarefa de manutenção do Servidor do Servidor do **Site de Backup.** Numa hierarquia, ao restaurar um local primário, o processo de recuperação recupera do CAS quaisquer alterações feitas na base de dados do site após a última cópia de segurança. Ao restaurar o CAS, o processo de recuperação recupera estas alterações a partir de um local primário de referência. Quando recupera a base de dados do site para um site primário autónomo, perde alterações no site após a última cópia de segurança.  

Quando se recupera a base de dados do site para um site numa hierarquia, o comportamento de recuperação é diferente para um CAS e um site primário. O comportamento também é diferente quando a última cópia de segurança está dentro ou fora do período de retenção de localização de alterações do Servidor SQL. Para mais informações, consulte a secção de cenários de [recuperação](#site-database-recovery-scenarios) da base de dados do Site neste artigo.  

> [!NOTE]  
> Se selecionar restaurar a base de dados do site utilizando um conjunto de cópias de segurança, mas a base de dados do site já existe, a recuperação falha.  

#### <a name="create-a-new-database-for-this-site"></a>Criar uma nova base de dados para este site

Utilize esta opção quando não tiver uma cópia de segurança da base de dados do site. Numa hierarquia, o processo de recuperação cria uma nova base de dados do site. Ao restaurar um local primário infantil, recupera os dados replicando-se do CAS. Ao restaurar o CAS, replica dados de um site primário de referência. Esta opção não está disponível quando se está a recuperar um local primário autónomo ou um CAS que não tem sites primários.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Utilize uma base de dados do site que tenha sido recuperada manualmente

Utilize esta opção quando já recuperou a base de dados do site do Gestor de Configuração, mas precisa de concluir o processo de recuperação.  

- O Gestor de Configuração pode recuperar a base de dados do site de qualquer um dos seguintes processos:  

  - A tarefa de manutenção de backup do Gestor de Configuração  
  - Uma cópia de segurança da base de dados do site utilizando o Gestor de Proteção de Dados (DPM)  
  - Outro processo de backup  

    Depois de restaurar a base de dados do site utilizando um método fora do 'Configuração Manager', executar configuração e selecionar esta opção para completar a recuperação da base de dados do site.  

    > [!NOTE]  
    > Quando utilizar o DPM para fazer o backup da base de dados do site, utilize os procedimentos dPM para restaurar a base de dados do site para um local especificado antes de continuar o processo de restauro no Gestor de Configuração. Para mais informações sobre o DPM, consulte a biblioteca de documentação [do Gestor de Proteção](https://docs.microsoft.com/system-center/dpm) de Dados.  

- Numa hierarquia, quando se recupera uma base de dados primária do site, o processo de recuperação recupera do CAS quaisquer alterações feitas na base de dados do site após a última cópia de segurança. Ao restaurar o CAS, o processo de recuperação recupera estas alterações a partir de um local primário de referência. Quando recupera a base de dados do site para um site primário autónomo, perde alterações no site após a última cópia de segurança.  

#### <a name="skip-database-recovery"></a>Saltar recuperação da base de dados

Utilize esta opção quando não ocorrer nenhuma perda de dados no servidor de base de dados do Site Do Gestor de Configuração. Esta opção só é válida quando a base de dados do site está num computador diferente do servidor do site que está a recuperar.  

### <a name="sql-server-change-tracking-retention-period"></a>Período de retenção do registo de alterações do SQL Server

O Gestor de Configuração permite o rastreio de alterações para a base de dados do site no Servidor SQL. Alterar o rastreio permite que o Gestor de Configuração se questione para obter informações sobre as alterações feitas nas tabelas de bases de dados após um ponto de tempo anterior. O período de retenção especifica a duração da utilização das informações de rastreio de alterações. Por predefinição, a base de dados do site está configurada para ter um período de retenção de cinco dias. Quando recupera a base de dados de um site, o processo de recuperação procede de forma diferente se a sua cópia de segurança estiver dentro ou fora do período de retenção. Por exemplo, se o seu servidor SQL falhar, e a sua última cópia de segurança tiver sete dias, está fora do período de retenção.

Para obter mais informações sobre os internos de rastreio de alterações do SQL Server, consulte as seguintes publicações de blog da equipa do SQL Server: [Change Tracking Cleanup - parte 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) e Change Tracking [Cleanup - parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialização do site ou dados globais

O processo para reinicializar um site ou dados globais substitui dados existentes na base de dados do site por dados da base de dados de outro site. Por exemplo, quando o site ABC reinicializa dados do site XYZ, ocorrem os seguintes passos:

- Os dados são copiados do site XYZ para o site ABC.
- Os dados existentes do site XYZ são removidos da base de dados do site no site ABC.
- Os dados copiados do site XYZ são inseridos na base de dados do site ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Exemplo cenário 1: O site primário reininicia os dados globais do CAS

O processo de recuperação remove os dados globais existentes para o local primário na base de dados do site primário e substitui os dados pelos dados globais copiados do CAS.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Exemplo cenário 2: O CAS reininicia os dados do site a partir de um site primário

O processo de recuperação remove os dados do site existentes para esse local primário na base de dados cas. Substitui os dados com os dados do site copiados do local principal. Os dados do site de outros locais primários não são afetados.

### <a name="site-database-recovery-scenarios"></a>Cenários de recuperação de bases de dados de site

Depois de uma base de dados do site ser restaurada a partir de uma cópia de segurança, o Gestor de Configuração tenta restaurar as alterações no site e dados globais após a última cópia de segurança da base de dados. O Gestor de Configuração inicia as seguintes ações depois de uma base de dados do site ser restaurada a partir de cópia de segurança:  

#### <a name="recovered-site-is-a-cas"></a>O local recuperado é um CAS

- Cópia de segurança da base de dados dentro do período de retenção do registo de alterações  

  - **Dados globais**: As alterações nos dados globais após a cópia de segurança são replicadas em todos os sites primários.  

  - **Dados**do site : As alterações nos dados do site após a cópia de segurança são replicadas em todos os sites primários.  

- Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações  

  - **Dados globais**: O CAS reininicia os dados globais do site primário de referência se os especificar. Em seguida, todos os outros sites primários reinicializam os dados globais do CAS. Se não especificar um site de referência, todos os sites primários reincionam os dados globais do CAS. Estes dados são o que restaurou a partir de backup.  

  - **Dados**do site : O CAS reinicializa os dados do site de cada local primário.  

#### <a name="recovered-site-is-a-primary-site"></a>O local recuperado é um local primário

- Cópia de segurança da base de dados dentro do período de retenção do registo de alterações  

  - **Dados globais**: As alterações nos dados globais após a cópia de segurança são replicadas a partir do CAS.  

  - **Dados**do site : O CAS reininicia os dados do site a partir do local principal. Mudanças após a perda do reforço. Os clientes regeneram a maioria dos dados quando enviam informações para o site principal.  

- Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações  

  - **Dados globais**: O site primário reininicia os dados globais do CAS.  

  - **Dados**do site : O CAS reininicia os dados do site a partir do local principal. Mudanças após a perda do reforço. Os clientes regeneram a maioria dos dados quando enviam informações para o site principal.  

## <a name="site-recovery-procedures"></a>Procedimentos de recuperação de sites

Utilize um dos seguintes procedimentos para o ajudar a recuperar o servidor do site e a base de dados do site:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Inicie uma recuperação do site no assistente de configuração

1. Copie o [CD. Última pasta](the-cd.latest-folder.md) para um local fora da pasta de instalação do Gestor de Configuração. Da cópia do CD. Última pasta, execute o assistente de configuração do Gestor de Configuração.  

2. Na página **Getting Started,** selecione **Recuperar um site**, e, em seguida, selecione **Next**.  

3. Conclua o assistente utilizando as opções adequadas para a recuperação do seu site.  

     - Durante a recuperação, a configuração identifica a porta SQL Server Broker (SSB) utilizada pelo Servidor SQL. Não altere esta definição de porta durante a recuperação ou a replicação de dados não funcionará corretamente após a recuperação.  

     - Pode especificar o original ou um novo caminho a utilizar para a instalação do Gestor de Configuração no assistente de configuração.  

### <a name="start-an-unattended-site-recovery"></a>Iniciar uma recuperação do site sem supervisão

1. Prepare o script de instalação automática para as opções de que necessita para a recuperação do site. Para mais informações, consulte a [recuperação do site sem supervisão.](unattended-recovery.md)  

2. Executar Configuração do Gestor `/script` de Configuração utilizando a opção linha de comando. Por exemplo, cria um ficheiro de inicialização de configuração **ConfigMgrUnattend.ini**. Guarde-o `C:\Temp` no diretório do computador em que está a executar a configuração. Utilize o seguinte comando:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Depois de recuperar um CAS, a replicação de alguns dados do site de sites infantis pode não ser estabelecida. Estes dados podem incluir inventário de hardware, inventário de software e mensagens de estado.
>
> Se este problema ocorrer, reinicialize a **Fila de Sítios ConfigMgrDRDrS** para a replicação da base de dados. Utilize o **Gestor de Servidores SQL** para executar a seguinte consulta na base de dados do site para o CAS:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Tarefas de pós-recuperação

Depois de recuperar o seu site, existem várias tarefas pós-recuperação a considerar antes da recuperação do site estar completa. Utilize as secções seguintes para concluir o processo de recuperação do site.

### <a name="reenter-user-account-passwords"></a>Reintroduzir as palavras-passe da conta de utilizador

Após a recuperação do servidor do site, reintroduza as palavras-passe para quaisquer contas de utilizador no site. Estas palavras-passe são redefinidas durante a recuperação do site. As contas estão listadas na página **final** do assistente de configuração após a recuperação do site ser concluída. A lista também `C:\ConfigMgrPostRecoveryActions.html` é guardada no servidor do site recuperado.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Reintroduza as palavras-passe da conta do utilizador após a recuperação do site

1. Abra a consola do Gestor de Configuração e ligue-se ao site recuperado.  

2. Vá ao espaço de trabalho da **Administração,** expanda **a Segurança,** e depois selecione **Contas**.  

3. Para cada conta, faça os seguintes passos para reintroduzir a palavra-passe:  

     1. Selecione a conta da lista identificada após a recuperação do local.  

     2. Selecione **Propriedades** na fita.  

     3. No separador **Geral,** selecione **set**, e, em seguida, reintroduza a palavra-passe para a conta.  

     4. Selecione **Verificar,** escolha a fonte de dados apropriada para a conta de utilizador selecionada e, em seguida, selecione a **ligação de teste**. Este passo testa que a conta de utilizador pode ligar-se à fonte de dados e verifica as credenciais.  

     5. Selecione **OK** para guardar as alterações da palavra-passe e, em seguida, selecione **OK** para fechar a página de propriedades da conta.  

#### <a name="reenter-pxe-passwords"></a>Reenter PXE palavras-passe

<!-- SCCMDocs#1683 -->

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.** Qualquer ponto de distribuição no local com **Sim** na coluna **PXE** está ativado para PXE e pode ter uma senha para reentrar.

1. Selecione um ponto de distribuição ativado por PXE e selecione **Propriedades** na fita.

1. Mude para o separador **PXE.**

1. Se a opção **de exigir uma palavra-passe quando os computadores utilizarem o PXE** estiver ativada, introduza e confirme a palavra-passe.

1. Selecione **OK** para guardar e fechar as propriedades.

Repita este processo para qualquer outro ponto de distribuição no local ativado por PXE.

#### <a name="reenter-task-sequence-passwords"></a>Reintroduzir palavras-passe da sequência de tarefas

<!-- SCCMDocs#1683 -->

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**

1. Selecione uma sequência de tarefas e, em seguida, na fita, **selecione Editar**.

1. Reveja os seguintes passos para que as palavras-passe voltem a entrar:

    - **Aplicar As Definições do Windows**: Se ativar e especificar a palavra-passe do administrador local, volte a inserir e confirme a palavra-passe.

    - **Aplicar Definições**de rede : Para a conta que tem permissão para aderir ao domínio, selecione **Definir**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

    - **Capturar Imagem do sistema operativo**: Para a conta utilizada para aceder ao destino, selecione **set**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

    - **Ligue à pasta da rede**: Para a conta utilizada para ligar uma pasta de rede, selecione **set**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

    - **Ativar o BitLocker**: Se utilizar a opção de gestão da chave **TPM e PIN,** reintroduza o PIN.

    - **Junte-se ao Domain ou ao Grupo de Trabalho**: Para a conta que tem permissão para aderir ao domínio, selecione **set**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

    - **Executar linha**de comando : Se utilizar a opção de **executar este passo como a seguinte conta,** selecione **set**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

    - **Executar o Script PowerShell**: Se utilizar a opção de **executar este passo como a seguinte conta,** selecione **set**. Introduza e confirme a palavra-passe e, em seguida, selecione **Verificar**.

Repita este processo para todas as sequências de tarefas.

### <a name="reenter-sideloading-keys"></a>Reenter teclas de sideloading

Após a recuperação do servidor do site, reintroduza as teclas de sideloading do Windows especificadas para o site. Estas chaves são redefinidas durante a recuperação do local. Depois de reentrar nas teclas de carga lateral, o site repõe a contagem na coluna **Ativações utilizada** para teclas de sideloading Windows.

Por exemplo, antes da falha do local, a contagem total de **ativações** mostra como **100**. O número de teclas que os dispositivos utilizaram, ou **as ativações utilizadas,** é **de 90**. Após a recuperação do local, o valor total de **ativações** ainda apresenta **100**, mas as **Ativações utilizadas** incorretamente **exibem 0**. Depois de 10 novos dispositivos utilizarem uma tecla de carga lateral, não existem mais teclas de carga lateral, e o 11º dispositivo não aplica uma tecla de carga lateral.

### <a name="recreate-azure-services"></a>Recriar serviços Azure

<!-- SCCMDocs#1022 -->

Na versão 1806 do Gestor de Configuração, após a recuperação do site, verá o seguinte erro no cloudmgr.log:

`Index (zero-based) must be greater than or equal to zero`

Para resolver isto, [renovar a chave secreta](../deploy/configure/azure-services-wizard.md#bkmk_renew) para cada ligação ao inquilino Azure.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de sites que utilizam IIS

Quando recuperar os sistemas do site que executam o IIS e configurar para HTTPS, reconfigure o IIS para utilizar o certificado do servidor web.

### <a name="reinstall-hotfixes"></a>Reinstalar os hotfixes

Após uma recuperação do site, deve reinstalar quaisquer [hotfixes fora da banda](updates.md#bkmk_outofband) que tenham sido aplicados ao servidor do site. Após a recuperação do site, consulte a lista dos hotfixos previamente instalados na página **Final** do assistente de configuração. Esta lista também `C:\ConfigMgrPostRecoveryActions.html` é guardada no servidor do site recuperado.

### <a name="recover-custom-reports"></a>Recuperar relatórios personalizados

Alguns clientes criam relatórios personalizados nos Serviços de Reporte de Servidores SQL. Quando este componente falhar, recupere os relatórios de uma cópia de segurança do servidor de relatório. Para obter mais informações sobre a restauração dos seus relatórios personalizados nos Serviços de Reportagem, consulte operações de [backup e restauro para serviços de reporte](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Recuperar ficheiros de conteúdo

A base de dados do site rastreia onde o servidor do site armazena os ficheiros de conteúdo. Os ficheiros de conteúdo em si não são apoiados ou restaurados como parte do processo de backup e recuperação. Para recuperar totalmente os ficheiros de conteúdo, restaure a biblioteca de conteúdos e os ficheiros de origem do pacote para a localização original. Existem vários métodos para recuperar os seus ficheiros de conteúdo. O método mais fácil é restaurar os ficheiros a partir de uma cópia de segurança do sistema de ficheiros do servidor do site.

Se não tiver uma cópia de segurança do sistema de ficheiros para os ficheiros de origem do pacote, copie-os manualmente ou descarregue-os. Este processo é semelhante ao de quando criou originalmente o pacote. Execute a seguinte consulta no SQL Server para encontrar a localização `SELECT * FROM v_Package`de origem do pacote para todos os pacotes e aplicações: . Identifique o site de origem do pacote olhando para os três primeiros caracteres do ID do pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.

Se não tiver uma cópia de segurança do sistema de ficheiros que inclua a biblioteca de conteúdos, tem as seguintes opções de restauro:  

- Importar um ficheiro de **conteúdo pré-encenado**: Numa hierarquia do Gestor de Configuração, pode criar um ficheiro de conteúdo pré-encenado com todos os pacotes e aplicações de outro local. Em seguida, importe o ficheiro de conteúdo pré-encenado para recuperar a biblioteca de conteúdos no servidor do site.  

- **Conteúdo de atualização**: O Gestor de Configuração copia o conteúdo da fonte do pacote para a biblioteca de conteúdos. Para que esta ação termine com sucesso, os ficheiros de origem do pacote devem estar disponíveis no local original. Faça esta ação em cada pacote e aplicação.

### <a name="recover-custom-software-updates"></a>Recuperar atualizações de software personalizadas

Quando tiver incluído ficheiros de base de dados do System Center Updates Publisher no seu plano de backup, pode recuperar as bases de dados se o computador Updates Publisher falhar. Para mais informações sobre updates Publisher, consulte [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Restaurar a base de dados da Editora de Atualizações

1. Reinstalar atualizações Editor no computador recuperado.  

2. Copie o ficheiro de base de dados `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` **Scupdb.sdf** do seu destino de reserva para o computador que executa o Editor de Atualizações.  

3. Quando mais de um utilizador executa atualizações Do Publisher no computador, copie cada ficheiro de base de dados para a localização do perfil de utilizador apropriado.  

### <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador

Como parte das propriedades do ponto de migração do Estado, especifica as pastas que armazenam os dados do estado do utilizador. Depois de recuperar um ponto de migração estatal, restaure manualmente os dados do estado do utilizador no servidor. Restaurá-lo nas mesmas pastas que armazenaram os dados antes da falha.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição

Depois de restaurar um site, o **distmgr.log** pode listar `Failed to decrypt cert PFX data`a seguinte entrada para um ou mais pontos de distribuição: . Esta entrada indica que os dados do certificado de ponto de distribuição não podem ser desencriptados pelo site. Para resolver esta questão, regenerar ou reimportar o certificado para os pontos de distribuição afetados. Utilize o cmdlet [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar certificados utilizados para pontos de distribuição baseados na nuvem

O Gestor de Configuração requer um certificado de gestão Azure para o servidor do site comunicar com pontos de distribuição baseados na nuvem. Após a recuperação do site, atualize os certificados para pontos de distribuição baseados na nuvem.

## <a name="recover-a-secondary-site"></a>Recuperar um site secundário

O Gestor de Configuração não suporta a cópia de segurança da base de dados num local secundário, mas suporta a recuperação reinstalando o site secundário. A recuperação do site secundário é necessária quando um site secundário do Gestor de Configuração falha.

### <a name="requirements"></a>Requisitos

- O servidor deve cumprir todos os pré-requisitos do site secundário e ter os direitos de segurança adequados configurados.  

- Utilize o mesmo caminho de instalação que foi utilizado para o local falhado.  

- Utilize um servidor com a mesma configuração que o servidor falhado. Esta configuração inclui o seu nome de domínio totalmente qualificado (FQDN).  

- O servidor deve ter a mesma configuração do Servidor SQL que o site falhado.  

  - Durante uma recuperação secundária do site, o Gestor de Configuração não instala o SQL Server Express se ainda não estiver instalado no computador.  

  - Utilize a mesma versão do SQL Server e a mesma instância do Servidor SQL que utilizou para a base de dados do site secundário antes da falha.  

### <a name="procedure"></a>Procedimento

Utilize a ação do **Site Secundário de Recuperação** a partir do nó **de Sites** na consola 'Gestor de Configuração'. Ao contrário de outros tipos de sites, a recuperação para um site secundário não usa um ficheiro de backup. Este processo reinstala os ficheiros do site secundário no servidor falhado. Após a reinstalação do site, os dados do site secundário são reinicializados a partir do local primário dos pais.

Durante o processo de recuperação, o Gestor de Configuração verifica se a biblioteca de conteúdos existe no servidor do site secundário. Verifica igualmente que o conteúdo adequado está disponível. O site secundário utiliza a biblioteca de conteúdos existente, se incluir o conteúdo apropriado. Caso contrário, para recuperar a biblioteca de conteúdos de um site secundário, redistribuir ou pré-encenar o conteúdo para o servidor.

Quando se tem um ponto de distribuição que não esteja no servidor do site secundário, não é necessário reinstalar o ponto de distribuição durante uma recuperação do site secundário. Após a recuperação do site secundário, o site sincroniza automaticamente com o ponto de distribuição.

Pode verificar o estado da recuperação do local secundário utilizando a ação **'Instalação de Posição'** a partir do nó de **Sites** na consola 'Gestor de Configuração'.
