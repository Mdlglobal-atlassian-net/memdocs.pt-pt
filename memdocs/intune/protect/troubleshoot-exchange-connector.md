---
title: Resolução de problemas do conector do Exchange
titleSuffix: Microsoft Intune
description: Resolução de problemas relacionados com o conector do Exchange no local do Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8a2cee7e57f303f798f3484e52462a22e981ed59
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079132"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Resolução de problemas no Conector de Câmbio Intune

Este artigo descreve como resolver problemas relacionados com o Conector de Câmbio Intune.

## <a name="before-you-start"></a>Antes de começar

Antes de começar a resolver problemas com um problema de Conector de Intercâmbio em Intune, recolha algumas informações básicas para que esteja a trabalhar numa base sólida. Esta abordagem pode ajudá-lo a compreender melhor a natureza do problema e resolvê-lo mais rapidamente.

- Verifique se o seu processo satisfaz os requisitos de instalação. Consulte [a configuração do conector de troca intune](exchange-connector-install.md)no local .
- Verifique se a sua conta tem permissões de administrador exchange e intune.
- Note o texto completo e exato da mensagem de erro, detalhes e onde a mensagem é exibida.
- Determine quando o problema começou: 
  - Estás a preparar o conector pela primeira vez? 
  - O conector funcionou corretamente e depois falhou?
  - Se estava a funcionar, que mudanças ocorreram no ambiente Intune, no ambiente de intercâmbio ou no computador que executa o software de conector?
- O que é a autoridade do MDM?
- Que versão da Exchange usas?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Use powerShell para obter mais dados sobre questões de Conectore de troca

- Para obter uma lista de todos os dispositivos móveis para uma caixa de correio, use`Get-ActiveSyncDeviceStatistics -mailbox mbx`
- Para obter uma lista de endereços SMTP para uma caixa de correio, use`Get-Mailbox -Identity user | select emailaddresses | fl`
- Para obter informações detalhadas sobre o estado de acesso de um dispositivo, use`Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>Reveja a configuração do conector

Reveja os requisitos do [conector de troca no local](exchange-connector-install.md#intune-exchange-connector-requirements) para se certificar de que o seu ambiente e o conector estão configurados corretamente. 

### <a name="general-considerations-for-the-connector"></a>Considerações gerais para o conector

- Certifique-se de que os seus servidores de firewall e proxy permitem a comunicação entre o servidor que acolhe o Conector de Permuta Intune e o serviço Intune.

- O computador que acolhe o Conector de Câmbio Intune e o Servidor de Acesso ao Cliente de Troca (CAS) deve ser unido e na mesma LAN. Certifique-se de que as permissões necessárias são adicionadas para a conta utilizada pelo conector Intune Exchange.

- A conta de notificação é utilizada para recuperar as definições *de Autodiscover.* Para mais informações sobre a Autodisover em Exchange, consulte o [serviço Autodiscover no Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- O Intune Exchange Connector envia um pedido para o URL da EWS utilizando as credenciais da conta de notificação para enviar mensagens de correio eletrónico de notificação juntamente com o link *Get Started* (para se inscrever no Intune). A utilização do link *Get Started* para se inscrever é um requisito para dispositivos Android não-Knox. Caso contrário, estes dispositivos serão bloqueados pelo Acesso Condicional.

### <a name="common-issues-for-connector-configurations"></a>Questões comuns para configurações de conector

- **Permissões de conta**: Na caixa de diálogo do Conector de Troca Intune da Microsoft, certifique-se de que especificou uma conta de utilizador que distenha as permissões adequadas para executar os [cmdlets de troca do Windows PowerShell necessários](exchange-connector-install.md#exchange-cmdlet-requirements).
- **Mensagens de correio**eletrónico de notificação : Ativar notificações e especificar uma conta de notificação.
- Sincronização do Servidor de Acesso ao **Cliente**: Ao configurar o Conector de Troca, especifique um CAS que tenha a latência de rede mais baixa possível para o servidor que acolhe o conector De troca. A latência de comunicação entre o CAS e o conector Exchange pode atrasar a descoberta do dispositivo, especialmente quando se utiliza o Exchange Online Dedicated.
- Calendário de **sincronização**: Um utilizador com um dispositivo recém-inscrito pode ser adiado para ter acesso até que o conector Detroca sincronize com o EXCHANGE CAS. Uma sincronização completa é realizada uma vez ao dia e uma sincronização (rápida) delta ocorre várias vezes ao dia. Pode [forçar manualmente uma sincronização rápida ou uma sincronização completa](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) para minimizar atrasos.

## <a name="next-steps"></a>Passos seguintes
Os seguintes artigos podem ajudar a resolver problemas comuns e erros específicos:

- [Resolver problemas comuns para o Conector de Câmbio Intune](troubleshoot-exchange-connector-common-problems.md).
- [Resolva erros comuns para o Conector](troubleshoot-exchange-connector-common-errors.md)de Câmbio Intune .

Procure assistência do apoio ou da comunidade Intune:

- Consulte o [Suporte](../fundamentals/get-support.md) para utilizar a Consola Intune para ajudar a resolver o problema ou para abrir um caso de suporte com a Microsoft. 
- Publique o seu problema nos [fóruns da Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
