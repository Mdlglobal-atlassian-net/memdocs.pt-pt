---
title: Pré-visualização técnica 1806.2
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de Pré-visualização Técnica 1806.2 do Gestor de Configuração.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 426767b65e0fd770a9a41ce9463948007a524c41
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078758"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1806.2 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1806.2. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

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

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a>Os clientes não atualizam automaticamente
<!--518760-->
Ao atualizar para a versão 1806.2, o site também atualiza o Cliente Nativo SQL, o que pode causar um reinício pendente no servidor do site. Este atraso faz com que certos ficheiros não atualizem, o que afeta a atualização automática do cliente.

#### <a name="workarounds"></a>Soluções
Evite este problema atualizando manualmente o Cliente Nativo SQL antes de *atualizar* o Gestor de Configuração para a versão 1806.2. Para mais informações, consulte a [mais recente atualização de serviço para o SQL Server 2012 Client Nativo](https://www.microsoft.com/download/details.aspx?id=50402).

Se já atualizou o seu site, a atualização automática do cliente e o impulso do cliente não funcionarão. Precisa atualizar os clientes para testar totalmente a maioria das novidades. Atualize manualmente os seus clientes de pré-visualização técnica utilizando o seguinte processo:  

1. Localize os ficheiros de origem do cliente na pasta **CMUClient** do diretório de instalação do Gestor de Configuração no servidor do site. Por exemplo, `C:\Program Files\Configuration Manager\CMUClient`  

2. Copie toda a pasta CMUClient para o dispositivo cliente. Por exemplo, `C:\Temp\CMUClient`  

    Esta localização pode ser uma partilha de rede acessível a partir dos clientes.  

3. Executar a seguinte linha de comando a partir de um pedido de comando elevado:`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Se estiver a instalar um novo cliente no seu site de pré-visualização técnica 1806.2, utilize este mesmo processo. 

> [!Important]  
> Não use o `/MP` parâmetro da linha de comando neste cenário. Este parâmetro tem `/source` prioridade e faz com que a CCMsetup baixe o conteúdo do cliente a partir do ponto de gestão ou ponto de distribuição.
> 
> As propriedades da linha de comando, tais como SMSSITECODE ou CCMLOGLEVEL, estão bem de usar, mas não devem ser necessárias para atualizar um cliente existente. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a>Versão 1806.2 mostra versão 1806 em Cerca de Gestor de Configuração
<!--518148-->
Depois de atualizar para a versão de pré-visualização técnica 1806.2, se abrir a janela **About Configuration Manager** a partir do canto superior esquerdo da consola, ainda mostra a versão **1806**. 

#### <a name="workaround"></a>Solução
Utilize a propriedade da **versão Site** para determinar a diferença entre 1806 e 1806.2:

| Versão do site  | Versão
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a>Melhorias nas implementações faseadas

Esta versão inclui as seguintes melhorias nas [implementações faseadas:](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
- [Estado de implantação faseada](#bkmk_pod-monitor)
- [Implantação faseada de aplicações](#bkmk_pod-app)
- [Lançamento gradual durante implantações faseadas](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a>Estado de implantação faseada
<!--1358577-->
As implementações faseadas têm agora uma experiência de monitorização nativa. A partir do nó de **implantação** no espaço de trabalho **de monitorização,** selecione uma implantação faseada e, em seguida, clique no Estado de **Implantação Faseada** na fita.

![Painel de instrumentos de implantação faseado mostrando o estado de duas fases](media/1358577-phased-deployment-status.png)

Este painel de instrumentos mostra as seguintes informações para cada fase da implantação:  

- **Total de dispositivos**: Quantos dispositivos são alvo desta fase.  

- **Estado**: O estado atual desta fase. Cada fase pode estar num dos seguintes estados:  

    - **Implementação criada**: A implementação faseada criou uma implementação do software para a recolha para esta fase. Os clientes são ativamente direcionados para este software.  

    - **Espera**: A fase anterior ainda não atingiu os critérios de sucesso para que a implantação continue nesta fase.  

    - **Suspenso**: Um administrador suspendeu a implantação.  

- **Progresso**: Os estados de implantação codificados por cores dos clientes. Por exemplo: Sucesso, Progresso, Erro, Requisitos Não Cumpridos e Desconhecidos. 


#### <a name="known-issue"></a>Problema conhecido
O painel de instrumentos de estado de implantação faseado pode apresentar várias linhas para a mesma fase.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a>Implantação faseada de aplicações
<!--1358147-->
Criar implementações faseadas para aplicações. As implementações faseadas permitem-lhe orquestrar um lançamento coordenado e sequenciado de software com base em critérios e grupos personalizáveis.

Na consola de Configuração Manager, vá à Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione **Aplicações.** Selecione uma aplicação e, em seguida, clique em **Criar Implantação Faseada** na fita. 

O comportamento de uma implementação faseada de aplicação é o mesmo que para sequências de tarefas. Para obter mais informações, consulte [Criar implementações faseadas para uma sequência](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)de tarefas .

#### <a name="prerequisite"></a>Pré-requisito
Distribua o conteúdo da aplicação para um ponto de distribuição antes de criar a implementação faseada.<!--518293-->

#### <a name="known-issue"></a>Problema conhecido
Não se pode criar fases manualmente para uma aplicação. O assistente cria automaticamente duas fases para as implementações da aplicação.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a>Lançamento gradual durante implantações faseadas
<!--1358578-->
Durante uma implantação faseada, o lançamento em cada fase pode agora acontecer gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implementação, e diminui a carga na rede causada pela distribuição de conteúdos aos clientes. O site pode gradualmente disponibilizar o software dependendo da configuração para cada fase. Cada cliente numa fase tem um prazo em relação ao tempo que o software é disponibilizado. O intervalo de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. 

Quando criar uma implementação faseada e configurar manualmente uma fase, na página de **Definições** de Fase do Assistente de Fase adicionar, ou na página **definições** do assistente de implementação faseada, configure a opção: **Gradualmente disponibilize este software durante este período de tempo (em dias)**. O valor padrão desta definição é **de 0**, por isso, por padrão, a implantação não é acelerada.

> [!Note]  
> Esta opção está atualmente disponível apenas para implementações faseadas de sequências de tarefas.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a>Suporte para novos formatos de pacotes de aplicativos Windows
<!--1357427-->
O Gestor de Configuração suporta agora a implementação de novos formatos de pacote de aplicações Do Windows 10 (.msix) e pacote de aplicações (.msixbundle). As mais recentes [visualizações](https://insider.windows.com/) do Windows Insider suportam atualmente estes novos formatos.

Para uma visão geral do MSIX, veja [mais de perto o MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Para como criar uma nova aplicação MSIX, consulte o [suporte MSIX introduzido no Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Pré-requisitos
- Um cliente do Windows 10 que executa pelo menos o Windows Insider Preview 17682
- Um pacote de aplicativos Windows no formato MSIX

### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola 'Gestor de Configuração', [crie uma aplicação](../../apps/deploy-use/create-applications.md). 
2. Selecione o ficheiro de instalação de aplicação **Type** as **Windows app package\*( .appx, \*.appxbundle, \*.msix, \*.msixbundle)**.
3. [Implemente a aplicação](../../apps/deploy-use/deploy-applications.md) para o cliente que executa a mais recente construção de Pré-visualização do Windows Insider.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a>Melhoria da segurança do impulso do cliente
<!--1358204-->
Ao utilizar o método de pressão do [cliente](../clients/deploy/plan/client-installation-methods.md#client-push-installation) para instalar o cliente Do Gestor de Configuração, o servidor do site cria uma ligação remota ao cliente para iniciar a instalação. A partir desta versão, o site pode exigir a autenticação mútua kerberos, não permitindo o recuo à NTLM antes de estabelecer a ligação. Esta melhoria ajuda a garantir a comunicação entre o servidor e o cliente. 

Dependendo das suas políticas de segurança, o seu ambiente pode já preferir ou exigir a Kerberos em vez da autenticação NTLM mais antiga. Para obter mais informações sobre as considerações de segurança destes protocolos de autenticação, consulte a definição da política de [segurança do Windows para restringir a NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Pré-requisito

Para utilizar esta funcionalidade, os clientes devem estar numa floresta de Diretório Ativo de confiança. Kerberos no Windows conta com o Diretório Ativo para autenticação mútua. 


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

Ao atualizar o site, o comportamento existente persiste. Assim que *abrir* as propriedades de instalação push do cliente, o site permite automaticamente a verificação Kerberos. Se necessário, pode permitir que a ligação recue para utilizar uma ligação NTLM menos segura, o que não é recomendado. 

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione **Sites**. Selecione o local do alvo. Na fita, clique em Definições de **Instalação do Cliente** e selecione **Instalação de impulso do cliente**.  

2. O site já permitiu que os Kerberos verificassem o impulso do cliente. Clique em **OK** para fechar a janela.  

3. Se necessário para o seu ambiente, na janela Propriedades de Instalação de Impulso do Cliente, no separador **Geral,** consulte a opção de permitir a queda de **ligação à NTLM**. Esta opção está desativada por predefinição. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a>Insights de gestão para manutenção proativa
<!--1352184,et al-->
Neste lançamento estão disponíveis insights de gestão adicionais para destacar potenciais problemas de configuração. Reveja as seguintes regras no novo grupo proactivo de **manutenção:**  

- Itens de **configuração não utilizados**: Itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias.  

- **Imagens**de arranque não utilizadas : Imagens de arranque não referenciadas para a utilização da bota PXE ou da sequência de tarefas.  

- **Grupos de fronteira sem sistemas**de site atribuídos : Sem sistemas de site atribuídos, os grupos de fronteira só podem ser utilizados para a atribuição do local.  

- **Grupos de fronteira sem membros**: Os grupos de fronteira não são aplicáveis para a atribuição do site ou procura de conteúdo se não tiverem membros.  

- **Pontos**de distribuição não servindo conteúdo aos clientes : Pontos de distribuição que não serviram conteúdo aos clientes nos últimos 30 dias. Estes dados baseiam-se em relatórios de clientes do seu histórico de descarregamento.  

- **Atualizações expiradas encontradas**: As atualizações expiradas não são aplicáveis à implementação.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a>Carga de trabalho de aplicativos móveis de transição para dispositivos cogeridos
<!--1357892-->
Gerencie aplicações móveis com o Microsoft Intune enquanto continua a utilizar o Configuração Manager para implementar aplicações de ambiente de trabalho do Windows. Para fazer a transição da carga de trabalho das aplicações modernas, vá à página de propriedades de cogestão. Mova a barra de slider do Gestor de Configuração para Pilot ou All. 

Após a transição desta carga de trabalho, todas as aplicações disponíveis implantadas a partir de Intune estão disponíveis no Portal da Empresa. As aplicações que implementa no 'Gestor de Configuração' estão disponíveis no Software Center. 

Para obter mais informações, veja os artigos seguintes:  

- [Cogestão para os dispositivos com Windows 10](../../comanage/overview.md)  

- [What is Microsoft Intune app management?](https://docs.microsoft.com/intune/app-management) (O que é a gestão de aplicações do Microsoft Intune)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Opções de grupo de limites para downloads de pares
<!--1356193-->
Os grupos de fronteira saem agora de definições adicionais para lhe dar mais controlo sobre a distribuição de conteúdos no seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir transferências de pares neste grupo de limites**: Esta definição está ativada por defeito. O ponto de gestão fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Existem dois cenários comuns em que deve considerar a desativação desta opção:  

    - Se tiver um grupo de fronteiras que inclua limites de locais geograficamente dispersos, como uma VPN. Dois clientes podem estar no mesmo grupo de fronteiraporque estão ligados através da VPN, mas em locais muito diferentes que são inadequados para a partilha de conteúdos pelos pares.  

    - Se utilizar um único grupo de limites para a atribuição do site que não referencia pontos de distribuição.  

- **Durante os downloads dos pares, utilize apenas pares dentro da mesma sub-rede**: Esta definição depende da acima. Se ativar esta opção, o ponto de gestão apenas inclui na lista de dados de conteúdo fontes de pares que estão na mesma sub-rede que o cliente.

    Cenários comuns para permitir esta opção:

    - O design do seu grupo de fronteira para distribuição de conteúdos inclui um grande grupo de fronteiras que se sobrepõe a outros grupos de fronteira menores. Com esta nova configuração, a lista de fontes de conteúdo que o ponto de gestão fornece aos clientes apenas inclui fontes par imediadas da mesma subnet.

    - Você tem um único grande grupo de fronteiras para todos os locais de escritório remoto. Ative esta opção e os clientes só partilham conteúdo dentro da sub-rede no local do escritório remoto, em vez de arriscarem partilhar conteúdo entre locais.


### <a name="known-issue"></a>Problema conhecido
Se o cliente de origem de pares tiver mais de um endereço IP (IPv4, IPv6, ou ambos), então o caching dos pares não funciona. A nova opção, Durante os **downloads por pares, utilize apenas pares dentro da mesma sub-rede,** não tem efeito se a fonte de pares tiver mais de um endereço IP.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a>Suporte de atualizações de software de terceiros para catálogos personalizados
<!--1358714-->
Esta versão iterates ainda mais no suporte para atualizações de software de terceiros como resultado do feedback do [UtilizadorVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [A versão de pré-visualização técnica 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) forneceu suporte para catálogos de *parceiros,* que são catálogos registados de fornecedores de software. Os catálogos que fornece, que não estão registados na Microsoft, são *chamados catálogos personalizados.* Adicione catálogos personalizados na consola 'Gestor de Configuração'.  


### <a name="prerequisites"></a>Pré-requisitos 

- Configurar [atualizações de software de terceiros.](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) Fase completa 1: Ativar e configurar a função.   

- Um catálogo personalizado assinado digitalmente que contém atualizações de software assinadas digitalmente.  

- O administrador requer as seguintes permissões:  

    - Site: Criar, Modificar  


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Então envie [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) para nos dizer como funcionou.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e selecione o nó de **Catálogos de Atualizações de Software de Terceiros.** Clique em **Adicionar Catálogo Personalizado** na fita.  

2. Na página **Geral,** especifique os seguintes detalhes:  

    - **Baixar URL**: Um endereço HTTPS válido do catálogo personalizado.  

    - **Editor**: O nome da organização que publica o catálogo.  

    - **Nome**: O nome do catálogo a exibir na consola 'Gestor de Configuração'.  

    - **Descrição**: Uma descrição do catálogo.  

    - **URL** de suporte (Opcional): Um endereço HTTPS válido de um website para obter ajuda com o catálogo.  

    - **Contacto de Suporte** (Opcional): Informações de contacto para obter ajuda com o catálogo.  

3. Conclua o assistente. O assistente adiciona o novo catálogo num estado sem subscrição.  

4. Subscreva o catálogo personalizado utilizando a ação **subscrito para catálogo** existente. Para mais informações, consulte [a Fase 2: Subscreva um catálogo de terceiros e atualizações de sincronização.](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates)  

> [!Note]  
> Não pode adicionar catálogos com o mesmo URL de download, e não pode editar propriedades de catálogo. Se especificar propriedades incorretas para um catálogo personalizado, elimine o catálogo antes de o adicionar novamente.  


#### <a name="unsubscribe-from-a-catalog"></a>Cancelar a subscrição de um catálogo
Para cancelar a subscrição de um catálogo, selecione o catálogo pretendido na lista e clique em Cancelar a **subscrição** do Catálogo na fita. Se cancelar a subscrição de um catálogo, ocorrem as seguintes ações e comportamentos: 
- O site para a sincronização de novas atualizações 
- O site bloqueia os certificados associados para a assinatura e atualização do catálogo. 
- As atualizações existentes não são removidas, mas pode não ser capaz de publicá-las ou implantá-las.

#### <a name="delete-a-custom-catalog"></a>Eliminar um catálogo personalizado
Elimine catálogos personalizados do mesmo nó da consola. Selecione um catálogo personalizado num estado *sem subscrição* e clique em Eliminar catálogo **personalizado**. Se já subscreveu o catálogo, cancele primeiro a subscrição antes de o apagar. Não pode excluir catálogos de parceiros. A eliminação de um catálogo personalizado remove-o da lista de catálogos. Esta ação não afeta quaisquer atualizações de software que publicou no seu ponto de atualização de software.


### <a name="known-issue"></a>Problema conhecido
A ação de exclusão em catálogos personalizados está acinzentada, pelo que não é possível eliminar catálogos personalizados da consola. Para contornar este problema, utilize a ferramenta **mais wbemtest** no servidor do site. Consulta por exemplo que pretende eliminar com o nome ou `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`baixar URL, por exemplo: . Na janela de resultados da consulta, selecione o objeto e clique em **Eliminar**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a>Melhorias nas funcionalidades de gestão de nuvem

Esta versão inclui as seguintes melhorias:  

- As seguintes funcionalidades agora apoiam o uso da Nuvem governamental azure dos EUA:<!--511980-->  

    - Onboarding no site para **Cloud Management** através [dos Serviços Azure](../servers/deploy/configure/azure-services-wizard.md)  

    - Implementação de um portal de gestão de nuvem com o Gestor de [Recursos Azure](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Implantação de um ponto de distribuição em nuvem com o Gestor de [Recursos Azure](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Os clientes estão a utilizar o Windows AutoPilot para fornecer o Windows 10 em dispositivos ligados ao Azure Ative Directory que estão ligados à rede no local. Para instalar ou atualizar o cliente do Gestor de Configuração nestes dispositivos, agora não precisa de um ponto de distribuição em nuvem ou de ponto de distribuição no local configurado para **permitir aos clientes a ligação de forma anónima**. Em vez disso, ative a opção do site de utilizar certificados gerados pelo Gestor de **Configuração para sistemas**de site HTTP, o que permite a um cliente ligado ao domínio em nuvem comunicar com um ponto de distribuição ativado pelo HTTP no local. Para mais informações, consulte [Melhoria das comunicações seguras do cliente](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a>Novo relatório de conformidade atualiza atualizações de software
<!--1357775-->
Ver relatórios para atualizações de software a conformidade tradicionalmente inclui dados de clientes que não contactaram recentemente o site. Um novo relatório permite filtrar os resultados de conformidade de um grupo específico de atualização de software por clientes "saudáveis". Este relatório mostra o estado de conformidade mais realista dos clientes ativos no seu ambiente. 
 
Para visualizar o relatório, vá ao espaço de trabalho **de Monitorização,** expanda **relatórios,** expanda **Relatórios,** expanda As Atualizações de Software - A Compliance , e selecione **Compliance 9 - Saúde geral e conformidade.** **Reports** Especifique o **Grupo de Atualização,** **Nome de Recolha**e Estado de **Saúde do Cliente.**

O relatório inclui as seguintes partes:
- **Clientes Saudáveis vs Clientes Totais**: Este gráfico de barras compara os clientes "saudáveis" que comunicaram com o site no período de tempo especificado com o número total de clientes na coleção especificada.
- **Visão geral de conformidade**: Este gráfico de tartes mostra o estado de conformidade geral para o grupo específico de atualização de software sobre clientes ativos na coleção especificada.
- **Top 5 Não Conforme pelo ID do artigo**: Este gráfico de barras apresenta as cinco principais atualizações de software do grupo especificado que não são compatíveis com clientes ativos na recolha especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
