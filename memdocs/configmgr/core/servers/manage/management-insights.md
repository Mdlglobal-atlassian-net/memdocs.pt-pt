---
title: Informações de gestão
titleSuffix: Configuration Manager
description: Conheça a funcionalidade de insights de gestão disponível na consola Do Gestor de Configuração.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69b2533dd5c86124a6aff9feac7306ecf16c6e5a
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268968"
---
# <a name="management-insights-in-configuration-manager"></a>Insights de gestão em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os conhecimentos de gestão no Gestor de Configuração fornecem informações sobre o estado atual do seu ambiente. A informação baseia-se na análise de dados da base de dados do site. As ideias ajudam-no a entender melhor o seu ambiente e a tomar medidas com base na perceção. <!--1353967-->

## <a name="review-management-insights"></a>Rever insights de gestão

Para ver as regras, a sua conta necessita da permissão de **leitura** no objeto do **site.**

1. Abra a consola de gestor de configuração.  

2. Vá ao espaço de trabalho da **Administração,** expanda **os Insights de Gestão,** e selecione **All Insights**.  

    > [!Note]  
    > Ao selecionar o nó **Management Insights,** mostra o painel de insights de [Gestão](#bkmk_insights).  

3. Abra o nome do grupo de insights de gestão que pretende rever. Selecione **Mostrar Insights** na fita.  

Os seguintes quatro separadores estão disponíveis para revisão:

- **Todas as Regras**: Apresenta a lista completa de regras para o grupo de gestão de insights escolhidos.  

- **Completo**: Lista regras sempre que não é necessária qualquer ação.  

- **Em Progresso**: Mostra regras em que alguns, mas não todos, pré-requisitos estão completos.  

- **Ação necessária**: Estão enumeradas as regras que necessitam de ações tomadas. Selecione **Mais Detalhes** para recuperar itens específicos onde a ação é necessária.  

O painel de **pré-requisitos** lista os itens necessários para executar a regra.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas as regras e pré-requisitos para o grupo de serviços na nuvem

![Informações de gestão- Todas as regras e pré-requisitos para o grupo de serviços na nuvem](./media/Management-insights-all-cloud-rules.png)

Selecione uma regra e, em seguida, selecione **Mais Detalhes** para ver os detalhes da regra.

## <a name="operations"></a>Operações

As regras de informação de gestão reavaliam a sua aplicabilidade num horário semanal. Para reavaliar uma regra a pedido, clique na regra e **selecione Reavaliar**.

O ficheiro de registo para regras de insight de gestão é **SMS_DataEngine.log** no servidor do site.

<!--1357930-->
Algumas regras permitem-te agir. Selecione uma regra, selecione **Mais Detalhes,** e, se estiver disponível, **tome medidas**.

Dependendo da regra, esta ação tem um dos seguintes comportamentos:  

- Navegue automaticamente na consola até ao nó onde poderá tomar mais medidas. Por exemplo, se o insight de gestão recomendar a alteração da definição de um cliente, tomar medidas navega para o nó de Definições do Cliente. Em seguida, tome mais medidas modificando o padrão ou um objeto de definições personalizadas do cliente.  

- Navegue para uma vista filtrada com base numa consulta. Por exemplo, tomar medidas sobre a regra das coleções vazias mostra apenas estas coleções na lista de coleções. Em seguida, tome medidas adicionais, tais como a eliminação de uma coleção ou a alteração das suas regras de adesão.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Painel de insights de gestão

<!--1357979-->

O nó **Management Insights** inclui um painel gráfico. Este painel apresenta uma visão geral dos estados de regra, o que facilita a sua demonstração do seu progresso.

Utilize os seguintes filtros na parte superior do painel de instrumentos para aperfeiçoar a vista:

- Show Concluído
- Opcional
- Recomendado
- Crítico

O painel inclui os seguintes azulejos:  

- **Índice de insights**de gestão : Acompanha o progresso global das regras de insights de gestão. O índice é uma média ponderada. As regras críticas são as que valem mais. Este índice dá o menor peso às regras opcionais.  

- **Grupos de insights**de gestão : Mostra por cento das regras de cada grupo, honrando os filtros. Selecione um grupo para aprofundar as regras específicas deste grupo.  

- Prioridade dos insights de **gestão**: Mostra por cento das regras por prioridade, honrando os filtros.  

- **Todos os insights**: Uma tabela de insights, incluindo prioridade e estado. Utilize o campo **Filtro** na parte superior da tabela para combinar cordas em qualquer uma das colunas disponíveis. O painel de instrumentos classifica a tabela na seguinte ordem:

  - Estado: Ação Necessária, Concluída, Desconhecida  
  - Prioridade: Crítico, Recomendado, Opcional  
  - Last Changed: datas mais antigas no topo  

![Screenshot do painel de insights de gestão](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Grupos e regras

As regras são organizadas nos seguintes grupos de informação de gestão:

- [Aplicações](#applications)
- [Serviços em nuvem](#cloud-services)
- [Coleções](#collections)
- [Avaliação do Gestor de Configuração](#configuration-manager-assessment)
- [Manutenção proativa](#proactive-maintenance)
- [Segurança](#security)
- [Gestão simplificada](#simplified-management)
- [Centro de Software](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Aplicações

Insights para a sua gestão de aplicações.

- **Aplicações sem implementações**: Lista as aplicações no seu ambiente que não têm implementações ativas. Esta regra ajuda-o a encontrar e eliminar aplicações não utilizadas para simplificar a lista de aplicações apresentadas na consola. Para mais informações, consulte [aplicações de implementação](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Serviços em nuvem

Ajuda-o a integrar-se com muitos serviços na nuvem, que permitem a gestão moderna dos seus dispositivos.

- **Avaliar a prontidão de cogestão**: Ajuda-o a perceber que passos são necessários para permitir a cogestão. Esta regra tem pré-requisitos. Para mais informações, consulte a [visão geral da cogestão.](../../../comanage/overview.md)  

- **Dispositivos não enviados para AD Azure**: A partir da versão 2002, esta regra lista dispositivos que não são enviados para a AD Azure porque o site não está devidamente configurado para HTTPS.<!--6268489--> Configure [O HTTP melhorado,](../../plan-design/hierarchy/enhanced-http.md)ou ative pelo menos um ponto de gestão para HTTPS. Se já configurar o site para comunicação HTTPS, esta regra não aparece.

- **Configure os serviços Azure para utilização com o Gestor**de Configuração : Esta regra ajuda-o a bordo do Gestor de Configuração para a AD Azure, o que permite aos clientes autenticar em com o site utilizando o Azure AD. Para mais informações, consulte os [serviços do Configure Azure.](../deploy/configure/azure-services-wizard.md)  

- **Ativar os dispositivos para serem híbridos Azure Ative Directory aderidos**: Os dispositivos ligados ao Azure AD permitem que os utilizadores assinem com as suas credenciais de domínio, garantindo que os dispositivos cumprem as normas de segurança e conformidade da organização. Para mais informações, consulte as considerações de [design de identidade híbrida Azure AD.](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)  

- **Sites que não possuem configuração HTTPS adequada**: A partir da versão 2002, esta regra lista sites na sua hierarquia que não estão devidamente configurados para HTTPS. Esta configuração impede que o site [sincronize os resultados da adesão à coleção para grupos azure Ative Directory (Azure AD).](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) Pode fazer com que a sincronização da AD Azure não carregue todos os dispositivos. A gestão destes clientes pode não funcionar corretamente.<!--6268489--> Configure [O HTTP melhorado,](../../plan-design/hierarchy/enhanced-http.md)ou ative pelo menos um ponto de gestão para HTTPS. Se já configurar o site para comunicação HTTPS, esta regra não aparece.

- **Atualizar os clientes para a versão mais recente do Windows 10**: Windows 10, versão 1709 ou superior melhora e moderniza a experiência de computação dos seus utilizadores. Para mais informações, consulte os [principais artigos sobre a adoção](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)do Windows como um serviço .  

### <a name="collections"></a>Coleções

Insights que ajudam a simplificar a gestão, limpando e reconfigurando coleções.

- **Coleções Vazias**: Lista coleções no seu ambiente que não têm membros. Para mais informações, consulte [Como gerir as coleções.](../../clients/manage/collections/manage-collections.md)  

A partir da versão de 1902, existem novas regras com recomendações sobre gestão de coleções.<!--3555752--> Use estes insights para simplificar a gestão e melhorar o desempenho:

- **Coleções sem regras de consulta e sem membros diretos**: Para simplificar a lista de coleções na sua hierarquia, elimine estas coleções.  

- **Coleções com o mesmo horário de reavaliação**: Estas coleções têm o mesmo tempo de reavaliação que outras coleções. Modifique o tempo de reavaliação para que não entrem em conflito.  

- **Coleções com tempo de consulta ao longo**de 5 minutos : Reveja as regras de consulta para esta coleção. Considere modificar ou apagar a coleção.

- As seguintes regras incluem configurações que potencialmente causam carga desnecessária no site. Reveja estas coleções, e depois elimine-as ou desative a avaliação das regras:  

  - **Coleções sem regras de consulta e atualizações incrementais ativadas**  

  - **Coleções sem regras de consulta e habilitadas para qualquer horário**  

  - **Coleções sem regras de consulta e agendar avaliação completa selecionada**  

### <a name="configuration-manager-assessment"></a>Avaliação do Gestor de Configuração

<!--3607758-->

A partir da versão 2002, este grupo é cortesia da Microsoft Premier Field Engineering. Estas regras são uma amostra dos muitos mais controlos que a Microsoft Premier fornece no Centro de [Serviços.](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments)

- **Ative Directory Security Group Discovery está configurado para funcionar com demasiada frequência:** Normalmente não é necessário configurar a Ative Directory Security Group Discovery para ocorrer com mais frequência do que a cada três horas. Uma configuração mais frequente pode ter um impacto negativo no desempenho no Diretório Ativo, na rede e no Gestor de Configuração. Ative a sincronização incremental em vez de utilizar um cronograma completo. Para mais informações, consulte a descoberta do [grupo Ative Directory.](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)

- **Ative Directory System Discovery está configurado para ser executado com demasiada frequência:** Normalmente não é necessário configurar a Ative Directory System Discovery para ocorrer com mais frequência do que a cada três horas. Uma configuração mais frequente pode ter um impacto negativo no desempenho no Diretório Ativo, na rede e no Gestor de Configuração. Ative a sincronização incremental em vez de utilizar um cronograma completo. Para mais informações, consulte a descoberta do [sistema de Diretório Ativo.](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)

- **A Ative Directory User Discovery está configurada para ser executada com demasiada frequência:** Normalmente não é necessário configurar a Descoberta do Utilizador do Diretório Ativo para ocorrer com mais frequência do que a cada três horas. Uma configuração mais frequente pode ter um impacto negativo no desempenho no Diretório Ativo, na rede e no Gestor de Configuração. Ative a sincronização incremental em vez de utilizar um cronograma completo. Para mais informações, consulte a descoberta do [utilizador do Ative Directy.](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)

- **Coleções limitadas a Todos os Sistemas ou Todos os Utilizadores**: Reveja quaisquer coleções que utilizem as coleções De Todos os **Sistemas** ou **Todos os Utilizadores** como a recolha limitativa. O Gestor de Configuração atualiza a adesão destas coleções predefinidas com dados dos métodos de descoberta do Diretório Ativo. Estes dados podem não ser informações válidas para os clientes do Gestor de Configuração.

- **Heartbeat Discovery está desativado**: A descoberta do batimento cardíaco requer que instale o cliente do Gestor de Configuração nos dispositivos. É o único método de descoberta que os clientes começam. Todos os outros métodos ocorrem nos servidores do site. A descoberta do batimento cardíaco é essencial para manter o estado de atividade do cliente atual. Certifica-se de que o site não envelhece acidentalmente os registos de recursos da base de dados do site. Para mais informações, consulte a [descoberta do Heartbeat.](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)

- Consultas de recolha de **longa duração ativadas para atualizações incrementais**: Coleções com um último tempo de atualização incremental superior a 30 segundos usam recursos do servidor do site e da base de dados, o que pode potencialmente afetar o desempenho geral do Gestor de Configuração. Para mais informações, consulte [as melhores práticas para recolhas.](../../clients/manage/collections/best-practices-for-collections.md)

- **Reduza o número de aplicações e pacotes em pontos de distribuição**: A Microsoft suporta oficialmente um total combinado de até 10.000 pacotes e aplicações num ponto de distribuição. Ultrapassar este total pode levar a problemas operacionais. Para mais informações, consulte [tamanho e números de escala - ponto de distribuição](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Problemas**de instalação do local secundário : O estado de instalação de alguns locais secundários está **pendente** ou **falhado**. Estes estados significam que iniciou a instalação, mas não completou com sucesso. Até que o site secundário ainstale, os clientes podem não comunicar corretamente com o site principal. Verifique o espaço de trabalho **de monitorização** e volte a tentar a instalação. Para mais informações, consulte [a instalação de Retry de uma atualização falhada](install-in-console-updates.md#bkmk_retry).

- **Atualizar todos os sites para a mesma versão**: Use a mesma versão do Gestor de Configuração numa hierarquia. Esta configuração garante que todos os sites fornecem a mesma funcionalidade. Sites de diferentes versões na mesma hierarquia introduzem cenários de interoperabilidade. Versões posteriores do Gestor de Configuração incluem novas funcionalidades e resolvem problemas conhecidos. Para mais informações, consulte [Interoperabilidade entre diferentes versões](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Para obter mais informações sobre estas regras, consulte os passos de [Reparação para insights](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr)de gestão do Gestor de Configuração .

> [!TIP]
> Se já é cliente da Microsoft Unified ou microsoft Premier, inscreva-se no [Services Hub](https://serviceshub.microsoft.com/assessments/) para avaliações adicionais a pedido.
>
> Para obter mais informações sobre os Serviços microsoft, consulte [Soluções](https://www.microsoft.com/enterprise/services/support)de Suporte .

### <a name="proactive-maintenance"></a>Manutenção proativa

<!--1352184-->
As regras deste grupo destacam potenciais problemas de configuração para evitar através da manutenção de objetos do Gestor de Configuração.

- **Grupos de fronteira sem sistemas**de site atribuídos : Sem sistemas de site atribuídos, os grupos de fronteira só podem ser utilizados para a atribuição do local. Para mais informações, consulte [os grupos de fronteira configure](../deploy/configure/boundary-groups.md).  

- **Grupos de fronteira sem membros**: Os grupos de fronteira não são aplicáveis para a atribuição do site ou procura de conteúdo se não tiverem membros. Para mais informações, consulte [os grupos de fronteira configure](../deploy/configure/boundary-groups.md).  

- **Pontos**de distribuição não servindo conteúdo aos clientes : Pontos de distribuição que não serviram conteúdo aos clientes nos últimos 30 dias. Estes dados baseiam-se em relatórios de clientes do seu histórico de descarregamento. Para mais informações, consulte [Instalar e configurar pontos](../deploy/configure/install-and-configure-distribution-points.md)de distribuição .  

- Ativar a **Limpeza WSUS**: Verifica que ativou a opção de executar a limpeza wSUS nas propriedades do componente de ponto de atualização de software. Esta opção ajuda a melhorar o desempenho da WSUS. Para mais informações, consulte a [manutenção da atualização de Software.](../../../sum/deploy-use/software-updates-maintenance.md)  

- **Imagens**de arranque não utilizadas : Imagens de arranque não referenciadas para a utilização da bota PXE ou da sequência de tarefas. Para mais informações, consulte [Gerir imagens](../../../osd/get-started/manage-boot-images.md)de arranque .  

- Itens de **configuração não utilizados**: Itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias. Para mais informações, consulte Criar linhas de base de [configuração](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Atualize as fontes de cache dos pares para a versão mais recente do cliente do Gestor de Configuração:** Identifique os clientes que servem como fonte de cache de pares, mas não atualizaram a partir de uma versão cliente pré-1806. Os clientes pré-1806 não podem ser usados como fonte de cache para clientes que executam a versão 1806 ou mais tarde. Selecione **Tomar medidas** para abrir uma vista de dispositivo que exibe a lista de clientes.<!--1358008-->  

### <a name="security"></a>Segurança

Insights para melhorar a segurança das suas infraestruturas e dispositivos.

- O recuo da **NTLM está ativado:**<!--4572953--> A partir da versão 1906, esta regra deteta se permitiu o método de recuo de autenticação NTLM menos seguro para o site. Ao utilizar o método de pressão do cliente para instalar o cliente Do Gestor de Configuração, o site pode exigir a autenticação mútua da Kerberos. Esta melhoria ajuda a garantir a comunicação entre o servidor e o cliente. Para mais informações, consulte [Como instalar clientes com pressão](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)do cliente .

- **Versões**de clientes antimalware não suportadas : Mais de 10% dos clientes estão a executar versões de System Center Endpoint Protection que não são suportadas. Para mais informações, consulte [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Gestão simplificada

Insights que o ajudam a simplificar a gestão do seu ambiente no dia-a-dia.

- **Ligue o site à nuvem da Microsoft para atualizações**do Gestor de Configuração : Esta regra garante que o seu ponto de ligação ao Sistema de Configuração está ligado à nuvem da Microsoft nos últimos sete dias. Esta ligação é para descarregar conteúdo para atualizações regulares. Reveja DMPDownloader.log e hman.log. Para mais informações, consulte os requisitos de [acesso à Internet.](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)

- **Versões**de clientes não CB : Lista todos os clientes cujas versões não são uma construção de ramo atual (CB). Para mais informações, consulte [os clientes de Upgrade](../../clients/manage/upgrade/upgrade-clients.md).  

- **Atualizar os clientes para uma versão suportada**do Windows 10 : A partir da versão 1902, esta regra reporta sobre clientes que estão a executar uma versão do Windows 10 que já não é suportada. Também inclui clientes com uma versão do Windows 10 que está perto do fim do serviço (três meses).<!--3897268-->  

### <a name="software-center"></a>Centro de Software

Insights para gerir o Software Center.

- **Utilizadores diretos para o Centro de Software em vez do Catálogo de Aplicações**: Verifique se os utilizadores instalaram ou solicitaram aplicações do catálogo da aplicação nos últimos 14 dias. A principal funcionalidade do catálogo de aplicações está agora incluída no Software Center. O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [as funcionalidades deprecatadas.](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)  

- **Utilize a nova versão do Software Center**: A versão anterior do Software Center já não é suportada. Configurar clientes para utilizar o novo Centro de Software, permitindo que o cliente afina **o novo Software Center** no grupo De agente **informático.** Para mais informações, consulte [as definições do cliente](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Atualizações de Software

- **As definições do cliente não estão configuradas para permitir que os clientes descarreguem conteúdo delta**: Algumas atualizações de software sincronizadas no seu ambiente incluem conteúdo delta. Ative a definição do cliente, permita que os **clientes descarreguem conteúdo delta quando disponíveis**. Se não ativar esta definição, quando implementar estas atualizações, o cliente irá descarregar desnecessariamente mais conteúdo do que o necessário. Para mais informações, consulte [as definições do Cliente - Atualizações de software](../../clients/deploy/about-client-settings.md#software-updates).

- **Ativar a categoria de produtos de atualizações de software 'Windows 10, versão 1903 e mais tarde'**: Existe uma nova categoria de produto de atualizações de software para o Windows 10, versão 1903 e mais tarde. Se sincronizar as atualizações do Windows 10 e tiver o Windows 10, a versão 1903 ou clientes posteriores, selecione o **Windows 10, a versão 1903 e a** categoria de produto posterior nas propriedades dos componentes de ponto de atualização de software. Para mais informações, consulte classificações e produtos da[Configuração para sincronizar](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Insights relacionados com a implementação e manutenção do Windows 10. O grupo de informação de gestão do Windows 10 só está disponível quando mais de metade dos clientes estiverem a executar o Windows 7, Windows 8 ou Windows 8.1.

- **Configure os dados**de diagnóstico do Windows e a chave de ID comercial : Para utilizar dados do Desktop Analytics, configure os dispositivos com uma chave de ID comercial e permita a recolha de dados de diagnóstico. Detete os dispositivos do Windows 10 para um nível **melhorado (limitado)** ou superior. Para mais informações, consulte A partilha de [dados para Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Regras de insights de gestão do Windows 10

![Informações de gestão - Regras para o Windows 10](./media/Windows-10-insights-group.png)
