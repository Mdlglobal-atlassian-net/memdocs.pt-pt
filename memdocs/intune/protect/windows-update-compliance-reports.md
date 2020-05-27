---
title: Utilize relatórios de conformidade de atualização para atualizações do Windows no Microsoft Intune
titleSuffix: Microsoft Intune
description: Utilize a conformidade da atualização OMS para visualizar os dados do relatório para as Atualizações do Windows que implementa com o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4ef3a4c2ba539cc507ef413a4648b42e246b11d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990919"
---
# <a name="intune-compliance-reports-for-updates"></a>Intune relatórios de conformidade para atualizações

Quando utilizar o Intune para implementar a atualização do Windows para dispositivos Windows 10, veja detalhes sobre a conformidade da atualização utilizando o Intune ou uma solução gratuita chamada *'Actualização'.* A Atualização Compliance faz parte da Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Utilizar Intune

Para rever um relatório de política sobre o estado de implementação dos anéis de atualização do Windows 10 que configura:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione o estado da atualização do software de visão geral dos **dispositivos**  >  **Overview**  >  **Software update status**. Poderá ver informações gerais sobre o estado de qualquer cadência de atualizações que tenha atribuído.

3. Para ver detalhes adicionais, selecione **Monitor**. Em seguida, abaixo das **atualizações do Software**, selecione o estado de implementação do **anel de atualização Per** e escolha o anel de implementação para rever.

   Na secção **Monitorizar**, selecione um dos seguintes relatórios para ver informações mais detalhadas sobre a cadência de atualização:

   - **Estado do dispositivo**- Isto mostrará o estado de configuração do dispositivo, para mais detalhes ver [Dispositivo de ActualizaçãoConfiguraçãoStatus]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Estado do utilizador**- Isto mostrará o nome do utilizador, o estado e a data do último relatório, para mais detalhes ver [Lista de DispositivoSConfiguraçõesUserStatuses](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Estado da atualização do utilizador final**- Isto mostrará o estado de atualização do dispositivo Windows, para mais detalhes ver [windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Utilizar conformidade da atualização

Pode monitorizar os lançamentos da atualização do Windows 10 utilizando a Conformidade da [Atualização](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor). Atualização A conformidade é oferecida através do portal Azure e está disponível gratuitamente para dispositivos que cumpram os seus [pré-requisitos.](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites)  

Quando utiliza esta solução, implementa um ID comercial em qualquer um dos seus dispositivos geridos pelo Intune do Windows 10 para os quais pretende reportar a conformidade da atualização.  

Em Intune, utiliza as definições OMA-URI de uma política personalizada para configurar o ID comercial. Consulte [as definições personalizadas para dispositivos Windows 10 no Intune](../configuration/custom-settings-windows-10.md).

O caminho OMA-URI (sensível a casos sensíveis ao caso) para configurar o ID comercial é: *./Fornecedor/MSFT/DMClient/Provider/MS DM Server/CommercialID*

Por exemplo, pode utilizar os seguintes valores na **Definição Adicionar ou editar OMA-URI**:

- **Nome da Definição**: ID Comercial do Windows Analytics
- **Definição descrição**: Configurar id comercial para soluções Windows Analytics
- **OMA-URI** (sensível a casos): *./Fornecedor/MSFT/DMClient/Provider/MS DM Server/CommercialID*
- **Tipo de Dados:** cadeia
- **Valor**: \< Utilize o GUIA mostrado no separador Telemetria Windows no seu espaço de trabalho OMS>

> [!NOTE]
> Para obter mais informações sobre o servidor de DM MS, veja [Fornecedor de serviço de configuração (CSP) do DMClient]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).

## <a name="next-steps"></a>Passos seguintes

[Gerir atualizações de software no Intune](windows-update-for-business-configure.md)
