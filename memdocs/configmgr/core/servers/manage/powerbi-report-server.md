---
title: Integrar com o Power BI Report Server
titleSuffix: Configuration Manager
description: Integre o Power BI Report Server com relatório de configuração para visualização moderna e melhor desempenho.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c596ba410adc979b92a000c28d815e89695a9b0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713668"
---
# <a name="integrate-with-power-bi-report-server"></a>Integrar com o Power BI Report Server

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3721603-->

A partir da versão 2002, pode integrar o [Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) com relatórios do Gestor de Configuração. Esta integração confere-lhe uma visualização moderna e um melhor desempenho. Adiciona suporte de consola para relatórios Power BI semelhantes ao que já existe com os Serviços de Reporte de Servidores SQL.

Guarde os ficheiros de relatório sinuoso Power BI (. PBIX) e desloque-os para o Servidor de Relatório power BI. Este processo é semelhante ao dos ficheiros de relatórios do SQL Server Reporting Services (. RDL). Também pode lançar os relatórios no navegador diretamente a partir da consola 'Gestor de Configuração'.

## <a name="prerequisites"></a>Pré-requisitos

- Licença power BI Report Server. Para mais informações, consulte [o Licensing Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Baixe [o Microsoft Power BI Report Server-September 2019](https://www.microsoft.com/download/details.aspx?id=57270), ou mais tarde.

    > [!NOTE]
    > Não instale o Power BI Report Server imediatamente. Para obter o processo adequado baseado no seu ambiente, consulte [Configurar o ponto de serviços de reporte](#configure-the-reporting-services-point).

- Baixe [o Microsoft Power BI Desktop (Otimizado para Power BI Report Server - setembro de 2019)](https://www.microsoft.com/download/details.aspx?id=57271), ou mais tarde.

    > [!IMPORTANT]
    > - Utilize apenas versões do Power BI Desktop do [Microsoft Download Center](https://www.microsoft.com/download/), não utilize uma versão da Microsoft Store.
    > - Utilize apenas uma versão do [Power BI Desktop que indique que está **otimizado para o Power BI Report Server**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

- A integração do Power BI utiliza a mesma administração baseada em papéis para reportar.

## <a name="configure-the-reporting-services-point"></a>Configure o ponto de serviços de reporte

Este processo varia consoante já tenha este papel no site.

### <a name="you-have-a-reporting-services-point"></a>Tem um ponto de serviço sinuoso

Utilize este processo apenas se já tiver um ponto de serviços de reporte no site. Faça todos os passos deste processo no mesmo servidor:

1. No Gestor de **Configuração**do Servidor de Relatórios, volte a fazer o back the **Crypton Keys**. Para mais informações, consulte [as teclas de encriptação SSRS - Back Up e Restore CryptCrypt Cryption Keys](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Se saltar este passo, perderá o acesso a quaisquer relatórios personalizados nos Serviços de Relato do Servidor SQL.

1. Remova a função de ponto de ponto dos serviços de reporte do site.

1. Desinstale os Serviços de Reporte do Servidor SQL, mas mantenha a base de dados.

1. Instalar o Power BI Report Server.

1. Configure o servidor de relatório power BI

    1. Utilize a base de dados do servidor de relatórios anterior.

    1. Utilize **o Gestor de Configuração do Servidor de Relatórios** para restaurar as **teclas de encriptação**.

1. Adicione a função de ponto de ponto de serviços de reporte no Gestor de Configuração.

### <a name="you-dont-have-a-reporting-services-point"></a>Não tem um ponto de serviço de reporte.

Utilize este processo apenas se ainda não tiver um ponto de serviços de reporte no site. Faça todos os passos deste processo no mesmo servidor:

1. Instalar o Power BI Report Server.

2. Adicione a função de ponto de ponto de serviços de reporte no Gestor de Configuração. Para mais informações, consulte [o relatório Configure](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Configure a consola de Gestor de Configuração

1. Num computador que tenha a consola Do Gestor de Configuração, atualize a consola do Gestor de Configuração para a versão mais recente.

1. Instale o Power BI Desktop. Certifique-se de que a língua é a mesma.

1. Depois de instalar, lance o Power BI Desktop pelo menos uma vez antes de abrir a consola 'Gestor de Configuração'.

## <a name="create-power-bi-reports"></a>Criar relatórios power bi

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o novo nó de **Relatórios power bi.**

1. Na fita, selecione **Criar Relatório**. Esta ação abre o Power BI Desktop.

1. Crie um relatório no Power BI Desktop.

    - No Power BI Desktop, quando se ligar a uma fonte de dados, selecione **DirectQuery** para as definições de Ligação.

    - Utilize apenas pontos de vista SQL suportados nestes relatórios. Para mais informações, consulte [criar relatórios personalizados utilizando as vistas do Servidor SQL no Gestor](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)de Configuração .

1. Quando o relatório estiver pronto a guardar, vá ao menu **'Ficheiro',** selecione **Guardar como**, em seguida, escolha power BI **Report Server**.

1. Na janela **power bi report server Selection,** introduza o URL para o ponto de serviços de reporte como o novo endereço do servidor de **relatório**. Por exemplo, `https://rsp.contoso.com/Reports`.

Na consola Do Gestor de Configuração, vê o novo relatório na lista de Relatórios power bi.

## <a name="next-steps"></a>Passos seguintes

Depois de criar um relatório, utilize as seguintes ações na consola 'Gestor de Configuração':

- **Executar no Browser**: Abre o relatório Power BI no navegador web. Partilhe este URL com outros, por exemplo:`https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Só é possível visualizar estes relatórios no navegador web.

- **Editar**: Faça alterações no relatório no Power BI Desktop. Para um relatório existente, utilize a opção **Guardar** para guardar alterações no servidor de relatório.

Para obter mais informações sobre ficheiros de registo para reportar, consulte a referência do [ficheiro Deregisto - Reportar](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
