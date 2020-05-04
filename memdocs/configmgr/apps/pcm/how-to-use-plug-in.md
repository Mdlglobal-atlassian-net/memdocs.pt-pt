---
title: Como utilizar o plug-in de conversão
titleSuffix: Configuration Manager
description: Utilize o plug-in do Gestor de Conversão de Pacotes para personalizar os processos de análise e conversão.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709881"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Como utilizar o plug-in do Gestor de Conversão de Pacotes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

O plug-in do Gestor de Conversão de Pacotes ajuda-o a personalizar os processos de análise e conversão. Para utilizar o plug-in do Gestor de Conversão de Pacotes, escreva um ficheiro executável ou script que execute operações personalizadas. Em seguida, editar o ficheiro de configuração, Microsoft.ConfigurationManagement.exe.config, para chamar o executável ou script. As línguas mais comuns usadas para escrever o script são VBScript ou PowerShell.

O plug-in do Gestor de Conversão de Pacotes funciona uma vez por cada embalagem. Se analisar ou converter vários pacotes de uma só vez, o plug-in do Gestor de Conversão do Pacote funciona cada vez.

> [!NOTE]  
> Para obter mais informações sobre os elementos do Gestor de Conversão de Pacotes no ficheiro de configuração do Gestor de Configuração, consulte [referência técnica para a configuração plug-in](plugin-config-xml.md)do Gestor de Conversão de Pacotes XML .



## <a name="default-process"></a>Processo predefinido

Por predefinição, o Gestor de Conversão de Pacotes faz as seguintes ações:

1.  Leia um pacote de Gestor de Configuração.  

2.  Crie uma aplicação a partir do pacote e adicione atributos padrão.  

3.  Analise a aplicação e determine um estado de prontidão do pacote.  

4.  Tome uma das seguintes ações, dependendo da operação do Gestor de Conversão de Pacotes:  

    - **Análise**: Mostrar o estado de prontidão do pacote na consola Do Gestor de Configuração.  

    - **Converter**: Escreva a aplicação na base de dados do Gestor de Configuração.  


## <a name="plug-in-based-process"></a>Processo plug-in 

Quando utiliza o plug-in, o Gestor de Conversão de Pacotes faz as seguintes ações:

1.  Leia um pacote de Gestor de Configuração.  

2.  Crie uma aplicação a partir do pacote e adicione atributos padrão.  

3.  Converta a aplicação para XML. Em seguida, guarde o ficheiro para o disco.  

4.  Executar o script plug-in para modificar a aplicação XML. Para mais informações, consulte [referência técnica para a configuração plug-in do Gestor de Conversão de Pacotes XML](plugin-config-xml.md).  

5.  Converta a aplicação XML numa aplicação de Gestor de Configuração.  

6.  Analise a aplicação e determine um estado de prontidão do pacote.  

7.  Tome uma das seguintes ações, dependendo da operação do Gestor de Conversão de Pacotes:  

    - **Análise**: Mostrar o estado de prontidão do pacote na consola Do Gestor de Configuração.  

    - **Converter**: Escreva a aplicação na base de dados do Gestor de Configuração.  



## <a name="see-also"></a>Consulte também

[Referência técnica para a configuração plug-in do Gestor de Conversão de Pacotes XML](plugin-config-xml.md)
