---
title: Estado de funcionamento da ligação do monitor
titleSuffix: Configuration Manager
description: Detalhes sobre como monitorizar os estados de saúde e dispositivo de ligação para desktop Analytics no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fdc15860f2d093a4c9c61b787ba0b780051d3f3d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864876"
---
# <a name="monitor-connection-health"></a>Estado de funcionamento da ligação do monitor

Utilize o painel de **conexão Health** no Gestor de Configuração para reduzir as categorias pela saúde do dispositivo. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o nó de manutenção desktop **Analytics** e selecione o painel de assistência à saúde de **ligação.**  

[![Screenshot do painel de saúde de conexão do gestor de configuração](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Quando configurar pela primeira vez o Desktop Analytics, estes gráficos podem não mostrar dados completos. Pode levar 2 a 3 dias para que os dispositivos ativos enviem dados de diagnóstico para o serviço Desktop Analytics, o serviço para processar os dados e, em seguida, sincronizar com o site do Gestor de Configuração.<!-- 4098037 -->

## <a name="connection-details"></a>Detalhes da ligação

Este azulejo apresenta as seguintes informações básicas sobre a ligação do Gestor de Configuração ao Desktop Analytics:

- **Nome**do inquilino : O nome da ligação Desktop Analytics no nó **dos Serviços Azure**

- **Coleção de alvos**: A mesma coleção de *destino* que especificou ao ligar o Gestor de Configuração ao Desktop Analytics. Esta recolha inclui todos os dispositivos que o Gestor de Configuração conere com as definições de ID comerciais e dados de diagnóstico. É o conjunto completo de dispositivos que o Gestor de Configuração liga ao serviço Desktop Analytics.

- **Dispositivos direcionados:** Todos os dispositivos da recolha do alvo, menos os seguintes tipos de dispositivos:

  - Desativado
  - Obsoleto
  - Inativa
  - Não gerido
  - Dispositivos que executam versões do Canal de Manutenção de Longo Prazo (LTSC) do Windows 10
  - Dispositivos que executam o Servidor do Windows

    Para obter mais informações sobre estes estados do dispositivo, consulte sobre o [estado do cliente](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > O Gestor de Configuração envia para desktop Analytics todos os dispositivos na coleção de alvos menos clientes desativados e obsoletos.

- **Dispositivos elegíveis para DA**: O número de dispositivos direcionados menos dispositivos que não são elegíveis para desktop Analytics. Por exemplo, dispositivos na coleção de alvos que executam o Windows Server ou o Canal de Manutenção a longo prazo do Windows 10 (LTSC).

## <a name="last-sync-details"></a>Últimos detalhes de sincronização

Este azulejo mostra quando o Gestor de Configuração sincroniza com o serviço de nuvem Desktop Analytics e quantos dispositivos sincroniza.

- **Dispositivos sincronizados**: O número de dispositivos elegíveis que o Gestor de Configuração enviou para desktop Analytics. O serviço inclui estes dispositivos no instantâneo atualmente visível.

- **Última sincronização de serviço**: O mesmo que a última hora **atualizada** no portal Desktop Analytics.

- **Próxima sincronização de serviço**: Quando pode esperar o próximo instantâneo diário no Desktop Analytics.

> [!Note]  
> Quando inscreveu os dispositivos pela primeira vez no Desktop Analytics, pode levar vários dias para os dados carregarem e processarem. Durante este tempo, o **último azulejo de sincronização** pode parecer em branco.
> Além disso, nenhum dos valores neste azulejo atualiza automaticamente quando solicita um instantâneo a pedido. Para mais informações, consulte [a latência de Dados](troubleshooting.md#data-latency).

Se pensa que alguns dispositivos não estão a aparecer no Desktop Analytics, certifique-se de que os dispositivos são suportados pelo Desktop Analytics. Para mais informações, consulte [os pré-requisitos.](overview.md#prerequisites)

## <a name="connection-health"></a>Saúde de ligação

O gráfico de **saúde da Ligação** apresenta o número de dispositivos nos seguintes estados de saúde:  

- [Devidamente matriculado](#properly-enrolled): O dispositivo aparece no Desktop Analytics com um inventário completo
- [Incapaz de se inscrever](#unable-to-enroll): Há um problema de bloqueio que impede a inscrição do dispositivo
- [Alerta de configuração](#configuration-alert): O dispositivo não aparece no Desktop Analytics ou aparece com um inventário incompleto. O Gestor de Configuração também identificou um problema com a inscrição do dispositivo.
- [Aguardando inscrição](#awaiting-enrollment): O Gestor de Configuração configurou o dispositivo, mas ainda não aparece no Desktop Analytics
- [Estado pendente](#status-pending): O Gestor de Configuração ainda está a configurar este dispositivo, ou não tem dados suficientes do dispositivo para determinar o seu estado
- [Dados em falta](#missing-data): Configuração Do Gestor configurado o dispositivo, mas desktop Analytics apenas tem dados parciais

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

O número total de dispositivos neste gráfico deve ser o mesmo que os **Dispositivos elegíveis para** o valor da DA no azulejo De Connection Details.

Selecione a fatia na tabela para perfurar até uma lista de dispositivos com esse estado. Para mais informações, consulte a [lista do Dispositivo](#device-list).

Selecione o nome da categoria na legenda para removê-lo ou adicioná-lo do gráfico. Esta ação ajuda a ampliar o gráfico para que possa ver os tamanhos relativos de segmentos menores.

### <a name="properly-enrolled"></a>Devidamente matriculado

O dispositivo tem os seguintes atributos:

- Uma versão cliente do Gestor de Configuração 1902 ou mais tarde  
- Não existem erros de configuração  
- Desktop Analytics recebeu dados completos de diagnóstico deste dispositivo nos últimos 28 dias  
- Desktop Analytics tem um inventário completo da configuração do dispositivo e aplicações instaladas  

### <a name="unable-to-enroll"></a>Incapaz de se inscrever

O Gestor de Configuração deteta um ou mais problemas de bloqueio que impedem a inscrição do dispositivo. Para mais informações, consulte a lista de propriedades do dispositivo Desktop Analytics no Gestor de [Configuração](#bkmk_config-issues).  

Por exemplo, o cliente do Gestor de Configuração não é pelo menos a versão 1902 (5.0.8790). Atualize o cliente para a versão mais recente. Considere permitir a atualização automática do cliente para o site do Gestor de Configuração. Para mais informações, consulte [os clientes de Upgrade](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> Há um problema conhecido com a atualização de segurança estendida de abril de 2020 (ESU) para o Windows 7 que faz com que os dispositivos reportem mal este erro. Para mais informações, consulte notas de [lançamento](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

A partir da versão 2002, pode identificar mais facilmente os problemas de configuração de procuração de clientes em duas áreas:

- **Verificações**de conectividade endpoint : Se os clientes não conseguirem alcançar um ponto final necessário, você vê um alerta de configuração no painel de instrumentos. Aperte-se em clientes que não consigam inscrever-se para ver os pontos finais aos quais os clientes não podem ligar devido a problemas de configuração por procuração. Para mais informações, consulte verificações de [conectividade Endpoint](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Estado de conectividade**: Se os seus clientes utilizarem um servidor proxy para aceder ao Desktop Analytics, o Gestor de Configuração apresenta problemas de autenticação por procuração dos clientes. Faça um trabalho para ver clientes que não possam inscrever-se devido a problemas de autenticação por procuração. Para mais informações, consulte [o estado da Conectividade.](#connectivity-status)<!-- 4963383 -->

### <a name="configuration-alert"></a>Alerta de configuração

O dispositivo não aparece no Desktop Analytics ou aparece com um inventário incompleto. O Gestor de Configuração também identificou um problema com a inscrição do dispositivo. Para mais informações, consulte a lista de propriedades do dispositivo Desktop Analytics no Gestor de [Configuração](#bkmk_config-issues).

Por exemplo, o dispositivo não tem conectividade com o serviço. Para mais informações, consulte a conectividade do ponto final do [Windows.](#windows-diagnostic-endpoint-connectivity)

### <a name="awaiting-enrollment"></a>Aguardando inscrição

O Desktop Analytics não tem dados de diagnóstico para este dispositivo. Este problema pode ser porque adicionou recentemente o dispositivo à recolha do alvo e ainda não enviou dados. Também pode significar que o dispositivo não está a comunicar adequadamente com o serviço, e os dados de diagnóstico mais recentes têm mais de 28 dias.

Certifique-se de que o dispositivo pode comunicar com o serviço. Para mais informações, consulte [Pontos Finais](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Estado pendente

O Gestor de Configuração ainda está a configurar este dispositivo, ou não tem dados suficientes do dispositivo para determinar o seu estado.

### <a name="missing-data"></a>Dados em falta

O Gestor de Configuração configurou com sucesso o dispositivo, mas o Desktop Analytics não consegue criar uma avaliação de compatibilidade. Não tem um conjunto completo de dados para a configuração do dispositivo (recenseamento) ou aplicações instaladas (inventário).

Este problema é muitas vezes corrigido automaticamente quando o dispositivo se retenta. Se persistir, certifique-se de que o dispositivo pode comunicar com o serviço. Para mais informações, consulte [Pontos Finais](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Lista de dispositivos

Para ver uma lista específica de dispositivos por estado, comece pelo dashboard **Connection Health.** Selecione um dos segmentos do azulejo de **saúde connection** e aperte até uma lista de dispositivos neste estado. Esta visualização personalizada do dispositivo apresenta as seguintes colunas Desktop Analytics por padrão:

- Configuração de ID comercial
- Atualização mínima de compatibilidade
- Opt-in de dados de diagnóstico do Windows
- Opt-in de dados comerciais do Windows
- Conectividade final do ponto final do windows de diagnóstico
- Estado de conectividade (a partir da versão 2002)
- Verificações de conectividade endpoint (a partir da versão 2002)

Estas colunas correspondem aos [pré-requisitos](overview.md#prerequisites) fundamentais para que os dispositivos se comuniquem com desktop Analytics.

[![Screenshot da lista de dispositivos incapazes de inscrever](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Selecione um dispositivo para ver a lista completa das propriedades disponíveis no painel de detalhes. Também pode adicionar qualquer uma destas propriedades como colunas à lista de dispositivos.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a>Propriedades do dispositivo

As seguintes propriedades do dispositivo Desktop Analytics estão disponíveis como colunas na lista de dispositivos do Gestor de Configuração:

- [Verificações](#endpoint-connectivity-checks) de conectividade endpoint (a partir da versão 2002)
- [Estado de conectividade](#connectivity-status) (a partir da versão 2002)
- [Configuração do avaliador](#appraiser-configuration)  
- [Atualização mínima de compatibilidade](#minimum-compatibility-update)  
- [Versão do avaliador](#appraiser-version)  
- [Última e bem sucedida corrida completa de Avaliador](#last-successful-full-run-of-appraiser)  
- [Recolha de dados do avaliador](#appraiser-data-collection)  
- [Última e bem sucedida execução completa de Censos](#last-successful-full-run-of-census)  
- [Recolha de dados de recenseamento](#census-data-collection)  
- [Conectividade final do ponto final do windows de diagnóstico](#windows-diagnostic-endpoint-connectivity)  
- [Verifique os dados de diagnóstico do utilizador final](#check-end-user-diagnostic-data)  
- [Verifique o proxy do utilizador](#check-user-proxy)  
- [Configuração de ID comercial](#commercial-id-configuration)  
- [Opt-in de dados comerciais do Windows](#windows-commercial-data-opt-in)  
- [Verifique o nome do dispositivo em dados de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuração do serviço DiagTrack](#diagtrack-service-configuration)  
- [Versão DiagTrack](#diagtrack-version)  
- [Recuperação de ID SQM](#sqm-id-retrieval)  
- [Recuperação de identificador de dispositivo único](#unique-device-identifier-retrieval)  
- [Opt-in de dados de diagnóstico do Windows](#windows-diagnostic-data-opt-in)  

Os **bloqueadores de inscrição mais frequentes e alertas** de configuração do painel de instrumentos Connection Health exibem as propriedades que os dispositivos mais frequentemente reportam como um problema.

### <a name="endpoint-connectivity-checks"></a>Verificações de conectividade endpoint

Começando na versão 2002,<!-- 4963230 --> para detetar problemas de autenticação por procuração, os clientes realizam controlos de conectividade contra os pontos finais necessários. Se um cliente não consegue alcançar um ponto final necessário, esta propriedade mostra uma lista numerada de pontos finais aos quais não pode ligar devido a problemas de configuração de procuração. Compare esta lista com a lista publicada de [pontos finais necessários](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Estado da conectividade

Começando na versão 2002,<!-- 4963383 --> se os seus clientes utilizarem um servidor proxy para aceder ao Desktop Analytics, esta propriedade mostra problemas de autenticação por procuração. Inclui os seguintes detalhes relacionados com a autenticação por procuração:

- Código de estado
- Código de retorno

Verá erros semelhantes aos seguintes no ficheiro de registo:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Onde `%s` está o URL de um ponto final necessário.

Também pode ver mensagens de erro não determinísticas que não precisam de atenção até que os dispositivos tenham problemas de inscrição. Por exemplo:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Para obter mais informações sobre a configuração de servidores proxy para utilização com desktop Analytics, consulte a [autenticação](enable-data-sharing.md#proxy-server-authentication)do servidor Proxy .

### <a name="appraiser-configuration"></a>Configuração do avaliador

<!--20,21-->
O avaliador é o componente Do Windows que corresponde às [atualizações](enroll-devices.md#update-devices)de compatibilidade . Avalia as aplicações e os condutores no dispositivo para compatibilidade com a versão mais recente do Windows.

Se esta verificação for bem sucedida, o componente de avaliação está corretamente configurado no dispositivo.

Caso contrário, poderá apresentar um dos seguintes erros:

- Não é possível configurar a recolha de dados de compatibilidade da aplicação do dispositivo (SetRequestAllAppraiserVersions). Verifique os registos para obter os detalhes da exceção  

- Não é possível configurar a recolha de dados de compatibilidade da aplicação do dispositivo (SetRequestAllAppraiserVersions). Verifique os registos para obter os detalhes da exceção  

- Não é possível escrever as Versões RequestAllAppraiserVersions à chave de registo `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser` . Verifique permissões  

Verifique as permissões desta chave de registo. Certifique-se de que a conta do Sistema local pode aceder a esta chave para o cliente do Gestor de Configuração definir.  

Para mais informações, reveja o registo m365AHandler no cliente.  

### <a name="minimum-compatibility-update"></a>Atualização mínima de compatibilidade

<!--18,19,32-->
A atualização de compatibilidade (appraiser.dll) não está instalada nem desatualizada no dispositivo. É mais antigo do que o requisito mínimo para desktop Analytics, 10.0.17763.

Instale a última atualização de compatibilidade. Para mais informações, consulte [as atualizações](enroll-devices.md#update-devices)da Compatibilidade .

### <a name="appraiser-version"></a>Versão do avaliador

Esta propriedade exibe a versão atual do componente Appraiser no dispositivo. Mostra a versão do ficheiro, `%windir%\System32\appraiser.dll` sem os pontos decimais. Por exemplo, a versão de ficheiro 10.0.17763 exibe como 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Última e bem sucedida corrida completa de Avaliador

Esta propriedade exibe a data e hora que o dispositivo executou com sucesso o Appraiser.

### <a name="appraiser-data-collection"></a>Recolha de dados do avaliador

<!--Appraiser run status-->
<!--22,33-->
Esta propriedade mostra o resultado mais recente do Windows executar o componente de avaliação.

Se não for bem sucedido, pode mostrar um dos seguintes erros:

- Não é possível recolher dados de compatibilidade de aplicações (RunAppraiser). Verifique os registos para obter detalhes  

- A recolha de dados de compatibilidade com aplicações (CompatTelRunner.exe) terminou com um código de erro  

Para mais informações, reveja o registo m365AHandler no cliente.

Verifique o seguinte ficheiro: `%windir%\System32\CompatTelRunner.exe` . Se não existir, reinstale as atualizações de [compatibilidade necessárias](enroll-devices.md#update-devices). Certifique-se de que nenhum outro componente do sistema está a remover este ficheiro, como a política de grupo ou um serviço antimalware.

Se o ficheiro M365AHandler.log no cliente incluir um dos seguintes erros:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Para ajudar a remediar estes erros, execute os seguintes comandos a partir de uma consola elevada do Windows PowerShell no cliente afetado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Última e bem sucedida execução completa de Censos

Esta propriedade exibe a data e hora que o dispositivo executou com sucesso Census.

### <a name="census-data-collection"></a>Recolha de dados de recenseamento

<!-- Census run status -->
<!--51,52-->
O recenseamento é o componente do Windows que inventa o dispositivo. Estes dados de inventário são utilizados para compreender o dispositivo e a sua configuração.

Esta propriedade mostra o resultado mais recente do Windows executar o componente de recenseamento.

Se não for bem sucedido, pode mostrar um dos seguintes erros:

- Não é possível recolher dados sobre o dispositivo e a sua configuração (RunCensus). Verifique os registos para obter os detalhes da exceção  

- Dispositivo e ferramenta de recolha de dados de configuração (devicecensus.exe) não encontrado  

Para mais informações, reveja o registo m365AHandler no cliente.

Verifique o seguinte ficheiro: `%windir%\System32\DeviceCensus.exe` . Se não existir, reinstale as atualizações de [compatibilidade necessárias](enroll-devices.md#update-devices). Certifique-se de que nenhum outro componente do sistema está a remover este ficheiro, como a política de grupo ou um serviço antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividade final do ponto final do windows de diagnóstico

<!--12,15-->
Se esta verificação for bem sucedida, o dispositivo pode ligar-se à experiência do utilizador conectado e ao ponto final da Telemetria (Vortex).

Caso contrário, pode apresentar um dos seguintes erros:  

- Não é possível ligar-se à experiência do utilizador conectado e ao ponto final de telemetria (Vortex). Verifique as definições de rede/procuração  

- Não é possível verificar a conectividade com a experiência do utilizador conectado e o ponto final da telemetria (CheckVortexConnectivity). Verifique os registos para obter os detalhes da exceção  

Os dispositivos verificam a conectividade com um pedido GET para o seguinte ponto final com base na versão OS:

| Versão do SO | Ponto Final |
|------------|----------|
| - Windows 10, versão 1809 ou mais tarde<br/>- Windows 10, versão 1803 com a atualização cumulativa 2018-09 ou posterior | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1803 *sem* a atualização acumulada 2018-09 ou posterior | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1709 ou mais cedo | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 ou Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Certifique-se de que o dispositivo pode comunicar com o serviço. Este cheque valida alguns, mas não todos os pontos finais necessários. Para mais informações, consulte [Pontos Finais](enable-data-sharing.md#endpoints).  

Para mais informações, reveja o registo m365AHandler no cliente.  

### <a name="check-end-user-diagnostic-data"></a>Verifique os dados de diagnóstico do utilizador final

<!--1004-->
Se esta verificação não for bem sucedida, um utilizador selecionou dados de diagnóstico do Windows mais baixos no dispositivo. Também pode ser causado por um objeto político de grupo conflituoso. Para mais informações, consulte [as definições do Windows](enroll-devices.md#windows-settings).

Dependendo dos seus requisitos de negócio, pode desativar a escolha do utilizador através da política de grupo. Utilize a definição para configurar a **definição de opt-in de definição de telemetria**. Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Verifique o proxy do utilizador

<!--30,35-->
A definição DesactivadaEnterpriseAuthProxy está ativada por padrão para o Windows 7. Para computadores Windows 8.1, o Gestor de Configuração define a definição de DisableEnterpriseAuthProxy para 0 (não desativado).

Esta propriedade pode apresentar os seguintes erros:

- O proxy de autenticação está ativado. Definir DisableEnterpriseAuthProxy a 0 em`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Não posso verificar o estado de procuração de autenticação. Verifique os registos para obter os detalhes da exceção

Para mais informações, reveja o registo m365AHandler no cliente.  

Verifique as permissões desta chave de registo. Certifique-se de que a conta do Sistema local pode aceder a esta chave para o cliente do Gestor de Configuração definir. Também pode ser causado por um objeto político de grupo conflituoso. Para mais informações, consulte [as definições do Windows](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuração de ID comercial

<!--9, 11, 53-->
A Microsoft utiliza um ID comercial único para mapear informações de dispositivos para o seu espaço de trabalho desktop Analytics. Quando integra o Gestor de Configuração com desktop Analytics, ele automaticamente consulta o serviço para este ID. O Gestor de Configuração deve aplicar automaticamente este ID aos clientes aos quais se direciona as definições do Desktop Analytics.

Se esta verificação for bem sucedida, o dispositivo está devidamente configurado com um ID comercial.

Caso contrário, pode apresentar um dos seguintes erros:

- Não se pode escrever o CommercialId para a chave de `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` registo. Verifique permissões  

- Não é possível atualizar o CommercialId na chave de registo `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Verifique os registos para obter os detalhes da exceção  

- Fornecer o valor CommercialId correto em`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para mais informações, reveja o registo m365AHandler no cliente.  

Verifique as permissões desta chave de registo. Certifique-se de que a conta do Sistema local pode aceder a esta chave para o cliente do Gestor de Configuração definir. Também pode ser causado por um objeto político de grupo conflituoso. Para mais informações, consulte [as definições do Windows](enroll-devices.md#windows-settings).  

Há uma identificação diferente para o dispositivo. Esta chave de registo é utilizada pela política de grupo. Tem precedência sobre o ID fornecido pelo Gestor de Configuração.  

<a name="bkmk_ViewCommercialID"></a>Para visualizar o ID comercial no portal Desktop Analytics, utilize o seguinte procedimento:

1. Vá ao portal Desktop Analytics e selecione **serviços Conectados** no grupo Definições Globais.  

2. No painel de **serviços Conectados,** o painel de **dispositivos De Inscrição** é selecionado por defeito. No painel de dispositivos De Inscrição, a secção informação apresenta a sua chave de IDENTIFICAção Comercial.  

[![Screenshot do ID comercial no portal Desktop Analytics](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Só **obtenha uma nova chave de identificação** quando não puder usar a atual. Se regenerar o ID comercial, [reinscreva os seus dispositivos com o novo Id](enroll-devices.md#device-enrollment). Este processo pode resultar na perda de dados de diagnóstico durante a transição.  

### <a name="windows-commercial-data-opt-in"></a>Opt-in de dados comerciais do Windows

<!--64-->
Esta propriedade é específica para dispositivos que executam o Windows 7 ou Windows 8.1. Executa testes semelhantes aos dados de [diagnóstico do Windows,](#windows-diagnostic-data-opt-in)com exceção do valor ComercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Verifique o nome do dispositivo em dados de diagnóstico

<!--56,58-->
Se esta verificação for bem sucedida, o dispositivo está corretamente configurado para partilhar o nome do dispositivo.

Caso contrário, pode apresentar um dos seguintes erros:

- Não é possível verificar se o nome do dispositivo será enviado para a Microsoft como parte dos dados de diagnóstico do Windows. Verifique os registos para obter os detalhes da exceção  

- Não é possível escrever AllowDeviceNameInTelemettry para a chave de registo `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` . Verifique permissões  

Para mais informações, reveja o registo m365AHandler no cliente.  

Verifique as permissões desta chave de registo. Certifique-se de que a conta do Sistema local pode aceder a esta chave para o cliente do Gestor de Configuração definir. Também pode ser causado por um objeto político de grupo conflituoso. Para mais informações, consulte [as definições do Windows](enroll-devices.md#windows-settings).  

Certifique-se de que outro mecanismo político, como a política de grupo, não está a desativar este cenário.

### <a name="diagtrack-service-configuration"></a>Configuração do serviço DiagTrack

<!--44,45,50-->
Se esta verificação for bem sucedida, o componente DiagTrack está corretamente configurado no dispositivo. A versão mínima exigida pelo Desktop Analytics é 10010586 (10.0.10586).

Caso contrário, poderá apresentar um dos seguintes erros:

- O componente Connected User Experience and Telemettry (diagtrack.dll) está desatualizado. Verificar os requisitos  

    > [!TIP]
    > Há um problema conhecido com a atualização de segurança estendida de abril de 2020 (ESU) para o Windows 7 que faz com que os dispositivos reportem mal este erro. Para mais informações, consulte notas de [lançamento](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- Não é possível encontrar o componente De Experiência e Telemetria Conectada (diagtrack.dll). Verificar os requisitos  

- Ativar e iniciar o serviço Connected User Experiences and Telemettry para enviar dados para a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale as últimas atualizações. Para mais informações, consulte [as atualizações do Dispositivo](enroll-devices.md#update-devices).

Certifique-se de que o serviço connected **user experiences and Telemettry** no dispositivo está em funcionamento.

### <a name="diagtrack-version"></a>Versão DiagTrack

Esta propriedade exibe a versão atual do componente De experiência e telemetria do utilizador conectado no dispositivo. Mostra a versão do ficheiro, `%windir%\System32\diagtrack.dll` sem os pontos decimais. Por exemplo, a versão de ficheiro 10.0.10586 exibe como 10010586.

### <a name="sqm-id-retrieval"></a>Recuperação de ID SQM

<!--38-->
Esta propriedade é principalmente para dispositivos Windows 7. Pode ser usado por versões posteriores do SO como um identificador de recuo para o dispositivo.

Se não for bem sucedido, pode apresentar o seguinte erro:

- Não é possível recuperar o identificador de telemetria do dispositivo legado (SQM ID)

Para mais informações, reveja o registo m365AHandler no cliente.  

Certifique-se de não ter identificações duplicadas no seu ambiente. Por exemplo, se os dispositivos fossem implantados com uma imagem de Os que não fosse generalizada.

### <a name="unique-device-identifier-retrieval"></a>Recuperação de identificador de dispositivo único

<!--54-->
O Desktop Analytics utiliza o serviço Microsoft Account para uma identidade de dispositivo mais fiável.

Certifique-se de que o serviço de **assistente de sessão** de conta da Microsoft não está desativado. O tipo de arranque deve ser **Manual (Trigger Start)**.

Para desativar o acesso à conta da Microsoft no utilizador final, utilize as definições de política em vez de bloquear este ponto final. Para mais informações, consulte [a conta da Microsoft na empresa.](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)

### <a name="windows-diagnostic-data-opt-in"></a>Opt-in de dados de diagnóstico do Windows

<!--8,40,55,62-->
Esta propriedade verifica se o Windows está devidamente configurado para permitir dados de diagnóstico. Verifica o valor da AllowTelemetria nas seguintes teclas de registo:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Verifique as permissões nestas chaves do registo. Certifique-se de que a conta do Sistema local pode aceder a estas chaves para o cliente do Gestor de Configuração definir. Também pode ser causado por um objeto político de grupo conflituoso. Para mais informações, consulte [as definições do Windows](enroll-devices.md#windows-settings).  

Para mais informações, reveja o registo m365AHandler no cliente.  

## <a name="see-also"></a>Consulte também

[Resolver problemas da Análise de Computadores](troubleshooting.md)
