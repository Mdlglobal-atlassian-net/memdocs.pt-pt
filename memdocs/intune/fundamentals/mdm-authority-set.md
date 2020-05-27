---
title: Definir a autoridade de gestão de dispositivos móveis
titleSuffix: Microsoft Intune
description: Definir a autoridade de gestão de dispositivos móveis no Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7244872fa888aaee164187e62a2355a94f793499
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985176"
---
# <a name="set-the-mobile-device-management-authority"></a>Definir a autoridade de gestão de dispositivos móveis

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A definição da autoridade de gestão de dispositivos móveis (MDM) determina como gere os seus dispositivos. Como administrador de TI, tem de definir uma autoridade de MDM antes de os utilizadores poderem inscrever dispositivos para gestão.

As configurações possíveis são:

- **Intune Autónomo** – gestão apenas na cloud, que configura através do portal do Azure. Inclui o conjunto completo das funcionalidades que o Intune oferece. [Defina a autoridade de MDM na consola do Intune](#set-mdm-authority-to-intune).

- **Intune co-management** - integração da solução de nuvem Intune com O Gestor de Configuração para dispositivos Windows 10. Configura o Intune com a consola do Configuration Manager. [Configure a inscrição automática dos dispositivos para Intune](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Gestão de Dispositivos Móveis para o Office 365** – integração do Office 365 com a solução cloud do Intune. Deve configurar o Intune no centro de administração do Microsoft 365. Inclui um subconjunto das funcionalidades que estão disponíveis com o Intune Autónomo. Consulte a Configuração da [Gestão de Dispositivos Móveis (MDM) no Office 365](https://support.office.com/en-us/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd)

- **Escritório 365 MDM Coexistência** Pode ativar e utilizar simultaneamente o MDM para o Office e o Intune em simultâneo com o seu inquilino e definir a autoridade de gestão para intune ou MDM para que cada utilizador dite qual o serviço que será utilizado para gerir os seus dispositivos matriculados no MDM. A autoridade de gestão de cada utilizador é definida com base na licença atribuída ao utilizador: Se o utilizador tiver apenas uma licença para o Microsoft 365 Basic ou Standard, os seus dispositivos serão geridos pelo MDM para o Office. Se o utilizador tiver uma licença que cintuse intune, os seus dispositivos serão geridos pela Intune. Se adicionar uma licença que cativa o Intune a um utilizador anteriormente gerido pelo MDM para o Office, os seus dispositivos serão transferidos para a gestão intune. Certifique-se de que as configurações Intune são atribuídas aos utilizadores para substituir o MDM no Office antes de mudar os utilizadores para Intune, caso contrário os seus dispositivos perderão MDM para a configuração do Office e não receberão qualquer substituição do Intune.

## <a name="set-mdm-authority-to-intune"></a>Definir a autoridade de MDM como o Intune

Se ainda não configurou a autoridade de MDM, siga os passos abaixo.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione o banner laranja para abrir a definição da Autoridade de Gestão de **Dispositivos Móveis.** A faixa cor de laranja só é apresentada se ainda não tiver configurado a autoridade de MDM.
2. Em **Autoridade de Gestão de Dispositivos Móveis**, selecione a sua autoridade de MDM a partir das seguintes opções:
   - **Autoridade de MDM do Intune**
   - **Nenhum**

   ![Captura de ecrã do ecrã Definir a autoridade de gestão de dispositivos móveis do Intune](./media/mdm-authority-set/set-mdm-auth.png)

   Uma mensagem indica que definiu com êxito a autoridade de MDM como o Intune.

### <a name="workflow-of-intune-administration-ui"></a>Fluxo de trabalho da IU de Administração do Intune
Quando a gestão de dispositivos Android ou Apple está ativada, o Intune envia informações sobre o dispositivo e o utilizador para se integrar com estes serviços de terceiros e gerir os respetivos dispositivos.

Os cenários que acrescentam uma janela de consentimento para partilhar dados são incluídos quando:
- Ativa os perfis de trabalho do Android.
- Ativar e carregar certificados Push de MDM da Apple.
- Ativar qualquer um dos serviços da Apple, tal como o Programa de Registo de Aparelho, o School Manager e o Programa de Compras em Volume.

Em cada caso, o consentimento está estritamente relacionado com a execução de um serviço de gestão de dispositivos móveis. Por exemplo, confirmar que um administrador de TI autorizou a inscrição de dispositivos Google ou Apple. A documentação que aborda as informações que serão partilhadas quando o novo fluxo de trabalho for disponibilizado está disponível nas seguintes localizações:
- [Dados que o Intune envia para a Google](https://aka.ms/Data-intune-sends-to-google)
- [Dados que o Intune envia para a Apple](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Considerações-chave
Depois de mudar para a nova autoridade de MDM, provavelmente haverá um tempo de transição (até oito horas) até que o dispositivo faça o registo e sincronize com o serviço. É necessário configurar as definições na nova autoridade do MDM para garantir que os dispositivos matriculados continuarão a ser geridos e protegidos após a alteração. 
- Depois da alteração, os dispositivos têm de se ligar ao serviço para que as definições da nova autoridade de MDM (Intune autónomo) substituam as definições existentes no dispositivo.
- Depois de alterar a autoridade do MDM, algumas das definições básicas (tais como perfis) da autoridade anterior do MDM permanecerão no dispositivo por um período máximo de sete dias ou até que o dispositivo se ligue ao serviço pela primeira vez. Recomenda-se que configure aplicações e configurações (políticas, perfis, apps, etc.) na nova autoridade do MDM o mais rapidamente possível e implemente a definição para os grupos de utilizadores que contenham utilizadores que tenham dispositivos inscritos existentes. Assim que um dispositivo se ligar ao serviço após a alteração da autoridade de MDM, irá receber as novas definições da nova autoridade de MDM e impedir lacunas na gestão e proteção.
- Os dispositivos que não tenham utilizadores associados (normalmente quando tem o Programa de Inscrição de Dispositivos iOS/iPadOS ou cenários de inscrição a granel) não são migrados para a nova autoridade do MDM. Para mover estes dispositivos para a nova autoridade de MDM, terá de contactar o suporte para obter assistência.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Limpeza de dispositivos móveis após a expiração do certificado MDM

O certificado MDM é renovado automaticamente quando os dispositivos móveis estão a comunicar com o serviço do Intune. Se os dispositivos móveis forem eliminados ou não conseguirem comunicar com o serviço do Intune durante um determinado período de tempo, o certificado MDM não será renovado. O dispositivo é removido do portal do Azure 180 dias depois da expiração do certificado MDM.

## <a name="remove-mdm-authority"></a>Remover a autoridade de MDM

A autoridade de MDM não pode ser novamente alterada para Desconhecida. A autoridade do MDM é utilizada pelo serviço para determinar a que portal os dispositivos matriculados reportam (Microsoft Intune ou Office 365 MDM).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>O que esperar depois de alterar a autoridade de MDM

- Quando o serviço Intune detetar que a autoridade de MDM de um inquilino mudou, envia uma mensagem de notificação a todos os dispositivos inscritos para fazer o check-in e sincronizar com o serviço (esta notificação está fora do check-in regular). Assim, depois de a autoridade do MDM para o inquilino ter sido alterada de Intune autónoma, todos os dispositivos que são ligados e online ligar-se-ão ao serviço, receberão a nova autoridade do MDM e serão geridos pela nova autoridade do MDM. A gestão e proteção destes dispositivos é contínua.
- Mesmo nos dispositivos ligados e online durante (ou pouco depois) a alteração da autoridade de MDM, irá ocorrer um atraso de até oito horas (consoante a hora do próximo registo regular agendado) até que os dispositivos sejam registados com o serviço da nova autoridade de MDM.    

  > [!IMPORTANT]    
  > Entre o momento em que muda a autoridade do MDM e quando o certificado APNs renovado é enviado para a nova autoridade, falhas nas novas matrículas de dispositivos e no check-in do dispositivo iOS/iPadOS. Como tal, é importante que reveja e carregue o certificado do APNs para a nova autoridade o mais rapidamente possível após a alteração da autoridade de MDM.

- Os utilizadores podem mudar rapidamente para a nova autoridade de MDM ao iniciar manualmente um registo do dispositivo no serviço. Os utilizadores podem fazer facilmente esta alteração através da aplicação Portal da Empresa e ao iniciar uma verificação da conformidade do dispositivo.
- Para validar que as coisas estão a funcionar corretamente depois de os dispositivos terem feito o check-in e sincronizado com o serviço após a alteração da autoridade do MDM, procure os dispositivos na nova autoridade do MDM.
- Existe um período provisório em que um dispositivo está offline durante a alteração da autoridade de MDM e em que esse dispositivo é registado no serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcional durante este período provisório, os seguintes perfis permanecem no dispositivo até sete dias (ou até que o serviço seja ligado à nova autoridade de MDM e receba as novas definições que substituirão as existentes):
  - Perfil e-mail
  - Perfil VPN
  - Perfil certificado
  - Perfil Wi-Fi
  - Perfis de configuração
- Depois de mudar para a nova autoridade de MDM, poderá demorar uma semana até que os dados de conformidade sejam corretamente apresentados na consola de administração do Microsoft Intune. No entanto, os estados de conformidade no Azure Active Directory e no dispositivo serão exatos para que o dispositivo permaneça protegido.
- Certifique-se de que as novas definições têm o mesmo nome que as definições antigas para garantir que as mesmas são substituídas. Caso contrário, os dispositivos poderão ficar com políticas e perfis redundantes.    

  > [!TIP]    
  > Como melhor prática, deve criar todas as implementações, configurações e definições de gestão pouco depois de concluir a alteração da autoridade de MDM. Isto ajuda a garantir que os dispositivos estão protegidos e são geridos ativamente durante o período provisório.

- Depois de alterar a autoridade de MDM, execute os seguintes passos para verificar se os dispositivos foram inscritos com êxito na nova autoridade:   
  - Inscrever um novo dispositivo
  - Certifique-se de que o dispositivo recém-inscrito aparece na nova autoridade do MDM.
  - Execute uma ação para o dispositivo, como o Bloqueio Remoto, a partir da consola de administração. Se tiver êxito, significa que o dispositivo está a ser gerido pela nova autoridade de MDM.
- Se tiver problemas com dispositivos específicos, pode anular a inscrição e inscrever novamente os dispositivos para ligá-los à nova autoridade e geri-los o mais rapidamente possível.

## <a name="next-steps"></a>Passos seguintes

Com a autoridade de MDM definida, pode começar a [inscrever dispositivos](../enrollment/device-enrollment.md).
