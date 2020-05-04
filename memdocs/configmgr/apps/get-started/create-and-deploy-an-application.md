---
title: Criar e implementar uma aplicação
titleSuffix: Configuration Manager
description: Crie e implemente uma aplicação que contenha uma app de linha de negócioe aprenda a gerir as aplicações de forma eficaz.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710511"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Criar e implementar uma aplicação com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Neste tópico, você vai entrar e criar uma aplicação com O Gestor de Configuração. Neste exemplo, irá criar e implementar uma aplicação que contém uma aplicação de linha de negócio para PCs Windows chamada **Contoso.msi**, que deve ser instalada em todos os PCs que estão a executar o Windows 10 na sua empresa. Ao longo do caminho, você vai aprender sobre muitas das coisas que você pode fazer para gerir aplicações de forma eficaz.  

 Este procedimento foi concebido para lhe dar uma visão geral de como criar e implementar aplicações do Gestor de Configuração. No entanto, não abrange todas as opções de configuração, nem como criar e implementar aplicações para outras plataformas.  

 Para obter detalhes específicos que sejam relevantes para cada plataforma, consulte um dos seguintes tópicos:  

- [Criar aplicações Windows](creating-windows-applications.md)
- [Criar aplicações Windows Phone](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Criar aplicações para computadores Mac](creating-mac-computer-applications.md)
- [Criar aplicações de servidor Linux e UNIX](creating-linux-and-unix-server-applications.md)
- [Criar aplicações Windows Embedded](creating-windows-embedded-applications.md)


Se já está familiarizado com as aplicações do Gestor de Configuração, pode ignorar este tópico. No entanto, é melhor rever [as aplicações Create](../../apps/deploy-use/create-applications.md) para conhecer todas as opções disponíveis quando criar e implementar aplicações.  

## <a name="before-you-start"></a>Antes de começar  

Certifique-se de que reviu a informação em [Introdução à gestão](../understand/introduction-to-application-management.md) de aplicações para que tenha preparado o seu site para instalar aplicações e compreenda a terminologia que é usada neste tópico.  

 Além disso, certifique-se de que os ficheiros de instalação da aplicação **Contoso.msi** estão num local acessível na sua rede.  

## <a name="create-the-configuration-manager-application"></a>Criar a aplicação do Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Para iniciar o Assistente de Aplicação Criar e criar a aplicação  

1. Na consola de Configuração Manager, escolha aplicações de**gestão** > de**aplicações**da Biblioteca > de **Software.**  

2. No separador **Casa,** no grupo **Criar,** escolha **Criar Aplicação**.  

3. Na página **geral** do Assistente de **Aplicação Criar,** escolha **automaticamente detetar informações sobre esta aplicação a partir de ficheiros de instalação**. Isto pré-povoa algumas das informações no assistente com informações extraídas do ficheiro .msi de instalação. Em seguida, especifique as seguintes informações:  

   - **Tipo:** Escolha **o\*Instalador do Windows (ficheiro .msi)**.  

   - **Localização**: Digite a localização (ou escolha **Navegar** para selecionar a localização) do ficheiro de instalação **Contoso.msi**. Note que a localização deve ser especificada no formulário * \\\Server\Share\File* for Configuration Manager para localizar os ficheiros de instalação.  

   Vais acabar com algo que se parece com a seguinte imagem:  

   ![Página geral do assistente de gestão de aplicativos](media/App-management-wizard-general-page.png)  

4. Escolha **Seguinte**. Na página de Informações sobre **Importações,** você verá algumas informações sobre a app e quaisquer ficheiros associados que foram importados para O Gestor de Configuração. Uma vez feito, escolha **o próximo** novamente.  

5. Na página **Informação Geral,** pode fornecer mais informações sobre a aplicação para o ajudar a ordenar e localizá-la na consola do Gestor de Configuração.  

    Além disso, o campo do **programa de instalação** permite especificar a linha de comando completa que será usada para instalar a aplicação em Computadores. Pode editar isto para adicionar as suas próprias propriedades (por **exemplo/q** para uma instalação sem supervisão).  

   > [!TIP]  
   > Alguns dos campos nesta página do assistente poderão ter sido preenchidos automaticamente quando importou os ficheiros de instalação da aplicação.  

    Acabará com um ecrã que se parece com a seguinte imagem:  

    ![Página geral de informação geral do assistente de gestão de aplicações](media/App-management-wizard-general-information-page.png)  

6. Escolha **Seguinte**. Na página Resumo, pode confirmar as definições da sua aplicação e, em seguida, completar o assistente.  

   Acabou de criar a aplicação. Para encontrá-lo, no espaço de trabalho da Biblioteca de **Software,** expandir a Gestão de **Aplicações,** e depois escolher **Aplicações.** Para este exemplo, será apresentado:  

   ![Gráfico final da aplicação](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar as propriedades da aplicação e o respetivo tipo de implementação  

Agora que criou uma aplicação, pode aperfeiçoar as definições de aplicação se precisar. Para ver as propriedades da aplicação, selecione a aplicação e, em seguida, no separador **Home** no grupo **Properties,** escolha **Propriedades**.  

 Na caixa de diálogo **<Contoso\> Application Properties,** você verá muitos itens que você pode configurar para refinar o comportamento da aplicação. Para mais detalhes sobre todas as definições que pode configurar, consulte [Criar aplicações](../../apps/deploy-use/create-applications.md). Para efeitos deste exemplo, irá alterar apenas algumas propriedades do tipo de implementação da aplicação.  

 Escolha o separador Tipos de **Implementação** > tipo de implementação da **aplicação Contoso** > **Editar**.

Será apresentada uma caixa de diálogo como a seguinte:  

![Página de propriedades de aplicativos de gestão de aplicativos](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Adicionar um requisito ao tipo de implementação

 Os requisitos especificam condições que têm ser satisfeitas para que uma aplicação possa ser instalada num dispositivo.  Pode escolher entre os requisitos incorporados ou pode criar os seus próprios. Neste exemplo, adiciona-se a exigência de que a aplicação só será instalada em PCs que estejam a executar o Windows 10.  

1. A partir da página de propriedades do tipo de implementação que acaba de abrir, escolha o separador **Requisitos.**  

2. Escolha **Adicionar** para abrir a caixa de diálogo **Criar Requisitos.**  

3. Na caixa de diálogo **Criar Requisito** , especifique as seguintes informações:  

    - **Categoria**: **Dispositivo**  

    - **Condição**: **Sistema operativo**  

    - **Tipo de regra**: **Valor**  

    - **Operador**: **Um dos**  

    - Na lista de sistemas operativos, selecione **Windows 10**.  

    Será apresentada uma caixa de diálogo semelhante à seguinte:  

    ![Página de requisitos de gestão de aplicações](media/App-management-requirements-page.png)  

4. Escolha **OK** para fechar cada página de propriedade que abriu. Em seguida, volte à lista de **Aplicações** na consola 'Gestor de Configuração'.  

> [!TIP]  
> Os requisitos podem ajudar a reduzir o número de coleções do Gestor de Configuração que você precisa. Uma vez que acaba de especificar que a aplicação só pode ser instalada em PCs que estão a executar o Windows 10, pode posteriormente implementá-lo para uma coleção que contém PCs que executam vários sistemas operativos diferentes. Mas a aplicação só será instalada nos Computadores Windows 10.

## <a name="add-the-application-content-to-a-distribution-point"></a>Adicionar o conteúdo da aplicação a um ponto de distribuição  

Em seguida, para implementar a aplicação em Computadores, certifique-se de que o conteúdo da aplicação é copiado para um ponto de distribuição. Os computadores acedem ao ponto de distribuição para instalar a aplicação.  

> [!TIP]  
> Para saber mais sobre pontos de distribuição e gestão de conteúdos no Gestor de Configuração, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)

1. Na consola De Configuração, escolha a Biblioteca de **Software.**  

2. No espaço de trabalho da Biblioteca de **Software,** expandir **aplicações.** Depois, na lista de aplicações, selecione a **Aplicação Contoso** que criou.  

3. No separador **Home,** no grupo **De implantação,** escolha **Distribute Content**.  

4. Na página **geral** do Assistente de **Conteúdo distribuído,** verifique se o nome da aplicação está correto e, em seguida, escolha **Seguinte**.  

5. Na página **'Conteúdo',** reveja as informações que serão copiadas para o ponto de distribuição e, em seguida, escolha **A Seguinte**.  

6. Na página destino de **conteúdo,** escolha **Adicionar** para selecionar um ou mais pontos de distribuição, ou grupos de pontos de distribuição para instalar o conteúdo da aplicação.  

7. Conclua o assistente.  

Pode verificar se o conteúdo da aplicação foi copiado com sucesso para o ponto de distribuição a partir do espaço de trabalho de **monitorização,** sob o estado do**conteúdo**do **estado** > de distribuição .  

## <a name="deploy-the-application"></a>Implementar a aplicação  

Em seguida, implemente a aplicação numa coleção de dispositivos na sua hierarquia. Neste exemplo, implementa a aplicação para a recolha de dispositivos **All Systems.**  

> [!TIP]  
> Lembre-se que apenas os computadores Windows 10 irão instalar a aplicação devido aos requisitos que selecionou anteriormente.

1. Na consola de Configuração Manager, escolha aplicações de**gestão** > de**aplicações**da Biblioteca > de **Software.**  

2. A partir da lista de aplicações, selecione a aplicação que criou anteriormente (**Aplicação Contoso),** e depois, no separador **Home** no grupo **Deployment,** escolha **Deploy**.  

3. Na página **geral** do **Assistente de Software de Implementação,** escolha **navegar** para selecionar a coleção de dispositivos **All Systems.**  

4. Na página **'Conteúdo',** verifique se o ponto de distribuição a partir do qual pretende que os Computadores instalam a aplicação seja selecionado.  

5. Na página definições de **implementação,** certifique-se de que a ação de implementação está definida para **instalar**, e o objetivo de implementação está definido para **O Necessário**.  

    > [!TIP]  
    > Ao definir o propósito de implementação para **o Necessário,** certifique-se de que a aplicação está instalada em PCs que satisfaçam os requisitos que definiu. Se definir este valor como **Disponível**, os utilizadores poderão instalar a aplicação a pedido a partir do Centro de Software.

6. Na página **Agendamento** , pode configurar quando a aplicação será instalada. Para este exemplo, selecione **Logo que possível após o tempo disponível**.  

7. Na página Experiência do **Utilizador,** escolha **A seguir** para aceitar os valores predefinidos.  

8. Conclua o assistente.  

Utilize as informações no seguinte Monitor a secção **de aplicação** para ver o estado da sua implementação da aplicação.  

## <a name="monitor-the-application"></a>Monitorizar a aplicação

 Nesta secção, você vai olhar rapidamente para o estado de implementação da aplicação que acabou de implementar.  

### <a name="to-review-the-deployment-status"></a>Para rever o estado de implementação  

1. Na consola 'Gestor de Configuração', escolha**implementações** **de monitorização** > .  

2. Na lista de implementações, selecione **Aplicação Contoso**.  

3. No separador **Home,** no grupo **de implantação,** escolha **'Ver Status**' .  

4. Selecione um dos seguintes separadores para ver mais atualizações de estado sobre a implementação da aplicação:  

    - **Sucesso**: A aplicação instalada com sucesso nos Computadores Indicados.  

    - **Em Curso**: A aplicação ainda não terminou de instalar.  

    - **Erro**: Ocorreu um erro ao instalar a aplicação nos Computadores Indicados. São também apresentadas mais informações sobre o erro.  

    - **Requisitos Não Cumpridos**: Não foi feita nenhuma tentativa de instalação nos dispositivos indicados porque não satisfaziam os requisitos configurados (neste exemplo, porque não funcionam no Windows 10).  

    - **Desconhecido**: O Gestor de Configuração não pôde reportar o estado da implantação. Verifique novamente mais tarde.  

> [!TIP]  
> Existem algumas formas de monitorizar as implementações de aplicações. Para mais detalhes, consulte [as aplicações do Monitor](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Experiência do utilizador final  

Os utilizadores que possuem PCs que são geridos pelo Gestor de Configuração e que executam o Windows 10 vêem uma mensagem a dizer-lhes que devem instalar a aplicação Contoso. Uma vez que aceitem a instalação, a aplicação é instalada.  

A partir da versão 1906 do Gestor de Configuração, a notificação do **New Software is Available** só será mostrada uma vez para um utilizador para uma determinada aplicação e revisão. O utilizador deixará de ver a notificação sempre que iniciar sessão. Só verão outra notificação para um pedido se o pedido tiver mudado ou sido redistribuído.

## <a name="next-steps"></a>Passos seguintes

[Monitorizar aplicações](../deploy-use/monitor-applications-from-the-console.md)
