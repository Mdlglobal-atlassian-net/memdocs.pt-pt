---
title: Gerir as definições antivírus com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas e utilize relatórios para dispositivos que gere com a política antivírus de segurança final no Microsoft Endpoint Manager.
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
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431383"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Política antivírus para segurança de pontofinal em Intune

As políticas antivírus de segurança intune Endpoint podem ajudar os administradores de segurança a concentrarem-se na gestão do grupo discreto de definições antivírus para dispositivos geridos. Para utilizar a política Antivírus, integre o Intune com a Microsoft Defender Advanced Threat Protection (Defender ATP) como uma solução de Defesa de Ameaças Móveis.

A política antivírus inclui vários perfis. Cada perfil contém apenas as definições relevantes para o antivírus ATP defender para macOS, Windows 10 ou para a experiência do utilizador na aplicação Windows Security nos dispositivos Windows 10.

Encontrará as políticas antivírus no **âmbito do Manage** in the Endpoint security node de segurança do centro de administração do Microsoft [Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

As políticas antivírus incluem as mesmas definições encontradas nos perfis de proteção de *pontos finais* ou de restrição de *dispositivos* para a política de [configuração](../configuration/device-profile-create.md) do dispositivo e são semelhantes às definições da política de conformidade do [dispositivo.](../protect/device-compliance-get-started.md) No entanto, esses tipos de políticas incluem categorias adicionais de configurações que não estão relacionadas com o Antivírus. As configurações adicionais podem complicar a tarefa de configurar o Antivírus. Além disso, as definições encontradas na política antivírus para macOS não estão disponíveis através dos outros tipos de políticas. O perfil macOS Antivírus substitui a necessidade de configurar as definições utilizando `.plist` ficheiros.

## <a name="prerequisites-for-antivirus-policy"></a>Pré-requisitos para a política antivírus

- **macOS**
  - Qualquer versão suportada do macOS
  - Para que a Intune gere as definições antivírus num dispositivo, o Defender ATP deve ser instalado nesse dispositivo. Vê. [Defender ATP para macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (Na documentação ATP defender)

- **Windows 10 e posterior**
  - Para que a Intune gere as definições antivírus num dispositivo, o Defender ATP deve ser instalado nesse dispositivo. Veja, [Microsoft Defender ATP para Windows,](../protect/advanced-threat-protection.md)na documentação Intune.
  - A aplicação Windows Security está instalada em todos os dispositivos que executam a Janela 10, e não são necessários pré-requisitos adicionais.

## <a name="antivirus-profiles"></a>Perfis antivírus

**perfis macOS:**

- **Antivírus** - Gerir [as definições de política antivírus](../protect/antivirus-microsoft-defender-settings-macos.md) para macOS.

  Quando utilizar o [Microsoft Defender ATP para Mac,](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)pode configurar e implementar as definições antivírus nos dispositivos macOS geridos através do Intune, em vez de configurar essas definições através da utilização de `.plist` ficheiros.

**Perfis do Windows 10:**

- **Microsoft Defender Antivírus** - [Gerencie as definições](../protect/antivirus-microsoft-defender-settings-windows.md) de política antivírus para o Windows 10.

  O Defender Antivirus é o componente de proteção de próxima geração da Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). A proteção de próxima geração reúne machine learning, análise de big data, pesquisa aprofundada de resistência a ameaças e infraestruturas em nuvem para proteger dispositivos na sua organização empresarial.

  O perfil *Antivírus Do Microsoft Defender* é uma instância separada das definições antivírus que são encontradas no perfil de *restrição* do dispositivo para a política de configuração do dispositivo.
  
  Ao contrário das definições antivírus num perfil de *restrição*de dispositivos, pode utilizar estas definições com dispositivos cogeridos. Para utilizar estas definições, o slider de [carga de trabalho de cogestão](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para proteção de pontos finais deve ser definido para Intune.

- **Experiência de Segurança do Windows** – Gerir as definições da [aplicação Windows Security](../protect/antivirus-security-experience-windows-settings.md) que os utilizadores finais podem visualizar no centro de Segurança do Microsoft Defender e nas notificações que recebem. A aplicação de segurança Windows é utilizada por uma série de funcionalidades de segurança do Windows para fornecer notificações sobre a saúde e segurança da máquina. As notificações de aplicações de segurança incluem firewalls, produtos antivírus, Windows Defender SmartScreen, entre outros.

## <a name="antivirus-policy-reports"></a>Relatórios de política antivírus

Os relatórios de política antivírus mostram detalhes do estado sobre as políticas antivírus de segurança do ponto final e o estado do dispositivo. Estes relatórios estão disponíveis no nó de segurança Endpoint do centro de administração do Microsoft Endpoint Manager.

Para ver os relatórios, no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)vá à segurança endpoint e selecione **Antivírus**. A seleção do Antivírus abre a página Resumo. Relatórios adicionais e pontos de vista de estado estão disponíveis como páginas adicionais.

### <a name="summary"></a>Resumo

Na página **Resumo,** pode [criar novas políticas](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) e ver uma lista das políticas que foram previamente criadas. A lista inclui detalhes de alto nível sobre o perfil que a política inclui (Tipo de Política), e se a política for atribuída.

![Página geral da política antivírus](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Quando seleciona uma política da lista, a página *de visão geral* para essa instância de política abre e exibe mais informações. Quando seleciona um azulejo desta vista, intune apresenta detalhes adicionais para esse perfil se estiverem disponíveis.

![Página geral da política antivírus](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Pontos finais pouco saudáveis do Windows 10

Na página de **pontos finais pouco saudáveis do Windows 10,** pode visualizar informações sobre o estado antivírus dos seus dispositivos Windows 10 geridos pelo MDM. Esta informação é devolvida do Antivírus Do Windows Defender que funciona no dispositivo, como estado do *agente ameaça*.

Apenas os dispositivos com problemas detetados aparecem nesta visão. Esta vista não mostra detalhes para dispositivos identificados como limpos.

![Página geral da política antivírus](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Próximos passos

[Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
