---
title: Requisitos de infraestrutura osd
titleSuffix: Configuration Manager
description: Conheça as dependências e requisitos externos e de produto para a implementação do OS no Gestor de Configuração
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34c803cb2b43a2c69cee4c16f5029474e318eb2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724434"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Requisitos de infraestrutura para implantação de OS em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A implantação de OS no Gestor de Configuração tem dependências externas, bem como dependências dentro do produto. Use este artigo para ajudá-lo a preparar a infraestrutura para implantação de SO.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a>Dependências externas ao Gestor de Configuração  

Esta secção fornece informações sobre ferramentas externas, kits de instalação e versões DE SO que são necessárias para implementar sistemas operativos no Gestor de Configuração.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  

O Windows Assessment and Deployment Kit (ADK) é um conjunto de ferramentas e documentação que suportam a configuração e implementação do Windows. O Gestor de Configuração utiliza o Windows ADK para automatizar ações como instalar o Windows, capturar imagens e migrar perfis e dados dos utilizadores.  

Para obter mais informações, veja os artigos seguintes:  

- [Cenários do Windows ADK para Windows 10 para Profissionais de TI](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Transferir o Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Certifique-se de que descarrega tanto o **Windows ADK para windows 10** como o **addon Windows PE para o ADK**.

- [Suporte para o Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Sistema de sites
O Windows ADK é um pré-requisito para os seguintes servidores de sistemas de sites:

- O servidor do site de alto nível na hierarquia  

- O servidor do site de cada site primário na hierarquia  

- Todas as instâncias do Provedor de SMS  


> [!NOTE]  
> Instale manualmente o Windows ADK em cada servidor do site antes de instalar o site do Gestor de Configuração.  

#### <a name="windows-adk-features"></a>Funcionalidades do Windows ADK
Instale as seguintes funcionalidades do Windows ADK:  

-   User State Migration Tool (USMT)  

    > [!Note]  
    > UsMT não é necessário no Provedor de SMS.

-   Ferramentas de Implementação do Windows  

-   Ambiente de Pré-instalação do Windows (Windows PE)  

    > [!Important]  
    > A partir da versão 1809 do Windows 10, o Windows PE é um instalador separado. Caso contrário, não há diferença funcional.<!--SCCMDocs-pr issue 2908-->  

Para obter uma lista das versões do ADK do Windows 10 que pode utilizar com diferentes versões do 'Gestor de Configuração', consulte [suporte para windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>User State Migration Tool (USMT)  

O Gestor de Configuração utiliza um pacote USMT que inclui os ficheiros de origem USMT 10 para capturar e restaurar o estado de utilizador como parte da sua implementação de SO. Configuração do Gestor de Configuração no site de alto nível cria automaticamente o pacote USMT. UsMT 10 captura o estado de utilizador do Windows 7, Windows 8, Windows 8.1 e Windows 10.  

Para obter mais informações, veja os artigos seguintes:  

- [Cenários Comuns de Migração do USMT 10](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Gerir o estado do utilizador](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

O Windows PE é utilizado para imagens de arranque para iniciar um computador. É uma versão do Windows com serviços limitados que é usado durante a pré-instalação e implementação do Windows. A lista que se segue inclui as versões suportadas do Windows ADK para O Gestor de Configuração, ramo atual:  

#### <a name="windows-adk-version"></a>Versão do Windows ADK  
Windows ADK para windows 10. Para mais informações, consulte [Suporte para Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Versões Windows PE para imagens de arranque personalizáveis a partir da consola Do Gestor de Configuração  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Versões suportadas pelo Windows PE para imagens de arranque não personalizáveis a partir da consola Do Gestor de Configuração  
Windows PE 3.1<sup>1</sup> e Windows PE 5  

<sup>1</sup> Só pode adicionar uma imagem de arranque ao Gestor de Configuração quando for baseada no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Baixe o suplemento Windows AIK para windows 7 SP1 a partir do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

Por exemplo, quando tiver o Gestor de Configuração, pode personalizar imagens de boot do Windows ADK para windows 10 (com base no Windows PE 10) a partir da consola 'Gestor de Configuração'. No entanto, enquanto as imagens de arranque baseadas no Windows PE 5 são suportadas, deve personalizá-las a partir de um computador diferente e utilizar a versão do DISM que está instalada com o Windows ADK para o Windows 8. Em seguida, adicione a imagem de boot à consola 'Gestor de Configuração'. Para mais informações com os passos para personalizar uma imagem de arranque (adicione componentes e controladores opcionais), ative o suporte de comando à imagem de arranque, adicione a imagem de arranque à consola Do Gestor de Configuração e atualize os pontos de distribuição com a imagem de arranque, consulte [Personalizar imagens](../get-started/customize-boot-images.md)de arranque . Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

A WSUS é necessária para o ponto de atualização de software, que é necessário para instalar atualizações de software durante a implementação do OS. Para mais informações, consulte [Instale um ponto](../../sum/get-started/install-a-software-update-point.md)de atualização de software .


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informação Internet) nos servidores do sistema de sites  

O IIS é necessário para o ponto de distribuição, ponto de migração do Estado e ponto de gestão. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>Serviços de implementação do Windows (WDS)  

Na versão 1802 e anterior, o WDS é necessário para implementações de PXE. A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS. Para mais informações, consulte os Serviços de [Implementação](#BKMK_WDS) do Windows neste artigo. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP (Dynamic Host Configuration Protocol)  

O protocolo DHCP é necessário para implementações de PXE. É necessário ter um servidor DHCP a funcionar com um anfitrião ativo para implementar sistemas operativos com PXE. Para obter mais informações sobre as implementações do PXE, consulte [use O PXE para implementar o Windows sobre a rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos suportados e configurações do disco rígido  

Para obter mais informações sobre as versões OS e configurações de discos rígidos que são suportadas pelo Gestor de Configuração quando implementa sistemas operativos, consulte [sistemas operativos suportados](#BKMK_SupportedOS) e [configurações de discos suportados](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Controladores de dispositivo do Windows  

Os controladores de dispositivos Windows podem ser utilizados quando instalar o SISTEMA no computador de destino. Também são usados quando executa o Windows PE numa imagem de arranque. Para mais informações, consulte [Gerir os condutores](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a>Dependências do Gestor de Configuração  

Esta secção fornece informações sobre os pré-requisitos de implementação do Sistema de Configuração OS.  


### <a name="os-image"></a>Imagem de OS  

As imagens osso no Gestor de Configuração são armazenadas no formato de ficheiro suver (WIM) do Windows Imaging. Representam uma coleção comprimida de ficheiros e pastas de referência. Estas imagens são necessárias para instalar e configurar com sucesso um SISTEMA num computador. Para mais informações, consulte [Gerir imagens do OS](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catálogo de controladores  

Para implantar um controlador de dispositivo, importe o controlador do dispositivo, ative-o e disponibilize-o num ponto de distribuição a que o cliente do Gestor de Configuração possa aceder. Para mais informações sobre o catálogo do condutor, consulte [Gerir os condutores](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Ponto de gestão  

Pontos de gestão transferem informações entre clientes e o site do Gestor de Configuração. O cliente usa um ponto de gestão para executar a sequência de tarefas para completar a implementação do SO. Para obter mais informações sobre sequências de tarefas, consulte [considerações de Planeamento para automatizar tarefas](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Ponto de distribuição  

Os pontos de distribuição são usados na maioria das implementações para armazenar os dados que são usados para implementar um SISTEMA, como a imagem ou os pacotes de condutor. As sequências de tarefas normalmente recuperam dados de um ponto de distribuição para implantar o SISTEMA. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdos, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  


### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição com PXE ativado  

Para implementar implementações iniciadas pelo PXE, configure um ponto de distribuição para aceitar pedidos de PXE dos clientes. Para mais informações, consulte [Configure um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição com multicast ativado  

Para otimizar as suas implementações de SO utilizando multicast, configure um ponto de distribuição para suportar o multicast. Para mais informações, consulte [Configure um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Ponto de Migração de Estado  

Quando capturar e restaurar os dados do estado do utilizador para implementações lado a lado e atualizar, configure um ponto de migração estatal para armazenar os dados do estado do utilizador noutro computador.  

Para obter mais informações sobre como configurar o ponto de migração de estado, veja [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Para obter mais informações sobre como capturar e restaurar o estado do utilizador, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services  

Para utilizar relatórios do Gestor de Configuração para implementações de OS, instale e configure um ponto de reporte. Para mais informações, consulte [Introdução a relatórios.](../../core/servers/manage/introduction-to-reporting.md)  


### <a name="security-permissions-for-os-deployments"></a>Permissões de segurança para implementações de OS  

A função de segurança do Gestor de **Implementação** do Sistema Operativo é um papel incorporado que não se pode mudar. No entanto, é possível copiar a função, efetuar alterações e, em seguida, guardar estas alterações como uma nova função de segurança personalizada. Aqui estão algumas das permissões que se aplicam diretamente às implementações de SO:  

- **Pacote de Imagem de Arranque**: Criar, Eliminar, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Âmbito de Segurança  

- **Controladores de Dispositivo**: Criar, Eliminar, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório  

- **Pacote de Controlador**: Criar, Eliminar, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Âmbito de Segurança  

- **Imagem do Sistema Operativo**: Criar, Eliminar, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Âmbito de Segurança  

- **Pacote de atualização do sistema operativo**: Criar, Eliminar, Modificar, Modificar pasta, mover objeto, ler, definir âmbito de segurança  

- **Pacote de Sequência de Tarefas**: Criar, Criar Suportes de Dados da Sequência de Tarefas, Eliminar, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório, Definir Âmbito de Segurança  

Para mais informações, consulte [Criar funções de segurança personalizadas.](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  


### <a name="security-scopes-for-os-deployments"></a>Âmbitos de segurança para implementações de OS  

Utilize âmbitos de segurança para fornecer aos utilizadores administrativos o acesso aos objetos securáveis utilizados nas implementações de S, tais como imagens de SO e boot, pacotes de controladores e pacotes de sequência de tarefas. Para obter mais informações, veja [Âmbitos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Serviços de Implementação do Windows  

Na versão 1802 e anterior, os Serviços de Implementação do Windows (WDS) devem ser instalados no mesmo servidor que os pontos de distribuição que configura para suportar PXE ou multicast. O WDS está incluído no sistema operativo. Para implementações de PXE, o WDS é o serviço que executa o arranque PXE. Quando o ponto de distribuição é instalado e ativado para PXE, o Gestor de Configuração instala um fornecedor em WDS que utiliza as funções de arranque WDS PXE.  

A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS. Para mais informações, consulte o **serviço de resposta Enable a PXE sem** a opção de Serviço de Implementação do Windows na [Instalação e configurar pontos](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)de distribuição .


> [!NOTE]  
>  Se o servidor necessitar de um reinício, a instalação de WDS poderá falhar. 


### <a name="wds-requirements"></a>Requisitos de WDS  

-   A instalação WDS no servidor requer que o administrador seja membro do grupo de Administradores locais.  

-   O servidor WDS tem de ser membro de um domínio do Active Directory ou de um controlador de domínio para um domínio do Active Directory. Todas as configurações de domínio e de floresta de Windows suportam WDS.  

-   Se o fornecedor estiver instalado num servidor remoto, instale o WDS no servidor do site e no fornecedor remoto.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Considerações sobre quando tiver o WDS e DHCP no mesmo servidor  

Se planeia co-hospedar o ponto de distribuição num servidor que executa o DHCP, considere os seguintes problemas de configuração:  

-   Tem de ter um servidor DHCP funcional com um âmbito ativo. O WDS utiliza o PXE, que requer um servidor DHCP.  

-   É necessário um servidor DNS para executar o WDS.  

-   As seguintes portas UDP devem estar abertas no servidor WDS:  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Se for necessária autorização do DHCP no servidor, necessita da porta cliente DHCP 68 para estar aberta no servidor.  

-   DHCP e WDS exigem a porta número 67. Se co-hospedar o WDS e o DHCP, pode mover o DHCP ou o ponto de distribuição configurado para O PXE para um servidor separado. Ou, pode utilizar o seguinte procedimento para configurar o servidor WDS para ouvir uma porta diferente.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar o servidor WDS para ouvir uma porta diferente  

1.  Modifique a seguinte chave de registo:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Defina o valor de registo **UseDHCPPorts** para **0**.  

3.  Para efetivar a nova configuração, execute o seguinte comando no servidor:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> Na versão 1810 e anterior, não é suportado para usar o resposta PXE sem WDS em servidores que também estão executando um servidor DHCP.
>
> A partir da versão 1902, quando ativa um xeque PXE num ponto de distribuição sem o Windows Deployment Service, pode agora estar no mesmo servidor que o serviço DHCP. Para mais informações, consulte [Configure pelo menos um ponto de distribuição para aceitar pedidos de PXE](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a>Sistemas operativos suportados  

Todos os sistemas operativos Windows listados como clientes suportados em [sistemas operativos suportados para clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são suportados para implementação de OS.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a>Configurações de discos suportados  

As combinações de configuração de disco rígido nos computadores de referência e destino que são suportados para a implementação do Sistema de Configuração OS são mostradas na tabela seguinte:  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples num disco dinâmico|Volume simples num disco dinâmico|  

O Gestor de Configuração suporta a captura de uma imagem de OS apenas a partir de computadores configurados com volumes simples. Não há suporte para as seguintes configurações de disco rígido:  

-   Volumes expandidos  

-   Volumes repartidos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

A tabela seguinte mostra uma configuração adicional de disco rígido nos computadores de referência e destino que não é suportado com a implementação do Sistema de Configuração O.  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  



## <a name="next-steps"></a>Passos seguintes

- [Preparar funções do sistema de sites para implementações de SO](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Preparar a implementação do SO](../get-started/prepare-for-operating-system-deployment.md)
