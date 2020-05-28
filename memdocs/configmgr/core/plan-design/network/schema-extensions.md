---
title: Extensões de esquema
titleSuffix: Configuration Manager
description: Estenda o esquema de Diretório Ativo para apoiar o Gestor de Configuração.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904077"
---
# <a name="schema-extensions-for-configuration-manager"></a>Extensões de esquema para o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode estender o esquema de Diretório Ativo para suportar o Gestor de Configuração. Isto edita o esquema ative diretório de uma floresta para adicionar um novo recipiente e vários atributos que os sites do Gestor de Configuração usam para publicar informações chave no Ative Directory onde os clientes podem usá-lo de forma segura. Esta informação pode simplificar a implementação e configuração dos clientes e ajudar os clientes a localizar recursos do site como servidores com conteúdo implantado ou que fornecem diferentes serviços aos clientes.  

-   É uma boa ideia estender o esquema do Diretório Ativo, mas não é necessário.  

Antes de [expandir o esquema do Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), deve estar familiarizado com os Serviços de Domínio do Active Directory e à vontade para [modificar o esquema do Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considerações para alargar o esquema de Diretório Ativo para Gestor de Configuração  

-   As extensões de esquema de diretório ativo para O Gestor de Configuração são inalteradas das que o Gestor de Configuração 2007 e o Gestor de Configuração 2012 usam. Caso tenha expandido anteriormente o esquema de uma das versões, não precisa de expandir novamente o esquema.  

-   O alargamento do esquema é uma ação irreversível em toda a floresta, única.  

-   Apenas um utilizador que seja membro do Grupo Schema Admins ou que tenha sido delegado autorizações suficientes para alterar o esquema pode estender o esquema.  

-   Embora possa estender o esquema antes ou depois de executar configuração do Gestor de Configuração, é uma boa ideia estender o esquema antes de começar a configurar os seus sites e configurações de hierarquia. Isto poderá simplificar muitos passos de configuração posteriores.  

-   Depois de estender o esquema, o catálogo global ative Directy é replicado em toda a floresta. Por conseguinte, planeie alargar o esquema quando o tráfego de replicação não afetar negativamente outros processos dependentes da rede:  

    -   Nas florestas do Windows 2000, o alargamento do esquema causa uma sincronização completa de todo o catálogo global.  

    -   Começando pelas florestas do Windows 2003, apenas os atributos recém-adicionados são replicados.  

**Dispositivos e clientes que não utilizam o esquema do Active Directory:**  

-   Dispositivos móveis geridos pelo conector do Exchange Server  

-   O cliente para computadores Mac  

-   O cliente para servidores Linux e UNIX  

-   Dispositivos móveis que são matriculados pelo Gestor de Configuração  

-   Dispositivos móveis que estão matriculados pela Microsoft Intune  

-   Clientes legados do dispositivo móvel  

-   Clientes Windows que estão configurados para gestão de clientes apenas na Internet  

-   Clientes windows que são detetados pelo Gestor de Configuração para estar na Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Capacidades que beneficiam da expansão do esquema  
Tarefa de **instalação e site** do cliente - Quando um computador Windows instala um novo cliente, o cliente procura Serviços de Domínio de Diretório Ativo para propriedades de instalação.  

-   **Sinuosos:** Se não estender o esquema, utilize uma das seguintes opções para fornecer detalhes de configuração que os computadores devem instalar:  

    -   **Utilize a instalação push de cliente**. Antes de utilizar um método de instalação do cliente, certifique-se de que todos os pré-requisitos são cumpridos. Para obter mais informações, consulte a secção "Dependências do Método de Instalação" em [Pré-requisitos para a implementação](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)de clientes para computadores Windows .  

    -   **Instale os clientes manualmente** e forneça propriedades de instalação do cliente utilizando propriedades de linha de comando de instalação CCMSetup. Isto deve incluir o seguinte:  

        -   Especifique um ponto de gestão ou um caminho de origem a partir do qual o computador pode descarregar os ficheiros de instalação utilizando a propriedade CCMSetup **/mp:= &lt; nome \> ** de ponto de gestão nome de computador ou **/fonte: &lt; caminho para ficheiros \> de origem do cliente** na linha de comando CCMSetup durante a instalação do cliente.  

        -   Especifique uma lista de pontos de gestão iniciais para o cliente usar para que possa atribuí-los ao site e, em seguida, baixar a política do cliente e as definições do site. Para o efeito, utilize a propriedade SMSMP do CCMSetup Client.msi.  

    -   **Publique o ponto de gestão no DNS ou WINS** e configure clientes para utilizar este método de localização do serviço.  

**Configuração da porta para comunicação cliente-servidor** - Quando um cliente instala, é configurado com informações portuárioarmazenadas em Diretório Ativo. Se posteriormente alterar a porta de comunicação cliente-a-servidor para um site, um cliente pode obter esta nova definição de porta a partir dos Serviços de Domínio do Diretório Ativo.  

-   **Soluções:** Se não expandir o esquema, utilize uma das seguintes opções para fornecer esta nova configuração da porta aos clientes existentes:  

    -   **Reinstale os clientes** utilizando opções que configuram a nova porta.  

    -   **Implemente um script personalizado nos clientes para atualizar as informações da porta**. Se os clientes não puderem comunicar com um site por causa de uma mudança de porta, não pode utilizar o Gestor de Configuração para implementar este script. Por exemplo, pode utilizar a Política de Grupo.  

**Cenários** de implementação de conteúdos - Quando cria conteúdo num site e, em seguida, implementa esse conteúdo para outro site na hierarquia, o site recetor deve ser capaz de verificar a assinatura dos dados de conteúdo assinados. Isto requer acesso à chave pública do site de origem onde são criados estes dados. Ao estender o esquema de Diretório Ativo para Gestor de Configuração, a chave pública de um site está disponível para todos os sites da hierarquia.  

-   **Solução:** se não expandir o esquema, utilize a ferramenta de manutenção da hierarquia, **preinst.exe**, para trocar as informações da chave segura entre sites.  

     Por exemplo, se planeia criar conteúdo num site primário e implementar esse conteúdo para um site secundário abaixo de um site primário diferente, deve estender o esquema de Diretório Ativo para permitir que o site secundário obtenha a chave pública do site primário de origem, ou use preinst.exe para partilhar chaves entre os dois sites diretamente.  

## <a name="active-directory-attributes-and-classes"></a>Atributos e classes de Diretório Ativo  
Quando estende o esquema para O Gestor de Configuração, as seguintes classes e atributos são adicionados ao esquema e estão disponíveis para todos os sites do Gestor de Configuração naquela floresta de Diretório Ativo.  

-   Attributes:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Nome  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Limites  
        em  

    -   cn=MS-SMS-Site-Limites  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Versão  

-   Classes:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  As extensões de esquema podem incluir atributos e classes que são transportadas para a frente a partir de versões anteriores do produto, mas não utilizadas pelo Gestor de Configuração. Por exemplo:  
> 
> 
> - Atributo: cn=MS-SMS-Site-Limites  
>   -   Classe: cn=MS-SMS-Server-Locator-Point  

Pode garantir que as listas anteriores estão atuais visualizando o **ConfigMgr_ad_schema. Ficheiro LDF** da pasta **\SMSSETUP\BIN\x64** do meio de instalação do Gestor de Configuração.  
