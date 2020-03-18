---
title: Adicione ou configure as definições de educação no Microsoft Intune - Azure  Microsoft Docs
description: Utilize a aplicação Take a Test num perfil de configuração do dispositivo no Windows 10 e posteriormente em dispositivos no Microsoft Intune. Crie um perfil de configuração utilizando as definições de Educação e introduza um URL de aplicação de teste, escolha como os utilizadores sinuem, monitorizem o ecrã durante o teste e permitam ou previnem sugestões de texto durante o teste.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2019
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
ms.openlocfilehash: 12d04869834691167c2f31be853029c9a939a338
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333093"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Utilize a aplicação Take a Test em dispositivos Windows 10 no Microsoft Intune



Os perfis de educação em Intune são projetados para que os alunos faça um teste ou exame em dispositivos. Esta funcionalidade inclui a aplicação **Take a Test** e as definições para adicionar um URL de teste, escolher como os utilizadores finais se inscrevem no teste, e muito mais. Esta funcionalidade suporta a seguinte plataforma:

- Windows 10 e posterior

Quando o utilizador faz o sinal de entrada, a aplicação Take a Test abre automaticamente com o teste em que entrou. Nenhuma outra aplicação pode ser executada no dispositivo enquanto o teste estiver em curso. [A tomada de testes no Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) fornece mais detalhes sobre a aplicação Take a Test.

Este artigo lista os passos para criar um perfil de configuração do dispositivo no Microsoft Intune. Também inclui informações para ler e aprender sobre as definições de educação disponíveis para os seus dispositivos Windows 10.

## <a name="create-a-device-profile"></a>Criar um perfil de dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: introduza um nome descritivo para o novo perfil.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: selecione **Windows 10 e posterior**.
    - **Perfil**: Escolha **o perfil de Educação**.

4. Introduza as definições que pretende configurar:

    - [Windows 10 e posterior](education-settings-windows.md)

5. Selecione **OK** > **Criar** para guardar as alterações.

Após introduzir as suas definições e criar o perfil, este será apresentado na lista de perfis. Em seguida, [atribua este perfil a alguns grupos](device-profile-assign.md).

## <a name="next-steps"></a>Próximos passos

Consulte uma lista das definições de [educação do Windows 10](education-settings-windows.md) e respetivas descrições.

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
