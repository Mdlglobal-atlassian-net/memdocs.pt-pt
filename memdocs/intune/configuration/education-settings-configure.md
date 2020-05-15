---
title: Adicione ou configure as definições de educação no Microsoft Intune - Azure [ Microsoft Docs
description: Utilize a aplicação Take a Test num perfil de configuração do dispositivo no Windows 10 e posteriormente em dispositivos no Microsoft Intune. Crie um perfil de configuração utilizando as definições de Educação e introduza um URL de aplicação de teste, escolha como os utilizadores sinuem, monitorizem o ecrã durante o teste e permitam ou previnem sugestões de texto durante o teste.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 476f0c3ef058c1c051ce3b571adec5d48787ee0e
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401716"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Utilize a aplicação Take a Test em dispositivos Windows 10 no Microsoft Intune

Os perfis de educação em Intune são projetados para que os alunos faça um teste ou exame em dispositivos. Esta funcionalidade inclui a aplicação **Take a Test** e as definições para adicionar um URL de teste, escolher como os utilizadores finais se inscrevem no teste, e muito mais. Esta funcionalidade suporta a seguinte plataforma:

- Windows 10 e posterior

Quando o utilizador faz o sinal de entrada, a aplicação Take a Test abre automaticamente com o teste em que entrou. Nenhuma outra aplicação pode ser executada no dispositivo enquanto o teste estiver em curso. [A tomada de testes no Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) fornece mais detalhes sobre a aplicação Take a Test.

Este artigo lista os passos para criar um perfil de configuração do dispositivo no Microsoft Intune. Também inclui informações para ler e aprender sobre as definições de educação disponíveis para os seus dispositivos Windows 10.

## <a name="create-a-device-profile"></a>Criar um perfil de dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **o Windows 10 e mais tarde**.
    - **Perfil**: Selecione **avaliação segura (Educação)**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: introduza um nome descritivo para o novo perfil.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração,** introduza as definições que pretende configurar:

    - [Windows 10 e posterior](education-settings-windows.md)

8. Selecione **Seguinte**.

9. Nas **etiquetas de âmbito** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como ou `US-NC IT Team` `JohnGlenn_ITDepartment` . Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

    Selecione **Seguinte**.

10. Em **Atribuições,** selecione os utilizadores ou grupo de utilizadores que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](device-profile-assign.md).

    Selecione **Seguinte**.

11. Em **Review + criar,** reveja as suas definições. Quando selecionar **Criar,** as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

Da próxima vez que cada dispositivo entrar, a apólice é aplicada.

## <a name="next-steps"></a>Passos seguintes

Consulte uma lista das definições de [educação do Windows 10](education-settings-windows.md) e respetivas descrições.

Depois de atribuído o [perfil,](device-profile-assign.md) [monitorize o seu estado](device-profile-monitor.md).
