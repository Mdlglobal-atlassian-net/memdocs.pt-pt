---
title: Pacotes e programas
titleSuffix: Configuration Manager
description: Suporte implementações que utilizam pacotes e programas legados com Gestor de Configuração.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2c125212a13790e196d001f53411633d1e42d4f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710112"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Pacotes e programas em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração continua a apoiar pacotes e programas que foram utilizados no Gestor de Configuração 2007. Uma implementação que utilize pacotes e programas pode ser mais adequada do que uma aplicação quando implementa qualquer uma das seguintes ferramentas ou scripts:  

- Ferramentas administrativas que não instalam uma aplicação num computador
- Scripts "one-off" que não precisam de ser monitorizados continuamente  
- Scripts que funcionam em um horário recorrente e não podem usar avaliação global

> [!TIP]  
> Considere utilizar a funcionalidade [Scripts](create-deploy-scripts.md) na consola 'Gestor de Configuração'. Scripts podem ser uma solução melhor para alguns dos cenários anteriores em vez de usar pacotes e programas.

Ao migrar pacotes de uma versão anterior do Gestor de Configuração, pode implantá-los na hierarquia do Gestor de Configuração. Quando a migração é concluída, os pacotes são apresentados no nó **Pacotes** na área de trabalho**Biblioteca de Software**.

Pode modificar e implementar estes pacotes da mesma forma que fez utilizando a distribuição de software. O **Pacote de Importação do Assistente de Definição** permanece no Gestor de Configuração para importar pacotes legados. Os anúncios são convertidos para implementações quando se migra do Gestor de Configuração 2007 para uma hierarquia do Gestor de Configuração.  

> [!NOTE]  
> Utilize o Gestor de Conversão de Pacotes para converter pacotes e programas em aplicações de Gestor de Configuração.  
>
> A partir da versão 1806, o Gestor de Conversão de Pacotes está integrado com o Gestor de Configuração. Para mais informações, consulte O Gestor de Conversão de [Pacotes](../pcm/package-conversion-manager.md).  

Os pacotes podem usar algumas novas funcionalidades do Gestor de Configuração, incluindo grupos de pontos de distribuição e monitorização. Não é possível implementar aplicações de Virtualização de Aplicações microsoft (App-V) com pacotes e programas no 'Gestor de Configuração'. Para distribuir aplicações virtuais, crie-as como aplicações do Gestor de Configuração. Para mais informações, consulte [implementar aplicações virtuais App-V](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Criar um pacote e programa

### <a name="use-the-create-package-and-program-wizard"></a>Use o pacote criar e programar assistente

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Pacotes.**  

2. No separador **Casa** da fita, no grupo **Criar,** escolha **Criar Pacote**.  

3. Na página **pacote** do Programa Criar pacote e assistente de **programa,** especifique as seguintes informações:  

    - **Nome**: Especifique um nome para a embalagem com um máximo de 50 caracteres.  

    - **Descrição**: Especifique uma descrição para este pacote com um máximo de 128 caracteres.  

    - **Fabricante** (opcional): Especifique um nome de fabricante para ajudá-lo a identificar o pacote na consola 'Gestor de Configuração'. Este nome pode ter um máximo de 32 carateres.

    - **Idioma** (opcional): Especifique a versão linguística do pacote com um máximo de 32 caracteres.  

    - **Versão** (opcional): Especifique um número de versão para a embalagem com um máximo de 32 caracteres.

    - **Esta embalagem contém ficheiros de origem**: Esta definição indica se o pacote requer ficheiros de origem para estar presente nos dispositivos do cliente. Por predefinição, o assistente não ativa esta opção e o Gestor de Configuração não utiliza pontos de distribuição para o pacote. Quando selecionar esta opção, especifique o conteúdo do pacote para distribuir para pontos de distribuição.  

    - **Fonte**: Se o pacote contiver ficheiros de origem, escolha **navegar** para abrir a caixa de diálogo da **Pasta De Origem e,** em seguida, especificar a localização dos ficheiros de origem para a embalagem.  

        > [!NOTE]  
        > A conta de computador do servidor do site deve ter permissões de acesso de leitura para a pasta de origem que especificar.  

    - A partir da versão 1906, se quiser pré-cache conteúdo num cliente, especifique a **Arquitetura** e **A Linguagem** do pacote. Para mais informações, consulte o [conteúdo pré-cache da Configure](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. Na página tipo de **programa** do **Programa Do Programa criar pacote e programa,** selecione o tipo de programa para criar e, em seguida, escolha **A Seguir**. Pode criar um programa para um [computador](#create-a-standard-program) ou [dispositivo,](#create-a-device-program)ou pode saltar este passo e criar um programa mais tarde.  

    > [!TIP]  
    > Para criar um novo programa para um pacote existente, primeiro selecione o pacote. Em seguida, no separador **Home,** no grupo **Pacote,** escolha **Criar Programa** para abrir o Assistente do **Programa Criar**.  

#### <a name="create-a-standard-program"></a>Criar um programa padrão

1. Na página tipo de **programa** do Programa Criar Pacote e Assistente de **Programa,** escolha **o Programa Standard,** e depois escolha **o Seguinte**.  

2. Na página do **Programa Standard,** especifique as seguintes informações:  

    - **Nome** - epecifique um nome para o programa com um máximo de 50 carateres.  

        > [!NOTE]  
        > O nome do programa deve ser exclusivo num pacote. Depois de criar um programa, não pode modificar o nome.  

    - **Linha de Comando**: Introduza a linha de comando para utilizar para iniciar este programa ou escolha **navegar** para navegar até à localização do ficheiro.  

        Se não especificar uma extensão para um nome de ficheiro, o Gestor de Configuração tenta utilizar .com, .exe e .bat como possíveis extensões.  

        Quando o cliente executa o programa, o Gestor de Configuração procura o ficheiro nos seguintes locais:

        - Dentro do pacote
        - A pasta local do Windows
        - O *%caminho local%*

        Se não encontrar o ficheiro, o programa falha.  

    - **Pasta** de arranque (opcional): Especifique a pasta a partir da qual o programa funciona, até 127 caracteres. Esta pasta pode ser um caminho absoluto para o cliente. Também pode ser um caminho relativo à pasta do ponto de distribuição que contém o pacote.

    - **Executar**: Especifique o modo em que o programa funciona nos computadores dos clientes. Selecione uma das seguintes opções:  

        - **Normal**: O programa funciona no modo normal com base nos predefinidos do sistema e do programa. Este é o modo predefinido.  

        - **Minimizado**: O programa é minimizado em dispositivos de cliente. Os utilizadores podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

        - **Maximizado**: O programa é maximizado em dispositivos de cliente. Os utilizadores vêem toda a atividade de instalação.  

        - **Hidden**: O programa é executado escondido em dispositivos de cliente. Os utilizadores não vêem nenhuma atividade de instalação.  

    - **O programa pode ser executado**: Especificar se o programa funciona apenas quando um utilizador é inscrito, apenas quando nenhum utilizador é inscrito, ou independentemente de um utilizador estar inscrito no computador cliente.  

    - **Modo de execução**: Especifique se o programa funciona com permissões administrativas ou com as permissões do utilizador que está atualmente inscrito.  

    - **Permitir que os utilizadores vejam e interajam com a instalação do programa**: Utilize esta definição, se disponível, para especificar se permite que os utilizadores interajam com a instalação do programa. Esta opção só está disponível se forem satisfeitas as seguintes condições:

        - **O programa pode executar** a definição **apenas quando nenhum utilizador é ligado** ou se um utilizador está ou não **ligado**
        - A definição do **modo de execução** é **correr com direitos administrativos**  

    - **Modo de acionamento**: Especifique informações sobre o funcionamento deste programa na rede. Selecione uma das seguintes opções:  

        - **Executa com o nome UNC**: Especifique que o programa executa com um nome de Convenção Universal de Nomeação (UNC). Esta é a predefinição.  

        - **Requer a carta de unidade**: Especifique que o programa requer uma carta de unidade para qualificar totalmente a sua localização. Para esta definição, o Gestor de Configuração pode utilizar qualquer letra de unidade disponível no cliente.  

        - **Requer uma carta**de unidade específica : Especifique que o programa requer uma letra de unidade específica que especifica para qualificar totalmente a sua localização. Por exemplo, **Z:**. Se o cliente já estiver a usar a carta de unidade especificada, o programa não funciona.  

    - **Religue-se ao ponto**de distribuição no início do início : Indique se o cliente volta a ligar-se ao ponto de distribuição quando o utilizador faz o login. Por predefinição, o assistente não ativa esta opção.

3. Na página De requisitos do **Programa Criar Pacote e Assistente de Programa,** especifique as **seguintes** informações:  

    - **Executar primeiro outro programa**: Identifique um pacote e programa que corre antes de este pacote e programa funcionar.  

    - **Requisitos da plataforma**: Selecione **Este programa pode ser executado em qualquer plataforma** ou este programa só pode ser executado em plataformas **especificadas**. Em seguida, escolha as versões OS que os clientes devem ter de instalar este pacote e programa.  

    - **Espaço estimado**do disco : Especifique a quantidade de espaço em disco que o programa necessita para ser executado no computador. A definição predefinida é **Desconhecida**. Se necessário, especifique um número inteiro maior ou igual a zero. Se definir um valor, selecione também unidades para o valor.  

    - **Máximo tempo de execução permitido (minutos)**: Especifique o tempo máximo que espera que o programa seja executado no computador cliente. O valor padrão é de **120** minutos. Só use números inteiros maiores que zero.  

        > [!IMPORTANT]  
        > Se utilizar janelas de manutenção na mesma coleção para a qual implementa este programa, poderá ocorrer um conflito se o **tempo máximo de execução permitido** for mais longo do que a janela de manutenção programada. Se definir o tempo máximo de execução para **Unknown,** o programa começa a funcionar durante a janela de manutenção. Em seguida, continua a funcionar conforme necessário após o fecho da janela de manutenção. Se definir o tempo máximo de execução para um período específico que seja maior do que o comprimento de qualquer janela de manutenção disponível, então o cliente não executa o programa.  

        Se definir este valor para **Unknown,** O Gestor de Configuração define o tempo máximo de funcionamento permitido como 12 horas (720 minutos).  

        > [!NOTE]  
        > Se o programa exceder o tempo máximo de execução, o Gestor de Configuração pára-o se forem satisfeitas as seguintes condições:
        >
        > - Você permite a opção **de Correr com direitos administrativos**
        > - Não permite que os **utilizadores vejam e interajam com a instalação do programa**  

#### <a name="create-a-device-program"></a>Criar um programa de dispositivos  

1. Na página tipo de **programa** do Programa Do **Programa criar pacote e programa,** selecione **Programa para dispositivo**, e depois escolha **Seguinte**.  

2. Na página **Programa para Dispositivo,** especifique as seguintes definições:  

    - **Nome**: Especifique um nome para o programa com um máximo de 50 caracteres.  

        > [!NOTE]  
        > O nome do programa deve ser exclusivo num pacote. Depois de criar um programa, não pode modificar o nome.  

    - **Comentário** (opcional): Especifique um comentário para este programa de dispositivocom um máximo de 127 caracteres.  

    - **Baixar a pasta**: Especifique o nome da pasta no dispositivo no qual armazenará os ficheiros de origem do pacote. O valor predefinido é `\Temp\`.  

    - **Linha de Comando**: Introduza a linha de comando para utilizar para iniciar este programa. Para navegar na localização do ficheiro, escolha **Navegar**.  

    - **Executar a linha de comando na pasta de descarregamento**: Selecione esta opção para executar o programa a partir da pasta de descarregamento.  

    - **Executar a linha de comando a partir desta pasta**: Selecione esta opção para especificar uma pasta diferente a partir da qual executar o programa.  

3. Na página **Requisitos,** especifique as seguintes definições:  

    - **Espaço estimado**do disco : Especifique a quantidade de espaço em disco que é necessário para o software. O cliente exibe este valor aos utilizadores de dispositivos móveis antes de instalar o programa.  

    - **Programa de descarregamento**: Especifique informações sobre quando o dispositivo móvel pode descarregar este programa. Pode especificar **Assim que possível**, **Apenas sobre uma rede rápida** ou **Apenas quando o dispositivo estiver ancorado**.  

    - **Requisitos adicionais**: Especifique quaisquer requisitos adicionais para este programa. Os utilizadores vêem estes requisitos antes de instalarem o software. Por exemplo, pode indicar os utilizadores que necessitam de fechar todas as outras aplicações antes de executar o programa.  

## <a name="deploy-packages-and-programs"></a>Implementar pacotes e programas  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Pacotes.**  

2. Selecione o pacote que pretende implementar. No separador **Home** da fita, no grupo **de implantação,** escolha **Implantação**.  

3. Na página **geral** do **Assistente de Software de Implementação,** especifique o nome do pacote e programa que pretende implementar. Selecione a coleção para a qual pretende implementar o pacote e programa, e quaisquer comentários opcionais.  

    Para armazenar o conteúdo do pacote no grupo de pontos de distribuição predefinido da coleção, selecione a opção de utilizar grupos de pontos de **distribuição predefinidos associados a esta recolha**. Se não associou esta coleção a um grupo de pontos de distribuição, esta opção não está disponível.  

4. Na página **de Conteúdo,** escolha **Adicionar**. Selecione os pontos de distribuição ou os grupos de pontos de distribuição para os quais pretende distribuir o conteúdo para este pacote e programa.  

5. Na página Definições de **Implementação,** configure as seguintes definições:  

    - **Objetivo**: Escolha uma das seguintes opções:

        - **Disponível**: O utilizador vê o pacote e programa publicados no Centro de Software e pode instalá-lo a pedido.  

        - **Requerido**: O pacote e o programa são implantados automaticamente, de acordo com o horário configurado. No Software Center, pode rastrear o seu estado de implementação e instalá-lo antes do prazo.  

        > [!NOTE]
        > Se vários utilizadores forem assinados no dispositivo, as implementações de sequências de pacotes e de tarefas podem não aparecer no Centro de Software.

    - **Envie pacotes de despertar**: Se definir o propósito de implementação para **O Necessário** e selecionar esta opção, o site envia primeiro um pacote de despertar para computadores no prazo de instalação. Antes de poder utilizar esta opção, configure os computadores para Wake On LAN. Para mais informações, consulte [Como configurar Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Permitir que os clientes numa ligação à Internet medido descarreguem conteúdos após o prazo de instalação, o que pode incorrer em custos adicionais**  

    > [!NOTE]  
    > Quando implementa um pacote e programa, a opção de **pré-implementação** do software para o dispositivo principal do utilizador não está disponível.  

6. Na página **de Agendamento,** configure quando implementar este pacote e programa para dispositivos clientes.  

    As opções nesta página variam consoante definir a ação de implementação para **Disponível** ou **Obrigatório**.  

    Para as implementações **necessárias,** configure o comportamento de reexecutar para o programa a partir do menu de **rerun.** Pode escolher uma das seguintes opções:  

    | Comportamento da nova execução | Descrição |
    |----------------|-------------|
    | **Nunca voltar a executar o programa implementado** | O cliente não vai refazer o programa. Este comportamento acontece mesmo que o programa falhe inicialmente ou se os ficheiros do programa forem alterados. |
    | **Executar sempre novamente o programa** | O cliente repete sempre o programa quando a implementação está programada. Este comportamento acontece mesmo que o programa já tenha executado com sucesso. É útil com implementações recorrentes quando atualiza o programa. |
    | **Executar novamente se a tentativa anterior falhar** | O cliente repete o programa quando a implementação está programada, apenas se falhar na tentativa de execução anterior. |
    | **Executar novamente se a tentativa anterior tiver êxito** | O cliente só regere o programa se tiver sido executado com sucesso no cliente. Este comportamento é útil com implementações recorrentes quando atualiza o programa rotineiramente, e cada atualização requer que a atualização anterior seja instalada com sucesso. |

7. Na página **Experiência de Utilizador** , especifique as seguintes informações:  

    - **Permitir que os utilizadores executem o programa de forma independente das atribuições**: Os utilizadores podem instalar este software no Software Center, independentemente de qualquer tempo de instalação programado.  

    - **Instalação do software**: permite que o software seja instalado fora de quaisquer janelas de manutenção configuradas.  

    - **Reinício do sistema (se necessário para completar a instalação)**: Se a instalação do software necessitar de um reinício do dispositivo para terminar, permita que esta ação aconteça fora de quaisquer janelas de manutenção configuradas.  

    - **Dispositivos incorporados**: Quando implementa pacotes e programas para dispositivos Incorporados do Windows que estão ativados por filtros de escrita, pode especificar que instalam pacotes e programas na sobreposição temporária e cometem alterações posteriormente. Alternadamente, comprometa as alterações no prazo de instalação ou durante uma janela de manutenção. Quando comete alterações no prazo de instalação ou durante uma janela de manutenção, é necessário reiniciar e as alterações persistem no dispositivo.  

        > [!NOTE]  
        > Quando implementa um pacote ou programa num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Para obter mais informações sobre como as janelas de manutenção são usadas quando implementa pacotes e programas para dispositivos Incorporados windows, consulte a Criação de [aplicações Incorporadas do Windows](../get-started/creating-windows-embedded-applications.md).  

8. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    - **Opções de implementação**: Especifique a ação de que um cliente quando utiliza um ponto de distribuição no seu atual grupo de limites. Selecione também a ação para o cliente quando utilizar um ponto de distribuição de um grupo de fronteira sinuoso ou do grupo de fronteira do site predefinido.

        > [!IMPORTANT]  
        > Se configurar a opção de implementação para executar o programa a **partir do ponto de distribuição,** certifique-se de ativar a opção de copiar o conteúdo neste pacote para uma partilha de pacote em **pontos** de distribuição no separador **data Access** das propriedades do pacote. Caso contrário, o pacote não está disponível para ser executado a partir de pontos de distribuição.  

    - Permitir que os **clientes utilizem pontos de distribuição do grupo**de limites do site padrão : Quando este conteúdo não estiver disponível a partir de qualquer ponto de distribuição nos grupos de fronteira atuais ou vizinhos, permita-lhes que experimentem pontos de distribuição no grupo de limites padrão do site.

9. Conclua o assistente.  

Ver a implantação no nó de **implantação** do espaço de trabalho de **monitorização** e no painel de detalhes do separador de implementação do pacote quando selecionar a implementação. Para mais informações, consulte os [pacotes e programas do Monitor.](#monitor-packages-and-programs)  


## <a name="monitor-packages-and-programs"></a>Monitorizar pacotes e programas

Para monitorizar as implementações de pacotes e programas, utilize os mesmos procedimentos que utiliza para monitorizar as aplicações conforme detalhado nas [aplicações do Monitor](monitor-applications-from-the-console.md).  

Os pacotes e programas também incluem uma série de relatórios incorporados, que lhe permitem monitorizar informações sobre o estado de implementação de pacotes e programas. Estes relatórios têm a categoria de relatório de **Distribuição de Software – Pacotes e Programas** e **Distribuição de Software - Estado de Implementação do Pacote e do Programa**.  

Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Gerir pacotes e programas

No espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Pacotes.** Selecione o pacote que pretende gerir e, em seguida, escolha uma tarefa de gestão.  

### <a name="create-prestage-content-file"></a>Criar Ficheiro de Conteúdo Pré-configurado

Abre o Assistente de Ficheiros de **Conteúdo Pré-Encenado,** para criar um ficheiro que contenha o conteúdo do pacote. Utilize este ficheiro para importar manualmente a embalagem para um ponto de distribuição remoto. Esta ação é útil quando se tem baixa largura de banda de rede entre o servidor do site e o ponto de distribuição.

### <a name="create-program"></a>Criar Programa

Abre o Assistente do **Programa Criar,** para criar um novo programa para este pacote.

### <a name="export"></a>Exportar

Abre o Assistente do **Pacote de Exportação,** para exportar o pacote selecionado e o seu conteúdo para um ficheiro. Use este ficheiro para importar o ficheiro para outra hierarquia.

Para obter informações sobre como importar pacotes e programas, consulte [Criar pacotes e programas.](#create-a-package-and-program)

### <a name="deploy"></a>Implementação

Abre o **Assistente de Software de Implantação,** para implementar o pacote e programa selecionados para uma coleção. Para mais informações, consulte [Pacotes e programas de implantação.](#deploy-packages-and-programs)

### <a name="distribute-content"></a>Distribuir conteúdo

Abre o **Assistente de Conteúdo**distribuído, para enviar o conteúdo para um pacote e programa para pontos de distribuição selecionados ou grupos de pontos de distribuição.

### <a name="update-distribution-points"></a>Atualizar pontos de distribuição

Atualiza pontos de distribuição com o conteúdo mais recente para o pacote e o programa selecionados.


## <a name="see-also"></a>Consulte também

- [Scripts](create-deploy-scripts.md)

- [Gestor de Conversão de Pacotes](../pcm/package-conversion-manager.md)

- [Ficheiros de definição de pacote](package-definition-files.md)
