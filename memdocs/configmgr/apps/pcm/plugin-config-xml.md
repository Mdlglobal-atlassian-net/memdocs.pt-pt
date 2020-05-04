---
title: Configuração plug-in XML
titleSuffix: Configuration Manager
description: Referência técnica para os elementos XML do plug-in do Gestor de Conversão de Pacotes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ced1cc1347167451d4efb789b40746ff849710ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709965"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Referência técnica para a configuração plug-in do Gestor de Conversão de Pacotes XML

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

Este artigo descreve os elementos XML no ficheiro de configuração do Gestor de Configuração (Microsoft.ConfigurationManagement.exe.config) que controlam o funcionamento do plug-in do Gestor de Conversão do Pacote. Para obter mais informações sobre como utilizar este plug-in, consulte [como utilizar o plug-in do Gestor](how-to-use-plug-in.md)de Conversão de Pacotes .



## <a name="xml-configuration-elements"></a>Elementos de configuração XML

A tabela seguinte descreve os elementos XML no ficheiro de configuração do Gestor de Configuração que se relacionam com o plug-in do Gestor de Conversão do Pacote.

|Elemento  |Tipo  |Descrição  |
|---------|---------|---------|
|**PcmPlugIn**|String|O nome do script ou executável para usar como plug-in do Gestor de Conversão do Pacote.|
|**PcmPlugInTimeoutMilliseconds**|Número inteiro|O tempo máximo, em milissegundos, para aguardar o script plug-in do Gestor de Conversão do Pacote ou executável para completar o processamento de um pacote.|
|**PcmPluginExitCode**|Número inteiro|O código de saída esperado do processo de encaixe. Este valor indica sucesso. Todos os outros códigos são considerados um erro.|
|**ForçaRequisitos Extração**|Booleano|Permitir a conversão automática para utilizar os requisitos de recolha associados a uma embalagem. Isto só deve ser definido para True quando trabalhar com um plug-in do Gestor de Conversão de Pacotes que foi concebido para tomar decisões sobre quais os requisitos a utilizar.|



## <a name="sample-configuration-xml"></a>Configuração da amostra XML

Esta secção fornece um exemplo da configuração do Gestor de Conversão de Pacotes elementos XML no ficheiro de configuração do Gestor de Configuração, **Microsoft.ConfigurationManagement.exe.config**. Por predefinição, este ficheiro encontra-se no seguinte caminho:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

Na amostra, os elementos relacionados com o Gestor de Conversão de Pacotes estão dentro do seguinte elemento:`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

