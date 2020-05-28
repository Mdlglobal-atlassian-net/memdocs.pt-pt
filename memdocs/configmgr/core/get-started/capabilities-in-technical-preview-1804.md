---
title: Pré-visualização técnica 1804
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de Pré-visualização Técnica do Gestor de Configuração 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b709d6ec0c0cda188502c314d945a70e8de71288
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905257"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1804 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1804. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja o artigo [de Pré-visualização Técnica](technical-preview.md) antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Questões Conhecidas nesta Pré-Visualização Técnica

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a>Configurar link para descarregar atualizações que não funcionam
<!--514334-->
Se executar a configuração a partir dos meios de comunicação, a página inicial inclui um link intitulado **Get the latest Configuration Manager updates**, que não funciona neste lançamento. Este link destina-se a descarregar os ficheiros necessários para configuração.

#### <a name="workaround"></a>Solução
Para descarregar os ficheiros necessários para configuração, execute o assistente de configuração. Na página Descarregamentos pré-requisito, utilize a opção de **descarregar ficheiros necessários**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a>O ponto de serviço web do catálogo de aplicações não pode ser ativado por HTTPS
<!--512637-->
Se o ponto de serviço web do catálogo de aplicações estiver ativado por HTTPS:

- Aplicações implementadas como disponíveis para utilizadores não aparecem no Centro de Software  

- O seguinte erro mostra no awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solução
Reconfigurar o ponto de serviço web do catálogo de aplicações para comunicar utilizando ligações HTTP.  




</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configure uma biblioteca de conteúdos remotos para o servidor do site  
<!--1357525-->
Para libertar espaço de disco rígido no servidor do seu site principal, desloque a sua biblioteca de [conteúdos](../plan-design/hierarchy/the-content-library.md) para outro local de armazenamento. Pode mover a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerantes a falhas numa rede de área de armazenamento (SAN). Recomendamos um SAN pois fornece armazenamento elástico que cresce ou encolhe ao longo do tempo para satisfazer os seus requisitos de conteúdo em mudança. 

Esta biblioteca de conteúdos remotos é um novo pré-requisito para a elevada disponibilidade do servidor do [site.](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) 

> [!Note]  
> Esta ação apenas move a biblioteca de conteúdos no servidor do site. Não afeta a localização da biblioteca de conteúdos nos pontos de distribuição. 

### <a name="prerequisites"></a>Pré-requisitos  
- A conta de computador do servidor do site precisa de **ser lida** e **de escrever** permissões para o caminho da rede para o qual está a mover a biblioteca de conteúdos. Não são instalados componentes no sistema remoto. 

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](#bkmk_feedback) para nos dizer como funcionou.

1. Na consola 'Gestor de Configuração', mude para o espaço de trabalho da **Administração.** Expandir a **configuração do site** e selecionar **sites**. No separador **Resumo** na parte inferior do painel de detalhes, note uma nova coluna para a **Biblioteca de Conteúdos**.  

2. Clique em Gerir a biblioteca de **conteúdos** na fita.  

3. Selecione **numa partilha de rede** e introduza um caminho de rede válido. Este caminho é o local para onde o site move a biblioteca de conteúdos. Clique em **OK**.  

4. Note a propriedade **Status** na coluna da Biblioteca de Conteúdos no painel de detalhes. Atualiza para mostrar o progresso do site na mudança da biblioteca de conteúdos. Quando em curso exibe a percentagem completa. Se houver um estado de erro, exibe o erro. Erros comuns incluem `access denied` ou `disk full` . Quando estiver concluído, exibe `OK` . Consulte o **distmgr.log** para obter mais detalhes. Para mais informações, consulte os [registos](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog)do servidor do servidor do Site e do servidor do site .  

Se precisar de mover a biblioteca de conteúdos de volta para o servidor do site, repita este processo, mas selecione a opção **Local para o servidor do site**.  

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, utilize a ferramenta de transferência da **Biblioteca de Conteúdos.** Para mais informações, consulte [Configuração Manager Toolkit](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a>Enviar feedback da consola 'Gestor de Configuração'  
<!--1357542-->

Mande um sorriso! Já pode contar diretamente à equipa do Gestor de Configuração as suas experiências. Enviar feedback é fácil a partir da consola 'Gestor de Configuração'. Queremos ouvir todo o seu feedback: louvor, problemas e sugestões.  

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie **feedback** para nos dizer como funcionou.  

1. Na consola 'Gestor de Configuração', clique no botão de sorriso no canto superior direito acima da fita.  

2. A partir da lista de lançamentos, selecione uma das opções disponíveis:  

   - **Envie um sorriso:** Gostou mesmo de algo! Para esta opção, insira os detalhes do seu feedback. Em seguida, opcionalmente inclua uma imagem e o seu endereço de e-mail.  

   - **Envie uma testa:** Encontrou um problema na consola, ou algo não funcionou como esperado. Para esta opção, introduza os detalhes da potencial questão do produto. Em seguida, opcionalmente inclua uma imagem, o seu endereço de e-mail e dados de diagnóstico.  

   - **Envie uma sugestão:** Tem uma ideia para alterar e melhorar o Gestor de Configuração. Esta opção abre o nosso site [UserVoice](https://configurationmanager.uservoice.com) no seu navegador web.  

Este feedback vai diretamente para a equipa de produtos da Microsoft para O Gestor de Configuração. Enquanto a utilização do Hub de Feedback do Windows 10 ainda é suportada, é sucudedo a utilização do mecanismo de feedback na consola.  

As seguintes informações anónimas são sempre incluídas com o feedback para o contexto:  

- Versão e idioma da consola do Gestor de Configuração  

- Versão do site do Gestor de Configuração  

- Id de suporte, também conhecido como id da hierarquia  

- Versão osso e idioma para o sistema em que a consola está a funcionar  

- A localização exata na consola a partir da qual clicou no sorriso  

Estes dados são consistentes com a recolha dos nossos dados de diagnóstico e utilização. Para mais informações, consulte [Diagnósticos e dados de utilização](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Problemas conhecidos

Se tentar enviar feedback de um dispositivo que não seja capaz de aceder à internet, a aplicação pode fechar inesperadamente. Para enviar um sorriso ou franzir a testa, certifique-se de que o dispositivo é capaz de aceder petrol.office.microsoft.com.



## <a name="support-center"></a>Centro de Suporte
<!--1357489-->

Utilize o Centro de Suporte para resolução de problemas do cliente, visualização de registoem em tempo real ou capturando o estado de um computador cliente do Gestor de Configuração para posterior análise. O Centro de Suporte é uma única ferramenta para consolidar muitas ferramentas de resolução de problemas do administrador. Uma pré-visualização da versão mais recente do Support Center com correções de bugs, melhorias e uma pré-visualização do nosso novo observador de registos está disponível na pré-visualização técnica. Encontre o instalador do Centro de Suporte no servidor do site na pasta **cd.latest\SMSSETUP\Tools\SupportCenter.**


### <a name="new-support-center-features"></a>Novas funcionalidades do Centro de Suporte  

- Um novo espectador de registos, oneTrace. Funciona semelhante ao CMTrace, e inclui melhorias como uma vista para acamado e janelas dockable.  

- Uma nova funcionalidade de recolha de dados reúne registos de diagnóstico do cliente local ou remoto do Gestor de Configuração. Fornece diagnóstico em tempo real de inventário (substitui O Espião do Cliente), política (substitui Policy Spy) e cache do cliente.  



## <a name="configuration-manager-toolkit"></a>Kit de ferramentas de gestor de configuração
<!--1357145-->

O servidor do Gestor de Configuração e as ferramentas do cliente estão agora incluídos na pré-visualização técnica. Encontre-os na pasta **cd.latest\SMSSETUP\Tools** no servidor do site. Não é necessária mais nenhuma instalação.

#### <a name="server-tools"></a>Ferramentas de servidor  

- **DP Job Manager**: Troubleshoots empregos de distribuição de conteúdos para pontos de distribuição  

- **Avaliação de avaliação de recolha Espectador**: Ver detalhes da avaliação da coleção  

- **Explorador de Biblioteca**de Conteúdos : Ver conteúdos da loja de instâncias únicas da biblioteca de conteúdos  

- **Transferência da Biblioteca de Conteúdos**: Transfere biblioteca de conteúdos entre unidades  

- **Ferramenta de propriedade de conteúdo**: Altera a propriedade de pacotes órfãos. Estes pacotes existem no site sem um servidor de site próprio.  

- **Ferramenta de Administração e Auditoria baseada em funções**: Ajuda administradores a auditar funções  

#### <a name="client-tools"></a>Ferramentas de cliente

- **CMTrace**: Ver registos  

- **Ferramenta de monitorização**de implementação : Aplicações de resolução de problemas, atualizações e implementações de base  

- **Policy Spy**: Ver atribuições políticas  

- **Ferramenta power viewer**: Ver estado da funcionalidade de gestão de energia  

- **Ferramenta de envio**de horários : Horários de disparo e avaliações das linhas de base do DCM  

> [!Important]  
> [O Centro](#support-center) de Suporte é recomendado para a maioria dos casos de utilização, uma vez que inclui a mesma funcionalidade ou melhor a funcionalidade para as seguintes ferramentas:  
> - Espião do Cliente
> - CMTrace<sup>1</sup> 
> - Ferramenta de Monitorização da Implementação
> - Espião de Política
> - Ferramenta de Envio de Agendamento
> 
> <sup>1</sup> CMTrace não depende de .NET ou Windows Presentation Foundation (WPF), pelo que ainda é utilizado em imagens de arranque do Windows PE.

### <a name="known-issues"></a>Problemas conhecidos
Algumas ferramentas de cliente e servidor podem sair inesperadamente no lançamento. Esta questão deve-se a um ficheiro em falta nos meios de comunicação. Como uma sucinta, copie o ficheiro **Microsoft.Diagnostics.Tracing.EventSource.dll** do diretório AdminConsole\bin em ambos os diretórios SMSSETUP\Tools\ClientTools e ServerTools. Este ficheiro deve ser a mesma versão utilizada pela consola 'Gestor de Configuração'. Outras versões podem não funcionar. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Desinstalar aplicação na revogação da aprovação
<!--1357891-->

O comportamento mudou quando revoga a aprovação de uma candidatura. Agora, quando nega o pedido para a aplicação, o cliente desinstala a aplicação a partir do dispositivo do utilizador. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar a funcionalidade Aprovar pedidos de **aplicação para utilizadores por dispositivo**.

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](#bkmk_feedback) para nos dizer como funcionou.

1. Na consola 'Gestor de Configuração', desloque para um utilizador uma aplicação que necessite de aprovação. No separador **Definições** de Implementação da implementação, ative a opção **Um administrador deve aprovar um pedido para esta aplicação no dispositivo**.  

2. No cliente do Gestor de Configuração no Centro de Software, o utilizador solicita a aprovação para instalar a aplicação.  

3. Na consola 'Gestor de Configuração', aprove o pedido para que este utilizador instale a aplicação no dispositivo. Os pedidos de aprovação de candidaturas são apresentados no espaço de trabalho da Biblioteca de **Software,** no âmbito da Gestão de **Aplicações,** no nó **de Pedidos de Aprovação.**  

4. No cliente do Software Center, o utilizador instala a aplicação.  

5. Na consola 'Gestor de Configuração', negue o pedido do utilizador para a aplicação no dispositivo.  

### <a name="known-issues"></a>Problemas conhecidos
- Depois de o utilizador instalar a aplicação no cliente, atualize a política do utilizador. No Centro de Software, altere para o separador **Opções,** expanda a **manutenção do Computador** e clique em Política de **Sincronização**.<!--480609-->  

- O ponto de serviço web do catálogo de aplicações deve ser HTTP. Para mais informações, consulte [questões conhecidas nesta pré-visualização técnica](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Excluir recipientes de Diretório Ativo da descoberta
<!--1358143-->
Para reduzir o número de objetos descobertos, pode agora excluir recipientes específicos da descoberta do sistema de Diretório Ativo. Esta funcionalidade é o resultado do feedback do [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](#bkmk_feedback) para nos dizer como funcionou.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **a Configuração da Hierarquia** e selecionar **métodos de descoberta.** Selecione **Ative Directory System Discovery** e clique em **Propriedades** na fita.  

2. Clique no novo ícone para especificar um novo recipiente de Diretório Ativo.   

3. Na caixa de diálogo do Recipiente de Diretório Ativo, navegue para ou entre no **Caminho** da secção Localização para iniciar a descoberta.  

4. Na secção Opções de Pesquisa, ative a opção de **procurar recursivamente recipientes para crianças do Diretório Ativo**. Em seguida, clique em **Adicionar** para selecionar subrecipientes para serem excluídos desta descoberta.  

5. Na caixa de diálogo Select New Container, selecione um recipiente para crianças para excluir. Clique **em OK** para fechar a caixa de diálogo Select New Container.  

6. Clique **em OK** para fechar a caixa de diálogo do Recipiente de Diretório Ativo.  

7. Na janela Ative Directory System Discovery Properties, veja o caminho do recipiente Ative Directory no qual a descoberta começa. A coluna **Recursiva** mostra **Sim,** e a nova coluna **Has Exclusions** também mostra **Sim.** Clique **em OK** para fechar a janela Ative Directory System Discovery Properties.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especifique a visibilidade do link do site do Catálogo de Aplicações no Centro de Software
<!--1358214-->

Agora pode controlar se o link para Abrir o site do Catálogo de **Aplicações** aparece no nó de estado de **instalação** do Software Center.  

> [!Note]  
> O suporte para a experiência do utilizador do catálogo de aplicações termina com a primeira atualização lançada após 1 de junho de 2018. Para mais informações, consulte [funcionalidades removidas e depreciadas](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Então envie [feedback](#bkmk_feedback) para nos dizer como funcionou.

1. Na consola de Configuração Manager, espaço de trabalho **de Administração,** nó de Definições de **Cliente,** crie uma política personalizada de definições de dispositivos de cliente.  

2. Selecione o grupo **Software Center.**  

3. Para **configurações do Centro de Software,** clique em **Personalizar**.  

4. Ative a opção **de ocultar o link do site do Catálogo de Aplicações no Centro**de Software .   

Para obter mais informações sobre as definições do cliente, consulte as definições do [cliente Configurar](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implementação automática pela arquitetura de atualização de software
 <!--1322266-->
Agora pode filtrar regras de implementação automáticas para excluir arquiteturas como Itanium e ARM64.

### <a name="try-it-out"></a>Experimente!
Tente completar as tarefas. Então envie [feedback](#bkmk_feedback) para nos dizer como funcionou.

1. Na consola Do Gestor de Configuração, mude para o espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações** de software e selecionar **regras de implementação automáticas**. Na fita, selecione Criar regra de **implantação automática**.  

2. Preencha as definições apropriadas para o separador **Geral** e o separador Definições de **Implementação.**  

3. No separador Atualizações de **Software,** selecione **Arquitetura** e, em seguida, clique em itens para encontrar nos **critérios** de **Pesquisa**.  

4. Selecione as arquiteturas que pretende incluir na regra de implementação automática.  

5. Clique em **Seguinte** e prossiga com a criação da regra de implementação automática.  

> [!IMPORTANT]  
> Lembre-se que existem aplicações e componentes de 32 bits (x86) em execução em sistemas de 64 bits (x64). A menos que tenha certeza de que não precisa de x86, também o ative quando escolher x64.  

### <a name="known-issues"></a>Problemas conhecidos
Depois de adicionar os critérios de arquitetura, a página de propriedades da regra de implementação automática mostra **título** nos critérios de pesquisa. A regra de implementação automática ainda funciona como esperado e seleciona as atualizações de software corretas. No entanto, não pode incluir os critérios de **Arquitetura** e **Título** neste momento. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Melhorias na implantação do OS
Fizemos as seguintes melhorias na implementação do OS, algumas das quais foram o resultado do feedback de voz do utilizador.  

- [Máscara dados sensíveis armazenados em variáveis](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed)de sequência de tarefas : Na sequência de [tarefas definidas passo variável,](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) selecione a nova opção para **não exibir este valor**. Por exemplo, ao especificar uma palavra-passe.<!--1358330--> Os seguintes comportamentos aplicam-se quando ativa esta opção:
  - O valor da variável não é mostrado em smsts.log.
  - A consola do Gestor de Configuração e o Fornecedor SMS lidam com este valor da mesma forma que outros segredos, tais como palavras-passe.
  - O valor não está incluído quando se exporta a sequência de tarefas.
  - O editor da sequência de tarefas não lê este valor quando edita o passo. Reescreva todo o valor para fazer alterações.

  > [!Important]  
  > As variáveis e os seus valores são guardados com a sequência de tarefas como XML, e obfuscados na base de dados. Quando o cliente solicita uma política de sequência de tarefas a partir do ponto de gestão, é encriptado em trânsito e quando armazenado no cliente. No entanto, todos os valores variáveis são texto simples no ambiente de sequência de tarefas na memória durante o tempo de execução do cliente. Se a sequência de tarefas incluir um passo para obter o valor da variável, esta saída encontra-se em texto simples. Este comportamento requer uma ação explícita do administrador para incluir tal passo na sequência de tarefas. 


- Nome do [programa de máscaras durante a sequência de comando de execução](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Para evitar que os dados potencialmente sensíveis sejam exibidos ou registados, detete a variável de sequência de tarefas **OSDDoNotLogCommand para** `TRUE` . Esta variável disfarça o nome do programa [Run Command Line](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) no smsts.log durante um passo de sequência de tarefa smsts.log. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias na consola do Gestor de Configuração
- A informação principal do utilizador é agora visível ao visualizar os membros de uma coleção ao abrigo de **Ativos e Compliance,** **Recolhas de Dispositivos.**<!--510252-->  



## <a name="next-steps"></a>Próximos passos
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
