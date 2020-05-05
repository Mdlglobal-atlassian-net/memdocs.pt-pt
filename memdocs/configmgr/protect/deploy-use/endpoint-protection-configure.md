---
title: Configurar o Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar o Gestor de Configuração para atualizar e distribuir definições de malware para o Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720885"
---
# <a name="configure-endpoint-protection"></a>Configurar o Endpoint Protection

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de poder utilizar a Endpoint Protection para gerir a segurança e malware nos computadores clientes do Gestor de Configuração, tem de executar os passos de configuração detalhados neste artigo.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como Configurar o Endpoint Protection no Configuration Manager  
 Endpoint Protection in Configuration Manager tem dependências e dependências externas no produto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Passos para configurar proteção de ponto final no gestor de configuração  
 Utilize a tabela seguinte para obter os passos, detalhes e mais informações sobre como configurar o Endpoint Protection.  

> [!IMPORTANT]  
>  Se gere a proteção de pontofinal para computadores Windows 10, então tem de configurar o 'Configur'se de Configurar O Gestor de Configuração para atualizar e distribuir definições de malware para o Windows Defender. O Windows Defender está incluído no Windows 10, mas o SCEPInstall ainda tem de ser instalado e as definições personalizadas do cliente para a Proteção de Pontos Finais **(Passo 5** abaixo) ainda são necessárias. </br> </br>
> A partir do 'Configuração Manager' 1802, os dispositivos do Windows 10 não necessitam de instalar o agente de proteção de pontofinal (SCEPInstall). Se já estiver instalado nos dispositivos do Windows 10, o Gestor de Configuração não o removerá. Os administradores podem remover o agente de proteção de ponto final nos dispositivos do Windows 10 que estão a executar pelo menos a versão cliente de 1802. O SCEPInstall.exe pode ainda estar presente em C:\Windows\ccmsetup em algumas máquinas, mas não deve ser descarregado em novas instalações de clientes. As configurações personalizadas do cliente para a Proteção de**Pontofinal (Passo 5** abaixo) ainda são necessárias. <!--503654-->

|Passos|Detalhes|  
|-----------|-------------|  
|**Passo 1:** Criar uma função de sistema de site de [ponto de proteção de pontos finais](endpoint-protection-site-role.md)|A função de sistema de sites de ponto do Endpoint Protection tem de ser instalada antes de poder utilizar o Endpoint Protection. Tem de ser instalada apenas num servidor do sistema de sites e tem de ser instalada na parte superior da hierarquia num site de administração central ou num site primário autónomo. |  
|**Passo 2:** [Configurar alertas para proteção de pontos finais](endpoint-configure-alerts.md)|Os alertas informam o administrador quando ocorreram eventos específicos, tal como uma infeção de software maligno. Os alertas são apresentados no nó **Alertas** da área de trabalho **Monitorização** ou, opcionalmente, podem ser enviados por e-mail para utilizadores especificados. |  
|**Passo 3:** Configure as fontes de atualização de [definição para clientes de proteção de pontofinal](endpoint-definition-updates.md)|A Proteção do Ponto Final pode ser configurada para utilizar várias fontes para descarregar atualizações de definição. |  
|**Passo 4:** [Configure a política antimalware padrão e crie políticas antimalware personalizadas](endpoint-antimalware-policies.md)|A política padrão antimalware é aplicada quando o cliente Endpoint Protection é instalado. As políticas personalizadas que tiver implementado são aplicadas por predefinição num período de 60 minutos após implementar o cliente. Certifique-se de que configuraas políticas antimalware antes de implementar o cliente Endpoint Protection. |  
|**Passo 5:** [Configure as definições personalizadas do cliente para a Proteção do Ponto Final](endpoint-protection-configure-client.md)|Utilize as definições personalizadas do cliente para configurar as definições de Proteção de Pontofinal para coleções de computadores na sua hierarquia.<br /><br /> Nota: Não configure as definições padrão do cliente de Proteção de Pontofinal, a menos que tenha a certeza de que pretende que estas definições sejam aplicadas a todos os computadores da sua hierarquia. |  
