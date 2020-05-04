---
title: Gerir o Windows como um Serviço
titleSuffix: Configuration Manager
description: Veja o estado do Windows como um Serviço (WaaS) usando o Gestor de Configuração, crie planos de manutenção para formar anéis de implementação e veja alertas quando os clientes do Windows 10 estão perto do fim do suporte.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710840"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Gerir o Windows como um serviço usando o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

No 'Gestor de Configuração', pode ver o estado do Windows como um Serviço (WaaS) no seu ambiente. Crie planos de manutenção para formar anéis de implementação e certifique-se de que os sistemas Windows 10 são mantidos atualizados quando novas construções forem lançadas. Também pode ver alertas quando os clientes do Windows 10 estão perto do fim do suporte para a sua construção semestral do Canal.

Para mais informações sobre as opções de manutenção do Windows 10, consulte a [visão geral do Windows como um Serviço](/windows/deployment/update/waas-overview#servicing-channels).

Utilize as seguintes secções para gerir o Windows como um serviço.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a>Pré-requisitos

Para ver os dados no painel de assistência do Windows 10, deve fazer as seguintes ações:

- Os computadores windows 10 devem utilizar atualizações de software do Gestor de Configuração com os Serviços de Atualização do Servidor do Windows (WSUS) para a gestão da atualização de software. Quando os computadores utilizam o Windows Update para O Negócio (ou Windows Insiders) para a gestão de atualizações de software, o computador não é avaliado nos planos de manutenção do Windows 10. Para obter mais informações, veja [Integration with Windows Update for Business in Windows 10 (Integração com o Windows Update for Business no Windows 10)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Utilize uma versão WSUS suportada:
  - WSUS 10.0.14393 (função no Windows Server 2016)
  - WSUS 10.0.17763 (função no Windows Server 2019) (Requer o Gestor de Configuração 1810 ou mais tarde)
  - WSUS 6.2 e 6.3 (função no Windows Server 2012 e Windows Server 2012 R2)
    - [KB 3095113 e KB 3159706 (ou uma atualização equivalente) devem ser instalados](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) nos WSUS 6.2 e 6.3.

- Ative a Deteção Heartbeat. Os dados apresentados no dashboard de manutenção do Windows 10 são encontrados através da deteção. Para obter mais informações, veja [Configure Heartbeat Discovery (Configurar a Deteção de Heartbeat)](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    O canal seguinte do Windows 10 e a informação de construção são descobertos e armazenados nos seguintes atributos:  

    - **Ramo de prontidão**do sistema operativo : Especifica o canal do sistema operativo. Por exemplo, **0** = Canal Semi-Anual - Direcionado (não adia atualizações), **1** = Canal Semi-Anual (atualizações de adiamento), **2** = Canal de Manutenção a Longo Prazo (LTSC)

    - **Construção do sistema operativo**: Especifica a construção do sistema operativo. Por exemplo, **10.0.10240** (RTM) ou **10.0.10586** (versão 1511)

- O ponto de ligação de serviço deve ser instalado e configurado para o modo de **ligação on-line persistente** para ver os dados no painel de assistência do Windows 10. Quando estiver em modo offline, não vê atualizações de dados no painel de instrumentos até obter atualizações de manutenção do Gestor de Configuração. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- O Internet Explorer 9 ou posteriormente deve ser instalado no computador que executa a consola 'Gestor de Configuração'.

- As atualizações de software têm de ser configuradas e sincronizadas. Selecione a classificação de **Upgrades** e sincronize as atualizações de software antes de quaisquer atualizações de funcionalidades do Windows 10 estarem disponíveis na consola 'Gestor de Configuração'. Para mais informações, consulte [Prepare-se para a gestão](../../sum/get-started/prepare-for-software-updates-management.md)de atualizações de software.

- A partir da versão 1902 do Gestor de Configuração, verifique a prioridade de **linha de especificação para atualizações de funcionalidades** [para](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) garantir que é apropriado para o seu ambiente.

- A partir da versão 1906 do Gestor de Configuração, verifique a [atualização](../../core/clients/deploy/about-client-settings.md#bkmk_du) **dinâmica do Enable para atualizações** de funcionalidades para garantir que é apropriado para o seu ambiente. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a>Painel de assistência do Windows 10

O dashboard de manutenção do Windows 10 fornece informações sobre computadores Windows 10 no seu ambiente, planos de manutenção ativos, informações de compatibilidade, etc. Os dados no dashboard de manutenção do Windows 10 estão dependentes de ter um Ponto de Ligação de Serviço instalado. O dashboard tem os seguintes mosaicos:

- Azulejo de **utilização do Windows 10**: Proporciona uma avaria nas construções públicas do Windows 10. As construções do Windows Insiders estão listadas como **outras,** bem como quaisquer construções que ainda não sejam conhecidas do seu site. O ponto de ligação ao serviço descarrega metadados que o informam sobre as construções do Windows, e depois estes dados são comparados com os dados da descoberta.

- **Azulejo do Windows 10 Rings**: Proporciona uma avaria do Windows 10 por canal e estado de prontidão. O segmento LTSC inclui todas as versões LTSC. O primeiro azulejo decompõe as versões específicas, por exemplo, o Windows 10 LTSC 2015.

- **Criar azulejos do Plano de Serviço**: Fornece uma forma rápida de criar um plano de manutenção. Especifica o nome, a recolha (apenas exibe as 10 melhores coleções por tamanho, a menor primeira), o pacote de implementação (apenas exibe os 10 pacotes mais recentes modificados) e estado de prontidão. Os valores predefinidos são utilizados para as outras definições. Clique em **Definições Avançadas** para iniciar o assistente do Plano de Manutenção Criar, onde pode configurar todas as definições do plano de serviço.

- **Mosaico Expirado**: mostra a percentagem de dispositivos que estão numa compilação do Windows 10 que passou o respetivo final de vida. O Gestor de Configuração determina a percentagem dos metadados que o Service Connection Point descarrega e compara-a com os dados de descoberta. Uma construção que já passou do seu fim de vida já não está a receber atualizações acumuladas mensais, que incluem atualizações de segurança. Os computadores nesta categoria devem ser atualizados para a próxima versão de compilação. O Gestor de Configuração completa até ao número completo seguinte. Por exemplo, se tiver 10.000 computadores e apenas um numa construção expirada, o azulejo apresenta 1%.

- **Mosaico Expirar em Breve**: mostra a percentagem de computadores que estão numa compilação que está perto do final de vida (dentro de, aproximadamente, quatro meses), semelhante ao mosaico **Expirado** . O Gestor de Configuração completa até ao número completo seguinte.

- **Mosaico Alertas**: mostra os alertas ativos.

- Azulejo de **monitorização**do plano de serviço : Mostrar planos de manutenção que criou e um gráfico da conformidade para cada um. Este azulejo dá-lhe uma visão geral rápida do estado atual das implementações do plano de manutenção. Se um anel de implementação anterior for ao encontro das suas expectativas em termos de conformidade, poderá selecionar um plano de manutenção posterior (anel de implementação) e clicar em **Implementar Agora** em vez de aguardar que as regras do plano de manutenção sejam acionadas automaticamente.

- O **Windows 10 Constrói azulejos**: O display é uma linha de tempo de imagem fixa que lhe fornece uma visão geral das construções do Windows 10 que são atualmente lançadas e que lhe dá uma ideia geral de quando constrói a transição para diferentes estados. Este azulejo foi removido a partir da versão 1902 do Gestor de Configuração, uma vez que são oferecidas informações mais detalhadas no painel de [instrumentos](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md)do Ciclo de Vida do Produto . <!--3446861-->

> [!IMPORTANT]
> As informações mostradas no dashboard de manutenção do Windows 10 (por exemplo, o ciclo de vida de suporte para as versões do Windows 10) são fornecidas para sua comodidade e apenas para utilização interna na empresa. Não deverá confiar apenas nestas informações para confirmar a compatibilidade de atualização. Certifique-se de que verifica a exatidão das informações que lhe são fornecidas.

## <a name="drill-through-required-updates"></a>Perfurar através de atualizações necessárias
<!--4224414-->
*(Introduzido na versão 1906)*

Pode perfurar as estatísticas de conformidade para ver quais os dispositivos que requerem uma atualização específica da funcionalidade do Windows 10. Para ver a lista do dispositivo, é necessário permissão para visualizar atualizações e as coleções a que os dispositivos pertencem. Para aprofundar a lista do dispositivo:

1. Vá à **Biblioteca** > de Software**Windows 10 a manutenção** > de**todas as atualizações do Windows 10**.
1. Selecione qualquer atualização que seja necessária por pelo menos um dispositivo.
1. Olhe para o separador **Resumo** e encontre o gráfico de tartes em **estatísticas.**
1. Selecione a hiperligação necessária para **ver** junto ao gráfico de tartes para aprofundar a lista do dispositivo.
1. Esta ação leva-o a um nó temporário em **Dispositivos** onde pode ver os dispositivos que necessitam da atualização. Você também pode tomar ações para o nó, como criar uma nova coleção a partir da lista.

## <a name="servicing-plan-workflow"></a>Fluxo de trabalho do plano de manutenção

Os planos de manutenção do Windows 10 no Gestor de Configuração são muito parecidos com as regras de implementação automática para atualizações de software. Cria um plano de manutenção com os seguintes critérios que o Gestor de Configuração avalia:

- **Classificação Atualizações**: só são avaliadas as atualizações que estão na classificação **Atualizações** .

- **Estado de preparação**: o estado de preparação definido no plano de manutenção é comparado ao estado de preparação da atualização. Os metadados para a atualização são obtidos quando o ponto de ligação de serviço verifica a existência de atualizações.

- **Diferimento por tempo**: o número de dias que especificou para **Quantos dias depois de a Microsoft ter publicado uma nova atualização gostaria de aguardar antes de implementar no seu ambiente** no plano de manutenção. Se a data atual for posterior à data de lançamento mais o número configurado de dias, o Gestor de Configuração avalia se deve incluir uma atualização na implementação.

  Quando uma atualização cumpre os critérios, o plano de manutenção adiciona a atualização ao pacote de implementação, distribui o pacote por pontos de distribuição e implementa a atualização na coleção com base nas definições configuradas no plano de manutenção. Pode monitorizar as implementações no mosaico Monitorização do Plano de Serviço no Dashboard de Manutenção do Windows 10. Para mais informações, consulte [as atualizações](../../sum/deploy-use/monitor-software-updates.md)de software do Monitor .

> [!NOTE]
> **O Windows 10, a versão 1903 e mais tarde** foi adicionado ao Microsoft Update como seu próprio produto, em vez de fazer parte do produto **do Windows 10** como versões anteriores. Esta alteração fez com que fizesse uma série de passos manuais para garantir que os seus clientes vêem estas atualizações. Ajudamos a reduzir o número de passos manuais que tem de tomar para o novo produto na versão 1906 do Gestor de Configuração. Para mais informações, consulte [a Configuração de produtos para versões do Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Plano de manutenção do Windows 10

Ao implementar o Canal Semi-Anual do Windows 10, pode criar um ou mais planos de manutenção para definir os anéis de implementação que deseja no seu ambiente e, em seguida, monitorá-los no painel de assistência do Windows 10. Os planos de serviço utilizam apenas a classificação de atualizações de software **Atualizações** e não atualizações cumulativas para o Windows 10. Para essas atualizações, ainda precisa de ser implementado utilizando o fluxo de trabalho das atualizações de software. A experiência do utilizador final com um plano de manutenção é idêntica à das atualizações de software, incluindo as definições configuradas no plano de manutenção.  

> [!NOTE]
> Pode utilizar uma sequência de tarefas para implementar uma atualização para cada compilação do Windows 10, mas requer mais trabalho manual. Terá de importar os ficheiros de origem atualizados como um pacote de atualização do sistema operativo e, em seguida, criar e implementar a sequência de tarefas para o conjunto adequado de computadores. No entanto, uma sequência de tarefas fornece opções personalizadas adicionais, tais como as ações de pré-implementação e pós-implementação.

Pode criar um plano de manutenção básico a partir do dashboard de manutenção do Windows 10. Depois de especificar o nome, a recolha (apenas apresenta as 10 coleções top 10 por tamanho, a menor primeira), pacote de implementação (apenas apresenta os 10 pacotes top por mais recentemente modificados) e estado de prontidão, O Gestor de Configuração cria o plano de manutenção com valores predefinidos para as outras definições. Também pode iniciar o assistente Criar Plano de Manutenção para configurar todas as definições. Utilize o procedimento seguinte para criar um plano de manutenção utilizando o assistente Criar Plano de Manutenção.  

> [!NOTE]  
> Você pode gerir o comportamento para implementações de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha o objetivo **Obrigatório** que implemente o Windows 10 é considerada uma implementação de alto risco. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>Para criar um plano de manutenção do Windows 10

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.

1. Na área de trabalho Biblioteca de Software, expanda **Manutenção do Windows 10**e, em seguida, clique em **Planos de Manutenção**.

1. No separador **Home page** , no grupo **Criar** , clique em **Criar Plano de Manutenção**. O assistente Criar Plano de Manutenção abre.

1. Na página **Geral,** configure as seguintes definições:

    - **Nome**: especifique o nome do plano de manutenção. O nome deve ser único, ajudar a descrever o objetivo da regra, e identificá-lo de outros no site do Gestor de Configuração.

    - **Descrição**: especifique uma descrição para o plano de manutenção. A descrição deve fornecer uma visão geral do plano de manutenção e de quaisquer outras informações relevantes que ajudem a identificar e diferenciar o plano entre outros no site do Gestor de Configuração. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.

1. Na página do Plano de Manutenção, especifique a Coleção do **Alvo**. Os membros da coleção recebem as atualizações do Windows 10 definidas no plano de manutenção.

    - Ao implementar uma implementação de alto risco, como um plano de manutenção, a janela **Select Collection** exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site.

    - As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não se pode selecionar uma coleção incorporada, como **a All Systems**. Desmarque **as coleções Hide com um membro contam mais do que a configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que contenham menos clientes do que o tamanho máximo configurado. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - As definições de verificação da implementação são baseadas na associação atual da coleção. Depois de implementar o plano de manutenção, a associação de recolha não é reavaliada para as definições de implementação de alto risco.

      - Por exemplo, digamos que definiu o **tamanho padrão** para 100 e o **tamanho máximo** para 1000. Quando criar uma implementação de alto risco, a janela **Select Collection** apenas apresentará coleções que contenham menos de 100 clientes. Se limpar as coleções Hide com uma contagem de **membros maior do que a configuração de tamanho mínimo do site,** a janela apresentará coleções que contenham menos de 1000 clientes.  
      Quando seleciona uma coleção que contenha uma função no local, aplicam-se os seguintes critérios:
        - Se a coleção contiver um servidor de sistema de site e nas definições de verificação de implementação configurar para bloquear coleções com servidores do sistema do site, então ocorre um erro e não pode continuar.
        - Se a coleção contiver um servidor do sistema de sites e nas definições de verificação da implementação configurar a apresentação de um aviso caso as coleções incluam servidores do sistema de sites, se a coleção ultrapassar o valor do tamanho predefinido ou se a coleção contiver um servidor, o Assistente de Implementação de Software apresentará um aviso de alto risco. Tem de aceitar criar uma implementação de alto risco e é criada uma mensagem de estado de auditoria.

1. Na página Anel de Implementação, configure as seguintes definições:

   - **Especifique o estado de prontidão do Windows a que este plano**de manutenção deve ser aplicado : Selecione uma das seguintes opções:

      - **Canal Semi-Anual (Direcionado)**: Neste modelo de manutenção, as atualizações de funcionalidades estão disponíveis assim que a Microsoft as lançar.

      - **Canal semi-anual**: Este canal de manutenção é normalmente utilizado para uma ampla implantação. Os clientes do Windows 10 no Canal SemEstanual recebem a mesma construção do Windows 10 que os dispositivos no canal direcionado, apenas mais tarde.

        Para mais informações sobre os canais de manutenção e quais as melhores opções para si, consulte os [canais de manutenção.](/windows/deployment/update/waas-overview#servicing-channels)

   - **Quantos dias depois**de a Microsoft ter publicado uma nova atualização gostaria de esperar antes de ser implementado no seu ambiente : Se a data atual for após a data de lançamento mais o número de dias que configura para esta definição, o ConfigurManager avalia se deve incluir uma atualização na implementação.

1. Na página Upgrades, configure os critérios de pesquisa para filtrar as atualizações que são adicionadas ao plano de serviço. Apenas são adicionadas atualizações que satisfaçam os critérios especificados à implantação associada. Estão disponíveis os seguintes filtros de propriedade: <!--3098809, 3113836, 3204570 -->

   - **Arquitetura** (a partir da versão 1810)
   - **Idioma**
   - **Categoria de Produto** (a partir da versão 1810)
   - **Necessário**
      > [!IMPORTANT]
      > Recomendamos que, como parte dos seus critérios de pesquisa, detete te o campo **Obrigatório** com um valor de **>=1**. A utilização destecritério garante que apenas são adicionadas atualizações aplicáveis ao plano de serviço.
   - **Substituído** (a partir da versão 1810)
   - **Título**

    Clique em **Pré-visualizar** para ver as atualizações que cumprem os critérios especificados.

1. Na página Agenda de Implementação, configure as seguintes definições:

   - **Avaliação do horário**: Especifique se o Gestor de Configuração avalia os prazos de tempo e de tempo de instalação disponíveis utilizando a UTC ou a hora local do computador que executa a consola do Gestor de Configuração.

       > [!NOTE]
       > Quando selecionar a hora local e, em seguida, selecionar o **mais rapidamente possível** para o prazo de tempo ou **instalação**disponível do **Software,** o tempo atual no computador que executa a consola do Gestor de Configuração é utilizado para avaliar quando as atualizações estão disponíveis ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.

   - **Hora de disponibilização do software**: selecione uma das seguintes definições para especificar o momento em que as atualizações de software são disponibilizadas aos clientes:

        - **Logo que possível**: selecione esta definição para disponibilizar as atualizações de software incluídas na implementação aos computadores cliente o mais rapidamente possível. Quando cria a implementação com esta definição selecionada, o Gestor de Configuração atualiza a política do cliente. Depois, no próximo ciclo de sondagens de política de clientes, os clientes ficam cientes da implementação e podem obter as atualizações disponíveis para instalação.

        - **Hora específica**: selecione esta definição para disponibilizar as atualizações de software incluídas na implementação aos computadores cliente numa data e hora específicas. Quando cria a implementação com esta definição ativada, o Gestor de Configuração atualiza a política do cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software na implementação só estão disponíveis para instalação após a data e hora configuradas.

   - **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações do software na implementação:

        - **Logo que possível**: selecione esta definição para instalar automaticamente as atualizações de software o mais rapidamente possível.

        - **Hora específica**: selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas. O Gestor de Configuração determina o prazo para instalar atualizações de software adicionando o intervalo de **tempo específico** configurado ao **tempo disponível**do Software .

           > [!NOTE]
           > A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações na implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.
           >
           > Pode configurar a definição de cliente **Agente do Computador****Desativar a aleatoriedade de prazos** para desativar o atraso da aleatoriedade da instalação para as atualizações necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - Atrasar a **execução desta implementação de acordo com as preferências do utilizador, até ao período**de carência definido no cliente : Selecione esta opção para honrar o período Grace para a execução após a definição do cliente do prazo de [ **implementação (horas).** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours)

1. Na página Experiência de Utilizador, configure as seguintes definições:  

    - **Notificações do utilizador**: especifique se pretende apresentar a notificação de atualizações do Centro de Software no computador cliente à **Hora de disponibilização do software** configurada e se quer apresentar as notificações de utilizador nos computadores cliente.

    - **Comportamento do prazo**: especifique o comportamento a adotar quando é atingido o prazo de implementação da atualização. Especifique se pretende instalar as atualizações na implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Comportamento do reinício do dispositivo**: especifique se pretende suprimir um reinício do sistema nos servidores e estações de trabalho após as atualizações serem instaladas e se é necessário reiniciar o sistema para concluir a instalação.

    - **Processamento do filtro de escrita para dispositivos Windows Embedded**: ao implementar atualizações em dispositivos Windows Embedded que tenham um filtro de escrita ativado, poderá especificar a instalação da atualização na sobreposição temporária e optar por confirmar as alterações mais tarde ou por confirmá-las no prazo da instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.
        - Ao implementar uma atualização num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.

    - **Software atualiza comportamento de reavaliação de implementação após o reinício**: Para forçar outro ciclo de avaliação de implementação de atualizações após o reinício, selecione a opção **Se qualquer atualização nesta implementação necessitar de um reinício do sistema, executar**o ciclo de avaliação de implementação de atualizações após o reinício .

1. Na página do Pacote de Implementação, selecione um pacote de implementação existente, sem pacote de implementação ou configure as seguintes definições para criar um novo pacote de implementação:

    1. **Nome**: especifique o nome do pacote de implementação. Este nome deve ser único e descreve o conteúdo do pacote. Está limitado a 50 caracteres.

    1. **Descrição**: especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição está limitada a 127 carateres.

    1. **Origem do pacote**: especifica a localização dos ficheiros de origem de atualização de software. Digite um caminho de rede para a localização de origem, por **Browse** exemplo, ** \\o caminho\\\\**do nome de partilha do servidor \, ou clique em Navegar para encontrar a localização da rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de continuar na página seguinte.
        - A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.
        - Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deve restringir cuidadosamente o acesso ao local de descarregamento para reduzir o risco de os atacantes adulterarem os ficheiros de origem da atualização de software.
        - Pode alterar a localização da fonte do pacote nas propriedades do pacote de implementação após o Gestor de Configuração criar o pacote de implementação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.

    1. **Prioridade de envio**: especifique a prioridade de envio para o pacote de implementação. O Gestor de Configuração utiliza a prioridade de envio do pacote de implementação quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem prioritária: Alto, Médio ou Baixo. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver atrasos, o pacote processa imediatamente, independentemente da sua prioridade.

    1. **Ativar a replicação diferencial binária**: Ative esta opção se pretender utilizar a replicação diferencial binária.

1. Na página pontos de distribuição, especifique os pontos de distribuição ou os grupos de pontos de distribuição que acolhem os ficheiros de atualização. Para obter mais informações sobre pontos de distribuição, consulte [Configure um ponto](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)de distribuição .

    > [!NOTE]
    > Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

1. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização a partir da Internet ou da rede local. Configure as seguintes definições:

    - **Transferir as atualizações de software a partir da Internet**: selecione esta definição para transferir as atualizações a partir de uma localização especificada na Internet. Esta definição está ativada por predefinição.

    - **Transferir atualizações de software a partir de uma localização na rede local**: selecione esta definição para transferir as atualizações a partir de um diretório local ou de uma pasta partilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador que disponha de acesso à Internet poderá transferir provisoriamente as atualizações e armazená-las numa localização da rede local que esteja acessível ao computador que executa o assistente.

1. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações selecionadas. As atualizações só são descarregadas se estiverem disponíveis nos idiomas selecionados. As atualizações que não são específicas do idioma são sempre descarregadas. Por padrão, o assistente seleciona os idiomas configurados nas propriedades do ponto de atualização do software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Quando seleciona apenas idiomas que não são suportados por uma atualização, o download falha na atualização.

1. Na página Resumo, reveja as definições e clique em **Seguinte** para criar o plano de manutenção.  

Depois de completar o assistente, o plano de manutenção vai funcionar. Adiciona as atualizações que cumprem os critérios especificados a um grupo de atualização de software, descarrega as atualizações para a biblioteca de conteúdos no servidor do site, distribui as atualizações para os pontos de distribuição configurados e, em seguida, implementa o grupo de atualização de software para os clientes na coleção de alvos.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Modificar um plano de manutenção

Depois de criar um plano básico de manutenção a partir do painel de assistência do Windows 10 ou de alterar as definições para um plano de manutenção existente, pode ir às propriedades para o plano de manutenção.

> [!NOTE]
> Pode configurar as definições nas propriedades para o plano de manutenção que não estão disponíveis no assistente quando criar o plano de manutenção. O assistente utiliza definições predefinidas para as seguintes definições: descarregamento de definições, definições de implementação e alertas.  

Utilize o procedimento seguinte para modificar as propriedades de um plano de manutenção. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Para modificar as propriedades de um plano de manutenção

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.

1. No espaço de trabalho da Biblioteca de Software, expanda a **manutenção do Windows 10,** clique em **Planos de Manutenção**e, em seguida, selecione o plano de manutenção que pretende modificar.

1. No separador **Home page** , clique em **Propriedades** para abrir as propriedades do plano de manutenção selecionado.

    As seguintes definições estão disponíveis nas propriedades do plano de manutenção que não foram configuradas no assistente:

    **Definições de implementação**: No separador Definições de Implementação, configure as seguintes definições:

    - **Utilizar a Reativação por LAN para reativar os clientes para as implementações necessárias**: especifique se pretende ativar a Reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software no âmbito da implementação. Todos os computadores que estejam em modo de sono no prazo de instalação são despertados para que a instalação da atualização de software possa iniciar. Os clientes que estão em modo de sono que não necessitam de atualizações de software na implementação não foram iniciados. Por predefinição, esta definição não está ativada.

        > [!WARNING]
        > Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.

    - **Nível de detalhe**: especifique o nível de detalhe das mensagens de estado que são enviadas pelos computadores cliente.

    **Baixar Definições**: No separador Definições de Descarregamento, configure as seguintes definições:

    - Especifique se o cliente descarrega e instala as atualizações de software quando um cliente está ligado a uma rede lenta ou se está a utilizar uma localização de conteúdo de recuo.

    - Especifique se deve fazer o download do cliente e instalar as atualizações de software a partir de um ponto de distribuição de recuo quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferido.

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para obter mais informações sobre branchCache, consulte [conceitos fundamentais para a gestão de conteúdos.](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)

    - Especifique se os clientes descarregam atualizações de software a partir do Microsoft Update se as atualizações de software não estiverem disponíveis em pontos de distribuição.
        > [!IMPORTANT]
        > Não utilize esta definição para atualizações de assistência ao Windows 10. O Gestor de Configuração (pelo menos através da versão 1610) não consegue descarregar as atualizações de Manutenção do Windows 10 a partir do Microsoft Update.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.

    **Alertas**: No separador Alertas, configure como o Gestor de Configuração e o Gestor de Operações do Centro de Sistemageram alertas para esta implementação.
    - Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .

## <a name="next-steps"></a>Passos seguintes

Para mais informações, consulte os [Fundamentos do Gestor de Configuração como um serviço e o Windows como um serviço](../../core/understand/configuration-manager-and-windows-as-service.md).
