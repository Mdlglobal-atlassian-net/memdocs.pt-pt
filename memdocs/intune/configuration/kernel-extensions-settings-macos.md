---
title: definições de extensão de kernel macOS no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Adicione, configure ou crie configurações em dispositivos macOS para utilizar extensões de kernel. Além disso, permitir que os utilizadores anulem as extensões aprovadas, permitam todas as extensões de um identificador de equipa ou permitam extensões ou aplicações específicas no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
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
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359284"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>definições do dispositivo macOS para configurar e utilizar extensões de kernel em Intune

Este artigo lista e descreve as diferentes definições de extensão de kernel que pode controlar em dispositivos macOS. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para adicionar e gerir extensões de kernel nos seus dispositivos.

Para saber mais sobre extensões de kernel em Intune, e quaisquer pré-requisitos, consulte [adicionar extensões de kernel macOS](kernel-extensions-overview-macos.md).

Estas definições são adicionadas a um perfil de configuração do dispositivo no Intune e, em seguida, atribuídas ou implementadas nos dispositivos macOS.

## <a name="before-you-begin"></a>Antes de começar

[Criar um perfil](kernel-extensions-overview-macos.md)de configuração de extensões de kernel do dispositivo .

> [!NOTE]
> Estas definições aplicam-se a diferentes tipos de matrículas. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="kernel-extensions"></a>Extensões kernel

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Definições aplicam-se a: Utilizador aprovado, inscrição automática do dispositivo

- **Permitir sobreposições**do utilizador : **Permitir que** os utilizadores aprovem extensões de kernel não incluídas no perfil de configuração. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores permitam extensões não incluídas no perfil de configuração. Ou seja, só são permitidas extensões incluídas no perfil de configuração.

  Consulte o [carregamento de extensão de kernel aprovado pelo utilizador](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (abre o site da Apple) para obter mais informações sobre esta funcionalidade.

- **Identificadores de equipa permitidos**: Utilize esta definição para permitir uma ou muitas identificações de equipa. Quaisquer extensões de kernel assinadas com as identificações da equipa em que entram são permitidas e confiáveis. Por outras palavras, utilize esta opção para permitir todas as extensões de kernel dentro do mesmo ID da equipa, que pode ser um desenvolvedor ou parceiro específico.

  **Adicione** um identificador de equipa de extensões de kernel válidas e assinadas que pretende carregar. Pode adicionar vários identificadores de equipa. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, introduza `ABCDE12345`.

  Depois de adicionar um identificador de equipa, também pode ser eliminado.

  [Localizar o seu ID de equipa](https://help.apple.com/developer-account/#/dev55c3c710c) (abre o site da Apple) tem mais informações.

- **Extensões de kernel permitidas**: Utilize esta definição para permitir extensões específicas do núcleo. Apenas as extensões de kernel que introduz são permitidas ou confiáveis.

  **Adicione** o identificador de pacote e o identificador de equipa de uma extensão de kernel que pretende carregar. Para extensões de kernel legado não assinadas, utilize um identificador de equipa vazio. Pode adicionar várias extensões de kernel. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, insira `com.contoso.appname.macos` para o **Bundle ID**, e `ABCDE12345` para **identificador de equipa**.

  > [!TIP]
  > Para obter o Bundle ID de uma extensão de kernel (Kext) num dispositivo macOS, pode:
  >
  > 1. No Terminal, corra `kextstat | grep -v com.apple`, e note a saída. Instale o software ou o Kext que deseja. Executar `kextstat | grep -v com.apple` novamente, e procurar mudanças.
  >
  >    No Terminal, `kextstat` lista todas as extensões de kernel no SISTEMA. 
  >
  > 2. No dispositivo, abra o ficheiro Information Property List (Info.plist) para um Kext. O pacote de identificação é mostrado. Cada Kext tem um ficheiro Info.plist armazenado no seu interior.

> [!NOTE]
> Não é preciso adicionar identificadores de equipa e extensões de kernel. Pode configurar um ou outro.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
