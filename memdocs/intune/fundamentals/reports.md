---
title: Microsoft Intune reports
titleSuffix: Microsoft Intune
description: Intune fornece tipos específicos de relatórios com pontos de vista focados que contêm dados consistentes e oportunos.
keywords: ''
author: erikre
ms.author: erikre
manager: dougeby
ms.date: 12/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d4e377e0cd9ad15d1d3a0ac9fb5c088dc1366d48
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80326752"
---
# <a name="intune-reports"></a>Relatórios do Intune
Os relatórios Microsoft Intune permitem-lhe monitorizar de forma mais eficaz e proativa a saúde e atividade dos pontos finais em toda a sua organização, e também fornece outros dados de reporte em toda a Intune. Por exemplo, poderá ver relatórios sobre a conformidade do dispositivo, a saúde do dispositivo e as tendências do dispositivo. Além disso, pode criar relatórios personalizados para obter dados mais específicos. 

> [!NOTE]
> As alterações de reporte intune serão lançadas gradualmente ao longo de um período de tempo para ajudá-lo a preparar e adaptar-se à nova estrutura.

Os tipos de relatórios são organizados nas seguintes áreas de foco:
- **Operacional** - Fornece dados atempados e direcionados que o ajudam a concentrar-se e a tomar medidas. Administradores, especialistas em assuntos e helpdesk acharão estes relatórios mais úteis.
- **Organizacional** - Fornece um resumo mais amplo de uma visão geral, como o estado de gestão de dispositivos. Gestores e administradores acharão estes relatórios mais úteis.
- **Histórico** - Fornece padrões e tendências ao longo de um período de tempo. Gestores e administradores acharão estes relatórios mais úteis.
- **Especialista** - Permite-lhe utilizar dados brutos para criar os seus próprios relatórios personalizados. Os administradores acharão estes relatórios mais úteis.

O quadro de relatórios proporciona uma experiência de reporte consistente e mais abrangente. Os relatórios disponíveis fornecem a seguinte funcionalidade:
- **Pesquisar e classificar** – Pode pesquisar e classificar todas as colunas, independentemente do tamanho do conjunto de dados.
- **Visualização** de dados – Pode digitalizar os seus dados com base na pagagem, página a página ou saltando para uma página específica.
- **Performance** - Você pode gerar e ver rapidamente relatórios criados a partir de grandes inquilinos.
- **Exportação** – Pode exportar rapidamente dados de reporte gerados por grandes inquilinos.

### <a name="who-can-access-the-data"></a>Quem pode aceder aos dados?

Os utilizadores com as seguintes permissões podem rever os registos:

- Administrador Global
- Administrador de Serviços do Intune
- Administradores designados para um papel intune com permissões **de leitura**

## <a name="non-compliant-devices-report-operational"></a>Relatório de dispositivos não conformes (Operacional)
Os dispositivos não conformes reportam dados normalmente utilizados por funções de Helpdesk ou administração para identificar problemas e ajudar a remediar problemas. Os dados encontrados nestes relatórios são oportunos, chama a atenção para comportamentos inesperados, e é suposto ser atorável. O relatório está disponível juntamente com a carga de trabalho, tornando os dispositivos não conformes acessíveis sem navegar longe de fluxos de trabalho ativos. Este relatório fornece capacidades de filtragem, pesquisa, paging e triagem. Além disso, podes perfurar para ajudar a resolver problemas.

Pode ver o relatório de **dispositivos não conformes** utilizando os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **dispositivos** > **Monitor de** > **dispositivos não conformes**.

    ![Relatório de dispositivos não conformes](./media/intune-reports/intune-reports-02.png)

    > [!TIP]
    > Se já utilizou anteriormente intune no portal Azure, encontrou os detalhes acima referidos no portal Azure, inserindo-se no [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) e selecionando**dispositivos não conformes**com o **dispositivo.** > 

## <a name="device-compliance-report-organizational"></a>Relatório de conformidade com dispositivos (Organizacional)

Os relatórios de conformidade do dispositivo devem ser de natureza ampla e fornecer uma visão mais tradicional de relatórios de dados para identificar métricas agregadas. Este relatório foi concebido para trabalhar com grandes conjuntos de dados para obter uma imagem completa do cumprimento do dispositivo. Por exemplo, o relatório de conformidade do dispositivo para a conformidade do dispositivo mostra todos os estados de conformidade para que os dispositivos dêem uma visão mais ampla dos dados, independentemente do tamanho do conjunto de dados. Este relatório mostra a desagregação completa dos registos, para além de uma visualização conveniente das métricas agregadas. Este relatório pode ser gerado aplicando filtros nele e selecionando o botão "Gerar relatório". Isto irá atualizar os dados para mostrar o estado mais recente com a capacidade de visualizar os registos individuais que compõem os dados agregados. Tal como a maioria dos relatórios no novo quadro, estes registos podem ser classificados e pesquisados para se concentrarem na informação de que necessita.

Para ver um relatório gerado do estado do dispositivo, pode utilizar os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Relatórios** para ver o resumo dos relatórios.
3. Selecione **Conformidade do dispositivo**.
4. Selecione o **estado de conformidade,** **OS**e filtros **de propriedade** para refinar o seu relatório.
5. Clique em **Gerar relatório** (ou **Gerar novamente)** para recuperar os dados atuais.

    ![Relatório de conformidade do dispositivo](./media/intune-reports/intune-reports-02a.png)

    > [!NOTE]
    > Este relatório de conformidade do **dispositivo** fornece um carimbo de tempo de quando o relatório foi gerado pela última vez. 

Para obter informações relacionadas, consulte Impor a conformidade com o [Microsoft Defender ATP com acesso condicional no Intune](../protect/advanced-threat-protection.md).

## <a name="reports-summary"></a>Resumo dos relatórios 

O relatório de conformidade do dispositivo está disponível como relatório sumário na carga de trabalho dos **Relatórios.** Utilize os seguintes passos para visualizar o relatório de conformidade do dispositivo:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Relatórios** para ver o resumo dos relatórios.

    ![Resumo dos Relatórios Intune](./media/intune-reports/intune-reports-01.png)

## <a name="device-compliance-trend-report-historical"></a>Relatório de tendências de conformidade do dispositivo (Histórico)

Os relatórios de tendências de conformidade do dispositivo são mais propensos a serem usados por administradores e arquitetos para identificar tendências de longo prazo para o cumprimento do dispositivo. Os dados agregados são apresentados ao longo de um período de tempo, e são úteis para tomar futuras decisões de investimento, impulsionar melhorias no processo ou levar à investigação de quaisquer anomalias. Os filtros também podem ser aplicados para ver tendências específicas. Os dados fornecidos por este relatório são uma imagem do estado atual do arrendatário (quase em tempo real). 

Um relatório de tendência de conformidade do dispositivo para as tendências de conformidade do dispositivo pode mostrar a tendência dos estados de conformidade do dispositivo durante um período de tempo. Pode identificar onde ocorreram picos de conformidade e concentrar o seu tempo e esforço em conformidade.

Pode ver o relatório **Tendências** utilizando os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Relatórios** > **Tendências** para ver a conformidade do dispositivo ao longo de uma tendência de 60 dias.

    ![Relatório de tendências insintonizado](./media/intune-reports/intune-reports-03.png)

## <a name="azure-monitor-integration-reports-specialist"></a>Relatórios de integração do Monitor Azure (Especialista)
Pode personalizar os seus próprios relatórios para obter os dados que deseja. Os dados nos seus relatórios estarão opcionalmente disponíveis através [do Monitor Azure](https://docs.microsoft.com/azure/azure-monitor/overview) utilizando livros de [log analytics](reports.md#log-analytics) e [monitor azure.](reports.md#workbooks) Estas soluções permitem criar consultas personalizadas, configurar alertas e fazer dashboards para mostrar os dados de conformidade do dispositivo da forma que pretende. Além disso, pode reter os registos de atividade na sua conta de armazenamento Azure, integrar-se com os relatórios utilizando ferramentas de informação de segurança e gestão de [eventos (SIEM)](https://docs.microsoft.com/microsoft-365/security/office-365-security/siem-server-integration)e correlacionar os relatórios aos registos de atividade da Azure AD. Os livros de trabalho Do Monitor Azure podem ser utilizados para além da importação de tabliers para necessidades de reporte personalizados.

> [!NOTE]
> A funcionalidade complexa de reporte requer uma subscrição do Azure.

Um relatório especializado de exemplo iria corelate dados de propriedade do dispositivo com dados de inscrição da plataforma em um relatório personalizado. Em seguida, este relatório personalizado poderia ser exibido num painel de instrumentos existente no portal Azure Ative Diretório.

Pode criar e ver relatórios personalizados utilizando os seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Relatórios** > **As definições de** diagnóstico adicionam uma [definição de diagnóstico](reports.md#diagnostic-settings).

    ![Resumo dos Relatórios Intune](./media/intune-reports/intune-reports-04.png)

3. Clique em **adicionar definição de diagnóstico** para visualizar o painel de definições de **diagnóstico.** 
4. Adicione um **Nome** para as definições de diagnóstico. 
5. Selecione as definições **enviar para registar análises** e **dispositivosComplianceOrg.**

    ![Resumo dos Relatórios Intune](./media/intune-reports/intune-reports-04a.png)

6. Clique em **Guardar**.
7. Em seguida, selecione **log analytics** para criar e executar uma nova consulta de log usando [Log Analytics](reports.md#log-analytics).

   ![Log Analytics - Consulta de registo](./media/intune-reports/intune-reports-05.png)

8. Selecione **Livros** para criar ou abrir um relatório interativo utilizando [livros de trabalho do Monitor Azure](reports.md#workbooks).

   ![Livros - Relatórios interativos](./media/intune-reports/intune-reports-07.png)

### <a name="diagnostic-settings"></a>Definições de diagnóstico
Cada recurso Azure requer a sua própria configuração de diagnóstico. A definição de diagnóstico define o seguinte para um recurso:

- Categorias de registos e dados métricos enviados para os destinos definidos na definição. As categorias disponíveis variarão para diferentes tipos de recursos.
- Um ou mais destinos para enviar os registos. Os destinos atuais incluem log analytics workspace, Event Hubs e Armazenamento Azure.
- Política de retenção de dados armazenados no Armazenamento Azure.

Uma única definição de diagnóstico pode definir um dos destinos. Se quiser enviar dados para mais do que um tipo de destino particular (por exemplo, dois espaços de trabalho diferentes do Log Analytics), então crie várias configurações. Cada recurso pode ter até 5 configurações de diagnóstico.

Para mais informações, sobre configurações de diagnóstico, consulte [Criar definição de diagnóstico para recolher registos e métricas](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings)da plataforma em Azure .

### <a name="log-analytics"></a>Log Analytics
O Log Analytics é a principal ferramenta no portal Azure para escrever consultas de registo e analisar interativamente os resultados das consultas. Mesmo que uma consulta de log seja usada em outro lugar do Monitor Azure, você normalmente escreverá e testará a consulta usando log analytics. Para mais detalhes sobre a utilização do Log Analytics e a criação de consultas de registo, consulte a [visão geral das consultas de registo no Monitor Azure](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview). 

### <a name="workbooks"></a>Livros
Os livros de trabalho combinam texto, consultas de Análise, Métricas Azure e parâmetros em relatórios interativos ricos. Os livros de recção são editáveis por quaisquer outros membros da equipa que tenham acesso aos mesmos recursos Do Azure. Para obter mais informações sobre livros, consulte [os livros do Monitor Do Azure.](https://docs.microsoft.com/azure/azure-monitor/app/usage-workbooks) Além disso, pode trabalhar e contribuir para modelos de livro. Para mais informações, consulte os modelos do [livro do Monitor Azure](https://go.microsoft.com/fwlink/?linkid=867045).

## <a name="next-steps"></a>Passos seguintes 

Saiba mais sobre as seguintes tecnologias:
- [Blog - Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)
- [Azure Monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor)
- [O que é o Log Analytics?](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview#what-is-log-analytics)
- [Registar consultas](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview)
- [Começar com Log Analytics no Monitor Azure](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal)
- [Livros Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/app/usage-workbooks)
- [Ferramentas de informação de segurança e gestão de eventos (SIEM)](https://docs.microsoft.com/microsoft-365/security/office-365-security/siem-server-integration)
