---
title: Acerca dos ficheiros de registo
titleSuffix: Configuration Manager
description: Utilize ficheiros de registo para resolver problemas com clientes do Gestor de Configuração e sistemas de site.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6be23adc7ac082545bffeef59ed52d3455d9931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720304"
---
# <a name="about-log-files-in-configuration-manager"></a>Sobre ficheiros de registo no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

No Gestor de Configuração, os componentes do cliente e do servidor do site registam informações sobre o processo em ficheiros de registo individuais. Pode utilizar a informação nestes ficheiros de registo para o ajudar a resolver problemas que possam ocorrer. Por predefinição, o Gestor de Configuração permite o registo de componentes de clientes e servidores.

Este artigo fornece informações gerais sobre os ficheiros de registo do Gestor de Configuração. Inclui ferramentas para usar, como configurar os registos e onde encontrá-los. Para obter mais informações sobre ficheiros de registo específicos, consulte a referência dos [ficheiros De registo](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a>Como funciona

A maioria dos processos no Gestor de Configuração escrevem informações operacionais para um ficheiro de registo que é dedicado a esse processo. Os ficheiros de registo são identificados por extensões de **ficheiros .log** ou **.lo_.** O Gestor de Configuração escreve para um ficheiro .log até que o registo atinja o seu tamanho máximo. Quando o registo está cheio, o ficheiro .log é copiado para um ficheiro com o mesmo nome, mas com a extensão .lo_, e o processo ou componente continua a escrever para o ficheiro .log. Quando o ficheiro .log volta a atingir o seu tamanho máximo, o ficheiro .lo_ é substituído e o processo repete-se. Alguns componentes estabelecem um histórico de ficheiros de registo, através da adesão de uma data e carimbo de hora ao nome do ficheiro de registo e mantendo a extensão .log.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a>Ferramentas de visualização de log

Todos os ficheiros de registo do Gestor de Configuração são texto simples, para que possa vê-los com qualquer leitor de texto como o Notepad. Os registos usam formatação única que é melhor vista com uma das seguintes ferramentas especializadas:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Espectador de registo do Centro de Suporte](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Para visualizar os registos, utilize a ferramenta de visualização de registo do Gestor de Configuração **CMTrace**. Está localizado na `\SMSSetup\Tools` pasta do diretor de configuração. A ferramenta CMTrace é adicionada a todas as imagens de arranque que são adicionadas à Biblioteca de Software. A ferramenta de visualização de log CMTrace é instalada automaticamente juntamente com o cliente do Gestor de Configuração.<!--1357971--> Para mais informações, consulte [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

A partir da versão 1906, o **OneTrace** é um novo espectador de log com Support Center. Funciona da mesma forma com a CMTrace, com melhorias. Para mais informações, consulte [o Suporte Center OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Espectador de registo do Centro de Suporte

**O Centro** de Suporte inclui um espectador de registo moderno. Esta ferramenta substitui o CMTrace e fornece uma interface personalizável com suporte para separadores e janelas dockable. Tem uma camada de apresentação rápida e pode carregar ficheiros de registo grandes em segundos. Para mais informações, consulte a referência do Observador de [Registodo do Centro](../../support/support-center-ui-reference.md#bkmk_log-viewer)de Suporte .

> [!Note]  
> O Centro de Suporte e o OneTrace utilizam a Windows Presentation Foundation (WPF). Este componente não está disponível no Windows PE. Continue a utilizar o CMTrace em imagens de arranque com implementações de sequência de tarefas.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a>Configurar opções de exploração madeireira

Pode alterar a configuração dos ficheiros de registo, tais como o nível verboso, tamanho e histórico. Existem várias formas de alterar estas definições:

- [Durante a instalação do cliente](#bkmk_logoptions-clientprop)
- [Usando o Gestor de Serviço de Gestor de Configuração](#bkmk_logoptions-sm)
- [Utilização do Registo windows](#bkmk_logoptions-registry)
- [Na consola de Gestor de Configuração](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a>Configure as opções de exploração madeireira durante a instalação do cliente

Pode definir a configuração dos ficheiros de registo do cliente durante a instalação. Utilize as seguintes propriedades:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Para mais informações, consulte as propriedades de [instalação do Cliente.](../../clients/deploy/about-client-installation-properties.md#clientMsiProps)

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a>Configure as opções de registo utilizando o Gestor de Serviço de Gerente de Configuração

Pode alterar onde o Gestor de Configuração armazena os ficheiros de registo e o seu tamanho.  

Para modificar o tamanho dos ficheiros de registo, altere o nome e a localização do ficheiro de registo, ou para forçar vários componentes a escrever num único ficheiro de registo, faça os seguintes passos:  

#### <a name="modify-logging-for-a-component"></a>Modificar a exploração madeireira para um componente  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o **Estado do Sistema**e, em seguida, selecione o nó de Estado do **Site** ou do Estado **do Componente.**  

2. Na fita, selecione **Iniciar**, e, em seguida, selecione Gestor de Serviço de Gestor de **Configuração**.  

3. Quando o Gestor de Serviços de Configuração abrir, ligue-se ao site que pretende gerir. Se o site que pretende gerir não for mostrado, selecione **Site**, selecione **Connect**e introduza o nome do servidor do site para o site correto.  

4. Expandir o site e ir para **Componentes** ou **Servidores,** dependendo de onde estão localizados os componentes que pretende gerir.  

5. No painel direito, selecione um ou mais componentes.  

6. No menu **Componente,** **selecione Logging**.  

7. Na caixa de diálogo **Registo de Componente do Configuration Manager**, preencha as opções de configuração disponíveis para a sua seleção.  

8. Selecione **OK** para salvar a configuração.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a>Configure as opções de exploração madeireira utilizando o Registo do Windows

<!-- SCCMDocs#992 -->
Utilize o Registo do Windows nos servidores ou clientes para alterar as seguintes opções de registo:

- Nível verboso
- História máxima
- Tamanho máximo

Ao resolver um problema, pode permitir que o registo verbose para o Gestor de Configuração escreva detalhes adicionais nos ficheiros de registo.

> [!Warning]
> A configuração errada destas definições pode fazer com que o Gestor de Configuração registe grandes quantidades de informação, ou nenhuma. Embora estes dados possam ser benéficos para a resolução de problemas, tenha cuidado ao alterar estes valores em locais de produção. Teste sempre estas mudanças num ambiente de laboratório primeiro. Pode ocorrer uma exploração madeireira excessiva, o que pode dificultar a descoberta de informações relevantes nos ficheiros de registo.

Depois de efazer alterações nestas definições de registo, reinicie o componente:

- Se alterar as definições do cliente, reinicie o serviço de hospedar o **Agente SMS** (CcmExec).
- Se alterar as definições do servidor, reinicie o serviço **SMS Executive.**

As definições de registo variam consoante o componente:

- [Ponto de cliente e gestão](#bkmk_reg-client)
- [Servidor do site](#bkmk_reg-site)
- [Função do sistema de sites](#bkmk_reg-role)
- [Consola do Configuration Manager](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a>Opções de registo de pontos de cliente e gestão

Para configurar opções de registo de todos os componentes num sistema de site de pontos de cliente ou de ponto de gestão, configure estes **valores REG_DWORD** sob a seguinte chave de Registo do Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Nome  |Valores  |Descrição  |
|---------|---------|---------|
|Nível de Registo|`0`: Verbose<br>`1`: Padrão<br>`2`: Advertências e erros<br>`3`: Erros apenas|O nível de detalhe para escrever para registar ficheiros.|
|LogMaxHistory|Qualquer inteiro maior ou igual a zero, por exemplo:<br>`0`: Sem história<br>`1`: Padrão|Quando um ficheiro de registo atinge o tamanho máximo, o cliente renomea-o como uma cópia de segurança e cria um novo ficheiro de registo. Especifique quantas versões anteriores manter.|
|LogMaxSize|Qualquer inteiro maior ou igual a 10.000, por exemplo:<br>250000|O tamanho máximo do ficheiro de registo em bytes. Quando um registo cresce para o tamanho especificado, o cliente renomea-o como um ficheiro de histórico, e cria um novo ficheiro. O valor padrão é de 250.000 bytes.|

> [!Note]  
> Não altere outros valores que possam existir nesta chave de registo.

Para depuração avançada, também pode adicionar este **valor REG_SZ** sob a seguinte tecla de Registo do Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Nome  |Valores  |Descrição  |
|---------|---------|---------|
|Ativado | `True`: ativar registos de depuração<br>`False`: desativar os registos de depuração |Permite a desflorestação de depuração para fins de resolução de problemas.|

Esta definição faz com que o cliente faça com que o cliente sintetetiza informações de baixo nível para resolução de problemas. Evite utilizar esta definição em locais de produção. Pode ocorrer uma exploração madeireira excessiva, o que pode dificultar a descoberta de informações relevantes nos ficheiros de registo. Certifique-se de desligar esta definição depois de resolver o problema.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a>Opções de registo do servidor do site

Pode configurar as definições globalmente ou para um componente específico no servidor do site do Gestor de Configuração.

Configure estes valores sob a seguinte tecla de Registo do Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Nome  |Valores  |Tipo  |Descrição
|---------|---------|---------|---------|
|SqlEnabled| `1`: ativar rastreio SQL<br> `0`: desativar o rastreio SQL |REG_DWORD|Adicione o registo de rastreio SQL em todos os registos do servidor do site.|
|Arquivado| `1`: ativar arquivos de registo<br> `0`: desativar os arquivos de registo | REG_DWORD |Arquivar registos de servidores do site para um local separado para preservação histórica.|
|ArquivoCaminho| Um caminho de pasta válido, por exemplo`C:\Logs\Archive` | REG_SZ |O caminho para arquivar registos de servidores do site.|

Apenas permita rastreio sQL para fins de resolução de problemas. Evite usá-lo em locais de produção. Pode ocorrer uma exploração madeireira excessiva, o que pode dificultar a descoberta de informações relevantes nos ficheiros de registo. Certifique-se de desligar esta definição depois de resolver o problema.

> [!Note]  
> Não altere outros valores que possam existir nesta chave de registo.

Para configurar as opções de registo de um componente específico do servidor, configure estes valores **REG_DWORD** sob a seguinte tecla de Registo do Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Nome  |Valores  |Descrição  |
|---------|---------|---------|
|Nível de exploração|`0`: Verbose<br>`1`: Padrão<br>`2`: Advertências e erros<br>`3`: Erros apenas|O nível de detalhe para escrever para registar ficheiros.|
|LogMaxHistory|Qualquer inteiro maior ou igual a zero, por exemplo:<br>`0`: Sem história<br>`1`: Padrão|Quando um ficheiro de registo atinge o tamanho máximo, o servidor renomea-o como uma cópia de segurança e cria um novo ficheiro de registo. Especifique quantas versões anteriores manter.|
|MaxFileSize|Qualquer inteiro maior ou igual a 10.000, por exemplo:<br>250000|O tamanho máximo do ficheiro de registo em bytes. Quando um registo cresce para o tamanho especificado, o cliente renomea-o como um ficheiro de histórico, e cria um novo ficheiro. O valor padrão é de 250.000 bytes.|
|Depuração| `1`: ativar registos de depuração<br>`0`: desativar os registos de depuração |Permite a desflorestação de depuração para fins de resolução de problemas.|

A definição DebugLogging faz com que o servidor sintetiza informações de baixo nível para resolução de problemas. Evite utilizar esta definição em locais de produção. Pode ocorrer uma exploração madeireira excessiva, o que pode dificultar a descoberta de informações relevantes nos ficheiros de registo. Certifique-se de desligar esta definição depois de resolver o problema.

> [!Note]  
> Não altere outros valores que possam existir nesta chave de registo.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a>Opções de registo de funções do sistema do site

Pode configurar as definições globalmente ou para um componente específico num sistema de site que acolhe uma função de servidor do Gestor de Configuração.

Para configurar as opções de registo de um componente específico do servidor, configure estes valores **REG_DWORD** sob a seguinte tecla de Registo do Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Por exemplo, para o papel do ponto de distribuição:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Nome  |Valores  |Descrição  |
|---------|---------|---------|
|Nível de Registo|`0`: Verbose<br>`1`: Padrão<br>`2`: Advertências e erros<br>`3`: Erros apenas|O nível de detalhe para escrever para registar ficheiros.|
|LogMaxHistory|Qualquer inteiro maior ou igual a zero, por exemplo:<br>`0`: Sem história<br>`1`: Padrão|Quando um ficheiro de registo atinge o tamanho máximo, o servidor renomea-o como uma cópia de segurança e cria um novo ficheiro de registo. Especifique quantas versões anteriores manter.|
|LogMaxSize|Qualquer inteiro maior ou igual a 10.000, por exemplo:<br>250000|O tamanho máximo do ficheiro de registo em bytes. Quando um registo cresce para o tamanho especificado, o servidor renomea-o como um ficheiro de histórico e cria um novo ficheiro. O valor padrão é de 250.000 bytes.|

> [!Note]  
> Não altere outros valores que possam existir nesta chave de registo.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a>Opções de loglogging de consola do Gestor de Configuração

Para alterar o nível verboso do registo AdminUI.log para a consola 'Gestor de Configuração', utilize o seguinte procedimento:

1. Abra o ficheiro de configuração da consola, **Microsoft.ConfigurationManagement.exe.config,** num editor XML como o Notepad. O ficheiro de configuração predefinido encontra-se no seguinte local:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. Sob o sistema.elemento fonte de**source** **fonte** > de >  **diagnóstico,** altere o atributo **switchValue** de `Error` . `Verbose` Por exemplo:

    Original: `<source name="SmsAdminUISnapIn" switchValue="Error">` Novo:`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Guarde o ficheiro e reinicie a consola.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a>Configure as opções de registo na consola do Gestor de Configuração

<!-- 4433455 -->

A partir da versão 1910, ative ou desative o registo verbose num cliente ou coleção a partir da consola:

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance,** selecione o nó de **Dispositivos** e escolha um dispositivo-alvo.

1. Na fita, no separador **Home,** no grupo **Dispositivo,** selecione **Diagnósticos do Cliente**. Escolha uma das ações disponíveis.

Para mais informações, consulte [diagnósticos do Cliente.](../../clients/manage/client-notification.md#client-diagnostics)

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a>Localização de ficheiros de registo

Configuração Manager e componentes dependentes armazenam ficheiros de registo em vários locais. Estas localizações dependem do processo que cria o ficheiro de registo e a configuração do seu ambiente.

Os seguintes locais são os incumprimentos. Se personalizar os diretórios de instalação no seu ambiente, os caminhos reais podem variar.

- Cliente:`C:\Windows\CCM\logs`
- Servidor:`C:\Program Files\Microsoft Configuration Manager\Logs`
- Ponto de gestão:`C:\SMS_CCM\Logs`
- Consola de Gestor de Configuração:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- IIS:`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Localizações de registo de sequência de tarefas

A localização do ficheiro de registo de sequência de tarefas **smsts.log** varia consoante a fase da sequência de tarefas:

- No Windows PE antes do `X:\Windows\temp\smstslog\smsts.log` passo do disco de [formato e partição:](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) (X é a unidade RAM do Windows PE)
- No Windows PE após o `X:\smstslog\smsts.log`passo do disco `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` de **formato e partição:**
- No novo Sistema Operativo Windows antes da instalação do cliente:`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- No Windows após a instalação do cliente:`C:\Windows\CCM\Logs\smstslog\smsts.log`
- No Windows após a conclusão da sequência de tarefas:`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> A variável de sequência de tarefas apenas de leitura [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) sempre contém o caminho do ficheiro de registo atual.


## <a name="see-also"></a>Consulte também

- [Referência de ficheiros de registo](log-files.md)

- [Centro de Suporte OneTrace](../../support/support-center-onetrace.md)

- [Espectador de ficheiro sonorde do Centro de Suporte](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
