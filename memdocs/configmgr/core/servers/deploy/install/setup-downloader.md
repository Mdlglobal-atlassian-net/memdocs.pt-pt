---
title: Ferramenta de descarregamento de configuração
titleSuffix: Configuration Manager
description: Utilize a ferramenta autónoma para descarregar as versões atuais dos ficheiros de instalação de chaves para configuração.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428837"
---
# <a name="setup-downloader-for-configuration-manager"></a>Downloader de configuração para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de executar a configuração do 'Gestor de Configuração' para instalar ou atualizar um site, pode utilizar a ferramenta autónoma do download de configuração para descarregar ficheiros de configuração atualizados. Execute a ferramenta a partir da versão do Gestor de Configuração que pretende instalar. Utilize ficheiros de configuração atualizados para se certificar de que a instalação do seu site utiliza versões atuais dos ficheiros de instalação de chaves.

Quando utilizar o descarregador de configuração, especifice uma pasta para conter os ficheiros. A conta que utiliza para executar a ferramenta deve ter permissões **de Controlo Total** para a pasta de descarregamento. Quando executar a configuração para instalar ou atualizar um site, pode especificar esta cópia local dos ficheiros que já descarregou anteriormente. Este comportamento impede que a configuração se ligue à Microsoft quando iniciar a instalação ou atualização do site. Pode utilizar a mesma cópia local dos ficheiros de configuração para outras instalações do site ou atualizações da mesma versão.

A ferramenta de descarregamento de configuração descarrega os seguintes tipos de ficheiros:

- Ficheiros redistribuíveis pré-requisitos necessários
- Pacotes de idiomas
- As últimas atualizações do produto para configuração

Tem duas opções para executar o downloader de configuração:

- Executar a aplicação com a interface do utilizador
- Executar a aplicação num pedido de comando para opções adicionais da linha de comando

Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, tem de permitir que a ferramenta aceda a pontos finais da Internet. O dispositivo onde irá executar a ferramenta requer acesso à Internet da mesma forma que o ponto de ligação de serviço. Para mais informações, consulte os requisitos de [acesso à Internet.](../../../plan-design/network/internet-endpoints.md#bkmk_scp)<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Executar downloader de configuração com a interface do utilizador

1. Num computador que tenha acesso à Internet, navegue para os meios de instalação para a versão do Gestor de Configuração que pretende instalar.

1. Na subpasta **SMSSETUP\BIN\X64,** executar **Setupdl.exe**.

1. Especifique o caminho para a pasta armazenar os ficheiros de instalação atualizados e, em seguida, selecione **Download**. O descarregador de configuração verifica os ficheiros que estão atualmente na pasta de descarregamento. Descarrega apenas ficheiros que faltam ou que são mais recentes do que os ficheiros existentes. Cria subpastas para idiomas descarregados e outros componentes necessários.

1. Para rever os resultados do download, consulte **C:\ConfigMgrSetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Executar descarregador de configuração a partir de um pedido de comando

1. Abra um pedido de comando e mude o diretório para os meios de instalação para a versão do Gestor de Configuração que pretende instalar.

1. Mude o diretório para a subpasta **SMSSETUP\BIN\X64** e execute **Setupdl.exe** com as opções necessárias.

1. Para rever os resultados do download, consulte **C:\ConfigMgrSetup.log**.

### <a name="command-line-options"></a>Opções da linha de comandos

Pode utilizar as seguintes opções de linha de comando com **Setupdl.exe:**

- **/CHECK**: Verifique os ficheiros na pasta de descarregamento, que incluem ficheiros de idiomas. Para a lista de ficheiros desatualizados, reveja **C:\ConfigMgrSetup.log**. Quando utiliza esta opção, não descarrega ficheiros.

- **/CHECKLANG**: Verifique apenas os ficheiros de idiomas na pasta de descarregamento. Para a lista de ficheiros de idiomas desatualizados, reveja **C:\ConfigMgrSetup.log**.

- **/LANG**: Descarregue apenas os ficheiros de idiomas para a pasta de descarregamento.

- **/NOUI:** Inicie o descarregador de configuração sem a interface do utilizador. Quando utiliza esta opção, é necessário o caminho de **descarregamento.**

- **Descarregue**o caminho : Para iniciar automaticamente o processo de verificação ou descarregamento, especifique o caminho para a pasta de descarregamento. Quando utilizar a opção **/NOUI,** é necessário o caminho de descarregamento. Se não especificar um caminho de descarregamento, o descarregador de configuração pede-lhe para especificar o caminho. Se a pasta não existir, o descarregador de configuração cria-a.

### <a name="example-commands"></a>Comandos de exemplo

#### <a name="example-1"></a>Exemplo 1

O descarregador de configuração verifica os ficheiros na pasta de descarregamento especificada e, em seguida, descarrega ficheiros.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Exemplo 2

O descarregador de configuração apenas verifica os ficheiros na pasta de descarregamento especificada.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Exemplo 3

O descarregador de configuração verifica os ficheiros na pasta de descarregamento especificada e, em seguida, descarrega ficheiros. A ferramenta não mostra nenhuma interface de utilizador.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Exemplo 4

O descarregador de configuração verifica os ficheiros de idiomas na pasta de descarregamento especificada e, em seguida, descarrega apenas os ficheiros de idiomas.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Copiar ficheiros de descarregamento de configuração para outro computador

1. No Windows Explorer, vá a qualquer um dos seguintes locais:

    - **&lt;Configuração Manager de instalação>\SMSSETUP\BIN\X64**

    - **&lt;Caminho de instalação do Gestor de Configuração>\BIN\X64**

1. Copie os seguintes ficheiros para a mesma pasta de destino no outro computador:

    - **setupdl.exe**

    - **.\\&lt; language> \\ setupdlres.dll**

        > [!NOTE]
        > Este ficheiro encontra-se na subpasta para o idioma de instalação. Por exemplo, o inglês está na `00000409` subpasta.

    As pastas de destino do seu dispositivo devem parecer o seguinte exemplo:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Executar o descarregador de configuração a partir do computador de destino. Utilize a interface do [utilizador](#bkmk_ui) ou o pedido de [comando](#bkmk_cmd).
