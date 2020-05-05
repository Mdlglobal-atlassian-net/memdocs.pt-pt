---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: Conheça o processo que fornece atualizações para o produto a partir da consola 'Gestor de Configuração'.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720514"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>O CD. Última pasta para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração tem um processo para fornecer atualizações ao produto a partir da consola 'Gestor de Configuração'. Para suportar este novo método de atualização do Gestor de Configuração, é criada uma nova pasta chamada **CD. Mais recente.** Esta pasta contém uma cópia dos ficheiros de instalação do Gestor de Configuração para a versão atualizada do seu site.  

O CD. A pasta mais recente contém uma pasta chamada **Redist,** que contém os ficheiros redistribuíveis que configuram os downloads e utilizações. Estes ficheiros correspondem à versão dos ficheiros do Configuration Manager localizados na pasta CD.Latest. Ao executar o programa de configuração a partir da pasta CD.Latest, tem de utilizar ficheiros que correspondem a essa versão do programa de configuração. Pode direcionar a Configuração para descarregar ficheiros novos e atuais da Microsoft ou configurar para utilizar os ficheiros da pasta Redist incluídos no CD. Última pasta.

Os meios de base não incluem uma pasta **Redist.** O site não cria uma pasta Redist até instalar uma atualização na consola. Entretanto, utilize a pasta Redist que utilizou na instalação de sites a partir dos meios de base.  

> [!TIP]  
> Certifique-se de que os ficheiros redistribuíveis que utiliza estão atuais. Se ainda não descarregou ficheiros redistribuíveis recentemente, planeie permitir que a Configuração o faça a partir da Microsoft.   

Os seguintes cenários criam ou atualizam o CD. Última pasta num site de administração central ou servidor de site primário:  

- Quando instala uma atualização ou um 'hotfix' dentro da consola 'Gestor de Configuração', o site cria ou atualiza a pasta na pasta de instalação do Gestor de Configuração.  

- Quando executa a tarefa de backup do Gestor de Configuração incorporado, o site cria ou atualiza a pasta sob a localização da pasta de reserva designada.  

- Quando instala um novo site utilizando meios de base, o site cria o CD. Última pasta.


## <a name="supported-scenarios"></a>Cenários suportados

Os ficheiros de origem do CD. A pasta mais recente é suportada para os seguintes cenários:  

### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação
Para recuperar um site, utilize os ficheiros de origem de um CD. Última pasta que corresponde ao seu site. Quando executa uma cópia de segurança do site utilizando a tarefa de backup do site incorporado, o CD. A pasta mais recente está incluída como parte da cópia de segurança.

- Quando reinstala um site como parte de uma recuperação de site, instala o site a partir da pasta CD.Latest incluída na sua cópia de segurança. Esta ação instala o site utilizando as versões de ficheiros que correspondem à cópia de segurança do seu site e à base de dados do site.  

    - Se não tiver acesso ao CD correto. Versão mais recente da pasta, obtenha o CD. Última pasta com as versões de ficheiro sinuosas, instalando um site num ambiente de laboratório. Em seguida, atualize esse site para corresponder à versão que pretende recuperar.  

    - Se não tiver o CD correto. A pasta mais recente e os seus conteúdos disponíveis não podem recuperar um site. Nestas circunstâncias, é necessário reinstalar o site.  

- Quando não se tem CD. A última pasta, mas tem um site primário ou central de crianças em funcionamento, pode usar esse site como um site de referência para uma recuperação do site.  

### <a name="install-a-child-primary-site"></a>Instale um local primário para crianças
Quando pretender instalar um novo site primário para crianças abaixo de um site de administração central que tenha instalado uma ou mais atualizações na consola, utilize a Configuração e os ficheiros de origem do CD. Última pasta do site da administração central. Este processo utiliza ficheiros de origem de instalação que correspondem à versão do site da administração central. Para mais informações, consulte [Utilize o Assistente de Configuração para instalar sites](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Expandir um local primário autónomo
Quando expandir um site primário autónomo instalando um novo site de administração central, utilize a Configuração e os ficheiros de origem do CD. Última pasta do site principal. Este processo utiliza ficheiros de origem de instalação que correspondem à versão do local principal. Para mais informações, consulte [Expandir um site primário autónomo](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Instale um site secundário
<!-- SCCMDocs-pr issue #3164 -->
Quando pretender instalar um novo site secundário abaixo de um site primário que tenha instalado uma ou mais atualizações na consola, utilize os ficheiros de origem do CD. Última pasta do site principal. 

Para mais informações, consulte [Instale um site secundário](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Cenários não suportados

O CD atualizado. Os ficheiros de origem mais recentes não são suportados para:  

- Instalar um novo site para uma nova hierarquia  
- Atualizar um site do Microsoft System Center 2012 Para configuração do gestor de funções
- Instalação de clientes do Gestor de Configuração
- Instalação de consolas de Gestor de Configuração
