---
title: Compreender entre intune e azure limite restrições
titleSuffix: ''
description: Compreenda as diferenças entre as restrições de limite de dispositivos da Intune e as restrições de delimitação da Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 749b648cb3527c75aac85fd7817b918a61f3a2a8
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83733644"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Compreender as restrições de limite de dispositivos da Intune e da Azure AD

As restrições de limite do dispositivo podem ser configuradas de duas formas:
- Inscrição intonizada
- Azure Ative Directory (AD) juntou-se ou Azure AD registrado

Este artigo esclarece quando estes limites são aplicados com base na sua configuração.

## <a name="intune-device-limit-restrictions"></a>Restrições de limite de dispositivos insinados

As restrições de limitação do dispositivo insintonizam o número máximo de dispositivos que um utilizador pode controlar (a regulação máxima é de 15). Para definir este limite de **dispositivo,** vá ao [microsoft Endpoint Manager administrador do centro](https://go.microsoft.com/fwlink/?linkid=2109431)de  >  aplicação**de**  >  **restrições**de inscrição . Para mais informações, consulte [Criar uma restrição de limite](enrollment-restrictions-set.md#create-a-device-limit-restriction) de dispositivo

## <a name="azure-device-limit-restriction"></a>Restrição de limite de dispositivo sinuoso do dispositivo Azure

As restrições de limitação do dispositivo Azure estabelecem o número máximo de dispositivos que o Azure AD junta ou o Azure AD regista. Para definir o **número máximo de dispositivos por utilizador,** vá ao portal Azure > Dispositivos **de Diretório Ativo Azure**  >  **Devices**. Para mais informações, consulte [as definições do dispositivo Configure](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="settings-applied-based-on-user-affinity"></a>Definições aplicadas com base na afinidade do utilizador

Se tiver as restrições de limite do dispositivo Intune e Azure definidas, a tabela que se segue mostra-lhe o que é aplicado com base na definição de afinidade do utilizador.

| Plataforma de dispositivo | Afinidade do utilizador | Azure aplica-se | Intune aplica-se |
| ----- | ----- | ----- | ----- | ----- |
| Perfil de trabalho android Enterprise | Sim | Sim | Sim|
| Dispositivo dedicado android enterprise | Não | Não | Não |
| Android Enterprise totalmente gerido | Sim | Sim | Sim |
| Android device administrator (Administrador de dispositivos Android) | Sim | Sim | Sim |
| Administrador de dispositivos Android DEM | Não | | Não | 
| iOS/macOS BYOD | Sim | Sim | Sim |
| Inscrição de dispositivos automatizados iOS/macOS (ADE) | Sim | Sim | Sim |
| iOS/macOS ADE | Não | Sim | Não |
| Windows BYOD | Sim | Sim | Sim |
| Apenas para O MD do Windows | | Sim | Sim |
| AD do Windows Azure juntou-se| Sim | Sim | Não |
| Windows Autopilot | Sim | Sim | Não |
| AD Azure híbrido windows juntou-se | Não | Não | Sim |
| Cogestão do Windows | Não | Sim | Não |
| Windows DEM | Não | Sim | Não |
| Inscrição a granel do Windows | Não | Sim | Não |


## <a name="android-and-ios-devices"></a>Dispositivos Android e iOS

### <a name="ios-or-android-devices-example-1"></a>iOS ou dispositivos Android exemplo 1

- O **número máximo de dispositivos Azure por** definição de utilizador está definido para 3.
- A definição de limite do **dispositivo** intune está definida para 5.
 
**Resultado:** O número máximo é por utilizador. Por exemplo, se inscrever três dispositivos Intune, o registo Azure para o quarto dispositivo falhará devido às definições para limitar o número de inscrições para os dispositivos.

### <a name="ios-or-android-devices-example-2"></a>iOS ou dispositivos Android exemplo 2

- O **número máximo de dispositivos Azure por** definição de utilizador está definido para 20.
- A definição de limite do **dispositivo** intune está definida para 2.

**Resultado:** Pode registar-se e inscrever com sucesso dois dispositivos. A inscrição intonizada será bloqueada para quaisquer dispositivos adicionais. O ADE sem afinidade do utilizador é restringido pelos limites de registo do dispositivo Azure, embora não esteja associado a um utilizador.

## <a name="windows-devices"></a>Dispositivos Windows

As restrições de limite do dispositivo intonnão se aplicam para os seguintes tipos de matrículas do Windows:
- Inscrições cogeridas
- Inscrições de objetos de política de grupo (GPO)
- Azure AD juntou-se às matrículas
- A AD agranel Azure juntou-se às matrículas
- Inscrições no Autopilot
- Inscrições do gestor de inscrição do dispositivo

Não é possível impor restrições de limite de dispositivos para estes tipos de matrículas porque são considerados cenários de dispositivos partilhados. Pode definir limites fixos para estes tipos de inscrição no Azure Active Directory.

Para a restrição de limite de dispositivo seletiva em Azure, o **número máximo de dispositivos por** definição de utilizador aplica-se a dispositivos que estejam a aderir a Azure AD ou a Azure AD registada. Esta definição não se aplica aos dispositivos híbridos Azure AD.

### <a name="windows-10-example-1"></a>Windows 10 exemplo 1

- O **número máximo de dispositivos Azure por** definição de utilizador está definido para 5.
- A definição de limite do **dispositivo** intune está definida para 3.
- Os dispositivos são híbridos Azure AD unidos e matriculados automaticamente (GPO configurado).

**Resultado:** Como a inscrição é empurrada através de GPO, o limite de registo do dispositivo Azure não se aplica.  A restrição de limite do dispositivo Intune também não se aplica.

### <a name="windows-10-example-2"></a>Windows 10 exemplo 2

- O **número máximo de dispositivos Azure por** definição de utilizador está definido para 5.
- A definição de limite do **dispositivo** intune está definida para 2.
- Os dispositivos são de domínio local unidos e matriculados utilizando **definições**  >  **De Acesso ao Trabalho ou**  >  **Ligação**Escolar .

**Resultado:** Só pode sinuosar dois dispositivos antes de serem bloqueados. Pode registar até cinco dispositivos.


## <a name="next-steps"></a>Próximos passos

- [Crie uma restrição de limite de dispositivo em Azure.](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal.md#configure-device-settings)
- [Configure as definições do dispositivo em Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Saiba mais sobre o registo e o domínio adeferido.](https://docs.microsoft.com/azure/active-directory/devices/overview.md#getting-devices-in-azure-ad)