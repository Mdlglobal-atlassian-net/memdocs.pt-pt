---
title: Introdução aos relatórios
titleSuffix: Configuration Manager
description: Conheça o conjunto de ferramentas e recursos disponíveis para gerir relatórios em 'Gestor de Configuração'.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1aae76845d18d8191b6f773df5491d3a144940c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713808"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Introdução a relatórios no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Relatório em Configuração Manager fornece um conjunto de ferramentas e recursos que o ajudam a usar as capacidades avançadas de reporte dos Serviços de Reporte de Servidores SQL (SSRS) e power BI Report Server. Ambas as plataformas de reporte fornecem experiências ricas de autoria para relatórios personalizados. O reporte ajuda-o a reunir, organizar e apresentar informações sobre a riqueza de dados do Gestor de Configuração na sua organização. O Gestor de Configuração fornece muitos relatórios predefinidos nos Serviços de Informação que pode utilizar sem alterações. Pode duplicar e modificar os relatórios predefinidos para satisfazer os seus requisitos, ou pode criar relatórios personalizados.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

O SQL Server Reporting Services fornece uma gama completa de ferramentas e serviços prontos a usar para ajudá-lo a criar, implementar e gerir relatórios para a sua organização. Possui também funcionalidades de programação que lhe permitem estender e personalizar a sua funcionalidade de reporte. Reporting Services é uma plataforma de reporte baseada em servidores que fornece uma funcionalidade de reporte abrangente para diferentes tipos de fontes de dados.

O Gestor de Configuração utiliza os Serviços de Relato do Servidor SQL como a sua principal solução de reporte. A integração com o Reporting Services proporciona as seguintes vantagens:  

- Utiliza um sistema de reporte padrão da indústria para consultar a base de dados do Gestor de Configuração.  

- Exibe relatórios utilizando o Visualizador de Relatório do Gestor de Configuração ou utilizando o Report Manager, que é uma ligação baseada na Web ao relatório.  

- Fornece desempenho, disponibilidade e escalabilidade elevados.  

- Fornece subscrições de relatórios aos quais os utilizadores podem subscrever. Por exemplo, um gestor subscreve um relatório por e-mail todos os dias que detalha o estado de uma atualização de software.

- Relatórios de exportações em diferentes tipos de formatos populares.  

Para mais informações, consulte [O que é o SQL Server Reporting Services (SSRS)?](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports?view=sql-server-ver15)

## <a name="power-bi-report-server"></a>Power BI Report Server

<!-- 3721603 -->

A partir da versão 2002, integre o Power BI Report Server com relatório sinuoso de Configuração Manager. Esta integração confere-lhe uma visualização moderna e um melhor desempenho. Adiciona suporte de consola para relatórios Power BI semelhantes ao que já existe com os Serviços de Reporte de Servidores SQL. Para mais informações, consulte [Integrar com o Power BI Report Server](powerbi-report-server.md).

Power BI Report Server é um servidor de relatório no local com um portal web no qual exibe e gere relatórios. Inclui ferramentas para criar relatórios power bi, relatórios paginados, relatórios móveis e KPIs. Para mais informações, consulte [o que é o Power BI Report Server?](https://docs.microsoft.com/power-bi/report-server/get-started)

## <a name="reporting-services-point"></a>Ponto do Reporting Services

O ponto de serviços de reporte é uma função do sistema de site que adiciona num servidor que executa os Serviços de Relato do Servidor Microsoft SQL. O ponto de serviços de reporte faz as seguintes funções:

- Copia as definições de relatório do Gestor de Configuração para Serviços de Reporte
- Cria pastas de relatório com base nas categorias de relatórios
- Define a política de segurança nas pastas e relatórios do relatório. Estas políticas baseiam-se nas permissões baseadas em papéis para utilizadores administrativos do Gestor de Configuração. Num intervalo de 10 minutos, o ponto de serviços de reporte liga-se aos Serviços de Informação para reaplicar a política de segurança se a alterar.

Para obter mais informações sobre como planear e instalar um ponto de serviços de reporte, consulte os seguintes artigos:

- [Planear relatórios](planning-for-reporting.md)

- [Configurar relatórios](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Relatórios do Configuration Manager

O Gestor de Configuração fornece definições de relatório para mais de 400 relatórios em mais de 50 pastas de relatório. Durante o processo de instalação de pontos de serviços de reporte, copia-os para a pasta de relatório de raiz nos Serviços de Reporte de Servidores SQL. A consola Do Gestor de Configuração mostra os relatórios e organiza-os em subpastas com base na categoria de relatório.

Os relatórios não se propagam para cima ou para baixo na hierarquia do Diretor de Configuração. Eles correm apenas contra a base de dados do site em que os crias. Como o Gestor de Configuração replica dados globais em toda a hierarquia, você tem acesso a informação em toda a hierarquia em relatórios. Quando um relatório obtém dados de uma base de dados de site, tem acesso a dados do site atual e dos sites subordinados e aos dados globais de todos os sites da hierarquia.

Tal como outros objetos do Gestor de Configuração, um utilizador administrativo deve ter as permissões adequadas para executar ou modificar relatórios. Para executar um relatório, um utilizador administrativo tem de ter a permissão **Executar Relatório** para o objeto. Para criar ou modificar um relatório, um utilizador administrativo tem de ter a permissão **Modificar Relatório** para o objeto.

### <a name="create-and-modify-reports"></a>Criar e modificar relatórios

Para relatórios baseados em Serviços de Report, o Gestor de Configuração utiliza o Microsoft SQL Server Report Builder como a ferramenta exclusiva de autoria e edição para relatórios baseados em modelos e sql. Quando cria ou edita um relatório na consola do Gestor de Configuração, o Report Builder abre. Para mais informações, consulte [Operações e manutenção para reportagem](operations-and-maintenance-for-reporting.md).

A partir da versão 2002, para criar ou editar relatórios power BI, a consola integra-se com o Power BI Desktop. Para mais informações, consulte [create power bi reports](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Executar relatórios

Quando executa um relatório baseado em Serviços de Reporte na consola do Gestor de Configuração, o Report Viewer abre e conecta-se aos Serviços de Reportagem. Depois de especificar os parâmetros de relatório necessários, o Reporting Services obtém os dados e apresenta os resultados no visualizador. Também pode ligar ao SQL Services Reporting Services, ligar à origem de dados para o site e executar relatórios.

A partir da versão 2002, quando executa um relatório baseado em Power BI, abre no navegador web.

### <a name="report-prompts"></a>Pedidos de relatório

Pode configurar um aviso ou parâmetro de relatório quando criar ou modificar um relatório. Criar relatórios solicita limitar ou direcionar os dados que um relatório recupera. Um relatório pode conter mais do que um pedido. Certifique-se de que os nomes de aviso são únicos e contêm apenas caracteres alfanuméricos que estão em conformidade com as regras do Servidor SQL para identificadores.

Quando executa um relatório, o pedido de solicitação um valor para um parâmetro necessário. Com base no valor do parâmetro, recupera os dados do relatório. Por exemplo, a **informação do Computador para um** relatório de computador específico indica um nome de computador. Os Serviços de Reporte passam o valor especificado para uma variável definida na declaração sql do relatório.

### <a name="report-links"></a>Ligações de relatórios

As ligações de relatório no Gestor de Configuração são utilizadas num relatório de origem para fornecer fácil acesso a dados adicionais. Por exemplo, pode ligar-se a informações mais detalhadas sobre cada um dos itens do relatório fonte. Se o relatório de destino necessitar de um ou mais pedidos para a execução, o relatório de origem terá de conter uma coluna com os valores adequados para cada pedido.

O link precisa especificar o número da coluna com o valor para o pedido. Por exemplo:

- Há um relatório que lista computadores que o site descobriu recentemente.
- Liga-se a partir dele a outro relatório que lista as últimas mensagens que o site recebe para um computador específico.
- Cria o link e especifica-se que a coluna `2` no relatório de origem contém o nome do computador. Este valor é um pedido necessário para o relatório de destino.
- Executa o relatório de origem, e um ícone de ligação aparece à esquerda de cada linha de dados.
- Selecione o ícone numa linha e o Visualizador de Relatórios passa o valor na coluna especificada para essa linha como o valor rápido para o relatório de destino.

Só é possível configurar uma ligação para um relatório, e essa ligação só pode ligar-se a um único relatório de destino.

> [!WARNING]  
> Se mover um relatório de destino para uma pasta de relatórios diferente, altera a localização do relatório de destino. O Gestor de Configuração não atualiza automaticamente o link do relatório no relatório de origem com a nova localização, e o link não funcionará no relatório de origem.

## <a name="report-folders"></a>Pastas de relatórios

As pastas de relatório fornecem um método para classificar e filtrar relatórios que o Gestor de Configuração armazena nos Serviços de Reporte. As pastas de relatório são úteis quando tem muitos relatórios para gerir. Ao instalar um ponto de serviços de reporte, copia relatórios para serviços de reporte e organiza-os em mais de 50 pastas de relatório. As pastas de relatórios são só de leitura. Não pode modificá-los na consola Do Gestor de Configuração.

## <a name="report-subscriptions"></a>Subscrições de relatórios

Uma subscrição de relatório em Serviços de Informação é um pedido recorrente para entregar um relatório num momento específico ou em resposta a um evento. Especifica na subscrição um formato de ficheiro de aplicação. As subscrições são uma alternativa à execução de um relatório a pedido. Os relatórios a pedido requerem que selecione ativamente o relatório de cada vez que pretender vê-lo. Em contraste, as subscrições podem ser utilizadas para agendar e automatizar a entrega de um relatório.

Pode gerir as subscrições de relatório na consola 'Gestor de Configuração'. O servidor de relatório processa as subscrições. Distribui-as utilizando extensões de entrega que são implantadas no servidor. Por predefinição, pode criar subscrições que enviem relatórios para uma pasta partilhada ou para um endereço de correio eletrónico.

Para mais informações, consulte [Gerir as assinaturas do relatório](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Report Builder

Para relatórios baseados em Serviços de Report, o Gestor de Configuração utiliza o Microsoft SQL Server Report Builder como a ferramenta exclusiva de autoria e edição para relatórios baseados em modelos e sql. Se criar ou editar um relatório na consola do Gestor de Configuração, o Report Builder abre. Quando cria ou modifica um relatório pela primeira vez, o Report Builder instala-se automaticamente. A versão do Report Builder associada à versão instalada do SQL Server é aberta quando executa ou edita relatórios.  

 A instalação do Report Builder adiciona suporte para mais de 20 idiomas. Quando executa o Report Builder, exibe dados na linguagem do SISTEMA do computador local. Se o Report Builder não apoiar o idioma, exibe os dados em inglês. O Report Builder suporta todas as capacidades dos Serviços de Reporte de Servidores SQL, que inclui as seguintes capacidades:

- Fornece um ambiente de criação de relatórios intuitivo com um aspeto semelhante ao do Microsoft Office.  

- Oferece o layout flexível do relatório do idioma de definição de relatório SQL Server (RDL).  

- Fornece várias formas de visualização de dados, incluindo gráficos e medidores.  

- Fornece caixas de texto com formatação.  

- Exporta para o formato do Microsoft Word.  

Também pode abrir o Report Builder diretamente dos Serviços de Reporte de Servidores Da SQL.

## <a name="report-models-in-sql-server-reporting-services"></a>Modelos de relatórios no SQL Server Reporting Services

Os Serviços de Reporte SQL utilizam modelos de relatório supor que selecionam itens da base de dados do Gestor de Configuração para incluir em relatórios baseados em modelos. Quando se constrói um relatório, os modelos de relatório expõem apenas pontos de vista e itens especificados para escolher. Para criar relatórios baseados em modelos, tem de estar disponível pelo menos um modelo de relatório.

Os modelos de relatórios têm as seguintes funcionalidades:

- Dê nomes lógicos de negócios aos campos de base de dados e vistas. Para produzir relatórios, não é necessário conhecer a estrutura da base de dados do Gestor de Configuração.

- Itens de grupo logicamente.  

- Definir relações entre itens.  

- Elementos de modelo seguros para que os utilizadores administrativos possam ver apenas os dados que têm permissão para ver.

Embora o Gestor de Configuração forneça modelos de relatório de amostra, também pode definir modelos de relatório para satisfazer os seus próprios requisitos de negócio. Para obter mais informações sobre como criar modelos de relatório, consulte [Criar modelos de relatório personalizados](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Passos seguintes

[Planear relatórios](planning-for-reporting.md)
