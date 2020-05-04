---
title: Configurar portais do BitLocker
titleSuffix: Configuration Manager
description: Instale os componentes de gestão BitLocker para o portal de self-service, e o site de administração e monitorização
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cbd7c516515718cca96bff9b1715233964cb2aa5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717364"
---
# <a name="set-up-bitlocker-portals"></a>Configurar portais do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Para utilizar os seguintes componentes de gestão BitLocker no Gestor de Configuração, primeiro é necessário instalá-los:

- Portal de autosserviço do utilizador
- Site de administração e monitorização (portal de helpdesk)

Pode instalar os portais num servidor de site existente com o IIS ou utilizar um servidor web autónomo para os hospedar.

> [!NOTE]
> Instale apenas o portal de auto-atendimento e o site de administração e monitorização com uma base de dados de site primário. Numa hierarquia, instale estes websites para cada local primário.

Antes de começar, confirme os [pré-requisitos](../../plan-design/bitlocker-management.md#prerequisites) para estes componentes.

## <a name="script-usage"></a>Utilização do script

Este processo utiliza um script PowerShell, MBAMWebSiteInstaller.ps1, para instalar estes componentes no servidor web. Aceita os seguintes parâmetros:

- `-SqlServerName <ServerName>`(obrigatório): O nome de domínio totalmente qualificado do servidor de base de dados do site primário.

- `-SqlInstanceName <InstanceName>`: O nome da instância SQL Server para a base de dados do site primário. Se a SQL utilizar a instância predefinida, não inclua este parâmetro.

- `-SqlDatabaseName <DatabaseName>`(obrigatório): O nome da base de dados `CM_ABC`do local primário, por exemplo.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: O URL do serviço web do ponto de serviço de reporte do site primário. É o valor URL do **Serviço Web** no Gestor de Configuração de **Serviços de Reporte.**

    > [!NOTE]
    > Este parâmetro é para instalar o Relatório de Auditoria de **Recuperação** que está ligado ao site de administração e monitorização. Por padrão, o Gestor de Configuração inclui os outros relatórios de gestão bitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Por `contoso\BitLocker help desk users`exemplo, . Um grupo de utilizadores de domínio cujos membros têm acesso às áreas de **Gestão TPM** e **Drive Recovery** do site de administração e monitorização. Ao utilizar estas opções, esta função precisa de preencher todos os campos, incluindo o domínio do utilizador e o nome da conta.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Por `contoso\BitLocker help desk admins`exemplo, . Um grupo de utilizadores de domínio cujos membros têm acesso a todas as áreas de recuperação do site de administração e monitorização. Ao ajudar os utilizadores a recuperar em seus impulsos, esta função só tem de entrar na chave de recuperação.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Por `contoso\BitLocker report users`exemplo, . Um grupo de utilizadores de domínio cujos membros têm acesso apenas à área de **Relatórios** da administração e do site de monitorização.

    > [!NOTE]
    > O script do instalador não cria os grupos de utilizadores de domínio que especifica nos parâmetros **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**e **-MbamReportUsersGroupName.** Antes de executar o guião, certifique-se de criar estes grupos.
    >
    > Quando especificar os parâmetros **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**e **-MbamReportUsersGroupName,** certifique-se de especificar tanto o nome de domínio como o nome do grupo. Utilize o formato `"domain\user_group"`. Não exclua o nome de domínio. Se o nome de domínio ou nome de grupo contiver espaços`"`ou caracteres especiais, encerre o parâmetro em aspas ().

- `-SiteInstall Both`: Especificar quais dos componentes a instalar. As opções válidas incluem:
  - `Both`: Instalar ambos os componentes
  - `HelpDesk`: Instalar apenas o site de administração e monitorização
  - `SSP`: Instalar apenas o portal de auto-atendimento

- `-IISWebSite`: O site onde o script instala as aplicações web MBAM. Por padrão, utiliza o website padrão IIS. Crie o site personalizado antes de utilizar este parâmetro.

- `-InstallDirectory`: O caminho onde o script instala os ficheiros de aplicação web. Por defeito, `C:\inetpub`este caminho é . Crie o diretório personalizado antes de utilizar este parâmetro.

- `-Uninstall`: Desinstala os sites do portal de ajuda de gestão bitLocker/self-service num servidor web onde foram previamente instalados.


## <a name="run-the-script"></a>Executar o script

No servidor web alvo, faça as seguintes ações:

> [!NOTE]
> Dependendo do design do seu site, poderá ter de executar o script várias vezes. Por exemplo, executar o script no ponto de gestão para instalar o site de administração e monitorização. Em seguida, executá-lo novamente em um servidor web autónomo para instalar o portal de self-service.

1. Copie os `SMSSETUP\BIN\X64` seguintes ficheiros da pasta de instalação do Gestor de Configuração no servidor do site para uma pasta local no servidor alvo:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Executar powerShell como administrador e, em seguida, executar o script semelhante à seguinte linha de comando:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Por exemplo,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > Esta linha de comando de exemplo usa todos os parâmetros possíveis para mostrar o seu uso. Ajuste o seu uso de acordo com os seus requisitos no seu ambiente.

Após a instalação, aceda aos portais através dos seguintes URLs:

- Portal de self-service:`https://webserver.contoso.com/SelfService`
- Site de administração e monitorização:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> A Microsoft recomenda, mas não requer a utilização de HTTPS. Para mais informações, consulte [Como configurar o SSL no IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="verify"></a>Verificar

Monitor e resolução de problemas utilizando os seguintes registos:

- Registos do Windows Event em **Microsoft-Windows-MBAM-Web**. Para mais informações, consulte os registos de [eventos bitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [registos de eventos do Servidor](../../tech-ref/bitlocker/server-event-logs.md).

- Os registos de cada componente encontram-se nos seguintes locais predefinidos:

  - Portal de self-service:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Site de administração e monitorização:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Para obter mais informações sobre resolução de problemas, consulte [Troubleshoot BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Passos seguintes

[Implementar o portal self-service](customize-self-service-portal.md)

Para obter mais informações sobre a utilização dos componentes instalados, consulte os seguintes artigos:

- [Site de administração e monitorização BitLocker](helpdesk-portal.md)
- [Portal de self-service BitLocker](self-service-portal.md)
