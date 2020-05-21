---
title: Configurar definições de proteção de ponto final no Microsoft Intune – Azure | Microsoft Docs
description: Crie definições de proteção de ponto final ao criar um perfil de dispositivo com o Windows 10 ou macOS no Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 6f1f262c3ef2d7f2ca363057055fa22a018498ec
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429789"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Adicionar definições de proteção de ponto final no Intune

Com o Intune, pode utilizar perfis de configuração do dispositivo para gerir funcionalidades comuns de proteção de pontos finais nos dispositivos, incluindo:

- Firewall
- BitLocker
- Permitir e bloquear aplicações
- Microsoft Defender e encriptação

Por exemplo, pode criar um perfil de proteção de ponto final que apenas permita aos utilizadores do macOS instalarem aplicações a partir da Mac App Store. Em alternativa, ative o Windows SmartScreen ao executar aplicações em dispositivos com o Windows 10.

Antes de criar um perfil, reveja os seguintes artigos que detalham as definições de proteção de pontofinal Que intune pode gerir para cada plataforma suportada:

- [Definições do macOS](endpoint-protection-macos.md)
- [Definições do Windows 10](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Criar um perfil de dispositivo com as definições de proteção de ponto final

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Introduza as seguintes propriedades:

    - **Plataforma**: Escolha a plataforma dos seus dispositivos. As opções são:

        - **macOS**
        - **Windows 10 e posterior**

    - **Perfil**: Selecione **proteção do ponto final**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

   - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política pode incluir o tipo de perfil e plataforma.

   - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração**, dependendo da plataforma que escolheu, as definições que pode configurar são diferentes. Escolha a sua plataforma para configurações detalhadas:

   - [Definições do macOS](endpoint-protection-macos.md)
   - [Definições do Windows 10](endpoint-protection-windows-10.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](../configuration/device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Adicione regras personalizadas de Firewall para dispositivos Windows 10

Quando configurar o Microsoft Defender Firewall como parte de um perfil que inclui regras de proteção de pontos finais para o Windows 10, pode configurar regras personalizadas para Firewalls. As regras personalizadas permitem expandir-se no conjunto pré-definido de regras de Firewall suportadas para o Windows 10.

Quando planeia perfis com regras personalizadas de Firewall, considere as seguintes informações, que podem afetar a forma como escolhe agrupar regras de firewall nos seus perfis:

- Cada perfil suporta até 150 regras de firewall. Quando se utiliza mais de 150 regras, crie perfis adicionais, cada um limitado a 150 regras.

- Para cada perfil, se uma única regra não for aplicável, todas as regras desse perfil são falhadas e nenhuma das regras é aplicada ao dispositivo.

- Quando uma regra não se aplica, todas as regras do perfil são reportadas como falhadas. Intune não pode identificar que regra individual falhou.  

As regras de Firewall que o Intune pode gerir são detalhadas no fornecedor de serviços de [configuração](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) do Windows Firewall (CSP). Para rever a lista de definições de firewall personalizadas para dispositivos Windows 10 que intune suporta, consulte [as regras de Firewall personalizadas](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Para adicionar regras de firewall personalizadas a um perfil de proteção Endpoint

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.

3. Para *a Plataforma*, selecione o Windows **10 e, posteriormente,** e, em seguida, para selecionar a **proteção de ponto final**do *Perfil* .

    Selecione **Criar**.

4. Introduza um **Nome** para o seu perfil > **Seguinte**.
5. Nas **definições de Configuração,** selecione **Microsoft Defender Firewall**. Para *as regras de Firewall,* selecione **Adicionar** para abrir a página **Criar** Regra.

6. Especifique as definições para a regra firewall e, em seguida, selecione **OK** para salvá-la. Para rever as opções de regra de firewall personalizadas disponíveis na documentação, consulte [as regras de Firewall personalizadas](endpoint-protection-windows-10.md#firewall-rules).

    1. A regra aparece na página *Microsoft Defender Firewall* na lista de regras.
    2. Para modificar uma regra, selecione a regra da lista, para abrir a página 'Regra de **Edição'.**
    3. Para eliminar uma regra de um perfil, selecione a elipse **(...)** para a regra e, em seguida, selecione **Delete**.
    4. Para alterar a ordem em que as regras se exibem, selecione a *seta para cima, para baixo o* ícone da seta no topo da lista de regras.

7. Selecione **Em seguida** até começar a **Rever + criar**. Quando selecionar **Criar,** as alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="next-steps"></a>Próximos passos

O perfil é criado, mas pode ainda não estar a fazer nada. Em seguida, [atribua o perfil](../configuration/device-profile-assign.md) e [monitorize o estado](../configuration/device-profile-monitor.md).
