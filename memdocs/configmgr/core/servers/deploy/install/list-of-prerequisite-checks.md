---
title: Verificações de pré-requisitos
titleSuffix: Configuration Manager
description: Referência das verificações pré-requisitoespecíficas específicas para atualizações do Gestor de Configuração.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f0ed1d5913154d90242d1aa2a47efbcf7d22282
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943795"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista de verificações pré-requisitos para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo detalha as verificações pré-requisitos que são executadas quando instala ou atualiza o Gestor de Configuração. Para mais informações, consulte [o verificador Pré-Requisito](prerequisite-checker.md).  



## <a name="errors"></a>Erros

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapeamentos de migração ativos no site primário de destino

*Aplica-se a: Central administration site*

Não existem mapeamentos de migração ativos para locais primários.

### <a name="active-replica-mp"></a>Réplica ativa MP

*Aplica-se a: Sítio Primário*

Há uma réplica de ponto de gestão ativa.

### <a name="administrative-rights-on-expand-primary-site"></a>Direitos administrativos sobre expansão do sítio primário

*Aplica-se a: Central administration site*

Ao expandir um site primário para uma hierarquia, a conta de utilizador que executa a configuração tem direitos **de Administrador** no servidor de site primário autónomo.

### <a name="administrative-rights-on-site-system"></a>Direitos administrativos no sistema de sites

*Aplica-se a: Site da administração central, local primário, local secundário*

A conta de utilizador que executa a configuração do Gestor de Configuração tem direitos **de Administrador** no servidor do site.

### <a name="administrator-rights-on-central-administration-site"></a>Direitos de administrador no site da administração central

*Aplica-se a: Sítio Primário*

A conta de utilizador que executa a configuração do Gestor de Configuração tem direitos **de Administrador** no servidor do site da administração central.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Ponto de sincronização da Inteligência de Ativos no site primário expandido

*Aplica-se a: Central administration site*

Quando se expande um site primário para uma hierarquia, o papel de ponto de sincronização da Inteligência de Ativos não está instalado no local primário autónomo.

### <a name="bits-enabled"></a>BITS habilitado

*Aplica-se a: Ponto de gestão*

O Serviço de Transferência Inteligente de Fundo (BITS) está instalado no ponto de gestão. Este cheque pode falhar por uma das seguintes razões:

- BITS não está instalado  

- O componente de compatibilidade IIS 6.0 WMI para iIS 7.0 não está instalado no servidor ou no anfitrião IIS remoto  

- A configuração não pôde verificar as definições remotas do IIS. Os componentes comuns do IIS não estão instalados no servidor do site.  

### <a name="case-insensitive-collation-on-sql-server"></a>Colagem insensível a casos no Servidor SQL

*Aplica-se a: servidor de base de dados do site*

A instalação Do Servidor SQL utiliza uma colagem insensível a casos, como **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Direitos administrativos do servidor do site da administração central sobre expandir o site primário

*Aplica-se a: Central administration site*

Ao expandir um site primário para uma hierarquia, a conta de computador do servidor do site da administração central tem direitos **de Administrador** no servidor de site primário autónomo.

### <a name="client-version-on-management-point-computer"></a>Versão do cliente no computador de ponto de gestão

*Aplica-se a: Ponto de gestão*

Está a instalar o ponto de gestão num servidor que não tem uma versão diferente do cliente do Gestor de Configuração instalado.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Gateway de gestão de nuvem no local primário expandido

*Aplica-se a: Central administration site*

Quando se expande um local primário para uma hierarquia, o papel de gateway de gestão de nuvem não é instalado no local primário autónomo.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Ligação ao Servidor SQL no site da administração central

*Aplica-se a: Sítio Primário*

A conta de utilizador que executa a configuração do Gestor de Configuração no site principal para se juntar a uma hierarquia existente tem a função **de sisadmina** no site do Servidor SQL para o site da administração central.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>As configurações personalizadas do agente cliente têm o NAP ativado

*Aplica-se a: Site da administração central, local primário*

Não existem configurações personalizadas do cliente que permitam a proteção de acesso à rede (NAP).

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Ponto de serviço de armazém de dados no local primário expandido

*Aplica-se a: Central administration site*

Quando se expande um local primário para uma hierarquia, a função de ponto de serviço de armazém de dados não é instalada no local primário autónomo.

### <a name="dedicated-sql-server-instance"></a>Instância dedicada do Servidor SQL

*Aplica-se a: Site da administração central, local primário, local secundário*

Configurou uma instância dedicada do Servidor SQL para alojar a base de dados do Site Do Gestor de Configuração.

Se outro site utilizar a instância, deve selecionar uma instância diferente para o novo site. Também pode desinstalar o outro site, ou mover a sua base de dados para uma instância diferente para o servidor SQL.

### <a name="default-client-agent-settings-have-nap-enabled"></a>As definições padrão do agente cliente têm o NAP ativado

*Aplica-se a: Site da administração central, local primário*

As definições padrão do cliente não permitem a proteção de acesso à rede (NAP).

### <a name="domain-membership-error"></a>Adesão ao domínio (erro)

*Aplica-se a: Site de administração central, site primário, site secundário, Provedor SMS, Servidor SQL*

O computador 'Gestor de Configuração' é membro de um domínio Windows.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Ponto de proteção de pontofinal no local primário expandido

*Aplica-se a: Central administration site*

Quando se expande um local primário para uma hierarquia, a função de ponto de proteção de pontos finais não é instalada no local primário autónomo.

### <a name="existing-configuration-manager-server-components-on-server"></a>Componentes do servidor do Gestor de Configuração existentes no servidor

*Aplica-se a: Site da administração central, local primário, local secundário*

Um servidor de site ou função do sistema do site ainda não está instalado no servidor selecionado para a instalação do site.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Site primário autónomo existente para versão e código do site

*Aplica-se a: Site da administração central, local primário*

O local principal que planeia expandir é um local primário autónomo. Tem a mesma versão do Gestor de Configuração, mas um código de site diferente do site da administração central a instalar.

### <a name="firewall-exception-for-sql-server"></a>Exceção de firewall para SQL Server

*Aplica-se a: Site da administração central, local primário, local secundário, ponto de gestão*

O Windows Firewall está desativado ou existe uma exceção relevante para o Windows Firewall para o Servidor SQL.

Permita que o Sqlservr.exe ou as portas TCP necessárias sejam acedidas remotamente. Por predefinição, o SQL Server ouve na porta TCP 1433, e o SQL Server Service Broker (SSB) utiliza a porta TCP 4022.

### <a name="free-disk-space-on-site-server"></a>Espaço de disco gratuito no servidor do site

*Aplica-se a: Site da administração central, local primário, local secundário*

Para instalar o servidor do site, deve ter pelo menos 15 GB de espaço de disco livre. Se instalar o Fornecedor SMS no mesmo servidor, necessita de mais 1 GB de espaço livre.

### <a name="iis-service-running"></a>Serviço IIS em execução

*Aplica-se a: ponto de gestão, ponto de distribuição*

O IIS está instalado e a funcionar no servidor para o ponto de gestão ou ponto de distribuição.

### <a name="incompatible-collection-references"></a>Referências de recolha incompatíveis

*Aplica-se a: Central administration site*

Durante uma atualização, as coleções referem apenas outras coleções do mesmo tipo.

### <a name="match-collation-of-expand-primary-site"></a>Coação de correspondência do site primário de expandir

*Aplica-se a: Central administration site*

Ao expandir um site primário para uma hierarquia, a base de dados do site para o local primário autónomo tem a mesma colagem que a base de dados do site no site da administração central.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Tamanho máximo de replicação de texto para SQL Server Sempre em grupos de disponibilidade

*Aplica-se a: servidor de base de dados do site*

Ao utilizar o Servidor SQL Sempre ligado, a definição de tamanho de **repl** de texto max deve estar corretamente configurada. Para mais informações, consulte [Prepare-se para utilizar o Servidor SQL Sempre em grupos de disponibilidade com o Gestor](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)de Configuração .

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune Connector no site primário expandido

*Aplica-se a: Central administration site*

Quando expande um site primário para uma hierarquia, a função Microsoft Intune Connector não está instalada no site primário autónomo.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Biblioteca de Compressão Diferencial Remota da Microsoft (RDC) registada

*Aplica-se a: Site da administração central, local primário, local secundário*

A biblioteca RDC está registada no servidor do site do Gestor de Configuração.

### <a name="microsoft-windows-installer"></a>Instalador microsoft Windows

*Aplica-se a: Site da administração central, local primário, local secundário*

Verifica a versão do Instalador do Windows.

Quando esta verificação falha, a configuração não pôde verificar a versão, ou a versão instalada não cumpre o requisito mínimo do Instalador do Windows 4.5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versão mínima .NET-Quadro para consola de Gestor de Configuração

*Aplica-se a: Consola de Gestor de Configuração*

A Microsoft .NET Framework 4.0 está instalada no computador da consola Do Gestor de Configuração.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versão mínima .NET-Quadro para servidor de site do Gestor de Configuração

*Aplica-se a: Site da administração central, local primário, local secundário*

.NET A estrutura 3.5 está instalada ou ativada no servidor do site do Gestor de Configuração.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Versão mínima .NET Framework para instalação de edição SQL Server Express para site secundário do Gestor de Configuração

*Aplica-se a: Local secundário*

.NET A estrutura 4.0 está instalada ou ativada no servidor de site secundário do Gestor de Configuração. Esta versão é exigida pelo SQL Server Express.

### <a name="parent-database-collation"></a>Colagem da base de dados dos pais

*Aplica-se a: Sítio Primário, Local secundário*

A colagem da base de dados do site corresponde à colagem da base de dados do site-mãe. Todos os sites de uma hierarquia têm de utilizar o mesmo agrupamento de bases de dados.

### <a name="parent-site-replication-status"></a>Estado de replicação do site dos pais

*Aplica-se a: Site da administração central, local primário*

O estado de replicação do local-mãe é **replicação ativa** (estado **125**).

### <a name="pending-system-restart"></a>Reinício de sistema pendente

*Aplica-se a: Site da administração central, local primário, local secundário*

Antes de executar a configuração, outro programa requer que o servidor seja reiniciado.

A partir da versão 1810, este cheque é mais resistente. Para ver se o computador se encontra em estado de reinício pendente, verifica os seguintes locais de registo:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>FQDN primário

*Aplica-se a: Site da administração central, site primário, site secundário, servidor de base de dados do site*

O nome NetBIOS do computador corresponde ao nome de anfitrião local no nome de domínio totalmente qualificado (FQDN).

### <a name="read-only-domain-controller"></a>Controladores de domínio só de leitura

*Aplica-se a: Site da administração central, local primário, local secundário*

Servidores de base de dados do site e servidores secundários do site não são suportados num controlador de domínio apenas para leitura (RODC).

Para mais informações, consulte o artigo de Suporte da Microsoft sobre [problemas ao instalar o SQL Server num controlador de domínio](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Colagem necessária do Servidor SQL

*Aplica-se a: Site da administração central, local primário, local secundário*

A instância para o Servidor SQL está configurada para utilizar **a** SQL_Latin1_General_CP1_CI_AS colagem.

Se a base de dados do site do Gestor de Configuração já estiver instalada, este controlo também se aplica à base de dados. Para obter informações sobre a alteração da instância do SQL Server e as colagens de bases de dados, consulte a [colagem SQL e](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)o suporte unicode .

Se estiver a usar um OS chinês e necessitar de suporte GB18030, este cheque não se aplica. Para obter mais informações sobre o apoio ao GB18030, consulte o [apoio internacional.](../../../plan-design/hierarchy/international-support.md)

### <a name="server-service-is-running"></a>O serviço de servidor está a funcionar

*Aplica-se a: Site da administração central, local primário, local secundário*

O serviço Server está iniciado e a funcionar.

### <a name="setup-source-folder"></a>Configurar pasta de origem

*Aplica-se a: Local secundário*

A conta do computador para o site secundário tem as seguintes permissões para a pasta fonte de configuração e partilha:

- **Ler** Permissões do sistema de ficheiros NTFS  

- **Ler** permissões de partilha  

> [!Note]  
> Se utilizar ações administrativas, por exemplo, C$ e D$, a conta de computador do site secundário deve ser um **Administrador** no servidor.  

### <a name="setup-source-version"></a>Versão de origem de configuração

*Aplica-se a: Local secundário*

A versão 'Gestor de Configuração' na pasta de origem especificada para a instalação do site secundário corresponde à versão 'Gestor de Configuração' do site principal.

### <a name="site-code-in-use"></a>Código do site em uso

*Aplica-se a: Sítio Primário*

O código de site especificado ainda não está em uso na hierarquia do Gestor de Configuração. Especifique um código de site único para este site.

### <a name="site-server-computer-account-administrative-rights"></a>Direitos administrativos de conta de servidor de servidor do site

*Aplica-se a: Site primário, servidor de base de dados do site*

A conta de computador do servidor do site tem direitos **de administrador** no servidor E ponto de gestão SQL.

### <a name="site-server-fqdn-length"></a>Comprimento FQDN do servidor do site

*Aplica-se a: Site da administração central, local primário, local secundário*

O comprimento do FQDN do servidor do site.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Servidor do site em modo passivo no site primário expandido

*Aplica-se a: Central administration site*

Quando expande um site primário para uma hierarquia, o servidor do site em função de modo passivo não está instalado no site primário autónomo.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Provedor SMS no mesmo domínio que o servidor do site

*Aplica-se a: Fornecedor SMS*

Qualquer instância do Fornecedor SMS está no mesmo domínio que o servidor do site.

### <a name="software-update-point-in-nlb-configuration"></a>Ponto de atualização de software na configuração nLB

*Aplica-se a: Ponto de atualização de software*

O site não está a utilizar o equilíbrio de carga de rede (NLB) com quaisquer localizações virtuais para pontos de atualização de software ativos.

### <a name="software-update-point-using-a-load-balancer"></a>Ponto de atualização de software usando um balanceador de carga

*Aplica-se a: Ponto de atualização de software*

O Gestor de Configuração não suporta pontos de atualização de software em rede (NLB) ou em equilibradores de carga de hardware (HLB).

### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidade Always On do SQL Server

*Aplica-se a: servidor de base de dados do site*

Ao utilizar o Servidor SQL Always On, deve cumprir os requisitos mínimos para acolher um grupo de disponibilidade. Para mais informações, consulte [Prepare-se para utilizar o Servidor SQL Sempre em grupos de disponibilidade com o Gestor](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)de Configuração .

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Grupo de disponibilidade do Servidor SQL configurado para secundários legíveis

*Aplica-se a: servidor de base de dados do site*

Ao utilizar o SQL Server Always On, verifique as réplicas do grupo de disponibilidade secundária.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>Grupo de disponibilidade do Servidor SQL configurado para falha manual

*Aplica-se a: servidor de base de dados do site*

Ao utilizar o Servidor SQL Always On, as réplicas do grupo de disponibilidade são configuradas para falhas manuais.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Réplicas do grupo de disponibilidade do Servidor SQL em instância padrão

*Aplica-se a: servidor de base de dados do site*

Ao utilizar o Servidor SQL Always On, as réplicas do grupo de disponibilidade estão na instância predefinida.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>As réplicas do grupo de disponibilidade SQL devem ter o mesmo modo de sementeira

<!-- SCCMDocs-pr#3899 -->
*Aplica-se a: servidor de base de dados do site*

A partir da versão 1906, quando utilizar o SQL Server Always On, é necessário configurar réplicas de grupo de disponibilidade com o mesmo modo de [sementeir](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### <a name="sql-availability-group-replicas-must-be-healthy"></a>Réplicas do grupo de disponibilidade SQL devem ser saudáveis

<!-- SCCMDocs-pr#3899 -->
*Aplica-se a: servidor de base de dados do site*

A partir da versão 1906, quando se utiliza o SQL Server Always On, as réplicas do grupo de disponibilidade estão num estado saudável.

### <a name="sql-server-configuration-for-site-upgrade"></a>Configuração do Servidor SQL para aactualização do site

*Aplica-se a: servidor de base de dados do site*

O Servidor SQL cumpre os requisitos mínimos para a atualização do site. Para mais informações, consulte [as versões Suportadas Do Servidor SQL](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>Edição do SQL Server

*Aplica-se a: servidor de base de dados do site*

O Servidor SQL no site não é O Expresso do Servidor SQL.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express no site secundário

*Aplica-se a: Local secundário*

O SQL Server Express pode instalar com sucesso no servidor de site secundário.

### <a name="sql-server-on-the-secondary-site-server"></a>Servidor SQL no servidor de site secundário

*Aplica-se a: Local secundário*

O Servidor SQL está instalado no servidor de site secundário. Não é possível instalar o SQL Server num sistema de site remoto para um site secundário.

> [!Warning]  
> Esta verificação só se aplica quando se leciona ter configuração, utilize uma instância existente do Servidor SQL.  

### <a name="sql-server-service-running-account"></a>Conta de execução do serviço SQL Server

*Aplica-se a: Site da administração central, local primário, local secundário*

A conta de inscrição para o serviço SQL Server não é uma conta de utilizador local ou **SERVIÇO LOCAL**.

Configure o serviço SQL Server para utilizar uma conta de domínio válida, **SERVIÇO DE REDE,** ou **SISTEMA LOCAL**.

### <a name="sql-server-site-database-consistency"></a>Consistência da base de dados do site do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

Verifique a consistência da base de dados.

### <a name="sql-server-sysadmin-rights"></a>Direitos de sindina do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

A conta de utilizador que executa a configuração do Gestor de Configuração tem a função **de sysadmina** na instância do Servidor SQL que selecionou para a instalação da base de dados do site. Esta verificação também falha quando a configuração não consegue aceder à instância do Servidor SQL para verificar permissões.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Direitos de sisadmina do Servidor SQL para site de referência

*Aplica-se a: servidor de base de dados do site*

A conta de utilizador que executa a configuração do Gestor de Configuração tem a função **de sysadmina** na instância de função do Servidor SQL que selecionou como base de dados do site de referência. São necessárias permissões de funções de **sisadmina** do Servidor SQL para modificar a base de dados do site.

### <a name="sql-server-tcp-port"></a>Porta TCP do servidor SQL

*Aplica-se a: servidor de base de dados do site*

O TCP está ativado para a instância Do Servidor SQL, e está programado para usar uma porta estática.

### <a name="sql-server-version"></a>Versão do SQL Server

*Aplica-se a: servidor de base de dados do site*

Uma versão suportada do SQL Server está instalada no servidor de base de dados do site especificado.

Para mais informações, consulte [as versões De Suporte para Servidor SQL](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>Os sem suporte para consola de Gestor de Configuração

*Aplica-se a: Consola de Gestor de Configuração*

Instale a consola 'Gestor de Configuração' em computadores que executem uma versão SISTEMA suportada.

Para mais informações, consulte as [versões O Suportadas para a consola Do Gestor](../../../plan-design/configs/supported-operating-systems-consoles.md)de Configuração .

### <a name="unsupported-os-for-site-server"></a>SO não suportado para servidor de site

*Aplica-se a: Site da administração central, site primário, site secundário, consola de Gestor de Configuração, ponto de gestão, ponto de distribuição*

O servidor executa uma versão sistemas osiada.

Para mais informações, consulte as versões De Sistema de Sistema de Sistema de [Configuração suportadas para servidores](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do Gestor de Configuração .

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Função do sistema de site não suportado: fora do ponto de serviço da banda

*Aplica-se a: Sítio Primário*

A função do sistema de site de pontos de banda não está instalada.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Função do sistema do site não suportado: ponto de validação da saúde do sistema

*Aplica-se a: Sítio Primário*

A função do sistema de validação da saúde do sistema não está instalada.

### <a name="unsupported-upgrade-path"></a>Caminho de upgrade não suportado

*Aplica-se a: Site da administração central, local primário*

Todos os servidores do site na hierarquia cumprem a versão mínima do Gestor de Configuração que é necessária para o upgrade.

### <a name="usmt-installed"></a>USMT instalado

*Aplica-se a: Site da administração central, local primário (apenas autónomo)*

Está instalado o componente da Ferramenta de Migração do Estado utilizador (USMT) do Kit de Avaliação e Implementação do Windows (ADK) para windows.

### <a name="validate-fqdn-of-sql-server"></a>Validar fQDN do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

Especificou um FQDN válido para o computador SQL Server.

### <a name="verify-central-administration-site-version"></a>Verifique a versão do site da administração central

*Aplica-se a: Sítio Primário*

O site da administração central tem a mesma versão do Gestor de Configuração.

### <a name="verify-database-consistency"></a>Verificar a consistência da base de dados

*Aplica-se a: Site da administração central, local primário*

Verifica a consistência da base de dados do site no Servidor SQL.  

### <a name="windows-deployment-tools-installed"></a>Ferramentas de implementação do Windows instaladas

*Aplica-se a: Fornecedor SMS*

O componente de ferramentas de implementação do Windows do Windows ADK está instalado.

### <a name="windows-failover-cluster"></a>Cluster de Ativação Pós-falha do Windows

*Aplica-se a: Servidor do site, ponto de gestão, ponto de distribuição*

O servidor com o servidor do site, ponto de gestão ou funções de ponto de distribuição não fazem parte de um Cluster do Windows.

A partir da versão 1810, o processo de configuração do Gestor de Configuração já não bloqueia a instalação da função do servidor do site num computador com a função Windows para o Clusterfailover. O SQL Always On requer esta função, pelo que anteriormente não conseguiu colocar a base de dados do site no servidor do site. Com esta alteração, pode criar um site altamente disponível com menos servidores utilizando o SQL Always On e um servidor de site em modo passivo. Para mais informações, consulte [Opções de Alta Disponibilidade](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE instalado

*Aplica-se a: Fornecedor SMS*

O componente de pré-instalação do Windows Environment (PE) do Windows ADK está instalado.



## <a name="warnings"></a>Avisos

### <a name="active-directory-domain-functional-level"></a>Nível funcional de domínio de diretório ativo

*Aplica-se a: Site da administração central, local primário*

O domínio do Diretório Ativo e o nível funcional da floresta são um mínimo do Windows Server 2008 R2. Para mais informações, consulte [Suporte para domínios de Diretório Ativo](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Direitos administrativos sobre o ponto de distribuição

*Aplica-se a: Ponto de distribuição*

A configuração da conta de utilizador que executa a conta tem direitos **de administrador** sobre o ponto de distribuição.

### <a name="administrative-rights-on-management-point"></a>Direitos administrativos sobre o ponto de gestão

*Aplica-se a: ponto de gestão, ponto de distribuição*

A conta de computador do servidor do site tem direitos **de Administrador** sobre o ponto de gestão e ponto de distribuição.

### <a name="administrative-share-site-system"></a>Partilha administrativa (sistema de site)

*Aplica-se a: Ponto de gestão*

As ações administrativas necessárias estão presentes no computador do sistema do site.

### <a name="application-compatibility"></a>Compatibilidade de aplicações

*Aplica-se a: Site da administração central, local primário*

As aplicações atuais estão em conformidade com o esquema de aplicação.

### <a name="backlogged-inboxes"></a>Caixas de entrada bloqueadas

*Aplica-se a: Site da administração central, local primário*

O servidor do site está a processar caixas de entrada críticas em tempo útil. As caixas de entrada não contêm ficheiros mais antigos do que um dia.

Verifica as seguintes pastas de caixa de entrada:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Para resolver este aviso, verifique se os componentes do sistema de despooler e do programador estão em execução.

### <a name="bits-installed"></a>BITS instalado

*Aplica-se a: Ponto de gestão*

O Serviço de Transferência Inteligente de Fundo (BITS) está instalado e ativado no IIS.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Verifique se o site utiliza o conector de nuvem de preparação de upgrade

*Aplica-se a: Site da administração central, local primário*

O serviço de Preparação de Upgrade está reformado a partir de 31 de janeiro de 2020. Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics é a evolução do Windows Analytics. Para mais informações, consulte [o que é desktop Analytics](../../../../desktop-analytics/overview.md).

Se o site do Gestor de Configuração tiver uma ligação com a Prontidão de Upgrade, tem de o remover e reconfigurar os clientes. Para mais informações, consulte [A ligação de preparação de atualização .](../../../clients/manage/upgrade-readiness.md#bkmk_remove)

Se ignorar este aviso pré-requisito, a configuração do Gestor de Configuração remove automaticamente o conector de preparação de atualização.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Gateway de gestão de nuvem requer autenticação baseada em token ou um ponto de gestão HTTPS

*Aplica-se a: Gateway de gestão de nuvem*

Com algumas versões do Gestor de Configuração, não é possível utilizar um ponto de gestão HTTP com o gateway de gestão de nuvem (CMG). Configure o CMG para HTTPS ou configure o site para HTTP melhorado. Para mais informações, consulte [Plan for cloud management gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Configuração para utilização da memória do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

O Servidor SQL está configurado para uso ilimitado da memória. Configure a memória do Servidor SQL para ter um limite máximo.

### <a name="distribution-point-package-version"></a>Versão pacote de ponto de distribuição

*Aplica-se a: Pontos de distribuição*

Todos os pontos de distribuição do site têm a versão mais recente dos pacotes de distribuição de software.

### <a name="domain-membership-warning"></a>Adesão ao domínio (aviso)

*Aplica-se a: ponto de gestão, ponto de distribuição*

O computador 'Gestor de Configuração' é membro de um domínio Windows.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Exceção de firewall para O Servidor SQL (site primário autónomo)

*Aplica-se a: Sítio primário (apenas autónomo)*

O Windows Firewall está desativado ou existe uma exceção relevante para o Windows Firewall para o Servidor SQL.

Permita que o Sqlservr.exe ou as portas TCP necessárias sejam acedidas remotamente. Por predefinição, o SQL Server ouve na porta TCP 1433, e o Corretor de Serviços de Servidor (SSB) utiliza a porta TCP 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Exceção de firewall para SQL Server para ponto de gestão

*Aplica-se a: Ponto de gestão*

O Windows Firewall está desativado ou existe uma exceção relevante para o Windows Firewall para o Servidor SQL.

### <a name="iis-https-configuration"></a>Configuração IIS HTTPS

*Aplica-se a: ponto de gestão, ponto de distribuição*

O site iIS tem encadernações para o protocolo de comunicação HTTPS.

Quando instalar funções no site que requerem HTTPS, configure as ligações do site IIS no servidor especificado com um certificado de infraestrutura de chave pública válida (PKI).

### <a name="invalid-discovery-records"></a>Registos de descobertas inválidos

*Aplica-se a: site da administração central*

Há registos de descobertas que já não são válidos. Estes registos serão marcados para a eliminação.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*Aplica-se ao site da administração central, site primário, site secundário, consola de Gestor de Configuração, ponto de gestão, ponto de distribuição*

Verifica se mSXML 6.0 ou uma versão posterior está instalada.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>A proteção do acesso à rede (PAN) já não é suportada

*Aplica-se a: Sítio Primário*

Não existem atualizações de software que estejam ativadas para o PAN.

### <a name="ntfs-drive-on-site-server"></a>Unidade NTFS no servidor do site

*Aplica-se a: Sítio Primário*

A unidade do disco está formatada com o sistema de ficheiros NTFS. Para uma melhor segurança, instale os componentes do servidor do site em unidades de disco formatadas com o sistema de ficheiros NTFS.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a>Atualizações de políticas de itens de configuração pendentes

<!--SCCMDocs-pr issue 2814-->

*Aplica-se a: Sítio Primário*

A partir da versão 1806, se estiver a atualizar a partir da versão 1706 ou posterior, poderá ver este aviso se tiver muitas implementações de aplicações e pelo menos uma delas necessitar de aprovação.

Tem duas opções:  

- Ignore o aviso e continue com a atualização. Esta ação causa um maior processamento no servidor do site durante a atualização à medida que processa as políticas. Pode também ver mais carga do processador no ponto de gestão após a atualização.  

- Reveja uma das aplicações que não tem requisitos ou requisitos de SO específicos. Pré-processe parte da carga no servidor do site nessa altura. Reveja **objreplmgr.log**e, em seguida, monitorize o processador no ponto de gestão. Depois de concluído o processamento, atualize o site. Haverá ainda algum processamento adicional após a atualização, mas menos do que se ignorar o aviso com a primeira opção.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Sistema pendente reinicia no servidor Remoto SQL

*Aplica-se a: Versão 1902 e posteriormente, servidor Remoto SQL*

Antes de executar a configuração, outro programa requer que o servidor seja reiniciado.

Para ver se o computador se encontra em estado de reinício pendente, verifica os seguintes locais de registo:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 no servidor do site

*Aplica-se a: Site primário com conector de troca*

O Windows PowerShell 2.0 ou uma versão posterior está instalado no servidor do site para o Conector de Troca de Gestor de Configuração.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Ligação remota ao WMI no local secundário

*Aplica-se a: Local secundário*

A configuração pode estabelecer uma ligação remota ao WMI no servidor de site secundário.

### <a name="schema-extensions"></a>Extensões de esquema

*Aplica-se a: Site da administração central, local primário*

O esquema do Diretório Ativo foi alargado. Se for estendida, a versão das extensões de esquemas que foram usadas.

O Gestor de Configuração não requer extensões de esquema de Diretório Ativo para a instalação do servidor do site. A Microsoft recomenda-os para a utilização completa de todas as funcionalidades do 'Gestor de Configuração'. Para obter mais informações sobre as vantagens de estender o esquema, consulte Prepare O [Diretório Ativo para publicação](../../../plan-design/network/extend-the-active-directory-schema.md)do site .

### <a name="share-name-in-package"></a>Nome da partilha no pacote

*Aplica-se a: Site da administração central, local primário*

Os pacotes não têm caracteres inválidos no nome da partilha, tais como `#` .

### <a name="site-system-to-sql-server-communication"></a>Sistema de site para comunicação SQL Server

*Aplica-se a: Site secundário, ponto de gestão*

A conta que configurapara executar o serviço SQL Server para a instância de base de dados do site tem um nome principal de serviço válido (SPN) em Serviços de Domínio de Diretório Ativo. Registe um SPN válido em Diretório Ativo para apoiar a autenticação kerberos.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a>Limpeza de rastreio do servidor SQL

*Aplica-se a: servidor de base de dados do site*

A partir da versão 1810, verifique se a base de dados do site tem um atraso nos dados de rastreio de alterações SQL.<!--SCCMDocs-pr issue 3023-->  

Verifique manualmente esta verificação executando um procedimento de diagnóstico armazenado na base de dados do site. Primeiro, crie uma [ligação de diagnóstico](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) à base de dados do seu site. O método mais fácil é usar o Editor de Consulta de Motor de Base de Dados do SQL Server Management Studio e ligar-se a `admin:<instance name>` .

Numa janela de consulta de ligação de administrador dedicada, execute os seguintes comandos:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Dependendo do tamanho da sua base de dados e do tamanho do atraso, este procedimento armazenado pode funcionar em poucos minutos ou várias horas. Quando a consulta estiver concluída, você vê duas secções de dados relacionados com o atraso. Primeiro olhar para **CT_Days_Old.** Este valor diz-lhe a idade (dias) da entrada mais antiga na sua tabela syscommittab. Devem ser cinco dias, que é o valor padrão do Gestor de Configuração. Não altere este valor predefinido. Em momentos de processamento ou replicação de dados pesados, a entrada mais antiga em syscommittab pode ser superior a cinco dias. Se este valor for superior a sete dias, ecorra numa limpeza manual dos dados de rastreio de alterações.  

Para limpar os dados de rastreio de alterações, execute o seguinte comando na ligação de administração dedicada:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Este comando inicia uma limpeza de syscommittab e todas as mesas laterais associadas. Pode funcionar em vários minutos ou várias horas. Para monitorizar o seu progresso, consulte a vista **vLogs.** Para ver o progresso atual, execute a seguinte consulta:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

<!--SCCMDocs-pr issue 3094-->

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Atualizar o Cliente Nativo do Servidor SQL pode exigir um reinício, o que pode afetar o processo de instalação do site.

Esta verificação garante que o servidor do site tem uma versão suportada do Cliente Nativo SQL. A verificação prévia não verifica a versão do Cliente Nativo SQL em sistemas de sites remotos.

A versão mínima é SQL 2012 SP4 `11.*.7001.0` ( ). Esta versão SQL Native Client suporta TLS 1.2. Para obter mais informações, veja os seguintes artigos:

- [Suporte TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Como ativar o TLS 1.2 para o Gestor de Configuração](../../../plan-design/security/enable-tls-1-2.md)  

O Gestor de Configuração utiliza o Cliente Nativo do Servidor SQL nas seguintes funções do sistema do site:<!-- SCCMDocs issue 1150 -->

- Servidor da base de dados do site
- Servidor do site: site da administração central, site primário ou site secundário
- Ponto de gestão
- Ponto de gestão de dispositivos
- Ponto de Migração de Estado
- Fornecedor de SMS
- Ponto de atualização de software
- Ponto de distribuição com multicast ativado
- Ponto de serviço de atualização de Inteligência de Ativos
- Ponto do Reporting Services
- Serviço web de catálogo de aplicações
- Ponto de inscrição
- Ponto de Endpoint Protection
- Ponto de ligação de serviço
- Ponto de registo de certificados
- Ponto de serviço de armazém de dados

### <a name="sql-server-process-memory-allocation"></a>Alocação de memória de processo do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

O SQL Server reserva um mínimo de 8 GB de memória para o site da administração central e o local primário, e um mínimo de 4 GB de memória para o local secundário.

Para mais informações, consulte [como configurar opções de memória utilizando o Estúdio de Gestão de Servidores SQL](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Esta verificação não é aplicável ao SQL Server Express num site secundário. Esta edição está limitada a 1 GB de memória reservada.  

### <a name="sql-server-security-mode"></a>Modo de segurança do Servidor SQL

*Aplica-se a: servidor de base de dados do site*

O Servidor SQL está configurado para a segurança de autenticação do Windows.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versão os sistema de site não suportada SISTEMA OS para upgrade

*Aplica-se a: Sítio Primário, Local secundário*

As funções do sistema do site, para além dos pontos de distribuição, estão instaladas em servidores que executam o Windows Server 2012 ou posteriormente.

Para obter mais informações, consulte [sistemas operativos suportados para servidores](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do Gestor de Configuração .

> [!NOTE]  
> Este controlo não pode resolver o estado das funções do sistema do site instaladas no Azure ou para o armazenamento em nuvem utilizado pela Microsoft Intune. Ignore os avisos para estes papéis como falsos positivos.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>O kit de ferramentas de avaliação de upgrade não é suportado

*Aplica-se a: Site da administração central, local primário*

O Kit de Ferramentas de Avaliação de Upgrade não está instalado. Para mais informações, consulte [funcionalidades removidas e depreciadas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verifique as permissões do servidor do site para publicar no Ative Directory

*Aplica-se a: Site da administração central, local primário, local secundário*

A conta do computador para o servidor do site tem permissões **de Controlo Completo** para o recipiente de Gestão de **Sistemas** no domínio do Diretório Ativo.

Para mais informações, consulte Prepare o [Diretório Ativo para a publicação](../../../plan-design/network/extend-the-active-directory-schema.md)do site.

> [!NOTE]  
> Se verificar manualmente as permissões, pode ignorar este aviso.

### <a name="windows-remote-management-winrm-v11"></a>Gestão remota do Windows (WinRM) v1.1

*Aplica-se a: Site primário, consola de Gestor de Configuração*

O WinRM 1.1 está instalado no servidor principal do site ou no computador de consola do Gestor de Configuração para executar a consola de gestão fora de banda.

O WinRM é instalado automaticamente com todas as versões suportadas atualmente pelo Windows. Para mais informações, consulte [instalação e configuração para gestão remota do Windows](https://docs.microsoft.com/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>WSUS no servidor do site

*Aplica-se a: Site da administração central, local primário*

Uma versão suportada dos Serviços de Atualização do Servidor do Windows (WSUS) está instalada no servidor do site.

Quando utilizar um ponto de atualização de software num servidor diferente do servidor do site, tem de instalar a Consola de Administração WSUS no servidor do site. Para mais informações sobre o WSUS, consulte os Serviços de [Atualização](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)do Servidor do Windows .
