---
title: Funcionalidades e capacidades
titleSuffix: Configuration Manager
description: Conheça as principais capacidades de gestão do Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722376"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Funcionalidades e capacidades do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo resume as principais funcionalidades de gestão do Gestor de Configuração. Cada funcionalidade tem os seus próprios pré-requisitos, e como cada um pode influenciar o design e implementação da sua hierarquia do Gestor de Configuração. Por exemplo, se pretender implementar atualizações de software para dispositivos na sua hierarquia, precisa de uma função do sistema de pontode atualização de software.  

Para obter mais informações sobre como planear e instalar o Gestor de Configuração para suportar estas capacidades de gestão no seu ambiente, consulte [Prepare-se para O Gestor](../get-ready.md)de Configuração .  

## <a name="co-management"></a>Cogestão

A cogestão é uma das principais formas de anexar a implementação do seu Gestor de Configuração existente à nuvem Microsoft 365. Permite-lhe gerir simultaneamente os dispositivos do Windows 10 utilizando tanto o 'Configuração Manager' como o Microsoft Intune. A cogestão permite-lhe anexar o seu investimento existente em 'Gestor de Configuração', adicionando novas funcionalidades como acesso condicional. Para mais informações, consulte [o que é a cogestão?](../../../comanage/overview.md)

## <a name="desktop-analytics"></a>Análise de Computadores

Desktop Analytics é um serviço baseado na nuvem que se integra com o Gestor de Configuração. O serviço fornece informações e inteligência para que tome decisões mais informadas sobre a prontidão da atualização dos seus clientes Windows. Combina dados da sua organização com dados agregados de milhões de dispositivos ligados aos serviços de cloud da Microsoft. Para mais informações, consulte [o que é desktop Analytics?](../../../desktop-analytics/overview.md)

## <a name="cloud-attached-management"></a>Gestão ligada à cloud

Utilize funcionalidades como o gateway de gestão na cloud, os pontos de distribuição baseados na cloud e o Azure Active Directory para gerir clientes baseados na Internet.

Para obter mais informações, veja os artigos seguintes:

- [Gerir clientes na internet](../../clients/manage/manage-clients-internet.md)
- [Plano do Microsoft Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Serviços do Azure](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Gestão em tempo real

Utilize a CMPivot para consultar imediatamente os dispositivos online, em seguida, filtrar e agrupar os dados para informações mais profundas. Utilize também a consola 'Gestor de Configuração' para gerir e implementar scripts Do Windows PowerShell para os clientes. Para mais informações, consulte [cmPivot](../../servers/manage/cmpivot.md) e [Criar e executar scripts PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Gestão de aplicações

Ajuda-o a criar, gerir, implementar e monitorizar aplicações para uma gama de dispositivos diferentes que gere. Implementar, atualizar e gerir o Office 365 a partir da consola Do Gestor de Configuração. Além disso, o Gestor de Configuração integra-se com a Microsoft Store for Business and Education para fornecer aplicações baseadas na nuvem. Para mais informações, consulte [Introdução à gestão de aplicações.](../../../apps/understand/introduction-to-application-management.md)

## <a name="os-deployment"></a>Implementação de SO

Implemente uma atualização no local do Windows 10, ou capture e implemente imagens de OS. A implementação da imagem pode utilizar suportes PXE, multicast ou bootable. Também pode ajudar a reimplantar dispositivos existentes utilizando o Windows AutoPilot. Para mais informações, consulte [Introdução à implementação do OS](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Atualizações de software

Gerir, implementar e monitorizar atualizações de software na organização. Integre com a Otimização de Entrega do Windows e outras tecnologias de cache de pares para ajudar a controlar o uso da rede. Para mais informações, consulte [Introdução a atualizações de software](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Acesso aos recursos da empresa

Permite-lhe dar aos utilizadores da sua organização acesso a dados e aplicações a partir de locais remotos. Esta funcionalidade inclui perfis de Wi-Fi, VPN, e-mail e certificado. Para mais informações, consulte [Proteja os dados e a infraestrutura do site.](../../../protect/understand/protect-data-and-site-infrastructure.md)

## <a name="compliance-settings"></a>Definições de compatibilidade

Ajuda-o a avaliar, rastrear e remediar a conformidade de configuração dos dispositivos clientes na organização. Além disso, pode utilizar as definições de conformidade para configurar uma série de funcionalidades e definições de segurança nos dispositivos que gere. Para mais informações, consulte Garantir a [conformidade do dispositivo](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Endpoint Protection

Fornece gestão de segurança, antimalware e Firewall do Windows para computadores na sua organização. Esta área inclui gestão e integração com as seguintes funcionalidades do windows defender:

- Antivírus do Windows Defender
- Proteção Avançada Contra Ameaças do Microsoft Defender
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Controlo de Aplicações do Windows Defender
- Firewall do Windows Defender

Para mais informações, consulte [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Inventário

Ajuda-o a identificar e monitorizar os bens.

### <a name="hardware-inventory"></a>Inventário de Hardware

Recolhe informações detalhadas sobre o hardware dos dispositivos na sua organização. Para mais informações, consulte Introdução ao inventário de [hardware](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Inventário de software

Recolhe e reporta informações sobre os ficheiros que são armazenados em computadores clientes na sua organização. Para mais informações, consulte [Introdução ao inventário de software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Asset Intelligence

Fornece ferramentas para recolher dados de inventário e monitorizar o uso da licença de software na sua organização. Para mais informações, consulte Introdução à Inteligência de [Ativos.](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)  

## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local

Inscreve e gere os dispositivos utilizando a infraestrutura do Gestor de Configuração no local com a funcionalidade de gestão incorporada nas plataformas do dispositivo. (A gestão típica utiliza um cliente de Gestor de Configuração instalado separadamente.) Esta funcionalidade suporta atualmente a gestão de dispositivos Windows 10 Enterprise e Windows 10 Mobile. Para mais informações, consulte [Gerir dispositivos móveis com infraestrutura no local.](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)  

## <a name="power-management"></a>Gestão de energia

Gerir e monitorizar o consumo de energia dos computadores clientes na organização. Configure os planos de energia e use Wake-on-LAN para fazer manutenção fora do horário comercial. Para mais informações, consulte [Introdução à gestão de energia.](../../clients/manage/power/introduction-to-power-management.md)  

## <a name="remote-control"></a>Controlo remoto

Fornece ferramentas para administrar remotamente computadores clientes a partir da consola Do Gestor de Configuração. Para mais informações, consulte [Introdução ao controlo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Relatórios

Utilize as capacidades avançadas de reporte dos Serviços de Reporte de Servidores SQL a partir da consola Do Gestor de Configuração. Esta funcionalidade fornece centenas de relatórios predefinidos. Para mais informações, consulte [Introdução a relatórios.](../../servers/manage/introduction-to-reporting.md)  

## <a name="software-metering"></a>Medição de software

Monitorize e colete dados de utilização de software a partir de clientes do Gestor de Configuração. Pode utilizar estes dados para determinar se o software é utilizado após a sua instalação. Para obter mais informações, consulte o [uso da aplicação Monitor com a medição de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
