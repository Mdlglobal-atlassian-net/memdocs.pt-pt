---
title: Ferramenta de registo de atualização
titleSuffix: Configuration Manager
description: Descubra quando e como utilizar a ferramenta de registo de atualização para importar manualmente uma atualização para a consola Do Gestor de Configuração.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711239"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Utilize a Ferramenta de Registo de Atualização para importar hotfixes para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Algumas atualizações para O Gestor de Configuração não estão disponíveis no serviço de cloud da Microsoft e são obtidas apenas fora da banda. Um exemplo é uma correção de versão limitada para resolver um problema específico.   
Quando tiver de instalar um desbloqueio fora de banda e o nome de ficheiro atualização ou de correção de hotfix terminar com a **atualização de extensão.exe,** utilize a ferramenta de registo de **atualização** para importar manualmente a atualização para a consola 'Gestor de Configuração'. A ferramenta permite extrair e transferir o pacote de atualização para o servidor do site e registar a atualização na consola do Configuration Manager.  

 Se o ficheiro hotfix tiver a extensão de ficheiro **.exe** (não **atualizar.exe),** consulte [Utilize o Instalador Hotfix para instalar atualizações para o 'Gestor de Configuração')](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Este tópico fornece orientações gerais sobre como instalar hotfixes que atualizam o Gestor de Configuração. Para mais detalhes sobre um hotfix ou atualização específico, consulte o seu artigo correspondente da Base de Conhecimento (KB) no Microsoft Support.  

 **Pré-requisitos para utilizar a ferramenta de registo de atualização:**  

-   Apenas atualizações fora da banda que terminam com a extensão **.update.exe** podem ser instaladas usando esta ferramenta  

-   A ferramenta é autossuficiente com as atualizações individuais que obtém diretamente da Microsoft  

-   A ferramenta não tem uma dependência sobre o modo do ponto de ligação de serviço  

-   A ferramenta deve ser executada no computador que aloja o ponto de ligação de serviço  

-   O computador onde a ferramenta funciona (o computador do ponto de ligação de serviço) deve ter a .NET Framework 4.52 instalada  

-   A conta que utiliza para executar a ferramenta deve ter permissões de **administrador local** no computador que acolhe o ponto de ligação de serviço (onde a ferramenta é executada)  

-   A conta que utiliza para executar a ferramenta deve ter permissões de **escrita** para a seguinte pasta no computador que acolhe o ponto de ligação de serviço: ** &lt;O diretório\>de instalação ConfigMgr \EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Utilizar a ferramenta de registo de atualização  

1. No computador que aloja o ponto de ligação de serviço:  

   -   Abra um pedido de comando com privilégios administrativos e, em seguida, mude de diretórios para o local que contém ** &lt;versão do produto\>-&lt;\>-&lt;produto Produto KB artigo\>ID -ConfigMgr.Update.exe**  

2. Execute o seguinte comando para iniciar a ferramenta de registo de atualização:  

   -   **&lt;Versão\>-\>-&lt;do produto KB artigo KB ID\>-ConfigMgr.Update.exe&lt;**  

   Depois de a correção ser registada, é apresentada como uma nova atualização na consola no prazo de 24 horas.  Pode acelerar o processo:

   - Abra a consola do Gestor de Configuração e vá para Atualizações de **Administração** > **e Manutenção,** e clique em Verificar **atualizações**. (Antes da versão 1702, atualizações e manutenção estava **sob** > **serviços**de cloud administration .) 

   A ferramenta de registo de atualização regista as ações num ficheiro .log no computador local. O ficheiro de registo tem o mesmo nome que o ficheiro hotfix .exe e está escrito na pasta **%SystemRoot%/Temp.**  

    Depois de a atualização ser registada, pode fechar a ferramenta de registo de atualização.  

3. Abra a consola do Gestor de Configuração e navegue para**Atualizações de** **Administração** > e Manutenção . As correções importadas estão agora disponíveis para instalação. (Antes da versão 1702, atualizações e manutenção estava **sob** > **serviços**de cloud administration .)

   Para obter informações sobre a instalação de atualizações, consulte [instalar atualizações na consola para O Gestor de Configuração](../../../core/servers/manage/install-in-console-updates.md)  
