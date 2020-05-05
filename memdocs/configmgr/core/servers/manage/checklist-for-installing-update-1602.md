---
title: Lista de verificação para 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a tomar antes de atualizar da versão 1511 do Gestor de Configuração para a versão 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717861"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1602 para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de atualizar da versão 1511 do Gestor de Configuração para a versão 1602, reveja as seguintes informações e lista de verificação para as ações a tomar antes de iniciar a atualização.  

 **Sobre a instalação da atualização 1602:**  

 A atualização 1602 só pode ser instalada no site de nível superior da sua hierarquia. Isto significa que inicia a instalação a partir do seu site de administração central se tiver um, ou do seu site primário autónomo.  

-   Os sites primários infantis instalam a atualização automaticamente após o site da administração central terminar a instalação da atualização. Pode utilizar janelas de manutenção para controlar quando um site instala atualizações. Começando com o lançamento da atualização 1602, as janelas de manutenção foram *renomeadas janelas*de serviço . Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .  

-   Tem de atualizar manualmente os sites secundários a partir da consola 'Gestor de Configuração' depois de o site principal dos pais terminar a instalação da atualização. As atualizações automáticas dos servidores secundários do site não são suportadas.  

Quando o servidor do site instala a atualização, as funções do sistema do site que são instaladas no servidor do site e as que estão instaladas em computadores remotos são automaticamente atualizadas. Portanto, antes de instalar a atualização, certifique-se de que cada servidor do sistema do site satisfaz quaisquer novos pré-requisitos para operações com a nova versão da atualização.  

A primeira vez que utilizar uma consola de Configuração Manager após a atualização, será solicitado a atualizar essa consola. Para tal, tem de executar a configuração do 'Gestor de Configuração' no computador que acolhe a consola e escolher a opção de atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.  

 **Lista de verificação:**  

 **Certifique-se de que todos os sites executam uma versão suportada do Gestor de Configuração:**  Cada servidor de site na hierarquia deve executar a versão 1511 do Gestor de Configuração antes de poder iniciar a instalação da atualização 1602.  

 **Rever as versões Microsoft .NET instaladas nos servidores do sistema** do site: Quando um site instala a atualização 1602, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2 em cada computador que acolhe uma das seguintes funções do sistema do site (se a .NET Framework 4.5 ou posterior ainda não estiver instalada):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor do sistema do site num estado pendente de reinicialização e reportar erros ao visualizador de status do componente Do Gestor de Configuração. Além disso, as aplicações .NET no servidor podem experimentar falhas aleatórias até que o servidor seja reiniciado.  

 Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Analise o estado do site e da hierarquia e certifique-se de que não existem problemas por resolver:** antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e das funções do sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

Para mais informações, consulte [Os alertas de utilização e o sistema de estado para O Gestor](../../../core/servers/manage/use-alerts-and-the-status-system.md)de Configuração .  

 **Rever a replicação de ficheiros e dados entre sites:**  certifique-se de que a replicação de ficheiros e de base de dados entre sites está operacional e atualizada. Atrasos ou atrasos em qualquer um dos dois podem impedir uma atualização suave e bem sucedida.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.    

 Para mais informações, consulte [sobre o Analisador](monitor-replication.md#BKMK_RLA)de Ligações de Replicação .  

 **Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que acolhem o site, o servidor** de base de dados do site e as funções do sistema de site remoto: Antes de instalar uma atualização para O Gestor de Configuração, instale quaisquer atualizações críticas para cada sistema de site aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 Desativar réplicas de bases de dados para pontos de **gestão em locais primários:** O Gestor de Configuração não pode atualizar com sucesso um site primário que tenha uma réplica de base de dados para pontos de gestão ativados. Desative a replicação de base de dados antes de:  

-   Crie uma cópia de segurança da base de dados do site para testar a atualização da base de dados.  

-   Instale uma atualização para O Gestor de Configuração.  

Para mais informações, consulte [réplicas de Base de Dados para pontos de gestão para Gestor de Configuração](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigurar os pontos de atualização de software que utilizam NLBs:** O Gestor de Configuração não pode atualizar um site que utilize um cluster de equilíbrio de carga de rede (NLB) para hospedar pontos de atualização de software.  Se utilizar clusters NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

 Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .  

 **Desative todas as tarefas de manutenção do site em cada local durante a duração da instalação da atualização nesse local:** Antes de instalar atualizações, desative qualquer tarefa de manutenção do site que possa ser executada durante o tempo em que o processo de atualização estiver ativo. Estas tarefas incluem (mas não se limitam) ao seguinte:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.  

 Para mais informações, consulte as tarefas de [manutenção para O Gestor de Configuração](../../../core/servers/manage/maintenance-tasks.md) e Referência para tarefas de manutenção para O Gestor de [Configuração](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Pare temporariamente qualquer software antivírus nos servidores do Gestor de Configuração:** Antes de atualizar um site, certifique-se de que parou o software antivírus nos servidores do Gestor de Configuração. <!--SMS.503481--> 

 **Criar uma cópia de segurança da base de dados do site no site da administração central e nos principais locais:** Antes de atualizar um site, faça backup na base de dados do site para garantir que tem uma cópia de segurança bem sucedida para utilizar para a recuperação de desastres.   

Para mais informações, consulte [Backup e recuperação para Gestor de Configuração](backup-and-recovery.md).  

 **Faça backup um ficheiro Configuração.mof personalizado:** Se utilizar um ficheiro Configuração.mof personalizado para definir classes de dados que utiliza com inventário de hardware, crie uma cópia de segurança deste ficheiro antes de atualizar o site. Após a atualização, restaure este ficheiro no site da versão 1602. Quando atualiza um site, o ficheiro atual é substituído com a versão original (padrão) do ficheiro. Para mais informações sobre a utilização deste ficheiro, consulte [como alargar o inventário de hardware](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Teste a atualização da base de dados numa cópia da mais recente cópia da base de dados do site:** Antes de atualizar um site de administração central do Gestor de Configuração ou site primário, teste o processo de atualização da base de dados do site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização da base de dados do site porque quando atualiza um site, a base de dados do site pode ser modificada.  

-   Embora não seja necessária uma atualização da base de dados de testes, pode identificar problemas para a atualização antes de a sua base de dados de produção ser afetada.  

-   Uma atualização falhada da base de dados do site pode tornar a base de dados do seu site inoperável e pode exigir uma recuperação do site para restaurar a funcionalidade.  

-   Embora a base de dados do site seja partilhada entre sites numa hierarquia, planeie testar a base de dados em cada site aplicável antes de atualizar esse site.  

-   Se utilizar réplicas de bases de dados para pontos de gestão num site primário, desative a replicação antes de criar a cópia de segurança da base de dados do site.  

O Gestor de Configuração não suporta a cópia de segurança de sites secundários nem suporta a atualização de teste de uma base de dados de site secundário.   
Não ecorra uma atualização da base de dados de testes na base de dados do site de produção. Tal procedimento atualiza a base de dados do site e pode fazer com que deixe de funcionar. Para mais informações, consulte [o Passo 2: Teste a atualização da base](install-in-console-updates.md#bkmk_step2) de dados antes de instalar uma atualização antes de instalar uma **atualização na consola**.  

 **Plano de pilotagem de clientes:** Quando instalar uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os seus clientes ativos.   

 Para tirar partido desta opção, tem de configurar o seu site para suportar atualizações automáticas para pré-produção antes de iniciar a instalação da atualização. Para mais informações, consulte [clientes de Upgrade](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações dos clientes numa coleção de pré-produção.](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Planeie utilizar janelas** de manutenção para controlar quando os servidores do site instalarem atualizações: Pode utilizar as janelas de manutenção para definir um período de tempo durante o qual as atualizações para o servidor do site podem ser instaladas. Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.   

Começando com o lançamento da atualização 1602, as janelas de manutenção foram *renomeadas janelas*de serviço . Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .  

 **Executar verificador pré-requisito de configuração:**  Antes de instalar a atualização 1602, pode executar o verificador pré-requisito independentemente da instalação da atualização. Quando instalar a atualização no site, o verificador pré-requisito corre novamente.  

Para mais informações, consulte **o Passo 3: Executar o verificador pré-requisito antes** de instalar uma atualização no tópico de Atualizações para Gestor de [Configuração.](../../../core/servers/manage/updates.md)  

> [!IMPORTANT]  
>  Quando o verificador pré-requisito funciona de forma independente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do local. Portanto, depois de executar o verificador pré-requisito, mas antes de instalar a atualização 1602, se precisar de executar uma tarefa de manutenção do site, execute **setupwfe.exe** (Configuração do Gestor de Configuração) a partir do CD. Última pasta no servidor do site.  

 **Atualizar sites:** está agora pronto para iniciar a instalação da atualização na sua hierarquia. Recomendamos que planeie instalar a atualização fora do horário normal de trabalho para cada site, quando o processo de instalação da atualização e as suas ações para reinstalar os componentes do site e as funções do sistema do site terão o menor efeito nas suas operações comerciais.

Para mais informações, consulte [Atualizações para Gestor de Configuração](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Consulte também  
 [Atualizações para o Configuration Manager](../../../core/servers/manage/updates.md)
