---
title: Armazém de dados
titleSuffix: Configuration Manager
description: Ponto de serviço de armazém de dados e base de dados para Gestor de Configuração
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: abe6b05d24955959e1d08defc2c5054c4499d756
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075596"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>O ponto de serviço de armazém de dados para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1277922-->
Utilize o ponto de serviço de armazém de dados para armazenar e reportar dados históricos a longo prazo para a sua implementação do Gestor de Configuração.

> [!Note]  
> Na versão 1910, o Gestor de Configuração permite esta funcionalidade por padrão. Na versão 1906 ou anterior, o Gestor de Configuração não permite esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](install-in-console-updates.md#bkmk_options).<!--505213-->  


O armazém de dados suporta até 2 TB de dados, com carimbos temporais para rastreio de alterações. O armazém de dados armazena dados sincronizando automaticamente os dados da base de dados do Site Do Gestor de Configuração para a base de dados do armazém de dados. Esta informação é então acessível a partir do seu ponto de serviço de reporte. Os dados sincronizados na base de dados do armazém de dados são mantidos durante três anos. Periodicamente, uma tarefa incorporada remove dados que têm mais de três anos.

Os dados sincronizados incluem o seguinte dos grupos Global Data and Site Data:
- Saúde das infraestruturas
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes do inventário (no entanto, o histórico de inventário não é sincronizado)

Quando a função do sistema do site se instala, instala e configura a base de dados do armazém de dados. Também instala vários relatórios para que possa facilmente pesquisar e reportar sobre estes dados.

A partir da versão 1810, pode sincronizar mais tabelas desde a base de dados do site até ao armazém de dados. Esta alteração permite-lhe criar mais relatórios com base nos seus requisitos de negócio.<!--1358870--> 



## <a name="prerequisites"></a>Pré-requisitos

- A função do sistema de site de armazenamento de dados é suportada apenas no local de topo da sua hierarquia. Por exemplo, um site de administração central ou um local primário autónomo.  

- O computador onde instala a função do sistema do site requer .NET Framework 4.5.2 ou posterior.  

- Conceda a Conta ponto de informação dos serviços de **informação** a **db_datareader** permissão na base de dados do armazém de dados.  

- Para sincronizar dados com a base de dados do armazém de dados, o Gestor de Configuração utiliza a conta de computador da função do sistema do site. Esta conta requer as seguintes permissões:  

    - **Administrador** no computador que acolhe a base de dados do armazém de dados.  

    - **DB_Creator** permissão na base de dados do armazém de dados.  

    - Quer **DB_owner** ou **DB_reader** com permissões de **execução** para a base de dados do site de topo.  

- A base de dados do armazém de dados requer a utilização do SQL Server 2012 ou posteriormente. A edição pode ser Standard, Enterprise ou Datacenter. A versão SQL Server para o armazém de dados não precisa de ser a mesma que o servidor de base de dados do site.<!--SCCMDocs issue 662-->  

- A base de dados do armazém suporta as seguintes configurações do Servidor SQL:  

    - Uma instância padrão ou nomeada  

    - SQL Server Sempre No grupo de disponibilidade  

    - Cluster de falha do Servidor SQL  

- Se utilizar [vistas distribuídas,](../../plan-design/hierarchy/database-replication.md#bkmk_distviews)o ponto de serviço do armazém de dados deve instalar-se no mesmo servidor que acolhe a base de dados do site da administração central.  

Para obter mais informações sobre o licenciamento do SQL Server, consulte o [produto e licenciando as FAQ](../../understand/product-and-licensing-faq.md). <!-- sms500967 -->

Dimensione a base de dados do armazém de dados da mesma forma que a base de dados do seu site. Enquanto o armazém de dados é menor no início, vai crescer com o tempo. <!--SCCMDocs issue 756-->



## <a name="install"></a>Instalar

Cada hierarquia suporta uma única instância desta função, em qualquer sistema de site do site de topo. O Servidor SQL que acolhe a base de dados do armazém pode ser local para a função do sistema do site, ou remoto. O armazém de dados trabalha com o ponto de serviços de reporte instalado no mesmo local. Não é necessário instalar as duas funções do sistema de site no mesmo servidor.   

Para instalar a função, utilize o Assistente de **Funções** do Sistema do Site adicionar ou criar o Assistente do Servidor do **Sistema do Site**. Para mais informações, consulte [Instalar as funções](../deploy/configure/install-site-system-roles.md)do sistema do site. Na página de Seleção de **Funções** do Sistema do assistente, selecione a função de ponto de serviço data **Warehouse.** 

Quando instala a função, o Gestor de Configuração cria a base de dados do armazém de dados para si na instância do Servidor SQL que especifica. Se especificar o nome de uma base de dados existente, o Gestor de Configuração não cria uma nova base de dados. Em vez disso, usa o que especifica. Este processo é o mesmo que quando [se desloca a base de dados do armazém de dados para um novo Servidor SQL](#move-the-database).


### <a name="configure-properties"></a>Configurar propriedades

#### <a name="general-page"></a>Página geral

- Nome de domínio totalmente qualificado do **SQL Server**: Especifique o nome de domínio completo qualificado (FQDN) do servidor que acolhe a base de dados de pontos de serviço do armazém de dados.  

- Nome da **instância do Servidor SQL, se aplicável**: Se não utilizar uma instância predefinida do Servidor SQL, especifique a instância nomeada.  

- **Nome da base**de dados : Especifique um nome para a base de dados do armazém de dados. O Gestor de Configuração cria a base de dados do armazém de dados com este nome. Se especificar um nome de base de dados que já existe na instância do servidor SQL, o Gestor de Configuração utiliza essa base de dados.  

- **Porta SQL Server utilizada para a ligação**: Especifique o número de porta TCP/IP utilizado pelo Servidor SQL que acolhe a base de dados do armazém de dados. O serviço de sincronização de armazéns de dados utiliza esta porta para se ligar à base de dados do armazém de dados. Por padrão, utiliza a porta SQL Server **1433** para comunicação.  

- **Conta**de ponto de serviço de armazém de dados : A partir da versão 1802, detete o nome de **utilizador** que os Serviços de Informação do Servidor SQL utilizam quando se conecta à base de dados do armazém de dados.  


#### <a name="synchronization-schedule-page"></a>Página de horário de sincronização
*Aplica-se à versão 1806 e anterior*

- **Início**: Especifique o tempo em que pretende que a sincronização do armazém de dados comece.  

- **Padrão de recorrência**

    - **Diariamente**: Especifique que a sincronização é executado todos os dias.  

    - **Semanalmente**: Especifique um único dia por semana e recorrência semanal para sincronização.


#### <a name="synchronization-settings-page"></a>Página de definições de sincronização
*Aplica-se à versão 1810 e posterior*

- **Definição personalizada**de sincronização de dados : Escolha a opção para **Selecionar tabelas**. Na janela das tabelas base de dados, selecione os nomes das tabelas para sincronizar na base de dados do armazém de dados. Utilize o filtro para pesquisar pelo nome ou selecione a lista de drop-down para escolher grupos específicos. Selecione **OK** quando estiver completo para guardar.  

    > [!Note]  
    > Não é possível remover as tabelas que a função seleciona por defeito.  

- **Início**: Especifique o tempo em que pretende que a sincronização do armazém de dados comece.  

- **Padrão de recorrência**

    - **Diariamente**: Especifique que a sincronização é executado todos os dias.  

    - **Semanalmente**: Especifique um único dia por semana e recorrência semanal para sincronização.



## <a name="reporting"></a>Relatórios

Depois de instalar um ponto de serviço de armazém de dados, vários relatórios ficam disponíveis no ponto de serviços de reporte do site. Se instalar o ponto de serviço de depósito de dados antes de instalar um ponto de serviçode reporte, os relatórios são adicionados automaticamente quando instala o ponto de serviços de reporte.

> [!WARNING]  
> A partir da versão 1802, o ponto de armazém de dados suporta credenciais alternativas.<!--507334--> Se atualizou a partir de uma versão anterior do Gestor de Configuração, precisa especificar credenciais que os Serviços de Reporte de Servidores SQL utilizam para se ligarem à base de dados do armazém de dados. Os relatórios do armazém de dados não abrem até adicionarcredenciais. 
> 
> Para especificar uma conta, detete o nome do **Utilizador** para a conta de ponto de serviço do armazém de dados nas propriedades de função. Para mais informações, consulte [as propriedades da Configuração](#configure-properties). 

A função do sistema de site de armazém de dados inclui os seguintes relatórios, na categoria **Data Warehouse:**  

- **Implementação de Aplicações - Histórico**: Ver detalhes para a implementação de aplicações para uma aplicação e máquina específicas.  

- **Conformidade de Proteção de Pontofinal e Atualização**de Software - Histórico : Ver computadores que faltam atualizações de software.  

- **Inventário Geral de Hardware - Histórico**: Ver todo o inventário de hardware para uma máquina específica.  

- **Inventário Geral de Software - Histórico**: Ver todo o inventário de software para uma máquina específica.  

- **Visão geral da saúde da infraestrutura - Histórico:** Exibe uma visão geral da saúde da sua infraestrutura de Gestor de Configuração.  

- **Lista de Malware Detetado - Histórico**: Ver malware que foi detetado na organização.  

- **Resumo da Distribuição de Software - Histórico:** Um resumo da distribuição de software para um anúncio e máquina específicos.  



## <a name="site-expansion"></a>Expansão do site

Antes de poder instalar um site de administração central para expandir um local primário autónomo existente, primeiro desinstale a função de ponto de serviço de armazém de dados. Depois de instalar o site da administração central, pode então instalar a função do sistema do site no site da administração central.  

Ao contrário de um movimento da base de dados do armazém de dados, esta alteração resulta numa perda dos dados históricos que já sincronizou no local principal. Não é suportado para fazer cópias da base de dados do local principal e restaurá-la no site da administração central.



## <a name="move-the-database"></a>Mova a base de dados

Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo Servidor SQL:  

1. Utilize o Estúdio de Gestão de Servidores SQL para fazer o backup da base de dados do armazém de dados. Em seguida, devolte essa base de dados a um Servidor SQL no novo computador que acolhe o armazém de dados.  

    > [!NOTE]  
    > Depois de restaurar a base de dados do novo servidor, certifique-se de que as permissões de acesso à base de dados são as mesmas na nova base de dados de depósitos de dados como estavam na base de dados original do armazém de dados.  

2. Utilize a consola 'Gestor de Configuração' para remover a função de ponto de serviço do armazém de dados do servidor atual.  

3. Reinstale o ponto de serviço do armazém de dados. Especifique o nome do novo Servidor SQL e instância que acolhe a base de dados de armazém de dados restaurado.  

4. Após a instalação da função do sistema do local, o movimento está completo.  



## <a name="troubleshooting"></a>Resolução de problemas 

### <a name="log-files"></a>Ficheiros de registo 

Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do armazém de dados ou sincronização de dados:

- **DWSSMSI.log** e **DWSSSetup.log**: Utilize estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.  

- **Microsoft.ConfigMgrDataWarehouse.log**: Utilize este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.  


### <a name="set-up-failure"></a>Configurar falha 

Quando a função de ponto de serviço do armazém de dados é a primeira que instala num servidor remoto, a instalação falha no armazém de dados.  

#### <a name="workaround"></a>Solução 
Certifique-se de que o computador no qual instala o ponto de serviço do armazém de dados já acolhe pelo menos uma outra função.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Sincronização não conseguiu povoar objetos de esquema 

A sincronização falha com a seguinte mensagem no **Microsoft.ConfigMgrDataWarehouse.log**:`failed to populate schema objects`

#### <a name="workaround"></a>Solução 
Certifique-se de que a conta de computador da função do sistema do site é um **db_owner** na base de dados do armazém de dados de dados.


### <a name="reports-fail-to-open"></a>Os relatórios não abrem

Os relatórios do armazém de dados não abrem quando a base de dados de armazém de dados e o ponto de serviço de reporte estão em diferentes sistemas de sites.  

#### <a name="workaround"></a>Solução
Conceda a Conta ponto de informação dos serviços de **informação** a **db_datareader** permissão na base de dados do armazém de dados.


### <a name="error-opening-reports"></a>Relatórios de abertura de erros

Ao abrir um relatório de armazém de dados, devolve o seguinte erro:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Solução 
Utilize os seguintes passos para configurar certificados:

1. No computador que acolhe a base de dados do armazém de dados:  

    1. Abra o IIS, selecione **Certificados**de Servidor e, em seguida, clique à direita no **Certificado Criar Auto-Assinado**. Em seguida, especifique o "nome amigável" do nome do certificado como Certificado de Identificação do **Servidor Data Warehouse SQL**. Selecione a loja de certificados como **Pessoais**.  

    2. Abra o **Gestor de Configuração do SQL Server**. Sob a configuração da rede de **servidorS SQL,** clique no clique direito para selecionar **propriedades** sob **protocolos para MSSQLSERVER**. Mude para o separador **Certificado,** selecione **Data Warehouse SQL Server Identification Certificate** como certificado e, em seguida, guarde as alterações.  

    3. No **SQL Server Configuration Manager**, sob os **Serviços de Servidor SQL,** reinicie o **serviço SQL Server**. Se os Serviços de Reporte SQL também estiverem instalados no servidor que acolhe a base de dados do armazém de dados, reinicie também os serviços de Serviço de **Reporte.**  

    4. Abra a Consola de Gestão da Microsoft (MMC) e adicione os **Certificados** snap-in. Selecione **conta de computador** da máquina local. Expandir a pasta **Pessoal** e selecionar **Certificados**. Exportar o Certificado de Identificação do **Servidor SQL** do Armazém de Dados como um **DER codificado binário X.509 (. Arquivo CER).**  

2. No computador que acolhe os Serviços de Reporte de Servidores SQL, abra o MMC e adicione o snap-in dos **Certificados.** Selecione **conta de computador**. Sob a pasta **de Certificados de Raiz Fidedignos,** importe o Certificado de Identificação do **Servidor SQL do Armazém**de Dados .  



## <a name="data-flow"></a>Fluxo de dados   

![Diagrama mostrando o fluxo lógico de dados entre os componentes do local para o armazém de dados](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Armazenamento e sincronização de dados

| Passo   | Detalhes  |
|--------|----------|  
| **1**  | O servidor do site transfere e armazena dados na base de dados do site. |  
| **2**  | Com base na sua programação e configuração, o ponto de serviço do armazém de dados obtém dados da base de dados do site. |  
| **3**  | O ponto de serviço do armazém de dados transfere e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  


#### <a name="reporting"></a>Relatórios

| Passo   | Detalhes  |
|--------|----------|  
| **A**  | Utilizando relatórios incorporados, um utilizador solicita dados. Este pedido é passado para o ponto de serviço de reporte utilizando os Serviços de Reporte de Servidores SQL. |  
| **B**  | A maioria dos relatórios são para informações atuais, e estes pedidos são executados contra a base de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos utilizando um dos relatórios com uma *categoria* de **Data Warehouse,** o pedido vai contra a base de dados do armazém de dados. |  
