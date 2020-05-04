---
title: Segurança e privacidade da gestão de energia
titleSuffix: Configuration Manager
description: Obtenha informações de segurança e privacidade para gestão de energia no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715180"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Segurança e privacidade para gestão de energia em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Esta secção contém informações de segurança e privacidade para a gestão de energia no Gestor de Configuração.  

## <a name="security-best-practices-for-power-management"></a>Melhores práticas de segurança para gestão de energia  
 Não existem melhores práticas relacionadas com segurança para gestão de energia.  

## <a name="privacy-information-for-power-management"></a>Informações de privacidade para gestão de energia  
 A gestão de energia utiliza funcionalidades incorporadas no Windows para monitorizar a utilização da energia e aplicar definições de energia aos computadores durante as horas de expediente e fora de expediente. O Gestor de Configuração recolhe informações de utilização de energia a partir de computadores, que inclui dados sobre quando um utilizador está a usar um computador. Embora o Gestor de Configuração monitorize o uso de energia para uma coleção e não para cada computador, uma coleção pode conter apenas um computador. A gestão de energia não está ativada por predefinição e tem de ser configurada por um administrador.  

 As informações de utilização de energia são armazenadas na base de dados do Gestor de Configuração e não são enviadas para a Microsoft. As informações detalhadas são mentidas na base de dados por 31 dias e as informações resumidas são mantidas por 13 meses. Não pode configurar o intervalo de eliminação.  

 Antes de configurar a gestão de energia, considere os requisitos de privacidade.  
