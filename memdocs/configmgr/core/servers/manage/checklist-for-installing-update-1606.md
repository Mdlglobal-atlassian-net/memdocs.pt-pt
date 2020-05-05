---
title: Lista de verificação para 1606
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a tomar antes de atualizar a partir da versão 1511 ou 1602 do Gestor de Configuração para a versão 1606.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723083"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1606 para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A versão 1606 para o ramo atual do Gestor de Configuração é uma atualização que pode utilizar para atualizar a partir da versão 1511 ou 1602.

Antes de instalar a versão 1606 como atualização, reveja as seguintes informações e lista de verificação para as ações a tomar antes de iniciar a atualização.

Para obter informações sobre versões de base, consulte [as versões Baseline e atualização](../../../core/servers/manage/updates.md#bkmk_Baselines) em [Atualizações para O Gestor](../../../core/servers/manage/updates.md)de Configuração .

## <a name="about-installing-update-1606"></a>Sobre a instalação da atualização 1606

Como *uma atualização,* 1606 só pode ser instalado no local de alto nível da sua hierarquia. Isto significa que inicia a instalação a partir do seu site de administração central se tiver um, ou do seu site primário autónomo.  

- Os sites primários infantis instalam a atualização automaticamente após o site da administração central terminar a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala atualizações. Antes da versão 1606, as janelas de serviço eram chamadas janelas de manutenção. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .  

- Tem de atualizar manualmente os sites secundários a partir da consola 'Gestor de Configuração' depois de o site principal dos pais terminar a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.  

Quando o servidor do site instala a atualização, as funções do sistema do site que estão instaladas no servidor do site e as que estão instaladas em computadores remotos são atualizadas automaticamente. Portanto, antes de instalar a atualização, certifique-se de que cada servidor do sistema do site satisfaz quaisquer novos pré-requisitos para operações com a nova versão da atualização.  

A primeira vez que utilizar uma consola de Configuração Manager após a instalação da atualização, será solicitado a atualizar essa consola.  Para tal, tem de executar a configuração do 'Gestor de Configuração' no computador que acolhe a consola e, em seguida, escolher a opção de atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

**Questões conhecidas para esta atualização**   
Aplicam-se os seguintes problemas quando visualiza o estado de instalação do pacote de atualização:
- Ao atualizar da versão 1602 a 1606, a carga útil do pacote de **atualização Step Extract** apresenta um Status of **Not started**, mesmo que o download tenha sido concluído.
- Ao atualizar da versão 1511 para 1606, algumas etapas mostrarão um estado de **Concluído,** mas não apresentarão um valor para o tempo de **última atualização**.


## <a name="checklist"></a>Lista de Verificação  

**Certifique-se de que todos os sites executam uma versão suportada do Gestor de Configuração:**  Antes de iniciar a instalação da atualização 1606, cada servidor de site na hierarquia deve executar a mesma versão do Gestor de Configuração: ou versão 1511 ou 1602.

**Reveja as versões instaladas Microsoft.NET nos servidores do sistema** do site: Quando um site instala a atualização 1606, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2 em cada computador que acolhe uma das seguintes funções do sistema do site (se a .NET Framework 4.5 ou posterior ainda não estiver instalada):  

- Ponto proxy de registo  

- Ponto de inscrição  

- Ponto de gestão  

- Ponto de ligação de serviço  

Esta instalação pode colocar o servidor do sistema do site num estado de reinicialização pendente e reportar erros ao visualizador de status do componente Do Gestor de Configuração. Além disso, as aplicações .NET no servidor podem ter falhas aleatórias até que o servidor seja reiniciado.  

Para mais informações consulte os [pré-requisitos](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)do site e do sistema do site.  

**Analise o estado do site e da hierarquia e certifique-se de que não existem problemas por resolver:** antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e das funções do sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para mais informações, consulte [Os alertas de utilização e o sistema de estado para O Gestor](../../../core/servers/manage/use-alerts-and-the-status-system.md)de Configuração .  

**Rever a replicação de ficheiros e dados entre sites:**  certifique-se de que a replicação de ficheiros e de base de dados entre sites está operacional e atualizada. Atrasos ou atrasos em qualquer um dos dois podem impedir uma atualização suave e bem sucedida.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização. Para mais informações, consulte [sobre o Analisador](monitor-replication.md#BKMK_RLA)de Ligações de Replicação .  


**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que acolhem o site, o servidor** de base de dados do site e as funções do sistema de site remoto: Antes de instalar uma atualização para O Gestor de Configuração, instale quaisquer atualizações críticas para cada sistema de site aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

Desativar réplicas de bases de dados para pontos de **gestão em locais primários:** O Gestor de Configuração não pode atualizar com sucesso um site primário que tenha uma réplica de base de dados para pontos de gestão ativados. Desative a replicação da base de dados antes de instalar uma atualização para O Gestor de Configuração.  

Para mais informações, consulte [réplicas de Base de Dados para pontos de gestão para Gestor de Configuração](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Desajuste os grupos de disponibilidade do Servidor SQL AlwaysOn para falhas manuais:**  
Antes de instalar atualizações, como a versão 1606, certifique-se de que o grupo de disponibilidade está definido para falha manual. Depois de o site ter sido atualizado, pode restaurar a falha para ser automático. Para mais informações, consulte [o SQL Server AlwaysOn para obter uma base de dados](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)do site .

**Reconfigurar os pontos de atualização de software que utilizam NLBs:** O Gestor de Configuração não pode atualizar um site que utilize um cluster de equilíbrio de carga de rede (NLB) para hospedar pontos de atualização de software.  

Se utilizar clusters NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .  

**Desative todas as tarefas de manutenção do site em cada local durante a duração da instalação da atualização nesse local:** Antes de instalar a atualização, desative quaisquer tarefas de manutenção do local que possam ser executadas durante o tempo em que o processo de atualização esteja ativo. Estas incluem as seguintes, entre outras:  

- Servidor do Site de Reserva  

- Eliminar Operações de Cliente Desatualizadas  

- Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, grave o calendário da tarefa para que possa restaurar a sua configuração depois de a atualização ter sido instalada.  

Para mais informações, consulte as tarefas de [manutenção para O Gestor de Configuração](../../../core/servers/manage/maintenance-tasks.md) e Referência para tarefas de manutenção para O Gestor de [Configuração](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Pare temporariamente qualquer software antivírus nos servidores do Gestor de Configuração:** Antes de atualizar um site, certifique-se de que parou o software antivírus nos servidores do Gestor de Configuração. <!--SMS.503481--> 

**Criar uma cópia de segurança da base de dados do site no site de administração central e em sites primários:** antes de atualizar um site, faça uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança bem-sucedida para utilizar para a recuperação após desastre.   

Para mais informações, consulte [Backup e recuperação para Gestor de Configuração](backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Plano de pilotagem de clientes:** Quando instalar uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os seus clientes ativos.   

Para aproveitar esta opção, antes de iniciar a instalação da atualização, tem de configurar o seu site para suportar atualizações automáticas para pré-produção. Para mais informações, consulte [clientes de Upgrade](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações dos clientes numa coleção de pré-produção.](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

**Planeie utilizar as janelas** de serviço para controlar quando os servidores do site instalarem atualizações: Pode utilizar as janelas de serviço para definir um período durante o qual as atualizações para um servidor de site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.
Antes da versão 1606, as janelas de serviço eram chamadas janelas de manutenção. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .  

**Executar verificador pré-requisito de configuração:**  Antes de instalar a atualização 1606, pode executar o verificador pré-requisito independentemente da instalação da atualização. Quando instalar a atualização no site, o verificador pré-requisito corre novamente.  

Para mais informações, consulte **o Passo 3: Executar o verificador pré-requisito antes** de instalar uma atualização no tópico de Atualizações para Gestor de [Configuração.](../../../core/servers/manage/install-in-console-updates.md)  

> [!IMPORTANT]  
> Quando o verificador pré-requisito funciona de forma independente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do local. Portanto, depois de executar o verificador pré-requisito, mas antes de instalar a atualização 1606, se precisar de executar uma tarefa de manutenção do site, execute **setupwpf.exe** (Configuração do Gestor de Configuração) a partir do CD. Última pasta no servidor do site.  

**Atualizar sites:** está agora pronto para iniciar a instalação da atualização na sua hierarquia.  
Recomendamos que planeie instalar a atualização fora do horário normal de trabalho para cada site, quando o processo de instalação da atualização e as suas ações para reinstalar os componentes do site e as funções do sistema do site terão o menor efeito nas suas operações comerciais.

Para mais informações, consulte [Atualizações para Gestor de Configuração](../../../core/servers/manage/updates.md).  
