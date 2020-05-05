---
title: Ação do dispositivo de resolução de problemas
titleSuffix: Configuration Manager
description: Dispositivo de resolução de problemas faz referência técnica para Gestor de Configuração
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717595"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Ações de dispositivos de resolução de problemas para dispositivos de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A partir do Configuration Manager 2002, os clientes do Gestor de Configuração podem ser sincronizados com o centro de administração do Microsoft Endpoint Manager. Algumas ações de clientes podem ser executadas a partir do centro de administração do Microsoft Endpoint Manager sobre os clientes sincronizados.

As ações disponíveis são:
- Política de Máquina sincronizada
- Política de Utilizador sincronizado
- Ciclo de Avaliação de Aplicações


[![Visão geral do dispositivo no centro de administração do Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Quando um administrador executa uma ação do centro de administração do Microsoft Endpoint Manager, o pedido de notificação é encaminhado para o site do Gestor de Configuração e do site para o cliente.

## <a name="configuration-manager-components"></a>Componentes do Gestor de Configuração

- **SMS_SERVICE_CONNECTOR**: Utiliza o Gateway Notification Worker para o processamento da notificação do centro de administração do Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: Recebe a notificação e cria uma notificação do cliente.
- **BgbAgent**: O cliente recebe a tarefa e executa a ação solicitada.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Quando uma ação é iniciada a partir do centro de administração do Microsoft Endpoint Manager, **o CMGatewayNotificationWorker.log** processa o pedido.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Uma notificação é recebida do centro de administração do Microsoft Endpoint Manager.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. As ações do utilizador e do dispositivo são validadas.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. A tarefa remota é reencaminhada para o SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Uma vez que a mensagem é enviada para o SMS_NOTIFICATION_SERVER, uma tarefa é enviada do ponto de gestão para o cliente correspondente. Verá o abaixo no **BgbServer.log**, que está no ponto de gestão:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

O último passo ocorre no cliente e pode ser visto no **ccmNotificationAgent.log**. Uma vez recebida a tarefa, solicitará ao programador a realização da ação. Quando a ação for executada, verá uma mensagem de confirmação:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Problemas comuns

Se o administrador não tiver as permissões necessárias no Gestor `Unauthorized` de Configuração, verá uma resposta no **cmGatewayNotificationWorker.log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Certifique-se de que o utilizador que executa a ação a partir do centro de administração do Microsoft Endpoint Manager tem as permissões necessárias no site do Gestor de Configuração. Para mais informações, consulte o inquilino do [Microsoft Endpoint Manager anexar pré-requisitos.](device-sync-actions.md#prerequisites)

## <a name="next-steps"></a>Passos seguintes

[Permitir a cogestão](../comanage/overview.md) para obter capacidades adicionais alimentadas por nuvem, como acesso condicional.
