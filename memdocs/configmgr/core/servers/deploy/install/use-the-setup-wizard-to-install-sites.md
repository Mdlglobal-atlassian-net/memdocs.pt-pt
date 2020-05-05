---
title: Assistente de configuração
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e32956d2ca9385c22e9073cfa2665e1f61b3ebd3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078639"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Utilize o Assistente de Configuração para instalar sites do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para instalar um novo site do Gestor de Configuração utilizando uma interface de utilizador guiada, utilize o Assistente de Configuração do Gestor de Configuração (configuração.exe). O assistente suporta a instalação de um local primário ou local de administração central. Também utiliza o assistente para [atualizar uma instalação](upgrade-an-evaluation-install-to-a-full-install.md) de avaliação do Gestor de Configuração para uma instalação totalmente licenciada. Quando não quiser utilizar o assistente, pode utilizar um script de [instalação](use-a-command-line-to-install-sites.md) e executar uma instalação de linha de comando sem supervisão.

Instale um site secundário a partir da consola 'Gestor de Configuração'. Os sites secundários não suportam uma instalação de linha de comando escrita.

> [!Note]  
> A partir da versão 1906, o ficheiro **splash.hta** já não existe na raiz dos meios de instalação. Forneceu ligações às seguintes informações:<!--SCCMDocs-pr#3545-->
>
> - **Instalar o local:** `smssetup\bin\x64\setup.exe`. Para mais informações, consulte [Instale uma administração central ou um site primário](#bkmk_primary).
> - **Antes de começar**: [Desenhe uma hierarquia de sites](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Avaliar a prontidão do servidor**: [Verificador pré-requisito](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Descarregue os ficheiros pré-requisitos necessários:** `smssetup\bin\x64\setupdl.exe`. Para mais informações, consulte O Downloader de [Configuração](setup-downloader.md).
> - Instalar a consola `smssetup\bin\i386\consolesetup.exe`de Gestor de **Configuração**: . Para mais informações, consulte [Instalar consolas.](install-consoles.md)
> - [**Descarregue o Editor de Atualizações do Centro de Sistemas**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Descarregue os clientes para sistemas operativos adicionais:** <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager - macOS Client (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Clientes da UNIX e Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Notas de versão**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Ler documentação**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - Obter assistência à **instalação**: [TechNet Forums: Gestor de Configuração (Ramo Atual) – Implantação de Site e Cliente](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Comunidade gestora de configuração**: [System Center Community: Como Participar](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Casa do Gestor de Configuração**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a>Instale uma administração central ou um local primário

Utilize o seguinte procedimento para instalar um site de administração central ou um local primário. Também o utilize para atualizar um site de avaliação para um site de Configuração totalmente licenciado.

Antes de iniciar a instalação do local, esteja familiarizado com os detalhes dos seguintes artigos:

- [Preparar a instalação de sites](prepare-to-install-sites.md)
- [Pré-requisitos para instalar sites](prerequisites-for-installing-sites.md)

Se estiver a instalar um site de administração central como parte de um cenário de expansão do site, reveja [expandir um site primário autónomo](use-the-setup-wizard-to-install-sites.md#bkmk_expand) antes de utilizar o seguinte procedimento.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a>Processo para instalar um site de administração primária ou central

1. No computador onde pretende instalar o `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` site, corra para iniciar o Assistente de **Configuração do Gestor**de Configuração .  

    > [!NOTE]  
    > Quando instalar um site de administração central para expandir num local primário autónomo ou instalar um novo site primário infantil numa hierarquia existente, utilize meios de instalação (ficheiros de origem) que correspondam à versão do site ou sites existentes. Se instalou atualizações na consola que alteraram a versão dos sites previamente instalados, não utilize os meios de instalação originais. Em vez disso, utilize ficheiros de origem do [CD. Última pasta](../../manage/the-cd.latest-folder.md) de um site atualizado. O Gestor de Configuração requer que utilize ficheiros de origem que correspondam à versão do site existente a que o seu novo site se irá ligar.  

2. Na página **Antes de Começar,** escolha **A Seguir**.  

3. Na página **Getting Started,** selecione o tipo de site que pretende instalar:  

    - Sítio da **administração central,** como o primeiro local de uma nova hierarquia, ou ao expandir um local primário autónomo:  

        Selecione Instalar um site central de **administração do Gestor**de Configuração .  

        Durante um passo posterior deste procedimento, é-lhe oferecida a opção de instalar um site de administração central como o primeiro local de uma nova hierarquia, ou instalar um site de administração central para expandir-se em um local primário autónomo.  

    - **Local primário,** como um local primário autónomo que é o primeiro local de uma nova hierarquia, ou como uma criança primária:  

        **Selecione Instalar um site primário do Gestor de Configuração**.  

        > [!TIP]  
        > Normalmente, você seleciona apenas a opção **Utilize opções típicas** de instalação para um local primário autónomo quando pretende instalar um local primário autónomo num ambiente de teste. Quando selecionar esta opção, a configuração faz as seguintes ações:  
        >
        > - Configura automaticamente o site como um local primário autónomo.  
        > - Usa um caminho de instalação predefinido.  
        > - Utiliza uma instalação local da instância padrão do Servidor SQL para a base de dados do site.  
        > - Instala um ponto de gestão e um ponto de distribuição no computador do servidor do site.  
        > - Configura o site com o inglês e o idioma de exibição do SISTEMA no servidor do site primário se corresponder a um dos idiomas que o Gestor de Configuração suporta.  

4. Na página chave do **produto:**  

    - Escolha se instala o Gestor de Configuração como uma edição de avaliação ou uma edição licenciada.  

        - Se selecionar uma edição licenciada, insira a chave do produto e escolha **A Seguinte**.  

        - Se selecionar uma edição de avaliação, escolha **Next**. (Pode atualizar uma instalação de avaliação para uma instalação completa mais tarde.)  

    - Também pode especificar a data de validade da Garantia de **Software** do seu contrato de licenciamento. É uma lembrança conveniente dessa data. Se não introduzir esta data durante a Configuração, poderá especificá-la mais tarde a partir da consola 'Gestor de Configuração'.  

        > [!NOTE]  
        > A Microsoft não valida a data de validade que inseriu e não utiliza esta data para validação da licença. Pode usá-lo como um lembrete da sua data de validade. Esta data é útil porque o Gestor de Configuração verifica periodicamente novas atualizações de software oferecidas online. O estado da licença de garantia de software deve estar atual para que possa utilizar estas atualizações adicionais.  

    Para mais informações, consulte [Licenciamento e Balcões.](../../../understand/learn-more-editions.md)  

5. Na página de Termos de Licença de Software da **Microsoft,** leia e aceite os termos da licença.  

6. Na página **De Licenças Pré-Requisitos,** leia e aceite os termos da licença para o software pré-requisito. A configuração descarrega e instala automaticamente o software nos sistemas do site ou nos clientes quando é necessário. Aceite todos os termos antes de continuar para a página seguinte.  

7. Na página **Descarregamentos Pré-Requisito,** especifique se a Configuração deve descarregar os ficheiros redistribuíveis pré-requisitos mais recentes da internet ou utilizar ficheiros previamente descarregados:  

    - Se pretender configurar para descarregar os ficheiros neste momento, selecione **Descarregar ficheiros necessários**. Em seguida, especifique a localização para armazenar os ficheiros.  

    - Se já descarregou os ficheiros utilizando o Downloader de [Configuração,](setup-downloader.md)selecione **Use ficheiros previamente descarregados**. Em seguida, especifique a pasta de descarregamento.  

        > [!TIP]  
        > Se utilizar ficheiros previamente descarregados, verifique se o caminho para a pasta de descarregamento contém a versão mais recente dos ficheiros.  

8. Na página de Seleção de Idiomas do **Servidor,** selecione os idiomas disponíveis para a consola do Gestor de Configuração e para os relatórios. (O inglês é selecionado por padrão e não pode ser removido.) Para mais informações, consulte [pacotes de idioma.](language-packs.md)  

9. Na página de Seleção de **Idiomas do Cliente,** selecione os idiomas disponíveis para computadores clientes. Especifique também se permite todas as línguas de cliente para clientes de dispositivos móveis. (O inglês é selecionado por padrão e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando utilizar um site de administração central, certifique-se de que as línguas de cliente que configura no site da administração central incluem todas as línguas de cliente que configura em cada site primário infantil. Os clientes que instalam a partir de um ponto de distribuição têm acesso às línguas dos clientes a partir do site de topo, enquanto os clientes que instalam a partir de um ponto de gestão têm acesso às línguas do cliente a partir do seu site primário designado.  

10. Na página definições de Definições do **Site e da Instalação,** especifique as seguintes definições para o novo site que está a instalar:  

    - **Código do site**: Cada código de [site numa hierarquia deve ser único](prepare-to-install-sites.md#bkmk_sitecodes). Utilize três dígitos alfa-numéricos: A a Z e 0 a 9. Como o código do site é usado em nomes de pastas, não utilize nomes reservados ao Windows, incluindo:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > A configuração não verifica se o código do site que especifica já está a ser utilizado, ou se é um nome reservado.  

    - **Nome**do site : Cada site requer este nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: Esta pasta é o caminho para a instalação do Gestor de Configuração. Não pode alterar a localização depois da instalação do site. O caminho não pode conter caracteres Unicode ou espaços de fuga.  

        > [!NOTE]  
        > Considere se pretende utilizar a pasta de instalação predefinida. Se utilizar a partição padrão do OS num ambiente de produção, poderá vir a ter os seguintes problemas no futuro:  
        >
        > - Se o Gestor de Configuração utilizar o espaço adicional de disco gratuito na divisória S, nem o Windows nem o 'Gestor de Configuração' funcionarão corretamente. Se instalar o Gestor de Configuração numa divisória separada, o seu consumo de disco não afetará o Sistema operativo.
        > - O desempenho do Gestor de Configuração é melhor com um disco rápido. Alguns designs de servidores não otimizam o disco DE SO para a velocidade.
        > - Pode servir, restaurar ou reinstalar o SISTEMA sem afetar a instalação do Gestor de Configuração.  

11. Na página de Instalação do **Site,** utilize a seguinte opção que corresponda ao seu cenário:  

    - **Estou a instalar um site da administração central:**  

        Na página de instalação do **Site da Administração Central,** selecione **Instalar como primeiro site numa nova hierarquia**, e depois escolher **O Próximo** para continuar.  

    - **Estou a expandir uma primária autónoma para uma hierarquia com um site de administração central:**  

        Na página de instalação do **Site da Administração Central,** selecione **Expandir uma primária autónoma existente numa hierarquia**. Em seguida, especifique o FQDN do servidor de site primário autónomo e escolha **Next** para continuar.  

        Os meios que utiliza para instalar o novo site da administração central devem coincidir com a versão do site principal.  

    - **Estou a instalar um local primário autónomo:**  

        Na página de instalação do **sítio primário,** selecione **Instale o site principal como um site autónomo**e, em seguida, escolha **Seguinte**.  

    - **Estou a instalar um local primário para crianças:**  

        Na página de Instalação do **Sítio Primário,** selecione **Juntar o site principal a uma hierarquia existente**. Em seguida, especifique o FQDN para o site da administração central, e escolha **Next**.  

12. Na página informação da base de **dados,** especifique as seguintes informações:  

    - Nome do **Servidor SQL (FQDN)**: Por padrão, este valor é definido para o computador do servidor do site.  

        Se utilizar uma porta personalizada, adicione essa porta ao FQDN do Servidor SQL. Siga o FQDN do Servidor SQL com uma vírem e, em seguida, o número de porta. Por exemplo, para *SQLServer1.fabrikam.com*do servidor, utilize o seguinte para especificar a porta *1551:*`SQLServer1.fabrikam.com,1551`  

    - **Nome da instância**: Por defeito, este valor é em branco. Utiliza a instância padrão de SQL no computador do servidor do site.  

    - **Nome da base**de dados : `CM_<Sitecode>`Por predefinição, este valor está definido para . Pode personalizar este valor.  

    - Porta corretor **de serviços**: Por padrão, este valor está definido para utilizar a porta padrão do SQL Server Broker (SSB) de 4022. A SQL usa-o para comunicar diretamente à base de dados do site noutros sites.  

13. Na segunda página de Informação de Base de **Dados,** pode especificar localizações personalizadas para o ficheiro de dados do Servidor SQL e o ficheiro de registo do Servidor SQL para a base de dados do site:  

    - Por predefinição, utiliza as localizações de ficheiros predefinidos para o Servidor SQL.  

    - Quando utiliza um cluster SQL Server, a opção de especificar localizações de ficheiros personalizadas não está disponível.  

    - O verificador pré-requisito não verifica o espaço de disco gratuito para localizações de ficheiros personalizados.  

14. Na página definições do **Fornecedor SMS,** especifique o FQDN para o servidor onde pretende instalar o Fornecedor SMS.  

    - Por padrão, especifica o servidor do site.  

    - Após a instalação do site, pode configurar fornecedores de SMS adicionais. Para mais informações, consulte [Plan for the SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. Na página de Definições de **Comunicação do Cliente,** escolha se configurar todos os sistemas do site para aceitar apenas a comunicação HTTPS dos clientes ou para que o método de comunicação seja configurado para cada função do sistema do site.  

    Quando selecionar Todas as funções do sistema do **site aceitam apenas comunicação HTTPS dos clientes,** o computador cliente deve ter um certificado PKI válido para autenticação do cliente. Para mais informações, consulte os requisitos do [certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Este passo só se aplica quando se instala um local primário. Se está a instalar um site da administração central, ignore este passo.  

16. Na página **Defunções** do Sistema do Site, escolha se instala um ponto de gestão ou ponto de distribuição. Para cada função que escolher ter instalado por Configuração:  

    - Introduza o **FQDN** para o servidor que irá acolher a função. Em seguida, escolha o método de ligação ao cliente que o servidor irá suportar: HTTP ou HTTPS.  

    - Se selecionou Todas as funções do sistema do **site aceitam apenas comunicação HTTPS dos clientes** na página anterior, as definições de ligação ao cliente são automaticamente configuradas para HTTPS. Não pode alterar esta definição a menos que volte à página anterior.  

    > [!NOTE]  
    > Este passo só se aplica quando se instala um local primário. Se está a instalar um site da administração central, ignore este passo.  

    > [!NOTE]  
    > Para instalar as funções do sistema do site, a Configuração utiliza a conta de **instalação**do sistema do site . Por padrão, isto utiliza a conta de computador do site principal. Esta conta deve ser um administrador local num computador remoto para instalar a função do sistema do site. Se esta conta não tiver as permissões necessárias, desverifique as funções do sistema do site e instale-as mais tarde a partir da consola 'Gestor de Configuração', depois de configurar contas adicionais para utilizar como contas de instalação do sistema do site. Para mais informações, consulte [Contas](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. Na página Dados de **Utilização,** reveja as informações sobre os dados que a Microsoft recolhe e, em seguida, escolha **A Seguir**. Para mais informações, consulte [Diagnósticos e dados de utilização](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. A página de configuração do ponto de **ligação** ao serviço só está disponível durante os seguintes cenários:  

    - Quando estiver a instalar um local primário autónomo.  

    - Quando estiver a instalar um site de administração central.  

    > [!NOTE]  
    > Se estiver a instalar um local primário para crianças, ignore este passo.  

     Se estiver a instalar um site de administração central como parte de um cenário de expansão do site, e esta função já estiver instalada no local primário autónomo, primeiro desinstale esta função a partir do local primário autónomo. Apenas um exemplo deste papel é permitido numa hierarquia, e só é apoiado no local de topo da hierarquia.  

     Depois de selecionar uma configuração para o Ponto de Ligação de **Serviço,** escolha **Seguinte**. Depois de configurar, pode alterar esta configuração a partir da consola 'Gestor de Configuração'. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../configure/about-the-service-connection-point.md).  

19. Na página Resumo das **Definições,** reveja a definição que selecionou. Quando estiver pronto, escolha **o Próximo** para iniciar o Verificador Pré-Requisito.  

20. Na página de Verificação de **Instalações Pré-Requisito,** ele lista quaisquer problemas que o verificador possa identificar.  

    - Quando o Verificador Pré-Requisito encontrar um problema, escolha um item na lista para obter detalhes sobre como resolver o problema.  

    - Antes de poder continuar a instalar o site, resolva itens **falhados.** Tente também resolver itens com estatuto de **Aviso,** mas não bloqueiam a instalação do local.  

    - Depois de resolver problemas, escolha **'Verificar',** para reexecutar o Verificador Pré-Requisito.  

        Quando o Verificador Pré-Requisito funciona e não há verificações recebem um estado **falhado,** pode escolher Iniciar a **Instalação** para iniciar a instalação do local.  

    > [!TIP]  
    > Além do feedback que o assistente fornece, pode encontrar informações adicionais sobre questões pré-requisitos no ficheiro **ConfigMgrPrereq.log.** Está na raiz da unidade do sistema do computador em que está a instalar o site. Para mais informações, consulte [A Lista de Verificações pré-requisitos](list-of-prerequisite-checks.md).  

21. Na página de **Instalação,** a Configuração apresenta o estado de instalação. Quando a instalação do servidor do local central estiver completa, pode **fechar** o assistente de instalação. Quando fechar o assistente, as configurações de instalação e local inicial continuam em segundo plano.  

    - Pode ligar uma consola de Configuração ao site antes de a Configuração estar completa. Esta consola liga-se apenas à leitura e permite-lhe visualizar objetos e configurações, mas não pode modificar nada.  

    - Depois de a Configuração estar concluída, pode ligar uma consola que pode editar objetos e definições.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a>Expandir um local primário autónomo

Quando instalou um site primário autónomo como o seu primeiro site, tem a opção de expandir esse site para uma hierarquia maior, instalando um site de administração central.

Ao expandir um site primário autónomo, instala um novo site de administração central que utiliza a base de dados de sites primários autónomos existente como referência. Após a instalação do novo site da administração central, o local primário autónomo funciona como um local primário infantil.

- Só se pode expandir um local primário autónomo para uma nova hierarquia.  

- Só se pode expandir um local primário autónomo numa hierarquia específica. Não pode usar esta opção para juntar locais primários autónomos adicionais na mesma hierarquia. Em vez disso, use o Feiticeiro de Migração para migrar dados de uma hierarquia para outra. Para obter mais informações, consulte os [dados migrados entre hierarquias](../../../migration/migrate-data-between-hierarchies.md).  

- Depois de expandir um site autónomo para uma hierarquia com um site de administração central, você pode adicionar locais adicionais para crianças primárias.  

- Para remover um local primário de uma hierarquia com um site de administração central, primeiro desinstale o local principal.  

Para expandir o site, utilize o Assistente de Configuração do Gestor de Configuração para instalar um novo site de administração central com as seguintes ressalvas:  

- Instale o site da administração central utilizando a mesma versão do Gestor de Configuração que o local primário autónomo.  

- Na página **Getting Started** do Assistente de Configuração, selecione a opção de instalar um site de administração central. Numa fase posterior da Configuração, você escolherá uma opção para expandir um site primário autónomo existente.  

- Quando configurar a página de Seleção de **Idiomas do Cliente** para o novo site da administração central, selecione os mesmos idiomas de cliente que estão configurados para o site primário autónomo que está a expandir.  

- Na página de Instalação do **Site,** selecione a opção de expandir o site primário autónomo.  

Para expandir um local primário autónomo, primeiro consulte os [pré-requisitos para expandir um site](prerequisites-for-installing-sites.md#bkmk_expand). Em seguida, utilize o procedimento [Para instalar um site de administração primária ou central](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) no início deste artigo.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a>Instale um site secundário

Utilize a consola 'Gestor de Configuração' para instalar um site secundário.  

- Se a consola que utiliza não estiver ligada ao local principal que será o local principal do novo local secundário, o comando para instalar o site é replicado para o local primário correto.  

- Antes de iniciar a instalação do site, certifique-se de que a sua conta de utilizador possui as permissões pré-requisitos. Certifique-se também de que o servidor que irá hospedar o novo site secundário satisfaz todos os pré-requisitos para utilização como servidor de site secundário.  

- Ao instalar o site secundário, o Gestor de Configuração configura o novo site para utilizar as portas de comunicação do cliente que estão configuradas no local principal dos pais.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a>Processo para instalar um site secundário  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site que será o local principal do novo local secundário.  

2. Para iniciar o Assistente do **Site Secundário Criar,** escolha **criar o Sítio Secundário** na fita.  

3. Na página **Antes de Começar,** confirme que o site principal listado é o site que pretende ser o pai do novo site secundário. Em seguida, escolha **Next**.  

4. Na página **Geral** , especifique as seguintes definições:  

    - **Código**do site : Cada código de site numa hierarquia deve ser único. Utilize três dígitos alfa-numéricos: A a Z e 0 a 9. Como o código do site é usado em nomes de pastas, não utilize nomes reservados ao Windows, incluindo:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > A configuração não verifica se o código do site que especifica já está a ser utilizado, ou se é um nome reservado.  

    - **Nome**do servidor do site : Este valor é o FQDN do servidor onde o novo site secundário irá instalar.  

    - **Nome**do site : Cada site requer este nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: Esta pasta é o caminho para a instalação do Gestor de Configuração. Não pode alterar a localização depois da instalação do site. O caminho não pode conter caracteres Unicode ou espaços de fuga.  

    > [!IMPORTANT]  
    > Depois de especificar detalhes nesta página, pode escolher **resumo** para ir diretamente para a página **sumária** do assistente. Esta ação utiliza as definições predefinidas para o resto das opções do site secundário.  
    > 
    > - Utilize apenas esta opção quando estiver familiarizado com as definições predefinidas neste assistente, e são as definições que pretende utilizar.  
    > - Quando utiliza as definições predefinidas, os grupos de limites não estão associados ao ponto de distribuição. Até configurar grupos de limites que incluam o servidor de site secundário, os clientes não usarão o ponto de distribuição instalado neste site secundário como uma localização de fonte de conteúdo.  

5. Na página Ficheiros fonte de **instalação,** escolha como o computador do site secundário obtém ficheiros de origem para a instalação do site.  

    Quando usar CD. Os ficheiros de origem mais recentes que são partilhados na rede ou copiados localmente para o servidor de site secundário alvo:  

    - **Versão 1802 e mais cedo**

        - O CD. A última localização do ficheiro de origem inclui uma pasta chamada **Redist**. Mova esta pasta **Redist** como subpasta sob a pasta **SMSSETUP.**  

            > [!Note]  
            > Se ocorrerem erros de incompatibilidade de hash durante a configuração, atualize a pasta **Redist.** Utilize o Downloader de [Configuração](setup-downloader.md) para obter os ficheiros mais recentes. Para quaisquer ficheiros que causem um erro de incompatibilidade de hash, copie-os também da pasta **Redist** atualizada para a pasta **SMSSETUP\BIN\X64.**

    - **Versão 1806 e mais tarde**<!-- SCCMDocs-pr issue 3164 -->

        - O CD. A última localização do ficheiro de origem inclui uma pasta chamada **Redist**. Mova esta pasta **Redist** como subpasta sob a pasta **SMSSETUP.**  

        - Copie os seguintes ficheiros da pasta **Redist** para a pasta **SMSSETUP\BIN\X64:**  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Se algum dos ficheiros do **Redist** não estiver disponível, a Configuração não instala o site secundário.  

    - A conta de computador do servidor de site secundário deve ter **permissões de leitura** na pasta de ficheiros de origem e partilhar.  

6. Na página de Definições do **Servidor SQL,** especifique a versão do Servidor SQL para utilizar e, em seguida, configure as definições relacionadas.  

    > [!NOTE]  
    > A configuração não valida a informação que introduz nesta página até iniciar a instalação. Antes de continuar, verifique estas definições.  

    - **Instale e configure uma cópia local do SQL Express no computador do site secundário**  

        - Porta de serviço do **servidor SQL**: Especifique a porta de serviço SQL Server para o SQL Server Express utilizar. A porta de serviço é tipicamente configurada para utilizar a porta TCP 1433, mas pode configurar outra porta.  

        - Porta de corretor de **servidorS SQL**: Especifique a porta SQL Server Broker (SSB) para o SQL Server Express utilizar. O Corretor de Serviços é tipicamente configurado para utilizar a porta TCP 4022, mas pode configurar uma porta diferente. Especifique uma porta válida que nenhum outro site ou serviço está a usar, e que não estão a bloquear quaisquer restrições de firewall.  

    - **Use uma instância de Servidor SQL existente**  

        - **SQL Server FQDN**: Reveja o FQDN para o computador que executa o Servidor SQL. Tem de utilizar um servidor local que executa o SQL Server para alojar a base de dados do site secundário e não pode modificar esta definição.  

        - **Instância do Servidor SQL**: Especifique a instância do Servidor SQL para utilizar como base de dados de site secundário. Deixe esta opção em branco para utilizar a instância predefinida.  

        - Nome da base de dados do **site ConfigMgr**: Especifique o nome a utilizar para a base de dados do site secundário.  

        - Porta de corretor de **servidorS SQL**: Especifique a porta SQL Server Broker (SSB) para o Servidor SQL utilizar. Especifique uma porta válida que nenhum outro site ou serviço está a usar, e que nenhuma restrição de firewall bloqueia.  

    > [!TIP]  
    > Para obter uma lista das versões do SQL Server que o Gestor de Configuração suporta, consulte [as versões Suportadas Do Servidor SQL](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. Na página ponto de **distribuição,** configure as definições para o ponto de distribuição que será instalado no servidor do site secundário.  

    - **Definições necessárias:**  

        - **Especifique como os dispositivos clientes comunicam com o ponto de distribuição**: Escolha entre HTTP e HTTPS.  

        - **Crie um certificado auto-assinado ou importe um certificado**de cliente PKI : Escolha entre usar um certificado auto-assinado ou importar um certificado do seu PKI. Um certificado auto-assinado permite também que as ligações anónimas dos clientes do Gestor de Configuração possam ir à biblioteca de conteúdos. O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão antes que o ponto de distribuição envie mensagens de estado. Para mais informações, consulte os requisitos do [certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Configurações opcionais:**  

        - **Instale e configure o IIS se necessário pelo Gestor**de Configuração : Selecione esta definição para permitir que o Gestor de Configuração instale e configure os Serviços de Informação de Internet (IIS) no servidor, se ainda não estiver instalado. O IIS é necessário em todos os pontos de distribuição.  

            > [!NOTE]  
            > Embora esta definição seja opcional, o IIS deve ser instalado no servidor antes de um ponto de distribuição poder ser instalado com sucesso.  

        - **Ativar e configurar BranchCache para este ponto de distribuição**  

        - **Descrição**: Este valor é uma descrição amigável para o ponto de distribuição para ajudá-lo a reconhecê-lo.  

        - **Ativar este ponto de distribuição para conteúdo pré-encenado**  

8. Na página **'Definições de Unidade',** especifique as definições de unidade para o ponto de distribuição do site secundário.  

    Pode configurar até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha do pacote. No entanto, o Gestor de Configuração pode utilizar unidades adicionais quando os dois primeiros chegarem à reserva de espaço de acionamento configurado. A página **'Definições de Accionamento'** é onde configura a prioridade para as unidades de disco e a quantidade de espaço de disco livre para permanecer em cada unidade de disco.  

    - Reserva de espaço de **acionamento (MB)**: O valor que configura para esta definição determina a quantidade de espaço livre numa unidade antes que o Gestor de Configuração escolha uma unidade diferente e continue o processo de cópia para essa unidade. Os ficheiros de conteúdo podem abranger várias unidades.  

    - **Localização do Conteúdo**: Especifique os locais de conteúdo para a biblioteca de conteúdos e a partilha de pacotes. O Gestor de Configuração copia o conteúdo para a localização do conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para a **reserva espacial Drive (MB)**.  

    Por predefinição, as localizações do conteúdo estão definidas como **Automáticas**. A localização do conteúdo primário está definida para a unidade de disco que tem mais espaço em disco no tempo de instalação. A localização secundária está definida para a unidade de disco que tem o espaço de disco mais livre após a unidade primária. Quando as unidades primárias e secundárias chegam à reserva de espaço de acionamento, o Select Manager seleciona outra unidade disponível com o espaço de disco mais livre e continua o processo de cópia.  

9. Na página de Validação de **Conteúdos,** especifique se valida a integridade dos ficheiros de conteúdo no ponto de distribuição.  

    - Quando ativa a validação de conteúdos numa programação, o Gestor de Configuração inicia o processo na hora programada. Todos os conteúdos do ponto de distribuição são verificados.  

    - Também pode configurar a prioridade de validação de **Conteúdos.**  

    - Para ver os resultados do processo de validação de conteúdos, na consola do Gestor de Configuração, vá ao espaço de trabalho **de Monitorização,** expanda o Estado de **Distribuição**e selecione o nó de Estado de **Conteúdo.** Exibe o conteúdo de cada tipo de embalagem. Estes tipos incluem aplicações, pacotes de atualização de software e imagens de arranque.  

10. Na página dos **Grupos de Fronteiras,** gerencie os grupos de fronteira a que este ponto de distribuição é atribuído:  

    - Durante a implementação de conteúdos, os clientes devem estar num grupo de limites associado ao ponto de distribuição para usá-lo como local de origem para o conteúdo.  

    - Pode selecionar a localização de **origem de recuo para** a opção de conteúdo para permitir que os clientes fora destes grupos de fronteira recuem e utilizem o ponto de distribuição como local de origem para conteúdos quando não existem pontos de distribuição preferidos.  

        Para mais informações, consulte os [conceitos Fundamentais para a gestão](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)de conteúdos.  

11. Na página **Resumo,** verifique as definições e escolha **o Próximo** para instalar o site secundário. Quando o assistente apresentar a página **Conclusão,** pode fechar o assistente. A instalação do local secundário continua em segundo plano.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a>Como verificar o estado de instalação do local secundário  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site secundário que está a instalar e, em seguida, escolha o Estado de **Instalação** do Show na fita.  

    > [!TIP]  
    > Quando instala mais de um local secundário de cada vez, o Verificador Pré-Requisito corre contra um único site de cada vez. Deve terminar um site antes de começar a verificar o próximo local.  
