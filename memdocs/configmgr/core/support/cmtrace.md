---
title: CMTrace
titleSuffix: Configuration Manager
description: Saiba como utilizar a ferramenta CMTrace para visualizar ficheiros de registo para O Gestor de Configuração.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723426"
---
# <a name="cmtrace"></a>CMTrace

*Aplica-se a: Gestor de Configuração (ramo atual)*

CmTrace é uma das ferramentas do Gestor de [Configuração.](tools.md) Permite-lhe visualizar e monitorizar ficheiros de registo, incluindo os seguintes tipos:  

- Ficheiros de registo no formato Gestor de Configuração ou Gestor de Componentes do Cliente (CCM)  

- Ficheiros de texto Simples ASCII ou Unicode, tais como registos do Instalador do Windows  

A ferramenta ajuda a analisar ficheiros de registo realçando, filtrando e procurando erros.

A partir da versão 1806, a ferramenta de visualização de log CMTrace é instalada automaticamente juntamente com o cliente do Gestor de Configuração. É adicionado ao diretório de instalação do `%WinDir%\CCM\CMTrace.exe`cliente, que por padrão é .<!--1357971-->

> [!Note]  
> O CMTrace não está registado automaticamente com o Windows para abrir a extensão do ficheiro .log. Para mais informações, consulte [as associações de ficheiros.](#file-associations)  

A partir da versão 1906, o **OneTrace** é um novo espectador de log com Support Center. Funciona da mesma forma com a CMTrace, com melhorias. Para mais informações, consulte [o Suporte Center OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Utilização

Executar **CMTrace.exe**. A primeira vez que executa a ferramenta, vê um pedido de associação de ficheiros. Para mais informações, consulte [as associações de ficheiros.](#file-associations)

Você toma a maioria das ações em CMTrace a partir dos seguintes menus:

- [Ficheiro](#file-menu)
- [Ferramentas](#tools-menu)

### <a name="file-menu"></a>Menu Ficheiro

As seguintes ações estão disponíveis no menu **Ficheiro:**  

- [Abrir](#open)
- [Abrir no Servidor](#open-on-server)
- [Imprimir](#print)
- [Preferências](#preferences)

O menu Ficheiro também lista os últimos oito ficheiros recentes. Reabra rapidamente um destes registos selecionando-os a partir do menu 'Ficheiro'.

#### <a name="open"></a>Abrir

Exibe a caixa de diálogo Open para procurar um ficheiro de registo.

Filtrar a vista para ficheiros dos seguintes tipos:

- Ficheiros\*de registo (.log)  
- Ficheiros de\*registo antigos (.lo_)
- Todos os\*\*ficheiros . .

As duas opções que se seguem não são selecionadas por defeito:  

- **Ignore as linhas existentes**: Quando selecionado, o CMTrace ignora o conteúdo existente do ficheiro de registo selecionado e apresenta novas linhas apenas à medida que são adicionadas. Utilize esta opção para monitorizar apenas novas ações quando não precisar de o histórico completo do ficheiro de registo.  

- **Fundir ficheiros selecionados**: Se ativar esta opção e selecionar mais de um ficheiro de registo, a CMTrace funde os registos selecionados na vista. Mostra-os como se fossem um único ficheiro de registo. O registo fundido atualiza o mesmo e suporta todas as outras funcionalidades CMTrace como se fosse um único ficheiro de registo.  

#### <a name="open-on-server"></a>Abrir no Servidor

Navegue na pasta de registos do Gestor de Configuração num computador do sistema de site com a caixa de diálogo padrão Browse. Também pode navegar na rede para obter um computador remoto.

Quando seleciona um computador remoto para navegar, a CMTrace verifica a parte do Gestor de Configuração. Se não encontrar uma parte com ficheiros de registo do Gestor de Configuração, apresenta uma mensagem de erro.  

Para ligar diretamente a um computador conhecido sem navegar, utilize a ação [Open.](#open) Em seguida, introduza um nome de servidor e partilhe usando o formato UNC.

#### <a name="print"></a>Imprimir

Exiba a caixa de diálogo padrão do Windows Print. Esta ação envia o ficheiro de registo atual para uma impressora. Forma a saída de acordo com as definições no separador de impressão de preferências CMTrace.

#### <a name="preferences"></a>Preferências

Configurar as definições para CMTrace. Estão disponíveis as seguintes opções:  

- **Separador geral**  

    - **Intervalo de atualização:** Controla a frequência com que o CMTrace verifica as alterações aos ficheiros de registo e carrega novas linhas. Por padrão, este valor é de 500 milissegundos.  

    - **Destaque**: Define a cor que o CMTrace utiliza ao destacar linhas de registo que escolhe. Por defeito, esta cor é amarela básica (Vermelho: 255, Verde: 255, Azul: 0).  

    - **Colunas**: Configura as colunas visíveis na vista de registo e a ordem em que aparecem. Por predefinição, apresenta texto de registo, componente, data/hora e fio.  

- **Separador de impressão**  

    - **Colunas**: Configure quais as colunas que utiliza ao imprimir ficheiros de registo e a ordem em que aparecem. Por padrão, imprime as mesmas colunas que exibe.  

    - **Orientação**: Define a orientação de impressão predefinida ao imprimir ficheiros de registo. Anular esta definição na caixa de diálogo Print. Por padrão, usa a orientação do Retrato.  

- **Separador avançado**  

    - **Intervalo de atualização**: Obriga a CMTrace a atualizar a vista de registo num intervalo determinado ao carregar um grande número de linhas. Por predefinição, esta opção é desativada com um valor de zero.  

        > [!Note]  
        > Em geral, não modifique o intervalo de **atualização**. Pode aumentar significativamente o tempo que leva para abrir ficheiros de registo grandes.

### <a name="tools-menu"></a>Menu de ferramentas

As seguintes ações estão disponíveis no menu **Ferramentas:**

- [Localizar](#find)
- [Encontrar A Seguir](#find-next)
- [Copiar para a área de transferência](#copy-to-clipboard)
- [Realce](#highlight)
- [Filtro](#filter)
- [Procuração de erros](#error-lookup)
- [Colocar em pausa](#pause)
- [Detalhes de mostrar/ocultar](#showhide-details)
- [Painel de informações de show/hide](#showhide-info-pane)

#### <a name="find"></a>Localizar

Procure no ficheiro de registo aberto por uma cadeia de texto especificada.  

#### <a name="find-next"></a>Encontrar A Seguir

Encontra a próxima corda correspondente, como especificado anteriormente na caixa de diálogo Find.  

#### <a name="copy-to-clipboard"></a>Copiar para a área de transferência

Copia as linhas selecionadas como texto simples para a área de sobre-saque do Windows. Se estiver a examinar ficheiros de registo do Gestor de Configuração e ccm, copia as colunas na mesma ordem que a vista. Separa cada coluna por um caracteres de separador. Utilize esta ação ao copiar registos em mensagens de correio eletrónico ou outros documentos.  

#### <a name="highlight"></a>Realce

Introduza uma cadeia que a CMTrace utiliza para pesquisar o texto de cada entrada de registo. Em seguida, realça qualquer texto de registo que corresponda à corda que introduz.  

- O destaque utiliza a cor especificada nas Preferências.  

- Para desligar o destaque, limpando a corda deste campo.  

- Se introduzir um número decimal ou hexadecimal, a CMTrace tenta corresponder ao valor da coluna Thread. Use este comportamento para destacar o processamento de um único fio, sem filtrar outros fios que possam interagir com ele.  

- Para comparar as cordas por caixa, ative a opção para **case sensitive**.  

#### <a name="filter"></a>Filtro

Mostrar ou ocultar linhas de registo com base nos critérios especificados. Aplique filtros em qualquer uma das quatro colunas, independentemente de serem visíveis. Estas definições aplicam-se a cada ficheiro de registo aberto.

Exemplos:
<!--SCCMDocs issue #603-->

- Filtrar **smsts.log** no texto de entrada contendo "a ação" ou "o grupo".
- Filter **InventoryAgent.log** onde o texto de entrada contém "destino".

#### <a name="error-lookup"></a>Procuração de erros

Digite ou colhe um código de erro em formato decimal ou hexadecimal para apresentar uma descrição. Possíveis fontes de erro incluem: Windows, WMI ou Winhttp.

#### <a name="pause"></a>Colocar em pausa

Suspender ou reiniciar a monitorização do registo. Os seguintes casos de utilização são algumas das razões possíveis para utilizar esta ação:  

- Quando o CMTrace está a apresentar informações de ficheiros de registo muito rapidamente  

- Quando pausa a monitorização do registo, a informação que o CMTrace exibe não se perde se o ficheiro atual passar para um novo registo  

- Quando pretende impedir o CMTrace de apresentar novos dados enquanto examina o ficheiro de registo  

#### <a name="showhide-details"></a>Detalhes de mostrar/ocultar

Mostre ou esconda todas as colunas que não o texto de registo. Também expande a coluna de texto de registo para a largura da janela. Utilize esta ação quando estiver a visualizar registos num computador com baixa resolução de ecrã. Exibe mais texto de registo.  

> [!Note]  
> Ao visualizar ficheiros de texto simples, o CMTrace esconde automaticamente os detalhes porque estão sempre vazios.  

#### <a name="showhide-info-pane"></a>Painel de informações de show/hide

Mostre ou esconda o painel de informação. Utilize esta ação quando estiver a visualizar registos num computador com baixa resolução de ecrã. Apresenta mais detalhes de registo.  


## <a name="log-pane"></a>Painel de log

O painel de madeira está na parte superior da janela CMTrace. Apresenta linhas a partir de ficheiros de registo.

Quando seleciona uma linha, é temporariamente realçada utilizando o esquema de cores de seleção do Windows.

As linhas destacadas correspondem aos critérios que define com a opção **Highlight** no menu **Ferramentas.** O destaque utiliza a cor que especifica nas **Preferências**.

CMTrace exibe linhas com erros utilizando um fundo vermelho e uma cor de texto amarela. Nos registos do formato CCM, as entradas de registo têm um valor de tipo explícito que indica a entrada como um erro. Para outros formatos de registo, o CMTrace faz uma pesquisa por caso insensível em cada entrada para qualquer sequência de linha de texto que corresponda a "erro".

Exibe linhas com avisos utilizando um fundo amarelo. Nos registos do formato CCM, as entradas de registo têm um valor de tipo explícito que indica a entrada como aviso. Para outros formatos de registo, a CMTrace faz uma pesquisa insensível em cada entrada para qualquer sequência de linha de texto "admissão".


## <a name="info-pane"></a>Painel de informações

O painel Info está na parte inferior da janela CMTrace. Inclui as seguintes características:

- Detalhes sobre a entrada de registo atualmente selecionada  

- Uma caixa de texto que exibe o texto de registo  

- Exibe devoluções de carruagem para que o texto formatado seja mais fácil de ler  

- Mais fácil de ler entradas longas que não são totalmente visíveis no painel de registo  

Mostre ou esconda o painel info com a opção **Show/Hide Info Pane** no menu **Ferramentas.** Se o painel info tomar mais de metade da janela de log, a CMTrace esconde-a automaticamente.

### <a name="progress-bar"></a>Barra de progresso

Quando abre pela primeira vez um ficheiro de registo, a CMTrace substitui o painel info por uma barra de progresso. Este progresso indica quanto do conteúdo do ficheiro existente está carregado. O progresso atinge 100%, a CMTrace remove a barra de progresso e substitui-a pelo painel Info. Ao carregar ficheiros grandes, este comportamento fornece-lhe uma indicação de quanto tempo a carga pode demorar.

### <a name="status-bar"></a>Barra de estado

Para os ficheiros de formato de formato de configuração e formato CCM, a barra de estado apresenta o tempo decorrido para as entradas de registo selecionadas. Se selecionar uma única entrada, a ferramenta apresenta o tempo desde a primeira entrada de registo até à entrada selecionada. Se selecionar várias entradas, calcula o tempo desde a entrada mais selecionada até à entrada mais abaixo selecionada. A CMTrace formata esta informação da seguinte forma:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Integração de conchas do Windows

A CMTrace suporta associações de [ficheiros](#file-associations) e [arrastar e largar](#drag-and-drop).

### <a name="file-associations"></a>Associações de ficheiros

A CMTrace pode associar-se a extensões de nome de ficheiro .log e .lo_. Quando o programa começa, verifica o registo para determinar se já está associado a estas extensões de nome de ficheiro. Se a CMTrace ainda não estiver associada a quaisquer extensões de nome de ficheiro, é solicitado que associe as extensões de nome do ficheiro com a CMTrace. Se selecionar **Não me pergunte isto novamente,** a CMTrace ignora esta verificação sempre que é executada neste computador.

### <a name="drag-and-drop"></a>Arrastar e largar

A CMTrace suporta a funcionalidade básica de arrastar e largar. Arraste um ficheiro de registo do Windows Explorer para cmTrace para abri-lo.


## <a name="other-tips"></a>Outras dicas

### <a name="last-directory-registry-key"></a>Última chave de registo de diretório

<!--511280-->
Por predefinição, a CMTrace guarda a última localização de registo que abriu. Este comportamento é útil no servidor do site, uma vez que se incorre sempre no caminho dos registos.

A primeira vez que o lança num cliente, falha no atual diretório de trabalho. Esta localização pode ser o caminho onde guardou `%userprofile%\Desktop`cmTrace, ou um caminho como .

O valor **do Último Diretório** na chave `HKEY_CURRENT_USER\Software\Microsoft\Trace32` do registo controla esta localização predefinida. Se definir este `%windir%\CCM\Logs` valor nos seus clientes, então a CMTrace abre ficheiros no local de registo do cliente na primeira vez que o executa.


## <a name="see-also"></a>Consulte também

- [Ficheiros de registo](../plan-design/hierarchy/log-files.md)

- [Espectador de ficheiro sonorde do Centro de Suporte](support-center.md#support-center-log-file-viewer)

- [Centro de Suporte OneTrace](support-center-onetrace.md)
