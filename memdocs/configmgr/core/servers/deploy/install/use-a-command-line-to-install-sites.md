---
title: Instalação da linha de comando
titleSuffix: Configuration Manager
description: Aprenda a executar configuração do Gestor de Configuração num pedido de comando para uma variedade de instalações do site.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717959"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Utilize uma linha de comando para instalar sites do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Pode executar configuração do Gestor de Configuração a uma solicitação de comando para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas suportadas para instalações de linha de comando
 Este método de execução da Configuração suporta as seguintes tarefas de instalação e manutenção do local:

- **Instale um site de administração central ou local primário a partir de um pedido de comando**  
  Ver [opções de linha de comando para configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Modificar as línguas em uso num site de administração central ou local primário**  
   Para modificar as línguas que são instaladas num local a partir de um pedido de comando (incluindo idiomas para dispositivos móveis), deve:  

  - Executar Configuração a partir de ** &lt;ConfigMgrInstallationPath\>\Bin\X64** no servidor do site,
  - Utilize a opção linha de comando **/MANAGELANGS,**
  - Especifique um ficheiro de script de idioma que especifica os idiomas que pretende adicionar ou remover,  

    Por exemplo, utilize a seguinte sintaxe de comando: **configuraçãowpf.exe /MANAGELANGS &lt;ficheiro\> ** de script de idioma  

    Para criar o ficheiro script idioma, use a informação nas opções da [linha De comando para gerir idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Utilize um ficheiro de script de instalação para instalações não vigiadas ou recuperação do local**  
   Pode executar a Configuração a partir de um pedido de comando utilizando um script de instalação e executa uma instalação do local sem supervisão. Também pode usar esta opção para recuperar um site.    

   Para utilizar um script com configuração:  

  - Executar Configuração com a opção de linha de comando **/SCRIPT** e especificar um ficheiro script.  

  - O ficheiro script deve ser configurado com as teclas e valores necessários.  

    Para uma instalação não atendida de um site de administração central ou local primário, o ficheiro script deve ter as seguintes secções:  

  - Identificação    
  - Opções    
  - SQLConfigOptions    
    -   Hierárquios    
  - CloudConnectorOptions   

    Para recuperar um site, deve incluir também as seguintes secções do ficheiro script:  

  - Identificação  
  - Recuperação

Para mais informações, consulte a recuperação do [site não acompanhado para O Gestor de Configuração](../../manage/unattended-recovery.md).  

Para obter uma lista de teclas e valores a utilizar num ficheiro de script de instalação não vigiado, consulte as teclas de ficheiro de [configuração não atendidas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o ficheiro de script de linha de comando  
 Para instalações não atendidas do Gestor de Configuração, pode executar a Configuração com a opção linha de comando **/SCRIPT,** e especificar um ficheiro de script que contenha opções de instalação. As seguintes tarefas são apoiadas utilizando este método:  

-   Instale um site de administração central  
-   Instale um local primário  
-   Instale uma consola de gestor de configuração  
-   Recuperar um site  

> [!NOTE]  
>  Não é possível utilizar o ficheiro script sem supervisão para atualizar um site de avaliação para uma instalação licenciada de 'Gestor de Configuração'.  

### <a name="the-cdlatest-key-name"></a>O nome chave CDMais
Quando se usa os meios de comunicação do CD. Última pasta para executar uma instalação escrita das seguintes quatro opções de instalação, o seu script deve incluir a tecla **CDLatest** com um valor de **1**:
- Instale um novo site de administração central
- Instalar um novo local primário
- Recuperar um site de administração central
- Recuperar um local primário

Este valor não é suportado para utilização com suportes de instalação que obtém do site da Microsoft Volume License.
Consulte [as opções da linha de comando](command-line-options-for-setup.md) para obter informações sobre como utilizar este nome chave no ficheiro script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é automaticamente criado quando executa a [Configuração para instalar um site utilizando a interface do utilizador](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando confirma as definições na página **resumo** do assistente, acontece o seguinte:  

-   A configuração cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Pode renomear este ficheiro antes de o utilizar, mas deve manter a extensão do ficheiro .ini.  
-   O script de instalação sem supervisão contém as definições selecionadas no assistente.  
-   Após a criação do script, pode modificar o script para instalar outros sites na sua hierarquia.  
-   Em seguida, pode utilizar este script para realizar uma configuração não acompanhada de 'Configuração Manager'.  

Este ficheiro de script fornece as mesmas informações que o Assistente de Configuração solicita, exceto que não existem definições predefinidas.   
Deve especificar todos os valores das teclas de configuração que se aplicam ao tipo de instalação que está a utilizar.   

Quando a Configuração cria o script de instalação sem supervisão, é povoada com o valor chave do produto que introduz durante a Configuração. Esta pode ser uma chave de produto válida, ou **EVAL** quando instalar uma versão de avaliação do 'Gestor de Configuração'. O valor-chave do produto no script é povoado para que a verificação pré-requisito possa terminar.   

Quando a Configuração inicia a instalação do site real, o script criado automaticamente é escrito novamente para limpar o valor chave do produto no script que cria. Antes de utilizar o script para uma instalação não atendida de um novo site, pode editar o script para fornecer uma chave de produto válida ou especificar uma instalação de avaliação do Gestor de Configuração.  

### <a name="section-names-key-names-and-values"></a>Nomes de secção, nomes-chave e valores
O script contém nomes de secções, nomes de chaves e valores. Tenha em atenção as seguintes informações:
-   Os nomes de chaves de secção necessários variam dependendo do tipo de instalação que está a escrever.
-   A ordem das teclas dentro das secções e a ordem das secções dentro do ficheiro não é importante.     
-   As chaves não são sensíveis ao caso.  
-   Quando fornece valores para as teclas, o nome da chave deve ser seguido por um sinal igual (=) e o valor da chave.    

> [!TIP]  
>  Para ver o conjunto completo de opções, consulte [opções de linha de comando para Configuração e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Utilize a opção de linha de comando /SCRIPT Configuração

-   Deve utilizar um ficheiro de script de configuração e especificar o nome do ficheiro após a opção de linha de comando **/SCRIPT** Configuração. Tenha em atenção as seguintes informações:   
    -   O nome do ficheiro deve ter a extensão do nome do ficheiro **.ini.**  
    -   Quando fizer referência ao ficheiro de script configuração no pedido de comando, deve fornecer o caminho completo para o ficheiro. Por exemplo, se o ficheiro de inicialização de configuração for denominado Setup.ini, e for armazenado na pasta C:\Configuração, no pedido de comando, escreva: **configuração /script c:\setup\setup.ini**.  

-   A conta que executa a Configuração deve ter direitos **de administrador** no computador. Quando executar a Configuração com o script sem supervisão, abra a janela Command Prompt utilizando a **opção Executar como** opção de administrador.   
