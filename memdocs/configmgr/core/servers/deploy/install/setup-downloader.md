---
title: Programa de Transferência da Configuração
titleSuffix: Configuration Manager
description: Leia sobre esta aplicação autónoma concebida para garantir que a instalação do seu site utiliza versões atuais de ficheiros de instalação chave.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718078"
---
# <a name="setup-downloader-for-configuration-manager"></a>Downloader de configuração para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de executar a Configuração para instalar ou atualizar um site do 'Gestor de Configuração', pode utilizar a aplicação autónoma do Downloader de Configuração a partir da versão do 'Gestor de Configuração' que pretende instalar para descarregar ficheiros de Configuração atualizados.  

A utilização de ficheiros de configuração atualizados garante que a instalação do seu site utiliza as versões atuais dos ficheiros de instalação de chaves. Em oveview:   
-   Quando utilizar o Downloader de Configuração para descarregar ficheiros antes de iniciar a configuração, especifice uma pasta para conter os ficheiros.  
-   A conta que utiliza para executar o Downloader de Configuração deve ter permissões **de Controlo Completo** para a pasta de descarregamento.  
-   Quando executa a Configuração para instalar ou atualizar um site, pode direcioná-lo para utilizar esta cópia local dos ficheiros que já descarregou anteriormente. Isto impede que o formulário de configuração tenha de se ligar à Microsoft quando iniciar a instalação ou atualização do site.  
-   Pode utilizar a mesma cópia local dos ficheiros de configuração para instalações ou atualizações posteriores do site.  

Os seguintes tipos de ficheiros são descarregados pelo Downloader de Configuração:  
-   Ficheiros redistribuíveis pré-requisitos necessários  
-   Pacotes de idiomas  
-   As últimas atualizações do produto para Configuração  

Tem duas opções para executar o Downloader de Configuração:
- Executar a aplicação com a interface do utilizador
- Para opções de linha de comando, executar a aplicação em um pedido de comando


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Executar Downloader de Configuração com a interface do utilizador  

1.  Num computador que tenha acesso à Internet, abra o Windows Explorer e vá ao ** &lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Para abrir o Downloader de Configuração, clique duas vezes **em Setupdl.exe**.   

3. Especifique o caminho para a pasta que irá alojar os ficheiros de instalação atualizados e, em seguida, clique em **Descarregar**. Configurar O Downloader verifica os ficheiros que estão atualmente na pasta de descarregamento. Descarrega apenas ficheiros que faltam ou que são mais recentes do que os ficheiros existentes. Configuração Downloader cria subpastas para idiomas descarregados, e outras subpastas necessárias.  

4.  Para rever os resultados do download, abra o ficheiro **ConfigMgrSetup.log** no diretório raiz da unidade C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Executar Downloader de Configuração a partir de um pedido de comando  

1.  Numa janela De Comando, vá ao ** &lt;meio\>de *instalação do Gestor*de Configuração \SMSSETUP\BIN\X64**.   

2.  Para abrir o Downloader de Configuração, executar **Setupdl.exe**.

    Pode utilizar as seguintes opções de linha de comando com **Setupdl.exe:**   

    -   **/CHECK**: Utilize esta opção para verificar os ficheiros na pasta de descarregamento, que incluem ficheiros de idiomas. Reveja o ficheiro ConfigMgrSetup.log no diretório raiz da unidade C para obter uma lista de ficheiros que estão desatualizados. Não são descarregados ficheiros quando utiliza esta opção.  

    -   **/CHECKLANG**: Utilize esta opção para verificar os ficheiros de idiomas na pasta de descarregamento. Reveja o ficheiro ConfigMgrSetup.log no diretório raiz da unidade C para obter uma lista de ficheiros linguísticos que estão desatualizados.

    -   **/LANG**: Utilize esta opção para descarregar apenas os ficheiros de idiomas para a pasta de descarregamento.  

    -   **/NOUI:** Utilize esta opção para iniciar o Downloader de Configuração sem visualizar a interface do utilizador. Quando utilizar esta opção, deve especificar o caminho de **descarregamento** como parte do comando no pedido de comando.  

    -   **DownloadPath\>: Pode especificar o caminho para a pasta de descarregamento para iniciar automaticamente o processo de verificação ou descarregamento. &lt;** Deve especificar o caminho de descarregamento quando utilizar a opção **/NOUI.** Se não especificar um caminho de descarregamento, deve especificar o caminho quando o Downloader de Configuração abrir. Configurar o Downloader cria a pasta se não existir.  

    Comandos de exemplo:

    -   **configuração &lt;DownloadPath\>**  

        -   O Downloader de Configuração inicia, verifica os ficheiros na pasta de descarregamento especificada e, em seguida, descarrega apenas os ficheiros que faltam ou que têm versões mais recentes do que os ficheiros existentes.     

    -   **configuração /CHECK &lt;DownloadPath\>**  

        -   Configurar o Downloader inicia e verifica os ficheiros na pasta de descarregamento especificada.  

    -   **configuração /NOUI &lt;DownloadPath\>**  

        -   O Downloader de Configuração inicia, verifica os ficheiros na pasta de descarregamento especificada e, em seguida, descarrega apenas os ficheiros que faltam ou que são mais recentes do que os ficheiros existentes.  

    -   **configuração /LANG &lt;DownloadPath\>**  

        -   O Downloader de Configuração inicia, verifica os ficheiros de idiomas na pasta de descarregamento especificada e, em seguida, descarrega apenas os ficheiros de idiomas que faltam ou que são mais recentes do que os ficheiros existentes.  

    -   **configuração /CHECK**  

        -   O Downloader de configuração começa e, em seguida, deve especificar o caminho para a pasta de descarregamento. Em seguida, depois de clicar em **Verificar,** o Downloader de Configuração verifica os ficheiros na pasta de descarregamento.  

3.  Para rever os resultados do download, abra o ficheiro **ConfigMgrSetup.log** no diretório raiz da unidade C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Copiar Ficheiros de descarregador de configuração para outro computador

1. No Windows Explorer, vá a qualquer um dos seguintes locais:

    - **&lt;Configuração Manager de instalação>\SMSSETUP\BIN\X64**
    - **&lt;Caminho de instalação do Gestor de Configuração>\BIN\X64**
    
1. Copie os seguintes ficheiros para a mesma pasta de destino no outro computador:
    
    - **setupdl.exe**
    - **. \\>\\configurações.dll &lt;**
      - Este ficheiro encontra-se na subpasta para o idioma de instalação. Por exemplo, o `00000409` inglês está na subpasta.

    Como exemplo, as pastas de destino no seu dispositivo devem ser assim:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Lance o Downloader de Configuração a partir do computador utilizando a interface do [utilizador](#bkmk_ui) ou o pedido de [comando](#bkmk_cmd), descrito nas secções acima.
