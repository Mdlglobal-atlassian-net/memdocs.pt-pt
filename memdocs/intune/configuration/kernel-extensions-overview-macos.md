---
title: Criar extensões do sistema macOS e kernel com a Microsoft Intune - Azure [ Microsoft Docs
titleSuffix: ''
description: Adicione ou crie um perfil de dispositivo macOS que configura extensões do sistema ou extensões de kernel para permitir a sobreposição do utilizador, adiciona identificador de equipa e adiciona um pacote e identificador de equipa no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea801f528199dfee419ae8bbea63f53c45c7e43a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429588"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Adicione o sistema macOS e as extensões de kernel em Intune

> [!NOTE]
> As extensões de kernel macOS estão a ser substituídas por extensões do sistema. Para mais informações, consulte [Dica de Suporte: Utilizar extensões do sistema em vez de extensões de kernel para macOS Catalina 10.15 em Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Nos dispositivos macOS, pode adicionar extensões de kernel e extensões do sistema. Ambas as extensões de kernel e extensões do sistema permitem que os utilizadores instalem extensões de aplicações que alargam as capacidades nativas do sistema operativo. As extensões de kernel executam o seu código ao nível do núcleo. As extensões do sistema funcionam num espaço de utilizador bem controlado.

Para adicionar extensões que são sempre autorizadas a carregar nos seus dispositivos, utilize o Microsoft Intune. Intune usa "perfis de configuração" para criar e personalizar estas configurações para as necessidades da sua organização. Depois de adicionar estas funcionalidades num perfil, empurre ou implemente o perfil para dispositivos macOS na sua organização.

Este artigo descreve extensões do sistema e extensões de kernel. Também mostra como criar um perfil de configuração do dispositivo usando extensões em Intune.

## <a name="system-extensions"></a>Extensões do sistema

As extensões do sistema funcionam no espaço do utilizador e não acedem ao núcleo. O objetivo é aumentar a segurança, fornecer mais controlo final do utilizador e limitar os ataques ao nível do kernel. Estas extensões podem ser:

- Extensões do condutor, incluindo condutores para USB, cartões de interface de rede (NIC), controladores em série e dispositivos de interface humana (HID)
- Extensões de rede, incluindo filtros de conteúdo, proxies DNS e clientes VPN
- Extensões de segurança de ponto final, incluindo deteção de pontofinal, resposta de ponto final e antivírus

As extensões do sistema estão incluídas no pacote de uma aplicação e instaladas a partir da aplicação.

Para obter mais informações sobre as extensões do sistema, consulte [as extensões](https://developer.apple.com/documentation/systemextensions) do sistema (abre o site da Apple).

## <a name="kernel-extensions"></a>Extensões kernel

As extensões de kernel adicionam características ao nível do núcleo. Estes recursos de acesso a partes do SISTEMA que os programas regulares não podem aceder. A sua organização pode ter necessidades ou requisitos específicos que não estejam disponíveis numa aplicação, uma funcionalidade de dispositivo, e assim por diante.

Por exemplo, tem um programa de digitalização de vírus que digitaliza o seu dispositivo para obter conteúdo malicioso. Pode adicionar a extensão do núcleo de digitalização do vírus como uma extensão de kernel permitida em Intune. Em seguida, "atribuir" a extensão aos seus dispositivos macOS.

Com esta funcionalidade, os administradores podem permitir que os utilizadores sobreporem extensões de kernel, adicionar identificadores de equipa e adicionar extensões específicas de kernel em Intune.

Para obter mais informações sobre extensões de [kernel, consulte extensões de kernel](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (abre o site da Apple).

## <a name="prerequisites"></a>Pré-requisitos

- Esta funcionalidade aplica-se a:

  - macOS 10.13.2 e mais recentes (extensões de kernel)
  - macOS 10.15 e mais recentes (extensões do sistema)

  De macOS 10.15 a 10.15.4, as extensões de kernel e as extensões do sistema podem ser executadas lado a lado.

- Para utilizar esta funcionalidade, os dispositivos devem ser:

  - Matriculado em Intune utilizando o Programa de Inscrição de Dispositivos da Apple (DEP). [Os dispositivos macOS de inscrição automática](../enrollment/device-enrollment-program-enroll-macos.md) têm mais informações.

    OU

  - Matriculado em Intune com "inscrição aprovada pelo utilizador" (termo da Apple). [Prepare-se para alterações às extensões de kernel no macOS High Sierra](https://support.apple.com/en-us/HT208019) (abre o site da Apple) tem mais informações.

## <a name="what-you-need-to-know"></a>O que tem de saber

- Podem ser adicionadas extensões de kernel legado não assinadas e extensões do sistema.
- Certifique-se de introduzir o identificador de equipa correto e adtifique a identidade da extensão. Intune não valida os valores que entra. Se introduzir informações erradas, a extensão não funcionará no dispositivo. Um identificador de equipa tem exatamente 10 caracteres alfanuméricos.

> [!NOTE]
> A Apple divulgou informações sobre a assinatura e a notização de todos os softwares. No macOS 10.14.5 e mais recente, as extensões de kernel implementadas através do Intune não têm de cumprir a política de notização da Apple.
>
> Para obter informações sobre esta política de notariação, e quaisquer atualizações ou alterações, consulte os seguintes recursos:
>
> - [Notar a sua aplicação antes](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) da distribuição (abre o site da Apple) 
> - [Prepare-se para alterações às extensões de kernel no macOS High Sierra](https://support.apple.com/en-us/HT208019) (abre o site da Apple)

## <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **macOS**
    - **Perfil**: **Selecione extensões**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para a apólice. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de política é **macOS: Adicione a varredura antivírus às extensões**do núcleo nos dispositivos .
    - **Descrição**: Insira uma descrição para a apólice. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração,** configure as definições:

    - [macOS](kernel-extensions-settings-macos.md)

8. Selecione **Seguinte**.
9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="next-steps"></a>Próximos passos

Depois que o perfil é criado, está pronto para ser atribuído. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).
