---
title: Monitorizar as definições de conformidade
titleSuffix: Configuration Manager
description: Utilize um ou mais procedimentos neste tópico para mostrar o estado de conformidade da linha de base de configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 839c08c8782a815703a19999bf1315fd65980ed8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712296"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Monitorizar as definições de conformidade no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de ter implementado as linhas de base de configuração do Gestor de Configuração para dispositivos na sua hierarquia, pode utilizar um ou mais dos procedimentos neste tópico para mostrar o estado de conformidade da linha de base de configuração:

> [!NOTE]  
>  Os campos de critérios de validação nos relatórios de definições de compatibilidade (o equivalente no relatório do lado do cliente **Restrições**) apresentam o Service Modeling Language (SML). Isto pode dificultar aos administradores que tenham sido autores do item de configuração na consola do Gestor de Configuração para entender quais são os critérios de validação se não tiverem conhecimento do SML. Neste caso, utilize o espaço de trabalho **de Monitorização** na consola Do Gestor de Configuração para visualizar as propriedades do item de configuração e os seus critérios de validação.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver os resultados de compatibilidade na consola do Configuration Manager  
 Utilize este procedimento para visualizar detalhes sobre a conformidade das linhas de base de configuração implementadas na consola Do Gestor de Configuração.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver os resultados de compatibilidade na consola do Configuration Manager  

1.  Na consola 'Gestor de Configuração', clique em**Implementações** **de Monitorização** > .  

3.  Na lista **Implementações** , selecione a implementação de linha de base de configuração cujas informações de compatibilidade pretende rever.  

4.  Poderá rever as informações de resumo sobre a compatibilidade da implementação da linha de base de configuração na página principal. Para ver informações mais detalhadas, selecione a implementação de linha de base de configuração e, no separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado** para abrir a página **Estado da Implementação** .  

     A página **Estado da Implementação** contém os seguintes separadores:  

    -   **Compatibilidade:** apresenta a compatibilidade da linha de base de configuração com base no número de ativos afetados. Pode clicar numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Conformidade** que contém todos os utilizadores ou dispositivos conformes com esta regra. O painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos conformes com a linha de base de configuração. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar informações adicionais.  

        > [!IMPORTANT]  
        >  Uma regra de configuração não é avaliada se não for detetada ou não aplicável num dispositivo cliente; no entanto, a regra é devolvida como conforme.  

    -   **Erro**: apresenta uma lista de todos os erros da implementação da linha de base de configuração selecionada com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Conformidade** que contém todos os utilizadores ou dispositivos que geraram erros com esta regra. Quando seleciona um utilizador ou dispositivo, o painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos que são afetados pelo problema selecionado. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar informações adicionais sobre o problema.  

    -   **Não conforme:** apresenta uma lista de todas as regras de não conformidade na linha de base de configuração com base no número de ativos afetados. Pode clicar numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Conformidade** que contém todos os utilizadores ou dispositivos não conformes com esta regra. Quando seleciona um utilizador ou dispositivo, o painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos que são afetados pelo problema selecionado. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar mais informações sobre o problema.  

    -   **Desconhecido:** apresenta uma lista de todos os utilizadores e dispositivos que não reportaram conformidade para a implementação da linha de base de configuração selecionada, juntamente com o estado atual do cliente dos dispositivos.  

5.  Na página **Estado da Implementação** , poderá rever informações detalhadas sobre a compatibilidade da linha de base de configuração implementada. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

##  <a name="view-compliance-results-by-using-reports"></a>Ver resultados de conformidade usando relatórios  
 As definições de conformidade no Gestor de Configuração incluem uma série de relatórios incorporados que permitem monitorizar informações sobre itens de configuração, linhas de base de configuração e implementações. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deve utilizar um**%** carácter wildcard () quando utilizar os parâmetros **O filtro do dispositivo** e o filtro do utilizador nos relatórios de definições de conformidade.  

 Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Ver resultados de conformidade num computador cliente do Gestor de Configuração Windows

> [!NOTE]  
>  Não é possível visualizar informações sobre o cliente do Gestor de Configuração Windows se estiver ligado a uma conta de hóspedes de domínio.    

1.  Navegue para **Configuration Manager** no Painel de Controlo do computador cliente e faça duplo clique no mesmo para abrir as respetivas propriedades.  

2.  Clique no separador **Configurações** e veja a lista de linhas de base de configuração implementadas.  

3.  Veja o **Estado de Conformidade** para cada linha de base da configuração:  

    > [!IMPORTANT]  
    >  Os resultados da avaliação são colocados em cache no cliente por 15 minutos. Se iniciar uma reavaliação dentro do período de 15 minutos, os resultados de compatibilidade desta cache são devolvidos, em vez de ser efetuada uma nova avaliação. Por conseguinte, se fizer uma alteração ao cliente que possa afetar os resultados da avaliação de compatibilidade, aguarde até que os 15 minutos tenham decorrido antes de iniciar uma reavaliação.  

    -   **Compatível**: o computador cliente está em conformidade com a linha de base de configuração avaliada.  

    -   **Não Compatível**: o computador cliente não está em conformidade com a linha de base de configuração avaliada.  

    -   **Desconhecido**: o computador cliente ainda não avaliou a linha de base de configuração. Se pretender iniciar a avaliação fora da agenda de avaliação de compatibilidade, selecione as linhas de base de configuração a avaliar e, em seguida, clique em **Avaliar**.  

        > [!NOTE]  
        >  Se tiver credenciais de administrador local no computador cliente, pode ver detalhes de cada linha de base de configuração avaliada para determinar qual o item de configuração que está a comunicar um estado não compatível. Para tal, selecione a linha de base de configuração e, em seguida, clique em **Ver Relatório**.  

4.  Clique em **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Criar coleções com base na conformidade da linha de base de configuração  
 Utilize o seguinte procedimento para criar uma coleção de Gestor de Configuração baseada em dispositivos com uma conformidade especificada. Pode criar coleções baseadas nos seguintes estados de compatibilidade:  

-   **Compatível**  

-   **Erro**  

-   **Não conforme**  

-   **Desconhecido**  

1.  Na consola do Gestor de Configuração, clique em **Ativos e** > **Definições** > de Conformidade **.**  

3.  Na lista **Linhas de Base de Configuração** , selecione a linha de base de configuração a partir da qual pretende criar uma coleção.  

4.  No separador **Implementação** , no **Grupo de Implementação**, clique em **Criar Nova Coleção** e, em seguida, na lista pendente, selecione o nível de compatibilidade para o qual pretende criar uma coleção.  

5.  É aberta opção **Assistente de Criação de Coleção de Utilizadores** ou **Assistente de Criação de Coleção de Dispositivos** , dependendo de o item de configuração ser implementado em utilizadores ou em dispositivos. O assistente é preenchido automaticamente com os valores corretos para criar a coleção; no entanto, pode editar esses valores.  

6.  Após concluir o assistente, a coleção é apresentada no nó **Coleções de Utilizadores** ou **Coleções de Dispositivos** , na área de trabalho **Recursos e Compatibilidade** .  
