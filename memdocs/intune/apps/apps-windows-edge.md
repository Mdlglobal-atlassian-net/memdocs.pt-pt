---
title: Adicione o Microsoft Edge para windows 10 ao Microsoft Intune
titleSuffix: ''
description: Saiba adicionar o Microsoft Edge para windows ao Microsoft Intune.
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
ms.openlocfilehash: 64cb05d6e031cfe08789d6b7c923d9e489d0e433
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254321"
---
# <a name="add-microsoft-edge-for-windows-10-to-microsoft-intune"></a>Adicione o Microsoft Edge para windows 10 ao Microsoft Intune

Antes de poder implementar, configurar, monitorizar ou proteger aplicações, deve adicioná-las ao Intune. Um dos tipos de [aplicações](apps-add.md#app-types-in-microsoft-intune) disponíveis é o Microsoft Edge *versão 77 e mais tarde.* Ao selecionar este tipo de aplicação em Intune, pode atribuir e instalar a versão 77 do Microsoft Edge *e, mais tarde,* aos dispositivos que gere que executam o Windows 10.

> [!IMPORTANT]
> Este tipo de aplicação oferece canais estáveis, beta e dev para o Windows 10. A implementação é apenas em inglês (EN), no entanto os utilizadores finais podem alterar o idioma de exibição no navegador em **Configurações** > **Idiomas**. O Microsoft Edge é uma aplicação Win32 instalada no contexto do sistema e em arquiteturas semelhantes (aplicação x86 no X86 OS e x64 no X64 OS). Intune detetará quaisquer instalações pré-existentes do Microsoft Edge. Se for instalado no contexto do utilizador, uma instalação do sistema irá sobrepor-se. Se for instalado no contexto do sistema, o sucesso da instalação é relatado. Além disso, as atualizações automáticas do Microsoft Edge estão **on** por padrão.

> [!NOTE]
> A *versão 77 do* Microsoft Edge está disponível para o macOS também.
>
> Não é possível utilizar a implementação de aplicações incorporadas do Microsoft Edge para se juntar aos computadores no local de trabalho. A implementação de aplicações incorporadas requer a extensão de gestão Intune, que só existe para dispositivos aderidos a AAD. Ainda pode implementar a versão 77 do Microsoft Edge *e, mais tarde,* utilizar uma *.msi* enviada para **apps**, consulte [adicionar uma aplicação de linha de negócio do Windows ao Microsoft Intune](lob-apps-windows.md).

## <a name="prerequisites"></a>Pré-requisitos

- Windows 10 versão 1709 ou mais tarde.
- Quaisquer versões pré-instaladas da versão 77 do Microsoft Edge *e posteriormente* para todos os canais no contexto do utilizador serão substituídas com o Edge instalado no contexto do sistema.

## <a name="configure-the-app-in-intune"></a>Configure a app em Intune

Pode adicionar uma versão 77 do Microsoft Edge e, mais tarde, a Intune utilizando os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **Todas as aplicações** > **Adicionar**.
3. Na lista do **tipo App** no **Microsoft Edge, versão 77 e posterior**, selecione O Windows **10**.

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

## <a name="configure-app-settings"></a>Configurar as definições da aplicação
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
1.    Selecione **Scope (Tags)** > **Adicionar**.
2.    Utilize a caixa **Select** para procurar etiquetas de mira.
3.    Selecione a caixa de verificação junto às etiquetas de âmbito que pretende atribuir a esta aplicação.
4.    Clique em **Selecione** > **OK**.

## <a name="add-the-app"></a>Adicionar a aplicação
Quando tiver concluído a configuração da aplicação, selecione **Adicionar** a partir do painel de aplicações da **App.** 

A aplicação criada é apresentada na lista de aplicações, onde a pode atribuir aos grupos que selecionar. 

> [!NOTE]
> Atualmente, se não atribuir a implementação do Microsoft Edge, este permanecerá no dispositivo.

## <a name="uninstall-the-app"></a>Desinstalar a aplicação

Quando necessitar de desinstalar o Microsoft Edge a partir dos dispositivos do utilizador, utilize os seguintes passos.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **Todas as aplicações** > microsoft*Edge* app > **Assignments** > **Add grupo**.
3. No painel do **grupo Adicionar,** selecione **Desinstalar**.

    > [!NOTE]
    > A aplicação é desinstalada a partir de dispositivos nos grupos selecionados se intune já tiver instalado a aplicação no dispositivo através de uma **disposição disponível para dispositivos matriculados** ou atribuição **obrigatória** utilizando a mesma implementação.
4. Selecione **Grupos Incluídos** para selecionar os grupos de utilizadores que são afetados pela atribuição desta aplicação.
5. Selecione os grupos que pretende aplicar a atribuição de desinstalação.
6. Clique em **Selecionar** no painel de **grupos Select.**
7. Clique **ok** no painel **de atribuir** para definir a atribuição.
8. Selecione **Excluir Grupos** se quiser excluir grupos de utilizadores de serem afetados por esta atribuição de aplicações.
9. Se tiver optado por excluir grupos, em **Selecionar grupos**, selecione **Selecionar**.
10. Selecione **OK** no painel do **grupo Adicionar.**
11. Selecione **Guardar** no painel de atribuição de **aplicações.**

> [!IMPORTANT]
> Para desinstalar a aplicação com sucesso, certifique-se de remover os membros ou atribuição de grupo para instalação antes de atribuir a sua desinstalação. Se um grupo for designado para instalar uma aplicação e desinstalar uma aplicação, a aplicação permanecerá e não será removida.

## <a name="troubleshooting"></a>Resolução de problemas
**Microsoft Edge versão 77 e mais tarde para windows 10:**<br>
Intune utiliza a extensão de gestão Intune para descarregar e implementar o instalador Microsoft Edge para dispositivos Windows 10 atribuídos, em seguida, comunica as definições de implementação para o instalador Microsoft Edge, que descarrega e instala o navegador Microsoft Edge diretamente a partir do CDN. Consulte os [pré-requisitos para a extensão de gestão Intune](intune-management-extension.md#prerequisites), e as melhores práticas descritas no acesso ao Azure Update Service e ao CDN para garantir que a configuração da sua rede permite que os dispositivos Windows 10 acedam a estes locais. Além disso, para permitir o acesso aos ficheiros de instalação a partir de um CDN para instalar o navegador, é necessário permitir o acesso aos pontos finais do Windows Update. Para mais informações, consulte [Gerir pontos finais de ligação para windows 10, versão 1809 – Windows Update](https://docs.microsoft.com/windows/privacy/manage-windows-1809-endpoints#windows-update) e [pontos finais da Rede para o Microsoft Intune](../fundamentals/intune-endpoints.md).

## <a name="next-steps"></a>Passos seguintes
- [Atribuir aplicações a grupos](apps-deploy.md)
