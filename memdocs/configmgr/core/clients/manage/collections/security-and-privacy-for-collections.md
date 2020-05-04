---
title: Segurança e privacidade de coleções
titleSuffix: Configuration Manager
description: Obtenha as melhores práticas de segurança e privacidade em coleções em 'Gestor de Configuração'.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714494"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Segurança e privacidade para coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém boas práticas de segurança e informações de privacidade para coleções em 'Gestor de Configuração'.  

 Não existem informações de privacidade especificamente para coleções no Gestor de Configuração. As coleções são contentores de recursos, tais como utilizadores e dispositivos. A adesão à recolha depende frequentemente da informação que o Gestor de Configuração recolhe durante o funcionamento padrão. Por exemplo, através da utilização de informações de recursos que tenham sido recolhidas pela deteção ou inventário, uma coleção pode ser configurada para conter os dispositivos que cumprem critérios específicos. As coleções também podem basear-se nas informações de estado atuais para operações de gestão de clientes, tais como implementação de software e verificação de compatibilidade. Além destas coleções baseadas em consultas, os utilizadores administrativos também podem adicionar recursos a coleções.  

 Para obter mais informações sobre coleções, consulte [Introdução a coleções.](../../../../core/clients/manage/collections/introduction-to-collections.md) Para obter mais informações sobre quaisquer boas práticas de segurança e informações de privacidade para operações do Gestor de Configuração que possam ser usadas para configurar a adesão à recolha, consulte [as melhores práticas de segurança e informações de privacidade para O Gestor de Configuração.](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md)  

## <a name="security-best-practices-for-collections"></a>Melhores Práticas de Segurança para Coleções  
 Utilize a melhor prática de segurança seguinte para coleções.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exportar ou importar uma coleção utilizando um ficheiro no formato MOF (Managed Object Format) guardada numa localização de rede, proteja a localização e o canal de rede.|Restringe quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da coleção exportados. Utilize IPsec para encriptar os dados na rede para evitar a divulgação de informações.|  

### <a name="security-issues-for-collections"></a>Problemas de Segurança para Coleções  
 As coleções têm os seguintes problemas de segurança:  

-   Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais.  

     As variáveis de coleção podem ser utilizadas quando implementar um sistema operativo.  
