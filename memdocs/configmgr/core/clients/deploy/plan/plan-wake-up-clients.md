---
title: Acordar clientes
titleSuffix: Configuration Manager
description: Planeie como acordar os clientes no Gestor de Configuração usando Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713262"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Planeie como acordar clientes no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 O Gestor de Configuração suporta pacotes tradicionais de despertar para acordar computadores no modo de sono quando pretende instalar software necessário, como atualizações de software e aplicações.

> [!NOTE]
> Este artigo descreve como uma versão mais antiga de Wake on LAN funciona. Esta funcionalidade ainda existe na versão 1810 do Configuration Manager, que também inclui uma versão mais recente do Wake on LAN. Ambas as versões de Wake on LAN podem, e em muitos casos, serão ativadas simultaneamente. Para obter mais informações sobre como funciona a nova versão de Wake on LAN a partir de 1810 e permitindo qualquer ou ambas as versões, consulte [Como configurar Wake on LAN](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Como acordar clientes no Gestor de Configuração

 O Gestor de Configuração suporta pacotes tradicionais de despertar para acordar computadores no modo de sono quando pretende instalar software necessário, como atualizações de software e aplicações.  

Pode complementar o método tradicional do pacote de despertar utilizando as definições do cliente proxy de despertar. O wake-up proxy usa um protocolo peer-to-peer e computadores eleitos para verificar se outros computadores na subnet estão acordados, e para acordá-los se necessário. Quando o site está configurado para Wake On LAN e os clientes estão configurados para procuração de despertar, o processo funciona da seguinte forma:  

1. Os computadores com o cliente do Gestor de Configuração instalados e que não estão a dormir na sub-rede verificam se outros computadores da subnet estão acordados. Fazem este controlo enviando um comando de ping TCP/IP a cada cinco segundos.  

2. Se não houver resposta de outros computadores, presume-se que estão a dormir. Os computadores acordados tornam-se *gestores de computador* esportiva para a sub-rede.  

    Porque é possível que um computador não responda por uma razão que não esteja a dormir (por exemplo, está desligado, removido da rede, ou a configuração do cliente proxy wake-up já não é aplicada), os computadores são enviados um pacote de despertar todos os dias às 14:00. hora local. Os computadores que não responderem já não serão assumidos como estando a dormir e não serão acordados por procuração de despertar.  

    Para suportar o alerta proxy, pelo menos três computadores devem estar acordados para cada sub-rede. Para atingir este requisito, três computadores são escolhidos não determinicamente para serem *computadores guardiões* para a sub-rede. Este estado significa que permanecem acordados, apesar de qualquer política de poder configurada para dormir ou hibernar após um período de inatividade. Os computadores guardian honram comandos de paragem ou reinício, por exemplo, como resultado de tarefas de manutenção. Se esta ação acontecer, os restantes computadores guardiães acordam outro computador na subnet para que a sub-rede continue a ter três computadores tutores.  

3. Os computadores gerentes pedem ao interruptor de rede para redirecionar o tráfego de rede para os computadores adormecidos para si mesmos.  

    A redirecção é conseguida pelo computador gestor que transmite uma moldura Ethernet que utiliza o endereço MAC do computador adormecido como endereço de origem. Este comportamento faz com que o interruptor de rede se comporte como se o computador adormecido tivesse mudado para a mesma porta em que o computador gestor está. O computador gerente também envia pacotes ARP para os computadores adormecidos para manter a entrada fresca na cache ARP. O computador gestor também responde aos pedidos da ARP em nome do computador adormecido e responde com o endereço MAC do computador adormecido.  

   > [!WARNING]  
   >  Durante este processo, o mapeamento IP-to-MAC para o computador adormecido permanece o mesmo. Wake-up proxy funciona informando o interruptor de rede que um adaptador de rede diferente está usando a porta que foi registada por outro adaptador de rede. No entanto, este comportamento é conhecido como um retalho MAC e é incomum para o funcionamento padrão da rede. Algumas ferramentas de monitorização da rede procuram este comportamento e podem assumir que algo está errado. Consequentemente, estas ferramentas de monitorização podem gerar alertas ou desligar portas quando utilizar procuração de despertar.  
   >   
   >  Não utilize procuração de despertar se as suas ferramentas e serviços de monitorização de rede não permitirem flaps MAC.  

4. Quando um computador gerente vê um novo pedido de ligação TCP para um computador adormecido e o pedido é para uma porta que o computador adormecido estava a ouvir antes de adormecer, o computador gerente envia um pacote de despertar para o computador adormecido, e depois para de redirecionar o tráfego para este computador.  

5. O computador adormecido recebe o pacote de despertar e acorda. O computador de envio tenta automaticamente a ligação e, desta vez, o computador está acordado e pode responder.  

   O representante de despertar tem os seguintes pré-requisitos e limitações:  

> [!IMPORTANT]  
>  Se tiver uma equipa separada responsável pela infraestrutura de rede e serviços de rede, notifique e inclua esta equipa durante o seu período de avaliação e teste. Por exemplo, numa rede que utiliza o controlo de acesso à rede 802.1X, o wake-up proxy não funcionará e pode perturbar o serviço de rede. Além disso, o wake-up proxy poderia fazer com que algumas ferramentas de monitorização da rede gerassem alertas quando as ferramentas detetam o tráfego para despertar outros computadores.  

-   Todos os sistemas operativos Windows listados como clientes suportados em [sistemas operativos suportados para clientes e dispositivos](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são suportados para Wake On LAN.  

-   Os sistemas operativos dos hóspedes que funcionam numa máquina virtual não são suportados.  

-   Os clientes devem ser ativados para o proxy de despertar utilizando as definições do cliente. Embora a operação de procuração de despertar não dependa do inventário de hardware, os clientes não reportam a instalação do serviço de procuração de despertar, a menos que estejam habilitados para o inventário de hardware e submetidos pelo menos um inventário de hardware.  

-   Os adaptadores de rede (e possivelmente o BIOS) devem ser ativados e configurados para pacotes de despertar. Se o adaptador de rede não estiver configurado para pacotes de despertar ou se esta definição estiver desativada, o Gestor de Configuração configurará-o automaticamente e activa-o-á para um computador quando receber a definição do cliente para ativar o proxy de despertar.  

-   Se um computador tiver mais de um adaptador de rede, não é possível configurar qual adaptador a utilizar para procuração de despertar; a escolha não é determinista. No entanto, o adaptador escolhido\> @SYSTEM_0.log é registado no ficheiro SleepAgent_<DOMAIN.  

-   A rede deve permitir pedidos de eco do ICMP (pelo menos dentro da sub-rede). Não é possível configurar o intervalo de cinco segundos que é usado para enviar os comandos de ping do ICMP.  

-   A comunicação não é encriptada e não autenticada, e o IPsec não é suportado.  

-   As seguintes configurações de rede não são suportadas:  

    -   802.1X com autenticação portuário  

    -   Redes sem fios  

    -   Interruptores de rede que ligam endereços MAC a portas específicas  

    -   Redes iPv6 só  

    -   Duração do contrato de arrendamento DHCP inferior a 24 horas  

Se quiser acordar computadores para instalação de software programado, tem de configurar cada site primário para utilizar pacotes de despertar.  

 Para utilizar o proxy de despertar, deve implementar as definições de cliente proxy de despertar da Power Management para além de configurar o site principal.  

Decida se utiliza pacotes de transmissão dirigidos a subredes, ou pacotes unicast, e que número de porta UDP usar. Por padrão, os pacotes tradicionais de despertar são transmitidos usando a porta 9 da UDP, mas para ajudar a aumentar a segurança, pode selecionar uma porta alternativa para o site se esta porta alternativa for suportada por routers e firewalls intervindo.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Escolha entre a Transmissão Unicast e subnet-dirigida para Wake-on-LAN  
 Se optou por acordar computadores enviando pacotes tradicionais de despertar, tem de decidir se transmite pacotes unicast ou pacotes de transmissão direta supérrios. Se utilizar procuração de despertar, deve utilizar pacotes unicast. Caso contrário, utilize a tabela seguinte para o ajudar a determinar qual o método de transmissão a escolher.  

|Método de transmissão|Vantagem|Desvantagem|  
|-------------------------|---------------|------------------|  
|Unicast|Solução mais segura do que as transmissões direcionadas para a sub-rede porque o pacote é enviado diretamente para um computador em vez de para todos os computadores numa subnet.<br /><br /> Pode não necessitar de reconfiguração dos routers (pode ter de configurar a cache ARP).<br /><br /> Consome menos largura de banda de rede do que as transmissões de transmissão dirigidas por subredes.<br /><br /> Suportado com IPv4 e IPv6.|Os pacotes de despertar não encontram computadores de destino que tenham alterado o seu endereço de subnet após o último calendário de inventário de hardware.<br /><br /> Os interruptores podem ter de ser configurados para encaminhar pacotes uDP.<br /><br /> Alguns adaptadores de rede podem não responder a pacotes de despertar em todos os estados do sono quando usam unicast como o método de transmissão.|  
|Transmissão dirigida por subnet|Taxa de sucesso mais elevada do que unicast se tiver computadores que frequentemente alteram o seu endereço IP na mesma sub-rede.<br /><br /> Não é necessária reconfiguração do interruptor.<br /><br /> Alta taxa de compatibilidade com adaptadores de computador para todos os estados do sono, porque as transmissões dirigidas por subredes eram o método de transmissão original para o envio de pacotes de despertar.|Solução menos segura do que usar o unicast porque um intruso poderia enviar fluxos contínuos de pedidos de eco do ICMP de um endereço de origem falsificado para o endereço de transmissão dirigido. Isto faz com que todos os anfitriões respondam a esse endereço de origem. Se os routers estiverem configurados para permitir transmissões direcionadas para a sub-rede, a configuração adicional é recomendada por razões de segurança:<br /><br /> - Configure os routers para permitir apenas transmissões direcionadas por IP do servidor do site do Gestor de Configuração, utilizando um número de porta UDP especificado.<br />- Configure o Gestor de Configuração para utilizar o número de porta não predefinido especificado.<br /><br /> Pode exigir a reconfiguração de todos os routers intervenientes para permitir transmissões dirigidas por sub-rede.<br /><br /> Consome mais largura de banda da rede do que transmissões unicast.<br /><br /> Suportado apenas com IPv4; O IPv6 não é suportado.|  

> [!WARNING]  
>  Existem riscos de segurança associados a transmissões direcionadas para a sub-rede: Um intruso pode enviar fluxos contínuos de pedidos de eco do Protocolo de Mensagem de Controlo de Internet (ICMP) a partir de um endereço de origem falsificado para o endereço de transmissão dirigido, o que faz com que todos os anfitriões respondam a esse endereço de origem. Este tipo de ataque de negação de serviço é geralmente chamado de ataque de smurf e é tipicamente atenuado por não permitir transmissões dirigidas por subredes.
