---
title: Políticas de conformidade de dispositivos no Microsoft Intune – Azure | Microsoft Docs
description: Inicie-se com as políticas de conformidade do dispositivo de utilização, visão geral dos níveis de estado e gravidade, utilizando o estado InGracePeriod, trabalhando com acesso condicional e dispositivos de manuseamento sem uma política atribuída.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 559d9a704f0b33e3fda3adf628626b56ff263de3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989718"
---
# <a name="set-rules-on-devices-to-allow-access-to-resources-in-your-organization-using-intune"></a>Definir regras em dispositivos para permitir o acesso a recursos na sua organização através do Intune

Muitas soluções de gestão de dispositivos móveis (MDM) ajudam a proteger os dados organizacionais ao exigir que os utilizadores e os dispositivos cumpram alguns requisitos. No Intune, esta funcionalidade é denominada “políticas de conformidade”. As políticas de conformidade definem as regras e as definições que os utilizadores e os dispositivos têm de cumprir para estarem em conformidade. Quando combinados com o Acesso Condicional, os administradores podem bloquear utilizadores e dispositivos que não cumpram as regras.

Por exemplo, um administrador do Intune pode exigir que:

- Os utilizadores finais utilizem uma palavra-passe para aceder aos dados organizacionais nos dispositivos móveis
- O dispositivo não estejam desbloqueados por jailbreak ou rooting
- Exista uma versão mínima ou máxima do sistema operativo no dispositivo
- O dispositivo se mantenha ou esteja abaixo de um nível de ameaça

Também pode utilizar esta funcionalidade para monitorizar o estado de conformidade dos dispositivos na sua organização.

> [!IMPORTANT]
> O Intune segue o agendamento de registo do dispositivo para todas as avaliações de conformidade no dispositivo. Os ciclos de atualização de políticas e perfis listam os [tempos estimados](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) de atualização.

<!---### Actions for noncompliance

You can specify what needs to happen when a device is determined as noncompliant. This can be a sequence of actions during a specific time.
When you specify these actions, Intune will automatically initiate them in the sequence you specify. See the following example of a sequence of
actions for a device that continues to be in the noncompliant status for
a week:

- When the device is first determined to be noncompliant, an email with noncompliant notification is sent to the user.

- 3 days after initial noncompliance state, a follow up reminder is sent to the user.

- 5 days after initial noncompliance state, a final reminder with a notification that access to company resources will be blocked on the device in 2 days if the compliance issues are not remediated is sent to the user.

- 7 days after initial noncompliance state, access to company resources is blocked. This requires that you have Conditional Access policy that specifies that access from noncompliant devices should    be blocked for services such as Exchange and SharePoint.

### Grace Period

This is the time between when a device is first determined as
noncompliant to when access to company resources on that device is blocked. This time allows for time that the user has to resolve
compliance issues on the device. You can also use this time to create your action sequences to send notifications to the user before their access is blocked.

Remember that you need to implement Conditional Access policies in addition to compliance policies in order for access to company resources to be blocked.--->

## <a name="device-compliance-policies-work-with-azure-ad"></a>As políticas de conformidade de dispositivos funcionam com o Microsoft Azure AD

Intune usa [acesso condicional](../protect/conditional-access.md) para ajudar a impor o cumprimento. O Acesso Condicional é uma tecnologia do Azure Active Directory (Azure AD).

Quando um dispositivo se inscreve no Intune, é iniciado o processo de registo do Microsoft Azure AD e a informação do dispositivo é atualizada no Microsoft Azure AD. Uma das principais informações do dispositivo é o estado de conformidade do dispositivo. Este estado de conformidade é utilizado pelas políticas de Acesso Condicional para bloquear ou permitir o acesso a e-mails e outros recursos da organização.

Saiba mais sobre acesso condicional e Insintonização:

- [Formas comuns de usar o Acesso Condicional com Intune](conditional-access-intune-common-ways-use.md)

Conheça o Acesso Condicional na documentação da AD Azure:
  - [O que é acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
  - [O que é uma identidade de dispositivo](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

## <a name="ways-to-use-device-compliance-policies"></a>Formas de utilizar as políticas de conformidade de dispositivos

### <a name="with-conditional-access"></a>Com Acesso Condicional

Para dispositivos que cumpram as regras políticas, pode dar a esses dispositivos acesso a e-mails e outros recursos da organização. Se os dispositivos não cumprirem as regras políticas, então não têm acesso aos recursos da organização. Isto é acesso condicional.

### <a name="without-conditional-access"></a>Sem acesso condicional

Também pode utilizar as políticas de conformidade do dispositivo sem qualquer Acesso Condicional. Quando utilizar políticas de conformidade de forma independente, os dispositivos visados são avaliados e reportados com o respetivo estado de conformidade. Por exemplo, pode obter um relatório sobre o número de dispositivos que não estão encriptados ou quais os dispositivos que foram desbloqueados por jailbreak ou rooting. Quando utiliza políticas de conformidade sem acesso condicional, não existem restrições de acesso aos recursos da organização.

## <a name="ways-to-deploy-device-compliance-policies"></a>Formas de implementar as políticas de conformidade de dispositivos

Pode implementar a política de conformidade a utilizadores em grupos de utilizadores ou dispositivos em grupos de dispositivos. Quando uma política de conformidade é implementada num utilizador, todos os dispositivos do utilizador são verificados relativamente à conformidade. Utilizar grupos de dispositivos neste cenário ajuda com os relatórios de conformidade.

O Intune também inclui um conjunto de definições de políticas de conformidade incorporadas. As seguintes políticas incorporadas são avaliadas em todos os dispositivos inscritos no Intune:

- **Marque dispositivos sem uma política**de conformidade atribuída como : Esta é uma ação padrão para o incumprimento. esta propriedade tem dois valores:

  - **Conformidade** *(predefinição*): função de segurança desligada
  - **Não conforme:** funcionalidade de segurança em

  Se um dispositivo não tiver uma política de conformidade atribuída, então este dispositivo é considerado conforme por padrão. Se utilizar o Acesso Condicional com as políticas de conformidade, recomendamos que altere a definição predefinida para **Não conforme**. Se um utilizador final não estiver em conformidade porque não foi atribuída uma política, a [aplicação do Portal da Empresa](../apps/company-portal-app.md) mostrará `No compliance policies have been assigned`.

- **Deteção melhorada de jailbreak** (*Aplica-se ao iOS/iPadOS*): Quando ativada, esta definição faz com que o estado do dispositivo quebrado na cadeia ocorra com mais frequência nos dispositivos iOS/iPadOS. Esta definição apenas afeta dispositivos que são direcionados com uma política de conformidade que bloqueia dispositivos quebrados. Ativar esta propriedade utiliza os serviços de localização do dispositivo e pode afetar o uso da bateria. Os dados de localização do utilizador não são armazenados pela Intune e são usados apenas para desencadear a deteção de jailbreak com mais frequência em segundo plano. 

  Ativar esta definição exige que os dispositivos:
  - Ativem os serviços de localização ao nível do SO.
  - Permita sempre que o Portal da Empresa utilize serviços de localização.

  A deteção reforçada funciona através dos serviços de localização. A avaliação é desencadeada pela abertura da app Portal da Empresa ou movendo fisicamente o dispositivo a uma distância significativa de aproximadamente 500 metros ou mais. No iOS 13 e acima, esta funcionalidade requer que os utilizadores selecionem Sempre Permita sempre que o dispositivo os insto para continuar a permitir que o Portal da Empresa utilize a sua localização em segundo plano. Se os utilizadores nem sempre permitirem o acesso à localização e tiverem uma política com esta definição configurada, o seu dispositivo será marcado sem conformidade. Note que Intune não pode garantir que cada alteração significativa de localização garantirá uma verificação de deteção de jailbreak, uma vez que isso depende da ligação de rede de um dispositivo no momento.

- **Período de validade do estado de conformidade (dias)**: introduza o período de tempo durante o qual os dispositivos devem comunicar o estado para todas as políticas de conformidade recebidas. Os dispositivos que não devolvam o estado dentro deste período de tempo são tratados como não conformes. O valor predefinido é de 30 dias. O valor máximo é de 120 dias. O valor mínimo é 1 dia.

  Esta definição mostra como a política **de** conformidade por defeito ativo (Conformidade de Definição de**Monitor de Dispositivos**  >  **Monitor**  >  **Setting compliance**). A tarefa de fundo desta política funciona uma vez por dia.

Pode utilizar estas políticas incorporadas para monitorizar as definições. O Intune também [atualiza ou verifica a existência de atualizações](create-compliance-policy.md#refresh-cycle-times) com diferentes intervalos, consoante a plataforma do dispositivo. O artigo [Perguntas comuns, problemas e resoluções relativas aos perfis e políticas dos dispositivos no Microsoft Intune](../configuration/device-profile-troubleshoot.md) poder ser útil.

Os relatórios de conformidade são uma excelente forma de verificar o estado dos dispositivos. O artigo [Monitorizar as políticas de conformidade](compliance-policy-monitor.md) inclui algumas orientações.

## <a name="non-compliance-and-conditional-access-on-the-different-platforms"></a>Incumprimento e Acesso Condicional nas diferentes plataformas

O quadro seguinte descreve como as configurações não conformes são geridas quando uma política de conformidade é utilizada com uma política de acesso condicional.

---------------------------

|**Definição de políticas**| **Plataforma** |
| --- | ----|
| **Configuração do PIN ou da palavra-passe** | - **Android 4.0 e mais tarde**: Quarentena<br>- **Samsung Knox Standard 4.0 e mais tarde**: Quarentena<br>- **Android Enterprise**: Quarentena  <br>  <br>- **iOS 8.0 e mais tarde:** Remediado<br>- **macOS 10.11 e posteriormente:** Remediado  <br>  <br>- **Windows 8.1 e mais tarde**: Remediado<br>- **Windows Phone 8.1 e mais tarde**: Remediado|
| **Encriptação do dispositivo** | - **Android 4.0 e mais tarde**: Quarentena<br>- **Samsung Knox Standard 4.0 e mais tarde**: Quarentena<br>- **Android Enterprise**: Quarentena<br><br>- **iOS 8.0 e mais tarde:** Remediado (definindo PIN)<br>- **macOS 10.11 e posteriormente:** Remediado (por definição DE PIN)<br><br>- **Windows 8.1 e mais tarde**: Não aplicável<br>- **Windows Phone 8.1 e mais tarde**: Remediado |
| **Dispositivo desbloqueado por jailbreak ou obtenção de controlo de raiz** | - **Android 4.0 e mais tarde**: Quarentena (não um cenário)<br>- **Samsung Knox Standard 4.0 e mais tarde**: Quarentena (não um cenário)<br>- **Android Enterprise**: Quarentena (não um cenário)<br><br>- **iOS 8.0 e mais tarde:** Quarentena (não um ajuste)<br>- **macOS 10.11 e posteriormente**: Não aplicável<br><br>- **Windows 8.1 e mais tarde**: Não aplicável<br>- **Windows Phone 8.1 e mais tarde**: Não aplicável |
| **Perfil de e-mail** | - **Android 4.0 e mais tarde**: Não aplicável<br>- **Samsung Knox Standard 4.0 e mais tarde**: Não aplicável<br>- **Android Enterprise**: Não aplicável<br><br>- **iOS 8.0 e mais tarde:** Quarentena<br>- **macOS 10.11 e mais tarde:** Quarentena<br><br>- **Windows 8.1 e mais tarde**: Não aplicável<br>- **Windows Phone 8.1 e mais tarde**: Não aplicável |
| **Versão mínima do SO** | - **Android 4.0 e mais tarde**: Quarentena<br>- **Samsung Knox Standard 4.0 e mais tarde**: Quarentena<br>- **Android Enterprise**: Quarentena<br><br>- **iOS 8.0 e mais tarde:** Quarentena<br>- **macOS 10.11 e mais tarde:** Quarentena<br><br>- **Windows 8.1 e mais tarde**: Quarentena<br>- **Windows Phone 8.1 e mais tarde**: Quarentena |
| **Versão máxima do SO** | - **Android 4.0 e mais tarde**: Quarentena<br>- **Samsung Knox Standard 4.0 e mais tarde**: Quarentena<br>- **Android Enterprise**: Quarentena<br><br>- **iOS 8.0 e mais tarde:** Quarentena<br>- **macOS 10.11 e mais tarde:** Quarentena<br><br>- **Windows 8.1 e mais tarde**: Quarentena<br>- **Windows Phone 8.1 e mais tarde**: Quarentena |
| **Atestado do estado de funcionamento do Windows** | - **Android 4.0 e mais tarde**: Não aplicável<br>- **Samsung Knox Standard 4.0 e mais tarde**: Não aplicável<br>- **Android Enterprise**: Não aplicável<br><br>- **iOS 8.0 e mais tarde**: Não aplicável<br>- **macOS 10.11 e posteriormente**: Não aplicável<br><br>- **Windows 10 e Windows 10 Mobile**: Quarentena<br>- **Windows 8.1 e mais tarde**: Quarentena<br>- **Windows Phone 8.1 e mais tarde**: Não aplicável |

---------------------------

**Remediado**: O sistema operativo do dispositivo impõe a conformidade. Por exemplo, forçar o utilizador a definir um PIN.

**Quarentena**: O sistema operativo do dispositivo não impõe a conformidade. Por exemplo, os dispositivos Android e Android Enterprise não forçam o utilizador a encriptar o dispositivo. Quando o dispositivo não é conforme, são realizadas as seguintes ações:

- Se uma política de acesso condicional se aplicar ao utilizador, o dispositivo está bloqueado.
- A aplicação do Portal da Empresa notifica o utilizador sobre eventuais problemas de conformidade.

## <a name="next-steps"></a>Passos seguintes

- [Criar uma política](create-compliance-policy.md) e ver os pré-requisitos.
- Ver as definições de conformidade para as diferentes plataformas de dispositivos:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 e posterior](compliance-policy-create-windows-8-1.md)
  - [Windows 10 e posterior](compliance-policy-create-windows.md)

- [Referência das entidades de políticas](../developer/reports-ref-policy.md) tem informações sobre as entidades das políticas do Data Warehouse do Intune.
