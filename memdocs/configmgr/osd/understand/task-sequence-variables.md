---
title: Referência de variáveis de sequência de tarefas
titleSuffix: Configuration Manager
description: Aprenda sobre as variáveis para controlar e personalizar uma sequência de tarefas do Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e2c8b369b69bd5fcddd2f52b875b5089d82ebb0e
ms.sourcegitcommit: d05b1472385c775ebc0b226e8b465dbeb5bf1f40
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605139"
---
# <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo é uma referência para todas as variáveis disponíveis por ordem alfabética. Utilize a função localizar o navegador **(tipicamente** **CTRL** + **F)** para encontrar uma variável específica. A variável notas se é específica para um passo particular. O artigo sobre [os passos](task-sequence-steps.md) da sequência de tarefas inclui a lista de variáveis específicas a cada passo.

Para obter mais informações, consulte [A utilização de variáveis](using-task-sequence-variables.md)de sequência de tarefas .

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a>Referência variável de sequência de tarefas

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a>_OSDDetectedWinDir

A sequência de tarefas digitaliza os discos rígidos do computador para uma instalação anterior do sistema operativo quando o Windows PE começa. A localização da pasta do Windows é armazenada nesta variável. Pode configurar a sequência de tarefas para obter este valor a partir do ambiente e utilizá-la para especificar a localização da pasta Windows utilizada para a nova instalação do sistema operativo.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a>_OSDDetectedWinDrive

A sequência de tarefas digitaliza os discos rígidos do computador para uma instalação anterior do sistema operativo quando o Windows PE começa. A localização do disco rígido onde o sistema operativo é instalado é armazenada nesta variável. Pode configurar a sequência de tarefas para obter este valor a partir do ambiente e utilizá-la para especificar a localização do disco rígido utilizada para o novo sistema operativo.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a>_OSDMigrateUsmtPackageID

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Especifica o ID do pacote de Gestor de Configuração que contém os ficheiros USMT. Esta variável é necessária.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a>_OSDMigrateUsmtRestorePackageID

*Aplica-se ao passo [do Estado do Utilizador de Restauração.](task-sequence-steps.md#BKMK_RestoreUserState)*

(entrada)

Especifica o ID do pacote de Gestor de Configuração que contém os ficheiros USMT. Esta variável é necessária.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a>_SMSTSAdvertID

Armazena o ID exclusivo de implementação da sequência de tarefas atualmente em execução. Utiliza o mesmo formato que um ID de distribuição de software do Gestor de Configuração. Se a sequência de tarefas for executada a partir de um suporte de dados autónomo, esta variável é indefinida.

#### <a name="example"></a>Exemplo

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a>_SMSTSAssetTag

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica a etiqueta de ativo para o computador.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a>_SMSTSBootImageID

Se a sequência de tarefas de execução atual for referenciada por um pacote de imagem de arranque, esta variável armazena o pacote de imagem de arranque ID. Se a sequência de tarefas não referenciar um pacote de imagem de arranque, esta variável não está definida.

#### <a name="example"></a>Exemplo

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a>_SMSTSBootUEFI

A sequência de tarefas define esta variável quando deteta um computador que está no modo UEFI.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a>_SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
A sequência de tarefas define esta variável quando caches conteúdo na unidade local. A variável contém o caminho para a cache. Se esta variável não existe, então não há cache.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a>_SMSTSClientGUID

Armazena o valor do cliente GUID do Gestor de Configuração. Se a sequência de tarefas estiver a funcionar a partir de meios autónomos, esta variável não está definida.

#### <a name="example"></a>Exemplo

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a>_SMSTSCurrentActionName

Especifica o nome do passo da sequência de tarefas em execução atual. Esta variável é definida antes de o gestor da sequência de tarefas executar cada passo individual.

#### <a name="example"></a>Exemplo

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a>_SMSTSDefaultGateways

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica os gateways predefinidos utilizados pelo computador.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a>_SMSTSDownloadOnDemand

Se a sequência de tarefas atual estiver a funcionar `true`no modo de descarregamento a pedido, esta variável é . Modo de descarregamento a pedido significa que o gestor da sequência de tarefas descarrega conteúdo localmente apenas quando tem de aceder ao conteúdo.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a>_SMSTSInWinPE

Quando o passo atual da sequência de tarefas está a decorrer no Windows PE, esta variável é `true`. Teste esta variável de sequência de tarefas para determinar o ambiente atual do Os.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a>_SMSTSIPAddresses

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica os endereços IP utilizados pelo computador.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a>_SMSTSLastActionName

Armazena o nome da última ação que foi executada. Esta variável diz respeito a **_SMSTSLastActionRetCode.** A sequência de tarefas regista estes valores no ficheiro smsts.log. Esta variável é benéfica quando se resoluuma sequência de tarefas. Quando um passo falha, um script personalizado pode incluir o nome do passo juntamente com o código de retorno.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a>_SMSTSLastActionRetCode

Armazena o código de devolução da última ação que foi executada. Esta variável pode ser utilizada como uma condição para determinar se o próximo passo é executado.

#### <a name="example"></a>Exemplo

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a>_SMSTSLastActionSucceeded

- Se o último passo for `true`bem sucedido, esta variável é .  

- Se o último passo falhou, é. `false`  

- Se a sequência de tarefas saltou a última ação, porque o passo está desativado ou a condição associada avaliada a **falsas,** esta variável não é redefinida. Ainda detém o valor da ação anterior.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a>_SMSTSLastContentDownloadLocation

<!-- 2840337 -->
A partir da versão 1906, esta variável contém o último local onde a sequência de tarefas descarregou ou tentou descarregar conteúdo. Inspecione esta variável em vez de analisar os registos do cliente para obter esta localização de conteúdo.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a>_SMSTSLaunchMode

Especifica que a sequência de tarefas começou através de um dos seguintes métodos:  

- **SMS**: O cliente do Gestor de Configuração, como quando um utilizador o inicia no Centro de Software
- **UFD**: Suportes USB legados
- **UFD+FORMAT**: Mais recentes suportes USB
- **CD**: Um CD sapateado
- **DVD**: Um DVD sapateado
- **PXE**: Bota de rede com PXE
- **HD**: Meios pré-encenados num disco rígido

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a>_SMSTSLogPath

Armazena o caminho completo do diretório de registo. Utilize este valor para determinar onde os passos da sequência de tarefas registam as suas ações. Este valor não é definido quando um disco rígido não está disponível.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a>_SMSTSMacAddresses

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica os endereços MAC utilizados pelo computador.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a>_SMSTSMachineName

Armazena e especifica o nome do computador. Armazena o nome do computador que a sequência de tarefas utiliza para registar todas as mensagens de estado. Para alterar o nome do computador no novo SISTEMA, utilize a variável [OSDComputerName.](#OSDComputerName-input)

### <a name="_smstsmake"></a><a name="SMSTSMake"></a>_SMSTSMake

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica a marca do computador.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a>_SMSTSMDataPath

Especifica o caminho definido pela variável [SMSTSLocalDataDrive.](#SMSTSLocalDataDrive) Quando define sMSTSLocalDataDrive antes do início da sequência de tarefas, como por exemplo, definindo uma variável de recolha, o Gestor de Configuração define a variável _SMSTSMDataPath assim que a sequência de tarefas começar.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a>_SMSTSMediaType

Especifica o tipo de mídia que é usado para iniciar a instalação. Exemplos de tipos de suportes de dados: Suporte de Dados de Arranque, Suporte de Dados Completo, PXE e Suporte de Dados Pré-configurado.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a>_SMSTSModel

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica o modelo do computador.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a>_SMSTSMP

Armazena o endereço URL ou IP de um ponto de gestão do Gestor de Configuração.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a>_SMSTSMPPort

Armazena o número de porta de um ponto de gestão do Gestor de Configuração.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a>_SMSTSOrgName

Armazena o nome do título de marca que a sequência de tarefas exibe no diálogo de progresso.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a>_SMSTSOSUpgradeActionReturnCode

*Aplica-se ao passo do [sistema operativo upgrade.](task-sequence-steps.md#BKMK_UpgradeOS)*

Armazena o valor do código de saída que o Windows Setup retorna para indicar sucesso ou falha. Esta variável é `/Compat` útil com a opção linha de comando.

#### <a name="example"></a>Exemplo

Após a conclusão de uma verificação apenas com compatibilidade, tome medidas em etapas posteriores, dependendo do código de saída de falha ou sucesso. Sobre o sucesso, inicie a atualização. Ou definir um marcador no ambiente para recolher com inventário de hardware. Por exemplo, adicione um ficheiro ou defino uma chave de registo. Utilize este marcador para criar uma coleção de computadores que estejam prontos para atualizar, ou que necessitem de ação antes da atualização.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a>_SMSTSPackageID

Armazena o ID da sequência de tarefas atualmente em execução. Este ID utiliza o mesmo formato que um ID de pacote de Gestor de Configuração.

#### <a name="example"></a>Exemplo

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a>_SMSTSPackageName

Armazena o nome atual da sequência de tarefas. Um administrador do Gestor de Configuração especifica este nome ao criar a sequência de tarefas.

#### <a name="example"></a>Exemplo

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a>_SMSTSRunFromDP

Ajuste `true` para se a sequência de tarefa sintetizada estiver em execução no modo de ponto de distribuição. Este modo significa que o gestor da sequência de tarefas obtém as quotas de pacote necessárias a partir do ponto de distribuição.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a>_SMSTSSerialNumber

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica o número de série do computador.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a>_SMSTSSetupRollback

Especifica se a Configuração do Windows realizou uma operação de reversão durante uma atualização no local. Os valores `true` variáveis podem ser ou `false`.

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a>_SMSTSSiteCode

Armazena o código de site do site do Gestor de Configuração.

#### <a name="example"></a>Exemplo

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a>_SMSTSTimezone

Esta variável armazena a informação do fuso horário no seguinte formato:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Exemplo

Para o fuso horário **Horário Oriental (EUA e Canadá)**:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a>_SMSTSType

Especifica o tipo da sequência de tarefas atualmente em execução. Pode ter um dos seguintes valores:  

- **1**: Sequência de tarefas genérica
- **2**: Sequência de tarefas de implantação do OS

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a>_SMSTSUseCRL

Quando a sequência de tarefas utiliza HTTPS para comunicar com o ponto de gestão, esta variável especifica se utiliza a lista de revogação do certificado (CRL).

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a>_SMSTSUserStarted

Especifica se um utilizador iniciou a sequência de tarefas. Esta variável só é definida se a sequência de tarefas for iniciada a partir do Centro de Software. Por exemplo, [_SMSTSLaunchMode](#SMSTSLaunchMode) se _SMSTSLaunchMode `SMS`for definido para .

Esta variável pode ter os seguintes valores:  

- `true`: Especifica que a sequência de tarefas é iniciada manualmente por um utilizador do Centro de Software.  

- `false`: Especifica que a sequência de tarefas é iniciada automaticamente pelo programador do Gestor de Configuração.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a>_SMSTSUseSSL

Especifica se a sequência de tarefas utiliza o SSL para comunicar com o ponto de gestão do Gestor de Configuração. Se configurar os sistemas do seu site `true`para HTTPS, o valor está definido para .

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a>_SMSTSUUID

*Aplica-se ao passo [de Variáveis Dinâmicas definidas.](task-sequence-steps.md#BKMK_SetDynamicVariables)*

Especifica o UUID do computador.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a>_SMSTSWTG

Especifica se o computador está a ser executado como um dispositivo Windows To Go.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a>_TS_CRMEMORY

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se a`1` **verificação da memória mínima (MB)** devolvida verdadeira ( ) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a>_TS_CRSPEED

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se o controlo`1`mínimo de`0`velocidade do **processador (MHz)** devolvido verdadeiro ( ) ou falso ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a>_TS_CRDISK

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se o espaço`1`mínimo de`0`disco **livre (MB)** verificar devolvido verdadeiro ( ) ou falso ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a>_TS_CROSTYPE

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se o **Sistema operativo atual a ser atualizado é** verificado de forma verdadeira (`1`) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a>_TS_CRARCH

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se a **Arquitetura da verificação atual do OS** retornou verdadeira (`1`) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a>_TS_CRMINOSVER

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se`1`a versão`0`mínima **de SISTEMA** devolvido verdadeiro ( ) ou falso ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a>_TS_CRMAXOSVER

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se`1`a versão`0`máxima **de OS** despertá-la é verdadeira ( ) ou falsa ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a>_TS_CRCLIENTMINVER

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se`1`a versão`0`do **cliente mínimo** deverificação devolvida verdadeira ( ) ou falsa ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a>_TS_CROSLANGUAGE

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se a **linguagem da verificação atual do OS** retornou verdadeira (`1`) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a>_TS_CRACPOWER

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para saber se`1`a potência`0`ca **ligada à** verificação retornou verdadeiramente ( ) ou falsa ( ). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a>_TS_CRNETWORK

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se o **adaptador** de rede de verificação retornada verdadeira (`1`) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a>_TS_CRWIRED

*Começando na versão 2002* <!--6005561-->  
*Aplica-se ao passo de prontidão de [verificação.](task-sequence-steps.md#BKMK_CheckReadiness)*

Uma variável de leitura apenas para se o **adaptador de rede não é** verificação sem fios devolvida verdadeiramente (`1`) ou falsa (`0`). Se não ativar a verificação, o valor desta variável apenas para leitura é em branco.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a>_TSAppInstallStatus

A sequência de tarefas define esta variável com o estado de instalação da aplicação durante a etapa de instalação da [aplicação.](task-sequence-steps.md#BKMK_InstallApplication) Define um dos seguintes valores:  

- **Indefinido**: O passo da aplicação de instalação não foi executado.  

- **Erro**: Pelo menos uma aplicação falhou devido a um erro durante a fase de instalação da aplicação.  

- **Aviso**: Não ocorreram erros durante a etapa de instalação. Uma ou mais aplicações, ou uma dependência necessária, não foram instaladas porque um requisito não foi cumprido.  

- **Sucesso**: Não são detetados erros ou advertências durante a etapa de Instalação.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a>_TSSecureBoot

*Começando na versão 2002* <!--5842295-->  

Utilize esta variável para determinar o estado da bota segura num dispositivo ativado pela UEFI. A variável pode ter um dos seguintes valores:

- `NA`: O valor do registo associado não existe, o que significa que o dispositivo não suporta a bota segura.
- `Enabled`: O aparelho tem uma bota segura ativada.
- `Disabled`: O aparelho tem uma bota segura desativada.

### <a name="osdadapter"></a><a name="OSDAdapter"></a>OsDAdapter

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Esta variável de sequência de tarefas é uma variável de *matriz.* Cada elemento da matriz representa as definições para um adaptador de rede individual no computador. Aceda às definições de cada adaptador combinando o nome variável da matriz com o índice de adaptador de rede baseado em zero e o nome de propriedade.

Se o passo de Definições de Rede Aplicar configura vários adaptadores de rede, define as propriedades para o *segundo* adaptador de rede utilizando o índice **1** no nome variável. Por exemplo: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList e OSDAdapter1DNSDomain.

Utilize os seguintes nomes variáveis para definir as propriedades do *primeiro* adaptador de rede para o passo de configurar:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Esta definição é obrigatória. Os valores possíveis são `True` ou `False`. Por exemplo:

`true`: ativar o Protocolo de Configuração dinâmica do hospedeiro (DHCP) para o adaptador

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Lista de endereços IP deslimitados com vírpara o adaptador. Esta propriedade é ignorada a menos que `false` **o EnableDHCP** esteja definido para . Esta definição é obrigatória.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Lista de máscaras de sub-rede delimitadas. Esta propriedade é ignorada a menos que `false` **o EnableDHCP** esteja definido para . Esta definição é obrigatória.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Lista de endereços ip deslimitada sintetmente. Esta propriedade é ignorada a menos que `false` **o EnableDHCP** esteja definido para . Esta definição é obrigatória.

#### <a name="osdadapter0dnsdomain"></a>DOMÍNIO OSDAdapter0DNSDomain

Domínio do Sistema de Nome de Domínio (DNS) para o adaptador.

#### <a name="osdadapter0dnsserverlist"></a>Lista osdAdapter0DNSServerList

Lista de servidores DNS delimitada selada para o adaptador. Esta definição é obrigatória.

#### <a name="osdadapter0enablednsregistration"></a>REGISTO OSDAdapter0EnableDNS

Prepara-se para `true` registar o endereço IP do adaptador em DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

`true` Decidiu registar o endereço IP do adaptador em DNS com o nome DNS completo para o computador.

#### <a name="osdadapter0enableipprotocolfiltering"></a>FILTRAgem de protocolos ENABLEIP EnableIP

Decidiu `true` ativar a filtragem do protocolo IP no adaptador.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Lista de protocolos delimitados com a comma autorizados a passar por cima do IP. Esta propriedade é ignorada se o **EnableIPProtocolFiltering** estiver definido para `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>FILTRAgem OSDAdapter0EnableTCP

Delineado para `true` ativar a filtragem da porta TCP para o adaptador.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterFilterPortList

Lista de portas delimitada saqueadas a serem concedidas permissões de acesso para a TCP. Esta propriedade é ignorada se o **EnableTCPFiltering** estiver definido para `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Opções para NetBIOS em TCP/IP. Os valores possíveis são:  

- `0`: Utilizar as definições NetBIOS do servidor DHCP  
- `1`: Ativar o NetBIOS sobre TCP/IP  
- `2`: Desativar o NetBIOS sobre TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Prepara-te para `true` utilizar o WINS para resolução de nomes.

#### <a name="osdadapter0winsserverlist"></a>LISTA OSDAdapter0WINSServerList

Lista delimitada de comma dos endereços IP do servidor WINS. Esta propriedade é ignorada a menos `true`que **enableWINS** esteja definido para .

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

O endereço MAC utilizado para combinar as definições com o adaptador de rede física.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

O nome da ligação de rede tal como aparece no programa do painel de controlo de ligações de rede. O nome tem entre 0 e 255 caracteres de comprimento.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Índice das definições do adaptador de rede na gama de definições.

#### <a name="example"></a>Exemplo

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a>OSDAdapterCount

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica o número de adaptadores de rede instalados no computador de destino. Quando definir o valor **OSDAdapterCount,** também detetete todas as opções de configuração para cada adaptador.

Por exemplo, se definir o valor **OSDAdapter0TCPIPNetbiosOptions** para o primeiro adaptador, então deve configurar todos os valores para esse adaptador.

Se não especificar este valor, a sequência de tarefas ignora todos os valores **OSDAdapter.**

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a>OSDApplyDriverBootCriticalContentUniqueID

*Aplica-se ao passo do pacote do [condutor aplicável.](task-sequence-steps.md#BKMK_ApplyDriverPackage)*

(entrada)

Especifica o ID de conteúdo do controlador de dispositivo de armazenamento em massa a instalar a partir do pacote de controlador. Se esta variável não for especificada, não é instalado nenhum controlador de armazenamento em massa.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a>OSDApplyDriverBootCriticalHardwareComponent

*Aplica-se ao passo do pacote do [condutor aplicável.](task-sequence-steps.md#BKMK_ApplyDriverPackage)*

(entrada)

Especifica se um controlador de dispositivo de armazenamento em massa está instalado, esta variável deve ser **scsi**.

Se o [OSDApplyDriverBootCriticalCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) for definido, esta variável é necessária.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a>OSDApplyDriverBootCriticalID

*Aplica-se ao passo do pacote do [condutor aplicável.](task-sequence-steps.md#BKMK_ApplyDriverPackage)*

(entrada)

Especifica o ID crítico de arranque do controlador de dispositivo de armazenamento em massa a instalar. Este ID está listado na secção **scsi** do ficheiro txtsetup.oem do controlador do dispositivo.

Se o [OSDApplyDriverBootCriticalCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) for definido, esta variável é necessária.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a>OSDApplyDriverBootCriticalINFFile

*Aplica-se ao passo do pacote do [condutor aplicável.](task-sequence-steps.md#BKMK_ApplyDriverPackage)*

(entrada)

Especifica o ficheiro INF do controlador de armazenamento em massa a instalar.

Se o [OSDApplyDriverBootCriticalCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) for definido, esta variável é necessária.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a>OSDAutoApplyDriverBestMatch

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

(entrada)

Se houver vários controladores de dispositivos no catálogo do condutor compatíveis com um dispositivo de hardware, esta variável determina a ação do passo.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido): Só instale o melhor controlador de dispositivos  

- `false`: Instala todos os controladores de dispositivos compatíveis e o Windows escolhe o melhor controlador a utilizar  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a>Lista de Condutores Autoaplicados OSDAuto

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

(entrada)

Uma lista delimitada por vírgulas dos IDs exclusivos das categorias do catálogo de controladores. O passo do condutor de **aplicação automática** apenas considera os condutores em pelo menos uma das categorias especificadas. Este valor é opcional, e não é definido por padrão. Obtenha as identificações da categoria disponível enumerando a lista de objetos **SMS_CategoryInstance** no site.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a>Contagem de rebootde osdbitlocker

*Aplica-se ao passo [Desativar o BitLocker.](task-sequence-steps.md#BKMK_DisableBitLocker)*

<!-- 4512937 -->
A partir da versão 1906, utilize esta variável para definir o número de reinícios após o qual retoma a proteção.

#### <a name="valid-values"></a>Valores válidos

Um inteiro `1` de. `15`

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a>OSDBitLockerRebootCountOverride

*Aplica-se ao passo [Desativar o BitLocker.](task-sequence-steps.md#BKMK_DisableBitLocker)*

<!-- 4512937 -->
A partir da versão 1906, deset este valor para sobrepor a contagem definida pelo passo ou pela variável [OSDBitLockerRebootCount.](#OSDBitLockerRebootCount) Enquanto os outros métodos só aceitam valores 1 a 15, se definir esta variável para 0, o BitLocker permanece inativado indefinidamente. Esta variável é útil quando a sequência de tarefas define um valor, mas pretende definir um valor separado numa base por dispositivo ou por coleção.

#### <a name="valid-values"></a>Valores válidos

Um inteiro `0` de. `15`

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a>Palavra-passe para recuperação de osdbitlocker

*Aplica-se ao passo [Enable BitLocker.](task-sequence-steps.md#BKMK_EnableBitLocker)*

(entrada)

Em vez de gerar uma senha de recuperação aleatória, o passo **Enable BitLocker** utiliza o valor especificado como senha de recuperação. O valor tem de ser uma palavra-passe de recuperação do BitLocker numérica válida.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a>OsdbitLockerStartupKey

*Aplica-se ao passo [Enable BitLocker.](task-sequence-steps.md#BKMK_EnableBitLocker)*

(entrada)

Em vez de gerar uma chave de arranque aleatória para a opção de gestão chave **Chave startup apenas USB,** o passo **Enable BitLocker** utiliza o Módulo plataforma fidedigno (TPM) como chave de arranque. O valor tem de ser uma chave de arranque do BitLocker codificada em Base64 de 256 bits válida.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a>Conta OSDCapture

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Especifica um nome de conta Windows que tem permissões para armazenar a imagem capturada numa partilha de rede[(OSDCaptureDestination).](#OSDCaptureDestination) Especifique também a [Palavra-passe da Conta de Captura osS](#OSDCaptureAccountPassword).

Para obter mais informações sobre a conta de imagem de captura do OS, consulte [Contas](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a>OsdCaptureAccountPassword

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Especifica a palavra-passe para a conta Windows[(OSDCaptureAccount)](#OSDCaptureAccount)utilizada para armazenar a imagem capturada numa partilha de rede[(OSDCaptureDestination).](#OSDCaptureDestination)

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a>DESTINO OSDCapture

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Especifica a localização onde a sequência de tarefas salva a imagem de Os capturada. O comprimento máximo do nome do diretório é 255 carateres. Se a parte da rede necessitar de autenticação, especifique as variáveis [OSDCaptureAccount](#OSDCaptureAccount) e [OSDCaptureAccountPassword.](#OSDCaptureAccountPassword)

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a>NOME OSDComputer (entrada)

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica o nome do computador de destino.

#### <a name="example"></a>Exemplo

`%_SMSTSMachineName%`(predefinido)

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a>NOME OSDComputer (saída)

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

Definida como o nome NetBIOS do computador. O valor só é definido se a variável `true` [OSDMigrateComputerName](#OSDMigrateComputerName) estiver definida para .

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a>Nome de ficheiro OSDConfig

*Aplica-se ao passo [de imagem de aplicar o OS.](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)*

(entrada)

Especifica o nome de ficheiro do ficheiro de resposta de implementação do SISTEMA associado ao pacote de imagem de implementação do SISTEMA.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a>Índice de Imagem de Dados OSDData

*Aplica-se ao passo de Imagem de [Dados aplicado.](task-sequence-steps.md#BKMK_ApplyDataImage)*

(entrada)

Especifica o valor de índice da imagem que é aplicada ao computador de destino.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a>Índice OSDDisk

*Aplica-se ao passo do [formato e do disco de partição.](task-sequence-steps.md#BKMK_FormatandPartitionDisk)*

(entrada)

Especifica o número do disco físico a particionar.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a>Domínio OSDDNS

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica o servidor DNS primário que o computador de destino utiliza.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a>OSDDNSSufixSearchOrder

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica a ordem de procura DNS para o computador de destino.

### <a name="osddomainname"></a><a name="OSDDomainName"></a>Nome OSDDomain

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica o nome do domínio do Diretório Ativo a que o computador de destino se junta. O valor especificado tem de ser um nome de domínio de Serviços de Domínio do Active Directory válido.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a>NOME OSDDomainOUName

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo.

#### <a name="example"></a>Exemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a>Comando osddonotlog

<!--1358493-->
*Aplica-se ao passo do [Pacote de Instalação.](task-sequence-steps.md#BKMK_InstallPackage)*

*Começando na versão 1902*  
*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

(entrada)

Para evitar que os dados potencialmente sensíveis sejam `TRUE`exibidos ou registados, detete te a variável para . Esta variável disfarça o nome do programa no **smsts.log** durante um passo **de Pacote de Instalação.**

A partir da versão 1902, quando `TRUE`se define esta variável para, também esconde a linha de comando do passo da Linha de **Comando run** no ficheiro de registo.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a>Filtragem osdEnableTCPIPPIP

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica se a filtragem TCP/IP está ativada.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a>OsDGPTBootdisk

*Aplica-se ao passo do [formato e do disco de partição.](task-sequence-steps.md#BKMK_FormatandPartitionDisk)*

(entrada)

Especifica se criará uma partição EFI num disco rígido GPT. Os computadores baseados na EFI usam esta partição como disco de arranque.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a>Criador de Imagem

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Um nome opcional do utilizador que criou a imagem. Este nome é armazenado no ficheiro WIM. O comprimento máximo do nome de utilizador é 255 carateres.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a>Descrição da imagem do OSDImage

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Uma descrição opcional definida pelo utilizador da imagem de Os capturada. Esta descrição é armazenada no ficheiro WIM. O comprimento máximo da descrição é 255 carateres.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a>Índice DE Imagem OSDImage

*Aplica-se ao passo [de imagem de aplicar o OS.](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)*

(entrada)

Especifica o valor do índice de imagem do ficheiro WIM que é aplicado ao computador de destino.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a>Versão OSDImage

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

(entrada)

Um número opcional de versão definida pelo utilizador para atribuir à imagem de OS capturada. Este número de versão é armazenado no ficheiro WIM. Este valor pode ser qualquer combinação de caracteres alfanuméricos com um comprimento máximo de 32.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a>OsdInstallDriversAdicionações

<!--516679/2840016-->
*Aplica-se ao passo do pacote do [condutor aplicável.](task-sequence-steps.md#BKMK_ApplyDriverPackage)*

(entrada)

Especifica opções adicionais para adicionar à linha de comando DISM ao aplicar um pacote de controlador. A sequência de tarefas não verifica as opções da linha de comando.

Para utilizar esta variável, ative a definição, instale o **pacote do controlador através da execução dISM com opção de recurse,** na etapa do Pacote do Condutor **Aplicável.**

Para mais informações, consulte as opções de [linha de comando DoDM do Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a>Conta OSDJoin

*Aplica-se aos seguintes passos:*  

- [Aplicar Definições de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Associar Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica a conta de utilizador de domínio que é usada para adicionar o computador de destino ao domínio. Esta variável é necessária ao associar um domínio.

Para obter mais informações sobre a conta de junção do domínio da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)consulte Contas .

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a>Nome osdjoindomain

*Aplica-se ao passo [do Domínio de Adesão ou do Grupo de Trabalho.](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)*

(entrada)

Especifica o nome de um domínio de Diretório Ativo que o computador de destino se junta. O comprimento do nome de domínio deve estar entre 1 e 255 caracteres.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a>OSDJoinDomainOUName

*Aplica-se ao passo [do Domínio de Adesão ou do Grupo de Trabalho.](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)*

(entrada)

Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo. O comprimento do nome Ou deve ser entre 0 e 32.767 caracteres. Este valor não é definido se a variável `1` [OSDJoinType](#OSDJoinType) estiver definida para (junte-se ao grupo de trabalho).

#### <a name="example"></a>Exemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a>OsdJoinPassword

*Aplica-se aos seguintes passos:*  

- [Aplicar Definições de Rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Associar Domínio ou Grupo de Trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica a palavra-passe para o [OSDJoinAccount](#OSDJoinAccount) que o computador de destino utiliza para aderir ao domínio de Diretório Ativo. Se o ambiente da sequência de tarefas não incluir esta variável, então o Windows Configuração tenta uma palavra-passe em branco. Se a variável variável [VARIÁVEL OSDJoinType](#OSDJoinType) estiver definida para `0` (unir domínio), este valor é necessário.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a>OsdJoinSkipReboot

*Aplica-se ao passo [do Domínio de Adesão ou do Grupo de Trabalho.](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)*

(entrada)

Especifica se pretende ignorar o reinício após o computador de destino ser associado ao domínio ou grupo de trabalho.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a>OSDJoinType

*Aplica-se ao passo [do Domínio de Adesão ou do Grupo de Trabalho.](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)*

(entrada)

Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho.

#### <a name="valid-values"></a>Valores válidos

- `0`: Junte-se ao computador de destino para um domínio Windows  
- `1`: Junte-se ao computador de destino a um grupo de trabalho  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a>Nome do grupo OSDJoinWork

*Aplica-se ao passo [do Domínio de Adesão ou do Grupo de Trabalho.](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)*

(entrada)

Especifica o nome de um grupo de trabalho ao qual o computador de destino é associado. O comprimento do nome do grupo de trabalho tem de ser entre 1 e 32 carateres.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a>Ativação osdkeep

*Aplica-se ao preparar o Windows para o passo [de captura.](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)*

(entrada)

Especifica se a sysprep mantém ou repõe a bandeira de ativação do produto.

#### <a name="valid-values"></a>Valores válidos

- `true`: manter a bandeira de ativação
- `false`(predefinido): redefinir a bandeira de ativação

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a>OsdLocalAdminPassword

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica a senha da conta do Administrador local. Se permitir a opção de **gerar aleatoriamente a palavra-passe do administrador local e desativar a conta em todas as plataformas suportadas,** então o passo ignora esta variável. O valor especificado tem de ter entre 1 e 255 carateres.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a>OSDLogPowerShellParameters

<!--3556028-->
*Começando na versão 1902*  
*Aplica-se ao passo [do Script PowerShell de execução.](task-sequence-steps.md#BKMK_RunPowerShellScript)*

(entrada)

Para evitar que os dados potencialmente sensíveis sejam registados, o passo **do Script Run PowerShell** não regista parâmetros de script no ficheiro **smsts.log.** Para incluir os parâmetros do script no registo da sequência de tarefas, defina esta variável para **TRUE**.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a>OSDMigrateAdapterSettings

*Aplica-se ao passo de Definições da [Rede de Captura.](task-sequence-steps.md#BKMK_CaptureNetworkSettings)*

(entrada)

Especifica se a sequência de tarefas captura a informação do adaptador de rede. Esta informação inclui configurações de configuração para TCP/IP, DNS e WINS.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido)
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a>OSDMigrateOps de Captura Adicional

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Especifique opções adicionais de linha de comando para a ferramenta de migração do estado do utilizador (USMT) que a sequência de tarefas utiliza para capturar o estado do utilizador. O passo não expõe estas definições no editor da sequência de tarefas. Especifique estas opções como uma cadeia, que a sequência de tarefas anexa à linha de comando USMT gerada automaticamente para o ScanState.

As opções USMT especificadas com esta variável de sequência de tarefas não são validadas para precisão antes de executar a sequência de tarefas.

Para obter mais informações sobre as opções disponíveis, consulte [ScanState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a>OSDMigrateAdicionaRestaurarOpções

*Aplica-se ao passo [do Estado do Utilizador de Restauração.](task-sequence-steps.md#BKMK_RestoreUserState)*

(entrada)

Especifica opções adicionais de linha de comando para a ferramenta de migração do estado do utilizador (USMT) que a sequência de tarefas utiliza ao restaurar o estado do utilizador. Especifique as opções adicionais como uma cadeia, que a sequência de tarefas anexa à linha de comando USMT gerada automaticamente para o LoadState.

As opções USMT especificadas com esta variável de sequência de tarefas não são validadas para precisão antes de executar a sequência de tarefas.

Para obter mais informações sobre as opções disponíveis, consulte [loadState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a>OSDMigrateComputerName

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

(entrada)

Especifica se o nome do computador é migrado.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido). A variável [OSDComputerName (saída)](#OSDComputerName-output) é definida para o nome NetBIOS do computador.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a>OSDMigrateConfigFiles

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Especifica os ficheiros de configuração utilizados para controlar a captura de perfis de utilizador. Esta variável só é utilizada se o `Advanced` [OSDMigrateMode](#OSDMigrateMode) estiver definido para . Este valor da lista delimitada por vírgulas está definido para efetuar a migração personalizada de perfis de utilizador.

#### <a name="example"></a>Exemplo

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a>OSDMigrateContinueOnLockedFiles

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Se o USMT não conseguir capturar alguns ficheiros, esta variável permite que a captura do estado do utilizador prossiga.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido)  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a>OSDMigrateContinueRestaurar

*Aplica-se ao passo [do Estado do Utilizador de Restauração.](task-sequence-steps.md#BKMK_RestoreUserState)*

(entrada)

Continue o processo, mesmo que usMT não possa restaurar alguns ficheiros.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido)  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a>OSDMigrateEnableVerboseLogging

*Aplica-se aos seguintes passos:*  

- [Capturar Estado do Utilizador](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Restaurar Estado do Utilizador](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

Permite a exploração verbosa para USMT. O passo requer este valor.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a>CONTAS LOCAIS OSDMigrate

*Aplica-se ao passo [do Estado do Utilizador de Restauração.](task-sequence-steps.md#BKMK_RestoreUserState)*

(entrada)

Especifica se a conta de computador local é restaurada.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a>OsDMigrateLocalAccountPassword

*Aplica-se ao passo [do Estado do Utilizador de Restauração.](task-sequence-steps.md#BKMK_RestoreUserState)*

(entrada)

Se a variável [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) for, `true`esta variável deve conter a palavra-passe atribuída a *todas as* contas locais migradas. UsMT atribui a mesma senha a todas as contas locais migradas. Considere esta senha como temporária, e mude-a mais tarde por outro método.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a>OSDMigrateMode

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Permite personalizar os ficheiros que o USMT captura.

#### <a name="valid-values"></a>Valores válidos

- `Simple`: A sequência de tarefas utiliza apenas os ficheiros de configuração USMT padrão  

- `Advanced`: A variável de sequência de tarefas [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) especifica os ficheiros de configuração que o USMT utiliza  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a>OsDMigrateNetworkMembership

*Aplica-se ao passo de Definições da [Rede de Captura.](task-sequence-steps.md#BKMK_CaptureNetworkSettings)*

(entrada)

Especifica se a sequência de tarefas migra as informações de membrodo do grupo de trabalho ou do domínio.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido)
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a>OSDMigrateRegistrationInfo

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

(entrada)

Especifica se o passo migra a informação do utilizador e da organização.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido). A variável [OSDRegisteredOrgName (saída)](#OSDRegisteredOrgName-output) é definida para o nome de organização registado do computador.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a>OSDMigrateSkipFicheiros Encriptados

*Aplica-se ao passo [do Estado do Utilizador de Captura.](task-sequence-steps.md#BKMK_CaptureUserState)*

(entrada)

Especifica se são capturados ficheiros encriptados.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a>OSDMigrateTimeZone

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

(entrada)

Especifica se o fuso horário do computador é migrado.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido). A variável [OSDTimeZone (saída)](#OSDTimeZone-output) está definida para o fuso horário do computador.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a>OsdNetworkJoinType

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica se o computador de destino se junta a um domínio de Diretório Ativo ou a um grupo de trabalho.

#### <a name="value-values"></a>Valores de valor

- `0`: Junte-se a um domínio de Diretório Ativo  
- `1`: Junte-se a um grupo de trabalho

### <a name="osdpartitions"></a><a name="OSDPartitions"></a>OsDPartitions

*Aplica-se ao passo do [formato e do disco de partição.](task-sequence-steps.md#BKMK_FormatandPartitionDisk)*

(entrada)

Esta variável de sequência de tarefas é uma variável de matriz de definições de partição. Cada um dos elementos da matriz representa as definições para uma partição individual no disco rígido. Aceda às definições definidas para cada partição, combinando o nome variável da matriz com o número de divisória de disco de base zero e o nome da propriedade.

Utilize os seguintes nomes variáveis para definir as propriedades para a *primeira* partição que este passo cria no disco rígido:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Especifica o tipo de partição. Esta propriedade é necessária. Os valores `Logical`válidos `Hidden`são, `Primary` `Extended`e .

#### <a name="osdpartitions0filesystem"></a>SISTEMA OSDPartitions0FileSystem

Especifica o tipo de sistema de ficheiros a utilizar ao formatar a divisória. Esta propriedade é opcional. Se não especificar um sistema de ficheiros, o passo não formata a partição. Valores `FAT32` válidos são e `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Especifica se a partição é sabotável. Esta propriedade é necessária. Se este valor `TRUE` for definido para discos MBR, então o passo marca esta partição como ativa.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Especifica o tipo de formato que é utilizado. Esta propriedade é necessária. Se este valor `TRUE`estiver definido, o passo executa um formato rápido. Caso contrário, o passo executa um formato completo.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Especifica o nome que é atribuído ao volume quando é formatado. Esta propriedade é opcional.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Especifica o tamanho da divisória. Esta propriedade é opcional. Se esta propriedade não for especificada, a partição é criada usando todo o espaço livre restante. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

O passo utiliza estas unidades para interpretar a variável **OSDPartitions0Size.** Esta propriedade é opcional. Os valores válidos são `MB` (predefinidos), `GB`e `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Quando este passo cria divisórias, utiliza sempre a próxima letra disponível no Windows PE. Utilize esta propriedade opcional para especificar o nome de outra variável de sequência de tarefas. O passo usa esta variável para guardar a nova letra de unidade para referência futura.

Se definir várias divisórias com este passo de sequência de tarefas, as propriedades para a *segunda* partição são definidas utilizando o índice **1** no nome variável. Por exemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, and **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a>Estilo OSDPartition

*Aplica-se ao passo do [formato e do disco de partição.](task-sequence-steps.md#BKMK_FormatandPartitionDisk)*

(entrada)

Especifica o estilo de partição a utilizar ao particionar o disco.

#### <a name="valid-values"></a>Valores válidos

- `GPT`: Utilize o estilo guid partition table
- `MBR`: Utilize o estilo de partição de disco de arranque principal

### <a name="osdproductkey"></a><a name="OSDProductKey"></a>OsdProductKey

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica a chave de produto do Windows. O valor especificado tem de ter entre 1 e 255 carateres.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a>OsdRandomAdminPassword

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica uma palavra-passe gerada aleatoriamente para a conta de Administrador local no novo SISTEMA.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido): Configuração do Windows desativa a conta de Administrador local no computador-alvo  

- `false`: Configuração do Windows permite a conta de administrador local no computador alvo e define a palavra-passe da conta para o valor de [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a>OSDRegisteredOrgName (entrada)

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica o nome de organização registado por defeito no novo SISTEMA. O valor especificado tem de ter entre 1 e 255 carateres.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a>OSDRegisteredOrgName (saída)

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

Definida como o nome da organização registado do computador. O valor só é definido se a variável `true` [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) estiver definida para .

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a>Nome de utilizador registado sinuoso

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica o nome de utilizador registado por defeito no novo SISTEMA. O valor especificado tem de ter entre 1 e 255 carateres.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a>Limite de conexão licença de servidor osdserver

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica o número máximo de ligações permitido. O número especificado tem estar no intervalo de 5 a 9999 ligações.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a>Modo osdserverlicensemode

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

(entrada)

Especifica o modo de licença do Windows Server que é utilizado.

#### <a name="valid-values"></a>Valores válidos

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a>OSDSetupAdicionações adicionais

*Aplica-se ao passo do [Sistema Operativo de Atualização.](task-sequence-steps.md#BKMK_UpgradeOS)*

(entrada)

Especifica as opções adicionais da linha de comando que são adicionadas à Configuração do Windows durante uma atualização do Windows 10. A sequência de tarefas não verifica as opções da linha de comando.

Para obter mais informações, consulte [Windows Setup Command-Line Options (Opções da Linha de Comandos de Configuração do Windows)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a>OSDStateFallbackToNAA

*Aplica-se ao passo [da Loja do Estado de Pedido.](task-sequence-steps.md#BKMK_RequestStateStore)*

(entrada)

Quando a conta de computador não se liga ao ponto de migração do Estado, esta variável especifica se a sequência de tarefas recua para utilizar a conta de acesso à rede (NAA).

Para obter mais informações sobre a conta de acesso à rede, consulte [Contas](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`(predefinido)  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a>OsdStateSMPRetryCount

*Aplica-se ao passo [da Loja do Estado de Pedido.](task-sequence-steps.md#BKMK_RequestStateStore)*

(entrada)

Especifica o número de vezes que o passo de sequência de tarefas tenta encontrar um ponto de migração de estado antes de o passo falhar. O número especificado tem de estar compreendido entre 0 e 600.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a>OSDStateSMPRetryTime

*Aplica-se ao passo [da Loja do Estado de Pedido.](task-sequence-steps.md#BKMK_RequestStateStore)*

(entrada)

Especifica o número de segundos que o passo de sequência de tarefas aguarda entre as tentativas. O número de segundos pode ter um máximo de 30 carateres.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a>OSDStateStorePath

*Aplica-se aos seguintes passos:*  

- [Capturar Estado do Utilizador](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Disponibilizar Armazenamento de Estados](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Solicitar Armazenamento de Estados](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Restaurar Estado do Utilizador](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

A partilha de rede ou o nome de caminho local da pasta onde a sequência de tarefas salva ou restaura o estado do utilizador. Não há valor predefinido.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a>OsdTargetSystemDrive

*Aplica-se ao passo [de imagem de aplicar o OS.](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)*

(saída)

Especifica a letra de unidade da divisória que contém os ficheiros S após a aplicação da imagem.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a>OSDTargetSystemRoot (entrada)

*Aplica-se ao passo [de imagem de captura do OS.](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)*

Especifica o caminho para o diretório do Windows do SISTEMA instalado no computador de referência. A sequência de tarefas verifica-a como um SISTEMA suportado para captura por Configuração Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a>OSDTargetSystemRoot (saída)

*Aplica-se ao preparar o Windows para o passo [de captura.](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)*

Especifica o caminho para o diretório do Windows do SISTEMA instalado no computador de referência. A sequência de tarefas verifica-a como um SISTEMA suportado para captura por Configuração Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a>OSDTimeZone (entrada)

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição de fuso horário predefinido que é usada no novo SISTEMA.

Detete o valor desta variável para o nome invariante da linguagem do fuso horário. Por exemplo, utilize a `Std` corda no valor para um fuso horário sob a seguinte chave de registo: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a>OSDTimeZone (saída)

*Aplica-se ao passo de Definições do [Windows de captura.](task-sequence-steps.md#BKMK_CaptureWindowsSettings)*

Definida como o fuso horário do computador. O valor só é definido se a variável `true` [OSDMigrateTimeZone](#OSDMigrateTimeZone) estiver definida para .

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a>OSDWindowsSettingsInputLocale

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição de local de entrada padrão que é usada no novo SISTEMA.

Para obter mais informações sobre o valor do ficheiro de resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core - InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a>OSDWindowsSettingsSystemSystemLocale

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição de localização do sistema predefinido que é usada no novo SISTEMA.

Para obter mais informações sobre o valor do ficheiro de resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core - SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a>OSDWindowsSettingsULanguage

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição de idioma de interface de utilizador predefinida que é usada no novo SISTEMA.

Para obter mais informações sobre o valor do ficheiro de resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core - UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a>OSDWindowsSettingsUILanguageFallback

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição de linguagem de interface de utilizador que é usada no novo SISTEMA.

Para obter mais informações sobre o valor do ficheiro de resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core - UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a>OSDWindowsSettingsUserLocale

*Aplica-se ao passo [de definições do Windows De aplicação.](task-sequence-steps.md#BKMK_ApplyWindowsSettings)*

Especifica a definição local do utilizador padrão que é usada no novo SISTEMA.

Para obter mais informações sobre o valor do ficheiro de resposta de configuração do Windows, consulte [Microsoft-Windows-International-Core - UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a>Partição osdwipeDestination

*Aplica-se ao passo de Imagem de [Dados aplicado.](task-sequence-steps.md#BKMK_ApplyDataImage)*

(entrada)

Especifica se pretende eliminar os ficheiros localizados na partição de destino.

#### <a name="valid-values"></a>Valores válidos

- `true`(predefinido)
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a>Nome do grupo OSDWork

*Aplica-se ao passo de Definições de [Rede de Aplicação.](task-sequence-steps.md#BKMK_ApplyNetworkSettings)*

(entrada)

Especifica o nome do grupo de trabalho ao qual o computador de destino é associado.

Especifique esta variável ou a variável [OSDDomainName.](#OSDDomainName) O nome do grupo de trabalho pode ter um máximo de 32 carateres.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a>ConfiguraçãoCompletePause

*Aplica-se ao passo do [Sistema Operativo de Atualização.](task-sequence-steps.md#BKMK_UpgradeOS)*

<!-- 4680263 -->

A partir da versão 1910, utilize esta variável para resolver problemas de tempo com a sequência de tarefas de upgrade da Janela 10 em dispositivos de alto desempenho quando a configuração do Windows estiver concluída. Quando atribui um valor em segundos a esta variável, o processo de configuração do Windows atrasa esse tempo antes de iniciar a sequência de tarefas. Este tempo de tempo proporciona ao cliente do Gestor de Configuração tempo adicional para inicializar.

As seguintes entradas de registo são exemplos comuns desta questão que pode remediar com esta variável:

- O componente TSManager regista entradas semelhantes aos seguintes erros no **smsts.log:**

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- A configuração do Windows regista entradas semelhantes aos seguintes erros no **setupcomplete.log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a>Propriedades SMSClientInstallProperties

*Aplica-se ao [passo De Configuração Windows e ConfigMgr.](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)*

(entrada)

Especifica as propriedades de instalação do cliente que a sequência de tarefas utiliza na instalação do cliente Do Gestor de Configuração.

Para mais informações, consulte sobre os parâmetros e propriedades de [instalação do cliente.](../../core/clients/deploy/about-client-installation-properties.md)

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a>SMSConnectNetworkfolderAccount

*Aplica-se ao passo [da pasta de ligação à rede.](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)*

(entrada)

Especifica a conta de utilizador que é utilizada para ligar à parte da rede no [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Especifique a palavra-passe da conta com o valor [smSConnectNetworkPasswordPassword.](#SMSConnectNetworkFolderPassword)

Para obter mais informações sobre a conta de ligação da rede de sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)consulte Contas .

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a>SMSConnectNetworkFolderDriveLetterLetter

*Aplica-se ao passo [da pasta de ligação à rede.](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)*

(entrada)

Especifica a letra de unidade de rede à qual ligar. Este valor é opcional. Se não for especificada, a ligação de rede não está mapeada para uma carta de condução. Se este valor for especificado, o valor deve estar na gama de D a Z. Não utilize X, é a letra de unidade utilizada pelo Windows PE durante a fase do Windows PE.

#### <a name="examples"></a>Exemplos

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a>SMSConnectNetworkfolderPassword

*Aplica-se ao passo [da pasta de ligação à rede.](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)*

(entrada)

Especifica a palavra-passe para a [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) que é usada para ligar à parte da rede no [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a>SMSConnectNetworkfolderPath

*Aplica-se ao passo [da pasta de ligação à rede.](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)*

(entrada)

Especifica o caminho de rede para a ligação. Se precisar de mapear este caminho para uma letra de unidade, utilize o valor [SMSConnectNetworkFolderDriveLetter.](#SMSConnectNetworkFolderDriveLetter)

#### <a name="example"></a>Exemplo

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a>Alvo de atualização de smsinstall

*Aplica-se ao passo [de Instalação](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) de Atualizações de Software.*

(entrada)

Especifica se pretende instalar todas as atualizações ou apenas as atualizações obrigatórias.

#### <a name="valid-values"></a>Valores válidos

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a>Mensagem de reinício de sms

*Aplica-se ao passo [do Computador restart.](task-sequence-steps.md#BKMK_RestartComputer)*

(entrada)

Especifica a mensagem a apresentar aos utilizadores antes de reiniciar o computador de destino. Se esta variável não estiver definida, o texto de mensagem predefinido é apresentado. A mensagem especificada não pode exceder 512 caracteres.

#### <a name="example"></a>Exemplo

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a>SMSRebootTimeout

*Aplica-se ao passo [do Computador restart.](task-sequence-steps.md#BKMK_RestartComputer)*

(entrada)

Especifica o número de segundos durante o qual o aviso é apresentado ao utilizador antes de o computador ser reiniciado.

#### <a name="examples"></a>Exemplos

- `0`(predefinido): Não apresentar uma mensagem de reinício  
- `60`: Mostrar o aviso durante um minuto  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a>SMSTSAssignmentsDownloadInterval

O número de segundos para esperar antes que o cliente tente baixar a apólice desde a última tentativa que não devolveu nenhuma apólice. Por padrão, o cliente espera **0** segundos antes de tentar novamente.

Pode definir esta variável utilizando um comando de pré-início do suporte de dados ou do PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a>SMSTSAssignmentsDownloadRetry

O número de vezes que um cliente tenta descarregar a apólice depois de não serem encontradas apólices na primeira tentativa. Por padrão, o cliente retenta **0** vezes.

Pode definir esta variável utilizando um comando de pré-início do suporte de dados ou do PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a>Modo de Utilizadores SMSTSSign

Especifica como uma sequência de tarefas associa os utilizadores ao computador de destino. Defina a variável num dos seguintes valores:  

- **Auto**: Quando a sequência de tarefas implanta o SISTEMA para o computador de destino, cria uma relação entre os utilizadores especificados e o computador de destino.  

- **Pendente**: A sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino. Um administrador deve aprovar a relação para defini-la.  

- **Desativado**: A sequência de tarefas não associa os utilizadores ao computador de destino quando implementa o SISTEMA.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a>SMSTSDisableStatusRetry

<!--512358-->
Em cenários desligados, o motor de sequência de tarefas tenta enviar repetidamente mensagens de estado para o ponto de gestão. Este comportamento neste cenário causa atrasos no processamento da sequência de tarefas.

Desloque `true` esta variável e o motor de sequência de tarefas não tente enviar mensagens de estado depois de a primeira mensagem não enviar. Esta primeira tentativa inclui múltiplas tentativas.

Quando a sequência de tarefas recomeça, o valor desta variável persiste. No entanto, a sequência de tarefas tenta enviar uma mensagem de estado inicial. Esta primeira tentativa inclui múltiplas tentativas. Se for bem sucedida, a sequência de tarefas continua a enviar o estado independentemente do valor desta variável. Se o estado não enviar, a sequência de tarefas utiliza o valor desta variável.

> [!NOTE]  
> O relatório do estado da sequência de [tarefas](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) baseia-se nestas mensagens de estado para mostrar o progresso, o histórico e os detalhes de cada passo. Se as mensagens de estado não enviarem, não estão na fila. Quando a conectividade é restaurada até ao ponto de gestão, não são enviadas mais tarde. Este comportamento resulta em relatórios de estado de sequência de tarefas incompletos e em falta.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a>SMSTSDisableWow64Redirection

*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

(entrada)

Por padrão num SISTEMA de 64 bits, a sequência de tarefas localiza e executa o programa na linha de comando utilizando o redirector do sistema de ficheiros WOW64. Este comportamento permite que o comando encontre versões de 32 bits de programas de SE e DLLs. A definição `true` desta variável para desativar a utilização do redirector do sistema de ficheiros WOW64. O comando encontra versões nativas de 64 bits de programas de SE e DLLs. Esta variável não tem qualquer efeito ao correr num Sistema Operativo de 32 bits.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a>Código de abortador SMSTSDownload

Esta variável contém o valor de código de abortar para o descarregador de programas externos. Este programa é especificado na variável [SMSTSDownloadProgram.](#SMSTSDownloadProgram) Se o programa devolver um código de erro igual ao valor da variável SMSTSDownloadAbortCode, então o download de conteúdo falha e nenhum outro método de descarregamento é tentado.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a>Programa smstsdownload

Utilize esta variável para especificar um fornecedor de conteúdos alternativo (ACP). Um ACP é um programa de descarregamento que é usado para descarregar conteúdo. A sequência de tarefas utiliza o ACP em vez do downloader padrão do Gestor de Configuração. Como parte do processo de descarregamento de conteúdo, a sequência de tarefas verifica esta variável. Se especificada, a sequência de tarefas executa o programa para descarregar o conteúdo.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a>SMSTSDownloadRetrycount

O número de vezes que o Gestor de Configuração tenta descarregar conteúdo a partir de um ponto de distribuição. Por padrão, o cliente tenta **2** vezes.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a>Atraso no SMSTSDownloadRetryDelay

O número de segundos que o Gestor de Configuração espera antes de voltar a tentar descarregar conteúdo a partir de um ponto de distribuição. Por padrão, o cliente espera **15** segundos antes de tentar novamente.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a>SMSTSDriverRequestConnectTimeout

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

Ao solicitar o catálogo do controlador, esta variável é o número de segundos que a sequência de tarefas aguarda pela ligação do servidor HTTP. Se a ligação demorar mais tempo do que a definição de tempo, a sequência de tarefas cancela o pedido. Por predefinição, o tempo de paragem é definido para **60** segundos.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a>SMSTSDriverRequestReceberTimeout

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

Ao solicitar o catálogo do condutor, esta variável é o número de segundos que a sequência de tarefas aguarda por uma resposta. Se a ligação demorar mais tempo do que a definição de tempo, a sequência de tarefas cancela o pedido. Por predefinição, o tempo de paragem é definido para **480** segundos.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a>SMSTSDriverRequestResolveTimeout

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

Ao solicitar o catálogo do condutor, esta variável é o número de segundos que a sequência de tarefas aguarda pela resolução de nome http. Se a ligação demorar mais tempo do que a definição de tempo, a sequência de tarefas cancela o pedido. Por predefinição, o tempo de paragem é definido para **60** segundos.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a>SMSTSDriverRequestSendTimeout

*Aplica-se ao passo de [autoaplicação dos condutores.](task-sequence-steps.md#BKMK_AutoApplyDrivers)*

Ao enviar um pedido para o catálogo do condutor, esta variável é o número de segundos que a sequência de tarefas aguarda para enviar o pedido. Se o pedido demorar mais tempo do que a definição de tempo, a sequência de tarefas cancela o pedido. Por predefinição, o tempo de paragem é definido para **60** segundos.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a>SMSTSErrorDialogTimeout

Quando ocorre um erro numa sequência de tarefas, apresenta uma caixa de diálogo com o erro. A sequência de tarefas descarta-a automaticamente após o número de segundos especificados por esta variável. Por defeito, este valor é de **900** segundos (15 minutos).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a>Pasta smstslanguagefolder

Utilize esta variável para alterar o idioma de apresentação de uma imagem de arranque de idioma neutro.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a>SMSTSLocalDataDrive

Especifica onde a sequência de tarefas armazena ficheiros temporários no computador de destino enquanto está em execução.

Defina esta variável antes do início da sequência de tarefas, como por exemplo, definindo uma variável de recolha. Uma vez iniciada a sequência de tarefas, o Gestor de Configuração define a [variável _SMSTSMDataPath](#SMSTSMDataPath) assim que a sequência de tarefas começa.

### <a name="smstsmp"></a><a name="SMSTSMP"></a>SMSTSMP

Utilize esta variável para especificar o endereço URL ou IP do ponto de gestão do Gestor de Configuração.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a>SMSTSMPListRequestTimeoutEnabled

*Aplica-se aos seguintes passos:*  

- [Instalar Aplicação](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Se o cliente não estiver na intranet, utilize esta variável para permitir repetidos pedidos de MPList para atualizar o cliente. Por padrão, esta variável está definida para `True`.

Quando os clientes estiverem na internet, detete esta variável para `False` evitar atrasos desnecessários.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a>Tempo de solicitação sMSTSMPListRequestTimeout

*Aplica-se aos seguintes passos:*  

- [Instalar Aplicação](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar Atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Se a sequência de tarefas não conseguir recuperar a lista de pontos de gestão (MPList) dos serviços de localização, esta variável especifica quantos milissegundos espera antes de voltar a tentar o passo. Por defeito, a `60000` sequência de tarefas aguarda milissegundos (60 segundos) antes de se voltar a tentar. Tenta até três vezes.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a>SMSTSpeerDownload

Utilize esta variável para permitir ao cliente utilizar a cache de pares do Windows PE. Configurar esta `true` variável para ativar esta funcionalidade.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a>SmStspeerRequestport

Uma porta de rede personalizada que o Windows PE peer cache utiliza para a transmissão inicial. A porta predefinida configurada nas definições do cliente é **de 8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a>SMSTSPersistContent

Utilize esta variável para manter temporariamente o conteúdo na cache da sequência de tarefas. Esta variável é diferente do [SMSTSPreserveContent,](#SMSTSPreserveContent)que mantém o conteúdo na cache do cliente do Gestor de Configuração após a conclusão da sequência de tarefas. O SMSTSPersistContent utiliza a cache de sequência de tarefas, o SMSTSPreserveContent utiliza a cache do cliente do Gestor de Configuração.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a>SMSTSPostAction

Especifica um comando que é executado após o completo da sequência de tarefas. Por exemplo, `shutdown.exe /r /t 30 /f` especifique para reiniciar o computador 30 segundos após o conclusão da sequência de tarefas.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a>SMSSPreferredAdvertID

Força a sequência de tarefas a executar uma implantação específica no computador de destino. Desloque esta variável através de um comando prestart a partir de meios de comunicação ou PXE. Se esta variável for definida, a sequência de tarefas substitui quaisquer implementações necessárias.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a>SMSTSPreserveContent

Esta variável assinala o conteúdo na sequência de tarefas a manter na cache do cliente do Gestor de Configuração após a implantação. Esta variável é diferente do [SMSTSPersistContent,](#SMSTSPersistContent)que apenas mantém o conteúdo durante a duração da sequência de tarefas. O SMSTSPersistContent utiliza a cache de sequência de tarefas, o SMSTSPreserveContent utiliza a cache do cliente do Gestor de Configuração. Detete O SMSTSPreserveContent para `true` ativar esta funcionalidade.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a>Atraso de reinicialização de SMSTS

Especifica quantos segundos deve aguardar até que o computador seja reiniciado. Se esta variável for zero (0), o gestor da sequência de tarefas não apresentará um diálogo de notificação antes de reiniciar.

#### <a name="example"></a>Exemplo

- `0`: não apresentar uma notificação  

- `60`: apresentar uma notificação por um minuto  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a>Atraso de reinicialização de SMSTSNext

<!--4447680-->
A partir da versão 1906, utilize esta variável com a variável [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) existente. Se quiser que mais tarde ocorram reboots com um tempo de paragem diferente do primeiro, desloque o SMSTSRebootDelayNext a um valor diferente em segundos.

#### <a name="example"></a>Exemplo

Pretende dar aos utilizadores uma notificação de reinício de 60 minutos no início de uma sequência de tarefas de atualização do Windows 10 no local. Depois do primeiro intervalo, quer que os intervalos adicionais sejam de apenas 60 segundos. Despleite o Atraso `3600`do Reboot de SMSTS para , e SMSTSRebootDelayNextA a `60`.  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a>Mensagem de reinício de SMSTS

Especifica a mensagem a exibir no diálogo de notificação de reinício. Se esta variável não estiver definida, aparece uma mensagem predefinida.

#### <a name="example"></a>Exemplo

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a>SMSTSRebootSolicitado

Indica que é pedido um reinício após a conclusão do passo de sequência de tarefas atual. Se o passo da sequência de tarefas exigir um reinício para completar a ação, detete esta variável. Após o reinício do computador, a sequência de tarefas continua a funcionar a partir do próximo passo da sequência de tarefas.

- `HD`: Reiniciar para o Sistema Operativo instalado
- `WinPE`: Reiniciar a imagem de arranque associada

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a>SMSTSRetrySolicitado

Pede uma repetição após a conclusão do passo de sequência de tarefas atual. Se esta variável de sequência de tarefas for definida, `true`também detete a variável [SMSTSRebootRequested](#SMSTSRebootRequested) para . Depois de o computador ser reiniciado, o gestor da sequência de tarefas repete o mesmo passo de sequência de tarefas.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a>SMSTSRunCommandlineasuser

*Começando na versão 2002* <!-- 5573175 -->  
*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

Utilize variáveis de sequência de tarefas para configurar o contexto do utilizador para o passo **da Linha de Comando executar.** Não é necessário configurar o passo da Linha de **Comando executar** com uma conta de espaço reservado para utilizar as variáveis [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) e [SMSTSRunCommandLineUserPassword.](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)

Configure `SMSTSRunCommandLineAsUser` com um dos seguintes valores:

- `true`: Quaisquer outros passos da Linha de Comando `SMSTSRunCommandLineUserName`de **Execução** são executados no contexto do utilizador especificado em .

- `false`: Quaisquer outros passos da Linha de **Comando de Execução** são executados no contexto que configurado no degrau.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a>Nome de utilizador da linha de comando smstsrun

*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

(entrada)

Especifica a conta através da qual a linha de comandos é executada. O valor é uma cadeia de formato nomedeutilizador ou domínio\nomedeutilizador. Especifique a palavra-passe da conta com a variável [SMSTSRunCommandLineUserPassword.](#SMSTSRunCommandLineUserPassword)

> [!NOTE]
> A partir da versão 2002, utilize a variável [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) com esta variável para configurar o contexto do utilizador para este passo.
>
> Na versão 1910 e anterior, configure o passo **da Linha de Comando executar** com a definição para executar este passo como a seguinte **conta**. Quando ativar esta opção, se estiver a definir o nome de utilizador e a palavra-passe com variáveis, especifique qualquer valor para a conta.

Para obter mais informações sobre a conta de execução da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)consulte contas .

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a>SmstsrunCommandlineuserpassword

*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

(entrada)

Especifica a palavra-passe para a conta especificada pela variável [SMSTSRunCommandLineUserName.](#SMSTSRunCommandLineUserName)

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a>SmstsrunPowerShellasuser

*Começando na versão 2002* <!-- 5573175 -->  
*Aplica-se ao passo [do Script PowerShell de execução.](task-sequence-steps.md#BKMK_RunPowerShellScript)*

Utilize variáveis de sequência de tarefas para configurar o contexto do utilizador para o passo **do Script PowerShell executar.** Não é necessário configurar o passo do **Script Run PowerShell** com uma conta de espaço reservado para utilizar as variáveis [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) e [SMSTSRunPowerShellUserPassword.](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)

Configure `SMSTSRunPowerShellAsUser` com um dos seguintes valores:

- `true`: Quaisquer outros passos do **Script PowerShell** executados no contexto do utilizador especificado em `SMSTSRunPowerShellUserName`.

- `false`: Quaisquer outros passos **do Script PowerShell** executados no contexto que configurado no degrau.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a>SmstsrunPowerShelluserName

*Aplica-se ao passo [do Script PowerShell de execução.](task-sequence-steps.md#BKMK_RunPowerShellScript)*

(entrada)

Especifica a conta pela qual o script PowerShell é executado. O valor é uma cadeia de formato nomedeutilizador ou domínio\nomedeutilizador. Especifique a palavra-passe da conta com a variável [SMSTSRunPowerShellUserUserPassword.](#SMSTSRunPowerShellUserPassword)

> [!NOTE]
> Para utilizar estas variáveis, configure o passo do **Script Run PowerShell** com a definição para **executar este passo como a seguinte conta**. Quando ativar esta opção, se estiver a definir o nome de utilizador e a palavra-passe com variáveis, especifique qualquer valor para a conta.

Para obter mais informações sobre a conta de execução da sequência de [tarefas,](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)consulte contas .

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a>SMSTSRunPowerShelluserpassword

*Aplica-se ao passo [do Script PowerShell de execução.](task-sequence-steps.md#BKMK_RunPowerShellScript)*

(entrada)

Especifica a palavra-passe para a conta especificada pela variável [SMSTSRunPowerShellUserName.](#SMSTSRunPowerShellUserName)

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a>SMSTSSoftwareUpdateScanTimeout

*Aplica-se ao passo [de Instalação](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) de Atualizações de Software.*

(entrada)

Controle o tempo de paragem para as atualizações de software durante este passo. Por exemplo, se esperar inúmeras atualizações durante a varredura, aumente o valor. O valor `3600` predefinido é de segundos (60 minutos). O valor variável é definido em segundos.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a>Utilizadores de SMSTSUDA

Especifica os utilizadores primários do computador de destino `<DomainName>\<UserName>`utilizando o seguinte formato: . Separe vários utilizadores utilizando`,`uma vírvia ( ). Para mais informações, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino.

#### <a name="example"></a>Exemplo

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a>Smstswaitforsecondreboot

*Aplica-se ao passo [de Instalação](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) de Atualizações de Software.*

(entrada)

Esta variável de sequência de tarefas opcional controla o comportamento do cliente quando uma instalação de atualização de software requer dois recomeços. Descoloque esta variável antes deste passo para evitar que uma sequência de tarefas falhe devido a um segundo reinício da instalação da atualização de software.

Detete o valor SMSTSWaitForSecondReboot em segundos para especificar quanto tempo a sequência de tarefas para neste passo enquanto o computador reinicia. Dê tempo suficiente para o caso de haver um segundo recomeço.

Por exemplo, se definir o SMSTSWaitForSecondReboot para `600`, a sequência de tarefas para durante 10 minutos após um reinício antes de os passos adicionais funcionarem. Esta variável é útil quando um único passo de sequência de atualizações de software instala centenas de atualizações de software.

> [!Note]
> Esta variável aplica-se apenas a uma sequência de tarefas que implementa um SISTEMA. Não funciona numa sequência de tarefas personalizada. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a>Modo TSDebug

<!--3612274-->
A partir da versão 1906, `TRUE` deset esta variável numa coleção ou objeto de computador para o qual a sequência de tarefas é implementada. Qualquer dispositivo que tenha este conjunto variável colocará qualquer sequência de tarefa saquires no modo de depuração.

Para mais informações, consulte [Debug uma sequência](../deploy-use/debug-task-sequence.md)de tarefas .

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a>Erro DebugOn

<!-- 5012536 -->
A partir da versão 1910, `TRUE` deset esta variável para iniciar automaticamente a [sequência de tarefas](../deploy-use/debug-task-sequence.md) debugger quando a sequência de tarefas devolve um erro.

Desdefinir esta variável usando:

- O passo variável da sequência de [tarefas definida](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Uma variável de coleção. Para mais informações, consulte [Como definir variáveis](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a>TSDisableProgressui

<!-- 1354291 -->
Utilize esta variável para controlar quando a sequência de tarefas apresentar progressos para os utilizadores finais. Para ocultar ou exibir o progresso em diferentes momentos, detete esta variável várias vezes numa sequência de tarefas.  

- `true`: Ocultar o progresso da sequência de tarefas  

- `false`: Progresso da sequência de tarefas de exibição  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a>Aviso de Erroon

*Aplica-se ao passo de [instalação.](task-sequence-steps.md#BKMK_InstallApplication)*

(entrada)

Especifique se o motor de sequência de tarefas considera um aviso detetado como um erro durante este passo. A sequência de tarefas `Warning` define a [variável _TSAppInstallStatus](#TSAppInstallStatus) para quando uma ou mais aplicações, ou uma dependência necessária, não foram instaladas porque não cumpria um requisito. Quando se define `True`esta variável para , `Warning`e a sequência de tarefas define **_TSAppInstallStatus** para , o resultado é um erro. Um valor `False` é o comportamento padrão.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a>TSProgressInfoLevel

*Começando na versão 2002*<!--5932692-->  

Especifique esta variável para controlar o tipo de informação que a janela de progresso da sequência de tarefas exibe. Utilize os seguintes valores para esta variável:

- `1`: Incluir o passo atual e os passos totais para o texto de progresso. Por exemplo, **2 de 10**.
- `2`: Incluir o passo atual, os passos totais e a percentagem concluída. Por exemplo, **2 de 10 (20% completo)**.
- `3`: Incluir a percentagem completada. Por exemplo, **(20% completo)**.

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a>Diretório de Trabalho

*Aplica-se ao passo [da Linha de Comando de Execução.](task-sequence-steps.md#BKMK_RunCommandLine)*

(entrada)

Especifica o diretório inicial para uma ação da linha de comandos. O nome de diretório especificado não pode exceder 255 caracteres.

#### <a name="examples"></a>Exemplos

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Variáveis depreciadas

As seguintes variáveis são depreciadas:

- **OSDAllowUnsignedDriver**: Não é utilizado na implementação do Windows Vista e posteriormente dos sistemas operativos
- **OSDBuildStorageDriverList**: Só se aplica ao Windows XP e ao Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: Só necessário na implementação do Windows XP ou Windows Server 2003
- **OSDInstallEditionIndex**: Não é necessário pós-Windows Vista
- **OSDPreserveDriveLetter**: Para mais informações, consulte [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Esta variável de sequência de tarefas é depreciada.
>
> Durante uma implementação do OS, por padrão, a Configuração do Windows determina a melhor letra de unidade a utilizar (tipicamente C:).

*Comportamento anterior*: ao aplicar uma imagem, a variável OSDPreverveDriveLetter determina se a sequência de tarefas utiliza a letra de unidade capturada no ficheiro de imagem (WIM). Defina o valor `false` desta variável para utilizar a localização que especifica para a definição de **Destino** na etapa de sequência de tarefas **do Sistema Operativo Aplicar.** Para mais informações, consulte [Aplicar a imagem do OS](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Consulte também

- [Passos de sequência de tarefas](task-sequence-steps.md)
- [Utilização de variáveis de sequência de tarefas](using-task-sequence-variables.md)
- [Considerações sobre planeamento para automatizar tarefas](../plan-design/planning-considerations-for-automating-tasks.md)
