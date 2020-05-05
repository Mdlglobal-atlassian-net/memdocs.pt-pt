---
title: Passos de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre os passos que pode adicionar a uma sequência de tarefas do Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 385a7222b33275951de294554a870d8e490a5ddc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719093"
---
# <a name="task-sequence-steps"></a>Passos de sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os seguintes passos de sequência de tarefapodem ser adicionados a uma sequência de tarefas do Gestor de Configuração. Para mais informações, consulte [Utilize o editor da sequência de tarefas](task-sequence-editor.md).  

## <a name="common-settings"></a>Definições comuns

As seguintes definições são comuns a todas as etapas de sequência de tarefas:

### <a name="properties-for-all-steps"></a>Propriedades para todos os passos

- **Nome**: O editor da sequência de tarefas requer que especifique um nome curto para descrever este passo. Quando adiciona um novo passo, o editor da sequência de tarefas define o nome para o Tipo por padrão. O comprimento do **nome** não pode exceder 50 caracteres.  

- **Descrição**: Opcionalmente, especifique informações mais detalhadas sobre este passo. O comprimento da **descrição** não pode exceder 256 caracteres.  

O resto deste artigo descreve as outras definições no separador **Propriedades** para cada passo de sequência de tarefas.

### <a name="options-for-all-steps"></a>Opções para todos os passos

- **Desative este passo**: A sequência de tarefas salta este passo quando funciona num computador. O ícone deste passo está acinzentado no editor da sequência de tarefas.  

- **Continue a error**: Se ocorrer um erro durante a execução do passo, a sequência de tarefas continua. Para mais informações, consulte [as considerações de Planeamento para automatizar tarefas.](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups)  

- **Adicionar Condição**: A sequência de tarefas avalia estas declarações condicionais para determinar se corre o passo. Para um exemplo de utilização de uma variável de sequência de tarefas como condição, consulte [Como utilizar variáveis](using-task-sequence-variables.md#bkmk_access-condition)de sequência de tarefas . Para mais informações sobre as condições, consulte o editor da [sequência de tarefas - Condições](task-sequence-editor.md#bkmk_conditions).

As secções abaixo para passos específicos de sequência de tarefas descrevem outras configurações possíveis no separador **Opções.**



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a>Aplicar Imagem de Dados

Utilize este passo para copiar a imagem de dados para a divisória de destino especificada.  

Este passo é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens,** e selecione **Aplicar imagem de dados**.

### <a name="variables-for-apply-data-image"></a>Variáveis para aplicar imagem de dados

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Cmdlets para aplicar imagem de dados

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps)
- [New-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps)
- [Remover CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps)
- [Set-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps)

### <a name="properties-for-apply-data-image"></a>Propriedades para aplicar imagem de dados

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="image-package"></a>Pacote de Imagem

**Selecione Navegar** para especificar o **Pacote de Imagem** utilizado por esta sequência de tarefas. Selecione o pacote que pretende instalar na caixa de diálogo **Selecionar um Pacote**. A parte inferior da caixa de diálogo exibe as informações de propriedade associadas para cada pacote de imagem existente. Utilize a lista pendente para selecionar a **Imagem** que pretende instalar a partir do **Pacote de Imagem** selecionado.  

> [!NOTE]  
> Esta ação de sequência de tarefas trata a imagem como um ficheiro de dados. Esta ação não faz qualquer configuração para iniciar a imagem como um SISTEMA.  

#### <a name="destination"></a>Destino

Configure uma das seguintes opções:

- **Próxima partição disponível**: Utilize a próxima partição sequencial que um **sistema operativo de aplicação** ou um passo de imagem de **dados** na sequência de tarefas ainda não tem como alvo.  

- **Disco específico e partição:** Selecione o número **do disco** (começando com 0) e o número **de partição** (começando com 1).  

- **Letra de unidade lógica específica**: Especifique a letra de **unidade** que o Windows PE atribui à divisória. Esta carta de unidade pode ser diferente da carta de unidade atribuída pelo sistema operativo recentemente implantado.  

- **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Esta variável é tipicamente definida na secção Avançada da caixa de diálogo **Divisória Properties** para o passo de sequência de tarefas **formato e de divisão.**  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Elimine todo o conteúdo na partição antes de aplicar a imagem  

Especifica que a sequência de tarefas elimina todos os ficheiros da divisória do alvo antes de instalar a imagem. Ao não apagar o conteúdo da partição, esta ação pode ser utilizada para aplicar conteúdo adicional a uma partição previamente direcionada.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a>Aplicar pacote de motorista  

Utilize este passo para descarregar todos os controladores na embalagem do controlador e instalá-los no Sistema Operativo Windows.

O passo de sequência de tarefas **Aplicar Pacote de Controlador** torna todos os controladores de dispositivo num pacote de controlador disponíveis para serem utilizados pelo Windows. Adicione este passo entre o **Sistema Operativo Aplicar** e configurar os **passos Windows e ConfigMgr** para disponibilizar os controladores da embalagem para windows. O passo de sequência de tarefas **Aplicar Pacote de Controlador** também é útil em cenários de implementação de suportes de dados autónomos.  

Coloque condutores de dispositivos semelhantes num pacote de condutor e distribua-os nos pontos de distribuição apropriados. Por exemplo, coloque todos os condutores de um fabricante num pacote de condutor. Em seguida, distribua o pacote para pontos de distribuição onde os computadores associados podem aceder-lhes.

O passo **do Pacote do Condutor Aplicável** é útil para meios autónomos. Este passo também é útil para instalar um conjunto específico de controladores. Este tipo de controladores inclui dispositivos que o Windows não deteta, como impressoras de rede.  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **Controladores,** e selecione Aplique o **Pacote do Condutor**.

> [!TIP]
> Para obter uma visão geral dos controladores no Gestor de Configuração, consulte Utilize sequências de [tarefas para instalar controladores](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Utilize o pré-cache de conteúdo para descarregar uma embalagem de controlador aplicável antes de um utilizador instalar a sequência de tarefas. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Variáveis para aplicar pacote de motorista

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OsdInstallDriversAdicionações](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Cmdlets para aplicar pacote de motorista

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Pacote Get-CMTSStepApplyDriverpackage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Pacote new-CMTSStepApplyDriverpackage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Pacote de condutor de condutor de condutor de remove-CMTSStepApply](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Pacote set-CMTSStepApplyDriverpackage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps)

### <a name="properties-for-apply-driver-package"></a>Propriedades para aplicar pacote de motorista

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="driver-package"></a>Pacote de controladores

Especifique a embalagem do condutor que contém os controladores necessários. **Selecione Navegar** para lançar a caixa de diálogo **Select a Package.** Selecione um pacote de motorista existente para aplicar. A parte inferior da caixa de diálogo exibe as propriedades do pacote associado.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Instale o pacote do controlador através do DISM em execução com opção de recurse

Selecione esta `/recurse` opção para adicionar o parâmetro à linha de comando DISM quando o Windows aplicar a embalagem do controlador.

Quando ativa esta opção, também pode especificar parâmetros adicionais da linha de comando DISM. Utilize a variável de sequência de [tarefas OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) para incluir mais opções. Para mais informações, consulte as opções de [linha de comando DoDM do Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Selecionar o controlador de armazenamento em massa no pacote que tem de ser instalado antes da configuração em sistemas operativos anteriores ao Windows Vista

Especifique quaisquer controladores de armazenamento em massa necessários para instalar um SISTEMA clássico.  

##### <a name="driver"></a>Controlador

Selecione o ficheiro do controlador de armazenamento em massa para instalar antes da instalação de um SISTEMA clássico. A lista de abandono suvaria a partir do pacote especificado.  

##### <a name="model"></a>Modelo

Especifique o dispositivo crítico de arranque que é necessário para as implementações pré-Windows Vista OS.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido

Esta opção permite que o Windows instale controladores sem assinatura digital.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a>Aplicar Definições de Rede  

Utilize este passo para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta apropriado. O Windows Setup utiliza este ficheiro de resposta durante a ação **'Configurar Windows' e ConfigMgr.**  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Definições**, e selecione **'Aplicar Definições de rede**.

> [!NOTE]
> Se incluir várias instâncias deste passo numa sequência de tarefas, as condições não se aplicam. As definições do último exemplo deste passo na sequência de tarefas são aplicadas ao dispositivo. Para contornar este comportamento, inclua cada passo num grupo separado com condições no grupo.

### <a name="variables-for-apply-network-settings"></a>Variáveis para aplicar definições de rede

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Cmdlets para aplicar definições de rede

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [New-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Eliminação CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Set-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps)

### <a name="properties-for-apply-network-settings"></a>Propriedades para aplicar definições de rede

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="join-a-workgroup"></a>Aderir a um grupo de trabalho

Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Introduza o nome do grupo de trabalho na linha **Grupo de Trabalho**. O valor que a sequência de **definições** de rede de captura captura pode sobrepor-se a este valor.

#### <a name="join-a-domain"></a>Aderir a um domínio

Selecione esta opção para associar o computador de destino ao domínio especificado. Especifique ou navegue `fabricam.com`no domínio, como . Especifique ou navegue para um caminho de Protocolo de Acesso ao Diretório Leve (LDAP) para uma unidade organizacional. Por exemplo: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Conta

Selecione **Definir** para especificar uma conta com as permissões necessárias para juntar o computador ao domínio. Na caixa de diálogo **da Conta utilizador do Windows,** introduza o nome do utilizador no seguinte formato: `Domain\User`. Para mais informações, consulte a [conta de adesão ao Domínio.](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)

#### <a name="adapter-settings"></a>Definições da placa

Especifique as configurações de rede para cada placa de rede no computador. Selecione **Novo** para abrir a caixa de diálogo **definições** de rede e, em seguida, especificar as definições de rede.

- Se utilizar também o passo de Definições de **Rede de Captura,** a sequência de tarefas aplica as definições previamente capturadas ao adaptador de rede.
- Se a sequência de tarefas não tiver capturado previamente as definições de rede, aplica as definições que especifica neste passo.
- A sequência de tarefas aplica estas definições aos adaptadores de rede na ordem de enumeração do dispositivo Windows.  
- A sequência de tarefas não aplica imediatamente as definições que especifica neste passo para o computador.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a>Aplicar imagem do sistema operativo  

Utilize este passo para instalar um SISTEMA no computador de destino.

Após o funcionamento da ação do **Sistema Operativo Aplicar,** define a variável **OSDTargetSystemDrive** para a letra de unidade da divisória que contém os ficheiros OS.  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens,** e selecione **Aplicar imagem do sistema operativo**.

> [!TIP]
> A começar pelo Windows 10, versão 1709, os meios de comunicação incluem várias edições. Quando configurar uma sequência de tarefas para utilizar um pacote de atualização de OS ou imagem de OS, certifique-se de selecionar uma [edição suportada](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Utilize o pré-cache de conteúdo para descarregar um pacote de atualização de OS aplicável antes de um utilizador instalar a sequência de tarefas. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).
>
> O passo **de configuração Windows e ConfigMgr** inicia a instalação do Windows.

### <a name="variables-for-apply-os-image"></a>Variáveis para aplicar imagem de OS

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OsdTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Cmdlets para aplicar imagem osso

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Novo CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Remover CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Set-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps)

### <a name="behaviors-for-apply-os-image"></a>Comportamentos para aplicar imagem de OS

Este passo executa diferentes ações dependendo se utiliza uma imagem de OS ou um pacote de upgrade de OS.  

#### <a name="os-image-actions"></a>Ações de imagem do OS

O passo **de imagem do sistema operativo aplicar** executa as seguintes ações ao utilizar uma imagem de OS:  

1. Elimine todos os conteúdos no volume visado, exceto ficheiros na pasta especificada pela variável ** \_SMSTSUserStatePath.**  

2. Extrair o conteúdo do ficheiro .wim especificado para a divisória de destino especificada.  

3. Prepare o ficheiro de resposta:  

    1. Crie um novo ficheiro de resposta de configuração do Windows (sysprep.inf ou unattend.xml) para o SISTEMA implantado.  

    2. Fundir quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

4. Copie os carregadores de boot do Windows na divisória ativa.  

5. Detete a bota.ini ou a Base de Dados de Configuração de Arranque (BCD) para fazer referência ao OS recém-instalado.  

#### <a name="os-upgrade-package-actions"></a>Ações de pacotes de upgrade de OS

O passo **de imagem do sistema operativo aplicar** executa as seguintes ações ao utilizar um pacote de atualização do OS:  

1. Elimine todos os conteúdos no volume visado, exceto ficheiros na pasta especificada pela variável ** \_SMSTSUserStatePath.**  

2. Prepare o ficheiro de resposta:  

    1. Crie um novo ficheiro de resposta com valores padrão criados pelo Gestor de Configuração.  

    2. Fundir quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

### <a name="properties-for-apply-os-image"></a>Propriedades para Aplicar Imagem OS

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Aplicar o sistema operativo a partir de uma imagem capturada

Instala uma imagem de OS que capturou. **Selecione Navegar** para abrir a caixa de diálogo **Selecione.** Em seguida, selecione o pacote de imagem existente que pretende instalar. Se várias imagens estiverem associadas ao pacote de **imagem**especificado, selecione a partir da lista de drop-down a imagem associada a utilizar para esta implementação. Pode ver informações básicas sobre cada imagem existente selecionando-a.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Aplicar o sistema operativo a partir de uma origem de instalação original

Instala um SISTEMA utilizando um pacote de upgrade de OS, que também é uma fonte de instalação original. **Selecione Navegar** para abrir a caixa de diálogo do pacote de atualização do **sistema operativo.** Em seguida, selecione o pacote de atualização de osso existente que pretende utilizar. Pode visualizar informações básicas sobre cada fonte de imagem existente selecionando-as. O painel de resultados na parte inferior da caixa de diálogo exibe as propriedades de origem de imagem associadas. Se houver várias edições associadas ao pacote especificado, utilize a lista de drop-down para selecionar a **Edição** que pretende utilizar.  

> [!NOTE]  
> **Os pacotes** de atualização do sistema operativo destinam-se principalmente a ser utilizados com atualizações no local e não para novas instalações do Windows. Ao implementar novas instalações do Windows, utilize o **sistema operativo Apply** a partir de uma opção de imagem capturada e **instale.wim** a partir dos ficheiros de origem de instalação.
>
> A implementação de novas instalações do Windows através de Pacotes de **Atualização** do Sistema Operativo ainda é suportada, mas está dependente de que os condutores sejam compatíveis com este método. Ao instalar o Windows a partir de um pacote de atualização DES, os controladores são instalados enquanto ainda estão no Windows PE versus simplesmente serem injetados enquanto estão no Windows PE. Alguns condutores não são compatíveis com a instalação do Windows PE.
>
> Se os controladores não forem compatíveis com a instalação do Windows PE, crie uma **Imagem do Sistema Operativo** com a **instalação.wim** a partir dos ficheiros de origem de instalação originais. Em seguida, desloque-se através do sistema operativo Apply a partir de uma opção de **imagem capturada.**

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Utilize um ficheiro de resposta Sysprep ou autónomo para uma instalação personalizada

Utilize esta opção para fornecer um ficheiro de resposta de configuração do Windows **(unattend.xml,** **unattend.txt,** ou **sysprep.inf**), dependendo da versão osso e do método de instalação. O ficheiro que especificar pode incluir qualquer uma das opções de configuração padrão suportadas pelos ficheiros de resposta do Windows. Por exemplo, pode utilizá-lo para especificar a home page predefinida do Internet Explorer. Especifique o pacote que contém o ficheiro de resposta e o caminho associado para o ficheiro na embalagem.  

> [!NOTE]  
> O ficheiro de resposta de configuração do Windows que `%varname%`fornece pode conter variáveis de sequência de tarefaincorporadas do formulário , onde *o nome* é o nome da variável. O passo **Configuração Windows e ConfigMgr** substitui a cadeia variável pelo valor real da variável. Não pode utilizar estas variáveis de sequência de tarefaincorporadas em campos numéricos num ficheiro de resposta sem vigilância.xml.  

Se não fornecer um ficheiro de resposta de configuração do Windows, a sequência de tarefas gera automaticamente um ficheiro de resposta.  

#### <a name="destination"></a>Destino

Configure uma das seguintes opções:  

- **Próxima partição disponível**: Utilize a próxima partição sequencial ainda não visada por um **Sistema Operativo de Aplicação** ou **por aplicar** passo de imagem de dados nesta sequência de tarefas.  

- **Disco específico e partição:** Selecione o número **do disco** (começando com 0) e o número **de partição** (começando com 1).  

- **Letra de unidade lógica específica**: Especifique a letra de **unidade** atribuída à partição pelo Windows PE. Esta carta de unidade pode ser diferente da carta de unidade atribuída pelo sistema operativo recentemente implantado.  

- **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas contendo a letra de unidade atribuída à partição pelo Windows PE. Esta variável é tipicamente definida na secção Avançada da caixa de diálogo **Divisória Properties** para o passo de sequência de tarefas **formato e de divisão.**  

### <a name="options-for-apply-os-image"></a>Opções para Aplicar Imagem OS

Além das opções predefinidas, configure as seguintes definições adicionais no separador **Opções** deste passo de sequência de tarefas:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Aceder diretamente aos conteúdos a partir do ponto de distribuição

Configure a sequência de tarefas para aceder diretamente à imagem do SISTEMA a partir do ponto de distribuição. Por exemplo, utilize esta opção quando implementar sistemas operativos em dispositivos incorporados com capacidade de armazenamento limitada. Ao selecionar esta opção, configure também as definições de partilha de pacotes no separador **de Acesso** de Dados das propriedades da imagem DO.  

> [!NOTE]  
> Esta definição substitui a opção de implementação que configura na página **Pontos** de Distribuição no **Assistente de Software de Implementação**. Esta sobreposição é apenas para a imagem de OS que este passo especifica, não para todos os conteúdos de sequência de tarefas.  

> [!IMPORTANT]  
> Para maior segurança, recomenda-se vivamente que não selecione esta opção. Esta opção foi concebida principalmente para utilização em dispositivos com capacidade de armazenamento limitada. Esta opção não destina-se a ajudar a aumentar a velocidade da sequência de tarefas. Quando esta opção é selecionada, o hash do pacote não é verificado para o pacote do sistema operativo. Por conseguinte, a integridade do pacote não pode ser assegurada porque é possível aos utilizadores com direitos administrativos alterar ou adulterar conteúdos de pacotes.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a>Aplicar as definições do Windows

Utilize este passo para configurar as definições do Windows para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta apropriado. A Configuração do Windows utiliza este ficheiro de resposta durante o **passo De Configuração Windows e ConfigMgr.**  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Definições**, e selecione **Aplicar as Definições do Windows**.

### <a name="variables-for-apply-windows-settings"></a>Variáveis para aplicar definições do Windows

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsULanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Cmdlets para aplicar definições do Windows

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Definição de janelas new-CMTSStepApply](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Remover CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Set-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps)

### <a name="properties-for-apply-windows-settings"></a>Propriedades para aplicar definições do Windows

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="user-name"></a>Nome de utilizador

Especifique o nome de utilizador registado para associar ao computador de destino. O valor que a sequência de tarefas **de Capturar Definições do Windows** pode sobrepor-se a este valor.  

#### <a name="organization-name"></a>Nome da organização

Especifique o nome da organização registada para associar ao computador de destino. O valor que a sequência de tarefas **de Capturar Definições do Windows** pode sobrepor-se a este valor.  

#### <a name="product-key"></a>Chave de produto  

Especifique a chave do produto a utilizar para a instalação do Windows no computador de destino.  

#### <a name="server-licensing"></a>Licenciamento do servidor

Especifique o modo de licenciamento do servidor.

- Selecione **Por servidor** ou **por utilizador** como o modo de licenciamento.  
- Se selecionar **o servidor Per,** especifique também o número máximo de ligações permitidas de acordo com o seu contrato de licença.  
- Se o computador de destino não for um servidor, ou se não quiser especificar o modo de licenciamento, **selecione Não especifique**.  

#### <a name="maximum-connections"></a>Número máximo de ligações

> [!NOTE]
> Esta definição aplica-se apenas a versões antigas do Windows que já não são suportadas.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Gerar aleatoriamente a palavra-passe do administrador local e desativar a conta nas plataformas suportadas (recomendado)  

Selecione esta opção para definir a palavra-passe do administrador local para uma cadeia gerada aleatoriamente. Esta opção também desativa a conta de administrador local em plataformas que suportam esta capacidade.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Ativar a conta e especificar a palavra-passe do administrador local  

Selecione esta opção para ativar a conta de administrador local utilizando a senha especificada. Introduza a palavra-passe na linha **Palavra-passe** e confirme-a na linha **Confirmar palavra-passe**.  

#### <a name="time-zone"></a>Fuso horário

Especifique o fuso horário a configurar no computador de destino. O valor que a sequência de tarefas **de Capturar Definições do Windows** pode sobrepor-se a este valor.  

#### <a name="language-settings"></a>Definições de idioma

<!--5411057, 5138936-->

A partir da versão 1910, controle a configuração do idioma durante a implementação do SO. Se já estiver a aplicar estas definições linguísticas, esta alteração pode ajudá-lo a simplificar a sua sequência de tarefas de implementação de SO. Em vez de utilizar vários passos por idioma ou scripts separados, utilize uma instância por idioma deste passo com uma condição para essa língua.

Configure as seguintes definições:

- Local de entrada (layout padrão do teclado)
- Localização do sistema
- Língua ui
- Recuo da língua da UI
- Local do utilizador

Para obter mais informações sobre estes valores de ficheirode resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Se criar um ficheiro de resposta de configuração personalizado do Windows (unattend.xml), este passo substitui quaisquer valores existentes. Para automatizar um processo dinâmico para estas definições, utilize as variáveis de sequência de tarefas relacionadas. Por exemplo, [OSDWindowsSettingsInputPutPutLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a>Auto Apply Drivers

Utilize este passo para combinar e instalar os controladores como parte da implementação do SISTEMA.  

> [!IMPORTANT]  
> Os meios de comunicação autónomos não podem utilizar o passo de **Auto Apply Drivers.** A sequência de tarefas não tem qualquer ligação ao site do Gestor de Configuração neste cenário.  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **Controladores,** e selecione **Auto Apply Drivers**.

> [!TIP]
> Para uma visão geral dos controladores no Gestor de Configuração, consulte Utilize sequências de [tarefas para instalar os controladores](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Comportamentos para autoaplicar condutores

O passo de sequência de tarefas **Aplicar Controladores Automaticamente** executa as seguintes ações:  

1. Scaneie o hardware e encontre as IDs plug-and-play para todos os dispositivos presentes no sistema.  

2. Envie a lista de dispositivos e as suas iDs plug-and-play para o ponto de gestão. O ponto de gestão devolve uma lista de controladores compatíveis do catálogo de controladores para cada dispositivo de hardware. A lista inclui todos os condutores habilitados, independentemente do pacote de condutores em que se encontram, e os condutores marcados com a categoria de condutor especificado.  

3. Para cada dispositivo de hardware, a sequência de tarefas escolhe o melhor controlador. Este controlador é apropriado para o Sistema operativo implantado e encontra-se num ponto de distribuição acessível.  

4. A sequência de tarefas descarrega os condutores selecionados a partir de um ponto de distribuição e encena os condutores no SISTEMA de oms-alvo.  

    1. Ao utilizar uma imagem de OS, a sequência de tarefacoloca os condutores na loja de controladores DO.  

    2. Ao utilizar um pacote de atualização de OS como fonte de instalação original, a sequência de tarefas configura o Windows Setup com a localização dos controladores.  

5. Durante a **configuração do Windows e da ConfigMgr** na sequência de tarefas, o Windows Setup encontra os controladores encenados por este passo.  

### <a name="variables-for-auto-apply-drivers"></a>Variáveis para autoaplicar condutores

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeout](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceberTimeout](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeout](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeout](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Cmdlets para condutores de aplicação automática

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Novo CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Remover CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Set-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps)

### <a name="properties-for-auto-apply-drivers"></a>Propriedades para Auto Apply Drivers

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Instalar apenas os controladores com melhor compatibilidade

Especifica que o passo de sequência de tarefas instala apenas os controladores com melhor compatibilidade para cada dispositivo de hardware detetado.  

#### <a name="install-all-compatible-drivers"></a>Instalar todos os controladores compatíveis

A sequência de tarefas instala todos os controladores compatíveis para cada dispositivo de hardware detetado. A Configuração do Windows escolhe então o melhor condutor. Esta opção requer mais largura de banda de rede e espaço em disco. A sequência de tarefas descarrega mais controladores, mas o Windows pode selecionar um condutor melhor.  

#### <a name="consider-drivers-from-all-categories"></a>Considerar controladores de todas as categorias

A sequência de tarefas procura todas as categorias de condutores disponíveis para os controladores apropriados do dispositivo.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas

A sequência de tarefas procura nas categorias de condutor especificadas para os controladores de dispositivos apropriados.  

Se selecionar várias categorias, devolve todos os controladores correspondentes que estão presentes em qualquer uma das categorias. É equivalente a `OR` uma operação.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido

Esta opção permite que o Windows instale controladores sem assinatura digital.  

> [!IMPORTANT]  
> Esta opção não se aplica a sistemas operativos onde não é possível configurar a política de contratação do condutor.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a>Capturar Definições de rede

Utilize este passo para capturar as definições de rede da Microsoft a partir do computador que executa a sequência de tarefas. A sequência de tarefas guarda estas definições em variáveis de sequência de tarefas. Estas definições sobrepõem as definições predefinidas que configura na fase de Definições de **Rede de Aplicação.**  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Definições**, e selecione **Definições**de rede de captura .

### <a name="variables-for-capture-network-settings"></a>Variáveis para definições de rede de captura

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Cmdlets para definições de rede de captura

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Definições de redes de rede get-CMTSStepCapture](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Definições de redes de captação de novos cmtsstepcapture](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Remover cmtsStepcaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Definições de definição CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps)

### <a name="properties-for-capture-network-settings"></a>Propriedades para definições de rede de captura

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrar associações de domínio e de grupo de trabalho

Captura as informações de associação de domínios e grupos de trabalho do computador de destino.  

#### <a name="migrate-network-adapter-configuration"></a>Migrar configuração da placa de rede

Captura a configuração da placa de rede do computador de destino. Captura as seguintes informações:

- Configurações globais da rede  
- Número de adaptadores  
- As seguintes definições de rede associadas a cada adaptador: DNS, WINS, IP e filtros de porta



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a>Capturar imagem do sistema operativo

Este passo captura uma ou mais imagens de um computador de referência. A sequência de tarefas cria um ficheiro de imagem do Windows (.wim) na parte especificada da rede. Em seguida, utilize o assistente do Pacote de **Imagem do Sistema Operativo Add** para importar esta imagem para o Gestor de Configuração para implementações de SISTEMA baseadas em imagem.  

O Gestor de Configuração captura cada volume (unidade) do computador de referência para uma imagem separada dentro do ficheiro .wim. Se o computador referenciado tiver vários volumes, o ficheiro .wim resultante contém uma imagem separada para cada volume. Este passo apenas captura volumes que são formatados como NTFS ou FAT32. Salta volumes com outros formatos e volumes USB.  

O SISTEMA instalado no computador de referência deve ser uma versão do Windows que o Gestor de Configuração suporta. Utilize a ferramenta SysPrep para preparar o SISTEMA no computador de referência. O volume de Os instalado e o volume de arranque devem ser do mesmo volume.  

Especifique uma conta com permissões de escrita para a parte de rede selecionada. Para obter mais informações sobre a conta de imagem de captura do OS, consulte [Contas](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens**e selecione **Capture A Imagem do Sistema Operativo**.

### <a name="variables-for-capture-os-image"></a>Variáveis para capturar imagem de OS

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Cmdlets para capturar imagem de OS

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Nova CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Remover CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Set-CMTSStepcapturesystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps)

### <a name="properties-for-capture-os-image"></a>Propriedades para capturar imagem osso

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="target"></a>Destino  

Caminho do sistema de ficheiros para a localização que o Gestor de Configuração utiliza ao armazenar a imagem de OS capturada.  

#### <a name="description"></a>Descrição  

Uma descrição opcional definida pelo utilizador da imagem de OS capturada que está armazenada no ficheiro de imagem.  

#### <a name="version"></a>Versão  

Um número opcional de versão definida pelo utilizador para atribuir à imagem de OS capturada. Este valor pode ser qualquer combinação de letras e números. Está guardado no ficheiro de imagem.  

#### <a name="created-by"></a>Criado por  

O nome opcional do utilizador que criou a imagem de OS. Está guardado no ficheiro de imagem.  

#### <a name="capture-operating-system-image-account"></a>Conta para captura da imagem do sistema operativo  

Introduza a conta Windows que tem permissões para a parte de rede especificada. Selecione **Definir** para especificar o nome da conta Windows.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a>Capturar Estado utilizador

Este passo utiliza a Ferramenta de Migração do Estado do Utilizador (USMT) para capturar o estado do utilizador e as definições a partir do computador que executa a sequência de tarefas. Este passo de sequência de tarefas é utilizado em conjunto com o passo de sequência de tarefas **Restaurar Estado do Utilizador**. Este passo encripta sempre a loja estatal USMT utilizando uma chave de encriptação que o Gestor de Configuração gera e gere.  

Para obter mais informações sobre a gestão do estado do utilizador ao implementar sistemas operativos, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  

Se pretender guardar e restaurar as definições do estado do utilizador a partir de um ponto de migração estatal, utilize este passo com as etapas da **Loja estatal de Pedido** e de Lançamento da State **Store.**  

Este passo fornece o controlo sobre um subconjunto limitado das opções USMT mais usadas. Especifique opções adicionais de linha de comando utilizando a variável de sequência de tarefas **OSDMigrateAdditionalCaptureOptions.**  

Este passo de sequência de tarefas é executado apenas no Windows PE. Não funciona em todo o sistema operativo.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **User State**, e selecione Capture **User State**.

### <a name="variables-for-capture-user-state"></a>Variáveis para capturar o Estado do Utilizador

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Cmdlets para capturar estado utilizador

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepcaptureuserstate](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps)
- [New-CMTSStepcaptureuserstate](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps)
- [Remover CMTSStepcaptureuserstate](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps)
- [Set-CMTSStepcaptureuserstate](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps)

### <a name="properties-for-capture-user-state"></a>Propriedades para capturar estado utilizador

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="user-state-migration-tool-package"></a>Pacote do User State Migration Tool

Especifique o pacote que contém a ferramenta de migração do Estado utilizador (USMT). A sequência de tarefas utiliza esta versão do USMT para capturar o estado e as definições do utilizador. Este pacote não requer um programa. Especifique um pacote que contenha a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do SO de onde a sequência de tarefas está a capturar o estado.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Capturar todos os perfis de utilizador com opções padrão

Migrar todas as informações sobre o perfil do utilizador. Esta é a opção predefinida.  

Se selecionar esta opção, mas não selecionar restaurar os **perfis de utilizador do computador local** na etapa do Estado do Utilizador **restaurar,** a sequência de tarefas falha. O Gestor de Configuração não pode migrar as novas contas sem lhes atribuir senhas.

Quando utilizar a **instalação de uma** opção de pacote de imagem existente do novo assistente de sequência de **tarefas,** a sequência de tarefas resultante falha para capturar todos os perfis do utilizador **com opções padrão**. Esta sequência de tarefas padrão não seleciona a opção de restaurar os **perfis de utilizador de computador locais,** ou contas de utilizador não domínio.  

Selecione **Restaurar os perfis de utilizador do computador local** e fornecer uma palavra-passe para a conta migrar. Numa sequência de tarefas criada manualmente, esta definição encontra-se sob o passo do Estado do **Utilizador restaurar.** Numa sequência de tarefas criada pelo assistente **Nova Sequência de Tarefas**, esta definição pode ser encontrada na página do assistente no passo **Restaurar Definições e Ficheiros do Utilizador**.  

Se não tiver contas de utilizador locais, esta definição não se aplica.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personalizar como os perfis de utilizador são capturados

Selecione esta opção para especificar um ficheiro de perfil personalizado para migração. Selecione **Ficheiros** para selecionar os ficheiros de configuração para USMT para utilizar com este passo. Especifique um ficheiro .xml personalizado que contenha regras que definem os ficheiros do estado do utilizador para migrar.  

#### <a name="click-here-to-select-configuration-files"></a>Clique aqui para selecionar ficheiros de configuração

Selecione esta opção para selecionar os ficheiros de configuração no pacote do USMT que pretende utilizar para capturar os perfis de utilizador. Selecione o botão **Ficheiros** para lançar a caixa de diálogo **'Ficheiros** de Configuração'. Para especificar um ficheiro de configuração, introduza o nome do ficheiro na linha **'Nome** de ficheiros' e selecione o botão **Adicionar.**  

#### <a name="enable-verbose-logging"></a>Ativar registo verboso

Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao capturar o estado, a sequência de tarefa por padrão gera **ScanState.log** na pasta de registo da sequência de tarefas, `%WinDir%\ccm\logs`.  

#### <a name="skip-files-using-encrypted-file-system"></a>Ignorar ficheiros que utilizam o sistema de encriptação de ficheiros

Ative esta opção de ignorar a captura de ficheiros encriptados com o Sistema de Ficheiros Encriptados (EFS). Estes ficheiros incluem ficheiros de perfil do utilizador. Dependendo das versões OS e USMT, os ficheiros encriptados podem não ser legíveis depois de restaurar. Para mais informações, consulte a documentação do USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copiar utilizando o acesso do sistema de ficheiros

Ative esta opção para especificar qualquer uma das seguintes definições:  

- **Continue se alguns ficheiros não puderem ser capturados**: Permitir que esta definição continue o processo de migração mesmo que não consiga capturar alguns ficheiros. Se desativar esta opção, e um ficheiro não puder ser capturado, então este passo falha. Por predefinição, esta opção encontra-se ativada.  

- **Capturar localmente ao utilizar ligações em vez de copiar ficheiros**: ative esta definição para utilizar ligações fixas NTFS para capturar ficheiros.  

    Para obter mais informações sobre dados migratórios utilizando links rígidos, consulte a [Hard-Link Migration Store](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Capturar no modo off-line (apenas windows PE)**: Ative esta definição para capturar o estado do utilizador enquanto estiver no Windows PE em vez do SISTEMA completo.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Capturar utilizando o Serviço Sombra de Cópia de Volume (VSS)

Esta opção permite-lhe capturar ficheiros mesmo que estejam bloqueados para serem editados por outra aplicação.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a>Capturar definições do Windows

Utilize este passo para capturar as definições do Windows a partir do computador que executa a sequência de tarefas. A sequência de tarefas guarda estas definições em variáveis de sequência de tarefas. Estas definições capturadas sobrepõem as definições predefinidas que configura na fase de definições do **Windows Apply.**  

Este passo de sequência de tarefas funciona no Windows PE ou no SISTEMA completo.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Definições**, e selecione **Capturar definições do Windows**.

### <a name="variables-for-capture-windows-settings"></a>Variáveis para capturar definições do Windows

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Cmdlets para capturar definições do Windows

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Definições de janelas de captura de passos get-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Definições de windowswindows de captura de novos CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Remover cmtsStepcaptureWindowsDefinições](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Definição de definição cmtsstepcaptureWindowsDefinições](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps)

### <a name="properties-for-capture-windows-settings"></a>Propriedades para capturar definições do Windows

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="migrate-computer-name"></a>Migrar nome do computador

Capture o nome do computador NetBIOS do computador.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrar nomes organizacionais e de utilizador registados

Capture os nomes de utilizador e organização registados a partir do computador.  

#### <a name="migrate-time-zone"></a>Migrar fuso horário

Capture a definição do fuso horário no computador.  



## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a>Verificar prontidão

Utilize este passo para verificar se o computador-alvo satisfaz as condições pré-requisitos de implementação especificadas.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **General**, e selecione **Verificar prontidão**.

A partir da versão 2002, este passo inclui oito novos cheques. Nenhum destes novos controlos é selecionado por defeito em casos novos ou existentes do passo.<!--6005561--> Para obter mais informações sobre cada verificação, consulte as secções específicas abaixo.

- **Arquitetura do sistema operativo atual**
- **Versão mínima do SO**
- **Versão máxima do SO**
- **Versão mínima do cliente**
- **Linguagem do sistema operativo atual**
- **Alimentação ca-eléctrica ligada**
- **Adaptador de rede ligado**
  - **Adaptador de rede não é sem fios**

> [!IMPORTANT]
> Para aproveitar esta nova funcionalidade de Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

O **smsts.log** inclui o resultado de todos os cheques. Se uma verificação falhar, o motor de sequência de tarefas continua a avaliar as outras verificações. O passo não falha até que todos os cheques estejam completos. Se pelo menos uma verificação falhar, o passo falha e devolve o código de erro **4316**. Este código de erro traduz-se em "O recurso necessário para esta operação não existe."

### <a name="variables-for-check-readiness"></a>Variáveis para verificação de prontidão

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)

### <a name="cmdlets-for-check-readiness"></a>Cmdlets para verificar prontidão

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestatCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps)
- [Novo CMTSStepPrestatCheck](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps)
- [Remover CMTSStepPrestatCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps)
- [Set-CMTSStepPrestatCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps)

### <a name="properties-for-check-readiness"></a>Propriedades para Verificação de Prontidão

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="minimum-memory-mb"></a>Memória mínima (MB)

Verifique se a quantidade de memória, em megabytes (MB), satisfaz ou excede a quantidade especificada. O passo permite esta definição por defeito.  

#### <a name="minimum-processor-speed-mhz"></a>Velocidade mínima do processador (MHz)  

Verifique se a velocidade do processador, em megahertz (MHz), corresponde ou excede a quantidade especificada. O passo permite esta definição por defeito.  

#### <a name="minimum-free-disk-space-mb"></a>Espaço mínimo de disco livre (MB)

Verifique se a quantidade de espaço em disco livre, em megabytes (MB), corresponde ou excede a quantidade especificada.  

#### <a name="current-os-to-be-refreshed-is"></a>O sistema operativo atual a ser refrescado é

Verifique se o SISTEMA instalado no computador-alvo satisfaz o requisito especificado. O passo define esta definição para **CLIENTE** por padrão.  

#### <a name="architecture-of-current-os"></a>Arquitetura do sistema operativo atual

A partir da versão 2002, verifique se o atual SISTEMA é **de 32 bits** ou **64 bits**.

#### <a name="minimum-os-version"></a>Versão mínima do SO

A partir da versão 2002, verifique se o sistema operativo operativo atual está a executar uma versão mais tarde do que o especificado. Especifique a versão com versão principal, versão menor e número de construção. Por exemplo, `10.0.16299`.

#### <a name="maximum-os-version"></a>Versão máxima do SO

A partir da versão 2002, verifique se o sistema operativo operativo atual está a executar uma versão mais cedo do que o especificado. Especifique a versão com versão principal, versão menor e número de construção. Por exemplo, `10.0.18356`.

#### <a name="minimum-client-version"></a>Versão mínima do cliente

A partir da versão 2002, verifique se a versão cliente do Gestor de Configuração é, pelo menos, a versão especificada. Especifique a versão `5.00.8913.1005`cliente no seguinte formato: .

#### <a name="language-of-current-os"></a>Linguagem do sistema operativo atual

A partir da versão 2002, verifique se a língua atual do OS corresponde ao que especifica. Selecione o nome do idioma e o passo compara o código de idioma associado. Este cheque compara o idioma que seleciona à propriedade **OSLanguage** da classe **WMI Win32_OperatingSystem** no cliente.

#### <a name="ac-power-plugged-in"></a>Alimentação ca-eléctrica ligada

A partir da versão 2002, verifique se o dispositivo está ligado e não a bateria.

#### <a name="network-adapter-connected"></a>Adaptador de rede ligado

A partir da versão 2002, verifique se o dispositivo tem um adaptador de rede ligado à rede. Também pode selecionar a verificação dependente para verificar se o **adaptador rede não é sem fios**.

### <a name="options-for-check-readiness"></a>Opções para Verificar Prontidão

> [!NOTE]  
> Se ativar a definição de **erro continue** no separador **Opções** deste passo, apenas regista os resultados da verificação de prontidão. Se uma verificação falhar, a sequência de tarefas não para.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a>Ligar à pasta da rede

Use este passo para criar uma ligação a uma pasta de rede partilhada.  

Este passo de sequência de tarefas funciona em todo o SISTEMA ou Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **General**, e selecione A pasta Connect **To Network**.

### <a name="variables-for-connect-to-network-folder"></a>Variáveis para ligar à pasta de rede

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Cmdlets para Ligar à Pasta da Rede

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkfolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Pasta new-CMTSStepConnectNetwork](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Remover cmtsStepConnectNetworkfolder](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Set-CMTSStepConnectNetworkfolder](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps)

### <a name="properties-for-connect-to-network-folder"></a>Propriedades para Ligar à Pasta de Rede

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="path"></a>Caminho  

**Selecione Navegar** para especificar o caminho da pasta da rede. Utilize o formato `\\server\share`.

#### <a name="drive"></a>Lista de unidades  

Selecione a carta de unidade local para atribuir para esta ligação.

#### <a name="account"></a>Conta

Selecione **Definir** para especificar a conta de utilizador com permissões para ligar a esta pasta de rede. Para obter mais informações sobre a conta de ligação da rede de sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)consulte Contas .



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a>Desativar bitLocker

Utilize este passo para desativar a encriptação BitLocker na unidade de Sistema operativo atual ou numa unidade específica. Esta ação deixa os protectores-chave visíveis num texto claro no disco rígido. Não desencripta o conteúdo da unidade. Esta ação completa quase instantaneamente.  

> [!NOTE]  
> A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

Se tiver várias unidades encriptadas, desative o BitLocker em quaisquer unidades de dados antes de desativar o BitLocker na unidade OS.  

Este passo funciona apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **Discos,** e selecione **Disable BitLocker**.

### <a name="variables-for-disable-bitlocker"></a>Variáveis para Desativar BitLocker

A partir da versão 1906, utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [Contagem de rebootde osdbitlocker](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Cmdlets para Desativar BitLocker

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps)
- [New-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps)
- [Remover CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps)
- [Set-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps)

### <a name="properties-for-disable-bitlocker"></a>Propriedades para Desativar BitLocker

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="current-operating-system-drive"></a>Unidade do sistema operativo atual

Desativa o BitLocker na unidade atual de Sistema operativo.  

#### <a name="specific-drive"></a>Unidade específica  

Desativa o BitLocker numa unidade específica. Utilize a lista pendente para especificar a unidade na qual o BitLocker está desativado.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Retomar a proteção depois de o Windows ter sido reiniciado o número especificado de vezes

<!-- 4512937 -->
A partir da versão 1906, utilize esta opção para especificar o número de reinícios para manter o BitLocker desativado. Em vez de adicionar várias instâncias deste passo, detete teum valor entre 1 (padrão) e 15.

Pode definir e modificar este comportamento com as variáveis de sequência de [tarefas OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) e [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a>Baixar conteúdo de pacote

Utilize este passo para descarregar qualquer um dos seguintes tipos de pacotes:  

- Imagens do SO  
- Pacotes de upgrade de OS  
- Pacotes de controladores  
- Pacotes  
- Imagens de arranque <sup> [Nota 1](#bkmk_note1)</sup>  

Este passo funciona bem numa sequência de tarefas para atualizar um Sistema operativo nos seguintes cenários:  

- Para utilizar uma única sequência de tarefas de atualização que funciona com plataformas x86 e x64. Inclua dois passos de conteúdo de pacote de **descarregamento** no grupo **Prepare-se para upgrade.** Especifique as condições no separador **Opções** para detetar a arquitetura do cliente e faça o download apenas do pacote de upgrade de SO apropriado. Configure cada passo de conteúdo do **pacote de descarregamento** para usar a mesma variável. Utilize a variável para o caminho dos meios de comunicação na etapa do **Sistema Operativo de Upgrade.**  

- Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada passo de conteúdo do **pacote de descarregamento** para usar a mesma variável. Utilize a variável para o valor de **conteúdo encenado** na secção de Controladores da etapa do **Sistema Operativo de Atualização.**  

> [!NOTE]  
> Quando implementar uma sequência de tarefas que contenha este passo, não selecione **Descarregue todos os conteúdos localmente antes** de iniciar a sequência de tarefas ou **o conteúdo de acesso diretamente a partir de um ponto** de distribuição para **opções** de distribuição na página **pontos** de distribuição do Assistente de Software de Implementação.  

Este passo funciona em todo o SISTEMA ou Windows PE. A opção de guardar o pacote na cache do cliente do Gestor de Configuração não é suportada no Windows PE.

> [!NOTE]  
> A tarefa de **descarregamento** de conteúdo de pacote não é suportada para uso com meios autónomos. Para mais informações, consulte [ações não apoiadas para meios de comunicação autónomos.](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media)  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Software**, e selecione **Descarregamento Conteúdo**de Pacote .

### <a name="cmdlets-for-download-package-content"></a>Cmdlets para descarregar conteúdo de pacote

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps)
- [New-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Remover cmtsstepdownloadpacote](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Set-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps)

### <a name="properties-for-download-package-content"></a>Propriedades para descarregamento de conteúdo de pacote

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="select-package"></a>Selecionar o pacote  

Selecione o ícone para escolher o pacote para descarregar. Depois de escolher um pacote, selecione novamente o ícone para escolher outro pacote.  

#### <a name="place-into-the-following-location"></a>Coloque na seguinte localização

Opte por guardar a embalagem num dos seguintes locais:  

- **Diretório**de trabalho de sequência de tarefas : Esta localização também é referida como a cache da sequência de tarefas.  

- **Configuração Manager cache cliente**: Use esta opção para armazenar o conteúdo na cache do cliente. Por defeito, `%WinDir%\ccmcache`este caminho é .  

- **Percurso personalizado**: O motor de sequência de tarefas primeiro descarrega o pacote para o diretório de trabalho da sequência de tarefas. Em seguida, move o conteúdo para este caminho que especifica. O motor de sequência de tarefas adere o caminho com o ID do pacote.  

#### <a name="save-path-as-a-variable"></a>Guardar o caminho como uma variável

Guarde o caminho do pacote para uma variável de sequência de tarefas personalizada. Em seguida, use esta variável em outro passo de sequência de tarefa.

O Gestor de Configuração adiciona um sufixo numérico ao nome variável. Por exemplo, especifica-se `%MyContent%` uma variável como variável personalizada. É a raiz para onde a sequência de tarefas armazena todos os conteúdos referenciados para este passo. Este conteúdo pode conter vários pacotes. Quando se referir à variável, adicione um sufixo numérico. Para o primeiro pacote, consulte `%MyContent01%`. Quando se refere à variável em etapas subsequentes, como sistema operativo de **upgrade,** utilize `%MyContent02%` ou `%MyContent03%`, quando o número corresponder à ordem de que a etapa de **Descarregamento** do Conteúdo do Pacote lista as embalagens.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Se a transferência de um pacote falhar, continue a transferir os outros pacotes da lista

Se a sequência de tarefas não conseguir descarregar um pacote, começa a descarregar o próximo pacote da lista.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a>Nota 1: Utilização de imagens de arranque na etapa de conteúdo do pacote de descarregamento

*Aplica-se à versão 1910 e posterior*<!-- SCCMDocs-pr #4202 -->

Se configurar as propriedades da sequência de [tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) para utilizar uma imagem de **arranque,** então adicionar uma imagem de bota a este passo é redundante. Adicione apenas uma imagem de bota a este passo se não for especificada nas propriedades da sequência de tarefas.

#### <a name="example-use-case"></a>Caso de utilização de exemplo

- Uma única sequência de tarefas para pré-descarregar conteúdo:
  - Sem imagem de arranque associada.
  - Funciona apenas em todo o SISTEMA, provavelmente sem interação do utilizador.
  - Utiliza vários passos de conteúdo de pacote de **descarregamento** com condições. Dependendo da linguagem e arquitetura específicas, ele descarrega conteúdo para a cache do cliente para se preparar para a sequência de tarefas de implementação de SO.
  - Há apenas um exemplo desta sequência de tarefas, com todas as opções de conteúdo possíveis.

- Múltiplas sequências de tarefas de implementação do OS:
  - Uma sequência normal de tarefas de implantação de SO.
  - Tem uma imagem de arranque referenciada nas suas propriedades.
  - Existem múltiplos casos desta sequência de tarefas, com diferentes imagens de boot como necessárias pela arquitetura e linguagem

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a>Ativar o BitLocker

Utilize este passo para ativar a encriptação BitLocker em pelo menos duas divisórias no disco rígido. A primeira partição ativa contém o código de arranque do sistema do Windows. Outra divisória contém o SO. A partição de arranque do sistema tem de permanecer desencriptada.  

Utilize o passo **BitLocker de pré-fornecimento** para ativar o BitLocker numa unidade enquanto estiver no Windows PE. Para mais informações, consulte [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
> A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

Este passo funciona apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Discos**, e selecione **Enable BitLocker**.

Quando especificar **apenas TPM**, **TPM e Chave de Arranque em USB,** ou **TPM e PIN,** o Módulo de Plataforma Fidedigna (TPM) deve estar no seguinte estado antes de poder executar o passo **Enable BitLocker:**  

- Ativado  
- Ativado  
- Propriedade Permitida  

Este passo completa qualquer inicialização tpm restante. Os passos restantes não requerem presença física ou reinicialização. O passo **Enable BitLocker** completa de forma transparente as seguintes etapas de inicialização tpm restantes, se necessário:  

- Criar par de chaves de endossamento  
- Criar valor de autorização do proprietário e efetuar caução para o Active Directory, expandido para suportar este valor  
- Obter propriedade  
- Criar SRK (Storage Root Key) ou repor se já existir mas for incompatível  

Se pretender que a sequência de tarefas aguarde o passo **Enable BitLocker** para completar o processo de encriptação de unidade, então selecione a opção **Esperar.** Se não selecionar a opção **Esperar,** o processo de encriptação da unidade acontece em segundo plano. A sequência de tarefas prossegue imediatamente para o próximo passo.  

O BitLocker pode ser usado para encriptar várias unidades num sistema informático, tanto o SISTEMA como as unidades de dados. Para encriptar uma unidade de dados, primeiro criptografe a unidade DE SO e complete o processo de encriptação. Este requisito deve-se ao facto de o acionamento soque armazena os principais protetores para as unidades de dados. Se encriptar o OS e os dados na mesma sequência de tarefas, selecione a opção **'Esperar'** no passo **Enable BitLocker** para a unidade OS.  

Se o disco rígido já estiver encriptado, mas o BitLocker estiver desativado, o passo **Enable BitLocker** volta a ativar os protectores-chave e completa-se rapidamente. A reencriptação do disco rígido não é necessária neste caso.  

### <a name="variables-for-enable-bitlocker"></a>Variáveis para Enable BitLocker

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>Cmdlets para Enable BitLocker

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps)
- [New-CMTSStepenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps)
- [Remover CMTSStepenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps)

### <a name="properties-for-enable-bitlocker"></a>Propriedades para Enable BitLocker

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="choose-the-drive-to-encrypt"></a>Selecione a unidade a encriptar

Especifica a unidade a encriptar. Para encriptar a unidade atual do SISTEMA OS, selecione a unidade do **sistema operativo Atual**. Em seguida, configure uma das seguintes opções para a gestão chave:  

- **Apenas TPM**: selecione esta opção para utilizar apenas o Trusted Platform Module (TPM).  

- **Apenas Chave de Arranque em USB**: selecione esta opção para utilizar uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

- **TPM e Chave de Arranque em USB**: selecione esta opção para utilizar TPM e uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

- **TPM e PIN**: Selecione esta opção para utilizar TPM e um número de identificação pessoal (PIN). Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até o utilizador fornecer o PIN.  

Para encriptar uma unidade de dados específica e não-OS, selecione **unidade específica**. Em seguida, selecione a unidade da lista.  

#### <a name="use-full-disk-encryption"></a>Use encriptação completa do disco

<!--SCCMDocs-pr issue 2671-->
Por predefinição, este passo apenas encripta o espaço usado na unidade. Este comportamento padrão é recomendado, uma vez que é mais rápido e eficiente. Se a sua organização necessitar de encriptar toda a unidade durante a configuração, então ative esta opção. A Configuração do Windows aguarda que toda a unidade encripte, o que demora muito tempo, especialmente em grandes unidades.

> [!TIP]
> A partir da versão 1910, pode criar e implementar políticas de gestão bitLocker, que utilizam encriptação completa do *disco.* Para gerir o BitLocker nos dispositivos após a sequência de tarefas implementar o SISTEMA, ative esta opção. Para mais informações, consulte [Plan for BitLocker management](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Escolha onde criar a chave de recuperação

Para especificar para o BitLocker criar a palavra-passe de recuperação e depositá-la no Diretório Ativo, selecione **In Ative Directory**. Esta opção requer que estenda o Diretório Ativo para a chave BitLocker. O BitLocker pode então guardar as informações de recuperação associadas no Diretório Ativo. Selecione **Não crie a chave de recuperação** para não criar uma palavra-passe. Criar uma palavra-passe é a opção recomendada.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Aguardar que o BitLocker conclua o processo de encriptação da unidade em todas as unidades antes de continuar a execução da sequência de tarefas

Selecione esta opção para permitir que a encriptação de unidade BitLocker esteja completa antes de executar o próximo passo na sequência de tarefas. Se selecionar esta opção, o BitLocker encripta todo o volume do disco antes de o utilizador poder iniciar sessão no computador.  

O processo de encriptação pode demorar horas a ser concluído ao encriptar um grande disco rígido. Não selecionar esta opção permite que a sequência de tarefas prossiga imediatamente.  



## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a>Formato e Disco de Partição

Utilize este passo para formatar e dividir um disco especificado no computador de destino.  

> [!IMPORTANT]  
> Cada definição especificada para este passo aplica-se a um único disco especificado. Para formatar e dividir outro disco no computador de destino, adicione um formato adicional e um passo de disco de **partição** na sequência de tarefas.  

Este passo é executado apenas no Windows PE. Não funciona em todo o sistema operativo.  

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **Discos,** e selecione **Formato e Disco de Partição**.

### <a name="variables-for-format-and-partition-disk"></a>Variáveis para Formato e Disco de Partição

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Cmdlets para formato e disco de partição

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Disco de Partição Get-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps)
- [Disco de Partição New-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps)
- [Remover cmtsSteppartitiondisk](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps)
- [Set-CMTSStepPartitiondisk](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps)

### <a name="properties-for-format-and-partition-disk"></a>Propriedades para Formato e Disco de Partição

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="disk-number"></a>Número do Disco

O número físico do disco para o formato. O número é baseado na ordem de enumeração de discos do Windows.  

#### <a name="disk-type"></a>Tipo de Disco

O tipo do disco em formato. Existem duas opções disponíveis para seleção na lista pendente:

- **Standard (MBR)**: Master Boot Record  
- **GPT**: Tabela de Partição GUID  

> [!NOTE]  
> Se alterar o tipo de disco de **Standard (MBR)** para **GPT,** e o layout da divisória contiver uma divisória estendida, a sequência de tarefaremove todas as divisórias estendidas e lógicas do layout. O editor da sequência de tarefas solicita que confirme esta ação antes de alterar o tipo de disco.  

#### <a name="volume"></a>Volume

Informações específicas sobre a partição ou volume que a sequência de tarefas cria, incluindo os seguintes atributos:  

- Nome  
- Espaço em disco restante  

Para criar uma nova partição, selecione **New** para lançar a caixa de diálogo **Partition Properties.** Especifique o tipo e o tamanho da partição, e se for uma partição de botas. Para modificar uma divisória existente, selecione a divisória a modificar e, em seguida, selecione o botão **Propriedades.** Para obter mais informações sobre como configurar divisórias de disco rígido, consulte um dos seguintes artigos:  

- [Partições de disco rígido baseadas em UEFI/GPT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Partições de disco rígido baseadas em BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Para eliminar uma partição, escolha a partição e, em seguida, **selecione Delete**.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a>Instalar aplicação

Este passo instala as aplicações especificadas, ou um conjunto de aplicações definidas por uma lista dinâmica de variáveis de sequência de tarefas. Quando a sequência de tarefas passa este passo, a instalação da aplicação começa imediatamente sem esperar por um intervalo de votação política.  

Os pedidos devem satisfazer os seguintes critérios:  

- A aplicação deve ter um tipo de instalação de **implementação** do Instalador do Windows ou do instalador **de Scripts.** Os tipos de implementação do pacote de aplicativos Windows (.appx file) não são suportados.  

- Deve ser executado sob a conta do Sistema Local e não da conta de utilizador.  

- Não pode interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

- Não pode iniciar um reinício por si só. O pedido deve solicitar um reinício utilizando o código de reinício padrão, 3010. Este comportamento garante que este passo lida corretamente com o reinício. Se a aplicação devolver um código de saída 3010, o motor de sequência de tarefas reinicia o computador. Após o reinício, a sequência de tarefas continua automaticamente.  

> [!Note]
> Se a aplicação verificar a execução de [ficheiros executáveis,](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check)a sequência de tarefas não o instalará. Se não configurar este passo para continuar com o erro, então toda a sequência de tarefas falha.

Quando este passo corre, a aplicação verifica a aplicabilidade das regras de exigência e o método de deteção nos seus tipos de implementação. Com base nos resultados desta verificação, a aplicação instala o tipo de implementação aplicável. Se um tipo de implantação contiver dependências, o tipo de implantação dependente é avaliado e instalado como parte deste passo. As dependências de aplicações não são suportadas para meios de comunicação autónomos.  

> [!NOTE]  
> Para instalar uma aplicação que substitui outra aplicação, os ficheiros de conteúdo para a aplicação substituído devem estar disponíveis. Caso contrário, este passo de sequência de tarefafalha. Por exemplo, o Microsoft Visio 2010 é instalado num cliente ou numa imagem capturada. Quando a etapa de instalação da **Aplicação** instalar o Microsoft Visio 2013, os ficheiros de conteúdo do Microsoft Visio 2010 (a aplicação supersed) devem estar disponíveis num ponto de distribuição. Se o Microsoft Visio não estiver instalado num cliente ou numa imagem capturada, a sequência de tarefas instala o Microsoft Visio 2013 sem verificar os ficheiros de conteúdo da Microsoft Visio 2010.  
>
> Se retirar uma aplicação supersed, e a nova aplicação for referenciada numa sequência de tarefas, a sequência de tarefas não começa.
Este comportamento é por design: a sequência de tarefas requer todas as referências da aplicação.<!-- SCCMDocs 1711 -->  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Software**, e selecione **Instalar aplicação**.

### <a name="variables-for-install-application"></a>Variáveis para instalação de aplicação

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Se o cliente não conseguir recuperar a lista de pontos de gestão dos serviços de localização, utilize as variáveis de sequência de tarefas **SMSTSMPListRequestTimeout** e **SMSTSMPListRequestTimeout.** Estas variáveis especificam quantos milissegundos uma sequência de tarefas espera antes de voltar a instalar uma aplicação. Para obter mais informações, consulte variáveis de sequência de [tarefas](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Cmdlets para instalação

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Aplicação de instalação Get-CMTSStep](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [Nova CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remover cmtsstepinstalação](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties-for-install-application"></a>Propriedades para Instalação

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="install-the-following-applications"></a>Instale as seguintes aplicações

A sequência de tarefas instala estas aplicações na ordem especificada.  

O Gestor de Configuração filtra quaisquer aplicações desativadas ou quaisquer aplicações com as seguintes definições:  

- Apenas quando um utilizador tiver sessão iniciada  
- Executar com direitos de utilizador  

Estas aplicações não aparecem na **aplicação Select para instalar** a caixa de diálogo.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Instalar aplicações de acordo com a lista de variáveis dinâmicas

A sequência de tarefas instala aplicações utilizando este nome variável base. O nome variável base é para um conjunto de variáveis de sequência de tarefadefinidas definidas para uma coleção ou computador. Estas variáveis especificam as aplicações que a sequência de tarefas instala para essa recolha ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 01. O valor de cada variável tem de conter o nome da aplicação e mais nada.  

Para que a sequência de tarefas instale aplicações utilizando uma lista variável dinâmica, ative a seguinte definição no separador **Geral** da aplicação **Propriedades**: Permita que esta aplicação seja instalada a partir da ação de sequência de **tarefas de instalação em vez de ser implantada manualmente**.  

> [!NOTE]  
> Não é possível instalar aplicações utilizando uma lista variável dinâmica para implementações autónomas de meios de comunicação.  

Por exemplo, para instalar uma única aplicação utilizando uma variável de sequência de tarefas chamada AA01, especifique a seguinte variável:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Para instalar duas aplicações, especifique as seguintes variáveis:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

As seguintes condições afetam as aplicações instaladas pela sequência de tarefas:  

- O valor de uma variável contém quaisquer informações além do nome da aplicação. A sequência de tarefas não instala a aplicação e a sequência de tarefas continua.  

- Se a sequência de tarefas não encontrar uma variável com o nome base especificado e sufixo "01", a sequência de tarefas não instala nenhuma aplicação.  

> [!Important]  
> Estes valores são sensíveis aos casos. Por exemplo, "instalar" é diferente de "Instalar". Se precisar de alterar o valor, o editor da sequência de tarefas não deteta uma mudança de caso. Faça outra edição ao mesmo tempo, por exemplo, modifique a descrição do passo.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Se a instalação de uma aplicação falhar, continue a instalar outras aplicações na lista

Esta definição especifica que o passo continua quando uma instalação de aplicação individual falha. Se especificar esta definição, a sequência de tarefas continua independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Limpar o conteúdo da aplicação a partir da cache após a instalação

<!--4485675-->
A partir da versão 1906, apague o conteúdo da aplicação da cache do cliente após a corrida do passo. Este comportamento é benéfico em dispositivos com pequenos discos rígidos ou na instalação de muitas grandes aplicações sucessivamente.


### <a name="options-for-install-application"></a>Opções para Instalação de Aplicação

> [!NOTE]  
> Quando selecionar **Continue a trabalhar no** separador **Opções** deste passo, a sequência de tarefas continua quando uma aplicação não instala. Quando não permite esta opção, a sequência de tarefas falha e não instala as restantes aplicações.  

Além das opções predefinidas, configure as seguintes definições adicionais no separador **Opções** deste passo de sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Tente novamente este passo se o computador reiniciar inesperadamente

Se uma das instalações da aplicação reiniciar inesperadamente o computador, tente novamente este passo. O passo permite esta definição por defeito com duas repetições. Pode especificar de um a cinco repetições.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a>Instalar pacote

Utilize este passo para instalar um pacote de software como parte da sequência de tarefas. Quando este passo corre, a instalação começa imediatamente sem esperar por um intervalo de votação política.  

O pacote deve satisfazer os seguintes critérios:  

- Deve ser executado sob a conta do Sistema Local e não uma conta de utilizador.  

- Não devia interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

- Não pode iniciar um reinício por si só. O software deve solicitar um reinício utilizando o código de reinício padrão, 3010. Este comportamento certifica-se de que a sequência de tarefas lida corretamente com o reinício. Se o software devolver um código de saída 3010, o motor de sequência de tarefas reinicia o computador. Após o reinício, a sequência de tarefas continua automaticamente.  

Os programas que utilizam o **programa Executar outra** opção para instalar um programa dependente não são suportados na implementação de um SISTEMA. Se ativar a opção do pacote **Executar primeiro outro programa**, e o programa dependente já executado no computador de destino, o programa dependente funciona e a sequência de tarefas continua. No entanto, se o programa dependente ainda não tiver corrido no computador de destino, o passo da sequência de tarefas falha.  

> [!NOTE]  
> O site da administração central não tem as políticas de configuração necessárias para ativar o agente de distribuição de software durante a sequência de tarefas. Quando cria um suporte de dados autónomo para uma sequência de tarefas do site de administração central e a sequência de tarefas inclui um passo **Instalar Pacote**, pode aparecer o erro seguinte no ficheiro CreateTsMedia.log:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> Para meios autónomos que incluam um passo **de Pacote de Instalação,** crie os meios autónomos num site primário que tenha o agente de distribuição de software ativado. Em alternativa, adicione um passo de linha de comando de **execução** após o passo de **Configuração Windows e ConfigMgr** e antes do primeiro passo do **Pacote de Instalação.** O passo **da Linha de Comando executar** executa um comando WMIC para ativar o agente de distribuição de software antes do primeiro passo do Pacote de **Instalação.** Utilize o seguinte comando na linha de **comando de execução:**  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Para obter mais informações sobre a criação de meios de comunicação autónomos, consulte [Create stand-alone media](../deploy-use/create-stand-alone-media.md).  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Software**, e selecione **Instalar Pacote**.

### <a name="variables-for-install-package"></a>Variáveis para pacote de instalação

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [Comando osddonotlog](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Cmdlets para pacote de instalação

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps)
- [Novo CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps)
- [Remover cmtsstepinstalar software](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps)
- [Set-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps)

> [!TIP]
> Utilize o pré-cache de conteúdo para descarregar um pacote de atualização de OS aplicável antes de um utilizador instalar a sequência de tarefas. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Propriedades para pacote de instalação

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="install-a-single-software-package"></a>Instalar um pacote de software único

Esta definição especifica um pacote de software De Configuração Manager. O passo aguarda até que a instalação esteja concluída.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Instalar os pacotes de software de acordo com a lista de variáveis dinâmicas

A sequência de tarefas instala pacotes utilizando este nome variável base. O nome variável base é para um conjunto de variáveis de sequência de tarefadefinidas definidas para uma coleção ou computador. Estas variáveis especificam as embalagens que a sequência de tarefas instala para essa recolha ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 001. O valor de cada variável tem de conter um ID de pacote e o nome do software separados por dois pontos.  

Para que a sequência de tarefas instale o software utilizando uma lista variável dinâmica, ative a seguinte definição no separador **Avançado** da embalagem **Propriedades**: Permita que este programa seja instalado a partir da sequência de **tarefas do Pacote de Instalação sem ser implementado**.  

> [!NOTE]  
> Não é possível instalar pacotes de software utilizando uma lista variável dinâmica para implementações autónomas de meios de comunicação.  

Por exemplo, para instalar um único pacote de software através de uma variável de sequência de tarefas denominada AA001, tem de especificar a seguinte variável:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Para instalar três pacotes de software, tem de especificar as seguintes variáveis:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

As seguintes condições afetam as embalagens instaladas pela sequência de tarefas:  

- Se não criar o valor de uma variável no formato correto, ou se não especificar um ID e nome de pacote válidos, a instalação do software falha.  

- Se o ID do pacote contiver caracteres minúsculos, a instalação do software falha.  

- Se a sequência de tarefas não encontrar uma variável com o nome base especificado e sufixo "001", a sequência de tarefas não instala quaisquer pacotes. A sequência de tarefas continua.  

> [!Important]  
> Estes valores são sensíveis aos casos. Por exemplo, "instalar" é diferente de "Instalar". Se precisar de alterar o valor, o editor da sequência de tarefas não deteta uma mudança de caso. Faça outra edição ao mesmo tempo, por exemplo, modifique a descrição do passo.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Se a instalação de um pacote de software falhar, continuar a instalar outros pacotes na lista

Esta definição especifica que o passo continuará se a instalação de um pacote de software individual falhar. Se especificar esta definição, a sequência de tarefas continua independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a>Instalar atualizações de software

Utilize este passo para instalar atualizações de software no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que este passo de sequência de tarefas seja executado. Nessa altura, o computador de destino é avaliado para atualizações de software como qualquer outro cliente do Gestor de Configuração. Para este passo para instalar atualizações de software, primeiro implemente as atualizações para uma coleção da qual o computador-alvo é membro.  

> [!IMPORTANT]  
> Para melhor desempenho, instale a versão mais recente do Windows Update Agent.  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Software**, e selecione **Instalar Atualizações**de Software .

### <a name="variables-for-install-software-updates"></a>Variáveis para instalar atualizações de software

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Se o cliente não conseguir recuperar a lista de pontos de gestão dos serviços de localização, utilize as variáveis **SMSTSMPListRequestTimeoute** e **SMSTSMPListRequestTimeout.** Estas variáveis especificam quantos milissegundos uma sequência de tarefas espera antes de voltar a instalar uma aplicação ou atualização de software. Para obter mais informações, consulte variáveis de sequência de [tarefas](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Cmdlets para instalar atualizações de software

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps)
- [New-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps)
- [Remover cmtsstepinstalarupdate](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps)
- [Set-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps)

Para mais recomendações e um diagrama de gráfico de fluxo técnico para este passo, consulte [Instalar Atualizações](install-software-updates.md)de Software .

### <a name="properties-for-install-software-updates"></a>Propriedades para instalar atualizações de software

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Necessário para instalação - apenas atualizações de software obrigatórias

Selecione esta opção para instalar todas as atualizações obrigatórias de software com prazos de instalação definidos pelo administrador.  

#### <a name="available-for-installation---all-software-updates"></a>Disponível para instalação - todas as atualizações de software

Selecione esta opção para instalar todas as atualizações de software disponíveis. Primeiro implemente estas atualizações para uma coleção da qual o computador é membro. A sequência de tarefas instala todas as atualizações de software disponíveis nos computadores de destino.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Avaliar atualizações de software a partir de resultados de análise em cache

Por predefinição, este passo utiliza resultados de digitalização em cache do Agente de Atualização do Windows. Desative esta opção para instruir o Agente de Atualização do Windows a descarregar o mais recente catálogo a partir do ponto de atualização do software. Ative esta opção ao utilizar uma sequência de tarefas para [capturar e construir uma imagem de OS](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Um grande número de atualizações de software é provável neste cenário.

Muitas destas atualizações têm dependências. Por exemplo, instale a atualização ABC antes da atualização XYZ aparecer conforme aplicável. Quando desativa esta definição e implementa a sequência de tarefas para muitos clientes, todos eles se ligam ao ponto de atualização do software ao mesmo tempo. Este comportamento resulta em problemas de desempenho durante o processo e download do catálogo de atualizações.

Na maioria das circunstâncias, utilize a definição predefinida para utilizar resultados de digitalização em cache.

A variável **SMSTSSoftwareUpdateScanTimeout** controla as atualizações de software durante este passo. O valor padrão é de 60 minutos. Para obter mais informações, consulte variáveis de sequência de [tarefas](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Opções para instalar atualizações de software

Além das opções predefinidas, configure as seguintes definições adicionais no separador **Opções** deste passo de sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Tente novamente este passo se o computador reiniciar inesperadamente

Se uma das atualizações reiniciar inesperadamente o computador, tente novamente este passo. O passo permite esta definição por defeito com duas repetições. Pode especificar de um a cinco repetições.  

> [!NOTE]  
> Configure a variável **SMSTSWaitForSecondReboot** para especificar quantos segundos a sequência de tarefas pausa após o computador reiniciar neste cenário. Para obter mais informações, consulte variáveis de sequência de [tarefas](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a>Junte-se ao Domínio ou ao Grupo de Trabalho

Use este passo para adicionar o computador de destino a um grupo de trabalho ou domínio.  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **General**, e selecione **Join Domain ou Workgroup**.

### <a name="variables-for-join-domain-or-workgroup"></a>Variáveis para integrar domínio ou grupo de trabalho

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Cmdlets para integrar domínio ou grupo de trabalho

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Novo GRUPO CMTSStepJoinDomainWork](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Remover CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Set-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps)

### <a name="properties-for-join-domain-or-workgroup"></a>Propriedades para Join Domain ou Workgroup

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="join-a-workgroup"></a>Aderir a um grupo de trabalho

Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Se o computador for atualmente membro de um domínio, a seleção desta opção faz com que o computador reinicie.  

#### <a name="join-a-domain"></a>Aderir a um domínio

Selecione esta opção para associar o computador de destino ao domínio especificado.  

Opcionalmente, introduza ou procure uma unidade organizacional (UO) no domínio especificado para o computador ser associado. Se o computador for atualmente membro de algum outro domínio ou de um grupo de trabalho, esta opção faz com que o computador reinicie. Se o computador já for membro de outro OU, uma vez que os Serviços de Domínio de Diretório Ativo não permitem alterar a OU através deste método, o Windows Setup ignora esta definição.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Introduzir a conta com permissões para ser associada ao domínio

Selecione **Definir** para introduzir o nome de utilizador e a palavra-passe para uma conta com permissões para aderir ao domínio. Insira a conta `Domain\account`no formato: . Para obter mais informações sobre a conta de junção do domínio da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)consulte Contas .  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a>Prepare o Cliente ConfigMgr para captura

Utilize este passo para remover ou configurar o cliente do Gestor de Configuração no computador de referência. Esta ação prepara o computador para ser capturado como parte do processo de imagem.

Este passo remove completamente o cliente do Gestor de Configuração, em vez de apenas remover informações chave. Quando a sequência de tarefas implanta a imagem de OS capturada, instala sempre um novo cliente do Gestor de Configuração.  

> [!Note]  
> O motor de sequência de tarefas apenas remove o cliente durante a Construção e captura uma sequência de tarefade imagem do **sistema operativo de referência.** O motor de sequência de tarefas não remove o cliente durante outros métodos de captura, tais como meios de captura ou uma sequência de tarefas personalizada.  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens,** e selecione Prepare o **Cliente ConfigMgr para capturar**.

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Cmdlets para preparar cliente ConfigMgr para captura

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Novo CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Remover CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Set-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a>Prepare janelas para captura

Utilize este passo para especificar as opções de Sysprep ao capturar uma imagem de SO no computador de referência. Este passo executa o Sysprep e, em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas. Esta ação falha se o computador de referência estiver unido a um domínio.  

Este passo funciona apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens**e selecione **Prepare o Windows para capturar**.

### <a name="variables-for-prepare-windows-for-capture"></a>Variáveis para preparar janelas para captura

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Cmdlets para preparar janelas para captura

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps)
- [Novos CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps)
- [Remover CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps)
- [Set-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps)

### <a name="properties-for-prepare-windows-for-capture"></a>Propriedades para preparar janelas para captura

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Compilar automaticamente a lista de controladores de armazenamento de massa

Selecione esta opção para o Sysprep compilar automaticamente uma lista de controladores de armazenamento em massa a partir do computador de referência. Esta opção ativa a opção Compilar Controladores de Armazenamento em Massa no ficheiro sysprep.inf no computador de referência. Para mais informações sobre este cenário, consulte a documentação da Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Não repor o sinalizador de ativação

Selecione esta opção para impedir o Sysprep de repor o sinalizador de ativação do produto.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Desligue o computador depois de executar esta ação

<!--SCCMDocs-pr issue 2695-->
Esta opção instrui a Sysprep a desligar o computador em vez do seu comportamento de reinício predefinido.

O Windows Autopilot para a sequência de tarefas dos [dispositivos existentes](../deploy-use/windows-autopilot-for-existing-devices.md) utiliza este passo com esta opção.

- Se pretender que a sequência de tarefas refresque o dispositivo e, em seguida, inicie imediatamente o OOBE para o Autopilot, deixe esta opção desligada.  

- Ative esta opção de desligar o dispositivo após a imagem. Depois pode entregar o dispositivo a um utilizador, que inicia o OOBE com Autopilot quando o ligar pela primeira vez.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a>Pré-provisionamento BitLocker

Utilize este passo para ativar o BitLocker numa unidade enquanto estiver no Windows PE. Por padrão, apenas o espaço de acionamento usado é encriptado, por isso os tempos de encriptação são muito mais rápidos. Aplica as opções de gestão chave utilizando o passo [Enable BitLocker](#BKMK_EnableBitLocker) após a instalação do SISTEMA.

> [!IMPORTANT]
> O BitLocker de pré-fornecimento requer que o computador tenha um Módulo de Plataforma Fidedigna suportado e ativado (TPM).

Este passo é executado apenas no Windows PE. Não funciona em todo o sistema operativo.  

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **Discos,** e selecione **BitLocker pré-provisionado**.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Cmdlets para Pré-provision BitLocker

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepofflineenablebitlocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [New-CMTSStepofflineenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Remover CMTSStepofflineenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepofflineenablebitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps)

### <a name="properties-for-pre-provision-bitlocker"></a>Propriedades para Pré-provision BitLocker

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Aplicar BitLocker à unidade especificada

Especifique a unidade para a qual pretende ativar o BitLocker. O BitLocker apenas encripta o espaço usado na unidade.  

#### <a name="use-full-disk-encryption"></a>Use encriptação completa do disco

<!--SCCMDocs-pr issue 2671-->
Por predefinição, este passo apenas encripta o espaço usado na unidade. Este comportamento padrão é recomendado, uma vez que é mais rápido e eficiente. Se a sua organização necessitar de encriptar toda a unidade durante a configuração, então ative esta opção. A Configuração do Windows aguarda que toda a unidade encripte, o que demora muito tempo, especialmente em grandes unidades.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Ignorar este passo em computadores que não têm TPM ou quando o TPM não está ativado

Selecione esta opção para ignorar a encriptação de acionamento num computador que não contenha um TPM suportado ou ativado. Por exemplo, utilize esta opção quando implementar um Sistema operativo para uma máquina virtual.  



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a>Livraria State Store

Use este passo para notificar o ponto de migração do Estado de que a ação de captura ou restauro está completa. Utilize este passo em conjunto com a **Loja do Estado de Pedido,** capture o Estado do **Utilizador**e **restaure** os passos do Estado do Utilizador. Utiliza estes passos para migrar dados do Estado do utilizador utilizando um ponto de migração do Estado e a Ferramenta de Migração do Estado utilizador (USMT).  

Para obter mais informações sobre a gestão do estado do utilizador ao implementar sistemas operativos, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  

Se utilizar o passo **da Loja do Estado de Pedido** para solicitar o acesso a um ponto de migração estatal para *capturar* o estado do utilizador, este passo notifica o ponto de migração do Estado de que o processo de captura está concluído. O ponto de migração do Estado marca então os dados do Estado do utilizador como disponíveis para restauro. O ponto de migração do Estado define as permissões de controlo de acesso para os dados do estado do utilizador, de modo que apenas o computador restaurador tem acesso apenas de leitura.  

Se utilizar a etapa da **Loja do Estado de Pedido** para solicitar o acesso a um ponto de migração estatal para *restaurar* o estado do utilizador, este passo notifica o ponto de migração do Estado de que o processo de restauro está concluído. O ponto de migração do Estado ativa então as definições de retenção de dados configuradas.  

> [!IMPORTANT]  
> Detete a opção **Continuar no Erro** para quaisquer passos entre as etapas da Loja **estatal de Depósito** supor e de lançamento da Loja **estatal.** Cada passo **da Loja estatal de Pedidos** deve ter um passo de **Liberação estatal** correspondente.  

Este passo funciona apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **User State**, e selecione Release **State Store**.

### <a name="variables-for-release-state-store"></a>Variáveis para Lançamento Da Loja do Estado

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Cmdlets para Lançamento Da State Store

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepreleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps)
- [New-CMTSStepreleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps)
- [Remover CMTSStepreleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps)
- [Set-CMTSStepreleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps)

### <a name="properties-for-release-state-store"></a>Propriedades para Lançamento State Store

Este passo não requer definições no separador **Propriedades.**



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a>Solicitar loja estatal

Use este passo para solicitar o acesso a um ponto de migração do Estado ao capturar ou restaurar o Estado.  

Para obter mais informações sobre a gestão do estado do utilizador ao implementar sistemas operativos, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  

Utilize este passo em conjunto com a Loja do Estado de **Lançamento,** capture o **Estado do Utilizador**e **restaure** os passos do Estado do Utilizador. Utiliza estes passos para migrar o estado informático utilizando um ponto de migração do Estado e a Ferramenta de Migração do Estado utilizador (USMT).  

> [!NOTE]  
> Ao criar um novo ponto de migração do Estado, o armazenamento do Estado dos utilizadores não está disponível até uma hora. Para acelerar a disponibilidade, ajuste quaisquer definições de propriedade no ponto de migração do estado para desencadear uma atualização de ficheirode controlo do site.  

Este passo funciona em todo o SISTEMA e no Windows PE para USMT offline.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **User State**, e selecione Request **State Store**.

### <a name="variables-for-request-state-store"></a>Variáveis para Pedido De Loja do Estado

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Cmdlets para Loja Estatal de Pedido

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps)
- [New-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps)
- [Remover CMTSStepRequestRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps)
- [Set-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps)

### <a name="properties-for-request-state-store"></a>Imóveis para Pedido State Store

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="capture-state-from-the-computer"></a>Capturar estado a partir do computador

Encontre um ponto de migração estatal que cumpra os requisitos mínimos configurados nas definições do ponto de migração do Estado. Por exemplo, **Número máximo de clientes** e quantidade mínima de espaço em disco **livre**. Esta opção não garante que haja espaço suficiente no momento da migração do Estado. Esta opção solicita o acesso ao ponto de migração do Estado com o objetivo de capturar o estado do utilizador e as definições de um computador.  

Se o site do Gestor de Configuração tiver vários pontos de migração ativos do Estado, este passo encontra um ponto de migração estatal com espaço de disco disponível. A sequência de tarefas questiona o ponto de gestão de uma lista de pontos de migração do Estado, e avalia cada um até encontrar um que cumpra os requisitos mínimos.  

#### <a name="restore-state-from-another-computer"></a>Restaurar estado a partir de outro computador

Solicite o acesso a um ponto de migração estatal para restaurar o estado de utilizador previamente capturado e as configurações para um computador de destino.  

Se houver vários pontos de migração do Estado, este passo encontra o ponto de migração do Estado que tem o estado para o computador de destino.  

#### <a name="number-of-retries"></a>Número de tentativas

O número de vezes que este passo tenta encontrar um ponto de migração estatal apropriado antes de falhar.  

#### <a name="retry-delay-in-seconds"></a>Intervalo de repetição (em segundos)

Período de tempo em segundos que o passo de sequência de tarefas aguarda entre as tentativas.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Se a conta de computador não ligar a uma loja estatal, utilize a conta de acesso à rede

Se a sequência de tarefas não conseguir aceder ao ponto de migração do Estado utilizando a conta de computador, utiliza as credenciais da conta de acesso à rede para se ligar. Esta opção é menos segura porque outros computadores poderiam usar a conta de acesso à rede para aceder ao estado armazenado. Esta opção pode ser necessária se o computador de destino não for de domínio.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a>Reiniciar computador

Utilize este passo para reiniciar a sequência de tarefas do computador. Após o reinício, o computador continua automaticamente com o próximo passo na sequência de tarefas.  

Este passo pode ser executado em todos os SISTEMAs operativos ou windows PE.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **General**, e selecione **Restart Computer**.

### <a name="variables-for-restart-computer"></a>Variáveis para reiniciar computador

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Cmdlets para reiniciar computador

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps)
- [New-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps)
- [Remover CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps)
- [Set-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps)

### <a name="properties-for-restart-computer"></a>Propriedades para reiniciar computador

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>A imagem de arranque atribuída a esta sequência de tarefas

Selecione esta opção para o computador de destino utilizar a imagem de arranque atribuída à sequência de tarefas. A sequência de tarefas utiliza a imagem do arranque para executar passos subsequentes no Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>O sistema operativo predefinido atualmente instalado

Selecione esta opção para o computador de destino reiniciar no SISTEMA instalado.  

#### <a name="notify-the-user-before-restarting"></a>Notificar o utilizador antes de reiniciar

Selecione esta opção para apresentar uma notificação ao utilizador antes do computador de destino reiniciar. O passo seleciona esta opção por padrão.  

#### <a name="notification-message"></a>Mensagem de notificação

Introduza uma mensagem de notificação para mostrar ao utilizador antes do computador de destino reiniciar.  

#### <a name="message-display-time-out"></a>Tempo limite de visualização da mensagem

Especifique a quantidade de tempo em segundos antes do computador de destino reiniciar. O padrão é de 60 segundos.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a>Restaurar o Estado do Utilizador

Utilize este passo para iniciar a Ferramenta de Migração do Estado utilizador (USMT) para restaurar o estado do utilizador e as definições para o computador de destino. Utilize este passo em conjunto com o passo **do Estado do Utilizador de Captura.**  

Para obter mais informações sobre a gestão do estado do utilizador ao implementar sistemas operativos, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  

Utilize este passo com as etapas da **Loja estatal de Depósito de Pedido** e de **Lançamento** para guardar ou restaurar as definições do Estado com um ponto de migração estatal. Esta opção desencripta sempre a loja estatal USMT utilizando uma chave de encriptação que o Gestor de Configuração gera e gere.  

O passo **do Estado do Utilizador restaurar** fornece controlo sobre um subconjunto limitado das opções USMT mais usadas mais comumente usadas. Especifique opções adicionais de linha de comando com a variável **OSDMigrateAdicionalRestoreRestoreOptions.**  

> [!IMPORTANT]  
> Se estiver a utilizar este passo para uma finalidade não relacionada com um cenário de implementação do SISTEMA, adicione o passo [do Computador Restart](#BKMK_RestartComputer) imediatamente após o passo do Estado do Utilizador **restaurar.**  

Este passo funciona apenas em todo o Sistema Operativo. Não funciona no Windows PE.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **User State**, e selecione Restaurar o Estado **do Utilizador**.

### <a name="variables-for-restore-user-state"></a>Variáveis para restaurar o estado do utilizador

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Cmdlets para restaurar o estado do utilizador

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreuserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps)
- [Novo CMTSStepRestoreuserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps)
- [Remover CMTSStepRestoreuserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps)
- [Set-CMTSStepRestoreuserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps)

### <a name="properties-for-restore-user-state"></a>Propriedades para restaurar o estado do utilizador

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="user-state-migration-tool-package"></a>Pacote do User State Migration Tool

Especifique o pacote que contém a versão do USMT para este passo a utilizar. Este pacote não requer um programa. Quando o passo corre, a sequência de tarefas utiliza a versão do USMT no pacote especificado. Especifique um pacote que contenha a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do SO para a qual a sequência de tarefas está a restaurar o estado.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Restaurar todos os perfis de utilizador capturados com opções padrão

Restaura todos os perfis de utilizador capturados com as opções padrão. Para personalizar as opções que o USMT restaura, selecione Personalizar a captura do perfil do **utilizador**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Personalizar como os perfis de utilizador são restaurados

Permite personalizar os ficheiros que pretende restaurar para o computador de destino. Selecione **Ficheiros** para especificar os ficheiros de configuração no pacote USMT que pretende utilizar para restaurar os perfis do utilizador. Para adicionar um ficheiro de configuração, introduza o nome do ficheiro na caixa de nome de **ficheiros** e, em seguida, selecione **Adicionar**. O painel de Ficheiros lista os ficheiros de configuração que o USMT utiliza. O ficheiro .xml que especifica define qual o ficheiro usmt do utilizador que restaura.  

#### <a name="restore-local-computer-user-profiles"></a>Restaurar perfis de utilizador do computador local

Restaura os perfis de utilizador do computador local. Estes perfis não são para utilizadores de domínio. Atribuir novas palavras-passe às contas de utilizador locais restauradas. UsMT não pode migrar as senhas originais. Introduza a nova palavra-passe na caixa **Palavra-passe** e confirme-a na caixa **Confirmar Palavra-passe**.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continuar se não for possível restaurar alguns ficheiros

Continua a restaurar o estado e as definições do utilizador mesmo que o USMT não consiga restaurar alguns ficheiros. O passo permite esta opção por defeito. Se desativar esta opção, e usmt encontrar erros ao restaurar ficheiros, este passo falha imediatamente. UsMT não restaura todos os ficheiros.

#### <a name="enable-verbose-logging"></a>Ativar registo verboso

Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao restaurar o estado, a sequência de tarefa por padrão gera `%WinDir%\ccm\logs` **Loadstate.log** na pasta de registo da sequência de tarefas, .  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a>Linha de Comando executar

Utilize este passo para executar a linha de comando especificada.  

Este passo pode ser executado em todo o SISTEMA ou Windows PE.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **General**, e selecione Executar Linha de **Comando**.

### <a name="variables-for-run-command-line"></a>Variáveis para linha de comando de execução

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (a partir da versão 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SmstsrunCommandlineuserpassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (a partir da versão 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Cmdlets para linha de comando de execução

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandline](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps)
- [Linha de Comando new-CMTSStepRun](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps)
- [Remover cmtsstepruncommandline](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps)
- [Set-CMTSStepRunCommandline](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps)

### <a name="properties-for-run-command-line"></a>Propriedades para Linha de Comando de Execução

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="command-line"></a>Linha de comandos

Especifica a linha de comando que a sequência de tarefas funciona. Este campo é obrigatório. Inclua extensões de nome de ficheiro, por exemplo, .vbs e .exe. Inclua todos os ficheiros de definições necessários e opções de linha de comando.  

Se não especificar a extensão do nome do ficheiro, o Gestor de Configuração tenta .com, .exe e .bat. Se o nome do ficheiro tiver uma extensão que não seja um tipo executável, o Gestor de Configuração tenta aplicar uma associação local. Por exemplo, se a linha de comando for readme.gif, o Gestor de Configuração inicia a aplicação especificada no computador de destino para a abertura de ficheiros .gif.  

Exemplos:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Para correr com sucesso, precede as ações da linha de comando com o comando **cmd.exe /c.** Exemplo destas ações incluem redirecionamento de saída, tubagem e comandos de cópia.  

#### <a name="output-to-task-sequence-variable"></a>Variável de sequência de tarefas

<!--user story 4977616/bug 4798352-->

A partir da versão 1910, guarde a saída de comando para uma variável de sequência de tarefas personalizada.

> [!Note]  
> O Gestor de Configuração limita esta saída aos últimos 1000 caracteres.

#### <a name="disable-64-bit-file-system-redirection"></a>Desativar redirecionamento de sistema de ficheiros de 64 bits

Por predefinição, os sistemas operativos de 64 bits utilizam o redirector do sistema de ficheiros WOW64 para executar linhas de comando. Este comportamento é encontrar adequadamente versões de 32 bits de executáveis e bibliotecas de SO. Selecione esta opção para desativar a utilização do redirector do sistema de ficheiros WOW64. O Windows executa o comando utilizando versões nativas de 64 bits de executáveis e bibliotecas de SO. Esta opção não tem qualquer efeito ao correr num Sistema Operativo de 32 bits.  

#### <a name="start-in"></a>Iniciar em

Especifica a pasta executável do programa, até 127 carateres. Esta pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote. Este campo é opcional.  

Exemplos:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> O botão **Browse** navega no computador local para ficheiros e pastas. Tudo o que selecionar também deve existir no computador de destino. Deve existir no mesmo local e com os mesmos nomes de ficheiros e pastas.  

#### <a name="package"></a>Pacote

Quando especificar ficheiros ou programas na linha de comando que ainda não estão presentes no computador de destino, selecione esta opção para especificar o pacote 'Gestor de Configuração' que contém os ficheiros necessários. O pacote não requer um programa. Se os ficheiros especificados existirem no computador de destino, esta opção não é necessária.  

#### <a name="time-out"></a>Limite de Tempo Excedido

Especifica um valor que representa o tempo de funcionação do Gestor de Configuração. Este valor pode ir de um minuto a 999 minutos. O valor predefinido é 15 minutos. Esta opção está desativada por predefinição.  

> [!IMPORTANT]  
> Se introduzir um valor que não permite tempo suficiente para que o comando especificado esteja concluído com sucesso, este passo falha. Toda a sequência de tarefas pode falhar dependendo das condições de passo ou de grupo. Se o prazo expirar, o Gestor de Configuração termina o processo da linha de comando.  

#### <a name="run-this-step-as-the-following-account"></a>Executar este passo de acordo com a seguinte conta

Especifica que a linha de comando é executada como uma conta de utilizador do Windows diferente da conta do Sistema Local.  

> [!NOTE]  
> Para executar scripts ou comandos simples com outra conta após a instalação do SISTEMA, adicione primeiro a conta ao computador. Além disso, poderá ser necessário restaurar os perfis de utilizador do Windows para executar programas mais complexos, como um Instalador windows.  

#### <a name="account"></a>Conta

Especifica a conta de utilizador do Windows que este passo utiliza para executar a linha de comando. A linha de comando funciona com as permissões da conta especificada. Selecione **Definir** para especificar o utilizador local ou a conta de domínio. Para obter mais informações sobre a conta de execução da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)consulte contas .

> [!IMPORTANT]  
> Se este passo especificar uma conta de utilizador e correr no Windows PE, a ação falha. Não pode aderir ao Windows PE a um domínio. O ficheiro **smsts.log** regista esta falha.  

### <a name="options-for-run-command-line"></a>Opções para Linha de Comando de Execução

Além das opções predefinidas, configure as seguintes definições adicionais no separador **Opções** deste passo de sequência de tarefas:  

#### <a name="success-codes"></a>Códigos de sucesso

Inclua outros códigos de saída do script que o passo deve avaliar como sucesso.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a>Executar o script PowerShell

Utilize este passo para executar o script especificado do Windows PowerShell.  

Este passo pode ser executado em todo o SISTEMA ou Windows PE. Para executar este passo no Windows PE, ative o PowerShell na imagem de arranque. Ative o componente WinPE-PowerShell a partir do separador **Componentes Opcionais** nas propriedades para a imagem de arranque. Para obter mais informações sobre como modificar uma imagem de arranque, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

> [!NOTE]  
> O PowerShell não está ativado por padrão nos sistemas operativos Windows Embedded.  

> [!WARNING]
> Certos softwares anti-malware podem inadvertidamente desencadear eventos contra o passo de sequência de tarefas do PowerShell Script do Gestor de Configuração. Recomenda-se excluir %windir%\temp\smstspowershellscripts para que o software anti-malware permita que esses scripts executem sem interferência.

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **General**, e selecione **Executar PowerShell Script**.

### <a name="variables-for-run-powershell-script"></a>Variáveis para executar o script PowerShell

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (a partir da versão 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (a partir da versão 2002)<!-- 5573175 -->
- [SmstsrunPowerShelluserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShelluserpassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Cmdlets para executar o script PowerShell

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellscript](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps)
- [New-CMTSStepRunPowerShellscript](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps)
- [Remover CMTSStepRunPowerShellscript](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps)
- [Set-CMTSStepRunPowerShellscript](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps)

> [!Note]  
> Utilize scripts PowerShell assinados em formato Unicode. O formato ANSI, que é o padrão, não funciona com este passo.

### <a name="properties-for-run-powershell-script"></a>Propriedades para Executar PowerShell Script

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="package"></a>Pacote

Especifique o pacote 'Gestor de Configuração' que contém o script PowerShell. Um pacote pode conter vários scripts do PowerShell.  

#### <a name="script-name"></a>Nome do script

Especifica o nome do script do PowerShell a executar. Este campo é obrigatório.  

#### <a name="enter-a-powershell-script"></a>Introduza um script PowerShell

<!-- 3556028 -->
A partir da versão 1902, introduza diretamente o código PowerShell do Windows neste passo. Esta funcionalidade permite-lhe executar comandos PowerShell durante uma sequência de tarefas sem primeiro criar e distribuir um pacote com o script.

Quando adiciona ou edita um script, a janela de script PowerShell fornece as seguintes ações:  

- Editar o script diretamente  

- Abra um script existente a partir de arquivo  

- Navegue por um [script](../../apps/deploy-use/create-deploy-scripts.md) aprovado existente no Gestor de Configuração

> [!Important]  
> Para aproveitar esta nova funcionalidade de Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

#### <a name="parameters"></a>Parâmetros

Especifica os parâmetros passados para o script PowerShell. Estes parâmetros são os mesmos que os parâmetros do script PowerShell na linha de comando.  

Forneça parâmetros consumidos pelo script e não para a linha de comandos do Windows PowerShell.  
O exemplo seguinte contém parâmetros válidos:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

O exemplo seguinte contém parâmetros inválidos. Os dois primeiros itens são os parâmetros da linha de comando Windows PowerShell **(-NoLogo** e **-ExecutionPolicy Unrestricted**). O guião não consome estes parâmetros.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Se um valor de parâmetro incluir um carácter`'`especial, utilize aspas únicas () em torno do valor. A utilização de`"`marcas duplas de aspas pode fazer com que o passo da sequência de tarefas processe incorretamente o parâmetro.

Por exemplo: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

A partir da versão 2002, deteteto esta propriedade como uma variável.<!-- 5690481 --> Por exemplo, se `%MyScriptVariable%`especificar , quando a sequência de tarefas executa o script, adiciona o valor desta variável personalizada à linha de comando PowerShell.

#### <a name="powershell-execution-policy"></a>Política de execução do PowerShell

Determine quais os scripts PowerShell (se houver) que permite executar no computador. Escolha uma das seguintes políticas de execução:  

- **AllSigned**: Apenas executar scripts assinados por um editor de confiança  

- **Indefinido**: Não defina nenhuma política de execução  

- **Bypass**: Carregue todos os ficheiros de configuração e execute todos os scripts. Se descarregar um script não assinado a partir da internet, o Windows PowerShell não solicita permissão antes de executar o script.  

> [!IMPORTANT]  
> PowerShell 1.0 não suporta políticas de execução indefinidas e de bypass.  

#### <a name="output-to-task-sequence-variable"></a>Variável de sequência de tarefas

<!-- 3556028 -->
A partir da versão 1902, guarde a saída do script para uma variável de sequência de tarefas personalizada.

> [!Note]  
> A partir da versão 1910, o Gestor de Configuração limita esta saída aos últimos 1000 caracteres.

Para um exemplo de como usar esta propriedade passo, veja [como definir variáveis](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Iniciar em

<!-- 3556028 -->
A partir da versão 1902, especifique a pasta inicial para o script, até 127 caracteres. Esta pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote. Este campo é opcional.  

> [!NOTE]  
> O botão **Browse** navega no computador local para ficheiros e pastas. Tudo o que selecionar também deve existir no computador de destino. Deve existir no mesmo local e com os mesmos nomes de ficheiros e pastas.  

#### <a name="time-out"></a>Limite de Tempo Excedido

<!-- 3556028 -->
A partir da versão 1902, especifique um valor que represente o tempo que o Gestor de Configuração permite que o script PowerShell seja executado. Este valor pode ir de um minuto a 999 minutos. O valor predefinido é 15 minutos. Esta opção está desativada por predefinição.  

> [!IMPORTANT]  
> Se introduzir um valor que não permite tempo suficiente para que o script especificado esteja concluído com sucesso, este passo falha. Toda a sequência de tarefas pode falhar dependendo das condições de passo ou de grupo. Se o prazo expirar, o Gestor de Configuração termina o processo PowerShell.  

#### <a name="run-this-step-as-the-following-account"></a>Executar este passo de acordo com a seguinte conta

<!-- 3556028 -->
A partir da versão 1902, especifique que o script PowerShell é executado como uma conta de utilizador do Windows diferente da conta do Sistema Local.  

> [!NOTE]  
> Para executar scripts ou comandos simples com outra conta após a instalação do SISTEMA, adicione primeiro a conta ao computador. Além disso, poderá ser necessário restaurar os perfis de utilizador do Windows para executar ações mais complexas.  

#### <a name="account"></a>Conta

<!-- 3556028 -->
A partir da versão 1902, especifique a conta de utilizador do Windows que este passo utiliza para executar o script PowerShell. A conta especificada deve ser um administrador local no sistema e o script executa com as permissões desta conta. Selecione **Definir** para especificar o utilizador local ou a conta de domínio. Para obter mais informações sobre a conta de execução da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)consulte contas .

> [!IMPORTANT]  
> Se este passo especificar uma conta de utilizador e correr no Windows PE, a ação falha. Não pode aderir ao Windows PE a um domínio. O ficheiro **smsts.log** regista esta falha.  

### <a name="options-for-run-powershell-script"></a>Opções para Executar PowerShell Script

Além das opções predefinidas, configure as seguintes definições adicionais no separador **Opções** deste passo de sequência de tarefas:  

#### <a name="success-codes"></a>Códigos de sucesso

<!-- 3556028 -->
A partir da versão de 1902, incluem outros códigos de saída do script que o passo deve avaliar como sucesso.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a>Executar sequência de tarefas

> [!Note]  
> Na versão 1910, o Gestor de Configuração permite esta funcionalidade por padrão. Na versão 1906 ou anterior, o Gestor de Configuração não permite esta funcionalidade opcional por padrão. Ative esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

Este passo executa outra sequência de tarefas. Cria uma relação pai-filho entre as sequências de tarefas. Com sequências de tarefas infantis, pode criar sequências de tarefas mais modulares e reutilizáveis.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **General**, e selecione Executar sequência de **tarefas**.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Especificações e limitações para sequência de tarefas de execução

Considere os seguintes pontos quando adicionar uma sequência de tarefas para crianças a uma sequência de tarefas:  

- As sequências de tarefas dos pais e das crianças são efetivamente combinadas numa única política que o cliente executa.  

- O ambiente é global. Se a sequência de tarefas dos pais definir uma variável, e então a sequência de tarefas da criança mudar essa variável, ela mantém o valor mais recente. Se a sequência de tarefas da criança criar uma nova variável, está disponível para o resto da sequência de tarefas dos pais.  

- As mensagens de estado são enviadas normalmente para uma única operação de sequência de tarefas.  

- A sequência de tarefas escreve entradas no ficheiro **smsts.log,** com novas entradas de registo que deixam claro quando uma sequência de tarefas infantil começa.  

<!--the following points are from SCCMdocs issue #1079-->

- Não é possível selecionar uma sequência de tarefas com uma referência de imagem de arranque. Para qualquer implementação que exija uma imagem de arranque, especifique-a na sequência de tarefas dos pais.  

- Se uma sequência de tarefas para crianças for desativada, a colocação falha. Não pode utilizar a opção **continue a** trabalhar em torno desta limitação.  

- Se uma sequência de tarefas para crianças contiver passos considerados *de alto impacto,* o Software Center não a deteta e mostra a notificação de alto impacto. Modifique as propriedades da sequência de tarefas dos pais, no separador Notificação do Utilizador, para especificar que **se trata de uma sequência de tarefas de alto impacto**.  

- Se uma sequência de tarefas para crianças tiver uma referência de pacote em falta, ver a sequência de tarefas dos pais não deteta este estado. Se editar a sequência de tarefas dos pais, deteta quaisquer referências em falta nas sequências de tarefas da criança quando faz alterações no progenitor.  

### <a name="cmdlets-for-run-task-sequence"></a>Cmdlets para executar sequência de tarefas

A partir da versão 1906, gerencie este passo com os seguintes cmdlets PowerShell:<!-- 2839943, SCCMDocs#1118 -->

- **Get-CMTSStepRunTaskSequence**
- **Nova CMTSStepRunTaskSequence**
- **Remover cmtsstepruntasksequence**
- **Set-CMTSStepRunTaskSequence**

Para mais informações, consulte notas de lançamento de [1906 - Novos cmdlets](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Propriedades para sequência de tarefas de execução

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="select-task-sequence-to-run"></a>Selecione sequência de tarefas para executar

**Selecione Navegar** para selecionar a sequência de tarefas para crianças. A caixa de diálogo **Select a Task Sequence** não mostra a sequência de tarefas dos pais.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a>Definir Variáveis Dinâmicas

Utilize este passo para realizar as seguintes ações:  

1. Recolha informações do computador e do seu ambiente. Em seguida, definir variáveis de sequência de tarefa especificadas com a informação.  

2. Avaliar regras definidas. Detete variáveis de sequência de tarefas com base nas regras que avaliam verdadeiramente.  

Este passo pode ser executado em todos os SISTEMAs operativos ou windows PE.  

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **General**, e selecione set **Dynamic Variables**.

### <a name="variables-for-set-dynamic-variables"></a>Variáveis para definir variáveis dinâmicas

A sequência de tarefas define automaticamente as seguintes variáveis de sequência de tarefas só de leitura:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresss](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_Número de Série SMSTS](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssettag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Cmdlets para definir variáveis dinâmicas

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Nova CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Remover CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Set-CMTSStepSetDynamicvariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps)

### <a name="properties-for-set-dynamic-variables"></a>Propriedades para definir variáveis dinâmicas

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="dynamic-rules-and-variables"></a>Regras e variáveis dinâmicas

Para definir uma variável dinâmica para utilização na sequência de tarefas, adicione uma regra. Em seguida, detete um valor para cada variável especificada na regra. Adicionalmente, adicione uma ou mais variáveis sem adicionar uma regra. Quando adicionar uma regra, escolha entre as seguintes categorias:  

- **Computador:** Avaliar valores para etiqueta de ativo de hardware, UUID, número de série ou endereço MAC. Definir vários valores conforme necessário. Se algum valor for verdadeiro, então a regra avalia como verdadeira. Por exemplo, a seguinte regra avalia como verdadeira se o número de série do dispositivo for 5892087 e o endereço MAC for 22-A4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Localização**: Avaliar valores para o gateway de rede predefinido  

- **Make and Model**: Avaliar valores para a transformação e modelo de um computador. A marca e o modelo têm de avaliar como verdadeiro para a regra avaliar como verdadeiro.

    Especifique um`*`asterisco`?`() e um ponto de interrogação ( ) como caracteres de cartas selvagens. O asterisco corresponde a vários caracteres e o ponto de interrogação corresponde a um único personagem. Por exemplo, `DELL*900?` a `DELL-ABC-9001` corda `DELL9009`combina tanto com a .  

- **Variável de sequência**de tarefas : Adicione uma variável de sequência de tarefas, condição e valor para avaliar. A regra avalia como verdadeiro quando o conjunto de valores da variável cumpre a condição especificada.  

    Especifique uma ou mais variáveis para definir para uma regra que avalie as variáveis verdadeiras ou que estabeleça variáveis sem usar uma regra. Selecione uma variável existente ou crie uma variável personalizada.  

    - **Variáveis de sequência de tarefas existentes:** Selecione uma ou mais variáveis a partir de uma lista de variáveis de sequência de tarefas existentes. Variáveis de matriz não estão disponíveis para selecionar.  

    - **Variáveis de sequência de tarefas personalizadas**: Defina uma variável de sequência de tarefas personalizada. Também pode especificar uma variável de sequência de tarefas existente. Esta definição é útil para especificar uma matriz variável existente, como o **OSDAdapter,** uma vez que as matrizes variáveis não estão na lista de variáveis de sequência de tarefas existentes.  

Depois de selecionar as variáveis para uma regra, forneça um valor para cada variável. A variável é definida para o valor especificado quando a regra avalia como verdadeiro. Para cada variável, pode selecionar **Valor secreto** para ocultar o valor da variável. Por padrão, algumas variáveis existentes escondem valores, como a variável **OSDCaptureAccountPassword.**  

> [!IMPORTANT]  
> O Gestor de Configuração remove quaisquer valores variáveis marcados como um **valor secreto** quando importa uma sequência de tarefas com o passo set **Dynamic Variables.** Reintroduza o valor para a variável dinâmica depois de importar a sequência de tarefas.  



## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a>Definir variável de sequência de tarefas

Use este passo para definir o valor de uma variável que é usada com a sequência de tarefas.  

Este passo pode ser executado em todos os SISTEMAs operativos ou windows PE.

Para adicionar este passo no editor de sequência de tarefas, **selecione Adicionar**, selecione **General**, e selecione Definir Variável de sequência de **tarefas**.

### <a name="variables-for-set-task-sequence-variable"></a>Variáveis para variável de sequência de tarefas definidas

As variáveis de sequência de tarefas são lidas pelas ações de sequência de tarefas e especificam o comportamento dessas ações. Para obter mais informações sobre variáveis específicas da sequência de tarefas e como usá-las, consulte os seguintes artigos:  

- [Como utilizar variáveis de sequência de tarefas](using-task-sequence-variables.md)  
- [Variáveis de sequência de tarefas](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Cmdlets para definir variável de sequência de tarefa

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetvariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps)
- [Variável new-CMTSStepSetvariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps)
- [Remover cmtsstepsetvariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps)
- [Set-CMTSStepSetvariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps)

### <a name="properties-for-set-task-sequence-variable"></a>Propriedades para definir variável de sequência de tarefa

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="task-sequence-variable"></a>Variável da sequência de tarefas

Especifique o nome de uma sequência de tarefaincorporada ou variável de ação, ou especifique o seu próprio nome variável definido pelo utilizador.  

#### <a name="do-not-display-this-value"></a>Não exiba este valor

<!--1358330-->
Ative esta opção de mascarar dados sensíveis armazenados em variáveis de sequência de tarefas. Por exemplo, ao especificar uma palavra-passe.

> [!Note]  
> Ative esta opção e, em seguida, definir o valor da variável de sequência de tarefas. Caso contrário, o valor variável não está definido como pretende, o que pode causar comportamentos inesperados quando a sequência de tarefas corre.<!--SCCMdocs issue #800-->

#### <a name="value"></a>Valor  

A sequência de tarefas define a variável para este valor. Detete esta variável de sequência de tarefas `%varname%`para o valor de outra variável de sequência de tarefas com a sintaxe .  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a>Configurar janelas e ConfigMgr

Utilize este passo para realizar a transição do Windows PE para o novo SISTEMA. Este passo de sequência de tarefas é uma parte necessária de qualquer implantação de SO. Instala o cliente do Gestor de Configuração no novo SISTEMA, e prepara-se para que a sequência de tarefas continue a ser executada no novo SISTEMA.  

Este passo é responsável pela transição da sequência de tarefas do Windows PE para o sistema operativo completo. O passo corre tanto no Windows PE como no Sistema Operativo completo por causa desta transição. No entanto, uma vez que a transição começa no Windows PE, só pode ser adicionada durante a parte do Windows PE da sequência de tarefas.  

Este passo substitui variáveis de diretório sysprep.inf ou `%WINDIR%` unattend.xml, tais como e `%ProgramFiles%`, com o diretório de instalação do Windows PE, `X:\Windows`. A sequência de tarefas ignora as variáveis especificadas utilizando estas variáveis ambientais.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens**, e selecione **Setup Windows e ConfigMgr**.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Comportamentos para Configurar Janelas e ConfigMgr

Este passo executa as seguintes ações:  

#### <a name="preliminaries-windows-pe"></a>Preliminares: Windows PE  

1. Substitua variáveis de sequência de tarefas no ficheiro unattend.xml.  

2. Descarregue o pacote que contém o cliente do Gestor de Configuração. Adicione o pacote à imagem implantada.  

#### <a name="set-up-windows"></a>Configurar o Windows  

- Instalação baseada em imagem  

    1. Desative o cliente do Gestor de Configuração na imagem, se existir. Por outras palavras, desative o Autostart para o serviço de cliente do Gestor de Configuração.  

    2. Atualize o registo na imagem implementada para iniciar o SISTEMA implantado com a mesma letra de unidade que o computador de referência.  

    3. Reinicie para o Sistema operativo implantado.  

    4. A mini-configuração do Windows funciona utilizando o ficheiro de resposta sysprep.inf ou unattend.xml previamente especificado que tem todas as interações com o utilizador final suprimidas. Se utilizar o passo **de Definições** de Rede Aplicar para se juntar a um domínio, então essa informação está no ficheiro de resposta. A mini-configuração do Windows junta o computador ao domínio.  

- Instalação baseada em Setup.exe. Executa Setup.exe, que segue o processo de configuração normal do Windows:  

    1. Copie o pacote de atualização do SISTEMA OS, especificado na etapa do **Sistema Operativo Aplicar,** para a unidade de disco rígido.  

    2. Reinicie para o osso recém-implantado.  

    3. A mini-configuração do Windows funciona utilizando o ficheiro de resposta sysprep.inf ou unattend.xml previamente especificado que tem todas as definições de interface do utilizador suprimidas. Se utilizar o passo **de Definições** de Rede Aplicar para se juntar a um domínio, então essa informação está no ficheiro de resposta. A mini-configuração do Windows junta o computador ao domínio.  

#### <a name="set-up-the-configuration-manager-client"></a>Configurar o cliente do Gestor de Configuração  

1. Após a conclusão da miniconfiguração do Windows, a sequência de tarefas é retomada com o setupcomplete.cmd. Para mais informações, consulte Executar um script após a [configuração estar completa (ConfigurarComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. Ativar ou desativar a conta do Administrador local, com base na opção selecionada na fase **de Definições** do Windows.  

3. Instale o cliente do Gestor de Configuração utilizando o pacote previamente descarregado e as propriedades de instalação especificadas neste passo. O cliente instala-se em "modo de provisionamento". Este modo impede o cliente de processar novos pedidos de política até que a sequência de tarefas esteja concluída. Para mais informações, consulte [o modo de provisionamento](provisioning-mode.md).  

4. Espere que o cliente esteja totalmente operacional.  

#### <a name="the-step-completes"></a>O passo completa

A sequência de tarefas continua a correr o próximo passo.  

> [!Note]  
> A política do grupo Windows normalmente não é processada até que a sequência de tarefas esteja completa. Este comportamento é consistente em diferentes versões do Windows. Outras ações personalizadas durante a sequência de tarefas podem desencadear a avaliação da política do grupo. Para obter mais informações sobre a ordem de operações, consulte Executar um script após a [configuração estar concluída (ConfigurarComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Variáveis para Configurar Janelas e ConfigMgr

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Cmdlets para configurar janelas e ConfigMgr

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Novo CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Remover CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Set-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)

### <a name="properties-for-setup-windows-and-configmgr"></a>Propriedades para Configurar Janelas e ConfigMgr

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="client-package"></a>Pacote de cliente

Selecione **Browse**e, em seguida, escolha o pacote de instalação do cliente Do Gestor de Configuração para usar com este passo.  

#### <a name="use-pre-production-client-package-when-available"></a>Utilizar o pacote de cliente de pré-produção quando disponível

Se houver um pacote de clientes pré-produção disponível, e o computador for membro da coleção de pilotagem, a sequência de tarefas utiliza este pacote em vez do pacote de clientes de produção. O cliente de pré-produção é uma versão mais recente para testes no ambiente de produção. Selecione **Browse,** em seguida, escolha o pacote de instalação de cliente pré-produção para usar com este passo.  

#### <a name="installation-properties"></a>Propriedades da Instalação

O passo da sequência de tarefas especifica automaticamente a atribuição do site e a configuração predefinida. Utilize este campo para especificar quaisquer propriedades de instalação adicionais para utilizar quando instalar o cliente. Para introduzir várias propriedades de instalação, separe-as com um espaço.  

Especifique as opções da linha de comando para utilizar durante a instalação do cliente. Por exemplo, `/skipprereq: silverlight.exe` insira informar CCMSetup.exe para não instalar o pré-requisito microsoft Silverlight. Para obter mais informações sobre as opções disponíveis da linha de comando para CCMSetup.exe, consulte as propriedades de [instalação do cliente](../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="options-for-setup-windows-and-configmgr"></a>Opções para Configurar Windows e ConfigMgr

> [!NOTE]  
> Não ative **Continuar a trabalhar no** separador **Opções.** Se houver um erro durante este passo, a sequência de tarefas falha se ativa ou não esta definição.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a>Sistema Operativo de Upgrade

Utilize este passo para atualizar uma versão mais antiga do Windows para uma versão mais recente do Windows 10.  

Este passo de sequência de tarefa saem apenas em todo o Sistema Operativo. Não funciona no Windows PE.  

Para adicionar este passo no editor de sequência de tarefas, selecione **Adicionar**, selecione **Imagens**e selecione **Sistema Operativo de Upgrade**.

> [!TIP]
> A começar pelo Windows 10, versão 1709, os meios de comunicação incluem várias edições. Quando configurar uma sequência de tarefas para utilizar um pacote de atualização de OS ou imagem de OS, certifique-se de selecionar uma [edição suportada](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Utilize o pré-cache de conteúdo para descarregar um pacote de atualização de OS aplicável antes de um utilizador instalar a sequência de tarefas. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>Variáveis para upgrade de Os

Utilize as seguintes variáveis de sequência de tarefas com este passo:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [ConfiguraçãoCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Cmdlets para upgrade os o

Gerencie este passo com os seguintes cmdlets PowerShell:<!-- SCCMDocs #1118 -->

- [Sistema operacional get-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Novo CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Remover cmtsstepupgradeSistema de funcionamento](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Sistema operativo set-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps)

### <a name="properties-for-upgrade-os"></a>Propriedades para Upgrade OS

No separador **Propriedades** para este passo, configure as definições descritas nesta secção.  

#### <a name="upgrade-package"></a>Pacote de atualização

Selecione esta opção para especificar o pacote de atualização do Sistema operativo Windows 10 para utilizar para a atualização.  

#### <a name="source-path"></a>Caminho de origem

Especifica um caminho local ou de rede para os meios de comunicação Windows 10 que o Windows Setup utiliza. Esta definição corresponde à opção `/InstallFrom`de linha de comando de configuração do Windows .

Também pode especificar uma variável, como `%MyContentPath%` ou `%DPC01%`. Quando utilizar uma variável para o caminho de origem, desloque o seu valor mais cedo na sequência de tarefas. Por exemplo, utilize o passo de [Conteúdo do Pacote de Descarregamento](#BKMK_DownloadPackageContent) para especificar uma variável para a localização do pacote de atualização do OS. Em seguida, use essa variável para o caminho de origem para este passo.  

#### <a name="edition"></a>Edição

Especifique a edição dentro dos meios de comunicação osso para utilizar para a atualização.  

#### <a name="product-key"></a>Chave de produto

Especifique a chave do produto para aplicar ao processo de atualização.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Fornecer o seguinte conteúdo de controlador à Configuração do Windows durante a atualização

Adicione os controladores ao computador de destino durante o processo de atualização. Os controladores têm de ser compatíveis com o Windows 10. Esta definição corresponde à opção `/InstallDriver`de linha de comando de configuração do Windows . Para mais informações, consulte [as opções da linha de comando sinuosa](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers)do Windows Configuração .

Especifique uma das seguintes opções:  

- **Pacote de controlador**: Selecione **Navegar** e escolha um pacote de controlador existente na lista.

- **Conteúdo encenado**: Selecione esta opção para especificar a localização para o conteúdo do condutor. Pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando utilizar uma variável para o caminho de origem, desloque o seu valor mais cedo na sequência de tarefas. Por exemplo, utilizando o passo de conteúdo do [pacote de descarregamento.](task-sequence-steps.md#BKMK_DownloadPackageContent)  

> [!TIP]
> Se quiser ter conteúdo dinâmico para vários tipos de hardware:
>
> - Utilize várias instâncias deste passo com condições para os tipos de hardware e conteúdo separado do condutor.
>
> - Utilize várias instâncias da etapa de Conteúdo do [Pacote de Descarregamento.](task-sequence-steps.md#BKMK_DownloadPackageContent) Coloque o conteúdo num local comum e, em seguida, utilize a opção de **conteúdo encenado.** O benefício deste método é que a sequência de tarefas tem um único passo **de Upgrade OS.**

#### <a name="time-out-minutes"></a>Tempo limite (minutos)

Especifique o número de minutos antes de o Gestor de Configuração falhar este passo. Esta opção é útil se o Windows Setup parar de processar, mas não termina.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Efetuar análise de compatibilidade da Configuração do Windows sem iniciar a atualização

Execute a análise de compatibilidade do Windows Configuração sem iniciar o processo de atualização. Esta definição corresponde à opção `/Compat ScanOnly`de linha de comando de configuração do Windows . Implemente todo o pacote de upgrade do OS com esta opção.

<!--SCCMDocs-pr issue 2812-->
Quando ativa esta opção, este passo não coloca o cliente do Gestor de Configuração no modo de provisionamento. A Configuração do Windows funciona silenciosamente em segundo plano e o cliente continua a funcionar normalmente. Para mais informações, consulte [o modo de provisionamento](provisioning-mode.md).

A Configuração devolve um código de saída como resultado da análise. A tabela que se segue fornece alguns dos códigos de saída mais comuns:  

|Código de saída|Detalhes|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Não existem problemas de compatibilidade ("êxito").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Questões de compatibilidade atolo.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0XC1900204)|A escolha de migração selecionada não está disponível. Por exemplo, uma atualização do Empresarial para o Profissional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não é elegível para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Não existe espaço livre suficiente no disco.|  

Para mais informações sobre este parâmetro, consulte [as opções de linha de comando do Windows Configuração](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorar mensagens de compatibilidade dispensáveis

Especifica que a Configuração completa a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis. Esta definição corresponde à opção `/Compat IgnoreWarning`de linha de comando de configuração do Windows .  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Atualizar dinamicamente a Configuração do Windows com o Windows Update

Ativar a configuração para executar operações de Atualização Dinâmica, tais como pesquisa, download e instalação de atualizações. Esta definição corresponde à opção `/DynamicUpdate`de linha de comando de configuração do Windows . Esta definição não é compatível com atualizações de software do Gestor de Configuração. Ative esta opção quando gere atualizações com serviços de atualização de servidores do Windows (WSUS) ou Windows Update para O Negócio.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Sobrepor a política e utilizar o Microsoft Update padrão

Anule temporariamente a política local em tempo real para executar operações de Atualização Dinâmica. O computador recebe atualizações a partir do Windows Update.
