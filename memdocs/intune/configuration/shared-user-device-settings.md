---
title: Definições de dispositivos partilhados ou multiutilizadores no Microsoft Intune - Azure / Microsoft Docs
description: Adicione e utilize o Windows 10 e o Windows Holographic para dispositivos Empresariais partilhados ou utilizados por vários utilizadores no Microsoft Intune. Consulte uma lista de todas as definições e o que fazem nos dispositivos, incluindo o Microsoft HoloLens. Controle as contas dos hóspedes, gere as contas e elimine contas inativas, permita ou previna a poupança para o armazenamento local, delineie opções de energia e sono, escolha quando as atualizações são instaladas e utilize dispositivos em ambientes de educação num perfil de configuração do dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 179314f363c8f086239b2c926c4bed8d09c68204
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333041"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Controle o acesso, contas e funcionalidades de potência em dispositivos de PC ou multiutilizadores partilhados utilizando o Intune

Os dispositivos que têm vários utilizadores são chamados dispositivos partilhados, e são uma parte comum das soluções de gestão de dispositivos móveis (MDM). Utilizando o Microsoft Intune, pode personalizar dispositivos partilhados que executam as seguintes plataformas:

- Windows 10 Profissional e mais recente
- Windows 10 Enterprise e mais recente
- Windows Holographic for Business, como os HoloLens

Por exemplo, as escolas têm dispositivos que são normalmente usados por muitos alunos. Com esta definição, o administrador intune da escola pode ligar a funcionalidade de PC partilhado para permitir um utilizador de cada vez. Os alunos não podem alternar entre diferentes contas de assinatura no dispositivo. Quando o aluno se inscreve, também opta por remover todas as definições específicas do utilizador.

Os utilizadores finais podem iniciar sessão nestes dispositivos partilhados com uma conta de hóspedes. Após o inicio dos utilizadores, as credenciais são em cache. À medida que utilizam o dispositivo, os utilizadores finais só têm acesso às funcionalidades que permite. Por exemplo, escolhe quando o dispositivo entra no modo de sono, se os utilizadores podem ver e guardar ficheiros localmente, ativar ou desativar as definições de gestão de energia, e muito mais. Também controla se a conta de hóspedes apaga quando o utilizador assina ou elimina contas inativas quando um limiar é atingido.

Este artigo mostra-lhe como criar um perfil de configuração e inclui links para as definições disponíveis com as suas descrições.

Quando o perfil é criado em Intune, implementa ou atribui o perfil a grupos de dispositivos na sua organização. Também pode atribuir este perfil a grupos de dispositivos com tipos de dispositivos mistos e versões de sistema operativo (OS).

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione perfis de**configuração** > de **dispositivos** > **Criar perfil**.
3. Introduza as seguintes propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
   - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
   - **Tipo de perfil**: Selecione **dispositivo multiutilizador partilhado**.

4. Configure as definições para [windows 10 e posteriormente](shared-user-device-settings-windows.md) ou [Windows Holographic para Negócios](shared-user-device-settings-windows-holographic.md).

5. Selecione **OK** > **Criar** para guardar as suas alterações.

O teu perfil é criado e mostrado na lista, mas ainda não está a fazer nada. Certifique-se de [atribuir o perfil](device-profile-assign.md) a grupos de dispositivos na sua organização.

## <a name="next-steps"></a>Passos seguintes

- Consulte todas as definições para [windows 10 e mais recente](shared-user-device-settings-windows.md) e Windows [Holographic para Negócios](shared-user-device-settings-windows-holographic.md).
- [Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
