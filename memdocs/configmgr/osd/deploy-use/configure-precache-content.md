---
title: Configurar conteúdo de pré-cache
titleSuffix: Configuration Manager
description: Saiba como os clientes podem descarregar conteúdo de implementação de OS antes de um utilizador instalar a sequência de tarefas.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 184bdc58ac6dc0e311875cc1ddab8c605d8eec32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720626"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Configure o conteúdo pré-cache para sequências de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1021244-->
A função pré-cache para implementações disponíveis de sequências de tarefas permite que os clientes descarreguem conteúdo relevante antes de um utilizador instalar a sequência de tarefas. O cliente pode pré-cache conteúdo para sequências de tarefas que [atualizem um SISTEMA](create-a-task-sequence-to-upgrade-an-operating-system.md) ou [instalam uma imagem de OS](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> Na versão 1910, o Gestor de Configuração permite esta funcionalidade por padrão. Na versão 1906 ou anterior, o Gestor de Configuração não permite esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Por exemplo, você só quer uma única sequência de tarefas de upgrade no local para todos os utilizadores, e tem muitas arquiteturas e idiomas. Em versões anteriores, o conteúdo começa a ser descarregado quando o utilizador instala uma sequência de tarefas disponível a partir do Software Center. Este atraso adiciona tempo adicional antes de a instalação estar pronta para arrancar. Todos os conteúdos referenciados na sequência de tarefas são descarregados. Este conteúdo inclui o pacote de upgrade de SO para todas as línguas e arquiteturas. Se cada pacote de atualização tiver aproximadamente 3 GB de tamanho, o conteúdo total é muito grande.

O conteúdo pré-cache dá-lhe a opção de o cliente apenas descarregar o conteúdo aplicável e todos os outros conteúdos referenciados assim que receber a implementação. Quando o utilizador clica **em Instalar** no Centro de Software, o conteúdo está pronto. A instalação começa rapidamente porque o conteúdo está no disco rígido local.

Na versão 1902 e anterior do Gestor de Configuração, este comportamento aplica-se apenas ao pacote de *atualização do OS*. Este pacote é o único conteúdo em que especifica a arquitetura ou linguagem correspondentes. Por exemplo, se a sequência de tarefas também referencia vários pacotes de controladores, o cliente descarrega-os todos. O motor de sequência de tarefas avalia as condições dos passos quando a sequência de tarefas funciona, não com antecedência. O cliente utiliza as etiquetas nas propriedades do pacote para determinar qual o conteúdo para pré-cache.

Começando na versão de 1906,<!--4224642--> pode utilizar pré-cachepara reduzir o consumo de largura de banda dos seguintes tipos de conteúdo:

- Pacotes de upgrade de OS
- Imagens do SO
- Pacotes de controladores
- Pacotes

## <a name="configure-pre-caching"></a>Configurar pré-cache

Existem três passos para configurar a função pré-cache:

1. [Criar e configurar os pacotes](#bkmk_createpkg)
2. [Criar uma sequência de tarefas com passos condicional](#bkmk_createts)
3. [Implementar a sequência de tarefas e ativar o pré-cache](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a>1. Criar e configurar os pacotes

O cliente avalia os atributos dos pacotes para determinar que conteúdo descarrega durante a pré-cache.  

#### <a name="os-upgrade-package"></a>Pacote de upgrade de OS

Crie [pacotes](../get-started/manage-operating-system-upgrade-packages.md) de upgrade de OS para arquiteturas e línguas específicas. Especifique a **Arquitetura** e **A Linguagem** no separador Fonte de **Dados** das suas propriedades.

#### <a name="os-image"></a>Imagem de OS

Crie [imagens de OS](../get-started/manage-operating-system-images.md) para arquiteturas e línguas específicas. Especifique a **Arquitetura** e **A Linguagem** no separador Fonte de **Dados** das suas propriedades.

#### <a name="driver-package"></a>Pacote de controladores

Crie pacotes de condutor para [modelos](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) de hardware específicos. Especifique o **Modelo** no separador **Geral** das suas propriedades.

Para determinar qual o pacote de condutor que descarrega durante a pré-cache, o cliente avalia o modelo contra a propriedade **Nome** da classe **WMI Win32_ComputerSystemProduct.**

> [!TIP]
> A consulta real `LIKE` usa uma declaração `select * from win32_computersystemproduct where name like "%yourstring%"`com wildcards: . Por exemplo, se `Surface` especificar como modelo, a consulta corresponde a todos os modelos que incluem essa cadeia.<!-- 6315551 -->

#### <a name="package"></a>Pacote

Crie pacotes para [arquiteturas](../../apps/deploy-use/packages-and-programs.md) e línguas específicas. Especifique a **Arquitetura** e **a Língua** no separador **Geral** das suas propriedades.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a>2. Criar uma sequência de tarefas

Crie uma sequência de tarefas com passos condicionais para as diferentes línguas e arquiteturas, ou diferentes modelos de hardware para pacotes de condutor.

|Conteúdo|Passo|
|---------|---------|
|Pacote de upgrade de OS|[Upgrade OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Imagem de OS|[Aplicar imagem de OS](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Pacote de controladores|[Aplicar Pacote de Controlador](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Pacote|[Instalar Pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Por exemplo, o seguinte passo **de Upgrade OS** utiliza a versão inglesa:  

![Editor de sequência de tarefas mostrando vários passos de Upgrade OS para ENU, DEU e JPN](../media/precacheproperties2.png)

![Editor de sequência de tarefas, separador opções, exibindo a consulta WMI WQL para Locale e OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> Recomenda-se a seguinte consulta do WMI para o Inglês (Estados Unidos) OS e arquitetura de 64 bits:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Em primeiro lugar, adicione o idioma selecionando a condição de **Linguagem do Sistema Operativo.** Em seguida, editar a consulta do WMI para incluir a cláusula de arquitetura.


### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a>3. Implementar a sequência de tarefas

[Implementar a sequência de tarefas](deploy-a-task-sequence.md). Para a função pré-cache, configure as seguintes definições:  

- No separador **Geral,** selecione **o conteúdo de pré-descarregamento para esta sequência de tarefas**.  

- No separador de definições de **implementação,** configure a sequência de tarefas conforme **disponível**.  

- No separador **Agendamento,** escolha o tempo atualmente selecionado para a definição, **Agendar quando esta implementação estará disponível**. O cliente inicia o conteúdo pré-cache no tempo disponível da implementação. Quando um cliente direcionado recebe esta apólice, o tempo disponível é no passado, assim o download pré-cache começa imediatamente. Se o cliente receber esta apólice mas o tempo disponível for no futuro, o cliente não começa a pré-cacher conteúdos até que o tempo disponível ocorra.  

- No separador Pontos de **Distribuição,** configure as definições das opções de **implementação.** Se o conteúdo não estiver pré-cacheantes antes de um utilizador iniciar a instalação, o cliente utiliza estas definições.  

    > [!Important]  
    > Para uma sequência de tarefas que instala uma imagem de OS, não utilize a opção de implementação para descarregar conteúdo localmente quando necessário pela sequência de **tarefas de execução**. Quando a sequência de tarefalimpa o disco antes de aplicar a imagem de OS, remove a cache do cliente. Desde que o conteúdo se foi, a sequência de tarefas falha.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Experiência de utilizador

- Quando o cliente recebe a política de implementação, começa a pré-cache o conteúdo após o tempo disponível da implementação. Este conteúdo inclui todos os pacotes referenciados, mas apenas o pacote de upgrade do SO que corresponde à arquitetura e atributos linguísticos no pacote.  

- Quando o cliente disponibiliza a implementação aos utilizadores, uma notificação apresenta-se para informar os utilizadores sobre a nova implementação. Agora a sequência de tarefas é visível no Centro de Software. O utilizador pode ir ao Centro de Software e clicar **em Instalar** para iniciar a instalação.  

- Se o cliente não tiver pré-cache o conteúdo quando o utilizador instala a sequência de tarefas, então o cliente utiliza as definições que especifica no separador Opção de **Implementação** da implementação.  


## <a name="see-also"></a>Consulte também

- [Criar uma sequência de tarefas para atualizar um SO](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Cenário para atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)
