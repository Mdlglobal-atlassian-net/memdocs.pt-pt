---
title: Instalador hotfix
titleSuffix: Configuration Manager
description: Descubra quando e como instalar atualizações através do Instalador Hotfix para O Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9389f407f8bdbafd057770ff63ed9b139e6600b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720710"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Utilize o Instalador Hotfix para instalar atualizações para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Algumas atualizações para O Gestor de Configuração não estão disponíveis no serviço de cloud da Microsoft e são obtidas apenas fora da banda. Um exemplo é uma correção de versão limitada para resolver um problema específico.   
Quando tiver de instalar uma atualização (ou 'hotfix' que recebe da Microsoft, e essa atualização tem um nome de ficheiro que termina com a extensão **.exe** (not **update.exe),** utiliza o instalador hotfix que está incluído com esse 'hotfix' para instalar a atualização diretamente no servidor do site do 'Gestor de Configuração'.  

Se o ficheiro hotfix tiver a extensão do ficheiro **.update.exe,** consulte [Utilize a Ferramenta de Registo de Atualização para importar hotfixes para o Gestor](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)de Configuração .  

> [!NOTE]  
> Este tópico fornece orientações gerais sobre como instalar hotfixes que atualizam o Gestor de Configuração. Para obter detalhes sobre uma atualização específica, consulte o artigo correspondente na Base de Dados de Conhecimento (KB), no Suporte da Microsoft.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a>Visão geral dos hotfixes para O Gestor de Configuração  
Os hotfixes para o Gestor de Configuração são semelhantes aos de outros produtos da Microsoft, como o SQL Server, contêm uma correção individual ou um pacote (um rollup de correções), e são descritos num artigo da Microsoft Knowledge Base.  

As atualizações individuais incluem uma única atualização focada para uma versão específica do Gestor de Configuração.  
Os pacotes de atualizações incluem múltiplas atualizações para uma versão específica do Gestor de Configuração.  
Quando uma atualização é um pacote, não é possível instalar atualizações individuais a partir desse pacote.  

Se planear criar implementações para instalar atualizações em computadores adicionais, terá de instalar o pacote de atualização num servidor do site de administração central ou num servidor do site primário.  

Quando executa o pacote de atualização, ocorrerá o seguinte:  

- Extrai os ficheiros de atualização para cada componente aplicável a partir do pacote de atualização.  

- Inicia um assistente que o orienta ao longo de um processo para configurar as atualizações e opções de implementação para as atualizações.  

- Depois de concluir o assistente, as atualizações do pacote aplicáveis ao servidor do site são instaladas no mesmo.  

O assistente cria também implementações que poderá utilizar para instalar as atualizações em computadores adicionais. O utilizador implementa as atualizações em computadores adicionais ao utilizar um método de implementação suportado, como um pacote de implementação de software ou o Microsoft System Center Updates Publisher 2011.  

Quando o assistente é executado, é criado um ficheiro **.cab** no servidor do site para ser utilizado com o Updates Publisher 2011. Opcionalmente, pode configurar o assistente para também criar um ou mais pacotes para a implementação de software. Pode utilizar estas implementações para instalar atualizações em componentes, como clientes ou a consola 'Gestor de Configuração'. Também pode instalar atualizações manualmente em computadores que não executam o cliente do Gestor de Configuração.  

Os seguintes três grupos no Gestor de Configuração podem ser atualizados:  

- Funções de servidor do Gestor de Configuração, que incluem:  

  - Site de administração central  

  - Site primário  

  - Site Secundário  

  - Fornecedor de SMS Remoto  

- Consola do Configuration Manager  

- Cliente do Gestor de Configuração  

> [!NOTE]  
> **As atualizações para as funções** do sistema do site (incluindo atualizações para a base de dados do site e pontos de distribuição baseados na nuvem) são instaladas como parte da atualização para servidores e serviços do site pelo gestor de componentes do site.  
>   
> No entanto, as atualizações são servida pelo gestor de distribuição em vez do gestor de componentes do site.  

Cada pacote de atualização para O Gestor de Configuração é um ficheiro .exe auto-extraível (SFX) que contém os ficheiros necessários para instalar a atualização nos componentes aplicáveis do Gestor de Configuração. Normalmente, o ficheiro SFX pode conter os seguintes ficheiros:  

|Ficheiro|Detalhes|  
|----------|-------------|  
|&lt;Versão\>do produto -QFE-KB\>-&lt;\>-&lt;KB idioma da plataforma id\>do artigo KB&lt;.exe|Este é o ficheiro de atualização. A linha de comandos para este ficheiro é gerida por Updatesetup.exe.<br /><br /> Por exemplo:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Este invólucro .msi gere a instalação do pacote de atualização.<br /><br /> Ao executar a atualização, o Updatesetup.exe deteta o idioma de apresentação do computador em que é executado. Por predefinição, a interface de utilizador da atualização encontra-se em inglês. No entanto, quando o idioma de apresentação é suportado, a interface de utilizador é apresentada no idioma local do computador.|  
|License_&lt;idioma\>.rtf|Quando aplicável, cada atualização contém um ou mais ficheiros de licença para os idiomas suportados.|  
|&lt;Produto&updatetype&lt;>- versão\>-&lt;\>-&lt;produto KB artigo ID plataforma\>.msp|Quando a atualização se aplica à consola ou clientes do Gestor de Configuração, o pacote de atualização inclui ficheiros separados do Patch (.msp) do Instalador do Windows.<br /><br /> Por exemplo:<br /><br /> **Atualização da consola do Configuration Manager:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Atualização do cliente:** ConfigMgr1511-cliente-KB1234567-i386.msp<br />ConfigMgr1511-cliente-KB1234567-x64.msp|  

Por predefinição, o pacote de atualização regista as ações num ficheiro .log no servidor do site. O ficheiro de registo tem o mesmo nome que o pacote de atualização e é escrito na pasta **%SystemRoot%/Temp** .  

Quando executa o pacote de atualização, é extraído um ficheiro para uma pasta temporária com o mesmo nome que o pacote de atualização e, em seguida, Updatesetup.exe é executado. Updatesetup.exe inicia a atualização &lt;de\> &lt;software\> para a versão do produto KB Number Wizard do Gestor de Configuração.  

Conforme aplicável ao âmbito da atualização, o assistente cria uma série de pastas sob a pasta de instalação do Gestor de Configuração no servidor do site. A estrutura de pastas é semelhante à seguinte:   
**&lt;\>\\&lt;\>\\&lt;\\&lt;\>Nome\>do servidor \SMS_ Código do Site\>\Hotfix KB Plataforma de atualização de números . \\ \\ &lt;**  

A tabela seguinte fornece detalhes sobre as pastas na estrutura de pastas:  

|Nome da pasta|Mais informações|  
|-----------------|----------------------|  
|&lt;Nome do servidor\>|Este é o nome do servidor do site em que executou o pacote de atualização.|  
|Código&lt;do Site SMS_\>|Este é o nome de partilha da pasta de instalação do Gestor de Configuração.|  
|&lt;Número da BDC\>|Este é o número de ID do artigo da Base de Dados de Conhecimento relativo a este pacote de atualização.|  
|&lt;Tipo de atualização\>|Estes são os tipos de atualizações para O Gestor de Configuração. O assistente cria uma pasta separada para cada tipo de atualização contido no pacote de atualização. Os nomes das pastas representam os tipos de atualização. Incluem o seguinte:<br /><br /> **Servidor**: Inclui atualizações para servidores de site, servidores de base de dados de sites e computadores que executam o Fornecedor SMS.<br /><br /> **Cliente**: Inclui atualizações para o cliente do Gestor de Configuração.<br /><br /> **AdminConsole**: Inclui atualizações para a consola de Configuração Manager<br /><br /> Além dos tipos de atualização anteriores, o assistente cria uma pasta chamada **SCUP**. Esta pasta não representa um tipo de atualização. Em vez disso, contém o ficheiro .cab para o Updates Publisher.|  
|&lt;Plataforma\>|Esta é uma pasta específica da plataforma. Contém os ficheiros de atualização específicos de um tipo de processador.  Estas pastas incluem:<br /><br />- x64<br /><br /> - I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Como instalar atualizações  
Para instalar atualizações, terá primeiro de instalar o pacote de atualização num servidor do site. Ao instalar um pacote de atualizações, este inicia um assistente de instalação para essa atualização. Este assistente faz o seguinte:  

- Extrai os ficheiros de atualização  

- Ajuda-o a configurar as implementações  

- Instala as atualizações aplicáveis nos componentes de servidor do computador local  

Depois de instalar o pacote de atualização num servidor de site, poderá então atualizar componentes adicionais para o 'Gestor de Configuração'. A tabela seguinte descreve as ações de atualização destes diversos componentes:  

|Componente|Instruções|  
|---------------|------------------|  
|Servidor do site|Implementar as atualizações num servidor de site remoto quando não optar por instalar o pacote de atualização diretamente nesse servidor de site remoto.|  
|Base de dados do site|Em servidores de site remotos, implemente as atualizações do servidor que incluam uma atualização da base de dados do site se não instalar o pacote de atualização diretamente nesse servidor de site remoto.|  
|Consola do Configuration Manager|Após a instalação inicial da consola 'Gestor de Configuração', pode instalar atualizações para a consola 'Gestor de Configuração' em cada computador que executa a consola. Não é possível modificar os ficheiros de instalação da consola Do Gestor de Configuração para aplicar as atualizações durante a instalação inicial da consola.|  
|Fornecedor de SMS Remoto|Instale atualizações para cada instância do Fornecedor de SMS que seja executada num computador que não o servidor do site onde instalou o pacote de atualização.|  
|Clientes do Gestor de Configuração|Após a instalação inicial do cliente do Gestor de Configuração, pode instalar atualizações para o cliente do Gestor de Configuração em cada computador que executa o cliente.|  

> [!NOTE]  
> Só pode implementar atualizações para computadores que executam o cliente do Gestor de Configuração.  

Se reinstalar um cliente, uma consola de Gestor de Configuração ou fornecedor de SMS, também deve reinstalar as atualizações para estes componentes.  

Utilize as informações nas seguintes secções para instalar atualizações em cada um dos componentes para O Gestor de Configuração.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Atualizar servidores  
As atualizações de servidores podem incluir atualizações de **sites**, da **site database**e de computadores que executem uma instância do **Fornecedor de SMS**:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a>Atualizar um site  
Para atualizar um site do Gestor de Configuração, pode instalar o pacote de atualização diretamente no servidor do site, ou pode implementar as atualizações para um servidor de site depois de instalar o pacote de atualização num site diferente.  

Ao instalar uma atualização num servidor de site, o processo de instalação da atualização gere as ações adicionais necessárias para aplicar a atualização, tais como atualizar as funções do sistema de sites. A exceção a este procedimento é a base de dados do site. A secção seguinte contém informações sobre como atualizar a base de dados do site.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a>Atualizar uma base de dados do site  
Para atualizar a base de dados do site, o processo de instalação executa um ficheiro chamado **update.sql** na base de dados do site. Poderá configurar o processo de atualização para atualizar automaticamente a base de dados do site ou optar por atualizar manualmente a base de dados do site, mais tarde.  

**Atualização Automática da Base de Dados do Site**  

Quando instalar o pacote de atualização num servidor de site, pode optar por atualizar automaticamente a base de dados do site quando a atualização do servidor estiver instalada. Esta decisão aplica-se apenas ao servidor do site onde instala o pacote de atualizações e não se aplica às implementações criadas para instalar as atualizações nos servidores do site remoto.  

> [!NOTE]  
> Quando opta por atualizar automaticamente a base de dados do site, o processo atualiza uma base de dados independentemente de a base de dados estar localizada no servidor do site ou num computador remoto.  

> [!IMPORTANT]  
> Antes de atualizar a base de dados do site, crie uma cópia de segurança da base de dados do site. Não é possível desinstalar uma atualização da base de dados do site. Para obter informações sobre como criar uma cópia de segurança para O Gestor de Configuração, consulte [backup e recuperação para 'Gestor](backup-and-recovery.md)de Configuração'.  

**Atualização Manual da Base de Dados do Site**  

Se optar por não atualizar automaticamente a base de dados do site quando instalar o pacote de atualização no servidor do servidor do site, a atualização do servidor não modifica a base de dados do servidor do site onde o pacote de atualização é executado. No entanto, as implementações que utilizam o pacote que é criado para a implementação de software ou que instala atualizam sempre a base de dados do site.  

> [!WARNING]  
> Quando a atualização inclui atualizações tanto para o servidor do site como para a base de dados do site, a atualização não está funcional até que a atualização esteja concluída tanto para o servidor do site como para a base de dados do site. Até que a atualização seja aplicada na base de dados do site, o site encontra-se em estado não apoiado.  

**Para atualizar manualmente uma base de dados do site:**  

1.  No servidor do site pare o serviço de SMS_SITE_COMPONENT_MANAGER e, em seguida, pare o serviço SMS_EXECUTIVE.  

2.  Feche a consola do Gestor de Configuração.  

3.  Execute o script de atualização nomeado **update.sql** na base de dados do site. Para obter informações sobre como executar um script para atualizar uma base de dados do SQL Server, consulte a documentação para a versão do Servidor SQL que utiliza para o servidor de base de dados do seu site.  

4.  Reinício dos serviços que foram interrompidos em etapas anteriores.  

5.  Quando o pacote de atualização se instala, extrai **atualização.sql** para a seguinte localização no servidor do site: ** \\ \\ &lt;\>Nome do&lt;servidor \SMS_ Código\>do Site \Hotfix\\&lt;Número\>KB \update.sql**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a>Atualizar um computador que executa o Provedor de SMS  
Depois de instalar um pacote de atualização que inclui atualizações para o Fornecedor SMS, tem de implementar a atualização para cada computador que executa o Fornecedor SMS. A única exceção é a instância do Fornecedor de SMS instalada anteriormente no servidor do site onde instalou o pacote de atualizações. A instância local do Fornecedor SMS no servidor do site é atualizada quando instala o pacote de atualização.  

Se remover e, em seguida, reinstalar o Fornecedor SMS num computador, terá de reinstalar a atualização para o Fornecedor SMS nesse computador.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a>Atualizar clientes  
Quando instala uma atualização que inclui atualizações para o cliente do Gestor de Configuração, é-lhe apresentada a opção de atualizar automaticamente os clientes com a instalação da atualização ou atualizar manualmente os clientes mais tarde. Para obter mais informações sobre a atualização automática de clientes, veja [Como atualizar clientes em computadores Windows](https://technet.microsoft.com/library/mt627885.aspx).  

Pode implementar atualizações com o Updates Publisher ou um pacote de implementação de software, ou pode optar por instalar manualmente a atualização em cada cliente. Para obter mais informações sobre como utilizar implementações para instalar atualizações, veja a secção [Implementar atualizações para o Configuration Manager](#BKMK_Deploy) deste tópico.  

> [!IMPORTANT]  
> Quando instalar atualizações para clientes e o pacote de atualizações inclui atualizações para servidores, certifique-se de que também instala as atualizações do servidor no site principal para o qual os clientes são atribuídos.  

Para instalar manualmente a atualização do cliente, em cada cliente do Gestor de Configuração, deve executar **msiexec.exe** e fazer referência à atualização específica do cliente .msp.  

Por exemplo, pode utilizar a seguinte linha de comando para uma atualização do cliente. Esta linha de comando executa mSIEXEC no computador cliente e refere o ficheiro .msp que o pacote de atualização extraído no servidor do site: **msiexec.exe \\ \\ &lt;/p ServerName\>\SMS_&lt;SiteCode\>\Hotfix KB Number \Hotfix\\&lt;\>\\&lt;\>\\&lt;\> Platform msp /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a>Consolas de Gestor de Configuração de Atualização  
Para atualizar uma consola do Gestor de Configuração, tem de instalar a atualização no computador que executa a consola após a instalação da consola estar terminada.  

> [!IMPORTANT]  
> Quando instalar atualizações para a consola 'Gestor de Configuração', e o pacote de atualizações inclui atualizações para servidores, certifique-se de que também instala as atualizações do servidor no site que utiliza com a consola 'Gestor de Configuração'.  

Se o computador que atualiza for executado o cliente do Gestor de Configuração:  

- Pode utilizar uma implementação para instalar a atualização. Para obter mais informações sobre como utilizar implementações para instalar atualizações, veja a secção [Implementar atualizações para o Configuration Manager](#BKMK_Deploy) deste tópico.  

- Se tiver iniciado sessão diretamente no computador cliente, pode executar a instalação interativamente.  

- Pode instalar manualmente a atualização em cada computador. Para instalar manualmente a atualização da consola do Gestor de Configuração, em cada computador que executa a consola Do Gestor de Configuração, pode executar msiexec.exe e fazer referência à atualização da consola do Gestor de Configuração .msp.  

Por exemplo, pode utilizar a seguinte linha de comando para atualizar uma consola do Gestor de Configuração. Esta linha de comando executa mSIEXEC no computador e refere o ficheiro .msp que o pacote de atualização extraído no servidor do site: **msiexec.exe /p \\ \\ &lt;ServerName\>\SMS_&lt;\>SiteCode \Hotfix\\&lt;KB Number\>\AdminConsole\\&lt;Platform\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Implementar atualizações para o Configuration Manager  
Depois de instalar o pacote de atualização num servidor de site, pode utilizar um dos três métodos seguintes para implementar atualizações para computadores adicionais.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a>Utilizar atualizações Publisher 2011 para instalar atualizações  
Quando instala o pacote de atualização num servidor de site, o Assistente de instalação cria um ficheiro de catálogo para Atualizações editora que pode utilizar para implementar as atualizações para computadores aplicáveis. O assistente cria sempre este catálogo, mesmo quando o utilizador seleciona a opção **Utilizar pacote e programa para implementar esta atualização**.  

O catálogo de Atualizações Editor chama-se **SCUPCatalog.cab** e pode ser encontrado no seguinte local no computador onde o pacote de atualização é executado: ** \\ \\ &lt;ServerName\>\SMS_&lt;\>SiteCode \Hotfix\\&lt;KB Number\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Uma vez que o ficheiro SCUPCatalog.cab é criado utilizando caminhos específicos para o servidor do site onde o pacote de atualização está instalado, não pode ser utilizado em outros servidores do site.  

Depois de o assistente estar terminado, pode importar o catálogo para updates Publisher e, em seguida, utilizar atualizações de software Do Gestor de Configuração para implementar as atualizações. Para obter informações sobre updates Publisher, consulte [Updates Publisher 2011](https://go.microsoft.com/fwlink/p/?LinkID=83449) na biblioteca TechNet para System Center 2012.  

Utilize o seguinte procedimento para importar o ficheiro SCUPCatalog.cab para atualizar o Editor e publicar as atualizações.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Para importar as atualizações para updates Publisher 2011  

1.  Inicie a consola Updates Publisher e clique **em Importar**.  

2.  Na página **do Tipo de Importação** do Assistente de Catálogo de Atualizações de Software de Importação, selecione Especificar o caminho para o catálogo a **importar**e, em seguida, especificar o ficheiro SCUPCatalog.cab.  

3.  Clique **em Seguinte**, e depois clique em **Seguinte** novamente.  

4.  Na caixa de diálogo **de validação** de catálogo , clique em **Aceitar**. Feche o assistente depois de terminado.  

5.  Na consola Updates Publisher, selecione a atualização que pretende implementar e, em seguida, clique em **Publicar**.  

6.  Na página **De publicar Opções** do Assistente de Atualizações de Software, selecione **Conteúdo Completo**, e clique em **Seguinte**.  

7.  Complete o assistente para publicar as atualizações.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a>Utilize a implementação de software para instalar atualizações  
Quando instalar o pacote de atualização no servidor do site principal ou no site da administração central, pode configurar o Assistente de instalação para criar pacotes de atualização para implementação de software. Em seguida, pode implantar cada pacote numa coleção de computadores que pretende atualizar.  

Para criar um pacote de implementação de software, na página de Implementação de Atualização de **Software Configure** do assistente, selecione a caixa de verificação para cada tipo de pacote de atualização que pretende atualizar. Os tipos disponíveis podem incluir servidores, consolas de Configuração Manager e clientes. É criado um pacote separado para cada tipo de atualização que seleciona.  

> [!NOTE]  
> O pacote para servidores contém atualizações para os seguintes componentes:  
>   
> - Servidor do site  
> - Fornecedor de SMS  
> - Base de dados do site  

Em seguida, na página **Configurar Método de Implementação de Atualização do Software** do assistente, selecione a opção **Utilizarei a distribuição de software**. Esta seleção direciona o assistente para criar os pacotes de implementação de software.  

Depois de o assistente estar terminado, pode ver os pacotes que cria na consola Do Gestor de Configuração no nó de **Pacotes** no espaço de trabalho da Biblioteca de **Software.** Em seguida, pode utilizar o seu processo padrão para implementar pacotes de software para clientes do Gestor de Configuração. Quando um pacote é executado em um cliente, instala as atualizações para os componentes aplicáveis do Gestor de Configuração no computador cliente.  

Para obter informações sobre como implementar pacotes para clientes do Gestor de Configuração, consulte [Pacotes e programas.](../../../apps/deploy-use/packages-and-programs.md)  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a>Criar coleções para implementar atualizações para O Gestor de Configuração  
Pode implementar atualizações específicas para clientes aplicáveis. As seguintes informações podem ajudá-lo a criar coleções de dispositivos para os diferentes componentes para O Gestor de Configuração.  

|Componente do Gestor de Configuração|Instruções|  
|----------------------------------------|------------------|  
|Servidor do site de administração central|Crie uma consulta de associação direta e adicione o computador do servidor do site de administração central.|  
|Todos os servidores primários do site|Crie uma consulta de associação direta e adicione cada computador do servidor do site primário.|  
|Todos os servidores do site secundário|Crie uma consulta de associação direta e adicione cada computador do servidor do site secundário.|  
|Todos os clientes x86|Criar uma coleção com os seguintes critérios de consulta:<br /><br /> **Selecione \* a partir de SMS_R_System interior junte SMS_G_System_SYSTEM na SMS_G_System_SYSTEM. ResourceID = SMS_R_System.ResourceId onde SMS_G_System_SYSTEM. SystemType = "Pc baseado em X86"**|  
|Todos os clientes x64|Criar uma coleção com os seguintes critérios de consulta:<br /><br /> **Selecione \* a partir de SMS_R_System interior junte SMS_G_System_SYSTEM na SMS_G_System_SYSTEM. ResourceID = SMS_R_System.ResourceId onde SMS_G_System_SYSTEM. SystemType = "Pc baseado em X64"**|  
|Todos os computadores que executam a consola Do Gestor de Configuração|Crie uma consulta de associação direta e adicione cada computador.|  
|Computadores remotos que executam uma instância do Fornecedor de SMS|Crie uma consulta de associação direta e adicione cada computador.|  

> [!NOTE]  
> Para atualizar uma base de dados do site, implemente a atualização no servidor deste site.  

Para obter informações sobre como criar coleções, consulte [Como criar coleções.](../../../core/clients/manage/collections/create-collections.md)  
