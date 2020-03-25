---
title: O que é Microsoft Intune - Azure  Microsoft Docs
description: Saiba como a Microsoft Intune é a componente de gestão de dispositivos móveis (MDM) e gestão de aplicações móveis (MAM) da solução Enterprise Mobility + Security e como ajuda a proteger os dados da empresa.
keywords: o que é o Intune
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 10/14/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b4e778d-ac13-4c23-974f-5122f74626bc
ms.reviewer: pmay
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8fce5e8d7a92922d6061c33655bc4e83b3a1a95
ms.sourcegitcommit: 670c90a2e2d3106048f53580af76cabf40fd9197
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233483"
---
# <a name="microsoft-intune-is-an-mdm-and-mam-provider-for-your-devices"></a>Microsoft Intune é um fornecedor de MDM e MAM para os seus dispositivos

O Microsoft Intune é um serviço baseado na nuvem que se foca na gestão de dispositivos móveis (MDM) e na gestão de aplicações móveis (MAM). Intune está incluído no [suite Enterprise Mobility + Security (EMS)](https://www.microsoft.com/microsoft-365/enterprise-mobility-security)da Microsoft, e permite que os utilizadores sejam produtivos, mantendo os dados da sua organização protegidos. Integra-se com outros serviços, incluindo o Microsoft 365 e o Azure Ative Directory (Azure AD) para controlar quem tem acesso e aquilo a que têm acesso, e a Proteção de Informação Azure para proteção de dados. Quando o utiliza com o Microsoft 365, pode permitir que a sua força de trabalho seja produtiva em todos os seus dispositivos, mantendo as informações da sua organização protegidas.

![Imagem da arquitetura do Intune](./media/what-is-intune/intunearch_sm.png)

Veja uma [versão maior](./media/what-is-intune/intunearchitecture.svg) do diagrama da arquitetura do Intune.

Com o Intune, pode:

- Opte por ser 100% nuvem com Intune, ou ser [cogerido](https://docs.microsoft.com/configmgr/comanage/overview) com O Gestor de Configuração e Intune.
- Detete regras e configure as definições em dispositivos pessoais e de propriedade da organização para aceder a dados e redes.
- Implementar e autenticar aplicações em dispositivos -- no local e no telemóvel.
- Proteja as informações da sua empresa controlando a forma como os utilizadores acedem e partilham informações.
- Certifique-se de que os dispositivos e aplicações estão em conformidade com os seus requisitos de segurança.

## <a name="manage-devices"></a>Gerir dispositivos

Em Intune, gere-se dispositivos usando uma abordagem que é a certa para si. Para dispositivos pertencentes à organização, pode querer o controlo total dos dispositivos, incluindo configurações, funcionalidades e segurança. Nesta abordagem, os dispositivos e utilizadores destes dispositivos "matriculam-se" no Intune. Uma vez matriculados, recebem as suas regras e configurações através de políticas configuradas no Intune. Por exemplo, pode definir os requisitos de palavra-passe e PIN, criar uma ligação VPN, configurar a proteção contra ameaças e muito mais.

Para dispositivos pessoais ou dispositivos de bring-your-your-own (BYOD), os utilizadores podem não querer que os seus administradores de organização tenham controlo total. Nesta abordagem, dê aos utilizadores opções. Por exemplo, os utilizadores [matriculam](../enrollment/device-enrollment.md) os seus dispositivos se quiserem ter acesso total aos recursos da sua organização. Ou, se estes utilizadores apenas querem ter acesso a e-mails ou Equipas Microsoft, então utilize políticas de proteção de aplicações que exijam a autenticação de vários fatores (MFA) para usar estas aplicações.

Quando os dispositivos são matriculados e geridos em Intune, os administradores podem:

- Consulte os dispositivos matriculados e obtenha um inventário de dispositivos que acedam aos recursos da organização.
- Configure os dispositivos para que cumpram os seus padrões de segurança e saúde. Por exemplo, provavelmente queres bloquear dispositivos de prisão.
- Empurre os certificados para dispositivos para que os utilizadores possam aceder facilmente à sua rede Wi-Fi ou utilizar uma VPN para se ligar à sua rede.
- Consulte relatórios sobre utilizadores e dispositivos que sejam conformes e não conformes.
- Remova os dados da organização se um dispositivo estiver perdido, roubado ou não utilizado mais.

**Recursos online:**

- [O que é a inscrição de dispositivos?](../enrollment/device-enrollment.md)

- [Aplique funcionalidades e definições nos seus dispositivos utilizando perfis de dispositivos](../configuration/device-profiles.md)

- [Proteja os dispositivos com a Microsoft Intune](../protect/device-protect.md)

## <a name="manage-apps"></a>Gerir aplicações

A gestão de aplicações móveis (MAM) em Intune foi concebida para proteger os dados da organização ao nível da aplicação, incluindo aplicações personalizadas e aplicações de loja. A gestão de aplicações pode ser usada em dispositivos de propriedade organizacional e dispositivos pessoais.

Quando as aplicações são geridas em Intune, os administradores podem:

- Adicione e atribua aplicações móveis a grupos e dispositivos de utilizadores, incluindo utilizadores em grupos específicos, dispositivos em grupos específicos e muito mais.
- Configure as aplicações para iniciar ou executar com configurações específicas ativadas e atualizar as aplicações já existentes no dispositivo.
- Consulte os relatórios sobre quais as aplicações utilizadas e rastreie o seu uso.
- Faça uma limpeza seletiva removendo apenas dados da organização de aplicações.

Uma das formas que o Intune fornece a segurança das aplicações móveis é através de políticas de **[proteção de aplicações.](../apps/app-protection-policy.md)** Políticas de proteção de aplicações:

- Utilize a identidade Azure AD para isolar os dados da organização a partir de dados pessoais. Assim, as informações pessoais estão isoladas da consciência organizacional das TI. Os dados acedidos usando credenciais da organização recebem proteção adicional de segurança.
- Ajude a garantir o acesso aos dispositivos pessoais, restringindo as ações que os utilizadores podem tomar, tais como cópia e pasta, economize e vista.
- Pode ser criado e implantado em dispositivos matriculados em Intune, matriculados noutro serviço de MDM, ou não matriculados em qualquer serviço de MDM. Em dispositivos matriculados, as políticas de proteção de aplicações podem adicionar uma camada extra de proteção.

Por exemplo, um utilizador insere-se num dispositivo com as suas credenciais de organização. A sua identidade de organização permite o acesso a dados que são negados à sua identidade pessoal. À medida que os dados da organização são utilizados, as políticas de proteção de aplicações controlam a forma como os dados são guardados e partilhados. Quando os utilizadores assinam com a sua identidade pessoal, essas mesmas proteções não são aplicadas. Desta forma, a TI tem o controlo dos dados da organização, enquanto os utilizadores finais mantêm o controlo e privacidade sobre os seus dados pessoais.

E pode usar intune com os outros serviços em EMS. Esta funcionalidade fornece a segurança da sua organização para aplicações móveis para além do que está incluído no sistema operativo e em quaisquer aplicações. As aplicações geridas com o EMS têm acesso a um conjunto mais alargado de funcionalidades de aplicação móvel e proteção de dados.

![Imagem que mostra os níveis da segurança de dados de gestão de aplicações](./media/what-is-intune/managing-mobile-apps.png)

## <a name="compliance-and-conditional-access"></a>Conformidade e acesso condicional

O Intune está integrado no Azure AD para possibilitar um conjunto abrangente de cenários de controlo de acesso. Por exemplo, exigir que os dispositivos móveis sejam compatíveis com os padrões de organização definidos em Intune antes de aceder aos recursos da rede, como e-mail ou SharePoint. Da mesma forma, você pode bloquear serviços para que eles só estejam disponíveis para um conjunto específico de aplicações móveis. Por exemplo, pode bloquear o Exchange Online para que só seja acedido pelo Outlook ou pelo Outlook Mobile.

**Recursos online:**

- [Desestabeleça regras sobre dispositivos que permitam o acesso aos recursos da sua organização](../protect/device-compliance-get-started.md)

- [Formas comuns de usar o Acesso Condicional com Intune](../protect/conditional-access-intune-common-ways-use.md)

## <a name="how-to-get-intune"></a>Como ficar insinado

Intune está disponível:

- Como um [serviço Azure](https://go.microsoft.com/fwlink/?linkid=2090973) autónomo
- Incluído com [microsoft 365](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/microsoft-intune) e [microsoft 365 governo](https://www.microsoft.com/microsoft-365/government)
- Como Gestão de [Dispositivos Móveis no Office 365,](https://support.office.com/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd)que consiste em algumas características limitadas intune

Intune é usado em muitos setores, incluindo [governo](https://docs.microsoft.com/enterprise-mobility-security/solutions/ems-govt-service-description), [educação,](https://www.microsoft.com/en-us/education/intune) [quiosque ou dispositivo dedicado](../configuration/kiosk-settings.md) para fabricação e retalho, e muito mais.

## <a name="next-steps"></a>Próximos passos

- Leia alguns dos [problemas comerciais comuns que Intune ajuda a resolver.](common-scenarios.md)
- Comece com um [julgamento de 30 dias de Intune.](free-trial-sign-up.md)
- Planeie a sua [migração para Intune.](migration-guide.md)
- Utilizando o seu teste ou subscrição gratuitos, passe pelo [Quickstart: Crie um perfil de dispositivo de e-mail para iOS](../configuration/quickstart-email-profile.md).
