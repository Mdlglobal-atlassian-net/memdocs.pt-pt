---
title: Excluir atualizações de clientes para Windows
titleSuffix: Configuration Manager
description: Saiba como excluir os clientes do Windows de serem atualizados no 'Gestor de Configuração'.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715418"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Como excluir clientes da atualização no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode excluir uma coleção de clientes da instalação automática de versões de clientes atualizadas. Utilize esta exclusão para uma coleção de computadores que precisam de maior cuidado ao atualizar o cliente. Um cliente que está numa coleção excluída ignora pedidos para instalar software de cliente atualizado.

Esta exclusão aplica-se aos seguintes métodos:

- Atualização automática
- Atualização baseada em atualização de software
- Scripts de logon
- Política de grupo

> [!NOTE]
> Embora a interface de utilizador indique que os clientes não atualizam através de qualquer método, existem dois métodos que pode utilizar para anular estas definições. Utilize o impulso do cliente ou a instalação manual do cliente para anular esta configuração. Para mais informações, consulte [Como atualizar um cliente excluído.](#bkmk_override)

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a>Configurar a exclusão

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a configuração do **site,** selecionar o nó **dos Sites** e, em seguida, selecionar **definições de hierarquia** na fita.

2. Mude para o separador **De atualização** do cliente.

3. Selecione a opção de **Excluir clientes especificados da atualização**. Em seguida, selecione a **coleção Exclusão** que pretende excluir. Só é possível selecionar uma única coleção para exclusão.

4. Selecione **OK** para fechar e guardar a configuração.

![Definições para exclusão automática de upgrade](media/automatic_upgrade_exclusion.png)

Após os clientes na política de atualização de recolha excluída, não instalam automaticamente atualizações de clientes. Para mais informações, consulte [Como atualizar os clientes para computadores Windows](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Os clientes excluídos ainda descarregam e executam a Ccmsetup, mas não atualizam.

Quando remove um cliente da recolha de exclusão, não atualiza automaticamente até ao próximo ciclo de atualização automática.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a>Como atualizar um cliente excluído

Se um dispositivo for membro de uma coleção que excluiu da atualização, ainda pode atualizar o cliente utilizando um dos seguintes métodos:

- **Instalação de impulso**do cliente : Ccmsetup permite instalação push cliente porque é a sua intenção direta. Este método permite-lhe atualizar um cliente sem o retirar da coleção, ou remover toda a coleção da exclusão.

- **Instalação manual**do cliente : Atualize manualmente um cliente excluído utilizando o seguinte parâmetro de linha de comando Ccmsetup: **/IgnoreSkipUpgrade**

    Se tentar atualizar manualmente um cliente que seja membro da coleção excluída, e não utilizar este parâmetro, o cliente não atualiza. Para mais informações, consulte [como instalar os clientes do Gestor de Configuração manualmente](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>Consulte também

- [Atualizar clientes](upgrade-clients.md)

- [Como implementar clientes em computadores Windows](../../deploy/deploy-clients-to-windows-computers.md)

- [Cliente de interoperabilidade expandido](../../../understand/interoperability-client.md)
