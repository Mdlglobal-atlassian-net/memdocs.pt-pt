---
title: Escolha o que migrar
titleSuffix: Configuration Manager
description: Saiba quais os dados que pode migrar e quais os dados que não pode migrar para o ramo atual do Gestor de Configuração.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718918"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Determine se deve migrar dados para o ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

No ramo atual do Gestor de Configuração, a migração fornece um processo de transferência de dados e configurações que criou a partir de versões suportadas de 'Gestor de Configuração' para a sua nova hierarquia.  Pode utilizar esta funcionalidade para:  

-   Combine várias hierarquias numa só.  

-   Mova dados e configurações de uma implantação de laboratório para a sua implantação de produção.

-   Mova dados e configuração a partir de uma versão anterior do Gestor de Configuração, como O Gestor de Configuração 2007, que não tem nenhum caminho de upgrade para o ramo atual do Gestor de Configuração, ou do System Center 2012 Configuration Manager (que suporta um caminho de upgrade para o ramo atual do Gestor de Configuração).  

Com exceção da função do sistema de sites do ponto de distribuição e dos computadores que alojam pontos de distribuição, nenhuma infraestrutura (incluindo sites, funções do sistema de sites e computadores que alojam uma função do sistema de sites) migra, transfere ou pode ser partilhada entre hierarquias.  

 Embora não possa migrar a infraestrutura do servidor, pode migrar clientes do Gestor de Configuração entre hierarquias. A migração de clientes envolve a migração dos dados utilizados pelos clientes da hierarquia de origem para a hierarquia de destino e a instalação e reatribuição do software de cliente de modo a que o cliente comunique com a nova hierarquia.

Depois de instalar um cliente na nova hierarquia e o cliente apresentar os seus dados, o seu ID exclusivo do Gestor de Configuração ajuda o Gestor de Configuração a associar os dados que anteriormente emigrou com cada computador cliente.  

 A funcionalidade fornecida pela migração ajuda-o a manter os investimentos que fez em configurações e implementações, permitindo-lhe tirar o máximo partido das mudanças de núcleo no produto primeiro (que foi introduzido pela primeira vez no System Center 2012 Configuration Manager e depois continuou no Gestor de Configuração). Estas alterações incluem uma hierarquia simplificada do Gestor de Configuração que utiliza menos sites e recursos, e o processamento melhorado que vem da utilização do código nativo de 64 bits que funciona em hardware de 64 bits.  

 Para obter informações sobre as versões do Gestor de Configuração que a migração suporta, consulte [pré-requisitos para a migração.](../../core/migration/prerequisites-for-migration.md)  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>Dados que pode migrar para o ramo atual do Gestor de Configuração

A migração pode migrar a maioria dos objetos entre hierarquias apoiadas do Gestor de Configuração. As instâncias migratórias de alguns objetos de uma versão suportada do Diretor de Configuração 2007 devem ser modificadas de forma a conformar-se com o esquema do System Center 2012 Configuração Manager e formato de objeto.

Estas modificações não afetam os dados na base de dados do site de origem. Os objetos migrados de uma versão suportada do System Center 2012 Configuração Manager ou do Gerente de Configuração não requerem modificação.  

Seguem-se objetos que podem migrar com base na versão do Gestor de Configuração na hierarquia de origem. Alguns objetos, como consultas, não são migrados. Se quiser continuar a utilizar estes objetos que não são migrados, tem de os recriar na nova hierarquia. Outros objetos, incluindo alguns dados do cliente, são automaticamente recriados na nova hierarquia quando gere clientes nessa hierarquia.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Objetos que pode migrar do System Center 2012 Configuração Manager ou Configuração Manager de gestão de ramo

-   Aplicações para System Center 2012 Configuration Manager e versões posteriores  

-   App-V Ambiente Virtual do System Center 2012 Configuração Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: Para migrar coleções de uma versão suportada do System Center 2012 Configuração Manager ou Configuração Manager atual, você usa um trabalho de migração de objetos.  

-   Definições de compatibilidade:  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implementações  

-   Implementação do sistema operativo:  

    -   Imagens de arranque  

    -   Pacotes de controladores  

    -   Controladores  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa: Critérios de pesquisa guardados  

-   Atualizações de software:  

    -   Implementações  

    -   Pacotes de implementação  

    -   Modelos  

    -   Listas de atualização de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicações virtuais  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objetos que pode migrar do Gestor de Configuração 2007 SP2

-   Anúncios  

-   Aplicações para System Center 2012 Configuration Manager e versões posteriores  

-   App-V Ambiente Virtual do System Center 2012 Configuração Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: Você migra coleções de uma versão suportada do Gestor de Configuração 2007 usando um trabalho de migração de coleção.  

-   Definições de compatibilidade (designadas como gestão de configuração pretendida no Configuration Manager 2007):  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implementação do sistema operativo:  

    -   Imagens de arranque  

    -   Pacotes de controladores  

    -   Controladores  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa: Pastas de pesquisa  

-   Atualizações de software:  

    -   Implementações  

    -   Pacotes de implementação  

    -   Modelos  

    -   Listas de atualização de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicações virtuais  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>Dados que não pode migrar para o ramo atual do Gestor de Configuração

Não é possível migrar os seguintes tipos de objetos:  

-   Informações de aprovisionamento de cliente AMT  

-   Ficheiros sobre clientes, incluindo:  

    -   Dados de inventário e histórico de cliente  

    -   Ficheiros na cache do cliente  

-   Consultas  

-   Configuração Manager 2007 direitos de segurança e instâncias para o site e objetos  

-   Relatórios do Gestor de Configuração 2007 dos Serviços de Reporte de Servidores SQL  

-   Relatórios web do Gestor de Configuração 2007  

-   System Center 2012 Configuração Manager e Relatórios de Configuração do Ramo  

-   System Center 2012 Diretor de Configuração e Gestor de Configuração atual administração baseada em funções de sucursal:  

    -   Funções de segurança  

    -   Âmbitos de segurança  
