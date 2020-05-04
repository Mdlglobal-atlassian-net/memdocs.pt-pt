---
title: Monitorizar aplicações a partir da consola
titleSuffix: Configuration Manager
description: Monitorize a implementação de software, incluindo atualizações, definições de conformidade e aplicações utilizando o espaço de trabalho de Monitorização no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710056"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Monitor aplicações da consola 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*


No 'Gestor de Configuração', pode monitorizar a implementação de todo o software, incluindo atualizações de software, definições de conformidade, aplicações, sequências de tarefas e pacotes e programas. Pode monitorizar as implementações utilizando o espaço de trabalho de **Monitorização** na consola do Gestor de Configuração ou utilizando relatórios.  

 As aplicações no Gestor de Configuração suportam a monitorização baseada no Estado, o que lhe permite rastrear o último estado de implementação de aplicações para utilizadores e dispositivos. Estas mensagens de estado apresentam informações sobre dispositivos individuais. Por exemplo, se uma aplicação for implementada para uma coleção de utilizadores, pode visualizar o estado de conformidade da implementação e o propósito de implementação na consola Do Gestor de Configuração.  

## <a name="learn-about-compliance-states"></a>Conheça os Estados de conformidade
 O estado de implementação de uma aplicação apresenta um dos seguintes estados de compatibilidade:  

-   **Bem Sucedido** – A implementação da aplicação foi bem-sucedida ou esta já está instalada.  

-   **Em curso** – A implementação da aplicação está em curso.  

-   **Desconhecido** – Não foi possível determinar o estado de implementação da aplicação. Este estado não é aplicável a implementações com um objetivo de **Disponível**. Este estado é geralmente apresentado quando ainda não tiverem sido recebidas mensagens de estado do cliente.  

-   **Requisitos Não Cumpridos** – A aplicação não foi implementada porque não era compatível com uma dependência ou uma regra de requisito ou porque o sistema operativo em que foi implementada não era aplicável.  

-   **Erro** – Falha na implementação da aplicação devido a um erro.  

Pode visualizar informações adicionais para cada estado de conformidade, incluindo subcategorias dentro do estado de conformidade e o número de utilizadores e dispositivos nesta categoria. Por exemplo, o estado de compatibilidade **Erro** inclui as seguintes subcategorias:  

- Erro na avaliação de requisitos  

- Erros relacionados com o conteúdo  

- Erros de instalação  

  Quando se aplica mais de um estado de compatibilidade à implementação de uma aplicação, é possível ver o estado agregado que representa a compatibilidade inferior. Por exemplo:  

  -   Se um utilizador fizer o sinal de dois dispositivos e a aplicação for instalada com sucesso num dispositivo, mas não tiver instalação no segundo dispositivo, o estado de implementação agregado da aplicação para esse utilizador apresenta-se como **Error**.  

  -   Se uma aplicação for implementada para todos os utilizadores que iniciarem sessão num computador, receberá vários resultados de implementação para esse computador. Se uma das implementações falhar, o estado agregado de implementação desse computador indicará **Erro**.  

O estado de implementação para implementações de pacotes e programas não é agregado.  

 Utilize estas subcategorias para o ajudar a identificar rapidamente problemas importantes relacionados com a implementação de uma aplicação. Pode também ver informações adicionais sobre os dispositivos que se enquadram numa subcategoria específica de um estado de compatibilidade.  

 A gestão de aplicações no Gestor de Configuração inclui uma série de relatórios incorporados que lhe permitem monitorizar informações sobre aplicações e implementações. Estes relatórios possuem a categoria de relatório de **Distribuição de Software - Monitorização de Aplicações**.  

 Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorize o estado de uma aplicação na consola 'Gestor de Configuração'  

1.  Na consola 'Gestor de Configuração', escolha**implementações** **de monitorização** > .  

3.  Para rever os detalhes de implementação de cada estado de conformidade e os dispositivos nesse estado, selecione uma implementação e, em seguida, no separador **Home,** no grupo **de implantação,** escolha **'Ver Status'** para abrir o painel **'Status' de implantação.** Neste painel, pode ver os ativos com cada estado de compatibilidade. Escolha qualquer ativo para visualizar informações mais detalhadas sobre o estado de implementação para esse ativo.  

    > [!NOTE]  
    >  O número de itens que podem ser apresentados no painel **Estado da Implementação** está limitado a 20 000. Se precisar de ver mais itens, utilize relatórios do 'Gestor de Configuração' para visualizar os dados do estado da aplicação.  
    >   
    >  O estado dos tipos de implementação é agregado no painel **Estado da Implementação** . Para ver informações mais detalhadas sobre os tipos de implementação, utilize o relatório **Erros da Infraestrutura da Aplicação** na categoria de relatório **Distribuição de Software - Monitorização de Aplicações**.  

4.  Para rever as informações gerais sobre uma implementação da aplicação, selecione uma implementação e, em seguida, escolha o separador **Resumo** na janela **de implantação selecionada.**  

5.  Para rever informações sobre o tipo de implementação de aplicações, selecione uma implementação e, em seguida, escolha o separador Tipos de **Implementação** na janela **de implantação selecionada.**  

A informação que é mostrada no painel de Estado de **Implementação** depois de escolher o **'Ver Status'** são dados ao vivo da base de dados do Gestor de Configuração. A informação que está mostrada no separador **Resumo** e no separador Tipos de **Implementação** são dados resumidos.

Se os dados apresentados no separador **Resumo** e no separador Tipos de **Implementação** não corresponderem aos dados apresentados no painel **'Status',** escolha **'Executar Summarization'** para atualizar os dados nestes separadores. Pode configurar o intervalo predefinido de resumo da implementação de aplicações da seguinte forma:  

1. Na consola de Gestor de Configuração, escolha**sites**de**configuração** > do site **da administração** > .

2. Na lista **de Sites,** selecione o site para o qual pretende configurar o intervalo de resumição e, em seguida, no separador **Home,** no grupo **Definições,** escolha **Resumos**de Estado .

3. Na caixa de diálogo **'Sumântes',** escolha resumo de **implementação**de aplicações , e, em seguida, escolha **Editar**.  

4. Na caixa de diálogo De implantação de **aplicações,** configurar os intervalos de resumição necessários e, em seguida, escolher **OK**.  
