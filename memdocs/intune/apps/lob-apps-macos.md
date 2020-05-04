---
title: Como adicionar aplicações de linha de negócio macOS ao Microsoft Intune
titleSuffix: ''
description: Saiba como adicionar aplicações de linha de negócio (LOB) macOS ao Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ef8008ac-8b85-4bfc-86ac-1f9fcbd3db76
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6dad4dffba0efadcca0ea5eb7d61960bec1b3f8e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80536824"
---
# <a name="how-to-add-macos-line-of-business-lob-apps-to-microsoft-intune"></a>Como adicionar aplicações de linha de negócio (LOB) macOS ao Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Utilize as informações neste artigo para adicionar aplicações de linha de negócio macOS ao Microsoft Intune. Tem de transferir uma ferramenta externa para pré-processar os ficheiros *.pkg* para poder carregar o ficheiro de linha de negócio para o Microsoft Intune. O pré-processamento dos ficheiros *.pkg* tem de ser realizado num dispositivo macOS.

> [!NOTE]
> Começando com o lançamento do macOS Catalina 10.15, antes de adicionar as suas aplicações ao Intune, verifique se as suas aplicações macOS LOB estão anotadas. Se os desenvolvedores das suas aplicações LOB não notarizarem as suas aplicações, as aplicações deixarão de funcionar nos dispositivos macOS dos seus utilizadores. Para mais informações sobre como verificar se uma aplicação está anotada, visite a [Notarize as suas aplicações macOS para se preparar para o macOS Catalina](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Notarizing-your-macOS-apps-to-prepare-for-macOS/ba-p/808579).

> [!NOTE]
> Apesar de os utilizadores de dispositivos macOS poderem remover algumas das aplicações macOS incorporadas, tais como Bolsa e Mapas, não pode utilizar o Intune para implementar novamente essas aplicações. Se os utilizadores finais eliminarem essas aplicações, têm de aceder à App Store e reinstalar manualmente.

## <a name="before-your-start"></a>Antes de começar

Tem de descarregar uma ferramenta externa, marcar a ferramenta descarregada como executável e pré-processar os seus ficheiros *.pkg* com a ferramenta antes de poder carregar o ficheiro de linha de negócios para o Microsoft Intune. O pré-processamento dos ficheiros *.pkg* tem de ser realizado num dispositivo macOS. Utilize a Ferramenta de Encapsulamento de Aplicações do Intune para Mac para permitir que as aplicações Mac sejam geridas pelo Microsoft Intune.

> [!IMPORTANT]
> O ficheiro *.pkg* deve ser assinado com o certificado "Developer ID Installer", obtido a partir de uma conta Apple Developer. Apenas os ficheiros *.pkg* podem servir para carregar aplicações LOB macOS para o Microsoft Intune. A conversão de outros formatos, como *.dmg* em *.pkg*, não é suportada.
>

1. Descarregue a ferramenta de embrulho de [aplicativos Intune para Mac](https://github.com/msintuneappsdk/intune-app-wrapping-tool-mac).

    > [!NOTE]
    > A **Ferramenta de Encapsulamento de Aplicações do Intune para Mac** tem de ser executada numa máquina macOS. 

2. Marque a ferramenta descarregada como executável:
   - Inicie a aplicação de terminais.
   - Mude o diretório para `IntuneAppUtil` o local onde está localizado.
   - Execute o seguinte comando para tornar a ferramenta executada:<br> 
       `chmod +x IntuneAppUtil`

3. Utilize o comando `IntuneAppUtil` na **Ferramenta de Encapsulamento de Aplicações do Intune para Mac** para encapsular o ficheiro da aplicação LOB *.pkg* num ficheiro *.intunemac*.<br>

    Comandos de exemplo a utilizar para a Ferramenta de Encapsulamento de Aplicações do Intune para Mac:
    > [!IMPORTANT]
    > Certifique-se `<source_file>` de que o argumento `IntuneAppUtil` não contém espaços antes de executar os comandos.

    - `IntuneAppUtil -h`<br>
    Este comando mostra informações de utilização da ferramenta.
    
    - `IntuneAppUtil -c <source_file> -o <output_directory_path> [-v]`<br>
    Este comando irá embrulhar o ficheiro de `<source_file>` aplicação *.pkg* LOB fornecido num ficheiro *.intunemac* com o mesmo nome e colocá-lo na pasta apontada por `<output_directory_path>`.
    
    - `IntuneAppUtil -r <filename.intunemac> [-v]`<br>
    Este comando extrai os parâmetros detetados e a versão do ficheiro *.intunemac* criado.

## <a name="select-the-app-type"></a>Selecione o tipo de aplicativo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **Todas as aplicações** > **Adicionar**.
3. No painel do **tipo de aplicação Select,** sob os **outros** tipos de aplicações, selecione **app Line-of-business**.
4. Clique em **Selecionar**. Os passos da **aplicação Add** são apresentados.

## <a name="step-1---app-information"></a>Passo 1 - Informações sobre aplicativos

### <a name="select-the-app-package-file"></a>Selecione o ficheiro de pacote de aplicativos

1. No painel de **aplicações Adicionar,** clique em Selecionar o ficheiro de pacote de **aplicativos**. 
2. No painel **Ficheiro de pacote de aplicação**, selecione o botão Procurar. Em seguida, selecione um ficheiro de instalação macOS com a extensão *.intunemac*.
   Os detalhes da aplicação serão apresentados.
3. Quando terminar, selecione **OK** no painel de **ficheiros** do pacote app para adicionar a aplicação.

### <a name="set-app-information"></a>Definir informações de aplicativos

1. Na página de informações da **App,** adicione os detalhes para a sua aplicação. Consoante a aplicação que tenha escolhido, alguns dos valores neste painel podem ser preenchidos automaticamente.
    - **Nome**: introduza o nome da aplicação tal como aparece no portal da empresa. Certifique-se de que todos os nomes de aplicações que utiliza são exclusivos. Se existir o mesmo nome duas vezes, só aparece uma das aplicações no portal da empresa.
    - **Descrição**: introduza a descrição da aplicação. A descrição aparece no portal da empresa.
    - **Editor**: Insira o nome do editor da app.
    - **Sistema Operativo Mínimo**: na lista, escolha a versão mínima do sistema operativo no qual a aplicação pode ser instalada. Se atribuir a aplicação a um dispositivo com um sistema operativo anterior, não será instalada.
    - **Categoria**: Selecione uma ou mais categorias de aplicações incorporadas ou selecione uma categoria que criou. As categorias permitem que os utilizadores encontrem a aplicação mais facilmente quando procurarem no portal da empresa.
    - **Mostre isto como uma aplicação em destaque no Portal da Empresa**: Mostrar a aplicação em destaque na página principal do portal da empresa quando os utilizadores navegam para apps.
    - **URL de Informações**: opcionalmente, introduza o URL de um site que contenha informações sobre esta aplicação. O URL aparece no portal da empresa.
    - **URL de Privacidade**: opcionalmente, introduza um URL para um site que contenha informações sobre a privacidade desta aplicação. O URL aparece no portal da empresa.
    - **Programador**: opcionalmente, introduza o nome do programador da aplicação.
    - **Proprietário**: opcionalmente, introduza o nome do proprietário desta aplicação. Por exemplo, **Departamento de RH**.
    - **Notas**: introduza quaisquer notas que queira associar a esta aplicação.
    - **Logótipo**: carregue um ícone associado à aplicação. Este ícone é apresentado com a aplicação quando os utilizadores procurarem no portal da empresa.
2. Clique em **Seguir** para exibir a página **de tags scope.**

## <a name="step-2---select-scope-tags-optional"></a>Passo 2 - Selecione etiquetas de âmbito (opcional)

Pode utilizar etiquetas de âmbito para determinar quem pode ver informações sobre aplicações do cliente no Intune. Para mais detalhes sobre etiquetas de âmbito, consulte [Use o controlo de acesso baseado em funções e as etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

1. Clique em **Selecionar etiquetas** de âmbito para adicionar opcionalmente etiquetas de âmbito para a aplicação. 
2. Clique em **Seguir** para exibir a página **de Tarefas.**

## <a name="step-3---assignments"></a>Passo 3 - Atribuições

1. Selecione o **Necessário**, **Disponível para dispositivos matriculados,** ou **desinstale** as atribuições do grupo para a aplicação. Para mais informações, consulte [grupos Add para organizar utilizadores e dispositivos](../fundamentals/groups-add.md) e [atribuir aplicações a grupos com](apps-deploy.md)o Microsoft Intune .
2. Clique em **Seguir** para exibir a página **Review + criar.** 

## <a name="step-4---review--create"></a>Passo 4 - Rever + criar

1. Reveja os valores e configurações que inseriu para a aplicação.
2. Quando terminar, clique em **Criar** para adicionar a app ao Intune.

    A lâmina **de visão geral** para a aplicação de linha de negócio seleção é apresentada.

A aplicação que criou é apresentada na lista de aplicações, onde pode atribuí-la aos grupos que escolher. Para obter ajuda, veja [Como atribuir aplicações a grupos](apps-deploy.md).

> [!NOTE]
> Se o ficheiro *.pkg* contiver várias aplicações ou instaladores de aplicações, o Microsoft Intune apenas comunicará que a *aplicação* foi instalada com êxito quando todas as aplicações instaladas no dispositivo forem detetadas.

## <a name="update-a-line-of-business-app"></a>Atualizar uma aplicação de linha de negócio

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

> [!NOTE]
> Para o serviço do Intune implementar com êxito um novo ficheiro *.pkg* no dispositivo, tem de incrementar o pacote `version` e a cadeia `CFBundleVersion` no ficheiro *packageinfo* do pacote *.pkg*.

## <a name="next-steps"></a>Passos seguintes

- A aplicação que criou é apresentada na lista de aplicações. Agora pode atribuí-la aos grupos que escolher. Para obter ajuda, veja [Como atribuir aplicações a grupos](apps-deploy.md).

- Saiba mais sobre as formas como pode monitorizar as propriedades e atribuições da sua aplicação. Para obter mais informações, consulte [Como monitorizar informações e atribuições da aplicação](apps-monitor.md).

- Saiba mais sobre o contexto da sua aplicação no Intune. Para obter mais informações, consulte [Descrição geral dos ciclos de vida de dispositivos e aplicações](../fundamentals/device-lifecycle.md)
