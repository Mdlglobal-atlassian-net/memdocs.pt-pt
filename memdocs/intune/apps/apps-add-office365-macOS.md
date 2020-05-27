---
title: Instale aplicações do Office 365 para dispositivos macOS utilizando o Microsoft Intune
titleSuffix: ''
description: Saiba como pode utilizar o Microsoft Intune para instalar as aplicações do Office 365 em dispositivos macOS.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14a4d66cfd5ac0ee3c0938e96794ed12d5b5fde6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989513"
---
# <a name="assign-office-365-to-macos-devices-with-microsoft-intune"></a>Atribuir o Office 365 a dispositivos macOS com o Microsoft Intune

Com este tipo de aplicação, é mais fácil atribuir aplicações da versão 2016 do Office 365 a dispositivos macOS. Ao utilizar este tipo de aplicação, pode instalar word, Excel, PowerPoint, Outlook, OneNote e Teams. Para ajudar a manter as aplicações mais protegidas e atualizadas, as aplicações vêm com Microsoft AutoUpdate (MAU). As aplicações que quer são mostradas como uma aplicação na lista de aplicações na consola do Intune.

> [!NOTE]
> O Microsoft Office 365 ProPlus foi renomeado para **microsoft 365 Apps para empresa**. Na nossa documentação, geralmente vamos referir-nos a ela como **Aplicações Microsoft 365**.

## <a name="before-you-start"></a>Antes de começar

Antes de começar a adicionar aplicações do Office 365 aos dispositivos macOS, compreenda os seguintes detalhes:

- Os dispositivos em que pretende implementar estas aplicações têm de ter o macOS 10.10 ou posterior em execução.
- O Intune suporta apenas a adição de aplicações do Office que são incluídas com o Office 2016 apenas suite de Mac.
- Se estiverem abertas aplicações do Office quando o Intune instalar o conjunto de aplicações, os utilizadores poderão perder os dados dos ficheiros não guardados.

## <a name="select-microsoft-365-apps"></a>Selecione Aplicações Microsoft 365

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps**  >  **Todas as aplicações**  >  **Adicionar**.
3. Selecione **o macOS** na secção aplicações microsoft **365** do painel do **tipo select.**
4. 4. Clique em **Selecionar**. Os passos **add Microsoft 365 Apps** são apresentados.

## <a name="step-1---app-suite-information"></a>Passo 1 - Informação da suite da aplicação

Neste passo, vai fornecer as informações acerca do conjunto de aplicações. Estas informações ajudam-no a identificar o conjunto de aplicações no Intune e também ajudam os utilizadores a encontrá-lo no portal da empresa.

1. Na página de informações do **suite app,** pode confirmar ou modificar os valores predefinidos:
    - **Nome do Conjunto**: introduza o nome do conjunto de aplicações tal como será apresentado no portal da empresa. Confirme que todos os nomes de conjuntos de aplicações que utiliza são exclusivos. Se o nome de um conjunto de aplicações existir em duplicado, apenas uma das aplicações será apresentada aos utilizadores no portal da empresa.
    - **Descrição do Conjunto**: introduza uma descrição para o conjunto de aplicações. Por exemplo, pode listar as aplicações que selecionou para inclusão.
    - **Publicador**: a Microsoft aparece como o publicador.
    - **Categoria**: em alternativa, selecione uma ou mais categorias de aplicações incorporadas ou uma categoria criada por si. Esta definição irá permitir que os utilizadores encontrem o conjunto de aplicações mais facilmente quando procurarem no portal da empresa.
    - **Mostre-o como uma aplicação em destaque no Portal da Empresa**: Selecione esta opção para exibir a suite de aplicações em destaque na página principal do portal da empresa quando os utilizadores navegam para apps.
    - **URL de Informações**: opcionalmente, introduza o URL de um site que contenha informações sobre esta aplicação. O URL é apresentado aos utilizadores no portal da empresa.
    - **URL de Privacidade**: opcionalmente, introduza um URL para um site que contenha informações sobre a privacidade desta aplicação. O URL é apresentado aos utilizadores no portal da empresa.
    - **Programador**: a Microsoft aparece como o programador.
    - **Proprietário**: a Microsoft aparece como o proprietário.
    - **Notas**: introduza quaisquer notas que queira associar a esta aplicação.
    - **Logotipo**: O logótipo das Aplicações Microsoft 365 é apresentado com a aplicação quando os utilizadores navegam no portal da empresa.
2. Clique em **Seguir** para exibir a página **de tags scope.**

## <a name="step-2---select-scope-tags-optional"></a>Passo 2 - Selecione etiquetas de âmbito (opcional)
Pode utilizar etiquetas de âmbito para determinar quem pode ver informações sobre aplicações do cliente no Intune. Para mais detalhes sobre etiquetas de âmbito, consulte [Use o controlo de acesso baseado em funções e as etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

1. Clique em **Selecionar etiquetas** de âmbito para adicionar opcionalmente etiquetas de âmbito para o suite da aplicação. 
2. Clique em **Seguir** para exibir a página **de Tarefas.**

## <a name="step-3---assignments"></a>Passo 3 - Atribuições

1. Selecione o **Necessário** ou Disponível para atribuições de grupo de **dispositivos inscritos** para o conjunto de aplicações. Para mais informações, consulte [grupos Add para organizar utilizadores e dispositivos](../fundamentals/groups-add.md) e [atribuir aplicações a grupos com](apps-deploy.md)o Microsoft Intune .

    >[!Note]
    > Não é possível desinstalar o pacote de aplicações 'Microsoft 365 para macOS' através do Intune.

2. Clique em **Seguir** para exibir a página **Review + criar.** 

## <a name="step-4---review--create"></a>Passo 4 - Rever + criar

1. Reveja os valores e configurações que inseriu para a suite da aplicação.
2. Quando terminar, clique em **Criar** para adicionar a app ao Intune.

    A lâmina **de visão geral** é exibida. O conjunto é apresentado na lista de aplicações como uma única entrada.

## <a name="next-steps"></a>Passos seguintes

- Para saber adicionar aplicações do Office 365 aos dispositivos Windows 10, consulte [as aplicações DoMicrosoft 365 para dispositivos Windows 10 com](apps-add-office365.md)o Microsoft Intune .
- Para saber mais sobre como incluir e excluir atribuições de aplicações a partir de grupos de utilizadores, veja [Incluir e excluir atribuições de aplicações](apps-inc-exl-assignments.md).
