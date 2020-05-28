---
title: Resolução de Problemas do Gestor de Conversão de Pacotes
titleSuffix: Configuration Manager
description: Aprenda a resolver problemas com o Gestor de Conversão de Pacotes no Gestor de Configuração.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877629"
---
# <a name="troubleshoot-package-conversion-manager"></a>Resolução de Problemas do Gestor de Conversão de Pacotes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

Utilize as informações deste artigo para ajudá-lo a resolver problemas ao utilizar o Gestor de Conversão de Pacotes.



## <a name="sms-provider"></a>Fornecedor de SMS

O Gestor de Conversão de Pacotes utiliza o Fornecedor SMS. Para mais informações, consulte [Plan for the SMS Provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

Se o Fornecedor SMS não estiver a funcionar corretamente, a consola do Gestor de Configuração, incluindo o Gestor de Conversão de Pacotes, não funciona.



## <a name="package-readiness"></a>Prontidão do pacote

Antes de converter um pacote para uma aplicação, analise o pacote utilizando a função **De** Análise do Gestor de Conversão de Pacotes. Após a análise, adicione a coluna **de prontidão** no nó de **Pacotes** da consola 'Gestor de Configuração'. A lista de pacotes apresenta um dos seguintes estados de prontidão do pacote analisado:

- **Automática**: A embalagem pode ser diretamente convertida utilizando a função **Converte.**      

  > [!NOTE]  
  > Uma conversão automática não converte consultas WQL em requisitos de aplicação. Utilize o processo **Desvendae converter** para converter estas consultas.  

- **Manual**: A embalagem necessita de algumas adições ou alterações antes de a converter utilizando a função **Fix and Converte.**  

- **Não Aplicável**: O pacote não é adequado para conversão. Ou corrija quaisquer problemas com a embalagem ou continue a implantá-lo como um pacote.  

- **Erro**: O pacote contém erros. Corrija manualmente estes erros antes de poder analisá-los e convertê-los.  

Os detalhes do nó dos **Pacotes** na consola do Gestor de Configuração mostram quaisquer problemas de prontidão. Selecione um pacote e, em seguida, selecione o separador **Resumo** no painel de detalhes.



## <a name="log-files"></a>Ficheiros de registo

### <a name="enable-logging"></a>Ativar registo

Ao ativar o loglogging para O Gestor de Conversão de Pacotes, regista todas as suas ações, exceções e erros.

Para ativar o registo deste componente no Gestor de Configuração, modifique o **Microsoft.ConfigurationManagement.exe.Config**. Por predefinição, este ficheiro de configuração encontra-se no seguinte caminho:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> A partir da versão 1910, este caminho mudou para utilizar a `Microsoft Endpoint Manager` pasta. Certifique-se de que não utiliza uma versão mais antiga do ficheiro que possa existir noutra pasta.

Insira os **seguintes interruptores** e **trace** elementos XML no elemento **de diagnóstico do sistema** após o elemento de última **fonte:**

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Esta amostra utiliza o ficheiro **PCMTrace.log**. Este registo está no computador que executa a consola 'Gestor de Configuração' no seguinte caminho:  
`%UserProfile%\AppData\Local\Temp`

Para configurar o nível de detalhe, altere a definição do interruptor de rastreio **pcmLogging.** Desfixaeste valor para quatro níveis de detalhe, desde menos detalhados ( `1` ) até mais detalhados ( `4` ).


### <a name="smsprovlog"></a>SMSProv.log

Em algumas situações, a informação relevante para resolver problemas o processo de conversão do pacote está no ficheiro **SMSProv.log.** Este ficheiro captura informações do Fornecedor SMS do Gestor de Configuração.

Por predefinição, este ficheiro de registo está localizado no servidor do site do Gestor de Configuração no seguinte caminho:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Se vir uma das seguintes mensagens de erro, o ficheiro **SMSProv.log** pode conter informações relevantes sobre resolução de problemas:

- `The SMS Provider reported an error`

- `Generic Failure`

Estas mensagens de erro normalmente indicam que ocorreu um erro no servidor do site e que a informação de erro não foi enviada para a consola do Gestor de Configuração.

Para mais informações, consulte [referência técnica para mensagens de erro do Gestor de Conversão](error-messages.md)de Pacotes .



## <a name="changing-package-attributes-after-analysis"></a>Alteração de atributos de pacote após análise

Depois de analisar um pacote e tiver um estado de prontidão de **Automático** ou **Manual,** o processo de conversão poderá falhar se alterar algum dos atributos relevantes.

Por exemplo, analisa-se um pacote e o seu estado de prontidão é **Automático**. Em seguida, adicione outro programa ao pacote. A conversão do pacote pode falhar.

Se precisar de fazer alterações num pacote após análise, refaça a análise antes da conversão. 



## <a name="see-also"></a>Consulte também

[Referência técnica para mensagens de erro do Gestor de Conversão de Pacotes](error-messages.md)
