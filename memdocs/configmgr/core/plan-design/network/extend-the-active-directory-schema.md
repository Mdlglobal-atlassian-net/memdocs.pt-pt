---
title: Publicação e o esquema de Diretório Ativo
titleSuffix: Configuration Manager
description: Alargar o esquema de Diretório Ativo para O Gestor de Configuração para simplificar o processo de implantação e configuração de clientes.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718764"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Prepare o Diretório Ativo para a publicação do site

*Aplica-se a: Gestor de Configuração (ramo atual)*

Ao estender o esquema de Diretório Ativo para Gestor de Configuração, introduz novas estruturas ao Ative Directory que são usadas pelos sites do Gestor de Configuração para publicar informações chave num local seguro onde os clientes podem facilmente aceder a ela.  

É uma boa ideia usar o Gestor de Configuração com um esquema de Diretório Ativo alargado quando gere clientes no local. Um esquema alargado pode simplificar o processo de implantação e criação de clientes. Um esquema alargado também permite que os clientes localizem eficientemente recursos como servidores de conteúdo e serviços adicionais que as diferentes funções do sistema do Site Do Gestor de Configuração fornecem.  

-   Se não está familiarizado com o que o esquema estendido prevê para uma implementação do Gestor de Configuração, pode ler sobre [as extensões de Schema para O Gestor](../../../core/plan-design/network/schema-extensions.md) de Configuração para ajudá-lo a tomar esta decisão.  

-   Quando não utilizar um esquema estendido, pode configurar outros métodos como DNS e WINS para localizar serviços e servidores do sistema do site. Estes métodos de localização de serviços necessitam de configurações adicionais e não são o método preferencial dos clientes para localização de serviços. Para saber mais, leia Compreender como os clientes encontram recursos e serviços do site para O Gestor de [Configuração,](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)  

-   Se o seu esquema de Diretório Ativo foi estendido para O Gestor de Configuração 2007 ou System Center 2012 Diretor de Configuração, então não precisa de fazer mais. As extensões de esquemas mantêm-se inalteradas e já estarão em vigor.  

Estender o esquema é uma ação única para qualquer floresta. Para estender e, em seguida, utilizar o esquema alargado do Diretório Ativo, siga estes passos:  

## <a name="step-1-extend-the-schema"></a>Passo 1. Expandir o esquema  
Para estender o esquema para O Gestor de Configuração:  

-   Use uma conta que seja membro do grupo de segurança Schema Admins.  

-   Seja inscrito no controlador de domínio mestre do esquema.  

-   Executar a ferramenta **Extadsch.exe** ou utilizar o utilitário lDIFDE da linha de comando com o ficheiro **ConfigMgr_ad_schema.ldf.** Tanto a ferramenta como o ficheiro estão na pasta **SMSSETUP\BIN\X64** no suporte de instalação do Gestor de Configuração.  

#### <a name="option-a-use-extadschexe"></a>Opção A: utilizar o Extadsch.exe  

1.  Execute o **extadsch.exe** para adicionar as novas classes e atributos ao esquema do Active Directory.  

    > [!TIP]  
    >  Execute esta ferramenta a partir de uma linha de comandos para ver comentários durante a execução da mesma.  

2.  Verifique se a extensão do esquema foi bem sucedida através da revisão do extadsch.log na raiz da unidade do sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opção B: utilizar o ficheiro LDIF  

1.  Editar o ficheiro **ConfigMgr_ad_schema.ldf** para definir o domínio raiz do Diretório Ativo que pretende estender:  

    -   Substitua todas as instâncias do texto, **DC=x,** no ficheiro com o nome completo do domínio para estender.  

    -   Por exemplo, se o nome completo do domínio para estender for nomeado widgets.microsoft.com, altere todas as instâncias de DC=x no ficheiro para **DC=widgets, DC=microsoft, DC=com**.  

2.  Utilize o utilitário lDIFDE da linha de comando para importar o conteúdo do ficheiro **ConfigMgr_ad_schema.lDF** para Serviços de Domínio de Diretório Ativo:  

    -   Por exemplo, a seguinte linha de comando importa as extensões de esquema para serviços de domínio de diretório ativo, liga a exploração madeireira verbosa e cria um ficheiro de registo durante o processo de importação: **ldifde -i -f ConfigMgr_ad_schema.ldf -v-j &lt;localização para armazenar ficheiro\>** de registo .  

3.  Para verificar se a extensão do esquema foi bem sucedida, reveja um ficheiro de registo criado pela linha de comando utilizada no passo anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Passo 2.  Criar o contentor de Gestão do Sistema e conceder permissões de sites ao contentor  
 Depois de estender o esquema, deve criar um recipiente denominado Gestão de **Sistemas** em Serviços de Domínio de Diretório Ativo (AD DS):  

-   Cria este recipiente uma vez em cada domínio que tem um site primário ou secundário que publicará dados para o Ative Directory.  

-   Para cada recipiente, concede permissões à conta de computador de cada servidor de site primário e secundário que publicará dados nesse domínio. Cada conta necessita de **Controlo Total** para o recipiente com a permissão avançada, **Aplicar em**, igual a Este objeto e todos **os objetos descendentes**.  

#### <a name="to-add-the-container"></a>Adicionar o contentor  

1.  Utilize uma conta que tenha a permissão **Criar Todos os Objetos Subordinados** no contentor **Sistema** nos Serviços de Domínio do Active Directory.  

2.  Executar **ADSI Edit** (adsiedit.msc) e ligar-se ao domínio do servidor do site.  

3.  Crie o contentor:  

    -   Expandir **Domain** &lt;o nome\>de domínio &lt;do\>domínio totalmente qualificado, expandir o nome distinto, clicar à direita **CN=System,** escolher **Novo,** e depois escolher **Objeto**.  

    -   Na caixa de diálogo **Create Object,** escolha **recipiente**, e escolha **Seguinte**.  

    -   Na caixa **Valor,** introduza **a Gestão do Sistema,** e depois escolha **a Seguinte**.  

4.  Atribuir permissões:  

    > [!NOTE]  
    >  Se preferir, pode utilizar outras ferramentas como a ferramenta administrativa De utilizadores de diretórios e computadores (dsa.msc) para adicionar permissões ao recipiente.  

    -   Clique à direita **CN=Gestão**do Sistema, e depois escolha **Propriedades**.  

    -   Escolha o separador **'Segurança',** escolha **Adicionar**, e, em seguida, adicione a conta do servidor do site com a permissão **de Controlo Completo.**  

    -   Escolha **Avançado,** escolha a conta de computador do servidor do site e, em seguida, escolha **Editar**.  

    -   Na lista **Apply on,** escolha **Este objeto e todos os objetos descendentes**.  

5.  Escolha **OK** para fechar a consola e guardar a configuração.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Passo 3. Criar sites para publicar nos Serviços de Domínio de Diretório Ativo  
 Depois de configurado o recipiente, são concedidas permissões e instalou um site primário do Gestor de Configuração, pode configurar esse site para publicar dados no Ative Directory.  

 Para mais informações sobre a publicação, consulte [publicar dados do site para O Gestor de Configuração](../../../core/servers/deploy/configure/publish-site-data.md).  
