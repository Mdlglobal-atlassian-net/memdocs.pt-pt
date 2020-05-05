---
title: Registo de eventos de clientes
titleSuffix: Configuration Manager
description: Uma referência técnica para as possíveis entradas de clientes BitLocker (MBAM) no registo de eventos do Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722061"
---
# <a name="client-event-logs"></a>Registo de eventos de clientes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Num cliente do Gestor de Configuração para o qual implementa uma política de gestão BitLocker, utilize o Windows Event Viewer para visualizar os registos de eventos do cliente BitLocker. Aceda a Registos de **Aplicações e Serviços,** **Microsoft,** **Windows,** **MBAM** para registos de eventos [de administração](#admin) e [operacionais.](#operational)

## <a name="admin"></a>Administrador

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Ocorreu um erro ao aplicar as políticas de MBAM.

#### <a name="error-code--2144272219"></a>Código de erro: -2144272219

Detalhes: A encriptação bitLocker Drive apenas suporta encriptação de espaço usado apenas em armazenamento fino.

Este erro ocorre se tentar utilizar o BitLocker para encriptar uma máquina virtual que está a executar a versão 1803 do Windows 10 ou mais cedo. As versões anteriores do Windows 10 não suportam encriptação completa do disco. As políticas de gestão bitLocker impõem encriptação completa do disco.

#### <a name="error-code--2147024774"></a>Código de erro: -2147024774

Detalhes: A área de dados passada para uma chamada do sistema é muito pequena.

Para resolver este problema, reinicie o computador.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Ocorreu um erro ao enviar dados do estado de encriptação.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

O volume do sistema está em falta. O SystemVolume é necessário para encriptar a unidade do sistema operativo.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

O hardware da TPM desapareceu. O TPM é necessário para encriptar a unidade do sistema operativo com qualquer protetor TPM.

### <a name="10-machinehwexempted"></a>10: MáquinaHWIsento

O computador está isento de encriptação. Estado de hardware da máquina: Isento

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

O computador está isento de encriptação. Estado de hardware da máquina: Desconhecido

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Verificação de isenção de hardware falhou.

### <a name="13-userisexempted"></a>13: UserIsExempted

O utilizador está isento de encriptação.

### <a name="14-useriswaiting"></a>14: UserisWaiting

O utilizador solicitou uma isenção.

### <a name="15-userexemptioncheckfailed"></a>15: Isenção de utilizadorCheckFailed

Verificação de isenção de utilizador falhou.

### <a name="16-userpostponed"></a>16: Utilizador Adiado

O utilizador adiou o processo de encriptação.

### <a name="17-tpminitializationfailed"></a>17: TPMInicializaçãoFalha

A inicialização do TPM falhou. O utilizador rejeitou as alterações bios.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Incapaz de ligar ao serviço mbam recovery e hardware.

#### <a name="error-code--2147024809"></a>Código de erro: -2147024809

Detalhes: O parâmetro está incorreto.

Este erro ocorre se o site não estiver HTTPS, ou se o cliente não tiver um certificado PKI.

### <a name="20-policymismatch"></a>20: PolicyMismatch

A política de gestão bitLocker está em conflito ou corrupta.

### <a name="21-conflictingosvolumepolicies"></a>21: Políticas contraditórias de volume de volume

As políticas de encriptação do volume de sotação detetadas entram em conflito. Verifique as políticas bitLocker relacionadas com protetores de unidade sO.

### <a name="22-conflictingfddvolumepolicies"></a>22: Políticas contraditórias de Volume de Volumes

As políticas de encriptação de volume de dados fixos detetadas são detetadas. Verifique as políticas bitLocker relacionadas com protetores de unidade de unidade de dados fixos.

### <a name="27-encryptionfailednodra"></a>27: EncriptaçãoFailedNoDra

Ocorreu um erro durante a encriptação. É necessário um protetor de agente de recuperação de dados (DRA) no modo FIPS para máquinas pré-Windows 8.1.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Falhou em repor o bloqueio do TPM.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Não conseguiu recuperar a TPM OwnerAuth dos serviços MBAM.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Falhou em atualizar o caminho de pesquisa da DLL para o fornecedor wMI.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Agente a parar. Cronometrado à espera da instância do fornecedor MBAM WMI.

## <a name="operational"></a>Operacional

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

As políticas de gestão bitLocker foram aplicadas com sucesso.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Os dados do estado de encriptação foram enviados com sucesso.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Ligado com sucesso ao serviço mbam recovery e hardware.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

O TPM OwnerAuth foi depositado.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

A chave de recuperação BitLocker para o volume foi depositada.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

A chave de recuperação BitLocker para o volume foi atualizada.

### <a name="31-enforcepolicydateset"></a>31: Conjunto de datações de aplicação da política

A data da política de aplicação... foi definido para o volume

### <a name="32-enforcepolicydatecleared"></a>32: Datação da Aplicação da Política Apurada

A data da política de aplicação... foi apurado para o volume.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Repor com sucesso o bloqueio do TPM.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceed

Recuperado com sucesso a TPM OwnerAuth dos serviços MBAM.

### <a name="39-removabledrivemounted"></a>39: RemovívelDriveMounted

Unidade amovível foi montada.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismontado

A unidade amovível estava desmontada.

### <a name="41-failedtoenactendpointunreachable"></a>41: FalhadoToEnactEndpoint Inalcançável

A não ligação ao serviço mbam recovery e hardware impediu que as políticas de gestão do BitLocker fossem aplicadas com sucesso ao volume.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

O estado de volume bloqueado impediu que as políticas de gestão bitLocker fossem aplicadas com sucesso ao volume.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

A não ligação ao serviço MBAM Compliance and Status impediu a transferência de dados do estado de encriptação.

## <a name="see-also"></a>Consulte também

Para obter mais informações sobre a utilização destes registos, consulte os registos do [evento BitLocker](about-event-logs.md).

Para obter mais informações sobre resolução de problemas, consulte [Troubleshoot BitLocker](troubleshoot.md).
