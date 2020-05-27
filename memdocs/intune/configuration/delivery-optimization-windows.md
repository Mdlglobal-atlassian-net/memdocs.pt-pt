---
title: Definições de Otimização de Entrega para windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Configure como os dispositivos do Windows 10 gere com a Otimização de Entrega intune. Em Intune, crie um perfil de configuração do dispositivo para instalar atualizações a partir da internet. Consulte também como substituir os anéis de atualização existentes por um perfil de Otimização de Entrega.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 4d491a3210229d5dd6c74ccaed7f44c4ae4eb83c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990069"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Definições de otimização de entrega no Microsoft Intune

Com o Intune, utilize as definições de Otimização de Entrega para os dispositivos Windows 10 para reduzir o consumo de largura de banda quando esses dispositivos descarregarem aplicações e atualizações. Configure a Otimização da Entrega como parte dos perfis de configuração do seu dispositivo.  

Este artigo descreve como configurar as definições de Otimização de Entrega como parte de um perfil de configuração do dispositivo. Depois de criar um perfil, atribui ou implementa esse perfil para os seus dispositivos Windows 10.

Para ver uma lista das definições de Otimização de Entrega que o Intune suporta, consulte as definições de [Otimização de Entrega para Intune](delivery-optimization-settings.md).  

Para saber mais sobre a Otimização de Entregas no Windows 10, consulte [as atualizações](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) de Otimização de Entrega na documentação do Windows.  

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Introduza as seguintes propriedades:

   - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
   - **Perfil**: **Selecione Otimização de Entrega**.

4. Selecione **Criar**.

5. No Básico, insira as **seguintes**propriedades:

   - **Nome**: introduza um nome descritivo para o novo perfil.
   - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Na página de definições de **Configuração,** defina como pretende que as atualizações e aplicações descarreguem. Para obter informações sobre as definições disponíveis, consulte [as definições de Otimização de Entrega para Intune](delivery-optimization-settings.md).

   Quando terminar as definições de configuração, selecione **Next**.

8. Na página **Scope (Tags),** selecione **Selecione etiquetas** de âmbito para abrir o painel *de etiquetas Select para* atribuir etiquetas de âmbito ao perfil.
  
   Selecione **Seguinte** para continuar.

9. Na página **de Atribuiçãos,** selecione os grupos que receberão este perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](../configuration/device-profile-assign.md).

   Selecione **Seguinte**.

10. Na página regras de **aplicabilidade,** utilize as opções **de Regra**, **Propriedade**e **Valor** para definir como este perfil se aplica dentro dos grupos designados.

11. Na página **Review + criar** página, quando terminar, escolha **Criar**. O perfil é criado e é mostrado na lista.

Da próxima vez que cada dispositivo entrar, a apólice é aplicada.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Remover otimização de entrega dos anéis de atualização do Windows 10

A Otimização da Entrega foi previamente configurada como parte dos Anéis de Atualização de Software. A partir de fevereiro de 2019, as definições de Otimização de Entrega são configuradas como parte de um perfil de configuração de dispositivo de otimização de deliver, que inclui configurações adicionais que afetam mais do que a entrega de Atualizações de Software para dispositivos. Se ainda não o fez, remova a definição de Otimização de Entrega dos seus Anéis de Atualização, definindo-a para *Não configurada,* e depois utilize um perfil de Otimização de Entrega para gerir a maior gama de opções disponíveis.

1. Criar um perfil de configuração do dispositivo de otimização de entrega:

    1. No centro de administração do Microsoft Endpoint Manager, selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
    2. Introduza as seguintes propriedades:

        - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
        - **Perfil**: **Selecione Otimização de Entrega**.

    3. Selecione **Criar**.
    4. No Básico, insira as **seguintes**propriedades:

        - **Nome**: introduza um nome descritivo para o novo perfil.
        - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

    5. Selecione **Seguinte**.
    6. Nas definições de **configuração,** escolha o mesmo modo utilizado pelo anel de atualização de  >  **Download mode**software existente, a *menos que* pretenda alterar as definições que aplica nos seus dispositivos. As opções são:

        - **Não configurado**
        - **Apenas HTTP, sem espreitar**
        - **HTTP misturado com o olhar atrás do mesmo NAT**
        - **HTTP misturado com olhing em um grupo privado**
        - **HTTP misturado com o peering da Internet**
        - **Modo de descarregamento simples sem espreitar**
        - **Modo bypass**

    7. Configure [quaisquer definições adicionais](delivery-optimization-settings.md) que queira gerir e continue a criar o perfil.

        Em **Atribuições**, atribua este novo perfil aos mesmos dispositivos e utilizadores que o anel de atualização de software existente. Para mais informações, consulte [a atribuição do perfil](device-profile-assign.md).

2. Desconfigure o anel de software existente:

    1. No centro de administração do Microsoft Endpoint Manager, vá a **atualizações** de Software > Windows 10 Update Rings.
    2. Na lista, selecione o seu anel de atualização.
    3. Nas definições, desajuste o modo de transferência de **otimização** da entrega para **Não configurado**.
    4. **OK**  >  **Guarde** as suas alterações.

## <a name="next-steps"></a>Passos seguintes

Depois de [atribuir o perfil,](device-profile-assign.md) [monitorize o seu estado.](device-profile-monitor.md)

Consulte as definições de [Otimização de Entrega](delivery-optimization-settings.md) para Intune.
