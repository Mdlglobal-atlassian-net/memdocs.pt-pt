---
title: Declaração de privacidade para cmdlets
titleSuffix: Configuration Manager
description: Saiba como a Microsoft recolhe e utiliza dados relacionados com o Gestor de Configuração
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714648"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Declaração de privacidade da biblioteca cmdlet manager de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Esta declaração de privacidade cobre as funcionalidades para a Biblioteca Cmdlet do Gestor de Configuração.  

## <a name="usage-data"></a>Dados de utilização  

#### <a name="what-this-feature-does"></a>O que esta funcionalidade faz

A biblioteca cmdlet do Gestor de Configuração permite-lhe gerir uma hierarquia do Gestor de Configuração utilizando cmdlets e scripts windows PowerShell. A biblioteca cmdlet recolhe informações sobre como usar os cmdlets na biblioteca para identificar tendências e padrões de utilização. A biblioteca cmdlet também recolhe os tipos e números de erros que recebe quando utiliza os cmdlets.  

#### <a name="information-collected-processed-or-transmitted"></a>Informação recolhida, processada ou transmitida
   
Os dados de utilização recolhidos incluem o arranque, paragem e terminação de cmdlets, funcionamento de cmdlets depreciados e métricas de atividade para operações do Provedor de SMS que estão relacionadas com os cmdlets. Esta informação não é pessoalmente identificável. As informações de erro recolhidas incluem erros que os cmdlets devolvem e erros de erro para erros de exceção. Alguns relatórios de detalhes de erro podem inadvertidamente incluir identificadores individuais, como um número de série para um dispositivo que está ligado ao seu computador. Os filtros da biblioteca cmdlet e a anonimizam a informação que está nos relatórios de erro para remover identificadores individuais antes da transmissão para a Microsoft.  

#### <a name="use-of-information"></a>Utilização de informação
   
A Microsoft utiliza estas informações para melhorar a qualidade, segurança e integridade dos produtos e serviços que oferecem.  

#### <a name="choicecontrol"></a>Escolha/controlo   

Esta função de dados de utilização é ativada por padrão. A biblioteca cmdlet do Gestor de Configuração tem duas chaves de registo que controlam esta funcionalidade.  

 Para optar por totalmente, detete estes dois valores-chave do registo. Destinam-se a cada um dos fornecedores de Rastreio de Eventos para Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opta por não utilizar dados para o fornecedor de unidades)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opta por não utilizar dados para os cmdlets)  

  As alterações nas definições de dados de utilização são específicas do computador onde são feitas.  


## <a name="next-steps"></a>Passos seguintes

[Configuração Manager Cmdlet Library documentação](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
