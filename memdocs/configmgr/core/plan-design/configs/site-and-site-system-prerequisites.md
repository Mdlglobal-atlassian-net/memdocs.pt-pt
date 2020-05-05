---
title: Pré-requisitos do site
titleSuffix: Configuration Manager
description: Aprenda a configurar um computador Windows como um servidor de sistema de configuração do gestor de configuração.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719191"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Pré-requisitos do sistema de site e site para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os computadores baseados no Windows requerem configurações específicas para suportar a sua utilização como servidores do sistema de configuração do gestor de configuração.

Para alguns produtos, como o Windows Server Update Services (WSUS) para o ponto de atualização de software, é necessário consultar a documentação do produto para identificar pré-requisitos adicionais e limitações para utilização. Apenas estão incluídas configurações que se aplicam diretamente para utilização com o Gestor de Configuração.

Para obter mais informações sobre o .NET Framework, consulte [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a>Requisitos e limitações gerais

Os seguintes requisitos aplicam-se a todos os servidores do sistema do site:

- Cada servidor do sistema de site deve utilizar um SISTEMA de 64 bits. A única exceção é a função do sistema de site de pontos de distribuição, que pode instalar em alguns sistemas operativos de 32 bits.  

- Os sistemas de site não são suportados nas instalações do Server Core de qualquer sistema operativo. Uma exceção é que as instalações do Server Core são suportadas para a função do sistema de site de pontode distribuição. Para obter mais informações, consulte [sistemas operativos suportados para servidores](supported-operating-systems-for-site-system-servers.md)do sistema do Gestor de Configuração .  

- Depois de instalado um servidor de sistema de site, não é suportado para alterar:  

    - O nome de domínio do domínio onde o computador do sistema do site está localizado (também chamado de **renome de domínio).**  

    - A filiação ao computador.  

    - O nome do computador.  

    Se tiver de alterar algum destes itens, retire primeiro a função do sistema do site do computador. Em seguida, reinstale a função após a alteração estar completa. Para alterações que afetem o servidor do site, desinstale primeiro o site. Em seguida, reinstale o site após a alteração estar completa.  

- As funções do sistema do site não são suportadas numa instância de um cluster do Windows Server. A única exceção é o servidor de base de dados do site. Para mais informações, consulte [Utilize um cluster de servidor SQL para a base](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)de dados do site do Gestor de Configuração .  

    A partir da versão 1810, o processo de configuração do Gestor de Configuração já não bloqueia a instalação da função do servidor do site num computador com a função Windows para o Clusterfailover. O SQL Always On requer esta função, pelo que anteriormente não conseguiu colocar a base de dados do site no servidor do site. Com esta alteração, pode criar um site altamente disponível com menos servidores utilizando o SQL Always On e um servidor de site em modo passivo. Para mais informações, consulte [Opções de Alta Disponibilidade](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Não é suportado para alterar o tipo de arranque ou as definições de "Iniciar sessão como" para qualquer serviço de Gestor de Configuração. Se o fizer, poderá evitar que os principais serviços funcionassem corretamente.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a>Pré-requisitos para o Windows Server 2012 e posteriores sistemas operativos  

Consulte as principais secções deste artigo para obter os pré-requisitos específicos para servidores e funções do sistema de site no Windows Server 2012 e posteriormente:

- [Site da administração central e servidores de site primário](#bkmk_2012sspreq)
- [Servidor do Site Secundário](#bkmk_2012secpreq)
- [Servidor de base de dados](#bkmk_2012dbpreq)
- [Servidor sms provider](#bkmk_2012smsprovpreq)
- [Ponto de Web site do Catálogo de Aplicações](#bkmk_2012acwspreq)
- [Ponto de serviço Web do Catálogo de Aplicações](#bkmk_2012ACwsitepreq)
- [Ponto de sincronização da Inteligência de Ativos](#bkmk_2012AIpreq)
- [Ponto de registo de certificados](#bkmk_2012crppreq)
- [Ponto de distribuição](#bkmk_2012dppreq)
- [Ponto de Endpoint Protection](#bkmk_2012EPPpreq)
- [Ponto de inscrição](#bkmk_2012Enrollpreq)
- [Ponto proxy de registo](#bkmk_2012EnrollProxpreq)
- [Ponto de estado de contingência](#bkmk_2012FSPpreq)
- [Ponto de gestão](#bkmk_2012MPpreq)
- [Ponto de serviços de reporte](#bkmk_2012RSpoint)
- [Ponto de ligação de serviço](#bkmk_SCPpreq)
- [Ponto de atualização de software](#bkmk_2012SUPpreq)
- [Ponto de Migração de Estado](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a>Site da administração central e servidores de site primário

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

- Compressão de Diferencial Remota  

- Quando utilizar um ponto de atualização de software num servidor diferente do servidor do site, instale a Consola de Administração WSUS no servidor do site.

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Antes de instalar ou atualizar um site de administração central ou um site primário, instale a versão do Windows Assessment and Deployment Kit (ADK) que é exigida pela versão do Gestor de Configuração para a qual está a instalar ou a atualizar. Para mais informações, consulte [o Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Para obter mais informações sobre este requisito, consulte [os requisitos de infraestrutura para a implantação do OS](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Visual C++ Redistribuável  

- O Gestor de Configuração instala o Pacote Redistribuível Microsoft Visual C++ 2013 em cada computador que instala um servidor de site.  

- Os sites da administração central e os sites primários requerem tanto as versões x86 como x64 do ficheiro redistribuível aplicável.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a>Servidor de site secundário

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

- Compressão de Diferencial Remota  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistribuável

- O Gestor de Configuração instala o Pacote Redistribuível Microsoft Visual C++ 2013 em cada computador que instala um servidor de site.  

- Os sites secundários requerem apenas a versão x64.  

### <a name="default-site-system-roles"></a>Funções de sistema de site padrão  

- Por padrão, um site secundário instala um ponto de **gestão** e um ponto de **distribuição**.  

- Certifique-se de que o servidor de site secundário satisfaz os pré-requisitos para estas funções do sistema do site.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a>Servidor de base de dados  

### <a name="remote-registry-service"></a>Serviço de Registo Remoto  

- Durante a instalação do site Do Gestor de Configuração, ative o serviço **de Registo Remoto** no computador que acolhe a base de dados do site.  

### <a name="sql-server"></a>SQL Server  

- Antes de instalar um site de administração central ou site primário, instale uma versão suportada do SQL Server para alojar a base de dados do site. Para mais informações, consulte [as versões Suportadas Do Servidor SQL](support-for-sql-server-versions.md).  

- Antes de instalar um site secundário, pode instalar uma versão suportada do Servidor SQL.  

- Se optar por que o Gestor de Configuração instale o SQL Server Express como parte da instalação do site secundário, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a>Servidor sms provider  

### <a name="windows-adk"></a>Windows ADK

- O computador onde instala uma instância do Fornecedor SMS deve ter a versão necessária do Windows ADK que a versão do Gestor de Configuração está a instalar ou a atualizar para exigir. Para mais informações, consulte [o Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Para obter mais informações sobre este requisito, consulte [os requisitos de infraestrutura para a implantação do sistema operativo.](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- Se estiver a utilizar o serviço de [administração,](../../../develop/adminservice/overview.md)o servidor que acolhe a função de Fornecedor SMS requer .NET 4.5 ou mais tarde  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > A versão 1810 do Gestor de Configuração requer .NET 4.5.2 ou mais tarde.

- Servidor Web (IIS): Todos os fornecedores tentam instalar o serviço de [administração](../../../develop/adminservice/overview.md). Este serviço tem uma dependência do IIS para ligar um certificado à porta HTTPS 443. O Gestor de Configuração utiliza APIs IIS para verificar a configuração deste certificado. Se configurar o site para [HTTP melhorado,](../hierarchy/enhanced-http.md)o Gestor de Configuração utiliza APIs IIS para ligar o certificado gerado pelo site. A partir da versão 2002, o site utiliza automaticamente o certificado auto-assinado do site.

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a>Ponto de site do catálogo de aplicações  

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS  

- Características comuns do HTTP:  

    - Documento Predefinido  

    - Conteúdo Estático  

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Segurança:  

    - Autenticação do Windows  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a>Ponto de serviço web de catálogo de aplicações  

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

- ASP.NET 4.5:  

    - Ativação HTTP (e opções automaticamente selecionadas)  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Características comuns do HTTP:  

    - Documento Predefinido  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

    - .NET Extensibility 4.5  

### <a name="computer-memory"></a>Memória do computador  

- O computador que acolhe esta função de sistema de site deve ter um mínimo de 5% da memória disponível do computador gratuitamente para permitir que a função do sistema do site processe os pedidos.  

- Quando esta função do sistema do site é colocalizada com outra função do sistema do site que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a>Ponto de sincronização da Inteligência de Ativos  

### <a name="net-framework"></a>.NET Framework

Instale uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a>Ponto de registo de certificado  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework

    - Ativação HTTP  

### <a name="net-framework"></a>.NET Framework

Instale uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

    - Compatibilidade com WMI do IIS 6  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a>Ponto de distribuição  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- Compressão de Diferencial Remota  

#### <a name="iis-configuration"></a>Configuração IIS

- Desenvolvimento de Aplicações:  

    - Extensões ISAPI  

- Segurança:  

    - Autenticação do Windows  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

    - Compatibilidade com WMI do IIS 6  

### <a name="powershell"></a>PowerShell  

- No Windows Server 2012 ou mais tarde, é necessário powerShell 3.0 ou 4.0 antes de instalar o ponto de distribuição.  

### <a name="visual-c-redistributable"></a>Visual C++ Redistribuável

- O Gestor de Configuração instala o Pacote Redistribuível Microsoft Visual C++ 2013 em cada computador que acolhe um ponto de distribuição.  

- A versão instalada depende da plataforma do computador (x86 ou x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Pode utilizar um serviço de cloud no Microsoft Azure para acolher um ponto de distribuição.  

### <a name="to-support-pxe-or-multicast"></a>Para suportar PXE ou multicast  

- Ative um ressurgimento de PXE num ponto de distribuição sem o Serviço de Implementação do Windows.  

- Instale e configure a função do Windows Deployment Services (WDS) Windows Server.  

    > [!NOTE]  
    > O WDS instala e configura automaticamente quando configura um ponto de distribuição para suportar O PXE ou multicast num servidor que executa o Windows Server 2012 ou mais tarde.  

- Para um ponto de distribuição multicast, certifique-se de que o Cliente Nativo do Servidor SQL está instalado e atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Para mais informações, consulte [Instalar e configurar pontos](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)de distribuição .

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando o ponto de distribuição transfere o conteúdo, transfere-se utilizando o Serviço de **Transferência Inteligente de Fundo** (BITS) incorporado no Windows. A função de ponto de distribuição não requer a instalação da funcionalidade opcional de extensão do servidor BITS IIS, uma vez que o cliente não faz o upload de informação para o mesmo.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a>Ponto de proteção de pontofinal  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server  

- .NET Framework 3.5

- Funcionalidades do Windows Defender (Windows Server 2016 ou posterior)  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a>Ponto de matrícula  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

    - Ativação HTTP (e opções automaticamente selecionadas)  

    - ASP.NET 4.5  

    - Serviços da Fundação de Comunicação do Windows (WCF)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

> [!Note]
> Quando esta função do sistema de site se instala, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2. Esta instalação pode colocar o servidor num estado pendente de reinicialização. Se estiver pendente um reboot para a .NET Framework, as aplicações .NET podem falhar até que o servidor reinicie e a instalação termine.  

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Características comuns do HTTP:  

    - Documento Predefinido  

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

    - .NET Extensibility 4.5  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

### <a name="computer-memory"></a>Memória do computador

- O computador que acolhe esta função de sistema de site deve ter um mínimo de 5% da memória disponível do computador gratuitamente para permitir que a função do sistema do site processe os pedidos.  

- Quando esta função do sistema do site é colocalizada com outra função do sistema do site que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a>Ponto de procuração de inscrição  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

> [!Note]
> Quando esta função do sistema de site se instala, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2. Esta instalação pode colocar o servidor num estado pendente de reinicialização. Se estiver pendente um reboot para a .NET Framework, as aplicações .NET podem falhar até que o servidor reinicie e a instalação termine.  

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Características comuns do HTTP:  

    - Documento Predefinido  

    - Conteúdo Estático  

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Segurança:  

    - Autenticação do Windows  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

### <a name="computer-memory"></a>Memória do computador

- O computador que acolhe esta função de sistema de site deve ter um mínimo de 5% da memória disponível do computador gratuitamente para permitir que a função do sistema do site processe os pedidos.  

- Quando esta função do sistema do site é colocalizada com outra função do sistema do site que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a>Ponto de estado de recuo

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- Extensões do servidor BITS (e opções selecionadas automaticamente) ou Serviços de Transferência Inteligente de Fundo (BITS) (e opções automaticamente selecionadas)

#### <a name="iis-configuration"></a>Configuração IIS

A configuração padrão IIS é necessária com as seguintes adições:  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a>Ponto de gestão  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- Extensões do servidor BITS (e opções selecionadas automaticamente) ou Serviços de Transferência Inteligente de Fundo (BITS) (e opções automaticamente selecionadas)  

### <a name="net-framework"></a>.NET Framework

Instale uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Desenvolvimento de Aplicações:  

    - Extensões ISAPI  

- Segurança:  

    - Autenticação do Windows  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

    - Compatibilidade com WMI do IIS 6  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a>Ponto de serviços de reporte  

### <a name="net-framework"></a>.NET Framework

Instale uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Instale e configure pelo menos uma instância do Servidor SQL para suportar os Serviços de Reporte do Servidor SQL antes de instalar o ponto de reporte.  

- A instância que utiliza para os Serviços de Reporte de Servidores SQL pode ser a mesma que utiliza para a base de dados do site.  

- Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center, desde que os outros produtos do System Center não tenham restrições para partilhar a instância do SQL Server.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a>Ponto de ligação de serviço  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

> [!Note]
> Quando esta função do sistema de site se instala, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2. Esta instalação pode colocar o servidor num estado pendente de reinicialização. Se estiver pendente um reboot para a .NET Framework, as aplicações .NET podem falhar até que o servidor reinicie e a instalação termine.  

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistribuável

- O Gestor de Configuração instala o Pacote Redistribuível Microsoft Visual C++ 2013 em cada computador que acolhe um ponto de distribuição.  

- A função do sistema do site requer a versão x64.  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a>Ponto de atualização de software  

### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

É necessária a configuração padrão Do IIS.

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Instale o serviço de atualização do servidor do Windows Windows Num computador antes de instalar um ponto de atualização de software.  

- Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .  

> [!NOTE]  
> Quando utilizar um Ponto de Atualização de Software num servidor diferente do servidor do site, tem de instalar a Consola de Administração WSUS no servidor do site.

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a>Ponto de migração do Estado

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Funções e funcionalidades do Windows Server

- .NET Framework 3.5

    - Ativação HTTP (e opções automaticamente selecionadas)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Ative a função Windows para .NET Framework 3.5.

Instale também uma versão suportada da versão .NET Framework 4.5 ou posterior. A partir da versão 1906, o Gestor de Configuração suporta .NET Framework 4.8.

> [!Note]
> Quando esta função do sistema de site se instala, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2. Esta instalação pode colocar o servidor num estado pendente de reinicialização. Se estiver pendente um reboot para a .NET Framework, as aplicações .NET podem falhar até que o servidor reinicie e a instalação termine.  

Para obter mais informações sobre as versões .NET Framework, consulte os seguintes artigos:

- [.NET Versões e dependências do quadro](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configuração IIS

- Características comuns do HTTP:  

    - Documento Predefinido  

- Desenvolvimento de Aplicações:  

    - ASP.NET 3.5 (e opções selecionadas automaticamente)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (e opções automaticamente selecionadas)  

    - .NET Extensibility 4.5  

- Compatibilidade de Gestão IIS 6:  

    - Compatibilidade com Metabase do IIS 6  

### <a name="sql-server-native-client"></a>Cliente nativo do servidor SQL

Quando instala um novo site, o Gestor de Configuração instala automaticamente o Cliente Nativo do Servidor SQL como um componente redistribuível. Depois de instalado o site, o Gestor de Configuração não atualiza o Cliente Nativo do Servidor SQL. Certifique-se de que este componente está atualizado. Para mais informações, consulte [verificações pré-requisitos - SQL Server Client Nativo](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

