---
title: Implementar o portal self-service
titleSuffix: Configuration Manager
description: Adicione informações específicas da organização ao portal de self-service de gestão BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713073"
---
# <a name="customize-the-self-service-portal"></a>Implementar o portal self-service

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Depois de [instalar o portal de self-service BitLocker,](setup-websites.md)pode personalizá-lo para a sua organização. Adicione um aviso personalizado, o nome da sua organização e outras informações específicas da organização.

## <a name="branding"></a>Imagem corporativa

Marque o portal de self-service com o nome da sua organização, ajude a secretária URL e note texto.

1. No servidor web que acolhe o portal de autosserviço, inscreva-se como administrador.

1. Inicie o Gestor de Serviços de Informação da **Internet (IIS)** (executar **inetmgr.exe**).

1. Expandir **sites,** expandir **o Web Site predefinido**e selecionar o nó **SelfService.** No painel de detalhes, **ASP.NET** grupo, abrir **as Definições de Aplicação.**

    [![Screenshot de exemplo das definições de aplicação selfService no IIS Manager](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Selecione o item que pretende alterar e no painel **Ações,** **selecione Editar**. Mude o **Valor** para o novo nome que pretende utilizar.

    > [!CAUTION]
    > Não mude os valores do **nome.** Por exemplo, não `CompanyName`mude, `Contoso IT`mude. Se alterar os valores do **Nome,** o portal de auto-atendimento deixará de funcionar.

As alterações entram em vigor imediatamente.

### <a name="supported-branding-values"></a>Valores de marca suportados

Para os valores que pode definir, consulte a tabela seguinte:

|Nome|Descrição|Valor&nbsp;por defeito|
|--- |--- |--- |
|CompanyName|O nome da organização que o portal de auto-atendimento exibe como um cabeçalho no topo de cada página.|`Contoso IT`|
|DisplayNotice|Apresentar um aviso inicial que o utilizador tem de reconhecer.|`true`|
|HelpdeskText|A corda no painel direito abaixo "Para todas as outras questões relacionadas"|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|O link para a cadeia HelpdeskText.|(vazio)|
|NoticeTextPath|O texto do aviso inicial que o utilizador tem de reconhecer. Por predefinição, o caminho completo `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`de ficheiros no servidor web é . Editar e guardar o ficheiro num simples editor de texto. Este valor de percurso é relativo à aplicação SelfService.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Para obter uma imagem do portal de autosserviço predefinido, consulte o [portal de autosserviço BitLocker](self-service-portal.md).

> [!TIP]
> Se necessário, pode localizar algumas destas cordas para exibir em diferentes línguas. Para mais informações, consulte [A Localização.](#bkmk_localize)

## <a name="session-time-out"></a>Hora da sessão

Para que a sessão do utilizador expire após um período de inatividade especificado, pode alterar a definição de tempo de saída da sessão para o portal de autosserviço.

1. No servidor web que acolhe o portal de autosserviço, inscreva-se como administrador.

1. Inicie o Gestor de Serviços de Informação da **Internet (IIS)** (executar **inetmgr.exe**).

1. Expandir **sites,** expandir **o Web Site predefinido**e selecionar o nó **SelfService.** Nos detalhes, **ASP.NET** grupo, open **Session State**.

1. No grupo **Definições** de Cookies, altere o valor do **Time-out (em minutos).** É o número de minutos após o qual a sessão do utilizador expira. O valor predefinido é `5`. Para desativar a definição, para que não haja `0`tempo para o intervalo, defina o valor para .

1. No painel **de ações,** selecione **Aplicar**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a>Texto de helpdesk localize e URL

Pode configurar versões localizadas da `HelpdeskText` declaração `HelpdeskUrl` e link do portal de auto-atendimento. Esta cadeia informa os utilizadores como obter ajuda adicional quando utilizam o portal. Se configurar texto localizado, o portal exibe a versão localizada para navegadores web nesse idioma. Se não encontrar uma versão localizada, exibe o valor `HelpdeskText` `HelpdeskUrl` predefinido nas definições e configurações.

1. No servidor web que acolhe o portal de autosserviço, inscreva-se como administrador.

1. Inicie o Gestor de Serviços de Informação da **Internet (IIS)** (executar **inetmgr.exe**).

1. Expandir **sites,** expandir **o Web Site predefinido**e selecionar o nó **SelfService.** No painel de detalhes, **ASP.NET** grupo, abrir **as Definições de Aplicação.**

1. No painel **Ações,** selecione **Adicionar**.

1. Na janela de definição de **aplicação adicionar,** configure os seguintes valores:

    - **Nome**: `HelpdeskText_<language>`insira, onde `<language>` está o código de línguas para o texto.

      Por exemplo, para criar `HelpdeskText` uma declaração localizada em `HelpdeskText_es-es`espanhol (Espanha), o nome é .

    - **Valor**: a corda localizada para exibir no painel direito do portal de autosserviço abaixo "Para todas as outras questões relacionadas"

1. Selecione **OK** para salvar a nova definição.

1. Repita este processo para adicionar `HelpdeskUrl_<language>` uma nova definição de aplicação para que corresponda à definição associada. `HelpdeskText_<language>`

Repita este processo para adicionar um par de configurações para todos os idiomas que apoia na sua organização.

## <a name="localize-the-notice-file"></a>Localize o ficheiro de aviso

Pode configurar versões localizadas do aviso inicial que o utilizador tem de reconhecer no portal de autosserviço. Por predefinição, o caminho completo `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`de ficheiros no servidor web é .

Para exibir texto de aviso localizado, crie um ficheiro notice.txt localizado. Em seguida, guarde-o sob uma pasta de idioma específica. Por exemplo: `Self Service Website\es-es\Notice.txt` para espanhol (Espanha).

O portal de autosserviço apresenta o texto de aviso com base nas seguintes regras:

- Se o ficheiro de aviso predefinido estiver em falta, o portal mostra uma mensagem de que o ficheiro predefinido está em falta.

- Se criar um ficheiro de aviso localizado na pasta de idioma apropriada, apresenta o texto de aviso localizado.

- Se o servidor web não encontrar uma versão localizada do ficheiro de aviso, apresenta o aviso predefinido.

- Se o utilizador definir o seu navegador para um idioma que não tenha um aviso localizado, o portal exibe o aviso predefinido.

### <a name="create-a-localized-notice-file"></a>Criar um ficheiro de aviso localizado

1. No servidor web que acolhe o portal de autosserviço, inscreva-se como administrador.

1. Crie `<language>` uma pasta para cada `Self Service Website` idioma suportado no caminho da aplicação. Por exemplo, `es-es` para o espanhol (Espanha). Por defeito, o `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`caminho completo é .

    Para obter uma lista dos códigos linguísticos válidos que pode utilizar, consulte referência aPi de [Suporte Linguístico Nacional (NLS).](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers)

    > [!TIP]
    > O nome da pasta linguística também pode ser o nome neutro da linguagem. Por exemplo, **es** para espanhol, em vez de **es-es** para espanhol (Espanha) e **es-ar** para espanhol (Argentina). Se o utilizador definir o seu navegador para **es-es**, e essa pasta de idioma não existir, o servidor web verifica recursivamente a pasta local **(es).** (Os locais-mãe são definidos em .NET.) Por exemplo,`Self Service Website\es\Notice.txt`. Este recuo recursivo imita as regras de carregamento de recursos .NET.

1. Crie uma cópia do seu ficheiro de pré-aviso com o texto localizado. Guarde-o na pasta para o código de idioma. Por exemplo, para o espanhol (Espanha), `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`por padrão, o caminho completo é .

Repita este processo para um ficheiro de aviso localizado para todas as línguas que apoia na sua organização.

## <a name="next-steps"></a>Passos seguintes

Agora que instalou e personalizou o portal de self-service, experimente! Para mais informações, consulte o [portal de self-service BitLocker](self-service-portal.md).
