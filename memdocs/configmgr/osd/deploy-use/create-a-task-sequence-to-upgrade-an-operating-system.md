---
title: Criar uma sequência de tarefas de atualização do SO
titleSuffix: Configuration Manager
description: Utilize uma sequência de tarefas para atualizar automaticamente do Windows 7 ou mais tarde para o Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b11e0a1747cb8303c14f5971b98d337ae7b2a834
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723006"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um OS em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize sequências de tarefas no Gestor de Configuração para atualizar automaticamente um SISTEMA num computador de destino. Esta atualização pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posteriormente ao Windows Server 2016. Crie uma sequência de tarefas que refira o pacote de upgrade do OS e qualquer outro conteúdo para instalar, tais como aplicações ou atualizações de software. A sequência de tarefas para atualizar um SISTEMA faz parte do Upgrade Windows para o cenário [da versão mais recente.](upgrade-windows-to-the-latest-version.md)  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar a sequência de tarefas, devem estar em vigor os seguintes requisitos:

### <a name="required"></a>Necessário

- O pacote de [atualização OS](../get-started/manage-operating-system-upgrade-packages.md) deve estar disponível na consola 'Gestor de Configuração'.  

- Ao atualizar para o Windows Server 2016, selecione o Ignore qualquer definição de mensagens de **compatibilidade desprezíveis** na etapa de sequência de tarefas do Sistema Operativo de Upgrade. Caso contrário, a atualização falha.  

### <a name="required-if-used"></a>Necessário (se utilizado)  

- [As atualizações de software](../../sum/get-started/synchronize-software-updates.md) devem ser sincronizadas na consola Do Gestor de Configuração.  

- [As aplicações](../../apps/deploy-use/create-applications.md) devem ser adicionadas à consola 'Gestor de Configuração'.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a>Criar uma sequência de tarefas para atualizar um OS  

Para atualizar o SISTEMA nos clientes, crie uma sequência de tarefas e selecione **Atualizar um sistema operativo a partir de um pacote de atualização** no Assistente de Sequência de Tarefas Create. O assistente adiciona os passos da sequência de tarefas para atualizar o SISTEMA, aplicar atualizações de software e instalar aplicações.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione sequências de **tarefas**.  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas**.  

3. Na página Criar uma nova sequência de **tarefas** do Assistente de Sequência de Tarefas, selecione Atualizar um sistema operativo a partir de um pacote de **atualização**, e, em **seguida,** selecione Next .  

4. Na página **informação** da sequência de tarefas, especifique as seguintes definições:  

    - **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    - **Descrição**: Especificar opcionalmente uma descrição.  

5. Na **página 'Actualizar' o Sistema Operativo Windows,** especifique as seguintes definições:  

    - **Pacote de atualização**: Especifique o pacote de atualização que contém os ficheiros de origem de atualização do SO. Verifique se selecionou o pacote de upgrade correto, analisando as informações no painel **Properties.** Para mais informações, consulte [gerir pacotes](../get-started/manage-operating-system-upgrade-packages.md)de upgrade do OS .  

    - **Índice de edição**: Se houver vários índices de edição de OS disponíveis no pacote, selecione o índice de edição pretendido. Por predefinição, o assistente seleciona o primeiro índice.  

    - **Chave do produto**: Especifique a chave do produto Windows para o SISTEMA instalar. Especifique as chaves de licença de volume codificadas ou as chaves padrão do produto. Se utilizar uma chave de produto padrão, separe`-`cada grupo de cinco caracteres por um painel (). Por exemplo: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Quando a atualização é para uma edição de licença de volume, a chave do produto pode não ser necessária.  

        > [!Note]  
        > Esta chave do produto pode ser uma chave de ativação múltipla (MAK), ou uma chave genérica de licenciamento de volume (GVLK). Um GVLK também é referido como uma chave de configuração de cliente de serviço de gestão (KMS). Para mais informações, consulte [Plano de ativação](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)de volume . Para obter uma lista das teclas de configuração do cliente KMS, consulte o [apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server.

    - **Ignore quaisquer mensagens de compatibilidade imperdíveis**: Selecione esta definição se estiver a atualizar para o Windows Server 2016. Se não selecionar esta definição, a sequência de tarefas não está concluída porque a Configuração do Windows está à espera que o utilizador selecione **Confirm** num diálogo de compatibilidade com aplicações do Windows.  

6. Na página **Incluir Atualizações,** especifique se deve instalar as atualizações necessárias, todas ou nenhumas atualizações de software. Em seguida, selecione **Seguinte**. Se especificar para instalar atualizações de software, o Gestor de Configuração instala apenas as atualizações direcionadas para as coleções das quais o computador de destino é membro.  

7. Na página **'Instalar Aplicações',** especifique as aplicações para instalar no computador de destino e, em seguida, selecione **Next**. Se selecionar mais do que uma aplicação, especifique também se a sequência de tarefas deve continuar se a instalação de uma aplicação específica falhar.  

8. Conclua o assistente.  

> [!Important]  
> Quando a sequência de tarefas funciona num dispositivo, o cliente do Gestor de Configuração cria vários scripts para controlar o comportamento da sequência de tarefas em vários cenários. Quando a sequência de tarefas estiver concluída, o cliente não remove estes scripts até que o computador reinicie. Estes ficheiros de guião não contêm informações confidenciais.  

O modelo de sequência de tarefas padrão para a atualização no local do Windows 10 inclui grupos adicionais com ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão a atualizar com sucesso dispositivos para o Windows 10. Para mais informações, consulte as etapas recomendadas de sequência de tarefas [para preparar a atualização](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [para o pós-processamento](#recommended-task-sequence-steps-for-post-processing).

A partir da versão 1806, este modelo de sequência de tarefas também inclui um grupo com ações recomendadas para adicionar caso o processo de atualização falhe. Estas ações facilitam a resolução de problemas. Para mais informações, consulte [os passos recomendados da sequência](#recommended-task-sequence-steps-on-failure)de tarefas sobre a falha .<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Configurar conteúdo de pré-cache

<!--1021244-->
A função pré-cache para implementações disponíveis de sequências de tarefas permite que os clientes descarreguem conteúdo de pacote de upgrade de OS relevante antes de um utilizador instalar a sequência de tarefas.  

Para mais informações, consulte o [conteúdo pré-cache da Configure](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Passos de sequência de tarefas recomendados para preparar a atualização

O modelo de sequência de tarefas padrão para a atualização no local do Windows 10 inclui grupos adicionais com ações recomendadas para adicionar antes do processo de atualização. Estas ações no grupo **Prepare para upgrade** são comuns entre muitos clientes que estão a atualizar com sucesso dispositivos para o Windows 10. Se tiver uma sequência de tarefas existente que ainda não tenha estas ações, adicione-as manualmente à sua sequência de tarefas no grupo **Prepare-se para Atualizar.**  

### <a name="battery-checks"></a>Verificação de baterias

Adicione passos neste grupo para verificar se o computador está a usar bateria ou energia com fios. Esta ação requer um script ou utilidade personalizado para realizar este cheque.

#### <a name="battery-check-example"></a>Exemplo de verificação da bateria

Utilize o WbemTest `root\cimv2` e ligue-se ao espaço de nome. Em seguida, executar a seguinte consulta:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Se devolver os resultados, o dispositivo está a funcionar com a bateria. Caso contrário, o dispositivo está ligado à potência com fios.  

### <a name="networkwired-connection-checks"></a>Verificações de ligação rede/com fios

Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está a usar uma ligação sem fios. Esta ação requer um script ou utilidade personalizado para realizar este cheque.

#### <a name="network-check-example"></a>Exemplo de verificação de rede

Utilize o WbemTest `root\cimv2` e ligue-se ao espaço de nome. Em seguida, executar a seguinte consulta:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Se devolver resultados, o dispositivo está a funcionar no Wi-Fi. Caso contrário, o dispositivo está ligado à ligação à rede com fios.

### <a name="remove-incompatible-applications"></a>Remover aplicações incompatíveis

Adicione passos neste grupo para remover quaisquer aplicações que sejam incompatíveis com esta versão do Windows 10. O método para desinstalar uma aplicação varia.  

Se a aplicação utilizar o Instalador do Windows, copie a linha de comando do **programa Desinstalar** a partir do separador **De si** no separador de implementação do Instalador do Windows. Em seguida, adicione um passo de Linha de **Comando executar** neste grupo com a linha de comando do programa desinstalação. Por exemplo:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Remover condutores incompatíveis

Adicione passos neste grupo para remover quaisquer controladores que sejam incompatíveis com esta versão do Windows 10.  

### <a name="removesuspend-third-party-security"></a>Remover/suspender a segurança de terceiros

Adicione passos neste grupo para remover ou suspender programas de segurança de terceiros, como antivírus.  

Se estiver a utilizar um programa de encriptação de discos de terceiros, forneça o seu controlador de encriptação ao Windows Setup com a `/ReflectDrivers` [opção linha de comando](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Adicione um passo variável de sequência de [tarefas definido](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) na sequência de tarefas deste grupo. Detete a variável de sequência de tarefas para **OSDSetupAdicionalUpgradeOptions**. Desloque `/ReflectDrivers` o valor com o caminho para o condutor. Esta [variável de sequência de tarefas](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) apendia a linha de comando de configuração do Windows utilizada pela sequência de tarefas. Contacte o seu fornecedor de software para obter qualquer orientação adicional sobre este processo.  

### <a name="download-package-content-task-sequence-step"></a>Descarregue passo de sequência de tarefas de conteúdo de pacote  

Utilize o passo de conteúdo do [pacote de descarregamento](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) antes de o **Sistema Operativo de Upgrade** pisar nos seguintes cenários:  

- Utilize uma única sequência de tarefas de atualização para plataformas x86 e x64. Inclua dois passos de conteúdo de pacote de **descarregamento** no grupo **Prepare-se para upgrade.** Estabeleça condições em cada passo para detetar a arquitetura do cliente. Esta condição faz com que o passo descarregue apenas o pacote de upgrade de SO apropriado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

- Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada passo de conteúdo do **pacote de descarregamento** para usar a mesma variável. Em seguida, utilize essa variável para o valor de **conteúdo encenado** na secção de recondutores na etapa do **Sistema Operativo de Atualização.**  

    > [!NOTE]  
    > O Gestor de Configuração adiciona um sufixo numérico a este nome variável. Por exemplo, se `%mycontent%` especificar como variável personalizada, o cliente armazena todos os conteúdos referenciados neste local. Quando se refere à variável num passo posterior, como sistema operativo de **upgrade,** utilize a variável com um sufixo numérico. Neste exemplo, `%mycontent01%` `%mycontent02%`ou , quando o número corresponder à ordem em que a etapa de **Descarregamento** do Conteúdo do Pacote lista este conteúdo específico.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Passos de sequência de tarefas recomendados para pós-processamento

Depois de criar a sequência de tarefas, adicione passos adicionais no grupo **pós-processamento** da sequência de tarefas.  

> [!NOTE]  
> Esta sequência de tarefas não é linear. Existem condições em passos que podem afetar os resultados da sequência de tarefas. Este comportamento depende se atualiza com sucesso o computador cliente, ou se tem de reversão do computador cliente para o SISTEMA original.  

O modelo de sequência de tarefas padrão para a atualização no local do Windows 10 inclui grupos adicionais com ações recomendadas para adicionar após o processo de atualização. Estas ações no grupo **Pós-Processamento** são comuns entre muitos clientes que estão a atualizar com sucesso dispositivos para o Windows 10. Se tiver uma sequência de tarefas existente que ainda não tenha estas ações, adicione-as manualmente à sua sequência de tarefas no grupo **pós-processamento.**  

### <a name="apply-setup-based-drivers"></a>Aplicar condutores baseados em configuração

Adicione passos neste grupo para instalar controladores baseados em configuração (.exe) a partir de pacotes.  

### <a name="installenable-third-party-security"></a>Instalar/ativar a segurança de terceiros

Adicione passos neste grupo para instalar ou ativar programas de segurança de terceiros, como antivírus.  

### <a name="set-windows-default-apps-and-associations"></a>Definir aplicativos e associações padrão do Windows

Adicione passos neste grupo para definir aplicações padrão do Windows e associações de ficheiros.

1. Prepare um computador de referência com as associações de aplicações desejadas.
1. Executar a seguinte linha de comando para exportar:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Adicione o ficheiro XML a uma embalagem.
1. Adicione um passo de linha de comando de [execução](../understand/task-sequence-steps.md#BKMK_RunCommandLine) neste grupo. Especifique a embalagem que contém o ficheiro XML e, em seguida, especifique a seguinte linha de comando:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Para mais informações, consulte as associações de pedidos por [defeito de exportação ou importação.](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)

### <a name="apply-customizations-and-personalization"></a>Aplicar personalizações e personalização

Adicione passos neste grupo para aplicar personalizações de menu Iniciar, tais como organizar grupos de programas. Para mais informações, consulte [Personalizar o ecrã Iniciar](/windows-hardware/manufacture/desktop/customize-the-start-screen).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Passos de sequência de tarefas opcionais para a reversão  

Quando algo corre mal com o processo de atualização após o reinício do computador, o Windows Setup reverte o sistema para o sistema anterior. A sequência de tarefas continua então com quaisquer passos no grupo **Rollback.** Depois de criar a sequência de tarefas, adicione passos opcionais neste grupo, se necessário. Por exemplo, invertê-lo por exemplo, reverter quaisquer alterações feitas no sistema no grupo Preparar para upgrade, tais como desinstalar software incompatível.


## <a name="recommended-task-sequence-steps-on-failure"></a>Passos de sequência de tarefarecomendados sobre falha

<!--1358500-->
A partir da versão 1806, o modelo de sequência de tarefas padrão para a atualização do Windows 10 inclui um grupo para **executar ações sobre falhas**. Este grupo inclui ações recomendadas para adicionar caso o processo de atualização falhe. Estas ações facilitam a resolução de problemas.

### <a name="collect-logs"></a>Recolher registos

Para recolher registos do cliente, adicione passos neste grupo.  

- Uma prática comum é copiar os ficheiros de registo para uma partilha de rede. Para estabelecer esta ligação, utilize o passo [de Ligação à Pasta](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) de Rede.  

- Para executar a operação de cópia, utilize um script ou utilidade personalizado com a linha de [comando executar](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ou executar o passo do [Script PowerShell.](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- Os ficheiros a recolher podem incluir os seguintes registos:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Para obter mais informações sobre o setupact.log e outros registos de configuração do Windows, consulte [os ficheiros de registo](https://docs.microsoft.com/windows/deployment/upgrade/log-files)de configuração do Windows .  

- Para obter mais informações sobre os registos do cliente do Gestor de Configuração, consulte os [registos do cliente do Gestor de Configuração.](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs)  

- Para obter mais informações sobre **_SMSTSLogPath** e outras variáveis úteis, consulte variáveis de sequência de [tarefas.](../understand/task-sequence-variables.md)  

### <a name="run-diagnostic-tools"></a>Executar ferramentas de diagnóstico

Para executar ferramentas de diagnóstico adicionais, adicione passos neste grupo. Automatizar estas ferramentas para recolher informações adicionais do sistema logo após a falha.  

Uma dessas ferramentas é o Windows [SetupDiag.](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) É uma ferramenta de diagnóstico autónoma para obter detalhes sobre o porquê de uma atualização do Windows 10 não ter sido bem sucedida.  

- No 'Gestor de Configuração', [crie um pacote](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) para a ferramenta.  

- Adicione um passo de Linha de [Comando de Execução](../understand/task-sequence-steps.md#BKMK_RunCommandLine) a este grupo da sua sequência de tarefas. Utilize a opção **Pacote** para fazer referência à ferramenta. A seguinte corda é uma linha de **comando**exemplo:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  


## <a name="additional-recommendations"></a>Recomendações adicionais

### <a name="windows-documentation"></a>Documentação do Windows

Reveja a documentação do Windows para resolver erros de [atualização do Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de upgrade.  

### <a name="check-minimum-disk-space"></a>Verifique o espaço mínimo do disco

No degrau de **predefinição Verificar Prontidão,** **certifique-se de espaço mínimo de disco livre (MB)**. Detete o valor para pelo menos **16384** (16 GB) para um pacote de upgrade de 32 bits, ou **20480** (20 GB) por 64 bits.  

### <a name="retry-downloading-policy"></a>Voltar a tentar baixar a política

Utilize a variável de sequência de [tarefas](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** para voltar a tentar a política de descarregamento. Atualmente por padrão, o cliente retenta duas vezes; esta variável é definida para dois (2). Se os seus clientes não estiverem numa ligação de rede intranet com fios, tentativas adicionais ajudam o cliente a obter a apólice. A utilização desta variável não causa nenhum efeito colateral negativo, além de falha retardada se não conseguir descarregar a política.<!--501016--> Aumente também a variável **SMSTSDownloadRetryDelay** a partir do padrão de 15 segundos.  

### <a name="perform-an-inline-compatibility-assessment"></a>Realizar uma avaliação de compatibilidade inline

1. Adicione um segundo passo do **Sistema Operativo de Upgrade** no início do grupo **Prepare-se para atualizar.**  

    1. Nomeie-o *Avaliação de Atualização*.
    1. Especifique o mesmo pacote de atualização e, em seguida, ative a opção de realizar a compatibilidade do **Windows Configuração sem iniciar a atualização**.
    1. Ativar **Continue a erro** no separador Opções.  

1. Imediatamente após este passo de *avaliação* de upgrade, adicione um passo de Linha de **Comando executar.** Especifique a seguinte linha de comando:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. No separador **Opções,** adicione a seguinte condição:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Este código de devolução é o equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma varredura de compatibilidade bem sucedida sem problemas. Se o passo de Avaliação de *Atualização* for bem sucedido e devolver este código, a sequência de tarefas ignora este passo. Caso contrário, se o passo de avaliação devolver qualquer outro código de devolução, este passo falha a sequência de tarefas com o código de retorno da compatibilidade do Windows Setup. Para obter mais informações sobre **_SMSTSOSUpgradeActionReturnCode,** consulte variáveis de sequência de [tarefas.](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)

Para mais informações, consulte o [sistema operativo Upgrade](../understand/task-sequence-steps.md#BKMK_UpgradeOS).  

### <a name="convert-from-bios-to-uefi"></a>Converter de BIOS para UEFI

Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [Converter de BIOS para UEFI durante uma atualização no local](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

### <a name="manage-bitlocker"></a>Gerir o BitLocker

<!--SCCMDocs issue #494-->
Se estiver a utilizar a Encriptação do Disco BitLocker, por padrão, o Windows Setup suspende-o automaticamente durante a atualização. A partir da versão 1803 do Windows `/BitLocker` 10, o Windows Configuração inclui o parâmetro da linha de comando para controlar este comportamento. Se os seus requisitos de segurança exigirem manter sempre a encriptação ativa do disco, utilize a variável de sequência de [tarefas](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** no grupo **Prepare para upgrade** para incluir `/BitLocker TryKeepActive`. Para mais informações, consulte [as opções da linha de comando configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Remover aplicações padrão

<!--SCCMDocs issue #526-->
Alguns clientes removem aplicações predefinidas no Windows 10. Por exemplo, a aplicação Bing Weather ou a Microsoft Solitaire Collection. Em algumas situações, estas aplicações regressam após atualizarem o Windows 10. Para mais informações, consulte [como manter as aplicações removidas do Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Adicione um passo de linha de comando de **execução** na sequência de tarefas no grupo **Preparar para atualizar.** Especifique uma linha de comando semelhante ao seguinte exemplo:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
