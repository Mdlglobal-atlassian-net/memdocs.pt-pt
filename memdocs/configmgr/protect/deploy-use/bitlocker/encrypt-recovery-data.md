---
title: Encriptar dados de recuperação
titleSuffix: Configuration Manager
description: Criptografe as chaves de recuperação bitLocker, os pacotes de recuperação e as hashes de senha tPM através da rede e na base de dados do Gestor de Configuração.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724441"
---
# <a name="encrypt-recovery-data"></a>Encriptar dados de recuperação

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Quando cria uma política de gestão BitLocker, o Gestor de Configuração implementa o serviço de recuperação para um ponto de gestão. Na página de **Gestão** de Clientes da política de gestão BitLocker, quando configura os Serviços de **Gestão BitLocker,** o cliente apoia informações de recuperação chave para a base de dados do site. Estas informações incluem chaves de recuperação BitLocker, pacotes de recuperação e hashes de senha TPM. Quando os utilizadores estão bloqueados fora do seu dispositivo protegido, pode utilizar estas informações para ajudá-los a recuperar o acesso ao dispositivo.

Dada a natureza sensível desta informação, é necessário protegê-la nas seguintes circunstâncias:

- O Gestor de Configuração requer uma ligação HTTPS entre o cliente e o serviço de recuperação para encriptar os dados em trânsito através da rede. Existem duas opções:

  - HTTPS-enable o site do IIS no ponto de gestão que acolhe o serviço de recuperação, não todo o papel de ponto de gestão. Esta opção aplica-se apenas à versão de Configuração Manager 2002.<!-- 5925660 -->

  - Configure o ponto de gestão para HTTPS. Sobre as propriedades do ponto de gestão, a definição de **conexões cliente** deve ser **HTTPS**. Esta opção aplica-se às versões 1910 ou 2002 do Gestor de Configuração.

    > [!NOTE]
    > Atualmente não suporta HTTP melhorado.

- Considere também encriptar estes dados quando armazenados na base de dados do site. Pode utilizar encriptação ao nível da célula SQL Server com o seu próprio certificado.

    Se não quiser criar um certificado de encriptação de gestão BitLocker, opte por armazenamento simples dos dados de recuperação. Quando criar uma política de gestão BitLocker, ative a opção de permitir que as informações de **recuperação sejam armazenadas em texto simples**.

    > [!NOTE]
    > Outra camada de segurança é encriptar toda a base de dados do site. Se ativar a encriptação na base de dados, não existem problemas funcionais no 'Gestor de Configuração'.
    >
    > Criptografe com cuidado, especialmente em ambientes de grande escala. Dependendo das tabelas que encripta e da versão do SQL, poderá notar até uma degradação de desempenho de 25%. Atualize os seus planos de backup e recuperação, para que possa recuperar com sucesso os dados encriptados.

## <a name="certificate-requirements"></a>Requisitos de certificados

### <a name="https-server-authentication-certificate"></a>Certificado de autenticação do servidor HTTPS

<!--5925660-->

Na versão atual do 'Gestor de Configuração' 1910, para integrar o serviço de recuperação BitLocker teve de ativar um ponto de gestão. A ligação HTTPS é necessária para encriptar as chaves de recuperação através da rede desde o cliente do Gestor de Configuração até ao ponto de gestão. Configurar o ponto de gestão e todos os clientes para HTTPS pode ser um desafio para muitos clientes.

A partir da versão 2002, o requisito HTTPS é para o site iIS que acolhe o serviço de recuperação, e não todo o papel de ponto de gestão. Esta alteração relaxa os requisitos do certificado e ainda encripta as chaves de recuperação em trânsito.

Agora, a propriedade de **ligações** ao Cliente do ponto de gestão pode ser **HTTP** ou **HTTPS**. Se o ponto de gestão estiver configurado para **HTTP,** para suportar o serviço de recuperação BitLocker:

1. Adquira um certificado de autenticação do servidor. Ligue o certificado ao website do IIS no ponto de gestão que acolhe o serviço de recuperação BitLocker.

2. Configure os clientes para confiar no certificado de autenticação do servidor. Há dois métodos para realizar esta confiança:

    - Utilize um certificado de um fornecedor de certificados de confiança pública e global. Por exemplo, mas não se limitando a, DigiCert, Thawte ou VeriSign. Os clientes windows incluem autoridades de certificados de raiz fidedignas (AE) destes fornecedores. Ao utilizar um certificado de autenticação do servidor emitido por um destes fornecedores, os seus clientes devem confiar automaticamente nele.

    - Utilize um certificado emitido por um CA da infraestrutura de chaves públicas da sua organização (PKI). A maioria das implementações do PKI adicionam os CAs de raiz confiáveis aos clientes windows. Por exemplo, utilizar serviços de certificados de diretório ativo com a política do grupo. Se emitir o certificado de autenticação do servidor a partir de um CA em que os seus clientes não confiam automaticamente, adicione o certificado raiz de confiança da AC aos clientes.

> [!TIP]
> Os únicos clientes que precisam de comunicar com o serviço de recuperação são os clientes que pretende visar com uma política de gestão BitLocker e inclui uma regra de **Gestão de Clientes.**

No cliente, utilize o **LogLockerManagementHandler.log** para resolver esta ligação. Para a conectividade com o serviço de recuperação, o registo mostra o URL que o cliente está a usar. Localize uma entrada `Checking for Recovery Service at`que comece com .

> [!NOTE]
> Se o seu site tiver mais de um ponto de gestão, ative HTTPS em todos os pontos de gestão do site com o qual um cliente gerido pelo BitLocker poderia potencialmente comunicar. Se o ponto de gestão HTTPS não estiver disponível, o cliente poderá falhar num ponto de gestão HTTP e, em seguida, não obter a sua chave de recuperação.
>
> Esta recomendação aplica-se a ambas as opções: ativar o ponto de gestão para HTTPS, ou ativar o website iIS que acolhe o serviço de recuperação no ponto de gestão.

### <a name="sql-encryption-certificate"></a>Certificado de encriptação SQL

Utilize este certificado para ativar a encriptação ao nível celular do SQL Server dos dados de recuperação do BitLocker. Pode utilizar o seu próprio processo para criar e implementar o certificado de encriptação de gestão BitLocker, desde que cumpra os seguintes requisitos:

- O nome do certificado de encriptação `BitLockerManagement_CERT`de gestão BitLocker deve ser .

- Criptografe este certificado com uma chave principal de base de dados.

- Os seguintes utilizadores de SQL precisam de permissões de **controlo** no certificado:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Implemente o mesmo certificado em todas as bases de dados do site da sua hierarquia.

- Crie o certificado com a versão mais recente do SQL Server no seu ambiente. Por exemplo:
  - Os certificados criados com o SQL Server 2016 ou posteriormente são compatíveis com o SQL Server 2014 ou mais cedo.
  - Os certificados criados com o SQL Server 2014 ou mais cedo não são compatíveis com o SQL Server 2016 ou mais tarde.

## <a name="example-scripts"></a>Exemplo de scripts

Estes scripts SQL são exemplos para criar e implementar um certificado de encriptação de gestão BitLocker na base de dados do site Do Gestor de Configuração.

### <a name="create-certificate"></a>Criar certificado

Este script de amostra faz as seguintes ações:

- Cria um certificado
- Define as permissões
- Cria uma chave de base de dados

Antes de utilizar este script num ambiente de produção, altere os seguintes valores:

- Nome da`CM_ABC`base de dados do site ()
- Palavra-passe para criar`MyMasterKeyPassword`a chave principal ( )
- Data de validade`20391022`do certificado ()

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Certificado de back up

Este guião de amostra saqueia um certificado. Quando guardar o certificado para um ficheiro, pode [então restaurá-lo](#restore-certificate) para outras bases de dados do site na hierarquia.

Antes de utilizar este script num ambiente de produção, altere os seguintes valores:

- Nome da`CM_ABC`base de dados do site ()
- Caminho e nome`C:\BitLockerManagement_CERT_KEY`de arquivo ()
- Palavra-passe`MyExportKeyPassword`chave de exportação ()

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Guarde o ficheiro de certificado exportado e a palavra-passe associada num local seguro.

### <a name="restore-certificate"></a>Restaurar certificado

Este script de amostra restaura um certificado de um ficheiro. Utilize este processo para implementar um certificado que criou noutra base de dados do site.

Antes de utilizar este script num ambiente de produção, altere os seguintes valores:

- Nome da`CM_ABC`base de dados do site ()
- Senha principal`MyMasterKeyPassword`()
- Caminho e nome`C:\BitLockerManagement_CERT_KEY`de arquivo ()
- Palavra-passe`MyExportKeyPassword`chave de exportação ()

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Verificar certificado

Utilize este script SQL para verificar se a SQL criou com sucesso o certificado com as permissões necessárias.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Se o certificado for válido, o `1`script devolve um valor de .

## <a name="see-also"></a>Consulte também

Para obter mais informações sobre estes comandos SQL, consulte os seguintes artigos:

- [SQL Server e chaves de encriptação de base de dados](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Criar certificado](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Certificado de reserva](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Criar chave-mestre](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Chave principal de backup](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Permissões de certificado de concessão](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
