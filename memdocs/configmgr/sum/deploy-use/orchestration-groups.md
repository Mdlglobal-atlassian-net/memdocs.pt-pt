---
title: Grupos de Orquestração
titleSuffix: Configuration Manager
description: Crie grupos de orquestração e implante atualizações para eles.
ms.date: 04/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9a307df23900abb985535b2ab59a5ff172cafb7
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254916"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Grupos de orquestração em Gestor de Configuração
<!--3098816-->
*Aplica-se a: Gestor de Configuração (ramo atual)*

A partir da versão De Configuração Manager 2002, pode criar grupos de orquestração. Crie um grupo de orquestração para controlar melhor a implementação de atualizações de software para dispositivos. Muitos administradores de servidores precisam de gerir cuidadosamente as atualizações para cargas de trabalho específicas e automatizar comportamentos pelo meio.

Um grupo de orquestração dá-lhe a flexibilidade para atualizar dispositivos com base numa percentagem, num número específico ou numa ordem explícita. Também pode executar um script PowerShell antes e depois de os dispositivos executarem a implementação da atualização.

Membros de um grupo de orquestração podem ser qualquer cliente do Gestor de Configuração, não apenas servidores. As regras do grupo de orquestração aplicam-se aos dispositivos para todas as implementações de atualizações de software para qualquer coleção que contenha um membro do grupo de orquestração. Outros comportamentos de implantação ainda se aplicam. Por exemplo, janelas de manutenção e horários de implantação.

> [!NOTE]
> Nesta versão do Gestor de Configuração, os grupos de orquestração são uma funcionalidade de pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../core/servers/manage/pre-release-features.md).  
>
> A funcionalidade Grupos de **Orquestração** é a evolução da funcionalidade [Grupos](service-a-server-group.md) de Servidores. Um grupo de orquestração é um objeto no Gestor de Configuração.

## <a name="orchestration-group-usage-example"></a>Exemplo de utilização do grupo de orquestração

- Como o software atualiza o administrador, gere todas as atualizações para a sua organização.
- Tem uma grande coleção para todos os servidores e uma grande coleção para todos os clientes. Implementa todas as atualizações destas coleções.
- Os administradores da SQL querem controlar todo o software instalado nos servidores SQL. Querem remendar cinco servidores numa ordem específica. O seu processo atual é parar manualmente serviços específicos antes de instalar atualizações e, em seguida, reiniciar os serviços posteriormente.
- Cria-se um grupo de orquestração e adiciona-se todos os cinco servidores SQL. Também adiciona pré-e post-scripts, utilizando os scripts PowerShell fornecidos pelos administradores SQL.
- Durante o próximo ciclo de atualização, cria e implementa as atualizações de software normalmente para a grande coleção de servidores. Os administradores da SQL executam a implantação, e o grupo de orquestração automatiza a ordem e os serviços.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="site-server-and-permission-prerequisites"></a>Servidor do site e pré-requisitos de permissão
- Para ver todos os grupos de orquestração e atualizações para esses grupos, a sua conta tem de ser um **Administrador Completo.**
   - A administração baseada em papéis para grupos de orquestração não está disponível atualmente.
- Ativar a função **Grupos de Orquestração.** Para mais informações, consulte [Ativar funcionalidades opcionais](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - Quando ativa **os Grupos de Orquestração,** o site desativa a funcionalidade **Grupos de Servidores.** Este comportamento evita quaisquer conflitos entre as duas características.

### <a name="client-prerequisites"></a>Pré-requisitos do cliente

- Atualize os dispositivos-alvo para a versão mais recente do cliente do Gestor de Configuração.
- Os membros de um grupo de orquestração devem ser designados para o mesmo local.
- Os dispositivos não podem estar em mais do que um grupo de orquestração.
   - Os dispositivos já num grupo de orquestração não estarão disponíveis para selecionar ao adicionar novos membros.


## <a name="limitations"></a>Limitações

- Pode ter até 1000 membros do grupo de orquestração.
- Grupos de orquestração não funcionam em modo de interoperabilidade. Para mais informações, consulte [Interoperabilidade entre diferentes versões do Gestor de Configuração](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Se as atualizações forem iniciadas pelos utilizadores do Centro de Software, a orquestração será ignorada. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Os grupos de servidores são automaticamente atualizados para grupos de orquestração

A funcionalidade Grupos de **Orquestração** é a evolução da funcionalidade [Grupos](service-a-server-group.md) de Servidores. Quando instala a versão do Gestor de Configuração 2002 ou posteriormente e tem grupos de servidores ativados, os grupos de servidores são automaticamente transferidos para grupos de orquestração.

## <a name="create-an-orchestration-group"></a>Criar um grupo de orquestração

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance** e selecione o nó do Grupo de **Orquestração.**

1. Na fita, selecione **Create Orchestration Group** para abrir o Assistente do **Grupo de Orquestração Create**.

1. Na página **Geral,** dê ao seu grupo de orquestração um **Nome** e opcionalmente uma **Descrição**. Especifique os seus valores para os seguintes itens:
   - Intervalo do **Grupo de Orquestração (em minutos)**: Prazo para todos os membros do grupo completarem a instalação da atualização.
   - Tempo limite para membro do **Grupo de Orquestração (em minutos)**: Prazo para um único dispositivo no grupo completar a instalação da atualização.

1. Na página de **Seleção de Membros,** primeiro especifique o **código do Site**. Em seguida, **selecione Adicionar** para adicionar recursos do dispositivo como membros deste grupo de orquestração. **Procure** por dispositivos pelo nome e, em seguida, **adicione-os.** Também pode filtrar a sua pesquisa para uma única coleção utilizando **o Search in Collection**.  Selecione **OK** quando terminar a adição de dispositivos à lista de recursos selecionados.
   - Ao selecionar recursos para o grupo, apenas são mostrados clientes válidos. São feitas verificações para verificar o código do site, para a instalação do cliente e para que os recursos não sejam duplicados.

1. Na página **'Seleção** de Regras', selecione uma das seguintes opções:

   - **Permita que uma percentagem das máquinas seja atualizada ao mesmo tempo,** em seguida, selecione ou introduza um número para esta percentagem. Utilize esta definição para permitir uma flexibilidade futura do tamanho do grupo de orquestração. Por exemplo, o seu grupo de orquestração contém 50 dispositivos, e você define este valor para 10. Durante uma implementação de atualização de software, o Gestor de Configuração permite que cinco dispositivos executem simultaneamente a implementação. Se aumentar mais tarde o tamanho do grupo de orquestração para 100 dispositivos, então 10 dispositivos atualização de uma só vez.

   - Deixe que **algumas das máquinas sejam atualizadas ao mesmo tempo,** em seguida, selecione ou introduza um número para esta contagem específica. Utilize esta definição para limitar sempre a um número específico de dispositivos, qualquer que seja o tamanho total do grupo de orquestração.

   - **Especifique a sequência de manutenção**e, em seguida, separe os recursos selecionados na ordem adequada. Utilize esta definição para definir explicitamente a ordem na qual os dispositivos executam a implementação da atualização do software.

1. Na página **Pré-Script,** introduza um script PowerShell para ser executado em cada dispositivo *antes* da implementação ser executada. O script deve devolver um valor de `0` sucesso, ou `3010` para o sucesso com o reinício.

1. Na página **Post-Script,** introduza um script PowerShell para ser executado em cada dispositivo *após* a execução. O comportamento é o mesmo que o PreScript.

1. Conclua o assistente.

> [!WARNING]
> Certifique-se de que os pré-scripts e pós-scripts são testados antes de os utilizar em grupos de orquestração. Os pré-scripts e pós-scripts não têm tempo e vão funcionar até que o intervalo do grupo de orquestração seja atingido.

## <a name="view-orchestration-groups-and-members"></a>Ver grupos de orquestração e membros

A partir do espaço de trabalho **Assets and Compliance,** selecione o nó do **Grupo de Orquestração.** Para ver os membros, selecione um grupo de orquestração e selecione **Show Members** na fita. Para obter mais informações sobre as colunas disponíveis para os nós, consulte [grupos de orquestração monitor e membros](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Editar ou eliminar um grupo de orquestração

Para eliminar o grupo de orquestração, selecione-o e, em seguida, clique em **Apagar** na fita ou no menu do clique direito. Para editar um grupo de orquestração, selecione-o e, em seguida, clique em **Propriedades** na fita ou no menu de clique direito. Alterar as definições dos seguintes separadores:

   - **Geral:** 
      - **Nome**: O nome do seu grupo de orquestração
      - **Descrição**: Descrição do grupo de orquestração (opcional)
      - Intervalo do **Grupo de Orquestração (em minutos)**: Prazo para todos os membros do grupo completarem a instalação da atualização.
      - Tempo limite para membro do **Grupo de Orquestração (em minutos)**: Prazo para um único dispositivo no grupo completar a instalação da atualização.

  - **Seleção dos Membros:**
     - **Código do Site**: Código do site para o grupo de orquestração.
     - **Membros**: Clique em **Adicionar** para selecionar dispositivos adicionais para o grupo de orquestração. Clique em **Remover** para remover o dispositivo selecionado.

   - **Seleção de Regras:**
      - **Permita que uma percentagem das máquinas seja atualizada ao mesmo tempo,** em seguida, selecione ou introduza um número para esta percentagem. Utilize esta definição para permitir uma flexibilidade futura do tamanho do grupo de orquestração. Por exemplo, o seu grupo de orquestração contém 50 dispositivos, e você define este valor para 10. Durante uma implementação de atualização de software, o Gestor de Configuração permite que cinco dispositivos executem simultaneamente a implementação. Se aumentar mais tarde o tamanho do grupo de orquestração para 100 dispositivos, então 10 dispositivos atualização de uma só vez.
      - Deixe que **algumas das máquinas sejam atualizadas ao mesmo tempo,** em seguida, selecione ou introduza um número para esta contagem específica. Utilize esta definição para limitar sempre a um número específico de dispositivos, qualquer que seja o tamanho total do grupo de orquestração.
      - **Especifique a sequência de manutenção**: Separe os recursos selecionados à ordem adequada. Utilize esta definição para definir explicitamente a ordem na qual os dispositivos executam a implementação da atualização do software.

   - **Pré-script**: 
       - Introduza um script PowerShell que seja executado em cada dispositivo *antes* da implementação ser executado. O script deve devolver um valor de `0` sucesso, ou `3010` para o sucesso com o reinício.
       
   - **Pós-Script:**
      - Introduza um script PowerShell para ser executado em cada dispositivo *após* a execução. O script deve devolver um valor de `0` sucesso, ou `3010` para o sucesso com o reinício.
   > [!WARNING]
   > Certifique-se de que os pré-scripts e pós-scripts são testados antes de os utilizar em grupos de orquestração. Os pré-scripts e pós-scripts não têm tempo e vão funcionar até que o intervalo do grupo de orquestração seja atingido.


## <a name="start-orchestration"></a>Iniciar a orquestração

1. [Implemente atualizações](deploy-software-updates.md) de software para uma coleção que contenha os membros do grupo de orquestração.

1. A orquestração começa quando qualquer cliente do grupo tenta instalar qualquer atualização de software no prazo ou durante uma janela de manutenção. Começa para todo o grupo, e garante que os dispositivos atualizam seguindo as regras do grupo de orquestração.
1. Pode iniciar a orquestração manualmente selecionando-a a partir do nó do **Grupo de Orquestração** e, em seguida, escolhendo iniciar **orquestração** a partir da fita ou do menu de clique direito.
1. Se um grupo de orquestração estiver em estado *falhado:*
   1. Determinar por que a orquestração falhou e resolver quaisquer problemas.
   1. [Redefinir o estado de orquestração para membros do grupo.](#bkmk_reset)
   1. A partir do nó do **Grupo de Orquestração,** clique no botão **Iniciar Orquestração** para reiniciar a orquestração.
   [![Iniciar orquestração](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Os grupos de orquestração aplicam-se apenas a implementações de atualizações de software. Não se aplicam a outros destacamentos.
> - Pode clicar num membro do Grupo de Orquestração e selecionar Membro do Grupo de **Orquestração de Reset**. Isto permite-lhe refazer a orquestração.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a>Monitorize grupos de orquestração

A partir do espaço de trabalho **Assets and Compliance,** selecione o nó do **Grupo de Orquestração.** Adicione qualquer uma das seguintes colunas para obter informações sobre os grupos:

- **Nome da Orquestração**: O nome do seu grupo de orquestração.
- **Código do Site**: Código do site para o grupo.
- **Tipo de orquestração:** é um dos seguintes tipos:
   - Número
   - Percentagem
   - Sequence

- **Valor da Orquestração**: Quantos membros ou a percentagem de membros que podem obter um bloqueio simultaneamente. **O valor da orquestração** só é povoado quando o **Tipo de Orquestração** é *número* ou *percentagem*.  
- **Estado de Orquestração**: Em curso durante a orquestração. Inativo quando não está em andamento.
- Hora de **início da orquestração**: Data e hora que a orquestração começou.
- **Número de sequência atual**: Indica para que membro da orquestração do grupo está ativo. Este número corresponde ao Número de **Sequência** para o membro.  
- **Tempo de tempo de orquestração (em minutos)**: Valor do intervalo do **Grupo de Orquestração (em minutos)** definido na página **geral** ao criar o grupo, ou no separador **Geral** ao editar o grupo.
- Timeout membro do **Grupo de Orquestração (em minutos)**: Tempo de tempo de membro do Grupo de **Orquestração (em minutos)** definido na página **geral** ao criar o grupo, ou no separador **Geral** ao editar o grupo.
- **ID do Grupo de Orquestração**: ID do grupo, O ID é utilizado em registos e na base de dados.
- **ID exclusivo do Grupo de Orquestração**: ID único do grupo, o ID exclusivo é usado em registos e na base de dados.

## <a name="monitor-orchestration-group-members"></a>Monitor membros do grupo de orquestração

No nó do **Grupo de Orquestração,** selecione um grupo de orquestração. Na fita, selecione **Show Members**. Pode ver os membros do grupo e o seu estatuto de orquestração. Adicione qualquer uma das seguintes colunas para obter informações sobre os membros:

- **Nome**: Nome do dispositivo do membro do grupo de orquestração
- **Estado atual**: Dá-lhe o estado do dispositivo membro.
   - **Em progresso** durante a orquestração.
   - **Espera**: Indica que o cliente está à espera no cadeado para a sua vez de instalar atualizações.
   - **Idle** quando a orquestração está completa ou não está a funcionar.
- **Código do Estado**: Pode clicar no membro do Grupo de Orquestração e selecionar Membro do Grupo de **Orquestração de Reset**. Este reset permite-lhe reexecutar a orquestração. Os Estados incluem: 
   - Ocioso
   - Esperando, o dispositivo está esperando a sua vez
   - Em curso, instalação de uma atualização
   - Falhou
   - Reiniciar pendente
- **Tempo adquirido**lock : As fechaduras são solicitadas pelo cliente com base na sua política. Assim que o cliente adquire uma fechadura, a orquestração é ativada nele.  
-**Última hora:** Tempo o membro reportou pela última vez um estado.
- **Número de sequência**: A localização do cliente na fila para instalar atualizações.
- **Código do site**: O código do site para o membro.
- **Atividade do Cliente**: Diz-lhe se o cliente está ativo ou inativo.
- **Utilizador Primário(s)**: Quais os utilizadores que são primários para o dispositivo.
- **Tipo cliente**: Que tipo de dispositivo é o cliente.
- **Atualmente registado no Utilizador**: Qual o utilizador que está atualmente ligado ao dispositivo.
- **OG ID**: ID do grupo de orquestração a que o membro pertence.
- **OG Unique ID**: Identificação única do grupo de orquestração a que o membro pertence.
- **ID de recursos**: Identificação de recursos do dispositivo.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a>Redefinir o estado de orquestração para um membro do grupo

Se quiser reexecutar a orquestração num membro do grupo, pode limpar o seu estado como *Complete* ou *Failed*. Para limpar o estado, clique à direita no membro do Grupo de Orquestração e selecione **Reset Orchestration Group Member**. Também pode clicar no **Reset Orchestration Group Member** a partir da fita. Antes de redefinir o estado, deve verificar o cliente para ver por que falhou e corrigir quaisquer problemas encontrados.
   [![Redefinir membro do Grupo de Orquestração](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Ficheiros de registo

Utilize os seguintes ficheiros de registo no servidor do site para ajudar a monitorizar e resolver problemas:

### <a name="site-server"></a>Servidor do site

- **Policypv.log**: mostra que o site tem como alvo o grupo de orquestração para os clientes.
- **SMS_OrchestrationGroup.log:** mostra os comportamentos do grupo de orquestração.

### <a name="client"></a>Cliente

- **ManutençãoCoordenador.log**: Mostra a aquisição do bloqueio, a instalação da atualização, pré e pós-scripts e o processo de libertação do bloqueio.
- **ActualizaçãoDeployment.log**: Mostra o processo de instalação da atualização.
- **PolicyAgent.log**: Verifica se o cliente está num grupo de orquestração.

## <a name="next-steps"></a>Próximos passos

[Deploy software updates](deploy-software-updates.md)