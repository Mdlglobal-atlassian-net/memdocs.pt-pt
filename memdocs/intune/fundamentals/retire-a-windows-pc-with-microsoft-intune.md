---
title: Extinguir um PC Windows
titleSuffix: Microsoft Intune
description: Como extinguir um PC Windows gerido pelo Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5c916182-d99c-44c5-a779-3f596f261c40
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7d88b5ba8f5071821d1a9901a26bfb4a5a6fbd3
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330677"
---
# <a name="retire-a-windows-pc"></a>Extinguir um PC Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Siga os seguintes passos para extinguir computadores que está a gerir como PCs através da execução do cliente de software do Intune nos mesmos. Quando extingue um PC, este é removido da gestão do Intune. Não é possível apagar um PC a partir do Intune para restaurar as respetivas definições de fábrica originais.

1. Na [consola de administração do Microsoft Intune](https://manage.microsoft.com/), selecione **Grupos** &gt; **Todos os Dispositivos** (ou outro grupo que contenha o PC que quer extinguir).

2. Selecione os dispositivos que pretende extinguir e, em seguida, escolha **Extinguir/Limpar**.

Para inscrever novamente um PC no Intune, reinstale o cliente de software no PC com as orientações em [Instalar o cliente do PC Windows com o Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Se não conseguir ligar um PC ao Intune, é apresentada uma mensagem na área de trabalho **Dashboard**.

Quando extingue um PC:

- Este é removido da gestão e do inventário do Intune, e a licença associada ao PC é disponibilizada para reutilização. Extinguir/Limpar remove o cliente de software do Intune, mas não remove aplicações ou dados do PC. Esta extinção não efetua uma eliminação completa no PC.

- O estado do mesmo já não é apresentado na consola do Intune.

- O Intune remove o cliente de software do PC. Se o PC não estiver ligado ao serviço do Intune, o cliente de software será removido na próxima vez que for ligado.

- O Endpoint Protection do Microsoft Intune é removido do PC. Se o PC tiver outra aplicação de ponto final instalada e esta estiver desativada, essa aplicação pode ser ativada novamente quando o Endpoint Protection do Microsoft Intune for removido para garantir a proteção do seu PC.

- Todas as políticas serão removidas do PC e os valores que estavam definidos pela política serão alterados.

- O PC deixará de receber atualizações de software ou atualizações de definições de software maligno do serviço do Intune.

- Dependendo de como estiverem configurados, os PC extintos poderão continuar a receber atualizações através dos Windows Server Update Services, o Windows Update ou o Microsoft Update.

    > [!IMPORTANT]
    > Se o software de cliente tiver sido instalado com um Objeto de Política de Grupo (GPO), tem de remover o Objeto de Política de Grupo (GPO) antes de poder remover o software de cliente, para impedir que o software seja reinstalado.

    Se o cliente do Endpoint Protection não for desinstalado, leia [Resolução de problemas do Endpoint Protection](/intune/troubleshoot-endpoint-protection-in-microsoft-intune) para obter mais ajuda.

## <a name="see-also"></a>Consulte também

[Tarefas de gestão comuns de PCs Windows com o cliente de software do Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
