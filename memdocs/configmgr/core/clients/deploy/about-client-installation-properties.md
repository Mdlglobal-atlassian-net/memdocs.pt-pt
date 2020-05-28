---
title: Parâmetros e propriedades de instalação do cliente
titleSuffix: Configuration Manager
description: Conheça os parâmetros e propriedades da linha de comando ccmsetup para instalar o cliente Do Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ccfb523cc1abc3a64d396f32d55a4dc4551987c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428599"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Sobre os parâmetros e propriedades de instalação do cliente em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o comando CCMSetup.exe para instalar o cliente 'Gestor de Configuração'. Se fornecer *parâmetros* de instalação do cliente na linha de comando, modificam o comportamento de instalação. Se fornecer *propriedades* de instalação do cliente na linha de comando, modificam a configuração inicial do agente cliente instalado.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a>Sobre CCMSetup.exe

O comando CCMSetup.exe descarrega ficheiros necessários para instalar o cliente a partir de um ponto de gestão ou de uma localização de origem. Estes ficheiros podem incluir:  

- O pacote do Windows Installer client.msi que instala o software do cliente

- Pré-requisitos do cliente

- Atualizações e correções para o cliente do Gestor de Configuração

> [!NOTE]
> Não pode instalar o cliente.  

CCMSetup.exe fornece *parâmetros* de linha de comando para personalizar a instalação. Os parâmetros são pré-fixados com um corte `/` ( ) e por convenção são minúsculos. Especifica o valor de um parâmetro quando necessário utilizando um cólon ( `:` ) imediatamente seguido pelo valor. Para mais informações, consulte [os parâmetros da linha de comando CCMSetup.exe](#ccmsetupexe-command-line-parameters).

Também pode fornecer *propriedades* na linha de comando CCMSetup.exe para modificar o comportamento do cliente.msi.Propriedades por convenção são maiúsculas. Especifica um valor para uma propriedade usando um sinal igual ( `=` ) imediatamente seguido pelo valor. Para mais informações, consulte [as propriedades do Cliente.msi.](#clientMsiProps)

> [!IMPORTANT]  
> Especifique os parâmetros CCMSetup antes de especificar propriedades para cliente.msi.  

CCMSetup.exe e os ficheiros de suporte estão no servidor do site na pasta **Cliente** da pasta de instalação do Gestor de Configuração. O Gestor de Configuração partilha esta pasta para a rede sob a partilha do site. Por exemplo, `\\SiteServer\SMS_ABC\Client`.

Na linha de comandos, o comando CCMSetup.exe utiliza o seguinte formato:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Este exemplo faz as seguintes coisas:  

- Especifica o ponto de gestão denominado SMSMP01 para solicitar uma lista de pontos de distribuição para descarregar os ficheiros de instalação do cliente.  

- Especifica que a instalação deve parar se já existir uma versão do cliente no computador.  

- Indica ao client.msi que atribua o código de site S01 ao cliente.  

- Indica ao client.msi que utilize o ponto de estado de contingência com o nome SMSFP01.  

> [!TIP]  
> Se um valor de parâmetro tiver espaços, rodeie-o com aspas.  

Se alargar o esquema de Diretório Ativo para Gestor de Configuração, o site publica muitas propriedades de instalação de clientes em Serviços de Domínio de Diretório Ativo. O cliente do Gestor de Configuração lê automaticamente estas propriedades. Para mais informações, consulte sobre propriedades de [instalação de clientes publicadas nos Serviços](about-client-installation-properties-published-to-active-directory-domain-services.md) de Domínio de Diretório Ativo  

## <a name="ccmsetupexe-command-line-parameters"></a>Parâmetros da linha de comando CCMSetup.exe

### <a name=""></a><a name="bkmk_help"></a> /?

Mostra os parâmetros disponíveis da linha de comando para ccmsetup.exe.  

Exemplo: `ccmsetup.exe /?`

### <a name="source"></a>/fonte

Especifica a localização do descarregamento de ficheiros. Use um caminho local ou unc. O dispositivo descarrega ficheiros utilizando o protocolo do bloco de mensagens do servidor (SMB). Para **utilizar/fonte,** a conta do utilizador do Windows para as necessidades de instalação do cliente **Leia** permissões para o local.

> [!TIP]  
> Pode utilizar o parâmetro **/fonte** mais de uma vez numa linha de comando para especificar localizações alternativas de descarregamento.  

Exemplo: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

Especifica um ponto de gestão de fontes para os computadores se ligarem. Os computadores usam este ponto de gestão para encontrar o ponto de distribuição mais próximo para os ficheiros de instalação. Se não houver pontos de distribuição, ou se os computadores não conseguirem descarregar os ficheiros dos pontos de distribuição após quatro horas, descarregam os ficheiros a partir do ponto de gestão especificado.  

> [!IMPORTANT]  
> Este parâmetro especifica um ponto de gestão inicial para os computadores encontrarem uma fonte de descarregamento, e pode ser qualquer ponto de gestão em qualquer site. Não *atribui* o cliente ao ponto de gestão especificado.

Os computadores transferem os ficheiros através de uma ligação HTTP ou HTTPS, conforme a configuração da função do sistema de sites para ligações de cliente. O download também pode usar estrangulamento BITS se o configurar. Se configurar todos os pontos de distribuição e pontos de gestão apenas para ligações ao cliente HTTPS, verifique se o computador cliente tem um certificado de cliente válido.  

Pode utilizar o parâmetro de linha de comando **/mp** para especificar mais do que um ponto de gestão. Se o computador não conseguir ligar-se ao primeiro, tenta o próximo na lista especificada. Quando especificar vários pontos de gestão, separe os valores por pontos evígulos.

Se o cliente se ligar a um ponto de gestão utilizando HTTPS, especifique o FQDN e não o nome do computador. O valor deve corresponder ao ponto de gestão do certificado PKI's **Subject** or **Subject Alternative Name**. Embora o Gestor de Configuração suporte a utilização de um nome de computador no certificado para ligações na intranet, recomenda-se a utilização de um FQDN.

Exemplo com o nome do computador:`ccmsetup.exe /mp:SMSMP01`  

Exemplo com o FQDN:`ccmsetup.exe /mp:smsmp01.contoso.com`  

Este parâmetro também pode especificar o URL de um gateway de gestão de nuvem (CMG). Utilize este URL para instalar o cliente num dispositivo baseado na Internet. Para obter o valor deste parâmetro, utilize os seguintes passos:

- Crie um CMG. Para mais informações, consulte [Configurar um CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Num cliente ativo, abra um pedido de comando Windows PowerShell como administrador.
- Execute o seguinte comando:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Apreite o `https://` prefixo a utilizar com o parâmetro **/mp.**

Exemplo para quando utiliza o URL de gateway de gestão de nuvem:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Ao especificar o URL de um portal de gestão de nuvens para o parâmetro **/mp,** deve começar com `https://` .

### <a name="regtoken"></a>/regtoken

<!--5686290-->

A partir da versão 2002, utilize este parâmetro para fornecer um sinal de registo a granel. Um dispositivo baseado na Internet utiliza este símbolo no processo de registo através de um gateway de gestão de nuvem (CMG). Para mais informações, consulte [a autenticação baseada em Token para CMG](deploy-clients-cmg-token.md).

Quando utilizar este parâmetro, inclua também os seguintes parâmetros e propriedades:

- [**/mp**](#mp)
- [**NOME DE ANFITRIÕES CCMHOSTNAME**](#ccmhostname)
- [**Código SMSSite**](#smssitecode)
- [**SMSMP**](#smsmp)

A seguinte linha de comando exemplo inclui os outros parâmetros e propriedades de configuração necessários:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Se ccMSetup.exe não descarregar ficheiros de instalação, utilize este parâmetro para especificar o intervalo de repetição em minutos. CcMSetup continua a tentar novamente até atingir o limite especificado no parâmetro [**/descarregamento.**](#downloadtimeout)

Exemplo: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Este parâmetro impede que o CCMSetup funcionacomo um serviço, o que faz por defeito. Quando o CCMSetup funciona como um serviço, funciona no contexto da conta do Sistema Local do computador. Esta conta pode não ter direitos suficientes de acesso aos recursos de rede necessários para a instalação. Com **/noservice,** CCMSetup.exe corre no contexto da conta de utilizador que utiliza para iniciar a instalação.

Exemplo: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Especifica que o CCMSetup deve funcionar como um serviço que utiliza a conta do Sistema Local.  

> [!TIP]
> Se estiver a utilizar um script para executar CCMSetup.exe com o parâmetro **/serviço,** ccMSetup.exe sai após o início do serviço. Pode não reportar corretamente os detalhes da instalação do script.

Exemplo: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Utilize este parâmetro para desinstalar o cliente do Gestor de Configuração. Para mais informações, consulte [Desinstalar o cliente](../manage/manage-clients.md#BKMK_UninstalClient).

Exemplo: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Se alguma versão do cliente já estiver instalada, este parâmetro especifica que a instalação do cliente deve parar.  

Exemplo: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Utilize este parâmetro para forçar o computador a reiniciar, se necessário, para completar a instalação. Se não especificar este parâmetro, o CCMSetup sai quando é necessário reiniciar. Em seguida, continua após o próximo reinício manual.

Exemplo: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

Quando o dispositivo descarregar ficheiros de instalação do cliente sobre uma ligação HTTP, utilize este parâmetro para especificar a prioridade de descarregamento. Especifique um dos seguintes valores possíveis:

- `FOREGROUND`

- `HIGH`

- `NORMAL`(predefinido)

- `LOW`

Exemplo: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Se o CCMSetup não descarregar os ficheiros de instalação do cliente, este parâmetro especifica o tempo máximo em minutos. Após este intervalo, o CCMSetup para de tentar descarregar os ficheiros de instalação. O valor predefinido é de **1440** minutos (um dia).

Utilize o parâmetro [**/repetição**](#retry) para especificar o intervalo entre tentativas de repetição.

Exemplo: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Especifique este parâmetro para que o cliente utilize um certificado de autenticação do cliente PKI. Se não incluir este parâmetro, ou se o cliente não encontrar um certificado válido, utiliza uma ligação HTTP com um certificado auto-assinado.

Exemplo: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> Em alguns cenários, não é preciso especificar este parâmetro, mas ainda assim usar um certificado de cliente. Por exemplo, a instalação de clientes baseados em push e software. Utilize este parâmetro quando instalar manualmente um cliente e utilize o parâmetro **/mp** com um ponto de gestão ativado por HTTPS.
>
> Especifique também este parâmetro quando instalar um cliente para comunicação apenas à Internet. Utilize a propriedade **CCMALWAYSINF=1** juntamente com as propriedades para o ponto de gestão baseado na Internet **(CCMHOSTNAME**) e o código do site **(SMSSITECODE).** Para obter mais informações sobre a gestão de clientes baseadana na Internet, consulte [considerações para comunicações de clientes a partir da internet ou uma floresta não confiável.](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)  

### <a name="nocrlcheck"></a>/NoCRLCheck

Especifica que um cliente não deve verificar a lista de revogação do certificado (CRL) quando comunica em HTTPS com um certificado PKI. Quando não especifica este parâmetro, o cliente verifica o CRL antes de estabelecer uma ligação HTTPS. Para mais informações sobre a verificação do cliente CRL, consulte Planeamento para revogação de [certificado sacerdotal](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Exemplo: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Este parâmetro especifica um ficheiro de texto que lista as propriedades de instalação do cliente.

- Se o CCMSetup funciona como um serviço, coloque este ficheiro na pasta do sistema CCMSetup: `%Windir%\Ccmsetup` .

- Se especificar o parâmetro [**/noservice,**](#noservice) coloque este ficheiro na mesma pasta que CCMSetup.exe.

Exemplo: `CCMSetup.exe /config:"configuration file name.txt"`

Para fornecer o formato de ficheiro correto, utilize o ficheiro **mobileclienttemplate.tcf** na pasta no diretório de instalação do Gestor de `\bin\<platform>` Configuração no servidor do site. Este ficheiro tem comentários sobre as secções e como usá-las. Especifique as propriedades de instalação do cliente na `[Client Install]` secção, após o seguinte texto: `Install=INSTALL=ALL` .

Entrada `[Client Install]` da secção exemplo:`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

Este parâmetro especifica que CCMSetup.exe não instala o pré-requisito especificado. Pode introduzir mais do que um valor. Utilize o carácter do `;` ponto-e-vírgula para separar cada valor.

Exemplos:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

Para obter mais informações sobre os pré-requisitos do cliente, consulte os [pré-requisitos do cliente windows](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

Especifique que ccMSetup.exe desinstala qualquer cliente existente e instala um novo cliente.  

### <a name="excludefeatures"></a>/Excluir Características

Este parâmetro especifica que CCMSetup.exe não instala a função especificada.

Exemplo: `CCMSetup.exe /ExcludeFeatures:ClientUI` não instala o Software Center no cliente.  

> [!NOTE]  
> `ClientUI`é o único valor que o parâmetro **/ExcluirCaracterísticas** suporta.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a>Códigos de devolução CCMSetup.exe

O comando CCMSetup.exe fornece os seguintes códigos de devolução. Para resolver problemas, reveja `%WinDir%\ccmsetup\ccmsetup.log` o cliente para obter contexto e detalhes adicionais sobre códigos de devolução.

|Código de retorno|Significado|  
|-----------|-------|  
|0|Êxito|  
|6|Erro|  
|7|Reinício necessário|  
|8|Programa de configuração já em execução|  
|9|Falha de avaliação de pré-requisitos|  
|10|Falha de validação de hash do manifesto de configuração|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a>Propriedades ccmsetup.msi

As seguintes propriedades podem modificar o comportamento de instalação de ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Utilize este ccmsetup. *propriedade msi* para passar parâmetros e propriedades adicionais da linha de comando para ccmsetup. *exe*. Inclua outros parâmetros e propriedades dentro das aspas `"` (). Utilize esta propriedade quando arrancar o cliente do Gestor de Configuração com o método de [instalação intune MDM](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Exemplo: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> O Microsoft Intune limita a linha de comando a 1024 caracteres.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a>Propriedades cliente.msi

As seguintes propriedades podem modificar o comportamento de instalação do cliente.msi, que ccmsetup.exe instala. Se utilizar o método de instalação push do [cliente,](plan/client-installation-methods.md#client-push-installation)especifique estas propriedades no separador **Cliente** das Propriedades de **Instalação de Impulso** do Cliente na consola 'Gestor de Configuração'.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Especifica o identificador de aplicativo de cliente Azure Ative Directory (Azure AD). Cria ou importa a aplicação de clientes quando [configura os serviços Azure](../../servers/deploy/configure/azure-services-wizard.md) para a Cloud Management. Um administrador azure pode obter o valor desta propriedade a partir do portal Azure. Para mais informações, consulte [obter id da aplicação](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Para a propriedade **AADCLIENTAPPID,** este ID de aplicação é para o tipo de aplicação **nativa.**

Exemplo: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Especifica o identificador de aplicações do servidor Azure AD. Cria ou importa a aplicação do servidor quando [configura os serviços Azure](../../servers/deploy/configure/azure-services-wizard.md) para a Cloud Management. Quando cria a aplicação do servidor, na janela Create Server Application, esta propriedade é o **ID DA Aplicação URI**.

Um administrador azure pode obter o valor desta propriedade a partir do portal Azure. No **Diretório Ativo do Azure,** encontre a aplicação do servidor sob registos de **Aplicações.** Procure aplicação do tipo de aplicação **Web / API**. Abra a aplicação, selecione **Definições,** e depois selecione **Propriedades**. Utilize o valor **APP ID URI** para esta propriedade de instalação de cliente **AADRESOURCEURI.**

Exemplo: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Especifica o identificador de inquilino da AD Azure. O Gestor de Configuração liga-se a este inquilino quando [configura os serviços azure](../../servers/deploy/configure/azure-services-wizard.md) para a Cloud Management. Para obter o valor desta propriedade, use os seguintes passos:

- Num dispositivo Windows 10 que se junta ao mesmo inquilino da AD Azure, abra um pedido de comando.
- Executar o seguinte comando:`dsregcmd.exe /status`
- Na secção Estado do Dispositivo, encontre o valor **TenantId.** Por exemplo, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Um administrador azure também pode obter este valor no portal Azure. Para mais informações, consulte [a identificação do inquilino.](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)

Exemplo: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Especifica uma ou mais contas ou grupos de utilizadores do Windows a que deve ser dado acesso a definições e políticas de cliente. Esta propriedade é útil quando você não tem credenciais administrativas locais no computador cliente. Especifique uma lista de contas separadas por pontos evímetros `;` ().

Exemplo: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Se necessário, deixe o computador reiniciar silenciosamente após a instalação do cliente.

> [!IMPORTANT]  
> Quando utiliza esta propriedade, o computador reinicia sem aviso prévio. Este comportamento ocorre mesmo que um utilizador seja inscrito no Windows.

Exemplo: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Para especificar que o cliente é sempre baseado na Internet e nunca se conecta à intranet, detetete este valor de propriedade para `1` . O tipo de ligação do cliente apresenta **Sempre Internet**.  

Utilize esta propriedade com [**CCMHOSTNAME**](#ccmhostname) para especificar o FQDN do ponto de gestão baseado na Internet. Utilize-o também com o parâmetro CCMSetup [**/UsePKICert**](#usepkicert) e o código do site[**(SMSSITECODE**](#smssitecode)).

Para obter mais informações sobre a gestão de clientes baseadana na Internet, consulte [considerações para comunicações de clientes a partir da internet ou uma floresta não confiável.](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)

Exemplo: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Utilize esta propriedade para especificar a lista de emitentes de certificados. Esta lista inclui informações de certificado para as autoridades de certificação de raiz confiáveis (CA) que o site do Gestor de Configuração confia.  

Este valor é uma correspondência sensível a casos para atributos sujeitos que estão no certificado ca raiz. Atributos separados por uma vírgula `,` ou um ponto evíplo `;` . Especifique mais de um certificado CA raiz utilizando uma barra de separador `|` ().

Exemplo: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Utilize o valor do atributo dos **CertificateIssuers** no ficheiro **mobileclient.tcf** para o site. Este ficheiro encontra-se na `\bin\<platform>` subpasta do diretório de instalação do Gestor de Configuração no servidor do site.

Para obter mais informações sobre a lista de emitentes de certificados e como os clientes a utilizam durante o processo de seleção de certificados, consulte [Planeamento para a seleção](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)de certificados de cliente PKI .

### <a name="ccmcertsel"></a>CCMCERTSEL

Se o cliente tiver mais de um certificado de comunicação HTTPS, este imóvel especifica os critérios para que este selecione um certificado de autenticação de cliente válido.

Utilize as seguintes palavras-chave para pesquisar o nome do assunto do certificado ou nome alternativo do sujeito:

- **Assunto**: Encontre uma correspondência exata
- **SubjectStr:** Encontre uma correspondência parcial

Exemplos:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: Procure um certificado com uma correspondência exata com o nome do computador `computer1.contoso.com` no Nome do Assunto ou no Nome Alternativo do Sujeito.

- `CCMCERTSEL="SubjectStr:contoso.com"`: Procure um certificado que contenha `contoso.com` o nome do assunto ou o nome alternativo do sujeito.

Utilize a palavra-chave **SubjectAttr** para procurar o identificador de objetos (OID) ou atributos de nome distintos no nome do assunto ou nome alternativo do sujeito.

Exemplos:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Procurar o atributo da unidade organizacional expresso como identificador de objetos e nomeado `Computers` .

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Procurar o atributo da unidade organizacional expresso como um nome distinto, e nomeado `Computers` .

> [!IMPORTANT]
> Se utilizar o Nome do Assunto, a palavra-chave do **assunto** é sensível a casos, e a palavra-chave **SubjectStr** é insensível a casos.
>
> Se utilizar o Nome Alternativo sujeito, tanto o **sujeito** como as palavras-chave **subjectstr** são insensíveis a casos.

Para obter a lista completa de atributos que pode utilizar para a seleção de certificados, consulte valores de [atributo suportados para critérios](#BKMK_attributevalues)de seleção de certificados PKI .

Se mais de um certificado corresponder à pesquisa, e definir [**ccMFIRSTCERT**](#ccmfirstcert) `1` para, então o instalador de clientes seleciona o certificado com o período de validade mais longo.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Se o instalador do cliente não conseguir localizar um certificado válido na loja de certificados **pessoais** padrão para o computador, utilize esta propriedade para especificar um nome de loja de certificados alternativo.

Exemplo: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Esta propriedade permite depuração de registo quando o cliente instala. Esta propriedade faz com que o cliente registre informações de baixo nível para resolução de problemas. Evite utilizar esta propriedade em locais de produção. Pode ocorrer uma exploração madeireira excessiva, o que pode dificultar a descoberta de informações relevantes nos ficheiros de registo. Também ativa o [**CCMENABLELOGGING**](#ccmenablelogging).

Valores suportados:

- `0`: Desligue a exploração de depuração (predefinido)
- `1`: Ligar a exploração de depuração

Exemplo: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Para mais informações, consulte [sobre ficheiros](../../plan-design/hierarchy/about-log-files.md)de registo .

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

O Gestor de Configuração permite o registo por padrão.

Valores suportados:

- `TRUE`: Ligar a exploração madeireira (predefinido)
- `FALSE`: Desligue a exploração madeireira

Exemplo: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Para mais informações, consulte [sobre ficheiros](../../plan-design/hierarchy/about-log-files.md)de registo .

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

A frequência em minutos em que funciona a ferramenta de avaliação da saúde do cliente (ccmeval.exe). Especifique um valor inteiro de `1` `1440` . Por padrão, a ccmeval funciona uma vez por dia (1440 minutos).

Exemplo: `CCMSetup.exe CCMEVALINTERVAL=1440`

Para obter mais informações sobre a avaliação da saúde do cliente, consulte [os clientes do Monitor.](../manage/monitor-clients.md#bkmk_health)

### <a name="ccmevalhour"></a>CCMEVALHOUR

A hora durante o dia em que funciona a ferramenta de avaliação da saúde do cliente (ccmeval.exe). Especifique um valor inteiro de `0` (meia-noite) para `23` (23:00). Por defeito, a ccmeval corre à meia-noite.

Para obter mais informações sobre a avaliação da saúde do cliente, consulte [os clientes do Monitor.](../manage/monitor-clients.md#bkmk_health)

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Se definir este imóvel para `1` , o cliente seleciona o certificado PKI com o período de validade mais longo.

Exemplo: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Se o cliente for gerido através da internet, esta propriedade especifica o FQDN do ponto de gestão baseado na Internet.  

Não especifique esta opção com a propriedade de instalação de **SMSSITECODE=AUTO**. Atribua diretamente clientes baseados na Internet a um site baseado na Internet.

Exemplo: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Esta propriedade pode especificar o endereço de um gateway de gestão de nuvem (CMG). Para obter o valor desta propriedade, use os seguintes passos:

- Crie um CMG. Para mais informações, consulte [Configurar um CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Num cliente ativo, abra um pedido de comando Windows PowerShell como administrador.
- Execute o seguinte comando:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Utilize o valor devolvido como está com a propriedade **CCMHOSTNAME.**

Por exemplo: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Quando especificar o endereço de um CMG para a propriedade **CCMHOSTNAME,** não anexa um prefixo como `https://` . Utilize apenas este prefixo com o URL **/mp** de um CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Especifica a porta para o cliente utilizar quando comunica através do HTTP para os servidores do sistema do site. Por defeito, este valor é `80` .

Exemplo: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Especifica a porta para o cliente utilizar quando comunica através do HTTPS para os servidores do sistema do site. Por defeito, este valor é `443` .

Exemplo: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Utilize esta propriedade para definir a pasta para instalar os ficheiros do cliente do Gestor de Configuração. Por defeito, `%WinDir%\CCM` utiliza.

> [!TIP]
> Independentemente de onde instale os ficheiros do cliente, instala sempre o ficheiro **ccmcore.dll** na `%WinDir%\System32` pasta. Num SISTEMA de 64 bits, instala uma cópia do ccmcore.dll na `%WinDir%\SysWOW64` pasta. Este ficheiro suporta aplicações de 32 bits que utilizam a versão de 32 bits das APIs do cliente do Gestor de Configuração SDK.

Exemplo: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Utilize esta propriedade para especificar o nível de detalhe para escrever para ficheiros de registo do Gestor de Configuração.

Valores suportados:

- `0`: Verbose
- `1`: Padrão
- `2`: Advertências e erros
- `3`: Erros apenas

Exemplo: `CCMSetup.exe CCMLOGLEVEL=0`

Para mais informações, consulte [sobre ficheiros](../../plan-design/hierarchy/about-log-files.md)de registo .

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando um ficheiro de registo do Gestor de Configuração atinge o tamanho máximo, o cliente renomea-o como uma cópia de segurança e cria um novo ficheiro de registo. Esta propriedade especifica quantas versões anteriores do ficheiro de registo deve ser guardada. O valor predefinido é `1`. Se definir o valor para, o cliente não mantém qualquer histórico de `0` registo.

Exemplo: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Para mais informações, consulte [sobre ficheiros](../../plan-design/hierarchy/about-log-files.md)de registo .

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Esta propriedade especifica o tamanho máximo do ficheiro de registo em bytes. Quando um registo cresce para o tamanho especificado, o cliente renomea-o como um ficheiro de histórico, e cria um novo. O tamanho padrão é de 250.000 bytes, e o tamanho mínimo é de 10.000 bytes.

Exemplo: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300.000 bytes)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Deteto esta propriedade para impedir que os administradores mudem o site atribuído no painel de controlo do Gestor de `TRUE` Configuração.

Exemplo: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se definido para TRUE, esta propriedade desativa a capacidade dos utilizadores administrativos de alterar as definições da pasta cache do cliente no painel de controlo do Gestor de **Configuração.**  

Exemplo: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Especifique um domínio DNS para os clientes localizarem pontos de gestão que publica no DNS. Quando o cliente localiza um ponto de gestão, conta ao cliente sobre outros pontos de gestão na hierarquia. Este comportamento significa que o ponto de gestão que o cliente encontra do DNS pode ser qualquer um na hierarquia.

> [!NOTE]
> Não tem de especificar esta propriedade se o cliente está no mesmo domínio que um ponto de gestão publicado. Nesse caso, o domínio do cliente é automaticamente utilizado para procurar dNS por pontos de gestão.

Para obter mais informações sobre a publicação do DNS como um método de localização de serviço para clientes do Gestor de Configuração, consulte a [localização do Serviço e como os clientes determinam](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)o seu ponto de gestão atribuído .

> [!NOTE]  
> Por predefinição, o Gestor de Configuração não permite a publicação do DNS.

Exemplo: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Especifique o ponto de estado de recuo que recebe e processa mensagens de Estado enviadas pelos clientes do Gestor de Configuração.

Para mais informações, consulte [Determine se precisa de um ponto de estado](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)de recuo .

Exemplo: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Se definir esta propriedade para , o instalador de `TRUE` clientes não verifica a versão mínima necessária da Virtualização de Aplicações microsoft (App-V).

> [!IMPORTANT]  
> Se instalar o cliente do Gestor de Configuração sem instalar o App-V, não pode [implementar aplicações virtuais.](../../../apps/get-started/deploying-app-v-virtual-applications.md)

Exemplo: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Quando você ativa esta propriedade, o cliente reporta o estado, mas não remedia os problemas que encontra.

Exemplo: `CCMSetup.exe NOTIFYONLY=TRUE`

Para mais informações, consulte [Como configurar o estado do cliente](configure-client-status.md).

### <a name="provisionts"></a>PROVISÕES

<!--5526972-->

A partir da versão 2002, utilize esta propriedade para iniciar uma sequência de tarefas num cliente depois de se registar com sucesso no site.

Por exemplo, você disponibiliza um novo dispositivo Windows 10 com O Windows Autopilot, inscreva-o automaticamente no Microsoft Intune e, em seguida, instale o cliente do Gestor de Configuração para cogestão. Se especificar esta nova opção, o cliente recém-provisionado executa uma sequência de tarefas. Este processo dá-lhe flexibilidade adicional para instalar aplicações e atualizações de software, ou configurar configurações.

Utilize o seguinte processo:

1. [Crie uma sequência de tarefas de implementação não-OS](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) para instalar aplicações, instalar atualizações de software e configurar definições.

1. [Implemente esta sequência de tarefas](../../../osd/deploy-use/deploy-a-task-sequence.md) para a nova coleção incorporada, **Todos os Dispositivos de Provisionamento.** Note o ID de implementação da sequência de tarefas, por exemplo `PRI20001` .

1. [Instale o cliente do Gestor](deploy-clients-to-windows-computers.md#BKMK_Manual) de Configuração num dispositivo e inclua a seguinte propriedade: `PROVISIONTS=PRI20001` . Detete o valor desta propriedade como id de implementação da sequência de tarefas.

    - Se estiver a instalar o cliente a partir de Intune durante a inscrição em cogestão, consulte [como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Este método pode ter pré-requisitos adicionais. Por exemplo, inscrever o site no Azure Ative Directory ou criar um gateway de gestão de nuvem ativado por conteúdos.

Depois de o cliente instalar e registar-se corretamente no site, inicia a sequência de tarefas referenciada. Se o registo do cliente falhar, a sequência de tarefas não começará.

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Se um cliente tiver a chave raiz fidedigna do Gestor de Configuração errada, não pode contactar um ponto de gestão fidedigno para receber a nova chave raiz fidedigna. Use esta propriedade para remover a velha chave de raiz de confiança. Esta situação pode ocorrer quando se desloca um cliente de uma hierarquia de um site para outra. Esta propriedade aplica-se a clientes que utilizam a comunicação de cliente por HTTP e HTTPS. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exemplo: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Permite a reatribuição automática do site para atualizações do cliente quando utilizada com [SMSSITECODE=AUTO](#smssitecode).

Exemplo: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Especifica a localização da pasta cache do cliente no computador cliente. Por defeito, a localização da cache é `%WinDir%\ccmcache` .

Exemplo: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Utilize esta propriedade com a propriedade [**SMSCACHEFLAGS**](#smscacheflags) para controlar a localização da pasta cache do cliente. Por exemplo, instalar a pasta cache do cliente na maior unidade de disco de cliente disponível:`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Utilize esta propriedade para especificar mais detalhes de instalação para a pasta cache do cliente. Pode utilizar propriedades **SMSCACHEFLAGS** individualmente ou em combinação separadas por pontos evívias `;` ().

Se você não incluir esta propriedade:

- O cliente instala a pasta cache de acordo com a propriedade [**SMSCACHEDIR**](#smscachedir)
- A pasta não está comprimida.
- O cliente utiliza a propriedade [**SMSCACHESIZE**](#smscachesize) como o limite de tamanho em MB da cache

Ao atualizar um cliente existente, o instalador de clientes ignora esta propriedade.

#### <a name="values-for-the-smscacheflags-property"></a>Valores para a propriedade SMSCACHEFLAGS

- **PERCENTDISKSPACE**: Desloque o tamanho da cache em percentagem do espaço *total* do disco. Se especificar esta propriedade, também coloque [**o SMSCACHESIZE**](#smscachesize) num valor percentual.

- **PERCENTFREEDISKSPACE**: Desloque o tamanho da cache em percentagem do espaço de disco *livre.* Se especificar esta propriedade, também coloque [**o SMSCACHESIZE**](#smscachesize) como um valor percentual. Por exemplo, o disco tem 10 MB grátis, e especifica `SMSCACHESIZE=50` . O instalador do cliente define o tamanho da cache para 5 MB. Você não pode usar esta propriedade com a propriedade **PERCENTDISKSPACE.**

- **MAXDRIVE**: Instale a cache no maior disco disponível. Se especificar um caminho com a propriedade [**SMSCACHEDIR,**](#smscachedir) o instalador de clientes ignora este valor.

- **MAXDRIVESPACE**: Instale a cache na unidade do disco com o espaço mais livre. Se especificar um caminho com a propriedade [**SMSCACHEDIR,**](#smscachedir) o instalador de clientes ignora este valor.

- **NTFSONLY:** Instale apenas a cache numa unidade de disco formada em NTFS. Se especificar um caminho com a propriedade [**SMSCACHEDIR,**](#smscachedir) o instalador de clientes ignora este valor.

- **COMPRESS:** Guarde a cache de forma comprimido.

- **FAILIFNOSPACE**: Se não houver espaço suficiente para instalar a cache, remova o cliente do Gestor de Configuração.

Exemplo: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> As definições do cliente estão disponíveis para especificar o tamanho da pasta cache do cliente. A adição dessas definições de cliente substitui eficazmente a utilização de SMSCACHESIZE como uma propriedade de client.msi para especificar o tamanho da cache do cliente. Para obter mais informações, veja as [definições do cliente para tamanho da cache](about-client-settings.md#client-cache-settings).  

Ao atualizar um cliente existente, o instalador de clientes ignora esta definição. O cliente também ignora o tamanho da cache quando descarrega atualizações de software.

Exemplo: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Se reinstalar um cliente, não pode utilizar **sMSCACHESIZE** ou **SMSCACHEFLAGS** para definir o tamanho da cache para ser menor do que era anteriormente. O tamanho anterior é o valor mínimo.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Utilize esta propriedade para especificar a localização e o pedido de que o instalador do cliente verifique as definições de configuração. É uma série de um ou mais caracteres, cada um definindo uma fonte de configuração específica:

- `R`: Verifique se há definições de configuração no registo.

  Para mais informações, consulte as propriedades de [instalação do cliente Provision](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: Verifique se há definições de configuração nas propriedades de instalação a partir da linha de comando.

- `M`: Verifique as definições existentes quando atualizar um cliente mais antigo.

- `U`: Atualize o cliente instalado para uma versão mais recente e utilize o código de site atribuído.

Por predefinição, o instalador do cliente utiliza `PU` . Verifica primeiro as propriedades de instalação `P` e, em seguida, as definições existentes `U` ().  

Exemplo: `CCMSetup.exe SMSCONFIGSOURCE=RP`

<!--
### SMSDIRECTORYLOOKUP

Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  
-->

### <a name="smsmp"></a>SMSMP

Especifica um ponto de gestão inicial para o cliente do Gestor de Configuração utilizar.  

> [!IMPORTANT]  
> Se o ponto de gestão apenas aceitar ligações ao cliente em vez de HTTPS, prefixe o nome do ponto de gestão com `https://` .

Exemplos:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Se o cliente não conseguir obter a chave raiz fidedigna do Gestor de Configuração dos Serviços de Domínio do Diretório Ativo, utilize esta propriedade para especificar a chave. Este imóvel aplica-se a clientes que utilizam comunicação HTTP e HTTPS. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exemplo: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Obtenha o valor da chave raiz fidedigna do site a partir do ficheiro mobileclient.tcf no servidor do site. Para obter mais informações, consulte [a pré-provisão de um cliente com a chave raiz fidedigna utilizando um ficheiro](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Utilize esta propriedade para reinstalar a chave raiz fidedigna do Gestor de Configuração. Especifica o caminho completo e o nome de um ficheiro que contém a chave raiz fidedigna. Esta propriedade aplica-se a clientes que utilizam a comunicação de cliente por HTTP e HTTPS. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exemplo: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Especifica o caminho completo e o nome do certificado auto-assinado exportado no servidor do site. O servidor do site armazena este certificado na loja de certificados **SMS.** Tem o **servidor** do site de nome sujeito e o nome amigável Site Server Signing **Certificate**.

Exemplo: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Esta propriedade especifica um site do Gestor de Configuração ao qual atribui o cliente. Este valor pode ser um código de três caracteres ou a palavra `AUTO` . Se especificar , ou não especificar este imóvel, o cliente tenta determinar a sua atribuição do site a partir de Serviços de Domínio de `AUTO` Diretório Ativo ou de um ponto de gestão especificado. Para ativar as atualizações dos `AUTO` clientes, também detetete [sitereasSIGN=TRUE](#sitereassign).

> [!NOTE]  
> Se também especificar um ponto de gestão baseado na Internet com a propriedade [**CCMHOSTNAME,**](#ccmhostname) não utilize `AUTO` com **SMSSITECODE**. Atribua diretamente o cliente ao seu site especificando o código do site.

Exemplo: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a>Valores de atributo saque para critérios de seleção de certificados

O Gestor de Configuração suporta os seguintes valores de atributo para os critérios de seleção de certificados PKI:

|Atributo OID|Atributo de Nome Único|Definição do atributo|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou E-mail|Endereço de e-mail|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome do requerente|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou distrito|  
|2.5.4.9|STREET|Morada|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Title|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome próprio|  
|2.5.4.43|I ou Initials|Iniciais|  
|2.5.29.17|(sem valor)|Nome Alternativo do Requerente|  
