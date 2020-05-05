---
title: CMPivot para dados em tempo real
titleSuffix: Configuration Manager
description: Aprenda a usar a CMPivot no Gestor de Configuração para consultar os clientes em tempo real.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719142"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot para dados em tempo real no Gestor de Configuração

<!--1358456-->

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração sempre forneceu uma grande loja centralizada de dados do dispositivo, que os clientes usam para fins de reporte. O site normalmente recolhe estes dados semanalmente. A partir da versão 1806, a CMPivot é um novo utilitário na consola que agora fornece acesso ao estado real dos dispositivos no seu ambiente. Executa imediatamente uma consulta em todos os dispositivos atualmente conectados na recolha do alvo e devolve os resultados. Em seguida, filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode responder mais rapidamente a questões de negócios, resolver problemas e responder a incidentes de segurança.

Por exemplo, na mitigação das [vulnerabilidades dos canais laterais de execução especulativa,](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)um dos requisitos é atualizar o sistema BIOS. Pode usar a CMPivot para consultar rapidamente informações bios do sistema e encontrar clientes que não estejam em conformidade.

 > [!IMPORTANT]  
 > - Alguns softwares de segurança podem bloquear scripts que saem da loja de scripts c:\windows\ccm\. Isto pode impedir a execução bem sucedida de consultas CMPivot. Alguns softwares de segurança também podem gerar eventos de auditoria ou alertas ao executar a CMPivot PowerShell.
 > - Certos softwares anti-malware podem inadvertidamente desencadear eventos contra as funcionalidades de execução do Gestor de Configuração ou CMPivot. Recomenda-se excluir %windir%\CCM\ScriptStore para que o software anti-malware permita que essas funcionalidades executem sem interferências.


## <a name="prerequisites"></a>Pré-requisitos

Os seguintes componentes são obrigados a utilizar a CMPivot:

- Atualize os dispositivos-alvo para a versão mais recente do cliente do Gestor de Configuração.  

- Os clientes-alvo requerem um mínimo da versão 4 da PowerShell.

- Para recolher dados para as seguintes entidades, os clientes-alvo requerem a versão PowerShell 5.0:  
  - Administradores
  - Ligação
  - IPConfig
  - SMBConfig


- Permissões para cmpivot:
  - **Leia** a permissão no objeto **de Scripts SMS**
  - Executar permissão **de Scripts** na **Coleção**
    - Em alternativa, a partir da versão 1906, pode utilizar **o Run CMPivot** na **Collection**.
  - **Ler** permissão em **Relatórios** de Inventário
  - O âmbito padrão.

>[!NOTE]
> **Executar Scripts** é um super conjunto da permissão **Run CMPivot.**
 
## <a name="limitations"></a>Limitações

- Numa hierarquia, ligue a consola do Gestor de Configuração a um *local primário* para executar a CMPivot. A ação **START CMPivot** não aparece na consola quando está ligada a um site de administração central (CAS).
  - A partir da versão 1902 do Gestor de Configuração, pode executar cmPivot a partir de um CAS. Em alguns ambientes, são necessárias permissões adicionais. Para mais informações, consulte a [CMPivot a partir da versão 1902](#bkmk_cmpivot1902).

- A CMPivot apenas devolve dados para clientes ligados ao site atual.  

- Se uma recolha contiver dispositivos de outro site, os resultados da CMPivot são apenas de dispositivos no local atual.  

- Não é possível personalizar propriedades da entidade, colunas para resultados ou ações em dispositivos.  

- Apenas uma instância de CMPivot pode ser executada ao mesmo tempo num computador que está a executar a consola do Gestor de Configuração.  

- Na versão 1806, a consulta para a entidade **administradores** só funciona se o grupo for nomeado "Administradores". Não funciona se o nome de grupo estiver localizado. Por exemplo, "Administradores" em francês.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Iniciar cmpivot

1. Na consola 'Gestor de Configuração', ligue-se ao local principal. Vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de Recolhas de **Dispositivos.** Selecione uma coleção de alvos e clique em **Iniciar CMPivot** na fita para lançar a ferramenta.  

    > [!Tip]  
    > Se não vir esta opção, verifique as seguintes configurações:  
    > 
    > - Confirme com um administrador do site que a sua conta tem as permissões necessárias. Para mais informações, consulte [os pré-requisitos.](#prerequisites)  
    > 
    > - Ligue a consola a um *local primário*.  

2. A interface fornece mais informações sobre a utilização da ferramenta.  

     - Introduza manualmente as cordas de consulta na parte superior ou clique nos links na documentação em linha.  

     - Clique numa das **Entidades** para adicioná-la à corda de consulta.  

     - Os links para **Operadores de Mesa,** Funções de **Agregação**e **Funções Escalar** abrem documentação de referência linguística no navegador web. CmPivot usa a [linguagem de consulta kusto (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Mantenha a janela CMPivot aberta para visualizar os resultados dos clientes. Quando fechar a janela CMPivot, a sessão está completa.  

    > [!Note]  
    > Se a consulta tiver sido enviada, os clientes ainda enviam uma resposta de mensagem de estado ao servidor.  



## <a name="how-to-use-cmpivot"></a>Como utilizar o CMPivot

![Amostra da janela CMPivot](media/1358456-cmpivot-sample.png)

A janela CMPivot contém os seguintes elementos:  

1. A coleção que a CMPivot tem atualmente como alvo está na barra de títulos na parte superior, e na barra de estado na parte inferior da janela. Por exemplo, "PM_Team_Machines" na imagem acima.  

2. O painel à esquerda lista as **Entidades** que estão disponíveis nos clientes. Algumas entidades confiam no WMI enquanto outras usam a PowerShell para obter dados dos clientes.   

    - Clique na direita numa entidade para as seguintes ações:  

       - **Inserção**: Adicione a entidade à consulta na posição de cursor atual. A consulta não corre automaticamente. Esta ação é o padrão quando clica duas vezes numa entidade. Use esta ação ao construir uma consulta.  

       - **Consulta a todos**: Fazer uma consulta para esta entidade, incluindo todas as propriedades. Use esta ação para consultar rapidamente uma única entidade.  

       - **Consulta por dispositivo**: Execute uma consulta para esta entidade e agrupe os resultados. Por exemplo, `Disk | summarize dcount( Device ) by Name`  

    - Expandir uma entidade para ver imóveis específicos disponíveis para cada entidade. Clique duas vezes numa propriedade para adicioná-la à consulta na posição de cursor atual.  

3. O separador **Home** mostra informações gerais sobre a CMPivot, incluindo links para consultas de amostra e documentação de apoio.  

4. O **separador Consulta** apresenta o painel de consulta, o painel de resultados e a barra de estado. O separador de consulta é selecionado no exemplo de imagem acima.  

5. O painel de consulta é onde você constrói ou escreve uma consulta para executar sobre clientes na coleção.  

    - CmPivot utiliza um subconjunto da [Linguagem de Consulta Kusto (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

    - Corte, cópia ou colar conteúdo no painel de consulta.  
    <!-- markdownlint-disable MD038 -->
    - Por padrão, este painel utiliza o IntelliSense. Por exemplo, se `D`começar a escrever, o IntelliSense sugere todas as entidades que começam com essa letra. Selecione uma opção e prima O separador para inseri-lo. Digite um personagem `| `de tubo e um espaço , e depois o IntelliSense sugere todos os operadores de mesa. Insira `summarize` e escreva um espaço, e intelliSense sugere todas as funções de agregação. Para obter mais informações sobre estes operadores e funções, clique no separador **Home** em CMPivot.  

    - O painel de consulta também fornece as seguintes opções:  

        - Execute a consulta.  

        - Ande para trás e para a frente na lista de consultas.  

        - Crie uma coleção direta de membros.  

        - Exportar os resultados da consulta para CSV ou para a pasta.  

6. O painel de resultados mostra os dados devolvidos por clientes ativos para a consulta.  

   - As colunas disponíveis variam com base na entidade e na consulta.  

   - Clique num nome de coluna para classificar os resultados por essa propriedade.  

   - Clique no direito em qualquer nome de coluna para agrupar os resultados pela mesma informação nessa coluna ou classificar os resultados.  

   - Clique no clique direito num nome do dispositivo para tomar as seguintes ações adicionais no dispositivo:  

      - **Pivô para**: Consulta para outra entidade neste dispositivo.  

      - **Executar script**: Lance o assistente do Script executar para executar um script PowerShell existente neste dispositivo. Para mais informações, consulte [Executar um guião](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Controlo remoto**: Lance uma sessão de controlo remoto do Gestor de Configuração neste dispositivo. Para mais informações, consulte [Como administrar remotamente um computador cliente do Windows](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Explorador de recursos**: Explorador de recursos do Gestor de Configuração de Lançamento para este dispositivo. Para mais informações, consulte [o inventário de hardware ou](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) ver o inventário de [software](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Clique à direita em qualquer célula não-dispositivo para tomar as seguintes ações adicionais:  

     - **Cópia**: Copiar o texto da célula para a pasta.  

     - **Mostrar dispositivos com**: Consulta para dispositivos com este valor para esta propriedade. Por exemplo, a partir `OS` dos resultados da consulta, selecione esta opção numa célula na linha Versão:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Mostrar dispositivos sem**: Consulta para dispositivos sem este valor para esta propriedade. Por exemplo, a partir `OS` dos resultados da consulta, selecione esta opção numa célula na linha Versão:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing it**: Launch the https://www.bing.com default web browser to with this value as the consulta string.  

   - Clique em qualquer texto hiperligado para girar a vista nessa informação específica.  

   - O painel de resultados não mostra mais de 20.000 filas. Ou ajuste a consulta para filtrar ainda mais os dados, ou reinicie a CMPivot numa recolha menor.  

7. A barra de estado mostra as seguintes informações (da esquerda para a direita):  

   - O estado da consulta atual à recolha do alvo. Este estado inclui:  
     - O número de clientes ativos que completaram a consulta (3)  
     - O número de clientes totais (5)  
     - O número de clientes offline (2)  
     - Quaisquer clientes que devolvessem o insucesso (0)  

       Por exemplo: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - A identificação da operação do cliente. Por exemplo: `id(16780221)`  

   - A coleção atual. Por exemplo: `PM_Team_Machines`  

   - O número total de linhas no painel de resultados. Por exemplo, `1 objects`  



## <a name="example-scenarios"></a>Cenários de exemplo

As seguintes secções fornecem exemplos de como pode utilizar a CMPivot no seu ambiente:


### <a name="example-1-stop-a-running-service"></a>Exemplo 1: Parar um serviço de funcionamento

O seu administrador de segurança pede-lhe para parar e desativar o serviço de navegador de computador o mais rapidamente possível em todos os dispositivos do departamento de contabilidade. Inicie a CMPivot numa coleção para todos os dispositivos em contabilidade e selecione **A Query na** entidade **de Serviço.** 

`Service`

À medida que os resultados aparecem, clique na coluna **Nome** e selecione **Grupo por**. 

`Service | summarize dcount( Device ) by Name`

Na linha para o serviço **Browser,** clique no número hiperligado na coluna **dcount_.** 

`Service | where (Name == 'Browser') | summarize count() by Device`

Selecione vários dispositivos, clique na seleção e escolha **Executar Script**. Esta ação lança o assistente do Run Script, a partir do qual executa um script existente que tem para parar e desativar um serviço. Com a CMPivot, responde rapidamente ao incidente de segurança de todos os computadores ativos, visualizando os resultados do assistente do Script executar. Em seguida, você segue para criar uma linha de base de configuração para remediar outros computadores na coleção à medida que eles se tornam ativos no futuro. 

![Exemplo CMPivot para serviço de navegador e ação de script executar](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemplo 2: Resolver proativamente falhas na aplicação  

Para ser proativo com a manutenção operacional, uma vez por semana executa a CMPivot contra uma coleção de servidores que gere e **selecione Query tudo** na entidade **AppCrash.** Clique na coluna **FileName** e selecione **Ordenar Ascendente**. Um dispositivo devolve sete resultados para sqlsqm.exe com um carimbo de tempo cerca das 03:00 todos os dias. Selecione o nome do ficheiro numa das linhas, clique à direita e selecione **Bing It**. Ao navegar nos resultados da pesquisa no navegador web, encontra um artigo de suporte da Microsoft para este problema com mais informações e resolução. 


### <a name="example-3-bios-version"></a>Exemplo 3: Versão BIOS

Para [mitigar as vulnerabilidades especulativas](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)do canal lateral da execução, um dos requisitos é atualizar o sistema BIOS. Começa-se com uma consulta para a entidade **BIOS.** Em seguida, **group by** the **Version** property. Em seguida, clique à direita num valor específico, como "LENOVO - 1140", e selecione **dispositivos Show com**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemplo 4: Espaço de disco gratuito

Precisa de armazenar temporariamente um ficheiro grande num servidor de ficheiros de rede, mas não tem a certeza de qual tem capacidade suficiente. Inicie a CMPivot contra uma coleção de servidores de ficheiros e consultar a entidade **disk.** Modifique a consulta para a CMPivot devolver rapidamente uma lista de servidores ativos com dados de armazenamento em tempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot a partir da versão 1810
<!--1359068, 3607759-->

A CMPivot inclui as seguintes melhorias a partir da versão 1810 do Gestor de Configuração:

- [Utilitário e desempenho cmpivot](#bkmk_cmpivot-perf)
- [Funções escalares](#bkmk_cmpivot-functions)  
- [Visualizações de renderização](#bkmk_cmpivot-charts)  
- [Inventário de Hardware](#bkmk_cmpivot-hinv)  
- [Operadores escalares](#bkmk_cmpivot-operators)  
- [Resumo da consulta](#bkmk_cmpivot-summary)  
- [Mensagens de estado de auditoria](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a>Utilitário e desempenho cmpivot

- A CMPivot vai devolver até 100.000 células em vez de 20.000 linhas.
  - Se a entidade tiver 5 propriedades, ou seja, 5 colunas, serão mostradas até 20.000 linhas.
  - Para uma entidade com 10 propriedades, serão mostradas até 10.000 filas.
  - Os dados totais mostrados serão inferiores ou iguais a 100.000 células.
- No separador Resumo de Consulta, selecione a contagem de dispositivos Failed ou Offline e, em seguida, selecione a opção de **Criar Recolha**. Esta opção facilita o alvo desses dispositivos com uma implementação de reparação.
- Guarde as consultas **favoritas** clicando no ícone da pasta.
   ![Exemplo de salvar uma consulta favorita na CMPivot](media/cmpivot-favorite.png)

- Os clientes atualizados para a versão 1810 devolvem a saída inferior a 80 KB para o site num canal de comunicação rápida.
  - Esta alteração aumenta o desempenho da visualização do script ou da saída de consulta.
  - Se o script ou a saída de consulta for superior a 80 KB, o cliente envia os dados através de uma mensagem de estado.
  - Se o cliente não for atualizado para a versão de cliente de 1810, continua a usar mensagens de Estado.

- Pode ver o seguinte erro quando iniciar o CMPivot: Não pode utilizar a **CMPivot neste momento devido a uma versão de script incompatível. Esta questão pode ser porque a hierarquia está em processo de modernização de um site. Aguarde até que a atualização esteja completa e tente novamente.**

  - Se vir esta mensagem, pode significar:
    - O âmbito de segurança não está bem montado.
    - Há problemas com a Atualização no processo.
    - O roteiro subjacente à CMPivot é incompatível.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a>Funções escalar
A CMPivot suporta as seguintes funções escalar:
- **atrás()**: Subtrai a hora do tempo do relógio atual UTC  
- **datetime_diff()**: Calcula a diferença de calendário entre dois valores de data-data  
- **agora()**: Devolve o atual tempo do relógio UTC  
- **bin()**: Valores de rodada até um múltiplo inteiro de um dado tamanho do caixote do lixo  

> [!Note]  
> O tipo de dados da data representa um instante no tempo, tipicamente expresso como uma data e hora do dia. Os valores do tempo são medidos em unidades de 1 segundo. O valor da data está sempre no fuso horário UTC. Sempre expresse os literais da data no formato ISO 8601, por exemplo,`yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Exemplos
- `datetime(2015-12-31 23:59:59.9)`: Uma data específica literal   
- `now()`: O tempo atual  
- `ago(1d)`: O tempo atual menos um dia  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a>Visualizações de renderização

A CMPivot inclui agora suporte básico para o operador de [renderização](https://docs.microsoft.com/azure/kusto/query/renderoperator)KQL . Este suporte inclui os seguintes tipos:  
- **barchart**: A primeira coluna é do eixo X, e pode ser texto, data ou numérico. As segundas colunas devem ser numéricas e ser apresentadas como uma tira horizontal.  
- **columnchart**: Tal como o barchart, com tiras verticais em vez de tiras horizontais.  
- **piechart**: Primeira coluna é eixo de cor, segunda coluna é numérica.  
- **tabela de tempo:** Gráfico de linha. A primeira coluna é o eixo X, e deve ser a hora do encontro. A segunda coluna é o eixo y.  

#### <a name="example-bar-chart"></a>Exemplo: gráfico de barras
A seguinte consulta torna as aplicações mais recentemente utilizadas como um gráfico de barras:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Exemplo de visualização do gráfico de barras CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Exemplo: gráfico de tempo
Para tornar os gráficos de tempo, utilize o novo operador de **caixotes** para agrupar eventos a tempo. A seguinte consulta mostra quando os dispositivos começaram nos últimos sete dias:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Exemplo de visualização do gráfico de tempo CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Exemplo: gráfico de tartes
A seguinte consulta exibe todas as versões de S num gráfico de tartes:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Exemplo de visualização do gráfico de tarte cmpivot](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a>Inventário de hardware
Use cmPivot para consultar qualquer classe de inventário de hardware. Estas aulas incluem quaisquer extensões personalizadas que faça para o inventário de hardware. A CMPivot devolve imediatamente os resultados em cache da última varredura de inventário de hardware armazenada na base de dados do site. Ao mesmo tempo, atualiza os resultados se necessário com dados ao vivo de qualquer cliente online.

A saturação de cores dos dados na tabela ou gráfico de resultados indica se os dados estão vivos ou em cache. Por exemplo, o azul escuro é dados em tempo real de um cliente online. Azul claro é dados em cache.

#### <a name="example"></a>Exemplo

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Exemplo de consulta de inventário CMPivot com visualização de gráfico de coluna](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitações
- As seguintes entidades de inventário de hardware não são suportadas:  
    - Propriedades de matriz, por exemplo endereço IP  
    - Real32/Real64 <!--example?-->  
    - Propriedades de objetos embutidos <!--example?-->  
- Nomes de entidades de inventário devem começar com um personagem
- Não se pode substituir as entidades incorporadas criando uma entidade de inventário com o mesmo nome  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a>Operadores escalar
A CMPivot inclui os seguintes operadores escalar:  

> [!Note]  
> - LHS: corda à esquerda do operador  
> - RHS: corda à direita do operador  


|Operador|Descrição|Exemplo (rendimentos verdadeiros)|
|--------|-----------|---------------------|
|==|É igual a|`"aBc" == "aBc"`|
|!=|Não é igual|`"abc" != "ABC"`|
|como|LHS contém uma correspondência para RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS não contém uma correspondência para RHS|`"Fabrikam" !like "%xyz%"`|
|contém|RhS ocorre como uma subsequência de LHS|`"FabriKam" contains "BRik"`|
|!contém|RhS não ocorre em LHS|`"Fabrikam" !contains "xyz"`|
|começa com|RHS é uma subsequência inicial de LHS|`"Fabrikam" startswith "fab"`|
|!começa com|RHS não é uma subsequência inicial de LHS|`"Fabrikam" !startswith "kam"`|
|termina com|RHS é uma subsequência de fecho de LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS não é uma subsequência de fecho de LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>Resumo da consulta

Selecione o separador Resumo de **Consulta** na parte inferior da janela CMPivot. Este estado ajuda-o a identificar clientes que estão offline, ou erros de resolução de problemas que possam ocorrer. Selecione um valor na coluna Count para abrir uma lista de dispositivos específicos com esse estatuto. 

Por exemplo, selecione a contagem de dispositivos com um estado de Falha. Consulte a mensagem de erro específica e exporte uma lista destes dispositivos. Se o erro for que um cmdlet específico não é reconhecido, crie uma recolha da lista de dispositivos exportados para implementar uma atualização do Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Mensagens de estado de auditoria da CMPivot

A partir da versão 1810, quando executa a CMPivot, é criada uma mensagem de estado de auditoria com **o MessageID 40805**. Pode visualizar as mensagens de estado indo para **monitorizar** > **as consultas**de mensagem de**estado** > do sistema . Pode executar todas as mensagens de estado de **auditoria para um utilizador específico,** todas as mensagens de estado de auditoria para um Site **Específico,** ou criar a sua própria consulta de mensagem de estado.

O seguinte formato é utilizado para a mensagem:

MessageId 40805: &lt;User UserName &lt;> executou script-Guid> com &lt; &lt;hash Script-Hash> na recolha de> de recolha de id.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 é o Script-Guid para cmpivot.
- O Script-Hash pode ser visto no ficheiro scripts.log do cliente.
- Também pode ver o hash armazenado na loja de scripts do cliente. O nome de ficheiro &lt;no cliente&lt;é Script-Guid>_ Script-Hash>.
    - Nome do ficheiro: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Amostra de mensagem de estado de auditoria cmpivot](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot a partir da versão 1902
<!--3610960-->
A partir da versão 1902 do Gestor de Configuração, pode executar a CMPivot a partir do site da administração central (CAS) numa hierarquia. O site principal ainda trata da comunicação ao cliente. Ao executar a CMPivot a partir do site da administração central, comunica com o site principal através do canal de subscrição de mensagens de alta velocidade. Esta comunicação não depende da replicação padrão da SQL entre os sites.

A execução da CMPivot no CAS exigirá permissões adicionais quando a SQL ou o fornecedor não estiverem na mesma máquina ou no caso da configuração SQL Always On. Com estas configurações remotas, você tem um "cenário de duplo salto" para CMPivot.

Para que a CMPivot trabalhe no CAS num "cenário de duplo salto", pode definir uma delegação restrita. Para compreender as implicações de segurança desta configuração, leia o artigo da [delegação limitada kerberos.](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) Kerberos precisa de trabalhar em todos os lúpulos entre as máquinas.<!--5746133--> Se tiver mais de uma configuração remota, como o SQL ou o SMS Provider, sendo ou não colocalizado com o CAS, ou com múltiplas florestas fidedignas, poderá necessitar de uma combinação de definições de permissão. Abaixo estão os passos que poderá ter de tomar:

### <a name="cas-has-a-remote-sql-server"></a>Cas tem um servidor SQL remoto

1. Vá ao servidor SQL de cada site primário.
   1. Adicione o servidor SQL remoto CAS e o servidor do site CAS ao grupo [Configmgr_DviewAccess.](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess)
   ![Configmgr_DviewAccess grupo no servidor SQL de um site primário](media/cmpivot-dviewaccess-group.png)
1. Vá a Utilizadores e Computadores de Diretório Ativo.
   1. Para cada servidor de site primário, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione o serviço de servidor SQL do CAS com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!
   1. Para o site CAS, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione o serviço de servidor SQL de cada site primário com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!

   ![Delegação da CMPivot AD exemplo para lúpulo duplo](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>Cas tem um fornecedor remoto

1. Vá ao servidor SQL de cada site primário.
   1. Adicione a conta de máquina do fornecedor CAS e o servidor do site CAS ao grupo [Configmgr_DviewAccess.](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess)
1. Vá a Utilizadores e Computadores de Diretório Ativo.
   1. Selecione a máquina de fornecedor CAS, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione o serviço de servidor SQL de cada site primário com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!
   1. Selecione o servidor do site CAS, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione o serviço de servidor SQL de cada site primário com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!
1. Reiniciar a máquina de fornecedor remoto CAS.

### <a name="sql-always-on"></a>SQL Sempre Ligado

1. Vá ao servidor SQL de cada site primário.
   1. Adicione o servidor do site CAS ao grupo [Configmgr_DviewAccess.](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess)
1. Vá a Utilizadores e Computadores de Diretório Ativo.
   1. Para cada servidor de site primário, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione as contas de serviço de servidor SQL do CAS para os nós SQL com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!
   1. Selecione o servidor do site CAS, clique à direita e selecione **Propriedades**.
      1. No separador de delegação, escolha a terceira opção, **confie neste computador para delegação apenas para serviços especificados**. 
      1. Escolha **apenas use Kerberos**.
      1. Adicione o serviço de servidor SQL de cada site primário com porta e instância.
      1. Certifique-se de que estas alterações estão alinhadas com a política de segurança da sua empresa!
1. Certifique-se de que o [SPN é publicado](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) para o nome do ouvinte CAS SQL e cada nome de ouvinte SQL primário.
1. Reiniciar os servidores SQL primários.
1. Reiniciar o servidor do site CAS e os servidores CAS SQL.

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot a partir da versão 1906

A partir da versão 1906, foram adicionados à CMPivot os seguintes itens:

- [Junta-se, operadores adicionais e agregadores](#bkmk_cmpivot_joins)
- [Permissões adicionais da CMPivot ao papel de Administrador de Segurança](#bkmk_cmpivot_secadmin1906)
- [CMPivot autónomo](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a>Adicione juntas, operadores adicionais e agregadores na CMPivot
<!--4054074-->
Tem agora operadores aritméticos adicionais, agregadores e a capacidade de adicionar consultas, tais como a utilização do Registo e do Arquivo em conjunto. Foram adicionados os seguintes itens:

#### <a name="table-operators"></a>Operadores de mesa

|Operadores de mesa| Descrição|
|-----|-----|
| [juntar-se](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Fundir as linhas de duas tabelas para formar uma nova tabela combinando linha para o mesmo dispositivo|
|render|Renderiza resultados como saída gráfica|

O operador de renderização já existe na CMPivot. Foram adicionados apoios para várias séries e a **declaração.** Para mais informações, consulte a secção de [exemplos](#bkmk_cmpivot_examples1906) e o artigo do [operador de](https://docs.microsoft.com/azure/kusto/query/joinoperator) kusto.

#### <a name="limitations-for-joins"></a>Limitações para adesão

1. A coluna de adesão é sempre feita implicitamente no campo **dispositivo.**
1. Você pode usar um máximo de 5 juntas por consulta.
1. Pode utilizar um máximo de 64 colunas combinadas.

#### <a name="scalar-operators"></a>Operadores escalares

|Operador| Descrição|Exemplo|
|-----|-----|-----|
| + | Adicionar| `2 + 1, now() + 1d`|
| - |  Subtrair| `2 - 1, now() - 1d`|
| * | Multiplicar| `2 * 2`|
| / | Dividir | `2 / 1`|
| % | Módulo | `2 % 1`

#### <a name="aggregation-functions"></a>Funções de agregação

|Função| Descrição|
|-----|-----|
| percentil()| Devolve uma estimativa para o percentil de nível mais próximo especificado da população definida pela Expr|
| sumif() | Devolve uma soma de Expr para a qual Predicato avalia a verdade|

#### <a name="scalar-functions"></a>Funções escalares

|Função| Descrição|
|-----|-----|
| case()| Avalia uma lista de predicados e devolve a primeira expressão de resultado satisfaça |
| iff() | Avalia o primeiro argumento e devolve o valor do segundo ou terceiro argumentos, dependendo se o predicado avaliado em verdadeiro (segundo) ou falso (terceiro)|
 | indexof() | Função reporta o índice de base zero da primeira ocorrência de uma corda especificada dentro da cadeia de entrada|
| strcat() | Concatenates entre 1 e 64 argumentos |
| strlen()| Devolve o comprimento, em caracteres, da cadeia de entrada|
| substring() | Extrai um substring de uma cadeia de origem que começa de algum índice até ao fim da corda |
| tostring() | Converte a entrada numa operação de cordas |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a>Exemplos

- Mostrar dispositivo, fabricante, modelo e OSVersion:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Mostre o gráfico dos tempos de arranque para um dispositivo:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Gráfico de bar empilhado mostrando tempos de arranque para um dispositivo em ms](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a>Permissões adicionais da CMPivot ao papel de Administrador de Segurança
<!--4683130-->

A partir da versão 1906, foram adicionadas as seguintes permissões ao papel de Administrador de **Segurança** incorporado do Gestor de Configuração:

 - **Ler** no Script SMS
 - **Executar CMPivot** na coleção
 - **Ler** no Relatório de Inventário

>[!NOTE]
> **Executar Scripts** é um super conjunto da permissão **Run CMPivot.**
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a>CMPivot autónomo
<!--3555890, 4619340, 4683130 -->

A partir da versão 1906, pode utilizar a CMPivot como uma aplicação autónoma. A CMPivot autónoma só está disponível em inglês. Execute a CMPivot fora da consola do Gestor de Configuração para ver o estado real dos dispositivos no seu ambiente. Esta alteração permite-lhe utilizar o CMPivot num dispositivo sem antes instalar a consola.

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1906 como uma [funcionalidade de pré-lançamento.](pre-release-features.md) Começando com a versão 2002, já não é uma funcionalidade de pré-lançamento.  

Pode partilhar o poder da CMPivot com outras personalidades, tais como helpdesk ou administradores de segurança, que não têm a consola instalada no seu computador. Estas outras personalidades podem usar cmPivot para consultar o Gestor de Configuração ao lado das outras ferramentas que tradicionalmente utilizam. Ao partilhar estes dados de gestão ricos, pode trabalhar em conjunto para resolver proativamente problemas de negócio que cruzam funções.

#### <a name="install-cmpivot-standalone"></a>Instale o CMPivot sozinho

1. Instale as permissões necessárias para executar a CMPivot. Para mais informações, consulte [os pré-requisitos.](#prerequisites) Também pode utilizar a [função de Administrador](#bkmk_cmpivot_secadmin1906) de Segurança se as permissões forem adequadas para o utilizador.
2. Encontre o instalador de aplicações `<site install path>\tools\CMPivot\CMPivot.msi`CMPivot no seguinte caminho: . Pode executá-lo a partir desse caminho, ou copiá-lo para outro local.
3. Quando executar a aplicação autónoma CMPivot, será-lhe pedido que se ligue a um site. Especifique o nome de domínio ou o nome do computador totalmente qualificados da Administração Central ou do servidor principal do site.
   - Cada vez que abrir o CMPivot sozinho, será solicitado a ligar-se a um servidor do site.
4. Navegue na coleção em que pretende executar a CMPivot e, em seguida, faça a sua consulta.

   ![Navegue na coleção que pretende executar a sua consulta contra](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> As ações de clique satisonárte, tais como **Scripts run,** **Resource Explorer,** e pesquisa web não estão disponíveis em CMPivot autónomamente. O uso principal da CMPivot autónoma está a consultar-se independentemente da infraestrutura do Gestor de Configuração. Para ajudar os administradores de segurança, o CMpivot autónomo inclui a capacidade de se ligar ao Microsoft Defender Security Center. <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot a partir da versão 1910
<!--5410930, 3197353-->
A partir da versão 1910, a CMPivot foi significativamente otimizada para reduzir o tráfego de rede e a carga nos seus servidores. Adicionalmente, foram adicionadas várias entidades e reforços de entidades para ajudar na resolução de problemas e na caça. Foram introduzidas as seguintes alterações para a CMPivot na versão 1910:

- [Otimizações para o motor CMPivot](#bkmk_optimization)
- Entidades adicionais e melhorias de entidades:
  - Registos de eventos windows[(WinEvent)](#bkmk_WinEvent)
  - Conteúdo de ficheiros[(Conteúdo de Ficheiros)](#bkmk_File)
  - Dlls carregados por processos[(ProcessModule)](#bkmk_ProcessModule)
  - Informação de Diretório Ativo Azure[(AADStatus)](#bkmk_AadStatus)
  - Estado de proteção do ponto final[(EPStatus)](#bkmk_EPStatus)
- [Avaliação de consulta de dispositivo local usando CMPivot autónomo](#bkmk_local-eval)
- [Outras melhorias para a CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a>Otimizações para o motor CMPivot
<!--3197353-->
Para reduzir o tráfego de rede e a carga nos seus servidores, a CMPivot foi otimizada em 1910. Muitas operações de consulta são agora realizadas diretamente no cliente e não nos servidores. Esta alteração também significa que algumas operações da CMPivot devolvem dados mínimos da primeira consulta. Se decidir perfurar os dados para obter mais informações, poderá ser executada uma nova consulta para obter os dados adicionais do cliente. Por exemplo, anteriormente, um grande conjunto de dados foi devolvido ao servidor quando executou uma consulta de "contagem resumida".  Ao devolver um grande conjunto de dados oferecido perfuração imediata, muitas vezes apenas a contagem resumida era necessária. Em 1910, quando opta por perfurar um cliente específico, ocorre outra recolha dos dados para devolver os dados adicionais que solicitou. Esta mudança traz um melhor desempenho e escalabilidade para consultas contra um grande número de clientes. <!--3197353, 5458337-->

#### <a name="examples"></a>Exemplos

As otimizações cmpivot reduzem drasticamente a carga CPU de rede e servidor necessária para executar consultas CMPivot. Com estas otimizações, podemos agora vasculhar os gigabytes de dados do cliente em tempo real. As seguintes consultas ilustram estas otimizações:

- Procure todos os registos de eventos em todos os clientes da sua empresa para obter falhas de autenticação.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Procure um ficheiro por hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>WinEvent,\<nome de\<>>,]

Esta entidade é usada para obter eventos a partir de registos de eventos e ficheiros de registo de rastreio de eventos. A entidade obtém dados de registos de eventos que são gerados pela tecnologia Windows Event Log. A entidade também obtém eventos em ficheiros de registo gerados por Event Tracing for Windows (ETW). WinEvent olha para os eventos que ocorreram nas últimas 24 horas por padrão. No entanto, o padrão de 24 horas pode ser ultrapassado, incluindo uma hora.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>FileContent\<(nome de ficheiro>)

FileContent é usado para obter o conteúdo de um ficheiro de texto.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>Módulo de\<Processos(> de processo)  

Esta entidade é usada para enumerar os módulos (dlls) carregados por um determinado processo. ProcessModule é útil na caça de malware que se esconde em processos legítimos.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a>AadStatus

Esta entidade pode ser usada para obter a informação de identidade do Atual Diretório Ativo Azure a partir de um dispositivo.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a>EPStatus

O EPStatus é utilizado para instalar o estado do software antimalware no computador.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a>Avaliação de consulta de dispositivo local usando CMPivot autónomo
<!--3197353-->
Ao utilizar o CMPivot fora da consola do Gestor de Configuração, pode consultar apenas o dispositivo local sem a necessidade da infraestrutura do Gestor de Configuração. Agora pode aproveitar as consultas CMPivot Azure Log Analytics para visualizar rapidamente as informações do WMI no dispositivo local. Isto também permite validação e refinação de consultas CMPivot, antes de executá-las em um ambiente maior. A CMPivot autónoma só está disponível em inglês. Para obter mais informações sobre a instalação autónoma da CMPivot, consulte instalar a [CMPivot autónoma](#install-cmpivot-standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Questões conhecidas para avaliação de consulta de dispositivolocal

 - Se consultar **este PC** por uma entidade WMI a que não tem acesso, como uma classe WMI bloqueada, poderá ver um acidente na CMPivot. Executar a CMPivot usando uma conta com privilégios elevados para consultar essas entidades. <!--5753242-->
- Se consultar entidades não-WMI **neste PC,** verá um espaço de **nome inválido** ou uma exceção ambígua.
- Execute a CMPivot autónoma a partir do atalho do menu inicial, não diretamente a partir do caminho do ficheiro executável. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Outras melhorias

- Pode fazer consultas regulares de `like` tipo de expressão utilizando o novo operador. Por exemplo:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Atualizámos as entidades **ccmLog()** e **EventLog** para apenas olhar mensagens nas últimas 24 horas por padrão. Este comportamento pode ser ultrapassado passando numa situação de tempo opcional. Por exemplo, a seguinte consulta analisará os eventos na última hora:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- A entidade **de Arquivo()** foi atualizada para recolher informações sobre ficheiros Ocultos e Sistemas, e incluir o haxixe MD5. Embora um hash MD5 não seja tão preciso como o hash SHA256, tende a ser o hash geralmente relatado na maioria dos boletins de malware.  

- Pode adicionar comentários em consultas.<!-- 5431463 --> Este comportamento é útil na partilha de consultas. Por exemplo:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- A CMPivot liga-se automaticamente ao último local.<!-- 5420395 --> Depois de iniciar a CMPivot, pode ligar-se a um novo site, se necessário.

- A partir do menu **Export,** selecione a nova opção para **a ligação Consulta à área de recortes**.<!-- 5431577 --> Esta ação copia um link para a área de prancheta que pode partilhar com os outros. Por exemplo:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Este link abre a CMPivot autónoma com a seguinte consulta:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Para que este link funcione, [instale a CMPivot autónoma](#install-cmpivot-standalone).

- Nos resultados da consulta, se o dispositivo estiver inscrito no Microsoft Defender Advanced Threat Protection (ATP), clique no dispositivo para lançar o portal online **Microsoft Defender Security Center.**

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Questões conhecidas para cmPivot na versão 1910

- O banner de resultados máximos não pode ser apresentado quando o limite for atingido. <!--5431427-->
  - Cada cliente está limitado a 128 KB de dados por consulta.
  - Os resultados podem ser truncados se os resultados da consulta excederem 128 KB.
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a>CMPivot a partir da versão 2002
<!--5870934-->
Tornámos mais fácil navegar em entidades cmpivot. A partir da versão De Configuração Manager 2002, pode pesquisar entidades CMPivot. Novos ícones também foram adicionados para diferenciar facilmente as entidades e os tipos de objetos da entidade.

![Pesquisar entidades CMPivot](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>Dentro da CMPivot

A CMPivot envia consultas aos clientes que usam o "canal rápido" do Gestor de Configuração. Este canal de comunicação de servidor para cliente também é utilizado por outras funcionalidades, tais como ações de notificação de clientes, estado do cliente e Proteção de Endpoint. Os clientes devolvem os resultados através do sistema de mensagens estatais igualmente rápido. As mensagens de Estado são armazenadas temporariamente na base de dados. Para mais informações sobre as portas utilizadas para notificação do cliente, consulte o artigo [Portos.](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP)

As consultas e os resultados são apenas texto. As entidades **InstallSoftware** e **Process** devolvem alguns dos maiores conjuntos de resultados. Durante os testes de desempenho, o maior tamanho de ficheiro de mensagem estatal de um cliente para estas consultas foi inferior a **1 KB**. Dimensionado para um grande ambiente com 50.000 clientes ativos, esta consulta única geraria menos de 50 MB de dados em toda a rede. Todos os itens na página de boas-vindas que são sublinhados, devolverão menos de 1k de informação por cliente.

![CmPivot sublinhou exemplo de entidades](media/cmpivot-underlined-entities.png)

A partir do Diretor de Configuração 1810, a CMPivot pode consultar dados de inventário de hardware, incluindo aulas de inventário de hardware alargadas. Estas novas entidades (entidades não sublinhadas na página de boas-vindas) podem devolver conjuntos de dados muito maiores, dependendo da quantidade de dados definidos para uma determinada propriedade de inventário de hardware. Por exemplo, a entidade "Executável Instalada" pode devolver vários MB de dados por cliente, dependendo dos dados específicos em que consulta. Esteja atento ao desempenho e escalabilidade dos seus sistemas ao devolver conjuntos de dados de inventário de hardware maiores de coleções maiores utilizando a CMPivot.

Uma consulta sai depois de uma hora. Por exemplo, uma coleção tem 500 dispositivos, e 450 dos clientes estão atualmente online. Estes dispositivos ativos recebem a consulta e devolvem os resultados quase imediatamente. Se deixar a janela CMPivot aberta, à medida que os outros 50 clientes ficam on-line, também recebem a consulta e devolvem os resultados. 

## <a name="log-files"></a>Ficheiros de registo

 As interações CMPivot são registadas nos seguintes ficheiros de registo:

**Lado do servidor:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**Do lado do cliente:**
- CcmNotificationAgent.log
- Scripts.log
- StateMessage.log

Para mais informações, consulte [ficheiros de registo](../../plan-design/hierarchy/log-files.md) e [acpivagem de problemas CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Passos seguintes
 
[Resolução de Problemas do CMPivot](cmpivot-tsg.md)

[Criar e executar scripts do PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)


