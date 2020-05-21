---
title: Gerir a segurança do ponto final no Microsoft Intune / Microsoft Docs
description: Saiba como os Administradores de Segurança podem usar o nó de Segurança Endpoint para gerir a segurança do dispositivo e remediar problemas para dispositivos no Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d721ffadc5d4fdee5248b9fdfd256623ccc7d77f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431379"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Gerir a segurança do ponto final no Microsoft Intune

Como Administrador de Segurança, utilize o nó de *segurança Endpoint* em Intune para configurar a segurança do dispositivo e gerir tarefas de segurança para dispositivos quando esses dispositivos estiverem em risco. As políticas de segurança endpoint são projetadas para ajudá-lo a focar-se na segurança dos seus dispositivos e mitigar o risco. As tarefas disponíveis ajudam-no a identificar dispositivos que estão em risco, a remediar esses dispositivos e a restaurá-los para um estado compatível ou mais seguro.

O nó de segurança Endpoint agrupa as ferramentas disponíveis através do Intune que utilizará para manter os dispositivos seguros:

- **Reveja o estado de todos os seus dispositivos geridos**. Utilize a visão [de Todos os dispositivos](#manage-devices) onde pode visualizar a conformidade do dispositivo a partir de um nível elevado e, em seguida, perfurar em dispositivos específicos para entender quais as políticas de conformidade não são cumpridas para que possa resolvê-los.

- **Implemente linhas de segurança que estabeleçam configurações de segurança de boas práticas para dispositivos**. Intune inclui [linhas de base](#manage-security-baselines) de segurança para dispositivos Windows e uma lista crescente de aplicações, como o Microsoft Defender Advanced Threat Protection (Defender ATP) e o Microsoft Edge. As linhas de base de segurança são grupos pré-configurados de definições do Windows que o ajudam a aplicar um grupo conhecido de definições e valores predefinidos que as equipas de segurança relevantes recomendam.

- **Gerencie as configurações**de segurança nos dispositivos através de políticas bem focadas .  Cada política de [segurança endpoint](#use-policies-to-manage-device-security) centra-se em aspetos de segurança do dispositivo como antivírus, encriptação de discos, firewalls e várias áreas disponibilizadas através da integração com o Defender ATP.

- **Estabelecer os requisitos**do dispositivo e do utilizador através da política de conformidade . Com as políticas de [conformidade,](../protect/device-compliance-get-started.md)define as regras que os dispositivos e os utilizadores devem cumprir para serem consideradas conformes. As regras podem incluir versões DE, requisitos de palavra-passe, níveis de ameaça de dispositivo, e muito mais.

  Quando se integra com as políticas de [acesso condicional](#configure-conditional-access) do Azure Ative Directory (Azure AD) para impor as políticas de conformidade, pode aceder ao acesso a recursos corporativos tanto para dispositivos geridos como para dispositivos que ainda não são geridos.

- **Integre o Intune com a sua equipa ATP Microsoft Defender**. Ao [integrar-se com o Defender ATP,](#set-up-integration-with-defender-atp) tem acesso a tarefas de [segurança.](#review-security-tasks-from-defender-atp) As tarefas de segurança ligam de perto o Defender ATP e o Intune para ajudar a sua equipa de segurança a identificar dispositivos que estão em risco e a entregar medidas detalhadas de reparação aos administradores intune que podem então agir.

As seguintes secções deste artigo discutem as diferentes tarefas que pode fazer a partir do nó de segurança de ponto final do centro de administração, e as permissões de controlo de acesso baseadas em papéis (RBAC) que são necessárias para usá-las.

## <a name="manage-devices"></a>Gerir dispositivos

O nó de segurança Endpoint inclui a vista *De todos os dispositivos,* onde pode ver uma lista de todos os dispositivos do seu Anúncio Azure que estão disponíveis no Microsoft Endpoint Manager.

A partir desta perspetiva, pode selecionar dispositivos para perfurar para obter mais informações, como as políticas com que um dispositivo não está em conformidade. Também pode utilizar o acesso a partir desta vista para remediar problemas para um dispositivo, incluindo, reiniciar um dispositivo, iniciar uma varredura para malware ou rodar as teclas BitLocker num dispositivo Windows 10.

Para mais informações, consulte [Gerir dispositivos com segurança de ponto final no Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Gerir as linhas de base de segurança

As linhas de base de segurança em Intune são grupos pré-configurados de configurações que são recomendações de boas práticas das equipas de segurança relevantes da Microsoft para o produto. Intune suporta linhas de segurança para configurações de dispositivos Windows 10, Microsoft Edge, Microsoft Defender Advanced Threat Protection, e muito mais.

Pode utilizar linhas de base de segurança para implementar rapidamente uma *configuração* de melhor prática do dispositivo e das definições de aplicação para proteger os seus utilizadores e dispositivos. As linhas de base de segurança são suportadas para dispositivos que executam a versão 1809 do Windows 10 e mais tarde.

Para mais informações, consulte Utilize as linhas de [segurança para configurar os dispositivos do Windows 10 no Intune](../protect/security-baselines.md).

As linhas de base de segurança são um dos vários métodos em Intune para configurar as definições nos dispositivos. Ao gerir as definições, é importante entender que outros métodos estão a ser utilizados no seu ambiente que podem configurar os seus dispositivos para evitar conflitos. Ver [Evitar conflitos políticos](#avoid-policy-conflicts) mais tarde neste artigo.

## <a name="review-security-tasks-from-defender-atp"></a>Rever as tarefas de segurança do Defender ATP

Quando integrar o Intune com o Microsoft Defender Advanced Threat Protection (Defender ATP), pode rever *as tarefas* de Segurança em Intune que identificam dispositivos de risco e fornecem medidas para mitigar esse risco. Em seguida, pode utilizar as tarefas para informar o Defender ATP quando esses riscos forem atenuados com sucesso.

- A sua equipa ATP desativa quais os dispositivos em risco e passa essa informação para a sua equipa Intune como uma tarefa de segurança. Com alguns cliques, criam uma tarefa de segurança para a Intune que identifica os dispositivos em risco, a vulnerabilidade, e fornece orientações sobre como mitigar esse risco.

- Os Intune Admins revêem as tarefas de segurança e, em seguida, atuam no Intune para remediar essas tarefas. Uma vez atenuados, definiram a tarefa para completar, que comunica esse estatuto de volta à equipa ATP do Defender.

Através de tarefas de Segurança, ambas as equipas permanecem em sintonia sobre quais os dispositivos em risco, e como e quando esses riscos são remediados.

Para saber mais sobre a utilização de tarefas de Segurança, consulte [O Intune use para remediar as vulnerabilidades identificadas pelo Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Utilize políticas para gerir a segurança do dispositivo

Como administrador de segurança, use as políticas de segurança que são encontradas no *nó de* segurança De Endpoint. Com estas políticas pode configurar a segurança do dispositivo sem a sobrecarga de navegar no corpo maior e na gama de configurações a partir de perfis de configuração do dispositivo e linhas de base de segurança.

![Gerir políticas](./media/endpoint-security/endpoint-security-policies.png)

Para saber mais sobre o uso destas políticas de segurança, consulte Gerir a segurança do dispositivo com políticas de [segurança de ponto final](../protect/endpoint-security-policy.md).

As políticas de segurança do endpoint são um dos vários métodos em Intune para configurar as definições nos dispositivos. Ao gerir as definições, é importante entender que outros métodos estão a ser utilizados no seu ambiente que podem configurar os seus dispositivos e evitar conflitos. Ver [Evitar conflitos políticos](#avoid-policy-conflicts) mais tarde neste artigo.

Também são encontrados no âmbito *do Manage* estão as políticas de conformidade do *Dispositivo* e de *acesso condicional.* Estes tipos de políticas não são políticas de segurança focadas para configurar pontos finais, mas são ferramentas importantes para gerir dispositivos e aceder aos seus recursos corporativos.

## <a name="use-device-compliance-policy"></a>Utilize a política de conformidade do dispositivo

Utilize a política de conformidade do dispositivo para estabelecer as condições pelas quais os dispositivos e utilizadores podem aceder à sua rede e recursos da empresa.

As [definições](../protect/device-compliance-get-started.md#next-steps) de conformidade disponíveis dependem da plataforma que utiliza, mas as regras de política comuns incluem:

- Exigir que os dispositivos executem uma versão sotamínima ou específica
- Definição de requisitos de palavra-passe
- Especificando um nível máximo permitido de ameaça de dispositivo, determinado pelo Defender ATP ou outro parceiro de Defesa de Ameaças Móveis

Para além das regras políticas, as políticas de conformidade apoiam:

- [Locais](../protect/use-network-locations.md) que define em Intune. Quando utiliza localizações com uma política de conformidade, a política pode garantir que os dispositivos estão ligados a uma rede de trabalho para serem conformes.
- [Ações de incumprimento.](../protect/actions-for-noncompliance.md) Estas ações são uma sequência de ações ordenada pelo tempo para aplicar a dispositivos não conformes. As ações incluem o envio de e-mails ou notificações para alertar os utilizadores do dispositivo sobre o incumprimento, dispositivos de bloqueio remoto ou até mesmo a retirada de dispositivos não conformes e remover quaisquer dados da empresa que possam estar nele.

Quando integra as políticas de [acesso condicional](#configure-conditional-access) da Azure AD para impor as políticas de conformidade, o acesso condicional pode utilizar os dados de conformidade para aceder ao acesso de porta a recursos corporativos tanto para dispositivos geridos como para dispositivos que não gere.

Para saber mais, consulte [as regras definidas sobre dispositivos para permitir o acesso aos recursos da sua organização utilizando o Intune](../protect/device-compliance-get-started.md).

As políticas de conformidade do dispositivo são um dos vários métodos em Intune para configurar as definições nos dispositivos. Ao gerir as definições, é importante entender que outros métodos estão a ser utilizados no seu ambiente que podem configurar os seus dispositivos e evitar conflitos. Ver [Evitar conflitos políticos](#avoid-policy-conflicts) mais tarde neste artigo.

## <a name="configure-conditional-access"></a>Configurar o acesso condicional

Para proteger os seus dispositivos e recursos corporativos, pode utilizar políticas de Acesso Condicional azure Ative (Azure AD) com a Intune.

Intune passa os resultados das políticas de conformidade do seu dispositivo para a AD Azure, que depois utiliza políticas de acesso condicional para impor quais dispositivos e aplicações podem aceder aos seus recursos corporativos. As políticas de acesso condicional podem ajudar o acesso do portal a dispositivos que não são geridos pela Intune. Pode até utilizar detalhes de conformidade dos [parceiros de Defesa de Ameaças Móveis](../protect/mobile-threat-defense.md) que integra com o Intune.

Seguem-se dois métodos comuns de utilização do acesso condicional com o Intune:

- **Acesso condicional baseado em dispositivos,** para garantir que apenas dispositivos geridos e conformes possam aceder aos recursos da rede.
- **Acesso condicional baseado em aplicativos**, que utiliza políticas de proteção de aplicações para gerir o acesso aos recursos de rede pelos utilizadores em dispositivos que não gere com o Intune.

Para saber mais sobre o uso do acesso condicional com Intune, consulte [Saiba sobre acesso condicional e Insinton .](../protect/conditional-access.md)

## <a name="set-up-integration-with-defender-atp"></a>Criar integração com o Defender ATP

Ao integrar a Microsoft Defender Advanced Threat Protection (Defender ATP) com o Intune, melhora a sua capacidade de identificar e responder a riscos.

Enquanto a Intune pode integrar-se com vários [parceiros de Defesa de Ameaças Móveis,](../protect/mobile-threat-defense.md)quando utiliza o Defender ATP ganha-se uma integração apertada entre o Defender ATP e o Intune com acesso a opções de proteção de dispositivos profundos, incluindo:

- Tarefas de segurança – Comunicação perfeita entre os administradores ATP e Intune sobre dispositivos em risco, como remediar os mesmos e confirmação quando esses riscos são atenuados.
- Streamlineon onboarding for Defender ATP on customers.
- Utilização de sinais de risco de dispositivo ATP nas políticas de conformidade intune.
- Acesso às capacidades de *proteção de Adulteração.*

 Para saber mais sobre a utilização do Defender ATP com Intune, consulte [Enforce compliance for Microsoft Defender ATP with Conditional Access in Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Requisitos de controlo de acesso baseados em funções

Para gerir tarefas no nó de segurança Endpoint do centro de administração do Microsoft Endpoint Manager, uma conta deve:

- Será atribuída uma licença para Intune.
- Dispor de permissões de controlo de acesso baseadas em papéis (RBAC) iguais às permissões fornecidas pelo papel intune incorporado do **Endpoint Security Manager**. O papel *do Endpoint Security Manager* concede acesso ao centro de administração do Microsoft Endpoint Manager. Esta função pode ser usada por indivíduos que gerem funcionalidades de segurança e conformidade, incluindo linhas de segurança, conformidade com dispositivos, acesso condicional e ATP do Microsoft Defender.

Para mais informações, consulte [o controlo de acesso baseado em Role (RBAC) com](../fundamentals/role-based-access-control.md) o Microsoft Intune

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Permissões concedidas pelo papel de Gestor de *Segurança endpoint*

Pode ver a seguinte lista de permissões no centro de administração do Microsoft Endpoint Manager, indo para a **administração do Tenant**  >  **Roles**  >  **All Roles**, selecione **Endpoint Security Manager**  >  **Properties**.

**Permissões:**

- **Android for Work**
  - Leitura
- **Dados de auditoria**
  - Leitura
- **Identificadores de dispositivos corporativos**
  - Leitura
- **Políticas de conformidade de dispositivo**
  - Atribuir
  - Criar
  - Eliminar
  - Leitura
  - Atualizar
  - Ver relatórios
- **Configurações de dispositivo**
  - Leitura
- **Gestores de inscrição de dispositivos**
  - Leitura
- **Relatórios de proteção do ponto final**
  - Leitura
- **Programas de inscrição**
  - Ler dispositivo
  - Ler perfil
  - Ler ficha
- **Armazém de dados insinado**
  - Leitura
- **Aplicações geridas**
  - Leitura
- **Dispositivos geridos**
  - Eliminar
  - Leitura
  - Definir o utilizador primário
  - Atualizar
- **Aplicações móveis**
  - Leitura
- **Organização**
  - Leitura
- **Conjuntos de Políticas**
  - Leitura
- **Assistência remota**
  - Leitura
- **Tarefas remotas**
  - Pegue a chave FileVault.
- **Funções**
  - Leitura
- **Linhas de base de segurança**
  - Atribuir
  - Criar
  - Eliminar
  - Leitura
  - Atualizar
- **Tarefas de segurança**
  - Leitura
  - Atualizar
- **Despesas de telecomunicações**
  - Leitura
- **Termos e condições**
  - Leitura

## <a name="avoid-policy-conflicts"></a>Evitar conflitos políticos

Muitas das definições que pode configurar para dispositivos podem ser geridas por diferentes funcionalidades em Intune. Estas funcionalidades incluem, mas não se limitam a:

- Políticas de segurança do ponto final
- Linhas de base de segurança
- Políticas de configuração do dispositivo
- Políticas de inscrição do Windows 10

Por exemplo, as definições encontradas nas políticas de segurança endpoint são um subconjunto das definições que são encontradas nos perfis de *proteção* de pontofinal e *de restrição* de dispositivos na política de configuração do dispositivo, e que também são geridas através de várias linhas de segurança.

Uma forma de evitar conflitos é não utilizar diferentes linhas de base, instâncias da mesma linha de base, ou diferentes tipos de políticas e instâncias para gerir as mesmas configurações num dispositivo. Isto requer planeamento dos métodos que utilizará para implementar configurações em diferentes dispositivos. Quando utilizar vários métodos ou instâncias do mesmo método para configurar a mesma definição, certifique-se de que os seus diferentes métodos concordam ou não estão implantados nos mesmos dispositivos.

Se os conflitos acontecerem, pode usar as ferramentas incorporadas de Intune para identificar e resolver a origem desses conflitos. Para obter mais informações, consulte:

- [Resolução de problemas de políticas e perfis no Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorize as suas linhas de base de segurança](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Próximos passos

Configurar:

- [Linhas de base de segurança](../protect/security-baselines.md)
- [Políticas de conformidade](../protect/device-compliance-get-started.md)
- [Políticas de acesso condicional](#configure-conditional-access)
- [Integração com o Defender ATP](../protect/advanced-threat-protection.md)
