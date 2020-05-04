---
title: Atualizar os clientes de Linux e UNIX
titleSuffix: Configuration Manager
description: Atualize um cliente num servidor Linux ou UNIX no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715397"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Como atualizar clientes para servidores Linux e UNIX no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Pode atualizar a versão do cliente para Linux e UNIX num computador para uma versão mais recente do cliente, sem desinstalar previamente o cliente atual. Para isso, instale o novo pacote de instalação do cliente no computador enquanto utiliza a propriedade da linha de comando **-keepdb.** Quando o cliente para Linux e UNIX é instalado, substitui dados existentes do cliente pelos novos ficheiros do cliente. No entanto, a propriedade de linha de comando **-keepdb** direciona o processo de instalação para reter o identificador único (GUID), base de dados local de informação e loja de certificados. Esta informação é seguidamente utilizada pela nova instalação do cliente.  

 Por exemplo, tem um computador RHEL5 x64 que executa o cliente a partir da versão original do cliente do Configuration Manager para Linux e UNIX. Para atualizar este cliente para a versão cliente a partir da atualização cumulativa 1, executa manualmente o script de **instalação** para instalar o pacote de cliente aplicável a partir da atualização cumulativa 1, com a adição do interruptor de linha de comando **-keepdb.** Consulte a seguinte linha de comando exemplo:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Como utilizar uma Implementação de Software para Atualizar o Cliente em Servidores Linux e UNIX  
 Pode utilizar uma implementação de software para atualizar o cliente do UNIX para uma nova versão do cliente. No entanto, o cliente do Gestor de Configuração não pode executar diretamente o script de instalação para instalar o novo cliente porque a instalação de um novo cliente deve primeiro desinstalar o cliente atual. Esta ação acabaria com o processo de cliente do Gestor de Configuração que executa o script de instalação antes do início da instalação do novo cliente. Para utilizar com sucesso uma implementação de software para instalar o novo cliente, tem de agendar a instalação para começar num futuro e ser executada pelas capacidades de agendamento incorporadas do sistema operativo.  

 Utilize uma implementação de software para primeiro copiar os ficheiros para o novo pacote de instalação do cliente para o computador cliente. Em seguida, implemente e execute um script para agendar o processo de instalação do cliente. O script usa o sistema operativo **incorporado no** comando para atrasar o seu início. Quando o script é executado, a sua operação é gerida pelo sistema operativo do cliente e não pelo cliente Do Gestor de Configuração no computador. Este comportamento permite que a linha de comando chamada pelo script desinstale primeiro o cliente do Gestor de Configuração e, em seguida, instale o novo cliente. Estas ações completam o processo de atualização do cliente no computador Linux ou UNIX. Após a atualização concluída, o cliente atualizado permanece gerido pelo Gestor de Configuração.  

 Utilize o procedimento seguinte para o ajudar a configurar uma implementação de software para atualizar o cliente para Linux e UNIX. Os seguintes passos e exemplos atualizam um computador RHEL5 x64 que executa a versão inicial do cliente para a versão de cliente da atualização cumulativa 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Para utilizar uma implementação de software para atualizar o cliente em servidores Linux e UNIX  

1. Copie o novo pacote de instalação do cliente para o computador que executa o cliente do Gestor de Configuração para atualizar.  

    Por exemplo, coloque o pacote de instalação do cliente e instale script para atualização cumulativa 1 no seguinte local no computador cliente: **/tmp/PATCH**  

2. Crie um script para gerir a atualização do cliente do Gestor de Configuração. Em seguida, coloque uma cópia do script na mesma pasta no computador cliente que os ficheiros de instalação do cliente a partir do passo 1.  

    O guião não requer um nome específico. Deve conter linhas de comando suficientes para utilizar os ficheiros de instalação do cliente a partir de uma pasta local no computador cliente e instalar o pacote de instalação do cliente utilizando a propriedade de linha de comando **-keepdb.** Utilize a propriedade de linha de comando **-keepdb** para manter o identificador único do cliente atual para ser usado pelo novo cliente que está a instalar.  

    Por exemplo, criar um script chamado **upgrade.sh** que contenha as seguintes linhas:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Em seguida, copie-a para a pasta **/tmp/PATCH** no computador cliente.

3. Utilize a implementação de software para que cada cliente utilize o comando **at** incorporado nos computadores para executar o script **upgrade.sh** com um pequeno atraso antes de executar o script.  

    Por exemplo, utilize a seguinte linha de comando para executar o script: **em -f /tmp/upgrade.sh -m agora + 5 minutos**  

   Depois de o cliente agendar com êxito a execução do script **upgrade.sh** , o cliente envia uma mensagem de estado que indica que a implementação de software foi concluída com êxito. No entanto, a instalação atual do cliente é então gerida pelo computador, depois do atraso. Depois de concluída a atualização do cliente, valide a instalação ao rever o ficheiro **/var/opt/microsoft/scxcm.log** no computador cliente. Confirme que o cliente está instalado e comunicando com o site visualizando detalhes para o cliente no nó de **Dispositivos** do espaço de trabalho **De Ativos e Compliance** na consola Do Gestor de Configuração.  
