---
title: Problemas de resolução de problemas para o conector Intune Exchange
titleSuffix: Microsoft Intune
description: Resolução de problemas e resolução de problemas comuns para o conector Microsoft Intune Exchange no local.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328877"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Resolver problemas comuns com o conector Intune Exchange
 
Este artigo pode ajudar o administrador Intune a resolver problemas comuns com o funcionamento do conector Intune Exchange.

Antes de começar a resolver problemas, reveja [o conector Desajustado no local](troubleshoot-exchange-connector.md) para obter informações básicas sobre o conector. Consulte também questões comuns para a configuração do conector.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Um dispositivo Exchange ActiveSync não é descoberto a partir de Exchange

Quando um dispositivo Exchange ActiveSync não for descoberto a partir do Exchange, [monitorize a atividade do conector Exchange](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support) para ver se o conector Exchange está a sincronizar com o servidor Exchange. Se não tiver ocorrido nenhuma sincronização desde que o dispositivo entrou, colete os registos de sincronização e prenda-os a um pedido de suporte. Se uma sincronização completa ou uma sincronização rápida tiver terminado com sucesso desde que o dispositivo entrou, verifique os seguintes problemas:

- Certifique-se de que os utilizadores têm uma licença Intune. Caso contrário, o conector Exchange não descobrirá os seus dispositivos.

- Se o endereço SMTP principal do utilizador for diferente do nome principal do utilizador (UPN) no Azure Ative Directory (Azure AD), o conector Exchange não descobrirá nenhum dispositivo para esse utilizador. Corrija o endereço SMTP principal para resolver o problema.

- Se tiver ambos os servidores de caixa de correio Exchange 2010 e Exchange 2013 no seu ambiente, recomendamos que indique o conector Exchange para um servidor de Acesso ao Cliente (CAS) Exchange 2013. Se o conector Exchange estiver configurado para comunicar com um CAS exchange 2010, o conector Exchange não descobrirá nenhum dispositivo de utilizador no Exchange 2013.

- Para ambientes dedicados à Exchange Online, deve indicar o conector Exchange a um CAS de Intercâmbio de 2013 (não um CAS de Troca 2010) no ambiente dedicado durante a configuração inicial. O conector comunicará apenas com um CAS de Troca 2013 quando executar cmdlets PowerShell.

## <a name="problems-with-the-notification-email-message"></a>Problemas com a mensagem de e-mail de notificação

Para suportar o acesso condicional para caixas de correio no local em dispositivos que não executem o Android Knox, certifique-se de que a inscrição intune começa a partir da mensagem de e-mail "Get Started Now" que o conector Intune Exchange envia. Iniciar a inscrição a partir da mensagem garante que o dispositivo recebe um ActiveSyncID único em todas as plataformas (Exchange, Azure AD, Intune).

Um utilizador pode não receber a mensagem de e-mail de notificação porque:

- A conta de notificação foi criada incorretamente.
- Autodiscover falhou na conta de notificação.
- O pedido de Troca de Serviços Web (EWS) para enviar a mensagem de e-mail falhou.

Reveja as seguintes secções para resolver problemas de notificação de e-mail.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Verifique a conta de notificação que recupera as definições de Autodiscover

1. Certifique-se de que o serviço Autodiscover e o EWS estão configurados nos serviços de Acesso ao Cliente de Troca. Para mais informações, consulte [os serviços](https://docs.microsoft.com/Exchange/architecture/client-access/client-access) de Acesso ao Cliente e [o serviço Autodiscover no Exchange Server](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Verifique se a sua conta de notificação satisfaz os seguintes requisitos:

   - A conta tem uma caixa de correio ativa que é hospedada pelo seu servidor Exchange on-premises.

   - A conta UPN corresponde ao endereço SMTP.

3. A Autodiscover requer um servidor DNS que tenha um registo DNS para **Autodiscover.SMTPdomain.com** (por exemplo Autodiscover.contoso.com) que aponta para o seu servidor de Acesso ao Cliente de Troca. Para verificar o registo, especifique o fQDN no lugar de *Autodiscover.SMTPdomain.com* e siga estes passos:

   1. Num pedido de comando, introduza o *NSLOOKUP*.

   2. Insira *Autodiscover.SMTPdomain.com*. A saída deve ser semelhante à seguinte imagem: ![resultados da Nslookup](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   Também pode testar o serviço Autodiscover a partir da internet em https://testconnectivity.microsoft.com. Ou testá-lo a partir de um domínio local utilizando a ferramenta Microsoft Connectivity Analyzer. Para mais informações, consulte a [ferramenta Microsoft Connectivity Analyzer](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscovery"></a>Consulte a Autodescoberta

Se a Autodiscover falhar, experimente os seguintes passos:

1. [Configure um registo DNS auto-descoberto válido](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. Código rígido o URL EWS no ficheiro de configuração do conector Intune Exchange:

   1. Determine o URL EWS. O URL EWS padrão para troca é `https://<mailServerFQDN>/ews/exchange.asmx`, mas o seu URL pode diferir. Contacte o administrador da Exchange para verificar o URL correto para o seu ambiente.

   2. Editar o ficheiro *OnPremisesExchangeConnectorServiceConfiguration.xml.* By default, the file is located in *%ProgramData%\Microsoft\Windows Intune Exchange Connector* on the computer that runs the Exchange connector. Abra o ficheiro num editor de texto e, em seguida, mude a seguinte linha para refletir o URL DoWS para o seu ambiente: `<ExchangeWebServiceURL> https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Guarde o ficheiro e, em seguida, reinicie o computador ou reinicie o serviço de conector Microsoft Intune Exchange.

>[!NOTE]
> Nesta configuração, o conector Intune Exchange para de utilizar o Autodiscover e, em vez disso, liga-se diretamente ao URL EWS.

## <a name="next-steps"></a>Próximos passos

Para obter ajuda com erros específicos, tente [resolver erros comuns para o conector Intune Exchange](troubleshoot-exchange-connector-common-errors.md).

Para obter apoio, ou para obter ajuda da comunidade Intune:

- Ver [Suporte para](../fundamentals/get-support.md) utilizar a consola Intune para resolver o problema ou abrir um caso de suporte com a Microsoft.
- Publique o seu problema nos [fóruns da Microsoft Intune](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).