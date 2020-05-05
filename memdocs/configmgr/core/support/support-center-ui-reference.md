---
title: Referência ui do Centro de Suporte
titleSuffix: Configuration Manager
description: Aprenda a utilizar as ferramentas do Centro de Suporte.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43bb35243b4f7e7b1e45b66319efd4ec21e92542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718617"
---
# <a name="support-center-user-interface-reference"></a>Referência de interface de utilizador do Centro de Suporte

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo é uma referência que descreve as interfaces de utilizador (UI) das ferramentas do Centro de Suporte:
- Centro de Suporte
- Espectador de log do centro de suporte
- Espectador do Centro de Suporte



## <a name="support-center-reference"></a>Referência do Centro de Apoio

Esta secção descreve a interface do utilizador para a ferramenta Do Centro de **Suporte.** 
- [Menu da janela](#bkmk_support-window)  
- [Separador Base](#bkmk_support-home)  
- [Separador de cliente](#bkmk_support-client)  
- [Separador de política](#bkmk_support-policy)  
- [Separador de conteúdo](#bkmk_support-content)  
- [Separador de inventário](#bkmk_support-inventory)  
- [Separador de resolução de problemas](#bkmk_support-troubleshoot)  
- [Separador de registos](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a>Menu da janela

No canto superior esquerdo da janela do Centro de Apoio, selecione a seta na caixa azul para abrir este menu.

#### <a name="local-machine-connection"></a>Conexão de máquina local
O Centro de Suporte reúne ficheiros de registo e realiza resolução de problemas no cliente que está a gerir o Centro de Suporte.

#### <a name="remote-connection"></a>Ligação Remota
Estabeleça uma ligação remota com outro cliente do Gestor de Configuração. Após a ligação, o Support Center recolhe ficheiros de registo e realiza resolução de problemas no cliente ao qual está ligado.

#### <a name="about"></a>Acerca de
Fornece informações sobre o Centro de Apoio.

#### <a name="options"></a>Opções
No diálogo **Opções,** pode:
- Reduzir o movimento de elementos de interface de utilizador animados  
- Alterar a localização de predefinição para ficheiros de pacotes de dados  
- Alterar a localização dos ficheiros temporários    
- Repor os avisos. Quaisquer mensagens de aviso que tenha suprimido anteriormente aparecem novamente quando ativadas.  
- Redefinir o caminho de ficheiro temporário para o padrão,`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Exit
Centro de Apoio Imediato.



### <a name="home-tab"></a><a name="bkmk_support-home"></a>Separador de casa

#### <a name="collect-selected-data"></a>Recolher dados selecionados
O Centro de Suporte recolhe informações do cliente do Gestor de Configuração. Por predefinição, recolhe os seguintes tipos:
- Ficheiros de registo
- Colecionador de configuração do cliente
- Sistema operativo

Para recolher outros tipos de informação, selecione a caixa de verificação ao lado do nome para esse tipo.

Selecione a gota na parte inferior do botão de **dados selecionado seleto** na fita e selecione **Recolher todos os dados**. Esta ação recolhe o conjunto completo de dados do Estado cliente.

Enquanto o Centro de Suporte está a recolher dados, selecione **cancelar a recolha** para detê-lo.

#### <a name="data-types"></a>Tipos de dados
Quando seleciona a caixa de verificação para uma opção, o Support Center recolhe esse tipo de dados da próxima vez que selecionar **Recolher dados selecionados**. Estão disponíveis os seguintes tipos:  

- **Ficheiros de registo**: Ficheiros de registo do cliente, incluindo registos de configuração  

- **Política**: Recolha de política do cliente  

- **Certificados**: Informação chave pública para certificados de cliente. O Centro de Apoio não recolhe chaves privadas de certificado.  

- **Colecionador de configuração do cliente**: Informações do cliente do Gestor de Configuração. Não pode desativar este tipo de dados.  

- **Registo do cliente**: Recolhe informações de configuração do cliente a partir do registo. O Centro de Suporte recolhe apenas informações sobre o registo do Gestor de Configuração.  

- **Client WMI**: Informação de configuração do cliente da WMI. O Centro de Apoio não recolhe a política do cliente.  

- **Resolução de problemas**: Dados de resolução de problemas em tempo real para ajudar a diagnosticar problemas comuns de clientes com Diretório Ativo, pontos de gestão, networking, atribuições de políticas e registo.  

    > [!NOTE]  
    > Este tipo de dados não é suportado quando se faz uma ligação remota a outro cliente.  

- **Despejos de depuração**: Realizar despejo de depuração de clientes e processos relacionados. As lixeiras de depuração podem ser grandes. Só ative esta opção quando resolver problemas com o desempenho do cliente.  

    > [!WARNING]  
    > A recolha de despejos de depuração fará com que os pacotes de dados se tornem muito grandes (em alguns casos, várias centenas de MB).  
    >  
    > As descargas de depuração contêm informações sensíveis, incluindo palavras-passe, segredos criptográficos ou dados do utilizador. As descargas de depuração só devem ser recolhidas por recomendação do pessoal do Microsoft Support. Os pacotes de dados que contenham despejos de depuração devem ser manuseados cuidadosamente para protegê-los de acesso não autorizado.  
    >  
    > Este tipo de dados não é suportado quando se faz uma ligação remota a outro cliente.  

- **Sistema operativo**: Recolhe informações de configuração sobre a máquina local. Estes dados incluem informações sobre a instalação do Windows, adaptadores de rede e configuração do serviço do sistema. Não pode desativar este tipo de dados.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a>Separador de cliente

#### <a name="load-or-refresh"></a>Carregar ou refrescar
O Centro de Suporte carrega ou atualiza detalhes para o cliente do Gestor de Configuração.

#### <a name="control-client-agent-service"></a>Controlar o serviço de agente cliente
Realizar uma das seguintes ações no serviço de agente cliente do Gestor de Configuração (ccmexec) no cliente conectado:  

- **Reiniciar cliente**  

    > [!IMPORTANT]  
    > Se o serviço de agente cliente não reiniciar com sucesso, o cliente não será gerível pelo Gestor de Configuração até que o serviço comece.  

- **Iniciar cliente**  

- **Parar o cliente**  

    > [!IMPORTANT]  
    > O cliente não é gerível pelo Gestor de Configuração até que o serviço comece.  

#### <a name="properties"></a>Propriedades
Quando carrega detalhes do cliente, o Centro de Suporte mostra as seguintes propriedades:  

- **ID do cliente**: Um identificador único que o Gestor de Configuração utiliza para identificar o cliente  

- **ID de hardware**: Um identificador único que o Gestor de Configuração usa para identificar o hardware do cliente  

- **Aprovado**: Indica se o cliente é aprovado no Gestor de Configuração  

- **Estado de Registo**: Indica se o cliente está registado no Gestor de Configuração  

- **Virado para a Internet**: Indica se o cliente está na internet  

- **Versão**: O número de versão do cliente do Gestor de Configuração instalado  

- **Código do Site**: O código do site para o local principal a que o cliente é atribuído  

- **MP atribuído**: O nome de domínio totalmente qualificado (FQDN) do ponto de gestão atribuído atualmente  

- **MP residente**: FQDN do ponto de gestão de residentes  

- **Proxy MP**: O nome de anfitrião ou FQDN do ponto de gestão proxy (se existir)  

- **Código do site proxy**: O código do site para o site secundário (se existir)  

- **Estado proxy**: O estado do ponto de gestão de procuração do cliente do Gestor de Configuração. Por exemplo, **Ativo** ou **Pendente**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a>Separador de política

Utilize as ações neste separador em vez da ferramenta [PolicySpy](policy-spy.md) mais antiga.

#### <a name="load-policy"></a>Política de carga
Esta opção varia consoante a vista:

- **Carregar a política real**: Selecione **Real** no grupo 'Ver' e, em seguida, selecione esta opção no grupo Política. O Centro de Suporte carrega a política do cliente que selecionou atualmente.  

- **Política solicitada**de carga : Selecione **Solicitado** no grupo 'Ver' e, em seguida, selecione esta opção no grupo Política. O Centro de Apoio carrega a política do cliente solicitada ao cliente.  

- **Política de padrão de carga**: Selecione **Predefinido** no grupo 'Ver' e, em seguida, selecione esta opção no grupo Política. O Centro de Suporte carrega a política de incumprimento para este cliente.  

Selecione a lista de drop-down na parte inferior deste botão para opções adicionais:

- **Carregar ou refrescar tudo:** Carrega ou atualiza a política real, solicitada e predefinida ao mesmo tempo.  

#### <a name="actual-view"></a>Vista real
Abre a visão política real

#### <a name="requested-view"></a>Vista solicitada
Abre a visão política solicitada

#### <a name="default-view"></a>Vista predefinida
Abre a visão de política padrão. (Esta política é o que os dispositivos obtêm quando instala o cliente do Gestor de Configuração.)

#### <a name="request-and-evaluate-policy"></a>Política de solicitar e avaliar
O Centro de Apoio solicita a política do cliente a partir do ponto de gestão e, em seguida, avalia essa política sobre o cliente.

Selecione a lista de drop-down na parte inferior deste botão para opções adicionais:  

- **Política de pedido**: Centro de Apoio solicita a política do cliente do ponto de gestão.  

- **Política de avaliação**: Centro de Apoio avalia a política do cliente sobre o cliente.  

- **Redefinir a política para padrão**: O Centro de Suporte diz ao cliente do Gestor de Configuração para reaplicar a política de predefinição. Remove todas as políticas de máquinas e utilizadores do cliente.  

#### <a name="listen-for-policy-events"></a>Ouça eventos políticos
Centro de Apoio ouve eventos políticos. Selecione novamente esta opção para desativar a audição de eventos políticos. Para visualizar **os eventos de política,** selecione a seta na parte inferior deste separador. 

#### <a name="clear-events"></a>Eventos claros
O Centro de Apoio iliba quaisquer eventos políticos.



### <a name="content-tab"></a><a name="bkmk_support-content"></a>Separador de conteúdo

Ver conteúdo sobre o cliente, incluindo conteúdo em cache. Monitorize o progresso das implementações de atualizações e aplicações de software. 

#### <a name="load-or-refresh"></a>Carregar ou refrescar
*Aplica-se às vistas de Conteúdo e Cache*

O Centro de Suporte carrega ou atualiza a lista de conteúdos atualmente no cliente.

#### <a name="invoke-trigger"></a>Invocar gatilho
Os seguintes itens neste menu solicitam uma ação do cliente relacionada com conteúdos:  

- **Serviços de localização**  

    - **Refresh localização de conteúdo**: Atualiza os pontos de distribuição utilizados por quaisquer transferências de conteúdo ativo.  

    - **Pontos de gestão atualizados**: Atualiza a lista interna de pontos de gestão utilizados pelo cliente.  

    - **Pedidos**de conteúdo time out : Se algum pedido de localização de conteúdo estiver em execução por muito tempo, esta ação interrompe o pedido.  

- **Avaliação de implementação**de aplicações : Inicia uma tarefa que avalia as aplicações implementadas.  

- **Avaliação**de implementação de atualizações de software : Inicia uma tarefa que avalia as atualizações de software implementadas.  

- **Software atualiza a imagem de origem**: Inicia uma tarefa que digitaliza as localizações de origem.  

- Atualização da lista de **fontes do Instalador do Windows**: Inicia uma tarefa que atualiza a localização de origem das instalações do Instalador do Windows (MSI).  

#### <a name="content-view"></a>Vista de conteúdo
Consulte aplicações, pacotes e atualizações que são carregadas no cliente. Quando selecionar uma aplicação, pacote ou atualização, pode visualizar detalhes sobre esse conteúdo. Para algumas aplicações, também pode fazer as seguintes ações:  

- **Atualização**: Refrescar a vista dos detalhes  

- **Verificar ou Descarregar:** Verifique se uma aplicação está disponível para download  

- **Instalação**: Instalar a aplicação  

- **Desinstalar**: Desinstalar a aplicação  

#### <a name="cache-view"></a>Vista cache
Consulte a configuração da cache do cliente e detalhes sobre o conteúdo da cache. Quando liga o Centro de Apoio a um cliente local, também faz as seguintes ações:  

- Para alterar a localização da cache, selecione **Alterar** ao lado do campo de **localização Cache.**  

- Para ajustar o tamanho da cache, selecione **Alterar** ao lado do campo **tamanho cache.**  

- Para limpar a cache do cliente, selecione **Clear** junto ao **campo de utilização Cache.**  

Esta vista mostra as seguintes propriedades:  

- **Localização**: A localização de cada pasta cache. Selecione o link para abrir a pasta no Windows Explorer.   
- **ID de conteúdo**  
- **Cache ID**  
- **Tamanho**  
- **Última Referência**: Esta propriedade é a data em que o cliente leu pela última vez ou escreveu a este item na cache.  

#### <a name="monitoring-view"></a>Vista de monitorização
Selecione **Monitor** para ver o progresso ativo das implementações de atualizações de software e atualizações de aplicações. Esta visão mostra mensagens estatais levantadas a partir de mensagens WMI de aplicação e atualizações de software.

Para cada evento, a vista mostra as seguintes propriedades:  

- **Tempo**: O tempo que o cliente levantou o evento  
- **Tipo de tópico**: O tipo de mensagem de estado  
- **Id**tópico : ID da mensagem do Estado, usado para mapear eventos em ficheiros de registo  
- **Tipo de ID**tópico : O subtipo da mensagem de estado  
- **ID do Estado**: O resultado da ação que está a monitorizar  
- **Detalhes** e dados do **Evento**: Mais informações sobre as mensagens de Estado mostradas nesta opinião. Os detalhes do estado podem, por vezes, estar em branco.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a>Separador de inventário

#### <a name="load-or-refresh"></a>Carregar ou refrescar
O Centro de Suporte carrega ou atualiza a lista de inventário do cliente para a vista atualmente selecionada.

#### <a name="invoke-trigger"></a>Invocar gatilho

> [!Note]  
> Para tarefas que não o ciclo de relatório de medição de **software:**  
> - Se solicitar a tarefa quando outra tarefa de inventário já está em execução, o cliente faz fila com a nova tarefa a executar depois de completar a tarefa atual e outras tarefas em fila.  
> - Acompanhe o progresso da tarefa em **InventoryAgent.log**.  

Os seguintes itens neste menu solicitam ação do cliente relacionada com inventário:  

- **Discovery data collection cycle (heartbeat)**: Desencadeia a tarefa do cliente usada para recolher informações sobre descobertas de dispositivos  

- Ciclo de recolha de **ficheiros**: Despoleta a tarefa do cliente utilizada para recolher ficheiros locais  

- Ciclo de inventário de **hardware**: Despoleta a tarefa do cliente usada para recolher dados de inventário de hardware  

- **Ciclo de recolha idmif**: Aciona a tarefa do cliente usada para recolher dados do IDMIF  

- **Ciclo**de inventário de software : Desencadeia a tarefa do cliente usada para recolher dados de inventário de software  

- Ciclo de **relatório de medição**de software : Aciona a tarefa do cliente usada para construir um relatório de medição de software e enviá-lo para o ponto de gestão. Acompanhe o progresso desta tarefa em **SWMTRReportGen.log**.

- **Envie mensagens estatais não enviadas na fila**: Aciona a tarefa do cliente para descarregar a fila de mensagens do Estado.

- **Avançado**  
    - **Ciclo de inventário de hardware (resincronização completa)**  
    - **Ciclo de inventário de software (resincronização completa)**  


#### <a name="views"></a>Vistas
Se uma funcionalidade não estiver ativada, a visualização não apresenta quaisquer dados. 

- **Estado**: Mostrar os conjuntos de dados de inventário que o cliente recolheu  

- **DDR**: Informação sobre os dados de descoberta do cliente recolhidos do cliente  

- **HINV**: Informações sobre os dados de inventário de hardware recolhidos do cliente  

- **SINV**: Informações sobre os dados de inventário de software recolhidos do cliente  

- **Recolha de ficheiros**: Informações sobre os ficheiros recolhidos do cliente  

- **IDMIF**: Informações sobre os dados do IDMIF e no IDMIF recolhidos do cliente  

- **Medição**: Informação sobre os dados de medição de software recolhidos do cliente  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a>Separador de resolução de problemas

Problemas de resolução de alguns dos problemas mais comuns com clientes do Gestor de Configuração:  
- Problemas com Diretório Ativo  
- Rede de janelas  
- Gestor de configuração   
    - Pontos de gestão  
    - Atribuição de política  
    - Registo  


> [!NOTE]  
> Este separador não está disponível quando se conecta a um cliente remoto do Gestor de Configuração.


#### <a name="start"></a>Iniciar
Começa a resolver problemas com o cliente

- **Diretório Ativo**: Consultas Ative Directory para recuperar informações publicadas do site do Gestor de Configuração  
- **MPCERTIFICATE**: Obtém certificados de ponto de gestão  
- **MPLIST**: Obtém uma lista de pontos de gestão  
- **MPKEYINFORMATION**: Obtém informações de chave criptográfica do ponto de gestão  
- **Networking**: Problemas de resolução de problemas com networking  
- **Atribuição de Políticas**: Recupera atribuições políticas  
- **Registo**: Verifica se o cliente está registado no site  

#### <a name="view-selected-log"></a>Ver registo selecionado
Depois de selecionar uma linha no separador Deresolução de Problemas, selecione esta ação para visualizar o ficheiro de registo.

#### <a name="keep-previous-results"></a>Manter resultados anteriores
Se resolver o problema com o cliente e, em seguida, querer tentar resolução de problemas novamente, escolha esta opção para reter resultados da sua primeira tentativa. Caso contrário, o Centro de Suporte substitui ficheiros de registo de resolução de problemas anteriores.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a>Separador de registos

Esta secção lista os itens no separador **Logs** da ferramenta Centro de Suporte. 

Este separador é quase idêntico à ferramenta **Log Viewer.** A ferramenta **Log Viewer** não inclui as funcionalidades de registo do **cliente Configure** e **dos grupos de registo descritos** nesta secção. A secção de referência do Observador de [Registo do Centro](#bkmk_log-viewer) de Suporte detalha as outras opções disponíveis neste separador.

#### <a name="configure-client-logging"></a>Configurar a exploração madeireira do cliente

Definir as seguintes opções: 
- **Nível de registo do cliente**: Verbosidade de log e tamanho de ficheiro  
- **Contagem máxima de ficheiros**: Permitir mais de um ficheiro de registo de um determinado tipo  
- **Tamanho máximo**do ficheiro : O tamanho em bytes de qualquer ficheiro de registo dado antes do cliente criar um novo registo  

> [!NOTE]  
> Se definir estes valores demasiado baixos, o cliente pode não registar qualquer informação útil. Se definir estes valores demasiado altos, os registos do cliente podem consumir grandes quantidades de armazenamento.  

#### <a name="log-groups"></a>Grupos de registo

Em vez de selecionar manualmente ficheiros de registo utilizando o botão **'Iniciar sessão',** utilize esta lista de lançamentos para abrir todos os ficheiros de registo associados às seguintes áreas de recurso: 
- **Gestão de Configuração Desejada**
- **Inventário**
- **Distribuição de Software**
- **Atualizações de software**
- **Gestão de Aplicações**
- **Policy**
- **Registo do Cliente**
- **Implantação do sistema operativo**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a>Referência do espectador de log do centro de suporte

Esta secção descreve a interface do utilizador para a ferramenta de visualização de log do Centro de **Suporte.** 

- [Menu da janela](#bkmk_log-window)  
- [Separador Base](#bkmk_log-home)  

A ferramenta **Log Viewer** é quase idêntica ao separador **Logs** do Centro de **Suporte**. A ferramenta **Log Viewer** não inclui as opções para **configurar** os **grupos**de registo de clientes e log .


### <a name="window-menu"></a><a name="bkmk_log-window"></a>Menu da janela

No canto superior esquerdo da janela do Visualizador de Registo do Centro de Suporte, selecione a seta na caixa azul para abrir este menu.

#### <a name="open-logs"></a>Abrir registos
Navegue na localização dos ficheiros de registo para abrir. 

#### <a name="options"></a>Opções
No diálogo **Opções,** pode:
- Reduzir o movimento de elementos de interface de utilizador animados  
- Registe o 'Visualizador de Registos' como a aplicação predefinida para ficheiros de registo com as extensões de ficheiro .log e .lo_  
- Repor os avisos. Quaisquer mensagens de aviso que tenha suprimido anteriormente aparecem novamente quando ativadas.  

#### <a name="about"></a>Acerca de
Exibe informações sobre o Visualizador de Registo do Centro de Suporte

#### <a name="close"></a>Fechar
Fecha o espectador de log do centro de suporte


### <a name="home-tab"></a><a name="bkmk_log-home"></a>Separador de casa

#### <a name="open-logs"></a>Abrir registos 
O Centro de Suporte pede-lhe que selecione um ou mais ficheiros de registo para abrir.

Selecione a gota na parte inferior do botão **de registos Abertona** fita e selecione uma das seguintes opções adicionais: 
- **Abrir registos na vista atual**: Abre os ficheiros de registo selecionados na vista atual  
- **Abrir registos em nova janela**: Abre os ficheiros de registo selecionados numa nova janela **do Log Viewer**  

#### <a name="close-and-clear-logs"></a>Registos de fecho e de sumo claro
Fecha quaisquer ficheiros de registo abertos. Também limpa quaisquer entradas de ficheiros de registo exibidos da janela. O Centro de Apoio não apresentará estas entradas no futuro.

Selecione a descida na parte inferior do botão **de registos Close e Clear** na fita e selecione uma das seguintes opções adicionais: 
- **Limpar todas as entradas**: Limpa quaisquer entradas de ficheiros de registo visualizadas da janela. O Centro de Apoio não apresentará estas entradas no futuro.  
- **Fechar todos os registos**: Fecha quaisquer ficheiros de registo abertos  

#### <a name="find"></a>Localizar
Abre o diálogo **Find.** Introduza uma corda para procurar. Para evitar fósforos em cordas curtas noutras cordas, pode optar por combinar palavras inteiras. Também pode optar por fazer uma correspondência sensível a casos para a corda.

#### <a name="find-next"></a>Encontre o próximo
Depois de encontrar uma correspondência para a corda que procura, esta opção leva-o ao próximo jogo.

#### <a name="find-previous"></a>Encontrar anteriores
Depois de encontrar dois ou mais fósforos para a corda que procura, esta opção leva-o ao jogo anterior.

#### <a name="options"></a>Opções

- **Atualização ao vivo:** Monitorize um ficheiro de registo aberto para alterações. Esta funcionalidade não funciona quando vários ficheiros de registo estão abertos. Por predefinição, esta opção encontra-se ativada.  

- **Auto-scroll**: Se também escolheu a opção de **atualização ao vivo,** esta opção desloca automaticamente a vista de registo para mostrar as entradas recém-adicionadas. Esta funcionalidade não funciona quando vários ficheiros de registo estão abertos. Por predefinição, esta opção encontra-se ativada.  

- **Mostrar detalhes**: Quando selecionar uma mensagem de ficheiro de registo, a parte inferior do separador **Logs** mostra os detalhes da mensagem de ficheiro de registo. Por predefinição, esta opção encontra-se ativada.  

- **Filtro rápido:** Filtrar as mensagens de ficheirode registo em todos os ficheiros de registo abertos para encontrar uma cadeia específica. Pode filtrar por texto de registo, nome do componente e ID da linha. Para encontrar mensagens de registo semelhantes, clique numa mensagem de registo e selecione **filtro Quick** no texto de registo.  

- **Texto de registo de embrulho**: Enrole mensagens longas e multi-linhas para caber numa única coluna. Este comportamento torna estas mensagens mais fáceis de ler. Por predefinição, esta opção encontra-se ativada.  

- **Display de entrada**de registo bruto : Exibe linhas de registo não processadas.  

- **Filtros avançados**: Abra o diálogo dos **filtros avançados.** Para mais informações, consulte [filtros de ficheiros de registo avançados](#bkmk_adv-filters).  

- **Links de código**de erro : Os códigos de erro no texto de registo são realçados e clicáveis. Por predefinição, esta opção encontra-se ativada.  

#### <a name="error-lookup"></a>Procura de erros
Introduza um código de erro para procurar esse código de erro nos ficheiros de registo atualmente abertos. Utilize os seguintes formatos de código de erro:
- **32 bits inteiro (assinado)**: Por exemplo,`-2147024891`  
- **32 bits inteiro (não assinado)**: Por exemplo,`2147942405`  
- **Hexadecimal de 32 bits:** Por exemplo,`0x80070005`  

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a>Filtros avançados de ficheiros de log

Filtros avançados de ficheiros de registo permitem-lhe incluir, excluir ou destacar cordas específicas. Estas cordas podem ocorrer num ficheiro de registo ou num grupo de ficheiros de registo quando se olha para as entradas de ficheiros de registo. Utilize pesquisas de wildcard ao criar um filtro. Quando tiver uma combinação útil de filtros, guarde-os como um conjunto de *filtros*. 

Filtros avançados de ficheiros de log superam filtros rápidos. Utilize ambos juntos, mas filtros rápidos aplicam-se apenas aos dados de registo apresentados. Filtros avançados determinam quais os dados inicialmente apresentados antes de aplicar quaisquer filtros rápidos.

No diálogo de filtros Avançados, pode criar conjuntos complexos de filtros. Estes conjuntos de filtros procuram cordas em muitos componentes de ficheiros de registo. Estes componentes incluem mensagens, fios, níveis de registo e componentes. Um conjunto de filtro contém múltiplas declarações de filtro que utiliza para incluir, excluir ou destacar mensagens de ficheirode ficheiro. Um filtro define uma coluna de ficheiros de registo para pesquisar dentro, um operador e um valor. O valor pode conter expressões regulares, como o caráter `*` *wildcard.*


### <a name="add-a-filter"></a>Adicionar um filtro

1. Na janela **'Visualizador** de Registos', ou no separador **registos** do Centro de Suporte, selecione **filtros Avançados**.  

2. No diálogo avançado de filtros, **selecione Adicionar**. Em seguida, selecione uma das seguintes opções para atuar nas entradas de registo que correspondam ao seu filtro:  
    - **Incluir**  
    - **Excluir**  
    - **Realce**  

3. No diálogo avançado de configuração do **filtro,** escolha uma coluna e um operador:  

    - **Coluna**: Escolha onde procurar cordas que correspondam ao filtro:  

         - **Texto de log**: Pesquisar dentro do texto de um ficheiro de registo  

         - **Severidade do registo**: Procure registos com um nível de gravidade específico. Descoloque estes níveis de gravidade no campo **Valor.**  

         - **Componente**: Procurar um componente específico por nome  

         - **ID do fio**: Procure mensagens de registo com um ID de linha específico  

         - **Ficheiro fonte**: Procurar mensagens de registo que ocorram num ficheiro de registo específico  

    - **Operador**: Escolha um operador para o seu filtro  

4. Introduza um valor para filtrar no campo **Valor.** Se o seu valor contiver expressões regulares, **selecione Ativar a correspondência regular de expressão**.  


### <a name="manage-filter-sets"></a>Gerir conjuntos de filtros

- Para editar um filtro, selecione o filtro e, em seguida, **selecione Editar**.  

- Para eliminar um filtro, selecione o filtro e, em seguida, **selecione Eliminar**.  

- Para limpar todos os filtros, selecione **Clear**.  

- Para salvar o conjunto de filtros atual, selecione **Guardar filtros**. Em seguida, guarde o seu conjunto de filtro como um ficheiro **.filterset.**  

- Para carregar um conjunto de filtros guardado, selecione **filtros de carga**. Em seguida, navegue para um ficheiro **.filterset** previamente guardado.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a>Referência do Espectador do Centro de Suporte

Esta secção descreve a interface do utilizador (UI) para a ferramenta do **Visualizador** do Centro de Suporte do Gestor de Configuração. Os separadores disponíveis variam em função do conteúdo do pacote de resolução de problemas. O [menu Janela](#bkmk_viewer-window) e o [separador Home](#bkmk_viewer-home) mostram por defeito.
- [Menu da janela](#bkmk_viewer-window)
- [Separador Base](#bkmk_viewer-home)
- [Separador de configuração](#bkmk_viewer-config)
- [Separador de registos](#bkmk_viewer-logs)
- [Separador de despejos de depurado](#bkmk_viewer-debug)
- [Separador WMI](#bkmk_viewer-wmi)
- [Separador de registo](#bkmk_viewer-registry)
- [Separador de política](#bkmk_viewer-policy)
- [Separador de certificados](#bkmk_viewer-certs)
- [Separador de resolução de problemas](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a>Menu da janela

No canto superior esquerdo da janela do Espectador do Centro de Apoio, selecione a seta na caixa azul para abrir este menu.

#### <a name="open-bundle"></a>Pacote aberto
Navegue na localização de um pacote de dados criado pelo Centro de Suporte.

#### <a name="about"></a>Acerca de
Exibe informações sobre o Espectador do Centro de Suporte.

#### <a name="options"></a>Opções
No diálogo **Opções,** pode:
- Reduzir o movimento de elementos de interface de utilizador animados  
- Alterar a localização dos ficheiros temporários    
- Repor os avisos. Quaisquer mensagens de aviso que tenha suprimido anteriormente aparecem novamente quando ativadas.  
- Redefinir o caminho de ficheiro temporário para o padrão,`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Exit
Saídas Espectador do Centro de Suporte


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a>Separador de casa

#### <a name="open-bundle"></a>Pacote aberto
Navegue na localização de um pacote de dados criado pelo Centro de Suporte.

#### <a name="open-log-file"></a>Abrir ficheiro de registo
Selecione um ou mais ficheiros de registo para abrir.

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a>Separador de configuração

O separador de **configuração** da ferramenta De saída do Centro de Suporte fornece as seguintes vistas utilizando dados recuperados de fornecedores de WMI:

#### <a name="client"></a>Cliente
Esta vista exibe as mesmas informações mostradas no separador **Cliente** do Centro de Suporte.

#### <a name="operating-system"></a>Sistema operativo
Detalhes para o sistema operativo do cliente. Usa a aula [de Win32_OperatingSystem.](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem)

#### <a name="computer"></a>Computador
Detalhes para o computador cliente. Usa a aula [de Win32_OperatingSystem.](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem)

#### <a name="services"></a>Serviços
Detalhes para serviços em execução no computador cliente. Usa a aula [de Win32_Service.](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service)

#### <a name="network-adapters"></a>Placas de rede
Detalhes para adaptadores de rede instalados no computador cliente. Usa a aula [de Win32_NetworkAdapterConfiguration.](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration)


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a>Separador de registos

O separador **Logs** mostra uma lista dos ficheiros de registo incluídos no pacote. Cada linha neste separador fornece o caminho, o nome e o tamanho do ficheiro de registo. 

#### <a name="open"></a>Abrir
Depois de selecionar um ficheiro de registo, selecione este botão para abrir o **Visualizador**de Registo . Fornece um subconjunto da funcionalidade vista no separador Registos do Centro de Suporte.

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a>Separador de despejos de depurado

Cada linha neste separador fornece detalhes sobre os ficheiros de despejo de depurados que estão disponíveis para exportação. Utilize este separador para exportar ficheiros de despejo de depurados (.dmp) para análises mais aprofundadas. Esta análise utiliza uma ferramenta de depuração como winDbg. 

> [!WARNING]  
> As descargas de depuração podem conter informações confidenciais, incluindo palavras-passe, segredos criptográficos ou dados do utilizador. Apenas recolha despejos de depuração por recomendação do pessoal do Microsoft Support. Os pacotes de dados que contenham despejos de depuração devem ser manuseados cuidadosamente para protegê-los de acesso não autorizado.  

#### <a name="export"></a>Exportar
Guarde uma cópia do ficheiro de despejo de depuração selecionado.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a>Separador WMI

Este separador mostra o conjunto de dados wMI do cliente do Gestor de Configuração que o pacote de dados inclui. 

#### <a name="find"></a>Localizar
Abre o diálogo Find, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia para procurar no conjunto de dados wMI. Suporta personagens wildcard.  

- **Veja:** Escolha se pretende pesquisar dentro do conjunto de dados wMI para uma **classe ou nome de instância**correspondente, **Propriedade**ou **Valor**.  

- **Combine apenas a corda inteira:** Por padrão, o diálogo de encontrar procura por cordas que contenham a corda para a qual está a procurar. Escolha esta caixa de verificação para encontrar apenas cordas que correspondam exatamente à corda que forneceu.  

#### <a name="find-next"></a>Encontre o próximo
Este botão abre a próxima instância da corda que forneceu no diálogo Find dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a>Separador de registo

Utilize o separador **Registry** para visualizar os dados do registo incluídos no pacote de dados e para exportar esses dados para análise mais aprofundada.

#### <a name="export"></a>Exportar
Guarde uma cópia da chave de registo e subchaves que seleciona como ficheiro de registo (.reg).

#### <a name="find"></a>Localizar
Abre o diálogo Find, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia para procurar no conjunto de dados wMI. Suporta personagens wildcard.  

- **Veja:** Escolha se pretende pesquisar dentro do conjunto de dados wMI para uma **classe ou nome de instância**correspondente, **Propriedade**ou **Valor**.  

- **Combine apenas a corda inteira:** Por padrão, o diálogo de encontrar procura por cordas que contenham a corda para a qual está a procurar. Escolha esta caixa de verificação para encontrar apenas cordas que correspondam exatamente à corda que forneceu.  

#### <a name="find-next"></a>Encontre o próximo
Este botão abre a próxima instância da corda que forneceu no diálogo Find dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a>Separador de política

O separador **Política** é utilizado para visualizar dados de política incluídos no pacote de dados. 

#### <a name="find"></a>Localizar
Abre o diálogo Find, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia para procurar no conjunto de dados wMI. Suporta personagens wildcard.  

- **Veja:** Escolha se pretende pesquisar dentro do conjunto de dados wMI para uma **classe ou nome de instância**correspondente, **Propriedade**ou **Valor**.  

- **Combine apenas a corda inteira:** Por padrão, o diálogo de encontrar procura por cordas que contenham a corda para a qual está a procurar. Escolha esta caixa de verificação para encontrar apenas cordas que correspondam exatamente à corda que forneceu.  

#### <a name="find-next"></a>Encontre o próximo
Este botão abre a próxima instância da corda que forneceu no diálogo Find dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Certificado de descodificação
Na caixa de diálogo de **certificado de descodificação,** colhe o valor do certificado serializado para qualquer certificado do cliente. Encontre este valor no registo, nos ficheiros de registo ou no WMI. Selecione **Processo** para ver informações gerais e detalhes no certificado. Esta informação inclui o seu caminho de certificação. Selecione **Exportar** para exportar o certificado como um ficheiro **.cer.**


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a>Separador de certificados

O separador **Certificados** é utilizado para visualizar certificados incluídos no pacote de dados e para exportá-los.

#### <a name="view-certificate"></a>Ver certificado
Exibe informações sobre um certificado selecionado.

#### <a name="export"></a>Exportar
Abre um diálogo **Save As** para guardar uma cópia do certificado que selecionar.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a>Separador de resolução de problemas

Utilize o separador **Deresolução** de Problemas para visualizar ficheiros de registo criados utilizando o separador de resolução de problemas do Centro de Suporte.

#### <a name="view-log"></a>Ver registo
Depois de selecionar uma linha no separador **Resolução** de Problemas, selecione esta opção para visualizar o ficheiro de registo com o Visualizador de Registo.
