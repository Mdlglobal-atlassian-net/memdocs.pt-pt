---
title: definições de extensão macOS no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Adicione, configure ou crie configurações em dispositivos macOS para utilizar extensões do sistema e extensões de kernel. Além disso, permitir que os utilizadores anulem as extensões aprovadas, permitam todas as extensões de um identificador de equipa ou permitam extensões ou aplicações específicas no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
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
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429517"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>definições do dispositivo macOS para configurar e utilizar extensões de kernel e sistema em Intune

> [!NOTE]
> As extensões de kernel macOS estão a ser substituídas por extensões do sistema. Para mais informações, consulte [Dica de Suporte: Utilizar extensões do sistema em vez de extensões de kernel para macOS Catalina 10.15 em Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Este artigo lista e descreve as diferentes definições de extensão de kernel e sistema que pode controlar em dispositivos macOS. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para adicionar e gerir extensões nos seus dispositivos.

Para saber mais sobre extensões em Intune, e quaisquer pré-requisitos, consulte [adicionar extensões macOS](kernel-extensions-overview-macos.md).

Estas definições são adicionadas a um perfil de configuração do dispositivo no Intune e, em seguida, atribuídas ou implementadas nos dispositivos macOS.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de configuração de [extensões macOS](kernel-extensions-overview-macos.md).

> [!NOTE]
> Estas definições aplicam-se a diferentes tipos de matrículas. Para obter mais informações sobre os diferentes tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="kernel-extensions"></a>Extensões kernel

Esta funcionalidade aplica-se a:

- macOS 10.13.2 e mais recente
- É necessária a inscrição do dispositivo aprovado pelo utilizador 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo aprovado pelo utilizador, inscrição automática do dispositivo

- **Permitir sobreposições**do utilizador : **Sim** permite que os utilizadores aprovem extensões de kernel não incluídas no perfil de configuração. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode impedir que os utilizadores permitam extensões não incluídas no perfil de configuração. Ou seja, só são permitidas extensões incluídas no perfil de configuração.

  Para obter mais informações sobre esta funcionalidade, consulte o [carregamento de extensão de kernel aprovado pelo utilizador](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (abre o site da Apple).

- **Identificadores de equipa permitidos**: Utilize esta definição para permitir uma ou muitas identificações de equipa. Quaisquer extensões de kernel assinadas com as identificações da equipa em que entram são permitidas e confiáveis. Por outras palavras, utilize esta opção para permitir todas as extensões de kernel dentro do mesmo ID da equipa, que pode ser um desenvolvedor ou parceiro específico.

  **Adicione** um identificador de equipa de extensões de kernel válidas e assinadas para carregar. Pode adicionar vários identificadores de equipa. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, introduza `ABCDE12345`.

  Depois de adicionar um identificador de equipa, também pode ser eliminado.

  [Localizar o seu ID de equipa](https://help.apple.com/developer-account/#/dev55c3c710c) (abre o site da Apple) tem mais informações.

- **Extensões de kernel permitidas**: Utilize esta definição para permitir extensões específicas do núcleo. Apenas as extensões de kernel que introduz são permitidas ou confiáveis.

  **Adicione** o identificador de pacote e o identificador de equipa de uma extensão de kernel para carregar. Para extensões de kernel legado não assinadas, utilize um identificador de equipa vazio. Pode adicionar várias extensões de kernel. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, introduza `com.contoso.appname.macos` o **Id do Bundle,** e `ABCDE12345` para **identificador de equipa**.

  > [!TIP]
  > Para obter o Bundle ID de uma extensão de kernel (Kext) num dispositivo macOS, pode:
  >
  > 1. No Terminal, `kextstat | grep -v com.apple` corra, e note a saída. Instale o software ou o Kext que deseja. Corra `kextstat | grep -v com.apple` de novo, e procure mudanças.
  >
  >    No Terminal, `kextstat` lista todas as extensões de kernel no SISTEMA. 
  >
  > 2. No dispositivo, abra o ficheiro Information Property List (Info.plist) para um Kext. O pacote de identificação é mostrado. Cada Kext tem um ficheiro Info.plist armazenado no seu interior.

> [!NOTE]
> Não é preciso adicionar identificadores de equipa e extensões de kernel. Pode configurar um ou outro.

## <a name="system-extensions"></a>Extensões do sistema

Esta funcionalidade aplica-se a:

- macOS 10.15 e mais recente
- É necessária a inscrição do dispositivo aprovado pelo utilizador

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Definições aplicam-se a: Inscrição do dispositivo aprovado pelo utilizador, inscrição automática do dispositivo

- Bloqueio de **sobreposições**do utilizador : **Sim** impede os utilizadores de aprovarem extensões do sistema que não estão na lista permitida. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir que os utilizadores aprovem extensões desconhecidas não incluídas no perfil de configuração. Ou seja, são permitidas extensões não incluídas no perfil de configuração.

- **Identificadores de equipa permitidos:** Utilize esta definição para permitir uma ou muitas identificações de equipa. Quaisquer extensões de sistema assinadas com as identificações da equipa em que entram são sempre permitidas e confiáveis. Por outras palavras, utilize esta opção para permitir todas as extensões do sistema dentro do mesmo ID da equipa, que pode ser um desenvolvedor ou parceiro específico.

  **Adicione** um **identificador** de equipa de extensões de sistema válidas e assinadas para carregar. Pode adicionar vários identificadores de equipa. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, introduza `ABCDE12345`.

  Depois de adicionar um identificador de equipa, também pode ser eliminado.

  [Localizar o seu ID de equipa](https://help.apple.com/developer-account/#/dev55c3c710c) (abre o site da Apple) tem mais informações.

- **Extensões permitidas do sistema**: Utilize esta definição para permitir sempre extensões específicas do sistema. Apenas as extensões do sistema que introduz são permitidas ou confiáveis.

  **Adicione** o **identificador de pacote** e **identificador** de equipa de uma extensão do sistema para carregar. Para extensões do sistema legado não assinadas, utilize um identificador de equipa vazio. Pode adicionar várias extensões do sistema. O identificador de equipa deve ser alfanumérico (letras e números) e ter 10 caracteres. Por exemplo, introduza `com.contoso.appname.macos` o **Id do Bundle,** e `ABCDE12345` para **identificador de equipa**.

- **Tipos de extensão de sistema permitidos**: Introduza o ID da equipa e os tipos de extensão do sistema para permitir esse ID da equipa:
  - **Identificador**de equipa : Introduza o ID de equipa de outra extensão do sistema que pretende permitir tipos de extensão específicos. Ou, introduza um ID de equipa adicionado às **extensões permitidas do sistema**.
  - **Tipos de extensão de sistema permitidos**: Selecione os tipos de extensão do sistema para permitir cada ID da equipa. As opções são:
    - Selecionar tudo
    - Extensões do condutor
    - Extensões de rede
    - Extensões de segurança de endpoint

    Para obter mais informações sobre estes tipos de extensão, consulte [extensões](https://developer.apple.com/system-extensions/) do sistema (abre o site da Apple).

    Pode adicionar um ID de equipa da lista de **extensões permitidas** do sistema e permitir um tipo de extensão específico. Se a extensão for um tipo que não é permitido, então a extensão pode não ser executada.

    Para permitir todos os tipos de extensão para um ID de equipa, adicione o ID da equipa à lista de **extensões permitidas** do sistema. Não adicione o ID da equipa à lista de tipos de **extensão do sistema permitido.** Por outras palavras, se um ID de equipa estiver na lista de **extensões permitidas** do sistema, e não na lista de tipos de extensão do **sistema permitido,** então todos os tipos de extensão são permitidos para esse ID da equipa.

> [!NOTE]
> Adicionar o mesmo ID de equipa para **extensões permitidas** do sistema e **identificadores de equipa permitidos** pode resultar num erro e a falha do perfil. Não adicione o mesmo identificador de equipa exato a ambas as definições. 

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
