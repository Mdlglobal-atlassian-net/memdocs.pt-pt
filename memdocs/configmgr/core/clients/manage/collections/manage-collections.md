---
title: Gerir coleções
titleSuffix: Configuration Manager
description: Faça tarefas comuns de gestão de coleções em 'Gestor de Configuração'.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714340"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Como gerir coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações de visão geral neste artigo para ajudá-lo a executar tarefas de gestão para coleções em 'Gestor de Configuração'.  

> [!NOTE]  
>  Para obter informações sobre como criar coleções do Gestor de Configuração, consulte [como criar coleções.](create-collections.md)



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a>Como gerir as coleções de dispositivos  

Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Dispositivos**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  


#### <a name="show-members"></a>Mostrar Membros
Apresenta todos os recursos que são membros da coleção selecionada num nó temporário sob o nó **Dispositivos** .


#### <a name="add-selected-items"></a>Adicionar Itens Selecionados
Fornece as seguintes opções: 

- **Adicione itens selecionados à coleção de dispositivos existentes**: Abre a caixa de diálogo **Select Collection.** Selecione a coleção à qual pretende adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .  

- **Adicione itens selecionados à new device collection**: Abre o Assistente de Recolha de **Dispositivos Create** onde pode criar uma nova coleção. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .  


Para mais informações, consulte [Como criar coleções.](create-collections.md)


#### <a name="install-client"></a>Instalar Cliente
Abre o **Assistente de Cliente de Instalação.** Este assistente utiliza a instalação de impulso do cliente para instalar um cliente de Gestor de Configuração em todos os computadores da coleção selecionada. Para mais informações, consulte a [instalação do impulso do Cliente.](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)


#### <a name="run-script"></a>Executar script
Abre o assistente **do Run Script** para executar um script PowerShell em todos os clientes da coleção. Para mais informações, consulte [Criar e executar scripts PowerShell](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Gerir Pedidos de Afinidade
Abre a caixa de diálogo **'Gerir dispositivo utilizador'.** Aprove ou rejeite pedidos pendentes para estabelecer afinidades de dispositivos de dispositivos na recolha selecionada. Para mais informações, consulte [utilizadores e dispositivos do Link com afinidade](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) do dispositivo do utilizador


#### <a name="clear-required-pxe-deployments"></a>Limpar as Implementações de PXE Necessárias
Limpa quaisquer implementações de arranque PXE necessárias de todos os membros da coleção selecionada. Para mais informações, consulte [Use PXE para implementar o Windows sobre a rede](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Atualizar Associação
Avalia a associação da coleção selecionada. Para coleções com muitos membros, esta atualização pode demorar algum tempo a concluir. Utilize a ação **Atualizar** para atualizar a apresentação com os novos membros de coleções após a atualização estar concluída.


#### <a name="add-resources"></a>Adicionar Recursos
Abre a caixa de diálogo **Add Resources to Collection.** Procure novos recursos para adicionar à coleção selecionada. O ícone da coleção selecionada apresenta um símbolo de ampulheta enquanto a atualização está em andamento.


#### <a name="client-notification"></a>Notificação de cliente
Para mais informações, consulte [notificações do Cliente](../client-notification.md).


#### <a name="endpoint-protection"></a>Endpoint Protection
Para mais informações, consulte [notificações do Cliente](../client-notification.md).


#### <a name="export"></a>Exportar
Abre o Assistente de Recolha de **Exportação** que o ajuda a exportar esta coleção para um ficheiro De formato de Objeto Gerido (MOF). Este ficheiro pode então ser arquivado ou importado noutro site do Gestor de Configuração. Quando se exporta uma coleção, as coleções referenciadas não são exportadas. Uma coleção referenciada é referenciada pela coleção selecionada através da utilização de uma regra **Incluir** ou **Excluir.**


#### <a name="copy"></a>Copiar
Cria uma cópia da coleção selecionada. A nova coleção utiliza a coleção selecionada como uma coleção restritiva.


#### <a name="refresh"></a>Atualizar
Refresque a vista.


#### <a name="delete"></a>Eliminar
Elimina a coleção selecionada. Também pode eliminar todos os recursos na coleção da base de dados do site. 

Não é possível eliminar as coleções incorporadas no Gestor de Configuração. Para obter uma lista das coleções incorporadas, consulte [Introdução às coleções.](introduction-to-collections.md#built-in-collections)


#### <a name="simulate-deployment"></a>Simular Implementação
Abre o Assistente de Implementação de **Aplicações simulação**. Este assistente permite-lhe testar os resultados de uma implementação de aplicação sem instalar ou desinstalar a aplicação. Para mais informações, consulte [como simular implementações de aplicações](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Implementação
Apresenta as seguintes opções:  

- **Aplicação**: Abre o **Assistente de Software de Implantação**. Selecione e configure uma implementação de aplicação para a coleção selecionada. Para mais informações, consulte [Como implementar aplicações](../../../../apps/deploy-use/deploy-applications.md).  

- **Programa**: Abre o **Assistente de Software de Implantação**. Selecione e configure um pacote e implementação de programa para a coleção selecionada. Para mais informações, consulte [Pacotes e programas.](../../../../apps/deploy-use/packages-and-programs.md)  

- **Linha de plano de configuração**: Abre a caixa de diálogo de configuração de configuração de **configuração.** Configure a implementação de uma ou mais linhas de base de configuração para a coleção selecionada. Para mais informações, consulte como implementar as [linhas de base de configuração](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Sequência de tarefas**: Abre o **Assistente de Software de Implantação**. Selecione e configure uma sequência de tarefas para a coleção selecionada. Para obter mais informações, consulte Gerir sequências de [tarefas para automatizar tarefas](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Atualizações de software**: Abre o Assistente de Atualizações de **Software de Implementação**. Configure a implementação de atualizações de software para recursos na coleção selecionada. Para mais informações, consulte [Gerir atualizações](../../../../sum/understand/software-updates-introduction.md)de software .  


#### <a name="clear-server-group-deployment-locks"></a>Bloqueios de implementação de grupo de servidor claro
Liberte manualmente todos os bloqueios de implementação do grupo de servidores para a recolha. Para mais informações, consulte [O Serviço de um grupo de servidores](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Mover
Mova a coleção selecionada para outra pasta no nó de **Recolha de Dispositivos.** 


#### <a name="properties"></a>Propriedades
Para mais informações, consulte [propriedades da Coleção.](#BKMK_CollProp)  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a>Como gerir as coleções dos utilizadores  

Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Utilizadores**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

> [!Note]  
> As seguintes ações estão disponíveis nas coleções dos utilizadores, mas os comportamentos são os mesmos que com as coleções de dispositivos. Para além de se aplicarem às coleções dos utilizadores e aos utilizadores no seu interior. Para mais informações, consulte a ação correspondente no âmbito de Como gerir as [coleções de dispositivos](#bkmk_device).  

- **Mostrar Membros**  
- **Adicionar Itens Selecionados**  
    - **Adicione itens selecionados à coleção de utilizadores existentes**  
    - **Adicione itens selecionados à nova coleção de utilizadores**  
- **Gerir Pedidos de Afinidade**  
- **Atualizar Associação**  
- **Adicionar Recursos**  
- **Exportar**  
- **Copiar**  
- **Atualizar**  
- **Eliminar**  
- **Simular Implementação**  
- **Implementar**  
    - **Aplicação**  
    - **Programa**  
    - **Linha de Base de Configuração**
- **Mover**  
- **Propriedades**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Propriedades da coleção  

Quando abrir a caixa de diálogo **Properties** para uma recolha, vista e configure as seguintes opções:  

#### <a name="general"></a>Geral
Ver e configurar informações gerais sobre a coleção selecionada, incluindo o nome da recolha e a recolha limitativa.

#### <a name="membership-rules"></a>Regras de Associação
Configure as regras de adesão que definem a adesão a esta coleção. Para mais informações, consulte [Como criar coleções.](create-collections.md)  

#### <a name="power-management"></a>Gestão de Energia
Configure os planos de gestão de energia que atribuiu aos computadores da coleção selecionada. Para mais informações, consulte [Introdução à gestão de energia.](../power/introduction-to-power-management.md)  

#### <a name="deployments"></a>Implementações
Exibe qualquer software que tenha implantado para membros da coleção selecionada.  

#### <a name="maintenance-windows"></a>Janelas de manutenção
Ver e configurar janelas de manutenção que são aplicadas aos membros da coleção selecionada. Para mais informações, consulte [Como utilizar as janelas de manutenção](use-maintenance-windows.md).

#### <a name="collection-variables"></a>Variáveis da Coleção
Configure variáveis que se aplicam a esta coleção e podem ser usadas por sequências de tarefas. Para mais informações, consulte [Como definir variáveis de sequência de tarefas](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).  

#### <a name="distribution-point-groups"></a>Grupos de Pontos de Distribuição
Associe um ou mais grupos de pontos de distribuição aos membros da coleção selecionada. Para mais informações, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md)

#### <a name="aad-group-sync"></a>Sincronização do Grupo AAD
Sincronizar os resultados da subscrição da coleção aos Grupos de Diretório Sonérórios Ativos da Azure. Esta sincronização é uma [funcionalidade de pré-lançamento](../../../servers/manage/pre-release-features.md) a partir da versão 1906. Para mais informações, consulte [Criar coleções.](create-collections.md#bkmk_aadcollsync)

#### <a name="security"></a>Segurança
Apresenta os utilizadores administrativos que têm permissões para a coleção selecionada a partir de funções e âmbitos de segurança associados. Para obter mais informações, consulte os [fundamentos da administração baseada no papel.](../../../understand/fundamentals-of-role-based-administration.md)  

#### <a name="alerts"></a>Alertas 
Configure quando os alertas forem gerados para o estado do cliente e proteção de pontofinal. Para mais informações, consulte [Como configurar o estado](../../deploy/configure-client-status.md) do cliente e como monitorizar a [Proteção do Ponto Final](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Usando powershell

PowerShell pode ser usado para gerir coleções.  Para obter mais informações, consulte:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [Coleção New-CM](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remover-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Regra de adições CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Regra de remoção de membros da cmcollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeuser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remover CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Regra de remoção de membros diretos da CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcluiMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Grupo Add-CMCollectiontoDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remover-CMCollectionIncluMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remover-CMCollectionExcluiRegra de Membership](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remoção-CMCollectionFromAdministrativeuser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
