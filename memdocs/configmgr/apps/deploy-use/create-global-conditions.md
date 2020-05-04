---
title: Criar condições globais
titleSuffix: Configuration Manager
description: Crie condições globais para especificar como uma aplicação é fornecida e implantada em dispositivos de cliente.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710287"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Como criar condições globais no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

No Gestor de Configuração, as condições globais são regras que representam condições comerciais ou técnicas que pode utilizar para especificar como uma aplicação é fornecida e implementada para dispositivos clientes. O acesso às condições globais é efetuado na página **Requisitos** do Assistente para Criar Tipo de Implementação.  

> [!NOTE]  
>  Só é possível editar as condições globais a partir do local onde foram criadas.  

 Utilize os seguintes procedimentos para criar condições globais do Gestor de Configuração.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fornecer informações básicas sobre a condição global  
 Existem vários tipos diferentes de condições globais. Aos diferentes tipos de condições globais estão associadas opções diferentes. Ao selecionar um tipo de condição global específico, o Gestor de Configuração mostra as opções que se aplicam à sua seleção.  

1.  Na consola de Configuração Manager, escolha > **condições globais**de gestão de > **aplicações**da Biblioteca de **Software.**  

3.  No separador **Home,** no grupo **Criar,** escolha **Criar Condição Global**.  

4.  Na caixa de diálogo **Criar Condição Global** , forneça um nome e uma descrição opcional para a condição global.  

5.  Na lista de desativação do **tipo Dispositivo,** escolha se a condição global é para um computador **Windows** ou um dispositivo **Windows Mobile.**  

6.  Na lista pendente **Tipo de Condição** , escolha uma das seguintes opções:  

    -   **Definição** – esta opção verifica a existência de um ou mais itens em dispositivos cliente. Por exemplo, pode verificar se existe um valor de chave de ficheiro, pasta ou registo num dispositivo cliente.  

    -   **Expressão** – Esta opção permite-lhe configurar regras mais complexas para verificar se a condição está satisfeita nos dispositivos do cliente. Por exemplo, pode verificar se a memória física de um computador está entre 2 GB e 4 GB ou se um dispositivo móvel utiliza a entrada do ecrã tátil.  

## <a name="set-up-rules-for-the-global-condition"></a>Estabelecer regras para a condição global  
 O procedimento para definir as regras de condição global é diferente dependendo se está a configurar uma definição ou uma expressão. Utilize aqui o procedimento aplicável para criar uma configuração ou expressão para a condição global.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Para criar um cenário para a condição global  

1. Na lista pendente **Tipo de Condição** , escolha **Definição**.  

2. Na lista pendente **Tipo de definição** , escolha o item a utilizar como a condição para a qual os requisitos serão verificados. Estão disponíveis os seguintes tipos e configurações de definição.  

   - **Consulta do Active Directory**  

     -   **Prefixo LDAP** - especifique um prefixo LDAP válido para a consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente. Pode utilizar **LDAP://** ou **GC://**.  

     -   **Nome distinto (DN)** - Especifique o nome distinto do objeto De serviços de domínio de diretório ativo que será avaliado para o cumprimento dos computadores clientes.  

     -   **Filtro de procura** - especifique um filtro de LDAP opcional para refinar os resultados da consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente.  

     -   **Âmbito da procura** - especifique o âmbito da procura nos Serviços de Domínio do Active Directory:  

         -   **Base** - Consultas apenas ao objeto especificado.  

         -   **One Level** - Esta opção não é utilizada nesta versão do Gestor de Configuração.  

         -   **Subtree** - Consultas o objeto especificado e a sua subárvore completa no diretório.  

     -   **Propriedade** - especifique a propriedade do objeto dos Serviços de Domínio do Active Directory que será utilizada para avaliar a compatibilidade em computadores cliente.  

     -   **Consulta** - Mostra a consulta LDAP que é construída a partir das entradas no **prefixo LDAP,** **nome distinto (DN)**, **Filtro** de Pesquisa se especificado, e **Propriedade**. Esta consulta será utilizada para avaliar a compatibilidade em computadores cliente.  

   - **Assemblagem**  

     -   **Nome da assemblagem** - Especifica o nome do objeto de assemblagem a procurar. O nome não pode ser o mesmo que qualquer outro objeto de montagem do mesmo tipo, e o nome deve ser registado no Cache de Montagem Global. O nome da montagem pode ser no máximo 256 caracteres.  

     > [!NOTE]  
     >  Uma assemblagem é um fragmento de código que pode ser partilhado entre aplicações. Os conjuntos podem ter a extensão do nome do ficheiro .dll ou .exe. A Global Assembly Cache é uma pasta denominada *%systemroot%\assembly* em computadores cliente em que todas as assemblagens partilhadas são armazenados.  

   - **Sistema de ficheiros**  

     - **Digite** – A partir da lista de lançamentos, escolha se pretende procurar um **Ficheiro** ou uma **Pasta**.  

     - **Caminho** – especifique o caminho da pasta ou do ficheiro especificado nos computadores cliente. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no caminho.  

       > [!NOTE]  
       >  Se utilizar a variável de ambiente *%USERPROFILE%* no campo **Caminho** ou **Nome da pasta ou ficheiro** , a procura será efetuada em todos os perfis de utilizador do computador cliente. Isto pode resultar na deteção de várias instâncias do ficheiro ou pasta.  

     - **Nome da pasta ou ficheiro** – especifique o nome do objeto de ficheiro ou de pasta que será procurado. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no nome da pasta ou ficheiro. Também pode usar o * e? wildcards no nome do arquivo.  

       > [!NOTE]  
       >  Se especificar um nome de ficheiro ou de pasta e utilizar carateres universais, isto poderá produzir um elevado número de resultados. Isto poderia resultar numa utilização elevada de recursos no computador cliente e no tráfego de rede elevado ao reportar resultados ao Gestor de Configuração.  

     - **Incluir subpastas** – ative esta opção se também pretender procurar em todas as subpastas do caminho especificado.  

     - **Este ficheiro ou pasta está associado a uma aplicação de 64 bits** - Escolha se a localização do ficheiro do sistema de 64 bits *(%windir%* \system32) deve ser pesquisada para além da localização do ficheiro do sistema de 32 bits *(%windir%* \syswow64) nos clientes do Gestor de Configuração que executam uma versão de 64 bits do Windows.  

       > [!NOTE]  
       >  Se o mesmo ficheiro ou pasta existir em ambas as localizações no mesmo computador de 64 bits, serão detetados múltiplos ficheiros pela condição global.  

       O tipo de definição **Sistema de ficheiros** não suporta a especificação de um caminho UNC de partilha de rede no campo **Caminho** .  

   - **Metabase do IIS**  

     -   **Caminho da metabase** - especifique um caminho válido para a Metabase do IIS.  

     -   **ID da Propriedade** - especifique a propriedade numérica da definição da Metabase do IIS.  

   - **Chave de registo**  

     -   **Hive** – A partir da lista de abandono, escolha a colmeia de registo que pretende pesquisar.  

     -   **Chave** – especifique o nome da chave de registo que pretende procurar. O formato utilizado deve ser *chave\subchave*.  

     -   **Esta chave de registo está associada a uma aplicação de 64 bits** – especifica se a procura deve ser efetuada nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

         > [!NOTE]  
         >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global detetará ambas as chaves de registo.  

   - **Valor de registo**  

     -   **Ramo** – na lista pendente, selecione o ramo do registo em que pretende procurar.  

     -   **Chave** – especifique o nome da chave de registo que pretende procurar. O formato utilizado deve ser *chave\subchave*.  

     -   **Valor** – especifique o valor que deve estar incluído na chave de registo especificada.  

     -   **Esta chave de registo está associada a uma aplicação de 64 bits** – especifica se a procura deve ser efetuada nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

         > [!NOTE]  
         >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global detetará ambas as chaves de registo.  

   - **Script**  

     -   **Discovery script** – Escolha **Adicionar** para introduzir ou navegar no script para usar. Pode utilizar scripts Windows PowerShell, VBScript ou JScript.  

     -   **Executar scripts utilizando as credenciais de utilizador registadas** – Se ativar esta opção, o script será executado em computadores clientes utilizando as credenciais do utilizador que está inscrito.  

         > [!NOTE]  
         >  O valor devolvido pelo script será utilizado para avaliar a compatibilidade da condição global. Por exemplo, quando utilizar o VBScript, pode utilizar o comando **WScript.Echo Result** para devolver o valor variável resultado à condição global.  
         >   
         >  Se o seu script devolver vários valores, estes valores devem estar numa única linha e separados com um ponto e vírgula. Se cada valor estiver numa linha separada, a avaliação irá falhar.  

   - **Consulta SQL**  

     -   **Instância do SQL Server** – escolha se pretende que a consulta SQL seja executada na instância predefinida, em todas as instâncias ou na instância de base de dados com o nome especificado.  

         > [!NOTE]  
         >  O nome da instância deve referir-se a uma instância local do SQL Server. Para fazer referência a uma instância do SQL Server em cluster, deverá utilizar uma definição de script.  

     -   **Base de dados** – especifique o nome da base de dados do Microsoft SQL Server relativamente à qual será executada a consulta SQL.  

     -   **Coluna** – especifique o nome da coluna devolvido pela instrução Transact-SQL a utilizar para avaliar a compatibilidade da condição global.  

     -   **Instrução Transact-SQL** – especifique a consulta SQL completa a utilizar para a condição global. Também pode escolher **o Open** para abrir uma consulta SQL existente.  

   - **Consulta WQL**  

     -   **Espaço de nomes** - especifique o espaço de nomes WMI que será utilizado para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente. O valor predefinido é Root\cimv2.  

     -   **Classe** - especifica a classe WMI que será utilizada para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente.  

     -   **Propriedade** - especifica a propriedade WMI que será utilizada para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente.  

     -   **Cláusula WHERE da consulta WQL** - pode utilizar o item **Cláusula WHERE da consulta WQL** para especificar uma cláusula WHERE a aplicar ao espaço de nomes, à classe e à propriedade especificados nos computadores cliente.  

   - **Consulta XPath**  

     -   **Caminho** - especifique o caminho para o ficheiro XML em computadores cliente que serão utilizados para avaliar a compatibilidade. O Gestor de Configuração suporta a utilização de todas as variáveis ambientais do sistema Windows e a variável de utilizador *%USERPROFILE%* no nome do caminho.  

     -   Nome do **ficheiro XML** - Especifique o nome do ficheiro que contém a consulta XML para avaliar a conformidade nos computadores dos clientes.  

     -   **Incluir subpastas** - Ative esta opção se também pretender pesquisar quaisquer subpastas no caminho especificado.  

     -   **Este ficheiro está associado a uma aplicação de 64 bits** - Escolha se a localização do ficheiro do sistema de 64 bits *(%windir%* \system32) deve ser pesquisada para além da localização de ficheiros do sistema de 32 bits *(%windir%* \syswow64) em clientes do Gestor de Configuração que executam uma versão de 64 bits do Windows.  

     -   **Consulta XPath** - especifique uma consulta da linguagem XPath completa e válida a utilizar para avaliar a compatibilidade em computadores cliente.  

     -   **Espaços de Nomes** - abre a caixa de diálogo **Espaços de Nomes XML** para identificar espaços de nomes e prefixos a utilizar durante a consulta XPath.  

3. Na lista pendente **Tipo de dados** , escolha o formato em que os dados serão devolvidos pela condição, antes da sua utilização para verificar os requisitos.  

   > [!NOTE]  
   >  A lista de desativação do **tipo Data** não é mostrada para todos os tipos de definição.  

4. Configurar mais detalhes sobre esta definição abaixo da lista de drop-down do **tipo Definição.** Os itens que pode configurar variarão dependendo do tipo de definição que selecionou.  

5. Escolha **OK** para salvar a regra e fechar a caixa de diálogo **Create Global Condition.**  

### <a name="set-up-an-expression-for-the-global-condition"></a>Criar uma expressão para a condição global  

1.  Na lista pendente **Tipo de Condição** , escolha **Expressão**.  

2.  Escolha **adicionar cláusula** para abrir a caixa de diálogo da Cláusula de **Adição.**  

3.  Na lista pendente **Selecionar categoria** , selecione se esta expressão se destina a um dispositivo ou um utilizador. Em alternativa, selecione **Personalizado** para utilizar uma condição global configurada anteriormente.  

4.  Na lista pendente **Selecione uma condição** , selecione a condição a utilizar para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. O conteúdo desta lista varia consoante a categoria selecionada.  

5.  Na lista pendente **Selecione operador** , escolha o operador que será utilizado para comparar a condição selecionada com o valor especificado para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. Os operadores disponíveis variam consoante a condição selecionada.  

6.  No campo **Valor** , especifique os valores que serão utilizados com a condição e o operador selecionados para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. Os valores disponíveis variam consoante a condição selecionada e o operador selecionado.  

7.  Escolha **OK** para salvar a expressão e fechar a caixa de diálogo **da Cláusula de Adição.**  

8.  Quando terminar de adicionar cláusulas à condição global, escolha **OK** para fechar a caixa de diálogo **Create Global Condition** e para salvar a condição global.  
