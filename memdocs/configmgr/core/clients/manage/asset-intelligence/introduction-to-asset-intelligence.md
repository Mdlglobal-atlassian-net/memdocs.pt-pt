---
title: Introdução da inteligência de ativos
titleSuffix: Configuration Manager
description: Utilize a inteligência de ativos no Gestor de Configuração para inventariar e gerir o uso da licença de software em toda a sua empresa.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714186"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introdução à inteligência de ativos no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Inventário e gestão do uso da licença de software em toda a sua empresa utilizando o catálogo de inteligência de ativos. A inteligência de ativos adiciona aulas de inventário de hardware para melhorar a amplitude da informação que o Gestor de Configuração recolhe. Estas informações incluem os títulos de hardware e software utilizados no seu ambiente. Mais de 60 relatórios apresentam esta informação num formato fácil de usar. Muitos destes relatórios estão ligados a relatórios mais específicos. Consulta para informações gerais e aprofundar informações mais detalhadas. 

Adicione informações personalizadas ao catálogo de inteligência de ativos. Por exemplo, categorias de software personalizados, famílias de software, etiquetas de software e requisitos de hardware. Para atualizar dinamicamente o catálogo de inteligência de ativos com as informações mais atuais disponíveis, conecte-o ao Microsoft Cloud. 

Use a inteligência do ativo para ajudar a conciliar o uso da licença de software da empresa. Importe informações de licença de software na base de dados do site Do Gestor de Configuração para vê-la contra o software que está a ser usado.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a>Catálogo de inteligência de ativos  

O catálogo de informações de ativos é um conjunto de tabelas de bases de dados armazenadas na base de dados do site. Estas tabelas incluem informações de categorização e identificação para mais de 300.000 títulos e versões de software. Também ajudam a gerir os requisitos de hardware para títulos de software específicos.  

A inteligência de ativos fornece informações de licença de software para títulos de software que estão a ser usados, tanto da Microsoft como de software não Microsoft. Um conjunto predefinido de requisitos de hardware para títulos de software está disponível no catálogo de inteligência de ativos, e você pode criar novas informações de requisitos de hardware definidos pelo utilizador para satisfazer os requisitos personalizados. Também pode personalizar informações no catálogo de inteligência de ativos e pode enviar informações sobre títulos de software para a nuvem da Microsoft para categorização.  

As atualizações do catálogo de informações de ativos que incluem software recém-lançado estão disponíveis para download periodicamente para executar atualizações de catálogo a granel. Também pode ser atualizado dinamicamente utilizando o ponto de sincronização da inteligência do ativo.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorias de software  

As categorias de software de inteligência de ativos são usadas para categorizar amplamente títulos de software inventariado e como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software poderá ser empresas de energia e uma família de software dentro dessa categoria de software poderá ser petróleo e gás ou hidroelétrica. Muitas categorias de software são predefinidas no catálogo de inteligência de ativos. Pode criar categorias definidas pelo utilizador para definir adicionalmente o software inventariado. O estado de validação de todas as categorias de software predefinidos é sempre **validado.** As informações personalizadas da categoria de software adicionadas ao catálogo de inteligência de ativos são **Definidas pelo Utilizador**. 

Para obter mais informações sobre como gerir categorias de software, consulte [a Configuração da inteligência dos ativos.](configuring-asset-intelligence.md)  

> [!NOTE]  
> As informações predefinidas da categoria de software armazenadas no catálogo de inteligência de ativos são apenas de leitura. Não pode mudá-lo ou apagá-lo. Os utilizadores administrativos podem adicionar, modificar ou eliminar categorias de software definidas pelo utilizador.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Famílias de software  

As famílias de software de inteligência de ativos são usadas para definir títulos de software inventariados dentro das categorias de software. Muitas famílias de software estão predefinidas no catálogo de inteligência de ativos. Pode criar categorias definidas pelo utilizador para definir adicionalmente o software inventariado. O estado de validação de todas as famílias de software predefinidos é sempre **validado.** As informações personalizadas da família do software adicionadas ao catálogo de inteligência de ativos são **definidas pelo utilizador.** 

Para obter mais informações sobre como gerir as famílias de software, consulte [a Configuração da inteligência](configuring-asset-intelligence.md)dos ativos.  

> [!NOTE]  
> A informação da família do software predefinido é apenas leitura e não pode ser alterada. Os utilizadores administrativos podem adicionar, modificar ou eliminar famílias de software definidas pelo utilizador.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a>Etiquetas de software  

As etiquetas de software personalizadas de inteligência de ativos permitem criar filtros para agrupar títulos de software e vê-los em relatórios de inteligência de ativos. Utilize etiquetas de software para criar grupos de títulos de software definidos pelo utilizador que partilham um atributo comum. Por exemplo, poderia criar uma etiqueta de software chamada Shareware, associá-lo a títulos de shareware inventariados, e executar um relatório para exibir todos os títulos de software com essa etiqueta. Não há rótulos predefinidos. O estado de validação para as etiquetas de software é sempre **Definido pelo Utilizador**. 

Para obter mais informações sobre como gerir as etiquetas de software, consulte a configuração da [inteligência dos ativos.](configuring-asset-intelligence.md)  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Requisitos de hardware  

Utilize as informações dos requisitos de hardware para verificar se os computadores cumprem os requisitos de hardware para títulos de software antes de serem direcionados para implementações de software. Gerencie os requisitos de hardware para títulos de software no espaço de trabalho **de Ativos e Compliance** no nó de Requisitos de **Hardware** sob o nó de Inteligência de **Ativos.** 

Muitos requisitos de hardware são predefinidos no catálogo de inteligência de ativos. Crie novas informações sobre o requisito de hardware definidos pelo utilizador para satisfazer os requisitos personalizados. O estado de validação de todos os requisitos de hardware pré-definidos é sempre **validado**. A informação dos requisitos de hardware definidopelo utilizador adicionada ao catálogo de informações de ativos é **definida pelo utilizador**. 

Para obter mais informações sobre como gerir os requisitos de hardware, consulte [a configuração](configuring-asset-intelligence.md)da inteligência dos ativos .  

> [!NOTE]  
> Os requisitos de hardware apresentados na consola Do Gestor de Configuração são recuperados do catálogo de inteligência de ativos. Não são baseados em informações inventariadas de títulos de software dos clientes. 
> 
> A informação sobre o requisito de hardware não é atualizada como parte do processo de sincronização com a Microsoft. 
> 
> Pode criar requisitos de hardware definidos pelo utilizador para software inventariado que não tenha requisitos de hardware associados.  

Por predefinição, as seguintes informações são apresentadas para cada requisito de hardware listado:  

- **Título do software**: O título de software associado ao requisito de hardware  

- **CpU mínimo (MHz)**: A velocidade mínima do processador em megahertz (MHz) exigida pelo título do software  

- **RAM mínimo (KB)**: A RAM mínima em quilobytes (KB) exigida pelo título do software  

- **Espaço mínimo do disco (KB)**: O espaço mínimo de disco rígido livre em KB exigido pelo título de software  

- **Tamanho mínimo do disco (KB)**: O tamanho mínimo do disco rígido em KB exigido pelo título de software  

- **Estado de Validação**: O estado de validação para o requisito de hardware  

Os requisitos de hardware pré-definidos armazenados no catálogo de inteligência de ativos são apenas de leitura e não podem ser eliminados. Os utilizadores administrativos podem adicionar, modificar ou eliminar requisitos de hardware definidos pelo utilizador para títulos de software que não estejam armazenados no catálogo de inteligência de ativos.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a>Títulos de software inventariados  

Para ver informações de títulode software inventariadas na consola do Gestor de Configuração, vá ao espaço de trabalho **de Ativos e Compliance,** expanda o nó **de Inteligência de Ativos** e selecione o nó de **Software Inventariado.** O agente de inventário de hardware recolhe as informações de software inventariadas dos clientes do Gestor de Configuração com base nos títulos de software armazenados no catálogo de inteligência de ativos.  

> [!Note]  
> O agente de inventário de hardware recolhe o inventário com base nas classes de relatórios de inventário de hardware de inteligência de ativos que você ativa. Para obter mais informações sobre como ativar as classes de reporte, consulte [a Configuração](configuring-asset-intelligence.md)da inteligência dos ativos .  

Por predefinição, as seguintes informações são apresentadas para cada título de software inventariado:  

- **Nome**: O nome do título de software inventariado  

- **Fornecedor**: O nome do fornecedor que desenvolveu o título de software inventariado  

- **Versão**: A versão do produto do título de software inventariado  

- **Categoria**: A categoria de software que está atualmente atribuída ao título de software inventariado  

- **Família**: A família de software que está atualmente atribuída ao título de software inventariado  

- **Etiqueta** [**1,** **2**, e **3**]: As etiquetas personalizadas associadas ao título do software. Os títulos de software inventariado podem ter até três etiquetas personalizadas associadas aos mesmos.  

- **Contagem**: O número de clientes do Gestor de Configuração que inventariaram o título do software  

- **Estado**: O estado de validação do título de software inventariado  

> [!NOTE]  
> Pode alterar a informação de categorização para software inventariado apenas no site de alto nível da sua hierarquia. Estas informações incluem nome do produto, fornecedor, categoria de software e família de software. Depois de modificar as informações de categorização para software predefinido, o estado de validação do software é alterado de **Validado** para **Definido pelo Utilizador**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Ponto de sincronização da inteligência do ativo  

O ponto de sincronização da inteligência do ativo é uma função do sistema de configuração do site Manager. É usado para ligar à nuvem da Microsoft na porta TCP 443 para gerir atualizações dinâmicas de informação de catálogo. Instale esta função de site apenas no local de alto nível da hierarquia. Configure toda a personalização do catálogo de informações de ativos utilizando uma consola de Configuração Manager ligada ao site de alto nível. 

Enquanto configura todas as atualizações no site de alto nível, as informações do catálogo são replicadas para outros sites da hierarquia. A função do site permite-lhe solicitar sincronização de catálogo a pedido com a Microsoft ou agendar sincronização automática de catálogos. Além de descarregar novas informações sobre o catálogo, o ponto de sincronização da inteligência de ativos pode enviar informações personalizadas sobre o título de software para a Microsoft para categorização. A Microsoft trata todos os títulos de software carregados como informação pública. Certifique-se de que os títulos de software personalizados não incluem informações confidenciais ou proprietárias.  

Depois de submeter um título de software não categorizado, a Microsoft não o revê até que haja pelo menos quatro pedidos de categorização dos clientes para o mesmo título de software. Em seguida, os investigadores da Microsoft identificam, categorizam e disponibilizam a informação de categorização do título de software a todos os clientes que estão a usar o serviço online. Os títulos de software que representem o maior número de pedidos de categorização recebem prioridade máxima de categorização. Software personalizado e aplicações de linha de negócio dificilmente receberão uma categoria. Não envie estes títulos de software para a Microsoft para categorização.  

É necessário um ponto de sincronização da inteligência dos ativos para se ligar à nuvem da Microsoft. Para obter informações sobre como instalar o papel, consulte a configuração da [inteligência do ativo.](configuring-asset-intelligence.md)  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a>Página inicial da inteligência do ativo  

O nó **de Inteligência de Ativos** no espaço de trabalho de Ativos e **Compliance** é a página inicial para inteligência de ativos em Gestor de Configuração. Esta página inicial exibe uma visão sumária do dashboard para informações sobre o catálogo de informações de ativos.  

> [!NOTE]  
> A página inicial **da Inteligência de Ativos** não atualiza automaticamente enquanto a vê.  

A página inicial **da Inteligência de Ativos** inclui as seguintes secções:  

- **Sincronização de Catálogo**: Informação sobre se a inteligência dos ativos está ativada e o estado atual do ponto de sincronização da inteligência do ativo.  

    > [!NOTE]  
    > A página inicial só exibe esta secção quando instala um ponto de sincronização de inteligência de ativos.  

    A secção também fornece as seguintes informações:  

    - Agenda de sincronização  

    - Se tiver importado um extrato de licença de cliente   

    - A última atualização de estado  

    - A hora da próxima atualização agendada  

    - O número de mudanças após a instalação do ponto de sincronização da inteligência do ativo   

- **Estado do Software Inventariado**: A contagem e percentagem de software inventariado, categorias de software e famílias de software identificadas pela Microsoft, identificadas por um administrador, pendentes de identificação online, ou não identificadas e não pendentes. As informações apresentadas em formato de tabela mostram a contagem de cada uma e as informações apresentadas no gráfico mostram a percentagem de cada uma.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Relatórios de inteligência de ativos  

Os relatórios de inteligência de ativos estão localizados na consola do Gestor de Configuração, no espaço de trabalho de **Monitorização,** na pasta de **inteligência Asset** sob o nó **reporte.** Os relatórios fornecem informações sobre hardware, gestão de licenças e software. Para obter mais informações sobre relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> A precisão da quantidade de títulos de software instalados e informações de licença apresentadas em relatórios de inteligência de ativos pode variar do número real de títulos de software instalados ou licenças que são usadas no ambiente. Esta variação deve-se às complexas dependências e limitações envolvidas no inventário de informações de licenças de software para títulos de software que estão instalados em ambientes empresariais. Não use relatórios de inteligência de ativos como a única fonte para determinar a conformidade com a licença de software adquirida.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a>Relatórios de hardware  

Relatórios de hardware de inteligência de ativos fornecem informações sobre ativos de hardware na organização. Utilizando informações de inventário de hardware, como velocidade, memória e dispositivos periféricos, os relatórios de hardware de inteligência de ativos podem apresentar informações sobre dispositivos USB, sobre hardware que deve ser atualizado, e até sobre computadores que não estão prontos para uma atualização específica do software.  

> [!NOTE]  
> Alguns dados dos utilizadores em relatórios de hardware de inteligência de ativos são recolhidos a partir do registo de eventos de segurança do Windows. Para obter uma melhor precisão no relatório, limpe este registo quando reatribuir um computador a um novo utilizador.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a>Relatórios de gestão de licenças  

Os relatórios de gestão de licenças de inteligência de ativos fornecem dados sobre licenças que estão a ser usadas. O relatório **License Ledger** lista aplicações instaladas da Microsoft num formato congruente com uma Declaração de Licença da Microsoft (MLS). Este formato fornece um método conveniente de combinar licenças adquiridas com licenças usadas. Outros relatórios de gestão de licenças fornecem informações sobre computadores que funcionam como servidores que executam o serviço de gestão de chaves (KMS) para estatísticas de ativação do Windows.  

> [!IMPORTANT]  
> Vários dos relatórios de gestão de licenças de inteligência de ativos apresentam informações sobre a função da KMS, um método de gestão do licenciamento de volume. Se não implementou um servidor KMS, alguns relatórios podem não devolver quaisquer dados.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a>Relatórios de software  

Os relatórios de software de inteligência de ativos fornecem informações sobre famílias de software, categorias e títulos de software específicos que são instalados em computadores da organização. Os relatórios de software apresentam informações como objetos auxiliares de navegador e software que começa automaticamente. Estes relatórios podem ser usados para identificar adware, spyware e outros malwares. Também pode usá-los para identificar a redundância do software para ajudar a agilizar a aquisição e suporte de software.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a>Relatórios de etiquetas de identificação de software  

Os relatórios de identificação de software de inteligência de ativos fornecem informações sobre software que inclui uma etiqueta de identificação de software compatível com ISO/IEC 19770-2. As etiquetas de identificação do software fornecem informações autoritárias utilizadas para identificar o software instalado. Quando ativa **a** SMS_SoftwareTag classe de relatórios de inventário de hardware, o Gestor de Configuração recolhe informações sobre o software com etiquetas de identificação de software. 

Os relatórios seguintes fornecem informações sobre o software:  

- **Software 14A - Pesquisa de software de identificação**de software ativado : A contagem de software instalado com uma etiqueta de identificação de software ativada  

- **Software 14B - Computadores com identificação específica de identificação de software software instalado**: Todos os computadores que instalaram software com uma etiqueta de identificação específica de software ativada  

- **Software 14C - Software de identificação**de software instalado num computador específico : Todo o software instalado com uma etiqueta de identificação específica de software ativada num computador específico  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a>Limitações de reporte  

Os relatórios de inteligência de ativos podem fornecer grandes quantidades de informação sobre títulos de software instalados e licenças de software adquiridas que estão a ser usadas. Não utilize esta informação como a única fonte para determinar a conformidade com a licença de software adquirida.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Exemplos de dependências  
A precisão da quantidade exibida nos relatórios de inteligência de ativos para títulos de software instalados e informações de licença pode variar das quantidades reais atualmente utilizadas. Esta variação é causada pelas complexas dependências envolvidas no inventário de informações de licenças de software para títulos de software em utilização em ambientes empresariais. Os seguintes exemplos mostram as dependências envolvidas na inventário de software instalado na empresa, utilizando inteligência de ativos que pode afetar a precisão dos relatórios de inteligência de ativos:  

- **Dependências**de inventário de hardware do cliente : Os relatórios de software instalados em inteligência de ativos baseiam-se em dados recolhidos dos clientes do Gestor de Configuração, alargando o inventário de hardware para permitir o reporte de informações de ativos. Devido a esta dependência no relatório de inventário de hardware, os relatórios de inteligência de ativos refletem dados apenas de clientes que completam com sucesso os processos de inventário de hardware com as classes de reporte de informação de ativos necessárias ativadas. Uma vez que os clientes do Gestor de Configuração realizam processos de inventário de hardware numa programação definida pelo utilizador administrativo, pode ocorrer um atraso no relato de dados que afeta a precisão dos relatórios de inteligência de ativos. 

    Por exemplo, um título de software licenciado inventariado poderá ser desinstalado após o cliente concluir um ciclo de inventário de hardware com êxito. Os relatórios de inteligência de ativos mostram o título de software como instalado até ao próximo ciclo de relatórios de inventário de hardware programado do cliente.  

- **Dependências de embalagem de software**: Os relatórios de inteligência de ativos baseiam-se em dados de títulos de software instalados recolhidos utilizando processos padrão de inventário de hardware do cliente do Gestor de Configuração. Alguns dados do título do software podem não ser recolhidos corretamente. Exemplos que podem causar relatórios imprecisos de informação sobre ativos:  

    - Instalações de software que não cumprem os processos de instalação padrão  

    - Instalações de software que foram alteradas antes da instalação   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Limitações legais  
A informação exibida nos relatórios de inteligência de ativos está sujeita a muitas limitações. As informações neles apresentadas não representam aconselhamento jurídico, contabilístico ou outro profissional. A informação fornecida pelos relatórios da inteligência dos ativos é apenas para informação. Não a utilize como única fonte de informação para determinar a conformidade com o uso da licença de software.  

As seguintes limitações são exemplos de utilização da inteligência do ativo que podem afetar a precisão dos relatórios:  

- **Limitações de quantidade**de utilização da licença da Microsoft:  

    - A quantidade de licenças de software da Microsoft adquiridas baseia-se em informações que os administradores fornecem. Reveja-o de perto para se certificar de que o número correto de licenças de software é fornecido.  

    - A quantidade reportada de licenças de software da Microsoft inclui informações apenas sobre licenças de software da Microsoft adquiridas através de programas de licenciamento de volume. Não reflete informações sobre licenças de software adquiridas através de retalho, OEM ou outros canais de venda de licenças de software.  

    - As licenças de software adquiridas nos últimos 45 dias podem não ser incluídas na quantidade de licenças de software Microsoft comunicada devido a prazos e requisitos de comunicação de revendedores de software.  

    - As transferências de licenças de software resultantes de fusões ou aquisições da empresa podem não ser refletidas nas quantidades de licenças de software Microsoft.  

    - Os termos e condições não padrão num acordo de Licenciamento de Volume da Microsoft (MVLS) podem afetar o número de licenças de software reportadas. Podem necessitar de uma revisão adicional por um representante da Microsoft.  

- Limitações de quantidade de **títulode software instalados**: Os clientes do Gestor de Configuração devem completar com sucesso os ciclos de reporte de inventário de hardware para os relatórios de inteligência de ativos reportarem com precisão a quantidade de títulos de software instalados. Pode haver um atraso entre a instalação ou a não instalação de um título de software licenciado após um ciclo de relatóriode inventário de hardware bem sucedido. Esta ação pode não se refletir nos relatórios de inteligência de ativos executados antes que o cliente reporte o seu próximo inventário de hardware agendado.  

- **Limitações**de reconciliação de licenças : A reconciliação da quantidade de títulos de software instalados à quantidade de licenças de software adquiridas é calculada utilizando uma comparação da quantidade de licença especificada pelo administrador e da quantidade de títulos de software instalados recolhidos dos inventários de hardware do cliente do Gestor de Configuração com base no calendário definido pelo administrador. Esta comparação não representa uma conclusão final da Microsoft sobre as posições de licença. O estado de licenciamento real depende dos direitos de utilização e das licenças de títulos de software específicos concedidos pelos termos de licenciamento.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a>Estados de validação de informação de ativos  

Os estados de validação de informação de ativos representam a fonte e o estado atual de validação da informação do catálogo de informações de ativos. A tabela seguinte mostra possíveis estados de validação de informação de ativos e ações de administrador que podem causar-lhes.  

| Estado | Definição | Ação do administrador | Comentário |  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|Investigadores da Microsoft definiram o item do catálogo|Nenhuma|Melhor estado|  
|**Definido pelo Utilizador**|Os investigadores da Microsoft não definiram o item do catálogo|Personalize as informações do catálogo local|Este estado é exibido em relatórios de inteligência de ativos|  
|**Pendente**|Os investigadores da Microsoft ainda não definiram o artigo do catálogo, mas submeteram o artigo à Microsoft para categorização|Nenhuma outra ação depois de pedir categorização|O item do catálogo permanece neste estado até que os investigadores da Microsoft categorizem o item e sincronizam o seu catálogo de inteligência de ativos|  
|**Atualizável**|Um artigo de catálogo definido pelo utilizador foi categorizado de forma diferente pela Microsoft durante a sincronização do catálogo.|Utilize a ação **Resolve Conflict** para decidir se utiliza as novas informações de categorização ou o valor anterior definido pelo utilizador. Para obter mais informações sobre como resolver conflitos, consulte [Operações de inteligência](operations-for-asset-intelligence.md)de ativos.|Depois de resolver um conflito de categorização, o item não é validado como conflituoso novamente, a menos que as atualizações posteriores da categorização introduzam novas informações sobre o item.|  
|**Não Categorizado**|O item do catálogo não foi definido pelos investigadores da Microsoft, o item não foi submetido à Microsoft para categorização, e o administrador não atribuiu um valor de categorização definido pelo utilizador.|Solicite categorização ou personalize as informações do catálogo local. Para mais informações, consulte [Operações para inteligência](operations-for-asset-intelligence.md)de ativos.|Nenhuma|  

> [!NOTE]  
> Os itens de catálogo que submete à Microsoft para categorização têm um estado de validação de **Pendente** num site de administração central, mas continuam a ser exibidos com um estado de validação de **Não categorizado** em sites primários infantis.  

Por exemplo, quando um estado de validação pode transitar de um estado para outro, ver transições de estado de [validação por exemplo para inteligência de ativos.](example-validation-state-transitions-for-asset-intelligence.md)  
