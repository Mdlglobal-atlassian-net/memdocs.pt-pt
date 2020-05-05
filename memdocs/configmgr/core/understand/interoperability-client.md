---
title: Cliente de interoperabilidade expandido
titleSuffix: Configuration Manager
description: Saiba utilizar o cliente de interoperabilidade alargado para suporte a longo prazo de um cliente de Gestor de Configuração estático com um site de sucursal atual.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722782"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utilize o software cliente do Gestor de Configuração para interoperabilidade prolongada com futuras versões de um site da Filial Atual

*Aplica-se a: Gestor de Configuração (ramo atual)*  

Os requisitos de negócio podem não permitir atualizar regularmente o cliente do Gestor de Configuração em alguns dispositivos. Por exemplo, você precisa seguir as políticas de gestão de mudança, ou o dispositivo é crítico de missão. Acomodar estas necessidades instalando um novo cliente para uso a longo prazo, chamado cliente de interoperabilidade alargada (EIC). Utilize a EIC apenas para dispositivos específicos que não possam ser atualizados com frequência, como quiosque ou dispositivos de ponto de venda. Continue a utilizar a [atualização automática](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) do cliente para a maioria dos seus clientes.

## <a name="how-it-works"></a>Como funciona

Normalmente, quando instala uma nova [atualização na consola](../servers/manage/install-in-console-updates.md) para O Gestor de Configuração, os clientes atualizam automaticamente o seu software de cliente para que possam utilizar essas novas funcionalidades. Com este cenário, ainda atualiza para o ramo atual que recebe as novas funcionalidades e atualizações. A maioria dos dispositivos atualiza o software cliente do Gestor de Configuração com cada atualização de versão que instala. No entanto, num subconjunto de sistemas críticos que não pretende receber atualizações de software de clientes, instala o cliente de interoperabilidade alargada. Estes clientes não instalam novo software de cliente até que você implemente explicitamente uma nova versão do software do cliente para eles.

## <a name="supported-versions"></a>Versões suportadas

A tabela seguinte lista as versões do cliente do Gestor de Configuração que são suportadas para este cenário:

| Versão | Data de disponibilidade | Data de fim do suporte |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 de março de 2019 | Não antes de 27 de março de 2021 |
| 1802<br/>5.00.8634 | 1 de maio de 2018 | Não antes de 1 de maio de 2020 |
| 1606<br/>5.00.8412 | 18 de novembro de 2016 | 1 de maio de 2019 |

> [!TIP]  
> A EIC é apoiada durante pelo menos dois anos a contar da data de lançamento. Para obter mais informações sobre as datas de lançamento, consulte as [versões atuais](../servers/manage/current-branch-versions-supported.md)do Suporte para O Gestor de Configuração .  

Planeie atualizar o cliente de interoperabilidade alargado em dispositivos que gere com a sucursal atual antes que o suporte para o cliente expire. Para tal, descarregue uma nova versão do cliente da Microsoft e, em seguida, implemente esse software de cliente atualizado para os seus dispositivos que utilizem o cliente de interoperabilidade estendido atual.

## <a name="how-to-use-the-eic"></a>Como utilizar o EIC

1. Adicione estes dispositivos a uma coleção e exclua essa recolha de atualizações automáticas de clientes. Para mais informações, consulte [Como excluir os clientes da atualização](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Obtenha uma versão suportada do `\SMSSETUP\Client` EIC a partir da pasta do sistema de instalação de atualização do Gestor de Configuração. Certifique-se de que copia todo o conteúdo da pasta.  

    > [!TIP]  
    > Para encontrar meios de Gestor de Configuração no Centro de [Serviços](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) de Licenciamento de `System Center Config`Volume (VLSC), vá ao **separador Downloads e Chaves,** procure, e, em seguida, selecione **System Center Config Mgr (ramo atual)**.

1. Instale manualmente o EIC nesses dispositivos. Para mais informações, consulte [Manualmente a instalação do cliente.](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

    > [!Important]  
    > Ao atualizar a versão 1606 clientes para a versão 1802, utilize a opção CCMSETUP **/AlwaysExcludeUpgrade:True**. Caso contrário, o cliente poderá receber a política do ponto de gestão para atualizar automaticamente antes da política de exclusão.  

## <a name="limitations"></a>Limitações

- As atualizações para o software de clientes de interoperabilidade alargada não estão disponíveis utilizando atualizações na consola. Para obter mais informações sobre como atualizar o EIC, consulte [como atualizar um cliente excluído](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- O EIC apenas suporta as seguintes características:  

  - Atualizações de software  
  - Inventário de hardware e software
  - Pacotes e programas

## <a name="next-steps"></a>Passos seguintes

[Como excluir clientes da atualização](../clients/manage/upgrade/exclude-clients-windows.md)

Para garantir que os clientes estão instalados corretamente nos dispositivos que deseja, consulte [como monitorizar os clientes](../clients/manage/monitor-clients.md).
