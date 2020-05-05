---
title: Monitor de perfis de email, Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba como monitorizar o estado de conformidade dos perfis de e-mail, Wi-Fi e VPN no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724497"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Monitor de perfis de email, Wi-Fi e VPN no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de ter implementado perfis de Email, Wi-Fi ou VPN para utilizadores na sua hierarquia, pode utilizar os seguintes procedimentos para monitorizar o estado de conformidade do perfil:  

-   [Como ver os resultados de conformidade na consola do Gestor de Configuração](#BKMK_console)  

-   [Como Ver Resultados de Compatibilidade através da Utilização de Relatórios](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a>Como ver os resultados de conformidade na consola do Gestor de Configuração  
 Utilize este procedimento para visualizar detalhes sobre a conformidade dos perfis implantados na consola 'Gestor de Configuração'.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver os resultados de compatibilidade na consola do Configuration Manager  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  Na área de trabalho **Monitorização**, clique em **Implementações**.  

3.  Na lista de **Implementações,** selecione a implementação do perfil para a qual pretende rever as informações de conformidade.  

4.  Pode rever informações sumárias sobre a conformidade da implementação do perfil na página principal. Para ver informações mais detalhadas, selecione a implementação do perfil e, em seguida, no separador **Home,** no grupo **Deimplantação,** clique no **'Ver Status'** para abrir a página **'Status' de implementação.**  

     A página **Estado da Implementação** contém os seguintes separadores:  

    -   **Conforme:** Exibe a conformidade do perfil que se baseia no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** , contendo todos os utilizadores compatíveis com este perfil. O painel **de Detalhes** do Ativo mostra os utilizadores que estão em conformidade com o perfil. Faça duplo clique num utilizador da lista para visualizar informações adicionais.  

        > [!IMPORTANT]  
        >  Um perfil não é avaliado se não for aplicável num dispositivo cliente; no entanto, é devolvido como conforme.  

    -   **Erro:** Apresenta uma lista de todos os erros para a implementação do perfil selecionado que se baseia no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** , contendo todos os utilizadores que geraram erros com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar informações adicionais sobre o problema.  

    -   **Não conforme:** Apresenta uma lista de todas as regras não conformes dentro do perfil que se baseia no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** , contendo todos os utilizadores não compatíveis com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar mais informações sobre o problema.  

    -   **Desconhecido:** Apresenta uma lista de todos os utilizadores que não reportaram o cumprimento da implementação do perfil selecionado juntamente com o estado atual do cliente dos dispositivos.  

5.  Na página 'Estado de **Implementação',** pode rever informações detalhadas sobre a conformidade do perfil implantado. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a>Como ver os resultados da conformidade utilizando relatórios  
 As definições de conformidade, que incluem perfis no Gestor de Configuração, também incluem uma série de relatórios incorporados que permitem monitorizar informações sobre perfis. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Você deve usar um wildcard (%) carácter quando utilizar os parâmetros **Filtro de dispositivo** e filtro do **utilizador** nos relatórios de definições de conformidade.  

 Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).  
