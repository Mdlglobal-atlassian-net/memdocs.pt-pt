---
title: Elevada disponibilidade do servidor do site
titleSuffix: Configuration Manager
description: Como configurar uma alta disponibilidade para o servidor do site do Gestor de Configuração adicionando um servidor de site de modo passivo.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718309"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Alta disponibilidade do servidor do site no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1128774-->

Historicamente, pode adicionar redundância à maioria dos papéis no Gestor de Configuração, tendo múltiplos casos destas funções no seu ambiente. Exceto pelo servidor do site em si. A alta disponibilidade para a função do servidor do site é uma solução baseada em Configuração manager para instalar um servidor de site adicional em modo *passivo.* O site da administração central e os sites primários infantis podem ter um servidor de site adicional em modo passivo. O servidor do site em modo passivo pode estar no local ou baseado em nuvem em Azure.

Esta funcionalidade traz os seguintes benefícios

- Redundância e elevada disponibilidade para o papel do servidor do site  
- Altere mais facilmente o hardware ou oss do servidor do site  
- Mova mais facilmente o seu servidor de site para O IaaS Azure  

O servidor do site em modo passivo é além do servidor do site existente que está em modo *ativo.* Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Inclua este servidor adicional do site como parte do seu design geral para tornar o serviço De Configuração [Manager altamente disponível](high-availability-options.md).  

Um servidor de site em modo passivo:

- Utiliza a mesma base de dados do site que o servidor do site em modo ativo.
- Não escreve dados para a base de dados do site quando está em modo passivo.
- Utiliza a mesma biblioteca de conteúdos que o servidor do site em modo ativo.

Para que o servidor do site em modo passivo se torne ativo, *promove-o* manualmente. Esta ação comuta o servidor do site em modo ativo para ser o servidor do site em modo passivo. As funções do sistema do site que estão disponíveis no servidor de modo ativo original permanecem disponíveis desde que esse computador esteja acessível. Apenas a função do servidor do site é trocada entre modos ativos e passivos.

A Microsoft Core Services Engineering and Operations utilizou esta funcionalidade para migrar o seu site de administração central para o Microsoft Azure. Para mais informações, consulte o [artigo microsoft IT Showcase](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Pré-requisitos

- A biblioteca de conteúdos do site deve estar numa partilha remota de rede. Ambos os servidores do site precisam de permissões de Controlo Total para a parte e o seu conteúdo. Para mais informações, consulte Gerir a [biblioteca de conteúdos.](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)<!--1357525-->  

  - A conta do computador do servidor do site precisa de permissões de **controlo completos** para o caminho da rede para o qual está a mover a biblioteca de conteúdos. Esta permissão aplica-se tanto à parte como ao sistema de ficheiros. Não são instalados componentes no sistema remoto.

  - O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também usa a biblioteca de conteúdos, e esta função não suporta uma biblioteca de conteúdos remotos. Depois de mover a biblioteca de conteúdos, não pode adicionar a função de ponto de distribuição ao servidor do site.  

- O servidor do site em modo passivo pode estar no local ou baseado em nuvem em Azure.  

    > [!NOTE]
    > Um servidor de site baseado em nuvem em modo passivo utiliza a infraestrutura Azure como serviço (IaaS). Para obter mais informações, veja os artigos seguintes:
    >
    >   - [Máquinas virtuais Azure (para infraestruturas baseadas em nuvem)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [FAQ para Gerente de Configuração em Azure](../../../understand/configuration-manager-on-azure.md)  

- Ambos os servidores do site devem ser unidos ao mesmo domínio de Diretório Ativo.  

- O Gestor de Configuração suporta servidores do site em modo passivo numa hierarquia. O site da administração central e os sites primários infantis podem ter um servidor de site adicional em modo passivo.<!-- 3607755 -->  

- Ambos os servidores do site devem usar a mesma base de dados do site.  

  - A base de dados pode ser remota de cada servidor do site. A partir da versão 1810, o processo de configuração do Gestor de Configuração já não bloqueia a instalação da função do servidor do site num computador com a função Windows para o Clusterfailover. O SQL Always On requer esta função, pelo que anteriormente não conseguiu colocar a base de dados do site no servidor do site. Com esta alteração, pode criar um site altamente disponível com menos servidores utilizando o SQL Always On e um servidor de site em modo passivo.<!-- SCCMDocs issue 1074 -->  

  - O Servidor SQL que acolhe a base de dados do site pode usar uma instância padrão, chamada instância, [cluster SQL Server,](use-a-sql-server-cluster-for-the-site-database.md)ou um [grupo de disponibilidade do Servidor SQL Always On](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Ambos os servidores do site precisam da função de segurança da **sisadmina** na instância do SQL Server que acolhe a base de dados do site. O servidor original do site já deve ter estas funções, por isso adicione-as para o novo servidor do site. Por exemplo, o seguinte script SQL adiciona estas funções para o novo servidor de site **VM2** no domínio Contoso:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Ambos os servidores do site precisam de acesso à base de dados do site na instância do Servidor SQL. O servidor original do site já deve ter este acesso, por isso adicione-o para o novo servidor do site. Por exemplo, o seguinte script SQL adiciona um login à **base de** dados CM_ABC para o novo servidor de site **VM2** no domínio Contoso:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - O servidor do site em modo passivo está configurado para utilizar a mesma base de dados do site que o servidor do site no modo ativo. O servidor do site em modo passivo apenas lê a partir da base de dados. Não escreve para a base de dados até depois de ser promovido ao modo ativo.  

- O servidor do site em modo passivo:  

  - Deve satisfazer os pré-requisitos para a instalação de um local primário. Por exemplo, .NET Framework, Compressão Diferencial Remota e O ADK do Windows. Para a lista completa, consulte os [pré-requisitos](../../../plan-design/configs/site-and-site-system-prerequisites.md)do site e do sistema do site .<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Certifique-se de instalar o Cliente Nativo do Servidor SQL. Se não o instalar, o verificador pré-requisito durante a configuração do Gestor de Configuração reportará um erro sobre as permissões do SQL Server em falta.<!-- SCCMDocs#2290 -->

  - Deve ter a sua conta de computador no grupo de Administradores locais no servidor do site em modo ativo.<!--516036-->

  - Deve instalar utilizando ficheiros de origem que correspondam à versão do servidor do site no modo ativo.  

  - Não é possível ter uma função do sistema do site a partir de qualquer site instalado no mesmo antes de instalar o servidor do site em função de modo passivo.  

- Ambos os servidores do site podem executar diferentes versões de OS ou pacote de serviço, desde que ambos sejam [suportados pelo Gestor](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)de Configuração .  

- Não apresente a função de ponto de ligação de serviço em nenhum dos servidores do site configurado para alta disponibilidade. Se estiver atualmente no servidor do site original, remova-o e instale-o noutro servidor do sistema do site. Para mais informações, consulte sobre o ponto de [ligação ao serviço](about-the-service-connection-point.md).  

- Permissões para a conta de [instalação](../../../plan-design/hierarchy/accounts.md#site-system-installation-account) do sistema do site  

  - Por padrão, muitos clientes usam a conta de computador do servidor do site para instalar novos sistemas de site. O requisito é então adicionar a conta de computador do servidor do site ao grupo **de Administradores locais** no sistema de site remoto. Se o seu ambiente utilizar esta configuração, certifique-se de adicionar a conta de computador do novo servidor do site a este grupo local em todos os sistemas de site remoto. Por exemplo, todos os pontos de distribuição remota.  

  - A configuração mais segura e recomendada é utilizar uma conta de serviço para instalar o sistema do site. A configuração mais segura é usar uma conta de serviço local. Se o seu ambiente utilizar esta configuração, não é necessária qualquer alteração.  

## <a name="limitations"></a>Limitações

- Apenas um servidor de site em modo passivo é suportado em cada site.  

- Um servidor de site em modo passivo não é suportado num site secundário.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Os sites secundários ainda são suportados sob um site primário com servidores de site altamente disponíveis.

- A promoção do servidor do site em modo passivo para o modo ativo é manual. Não há falha automática.  

- As funções do sistema do site não podem ser instaladas no novo servidor antes de adicionar o servidor do site em modo passivo.  

    > [!NOTE]
    > Depois de instalar o servidor do site em modo passivo, pode adicionar funções adicionais conforme necessário. Por exemplo, um ponto de gestão num local primário.

- Para funções como o ponto de reporte que usam uma base de dados, aloja a base de dados num servidor que é remoto de ambos os servidores do site.  

- A consola 'Gestor de Configuração' não instala automaticamente no servidor do site em modo passivo.  

## <a name="add-a-site-server-in-passive-mode"></a>Adicione um servidor de site em modo passivo

Para obter mais informações sobre o processo geral de adição de funções, consulte [instalar as funções](install-site-system-roles.md)do sistema do site .

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **da Administração,** expanda a Configuração do **Site,** selecione o nó **de Sites** e clique em Criar servidor de sistema de **site** na fita.

2. Na página **geral** do Assistente do Servidor do Sistema de Criar o Site, especifique o servidor para hospedar o servidor do site em modo passivo. O servidor que especifica não pode alojar quaisquer funções do sistema do site antes de instalar um servidor do site em modo passivo.  

3. Na página de Seleção de Funções do **Sistema,** selecione apenas o **servidor do Site no modo passivo**.  

    > [!NOTE]  
    > O assistente executa as seguintes verificações pré-requisitos iniciais nesta página:
    >
    > - O servidor selecionado não é um servidor de site secundário
    > - O servidor selecionado já não é um servidor de site em modo passivo
    > - A biblioteca de conteúdos do site está num local remoto  
    >  
    > Se estas verificações pré-requisitos iniciais falharem, não pode continuar a passar por esta página do assistente.  

4. Na página do Servidor do **Site em Modo Passivo,** forneça as seguintes informações que são utilizadas para executar a configuração e instalar a função do servidor do site no servidor especificado:

     - Selecione uma das seguintes opções:  

         - **Copie os ficheiros de origem de instalação sobre a rede a partir do servidor do site no modo ativo**: Esta opção cria um pacote comprimido e envia-os para o novo servidor do site.  

         - **Utilize os ficheiros de origem no seguinte local no servidor do site em modo passivo**: Por exemplo, um caminho local para o qual já copiou os ficheiros de origem. Certifique-se de que este conteúdo é a mesma versão que o servidor do site em modo ativo.  

         - *(Recomendado)* **Utilize os ficheiros de origem no seguinte local**da rede : Especifique o caminho diretamente para o conteúdo do **CD. Última** pasta do servidor do site em modo ativo. Por exemplo, `\\Server\SMS_ABC\CD.Latest` onde "*Server*" é o nome do servidor do site em modo ativo, e "*ABC*" é o código do site.  

     - Especifique o caminho local para instalar o Gestor de Configuração no novo servidor do site. Por exemplo: `C:\Program Files\Configuration Manager`  

5. Conclua o assistente. O Gestor de Configuração instala o servidor do site em modo passivo no servidor especificado.

Para um estado de instalação detalhado, na consola vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Status do Servidor do Site.** A unidade de segurança para o servidor do site em modo passivo exibe como **Instalação**. Para obter informações mais detalhadas, selecione o servidor e clique no **Estado do Espetáculo**. Esta ação abre a janela de estado de instalação do servidor do site. Quando o processo está concluído, o estado mostra **OK** para ambos os servidores.

Para obter mais informações sobre o processo de configuração, consulte [o Flowchart - Configurar um servidor de site em modo passivo](passive-site-server-flowchart.md).

Depois de adicionar um servidor de site em modo passivo, consulte os dois servidores do site no separador **Nódosos** no nó de **Sites** da consola.

Todos os componentes do servidor do site do Gestor de Configuração estão em modo de espera no servidor do site em modo passivo. Os serviços windows ainda estão em funcionamento.

## <a name="site-server-promotion"></a>Promoção do servidor do site  

Da mesma forma que com a cópia de segurança e recuperação, planeie e pratique o seu processo para alterar os servidores do site. Considere os seguintes pontos no seu plano de promoção:  

- Pratique uma promoção planeada, onde ambos os servidores do site estão online. Também pratique uma falha não planeada, desligando ou desligando à força o servidor do site em modo ativo.  

- Determine os seus processos operacionais durante o failover e o que comunicar com outros administradores do Gestor de Configuração.  

- Antes de uma promoção planeada:  

  - Verifique o estado geral dos componentes do site e do local. Certifique-se de que está tudo saudável como normal para o seu ambiente.  

  - Verifique o estado do conteúdo de quaisquer pacotes que se replicam ativamente entre os sites.  

  - Verifique o estado secundário do local e a replicação do local.

  - Não inicie novos trabalhos de distribuição de conteúdos ou manutenção em servidores de sites infantis ou secundários.

    > [!NOTE]
    > Se a replicação de ficheiros ou bases de dados entre os sites estiver em andamento durante a failover, o novo servidor do site pode não receber o conteúdo replicado. Se isso acontecer, redistribua o conteúdo do software depois de o novo servidor do site estar ativo.<!--515436--> Para a replicação da base de dados, poderá necessitar de reinicializar um site secundário após a falha.<!-- SCCMDocs issue 808 -->

  - Reduza ou remova outras atividades programadas ao mesmo tempo. Por exemplo, não planeie promover um servidor de site imediatamente após atualizar o site para uma nova versão. A atualização do site inclui outras tarefas que podem potencialmente entrar em conflito com a promoção do servidor do site.

    > [!TIP]
    > Aqui está um exemplo de como outras atividades podem entrar em conflito com a promoção do servidor do site:
    >
    > - Segunda-feira: Atualizar o site para a versão mais recente. Ativar a atualização automática do cliente com a pilotagem do cliente.
    > - Terça-feira: Promover o servidor do site em modo passivo para ser o servidor do site ativo.
    >
    > Até quarta ou quinta-feira, esta ação pode levar *todos os* clientes a fazer upgrade, e não apenas a coleção piloto. Este comportamento pode causar uma utilização significativa da rede e uma carga inesperada nos pontos de distribuição.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processo para promover o servidor do site em modo passivo para o modo ativo

Esta secção descreve como alterar o servidor do site em modo passivo para o modo ativo. Para aceder ao site e fazer esta alteração, é necessário ter acesso a uma instância do Provedor de SMS. Para mais informações, consulte [Utilize vários Fornecedores de SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Se todos os casos do Fornecedor SMS estiverem offline, não pode ligar-se ao site, uma vez que nenhum fornecedor está disponível. Quando adicionar o servidor do site em modo passivo, a configuração instala uma instância do Fornecedor SMS neste servidor.<!-- SCCMDocs#1613 -->
>
> A consola Do Gestor de Configuração solicita a lista de Fornecedores de SMS disponíveis da WMI no servidor do site. Ao instalar vários Fornecedores de SMS num site, o site atribui aleatoriamente cada novo pedido de ligação para utilizar um Fornecedor sms instalado. Não é possível especificar a localização do Fornecedor SMS para utilizar com uma sessão de ligação específica. Se a sua consola não conseguir ligar-se ao site porque o servidor do site atual está offline, especifique o outro servidor do site na janela de Ligação do Site.  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site e, em seguida, mude para o separador **Nós.** Selecione o servidor do site em modo passivo e, em seguida, clique em **Promover para ativo** na fita. Clique **em Sim** para confirmar e continuar.
  
2. Refresque o nó da consola. A coluna **'Estado'** para o servidor que está a promover exibe no separador **Nós** como **Promoção**.  

3. Após a promoção estar concluída, a coluna **Status** mostra **OK** tanto para o novo servidor do site em modo ativo, como para o novo servidor do site em modo passivo. A coluna Nome do **Servidor** para o site apresenta agora o nome do novo servidor do site no modo ativo.

Para obter um estado detalhado, vá ao espaço de trabalho **de Monitorização** e selecione o nó de Estado do Servidor do **Site.** A coluna **Modo** identifica qual *o* servidor ativo ou *passivo*. Quando promover um servidor do modo passivo para o modo ativo, selecione o servidor do site que está a promover para ativo e, em seguida, escolha o Estado do **Espetáculo** a partir da fita. Esta ação abre a janela de Estado de Promoção do Servidor do Site que apresenta detalhes adicionais sobre o processo.

Quando um servidor de site em modo ativo muda para o modo passivo, apenas a função do sistema do site é tornada passiva. Todas as outras funções do sistema do site que estão instaladas nesse computador permanecem ativas e acessíveis aos clientes.

Para obter mais informações sobre o processo de promoção *planeado,* consulte Flowchart - Promover o servidor do [site (planeado)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Ativação pós-falha não planeada

Se o servidor do site atual em modo ativo estiver offline, o servidor do site para promoção tenta contactar o servidor do site atual no modo ativo durante 30 minutos. Se o servidor offline voltar antes deste tempo, é notificado com sucesso, e a mudança prossegue graciosamente. Caso contrário, o servidor do site para promoção atualiza à força a configuração do site para que esteja ativo. Se o servidor offline voltar após este tempo, verifica primeiro o estado atual na base de dados do site. Em seguida, procede com a despromoção para o servidor do site em modo passivo.

Durante este período de espera de 30 minutos, o site não tem servidor de site em modo ativo. Os clientes ainda comunicam com papéis orientados para o cliente, tais como pontos de gestão, pontos de atualização de software e pontos de distribuição. Os utilizadores podem instalar software que já está implementado. Nenhuma administração do site é possível neste período de tempo. Para mais informações, consulte [os impactos de falha do Site.](../../manage/site-failure-impacts.md)  

Se o servidor offline estiver danificado de modo a não poder regressar, elimine este servidor de site da consola. Em seguida, crie um novo servidor de site em modo passivo para restaurar um serviço altamente disponível.

Para obter mais informações sobre o processo de failover *não planeado,* consulte Flowchart - Promover o servidor do [site (não planeado)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Tarefas adicionais após a promoção do servidor do site  

Depois de trocar os servidores do site, não tem de fazer a maioria das outras tarefas necessárias para [recuperar um site](../../manage/recover-sites.md#post-recovery-tasks). Por exemplo, não precisa de redefinir palavras-passe ou reconectar a subscrição microsoft Intune.

Podem ser necessários os seguintes passos no seu ambiente:  

- Se importar certificados PKI para pontos de distribuição, reimporte o certificado para servidores afetados. Para obter mais informações, consulte [Regenerar os certificados para pontos de distribuição](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Se integrar o Gestor de Configuração com a Microsoft Store for Business, reconfigure essa ligação. Para mais informações, consulte [Gerir aplicações da Microsoft Store para negócios.](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

## <a name="daily-monitoring"></a>Monitorização diária

Quando tiver um servidor de site em modo passivo, monitorize-o diariamente. Certifique-se de que o seu Estado permanece OK e está pronto a ser utilizado. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó de **Status do Servidor do Site.** Ver tanto os servidores do site como o seu estado atual. Veja também o estado no espaço de trabalho da **Administração.** Expandir a **Configuração**do Site, e selecionar o nó **de Sites.** Selecione o site e, em seguida, mude para o separador **Nós.**

> [!NOTE]
> Quando atualiza o site para uma nova versão do 'Gestor de Configuração', também atualiza o servidor do site em modo passivo. <!-- SCCMDocs-pr#4293 -->