---
title: Criptografe dispositivos macOS com encriptação de disco FileVault com Intune
titleSuffix: Microsoft Intune
description: Criptografe os dispositivos macOS com o método de encriptação incorporado FileVault e gerencie as chaves de recuperação para esses dispositivos encriptados a partir do portal Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 18a26bcf282b7b586c7cd0209b0381f31c44ac2f
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551749"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Utilize encriptação de disco FileVault para macOS com Intune

Intune suporta encriptação do disco macOS FileVault. FileVault é um programa de encriptação de discos inteiros que está incluído com macOS. Pode utilizar o Intune para configurar o FileVault em dispositivos que executam **o macOS 10.13 ou posteriormente**.

Utilize um dos seguintes tipos de políticas para configurar o FileVault nos seus dispositivos geridos:

- **[Política de segurança de endpoint para macOS FileVault](#create-an-endpoint-security-policy-for-filevault)**. O perfil fileVault na *segurança endpoint* é um grupo focado de configurações que é dedicado a configurar fileVault.

  Ver as definições do [FileVault que estão disponíveis nos perfis para](../protect/endpoint-security-disk-encryption-profile-settings.md)a política de encriptação do disco .

- **[Perfil de configuração do dispositivo para proteção de ponto final para o macOS FileVault](#create-an-endpoint-security-policy-for-filevault)**. As definições do FileVault são uma das categorias de definições disponíveis para a proteção do ponto final macOS. Para obter mais informações sobre a utilização de um perfil de configuração do dispositivo, consulte Criar um perfil de [dispositivo no Inunte](../configuration/device-profile-create.md).

  Consulte as [definições do FileVault que estão disponíveis nos perfis](../protect/endpoint-protection-macos.md#filevault)de proteção de pontofinal para a política de configuração do dispositivo .

Para gerir o BitLocker para o Windows 10, consulte a [política Manage BitLocker](../protect/encrypt-devices.md).

> [!TIP]
> [relatório de encriptação](encryption-monitor.md) que apresenta detalhes sobre o estado de encriptação dos dispositivos, em todos os seus dispositivos geridos.

Depois de criar uma política para encriptar dispositivos com FileVault, a política é aplicada aos dispositivos em duas fases. Em primeiro lugar, o dispositivo está preparado para permitir que a Intune recupere e volte a fazer o backup da chave de recuperação. Esta ação é referida como caução. Depois de a chave ser depositada, a encriptação do disco pode começar.

A inscrição do dispositivo aprovado pelo utilizador é necessária para que o FileVault funcione num dispositivo. O utilizador deve aprovar manualmente o perfil de gestão a partir das preferências do sistema para que a inscrição seja considerada aprovada pelo utilizador.

## <a name="permissions-to-manage-filevault"></a>Permissões para gerir fileVault

Para gerir o FileVault in Tune, a sua conta deve ter as permissões de controlo de acesso (RBAC) baseadas em [funções](../fundamentals/role-based-access-control.md) aplicáveis.

Seguem-se as permissões FileVault, que fazem parte da categoria de **tarefas Remotas,** e as funções RBAC incorporadas que concedem a permissão:

- **Obtenha a tecla FileVault:**
  - Operador de mesa de ajuda
  - Gestor de segurança endpoint

- **Chave Rotate FileVault**
  - Operador de mesa de ajuda

## <a name="create-and-deploy-policy"></a>Criar e implementar política

### <a name="create-an-endpoint-security-policy-for-filevault"></a>Criar uma política de segurança de ponto final para fileVault

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione a encriptação de **fim de segurança**Do  >  **disco**  >  **Criar política**.

3. Na página **Basics,** introduza as seguintes propriedades e, em seguida, escolha **A Seguinte**.
   1. **Plataforma**: macOS
   2. **Perfil**: FileVault

   ![Selecione o perfil FileVault](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. Na página de definições de **Configuração:**
   1. Definir *ativar o FileVault* para **Sim**.
   2. Para o tipo de *chave de recuperação,* apenas é suportada **a Chave de Recuperação Pessoal.**
   3. Configure configurar configurações adicionais para satisfazer os seus requisitos.

   Considere adicionar uma mensagem para ajudar a orientar os utilizadores sobre como recuperar a chave de recuperação do seu dispositivo. Estas informações podem ser úteis para os seus utilizadores quando utiliza a definição para a rotação da chave de recuperação pessoal, que pode gerar automaticamente uma nova chave de recuperação para um dispositivo periodicamente.

   Por exemplo: Para recuperar uma chave de recuperação perdida ou recentemente rotativa, inscreva-se no site do Portal da Empresa Intune a partir de qualquer dispositivo. No portal, vá a Dispositivos e selecione o dispositivo que tem o FileVault ativado e, em seguida, selecione a *chave de recuperação Get*. A chave de recuperação atual é apresentada.

5. Quando terminar as definições de configuração, selecione **Next**.

6. Na página **Scope (Tags),** escolha **Selecione etiquetas** de âmbito para abrir o painel de etiquetas Select para atribuir etiquetas de âmbito ao perfil.

   Selecione **Seguinte** para continuar.

7. Na página **de Atribuiçãos,** selecione os grupos que receberão este perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de utilizador e dispositivo de atribuição.
Selecione **Seguinte**.

8. Na página **Review + criar** página, quando terminar, escolha **Criar**. O novo perfil é apresentado na lista quando seleciona o tipo de política para o perfil que criou.

### <a name="create-a-device-configuration-policy-for-filevault"></a>Criar uma política de configuração do dispositivo para FileVault

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Definir as seguintes opções:
   1. **Plataforma**: macOS
   2. **Perfil**: Proteção de pontofinal

   ![Selecione o perfil FileVault](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Selecione **Definições**  >  **FileVault**.

   ![Definições de FileVault](./media/encrypt-devices-filevault/filevault-settings.png)

5. Para *fileVault,* **selecione Ativar**.

6. Para o tipo de *tecla de recuperação,* apenas a **chave pessoal** é suportada.

   Considere adicionar uma mensagem para ajudar a orientar os utilizadores sobre como recuperar a chave de recuperação do seu dispositivo. Estas informações podem ser úteis para os seus utilizadores quando utiliza a definição para a rotação da chave de recuperação pessoal, que pode gerar automaticamente uma nova chave de recuperação para um dispositivo periodicamente.

   Por exemplo: Para recuperar uma chave de recuperação perdida ou recentemente rotativa, inscreva-se no site do Portal da Empresa Intune a partir de qualquer dispositivo. No portal, vá a *Dispositivos* e selecione o dispositivo que tem o FileVault ativado e, em seguida, selecione a *chave de recuperação Get*. A chave de recuperação atual é apresentada.

7. Configure as definições restantes [do FileVault](endpoint-protection-macos.md#filevault) para satisfazer as necessidades do seu negócio e, em seguida, selecione **OK**.

8. Complete a configuração de configurações adicionais e, em seguida, guarde o perfil.

## <a name="manage-filevault"></a>Gerir fileVault

Para visualizar informações sobre dispositivos que recebem a política do FileVault, consulte a [encriptação](../protect/encryption-monitor.md)do disco Monitor .

Quando a Intune encripta pela primeira vez um dispositivo macOS com fileVault, é criada uma chave de recuperação pessoal. Após a encriptação, o dispositivo apresenta a chave pessoal uma única vez para o utilizador do dispositivo.

Para dispositivos geridos, o Intune pode esquendar uma cópia da chave de recuperação pessoal. O depósito de teclas permite que os administradores intune rodem as teclas para ajudar a proteger os dispositivos, e os utilizadores recuperem uma chave de recuperação pessoal perdida ou rotativa.

Depois de Intune encriptar um dispositivo macOS com FileVault:

- Os administradores podem visualizar e gerir as chaves de recuperação do FileVault utilizando o relatório de encriptação Intune.
- Os utilizadores podem visualizar a chave de recuperação pessoal de um dispositivo a partir do Portal da Empresa web no dispositivo. A partir do Portal da Empresa web, escolha o dispositivo macOS encriptado e, em seguida, opte por "Obter a chave de recuperação" como uma ação remota do dispositivo.

> [!IMPORTANT]
> Os dispositivos encriptados pelos utilizadores, e não pelo Intune, não podem ser geridos pela Intune. Isto significa que Intune não pode caucionar a recuperação pessoal destes dispositivos, nem gerir a rotação da chave de recuperação. Antes de a Intune poder gerir o FileVault e as chaves de recuperação do dispositivo, o utilizador deve desencriptar o dispositivo e, em seguida, deixar o Intune encriptar o dispositivo.

### <a name="retrieve-personal-recovery-key"></a>Recuperar a chave de recuperação pessoal

Para um dispositivo macOS que foi encriptado pela Intune, os utilizadores finais podem recuperar a sua chave de recuperação pessoal (chave FileVault) utilizando a aplicação portal da empresa iOS, a aplicação Portal da Empresa Android ou através da aplicação Android Intune.

O dispositivo que tenha a chave de recuperação pessoal deve ser matriculado com Intune e encriptado com fileVault através de Intune. Utilizando a aplicação portal da empresa iOS, a aplicação Portal da Empresa Android, a aplicação Android Intune ou o website Do Portal da Empresa, o utilizador pode ver a chave de recuperação **do FileVault** necessária para aceder aos seus dispositivos Mac.

Os utilizadores do dispositivo podem selecionar **dispositivos**  >  *o dispositivo macOS encriptado e inscrito*Obtenha a chave de  >  **recuperação**. O navegador mostrará o Portal da Empresa Web e exibirá a chave de recuperação.

### <a name="rotate-recovery-keys"></a>Teclas de recuperação rotativas

Intune suporta múltiplas opções para rodar e recuperar chaves de recuperação pessoal. Uma das razões para rodar uma chave é se a chave pessoal atual estiver perdida ou se pensa estar em risco.

- **Rotação automática**: Como administrador, pode configurar a rotação da chave de recuperação pessoal do FileVault para gerar automaticamente a nova chave de recuperação periodicamente. Quando uma nova tecla é gerada para um dispositivo, a chave não é apresentada ao utilizador. Em vez disso, o utilizador deve obter a chave quer a partir de um administrador, quer através da aplicação portal da empresa.

- **Rotação manual**: Como administrador, pode visualizar informações para um dispositivo que gere com o Intune e que está encriptado com fileVault. Em seguida, pode optar por rodar manualmente a chave de recuperação para dispositivos corporativos. Não se pode rodar as chaves de recuperação para dispositivos pessoais.

  Para rodar uma chave de recuperação:

  1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Selecione **Dispositivos**   >  **Todos os dispositivos**.

  3. A partir da lista de dispositivos, selecione o dispositivo encriptado e para o qual pretende rodar a sua chave. Em seguida, sob o Monitor, selecione **Teclas de recuperação**.
  
  4. No painel das teclas recovery, **selecione Rotação fileVault chave**de recuperação .

     Da próxima vez que o dispositivo fizer o check-in com Intune, a chave pessoal é girada. Quando necessário, a nova chave pode ser obtida pelo utilizador através do portal da empresa.

### <a name="recover-recovery-keys"></a>Recuperar chaves de recuperação

- **Administrador**: Os administradores não podem ver chaves de recuperação pessoais para dispositivos encriptados com FileVault.

- **Utilizador final**: Os utilizadores finais utilizam o website do Portal da Empresa a partir de qualquer dispositivo para visualizar a chave de recuperação pessoal atual para qualquer um dos seus dispositivos geridos. Não é possível ver chaves de recuperação da aplicação Portal da Empresa.

  Para ver uma chave de recuperação:
  
  1. Inscreva-se no site do *Intune Company Portal* a partir de qualquer dispositivo.

  2. No portal, vá a **Dispositivos** e selecione o dispositivo macOS que está encriptado com fileVault.

  3. Selecione **Obter tecla de recuperação**. A chave de recuperação atual é apresentada.

## <a name="next-steps"></a>Próximos passos

[Gerir a política BitLocker](../protect/encrypt-devices.md)

[Monitorizar encriptação de discos](../protect/encryption-monitor.md)
