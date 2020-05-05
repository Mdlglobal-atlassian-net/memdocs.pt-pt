---
title: Clientes e dispositivos suportados
titleSuffix: Configuration Manager
description: Saiba qual as versões OS Do Gestor de Configuração suportapara clientes e dispositivos.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 57c60fcdadf3e58b59d33ecf2753789122a38ecc
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078690"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versões de SO suportadas para clientes e dispositivos para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta a instalação de software cliente em computadores Windows e macOS.  

## <a name="general-requirements-and-limitations"></a>Requisitos e limitações gerais

Reveja os seguintes requisitos e limitações para todos os clientes:

- Alterar o tipo de arranque ou **iniciar sessão como** configurações para qualquer serviço de 'Gestor de Configuração' não é suportado. Esta alteração pode impedir que os serviços-chave funcionassem corretamente.

## <a name="windows-computers"></a>Computadores Windows  

Para gerir as seguintes versões do Windows OS, utilize o cliente incluído no 'Gestor de Configuração'. Para mais informações, consulte [como implementar clientes para computadores Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Versões de Os do cliente suportadas

- **Windows 10**  

    Para obter informações mais detalhadas, consulte [suporte para o Windows 10](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Profissional, Empresa

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[O Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) é um serviço de virtualização de computadores e aplicações que funciona no Microsoft Azure. A partir da versão 1906, utilize o Gestor de Configuração para gerir estes dispositivos virtuais que executam o Windows em Azure.

Semelhante a um servidor de terminal, alguns destes dispositivos virtuais permitem múltiplas sessões de utilizador ativas simultâneas. Para ajudar no desempenho do cliente, o Gestor de Configuração desativa agora as políticas do utilizador em qualquer dispositivo que permita estas múltiplas sessões de utilizador. Mesmo que ative as políticas do utilizador, o cliente desativa-as por padrão nestes dispositivos, que incluem servidores multissessões e terminais do Windows 10 Enterprise.

O cliente só desativa a política do utilizador quando deteta este tipo de dispositivo durante uma nova instalação. Para um cliente existente deste tipo que atualiza para esta versão, o comportamento anterior persiste. Num dispositivo existente, configura a definição da política do utilizador mesmo que detete que o dispositivo permite várias sessões de utilizador.

Se necessitar da política do utilizador neste cenário e aceitar qualquer impacto potencial de desempenho, utilize um dos seguintes métodos para ativar a política do utilizador:

- Na versão 1910 e mais tarde, utilize [as definições do cliente.](../../clients/deploy/configure-client-settings.md) No grupo **Política do Cliente,** configure a seguinte definição: **Ative a política do utilizador para várias sessões de utilizador**.<!-- 4737447 -->

- Na versão 1906, utilize o Gestor de Configuração SDK com a [classe WMI](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md)do servidor SMS_PolicyAgentConfig . Desloque a nova `PolicyEnableUserPolicyOnTS` propriedade para `true`.

> [!Note]  
> Não pode usar a cogestão com um cliente que executa a multi-sessão do Windows 10 Enterprise. <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>Versões de Os do servidor suportadas

- **Windows Server 2019**: Standard, <sup> [Datacenter Nota 1](#bkmk_note1)</sup>  
    (Começando com a versão 1806 do Gestor de Configuração.)

- **Windows Server 2016**: Standard, <sup> [Datacenter Nota 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup, Standard  

- **Windows Server 2012 R2** (x64): Standard, <sup> [Datacenter Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, <sup> [Datacenter Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

As seguintes versões referem-se especificamente à instalação do Núcleo do Servidor do SISTEMA. <sup>[Nota 3](#bkmk_note3)</sup>  

As versões semi-anuais do Canal do Windows Server são instalações do Server Core, como o Windows Server, versão 1809. Como cliente do Gestor de Configuração, são suportados da mesma forma que a versão semi-anual do Windows 10 associada. Para mais informações, consulte [suporte para o Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup> [Nota 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup> [Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup> [Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup> [Nota 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>Nota 1

O Gestor de Configuração testa e suporta as edições do Windows Server Datacenter, mas não está oficialmente certificado para o Windows Server. O suporte de hotfix do Gestor de Configuração não é oferecido para problemas específicos da Edição de Datacenter do Windows Server. Para obter mais informações sobre o programa de certificação do Windows Server, consulte o [Catálogo do Servidor do Windows](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a>Nota 2

Para apoiar a [instalação push](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)do cliente, adicione o serviço de Servidor de Ficheiros da função de servidor de Serviços de Arquivo e Armazenamento. Para obter mais informações sobre a instalação de funcionalidades do Windows no Núcleo do Servidor, consulte [Instalar funções, serviços de funções e funcionalidades utilizando cmdlets Windows PowerShell](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="note-3"></a><a name="bkmk_note3"></a>Nota 3

A nova aplicação do Software Center não é suportada em nenhuma versão do Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Computadores incorporados ao Windows  

Gerencie os dispositivos Incorporados do Windows instalando o cliente do Gestor de Configuração no dispositivo. Para mais informações, consulte [Planplanning para implementação de clientes em dispositivos Incorporados](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)windows .  

### <a name="requirements-and-limitations"></a>Requisitos e limitações

- Todas as funcionalidades do cliente são suportadas em sistemas Windows Embedded que não têm filtros de escrita ativados.  

- Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades, com exceção da gestão de energia:  

  - Filtros de escrita melhorados (EWF)

  - Filtros de escrita baseados em ficheiros RAM (FBWF)

  - Filtros de escrita unificados (UWF)  

- O catálogo de aplicações não é suportado para qualquer dispositivo Windows Embedded.  

### <a name="supported-os-versions"></a>Versões de Os Suportadas  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de manutenção a longo prazo (LTSC). Para mais informações, consulte a [Visão Geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Indústria** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 com SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Computadores CE do Windows

Gerencie os dispositivos CE do Windows com o cliente legado do dispositivo móvel Do Gestor de Configuração que está incluído no Gestor de Configuração.  

### <a name="requirements-and-limitations"></a>Requisitos e limitações

- O cliente do dispositivo móvel requer 0,78 MB de espaço de armazenamento para instalação. O sessão pode exigir até 256 KB de espaço adicional de armazenamento.

- As funcionalidades para estes dispositivos móveis variam consoante a plataforma e o tipo de cliente. Para obter informações sobre quais as funções de gestão, consulte [Escolha uma solução](../choose-a-device-management-solution.md)de gestão de dispositivos .  

### <a name="supported-os-versions"></a>Versões de Os Suportadas

- Windows CE 7.0 (processadores ARM e X86)  

    > [!Note]
    > O suporte é depreciado para o Windows CE 7.0 no Gestor de Configuração. Para mais informações, consulte [itens removidos e depreciados para clientes do Gestor](../changes/deprecated/removed-and-deprecated-client.md)de Configuração .

#### <a name="supported-languages-include"></a>Línguas apoiadas incluem

- Chinês (simplificado e tradicional)

- Inglês (E.U.A.)

- Francês (França)

- Alemão

- Italiano

- Japonês  

- Coreano  

- Português (Brasil)  

- Russo  

- Espanhol (Espanha)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Atualizações de segurança estendidas e gestor de configuração

O programa [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) é uma opção de último recurso para os clientes que precisam de executar certos produtos legados da Microsoft após o fim do suporte. Por exemplo, o Windows 7. Inclui atualizações de segurança críticas e/ou importantes (conforme definido pelo [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)durante um máximo de três anos após a data de fim do suporte alargado do produto.

Os produtos que estão para além do seu ciclo de vida de suporte não são suportados para uso com O Gestor de Configuração. Isto inclui todos os produtos abrangidos pelo programa ESU. As atualizações de segurança lançadas no âmbito do programa ESU serão publicadas nos Serviços de Atualização do Servidor do Windows (WSUS). Estas atualizações aparecerão na consola 'Gestor de Configuração'. Embora os produtos abrangidos pelo programa ESU deixem de ser suportados para utilização com o Gestor de Configuração, a [versão mais recente do atual ramo](../../servers/manage/updates.md#version-details) do Gestor de Configuração pode ser utilizada para implementar e instalar atualizações de segurança do Windows lançadas no âmbito do programa. A versão mais recente também pode ser utilizada para implementar o Windows 10 para dispositivos que executam o Windows 7.

As funcionalidades de gestão de clientes não relacionadas com a gestão de atualizações de software windows ou a implementação de OS deixarão de ser testadas nos sistemas operativos abrangidos pelo programa ESU e não garantimos que continuarão a funcionar. É altamente recomendado atualizar ou migrar para uma versão atual dos sistemas operativos o mais rapidamente possível para receber apoio de gestão de clientes.

## <a name="mac-computers"></a>Computadores Mac  

Gerencie os computadores Apple Mac com o cliente do Gestor de Configuração para o macOS.  

O pacote de instalação do cliente macOS não é fornecido com os meios de Configuração Manager. Descarregue-o a partir do Microsoft Download Center, [Microsoft Endpoint Configuration Manager - macOS Client (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850).  

Para mais informações, consulte [como implementar clientes para Macs](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Requisitos e limitações

- A instalação ou execução do cliente do Gestor de Configuração para o macOS em computadores sob uma conta que não seja raiz não é suportada. Ao fazê-lo, os serviços-chave podem funcionar corretamente.  

### <a name="supported-versions"></a>Versões suportadas

- **macOS Catalina (10.15)** (requer versão de site do Gestor de Configuração 1910 ou posterior, e cliente do Gestor de Configuração para a versão 5.0.8742.1000 ou posterior)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX  

> [!Important]  
> A versão 1902 do Gestor de Configuração deixa cair o suporte para linux e UNIX como cliente. A deprecation foi anunciada com a [versão 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Os pacotes de instalação de clientes Linux e UNIX não são fornecidos com os meios de configuração do Gestor de Configuração. Baixe os **Clientes para sistemas operativos adicionais** a partir do [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script que gere a instalação do cliente em cada computador.  

### <a name="requirements-and-limitations"></a>Requisitos e limitações

- Para rever as dependências de ficheiros OS para o cliente para linux e UNIX, consulte [pré-requisitos para a implementação do cliente nos servidores Linux e UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Para uma visão geral das capacidades de gestão suportadas para linux ou UNIX, consulte [como implementar clientes para servidores UNIX e Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- Para versões suportadas de Linux e UNIX, a versão listada inclui todas as versões menores subsequentes. Por exemplo, a versão 6 do CentOS inclui o CentOS 6.3. Da mesma forma, o suporte para um OS que utiliza pacotes de serviço (como o SUSE Linux Enterprise Server 11 SP1) inclui pacotes de serviço subsequentes para essa versão OS.  

- Para obter informações sobre os pacotes de instalação de clientes e o Agente Universal, consulte [como implementar clientes para servidores UNIX e Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Versões suportadas

As seguintes versões são suportadas utilizando o ficheiro .tar indicado.  

#### <a name="aix"></a>AIX  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 6.1 (Potência)|ccm-Aix61ppc. &lt;construir\>.alcatrão|  
|Versão 7.1 (Potência)|ccm-Aix71ppc. &lt;construir\>.alcatrão|  

#### <a name="centos"></a>CentOS  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

#### <a name="debian"></a>Debian  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 8 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 8 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

#### <a name="hp-ux"></a>HP-UX  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64. &lt;construir\>.alcatrão|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 5 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 5 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 6 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 6 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 7 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

#### <a name="solaris"></a>Solaris  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 10 x86|ccm-Sol10x86. &lt;construir\>.alcatrão|  
|Versão 10 SPARC|ccm-Sol10sparc. &lt;construir\>.alcatrão|  
|Versão 11 x86|ccm-Sol11x86. &lt;construir\>.alcatrão|  
|Versão 11 SPARC|ccm-Sol11sparc. &lt;construir\>.alcatrão|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 10 SP1 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 10 SP1 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 11 SP1 x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 11 SP1 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 12 x64|ccm-Universalx64. &lt;construir\>.alcatrão|  

#### <a name="ubuntu"></a>Ubuntu  

|Versão|Arquivo TAR|  
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 10.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 12.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 12.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 14.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 14.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  
|Versão 16.04 LTS x86|ccm-Universalx86. &lt;construir\>.alcatrão|  
|Versão 16.04 LTS x64|ccm-Universalx64. &lt;construir\>.alcatrão|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a>NO LOCAL MDM

O Gestor de Configuração tem capacidades incorporadas para gerir dispositivos móveis que estão no local sem instalar software de cliente. Para mais informações, consulte [Gerir dispositivos móveis com infraestrutura no local.](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)  

### <a name="supported-operating-systems"></a>Sistemas operativos suportados

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de manutenção a longo prazo (LTSC). Para mais informações, consulte a [Visão Geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Equipa do Windows 10 para surface hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!Note]
    > O suporte é depreciado para Windows 10 Mobile e Windows 10 Mobile Enterprise em 'Configuração Manager'. Para mais informações, consulte [itens removidos e depreciados para clientes do Gestor](../changes/deprecated/removed-and-deprecated-client.md)de Configuração .


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a>Conector de servidor de troca  

O Gestor de Configuração suporta uma gestão limitada de dispositivos que se ligam ao seu Servidor de Intercâmbio, sem instalar o cliente do Gestor de Configuração. Para mais informações, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Versões suportadas do Exchange Server

- **Exchange Online (Office 365)**: Esta versão inclui a Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** ou **Exchange Server 2010 SP2**
