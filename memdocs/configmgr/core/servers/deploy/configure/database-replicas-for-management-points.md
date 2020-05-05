---
title: Réplicas de bases de dados de pontos de gestão
titleSuffix: Configuration Manager
description: Utilize uma réplica de base de dados para reduzir a carga do CPU colocada no servidor de base de dados do site por pontos de gestão.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8d413221f7dc4ea905844ad3b2dbe08826314a54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720990"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Réplicas de base de dados para pontos de gestão para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os sites primários do Gestor de Configuração podem usar uma réplica de base de dados para reduzir a carga de CPU colocada no servidor de base de dados do site por pontos de gestão, uma vez que eles serviços pedidos de clientes.  

-   Quando um ponto de gestão utiliza uma réplica de base de dados, esse ponto de gestão solicita dados ao computador com o SQL Server que aloja a réplica da base de dados em vez de solicitar ao servidor da base de dados do site.  

-   Isto pode ajudar a reduzir os requisitos de processamento da CPU no servidor da base de dados do site ao descarregar tarefas de processamento frequentes relacionadas com clientes.  Um exemplo de tarefas de processamento frequentes para clientes inclui sites onde existe um grande número de clientes que efetuam pedidos frequentes de política de cliente  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Preparar a utilização de réplicas de bases de dados  
**Acerca das réplicas de bases de dados para pontos de gestão:**  

-   Réplicas são uma cópia parcial da base de dados do site que é replicada para uma instância separada do SQL Server:  

    -   Os sites primários suportam uma réplica de base de dados dedicada para cada ponto de gestão no site (os sites secundários não suportam réplicas de bases de dados)  

    -   Uma réplica de base de dados única pode ser utilizada por mais de um ponto de gestão do mesmo site  

    -   Um SQL Server pode alojar várias réplicas de base de dados para utilização por pontos de gestão diferentes, desde que cada uma seja executada numa instância separada do SQL Server  

-   As réplicas sincronizam uma cópia da base de dados do site numa agenda fixa a partir dos dados publicados pelo servidor da base de dados do site para este fim.  

-   Os pontos de gestão podem ser configurados para utilizar uma réplica quando o utilizador instala o ponto de gestão ou numa altura posterior ao reconfigurar o ponto de gestão anteriormente instalado para utilizar a réplica da base de dados  

-   Monitorize regularmente o servidor da base de dados do site e todos os servidores de réplicas da base de dados para garantir que a replicação ocorre entre eles e que o desempenho do servidor de réplicas da base de dados é suficiente para o desempenho pretendido para o site e cliente  

**Pré-requisitos para réplicas de base de dados:**  

-   **Requisitos do Servidor SQL:**  

    -   O SQL Server que aloja a réplica da base de dados tem de preencher os mesmos requisitos que o servidor da base de dados do site. No entanto, o servidor da réplica não precisa de executar a mesma versão ou edição do SQL Server que o servidor da base de dados do site, desde que execute uma versão e edição suportadas do SQL Server. Para obter informações consulte [Suporte para versões SQL Server para Gestor](../../../../core/plan-design/configs/support-for-sql-server-versions.md) de Configuração  

    -   O Serviço de Servidor EsqL no computador que acolhe a base de dados de réplicas deve ser executado como conta **System.**  

    -   O SQL Server que aloja a base de dados do site e que aloja uma réplica de base de dados têm de ter **replicação do SQL Server** instalada.  

    -   A base de dados do site tem de **publicar** a réplica da base de dados e cada servidor de réplica de base de dados remota tem de **subscrever** os dados publicados.  

    -   O SQL Server que aloja a base de dados do site e que aloja uma réplica da base de dados têm de estar configurados para suportar um **Tamanho de Replicação de Texto Máx.** de 2 GB. Para ver um exemplo desta configuração para o SQL Server 2012, veja [Configure the max text repl size Server Configuration Option (Configurar a Opção de Configuração de Servidor max text repl size)](https://go.microsoft.com/fwlink/p/?LinkId=273960).  

-   **Certificado auto-assinado:** Para configurar uma réplica de base de dados, deve criar um certificado auto-assinado no servidor de réplica de base de dados e disponibilizar este certificado a cada ponto de gestão que utilize esse servidor de réplica de base de dados.  

    -   O certificado é automaticamente disponibilizado aos pontos de gestão que estejam instalados no servidor de réplicas da base de dados.  

    -   Para disponibilizar este certificado a pontos de gestão remotos, terá de exportar o certificado e adicioná-lo ao arquivo de certificados **Pessoas Fidedignas** no ponto de gestão remoto.  

-   **Notificação do cliente:** para suportar a notificação de cliente com uma réplica de base de dados para um ponto de gestão, é necessário configurar a comunicação entre o servidor da base de dados do site e o servidor de réplica da base de dados para o **SQL Server Service Broker**. Isto requer a:  

    -   Configuração de cada base de dados com informações sobre a outra base de dados  

    -   Troca de certificados entre as duas bases de dados para comunicação segura  

**Limitações ao utilizar réplicas de base de dados:**  

-   Quando o site está configurado para publicar réplicas de base de dados, devem ser utilizados os procedimentos seguintes em vez dos procedimentos normais:  

    -   [Desinstale um servidor de site que publique uma réplica de base de dados](#BKMK_DBReplicaOps_Uninstall)  

    -   [Mover um servidor do site que publica uma réplica de base de dados](#BKMK_DBReplicaOps_Move)  

-   **Upgrades para o ramo atual do Gestor**de Configuração : Antes de atualizar um site, seja do System Center 2012 Configuration Manager para o diretor de configuração da secção atual ou de atualizar o atual ramo do Gestor de Configuração para o mais recente lançamento, deve desativar réplicas de base de dados para pontos de gestão.  Após a atualização do site, pode reconfigurar as réplicas de base de dados para pontos de gestão.  

-   **Múltiplas réplicas num único Servidor SQL:**  Se configurar um servidor de réplica de base de dados para alojar várias réplicas de bases de dados para pontos de gestão (cada réplica deve estar numa instância separada) deve utilizar um script de configuração modificado (a partir do passo 4 da secção seguinte) para evitar a sobreposição do certificado auto-assinado em uso por réplicas de bases de dados previamente configuradas nesse servidor.  

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Configurar réplicas de base de dados  
Para configurar uma réplica de base de dados, são necessários os passos seguintes:  

-   [Passo 1 - Configurar o servidor da base de dados do site para publicar a réplica da base de dados](#BKMK_DBReplica_ConfigSiteDB)  

-   [Passo 2 - Configuração do servidor de réplica de base de dados](#BKMK_DBReplica_ConfigSrv)  

-   [Passo 3 - Configurar pontos de gestão para utilizar a réplica da base de dados](#BKMK_DBReplica_ConfigMP)  

-   [Passo 4 - Configure um certificado auto-assinado para o servidor de réplica de base de dados](#BKMK_DBReplica_Cert)  

-   [Passo 5 - Configure o Corretor de Serviço sQL server para o servidor de réplica de base de dados](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a>Passo 1 - Configure o servidor de base de dados do site para publicar a réplica da base de dados  
 Utilize o procedimento seguinte como exemplo de como configurar o servidor da base de dados do site num computador com o Windows Server 2008 R2 para publicar a réplica da base de dados. Se tiver outra versão do sistema operativo, consulte a respetiva documentação e ajuste os passos deste procedimento conforme necessário.  

##### <a name="to-configure-the-site-database-server"></a>Para configurar o servidor da base de dados do site  

1.  No servidor da base de dados do site, defina o SQL Server Agent para ser iniciado automaticamente.  

2.  No servidor de base de dados do site, crie um grupo de utilizadores local com o nome **ConfigMgr_MPReplicaAccess**. Terá de adicionar a este grupo a conta de computador de cada servidor de réplicas da base de dados que utiliza neste site, para permitir que esses servidores de réplicas sincronizem com a réplica da base de dados publicada.  

3.  No servidor de base de dados do site, configure uma partilha de ficheiros com o nome **ConfigMgr_MPReplica**.  

4.  Adicione as seguintes permissões à **ConfigMgr_MPReplica** partilha:  

    > [!NOTE]  
    >  Se o SQL Server Agent utilizar uma conta diferente da conta do sistema local, substitua SYSTEM por esse nome de conta na lista seguinte.  

    -   **Permissões de Partilha**:  

        -   SYSTEM: **Escrita**  

        -   ConfigMgr_MPReplicaAccess: **Ler**  

    -   **Permissões de NTFS**:  

        -   SYSTEM: **Controlo Total**  

        -   ConfigMgr_MPReplicaAccess: **Ler**, **Ler & executar**, Listar conteúdos de **pastas**  

5.  Utilize o **SQL Server Management Studio** para estabelecer ligação à base de dados do site e execute o seguinte procedimento armazenado como uma consulta: **spCreateMPReplicaPublication**  

Quando o procedimento armazenado for concluído, o servidor da base de dados do site estará configurado para publicar a réplica da base de dados.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Passo 2 - Configurar o servidor de réplicas da base de dados  
O servidor de réplica da base de dados é um computador que executa o SQL Server e que aloja uma réplica da base de dados do site para utilização pelos pontos de gestão. Numa agenda fixa, o servidor de réplicas da base de dados sincroniza a sua cópia da base de dados com a réplica da base de dados que é publicada pelo servidor da base de dados do site.  

O servidor de réplicas da base de dados tem de satisfazer os mesmos requisitos que o servidor da base de dados do site. No entanto, o servidor de réplica da base de dados poderá executar uma edição ou versão do SQL Server diferente da utilizada pelo servidor da base de dados do site. Para obter informações sobre as versões suportadas do Servidor SQL, consulte o [suporte para versões SQL Server para](../../../../core/plan-design/configs/support-for-sql-server-versions.md) tópico de Gestor de Configuração.  

> [!IMPORTANT]  
>  O Serviço do SQL Server no computador que aloja a réplica da base de dados tem de ser executado como a conta do Sistema.  

Utilize o seguinte procedimento como exemplo de como configurar um servidor de réplica da base de dados num computador com o Windows Server 2008 R2. Se tiver outra versão do sistema operativo, consulte a respetiva documentação e ajuste os passos deste procedimento conforme necessário.  

##### <a name="to-configure-the-database-replica-server"></a>Para configurar o servidor de réplicas da base de dados  

1. No servidor de réplicas da base de dados, defina o SQL Server Agent para arrancar automaticamente.  

2. No servidor de réplica da base de dados, utilize o **SQL Server Management Studio** para estabelecer ligação ao servidor local, navegue para a pasta **Replicação** , clique em Subscrições Locais e selecione **Novas Subscrições** para iniciar o **Assistente de Nova Subscrição**:  

   1. Na página **Publicação** , na caixa de listagem **Publicador** , selecione **Procurar Publicador do SQL Server**, introduza o nome do servidor da base de dados do site e clique em **Ligar**.  

   2. Selecione **ConfigMgr_MPReplica**e, em seguida, clique em **Seguinte**.  

   3. Na página de Localização do **Agente de Distribuição,** selecione **Executar cada agente no seu Assinante (assinaturas de puxar)** e clique **em Seguinte**.  

   4. Na página **Subscritores** , execute um dos seguintes procedimentos:  

      -   Selecione uma base de dados existente no servidor de réplica da base de dados a utilizar para a réplica da base de dados e clique em **OK**.  

      -   Selecione **Nova base de dados** para criar uma nova base de dados para a réplica da base de dados. Na página **Nova Base de Dados** , especifique um nome para a base de dados e clique em **OK**.  

   5. Clique **em Seguir** para continuar.  

   6. Na página de Segurança do **Agente de Distribuição,** clique no botão de propriedades **(....)** na linha de ligação de assinante da caixa de diálogo e, em seguida, configure as definições de segurança para a ligação.  

      > [!TIP]  
      >  O botão de propriedades, **(....)**, está na quarta coluna da caixa de visualização.  

      **Definições de segurança:**  

      - Configure a conta que gere o processo do Agente de Distribuição (a conta de processo):  

        -   Se o Agente servidor SQL funcionar como sistema local, selecione Executar sob a conta de **serviço do Agente de Servidor SQL (esta não é uma melhor prática de segurança recomendada.)**  

        -   Se o SQL Server Agent for executado utilizando outra conta, selecione **Executar sob a seguinte conta do Windows**e configure essa conta. Poderá especificar uma conta do Windows ou uma conta do SQL Server.  

        > [!IMPORTANT]  
        >  Terá de conceder à conta que executa o Agente de Distribuição permissões para o publicador como subscrição de solicitação. Para obter informações sobre a configuração destas permissões, veja [Distribution Agent Security (Segurança do Agente de Distribuição)](https://go.microsoft.com/fwlink/p/?LinkId=238463) na Biblioteca TechNet do SQ Server.  

      - Em **Ligar ao Distribuidor**, selecione **Representando a conta de processo**.  

      - Em **Ligar ao Subscritor**, selecione **Representando a conta de processo**.  

        Após configurar as definições de segurança da ligação, clique em **OK** para guardá-las e clique em **Seguinte**.  

   7. Na página **Agendamento da Sincronização** , na caixa de listagem **Agenda do Agente** , selecione **Definir agenda**e configure a **Nova Agenda de Tarefa**. Desloque a frequência a ocorrer **Diariamente,** repita a cada **5 minutos,** e a duração para não ter **data de fim**. Clique em **Seguinte** para guardar o agendamento e clique novamente em **Seguinte** .  

   8. Na página **Descontadores** de Assistentes, selecione a caixa de verificação para **Criar as subscrições(s)** e, em seguida, clique **em Seguinte**.  

   9. Na página **Concluir o Assistente** , clique em **Concluir**e em **Fechar** para concluir o Assistente.  

3. Imediatamente depois de concluir o Assistente de nova subscrição, utilize **SQL Server Management Studio** para estabelecer ligação à base de dados do servidor de réplica da base de dados e execute a seguinte consulta para ativar a propriedade de base de dados TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Consulte o estado da sincronização para confirmar que a subscrição teve êxito:  

   -   No computador subscritor:  

       -   No **SQL Server Management Studio**, estabeleça ligação ao servidor de réplica da base de dados e expanda **Replicação**.  

       -   Expandir **subscrições locais,** clicar na subscrição da base de dados do site e, em seguida, selecionar **o Estado de Sincronização**do View .  

   -   No computador publicador:  

       -   No **Estúdio de Gestão de Servidores SQL,** ligue-se ao computador de base de dados do site, clique à direita na pasta **de Replicação** e, em seguida, selecione **Launch Replication Monitor**.  

5. Para permitir a integração do tempo de execução da linguagem comum (CLR) para a réplica da base de dados, utilize o **SQL Server Management Studio** para se ligar à réplica da base de dados no servidor de réplica seletiva e executar o seguinte procedimento armazenado como uma consulta: **executivo sp_configure 'clr habilitado', 1; Reconfigurar COM SOBREPOSIÇÃO**  

6. Para cada ponto de gestão que utilize um servidor de réplica da base de dados, adicione a respetiva conta de computador ao grupo local **Administradores** desse servidor de réplica da base de dados.  

   > [!TIP]  
   >  Este passo não é necessário para pontos de gestão que sejam executados no servidor de réplicas da base de dados.  

   A réplica da base de dados está agora pronta para ser utilizada por um ponto de gestão.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a>Passo 3 - Configure pontos de gestão para usar a réplica da base de dados  
 Poderá configurar um ponto de gestão num site primário para utilizar uma réplica da base de dados quando instalar a função de ponto de gestão, ou poderá reconfigurar um ponto de gestão existente para utilizar uma réplica da base de dados.  

 Utilize as informações seguintes para configurar um ponto de gestão para utilizar uma réplica da base de dados:  

-   **Para configurar um novo ponto de gestão:** na página **Base de Dados do Ponto de Gestão** do assistente utilizado para instalar o ponto de gestão, selecione **Utilizar uma réplica da base de dados**e especifique o FQDN do computador que aloja a réplica da base de dados. Em seguida, em **Nome da base de dados do site do ConfigMgr**, especifique o nome da base de dados da réplica da base de dados nesse computador.  

-   **Para configurar um ponto de gestão previamente instalado**: abra a página de propriedades do ponto de gestão, selecione o separador **Base de Dados do Ponto de Gestão** , selecione **Utilizar uma réplica da base de dados**e especifique o FQDN do computador que aloja a réplica da base de dados. Em seguida, em **Nome da base de dados do site do ConfigMgr**, especifique o nome da base de dados da réplica da base de dados nesse computador.  

-   Para cada ponto de **gestão que utilize uma réplica**de base de dados, deve adicionar manualmente a conta de computador do servidor de pontos de gestão ao **db_datareader** função para a réplica da base de dados.  

Além de configurar o ponto de gestão para utilizar o servidor de réplica da base de dados, terá de ativar a **Autenticação do Windows** no **IIS** no ponto de gestão:  

1.  Open **Internet Information Services (IIS) Manager**.  

2.  Selecione o site utilizado pelo ponto de gestão e abra **Autenticação**.  

3.  Detete a **autenticação do Windows** para **ativado**e, em seguida, feche o Gestor de Serviços de Informação de **Internet (IIS).**  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Passo 4 - Configurar um certificado autoassinado para o servidor de réplica da base de dados  
 Deve criar um certificado auto-assinado no servidor de réplica de base de dados e disponibilizar este certificado a cada ponto de gestão que utilize esse servidor de réplica de base de dados.  

 O certificado é automaticamente disponibilizado aos pontos de gestão que estejam instalados no servidor de réplicas da base de dados. No entanto, para disponibilizar o certificado aos pontos de gestão remotos, terá de exportar o certificado e adicioná-lo ao arquivo de certificados de Pessoas Fidedignas no ponto de gestão remoto.  

 Utilize os seguintes procedimentos como um exemplo de como configurar o certificado auto-assinado no servidor de réplica de base de dados para um computador R2 do Windows Server 2008. Se tiver outra versão do sistema operativo, consulte a respetiva documentação e ajuste os passos destes procedimentos conforme necessário.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Para configurar um certificado auto-assinado para o servidor de réplica de base de dados  

1.  No servidor de réplicas de base de dados, abra um pedido de comando PowerShell com privilégios administrativos e, em seguida, executar o seguinte comando: **set-executionpolicy UnRestricted**  

2.  Copie o seguinte script do PowerShell e guarde-o como um ficheiro com o nome **CreateMPReplicaCert.ps1**. Coloque uma cópia deste ficheiro na pasta raiz da partição do sistema do servidor de réplicas da base de dados.  

    > [!IMPORTANT]  
    >  Se estiver a configurar mais do que uma réplica de base de dados num único SQL Server, para cada réplica subsequente que configurar tem de utilizar uma versão modificada deste script para este procedimento. Veja  [Script suplementar para réplicas de base de dados adicionais num único SQL Server](#bkmk_supscript)  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  No servidor de réplica da base de dados, execute o seguinte comando que se aplica à configuração do SQL Server:  

    -   Para uma instância predefinida do Servidor SQL: Clique à direita no ficheiro **CreateMPReplicaCert.ps1** e selecione **Executar com PowerShell**. Quando o script é executado, cria o certificado auto-assinado e confunde o SQL Server para usar o certificado.  

    -   Para uma instância nomeada de SQL Server: Use PowerShell para executar o comando **%path%\CreateMPReplicaCert.ps1 xxxxxx** onde **xxxxxx** é o nome da instância SQL Server.  

    -   Após a conclusão do script, certifique-se de que o SQL Server Agent está em execução. Se não estiver, reinicie o SQL Server Agent.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Para configurar pontos de gestão remota para usar o certificado auto-assinado do servidor de réplica de base de dados  

1.  Execute os seguintes passos no servidor de réplica de base de dados para exportar o certificado auto-assinado do servidor:  

    1.  Clique em **Iniciar,** clique em **Executar,** e digite **mmc.exe**. Na consola vazia, clique em **Ficheiro**e clique em **Adicionar/Remover Snap-in**.  

    2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

    3.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Seguinte**.  

    4.  Na caixa de diálogo **Selecionar Computador** , certifique-se de que **Computador local: (o computador onde esta consola está a ser executada)** está selecionado e, em seguida, clique em **Concluir**.  

    5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

    6.  Na consola, expandir **Certificados (Computador Local),** expandir **Pessoal,** e selecionar **Certificados**.  

    7.  Clique no certificado com o nome amigável do Certificado de Identificação do **Servidor ConfigMgr SQL,** clique em **Todas as Tarefas**e, em seguida, selecione **Export .**  

    8.  Conclua o **Assistente para Exportar Certificados** , utilizando as opções predefinidas, e guarde o certificado com a extensão de nome de ficheiro **.cer** .  

2.  Execute os seguintes passos no computador do ponto de gestão para adicionar o certificado auto-assinado para o servidor de réplica de base de dados à loja de certificados Pessoas Fidedignas no ponto de gestão:  

    1.  Repita os passos anteriores de 1.a a 1.e para configurar o **MMC** de encaixe do certificado no computador do ponto de gestão.  

    2.  Na consola, expanda **Certificados (Computador Local)**, expanda **Pessoas Fidedignas**, clique com o botão direito do rato em **Certificados**, selecione **Todas as Tarefas**e, em seguida, selecione **Importar** para iniciar o **Assistente para Importar Certificados**.  

    3.  Na página **Ficheiro a Importar** , selecione o certificado guardado no passo 1.h e, em seguida, clique em **Seguinte**.  

    4.  Na página **Arquivo de Certificados** , selecione **Colocar todos os certificados no seguinte arquivo**, com o **Arquivo de certificados** definido para **Pessoas Fidedignas**, e clique em **Seguinte**.  

    5.  Clique em **Concluir** para fechar o assistente e concluir a configuração do certificado no ponto de gestão.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Passo 5 - Configurar o SQL Server Service Broker para o servidor de réplica da base de dados  
Para suportar a notificação de cliente com uma réplica de base de dados para um ponto de gestão, é necessário configurar a comunicação entre o servidor da base de dados do site e o servidor de réplica de base de dados para o SQL Server Service Broker. Isto requer a configuração de cada base de dados com informações sobre a outra base de dados e a troca de certificados entre as duas bases de dados para uma comunicação segura.  

> [!NOTE]  
>  Para poder utilizar o procedimento seguinte, o servidor de réplica de base de dados deve concluir com êxito a sincronização inicial com o servidor de base de dados do site.  

 O procedimento seguinte não modifica a porta do Service Broker que está configurada no SQL Server para o servidor de base de dados do site ou para o servidor de réplica de base de dados. Em vez disso, este procedimento configura cada base de dados para comunicar com a outra base de dados, utilizando a porta correta do Service Broker.  

 Utilize o procedimento seguinte para configurar o Service Broker para o servidor da base de dados e para o servidor de réplica da base de dados.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Para configurar o Service Broker para uma réplica de base de dados  

1. Utilize o **Estúdio de Gestão de Servidores SQL** para se ligar à base de dados do servidor de réplicas de base de dados e, em seguida, executar a seguinte consulta para ativar o Corretor de Serviços no servidor de réplica de base de dados: **ALTER DATABASE &lt;Replica Database\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. Em seguida, no servidor de réplica de base de dados, configure o Service Broker para notificação de cliente e exporte o certificado do Service Broker. Para isso, execute um procedimento armazenado do SQL Server que configura o Service Broker e exporta o certificado numa única ação. Ao executar o procedimento armazenado, deve especificar o FQDN do servidor de réplica de base de dados, o nome da base de dados de réplicas de bases de dados e uma localização para a exportação do ficheiro de certificado.  

    Executar a seguinte consulta para configurar os detalhes necessários no servidor de réplica de base de dados e para exportar o certificado para o servidor de réplica de base de dados: **EXEC sp_BgbConfigSSBForReplicaDB '&lt;Replica SQL Server FQDN\>', '&lt;Replica Database Name\>', '&lt;Certificate Backup File Path\>'**  

   > [!NOTE]  
   >  Para este passo, se o servidor de réplica da base de dados não estiver na instância predefinida do SQL Server, é necessário especificar também o nome da instância além do nome da base de dados de réplica. Para tal, ** &lt;\> ** substitua o Nome da Base de Dados de Réplica sintetizada por ** &lt;nome de réplica de nome\\Replica Database Name\>**.  

    Depois de exportar o certificado do servidor de réplica de base de dados, coloque uma cópia do certificado no servidor de base de dados de sites primários.  

3. Utilize o **SQL Server Management Studio** para ligar à base de dados do site primário. Depois de ligar à base de dados de sites primários, execute uma consulta para importar o certificado e especificar a porta do Service Broker que está a ser utilizada no servidor de réplica de base de dados, o FQDN do servidor de réplica de base de dados e o nome da base de dados de réplicas de bases de dados. Isto configura a base de dados de sites primários que o Service Broker utilizará para comunicar com a base de dados do servidor de réplica de base de dados.  

    Executar a seguinte consulta para importar o certificado do servidor de réplica de base de dados e especificar os detalhes necessários: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;SQL Service Broker Port\>',&lt;' Certificado Ficheiro ',\>'&lt;Replica SQL Server FQDN\>', '&lt;Replica Database Name\>'**  

   > [!NOTE]  
   >  Para este passo, se o servidor de réplica da base de dados não estiver na instância predefinida do SQL Server, é necessário especificar também o nome da instância além do nome da base de dados de réplica. Para tal, substitua ** &lt;\> ** o Nome da Base de Dados de Réplicas por **"Nome\\de Réplica De\>base de dados**de réplicas " Nome base de dados .  

4. Em seguida, no servidor de base de dados do site, executar o seguinte comando para exportar o certificado para o servidor de base de dados do site: **EXEC sp_BgbCreateAndBackupSQLCert '&lt;Certificado Backup File Path\>' '**  

    Depois de exportar o certificado do servidor de base de dados do site, coloque uma cópia do certificado no servidor de réplica de base de dados.  

5. Utilize o **SQL Server Management Studio** para ligar à base de dados do servidor de réplica da base de dados. Depois de ligar à base de dados do servidor de réplica de base de dados, execute uma consulta para importar o certificado e especificar o código do site do site primário e a porta do Service Broker que está a ser utilizada no servidor de base de dados do site. Isto configura o servidor de réplica de base de dados para utilizar o Service Broker para comunicar com a base de dados do site primário.  

    Executar a seguinte consulta para importar o certificado do servidor de base de dados do site: **EXEC sp_BgbConfigSSBForRemoteService '&lt;Código\>de site '' '&lt;SQL Service Broker Port\>', '&lt;Certificado Ficheiro Path\>' '**  

   Alguns minutos depois de concluir a configuração da base de dados do site e da base de dados de réplica de base de dados, o Notification Manager do site primário configura a conversa do Service Broker para notificação de cliente da base de dados do site primário para a réplica de base de dados.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Script suplementar para réplicas de base de dados adicionais num único SQL Server  
 Quando utilizar o script do passo 4 para configurar um certificado auto-assinado para o servidor de réplica de base de dados num Servidor SQL que já tem uma réplica de base de dados que planeia continuar a utilizar, tem de utilizar uma versão modificada do script original. As seguintes modificações impedem o script de eliminar um certificado existente no servidor e criam certificados subsequentes com nomes amigáveis exclusivos.  Edite o script original da seguinte forma:  

-   Comentar (evitar a execução) cada linha entre as entradas do script **# Eliminar cert existente se existir** e # Criar o novo **cert**. Para tal, adicione **#** um como o primeiro personagem de cada linha aplicável.  

-   Para cada réplica de base de dados subsequente, utilize este script para configurar, atualizar e atribuir um nome amigável ao certificado.  Para isso, edite a linha **$enrollment. CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** e substitua o Certificado de Identificação do **Servidor ConfigMgr SQL** por um novo nome, como O Certificado de Identificação do **Servidor ConfigMgr SQL1**.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a>Gerir configurações de réplicas de base de dados  
 Quando utilizar uma réplica de base de dados num site, utilize as informações das secções seguintes para complementar o processo de desinstalação de uma réplica de base de dados, o processo de desinstalação de um site que utiliza uma réplica de base de dados ou o processo de transferência da base de dados do site para uma nova instalação do SQL Server. Quando utilizar informações das secções seguintes para eliminar publicações, utilize as orientações para eliminar a replicação transacional para a versão do SQL Server utilizada para a réplica de base de dados. Por exemplo, se utilizar o SQL Server 2008 R2, consulte [Como: Eliminar uma Publicação (Programação Transact-SQL de replicação)](https://go.microsoft.com/fwlink/p/?LinkId=273934).  

> [!NOTE]  
>  Depois de restaurar uma base de dados do site configurada para réplicas de bases de dados, antes de poder utilizar as réplicas de bases de dados, tem de reconfigurar cada réplica de base de dados, recriando as publicações e as subscrições.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Desinstalar uma réplica de base de dados  
 Ao utilizar uma réplica de base de dados para um ponto de gestão, poderá ser necessário desinstalar a réplica de base de dados durante um período de tempo e depois reconfigurá-la para utilização. Por exemplo, tem de remover réplicas de bases de dados antes de atualizar um site do Gestor de Configuração para um novo pacote de serviços. Após a conclusão da atualização do site, pode restaurar a réplica de base de dados para utilização.  

 Utilize os passos seguintes para desinstalar uma réplica de base de dados.  

1.  No espaço de trabalho da **Administração** da consola Do Gestor de Configuração, expanda a **Configuração**do Site, selecione **Servidores e Funções**de Sistema de Site, e, em seguida, no painel de detalhes selecione o servidor do sistema do site que acolhe o ponto de gestão que utiliza a réplica da base de dados que irá desinstalar.  

2.  No painel **Funções de Sistema de Sites** , clique com o botão direito do rato em **Ponto de gestão** e selecione **Propriedades**.  

3.  No separador **Base de Dados do Ponto de Gestão** , selecione **Utilizar a base de dados do site** para configurar o ponto de gestão para utilizar a base de dados em vez da réplica da base de dados. Em seguida, clique em **OK** para guardar a configuração.  

4.  Depois, utilize o **SQL Server Management Studio** para executar as seguintes tarefas:  

    -   Eliminar a publicação da réplica de base de dados na base de dados de servidor do site.  

    -   Eliminar a subscrição da réplica de base de dados no servidor de réplica de base de dados.  

    -   Eliminar a base de dados de réplica no servidor de réplica de base de dados.  

    -   Desativar a publicação e a distribuição no servidor de base de dados do site. Para desativar a publicação e distribuição, clique na pasta replicação e clique em **Desativar a publicação e distribuição**.  

5.  Depois de eliminar a publicação, a subscrição e a base de dados de réplica e de desativar a publicação no servidor de base de dados do site, a réplica de base de dados é desinstalada.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Desinstalar um servidor do site que publica uma réplica de base de dados  
 Antes de desinstalar um site que publica uma réplica de base de dados, utilize os passos seguintes para limpar a publicação e quaisquer subscrições.  

1.  Utilize o **SQL Server Management Studio** para eliminar a publicação da réplica de base de dados na base de dados do servidor do site.  

2.  Utilize o **SQL Server Management Studio** para eliminar a subscrição da réplica de base de dados de cada SQL Server remoto que aloja uma réplica de base de dados deste site.  

3.  Desinstale o site.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a>Mova uma base de dados de servidor de site que publique uma réplica de base de dados  
 Quando mover a base de dados do site para um novo computador, utilize os seguintes passos:  

1.  Utilize o **SQL Server Management Studio** para eliminar a publicação da réplica de base de dados na base de dados do servidor do site.  

2.  Utilize o **SQL Server Management Studio** para eliminar a subscrição da réplica de base de dados em cada servidor de réplica de base de dados deste site.  

3.  Mova a base de dados para o novo computador com SQL Server. Para mais informações, consulte a secção [de configuração da base](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) de dados do site no tópico de infraestrutura do Gestor de [Configuração.](../../../../core/servers/manage/modify-your-infrastructure.md)  

4.  Recrie a publicação da réplica de base de dados no servidor da base de dados do site. Para obter mais informações, veja o [Passo 1 - Configurar o servidor da base de dados do site para publicar a réplica da base de dados](#BKMK_DBReplica_ConfigSiteDB) deste tópico.  

5.  Recrie as subscrições para a réplica de base de dados em cada servidor de réplica de base de dados. Para obter mais informações, veja o [Passo 2 - Configurar o servidor de réplica da base de dados](#BKMK_DBReplica_ConfigSrv) deste tópico.  
