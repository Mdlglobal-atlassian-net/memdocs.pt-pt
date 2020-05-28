---
title: Pré-visualização técnica 1805
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de Pré-visualização Técnica do Gestor de Configuração 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d8c1cd6610bd09b2714951d8a755770b6347b2f6
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905236"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1805 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1805. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja o artigo [de Pré-visualização Técnica](technical-preview.md) antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Criar uma implantação faseada com fases configuradas manualmente para uma sequência de tarefas
<!--1358148-->
Agora pode [criar uma implementação faseada](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) com fases configuradas manualmente para uma sequência de tarefas. Pode adicionar até 10 fases adicionais a partir do separador **Fases** do assistente de implantação faseada. 


### <a name="try-it-out"></a>Experimente!
Siga as instruções para criar uma implantação faseada onde configura manualmente todas as fases. Envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou. 

1. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**  

2. Clique à direita numa sequência de tarefas existente e selecione **Criar implantação faseada**.  

3. No separador **Geral,** dê à implementação faseada um nome, descrição (opcional) e **selecione manualmente configurar todas as fases**.  

4. No separador **Fases,** clique em **Adicionar**.  

5. Especifique um **Nome** para a fase e, em seguida, navegue para a Coleção de **Fase-Alvo**.  

6. No separador Definições de **Fase,** escolha uma opção para cada uma das definições de agendamento e selecione **Seguinte** quando estiver completo.  

    - Critérios para o sucesso da fase anterior (Esta opção é desativada para a primeira fase.)
        - **Percentagem de sucesso**de implementação : Especifique por cento dos dispositivos que completem com sucesso a implementação para os critérios de sucesso da fase anterior.  

    - Condições para iniciar esta fase de implantação após o sucesso da fase anterior  
        - Iniciar automaticamente esta fase após um período de **diferimento (em dias)**: Escolha o número de dias para esperar antes de iniciar a próxima fase após o sucesso da fase anterior. 
        - **Inicie manualmente esta fase de implantação**: Não inicie esta fase automaticamente após o sucesso da fase anterior.  

    - Uma vez que um dispositivo é direcionado, instale o software
        - **O mais rapidamente possível**: Estabelece o prazo para a instalação no aparelho logo que o dispositivo seja direcionado.
        - **Prazo (em relação ao dispositivo**de tempo) : Estabelece o prazo para a instalação de um determinado número de dias após o alvo do dispositivo.  
     
7. Complete o assistente de Definições de Fase.

8. No separador **Fases** do assistente de implantação faseada, pode agora adicionar, remover, reencomendar ou editar as fases para esta implementação.  

9. Complete o assistente de implantação faseada create.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte de ponto de distribuição em nuvem para Gestor de Recursos Azure
<!--1322209-->
Ao criar uma instância do ponto de distribuição da [nuvem,](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)o assistente oferece agora a opção de criar uma implementação do Gestor de **Recursos Azure**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de [recursos.](/azure/azure-resource-manager/resource-group-overview#resource-groups) Ao implantar um ponto de distribuição em nuvem com o Azure Resource Manager, o site utiliza o Azure Ative Directory (Azure AD) para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure.  

O assistente de ponto de distribuição em nuvem ainda fornece a opção para uma **implementação de serviço clássico** usando um certificado de gestão Azure. Para simplificar a implantação e gestão de recursos, recomendamos a utilização do modelo de implantação do Gestor de Recursos Azure para todos os novos pontos de distribuição na nuvem. Se possível, reimplante os pontos de distribuição de nuvem existentes através do Gestor de Recursos.

O Gestor de Configuração não migra os pontos clássicos de distribuição da nuvem existentes para o modelo de implementação do Gestor de Recursos Azure. Crie novos pontos de distribuição em nuvem utilizando implementações do Gestor de Recursos Azure e, em seguida, remova os pontos clássicos de distribuição da nuvem. 

> [!IMPORTANT]  
> Esta capacidade não permite suporte para fornecedores de serviços de nuvem Azure (CSP). A implantação do ponto de distribuição em nuvem com o Azure Resource Manager continua a utilizar o serviço clássico de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Pré-requisitos  
- Integração com [a Azure AD.](../clients/deploy/deploy-clients-cmg-azure.md) Não é necessária a descoberta do utilizador da AD Azure.  

- Os [mesmos requisitos para um ponto](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements)de distribuição em nuvem, com exceção do certificado de gestão Azure.  


### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola de Gestor de Configuração, espaço de trabalho **da Administração,** expandir **os Serviços cloud,** e selecionar **Pontos**de Distribuição de Cloud . Clique em **Criar ponto** de distribuição de nuvem na fita.   

2. Na página **Geral,** selecione implementação do **Gestor de Recursos Azure**. Clique **em Iniciar sessão** para autenticar com uma conta de administrador de subscrição Azure. O assistente povoa automaticamente os restantes campos da informação de subscrição da AD Azure armazenada durante o pré-requisito de integração. Se possuir várias subscrições, selecione a subscrição desejada para utilizar. Clique em **Seguinte**.  

3. Na página **Definições,** forneça o ficheiro de **Certificado** PKI do servidor, como de costume. Este certificado define o serviço de ponto de distribuição em nuvem **FQDN** utilizado pelo Azure. Selecione a **Região**e, em seguida, selecione uma opção de grupo de recursos para **criar novas** ou **utilizar existentes**. Introduza o novo nome do grupo de recursos ou selecione um grupo de recursos existente na lista de drop-down.  

4. Conclua o assistente.  

> [!NOTE]  
> Para a aplicação de servidor AD Azure selecionada, o Azure atribui a permissão do **colaborador** de subscrição.  

Monitorize o progresso da implementação do serviço com **cloudmgr.log** no ponto de ligação de serviço.



## <a name="take-actions-based-on-management-insights"></a>Tomar ações com base em insights de gestão
<!--1357930-->
Alguns [conhecimentos de gestão](../servers/manage/management-insights.md) têm agora a opção de tomar uma ação. Dependendo da regra, esta ação exibe um dos seguintes comportamentos:  

- Navegue automaticamente na consola até ao nó onde poderá tomar mais medidas. Por exemplo, se o insight de gestão recomendar a alteração da definição de um cliente, tomar medidas navega para o nó de Definições do Cliente. Pode tomar mais medidas modificando o padrão ou um objeto de definições personalizadas do cliente.  

- Navegue para uma vista filtrada com base numa consulta. Por exemplo, tomar medidas sobre a regra das coleções vazias mostra apenas estas coleções na lista de coleções. Aqui pode tomar medidas adicionais, tais como apagar uma coleção ou modificar as suas regras de adesão.  

As seguintes regras de insight de gestão têm ações nesta versão:
- Segurança
    - Versões de clientes antimalware não suportadas
- Centro de Software
    - Use a nova versão do Software Center
- Aplicações
    - Aplicações sem implementações
- Gestão Simplificada
    - Versões de clientes não CB
- Coleções
    - Coleções Vazias 
- Serviços Cloud
    - Atualizar clientes para a versão mais recente do Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Carga de trabalho de configuração do dispositivo de transição para Intune usando cogestão
<!--1357903-->

Agora pode transitar a carga de trabalho de configuração do dispositivo de Configuração Manager para Intune depois de permitir a cogestão. A transição desta carga de trabalho permite-lhe utilizar o Intune para implantar polícias de MDM, ao mesmo tempo que continua a utilizar o Gestor de Configuração para a implementação de aplicações. 

Para fazer a transição desta carga de trabalho, vá à página de propriedades de cogestão e mova a barra de slider de Configuração Manager para **Pilot** ou **All**. Para mais informações, consulte [co-management para dispositivos Windows 10](../../comanage/overview.md).

> [!Note]  
> Mover esta carga de trabalho também move as cargas de trabalho de acesso a **recursos** e de proteção de **pontos finais,** que são um subconjunto da carga de trabalho de configuração do dispositivo.

Ao transitar esta carga de trabalho, ainda pode implementar definições do 'Configuração Manager' para dispositivos cogeridos, mesmo que intune seja a autoridade de configuração do dispositivo. Esta exceção pode ser usada para configurar configurações que são exigidas pela sua organização, mas ainda não disponíveis em Intune. Especifique esta exceção numa linha de base de configuração do Gestor de Configuração. Ative a opção de **aplicar sempre esta linha de base mesmo para clientes cogeridos** ao criar a linha de base, ou no separador **Geral** das propriedades de uma linha de base existente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ativar pontos de distribuição para usar o controlo de congestionamento da rede
<!--1358112-->

O Windows Low Delay Background Transport (LEDBAT) é uma funcionalidade do Windows Server para ajudar a gerir as transferências de rede de fundo. Para os pontos de distribuição que estão em execução em versões suportadas do Windows Server, pode ativar uma opção para ajudar a ajustar o tráfego de rede. Os clientes só usam largura de banda da rede quando estão disponíveis. 


### <a name="prerequisites"></a>Pré-requisitos
- Um ponto de distribuição no Windows Server, versão 1709.  

- Não há nenhum pré-requisito do cliente.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Selecione o nó pontos de **distribuição.** Selecione o ponto de distribuição do alvo e clique em **Propriedades** na fita.  

2. No separador **Geral,** ative a opção de ajustar a velocidade de descarregamento para utilizar a largura de banda da **rede não utilizada (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Painel de gestão de nuvem
<!--1358461-->
O novo **painel de gestão** de nuvem proporciona uma visão centralizada para o uso de gateway de gestão de nuvem (CMG). Quando o site está a bordo com a AD Azure, também exibe dados sobre utilizadores e dispositivos da nuvem.  

A seguinte imagem é uma parte do painel de gestão de nuvens mostrando dois dos azulejos disponíveis:  
![Painel de instrumentos de gestão de nuvem azulejos CMG tráfego e clientes online atuais](media/1358461-cmg-dashboard.png)

Esta funcionalidade também inclui o analisador de **ligação CMG** para verificação em tempo real para ajudar na resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através do ponto de ligação CMG a quaisquer pontos de gestão que permitam o tráfego cmg.


### <a name="prerequisites"></a>Pré-requisitos
- Um gateway de [gestão](../clients/manage/cmg/plan-cloud-management-gateway.md) de nuvem ativa usado por clientes baseados na Internet.  

- O site a bordo dos [serviços azure](../servers/deploy/configure/azure-services-wizard.md) para gestão de nuvem.  


### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

#### <a name="cloud-management-dashboard"></a>Painel de gestão de nuvem

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Selecione o nó **de Cloud Management** e veja os azulejos do painel de instrumentos.  

#### <a name="cmg-connection-analyzer"></a>Analisador de ligação CMG

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **os Serviços cloud** e selecionar gateway de **gestão**cloud .  

2. Selecione a instância CMG alvo e, em seguida, selecione o analisador de **ligação** na fita.  

3. Na janela analisador de ligação CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Utilizador da AD Azure:** utilize esta opção para simular a comunicação da mesma forma que uma identidade de utilizador baseada na nuvem ligada a um dispositivo Windows 10 ligado ao Azure AD. Clique **em Iniciar sessão** para introduzir de forma segura as credenciais para esta conta de utilizador da AD Azure.  

     2. **Certificado de cliente:** utilize esta opção para simular a comunicação da mesma forma que um cliente do Gestor de Configuração com um certificado de [autenticação do cliente.](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth)  

4. Clique **em Começar** a análise. Os resultados são apresentados na janela do analisador. Selecione uma entrada para ver mais detalhes no campo Descrição.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
O Gestor de Configuração sempre forneceu uma grande loja centralizada de dados do dispositivo, que os clientes usam para fins de reporte. No entanto, esses dados são tão bons quanto a última vez que foram recolhidos junto dos clientes. 

A CMPivot é um novo utilitário na consola que proporciona acesso ao estado real dos dispositivos no seu ambiente. Executa imediatamente uma consulta em todos os dispositivos atualmente conectados na recolha do alvo e devolve os resultados. Em seguida, pode filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode responder mais rapidamente a questões de negócios, resolver problemas e responder a incidentes de segurança.

Por exemplo, na mitigação das [vulnerabilidades dos canais laterais de execução especulativa,](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)um dos requisitos é atualizar o sistema BIOS. Pode utilizar a CMPivot para consultar rapidamente informações do sistema BIOS e encontrar clientes que não estejam em conformidade. 

Nesta imagem, a CMPivot apresenta duas versões BIOS separadas com uma contagem de dispositivos de cada. Pode utilizar esta consulta de exemplo quando experimentar a CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Janela CMPivot com consulta de exemplo fro BIOSVersion](media/1358456-cmpivot-biosversion.png)

Pode clicar na contagem do dispositivo para perfurar para ver os dispositivos específicos. Ao visualizar dispositivos na CMPivot, pode clicar num dispositivo e selecionar as seguintes ações de notificação do [cliente:](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)
- Executar script
- Controlo Remoto
- Explorador de Recursos

Ao clicar à direita num dispositivo específico, também pode orientar a visão do dispositivo específico para um dos seguintes atributos:
- Comandos autostart
- Produtos Instalados
- Processos
- Serviços
- Utilizadores
- Conexões Ativas
- Atualizações em falta

### <a name="prerequisites"></a>Pré-requisitos
- Os clientes-alvo devem ser atualizados para a versão mais recente.  

- O administrador do Gestor de Configuração precisa de permissões para executar scripts. Para mais informações, consulte [as funções de Segurança para scripts](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola De Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance** e selecione Coleçãos de **Dispositivos**. Selecione uma coleção de alvos e clique em **Iniciar CMPivot** na fita para lançar a ferramenta.  

2. A interface fornece mais informações sobre a utilização da ferramenta. 
     - Pode introduzir manualmente cordas de consulta na parte superior ou clicar nos links na documentação em linha.
     - Clique numa das **Entidades** para adicioná-la à corda de consulta. 
     - Os links para **Operadores de Mesa,** Funções de **Agregação**e **Funções Escalar** abrem documentação de referência linguística no navegador web. A CMPivot usa a mesma linguagem de consulta que o [Azure Log Analytics.](https://docs.microsoft.com/azure/kusto/query/)



## <a name="improved-secure-client-communications"></a>Melhoria das comunicações seguras dos clientes
<!--1356889,1358228,1358460-->
A utilização da comunicação HTTPS é recomendada para todos os caminhos de comunicação do Gestor de Configuração, mas pode ser um desafio para alguns clientes devido à sobrecarga de gestão de certificados PKI. A introdução da integração do Azure Ative Directory (Azure AD) reduz alguns, mas não todos os requisitos de certificado. 

Esta versão inclui melhorias na forma como os clientes comunicam com os sistemas do site. Há dois objetivos primários para estas melhorias:  

- Pode garantir a comunicação do cliente sem a necessidade de certificados de autenticação do servidor PKI.  

- Os clientes podem aceder de forma segura a conteúdos a partir de pontos de distribuição sem a necessidade de uma conta de acesso à rede.  

> [!Note]  
> Os certificados PKI ainda são uma opção válida para os clientes que pretendam utilizá-lo.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Cenários
Os seguintes cenários beneficiam destas melhorias:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a>Cenário 1: Cliente para ponto de gestão
<!--1356889-->
[Os dispositivos unidos da Azure AD](/azure/active-directory/devices/concept-azure-ad-join) podem comunicar através de um portal de gestão de nuvem (CMG) com um ponto de gestão configurado para HTTP. O servidor do site gera um certificado para o ponto de gestão que lhe permite comunicar através de um canal seguro.   

> [!Note]  
> Este comportamento é alterado da versão atual do 'Gestor de Configuração' 1802, que requer um ponto de gestão ativado por HTTPS para este cenário. Para mais informações, consulte O ponto de [gestão enable para HTTPS](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a>Cenário 2: Cliente para ponto de distribuição
<!--1358228-->
Um grupo de trabalho ou um cliente azure ad pode descarregar conteúdo num canal seguro a partir de um ponto de distribuição configurado para HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a>Cenário 3 Identidade do dispositivo AD Azure 
<!--1358460-->
Um [dispositivo Azure AD azure](/azure/active-directory/devices/concept-azure-ad-join-hybrid) ou híbrido sem um utilizador azure AD sessão pode comunicar com segurança com o seu site atribuído. A identidade do dispositivo baseado na nuvem é agora suficiente para autenticar com o CMG e o ponto de gestão.  


### <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gestão configurado para ligações ao cliente HTTP. Detete esta opção no separador **Geral** das propriedades do sistema do site.  

- Um ponto de distribuição configurado para ligações ao cliente HTTP. Detete esta opção no separador **Geral** das propriedades do sistema do site. Não permita que os **clientes se conectem de forma anónima**.  

- Um portal de gestão de nuvens.  

- A bordo do site para Azure AD para gestão de nuvens.  

    - Se já preencheu este pré-requisito para o seu site, precisa de atualizar a aplicação Azure AD. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud,** e selecione **Azure Ative Directory Tenants**. Selecione o inquilino Azure AD, selecione a aplicação web no painel **de Aplicações** e, em seguida, clique na definição de **aplicação Update** na fita.  

- Um cliente que executa a versão 1803 do Windows 10 e se juntou ao Azure AD. (Este requisito é tecnicamente apenas para o [Cenário 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione **Sites**. Selecione o site e clique em **Propriedades** na fita.  

2. Mude para o separador comunicação do **computador cliente.** Selecione a opção para **HTTPS ou HTTP** e, em seguida, ative a nova opção de utilizar certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP**.  

Consulte a lista anterior [de cenários](#bkmk_token) para validar.

> [!Tip]
> Neste comunicado, aguarde até 30 minutos para que o ponto de gestão receba e configure o novo certificado a partir do site.

Pode ver estes certificados na consola 'Gestor de Configuração'. Vá ao espaço de trabalho da **Administração,** expanda **a Segurança**e selecione o nó de **Certificados.** Procure o certificado raiz de **emissão SMS,** bem como os certificados de função do servidor do site emitidos pela raiz de emissão SMS.


### <a name="known-issues"></a>Problemas conhecidos
- O utilizador não pode visualizar no Software Center quaisquer aplicações direcionadas para eles como disponíveis.  

- Os cenários de implantação do OS ainda requerem a conta de acesso à rede.  

- Permitir e desativar repetidamente a opção de utilizar certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP** pode fazer com que o certificado não se ligue adequadamente às funções do sistema do site. Nenhum certificado emitido pelo certificado "SMS Esuing" está vinculado a um website nos Serviços de Informação de Internet do Windows Server (IIS). Para resolver este problema, elimine todos os certificados emitidos pela "Emissão SMS" da loja de certificados **SMS** no Windows e, em seguida, reinicie o serviço SMS.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Melhorias para permitir suporte a atualização de software de terceiros
<!--1357605-->
Como resultado do feedback do UserVoice no suporte de atualização de [software de terceiros,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)esta versão iterates ainda mais sobre a integração com system Center Updates Publisher (SCUP). A versão técnica de pré-visualização do Gestor de Configuração [1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) adicionou a capacidade de ler o certificado da WSUS para atualizações de terceiros e, em seguida, implementar esse certificado para os clientes. Mas ainda precisava de usar a ferramenta SCUP para criar e gerir o certificado para a assinatura de atualizações de software de terceiros.

Nesta versão, pode ativar o site do Gestor de Configuração para configurar automaticamente o certificado. O site comunica com a WSUS para gerar um certificado para o efeito. O Gestor de Configuração continua a implementar esse certificado para os clientes. Esta iteração elimina a necessidade de utilizar a ferramenta SCUP para criar e gerir o certificado. 

Para obter mais informações sobre o uso geral da ferramenta SCUP, consulte [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Pré-requisitos
- Ative e implemente a definição do cliente **Ativar atualizações** de software de terceiros no grupo **Deactualizações** de Software.
- Se o WSUS estiver num servidor separado do ponto de atualização do software, deve fazer uma das seguintes opções no servidor WSUS remoto:
    - Ativar o serviço de Registo Remoto no Windows  
    ou
    - Na chave de `HKLM\Software\Microsoft\Update Services\Server\Setup` registo, crie um novo DWORD denominado **EnableSelfSignedCertificates** com um valor de `1` . 

### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **configuração do site** e selecionar **sites**. Selecione o site de nível superior, clique em **Configurar componentes** do site na fita e selecione **Software Update Point**.  

2. Mude para o separador Atualizações de **Terceiros.** Selecione a opção para **ativar atualizações de software de terceiros**e, em seguida, selecione a opção para 'Gestor de **Configuração' gere automaticamente o certificado**.

3. Continue com o resto do fluxo de trabalho típico da SCUP para importar um catálogo de atualização de software de terceiros e, em seguida, implementar as atualizações para os clientes.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade do Windows 10
<!--1358500-->

O modelo de sequência de tarefas padrão para a atualização do Windows 10 inclui agora outro novo grupo com ações recomendadas para adicionar caso o processo de atualização falhe. Estas ações facilitam a resolução de problemas.

### <a name="new-groups-under-run-actions-on-failure"></a>Novos grupos sob **ações de Run sobre o fracasso**
- **Recolher registos**: Para recolher registos do cliente, adicione passos neste grupo. 
    - Uma prática comum é copiar os ficheiros de registo para uma partilha de rede. Para estabelecer esta ligação, utilize o passo [de Ligação à Pasta](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) de Rede. 
    - Para executar a operação de cópia, utilize um script ou utilidade personalizado com a linha de [comando executar](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) ou executar o passo do [Script PowerShell.](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)
    - Os ficheiros a recolher podem incluir os seguintes registos:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Para obter mais informações sobre o setupact.log e outros registos de configuração do Windows, consulte [os ficheiros de registo](/windows/deployment/upgrade/log-files)de configuração do Windows .
    - Para obter mais informações sobre os registos de clientes do Gestor de Configuração, consulte os [registos do cliente do Gestor de Configuração](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)
    - Para obter mais informações sobre _SMSTSLogPath e outras variáveis úteis, consulte [variáveis incorporadas](../../osd/understand/task-sequence-variables.md) na sequência de tarefas

- **Executar ferramentas de diagnóstico**: Para executar ferramentas de diagnóstico adicionais, adicione passos neste grupo. Estas ferramentas devem ser automatizadas para recolher informações adicionais do sistema logo após a falha possível.
    - Uma dessas ferramentas é o Windows [SetupDiag.](/windows/deployment/upgrade/setupdiag) É uma ferramenta de diagnóstico autónoma que pode utilizar para obter detalhes sobre o porquê de uma atualização do Windows 10 não ter sido bem sucedida.
         - No 'Gestor de Configuração', [crie um pacote](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) para a ferramenta.
         - Adicione um passo de Linha de [Comando de Execução](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) a este grupo da sua sequência de tarefas. Utilize a opção **Pacote** para fazer referência à ferramenta. A seguinte corda é uma linha de **comando**exemplo:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace instalado com cliente
<!--1357971-->

A ferramenta de visualização de log CMTrace é agora instalada automaticamente juntamente com o cliente do Gestor de Configuração. É adicionado ao diretório de instalação do cliente, que por padrão é `%WinDir%\ccm\cmtrace.exe` .

> [!Note]  
> O CMTrace *não* está registado automaticamente com o Windows para abrir a extensão do ficheiro .log.



## <a name="improvement-to-the-configuration-manager-console"></a>Melhoria da consola De Configuração Manager
<!--1358202-->
Fizemos a seguinte melhoria na consola do Gestor de Configuração:

- Listas de dispositivos em Ativos e Compliance, Dispositivos, agora por predefinição do visualização do utilizador atualmente registado. Este valor é tão atual como o estatuto do [cliente.](../clients/manage/monitor-clients.md#bkmk_indStatus) O valor é apurado quando o utilizador inicia o loga. Se nenhum utilizador estiver ligado, o valor está em branco. 

### <a name="known-issues"></a>Problemas conhecidos
O valor atualmente registado no valor do utilizador está em branco no nó dos Dispositivos ou ao visualizar uma lista de dispositivos sob o nó de Recolha seletiva do Dispositivo. Para contornar este problema, descarregue este [script SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Execute sp_BgbUpdateLiveData.sql no servidor de base de dados do site e, em seguida, reinicie os serviços smsexec e sms_notification_server no ponto de gestão.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Melhorias no feedback das consolas
<!--1357542-->
Esta versão inclui as seguintes melhorias ao novo mecanismo de [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) na consola Do Gestor de Configuração:  

- O diálogo de feedback agora lembra-se das definições anteriores, tais como as opções selecionadas e o seu endereço de e-mail.  

- Agora suporta feedback offline. Guarde o seu feedback da consola e, em seguida, faça o upload para a Microsoft a partir de um sistema ligado à Internet. Utilize a nova ferramenta de uploader de feedback offline localizada em `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` . Para ver as opções de linha de comando disponíveis e necessárias, execute a ferramenta com a `--help` opção. O sistema conectado precisa de acesso a **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problemas conhecidos
Ao utilizar **Enviar um sorriso** ou enviar uma **franja** da consola numa máquina com conectividade de internet, pode voltar com a seguinte mensagem: "Error envio feedback". Se clicar em **Mais detalhes,** mostra o seguinte texto: `{"Message":""}` . Este erro deve-se a um problema conhecido com a resposta do sistema de feedback backend. Pode descartar o erro. A Microsoft ainda recebeu o seu feedback. (Se os detalhes apresentarem uma mensagem diferente, utilize a opção de feedback offline para voltar a enviar o seu feedback mais tarde.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias nos pontos de distribuição ativados pelo PXE
<!--1357580-->

Esta versão inclui as seguintes melhorias adicionais quando utiliza a opção de [**ativar um serviço de resposta PXE sem o Serviço**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) de Implementação do Windows num ponto de distribuição:  

- As regras do Windows Firewall são criadas automaticamente no ponto de distribuição quando ativar esta opção  
- Melhorias na exploração madeireira de componentes



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Melhoria do inventário de hardware para grandes valores inteiros
<!--1357880-->
O inventário de hardware tem atualmente um limite para inteiros superiores a 4.294.967.296 (2^32). Este limite pode ser atingido para atributos como tamanhos de disco rígido em bytes. O ponto de gestão não processa valores inteiros acima deste limite, pelo que nenhum valor é armazenado na base de dados. Agora, nesta versão, o limite é aumentado para 18.446.744.073.709.551.616 (2^64). 

Para uma propriedade com um valor que não muda, como o tamanho total do disco, você pode não ver imediatamente o valor após a modernização do site. A maioria do inventário de hardware é um relatório delta. O cliente só envia valores que mudam. Para contornar este comportamento, adicione outra propriedade à mesma classe. Esta ação faz com que o cliente atualize todas as propriedades da classe que mudaram. 



## <a name="improvement-to-wsus-maintenance"></a>Melhoria da manutenção da WSUS
<!--1357898-->

O assistente de limpeza WSUS agora recusa atualizações que são expiradas ou superseded de acordo com as regras de supersedência. Estas regras são definidas nas propriedades dos componentes do ponto de atualização do software.

### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **configuração do site** e selecionar **sites**. Selecione o site de nível superior, clique em **Configurar componentes** do site na fita e selecione **Software Update Point**.  

2. Mude para o separador Regras de **Supersedência.** Ative a opção de executar o assistente de **limpeza WSUS**. Especifique o comportamento de supersedência desejado.  

3. Reveja o ficheiro WSyncMgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Melhoria do apoio aos certificados de GNC
<!--1357314-->
Nesta versão, utilize [certificados CNG](../plan-design/network/cng-certificates-overview.md) para as seguintes funções adicionais de servidor escusadoes:  
- Ponto de registo de certificado, incluindo o servidor NDES com o módulo de política do Gestor de Configuração



## <a name="next-steps"></a>Próximos passos
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
