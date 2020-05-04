---
title: Criar ambientes virtuais App-V
titleSuffix: Configuration Manager
description: Crie ambientes virtuais com a Virtualização de Aplicações da Microsoft para que as aplicações possam partilhar dados entre si.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710420"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>Criar ambientes virtuais App-V em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Num ambiente virtual de virtual de virtualização de aplicações da Microsoft (App-V) no Gestor de Configuração, as aplicações virtuais implementadas podem partilhar o mesmo sistema de ficheiros e registo em Computadores Windows clientes. Ao contrário das aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Ambientes virtuais são criados ou modificados em Computadores de cliente quando a aplicação é instalada ou quando os clientes avaliam as suas aplicações instaladas. Pode ordenar estas aplicações para que a aplicação com a ordem mais elevada tenha prioridade quando várias aplicações tentarem modificar um sistema de ficheiros ou um valor de registo.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais App-V para fornecer proteção de segurança, como por exemplo, de malware.  

 Utilize o seguinte procedimento para criar um ambiente virtual App-V no Gestor de Configuração.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual App-V  

1.  Na consola de Configuração Manager, escolha > **ambientes virtuais app-V**de gestão de > **aplicações**da Biblioteca de **Software.**  

3.  No separador **Home,** no grupo **Criar,** escolha **Criar Ambiente Virtual**.  

4.  Na caixa de diálogo **Create Virtual Environment,** introduza as seguintes informações:  

    -   **Nome.**  Introduza um nome único para o ambiente virtual (máximo de 128 caracteres).  

    -   **Descrição**. (Opcional) Introduza uma descrição para o ambiente virtual.  

5.  Para adicionar um novo tipo de implementação ao ambiente virtual, escolha **Adicionar**. Tem de adicionar pelo menos um tipo de implementação.  

6.  Na caixa de diálogo **Add Applications,** especifique um **nome de Grupo** (máximo 128 caracteres). Você usará este nome para se referir ao grupo de aplicações que você adiciona ao ambiente virtual.  

7.  Escolha **Adicionar**, selecione as aplicações App-V 5 e os tipos de implementação que pretende adicionar ao grupo e, em seguida, escolha **OK**.  

8.  Na caixa de diálogo **Adicionar Aplicações,** pode selecionar **Ordem de Aumento** ou Diminuição **para** definir a aplicação que tem prioridade se várias aplicações tentarem modificar o sistema de ficheiros ou configurações de registo no mesmo ambiente virtual.  

9. Para voltar à caixa de diálogo **Create Virtual Environment,** escolha **OK**.  

10. Quando terminar de adicionar grupos, escolha **OK** para criar o ambiente virtual. O novo ambiente virtual é apresentado no nó de **Ambientes Virtuais App-V** da consola 'Gestor de Configuração'. Pode monitorizar o estado dos seus ambientes virtuais utilizando o relatório do Estado do Ambiente Virtual app-V.  

    > [!NOTE]  
    >  O ambiente virtual é adicionado ou modificado em Computadores clientes quando a aplicação é instalada ou quando o cliente avalia as aplicações instaladas.  
