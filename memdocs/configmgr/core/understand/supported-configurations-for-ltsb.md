---
title: 'Configurações suportadas para o LTSB '
titleSuffix: Configuration Manager
description: Compreenda quais os sistemas operativos e produtos dependentes que funcionam com o Ramo de Manutenção a Longo Prazo do Gestor de Configuração do Centro de Sistemas.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 39039347361076ae7c8491f95419187d0af9da85
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722621"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurações suportadas para o ramo de manutenção a longo prazo do gestor de configuração do centro de sistema

*Aplica-se a: System Center Configuration Manager (Ramo de Manutenção a Longo Prazo)*

Utilize as informações neste tópico para entender quais os sistemas operativos e dependências do produto suportados pelo Ramo de Manutenção a Longo Prazo (LTSB) do Gestor de Configuração.
Se não for indicado o contrário neste ou nos tópicos específicos ltSB, as mesmas configurações e limitações aplicáveis à versão 1606 do Ramo Atual aplicam-se ao LTSB.  Quando ocorrerem conflitos, utilize a informação que se aplica à edição que está a utilizar. Tipicamente, o LTSB é mais limitado do que o Ramo Atual.

## <a name="general-statement-of-support"></a>Declaração geral de apoio
Os seguintes produtos e tecnologias são suportados por este ramo de Gestor de Configuração. No entanto, a sua inclusão neste conteúdo não expressa uma extensão do suporte a qualquer produto ou versão para além do ciclo de vida individual de suporte desse produto. Os produtos que estão para além do seu ciclo de vida de suporte não são suportados para uso com o Gestor de Configuração. Para mais informações, visite o site [microsoft Support Lifecycle](https://go.microsoft.com/fwlink/p/?LinkId=208270) e leia o [FAQ](https://go.microsoft.com/fwlink/p/?LinkId=31976)da Política de Suporte ao Vida da Microsoft .

Além disso, os produtos e versões de produtos que não estão listados nos seguintes tópicos não são suportados a menos que tenham sido anunciados no [Enterprise Mobility + Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitações para apoio futuro:** O LTSB tem suporte limitado para futuros sistemas operativos de servidores e clientes e dependências de produtos. A lista de plataformas para o LTSB é fixada para a vida útil do lançamento:

**Janelas:**
- Apenas são suportadas atualizações de qualidade e segurança para windows.
- Não é adicionado suporte para as atuais sucursais (CB), sucursais atuais para negócios (CBB) ou LTSB do Windows 10.
- Sem suporte para novas versões principais do Windows Server.

**Servidor SQL:**
- Apenas atualizações de qualidade e segurança, ou pequenas atualizações como pacotes de serviço, são suportadas para o SQL Server.
- Sem suporte para novas versões principais do SQL Server.  

## <a name="site-systems-and-servers"></a>Sistemas e servidores do site
O LTSB suporta a utilização dos seguintes sistemas operativos do Windows como sistemas de sites.  Cada sistema operativo tem os mesmos requisitos e limitações que a mesma entrada em [sistemas operativos suportados para servidores](../plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do site .  Por exemplo, a instalação do Server Core do Windows 2012 R2 deve ser uma versão x64, é suportada apenas para hospedar um ponto de distribuição, e não suporta PXE ou Multicast.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Profissional, Empresa
- A instalação do Núcleo do Servidor do Windows 2012
- A instalação do Núcleo do Servidor do Windows 2012 R2

## <a name="client-management"></a>Gestão de clientes
As seguintes secções identificam os sistemas operativos do cliente que pode gerir com o LTSB. O LTSB não suporta a adição de novos sistemas operativos como clientes apoiados.

### <a name="windows-computers"></a>Computadores Windows
Pode utilizar o LTSB para gerir os seguintes sistemas operativos do Windows com o software cliente do Gestor de Configuração que está incluído no 'Gestor de Configuração'. Para mais informações, consulte [como implementar clientes para computadores Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Nota 1)
- Windows Server 2012 (x64): Standard, Datacenter (Nota 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Profissional, Empresa
- A instalação do Núcleo do Servidor do Windows 2012 R2 (x64) (Nota 2)
- A instalação do Server Core do Windows Server 2012 (x64) (Nota 2)

**(Nota 1)** As versões do Datacenter são suportadas, mas não certificadas para O Gestor de Configuração.  
**(Nota 2)** Para suportar a instalação de push do cliente, o computador que executa esta versão do sistema operativo deve executar o serviço de função de Servidor de Ficheiros para a função de servidor de Ficheiros e Serviços de Armazenamento. Para obter informações sobre a instalação de funcionalidades do Windows num computador Core do Servidor, consulte a instalação de [funções e funcionalidades do servidor num servidor de núcleo](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) de servidor na biblioteca TechNet do Windows Server 2012.

### <a name="windows-embedded"></a>Windows Embedded
Pode utilizar o LTSB para gerir os seguintes dispositivos Windows Embedded instalando o software cliente no dispositivo.  Para mais informações, consulte [Planplanning para implementação de clientes em dispositivos Incorporados](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)windows .

**Requisitos e limitações:**  

-   Todas as funcionalidades do cliente são suportadas em sistemas Windows Embedded suportados que não têm filtros de escrita ativados.  

-   Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades, com exceção da gestão de energia:  

    -   Filtros de escrita melhorados (EWF)    

    -   Filtros de escrita baseados em ficheiros RAM (FBWF)    

    -   Filtros de escrita unificados (UWF)  

-   O Catálogo de Aplicações não é suportado para qualquer dispositivo Incorporado no Windows.  

-   Antes de poder monitorizar o malware detetado em dispositivos Incorporados do Windows com base no Windows XP, tem de instalar o pacote de scripts WMI do Microsoft Windows no dispositivo incorporado. Utilize o Designer de Alvo incorporado do Windows para instalar este pacote. O *WBEMDISP. DLL* e *WBEMDISP. Os* ficheiros TLB devem existir e ser registados na pasta %windir%\System32\WBEM no dispositivo incorporado para garantir que o malware detetado é relatado.  

**Sistemas operativos suportados:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Indústria (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 com SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Pode gerir os dispositivos CE do Windows com o cliente legado do dispositivo móvel Do Gestor de Configuração que está incluído no Gestor de Configuração.  

**Requisitos e limitações:**  

-   O cliente do dispositivo móvel requer 0,78 MB de espaço de armazenamento para instalar o cliente. Um dispositivo móvel pode exigir até 256 KB de espaço de armazenamento adicional para iniciar sessão.    

-   As funcionalidades para estes dispositivos móveis variam consoante a plataforma e o tipo de cliente. Para obter informações sobre o tipo de funções de gestão que o Gestor de Configuração suporta para um cliente legado de dispositivo móvel, consulte Escolha uma solução de gestão de [dispositivos para O Gestor](../plan-design/choose-a-device-management-solution.md)de Configuração .  

**Sistemas operativos suportados:**  

-   Windows CE 7.0 (processadores ARM e X86)  

**As linguagens suportadas incluem:**  
-   Chinês (simplificado e tradicional)    
-   Inglês (E.U.A.)    
-   Francês (França)    
-   Alemão    
-   Italiano    
-   Japonês  
-   Coreano  
-   Português (Brasil)  
-   Russo  
-   Espanhol (Espanha)  

### <a name="mac-computers"></a>Computadores Mac  
 Pode utilizar o LTSB para gerir computadores Mac OS X com o cliente do Gestor de Configuração para Mac.

O pacote de instalação do cliente Mac não é fornecido com os meios de Configuração Manager. Pode descarregá-lo como parte do download "Clientes para Sistemas Operativos Adicionais" do [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184).  

O suporte para sistemas operativos Mac está limitado aos indicados nesta secção. O suporte não inclui sistemas operativos adicionais que possam ser suportados por uma futura atualização aos pacotes de instalação de clientes Mac para a Filial Atual.

Para mais informações, consulte [como implementar clientes para Macs](../clients/deploy/deploy-clients-to-macs.md).

**Versões suportadas:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX
Pode utilizar o LTSB para gerir servidores Linux e UNIX com o cliente do Gestor de Configuração para o Linux e uniX.

Os pacotes de instalação de clientes Linux e UNIX não são fornecidos com os meios de configuração do Gestor de Configuração. Pode descarregá-los como parte do download "Clientes para Sistemas Operativos Adicionais" do [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, a transferência do cliente inclui o script de instalação que gere a instalação do cliente em cada computador.

O suporte para sistemas operativos Linux e UNIX está limitado aos indicados nesta secção. O suporte não inclui sistemas operativos adicionais que possam ser suportados por uma futura atualização para pacotes de clientes Linux e UNIX para a Current Branch.

**Requisitos e limitações:**  

-   Para rever as dependências de ficheiros do sistema operativo para o cliente do Linux e da UNIX, consulte [os pré-requisitos para](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)a implementação do cliente no Linux e nos Servidores UNIX .  
-   Para uma visão geral das capacidades de gestão suportadas para computadores que executam o Linux ou o UNIX, consulte [como implementar clientes para servidores UNIX e Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   Para versões suportadas de Linux e UNIX, a versão listada inclui todas as versões menores subsequentes. Por exemplo, quando o suporte é indicado para a versão 6 do CentOS, isto também inclui qualquer versão menor subsequente do CentOS 6, como o CentOS 6.3. Da mesma forma, quando o suporte está listado para um sistema operativo que utiliza pacotes de serviços, como o SUSE Linux Enterprise Server 11 SP1, o suporte inclui pacotes de serviçosubsequentes para essa versão do sistema operativo.
-   Para obter informações sobre os pacotes de instalação de clientes e o Agente Universal, consulte [como implementar clientes para servidores UNIX e Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Versões suportadas:**   
As seguintes versões são suportadas utilizando o ficheiro .tar indicado.  
### <a name="aix"></a>AIX  

|Versão|Ficheiro|  
|-|-|  
|Versão 5.3 (Potência)|ccm-Aix53ppc. &lt;construir\>.alcatrão|  
|Versão 6.1 (Potência)|ccm-Aix61ppc. &lt;construir\>.alcatrão|  
|Versão 7.1 (Potência)|ccm-Aix71ppc. &lt;construir\>.alcatrão|  

### <a name="centos"></a>CentOS  

|Versão|Ficheiro|  
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="debian"></a>Debian  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 8 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 8 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="hp-ux"></a>HP-UX  

|Versão|Ficheiro|  
|-|-|  
|Versão 11iv2 IA64|ccm-HpuxB.11.23i64. &lt;construir\>.alcatrão|  
|Versão 11iv2 PA-RISC|ccm-HpuxB.11.23PA. &lt;construir\>.alcatrão|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64. &lt;construir\>.alcatrão|  
|Versão 11iv3 PA-RISC|ccm-HpuxB.11.31PA. &lt;construir\>.alcatrão|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Ficheiro|  
|-|-|  
|Versão 4 x86|ccm-RHEL4x86. &lt;construir\>.alcatrão|  
|Versão 4 x64|ccm-RHEL4x64. &lt;construir\>.alcatrão|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="solaris"></a>Solaris  

|Versão|Ficheiro|   
|-|-|  
|Versão 9 SPARC|ccm-Sol9sparc. &lt;construir\>.alcatrão|  
|Versão 10 x86|ccm-Sol10x86. &lt;construir\>.alcatrão|  
|Versão 10 SPARC|ccm-Sol10sparc. &lt;construir\>.alcatrão|  
|Versão 11 x86|ccm-Sol11x86. &lt;construir\>.alcatrão|  
|Versão 11 SPARC|ccm-Sol11sparc. &lt;construir\>.alcatrão|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Ficheiro|  
|-|-|  
|Versão 9 x86|ccm-SLES9x86. &lt;construir\>.alcatrão|  
|Versão 10 SP1 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 10 SP1 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 11 SP1 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 11 SP1 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 12 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="ubuntu"></a>Ubuntu  

|Versão|Ficheiro|    
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 10.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 12.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 12.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 14.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 14.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

### <a name="exchange-server-connector"></a>Conector do Exchange Server
 O LTSB suporta uma gestão limitada de dispositivos que se ligam à instância do Exchange Server, sem instalar o software do cliente. Para mais informações, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Requisitos e limitações:**  

-   O Gestor de Configuração oferece uma gestão limitada para dispositivos móveis. A gestão limitada está disponível quando utiliza o conector Exchange Server para dispositivos compatíveis com o Exchange Ative Sync (EAS) que se ligam a um servidor que executa o Exchange Server ou o Exchange Online.  

-   Para obter mais informações sobre as funções de gestão que o Gestor de Configuração suporta para dispositivos móveis que o conector do Exchange Server gere, consulte Escolha uma solução de gestão de [dispositivos para O Gestor](../plan-design/choose-a-device-management-solution.md)de Configuração .  

**Versões suportadas do Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> O LTSB não suporta a gestão de dispositivos que se conectam através de um serviço online, como o Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Consola do Configuration Manager
O LTSB suporta os seguintes sistemas operativos para executar a consola 'Gestor de Configuração'. Cada computador que acolhe a consola deve ter uma versão mínima .NET Framework de 4.5.2, com exceção do Windows 10, que requer um mínimo de .NET Framework 4.6.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Profissional, Empresa


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versões SQL Server suportadas para a base de dados do site e ponto de reporte
O LTSB suporta as seguintes versões do SQL Server para alojar a base de dados do site e o ponto de reporte. Para cada versão suportada, aplicam-se ao LTSB os mesmos requisitos e limitações de configuração que aparecem no [Suporte para as versões Do Servidor SQL](../plan-design/configs/support-for-sql-server-versions.md) para o Ramo Atual.  Isto inclui a utilização de um Cluster de ServidorEs SQL, ou de um grupo de disponibilidade sQL Server AlwaysOn.  

**Versões suportadas:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Suporte para domínios do Active Directory
Todos os sistemas de site LTSB devem ser membros de um domínio de Diretório Ativo Windows suportado. O suporte para domínios de Diretório Ativo tem os mesmos requisitos e limitações que os que aparecem no [Suporte para domínios de Diretório Ativo,](../plan-design/configs/support-for-active-directory-domains.md)mas está limitado aos seguintes níveis funcionais de domínio:

**Níveis suportados:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Tópicos de apoio adicionais aplicáveis ao Ramo de Manutenção a Longo Prazo
As informações nos seguintes tópicos da Sucursal atual aplicam-se ao LTSB:
- [Dimensionamento e números da escala](../plan-design/configs/size-and-scale-numbers.md)
- [Pré-requisitos do site e sistema de sites](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Opções de elevada disponibilidade](../servers/deploy/configure/high-availability-options.md)
- [Hardware recomendado](../plan-design/configs/recommended-hardware.md)
- [Suporte para funcionalidades e redes do Windows](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Apoio a ambientes de virtualização](../plan-design/configs/support-for-virtualization-environments.md)
