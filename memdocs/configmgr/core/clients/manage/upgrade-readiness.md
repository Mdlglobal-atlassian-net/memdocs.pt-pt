---
title: Preparação de Atualizações
titleSuffix: Configuration Manager
description: Integre a prontidão de upgrade com o Gestor de Configuração para aceder aos dados de compatibilidade de upgrade do Windows 10 e dispositivos-alvo para atualização ou reparação.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 18d8b66a7b9f5ad889645cbc8e48ebcbfe6550a9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715047"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrar a prontidão de upgrade com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> O serviço Windows Analytics está reformado a partir de 31 de janeiro de 2020. Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics é a evolução do Windows Analytics. Para mais informações, consulte [o que é desktop Analytics](../../../desktop-analytics/overview.md).

Se o site do Gestor de Configuração tiver uma ligação com a Prontidão de Upgrade, tem de o remover e reconfigurar os clientes.

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a>Remover a ligação de prontidão de upgrade

1. Abra a consola 'Gestor de Configuração' como utilizador com a função **de administrador completo.**

1. Vá ao espaço de trabalho da **Administração,** expanda os **Serviços cloud,** e selecione o nó dos **Serviços Azure.**

1. Elimine o serviço Windows Analytics.

## <a name="reconfigure-clients"></a>Reconfigurar clientes

### <a name="unenroll-devices"></a>Dispositivos de desinscrição

Em primeiro lugar, reveja as definições padrão do site ou quaisquer definições de dispositivo supérrico no grupo **Windows Analytics.** Por exemplo, desative a seguinte definição: Gerir as definições de **telemetria do Windows com o 'Gestor**de Configuração '.

> [!IMPORTANT]
> Se planeia utilizar o Desktop Analytics, ele confunde as definições de dados de diagnóstico do Windows nos clientes. Utilize o assistente de ligação de serviços Azure para configurar estas definições para utilização com desktop Analytics. Para mais informações, consulte [Como ligar o Gestor de Configuração ao Desktop Analytics](../../../desktop-analytics/connect-configmgr.md).

Nos dispositivos matriculados, remova o valor CommercialID das seguintes teclas do Registo windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuração de dados de diagnóstico do Windows

Se não quiser que os seus dispositivos continuem a enviar dados de diagnóstico:

- Windows 10: definir o nível de dados de diagnóstico para **A Segurança**
- Windows 7 SP1 ou 8.1: desativar a **chave de opt-in de dados comerciais**

Desdefinir estes valores utilizando um dos seguintes métodos:

- Política de grupo, na **configuração de computador modelos** > **administrativos** > De recolha de dados de componentes > **windows**e**visualizações**
- Gestão de dispositivos móveis (MDM), como [o Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Quando aplica estas alterações, os dispositivos deixam imediatamente de enviar dados de diagnóstico. Pode levar 24 a 48 horas para a Microsoft parar de processar insights para o seu espaço de trabalho. A Microsoft elimina estes dados dos seus serviços na nuvem dentro de 30 dias ou menos.

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)  
