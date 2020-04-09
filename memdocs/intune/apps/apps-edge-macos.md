---
title: Adicione o Microsoft Edge aos dispositivos macOS utilizando o Microsoft Intune
titleSuffix: ''
description: Saiba adicionar o Microsoft Edge aos dispositivos macOS utilizando o Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0d9267f989988ae33d56696d424de56a649bca2
ms.sourcegitcommit: 9908de7d30991ee499cc462d2eb730e1e4fd75a9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80900478"
---
# <a name="add-microsoft-edge-to-macos-devices-using-microsoft-intune"></a>Adicione o Microsoft Edge aos dispositivos macOS utilizando o Microsoft Intune

Antes de poder implementar, configurar, monitorizar ou proteger aplicações, deve adicioná-las ao Intune. Um dos tipos de [aplicações](apps-add.md#app-types-in-microsoft-intune) disponíveis é o Microsoft Edge *versão 77 e mais tarde.* Ao selecionar este tipo de aplicação em Intune, pode atribuir e instalar a versão 77 do Microsoft Edge *e, mais tarde,* aos dispositivos que gere o macOS. Este tipo de aplicação facilita a atribuição do Microsoft Edge aos dispositivos macOS sem que utilize a ferramenta de embrulho da aplicação macOS. Para ajudar a manter as aplicações mais seguras e atualizadas, a aplicação vem com o Microsoft AutoUpdate (MAU).

> [!IMPORTANT]
> Este tipo de aplicação oferece canais de desenvolvimento e beta para macOS. A implementação é apenas em inglês (EN), no entanto os utilizadores finais podem alterar o idioma de exibição no navegador em **Definições** > **Idiomas**. 

> [!NOTE]
> O Microsoft Edge *versão 77 e mais tarde* está disponível para o Windows 10 também.

## <a name="prerequisites"></a>Pré-requisitos

- O dispositivo macOS deve estar a funcionar com o macOS 10.12 ou mais tarde antes de instalar o Microsoft Edge.

## <a name="add-microsoft-edge-to-intune"></a>Adicione microsoft edge ao Intune

Pode adicionar a versão 77 do Microsoft Edge e, mais tarde, a Intune utilizando os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **Todas as aplicações** > **Adicionar**.
3. Na lista do **tipo App** no **Microsoft Edge, versão 77 e posterior**, selecione **macOS**.

## <a name="configure-app-information"></a>Configurar as informações da aplicação
Neste passo, fornece informações sobre esta implementação da aplicação. Esta informação ajuda-o a identificar a aplicação em Intune, e ajuda os utilizadores a encontrar a app no portal da empresa.

1. Clique em **informações da App** para exibir o painel de informações da **App.**
2. No painel de informações da **App,** fornece informações sobre a implementação desta aplicação. Esta informação ajuda-o a identificar a aplicação em Intune, e ajuda os utilizadores a encontrar a app no portal da empresa.
    - **Nome**: Introduza o nome da aplicação tal como será apresentado no portal da empresa. Certifique-se de que todos os nomes são únicos. Se existir o mesmo nome duas vezes, só é apresentada uma das aplicações aos utilizadores no portal da empresa.
    - **Descrição**: introduza uma descrição para a aplicação. Por exemplo, pode enumerar os utilizadores visados na descrição.
    - **Publicador**: a Microsoft aparece como o publicador.
    - **Categoria**: em alternativa, selecione uma ou mais categorias de aplicações incorporadas ou uma categoria criada por si. Esta definição facilita aos utilizadores encontrar a app quando navegam no portal da empresa.
    - **Exiba-o como uma aplicação em destaque no Portal da Empresa**: Selecione esta opção para exibir a aplicação em destaque na página principal do portal da empresa quando os utilizadores navegam para apps.
    - **URL de Informações**: opcionalmente, introduza o URL de um site que contenha informações sobre esta aplicação. O URL é apresentado aos utilizadores no portal da empresa.
    - **URL de Privacidade**: opcionalmente, introduza um URL para um site que contenha informações sobre a privacidade desta aplicação. O URL é apresentado aos utilizadores no portal da empresa.
    - **Programador**: a Microsoft aparece como o programador.
    - **Proprietário**: a Microsoft aparece como o proprietário.
    - **Notas**: opcionalmente, introduza quaisquer notas que queira associar a esta aplicação.
3. Selecione **OK**.

## <a name="configure-microsoft-edge-settings"></a>Configurar definições do Microsoft Edge
Neste passo, configure as opções de instalação para a aplicação.

1. No painel **adicionar app,** selecione **as definições da App**.
2. No painel de definições da **App,** selecione **estável,** **Beta** ou **Dev** da lista **do Canal** para determinar de que Canal de Borda irá implementar a aplicação.

    - **O** canal estável é o canal recomendado para a implantação em ambientes empresariais. Atualiza a cada seis semanas, cada versão incorporando melhorias do canal Beta.
    - **O** canal Beta é a experiência de pré-visualização mais estável do Microsoft Edge e a melhor escolha para um piloto completo dentro da sua organização. Com grandes atualizações a cada seis semanas, cada lançamento incorpora as aprendizagens e melhorias do canal Dev.
    - O canal **Dev** está pronto para feedback da empresa no Windows, Windows Server e macOS. Atualiza todas as semanas e contém as últimas melhorias e correções.

    > [!NOTE]
    > O logótipo do navegador Microsoft Edge é apresentado com a aplicação quando os utilizadores navegam no portal da empresa.

3.    Selecione **OK**.

## <a name="select-scope-tags-optional"></a>Selecione etiquetas de âmbito (opcional)
Pode utilizar etiquetas de âmbito para determinar quem pode ver informações sobre aplicações do cliente no Intune. Para mais detalhes sobre etiquetas de âmbito, consulte Use o controlo de acesso baseado em funções e etiquetas de âmbito para TI distribuídos.
1.    Selecione **Scope (Tags)**  > **Adicionar**.
2.    Utilize a caixa **Select** para procurar etiquetas de mira.
3.    Selecione a caixa de verificação junto às etiquetas de âmbito que pretende atribuir a esta aplicação.
4.    Clique em **selecionar** > **OK**.

## <a name="add-the-app"></a>Adicionar a aplicação
Quando tiver concluído a configuração, selecione **Adicionar** a partir do painel de aplicações da **App.** 

A aplicação criada é apresentada na lista de aplicações, onde a pode atribuir aos grupos que selecionar. 

> [!NOTE]
> Atualmente, a Apple não fornece uma forma de a Intune desinstalar o Microsoft Edge em dispositivos macOS.

## <a name="next-steps"></a>Próximos passos
- Para saber configurar o Microsoft Edge em dispositivos macOS, consulte [configure Microsoft Edge em dispositivos macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
- Para saber mais sobre como incluir e excluir atribuições de aplicações a partir de grupos de utilizadores, veja [Incluir e excluir atribuições de aplicações](apps-inc-exl-assignments.md).
- [Atribuir aplicações a grupos](apps-deploy.md)
