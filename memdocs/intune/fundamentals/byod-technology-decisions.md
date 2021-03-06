---
title: Decisões tecnológicas para BYOD com o EMS
description: As decisões tecnológicas chave para ativar o BYOD e proteger dados empresariais com o Microsoft Enterprise Mobility + Security.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 12/8/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 297926f6-c029-4003-bda4-9ee031d47dda
ms.reviewer: pfetty
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5d0e809e834a82f192128263742bc2b9b0024a2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079285"
---
# <a name="technology-decisions-for-enabling-byod-with-microsoft-enterprise-mobility--security-ems"></a>Decisões tecnológicas para ativar o BYOD com o Microsoft Enterprise Mobility + Security

Ao desenvolver a sua estratégia para permitir que os funcionários trabalhem remotamente a partir dos respetivos dispositivos (BYOD), precisará de tomar decisões chave nos cenários de ativação do BYOD e proteção os seus dados empresariais. Felizmente, o EMS oferece todas as funcionalidades necessárias num conjunto completo de soluções.  

Neste tópico, examinamos o caso simples de utilização da permissão de acesso BYOD ao e-mail empresarial. Vamos focar-nos em saber se precisa ou não de gerir todo o dispositivo ou apenas das aplicações, ambas são escolhas completamente válidas.

## <a name="assumptions"></a>Pressupostos
* Tem conhecimentos básicos sobre o Azure Active Directory e o Microsoft Intune
* As suas contas de e-mail estão alojadas no Exchange Online

## <a name="common-reasons-to-manage-the-device-mdm"></a>Motivos mais comuns para gerir o dispositivo (MDM)
Pode facilmente levar os utilizadores a inscreverem os seus dispositivos na gestão de dispositivos, implementando uma política de [Acesso Condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) no Exchange Online. Eis os motivos pelos quais poderá querer gerir dispositivos pessoais:

**Wi-Fi/VPN**: se os seus utilizadores precisarem de um perfil de conectividade empresarial para serem produtivos, isto pode ser configurado sem problemas.

**Aplicações**: se os seus utilizadores precisarem de instalar um conjunto de aplicações nos respetivos dispositivos, isto pode ser feito sem problemas. Isto inclui aplicações que poderá precisar por motivos de segurança, como uma aplicação de Defesa Contra Ameaças para Dispositivos Móveis.

**Conformidade**: algumas organizações precisam de cumprir políticas de regulamentação ou outras políticas que necessitem de controlos de MDM específicos. Por exemplo, precisa da MDM para encriptar todo o dispositivo ou para criar um relatório de todas as aplicações do dispositivo.

## <a name="common-reasons-to-only-manage-the-apps-mam"></a>Motivos mais comuns para gerir apenas as aplicações (MAM)
A MAM sem a MDM é muito popular em organizações que suportam o BYOD. Pode levar os utilizadores a acederem a e-mails do Outlook Mobile (que suporta as proteções MAM) implementando uma política de acesso condicional no Exchange Online. Eis os motivos pelos quais poderá querer gerir apenas as aplicações em dispositivos pessoais:

**Experiência do utilizador**: a inscrição na MDM inclui muitos pedidos de avisos (implementados pela plataforma) que, muitas vezes, fazem com que o utilizador opte por não aceder ao e-mail no respetivo dispositivo pessoal. A MAM é muito menos alarmante para os utilizadores, uma vez que apenas recebem um pop-up uma vez para os informar de que as proteções da MAM estão implementadas.

**Conformidade**: algumas organizações precisam de cumprir políticas que exigem menos funcionalidades de gestão em dispositivos pessoais. Por exemplo, a MAM só consegue remover dados empresariais de aplicações, em oposição à MDM que consegue remover todos os dados de um dispositivo.

![Imagem a comparar a gestão de dispositivos e de aplicações em dispositivos móveis](./media/byod-technology-decisions/byod-app-device-mgmt.png)

Saiba mais sobre [os ciclos de vida da gestão de dispositivos e aplicações](device-lifecycle.md).

## <a name="mdm-vs-mam-capability-comparison"></a>Comparação entre as funcionalidades da MDM e da MAM
Como já referido, o Acesso Condicional pode levar um utilizador a inscrever o seu dispositivo ou a utilizar uma aplicação gerida como o Outlook Mobile. Muitas outras condições podem ser aplicadas em cada um dos casos, incluindo:

* Que utilizador está a tentar aceder
* Se a localização é de confiança ou não
* Nível de risco de início de sessão
* Plataforma de dispositivo

Ainda assim, muitas organizações têm frequentemente riscos específicos com os que se preocupam.  A tabela abaixo lista as preocupações mais comuns e as respostas da MDM e da MAM para essas preocupações.

| Preocupação   |   MDM  |   MAM  |
|------------|--------|--------|
|Acesso a dados não autorizado | Exigir a associação a grupos | Exigir a associação a grupos |
|Acesso a dados não autorizado | Exigir a inscrição de dispositivos | Exigir aplicação protegida |
|Acesso a dados não autorizado | Exigir localização específica | Exigir localização específica |
| | | |
|Conta de utilizador comprometida| Requerer MFA | Requerer MFA|
|Conta de utilizador comprometida | Bloquear utilizadores de alto risco | Bloquear utilizadores de alto risco |
|Conta de utilizador comprometida | PIN do dispositivo | PIN da aplicação |
| | | |
| Aplicação comprometida ou dispositivo comprometido | Exigir um dispositivo em conformidade | Verificação de jailbreak na iniciação da aplicação |
| Aplicação comprometida ou dispositivo comprometido | Encriptar os dados do dispositivo | Encriptar dados da aplicação |
| | | |
|Perda ou roubo do dispositivo | Remover todos os dados do dispositivo | Remover todos os dados da aplicação|
| | | |
| Dados guardados em localizações não protegidas ou partilhados acidentalmente | Restringir as cópias de segurança dos dados do dispositivo | Restringir as ações cortar/copiar/colar|
| Dados guardados em localizações não protegidas ou partilhados acidentalmente | Restringir a opção Guardar Como | Restringir a opção Guardar Como |
|Dados guardados em localizações não protegidas ou partilhados acidentalmente | Desativar a impressão | n/d|

## <a name="next-steps"></a>Passos seguintes
Agora é hora de decidir se vai ativar o BYOD na sua organização, focando-se na gestão de dispositivos, gestão de aplicações ou uma combinação dos dois. A escolha de implementação é sua, mas seja qual for a sua opção, pode ter sempre a certeza de que as funcionalidades de identidade e segurança do Azure AD estarão disponíveis.  

Utilize o [Guia de Planeamento](planning-guide.md) do Intune para mapear o seu próximo nível de planeamento.
