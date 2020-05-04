---
title: Importar dados de configuração
titleSuffix: Configuration Manager
description: Dados de configuração de importação se estiver em formato de ficheiro de armário e aderir ao esquema de linguagem de modelação de serviço suportado.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4f70a956051858fce5b4ba5f519c7e1035600793
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712310"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Dados de configuração de importação com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Além de criar linhas de base de configuração e itens de configuração na consola do Gestor de Configuração, pode importar dados de configuração se estiver contido num formato de ficheiro (.cab) do armário e aderir ao esquema de linguagem de modelação de serviço suportado (SML). Pode importar dados de configuração a partir de:  

- Dados de configuração de melhores práticas (Pacotes de Configuração) transferidos da Microsoft ou de outros sites de fornecedores de software.  

- Dados de configuração que foram exportados do System Center 2012 Configuration Manager e posteriormente.  

- Dados de configuração que foram da autoria externa e que estão em conformidade com o esquema SML.  

  Para obter um exemplo de Pacote de Configuração que ajude a gerir a conformidade para funções de servidor de site do System Center 2012 Configuration Manager, consulte [Pacote de Configuração do System Center 2012 Configuration Manager](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Quando importar uma linha de base de configuração, alguns ou todos os itens de configuração referenciados na linha de base de configuração também podem ser incluídos no ficheiro CAB. Durante o processo de importação, o Gestor de Configuração verifica que todos os itens de configuração referenciados na linha de base de configuração também estão incluídos no ficheiro do gabinete ou já existem no site do Gestor de Configuração. O processo de importação falha se tentar importar uma linha de base de configuração que referencia os dados de configuração que o Gestor de Configuração não consegue localizar.  

Outros cenários em que o processo de importação poderá falhar incluem os seguintes:  

-   Os dados de configuração referem dados de configuração que o Gestor de Configuração não consegue localizar, quer na sua base de dados quer no próprio ficheiro do gabinete.  

-   Os dados de configuração já estão presentes na base de dados do Gestor de Configuração com o mesmo nome e versão de dados de configuração, mas a versão de conteúdo difere.  

-   Os dados de configuração já estão presentes na base de dados do Gestor de Configuração com a mesma versão de conteúdo, mas o cálculo do hash identifica-os como sendo diferentes.  

-   Uma versão mais recente dos dados de configuração com o mesmo nome já está presente ou foi recentemente eliminada na base de dados do Gestor de Configuração.  

-   Numa hierarquia multi-site do Gestor de Configuração, os dados de configuração foram originalmente importados de um site-mãe. Tem de atualizá-los a partir do mesmo site e não de um site subordinado.  

### <a name="import-configuration-data"></a>Importar dados de configuração  

1.  Na consola do Gestor de Configuração, clique em Itens de**Configuração** **de Ativos e Conformidade** > ou **linhas de base de configuração**
2.  No separador **Home,** no grupo **Criar,** clique em Dados de **Configuração de Importação**.  
3.  Na página **Selecionar Ficheiros** do **Assistente de Importação de Dados de Configuração**, clique em **Adicionar**e, na caixa de diálogo **Abrir** , selecione os ficheiros .cab que pretende importar.  
4.  Selecione a Create uma nova cópia das linhas de base de **configuração importadas e itens** de configuração verificar caixa se quiser que os dados de configuração importados sejam editáveis na consola Do Gestor de Configuração.  
5.  Na página **Resumo,** reveja as ações que serão tomadas e, em seguida, complete o assistente.  

Os dados de configuração importados mostram no nó de **Definições** de Conformidade do espaço de trabalho **Ativos e Compliance.**  
