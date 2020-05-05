---
title: Instalar o conector do Exchange
titleSuffix: Configuration Manager
description: Instale e configure o conector Exchange para O Gestor de Configuração para gerir dispositivos móveis via ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721956"
---
# <a name="install-and-configure-the-exchange-connector"></a>Instalar e configurar o conector De Troca

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize este procedimento para instalar e configurar um conector exchange server para gerir dispositivos móveis. O Configuration Manager suporta apenas um conector numa organização do Exchange.

Antes de instalar o conector do Exchange Server para o 'Gestor de Configuração', certifique-se de que tem as permissões e versões necessárias. Para mais informações, consulte a [gestão do dispositivo com o Exchange and Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Conta de ligação cambial

Decida qual a conta que irá estabelecer ligação com o servidor de Acesso de Cliente do Exchange para gerir os dispositivos móveis. A conta pode ser a conta de computador do servidor do site ou uma conta de utilizador do Windows.

Em seguida, configure esta conta num grupo de papel de Troca para executar os seguintes cmdlets do Exchange Server:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Caixa de correio de entrada**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Utilizador-a-utilizador**  

- **Definição-activeSyncOrganizationSettings**  

As seguintes funções de gestão do Exchange Server incluem estes cmdlets:

- Gestão de Destinatários
- Gestão de Organização sem vista
- Gestão de Servidores

Para mais informações, consulte os grupos de [gestão de Understanding](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help) na documentação do Exchange Server 2013.

> [!TIP]  
> Se tentar instalar ou utilizar o conector 'Exchange Server' sem os cmdlets necessários, verá o seguinte `Invoking cmdlet <cmdlet> failed`erro no ficheiro EasDisc.log no computador do servidor do site: .

## <a name="install-the-connector"></a>Instale o conector

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração da Hierarquia,** e depois selecione **Conectores de Servidores de Troca**.

1. No separador **Casa** da fita, no grupo **Criar,** selecione **Adicionar Servidor de Troca**.

1. Na página **geral** do assistente do Add Exchange Server, selecione um dos ambientes do Exchange Server:

    - **No local, Exchange Server**: Especifique um único servidor ou um servidor de acesso ao cliente para cada site de Diretório Ativo.

        Se o servidor ou a matriz estiveroffline, o Gestor de Configuração tenta descobrir um Servidor de Acesso ao Cliente para utilizar. Se isso falhar, o Gestor de Configuração volta a utilizar um servidor de caixa de correio para fazer uma ligação a um Servidor de Acesso ao Cliente. Quando tenta novamente a ligação, regista os seguintes avisos no ficheiro `Failed to open runspace for site <site_name>`EasDisc.log no computador do servidor do site: .

    - **Servidor**de troca hospedado : Especifique o endereço do servidor do seu ambiente Exchange Online.

    Em seguida, selecione o site principal para executar o conector Do Servidor de Câmbio.

1. Na página **da Conta,** especifique a conta para se ligar ao Servidor de Câmbio. Para mais informações, consulte a [conta de ligação de troca](#exchange-connection-account).

1. Na página **Discovery,** configure o calendário de sincronização e as regras para encontrar dispositivos.

1. Na página **Definições,** configure as definições do dispositivo móvel nos seguintes grupos:

    - **General**
    - **Palavra-passe**
    - **Gestão de E-mails**
    - **Segurança**
    - **Aplicação**

    Para mais informações, consulte [as definições do conector De troca](manage-mobile-devices-with-exchange-activesync.md#policies).

    Se também inscrever dispositivos móveis utilizando o Diretor de Configuração [no local do MDM,](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)ative a opção de permitir a gestão externa de **dispositivos móveis.** Esta definição permite que estes dispositivos móveis continuem a receber e-mails da Exchange depois de o Gestor de Configuração os inscrever.

1. Conclua o assistente.

## <a name="verify-and-monitor"></a>Verificar e monitorizar

Verifique a instalação do conector do Servidor de Câmbio com mensagens de estado e ficheiros de registo:

- Confirme que o Gestor de Componentes do Site instalou com sucesso o conector do Exchange Server. Procure o estado da mensagem ID **1015** do componente **SMS_EXCHANGE_CONNECTOR.**

    A instalação pode falhar se o servidor de acesso ao cliente especificado estiver offline. Se o Gestor de Configuração não conseguir instalar com sucesso o conector, o Gestor de Configuração volta a tentar a instalação a cada 60 minutos. Continua a tentar novamente até que a instalação tenha sucesso ou remova o conector do Exchange Server.

- No computador do servidor do site, reveja o `Component SMS_EXCHANGE_CONNECTOR flagged for installation` **siteComp.log** para a seguinte entrada: . Em seguida, regista a instalação `STATMSG: ID=1015`bem sucedida com o seguinte texto: .

Depois de concluir a instalação, monitorize os dispositivos móveis que são encontrados e geridos pelo conector. Veja as coleções de dispositivos móveis e utilize os relatórios para dispositivos móveis.

> [!NOTE]  
> O Gestor de Configuração gera nomes para os dispositivos móveis que encontra. Utiliza o *nome*de utilizador do formato _*tipo de dispositivo*. Por exemplo, **jdoe_WindowsPhone.** Se um utilizador tiver mais de um dispositivo móvel com o mesmo tipo de dispositivo, o 'Configuração Manager' apresenta o mesmo nome para estes dispositivos móveis na consola e em relatórios.  

## <a name="see-also"></a>Consulte também

- [Portas utilizadas pelos clientes de Configuração e sistemas de site](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Suporte para o servidor proxy](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Recomendações de segurança para dispositivos móveis](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Informações de privacidade para dispositivos móveis que são geridos com o conector Exchange Server](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
