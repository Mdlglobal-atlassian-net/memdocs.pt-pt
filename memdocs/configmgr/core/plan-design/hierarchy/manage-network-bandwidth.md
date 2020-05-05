---
title: Gerir a largura de banda da rede para conteúdos
titleSuffix: Configuration Manager
description: Configure o agendamento, o estrangulamento e o conteúdo pré-encenado para o Gestor de Configuração.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ee7d00f3b5c98528d9999b83b07aa393b72e36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720591"
---
# <a name="manage-network-bandwidth-for-content"></a>Gerir a largura de banda da rede para conteúdos
Para ajudá-lo a gerir a largura de banda da rede que é usada para o processo de gestão de conteúdos do Gestor de Configuração, pode utilizar controlos incorporados para agendamento e estrangulamento. Também pode utilizar conteúdo pré-encenado. As secções seguintes descrevem estas opções mais detalhadamente.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Agendamento e estrangulamento  

 Quando criar um pacote, altere a rota de origem para o conteúdo ou atualize o conteúdo no ponto de distribuição, os ficheiros são copiados do caminho de origem para a biblioteca de conteúdos no servidor do site. Em seguida, o conteúdo é copiado da biblioteca de conteúdos no servidor do site para a biblioteca de conteúdos nos pontos de distribuição. Quando os ficheiros de origem de conteúdo são atualizados e os ficheiros de origem já foram distribuídos, o Gestor de Configuração recupera apenas os ficheiros novos ou atualizados e envia-os para o ponto de distribuição.

 Pode utilizar controlos de agendamento e estrangulamento para a comunicação site-to-site e para comunicação entre um servidor de site e um ponto de distribuição remoto. Se a largura de banda da rede for limitada mesmo depois de configurar os controlos de agendamento e estrangulamento, poderá considerar antecipar o conteúdo no ponto de distribuição.  

 No 'Gestor de Configuração', pode configurar um horário e especificar definições de estrangulamento em pontos de distribuição remota que determinam quando e como a distribuição de conteúdos é realizada. Cada ponto de distribuição remoto pode ter configurações diferentes que ajudam a lidar com as limitações de largura de banda da rede desde o servidor do site até ao ponto de distribuição remoto. Os controlos de agendamento e estrangulamento ao ponto de distribuição remoto são semelhantes às definições para um endereço de remetente padrão. Neste caso, as definições são utilizadas por um novo componente, chamado Gestor de Transferência de Pacotes.

 O Gestor de Transferência de Pacotes distribui conteúdo de um servidor de site, como um site primário ou site secundário, para um ponto de distribuição que está instalado num sistema de site. As definições de estrangulamento são especificadas no separador **Limites** de Taxa, e as definições de agendamento são especificadas no separador **'Agendar',** para um ponto de distribuição que não se encontra num servidor de site. As definições de tempo baseiam-se no fuso horário do local de envio, não no ponto de distribuição.  

> [!IMPORTANT]  
>  Os **separadores Rate Limits** e **Schedule** são apresentados apenas nas propriedades para pontos de distribuição que não estão instalados num servidor de site.  

Para mais informações, consulte [Instalar e configurar pontos](../../servers/deploy/configure/install-and-configure-distribution-points.md)de distribuição para 'Gestor de Configuração'.  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Conteúdo pré-encenado  
 Pode pré-encenar o conteúdo para adicionar os ficheiros de conteúdo à biblioteca de conteúdos num servidor ou ponto de distribuição do site, antes de distribuir o conteúdo. Como os ficheiros de conteúdo já estão na biblioteca de conteúdos, não transferem a rede quando distribui o conteúdo. Pode pré-encenar ficheiros de conteúdo para aplicações e pacotes.  

Na consola 'Gestor de Configuração', selecione o conteúdo que pretende pré-encenar e, em seguida, utilize o Assistente de Ficheiros de **Conteúdo Pré-encenado**. Isto cria um ficheiro de conteúdo comprimido e pré-encenado que contém os ficheiros e metadados associados para o conteúdo. Em seguida, pode importar manualmente o conteúdo num servidor ou ponto de distribuição do site. Tenha em atenção os seguintes pontos:  

-   Quando importa o ficheiro de conteúdo pré-encenado num servidor de site, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no servidor do site e, em seguida, registados na base de dados do servidor do site.  

-   Quando importa o ficheiro de conteúdo pré-encenado num ponto de distribuição, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no ponto de distribuição. Uma mensagem de estado é enviada para o servidor do site que informa o site de que o conteúdo está disponível no ponto de distribuição.  

Pode configurar opcionalmente o ponto de distribuição como **pré-encenado** para ajudar a gerir a distribuição de conteúdos. Depois, quando distribui conteúdo, pode escolher se pretende:  

-   Sempre pré-estágio do conteúdo no ponto de distribuição.  

-   Pré-fase do conteúdo inicial para a embalagem e, em seguida, use o processo de distribuição padrão de conteúdo quando houver atualizações para o conteúdo.  

-   Utilize sempre o processo padrão de distribuição de conteúdos para o conteúdo da embalagem.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Determine se deve pré-encenar conteúdo  
 Considere o conteúdo preponderantes para aplicações e pacotes nos seguintes cenários:  

-   **Para resolver a questão da largura de banda de rede limitada do servidor do site para um ponto de distribuição.** Se o agendamento e o estrangulamento não forem suficientes para satisfazer as suas preocupações sobre a largura de banda, considere antecipar o conteúdo no ponto de distribuição. Cada ponto de distribuição tem o Ponto de distribuição Enable para a definição **de conteúdo pré-encenado** que pode escolher nas propriedades do ponto de distribuição. Quando ativa esta opção, o ponto de distribuição é identificado como um ponto de distribuição pré-encenado, e pode escolher como gerir o conteúdo numa base por pacote.  

    As seguintes definições estão disponíveis nas propriedades para uma aplicação, pacote, pacote de controlador, imagem de arranque, instalador do sistema operativo e imagem. Estas definições permitem-lhe escolher como a distribuição de conteúdos é gerida em pontos de distribuição remota que são identificados como pré-encenados:  

    -   **Descarregue automaticamente os conteúdos quando os pacotes forem atribuídos a pontos de distribuição**: Utilize esta opção quando tiver pacotes mais pequenos, e as definições de agendamento e estrangulamento fornecem controlo suficiente para a distribuição de conteúdos.  

    -   **Descarregue apenas alterações de conteúdo para o ponto de distribuição**: Utilize esta opção quando espera que futuras atualizações do conteúdo da embalagem sejam geralmente menores do que a embalagem inicial. Por exemplo, pode pré-encenar uma aplicação como o Microsoft Office, porque o tamanho inicial do pacote é superior a 700 MB e é demasiado grande para enviar a rede. No entanto, as atualizações de conteúdo deste pacote podem ser inferiores a 10 MB, e são aceitáveis para distribuir pela rede. Outro exemplo pode ser o pacote de condutores, onde o tamanho inicial do pacote é grande, mas as adições incrementais do condutor à embalagem podem ser pequenas.  

    -   **Copie manualmente o conteúdo desta embalagem para o ponto**de distribuição : Utilize esta opção quando tiver grandes pacotes, com conteúdos como um sistema operativo, e nunca pretende utilizar a rede para distribuir o conteúdo até ao ponto de distribuição. Quando selecionar esta opção, deve pré-encenar o conteúdo no ponto de distribuição.  

    > [!IMPORTANT]  
    >  As opções anteriores são aplicáveis por pacote, e só são utilizadas quando um ponto de distribuição é identificado como pré-encenado. Os pontos de distribuição que não foram identificados como pré-encenados ignoram estas definições. Neste caso, o conteúdo é sempre distribuído pela rede desde o servidor do site até aos pontos de distribuição.  

-   **Para restaurar a biblioteca de conteúdos num servidor do site.** Quando um servidor de site falha, as informações sobre pacotes e aplicações que estão contidas na biblioteca de conteúdos são restauradas na base de dados do site como parte do processo de restauro, mas os ficheiros da biblioteca de conteúdos não são restaurados como parte do processo. Se não tiver uma cópia de segurança do sistema de ficheiros para restaurar a biblioteca de conteúdos, pode criar um ficheiro de conteúdo pré-encenado a partir de outro site que contenha os pacotes e aplicações que tem de ter. Em seguida, pode extrair o ficheiro de conteúdo pré-encenado no servidor do site recuperado. Para obter mais informações sobre a cópia de segurança e recuperação do servidor do site, consulte [backup e recuperação para 'Gestor](../../servers/manage/backup-and-recovery.md)de Configuração'.  
