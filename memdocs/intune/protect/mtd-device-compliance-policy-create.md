---
title: Criar uma política de conformidade de dispositivos MTD com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Crie uma política de conformidade de dispositivo do Intune que utilize os níveis de ameaça de parceiro MTD para determinar se um dispositivo móvel pode aceder a recursos da empresa.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5c9baa75474161d7ae5260522a1e28f8c05c2a3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329157"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Criar a política de conformidade de dispositivos da Defesa Contra Ameaças para Dispositivos Móveis (MTD) com o Intune

O Intune com a MTD ajuda-o a detetar ameaças e a avaliar os riscos em dispositivos móveis. Pode criar uma regra de política de conformidade de dispositivos do Intune que avalie o risco para determinar se o dispositivo está ou não em conformidade. Em seguida, pode utilizar uma política de [Acesso Condicional](create-conditional-access-intune.md) para bloquear o acesso aos serviços com base na conformidade do dispositivo.

> [!NOTE]
> Estas informações aplicam-se a todos os parceiros de Defesa Contra Ameaças para Dispositivos Móveis.

## <a name="before-you-begin"></a>Antes de começar

Como parte da configuração da MTD, na consola do parceiro MTD, criou uma política que classifica as várias ameaças como sendo de nível alto, médio e baixo. Na política de conformidade de dispositivos do Intune, precisa agora de definir o nível de Defesa Contra Ameaças para Dispositivos Móveis.

Pré-requisitos da política de conformidade de dispositivos com a MTD:

- Configurar a integração da MTD com o Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Para criar uma política de conformidade MTD do dispositivo

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **as políticas** de conformidade do **dispositivo** >  > Criar **a política**.

3. Especifique uma política de conformidade do dispositivo **Nome**, **Descrição,** selecione a **Plataforma**e, em seguida, selecione **Configurar** sob a secção **Definições.**

4. No painel **política de conformidade**, selecione **Estado de Funcionamento do Dispositivo**.

5. No painel **de saúde** do dispositivo, escolha o Nível de Ameaça Móvel da lista de drop-down para **exigir que o dispositivo esteja no nível de ameaça**do dispositivo .

   - **Seguro**: este é o nível mais seguro. O dispositivo não pode aceder aos recursos da empresa se contiver ameaças. Se forem detetadas ameaças, o dispositivo será avaliado como não conforme.

   - **Baixo**: o dispositivo está em conformidade se só estiverem presentes ameaças de nível baixo. Qualquer nível mais alto coloca o dispositivo num estado de não conforme.

   - **Médio**: o dispositivo está em conformidade se as ameaças encontradas forem de nível baixo ou médio. Se forem detetadas ameaças de nível alto, o estado do dispositivo será determinado como não conforme.

   - **Elevado**: este é o nível menos seguro. Este nível permite que todos os níveis de ameaça estejam presentes e utiliza a Defesa Contra Ameaças para Dispositivos Móveis apenas para a criação de relatórios. É necessário que os dispositivos tenham a aplicação de MTD ativada com esta definição.

6. Selecione **OK** duas vezes e, em seguida, selecione **Criar** para criar a apólice.

> [!IMPORTANT]
> Se criar políticas de Acesso Condicional para o Office 365 ou outros serviços, a avaliação da conformidade do dispositivo é avaliada e os dispositivos não conformes são impedidos de aceder a recursos corporativos até que a ameaça seja resolvida no dispositivo.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Para atribuir uma política de conformidade MTD do dispositivo

Para atribuir uma política de conformidade do dispositivo aos utilizadores:

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **as políticas**de conformidade do **dispositivo** > .

3. Selecione a política que pretende atribuir aos utilizadores e, em seguida, selecione **Atribuições**. Utilize as opções disponíveis para *incluir* e *excluir* grupos para receber esta política.  

4. Selecione Guardar para completar a atribuição. Quando guarda a atribuição, a política é implementada para os seus utilizadores selecionados e os seus dispositivos são avaliados para o cumprimento.

## <a name="next-steps"></a>Próximos passos

[Ativar a Defesa Contra Ameaças para Dispositivos Móveis no Intune](mtd-connector-enable.md)
