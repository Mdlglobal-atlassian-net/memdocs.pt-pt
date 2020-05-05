---
title: Lista de verificação para 1902
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a tomar antes de atualizar para a versão 1902 do Gestor de Configuração.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 150194be4d7d2fa07fb868e9a5f65f52f3bdd768
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723265"
---
# <a name="checklist-for-installing-update-1902-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1902 para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando utilizar o atual ramo do Gestor de Configuração, pode instalar a atualização na consola para a versão 1902 para atualizar a sua hierarquia a partir de uma versão anterior. <!-- baseline only statement:-->(Como a versão 1902 também está disponível como meio de [base,](updates.md#bkmk_Baselines)pode utilizar os meios de instalação para instalar o primeiro local de uma nova hierarquia.)

Para obter a atualização para a versão 1902, deve utilizar um ponto de ligação de serviço no local de alto nível da sua hierarquia. Esta função do sistema de site pode estar em modo online ou offline. Depois da sua hierarquia descarregar o pacote de atualização da Microsoft, encontre-o na consola. No espaço de trabalho da **Administração,** selecione as Atualizações e o nó **de Manutenção.**

-   Quando a atualização estiver listada como **disponível,** a atualização está pronta para ser instalada. Antes de instalar a versão 1902, reveja as seguintes informações sobre a instalação da [atualização 1902](#about-installing-update-1902) e a lista de [verificação](#checklist) para configurações a fazer antes de iniciar a atualização.

-   Se a atualização for **a descarregada** e não alterar, reveja o **hman.log** e **o dmpdownloader.log** para erros.

    -   O dmpdownloader.log pode indicar que o processo dmpdownloader está à espera de um intervalo antes de verificar se há atualizações. Para reiniciar o download dos ficheiros de redistribuição da atualização, reinicie o serviço **SMS_Executive** no servidor do site.

    -   Outro problema comum de descarregamento ocorre `silverlight.dlservice.microsoft.com` `download.microsoft.com`quando `go.microsoft.com`as definições do servidor proxy impedem os downloads de , e .

Para mais informações sobre a instalação de atualizações, consulte [as atualizações e a manutenção da consola](updates.md#bkmk_inconsole).

Para obter mais informações sobre as versões atuais do ramo, consulte as [versões Baseline e update](updates.md#bkmk_Baselines).



## <a name="about-installing-update-1902"></a>Sobre a instalação da atualização 1902

#### <a name="sites"></a>Sites
Instala a atualização 1902 no local de alto nível da sua hierarquia. Inicie a instalação a partir do seu site de administração central ou do seu local primário autónomo. Após a atualização ser instalada no site de alto nível, os sites infantis têm o seguinte comportamento de atualização:

-   Os locais primários para crianças instalam a atualização automaticamente após o site da administração central terminar a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala a atualização. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .

-   Atualize manualmente cada local secundário a partir da consola Do Gestor de Configuração após o local principal dos pais terminar a instalação da atualização. A atualização automática dos servidores secundários do site não é suportada.

#### <a name="site-system-roles"></a>Funções do sistema de sites
Quando um servidor de site instala a atualização, atualiza automaticamente todas as funções do sistema do site. Estas funções estão no servidor do site ou instaladas em servidores remotos. Antes de instalar a atualização, certifique-se de que cada servidor do sistema do site satisfaz os pré-requisitos atuais para a nova versão da atualização.

#### <a name="configuration-manager-consoles"></a>Consolas de Gestor de Configuração   
A primeira vez que utilizas uma consola de Configuração Manager depois da atualização, és solicitado a atualizar essa consola. Também pode executar a configuração do Gestor de Configuração no computador que acolhe a consola e escolher a opção de atualizar a consola. Instale a atualização na consola o mais rapidamente possível. Para mais informações, consulte [Instalar a consola 'Gestor de Configuração'.](../deploy/install/install-consoles.md)

> [!IMPORTANT]  
> Quando instalar uma atualização no site da administração central, esteja ciente das seguintes limitações e atrasos que existem até que todos os locais primários infantis também completem a instalação da atualização:    
> - **As atualizações dos clientes** não começam. Isto inclui atualizações automáticas de clientes e clientes de pré-produção. Além disso, não é possível promover clientes de pré-produção à produção até que o último site complete a instalação da atualização. Depois de o último site concluir a instalação da atualização, as atualizações do cliente começarão com base nas suas escolhas de configuração.   
> - Não estão disponíveis **novas funcionalidades** com a atualização. Isto é para evitar que a replicação de dados relacionados com essa funcionalidade seja enviada para um site que ainda não instalou suporte para essa funcionalidade. Depois de todos os sites primários instalarem a atualização, a funcionalidade estará disponível para utilização.   
> - **As ligações** de replicação entre o site da administração central e os locais primários infantis exibem como não atualizadas. Isto apresenta-se no estado de instalação da embalagem de atualização como um estado de Completado com aviso para a inicialização da replicação de monitorização. No nó de monitorização da consola, isto exibe à medida que o *Link está a ser configurado*.


## <a name="checklist"></a>Lista de Verificação

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Todos os sites executam uma versão suportada do Gestor de Configuração  
Cada servidor de site na hierarquia deve executar a mesma versão do Gestor de Configuração antes de poder iniciar a instalação da atualização 1902. Para atualizar para 1902, tem de utilizar a versão 1802, 1806 ou 1810.

#### <a name="review-the-status-of-your-product-licensing"></a>Reveja o estado do licenciamento do seu produto 
Deve ter um acordo ativo de Garantia de Software (SA) ou direitos de subscrição equivalentes para instalar esta atualização. Ao atualizar o site, a página **de Licenciamento** apresenta a opção de confirmar a data de validade da garantia de **software**.

Este valor é opcional. Pode especificar como um lembrete conveniente da data de validade da sua licença. Esta data é visível quando instalar futuras atualizações. Pode ter especificado previamente este valor durante a configuração ou instalação de uma atualização. Também pode especificar este valor na consola 'Gestor de Configuração'. No espaço de trabalho da **Administração,** expandir a Configuração do **Site,** e selecionar **Sites.** **Selecione Definições de hierarquia** na fita e mude para o separador **Licenciamento.**

Para mais informações, consulte [Licenciamento e Balcões.](../../understand/learn-more-editions.md)

#### <a name="review-microsoft-net-versions"></a>Rever as versões Microsoft .NET 
Quando um site instala esta atualização, se não for instalado o requisito mínimo de .NET Framework 4.5, o Gestor de Configuração instala automaticamente .NET Framework 4.5.2. Quando este pré-requisito ainda não está instalado, o site instala-o em cada servidor que acolhe uma das seguintes funções do sistema do site:

-   Ponto de gestão
-   Ponto de ligação de serviço
-   Ponto proxy de registo
-   Ponto de inscrição

Esta instalação pode colocar o servidor do sistema do site num estado de reinicialização pendente e reportar erros ao visualizador de status do componente Do Gestor de Configuração. Além disso, as aplicações .NET no servidor podem experimentar falhas aleatórias até que o servidor seja reiniciado.

Para mais informações, consulte os [pré-requisitos](../../plan-design/configs/site-and-site-system-prerequisites.md)do site e do sistema do site.

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Reveja a versão do Windows ADK para windows 10
A versão do Kit de Avaliação e Implementação do Windows 10 (ADK) deve ser suportada para a versão 1902 do Gestor de Configuração. Para obter mais informações sobre as versões ADK suportadas pelo Windows, consulte [o Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Se necessitar de atualizar o Windows ADK, faça-o antes de iniciar a atualização do 'Gestor de Configuração'. Esta encomenda garante que as imagens de boot predefinidas são automaticamente atualizadas para a versão mais recente do Windows PE. Atualize manualmente quaisquer imagens de boot personalizadas após a atualização do site.

Se atualizar o site antes de atualizar o Windows ADK, consulte [os pontos](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)de distribuição do Update com a imagem de arranque .

#### <a name="review-sql-server-native-client-version"></a>Rever a versão do Cliente Nativo do Servidor SQL
Deve ser instalada uma versão mínima do SQL Server 2012 Client Nativo, que inclui suporte para TLS 1.2. Para mais informações, consulte a [Lista de Verificações pré-requisitos](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Reveja o estado do site e da hierarquia para questões não resolvidas 
Uma atualização de site pode falhar devido a problemas operacionais existentes. Antes de atualizar um site, resolva todos os problemas operacionais para os seguintes sistemas:  
- O servidor do site  
- O servidor de base de dados do site  
- Funções do sistema de site remoto em outros servidores   

Para mais informações, consulte [Alertas de Utilização e o sistema de estado](use-alerts-and-the-status-system.md).

#### <a name="review-file-and-data-replication-between-sites"></a>Rever ficheiros e replicação de dados entre sites   
Certifique-se de que a replicação de ficheiros e bases de dados entre os sites está operacional e atual. Atrasos ou atrasos em qualquer um dos dois podem impedir uma atualização suave e bem sucedida. Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para mais informações, consulte [sobre o Analisador](monitor-replication.md#BKMK_RLA)de Ligações de Replicação .

#### <a name="install-all-applicable-critical-windows-updates"></a>Instale todas as atualizações críticas do Windows aplicáveis
Antes de instalar uma atualização para O Gestor de Configuração, instale quaisquer atualizações críticas do SISTEMA OPERATIVO para cada sistema de site aplicável. Estes servidores incluem o servidor do site, o servidor de base de dados do site e as funções do sistema do site remoto. Se uma atualização que instala necessitar de um reinício, reinicie os servidores aplicáveis antes de iniciar a atualização.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Desativar réplicas de bases de dados para pontos de gestão em locais primários   
O Gestor de Configuração não consegue atualizar com sucesso um site primário que tenha uma réplica de base de dados para pontos de gestão ativados. Antes de instalar uma atualização para O Gestor de Configuração, desative a replicação da base de dados.

Para mais informações, consulte réplicas de Base de [Dados para pontos](../deploy/configure/database-replicas-for-management-points.md)de gestão .

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Desajuste os grupos de disponibilidade do Servidor SQL AlwaysOn para falhas manuais   
Se utilizar um grupo de disponibilidade, certifique-se de que o grupo de disponibilidade está definido para falha manual antes de iniciar a instalação da atualização. Depois de o site ter sido atualizado, pode restaurar a falha para ser automático. Para mais informações, consulte [o SQL Server AlwaysOn para obter uma base de dados](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)do site .

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Desativar as tarefas de manutenção do site em cada site
Antes de instalar a atualização, desative qualquer tarefa de manutenção do local que possa ser executada durante o tempo em que o processo de atualização estiver ativo. Por exemplo, mas não se limitando a:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, grave o calendário da tarefa para que possa restaurar a sua configuração depois de a atualização ter sido instalada.

Para mais informações, consulte [tarefas](maintenance-tasks.md) de manutenção e [referência para tarefas](reference-for-maintenance-tasks.md)de manutenção .

#### <a name="temporarily-stop-any-antivirus-software"></a>Parar temporariamente qualquer software antivírus 
Antes de atualizar um site, pare o software antivírus nos servidores do Gestor de Configuração. O software antivírus pode bloquear alguns ficheiros que precisam de ser atualizados, o que faz com que a nossa atualização falhe. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Criar uma cópia de segurança da base de dados do site 
Antes de atualizar um site, faça o backup da base de dados do site no site da administração central e nos principais sites. Este backup garante que tem um apoio bem sucedido para usar para a recuperação de desastres.

Para mais informações, consulte [Backup e recuperação.](backup-and-recovery.md)

#### <a name="plan-for-client-piloting"></a>Plano de pilotagem de clientes   
Quando instalar uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os seus clientes ativos. Para tirar partido desta opção, tem de configurar o seu site para suportar atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para mais informações, consulte os [clientes de Upgrade](../../clients/manage/upgrade/upgrade-clients.md) e Como testar as atualizações dos [clientes numa recolha pré-produção.](../../clients/manage/upgrade/test-client-upgrades.md)

#### <a name="plan-to-use-service-windows"></a>Plano para usar janelas de serviço   
Para definir um período durante o qual as atualizações para um servidor de site podem ser instaladas, utilize as janelas de serviço. Podem ajudá-lo a controlar quando os sites da sua hierarquia instalam a atualização. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .

#### <a name="review-supported-extensions"></a>Rever extensões apoiadas
<!--SCCMdocs#587-->
Se alargar o Gestor de Configuração a outros produtos de parceiros da Microsoft ou da Microsoft, confirme que esses produtos suportam a versão 1902. Consulte o fornecedor do produto para obter esta informação. Por exemplo, consulte as [notas](../../../mdt/release-notes.md)de lançamento do Microsoft Deployment Toolkit .

#### <a name="run-the-setup-prerequisite-checker"></a>Executar o verificador pré-requisito de configuração   
Quando a atualização estiver listada na consola como **disponível,** pode executar o verificador pré-requisito antes de instalar a atualização. (Quando instalar a atualização no site, o verificador pré-requisito corre novamente.)

Para espaçar a partir da consola, dirija-se ao espaço de trabalho da **Administração** e selecione **Atualizações e Manutenção**. Selecione o pacote de atualização Do Gestor de **Configuração 1902** e selecione **Executar pré-requisito seleção** na fita.

Para mais informações, consulte a secção para **executar o verificador pré-requisito antes** de instalar uma atualização antes de instalar uma [atualização na consola](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Quando o verificador pré-requisito é executado, o processo atualiza alguns ficheiros de origem do produto que são usados para tarefas de manutenção do site. Portanto, depois de executar o verificador pré-requisito, mas antes de instalar a atualização, se precisar de executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (Configuração do Gestor de Configuração) a partir do CD. Última pasta no servidor do site.

#### <a name="update-sites"></a>Atualizar sites   
Está agora pronto para iniciar a instalação de atualização para a sua hierarquia. Para mais informações sobre a instalação da atualização, consulte [a instalação de atualizações na consola](install-in-console-updates.md#bkmk_install).

Pode planear instalar a atualização fora do horário normal de trabalho. Determine quando o processo terá o menor efeito nas suas operações comerciais. Instalar a atualização e as suas ações reinstalar os componentes do local e as funções do sistema do site.

Para mais informações, consulte [Atualizações para Gestor de Configuração](updates.md).



## <a name="post-update-checklist"></a>Lista de verificação pós-actualização

Após as atualizações do site, utilize a seguinte lista de verificação para completar tarefas e configurações comuns.


#### <a name="confirm-version-and-restart-if-necessary"></a>Confirmar versão e reiniciar (se necessário)
Certifique-se de que cada função do servidor do site e do sistema do site foi atualizada para a versão 1902. Na consola, adicione a coluna **Versão** aos nós de **Sites** e **Pontos de Distribuição** no espaço de trabalho da **Administração.** Quando necessário, uma função do sistema do site reinstala-se automaticamente para atualizar para a nova versão. 

Considere reiniciar sistemas de sites remotos que não atualizam com sucesso no início. Reveja a infraestrutura do seu site e certifique-se de que os servidores do site aplicáveis e servidores de sistemas de site remoto saem reiniciados com sucesso. Normalmente, os servidores do site reiniciam apenas quando o Gestor de Configuração instala .NET como pré-requisito para uma função do sistema do site.


#### <a name="confirm-site-to-site-replication-is-active"></a>Confirmar que a replicação local-a-local está ativa
Na consola 'Gestor de Configuração', vá aos seguintes locais para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização do** espaço de trabalho, nó **da hierarquia do site**  

-   **Monitorização do** espaço de trabalho, nó de **replicação de base** de dados  

Para obter mais informações, veja os artigos seguintes:  

- [Monitorizar a hierarquia](monitor-hierarchy.md)
- [Monitorizar a replicação](monitor-replication.md)
- [Sobre o Analisador de Ligação de Replicação](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Atualizar consolas do Configuration Manager
Atualize todas as consolas remotas do Gestor de Configuração para a mesma versão. É-lhe pedido que atualize a consola quando:  

-   Abres a consola.  

-   Vais para um novo nó na consola.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Reconfigurar réplicas de bases de dados para pontos de gestão
Depois de atualizar um site primário, reconfigure a réplica da base de dados para os pontos de gestão que desinstalou antes de atualizar o site. Para mais informações, consulte réplicas de Base de [Dados para pontos](../deploy/configure/database-replicas-for-management-points.md)de gestão .  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Reconfigurar quaisquer tarefas de manutenção com deficiência
Se desativar [as tarefas](maintenance-tasks.md) de manutenção da base de dados num site antes de instalar a atualização, reconfigure essas tarefas. Utilize as mesmas definições que estavam em vigor antes da atualização.  


#### <a name="update-clients"></a>Atualizar clientes
Atualize os clientes de acordo com o plano que criou, especialmente se configurar a pilotagem do cliente antes de instalar a atualização. Para mais informações, consulte [Como atualizar os clientes para computadores Windows](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### <a name="third-party-extensions"></a>Extensões de terceiros
Se utilizar quaisquer extensões ao 'Gestor de Configuração', atualize-as na versão mais recente para suportar a versão 1902 do Gestor de Configuração. 


#### <a name="update-custom-boot-images-and-media"></a>Atualizar imagens e meios de arranque personalizados
<!--SCCMDocs issue 775-->

Utilize a ação Pontos de Distribuição de **Atualização** para qualquer imagem de arranque que utilize, seja uma imagem de arranque padrão ou personalizada. Esta ação garante que os clientes podem usar a versão mais recente. Mesmo que não exista uma nova versão do Windows ADK, os componentes do cliente do Gestor de Configuração podem mudar com uma atualização. Se não atualizar imagens de arranque e meios de comunicação, as implementações da sequência de tarefas podem falhar nos dispositivos. 

Quando atualiza o site, o Gestor de Configuração atualiza automaticamente as imagens de boot *predefinidas.* Não distribui automaticamente o conteúdo atualizado para pontos de distribuição. Utilize a ação Pontos de Distribuição de **Atualização** em imagens específicas de arranque quando estiver pronto para distribuir este conteúdo pela sua rede. 

Depois de atualizar o site, atualize manualmente quaisquer imagens de boot *personalizadas.* Esta ação atualiza a imagem de arranque com os mais recentes componentes do cliente, se necessário, recarrega-a opcionalmente com a versão atual do Windows PE e redistribui o conteúdo para os pontos de distribuição. 

Para mais informações, consulte pontos de [distribuição de Atualização com a imagem do arranque](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
