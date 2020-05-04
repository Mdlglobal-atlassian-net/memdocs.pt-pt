---
title: Pré-requisitos da gestão de energia
titleSuffix: Configuration Manager
description: Obtenha os pré-requisitos para a gestão de energia no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715187"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Pré-requisitos para a gestão de energia no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A gestão de energia no Gestor de Configuração tem dependências e dependências externas dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas ao Gestor de Configuração para a utilização da gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Os computadores cliente devem ter capacidade para suportar os estados de energia necessários|Para utilizar todas as funcionalidades de gestão de energia, os computadores cliente devem ser capazes de suportar as ações do modo de suspensão, hibernação, reativação da suspensão e reativação da hibernação. Pode utilizar o relatório **Funções de Energia** para determinar se os computadores podem suportar estas ações. Para mais informações, consulte o [relatório Power Capabilities](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) no tópico [Como monitorizar e planear a gestão de energia.](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 A tabela seguinte lista as dependências dentro do Gestor de Configuração para a utilização da gestão de energia.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|A gestão de energia deve ser ativada antes de criar e monitorizar os esquemas de energia.|Para obter informações sobre como ativar e configurar a gestão de energia, consulte a configuração da [gestão de energia.](../../../../core/clients/manage/power/configuring-power-management.md)|  
|Ponto do Reporting Services|Deve configurar um ponto do sistema de reporte antes de poder visualizar relatórios de gestão de energia. Para mais informações, consulte [Introdução a relatórios.](../../../servers/manage/introduction-to-reporting.md)|  
