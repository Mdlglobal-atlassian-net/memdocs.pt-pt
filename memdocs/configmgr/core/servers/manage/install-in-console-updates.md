---
title: Atualizações na consola
titleSuffix: Configuration Manager
description: Instale atualizações para O Gestor de Configuração a partir da nuvem da Microsoft
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fee0cdf72ae8975d26bebd4da765941116421c25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713836"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instale atualizações na consola para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, instale estas atualizações a partir da consola 'Gestor de Configuração'.

## <a name="get-available-updates"></a>Obter as atualizações disponíveis

O site apenas descarrega atualizações que se aplicam à sua infraestrutura e versão. Esta sincronização pode ser automática ou manual, dependendo da configuração do ponto de ligação de serviço para a sua hierarquia:

- No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

    Por predefinição, o Gestor de Configuração verifica novas atualizações a cada 24 horas. Verifique manualmente se há atualizações na consola 'Gestor de Configuração'. Vá ao espaço de trabalho da **Administração,** selecione as **Atualizações e** o nó de Manutenção e escolha **Verificar as atualizações** na fita.  

- No **modo offline,** o ponto de ligação ao serviço não se liga ao serviço de nuvem da Microsoft. Para descarregar e, em seguida, importar as atualizações disponíveis, utilize a Ferramenta de [Ligação de Serviço](use-the-service-connection-tool.md).  

> [!NOTE]  
> Se necessário, importe correções fora da banda para a sua consola. Para isso, utilize a ferramenta de registo de [atualização](use-the-update-registration-tool-to-import-hotfixes.md). Estas correções fora de banda complementam as atualizações que obtém quando sincroniza com o serviço de nuvem da Microsoft.  

Depois de atualizações sincronizar, veja-as na consola Do Gestor de Configuração. Vá ao espaço de trabalho da **Administração** e selecione as Atualizações e o nó **de Manutenção.**  

- Atualizações que não instalou o ecrã como **disponível**.  

- Atualizações que instalou o ecrã como **Instalado**. Apenas é mostrada a atualização mais recente. Para ver atualizações previamente instaladas, selecione **History** na fita.  

Antes de configurar o ponto de ligação de serviço, compreenda e planeie as suas utilizações adicionais. As seguintes utilizações podem afetar a forma como configura este papel do sistema do site:  

- O site utiliza o ponto de ligação de serviço para fazer upload de informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para mais informações, consulte [Diagnósticos e dados de utilização](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para entender melhor o que acontece quando as atualizações são descarregadas, consulte os seguintes fluxogramas:  

- [Fluxograma – Transferir atualizações](download-updates-flowchart.md)  

- [Fluxograma – Atualizar replicação](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para visualizar e gerir atualizações e funcionalidades

Para visualizar atualizações na consola, um utilizador deve ter uma função de segurança de administração baseada em papéis que inclua os pacotes de **atualização**da classe de segurança . Esta classe concede acesso a visualização e gestão de atualizações na consola 'Gestor de Configuração'.

### <a name="about-the-update-packages-class"></a>Sobre a classe de pacotes update

Por predefinição, a classe **de pacotes update** (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança incorporadas com as permissões listadas:  

- **Administrador Total** com permissões de **Modificação** e **Leitura** :  

  - Um utilizador com esta função de segurança e acesso ao âmbito de segurança **All** pode visualizar e instalar atualizações. O utilizador também pode ativar as funcionalidades durante a instalação e ativar as funcionalidades individuais após as atualizações do site.  

  - Um utilizador com esta função de segurança e acesso ao âmbito de segurança **Predefinido** pode visualizar e instalar atualizações. O utilizador também pode ativar as funcionalidades durante a instalação e visualizar funcionalidades após as atualizações do site. Mas este utilizador não consegue ativar as funcionalidades após as atualizações do site.  

- **Analista só de leitura** com permissões de **Leitura** :  

  - Um utilizador com esta função de segurança e acesso ao âmbito **Predefinido** pode ver atualizações, mas não instalá-las. Este utilizador também pode visualizar funcionalidades após as atualizações do site, mas não pode ativar as mesmas.  

### <a name="permissions-required-for-updates-and-servicing"></a>Permissões necessárias para atualizações e manutenção

- Utilize uma conta à qual atribui uma função de segurança que inclui a classe **de pacotes Update** com permissões **De modificação** e **leitura.**  

- Atribuir a conta ao âmbito **predefinido.**  

### <a name="permissions-to-only-view-updates"></a>Permissões para apenas ver atualizações

- Utilize uma conta à qual atribui uma função de segurança que inclui a classe **de pacotes Update** com apenas a permissão **Read.**  

- Atribuir a conta ao âmbito **predefinido.**  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Permissões necessárias para ativar funcionalidades após as atualizações do site

- Utilize uma conta à qual atribui uma função de segurança que inclui a classe **de pacotes Update** com permissões **De modificação** e **leitura.**  

- Atribuir a conta ao âmbito **all.**  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  

Reveja os seguintes passos antes de instalar uma atualização a partir da consola 'Gestor de Configuração'.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Passo 1: rever a lista de verificação de atualizações  

Reveja a lista de verificação de atualização aplicável para que as ações tomem antes de iniciar a atualização:

- [Lista de verificação para instalar a atualização de 2002](checklist-for-installing-update-2002.md)

- [Lista de verificação para instalar a atualização 1910](checklist-for-installing-update-1910.md)  

- [Lista de verificação para instalar a atualização 1906](checklist-for-installing-update-1906.md)  

- [Lista de verificação para instalar a atualização 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a>Passo 2: Executar o verificador pré-requisito antes de instalar uma atualização  

Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

- O site replica ficheiros de atualização para outros sites antes de instalar a atualização.  

- Quando optar por instalar a atualização, a verificação prévia é automaticamente reparada.  

> [!NOTE]  
> Quando inicia uma verificação pré-requisito e, em seguida, vê o estado, a fase de **instalação** parece estar ativa. No entanto, o site não está realmente a instalar a atualização. Para eexecutar a verificação pré-requisito, o processo de atualização extrai o pacote da biblioteca de conteúdos. Em seguida, coloca o pacote numa pasta de encenação onde pode aceder às verificações pré-requisitos atuais. Quando instala uma atualização, este mesmo processo decorre. Este comportamento é por isso que a fase de instalação mostra como **em curso**. Apenas a etapa do *pacote de atualização* de extração é mostrada na categoria de Instalação.  

Mais tarde, quando instalar a atualização, pode configurar a atualização para ignorar os avisos de verificação pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione as Atualizações e o nó **de Manutenção.**  

2. Selecione o pacote de atualização para o qual pretende executar a verificação prévia.  

3. Selecione **Executar pré-requisito verifique** a fita.  

    Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados. Consulte o **distmgr.log** no servidor do site para confirmar que o conteúdo se replica com sucesso.  

4. Para ver os resultados da verificação pré-requisito:  

    1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.**  

    2. Selecione o nó **de Atualizações e Estado de Manutenção** e procure o estado pré-requisito.  

    3. Para mais informações, consulte o **registo ConfigMgrPrereq** no servidor do site.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Instalar atualizações na consola  

Quando estiver pronto para instalar atualizações a partir da consola 'Gestor de Configuração', comece com o site de alto nível da sua hierarquia. Este site é ou o site da administração central ou um local primário autónomo.  

Instale a atualização fora do horário normal de trabalho para cada site para minimizar o efeito nas operações comerciais. A instalação da atualização pode incluir ações como a reinstalação de componentes do site e funções do sistema do site.  

- Os sites primários infantis iniciam automaticamente a atualização após o site da administração central concluir a instalação da atualização. Este processo é por defeito e recomendado. Para controlar quando um site primário instala atualizações, utilize [as janelas do Serviço para servidores](service-windows.md)do site .  

- Após a atualização do site principal dos pais estar concluída, atualize manualmente os sites secundários a partir da consola 'Gestor de Configuração'. A atualização automática dos servidores secundários do site não é suportada.  

- Quando utilizar uma consola de Configuração Manager após a atualização do site, é-lhe solicitado que atualize a consola.  

- Depois de o servidor do site concluir com sucesso a instalação de uma atualização, atualiza automaticamente todas as funções do sistema do site aplicáveis. No entanto, todos os pontos de distribuição não se reinstalam e ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor do site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização a um subconjunto de pontos de distribuição de cada vez. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Os pontos de distribuição que ainda não começaram a atualizar ou que tenham concluído a atualização permanecem online e capazes de fornecer conteúdo aos clientes.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  

#### <a name="1-when-the-update-installation-starts"></a>1. Quando a instalação da atualização é iniciada

É apresentado ao Assistente de Atualizações que apresenta uma lista das áreas do produto a que a atualização se aplica.  

- Na página **geral** do assistente, configure **as advertências pré-requisitos** conforme necessário:  

  - Os erros de pré-requisitos interrompem sempre a instalação da atualização. Corrija erros antes de poder voltar a tentar a instalação da atualização com sucesso. Para mais informações, consulte [a instalação de Retry de uma atualização falhada](#bkmk_retry).  

  - Os avisos de pré-requisitos também podem interromper a instalação da atualização. Corrija os avisos antes de voltar a tentar a instalação da atualização. Para mais informações, consulte [a instalação de Retry de uma atualização falhada](#bkmk_retry).  

  - **Ignore quaisquer avisos de verificação pré-requisitos e instale esta atualização independentemente dos requisitos em falta**: Desempre uma condição para que a instalação da atualização ignore as advertências pré-requisitos. Esta opção permite que a instalação da atualização continue. Se não selecionar esta opção, a instalação da atualização para quando o processo encontra um aviso. A menos que tenha feito previamente a verificação pré-requisito e os avisos pré-requisitos fixos para um site, não utilize esta opção.  

    Tanto nos espaços de trabalho da **Administração** como da **Monitorização,** as Atualizações e o nó de Manutenção incluem um botão na fita denominada **Ignorar avisos pré-requisitos**. Este botão fica disponível quando um pacote de atualização não está a concluir a instalação devido a avisos de verificação pré-requisitos. Por exemplo, instala uma atualização sem utilizar a opção de ignorar os avisos pré-requisitos (a partir do Assistente de Atualizações). A instalação da atualização para com um estado de aviso pré-requisito, mas sem erros. Mais tarde, selecione **Ignorar avisos pré-requisitos** na fita. Esta ação desencadeia uma continuação automática dessa instalação de atualização, que ignora as advertências pré-requisitos. Quando utiliza esta opção, a instalação da atualização continua automaticamente após alguns minutos.  

- Quando uma atualização se aplica ao cliente do Gestor de Configuração, opte por testar a atualização do cliente com um conjunto limitado de clientes. Para mais informações, consulte como testar as atualizações dos [clientes numa coleção pré-produção.](../../clients/manage/upgrade/test-client-upgrades.md)  

#### <a name="2-during-the-update-installation"></a>2. Durante a instalação da atualização

Como parte da instalação da atualização, o Gestor de Configuração faz as seguintes ações:  

- Reinstala quaisquer componentes afetados, como funções de sistema de site ou a consola Do Gestor de Configuração.  

- Gere atualizações para clientes com base nas seleções que fez para a pilotagem de clientes e para [atualizações automáticas](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)de clientes.  

- Os servidores do sistema do site geralmente não precisam de reiniciar como parte da atualização. Se uma função utilizar .NET e o pacote atualizar esse componente pré-requisito, então o sistema de site pode reiniciar.  

> [!TIP]  
> Quando instala atualizações do 'Gestor de Configuração', o site também atualiza o CD. Última pasta. Para mais informações, consulte [o CD. Última pasta.](the-cd.latest-folder.md)  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorizar o progresso das atualizações à medida que são instaladas

Utilize os seguintes passos para monitorizar o progresso:  

- Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione as Atualizações e o nó **de Manutenção.** Este nó mostra o estado da instalação para todos os pacotes de atualização.  

- Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Atualizações e Estado de Manutenção.** Este nó mostra o estado de instalação apenas do pacote de atualização atual que o site está a instalar.  

    A instalação da atualização está dividida em várias fases para uma monitorização mais fácil. Para cada uma das seguintes fases, os detalhes adicionais no estado de instalação incluem qual o ficheiro de registo a visualizar para obter mais informações:  

  - **Download**: Esta fase aplica-se apenas ao site de alto nível com o ponto de ligação de serviço.

  - **Replicação**

  - **Verificação de Pré-requisitos**

  - **Instalação**

  - **Instalação do post**: Para mais informações, consulte as tarefas de [instalação do correio.](#post-installation-tasks)  

- Ver o ficheiro **CMUpdate.log** `<ConfigMgr_Installation_Directory>\Logs` no servidor do site.  

>[!NOTE]
> A partir da versão 1906, pode ver o estado da tarefa de base de **dados Upgrade ConfigMgr** durante a fase de **instalação.**
>
> - Se a atualização da base de dados estiver bloqueada, receberão o aviso **Em andamento, necessitará de atenção.**
>   - O cmupdate.log registará o nome do programa e o sessionid da SQL que está bloqueando a atualização da base de dados.
> - Quando a atualização da base de dados já não estiver bloqueada, o estado será reiniciado em **curso** ou **Concluído**.
>   - Quando a atualização da base de dados está bloqueada, uma verificação é feita a cada 5 minutos para ver se ainda está bloqueada.

#### <a name="4-when-the-update-installation-completes"></a>4. Quando a instalação da atualização é concluída

Após a instalação da primeira atualização do site ser concluída:  

- Os sites primários infantis instalam a atualização automaticamente. Não são necessárias mais ações.  

- Atualize manualmente os sites secundários a partir da consola 'Gestor de Configuração'. Para mais informações, consulte [iniciar a instalação da atualização num local secundário](#bkmk_secondary).  

- Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para mais informações, consulte [Interoperabilidade entre diferentes versões](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Consolas do Gestor de Configuração de Atualizações

Depois de um site de administração central ou atualizações do site primário, cada consola do Gestor de Configuração que se conecta ao site também deve atualizar. É-lhe pedido que atualize uma consola:  

- Quando abrir a consola  

- Quando fores a um novo nó numa consola aberta  

Atualize a consola imediatamente após as atualizações do site.  

Depois de a atualização da consola estar concluída, verifique se as versões da consola e do site estão corretas. Vá ao **About Configuration Manager** no canto superior esquerdo da consola.  

> [!Note]  
> A versão da consola é ligeiramente diferente da versão do site. A versão menor da consola corresponde à versão de lançamento do Gestor de Configuração. Por exemplo, na versão 1802 do Configuration Manager a versão inicial do site é de 5.0.8634.1000, e a versão inicial da consola é de 5. **1802**.1082.1700. Os números de construção (1082) e revisão (1700) podem mudar com futuros hotfixos.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a>Para iniciar a instalação de atualização no site de alto nível  

No site de alto nível da sua hierarquia, na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione as Atualizações e o nó **de Manutenção.** Selecione uma atualização com o estado **disponível**e, em seguida, escolha instalar o **Pack de Atualização** na fita.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  

Depois de atualizações do site principal do site secundário, atualize o site secundário a partir da consola Do Gestor de Configuração. Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site secundário que pretende atualizar e, em seguida, escolha **o Upgrade** na fita.  

2. Selecione **Sim** para iniciar a atualização do site secundário.  

Para monitorizar a instalação da atualização num local secundário, selecione o local secundário e escolha o Estado de **Instalação** do Show na fita. Adicione também a coluna **Versão** ao nó dos Sites para que possa ver a versão de cada site secundário.  

Em alguns casos, o estado na consola não atualiza ou sugere que a atualização falhou. Depois de um site secundário atualizar com sucesso, utilize a opção de **instalação Retry.** Esta opção não reinstala a atualização para um site secundário que instalou com sucesso a atualização, mas obriga a consola a atualizar o estado.

### <a name="post-installation-tasks"></a>Tarefas de pós-instalação

Quando um site instala uma atualização, existem várias tarefas que só podem arrancar depois de a atualização concluir a instalação no servidor do site. Esta lista inclui as tarefas de pós-instalação que são fundamentais para operações de site e hierarquia. Porque são críticos, são monitorizados ativamente. Tarefas adicionais que não são monitorizadas diretamente incluem a reinstalação de funções do sistema do site. Para ver o estado das tarefas críticas de pós-instalação, selecione a tarefa de **instalação de correio** enquanto monitoriza a instalação da atualização para um local.

Nem todas as tarefas completam imediatamente. Algumas tarefas só começam quando cada site concluir a instalação da atualização. A nova funcionalidade que pode esperar pode ser adiada até que estas tarefas estejam concluídas. Ligar novas funcionalidades só começa quando todos os sites completam a instalação da atualização, pelo que novas funcionalidades podem não ser visíveis durante algum tempo.

As tarefas de instalação de correio incluem:

- **Instalação do serviço SMS_EXECUTIVE**

  - Serviço crítico que funciona no servidor do site.
  - A reinstalação deste serviço deve ser concluída rapidamente.

- **Instalação de componentes SMS_DATABASE_NOTIFICATION_MONITOR**

  - Fio de componente de local crítico do serviço SMS_EXECUTIVE.
  - A reinstalação deste serviço deve ser concluída rapidamente.

- **Instalação de componentes SMS_HIERARCHY_MANAGER**

  - Componente de site crítico que funciona no servidor do site.
  - Responsável pela reinstalação de funções nos servidores do sistema do site. O estado da reinstalação de funções do sistema de site individual não é apresentado.
  - A reinstalação deste serviço deve ser concluída rapidamente.

    > [!Note]
    > Algumas funções de site do Gestor de Configuração partilham o quadro do cliente. Por exemplo, o ponto de gestão e o ponto de distribuição de puxar. Quando estas funções atualizam, a versão do cliente nestes servidores atualiza ao mesmo tempo. Para mais informações, consulte [Como atualizar os clientes.](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)

- **Instalação SMS_REPLICATION_CONFIGURATION_MONITOR componente**

  - Componente de site crítico que funciona no servidor do site.
  - A reinstalação deste serviço deve ser concluída rapidamente.

- **Instalação SMS_POLICY_PROVIDER componente**

  - Componente de local crítico que funciona apenas em locais primários.
  - A reinstalação deste serviço deve ser concluída rapidamente.

- **Monitorização da rubrica de replicação**

  - Esta tarefa apenas se exibe no local da administração central e nos locais primários infantis.
  - Dependente do SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Deve completar rapidamente.

- **Atualizar pacote de pré-produção do gestor de configuração do cliente**

  - Esta tarefa exibe mesmo quando a pré-produção do cliente (também chamada de pilotagem de clientes) não está ativada para utilização.
  - Só começa quando todos os sites da hierarquia terminam a instalação da atualização.

- **Atualizar a pasta do Cliente no Servidor do Site**

  - Esta tarefa não é apresentada se utilizar o cliente na pré-produção.  
  - Deve completar rapidamente.

- **Atualizar pacote de cliente de gestor de configuração**

  - Esta tarefa não é apresentada se utilizar o cliente na pré-produção.  
  - Só termina depois de todos os sites instalarem a atualização.  

- **Ligando as funcionalidades**

  - Esta tarefa exibe apenas no local de topo da hierarquia.
  - Só começa quando todos os sites da hierarquia terminam a instalação da atualização.
  - Não são apresentadas características individuais.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  

Quando a instalação de uma atualização falhar, reveja os comentários na consola para identificar resoluções de avisos e erros. Para mais detalhes, consulte o **registo ConfigMgrPrereq** no servidor do site. Antes de voltar a tentar a instalação de uma atualização, tem de corrigir erros e corrigir avisos.  

> [!TIP]  
> Se uma atualização tiver problemas em descarregar ou replicar, utilize a ferramenta de [reset da atualização](update-reset-tool.md).  

Quando estiver pronto para voltar a tentar a instalação de uma atualização, selecione a atualização falhada e, em seguida, escolha uma opção aplicável. O comportamento de retry de instalação da atualização depende do nó onde iniciar a retry, e da opção de retry que utiliza.  

### <a name="retry-installation-for-the-hierarchy"></a>Instalação de retry para a hierarquia

Retry a instalação de uma atualização para toda a hierarquia quando essa atualização estiver num dos seguintes estados:  

- As verificações pré-requisitos foram passadas com um ou mais avisos, e a opção de ignorar os avisos de verificação pré-requisito não foi definida no Assistente de Atualização. (O valor da atualização para ignorar o **aviso prereq** nas **atualizações e** no nó de manutenção é **nº .)**

- Falha no pré-requisito

- Falha na instalação  

- Falha na replicação do conteúdo para o site

Vá ao espaço de trabalho da **Administração** e selecione as Atualizações e o nó **de Manutenção.** Selecione a atualização e, em seguida, escolha uma das seguintes opções:  

- **Retry**: Quando **voltar** a tentar **de Atualizações e Manutenção,** a instalação da atualização recomeça e ignora automaticamente as advertências pré-requisitos. Se a replicação de conteúdo falhou anteriormente, o conteúdo da atualização volta a ser replicado.  

- **Ignore as advertências pré-requisitos**: Se a instalação da atualização parar devido a um aviso, pode então escolher **ignorar avisos pré-requisitos**. Esta ação permite que a instalação da atualização continue após alguns minutos, e utiliza a opção de ignorar avisos pré-requisitos.

### <a name="retry-installation-for-the-site"></a>Instalação de retry para o local

Retry a instalação de uma atualização num local específico quando essa atualização estiver num dos seguintes estados:  

- As verificações pré-requisitos foram passadas com um ou mais avisos, e a opção de ignorar os avisos de verificação pré-requisito não foi definida no Assistente de Atualização. (O valor das atualizações para **o Aviso Prereq Ignore** nas Atualizações e no nó de manutenção é o **nº .)**  

- Falha no pré-requisito

- Falha na instalação

Vá ao espaço de trabalho **de Monitorização** e selecione o nó do Estado de Manutenção do **Local.** Selecione a atualização e, em seguida, escolha uma das seguintes opções:  

- **Retry**: Quando voltar a **tentar** o Estado de Manutenção do **Local,** reinicia a instalação da atualização apenas nesse local. Ao contrário de executar **Retry** a partir das Atualizações e do nó **de Manutenção,** este retry não ignora avisos pré-requisitos.  

- **Ignore as advertências pré-requisitos**: Se a instalação da atualização parar devido a um aviso, pode então selecionar **ignorar avisos pré-requisitos**. Esta ação permite que a instalação da atualização continue após alguns minutos, e utiliza a opção de ignorar avisos pré-requisitos.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Após uma site instalar uma atualização  

Após as atualizações do site, reveja a lista de verificação pós-actualização para a versão aplicável:  

- [Lista de verificação pós-atualização para a versão 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Lista de verificação pós-actualização para a versão 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Lista de verificação pós-actualização para a versão 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Lista de verificação pós-actualização para a versão 1902](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  

Quando uma atualização inclui uma ou mais funcionalidades opcionais, tem a oportunidade de ativar essas funcionalidades na sua hierarquia. Ative as funcionalidades quando a atualização se instalar ou volte à consola mais tarde para ativar as funcionalidades opcionais.

Para visualizar as funcionalidades disponíveis e o seu estado, na consola vá para o espaço de trabalho **da Administração,** expandir **Atualizações e Manutenção,** e selecionar o nó **de Funcionalidades.**

Quando uma funcionalidade não é opcional, é instalada automaticamente. Não aparece no nó **features.**  

> [!Important]  
> Numa hierarquia multi-site, ative funcionalidades opcionais ou de pré-lançamento apenas a partir do site da administração central. Este comportamento garante que não há conflitos em toda a hierarquia. <!--507197-->  

Quando ativar uma nova funcionalidade ou funcionalidade de pré-lançamento, o gestor de hierarquia do Gestor de Configuração (HMAN) deve processar a alteração antes que essa funcionalidade fique disponível. O processamento da mudança é muitas vezes imediato. Dependendo do ciclo de processamento de HMAN, pode levar até 30 minutos para ser concluído. Depois de processada a alteração, reinicie a consola antes de utilizar a funcionalidade.

Começando na versão 2002,<!--5834830--> quando novas funcionalidades baseadas na nuvem estiverem disponíveis no centro de administração do Microsoft Endpoint Manager, ou outros serviços de cloud anexados para a instalação do Gestor de Configuração no local, pode agora optar por estas novas funcionalidades na consola Do Gestor de Configuração.

### <a name="list-of-optional-features"></a>Lista de funcionalidades opcionais

As seguintes funcionalidades são opcionais na versão mais recente do Gestor de Configuração:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Gestão do BitLocker](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Sincronizar os resultados da adesão à coleção para o Azure Ative Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Descoberta do grupo de utilizadores do Diretório Ativo Azure](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Grupos de candidatura](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Debugger de sequência de tarefas](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Gestor de conversão de pacotes](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Aplicativos de clientes para dispositivos cogeridos](../../../comanage/workloads.md#client-apps) (anteriormente conhecidos como *aplicativos Móveis para dispositivos cogeridos)* <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Atualizações de software de terceiros](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Aprovar pedidos de pedido para utilizadores por dispositivo](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Criar e executar scripts](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Atualizações do condutor de superfície](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Gateway de gestão da cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [PFX criar](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Conector Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Política de Exploração do Windows Defender](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN para Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Manutenção de uma coleção consciente do cluster (grupos servidor)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md) (anteriormente conhecido como *Passport for Work)* <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Para obter mais informações sobre funcionalidades que requeiram o consentimento para ativar, consulte [as funcionalidades de pré-lançamento](pre-release-features.md).  
>
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo técnico de pré-visualização, consulte [A Pré-visualização Técnica](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações

O ramo atual inclui funcionalidades de pré-lançamento para testes precoces num ambiente de produção. Para mais informações, consulte [as funcionalidades de pré-lançamento](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Perguntas frequentes

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Por que não vejo certas atualizações na minha consola?

Se não encontrar uma atualização específica na sua consola depois de uma sincronização bem sucedida com o serviço de nuvem da Microsoft, este comportamento pode ser devido a uma das seguintes razões:  

- A atualização requer uma configuração que a sua infraestrutura não utiliza, ou a versão atual do produto não preenche um pré-requisito para receber a atualização.  

    Se achar que tem as configurações e pré-requisitos necessários para uma atualização em falta, confirme que o ponto de ligação ao serviço está em modo online. Em seguida, utilize a opção **'Verificar actualizações'** nas **atualizações e** no nó de manutenção para forçar uma verificação. Se o seu ponto de ligação de serviço estiver no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com o serviço de nuvem.  

- A sua conta carece das permissões corretas de administração baseadas em funções para visualizar atualizações na consola 'Gestor de Configuração'. Para mais informações, consulte [Permissões para gerir atualizações](#assign-permissions-to-view-and-manage-updates-and-features).  
