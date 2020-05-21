---
title: Definições de educação do Windows 10 no Microsoft Intune - Azure Microsoft Docs
description: Consulte uma lista de todas as definições de educação para dispositivos Windows 10. Utilize estas definições num perfil de configuração do dispositivo com a aplicação Take a Test, escolha como os utilizadores ou alunos se inscrevem, monitorize o ecrã durante o teste e muito mais em Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55e38ac8b5503e98df4878529ac892b55a52be47
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429611"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Configure a aplicação Take a Test em dispositivos Windows 10 usando Intune

A aplicação Take a Test permite-lhe administrar de forma segura testes online nos dispositivos Windows 10 da sua sala de aula. Para configurar a aplicação Take a Test, terá de criar um perfil de configuração do dispositivo em Intune e configurar as definições de avaliação segura. Este artigo descreve as definições que encontrará para a aplicação Take a Test. 

Depois de configurar o perfil, atribuir e implantá-lo aos seus alunos. 

[Tome uma aplicação de Teste em Intune](education-settings-configure.md) fornece mais informações sobre esta funcionalidade.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Faça um teste de definições

- Tipo de **conta:** Escolha como os utilizadores se inscrevem no teste. As opções são:
  - Conta do Azure AD
  - Conta do domínio
  - Conta local
  - Conta de hóspedes local: Disponível apenas em dispositivos com windows 10, versão 1903 e posterior.
- **Nome**do utilizador da conta : Introduza o nome de utilizador da conta utilizada com a aplicação Take a Test. Pode introduzir contas no seguinte formato:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Nome**da conta : Para configurar um tipo de conta local, insira o nome da conta utilizada com a app Take a Test. O nome da conta aparecerá como um azulejo no ecrã de entrada. Os alunos clicam no azulejo para lançar o teste.  
- **URL de avaliação**: Introduza o URL do teste que pretende que os utilizadores tomem. Para obter o URL, consulte a [documentação Do Teste .](https://docs.microsoft.com/education/windows/take-tests-in-windows-10)
- **Ligação à impressora**: **Só** permite o acesso à aplicação Take a Test a partir de dispositivos ligados a uma impressora. Esta definição também disponibiliza o botão de impressão da aplicação aos participantes. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por padrão, o SISTEMA pode permitir que os estudantes acedam à aplicação a partir de dispositivos que não estejam ligados a uma impressora.  
- **Monitorização do ecrã**: **Permitir monitores** da atividade do ecrã enquanto os utilizadores estão a fazer um teste. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir-lhe de monitorizar o ecrã durante o teste.
- **Sugestões de texto**: Escolha **Permitir** para que os participantes possam ver sugestões de texto. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode bloquear sugestões de texto enquanto os utilizadores estão a fazer um teste.

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Saiba mais sobre a [aplicação Take a Test](education-settings-configure.md).
