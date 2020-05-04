---
title: Configurações suportadas
titleSuffix: Configuration Manager
description: Identifique configurações e requisitos chave para que possa planear, implementar e manter uma implementação funcional do Gestor de Configuração.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709573"
---
# <a name="supported-configurations-for-configuration-manager"></a>Configurações suportadas do Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Como solução no local, o Gestor de Configuração utiliza os seus servidores, clientes, configurações de rede e produtos adicionais como microsoft Intune, SQL Server e Azure.

A informação neste e nos seguintes tópicos é essencial para ajudá-lo a identificar configurações, requisitos e limitações chave, para que possa planear, implementar e manter uma implementação funcional do Gestor de Configuração.  Esta informação é específica da infraestrutura para sites de Gestor de Configuração, hierarquias e dispositivos geridos.

Quando uma funcionalidade ou capacidade do Gestor de Configuração requer configurações mais específicas, essa informação é incluída com a documentação específica da funcionalidade, e é suplementar aos detalhes de configuração mais gerais.  

 Os produtos e tecnologias que são descritos nos seguintes tópicos são suportados pelo Gestor de Configuração. No entanto, a sua inclusão neste conteúdo não implica uma extensão do suporte a qualquer produto para além do ciclo de vida individual de suporte desse produto. Os produtos que estão para além do seu ciclo de vida de suporte não são suportados para uso com o Gestor de Configuração, incluindo quaisquer produtos abrangidos pelo programa [Extended Security Updates (ESU).](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270) . Para obter mais informações sobre atualizações de segurança estendidas no Gestor de Configuração, consulte [versões De SO suportadas para clientes e dispositivos para O Gestor](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU)de Configuração .

> [!NOTE]  
>  Para obter informações sobre a política de suporte de vida da Microsoft, vá ao site FAQ da Política de Suporte ao Suporte ao Vida da Microsoft no [Microsoft Support Lifecycle Policy FAQ](https://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Além disso, os produtos e versões de produtos que não estão listados nos seguintes tópicos não são suportados com o Gestor de Configuração, a menos que tenham sido anunciados no Blog de [Mobilidade e Segurança Empresarial.](https://blogs.technet.microsoft.com/enterprisemobility/)  Por vezes, o conteúdo deste blog antecede uma atualização a este corpo de documentação.


-  [Dimensionamento e números da escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Saiba quantos sites, funções do sistema de site por site, e clientes ou dispositivos são suportados em diferentes projetos de hierarquia para Configuração Manager.

-  [Pré-requisitos do site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Saiba mais sobre as configurações que são necessárias num Servidor do Windows para suportar diferentes tipos de site e funções do sistema do site.

-  [Sistemas operativos suportados para servidores do sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Saiba quais os sistemas operativos que pode utilizar como servidor de servidor de site ou servidor de sistema de site.

-  [Sistemas operativos suportados por clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Saiba quais os sistemas operativos que pode gerir com o Gestor de Configuração, incluindo Windows, Windows Embedded, Linux e UNIX, Mac e dispositivos móveis.

-  [Sistemas operativos suportados para a consola](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Saiba quais os sistemas operativos que podem alojar a consola Do Gestor de Configuração para fornecer um ponto de acesso para gerir a sua implementação.  

-  [Suporte para versões do SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Saiba quais as versões do SQL Server que podem alojar a base de dados do site e a base de dados de relatórios, bem como sobre configurações e configurações opcionais que pode utilizar.

-  [Opções de alta disponibilidade](../../servers/deploy/configure/high-availability-options.md)  
Saiba mais sobre as opções que pode implementar ao projetar o seu ambiente para ajudar a manter um elevado nível de serviço disponível para a implementação do Seu Gestor de Configuração.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Saiba mais sobre as diretrizes que podem ajudá-lo a identificar o hardware e configurações certos para hospedar os seus sites de Configuração Manager e serviços chave.

-  [Suporte para domínios do Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Conheça as configurações de domínio ative diretório suportadas que o Gestor de Configuração requer e suporta.

-  [Suporte para funcionalidades e redes do Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Conheça as tecnologias suportadas pelo Windows (como branchCache e desduplicação de dados) e limitações para a sua utilização com o Gestor de Configuração.

-  [Apoio a ambientes de virtualização](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Saiba mais sobre como usar tecnologias de máquinas virtuais suportadas.
