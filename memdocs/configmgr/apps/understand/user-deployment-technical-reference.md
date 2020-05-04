---
title: Implementação de aplicativos para utilizadores de referência técnica
titleSuffix: Configuration Manager
description: Implementações de aplicações de resolução de problemas para referência técnica dos utilizadores para O Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710798"
---
# <a name="application-deployment-policy-for-users"></a>Política de Implementação de Aplicações para Utilizadores

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando uma aplicação é implementada para uma coleção de utilizadores, a política de implementação é criada apenas para implementações necessárias. Para implementações disponíveis, a política é criada quando o utilizador tenta instalar a aplicação a partir do Centro de Software. Este artigo explicará o processo de implantação para implementações necessárias, bem como disponíveis.

> [!TIP]
> Todas as informações necessárias para rever os registos do cliente podem ser obtidas executando a consulta SQL referenciada na secção [Antes de iniciar.](app-deployment-technical-reference.md#before-you-begin)

## <a name="required-deployments"></a>Implementações necessárias

A política de implementação de aplicações necessária para uma recolha de utilizadores é direcionada a todos os utilizadores da recolha quando a implementação for criada. O processamento do lado do cliente para estas implementações é semelhante a uma implementação necessária para uma coleção de Dispositivos. A ativação de implantação ocorre no tempo disponível definido, e a execução ocorre no prazo definido. Para mais informações, consulte [a Implementação de Aplicações para Recolha de Dispositivos](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Implementações disponíveis

As aplicações que são implementadas para uma recolha de utilizadores como disponíveis comportam-se de forma diferente. Esta alteração de comportamento permite ao Administrador disponibilizar aplicações aos utilizadores sem causar a contestação de recursos à política. Quando um utilizador lança o Centro de Software, uma lista de aplicações disponíveis para o utilizador é consultada a partir do Ponto de Gestão em tempo real. Este pedido é `CMUserService_WindowsAuth` feito para o diretório virtual no Ponto de Gestão e pode ser visto no **SCClient_[UserName].log** no cliente.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Quando o Ponto de Gestão recebe este pedido, consulta a lista `usp_GetApplicationPropertyValuesFiltered` de aplicações disponíveis ao utilizador executando o procedimento armazenado. Esta atividade pode ser rastreada no **UserService.log** no Ponto de Gestão.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

O Software Center recebe a lista e exibe as aplicações que o utilizador pode instalar. Quando o utilizador clica na aplicação, são consultadas informações adicionais sobre a aplicação a partir do Ponto de Gestão, que envolve a execução de procedimentos armazenados como usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp, etc.

A implementação é ativada quando o utilizador seleciona a aplicação e clica no botão **Instalar,** e é criado um DCM Agent Job para avaliar a aplicação. Se a aplicação for aplicável, outro DCM Agent Job é criado para descarregar e fazer cumprir a aplicação. Esta atividade pode ser rastreada no **Registo DCMAgent.no** cliente.

## <a name="next-steps"></a>Passos Seguintes

- [Compreender componentes do cliente de implementação de aplicações](client-components-technical-reference.md)
