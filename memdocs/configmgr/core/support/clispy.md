---
title: Espião do Cliente
titleSuffix: Configuration Manager
description: Utilize o Client Spy para resolver problemas na distribuição de software, inventário e medição de software em clientes do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723433"
---
# <a name="client-spy"></a>Espião do Cliente

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Client Spy é uma das ferramentas do Gestor de [Configuração.](tools.md) É uma ferramenta para a distribuição de software, inventário e medidor de software em clientes do Gestor de Configuração. 

A maioria das informações obtidas pela ferramenta diz respeito a implementações de software:
- Todas as implementações de software atuais 
- Histórico de distribuição de software
- A configuração do cache do cliente
- Artigos em cache
- Pendente de implantações necessárias
- Implementações disponíveis  

Também exibe as seguintes informações de inventário
- A última data do ciclo de inventário
- A última data do relatório
- Inventário de software versões principais e menores
- Recolha de ficheiros
- Inventário de Hardware
- Coleção IDMIF
- Registos de dados de descoberta (DDRs) 

Também são apresentadas regras de medição de software. 

> [!Note]   
> Para melhorar o desempenho, a ferramenta recolhe apenas informações para cada separador quando o selecionar. Da mesma forma, ao clicar em **Refresh,** apenas atualiza as informações para o separador atualmente apresentado.



## <a name="usage"></a>Utilização


### <a name="tools-menu"></a>Menu de ferramentas

As seguintes ações estão disponíveis no menu **Ferramentas:**  

#### <a name="connect"></a>Ligar
Recuperar informações de um computador diferente.  

- Por predefinição, a ferramenta exibe informações do computador atual. 

- Conecte-se utilizando o nome do computador remoto, o nome do utilizador e a palavra-passe para a conta. A ferramenta faz uma ligação à parte do IPC$ no computador remoto. Elimina a ligação quando a ferramenta sai ou se liga a outro computador.  

- Requer uma conta com credenciais suficientes para obter a informação.  

- Se não especificar o nome de utilizador e a palavra-passe, o Client Spy utiliza o contexto de segurança do utilizador atualmente inscrito para tentar efazer a ligação.  

- Quando se liga a um computador remoto, todos os separadores que são apresentados mostram informações do computador remoto.

#### <a name="software-distribution"></a>Distribuição de Software
Exibe os separadores de Distribuição de [Software](#software-distribution) e esconde os outros separadores. Por padrão, o Client Spy exibe os separadores de Distribuição de Software.

#### <a name="inventory"></a>Inventário
Exibe o separador Inventário e esconde os outros separadores.

#### <a name="software-metering"></a>Medição de Software
Exibe o separador De medição de software e esconde os outros separadores.

#### <a name="save-current-tab-to-file"></a>Guardar o separador atual para arquivar
Guarda as informações no separador atualmente apresentado para um ficheiro de texto que especifica. 

#### <a name="save-all-tabs-to-file"></a>Guarde todos os separadores para arquivar
Guarde a informação em todos os separadores para um ficheiro de texto que especifique. Só guarda informações que a sua conta pode ver.



## <a name="software-distribution-tab"></a>Separador de distribuição de software

Configure as definições nos seguintes quatro separadores:
- [Pedidos de execução de distribuição de software](#bkmk_exec-requests)
- [Histórico de distribuição de software](#bkmk_history)
- [Informação de cache de distribuição de software](#bkmk_cache-info)
- [Distribuição de Software Execuções Pendentes](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a>Pedidos de execução de distribuição de software

Este separador apresenta todas as implementações existentes, incluindo implementações orientadas para dispositivos e utilizadores.

Cada item de árvore no separador Pedidos de Execução de Distribuição de Software contém os seguintes quatro atributos:
- Identificação do anúncio. Este valor pode estar em branco, se for uma implementação disponível. 
- ID do Pacote 
- Nome do Programa 
- O utilizador. Este pode ser o SID do utilizador visado ou o SID do utilizador que iniciou o pedido. Se ambos forem pedidos de sistema, o utilizador apresentado é sistema. 

Para cada pedido de execução, também exibe as seguintes informações numa estrutura subárvore:
- Nome do Programa 
- ID do Pacote 
- Nome do Pacote 
- Tempo de Pedido de Criação 
- Estado 
- Estado de execução, se o Estado está em execução 
- Contexto de execução (Utilizador ou Administrador) 
- Estado histórico (Sucesso, Fracasso ou NotRun) 
- LastRunTime (Nunca, se o programa não tiver sido executado antes) 
- RetryCount, se o Estado está à espera 
- ContentAccess (Contagem de retry, se o Estado está à espera de retry) 
- FalhaCódigo, se o Estado está à espera de retry 
- FalhaReason, se o Estado está à espera de retry 

Se o pedido necessitar de conteúdo, o Estado está WaitingContent. O separador informação de cache de distribuição de software mostra os detalhes para este pedido de descarregamento.

Se o pedido de execução for um pedido de descarregamento, também exibe o número de bytes descarregados.

> [!Note]   
> Utiliza diferentes ícones para diferentes estados de um pedido de execução.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a>Histórico de distribuição de software

Este separador contém informações sobre todos os programas anteriormente executados. Esta informação está armazenada no registo.

Os principais ramos desta árvore são as diferentes histórias de utilizadores, incluindo o System. Apresenta uma subárvore contendo a lista de pacotes a partir dos quais os programas foram executados para cada utilizador. 

O id do pacote e o nome do pacote para cada subárvore do pacote exibe uma lista de programas que foram executados. Apresenta os seguintes atributos para cada um: 
- Nome do programa
- Estado de execução
- Última corrida
- Código de falha
- Razão de falha  

O código de falha e a razão de falha estão em branco quando um programa foi executado com sucesso.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a>Informação de cache de distribuição de software

#### <a name="cache-config"></a>Cache Config
Contém informações sobre a cache do Cliente do Gestor de Configuração. Estas informações incluem a localização da cache, o tamanho da cache, e se está atualmente a ser utilizada. 

#### <a name="cached-items"></a>Artigos em cache
Contém uma subárvore de todos os itens atualmente na cache. Cada item de árvore inclui as seguintes informações sobre cada item: 
- Localização do item (pasta) na cache
- Estado atual
- ID do Pacote
- Nome do pacote
- Versão de pacote
- Tamanho do pacote
- Contagem de referência atual
- Última hora referenciada (UTC)  

#### <a name="downloading-items"></a>Itens de descarregamento
Estes são os itens que o cliente está atualmente a descarregar. Cada um deles mostra as mesmas informações exibidas pelos itens em cache e o número de quilobytes descarregados. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a>Distribuição de Software Execuções Pendentes

Este separador contém informações que detalham as implementações necessárias e futuras e uma lista de implementações disponíveis.

Cada ramo de árvore é para cada conta de utilizador com implementações disponíveis, incluindo o Sistema.

Para cada utilizador, uma subárvore contém os seguintes três itens:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Anúncios obrigatórios com execuções futuras
Estes são anúncios obrigatórios que ainda têm programas por executar. Estes podem ser anúncios recorrentes, únicos ou múltiplos anúncios de horários. Cada um exibe o ID de publicidade, a próxima hora de execução, e o horário em que o anúncio é executado. 

#### <a name="optional-advertisements"></a>Anúncios Opcionais
Exibe uma lista de todos os anúncios que são publicados. Também exibe detalhes como ID de publicidade, nome do programa e nome do pacote para cada um. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Anúncios obrigatórios passados sem execuções programadas futuras
Esta é uma lista de anúncios que existem no cliente que não têm futuros programas agendados para executar. O id de anúncio, nome do pacote e nome do programa são apresentados. Um item de subárvore é apresentado para quaisquer anúncios que sejam opcionais.

> [!Note]  
> As informações sobre o nome do pacote só estão disponíveis para pacotes que tenham políticas publicitadas associadas a eles no computador que está a ser visualizada. Os pacotes que já não têm políticas disponíveis que lhes estão associados exibem a mensagem "Nome de pacote já não está disponível".  



## <a name="inventory-tab"></a>Separador de inventário

Só há um separador contendo informações de inventário. A árvore principal contém os seguintes cinco itens:  

- **Inventário de Software**: Contém a data em que o último ciclo começou, a data do último relatório, e as versões menores e principais do último relatório.  

- **Recolha de Ficheiros**: Contém a data em que o último ciclo começou, a data do último relatório, e as versões menores e principais do último relatório.  

- Inventário de **Hardware**: Contém a data em que o último ciclo começou, a data do último relatório, e as versões menores e principais do último relatório.  

- **IdMIF Collection**: Contém a data em que o último ciclo começou, a data do último relatório, e as versões menores e principais do último relatório.  

- **DDR**: Contém a data em que o último ciclo começou, a data do último relatório, e as versões menores e principais do último relatório. A informação dDR também é exibida numa subárvore.



## <a name="software-metering-tab"></a>Separador de medição de software

Este separador exibe informações como uma subárvore e inclui todas as regras de medição de software. Exibe cada regra como nó, que identifica pelo nome do ficheiro e identificação da regra. Expanda cada nó na árvore e veja as seguintes informações:
- Nome do ficheiro do explorador 
- Nome de arquivo original
- ID da Regra
- Versão do ficheiro
- Idioma


