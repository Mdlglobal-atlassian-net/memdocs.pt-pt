---
title: Lista de verificação para 1802
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a tomar antes de atualizar para a versão 1802 do Gestor de Configuração.
ms.date: 06/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6af92de2-b2c7-4d5c-affd-6cce81979fb5
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f9c0c44d6a5f3921fd9a2ea4292e94cff1fa7d9f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723272"
---
# <a name="checklist-for-installing-update-1802-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1802 para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando utilizar o atual ramo do Gestor de Configuração, pode instalar a atualização na consola para a versão 1802 para atualizar a sua hierarquia a partir de uma versão anterior. <!-- baseline only statement: -->(Como a versão 1802 também está disponível como meio de [base,](updates.md#bkmk_Baselines)pode utilizar os meios de instalação para instalar o primeiro local de uma nova hierarquia.)

Para obter a atualização para a versão 1802, deve utilizar um ponto de ligação de serviço no local de alto nível da sua hierarquia. Esta função do sistema de site pode estar em modo online ou offline. Depois de a sua hierarquia descarregar o pacote de atualização da Microsoft, pode encontrá-lo na consola sob o espaço de trabalho **da Administração** nas Atualizações e no nó **de Manutenção.**

-   Quando a atualização estiver listada como **disponível,** a atualização está pronta para ser instalada. Antes de instalar a versão 1802, reveja as seguintes informações sobre a instalação da [atualização 1802](#about-installing-update-1802) e a lista de [verificação](#checklist) para configurações a fazer antes de iniciar a atualização.

-   Se a atualização for **reparada** como Downloading e não mudar, reveja o **hman.log** e **dmpdownloader.log** para erros.

    -   Se o dmpdownloader.log indicar que o processo de descarregamento está a dormir e à espera de um intervalo antes de verificar as atualizações, pode reiniciar o serviço **SMS_Executive** no servidor do site para reiniciar o download dos ficheiros de redistribuição da atualização.

    -   Outro problema comum de descarregamento ocorre `silverlight.dlservice.microsoft.com` `download.microsoft.com`quando as definições do servidor proxy impedem os downloads de e .

Para mais informações sobre a instalação de atualizações, consulte [as atualizações e a manutenção da consola](updates.md#bkmk_inconsole).

Para obter informações sobre as versões do Ramo Atual, consulte [as versões Base de Base e atualização](updates.md#bkmk_Baselines) em [Atualizações para Gestor de Configuração](updates.md).

## <a name="about-installing-update-1802"></a>Sobre a instalação da atualização 1802

**Sites:**  
Instale a atualização 1802 no local de alto nível da sua hierarquia. Isto significa que inicia a instalação a partir do seu site de administração central se tiver um, ou do seu site primário autónomo. Após a atualização ser instalada no site de topo, os sites infantis têm o seguinte comportamento de atualização:

-   Os locais primários para crianças instalam a atualização automaticamente após o site da administração central terminar a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala a atualização. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .

-   Tem de atualizar manualmente cada local secundário a partir da consola 'Gestor de Configuração' depois de o local principal dos pais terminar a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções do sistema de sites:**  
Quando um servidor de site instala a atualização, as funções do sistema do site que são instaladas no computador do servidor do site e as que estão instaladas em computadores remotos, são automaticamente atualizadas. Antes de instalar a atualização, certifique-se de que cada servidor do sistema do site satisfaz os pré-requisitos para o funcionamento com a nova versão da atualização.

**Consolas de Gestor de Configuração:**   
A primeira vez que utilizar uma consola de Configuração Manager após a atualização, será solicitado a atualizar essa consola. Para tal, tem de executar a configuração do 'Gestor de Configuração' no computador que acolhe a consola e, em seguida, escolher a opção de atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

> [!IMPORTANT]  
> Quando instalar uma atualização no site da administração central, esteja ciente das seguintes limitações e atrasos que existem até que todos os locais primários infantis também completem a instalação da atualização:    
> - **As atualizações dos clientes** não começam. Isto inclui atualizações automáticas de clientes e clientes de pré-produção. Além disso, não é possível promover clientes de pré-produção à produção até que o último site complete a instalação da atualização. Depois de o último site concluir a instalação da atualização, as atualizações do cliente começarão com base nas suas escolhas de configuração.   
> - Não estão disponíveis **novas funcionalidades** com a atualização. Isto é para evitar que a replicação de dados relacionados com essa funcionalidade seja enviada para um site que ainda não instalou suporte para essa funcionalidade. Depois de todos os sites primários instalarem a atualização, a funcionalidade estará disponível para utilização.   
> - **As ligações** de replicação entre o site da administração central e os locais primários infantis exibem como não atualizadas. Isto apresenta-se no estado de instalação da embalagem de atualização como um estado de Completado com aviso para a inicialização da replicação de monitorização. No nó de monitorização da consola, isto exibe à medida que o *Link está a ser configurado*.


## <a name="checklist"></a>Lista de Verificação

**Certifique-se de que todos os sites executam uma versão do Gestor de Configuração que suporta a atualização até 1802:**   
Cada servidor de site na hierarquia deve executar a mesma versão do Gestor de Configuração antes de poder iniciar a instalação da atualização 1802. Para atualizar para 1802, tem de utilizar a versão 1702, 1706 ou 1710.

**Reveja o estado da sua Garantia de Software ou direitos de subscrição equivalentes:**   
Tem de ter um acordo ativo de Garantia de Software (SA) para instalar a atualização 1802. Quando instala esta atualização, o separador **Licenciamento** apresenta a opção de confirmar a data de validade da garantia de **software**.

Este é um valor opcional que pode especificar como um lembrete conveniente da data de validade da sua licença. Esta data é visível quando instalar futuras atualizações. Pode ter especificado previamente este valor durante a configuração ou instalação de uma atualização, ou utilizando o separador **de licenciamento** das **Definições da Hierarquia,** a partir da consola do Gestor de Configuração.

Para mais informações, consulte [Licenciamento e balcões para Gestor de Configuração](../../understand/learn-more-editions.md).

**Rever as versões Microsoft .NET instaladas nos servidores do sistema** do site: Quando um site instala esta atualização, o Gestor de Configuração instala automaticamente a .NET Framework 4.5.2 em cada computador que acolhe uma das seguintes funções do sistema do site quando a .NET Framework 4.5 ou posterior ainda não estiver instalada:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor do sistema do site num estado de reinicialização pendente e reportar erros ao visualizador de status do componente Do Gestor de Configuração. Além disso, as aplicações .NET no servidor podem experimentar falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Reveja a versão do Kit de Avaliação e Implementação do Windows (ADK) para o Windows 10** O Windows 10 ADK deve ser a versão 1703 ou mais tarde. (Para obter mais informações sobre as versões ADK suportadas pelo Windows, consulte [o Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk).) Se tiver de atualizar o Windows ADK, faça-o antes de iniciar a atualização do 'Gestor de Configuração'. Isto garante que as imagens de boot padrão são automaticamente atualizadas para a versão mais recente do Windows PE. (As imagens de arranque personalizadas devem ser atualizadas manualmente.)

Se atualizar o site antes de atualizar o Windows ADK, consulte [os pontos](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)de distribuição do Update com a imagem de arranque .

**Analise o estado do site e da hierarquia e certifique-se de que não existem problemas por resolver:** antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e das funções do sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para mais informações, consulte [Os alertas de utilização e o sistema de estado para O Gestor](use-alerts-and-the-status-system.md)de Configuração .

**Rever ficheiros e replicação de dados entre sites:**   
Certifique-se de que a replicação de ficheiros e bases de dados entre os sites está operacional e atual. Atrasos ou atrasos em qualquer um dos dois podem impedir uma atualização suave e bem sucedida.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para mais informações, consulte [sobre o Analisador](monitor-replication.md#BKMK_RLA)de Ligações de Replicação .

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que acolhem o site, o servidor** de base de dados do site e as funções do sistema de site remoto: Antes de instalar uma atualização para O Gestor de Configuração, instale quaisquer atualizações críticas para cada sistema de site aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.

**Desativar réplicas de bases de dados para pontos de gestão em locais primários:**   
O Gestor de Configuração não pode atualizar com sucesso um site primário que tenha uma réplica de base de dados para pontos de gestão ativados. Desative a replicação da base de dados antes de instalar uma atualização para O Gestor de Configuração.

Para mais informações, consulte [réplicas de Base de Dados para pontos de gestão para Gestor de Configuração](../deploy/configure/database-replicas-for-management-points.md).

**Desajuste os grupos de disponibilidade do Servidor SQL AlwaysOn para falhas manuais:**   
Se utilizar um grupo de disponibilidade, certifique-se de que o grupo de disponibilidade está definido para falha manual antes de iniciar a instalação da atualização. Depois de o site ter sido atualizado, pode restaurar a falha para ser automático. Para mais informações consulte [o SQL Server AlwaysOn para obter uma base de dados](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)do site .

**Reconfigurar os pontos de atualização de software que utilizam NLBs:**   
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
O Gestor de Configuração não pode atualizar um site que utilize um cluster de equilíbrio de carga de rede (NLB) para hospedar pontos de atualização de software.

Se utilizar clusters NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .

**Desative todas as tarefas de manutenção do site em cada local durante a duração da instalação da atualização nesse local:**   
Antes de instalar a atualização, desative qualquer tarefa de manutenção do local que possa ser executada durante o tempo em que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, grave o calendário da tarefa para que possa restaurar a sua configuração depois de a atualização ter sido instalada.

Para mais informações, consulte as tarefas de [manutenção para O Gestor de Configuração](maintenance-tasks.md) e Referência para tarefas de manutenção para O Gestor de [Configuração](reference-for-maintenance-tasks.md).

**Pare temporariamente qualquer software antivírus nos servidores do Gestor de Configuração:** Antes de atualizar um site, certifique-se de que parou o software antivírus nos servidores do Gestor de Configuração. <!--SMS.503481--> 

**Criar uma cópia de segurança da base de dados do site no site de administração central e em sites primários:** antes de atualizar um site, faça uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança bem-sucedida para utilizar para a recuperação após desastre.

Para mais informações, consulte [Backup e recuperação para Gestor de Configuração](backup-and-recovery.md).

**Plano de pilotagem de clientes:**   
Quando instalar uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os seus clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para mais informações, consulte os [clientes de Upgrade](../../clients/manage/upgrade/upgrade-clients.md) e Como testar as atualizações dos clientes numa recolha [pré-produção.](../../clients/manage/upgrade/test-client-upgrades.md)

**Planeie utilizar as janelas de serviço para controlar quando os servidores do site instalarem atualizações:**   
Utilize as janelas de serviço para definir um período durante o qual as atualizações para um servidor de site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Para mais informações, consulte [as janelas de serviço para servidores](service-windows.md)do site .

**Rever extensões apoiadas por revisão:**   
<!--SCCMdocs#587-->   
Se alargar o Gestor de Configuração a outros produtos de parceiros da Microsoft ou da Microsoft, confirme que esses produtos suportam a versão 1802. Consulte o fornecedor do produto para obter esta informação. Por exemplo, consulte as [notas](../../../mdt/release-notes.md)de lançamento do Microsoft Deployment Toolkit .

**Executar o verificador pré-requisito de configuração:**   
Quando a atualização estiver listada na consola como **disponível,** pode executar o verificador pré-requisito antes de instalar a atualização. (Quando instalar a atualização no site, o verificador pré-requisito corre novamente.)

Para espaçar a partir da consola, dirija-se ao espaço de trabalho da **Administração** e selecione **Atualizações e Manutenção**. Selecione o pacote de atualização Do Gestor de **Configuração 1802** e clique em **Executar pré-requisito verifique** na fita.

Para obter mais informações sobre o início e, em seguida, a monitorização da verificação pré-requisito, consulte **o Passo 3: Executar o verificador pré-requisito antes** de instalar uma atualização no tópico [Instale atualizações na consola para O Gestor de Configuração](install-in-console-updates.md).

> [!IMPORTANT]  
> Quando o verificador pré-requisito funciona de forma independente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do local. Portanto, depois de executar o verificador pré-requisito, mas antes de instalar a atualização, se precisar de executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (Configuração do Gestor de Configuração) a partir do CD. Última pasta no servidor do site.

**Atualizar sites:**   
Está agora pronto para iniciar a instalação de atualização para a sua hierarquia. Para mais informações sobre a instalação da atualização, consulte [a instalação de atualizações na consola.](install-in-console-updates.md#bkmk_install)

Recomendamos que planeie instalar a atualização fora do horário normal de trabalho para cada site quando o processo de instalação da atualização e as suas ações para reinstalar os componentes do site e as funções do sistema do site terão o menor efeito nas suas operações comerciais.

Para mais informações, consulte [Atualizações para Gestor de Configuração](updates.md).

## <a name="post-update-checklist"></a>Lista de verificação de atualizações postais
Reveja as seguintes ações a tomar após a instalação da atualização estar concluída.
1. Certifique-se de que a replicação local-a-local está ativa. Na consola, veja a Hierarquia do**Site** **de Monitorização** > e a**Replicação** da Base de Dados de **Monitorização** > para obter indicações de problemas ou confirmação de que as ligações de replicação estão ativas.
2. Certifique-se de que cada função do servidor do site e do sistema do site foi atualizada para a versão 1802. Na consola, pode adicionar a **versão** de coluna opcional ao ecrã de alguns nós, incluindo **Sites** e **Pontos de Distribuição**.

   Quando necessário, uma função do sistema do site reinstala-se automaticamente para atualizar para a nova versão. Considere reiniciar sistemas de sites remotos que não atualização com sucesso.
3. Reconfigure as réplicas da base de dados para pontos de gestão em sites primários que desativou antes de iniciar a atualização.
4. Reconfigure as tarefas de manutenção da base de dados que desativou antes de iniciar a atualização.
5. Se configurar a pilotagem do cliente antes de instalar a atualização, atualize os clientes de acordo com o plano que criou.
6. Se utilizar quaisquer extensões ao 'Gestor de Configuração', atualize-as na versão mais recente para suportar esta atualização do Gestor de Configuração. 
