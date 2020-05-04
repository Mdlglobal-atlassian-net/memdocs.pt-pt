---
title: Manage VDI clients (Gerir clientes de VDI)
titleSuffix: Configuration Manager
description: Gerencie os clientes do Gestor de Configuração numa infraestrutura virtual de ambiente de trabalho (VDI).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713325"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Gerir clientes do Gestor de Configuração numa infraestrutura virtual de ambiente de trabalho (VDI)

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta a instalação do cliente do Gestor de Configuração nos seguintes cenários de infraestrutura de ambiente de trabalho virtual (VDI):  

- **Máquinas virtuais pessoais** - As máquinas virtuais pessoais são geralmente utilizadas quando pretende certificar-se de que os dados e configurações do utilizador são mantidos na máquina virtual entre sessões.  

- **Sessões remotas** de Serviços de Desktop - Serviços de Ambiente de Trabalho Remoto saem de um servidor para acolher múltiplas sessões de clientes simultâneas. Os utilizadores podem ligar-se a uma sessão e depois executar aplicações nesse servidor.  

- **Máquinas virtuais agruizadas** - Máquinas virtuais agrinadas não são persistidas entre sessões. Quando uma sessão está fechada, todos os dados e configurações são descartados. As máquinas virtuais agruizadas são úteis quando os Serviços de Ambiente de Trabalho Remoto não podem ser utilizados porque uma aplicação de negócios necessária não pode ser executada no Windows Server que acolhe as sessões do cliente.  

  A tabela seguinte enumera considerações para gerir o cliente do Gestor de Configuração numa infraestrutura virtual de ambiente de trabalho.  

|Tipo de máquina virtual|Considerações|  
|--------------------------|--------------------|  
|Máquinas virtuais pessoais|O Gestor de Configuração trata as máquinas virtuais pessoais de forma idêntica a um computador físico. O cliente Do Gestor de Configuração pode ser pré-instalado na imagem da máquina virtual ou implantado após o fornecimento da máquina virtual.|  
|Serviços de Ambiente de Trabalho Remoto|O cliente do Gestor de Configuração não está instalado para sessões individuais de ambiente de trabalho remoto. Em vez disso, o cliente só é instalado uma vez no servidor Remote Desktop Services. Todas as funcionalidades do Gestor de Configuração podem ser utilizadas no servidor Remote Desktop Services.|  
|Máquinas virtuais reunidas|Quando uma máquina virtual agropcada é desativada, quaisquer alterações que faça utilizando o Gestor de Configuração perdem-se.<br /><br /> Os dados devolvidos do Gestor de Configuração, tais como inventário de hardware, inventário de software e medição de software podem não ser relevantes para as suas necessidades, uma vez que a máquina virtual só poderá estar operacional por um curto período de tempo. Considere excluir máquinas virtuais reunidas de tarefas de inventário.|  

 Uma vez que a virtualização suporta a execução de vários clientes do Gestor de Configuração no mesmo computador físico, muitas operações de clientes têm um atraso aleatório incorporado para ações programadas como hardware e inventário de software, digitalizações antimalware, instalações de software e atualização de software. Este atraso ajuda a distribuir o processamento do CPU e a transferência de dados para um computador que tem várias máquinas virtuais que executam o cliente do Gestor de Configuração.  

> [!NOTE]  
>  Com exceção dos clientes Incorporados do Windows que estão em modo de manutenção, os clientes do Gestor de Configuração que não estão a funcionar em ambientes virtualizados também utilizam este atraso aleatório. Quando tem muitos clientes implantados, este comportamento ajuda a evitar picos na largura de banda da rede e reduz o requisito de processamento de CPU nos sistemas do site do Gestor de Configuração, como o ponto de gestão e servidor do site. O intervalo de atraso varia de acordo com a capacidade do Gestor de Configuração.  
>   
>  O atraso de aleatoriedade é desativado por padrão para atualizações de software necessárias utilizando a seguinte definição do cliente: **Computer Agent**: **Desativar a aleatoriedade do prazo**.
