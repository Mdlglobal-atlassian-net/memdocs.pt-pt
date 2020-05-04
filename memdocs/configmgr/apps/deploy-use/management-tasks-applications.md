---
title: Tarefas de gestão de candidaturas
titleSuffix: Configuration Manager
description: Gerir aplicações e tipos de implementação do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0896204fa994643064676b55b20d63d349c4098b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710119"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Tarefas de gestão para aplicações de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para ajudá-lo a gerir aplicações e tipos de implementação do Gestor de Configuração.  

Para ajudar a criar aplicações e tipos de implementação, consulte [Criar aplicações.](../../apps/deploy-use/create-applications.md)  

> [!IMPORTANT]  
>  Dependendo do tipo de aplicação ou tipo de implementação, algumas opções de gestão podem não estar disponíveis.  

##  <a name="manage-applications"></a>Gerir aplicações  
 No espaço de trabalho da Biblioteca de **Software,** expandir aplicações de **gestão** > de**aplicações,** escolher a aplicação para gerir e, em seguida, escolher uma tarefa de gestão.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Gerir Contas de Acesso**|Abre a caixa de diálogo **Gerir Contas de Acesso** que lhe permite especificar o nível de acesso permitido para o conteúdo associado à aplicação selecionada.|  
|**Criar ficheiro de conteúdo pré-estágio**|Abre o **Assistente para Criar Ficheiro de Conteúdo Pré-Configurado** que lhe permite gerir a distribuição do conteúdo por pontos de distribuição remotos. Quando o agendamento e limitação não fornecem uma solução válida para o ponto de distribuição remoto, é possível pré-configurar o conteúdo do ponto de distribuição.<br /><br /> Ver Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)|  
|**Histórico de Revisão**|Abre a caixa de diálogo histórico de revisão de **aplicações** que lhe permite visualizar as propriedades das revisões que foram feitas a esta aplicação, eliminar revisões antigas de aplicações e restaurar versões antigas desta aplicação.<br /><br /> Ver [Como rever e substituir aplicações.](../../apps/deploy-use/revise-and-supersede-applications.md)|  
|**Criar Tipo de Implementação**|Abre o **Assistente do Tipo de Implementação Create** que lhe permite adicionar um novo tipo de implementação à aplicação selecionada.<br /><br /> Ver [Criar aplicações](../../apps/deploy-use/create-applications.md).|  
|**Estatísticas de Atualização**|Atualiza as informações que são apresentadas no nó **Implementações** da área de trabalho **Monitorização** sobre as implementações desta aplicação.<br /><br /> Consulte [as aplicações monitorada na consola 'Gestor de Configuração'.](../../apps/deploy-use/monitor-applications-from-the-console.md)|  
|**Restabelecer**|Repõe um requerimento que foi retirado utilizando a tarefa de gestão da **Reforma.**|  
|**Extinguir**|Quando se reforma uma candidatura, já não está disponível para implementação, mas a aplicação e implementação do pedido não são eliminadas. As cópias existentes desta aplicação que tenham sido instaladas em computadores cliente não serão removidas. Quaisquer revisões à aplicação serão eliminadas do Configuration Manager após 60 dias. Mas as cópias instaladas da aplicação não são removidas.<br /><br /> Para eliminar uma aplicação, primeiro deve retirar a aplicação, eliminar todas as implementações, remover referências à aplicação por outras implementações e, em seguida, apagar todas as revisões da aplicação.<br /><br /> Consulte [aplicações Revise e supersede](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportar**|Abre o **Assistente de Aplicações** de Exportação que lhe permite exportar as aplicações selecionadas para um ficheiro .zip que pode então arquivar ou instalar noutro site. Se optar por exportar conteúdo de aplicação, será criada uma pasta que tenha o conteúdo.<br /><br /> Você também pode exportar dependências de aplicações, relacionamentos e condições de supersedência, e conteúdo para a aplicação e suas dependências.<br /><br /> O cmdlet Windows PowerShell, **Export-CMApplication,** faz a mesma função. Para mais informações, consulte [a Export-CMApplication](https://go.microsoft.com/fwlink/p/?LinkID=258880) no Microsoft System Center 2012 Configuration Manager SP1 cmdlet documentação de referência.|  
|**Eliminar**|Elimina a aplicação selecionada atualmente.<br /><br /> Não é possível eliminar uma aplicação se outras aplicações dependerem da mesma, se tiver uma implementação ativa ou se tiver sequências de tarefas dependentes.|  
|**Simular Implementação**|Abra o **Assistente de Simulação de Implementação da Aplicação** para testar os resultados da implementação de uma aplicação em computadores sem instalar ou desinstalar a aplicação.<br /><br /> Ver [Simular implementações de aplicações](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Implementar**|Abre o **Assistente de Implementação de Software** para poder implementar a aplicação selecionada em conjuntos de computadores da hierarquia.<br /><br /> Ver [Aplicações de implantação](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuir Conteúdo**|Abre o **Assistente para Distribuir Conteúdo** para poder copiar o conteúdo da aplicação selecionada em pontos de distribuição da hierarquia.<br /><br /> Ver Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)|  
|**Ver Relações**|Mostra um diagrama gráfico das relações das aplicações selecionadas a outras aplicações. Selecione uma das seguintes opções:<br><br><ul><li>**Dependência** – Mostra aplicações que dependem da aplicação selecionada e das aplicações de que a aplicação selecionada depende.</li><li>**Supersedência** – Mostra aplicações que a aplicação selecionada substitui e aplica ções pelas quais a aplicação selecionada é substituído.</li><li>**Condições Globais** – Mostra as condições globais que são referenciadas por esta aplicação.</li></ol><br /> Consulte [revise e substitui aplicações](../../apps/deploy-use/revise-and-supersede-applications.md) e [crie condições globais.](../../apps/deploy-use/create-global-conditions.md)|  
|**Aplicações de cópia**|Copiar ou duplicar, aplicações do Gestor de Configuração para criar uma nova. Esta ação é útil para testar algo ou quando você precisa criar uma aplicação semelhante. O site cria uma nova aplicação, com **-cópia** anexada ao nome. Enquanto o site copia a maioria dos metadados para a nova aplicação, não copia nenhuma implementação.|

##  <a name="manage-deployment-types"></a>Gerir tipos de implementação  
 No espaço de trabalho da Biblioteca de **Software,** expandir a Gestão de **Aplicações,** escolher **Aplicações,** e depois escolher a aplicação que tem o tipo de implementação que pretende gerir. No painel de detalhes, escolha o separador Tipos de **Implementação,** escolha o tipo de implementação que pretende gerir e, em seguida, escolha uma tarefa de gestão.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Aumentar Prioridade**|Aumenta a prioridade do tipo de implementação selecionado. Os tipos de implementação são avaliados por ordem. Quando um tipo de implantação satisfaz os requisitos especificados, será executado e, em seguida, nenhum outro tipo de implementação na lista de prioridades será avaliado.|  
|**Diminuir Prioridade**|Diminui a prioridade do tipo de implementação selecionado.|  
|**Eliminar**|Elimina o tipo de implementação selecionado.<br><br>Não é possível eliminar um tipo de implementação se este for referenciado por um tipo de implementação de outra aplicação.<br>Para eliminar um tipo de implantação, deve remover todas as dependências do tipo de implantação que se encontram noutros tipos de implementação.<br>Além disso, deve também remover revisões anteriores de todas as aplicações que tenham um tipo de implementação que refira o tipo de implementação que pretende eliminar.|  
|**Atualizar Conteúdo**|Atualiza o conteúdo do tipo de implementação selecionado.<br /><br /> Quando inicia este assistente para um tipo de implementação que tenha uma aplicação virtual, o Assistente de Conteúdo de **Atualização** está iniciado. Este assistente permite alterar as opções de publicação e as regras de exigência para a aplicação virtual selecionada. Para mais informações, consulte [Criar aplicações](../../apps/deploy-use/create-applications.md).<br /><br /> Quando atualiza o conteúdo de um tipo de implementação, é criada uma nova revisão da aplicação. Isto pode fazer com que dispositivos cliente sejam atualizados com a nova aplicação.|  
