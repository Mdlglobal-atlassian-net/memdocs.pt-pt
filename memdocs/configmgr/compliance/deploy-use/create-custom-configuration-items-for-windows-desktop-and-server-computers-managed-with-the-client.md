---
title: Criar itens de configuração personalizados
titleSuffix: Configuration Manager
description: Gerir as definições para computadores e servidores windows com um item de configuração personalizado para desktops e servidores do Windows
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f11066918854d72af0f1160d7d7569a93d7ebe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712387"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Criar itens de configuração personalizados para computadores de desktop e servidor do Windows geridos com o cliente do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


Utilize o dispositivo de configuração personalizado do Gestor de Configuração **do Windows e servidores** para gerir as definições para computadores windows e servidores que são geridos pelo cliente do Gestor de Configuração.  



## <a name="start-the-wizard"></a>Inicie o assistente

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione o nó de Itens de **Configuração.**  

2. No separador **Casa** da fita, no grupo **Criar,** selecione **Create Configuration Item**.  

3. Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

4. Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Servidores e Computadores de Secretária Windows (personalizado)**.  

    > [!TIP]  
    > Se pretender fornecer as definições do método de deteção que verificam a existência de uma aplicação, selecione **Este ficheiro de configuração contém as definições da aplicação**.  

5. Para ajudá-lo a pesquisar e filtrar itens de configuração na consola do Gestor de Configuração, selecione **Categorias** para criar e atribuir categorias.  



## <a name="detection-methods"></a>Métodos de deteção  

Utilize este procedimento para fornecer informações do método de deteção para o item de configuração.  

> [!NOTE]  
> Esta informação só se aplica se selecionar este item de **configuração contém definições** de aplicação na página **geral** do assistente.  

Um método de deteção no Gestor de Configuração contém regras que são usadas para detetar se uma aplicação é instalada num computador. Esta deteção ocorre antes de o cliente avaliar a sua conformidade com o item de configuração. Para detetar se uma aplicação está instalada, pode detetar a presença de um ficheiro do Windows Installer para a aplicação, utilizar um script personalizado ou selecionar **Assumir sempre que a aplicação está instalada** para avaliar o item de configuração relativamente à compatibilidade, independentemente se a aplicação está instalada.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detetar uma instalação de aplicação utilizando o ficheiro Instalador do Windows  

1. Na página **métodos** de deteção do assistente de **configuração create**configuração, selecione a opção de utilizar a deteção do **instalador do Windows**.  

2. Selecione **Abrir,** navegue no ficheiro Do Instalador do Windows (.msi) que pretende detetar e, em seguida, selecione **Open**.  

3. O campo **Versão** preenche automaticamente com o número de versão do ficheiro Instalador do Windows. Se o valor apresentado estiver incorreto, introduza aqui um novo número de versão.  

4. Se pretender detetar cada perfil de utilizador no computador, selecione **Esta aplicação está instalada para um ou mais utilizadores**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detetar uma aplicação e um tipo de implementação específicos  

1. Na página **métodos** de deteção do Assistente de **Configuração Criar,** selecione para **detetar uma aplicação específica e tipo**de implementação . Escolha **Selecionar**.   

2. Na caixa de diálogo **Especificar Aplicação**, selecione a aplicação e um tipo de implementação associados que pretende detetar.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detetar uma instalação de aplicações utilizando um script personalizado  

1. Na página métodos de **deteção** do Assistente de **Configuração Criar,** selecione a opção de **utilizar um script personalizado para detetar esta aplicação**.  

2. Na lista, selecione o idioma do script. Escolha entre os seguintes formatos:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > A partir da versão 1810, quando um script do Windows PowerShell funciona como `-NoProfile` um método de deteção, o cliente do Gestor de Configuração chama powerShell com o parâmetro. Esta opção inicia a PowerShell sem perfis. Um perfil PowerShell é um script que corre quando o PowerShell começa. <!--3607762-->  

3. Selecione **Abrir,** navegue no script que pretende utilizar e, em seguida, **selecione Open**.  



## <a name="specify-supported-platforms"></a>Especificar plataformas suportadas  

Na página das **Plataformas Suportadas** do Assistente de **Configuração Criar,** selecione as versões do Windows nas quais pretende que o item de configuração seja avaliado para conformidade, ou escolha **Selecione tudo**.

Também pode **especificar manualmente a versão do Windows**. Selecione **Adicionar** e especificar cada parte do número de construção do Windows.

> [!NOTE]
> Ao especificar o Windows Server 2016, a seleção também `All Windows Server 2016 and higher 64-bit)` inclui o Windows Server 2019. Para especificar apenas o Windows Server 2016, utilize a opção para **especificar manualmente a versão do Windows**. <!--5866480-->



##  <a name="configure-settings"></a>Configurar definições  

Utilize este procedimento para configurar as definições no item de configuração.  

As definições representam as condições empresariais ou técnicas utilizadas para avaliar a compatibilidade nos dispositivos cliente. Pode configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

1. Na página **Definições** do Assistente de **Configuração Criar,** selecione **New**.  

2. No separador **Geral** da caixa de diálogo **Criar Definição**, forneça as seguintes informações:  

    - **Nome**: Introduza um nome único para a definição. Pode utilizar até 256 carateres.  

    - **Descrição**: Introduza uma descrição para a definição. Pode utilizar até 256 carateres.  

    - **Tipo de definição**: Na lista, escolha e configure um dos seguintes tipos de definição a utilizar para esta definição:  
        - [Consulta do Active Directory](#bkmk_adquery)
        - [Assemblagem](#bkmk_assembly)
        - [Sistema de ficheiros](#bkmk_file)
        - [Metabase do IIS](#bkmk_iis)
        - [Chave de registo](#bkmk_regkey)
        - [Valor de registo](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Consulta SQL](#bkmk_sql)
        - [Consulta WQL](#bkmk_wql)
        - [Consulta XPath](#bkmk_xpath)

    - Tipo de **dados:** Escolha o formato em que a condição devolve os dados antes de ser utilizado para avaliar a definição. A lista de **tipos de Dados** não é apresentada para todos os tipos de definição.  

        > [!Tip]  
        > O tipo de dados **de ponto flutuante** suporta apenas três dígitos após o ponto decimal.  

3. Configure detalhes adicionais sobre esta definição na lista **Tipo de definição**. Os itens que pode configurar variam consoante o tipo de definição que selecionou.  

4. Selecione **OK** para salvar a definição e feche a caixa de diálogo **Create Definição.**  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a>Consulta de Diretório Ativo

- **Prefixo LDAP**: Especifique um prefixo válido para a consulta de Serviços de Domínio do Diretório Ativo para avaliar a conformidade nos computadores dos clientes. Para fazer uma pesquisa global `LDAP://` `GC://`de catálogo, use ou .  

- **Nome Distinto (DN)**: Especifique o nome distinto do objeto de Serviços de Domínio do Diretório Ativo que é avaliado para o cumprimento dos computadores clientes.  

- **Filtro de pesquisa**: Especifique um filtro LDAP opcional para refinar os resultados da consulta dos Serviços de Domínio do Diretório Ativo para avaliar a conformidade nos computadores dos clientes. Para devolver todos os resultados `(objectclass=*)`da consulta, insira .  

- **Âmbito de pesquisa**: Especificar o âmbito de pesquisa nos Serviços de Domínio de Diretório Ativo  

    - **Base**: Consultas apenas ao objeto especificado  

    - **One Level**: Esta opção não é usada nesta versão do Gestor de Configuração  

    - **Subtree**: Consultas ao objeto especificado e à sua subárvore completa no diretório  

- **Propriedade**: Especifique a propriedade do objeto Ative Directory Domain Services que é usado para avaliar a conformidade nos computadores dos clientes.  

    Por exemplo, se quiser consultar a propriedade Do Diretório Ativo que armazena o `badPwdCount` número de vezes que um utilizador insere incorretamente uma palavra-passe, introduza neste campo.  

- **Consulta**: Exibe a consulta construída a partir das entradas no **prefixo LDAP,** **nome distinto (DN)**, **Filtro de Pesquisa** (se especificado) e **Propriedade**.  


### <a name="assembly"></a><a name="bkmk_assembly"></a>Montagem

Uma assemblagem é um fragmento de código que pode ser partilhado entre aplicações. As assemblagens podem ter a extensão de nome de ficheiro .dll ou .exe. A cache de montagem `%SystemRoot%\Assembly` global é a pasta nos computadores dos clientes. Esta cache é onde o Windows armazena todas as assembleias partilhadas.  

- **Nome da assemblagem:** especifica o nome do objeto de assemblagem a procurar. O nome não pode ser o mesmo que outros objetos de montagem do mesmo tipo. Primeiro registe-o na cache de montagem global. O nome da assemblagem pode ter até 256 carateres.  


### <a name="file-system"></a><a name="bkmk_file"></a>Sistema de ficheiros

- **Tipo**: Na lista, selecione se pretende procurar um **Ficheiro** ou uma **Pasta**.  

- **Caminho**: Especifique o caminho do ficheiro ou pasta especificado nos computadores dos clientes. Pode especificar variáveis ambientais `%USERPROFILE%` do sistema e a variável ambiental no caminho.  

    > [!NOTE]  
    > Se utilizar `%USERPROFILE%` a variável ambiental nas caixas de nome **saque** ou **ficheiro ou de pasta,** o cliente do Gestor de Configuração procura todos os perfis do utilizador no computador cliente. Este comportamento pode resultar na descoberta de várias instâncias do ficheiro ou pasta.  
    >   
    > Se as definições de conformidade não tiverem acesso ao caminho especificado, gera-se um erro de descoberta. Além disso, se o ficheiro que está a procurar estiver atualmente em utilização, é gerado um erro de deteção.  

    > [!Tip]  
    > **Selecione Navegar** para configurar a definição a partir de valores num computador de referência.   

- **Nome de ficheiro ou pasta**: Especifique o nome do ficheiro ou do objeto de pasta para procurar. Pode especificar variáveis ambientais `%USERPROFILE%` do sistema e a variável ambiental no nome do ficheiro ou da pasta. Também pode utilizar os `*` `?` wildcards e o nome do ficheiro.  

    > [!NOTE]  
    > Se especificar um nome de ficheiro ou pasta e utilizar wildcards, esta combinação poderá produzir um elevado número de resultados. Também poderia resultar em uma utilização elevada de recursos no computador cliente, e tráfego de rede elevado ao reportar resultados ao Gestor de Configuração.  

- **Incluir subpastas**: Procure também quaisquer subpastas sob o caminho especificado.  

- **Este ficheiro ou pasta está associado a uma aplicação de 64 bits**: Se `%ProgramFiles%` ativado, procure apenas localizações de ficheiros de 64 bits, como em computadores de 64 bits. Se esta opção não estiver ativada, procure em ambos os locais `%ProgramFiles(x86)%`de 64 bits e em 32 bits, tais como .  

    > [!NOTE]  
    > Se o mesmo ficheiro ou pasta existir em ambas as localizações no mesmo computador de 64 bits, são detetados múltiplos ficheiros pela condição global.  

    O tipo de definição do **sistema de ficheiros** não suporta especificar um caminho unc para uma partilha de rede na caixa **Path.**  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a>Metabase IIS

- **Caminho de metabase**: Especifique um caminho válido para a metabase dos Serviços de Informação da Internet (IIS). Por exemplo, `/LM/W3SVC/`.  

- **ID da propriedade:** Especifique a propriedade numérica da definição de metabase IIS.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a>Chave de registo

- **Colmeia**: Selecione a colmeia de registo que pretende pesquisar

    > [!Tip]  
    > **Selecione Navegar** para configurar a definição a partir de valores num computador de referência. Para navegar numa chave de registo num computador remoto, ative o serviço **de Registo Remoto** no computador remoto.  

- **Chave**: Especifique o nome da chave do registo que pretende procurar. Utilize o formato `key\subkey`.  

- Esta chave de **registo está associada a uma aplicação de 64 bits**: Procure chaves de registo de 64 bits para além das chaves de registo de 32 bits nos clientes que estão a executar uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  


### <a name="registry-value"></a><a name="bkmk_regval"></a>Valor do registo

- **Colmeia**: Selecione a colmeia de registo para pesquisar.  

    > [!Tip]  
    > **Selecione Navegar** para configurar a definição a partir de valores num computador de referência. Para navegar por um valor de registo num computador remoto, ative o serviço **de Registo Remoto** no computador remoto. Também precisa de permissões de administrador para aceder ao computador remoto.  

- **Chave**: Especifique o nome da chave do registo para procurar. Utilize o formato `key\subkey`.  

- **Valor**: Especifique o valor que deve ser contido na chave de registo especificada.  

- Esta chave de **registo está associada a uma aplicação de 64 bits**: Procure as teclas de registo de 64 bits para além das chaves de registo de 32 bits nos clientes que estão a executar uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  


### <a name="script"></a><a name="bkmk_script"></a>Roteiro

O valor devolvido pelo script é utilizado para avaliar a compatibilidade da condição global. Por exemplo, quando utilizar VBScript, poderá utilizar o comando **WScript.Echo Result** para devolver o valor da variável *Result* à condição global.  

- **Discovery script**: Selecione **Adicionar Script**, e insira ou navegue para um script. Este guião é usado para encontrar o valor. Pode utilizar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Script de reparação (opcional)**: **Selecione Adicionar script**, e insira ou navegue para um script. Este script é utilizado para remediar valores de definição não conformes. Pode utilizar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Executar scripts utilizando as credenciais de utilizador registadas**: Se ativar esta opção, o script é executado em computadores clientes que utilizam as credenciais do utilizador inscrito.  

> [!Note]  
> A partir da versão 1810, quando utiliza o Windows PowerShell como um script de `-NoProfile` descoberta ou remediação, o cliente do Gestor de Configuração chama powerShell com o parâmetro. Esta opção inicia a PowerShell sem perfis. Um perfil PowerShell é um script que corre quando o PowerShell começa. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a>Consulta SQL

- **Instância do Servidor SQL**: Escolha se pretende que a consulta SQL seja executada na instância predefinida, em todas as instâncias ou num nome de instância de base de dados especificado.  

    > [!NOTE]  
    > O nome da instância deve referir-se a uma instância local do SQL Server. Para fazer referência a uma instância do SQL Server em cluster, deverá utilizar uma definição de script.  

- **Base de dados**: Especifique o nome da base de dados do Microsoft SQL Server contra a qual pretende executar a consulta SQL.  

- **Coluna**: Especifique o nome da coluna devolvido pela declaração Transact-SQL que é utilizada para avaliar a conformidade da condição global.  

- **Declaração Transact-SQL**: Especifique a consulta Completa sQL que pretende utilizar para a condição global. Para utilizar uma consulta SQL existente, selecione **Open**.  

    > [!IMPORTANT]  
    > As definições de consulta SQL não suportam quaisquer comandos SQL que modifiquem a base de dados. Apenas pode utilizar comandos SQL que leem as informações da base de dados.  


### <a name="wql-query"></a><a name="bkmk_wql"></a>Consulta WQL

- **Espaço de nome**: Especifique o espaço de nome WMI avaliado para a conformidade nos computadores dos clientes. O valor predefinido é `root\cimv2`.  

- **Classe**: Especifique a classe WMI alvo no espaço de nome acima.  

- **Propriedade**: Especifique a propriedade-alvo wMI na classe acima.  

- **Consulta WQL ONDE a cláusula**: Especifique uma cláusula de qualificação para reduzir os resultados. Por exemplo, só para consultar o serviço DHCP na classe `Name = 'DHCP' and StartMode = 'Auto'`Win32_Service, a cláusula WHERE poderia ser .   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a>Consulta XPath

- **Caminho**: Especifique o caminho do ficheiro .xml nos computadores clientes que é utilizado para avaliar a conformidade. O Gestor de Configuração suporta a utilização `%USERPROFILE%` de todas as variáveis ambientais do sistema Windows e a variável do utilizador no nome do caminho.  

- Nome do **ficheiro XML**: Especifique o nome do ficheiro que contém a consulta XML no caminho acima.  

- **Incluir subpastas**: Ative esta opção de pesquisar quaisquer subpastas sob o caminho especificado.  

- **Este ficheiro está associado a uma aplicação de 64 bits**: Procure a localização `%Windir%\System32` do `%Windir%\Syswow64` ficheiro do sistema de 64 bits para além da localização do ficheiro do sistema de 32 bits nos clientes do Gestor de Configuração que estão a executar uma versão de 64 bits do Windows.  

- **Consulta XPath**: Especifique uma consulta de percurso xml completa válida (XPath).  

- Espaços de **nomes**: Identifique espaços de nome e prefixos a utilizar durante a consulta XPath.  

Se tentar descobrir um ficheiro .xml encriptado, as definições de conformidade encontram o ficheiro, mas a consulta XPath não produz resultados. O cliente do Gestor de Configuração não gera um erro.  

Se a consulta XPath não for válida, a definição é avaliada como incompatível com os computadores dos clientes.  



##  <a name="configure-compliance-rules"></a>Configurar regras de compatibilidade  

As regras de compatibilidade especificam as condições que definem a compatibilidade de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, tem de ter, pelo menos, uma regra de compatibilidade. O WMI, o registo e as definições de script permitem remediar os valores considerados não compatíveis. Pode criar novas regras ou navegar para uma definição existente em qualquer item de configuração para selecionar regras no mesmo.  


### <a name="to-create-a-compliance-rule"></a>Para criar uma regra de compatibilidade  

1. Na página regras de **conformidade** do Assistente de **Configuração Criar,** selecione **New**.  

2. Na caixa de diálogo **Criar Regra**, forneça as seguintes informações:  

    - **Nome**: Introduza um nome para a regra de conformidade.  

    - **Descrição**: Introduza uma descrição para a regra de conformidade.  

    - **Definição selecionada**: **Selecione Procurar** para abrir a caixa de diálogo **Select Setting.** Selecione a definição para a qual pretende definir uma regra ou selecione **New Setting**. Quando terminar, escolha **Selecionar**.  

        > [!Tip]  
        > Para ver informações sobre a definição atualmente selecionada, selecione **Propriedades**.  

    - **Tipo**de regra : Selecione o tipo de regra de conformidade que pretende utilizar:  

        - **Valor**: Crie uma regra que compare o valor devolvido pelo item de configuração com um valor que especifica. Para obter mais informações sobre as definições adicionais, consulte [as regras de valor](#bkmk_value).  

        - **Existencial**: Crie uma regra que avalie a definição dependendo se existe num dispositivo cliente ou no número de vezes que encontra. Para obter mais informações sobre as definições adicionais, consulte [as regras existenciais.](#bkmk_exist)  

3. Selecione **OK** para fechar a caixa de diálogo **'Criar Regra'.**  




### <a name="value-rules"></a><a name="bkmk_value"></a>Regras de valor  

- **Propriedade**: A propriedade do objeto para verificar varia consoante a definição selecionada. As propriedades disponíveis variam em função do tipo de configuração. 

- **A definição deve estar em conformidade com o seguinte...**: As regras ou permissões disponíveis variam com base no tipo de definição.

- **Remediar regras não conformes quando suportadas**: Selecione esta opção para o Gestor de Configuração para remediar automaticamente as regras não conformes. O Gestor de Configuração suporta esta ação com os seguintes tipos de regras:  

    - **Valor do registo**: Se não for conforme, o cliente define o valor do registo. Se não existir, o cliente cria o valor.  

    - **Script**: O cliente utiliza o script de reparação que especificou com a definição.  

    - **Consulta WQL**  

    > [!IMPORTANT]  
    > Só pode remediar regras incompatíveis quando o operador de regra estiver definido como **É igual a**.  

- **Reportar incumprimento se esta definição não for encontrada**: Se esta definição não for encontrada nos computadores dos clientes, ative esta opção para que o item de configuração reporte o incumprimento.  

- **Severidade de incumprimento dos relatórios**: Especifique o nível de gravidade que é reportado nos relatórios do Gestor de Configuração se esta regra de conformidade falhar. Estão disponíveis os seguintes níveis de gravidade:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítica**  
    - **Crítico com evento**: Computadores que falham esta regra de conformidade reportam uma falha da **Critical**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a>Regras existenciais 

> [!NOTE]  
> As opções apresentadas podem variar dependendo do tipo de definição para o qual está a configurar uma regra.  

- **A definição tem de existir nos dispositivos cliente**  

- **A definição não pode existir nos dispositivos cliente**  

- **A definição ocorre o número de vezes seguinte:**  

- **Severidade de incumprimento dos relatórios**: Especifique o nível de gravidade que é reportado nos relatórios do Gestor de Configuração se esta regra de conformidade falhar. Estão disponíveis os seguintes níveis de gravidade:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítica**  
    - **Crítico com evento**: Computadores que falham esta regra de conformidade reportam uma falha da **Critical**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a>Reparações de itens de configuração de rastreio
<!--4261411-->
*(Introduzido na versão 2002)*

A partir da versão de 2002 do Gestor de Configuração, pode rastrear o histórico de **reparação quando suportado** nas regras de conformidade do seu item de configuração. Quando esta opção está ativada, qualquer reparação que ocorra no cliente para o item de configuração gera uma mensagem de estado. O histórico está armazenado na base de dados do Gestor de Configuração.

Construa relatórios personalizados para ver o histórico da reparação utilizando a visão do público **v_CIRemediationHistory**. A `RemediationDate` coluna é a hora, na UTC, o cliente fez a reparação. O `ResourceID` dispositivo identifica o dispositivo. Construir relatórios personalizados com a **vista v_CIRemediationHistory** ajuda-o:

- Identifique possíveis problemas com os seus scripts de reparação
- Encontre tendências em reparações como um cliente que não cumpra consistentemente cada ciclo de avaliação.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Ativar o histórico de reparação da pista quando for suportada opção

- Para novos itens de **configuração,** adicione o histórico de reparação da faixa quando for suportado a opção no separador Regras de **Conformidade** quando criar uma nova definição na página **Definições** do assistente.
- Para os itens de configuração existentes, adicione o histórico de **reparação** da faixa quando for suportado a opção no separador Regras de **Conformidade** no item de configuração **Propriedades**.
[![Histórico de reparação de faixas quando suportado na versão 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Passos seguintes

[Criar linhas de base de configuração](create-configuration-baselines.md)
