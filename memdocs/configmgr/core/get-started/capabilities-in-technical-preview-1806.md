---
title: Pré-visualização técnica 1806
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de Pré-visualização Técnica do Gestor de Configuração 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2168f844f1c9ef98ea21da68b73531bca7aad999
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905179"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1806 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1806. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja o artigo [de Pré-visualização Técnica](technical-preview.md) antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Questões Conhecidas nesta Pré-Visualização Técnica

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a>Site falha em atualizar com biblioteca de conteúdos remotos
<!--514642-->
O site não atualiza com os seguintes erros em **cmupdate.log:**  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Este problema ocorre nesta versão quando a biblioteca de conteúdos está num local remoto.

#### <a name="workaround"></a>Solução
Mova a biblioteca de conteúdos para um drive local para o servidor do site. Para mais informações, consulte [Configure uma biblioteca de conteúdos remotos para o servidor do site](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a>Atualizações de software de terceiros
<!--1352101-->
Esta versão iterates ainda mais no suporte para atualizações de software de terceiros como resultado do feedback do [UtilizadorVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Já não é necessário utilizar o System Center Updates Publisher (SCUP) para alguns cenários comuns. O novo nó de Catálogos de **Atualizações de Software de Terceiros** na consola do Gestor de Configuração permite-lhe subscrever catálogos de terceiros, publicar as suas atualizações no seu ponto de atualização de software e, em seguida, implementá-los para clientes. 

Os seguintes catálogos de atualizações de software de terceiros estão disponíveis nesta versão:

 | Publisher | Nome do catálogo |
 |--------|---------------------|
 | HP | Catálogo de Atualizações de Clientes HP |

A SCUP continua a apoiar outros catálogos e cenários. A lista de catálogos no nó de Catálogos de Atualizações de Software de Terceiros da consola do Gestor de Configuração é dinâmica e será atualizada à medida que os catálogos adicionais estiverem disponíveis e suportados.


### <a name="prerequisites"></a>Pré-requisitos
- Configurar a gestão de atualizações de software, com um ponto de atualização de software ativado por HTTPS. Para mais informações, consulte [Prepare-se para a gestão](../../sum/get-started/prepare-for-software-updates-management.md)de atualizações de software.  
  - O ponto de atualização do software deve estar no servidor do site para esta funcionalidade nesta versão. <!--515810--> 

    > [!Tip]  
    > O ponto de atualização do software requer HTTPS porque é um requisito para as APIs wSUS usadas para lidar com certificados de assinatura. Os clientes também não precisam de ser ativados por HTTPS. Para obter mais informações sobre a habilitação do HTTPS sobre o WSUS, consulte os seguintes artigos para assistência:  
    > - [WSUS seguro com o protocolo Secure Sockets Layer](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [Post de blog wSUS Support](https://docs.microsoft.com/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- Espaço suficiente para o disco no ponto de atualização do software, pasta WSUSContent, para armazenar o conteúdo binário de origem para atualizações de software de terceiros. A quantidade de armazenamento necessário varia em função do fornecedor, tipos de atualizações e atualizações específicas que publica para implementação. Se precisar de mover a pasta WSUSContent para outra unidade com mais espaço livre, consulte a publicação de blog da equipa de suporte wSUS Como alterar o local onde a [WSUS armazena atualizações localmente](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).  

- Ative e implemente a definição do cliente [Ativar atualizações](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) de software de terceiros no grupo **Deactualizações** de Software.  

- O servidor do site requer acesso à internet para download.microsoft.com através da porta HTTPS 443. O serviço de sincronização de atualização de software de terceiros funciona atualmente no servidor do site. Este serviço atualiza a lista de catálogos disponíveis de terceiros, descarrega os catálogos quando se inscreve e descarrega as atualizações quando publicado. Configure as definições de procuração de internet, se necessário, no **separador Proxy** do sistema do site, propriedades do computador do servidor do site.  


### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Ativar e configurar a funcionalidade
Execute os seguintes passos *uma vez por hierarquia* para ativar e configurar a função para utilização:  

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **Configuração**do Site, e selecionar o nó **de Sites.**  

2. Selecione o site de alto nível na hierarquia. Na fita, clique em **Configurar componentes**do site , e selecione **Software Update Point**.  

3. Mude para o separador Atualizações de **Terceiros.** Selecione a opção para **ativar atualizações de software de terceiros**. Para obter mais informações sobre as opções do certificado, consulte [Melhorias para permitir o suporte à atualização de software de terceiros.](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  

   > [!Note]  
   > Se utilizar a opção predefinida para o Gestor de Configuração gerir este certificado, é criado um novo certificado de **assinatura WSUS** de terceiros do tipo De terceiros no nó de **Certificados** sob **Segurança** no espaço de trabalho da **Administração.**  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Subscreva um catálogo de terceiros e atualizações de sincronização
Execute os seguintes passos para *cada catálogo de terceiros* a que pretende subscrever:  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações** de software e selecionar o nó de **Catálogos de Atualizações de Software de Terceiros.**  

2. Selecione o catálogo para subscrever e clique **em Subscrever o Catálogo** na fita.   

3. Reveja e aprove o certificado de catálogo.  

   > [!Note]  
   > Quando subscreve um catálogo de atualizações de software de terceiros, o certificado que analisa e aprova no assistente é adicionado ao site. Este certificado é do tipo Catálogo **de Atualizações de Software de Terceiros.** Você pode geri-lo a partir do nó de **Certificados** sob **segurança** no espaço de trabalho **da Administração.**  

4. Conclua o assistente.  

   > [!Tip]  
   > Após a subscrição inicial, o catálogo deve começar a descarregar imediatamente. Em seguida, resincroniza a cada 24 horas neste lançamento. Se não quiser esperar que o catálogo descarregue automaticamente, clique em **Sync agora** na fita.  
   > 
   > Após o download do catálogo, os metadados do produto devem ser sincronizados no ponto de atualização do software. Para obter mais informações sobre este processo, bem como como iniciar manualmente, consulte as atualizações de [software Synchronize](../../sum/get-started/synchronize-software-updates.md). Neste ponto, pode ver as atualizações de terceiros no nó **All Updates.** 

5. Em seguida, configure o ponto de atualização de software **Produtos** para o catálogo de terceiros ao qual subscreveu. Para mais informações, consulte classificações e produtos da [Configuração para sincronizar](../../sum/get-started/configure-classifications-and-products.md). Após a alteração dos critérios do produto, a sincronização da atualização do software deve ocorrer novamente.

Antes de poder ver os resultados de conformidade dos clientes, eles precisam digitalizar e avaliar atualizações. Pode acionar manualmente este ciclo a partir do painel de controlo do Gestor de Configuração num cliente, executando a ação **software Updates Scan Cycle.** Para obter mais informações sobre o processo, consulte a introdução de atualizações de [Software.](../../sum/understand/software-updates-introduction.md)


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: Implementar atualizações de software de terceiros
Execute os seguintes passos para *quaisquer atualizações de software de terceiros* que pretenda implementar para os clientes:  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expanda **as Atualizações** de Software e selecione o nó **de Atualizações** de Software.  

   > [!Tip]  
   > Clique em **Adicionar Critérios** para filtrar a lista de atualizações. Por exemplo, adicione **o Fornecedor** para **a Adobe Systems, Inc.** para ver todas as atualizações da Adobe.  

2. Selecione as atualizações que são exigidas pelos clientes. Clique em **publicar conteúdo de atualização de software de terceiros** e reveja o progresso no SMS_ISVUPDATES_SYNCAGENT.log. Esta ação descarrega os binários de atualização do fornecedor e armazena-os na pasta WSUSContent no ponto de atualização do software. Também altera o estado da atualização de metadados apenas com conteúdo e implementável.  

   > [!Note]  
   > Quando publica conteúdo de atualização de software de terceiros, quaisquer certificados utilizados para assinar o conteúdo são adicionados ao site. Estes certificados são do tipo Conteúdo **de Atualizações de Software de Terceiros.** Você pode geri-los a partir do nó de **Certificados** sob **segurança** no espaço de trabalho **da Administração.**  

3. Implemente as atualizações utilizando o processo de gestão de atualizações de software existente. Para mais informações, consulte [a implementação](../../sum/deploy-use/deploy-software-updates.md)de atualizações de software . Na página de Localizações de **Descarregamento** do Assistente de Atualizações de Software de Implementação, selecione a opção padrão para **descarregar atualizações de software a partir da internet**. Neste cenário, o conteúdo já é publicado no ponto de atualização de software, que é usado para descarregar o conteúdo para o pacote de implementação.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorização do progresso das atualizações de software de terceiros
A sincronização de atualizações de software de terceiros é tratada pelo componente SMS_ISVUPDATES_SYNCAGENT no servidor do site. Pode visualizar mensagens de estado deste componente ou ver o estado mais detalhado no registo SMS_ISVUPDATES_SYNCAGENT.log. Este registo encontra-se no servidor do site na subpasta **Logs** do diretório de instalação do site. Por defeito, este caminho é `C:\Program Files\Microsoft Configuration Manager\Logs` . Para obter mais informações sobre a monitorização do processo geral de gestão de atualizações de software, consulte [as atualizações](../../sum/deploy-use/monitor-software-updates.md)de software do Monitor .


### <a name="known-issues"></a>Problemas conhecidos
- O serviço de sincronização de atualização de software de terceiros não suporta o ponto de atualização de software configurado para utilizar uma Conta de Ligação ao **Servidor WSUS**. Se esta conta estiver configurada no **separador Proxy e 'Definições** de Conta' da página de atualização do Software, verá o seguinte erro no SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Para obter mais informações sobre esta conta, consulte a Conta de Ligação de Pontos de [Atualização](../plan-design/hierarchy/accounts.md#software-update-point-connection-account)de Software .<!--515492-->  

- Não misture o uso de outras ferramentas, como a SCUP, com esta nova funcionalidade integrada de atualização de software de terceiros. O serviço de sincronização de atualização de software de terceiros não pode publicar conteúdo em atualizações apenas de metadados que foram adicionados à WSUS por outra aplicação, ferramenta ou script, como o SCUP. A ação **de atualização de software de terceiros** não se aciona nestas atualizações. Se necessitar de implementar atualizações de terceiros que esta funcionalidade ainda não suporta, utilize o seu processo existente na íntegra para implementar essas atualizações.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configure as definições do SmartScreen do Windows Defender para o Microsoft Edge
<!--1353701-->
Esta versão adiciona três definições para [o Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) à política de [definições](../../compliance/deploy-use/browser-profiles.md)de conformidade do navegador Microsoft Edge . A política inclui agora as seguintes definições adicionais na página de **Definições do SmartScreen:**
- **Permitir o SmartScreen**: Especifica se o Windows Defender SmartScreen é permitido. Para mais informações, consulte a política de [navegador AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- Os utilizadores podem substituir o **pedido do SmartScreen para sites**: Especifica se os utilizadores podem anular os avisos do Filtro SmartScreen do Windows Defender sobre websites potencialmente maliciosos. Para mais informações, consulte a política de [navegador PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- Os utilizadores podem substituir o **pedido do SmartScreen para ficheiros**: Especifica se os utilizadores podem anular os avisos do Filtro SmartScreen do Windows Defender sobre o descarregamento de ficheiros não verificados. Para mais informações, consulte a política de [navegador PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sync MDM política da Microsoft Intune para um dispositivo cogerido
<!--1357377-->
A partir desta versão, quando muda uma carga de [trabalho de cogestão,](../../comanage/how-to-switch-workloads.md)os dispositivos cogeridos sincronizam automaticamente a política de MDM da Microsoft Intune. Esta sincronização também acontece quando inicia a ação de Política de Computador de **Descarregamento** a partir de Notificações de Cliente na consola 'Gestor de Configuração'. Para mais informações, consulte Iniciar a recuperação da [política do cliente através da notificação do cliente](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Gabinete de Transição 365 carga de trabalho para Intune usando cogestão
<!--1357841-->
Agora pode transitar a carga de trabalho do Office 365 do Diretor de Configuração para o Microsoft Intune depois de permitir a cogestão. Para fazer a transição desta carga de trabalho, vá à página de propriedades de cogestão e mova a barra de slider de Configuração Manager para Pilot ou All. Para mais informações, consulte [co-management para dispositivos Windows 10](../../comanage/overview.md).

Há também uma nova condição global, são as **aplicações do Office 365 geridas pela Intune no dispositivo.** Esta condição é adicionada por defeito como requisito para os novos pedidos do Office 365. Ao transitar esta carga de trabalho, os clientes cogeridos não cumprem os requisitos da aplicação, pelo que não instalam o Office 365 implementado através do Gestor de Configuração.

### <a name="known-issue"></a>Problema conhecido
- Esta transição de carga de trabalho aplica-se atualmente apenas às implantações do Office 365. O Gestor de Configuração continua a gerir as atualizações do Office 365.<!--510876--> Para mais informações, incluindo uma possível suposição, consulte a versão de lançamento do 'Gestor de Configuração' 1802, [alterando a definição de cliente do Office 365.](../servers/deploy/install/release-notes.md)



## <a name="package-conversion-manager"></a>Gestor de Conversão de Pacotes 
<!--1357861-->
O Gestor de Conversão de Pacotes é agora uma ferramenta integrada que lhe permite converter pacotes legados do Gestor de Configuração 2007 em aplicações atuais do Gestor de Configuração. Depois pode utilizar funcionalidades de aplicações como dependências, regras de exigência e afinidade do dispositivo de utilização.

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

> [!Important]  
> Se já instalou uma versão mais antiga do Gestor de Conversão de Pacotes, desinstale-o primeiro antes de atualizar o seu site. A nova versão integrada não requer instalação, mas pode entrar em conflito com as versões existentes.  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir gestão de **aplicações** e selecionar **pacotes.**  
2. Selecione um pacote. As seguintes três opções estão disponíveis no grupo de conversão de **pacotes** da fita:  
     - **Pacote de análise**: Inicie o processo de conversão analisando o pacote.
     - **Pacote conversão**: Alguns pacotes podem ser facilmente convertidos em aplicações com esta ação.
     - **Corrigir e Converter**: Alguns pacotes requerem problemas a corrigir antes de se converterem em aplicações.  


3. Vá ao espaço de trabalho **de monitorização** e selecione **O Estado**de Conversão do Pacote . Este novo painel de instrumentos mostra o estado geral de análise e conversão dos pacotes no site. Uma nova tarefa de fundo resume automaticamente os dados da análise.  

   > [!Tip]  
   > O Gestor de Conversão de Pacotes não requer que agende a análise dos pacotes. Esta ação é agora tratada pela tarefa integrada de resumição.  

![Screenshot do painel de instrumentos de estado de conversão do pacote](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Implementar atualizações de software sem conteúdo
<!--1357933-->
Agora pode implementar atualizações de software para dispositivos sem primeiro descarregar e distribuir conteúdos de atualização de software para pontos de distribuição. Esta funcionalidade é benéfica quando se lida com conteúdos de atualização extremamente grandes, ou quando sempre deseja que os clientes obtenha conteúdo do serviço cloud microsoft Update. Os clientes neste cenário também podem descarregar conteúdos de pares que já tenham os conteúdos necessários. O cliente do Gestor de Configuração continua a gerir o download de conteúdos, podendo assim utilizar a funcionalidade de cache de pares do Gestor de Configuração, ou outras tecnologias, como a Otimização de Entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Gestor de Configuração, incluindo atualizações do Windows e do Office. 

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Inicie uma implementação de atualização de software normalmente. Para mais informações, consulte [a implementação](../../sum/deploy-use/deploy-software-updates.md)de atualizações de software .
2. No Assistente de Atualizações de Software de Implementação, na página pacote de **implementação,** selecione a nova opção para nenhum pacote de **implementação**.

### <a name="known-issues"></a>Problemas conhecidos
- O ícone para uma atualização implementada com esta definição mostra incorretamente com um X vermelho como se a atualização fosse inválida. Para mais informações, consulte [ícones utilizados para atualizações](../../sum/understand/software-updates-icons.md)de software . <!--515556-->  
- Esta definição só está integrada com o Assistente de Atualizações de Software de Implementação. Não está disponível atualmente com regras de implementação automáticas. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração de ferramentas de personalização de escritório com o Instalador office 365
<!--1358149-->
A Ferramenta de Personalização do Office está agora integrada com o Instalador office 365 na consola Do Gestor de Configuração. Ao criar uma implementação para o Office 365, pode agora configurar dinamicamente as mais recentes definições de gestão do Office. A Ferramenta de Personalização do Office é atualizada ao mesmo tempo que o lançamento de novas construções do Office 365. Agora pode aproveitar as novas definições de gestão no Office 365 assim que estiverem disponíveis. 

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola Do Gestor de Configuração precisa de acesso à Internet através da porta HTTPS 443. O Assistente de Instalação de Clientes do Office 365 utiliza um API padrão do navegador Windows para abrir https://config.office.com . Se for utilizado um proxy de internet, o utilizador deve poder aceder a este URL.

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software** e selecione o nó de Gestão de **Clientes do Office 365.**
2. Clique no azulejo do **Instalador office 365** no painel de instrumentos para lançar o Assistente de Instalação do Cliente do Office 365. Para mais informações, consulte o [Deploy Office 365 apps](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).
3. Na página definição de **escritório,** clique em **Ir para a página web do Office**. Utilize a ferramenta de personalização do office online para especificar as definições para esta implementação. 
4. Clique em **Submeter** no canto superior direito quando estiver concluído. Termine o Assistente de Instalação do Cliente do Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Melhorias na porta de entrada de gestão de nuvem
Esta versão inclui as seguintes melhorias ao gateway de gestão da nuvem (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de botas de cliente simplificada
<!--1358215-->
Ao instalar o cliente Do Gestor de Configuração na internet através de um CMG, são agora necessárias menos propriedades de linha de comando. Para obter mais informações sobre um exemplo deste cenário, consulte a linha Comando para instalar o cliente do Gestor de [Configuração](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) quando se preparar para a cogestão. 

As seguintes propriedades da linha de comando são necessárias em todos os cenários:
- CCMHOSTNAME  
- SMSSITECODE  

São necessárias as seguintes propriedades ao utilizar a AD Azure para autenticação de clientes em vez de certificados de autenticação de clientes baseados em PKI:
- AADCLIENTAPPID  
- AADRESOURCEURI  

A seguinte propriedade é necessária se o cliente irá voltar para a intranet:
- SMSMP  

O exemplo seguinte inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para mais informações, consulte as propriedades de [instalação do Cliente.](../clients/deploy/about-client-installation-properties.md)

### <a name="download-content-from-a-cmg"></a>Descarregue conteúdo de um CMG
<!--1358651-->
Anteriormente, tinha de implantar um ponto de distribuição em nuvem e CMG como funções separadas. Agora, neste comunicado, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure. Para ativar esta funcionalidade, ative a nova opção de permitir que a CMG funcione como um ponto de distribuição na **nuvem e sirva conteúdo do armazenamento Azure** no separador **Definições** das propriedades CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Certificado de raiz fidedigno não é necessário com Azure AD
<!--503899-->
Quando cria um CMG, já não é necessário fornecer um [certificado de raiz fidedigno](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) na página Definições. Este certificado não é necessário quando se utiliza o Azure Ative Directory (Azure AD) para autenticação do cliente, mas costumava ser exigido no assistente.

> [!Important]  
> Se estiver a utilizar certificados de autenticação de clientes PKI, então ainda deve adicionar um certificado de raiz fidedigno à CMG.



## <a name="improvements-to-secure-client-communications"></a>Melhorias para garantir comunicações de clientes
<!--1358278,1358279-->
Esta versão continua a iterar na melhoria das [comunicações seguras](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) dos clientes, removendo dependências adicionais na conta de acesso à rede. Quando permite que a nova opção de utilização de certificados gerados pelo Gestor de Configuração utilize os certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP,** os seguintes cenários não requerem uma conta de acesso à rede para descarregar conteúdo a partir de um ponto de distribuição:  

- Sequências de tarefas que saem dos meios de arranque ou PXE
- Sequências de tarefas que correm do Centro de Software  

Estas sequências de tarefapodem ser para implementação de OS ou personalizadas. Também é suportado para computadores de grupo de trabalho.



## <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura do Software Center
<!--1358309-->
As funções de catálogo de aplicações já não são necessárias para exibir aplicações disponíveis pelo utilizador no Software Center. Esta alteração ajuda-o a reduzir a infraestrutura de servidores necessária para entregar aplicações aos utilizadores. O Software Center conta agora com o ponto de gestão para obter esta informação, o que ajuda a maiores ambientes a escalar melhor, atribuindo-os a [grupos de fronteira.](../servers/deploy/configure/boundary-groups.md#management-points)

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Remova todas as funções de catálogo de aplicações do site. Estas funções incluem o ponto de serviço web do catálogo de aplicações e o ponto de site do catálogo de aplicações.
2. Implemente uma aplicação disponível para uma recolha de utilizadores.
3. Utilize o Software Center como um utilizador direcionado para procurar, solicitar e instalar a aplicação.

### <a name="known-issue"></a>Problema conhecido
- Se utilizar um cliente ligado ao Diretório Ativo Azure com esta funcionalidade, não configure o site para **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**. Atualmente, entra em conflito com esta funcionalidade.<!--515846--> Para obter mais informações sobre esta definição, consulte melhores [comunicações seguras para o cliente](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Disponibilize pacotes de aplicativos Windows para todos os utilizadores num dispositivo
<!--1358310-->
Agora pode fornecer uma aplicação com um pacote de aplicações Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é fornecer uma aplicação da Microsoft Store for Business and Education, como Minecraft: Education Edition, a todos os dispositivos utilizados pelos alunos de uma escola. Anteriormente, o Gestor de Configuração apenas suportava a instalação destas aplicações por utilizador. Depois de iniciar sessão num novo dispositivo, um aluno teria de esperar para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada para o dispositivo para todos os utilizadores, podem ser produtivas mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, fornecimento e atualização de diferentes versões do mesmo pacote de aplicações windows num dispositivo, o que pode causar resultados inesperados. Este comportamento pode ocorrer ao utilizar o 'Configuração Manager' para fornecer a aplicação, mas depois permite que os utilizadores atualizem a aplicação a partir da Microsoft Store. Para mais informações, consulte a próxima orientação de passos quando [gerir aplicações da Microsoft Store for Business](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Ao fornecer uma aplicação licenciada offline, o Gestor de Configuração não permite que o Windows a atualize automaticamente a partir da Microsoft Store.  

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Criar uma nova aplicação. Esta aplicação deve ser de um pacote de aplicativos Windows, ou de uma aplicação licenciada offline, que sincronizou a partir da Microsoft Store para Negócios e Educação.  

2. Na página **informação geral** do Assistente de Aplicação Criar, ative a opção de **fornecer esta aplicação a todos os utilizadores do dispositivo**.  

   > [!Tip]  
   > Se estiver a modificar uma aplicação existente, esta definição está no separador **User Experience** das propriedades da aplicação.  

3. Implemente a aplicação para uma recolha de dispositivos.  

4. Inicie sessão num dispositivo direcionado com diferentes contas de utilizador e inicie a aplicação.  

> [!Note]  
> Se necessitar de desinstalar uma aplicação aprovisionada a partir de dispositivos aos quais os utilizadores já assinaram, precisa de criar duas implementações de desinstaladas. Direcione a primeira implementação de sinstalação para uma coleção de dispositivos que contenha os dispositivos. Direcione a segunda implementação de saque para uma coleção de utilizadores que contenha os utilizadores que já assinaram em dispositivos com a aplicação provisionada. Ao desinstalar uma aplicação aprovisionada num dispositivo, o Windows atualmente não desinstala essa aplicação para os utilizadores. 



## <a name="improvements-to-the-surface-dashboard"></a>Melhorias no painel surface
<!--1358654-->
Esta versão inclui as seguintes melhorias no [painel](../clients/manage/surface-device-dashboard.md)surface:
- O painel surface apresenta agora uma lista de dispositivos relevantes quando são selecionadas secções de gráficos.
   - Clicar no azulejo **Por cento dos dispositivos de superfície** abre uma lista de dispositivos Surface.
   - Clicar numa barra no azulejo **top 5 firmware versions** abre uma lista de dispositivos Surface com essa versão específica do firmware.
- Ao visualizar estas listas de dispositivos a partir do painel de instrumentos Surface, pode clicar num dispositivo e executar ações comuns.



## <a name="hardware-inventory-default-unit-revision"></a>Revisão da unidade padrão de inventário de hardware
<!--514442-->
Na [versão 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure)do Gestor de Configuração, a unidade padrão utilizada em muitas visualizações de reporte passou de megabytes (MB) para gigabytes (GB). Devido a melhorias no inventário de [hardware para grandes valores inteiros](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values), e com base no feedback do cliente, esta unidade padrão é agora MB novamente.



## <a name="next-steps"></a>Próximos passos
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
