---
title: Referência de configuração
titleSuffix: Configuration Manager
description: Reveja esta referência para ajudá-lo a preparar-se para instalar um site ou hierarquia do Gestor de Configuração.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718071"
---
# <a name="reference-for-configuration-manager-setup"></a>Referência para Configuração do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Configuração Manager Configuração fornece links para vários tópicos que são detalhados nas seguintes secções. As informações aqui apresentadas podem ajudá-lo a preparar-se para instalar um site ou hierarquia do Gestor de Configuração, e ajudar a prepará-lo para algumas das decisões que deve tomar durante a instalação.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a>Antes de começar  
Antes de instalar novos sites do Gestor de Configuração, certifique-se de que reviu as seguintes informações, o que pode ajudar a definir o palco para um design de implementação bem sucedido:  

-   [Noções básicas do Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Plano para infraestrutura de Gestor de Configuração](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Prepare-se para instalar sites do Gestor de Configuração](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a>Avaliar a prontidão do servidor  
Antes de iniciar a instalação de um novo site, certifique-se de que o servidor do site e os servidores do sistema de site remoto que planeia utilizar para o site (por exemplo, o servidor que acolhe a base de dados do site) cumprem todas as configurações pré-requisitos. Estes tópicos na biblioteca de documentação podem ajudar:  

-   [Configurações suportadas do Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Verificador de Pré-requisitos](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clientes de sistemas operativos adicionais  
Pode descarregar o software do cliente para O Gestor de Configuração do Microsoft Download Center para os seguintes sistemas operativos:  

- macOS (Apple)
- UNIX
- Linux

Utilize os seguintes links para descarregar clientes para a versão do Gestor de Configuração que utiliza:  

- [Microsoft Endpoint Configuration Manager - macOS Client (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Clientes do Microsoft Configuration Manager para sistemas operativos adicionais](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Níveis e definições de dados de utilização  
Quando instala o seu primeiro site de Configuração, o Gestor de Configuração instala e configura automaticamente uma nova função do sistema de site, o ponto de ligação ao **serviço,** no servidor do site. O ponto de ligação ao serviço tem estas definições predefinidas:  

-   **Modo online** (um modo offline também está disponível)  
-   **Nível de** recolha de dados melhorado (dois outros níveis de recolha de dados, Básico e Completo, também estão disponíveis)  

Quando a função do sistema de pontos de ligação de serviço está on-line, a Microsoft pode recolher automaticamente informações de diagnóstico e utilização através da Internet. As informações recolhidas ajudam-nos a:  

-   Identificar e resolver problemas  
-   Melhorar os nossos produtos e serviços  
-   Identificar as atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager utilizada  

### <a name="levels-of-data-collection"></a>Níveis de recolha de dados  
A recolha de dados inclui estes três níveis:

-   **O básico** inclui dados sobre configuração e atualização, como o número de sites e quais as funcionalidades do Gestor de Configuração. Não é transmitida nenhuma informação pessoalmente identificável.  

-   **O enhanced** inclui os dados na definição de nível Básico, além de transmitir dados sobre a hierarquia, como cada funcionalidade é usada (frequência e duração) e informações de diagnóstico melhoradas como o estado de memória do seu servidor quando ocorre um sistema ou falha de aplicação. Não são transmitidos dados pessoalmente identificáveis.  

-   **O completo** inclui os dados nas definições de nível Básico e Melhorado, e também envia informações avançadas de diagnóstico, como ficheiros do sistema e instantâneos de memória. Esta opção pode incluir informações pessoalmente identificáveis, mas não usaremos essa informação para identificá-lo ou contactá-lo, ou para direcionar a publicidade para si.  

Para obter mais informações, incluindo a divulgação dos detalhes recolhidos por cada nível, consulte diagnósticos e dados de [utilização para O Gestor](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)de Configuração .  

Para ver a Declaração de Privacidade do [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527)Gestor de Configuração on-line, vá para .
