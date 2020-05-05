---
title: Instalar Editor de Atualizações
titleSuffix: Configuration Manager
description: Instale o Editor de Atualizações do Centro de Sistemas no seu ambiente
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720374"
---
# <a name="install-updates-publisher"></a>Instalar Editor de Atualizações

*Aplica-se a: System Center Updates Publisher*

As informações nestes artigos podem ajudá-lo a descarregar, instalar e configurar o Editor de Atualizações para utilização com o ambiente do Gestor de Configuração.

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
Atualizações do Centro de Sistema A editora só pode ser utilizada com o Gestor de Configuração. Não se destina a ser usado com hierarquias wSUS autónomas.

As seguintes secções detalham os requisitos para instalar e utilizar atualizações Editora, e limitações ou problemas conhecidos para a sua utilização.  

### <a name="operating-systems"></a>Sistemas operativos
Instale e execute atualizações Editora numa edição de 64 bits dos seguintes sistemas operativos. Não existem requisitos mínimos de atualização cumulativa ou pacote de serviços.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Profissional, Empresa)

### <a name="prerequisites"></a>Pré-requisitos
São necessários os seguintes no computador que executa atualizações da Editora.

-   **Sistema operativo de 64 bits**: O computador onde instala atualizações A Editora deve executar um sistema operativo de 64 bits.
-   **WSUS 6.2 ou posterior:**
    -   No Windows Server, instale a Consola de Administração predefinida para satisfazer este requisito.
    -   Para windows 10 e Windows 8.1, instale as Ferramentas de Administração do [Servidor Remoto (RSAT) para sistemas operativos Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Isto instala o suporte necessário para utilizar atualizações Publisher (*API e PowerShell cmdlets*, e *User Interface Management Console).*
-   **Permissões:**
    -   Instalação: Administração local
    -   Maioria das operações: utilizador local
    -   Publicação ou operações que envolvam WSUS: Membro do grupo de administradores da WSUS no Servidor WSUS.

### <a name="supported-languages"></a>Linguagens suportadas
Updates Publisher está disponível apenas em inglês, mas pode gerir atualizações para outros idiomas. O suporte linguístico depende da tarefa, como publicar, criar ou editar atualizações.

Ao exportar ou publicar atualizações, a Updates Publisher apresenta o título e a descrição da atualização do software com base no local do computador onde o Updates Publisher está instalado.

Por exemplo, cria-se uma atualização de software que tem um título inglês e espanhol.

-   Se criar a atualização num computador cujo local é inglês, por padrão, verá o título e a descrição em inglês.
-   Se exportar ou publicar essa atualização para um computador cujo local é espanhol, nesse computador verá o título e a descrição em espanhol.

### <a name="publishing"></a>Publicar
Ao publicar atualizações de software, pode especificar o idioma do ficheiro binário de atualização de software. Também pode especificar que o binário é neutro em termos linguísticos. As seguintes línguas são suportadas:

-   Árabe
-   Chinês (Hong Kong S.A.R.)
-   Chinês (Tradicional)
-   Chinês (Simplificado)
-   Checo
-   Dinamarquês
-   Neerlandês
-   Inglês
-   Finlandês
-   Francês
-   Alemão
-   Grego
-   Hebraico
-   Húngaro
-   Italiano
-   Japonês
-   Coreano
-   Norueguês
-   Polaco
-   Português
-   Português (Brasil)
-   Russo
-   Espanhol
-   Sueco
-   Turco

### <a name="software-update-titles-and-descriptions"></a>Títulos e descrições de atualização de software
As seguintes línguas são suportadas para títulos e descrições de atualização de software.

-   Chinês (Tradicional)
-   Chinês (Simplificado)
-   Inglês
-   Francês
-   Alemão
-   Italiano
-   Japonês
-   Coreano
-   Português (Brasil)
-   Russo
-   Espanhol

## <a name="install-updates-publisher"></a>Instalar Editor de Atualizações
Obtenha o **UpdatesPubliser.msi** para instalar o System Center Updates Publisher a partir do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55543).

Para instalar atualizações Editora, execute **UpdatesPublisher.msi** num computador que cumpra os *pré-requisitos*. O instalador cria a seguinte pasta para conter os ficheiros necessários para executar Atualizações Editor: %PROGRAMFILES%\Microsoft\UpdatesPublisher*.

Uma vez que esta pasta contém todos os ficheiros necessários para utilizar o Editor de Atualizações, pode copiar a pasta e o seu conteúdo para uma nova localização ou computador e, em seguida, utilizar o Editor de Atualizações a partir desse local. No entanto, a nova localização ou computador deve cumprir os pré-requisitos para executar updates Publisher.

Depois de concluída a instalação, execute **UpdatesPublisher.exe** da pasta *UpdatesPublisher* para iniciar atualizações Da Editora.

## <a name="next-steps"></a>Passos seguintes
 Depois de instalar a Editora updates, recomendamos que [configure as opções](updates-publisher-options.md) para Updates Publisher. Tem de configurar algumas opções antes de poder utilizar algumas funcionalidades do Editor de Atualizações.

 No entanto, se pretender utilizar as falhas e não pretender implementar atualizações para um servidor de atualização ou para dispositivos geridos, pode saltar direito a [gerir catálogos](updates-publisher-catalogs.md)de atualizações de software, ou [criar atualizações](create-updates-with-updates-publisher.md) de software e criar catálogos de atualizações próprios.
