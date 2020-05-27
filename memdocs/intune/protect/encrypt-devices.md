---
title: Criptografe dispositivos Windows 10 com BitLocker em Intune
titleSuffix: Microsoft Intune
description: Criptografe os dispositivos com o método de encriptação incorporada bitLocker e gereas as chaves de recuperação para esses dispositivos encriptados a partir do portal Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 16a2558a0f4b002528e749f4a66d3341e83c8576
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989662"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Gerir a política bitLocker para windows 10 em Intune

Utilize insinopara configurar a encriptação bitLocker drive em dispositivos que executam o Windows 10.

O BitLocker está disponível em dispositivos que executam o Windows 10 ou mais tarde. Algumas definições para o BitLocker requerem que o dispositivo tenha um TPM suportado.

Utilize um dos seguintes tipos de políticas para configurar o BitLocker nos seus dispositivos geridos

- Política de encriptação do disco de **[segurança endpoint para Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)**. O perfil BitLocker na *segurança endpoint* é um grupo focado de configurações que é dedicado a configurar o BitLocker.

  Ver as definições bitLocker que estão disponíveis nos [perfis bitLocker a partir da política de encriptação do disco](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Perfil de configuração do dispositivo para proteção de ponto final para O Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)**. As definições bitLocker são uma das categorias de definições disponíveis para a proteção do ponto final do Windows 10.

  Consulte as definições bitLocker que estão disponíveis para bitLocker em perfis de [proteção final de perfis](../protect/endpoint-protection-windows-10.md#windows-settings)de configuração do dispositivo .

> [!TIP]
> Intune fornece um relatório de [encriptação](encryption-monitor.md) incorporado que apresenta detalhes sobre o estado de encriptação dos dispositivos, em todos os seus dispositivos geridos. Depois de o Intune encriptar um dispositivo Windows 10 com o BitLocker, pode visualizar e recuperar as chaves de recuperação do BitLocker quando visualizar o relatório de encriptação.
>
> Também pode aceder a informações importantes para o BitLocker a partir dos seus dispositivos, conforme encontrado no Azure Ative Directory (Azure AD).
[relatório de encriptação](encryption-monitor.md) que apresenta detalhes sobre o estado de encriptação dos dispositivos, em todos os seus dispositivos geridos.

## <a name="permissions-to-manage-bitlocker"></a>Permissões para gerir o BitLocker

Para gerir o BitLocker intune, a sua conta deve ter as permissões de controlo de acesso (RBAC) baseadas em [funções](../fundamentals/role-based-access-control.md) aplicáveis.

Seguem-se as permissões BitLocker, que fazem parte da categoria de tarefas Remotas, e as funções RBAC incorporadas que concedem a permissão:

- **Teclas BitLocker rotatm**
  - Operador de mesa de ajuda

## <a name="create-and-deploy-policy"></a>Criar e implementar política

Utilize um dos seguintes procedimentos para criar o tipo de política que prefere.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Criar uma política de segurança de ponto final para o BitLocker

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione a encriptação de **fim de segurança**Do  >  **disco**  >  **Criar política**.

3. Definir as seguintes opções:
   1. **Plataforma**: Windows 10 ou mais tarde
   2. **Perfil**: BitLocker

   ![Selecione o perfil BitLocker](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Na página de definições de **Configuração,** configure as definições para o BitLocker para atender às necessidades do seu negócio.  

   Se pretender ativar o BitLocker em silêncio, consulte [o BitLocker silenciosamente nos dispositivos,](#silently-enable-bitlocker-on-devices)neste artigo para obter pré-requisitos adicionais e as configurações de configuração específicas que deve utilizar.

   Selecione **Seguinte**.

5. Na página **Scope (Tags),** escolha **Selecione etiquetas** de âmbito para abrir o painel de etiquetas Select para atribuir etiquetas de âmbito ao perfil.

   Selecione **Seguinte** para continuar.

6. Na página **de Atribuiçãos,** selecione os grupos que receberão este perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de utilizador e dispositivo de atribuição.

   Selecione **Seguinte**.

7. Na página **Review + criar** página, quando terminar, escolha **Criar**. O novo perfil é apresentado na lista quando seleciona o tipo de política para o perfil que criou.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Criar um perfil de configuração do dispositivo para o BitLocker

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Definir as seguintes opções:
   1. **Plataforma**: Windows 10 e mais tarde
   2. **Tipo de perfil**: Proteção do ponto final

   ![Selecione o perfil BitLocker](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Selecione **Definições**  >  **de encriptação do Windows**.

   ![Definições bitLocker](./media/encrypt-devices/bitlocker-settings.png)

5. Configure as definições para o BitLocker para atender às necessidades do seu negócio.

   Se pretender ativar o BitLocker em silêncio, consulte [o BitLocker silenciosamente nos dispositivos,](#silently-enable-bitlocker-on-devices)neste artigo para obter pré-requisitos adicionais e as configurações de configuração específicas que deve utilizar.

6. Selecione **OK**.

7. Complete a configuração de configurações adicionais e, em seguida, guarde o perfil.

## <a name="manage-bitlocker"></a>Gerir o BitLocker

Para visualizar informações sobre dispositivos que recebem a política bitLocker, consulte a [encriptação](../protect/encryption-monitor.md)do disco Monitor . Também pode visualizar e recuperar as chaves de recuperação do BitLocker quando visualiza o relatório de encriptação.

### <a name="silently-enable-bitlocker-on-devices"></a>Ativar silenciosamente o BitLocker nos dispositivos

Pode configurar uma política BitLocker que automaticamente e silenciosamente ativa o BitLocker num dispositivo. Isto significa que o BitLocker permite com sucesso sem apresentar qualquer UI ao utilizador final, mesmo quando esse utilizador não é um Administrador local no dispositivo.

**Pré-requisitos do dispositivo:**

Um dispositivo deve satisfazer as seguintes condições para ser elegível para permitir silenciosamente o BitLocker:

- O dispositivo deve executar a versão 1809 do Windows 1809 ou mais tarde
- O dispositivo deve ser Azure AD Joined  

**Configuração da política BitLocker:**

As seguintes duas definições para as definições de *base bitLocker* devem ser configuradas na política BitLocker:

- **Aviso para outra encriptação**  =  do disco *Bloco.*
- **Permitir que os utilizadores padrão permitam a encriptação durante o Azure AD Join**  =  *Permitir*

A política BitLocker **não deve exigir** a utilização de um PIN de arranque ou chave de arranque. Quando é *necessária*uma chave PIN ou chave de arranque de arranque TPM, o BitLocker não consegue ativar silenciosamente e requer interação do utilizador final.  Este requisito é cumprido através das seguintes três definições de *unidade BitLocker OS* na mesma política:

- PIN de **arranque tpm compatível** não deve ser definido para exigir PIN de arranque com *TPM*
- Chave de **arranque TPM compatível** não deve ser definida para exigir chave de arranque com *TPM*
- Chave de **arranque TPM compatível e PIN** não devem definir para exigir chave de arranque e PIN com *TPM*

### <a name="view-details-for-recovery-keys"></a>Ver detalhes para chaves de recuperação

Intune fornece acesso à lâmina AD Azure para BitLocker para que possa ver IDs de chave BitLocker e chaves de recuperação para os seus dispositivos Windows 10, a partir do portal Intune. Para ser acessível, o aparelho deve ter as chaves depositadas na AD Azure.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos**  >  **Todos os dispositivos**.

3. Selecione um dispositivo da lista e, em seguida, sob *o Monitor,* selecione **teclas recovery**.
  
   Quando as chaves estiverem disponíveis em Azure AD, as seguintes informações estão disponíveis:
   - Id da chave BitLocker
   - Chave de recuperação bitLocker
   - Tipo de Unidade

   Quando as teclas não estiverem em Azure AD, intune apresentará *nenhuma tecla BitLocker encontrada para este dispositivo*.

A informação para o BitLocker é obtida utilizando o fornecedor de serviços de [configuração BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) (CSP). O BitLocker CSP é suportado na versão 1703 do Windows 10 e posteriormente, e para a versão 1809 do Windows 10 Pro.

### <a name="rotate-bitlocker-recovery-keys"></a>Teclas de recuperação BitLocker rotativas

Pode utilizar uma ação do dispositivo Intune para rodar remotamente a chave de recuperação BitLocker de um dispositivo que executa a versão 1909 do Windows 10 ou mais tarde.

#### <a name="prerequisites"></a>Pré-requisitos

Os dispositivos devem cumprir os seguintes pré-requisitos para suportar a rotação da chave de recuperação BitLocker:

- Os dispositivos devem executar a versão 1909 do Windows 10 ou mais tarde

- Os dispositivos azure ad-joined e híbrido-join-join devem ter suporte para a rotação da chave ativada:

  - **Rotação da palavra-passe de recuperação orientada pelo cliente**

  Esta definição encontra-se sob *encriptação do Windows* como parte de uma política de configuração do dispositivo para a Proteção de Pontofinal do Windows 10.

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Para rodar a chave de recuperação BitLocker

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos**  >  **Todos os dispositivos**.

3. Na lista de dispositivos que gere, selecione um dispositivo, selecione **Mais,** e, em seguida, selecione a ação remota do dispositivo de rotação da **tecla BitLocker.**

4. Na página **'Visão Geral** do dispositivo', selecione a rotação da **tecla BitLocker**. Se não vir esta opção, selecione a elipse (**...**) para mostrar opções adicionais e, em seguida, selecione a ação remota do dispositivo de rotação da **tecla BitLocker.**

   ![Selecione a elipse para ver mais opções](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Passos seguintes

[Manage FileVault policy (Gerir a política FileVault)](../protect/encrypt-devices-filevault.md)

[Monitorizar encriptação de discos](../protect/encryption-monitor.md)
