---
title: Preparar a implementação do SO
titleSuffix: Configuration Manager
description: Saiba como se preparar para implementações do sistema operativo no Gestor de Configuração
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724084"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Prepare-se para a implementação do OS no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Há várias coisas que deve fazer no 'Gestor de Configuração' antes de poder implementar sistemas operativos. Utilize os seguintes artigos para preparar a implantação do OS:  

-   [Gerir imagens de arranque](manage-boot-images.md)  

-   [Gerir imagens do SO](manage-operating-system-images.md)  

-   [Gerir pacotes de atualização do SO](manage-operating-system-upgrade-packages.md)  

-   [Gerir controladores](manage-drivers.md)  

-   [Gerir o estado do utilizador](manage-user-state.md)  

-   [Preparar implementações de computadores desconhecidos](prepare-for-unknown-computer-deployments.md)  

-   [Associar utilizadores a um computador de destino](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Tamanho da imagem do OS  

As imagens de sosão são de tamanho grande. Por exemplo, o tamanho da imagem para o Windows 7 é de 3 GB ou mais. O tamanho da imagem e o número de computadores para os quais simultaneamente implementa o SISTEMA afeta o desempenho da rede e a largura de banda disponível. Certifique-se de testar o desempenho da rede. Testar melhor o impacto mede o efeito que a implementação da imagem pode ter e o tempo que leva para completar a implementação. As atividades do Gestor de Configuração que afetam o desempenho da rede incluem distribuir a imagem para um ponto de distribuição, distribuir a imagem de um site para outro, e descarregar a imagem para o cliente.  

Certifique-se também de que planeia um espaço de armazenamento suficiente em disco nos pontos de distribuição que acolhem as imagens de SO.  

Para mais informações, consulte [considerações adicionais de planeamento para pontos de distribuição](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Tamanho da cache do cliente  

Quando os clientes do Gestor de Configuração descarregam conteúdo, utilizam automaticamente o Serviço de Transferência Inteligente de Fundo (BITS), se estiver disponível. Ao implementar uma sequência de tarefas que instala um SISTEMA, pode definir uma opção na implementação para que os clientes do Gestor de Configuração descarreguem a imagem completa para uma cache local antes da sequência de tarefas ser executado.  

Quando um cliente do Gestor de Configuração tem de descarregar uma imagem de OS, mas não há espaço suficiente na cache, o cliente pode limpar espaço na sua cache. Verifica os outros pacotes na cache para determinar se a abater algum dos pacotes mais antigos libertará espaço suficiente para acomodar a imagem. Se os pacotes de apagarem não libertarem espaço suficiente, o cliente não descarrega a imagem e a implementação falha. Este comportamento pode ocorrer se a cache tiver um pacote grande que configura para persistir na cache. Se a eliminação de pacotes antigos libertar espaço suficiente de disco na cache, o cliente eliminá-los-á e transferirá em seguida a imagem para a cache.  

O tamanho de cache padrão nos clientes do Gestor de Configuração pode não ser grande o suficiente para a maioria das implementações de imagem de SO. Se planeia descarregar a imagem completa para a cache do cliente, ajuste o tamanho da cache do cliente nos computadores de destino para acomodar o tamanho da imagem que está a implementar.  

Para mais informações, consulte [Configure a cache do cliente](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


