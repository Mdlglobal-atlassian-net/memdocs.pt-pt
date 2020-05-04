---
title: Atualizar clientes macOS
titleSuffix: Configuration Manager
description: Atualize o cliente do Gestor de Configuração em computadores Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715005"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Como atualizar clientes em computadores Mac em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Siga os passos de alto nível neste artigo para atualizar o cliente para computadores Mac utilizando uma aplicação De Configuração Manager. Também pode descarregar o ficheiro de instalação do cliente Mac, copiá-lo para uma localização de rede partilhada ou uma pasta local no computador Mac, e, em seguida, instruir os utilizadores a executar manualmente a instalação.  

> [!NOTE]  
> Antes de fazer estes passos, certifique-se de que o seu computador Mac satisfaz os pré-requisitos. Consulte [sistemas operativos suportados para computadores Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Descarregue o mais recente cliente Mac

O cliente Mac para Gestor de Configuração não é fornecido nos meios de instalação do Gestor de Configuração. Descarregue-o a partir do Microsoft Download Center, [Microsoft Endpoint Configuration Manager - macOS Client (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850). Os ficheiros de instalação do cliente Mac estão contidos num ficheiro do Instalador do Windows chamado **ConfigmgrMacClient.msi**.  

## <a name="create-the-mac-client-installation-file"></a>Criar o ficheiro de instalação do cliente Mac

Num computador que executa o Windows, execute **o ConfigmgrMacClient.msi**. Este instalador desembala o ficheiro de instalação do cliente Mac, chamado **Macclient.dmg**. Por predefinição, pode encontrar este ficheiro na seguinte pasta: **C:\Program Files\Microsoft\System Center Configuration Manager para cliente Mac**.  

## <a name="extract-the-client-installation-files"></a>Extrair os ficheiros de instalação do cliente

Copie **Macclient.dmg** para um computador Mac. Monte o ficheiro Macclient.dmg no macOS e, em seguida, copie o conteúdo para uma pasta no computador Mac.  

## <a name="create-a-cmmac-file"></a>Criar um ficheiro .cmmac

1. Abra a pasta **Ferramentas** dos ficheiros de instalação do cliente Mac. Utilize a ferramenta **CMAppUtil** para criar um ficheiro .cmmac a partir do pacote de instalação do cliente. Utilizará este ficheiro para criar a aplicação 'Gestor de Configuração'.  

2. Copie o novo ficheiro **CMClient.pkg.cmmac** para uma localização de rede que esteja disponível para o computador que executa a consola do Gestor de Configuração.  

    Para obter mais informações, consulte os [procedimentos suplementares para criar e implementar aplicações para computadores Mac](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Criar e implementar a app

1. Na consola 'Gestor de Configuração', [crie uma aplicação](../../../../apps/get-started/creating-mac-computer-applications.md) a partir do ficheiro **CMClient.pkg.cmmac.**  

2. [Implemente esta aplicação](../../../../apps/deploy-use/deploy-applications.md) para computadores Mac na sua hierarquia.  

## <a name="install-the-updated-client"></a>Instalar o cliente atualizado

O cliente do Gestor de Configuração existente nos computadores Mac irá solicitar ao utilizador que esteja disponível uma atualização para instalar. Depois de instalarem o cliente, os utilizadores têm de reiniciar o computador Mac.  

Após o reinício do computador, o assistente de **inscrição** do computador executa automaticamente para solicitar um novo certificado de utilizador.

Se não utilizar a inscrição do Gestor de Configuração, mas instale o certificado de cliente independentemente do Gestor de Configuração, consulte os [clientes da Configuração para utilizar um certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a>Configure os clientes para usar um certificado existente

Utilize este procedimento para evitar que o Assistente de Inscrição de Computadores esteja em funcionamento e para configurar o cliente atualizado para utilizar um certificado de cliente existente.  

1. Na consola 'Gestor de Configuração', [crie um item](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) de configuração do tipo **Mac OS X**.  

1. Adicione uma definição a este item de configuração com o tipo de definição **Script**.  

1. Adicione o script seguinte à definição:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Adicione o item de configuração a uma linha de base de [configuração](../../../../compliance/deploy-use/create-configuration-baselines.md). Em seguida, [implemente a linha de base de configuração](../../../../compliance/deploy-use/deploy-configuration-baselines.md) para todos os computadores Mac que instalam um certificado independentemente do Gestor de Configuração.  
