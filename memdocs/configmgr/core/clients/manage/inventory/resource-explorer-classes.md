---
title: Aulas de inventário padrão do Explorador de Recursos
titleSuffix: Configuration Manager
description: Mostra as classes que aparecem no Explorador de Recursos
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710735"
---
# <a name="resource-explorer-default-inventory-classes"></a>Aulas de inventário padrão do Explorador de Recursos

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve as classes de inventário padrão no Resource Explorer.

Estas são as classes de inventário padrão:

## <a name="1394-controller"></a>Controlador de 1394

Espaço de nome: raiz\cimv2

Win32_1394Controller de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="account-sid"></a>Conta SID

Espaço de nome: raiz\cimv2

Win32_AccountSID de classe

- (Corda) Elemento

- (Corda) Definição



## <a name="activesync-service"></a>Serviço ActiveSync

Espaço de nome: raiz\SmsDm

SMS_ActiveSyncService de classe


- (UInt32) Grandeversão

- (UInt32) Versão Menor

- (Corda) Última Sincronização



## <a name="amt-agent"></a>Agente AMT

Espaço de nome: root\cimv2\sms

SMS_AMTObject de classe


- (UInt32) DispositivoID

- (Corda) AMT

- (Corda) AMTApps

- (Corda) BiosVersão

- (Corda) Número de construção

- (Corda) Flash

- (Corda) LegacyMode

- (Corda) Netstack

- (UInt32) Modo de Provisiono

- (UInt32) Estado de Provision

- (Corda) RecoveryBuildnum

- (Corda) Versão de Recuperação

- (Corda) Rio Sku

- (UInt32) Rio TLSMode

- (Corda) FornecedorID

- (UInt32) ZTCEnabled



## <a name="appv-client-application"></a>Aplicação do cliente AppV

Espaço de nome: root\AppV

classe AppvClientApplication


- (Corda) Aplicação

- (Corda) Packageid

- (Corda) PackageVersionId

- (Boolean) Utilizador Ativo

- (Boolean) Habilitado Globalmente

- (Corda) Nome

- (Corda) Caminho-alvo

- (Corda) Versão



## <a name="appv-client-package"></a>Pacote de cliente AppV

Espaço de nome: root\AppV

classe AppvClientPackage


- (Corda) Packageid

- (Corda) VersãoId

- (Corda) Ativos[]

- (Corda) ImplementaçãoMachineData

- (Corda) ImplementaçãoUserData

- (Boolean) HasAssetIntelligence

- (Boolean) Inutilização

- (Boolean) IsPublishedGlobally

- (Boolean) IsPublishedToUser

- (Corda) Nome

- (UInt64) Tamanho do pacote

- (Corda) Caminho

- (UInt16) PercentLoaded

- (Corda) UserConfigurationData

- (Corda) Versão



## <a name="autostart-software"></a>AutoStart Software

Espaço de nome: root\cimv2\sms

SMS_AutoStartSoftware de classe


- (Corda) FilePropertiesHash

- (Corda) Versão binfile

- (Corda) Versão binproduct

- (Corda) Descrição

- (Corda) Nome de ficheiro

- (Corda) FilePropertiesHashEx

- (Corda) Versão de Ficheiros

- (Corda) Localização

- (Corda) Produto

- (Corda) Versão do Produto

- (Corda) Editora

- (Corda) StartupType

- (Corda) StartupValue



## <a name="baseboard"></a>Placa de Base

Espaço de nome: raiz\cimv2

Win32_BaseBoard de classe


- (Corda) Etiqueta

- (Corda) Legenda

- (Corda) ConfigOptions[]

- (Corda) Descrição

- (Boolean) Conselho de Acolhimento

- (Boolean) HotSwappable

- (Data) Data de Instalação

- (Corda) Fabricante

- (Corda) Modelo

- (Corda) Nome

- (Corda) OutraS Informações Identificantes

- (Corda) PartNumber

- (Boolean) PoweredOn

- (Corda) Produto

- (Boolean) Removível

- (Boolean) Substituível

- (Corda) RequisitosDescrição

- (Boolean) Requer DaughterBoard

- (Corda) Número de série

- (Corda) SKU

- (Corda) SlotLayout

- (Boolean) Requisitos Especiais

- (Corda) Estado

- (Corda) Versão



## <a name="battery"></a>Bateria

Espaço de nome: raiz\cimv2

Win32_Battery de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt16) Situação de Bateria

- (Corda) Legenda

- (UInt16) Química

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt32) Capacidade de Design

- (UInt64) DesignVoltage

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt16) Custo estimadoRemaining

- (UInt32) Tempo estimado

- (UInt32) Vida esperada

- (UInt32) FullChargeCapacity

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (UInt32) Hora máxima

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Versão SmartBattery

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (UInt32) TimeOnBattery

- (UInt32) TimetoFullCharge



## <a name="bitlocker"></a>BitLocker

Espaço de nome: root\cimv2\security\MicrosoftVolumeEncryption

Win32_EncryptableVolume de classe


- (Corda) DispositivoID

- (Corda) Carta de condução

- (Corda) PersistenteVolumeID

- (UInt32) Estatuto de Proteção



## <a name="bitlocker-encryption-details"></a>Detalhes de encriptação BitLocker

Espaço de nome: raiz\cimv2

Win32_BitLockerEncryptionDetails de classe


- (Corda) BitlockerPersistentVolumeId

- (SInt32) Conforme

- (SInt32) Estatuto de Conversão

- (Corda) Dispositivoid

- (Corda) Carta de condução

- (SInt32) Método de encriptação

- (Corda) Data de Aplicação da Política

- (Boolean) IsAutoUnlockEnabled

- (SInt32) Protetores de chaves[]

- (Corda) MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- (Corda) Não complianceDetectadaData

- (SInt32) Estatuto de Proteção

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>Política BitLocker

Espaço de nome: raiz\cimv2

Win32Reg_MBAMPolicy de classe


- (Corda) Nome de computador codificado

- (UInt32) Método de encriptação

- (UInt32) FixedDataDriveAutoUnlock

- (UInt32) Encriptação FixedDataDrive

- (UInt32) Frase de PassedeDrive FixedData

- (Corda) Nome-chave

- (Corda) ÚltimaConsolaUser

- (UInt32) Erro MBAMMachine

- (UInt32) MBAMPolicyEnforced

- (UInt32) OsDriveEncryption

- (UInt32) OsDriveProtector

- (Data) Data de Isenção de Utilizadores



## <a name="boot-configuration"></a>Configuração do arranque

Espaço de nome: raiz\cimv2

Win32_BootConfiguration de classe


- (Corda) Nome

- (Corda) BootDirectory

- (Corda) Caminho de Configuração

- (Corda) Descrição

- (Corda) LastDrive

- (Corda) ScratchDirectory

- (Corda) SettingID

- (Corda) TempDirectory



## <a name="browser-helper-object"></a>Objeto de ajudante de navegador

Espaço de nome: root\cimv2\sms

SMS_BrowserHelperObject de classe


- (Corda) FilePropertiesHash

- (Corda) Versão binfile

- (Corda) Versão binproduct

- (Corda) CLSID

- (Corda) Descrição

- (Corda) Nome de ficheiro

- (Corda) FilePropertiesHashEx

- (Corda) Versão de Ficheiros

- (Corda) Produto

- (Corda) Versão do Produto

- (Corda) Editora

- (Corda) Versão



## <a name="ccm_rax"></a>CCM_RAX

Espaço de nome: root\ccm\cimodels

CCM_RAXInfo de classe


- (Corda) AppID

- (Corda) FeedURL

- (Corda) UserSID



## <a name="cd-rom"></a>CD-ROM

Espaço de nome: raiz\cimv2

Win32_CDROMDrive de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (Corda) Método de Compressão

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt64) Tamanho de bloqueio predefinido

- (Corda) Descrição

- (Corda) Conduzir

- (Boolean) Integridade da unidade

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (UInt16) Bandeiras do Sistema de Ficheiros

- (UInt32) FileSystemFlagsEx

- (Corda) ID

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt64) Tamanho MaxBlock

- (UInt32) Comprimento máximo de componente

- (UInt64) MaxMediaSize

- (Boolean) MediaLoaded

- (Corda) MediaType

- (UInt64) Tamanho MinBlockSize

- (Corda) Nome

- (Boolean) NecessidadesLimpeza

- (UInt32) NumberOfMediaSupported

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Nível de Revisão

- (UInt32) SCSIBus

- (UInt16) Unidade Scsilógica

- (UInt16) SCSIPort

- (UInt16) Scsitargetid

- (UInt64) Tamanho

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Corda) Nome de volume

- (Corda) VolumeSerialNumber



## <a name="client-events"></a>Eventos de Clientes

Espaço de nome: raiz\ccm\invagt

classe ClientesEventos


- (Corda) Nome de evento

- (UInt16) Contagem



## <a name="computer-system"></a>Sistema de Computador

Espaço de nome: raiz\cimv2

Win32_ComputerSystem de classe


- (Corda) Nome

- (UInt16) AdminPasswordStatus

- (Boolean) Opção Automatic ResetBoot

- (Boolean) Capacidade de Reset Automático

- (UInt16) BootOptionOnLimit

- (UInt16) BootOptionOnWatchDog

- (Boolean) BootROMSuportaed

- (Corda) Estado de Arranque

- (Corda) Legenda

- (UInt16) ChassisBootupState

- (SInt16) AtualTimeZone

- (Boolean) Efeito daylightin

- (Corda) Descrição

- (Corda) Domínio

- (UInt16) DomínioRole

- (UInt16) FrontPanelResetStatus

- (Boolean) InfraredSupported

- (Corda) InicialLoadInfo[]

- (Data) Data de Instalação

- (UInt16) Estatuto de Palavra-passe do teclado

- (Corda) LastLoadInfo

- (Corda) Fabricante

- (Corda) Modelo

- (Corda) Formato de Nome

- (Boolean) Modo de Servidor de Rede

- (UInt32) NumberOfProcessadores

- (Corda) Mapa OEMLogoBitmap

- (Corda) OEMStringArray[]

- (SInt64) Pausa AfterReset

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) PowerOnPasswordStatus

- (UInt16) Estado-Poder

- (UInt16) PowerSupplyState

- (Corda) PrimaryOwnerContact

- (Corda) Nome principal proprietário

- (UInt16) ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- (Corda) Funções[]

- (Corda) Estado

- (Corda) Descrição do Contacto de Suporte[]

- (UInt16) Atraso do Arranque do Sistema

- (Corda) SystemStartupOptions[]

- (UInt8) SystemStartupSetting

- (Corda) SystemType

- (UInt16) Estado Termal

- (UInt64) Memória Total Física

- (Corda) Nome de utilizador

- (UInt16) WakeUpType



## <a name="computer-system-ex"></a>Sistema informático Ex

Espaço de nome: raiz\cimv2

CCM_ComputerSystemExtended de classe


- (Corda) Nome

- (UInt16) PCSystemType



## <a name="computer-system-product"></a>Produto do sistema informático

Espaço de nome: raiz\cimv2

Win32_ComputerSystemProduct de classe


- (Corda) Número de identificação

- (Corda) Nome

- (Corda) Versão

- (Corda) Legenda

- (Corda) Descrição

- (Corda) Número SKU

- (Corda) UUID

- (Corda) Fornecedor



## <a name="sms-advanced-client-ports"></a>Portas avançadas de clientes SMS

Espaço de nome: raiz\cimv2

Win32Reg_SMSAdvancedClientPorts de classe


- (Corda) InstânciaChave

- (UInt32) Nome httpsport

- (UInt32) Nome de porta



## <a name="sms-advanced-client-ssl-configurations"></a>Configurações SMS Avançadas do Cliente SSL

Espaço de nome: raiz\cimv2

Win32Reg_SMSAdvancedClientSSLConfiguration de classe


- (Corda) InstânciaChave

- (Corda) Critérios de Seleção de Certificados

- (Corda) Loja de Certificados

- (UInt32) ClientAlwaysOnInternet

- (UInt32) Bandeiras do Estado

- (Corda) Nome de anfitrião do InternetMP

- (UInt32) SelecioneFirstCertificate



## <a name="sms-advanced-client-state"></a>SMS Avançado Estado cliente

Espaço de nome: raiz\ccm

CCM_InstalledComponent de classe


- (Corda) Nome

- (Corda) Nome do ecrã

- (Corda) Versão



## <a name="connected-device"></a>Dispositivo Conectado

Espaço de nome: raiz\SmsDm

SMS_ActiveSyncConnectedDevice de classe


- (Corda) DeviceOEMInfo

- (Corda) Tipo de dispositivo

- (Corda) OS_Major

- (Corda) OS_Minor

- (Corda) OS_Platform

- (Corda) Arquitetura de Processadores

- (Corda) Nível de processador

- (Corda) Revisão de processadores

- (Corda) ClienteID instalado

- (Corda) Servidor de Cliento instalado

- (Corda) Versão de Cliento Instalada

- (Corda) Última Sincronização

- (Corda) OS_AdditionalInfo

- (Corda) OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

Espaço de nome: root\cimv2\sms

SMS_DefaultBrowser de classe


- (Corda) BrowserProgId



## <a name="desktop"></a>Ambiente de trabalho

Espaço de nome: raiz\cimv2

Win32_Desktop de classe


- (Corda) Nome

- (UInt32) Largura de Fronteira

- (Corda) Legenda

- (Boolean) CoolSwitch

- (UInt32) CursorBlinkRate

- (Corda) Descrição

- (Boolean) DragFullWindows

- (UInt32) GridGranularity

- (UInt32) IconSpacing

- (Corda) Nome do nome do icontitleFace

- (UInt32) Tamanho do título de ícone

- (Boolean) IconTitleWrap

- (Corda) Padrão

- (Boolean) ScreenSaverActive

- (Corda) ScreenSaverExecutável

- (Boolean) ScreenSaverSecure

- (UInt32) ScreenSaverTimeout

- (Corda) SettingID

- (Corda) Papel de parede

- (Boolean) Papel de parede Esticado

- (Boolean) Papel de paredeTiled



## <a name="desktop-monitor"></a>Monitor de ambiente de trabalho

Espaço de nome: raiz\cimv2

Win32_DesktopMonitor de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt32) Largura de banda

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt16) Tipo de visualização

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (Boolean) IsLocked

- (UInt32) Código de Erro

- (Corda) MonitorFabricante

- (Corda) MonitorType

- (Corda) Nome

- (UInt32) PixelsPerXLogicalInch

- (UInt32) PixelsPerYLogicalInch

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt32) Altura do ecrã

- (UInt32) Largura do ecrã

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema



## <a name="device-info"></a>Informações do dispositivo

Espaço de nome: Reservado

Device_Info de classe


- (Corda) CertExpiry

- (Corda) Nome do dispositivo

- (Corda) Fabricante

- (Corda) Modelo

- (Corda) OS



## <a name="mdm-devdetail"></a>MDM DevDetail

Espaço de nome: root\cimv2\mdm\dmmap

MDM_DevDetail_Ext01 de classe


- (Corda) Instância

- (Corda) Parentalid

- (Corda) DeviceHardwareData

- (Corda) Endereço WLANMAC



## <a name="disk"></a>Disco

Espaço de nome: raiz\cimv2

Win32_DiskDrive de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt32) BytesPerSector

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (Corda) Método de Compressão

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt64) Tamanho de bloqueio predefinido

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (UInt32) Índice

- (Data) Data de Instalação

- (Corda) InterfaceType

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt64) Tamanho MaxBlock

- (UInt64) MaxMediaSize

- (Boolean) MediaLoaded

- (Corda) MediaType

- (UInt64) Tamanho MinBlockSize

- (Corda) Modelo

- (Corda) Nome

- (Boolean) NecessidadesLimpeza

- (UInt32) NumberOfMediaSupported

- (UInt32) Divisórias

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt32) SCSIBus

- (UInt16) Unidade Scsilógica

- (UInt16) SCSIPort

- (UInt16) Scsitargetid

- (UInt32) SectoresPerTrack

- (UInt64) Tamanho

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (UInt64) Cilindros Totais

- (UInt32) Cabeças Totais

- (UInt64) TotalSectores

- (UInt64) TotalTracks

- (UInt32) Cilindro de Faixas



## <a name="partition"></a>Partição

Espaço de nome: raiz\cimv2

Win32_DiskPartition de classe


- (Corda) DispositivoID

- (UInt16) Acesso

- (UInt16) Disponibilidade

- (UInt64) BlockSize

- (Boolean) Sabotável

- (Boolean) Partição de Botas

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt32) DiskIndex

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (UInt32) Sectores Escondidos

- (UInt32) Índice

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Nome

- (UInt64) NumberOfBlocks

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Boolean) Partição Primária

- (Corda) Propósito

- (Boolean) Reescrever Partição

- (UInt64) Tamanho

- (UInt64) StartOffset

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Corda) Tipo



## <a name="dma"></a>DMA

Espaço de nome: raiz\cimv2

Win32_DeviceMemoryAddress de classe

- (UInt64) Endereço inicial

- (Corda) Legenda

- (Corda) Descrição

- (UInt64) Endereço final

- (Data) Data de Instalação

- (Corda) Tipo de memória

- (Corda) Nome

- (Corda) Estado



## <a name="dma-channel"></a>Canal DMA

Espaço de nome: raiz\cimv2

Win32_DMAChannel de classe


- (UInt32) Canal DMA

- (UInt16) Endereçotamanho

- (UInt16) Disponibilidade

- (Boolean) Modo BurstMode

- (UInt16) ByteMode

- (Corda) Legenda

- (UInt16) ChannelTiming

- (Corda) Descrição

- (Data) Data de Instalação

- (UInt32) Tamanho MaxTransfer

- (Corda) Nome

- (UInt32) Porto

- (Corda) Estado

- (UInt16) Larguras de transferência[]

- (UInt16) Tipoctiming

- (UInt16) WordMode



## <a name="driver---vxd"></a>Condutor - VxD

Espaço de nome: raiz\cimv2

Win32_DriverVXD de classe


- (Corda) Nome

- (Corda) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) Sistema de Operações de Alvo

- (Corda) Versão

- (Corda) Número de construção

- (Corda) Legenda

- (Corda) Conjunto de Códigos

- (Corda) Controlo

- (Corda) Descrição

- (Corda) DeviceDescriptorBlock

- (Corda) Código de Identificação

- (Data) Data de Instalação

- (Corda) Edição linguística

- (Corda) Fabricante

- (Corda) Outros TargetOS

- (Corda) PM_API

- (Corda) Número de série

- (UInt32) Tamanho de serviço

- (Corda) Estado

- (Corda) V86_API



## <a name="embedded-device-information"></a>Informações do dispositivo incorporado

Espaço de nome: root\cimv2\sms

CCM_EmbeddedDeviceInformation de classe


- (Corda) Tipo de dispositivo

- (Corda) Modelo

- (Corda) Nome oem



## <a name="environment"></a>Ambiente

Espaço de nome: raiz\cimv2

Win32_Environment de classe


- (Corda) Nome

- (Corda) Nome de utilizador

- (Corda) Legenda

- (Corda) Descrição

- (Data) Data de Instalação

- (Corda) Estado

- (Boolean) Variável do sistema

- (Corda) Valor Variável



## <a name="firmware"></a>Firmware

Espaço de nome: root\cimv2\sms

SMS_Firmware de classe


- (Boolean) UEFI

- (Boolean) SecureBoot



## <a name="usm-folder-redirection-health"></a>Saúde de redirecionamento da pasta USM

Espaço de nome: root\cimv2\sms

SMS_FolderRedirectionHealth de classe


- (Corda) Nome da pasta

- (Corda) SID

- (UInt8) Estado de Saúde

- (Data) ÚltimaS Inscréis

- (UInt8) LastSyncStatus

- (Data) Última Sincronização

- (Boolean) OfflineAccessEnabled

- (Corda) OfflineFileNameFolderguid

- (Boolean) Redirecionado



## <a name="ide-controller"></a>Controlador IDE

Espaço de nome: raiz\cimv2

Win32_IDEController de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="add-remove-programs-64"></a>Adicionar Programas de Remoção (64)

Espaço de nome: raiz\cimv2

Win32Reg_AddRemovePrograms64 de classe


- (Corda) ProdID

- (Corda) Nome do ecrã

- (Corda) Data de Instalação

- (Corda) Editora

- (Corda) Versão



## <a name="add-remove-programs"></a>Adicionar Programas de Remoção

Espaço de nome: raiz\cimv2

Win32Reg_AddRemovePrograms de classe


- (Corda) ProdID

- (Corda) Nome do ecrã

- (Corda) Data de Instalação

- (Corda) Editora

- (Corda) Versão



## <a name="installed-executable"></a>Executável instalado

Espaço de nome: root\cimv2\sms

SMS_InstalledExecutable de classe


- (Corda) Nome executável

- (Corda) Código de Produto

- (Corda) Versão binfile

- (Corda) Versão binproduct

- (Corda) Descrição

- (Corda) FilePropertiesHash

- (Corda) FilePropertiesHashEx

- (UInt32) Tamanho de ficheiro

- (Corda) Versão de Ficheiros

- (Boolean) Haspatchadded

- (Corda) InstaladoFilePath

- (Boolean) Ficheiro IsSystem

- (Boolean) IsVitalFile

- (UInt32) Língua

- (Corda) Produto

- (Corda) Versão do Produto

- (Corda) Editora



## <a name="installed-software"></a>Software instalado

Espaço de nome: root\cimv2\sms

SMS_InstalledSoftware de classe


- (Corda) Código de Software

- (Corda) Nome ARPDisplay

- (Corda) Código do Canal

- (Corda) CanalID

- (Corda) CM_DSLID

- (Corda) EvidenceSource

- (Data) Data de Instalação

- (UInt32) InstalaçãoValidação de Directory

- (Corda) Localização Instalada

- (Corda) InstalarSource

- (UInt32) Tipo de instalação

- (UInt32) Língua

- (Corda) Pacote Local

- (Corda) MPC

- (UInt32) OsComponent

- (Corda) Código de Pacote

- (Corda) ProductID

- (Corda) Nome do produto

- (Corda) Versão do Produto

- (Corda) Editora

- (Corda) RegistradoUser

- (Corda) ServicePack

- (Corda) SoftwarePropertiesHash

- (Corda) SoftwarePropertiesHashEx

- (Corda) Desinstalar String

- (Corda) Código de Upgrade

- (UInt32) VersãoMajor

- (UInt32) Versão Menor



## <a name="irq-table"></a>Tabela IRQ

Espaço de nome: raiz\cimv2

Win32_IRQResource de classe


- (UInt32) Número IRQ

- (UInt16) Disponibilidade

- (Corda) Legenda

- (Corda) Descrição

- (Boolean) Hardware

- (Data) Data de Instalação

- (Corda) Nome

- (Boolean) Partilhável

- (Corda) Estado

- (UInt16) TriggerLevel

- (UInt16) TriggerType

- (UInt32) Vetor



## <a name="keyboard"></a>Teclado

Espaço de nome: raiz\cimv2

Win32_Keyboard de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (Boolean) IsLocked

- (UInt32) Código de Erro

- (Corda) Layout

- (Corda) Nome

- (UInt16) NumberOfFunctionKeys

- (UInt16) Senha

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema



## <a name="load-order-group"></a>Grupo de encomenda de carga

Espaço de nome: raiz\cimv2

Win32_LoadOrderGroup de classe


- (Corda) Nome

- (Corda) Legenda

- (Corda) Descrição

- (Boolean) DriverEnabled

- (UInt32) Ordem de Grupo

- (Data) Data de Instalação

- (Corda) Estado



## <a name="logical-disk"></a>Disco Lógico

Espaço de nome: root\cimv2\sms

SMS_LogicalDisk de classe


- (Corda) DispositivoID

- (UInt16) Acesso

- (UInt16) Disponibilidade

- (UInt64) BlockSize

- (Corda) Legenda

- (Boolean) Comprimido

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt32) Tipo de condução

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (Corda) Sistema de Ficheiros

- (UInt64) FreeSpace

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (UInt32) Comprimento máximo de componente

- (UInt32) MediaType

- (Corda) Nome

- (UInt64) NumberOfBlocks

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Nome do provedor

- (Corda) Propósito

- (UInt64) Tamanho

- (Corda) Estado

- (UInt16) StatusInfo

- (Boolean) SuportesFileBasedCompression

- (Corda) Nome do sistema

- (Corda) Nome de volume

- (Corda) VolumeSerialNumber



## <a name="memory"></a>Memória

Espaço de nome: raiz\cimv2

CCM_LogicalMemoryConfiguration de classe


- (Corda) Nome

- (UInt64) Memória Virtual Disponível

- (UInt64) TotalPageFileSpace

- (UInt64) Memória Total Física

- (UInt64) Memória TotalVirtual



## <a name="device-bluetooth"></a>Dispositivo Bluetooth

Espaço de nome: Reservado

Device_Bluetooth de classe


- (Boolean) Habilitado



## <a name="device-camera"></a>Câmera de dispositivo

Espaço de nome: Reservado

Device_Camera de classe


- (Boolean) Habilitado



## <a name="device-certificates"></a>Certificados de Dispositivo

Espaço de nome: Reservado

Device_Certificates de classe


- (Corda) Impressão digital

- (Corda) Tipo

- (Corda) Emitido

- (Corda) Emitido

- (Data) Válido A partir de

- (Data) Válido



## <a name="device-client"></a>Cliente do dispositivo

Espaço de nome: Reservado

Device_Client de classe


- (Boolean) DownloadWhenRoaming

- (Boolean) SincronizaçãoRoaming



## <a name="device-client-agent-version"></a>Versão do Agente cliente do dispositivo

Espaço de nome: Reservado

Device_ClientAgentVersion de classe


- (Corda) Versão



## <a name="device-computer-system"></a>Sistema de computador de dispositivo

Espaço de nome: Reservado

Device_ComputerSystem de classe


- (Corda) Tecnologia Celular

- (Corda) DispositivoClientID

- (Corda) Fabricante de Dispositivos

- (Corda) Modelo de Dispositivos

- (Corda) DMVersion

- (Corda) Versão firmware

- (Corda) HardwareVersion

- (Corda) IMEI

- (Corda) IMSI

- (UInt8) IsActivationLockEnabled

- (UInt8) Prisão quebrada

- (Corda) MEID

- (Corda) OEM

- (Corda) Número de telefone

- (Corda) PlataformaType

- (UInt32) Arquitetura de Processadores

- (UInt32) Nível de processador

- (UInt32) Revisão de processadores

- (Corda) Produto

- (Corda) Versão do Produto

- (Corda) Número de série

- (Corda) Versão de software

- (Corda) Rede De Porta-assinantes



## <a name="device-display"></a>Exibição do dispositivo

Espaço de nome: Reservado

Device_Display de classe


- (UInt32) Resolução Horizontal

- (UInt64) NumberOfColors

- (UInt32) Resolução Vertical



## <a name="device-email"></a>Email do dispositivo

Espaço de nome: Reservado

Device_Email de classe


- (Corda) Endereço de e-mail proprietário

- (Corda) SyncDomain

- (Corda) SyncServer

- (Corda) Sincronizador

- (Corda) Tipo



## <a name="device-encryption"></a>Encriptação do dispositivo

Espaço de nome: Reservado

Device_Encryption de classe


- (UInt32) Algoritmo de Encriptação de email

- (UInt32) Negociação de email

- (Boolean) EmailEncryptionRequired

- (Boolean) Algoritmo de e-mail signing

- (Boolean) Assinatura de e-mailNecessária

- (Boolean) EncriptaçãoCompliance

- (Boolean) Memória do TelefoneEncriptada

- (Boolean) StorageCardEncriptado



## <a name="device-exchange"></a>Troca de Dispositivos

Espaço de nome: Reservado

Device_Exchange de classe


- (Boolean) Resolução de Conflitos

- (SInt32) HTMLEmailTruncation

- (UInt32) Formato de Correio

- (UInt32) MaxCalendarage

- (UInt32) MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- (UInt32) OffPeakSyncFrequency

- (UInt32) Dias de Pico

- (Corda) Pico EndTime

- (Corda) Pico StartTime

- (UInt32) PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- (Boolean) Enviar EmailImediatamente

- (Boolean) Calendário de Sincronização

- (Boolean) SyncContacts

- (Boolean) SyncEmail

- (Boolean) Tarefas sincronizadas

- (Boolean) SincronizaçãoRoaming



## <a name="device-installed-applications"></a>Aplicações instaladas no dispositivo

Espaço de nome: Reservado

Device_InstalledApplications de classe


- (Corda) Nome

- (Corda) Versão



## <a name="device-irda"></a>Dispositivo IrDA

Espaço de nome: Reservado

Device_IrDA de classe


- (Boolean) Habilitado



## <a name="mobile-device-location"></a>Localização do dispositivo móvel

Espaço de nome: Reservado

MDM_RemoteFind de classe


- (Real32) Latitude

- (Real32) Longitude



## <a name="device-memory"></a>Memória do dispositivo

Espaço de nome: Reservado

Device_Memory de classe


- (UInt64) ProgramaGratuito

- (UInt64) ProgramaTotal

- (UInt64) Depósito Sem Remo

- (UInt64) Armazenamento RemovívelTotal

- (UInt64) Armazenamento Gratuito

- (UInt64) ArmazenamentoTotal



## <a name="device-os-information"></a>Informações sobre o Sistema operativo

Espaço de nome: Reservado

Device_OSInformation de classe


- (Corda) Língua

- (Corda) Plataforma

- (Corda) Versão



## <a name="device-password"></a>Palavra-passe do dispositivo

Espaço de nome: Reservado

Device_Password de classe


- (Boolean) Permitir RecoveryPassword

- (UInt32) AutolockTimeout

- (Boolean) Habilitado

- (UInt32) Expiração

- (UInt32) História

- (UInt32) MaxAttemptsBeforeWipe

- (UInt32) MinComplexChars

- (UInt32) MinLength

- (UInt8) Qualidade das palavras-passe

- (UInt32) Tipo



## <a name="device-policy"></a>Política do Dispositivo

Espaço de nome: Reservado

Device_Policy de classe


- (Corda) Nome

- (Boolean) Forçado



## <a name="device-power"></a>Potência do dispositivo

Espaço de nome: Reservado

Device_Power de classe


- (UInt32) BacklightACTimeout

- (UInt32) BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) Pilhapor



## <a name="mobile-device-security-status"></a>Estado de segurança do dispositivo móvel

Espaço de nome: Reservado

MDM_SecurityStatus de classe


- (UInt32) HardwareEncryptionCaps

- (UInt8) PasscodeCompliant

- (UInt8) PasscodeCompliantWithProfiles

- (UInt8) Código de acessoPresente

- (UInt8) Exigir Encriptação



## <a name="device-windows-security-policy"></a>Política de segurança do Windows do dispositivo

Espaço de nome: Reservado

Device_WindowsSecurityPolicy de classe


- (UInt32) ID

- (Corda) Nome

- (UInt32) Valor



## <a name="device-wlan"></a>Dispositivo WLAN

Espaço de nome: Reservado

Device_WLAN de classe


- (Boolean) Habilitado

- (Corda) EthernetMAC

- (Corda) WiFiMAC



## <a name="modem"></a>Modem

Espaço de nome: raiz\cimv2

Win32_POTSModem de classe


- (Corda) DispositivoID

- (UInt16) Modo de Resposta

- (Corda) Anexado

- (UInt16) Disponibilidade

- (Corda) Blindoff

- (Corda) Blindon

- (Corda) Legenda

- (Corda) CompatibilidadeBandeiras

- (UInt16) CompressãoInfo

- (Corda) CompressãoOff

- (Corda) CompressãoOn

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) ConfiguraçãoDiálogo

- (Corda) Países Apoiados[]

- (Corda) País Selecionado

- (Corda) Palavras-passe atuais[]

- (Corda) DCB

- (Corda) Padrão

- (Corda) Descrição

- (Corda) Carregador de Dispositivos

- (Corda) Tipo de dispositivo

- (UInt16) Tipo de marcação

- (Data) Data do Condutor

- (Boolean) Erro Ilibado

- (Corda) Controlo de errosForçado

- (UInt16) ErrorControlInfo

- (Corda) ErrorControlOff

- (Corda) Controlo de erros

- (Corda) Descrição de erros

- (Corda) FlowControlHard

- (Corda) FlowControlOff

- (Corda) FlowControlSoft

- (Corda) Escala de Inatividade

- (UInt32) InatividadeTimeout

- (UInt32) Índice

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (UInt32) MaxBaudRateToPhone

- (UInt32) MaxBaudRateToSerialPort

- (UInt16) MaxNumberOfPasswords

- (Corda) Modelo

- (Corda) ModemInfPath

- (Corda) Secção ModemInf

- (Corda) ModulaçãoBell

- (Corda) ModulaçãoCCITT

- (UInt16) Esquema de Modulação

- (Corda) Nome

- (Corda) PNPDeviceID

- (Corda) PortSubClass

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Prefixo

- (Corda) Propriedades

- (Corda) Nome do provedor

- (Corda) Pulso

- (Corda) Reset

- (Corda) RespostasNome chave

- (UInt8) Anéis Antes da Resposta

- (Corda) SpeakerModeDial

- (Corda) SpeakerModeOff

- (Corda) Speakermodeon

- (Corda) SpeakerModeSetup

- (Corda) AltifalanteVolumeHigh

- (UInt16) SpeakerVolumeInfo

- (Corda) SpeakerVolumeLow

- (Corda) AltifalanteVolumeMed

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Formato string

- (Boolean) SuportesCallback

- (Boolean) SuportesSynchronousConnect

- (Corda) Nome do sistema

- (Corda) Exterminador

- (Data) TimeOfLastReset

- (Corda) Tom

- (Corda) Recurso voiceSwitch



## <a name="motherboard"></a>Motherboard

Espaço de nome: raiz\cimv2

Win32_MotherboardDevice de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) PrimaryBusType

- (Corda) Número de Revisão

- (Corda) SecondaryBusType

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema


## <a name="nap-client"></a>Cliente NAP

Espaço de nome: raiz\Nap

NAP_Client de classe


- Nome (Corda)

- Descrição (Corda)

- (String) fixupURL

- (Boolean) napEnabled

- (Cadeia) napProtocolVersion

- (Corda) estágioTempo

- (UInt32) sistema IsolationState



## <a name="nap-system-health-agent"></a>Agente de Saúde do Sistema PAN

Espaço de nome: raiz\Nap

NAP_SystemHealthAgent de classe


- (UInt32) ID

- Descrição (Corda)

- (UInt32) fixupState

- (String) amigávelName

- Informação Clisid

- (Boolean) isBound

- (UInt8) percentagem

- Inscrição (String)Data

- (String) nome do fornecedor

- Versão (String)



## <a name="network-adapter"></a>Adaptador de rede

Espaço de nome: raiz\cimv2

Win32_NetworkAdapter de classe


- (Corda) DispositivoID

- (Corda) AdaptadorType

- (Boolean) AutoSense

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt32) Índice

- (Data) Data de Instalação

- (Boolean) Instalado

- (UInt32) Código de Erro

- (Corda) MACAddress

- (Corda) Fabricante

- (UInt32) Número máximo Controlado

- (UInt64) MaxSpeed

- (Corda) Nome

- (Corda) Endereços de rede[]

- (Corda) Endereço Permanente

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Nome do produto

- (Corda) Nome de serviço

- (UInt64) Velocidade

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="network-adapter-configuration"></a>Configuração do adaptador de rede

Espaço de nome: raiz\cimv2

Win32_NetworkAdapterConfiguration de classe


- (UInt32) Índice

- (Boolean) ArpAlwaysSourceRoute

- (Boolean) ArpUseEtherSNAP

- (Corda) Legenda

- (Corda) Caminho de Base de Dados

- (Boolean) DeadGWDetectEnabled

- (Corda) DefaultIPGateway[]

- (UInt8) Incumprimento

- (UInt8) DefaultTTL

- (Corda) Descrição

- (Boolean) DHCPEnabled

- (Data) DHCPLeaseExpires

- (Data) DHCPLeaseObtido

- (Corda) DHCPServer

- (Corda) Domínio DNS

- (Corda) DNSDomainSuffixSearchOrder[]

- (Boolean) Resolução DNSEnabledForWINS

- (Corda) Nome de anfitrião DNS

- (Corda) DNSServerSearchOrder[]

- (Boolean) Registo de DomínioDNS

- (UInt32) Memória do Tampão Forward

- (Boolean) FullDNSRegistrationEnabled

- (UInt16) GatewayCostMetric[]

- (UInt8) IGMPLevel

- (Corda) Endereço IP[]

- (UInt32) IPConnectionMetric

- (Boolean) IPEnabled

- (Boolean) IPFilterSecurityEnabled

- (Boolean) IPPortSecurityEnabled

- (Corda) IPSecPermitIPProtocolos[]

- (Corda) IPSecPermitTCPPorts[]

- (Corda) IPSecPermitUDPPorts[]

- (Corda) IPSubnet[]

- (Boolean) Transmissão IPUseZero

- (Corda) Endereço IPX

- (Boolean) IPXEnabled

- (Corda) IPXFrameType

- (UInt32) IPXMediaType

- (Corda) NÚMERO IPXNetwork[]

- (Corda) Número IPXVirtualNet

- (UInt32) KeepAliveInterval

- (UInt32) KeepAliveTime

- (Corda) MACAddress

- (UInt32) MTU

- (UInt32) NumForwardPackets

- (Boolean) PMTUBHDetectEnabled

- (Boolean) PMTUDiscoveryEnabled

- (Corda) Nome de serviço

- (Corda) SettingID

- (UInt32) Opções de TcpipNetbios

- (UInt32) Transmissões TcpMaxConnectRes

- (UInt32) Transmissões TcpMaxDataRes

- (UInt32) TcpNumConnections

- (Boolean) TcpUseRFC1122UrgentePointer

- (UInt16) TcpWindowSize

- (Boolean) WINSEnableLMHostsLookup

- (Corda) WINSHostLookupFile

- (Corda) WINSPrimaryServer

- (Corda) WINSScopeID

- (Corda) WINSSecondaryServer



## <a name="network-client"></a>Cliente de Rede

Espaço de nome: raiz\cimv2

Win32_NetworkClient de classe


- (Corda) Nome

- (Corda) Legenda

- (Corda) Descrição

- (Data) Data de Instalação

- (Corda) Fabricante

- (Corda) Estado



## <a name="network-login-profile"></a>Perfil de login de rede

Espaço de nome: raiz\cimv2

Win32_NetworkLoginProfile de classe


- (Corda) Nome

- (Data) Contas Expirações

- (UInt32) Bandeiras de Autorização

- (UInt32) MauPasswordCount

- (Corda) Legenda

- (UInt32) Página de Código

- (Corda) Comentário

- (UInt32) CountryCode

- (Corda) Descrição

- (UInt32) Bandeiras

- (Corda) Nome completo

- (Corda) HomeDirectory

- (Corda) HomeDirectoryDrive

- (Data) LastLogoff

- (Data) LastLogon

- (Corda) Horas de Logon

- (Corda) LogonServer

- (UInt64) Armazenamento Máximo

- (UInt32) NumberOfLogons

- (Corda) Parâmetros

- (Data) PasswordAge

- (Data) PasswordExpires

- (UInt32) PrimaryGroupId

- (UInt32) Privilégios

- (Corda) Perfil

- (Corda) Roteiro

- (Corda) SettingID

- (UInt32) Semana das Unidades

- (Corda) Comentário do utilizador

- (UInt32) Userid

- (Corda) Tipo de utilizador

- (Corda) Estações de trabalho



## <a name="nt-eventlog-file"></a>Arquivo NT Eventlog

Espaço de nome: raiz\cimv2

Win32_NTEventlogFile de classe


- (Corda) Nome

- (UInt32) AccessMask

- (Boolean) Arquivo

- (Corda) Legenda

- (Boolean) Comprimido

- (Corda) Método de Compressão

- (Data) Data da Criação

- (Corda) Descrição

- (Corda) Conduzir

- (Corda) EightDotThreeFileName

- (Boolean) Encriptado

- (Corda) Método de encriptação

- (Corda) Extensão

- (Corda) Nome de ficheiro

- (UInt64) Tamanho de ficheiro

- (Corda) Tipo de ficheiro

- (Corda) FSName

- (Boolean) Escondido

- (Data) Data de Instalação

- (UInt64) Contagem inutiling

- (Data) ÚltimaAAda

- (Data) Última Modificada

- (Corda) Nome de ficheiro de registo

- (Corda) Fabricante

- (UInt32) MaxFileSize

- (UInt32) NumberOfRecords

- (UInt32) OverwriteOutDated

- (Corda) Política de Sobreescrita

- (Corda) Caminho

- (Boolean) Legível

- (Corda) Fontes[]

- (Corda) Estado

- (Boolean) Sistema

- (Corda) Versão

- (Boolean) Repreensível



## <a name="office365proplusconfigurations"></a>Configurações Office365ProPlus

Espaço de nome: raiz\cimv2

classe Office365ProPlusConfigurações


- (Corda) Nome-chave

- (Corda) AutoUpgrade

- (Corda) CCMManaged

- (Corda) CDNBaseUrl

- (String) cfgUpdateChannel

- (Corda) Cultura do Cliente

- (Corda) Pasta do Cliente

- (Corda) GPOChannel

- (Corda) GPOOfficeMgmtCOM

- (Corda) Caminho de Instalação

- (Corda) Última Cenário

- (Corda) Resultado do Cenário Final

- (Corda) OfficeMgmtCOM

- (Corda) Plataforma

- (Corda) CompartilhadoComputerLicensing

- (Corda) UpdateChannel

- (Corda) UpdatePath

- (Corda) AtualizaçõesEnabled

- (Corda) UpdateUrl

- (Corda) VersãoToReport



## <a name="office-addin"></a>Addin de escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeAddin de classe


- (Corda) Arquitetura

- (Corda) ID

- (Corda) OfficeApp

- (Corda) Tipo

- (UInt32) AverageLoadTimeInMillisegundos

- (Corda) CLSID

- (Corda) Nome da empresa

- (UInt32) CrashCount

- (Corda) Descrição

- (UInt32) ErrorCount

- (Corda) Nome de ficheiro

- (UInt64) Tamanho de ficheiro

- (UInt32) FileTimestamp

- (Corda) Versão de Ficheiros

- (Corda) Nome amigável

- (Corda) FriendlyNameHash

- (Corda) IdHash

- (UInt32) LoadBehavior

- (UInt32) Contagem de cargas

- (UInt32) Contagem de falhas de carga

- (Corda) Nome do produto

- (Corda) Versão do Produto



## <a name="office-client-metric"></a>Métrica do Cliente do Escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeClientMetric de classe


- (Corda) OfficeApp

- (UInt32) CompatibilidadeErrorCount

- (UInt32) CrashedSessionCount

- (UInt32) Contagem de Erros macrocompile

- (UInt32) MacroRuntimeErrorCount

- (UInt32) SessõesContagem



## <a name="office-device-summary"></a>Resumo do dispositivo de escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeDeviceSummary de classe


- (Boolean) IsProPlusInstalado

- (Boolean) IsTelemettryEnabled



## <a name="office-document-metric"></a>Métrica do documento do escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeDocumentMetric de classe


- (Corda) OfficeApp

- (UInt32) TotalCloudDocs

- (UInt32) TotalLegacyDocs

- (UInt32) TotalLocalDocs

- (UInt32) TotalMacroDocs

- (UInt32) TotalNonMacroDocs

- (UInt32) TotalUncDocs



## <a name="office-document-solution"></a>Solução de Documento de Escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeDocumentSolution de classe


- (Corda) Documentsolutionid

- (Corda) OfficeApp

- (UInt32) CompatibilidadeErrorCount

- (UInt32) CrashCount

- (Corda) Nome de arquivo de exemplo

- (UInt32) Contagem de cargas

- (UInt32) Contagem de falhas de carga

- (UInt32) Contagem de Erros macrocompile

- (UInt32) MacroRuntimeErrorCount

- (Corda) Tipo



## <a name="office-macro-error"></a>Erro macro do escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeMacroError de classe


- (Corda) Documentsolutionid

- (UInt32) Código de Erro

- (UInt32) Contagem

- (UInt64) Última Ocorrência

- (Corda) Tipo



## <a name="office-product-info"></a>Informações sobre produtos de escritório

Espaço de nome: root\ccm\InvAgt

CCM_OfficeProductInfo de classe


- (Corda) Nome do produto

- (Corda) Versão do Produto

- (Corda) Arquitetura

- (Corda) Canal

- (UInt32) IsProPlusInstalado

- (Corda) Língua

- (Corda) Estado de Licença



## <a name="office-vba-rule-violation"></a>Violação da regra do escritório Vba

Espaço de nome: root\ccm\InvAgt

CCM_OfficeVbaRuleViolation de classe


- (UInt32) Governo

- (UInt32) Contagem de Ficheiros

- (Corda) OfficeApp



## <a name="office-vbasummary"></a>Escritório VbaSummary

Espaço de nome: root\ccm\InvAgt

CCM_OfficeVbaScanResultsSummary de classe


- (UInt32) Design

- (UInt32) Design64

- (UInt32) DuplicateVba

- (Boolean) Resultados De HasResults

- (UInt32) Estação HasVba

- (UInt32) Inacessível

- (UInt32) Questões

- (UInt32) Questões64

- (UInt32) ProblemasNone

- (UInt32) ProblemasNone64

- (UInt32) Bloqueado

- (UInt32) Rio NoVba

- (UInt32) Protegido

- (UInt32) RemLimited

- (UInt32) RemLimited64

- (UInt32) RemSignificant

- (UInt32) RemSignificant64

- (UInt32) Pontuação

- (UInt32) Pontuação64

- (UInt32) Total

- (UInt32) Validação

- (UInt32) Validação64



## <a name="operating-system"></a>Sistema Operativo

Espaço de nome: raiz\cimv2

Win32_OperatingSystem de classe


- (Corda) Nome

- (Corda) Dispositivo de arranque

- (Corda) Número de construção

- (Corda) BuildType

- (Corda) Legenda

- (Corda) Conjunto de Códigos

- (Corda) CountryCode

- (Corda) CSDVersão

- (SInt16) AtualTimeZone

- (Boolean) Depuração

- (Corda) Descrição

- (Boolean) Distribuído

- (UInt8) ForegroundApplicationBoost

- (UInt64) Memória Física Livre

- (UInt64) Ficheiros FreeSpaceInPagingFiles

- (UInt64) Memória Virtual Gratuita

- (Data) Data de Instalação

- (Data) LastBootUpTime

- (Data) Hora do Local

- (Corda) Localidade

- (Corda) Fabricante

- (UInt32) MaxNumberOfProcesses

- (UInt64) MaxProcessMemorySize

- (Corda) MUILanguages[]

- (UInt32) NumberOfLicensedUsers

- (UInt32) NumberOfProcesses

- (UInt32) NumberOfUsers

- (UInt32) Sistemas OperativosKU

- (Corda) Organização

- (Corda) ARQUITETURA OS

- (UInt32) Linguagem OS

- (UInt32) OSProductSuite

- (UInt16) OSTipo

- (Corda) Descrição do outro tipo

- (Corda) PlusProductID

- (Corda) Número de versão plus

- (Boolean) Primária

- (UInt32) Tipo de Produto

- (Corda) RegistradoUser

- (Corda) Número de série

- (UInt16) ServicePackMajorVersion

- (UInt16) ServicePackMinorVersion

- (UInt64) SizeStoredInPagingFiles

- (Corda) Estado

- (Corda) Dispositivo de sistema

- (Corda) Diretório de Sistema

- (UInt64) TotalswapSpaceSize

- (UInt64) TotalVirtualMemorySize

- (UInt64) TotalVisibleMemorySize

- (Corda) Versão

- (Corda) WindowsDirectory



## <a name="operating-system-ex"></a>Sistema Operativo Ex

Espaço de nome: raiz\cimv2

CCM_OperatingSystemExtended de classe


- (Corda) Nome

- (UInt32) SKU



## <a name="operating-system-recovery-configuration"></a>Configuração de recuperação do sistema operativo

Espaço de nome: raiz\cimv2

Win32_OSRecoveryConfiguration de classe


- (Corda) Nome

- (Boolean) AutoReboot

- (Corda) Legenda

- (Corda) DebugFilePathPath

- (Corda) Descrição

- (Boolean) KernelDumpOnly

- (Boolean) SobreescritaExistingDebugFile

- (Boolean) EnviarAdminAlert

- (Corda) SettingID

- (Boolean) WriteDebugInfo

- (Boolean) WriteToSystemLog



## <a name="optional-feature"></a>Recurso Opcional

Espaço de nome: raiz\cimv2

Win32_OptionalFeature de classe


- (Corda) Nome

- (Corda) Legenda

- (Corda) Descrição

- (Data) Data de Instalação

- (UInt32) Instalação Do Estado

- (Corda) Estado



## <a name="page-file-setting"></a>Definição de ficheiro de página

Espaço de nome: raiz\cimv2

Win32_PageFileSetting de classe


- (Corda) Nome

- (Corda) Legenda

- (Corda) Descrição

- (UInt32) Tamanho inicial

- (UInt32) Tamanho máximo

- (Corda) SettingID



## <a name="parallel-port"></a>Porto Paralelo

Espaço de nome: raiz\cimv2

Win32_ParallelPort de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) DMASupport

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Boolean) OSAutoDescoberto

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="bios"></a>BIOS

Espaço de nome: raiz\cimv2

Win32_BIOS de classe


- (Corda) Nome

- (Corda) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) Sistema de Operações de Alvo

- (Corda) Versão

- (UInt16) BiosCharacteristics[]

- (Corda) BIOSVersão[]

- (Corda) Número de construção

- (Corda) Legenda

- (Corda) Conjunto de Códigos

- (Corda) AtualLanguage

- (Corda) Descrição

- (Corda) Código de Identificação

- (UInt16) Idiomas Instaladores

- (Data) Data de Instalação

- (Corda) Edição linguística

- (Corda) ListOfLanguages[]

- (Corda) Fabricante

- (Corda) Outros TargetOS

- (Boolean) PrimaryBIOS

- (Data) Data de Lançamento

- (Corda) Número de série

- (Corda) SMBIOSBIOSVERSION

- (UInt16) SMBIOSMajorversion

- (UInt16) SMBIOSMinorVersion

- (Boolean) SMBIOSPresent

- (Corda) Estado



## <a name="pcmcia-controller"></a>Controlador PCMCIA

Espaço de nome: raiz\cimv2

Win32_PCMCIAController de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="physical-memory"></a>Memória Física

Espaço de nome: raiz\cimv2

Win32_PhysicalMemory de classe


- (Corda) Nome de Classe Criação

- (Corda) Etiqueta

- (Corda) Rótulo Bancário

- (UInt64) Capacidade

- (Corda) Legenda

- (UInt16) Largura de Dados

- (Corda) Descrição

- (Corda) Localizador de dispositivos

- (UInt16) FormFactor

- (Boolean) HotSwappable

- (Data) Data de Instalação

- (UInt16) InterleaveDataDepth

- (UInt32) Posição interleave

- (Corda) Fabricante

- (UInt16) Tipo de memória

- (Corda) Modelo

- (Corda) Nome

- (Corda) OutraS Informações Identificantes

- (Corda) PartNumber

- (UInt32) Posicioninrow

- (Boolean) PoweredOn

- (Boolean) Removível

- (Boolean) Substituível

- (Corda) Número de série

- (Corda) SKU

- (UInt32) Velocidade

- (Corda) Estado

- (UInt16) Largura Total

- (UInt16) TipoDetalhe

- (Corda) Versão



## <a name="physicaldisk"></a>Disco Físico

Espaço de nome: root\microsoft\windows\storage

MSFT_PhysicalDisk de classe


- (Corda) Objectide

- (UInt64) Tamanho atribuído

- (UInt16) BusType

- (UInt16) Não pode não poolreason[]

- (Boolean) CanPool

- (Corda) Descrição

- (Corda) Dispositivoid

- (UInt16) Número de recinto

- (Corda) Versão firmware

- (Corda) Nome amigável

- (UInt16) Estado de Saúde

- (Boolean) IsIndicationEnabled

- (Boolean) É Parcial

- (UInt64) Dimensão lógica sectorial

- (Corda) Fabricante

- (UInt16) MediaType

- (Corda) Modelo

- (UInt16) Estatuto operacional[]

- (Corda) OutraDescrição de Razão de Não Podepiscina

- (Corda) PartNumber

- (Corda) Localização Física

- (UInt64) Tamanho físico

- (Corda) Número de série

- (UInt64) Tamanho

- (UInt16) SlotNumber

- (Corda) Versão de software

- (UInt32) Velocidade do fuso

- (UInt16) Utilizações Suportadas[]

- (Corda) Único

- (UInt16) Utilização



## <a name="pnp-device-driver"></a>Condutor de dispositivo pnp

Espaço de nome: raiz\cimv2

Win32_PnpEntity de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (Corda) Classguid

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Nome de Classe Criação

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Serviço

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) SystemCreationClassName

- (Corda) Nome do sistema



## <a name="pointing-device"></a>Dispositivo de ponta

Espaço de nome: raiz\cimv2

Win32_PointingDevice de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt16) Interface de Dispositivos

- (UInt32) Limiar de velocidade dupla

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt16) Destreza

- (Corda) HardwareType

- (Corda) Nome infFile

- (Corda) InfSection

- (Data) Data de Instalação

- (Boolean) IsLocked

- (UInt32) Código de Erro

- (Corda) Fabricante

- (Corda) Nome

- (UInt8) NumberOfButtons

- (Corda) PNPDeviceID

- (UInt16) Tipo de ponta

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt32) QuadSpeedThreshold

- (UInt32) Resolução

- (UInt32) Amostragem

- (Corda) Estado

- (UInt16) StatusInfo

- (UInt32) Sincronia

- (Corda) Nome do sistema



## <a name="portable-battery"></a>Bateria portátil

Espaço de nome: raiz\cimv2

Win32_PortableBattery de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt16) Situação de Bateria

- (UInt16) CapacidadeMultiplier

- (Corda) Legenda

- (UInt16) Química

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt32) Capacidade de Design

- (UInt64) DesignVoltage

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt16) Custo estimadoRemaining

- (UInt32) Tempo estimado

- (UInt32) Vida esperada

- (UInt32) FullChargeCapacity

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Localização

- (Corda) Data de Fabrico

- (Corda) Fabricante

- (UInt16) Erro maxBattery

- (UInt32) Hora máxima

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Versão SmartBattery

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (UInt32) TimeOnBattery

- (UInt32) TimetoFullCharge



## <a name="ports"></a>Portas

Espaço de nome: raiz\cimv2

Win32_PortResource de classe

- (UInt64) Endereço inicial

- (Boolean) Pseudónimo

- (Corda) Legenda

- (Corda) Descrição

- (UInt64) Endereço final

- (Data) Data de Instalação

- (Corda) Nome

- (Corda) Estado



## <a name="power-capabilities"></a>Capacidades de Energia

Espaço de nome: root\CCM\powermanagementagent

CCM_PwrMgmtSystemPowerCapabilities de classe


- (UInt32) Perfil de PMPM preferido

- (Boolean) ApmPresent

- (Boolean) Baterias A Curto Prazo

- (Boolean) FullWake

- (Boolean) LidPresent

- (Corda) MinDeviceWakeState

- (Boolean) ProcessadorThrottle

- (Corda) RtcWake

- (Boolean) Baterias do SistemaPresente

- (Boolean) Sistemas1

- (Boolean) Sistemas2

- (Boolean) Sistemas3

- (Boolean) Sistemas4

- (Boolean) Sistemas5

- (Boolean) UpsPresent

- (Boolean) VídeoDimPresent



## <a name="power-configurations"></a>Configurações de potência

Espaço de nome: root\CCM\policy\realconfig

CCM_PowerConfig de classe


- (Corda) PowerConfigID

- (UInt32) DuraçãoInSec

- (Corda) Plano Não PeakPower

- (Corda) Nome não-peakpowerplan

- (Corda) PicoPowerPlan

- (Corda) Nome PeakPowerPlan

- (Corda) PeakStartTimeHoursMin

- (Corda) WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>Razões de insónia de gestão de energia

Espaço de nome: root\CCM\powermanagementagent

CCM_PwrMgmtLastSuspendError de classe


- (Corda) Requester

- (Corda) RequesterType

- (Corda) Tipo de Pedido

- (Data) Tempo

- (UInt32) Código Adicional

- (Corda) AdicionalInfo

- (Corda) RequesterInfo

- (Boolean) Desconhecido



## <a name="power-management-daily"></a>Gestão de Energia Diariamente

Espaço de nome: root\CCM\powermanagementagent

CCM_PwrMgmtActualDay de classe


- (Data) Data

- (Corda) TipoofEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutosTotal



## <a name="power-client-opt-out-settings"></a>Power Client Opt out Settings

Espaço de nome: root\ccm\ClientSDK

CCM_PowerManagementClientOptoutSetting de classe


- (Boolean) AdministradorOptOptout

- (Boolean) EfetivamenteClientOptOut

- (Boolean) IsClientOptOut



## <a name="power-management-monthly"></a>Gestão de Energia Mensalmente

Espaço de nome: root\CCM\powermanagementagent

CCM_PwrMgmtMonth de classe


- (Data) Início do Mês

- (UInt32) minutosComputerActive

- (UInt32) minutosComputerOn

- (UInt32) minutosComputerShutdown

- (UInt32) minutosComputerSleep

- (UInt32) minutosMonitorOn

- (UInt32) minutosTotal

- (Corda) TipoofEvent



## <a name="power-settings"></a>Definições de potência

Espaço de nome: root\cimv2\sms

SMS_PowerSettings de classe


- (Corda) GUIA

- (Corda) ACSettingIndex

- (Corda) ACValue

- (Corda) DCSettingIndex

- (Corda) DCValue

- (Corda) Nome

- (Corda) UnitEspecificador



## <a name="print-jobs"></a>Imprimir Empregos

Espaço de nome: raiz\cimv2

Win32_PrintJob de classe


- (Corda) Nome

- (Corda) Legenda

- (Corda) DataType

- (Corda) Descrição

- (Corda) Documento

- (Corda) Nome do condutor

- (Data) Tempo decorrido

- (Corda) Fila de Impressão Anfitriã

- (Data) Data de Instalação

- (UInt32) Jobid

- (Corda) Estatuto de Emprego

- (Corda) Notificar

- (Corda) Proprietário

- (UInt32) Páginas Impressas

- (Corda) Parâmetros

- (Corda) Processador de Impressão

- (UInt32) Prioridade

- (UInt32) Tamanho

- (Data) Hora de Início

- (Corda) Estado

- (UInt32) StatusMask

- (Data) Prazo Submetido

- (UInt32) Páginas Totais

- (Data) Até o momento



## <a name="printer-configuration"></a>Configuração da impressora

Espaço de nome: raiz\cimv2

Win32_PrinterConfiguration de classe


- (Corda) Nome

- (UInt32) BitsPerPel

- (Corda) Legenda

- (Boolean) Collate

- (UInt32) Cor

- (UInt32) Cópias

- (Corda) Descrição

- (Corda) Nome do dispositivo

- (UInt32) Bandeiras de exibição

- (UInt32) DisplayFrequency

- (UInt32) DitherType

- (UInt32) Versão do condutor

- (Boolean) Duplex

- (Corda) Nome de formulário

- (UInt32) Resolução Horizontal

- (UInt32) ICMIntent

- (UInt32) IcMMethod

- (UInt32) Pixels

- (UInt32) MediaType

- (UInt32) Orientação

- (UInt32) Comprimento de papel

- (Corda) Tamanho de papel

- (UInt32) Largura de Papel

- (UInt32) PelsHeight

- (UInt32) PelsWidth

- (UInt32) Impressão Qualidade

- (UInt32) Escala

- (Corda) SettingID

- (UInt32) EspecificaçãoVersão

- (UInt32) TTOption

- (UInt32) Resolução Vertical

- (UInt32) Resolução X

- (UInt32) Resolução



## <a name="printer-device"></a>Dispositivo de impressora

Espaço de nome: raiz\cimv2

Win32_Printer de classe


- (Corda) DispositivoID

- (UInt32) Atributos

- (UInt16) Disponibilidade

- (UInt32) AveragePagesPerMinute

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt32) Prioridade por defeito

- (Corda) Descrição

- (UInt16) Detetou ErrorState

- (Corda) Nome do condutor

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt32) Resolução Horizontal

- (Data) Data de Instalação

- (UInt32) JobCountSinceLastReset

- (UInt16) Línguas Suportadas[]

- (UInt32) Código de Erro

- (Corda) Localização

- (Corda) Nome

- (UInt16) PaperSizesSupported[]

- (Corda) PNPDeviceID

- (Corda) Nome de porta

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Nomes de papel de impressora[]

- (UInt32) Estado da Impressora

- (UInt16) Estatuto da impressora

- (Corda) Tipo de dados de trabalho de impressão

- (Corda) Processador de Impressão

- (Corda) SeparadorFile

- (Corda) Nome do servidor

- (Corda) Nome de partilha

- (Boolean) SpoolEnabled

- (Data) Hora de Início

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset

- (Data) Até o momento

- (UInt32) Resolução Vertical



## <a name="process"></a>Processo

Espaço de nome: raiz\cimv2

Win32_Process de classe


- (Corda) Pega

- (Corda) Legenda

- (Data) Data da Criação

- (Corda) Descrição

- (Corda) Caminho Executável

- (UInt16) Estado de Execução

- (UInt32) Conde

- (Data) Data de Instalação

- (UInt64) KernelModeTime

- (UInt32) Tamanho máximo de trabalho

- (UInt32) Tamanho mínimo de trabalho

- (Corda) Nome

- (Corda) NOME OS

- (UInt64) Contagem de Outras Operações

- (UInt64) Contagem de Outras Transferências

- (UInt32) Falhas de página

- (UInt32) Utilização de ficheiros de página

- (UInt32) Parentprocessid

- (UInt32) Uso de ficheiros peakpage

- (UInt64) Pico VirtualSize

- (UInt32) PicoWorkingSetsize

- (UInt32) Prioridade

- (UInt64) Contagem de páginas privadas

- (UInt32) Processo

- (UInt32) Uso de QuotaNonPagedPool

- (UInt32) Uso de QuotaPagedPool

- (UInt32) Uso de quotaPeakNonPagedPool

- (UInt32) Uso de Piscina saem quotaPeakPagedPool

- (UInt64) Contagem de Leitura

- (UInt64) Contagem de Leitura

- (UInt32) SessãoId

- (Corda) Estado

- (Data) Data de Rescisão

- (UInt32) Contagem de fios

- (UInt64) UserModeTime

- (UInt64) Tamanho Virtual

- (Corda) Versão do Windows

- (UInt64) WorkingSetSize

- (UInt64) WriteOperationCount

- (UInt64) WriteTransferCount



## <a name="processor"></a>Processador

Espaço de nome: root\cimv2\sms

SMS_Processor de classe


- (Corda) DispositivoID

- (UInt16) Largura de endereço

- (UInt16) Arquitetura

- (UInt16) Disponibilidade

- (UInt16) BrandID

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) CPUHash

- (Corda) CPUKey

- (UInt16) CpuStatus

- (UInt32) Velocidade atual do relógio

- (UInt16) Tensão atual

- (UInt16) Largura de Dados

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt32) ExtClock

- (UInt16) Família

- (Data) Data de Instalação

- (Boolean) Is64Bit

- (Boolean) É HiperthreadAble

- (Boolean) IsHyperthreadEnabled

- (Boolean) IsMobile

- (Boolean) Execução fidedigna é capaz

- (Boolean) IsVitualizationAble

- (UInt32) Tamanho L2Cache

- (UInt32) Velocidade L2Cache

- (UInt32) Tamanho L3cache

- (UInt32) Velocidade L3cache

- (UInt32) Código de Erro

- (UInt16) Nível

- (UInt16) LoadPercentage

- (Corda) Fabricante

- (UInt32) Velocidade máxima

- (Corda) Nome

- (UInt32) NormSpeed

- (UInt32) NumberOfCores

- (UInt32) NumberOfLogicalProcessors

- (Corda) Outra Descrição Familiar

- (Boolean) PartofDomain

- (UInt32) PCache

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Processadorid

- (UInt16) ProcessadorTipo

- (UInt16) Revisão

- (Corda) Papel

- (Corda) Designação de tomadas

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Passo

- (Corda) Nome do sistema

- (Corda) Único

- (UInt16) Método de Upgrade

- (Corda) Versão

- (UInt32) Tensões Caps

- (Corda) Grupo de trabalho



## <a name="protected-volume-information"></a>Informações de volume protegido

Espaço de nome: root\cimv2\sms

CCM_ProtectedVolumeInfo de classe


- (Corda) Nome

- (Corda) Carta de condução

- (UInt32) Tipo de Proteção



## <a name="protocol"></a>Protocolo

Espaço de nome: raiz\cimv2

Win32_NetworkProtocol de classe


- (Corda) Nome

- (Corda) Legenda

- (Boolean) Serviço Sem Conexão

- (Corda) Descrição

- (Boolean) GarantiasEntrega

- (Boolean) GarantiasSequenciação

- (Data) Data de Instalação

- (UInt32) Tamanho máximo

- (UInt32) Tamanho máximo de mensagem

- (Boolean) MensagemOrientada

- (UInt32) Tamanho mínimo

- (Boolean) PseudoStreamOriented

- (Corda) Estado

- (Boolean) SuportesBroadcasting

- (Boolean) SuportesConnectData

- (Boolean) SuportesDisconnectData

- (Boolean) SuportaEncriptação

- (Boolean) SuportesExpeditedData

- (Boolean) Suportes Fragmentação

- (Boolean) SuportaGracefulClosing

- (Boolean) SuportaGuaranteedBandwidth

- (Boolean) Suportes Multicasting

- (Boolean) SuportesQualityofService



## <a name="quick-fix-engineering"></a>Engenharia de Correção Rápida

Espaço de nome: raiz\cimv2

Win32_QuickFixEngineering de classe


- (Corda) HotFixID

- (Corda) ServicePackInEffect

- (Corda) Legenda

- (Corda) Descrição

- (Corda) Reparação Comentários

- (Data) Data de Instalação

- (Corda) InstaladoBy

- (Corda) InstaladoOn

- (Corda) Nome

- (Corda) Estado



## <a name="ccm-recently-used-applications"></a>CcM Aplicações recentemente utilizadas

Espaço de nome: root\cimv2\sms

CCM_RecentlyUsedApps de classe


- (Corda) Nome do Ficheiro explorer

- (Corda) Caminho das Pastas

- (Corda) Apelido username

- (Corda) Códigos adicionais de produtos

- (Corda) Nome da empresa

- (Corda) Descrição do ficheiro

- (Corda) FilePropertiesHash

- (UInt32) Tamanho de ficheiro

- (Corda) Versão de Ficheiros

- (Data) Tempo Usado Última

- (UInt32) Contagem de lançamentos

- (String) msiDisplayName

- (String) msiPublisher

- (String) msiVersion

- (Corda) Nome original do ficheiro

- (Corda) Código de Produto

- (UInt32) Linguagem do Produto

- (Corda) Nome do produto

- (Corda) Versão do Produto

- (Corda) SoftwarePropertiesHash



## <a name="registry"></a>Registo

Espaço de nome: raiz\cimv2

Win32_Registry de classe


- (Corda) Nome

- (Corda) Legenda

- (UInt32) Tamanho atual

- (Corda) Descrição

- (Data) Data de Instalação

- (UInt32) Tamanho máximo

- (UInt32) Tamanho proposto

- (Corda) Estado



## <a name="scsi-controller"></a>Controlador SCSI

Espaço de nome: raiz\cimv2

Win32_SCSIController de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt32) Tempos de controlo

- (Corda) Descrição

- (Corda) Mapa do Dispositivo

- (Corda) Nome do condutor

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) HardwareVersion

- (UInt32) Índice

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Largura de Dados MaxData

- (UInt32) Número máximo Controlado

- (UInt64) MaxTransferRate

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) Gestão de Proteção

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="serial-port-configuration"></a>Configuração da porta de série

Espaço de nome: raiz\cimv2

Win32_SerialPortConfiguration de classe


- (Corda) Nome

- (Boolean) AbortoReadWriteOnError

- (UInt32) BaudRate

- (Boolean) BinaryModeEnabled

- (UInt32) BitsPerByte

- (Corda) Legenda

- (Boolean) ContinueXMitOnXOff

- (Boolean) CTSOutflowControl

- (Corda) Descrição

- (Boolean) DevoluçõesNULLBytes

- (Boolean) DSROutflowControl

- (Boolean) DSRSensibilidade

- (Corda) Tipo de Controlo de Fluxos DTR

- (UInt32) EOFCharacter

- (UInt32) ErrorReplaceCharacter

- (Boolean) Substituição de erroEnabled

- (UInt32) EventCharacter

- (Boolean) IsBusy

- (Corda) Paridade

- (Boolean) ParidadeCheckEnabled

- (Corda) RTSFlowControlType

- (Corda) SettingID

- (Corda) StopBits

- (UInt32) XoffCharacter

- (UInt32) XOffXMitThreshold

- (UInt32) XOnCharacter

- (UInt32) XOnXMitThreshold

- (UInt32) XonxoffinFlowControl

- (UInt32) XonXOffOutFlowControl



## <a name="serial-ports"></a>Portas Em Série

Espaço de nome: raiz\cimv2

Win32_SerialPort de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Boolean) Binário

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (UInt32) MaxBaudRate

- (UInt32) MaximumInputBufferSize

- (UInt32) MaximumOutputBufferSize

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Boolean) OSAutoDescoberto

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) FornecedorType

- (Boolean) SettableBaudRate

- (Boolean) SettableDataBits

- (Boolean) SettableFlowControl

- (Boolean) SettableParidade

- (Boolean) SettableParityCheck

- (Boolean) SettableRLSD

- (Boolean) SettableStopBits

- (Corda) Estado

- (UInt16) StatusInfo

- (Boolean) Suportes16BitMode

- (Boolean) SuportesDTRDSR

- (Boolean) SupportsTimeouts

- (Boolean) SuportesIntTimeouts

- (Boolean) SuportesParityCheck

- (Boolean) SuportesRLSD

- (Boolean) SuportesRTSCTS

- (Boolean) SuportaSpecialCharacters

- (Boolean) SuportesXOnXOff

- (Boolean) SuportesXOnXOffSet

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="server-feature"></a>Funcionalidade de Servidor

Espaço de nome: raiz\cimv2

Win32_ServerFeature de classe


- (UInt32) ID

- (Corda) Nome

- (UInt32) Parentalid



## <a name="services"></a>Serviços

Espaço de nome: raiz\cimv2

Win32_Service de classe


- (Corda) Nome

- (Boolean) Aceitar Pausa

- (Boolean) AceitarParar

- (Corda) Legenda

- (UInt32) CheckPoint

- (Corda) Descrição

- (Boolean) DesktopInteract

- (Corda) Nome do ecrã

- (Corda) ErrorControl

- (UInt32) Código de Saída

- (Data) Data de Instalação

- (Corda) Nome do caminho

- (UInt32) Processo

- (UInt32) ServiceSpecificExitCode

- (Corda) Tipo de serviço

- (Boolean) Iniciado

- (Corda) Modo de Arranque

- (Corda) Nome de partida

- (Corda) Estado

- (Corda) Estado

- (Corda) Nome do sistema

- (UInt32) Tagid

- (UInt32) WaitHint



## <a name="shares"></a>Partilhas

Espaço de nome: raiz\cimv2

Win32_Share de classe


- (Corda) Nome

- (UInt32) AccessMask

- (Boolean) Permitir Máximo

- (Corda) Legenda

- (Corda) Descrição

- (Data) Data de Instalação

- (UInt32) Máximo Permitido

- (Corda) Caminho

- (Corda) Estado

- (UInt32) Tipo



## <a name="sw-licensing-product"></a>Produto de licenciamento SW

Espaço de nome: raiz\cimv2

classe SoftwareLicensingProduct


- (Corda) ID

- (Corda) ApplicationID

- (Corda) Descrição

- (Data) Data final de avaliação

- (UInt32) GracePeriodRemaining

- (UInt32) Estatuto de Licença

- (Corda) MáquinaURL

- (Corda) Nome

- (Corda) Instalação offline

- (Corda) Chave de Produto Parcial

- (Corda) ProcessadorURL

- (Corda) ProductKeyID

- (Corda) ProductKeyURL

- (Corda) UseLicenseURL



## <a name="sw-licensing-service"></a>Serviço de Licenciamento SW

Espaço de nome: raiz\cimv2

classe SoftwareLicensingService


- (Corda) Versão

- (Corda) ClientMachineID

- (UInt32) Máquina de serviço de gestão iskeymanagement

- (UInt32) KeyManagementServiceCurrentCount

- (Corda) Máquina de Serviço de Gestão de Chaves

- (Corda) KeyManagementServiceProductKeyID

- (UInt32) PolicyCacheRefreshRequired

- (UInt32) Contagem de Clientes Obrigatório

- (UInt32) Intervalo de VLActivation

- (UInt32) VLRenewalInterval



## <a name="software-shortcut"></a>Atalho de software

Espaço de nome: root\cimv2\sms

SMS_SoftwareShortcut de classe


- (Corda) Abreviatura

- (Corda) Versão binfile

- (Corda) Versão binproduct

- (Corda) Descrição

- (Corda) FilePropertiesHash

- (Corda) FilePropertiesHashEx

- (UInt32) Tamanho de ficheiro

- (Corda) Versão de Ficheiros

- (UInt32) Língua

- (Corda) Nome-mãe

- (Corda) Produto

- (Corda) Código de Produto

- (Corda) Versão do Produto

- (Corda) Editora

- (Corda) Nome de atalho

- (UInt32) Tipo de atalho

- (Corda) TargetExecutável



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

Espaço de nome: root\cimv2\sms

SMS_SoftwareTag de classe


- (Corda) TagCreatorRegid

- (Corda) Id ID Único

- (Corda) Versão do ecrã

- (Boolean) DireitoS Exigidos

- (Corda) Nome do produto

- (Corda) Criador de Software

- (Corda) SoftwareCreatorRegid

- (Corda) Licenciador de Software

- (Corda) SoftwareLicensorRegid

- (Corda) TagCreator

- (SInt32) VersãoMajor

- (SInt32) Versão Menor



## <a name="sound-devices"></a>Dispositivos de Som

Espaço de nome: raiz\cimv2

Win32_SoundDevice de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (UInt16) Dmabuffersize

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Endereço MPU401

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Nome do produto

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema



## <a name="system-account"></a>Conta do Sistema

Espaço de nome: raiz\cimv2

Win32_SystemAccount de classe


- (Corda) Domínio

- (Corda) Nome

- (Corda) Legenda

- (Corda) Descrição

- (Data) Data de Instalação

- (Corda) SID

- (UInt8) SIDType

- (Corda) Estado



## <a name="system-boot-data"></a>Dados do arranque do sistema

Espaço de nome: raiz\CCM

CCM_SystemBootData de classe


- (UInt64) Tempo de início do sistema

- (UInt32) BiosDura

- (UInt16) BootdiskMediaType

- (UInt32) Duração do arranque

- (UInt32) EventLogStart

- (UInt32) GPDuração

- (Corda) OSVersão

- (UInt32) AtualizaçãoDuração



## <a name="system-boot-summary"></a>Resumo da bota do sistema

Espaço de nome: raiz\CCM

CCM_SystemBootSummary de classe


- (UInt32) MédiaBootFrequency

- (UInt32) Últimas BiosDura

- (UInt32) ÚltimaDuração do Arranque

- (UInt32) Últimadura de Arranquecore

- (UInt32) ÚltimaS EventLogStart

- (UInt32) Última Sanção GP

- (UInt32) ÚltimaS Atualizações Duração

- (UInt32) Duração máxima

- (UInt32) Duração máxima

- (UInt32) Duração máxima

- (UInt32) MaxEventLogStart

- (UInt32) Duração máxima

- (UInt32) Duração máxima

- (UInt32) MediabiosDura

- (UInt32) Duração medianaboot

- (UInt32) Duração medianacoreboot

- (UInt32) MedianEventLogStart

- (UInt32) Duração medianaGP

- (UInt32) Duração mediana



## <a name="system-console-usage"></a>Utilização da consola do sistema

Espaço de nome: root\cimv2\sms

SMS_SystemConsoleUsage de classe


- (Data) Data de Início do Log de Segurança

- (Corda) TopConsoleUser

- (UInt32) TotalConsoleTime

- (UInt32) Utilizadores TotalConsole

- (UInt32) Hora total do loglog de segurança



## <a name="system-console-user"></a>Utilizador da consola do sistema

Espaço de nome: root\cimv2\sms

SMS_SystemConsoleUser de classe


- (Corda) SystemConsoleUser

- (Data) Última Consolautilização

- (UInt32) NumberOfConsoleLogons

- (UInt32) TotalUserConsoleMinutes



## <a name="system-devices"></a>Dispositivos do Sistema

Espaço de nome: root\cimv2\sms

CCM_SystemDevices de classe


- (Corda) Nome

- (Corda) IDs compatíveis[]

- (Corda) DispositivoID

- (Corda) HardwareIDs[]

- (Boolean) IsPnP



## <a name="system-drivers"></a>Controladores de Sistema

Espaço de nome: raiz\cimv2

Win32_SystemDriver de classe


- (Corda) Nome

- (Boolean) Aceitar Pausa

- (Boolean) AceitarParar

- (Corda) Legenda

- (Corda) Descrição

- (Boolean) DesktopInteract

- (Corda) Nome do ecrã

- (Corda) ErrorControl

- (UInt32) Código de Saída

- (Data) Data de Instalação

- (Corda) Nome do caminho

- (UInt32) ServiceSpecificExitCode

- (Corda) Tipo de serviço

- (Boolean) Iniciado

- (Corda) Modo de Arranque

- (Corda) Nome de partida

- (Corda) Estado

- (Corda) Estado

- (Corda) Nome do sistema

- (UInt32) Tagid



## <a name="system-enclosure"></a>Cobertura do Sistema

Espaço de nome: raiz\cimv2

Win32_SystemEnclosure de classe


- (Corda) Etiqueta

- (Boolean) AudibleAlarm

- (Corda) Violação Descrição

- (Corda) Estratégia de Gestão de Cabos

- (Corda) Legenda

- (UInt16) ChassisTypes[]

- (SInt16) CurrentRequiredOrProduzido

- (Corda) Descrição

- (UInt16) HeatGeneration

- (Boolean) HotSwappable

- (Data) Data de Instalação

- (Boolean) LockPresent

- (Corda) Fabricante

- (Corda) Modelo

- (Corda) Nome

- (UInt16) NumberOfPowerCords

- (Corda) OutraS Informações Identificantes

- (Corda) PartNumber

- (Boolean) PoweredOn

- (Boolean) Removível

- (Boolean) Substituível

- (UInt16) Falha de segurança

- (UInt16) Estatuto de Segurança

- (Corda) Número de série

- (Corda) Descrições do serviço[]

- (UInt16) Filosofia de Serviço[]

- (Corda) SKU

- (Corda) SMBIOSAssettag

- (Corda) Estado

- (Corda) Descrições do tipo[]

- (Corda) Versão

- (Boolean) VisibleAlarm



## <a name="tape-drive"></a>Unidade de Fita

Espaço de nome: raiz\cimv2

Win32_TapeDrive de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (UInt16) Capacidades[]

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (UInt32) Compressão

- (Corda) Método de Compressão

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt64) Tamanho de bloqueio predefinido

- (Corda) Descrição

- (UInt32) ECC

- (UInt32) EOTWarningZoneSize

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (UInt32) Características High

- (UInt32) FeaturesLow

- (Corda) ID

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt64) Tamanho MaxBlock

- (UInt64) MaxMediaSize

- (UInt32) Contagem de Partição Max

- (Corda) MediaType

- (UInt64) Tamanho MinBlockSize

- (Corda) Nome

- (Boolean) NecessidadesLimpeza

- (UInt32) NumberOfMediaSupported

- (UInt32) Acolchoamento

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt32) ReportSetmarks

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema



## <a name="time-zone"></a>Fuso Horário

Espaço de nome: raiz\cimv2

Win32_TimeZone de classe


- (Corda) Nome Padrão

- (SInt32) Preconceito

- (Corda) Legenda

- (SInt32) DaylightBias

- (UInt32) Dia do Dia do Dia da Luz do

- (UInt8) Semana do Dia do Dia do Dia do Dia do Dia

- (UInt32) Horário diurno

- (UInt32) DaylightMillisecond

- (UInt32) Minuto diurno

- (UInt32) Mês diurno

- (Corda) Nome da luz do dia

- (UInt32) DaylightSecond

- (UInt32) Ano diurno

- (Corda) Descrição

- (Corda) SettingID

- (UInt32) StandardBias

- (UInt32) Dia Padrão

- (UInt8) StandardDayOfWeek

- (UInt32) Hora Padrão

- (UInt32) StandardMillisecond

- (UInt32) StandardMinute

- (UInt32) Mês Padrão

- (UInt32) StandardSecond

- (UInt32) Ano Padrão



## <a name="tpm"></a>TPM

Espaço de nome: root\CIMv2\Security\MicrosoftTpm

Win32_Tpm de classe


- (Boolean) IsActivated_InitialValue

- (Boolean) IsEnabled_InitialValue

- (Boolean) IsOwned_InitialValue

- (UInt32) Manufacturerid

- (Corda) Versão do fabricante

- (Corda) ManufacturerVersionInfo

- (Corda) PhysicalPresenceVersionInfo

- (Corda) Espectroversão



## <a name="tpm-status"></a>Estado do TPM

Espaço de nome: root\cimv2\sms

SMS_TPM de classe


- (Boolean) IsReady

- (UInt32) Informação

- (Boolean) É Aplicável



## <a name="ts-issued-license"></a>Licença Emitida tS

Espaço de nome: raiz\cimv2

Win32_TSIssuedLicense de classe


- (UInt32) Licenciado

- (Data) Data de Validade

- (Data) Data de Emissão

- (UInt32) KeyPackid

- (UInt32) Estatuto de Licença

- (String) sHardwareId

- (String) sIssuedToComputer

- (String) sIssuedToUser



## <a name="ts-license-key-pack"></a>Pacote de chaves de licença TS

Espaço de nome: raiz\cimv2

Win32_TSLicenseKeyPack de classe


- (UInt32) KeyPackid

- (UInt32) Licenças Disponíveis

- (Corda) Descrição

- (UInt32) Licenças Emitidas

- (UInt32) TecladoPackType

- (UInt32) Tipo de Produto

- (Corda) Versão do Produto

- (UInt32) TotalLicenses



## <a name="uninterruptible-power-supply"></a>Fornecimento de energia ininterrupto

Espaço de nome: raiz\cimv2

Win32_UninterruptiblePowerSupply de classe


- (Corda) DispositivoID

- (UInt16) ActiveInputVoltage

- (UInt16) Disponibilidade

- (Boolean) BateriaInstalada

- (Boolean) CanTurnOffRemotamente

- (Corda) Legenda

- (Corda) Ficheiro de comando

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt16) Custo estimadoRemaining

- (UInt32) Tempo estimado

- (UInt32) Atraso de Primeira Mensagem

- (Data) Data de Instalação

- (Boolean) IsSwitchingSupply

- (UInt32) Código de Erro

- (Boolean) LowBatterySignal

- (UInt32) Intervalo de mensagens

- (Corda) Nome

- (Corda) PNPDeviceID

- (Boolean) PowerFailSignal

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt32) Gama1InputFrequencyHigh

- (UInt32) Range1InputFrequencyLow

- (UInt32) Gama1InputVoltageHigh

- (UInt32) Gama1InputVoltageLow

- (UInt32) Gama2InputFrequencyHigh

- (UInt32) Range2InputFrequencyLow

- (UInt32) Range2InputVoltageHigh

- (UInt32) Range2InputVoltageLow

- (UInt16) Estatuto de Capacidade Remanescente

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (UInt32) TimeOnBackup

- (UInt32) TotalOutputPower

- (UInt16) TipoOfRangeSwitching

- (Corda) UPSPort



## <a name="usb-controller"></a>Controlador USB

Espaço de nome: raiz\cimv2

Win32_USBController de classe


- (Corda) DispositivoID

- (UInt16) Disponibilidade

- (Corda) Legenda

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Descrição

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Data) Data de Instalação

- (UInt32) Código de Erro

- (Corda) Fabricante

- (UInt32) Número máximo Controlado

- (Corda) Nome

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (Data) TimeOfLastReset



## <a name="usb-device"></a>Dispositivo USB

Espaço de nome: raiz\cimv2

Win32_USBDevice de classe


- (Corda) DispositivoID

- (Corda) Legenda

- (Corda) Classguid

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Nome de Classe Criação

- (Corda) Descrição

- (Corda) Fabricante

- (Corda) Nome

- (Corda) PNPDeviceID

- (Corda) Serviço

- (Corda) Estado

- (Corda) SystemCreationClassName

- (Corda) Nome do sistema



## <a name="usm-user-profile"></a>Perfil de utilizador USM

Espaço de nome: raiz\cimv2

Win32_UserProfile de classe


- (Corda) SID

- (UInt8) Estado de Saúde

- (Corda) Última TentativadeDownloadDePerfil

- (Corda) Última TentativadePerfilUploadTime

- (Corda) Última Experiência de Registo

- (Data) Última Hora de Download

- (Data) Última Hora do Upload

- (Data) Tempo de Última Utilização

- (Boolean) Carregado

- (Corda) Caminho Local

- (UInt32) RefCount

- (Boolean) RoamingConfigurado

- (Corda) RoamingPath

- (Boolean) RoamingPreference

- (Boolean) Especial

- (UInt32) Estado



## <a name="video-controller"></a>Controlador de vídeo

Espaço de nome: raiz\cimv2

Win32_VideoController de classe


- (Corda) DispositivoID

- (UInt16) Capacidades aceleradoras[]

- (Corda) AdapterCompatibilidade

- (Corda) AdaptadorDACType

- (UInt32) AdapterRAM

- (UInt16) Disponibilidade

- (Corda) Descrições da capacidade[]

- (Corda) Legenda

- (UInt32) Entradas de Colortable

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (UInt32) CurrentBitsPerPixel

- (UInt32) Resolução Horizontal atual

- (UInt64) Número de CorrenteSCores

- (UInt32) Números de CorrenteSColunas

- (UInt32) Números de correnteSOfRows

- (UInt32) Taxa de atualização de corrente

- (UInt16) CurrentScanMode

- (UInt32) Resolução Vertical atual

- (Corda) Descrição

- (UInt32) DispositivoSpecificPens

- (UInt32) DitherType

- (Data) Data do Condutor

- (Corda) Versão do condutor

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (UInt32) ICMIntent

- (UInt32) IcMMethod

- (Corda) Nome infFile

- (Corda) InfSection

- (Data) Data de Instalação

- (Corda) Controladores de Visualização Instalados

- (UInt32) Código de Erro

- (UInt32) MaxMemorySupported

- (UInt32) Número máximo Controlado

- (UInt32) MaxRefreshRate

- (UInt32) MinRefreshRate

- (Boolean) Monocromático

- (Corda) Nome

- (UInt16) NumberOfColorPlanes

- (UInt32) NumberOfVideoPages

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (UInt16) ProtocoloSuportado

- (UInt32) Entradas reservadas systempalette

- (UInt32) EspecificaçãoVersão

- (Corda) Estado

- (UInt16) StatusInfo

- (Corda) Nome do sistema

- (UInt32) SystemPaletteEntries

- (Data) TimeOfLastReset

- (UInt16) Arquitetura de Vídeo

- (UInt16) VideomemoryType

- (UInt16) Modo de Vídeo

- (Corda) Descrição do modo de vídeo

- (Corda) Processador de Vídeo



## <a name="virtual-application-packages"></a>Pacotes de aplicações virtuais

Espaço de nome: root\Microsoft\appvirt\cliente

pacote de classe


- (Corda) Pacoteguid

- (UInt64) Tamanho de lançamento em cache

- (UInt16) CachedPercentage

- (UInt64) CachedSize

- (UInt64) Tamanho de lançamento

- (Corda) Nome

- (Corda) SftPath

- (UInt64) Totalsize

- (Corda) Versão

- (Corda) VersãoGUID



## <a name="virtual-applications"></a>Aplicações Virtuais

Espaço de nome: root\Microsoft\appvirt\cliente

candidatura de classe


- (Corda) Nome

- (Corda) Versão

- (Corda) CachedOsdPath

- (UInt32) Contagem global de corridas

- (Data) Sistema LastLaunchOn

- (Boolean) Carregamento

- (Corda) OriginalOsdPath

- (Corda) Pacoteguid



## <a name="virtual-machine-64"></a>Máquina Virtual (64)

Espaço de nome: raiz\cimv2

Win32Reg_SMSGuestVirtualMachine64 de classe


- (Corda) InstânciaChave

- (Corda) Nome de anfitrião físico

- (Corda) Hospedeiro Físico Qualificado



## <a name="virtual-machine"></a>Máquina Virtual

Espaço de nome: raiz\cimv2

Win32Reg_SMSGuestVirtualMachine de classe


- (Corda) InstânciaChave

- (Corda) Nome de anfitrião físico

- (Corda) Hospedeiro Físico Qualificado



## <a name="virtual-machine-details"></a>Detalhes da máquina virtual

Espaço de nome: root\vm\VirtualServer

classe VirtualMachine


- (Corda) Nome

- (UInt32) CpuUtilização

- (UInt64) DiskBytesRead

- (UInt64) DiskBytesEscrito

- (UInt64) DiskSpaceUsed

- (UInt64) Contagem de batimentos cardíacos

- (UInt32) Intervalo do Batimento Cardíaco

- (UInt32) HeartbeatPercentage

- (UInt32) Batimento cardíaco

- (UInt64) NetworkBytesReceived

- (UInt64) NetworkBytesSent

- (UInt64) Memória FísicaAtribuída

- (UInt32) Tempo de subida



## <a name="volume"></a>Volume

Espaço de nome: raiz\cimv2

Win32_Volume de classe


- (Corda) DispositivoID

- (UInt16) Acesso

- (Boolean) Montagem automática

- (UInt16) Disponibilidade

- (UInt64) BlockSize

- (UInt64) Capacidade

- (Corda) Legenda

- (Boolean) Comprimido

- (UInt32) ConfigManagerErrorCode

- (Boolean) ConfigManagerUserConfig

- (Corda) Nome de Classe Criação

- (Corda) Descrição

- (Boolean) DirtyBitSet

- (Corda) Carta de condução

- (UInt32) Tipo de condução

- (Boolean) Erro Ilibado

- (Corda) Descrição de erros

- (Corda) Metodologia de Erro

- (Corda) Sistema de Ficheiros

- (UInt64) FreeSpace

- (Boolean) IndexaçãoHabilitado

- (Data) Data de Instalação

- (Corda) Etiqueta

- (UInt32) Código de Erro

- (UInt32) Comprimento máximo do nome do ficheiro

- (Corda) Nome

- (UInt64) NumberOfBlocks

- (Corda) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (Boolean) PowerManagementSupported

- (Corda) Propósito

- (Boolean) QuotasHabilitadas

- (Boolean) QuotasIncomplete

- (Boolean) Quotas Reconstrução

- (UInt32) Número de série

- (Corda) Estado

- (UInt16) StatusInfo

- (Boolean) SuportaDiskQuotas

- (Boolean) SuportesFileBasedCompression

- (Corda) SystemCreationClassName

- (Corda) Nome do sistema



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

Espaço de nome: root\ccm\cimodels

CCM_WebAppInstallInfo de classe


- (Corda) AppDeliveryTypeid

- (UInt32) AppDtRevision

- (Corda) TargetURL

- (Corda) UserSID

- (Corda) NOME URLFile

- (Corda) URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

Espaço de nome: root\cimv2\sms

SMS_Windows8Application de classe


- (Corda) Nome completo

- (Corda) Nome de aplicação

- (Corda) Arquitetura

- (Boolean) ConfigMgrManaged

- (Corda) Nomes de Aplicações de Dependência

- (Corda) Nome de família

- (Corda) Localização Instalada

- (Boolean) IsFramework

- (Corda) Editora

- (Corda) Publisherid

- (Corda) Versão



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

Espaço de nome: root\cimv2\sms

SMS_Windows8ApplicationUserInfo de classe


- (Corda) Nome completo

- (Corda) UserSecurityId

- (Corda) Instalação Do Estado

- (Corda) Nome da Conta de Utilizador



## <a name="windows-update"></a>Windows Update

Espaço de nome: raiz\cimv2

Win32Reg_SMSWindowsUpdate de classe


- (Corda) InstânciaChave

- (UInt32) AuOptions

- (UInt32) NoAutoUpdate

- (UInt32) UseWUServer



## <a name="windows-update-agent-version"></a>Versão do Agente de Atualização do Windows

Espaço de nome: root\cimv2\sms

Win32_WindowsUpdateAgentVersion de classe


- (Corda) Versão



## <a name="write-filter-state"></a>Escreva estado de filtro

Espaço de nome: root\cimv2\sms

CCM_WriteFilterState de classe


- (Boolean) WriteFilterEnabled
