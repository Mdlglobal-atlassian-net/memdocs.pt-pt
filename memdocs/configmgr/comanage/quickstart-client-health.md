---
title: Saúde do cliente com cogestão
titleSuffix: Configuration Manager
description: Manter a visibilidade da saúde cliente do Gestor de Configuração a partir do Intune on Azure portal
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711197"
---
# <a name="client-health-with-co-management"></a>Saúde do cliente com cogestão

A saúde da sua rede está diretamente ligada à saúde dos dispositivos que se deslocam dentro e fora dela. Intune pode comunicar com um cliente insalubre, mesmo quando não está na sua rede. Utilize a cogestão para combinar esta funcionalidade com a capacidade do Gestor de Configuração de reportar 98% dos clientes saudáveis conhecidos. Depois pode detetar, avaliar e fornecer visibilidade a todos os clientes em tempo real. Intune também adiciona o suporte necessário para upgrades de conformidade em todos os clientes conectados.

No vídeo seguinte, o gestor de programas sénior Rob York e o gestor de marketing de produtos Locky Ainley discutem e demo saúde do cliente com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Avaliar a saúde dos clientes é uma prioridade máxima. System Center 2012 Diretor de Configuração adicionado **CCMeval**. Este utilitário é externo ao cliente do Gestor de Configuração. Fornece monitorização e reparação automática de saúde do cliente. No entanto, este relatório baseia-se num dispositivo que está fisicamente ou virtualmente na sua rede interna. A cogestão ajuda a resolver esta questão.

Com a cogestão, intune pode reportar sobre o estado de saúde do cliente. Fornece informações sobre carimbo seleto para a validade dos dados. Estas informações dizem-lhe se os seus dispositivos são saudáveis, capazes de se conectar, capazes de instalar aplicações ou podem atualizar para as construções de SO necessárias. 

Para uma visão detalhada desta funcionalidade, consulte este vídeo da sessão [What's New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) na Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando o Gestor de Configuração fornece o estado do dispositivo que o cliente está instalado, mas não está, a Intune pode fornecer mais informações sem precisar de se ligar ao cliente. A informação sobre saúde do dispositivo em Intune é fácil de entender. Se o estatuto for diferente do **Healthy,** dá recomendações e próximos passos para resolver e corrigir.

> [!Note]  
> Estão previstas as seguintes prestações para uma versão futura:
> - O Gestor de Configuração incluirá funcionalidade adicional no CCMeval  
> - Será mais fácil identificar máquinas potencialmente pouco saudáveis tanto no Gestor de Configuração como no Intune  
> - Pode agrupar os dados de saúde do cliente em Intune  



## <a name="value-proposition"></a>Proposta de valor

Com esta funcionalidade, tem agora uma fonte de dados externa com a Intune. Permite-lhe determinar os próximos passos ao resolver um vasto leque de problemas com o cliente. Agora não precisa de criar relatórios adicionais ou usar outras ferramentas para retirar os dados dos clientes.

Quando tem clientes saudáveis, tem prontamente atualizado a conformidade com o patch. Melhor conformidade com o patch significa melhor segurança.



## <a name="configure"></a>Configurar

Para começar com esta funcionalidade, use os seguintes passos:

- Atualizar dispositivos para windows 10, versão 1709 ou mais tarde  

- [Ativar a cogestão](how-to-enable.md)  
    - Não precisa mudar nenhuma carga de trabalho para Intune  

- Atualize o site e os clientes do seu Gestor de Configuração para a *versão 1806* ou posterior  


### <a name="review-configuration-manager-client-health-in-intune"></a>Rever A saúde do cliente do Gestor de Configuração em Intune

1. Assine no [portal Azure.](https://portal.azure.com/)  

2. Escolha **todos os serviços** > **Intune**. O Intune encontra-se na secção **Monitorização + Gestão**.  

3. Assim que abrir o painel **Microsoft Intune,** no menu em **ajuda e suporte,** vá para a página de Resolução de **Problemas.**  

4. Utilize a opção **Select user,** encontre o dispositivo específico na lista de **Dispositivos** e selecione-o para abrir a página do dispositivo.  

5. As informações de cogestão são mostradas na parte inferior da página do dispositivo. Estas informações incluem os seguintes campos de saúde do cliente:  
    - **Estado de agente de gestor de configuração**  
    - **Verificação do agente do último gestor de configuração a tempo**  

> [!Tip]  
> Os dispositivos intune ligam-se ao serviço de nuvem três vezes por dia, aproximadamente a cada oito horas. 
