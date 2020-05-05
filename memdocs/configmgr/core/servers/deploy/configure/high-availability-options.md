---
title: Elevada disponibilidade
titleSuffix: Configuration Manager
description: Aprenda a implementar o Gestor de Configuração utilizando opções que mantêm um elevado nível de serviço disponível.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073318"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opções de alta disponibilidade para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve como implementar o Gestor de Configuração utilizando opções que mantêm um elevado nível de serviço disponível.

As seguintes opções do Gestor de Configuração suportam alta disponibilidade:

- Configure qualquer site primário autónomo com um servidor adicional do site em modo passivo.  

- Configure um grupo de disponibilidade de Um Servidor SQL sempre em conjunto para a base de dados do site em sites primários e no site da administração central.

- Os sites suportam múltiplas instâncias de funções do sistema do site que fornecem serviços importantes aos clientes. Por exemplo, pontos de gestão e pontos de distribuição.  

- Sites de administração central e sites primários suportam a cópia de segurança da base de dados do site. A base de dados do site armazena todas as configurações para sites e clientes. Os sites numa hierarquia partilham estes dados de configuração.  

- As opções de recuperação do site incorporada podem reduzir o tempo de inatividade do servidor. Estas opções avançadas simplificam a recuperação quando se tem uma hierarquia com um site de administração central.  

- Os clientes podem remediar automaticamente as questões típicas sem intervenção administrativa.  

- Os sites geram alertas sobre clientes que não conseguem enviar dados recentes, o que alerta os administradores para potenciais problemas.  

- O Gestor de Configuração fornece vários relatórios incorporados e dashboards. Use-os para identificar problemas e tendências antes que se tornem problemas para operações de servidor estoirar ou clientes.  

O Gestor de Configuração inclui várias funcionalidades que fornecem um serviço quase em tempo real. Se estas funcionalidades forem fundamentais para satisfazer os seus requisitos de negócio, planeie e configure os seus sites e hierarquias para uma elevada disponibilidade. Por exemplo:  

- As ações de [notificação do cliente](../../../clients/manage/manage-clients.md), tais como reiniciar, iniciar os exames do Windows Defender ou desktop remoto.  

- Mensagens estatais para monitorização de funcionalidades como atualizações de software e proteção de pontos finais.

- [Scripts](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Outras funcionalidades do Gestor de Configuração não fornecem serviço em tempo real. Estas funcionalidades incluem, mas não se limitam a configurações de clientes, hardware e inventário de software, implementações de software e definições de conformidade. Espere que operem com alguma latência de dados. É incomum para a maioria dos cenários que envolvem uma interrupção temporária do serviço para se tornar um problema crítico. Para minimizar o tempo de inatividade, manter a autonomia das operações e fornecer um elevado nível de serviço, configurar os seus sites e hierarquias com elevada disponibilidade em mente.  

Por exemplo, os clientes do Gestor de Configuração normalmente operam de forma autónoma utilizando horários e configurações conhecidas para operações, e horários para submeter dados ao site para processamento.  

- Quando os clientes não podem contactar o site, eles cache dados a serem submetidos até que possam entrar em contato com o site.  

- Os clientes que não podem contactar o site continuam a operar. Utilizam os últimos horários conhecidos e informações em cache, até poderem contactar o site e receber novas políticas. Por exemplo, um cliente pode manter uma aplicação previamente descarregada que deve executar ou instalar.

- O site monitoriza os seus sistemas de sites e clientes para atualizações periódicas de estado. Pode gerar alertas quando estes componentes não se registam.  

- Os relatórios incorporados fornecem informações sobre operações em curso, operações históricas e tendências atuais. O Gestor de Configuração também suporta mensagens baseadas no Estado que fornecem informações quase em tempo real para operações em curso.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>Alta disponibilidade para sites e hierarquias  

### <a name="use-a-site-server-in-passive-mode"></a>Utilize um servidor de site em modo passivo

Instale um servidor de site adicional em modo *passivo* para um local primário autónomo. O servidor do site em modo passivo é além do servidor do site existente no modo *ativo.* Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Para mais informações, consulte a elevada disponibilidade do [servidor do Site](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Utilize uma biblioteca de conteúdos remotos

Mova a biblioteca de conteúdos do site para um local remoto que forneça armazenamento altamente disponível. Esta funcionalidade é um requisito para a elevada disponibilidade do servidor do site. Para mais informações, consulte a biblioteca de [conteúdos.](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)

### <a name="centralize-content-sources"></a>Centralizar fontes de conteúdo

Todos os conteúdos de software no 'Gestor de Configuração' requerem uma localização de origem de pacote na rede. Utilize armazenamento centralizado e altamente disponível para alojar uma localização comum de origem de pacote para todos os conteúdos.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Use um grupo de disponibilidade de servidor SQL sempre em conjunto para hospedar a base de dados do site

Hospedar a base de dados do site em sites primários e o site da administração central em grupos de disponibilidade SQL Server Always On. Para mais informações, consulte [o SQL Server Always On para obter uma base de dados de site altamente disponível](sql-server-alwayson-for-a-highly-available-site-database.md).  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Utilize um cluster de Servidor SQL para alojar a base de dados do site

Quando utiliza um cluster SQL Server para a base de dados de um site de administração central ou de um site primário, utiliza o suporte fail-over incorporado no Servidor SQL.  

Os sites secundários não podem usar um cluster SQL Server, e não suportam cópiade segurança ou restauro da base de dados do site. Recupere um local secundário reinstalando o local secundário a partir do local primário dos pais.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Implementar uma hierarquia de sítios com um site de administração central, e um ou mais locais primários infantis

Esta configuração pode fornecer tolerância a falhas quando os seus sites gerem segmentos sobrepostos da sua rede. Também oferece uma opção adicional de recuperação para usar a informação na base de dados partilhada disponível em outro site, para reconstruir a base de dados do site no site recuperado. Utilize esta opção para substituir uma cópia de segurança falhada ou indisponível da base de dados do site falhado.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Criar backups regulares em sites de administração central e locais primários

Ao criar e testar uma cópia de segurança regular do site, esta certifica-se de que tem os dados necessários para recuperar um site. Também pratica a recuperação de um site no mínimo de tempo.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Instale várias instâncias de funções do sistema do site

Ao instalar várias instâncias de funções críticas do sistema do site, fornece pontos de contacto redundantes para os clientes. Por exemplo, vários pontos de gestão e pontos de distribuição fornecem um serviço redundante no caso de um servidor específico estar offline.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Instale várias instâncias do Fornecedor sms num site

O Provedor SMS fornece o ponto de contacto administrativo para uma ou mais consolas do Gestor de Configuração. Para fornecer redundância para pontos de contacto para administrar o seu site e hierarquia, instale vários Fornecedores de SMS.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>Alta disponibilidade para funções do sistema do site

Em cada site, implementa funções do sistema do site para fornecer os serviços que pretende que os clientes utilizem nesse site. A base de dados do site contém as informações de configuração para o site e para todos os clientes. Utilize uma ou mais opções disponíveis para fornecer uma elevada disponibilidade da base de dados do site e a recuperação da base de dados do site e do site, se necessário.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundância para importantes funções do sistema do site

- Ponto de serviço web de catálogo de aplicações  

- Ponto de site do catálogo de aplicações  

- Ponto de distribuição  

- Ponto de gestão  

- Ponto de atualização de software  

- Ponto de Migração de Estado  

Para fornecer redundância para reporte em sites e clientes, instale várias instâncias do ponto de serviços de reporte.

Para suporte de failover com o ponto de atualização de software, utilize o Windows PowerShell para instalar esta função num cluster de equilíbrio de carga de rede Windows (NLB).  

### <a name="built-in-site-backup"></a>Backup do site incorporado

O Gestor de Configuração inclui uma tarefa de backup incorporada para ajudá-lo a fazer backup do seu site e informações críticas num horário regular. Além disso, o assistente de configuração do Gestor de Configuração suporta as ações de restauro do local para ajudá-lo a restaurar um site para operações.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publicação para Serviços de Domínio de Diretório Ativo e DNS

Configure cada site para publicar dados sobre o site para Ative Directory Domain Services e DNS. Esta publicação permite aos clientes identificar o servidor mais acessível da rede. Os clientes também o utilizam para identificar quando estão disponíveis novos servidores do sistema de sites para fornecer serviços importantes, como pontos de gestão.  

### <a name="sms-provider-and-configuration-manager-console"></a>Consola de Gestor de SMS e Configuração

O Gestor de Configuração suporta a instalação de vários Fornecedores de SMS em servidores separados como múltiplos pontos de acesso para a consola. Se um servidor do SMS Provider estiver offline, ainda pode visualizar e gerir sites e clientes.  

Quando uma consola de Configuração Manager se conecta a um site, conecta-se a uma instância do Fornecedor SMS desse site. A instância do Fornecedor SMS é selecionada aleatoriamente. Se o Fornecedor SMS selecionado não estiver disponível, tem as seguintes opções:  

- Religue a consola ao site. Cada novo pedido de ligação é atribuído aleatoriamente uma instância do Provedor de SMS. É possível que a nova ligação seja atribuída a uma instância disponível.  

- Ligue a consola a um site diferente do Gestor de Configuração e gerencie a configuração a partir dessa ligação. Esta opção introduz um ligeiro atraso nas alterações de configuração não superior estivados por alguns minutos. Depois de o Fornecedor SMS para o site estar on-line, religue a consola do Gestor de Configuração diretamente ao site que pretende gerir.  

Instale a consola 'Gestor de Configuração' em vários computadores para utilização por administradores. Cada Fornecedor SMS suporta ligações de mais de uma consola.  

### <a name="management-point"></a>Ponto de gestão

Instale vários pontos de gestão em cada site primário e permita que os sites publiquem dados do site para a sua infraestrutura de Diretório Ativo e para o DNS.  

Vários pontos de gestão ajudam a equilibrar a utilização de qualquer ponto de gestão único por vários clientes. Considere também a instalação de uma ou mais réplicas de base de dados para pontos de gestão. Esta configuração diminui as operações intensivas do processador do ponto de gestão. Também aumenta a disponibilidade deste papel crítico do sistema do site.  

Os sites secundários apenas suportam a instalação de um ponto de gestão, que deve estar localizado no servidor do site secundário. Os pontos de gestão em sites secundários não são considerados como tendo uma configuração altamente disponível.  

> [!NOTE]  
> Os dispositivos geridos pela gestão de dispositivos móveis no local ligam-se a apenas um ponto de gestão num local primário. O ponto de gestão é atribuído pelo Gestor de Configuração ao dispositivo móvel durante a inscrição e, em seguida, não muda. Quando instala vários pontos de gestão e permite mais de um para dispositivos móveis, o ponto de gestão atribuído a um cliente de dispositivo móvel não é determinista.  
>
> Se o ponto de gestão que um cliente de dispositivo móvel utiliza ficar indisponível, deve resolver o problema com esse ponto de gestão ou limpar o dispositivo móvel e reinscrever o dispositivo móvel para que possa ser atribuído a um ponto de gestão operacional que esteja ativado para dispositivos móveis.  

### <a name="distribution-point"></a>Ponto de distribuição

Instale vários pontos de distribuição e implemente conteúdo em vários pontos de distribuição. Adicione mais de um ponto de distribuição por grupo de limites para garantir que os clientes obtêm várias opções no seu pedido de conteúdo. Configure as relações de grupo de fronteira para que tenham um comportamento predivel de recuo para outro grupo de fronteira ou ponto de distribuição de nuvem. Para mais informações, consulte [os grupos de fronteira configure](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Ponto de serviço web de catálogo de aplicações e ponto de site do catálogo de aplicações

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Instale mais de uma instância de cada função do sistema do site. Para um melhor desempenho, implemente um de cada um no mesmo servidor do sistema de site.  

Cada função do sistema de catálogo de aplicações fornece as mesmas informações que outras instâncias dessa função, independentemente da sua localização na hierarquia. Quando um cliente faz um pedido para o catálogo de aplicações, e configuraos clientes para detetar automaticamente o ponto de catálogo de aplicações predefinido, o cliente é direcionado para uma instância disponível. Os clientes preferem instâncias de catálogo de aplicações locais, com base na localização atual da rede do cliente.  

Para obter mais informações sobre esta definição de cliente e como funciona a deteção automática, consulte as definições do cliente [do Agente Informático.](../../../clients/deploy/about-client-settings.md#computer-agent)  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>Alta disponibilidade para clientes  

### <a name="client-operations-are-autonomous"></a>As operações dos clientes são autónomas

A autonomia do cliente do Gestor de Configuração inclui os seguintes comportamentos:  

- Os clientes não requerem contacto contínuo com servidores específicos do sistema do site. Usam configurações conhecidas para realizar ações pré-configuradas num horário.  

- Os clientes podem usar qualquer instância disponível de uma função do sistema de site que presta serviços aos clientes. Tentam contactar servidores conhecidos até localizarem um servidor disponível.  

- Os clientes podem executar inventário, implementações de software e ações programadas semelhantes independentes do contacto direto com servidores do sistema do site.  

- Os clientes que estejam configurados para usar um ponto de estado de recuo podem submeter detalhes ao ponto de estado de recuo quando não conseguem comunicar com um ponto de gestão.  

### <a name="clients-can-repair-themselves"></a>Os clientes podem reparar-se

Os clientes remediam automaticamente as questões mais típicas sem intervenção administrativa direta.  

- Periodicamente, os clientes autoavaliam o seu estado. Tomam medidas para remediar os problemas típicos utilizando uma cache local de medidas de reparação e ficheiros de origem para reparações.  

- Quando um cliente não envia informações de estado para o seu site, o site pode gerar um alerta. Os utilizadores administrativos que recebem estes alertas podem tomar medidas imediatas para restabelecer o normal funcionamento do cliente.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Informações de cache dos clientes para usar no futuro

Quando um cliente comunica com um ponto de gestão, o cliente pode obter e cache as seguintes informações:  

- Definições do cliente  

- Horários dos clientes  

- Informações sobre implementações de software e um download do software que o cliente está programado para instalar, quando a implementação estiver configurada para esta ação.  

Quando um cliente não pode contactar um ponto de gestão, os clientes localmente cache o estado, estado e informação do cliente que reportam ao site. O cliente transfere estes dados depois de estabelecer contacto com um ponto de gestão.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>O cliente pode submeter o estado a um ponto de estado de recuo

Quando configura um cliente para utilizar um ponto de estado de recuo, fornece um ponto de contacto adicional para o cliente apresentar detalhes importantes sobre o seu funcionamento. Os clientes que estão configurados para usar um ponto de estado de recuo continuam a enviar o status sobre as suas operações para o papel do sistema do site mesmo quando o cliente não consegue comunicar com um ponto de gestão.  

### <a name="central-management-of-client-data-and-client-identity"></a>Gestão central dos dados dos clientes e identidade do cliente

A base de dados do site, em vez de cada cliente, retém informações importantes sobre a identidade de cada cliente, e associa esses dados a um computador ou utilizador específico.  

- Os ficheiros de origem do cliente num computador podem ser desinstalados e reinstalados sem afetar os registos históricos do computador onde o cliente está instalado.  

- A falha de um computador cliente não afeta a integridade da informação armazenada na base de dados. Esta informação pode permanecer disponível para reporte.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a>Opções para sites e funções do sistema de site que não estão altamente disponíveis

Vários sistemas de sites não suportam múltiplas instâncias num local ou na hierarquia. Esta informação pode ajudá-lo a preparar estes sistemas de sites offline.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Ponto de sincronização da inteligência patrimonial (hierarquia)

Esta função do sistema do site não é considerada crítica da missão e fornece funcionalidade opcional no Gestor de Configuração. Se este sistema de site ficar offline, utilize uma das seguintes opções:  

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor.  

### <a name="endpoint-protection-point-hierarchy"></a>Ponto de proteção do ponto final (hierarquia)

Esta função do sistema do site não é considerada crítica da missão e fornece funcionalidade opcional no Gestor de Configuração. Se este sistema de site ficar offline, utilize uma das seguintes opções:  

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor.  

### <a name="enrollment-point-site"></a>Ponto de inscrição (site)

Esta função do sistema do site não é considerada crítica da missão e fornece funcionalidade opcional no Gestor de Configuração. Se este sistema de site ficar offline, utilize uma das seguintes opções:  

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor.  

### <a name="enrollment-proxy-point-site"></a>Ponto de procuração de inscrição (site)

Esta função do sistema do site não é considerada crítica da missão e fornece funcionalidade opcional no Gestor de Configuração. No entanto, pode instalar várias instâncias deste papel no sistema do site num site e em vários locais da hierarquia. Se este sistema de site ficar offline, utilize uma das seguintes opções:  

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor.  

Quando tiver mais de um servidor proxy de inscrição num site, utilize um pseudónimo DNS para o nome do servidor. Quando utiliza esta configuração, o Robin redondo DNS proporciona alguma tolerância à falha e equilíbrio de carga para quando os utilizadores matriculam os seus dispositivos móveis.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Ponto de estado de recuo (site ou hierarquia)

Esta função do sistema do site não é considerada crítica da missão e fornece funcionalidade opcional no Gestor de Configuração. Se este sistema de site ficar offline, utilize uma das seguintes opções:  

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor. Uma vez que os clientes recebem o ponto de estado de recuo durante a instalação do cliente, é necessário modificar os clientes existentes para utilizar o novo servidor do sistema do site.  

### <a name="service-connection-point-hierarchy"></a>Ponto de ligação ao serviço (hierarquia)

Embora esta função do sistema do site seja fundamental para manter o atual ramo do Gestor de Configuração atualizado, geralmente não é usado com frequência. Se este sistema ficar offline, utilize uma das seguintes opções:

- Resolva a razão para o sistema do site estar offline.  

- Desinstale a função a partir do servidor atual e instale a função num novo servidor.  


## <a name="see-also"></a>Consulte também

- [Configurações suportadas](../../../plan-design/configs/supported-configurations.md)  

- [Hardware recomendado](../../../plan-design/configs/recommended-hardware.md)  

- [Sistemas operativos suportados para servidores do sistema de sites](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Pré-requisitos do site e sistema de sites](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Impactos de falha do site](../../manage/site-failure-impacts.md)  
