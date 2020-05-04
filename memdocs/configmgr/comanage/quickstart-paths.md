---
title: Caminhos para a cogestão
titleSuffix: Configuration Manager
description: Compreenda os pré-requisitos para as duas formas primárias de configurar a cogestão.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a670660bcf7b3f5cb8209aaf6d0b59eb0f343e4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711491"
---
# <a name="paths-to-co-management"></a>Caminhos para a cogestão

Há duas maneiras primárias de criar a cogestão. É importante entender os pré-requisitos para cada caminho. Cada um deles requer alguma combinação de Azure Ative Directory (Azure AD), Configuration Manager, Microsoft Intune e Windows 10. 

1. [Inscrição automática de dispositivos geridos pelo Gestor de Configuração em Intune](#bkmk_path1)  
2. [Bootstrap o cliente do Gestor de Configuração com o fornecimento moderno](#bkmk_path2)  

![Diagrama de caminhos de cogestão](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>Caminho 1: Inscrição automática de clientes existentes

Tomar este caminho pode fazer com que os seus dispositivos geridos pelo Gestor de Configuração se inscrevam rapidamente no Intune. A gestão destes dispositivos do Gestor de Configuração não é diferente antes de ativar a cogestão. Agora recebes todos os benefícios baseados na nuvem. Este caminho é transparente para os seus utilizadores.

Eis o que precisa para o preparar:
- Azure AD Híbrido
    - Uma das [seguintes opções de identidade híbrida Azure AD:](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)  
       - [Sincronização](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) de hash password com [insígnia single seamless (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Autenticação pass-through](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) com [insígnia single sign-on (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [SSO Federado (com Serviços da Federação de Diretório Ativo (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Licença Azure AD Premium
    - Configure híbrido Azure AD-join (escolha uma opção):
        - Para domínios geridos
        - Para domínios federados
- Definição de agente de cliente para a adesão híbrida azure
- Configure a inscrição automática de dispositivos para Intune
- Atribuir licenças de utilizador intune
- Ativar a cogestão no Gestor de Configuração

Para um tutorial neste caminho, consulte [Tutorial: Ativar a cogestão para os clientes existentes do Gestor de Configuração.](tutorial-co-manage-clients.md)



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a>Caminho 2: Bootstrap com fornecimento moderno

Eis o que precisa para o preparar:

1. [Configuração melhorada HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Crie os serviços de nuvem em Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Configure o ponto de gestão e os clientes para usar o gateway de gestão de nuvem](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Use Intune para implementar o cliente de Gestor de Configuração](how-to-prepare-Win10.md)  

> [!Note]  
> Um tutorial para este caminho está para breve.

