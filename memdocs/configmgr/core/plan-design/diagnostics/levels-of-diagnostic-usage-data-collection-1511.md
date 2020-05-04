---
title: Dados de diagnóstico para 1511
titleSuffix: Configuration Manager
description: Conheça os níveis de diagnóstico e dados de utilização que a versão 1511 do Gestor de Configuração recolhe.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eaebab1e3c03ad2ffbcebf57bbccf88ce151923e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715600"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Níveis de recolha de dados de utilização de diagnóstico para a versão 1511 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A versão 1511 do Gestor de Configuração recolhe três níveis de diagnóstico e dados de utilização: **Básico,** **Melhorado**e **Completo**. Por predefinição, esta funcionalidade está definida no nível Avançado. As seguintes secções fornecem detalhes adicionais sobre os dados que cada nível recolhe.  

> [!IMPORTANT]  
>  O Gestor de Configuração não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis Básico ou Melhorado. Qualquer recolha desta informação no nível Completo não é propositada, isto é, potencialmente incluída em informações avançadas de diagnóstico, como ficheiros de registo ou instantâneos de memória. A Microsoft não utilizará estas informações para identificá-lo, contactá-lo ou desenvolver publicidade.  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Como alterar o nível  
 Os administradores que tenham um âmbito administrativo baseado em funções que inclua **modificar** permissões na classe de objetos **do Site** podem alterar o nível de dados recolhidos nas definições de Dados de Diagnóstico e Utilização na consola do Gestor de Configuração.

 Para tal, na consola, vá ao separador dos bastidores (o separador superior esquerdo com a seta de dropdown), selecione Dados de **Utilização**e, em seguida, selecione o nível de dados que pretende utilizar.  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nível 1 - Básico  
 O nível Básico inclui dados sobre a sua hierarquia, dados que são necessários para ajudar a melhorar a sua experiência de instalação ou upgrade, e dados que ajudam a determinar as atualizações do Gestor de Configuração aplicáveis à sua hierarquia.  

 Começando com a versão 1511 do Gestor de Configuração, este nível inclui o seguinte:  


-   Informações de configuração
    - Construir, instalar tipo, pacotes de idiomas e funcionalidades que permitiu

    - Atualizar o estado de implementação do pacote e os erros  

-   Métricas de desempenho da base de dados (informações de processamento de replicação, procedimentos armazenados por processador e utilização do disco)  

-   Configuração básica da base de dados (processadores, configuração de cluster e configuração de vistas distribuídas)  

-   Esquema de base de dados do Gestor de Configuração (hash de todas as definições de objeto)  

-   Contagem de versões de clientes do Gestor de Configuração e versões do sistema operativo  

-   Contagem dos sistemas operativos para dispositivos e políticas geridos definidos pelo Conector de Intercâmbio  

-   Conde de línguas e locais de cliente

-   Contagem de dispositivos Windows 10 por ramo e compilação  

-   Dados da hierarquia do site do Gestor de Configuração Básica (lista de site, tipo, versão, estado, contagem de clientes e fuso horário)  

-   Informação básica do servidor do sistema do site (funções do sistema do site utilizadas, estado da Internet e SSL, sistema operativo, processadores e máquina física ou virtual)  

-   Estatísticas básicas de descoberta do utilizador (contagem de descobertas do utilizador e tamanhos mínimo/máximo/médio do grupo)  

-   Informações básicas de proteção do ponto final (versões de cliente antimalware)  

-   Contagens básicas de aplicações e implementação (aplicações totais, aplicações totais com vários tipos de implementação, aplicações totais com dependências, aplicações supersed totais e contagem de tecnologias de implementação em uso)  

-   Contagens básicas de implantação do sistema operativo (OSD) (imagens)  

-   Tipos de pontos de distribuição e pontos de gestão e informações básicas de configuração (protegidas, pré-encenadas, PXE, multicast, estado SSL, pontos de distribuição pull/peer, ativados por MDM, ativados por SSL, etc.)  

-   Estatísticas de telemetria (quando executado, tempo de execução e erros)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nível 2 - Avançado  
O nível melhorado é o padrão após os acabamentos de configuração. Este nível inclui dados recolhidos no nível Básico, dados específicos de funcionalidades (frequência e duração da utilização), configurações do cliente do Gestor de Configuração (nome do componente, estado e certas configurações, como intervalos de votação), e informações básicas sobre atualizações de software).  

Este nível é recomendado porque fornece à Microsoft os dados mínimos necessários para fazer melhorias úteis em futuras versões de produtos e serviços. Este nível não recolhe nomes de objetos (sites, utilizadores, computadores ou objetos), detalhes sobre objetos relacionados com a segurança ou vulnerabilidades como contagens de sistemas que requerem atualizações de software.  

Começando com a versão 1511 do Gestor de Configuração, este nível inclui o seguinte:  

-   **Gestão de aplicações:**  

    -   Informações básicas de utilização/segmentação para tipos de implementação que são utilizados dentro da organização (utilizador versus dispositivo direcionado e necessário versus disponível)  

    -   Informações de implementação de aplicações (instalação/desinstalação, requer aprovação e interação do utilizador ativada/desativada)  

    -   Estatísticas de pedidos de aplicação disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicações por sistema operativo  

    -   Contagem de implementações de pacote/programa  

    -   Contagem de ambientes de App-V e propriedades de implementação  

    -   Contagem de licenças de aplicação licenciadas para Windows 10  

    -   Número máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo  

    -   Tipo e duração da janela de manutenção  

-   **Cliente:**  

    -   Lista/contagem de agentes de cliente ativados  

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem  

    -   Contagem de falhas de instalação de cliente  

-   **Definições de conformidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    -   Contagem de implementações que referenciam definições incorporadas (valor da definição não é capturada)  

    -   Contagem de regras e implementações que são criadas para configurações personalizadas  

    -   Contagem de modelos de protocolo de inscrição de certificado simples implantados  

-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações de grupo de fronteiras (contagem de fronteiras e sistemas de sites que são atribuídos a cada grupo de fronteiras)  

    -   Informações do grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  

    -   Informação de configuração de pontos de distribuição (utilização de cache de ramo e monitorização de pontos de distribuição)  

    -   Informação de configuração do Gestor de Distribuição (linhas, atraso de retry, número de repetições e definições de ponto de distribuição)  

-   **Proteção do ponto final:**  

    -   Utilização da política de proteção de pontos finais e de firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br />Isto não inclui qualquer informação sobre as definições incluídas na política.  

    -   Erros de implementação de proteção de pontos finais (contagem dos códigos de erro de implementação da política de proteção do ponto final)  

    -   Contagem de coleções selecionadas para aparecer no painel de proteção de ponto final  

    -   Contagem de alertas configurados para a função de Proteção de Pontofinal  

-   **Gestão de aplicações móveis (MAM):**  

    -   Contagem de aplicações do Office ativadas pelo MAM, aplicações de linha de negócio e políticas por sistema operativo  

    -   Contagem de implementações de aplicações/política de MAM  

    -   Contagem de regras que são criadas por definição de MAM  

-   **Gestão de dispositivos móveis (MDM):**  

    -   Contagem de ações de dispositivos móveis emitidas: lock, pin rest, wipe, and retire commands

    -   Contagem de dispositivos móveis geridos pelo Gestor de Configuração e Microsoft Intune e como foram matriculados (a granel ou baseados no utilizador)  

    -   Horário de sondagens de dispositivomóvel e estatísticas para verificação de dispositivos móveis  

    -   Contagem de políticas de dispositivos móveis  

    -   Contagem de utilizadores que tenham vários dispositivos móveis matriculados  

-   **Microsoft Intune resolução de problemas:**  

    -   Contagem e dimensão do estado, estado, inventário, RDR, DDR, UDX, Estado inquilino, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM e mensagens de conformidade que são descarregadas a partir do Microsoft Intune  

    -   Contagem e tamanho das ações do dispositivo (limpeza, aposentadoria, bloqueio), telemetria e mensagens de dados que são replicadas para Microsoft Intune  

    -   Estatísticas completas e delta de sincronização dos utilizadores para o Microsoft Intune  

-   **Gestão de dispositivos móveis (MDM) no local:**  

    -   Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  

    -   Contagem de pacotes e perfis de inscrição em massa do Windows 10  

-   **Implantação do sistema operativo:**  

    -   Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

-   **Atualizações de software:**  

    -   Número total/médio de coleções que têm implementações de atualizações de software e o número máximo/médio de atualizações implementadas  

    -   Número de regras de implantação automática ligadas à sincronização  

    -   Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente  

    -   Deltas disponíveis e prazos que são usados em regras de implementação automática  

    -   Número médio e máximo de atribuições por atualização  

    -   Contagem de atualizações criadas e implementadas com o System Center Update Publisher  

    -   Contagem de grupos de atualização e atribuições  

    -   Contagem dos pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são direcionados com pacotes  

    -   Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo  

    -   Número de atualizações e percentagem de atualizações que são implementadas, expiradas, sobrecarregadas, descarregadas e contêm EULAs  

    -   Atualizar códigos de erro de análise e contagem de máquinas  

    -   Avaliação de atualização de cliente e agendas de análise  

    -   Agenda de sincronização de ponto de atualização de software  

    -   Número de regras de implementação automática que têm múltiplas implementações  

    -   Configurações que são usadas para planos de manutenção ativos do Windows 10  

    -   Versões de conteúdo de dashboard do Windows 10  

    -   Contagem de clientes do Windows 10 que usam a Atualização do Windows para Negócios  

    -   Estatísticas de aplicação de patches de cluster  

    -   Contagem de atualizações do Office 365 implementadas  

-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de bases de dados  

    -   Informações de réplica do SQL Always-On  

    -   Contagem de coleções por tipo  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nível 3 - Completo  
O nível completo inclui todos os dados nos níveis Básico e Melhorado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações avançadas de diagnóstico, como ficheiros do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.  

Começando com a versão 1511 do Gestor de Configuração, este nível inclui o seguinte:  

-   Estatísticas de avaliação e de atualização de coleções  

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)  

-   Configuração da política do Endpoint Protection  

-   Informações de implementação de atualizações de software (percentagem de implementações que são direcionadas com o tempo cliente versus UTC, necessárias versus opcionais versus silenciosas, e reinicialização da supressão)  

-   Compatibilidade geral das implementações de atualizações de software  

-   Informações de agenda de avaliação de regras de implementações automáticas  

-   Número de clientes que têm políticas de proteção de acesso à rede  

-   Contagens e códigos de erro de implementação de atualizações de software  

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software  

-   Contagem de grupos que expiraram atualizações de software  

-   Número máximo/mínimo/médio de atualizações de software por pacote  

-   Percentagens de êxito de análise de atualização de software  

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software  
