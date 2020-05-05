---
title: Como se deslocar para piloto
titleSuffix: Configuration Manager
description: Um guia de como ser implantado para um grupo piloto de Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0e939b51c464215ac1d4feea539ceb5677a01a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723685"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Como se desdobrar para piloto com Desktop Analytics

Um dos benefícios do Desktop Analytics é ajudar a identificar o menor conjunto de dispositivos que fornecem a maior cobertura de fatores. Foca-se nos fatores que são mais importantes para um piloto de atualizações e atualizações do Windows. Certificar-se de que o piloto é mais bem sucedido permite-lhe mover-se mais rapidamente e com confiança para amplas implementações na produção.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identificar dispositivos

O primeiro passo é identificar dispositivos a incluir no piloto. O Desktop Analytics recomenda dispositivos com base nos dados reportados, podendo incluir ou substituir dispositivos nesta lista.

1. Vá ao [portal Desktop Analytics](https://aka.ms/desktopanalytics), e no grupo Gerir planos de **implementação**selecionados .

1. Selecione um plano de implantação.

1. No grupo Preparar o menu do plano de implementação, selecione **Identificar o piloto**.

Verá os dados do Desktop Analytics que mostram o número de dispositivos que recomenda, incluindo para a melhor cobertura. Este algoritmo baseia-se principalmente no uso de aplicações importantes e críticas, e na amplitude de configurações de hardware.

Tome as seguintes ações para a lista de dispositivos recomendados adicionais:

- **Adicione tudo ao piloto**: Adiciona todos os dispositivos recomendados ao grupo piloto
- **Adicionar ao piloto**: Adicione apenas dispositivos individuais
- **Substitua** quaisquer dispositivos específicos do piloto

À medida que adiciona os dispositivos do **recomendado** à lista piloto **incluída,** a cobertura e redundância para os seus ativos críticos e importantes nos aumentos piloto. Um maior despedimento significa que os ativos cobertos têm um número estatisticamente significativo de dispositivos incluídos no seu piloto.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Piloto Global

Também pode tomar decisões em todo o sistema sobre quais as coleções do Gestor de Configuração para incluir ou excluir dos pilotos. No menu principal do Desktop Analytics, no grupo Global Settings, selecione **Global pilot**.

Se ligar várias hierarquias do Gestor de Configuração à mesma instância desktop Analytics, um nome de exibição para a hierarquia prefixa o nome da coleção na configuração piloto global. Este nome é a propriedade **Display Name** na ligação Desktop Analytics na consola 'Gestor de Configuração'.<!-- 4814075 -->

> [!NOTE]
> O suporte para várias hierarquias requer a versão 1910 ou mais tarde do Gestor de Configuração.

- Não inclua coleções que contenham mais de 20% do total de dispositivos matriculados no Desktop Analytics. Se incluir uma grande coleção, o portal apresenta um aviso. Pode incluir várias pequenas coleções sem aviso prévio, mas ainda assim ser cauteloso quanto ao número de dispositivos no seu piloto. <!-- 6079184 -->

- Para obter recomendações piloto precisas para planos de implantação numa hierarquia específica do Gestor de Configuração, apenas incluem coleções dessa hierarquia.

### <a name="example"></a>Exemplo

- Configura a ligação Desktop Analytics no Gestor de Configuração para direcionar a coleção **De Todos os Sistemas.** Esta ação inscreve todos os clientes no serviço.

- Também configura coleções adicionais para sincronizar com desktop Analytics:

  - Todos os clientes do Windows 10 (3.000 dispositivos)

  - Todos os dispositivos de TI (200 dispositivos totais, 150 dos quais executam o Windows 10)

  - Escritório CEO (20 dispositivos)

- Nas definições de **piloto global,** inclui as coleções de **clientes All Windows 10.** Exclui a coleção de escritórios do **CEO.**

- Cria um plano de implementação e seleciona a recolha **de todos os dispositivos DE TI** como o seu grupo **Target**. Pretende este plano de implantação apenas para dispositivos no departamento de TI.

- Os **dispositivos Piloto incluídos** na lista contém o subconjunto de dispositivos que se encontram tanto no seu **grupo Target**: Todos os **dispositivos DE TI** e na lista de *inclusão* do Piloto Global: Todos os clientes do **Windows 10**. 150 dispositivos estão nesta lista, porque apenas 150 dispositivos na coleção **de dispositivos All IT** funcionam com o Windows 10.

- As **listas de Dispositivos Recomendados Adicionais** contêm um conjunto de dispositivos do seu **grupo Target** que fornecem a máxima cobertura e redundância para os seus importantes ativos. Desktop Analytics exclui desta lista quaisquer dispositivos na sua lista global de *exclusão* de pilotos: **ceo office**.

## <a name="address-issues"></a>Questões de endereço

Utilize o portal Desktop Analytics para rever quaisquer problemas reportados com ativos que possam bloquear a sua implementação. Em seguida, aprove, rejeite ou modifique a correção sugerida. Todos os itens devem ser marcados **Pronto** ou **Pronto (com reparação)** antes do início da implantação do piloto.

1. Vá ao [portal Desktop Analytics](https://aka.ms/desktopanalytics), e no grupo Gerir planos de **implementação**selecionados .  

2. Selecione um plano de implantação.  

3. No grupo Preparar o menu do plano de implementação, selecione **Preparar piloto**.  

4. No separador **Apps,** reveja as aplicações que precisam da sua entrada.  

5. Para cada aplicação, selecione o nome da aplicação. No painel de informações, reveja a recomendação e selecione a decisão de atualização. Se escolher **Não revisto** ou **Incapaz,** então o Desktop Analytics não inclui dispositivos com esta aplicação na implementação do piloto. Se escolher **Ready (com reparação)**, utilize as notas de **Reparação** para capturar as ações a tomar para resolver um problema, como *reinstalar* ou *encontrar a versão recomendada do fabricante*.

6. Repita esta revisão para outros ativos.  

Para obter mais informações para ajudar neste processo de revisão, consulte a avaliação da [compatibilidade.](compat-assessment.md)

## <a name="create-software"></a>Criar software

Antes de poder implementar o Windows, crie primeiro os objetos de software no 'Gestor de Configuração'. Para mais informações, consulte a [sequência de tarefas de upgrade](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)do Windows 10 no local .

## <a name="deploy-to-pilot-devices"></a>Implantação para dispositivos piloto

O Gestor de Configuração utiliza os dados do Desktop Analytics para criar coleções para as implementações piloto e de produção. Para garantir que os dispositivos estão saudáveis após cada fase de implementação, utilize o seguinte procedimento para criar uma implementação faseada integrada no Desktop Analytics:

1. Na consola do Gestor de Configuração, vá à Biblioteca de **Software,** expanda a manutenção do **Desktop Analytics**e selecione o nó de Planos de **Implementação.**  

2. Selecione o seu plano de implementação e, em seguida, selecione Detalhes do Plano de **Implementação** na fita.  

3. **Selecione Criar implantação faseada** na fita. Esta ação lança o assistente de implantação faseada create.

    > [!Tip]  
    > Se pretender criar uma sequência de tarefa clássica para apenas a recolha de pilotos, selecione **Deploy** no azulejo do **estado do piloto.** Esta ação lança o Assistente de Software de Implantação. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Introduza um nome para a implementação e selecione a sequência de tarefas a utilizar. Utilize a opção de criar automaticamente uma implementação de **duas fases por defeito**e, em seguida, configurar as seguintes coleções:  

    - **Primeira Recolha**: Encontre e selecione a coleção **Pilot** para este plano de implantação. A convenção padrão de `<deployment plan name> (Pilot)`nomeação para esta coleção é.

    - **Segunda Coleção**: Encontre e selecione a coleção **de produção** para este plano de implantação. A convenção padrão de `<deployment plan name> (Production)`nomeação para esta coleção é.

    > [!Note]  
    > Com a integração do Desktop Analytics, o Gestor de Configuração cria automaticamente coleções piloto e de produção para o plano de implementação. Antes de as poder utilizar, pode levar algum tempo para estas coleções sincronizarem. Para mais informações, consulte [Troubleshoot - Latência](troubleshooting.md#data-latency)de dados .<!-- 4984639 -->
    >
    > Estas coleções estão reservadas para dispositivos de plano de implementação desktop Analytics. Alterações manuais nestas coleções não são suportadas.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Complete o assistente para configurar a implementação faseada. Para mais informações, consulte [Criar implementações faseadas](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Utilize a definição predefinida para **iniciar automaticamente esta fase após um período de diferimento (em dias)**. Devem ser cumpridos os seguintes critérios para a segunda fase:
    >
    > 1. A primeira fase atinge os critérios **percentuais de sucesso** de implantação para o sucesso. Configura esta definição na implementação faseada.
    > 1. Você precisa rever e tomar decisões de upgrade no Desktop Analytics para marcar ativos importantes e críticos como *prontos*. Para mais informações, consulte os ativos da Revisão que precisam de uma decisão de [atualização.](deploy-prod.md#bkmk_review)
    > 1. O Desktop Analytics sincroniza com o Gestor de Configuração que coleta quaisquer dispositivos de produção que satisfaçam os critérios *prontos.*

> [!Important]  
> Estas coleções continuam a sincronizar-se à medida que a sua adesão muda. Por exemplo, se identificar um problema com um ativo e marcá-lo como **Incapaz**, os dispositivos com esse ativo já não cumprem os critérios *prontos.* Estes dispositivos são retirados da coleção de implantação de produção.

## <a name="monitor"></a>Monitorizar

### <a name="configuration-manager-console"></a>Consola do Configuration Manager

Abra o plano de implantação. As decisões de **preparação da atualização -** o azulejo de estado global fornece um resumo do estado do plano de implantação. Este estatuto é para as suas coleções piloto e de produção. Os dispositivos podem cair numa das seguintes categorias:

- **Atualizado**: Os dispositivos atualizaram para a versão alvo do Windows para este plano de implementação

- **Decisão de atualização completa**: Um dos seguintes estados:

  - Dispositivos com ativos notáveis que estão **prontos** ou **prontos com reparação**

  - O estado do dispositivo está **bloqueado,** [**substitua o dispositivo**](about-deployment-plans.md#plan-assets) ou **reinstale o dispositivo**

- **Não revistos**: Dispositivos com ativos notáveis **Não revistos** ou **Revistos em curso**

O estado do dispositivo atualiza-se no **estado piloto** e nas telhas de estado de **produção** com as seguintes ações:

- Faz alterações na avaliação da compatibilidade
- Dispositivos são atualizados para a versão-alvo do Windows
- A sua implantação progride

Também pode utilizar a monitorização de monitorização do Gestor de Configuração da mesma forma que qualquer outra implementação da sequência de tarefas. Para mais informações, consulte [as implementações do Monitor OS](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Portal desktop Analytics

Utilize o [portal Desktop Analytics](https://aka.ms/desktopanalytics) para ver o estado de qualquer plano de implementação. Selecione o plano de implementação e, em seguida, selecione a **visão geral do Plano**.

![Screenshot do plano de implementação visão geral em Desktop Analytics](media/deployment-plan-overview.png)

Selecione o azulejo **Pilot.** Resume o estado atual da implantação do piloto. Este azulejo também apresenta dados para o número de dispositivos não iniciados, em curso, concluídos ou problemas de devolução.

Quaisquer erros de reporte de dispositivos ou outros problemas também estão listados na área de pormenor do Piloto à direita. Para obter detalhes sobre o problema relatado, selecione **Review**. Esta ação altera a visão para a página de estado de **implantação**

A página de estado de **implantação** lista os dispositivos nas seguintes categorias:

- Não iniciadas
- Em curso
- Concluído
- Precisa de atenção - dispositivos
- Precisa de atenção - questões

As categorias **de atenção needs** mostram a mesma informação, mas ordenadas de forma diferente.

Selecione uma listagem específica em qualquer das vistas para obter mais detalhes sobre o problema detetado.

À medida que aborda estes problemas de implementação, o painel de instrumentos continua a mostrar o progresso dos dispositivos. Atualiza à medida que os dispositivos passam de **Necessidades atenção** para **Concluído**.

## <a name="next-steps"></a>Passos seguintes

Deixe o piloto correr durante algum tempo para recolher dados operacionais. Encoraje os utilizadores de dispositivos-piloto a testar aplicações.

Quando o seu destacamento piloto cumprir os seus critérios de sucesso, vá ao próximo artigo para ser implantado para a produção.
> [!div class="nextstepaction"]  
> [Implementar para produção](deploy-prod.md)  
