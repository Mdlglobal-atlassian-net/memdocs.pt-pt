---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710896"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.** Clique em **configurar a cogestão** na fita para abrir o **Assistente de Configuração de Cogestão**.

2. Na página **de Subscrição** do assistente, configure as seguintes definições:

    - O **ambiente Azure** para usar. Por exemplo, a Nuvem Pública Azure ou a Nuvem governamental azure dos EUA.<!--4075452-->  

    - Selecione **Iniciar sessão**. Inscreva-se como administrador global da AD Azure e, em seguida, selecione **Next**.  

        > [!TIP]
        > Assinas isto uma vez para os propósitos deste feiticeiro. As credenciais não são armazenadas ou reutilizadas noutro lugar.

3. Na página **de Habilitação,** escolha as seguintes definições:

   - **Inscrição automática em Intune** - Permite a inscrição automática do cliente em Intune para os clientes existentes do Gestor de Configuração. Esta opção permite-lhe permitir a cogestão num subconjunto de clientes para testar inicialmente a cogestão e a cogestão do rollout utilizando uma abordagem faseada. Se um dispositivo não estiver inscrito pelo utilizador, na próxima avaliação da apólice, irá reinscrever-se. <!--3330596-->

      - **Piloto** - Apenas os clientes do Gestor de Configuração que são membros da coleção **intune Auto Registration** estão automaticamente inscritos no Intune.
      - **Tudo** - Ativar a inscrição automática para todos os clientes do Windows 10, versão 1709 ou posterior.

   - **Inscrição Automática Intune** - Esta coleção deve conter todos os clientes que pretende embarcar em cogestão. É essencialmente um superconjunto de todas as outras coleções de encenação.

   ![Especificar a recolha de matrículas automáticas Intune ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > A partir da versão 1806, a inscrição automática não é imediata para todos os clientes. Este comportamento ajuda a escala de inscrição melhor para grandes ambientes. O Gestor de Configuração aleatoriamente ainscrição com base no número de clientes. Por exemplo, se o seu ambiente tem 100.000 clientes, quando permite esta configuração, a inscrição ocorre ao longo de vários dias.<!--1358003-->  
      >
      > A partir da versão de 1906:
      >
      > - Um novo dispositivo cogerido inscreveu-se automaticamente no serviço Microsoft Intune com base no seu *token* de dispositivo Azure Ative Directory (Azure AD). Não é preciso esperar que um utilizador inicie o contrato para a inscrição automática. Esta alteração ajuda a reduzir o número de dispositivos com o estado de inscrição Pendente de *registo do utilizador*.<!-- 4454491 --> Para suportar este comportamento, o dispositivo precisa de estar a executar o Windows 10, versão 1803 ou mais tarde. Para mais informações, consulte o estado de [inscrição na cogestão.](../how-to-monitor.md#co-management-enrollment-status)
      >
      > - Se já tem dispositivos matriculados para cogestão, os novos dispositivos matriculam-se imediatamente assim que cumprem os [pré-requisitos](../overview.md#prerequisites).<!--4321130-->

4. Para dispositivos baseados na Internet que já estejam matriculados em Intune, copie e guarde a linha de comando na página **de Habilitação.** Utilizará esta linha de comando para instalar o cliente do Gestor de Configuração como uma aplicação em Intune para dispositivos baseados na Internet. Se não guardar esta linha de comando agora, pode rever a configuração de cogestão a qualquer momento para obter esta linha de comando.

5. Na página **Workloads,** para cada carga de trabalho, escolha qual o grupo de dispositivos para se deslocar para gestão com intune. Para mais informações, consulte [Cargas de Trabalho](../workloads.md). Se só quiser ativar a cogestão, não precisa de mudar de carga de trabalho agora. Pode trocar de carga de trabalho mais tarde. Para mais informações, consulte [Como mudar as cargas de trabalho](../how-to-switch-workloads.md).  

    - **Pilot Intune** - Muda a carga de trabalho associada apenas para os dispositivos nas coleções piloto que irá especificar na página **de Encenação.** Cada carga de trabalho pode ter uma coleção piloto diferente.
    - **Intune** - Muda a carga de trabalho associada para todos os dispositivos do Windows 10 cogeridos.  

    > [!Important]
    > Antes de trocar as cargas de trabalho, certifique-se de configurar corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre geridas por uma das ferramentas de gestão dos seus dispositivos.  

6. Na página **de Encenação,** especifique a coleção piloto para cada uma das cargas de trabalho definidas para **O Plano De Intune**Piloto .

   ![Especificar a recolha de matrículas automáticas Intune ](../media/3555750-co-management-onboarding-staging.png)

7. Para permitir a cogestão, complete o assistente.
