---
title: Sync devices com Microsoft Intune - Azure [ Microsoft Docs
description: Sincronize dispositivos registados ou geridos com o Microsoft Intune para obter as políticas e ações mais recentes. Inclui os passos para sincronizar através do portal do Azure e lista os códigos de erro que podem ser repetidos.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650a91d17223c31e02d660e47874a42731de572a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983030"
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions-with-intune"></a>Sincronizar dispositivos para obter as políticas e ações mais recentes com o Intune


A ação **Sincronizar** dispositivo força o dispositivo selecionado a registar-se imediatamente com o Intune. Quando um dispositivo dá entrada, recebe imediatamente todas as ações ou políticas pendentes que foram atribuídas ao mesmo. Esta funcionalidade pode ajudá-lo a validar imediatamente e a resolver as políticas que atribuiu, sem esperar pelo próximo check-in agendado.

## <a name="supported-platforms"></a>Plataformas suportadas

- Windows
- Windows Phone
- iOS
- macOS
- Android

## <a name="sync-a-device"></a>Sincronizar um dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 
3. Selecione **Dispositivos**  >  **Todos os dispositivos**.
4. Na lista de dispositivos que gere, selecione um dispositivo para abrir o seu painel de *visão geral* e, em seguida, selecione **Sync**.
5. Para confirmar, selecione **Sim**.

Para ver o estado da ação de sincronização, escolha as ações do **Dispositivo**  >  **de Monitorização**de Dispositivos  >  **Device actions**.

Pode encontrar frequências padrão de check-in política Intune nos [tempos](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)do ciclo Refresh .

## <a name="retryable-error-codes"></a>Códigos de erro repetíveis

Quando um administrador executa a ação do dispositivo **Sync,** as aplicações iOS/iPadOS e Android que falharam e criaram um código de erro retível ainda estão disponíveis para o dispositivo. No entanto, as aplicações que geraram um código de erro não repetível têm de aguardar sete dias antes de estarem disponíveis no dispositivo.


| Código de erro  | Descrição sugerida | Repetível |
|---|---|---|
| 2016330898 | Ocorreu um erro desconhecido. | No |
| 2016330897 | A sua ligação com intune cronometrada. Reponha a sua ligação. | Yes |
| 2016330896 | Perdeu a ligação à Internet. Reinicie a sua ligação. | Yes |
| 2016330895 | Perdeu a ligação à Internet. Reinicie a sua ligação. | Yes |
| 2016330894 | Perdeu a ligação à Internet. Reinicie a sua ligação. | Yes |
| 2016330893 | Perdeu a ligação à Internet. Reinicie a sua ligação. | Yes|
| 2016330892 | O roaming internacional está desativado. | No|
| 2016330891 | A ligação de dados celulares para este dispositivo não pode ser acedida enquanto uma chamada telefónica está sendo feita. Aguarde a conclusão da chamada. | Yes|
| 2016330890 | A rede móvel deste dispositivo. Estes dispositivos não podiam ser usados neste momento. | No|
| 2016330889 | A ligação segura falhou. Reinicie a sua ligação. | Yes|
| 2016330888 | A avaliação da fidedignidade do servidor falhou. | Não|

## <a name="next-steps"></a>Próximos passos

Pode [verificar os detalhes](device-inventory.md) do dispositivo.
 
