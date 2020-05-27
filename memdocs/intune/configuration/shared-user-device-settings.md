---
title: Definições de dispositivos partilhados ou multiutilizadores no Microsoft Intune - Azure / Microsoft Docs
description: Adicione e utilize o Windows 10 e o Windows Holographic para dispositivos Empresariais partilhados ou utilizados por vários utilizadores no Microsoft Intune. Consulte uma lista de todas as definições e o que fazem nos dispositivos, incluindo o Microsoft HoloLens. Controle as contas dos hóspedes, gere as contas e elimine contas inativas, permita ou previna a poupança para o armazenamento local, delineie opções de energia e sono, escolha quando as atualizações são instaladas e utilize dispositivos em ambientes de educação num perfil de configuração do dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
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
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984005"
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
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

   - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
   - **Perfil**: Selecione **dispositivo multiutilizador partilhado**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

    - [Windows 10 e posterior](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Selecione **Seguinte**.

9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Tarefas,** selecione o grupo de dispositivos que receberá o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

    > [!NOTE]
    > Certifique-se de atribuir o perfil a grupos de dispositivos na sua organização.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

Da próxima vez que cada dispositivo entrar, a apólice é aplicada.

## <a name="next-steps"></a>Passos seguintes

- Consulte todas as definições para [windows 10 e mais recente](shared-user-device-settings-windows.md) e Windows [Holographic para Negócios](shared-user-device-settings-windows-holographic.md).
- Depois de atribuído o [perfil,](device-profile-assign.md) [monitorize o seu estado](device-profile-monitor.md).
