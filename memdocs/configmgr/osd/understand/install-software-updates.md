---
title: Instalar Atualizações de Software
titleSuffix: Configuration Manager
description: Recomendações para utilizar o passo da sequência de tarefas Instalar Atualizações de Software no Gestor de Configuração.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6528e979222bc6ecea2a57a003ff5266b5c096c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719996"
---
# <a name="install-software-updates"></a>Instalar Atualizações de Software

*Aplica-se a: Gestor de Configuração (ramo atual)*

O passo de Atualizações de **Software de Instalação** é comumente utilizado nas sequências de tarefas do Gestor de Configuração. Ao instalar ou atualizar o SISTEMA, aciona os componentes de atualizações de software para procurar e implementar atualizações. Este passo pode causar desafios para alguns clientes, tais como atrasos de tempo ou atualizações perdidas. Utilize a informação neste artigo para ajudar a mitigar questões comuns com este passo, e para uma melhor resolução de problemas quando as coisas correm mal.

Para mais informações sobre o passo, consulte [Instalar Atualizações](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) de Software



## <a name="recommendations"></a>Recomendações

Para ajudar este processo a ser bem sucedido, utilize as seguintes recomendações:

- [Utilizar manutenção offline](#use-offline-servicing)
- [Índice único](#single-index)
- [Reduzir o tamanho da imagem](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Utilizar manutenção offline

Utilize o Gestor de Configuração para instalar regularmente atualizações de software aplicáveis aos seus ficheiros de imagem. Esta prática reduz então o número de atualizações que precisa de instalar durante a sequência de tarefas.

Para mais informações, consulte [Aplicar atualizações](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)de software numa imagem .

### <a name="single-index"></a>Índice único

Muitos ficheiros de imagem incluem vários índices, como para diferentes edições do Windows. Reduza o ficheiro de imagem para um único índice que necessita. Esta prática reduz o tempo para aplicar atualizações de software à imagem. Também permite que a próxima recomendação reduza o tamanho da imagem.

A partir da versão 1902, automatiza este processo quando adiciona uma imagem de OS ao site. Para mais informações, consulte [Adicionar uma imagem de OS](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a>Reduzir o tamanho da imagem

Quando aplicar atualizações de software à imagem, otimize a saída removendo quaisquer atualizações supersed. Utilize a ferramenta de linha de comando DISM, por exemplo:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

A partir da versão de 1902, há uma nova opção para automatizar este processo. Para mais informações, consulte a manutenção de [imagem otimizada.](../get-started/manage-operating-system-images.md#bkmk_resetbase)<!--3555951-->


## <a name="image-engineering-decisions"></a>Decisões de engenharia de imagem

Ao conceber o seu processo de imagem, existem várias opções que podem afetar a instalação de atualizações de software:

- [Recapturar periodicamente a imagem](#bkmk_goldimage)  
- [Utilizar manutenção offline](#bkmk_offline)  
- [Utilize apenas a imagem padrão](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a>Recapturar periodicamente a imagem

Tem um processo automatizado para capturar uma imagem de OS personalizada numa programação regular. Esta sequência de tarefas de captura instala as atualizações mais recentes do software. Estas atualizações podem incluir atualizações cumulativas, não cumulativas e outras atualizações críticas, tais como atualizações de pilhas de manutenção (SSU). A sequência de tarefas de implementação instala quaisquer atualizações adicionais desde a captura.

Para obter mais informações sobre este processo, consulte Criar uma sequência de [tarefas para capturar um OS](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Vantagens

- Menos atualizações a aplicar no tempo de implantação por cliente, o que poupa tempo e largura de banda durante a implantação
- Menos atualizações para se preocupar em causar reinícios
- Imagem personalizada para a organização
- Menos variáveis no tempo de implantação

#### <a name="disadvantages"></a>Desvantagens

- Hora de criar e capturar imagem, mesmo que seja maioritariamente automatizado
- Tempo acrescido para distribuir a imagem para pontos de distribuição, que pode ser visto como uma paragem para implementações ativas
- O tempo para testar através de ambientes de pré-produção pode ser mais longo do que o ciclo de patch so, o que pode tornar a imagem atualizada irrelevante


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a>Utilizar manutenção offline

Agendar O Gestor de Configuração para aplicar atualizações de software nas suas imagens.

Para mais informações, consulte [Aplicar atualizações](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)de software numa imagem .

#### <a name="advantages"></a>Vantagens

- Menos atualizações a aplicar no tempo de implantação por cliente, o que poupa tempo e largura de banda durante a implantação
- Menos atualizações para se preocupar em causar reinícios
- Pode agendar o processo de manutenção no local

#### <a name="disadvantages"></a>Desvantagens

- Seleção manual de atualizações
- Aumento do tempo para distribuir a imagem em pontos de distribuição
- Apenas suporta atualizações baseadas na CBS. Não pode aplicar atualizações do Office

> [!Tip]  
> Pode automatizar a seleção de atualizações de software utilizando o PowerShell. Utilize o [cmdlet Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) para obter uma lista de atualizações. Em seguida, utilize o [cmdlet New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) para criar o horário de manutenção offline. O exemplo que se segue mostra um método para automatizar esta ação:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a>Utilize apenas a imagem padrão

Utilize o ficheiro de imagem de instalação do Windows.wim predefinido nas suas sequências de tarefas de implementação.

#### <a name="advantages"></a>Vantagens

- Uma boa fonte conhecida, que reduz o risco de corrupção de imagem como uma possível questão
- Elimina modificações na imagem como um possível problema

#### <a name="disadvantages"></a>Desvantagens

- Potencial para um elevado volume de atualizações durante a implementação
- Aumento do tempo de implementação para cada dispositivo
- Pode não ter necessidade de personalizações, requer passos adicionais de sequência de tarefas para personalizar



## <a name="flowchart"></a>Flowchart

Este diagrama de fluxográfico mostra o processo quando inclui o passo de Atualizações de Software de Instalação numa sequência de tarefas.

[Ver o diagrama em tamanho real](media/ts-step-install-software-updates.svg)

![Diagrama de fluxograma para o passo de sequência de tarefas de atualizações de software de instalação](media/ts-step-install-software-updates.svg)  

1. **O processo começa no cliente:** Uma sequência de tarefas em execução num cliente inclui o passo de atualizações do Software de Instalação.
2. **Compile e avalie políticas**: O cliente compila todas as políticas de atualização de software no espaço de nome WMI RequestedConfigs. (CIAgent.log)
3. *Este caso é a primeira vez que é chamado?*  
    1. **Sim:** Vá ao **exame completo**  
    2. **Não**: *O passo está configurado com a opção de [avaliar atualizações de software a partir de resultados de digitalização em cache?](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)*
        1. **Sim:** Vá à **varredura a partir de resultados em cache**
        2. **Não:** Ir ao **exame completo**
4. Processo de digitalização: ou uma varredura completa ou uma digitalização a partir de resultados em cache, com processo de monitorização em paralelo.
    1. **Digitalização completa**: O motor de sequência de tarefas chama o agente de atualização de software através da API de atualização para fazer uma varredura *completa.* (WUAHandler.log, ScanAgent.log)  
        1. **SUM agent scan - completo**: Processo normal de digitalização via Windows Update Agent (WUA), que comunica com o ponto de atualização de software que executa o WSUS. Adiciona quaisquer atualizações aplicáveis à loja de atualizações local. (WindowsUpdate.log, UpdateStore.log)
    2. **Scan a partir de resultados em cache**: O motor de sequência de tarefas chama o agente de atualização de software através da API de Atualização para digitalizar contra metadados em cache. (WUAHandler.log, ScanAgent.log)
        1. **SUM agent scan - cached**: O Agente de Atualização do Windows (WUA) verifica contra as atualizações já em cache na loja de atualizações local. (WindowsUpdate.log, UpdateStore.log)
    3. **Iniciar o temporizador**de arranque : O motor de sequência de tarefas inicia um temporizador e espera. (Este processo ocorre em paralelo com a varredura completa ou a digitalização do processo de resultados em cache.)
        1. **Monitorização**: O motor de sequência de tarefas monitoriza o agente SUM para o estado.
        2. *Qual é a resposta do agente da SUM?*
            - **Em curso**: O temporizador atingiu o valor na variável de sequência de [tarefas SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)? (Padrão 1 hora)
                - **Sim:** O passo falha.
                - **Não:** Ir para **a Monitorização**
            - **Falha:** O passo falha.
            - **Completo**: Vá à lista de **atualizações do Enumerate**
5. **Enumerar lista de atualizações**: O agente SUM enumera a lista de atualizações devolvidas pela digitalização, determinando quais estão disponíveis ou obrigatórias.
6. *Há alguma atualização na lista de resultados da digitalização?*
    - **Sim:** Ir instalar **atualizações**
    - **Não:** Nada para instalar, o passo completa com sucesso.
7. Processo de implementação: O processo de atualizações de instalação acontece em paralelo com o processo de monitorização da implementação.
    1. **Instalar atualizações**: O motor de sequência de tarefas chama o agente SUM através da Atualização API para instalar todas as atualizações disponíveis ou apenas obrigatórias. Este comportamento baseia-se na configuração do passo, quer selecione **o Necessário para a instalação - Apenas atualizações obrigatórias** de software ou disponíveis para **instalação - Todas as atualizações**de software . Também pode especificar este comportamento utilizando a variável [SMSInstallUpdateTarget.](task-sequence-variables.md#SMSInstallUpdateTarget)
        1. **Instalação**do agente SUM : Processo normal de instalação utilizando a lista de atualizações em cache existente, com o download padrão de conteúdos. Instale a atualização através do Windows Update Agent (WUA). (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Inicie o temporizador de implantação e mostre o progresso**: O motor de sequência de tarefas inicia um temporizador de instalação, mostra sub-progresso em intervalos de 10% na TS Progress UI, e espera.
        1. **Monitorização**: A sequência de tarefas do motor de intervenção coloca o agente SUM em função do estado.
        2. *Qual é a resposta do agente da SUM?*
            - **Em curso**: O processo de *instalação esteve inativo durante 8 horas?*
                - **Sim:** O passo falha.
                - **Não:** Ir para **a Monitorização**
            - **Falha:** O passo falha.
            - **Completo**: Ir a *É o passo configurado com a opção de **avaliar atualizações de software a partir de resultados de digitalização em cache?***


### <a name="timeouts"></a>Tempos limite

O diagrama inclui duas das variáveis de tempo limite que se aplicam a este passo. Existem outros temporizadores padrão de outros componentes que podem afetar este processo.

- Atualização tempo de tempo: 1 hora (smsts.log)  
- Tempo de tempo de pedido de localização: 1 hora (LocationServices.log, CAS.log)  
- Tempo de descarregamento de conteúdos: 1 hora (DTS.log)  
- Tempo de tempo de distribuição inativa: 1 hora (LocationServices.log, CAS.log)  
- Total de tempo de instalação inativa: 8 horas (smsts.log)  



## <a name="troubleshooting"></a>Resolução de problemas

Utilize os seguintes recursos e informações adicionais para ajudá-lo a resolver problemas com este passo:

- Certifique-se de direcionar as implementações da atualização do software para a mesma coleção que a implementação da sequência de tarefas.  

- Certifique-se de incluir pontos de atualização de software em grupos de fronteira. Para mais informações, consulte este artigo do [Microsoft Support](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Para ajudá-lo a resolver o processo de gestão de atualizações de software, consulte a resolução de problemas de gestão de [atualizações](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager)de software .  

- Para ajudar a melhorar o desempenho global, reduza o tamanho do catálogo de atualizações de software. Por exemplo:  

    - Remova classificações, produtos e línguas desnecessários. Para mais informações, consulte classificações e produtos da [Configuração para sincronizar](../../sum/get-started/configure-classifications-and-products.md).  

    - Reindexe a base de dados do site e reconstrua as estatísticas. Para mais informações, consulte o Gestor de [Configuração Perf e](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)o Papel Branco de Orientação de Escala .  

    - Recuse atualizações desnecessárias, por exemplo:
        - Substituído (A partir da versão 1810, o Gestor de Configuração faz esta ação para si. Para mais informações, consulte o comportamento de [limpeza wSUS a partir da versão 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itânio
        - Beta
        - Versão Seguinte
        - ARM
        - Versões do Windows que não está a implementar
