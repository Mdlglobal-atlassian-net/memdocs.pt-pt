---
title: ApIs de gráfico para configurar dispositivos no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Consulte uma lista de todas as entidades da API graph com o Windows CSP correspondente e compense o URI em dispositivos Windows 10 e mais recentes utilizados na configuração de dispositivos no Microsoft Intune. Consulte a API e o CSP correspondentes para Computadores partilhados, proteção de pontos finais, proteção avançada de ameaças do Microsoft Defender, proteção de identidade, Equipas Windows 10, quiosque e Windows Update para Negócios.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 737301d8171cd123224017a32c03db8365f4a90c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364753"
---
# <a name="graph-apis-and-matching-windows-10-csps-used-in-intune"></a>Graph APIs e CSPs do Windows 10 correspondentes utilizados no Intune

O Microsoft Intune utiliza as [entidades api](https://docs.microsoft.com/graph/api/resources/intune-graph-overview) do Gráfico (abre outro site do Docs) para configurar dispositivos **(Configuração intune** > **Device**) que executam o Windows 10 e mais tarde. O Graph API utiliza fornecedores de serviços de configuração (CSPs) para ler, definir, alterar e/ou eliminar as definições de configuração nos dispositivos.

Esta lista aplica-se a:

- Windows 10 e posterior

Este artigo lista as entidades graph e os seus CSPs do Windows 10 correspondentes e compensam os URIs.

Esta informação é útil para uma variedade de cenários. Por exemplo, veja o que é usado por Intune, consulte as configurações para incluir em configurações oMA-URI personalizadas, e assim por diante. 

## <a name="windows-10-csps"></a>Windows 10 CSPs

Para obter mais informações sobre os prestadores de serviços de configuração do Windows 10, consulte a referência do fornecedor de serviços de [configuração](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference) (abre outro site do Docs).

## <a name="graph-api-properties-to-csp-mapping"></a>Propriedades da API do gráfico para mapeamento CSP

A lista que se segue mostra a maioria das entidades api do Gráfico utilizadas pela Microsoft Intune para a configuração do dispositivo Windows 10. Também mostra o Correspondente Windows 10 CSP e compensa URI.

Para ver as versões do Windows 10 aplicam-se as seguintes APIs, utilize a referência do fornecedor de serviços de [configuração](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference) do Windows 10 (abre outro site do Docs).

### <a name="editionupgradeconfigurationlicense"></a>EditionUpgradeConfiguration.License 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsLicensing  
**Offset URI**: /UpgradeEditionWithLicense

### <a name="editionupgradeconfigurationlicensetype"></a>EditionUpgradeConfiguration.LicenseType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsLicensing  
**Offset URI**: /LicenseKeyType

### <a name="editionupgradeconfigurationproductkey"></a>EditionUpgradeConfiguration.ProductKey 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsLicensing  
**Offset URI**: /UpgradeEdition WithProductKey

### <a name="editionupgradeconfigurationwindowssmode"></a>EditionUpgradeConfiguration.WindowsSMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsLicensing  
**Offset URI**: /SMode/SwitchingPolicy

### <a name="sharedpcconfigurationaccountmanagerpolicy"></a>SharedPCConfiguration.AccountManagerPolicy 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /DeletionPolicy, /DiskLevelCaching, /InactiveThreshold, /DiskLevelDeletion

### <a name="sharedpcconfigurationaccountmanagerpolicy-windows-holographic-for-business-edition-targeted-devices"></a>SharedPCConfiguration.AccountManagerPolicy (Windows Holographic for Business edition targeted devices) 
**CSP**: ./Fornecedor/MSFT/Gestão de Contas  
**Offset URI**: /DeletionPolicy, /StorageCapacityStartDeletion, /StorageCapacityStopDeletion, /ProfileInactivityThreshold

### <a name="sharedpcconfigurationallowedaccounts"></a>SharedPCConfiguration.AllowedAccounts 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /AccountModel

### <a name="sharedpcconfigurationallowlocalstorage"></a>SharedPCConfiguration.AllowLocalStorage 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /Restringir o Armazenamento Local

### <a name="sharedpcconfigurationdisableaccountmanager"></a>SharedPCConfiguration.DisableAccountManager 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /EnableAccountManager

### <a name="sharedpcconfigurationdisableedupolicies"></a>SharedPCConfiguration.DisableEduPolicies 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SetEduPolicies

### <a name="sharedpcconfigurationdisablepowerpolicies"></a>SharedPCConfiguration.DisablePowerPolicies 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SetPowerPolicies

### <a name="sharedpcconfigurationdisablesigninonresume"></a>SharedPCConfiguration.DisableSignInOnResume 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SigninonResume

### <a name="sharedpcconfigurationenabled"></a>SharedPCConfiguration.Enabled 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /EnableSharedPCMode

### <a name="sharedpcconfigurationidletimebeforesleepinseconds"></a>SharedPCConfiguration.IdleTimeBeforeSleepInSeconds 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /InactiveThreshold

### <a name="sharedpcconfigurationkioskappdisplayname"></a>SharedPCConfiguration.KioskAppDisplayName 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /KioskModeUserTileDisplayText

### <a name="sharedpcconfigurationkioskappusermodelid"></a>SharedPCConfiguration.KioskAppUserModelId 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /KioskModeAUMID

### <a name="sharedpcconfigurationlocalstorage"></a>SharedPCConfiguration.LocalStorage 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /Restringir o Armazenamento Local

### <a name="sharedpcconfigurationmaintenancestarttime"></a>SharedPCConfiguration.MaintenanceStartTime 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /MaintenanceStartTime

### <a name="sharedpcconfigurationsetaccountmanager"></a>SharedPCConfiguration.SetAccountManager
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /EnableAccountManager

### <a name="sharedpcconfigurationsetedupolicies"></a>SharedPCConfiguration.SetEduPolicies 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SetEduPolicies

### <a name="sharedpcconfigurationsetpowerpolicies"></a>SharedPCConfiguration.SetPowerPolicies 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SetPowerPolicies

### <a name="sharedpcconfigurationsigninonresume"></a>SharedPCConfiguration.SignInOnResume 
**CSP**: ./Fornecedor/MSFT/SharedPC  
**Offset URI**: /SigninonResume

### <a name="windows10endpointconfigurationsmartscreenblockoverrideforfiles"></a>Windows10endpointconfiguration.smartScreenBlockOverrideForFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/SmartScreen/PreventOverrideForFilesInShell

### <a name="windows10endpointprotectionconfigurationapplicationguardallowfilesaveonhost"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowFileSaveOnHost 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/SaveFilesToHost

### <a name="windows10endpointprotectionconfigurationapplicationguardallowpersistence"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPersistence 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Configurações/Persistência de Permitir

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttolocalprinters"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToLocalPrinters 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/Definições de impressão

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttonetworkprinters"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToNetworkPrinters 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/Definições de impressão

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttopdf"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToPDF 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/Definições de impressão

### <a name="windows10endpointprotectionconfigurationapplicationguardallowprinttoxps"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToXPS 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/Definições de impressão

### <a name="windows10endpointprotectionconfigurationapplicationguardallowvirtualgpu"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardAllowVirtualGPU 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Configurações/AllowVirtualGPU

### <a name="windows10endpointprotectionconfigurationapplicationguardblockclipboardsharing"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardBlockClipboardSharing 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/Definições de clipboard

### <a name="windows10endpointprotectionconfigurationapplicationguardblockfiletransfer"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardBlockFileTransfer 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/ClipboardFileTypeType

### <a name="windows10endpointprotectionconfigurationapplicationguardblocknonenterprisecontent"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardBlockNonEnterpriseContent 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/BlockNonEnterpriseContent

### <a name="windows10endpointprotectionconfigurationapplicationguardenabled"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Definições/AllowWindowsDefenderApplicationGuard

### <a name="windows10endpointprotectionconfigurationapplicationguardforceauditing"></a>Windows10EndpointProtectionConfiguration.ApplicationGuardForceAuditing 
**CSP**: ./Dispositivo/Fornecedor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Audit/AuditApplicationGuard

### <a name="windows10endpointprotectionconfigurationbitlockerallowstandarduserencryption"></a>Windows10EndpointProtectionConfiguration.BitLockerAllowStandardUserEncryption 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /AllowStandardUserEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerdisablewarningforotherdiskencryption"></a>Windows10EndpointProtectionConfiguration.BitLockerDisableWarningForOtherDiskEncryption 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /AllowWarningForOtherDiskCrypton

### <a name="windows10endpointprotectionconfigurationbitlockerenablestoragecardencryptiononmobile"></a>Windows10EndpointProtectionConfiguration.BitLockerEnableStorageCardEncryptionOnMobile 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /RequireStorageCardEncryption

### <a name="windows10endpointprotectionconfigurationbitlockerencryptdevice"></a>Windows10EndpointProtectionConfiguration.BitLockerEncryptDevice 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /RequireDeviceCrypton

### <a name="windows10endpointprotectionconfigurationbitlockerfixeddrivepolicy"></a>Windows10EndpointProtectionConfiguration.BitLockerFixedDrivePolicy 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /FixedDrivesRequireEncryption, /FixedDrivesRecoveryOptions

### <a name="windows10endpointprotectionconfigurationbitlockerremovabledrivepolicy"></a>Windows10EndpointProtectionConfiguration.BitLockerRemovableDrivePolicy 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /RemovableDrivesRequire

### <a name="windows10endpointprotectionconfigurationbitlockersystemdrivepolicy"></a>Windows10EndpointProtectionConfiguration.BitLockerSystemDrivePolicy 
**CSP**: ./Dispositivo/Fornecedor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /SystemDrivesRequireStartupAuthentication, /SystemDrivesMinimumPINLength, /SystemDrivesRecoveryMessage, /SystemDrivesRecoveryRecoveryOptions

### <a name="windows10endpointprotectionconfigurationclientconnectionencryptionlevel"></a>windows10endpointprotectionconfiguration.clientConnectionEncryptionLevel 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/ClientConnectionCryptonLevel

### <a name="windows10endpointprotectionconfigurationconfiguresmbv1clientdriver"></a>windows10endpointprotectionconfiguration.configureSMBV1ClientDriver 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### <a name="windows10endpointprotectionconfigurationconnectivitydownloadingofprintdriversoverhttp"></a>Windows10EndpointProtectionConfiguration.ConnectivityDownloadingOfPrintDriversOverHttp 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/DescarregamentoDeSPrintDriversOverHTTP

### <a name="windows10endpointprotectionconfigurationconnectivityhardeneduncpaths"></a>Windows10EndpointProtectionConfiguration.ConnectivityHardenedUncPaths 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/HardenedUNCPaths

### <a name="windows10endpointprotectionconfigurationconnectivityinternetdownloadforwebpublishingandonlineorderingwizards"></a>Windows10EndpointProtectionConfiguration.ConnectivityInternetDownloadForWebPublishingAndOnlineOrderingWizards 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Connectivity/DisableInternetDownloadForWebPublishing AndOnlineOrderingWizards

### <a name="windows10endpointprotectionconfigurationconnectivityprintingoverhttp"></a>Windows10EndpointProtectionConfiguration.ConnectivityPrintingOverHttp 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/DiablePrintingOverHTTP

### <a name="windows10endpointprotectionconfigurationcredentialsuienumerateadministrators"></a>Windows10EndpointProtectionConfiguration.CredentialsUIEnumerateAdministrators 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/CredentialsUI/EnumerateAdministrators

### <a name="windows10endpointprotectionconfigurationdefenderadditionalguardedfolders"></a>Windows10EndpointProtectionConfiguration.DefenderAdditionalGuardedFolders 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/Defender/ControlledFolderAccessProtectedFolders

### <a name="windows10endpointprotectionconfigurationdefenderadvancedransomewareprotectiontype"></a>Windows10EndpointProtectionConfiguration.DefenderAdvancedRansomewareProtectionType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderattacksurfacereductionexcludedpaths"></a>Windows10EndpointProtectionConfiguration.DefenderAttackSurfaceReductionExcludedPaths 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionOnlyExclusions

### <a name="windows10endpointprotectionconfigurationdefenderemailcontentexecution"></a>Windows10EndpointProtectionConfiguration.DefenderEmailContentExecution 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowEmailScanning

### <a name="windows10endpointprotectionconfigurationdefenderemailcontentexecutiontype"></a>Windows10EndpointProtectionConfiguration.DefenderEmailContentExecutionType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderexploitprotectionxml"></a>Windows10EndpointProtectionConfiguration.DefenderExploitProtectionXml 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/ExploitGuard/ExploitProtectionSettings

### <a name="windows10endpointprotectionconfigurationdefenderexploitprotectionxmlfilename"></a>Windows10EndpointProtectionConfiguration.DefenderExploitProtectionXmlFileName 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/ExploitGuard/ExploitProtectionSettings

### <a name="windows10endpointprotectionconfigurationdefenderguardedfoldersallowedapppaths"></a>Windows10EndpointProtectionConfiguration.DefenderGuardedFoldersAllowedAppPaths 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/Defender/ControlledFolderAccessAllowedApplications

### <a name="windows10endpointprotectionconfigurationdefenderguardmyfolderstype"></a>Windows10EndpointProtectionConfiguration.DefenderGuardMyFoldersType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/EnableControlledFolderAccess

### <a name="windows10endpointprotectionconfigurationdefendernetworkprotectiontype"></a>Windows10EndpointProtectionConfiguration.DefenderNetworkProtectionType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/Defender/EnableNetworkProtection

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsexecutablecontentcreationorlaunch"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsExecutableContentCreationOrLaunch 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsexecutablecontentcreationorlaunchtype"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsExecutableContentCreationOrLaunchType
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderofficeappslaunchchildprocess"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsLaunchChildProcess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappslaunchchildprocesstype"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsLaunchChildProcessType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsotherprocessinjection"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsOtherProcessInjection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficeappsotherprocessinjectiontype"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeAppsOtherProcessInjectionType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType 

### <a name="windows10endpointprotectionconfigurationdefenderofficemacrocodeallowwin32imports"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32Imports 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderofficemacrocodeallowwin32importstype"></a>Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32ImportsType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderpreventcredentialstealingtype"></a>Windows10EndpointProtectionConfiguration.DefenderPreventCredentialStealingType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderprocesscreation"></a>Windows10EndpointProtectionConfiguration.DefenderProcessCreation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderprocesscreationtype"></a>Windows10EndpointProtectionConfiguration.DefenderProcessCreationType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderprotectagainstpotentiallyunwantedapplications"></a>Windows10EndpointProtectionConfiguration.DefenderProtectAgainstPotentiallyUnwantedApplications 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/TurnOnWindowsDefenderProtection AgainstPotentiallyUnwantedApplications

### <a name="windows10endpointprotectionconfigurationdefenderscriptdownloadedpayloadexecution"></a>Windows10EndpointProtectionConfiguration.DefenderScriptDownloadedPayloadExecution 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderscriptdownloadedpayloadexecutiontype"></a>Windows10EndpointProtectionConfiguration.DefenderScriptDownloadedPayloadExecutionType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefenderscriptobfuscatedmacrocode"></a>Windows10EndpointProtectionConfiguration.DefenderScriptObfuscatedMacroCode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderscriptobfuscatedmacrocodetype"></a>Windows10EndpointProtectionConfiguration.DefenderScriptObfuscatedMacroCodeType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterblockexploitprotectionoverride"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterBlockExploitProtectionOverride 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisableaccountui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableAccountUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableAccountProtectionUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisableappbrowserui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableAppBrowserUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableAppBrowserUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablefamilyui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableFamilyUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableFamilyUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablehealthui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableHealthUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableHealthUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablenetworkui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableNetworkUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableNetworkUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablesecurebootui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableSecureBootUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideSecureBoot

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisabletroubleshootingui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableTroubleshootingUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideTPMTroubleshooting

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterdisablevirusui"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableVirusUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableVirusUI

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpemail"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpEmail 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/Email

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpphone"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpPhone 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/Telefone

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterhelpurl"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpURL 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/URL

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenteritcontactdisplay"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterITContactDisplay 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /WindowsDefenderSecurityCenter/EnableCustomizedToasts, /WindowsDefenderSecurityCenter/EnableInAppCustomization

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenternotificationsfromapp"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterNotificationsFromApp 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideWindowsSecurityNotificationAreaControl

### <a name="windows10endpointprotectionconfigurationdefendersecuritycenterorganizationdisplayname"></a>Windows10EndpointProtectionConfiguration.DefenderSecurityCenterOrganizationDisplayName 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/Nome da empresa

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedexecutable"></a>Windows10EndpointProtectionConfiguration.DefenderUntrustedExecutable 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedexecutabletype"></a>Windows10EndpointProtectionConfiguration.DefenderUntrustedExecutableType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedusbprocess"></a>Windows10EndpointProtectionConfiguration.DefenderUntrustedUSBProcess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### <a name="windows10endpointprotectionconfigurationdefenderuntrustedusbprocesstype"></a>Windows10EndpointProtectionConfiguration.DefenderUntrustedUSBProcessType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuração requer propriedades do gráfico: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/ Configuração.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderCredentialStealingType, windows10endpointprotection/ Configuração.defenderNão trustedUSBProcessType

### <a name="windows10endpointprotectionconfigurationdeviceguardenablesecurebootwithdma"></a>Windows10EndpointProtectionConfiguration.DeviceGuardEnableSecureBootWithDMA 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceGuard/RequirePlatformSecurityFeatures

### <a name="windows10endpointprotectionconfigurationdeviceguardenablevirtualizationbasedsecurity"></a>Windows10EndpointProtectionConfiguration.DeviceGuardEnableVirtualizationBasedSecurity 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/DeviceGuard/EnableVirtualizationBasedSecurity

### <a name="windows10endpointprotectionconfigurationdeviceguardlaunchsystemguard"></a>Windows10EndpointProtectionConfiguration.DeviceGuardLaunchSystemGuard 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceGuard/ConfigureSystemGuardLaunch

### <a name="windows10endpointprotectionconfigurationdeviceguardlocalsystemauthoritycredentialguardsettings"></a>Windows10EndpointProtectionConfiguration.DeviceGuardLocalSystemAuthorityCredentialGuardSettings 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceGuard/LsaCfgFlags

### <a name="windows10endpointprotectionconfigurationdmaguarddeviceenumerationpolicy"></a>Windows10EndpointProtectionConfiguration.DmaGuardDeviceEnumerationPolicy 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DmaGuard/DeviceEnumerationPolicy

### <a name="windows10endpointprotectionconfigurationeventlogserviceapplicationlogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration.EventLogServiceApplicationLogMaximumFileSizeInKb 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EventLogService/EspecificarMaximumFileSizeApplicationLog

### <a name="windows10endpointprotectionconfigurationeventlogservicesecuritylogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration.EventLogServiceSecurityLogMaximumFileSizeInKb 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EventLogService/EspecificarMaximumFileSizeSecurityLog

### <a name="windows10endpointprotectionconfigurationeventlogservicesystemlogmaximumfilesizeinkb"></a>Windows10EndpointProtectionConfiguration.EventLogServiceSystemLogMaximumFileSizeInKb 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EventLogService/EspecificarMaximumFileSizeSystemSystemLog

### <a name="windows10endpointprotectionconfigurationexplorerdataexecutionprevention"></a>Windows10EndpointProtectionConfiguration.ExplorerDataExecutionPrevention 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/FileExplorer/TurnOffDataExecutionPreventionForExplorer

### <a name="windows10endpointprotectionconfigurationexplorerheapterminationoncorruption"></a>Windows10EndpointProtectionConfiguration.ExplorerHeapTerminationOnCorruption 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/FileExplorer/TurnOffHeapTerminationOnCorruption

### <a name="windows10endpointprotectionconfigurationfirewallblockstatefulftp"></a>Windows10EndpointProtectionConfiguration.FirewallBlockStatefulFTP 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/DisableStatefulFtp

### <a name="windows10endpointprotectionconfigurationfirewallcertificaterevocationlistcheckmethod"></a>Windows10EndpointProtectionConfiguration.FirewallCertificateRevocationListCheckMethod 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/CRLcheck

### <a name="windows10endpointprotectionconfigurationfirewallidletimeoutforsecurityassociationinseconds"></a>Windows10EndpointProtectionConfiguration.FirewallIdleTimeoutForSecurityAssociationInSeconds 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/SaIdleTime

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowdhcp"></a>Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowDHCP 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowicmp"></a>Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowICMP 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowneighbordiscovery"></a>Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowNeighborDiscovery 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallipsecexemptionsallowrouterdiscovery"></a>Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowRouterDiscovery 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### <a name="windows10endpointprotectionconfigurationfirewallmergekeyingmodulesettings"></a>Windows10EndpointProtectionConfiguration.FirewallMergeKeyingModuleSettings 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/OportunistaMatchAuthSetPerKM

### <a name="windows10endpointprotectionconfigurationfirewallpacketqueueingmethod"></a>Windows10EndpointProtectionConfiguration.FirewallPacketQueueingMethod 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/EnablePacketQueue

### <a name="windows10endpointprotectionconfigurationfirewallpresharedkeyencodingmethod"></a>Windows10EndpointProtectionConfiguration.FirewallPreSharedKeyEncodingMethod 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/PresharedKeyEncoding

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomain"></a>Windows10EndpointProtectionConfiguration.FirewallProfileDomain 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesTo MulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfileDomain.inboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundnotificationsblocked"></a>windows10endpointprotectionconfiguration.firewallProfileDomain.inboundNotificationsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomaininboundnotificationsblocked"></a>windows10endpointprotectionconfiguration.firewallProfileDomain.inboundNotificationsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofiledomainoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfileDomain.outboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivate"></a>Windows10EndpointProtectionConfiguration.FirewallProfilePrivate 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesTo MulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivatefirewallenabled"></a>windows10endpointprotectionconfiguration.firewallProfilePrivate.firewallEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateinboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePrivate.inboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateinboundnotificationsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePrivate.inboundNotificationsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofileprivateoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePrivate.outboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublic"></a>Windows10EndpointProtectionConfiguration.FirewallProfilePublic 
**CSP**: ./Fornecedor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesTo MulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicconnectionsecurityrulesfromgrouppolicymerged"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.connectionSecurityRulesFromGroupPolicyMerged 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/AllowLocalIpsecPolicyMerge

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicfirewallenabled"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.firewallEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/EnableFirewall

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicinboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.inboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DefaultInboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicinboundnotificationsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.inboundNotificationsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DisableInboundNotifications

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicoutboundconnectionsblocked"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.outboundConnectionsBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DefaultOutboundAction

### <a name="windows10endpointprotectionconfigurationfirewallprofilepublicpolicyrulesfromgrouppolicymerged"></a>windows10endpointprotectionconfiguration.firewallProfilePublic.policyRulesFromGroupPolicyMerged 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/AllowLocalPolicyMerge

### <a name="windows10endpointprotectionconfigurationlanmanagerauthenticationlevel"></a>Windows10EndpointProtectionConfiguration.LanManagerAuthenticationLevel 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_LANManagerAuthenticationLevel

### <a name="windows10endpointprotectionconfigurationlanmanagerworkstationdisableinsecureguestlogons"></a>Windows10EndpointProtectionConfiguration.LanManagerWorkstationDisableInsecureGuestLogons 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LanmanWorkstation/EnableInsecureGuestLogons

### <a name="windows10endpointprotectionconfigurationlanmanagerworkstationenableinsecureguestlogons"></a>Windows10EndpointProtectionConfiguration.LanManagerWorkstationEnableInsecureGuestLogons 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LanmanWorkstation/EnableInsecureGuestLogons

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsadministratoraccountname"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorAccountName 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Políticas LocaisSegurançaOpções/Contas\_RenomeAdministratorAccount

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsadministratorelevationpromptbehavior"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorElevationPromptBehavior
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_BehaviorOfTheElevationPromptForAdministrators

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowanonymousenumerationofsamaccountsandshares"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowAnonymousEnumerationOfSAMAccountsAndShares 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowpku2uauthenticationrequests"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowPKU2UAuthenticationRequests 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_AllowPKU2UAutenticaçãoRequests

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowremotecallstosecurityaccountsmanager"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowRemoteCallsToSecurityAccountsManager 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictCustomersAllowedToMakeRemoteCallsToSAM

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowremotecallstosecurityaccountsmanagerhelperbool"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowRemoteCallsToSecurityAccountsManagerHelperBool 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictCustomersAllowedToMakeRemoteCallsToSAM

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowsystemtobeshutdownwithouthavingtologon"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowSystemToBeShutDownWithoutHavingToLogOn 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Shutdown\_AllowSystemToBeShutDown withoutHavingToLogOn

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowuiaccessapplicationelevation"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUIAccessApplicationElevation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Políticas LocaisSecurityOptions/UserAccountControl\_AllowUIAccessApplicationsToPromptForElevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowuiaccessapplicationsforsecurelocations"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUIAccessApplicationsForSecureLocations 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsallowundockwithouthavingtologon"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUndockWithoutHavingToLogon 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_AllowUndock WithoutHavingToLogon

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockmicrosoftaccounts"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockMicrosoftAccounts 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_BlockMicrosoftAccounts

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockremotelogonwithblankpassword"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockRemoteLogonWithBlankPassword 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockremoteopticaldriveaccess"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockRemoteOpticalDriveAccess 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_RestrictCDROMAccessToLocallyLoggedOnUserOnly

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsblockusersinstallingprinterdrivers"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockUsersInstallingPrinterDrivers 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_PreventUsersFromInstallIngDriversWhenConnecttoSharedPrinters

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclearvirtualmemorypagefile"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClearVirtualMemoryPageFile 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Shutdown\_ClearVirtualMemoryPageFile

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclientdigitallysigncommunicationsalways"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClientDigitallySignCommunicationsAlways 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_DigitallySignCommunicationsAlways

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsclientsendunencryptedpasswordtothirdpartysmbservers"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClientSendUnencryptedPasswordToThirdPartySMBServers 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_SendUnencryptedPasswordToThirdPartySMBServers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdetectapplicationinstallationsandpromptforelevation"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDetectApplicationInstallationsAndPromptForElevation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_DetectApplicationInstallationsAndPromptForElevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableadministratoraccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableAdministratorAccount 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableAdministratorAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableclientdigitallysigncommunicationsifserveragrees"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableClientDigitallySignCommunicationsIfServerAgrees 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_DigitallySignCommunicationsIfServerAgrees

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableguestaccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableGuestAccount 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableGuestAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableserverdigitallysigncommunicationsalways"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableServerDigitallySignCommunicationsAlways 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer\_DigitallySignCommunicationsAlways

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdisableserverdigitallysigncommunicationsifclientagrees"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableServerDigitallySignCommunicationsIfClientAgrees 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer\_DigitallySignCommunicationsIfClientAgrees

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotallowanonymousenumerationofsamaccounts"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotAllowAnonymousEnumerationOfSAMAccounts 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_DoNotAllowAnonymousEnumerationOfSAMAccounts

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotrequirectrlaltdel"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotRequireCtrlAltDel 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotRequireCTRLALTDEL

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsdonotstorelanmanagerhashvalueonnextpasswordchange"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotStoreLANManagerHashValueOnNextPasswordChange 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_DoNotStoreLANManagerHashValueOnNextPasswordChange

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsenableadministratoraccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsEnableAdministratorAccount 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableAdministratorAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsenableguestaccount"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsEnableGuestAccount 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableGuestAccountStatus

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsformatandejectofremovablemediaalloweduser"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsFormatAndEjectOfRemovableMediaAllowedUser 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_AllowedToFormatAndEjectRemovableMedia

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsguestaccountname"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsGuestAccountName 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_RenameGuestAccount

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionshidelastsignedinuser"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsHideLastSignedInUser 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotDisplayLastSignedIn

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionshideusernameatsignin"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsHideUsernameAtSignIn 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotDisplayUsernameAtSignIn

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsinformationdisplayedonlockscreen"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsInformationDisplayedOnLockScreen 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DisplayUserInformation WhenTheSessionIsLocked

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsinformationshownonlockscreen"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsInformationShownOnLockScreen 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DisplayUserInformation WhenTheSessionIsLocked

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionslogonmessagetext"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsLogOnMessageText 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MessageTextForUsers AttempttoLogOn

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionslogonmessagetitle"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsLogOnMessageTitle 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MessageTitleForUsersAttemptToLogOn

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsmachineinactivitylimit"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMachineInactivityLimit 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MachineInactivityLimit

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsmachineinactivitylimitinminutes"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMachineInactivityLimitInMinutes 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MachineInactivityLimit

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsminimumsessionsecurityforntlmsspbasedclients"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMinimumSessionSecurityForNtlmSspBasedClients 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_MinimumSessionSecurityForNTLMSSPBasedClients

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsminimumsessionsecurityforntlmsspbasedservers"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMinimumSessionSecurityForNtlmSspBasedServers 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_MinimumSessionSecurityForNTLMSSPBasedServers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsonlyelevatesignedexecutables"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsOnlyElevateSignedExecutables 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Políticas locaisSegurançaOpções/UserAccountControl\_OnlyElevateExecutableFiles That AreSignedAndValidad

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsrestrictanonymousaccesstonamedpipesandshares"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsRestrictAnonymousAccessToNamedPipesAndShares 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictAnonymousAccessToNamedPipesAndShares

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionssmartcardremovalbehavior"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsSmartCardRemovalBehavior 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_SmartCardRemovalBehavior

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsstandarduserelevationpromptbehavior"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsStandardUserElevationPromptBehavior 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/User AccountControl\_BehavioroftheElevationpromptforStandardusers

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsswitchtosecuredesktopwhenpromptingforelevation"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsSwitchToSecureDesktopWhenPromptingForElevation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_SwitchtotheSecuredesktop Whenpromptingpromptingforelevation

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsuseadminapprovalmode"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsUseAdminApprovalMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_UseAdminApprovalMode

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsuseadminapprovalmodeforadministrators"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsUseAdminApprovalModeForAdministrators 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_RunAllAdministratorsInAdminApprovalMode

### <a name="windows10endpointprotectionconfigurationlocalsecurityoptionsvirtualizefileandregistrywritefailurestoperuserlocations"></a>Windows10EndpointProtectionConfiguration.LocalSecurityOptionsVirtualizeFileAndRegistryWriteFailuresToPerUserLocations 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations

### <a name="windows10endpointprotectionconfigurationnetworkicmpredirectsoverrideospfgeneratedroutes"></a>Windows10EndpointProtectionConfiguration.NetworkIcmpRedirectsOverrideOspfGeneratedRoutes 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSLegacy/AllowICMPRedirectsToOverrideOSPFGeneratedRoutes

### <a name="windows10endpointprotectionconfigurationnetworkignorenetbiosnamereleaserequestsexceptfromwinsservers"></a>Windows10EndpointProtectionConfiguration.NetworkIgnoreNetBiosNameReleaseRequestsExceptFromWinsServers 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSLegacy/AllowTheComputerToIgnoreNetBIOSNameReleaseRequestsExceptFromWINSServers

### <a name="windows10endpointprotectionconfigurationnetworkipsourceroutingprotectionlevel"></a>Windows10EndpointProtectionConfiguration.NetworkIpSourceRoutingProtectionLevel 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSLegacy/IPSourceRoutingProtectionLevel

### <a name="windows10endpointprotectionconfigurationnetworkipv6sourceroutingprotectionlevel"></a>Windows10EndpointProtectionConfiguration.NetworkIpV6SourceRoutingProtectionLevel 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSLegacy/IPv6SourceIngProtectionLevel

### <a name="windows10endpointprotectionconfigurationpasswordpinlogon"></a>Windows10EndpointProtectionConfiguration.PasswordPinLogOn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/CredenciaisProviders/AllowPINLogon

### <a name="windows10endpointprotectionconfigurationpowershellshellscriptblocklogging"></a>Windows10EndpointProtectionConfiguration.PowerShellShellScriptBlockLogging 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsPowerShell/TurnOnPowerShellScriptBlockLogging

### <a name="windows10endpointprotectionconfigurationremoteassistancesolicitedsetting"></a>Windows10EndpointProtectionConfiguration.RemoteAssistanceSolicitedSetting 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/HardenedUNCPaths

### <a name="windows10endpointprotectionconfigurationremotedesktopservicesclientconnectionencryptionlevel"></a>Windows10EndpointProtectionConfiguration.RemoteDesktopServicesClientConnectionEncryptionLevel 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/ClientConnectionCryptonLevel

### <a name="windows10endpointprotectionconfigurationremotedesktopservicesdriveredirection"></a>Windows10EndpointProtectionConfiguration.RemoteDesktopServicesDriveRedirection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/DoNotAllowDriveRedirection

### <a name="windows10endpointprotectionconfigurationremotedesktopservicespasswordsaving"></a>Windows10EndpointProtectionConfiguration.RemoteDesktopServicesPasswordSaving 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/DoNotAllowPasswordSaving

### <a name="windows10endpointprotectionconfigurationremotedesktopservicespromptforpassworduponconnection"></a>Windows10EndpointProtectionConfiguration.RemoteDesktopServicesPromptForPasswordUponConnection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/PromptForPasswordUponConnection

### <a name="windows10endpointprotectionconfigurationremotedesktopservicessecurerpccommunication"></a>Windows10EndpointProtectionConfiguration.RemoteDesktopServicesSecureRpcCommunication 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteDesktopServices/RequireSecureRPCCommunication

### <a name="windows10endpointprotectionconfigurationremotehostdelegationofnonexportablecredentials"></a>Windows10EndpointProtectionConfiguration.RemoteHostDelegationOfNonExportableCredentials 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/CredenciaisDelegação/Anfitrião RemotoAllowsDelegações De Credenciais Não Exportáveis

### <a name="windows10endpointprotectionconfigurationremotemanagementclientbasicauthentication"></a>Windows10EndpointProtectionConfiguration.RemoteManagementClientBasicAuthentication 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/AllowBasicAuthentication\_Client

### <a name="windows10endpointprotectionconfigurationremotemanagementclientdigestauthentication"></a>Windows10EndpointProtectionConfiguration.RemoteManagementClientDigestAuthentication 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/DisallowDigestAuthentication

### <a name="windows10endpointprotectionconfigurationremotemanagementclientunencryptedtraffic"></a>Windows10EndpointProtectionConfiguration.RemoteManagementClientUnencryptedTraffic 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/AllowUnencryptedTraffic\_Client

### <a name="windows10endpointprotectionconfigurationremotemanagementservicebasicauthentication"></a>Windows10EndpointProtectionConfiguration.RemoteManagementServiceBasicAuthentication 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/AllowBasicAuthentication\_Service

### <a name="windows10endpointprotectionconfigurationremotemanagementservicestoringrunascredentials"></a>Windows10EndpointProtectionConfiguration.RemoteManagementServiceStoringRunAsCredentials 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/DisallowStoringOfRunAsCredentials

### <a name="windows10endpointprotectionconfigurationremotemanagementserviceunencryptedtraffic"></a>Windows10EndpointProtectionConfiguration.RemoteManagementServiceUnencryptedTraffic 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteManagement/AllowUnencryptedTraffic\_Service

### <a name="windows10endpointprotectionconfigurationrpcunauthenticatedclientoptions"></a>Windows10EndpointProtectionConfiguration.RpcUnauthenticatedClientOptions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteProcedureCall/RestrictUnauthenticedRPCClients

### <a name="windows10endpointprotectionconfigurationsecurityguideapplyuacrestrictionstolocalaccountsonnetworklogon"></a>Windows10EndpointProtectionConfiguration.SecurityGuideApplyUacRestrictionsToLocalAccountsOnNetworkLogon 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/ApplyUACRestrictionsToLocalAccountsOnNetworkLogon

### <a name="windows10endpointprotectionconfigurationsecurityguidesmbv1clientdriverstartconfiguration"></a>Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1ClientDriverStartConfiguration 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### <a name="windows10endpointprotectionconfigurationsecurityguidesmbv1server"></a>Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1Server 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1Server

### <a name="windows10endpointprotectionconfigurationsecurityguidestructuredexceptionhandlingoverwriteprotection"></a>Windows10EndpointProtectionConfiguration.SecurityGuideStructuredExceptionHandlingOverwriteProtection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/EnableStructuredExceptionHandlingOverwriteProtection

### <a name="windows10endpointprotectionconfigurationsecurityguidewdigestauthentication"></a>Windows10EndpointProtectionConfiguration.SecurityGuideWDigestAuthentication 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/MSSecurityGuide/WDigestAuthentication

### <a name="windows10endpointprotectionconfigurationsmartscreenblockoverrideforfiles"></a>Windows10EndpointProtectionConfiguration.SmartScreenBlockOverrideForFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/DeviceGuard/RequirePlatformSecurityFeatures

### <a name="windows10endpointprotectionconfigurationsmartscreenenableinshell"></a>Windows10EndpointProtectionConfiguration.SmartScreenEnableInShell 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/SmartScreen/EnableSmartScreenInShell

### <a name="windows10endpointprotectionconfigurationsolicitedremoteassistance"></a>windows10endpointprotectionconfiguration.solicitedRemoteAssistance 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/RemoteAssistance/SolicitedRemoteAssistance

### <a name="windows10endpointprotectionconfigurationuserrightsaccesscredentialmanagerastrustedcaller"></a>Windows10EndpointProtectionConfiguration.UserRightsAccessCredentialManagerAsTrustedCaller 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/AccessCredentialManagerAsTrustedCaller

### <a name="windows10endpointprotectionconfigurationuserrightsaccessfromnetwork"></a>windows10EndpointProtectionConfiguration.UserRightsAccessFromNetwork 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/AccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsactaspartoftheoperatingsystem"></a>Windows10EndpointProtectionConfiguration.userRightsActAsPartOfTheOperatingSystem 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ActAspartofTheOperatingSystem

### <a name="windows10endpointprotectionconfigurationuserrightsallowaccessfromnetwork"></a>Windows10EndpointProtectionConfiguration.UserRightsAllowAccessFromNetwork 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/AccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsbackupdata"></a>Windows10EndpointProtectionConfiguration.UserRightsBackupData 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/BackupFilesAndDirectories

### <a name="windows10endpointprotectionconfigurationuserrightsblockaccessfromnetwork"></a>Windows10EndpointProtectionConfiguration.UserRightsBlockAccessFromNetwork 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/DenyAccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightschangesystemtime"></a>Windows10EndpointProtectionConfiguration.UserRightsChangeSystemTime 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ChangeSystemTime

### <a name="windows10endpointprotectionconfigurationuserrightscreateglobalobjects"></a>Windows10EndpointProtectionConfiguration.UserRightsCreateGlobalObjects 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/CreateGlobalObjects

### <a name="windows10endpointprotectionconfigurationuserrightscreatepagefile"></a>Windows10EndpointProtectionConfiguration.UserRightsCreatePageFile 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/CreatePageFile

### <a name="windows10endpointprotectionconfigurationuserrightscreatepermanentsharedobjects"></a>Windows10EndpointProtectionConfiguration.UserRightsCreatePermanentSharedObjects 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/CreatePermanentSharedObjects

### <a name="windows10endpointprotectionconfigurationuserrightscreatesymboliclinks"></a>Windows10EndpointProtectionConfiguration.UserRightsCreateSymbolicLinks 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/CreateSymbolicLinks

### <a name="windows10endpointprotectionconfigurationuserrightscreatetoken"></a>Windows10EndpointProtectionConfiguration.UserRightsCreateToken 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/CreateToken

### <a name="windows10endpointprotectionconfigurationuserrightsdebugprograms"></a>Windows10EndpointProtectionConfiguration.UserRightsDebugPrograms 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/DebugPrograms

### <a name="windows10endpointprotectionconfigurationuserrightsdelegation"></a>Windows10EndpointProtectionConfiguration.UserRightsDelegation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/EnableDelega

### <a name="windows10endpointprotectionconfigurationuserrightsdenyaccessfromnetwork"></a>windows10EndpointProtectionConfiguration.UserRightsDenyAccessFromNetwork 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/DenyAccessFromNetwork

### <a name="windows10endpointprotectionconfigurationuserrightsgeneratesecurityaudits"></a>Windows10EndpointProtectionConfiguration.UserRightsGenerateSecurityAudits 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/GenerateSecurityAudits

### <a name="windows10endpointprotectionconfigurationuserrightsimpersonateclient"></a>Windows10EndpointProtectionConfiguration.UserRightsImpersonateClient 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ImpersonateClient

### <a name="windows10endpointprotectionconfigurationuserrightsincreaseschedulingpriority"></a>Windows10EndpointProtectionConfiguration.UserRightsIncreaseSchedulingPriority 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/Aumentar A Prioridade de Agendamento

### <a name="windows10endpointprotectionconfigurationuserrightsloadunloaddrivers"></a>Windows10EndpointProtectionConfiguration.UserRightsLoadUnloadDrivers 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/LoadUnloadDeviceDrivers

### <a name="windows10endpointprotectionconfigurationuserrightslocallogon"></a>Windows10EndpointProtectionConfiguration.UserRightsLocalLogOn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/AllowLocalLogOn

### <a name="windows10endpointprotectionconfigurationuserrightslockmemory"></a>Windows10EndpointProtectionConfiguration.UserRightsLockMemory 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/LockMemory

### <a name="windows10endpointprotectionconfigurationuserrightsmanageauditingandsecuritylogs"></a>Windows10EndpointProtectionConfiguration.UserRightsManageAuditingAndSecurityLogs 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ManageAuditingAndSecurityLog

### <a name="windows10endpointprotectionconfigurationuserrightsmanagevolumes"></a>Windows10EndpointProtectionConfiguration.UserRightsManageVolumes 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ManageVolume

### <a name="windows10endpointprotectionconfigurationuserrightsmodifyfirmwareenvironment"></a>Windows10EndpointProtectionConfiguration.UserRightsModifyFirmwareEnvironment 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ModificarFirmwareEnvironment

### <a name="windows10endpointprotectionconfigurationuserrightsmodifyobjectlabels"></a>Windows10EndpointProtectionConfiguration.UserRightsModifyObjectLabels 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ModificarObjectLabel

### <a name="windows10endpointprotectionconfigurationuserrightsprofilesingleprocess"></a>Windows10EndpointProtectionConfiguration.UserRightsProfileSingleProcess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/ProfileSingleProcess

### <a name="windows10endpointprotectionconfigurationuserrightsregisterprocessasservice"></a>Windows10EndpointProtectionConfiguration.UserRightsRegisterProcessAsService 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/DenyLocalLogOn

### <a name="windows10endpointprotectionconfigurationuserrightsremotedesktopserviceslogon"></a>Windows10EndpointProtectionConfiguration.UserRightsRemoteDesktopServicesLogOn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/DenyRemoteDesktopServicesLogOn

### <a name="windows10endpointprotectionconfigurationuserrightsremoteshutdown"></a>Windows10EndpointProtectionConfiguration.UserRightsRemoteShutdown 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/RemoteShutdown

### <a name="windows10endpointprotectionconfigurationuserrightsrestoredata"></a>Windows10EndpointProtectionConfiguration.UserRightsRestoreData 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/RestoreFilesAndDirectories

### <a name="windows10endpointprotectionconfigurationuserrightstakeownership"></a>Windows10EndpointProtectionConfiguration.UserRightsTakeOwnership 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/UserRights/TakeOwnership

### <a name="windows10endpointprotectionconfigurationwindowsconnectionmanagerconnectiontonondomainnetworks"></a>Windows10EndpointProtectionConfiguration.WindowsConnectionManagerConnectionToNonDomainNetworks 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsConnectionManager/ProhitConnectionToNonDomainNetworksWhenConnectedToDomainAuthenticedNetwork

### <a name="windows10endpointprotectionconfigurationwindowslogonsigninlastinteractiveuseraftersysteminitiatedrestart"></a>Windows10EndpointProtectionConfiguration.WindowsLogOnSignInLastInteractiveUserAfterSystemInitiatedRestart 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsLogon/SignInLastInteractiveUserUserAutomaticamenteAfterASystemIniciado

### <a name="windows10endpointprotectionconfigurationxboxservicesaccessorymanagementservicestartupmode"></a>Windows10EndpointProtectionConfiguration.XboxServicesAccessoryManagementServiceStartupMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/SystemServices/ConfigureXboxAccessoryManagementServiceModo

### <a name="windows10endpointprotectionconfigurationxboxservicesenablexboxgamesavetask"></a>Windows10EndpointProtectionConfiguration.XboxServicesEnableXboxGameSaveTask 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/TaskScheduler/EnableXboxGameSaveTask

### <a name="windows10endpointprotectionconfigurationxboxservicesliveauthmanagerservicestartupmode"></a>Windows10EndpointProtectionConfiguration.XboxServicesLiveAuthManagerServiceStartupMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode

### <a name="windows10endpointprotectionconfigurationxboxserviceslivegamesaveservicestartupmode"></a>Windows10EndpointProtectionConfiguration.XboxServicesLiveGameSaveServiceStartupMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/SystemServices/XboxServicesLiveGameSaveServiceModo

### <a name="windows10endpointprotectionconfigurationxboxserviceslivenetworkingservicestartupmode"></a>Windows10EndpointProtectionConfiguration.XboxServicesLiveNetworkingServiceStartupMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode

### <a name="windows10enterprisemodernappmanagementconfigurationuninstallbuiltinapps"></a>Windows10EnterpriseModernAppManagementConfiguration.UninstallBuiltInApps
**CSP**: N/A Gráfico API chamada apenas **Offset URI**: N/A Gráfico API chamada apenas

### <a name="windows10generalconfigurationaccountsblockaddingnonmicrosoftaccountemail"></a>Windows10GeneralConfiguration.AccountsBlockAddingNonMicrosoftAccountEmail 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Accounts/AllowAddingNonMicrosoftAccountsManualmente

### <a name="windows10generalconfigurationantitheftmodeblocked"></a>Windows10GeneralConfiguration.AntiTheftModeBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/AntiTheftMode

### <a name="windows10generalconfigurationappmanagementmsiallowusercontroloverinstall"></a>Windows10GeneralConfiguration.AppManagementMSIAllowUserControlOverInstall 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/MSIAllowUserUserControlOverInstall

### <a name="windows10generalconfigurationappmanagementmsialwaysinstallwithelevatedprivileges"></a>Windows10GeneralConfiguration.AppManagementMSIAlwaysInstallWithElevatedPrivileges 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges

### <a name="windows10generalconfigurationappsallowtrustedappssideloading"></a>Windows10GeneralConfiguration.AppsAllowTrustedAppsSideloading 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowAllTrustApps

### <a name="windows10generalconfigurationappsblockwindowsstoreoriginatedapps"></a>Windows10GeneralConfiguration.AppsBlockWindowsStoreOriginatedApps 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/DisableStoreOrigindApps

### <a name="windows10generalconfigurationappsmicrosoftaccountsoptional"></a>Windows10GeneralConfiguration.AppsMicrosoftAccountsOptional 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/AppRuntime/AllowMicrosoftAccountsToBeOptional

### <a name="windows10generalconfigurationassignedaccessmultimodeprofiles"></a>Windows10GeneralConfiguration.AssignedAccessMultiModeProfiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Acesso Atribuído  
**Offset URI**: /Configuração

### <a name="windows10generalconfigurationassignedaccesssinglemodeappusermodelid"></a>Windows10GeneralConfiguration.AssignedAccessSingleModeAppUserModelId 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Acesso Atribuído  
**Offset URI**: /Configuração

### <a name="windows10generalconfigurationassignedaccesssinglemodeusername"></a>Windows10GeneralConfiguration.AssignedAccessSingleModeUserName 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Acesso Atribuído  
**Offset URI**: /Configuração

### <a name="windows10generalconfigurationauthenticationallowfidodevice"></a>Windows10GeneralConfiguration.AuthenticationAllowFIDODevice 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autenticação/AllowFidoDeviceSignon

### <a name="windows10generalconfigurationauthenticationallowsecondarydevice"></a>Windows10GeneralConfiguration.AuthenticationAllowSecondaryDevice 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autenticação/AllowSecondAuthenticationDevice

### <a name="windows10generalconfigurationauthenticationpreferredazureadtenantdomainname"></a>Windows10GeneralConfiguration.AuthenticationPreferredAzureADTenantDomainName 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autenticação/PreferredAadTenantDomainName

### <a name="windows10generalconfigurationauthenticationwebsignin"></a>Windows10GeneralConfiguration.AuthenticationWebSignIn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autenticação/EnableWebSignIn

### <a name="windows10generalconfigurationautoplaydefaultautorunbehavior"></a>Windows10GeneralConfiguration.AutoPlayDefaultAutoRunBehavior 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autoplay/SetDefaultAutoRunBehavior

### <a name="windows10generalconfigurationautoplayfornonvolumedevices"></a>Windows10GeneralConfiguration.AutoPlayForNonVolumeDevices 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autoplay/DisallowAutoplayForNonVolumeDevices

### <a name="windows10generalconfigurationautoplaymode"></a>Windows10GeneralConfiguration.AutoPlayMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Autoplay/TurnOffAutoPlay

### <a name="windows10generalconfigurationbluetoothallowedservices"></a>Windows10GeneralConfiguration.BluetoothAllowedServices 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/ServicesAllowedList

### <a name="windows10generalconfigurationbluetoothblockadvertising"></a>Windows10GeneralConfiguration.BluetoothBlockAdvertising 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/AllowAdvertising

### <a name="windows10generalconfigurationbluetoothblockdiscoverablemode"></a>Windows10GeneralConfiguration.BluetoothBlockDiscoverableMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/AllowDiscoverAbleMode

### <a name="windows10generalconfigurationbluetoothblocked"></a>Windows10GeneralConfiguration.BluetoothBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowBluetooth

### <a name="windows10generalconfigurationbluetoothblockprepairing"></a>Windows10GeneralConfiguration.BluetoothBlockPrePairing 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/AllowPrepairing

### <a name="windows10generalconfigurationbluetoothblockpromptedproximalconnections"></a>Windows10GeneralConfiguration.BluetoothBlockPromptedProximalConnections 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/AllowPromptPromptedProximalConnections

### <a name="windows10generalconfigurationbluetoothdevicename"></a>Windows10GeneralConfiguration.BluetoothDeviceName 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Bluetooth/LocalDeviceName

### <a name="windows10generalconfigurationbootstartdriverinitialization"></a>windows10generalconfiguration.bootStartDriverInitialization 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/BootStartDriverInitialization

### <a name="windows10generalconfigurationcamerablocked"></a>Windows10GeneralConfiguration.CameraBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Camera/AllowCamera

### <a name="windows10generalconfigurationcellularblockdatawhenroaming"></a>Windows10GeneralConfiguration.CellularBlockDataWhenRoaming 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowCellularDataRoaming

### <a name="windows10generalconfigurationcellularblockvpn"></a>Windows10GeneralConfiguration.CellularBlockVpn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowVPNOverCellular

### <a name="windows10generalconfigurationcellularblockvpnwhenroaming"></a>Windows10GeneralConfiguration.CellularBlockVpnWhenRoaming 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowVPNRoamingOverCellular

### <a name="windows10generalconfigurationcellulardata"></a>Windows10GeneralConfiguration.CellularData 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowCellularData

### <a name="windows10generalconfigurationcertificatesblockmanualrootcertificateinstallation"></a>Windows10GeneralConfiguration.CertificatesBlockManualRootCertificateInstallation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/AllowManualRootCertificateInstallation

### <a name="windows10generalconfigurationconnecteddevicesserviceblocked"></a>Windows10GeneralConfiguration.ConnectedDevicesServiceBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowConnectedDevices

### <a name="windows10generalconfigurationcopypasteblocked"></a>Windows10GeneralConfiguration.CopyPasteBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowCopyPaste

### <a name="windows10generalconfigurationcortanablocked"></a>Windows10GeneralConfiguration.CortanaBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/AboveLock/AllowCortanaAboveLock

### <a name="windows10generalconfigurationcryptographyallowfipsalgorithmpolicy"></a>Windows10GeneralConfiguration.CryptographyAllowFipsAlgorithmPolicy 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Cryptografia/AllowFipsAlgorithmPolicy

### <a name="windows10generalconfigurationdataprotectionblockdirectmemoryaccess"></a>Windows10GeneralConfiguration.DataProtectionBlockDirectMemoryAccess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DataProtection/AllowDirectMemoryAccess

### <a name="windows10generalconfigurationdefenderblockenduseraccess"></a>Windows10GeneralConfiguration.DefenderBlockEndUserAccess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowUserUIAccess

### <a name="windows10generalconfigurationdefenderblockonaccessprotection"></a>Windows10GeneralConfiguration.DefenderBlockOnAccessProtection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowOnAccessProtection

### <a name="windows10generalconfigurationdefendercloudblocklevel"></a>Windows10GeneralConfiguration.DefenderCloudBlockLevel 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/CloudBlockLevel

### <a name="windows10generalconfigurationdefendercloudextendedtimeout"></a>Windows10GeneralConfiguration.DefenderCloudExtendedTimeout 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/CloudExtendedTimeout

### <a name="windows10generalconfigurationdefendercloudextendedtimeoutinseconds"></a>Windows10GeneralConfiguration.DefenderCloudExtendedTimeoutInSeconds 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/CloudExtendedTimeout

### <a name="windows10generalconfigurationdefenderdaysbeforedeletingquarantinedmalware"></a>Windows10GeneralConfiguration.DefenderDaysBeforeDeletingQuarantinedMalware 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/DaysToRetainCleanedMalware

### <a name="windows10generalconfigurationdefenderdetectedmalwareactions"></a>Windows10GeneralConfiguration.DefenderDetectedMalwareActions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ThreatSeverityDefaultAction

### <a name="windows10generalconfigurationdefenderfileextensionstoexclude"></a>Windows10GeneralConfiguration.DefenderFileExtensionsToExclude 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ExclusedExtensions

### <a name="windows10generalconfigurationdefenderfilesandfolderstoexclude"></a>Windows10GeneralConfiguration.DefenderFilesAndFoldersToExclude 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ExclusedPaths

### <a name="windows10generalconfigurationdefendermonitorfileactivity"></a>Windows10GeneralConfiguration.DefenderMonitorFileActivity 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowRealTimeMonitoring

### <a name="windows10generalconfigurationdefenderpotentiallyunwantedappaction"></a>Windows10GeneralConfiguration.DefenderPotentiallyUnwantedAppAction 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/PUAProtection

### <a name="windows10generalconfigurationdefenderpotentiallyunwantedappactionsetting"></a>Windows10GeneralConfiguration.DefenderPotentiallyUnwantedAppActionSetting 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/PUAProtection

### <a name="windows10generalconfigurationdefenderprocessestoexclude"></a>Windows10GeneralConfiguration.DefenderProcessesToExclude 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/Excluídos Processos

### <a name="windows10generalconfigurationdefenderpromptforsamplesubmission"></a>Windows10GeneralConfiguration.DefenderPromptForSampleSubmission 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/SubmitSamplesConsent

### <a name="windows10generalconfigurationdefenderrequirebehaviormonitoring"></a>Windows10GeneralConfiguration.DefenderRequireBehaviorMonitoring 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowBehaviorMonitoring

### <a name="windows10generalconfigurationdefenderrequirecloudprotection"></a>Windows10GeneralConfiguration.DefenderRequireCloudProtection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowCloudProtection

### <a name="windows10generalconfigurationdefenderrequirenetworkinspectionsystem"></a>Windows10GeneralConfiguration.DefenderRequireNetworkInspectionSystem 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowIntrusionPreventionSystemSystem

### <a name="windows10generalconfigurationdefenderrequirerealtimemonitoring"></a>Windows10GeneralConfiguration.DefenderRequireRealTimeMonitoring 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowRealTimeMonitoring

### <a name="windows10generalconfigurationdefenderscanarchivefiles"></a>Windows10GeneralConfiguration.DefenderScanArchiveFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowArchiveScanning

### <a name="windows10generalconfigurationdefenderscandownloads"></a>Windows10GeneralConfiguration.DefenderScanDownloads 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowIOAVProtection

### <a name="windows10generalconfigurationdefenderscanincomingmail"></a>Windows10GeneralConfiguration.DefenderScanIncomingMail 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowScanningNetworkFiles

### <a name="windows10generalconfigurationdefenderscanmappednetworkdrivesduringfullscan"></a>Windows10GeneralConfiguration.DefenderScanMappedNetworkDrivesDuringFullScan 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowFullScanOnMappedNetworkDrives

### <a name="windows10generalconfigurationdefenderscanmaxcpu"></a>Windows10GeneralConfiguration.DefenderScanMaxCpu 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AvgCPULoadFactor

### <a name="windows10generalconfigurationdefenderscannetworkfiles"></a>Windows10GeneralConfiguration.DefenderScanNetworkFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowScanningNetworkFiles

### <a name="windows10generalconfigurationdefenderscanremovabledrivesduringfullscan"></a>Windows10GeneralConfiguration.DefenderScanRemovableDrivesDuringFullScan 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowFullScanRemovableDriveScanning

### <a name="windows10generalconfigurationdefenderscanscriptsloadedininternetexplorer"></a>Windows10GeneralConfiguration.DefenderScanScriptsLoadedInInternetExplorer 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/AllowScriptScanning

### <a name="windows10generalconfigurationdefenderscantype"></a>Windows10GeneralConfiguration.DefenderScanType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ScanParameter

### <a name="windows10generalconfigurationdefenderscheduledquickscantime"></a>Windows10GeneralConfiguration.DefenderScheduledQuickScanTime 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ScheduleQuickScanTime

### <a name="windows10generalconfigurationdefenderscheduledscantime"></a>Windows10GeneralConfiguration.DefenderScheduledScanTime 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ScheduleScanTime

### <a name="windows10generalconfigurationdefenderschedulescanday"></a>Windows10GeneralConfiguration.DefenderScheduleScanDay 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ScheduleScanDay

### <a name="windows10generalconfigurationdefendersignatureupdateintervalinhours"></a>Windows10GeneralConfiguration.DefenderSignatureUpdateIntervalInHours 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/SignatureUpdateInterval

### <a name="windows10generalconfigurationdefendersubmitsamplesconsenttype"></a>Windows10GeneralConfiguration.DefenderSubmitSamplesConsentType 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/SubmitSamplesConsent

### <a name="windows10generalconfigurationdefendersystemscanschedule"></a>Windows10GeneralConfiguration.DefenderSystemScanSchedule 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Defender/ScheduleScanDay

### <a name="windows10generalconfigurationdeveloperunlocksetting"></a>Windows10GeneralConfiguration.DeveloperUnlockSetting 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowDeveloperUnlock

### <a name="windows10generalconfigurationdevicemanagementblockfactoryresetonmobile"></a>Windows10GeneralConfiguration.DeviceManagementBlockFactoryResetOnMobile 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/AllowUserToResetPhone

### <a name="windows10generalconfigurationdevicemanagementblockmanualunenroll"></a>Windows10GeneralConfiguration.DeviceManagementBlockManualUnenroll 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowManualMDMUnregistration

### <a name="windows10generalconfigurationdiagnosticsdatasubmissionmode"></a>Windows10GeneralConfiguration.DiagnosticsDataSubmissionMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/AllowTelemettry

### <a name="windows10generalconfigurationdisplayapplistwithgdidpiscalingturnedoff"></a>Windows10GeneralConfiguration.DisplayAppListWithGdiDPIScalingTurnedOff 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Display/TurnOffGdiDPIScalingForApps

### <a name="windows10generalconfigurationdisplayapplistwithgdidpiscalingturnedon"></a>Windows10GeneralConfiguration.DisplayAppListWithGdiDPIScalingTurnedOn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Display/TurnOnGdiDPIScalingForApps

### <a name="windows10generalconfigurationedgeallowstartpagesmodification"></a>Windows10GeneralConfiguration.EdgeAllowStartPagesModification 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/HomePages

### <a name="windows10generalconfigurationedgeblockaccesstoaboutflags"></a>Windows10GeneralConfiguration.EdgeBlockAccessToAboutFlags 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventAccessToAboutFlagsInMicrosoftEdge

### <a name="windows10generalconfigurationedgeblockaddressbardropdown"></a>Windows10GeneralConfiguration.EdgeBlockAddressBarDropdown 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowAddressBarDropdown

### <a name="windows10generalconfigurationedgeblockautofill"></a>Windows10GeneralConfiguration.EdgeBlockAutofill 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowAutofill

### <a name="windows10generalconfigurationedgeblockcompatibilitylist"></a>Windows10GeneralConfiguration.EdgeBlockCompatibilityList 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowMicrosoftCompatibilityList

### <a name="windows10generalconfigurationedgeblockdevelopertools"></a>Windows10GeneralConfiguration.EdgeBlockDeveloperTools 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowDeveloperTools

### <a name="windows10generalconfigurationedgeblocked"></a>Windows10GeneralConfiguration.EdgeBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowBrowser

### <a name="windows10generalconfigurationedgeblockeditfavorites"></a>Windows10GeneralConfiguration.EdgeBlockEditFavorites 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/LockdownFavoritos

### <a name="windows10generalconfigurationedgeblockextensions"></a>Windows10GeneralConfiguration.EdgeBlockExtensions 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowExtensions

### <a name="windows10generalconfigurationedgeblockfullscreenmode"></a>Windows10GeneralConfiguration.EdgeBlockFullScreenMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowFullScreenMode

### <a name="windows10generalconfigurationedgeblockinprivatebrowsing"></a>Windows10GeneralConfiguration.EdgeBlockInPrivateBrowsing 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowInPrivate

### <a name="windows10generalconfigurationedgeblocklivetiledatacollection"></a>Windows10GeneralConfiguration.EdgeBlockLiveTileDataCollection 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventLiveTileDataCollection

### <a name="windows10generalconfigurationedgeblockpasswordmanager"></a>Windows10GeneralConfiguration.EdgeBlockPasswordManager 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowPasswordManager

### <a name="windows10generalconfigurationedgeblockpopups"></a>Windows10GeneralConfiguration.EdgeBlockPopups 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowPopups

### <a name="windows10generalconfigurationedgeblockprelaunch"></a>Windows10GeneralConfiguration.EdgeBlockPrelaunch 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowPrelaunch

### <a name="windows10generalconfigurationedgeblockprinting"></a>Windows10GeneralConfiguration.EdgeBlockPrinting 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowPrinting

### <a name="windows10generalconfigurationedgeblocksavinghistory"></a>Windows10GeneralConfiguration.EdgeBlockSavingHistory 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowSavingHistory

### <a name="windows10generalconfigurationedgeblocksearchsuggestions"></a>Windows10GeneralConfiguration.EdgeBlockSearchSuggestions 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowSearchSuggestionsinAddressBar

### <a name="windows10generalconfigurationedgeblocksendingdonottrackheader"></a>Windows10GeneralConfiguration.EdgeBlockSendingDoNotTrackHeader 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowDoNotTrack

### <a name="windows10generalconfigurationedgeblocksendingintranettraffictointernetexplorer"></a>Windows10GeneralConfiguration.EdgeBlockSendingIntranetTrafficToInternetExplorer 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SendIntranetTraffictoInternetExplorer

### <a name="windows10generalconfigurationedgeblocksideloadingextensions"></a>Windows10GeneralConfiguration.EdgeBlockSideloadingExtensions 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowSideloadingOfExtensions

### <a name="windows10generalconfigurationedgeblocktabpreloading"></a>Windows10GeneralConfiguration.EdgeBlockTabPreloading 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowTabPreloading

### <a name="windows10generalconfigurationedgeblockwebcontentonnewtabpage"></a>Windows10GeneralConfiguration.EdgeBlockWebContentOnNewTabPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowWebContentOnNewTabPage

### <a name="windows10generalconfigurationedgeclearbrowsingdataonexit"></a>Windows10GeneralConfiguration.EdgeClearBrowsingDataOnExit 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ClearBrowsingDataOnExit

### <a name="windows10generalconfigurationedgecookiepolicy"></a>Windows10GeneralConfiguration.EdgeCookiePolicy 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowCookies

### <a name="windows10generalconfigurationedgedisablefirstrunpage"></a>Windows10GeneralConfiguration.EdgeDisableFirstRunPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventFirstRunPage

### <a name="windows10generalconfigurationedgeenterprisemodesitelistlocation"></a>Windows10GeneralConfiguration.EdgeEnterpriseModeSiteListLocation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/EnterpriseSiteListServiceUrl

### <a name="windows10generalconfigurationedgefavoritesbarvisibility"></a>Windows10GeneralConfiguration.EdgeFavoritesBarVisibility 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureFavoritesBar

### <a name="windows10generalconfigurationedgefavoriteslistlocation"></a>Windows10GeneralConfiguration.EdgeFavoritesListLocation 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ProvisionFavorites

### <a name="windows10generalconfigurationedgefirstrunurl"></a>Windows10GeneralConfiguration.EdgeFirstRunUrl 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/FirstRunURL

### <a name="windows10generalconfigurationedgehomebuttonconfiguration"></a>Windows10GeneralConfiguration.EdgeHomeButtonConfiguration 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SetHomeButtonURL

### <a name="windows10generalconfigurationedgehomebuttonconfigurationenabled"></a>Windows10GeneralConfiguration.EdgeHomeButtonConfigurationEnabled 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureHomeButton

### <a name="windows10generalconfigurationedgehomepageurls"></a>Windows10GeneralConfiguration.EdgeHomepageUrls 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SetHomeButtonURL

### <a name="windows10generalconfigurationedgenewtabpageurl"></a>Windows10GeneralConfiguration.EdgeNewTabPageURL 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SetNewTabPageURL

### <a name="windows10generalconfigurationedgeopenswith"></a>Windows10GeneralConfiguration.EdgeOpensWith 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureOpenMicrosoftEdgeWith

### <a name="windows10generalconfigurationedgepreventcertificateerroroverride"></a>Windows10GeneralConfiguration.EdgePreventCertificateErrorOverride 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventCertErrorOverrides

### <a name="windows10generalconfigurationedgerequiresmartscreen"></a>Windows10GeneralConfiguration.EdgeRequireSmartScreen 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/AllowSmartScreen

### <a name="windows10generalconfigurationedgesearchengine"></a>Windows10GeneralConfiguration.EdgeSearchEngine 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SetDefaultSearchEngine

### <a name="windows10generalconfigurationedgesendintranettraffictointernetexplorer"></a>Windows10GeneralConfiguration.EdgeSendIntranetTrafficToInternetExplorer 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SendIntranetTraffictoInternetExplorer

### <a name="windows10generalconfigurationedgeshowmessagewhenopeninginternetexplorersites"></a>Windows10GeneralConfiguration.EdgeShowMessageWhenOpeningInternetExplorerSites 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ShowMessageWhenOpeningSitesInInternetExplorer

### <a name="windows10generalconfigurationedgesyncfavoriteswithinternetexplorer"></a>Windows10GeneralConfiguration.EdgeSyncFavoritesWithInternetExplorer 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/SyncFavoritesBetweenIEEMicrosoftEdge

### <a name="windows10generalconfigurationedgetelemetryformicrosoft365analytics"></a>Windows10GeneralConfiguration.EdgeTelemetryForMicrosoft365Analytics 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureTelemettryForMicrosoft365Analytics

### <a name="windows10generalconfigurationenableautomaticredeployment"></a>Windows10GeneralConfiguration.EnableAutomaticRedeployment 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/CredenciaisFornecedores/Desativar Credenciais de Reafectação Automática

### <a name="windows10generalconfigurationenterprisecloudprintdiscoveryendpoint"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintDiscoveryEndPoint 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint

### <a name="windows10generalconfigurationenterprisecloudprintdiscoverymaxlimit"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintDiscoveryMaxLimit 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit

### <a name="windows10generalconfigurationenterprisecloudprintmopriadiscoveryresourceidentifier"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintMopriaDiscoveryResourceIdentifier 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId

### <a name="windows10generalconfigurationenterprisecloudprintoauthauthority"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintOAuthAuthority 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### <a name="windows10generalconfigurationenterprisecloudprintoauthclientidentifier"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintOAuthClientIdentifier 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### <a name="windows10generalconfigurationenterprisecloudprintresourceidentifier"></a>Windows10GeneralConfiguration.EnterpriseCloudPrintResourceIdentifier 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintResourceId

### <a name="windows10generalconfigurationexperienceblockconsumerspecificfeatures"></a>Windows10GeneralConfiguration.ExperienceBlockConsumerSpecificFeatures 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsConsumerFeatures

### <a name="windows10generalconfigurationexperienceblockdevicediscovery"></a>Windows10GeneralConfiguration.ExperienceBlockDeviceDiscovery 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowDeviceDiscovery

### <a name="windows10generalconfigurationexperienceblockerrordialogwhennosim"></a>Windows10GeneralConfiguration.ExperienceBlockErrorDialogWhenNoSIM 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowSIMErrorDialogPromptWhenNoSIM

### <a name="windows10generalconfigurationexperienceblocktaskswitcher"></a>Windows10GeneralConfiguration.ExperienceBlockTaskSwitcher 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowTaskSwitcher

### <a name="windows10generalconfigurationexperienceblockwindowsspotlight"></a>Windows10GeneralConfiguration.ExperienceBlockWindowsSpotlight 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsSpotlight

### <a name="windows10generalconfigurationexperiencedonotsyncbrowsersettings"></a>Windows10GeneralConfiguration.ExperienceDoNotSyncBrowserSettings 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/DoNotSyncBrowserSettings

### <a name="windows10generalconfigurationgamedvrblocked"></a>Windows10GeneralConfiguration.GameDvrBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowGameDVR

### <a name="windows10generalconfigurationhardwaredeviceinstallationbydeviceidentifiers"></a>Windows10GeneralConfiguration.HardwareDeviceInstallationByDeviceIdentifiers 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### <a name="windows10generalconfigurationhardwaredeviceinstallationbysetupclasses"></a>Windows10GeneralConfiguration.HardwareDeviceInstallationBySetupClasses 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### <a name="windows10generalconfigurationinkworkspaceaccess"></a>Windows10GeneralConfiguration.InkWorkspaceAccess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### <a name="windows10generalconfigurationinkworkspaceaccessstate"></a>Windows10GeneralConfiguration.InkWorkspaceAccessState 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### <a name="windows10generalconfigurationinkworkspaceblocksuggestedapps"></a>Windows10GeneralConfiguration.InkWorkspaceBlockSuggestedApps 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsInkWorkspace/AllowSuggestedAppsInWindowsInkWorkspacespace

### <a name="windows10generalconfigurationinternetexploreractivexcontrolsinprotectedmode"></a>Windows10GeneralConfiguration.InternetExplorerActiveXControlsInProtectedMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DoNotAllowActiveXControlsInProtectedMode

### <a name="windows10generalconfigurationinternetexplorerautocomplete"></a>Windows10GeneralConfiguration.InternetExplorerAutoComplete 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/AllowAutoComplete

### <a name="windows10generalconfigurationinternetexplorerblockoutdatedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerBlockOutdatedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DoNotBlockOutdatedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerbypasssmartscreenwarnings"></a>Windows10GeneralConfiguration.InternetExplorerBypassSmartScreenWarnings 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DisableBypassOfSmartScreenWarnings

### <a name="windows10generalconfigurationinternetexplorerbypasssmartscreenwarningsaboutuncommonfiles"></a>Windows10GeneralConfiguration.InternetExplorerBypassSmartScreenWarningsAboutUncommonFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DisableBypassOfSmartScreenWarningsAboutUncommonFiles

### <a name="windows10generalconfigurationinternetexplorercertificateaddressmismatchwarning"></a>Windows10GeneralConfiguration.InternetExplorerCertificateAddressMismatchWarning 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/AllowCertificateAddressMismatchWarning

### <a name="windows10generalconfigurationinternetexplorercheckservercertificaterevocation"></a>Windows10GeneralConfiguration.InternetExplorerCheckServerCertificateRevocation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/CheckServerCertificateRevogavocation

### <a name="windows10generalconfigurationinternetexplorerchecksignaturesondownloadedprograms"></a>Windows10GeneralConfiguration.InternetExplorerCheckSignaturesOnDownloadedPrograms 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/CheckSignaturesOnDownloadedPrograms

### <a name="windows10generalconfigurationinternetexplorercrashdetection"></a>Windows10GeneralConfiguration.InternetExplorerCrashDetection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/Deteção de acidentes desativado

### <a name="windows10generalconfigurationinternetexplorerdisableprocessesinenhancedprotectedmode"></a>Windows10GeneralConfiguration.InternetExplorerDisableProcessesInEnhancedProtectedMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DesactivaçõesInEnhancedProtectedMode

### <a name="windows10generalconfigurationinternetexplorerdownloadenclosures"></a>Windows10GeneralConfiguration.InternetExplorerDownloadEnclosures 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/Desativação

### <a name="windows10generalconfigurationinternetexplorerencryptionsupport"></a>Windows10GeneralConfiguration.InternetExplorerEncryptionSupport 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DisableEncryptionSupport

### <a name="windows10generalconfigurationinternetexplorerenhancedprotectedmode"></a>Windows10GeneralConfiguration.InternetExplorerEnhancedProtectedMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/AllowEnhancedProtectedMode

### <a name="windows10generalconfigurationinternetexplorerfallbacktossl3"></a>Windows10GeneralConfiguration.InternetExplorerFallbackToSsl3 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/AllowFallbackToSSL3

### <a name="windows10generalconfigurationinternetexplorerignorecertificateerrors"></a>Windows10GeneralConfiguration.InternetExplorerIgnoreCertificateErrors 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DisableIgnoringCertificateErrors

### <a name="windows10generalconfigurationinternetexplorerincludeallnetworkpaths"></a>Windows10GeneralConfiguration.InternetExplorerIncludeAllNetworkPaths 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/IncludeAllNetworkPaths

### <a name="windows10generalconfigurationinternetexplorerinternetzoneaccesstodatasources"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneAccessToDataSources 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowAccessToDataSources

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowonlyapproveddomainstouseactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowOnlyApprovedDomainsToUseActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowonlyapproveddomainstousetdcactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowOnlyApprovedDomainsToUseTdcActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### <a name="windows10generalconfigurationinternetexplorerinternetzoneallowvbscripttorun"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowVBScriptToRun 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowVBScriptTorunInInternetExplorer

### <a name="windows10generalconfigurationinternetexplorerinternetzoneautomaticpromptforfiledownloads"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneAutomaticPromptForFileDownloads 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowAutomaticPromptingForFileDownloads

### <a name="windows10generalconfigurationinternetexplorerinternetzonecopyandpasteviascript"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneCopyAndPasteViaScript 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowCopyPasteViaScript

### <a name="windows10generalconfigurationinternetexplorerinternetzonecrosssitescriptingfilter"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneCrossSiteScriptingFilter 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableCrossSiteScriptingFilter

### <a name="windows10generalconfigurationinternetexplorerinternetzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedotnetframeworkreliantcomponents"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDotNetFrameworkReliantComponents 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowNETFrameworkReliantComponents

### <a name="windows10generalconfigurationinternetexplorerinternetzonedownloadsignedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDownloadSignedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneDownloadSignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedownloadunsignedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDownloadUnsignedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneDownloadUnsignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonedraganddroporcopyandpastefiles"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDragAndDropOrCopyAndPasteFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowDragAndDropCopyAndPasteFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonedragcontentfromdifferentdomainsacrosswindows"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDragContentFromDifferentDomainsAcrossWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows

### <a name="windows10generalconfigurationinternetexplorerinternetzonedragcontentfromdifferentdomainswithinwindows"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneDragContentFromDifferentDomainsWithinWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### <a name="windows10generalconfigurationinternetexplorerinternetzoneincludelocalpathwhenuploadingfilestoserver"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneIncludeLocalPathWhenUploadingFilesToServer 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneIncludeLocalPathWhenUploadingFilesToServer

### <a name="windows10generalconfigurationinternetexplorerinternetzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneJavaPermissions


### <a name="windows10generalconfigurationinternetexplorerinternetzonelaunchapplicationsandfilesinaniframe"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneLaunchApplicationsAndFilesInAnIFrame 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneLaunchingApplicationsAndFilesInIFRAME

### <a name="windows10generalconfigurationinternetexplorerinternetzonelessprivilegedsites"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneLessPrivilegedSites 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowLessLessPrivilegedSites

### <a name="windows10generalconfigurationinternetexplorerinternetzoneloadingofxamlfiles"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneLoadingOfXamlFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowLoadingOfXAMLFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonelogonoptions"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneLogonOptions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneLogonOptions

### <a name="windows10generalconfigurationinternetexplorerinternetzonenavigatewindowsandframesacrossdifferentdomains"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneNavigateWindowsAndFramesAcrossDifferentDomains 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneNavigateWindowsAndFrames

### <a name="windows10generalconfigurationinternetexplorerinternetzonepopupblocker"></a>Windows10GeneralConfiguration.InternetExplorerInternetZonePopupBlocker 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneUsePopupBlocker

### <a name="windows10generalconfigurationinternetexplorerinternetzoneprotectedmode"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneProtectedMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableProtectedMode

### <a name="windows10generalconfigurationinternetexplorerinternetzonerundotnetframeworkreliantcomponentssignedwithauthenticode"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneRunDotNetFrameworkReliantComponentsSignedWithAuthenticode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptingofwebbrowsercontrols"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptingOfWebBrowserControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScripting OfInternetExplorerWebBrowserControls

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptinitiatedwindows"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptInitiatedWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScriptScriptScript

### <a name="windows10generalconfigurationinternetexplorerinternetzonescriptlets"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptlets 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScriptlets

### <a name="windows10generalconfigurationinternetexplorerinternetzonesecuritywarningforpotentiallyunsafefiles"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneSecurityWarningForPotentiallyUnsafeFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneShowSecurityWarningForPotentiallyUnsafeFiles

### <a name="windows10generalconfigurationinternetexplorerinternetzonesmartscreen"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneSmartScreen 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerinternetzoneupdatestostatusbarviascript"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneUpdatesToStatusBarViaScript 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowUpdatesToStatusBarViaScript

### <a name="windows10generalconfigurationinternetexplorerinternetzoneuserdatapersistence"></a>Windows10GeneralConfiguration.InternetExplorerInternetZoneUserDataPersistence 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowUserUserPersistence

### <a name="windows10generalconfigurationinternetexplorerintranetzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerIntranetZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/IntranetZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerintranetzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration.InternetExplorerIntranetZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/IntranetZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerintranetzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerIntranetZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/IntranetZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlocalmachinezonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerLocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerlocalmachinezonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerLocalMachineZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LocalMachineZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddowninternetzonesmartscreen"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownInternetZoneSmartScreen 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownInternetZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerlockeddownintranetzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownIntranetZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownIntranetJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownlocalmachinezonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownLocalMachineZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownLocalMachineZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownrestrictedzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownRestrictedZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownRestrictedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerlockeddownrestrictedzonesmartscreen"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownRestrictedZoneSmartScreen 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownRestrictedSitesZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerlockeddowntrustedzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerLockedDownTrustedZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/LockedDownTrustSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerpreventmanagingsmartscreenfilter"></a>Windows10GeneralConfiguration.InternetExplorerPreventManagingSmartScreenFilter 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/PreventManagingSmartScreenFilter

### <a name="windows10generalconfigurationinternetexplorerpreventperuserinstallationofactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerPreventPerUserInstallationOfActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/PreventPerUserInstallationOfActiveXControls

### <a name="windows10generalconfigurationinternetexplorerprocessesconsistentmimehandling"></a>Windows10GeneralConfiguration.InternetExplorerProcessesConsistentMimeHandling 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/ConsistentMimeHandlingInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesmimesniffingsafetyfeature"></a>Windows10GeneralConfiguration.InternetExplorerProcessesMimeSniffingSafetyFeature 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/MimeSniffingSafetyFeatureInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesmkprotocolsecurityrestriction"></a>Windows10GeneralConfiguration.InternetExplorerProcessesMKProtocolSecurityRestriction 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/MKProtocolSecurityRestrictionInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesnotificationbar"></a>Windows10GeneralConfiguration.InternetExplorerProcessesNotificationBar 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/NotificationBarInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesprotectionfromzoneelevation"></a>Windows10GeneralConfiguration.InternetExplorerProcessesProtectionFromZoneElevation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/ProtectionFromZoneElevationInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesrestrictactivexinstall"></a>Windows10GeneralConfiguration.InternetExplorerProcessesRestrictActiveXInstall 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictActiveXInstallInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesrestrictfiledownload"></a>Windows10GeneralConfiguration.InternetExplorerProcessesRestrictFileDownload 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictFileDownloadInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerprocessesscriptedwindowsecurityrestrictions"></a>Windows10GeneralConfiguration.InternetExplorerProcessesScriptedWindowSecurityRestrictions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/ScriptedWindowSecurityRestrictionsInternetExplorerProcesses

### <a name="windows10generalconfigurationinternetexplorerremoverunthistimebuttonforoutdatedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRemoveRunThisTimeButtonForOutdatedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RemoveRunThisTimeButtonForOutdatedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneaccesstodatasources"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAccessToDataSources 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowAccessToDataSources

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneactivescripting"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneActiveScripting 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowActiveScripting

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowonlyapproveddomainstouseactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowOnlyApprovedDomainsToUseActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowonlyapproveddomainstousetdcactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowOnlyApprovedDomainsToUseTdcActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneallowvbscripttorun"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowVBScriptToRun 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowVBScriptToRunInInternetExplorer

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneautomaticpromptforfiledownloads"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAutomaticPromptForFileDownloads 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowAutomaticPromptingForFileDownloads

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonebinaryandscriptbehaviors"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneBinaryAndScriptBehaviors 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowBinaryAndScriptBehaviors

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonecopyandpasteviascript"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneCopyAndPasteViaScript 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowCopyPasteViaScript

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonecrosssitescriptingfilter"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneCrossSiteScriptingFilter 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableCrossSiteScriptingFilter

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedotnetframeworkreliantcomponents"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDotNetFrameworkReliantComponents 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowNETFrameworkReliantComponents

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedownloadsignedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDownloadSignedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDownloadSignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedownloadunsignedactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDownloadUnsignedActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDownloadUnsignedActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedraganddroporcopyandpastefiles"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragAndDropOrCopyAndPasteFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowDragAndDropCopyAndPasteFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedragcontentfromdifferentdomainsacrosswindows"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragContentFromDifferentDomainsAcrossWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfDifferentDomainsAcrossWindows

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonedragcontentfromdifferentdomainswithinwindows"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragContentFromDifferentDomainsWithinWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonefiledownloads"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneFileDownloads 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowFileDownloads

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneincludelocalpathwhenuploadingfilestoserver"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneIncludeLocalPathWhenUploadingFilesToServer 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneIncludeLocalPathWhenUploadingFilesToServer

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelaunchapplicationsandfilesinaniframe"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLaunchApplicationsAndFilesInAnIFrame 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneLaunchingApplicationsAndFilesInIFRAME

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelessprivilegedsites"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLessPrivilegedSites 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/Sites RestritosZoneAllowLessPrivilegedSites

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneloadingofxamlfiles"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLoadingOfXamlFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowLoadingOfXAMLFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonelogonoptions"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLogonOptions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneLogonOptions

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonemetarefresh"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneMetaRefresh 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowMETAREFRESH

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonenavigatewindowsandframesacrossdifferentdomains"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneNavigateWindowsAndFramesAcrossDifferentDomains 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneNavigateWindowsAndFrames

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonepopupblocker"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZonePopupBlocker 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneUsePopupBlocker

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneprotectedmode"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneProtectedMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneTurnOnProtectedMode

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonerunactivexcontrolsandplugins"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneRunActiveXControlsAndPlugins 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneRunActiveXControls AndPlugins

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonerundotnetframeworkreliantcomponentssignedwithauthenticode"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneRunDotNetFrameworkReliantComponentsSignedWithAuthenticode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptactivexcontrolsmarkedsafeforscripting"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptActiveXControlsMarkedSafeForScripting 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneScriptActiveXControlsMarcadosSegurosForScripting

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptingofjavaapplets"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptingOfJavaApplets 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneScripting OfJavaApplets

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptingofwebbrowsercontrols"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptingOfWebBrowserControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScripting OfInternetExplorerWebBrowserControls

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptinitiatedwindows"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptInitiatedWindows 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScriptScript

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonescriptlets"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptlets 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScriptlets

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonesecuritywarningforpotentiallyunsafefiles"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneSecurityWarningForPotentiallyUnsafeFiles 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneShowSecurityWarningForPotentiallyUnsafeFiles

### <a name="windows10generalconfigurationinternetexplorerrestrictedzonesmartscreen"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneSmartScreen 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowSmartScreenIE

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneupdatestostatusbarviascript"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneUpdatesToStatusBarViaScript 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowUpdatesToStatusBarViaScript

### <a name="windows10generalconfigurationinternetexplorerrestrictedzoneuserdatapersistence"></a>Windows10GeneralConfiguration.InternetExplorerRestrictedZoneUserDataPersistence 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowUserUserDataPersistence

### <a name="windows10generalconfigurationinternetexplorersecuritysettingscheck"></a>Windows10GeneralConfiguration.InternetExplorerSecuritySettingsCheck 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DesactivaçõesDeSegurançaCheck

### <a name="windows10generalconfigurationinternetexplorersecurityzonesuseonlymachinesettings"></a>Windows10GeneralConfiguration.InternetExplorerSecurityZonesUseOnlyMachineSettings 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/SecurityZonesUseOnlyMachineSettings

### <a name="windows10generalconfigurationinternetexplorersoftwarewhensignatureisinvalid"></a>Windows10GeneralConfiguration.InternetExplorerSoftwareWhenSignatureIsInvalid 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/AllowSoftwareWhenSignatureIsInvalid

### <a name="windows10generalconfigurationinternetexplorertrustedzonedonotrunantimalwareagainstactivexcontrols"></a>Windows10GeneralConfiguration.InternetExplorerTrustedZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### <a name="windows10generalconfigurationinternetexplorertrustedzoneinitializeandscriptactivexcontrolsnotmarkedassafe"></a>Windows10GeneralConfiguration.InternetExplorerTrustedZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneInitializeAndScriptActiveXControls

### <a name="windows10generalconfigurationinternetexplorertrustedzonejavapermissions"></a>Windows10GeneralConfiguration.InternetExplorerTrustedZoneJavaPermissions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneJavaPermissions

### <a name="windows10generalconfigurationinternetexploreruseactivexinstallerservice"></a>Windows10GeneralConfiguration.InternetExplorerUseActiveXInstallerService 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/SpecifyUseOfActiveXInstallerService

### <a name="windows10generalconfigurationinternetexplorerusersaddingsites"></a>Windows10GeneralConfiguration.InternetExplorerUsersAddingSites 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DoNotAllowUsersToAddSites

### <a name="windows10generalconfigurationinternetexploreruserschangingpolicies"></a>Windows10GeneralConfiguration.InternetExplorerUsersChangingPolicies 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/InternetExplorer/DoNotAllowUsersToChangePolicies

### <a name="windows10generalconfigurationinternetsharingblocked"></a>Windows10GeneralConfiguration.InternetSharingBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WiFi/AllowInternetSharing

### <a name="windows10generalconfigurationlocationservicesblocked"></a>Windows10GeneralConfiguration.LocationServicesBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/AllowLocation

### <a name="windows10generalconfigurationlockscreenallowtimeoutconfiguration"></a>Windows10GeneralConfiguration.LockScreenAllowTimeoutConfiguration 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/AllowScreenTimeoutWhileLockedUser/Config

### <a name="windows10generalconfigurationlockscreenblockactioncenternotifications"></a>Windows10GeneralConfiguration.LockScreenBlockActionCenterNotifications 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/AboveLock/AllowActionCenterNotifications

### <a name="windows10generalconfigurationlockscreenblockcortana"></a>Windows10GeneralConfiguration.LockScreenBlockCortana 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/AboveLock/AllowCortanaAboveLock

### <a name="windows10generalconfigurationlockscreenblocktoastnotifications"></a>Windows10GeneralConfiguration.LockScreenBlockToastNotifications 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/AboveLock/AllowToasts

### <a name="windows10generalconfigurationlockscreencamera"></a>Windows10GeneralConfiguration.LockScreenCamera 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/PreventenableingLockScreenCamera

### <a name="windows10generalconfigurationlockscreenhidenetworkselectionui"></a>Windows10GeneralConfiguration.LockScreenHideNetworkSelectionUI 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsLogon/DontDisplayNetworkSelectionUI

### <a name="windows10generalconfigurationlockscreenslideshow"></a>Windows10GeneralConfiguration.LockScreenSlideShow 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/PreventLockScreenSlideShow

### <a name="windows10generalconfigurationlockscreentimeoutinseconds"></a>Windows10GeneralConfiguration.LockScreenTimeoutInSeconds 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/ScreenTimeoutWhileLocked

### <a name="windows10generalconfigurationlogonblockfastuserswitching"></a>Windows10GeneralConfiguration.LogonBlockFastUserSwitching 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsLogon/HideFastUserSwitching

### <a name="windows10generalconfigurationmessagingblockmms"></a>Windows10GeneralConfiguration.MessagingBlockMMS 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Messaging/AllowMMS

### <a name="windows10generalconfigurationmessagingblockrichcommunicationservices"></a>Windows10GeneralConfiguration.MessagingBlockRichCommunicationServices 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Messaging/AllowRCS

### <a name="windows10generalconfigurationmessagingblocksync"></a>Windows10GeneralConfiguration.MessagingBlockSync 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Messaging/AllowMessageSync

### <a name="windows10generalconfigurationmicrosoftaccountblocked"></a>Windows10GeneralConfiguration.MicrosoftAccountBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Accounts/AllowMicrosoftAccountConnection

### <a name="windows10generalconfigurationmicrosoftaccountblocksettingssync"></a>Windows10GeneralConfiguration.MicrosoftAccountBlockSettingsSync 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowSyncMySettings

### <a name="windows10generalconfigurationmicrosoftaccountsigninassistantsettings"></a>Windows10GeneralConfiguration.MicrosoftAccountSignInAssistantSettings 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Contas  
**Offset URI**: /Permitir microsoftaccountsigninassistant

### <a name="windows10generalconfigurationnetworkproxyapplysettingsdevicewide"></a>Windows10GeneralConfiguration.NetworkProxyApplySettingsDeviceWide 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Networkproxy  
**Offset URI**: /ProxySettingsPerUser

### <a name="windows10generalconfigurationnetworkproxyautomaticconfigurationurl"></a>Windows10GeneralConfiguration.NetworkProxyAutomaticConfigurationUrl 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Networkproxy  
**Offset URI**: /ConfiguraçãoScriptUrl

### <a name="windows10generalconfigurationnetworkproxydisableautodetect"></a>Windows10GeneralConfiguration.NetworkProxyDisableAutoDetect 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Networkproxy  
**Offset URI**: /AutoDetect

### <a name="windows10generalconfigurationnetworkproxyserver"></a>Windows10GeneralConfiguration.NetworkProxyServer 
**CSP**: ./Fornecedor/MSFT/Networkproxy  
**Offset URI**: /ProxyAddress, /Exceções e /UseProxyForLocalAddresss

### <a name="windows10generalconfigurationnfcblocked"></a>Windows10GeneralConfiguration.NfcBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowNFC

### <a name="windows10generalconfigurationonedrivedisablefilesync"></a>Windows10GeneralConfiguration.OneDriveDisableFileSync 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/DisableOneDriveFileSync

### <a name="windows10generalconfigurationpasswordblocksimple"></a>Windows10GeneralConfiguration.PasswordBlockSimple 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/AllowSimpleDevicePassword

### <a name="windows10generalconfigurationpasswordexpirationdays"></a>Windows10GeneralConfiguration.PasswordExpirationDays 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/DevicePasswordExpiration

### <a name="windows10generalconfigurationpasswordminimumageindays"></a>Windows10GeneralConfiguration.PasswordMinimumAgeInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/MinimumPasswordAge

### <a name="windows10generalconfigurationpasswordminimumcharactersetcount"></a>Windows10GeneralConfiguration.PasswordMinimumCharacterSetCount 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/MinDevicePasswordComplexCharacters

### <a name="windows10generalconfigurationpasswordminimumlength"></a>Windows10GeneralConfiguration.PasswordMinimumLength 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/MinDevicePasswordLength

### <a name="windows10generalconfigurationpasswordminutesofinactivitybeforescreentimeout"></a>Windows10GeneralConfiguration.PasswordMinutesOfInactivityBeforeScreenTimeout 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/MaxInactivityTimeDeviceLock

### <a name="windows10generalconfigurationpasswordpreviouspasswordblockcount"></a>Windows10GeneralConfiguration.PasswordPreviousPasswordBlockCount 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/DevicePasswordHistory

### <a name="windows10generalconfigurationpasswordrequired"></a>Windows10GeneralConfiguration.PasswordRequired 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/DevicePasswordEnabled

### <a name="windows10generalconfigurationpasswordrequiredtype"></a>Windows10GeneralConfiguration.PasswordRequiredType 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/AlphanumericDevicePasswordRequired

### <a name="windows10generalconfigurationpasswordrequirewhenresumefromidlestate"></a>Windows10GeneralConfiguration.PasswordRequireWhenResumeFromIdleState 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/AllowIdleReturnWithoutPassword

### <a name="windows10generalconfigurationpasswordsigninfailurecountbeforefactoryreset"></a>Windows10GeneralConfiguration.PasswordSignInFailureCountBeforeFactoryReset 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceLock/MaxDevicePasswordTentativas falhadas

### <a name="windows10generalconfigurationpersonalizationdesktopimageurl"></a>Windows10GeneralConfiguration.PersonalizationDesktopImageUrl 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Personalização  
**Offset URI**: /DesktopImageUrl

### <a name="windows10generalconfigurationpersonalizationlockscreenimageurl"></a>Windows10GeneralConfiguration.PersonalizationLockScreenImageUrl 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Personalização  
**Offset URI**: /LockScreenImageUrl

### <a name="windows10generalconfigurationpowerrequirepasswordonwakewhileonbattery"></a>Windows10GeneralConfiguration.PowerRequirePasswordOnWakeWhileOnBattery 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Power/RequirePasswordWhenComputerWakesOnBattery

### <a name="windows10generalconfigurationpowerrequirepasswordonwakewhilepluggedin"></a>Windows10GeneralConfiguration.PowerRequirePasswordOnWakeWhilePluggedIn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Power/RequirePasswordWhenComputerWakesPluggedIn

### <a name="windows10generalconfigurationpowerstandbystateswhensleepingwhileonbattery"></a>Windows10GeneralConfiguration.PowerStandbyStatesWhenSleepingWhileOnBattery 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Power/AllowStandbyStatesWhenSleepingOnBattery

### <a name="windows10generalconfigurationpowerstandbystateswhensleepingwhilepluggedin"></a>Windows10GeneralConfiguration.PowerStandbyStatesWhenSleepingWhilePluggedIn 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Power/AllowStandbyWhenSleepingPluggedIn

### <a name="windows10generalconfigurationpreventinstallationofmatchingdeviceids"></a>windows10generalconfiguration.preventInstallationOfMatchingDeviceIDs 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### <a name="windows10generalconfigurationpreventinstallationofmatchingdevicesetupclasses"></a>windows10generalconfiguration.preventInstallationOfMatchingDeviceSetupClasses 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### <a name="windows10generalconfigurationprinterblockaddition"></a>Windows10GeneralConfiguration.PrinterBlockAddition 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Education/PreventAddingNewPrinters

### <a name="windows10generalconfigurationprinterdefaultname"></a>Windows10GeneralConfiguration.PrinterDefaultName 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Education/DefaultPrinterName

### <a name="windows10generalconfigurationprinternames"></a>Windows10GeneralConfiguration.PrinterNames 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Education/ImpressoraNames

### <a name="windows10generalconfigurationprivacyadvertisingid"></a>Windows10GeneralConfiguration.PrivacyAdvertisingId 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Privacidade/DesativarPublicID

### <a name="windows10generalconfigurationprivacyautoacceptpairingandconsentprompts"></a>Windows10GeneralConfiguration.PrivacyAutoAcceptPairingAndConsentPrompts 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts

### <a name="windows10generalconfigurationprivacyblockactivityfeed"></a>Windows10GeneralConfiguration.PrivacyBlockActivityFeed 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Privacidade/EnableActivityFeed

### <a name="windows10generalconfigurationprivacyblockinputpersonalization"></a>Windows10GeneralConfiguration.PrivacyBlockInputPersonalization 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Privacy/AllowInputPersonalization

### <a name="windows10generalconfigurationprivacyblockpublishuseractivities"></a>Windows10GeneralConfiguration.PrivacyBlockPublishUserActivities 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Privacidade/Atividades de Utilizadores Publicados

### <a name="windows10generalconfigurationsafesearchfilter"></a>Windows10GeneralConfiguration.SafeSearchFilter 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/SafeSearchPermissions

### <a name="windows10generalconfigurationscreencaptureblocked"></a>Windows10GeneralConfiguration.ScreenCaptureBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowScreenCapture

### <a name="windows10generalconfigurationsearchblockdiacritics"></a>Windows10GeneralConfiguration.SearchBlockDiacritics 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/AllowUsingDiacritics

### <a name="windows10generalconfigurationsearchblockwebresults"></a>Windows10GeneralConfiguration.SearchBlockWebResults 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/DoNotUseWebResults

### <a name="windows10generalconfigurationsearchdisableautolanguagedetection"></a>Windows10GeneralConfiguration.SearchDisableAutoLanguageDetection 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/AlwaysUseAutoLangDetection

### <a name="windows10generalconfigurationsearchdisableindexerbackoff"></a>Windows10GeneralConfiguration.SearchDisableIndexerBackoff 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/DisableBackoff

### <a name="windows10generalconfigurationsearchdisableindexingencrypteditems"></a>Windows10GeneralConfiguration.SearchDisableIndexingEncryptedItems 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/AllowIndexingEncryptedStoresOrItems

### <a name="windows10generalconfigurationsearchdisableindexingremovabledrive"></a>Windows10GeneralConfiguration.SearchDisableIndexingRemovableDrive 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/DisableRemovaBleDriveIndexing

### <a name="windows10generalconfigurationsearchdisablelocation"></a>Windows10GeneralConfiguration.SearchDisableLocation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/AllowSearchToUseLocation

### <a name="windows10generalconfigurationsearchdisableuselocation"></a>Windows10GeneralConfiguration.SearchDisableUseLocation 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/AllowSearchToUseLocation

### <a name="windows10generalconfigurationsearchenableautomaticindexsizemanangement"></a>Windows10GeneralConfiguration.SearchEnableAutomaticIndexSizeManangement 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/PreventIndexingLowDiskSpaceMB

### <a name="windows10generalconfigurationsearchenableremotequeries"></a>Windows10GeneralConfiguration.SearchEnableRemoteQueries 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Search/PreventRemoteQueries

### <a name="windows10generalconfigurationsecurityblockazureadjoineddevicesautoencryption"></a>Windows10GeneralConfiguration.SecurityBlockAzureADJoinedDevicesAutoEncryption 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/PreventAutomaticDeviceCryptonForAzureADJoinedDevices

### <a name="windows10generalconfigurationsettingsblockaccountspage"></a>Windows10GeneralConfiguration.SettingsBlockAccountsPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockaddprovisioningpackage"></a>Windows10GeneralConfiguration.SettingsBlockAddProvisioningPackage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/AllowAddProvisioningPackage

### <a name="windows10generalconfigurationsettingsblockappspage"></a>Windows10GeneralConfiguration.SettingsBlockAppsPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockchangelanguage"></a>Windows10GeneralConfiguration.SettingsBlockChangeLanguage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/AllowLanguage

### <a name="windows10generalconfigurationsettingsblockchangepowersleep"></a>Windows10GeneralConfiguration.SettingsBlockChangePowerSleep 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/AllowPowerSleep

### <a name="windows10generalconfigurationsettingsblockchangeregion"></a>Windows10GeneralConfiguration.SettingsBlockChangeRegion 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/AllowRegion

### <a name="windows10generalconfigurationsettingsblockchangesystemtime"></a>Windows10GeneralConfiguration.SettingsBlockChangeSystemTime 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/AllowDateTime

### <a name="windows10generalconfigurationsettingsblockdevicespage"></a>Windows10GeneralConfiguration.SettingsBlockDevicesPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockeaseofaccesspage"></a>Windows10GeneralConfiguration.SettingsBlockEaseOfAccessPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockeditdevicename"></a>Windows10GeneralConfiguration.SettingsBlockEditDeviceName 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/AllowEditDeviceName

### <a name="windows10generalconfigurationsettingsblockgamingpage"></a>Windows10GeneralConfiguration.SettingsBlockGamingPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblocknetworkinternetpage"></a>Windows10GeneralConfiguration.SettingsBlockNetworkInternetPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockpersonalizationpage"></a>Windows10GeneralConfiguration.SettingsBlockPersonalizationPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockprivacypage"></a>Windows10GeneralConfiguration.SettingsBlockPrivacyPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockremoveprovisioningpackage"></a>Windows10GeneralConfiguration.SettingsBlockRemoveProvisioningPackage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/AllowRemoveProvisioningPackage

### <a name="windows10generalconfigurationsettingsblocksystempage"></a>Windows10GeneralConfiguration.SettingsBlockSystemPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblocktimelanguagepage"></a>Windows10GeneralConfiguration.SettingsBlockTimeLanguagePage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationsettingsblockupdatesecuritypage"></a>Windows10GeneralConfiguration.SettingsBlockUpdateSecurityPage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Settings/PageVisibilityList

### <a name="windows10generalconfigurationshareduserappdataallowed"></a>Windows10GeneralConfiguration.SharedUserAppDataAllowed 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowSharedUserAppData

### <a name="windows10generalconfigurationsmartscreenblockpromptoverride"></a>Windows10GeneralConfiguration.SmartScreenBlockPromptOverride 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventSmartScreenPromptOverride

### <a name="windows10generalconfigurationsmartscreenblockpromptoverrideforfiles"></a>Windows10GeneralConfiguration.SmartScreenBlockPromptOverrideForFiles 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventSmartScreenPromptOverrideForFiles

### <a name="windows10generalconfigurationsmartscreenenableappinstallcontrol"></a>Windows10GeneralConfiguration.SmartScreenEnableAppInstallControl 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/SmartScreen/EnableAppInstallControl

### <a name="windows10generalconfigurationstartblockunpinningappsfromtaskbar"></a>Windows10GeneralConfiguration.StartBlockUnpinningAppsFromTaskbar 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/NoPinningToTaskbar

### <a name="windows10generalconfigurationstartmenuapplistvisibility"></a>Windows10GeneralConfiguration.StartMenuAppListVisibility 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideAppList

### <a name="windows10generalconfigurationstartmenuhidechangeaccountsettings"></a>Windows10GeneralConfiguration.StartMenuHideChangeAccountSettings 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideChangeAccountSettings

### <a name="windows10generalconfigurationstartmenuhidefrequentlyusedapps"></a>Windows10GeneralConfiguration.StartMenuHideFrequentlyUsedApps 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideFrequentlyUsedApps

### <a name="windows10generalconfigurationstartmenuhidehibernate"></a>Windows10GeneralConfiguration.StartMenuHideHibernate 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideHibernate

### <a name="windows10generalconfigurationstartmenuhidelock"></a>Windows10GeneralConfiguration.StartMenuHideLock 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideLock

### <a name="windows10generalconfigurationstartmenuhidepowerbutton"></a>Windows10GeneralConfiguration.StartMenuHidePowerButton 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HidePowerButton

### <a name="windows10generalconfigurationstartmenuhiderecentjumplists"></a>Windows10GeneralConfiguration.StartMenuHideRecentJumpLists 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideRecentJumplists

### <a name="windows10generalconfigurationstartmenuhiderecentlyaddedapps"></a>Windows10GeneralConfiguration.StartMenuHideRecentlyAddedApps 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideRecentlyAddedApps

### <a name="windows10generalconfigurationstartmenuhiderestartoptions"></a>Windows10GeneralConfiguration.StartMenuHideRestartOptions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideRestart

### <a name="windows10generalconfigurationstartmenuhideshutdown"></a>Windows10GeneralConfiguration.StartMenuHideShutDown 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideShutDown

### <a name="windows10generalconfigurationstartmenuhidesignout"></a>Windows10GeneralConfiguration.StartMenuHideSignOut 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideSignOut

### <a name="windows10generalconfigurationstartmenuhidesleep"></a>Windows10GeneralConfiguration.StartMenuHideSleep 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideSleep

### <a name="windows10generalconfigurationstartmenuhideswitchaccount"></a>Windows10GeneralConfiguration.StartMenuHideSwitchAccount 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideSwitchAccount

### <a name="windows10generalconfigurationstartmenuhideusertile"></a>Windows10GeneralConfiguration.StartMenuHideUserTile 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/HideUserTile

### <a name="windows10generalconfigurationstartmenulayoutedgeassetsxml"></a>Windows10GeneralConfiguration.StartMenuLayoutEdgeAssetsXml 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/ImportEdgeAssets

### <a name="windows10generalconfigurationstartmenulayoutxml"></a>Windows10GeneralConfiguration.StartMenuLayoutXml 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/StartLayout

### <a name="windows10generalconfigurationstartmenumode"></a>Windows10GeneralConfiguration.StartMenuMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/ForceStartSize

### <a name="windows10generalconfigurationstartmenupinnedfolderdocuments"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderDocuments 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderDocuments

### <a name="windows10generalconfigurationstartmenupinnedfolderdownloads"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderDownloads 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderDownloads

### <a name="windows10generalconfigurationstartmenupinnedfolderfileexplorer"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderFileExplorer 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderFileExplorer

### <a name="windows10generalconfigurationstartmenupinnedfolderhomegroup"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderHomeGroup 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderHomeGroup

### <a name="windows10generalconfigurationstartmenupinnedfoldermusic"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderMusic 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderMusic

### <a name="windows10generalconfigurationstartmenupinnedfoldernetwork"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderNetwork 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderNetwork

### <a name="windows10generalconfigurationstartmenupinnedfolderpersonalfolder"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderPersonalFolder 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderPersonalFolder

### <a name="windows10generalconfigurationstartmenupinnedfolderpictures"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderPictures 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderPictures

### <a name="windows10generalconfigurationstartmenupinnedfoldersettings"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderSettings 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderSettings

### <a name="windows10generalconfigurationstartmenupinnedfoldervideos"></a>Windows10GeneralConfiguration.StartMenuPinnedFolderVideos 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Start/AllowPinnedFolderVideos

### <a name="windows10generalconfigurationstorageblockremovablestorage"></a>Windows10GeneralConfiguration.StorageBlockRemovableStorage 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/AllowStorageCard

### <a name="windows10generalconfigurationstoragerequiremobiledeviceencryption"></a>Windows10GeneralConfiguration.StorageRequireMobileDeviceEncryption 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Security/RequireDeviceCrypton

### <a name="windows10generalconfigurationstoragerestrictappdatatosystemvolume"></a>Windows10GeneralConfiguration.StorageRestrictAppDataToSystemVolume 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/RestrictAppDataToSystemVolume

### <a name="windows10generalconfigurationstoragerestrictappinstalltosystemvolume"></a>Windows10GeneralConfiguration.StorageRestrictAppInstallToSystemVolume 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/RestrictAppToSystemVolume

### <a name="windows10generalconfigurationsystembootstartdriverinitialization"></a>Windows10GeneralConfiguration.SystemBootStartDriverInitialization 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/BootStartDriverInitialization

### <a name="windows10generalconfigurationsystemtelemetryproxyserver"></a>Windows10GeneralConfiguration.SystemTelemetryProxyServer 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/System/TelemettryProxy

### <a name="windows10generalconfigurationtaskmanagerblockendtask"></a>Windows10GeneralConfiguration.TaskManagerBlockEndTask 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/TaskManager/AllowEndTask

### <a name="windows10generalconfigurationtenantlockdownrequirenetworkduringoutofboxexperience"></a>Windows10GeneralConfiguration.TenantLockdownRequireNetworkDuringOutOfBoxExperience 
**CSP**: ./Fornecedor/MSFT/Inquilino  
**Offset URI**: /RequireNetworkInOOBE

### <a name="windows10generalconfigurationusbblocked"></a>Windows10GeneralConfiguration.UsbBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Conectividade/AllowUSBConnection

### <a name="windows10generalconfigurationvoicerecordingblocked"></a>Windows10GeneralConfiguration.VoiceRecordingBlocked 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowVoiceRecording

### <a name="windows10generalconfigurationwebrtcblocklocalhostipaddress"></a>Windows10GeneralConfiguration.WebRtcBlockLocalhostIpAddress 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/PreventUsingLocalHostIPAddressForWebRTC

### <a name="windows10generalconfigurationwifiblockautomaticconnecthotspots"></a>Windows10GeneralConfiguration.WiFiBlockAutomaticConnectHotspots 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WiFi/AllowAutoConnectToWiSenseHotspots

### <a name="windows10generalconfigurationwifiblocked"></a>Windows10GeneralConfiguration.WiFiBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Wifi/AllowWiFi

### <a name="windows10generalconfigurationwifiblockmanualconfiguration"></a>Configuração manual do Windows10General.WiFiblock 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WiFi/AllowManualWiFi/Configuração

### <a name="windows10generalconfigurationwifiscaninterval"></a>Windows10GeneralConfiguration.WiFiScanInterval 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WiFi/WLANScanMode

### <a name="windows10generalconfigurationwindowslogonlocalusersondomainjoinedcomputers"></a>Windows10GeneralConfiguration.WindowsLogOnLocalUsersOnDomainJoinedComputers 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/WindowsLogon/EnumerateLocalUsersOnDomainJoinedComputers

### <a name="windows10generalconfigurationwindowsspotlightblockconsumerspecificfeatures"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockConsumerSpecificFeatures 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsConsumerFeatures

### <a name="windows10generalconfigurationwindowsspotlightblocked"></a>Windows10GeneralConfiguration.WindowsSpotlightBlocked 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsSpotlight

### <a name="windows10generalconfigurationwindowsspotlightblockonactioncenter"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockOnActionCenter 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsSpotlightOnActionCenter

### <a name="windows10generalconfigurationwindowsspotlightblocktailoredexperiences"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockTailoredExperiences 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowTailoredExperiences WithDiagnosticData

### <a name="windows10generalconfigurationwindowsspotlightblockthirdpartynotifications"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockThirdPartyNotifications 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowThirdPartySuggestionsInWindowsSpotlight

### <a name="windows10generalconfigurationwindowsspotlightblockwelcomeexperience"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockWelcomeExperience 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsSpotlightWindowsWelcomeExperience

### <a name="windows10generalconfigurationwindowsspotlightblockwindowstips"></a>Windows10GeneralConfiguration.WindowsSpotlightBlockWindowsTips 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/AllowWindowsTips

### <a name="windows10generalconfigurationwindowsspotlightconfigureonlockscreen"></a>Windows10GeneralConfiguration.WindowsSpotlightConfigureOnLockScreen 
**CSP**: ./Utilizador/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Experience/ConfigureWindowsSpotlightOnLockScreen

### <a name="windows10generalconfigurationwindowsstoreblockautoupdate"></a>Windows10GeneralConfiguration.WindowsStoreBlockAutoUpdate 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowAppStoreAutoUpdate

### <a name="windows10generalconfigurationwindowsstoreblocked"></a>Windows10GeneralConfiguration.WindowsStoreBlocked 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/AllowStore

### <a name="windows10generalconfigurationwindowsstoreenableprivatestoreonly"></a>Windows10GeneralConfiguration.WindowsStoreEnablePrivateStoreOnly 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/ApplicationManagement/RequirePrivateStoreOnly

### <a name="windows10generalconfigurationwirelessdisplayblockprojectiontothisdevice"></a>Windows10GeneralConfiguration.WirelessDisplayBlockProjectionToThisDevice 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WirelessDisplay/AllowProjectionToPC

### <a name="windows10generalconfigurationwirelessdisplayblockuserinputfromreceiver"></a>Windows10GeneralConfiguration.WirelessDisplayBlockUserInputFromReceiver 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver

### <a name="windows10generalconfigurationwirelessdisplayrequirepinforpairing"></a>Windows10GeneralConfiguration.WirelessDisplayRequirePinForPairing 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/WirelessDisplay/RequirePINForPairing

### <a name="windows10networkboundaryconfigurationwindowsnetworkisolationpolicy"></a>Windows10NetworkBoundaryConfiguration.WindowsNetworkIsolationPolicy 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/NetworkIsolation/EnterpriseCloudResources, /Config/NetworkIsolation/EnterpriseIPRange, /Config/NetworkIsolation/EnterpriseIPRangesAreAuthoritative, /Config/NetworkIsolation/EnterpriseInternalProxyServers, /Config/NetworkIsolation/EnterpriseNetworkDomainNames, /Config/NetworkIsolation/EnterpriseIsolation

### <a name="windows10policyoverrideconfigurationprefermdmovergrouppolicy"></a>Windows10PolicyOverrideConfiguration.PreferMdmOverGroupPolicy 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/ControlPolicyConflict/MDMWinsOverGP

### <a name="windows10secureassessmentconfigurationallowprinting"></a>Windows10SecureAssessmentConfiguration.AllowPrinting 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /Exigir Impressão

### <a name="windows10secureassessmentconfigurationallowscreencapture"></a>Windows10SecureAssessmentConfiguration.AllowScreenCapture 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /Permitir Monitorização do Ecrã

### <a name="windows10secureassessmentconfigurationallowtextsuggestion"></a>Windows10SecureAssessmentConfiguration.AllowTextSuggestion 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /PermitirSugestões de Texto

### <a name="windows10secureassessmentconfigurationconfigurationaccount"></a>Windows10SecureAssessmentConfiguration.ConfigurationAccount 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /TesterAccount

### <a name="windows10secureassessmentconfigurationconfigurationaccounttype"></a>Windows10SecureAssessmentConfiguration.ConfigurationAccountType 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /TesterAccount

### <a name="windows10secureassessmentconfigurationlaunchuri"></a>Windows10SecureAssessmentConfiguration.LaunchUri 
**CSP**: ./Fornecedor/MSFT/SecureAssessment  
**Offset URI**: /LaunchURI

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsblocktelemetry"></a>Windows10TeamGeneralConfiguration.AzureOperationalInsightsBlockTelemetry 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /MOMAgent/WorkspaceID e /MOMAgent/WorkspaceKey

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsworkspaceid"></a>Windows10TeamGeneralConfiguration.AzureOperationalInsightsWorkspaceId 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /MOMAgent/WorkspaceID

### <a name="windows10teamgeneralconfigurationazureoperationalinsightsworkspacekey"></a>Windows10TeamGeneralConfiguration.AzureOperationalInsightsWorkspaceKey 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /MOMAgent/WorkspaceKey

### <a name="windows10teamgeneralconfigurationconnectappblockautolaunch"></a>Windows10TeamGeneralConfiguration.ConnectAppBlockAutoLaunch 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InBoxApps/Connect/AutoLaunch

### <a name="windows10teamgeneralconfigurationdeviceaccountblockexchangeservices"></a>Windows10TeamGeneralConfiguration.DeviceAccountBlockExchangeServices 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /DeviceAccount/Email

### <a name="windows10teamgeneralconfigurationdeviceaccountemailaddress"></a>Windows10TeamGeneralConfiguration.DeviceAccountEmailAddress 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /DeviceAccount/Email

### <a name="windows10teamgeneralconfigurationdeviceaccountexchangeserveraddress"></a>Windows10TeamGeneralConfiguration.DeviceAccountExchangeServerAddress 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /DeviceAccount/ExchangeServer

### <a name="windows10teamgeneralconfigurationdeviceaccountrequirepasswordrotation"></a>Windows10TeamGeneralConfiguration.DeviceAccountRequirePasswordRotation 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /DeviceAccount/PasswordRotationEnabled

### <a name="windows10teamgeneralconfigurationdeviceaccountsessioninitiationprotocoladdress"></a>Windows10TeamGeneralConfiguration.DeviceAccountSessionInitiationProtocolAddress 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Deviceaccount/SipAddress

### <a name="windows10teamgeneralconfigurationmaintenancewindowblocked"></a>Windows10TeamGeneralConfiguration.MaintenanceWindowBlocked 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /ManutençãoHorasSimples/Horas/Duração e /ManutençãoHorasSimples/Horas/Início

### <a name="windows10teamgeneralconfigurationmaintenancewindowdurationinhours"></a>Windows10TeamGeneralConfiguration.MaintenanceWindowDurationInHours 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /ManutençãoHorasSimples/Horas/Duração

### <a name="windows10teamgeneralconfigurationmaintenancewindowstarttime"></a>Windows10TeamGeneralConfiguration.MaintenanceWindowStartTime 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /ManutençãoHorasSimples/Horas/Início

### <a name="windows10teamgeneralconfigurationmiracastblocked"></a>Windows10TeamGeneralConfiguration.MiracastBlocked 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InBoxApps/WirelessProjection/Ativado

### <a name="windows10teamgeneralconfigurationmiracastchannel"></a>Windows10TeamGeneralConfiguration.MiracastChannel 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InBoxApps/WirelessProjection/Channel

### <a name="windows10teamgeneralconfigurationmiracastrequirepin"></a>Windows10TeamGeneralConfiguration.MiracastRequirePin 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InBoxApps/WirelessProjection/PINRequired

### <a name="windows10teamgeneralconfigurationsettingsblockmymeetingsandfiles"></a>Windows10TeamGeneralConfiguration.SettingsBlockMyMeetingsAndFiles 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/DonotShowMyMeetingsAndFiles

### <a name="windows10teamgeneralconfigurationsettingsblocksessionresume"></a>Windows10TeamGeneralConfiguration.SettingsBlockSessionResume 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/AllowSessionResume

### <a name="windows10teamgeneralconfigurationsettingsblocksigninsuggestions"></a>Windows10TeamGeneralConfiguration.SettingsBlockSigninSuggestions 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/Sugestões de Desativação

### <a name="windows10teamgeneralconfigurationsettingsdefaultvolume"></a>Windows10TeamGeneralConfiguration.SettingsDefaultVolume 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/Volume Predefinido

### <a name="windows10teamgeneralconfigurationsettingsscreentimeoutinminutes"></a>Windows10TeamGeneralConfiguration.SettingsScreenTimeoutInMinutes 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/ScreenTimeout

### <a name="windows10teamgeneralconfigurationsettingssessiontimeoutinminutes"></a>Windows10TeamGeneralConfiguration.SettingsSessionTimeoutInMinutes 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/SessionTimeout

### <a name="windows10teamgeneralconfigurationsettingssleeptimeoutinminutes"></a>Windows10TeamGeneralConfiguration.SettingsSleepTimeoutInMinutes 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Propriedades/SleepTimeout

### <a name="windows10teamgeneralconfigurationwelcomescreenbackgroundimageurl"></a>Windows10TeamGeneralConfiguration.WelcomeScreenBackgroundImageUrl 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /Inboxapps/Welcome/CurrentbackgroundPath

### <a name="windows10teamgeneralconfigurationwelcomescreenblockautomaticwakeup"></a>Windows10TeamGeneralConfiguration.WelcomeScreenBlockAutomaticWakeUp 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InboxApps/Welcome/AutoWakeScreen

### <a name="windows10teamgeneralconfigurationwelcomescreenmeetinginformation"></a>Windows10TeamGeneralConfiguration.WelcomeScreenMeetingInformation 
**CSP**: ./Fornecedor/MSFT/Surfacehub  
**Offset URI**: /InboxApps/Welcome/MeetingInfoOption

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectionoffboardingblob"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOffboardingBlob 
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Offboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectionoffboardingfilename"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOffboardingFilename
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Offboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectiononboardingblob"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOnboardingBlob 
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Onboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationadvancedthreatprotectiononboardingfilename"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOnboardingFilename 
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Onboarding 

### <a name="windowsdefenderadvancedthreatprotectionconfigurationallowsamplesharing"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.AllowSampleSharing 
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Configuração/Partilha de Amostras

### <a name="windowsdefenderadvancedthreatprotectionconfigurationenableexpeditedtelemetryreporting"></a>WindowsDefenderAdvancedThreatProtectionConfiguration.EnableExpeditedTelemetryReporting 
**CSP**: ./Dispositivo/fornecedor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Configuração/TelemetriaReportingFrequency

### <a name="windowsdeliveryoptimizationconfigurationdeliveryoptimizationmode"></a>WindowsDeliveryOptimizationConfiguration.DeliveryOptimizationMode 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeliveryOptimization/DODownloadMode

### <a name="windowsidentityprotectionconfigurationenhancedantispoofingforfacialfeaturesenabled"></a>WindowsIdentityProtectionConfiguration.EnhancedAntiSpoofingForFacialFeaturesEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/PassportForWork  
**Offset URI**: /Biometrics/FacialFeaturesUseEnhancedAntiSpoofing

### <a name="windowsidentityprotectionconfigurationpinexpirationindays"></a>WindowsIdentityProtectionConfiguration.PinExpirationInDays 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/Expiration

### <a name="windowsidentityprotectionconfigurationpinlowercasecharactersusage"></a>WindowsIdentityProtectionConfiguration.PinLowercaseCharactersUsage 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/LowercaseLetters

### <a name="windowsidentityprotectionconfigurationpinmaximumlength"></a>WindowsIdentityProtectionConfiguration.PinMaximumLength 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/MaximumPINLength

### <a name="windowsidentityprotectionconfigurationpinminimumlength"></a>WindowsIdentityProtectionConfiguration.PinMinimumLength 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/MinimumPINLength

### <a name="windowsidentityprotectionconfigurationpinpreviousblockcount"></a>WindowsIdentityProtectionConfiguration.PinPreviousBlockCount 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/History

### <a name="windowsidentityprotectionconfigurationpinrecoveryenabled"></a>WindowsIdentityProtectionConfiguration.PinRecoveryEnabled 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AadTenantid}/Policies/EnablepinRecovery

### <a name="windowsidentityprotectionconfigurationpinspecialcharactersusage"></a>WindowsIdentityProtectionConfiguration.PinSpecialCharactersUsage 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/SpecialCharacters

### <a name="windowsidentityprotectionconfigurationpinuppercasecharactersusage"></a>WindowsIdentityProtectionConfiguration.PinUppercaseCharactersUsage
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/UppercaseLetters

### <a name="windowsidentityprotectionconfigurationsecuritydevicerequired"></a>WindowsIdentityProtectionConfiguration.SecurityDeviceRequired 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AadTenantid}/Policies/RequireSecurityDevice

### <a name="windowsidentityprotectionconfigurationunlockwithbiometricsenabled"></a>WindowsIdentityProtectionConfiguration.UnlockWithBiometricsEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/PassportForWork  
**Offset URI**: /Biometria/UtilizaçãoBios

### <a name="windowsidentityprotectionconfigurationusecertificatesforonpremisesauthenabled"></a>WindowsIdentityProtectionConfiguration.UseCertificatesForOnPremisesAuthEnabled 
**CSP**: ./Dispositivo/Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/UseCertificateForOnPremAuth

### <a name="windowsidentityprotectionconfigurationwindowshelloforbusinessblocked"></a>WindowsIdentityProtectionConfiguration.WindowsHelloForBusinessBlocked 
**CSP**: ./Fornecedor/MSFT/PassportForWork  
**Offset URI**: /{AadTenantid}/Policies/UsePassportForWork

### <a name="windowskioskconfigurationedgekioskenablepublicbrowsing"></a>WindowsKioskConfiguration.EdgeKioskEnablePublicBrowsing 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureKioskMode

### <a name="windowskioskconfigurationedgekioskresetafteridletimeinminutes"></a>WindowsKioskConfiguration.EdgeKioskResetAfterIdleTimeInMinutes 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Browser/ConfigureKioskResetAfterIdleTimeout

### <a name="windowskioskconfigurationkioskbrowserblockedurlexceptions"></a>WindowsKioskConfiguration.KioskBrowserBlockedUrlExceptions 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/BlockedUrlExceptions

### <a name="windowskioskconfigurationkioskbrowserblockedurls"></a>WindowsKioskConfiguration.KioskBrowserBlockedURLs 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/BlockedUrls

### <a name="windowskioskconfigurationkioskbrowserdefaulturl"></a>WindowsKioskConfiguration.KioskBrowserDefaultUrl 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/DefaultUrl

### <a name="windowskioskconfigurationkioskbrowserenableendsessionbutton"></a>WindowsKioskConfiguration.KioskBrowserEnableEndSessionButton 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/EnableEndSessionButton

### <a name="windowskioskconfigurationkioskbrowserenablehomebutton"></a>WindowsKioskConfiguration.KioskBrowserEnableHomeButton 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/EnableHomeButton

### <a name="windowskioskconfigurationkioskbrowserenablenavigationbuttons"></a>WindowsKioskConfiguration.KioskBrowserEnableNavigationButtons 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/EnableNavigationButtons

### <a name="windowskioskconfigurationkioskbrowserrestartonidletimeinminutes"></a>WindowsKioskConfiguration.KioskBrowserRestartOnIdleTimeInMinutes 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/KioskBrowser/KioskBrowserRestartOnIdleTimeInMinutes

### <a name="windowsupdateforbusinessconfigurationautomaticupdatemode"></a>WindowsUpdateForBusinessConfiguration.AutomaticUpdateMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/AllowAutoUpdate

### <a name="windowsupdateforbusinessconfigurationautorestartnotificationdismissal"></a>WindowsUpdateForBusinessConfiguration.AutoRestartNotificationDismissal 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/AutoRestartRequiredNotificationDismissal

### <a name="windowsupdateforbusinessconfigurationbusinessreadyupdatesonly"></a>WindowsUpdateForBusinessConfiguration.BusinessReadyUpdatesOnly 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/BranchReadinessLevel

### <a name="windowsupdateforbusinessconfigurationdeliveryoptimizationmode"></a>WindowsUpdateForBusinessConfiguration.DeliveryOptimizationMode 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/DeliveryOptimization/DODownloadMode

### <a name="windowsupdateforbusinessconfigurationdriversexcluded"></a>WindowsUpdateForBusinessConfiguration.DriversExcluded 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/ExcludeWUDriversInQualityUpdate

### <a name="windowsupdateforbusinessconfigurationengagedrestartdeadlineforfeatureupdatesindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartDeadlineForFeatureUpdatesInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartDeadlineForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestartdeadlineindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartDeadlineInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartDeadline

### <a name="windowsupdateforbusinessconfigurationengagedrestartsnoozescheduleforfeatureupdatesindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartSnoozeScheduleForFeatureUpdatesInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartSnoozeScheduleForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestartsnoozescheduleindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartSnoozeScheduleInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartSnoozeSchedule

### <a name="windowsupdateforbusinessconfigurationengagedrestarttransitionscheduleforfeatureupdatesindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartTransitionScheduleForFeatureUpdatesInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartTransitionScheduleForFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationengagedrestarttransitionscheduleindays"></a>WindowsUpdateForBusinessConfiguration.EngagedRestartTransitionScheduleInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/EngagedRestartTransitionSchedule

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesdeferralperiodindays"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesDeferralPeriodInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/DeferFeatureUpdatesPeriodInDays

### <a name="windowsupdateforbusinessconfigurationfeatureupdatespaused"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesPaused 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/PauseFeatureUpdates

### <a name="windowsupdateforbusinessconfigurationfeatureupdatespausestartdatetime"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesPauseStartDateTime 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/PauseFeatureUpdatesStartTime

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesrollbackstartdatetime"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesRollbackStartDateTime
**CSP**: N/A - Gráfico API apenas **Offset URI**: N/A - Apenas gráfico API

### <a name="windowsupdateforbusinessconfigurationfeatureupdateswillberolledback"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesWillBeRolledBack 
**CSP**: N/A - Gráfico API apenas **Offset URI**: N/A - Apenas gráfico API

### <a name="windowsupdateforbusinessconfigurationfeatureupdatesrollbackwindowindays"></a>WindowsUpdateForBusinessConfiguration.FeatureUpdatesRollbackWindowInDays
**CSP**: N/A - Gráfico API apenas **Offset URI**: N/A - Apenas gráfico API

### <a name="windowsupdateforbusinessconfigurationinstallationschedule"></a>WindowsUpdateForBusinessConfiguration.InstallationSchedule
**CSP**: ./Dispositivo/Fornecedor/MSFT/Policy **Offset URI**: /Config/Update/ActiveHoursStart, /Config/Update/ActiveHoursEnd, /Config/Update/ScheduledInstallDay, /Config/Update/ScheduledInstallTime

### <a name="windowsupdateforbusinessconfigurationmicrosoftupdateserviceallowed"></a>WindowsUpdateForBusinessConfiguration.MicrosoftUpdateServiceAllowed 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/AllowMUUpdateService

### <a name="windowsupdateforbusinessconfigurationpreviewbuildsetting"></a>WindowsUpdateForBusinessConfiguration.PreviewBuildSetting 
**CSP**: ./Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/ManagePreviewBuilds

### <a name="windowsupdateforbusinessconfigurationqualityupdatesdeferralperiodindays"></a>WindowsUpdateForBusinessConfiguration.QualityUpdatesDeferralPeriodInDays 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/DeferQualityUpdatesPeriodInDays

### <a name="windowsupdateforbusinessconfigurationqualityupdatespaused"></a>WindowsUpdateForBusinessConfiguration.QualityUpdatesPaused 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Updates/PauseQualityUpdates

### <a name="windowsupdateforbusinessconfigurationqualityupdatespausestartdatetime"></a>WindowsUpdateForBusinessConfiguration.QualityUpdatesPauseStartDateTime 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/PauseQualityUpdatesStartTime

### <a name="windowsupdateforbusinessconfigurationqualityupdatesrollbackstartdatetime"></a>WindowsUpdateForBusinessConfiguration.QualityUpdatesRollbackStartDateTime
**CSP**: N/A - Gráfico API apenas **Offset URI**: N/A - Apenas gráfico API

### <a name="windowsupdateforbusinessconfigurationqualityupdateswillberolledback"></a>WindowsUpdateForBusinessConfiguration.QualityUpdatesWillBeRolledBack 
**CSP**: N/A - Gráfico API apenas **Offset URI**: N/A - Apenas gráfico API

### <a name="windowsupdateforbusinessconfigurationscheduleimminentrestartwarninginminutes"></a>WindowsUpdateForBusinessConfiguration.ScheduleImminentRestartWarningInMinutes 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/ScheduleIminenteRestartWarning

### <a name="windowsupdateforbusinessconfigurationschedulerestartwarninginhours"></a>WindowsUpdateForBusinessConfiguration.ScheduleRestartWarningInHours 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/ScheduleRestartWarning

### <a name="windowsupdateforbusinessconfigurationskipchecksbeforerestart"></a>WindowsUpdateForBusinessConfiguration.SkipChecksBeforeRestart 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/SetEDURestart

### <a name="windowsupdateforbusinessconfigurationupdateweeks"></a>WindowsUpdateForBusinessConfiguration.UpdateWeeks 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/ScheduledInstallEveryWeek, /Config/Update/ScheduledInstallFirstWeek, /Config/Update/ScheduledInstallFourthWeek

### <a name="windowsupdateforbusinessconfigurationuserpauseaccess"></a>WindowsUpdateForBusinessConfiguration.UserPauseAccess 
**CSP**: ./Dispositivo/Fornecedor/MSFT/Política  
**Offset URI**: /Config/Update/SetDisablePauseUXAccess


## <a name="next-steps"></a>Próximos passos

- [Visão geral da configuração do dispositivo](../configuration/device-profiles.md)
- Referência do prestador de serviços de [configuração](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference) (abre outro site do Docs)
