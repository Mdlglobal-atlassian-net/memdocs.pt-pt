---
title: Fundamentos da gestão do cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre as tarefas que executa para gerir os clientes do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722866"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Fundamentos das tarefas de gestão do cliente para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de instalar os clientes do Gestor de Configuração, existem várias tarefas que executa para gerir os clientes.  Algumas das tarefas são executadas a partir da consola 'Gestor de Configuração'. Outras tarefas são executadas a partir da aplicação cliente do Gestor de Configuração. A aplicação cliente do Gestor de Configuração está instalada com o software cliente do Gestor de Configuração.

## <a name="configuration-manager-console-tasks"></a>Tarefas de consola de Gestor de Configuração
 Na consola 'Gestor de Configuração', pode executar várias tarefas de gestão de clientes:  

-   Implementar aplicações, atualizações de software, scripts de manutenção e sistemas operativos. Configure a instalação para uma data e hora específicas, disponibilize o software para os utilizadores instalarem quando estes são solicitados, ou configure as aplicações para serem desinstaladas.  

-   Ajudar a proteger os computadores contra software maligno e ameaças à segurança, e receber notificações quando forem detetados problemas.  

-   Defina as definições de configuração do cliente que pretende monitorizar e remediar se estas estiverem fora de conformidade.  

-   Recolher informações do inventário de hardware e software, o que inclui a monitorização e a reconciliação das informações de licença da Microsoft.  

-   Resolver problemas de computadores utilizando o controlo remoto.  

-   Implementar definições de gestão de energia para gerir e monitorizar o consumo de energia dos computadores.  

A consola Do Gestor de Configuração monitoriza as tarefas anteriores em tempo real. Informações de notificação e estado para cada tarefa estão disponíveis na consola 'Gestor de Configuração'. Para capturar dados e tendências históricas, utilize as capacidades integradas de reporte dos Serviços de Reporte de Servidores SQL. Os clientes enviam detalhes para o site como o estado do cliente.  A informação sobre o estado do cliente fornece dados sobre a saúde da atividade do cliente e cliente, e é visualizada na consola ou utilizando os relatórios incorporados para O Gestor de Configuração. Estes dados ajudam a identificar computadores que não estão a responder e, em alguns casos, os problemas são automaticamente remediados.  

 Para obter mais informações sobre tarefas de gestão para clientes, consulte [Como gerir clientes](../../core/clients/manage/manage-clients.md) e como gerir clientes para [servidores Linux e UNIX](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para obter mais informações sobre como utilizar relatórios, consulte   
            [Introdução à reportagem.](../../core/servers/manage/introduction-to-reporting.md)  

## <a name="configuration-manager-client-application"></a>Aplicação de cliente do Gestor de Configuração  
 Quando instala o software cliente do Gestor de Configuração, a aplicação do cliente do Gestor de Configuração também está instalada. Ao contrário do Software Center, a aplicação do cliente Do Gestor de Configuração foi concebida para o balcão de ajuda e não para o utilizador final. Algumas opções de configuração requerem permissões administrativas locais, e a maioria das opções requerem conhecimentos técnicos sobre como funciona a aplicação do cliente do Gestor de Configuração. Pode utilizar esta aplicação para efetuar as seguintes tarefas num cliente:  

-   Veja propriedades sobre o cliente, como o número de construção, o seu site atribuído, o ponto de gestão com que está a comunicar, e se o cliente está a usar um certificado de infraestrutura de chave pública (PKI) ou um certificado auto-assinado.  

-   Confirme que o cliente descarregou com sucesso uma política de cliente após a instalação do cliente pela primeira vez. Confirme também que as definições do cliente estão ativadas ou desativadas como esperado, de acordo com as definições do cliente que estão configuradas na consola Do Gestor de Configuração.  

-   Inicie as ações dos clientes. Por exemplo, faça o download da política do cliente se houver uma recente alteração de configuração na consola do Gestor de Configuração, e não pretende esperar até à próxima hora programada.  

-   Atribuir manualmente um cliente a um site do Gestor de Configuração ou tentar encontrar um site. Em seguida, especifique o sufixo do Sistema de Nome de Domínio (DNS) para os pontos de gestão que publicam no DNS.  

-   Configure a cache do cliente que armazena temporariamente ficheiros. Em seguida, apague ficheiros na cache se necessitar de mais espaço em disco para instalar o software.  

-   Configurar as definições da gestão de clientes baseada na Internet.  

-   Ver linhas de base de configuração que foram implementadas no cliente, iniciar a avaliação de compatibilidade e ver relatórios de compatibilidade.  
