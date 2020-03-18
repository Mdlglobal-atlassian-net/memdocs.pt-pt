---
title: Ativar aplicações Win32 em dispositivos de modo S
titleSuffix: Microsoft Intune
description: Saiba como ativar as aplicações Win32 em dispositivos de modo S utilizando o Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/08/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c52261051000e7af1580f8213e5d348857a128c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325677"
---
# <a name="enable-win32-apps-on-s-mode-devices"></a>Ativar aplicações Win32 em dispositivos de modo S

[O modo Windows 10 S](https://docs.microsoft.com/windows/deployment/s-mode) é um sistema operativo bloqueado que só executa aplicações da Store. Por predefinição, os dispositivos de modo Windows S não permitem a instalação e execução das aplicações Win32. Estes dispositivos incluem uma única política de *base Win 10S*, que impede o dispositivo de modo S de executar quaisquer aplicações Win32 nele. No entanto, ao criar e utilizar uma política suplementar de **modo S** em Intune, pode instalar e executar aplicações Win32 em dispositivos geridos pelo modo Windows 10 S. Ao utilizar as ferramentas PowerShell powerShell do [Microsoft Defender Application Control (WDAC),](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) pode criar uma ou mais políticas suplementares para o modo Windows S. Deve assinar as políticas suplementares com o Serviço de Assinatura de Guarda de [Dispositivos (DGSS)](https://go.microsoft.com/fwlink/?linkid=2095629) ou com [signTool.exe](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/signing-policies-with-signtool) e, em seguida, carregar e distribuir as políticas via Intune. Como alternativa, pode assinar as políticas suplementares com um certificado de codificação da sua organização, no entanto o método preferido é utilizar a DGSS. No caso de utilizar o certificado de codificação da sua organização, o certificado de raiz que o certificado de codificação se encontra, deve estar presente no dispositivo.

Ao atribuir a política suplementar do modo S em Intune, permite que o dispositivo exceda a política de modo S existente do dispositivo, que permite o catálogo de aplicações assinado correspondente. A política define uma lista de aplicações permitidas (o catálogo de aplicações) que podem ser usadas no dispositivo de modo S.

> [!NOTE]
> As aplicações Win32 nos dispositivos de modo S só são suportadas no Windows 10 November 2019 Update (build 18363) ou versões posteriores.

<!-- Add WDAC tooling diagram  -->

As etapas para permitir que as aplicações Win32 sejam executadas num dispositivo Windows 10 no modo S são as seguintes:

1. Ative os dispositivos de modo S através do Intune como parte do processo de inscrição do Windows 10 S.
2. Crie uma política suplementar para permitir aplicações Win32:
   - Pode utilizar ferramentas de Controlo de [Aplicações do Microsoft Defender (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) para criar uma política suplementar. A política de base Id dentro da política deve corresponder ao Id da política de base de modo S (que é codificado duramente no cliente). Além disso, certifique-se de que a versão política é superior à versão anterior.
   - Usa a DGSS para assinar a sua política suplementar. Para mais informações, consulte a política de [integridade do código de sinal com a assinatura da Guarda de Dispositivos](https://docs.microsoft.com/microsoft-store/sign-code-integrity-policy-with-device-guard-signing).
   - Faça o upload da política suplementar assinada para Intune, criando uma política suplementar de modo Windows 10 S (ver abaixo).
3. Permite catálogos de aplicações Win32 através do Intune:
   - Cria ficheiros de catálogo (1 para cada aplicação) e assina-os utilizando a DGSS ou outra infraestrutura de certificados.
   - Embala o catálogo assinado no ficheiro *.intunewin* utilizando a Ferramenta de Preparação de [Conteúdo do Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730). Não existem restrições de nomeação ao criar um ficheiro de catálogo utilizando a Ferramenta de Preparação de [Conteúdo microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730). Ao gerar o ficheiro *.intunewin* a partir da pasta de origem especificada e do ficheiro de configuração, pode fornecer uma pasta separada contendo apenas ficheiros de catálogo utilizando a opção -uma cmdline. Para mais informações, consulte a gestão da [aplicação Win32 - Prepare o conteúdo da aplicação Win32 para upload](apps-win32-app-management.md#prepare-the-win32-app-content-for-upload).
   - Intune aplica o catálogo de aplicações assinado para instalar a aplicação Win32 no dispositivo de modo S utilizando a extensão de [gestão Intune](intune-management-extension.md).

> [!NOTE]
> Os pacotes de `.appx` e `.appx` de  e  no modo Windows 10 S serão suportados através da assinatura da Microsoft Store for Business (MSFB).
>
> **A política suplementar** do modo S para aplicações deve ser entregue através da Extensão de Gestão Intune.
>
> As políticas de modo S são aplicadas ao nível do dispositivo. Várias políticas direcionadas serão fundidas no dispositivo. A política de fusão será aplicada no dispositivo.

Para criar uma política suplementar de modo Windows 10 S, utilize os seguintes passos:

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **Políticas suplementares do modo S** > Criar a **política**.
3. Antes de adicionar o **ficheiro Política,** deve criá-lo e assiná-lo. Para obter mais informações, consulte:
    - [Crie uma política WDAC usando ferramentas PowerShell e converta-a num formato binário](https://go.microsoft.com/fwlink/?linkid=2095387)
    - [Assine usando o Serviço](https://go.microsoft.com/fwlink/?linkid=2095629) de Assinatura de Guarda de Dispositivo **(recomendado)**

4. Na página Basics, adicione os **seguintes valores:**

    | Valor | Descrição |
    |--------------|------------------------------------------------|
    | Arquivo de política | O ficheiro que contém a política do WDAC. |
    | Nome | O nome desta apólice. |
    | Descrição | [Opcional] A descrição desta política. |

5. Clique **em Seguir: Etiquetas**de âmbito .<br>
   Na página **scope tags** pode configurar opcionalmente as etiquetas de âmbito para determinar quem pode ver a política da aplicação em Intune. Para obter mais informações sobre etiquetas de âmbito, consulte [Utilize o controlo de acesso baseado em papéis e as etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

6. Clique **em seguir: Atribuições**.<br>
   A página **De Missões** permite-lhe atribuir a apólice a utilizadores e dispositivos. É importante notar que pode atribuir uma apólice a um dispositivo, quer o dispositivo seja ou não gerido pela Intune.
7. Clique **em Seguir: Rever + criar** para rever os valores introduzidos para o perfil.
8. Quando terminar, clique em **Criar** a política suplementar do modo S em Intune.

Uma vez criada a política, irá vê-la adicionada à lista de políticas suplementares do modo S em Intune. Uma vez atribuída a apólice, a política é implementada para os dispositivos. Note que deve implantar a app no mesmo grupo de segurança que a política suplementar. Pode começar a direcionar e atribuir aplicações a esses dispositivos. Isto permitirá que os utilizadores finais instalem e executem as aplicações nos dispositivos de modo S.

## <a name="removal-of-s-mode-policy"></a>Remoção da política de modo S

Atualmente, para remover a política suplementar do modo S do dispositivo, deve atribuir e implementar uma política vazia para substituir a política suplementar do modo S existente.

## <a name="policy-reporting"></a>Relatórios de Políticas

A política suplementar do modo S, que é aplicada ao nível do dispositivo, só tem relatórios de nível de dispositivo. O relatório de nível do dispositivo está disponível para condições de sucesso e erro.

Valores de reporte que são mostrados na consola Intune para s mode reporting polices:
- **Sucesso**: A política suplementar do modo S está em vigor.
- **Desconhecido**: O estado da política suplementar do modo S não é conhecido.
- **TokenError**: A política suplementar do modo S está estruturalmente bem, mas há um erro em autorizar o símbolo.
- **NotAuthorizedByToken**: O símbolo não autoriza esta política suplementar do modo S.
- **PolicyNotFound**: A política suplementar do modo S não é encontrada.

## <a name="next-steps"></a>Próximos passos

- Para mais informações, consulte [as aplicações Win32 no modo s](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/lob-win32-apps-on-s).
- Para obter mais informações sobre como adicionar aplicações ao Intune, veja [Adicionar aplicações ao Microsoft Intune](apps-add.md).
- Para mais informações sobre as aplicações Win32, consulte a gestão de [aplicações Intune Win32.](apps-win32-app-management.md)
