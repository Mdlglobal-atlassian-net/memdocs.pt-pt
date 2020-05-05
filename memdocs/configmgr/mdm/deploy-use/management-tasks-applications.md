---
title: Gerir aplicativos para MDM no local
titleSuffix: Configuration Manager
description: Gerir aplicações para gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721914"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Gerir aplicativos para MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando gere dispositivos com a gestão de dispositivos móveis do Gestor de Configuração (MDM), pode gerir os seguintes tipos de aplicações:

- Pacote de aplicação do Windows Phone (ficheiro *.xap)
- Pacote de aplicação do Windows Phone (na Loja Windows Phone)
- Windows Installer através de MDM
- Aplicação Web

Para obter informações mais gerais sobre a gestão de aplicações do Gestor de Configuração e tipos de implementação, consulte [as tarefas de Gestão para aplicações do Gestor de Configuração.](../../apps/deploy-use/management-tasks-applications.md)

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Criar aplicação Windows Phone

Uma aplicação De Configuração Manager tem um ou mais tipos de implementação. O tipo de implementação inclui os ficheiros de instalação e as informações necessárias para implementar software num dispositivo. Um tipo de implementação também tem regras que especificam quando e como o software é implementado.

Para que os passos gerais criem uma aplicação e tipos de implementação, consulte [criar uma aplicação](../../apps/deploy-use/create-applications.md#bkmk_create).

O Gestor de Configuração suporta os seguintes tipos de ficheiros de aplicações para dispositivos móveis Windows:

|Tipo de Dispositivo|Tipos de ficheiro suportados|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Implemente aplicações do Windows Phone conforme **disponível** ou **necessário.** Utilize também implementações para desinstalar aplicações.

## <a name="deploy-and-monitor-apps"></a>Implementar e monitorizar aplicações

Implemente e monitorize aplicações para dispositivos móveis em 'Configuração Manager' da mesma forma que faz para outros dispositivos, como desktops e servidores. Para obter mais informações, veja os artigos seguintes:

- [Implementar aplicações](../../apps/deploy-use/deploy-applications.md)
- [Monitorizar aplicações](../../apps/deploy-use/monitor-applications-from-the-console.md)

Reveja as seguintes limitações específicas aos dispositivos móveis:

- Os dispositivos matriculados no MDM não suportam implementações simuladas, experiência do utilizador ou definições de agendamento.

- Não adicione mais de 100 locais a uma única aplicação. Esta ação impede que a aplicação se instale no dispositivo.

## <a name="next-step"></a>Passo seguinte

Para efetuar alterações, desinstalar ou substituir uma aplicação implementada por uma nova aplicação, gerenciá-la da mesma forma que qualquer aplicação no 'Gestor de Configuração'. Para mais informações, consulte [As aplicações De Atualização e de reforma.](../../apps/deploy-use/update-and-retire-applications.md)
