---
title: Configurar o laboratório
titleSuffix: Configuration Manager
description: Criar um laboratório para avaliar o Gestor de Configuração com atividades simuladas na vida real.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a23f6106a8c922b3ff4e8306fb76aec4fd26b148
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711610"
---
# <a name="set-up-a-configuration-manager-lab"></a>Criar um laboratório de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Seguir a orientação neste tópico permitir-lhe-á criar um laboratório para avaliar o Gestor de Configuração com atividades simuladas na vida real.  

> [!NOTE]
> A Microsoft oferece uma versão pré-configurada deste laboratório utilizando uma versão de avaliação do ConfigurManager. Para mais informações, consulte o kit de laboratório de [implementação e gestão do Windows e do Office.](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab) 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Componentes principais  
 A configuração do seu ambiente para o Gestor de Configuração requer alguns componentes centrais para suportar a instalação do Gestor de Configuração.    

-   O ambiente de laboratório utiliza o **Windows Server 2012 R2,** no qual vamos instalar o Gestor de Configuração.  

     Pode descarregar uma versão de avaliação do Windows Server 2012 R2 do [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Considere modificar ou desativar a Configuração de Segurança Melhorada do Internet Explorer para aceder mais facilmente a alguns dos downloads referenciados ao longo destes exercícios. Reveja [Internet Explorer: configuração de segurança avançada](https://technet.microsoft.com/library/dd883248\(v=ws.10\).aspx) para obter informações adicionais.  

-   **O ambiente de laboratório utiliza o SQL Server 2012 SP2** para a base de dados do site.  

     Pode descarregar uma versão de avaliação do SQL Server 2012 do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43340).  

     O SQL Server tem [versões suportadas do Servidor SQL](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) que devem ser satisfeitas para utilização com o Gestor de Configuração.  

    -   O Gestor de Configuração requer uma versão de 64 bits do SQL Server para alojar a base de dados do site.  

    -   **SQL_Latin1_General_CP1_CI_AS** como classe do **Agrupamento SQL** . A  

    -   **Autenticação do Windows**, [em vez da autenticação SQL](https://technet.microsoft.com/library/ms144284.aspx), é necessária.  

    -   É necessária uma instância dedicada ao **Servidor SQL.**  

    -   Não limite a **memória endereçada** do sistema para o Servidor SQL.  

    -   Configure a conta de **serviço SQL Server** para executar usando uma conta de utilizador de domínio de baixos direitos.  

    -   Tem de instalar serviços de **reporte do SQL Server**.  

    -   **Comunicações entre locais** utiliza o SQL Server Service Broker na porta predefinida TCP 4022. As  

    -   **As comunicações intra-locais** entre o motor de base de dados do Servidor SQL e as funções do sistema de configuração do Gestor de Configuração utilizam a porta padrão TCP 1433.  

-   O controlador de domínio utiliza o **Windows Server 2008 R2** com serviços de domínio de diretório ativo instalados. O controlador de domínio também funciona como anfitrião para os servidores DHCP e DNS para utilização com um nome de domínio totalmente qualificado.  

     Para mais informações, reveja esta visão geral dos Serviços de Domínio do [Diretório Ativo.](https://technet.microsoft.com/library/hh831484)  

-   **O Hyper-V é utilizado com algumas máquinas virtuais** para verificar se as medidas de gestão tomadas nestes exercícios estão a funcionar como esperado. Recomenda-se um mínimo de três máquinas virtuais, com o Windows 10 instalado.  

     Para mais informações, reveja esta [visão geral da Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).  

-   **permissões de administrador** são necessárias para todos estes componentes. O  

    -   O Gestor de Configuração requer um administrador com permissões locais dentro do ambiente do Windows Server  

    -   do Active Directory requer um administrador com permissões para modificar o esquema  

    -   Máquinas virtuais requerem permissões locais nas próprias máquinas  

Apesar de não ser necessário para este laboratório, pode rever [as configurações suportadas para o Gestor](../../core/plan-design/configs/supported-configurations.md) de Configuração para obter informações adicionais sobre os requisitos para a implementação do Gestor de Configuração. Consulte a documentação para versões de software que não as referenciadas aqui.  

Depois de ter instalado todos estes componentes, existem passos adicionais que deve tomar para configurar o ambiente do Windows para O Gestor de Configuração:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Preparar o conteúdo do Active Directory para o laboratório  
 Para este laboratório, irá criar um grupo de segurança, em seguida, adicionar um utilizador de domínio ao mesmo.  

-   Grupo de segurança: **Evaluation**  

    -   Âmbito do grupo: **Universal**  

    -   Tipo de grupo: **Security**  

-   Utilizador de domínio: **ConfigUser**  

     Em circunstâncias normais, não concederia acesso universal a todos os utilizadores no seu ambiente. Está a fazê-lo com este utilizador para simplificar a colocação do seu laboratório online.  

Os próximos passos necessários para permitir aos clientes do Gestor de Configuração consultar os Serviços de Domínio do Diretório Ativo para localizar os recursos do site estão listados nos próximos procedimentos.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Criar o contentor de Gestão do Sistema.  
 O Gestor de Configuração não criará automaticamente o recipiente de Gestão de Sistemas necessário nos Serviços de Domínio de Diretório Ativo quando o esquema for estendido. Por conseguinte, irá criar este para o laboratório. Este passo irá solicitar-lhe que [instale o Editor de ADSI.](https://technet.microsoft.com/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)  

 Certifique-se de que iniciou sessão com uma conta que tenha a permissão **Criar Todos os Objetos Subordinados** no recipiente **Sistema** nos Serviços de Domínio do Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Para criar o contentor de Gestão do Sistema:  

1.  Execute o **Editor de ADSI**e estabeleça ligação ao domínio em que reside o servidor de site.  

2.  **New**Expandir o nome **Object** **\>** **&lt;\>** de domínio do domínio totalmente qualificado, expandir<nome distinto, clique direito **CN=System,** clique em Novo , e, em seguida, clique em Object .  

3.  Na caixa de diálogo **Criar Objeto** , selecione **Contentor**e clique em **Seguinte**.  

4.  Na caixa **Valor** , escreva **System Management**e, em seguida, clique em **Seguinte**.  

5.  Clique em **Concluir** para concluir o procedimento.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Definir permissões de segurança no contentor de Gestão do Sistema  
 Conceda à conta do computador do servidor de site as permissões necessárias para publicar informações do site no contentor. Irá utilizar também o Editor de ADSI para esta tarefa.  

> [!IMPORTANT]  
>  Certifique-se de que está ligado ao domínio do servidor de site antes de iniciar o procedimento seguinte.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Para definir permissões de segurança no contentor de Gestão do Sistema:  

1.  No painel da consola, expanda o **domínio do servidor do site,** expanda o nome **&lt;\>distinto**do servidor DC= e, em seguida, expanda o **CN=System**. Clique com o botão direito do rato em **CN=System Management**e clique em **Propriedades**.  

2.  Na caixa de diálogo **CN=Propriedades de gestão do sistema** , clique no separador **Segurança** e, em seguida, clique em **Adicionar** para adicionar a conta de computador do servidor de site. Conceda permissões de **Controlo Total** à conta.  

3.  Clique em **Avançado,** selecione a conta de computador do servidor do site e, em seguida, clique em **Editar**.  

4.  Na lista **Aplicar em** , selecione **Este objeto e os objetos subordinados**.  

5.  Clique em **OK** para fechar a consola **Editor de ADSI** e conclua o procedimento.  

     Para obter informações adicionais sobre este procedimento, por favor, reveja [O esquema de Diretório Ativo para O Gestor](../../core/plan-design/network/extend-the-active-directory-schema.md) de Configuração  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Expandir o esquema do Active Directory utilizando ExtADSch.exe  
 Irá estender o esquema de Diretório Ativo para este laboratório, pois isto permite-lhe utilizar todas as funcionalidades e funcionalidades do Gestor de Configuração com a menor quantidade de despesas administrativas. A extensão do esquema do Active Directory é uma configuração de toda a floresta e só pode ser efetuada uma vez por floresta. Expandir o esquema permanentemente modifica o conjunto de classes e atributos na configuração base do Active Directory. Esta ação é irreversível. O alargamento do esquema permite ao Gestor de Configuração aceder a componentes que lhe permitam funcionar de forma mais eficaz dentro do seu ambiente de laboratório.  

> [!IMPORTANT]  
>  Certifique-se de que iniciou sessão no controlador de domínio principal do esquema com uma conta que seja membro do grupo de segurança **Admins de esquemas** . Qualquer tentativa de utilizar credenciais alternativas irá falhar.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Para expandir o esquema do Active Directory utilizando ExtADSch.exe:  

1.  Crie uma cópia de segurança do estado do controlador de domínio mestre do esquema. Para obter mais informações sobre como fazer uma cópia de segurança do controlador de domínio principal, consulte [Cópia de Segurança do Windows Server](https://technet.microsoft.com/library/cc770757.aspx)  

2.  Navegue para **\SMSSETUP\BIN\X64** no suporte de dados de instalação.  

3.  Execute o **extadsch.exe**.  

4.  Certifique-se de que a extensão do esquema foi bem sucedida, revendo o **extadsch.log** localizado na pasta de raiz da unidade do sistema.  

     Para obter informações adicionais sobre este procedimento, consulte [o esquema de Diretório Ativo para O Gestor](../../core/plan-design/network/extend-the-active-directory-schema.md)de Configuração .  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Outras tarefas necessárias  
 Também terá de realizar as seguintes tarefas antes da instalação.  

 **Criar uma pasta para armazenar todas as transferências**  

 Durante este exercício, é provável que sejam necessárias várias transferências para os componentes do suporte de instalação. Antes de iniciar os procedimentos de instalação, determine uma localização que não requeira a transferência destes ficheiros até que decida desativar o laboratório. É recomendável utilizar uma única pasta com subpastas separadas para armazenar estas transferências.  

 **Instale o .NET e ative a Windows Communication Foundation**  

 Tem de instalar duas .NET Frameworks: primeiro, a .NET 3.5.1 e depois a .NET 4.5.2+. Terá também de ativar a WCF (Windows Communication Foundation). A WCF foi concebida para oferecer uma abordagem para cálculo distribuído, interoperabilidade abrangente e suporte direto para orientação do serviço e simplifica a programação de aplicações ligadas através de um modelo de programação orientado para o serviço. Reveja [O que é a Windows Communication Foundation?](https://technet.microsoft.com/subscriptions/ms731082\(v=vs.90\).aspx) para informações adicionais sobre a WCF.  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Para instalar o .NET e ativar a Windows Communication Foundation:  

1.  Abra o **Server Manager**e depois navegue para **Gerir**. Clique em **adicionar papéis e funcionalidades** para abrir os **papéis e funcionalidades adicionais.**  

2.  Reveja as informações fornecidas no painel **Antes de Começar** e, em seguida, clique em **Seguinte**.  

3.  Selecione **Instalação baseada em funções ou funcionalidades**e, em seguida, clique em **Seguinte**.  

4.  Selecione o servidor em **Agrupamento de Servidores**e, em seguida, clique em **Seguinte**.  

5.  Reveja o painel **Funções de Servidor** e, em seguida, clique em **Seguinte**.  

6.  Adicione as seguintes **Funcionalidades** selecionando-as na lista:  

    -   **Funcionalidades do .NET Framework 3.5**  

        -   **.NET Framework 3.5 (inclui .NET 2.0 e 3.0)**  

    -   **Funcionalidades do .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **Serviços WCF**  

            -   **Ativação HTTP**  

            -   **Partilha de portas TCP**  

7.  Reveja **Função de Servidor Web (IIS)** e o ecrã **Serviços de Função** e, em seguida, clique em **Seguinte**.  

8.  Reveja o ecrã **Confirmação** e, em seguida, clique em **Seguinte**.  

9. Clique em **Instalar** e certifique-se de que a instalação foi concluída corretamente no painel **Notificações** do **Gestor de Servidores**.  

10. Depois de concluída a instalação base do .NET, navegue para o [Centro de Transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=42643) para obter o instalador da Web para o .NET Framework 4.5.2. Clique no botão **Transferir** e, em seguida, em **Executar** para iniciar o instalador. O instalador irá detetar e instalar automaticamente os componentes necessários no idioma selecionado.  

Para obter mais informações, consulte os seguintes artigos para saber porque motivo estes .NET Frameworks são necessários:  

-   [Versões e dependências do .NET Framework](https://technet.microsoft.com/library/bb822049.aspx)  

-   [Instruções de Compatibilidade de Aplicações do .NET Framework 4 RTM](https://technet.microsoft.com/library/dd889541.aspx)  

-   [Como: atualizar uma Aplicação Web ASP.NET para ASP.NET 4](https://technet.microsoft.com/library/dd483478\(VS.100\).aspx)  

-   [Perguntas Frequentes sobre a Política de Ciclo de Vida do Microsoft .NET Framework](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR Inside out - In-Process Lado a Lado](https://msdn.microsoft.com/magazine/ee819091.aspx)  

**Ativar BITS, IIS e RDC**  

O [Serviço de Transferência Inteligente em Segundo Plano (BITS)](https://technet.microsoft.com/library/dn282296.aspx) é utilizado para aplicações que têm de transferir ficheiros assíncronos entre um cliente e um servidor. Ao medir o fluxo de transferências em primeiro e segundo plano, o BITS mantém a capacidade de resposta de outras aplicações de rede. Retoma também automaticamente as transferências de ficheiros se uma sessão de transferência for interrompida.  

O utilizador deve instalar o BITS para este laboratório, porque este servidor de site será também utilizado como ponto de gestão.  

Serviços de Informação Internet (IIS) é um servidor Web flexível e escalável que pode ser utilizado para alojar tudo na Web. É utilizado pelo Gestor de Configuração para uma série de funções do sistema do site. Para obter informações adicionais sobre o IIS, reveja [os Websites para servidores do sistema do site.](../../core/plan-design/network/websites-for-site-system-servers.md)  

[Compressão de Diferencial Remota (RDC)](https://technet.microsoft.com/library/cc754372.aspx) é um conjunto de API que as aplicações podem utilizar para determinar se foram efetuadas quaisquer alterações a um conjunto de ficheiros. A RDC permite que a aplicação replique apenas as partes alteradas de um ficheiro, mantendo o tráfego de rede para um mínimo.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Para ativar as funções de servidor de site BITS, IIS e RDC:  

1.  No servidor de site, abra **Server Manager**. Navegue até **Gerir**. Clique em **Adicionar Funções e Funcionalidades** para abrir o **Assistente para Adicionar Funções e Funcionalidades**.  

2.  Reveja as informações fornecidas no painel **Antes de Começar** e, em seguida, clique em **Seguinte**.  

3.  Selecione **Instalação baseada em funções ou funcionalidades**e, em seguida, clique em **Seguinte**.  

4.  Selecione o servidor em **Agrupamento de Servidores**e, em seguida, clique em **Seguinte**.  

5.  Adicione as seguintes **Funções de Servidor** selecionando-as na lista:  

    -   **Servidor Web (IIS)**  

        -   **Funcionalidades HTTP Comuns**  

            -   **Documento Predefinido**  

            -   **Navegação nos Diretórios**  

            -   **ERROS HTTP**  

            -   **Conteúdo Estático**  

            -   **Redireccionamento de HTTP**  

        -   **Estado de Funcionamento e de Diagnóstico**  

            -   **Registo HTTP**  

            -   **Ferramentas de Registo**  

            -   **Monitor de Pedidos**  

            -   **Rastreio**  

    -   **Desempenho**  

        -   **Compressão de Conteúdo Estático**  

        -   **Compressão de Conteúdo Dinâmico**  

    -   **Segurança**  

        -   **Filtragem de Pedidos**  

        -   **Autenticação Básica**  

        -   **Autenticação por Mapeamento de Certificados de Clientes**  

        -   **Restrições de Domínio e de IP**  

        -   **Autorização de URL**  

        -   **Autenticação do Windows**  

    -   **Desenvolvimento de Aplicações**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **Extensões ISAPI**  

        -   **Filtros ISAPI**  

        -   **O Lado do Servidor Inclui**  

    -   **Servidor FTP**  

        -   **Serviço FTP**  

    -   **Ferramentas de Gestão**  

        -   **Consola de Gestão do IIS**  

        -   **Compatibilidade de Gestão do IIS 6**  

            -   **Compatibilidade com Metabase do IIS 6**  

            -   **Consola de Gestão do IIS 6**  

            -   **Ferramentas de Scripts do IIS 6**  

            -   **Compatibilidade com WMI do IIS 6**  

        -   **Scripts e Ferramentas de Gestão do IIS 6**  

        -   **Serviço de Gestão**  

6.  Adicione as seguintes **Funcionalidades** selecionando-as na lista:  

    -   **Serviço de Transferência Inteligente em Segundo Plano (BITS)**  

          -   **Extensão de Servidor IIS**  

    -   **Ferramentas de Administração Remota do Servidor**  

          -   **Ferramentas de Administração de Funcionalidades**  

          -   **Ferramentas de Extensões de Servidor BITS**  

7.  Clique em **Instalar** e certifique-se de que a instalação foi concluída corretamente no painel **Notificações** do **Gestor de Servidores**.  

Por predefinição, o IIS bloqueia vários tipos de extensões de ficheiro e localizações de pastas contra o acesso através de comunicação HTTP ou HTTPS. Para permitir que estes ficheiros sejam distribuídos a sistemas cliente, terá de configurar a filtragem de pedidos do IIS no ponto de distribuição. Para mais informações, reveja [IIS Request Filtering for distribution points](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Para configurar a filtragem de IIS nos pontos de distribuição:  

1.  Abra **IIS Manager** e selecione o nome do seu servidor na barra lateral. Esta ação permite-lhe aceder ao ecrã **Início** .  

2.  Certifique-se de que **Vista de Funcionalidades** está selecionada na parte inferior do ecrã **Início** . Navegue para **IIS** e abra **Filtragem de Pedidos**.  

3.  No painel **Ações** , clique em **Permitir Extensão de Nome de Ficheiro…**  

4.  Introduza **.msi** na caixa de diálogo e clique em **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Instalar o Gestor de Configuração  
Criará um [Determine quando utilizar um site primário](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) para gerir diretamente os clientes. Isto permitirá ao seu ambiente de laboratório apoiar a gestão da escala do [sistema do Site](../plan-design/configs/size-and-scale-numbers.md) de potenciais dispositivos.  
Durante este processo, também irá instalar a consola 'Gestor de Configuração', que será usada para gerir os seus dispositivos de avaliação.  

Antes de iniciar a instalação, inicie o  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) no servidor utilizando o Windows Server 2012 para confirmar que todas as definições foram ativadas corretamente.  

#### <a name="to-download-and-install-configuration-manager"></a>Para transferir e instalar o Gestor de Configuração:  

1.  Navegue na página de [Avaliações](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) do Centro de Sistema para descarregar a mais recente versão de avaliação do Gestor de Configuração.  

2.  Descomprima o suporte de dados de transferência para a localização predefinida.  

3.  Siga o procedimento de instalação listado no [Site Instale um site utilizando o Assistente de Configuração do Gestor](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)de Configuração . De acordo com esse procedimento, deve introduzir o seguinte:  

    |Passo no procedimento de instalação do site|Seleção|  
    |-----------------------------------------|---------------|  
    |Passo 4: a página **Chave de produto**|Selecione **Avaliação**.|  
    |Passo 7:  **Transferências de Pré-requisitos**|Selecione **Transferir ficheiros necessários** e especifique a localização predefinida.|  
    |Passo 10: **Definições de Instalação e Site**|-   **Código do site:LAB**<br />-   **Nome do site:Evaluation**<br />-   **Pasta de instalação:** especifique a localização predefinida.|  
    |Passo 11: **Instalação de Site Principal**|Selecione **Instalar o site principal como um site autónomo**, em seguida, clique em **Seguinte**.|  
    |Passo 12: **Instalação da Base de Dados**|-   **Nome de SQL Server (FQDN):** aqui o FQDN.<br />-   **Nome da instância:** deixe em branco, porque irá utilizar a instância predefinida do SQL que instalou anteriormente.<br />-   **Porta do Service Broker:** deixe como a porta predefinida de 4022.|  
    |Passo 13: **Instalação da Base de Dados**|Deixe estas definições como a predefinição.|  
    |Passo 14: **Provedor de SMS**|Deixe estas definições como a predefinição.|  
    |Passo 15: **Definições de Comunicação de Cliente**|Confirme se **Todas as funções do sistema de site aceitam apenas comunicação HTTPS dos clientes** não estiver selecionada|  
    |Passo 16: **Funções do Sistema de Sites**|Introduza o FQDN e confirme que a seleção de **Todas as funções do sistema de site aceitam apenas comunicação HTTPS dos clientes** ainda está desmarcada.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a>Ativar a publicação para o site do Gestor de Configuração  
Cada site do Gestor de Configuração publica as suas próprias informações específicas do site para o recipiente de Gestão de Sistemas dentro da sua partilha de domínio no esquema de Diretório Ativo. Os canais bidirecionais para comunicação entre diretório ativo e Gestor de Configuração devem ser abertos para lidar com este tráfego. Irá também ativar a Deteção de Florestas para determinar certos componentes do seu Active Directory e da infraestrutura de rede.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação:  

1.  No canto inferior esquerdo da consola do Gestor de Configuração, clique em **Administration**.  

2.  Na área de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Métodos de Deteção**.  

3.  Selecione **Deteção de Florestas do Active Directory** e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , selecione **Ativar Deteção de Floresta do Active Directory**. Quando esta opção estiver ativa, selecione **Criar limites de site do Active Directory automaticamente quando os mesmos forem detetados**. É apresentada uma caixa de diálogo que indica **Quer executar a deteção completa assim que possível?** Clique **sim**.  

5.  No grupo **Método de Deteção** na parte superior do ecrã, clique em **Executar Agora a Deteção de Florestas**e, em seguida, navegue para **Florestas do Active Directory** na barra lateral. A floresta do Active Directory deve ser mostrada na lista de florestas detetadas.  

6.  Navegue para a parte superior do ecrã, para o separador **Geral** .  

7.  Na área de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Florestas do Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Para permitir que um site do Gestor de Configuração publique informações do site para a sua floresta de Diretório Ativo:  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Irá configurar uma nova floresta que ainda não tenha sido detetada.  

3.  Na área de trabalho **Administração** , clique em **Florestas do Active Directory**.  

4.  No separador **Publicação** das propriedades do site, selecione a floresta ligada e, em seguida, clique em **Ok** para guardar a configuração.
