---
title: Instalar consola
titleSuffix: Configuration Manager
description: Instale a consola Do Gestor de Configuração para se ligar a um site de administração central ou ao local principal.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718239"
---
# <a name="install-the-configuration-manager-console"></a>Instale a consola de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os administradores utilizam a consola Do Gestor de Configuração para gerir o ambiente do Gestor de Configuração. Cada consola do Gestor de Configuração pode ligar-se a um site de administração central (CAS) ou a um site primário. Não é possível ligar uma consola de Configuração a um site secundário.

A consola 'Gestor de Configuração' está sempre instalada no servidor do site para o CAS ou para um site primário. Para instalar a consola separada mente da instalação do servidor do local, execute o instalador autónomo.  



## <a name="prerequisites"></a>Pré-requisitos

- Tem direitos de **administrador** local no computador-alvo para a consola.  

- Tem **permissões de leitura** para a localização dos ficheiros de instalação da consola Do Gestor de Configuração.  



## <a name="source-paths"></a>Caminhos-de-origem

Decida qual o caminho de origem a utilizar:  

- Pasta ConsoleSetup no servidor do site:`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Quando instala um servidor de site, copia os ficheiros de instalação da consola e suporta pacotes de idiomas para o site na subpasta **Tools\ConsoleSetup.** Opcionalmente, pode copiar a pasta **ConsoleSetup** para um local alternativo para iniciar a instalação. Ao atualizar o site, mantém sempre a versão local atualizada.  

- Meios de instalação do Gestor de Configuração:`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Instalar a consola 'Gestor de Configuração' a partir do meio de instalação instala sempre instala a versão inglesa. Este comportamento acontece mesmo que o servidor do site suporte diferentes idiomas, ou o SISTEMA do computador alvo é definido para um idioma diferente.  

Quando possível, ligue o instalador da consola a partir da pasta **ConsoleSetup** e não a partir dos meios de origem.

> [!Important]  
> Não instale a consola utilizando o **CD. Os últimos** ficheiros de origem. É um cenário não suportado, e pode causar problemas com a instalação da consola. Para mais informações, consulte [o CD. Última pasta.](../../manage/the-cd.latest-folder.md#unsupported-scenarios)<!-- SCCMDocs issue 1359 -->  

Se criar uma embalagem para instalar a consola noutros computadores, certifique-se de que a embalagem inclui os seguintes ficheiros:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (a partir da versão 1902)
- ConfigMgr.AC_Extension.amd64.cab (a partir da versão 1902)



## <a name="use-the-setup-wizard"></a>Utilizar o Assistente de Configuração  

1. Navegue pelo caminho de origem e abra **consoleSetup.exe**.  

    > [!IMPORTANT]  
    > Instale sempre a consola utilizando **consoleSetup.exe**. Embora possa instalar a consola Do Gestor de Configuração executando AdminConsole.msi, este método não executa pré-requisitos ou verificações de dependência. A instalação pode não ser instalada corretamente.  

2. No assistente, selecione **Seguinte**.  

3. Na página do Servidor do **Site,** introduza o nome de domínio totalmente qualificado (FQDN) do servidor do site ao qual a consola do Gestor de Configuração se liga.  

4. Na página da pasta de **instalação,** introduza a pasta de instalação para a consola 'Gestor de Configuração'. O caminho da pasta não pode incluir espaços de trailing ou caracteres Unicode.  

5. Na página do Programa de Melhoria da Experiência do **Cliente,** selecione se deve aderir ao Programa de Melhoria da Experiência do Cliente (CEIP).  

    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

6. Na página **Ready to Install,** selecione **Instalar**.  



## <a name="install-from-a-command-prompt"></a>Instalar a partir de um pedido de comando  

> [!TIP]  
> Instalar a consola 'Gestor de Configuração' a partir de um pedido de comando instala sempre a versão inglesa. Este comportamento acontece mesmo que o SISTEMA do computador-alvo esteja definido para uma linguagem diferente. Para instalar a consola 'Gestor de Configuração' num idioma diferente do inglês, utilize o Assistente de [Configuração](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Opções de linha de comando ConsoleSetup.exe

#### <a name="q"></a>/q

Instala a consola Do Gestor de Configuração sem vigilância. As opções **EnableSQM**, **TargetDir**e **DefaultSiteServerName** são necessárias quando utiliza esta opção.

#### <a name="uninstall"></a>/uninstall

Desinstala a consola 'Gestor de Configuração'. Especifique esta opção primeiro quando a utilizar com a opção **/q.**

#### <a name="langpackdir"></a>LangPackDir

Especifica o caminho para a pasta que contém os ficheiros linguísticos. Pode utilizar o Downloader de **Configuração** para descarregar os ficheiros de idioma. Se não utilizar esta opção, a Configuração procura a pasta de idiomas na pasta atual. Se a pasta de idioma não for encontrada, a Configuração continua a instalar apenas o inglês. Para mais informações, consulte O Downloader de [Configuração](setup-downloader.md).

#### <a name="targetdir"></a>DestinoDir

Especifica a pasta de instalação para instalar a consola 'Gestor de Configuração'. Esta opção é necessária quando utiliza a opção **/q.**

#### <a name="enablesqm"></a>EnableSQM

Especifica se deve aderir ao Programa de Melhoria da Experiência do Cliente (CEIP). Use um valor de **1** para aderir ao CEIP, e um valor de **0** para não aderir ao programa. Esta opção é necessária quando utiliza a opção **/q.**

> [!Important]  
> A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto. A utilização do parâmetro fará com que a instalação falhe.

#### <a name="defaultsiteservername"></a>Nome de servidor de site predefinido

Especifica o FQDN do servidor do site ao qual a consola se liga quando abre. Esta opção é necessária quando utiliza a opção **/q.**


### <a name="examples"></a>Exemplos

> [!Important]  
> Para a versão 1802 e mais tarde, não inclua o parâmetro **EnableSQM**

#### <a name="silent-install"></a>Instalação silenciosa

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Instalação silenciosa com pacotes de idiomas

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Desinstalação silenciosa

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Consulte também

Um administrador vê objetos na consola com base nas permissões atribuídas à sua conta de utilizador. Para obter mais informações, consulte os [fundamentos da administração baseada no papel.](../../../understand/fundamentals-of-role-based-administration.md)

Para obter mais informações sobre os fundamentos da navegação na consola do Gestor de Configuração, consulte [Utilizar a consola](../../manage/admin-console.md).
