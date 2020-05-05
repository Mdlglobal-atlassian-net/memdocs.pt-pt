---
title: Migrar conteúdo
titleSuffix: Configuration Manager
description: Utilize pontos de distribuição para gerir o conteúdo enquanto migra dados para uma hierarquia de destino de destino de ramificação atual do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719688"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Planeie uma estratégia de migração de implementação de conteúdos no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Enquanto migra ativamente os dados para uma hierarquia de destino de destino de sucursal do Gestor de Configuração, os clientes do Gestor de Configuração nas hierarquias de origem e destino podem manter o acesso aos conteúdos que implementou na hierarquia de origem. Também pode usar a migração para atualizar ou reatribuir pontos de distribuição da hierarquia de origem para se tornar pontos de distribuição na hierarquia de destino. Quando partilha e atualiza ou reatribui um ponto de distribuição, esta estratégia pode ajudar a evitar a reimplementação de conteúdo em novos servidores na hierarquia de destino para os clientes migrados.  

Apesar de poder recriar e distribuir conteúdo na hierarquia de destino, também pode utilizar as seguintes opções para gerir este conteúdo:  

-   Partilhar os pontos de distribuição na hierarquia de origem com clientes da hierarquia de destino.  

-   Atualize os pontos de distribuição autónomos do Gestor de Configuração 2007 ou o Gestor de Configuração 2007 na hierarquia de origem para se tornarem pontos de distribuição na hierarquia de destino.  

-   Reatribuir pontos de distribuição de uma hierarquia de fonte do Gestor de Configuração para um site na hierarquia de destino.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Partilhar pontos de distribuição entre hierarquias de origem e destino  
Durante a migração, pode partilhar pontos de distribuição de uma hierarquia de origem com a hierarquia de destino. Pode utilizar pontos de distribuição partilhados para disponibilizar imediatamente conteúdo que tenha migrado de uma hierarquia de origem a clientes da hierarquia de destino, sem ter de recriar esse conteúdo e distribui-lo pelos novos pontos de distribuição na hierarquia de destino. Quando os clientes da hierarquia de destino pedirem conteúdo implementado em pontos de distribuição que partilhou, os pontos de distribuição partilhados poderão ser oferecidos aos clientes como localizações de conteúdo válidas.  

 Além de ser um local de conteúdo válido para os clientes na hierarquia de destino enquanto a migração da hierarquia de origem permanece ativa, é possível atualizar ou reatribuir um ponto de distribuição para a hierarquia de destino. Pode atualizar os pontos de distribuição partilhados do Gestor de Configuração 2007 e reatribuir os pontos de distribuição partilhados do System Center 2012. Quando atualiza ou reatribui um ponto de distribuição partilhado, este é removido da hierarquia de origem e passa a ser um ponto de distribuição da hierarquia de destino. Depois de atualizar ou reatribuir um ponto de distribuição partilhado, pode continuar a utilizá-lo na hierarquia de destino após a conclusão da migração a partir da hierarquia de origem. Para saber mais sobre como atualizar um ponto de distribuição partilhado, consulte [Plan to upgrade Configuration Manager 2007 pontos](#Planning_to_Upgrade_DPs)de distribuição partilhadas . Para saber mais sobre como reatribuir um ponto de distribuição partilhado, consulte Plan para [reatribuir pontos](#BKMK_ReassignDistPoint)de distribuição do Gestor de Configuração .  

 Pode optar por partilhar pontos de distribuição de qualquer site de origem da hierarquia de origem. Quando você partilha pontos de distribuição para um site de origem, os sites secundários para crianças são partilhados em cada ponto de distribuição de qualificação em cada local primário e em cada um dos locais primários. Para se qualificar para ser um ponto de distribuição partilhado, o servidor do sistema do site que acolhe o ponto de distribuição deve ser configurado com um nome de domínio totalmente qualificado (FQDN). Quaisquer pontos de distribuição que sejam criados com um nome NetBIOS são ignorados.  

> [!TIP]  
>  O Gestor de Configuração 2007 não requer que você configurar um FQDN para servidores do sistema do site.  

Utilize as informações seguintes para planear pontos de distribuição partilhados:  

-   Os pontos de distribuição que partilhar têm de cumprir os pré-requisitos para pontos de distribuição partilhados. Para mais informações sobre estes pré-requisitos, consulte [as configurações necessárias para a migração](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) em [pré-requisitos para a migração](../../core/migration/prerequisites-for-migration.md).  

-   A ação de partilha de ponto de distribuição é uma definição ao nível do site que partilha todos os pontos de distribuição elegíveis de um site de origem e de quaisquer sites secundários subordinados diretos. Não é possível selecionar pontos de distribuição individuais para partilhar quando ativa a partilha de pontos de distribuição.  

-   Os clientes da hierarquia de destino podem receber informações de localizações de conteúdo relativas a pacotes distribuídos aos pontos de distribuição partilhados a partir da hierarquia de origem. Para pontos de distribuição de uma hierarquia de fonte do Gestor de Configuração de 2007, isto inclui pontos de distribuição de filiais, pontos de distribuição em ações de servidores e pontos de distribuição padrão.  

    > [!WARNING]  
    >  Se alterar a hierarquia de origem, os pontos de distribuição partilhados a partir da hierarquia de origem original deixam de estar disponíveis e não será possível oferecê-los como localizações de conteúdo a clientes da hierarquia de destino. Se reconfigurar a migração para utilizar a hierarquia de origem original, os pontos de distribuição partilhados anteriormente serão restaurados como servidores de localização de conteúdo válidos.  

-   Quando migra um pacote alojado num ponto de distribuição partilhado, a versão do pacote tem de permanecer a mesma nas hierarquias de origem e de destino. Quando a versão de um pacote não é a mesma nas hierarquias de origem e de destino, os clientes da hierarquia de destino não conseguem obter esse conteúdo do ponto de distribuição partilhado. Consequentemente, se atualizar um pacote na hierarquia de origem, terá de migrar novamente os dados do pacote para que os clientes da hierarquia de destino possam obter esse conteúdo de um ponto de distribuição partilhado.  

    > [!NOTE]  
    >  Quando vê detalhes de um pacote que está hospedado num ponto de distribuição partilhado, o número de pacotes que exibem como **Pacotes Migrados Hospedados** no separador **Pontos** de Distribuição Partilhada do site de origem não é atualizado até que o próximo ciclo de recolha de dados esteja terminado.  

-   Pode ver pontos de distribuição partilhados e suas propriedades no nó da **Hierarquia Fonte** do espaço de trabalho da **Administração** na consola De Configuração Manager que se conecta à hierarquia de destino.  

-   Não é possível utilizar um ponto de distribuição partilhado a partir de uma hierarquia de origem do Gestor de Configuração de 2007 para hospedar pacotes para a Virtualização de Aplicações da Microsoft (App-V). Os pacotes de App-V têm de ser migrados e convertidos para serem utilizados pelos clientes na hierarquia de destino. No entanto, pode utilizar um ponto de distribuição partilhado a partir de um System Center 2012 Configuration Manager ou configuração de hierarquia de fonte de filial para hospedar pacotes App-V para clientes numa hierarquia de destino.  

-   Quando partilha um ponto de distribuição protegido de uma hierarquia de fonte do Gestor de Configuração de 2007, a hierarquia de destino cria um grupo de fronteiras que inclui as localizações de rede protegidadesse desse ponto de distribuição. Não se pode mudar este grupo de fronteiras na hierarquia do destino. No entanto, se alterar a informação de fronteira protegida para o ponto de distribuição na hierarquia de origem do Gestor de Configuração de 2007, essa mudança reflete-se na hierarquia de destino após o próximo ciclo de recolha de dados terminar.  

    > [!NOTE]  
    >  System Center 2012 Configuração Manager e Configuração Manager os sites de sucursais atuais usam o conceito de pontos de distribuição preferidos em vez de pontos de distribuição protegidos. Esta condição aplica-se apenas aos pontos de distribuição que são partilhados a partir de sites de origem do Gestor de Configuração de 2007.  

Os pontos de distribuição elegíveis não são visíveis na consola Do Gestor de Configuração antes de partilhar pontos de distribuição a partir de um site de origem. Depois de partilhar pontos de distribuição, apenas os pontos de distribuição partilhados com êxito são listados.  

Depois de ter partilhado pontos de distribuição, pode alterar a configuração de qualquer ponto de distribuição partilhado na hierarquia de origem. As alterações efetuadas à configuração de um ponto de distribuição são refletidas na hierarquia de destino após os ciclo de recolha de dados seguinte. Os pontos de distribuição que tenha atualizado para serem elegíveis para partilha são partilhados automaticamente, enquanto aqueles que já não são elegíveis deixam de ser partilhados. Por exemplo, pode ter um ponto de distribuição que não é configurado com uma intranet FQDN e não foi inicialmente partilhado com a hierarquia de destino. Depois de configurar o FQDN para esse ponto de distribuição, o próximo ciclo de recolha de dados identifica esta configuração, e o ponto de distribuição é então partilhado com a hierarquia de destino.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a>Plano para atualizar pontos de distribuição partilhadas do Gestor de Configuração 2007  
Quando se migra de uma hierarquia de origem do Gestor de Configuração de 2007, pode atualizar um ponto de distribuição partilhado para torná-lo um ponto de distribuição atual do Gestor de Configuração. Pode atualizar pontos de distribuição em locais primários e locais secundários. O processo de atualização remove o ponto de distribuição da hierarquia do Gestor de Configuração de 2007 e torna-o um servidor de sistema de site na hierarquia de destino. Este processo também copia o conteúdo existente que está no ponto de distribuição para uma nova localização no computador do ponto de distribuição. Em seguida, o processo de atualização modifica a cópia do conteúdo para criar o single instance store para utilização com a implementação de conteúdos na hierarquia de destino. Por isso, ao atualizar um ponto de distribuição, não é preciso redistribuir conteúdo migrado que foi hospedado no ponto de distribuição do Gestor de Configuração 2007.  

Depois de o Gestor de Configuração converter o conteúdo para a loja de instância única, o Gestor de Configuração elimina o conteúdo original de origem no computador de ponto de distribuição para libertar o espaço do disco. O Gestor de Configuração não utiliza a localização original do conteúdo de origem.  

Nem todos os pontos de distribuição do Gestor de Configuração 2007 que pode partilhar são elegíveis para upgrade para a filial atual do Gestor de Configuração. Para ser elegível para upgrade, um ponto de distribuição do Gestor de Configuração 2007 deve satisfazer as condições para a atualização. Estas condições incluem o servidor do sistema do site no qual o ponto de distribuição está instalado e o tipo de ponto de distribuição do Gestor de Configuração 2007 que está instalado. Por exemplo, não é possível atualizar qualquer tipo de ponto de distribuição que esteja instalado no computador do servidor do site num site primário, mas pode atualizar um ponto de distribuição padrão que esteja instalado no computador do servidor do site num site secundário.  

> [!NOTE]  
>  Só é possível atualizar os pontos de distribuição partilhados do Gestor de Configuração de 2007 que estão num computador que executa uma versão do sistema operativo que é suportada para pontos de distribuição na hierarquia de destino. Por exemplo, embora possa partilhar um ponto de distribuição do Gestor de Configuração de 2007 que está num computador que executa o Windows Vista, não é possível atualizar este ponto de distribuição partilhado porque o sistema operativo não é suportado pela atual sucursal do Gestor de Configuração para utilização como ponto de distribuição.  

A tabela seguinte lista os locais suportados para cada tipo de ponto de distribuição do Gestor de Configuração 2007 que pode atualizar.  

|Tipo de ponto de distribuição|Ponto de distribuição num computador do sistema de sites diferente do servidor do site|Ponto de distribuição num computador do sistema de sites diferente do servidor do site e que aloja outras funções de sistema de sites|Ponto de distribuição no servidor de um site secundário|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Ponto de distribuição padrão|Sim|Não|Sim|  
|Ponto de distribuição em partilhas de servidor<sup>1</sup>|Sim|Não|Não|  
|Ponto de distribuição secundário|Sim|Não|Não|  

 <sup>1</sup> O atual ramo do Gestor de Configuração não suporta as partilhas do servidor para os sistemas do site, mas suporta a atualização de um ponto de distribuição do Gestor de Configuração de 2007 que está numa partilha de servidor. Quando atualiza um ponto de distribuição do Gestor de Configuração 2007 que está numa parte do servidor, o tipo de ponto de distribuição é automaticamente convertido para um servidor, e deve selecionar a unidade no computador de ponto de distribuição que armazenará a loja de conteúdos de instância única.  

> [!WARNING]  
>  Antes de atualizar um ponto de distribuição de agências, desinstale o software cliente do Gestor de Configuração 2007. Ao atualizar um ponto de distribuição de sucursais que tenha instalado o software cliente Do Gestor de Configuração 2007, o conteúdo que foi previamente implantado para o computador é removido do computador e a atualização do ponto de distribuição falha.  

Para identificar pontos de distribuição elegíveis para upgrade na consola do Gestor de Configuração no nó **da Hierarquia source,** selecione um site de origem e, em seguida, selecione o separador Pontos de **Distribuição Partilhada.** Exibição de pontos de distribuição elegíveis **Sim** na coluna **Elegível para atualização.**  

Ao atualizar um ponto de distribuição instalado num servidor de site secundário do Gestor de Configuração 2007, o site secundário é desinstalado da hierarquia de origem. Embora este cenário seja designado uma atualização de site secundário, apenas se aplica à função de ponto de distribuição do sistema de sites. Por conseguinte, o site secundário não é atualizado e, em vez disso, é desinstalado. Isto deixa um ponto de distribuição da hierarquia de destino no computador que era o servidor de site secundário. Se planeia atualizar o ponto de distribuição num site secundário, consulte o Plano para atualizar os sites secundários do Gestor de [Configuração de 2007](#BKMK_UpgradeSS) neste tópico.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Processo de atualização de pontos de distribuição  
Pode utilizar a consola Do Gestor de Configuração para atualizar os pontos de distribuição do Gestor de Configuração 2007 que partilhou com a hierarquia do destino. Ao atualizar um ponto de distribuição partilhado, o ponto de distribuição é desinstalado no site do Gestor de Configuração de 2007. É então instalado como um ponto de distribuição que está ligado a um local primário ou secundário que especifica na hierarquia de destino. O processo de atualização cria uma cópia do conteúdo migrado que é armazenada no ponto de distribuição e, em seguida, converte esta cópia para o arquivo de conteúdos de instância única. Quando o Gestor de Configuração converte um pacote para a loja de conteúdos de instância única, elimina esse pacote da parte SMSPKG no computador do ponto de distribuição, a menos que o pacote tenha um ou mais anúncios que estão definidos para **executar programa a partir do ponto de distribuição**.  

Para atualizar o ponto de distribuição, o Gestor de Configuração utiliza a Conta de Acesso ao **Site Fonte** que é criada para recolher dados do Fornecedor SMS do site de origem. Embora esta conta exija apenas a permissão **de Leitura** para que os objetos do site recolham dados do site de origem, também deve ter a autorização **de Eliminar** e **Modificar** para a classe **Site** remover com sucesso o ponto de distribuição do site 'Gestor de Configuração' 2007 durante a atualização.  

> [!NOTE]  
>  O Gestor de Configuração pode converter conteúdo para a loja de instância única num único ponto de distribuição de cada vez. Quando configura várias atualizações de pontos de distribuição, os pontos de distribuição são em fila para upgrade e processados um de cada vez.  

Antes de atualizar um ponto de distribuição partilhado, certifique-se de que todos os conteúdos implementados no ponto de distribuição são migrados. Os conteúdos que não migrar antes de atualizar o ponto de distribuição não estarão disponíveis na hierarquia de destino após a atualização. Quando atualiza um ponto de distribuição, o conteúdo dos pacotes migrados é convertido para um formato compatível com o arquivo de instância única da hierarquia de destino.  

Para atualizar um ponto de distribuição a partir da consola Do Gestor de Configuração, o servidor do sistema de configuração 2007 deve satisfazer as seguintes condições:  

-   A configuração e a localização do ponto de distribuição deverão ser elegíveis para atualização.  

-   O computador de ponto de distribuição deve dispor de espaço suficiente para que o conteúdo seja convertido do formato de armazenamento de conteúdo do Gestor de Configuração 2007 para o formato de loja de instância única. Esta conversão necessita de um espaço em disco disponível equivalente ao tamanho do pacote mais volumoso que se encontra armazenado no ponto de distribuição.  

-   O computador do ponto de distribuição deverá estar a executar uma versão de sistema operativo que seja suportada como ponto de distribuição na hierarquia de destino.  

    > [!NOTE]  
    >  Quando o Gestor de Configuração verifica a elegibilidade de um ponto de distribuição para atualização, não valida a versão do sistema operativo do computador do ponto de distribuição.  

Para atualizar um ponto de distribuição, no espaço de trabalho da **Administração,** expandir a **Migração,** expandir o nó **da Hierarquia fonte** e, em seguida, selecionar o site que tem o ponto de distribuição que pretende atualizar. Em seguida, no separador **Pontos de Distribuição Partilhados** do painel de detalhes, selecione o ponto de distribuição que pretende atualizar.  

Poderá confirmar que o ponto de distribuição está preparado para atualização verificando o estado da coluna **Elegível para Reatribuição** .  Em seguida, na fita de consola do Gestor de Configuração, no separador Pontos de **Distribuição,** no grupo Ponto de **Distribuição,** selecione **Reassign**. Isto abre um assistente que utiliza para terminar a atualização do ponto de distribuição.  

Ao atualizar um ponto de distribuição partilhado, deverá atribuir o ponto de distribuição a um site primário ou a um site secundário da sua preferência na hierarquia de destino. Depois de atualizado o ponto de distribuição, gerencie o ponto de distribuição como ponto de distribuição na hierarquia do destino como qualquer outro ponto de distribuição.  

Pode monitorizar o progresso de uma atualização de ponto de distribuição na consola do Gestor de Configuração, selecionando o nó migração do Ponto de **Distribuição** sob **o** nó migratório migratório do espaço de trabalho da **Administração.** Também pode ver as informações do **Migmctrl.log** no servidor do site de administração central da hierarquia de destino, ou no **distmgr.log** do servidor do site na hierarquia de destino que gere o ponto de distribuição atualizado.  

> [!NOTE]  
>  Ao atualizar um ponto de distribuição para a hierarquia do destino, a função do sistema de site de pontos de distribuição é removida do site de origem do Gestor de Configuração de 2007. No entanto, os pacotes enviados para o ponto de distribuição não são atualizados na hierarquia do Gestor de Configuração de 2007. Na consola De Configuração 2007, os pacotes que tinham sido enviados para o ponto de distribuição continuam a listar o computador do sistema do site como um ponto de distribuição com um **Tipo** de **Desconhecido**. As atualizações subsequentes do pacote no Gestor de Configuração 2007 resultam em erros de relatório do Gestor de Distribuição no registo distmgr.log para esse site quando o site tenta atualizar o pacote no sistema de site desconhecido.  

Se decidir não atualizar um ponto de distribuição partilhado, ainda pode instalar um ponto de distribuição a partir da hierarquia de destino num antigo ponto de distribuição do Gestor de Configuração de 2007. Antes de poder instalar o novo ponto de distribuição, tem primeiro de desinstalar todas as funções do sistema de configuração 2007 a partir do computador do ponto de distribuição. Isto inclui o site 'Gestor de Configuração' 2007 se for o computador do servidor do site. Quando desinstala um ponto de distribuição do Gestor de Configuração de 2007, o conteúdo que foi implantado para o ponto de distribuição não é eliminado do computador.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a>Plano para atualizar sites secundários do Gestor de Configuração 2007  
 Quando utiliza a migração para atualizar um ponto de distribuição partilhado que está hospedado num servidor de site secundário do Gestor de Configuração de 2007, o Gestor de Configuração atualiza a função do sistema de site de pontos de distribuição para ser um ponto de distribuição na hierarquia do destino. Também desinstala o local secundário a partir da hierarquia de origem. O resultado é um ponto de distribuição atual do gerente de configuração, mas nenhum site secundário.  

 Para que um ponto de distribuição no computador do servidor do site seja elegível para upgrade, o Gestor de Configuração deve ser capaz de desinstalar o site secundário e cada uma das funções do sistema do site nesse computador. Tipicamente, um ponto de distribuição partilhado numa partilha de servidor do Gestor de Configuração 2007 é elegível para upgrade. No entanto, se existir uma partilha de servidor no servidor do site secundário, o site secundário e os pontos de distribuição partilhados nesse computador não serão elegíveis para atualização. Isto porque a partilha do servidor é tratada como um objeto adicional do sistema do site quando o processo tenta desinstalar o site secundário, e este processo não pode desinstalar este objeto. Neste cenário, poderá ativar um ponto de distribuição padrão no servidor de site secundário e, em seguida, redistribuir os conteúdos a esse ponto de distribuição padrão. Este processo não utiliza a largura de banda da rede e, quando terminado, pode desinstalar o ponto de distribuição na parte do servidor, remover a parte do servidor e, em seguida, atualizar o ponto de distribuição e o site secundário.  

 Antes de atualizar um ponto de distribuição partilhado, reveja a configuração do ponto de distribuição no Diretor de Configuração 2007 para evitar atualizar um ponto de distribuição num site secundário que ainda deseja utilizar com o Gestor de Configuração 2007. Esta é uma boa prática, porque depois de atualizar um ponto de distribuição partilhado que está num servidor de site secundário, o servidor do sistema do site é removido da hierarquia do Gestor de Configuração 2007 e já não está disponível para uso com essa hierarquia. Quando o site secundário for removido, quaisquer pontos de distribuição restantes nesse site secundário ficarão órfãos. Isto significa que não são geridos a partir do Diretor de Configuração 2007 e já não são partilhados ou elegíveis para atualização.  

> [!WARNING]  
>  Quando visualiza pontos de distribuição partilhados na consola Do Gestor de Configuração, não há nenhuma indicação visível de que um ponto de distribuição partilhado esteja num servidor de sistema de site remoto ou no servidor de site secundário.  

 Quando tiver um site secundário numa localização remota de rede que é usada principalmente para controlar a implementação de conteúdo para essa localização remota, considere atualizar sites secundários que tenham um ponto de distribuição partilhado. Uma vez que pode configurar o controlo da largura de banda para quando distribui conteúdo para um ponto de distribuição de filial atual do Gestor de Configuração, muitas vezes pode atualizar um site secundário para um ponto de distribuição, configurar o ponto de distribuição para controlos de largura de banda e evitar instalar um site secundário nessa localização de rede na hierarquia de destino.  

 O processo de atualização de um ponto de distribuição partilhado num servidor de site secundário é o mesmo que qualquer outro upgrade de ponto de distribuição partilhada. O conteúdo é copiado e convertido para a loja de instância única em uso pela hierarquia de destino. No entanto, ao atualizar um ponto de distribuição partilhado que se encontra num servidor de site secundário, o processo de atualização também desinstala o ponto de gestão (se presente) e depois desinstala o site secundário a partir do servidor. O resultado é que o local secundário é removido da hierarquia do Gestor de Configuração de 2007. Para desinstalar o site secundário, o Gestor de Configuração utiliza a conta que é configurada para recolher dados do site de origem.  

 Durante a atualização, há um atraso entre quando o site secundário do Gestor de Configuração de 2007 está desinstalado e a quando começa a instalação do ponto de distribuição na hierarquia de destino. O ciclo de recolha de dados determina este atraso de até quatro horas. O atraso destina-se a proporcionar tempo para que o local secundário desinstale antes do início da instalação do novo ponto de distribuição.  

 Para saber mais sobre como atualizar um ponto de distribuição partilhado, consulte [Plan to upgrade Configuration Manager 2007 pontos](#Planning_to_Upgrade_DPs)de distribuição partilhadas .  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a>Plano para reatribuir pontos de distribuição do Gestor de Configuração  
 Quando se migra de uma versão suportada do System Center 2012 Configuration Manager para uma hierarquia da mesma versão, pode reatribuir um ponto de distribuição partilhado da hierarquia de origem para um site na hierarquia de destino. Isto é como o conceito de upgrade de um ponto de distribuição de Configuração Manager 2007 para se tornar um ponto de distribuição na hierarquia de destino. Pode reatribuir pontos de distribuição de sites primários e locais secundários. A ação para reatribuir um ponto de distribuição remove o ponto de distribuição da hierarquia de origem e faz do computador e do seu ponto de distribuição um servidor de sistema de site do site que seleciona na hierarquia de destino.  

 Ao reatribuir um ponto de distribuição, não necessita de redistribuir os conteúdos migrados que se encontravam alojados no ponto de distribuição do site de origem. Além disso, ao contrário da atualização de um ponto de distribuição do Gestor de Configuração de 2007, a reatribuição de um ponto de distribuição não requer espaço adicional no disco no computador do ponto de distribuição. Isto porque, a partir do System Center 2012 Configuration Manager, os pontos de distribuição utilizam o formato de loja de uma instância única para conteúdos. O conteúdo do computador ponto de distribuição não precisa de ser convertido quando o ponto de distribuição é reatribuído entre hierarquias.  

 Para que um ponto de distribuição do Gestor de Configuração do System Center 2012 seja elegível para reatribuição, deve cumprir os seguintes critérios:  

-   Um ponto de distribuição partilhado tem de ser instalado num computador que não o do servidor do site.  

-   Um ponto de distribuição partilhado não pode ser localizado conjuntamente com quaisquer funções adicionais do sistema de sites.  

Para identificar pontos de distribuição elegíveis para reatribuição na consola do Gestor de Configuração no nó da Hierarquia **Source,** selecione um site de origem **Eligible for Upgrade** e, em seguida, selecione o separador Pontos de **Distribuição Partilhada.** **Yes** **Eligible for Reassignment**  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Processo de reatribuição de pontos de distribuição  
 Pode utilizar a consola Do Gestor de Configuração para reatribuir pontos de distribuição que partilhou a partir de uma hierarquia de origem ativa. Ao reatribuir um ponto de distribuição partilhado, o ponto de distribuição é desinstalado a partir do seu site de origem e depois instalado como um ponto de distribuição que está ligado a um site primário ou secundário que especifica na hierarquia de destino.  

 Para reatribuir o ponto de distribuição, a hierarquia de destino utiliza a Conta de Acesso ao Sítio Fonte que está configurada para recolher dados do Fornecedor SMS do site de origem. Para obter informações sobre permissões necessárias e pré-requisitos adicionais, consulte [os pré-requisitos para a migração](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhadaao mesmo tempo
A partir da versão 1610, pode utilizar o ponto de distribuição de **reassignos** para ter o processo de Configuração Manager em paralelo a reatribuição de até 50 pontos de distribuição partilhadas ao mesmo tempo. Isto inclui pontos de distribuição partilhados de sites de origem suportados que funcionam:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- Gestor de Configuração (ramo atual)

Ao reatribuir pontos de distribuição, cada ponto de distribuição deve ser qualificado para ser atualizado ou reatribuído. O nome da ação e processo envolvido (upgrade ou reatribuição) depende da versão do Gestor de Configuração que o site de origem executa. Os resultados finais de ambas as ações são os mesmos: o ponto de distribuição é atribuído a um dos seus sites da Filial Atual com o seu conteúdo no lugar.

Antes da versão 1610, o Gestor de Configuração só conseguia processar um ponto de distribuição de cada vez. Agora pode reatribuir os pontos de distribuição que quiser com as seguintes ressalvas:  
- Embora não seja possível selecionar vários pontos de distribuição a serem reatribuídos, quando tiver feito fila mais de um, o Gestor de Configuração irá processá-los em paralelo em vez de esperar para terminar um antes de começar o próximo.  
- Por predefinição, até 50 pontos de distribuição são processados paralelamente de cada vez. Após a reatribuição do primeiro ponto de distribuição, o Gestor de Configuração começará a processar o 51º, e assim por diante.  
- Quando utilizar o Gestor de Configuração SDK, pode alterar o **SharedDPImportThreadLimit** para ajustar o número de pontos de distribuição reatribuídos que o Gestor de Configuração pode processar em paralelo.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a>Atribuir a propriedade do conteúdo ao migrar conteúdo  
 Ao migrar conteúdo para implementações,necessita de atribuir o objeto do conteúdo a um site da hierarquia de destino. Em seguida, este site torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de alto nível da sua hierarquia de destino seja o site que migra os metadados para conteúdo, é o site atribuído que utiliza os ficheiros de origem originais para o conteúdo em toda a rede.  

 Para reduzir ao mínimo a largura de banda de rede que é utilizada para migrar os conteúdos, pondere transferir a propriedade dos conteúdos para um site da hierarquia de destino que esteja num local próximo da rede da localização dos conteúdos na hierarquia de origem. Dado que as informações sobre os conteúdos da hierarquia de destino são partilhadas globalmente, ficarão disponíveis em todos os sites.  

 Embora a informação sobre o conteúdo seja partilhada em todos os sites utilizando a replicação da base de dados, qualquer conteúdo que atribua a um site primário e, em seguida, implemente para pontos de distribuição em outros sites primários transfere por replicação baseada em ficheiros. Esta transferência é encaminhada através do site de administração central e, em seguida, para o site primário adicional. Pode reduzir as transferências de dados através de redes de baixa largura de banda centralizando pacotes que planeia distribuir para vários sites primários antes ou durante a migração quando atribuía um site como proprietário de conteúdo.
