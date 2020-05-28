---
title: Proteção Avançada Contra Ameaças do Microsoft Defender
titleSuffix: Configuration Manager
description: Saiba como gerir e monitorizar a Proteção avançada de ameaças do Microsoft Defender, um novo serviço que ajuda as empresas a responder a ataques avançados.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801aee9665e567ce1a983fba294f1e58f58eee04
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406670"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Microsoft Defender

*Aplica-se a: Gestor de Configuração (ramo atual)*

Endpoint Protection pode ajudar a gerir e monitorizar a Proteção avançada de [ameaças (ATP) do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (anteriormente conhecido como Windows Defender ATP). O Microsoft Defender ATP ajuda as empresas a detetar, investigar e responder a ataques avançados nas suas redes. As políticas do Gestor de Configuração podem ajudá-lo a bordo e monitorizar os clientes do Windows 10.

O Microsoft Defender ATP é um serviço no [Windows Defender Security Center](https://securitycenter.windows.com). Ao adicionar e implementar um ficheiro de configuração de embarque de cliente, o Gestor de Configuração pode monitorizar o estado de implementação e a saúde do agente ATP do Microsoft Defender. O Microsoft Defender ATP é suportado em PCs que executam o cliente do Gestor de Configuração ou [geridos pela Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Pré-requisitos

- Subscrição do serviço online Microsoft Defender Advanced Threat Protection  
- Computadores de clientes que executam o cliente do Gestor de Configuração
- Clientes que utilizem um SISTEMA listado na secção de [sistemas operativos de clientes suportados](#bkmk_os) abaixo.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a>Sistemas operativos de clientes suportados
Com base na versão do Gestor de Configuração que está a executar, os seguintes sistemas operativos do cliente podem ser abordados:

#### <a name="configuration-manager-version-1910-and-prior"></a>Versão 1910 e anterior do Gestor de Configuração

- Computadores de clientes com windows 10, versão 1607 e mais tarde

#### <a name="configuration-manager-version-2002-and-later"></a>Versão de Gestor de Configuração 2002 e posterior
<!--5229962-->
A partir da versão de 'Gestor de Configuração' de 2002, pode embarcar nos seguintes sistemas operativos:

- Windows 8.1
- Windows 10, versão 1607 ou mais tarde
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, versão 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Criar um ficheiro de configuração de embarque

1. Vá ao [serviço online ATP](https://securitycenter.windows.com/) do Microsoft Defender e inscreva-se.
1. Selecione **Gestão da Máquina** em **Definições**, e, em seguida, selecione **Onboarding**.
1. Selecione os sistemas operativos que pretende embarcar a bordo da lista.
   - Se estiver a embarcar no Windows 10, Windows Server 1803 e Windows Server 2019:
      1. Selecione **Configuração Manager (ramo atual) versão 1606** e selecione **pacote de descarregamento**.
      1. Descarregue o ficheiro de arquivo comprimido (.zip) e extrai o conteúdo.
   - Se estiver a embarcar noutro sistema operativo Windows:
      1. Selecione os sistemas operativos que deseja embarcar a partir da lista apresentada no serviço online ATP microsoft Defender.
      1. Copie os valores para a **chave Workspace** e **ID workspace** da secção de **ligação Configure** assim que o processo estiver concluído.

> [!IMPORTANT]
> - O ficheiro de configuração ATP microsoft Defender contém informações sensíveis que devem ser mantidas seguras.

## <a name="onboard-devices"></a>Dispositivos a bordo

1. Na consola De Configuração Manager, navegue para **Ativos e Compliance**  >  **Endpoint Protection**As políticas  >  **ATP do Windows Defender** e selecione Create Windows Defender **ATP Policy**. Abre o Assistente de Política ATP da Microsoft Defender.  
1. Digite o **nome** e **descrição** para a política ATP do Microsoft Defender e selecione **Onboarding**.
1. **Navegue** no ficheiro Configuração fornecido pelo inquilino do serviço de nuvem ATP da sua organização.
   - Para o Windows 8.1 ou Windows Server 2012 R2 e 2016, forneça a **chave Workspace** e **o ID do espaço de trabalho**.
   - Para a versão de 2002 do Gestor de Configuração, necessitará da **chave Workspace** e **do Id workspace,** mesmo que esteja a embarcar apenas no Windows Server 2019 e no Windows Server 1803 ou dispositivos posteriores. Obtenha estes valores selecionando **Definições**  >  **De embarque**no Windows 7 e  >  **8.1** do serviço online MICROSOFT Defender [ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Especifique as amostras de ficheiro que são recolhidas e partilhadas a partir de dispositivos geridos para análise.  

   - **Nenhum**

   - **Todos os tipos de ficheiros**  
1. Reveja o resumo e complete o assistente.  

Selecione **Implementar** para direcionar a política ATP do Microsoft Defender para os clientes.

## <a name="monitor"></a>Monitorizar

1. Na consola 'Gestor de Configuração', navegue na **Segurança de Monitorização**  >  **Security** e, em seguida, selecione O Windows **Defender ATP**.  

1. Reveja o painel de proteção de ameaças avançada do Microsoft Defender.  

    - **Estado de implementação**do Agente Windows Defender : O número e percentagem de computadores de clientes geridos elegíveis com a política ATP ativa do Microsoft Defender a bordo  

    - **Windows Defender ATP Agent Health**: Percentagem de clientes de computador que reportam o estado do seu agente ATP Microsoft Defender  

        - **Saudável** - Trabalhar corretamente  

        - **Inativo** - Não há dados enviados ao serviço durante o período de tempo  

        - **Estado do agente** - O serviço de sistema para o agente no Windows não está a funcionar  

        - **Não a bordo** - A política foi aplicada, mas o agente não reportou a política a bordo  

## <a name="create-an-offboarding-configuration-file"></a>Criar um ficheiro de configuração offboarding  

1. Inscreva-se no [serviço online ATP](https://securitycenter.windows.com/)do Microsoft Defender .

1. Selecione **Gestão da Máquina** em **Definições**, e, em seguida, selecione **Onboarding**.  

1. Selecione **Select Configuration Manager (ramo atual) versão 1606** e selecione **Offboarding Endpoint**.  

1. Descarregue o ficheiro de arquivo comprimido (.zip) e extrai o conteúdo. Os ficheiros offboarding são válidos por 30 dias.

1. Na consola De Configuração Manager, navegue para **Ativos e Compliance**  >  **Endpoint Protection**As políticas  >  **ATP do Windows Defender** e selecione Create Windows Defender **ATP Policy**. Abre o Assistente de Política ATP da Microsoft Defender.  

1. Digite o **nome** e **descrição** para a política ATP do Microsoft Defender e selecione **Offboarding**.

1. **Navegue** no ficheiro Configuração fornecido pelo inquilino do serviço de nuvem ATP da sua organização.

1. Reveja o resumo e complete o assistente.  

Selecione **Implementar** para direcionar a política ATP do Microsoft Defender para os clientes.  

> [!IMPORTANT]
> Os ficheiros de configuração ATP do Microsoft Defender contêm informações sensíveis que devem ser mantidas seguras.

## <a name="next-steps"></a>Próximos passos

- [Proteção Avançada Contra Ameaças do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Problemas de resolução de problemas Microsoft Defender Advanced Threat Protection onboarding questões](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
