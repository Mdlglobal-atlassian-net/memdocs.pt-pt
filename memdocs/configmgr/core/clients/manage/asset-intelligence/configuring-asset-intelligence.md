---
title: Configurar o Asset Intelligence
titleSuffix: Configuration Manager
description: Configurar a Inteligência de Ativos no Gestor de Configuração.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1a5c89d3fdd82bfa654f806c6931bde2621e714b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906616"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Configure inteligência de ativos no gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os inventários de Inteligência de Ativos e gere o uso da licença de software.   

## <a name="steps-to-configure-asset-intelligence"></a>Passos para configurar o Asset Intelligence  
   

- **Passo 1**:Para recolher os dados de inventário necessários para os relatórios de Inteligência de Ativos, tem de ativar o agente cliente de inventário de hardware, tal como descrito em [Como alargar o inventário de hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Passo 2**: Ativar as classes de [relatórios de inventário](#BKMK_EnableAssetIntelligence)de hardware de inteligência de ativos .  
- **Passo 3**: [Instale um ponto](#BKMK_InstallAssetIntelligenceSynchronizationPoint) de sincronização da inteligência do ativo
- **Passo 4**: [Permitir a auditoria de eventos de logon de sucesso](#BKMK_EnableSuccessLogonEvents)  
- **Passo 5**: [Informações sobre licençade software de importação](#BKMK_ImportSoftwareLicenseInformation)  
- **Passo 6**: [Configure tarefas](#BKMK_ConfigureMaintenanceTasks) de manutenção da Inteligência de Ativos 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para ativar a Inteligência de Ativos em sites do Gestor de Configuração, deve ativar uma ou mais classes de relatórios de inventário de hardware de Inteligência de Ativos. Pode ativar as classes na home page do **Asset Intelligence** ou, na área de trabalho **Administração** , no nó **Definições do Cliente** , nas propriedades de definições de cliente. Utilize um dos seguintes procedimentos.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Para ativar classes de relatório de inventário de hardware do Asset Intelligence a partir da home page do Asset Intelligence  

1.  Na consola de Gestor de Configuração, escolha A Inteligência de **Ativos e**  >  **Compliance**.  

3.  No separador **Home,** no grupo De Inteligência de **Ativos,** escolha Aulas de **Inventário de Edição**.   

4.  Para ativar o reporte de Informação de Ativos, selecione Enable todas as classes de **relatórios de Inteligência de Ativos** ou ative **apenas as classes selecionadas**de relatórios de Inteligência de Ativos , e selecione pelo menos uma classe de reporte das classes apresentadas.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que ativar através deste procedimento não apresentam dados até que os clientes tenham analisado e devolvido o inventário de hardware.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Para ativar classes de relatório de inventário de hardware do Asset Intelligence a partir das propriedades de definições de cliente  

1.  Na consola do Gestor **Administration**de Configuração, escolha as  >   **Client Settings**  >  **definições padrão**do agente do cliente de Configuração do Cliente . Se criou configurações personalizadas do cliente, pode selecioná-las.  

3.  No separador **Casa** > **Properties,** escolha **Propriedades**.   

4.  Escolha as classes de conjunto de inventário de **hardware**  >  **Set Classes**. .  

5.  Escolha **filtro por categoria**Asset Intelligence Reporting  >  **Classes**. A lista de classes é atualizada apenas com as classes de relatório de inventário de hardware do Asset Intelligence.  

6.  Selecione pelo menos uma aula de reportagem da lista.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que ativar através deste procedimento não apresentam dados até que os clientes tenham analisado e devolvido o inventário de hardware.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

A função do site de sincronização de pontos de sincronização da Inteligência de Ativos é usada para ligar sites do Gestor de Configuração ao System Center Online para sincronizar informações do catálogo de Asset Intelligence. O ponto de sincronização da Inteligência de Ativos só pode ser instalado num sistema de site localizado no site de alto nível da hierarquia do Gestor de Configuração e requer acesso à Internet para sincronizar com o System Center Online utilizando a porta TCP 443.

Para além de transferir novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações personalizadas de títulos de software para o System Center Online para categorização. A Microsoft trata todos os títulos de software carregados como informação pública. Certifique-se de que os títulos de software personalizados não contêm informações confidenciais ou próprias. Para obter mais informações sobre o pedido de categorização de títulos de software, consulte [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Para instalar uma função de sistema de sites do ponto de sincronização do Asset Intelligence  

1.  Na consola do Gestor de Configuração, escolha servidores de configuração do site **de administração**e funções do sistema do >  **Site Configuration**  >  **site.**  

3.  Adicione a função do sistema de sistema de sincronização de dados de inteligência de ativos a um servidor de sistema de site novo ou existente:  

    -  Para um **novo servidor**de sistema de site : No separador **Home,** no grupo **Criar,** escolha criar o **Servidor do Sistema** do Site para iniciar o assistente.   

        > [!NOTE]  
        >  Por predefinição, quando o Gestor de Configuração instala uma função do sistema de instalação, os ficheiros de instalação são instalados na primeira unidade de disco rígido formada ntfs disponível que tem o espaço de disco rígido gratuito mais disponível. Para evitar que o Gestor de Configuração instale em unidades específicas, crie um ficheiro vazio chamado No_sms_on_drive.sms e copie-o para a pasta raiz da unidade antes de instalar o servidor do sistema do site.  

    -  Para um **servidor de sistema**de site existente : Escolha o servidor no qual pretende instalar a função do sistema de sistema de sincronização de dados de inteligência de ativos. Quando escolhe um servidor, uma lista das funções do sistema do site que já estão instaladas no servidor são apresentadas no painel de detalhes.  

         No separador **Home,** no grupo **Servidor,** escolha **adicionar a função** do sistema do site para iniciar o assistente.  

4.  Complete a página **geral.** Quando adiciona o ponto de sincronização do Asset Intelligence a um servidor do sistema de sites existente, verifique os valores que foram anteriormente configurados.  

5.  Na página de Seleção de Papéis do **Sistema,** selecione **Asset Intelligence Synchronization Point** da lista de funções disponíveis.  

6.  Na página de Definições de Definições de Ligação de **Pontode Sincronização** de Informação de Ativos, escolha **Next**.  

     Por predefinição, a definição **Utilizar este ponto de Sincronização do Asset Intelligence** está selecionada e não pode ser configurada nesta página. O System Center Online aceita tráfego de rede apenas através da porta TCP 443 e, por conseguinte, a definição **Número de porta SSL** não pode ser configurada nesta página do assistente.  

7.  Opcionalmente, pode especificar um caminho para o certificado de autenticação Online do System Center (.pfx). Normalmente, não é necessário especificar um caminho para o certificado porque o certificado de ligação é automaticamente aprovisionado durante a instalação da função de site.  

8.  Na página definições do **Proxy Server,** especifique se o ponto de sincronização da Inteligência de Ativos utilizará um servidor proxy ao ligar-se ao System Center Online para sincronizar o catálogo e se utilizar ás credenciais para se ligar ao servidor proxy.  

    > [!WARNING]  
    >  Se for necessário um servidor proxy para ligar ao System Center Online, o certificado de ligação também pode ser eliminado se a palavra-passe da conta de utilizador expirar para a conta configurada para autenticação do servidor proxy.  

9. Na página **Agendamento da Sincronização** , especifique se pretende sincronizar catálogo do Asset Intelligence com base num agendamento. Quando ativar o agendamento da sincronização, especifique um agendamento de sincronização simples ou personalizado. Durante a sincronização agendada, o ponto de sincronização do Asset Intelligence liga ao System Center Online para obter o catálogo do Asset Intelligence mais recente. Pode sincronizar manualmente o catálogo de Inteligência de Ativos a partir do nó de Inteligência de Ativos na consola do Gestor de Configuração. Para os passos para sincronizar manualmente o catálogo de Inteligência de Ativos, consulte a secção [de catálogo sincronizar manualmente a](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) secção de catálogo de Inteligência de Ativos nas [Operações de Inteligência](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)de Ativos .  

10. Concluir o assistente 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Quatro relatórios do Asset Intelligence apresentam informações recolhidas a partir de registos de eventos de Segurança do Windows em computadores cliente. Aqui está como configurar as definições de logon da política de segurança do computador para permitir a auditoria de eventos de logon de sucesso.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Para ativar o registo de eventos de início de sessão bem-sucedidos através de uma política de segurança local  

1.  Num computador cliente do Gestor de Configuração, escolha **Iniciar**  >  **Ferramentas Administrativas**  >  **Política de Segurança Local**.  

2.  Na caixa de diálogo política de **segurança local,** em Definições de **Segurança,** expandir **políticas locais,** e depois escolher política de **auditoria.**  

3.  No painel de resultados, clique duas vezes em eventos de **logon de auditoria,** certifique-se de que a caixa de verificação **de sucesso** é selecionada e, em seguida, escolha **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Para ativar o registo de eventos de início de sessão bem-sucedidos através de uma política de segurança do domínio do Active Directory  

1.  Num computador controlador de domínio, escolha **Iniciar**, apontar para **ferramentas administrativas,** e depois escolher a Política de **Segurança do Domínio**.  

2.  Na caixa de diálogo política de **segurança local,** em Definições de **Segurança,** expandir **políticas locais,** e depois escolher política de **auditoria.**  

3.  No painel de resultados, clique duas vezes em eventos de **logon de auditoria,** certifique-se de que a caixa de verificação **de sucesso** é selecionada e, em seguida, escolha **OK**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 As seguintes secções descrevem os procedimentos necessários para importar informações de licenciamento de software da Microsoft e de software geral para a base de dados do site Do Gestor de Configuração utilizando o Assistente de Licença de Software de Importação. Ao importar informações de licenças de software para a base de dados do site a partir de ficheiros de declaração de licença, a conta do computador do servidor de site requer permissões de **Controlo Total** do sistema de ficheiros NTFS para a partilha de ficheiros utilizada para importar informações de licença de software.  

> [!IMPORTANT]  
>  Quando as informações de licença de software são importadas para a base de dados do site, as informações de licença de software existentes são substituídas. Certifique-se de que o ficheiro de informações de licença de software que utiliza com o Assistente Importar Licenças de Software contém uma lista completa de todas as informações de licença de software necessárias.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Para importar informações de licença de software para o catálogo do Asset Intelligence  

1.  No espaço de trabalho **de Ativo e Compliance,** escolha A Inteligência de **Ativos.**  

2.  No separador **Home,** no grupo Deinteligência de **Ativos,** escolha **Licenças**de Software de Importação .   

4.  Na página **Importar** , especifique se está a importar um ficheiro de Licenciamento em Volume da Microsoft (MVLS) (.xml ou .csv) ou um ficheiro de Declaração de Licença Geral (.csv). Para obter mais informações sobre a criação de um ficheiro de Declaração de Licença Geral, consulte [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) mais à frente neste tópico.  

    > [!WARNING]  
    >  Para transferir um ficheiro MVLS no formato .csv, que pode importar para o catálogo do Asset Intelligence, consulte [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Para aceder a estas informações, tem de ter uma conta registada no site. Tem de contactar o seu representante de conta Microsoft para obter informações sobre como obter o seu ficheiro MVLS no formato .xml.  

5.  Introduza o caminho unC para o ficheiro de declaração de licença ou escolha **Navegar** para selecionar uma pasta e ficheiro partilhados por rede.  

    > [!NOTE]  
    >  A pasta partilhada deve estar corretamente protegida para impedir o acesso não autorizado ao ficheiro de informações de licenciamento e a conta de computador do computador no qual o assistente está a ser executado tem de ter permissões de Controlo Total para a partilha que contém o ficheiro de importação de licença.  

6. Conclua o assistente.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Também é possível importar uma declaração de licença geral para o catálogo do Asset Intelligence, utilizando um ficheiro de importação de licença criado manualmente no formato de ficheiro delimitado por vírgulas (.csv).  

> [!NOTE]  
>  Embora apenas os campos **Nome**, **Fabricante**, **Versão**, e **QuantidadeEfetiva** tenham de conter dados, todos os campos têm de ser introduzidos na primeira linha do ficheiro de importação de licença. Todos os campos de data devem ser apresentados no seguinte formato: Mês/Dia/Ano, por exemplo, 08/04/2008.  

O Asset Intelligence faz corresponder os produtos que especificar na declaração de licença geral, utilizando o nome do produto e a versão do produto, mas não o nome do fabricante. Tem de utilizar um nome de produto na declaração de licença geral que seja uma correspondência exata com o nome de produto armazenado na base de dados do site. A Asset Intelligence pega no número **de Quantidade Efetiva** dado na declaração geral de licença e compara o número com o número de produtos instalados encontrados no inventário do Gestor de Configuração.  

> [!TIP]  
>  Para obter uma lista completa dos nomes do produto armazenados na base de dados do Site Do Gestor de Configuração, pode executar a seguinte consulta na base de dados do site: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Pode especificar as versões exatas de um produto ou especificar parte da versão, como, por exemplo, apenas a versão principal. Os exemplos seguintes fornecem as correspondências de versão resultantes para uma entrada de versão de declaração de licença geral para um produto específico.  

|Entrada de declaração de licença geral|Entradas da base de dados do site correspondentes|  
|-------------------------------------|------------------------------------|  
|Nome: "MySoftware", ProductVersion0:"2"|Nome do produto: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> Nome do produto0: "MySoftware", Versão0 do produto: "2.02.5678"<br /><br /> Nome do produto0: "MySoftware", Versão 0: "2.05.1234"<br /><br /> Nome do produto0: "MySoftware", Versão0 do produto: "2.05.5678"<br /><br /> Nome do produto: "MySoftware", Versão0 do produto: "2.05.3579.000"<br /><br /> Nome do produto0: "MySoftware", Versão 0 de produto: "2.10.1234"|  
|Nome: "MySoftware", Versão "2.05"|Nome do produto0: "MySoftware", Versão 0: "2.05.1234"<br /><br /> Nome do produto0: "MySoftware", Versão0 do produto: "2.05.5678"<br /><br /> Nome do produto: "MySoftware", Versão0 do produto: "2.05.3579.000"|  
|Nome: "Mysoftware", Versão "2"<br /><br /> Nome: "Mysoftware", Versão "2.05"|Erro durante a importação. A importação falha quando mais do que uma entrada corresponde à mesma versão de produto.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Para criar um ficheiro de importação de declaração de licença geral utilizando o Microsoft Excel  

1.  Abra o Microsoft Excel e crie uma nova folha de cálculo.  

2.  Na primeira linha da nova folha de cálculo, introduza todos os nomes de campos de dados de licença de software.  

3.  Na segunda e subsequentes linhas da nova folha de cálculo, introduza as informações de licença de software conforme necessário. Certifique-se de que, pelo menos, todos os campos de dados de licença de software necessários são introduzidos nas linhas subsequentes para cada licença de software a importar. O nome do título de software introduzido na folha de cálculo tem de ser igual ao título de software que é apresentado no Explorador de Recursos para um computador cliente após a execução do inventário de hardware.  

4.  Guarde o ficheiro em formato .csv.  

5.  Copie o ficheiro .csv para a partilha de ficheiros que é utilizada para importar informações de licença de software para o catálogo do Asset Intelligence.  

6.  Na consola 'Gestor de Configuração', utilize o Assistente de Licença de Software de Importação para importar o ficheiro .csv recém-criado.  

7.  Executar a Licença de Inteligência de Ativos **15A - Relatório** de Reconciliação de Software de Terceiros para verificar se a informação de licenciamento foi importada com sucesso para o catálogo de Inteligência de Ativos.  

> [!NOTE]  
>  Para um exemplo de um ficheiro geral de licença de software que pode usar para fins de teste, consulte [o arquivo de importação de licença geral da Asset Intelligence](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabela de exemplo para descrever as licenças de software  
 Ao criar um ficheiro de importação de declaração de licença geral, as informações na tabela seguinte podem ser utilizadas para descrever as licenças de software a importar para o catálogo do Asset Intelligence.  

|Nome da coluna|Tipo de dados|Necessário|Exemplo|  
|-----------------|---------------|--------------|-------------|  
|Name|Até 255 carateres|Sim|Título de software|  
|Publisher|Até 255 carateres|Sim|Fabricante de software|  
|Versão|Até 255 carateres|Sim|Versão do título de software|  
|Linguagem|Até 255 carateres|Sim|Idioma do título de software|  
|QuantidadeEfetiva|Valor inteiro|Sim|Número de licenças adquiridas|  
|NúmeroDePO|Até 255 carateres|Não|Informações de nota de encomenda|  
|NomeDoRevendedor|Até 255 carateres|Não|Informações do revendedor|  
|DataDeCompra|Valor de data no seguinte formato: MM/DD/AAAA|Não|Data de compra da licença|  
|SuporteAdquirido|Valor de bits|Não|0 ou 1: introduza 0 para Sim ou 1 para Não|  
|DataDeExpiraçãoDoSuporte|Valor de data no seguinte formato: MM/DD/AAAA|Não|Data de fim do suporte adquirido|  
|Comentários|Até 255 carateres|Não|Comentários opcionais|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 As seguintes tarefas de manutenção estão disponíveis para o Asset Intelligence:  

-   Consulte o Título da **Aplicação com Informações**de Inventário : Verifica que o título de software que é relatado no inventário de software é reconciliado com o título de software no catálogo de Inteligência de Ativos. Por defeito, esta tarefa está ativada e está programada para ser executada no sábado depois das 00h00. e antes das 5:00 da manhã. Esta tarefa de manutenção só está disponível no site de alto nível na hierarquia do Gestor de Configuração.  

-   Resumo Dados de **Software Instalados**: Fornece as informações que são exibidas no espaço de trabalho **De Ativos e Compliance,** no nó de **Software Inventariado,** sob o nó de Inteligência de **Ativos.** Quando a tarefa corre, o Gestor de Configuração reúne uma contagem para todos os títulos de software inventariados no site principal. Por defeito, esta tarefa está ativada e programada para ser executada todos os dias depois das 00:00. e antes das 5:00 da manhã. Esta tarefa de manutenção está disponível apenas em locais primários.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Para configurar tarefas de manutenção do Asset Intelligence  

1.  Na consola de Gestor de Configuração, escolha sites de configuração do site **da administração**  >  **Site Configuration**  >  **Sites**.  

3.  Selecione o site no qual pretende configurar a tarefa de manutenção do Asset Intelligence.  

4.  No separador **Casa,** no grupo **Definições,** escolha manutenção do **site**. Selecione uma tarefa e escolha **editar** para modificar as definições. 

    Recomendamos que estabeleça o período de tempo para as horas fora do pico do site. O período de tempo corresponde ao intervalo de tempo em que a tarefa pode ser executada. É definido pelos campos **Iniciar após** e **Última hora de início** especificados na caixa de diálogo **Propriedades da Tarefa** .  

    Pode iniciar a tarefa de imediato, selecionando o dia atual e definindo a hora em **Iniciar após** para alguns minutos após a hora presente.  

7.  Escolha **OK** para guardar as suas definições. A tarefa é agora executada de acordo com o respetivo agendamento.  

    > [!NOTE]  
    >  Se uma tarefa não funcionar na primeira tentativa, o Gestor de Configuração tenta reexecutar a tarefa até que a tarefa seja executada com sucesso ou até ao período de tempo em que a tarefa pode ser executada.  
