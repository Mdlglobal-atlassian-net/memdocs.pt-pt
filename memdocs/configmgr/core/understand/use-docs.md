---
title: Como utilizar a documentação
titleSuffix: Configuration Manager
description: Saiba dicas sobre a utilização da biblioteca de documentação técnica do Gestor de Configuração.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d694f9985e6d1e5118f2620e5cbd556de249788a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771320"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Como utilizar os docs do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece recursos e dicas para a utilização da biblioteca de documentação do Gestor de Configuração.

- Como pesquisar
- Submeter bugs do c., melhorias, perguntas e novas ideias
- Como ser notificado das alterações
- Como contribuir para os docs

Para obter ajuda geral com o produto, consulte [Encontrar ajuda.](find-help.md)

## <a name="search"></a><a name="bkmk_searchtips"></a>Pesquisar

Utilize as seguintes sugestões de procura para localizar as informações de que necessita:

- Ao utilizar o seu motor de pesquisa `ConfigMgr` preferido para localizar conteúdo para 'Gestor de Configuração', inclua juntamente com as suas palavras-chave de pesquisa.

  - Procure resultados `docs.microsoft.com/configmgr` da filial atual do Gestor de Configuração. Os `docs.microsoft.com/previous-versions` resultados são para versões de produtos mais antigas.

  - Para focar ainda mais os resultados `site:docs.microsoft.com` da pesquisa na biblioteca de conteúdos atuais, inclua o scope do motor de busca.

- Utilize termos de pesquisa que correspondam à terminologia na interface do utilizador e documentação online. Evite termos ou abreviaturas não oficiais que possa ver em conteúdos comunitários. Por exemplo, procure:

  - "ponto de gestão" em vez de "MP"
  - "Tipo de implantação" em vez de "DT"
  - "atualizações de software" em vez de "SUM"

- Para pesquisar dentro do artigo atual, use a funcionalidade **Find** do seu navegador. Com a maioria dos navegadores web modernos, prima **Ctrl**+**F** e, em seguida, insira os seus termos de pesquisa.

- Cada artigo `docs.microsoft.com` sobre inclui os seguintes campos para ajudar na pesquisa do conteúdo:

  - **Procure** no canto superior direito. Para pesquisar todos os artigos, insira os termos neste campo. Os artigos na biblioteca do `ConfigMgr` Gestor de Configuração incluem automaticamente o âmbito de pesquisa desta biblioteca de documentação.

  - **Filtrar por título** acima da tabela esquerda do conteúdo. Para pesquisar a tabela atual de conteúdos, insira os termos neste campo. Este campo apenas corresponde aos termos que aparecem nos títulos do artigo para o nó atual. Por exemplo, **Infraestrutura Central** (`docs.microsoft.com/configmgr/core`) ou Gestão de **Aplicações** ().`docs.microsoft.com/configmgr/apps`

- Tem problemas em encontrar alguma coisa? [Feedback do arquivo!](#bkmk_docfeedback) Ao arquivar o problema, forneça o motor de busca que está a usar, as palavras-chave que tentou e o artigo-alvo. Este feedback ajuda a Microsoft a otimizar o conteúdo para uma melhor pesquisa.

> [!TIP]
> Começando na versão 1902 do Gestor de Configuração, há um nó de **Documentação** no novo espaço de trabalho **comunitário** da consola Do Gestor de Configuração. Este nó inclui informações atualizadas sobre documentação do Gestor de Configuração e artigos de suporte. Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../servers/manage/admin-console.md#bkmk_doc-dashboard)

## <a name="feedback"></a><a name="bkmk_docfeedback"></a>Feedback

Selecione o link **Feedback** no direito superior de qualquer artigo para ir à secção de Feedback na parte inferior. Esta secção integra-se com as Questões GitHub. Para obter mais informações sobre integração com as Questões GitHub, consulte o post de blog da [plataforma docs.](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs)

Para partilhar feedback sobre o próprio produto Do Gestor de Configuração, selecione feedback do **Produto**. Para mais informações, consulte o [feedback do Produto.](find-help.md#product-feedback)

Uma [conta GitHub](https://github.com/join) é um pré-requisito para fornecer feedback de documentação. Assim que se inscreveu, há uma autorização única para a organização do MicrosoftDocs. Em seguida, quando selecionar **o feedback do Conteúdo,** insira um título e comente e, em seguida, **submeta feedback**. Esta ação apresenta uma nova emissão para o artigo-alvo no [repositório SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Esta integração também exibe quaisquer questões abertas ou fechadas existentes para o artigo-alvo. Se houver, reveja-os antes de apresentar uma nova emissão. Se encontrar um problema relacionado, selecione o ícone facial para adicionar uma reação, ou pode expandi-lo para adicionar um comentário.

#### <a name="types-of-feedback"></a>Tipos de feedback

Utilize problemas gitHub para submeter os seguintes tipos de feedback:

- Bug do doc: O conteúdo está desatualizado, pouco claro, confuso ou quebrado.
- Melhoria do doc: Uma sugestão para melhorar o artigo.
- Pergunta do doc: Você precisa de ajuda para encontrar documentação existente.
- Ideia do doc: Uma sugestão para um novo artigo. Utilize este método em vez do UserVoice para obter feedback de documentação.
- Kudos: Feedback positivo sobre um artigo útil ou informativo!
- Localização: Feedback sobre tradução de conteúdo.
- Otimização do motor de busca (SEO): Feedback sobre problemas à procura de conteúdo. Inclua o motor de busca, palavras-chave e artigo de destino nos comentários.

Se criar um problema para temas não relacionados com o doc, a Microsoft encerrará os problemas. Por exemplo:

- [Feedback do produto](find-help.md#product-feedback)
- [Questões de produtos](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Pedidos de suporte](https://aka.ms/cmcbsupport)

Para partilhar feedback na plataforma fundamental docs.microsoft.com, consulte o [feedback do Docs](https://aka.ms/sitefeedback). A plataforma inclui todos os componentes do invólucro, tais como o cabeçalho, tabela de conteúdos e menu direito. Também como os artigos são render izados no navegador, como a fonte, caixas de alerta e âncoras de página.

## <a name="notifications"></a><a name="bkmk_notifications"></a>Notificações

Para receber notificações quando o conteúdo mudar na biblioteca de documentação, utilize os seguintes passos:

1. Utilize a pesquisa dos [médicos](https://docs.microsoft.com/search/index?scope=ConfigMgr) para encontrar um artigo ou conjunto de artigos. Por exemplo:

    - Procure um único artigo por título, ["Ficheiros de registo para resolução de problemas - Gestor de Configuração"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Pesquisar por qualquer artigo sobre [o SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. No canto superior direito, selecione a ligação **RSS.**

3. Utilize este feed em qualquer aplicação RSS para receber notificações quando houver uma alteração em qualquer um dos resultados da pesquisa.

> [!TIP]
> Também pode **assistir** ao [repositório SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) no GitHub. Este método gera muitas notificações. Também não inclui alterações de um repositório privado usado pela Microsoft.

## <a name="contribute"></a><a name="bkmk_contribute"></a>Contribuir

A biblioteca de documentação do Gestor de Configuração, tal como a maioria dos conteúdos em docs.microsoft.com, é de código aberto no GitHub. Esta biblioteca aceita e encoraja contribuições comunitárias. Para mais informações sobre como começar, consulte o Guia do [Contribuinte.](https://docs.microsoft.com/contribute) O único pré-requisito é criar uma [conta GitHub.](https://github.com/join)

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Passos básicos para contribuir para os SCCMdocs

1. A partir do artigo-alvo, **selecione Editar**. Esta ação abre o ficheiro fonte no GitHub.

2. Para editar o ficheiro fonte, selecione o ícone do lápis.

3. Faça alterações na fonte de marcação. Para mais informações, consulte [Como utilizar o Markdown para escrever Docs](https://docs.microsoft.com/contribute/markdown-reference).

4. Na secção de alteração de ficheiros Proposta, insira o comentário de compromisso público descrevendo *o que* mudou. Em seguida, selecione **Propor alterar ficheiros**.

5. Desça e verifique as alterações que fez. Selecione **Criar pedido de puxar** para abrir o formulário. Descreva *por* que fez esta mudança. Marque o autor do artigo e peça que revejam. Selecione **Criar pedido de puxar**.

### <a name="what-to-contribute"></a>O que contribuir

Se quiser contribuir, mas não sabe por onde começar, consulte as seguintes sugestões:

- Pesquise a lista de questões para os rótulos direcionados para a comunidade:

  - [bom primeiro problema](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [ajuda-procurado](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Os autores da Microsoft atribuem estes rótulos a questões que são bons candidatos à contribuição comunitária.

- Reveja um artigo para precisão. Em seguida, atualize os `mm/dd/yyyy` metadados **ms.date** utilizando o formato. Esta contribuição ajuda a manter o conteúdo fresco.

- Adicione esclarecimentos, exemplos ou orientações com base na sua experiência. Esta contribuição usa o poder da comunidade para partilhar conhecimento.

- Traduções corretas numa língua não inglesa. Esta contribuição melhora a utilização de conteúdos localizados.

> [!NOTE]
> Grandes contribuições requerem a assinatura de um Contrato de Licença de Contribuição (CLA) se não for um funcionário da Microsoft. O GitHub exige automaticamente que assine este acordo quando uma contribuição cumpre o limiar.

### <a name="tips"></a>Sugestões

Siga estas diretrizes gerais quando contribuir para os docs do Gestor de Configuração:

- Não nos surpreenda com grandes pedidos de atração. Em vez disso, [apresente um problema](#bkmk_docfeedback) e inicie uma discussão. Então podemos concordar numa direção antes de investir uma grande quantidade de tempo.

- Leia o guia de [estilo da Microsoft](https://aka.ms/MicrosoftStyle). Conheça as [10 dicas do Top 10 para o estilo e voz](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)da Microsoft.

- Utilize o modelo de pedido de [puxão](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) como ponto de partida do seu trabalho.

- Siga o [fluxo de trabalho gitHub Flow](https://guides.github.com/introduction/flow/).

- Blog e tweet (ou o que quer que seja) sobre as suas contribuições, com frequência!

(Esta lista foi emprestada do guia de [contribuição .NET](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Consolidação da documentação para o Microsoft Endpoint Manager

Para melhor suportar cenários combinados para Intune e Configuration Manager, as suas bibliotecas de documentação são consolidadas no site do [Microsoft Endpoint Manager](https://docs.microsoft.com/mem). A documentação Intune está agora em [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune), e a documentação do Gestor de Configuração está agora em [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr). Se ainda utilizar um URL antigo, redirecionará automaticamente, para que não seja necessário fazer alterações para ler este conteúdo.

Se fornecer feedback ou contribuir para artigos, serão necessárias algumas alterações:

- As questões gitHub existentes permanecem no repositório original, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) ou [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - Estas questões não vão aparecer como questões abertas ou fechadas na secção de Feedback do artigo vinculado.

  - Continuaremos a trabalhar para resolver estas questões.

  - Em alguns casos, podemos tomar a difícil decisão de encerrar um assunto que achamos que não podemos resolver.

  - Se tiver algum problema no repositório existente, e estiver apaixonado por isso, preencha o feedback sobre o artigo migrado no [repositório MEMDocs.](https://github.com/MicrosoftDocs/MEMDocs)

- Agora, quando arquiva feedback ou edita um artigo, o pedido de emissão ou de pull vai para o repositório MEMDocs.
