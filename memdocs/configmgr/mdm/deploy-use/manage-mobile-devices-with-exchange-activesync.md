---
title: Gestão de dispositivos com o Exchange
titleSuffix: Configuration Manager
description: Gerencie dispositivos móveis com o conector Exchange Server no Gestor de Configuração.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721928"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Gestão de dispositivos com Gestor de Intercâmbio e Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Se tiver dispositivos móveis que se conectem ao Exchange Server através do protocolo ActiveSync, pode utilizar o conector do Exchange Server no Gestor de Configuração para gerir estes dispositivos. O conector trabalha com o Exchange Server ou o Exchange Online no local. Utilize a consola 'Gestor de Configuração' para configurar as funcionalidades de gestão de dispositivos móveis Exchange. Por exemplo, a limpeza remota do dispositivo e o controlo de definições para vários servidores de Intercâmbio.

![Diagrama lógico do conector do servidor de câmbio com gestor de configuração](media/configmgr-with-exchange.png)  

Quando gere dispositivos móveis com este conector, não instala o cliente do Gestor de Configuração nem matricula os dispositivos através do MDM. As funções de gestão do Exchange Server são limitadas em comparação com estas outras opções. Por exemplo, não é possível instalar software ou utilizar itens de configuração para configurar estes dispositivos. Para mais informações, consulte Escolha uma solução de gestão de [dispositivos para O Gestor de Configuração](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Políticas

Quando utiliza o conector, o Gestor de Configuração configura as definições nos dispositivos móveis. Os dispositivos não utilizam as políticas de caixa de correio 'Exchange ActiveSync'. Defina as definições que pretende utilizar nos seguintes grupos:

- **General**
- **Palavra-passe**
- **Gestão de E-mails**
- **Segurança**
- **Aplicação**

Por exemplo, no grupo **Password,** pode configurar as seguintes definições:

- Se os dispositivos móveis requerem uma senha
- O comprimento mínimo da palavra-passe
- Complexidade da palavra-passe
- Se a recuperação da palavra-passe é permitida

Quando configura pelo menos uma definição no grupo, o ConfigurManager gere todas as definições do grupo para dispositivos móveis. Se não configurar qualquer definição num grupo, o Exchange continua a gerir essas definições para os dispositivos móveis. Quaisquer políticas de caixa de correio Exchange ActiveSync que configure no Exchange Server e atribuir aos utilizadores ainda são aplicadas.

## <a name="access-rules-and-remote-actions"></a>Regras de acesso e ações remotas

Também pode configurar o conector Exchange Server para gerir as regras de acesso ao Exchange. Estas regras de acesso incluem dispositivos móveis de permitir, bloquear ou colocar em quarentena dispositivos móveis. Pode limpar remotamente os dispositivos móveis utilizando a consola 'Gestor de Configuração', e os utilizadores podem limpar remotamente os seus dispositivos móveis utilizando o catálogo da aplicação.

O dispositivo móvel de um utilizador aparece automaticamente no catálogo de aplicações quando o gere e o Exchange Server está no local. Para que o dispositivo móvel apareça no catálogo de aplicações quando utilizar o Exchange Online, configure manualmente a afinidade do dispositivo do utilizador. Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

> [!TIP]  
> Quando um dispositivo móvel é transferido para outro utilizador, antes de o novo proprietário configurar a sua conta De Troca no dispositivo, elimine o dispositivo móvel da consola 'Gestor de Configuração'.

## <a name="prerequisites"></a>Pré-requisitos

> [!IMPORTANT]  
> Antes de instalar este conector, confirme que o Gestor de Configuração suporta a sua versão de Exchange. Para mais informações, consulte [configurações suportadas - Conector de Servidor de Intercâmbio](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Permissões para configurar o conector

Precisa das seguintes permissões de segurança para configurar o conector do Exchange Server no Gestor de Configuração:

- Para adicionar, modificar e eliminar as funções do conector do Exchange Server: permissão **Modificar** para o objeto **Site** .  

- Para configurar as definições de dispositivo móvel: permissão **ModifyConnectorPolicy** para o objeto de **Site** .  

Por exemplo, a função **full administrator** incorporada inclui estas permissões necessárias.  

### <a name="permissions-to-manage-mobile-devices"></a>Permissões para gerir dispositivos móveis

Precisa das seguintes permissões de segurança para gerir dispositivos móveis:  

- Para apagar um dispositivo móvel: **Eliminar recurso** para o objeto **Coleção** .  

- Para cancelar um comando de eliminação: **Modificar recurso** para o objeto **Coleção** .  

- Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o objeto **Coleção** .  

Por exemplo, a função incorporada do Administrador de **Operações** inclui estas permissões necessárias.

Para mais informações, consulte a [configuração da administração baseada em papéis](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Instalar e configurar o conector De Troca](install-configure-exchange-connector.md)
