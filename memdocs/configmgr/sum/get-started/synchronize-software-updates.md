---
title: Gerir a sincronização de atualizações de software
titleSuffix: Configuration Manager
description: Utilize estes passos para agendar a sincronização de atualizações de software, iniciar manualmente a sincronização de atualizações de software e monitorizar a sincronização das atualizações de software.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712681"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a> Sincronizar atualizações de software

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Sincronização de atualização de software no Configurmanager é o processo de recuperação dos metadados de atualização de software que satisfaz os critérios que configura. Isto inclui produtos específicos, classificações e línguas. Normalmente, o ponto de atualização de software no site da administração central, ou num site primário autónomo, recupera os metadados do Microsoft Update. Em seguida, o site de alto nível enviará um pedido de sincronização para outros sites. Quando um site recebe o pedido de sincronização do site principal, o ponto de atualização do software para o site recupera metadados de atualizações de software a partir da sua fonte de [sincronização](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)a montante . Para obter mais informações sobre o processo de sincronização da atualização de software, consulte a sincronização das atualizações de [Software.](../understand/software-updates-introduction.md#BKMK_Synchronization)

Configura a sincronização da atualização de software para executar uma programação nas propriedades para o ponto de atualização de software no site de alto nível. Uma vez configurado o calendário de sincronização, normalmente não alterará o horário como parte das operações normais. No entanto, pode iniciar manualmente a sincronização da atualização de software quando for necessário.

  > [!NOTE]  
  >  Os pontos de atualização de software devem ser ligados à sua fonte de sincronização a montante para sincronizar atualizações de software. Se um ponto de atualização de software estiver desligado da respetiva origem de sincronização a montante, poderá utilizar o método de exportação e importação para sincronizar as atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Agendar atualizações de software sincronização
Quando configura uma programação para atualizações de software sincronizada, o ponto de atualização de software de alto nível começa a sincronizar com o Microsoft Update na data e hora programadas. A programação personalizada permite sincronizar as atualizações de software numa data e hora quando as exigências do servidor, servidor do servidor, servidor do site e rede do Windows Server (WSUS) são baixas. Por exemplo, pode definir a programação para que as atualizações de software sejam sincronizadas todas as semanas às 2:00 da manhã. Durante a sincronização agendada, todas as alterações nos metadados de atualizações de software desde a última sincronização agendada são inseridas na base de dados do site. Isto inclui novos metadados de atualizações de software ou metadados que foram modificados, removidos ou que agora expiraram.

Utilize os seguintes procedimentos no site de alto nível para agendar a sincronização de atualizações de software.  

#### <a name="to-schedule-software-updates-synchronization"></a>Para agendar a sincronização de atualizações de software  

  1.  Na consola do Configuration Manager, clique em **Administração**.  

  2.  Na área de trabalho Administração, expanda **Configuração do Site**e clique em **Sites**.  

  3.  No painel de resultados, clique no site de administração central ou no site autónomo principal.  

  4.  No separador **Home Page** , no grupo **Definições** , expanda **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.  

  5.  Na caixa de diálogo Propriedades do Componente do Ponto de Atualização de Software, selecione **Ativar sincronização num agendamento**e, em seguida, especifique o agendamento da sincronização.  

## <a name="manually-start-software-updates-synchronization"></a>Iniciar manualmente atualizações de software sincronização
Pode iniciar manualmente atualizações de software sincronizada no site de alto nível na consola Do Gestor de Configuração a partir do nó de **Atualizações** de Software all software no espaço de trabalho da Biblioteca de **Software.**  

Utilize os seguintes procedimentos no site de alto nível para iniciar manualmente a sincronização de atualizações de software.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Para iniciar manualmente atualizações de software sincronização  

1. Na consola De Configuração Manager que está ligada ao site da administração central ou ao site primário autónomo, clique na Biblioteca de **Software**.  

2. Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software** ou em **Grupos de Atualizações de Software**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Sincronizar Atualizações de Software**. Clique em **Sim** na caixa de diálogo para confirmar que quer iniciar o processo de sincronização.  

   Depois de iniciar o processo de sincronização no ponto de atualização do software, pode monitorizar o processo de sincronização a partir da consola Do Gestor de Configuração para todos os pontos de atualização de software da sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software.  


## <a name="monitor-software-updates-synchronization"></a>Monitorizar atualizações de software sincronização
Depois de iniciar o processo de sincronização, pode utilizar a consola 'Gestor de Configuração' para monitorizar o processo para todos os pontos de atualização de software da sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software. Para obter mais informações sobre a monitorização de atualizações de software, incluindo o processo de sincronização, consulte [as atualizações](../deploy-use/monitor-software-updates.md)de software do Monitor .

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorizar o processo de sincronização de atualizações de software  

1. Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2. No espaço de trabalho **de monitorização,** clique no Estado de **Sincronização do Ponto**de Atualização do Software .  

   Os pontos de atualização de software na hierarquia do Gestor de Configuração são apresentados no painel de resultados. A partir desta vista, poderá monitorizar o estado de sincronização de todos os pontos de atualização de software. Quando quiser obter informações mais detalhadas sobre o processo de sincronização, pode consultar o ficheiro wsyncmgr.log que está localizado em <*ConfigMgrInstallationPath*>\Logs em cada servidor do site.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importa atualizações do Catálogo de Atualizações da Microsoft

O Ponto de Atualização de Software de alto nível utiliza o WSUS para obter informações sobre atualizações de software da Microsoft para o 'Gestor de Configuração'. Ocasionalmente, pode necessitar de uma atualização que não se sincroniza automaticamente no WSUS para os seus produtos e classificações selecionados, mas que está disponível no Catálogo de [Atualizações](https://catalog.update.microsoft.com)da Microsoft . As atualizações que não sincronizam automaticamente no WSUS são normalmente destinadas a resolver problemas altamente específicos. Normalmente, se uma atualização estiver disponível no catálogo, pode importá-la para wSUS. Em seguida, pode sincronizá-lo no 'Gestor de Configuração' e implementá-lo como qualquer outra atualização.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Para importar uma atualização do Catálogo de Atualizações da Microsoft

1. Abra a consola de administração WSUS e conecte-a ao servidor WSUS de alto nível na sua hierarquia.
   - Se o Internet Explorer não for o navegador web padrão do computador, detetetei-o temporariamente como padrão.
2. Clique em **Atualizações** ou clique no nome do seu servidor WSUS. 
3. No painel **De Ações,** selecione **Import Updates...** que abrirá uma janela de navegador para o Catálogo de [Atualizações](https://catalog.update.microsoft.com)da Microsoft .
   ![Selecione atualizações de importação na consola WSUS](media/wsus-console-import-updates.png)
4. Se solicitado, instale o comando do Microsoft Update Catalog ActiveX. O controlo deve ser instalado para importar atualizações para o WSUS. 
5. Na janela do navegador, procure a atualização que deseja. Clique no botão **Adicionar*** para adicioná-lo ao cesto.
6. Clique no **cesto de visualização**. Certifique-se de que a opção **de importar diretamente para os Serviços** de Atualização do Servidor do Windows está selecionada. Em seguida, clique **em Importar**.
    ![Atualização de importação do catálogo para o WSUS](./media/import-catalog-update-into-wsus.png)
7. Assim que a importação estiver concluída, clique em **Fechar** a janela do navegador.
     - Redefinir o seu navegador predefinido, se necessário.
8. Sincronizar o ponto de atualização do software do Gestor de Configuração.


## <a name="next-steps"></a>Passos seguintes
Depois de sincronizar as atualizações de software pela primeira vez, ou depois de existirem novas classificações ou produtos disponíveis, tem de [configurar as novas classificações e produtos](configure-classifications-and-products.md) para sincronizar as atualizações de software com os novos critérios.

Depois de sincronizar as atualizações de software com os critérios de que necessita, [gere as definições para atualizações](manage-settings-for-software-updates.md)de software .  
