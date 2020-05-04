---
title: Atualizar e extinguir aplicações
titleSuffix: Configuration Manager
description: Reveja, substitui ou desinstale aplicações implantadas utilizando o 'Gestor de Configuração'.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710532"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>Atualizações e aplicações de aposentadoria com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


É provável que eventualmente queira fazer alterações a uma aplicação, desinstalar uma aplicação ou substituir uma aplicação já implantada por uma nova aplicação. O Gestor de Configuração dá-lhe estas capacidades, para ajudá-lo a atualizar e reformar aplicações:  

- **Rever as candidaturas.** Quando faz alterações a uma aplicação ou tipo de implementação, o Gestor de Configuração mantém um histórico das alterações. Pode reverter a aplicação para uma revisão anterior em qualquer altura. Também pode ver as suas propriedades, restaurar uma revisão prévia de uma aplicação ou apagar uma revisão antiga.  

  Para mais informações, consulte revisões da [Aplicação](revise-and-supersede-applications.md#application-revisions).  

- **Aplicações de supersede.** Pode atualizar ou substituir as aplicações existentes utilizando uma relação de supersedência. Quando substitui uma aplicação, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação supersed. Além disso, pode definir se deve atualizar ou desinstalar a aplicação supersedantes da instalação da aplicação de superseding.  

  Para mais informações, consulte [a supersedência da Aplicação.](revise-and-supersede-applications.md#application-supersedence)  

- **Desinstalar aplicações**. O Gestor de Configuração facilita a desinstalação de uma aplicação. Isto pode ser realizado silenciosamente, sem qualquer intervenção da aplicação ou utilizador do dispositivo.  

  Para mais informações, consulte [Desinstalar aplicações](uninstall-applications.md).  
