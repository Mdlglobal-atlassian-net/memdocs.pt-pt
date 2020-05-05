---
title: Pré-visualização técnica 1706
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1706 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d554f4f6e0c68912f4fac91bc1a8db2807b26a04
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078792"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1706 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1706. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**

- **Ponto de distribuição de movimento** - As opções na consola para mover um ponto de distribuição entre os sites não podem ser utilizadas com esta versão devido ao limite de pré-visualização técnica de um único local primário.

- **Definições de conformidade** do dispositivo - Pode experimentar comportamentos opostos ao utilizar as duas definições de conformidade do novo dispositivo:
  - **Bloquear a depuração USB no dispositivo**
  - **Bloquear aplicativos de fontes desconhecidas**

    Por exemplo, se os administradores configurarem a **depuração USB do bloco no dispositivo** como **verdadeiramente**, todos os dispositivos que não tenham depuração USB ativado são marcados como não conformes.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Melhores grupos de fronteira para pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui melhorias na forma como os pontos de atualização de software funcionam com grupos de fronteira. O seguinte resume o novo comportamento de recuo:
- O recuo para pontos de atualização de software usa agora um tempo configurável para o recuo para os grupos de fronteira dos vizinhos, com um tempo mínimo de 120 minutos.

- Independentemente da configuração de recuo, um cliente tenta alcançar o último ponto de atualização de software que utilizou durante 120 minutos. Depois de não ter chegado ao servidor durante 120 minutos, o cliente verifica então o seu conjunto de pontos de atualização de software disponíveis, para que possa encontrar um novo.

  - Todos os pontos de atualização de software do atual grupo de fronteira do cliente são adicionados à piscina do cliente imediatamente.

  - Como um cliente tenta usar o seu servidor original durante 120 minutos antes de procurar um novo, nenhum servidor adicional é contactado até que decorridos duas horas.

  - Se o recuo para um grupo vizinho estiver configurado durante o mínimo de 120 minutos, os pontos de atualização de software desse grupo de fronteira vizinhos farão parte do conjunto de servidores disponíveis do cliente.

- Depois de não ter atingido o seu servidor original durante duas horas, o cliente muda para um ciclo mais curto para contactar um novo ponto de atualização de software.

  Isto significa que se um cliente não se ligar a um novo servidor, ele rapidamente seleciona o próximo servidor a partir do seu conjunto de servidores disponíveis e tenta contactar esse.

  - Este ciclo continua até que o cliente se ligue a um ponto de atualização de software que pode utilizar.
  - Até que o cliente encontre um ponto de atualização de software, servidores adicionais são adicionados ao conjunto de servidores disponíveis quando o tempo de recuo para cada grupo de fronteira do vizinho é cumprido.

Para mais informações, consulte pontos de [atualização](../servers/deploy/configure/boundary-groups.md#software-update-points) de software no tópico dos Grupos de Fronteira para a Divisão Atual.


## <a name="site-server-role-high-availability"></a>Função do servidor do site alta disponibilidade
<!-- 1128774 -->
A alta disponibilidade para a função do servidor do site é uma solução baseada em Configuração manager para instalar um servidor de site primário adicional no modo *Passivo.* O servidor do site do modo passivo é além do servidor de site primário existente que se encontra no modo *Ative.* Um servidor de site de modo passivo está disponível para uso imediato, quando necessário.

Um servidor de site primário em modo passivo:
- Utiliza a mesma base de dados do site que o seu servidor de site ativo.
- Recebe uma cópia da biblioteca de conteúdos de servidores de servidores do site ativo, que é então mantida em sincronização.
- Não escreve dados para a base de dados do site desde que esteja em modo passivo.
- Não suporta a instalação ou remoção de funções opcionais do sistema do site desde que esteja em modo passivo.

Para tornar o servidor do site do modo passivo o servidor do site do modo ativo, promove-o manualmente. Isto muda o servidor do site ativo para ser o servidor passivo do site. As funções do sistema do site que estão disponíveis no servidor de modo ativo original permanecem disponíveis desde que esse computador esteja acessível. Apenas a função do servidor do site é trocada entre o modo ativo e passivo.

Para instalar um servidor de site de modo passivo, utiliza o Assistente do Servidor do **Sistema de Criar** o Sistema de Criação para configurar um novo servidor de site com um tipo de servidor de site **primário** e um modo de **passivo**. Em seguida, o assistente executa a Configuração do Gestor de Configuração no servidor especificado para instalar o novo servidor de site no modo passivo. Após a instalação estar concluída, o servidor do site do modo ativo mantém o servidor do site do modo passivo e a sua biblioteca de conteúdos em sincronização com alterações ou configurações que faz para o servidor do site ativo.

### <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
- Um único servidor de site em modo passivo é suportado em cada site primário.

- O servidor do site em modo passivo pode estar no local ou baseado em nuvem em Azure.

- Tanto o modo ativo como os servidores passivos do site devem estar no mesmo domínio.

- Tanto os servidores ativos do modo ativo como os servidores passivos do site devem utilizar a mesma base de dados do site, que deve ser remota dos computadores de cada servidor do site.

    - O Servidor SQL que acolhe a base de dados pode usar uma instância padrão, chamada exemplo, cluster SQL Server ou um Grupo De Disponibilidade Sempre On.

    - O servidor do site em modo passivo está configurado para usar a mesma base de dados do site que o servidor do site de modo ativo. No entanto, o servidor do site do modo passivo só utiliza essa base de dados depois de ser promovido ao modo ativo.

- O computador que executará o servidor do site do modo passivo:

    - Deve satisfazer os [pré-requisitos para a instalação](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site)de um local primário .

    - Instala utilizando ficheiros de origem que correspondam à versão do servidor do site do modo ativo.

    - Não pode ter uma função de sistema de site a partir de nenhum site antes de instalar o site de modo passivo.

- Os computadores de servidor de servidor de modo ativo e passivo podem executar diferentes sistemas operativos ou versões de pacote de serviço, desde que ambos permaneçam suportados pela sua versão de 'Configuração Manager'.

- A promoção do servidor do site do modo passivo para o servidor de modo ativo é manual. Não há falha automática.

- As funções do sistema do site só podem ser instaladas no servidor do site que se encontra em modo ativo.

    - Um servidor de site em modo ativo suporta todas as funções do sistema do site. Não é possível instalar as funções do sistema do site no servidor quando se encontra em modo passivo.

    - As funções do sistema do site que utilizam uma base de dados (como o ponto de reporte) devem ter essa base de dados num servidor que seja remota tanto do modo ativo como dos servidores do site do modo passivo.

    - O SMS_Provider não instala no servidor do site em modo passivo. Uma vez que tem de se ligar a uma SMS_Provider para que o site promova manualmente o servidor do site do modo passivo para o modo ativo, recomendamos [a instalação](../plan-design/hierarchy/plan-for-the-sms-provider.md) de pelo menos uma instância adicional do fornecedor num computador adicional.

**Edição conhecida:**   
Com esta versão, **o Status** para as seguintes condições aparece na consola como valores numéricos em vez de texto legível:
- 131071 – Falha na instalação do servidor do site
- 720895 – Falha na não instalação da função do servidor do site
- 851967 - Falha falhada

### <a name="add-a-site-server-in-passive-mode"></a>Adicione um servidor de site em modo passivo
1. Na consola vá aos**Sites** de**Configuração** > do Site **da Administração** > e inicie o Assistente de [Funções](../servers/deploy/configure/install-site-system-roles.md)do Sistema do Site Add . Também pode utilizar o Assistente do Servidor do Sistema de Criar O Sistema de **Criação**.

2. Na página **Geral,** especifique o servidor que irá alojar o servidor do site do modo passivo. O servidor que especifica não pode alojar quaisquer funções do sistema do site antes de instalar um servidor de site no modo passivo.

3. Na página de Seleção de Funções do **Sistema,** selecione apenas o **servidor do site primário no modo passivo**.

4. Para completar o assistente, deve fornecer as seguintes informações que são utilizadas para executar a Configuração e instalar a função do servidor do servidor do site no servidor especificado:
    - Opte por copiar ficheiros de instalação do servidor do site ativo para o novo servidor de site de modo passivo, ou especificar um caminho para uma localização que contenha o conteúdo do CD do servidor do servidor do site **ativo. Última** pasta.

    - Especifique o mesmo servidor de base de dados do site e nome de base de dados utilizado pelo servidor do site do modo ativo.

5. O Gestor de Configuração instala o servidor do site em modo passivo no servidor especificado.

Para um estado de instalação detalhado, vá aos**Locais**de**Configuração** > do Site **da Administração** > .
- O estado do servidor do site em modo passivo apresenta-se como **Instalação**.

- Selecione o servidor e, em seguida, clique no **Estado do Show** para abrir o Status de **Instalação do Servidor** do Site para obter informações mais detalhadas.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promover o servidor do site de modo passivo para o modo ativo
Quando pretende alterar o servidor do site do modo passivo para o modo ativo, fá-lo a partir do painel de **nós** nos**sites**de**configuração** > do site **da administração** > . Desde que possa aceder a uma instância do SMS_Provider, pode aceder ao site para fazer esta alteração.
1. No painel de **nós** da consola 'Gestor de Configuração', selecione o servidor do site em modo passivo e, em seguida, a partir da Fita, escolha **Promover para ativo**.

2. O **estado** simples para o servidor que está a promover exibe no painel de **nós** como **Promoção**.

3. Após a promoção estar concluída, a coluna **Status** mostra **OK** tanto para o novo servidor do site do modo *Ative* como para o novo servidor de site do modo *Passivo.*

4. Nos**Sites**de**Configuração** > do Site **da Administração,** > o nome do servidor principal do site apresenta agora o nome do novo servidor de site do modo *Ativo.*
Para obter um estado detalhado, vá ao Estado do Servidor do**Site** **de Monitorização** > .
    - A coluna **Modo** identifica qual *o* servidor ativo ou *passivo*.

    - Ao promover um servidor do modo passivo para o modo ativo, selecione o servidor do site que está a promover para ativo e, em seguida, escolha o Estado do **Espetáculo** a partir da fita. Isto abre a janela de Estado de **Promoção** do Servidor do Site que apresenta detalhes adicionais sobre o processo.

Quando um servidor de site em modo ativo muda para o modo passivo, apenas a função do sistema do site é tornada passiva. Todas as outras funções do sistema do site que estão instaladas nesse computador permanecem ativas e acessíveis aos clientes.


### <a name="daily-monitoring"></a>Monitorização diária
Quando tiver um site primário em modo passivo, monitorize-o diariamente para garantir que permanece sincronizado com o servidor do site do modo ativo e pronto a ser utilizado. Para isso, vá ao Estado do Servidor do**Site** **de Monitorização** > . Aqui pode ver tanto o modo ativo como os servidores do site do modo passivo.

O separador **Resumo:**
- A coluna **Modo** identifica qual o servidor ativo ou passivo.
- A coluna **'Status'** lista **OK** quando o servidor de modo passivo está sincronizado com o servidor de modo ativo.
- Para ver detalhes adicionais sobre o estado de sincronização de conteúdo, clique no **estado do Show** a partir do Estado de Sincronização de Conteúdo. Isto abre o separador Content Library onde pode tentar corrigir problemas de sincronização de conteúdo.

O separador Da Biblioteca de **Conteúdos:**
- Consulte o **Estado** para obter conteúdo que sincronize desde o servidor do site ativo até ao servidor do site de modo passivo.
- Pode selecionar conteúdo com um Estado de **Falha ,** e, em seguida, escolher **itens selecionados** sync a partir da Fita. Esta ação tenta resincronizar esse conteúdo desde a fonte do conteúdo até ao servidor do site do modo passivo. Durante a recuperação, o Estado exibe como **em curso**, e quando está em sincronização, exibe como **Sucesso**.

### <a name="try-it-out"></a>Experimente!
Tente completar as seguintes tarefas e, em seguida, envie-nos **feedback** do separador **Home** da Fita para nos informar como funcionava:
- Posso instalar um local primário em modo passivo.
- Posso usar a consola para promover o servidor de site de modo passivo para torná-lo o servidor de site de modo ativo, e confirmar a mudança de estado para ambos os servidores do site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclua confiança para ficheiros e pastas específicos numa política de Guarda de Dispositivos
<!-- 1324676 -->
Neste lançamento, adicionámos mais capacidades à gestão da política da [Guarda de Dispositivos](../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Agora pode adicionar opcionalmente confiança para ficheiros específicos para pastas numa política de Guarda de Dispositivos. Isto permite-lhe:

1. Superar problemas com comportamentos instaladores geridos
2. Aplicativos de linha de negócio sintetizados que não podem ser implementados com O Gestor de Configuração
3. Confie em aplicativos que estão incluídos numa imagem de implementação do sistema operativo.

### <a name="try-it-out"></a>Experimente!

1. Enquanto estiver a criar uma política de Guarda de Dispositivos, no separador Inclusãos do assistente de política Create Device Guard, clique em **Adicionar**.
2. Na caixa de diálogo **'Ficheiro' ou pasta Adicionar** Fidedignos, especifique informações sobre o ficheiro ou pasta em que pretende confiar. Pode especificar um ficheiro local ou uma pasta ou ligar-se a um dispositivo remoto ao qual tem permissão para ligar e especificar um ficheiro ou uma trajetória de pasta nesse dispositivo.
3. Conclua o assistente.


## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 -->
Nesta versão, pode controlar quando o progresso da sequência de tarefas é apresentado aos utilizadores finais utilizando uma nova variável. Na sua sequência de tarefas, utilize o passo variável da sequência de **tarefas definida** para definir o valor da variável **TSDisableProgressUI** para ocultar ou exibir o progresso da sequência de tarefas. Pode utilizar o passo variável da sequência de tarefas várias vezes numa sequência de tarefas para alterar o valor da variável. Isto permite-lhe ocultar ou exibir o progresso da sequência de tarefas em diferentes secções da sequência de tarefas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o passo variável da sequência de [tarefas definida](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** para **True** para ocultar o progresso da sequência de tarefas.

#### <a name="to-display-task-sequence-progress"></a>Para mostrar o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o passo variável da sequência de [tarefas definida](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) para definir o valor da variável **TSDisableProgressUI** para **False** para exibir o progresso da sequência de tarefas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especificar um local de conteúdo diferente para instalar conteúdo e desinstalar conteúdo
<!-- 1097546 -->
Hoje, no 'Gestor de Configuração', especifica a localização de instalação que contém os ficheiros de configuração de uma aplicação. Quando especifica uma localização de instalação, esta também é usada como a localização de desinstalada para o conteúdo da aplicação.
Com base no seu feedback, quando pretende desinstalar uma aplicação implementada, e o conteúdo da aplicação não está no computador do cliente, o cliente irá descarregar novamente todos os ficheiros de configuração da aplicação antes de a aplicação ser desinstalada.
Para resolver este problema, pode agora especificar tanto a localização do conteúdo de instalação como a uma localização opcional de desinstalação do conteúdo. Além disso, pode optar por não especificar a localização do conteúdo desinstalado.

### <a name="try-it-out"></a>Experimente!

1. No tipo de implementação propriedades de uma aplicação, clique no separador **Conteúdo.**
2. Configure a localização do **conteúdo instalar** normalmente.
3. Para **desinstalar as definições**de conteúdo, escolha uma das seguintes definições:
   - **Mesmo que instalar conteúdo** - A mesma localização do conteúdo será utilizada independentemente de estar a instalar ou desinstalar a aplicação.
   - **Sem desinstalar conteúdo** - Escolha isto se não quiser fornecer um local de desinstalação de conteúdo para a aplicação.
   - **Diferente do conteúdo de instalação** - Escolha isto se pretender especificar uma localização de conteúdo desinstalada diferente da localização do conteúdo de instalação.
5. Se selecionou **Diferente de instalar conteúdo,** navegue para ou introduza a localização do conteúdo da aplicação que será utilizado para desinstalar a aplicação.
6. Clique **em OK** para fechar a caixa de diálogo de propriedades do tipo de implementação.


## <a name="accessibility-improvements"></a>Melhorias de acessibilidade  
<!--1253000 -->
Esta pré-visualização introduz várias melhorias nas [funcionalidades](../understand/accessibility-features.md) de acessibilidade na consola 'Gestor de Configuração'. Estas incluem:     

**Novos atalhos de teclado para se mover em torno da consola:**
- CTRL + M - Conjuntos focam-se no painel principal (central).
- CTRL + T - Define o foco no nó superior do painel de navegação. Se o foco já estava naquele painel, o foco está definido para o último nó que visitou.
- CTRL + I - Define o foco na barra de migalhas de pão, abaixo da fita.
- CTRL + L - Define o foco no campo **de pesquisa,** quando disponível.
- CTRL + D - Define o foco no painel de detalhes, quando disponível.
- Alt – As alterações concentram-se dentro e fora da fita.

**Melhorias gerais:**
- Uma melhor navegação no painel de navegação quando digita as letras de um nome de nó.
- A navegação do teclado através da vista principal e da fita são agora circulares.
- A navegação do teclado no painel de detalhes é agora circular. Para voltar ao objeto ou painel anterior, utilize Ctrl + D e, em seguida, Mude + TAB.
- Depois de refrescar uma vista workspace, o foco está definido para o painel principal desse espaço de trabalho.
- Corrigiu um problema para permitir aos leitores de ecrã anunciar os nomes dos itens da lista.
- Acrescentou nomes acessíveis para vários controlos na página que permite aos leitores de ecrã anunciar informações importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Alterações ao Assistente de Serviços Azure para apoiar a prontidão de upgrade
<!-- 1353331 -->
A partir desta versão, utilize o Assistente de Serviços Azure para configurar uma ligação do Gestor de Configuração à Prontidão de Upgrade. A utilização do assistente simplifica a configuração do conector utilizando um assistente comum para serviços Azure relacionados.   

Embora o método para configurar a ligação tenha mudado, os pré-requisitos para a ligação e como utiliza a prontidão de atualização permanecem inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Pré-requisitos para a preparação da atualização
Os pré-requisitos para uma ligação à prontidão de atualização são inalterados em relação aos detalhados para o Atual Ramo de Gestor de Configuração. São repetidos aqui por conveniência:  

**Pré-requisitos**
- Para adicionar a ligação, o ambiente do Gestor de Configuração deve primeiro configurar um ponto de [ligação](../servers/deploy/configure/about-the-service-connection-point.md) de serviço num [modo online](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). Quando adicionar a ligação ao seu ambiente, também instalará o Agente de Monitorização da Microsoft na máquina que executa esta função do sistema do site.
- Registe o Gestor de Configuração como uma ferramenta de gestão "Web Application and/ou Web API", e obtenha o [ID do cliente a partir deste registo](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Crie uma chave de cliente para a ferramenta de gestão registada no Diretório Ativo Azure.
- No portal Azure, forneça à aplicação web registada permissão para aceder à OMS.

> [!IMPORTANT]       
> Ao configurar a permissão para aceder ao OMS, certifique-se de escolher a função **De Contribuinte** e atribuir permissões ao grupo de recursos da aplicação registada.

Depois de configurados os pré-requisitos, está pronto a utilizar o Assistente para criar a ligação.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Utilize o Assistente de Serviços Azure para configurar a prontidão de upgrade
1. Na consola, vá ao **Administration** > **Overview** > **Cloud Services** > **Azure Services**, e depois escolha os **Serviços Configure Azure** a partir do separador **Home** da fita, para iniciar o Assistente **de Serviços Azure**.

2. Na página **dos Serviços Azure,** selecione o **Conector**de Preparação de Atualização e, em seguida, clique em **Seguinte**.

3. Na página da **App,** especifique o seu **ambiente Azure** (a pré-visualização técnica suporta apenas a Nuvem Pública). Em seguida, clique **em Importar** para abrir a janela **De Importação apps.**

4. Na janela **Import Apps,** especifique detalhes para uma aplicação web que já existe no seu Anúncio Azure.
    - Forneça um nome amigável para o Nome do Inquilino Azure AD. Em seguida, especifique o ID do Inquilino, Nome da Aplicação, ID do Cliente, chave secreta para a aplicação web Azure e o APP ID URI.
    - Clique em **Verificar**, e se tiver sucesso, clique em **OK** para continuar.

5.  Na página **de Configuração,** especifique a subscrição, o grupo de recursos e o Espaço de Trabalho do Windows Analytics que pretende utilizar com esta ligação à Prontidão de Upgrade.  

6. Clique em **Next** para ir à página **Resumo** e, em seguida, complete o assistente para criar a ligação.


## <a name="new-client-settings-for-cloud-services"></a>Novas configurações de clientes para serviços na nuvem
<!-- 1319883 -->

Neste lançamento, adicionámos duas novas definições de cliente ao Gestor de Configuração. Vai encontrar isto na secção **de Serviços** de Nuvem.  Estas definições dão-lhe as seguintes capacidades:

- Controle quais os clientes do Gestor de Configuração que podem aceder a um gateway de gestão de nuvem configurado.
- Registe automaticamente os clientes Manger de Configuração ligados ao domínio do Windows 10 com o Diretório Ativo Azure.

Estas novas definições ajudam-no a realizar as capacidades descritas na [Pré-visualização técnica do Gestor de Configuração 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de começar

Você deve ter instalado e configurado Azure AD Connect entre o seu Diretório Ativo no local e o seu inquilino Azure AD.

Se remover a ligação, os dispositivos não estão registados, mas nenhum novo dispositivo se registará.

### <a name="try-it-out"></a>Experimente!

1. Configure as seguintes definições de cliente (encontradas na secção Cloud Services) utilizando as informações em [Como configurar as definições](../clients/deploy/configure-client-settings.md)do cliente .
   - **Registe automaticamente novos dispositivos de domínio Windows 10 com Diretório Ativo Azure** – set to **Yes** (predefinição) ou **No**.
   - **Ativar os clientes para utilizar um gateway** de gestão de nuvem – set to **Yes** (padrão) ou **Não**.
2. Implemente as definições do cliente na recolha de dispositivos necessárias.

Para confirmar que o dispositivo está unido ao Azure AD, execute o comando **dsregcmd.exe /status** numa janela de comando. O campo **AzureAdjoind** nos resultados mostrará **SIM** se o dispositivo for Azure AD juntou-se.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts PowerShell a partir da consola De Configuração Manager
<!-- 1236459 -->

No 'Gestor de Configuração', pode implementar scripts para dispositivos clientes utilizando pacotes e programas. Nesta pré-visualização técnica, adicionámos uma nova funcionalidade que lhe permite tomar as seguintes ações:

- Importar scripts PowerShell para gerente de configuração
- Editar os scripts da consola 'Gestor de Configuração' (apenas para scripts não assinados)
- Marque scripts como Aprovados ou Negados, para melhorar a segurança
- Execute scripts em coleções de computadores clientes windows e computadores geridos no local. Não se implantam scripts, em vez disso, são executados em quase tempo real em dispositivos de cliente.
- Examine os resultados devolvidos pelo script na consola 'Gestor de Configuração'.


### <a name="prerequisites"></a>Pré-requisitos

Para utilizar scripts, deve ser membro da função de segurança do Gestor de Configuração apropriado.

- **Para importar, e scripts** de autor - A sua conta deve ter permissões **para criar** permissões para **scripts SMS** na função de segurança **do Administrador Completo.**
- **Para aprovar, ou negar scripts** - A sua conta deve ter permissões **de aprovação** para **scripts SMS** na função de segurança **do Administrador Completo.**
- **Para executar scripts** - A sua conta deve ter permissões **de Script executar** para **Coleções** na função de segurança **compliance Settings Manager.**

Para obter mais informações sobre as funções de segurança do Gestor de Configuração, consulte [os fundamentos da administração baseada em papéis.](../understand/fundamentals-of-role-based-administration.md)

Por padrão, os utilizadores não podem aprovar um script que tenham sido autores. Uma vez que os scripts são poderosos, versáteis e podem ser implantados em muitos dispositivos, introduzimos um novo conceito de fornecer a capacidade de separar os papéis entre a pessoa que autora o guião e a pessoa que aprova o script. Isto dá um nível adicional de segurança contra executar um script sem supervisão. Pode desativar esta aprovação secundária, para facilitar os testes, particularmente durante o lançamento de Pré-visualização Técnica.

Para permitir que os utilizadores aprovem os seus próprios scripts:

1. Na consola do Configuration Manager, clique em **Administração**.
2. No espaço de trabalho da **Administração,** expanda a Configuração do **Site,** e depois clique em **Sites**.
3. Na lista de sites, escolha o seu site e, em seguida, no separador **Home,** no grupo **Sites,** clique em **Definições de Hierarquia**.
4. No separador **Geral** da caixa de diálogo de **definições** de hierarquia, limpe a caixa de verificação Não permita que os autores do **script aprovem os seus próprios scripts**.


### <a name="try-it-out"></a>Experimente!

#### <a name="import-and-edit-a-script"></a>Importar e editar um guião

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho da Biblioteca de **Software,** clique em **Scripts**.
3. No separador **Home,** no grupo **Criar,** clique em **Criar Script**.
4. Na página **script** do assistente **de script criar,** configure o seguinte:
   - **Nome script** - Introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, isto dificultará a sua descoberta do script que necessita na consola Do Gestor de Configuração.
   - **Linguagem script** - Atualmente, apenas os scripts **PowerShell** são suportados.
   - **Import** - Importar um script PowerShell para a consola. O script é exibido no campo **Script.**
   - **Clear** - Remove o script atual do campo **Script.**
   - **Script** - Exibe o script atualmente importado. Pode editar o guião neste campo conforme necessário.
5. Conclua o assistente. O novo script é apresentado na lista de **Script** com um estatuto de **Espera para aprovação**. Antes de poder executar este guião em dispositivos de cliente, tem de aprová-lo.


#### <a name="approve-or-deny-a-script"></a>Aprovar ou negar um guião



Antes de poder executar um guião, tem de ser aprovado. Para aprovar um guião:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho da Biblioteca de **Software,** clique em **Scripts**.
3. Na lista **script,** escolha o script que pretende aprovar ou negar e, em seguida, no separador **Home,** no grupo **Script,** clique **em Aprovar/Negar**.
4. Na Caixa de Diálogo **de Aprovação ou Negar,** **Aprove,** ou **negue** o script, e insira opcionalmente um comentário sobre a sua decisão. Se negar um guião, não pode ser executado em dispositivos de cliente.
5. Conclua o assistente. Na lista de **Scripts,** verás a alteração da coluna do Estado de **Aprovação** dependendo da ação que tomaste.

#### <a name="run-a-script"></a>Executar um roteiro

Uma vez aprovado um guião, pode ser executado contra uma coleção que escolher.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.
3. Na lista de Coleções de **Dispositivos,** clique na recolha de dispositivos em que pretende executar o script.
3. No separador **Home,** no grupo **All Systems,** clique no **Executar Script**.
4. Na página **script** do assistente do **Script Executar,** escolha um script da lista. Apenas são mostrados guiões aprovados. Clique em **Seguinte**e, em seguida, complete o assistente.

#### <a name="monitor-a-script"></a>Monitorize um script

Depois de ter executado um script para dispositivos clientes, use este procedimento para monitorizar o sucesso da operação.

1. Na consola 'Gestor de Configuração', clique em **Monitorização**.
2. No espaço de trabalho **de monitorização,** clique nos **Resultados do Script**.
3. Na lista de Resultados do **Script,** vê os resultados de cada script que executou nos dispositivos do cliente. Um código de saída de script de **0**, geralmente indica que o script correu com sucesso.

## <a name="pxe-network-boot-support-for-ipv6"></a>Suporte de arranque de rede PXE para IPv6
<!-- 1269793 -->
Agora pode ativar o suporte de arranque de rede PXE para o IPv6 para iniciar uma implementação do sistema operativo de sequência de tarefas. Quando utilizar esta definição, os pontos de distribuição ativados por PXE suportarão tanto o IPv4 como o IPv6. Esta opção não requer WDS e irá parar o WDS se estiver presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para ativar o suporte de arranque PXE para IPv6
Utilize o seguinte procedimento para ativar a opção de suporte IPv6 para PXE.

1. Na consola do Gestor de Configuração, vá a**Pontos**de Distribuição de Visão**Geral** > da **Administração,** > e clique em **Propriedades** para pontos de distribuição ativados por PXE.
2. No separador **PXE,** selecione **Suporte IPv6** para ativar suporte IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gerir as atualizações do controlador do Microsoft Surface
<!-- 1098490 -->
Agora pode utilizar o 'Gestor de Configuração' para gerir as atualizações do controlador do Microsoft Surface.

### <a name="prerequisites"></a>Pré-requisitos
Todos os pontos de atualização de software devem executar o Windows Server 2016.

### <a name="try-it-out"></a>Experimente!
Tente completar as seguintes tarefas e, em seguida, envie-nos **feedback** do separador **Home** da Fita para nos informar como funcionava:
1. Ativar a sincronização para os controladores Microsoft Surface. Utilize o procedimento na [classificação e produtos da Configuração](../../sum/get-started/configure-classifications-and-products.md) e selecione **Incluir controladores microsoft Surface e atualizações de firmware** no separador **Classificações** para ativar os controladores de Superfície.
2. [Sincronizar os controladores Microsoft Surface](../../sum/get-started/synchronize-software-updates.md).
3. [Implementar controladores sincronizados do Microsoft Surface](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configure atualização do Windows para políticas de adiamento de negócios
<!-- 1290890 -->
Agora pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento no novo nó **de Atualização do Windows para Políticas Empresariais** no âmbito da Manutenção da **Biblioteca** > de Software**Windows 10**.

### <a name="prerequisites"></a>Pré-requisitos
Os dispositivos Windows 10 geridos pelo Windows Update para o Negócios devem ter conectividade com a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma política de adiamento do Windows Update para negócios
1. Na **Biblioteca** > de Software**Windows 10 a servico** > **windows update para políticas empresariais**
2. No separador **Home,** no grupo **Create,** selecione **Create Windows Update for Business Policy** para abrir a Create Windows Update para o Assistente de Política de Negócios.
3. Na página **Geral,** forneça um nome e descrição para a apólice.
4. Na página **Deferral Policies,** configure se deve adiar ou interromper atualizações de funcionalidades.    
    Geralmente, as Atualizações de Funcionalidades são novas funcionalidades do Windows. Depois de configurar a definição do nível de prontidão do **Branch,** pode então definir se, e por quanto tempo, gostaria de adiar receber Atualizações de Funcionalidades após a sua disponibilidade da Microsoft.
    - **Nível de prontidão**do ramo : Desajuste o ramo para o qual o dispositivo receberá atualizações do Windows (Ramo Atual ou Ramo Atual para Negócios).
    - **Período de diferimento (dias)**: Especifique o número de dias para os quais as Atualizações de Funcionalidades serão adiadas. Pode diferir a receção destas Atualizações de Funcionalidades durante um período máximo de 180 dias após o seu lançamento.
    - **Pausa funcionalidades Atualizações a partir**de início : Selecione se suspender os dispositivos de receber Atualizações de Funcionalidades por um período de até 60 dias a partir do momento em que pausa as atualizações. Após ter decorrido o número máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações aplicáveis nas Atualizações do Windows. Após esta procura, pode colocar as atualizações em pausa novamente. Pode despausar atualizações de funcionalidades limpando a caixa de verificação.   
5. Escolha se deve adiar ou parar as Atualizações de Qualidade.     
    Geralmente, as Atualizações de Qualidade são correções e melhorias às funcionalidades do Windows existentes e, normalmente, são publicadas na primeira terça-feira de cada mês, embora possam ser lançadas em qualquer altura pela Microsoft. Pode definir se, e durante quanto tempo, gostaria de diferir a receção das Atualizações de Qualidade, após a sua disponibilidade.
    - **Período de diferimento (dias)**: Especifique o número de dias para os quais as Atualizações de Funcionalidades serão adiadas. Pode diferir a receção destas Atualizações de Funcionalidades durante um período máximo de 180 dias após o seu lançamento.
    - **Pausa Atualizações de Qualidade a partir**de início : Selecione se suspender os dispositivos de receber Atualizações de Qualidade por um período de até 35 dias a partir do momento em que pausa as atualizações. Após ter decorrido o número máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações aplicáveis nas Atualizações do Windows. Após esta procura, pode colocar as atualizações em pausa novamente. Pode despausar atualizações de qualidade limpando a caixa de verificação.
6. Selecione **Instalar atualizações de outros Produtos microsoft** para ativar a definição de política do grupo que torna as definições de diferimento aplicáveis ao Microsoft Update, bem como as Atualizações do Windows.
7. **Selecione Incluir controladores com Atualização do Windows** para atualizar automaticamente os controladores a partir de Atualizações do Windows. Se limpar esta definição, as atualizações do controlador não são descarregadas a partir de Atualizações do Windows.
8. Complete o assistente para criar a nova política de adiamento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implementar uma atualização do Windows para a política de adiamento de negócios
1. Na **Biblioteca** > de Software**Windows 10 a servico** > **windows update para políticas empresariais**
2. No separador **Home,** no grupo **implementação,** selecione Implementar a **Atualização do Windows para a Política de Negócios**.
3. Configure as seguintes definições:
    - Política de **configuração a implementar**: Selecione a atualização do Windows para a política de negócios que gostaria de implementar.
    - **Recolha**: Clique em **Navegar** para selecionar a coleção onde pretende implementar a apólice.
    - **Remediar regras não conformes quando suportadas**: Selecione para remediar automaticamente quaisquer regras que não estejam em conformidade com a Instrumentação de Gestão do Windows (WMI), o registo, scripts e todas as definições para dispositivos móveis matriculados pelo Gestor de Configuração.
    - **Permitir a reparação fora da janela de manutenção**: Se tiver sido configurada uma janela de manutenção para a recolha à qual está a implementar a apólice, ative esta opção para permitir que as definições de conformidade remediassem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../clients/manage/collections/use-maintenance-windows.md).
    - **Gerar um alerta**: Configura um alerta que é gerado se a conformidade da linha de base de configuração for inferior a uma percentagem especificada por uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar o processamento excessivo no Serviço de Inscrição de Dispositivos de Rede. O valor predefinido é 64 horas.
    - **Horário**: Especifique o calendário de avaliação de conformidade através do qual o perfil implantado é avaliado em computadores clientes. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Complete o assistente para implementar o perfil.



## <a name="support-for-entrust-certification-authorities"></a>Apoio às autoridades de certificação de Entrust
<!-- 1350740 -->
O Gestor de Configuração agora apoia as autoridades de certificação Da Entrust; isto permite a entrega de certificados PFX para dispositivos inscritos no Microsoft Intune.

Pode configurar a Entrust como autoridade de certificação ao adicionar uma função de Ponto de Registo de Certificado no Gestor de Configuração. Ao adicionar um novo perfil de certificado que emita certificados PFX, pode selecionar uma autoridade de certificação Microsoft ou Entrust.

**Problema conhecido**: Na pré-visualização técnica de 1706, os certificados PFX não são emitidos para as autoridades de certificação da Microsoft. Isto não afeta os certificados PFX importados ou os perfis SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Suporte da Cisco (IPsec) para perfis VPN iOS
<!-- 1321367 -->

Pode criar um perfil VPN iOS com cisco (IPsec) como o tipo de ligação. Para mais informações, consulte [Criar perfis VPN](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Definições de itens de configuração do Windows
<!-- 1354715 -->

Nesta versão, adicionámos as seguintes novas definições que pode utilizar em itens de configuração do Windows:

### <a name="password"></a>Palavra-passe

- **Encriptação do dispositivo**

### <a name="device"></a>Dispositivo

- **Modificação das definições da região (apenas no ambiente de trabalho)**
- **Modificação das definições de potência e sono**
- **Modificação de definições de idiomas**
- **Modificação do tempo do sistema**
- **Modificação do nome do dispositivo**

### <a name="store"></a>Arquivo

- **Aplicativos de atualização automática a partir da loja**
- **Utilize apenas loja privada**
- **Lançamento de app originada na loja**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloqueie o acesso a cerca de:bandeiras**
- **Substituição rápida do SmartScreen**
- **Substituição de aviso do SmartScreen para ficheiros**
- **Endereço IP local webRTC**
- **Motor de busca padrão**
- **OpenSearch XML URL**
- **Homepages (apenas desktop)**

Para obter mais informações sobre as definições de conformidade, consulte Garantir a [conformidade do dispositivo](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivos

* **Tipo de palavra-passe necessária**. Especifique se o utilizador deve criar uma palavra-passe alfanumérica ou uma palavra-passe numérica. Para senhas alfanuméricas, também especifica o número mínimo de conjuntos de caracteres que a palavra-passe deve ter. Os quatro conjuntos de caracteres são: minúsculas, letras maiúsculas, símbolos e números.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
<br></br>
* **Bloqueie a depuração USB no dispositivo**. Não é necessário configurar estas definições, uma vez que a depuração USB já está desativada em dispositivos Android for Work.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Bloqueie aplicações de fontes desconhecidas.** Exige que os dispositivos impeçam a instalação de aplicações de fontes desconhecidas. Não é preciso configurar esta definição, uma vez que os dispositivos Android for Work restringem sempre a instalação de fontes desconhecidas.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Requerer uma varredura de ameaças em apps**. Esta definição especifica que a funcionalidade de verificação de aplicações está ativada no dispositivo.

  **Suportado no:**
  * Android 4.2 a 4.4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
A partir desta versão, pode utilizar três novas definições de política de gestão de aplicações móveis (MAM):

- Captura de ecrã de **blocos (apenas dispositivos Android):** Especifica que as capacidades de captura do ecrã do dispositivo estão bloqueadas ao utilizar esta aplicação.

- **Desativar a sincronização de contacto:** Impede que a aplicação guarde dados para a aplicação Contacts nativa no dispositivo.

- **Desativar a impressão:** Impede que a aplicação imprimisse trabalhoou dados escolares.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição android e iOS
<!-- 1290826 -->
A partir desta versão, os administradores podem agora especificar que os utilizadores não podem inscrever dispositivos pessoais Android ou iOS no seu ambiente híbrido. Isto permite-lhe limitar os dispositivos matriculados a dispositivos pré-declarados, propriedade da empresa ou dispositivos iOS matriculados apenas no Programa de Inscrição de Dispositivos.

### <a name="try-it-out"></a>Experimente
1. Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2. No separador **Home** no grupo **Subscrição,** escolha **Plataformas Configure** e, em seguida, selecione **Android** ou **iOS**.
3. Selecione **dispositivos de propriedade pessoal do Bloco**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Política de gestão de aplicações Android for Work para copy-paste
Atualizámos as descrições de definição para itens de configuração Android for Work para a partilha de **dados permitir entre trabalho e perfil pessoal**.

|Antes de 1706 Pré-visualização técnica | Novo nome de opção | Comportamento|
|-|-|-|
|Impedir qualquer partilha entre limites| Restrições de partilha por defeito| Trabalho a pessoais: Padrão (espera-se que seja bloqueado em todas as versões) <br>Pessoal-a-trabalho: Padrão (permitido em 6.x+, bloqueado em 5.x)|
|Sem restrições| Aplicações no perfil pessoal podem lidar com pedidos de partilha a partir do perfil de trabalho| Trabalho a pessoal: Permitido  <br>Pessoal-a-trabalho: Permitido|
|Aplicações no perfil de trabalho podem lidar com pedidos de partilha de perfil pessoal |Aplicações no perfil de trabalho podem lidar com pedidos de partilha de perfil pessoal |Trabalho a pessoais: Padrão<br>Pessoal-a-trabalho: Permitido<br>(Apenas útil em 5.x onde o pessoal-a-trabalho é bloqueado)|

Nenhuma destas opções impede diretamente o comportamento da pasta de cópia. Adicionámos uma configuração personalizada ao serviço e à app Portal da Empresa em 1704 que pode ser configurada para evitar a pasta de cópias. Isto pode ser definido através de URI personalizado.

- OMA-URI: ./Fornecedor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo de valor: Boolean

Configurar o DisallowCrossProfileCopyPaste como verdadeiro impede o comportamento da pasta de cópia entre os perfis pessoais e de trabalho do Android para o Trabalho.

### <a name="try-it-out"></a>Experimente
1. Na consola do Gestor de Configuração, selecione Ativos **e** > **Overview** > itens de**configuração** > **Configuration items**de conformidade de conformidade .
2. Escolha **criar** um novo item de configuração e especifique **nome** e Android **para trabalho**.
3. No dispositivo de definição de grupos para configurar, selecione **Perfil de Trabalho**, e escolha **Seguinte**.
4. Selecione o valor para permitir a partilha de **dados entre trabalho e perfis pessoais**e, em seguida, complete o assistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Avaliação do Attestation de Saúde do Dispositivo para as políticas de conformidade para acesso condicional
<!-- 1097546 -->
A partir desta versão pode utilizar o estatuto de Attestation de Saúde do Dispositivo como regra da política de conformidade para o acesso condicional aos recursos da empresa.

### <a name="try-it-out"></a>Experimente
Selecione uma regra de Attestation de Saúde do Dispositivo como parte de uma avaliação da política de conformidade.
