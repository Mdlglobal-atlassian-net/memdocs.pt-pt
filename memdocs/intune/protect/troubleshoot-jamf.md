---
title: Resolução de problemas na integração do Jamf Pro com a Microsoft Intune
titleSuffix: Microsoft Intune
description: Sugestões para resolver problemas quando integra o Jamf Pro para dispositivos Mac, com a Microsoft Intune.
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
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328873"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Integração de problemas do Jamf Pro com a Microsoft Intune

Este artigo ajuda os administradores intune a compreender e resolver problemas com a integração do Jamf Pro para macOS com Intune.

> [!TIP]  
> Grande parte das informações deste artigo apareceram originalmente nos [problemas de Troubleshoot quando integra o Jamf com](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) a Microsoft Intune na support.microsoft.com.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar a resolver problemas, recolha algumas informações básicas para esclarecer o problema e reduza o tempo para encontrar uma resolução. Por exemplo, quando se depara com uma questão relacionada com a integração jamf-Intune, verifique sempre que os pré-requisitos foram todos cumpridos. Reveja as seguintes considerações antes de iniciar a resolução de problemas:

- Reveja os pré-requisitos da [Integrate Jamf Pro com Intune](conditional-access-integrate-jamf.md#prerequisites).
- Todos os utilizadores devem ter licenças Microsoft Intune e Microsoft AAD Premium P1 
- Deve ter uma conta de utilizador que tenha permissões de integração Intune microsoft na consola Jamf Pro.
- Deve ter uma conta de utilizador que tenha permissões global de administração no Azure.


Considere as seguintes informações ao investigar a integração do Jamf Pro com o Intune: 
- Qual é a mensagem exata de erro?
- Onde está a mensagem de erro?
- Quando começou o problema?  A integração do Jamf Pro com a Intune já funcionou?
- Quantos utilizadores são afetados? Todos os utilizadores são afetados ou apenas alguns?
- Quantos dispositivos são afetados? Todos os dispositivos são afetados ou apenas alguns?
 

## <a name="common-problems"></a>Problemas comuns 

As seguintes informações podem ajudá-lo a identificar e resolver problemas comuns para dispositivos após a instalação da integração intune e jamf Pro.  

| Problema   | Mais informações                  |
|-----------------|--------------------------|
| **Os dispositivos estão marcados como sem resposta no Jamf Pro**  | [Dispositivos não conseguem fazer o check-in com o Jamf Pro ou com a Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Dispositivos Mac solicitam o acesso ao keychain quando abre uma aplicação Os dispositivos não se registam**  | [Os utilizadores são solicitados para a sua palavra-passe para permitir que as aplicações se registem com o Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Dispositivos não se registam**  | Podem aplicar-se as seguintes causas: <br> **-** [ ***Cause 1*** - A aplicação Jamf Pro em Azure tem permissões incorretas](#cause-1) <br> **-** [ ***Cause 2*** - Existe um problema para o *Conector Jamf Native macOS* em Azure AD](#cause-2) <br> **-** [ ***Cause 3*** - O utilizador não tem uma licença intune ou jamf válida](#cause-3) <br> **-** [ ***Cause 4*** - O utilizador não usou o Jamf Self Service para iniciar a aplicação Portal da Empresa](#cause-4) <br> **-** [ ***Causa 5*** - Integração intune está desligada](#cause-5) <br> **-** [ ***Causa 6*** - O dispositivo foi previamente matriculado em Intune, ou o utilizador tentou registar o dispositivo várias vezes](#cause-6) <br> **-** [ ***Cause 7*** - JamfAAD solicita acesso a uma "Chave de Adesão ao Local de Trabalho da Microsoft" do porta-chaves dos utilizadores](#cause-7) |
|  **Dispositivo Mac mostra-se em conformidade no Intune mas não conforme em Azure** | [Problemas de registo de dispositivos](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **As entradas duplicadas aparecem na consola Intune para dispositivos Mac matriculados utilizando o Jamf** | [Múltiplas inscrições fro o mesmo dispositivo](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **A política de conformidade não avalia o dispositivo** | [Grupos de dispositivos de metas de política](#compliance-policy-fails-to-evaluate-the-device) |
| **Não conseguiu recuperar o sinal de acesso para a Microsoft Graph API** | Podem aplicar-se as seguintes causas: <br> -[Permissões para a app Jamf Pro em Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [licença expirada para Jamf ou Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Portos não estão abertos](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Os dispositivos estão marcados como sem resposta no Jamf Pro  

**Causa**: As seguintes causas são causas comuns de dispositivos marcados como *Sem Resposta* por Jamf Pro:

- O dispositivo não consegue fazer o check-in com o Jamf Pro.  
  O Jamf Pro espera que os dispositivos entrem a cada 15 minutos. Os dispositivos são marcados como sem resposta pelo Jamf quando não fazem o check-in durante um período de 24 horas.  

- O dispositivo não consegue fazer o check-in com a Azure AD.  
  Com registo bem sucedido na Azure AD, os dispositivos macOS recebem um símbolo Azure:
  - Este símbolo refresca-se a cada 12 horas.   
  - Quando a atualização do símbolo falha durante 24 horas ou mais, o Jamf Pro marca o dispositivo como sem resposta.  
  - Se o token Azure expirar, os utilizadores são solicitados a assinar no Azure para obter um novo token. Um token refrescante para acesso Azure é gerado a cada sete dias.

**Resolução**  
Depois de um dispositivo ser marcado como *Sem resposta* pelo Jamf Pro, o utilizador inscrito do dispositivo deve iniciar sessão para corrigir o estado não responsivo. Deve ser o utilizador que tem colocado o trabalho a juntar-se à conta, uma vez que tem a identidade de Intune no seu porta-chaves de login.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Dispositivos Mac solicitam o acesso ao keychain quando abre uma aplicação  

Depois de configurar a integração intune e jamf Pro e implementar políticas de acesso condicional, os utilizadores de dispositivos geridos com o Jamf Pro recebem indicações para uma palavra-passe ao abrir em aplicações do Microsoft Office 365, como Teams, Outlook e outras aplicações que requerem o Azure Autenticação ad. 

Por exemplo, aparece uma solicitação com texto semelhante ao seguinte exemplo ao abrir as Equipas Microsoft:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Causa**: Estas solicitações são geradas pela Jamf Pro para cada aplicação aplicável que requer o registo da AD Azure. 

**Resolução**   
A pedido, o utilizador deve fornecer a sua senha de dispositivo para iniciar sessão no Azure AD. As opções incluem:
- **Negue** - Não intensie e não utilize a aplicação.
- **Permitir** - Uma inscrição única. Da próxima vez que a aplicação abrir, solicita o seu insessão novamente.
- **Sempre permitir** - As credenciais de inscrição estão em cache para a aplicação. Da próxima vez que a aplicação abrir, não pede o inserto.  

Selecionar *Sempre Permitir uma* aplicação só aprova essa aplicação para futura sessão. Aplicações adicionais solicitam a autenticação até que também estejam definidas como *Sempre Permitir*. Credenciais em cache para uma aplicação não podem ser usadas por outra aplicação.  

### <a name="devices-fail-to-register"></a>Dispositivos não se registam  

Existem várias causas comuns para dispositivos Mac que não se registam.  

#### <a name="cause-1"></a>Causa 1  

**O pedido da empresa Jamf Pro em Azure tem a permissão errada ou tem mais de uma permissão**  

  Quando criar a aplicação em Azure, deve remover todas as permissões API padrão e, em seguida, atribuir insocale uma única permissão de *update_device_attributes*. 

  **Resolução**  
  Reveja e, se necessário, corrija as permissões para a app Jamf que criou em Azure AD. Consulte o procedimento para [criar um pedido para jamf em Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Causa 2  

**A app **Jamf Native macOS Connector** não foi criada no seu inquilino DaD Azure ou o consentimento para o conector foi assinado por uma conta que não tem direitos de administração globais**  

  **Resolução**  
  Consulte a secção de *Integração Intune* do MacOS em Integração com a [Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) na docs.jamf.com. 

#### <a name="cause-3"></a>Causa 3

**O utilizador não tem uma licença intune ou Jamf válida**  

  A falta de uma licença válida pode resultar no seguinte erro, o que indica que a licença Jamf está caducada:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Resolução**
  - Licença Jamf: Contacte a Jamf para obter uma nova licença para a Jamf.  
  - Licença Intonizada: Atribuir ao utilizador uma licença válida ou contactar a Microsoft ou o seu Parceiro para obter informações sobre como obter uma licença atual.

#### <a name="cause-4"></a>Causa 4  

**O utilizador não usou o *Jamf Self Service* para iniciar a aplicação Portal da Empresa**

Para que um dispositivo se inscreva e registe com sucesso com o Intune através do Jamf, o utilizador deve utilizar o Jamf Self Service para abrir o Portal da Empresa Intune. Se o utilizador abrir manualmente o portal da empresa, o dispositivo inscreve-se e regista-se sem a sua ligação ao Jamf.  

Para determinar qual o serviço utilizado para se inscrever e registar, procure na aplicação Portal da Empresa no dispositivo. Quando registado através do Jamf, deverá receber uma notificação para abrir a aplicação Self-Service para efetuar alterações.

Na aplicação Portal da Empresa, o utilizador poderá ver **`Not registered`** , podendo aparecer uma entrada semelhante ao seguinte exemplo nos registos do Portal da Empresa:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Resolução**  
Para alterar a fonte de registo de Intune para Jamf:
1. [Desinscreva o dispositivo macOS a partir de Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). Para evitar mais complicações para dispositivos que não sejam totalmente removidos de Intune, consulte a [*Causa 6*](#cause-6) nesta lista de causas.  

2. No dispositivo, utilize o Jamf Self Service para abrir a aplicação Do Portal da Empresa e, em seguida, matricular o dispositivo com intune. Esta tarefa requer que tenha [utilizado o Jamf para implementar a aplicação Portal da Empresa para o macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro), e ter [criado uma política no Jamf Pro que regista o dispositivo de utilizadores com a Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. Quando o portal abre, o primeiro ecrã que vê leva-o a iniciar o seu 'SignIn'. Use o seu trabalho ou conta escolar  

4. O Portal da Empresa confirma as informações da sua conta e mostra o estado de Inscrição e Conformidade do Dispositivo. Os triângulos amarelos realçam as ações que tem de efetuar para proteger o seu dispositivo macOS para a escola ou o trabalho. Clique em começar a inscrição.  

5. Se lhe for pedido, escreva as informações de início de sessão do seu computador.  
     
A inscrição do seu dispositivo na gestão poderá demorar alguns minutos. Durante este tempo, poderá fazer outras coisas no seu dispositivo. Irá receber uma mensagem após a conclusão da Configuração de Acesso da Empresa para o informar de que está pronto.

#### <a name="cause-5"></a>Causa 5  

**A integração intonizada está desligada**

Se a integração intune for desligada, os utilizadores recebem uma janela pop-up no Portal da Empresa com a seguinte mensagem quando tentam registar um dispositivo:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

O servidor Jamf Pro envia um pulso aos servidores Intune quando a integração é desligada que diz ao Intune que a integração é desativada. 

**Resolução**  
Reativar a integração intune dentro do Jamf Pro. Consulte [Configure Microsoft Intune Integration in Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a>Causa 6  

**O dispositivo foi previamente matriculado em Intune, ou o utilizador tentou registar o dispositivo várias vezes**

Se um dispositivo não estiver matriculado no Jamf, mas não for corretamente removido do Intune, ou se forem feitas várias tentativas de registo, poderá ver várias instâncias do mesmo dispositivo no portal. Isto faz com que a inscrição do Jamf falhe.

**Resolução**  
1. No Mac, inicie o **Terminal.**
2. Executar **sudo JAMF removendo perfil de dismídeo**.
3. Executar **sudo JAMF removerFramework**.
4. No servidor JAMF Pro, apague o registo de inventário do computador.
5. Elimine o dispositivo do AzureAD.
6. Elimine os seguintes ficheiros no dispositivo se existirem:
   - /Biblioteca/Suporte de Aplicação/com.microsoft.CompanyPortal.usercontext.info
   - /Biblioteca/Suporte de Aplicação/com.microsoft.CompanyPortal
   - /Biblioteca/Suporte de Aplicação/com.jamfsoftware.selfservice.mac
   - /Biblioteca/Aplicação Guardada
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Biblioteca/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Biblioteca/Preferências/com.microsoft.CompanyPortal.plist
   - /Biblioteca/Preferências/com.jamfsoftware.selfservice.mac.plist
   - /Biblioteca/Preferências/com.jamfsoftware.management.jamfAAD.plist
   - /Utilizadores/<username>/Biblioteca/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Utilizadores/<username>/Biblioteca/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Chave de transporte da Microsoft Session (chaves públicas e privadas)
   - Chave de adesão ao Microsoft Workplace (teclas públicas e privadas)
7. Remova qualquer coisa do porta-chaves do dispositivo que faz referência à *Microsoft*, *Intune*, ou *Portal da Empresa,* incluindo certificados DeviceLogin.microsoft.com. Remova as referências *JAMF,* com exceção da chave pública e privada JAMF. 
   > [!IMPORTANT]  
   > A remoção da chave pública e privada quebrará a inscrição do dispositivo.

8. Elimine qualquer uma das seguintes entradas que encontrar:  
   - Tipo: Palavra-passe de aplicação; Conta: com.microsoft.workplacejoin.thumbprint
   - Tipo: Palavra-passe de aplicação; Conta: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Tipo: Certificado; Emitido por: MS-Organization-Access
   - Tipo: Preferência de identidade; Nome (URL ADFS STS se presente): https://adfs\<DNSName>.com/adfs/ls
   - Tipo: Preferência de identidade; Nome: https://enterpriseregistration.windows.net
   - Tipo: Preferência de identidade; Nome: https://enterpriseregistration.windows.net/  
9. Reiniciar o dispositivo Mac.
10. Desinstale o Portal da Empresa a partir do dispositivo.
11. Vá ao portal.manage.microsoft.com e elimine todas as instâncias do dispositivo Mac. Espere pelo menos 30 minutos antes de passar para o próximo passo.
12. Reinscreva o dispositivo no JAMF Pro.
13. Reabra o Self Service e inicie a política de registo.


#### <a name="cause-7"></a>Causa 7  

**JamfAAD solicita acesso a uma chave de "Microsoft Workplace Join Key" do porta-chaves dos utilizadores**

Durante o registo, o utilizador de um dispositivo macOS recebe a seguinte solicitação para permitir o acesso do JamfAAD a uma chave a partir do seu porta-chaves: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**Resolução**  
Para registar com sucesso o dispositivo com a AD Azure, o Jamf exige que o utilizador forneça a sua palavra-passe de conta e selecione **Permitir**.

Este pedido é semelhante ao pedido de solicitação de [dispositivos Mac para iniciar o início](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)do sessão em cadeia quando abrir uma aplicação , no início deste artigo.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Dispositivo Mac mostra-se em conformidade no Intune mas não conforme em Azure  

**Causa**: As seguintes condições podem fazer com que um dispositivo apresente-se como conforme em Intune, mas não conforme em Azure:  
- O dispositivo não está registado corretamente.  
- O dispositivo foi registado várias vezes sem a limpeza necessária.

**Resolução**  
Para resolver este problema, siga a resolução para a [*Causa 6*](#cause-6) para *Dispositivos não se registar,* no início deste artigo. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>As entradas duplicadas aparecem na consola Intune para dispositivos Mac matriculados utilizando o Jamf  
 
**Causa**: Um dispositivo é registado com Intune várias vezes, normalmente sendo reregistado depois de ser removido de Intune.  

Quando um dispositivo é removido da integração intune e jamf Pro, alguns dados podem ser deixados para trás, o que pode causar registos sucessivos para criar entradas duplicadas.  

**Resolução**  
Para resolver este problema, siga a resolução para a [*Causa 6*](#cause-6) para *Dispositivos não se registar,* no início deste artigo. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>A política de conformidade não avalia o dispositivo  

**Causa**: A integração do Jamf com o Intune não suporta a política de conformidade que visa grupos de dispositivos. 

**Resolução**  
Modificar a política de conformidade para dispositivos macOS a atribuir aos grupos de utilizadores. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Não conseguiu recuperar o sinal de acesso para a Microsoft Graph API

Recebe o seguinte erro:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

A origem deste erro pode ser uma das seguintes causas: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Há um problema de permissão com a aplicação Jamf Pro em Azure

Ao registar a aplicação Jamf Pro em Azure, ocorreu uma das seguintes condições:  
- A aplicação recebeu mais de uma permissão.
- O **consentimento do administrador grant para\<a sua *empresa>***  a opção não foi selecionada.  

**Resolução**  
Consulte a resolução da Causa 1 para [Dispositivos não se registar,](#devices-fail-to-register)no início deste artigo.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Uma licença necessária para a integração Jamf-Intune expirou

**Resolução**: Consulte a resolução da Causa 3 para [dispositivos não se registar](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>As portas necessárias não estão abertas na sua rede

**Resolução**: Reveja as informações para as portas de rede em [pré-requisitos](conditional-access-integrate-jamf.md#prerequisites) para integrar o Jamf Pro com o Intune.


## <a name="next-steps"></a>Próximos passos
Saiba mais sobre [integrar o Jamf Pro com o Intune](conditional-access-integrate-jamf.md)