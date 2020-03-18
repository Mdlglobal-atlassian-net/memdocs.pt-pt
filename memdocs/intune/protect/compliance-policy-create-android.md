---
title: Definições de conformidade de dispositivos Android no Microsoft Intune – Azure | Microsoft Docs
description: Veja uma lista de todas as definições que pode utilizar quando define a conformidade para os dispositivos Android no Microsoft Intune. Defina regras de palavra-passe, escolha uma versão mínima ou máxima do sistema operativo, restrinja aplicações específicas, impeça a reutilização de palavras-passe e muito mais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58369ee2130ac296c9768812cf51b3fcbfed0d95
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329709"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Definições do Android para marcar dispositivos como conformes ou não conformes com o Intune

Este artigo apresenta e descreve as definições de conformidade diferentes que pode configurar em dispositivos Android no Intune. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para marcar os dispositivos desbloqueados por rooting (jailbreak) como não conformes, defina um nível de ameaça permitido, ative o Google Play Protect e muito mais.

Esta funcionalidade aplica-se a:

- Administrador de dispositivos Android

Enquanto administrador do Intune, utilize estas definições de conformidade para ajudar a proteger os recursos da sua organização. Para saber mais sobre as políticas de conformidade e para o que servem, veja a [introdução à conformidade de dispositivos](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Antes de começar

[Criar uma política de conformidade](create-compliance-policy.md#create-the-policy). Para **platform**, selecione **administrador de dispositivos Android**.

## <a name="device-health"></a>Estado de Funcionamento do Dispositivo

- **Dispositivos desbloqueados por rooting**:

  - **Não configurado** *(predefinido)* - esta definição não é avaliada para conformidade ou incumprimento.
  - **Bloco** - Mark dispositivos enraizados (jailbroken) como não conformes.

- **Exigir que o dispositivo esteja ao nível ou abaixo do Nível de Ameaça de Dispositivos**:

  Utilize esta definição para fazer a avaliação de risco de um serviço de defesa de ameaças móveis conectado como condição para o cumprimento.
  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento. 
  - **Secured** - Esta opção é a mais segura, uma vez que o dispositivo não pode ter ameaças. Se forem detetadas ameaças de qualquer nível no dispositivo, o mesmo será avaliado como não conforme.
  - **Baixo** - O dispositivo é avaliado como conforme se apenas houver ameaças de baixo nível. Qualquer nível mais alto coloca o dispositivo num estado de não conforme.
  - **Médio** - O dispositivo é avaliado como conforme se as ameaças existentes no dispositivo forem de baixo ou médio nível. Se forem detetadas ameaças de nível alto no dispositivo, este será determinado como não conforme.
  - **Alta** - Esta opção é a menos segura, e permite todos os níveis de ameaça. Poderá ser útil se utilizar esta solução apenas para fins de relatórios.

### <a name="google-play-protect"></a>Google Play Protect

- **Google Play Services configurado**:

  Os serviços do Google Play permitem realizar atualizações de segurança, que são uma dependência de nível base de várias funcionalidades de segurança dos dispositivos Google certificados.

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.  
  - **Require** - Require that the Google Play services app is installand and enabled.  

- **Fornecedor de segurança atualizado**:

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Require** - Exigir que um fornecedor de segurança atualizado possa proteger um dispositivo de vulnerabilidades conhecidas.

- **Análise de ameaças nas aplicações**:

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Require** - Require that the Android **Check Apps feature** is enabled.

  > [!NOTE]
  > Na plataforma Android legada, esta funcionalidade é uma definição de conformidade. O Intune só consegue verificar se esta definição está ativada ao nível do dispositivo.

- **Atestado do dispositivo SafetyNet**:

  introduza o nível do [Atestado SafetyNet](https://developer.android.com/training/safetynet/attestation.html) que tem de ser cumprido. As opções são:

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Verificação de integridade básica**
  - **Verificação de integridade básica e de dispositivos certificados**

> [!NOTE]
> Para configurar definições do Google Play Protect através de políticas de proteção de aplicações, veja [Definições de políticas de proteção de aplicações do Intune](../apps/app-protection-policy-settings-android.md#conditional-launch) no Android.

## <a name="device-properties"></a>Device Properties

### <a name="operating-system-version"></a>Versão do Sistema Operativo 

- **Versão mínima do SO**:

  quando um dispositivo não cumpre o requisito de versão mínima do SO, será reportado como não conforme. É apresentada uma ligação com informações sobre como atualizar. O utilizador final pode optar por atualizar o dispositivo e, em seguida, obter acesso aos recursos da empresa.

  *Por defeito, nenhuma versão está configurada.*

- **Versão máxima do SO**:

  quando um dispositivo utiliza uma versão do SO posterior à versão especificada na regra, o acesso aos recursos da empresa é bloqueado. É solicitado ao utilizador que contacte o seu administrador de TI. Até que uma regra seja alterada para permitir a versão S, este dispositivo não pode aceder aos recursos da empresa.

  *Por defeito, nenhuma versão está configurada.*

## <a name="system-security"></a>System Security

### <a name="password"></a>Palavra-passe

<!-- Removed
- **Minimum password length**: Enter the minimum number of digits or characters that the user's password must have.   


- **Maximum minutes of inactivity before password is required**: Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

- **Password expiration (days)**: Select the number of days before the password expires and the user must create a new password.

- **Number of previous passwords to prevent reuse**: Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.

-->

- **Exigir uma palavra-passe para desbloquear os dispositivos móveis**:

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Exigir** - Os utilizadores devem introduzir uma palavra-passe antes de poderem aceder ao seu dispositivo.

- **Tipo obrigatório de palavra-passe**:

  escolha se uma palavra-passe deve incluir apenas carateres numéricos ou uma combinação de números e de outros carateres. As opções são:

  - **Predefinição do dispositivo** - Para avaliar a conformidade com a palavra-passe, certifique-se de selecionar uma força de senha diferente da **predefinição do Dispositivo**.
  - **Biométrica de segurança baixa**
  - **Pelo menos numérica**
  - **Complexo numérico** - Algarismos repetidos ou consecutivos, como `1111` ou `1234`, não são permitidos.
  - **Pelo menos alfabética**
  - **Pelo menos alfanumérica**
  - **Pelo menos alfanumérica com símbolos**

### <a name="encryption"></a>Encriptação

- **Encriptação do armazenamento de dados num dispositivo**:  
  *Suportado no Android 4.0 e mais tarde, ou KNOX 4.0 e mais tarde.*

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Require** - Criptografe o armazenamento de dados nos seus dispositivos. Os dispositivos são encriptados quando seleciona a definição **Palavra-passe obrigatória para desbloquear os dispositivos móveis**.

### <a name="device-security"></a>Segurança do Dispositivo

- **Bloquear aplicações de origens desconhecidas**:

  - **Não configurado** *(predefinido)* - esta definição não é avaliada para conformidade ou incumprimento.
  - **Block** - Bloqueie dispositivos com **Segurança > Fontes Desconhecidas** ativadas por fontes (*suportadas no Android 4.0 através do Android 7.x. Não suportado no Android 8.0 e mais tarde.*

  Para aplicações de sideload, as origens desconhecidas têm de ser permitidas. Se não tiver aplicações Android de sideload, defina esta funcionalidade como **Bloquear** para ativar esta política de conformidade.

  > [!IMPORTANT]
  > As aplicações de sideload requerem a ativação da definição **Bloquear aplicações de origens desconhecidas**. Aplique esta política de conformidade apenas se não tiver aplicações Android de sideload nos dispositivos.

- **Integridade de tempo de execução de aplicações do portal da empresa**:

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Exigir** - Escolha *Exigir* confirmar que a aplicação Portal da Empresa satisfaz todos os seguintes requisitos:

    - Tem o ambiente de tempo de execução predefinido instalado
    - Está corretamente assinada
    - Não está no modo de depuração
    - Foi instalada a partir de uma origem conhecida

- **Bloqueie a depuração USB no dispositivo** *(Android 4.2 ou posterior)* :

  - **Não configurado** *(predefinido)* - Esta definição não é avaliada para conformidade ou incumprimento.
  - **Bloquear** - Evitar que os dispositivos utilizem a função de depuração USB.

- **Nível mínimo de patch** de segurança *(Android 6.0 ou mais tarde)*

  selecione o nível de correção de segurança mais antigo que um dispositivo pode ter. Os dispositivos que não tiverem pelo menos este nível de correção serão considerados como não conformes. A data tem de ser introduzida no formato `YYYY-MM-DD`.

  *Por predefinição, nenhuma data está configurada.*

- **Aplicações restritas**:

  Introduza o nome da **App** e o **pacote de identificação** de aplicativos para aplicações que devem ser restritas e, em seguida, selecione **Adicionar**. Um dispositivo com pelo menos uma aplicação restrita instalada é marcado como não conforme.

## <a name="next-steps"></a>Próximos passos

- [Adicionar ações para dispositivos não conformes](actions-for-noncompliance.md) e [utilizar etiquetas de âmbito para filtrar políticas](../fundamentals/scope-tags.md).
- [Monitorizar as políticas de conformidade](compliance-policy-monitor.md).
- Veja as [definições de política de conformidade para dispositivos Android Enterprise](compliance-policy-create-android-for-work.md).
