---
title: Replicação de base de dados
titleSuffix: Configuration Manager
description: Saiba como a replicação da base de dados do Gestor de Configuração utiliza o SQL Server para transferir dados na hierarquia.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720199"
---
# <a name="database-replication"></a>Replicação de base de dados

*Aplica-se a: Gestor de Configuração (ramo atual)*

A replicação da base de dados do Gestor de Configuração utiliza o Servidor SQL para transferir dados. Utiliza este método para fundir alterações na sua base de dados do site com a informação da base de dados de outros sites da hierarquia.

Note os seguintes pontos sobre a replicação da base de dados:

- Todos os sites partilham a mesma informação.  

- Quando instala um site numa hierarquia, o Gestor de Configuração estabelece automaticamente a replicação da base de dados entre o novo site e o seu site-mãe.  

- Quando a instalação do local terminar, a replicação da base de dados começa automaticamente.  

Quando adiciona um novo site a uma hierarquia, o Gestor de Configuração cria uma base de dados genérica no novo site. O site-mãe cria uma imagem instantânea dos dados relevantes na sua base de dados. Em seguida, transfere o instantâneo para o novo site usando [replicação baseada em ficheiros](file-based-replication.md). O novo site utiliza então o Programa de Cópia seleção a granel (BCP) para carregar a informação na sua cópia local da base de dados do Gestor de Configuração. Após o carregamento do instantâneo, cada site efetua a replicação de base de dados com outro site.  

Para replicar dados entre sites, o Gestor de Configuração utiliza o seu próprio serviço de replicação de bases de dados. O serviço de replicação de bases de dados utiliza o rastreio de alteração do Servidor SQL para monitorizar a base de dados local do site para obter alterações. Em seguida, replica as alterações para outros sites utilizando o SQL Server Service Broker (SSB). Por defeito, este processo utiliza a porta TCP 4022.  


## <a name="replication-groups"></a>Grupos de replicação

O Gestor de Configuração agrupa dados que se replicam por replicação de bases de dados em diferentes grupos de replicação. Cada grupo de replicação tem um calendário de replicação separado e fixo. O site usa esta programação para determinar com que frequência replica alterações a outros sites.  

Por exemplo, uma mudança para uma configuração de administração baseada em papéis replica-se rapidamente para outros sites. Este comportamento garante que o outro site pode aplicar rapidamente estas alterações. Uma mudança de configuração de menor prioridade, como um pedido de instalação de um novo site secundário, replica-se com menos urgência. Pode levar vários minutos para um novo pedido de site para chegar ao local principal do destino.  


## <a name="settings"></a>Definições

Pode modificar as seguintes definições para a replicação da base de dados:  

- **Ligações**de replicação de bases de dados : Controle quando o tráfego específico atravessa a rede.  

- **Pontos de vista distribuídos**: Quando um site de administração central (CAS) solicita dados do site selecionados, pode aceder diretamente aos dados da base de dados de um local primário infantil.  

- **Horários**: Especificar quando é utilizada uma ligação de replicação e quando se replicam diferentes tipos de dados do site.  

- **Resumo**: Alterar as definições para a resumição de dados sobre o tráfego de rede que atravessa as ligações de replicação. Por predefinição, o resumo ocorre a cada 15 minutos. É usado em relatórios para replicação de bases de dados.  

- **Limiares**de replicação da base de dados : Defina quando o site reportar ligações como degradadas ou falhadas. Também pode configurar quando o Gestor de Configuração levantar alertas sobre links de replicação que tenham um estado degradado ou falhado.  


## <a name="types-of-data"></a>Tipos de dados

O Gestor de Configuração classifica principalmente os dados que replica como *dados globais* ou dados do *site.* Quando ocorre a replicação da base de dados, o site transfere alterações para dados globais e dados do site através do link de replicação da base de dados. Os dados globais replicam-se para um site de pais ou filhos. Os dados do site replicam-se apenas para um site dos pais. Um terceiro tipo de dados, *dados locais,* não se replica para outros sites. Dados locais são informações que outros sites não requerem.  

### <a name="global-data"></a>Dados globais

Os dados globais são objetos criados por administradores que se replicam a todos os sites ao longo da hierarquia. Os sites secundários só recebem um subconjunto de dados globais, como dados globais de procuração. Cria dados globais no CAS e nos locais primários. Este tipo inclui os seguintes dados:

- Implementações de software
- Atualizações de software
- Definições de recolha
- Âmbitos de segurança da administração baseados em funções

### <a name="site-data"></a>Dados do site

Os dados do site são informações operacionais criadas pelos principais sites do Gestor de Configuração e seus clientes designados. Os dados do site replicam-se para o CAS, mas não para outros locais primários. Os dados do site só são visualizados no CAS e no local primário onde os dados são originados. Só é possível modificar os dados do site no local principal onde os criou. Este tipo inclui os seguintes dados:

- Inventário de Hardware
- Mensagens de estado
- Alertas
- Os resultados das coleções baseadas em consultas

Todos os dados do site se replicam para o CAS. O CAS faz administração e reportagens para toda a hierarquia do site.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a> Ligações de replicação de base de dados

Quando instala um novo site numa hierarquia, o Gestor de Configuração cria automaticamente uma ligação de replicação de base de dados entre o site-mãe e o novo site. Cria uma única ligação para ligar os dois sites.  

Para controlar a transferência de dados através da ligação de replicação, altere as definições para cada link. Cada ligação de replicação suporta configurações separadas. Cada ligação de replicação da base de dados inclui os seguintes controlos:  

- Impedir a replicação de dados do site selecionados de um local primário para o CAS. Esta ação faz com que o CAS aceda a estes dados diretamente a partir da base de dados do site principal.  

- Agendar dados do site selecionados para transferir de um site primário infantil para o CAS.

- Defina as definições que determinam quando uma ligação de replicação de base de dados tem um estado degradado ou falhado.

- Especifique quando levantar alertas para uma ligação de replicação falhada.

- Especifique a frequência com que o Gestor de Configuração resume dados sobre o tráfego de replicação que utiliza a ligação de replicação. Usa estes dados em relatórios.

Para configurar uma ligação de replicação de base de dados, na consola Do Gestor de Configuração, vá ao espaço de trabalho **de Monitorização.** Selecione o nó de **replicação** da base de dados e edite as propriedades para o link. Este nó também está no espaço de trabalho da **Administração,** sob o nó de **Configuração da Hierarquia.** Editar um link de replicação do site dos pais ou do local da criança do link de replicação.  

> [!TIP]  
> Pode editar ligações de replicação de base de dados a partir do nó **Replicação de Base de Dados** em qualquer uma das áreas de trabalho. No entanto, ao utilizar o nó de **replicação** da base de dados no espaço de trabalho **de monitorização,** também pode visualizar o estado da replicação da base de dados. Também fornece acesso à ferramenta Analisador de Ligações de [Replicação.](../../servers/manage/monitor-replication.md#BKMK_RLA) Utilize esta ferramenta para ajudar a investigar problemas com a replicação da base de dados.  

Para obter mais informações sobre como configurar links de replicação, consulte os controlos de [replicação da base](#BKMK_DBRepControls)de dados do Site . Para obter mais informações sobre como monitorizar a replicação, consulte a [replicação da base](../../servers/manage/monitor-replication.md)de dados Monitor .  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a>Vistas distribuídas  

Através de vistas distribuídas, quando faz um pedido no CAS para obter dados do site selecionados, acede diretamente à base de dados no local primário da criança. Este acesso direto substitui a necessidade de replicar os dados do site do local principal para o CAS. Como cada ligação de replicação é independente de outras ligações de replicação, pode utilizar pontos de vista distribuídos nas ligações de replicação que escolher. Não pode usar vistas distribuídas entre um local primário e um local secundário.  

As opiniões distribuídas proporcionam os seguintes benefícios:  

- Reduzir a carga do CPU para processar alterações na base de dados no CAS e nos principais locais

- Reduzir a quantidade de dados que transfere através da rede para o CAS

- Melhorar o desempenho do Servidor SQL que acolhe a base de dados CAS

- Reduzir o espaço do disco utilizado pela base de dados CAS

Considere utilizar vistas distribuídas quando um local primário está intimamente localizado para o CAS na rede, os dois sites estão sempre ligados e sempre ligados. As vistas distribuídas substituem a replicação dos dados selecionados entre os sites por ligações diretas entre os servidores SQL em cada site. O CAS faz uma ligação direta cada vez que solicita estes dados.

O site solicita dados de visualização distribuídos nos seguintes cenários exemplo:

- Quando executa relatórios ou consultas
- Quando vê informações no Explorador de Recursos
- Avaliação de recolha para coleções que incluam regras baseadas em dados do site

Por defeito, as vistas distribuídas são desligadas para cada ligação de replicação. Quando liga as vistas distribuídas, seleciona dados do site que não se replicam para o CAS através desse link. O CAS acede a estes dados diretamente a partir da base de dados do site primário infantil que partilha o link. Pode configurar os seguintes tipos de dados de site para vistas distribuídas:  

- Dados de inventário de **hardware** de clientes
- Dados de **inventário de software e de medição** de software dos clientes
- **Mensagens** de estado dos clientes, do site primário e de todos os sites secundários

Quando vê dados na consola do Gestor de Configuração ou em relatórios, as vistas distribuídas são operacionalmente invisíveis para si. Quando solicita dados que estão habilitados para visualizações distribuídas, o servidor de base de dados do site CAS acede diretamente à base de dados do site primário da criança para recuperar a informação.

Por exemplo, utiliza-se uma consola De Configuração Manager ligada ao CAS. Solicita informações sobre o inventário de hardware de dois sites primários: ABC e XYZ. Apenas permitiu o inventário de hardware para visualizações distribuídas no site ABC. O CAS recupera informações de inventário para clientes XYZ a partir da sua própria base de dados. O CAS recupera informações de inventário para clientes ABC diretamente da base de dados do site ABC. Esta informação aparece na consola do Gestor de Configuração ou num relatório sem identificar a fonte.  

Se uma ligação de replicação tiver um tipo de dados habilitados para visualizações distribuídas, o site primário da criança não replica esses dados para o CAS. Quando desliga as vistas distribuídas para um tipo de dados, o site primário da criança retoma a replicação normal de dados para o CAS. Antes de estes dados estarem disponíveis no CAS, os grupos de replicação para estes dados devem reinicializar entre o local primário e o CAS. Depois de desinstalar um site primário que tenha distribuído vistas ligadas, o CAS deve completar a reinicialização dos seus dados antes de poder aceder aos dados que permitiu para visualizações distribuídas no CAS.  

> [!IMPORTANT]  
> Quando utilizar vistas distribuídas sobre qualquer ligação de replicação na hierarquia do site, antes de desinstalar qualquer site primário, desligue as vistas distribuídas para todas as ligações de replicação. Para mais informações, consulte [Desinstalar um site primário que utilize vistas distribuídas](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Pré-requisitos e limitações para vistas distribuídas  

- Utilize apenas pontos de vista distribuídos sobre as ligações de replicação entre o CAS e um local primário.

- O CAS deve utilizar a edição SQL Server Enterprise. O local principal não tem este requisito.

- O CAS só pode ter uma instância do Fornecedor sms. Instale essa instância única no servidor de base de dados do site. Esta configuração suporta a autenticação kerberos. O servidor SQL do CAS requer que kerberos aceda ao servidor SQL no local primário da criança. Não existem limites para o fornecedor de SMS no site primário subordinado.

- Só é possível instalar um ponto de serviços de reporte no CAS. Instale os Serviços de Reporte do Servidor SQL no servidor de base de dados do site. Esta configuração suporta a autenticação kerberos. O servidor SQL do CAS requer que kerberos aceda ao servidor SQL no local primário da criança.

- Não é possível hospedar a base de dados do site num [cluster do Servidor SQL](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- Na versão 1902 e anterior, não é possível hospedar a base de dados do site num [grupo de disponibilidade sQL Server Always On](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). Para suportar esta configuração, atualize para a versão 1906 ou mais tarde.<!-- SCCMDocs-pr#3792 -->

- A conta de computador do servidor de base de dados CAS requer **permissões de leitura** na base de dados do site primário.

> [!IMPORTANT]  
> As vistas e [horários distribuídos](#BKMK_schedules) para quando os dados podem replicar-se são configurações mutuamente exclusivas para uma ligação de replicação de base de dados.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a>Agendar transferências de dados do site

Para ajudá-lo a controlar a largura de banda da rede que é usada para replicar os dados do site de um site primário infantil para o CAS, marque quando uma ligação de replicação é usada. Em seguida, especifique quando diferentes tipos de dados do site se replicam. Pode controlar quando as mensagens de estado, os dados de inventário e de medição são replicados pelo site primário. As ligações de replicação de bases de dados de sites secundários não suportam os horários dos dados do site. Não pode agendar a transferência de dados globais.  

Quando configurar um calendário de ligação de replicação de base de dados, pode restringir a transferência de dados do site selecionados do site principal para o CAS. Também pode configurar diferentes tempos para replicar diferentes tipos de dados do site.  

> [!IMPORTANT]  
> As vistas e horários [distribuídos](#bkmk_distviews) para quando os dados podem replicar-se são configurações mutuamente exclusivas para uma ligação de replicação de base de dados.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a>Resumição do tráfego  

Cada site resume periodicamente dados sobre o tráfego de rede que atravessa links de replicação de bases de dados para o site. O site utiliza dados resumidos em relatórios para replicação de bases de dados. Ambos os sites numa ligação de replicação resumem o tráfego de rede que atravessa a ligação de replicação. O servidor de base de dados do site resume os dados. Depois de resumir os dados, a informação replica-se a outros sites como dados globais.  

Por predefinição, o resumo ocorre a cada 15 minutos. Para modificar a frequência de resumição para o tráfego de rede, nas propriedades da ligação de replicação da base de dados, edite o **intervalo de sumreização**. A frequência da resumição afeta a informação que vê nos relatórios sobre a replicação da base de dados. Pode escolher um intervalo de 5 a 60 minutos. Quando aumenta a frequência do resumo, aumenta a carga de processamento no SQL Server de cada site na ligação de replicação.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a>Limiares de replicação de bases de dados

Os limiares de replicação da base de dados definem quando o Gestor de Configuração reporta o estado de uma ligação de replicação de base de dados como degradado ou falhado. Por padrão, estabelece uma ligação como *degradada* quando qualquer grupo de replicação não consegue completar a replicação por 12 tentativas consecutivas. Estabelece o link como *falhado* quando qualquer grupo de replicação não se replica em 24 tentativas consecutivas.  

Pode especificar valores personalizados para o estado degradado ou falhado. Se ajustar estes valores, poderá monitorizar com maior precisão a saúde da replicação da base de dados através dos links.  

Um ou mais grupos de replicação podem não se replicar enquanto outros grupos de replicação continuam a replicar-se com sucesso. Planeie rever o estado de replicação de um link quando reportar pela primeira vez como degradado.

Considere modificar os valores de retry para o estado degradado ou falhado do link nas seguintes situações:

- Há atrasos recorrentes para grupos de replicação específicos, e o seu atraso não é um problema

- A ligação de rede entre sites tem baixa largura de banda disponível

Quando aumenta o número de repetições antes de o site definir o link para degradado ou falhado, pode eliminar avisos falsos para questões conhecidas. Esta ação permite-lhe rastrear com maior precisão o estado do link.  

Para entender a frequência com que a replicação desse grupo ocorre, considere o intervalo de sincronização de replicação para cada grupo de replicação. Para ver o **intervalo de sincronização** para grupos de replicação, vá ao espaço de trabalho **de Monitorização** na consola 'Gestor de Configuração'. No nó de replicação da base de **dados,** selecione o separador De pormenor de **replicação** de uma ligação de replicação.  

Para obter mais informações sobre como monitorizar a replicação da base de dados, incluindo como visualizar o estado de replicação, consulte a [replicação da base](../../servers/manage/monitor-replication.md)de dados Monitor .  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a>Controlos de replicação da base de dados do site  

Para o ajudar a controlar a largura de banda da rede utilizada para a replicação da base de dados, altere as definições para cada base de dados do site. As definições aplicam-se apenas à base de dados do site na qual configura as definições. As definições são sempre utilizadas quando o site replica quaisquer dados por replicação de base de dados para qualquer outro site.  

Pode modificar os seguintes controlos de replicação para cada base de dados do site:  

- A porta SSB  

- O período de tempo para esperar antes que as falhas de replicação desencadeiem o site para reinicializar a sua cópia da base de dados do site  

- Comprima os dados que um site replica. Apenas comprime os dados para transferência entre sites, e não para armazenamento na base de dados do site em qualquer dos locais.  

Para alterar as definições dos controlos de replicação para uma base de dados do site, na consola Do Gestor de Configuração, no nó de replicação da Base de **Dados,** edite as propriedades da base de dados do site. Este nó aparece sob o nó de **Configuração da Hierarquia** no espaço de trabalho da **Administração,** e também aparece no espaço de trabalho **de Monitorização.** Para editar as propriedades da base de dados do site, selecione a ligação de replicação entre os sites e, em seguida, abra propriedades da Base de **Dados dos Pais** ou propriedades da base de dados **infantil**.  

> [!TIP]  
> Pode configurar os controlos de replicação de base de dados no nó **Replicação de Base de Dados** em ambas as áreas de trabalho. No entanto, quando utiliza o nó de **replicação** da base de dados no espaço de trabalho de **monitorização,** também pode ver o estado da replicação da base de dados para uma ligação de replicação e aceder à ferramenta De replicação Link Analyzer para ajudá-lo a investigar problemas com replicação.  


## <a name="see-also"></a>Consulte também

[Monitorizar a replicação](../../servers/manage/monitor-replication.md)

[Resolver problemas de replicação do SQL](../../servers/manage/replication/overview.md)
