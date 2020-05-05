---
title: Gerir sequências de tarefas
titleSuffix: Configuration Manager
description: Crie, edite, implante, importe e exporte sequências de tarefas para geri-las e automatizar tarefas no seu ambiente.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b38b0c8f28645fa0aae66058b0c93bd8beffc470
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078486"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Gerir sequências de tarefas para automatizar tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize sequências de tarefas para automatizar passos no ambiente do Gestor de Configuração. Estes passos podem implantar uma imagem de OS para um computador de destino, construir e capturar uma imagem de OS a partir de um conjunto de ficheiros de instalação de SE, e capturar e restaurar informações do estado do utilizador. As sequências de tarefas estão localizadas na consola do Gestor de Configuração. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.** O nó de sequências de **tarefas,** incluindo subpastas que cria, é replicado em toda a hierarquia do Gestor de Configuração. Para obter informações de planeamento, consulte [considerações de Planeamento para automatização de tarefas.](../plan-design/planning-considerations-for-automating-tasks.md)  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>Criar

Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

- [Sequência de tarefas para instalar um SISTEMA:](create-a-task-sequence-to-install-an-operating-system.md)Criar os passos para instalar um SISTEMA. Também inclui opções para migrar dados dos utilizadores, incluir atualizações de software e instalar aplicações.

- [Sequência de tarefas para atualizar um OS](create-a-task-sequence-to-upgrade-an-operating-system.md): Criar os passos para atualizar um SISTEMA. Também inclui opções para incluir atualizações de software e instalar aplicações.

- [Sequência de tarefas para capturar um SISTEMA:](create-a-task-sequence-to-capture-an-operating-system.md)Criar os passos para construir e capturar um SISTEMA a partir de um computador de referência. Pode incluir atualizações de software e instalar aplicações no computador de referência antes de capturar a imagem.

- [Sequência de tarefas para capturar e restaurar](create-a-task-sequence-to-capture-and-restore-user-state.md)o estado do utilizador : Adicione passos para uma sequência de tarefas existente para capturar e restaurar os dados do estado do utilizador.

- [Sequência de tarefas personalizada](create-a-custom-task-sequence.md): Este tipo não adiciona quaisquer passos à sequência de tarefas. Depois de criar esta sequência de tarefas, edite-a e adicione passos.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>Editar  

Modificar uma sequência de tarefas adicionando ou removendo passos, adicionando ou removendo grupos, ou alterando a ordem dos passos. Para mais informações, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md).

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a>Propriedades do Centro de Software

Utilize o seguinte procedimento para configurar os detalhes para a sequência de tarefas apresentada no Centro de Software. Estes detalhes são apenas para informação.  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**  

2. Selecione a sequência de tarefas para editar e selecione **Propriedades**.  

3. No separador **Geral,** estão disponíveis as seguintes definições para O Centro de Software:  

    - **Reinício requerido**: Informe o utilizador se é necessário reiniciar durante a instalação.  

    - **Tamanho do download (MB)**: Especifica quantos megabytes são apresentados no Centro de Software para a sequência de tarefas.  

    - **Tempo estimado de execução (minutos)**: Especifica o tempo estimado de execução em minutos que é apresentado no Centro de Software para a sequência de tarefas.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>Configurações avançadas

Utilize o seguinte procedimento para configurar o comportamento da sequência de tarefas no cliente do Gestor de Configuração.  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**  

2. Selecione a sequência de tarefas para editar e selecione **Propriedades**.  

3. No separador **Advanced,** estão disponíveis as seguintes definições:  

    - **Executar outro programa primeiro**: Selecione esta opção para executar um programa em outro pacote antes da sequência de tarefas ser executada. Por predefinição, esta caixa de verificação está desmarcada. Não precisa de implementar separadamente o programa que especifica para executar primeiro.  

        > [!IMPORTANT]
        > Esta definição aplica-se apenas às sequências de tarefas que funcionam em todo o Sistema Operativo. Se iniciar a sequência de tarefautilizando pXE ou boot media, o Gestor de Configuração ignora esta definição.  

        - **Pacote**: Navegue para o pacote que contém o programa a executar antes desta sequência de tarefas.  

        - **Programa**: Selecione o programa a executar antes desta sequência de tarefas.  

        > [!NOTE]  
        > Se o programa selecionado não funcionar num cliente, a sequência de tarefas não funciona. Se o programa selecionado funcionar com sucesso, não volta a funcionar, mesmo que a sequência de tarefas seja reexecutada no mesmo cliente.  

    - **Suprimir notificações**de sequência de tarefas : Selecione esta opção para ocultar o **Novo Software está disponível** notificação de torradas. Ainda vê o novo ícone de **software** do Software Center na área de notificação. Por defeito, esta opção está desativada.  

    - **Desative esta sequência de tarefas nos computadores onde está implantada**: Se selecionar esta opção, o Gestor de Configuração desativa temporariamente todas as implementações que contêm esta sequência de tarefas. Também remove a sequência de tarefas da lista de implementações disponíveis para executar. A sequência de tarefas não funciona até que a ative. Por defeito, esta opção está desativada.  

    - **Tempo máximo de execução permitido**: Especifica o tempo máximo em minutos que espera que a sequência de tarefas seja executada no computador de destino. Use um número inteiro igual ou superior a zero. Por defeito, este valor é de 120 minutos.  

        > [!IMPORTANT]  
        > Se estiver a utilizar janelas de manutenção para a recolha a que implementa esta sequência de tarefas, poderá ocorrer um conflito se o **tempo máximo de execução permitido** for mais longo do que a janela de manutenção programada. Se definir o tempo máximo de execução para **0**, a sequência de tarefas começa durante a janela de manutenção. Continua a funcionar até que esteja concluído ou falhe após o fecho da janela de manutenção. Como resultado, as sequências de tarefacom um tempo máximo de execução definido para **0** podem passar pela extremidade das suas janelas de manutenção. Se definir o tempo máximo de execução para um período específico (não zero) que exceda o comprimento de qualquer janela de manutenção disponível, então essa sequência de tarefas não funciona. Para mais informações, consulte [Como utilizar as janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

        Se definir o valor como **0**, O Gestor de Configuração avalia o tempo máximo de funcionamento permitido como **12** horas (720 minutos) para monitorizar o progresso. No entanto, a sequência de tarefas começa desde que a duração da contagem regressiva não exceda o valor da janela de manutenção.  

        > [!NOTE]
        > Quando atinge o tempo máximo de funcionamento, se não permitir que os utilizadores interajam com uma implementação necessária, então o Gestor de Configuração para a sequência de tarefas. Se a sequência de tarefaem si não for interrompida, o Gestor de Configuração para de monitorizar a sequência de tarefas depois de atingir o tempo máximo de execução permitido.

    - **Utilize uma imagem**de arranque : Utilize a imagem de arranque selecionada quando a sequência de tarefas estiver executada. **Selecione Browse** para selecionar uma imagem de arranque diferente. Limpe esta opção de desativar a utilização da imagem de boot selecionada quando a sequência de tarefas estiver em funcionação.  

    - **Esta sequência de tarefas pode ser executada em qualquer plataforma**: Se selecionar esta opção, o Gestor de Configuração não verifica o tipo de plataforma do computador de destino quando a sequência de tarefas funciona. Esta opção está selecionada por predefinição.  

    - **Esta sequência de tarefas só pode ser executada nas plataformas específicas do cliente**: Esta opção especifica os processadores, versões OS e pacotes de serviço sintetizadores em que esta sequência de tarefas pode ser executada. Quando selecionar esta opção, selecione pelo menos uma plataforma da lista. Por padrão, não são selecionadas plataformas. O Gestor de Configuração utiliza esta informação quando avalia quais os computadores de destino de uma coleção que recebem a sequência de tarefas implementada.  

        > [!NOTE]  
        > Quando executa uma sequência de tarefas a partir de boot media ou PXE, o Gestor de Configuração ignora esta opção. A sequência de tarefas funciona como se fosse a opção **que este programa pode executar em qualquer plataforma.**  

## <a name="high-impact-settings"></a>Definições de alto impacto

Configure uma sequência de tarefas como de alto impacto e personalize as mensagens que os utilizadores recebem quando executam a sequência de tarefas.

> [!WARNING]
> Se utilizar as implementações pXE e configurar o hardware do dispositivo com o adaptador de rede como o primeiro dispositivo de arranque, estes dispositivos podem iniciar automaticamente uma sequência de tarefas de implementação de SISTEMAS sem interação do utilizador. A verificação de implementação não gere esta configuração. Embora esta configuração possa simplificar o processo e reduzir a interação do utilizador, coloca o dispositivo em maior risco de reimagem acidental.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefade alto impacto

Utilize o procedimento seguinte para definir uma sequência de tarefas como de alto impacto.

> [!NOTE]  
> Qualquer sequência de tarefa que satisfaça determinadas condições é automaticamente definida como de alto impacto. Para obter mais informações, consulte [Gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**  

2. Selecione a sequência de tarefas para editar e selecione **Propriedades**.  

3. No separador Notificação do **Utilizador,** selecione **Esta é uma sequência de tarefas de alto impacto**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implementações de alto risco

Utilize o seguinte procedimento para criar uma notificação personalizada para implementações de alto impacto.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**  

2. Selecione a sequência de tarefas para editar e selecione **Propriedades**.  

3. No separador Notificação do **Utilizador,** selecione **Use texto personalizado**.  

    > [!NOTE]
    > Só é possível definir texto de notificação do utilizador quando selecionar a opção, **esta é uma sequência de tarefas de alto impacto**.  

4. Configure as seguintes definições:  

    > [!Note]  
    > Cada caixa de texto tem um limite máximo de 255 caracteres.  

    - **Texto de manchete**de notificação do utilizador : Especifica o texto azul que apresenta na notificação do utilizador do Centro de Software. Por exemplo, na notificação padrão do utilizador, esta secção contém "Confirme que pretende atualizar o sistema operativo neste computador."  

    - Texto de mensagem de **notificação**do utilizador : Existem três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto requerem que adicione texto.  

        - Primeira caixa de texto: Especifica o corpo principal do texto, que normalmente contém instruções para o utilizador. Por exemplo, na notificação padrão do utilizador, esta secção contém "A atualização do sistema operativo leva tempo e o computador pode reiniciar várias vezes."  

        - Segunda caixa de texto: Especifica o texto arrojado sob o corpo principal do texto. Por exemplo, na notificação padrão do utilizador, esta secção contém "Esta atualização no local instala o novo sistema operativo e migra automaticamente as suas aplicações, dados e configurações."  

        - Terceira caixa de texto: Especifica a última linha de texto sob o texto arrojado. Por exemplo, na notificação padrão do utilizador, esta secção contém "Clique em Instalar para começar. Caso contrário, clique em Cancelar."  

#### <a name="example"></a>Exemplo

Digamos que configura a seguinte notificação personalizada em propriedades.

![Separador de notificação personalizado do utilizador das propriedades da sequência de tarefas](../media/user-notification.png)

A seguinte mensagem de notificação mostra quando o utilizador final abre a instalação do Centro de Software.

![Notificação de sequência de tarefas personalizada ao utilizador final do Centro de Software](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Melhorias de desempenho para planos de energia

<!--3555926-->

A partir da versão 1910, pode agora executar uma sequência de tarefas com o plano de alta potência de desempenho. Esta opção melhora a velocidade global da sequência de tarefas. Confunde o Windows para usar o seu plano de potência de alto desempenho incorporado, que proporciona o máximo desempenho em detrimento de um maior consumo de energia. Esta opção está em predefinição para novas sequências de tarefas.

Quando a sequência de tarefas começa, na maioria dos cenários regista o plano de energia ativado atualmente. Em seguida, muda o plano de alimentação ativa para o plano de **alto desempenho** predefinido do Windows. Se a sequência de tarefa reiniciar o computador, repete este processo. No final da sequência de tarefas, repõe o plano de energia para o valor armazenado. Esta funcionalidade funciona tanto no Windows como no Windows PE, mas não tem impacto nas máquinas virtuais.

- Se a sequência de tarefas começar no Windows PE, a sequência de tarefas não regista o plano de alimentação atualmente ativado para posterior reutilização.

- Uma sequência de tarefade implementação de OS que remodela o computador (limpar e carregar) não preserva a definição do plano de energia do antigo SISTEMA. No final da sequência de tarefas, restaura o plano de potência **equilibrado** por defeito.

> [!Important]
> Para aproveitar esta nova funcionalidade de Gestor de Configuração, depois de atualizar o site, atualize os clientes para a versão mais recente. Atualize também as imagens de boot para incluir os mais recentes componentes do cliente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **sistemas operativos**e selecionar o nó de sequências de **tarefas.**

1. Crie ou escolha uma sequência de tarefas existente e, em seguida, selecione **Propriedades**.

1. Mude para o separador **Performance.**

1. Ative a opção de **executar como plano**de potência de alto desempenho .

> [!Warning]
> Seja cauteloso com esta definição no hardware de baixo desempenho. Executar operações intensas do sistema durante um longo período de tempo pode condicionar hardware de gama baixa. Consulte o seu fabricante de hardware para obter orientações específicas.

### <a name="known-issue"></a>Problema conhecido

<!-- 5554928 -->

É necessário criar uma nova sequência de tarefas para ativar ou desativar esta definição para um alto desempenho. A nova configuração aparece nas implementações existentes, mas não se aplica.<!-- SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>Distribuir conteúdo referenciado  

Antes de os clientes executarem uma sequência de tarefas que referencia o conteúdo, distribua esse conteúdo para pontos de distribuição. Em qualquer altura, pode selecionar a sequência de tarefas e distribuir o respetivo conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se fizer alterações na sequência de tarefas com conteúdo atualizado, redistribua o conteúdo antes de estar disponível para os clientes. Utilize o seguinte procedimento para distribuir os conteúdos que são referenciados por uma sequência de tarefas.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Processo de distribuição de conteúdo referenciado em pontos de distribuição  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende distribuir.  

3. No separador **Home** da fita, no grupo **De implantação,** selecione **Distribute Content**. Esta ação inicia o Assistente de Conteúdo distribuído.  

4. Na página **Geral,** verifique se a sequência de tarefas correta é selecionada para distribuição.  

5. Na página **'Conteúdo',** verifique o conteúdo a distribuir, como a imagem de arranque referenciada pela sequência de tarefas.  

6. Na página Destino do **Conteúdo,** especifique as coleções, ponto de distribuição ou grupo de pontos de distribuição onde pretende distribuir o conteúdo da sequência de tarefas.  

    > [!IMPORTANT]  
    > Se a sequência de tarefas que selecionou referencia o conteúdo que já foi distribuído para um ponto de distribuição específico, o assistente não lista esse ponto de distribuição.  

7. Conclua o assistente.  

Também pode pré-encenar o conteúdo referenciado na sequência de tarefas. O Gestor de Configuração cria um ficheiro de conteúdo pré-encenado comprimido que contém os ficheiros, dependências associadas e metadados associados para o conteúdo que seleciona. Em seguida, importa manualmente o conteúdo num servidor de site, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar ficheiros de conteúdo, consulte [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a>Implantação  

Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>Exportação e importação  

Sequências de tarefas de exportação e importação com ou sem objetos conexos. Este conteúdo referenciado inclui os seguintes objetos:  

- Imagens do SO  
- Imagens de arranque  
- Pacotes como o pacote de instalação do cliente  
- Pacotes de controladores  
- Aplicações com dependências  

Considere os seguintes pontos quando exportar e importar sequências de tarefas:  

- O Gestor de Configuração não exporta senhas na sequência de tarefas. Se exportar e importar uma sequência de tarefas que contenha senhas, edite a sequência de tarefas importada para reintroduzir quaisquer palavras-passe. Reveja os seguintes passos que podem incluir uma palavra-passe:  

  - [Associar Domínio ou Grupo de Trabalho](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Ligar à pasta da rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Linha de Comando executar](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Ao exportar uma sequência de tarefas com o passo **set Dynamic Variables,** o Gestor de Configuração não exporta valores para variáveis que configura com a definição de **valor Secreto.** Reintroduza os valores destas variáveis depois de importar a sequência de tarefas.  

- Quando tiver vários locais primários, importe sequências de tarefas no site da administração central.  

### <a name="process-to-export-task-sequences"></a>Processo para exportar sequências de tarefas  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. Na lista **Sequência de Tarefas** , selecione as sequências de tarefas que pretende exportar. Se selecionar mais do que uma sequência de tarefas, todas elas estão armazenadas num ficheiro de exportação.  

3. No separador **Home** da fita, no grupo sequência de **tarefas,** selecione **Exportação**. Esta ação inicia o Assistente de Sequência de Tarefas de Exportação.  

4. Na página **Geral** , especifique as seguintes definições:  

    - **Ficheiro**: Especificar a localização e o nome do ficheiro de exportação. Se introduzir diretamente o nome do ficheiro, certifique-se de que inclui a extensão .zip no nome do ficheiro. Se navegar para o ficheiro de exportação, o assistente adicionará automaticamente esta extensão de nome de ficheiro.  

    - Se não quiser exportar dependências de sequência de tarefas, desmarque a opção **de exportar todas as dependências**da sequência de tarefas . Por predefinição, o assistente verifica se existem todos os objetos relacionados e exporta-os juntamente com a sequência de tarefas. Estas dependências incluem qualquer um para aplicações.  

    - Se não quiser copiar o conteúdo da fonte do pacote para o local de exportação, desmarque a opção de **exportar todos os conteúdos para as sequências e dependências de tarefas selecionadas**. Se selecionar esta opção, o Assistente de Sequência de Tarefas de Importação utiliza o caminho de importação como a nova localização de origem do pacote.  

    - **Comentários do administrador**: Adicione uma descrição das sequências de tarefas a exportar.  

5. Conclua o assistente.  

O assistente cria os seguintes ficheiros de saída:  

- Se não exportar conteúdo: um ficheiro .zip.  

- Se não exportar conteúdos: um ficheiro .zip e uma pasta designada *exportar*_files, em que *exportar* corresponde ao nome do ficheiro .zip que contém os conteúdos exportados.  

Se incluir conteúdo ao exportar uma sequência de tarefas, certifique-se de que copia o ficheiro .zip e a pasta _files *de exportação,* ou se a importação falhar.  

### <a name="process-to-import-task-sequences"></a>Processo de importação de sequências de tarefas  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione A sequência de **tarefas de importação**. Esta ação inicia o Assistente de Sequência de Tarefas de Importação.  

3. Na página **geral** da fita, especifique o ficheiro .zip exportado.  

4. Na página **Conteúdo do Ficheiro** , selecione a ação de que necessita para cada objeto que importar. Esta página mostra todos os objetos que o Gestor de Configuração encontrou para importar.  

    - Se o objeto nunca tiver sido importado, selecione **Criar Novo**.  

    - Se o objeto tiver sido importado anteriormente, selecione uma das seguintes ações:  

        - **Ignore o Duplicate** (padrão): Esta ação não importa o objeto. Em vez disso, o assistente liga o objeto existente à sequência de tarefas.  

        - **Substituir**: esta ação substitui o objeto existente pelo objeto importado. Para aplicações, pode adicionar uma revisão para atualizar a aplicação existente ou criar uma nova aplicação.  

5. Conclua o assistente.  

Depois de importar a sequência de tarefas, edite-a para especificar as palavras-passe que estavam na sequência de tarefas original. Por razões de segurança, as palavras-passe não são exportadas.  

## <a name="return-to-previous-page-on-failure"></a>Volte à página anterior sobre o fracasso

Quando executas uma sequência de tarefas, e há uma falha, podes voltar a uma página anterior do assistente de sequência de tarefas. Em versões anteriores do 'Gestor de Configuração', teve de reiniciar a sequência de tarefas quando houve uma falha. Utilize o botão **Anterior** nos seguintes cenários:

- Quando um computador começa no Windows PE, o diálogo de armadilha de sequência de tarefas pode ser exibido antes da sequência de tarefas estar disponível. Quando selecionar Next neste cenário, a página final da sequência de tarefas mostra com uma mensagem que não existem sequências de tarefas disponíveis. Agora, pode selecionar **Anteriorpara** procurar novamente as sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.  

- Quando executa uma sequência de tarefas, mas os pacotes de conteúdo dependente ainda não estão disponíveis em pontos de distribuição, a sequência de tarefas falha. Se o conteúdo em falta ainda não foi distribuído, distribua-o agora. Ou esperar que o conteúdo esteja disponível em pontos de distribuição. Em seguida, selecione **Anterior para** que a sequência de tarefa volte a procurar o conteúdo.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a>Variáveis de recolha e dispositivo

Pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis que define para um computador são referidas como variáveis de sequência de tarefapor computador. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Para mais informações, consulte [as variáveis de Recolha e Dispositivo.](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>Ações adicionais  

Pode gerir sequências de tarefas utilizando ações adicionais quando selecionar uma sequência de tarefas.  

### <a name="edit"></a>Editar

Para mais informações, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Ativar

Ativa a sequência de tarefas para que os clientes possam executá-la. Não precisas de reimplantar uma sequência de tarefas depois de ativada.  

### <a name="disable"></a>Desativar

Desativa a sequência de tarefas para que não possa funcionar em computadores. Pode implementar uma sequência de tarefas desativada, mas os computadores não executam a sequência de tarefas até que a ative.  

### <a name="export"></a>Exportar

Para obter mais informações, consulte as sequências de [tarefas de exportação e importação](#BKMK_ExportImport).

### <a name="copy"></a>Copiar

Efetua uma cópia da sequência tarefas selecionada. Esta ação é útil para criar uma nova sequência de tarefas baseada numa sequência de tarefas existente.

Quando efetuar uma cópia de uma sequência de tarefas numa pasta, esta é listada nessa pasta até a atualizar o nó da sequência de tarefas. Após a atualização, cópia aparece na pasta raiz.  

### <a name="refresh"></a>Atualizar

Atualiza os detalhes para a sequência de tarefas selecionada.

### <a name="delete"></a>Eliminar

Elimina a sequência de tarefas selecionada.

### <a name="create-phased-deployment"></a>Criar implantação faseada

Para mais informações, consulte [Criar implementações faseadas](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Implementação

Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Distribuir Conteúdo

Inicia o Assistente de Conteúdo distribuído para enviar o conteúdo referenciado para pontos de distribuição.

### <a name="create-prestaged-content-file"></a>Criar Ficheiro de Conteúdo Pré-configurado

Inicia o Assistente para Criar Ficheiro de Conteúdo Pré-configurado para pré-configurar o conteúdo da sequência de tarefas. Para obter mais informações sobre como criar um ficheiro de conteúdo pré-configurado, consulte [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### <a name="move"></a>Mover

Move a sequência de tarefa selecionada para outra pasta no nó de sequências de **tarefas.**

### <a name="set-security-scopes"></a>Definir âmbitos de segurança

Selecione os âmbitos de segurança para a sequência de tarefas selecionada. Para obter mais informações, veja [Âmbitos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Propriedades

Para mais informações, consulte as propriedades do [Configure Software Center](#bkmk_prop-general) e [configure as definições avançadas de sequência](#bkmk_prop-advanced)de tarefas .

### <a name="view"></a>Vista

<!--3633146-->
A partir da versão 1902, a ação **View** nas sequências de tarefas é o padrão. Esta ação permite-lhe ver os passos da sequência de tarefas sem bloqueá-la para edição. Para mais informações, consulte [Utilize o editor da sequência de tarefas](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Consulte também

- [Cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md)

- [Utilizar o editor de sequência de tarefas](../understand/task-sequence-editor.md)

- [Implementar uma sequência de tarefas](deploy-a-task-sequence.md)

- [Passos de sequência de tarefas](../understand/task-sequence-steps.md)

- [Variáveis de recolha e dispositivo](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Criar implementações faseadas](create-phased-deployment-for-task-sequence.md)
