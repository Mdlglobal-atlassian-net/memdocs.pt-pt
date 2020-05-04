---
title: Descarregue as definições da Microsoft
titleSuffix: Configuration Manager
description: Saiba como ativar o download das definições de malware Endpoint Protection a partir de Microsoft Updates for Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715691"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Ativar definições de malware endpoint protection para descarregar a partir de Microsoft Updates

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando selecionar para descarregar atualizações de definição a partir do Microsoft Update, os clientes verificarão o site da Microsoft Update no intervalo definido na secção de **atualizações** de Segurança Intelligence da caixa de diálogo de política antimalware.

 Este método pode ser útil quando o cliente não tem conectividade com o site do Gestor de Configuração ou quando pretende que os utilizadores possam iniciar atualizações de definição.

> [!IMPORTANT]
> - Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.
> - A secção de **atualizações** de Definição foi renomeada para **atualizações de Inteligência** de Segurança a partir da versão 1902 do Gestor de Configuração.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Utilizar o Centro Microsoft de Proteção Contra Software Maligno para Transferir Definições
 Pode configurar os clientes para transferirem atualizações de definições a partir do Centro Microsoft de Proteção Contra Software Maligno. Esta opção é utilizada pelos clientes endpoint Protection para descarregar atualizações de definição se não tiverem sido capazes de descarregar atualizações de outra fonte. Este método de atualização pode ser útil se houver algum problema com a sua infraestrutura de Gestor de Configuração que impede a entrega de atualizações.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.
> 
> 
> [!div class="button"]
> [Próximo passo >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [>de volta](endpoint-configure-alerts.md)
