---
title: Configurar sites e hierarquias
titleSuffix: Configuration Manager
description: Consulte esta lista de verificação para garantir que considera as configurações mais comuns que afetam tanto os sites como as hierarquias.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720997"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configure sites e hierarquias para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de instalar o seu primeiro site de Gestor de Configuração ou adicionar sites adicionais à sua hierarquia, utilize esta lista de verificação para garantir que considera as configurações mais comuns que afetam tanto os sites como as hierarquias.  

As seguintes notas de configuração aplicam-se à maioria das implementações:  

- Algumas opções baseiam-se umas nas outras, tais como Ative Directory Forest Discovery, fronteiras e grupos de fronteira.  

- Várias configurações têm valores padrão para usar sem alterações de configuração, pelo menos para iniciar.  

- Outras configurações, como grupos de fronteira e grupos de pontos de distribuição, exigem que as configure antes de as utilizar.  

| Ação | Detalhes |  
|------------|-------------|  
| Configurar a administração baseada em funções | Segregar atribuições administrativas para controlar quais os utilizadores administrativos que possam visualizar e gerir diferentes objetos e dados no ambiente do Seu Gestor de Configuração.<br /><br /> As configurações para a administração baseada em funções são partilhadas com todos os sites numa hierarquia.   <br/><br/>Para mais informações, consulte a [configuração da administração baseada em papéis](configure-role-based-administration.md). |  
| Publique dados do site para Serviços de Domínio de Diretório Ativo | Facilite aos clientes encontrar serviços e utilizar eficientemente os recursos do site.<br /><br /> Em primeiro [lugar, alargar o esquema de Diretório Ativo.](../../../plan-design/network/extend-the-active-directory-schema.md) Em seguida, configurar individualmente cada site para [publicar dados do site](publish-site-data.md) |  
| Configurar um ponto de ligação de serviço | Planeie instalar e configurar o ponto de ligação de serviço no local de alto nível da sua hierarquia. Para mais informações, consulte sobre o ponto de [ligação ao serviço](about-the-service-connection-point.md). |  
| Adicionar funções do sistema de sites | Instale uma ou mais funções adicionais do sistema do site para sites individuais. Para mais informações, consulte [Adicionar as funções](add-site-system-roles.md)do sistema do site . |  
| Configurar limites e grupos de limites de sites | Especifique os limites que definem as localizações da rede na sua intranet que podem conter dispositivos que pretende gerir. Em seguida, configure os grupos de fronteira para que os clientes nessas localizações de rede possam encontrar recursos do Gestor de Configuração. Para mais informações, consulte Definir os limites do [site e os grupos de fronteira.](define-site-boundaries-and-boundary-groups.md) |  
| Configurar grupos de pontos de distribuição | Configure grupos lógicos de pontos de distribuição para facilitar a gestão das implementações. Para mais informações, consulte [Gerir grupos](install-and-configure-distribution-points.md#bkmk_manage)de pontos de distribuição . |  
| Executar a deteção | Encontre a descoberta para encontrar recursos na sua rede, incluindo infraestruturas de rede, dispositivos e utilizadores.<br /><br /> Para mais informações, consulte [a Descoberta de Run.](run-discovery.md) |  
| Adicionar redundância e capacidade para administradores | Instale consolas adicionais de SMS providers e configuração para expandir a capacidade para administradores gerirem a sua infraestrutura:<br /><br /> **Instale fornecedores adicionais de SMS** para fornecer redundância para ligações de consola e API ao site. Para mais informações, consulte [Gerir o Fornecedor de SMS](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Instale consolas adicionais do Gestor** de Configuração para fornecer acesso a utilizadores administrativos adicionais. Para mais informações, consulte as [consolas do Gestor](../install/install-consoles.md)de Configuração de Instalação . |  
| Configurar componentes de site | Configure os componentes do site em cada site para modificar o comportamento das funções do sistema do site e relatórios de estado do site. Para mais informações, consulte [os componentes do Site.](site-components.md) |  
| Criar coleções personalizadas | Utilizando informações que o site descobre sobre dispositivos e utilizadores, criar coleções personalizadas de objetos para simplificar futuras tarefas de gestão. Para mais informações, consulte [Como criar coleções.](../../../clients/manage/collections/create-collections.md) |  
| Configurar definições para gerir implementações de alto risco | Configure as definições num site para alertar os administradores quando criam uma implementação de alto risco. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Configurar réplicas de bases de dados para pontos de gestão | Configure uma réplica de base de dados para reduzir a carga do processador que é colocada no servidor de base de dados do site por pontos de gestão, uma vez que eles serviço saem pedidos dos clientes. Para mais informações, consulte réplicas de Base de [Dados para pontos](database-replicas-for-management-points.md)de gestão . |  
| Configure um servidor SQL sempre em grupo de disponibilidade | Configure os grupos de disponibilidade como soluções de alta disponibilidade e recuperação de desastres para hospedar a base de dados do site em locais primários e no site da administração central. Para mais informações, consulte [o SQL Server AlwaysOn para obter uma base de dados de site altamente disponível](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Modificar a replicação entre sites | Consulte [as transferências de Dados entre sites](../../../plan-design/hierarchy/data-transfers-between-sites.md) para conhecer os seguintes assuntos:<br /><br /> Configure [a replicação baseada em ficheiros](../../../plan-design/hierarchy/file-based-replication.md) entre sites secundários<br /><br /> Configurar links de [replicação de bases](../../../plan-design/hierarchy/database-replication.md) de dados<br /><br /> Configurar [vistas distribuídas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Configure servidores de site em modo passivo | A partir da versão 1806, configure um servidor de site em modo passivo para cada site primário e o site da administração central. Esta funcionalidade fornece um servidor de site altamente disponível. Para mais informações, consulte a elevada disponibilidade do [servidor do Site](site-server-high-availability.md). |  
