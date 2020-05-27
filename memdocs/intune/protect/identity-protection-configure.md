---
title: Utilize um PIN para iniciar sessão nos dispositivos do Windows 10 utilizando o Microsoft Intune - Azure [ Microsoft Docs
description: Utilize o Windows Hello for Business para permitir que os utilizadores instiem dispositivos com um PIN, uma impressão digital e muito mais. Crie um perfil de configuração de proteção de identidade em Intune para dispositivos Windows 10 com estas definições e atribua o perfil a grupos de utilizadores e grupos de dispositivos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 896574f956353c526858356fea40c2248ce70dd3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990798"
---
# <a name="use-windows-hello-for-business-on-windows-10-devices-with-microsoft-intune"></a>Utilize o Windows Hello para negócios em dispositivos Windows 10 com microsoft Intune

O Windows Hello for Business é um método para iniciar sessão nos dispositivos Windows, substituindo senhas, cartões inteligentes e cartões inteligentes virtuais. Intune inclui configurações incorporadas para que os Administradores possam configurar e usar o Windows Hello para Negócios. Por exemplo, pode utilizar estas definições para:

- Ativar o Windows Hello para Negócios para dispositivos e utilizadores
- Definir requisitos PIN do dispositivo, incluindo um comprimento pin mínimo ou máximo
- Permitir gestos, como uma impressão digital, que os utilizadores podem (ou não podem usar) para iniciar sessão em dispositivos

Esta funcionalidade aplica-se a dispositivos que executem:

- Windows 10 e posterior
- Windows 10 Mobile
- Windows Holographic for Business

Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, empurre ou implemente estas definições para grupos de utilizadores e dispositivos na sua organização.

Este artigo mostra-lhe como criar um perfil de configuração do dispositivo. Para obter uma lista de todas as definições e o que fazem, consulte [as definições do dispositivo do Windows 10 para ativar o Windows Hello for Business](identity-protection-windows-settings.md).

## <a name="create-the-device-profile"></a>Criar o perfil do dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Introduza as seguintes propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
   - **Plataforma**: Selecione **o Windows 10 e mais tarde**. O Windows Hello para Empresas só é suportado em dispositivos com o Windows 10 e versões posteriores.
   - **Tipo de perfil**: Selecione **a proteção de identidade**.

4. No painel *Windows Hello for Business,* configure as seguintes opções:

   - **Configure o Windows Hello for Business**: Escolha como pretende configurar o Windows Hello for Business:

     - **Não configurado** (predefinido): [Disposições Do Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning) no dispositivo. Quando atribuir perfis de proteção de identidade apenas a utilizadores, o contexto do dispositivo assume a predefinição **Não configurado**.

     - **Desativado**: Se não quiser utilizar o Windows Hello for Business, selecione esta opção. Esta opção desativa o Windows Hello for Business para todos os utilizadores.

     - **Ativado**: Escolha esta opção para [fornecer](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning)e configure as definições do Windows Hello for Business em Intune. Introduza as definições que pretende configurar. Para uma lista de todas as definições, e o que eles fazem, ver - definições do [dispositivo Do Windows 10 para ativar o Windows Hello for Business](identity-protection-windows-settings.md).

   - **Utilize as chaves de segurança para iniciar sessão**: Ative a chave de segurança Windows Hello como credencial de início de sessão para todos os Computadores do inquilino.

     - **Ativar**
     - **Não configurado** (padrão)

5. Quando terminar, selecione **OK**  >  **Create** para guardar as suas alterações.

O perfil é criado e aparece na lista de perfis. Em seguida, [atribua](../configuration/device-profile-assign.md) este perfil aos grupos de utilizadores e dispositivos para atender às suas necessidades.

> [!IMPORTANT]
> Para permitir que vários utilizadores sejam aprovisionados num dispositivo, especifique que a política do Windows Hello for Business seja aplicada aos dispositivos. Se a apólice for aplicada apenas aos utilizadores, apenas um utilizador pode ser provisionado a um dispositivo.

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/identity-protection-configure/disable-android-camera.png)

-->

## <a name="next-steps"></a>Passos seguintes

- Veja uma lista de todas [as definições e o que fazem.](identity-protection-windows-settings.md)
- [Atribua o perfil](../configuration/device-profile-assign.md) e [monitorize o respetivo estado](../configuration/device-profile-monitor.md).
