---
title: Plano no local MDM
titleSuffix: Configuration Manager
description: Plano para gestão de dispositivos móveis no local para gerir dispositivos móveis no Gestor de Configuração
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721851"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Plano para MDM no local em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Existem várias áreas-chave para rever quando planeia implementar no local a gestão de dispositivos móveis (MDM) no Gestor de Configuração:

- Dispositivos suportados e versões DE SO
- Funções do sistema de sites necessárias
- Comunicação segura
- Inscrição de dispositivos

> [!IMPORTANT]
> Embora o site ou qualquer dispositivo móvel não se conectem ao Microsoft Intune, a sua organização ainda necessita de licenças Intune para utilizar esta funcionalidade. Para mais informações, consulte o [licenciamento Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/licenses).

Considere os seguintes requisitos antes de preparar a infraestrutura do Gestor de Configuração para lidar com o MDM no local.

## <a name="supported-devices"></a><a name="bkmk_devices"></a>Dispositivos suportados  

O atual ramo do Gestor de Configuração suporta a inscrição na gestão de dispositivos móveis no local para dispositivos que executam o Windows 10. Estes tipos de dispositivos incluem principalmente portáteis, IoT e Surface Hub. Para mais informações e a lista de edições específicas, consulte [versões De SO suportadas para clientes e dispositivos.](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Funções do sistema do site

No local, o MDM requer pelo menos uma das seguintes funções do sistema do site:

- **Ponto proxy de registo** para suportar pedidos de inscrição.

- **Ponto de inscrição** para suportar a inscrição de dispositivos.

- **Ponto de gestão de dispositivos** para entrega de políticas. Esta função é uma variação do ponto de gestão, mas permite a gestão de dispositivos móveis.

- **Ponto de distribuição** para a entrega de conteúdo.

Dependendo das necessidades da sua organização, pode instalar estas funções no servidor único ou separadamente em diferentes servidores.

> [!NOTE]
> É necessário configurar cada função utilizada para o MDM no local como um ponto final HTTPS para comunicar com dispositivos fidedignos. Para obter mais informações, veja [Comunicações fidedignas necessárias](#bkmk_trustedComs).

Para obter informações mais gerais, consulte [plan para servidores e funções](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)do sistema de site .

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Comunicações fidedignas

No local, o MDM requer que ative as funções do sistema do site para comunicações HTTPS. Dependendo das suas necessidades, pode utilizar a autoridade de certificados da sua organização (CA) para estabelecer as ligações fidedignas entre servidores e dispositivos. Também pode usar um AC disponível publicamente para ser a autoridade de confiança. De qualquer forma, é necessário configurar os seguintes certificados:

- Um certificado de **servidor web** no IIS nos servidores que hospedam as funções de sistema de site necessárias. Se um servidor apresentar várias funções do sistema do site, só precisa de um certificado para esse servidor. Se cada função estiver num servidor separado, cada servidor necessita de um certificado separado.

- O **certificado de raiz fidedigno** da AC que emite os certificados do servidor web. Instale este certificado de raiz em todos os dispositivos que necessitem de se ligar às funções do sistema do site.

Para obter mais informações, consulte [A configuração de certificados para comunicações fidedignas no MDM](../get-started/set-up-certificates-on-premises-mdm.md)no local .

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Inscrição do dispositivo

Para permitir a inscrição do dispositivo para o MDM no local:

- Conceder aos utilizadores permissão para se inscreverem através das definições do cliente

- Configure dispositivos para comunicações fidedignas com os servidores do sistema do site que acolhem as funções necessárias

Como alternativa à inscrição iniciada pelo utilizador, pode configurar um pacote de inscrição a granel. Esta embalagem permite que o dispositivo se inscreva sem a intervenção do utilizador. Entregue a embalagem no dispositivo antes de ser disponibilizada para utilização ou depois de passar pelo seu processo OOBE.

Para mais informações, consulte [Configurar a inscrição](../get-started/set-up-device-enrollment-on-premises-mdm.md)do dispositivo para o MDM no local .

## <a name="next-step"></a>Passo seguinte

> [!div class="nextstepaction"]
> [Instalar funções do sistema de sites](../get-started/install-site-system-roles-for-on-premises-mdm.md)
