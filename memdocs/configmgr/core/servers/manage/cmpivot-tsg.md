---
title: CCMPivot de resolução de problemas
titleSuffix: Configuration Manager
description: Aprenda a resolver problemas com a CMPivot no Gestor de Configuração.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69178f9ac1c1acb1ee2a2931c88a55a0784435b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723510"
---
# <a name="troubleshoot-cmpivot"></a>CCMPivot de resolução de problemas

A CMPivot é uma ferramenta que proporciona acesso a um estado real dos dispositivos no seu ambiente. A CMPivot executa uma consulta em todos os dispositivos atualmente conectados na recolha do alvo e devolve os resultados.

Ocasionalmente, talvez precise sacar problemas à CMPivot. Por exemplo, se uma mensagem de estado de um cliente para CMPivot for corrompida, o servidor do site não pode processar a mensagem. Este artigo ajuda-o a compreender o fluxo de informação para a CMPivot.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a>Troubleshoot CMPivot na versão 1902 e mais tarde

Nas versões de Configuração 1902 e posteriormente, pode executar a CMPivot a partir do site da administração central (CAS) numa hierarquia. O site principal ainda trata da comunicação ao cliente.

Quando executa o CMPivot a partir do CAS, utiliza o canal de subscrição de mensagens de alta velocidade para comunicar com o site principal. A CMPivot não utiliza a replicação Padrão SQL entre os sites. Se a sua instância de Servidor SQL ou o seu fornecedor SQL estiver em controlo remoto, ou se utilizar o SQL Server Always On, terá um "cenário de duplo salto" para a CMPivot. Para obter informações sobre como definir a delegação restrita para um "cenário de duplo salto", consulte a [CMPivot a partir da versão 1902](cmpivot.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> Ao resolver problemas a CMPivot, ative o registo verbose nos seus pontos de gestão (MPs) e no SMS_MESSAGE_PROCESSING_ENGINE do servidor do site para obter mais informações. Além disso, se a saída do cliente for superior a 80 KB, ative o registo verbose no MP e no componente SMS_STATE_SYSTEM do servidor do site. Para obter informações sobre como ativar o registo verbose, consulte [as opções](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)de registo do servidor do Site .

### <a name="get-information-from-the-site-server"></a>Obtenha informações do servidor do site

Por predefinição, os ficheiros `C:\Program Files\Microsoft Configuration Manager\logs`de registo do servidor do site estão localizados em . Esta localização pode ser diferente se tiver especificado um diretório de instalação não predefinido ou itens descarregados como o Fornecedor SMS para outro servidor. Se executar cmpivot a partir do CAS, os registos estão no servidor do site principal.

`smsprov.log` Procure estas linhas:

- Versão do Gestor de Configuração 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Versão do Gestor de Configuração 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14`é o Script-Guid para cmPivot. Pode também ver este GUID nas mensagens de estado de [auditoria da CMPivot.](cmpivot.md#cmpivot-audit-status-messages)

Em seguida, encontre a identificação na janela cmpivot. Esta identificação `ClientOperationID`é a.

![Janela CMPivot com ClientOperationID em destaque](media/cmpivot-client-operationid-1902.png)

Encontre `TaskID` o da tabela ClientAction. O `TaskID` corresponde à `UniqueID` tabela ClienteAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

Em, `BgbServer.log`procure `TaskID` o recolhido da SQL `PushID`e note o . O `TaskID` está `TaskGUID`rotulado. Por exemplo:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Registos de clientes

Depois de ter a informação do servidor do site, verifique os registos do cliente. Por predefinição, os registos do cliente estão localizados em `C:\Windows\CCM\Logs`.

Em, `CcmNotificationAgent.log`procure entradas de log que se pareçam com as seguintes linhas:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

Verifique `Scripts.log` se `TaskID`o . No exemplo seguinte, `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`vê-se:  

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Se não vir "(rápido)" no `Scripts.log`, então os dados são provavelmente superiores a 80 KB. Neste caso, a informação é enviada para o servidor do site como mensagem de estado. Use o `StateMessage.log` do cliente e `Statesys.log`do servidor do site.

### <a name="review-messages-on-the-site-server"></a>Rever mensagens no servidor do site

Quando a [exploração madeireira verbosa](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) está ativada no ponto de gestão, pode ver como as mensagens de cliente são tratadas. Dentro, `MP_RelayMsgMgr.log`procure `TaskID`o.

No `MP_RelayMsgMgr.log` exemplo, pode ver a identificação `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`do cliente e o . Um ID de mensagem é atribuído à resposta do cliente antes de ser enviado para o motor de processamento de mensagens:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Quando a [exploração madeireira verbosa](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) está `SMS_MESSAGE_PROCESSING_ENGINE.log`ativada, os resultados do cliente são processados. Use o ID da `MP_RelayMsgMgr.log`mensagem que encontrou a partir do . As entradas de registo de processamento são semelhantes ao seguinte exemplo:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Se obtém uma exceção durante o processamento, pode revê-la executando a seguinte consulta SQL e olhando para a coluna Exception. Depois de a mensagem ser processada, deixará `MPE_RequestMessages_Instant` de estar na mesa.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

Em, `BgbServer.log`procure `PushID` o número de clientes que reportaram ou falharam.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Verifique a vista de monitorização da CMPivot `TaskID`a partir da SQL utilizando o .

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[![CmPivot SQL consultas para resolução de problemas na versão 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a>Troubleshoot CMPivot em 1810 e mais cedo

Nas versões 1810 e anteriores do Gestor de Configuração, o servidor do site trata da comunicação ao cliente.

### <a name="get-information-from-the-site-server"></a>Obtenha informações do servidor do site

Por predefinição, os ficheiros `C:\Program Files\Microsoft Configuration Manager\logs`de registo do servidor do site estão localizados em . Esta localização pode ser diferente se tiver especificado um diretório de instalação não predefinido ou itens descarregados como o Fornecedor SMS para outro servidor.

`smsprov.log` Procure esta linha:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Encontre a identificação na janela cmpivot. Esta identificação `ClientOperationID`é a.

![Janela CMPivot com ClientOperationID em destaque](media/cmpivot-clientoperationid.png)

Encontre `TaskID` o da tabela ClientAction. O `TaskID` corresponde à `UniqueID` tabela ClienteAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

Dentro, `BgbServer.log`procure `TaskID` o que reuniu da SQL. Está rotulado. `TaskGUID` Por exemplo:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Registos de clientes

Depois de ter a informação do servidor do site, verifique os registos do cliente. Por predefinição, os registos do cliente estão localizados em `C:\Windows\CCM\Logs`.

Em, `CcmNotificationAgent.log`procure registos semelhantes à seguinte entrada:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

Procure `Scripts.log` o. `TaskID` No exemplo seguinte, `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`vemos:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Olhe `StateMessage.log`para dentro. No exemplo seguinte, vê-se que `TaskID` está perto `<Param>`do fundo da mensagem ao lado de:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Rever mensagens no servidor do site

Aberto `statesys.log` para ver se a mensagem é recebida e processada. No exemplo seguinte, `TaskID` vê-se perto do `<Param>`fundo da mensagem ao lado de . Ative o [registo verboso](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) no componente SMS_STATE_SYSTEM para ver estas entradas de registo.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Se a mensagem não tiver sido processada, verifique a caixa de entrada da mensagem do estado. A localização da `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`caixa de entrada por defeito é . Procure os ficheiros nestes locais:

- Dados
- Corrompido
- Processo

Verifique a vista de monitorização da CMPivot a partir do SQL utilizando o `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Para clientes que estão a usar a versão 1810 ou superior, as mensagens estatais não são usadas a menos que a saída seja superior a 80 KB. Ao resolver problemas com a CMPivot nestes casos, pode obter mais informações quando permite o registo verbose nos seus MPs e no SMS_MESSAGE_PROCESSING_ENGINE do servidor do site. Para obter informações sobre como ativar o registo verbose, consulte [as opções](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)de registo do servidor do Site .
>
> Para resolução de problemas, consulte os seguintes registos:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Passos seguintes

- [Usando cmpivot](cmpivot.md)
- [Criar e executar scripts do PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
