---
title: Plano para automatizar tarefas
titleSuffix: Configuration Manager
description: Planeie antes de criar sequências de tarefas para automatizar tarefas com o Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723566"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Plano para automatizar tarefas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode criar sequências de tarefas para automatizar tarefas no ambiente do Gestor de Configuração. Estas tarefas vão desde a captura de um SISTEMA num computador de referência até à implementação do SISTEMA para um ou mais computadores de destino. As ações da sequência de tarefas são definidas nos passos individuais da sequência. Quando a sequência de tarefas funciona, executa as ações de cada passo ao nível da linha de comando no contexto do Sistema Local. Este comportamento significa que a sequência de tarefas é totalmente automatizada sem intervenção do utilizador.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a>Passos e ações de sequência de tarefas  

Os passos são os componentes básicos de uma sequência de tarefas. Podem incluir comandos como:

- Configure e capture o Os de um computador de referência
- Instale windows, controladores de hardware, o cliente do Gestor de Configuração e software no computador de destino

As ações do passo definem os comandos de um passo de sequência de tarefas. Existem dois tipos de ações:  

- Uma ação que se define usando uma corda de linha de comando é referida como uma *ação personalizada*  
- Uma ação predefinida pelo Gestor de Configuração é referida como uma *ação incorporada.*  

Uma sequência de tarefas pode fazer qualquer combinação de ações personalizadas e incorporadas.  

Os passos da sequência de tarefas também podem incluir condições que controlam o funcionando do passo. Estes comportamentos incluem parar a sequência de tarefas ou continuar a sequência de tarefas se ocorrer um erro. Um tipo de condição é uma variável de sequência de tarefas. Por exemplo, utilize a variável **SMSTSLastActionRetCode** para testar o estado do passo anterior. Adicione condições a um único passo ou a um grupo de passos.  

A sequência de tarefas processa passos sequencialmente. Esta sequência inclui a ação do passo e quaisquer condições no passo. Quando o Gestor de Configuração começa a processar um passo de sequência de tarefas, não inicia o próximo passo até que a ação anterior esteja completa.

Uma sequência de tarefas é considerada completa quando:

- Todos os seus passos estão completos  
- Um passo falhado faz com que o Gestor de Configuração pare de executar a sequência de tarefas antes de todos os seus passos estarem concluídos.  

Por exemplo, se o passo de uma sequência de tarefas não conseguir localizar uma imagem ou pacote referenciado num ponto de distribuição, a sequência de tarefas inclui uma referência quebrada. O Gestor de Configuração para de executar a sequência de tarefas nesse ponto, a menos que o passo falhado tenha uma condição para continuar quando ocorrer um erro.  

> [!IMPORTANT]  
> Por predefinição, uma sequência de tarefas falhará se falhar um passo ou ação. Se pretender que a sequência de tarefas continue mesmo quando um passo falha, edite a sequência de tarefas, mude para o separador **Opções** e, em seguida, selecione **Continue a error**.  

Para obter mais informações sobre os passos que podem ser adicionados a uma sequência de tarefas, consulte [os passos](../understand/task-sequence-steps.md)da sequência de tarefas .  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a>Grupos de sequência de tarefas  

Pode agrupar vários passos dentro de uma sequência de tarefas. Um grupo de sequência de tarefas é composto por um nome, uma descrição opcional e quaisquer condições opcionais. A sequência de tarefaavalia as condições do grupo como uma unidade antes de continuar com o próximo passo. Grupos de ninhos dentro uns dos outros, ou incluem uma mistura de passos e subgrupos. Os grupos são úteis para combinar diversos passos que partilhem uma condição comum.  

Atribuir um nome a grupos de sequência de tarefas. Não tem que ser único. Também poderá fornecer uma descrição opcional para o grupo de sequência de tarefas.  

> [!IMPORTANT]  
> Por predefinição, um grupo de sequência de tarefas falhará se falhar qualquer passo ou grupo incorporado no grupo. Se pretender que a sequência de tarefas continue quando um grupo ou um grupo incorporado falhar, detete a opção **Continue na** degrau ou grupo.  

A tabela seguinte mostra como funciona a opção **continue na** opção de erro quando se agrupam os passos.  

Neste exemplo, existem dois grupos de sequências de tarefas que incluem três passos de sequência de tarefas cada.  

|Grupo ou passo de sequência de tarefas|Definição Continuar com o erro|  
|---------------------------------|-------------------------------|  
|**Grupo de sequência de tarefas 1**|**Continuar com o erro** selecionado.|  
|Passo de sequência de tarefas 1|**Continuar com o erro** selecionado.|  
|Passo de sequência de tarefas 2|Não definido.|  
|Passo de sequência de tarefas 3|Não definido.|  
|**Grupo de sequência de tarefas 2**|Não definido.|  
|Passo de sequência de tarefas 4|Não definido.|  
|Passo de sequência de tarefas 5|Não definido.|  
|Passo de sequência de tarefas 6|Não definido.|  

- Se a sequência de tarefas falhar, a sequência de tarefas continua com o passo 2 da sequência de tarefas.  

- Se a sequência de tarefas passo 2 falhar, a sequência de tarefas não executa o passo 3 da sequência de tarefas. Como o grupo de sequência de tarefas 1 está configurado para **continuar no erro,** a sequência de tarefas continua a ser o grupo de sequência de tarefas 2. Executa a sequência de tarefas passo 4 próximo.  

- Se a sequência de tarefas passo 4 falhar, não são executados mais passos. A sequência de tarefas falha porque a definição **de continuação na** definição de erro não está configurada para o grupo de sequência de tarefas 2.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicione sequências de tarefas infantis a uma sequência de tarefas

<!--1261338-->

Adicione um novo passo de sequência de tarefas que executa outra sequência de tarefas. Este passo cria uma relação pai-filho entre as sequências de tarefas. A utilização deste passo permite-lhe criar mais sequências de tarefas modulares que pode reutilizar.  

Para mais informações, consulte executar a sequência de [tarefas](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a>Variáveis de sequência de tarefas  

Variáveis de sequência de tarefas são um conjunto de pares de nomes e valores. Eles fornecem configurações de configuração e implementação de SISTEMA para tarefas de configuração de computador, OS e estado do utilizador em um cliente De Configuração Manager. As variáveis de sequência de tarefas fornecem um mecanismo de configuração e personalização dos passos de uma sequência de tarefas.  

Quando executa uma sequência de tarefas, armazena muitas das definições da sequência de tarefas como variáveis ambientais. Pode aceder ou alterar os valores das variáveis de sequência de tarefas incorporadas. Também pode criar novas variáveis de sequência de tarefas para personalizar a forma como uma sequência de tarefas funciona num computador de destino.  

Utilize variáveis de sequência de tarefas para fazer as seguintes ações:  

- Configurar as definições para uma ação de sequência de tarefas  

- Fornecer argumentos de linha de comando para um passo de sequência de tarefas  

- Avaliar uma condição que determina se um passo de sequência de tarefas ou grupo corre  

- Fornecer valores para scripts personalizados usados numa sequência de tarefas  

Por exemplo, tem uma sequência de tarefaque inclui um passo de sequência de tarefas **do Domínio de União ou do Grupo de Trabalho.** Implemente a sequência de tarefas para diferentes coleções, onde a adesão à coleção é determinada pela adesão ao domínio. Especifique uma variável de sequência de tarefas por coleção para o nome de domínio de cada coleção. Em seguida, utilize essa variável de sequência de tarefas para fornecer o nome de domínio apropriado na sequência de tarefas.  

Para mais informações, consulte [Como utilizar variáveis de sequência de tarefas](../understand/using-task-sequence-variables.md).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a>Criar uma sequência de tarefas  

Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. O assistente pode criar sequências de tarefas incorporadas que fazem tarefas específicas ou sequências de tarefas personalizadas que podem fazer muitas tarefas diferentes. O assistente permite criar os seguintes tipos de sequências de tarefas:

- Instale uma imagem de OS existente num computador de destino  

- Construir e capturar uma imagem de OS de um computador de referência  

- Upgrade para o Windows 10 a partir de um pacote de upgrade de OS num computador de destino

- Criar uma sequência de tarefas personalizada que faça uma tarefa personalizada ou implementação de SO especializado  

Para mais informações, consulte [Criar sequências](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence)de tarefas .  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Editar uma sequência de tarefas  

Editar a sequência de tarefautilizando o Editor da Sequência de **Tarefas**. O editor pode efazer as seguintes alterações na sequência de tarefas:  

- Adicione ou remova passos da sequência de tarefas  

- Alterar a ordem dos passos da sequência de tarefas  

- Adicionar ou remover grupos de passos  

- Especifique se a sequência de tarefas continua quando ocorre um erro  

- Adicionar condições aos passos e grupos de uma sequência de tarefas  

> [!IMPORTANT]  
> Se a sequência de tarefas tiver referências não associadas a um objeto como resultado da edição, o editor requer que corrija a referência antes de poder fechar. As possíveis ações incluem:  
>
> - Corrija a referência
> - Eliminar o objeto não referenciado da sequência de tarefas  
> - Desative temporariamente o passo da sequência de tarefas falhada até que a referência quebrada seja corrigida ou removida  

Para obter mais informações sobre como editar sequências de tarefas, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> Implementar uma sequência de tarefas  

Implemente uma sequência de tarefas para computadores de destino que estejam em qualquer coleção do Gestor de Configuração. Utilize a coleção **incorporada de Todos os Computadores Desconhecidos** para implantar sistemas operativos em computadores desconhecidos. Não é possível implementar uma sequência de tarefas nas coleções dos utilizadores.  

> [!IMPORTANT]  
> Não implemente sequências de tarefas que instalam sistemas operativos em coleções inadequadas. Certifique-se de que a recolha para a qual implementa a sequência de tarefas inclui apenas os computadores onde pretende instalar o SISTEMA. Para ajudar a prevenir implementações de SO indesejadas, configure as definições para implementações de alto risco. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Cada computador de destino que recebe a sequência de tarefas executa a sequência de tarefas de acordo com as definições especificadas na implementação. As sequências de tarefas em si não contêm ficheiros ou programas associados. Quaisquer ficheiros que uma sequência de tarefas referências já devem estar presentes no computador de destino ou armazenados num ponto de distribuição a que os clientes possam aceder.

> [!NOTE]  
> A sequência de tarefas instala pacotes referenciados por programas, mesmo que o programa ou pacote já esteja instalado no computador de destino.
>
> Se a sequência de tarefas instalar uma aplicação, a aplicação instala-se apenas se as regras de requisito saem cumpridas e a aplicação ainda não estiver instalada, com base no método de deteção especificado para a aplicação.  

O cliente do Gestor de Configuração executa uma implementação de sequência de tarefas quando descarrega a política do cliente. Para desencadear esta ação em vez de esperar pelo próximo ciclo de sondagens, consulte [Iniciar a recuperação de políticas para um cliente do Gestor](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)de Configuração .  

Quando implementa sequências de tarefas para dispositivos Incorporados do Windows que estão ativados com um filtro de escrita, pode especificar se desativa o filtro de escrita no dispositivo durante a implementação e, em seguida, reiniciar o dispositivo após a implementação. Se o filtro de escrita não estiver desativado, a sequência de tarefas é implantada para uma sobreposição temporária e não estará disponível quando o dispositivo recomeçar.  

> [!NOTE]  
> Quando implementar uma sequência de tarefas para um dispositivo Incorporado no Windows, certifique-se de que o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada. Isto permite-lhe gerir quando o filtro de escrita está desativado e ativado, e quando o dispositivo reinicia.  
>
> Se os clientes descarregarem sequências de tarefas fora de uma janela de manutenção, a sequência de tarefas é descarregada duas vezes. Neste cenário, o cliente descarrega a sequência de tarefas, desativa o filtro de escrita, reinicia o computador e, em seguida, descarrega novamente a sequência de tarefas. Este comportamento deve-se ao facto de a sequência de tarefas ter sido originalmente descarregada para a sobreposição temporária, que é desmarcada quando o dispositivo reinicia.  

Para obter mais informações sobre como implementar sequências de tarefas, consulte a [sequência de tarefas .](../deploy-use/deploy-a-task-sequence.md)  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a>Exportação e importação

O Gestor de Configuração permite-lhe exportar e importar sequências de tarefas. Quando exporta uma sequência de tarefas, pode incluir os objetos referenciados pela sequência de tarefas.

Para obter mais informações, consulte as sequências de [tarefas de exportação e importação](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Executar uma sequência de tarefas  

As sequências de tarefas são sempre executadas utilizando a conta do Sistema Local. Quando a sequência de tarefas é executado, o cliente do Gestor de Configuração verifica primeiro quaisquer pacotes referenciados antes de iniciar os passos da sequência de tarefas. Se não conseguir validar ou descarregar um pacote referenciado, a sequência de tarefas devolve um erro para o passo da sequência de tarefas associada.  

> [!Note]  
> A linha de **comando de** execução da sequência de tarefas fornece a capacidade de executar um comando como uma conta diferente.  

Se configurar uma sequência de tarefas para descarregar e executar, o cliente do Gestor de Configuração descarrega todos os conteúdos dependentes para a sua cache. Se o tamanho da cache do cliente for demasiado pequeno ou se o conteúdo não puder ser encontrado, a sequência de tarefas falha. O cliente gera uma mensagem de estado.

Também pode especificar que o cliente descarrega o conteúdo apenas quando é necessário. Para fazer esta ação, selecione **o conteúdo de descarregamento localmente quando necessário, executando** a sequência de tarefas na implementação da sequência de tarefas. Outra opção é **executar o programa a partir do ponto de distribuição**. Com esta opção, o cliente instala os ficheiros diretamente do ponto de distribuição sem os transferir primeiro para a cache.

Quando configura a implementação da sequência de tarefas como **disponível,** se o cliente não conseguir localizar conteúdo dependente para a sequência de tarefas, envia imediatamente um erro. Para uma implementação **necessária,** o cliente do Gestor de Configuração aguarda nesta situação. Tenta descarregar o conteúdo até ao prazo, caso o conteúdo ainda não seja replicado para um local de conteúdo a que o cliente possa aceder.  

Quando uma sequência de tarefas completa com sucesso ou falha, o Gestor de Configuração regista este estado no histórico do cliente.

Uma vez que uma sequência de tarefas começa num computador, não pode cancelar ou detê-la.  

> [!IMPORTANT]  
> Se um passo de sequência de tarefas exigir que o computador reinicie, o cliente deve ser capaz de iniciar uma partição de disco formatado. Caso contrário, a sequência de tarefas falha independentemente de qualquer manipulação de erro que especifique na sequência de tarefas.  

Quando um objeto dependente de uma sequência de tarefas é atualizado para uma versão mais recente, qualquer sequência de tarefaque refira o pacote é automaticamente atualizada. Refere a versão mais recente, não importa quantas atualizações tenha implementado.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a>Utilize janelas de manutenção

Pode especificar quando a sequência de tarefas pode ser executada definindo uma janela de manutenção para a recolha do dispositivo. Configura janelas de manutenção com data de início, hora de início e de chegada e um padrão de recorrência. Quando definir o horário da janela de manutenção, pode especificar que a janela de manutenção se aplica apenas às sequências de tarefas. Para mais informações, consulte [Como utilizar as janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
> Quando configura uma janela de manutenção para executar uma sequência de tarefas, uma vez as sequências de tarefas iniciadas, continuam a ser executadas mesmo que a janela de manutenção se feche.  

Se um dispositivo tiver mais do que uma janela de manutenção aplicada, o cliente pode ignorar uma janela de manutenção de **todas as implementações.** A partir da versão 1810, utilize a seguinte definição do cliente para controlar este comportamento: Ativar a **instalação de atualizações de software na janela de manutenção "Todas as implementações" quando estiver disponível**a janela de manutenção "Software Update". Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a>Sequências de tarefas e a conta de acesso à rede  

> [!Important]  
> Alguns cenários de implementação de SO não requerem a utilização da conta de acesso à rede. Para mais informações, consulte [O HTTP Melhorado](#enhanced-http).

Embora as sequências de tarefas decorram apenas no contexto da conta do Sistema Local, poderá ser necessário configurar a conta de acesso à [rede](../../core/plan-design/hierarchy/accounts.md#network-access-account) nas seguintes circunstâncias:  

- Se a sequência de tarefas tentar aceder ao conteúdo do Gestor de Configuração nos pontos de distribuição. Configure corretamente a conta de acesso à rede, ou a sequência de tarefas falhará.

- Quando utiliza uma imagem de arranque para iniciar uma implementação de SO. Neste caso, o Gestor de Configuração utiliza o ambiente Windows PE, que não é um SISTEMA completo. O ambiente Windows PE utiliza um nome aleatório gerado automaticamente que não é membro de nenhum domínio. Se não configurar corretamente a conta de acesso à rede, o computador não pode aceder ao conteúdo necessário para a sequência de tarefas.  

> [!NOTE]  
> A conta de acesso à rede nunca é utilizada como contexto de segurança para executar programas, instalar aplicações, instalar atualizações ou executar sequências de tarefas. A conta de acesso à rede só é utilizada para aceder aos recursos associados na rede.  

Para obter mais informações sobre a conta de acesso à rede, consulte a conta de acesso à [rede.](../../core/plan-design/hierarchy/accounts.md#network-access-account)  

### <a name="enhanced-http"></a>HTTP melhorado
<!--1358278-->

Quando ativa o **Enhanced HTTP,** os seguintes cenários não requerem uma conta de acesso à rede para descarregar conteúdo a partir de um ponto de distribuição:

- Sequências de tarefas que saem dos meios de arranque ou PXE  
- Sequências de tarefas que correm do Centro de Software  

Estas sequências de tarefapodem ser para implementação de OS ou personalizadas. Também é suportado para computadores de grupo de trabalho.

Para mais informações, consulte [O HTTP Melhorado](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> Os seguintes cenários de implantação do OS ainda requerem a utilização de uma conta de acesso à rede:
>  
> - Opção [de implementação](../deploy-use/deploy-a-task-sequence.md)da sequência de tarefas , **Aceda diretamente ao conteúdo a partir de um ponto de distribuição quando necessário pela sequência de tarefas em execução**
> - Opção de passo [da Loja do Estado de Pedido,](../understand/task-sequence-steps.md#BKMK_RequestStateStore) Se a conta de computador não ligar a uma loja **estatal, utilize a conta de acesso à rede**
> - Ao ligar-se a um domínio não confiável ou através de florestas de Diretório Ativo
> - A opção [Desviação de Imagem Os Apply,](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) **Aceder diretamente ao conteúdo a partir do ponto de distribuição**
> - A sequência de [tarefas avançou](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) a definição para **executar outro programa primeiro**
> - [Multicast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a>Criar meios de comunicação

Pode escrever sequências de tarefas e seus ficheiros e dependências relacionados a vários tipos de meios de comunicação. O Gestor de Configuração suporta meios amovíveis, como um DVD ou uma pen USB para capturar, autónomo e suporte sinuoso. Os meios de comunicação pré-encenados utilizam um ficheiro de imagem do Windows (WIM).  

Quando criar meios de comunicação, especifique uma palavra-passe para controlar o acesso. Em seguida, uma pessoa deve introduzir a palavra-passe no computador-alvo para executar a sequência de tarefas.  

Quando executa uma sequência de tarefas a partir de meios de comunicação, a arquitetura especificada do processador dos meios de comunicação não é reconhecida. Se a arquitetura especificada não corresponder ao computador-alvo, a sequência de tarefas ainda tenta ser executada. Se a arquitetura dos meios de comunicação não corresponder à arquitetura do computador-alvo, a sequência de tarefas falha.  

Para mais informações, consulte Criar meios de sequência de [tarefas](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Tipos de suporte

O Gestor de Configuração suporta os seguintes tipos de meios:  

#### <a name="capture-media"></a>Capturar meios de comunicação

Este meio de comunicação capta uma imagem de OS que configura e cria fora da infraestrutura do Gestor de Configuração. O suporte de dados de captura pode conter programas personalizados que podem ser executados antes da execução de uma sequência de tarefas. O programa personalizado pode interagir com o ambiente de trabalho, solicitar ao utilizador valores de entrada ou criar variáveis a utilizar pela sequência de tarefas.  

Para mais informações, consulte [Criar meios de captura.](../deploy-use/create-capture-media.md)  

#### <a name="stand-alone-media"></a>Meios de comunicação autónomos

O suporte de dados autónomo contém a sequência de tarefas e todos os objetos associados necessários à execução da sequência de tarefas. As sequências de tarefas autónomas dos meios de comunicação podem ser executadas quando o Gestor de Configuração tem uma conectividade limitada ou sem conectividade com a rede. Executar meios de comunicação autónomos das seguintes formas:  

- Se o computador de destino não for iniciado, a imagem do Windows PE associada à sequência de tarefas é utilizada a partir dos meios de comunicação autónomos e a sequência de tarefas começa.  

- Inicie manualmente os meios de comunicação autónomos. Se um utilizador for inscrito no computador, pode iniciar a sequência de tarefas a partir do meio de comunicação.  

> [!IMPORTANT]  
> Os passos de uma sequência de tarefas autónomas dos meios de comunicação devem ser executados sem obter quaisquer dados da rede. Caso contrário, o passo da sequência de tarefas que tenta recuperar os dados falha. Por exemplo, um passo de sequência de tarefaque requer um ponto de distribuição para obter uma falha de um pacote. Se os meios de comunicação autónomos contiverem o pacote necessário, o passo da sequência de tarefas é bem sucedido.  

Para mais informações, consulte [Criar meios de comunicação autónomos.](../deploy-use/create-stand-alone-media.md)  

#### <a name="bootable-media"></a>Suporte de dados de arranque

Os meios de arranque contêm os ficheiros necessários para iniciar um computador de destino para que possa ligar-se à infraestrutura do Gestor de Configuração. Em seguida, determina quais as sequências de tarefas a executar com base nos seus membros de recolha. Estes meios não incluem a sequência de tarefas ou objetos dependentes. Em vez disso, o cliente descarrega o conteúdo pela rede. Este método é útil para novos computadores ou implementações de metal nu, quando nenhum SISTEMA está no computador de destino.  

Para mais informações, consulte [Criar meios de sapateado.](../deploy-use/create-bootable-media.md)  

#### <a name="prestaged-media"></a>Suportes de dados de pré-configuração

Os meios de comunicação pré-encenados implementam uma imagem de SO para um computador de destino que não é provisionado. Os meios de comunicação pré-encenados são armazenados como um ficheiro de imagem do Windows (WIM). Este ficheiro pode ser instalado num computador de metal nu pelo fabricante ou num centro de preparação empresarial. Um benefício dos meios de comunicação pré-encenados é que estes locais não requerem uma ligação ao ambiente do seu Gestor de Configuração.  

Para mais informações, consulte [Criar meios pré-encenados.](../deploy-use/create-prestaged-media.md)  

## <a name="next-steps"></a>Passos seguintes

- [Segurança e privacidade para implementação do SO](security-and-privacy-for-operating-system-deployment.md)

- [Preparar funções do sistema de sites para implementações de SO](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
