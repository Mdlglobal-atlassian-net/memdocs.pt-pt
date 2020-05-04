---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710889"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.** Clique em **configurar a cogestão** na fita para abrir o **Assistente de Configuração de Cogestão**.

2. Na página **de Subscrição** do assistente, selecione **Iniciar sessão**. Inscreva-se no seu inquilino Intune e, em seguida, selecione **Next**.  

3. Na página **de Habilitação,** escolha a sua inscrição automática na definição **Intune,** **piloto** ou **tudo**. Se um dispositivo não estiver inscrito pelo utilizador, na próxima avaliação da apólice, irá reinscrever-se. <!--3330596--> 

    Esta ação permite a inscrição automática de clientes em Intune para os clientes existentes do Gestor de Configuração. Quando escolher o **Pilot**, apenas os clientes do Gestor de Configuração que são membros da coleção piloto estão automaticamente inscritos no Intune. Esta opção permite-lhe permitir a cogestão num subconjunto de clientes para testar inicialmente a cogestão e a cogestão do rollout utilizando uma abordagem faseada. 

    > [!Note]  
    > A partir da versão 1806, a inscrição automática não é imediata para todos os clientes. Este comportamento ajuda a escala de inscrição melhor para grandes ambientes. O Gestor de Configuração aleatoriamente ainscrição com base no número de clientes. Por exemplo, se o seu ambiente tem 100.000 clientes, quando permite esta configuração, a inscrição ocorre ao longo de vários dias.<!--1358003-->  

4. Para dispositivos baseados na Internet que já estejam matriculados em Intune, copie e guarde a linha de comando na página **de Habilitação.** Pode utilizar esta linha de comando para instalar o cliente do Gestor de Configuração como uma aplicação em Intune. Se não guardar esta linha de comando agora, pode rever a configuração de cogestão a qualquer momento para obter esta linha de comando.

5. Na página **Workloads,** para cada carga de trabalho, escolha qual o grupo de dispositivos para se deslocar para gestão com intune. Para mais informações, consulte [Cargas de Trabalho](../workloads.md).  

    Se só quiser ativar a cogestão, não precisa de mudar de carga de trabalho agora. Pode trocar de carga de trabalho mais tarde. Para mais informações, consulte [Como mudar as cargas de trabalho](../how-to-switch-workloads.md).  

    A definição **Pilot Intune** comuta a carga de trabalho associada apenas para os dispositivos da recolha do piloto. A definição **Intune** comuta a carga de trabalho associada para todos os dispositivos do Windows 10 cogeridos.  

    > [!Important]
    > Antes de trocar as cargas de trabalho, certifique-se de configurar corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre geridas por uma das ferramentas de gestão dos seus dispositivos.  

6. Na página **de Encenação,** configure as seguintes definições:  

    - **Piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte do seu lançamento faseado de cogestão. Comece com uma pequena coleção de testes e, em seguida, adicione mais coleções ao grupo piloto à medida que lança a cogestão a mais utilizadores e dispositivos. Pode alterar as coleções do grupo piloto a qualquer momento.  

    - **Produção**: Configure o **grupo exclusão** com uma ou mais coleções. Os dispositivos que sejam membros de qualquer uma das coleções deste grupo estão excluídos da utilização da cogestão.  

7. Para permitir a cogestão, complete o assistente.  
