---
title: Ações remotas com cogestão
titleSuffix: Configuration Manager
description: Executar ações remotas a partir de Intune para dispositivos cogeridos
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075324"
---
# <a name="remote-actions-with-co-management"></a>Ações remotas com cogestão

Tem de se certificar de que todos os dispositivos que gere são acessíveis, independentemente de onde esteja, sempre que se conecta. Também precisa de fornecer a cada utilizador tudo o que precisa para se manter produtivo, protegendo as aplicações e dados. Com as ações do dispositivo suportadas por Intune, pode resolver remotamente estas funções críticas.

No vídeo seguinte, a diretora de programas Heidi Cheng e o gestor de programas sénior Danny Guillory discutem e demo ações remotas com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Benefícios

As ações do dispositivo remoto dão-lhe controlos de gestão no dispositivo sem interferir com os dados pessoais. Estas ações de dispositivo remoto permitem: 
- Eliminar dados da empresa sobre dispositivos perdidos ou roubados  
- Mudar o nome de um dispositivo  
- Reiniciar um dispositivo  
- Rever o inventário do dispositivo  
- Controlar remotamente um dispositivo  
- Eliminar aplicativos OEM pré-instalados com um reboot fresh start  
- Faça uma reset de fábrica em qualquer dispositivo do Windows 10  

Estas funções são uma forma importante e simples de proteger os dados corporativos armazenados nestes dispositivos, seja no e-mail ou no OneDrive.

Para obter mais informações sobre estas ações, consulte [as ações remotas disponíveis.](#available-remote-actions) 



## <a name="case-studies"></a>Estudos de caso

A empresa de consultoria global Avanade usa regularmente ações remotas para gerir os dispositivos utilizados pelos seus 30.000 colaboradores. Numa recente publicação no [blogue,](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)o CIO de Avanade observou:

> *A nossa vitória imediata de ter a funcionalidade Intune foi a capacidade de redefinir remotamente o Windows numa máquina. Isto é importante para nós para máquinas perdidas ou roubadas, o que é mais comum na nossa mão de obra altamente móvel.* 
> Esta é uma funcionalidade que de outra forma teríamos de *construir e manter num pacote configMgr personalizado.*

Para obter mais informações sobre como utilizar estas ações remotas, consulte [as ações do dispositivo disponível.](../../intune/remote-actions/device-management.md#available-device-actions)


## <a name="value-proposition"></a>Proposta de valor

Quando um dispositivo de Gestor de Configuração é cogerido, adiciona imediatamente estas funções que o Gestor de Configuração não tem de forma nativa. Agora pode fazer qualquer ação remota que seja apoiada por Intune. 

Com a cogestão, os dispositivos Do Gestor de Configuração são agora como qualquer outro dispositivo gerido pelo Intune. Por exemplo, eles têm uma presença total na nuvem, e você pode alcançá-los desde que eles tenham acesso à Internet. Você pode fazer todas estas ações sem tomar quaisquer passos adicionais além de permitir a cogestão.

Uma vez que o processo de inscrição automática é transparente para o utilizador, não há impacto na sua produtividade. O utilizador não precisa de fazer nada.


### <a name="available-remote-actions"></a>Ações remotas disponíveis

Utilize estas ações remotas a partir de Intune uma vez que permite a [cogestão](how-to-enable.md) no Gestor de Configuração.

#### <a name="remove-devices"></a>Remover dispositivos
- **Aposentado :** Esta ação remove aplicações e dados geridos (quando aplicável), configurações e perfis de e-mail que foram atribuídos a esse dispositivo. O dispositivo é então removido da gestão intune. Este processo acontece da próxima vez que o dispositivo faz o check-in e recebe a ação de aposentadoria remota. A função Retire deixa os dados pessoais do utilizador no dispositivo.  

- **Limpeza**: Esta ação restaura um dispositivo às suas definições predefinidas de fábrica. Se escolher a opção de reter o estado de **inscrição e**a conta de utilizador, então os dados do utilizador são mantidos. Caso contrário, a unidade é apagada de forma segura.  

- **Eliminar**: Se pretender remover os dispositivos do portal Intune on Azure, elimine-os do painel específico do dispositivo. Da próxima vez que o dispositivo verificar, remove quaisquer dados organizacionais armazenados nele.  

Para mais informações, consulte [Remova os dispositivos utilizando a limpeza, a retirada ou a desinscrição manual do dispositivo](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Eliminação seletiva
<!--SCCMDocs issue 973-->
Ao escolher uma limpeza seletiva da **App,** remove os dados da aplicação da empresa sem remover dados pessoais. Utilize esta ação quando um dispositivo for reportado como perdido ou roubado. 

Para mais informações, consulte [Como eliminar apenas dados corporativos de aplicações geridas por Intune](.. /.. /intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Sync
A ação **Sincronizar** dispositivo força o dispositivo selecionado a registar-se imediatamente com o Intune. Quando um dispositivo faz o check-in, recebe imediatamente quaisquer ações ou políticas pendentes que lhe tenha atribuído.

Esta funcionalidade pode ajudá-lo a validar imediatamente e a resolver as políticas que atribuiu, sem esperar pelo próximo check-in agendado.

Para mais informações, consulte os [dispositivos Sync para obter as mais recentes políticas e ações com o Intune](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Reiniciar
A ação do dispositivo **Restart** faz com que o dispositivo que opte por reiniciar. Esta ação é útil quando há um reboot pendente, mas o utilizador não está disponível para fazê-lo.

Para mais informações, consulte os dispositivos de [reinício remotamente com intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Começar do Zero
A ação do dispositivo **Fresh Start** remove todas as aplicações instaladas num dispositivo que executa o Windows 10, versão 1703 ou posterior. Fresh Start ajuda a remover aplicações pré-instaladas (OEM) que são normalmente instaladas com um novo dispositivo.

Se optar por não reter os dados do utilizador, o dispositivo restaura o seu estado fora da caixa. Desinscriça-se da Azure AD e do MDM.

Se tiver padrões pré-determinados em relação às aplicações que devem estar no dispositivo, então esta ação elimina as que não cumprem os seus critérios.

Para mais informações, consulte [Use Fresh Start para redefinir dispositivos Windows 10 com Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Controlo remoto
Os dispositivos geridos pelo Intune podem ser administrados remotamente com o [TeamViewer](https://www.teamviewer.com/). TeamViewer é um programa de terceiros que adquire separadamente.

Para mais informações, consulte [use TeamViewer para administrar remotamente os dispositivos Intune](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Configurar

Para além do controlo remoto via TeamViewer, para começar a utilizar estas ações de dispositivoremoto remoto no Intune, não é necessária nenhuma configuração adicional depois de ativar a [cogestão](how-to-enable.md).

Para obter mais informações sobre a utilização do TeamViewer para controlo remoto, consulte [o Use TeamViewer para administrar remotamente os dispositivos Intune](../../intune/remote-actions/teamviewer-support.md).
