---
title: O que é o Configuration Manager?
titleSuffix: Configuration Manager
description: Conheça os fundamentos do Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c3be302ecefad36d7be8617a4cc9354db1b685
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906064"
---
# <a name="what-is-configuration-manager"></a>O que é o Configuration Manager?

*Aplica-se a: Gestor de Configuração (ramo atual)*

A partir da versão 1910, o Gestor de Configuração faz agora parte do Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

O Microsoft Endpoint Manager é uma solução integrada para gerir todos os seus dispositivos. A Microsoft reúne o Gestor de Configuração e o Intune, sem uma migração complexa, e com licenciamento simplificado. Continue a alavancar os investimentos existentes no Gestor de Configuração, aproveitando ao mesmo ritmo o poder da nuvem da Microsoft.

As seguintes soluções de gestão da Microsoft fazem agora parte da marca **Microsoft Endpoint Manager:**

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Análise de Computadores](../../desktop-analytics/overview.md)
- [Piloto automático](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Outras funcionalidades na [Consola de Gestão](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760) de Dispositivos

Para mais informações, consulte [o Microsoft Endpoint Configuration Manager FAQ](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Introdução

Utilize o Gestor de Configuração para o ajudar nas seguintes atividades de gestão de sistemas:

- Aumente a produtividade e eficiência de TI reduzindo tarefas manuais e permitindo que se concentre em projetos de alto valor.  
- Maximizar os investimentos em hardware e software.  
- Capacitar a produtividade dos utilizadores fornecendo o software certo no momento certo.  

O Gestor de Configuração ajuda-o a fornecer serviços de TI mais eficazes, permitindo:

- Implementação segura e escalável de aplicações, atualizações de software e sistemas operativos.
- Ações em tempo real em dispositivos geridos.
- Análise e gestão alimentadas por nuvem para dispositivos no local e na Internet.
- Gestão de definições de conformidade.  
- Gestão abrangente de servidores, desktops e portáteis.

O Gestor de Configuração estende-se e trabalha ao lado de muitas tecnologias e soluções da Microsoft. Por exemplo, o Gestor de Configuração integra-se com:  

- Microsoft Intune para cogerir uma grande variedade de plataformas de dispositivos móveis
- Microsoft Azure vai acolher serviços na nuvem para alargar os seus serviços de gestão
- Windows Server Update Services (WSUS) para gerir atualizações de software
- Serviços de Certificados
- Exchange Server e Exchange Online
- Política de Grupo
- DNS
- Kit de implementação automatizado do Windows (Windows ADK) e a ferramenta de migração do Estado utilizador (USMT)
- Serviços de implementação do Windows (WDS)
- Ambiente de Trabalho Remoto e Assistência Remota

O Gestor de Configuração também utiliza:  

- Serviços de Domínio de Diretório Ativo e Diretório Ativo Azure para segurança, localização de serviço, configuração e para descobrir os utilizadores e dispositivos que pretende gerir.  
- O Microsoft SQL Server como base de dados de gestão de mudanças distribuídas e integra-se com os Serviços de Relato de Servidores SQL (SSRS) para produzir relatórios para monitorizar e rastrear atividades de gestão.  
- Funções do sistema do site que alargam a funcionalidade de gestão e utilizam os serviços web dos Serviços de Informação da Internet (IIS).
- Otimização de Entrega, Transporte de Fundo de Atraso Extra do Windows (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache e outras tecnologias de cache de pares para ajudar a gerir conteúdos nas suas redes e entre dispositivos.

Para ter sucesso com o Gestor de Configuração num ambiente de produção, planeie e teste cuidadosamente as funcionalidades de gestão. O Gestor de Configuração é uma aplicação de gestão poderosa, com potencial para afetar todos os computadores da sua organização. Quando implementa e gere o Gestor de Configuração com um planeamento cuidadoso e consideração dos seus requisitos de negócio, o Gestor de Configuração pode reduzir a sua despesa administrativa e o custo total de propriedade.  

## <a name="user-interfaces"></a>Interfaces de utilizador

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> A consola do Configuration Manager

Depois de instalar o Gestor de Configuração, utilize a consola Do Gestor de Configuração para configurar sites e clientes e executar e monitorizar tarefas de gestão. Esta consola é o principal ponto de administração, e permite-lhe gerir vários sites.  

Pode instalar a consola do Gestor de Configuração em computadores adicionais e restringir o acesso e limitar o que os utilizadores administrativos podem ver na consola utilizando a administração baseada em funções do Gestor de Configuração.  

Para mais informações, consulte [Utilize a consola 'Gestor de Configuração'.](../servers/manage/admin-console.md)

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a>Centro de Software

**O Software Center** é uma aplicação instalada quando instala o cliente do Gestor de Configuração num dispositivo Windows. Os utilizadores usam o Software Center para solicitar e instalar software que implementa. O Software Center permite que os utilizadores façam as seguintes ações:  

- Procure e instale aplicações, atualizações de software e novas versões de SO
- Veja o histórico de pedidos de software
- Ver conformidade com o dispositivo contra as políticas da sua organização

Também pode mostrar separadores personalizados no Software Center para satisfazer requisitos comerciais adicionais.

Para mais informações, consulte o guia de utilizador do Centro de [Software](software-center.md).

## <a name="next-steps"></a>Próximos passos

Antes de instalar o Gestor de Configuração, familiarize-se com os conceitos e termos básicos:

- Se estiver familiarizado com o System Center 2012 Configuration Manager, veja [o que mudou do System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Para uma visão geral técnica de alto nível do Gestor de Configuração, consulte [Fundamentos de Gestor de Configuração](fundamentals.md).

Quando estiver familiarizado com os conceitos básicos, use esta biblioteca de documentação para ajudá-lo a implementar e utilizar com sucesso o Gestor de Configuração. Comece com os seguintes artigos:

- [Funcionalidades e capacidades do Gestor de Configuração](../plan-design/changes/features-and-capabilities.md)  
- [Escolher uma solução de gestão de dispositivos](../plan-design/choose-a-device-management-solution.md)  
- [Avaliar o Gestor de Configuração construindo o seu próprio ambiente de laboratório](../get-started/set-up-your-lab.md)
- [Encontre ajuda para usar o Gestor de Configuração](find-help.md)  
