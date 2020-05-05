---
title: Criar aplicações
titleSuffix: Configuration Manager
description: Criar aplicações com tipos de implementação, métodos de deteção e requisitos para instalar software.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 33a95ae78fdc80c6c08b59cfe5ec5b2e88485a8f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074661"
---
# <a name="create-applications-in-configuration-manager"></a>Criar aplicações no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Uma aplicação de Gestor de Configuração define os metadados sobre a aplicação. Uma aplicação tem um ou mais tipos de implantação. Estes tipos de implementação incluem os ficheiros de instalação e as informações necessárias para instalar software nos dispositivos. Um tipo de implementação também tem regras, tais como métodos de deteção e requisitos. Estas regras especificam quando e como o cliente instala o software.  

Criar aplicações utilizando os seguintes métodos:  

- Criar automaticamente uma aplicação e tipos de implementação através da leitura dos ficheiros de instalação da aplicação:  
  - [Criar uma aplicação](#bkmk_create) e [detetar automaticamente](#bkmk_auto-app) informações sobre aplicações
  - [Criar um tipo](#bkmk_create-dt) de implementação e [identificar automaticamente](#bkmk_auto-dt) informações do tipo de implementação

- Criar manualmente uma aplicação e, em seguida, adicionar tipos de implementação mais tarde:  
  - [Criar uma aplicação](#bkmk_create) e [especificar manualmente](#bkmk_manual-app) as informações de aplicação
  - [Criar um tipo](#bkmk_create-dt) de implementação e [especificar manualmente](#bkmk_manual-dt) as informações do tipo de implementação

- [Importar um pedido](#bkmk_import) de um ficheiro  

Este artigo também inclui as seguintes informações para configurar um tipo de implementação:  

- [Conteúdo](#bkmk_dt-content)
- [Sequência de Tarefas](#bkmk_dt-ts)
- [Método de Deteção](#bkmk_dt-detect)
- [Experiência do Utilizador](#bkmk_dt-ux)
- [Requisitos](#bkmk_dt-require)
- [Códigos de Devolução](#bkmk_dt-return)
- [Dependências](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a>Criar uma aplicação  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**  

2. No separador **Casa** da fita, no grupo **Criar,** selecione **Criar Aplicação**.  

Em seguida, detete ou especifique manualmente as informações de aplicação:  

- [Detete automaticamente](#bkmk_auto-app) informações de aplicação para criar uma aplicação básica com um único tipo de implementação. Por exemplo, um ficheiro Instalador do Windows que não tem dependências ou requisitos. Depois de criar uma aplicação utilizando este procedimento, edite-a conforme necessário. Pode adicionar ou alterar tipos de implementação e adicionar métodos de deteção, dependências ou requisitos.  

- [Especifique manualmente](#bkmk_manual-app) as informações de aplicação para criar aplicações mais complexas. Defina mais do que um tipo de implantação, dependências, métodos de deteção ou requisitos.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a>Detete automaticamente informações sobre aplicações  

1. Na página **Geral** do assistente de Aplicação Criar, selecione **detetar automaticamente informações sobre esta aplicação a partir de ficheiros de instalação**.  

2. Na lista de drop-down do **Tipo,** selecione o tipo de ficheiro de instalação de aplicação que pretende utilizar para detetar informações sobre a aplicação. Para obter mais informações sobre os tipos de instalação disponíveis, consulte os tipos de [implementação suportados pelo Gestor](create-applications.md#bkmk_deploy-types)de Configuração .  

3. Na caixa **de localização,** especifique o ficheiro de instalação da aplicação que pretende utilizar para detetar informações sobre a aplicação. Esta localização é ou`\\server\share\filename`um caminho de rede ou um link de loja. Deve ter acesso ao caminho da rede e a quaisquer subpastas que incluam conteúdo de aplicação.  

    > [!IMPORTANT]  
    > Quando seleciona o **Instalador do Windows (ficheiro\*.msi)** como tipo de aplicação, o site importa todos os ficheiros na pasta especificada. Em seguida, envia estes ficheiros para pontos de distribuição. Certifique-se de que a pasta especificada contém apenas os ficheiros necessários para instalar a aplicação. A Microsoft testa o Gestor de Configuração para suportar até 20.000 ficheiros no pacote de aplicações. Se a sua aplicação tiver mais ficheiros, considere criar várias aplicações com menos ficheiros.  

4. Na página informação sobre **importações** do assistente de aplicação criar, reveja as informações e, em seguida, selecione **Next**. Se necessário, selecione **Anterior** para voltar e corrigir quaisquer erros.  

5. Na página **informação geral** do assistente de aplicação criar, especifique as seguintes informações:  

    > [!NOTE]  
    > Se o Gestor de Configuração detetar automaticamente esta informação a partir dos ficheiros de instalação da aplicação, já está povoado aqui. Além disso, as opções apresentadas poderão ser diferentes dependendo do tipo de aplicação que criou.  

    - Informações gerais sobre a aplicação, como o **nome**da aplicação, **comentários do administrador,** **versão Publisher**e **Software.** Para ajudá-lo a encontrar a aplicação na consola Do Gestor de Configuração, especifique uma **referência opcional,** ou selecione **categorias administrativas.**  

    - **Programa de instalação**: Especifique o programa de instalação e quaisquer propriedades necessárias para instalar o tipo de implementação da aplicação.  

        > [!TIP]  
        > Se o programa de instalação não aparecer, escolha **Navegar** e navegue até à localização do programa de instalação.  

    - **Instalar comportamento**: Selecione uma das três opções para como o Gestor de Configuração instala este tipo de implementação. Para obter mais informações sobre estas opções, consulte [a Experiência do Utilizador.](#bkmk_dt-ux)  

    - **Utilize uma ligação VPN automática (se configurada)**: Se tiver implementado um perfil VPN no dispositivo em que o utilizador lança a aplicação, ligue a VPN quando a aplicação começar. Esta opção é apenas para Windows 8.1 e Windows Phone 8.1. Nos dispositivos Windows Phone 8.1, se implementar mais de um perfil VPN para o dispositivo, as ligações VPN automáticas não são suportadas. Para mais informações, consulte [perfis VPN](../../protect/deploy-use/vpn-profiles.md).  

    - **Disponibilização desta aplicação para todos os utilizadores do dispositivo**<!--1358310-->: Fornecer uma aplicação com um pacote de aplicações Windows para todos os utilizadores do dispositivo. Para mais informações, consulte [Create Windows aplicações](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Se estiver a modificar uma aplicação existente, esta definição está no separador **User Experience** das propriedades do tipo de implementação de pacotes de aplicações Windows.  

6. Escolha **a seguir,** reveja as informações da aplicação na página **Resumo** e, em seguida, termine o assistente de Aplicação Criar.  

A nova aplicação aparece agora no nó de **Aplicações** da consola 'Gestor de Configuração'. Terminou de criar uma candidatura.

Para adicionar mais tipos de implementação ou configurar outras definições, consulte Criar tipos de [implementação para a aplicação](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a>Especificar manualmente as informações sobre a aplicação  

1. Na página **Geral** do assistente de aplicação criar, selecione **manualmente especificar as informações da aplicação**, e, em seguida, escolha **A Seguinte**.  

2. Especificar **Informações Gerais** sobre o pedido:  

    - O **nome** da aplicação é necessário e deve ter menos de 256 caracteres.  

    - **Comentários**de administrador , **versão Publisher**e **Software** são metadados adicionais para descrever ainda mais a aplicação.  

    - Para ajudá-lo a encontrar a aplicação na consola Do Gestor de Configuração, especifique uma **referência opcional,** ou selecione **categorias administrativas.**  

    - **Data publicada**  

    - Selecione utilizadores ou grupos responsáveis por esta aplicação como **Contactos Proprietários** e **Suportes**. Por predefinição, estes valores são definidos para o seu nome de utilizador.  

3. Na página do Centro de **Software** do assistente de aplicação criar, especifique as seguintes informações:  

    > [!Note]  
    > Na versão 1902 e anterior, esta página foi nomeada Catálogo de **Aplicações.**

    - **Idioma selecionado**: Na lista de drop-down, selecione a versão idioma da aplicação que pretende configurar. Escolha **Adicionar/Remover** para configurar mais idiomas para esta aplicação.  

    - **Nome**de candidatura localizado : Especifique o nome da aplicação no idioma selecionado.  

        > [!IMPORTANT]  
        > É necessário um nome de aplicação localizado para cada versão linguística que configura.  

    - **Categorias de utilizadores**: Escolha **editar** para especificar as categorias de aplicação no idioma selecionado. Os utilizadores do Software Center usam estas categorias para ajudar a filtrar e classificar as aplicações.  

        > [!Note]  
        > Na versão 1902 e anterior, as categorias de utilizadores aplicam-se apenas às implementações disponíveis nas coleções dos utilizadores. Se uma aplicação for implementada para uma recolha de computador, as categorias de utilizador são ignoradas.
        >
        > A partir da versão 1906, as categorias de utilizadores para implementações de aplicações direcionadas para dispositivos mostram como filtros no Software Center. Estas implementações podem estar disponíveis ou necessárias.
        >
        > <!-- 4726793 -->Renomear ou eliminar uma categoria não se aplica automaticamente a aplicações com esta categoria. Estas alterações aplicam-se na próxima revisão da app. Para contornar esta questão para renomear ou eliminar:
        >
        > - Primeiro limpe a caixa de verificação para a categoria em qualquer aplicação que a refira. Em seguida, aplique essa alteração, que revê a app.
        >     - Em vez da ação de renome, em seguida, criar uma nova categoria com o novo nome, e adicionar a nova categoria às aplicações relevantes.
        >     - Pode eliminar a categoria depois de rever as aplicações.

    - **Documentação do utilizador**: Especifique a localização de um ficheiro a partir do qual os utilizadores do Software Center podem obter mais informações sobre esta aplicação. Esta localização é um endereço de site, ou um caminho de rede e nome de arquivo. Certifique-se de que os utilizadores têm acesso a este local.  

    - **Link texto**: Especifique o texto que aparece no lugar de "Informações adicionais" quando a documentação do utilizador for especificada.  

    - **URL de privacidade**: Especifique um endereço do site para a declaração de privacidade da aplicação.  

    - **Descrição localizada**: Introduza uma descrição para esta aplicação no idioma selecionado.  

    - **Palavras-chave**: Introduza uma lista de palavras-chave no idioma selecionado. Estas palavras-chave ajudam os utilizadores do Software Center a procurar a aplicação.  

    - **Ícone**: **Selecione Navegar** para selecionar um ícone para esta aplicação. Se não especificar um ícone, o Gestor de Configuração utiliza um ícone predefinido. Os ícones podem ter dimensões de pixel de até 512x512.  

4. Na página 'Tipos de **Implementação'** do assistente de aplicação criar, escolha **adicionar** para criar um novo tipo de implementação. Para mais informações, consulte Criar tipos de [implementação para a aplicação](#bkmk_create-dt).  

5. Escolha **a seguir,** reveja as informações da aplicação na página **Resumo** e, em seguida, termine o assistente de Aplicação Criar.  

A nova aplicação aparece agora no nó de **Aplicações** da consola 'Gestor de Configuração'.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a>Criar tipos de implementação para a aplicação  

Se [detetar automaticamente as informações da aplicação,](#bkmk_auto-app)poderá não precisar de terminar alguns dos passos desta secção.  

> [!Note]  
> Quando vê as propriedades de um tipo de implantação existente, as seguintes secções correspondem a separadores da janela de propriedades do tipo de implantação:  
>
> - [Conteúdo](#bkmk_dt-content)
> - [Sequência de Tarefas](#bkmk_dt-ts)
> - [Método de Deteção](#bkmk_dt-detect)
> - [Experiência do Utilizador](#bkmk_dt-ux)
> - [Requisitos](#bkmk_dt-require)
> - [Códigos de Devolução](#bkmk_dt-return)
> - [Dependências](#bkmk_dt-depend)
>  
> Para obter informações sobre o separador **'Comportamento de instalação'** sobre as propriedades de um tipo de implementação, consulte a execução de [ficheiros executáveis](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Inicie o assistente do tipo de implementação Criar  

Existem três formas de iniciar o assistente do Tipo de Implementação Create:

- **No nó de Aplicações**: Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione o nó de **Aplicações.** Selecione uma aplicação e, em seguida, selecione Criar tipo de **implantação** na fita.  

- **Ao criar uma aplicação**: Quando [especificar manualmente as informações](#bkmk_manual-app) da aplicação no assistente de aplicação Criar, selecione **Adicionar** na página Tipos de Implementação.  

- **A partir de propriedades de aplicação**: Selecione uma aplicação existente no nó de **Aplicações** e selecione **Propriedades**. Mude para o separador Tipos de **Implementação** e selecione **Adicionar**.

Em seguida, utilize um dos seguintes procedimentos para [identificar](#bkmk_auto-dt) ou [especificar manualmente](#bkmk_manual-dt) as informações do tipo de implantação.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a>Identifique automaticamente as informações do tipo de implementação  

1. Na página **geral** do assistente do Tipo de Implantação Create:  

    1. Selecione o ficheiro de instalação de aplicação **Tipo** para detetar as informações do tipo de implementação.  

    2. Selecione identifique **automaticamente informações sobre este tipo de implementação a partir de ficheiros de instalação**.  

    3. Na caixa **de localização,** especifique o ficheiro de instalação da aplicação que pretende utilizar para detetar as informações do tipo de implementação. Esta localização é ou`\\server\share\filename`um caminho de rede ou um link de loja. Deve ter acesso ao caminho da rede e a quaisquer subpastas que incluam conteúdo de aplicação.  

2. Na página informação sobre **importações** do assistente do Tipo de Implantação Create, reveja as informações e, em seguida, selecione **Next**. Se necessário, selecione **Anterior** para voltar e corrigir quaisquer erros.  

3. Na página **informação geral** do assistente do Tipo de Implantação Criar, especifique as seguintes informações:  

    > [!NOTE]  
    > Algumas das informações sobre o tipo de implementação podem já estar presentes se já foram lidas nos ficheiros de instalação da aplicação. Além disso, as opções apresentadas podem diferir, dependendo do tipo de implementação que está a criar.  

    - **Informações Gerais** sobre o tipo de implantação:  
        - O **nome** é necessário  

        - **Administradores comentam** para descrevê-lo ainda mais  

        - **Línguas** que estão disponíveis para ele  

    - **Programa de instalação**: Especifique o programa de instalação e quaisquer propriedades que necessite para instalar o tipo de implantação.  

    - **Instalar comportamento**: Selecione uma das três opções para como o Gestor de Configuração instala este tipo de implementação. Para obter mais informações sobre estas opções, consulte [a Experiência do Utilizador.](#bkmk_dt-ux)  

    - **Utilize uma ligação VPN automática (se configurada)**: Se tiver implementado um perfil VPN no dispositivo em que o utilizador lança a aplicação, ligue a VPN quando a aplicação começar. Esta opção é apenas para Windows 8.1 e Windows Phone 8.1. Nos dispositivos Windows Phone 8.1, se implementar mais de um perfil VPN para o dispositivo, as ligações VPN automáticas não são suportadas. Para mais informações, consulte [perfis VPN](../../protect/deploy-use/vpn-profiles.md).  

4. Escolha **a seguir**, e continue a aplicar as opções de conteúdo do tipo de [implementação](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a>Especifique manualmente as informações do tipo de implementação  

1. Na página **Geral** do assistente do Tipo de Implantação Create, na lista de drop-down **do Tipo,** escolha o tipo de ficheiro de instalação de aplicação para este tipo de implementação.

2. **Selecione manualmente, especifique manualmente as informações do tipo**de implementação e, em seguida, selecione **Next**.

3. Na página **informação geral** do assistente do Tipo de Implantação Create, especifique um **nome** para o tipo de implementação. Especificar opcionalmente **os comentários do Administrador,** selecione os **Idiomas** para este tipo de implementação e, em seguida, selecione **Next**.  

4. Continue a aplicar as opções de conteúdo do [tipo de implementação](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a>Opções de **conteúdo** do tipo de implementação  

Na página **conteúdo,** especifique as seguintes informações:  

> [!Note]  
> Quando vê as propriedades de um tipo de implementação existente, algumas destas opções aparecem no separador **Conteúdo** e algumas no separador **Programas.**  

- **Localização**do conteúdo : Especifique a localização do conteúdo para este tipo de implementação ou **selecione Navegar** para escolher a pasta de conteúdo do tipo de implementação.  

    > [!IMPORTANT]  
    > A conta System do computador do servidor do site deve ter permissões para a localização do conteúdo especificado.  

  - **Persistir conteúdo na cache do cliente**: O cliente do Gestor de Configuração mantém indefinidamente na sua cache o conteúdo do tipo de implementação. O cliente persiste o conteúdo mesmo que a app já esteja instalada. Esta opção é útil com algumas implementações, como o software baseado no Windows Installer. O Instalador do Windows necessita de uma cópia local do conteúdo de origem para a aplicação de atualizações. Esta opção reduz o espaço de cache disponível. Se selecionar esta opção, pode causar uma grande falha numa grande implementação se a cache não tiver espaço disponível suficiente.  

- Programa de **instalação**: Especifique o nome do programa de instalação e os parâmetros de instalação necessários.  

  - **Início da instalação :** Especificar opcionalmente a pasta que tem o programa de instalação para o tipo de implantação. Esta pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta do ponto de distribuição que tem os ficheiros de instalação.  

- **Desinstalar o programa**: Especificar opcionalmente o nome do programa de desinstalação e os parâmetros necessários.  

  - **Desinstalar o início :** Especificar opcionalmente a pasta que tem o programa de desinstalação para o tipo de implementação. Esta pasta pode ser um caminho absoluto para o cliente. Também pode ser um caminho relativo num ponto de distribuição da pasta com o pacote.  

- **Programa de reparação**: Para os tipos de instalação do Instalador de Janelas e do Instalador de Scripts, especifique opcionalmente o nome do programa de reparação e os parâmetros necessários.<!--1357866-->  

  - **Reparação em**: Especificar opcionalmente a pasta que tem o programa de reparação para o tipo de implementação. Esta pasta pode ser um caminho absoluto para o cliente. Também pode ser um caminho relativo num ponto de distribuição da pasta com o pacote.  

- Executar a **instalação e desinstalar o programa como processo de 32 bits em clientes de 64 bits**: Utilize os locais de ficheiros e registos de 32 bits em computadores baseados no Windows para executar o programa de instalação para o tipo de implementação.  

#### <a name="deployment-type-properties-content-options"></a>Propriedades do tipo de implementação **Opções** de conteúdo

Quando visualiza as propriedades de um tipo de implementação, as seguintes opções aparecem apenas no separador **Conteúdo:**

- **Desinstalar as definições**de conteúdo:  

  - **Mesmo que instalar conteúdo**: Se o conteúdo de instalação e desinstalação for o mesmo, selecione esta opção. Esta é a opção predefinida.  

  - **Não instale conteúdo**: Se a sua aplicação não necessitar de conteúdo para desinstalar, selecione esta opção.  

  - **Diferente do conteúdo de instalação**: Se o conteúdo desinstalar for diferente do conteúdo de instalação, selecione esta opção.  

    - **Desinstalar**a localização do conteúdo : Especifique a rota de rede para o conteúdo utilizado para desinstalar a aplicação.  

- Permitir que os **clientes utilizem pontos de distribuição do grupo**de limites do site padrão : Especifique se os clientes devem descarregar e instalar o software a partir de um ponto de distribuição no grupo de limites padrão do site quando o conteúdo não estiver disponível a partir de um ponto de distribuição nos grupos de fronteira atuais ou vizinhos.  

- **Opções de implementação**: Especifique se os clientes devem descarregar a aplicação quando utilizam um ponto de distribuição de um vizinho ou dos grupos de fronteira do site predefinido.  

- **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para mais informações, consulte [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A BranchCache está sempre ativada nos clientes. Esta definição foi removida na versão 1802, uma vez que os clientes usam branchCache se o ponto de distribuição o suportar.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a>Opções de sequência de **tarefas** do tipo de implementação

<!--3555953-->

Para obter mais informações sobre o tipo de implementação da sequência de tarefas a partir da versão 2002, consulte o tipo de implementação da [sequência de tarefas](../get-started/creating-windows-applications.md#bkmk_tsdt).

Na página da Sequência de **Tarefas,** especifique as seguintes informações:

- **Instale a sequência**de tarefas : Selecione uma sequência de tarefas que execute o processo de instalação para esta aplicação.

- **Desinstale** a sequência de tarefas (opcional): Selecione uma sequência de tarefas que remova esta aplicação.

> [!TIP]  
> Se a sua sequência de tarefas não aparecer na lista, verifique duas vezes se não inclui quaisquer etapas de implementação de OS ou de atualização do OS. Também confirme que não está marcada como uma sequência de tarefas de alto impacto. Para obter mais informações, reveja os pré-requisitos para o tipo de implantação da [sequência de tarefas](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a>Opções do método de **deteção do** tipo de implementação

Este procedimento estabelece um método de deteção que indica a presença do tipo de implantação. Ou seja, se o dispositivo Windows já tem a aplicação instalada. Utilize um dos dois seguintes métodos para criar um método de deteção:

- [Configure regras para detetar a presença deste tipo de implementação](#bkmk_detect-rule)
- [Use um script personalizado para detetar a presença deste tipo de implementação](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a>Configure regras para detetar a presença deste tipo de implementação

1. Na página Método de **Deteção,** a opção de **configurar regras para detetar a presença deste tipo de implementação** é selecionada por padrão. Selecione **Adicionar Cláusula**.  

2. Na caixa de diálogo da regra de **deteção,** selecione um tipo de **definição** para detetar a presença do tipo de implantação:  

    - **Sistema de Ficheiros**: Detete se existe um ficheiro ou pasta especificado num dispositivo. Esta deteção indica que a aplicação está instalada. Especifique os seguintes detalhes adicionais:  

        - **Tipo:** Selecione se se trata de um ficheiro ou pasta.  

        - **Caminho** (Obrigatório): Insira ou navegue no caminho local no dispositivo que inclui o ficheiro ou pasta. Por exemplo, `C:\Program Files`. Não pode especificar um caminho de rede partilhado. Se selecionar **Navegar,** navegue no sistema de ficheiros local ou ligue-se a um cliente representativo para navegar.  

        - **Nome de ficheiro ou pasta** (Obrigatório): Especifique o ficheiro ou nome de pasta específico para detetar no caminho acima. Se o cliente detetar este ficheiro ou pasta no dispositivo, considera a aplicação como instalada no dispositivo.  

        - **Este ficheiro ou pasta está associado a uma aplicação de 32 bits em sistemas de 64 bits**: Esta opção é selecionada por padrão. O cliente verifica primeiro as localizações dos ficheiros de 32 bits para o ficheiro ou pasta especificado. Se o ficheiro ou pasta não for encontrado, o cliente procura então localizações de 64 bits.  

    - **Registo**: Detete se existe uma chave de registo especificada ou um valor de registo num dispositivo cliente. Esta deteção indica que a aplicação está instalada. Especifique os seguintes detalhes adicionais:  

        - **Colmeia** (Necessária): Escolha uma colmeia de registo da lista de abandono. Por exemplo, `HKEY_LOCAL_MACHINE`.  

        - **Chave** (Requerida): Especifique a chave de registo para procurar na colmeia acima. Por exemplo, `SOFTWARE\Microsoft\Office`.  

        - **Valor** (Opcional): Introduza um valor específico para detetar na tecla acima. Se pretender que o cliente detete o valor (Padrão), ative a opção **de utilizar o valor-chave do registo (Predefinido) para deteção**. Quando introduz um valor ou ativa esta opção, é necessário selecionar um Tipo de **Dados**.  

        - Esta chave de **registo está associada a uma aplicação de 32 bits em sistemas de 64 bits:** Selecione esta opção para verificar primeiro os locais de registo de 32 bits para a chave de registo especificada. Se a chave do registo não for encontrada, o cliente procura em 64 bits locais.  

    - **Instalador do Windows**: Detete se existe um ficheiro instalador do Windows especificado num dispositivo cliente. Esta deteção indica que a aplicação está instalada. Especifique o código do **Produto** MSI para detetar no cliente. Se selecionar **Browse,** escolha o ficheiro MSI para ler o código do produto.

3. Na parte inferior da janela da regra de deteção, especifique se o artigo deve existir ou satisfazer uma regra. Por exemplo, se detetar com um ficheiro, a seguinte opção é selecionada por defeito: A definição do sistema de **ficheiros deve existir no sistema-alvo para indicar a presença desta aplicação**. Selecione a outra opção para criar uma regra de deteção com base em propriedades de ficheiros ou pastas. Estas propriedades incluem data modificada, data criada, versão ou tamanho. Estes critérios de regra são diferentes para cada tipo de definição.  

4. Selecione **OK** para fechar a caixa de diálogo da Regra de **Deteção.**  

Quando se cria mais do que um método de deteção para um tipo de implementação, pode agrupar cláusulas para criar uma lógica mais complexa.  

#### <a name="group-detection-clauses-optional"></a>Cláusulas de deteção de grupos *(opcional)*

1. Crie três ou mais cláusulas de método de deteção num tipo de implementação.  

2. Selecione duas ou mais cláusulas consecutivas e, em seguida, selecione **Grupo**. Verá os parênteses adicionados às colunas associadas, que mostram onde o grupo começa e termina.  

    Exemplo:

    | Conector  |  ( | Cláusula           |  )  |
    |------------|----|------------------|-----|
    |            |    | Código do Produto MSI |     |
    | Ou         | (  | file1.texto existe|     |
    | E        |    | file2.txt existe | )   |

3. Para remover o grupo, selecione as cláusulas agruparadas e, em seguida, selecione **Ungroup**.  

*Continue* para a secção seguinte sobre a utilização de um script personalizado como método de deteção. Ou *saltar* para as opções [de Experiência do Utilizador](#bkmk_dt-ux) para o tipo de implementação.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a>Use um script personalizado para verificar a presença de um tipo de implementação  

1. Na página Método de **Deteção,** selecione um script personalizado para detetar a presença desta caixa **de tipo de implementação.** Em seguida, selecione **Editar**.  

2. Na caixa de diálogo do **Editor do Script,** selecione um **tipo de Script** para detetar o tipo de implementação: PowerShell, VBScript ou JScript.  

    > [!Note]  
    > Quando um script do Windows PowerShell funciona como um método de `-NoProfile` deteção de aplicações, o cliente do Gestor de Configuração chama powerShell com o parâmetro. Esta opção inicia a PowerShell sem perfis. Um perfil PowerShell é um script que corre quando o PowerShell começa. <!--3607762-->  

3. Na caixa de conteúdo do **Script,** introduza o script que pretende utilizar, ou colá-lo no conteúdo de um script existente. Escolha **o Open** para navegar num script guardado existente. Selecione **Clear** para remover o texto no campo de conteúdo do Script. Se necessário, ative a opção de executar o **script como processo de 32 bits em clientes de 64 bits**.  

    > [!NOTE]  
    > O tamanho máximo para um guião é de 32 KB.  

4. Selecione **OK** para guardar o script e fechar a caixa de diálogo do **Script Editor.** De volta ao assistente do Tipo de Implementação Create, a atualização dos campos **do Script Type** e script **Length** com detalhes sobre o seu script.

#### <a name="about-custom-script-detection-methods"></a>Sobre métodos personalizados de deteção de scripts  

O Gestor de Configuração verifica os resultados do script. Lê os valores escritos pelo script no fluxo de saída padrão (STDOUT), no fluxo de erro padrão (STDERR) e no código de saída. Se o script sair com um valor não zero, o script falha e o estado de deteção da aplicação é *Desconhecido*. Se o código de saída for zero e o STDOUT tiver dados, o estado de deteção da aplicação está *instalado*.

> [!TIP]
> Ao escrever um script de deteção, se devolver um código de saída zero mas não devolver a saída (dados em STDOUT), a aplicação não será detetada conforme instalada. Para mais informações, consulte os seguintes exemplos.

Utilize as seguintes tabelas para verificar se uma aplicação é instalada a partir da saída a partir de um script:  

##### <a name="zero-exit-code"></a>Código de saída zero

|STDOUT|STDERR|Resultado do script|Estado de deteção de aplicações|
|---------|---------|---------|---------|
|Vazio|Vazio|Êxito|Não instalado|
|Vazio|Não está vazio.|Falha|Desconhecido|
|Não está vazio.|Vazio|Êxito|Instalado|
|Não está vazio.|Não está vazio.|Êxito|Instalado|

##### <a name="non-zero-exit-code"></a>Código de saída não zero

|STDOUT|STDERR|Resultado do script|Estado de deteção de aplicações|
|---------|---------|---------|---------|
|Vazio|Vazio|Falha|Desconhecido|
|Vazio|Não está vazio.|Falha|Desconhecido|
|Não está vazio.|Vazio|Falha|Desconhecido|
|Não está vazio.|Não está vazio.|Falha|Desconhecido|

##### <a name="examples"></a>Exemplos

Utilize os seguintes exemplos PowerShell/VBScript para escrever os seus próprios scripts de deteção de aplicações:  

**Exemplo 1:** O script devolve um código de saída que não é zero. Este código indica que o script não foi executado com sucesso. Neste caso, o estado de deteção de aplicação é desconhecido.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Exemplo 2:** O script devolve um código de saída de zero, mas o valor do STDERR não está vazio. Este resultado indica que o script não correu com sucesso. Neste caso, o estado de deteção de aplicação é desconhecido.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Exemplo 3:** O script devolve um código de saída de zero, o que indica que funcionou com sucesso. No entanto, o valor para o STDOUT está vazio, o que indica que a aplicação não está instalada.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Exemplo 4:** O script devolve um código de saída de zero, o que indica que funcionou com sucesso. O valor para O DSTOUT não está vazio, o que indica que a aplicação está instalada.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Exemplo 5:** O script devolve um código de saída de zero, o que indica que funcionou com sucesso. Os valores para STDOUT e STDERR não estão vazios, o que indica que a aplicação está instalada.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a>Opções de experiência do tipo de **utilização do** tipo de implementação

Estas definições especificam como o cliente instala a aplicação nos dispositivos e o que o utilizador vê.  

Na página **Experiência de Utilizador** , especifique as seguintes informações:  

- **Comportamento de instalação**: Na lista de abandono, selecione uma das seguintes opções:  

  - **Instalação para utilizador**: O cliente apenas instala a aplicação para o utilizador a quem implementa a aplicação.  

  - **Instalação para sistema**: O cliente instala a aplicação apenas uma vez. Está disponível para todos os utilizadores.  

  - **Instale para sistema se o recurso for dispositivo; caso contrário, instale para o utilizador**: Se implementar a aplicação num dispositivo, o cliente instala-o para todos os utilizadores. Se implementar a aplicação a um utilizador, o cliente apenas a instala para esse utilizador.  

- **Requisito de início**de sessão : Selecione uma das seguintes opções:  

  - **Apenas quando um utilizador tiver sessão iniciada**  

  - **Se um utilizador está ou não ligado**  

  - **Só quando nenhum utilizador é ligado**  

    > [!NOTE]  
    > Esta opção não se aplica **apenas quando um utilizador é iniciado**. Se selecionar **Instalar para utilizador** na lista de desavenças do comportamento da **Instalação,** não pode alterar esta opção.  

- Visibilidade do programa de **instalação**: Especifique o modo em que o tipo de implementação funciona nos dispositivos do cliente. Selecione uma das seguintes opções:  

  - **Maximizado**: O tipo de implementação é maximizado nos dispositivos do cliente. Os utilizadores vêem toda a atividade de instalação.  

  - **Normal**: O tipo de implementação funciona no modo normal com base nas predefinições do sistema e do programa. Este é o modo predefinido.  

  - **Minimizado**: O tipo de implementação é minimizado nos dispositivos do cliente. Os utilizadores podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

  - **Ocultado**: O tipo de implementação é ocultado em dispositivos de cliente. Os utilizadores não vêem nenhuma atividade de instalação.  

- **Permitir que os utilizadores vejam e interajam com a instalação do programa**: Especifique se um utilizador pode interagir com a instalação do tipo de implementação para configurar as opções de instalação.  

    Se selecionou a opção **de instalação para opção de utilizador** na lista de desativação do comportamento da **Instalação,** esta opção está ativada por predefinição.  

    > [!IMPORTANT]  
    > Quando selecionar a **Instalação para** o comportamento do sistema, esta definição é opcional. Esta alteração destina-se principalmente a permitir que um utilizador final interaja com a instalação durante uma sequência de tarefas. Por exemplo, executar um processo de configuração que leva o utilizador final para várias opções. Alguns instaladores de aplicações não podem ter pedidos de utilizador silenciados, ou o processo de instalação pode exigir valores de configuração específicos apenas conhecidos do utilizador. <!--1356976-->  
    >  
    > Instalar no contexto do sistema e permitir que os utilizadores interajam com a instalação não é uma configuração segura. Para mais informações, consulte [segurança e privacidade para a gestão de aplicações.](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact)  

- **Máximo tempo de execução permitido (minutos)**: Especifique o tempo máximo em minutos que espera que o tipo de implementação seja executado no computador cliente. Especifique esta definição como um número inteiro superior a zero. O valor predefinido é de 120 minutos (duas horas).  

    Utilize este valor para as seguintes ações:  

  - Para monitorizar os resultados do tipo de implantação.  

  - Para verificar se um tipo de implementação é instalado quando define janelas de manutenção em dispositivos clientes. Quando uma janela de manutenção está no lugar, um tipo de implantação só começa se houver tempo suficiente disponível na janela de manutenção para acomodar a definição de tempo de **execução máximo permitido.**  

    > [!IMPORTANT]  
    > Pode ocorrer um conflito se o **tempo máximo de execução permitido** for mais longo do que a janela de manutenção programada. Se o utilizador definir o tempo máximo de funcionamento para um período superior ao comprimento de qualquer janela de manutenção disponível, esse tipo de implantação não funciona.  

- Tempo estimado de **instalação (minutos)**: Especifique o tempo estimado de instalação do tipo de implantação. Os utilizadores vêem desta vez no Centro de Software.  

#### <a name="deployment-type-properties-user-experience-options"></a>Propriedades do tipo de implementação Opções **de experiência de utilizador**

Quando vê as propriedades de um tipo de implementação, as seguintes opções aparecem apenas no separador **User Experience:**

Impor comportamentos específicos de pós-instalação. Selecione uma das seguintes opções:  

- **Determine o comportamento com base nos códigos**de devolução : Manuseie reboots com base nos códigos configurados no separador **Might Require a Reboot** [Códigos de Retorno.](#bkmk_dt-return) Se um utilizador for contratado durante a instalação, é solicitado dependendo da configuração da Experiência do Utilizador *da implementação.*  

- **Sem ação específica**: Não é necessário reiniciar após a instalação. O Centro de Software informa que não é necessário reiniciar.  

- O programa de **instalação do software pode forçar o reinício do dispositivo:** O Gestor de Configuração não controla ou inicia um reboot, mas a instalação real pode fazê-lo sem aviso prévio. Utilize esta definição para evitar que o Gestor de Configuração reporte falhas de instalação quando o instalador iniciar uma reinicialização. Os ecrãs do Centro de Software **podem necessitar de um reboot**.  

- O cliente do Gestor de **Configuração forçará um reinício obrigatório**do dispositivo: O Gestor de Configuração obriga um reboot do dispositivo após uma instalação bem sucedida. O Centro de Software informa que é necessário reiniciar. Se um utilizador for contratado durante a instalação, é solicitado dependendo da configuração da Experiência do Utilizador *da implementação.*  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Requisitos do** tipo de implantação

O Gestor de Configuração verifica estes requisitos nos dispositivos antes de instalar o tipo de implementação. Utilize requisitos para aperfeiçoar e controlar ainda mais os dispositivos ou utilizadores que recebem esta aplicação. Por exemplo, se implementar a aplicação para uma recolha de utilizadores, especifique os requisitos de hardware da aplicação aqui.

1. Na página **Requisitos,** selecione **Adicionar** para abrir a caixa de diálogo **Criar Requisitos.**  

2. Na lista de abandono da **categoria,** selecione se este requisito é para um **Dispositivo** ou um **Utilizador**.  

    Selecione **Custom** para usar uma condição global previamente criada. Quando selecionar **Personalizado,** também pode escolher **criar** uma nova condição global. Para saber mais sobre as condições globais, consulte [Como criar condições globais.](create-global-conditions.md)  

    > [!IMPORTANT]  
    > Se implementar a aplicação numa recolha de dispositivos, o cliente ignora qualquer exigência da categoria **Utilizador** e da condição **Dispositivo Primário**.  

3. Na lista de desistência da **Condição,** selecione a condição para avaliar se o utilizador ou o dispositivo cumprem os requisitos de instalação. O conteúdo desta lista varia consoante a categoria selecionada.  

4. Na lista de desistência do **Operador,** selecione o operador para utilizar. Este operador compara a condição selecionada com o valor especificado. Avalia se o utilizador ou o dispositivo cumprem os requisitos de instalação. Os operadores disponíveis variam consoante a condição selecionada.  

    > [!Note]  
    > Os requisitos disponíveis diferem consoante o tipo de dispositivo que o tipo de implementação utiliza.  

5. Na caixa **Valor,** especifique os valores a utilizar para comparação. Estes valores, juntamente com a condição selecionada e o operador, avaliam se o utilizador ou o dispositivo cumprem os requisitos de instalação. Os valores disponíveis variam consoante a condição selecionada e o operador selecionado.  

6. Escolha **OK** para salvar o requisito e feche a caixa de diálogo **Create Requirement.**  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>Tipo de implantação **Dependências**  

As dependências definem um ou mais tipos de implementação de outra aplicação que o cliente deve instalar antes de instalar este tipo de implementação.

> [!IMPORTANT]  
> Em alguns casos, um tipo de implantação depende de um tipo de implantação que também tem dependências. O número máximo de dependências suportadas na cadeia é de cinco.  

1. Na página **Dependências,** selecione **Adicionar**.  

2. Na janela Dependência Add, introduza o nome do **grupo Dependência**. Este nome refere-se a este grupo de dependências de aplicações.  

3. Na janela Adicionar Dependência, **selecione Adicionar**.  

4. Na janela **'Especte' de aplicação,** selecione uma aplicação disponível e pelo menos um dos seus tipos de implementação para utilizar como dependência.  

    > [!TIP]  
    > Selecione **Vista** para mostrar as propriedades da aplicação ou do tipo de implementação selecionados.  

5. Selecione **OK** para fechar a janela **de aplicação requerida especificada.**  

6. Se pretender que o cliente instale automaticamente a aplicação dependente, selecione **Instalar automaticamente** ao lado da dependência.  

    > [!NOTE]  
    > Não precisa de implementar uma aplicação dependente para o cliente instalá-la automaticamente.  

7. Se adicionar mais do que uma dependência, utilize os botões **Aumentar prioridade** e **Diminuir Prioridade.** Estas ações alteram a ordem em que o cliente avalia cada dependência.  

8. Selecione **OK** para fechar a janela **Adicionar Dependência.**  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>Códigos de **devolução** do tipo de implementação

> [!Note]  
> Esta página não está no assistente do Tipo de Implementação Create. É apenas uma conta sobre as propriedades de um tipo de implantação existente.  

Especifique códigos de devolução para controlar comportamentos após o tipo de implementação estar concluído. Por exemplo, sinal de que é necessário reiniciar, a instalação está completa.

1. No separador **Códigos** de Retorno da janela de propriedades do tipo de implementação, **selecione Adicionar**.  

2. Na janela Adicionar Código de Devolução, especifique o **Valor do Código de Retorno** que espera deste tipo de implementação. Este valor é qualquer inteiro positivo `-2147483648` `2147483647`ou negativo entre e .  

3. Selecione um **Código Tipo** da lista de lançamentos. Esta definição define como o Gestor de Configuração interpreta o código de retorno especificado deste tipo de implementação. Os tipos disponíveis variam em função da tecnologia do tipo de implementação.  

    - **Sucesso (sem reinicialização)**: O tipo de implantação instalado com sucesso e não é necessário reiniciar.  

    - **Falha (sem reinicialização)**: O tipo de implantação falhou na instalação.  

    - **Reinicialização difícil**: O tipo de implementação foi instalado com sucesso, mas requer que o dispositivo reinicie. Nada mais pode ser instalado até que o dispositivo reinicie.  

    - **Soft Reboot**: O tipo de implementação foi instalado com sucesso, mas solicita ao dispositivo que reinicie. Outras instalações podem ocorrer antes do reinício do dispositivo.  

    - **Fast Retry**: Outra instalação já está em andamento no dispositivo. O cliente tenta a cada duas horas, num total de 10 vezes.  

4. Opcionalmente, introduza um **Nome** e **Descrição** para este código de devolução.

5. Selecione **OK** para fechar a janela Adicionar Código de Devolução.  

#### <a name="example-non-zero-success"></a>Exemplo: sucesso não-zero

Está a implementar uma aplicação que `1` devolve um código de saída de quando instala com sucesso. Por predefinição, o Gestor de Configuração deteta este código de devolução não zero como uma falha. Especifique o `1`valor do código de devolução de , e selecione o Tipo de Código de **Sucesso (sem reboot)**. Agora O Gestor de Configuração interpreta o código de devolução como um sucesso para este tipo de implementação.

#### <a name="default-return-codes"></a>Códigos de devolução predefinidos

Quando cria alguns tipos de implementação, o Gestor de Configuração adiciona automaticamente os seguintes códigos de devolução que são comuns a essa tecnologia:  

##### <a name="windows-installer-msi-file"></a>Instalador windows\*(ficheiro .msi)

|Valor    |Tipo de Código|
|---------|---------|
|0        |Sucesso (sem reinicialização)|
|1707     |Sucesso (sem reinicialização)|
|3010     |Soft Reboot|
|1641     |Reinicialização difícil|
|1618     |Retry rápido|

##### <a name="script-installer"></a>Programa de Instalação de Scripts

|Valor    |Tipo de Código|
|---------|---------|
|0        |Sucesso (sem reinicialização)|
|1641     |Reinicialização difícil|
|3010     |Soft Reboot|
|1618     |Retry rápido|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Pacote de\*aplicativos Windows \*(.appx, .appxbundle, \*.msix, \*.msixbundle)

|Valor    |Tipo de Código|
|---------|---------|
|15605    |Retry rápido|
|15618    |Retry rápido|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a>Opções adicionais para tipos de implementação app-V  

Configure opções adicionais que sejam exclusivas dos tipos de implementação para aplicações virtuais (App-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a>Opções de **conteúdo** do tipo de implementação App-V  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**  

2. Selecione uma aplicação com um tipo de implementação App-V e selecione **Propriedades**.  

3. Nas propriedades da aplicação, mude para o separador Tipos de **Implementação.** Selecione o tipo de implementação App-V e **selecione Editar**.  

4. Nas propriedades do tipo de implementação, mude para o separador **Conteúdo.** Configure as seguintes opções conforme necessário:  

    - **Persistir conteúdo na cache do cliente**: O cliente do Gestor de Configuração não excluirá da sua cache o conteúdo para este tipo de implementação.  

    - **Carregue o conteúdo em cache App-V antes**do lançamento : Antes do início da aplicação, o cliente do Gestor de Configuração carrega na cache App-V todos os conteúdos para este tipo de implementação. O cliente não coloca o conteúdo na cache. Elimina o conteúdo conforme necessário.  

5. Selecione **OK** para fechar as propriedades do tipo de implementação. Em seguida, selecione **OK** para fechar as propriedades da aplicação.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a>Opções de **publicação** do tipo app-V

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**  

2. Selecione uma aplicação com um tipo de implementação App-V e selecione **Propriedades**.  

3. Nas propriedades da aplicação, mude para o separador Tipos de **Implementação.** Selecione o tipo de implementação App-V e **selecione Editar**.  

4. Nas propriedades do tipo de implementação, altere para o separador **Publishing.** Selecione os itens na aplicação virtual que pretende publicar.  

5. Selecione **OK** para fechar as propriedades do tipo de implementação. Em seguida, selecione **OK** para fechar as propriedades da aplicação.  

## <a name="import-an-application"></a><a name="bkmk_import"></a>Importar um pedido  

Utilize o seguinte procedimento para importar uma aplicação para o Gestor de Configuração:

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**  

2. Na fita, no separador **Home** e no grupo **Criar,** selecione **Aplicação de Importação**.  

3. Na página **geral** do Assistente de Aplicação de Importação, especifique a rota de rede para o **Ficheiro** para importar. Por exemplo, `\\server\share\file.zip`. Este ficheiro é um arquivo comprimido válido (formato ZIP) de uma aplicação de Gestor de Configuração exportada.  

4. Na página de Conteúdo de **Ficheiros,** selecione a ação a tomar se esta aplicação for uma duplicação de uma aplicação existente. Crie uma nova aplicação, ou ignore a duplicação e adicione uma nova revisão à aplicação existente.  

5. Na página **resumo,** reveja as ações e, em seguida, termine o assistente.  

A nova aplicação aparece no nó **Aplicações**.  

> [!TIP]  
> O Windows PowerShell cmdlet **Import-CMApplication** tem a mesma função que este procedimento. Para mais informações, consulte [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Para obter mais informações sobre como exportar um pedido, consulte as tarefas de [Gestão para aplicações.](management-tasks-applications.md)

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a>Tipos de implementação suportados  

O Gestor de Configuração suporta os seguintes tipos de implementação para aplicações:

| Nome do tipo de implementação | Descrição |
|--------------------------|----------------------|  
| **Instalador windows\*(ficheiro .msi)** | Um ficheiro instalador do Windows. |  
| **Pacote de\*aplicativos Windows \*(.appx, .appxbundle, \*.msix, \*.msixbundle)** | Um ficheiro de pacote de aplicativos Windows (.appx), um pacote de pacote de aplicativos Windows (.appxbundle), um pacote de aplicativos Windows 10 (.msix) ou pacote de aplicativos Windows 10 (.msixbundle).<!--1357427--> |  
| **Pacote de aplicações do Windows (na Loja Windows)** | Especifique um link para a aplicação na Windows Store ou navegue na loja para selecionar a aplicação.<sup>[Nota 1](#bkmk_note1)</sup> |  
| **Programa de Instalação de Scripts** | Especifique um script ou programa que seja executado em clientes do Windows para instalar conteúdo ou para fazer uma ação. Utilize este tipo de implementação para instaladores de configuração.exe ou invólucros de script. |  
| **Microsoft Application Virtualization 4** | Um manifesto Microsoft App-V v4. |  
| **Virtualização da aplicação da Microsoft 5** | Um ficheiro de pacote Microsoft App-V v5. |  
| **Pacote de aplicativo\*seletiva Windows Phone (ficheiro .xap)** | Um ficheiro de pacote de aplicativos Windows Phone. |  
| **Pacote de aplicação do Windows Phone (na Loja Windows Phone)** | Especifique um link para a aplicação na Windows Store. |  
| **Mac OS X** | Para computadores macOS que executam o cliente do Gestor de Configuração. Crie um ficheiro .cmmac com a ferramenta **CMAppUtil.** |  
| **Aplicação Web** | Especifique um link para uma aplicação web. Este tipo de implementação instala um atalho para a aplicação web no dispositivo do utilizador. |  
| **Instalador de Janelas através do MDM (.msi)\*** | Criar e implementar aplicações baseadas no Windows Installer para dispositivos Windows 10. Para mais informações, consulte implementar aplicações do [Instalador do Windows para dispositivos Windows 10 matriculados no MDM.](../get-started/creating-windows-applications.md#bkmk_mdm-msi) |
| **Sequência de tarefas** | A partir da versão 2002, instale ou desinstale aplicações complexas utilizando sequências de tarefas. Para mais informações, consulte o tipo de implementação da [sequência de tarefas](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> A consola 'Gestor de Configuração' pode apresentar outros tipos de implementação, mas são para plataformas que já não são suportadas. Para mais informações, veja [o que aconteceu ao híbrido?](../../mdm/understand/what-happened-to-hybrid.md)

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a>Nota 1: Pacote de aplicativos Windows (na Windows Store)

Para implementar a aplicação como um link para a Windows Store, configure a política do grupo **Desligue a aplicação Store**. Desative esta política para **Desativado** ou **Não configurado**. Se ativar esta definição, os clientes não podem ligar-se à Windows Store para descarregar e instalar aplicações.

Os clientes do Windows avaliam sempre os tipos de implementação que utilizam uma ligação a uma loja antes de outros tipos de implementação. Em seguida, o cliente avalia os tipos de implementação por prioridade.

> [!TIP]
> Alguns links de loja podem causar o seguinte erro no Assistente de Aplicação Criar: "Ligação de aplicação inválida". Por exemplo, algumas *aplicações em destaque* podem causar este erro. Ainda pode selecionar **Next** na página **geral** do assistente. O Gestor de Configuração cria com sucesso a aplicação e pode implantá-la com sucesso.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Passos seguintes

Depois de criar uma aplicação no Gestor de Configuração, o próximo passo é [implementar a aplicação](deploy-applications.md).

A partir da versão 1906, criar um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação. Para mais informações, consulte [Criar grupos](create-app-groups.md)de aplicação .

Para obter mais informações sobre a criação de aplicações em diferentes plataformas de SO, consulte os seguintes artigos:  

- [Criar aplicações Windows](../get-started/creating-windows-applications.md)
- [Criar aplicações Mac](../get-started/creating-mac-computer-applications.md)
- [Criar aplicações de servidor Linux e UNIX](../get-started/creating-linux-and-unix-server-applications.md)
- [Criar aplicações Windows Embedded](../get-started/creating-windows-embedded-applications.md)
