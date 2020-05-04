---
title: Erros comuns de resolução de problemas para o conector Intune Exchange
titleSuffix: Microsoft Intune
description: Resolução de problemas e resolução de erros comuns para o conector de câmbio Intune Microsoft Intune
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
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
ms.openlocfilehash: cb35fdc400c89c64b689f4695a48d201e50fc617
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79328885"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Resolver erros comuns para o Conector de Câmbio Intune

Este artigo pode ajudar o administrador Intune a resolver erros e mensagens específicas sobre o funcionamento do Conector de Câmbio Intune.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Configuração falhou e devolveu código de erro 0x00000001

**Emissão:**  
Quando tentar configurar o Conector de Troca Intune da Microsoft, recebe a seguinte mensagem de erro:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Este problema pode ocorrer se as definições de procuração da Internet estiverem mal configuradas.

**Resolução:**  
Configure as definições de procuração:
1. Contacte o administrador de rede local para se certificar de que as definições de procuração estão corretamente configuradas. 
2. Utilize o comando **Winhttp netsh** para configurar o servidor proxy e adicionar a lista de exclusão necessária. Por exemplo:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Configuração falhou e devolveu código de erro 0x000000b   

**Emissão:**  
Quando tentar configurar o Conector de Troca Intune da Microsoft, recebe a seguinte mensagem de erro:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Este problema pode ocorrer se a conta que usou para iniciar sintonização não for uma conta intune Global Administrator.

**Resolução:**  
Inscreva-se no Intune com uma conta que seja um Administrador Global, ou adicione a sua conta ao grupo Global Admin. Para mais informações, consulte o [controlo da administração baseado em Role (RBAC) com](../fundamentals/role-based-access-control.md)o Microsoft Intune .

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Configuração falhou e devolveu código de erro 0x00000006

**Emissão:**  
Quando tentar configurar o Conector de Troca Intune da Microsoft, recebe a seguinte mensagem de erro:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Este erro pode ocorrer se um servidor proxy for utilizado para ligar à Internet e estiver a bloquear o tráfego ao Serviço Intune. Para determinar se um proxy está a ser utilizado, vá às > **opções**de Internet do **Painel de Controlo,** selecione o separador **De Ligação** e, em seguida, clique em **Definições LAN**.

**Resolução:**  

- **Opção 1** - Remova as definições de procuração para permitir que o computador se conectem à Internet sem passar pelo proxy.  

- **Opção 2** - Configure o seu servidor proxy para permitir a comunicação ao serviço Intune, conforme documentado nos [requisitos do Conector de Troca Intune](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Evento 7000 ou 7041: O Serviço de Conector de Intercâmbio Intune da Microsoft não arranca

**Emissão:**  
Um dispositivo iOS não se inscreve em Intune e gera uma das seguintes mensagens de erro:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Este problema pode ocorrer se a conta **WIEC_User** não tiver o **Log on como** utilizador de serviço na política local.

**Resolução:**  
No computador que executa o Conector de Troca Intune, atribua o **Registo como** utilizador de serviço à conta de serviço **WIEC_User.** Se o computador for um nó num cluster, certifique-se de atribuir o Registo como utilizador *de serviço* direito à conta de serviço cluster em todos os nós do cluster.  

Para atribuir o **Registo como** utilizador de serviço diretamente à conta de serviço **WIEC_User** no computador, siga estes passos:

1. Inicie sessão no computador como administrador ou como membro do grupo Administradores.
2. Executar **secpol.msc** para abrir a Política de Segurança Local.
3. Vá para **as definições de segurança As** > **políticas locais,** e, em seguida, selecione A atribuição **de direitos**de utilizador .
4. No painel direito, clique duas vezes **em Log on como um serviço**.
5. Selecione **Adicionar Utilizador ou Grupo,** adicione **WIEC_USER** à apólice e, em seguida, selecione **OK** duas vezes.

Se o **Log on como** direito de utilizador de serviço foi atribuído a **WIEC_User** mas foi posteriormente removido, contacte o administrador de domínio para determinar se uma definição de Política de Grupo está a sobrepor-se.  

## <a name="next-steps"></a>Passos seguintes  

O seguinte artigo pode ajudar a resolver erros específicos:
- [Resolver problemas comuns para o Conector de Câmbio Intune](troubleshoot-exchange-connector-common-problems.md).git 

Procure ajuda do apoio ou da comunidade Intune.
- Consulte o [Suporte](../fundamentals/get-support.md) para utilizar a Consola Intune para ajudar a resolver o problema ou para abrir um caso de suporte com a Microsoft. 
- Publique o seu problema nos [fóruns da Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
