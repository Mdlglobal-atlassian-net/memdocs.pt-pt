---
title: Definições de dispositivos partilhados do Windows Holographic Business - Microsoft Intune - Azure [ Microsoft Docs
description: Adicione e utilize o Windows Holographic para o Negócio sintetizar dispositivos partilhados ou utilizados por vários utilizadores no Microsoft Intune. Consulte uma lista das definições de Gestão de Conta e o que fazem nos dispositivos, incluindo o Microsoft HoloLens.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b7e77933134dae3523edaf45f8b345aca4fc162
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326637"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Windows Holographic para configurações de Negócios para gerir dispositivos partilhados usando Intune

O Windows Holographic para dispositivos Empresariais, como o Microsoft HoloLens, pode ser utilizado por vários utilizadores. Os dispositivos que têm vários utilizadores são chamados dispositivos partilhados, e fazem parte das soluções de gestão de dispositivos móveis (MDM).

Utilizando o Microsoft Intune, os utilizadores podem iniciar sessão nestes dispositivos partilhados com uma conta de hóspedes. À medida que utilizam o dispositivo, só têm acesso às funcionalidades que permite.

Este artigo lista e descreve as definições que utiliza num perfil de configuração do Windows Holographic para dispositivos Empresariais. Quando o perfil é criado em Intune, então implementa ou atribui o perfil a grupos de dispositivos na sua organização. Também pode atribuir este perfil a um grupo de dispositivos com tipos de dispositivos mistos e versões DE SO.

Para obter mais informações sobre esta funcionalidade em Intune, consulte o acesso ao [Controlo, contas e funcionalidades de energia em dispositivos de PC ou multiutilizadores partilhados](shared-user-device-settings.md). Para obter mais informações sobre o CSP do Windows, consulte [O CSP](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)de Gestão de Conta .

## <a name="before-your-begin"></a>Antes do seu início

[Criar o perfil.](shared-user-device-settings.md)

## <a name="shared-multi-user-device-settings"></a>Definições partilhadas de dispositivos multiutilizadores

> [!NOTE]
> Os dispositivos que executam o Windows Holographic para negócios, incluindo os Microsoft HoloLens, apenas suportam as definições de gestão da **Conta.** Se configurar qualquer uma das outras definições mostradas no Intune, incluindo o **modo de PC partilhado,** não tem qualquer impacto nestes dispositivos.

- **Gestão de conta**: Definir para **permitir** a eliminação automática de contas locais criadas pelos hóspedes e contas em AD e Azure AD. Quando um utilizador assina fora do dispositivo, ou quando a manutenção do sistema é executado, estas contas são eliminadas. Quando ativado, também definido:
  - **Eliminação da conta**: Escolha quando as contas são eliminadas: **No limiar**do espaço de armazenamento , no limiar do espaço de armazenamento e no **limiar inativo,** ou imediatamente após o **log-out**. Também insira:
    - **Comece a eliminar o limiar(%)**: Introduza uma percentagem (0-100) de espaço em disco. Quando o espaço total de disco/armazenamento cai abaixo do valor que introduz, as contas em cache são eliminadas. Elimina continuamente as contas para recuperar o espaço do disco. As contas que estão inativas há mais tempo são eliminadas primeiro.
    - **Parar de eliminar limiar(%)**: Insira uma percentagem (0-100) do espaço do disco. Quando o espaço total de disco/armazenamento corresponde ao valor que introduz, a apagar para.

  Configurado para **Desativar** para manter as contas ad locais, AD e Azure criadas pelos hóspedes.

  > [!NOTE]
  > Os dispositivos Microsoft HoloLens apenas suportam as definições de gestão da **Conta.**

## <a name="next-steps"></a>Passos seguintes

- [Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
- Consulte as definições para [o Windows 10 e mais recente](shared-user-device-settings-windows.md).
