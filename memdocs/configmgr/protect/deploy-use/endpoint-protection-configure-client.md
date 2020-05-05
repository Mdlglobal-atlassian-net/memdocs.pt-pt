---
title: Definições do cliente de proteção endpoint
titleSuffix: Configuration Manager
description: Saiba como configurar as definições personalizadas do cliente para a Proteção de Endpoint.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724322"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições personalizadas de cliente para o Endpoint Protection

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este procedimento configura as definições personalizadas do cliente para a Proteção de Endpoint, que pode implementar para coleções de dispositivos na sua hierarquia.

> [!IMPORTANT]  
>  Apenas configure as definições padrão do cliente endpoint Protection se tiver a certeza de que as quer aplicadas a todos os computadores da sua hierarquia. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para ativar o Endpoint Protection e configurar definições personalizadas de cliente

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração** , clique em **Definições do Cliente**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Definições Personalizadas do Dispositivo Cliente**.  

4. Na caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** , forneça um nome e uma descrição para o grupo de definições e, em seguida, selecione **Endpoint Protection**.  

5. Configure as definições do cliente endpoint Protection que você precisa. Para obter uma lista completa das definições do cliente endpoint Protection que possa configurar, consulte a secção de Proteção de Pontofinal em [sobre as definições](../../core/clients/deploy/about-client-settings.md#endpoint-protection)do cliente .  

   > [!IMPORTANT]  
   >  Instale a função do sistema de proteção de pontos finais antes de configurar as definições do cliente para proteção de pontofinal.  

6. Clique em **OK** para fechar a caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** . As novas definições de cliente são apresentadas no nó **Definições do Cliente** da área de trabalho **Administração** .  

7. Em seguida, desloque as definições personalizadas do cliente para uma coleção. Selecione as definições personalizadas do cliente que pretende implementar. No separador **Casa,** no grupo Definições do **Cliente,** clique em **Implementar**.  

8. Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual pretende implementar as definições de cliente e, em seguida, clique em **OK**. A nova implementação é apresentada no separador **Implementações** do painel de detalhes.  

Os clientes estão configurados com estas configurações quando descarregam a próxima política do cliente. Para mais informações, consulte [Iniciar a recuperação de políticas para um cliente do Gestor de Configuração](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Como fornecer o cliente Endpoint Protection numa imagem de disco

Instale o cliente Endpoint Protection num computador que pretende utilizar como fonte de imagem de disco para a implementação do Sistema de Configuração O. Este computador é normalmente designado computador de referência. Depois de criar a imagem DE SO, utilize a implementação do Sistema de Configuração OS para implementar a imagem.

> [!Important]  
> O Windows 10 e o Windows Server 2016 têm o Windows Defender instalado por padrão. Não precisa deste procedimento nessas versões do Windows.  

Utilize os seguintes procedimentos para o ajudar a instalar e configurar o cliente endpoint Protection num computador de referência.


### <a name="prerequisites"></a>Pré-requisitos

A lista que se segue contém os pré-requisitos necessários para a instalação do software cliente Endpoint Protection num computador de referência.

- Tem de ter acesso ao pacote de instalação do cliente Endpoint Protection, **scepinstall.exe**. Encontre este pacote na pasta **Cliente** da pasta de instalação do Gestor de Configuração no servidor do site.  

- Para implementar o cliente Endpoint Protection com a configuração necessária da sua organização, crie e exporte uma política antimalware. Em seguida, especifique esta política quando instalar manualmente o cliente de Proteção de Pontofinal. Para mais informações, consulte [Como criar e implementar políticas antimalware.](endpoint-antimalware-policies.md)  

  > [!NOTE]  
  >  Não pode exportar a **Política Antimalware de Cliente Padrão.**  

- Se pretender instalar o cliente Endpoint Protection com as definições mais recentes, descarregue-os a partir da Inteligência de [Segurança do Windows Defender](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> A partir do 'Gestor de Configuração' 1802, não é necessário instalar o agente de proteção de pontofinal (SCEPInstall) nos dispositivos do Windows 10. Se já estiver instalado nos dispositivos do Windows 10, o Gestor de Configuração não o remove. Os administradores podem remover o agente de proteção de ponto final nos dispositivos do Windows 10 que estão a executar pelo menos a versão cliente de 1802. O SCEPInstall.exe ainda pode estar presente em C:\Windows\ccmsetup em algumas máquinas, mas as novas instalações de clientes não devem descarregá-lo. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Como instalar o cliente Endpoint Protection no computador de referência

Instale o cliente Endpoint Protection localmente no computador de referência a partir de um pedido de comando. Primeiro obtenha o ficheiro de instalação **scepinstall.exe**. Para mais informações, consulte Instalar o cliente de Proteção de [Pontofinal a partir de um pedido de comando](#bkmk_manual-install).

Se necessário, inclua também uma política antimalware pré-configurada ou com uma política antimalware que exportou anteriormente. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a>Para instalar o cliente endpoint Protection a partir de um pedido de comando

1. Copie **scepinstall.exe** da pasta **cliente** da pasta de instalação do Gestor de Configuração para o computador no qual pretende instalar o software cliente endpoint Protection.  

2. Abra uma linha de comandos como administrador. Mude o diretório para a pasta com o instalador. Em `scepinstall.exe`seguida, executar, adicionando quaisquer propriedades adicionais da linha de comando que você precisa:


   |  Propriedade   |                                  Descrição                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Executar o instalador silenciosamente                           |
   |    `/q`     |                        Extrair os ficheiros de configuração em silêncio                        |
   |    `/i`     |                           Executar o instalador normalmente                           |
   |  `/policy`  | Especifique um ficheiro de política antimalware para configurar o cliente durante a instalação |
   | `/sqmoptin` |     Opt-in para o Programa de Melhoria da Experiência do Cliente da Microsoft (CEIP)     |


3. Siga as instruções no ecrã para completar a instalação do cliente.  

4. Se tiver transferido o pacote de definição de atualização mais recente, copie o pacote para o computador cliente e, em seguida, faça duplo clique no pacote de definição para o instalar.  

   > [!NOTE]  
   >  Após a instalação do cliente Endpoint Protection, o cliente executa automaticamente uma verificação de atualização de definição. Se esta verificação de atualização for bem sucedida, não terá de instalar manualmente o pacote de atualização de definição mais recente.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Exemplo: instale o cliente com uma política antimalware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verifique a instalação do cliente endpoint Protection

Depois de instalar o cliente Endpoint Protection no seu computador de referência, verifique se o cliente está a trabalhar corretamente.

1.  No computador de referência, abra a **Proteção do Ponto final** do System Center da área de notificação do Windows.  

2.  No separador **Home** da caixa de diálogo **de proteção** do ponto final do Centro de Sistema, verifique se a **proteção em tempo real** está definida para **ligar**.  

3.  Verifique se é apresentado um dia para as definições **de** **Vírus e spyware**.  

4.  Para se certificar de que o seu computador de referência está pronto para imagens, sob **as opções de Digitalização,** selecione **Full**, e, em seguida, clique em **Digitalizar agora**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Prepare o cliente endpoint Protection para imagens

Execute os seguintes passos para preparar o cliente de Proteção de Pontofinal para a imagem:

1. No computador de referência, inscreva-se como administrador.  

2. Descarregue e instale **o PsExec** a partir do [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Execute um pedido de comando como administrador, mude o diretório para a pasta onde instalou PsTools e, em seguida, digite o seguinte comando:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Tenha cuidado quando dirigir o Editor de Registo desta forma. PsExec.exe executa-o no contexto LocalSystem.  

4. No Editor de Registo, elimine as seguintes teclas de registo:  

   > [!IMPORTANT]  
   >  Elimine estas teclas de registo como o último passo antes de imaginar o computador de referência. O cliente endpoint Protection recria estas chaves quando começa. Se reiniciar o computador de referência, elimine novamente as teclas de registo.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Está pronto para preparar o computador de referência para imagens.

Ao implementar uma imagem de OS que contenha o cliente endpoint Protection, reporta automaticamente informações ao site do Gestor de Configuração atribuído ao dispositivo. O cliente descarrega e aplica qualquer política antimalware direcionada.  



## <a name="see-also"></a>Consulte também

Para obter mais informações sobre a implementação do OS no Gestor de Configuração, consulte [Gerir as imagens do OS](../../osd/get-started/manage-operating-system-images.md).

