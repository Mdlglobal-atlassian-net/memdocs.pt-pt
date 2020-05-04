---
title: Ferramenta de Manutenção da Hierarquia
titleSuffix: Configuration Manager
description: Entenda o que a Ferramenta de Manutenção da Hierarquia faz e por que pode usá-la. Inclui referência de opções de linha de comando.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712443"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Ferramenta de Manutenção da Hierarquia (Preinst.exe) para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A ferramenta de Manutenção da Hierarquia (Preinst.exe) passa comandos para o Gestor de Hierarquia do Gestor de Configuração enquanto o serviço de Gestor de Hierarquia está em execução. A ferramenta de manutenção da hierarquia é instalada automaticamente quando instala um site do Gestor de Configuração. Pode encontrar Preinst.exe \\ &lt;no *SiteServerName* &lt;>\SMS_*SiteCode*\bin\X64\00000409 pasta partilhada no servidor do site.  

 Pode utilizar a ferramenta Manutenção da Hierarquia nos seguintes cenários:  

-   Quando é necessária uma troca de chaves segura, existem situações em que é necessário efetuar manualmente a troca inicial de chaves públicas entre sites. Para obter mais informações, veja [Trocar Manualmente Chaves Públicas Entre Sites](#BKMK_ManuallyExchangeKeys), neste tópico.  

-   Para remover tarefas ativas destinadas a um site de destino que já não está disponível.  

-   Para eliminar um servidor de site da consola 'Gestor de Configuração' quando não é possível desinstalar o site utilizando a Configuração. Por exemplo, se remover fisicamente um site do Gestor de Configuração sem primeiro executar a Configuração para desinstalar o site, as informações do site continuarão a existir na base de dados do site dos pais, e o site dos pais continuará a tentar comunicar com o site da criança. Para resolver este problema, deve executar a ferramenta de manutenção da hierarquia e eliminar manualmente o site da criança da base de dados do site dos pais.  

-   Para parar todos os serviços do Gestor de Configuração num site sem ter de parar os serviços individualmente.  

-   Quando estiver a recuperar um site, pode utilizar a opção CHILDKEYS para distribuir as chaves públicas de vários sites subordinados para o site de recuperação.  

Para executar a ferramenta Manutenção da Hierarquia, o utilizador atual deve ter privilégios administrativos no computador local. De igual modo, o utilizador deve ter explicitamente o direito de segurança Site - Administrador. Não é suficiente que o utilizador herde este direito pelo facto de ser membro de um grupo que tem essa permissão.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opções da Linha de Comandos da Ferramenta Manutenção da Hierarquia  
Quando utilizar a Ferramenta Manutenção da Hierarquia, deve executá-la localmente no servidor do site de administração central, do site primário ou do site secundário.  

Quando executar a ferramenta de manutenção da hierarquia, deve utilizar a seguinte sintaxe: preinst.exe /&lt;opção\>. O que se segue são opções de linhas de comandos.  

 **/DELJOB &lt; *SiteCode* > ** - Utilize esta opção num site para eliminar todos os trabalhos ou comandos do site atual para o local de destino especificado.  

 **/DELSITE &lt; *ChildSiteCodeToRemove* > ** - Utilize esta opção num site dos pais para eliminar os dados relativos a sites infantis da base de dados do site principal. Normalmente, utilize esta opção se o computador de um servidor do site for encerrado antes de desinstalar o site desse computador.  

> [!NOTE]  
>  A opção /DELSITE não desinstala o site no computador especificado pelo parâmetro ChildSiteCodeToRemove. Esta opção apenas remove as informações do site da base de dados do Site Do Gestor de Configuração.  

**/DUMP &lt; *SiteCode* > ** - Utilize esta opção no servidor do site local para escrever imagens de controlo do site para a pasta raiz da unidade em que o site está instalado. Pode escrever uma imagem de controlo do site específica na pasta ou escrever todos os ficheiros de controlo do site na hierarquia.  

-   /DUMP &lt; *SiteCode*> escreve a imagem de controlo do site apenas para o site especificado.  

-   /DUMP escreve os ficheiros de controlo do site de todos os sites.  

Uma imagem é uma representação binária do ficheiro de controlo do site, que é armazenado na base de dados do Site Do Gestor de Configuração. A imagem de ficheiro de controlo do site capturada é a soma da imagem base com as imagens diferenciais pendentes.  

Depois de despejar uma imagem de ficheiro de controlo do site com&lt;a ferramenta de manutenção da hierarquia, o nome do ficheiro encontra-se no formato sitectrl_*SiteCode*>.ct0.  

**/STOPSITE** - Utilize esta opção no servidor do site local para iniciar um ciclo de encerramento para o serviço de Gestor de Componentes do Gestor de Configuração, que reinicia parcialmente o site. Quando este ciclo de paragem é executado, alguns serviços de Gestor de Configuração num servidor de site e seus sistemas de site remoto são interrompidos. Estes serviços são sinalizados para reinstalação. Devido a este ciclo de encerramento, algumas palavras-passe são alteradas automaticamente quando os serviços são reinstalados.  

> [!NOTE]  
>  Se pretender ver um registo de encerramento, reinstalação e alterações de palavras-passe do Gestor do Componentes do Site, ative o registo para este componente antes de utilizar esta opção da linha de comandos.  

Depois de ser iniciado, o ciclo de encerramento prossegue automaticamente, ignorando todos os componentes ou computadores sem resposta. No entanto, se o serviço Gestor de Componentes do Site não conseguir aceder a um sistema de sites remoto durante o ciclo de encerramento, os componentes instalados no sistema de sites remoto serão reinstalados quando o serviço Gestor de Componentes do Site for reiniciado. Quando é reiniciado, o serviço Gestor de Componentes do Site tenta repetidamente reinstalar todos os serviços sinalizados para reinstalação até ter êxito.  

Para reiniciar o serviço Gestor de Componentes do Site, utilize o Service Manager. Depois de ser reiniciado, todos os serviços afetados são desinstalados, reinstalados e reiniciados. Depois de utilizar a opção /STOPSITE para iniciar o ciclo de encerramento, não é possível evitar os ciclos de reinstalação depois de o serviço Gestor de Componentes do Site reiniciar.  

**/KEYFORPARENT** - utilize esta opção num site para distribuir a chave pública do site para um site principal.  

A opção /KEYFORPARENT coloca a chave &lt;pública do site no site *de* ficheiros>. CT4 na raiz da unidade de ficheiros do programa. Depois de executar preinst.exe com esta &lt;opção, copie manualmente o Código do *Site*>. Ficheiro CT4 para a pasta ...\Caixas de entrada do site principal\hman.box (não hman.box\pubkey).  

**/KEYFORCHILD** - utilize esta opção num site para distribuir a chave pública do site para um site subordinado.  

A opção /KEYFORCHILD coloca a chave &lt;pública do site no *site de* ficheiros>. CT5 na raiz da unidade de ficheiros do programa. Depois de executar preinst.exe com esta &lt;opção, copie manualmente o Código do *Site*>. Ficheiro CT5 na pasta ...\Caixas de entrada do site da criança\hman.box (não hman.box\pubkey).  

**/CHILDKEYS** - pode utilizar esta opção nos sites subordinados de um site que estiver a recuperar. Utilize esta opção para distribuir as chaves públicas de vários sites subordinados para o site de recuperação.  

A opção /CHILDKEYS coloca a chave a partir do site onde executa a &lt;opção, e todos esses sites de sites de crianças sites chaves públicas no *sitecódigo* de arquivo>. CT6.  

Depois de executar preinst.exe com esta &lt;opção, copie manualmente o Código do *Site*>. Ficheiro CT6 na pasta ...\Caixas de entrada do site de recuperação\hman.box (não hman.box\pubkey).  

**/PARENTKEYS** - pode utilizar esta opção no site principal de um site que estiver a recuperar. Utilize esta opção para distribuir as chaves públicas de todos os sites principais para o site de recuperação.  

A opção /PARENTKEYS coloca a chave a partir do site onde executa a &lt;opção, e as chaves de cada site-mãe acima desse site para o site de ficheiros Código\>. CT7.  

Depois de executar preinst.exe com esta &lt;opção, copie manualmente o Código do *Site*>. Ficheiro CT7 para a pasta ...\Caixas de entrada do site de recuperação\hman.box (não hman.box\pubkey).  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a>Troca manual de chaves públicas entre sites  
Por predefinição, a opção de troca de **chaves segura Requirer** está ativada para sites do Gestor de Configuração. Quando é necessária uma troca de chaves segura, existem duas situações em que é necessário efetuar manualmente a troca inicial de chaves entre sites:  

-   Se o esquema de Diretório Ativo não tiver sido alargado para O Gestor de Configuração  

-   Os sites do Gestor de Configuração não estão a publicar dados do site para o Diretório Ativo  

Pode utilizar a ferramenta Manutenção da Hierarquia para exportar as chaves públicas para cada site. Depois de terem sido exportadas, tem de trocar manualmente as chaves entre os sites.  

> [!NOTE]  
>  Depois de trocar manualmente as chaves públicas, pode rever o ficheiro de registo **hman.log**, que regista as alterações da configuração do site e a publicação das informações do site nos Serviços de Domínio do Active Directory no servidor do site principal, para garantir que o site primário processou a nova chave pública.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Para transferir manualmente a chave pública do site subordinado para o site principal  

1.  Com sessão iniciada no site subordinado, abra uma linha de comandos e navegue para a localização do ficheiro **Preinst.exe**.  

2.  Digite o seguinte para exportar a chave pública do site infantil: **Preinst/keyforparent**  

3.  A opção /keyforparent coloca a chave pública do site da criança no ** &lt;código\>do site . Ficheiro CT4** localizado na raiz da unidade do sistema.  

4.  Mova o ** &lt;código\>do site. Ficheiro CT4** para o diretório de instalação do ** &lt;site-mãe\>\inboxes\hman.box** pasta.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Para transferir manualmente a chave pública do site principal para o site subordinado  

1.  Com sessão iniciada no site principal, abra uma linha de comandos e navegue para a localização do ficheiro **Preinst.exe**.  

2.  Digite o seguinte para exportar a chave pública do local-mãe: **Preinst/keyforchild**.  

3.  A opção /keyforchild coloca a chave pública do site principal no ** &lt;código\>do site . Ficheiro CT5** localizado na raiz da unidade do sistema.  

4.  Mova o ** &lt;código\>do site. Ficheiro CT5** para o ** &lt;\>diretório de instalação \inboxes\hman.box** diretório no site da criança.  
