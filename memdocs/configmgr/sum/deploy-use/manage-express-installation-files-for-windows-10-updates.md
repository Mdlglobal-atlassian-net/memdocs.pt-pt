---
title: Gerir atualizações expressas do Windows 10
titleSuffix: Configuration Manager
description: O Gestor de Configuração suporta ficheiros de instalação expresso para o Windows 10, que fornecem downloads menores e tempos de instalação mais rápidos nos clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4093eafe9f8a337ce322165a529f630a759b365f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718645"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação expresso para atualizações do Windows 10

O Gestor de Configuração suporta ficheiros de instalação expresso para atualizações do Windows 10. Configure o cliente para descarregar apenas as alterações entre a atualização de qualidade cumulativa do Windows 10 do mês em curso e a atualização do mês anterior. Sem ficheiros de instalação expresso, os clientes do Gestor de Configuração descarregam a atualização cumulativa completa do Windows 10 todos os meses, incluindo todas as atualizações dos meses anteriores. A utilização de ficheiros de instalação expresso fornece transferências menores e tempos de instalação mais rápidos nos clientes.

Para saber como utilizar o Gestor de Configuração para gerir os conteúdos da atualização para se manter atualizado com o Windows 10, consulte o [Otimize Windows 10 update delivery](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> O suporte ao cliente do OS está disponível no Windows 10, versão 1607, com uma atualização para o Windows Update Agent. Esta atualização está incluída com as atualizações lançadas a 11 de abril de 2017. Para mais informações sobre estas atualizações, consulte o [artigo 4015217](https://support.microsoft.com/kb/4015217). Futuras atualizações aproveitam o expresso para downloads mais pequenos. As versões anteriores do Windows 10 e da versão 1607 do Windows 10 sem esta atualização não suportam ficheiros de instalação expresso.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Ativar o site para descarregar ficheiros de instalação expresso para atualizações do Windows 10
Para começar a sincronizar os metadados dos ficheiros de instalação expresso do Windows 10, ative-os nas propriedades do ponto de atualização do software.  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site da administração central ou o local primário autónomo.  

3. Na fita, clique em **Configurar componentes**do site , e, em seguida, clique em Ponto de **Atualização**de Software . Mude para o separador **Ficheiros de Atualização** e selecione **Descarregue os dois ficheiros completos para todas as atualizações aprovadas e expresse ficheiros de instalação para o Windows 10**.

> [!NOTE]    
> Não é possível configurar o componente do ponto de atualização do software para *apenas* descarregar atualizações expressas.  O site descarrega os ficheiros de instalação expresso para além dos ficheiros completos. Isto aumenta a quantidade de conteúdo armazenado na biblioteca de conteúdos, e distribuído e armazenado nos seus pontos de distribuição.

> [!Tip]  
> Para determinar o espaço real utilizado no disco pelo ficheiro, verifique o **tamanho na** propriedade do disco do ficheiro. O tamanho da propriedade do disco deve ser consideravelmente menor do que o valor tamanho. Para mais informações, consulte [as FAQs para otimizar a entrega da atualização do Windows 10.](optimize-windows-10-update-delivery.md#bkmk_faq)  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Ativar os clientes para descarregar e instalar ficheiros de instalação expressa
Para ativar o suporte de ficheiros de instalação expresso nos clientes, ative ficheiros de instalação expresso no grupo de definições do cliente de **Software Updates.** Esta definição cria um novo ouvinte HTTP que ouve pedidos para descarregar ficheiros de instalação expresso na porta que especifica.

> [!NOTE]    
> Esta é uma porta local que os clientes usam para ouvir pedidos da Otimização de Entrega ou do Serviço de Transferência Inteligente de Fundo (BITS) para descarregar conteúdo expresso a partir do ponto de distribuição. Não precisas de abrir esta porta em firewalls porque todo o tráfego está no computador local.  

Uma vez implementada as definições do cliente para ativar esta funcionalidade no cliente, tenta descarregar o delta entre a atualização cumulativa do Windows 10 do mês em curso e a atualização do mês anterior. Os clientes devem executar uma versão do Windows 10 que suporta ficheiros de instalação expresso.  

1. Ativar o suporte para ficheiros de instalação expresso nas propriedades do componente de ponto de atualização de software (procedimento anterior).  

2. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração** e selecione **Definições de Cliente**.  

3. Selecione as definições apropriadas do cliente e clique em **Propriedades** na fita.  

4. Selecione o grupo **De atualizações** de software. Configure para **Sim** a definição para ativar a **instalação de Atualizações Expressas nos clientes**. Configure a **Porta utilizada para descarregar conteúdos para Express Updates** com a porta utilizada pelo ouvinte HTTP no cliente.
    - Na versão 1902, a **Port utilizada para descarregar conteúdos para Express Updates** foi alterada para o Porto que os clientes usam para receber pedidos de conteúdo **delta.**

## <a name="next-steps"></a>Passos seguintes

[Deploy software updates](deploy-software-updates.md)