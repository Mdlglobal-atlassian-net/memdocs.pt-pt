---
title: Como os utilizadores matriculam dispositivos
titleSuffix: Configuration Manager
description: Compreenda como os utilizadores matriculam dispositivos com gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722334"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Como os utilizadores matriculam dispositivos com MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração no local a gestão de dispositivos móveis (MDM), os utilizadores podem inscrever os seus dispositivos. Há dois pré-requisitos:

- Com as definições do cliente, concede ao utilizador permissão para se inscrever.

- Instala o certificado de raiz fidedigno necessário no dispositivo.

Para obter mais informações sobre como configurar a inscrição, consulte [Configurar a inscrição](../get-started/set-up-device-enrollment-on-premises-mdm.md)do dispositivo para o MDM no local .

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Inscreva o Windows 10

1. Num computador Windows 10, aceda a **Definições**.

1. Selecione **Contas,** e, em seguida, selecione **O trabalho de acesso ou escola**.

1. Selecione **Ligar,** introduza o nome principal do utilizador (UPN) e selecione **Continuar**. A UPN pode ser a mesma que jdoe@contoso.como seu endereço de e-mail, por exemplo, .

1. Introduza o nome de domínio totalmente qualificado (FQDN) do ponto de procuração de inscrição e selecione **Continuar**.

1. Insira a sua palavra-passe e selecione **Iniciar sessão**.

1. O Windows não precisa de se lembrar da informação de entrada para esta ação, por isso selecione **Skip**.

Após um curto período de tempo, o dispositivo matricula-se no Gestor de Configuração.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Matricular o Windows 10 Mobile

1. Num dispositivo Windows 10 Mobile, aceda a **Definições**.

1. Selecione **Contas,** e, em seguida, selecione Acesso ao **trabalho**.

1. Selecione **Ligar**.

1. Insira a sua UPN e a FQDN do ponto de procuração de inscrição. Em seguida, selecione **Ligar**.

1. No ecrã seguinte, introduza a sua UPN e a sua palavra-passe e, em seguida, selecione **Iniciar sessão**.

Após um curto período de tempo, o dispositivo matricula-se no Gestor de Configuração. Selecione **Done** (Concluído).

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Verificar a inscrição

Utilize a consola 'Gestor de Configuração' para verificar se os dispositivos estão matriculados com sucesso. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione **Dispositivos**. Navegue ou procure o dispositivo inscrito na lista de dispositivos.
