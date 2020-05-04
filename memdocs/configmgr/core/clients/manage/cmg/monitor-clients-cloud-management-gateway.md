---
title: Monitorizar gateway de gestão de nuvem
titleSuffix: Configuration Manager
description: Monitorize os clientes e tráfego de rede através do gateway de gestão de nuvem (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714228"
---
# <a name="monitor-cloud-management-gateway"></a>Monitorizar gateway de gestão de nuvem

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de o portal de gestão de nuvem (CMG) estar em execução e os clientes estarem a ligar-se através dele, pode monitorizar os clientes e o tráfego de rede para garantir que sabe como o serviço está a funcionar.


## <a name="monitor-clients"></a>Monitorizar clientes

Os clientes ligados através da CMG aparecem na consola do Gestor de Configuração da mesma forma que os clientes no local. Para mais informações, consulte [como monitorizar os clientes.](../monitor-clients.md)


## <a name="monitor-traffic-in-the-console"></a>Monitorizar o tráfego na consola

Monitorize o tráfego no CMG utilizando a consola 'Gestor de Configuração':

1. Vá ao espaço de trabalho da **Administração,** expanda os **Serviços cloud**e selecione o nó Gateway de Gestão de **Nuvem.**  

2. Selecione o CMG no painel da lista.  

3. Veja as informações de tráfego no painel de detalhes para o ponto de ligação CMG e as funções do sistema do site a que se conecta. Estas estatísticas mostram que os pedidos do cliente entram nestas funções. Os pedidos incluem política, localização, registo, conteúdo, inventário e notificações de clientes.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de trânsito de saída

Os alertas de tráfego de saída ajudam-no a saber quando o tráfego da rede se aproxima de um limiar de 14 dias. Quando criar o CMG, pode configurar alertas de trânsito. Se faltasse a essa parte, ainda pode configurar os alertas depois de o serviço estar em funcionamento. Ajuste as definições de alerta a qualquer momento.

1. Vá ao espaço de trabalho da **Administração,** expanda os **Serviços cloud**e selecione o nó Gateway de Gestão de **Nuvem.**  

2. Selecione o CMG no painel da lista e, em seguida, selecione **Propriedades** na fita.  

3. Vá ao separador **Alertas** para ativar o limiar e alertas. Especifique o limiar de dados de 14 dias em gigabytes (GB). Especifique também a percentagem limiar para elevar os diferentes níveis de alerta.  

4. Quando tiver terminado, selecione **OK**.  


## <a name="monitor-logs"></a>Monitor de registos

O CMG gera entradas em vários ficheiros de registo. Para mais informações, consulte os [registos do Gestor](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)de Configuração .


## <a name="cloud-management-dashboard"></a>Painel de gestão de nuvem

<!--1358461-->
A partir da versão 1806, o painel de controlo da nuvem proporciona uma vista centralizada para o uso de CMG. Quando o site está a bordo dos [serviços do Azure](../../../servers/deploy/configure/azure-services-wizard.md) para gestão de nuvem, também exibe dados sobre utilizadores e dispositivos na nuvem.  

A seguinte imagem é uma parte do painel de gestão de nuvens mostrando dois dos azulejos disponíveis:  
![Painel de instrumentos de gestão de nuvem azulejos CMG tráfego e clientes online atuais](media/1358461-cmg-dashboard.png)

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Selecione o nó **de Cloud Management** e veja os azulejos do painel de instrumentos.  


## <a name="connection-analyzer"></a>Analisador de ligação

A partir da versão 1806, utilize o analisador de ligação CMG para verificação em tempo real para ajudar na resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através do ponto de ligação CMG a quaisquer pontos de gestão que permitam o tráfego cmg.

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **os Serviços cloud** e selecionar o nó de gateway de **gestão cloud.**  

2. Selecione a instância CMG alvo e, em seguida, selecione o analisador de **ligação** na fita.  

3. Na janela analisador de ligação CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Utilizador da AD Azure**: utilize esta opção para simular a comunicação da mesma forma que uma identidade de utilizador baseada na nuvem assinada num dispositivo Windows 10 com a AD Azure. Clique **em Iniciar sessão** para introduzir de forma segura as credenciais para esta conta de utilizador da AD Azure.  

     2. **Certificado de cliente:** utilize esta opção para simular a comunicação da mesma forma que um cliente do Gestor de Configuração com um certificado de [autenticação do cliente.](certificates-for-cloud-management-gateway.md#bkmk_clientauth)  

4. Selecione **Iniciar** a análise. A janela do analisador exibe os resultados. Selecione uma entrada para ver mais detalhes no campo Descrição.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a>Pare cmg quando exceder o limiar

<!--3735092-->
A partir da versão 1902, o Gestor de Configuração pode agora parar um serviço CMG quando a transferência total de dados ultrapassar o seu limite. Utilize [alertas](#set-up-outbound-traffic-alerts) para desencadear notificações quando o uso atingir níveis de aviso ou de crítico. Para ajudar a reduzir quaisquer custos inesperados do Azure devido a um pico de utilização, esta opção desliga o serviço de cloud.

> [!Important]  
> Mesmo que o serviço não esteja em funcionamento, ainda há custos associados ao serviço de nuvem. Parar o serviço não elimina todos os custos associados do Azure. Para remover todos os custos para o serviço de nuvem, [remova o CMG](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Quando o serviço CMG é interrompido, os clientes baseados na Internet não podem comunicar com o Gestor de Configuração.  

A transferência total de dados (egress) inclui dados do serviço de nuvem e da conta de armazenamento. Estes dados provêm dos seguintes fluxos:

- CMG para cliente  
- CMG para o site, incluindo ficheiros de registo CMG  
- Se ativar a CMG para conteúdos, conta de armazenamento para cliente  

Para obter mais informações sobre estes fluxos de dados, consulte [as portas CMG e o fluxo de dados](plan-cloud-management-gateway.md#ports-and-data-flow).

O limiar de alerta de armazenamento é separado. Este alerta monitoriza a capacidade da sua instância de armazenamento Azure.

Ao selecionar a instância CMG no nó Gateway de **Gestão** de Nuvem na consola, pode ver a transferência total de dados no painel de detalhes.

O Gestor de Configuração verifica o valor limite a cada seis minutos. Se houver um aumento repentino de utilização, o Gestor de Configuração pode demorar até seis minutos a detetar que excedeu o limiar e, em seguida, parar o serviço.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Processo para parar o serviço de nuvem quando excede o limiar

1. [Instale alertas de trânsito de saída.](#set-up-outbound-traffic-alerts)  

2. No separador **Alertas** da janela de propriedades CMG, ative a opção de **parar este serviço quando o limiar crítico for ultrapassado**.  

Para testar esta funcionalidade, reduza temporariamente um dos seguintes valores:  

- **Limiar de 14 dias para transferência de dados de saída (GB)**. O valor predefinido é `10000`.  

- **Percentagem de limiar para elevar o alerta crítico.** O valor predefinido é `90`.  
