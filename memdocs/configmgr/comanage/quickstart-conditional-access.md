---
title: Acesso condicional com cogestão
titleSuffix: Configuration Manager
description: Controlar o acesso dos utilizadores aos recursos organizacionais com base nas regras de conformidade da Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711505"
---
# <a name="conditional-access-with-co-management"></a>Acesso condicional com cogestão

O acesso condicional garante que apenas os utilizadores de confiança podem aceder a recursos organizacionais em dispositivos fidedignos utilizando aplicações fidedignas. É construído de raiz na nuvem. Quer esteja a gerir dispositivos com o Intune ou a alargar a implementação do Seu Gestor de Configuração com cogestão, funciona da mesma forma.

No vídeo seguinte, o gestor de programas sénior Joey Glocke e o gestor de marketing de produtos Locky Ainley discutem e demo acesso condicional com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Com a cogestão, a Intune avalia todos os dispositivos da sua rede para determinar a sua fiabilidade. Faz esta avaliação das seguintes duas formas:

1. Intune certifica-se de que um dispositivo ou aplicação é gerido e configurado de forma segura. Este cheque depende de como define as políticas de conformidade da sua organização. Por exemplo, certifique-se de que todos os dispositivos têm encriptação ativada e não estão quebrados.  

    - Esta avaliação é de violação pré-segurança e baseada em configuração  

    - Para dispositivos cogeridos, o Gestor de Configuração também faz avaliação baseada na configuração. Por exemplo, as atualizações necessárias ou o cumprimento das aplicações. Intune combina esta avaliação juntamente com a sua própria avaliação.  

2. Intune deteta incidentes de segurança ativa num dispositivo. Utiliza a segurança inteligente da [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (anteriormente Windows Defender ATP) e de outros fornecedores de defesa de ameaças [móveis.](https://www.lookout.com/about/partners/microsoft) Estes parceiros executam uma análise comportamental contínua em dispositivos. Esta análise deteta incidentes ativos e, em seguida, passa esta informação para Intune para avaliação de conformidade em tempo real.  

    - Esta avaliação é violação pós-segurança e incidentes  

O vice-presidente corporativo da Microsoft, Brad Anderson, discute o acesso condicional em profundidade com demonstrações ao vivo durante o keynote Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

O acesso condicional também lhe proporciona um local centralizado para ver a saúde de todos os dispositivos ligados à rede. Obtém-se as vantagens da escala de nuvem, que é especialmente valiosa para testar casos de produção do Gestor de Configuração.


## <a name="benefits"></a>Benefícios

Todas as equipas de TI são obcecadas com a segurança da rede. É obrigatório certificar-se de que todos os dispositivos cumprem os seus requisitos de segurança e negócioantes de aceder à sua rede. Com acesso condicional, pode determinar os seguintes fatores: 
- Se todos os dispositivos estiverem encriptados  
- Se o malware for instalado  
- Se as suas definições forem atualizadas  
- Se estiver na prisão quebrada ou enraizada  

O acesso condicional combina o controlo granular sobre os dados organizacionais com uma experiência do utilizador que maximiza a produtividade dos trabalhadores em qualquer dispositivo a partir de qualquer local.

O seguinte vídeo mostra como a [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) está integrada em cenários comuns que experimenta regularmente:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Com a cogestão, a Intune pode incorporar as responsabilidades do Gestor de Configuração para avaliar as suas normas de segurança no cumprimento das atualizações ou aplicações necessárias. Este comportamento é importante para qualquer organização de TI que queira continuar a usar o Gestor de Configuração para uma gestão complexa de aplicações e patch.

O acesso condicional é também uma parte crítica do desenvolvimento da sua arquitetura [Zero Trust Network.](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) Com acesso condicional, os controlos de acesso do dispositivo em conformidade cobrem as camadas fundacionais da Rede Zero Trust. Esta funcionalidade é uma grande parte da forma como protege a sua organização no futuro.

Para mais informações, consulte a publicação do blog sobre [o melhoramento do acesso condicional com dados de risco de máquina sacar da Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Estudos de caso

A empresa de consultoria de TI Wipro utiliza acesso condicional para proteger e gerir os dispositivos utilizados por todos os 91.000 colaboradores. Num estudo de caso recente, o vice-presidente de TI da Wipro observou:

> *Conseguir acesso condicional é uma grande vitória para a Wipro. Agora, todos os nossos empregados têm acesso móvel à informação a pedido.* 
>  *Aumentámos a nossa postura de segurança e a produtividade dos colaboradores. Agora, 91.000 colaboradores beneficiam de um acesso altamente seguro a mais de 100 aplicações de qualquer dispositivo, em qualquer lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Outros exemplos incluem: 

- Nestlé, que usa acesso condicional baseado em aplicativos para mais de 150.000 funcionários  

- A empresa de software de automação, Cadence, que pode agora certificar-se de que "apenas os dispositivos geridos têm acesso a aplicações do Office 365, como as Equipas e a intranet da empresa". Podem também oferecer aos seus trabalhadores "um acesso mais seguro a outras aplicações baseadas na nuvem, como o Workday e o Salesforce". Para obter mais informações sobre a experiência da Cadence com o Intune, veja-se que [a Cadence aumenta o ritmo de negócios com ferramentas de colaboração móvel na Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune também está totalmente integrado com parceiros como Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Com estes parceiros, pode manter controlos de acesso com base na inscrição intune e no estado de conformidade do dispositivo através destas outras plataformas.

Para mais informações, consulte os seguintes vídeos:
- [Brad Anderson demos acesso condicional em detalhe](https://youtu.be/8321obNofgM?t=547)  
- [Detalhes adicionais da Zona Endpoint 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposta de valor

Com acesso condicional e integração ATP, está a fortalecer um componente fundamental de cada organização de TI: acesso seguro à nuvem.

Em mais de 63% de todas as violações de dados, os atacantes têm acesso à rede da organização através de credenciais de utilizador fracas, em incumprimento ou roubadas. Uma vez que o acesso condicional se centra na garantia da identidade do utilizador, restringe o roubo da credencial. O acesso condicional gere e protege as suas identidades, privilegiadas ou não privilegiadas. Não há melhor maneira de proteger os dispositivos e os dados sobre eles.

Uma vez que o acesso condicional é um componente central da Enterprise Mobility + Security (EMS), não é necessária configuração ou arquitetura no local. Com o Intune e o Azure Ative Directory (Azure AD), pode configurar rapidamente o acesso condicional na nuvem. Se está a utilizar o Gestor de Configuração, pode facilmente estender o seu ambiente à nuvem com cogestão e começar a usá-lo agora mesmo.

Para obter mais informações sobre a integração ATP, consulte esta publicação de blog [Microsoft Defender ATP a pontuação](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/)de risco do dispositivo expõe um novo ciberataque, impulsiona o acesso condicional para proteger redes . Detalha como um grupo avançado de hackers usou ferramentas nunca antes vistas. A nuvem da Microsoft detetou-os e deteve-os porque os utilizadores visados tinham acesso condicional. A intrusão ativou a política de acesso condicional baseada no risco do dispositivo. Embora o atacante já estabelecesse uma posição de pé na rede, as máquinas exploradas eram automaticamente restringidas do acesso a serviços organizacionais e dados geridos pela Azure AD.



## <a name="configure"></a>Configurar

O acesso condicional é fácil de usar quando ativa a [cogestão.](how-to-enable.md) Requer a deslocação da carga de trabalho das Políticas de **Conformidade** para Intune. Para mais informações, consulte Como mudar as cargas de [trabalho do Gestor de Configuração para Intune](how-to-switch-workloads.md). 

Para obter mais informações sobre o acesso condicional, consulte os seguintes artigos: 

- [Acesso condicional no Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Políticas de conformidade de dispositivos do Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Acesso condicional com base na aplicação com o Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> As funcionalidades de acesso condicional ficam imediatamente disponíveis para dispositivos híbridos azure ad-join. Estas funcionalidades incluem a autenticação multi-factor e o Híbrido Azure AD juntam-se ao controlo de acesso. Este comportamento é porque são baseados em propriedades da AD Azure. Para alavancar a avaliação baseada na configuração do Intune e do Gestor de Configuração, ative a cogestão. Esta configuração dá-lhe controlo de acesso diretamente a partir de Intune para dispositivos conformes. Também lhe dá a funcionalidade de avaliação de políticas de conformidade da Intune.  

