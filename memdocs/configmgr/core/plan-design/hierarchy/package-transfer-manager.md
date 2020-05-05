---
title: Gestor de Transferência de Pacotes
titleSuffix: Configuration Manager
description: Entenda como o Gestor de Transferência de Pacotes no Gestor de Configuração transfere conteúdo de um servidor de site para pontos de distribuição remotos.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722453"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Gestor de transferência de pacotes no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Num site do Gestor de Configuração, o Gestor de Transferência de Pacotes é um componente do serviço de SMS_Executive que gere a transferência de conteúdo de um computador de servidor de site para pontos de distribuição remoto num site. (Um ponto de distribuição remota é aquele que não está localizado no computador do servidor do site.) O Gestor de Transferência de Pacotes não suporta configurações pelo administrador, mas entender como funciona pode ajudá-lo a planear a sua infraestrutura de gestão de conteúdos. Também pode ajudá-lo a resolver problemas com a distribuição de conteúdos.


Quando distribui conteúdo para um ou mais pontos de distribuição remotos num site, o **Gestor de Distribuição** cria um trabalho de transferência de conteúdo. Em seguida, anota o Gestor de Transferência de Pacotes em servidores de sites primários e secundários para transferir o conteúdo para os pontos de distribuição remotos.

 O Gestor de Transferência de Pacotes regista as suas ações no ficheiro **pkgxfermgr.log** no servidor do site. O ficheiro de registo é o único local onde pode ver as atividades do Gestor de Transferência de Pacotes.  

> [!NOTE]  
>  Em versões anteriores do Gestor de Configuração, o Gestor de Distribuição gere a transferência de conteúdo para um ponto de distribuição remoto. O Gestor de Distribuição também gere a transferência de conteúdos entre sites. Com o Gestor de Configuração, o Gestor de Distribuição continua a gerir a transferência de conteúdos entre dois sites. No entanto, o Gestor de Transferência de Pacotes gere agora a transferência de conteúdos para um grande número de pontos de distribuição. Isto ajuda a aumentar o desempenho global da implementação de conteúdos tanto entre sites como para pontos de distribuição dentro de um site.  

Para transferir conteúdo para um ponto de distribuição padrão, o Gestor de Transferência de Pacotes opera da mesma forma que o Gestor de Distribuição opera em versões anteriores do Gestor de Configuração. Ou seja, gere ativamente a transferência de ficheiros para cada ponto de distribuição remoto. No entanto, para distribuir conteúdo para um ponto de distribuição de puxar, o Gestor de Transferência de Pacotes notifica o ponto de distribuição de puxar que o conteúdo está disponível. O ponto de distribuição de puxar assume então o processo de transferência.  

As seguintes informações descrevem como o Gestor de Transferência de Pacotes gere a transferência de conteúdo para pontos de distribuição padrão, e para pontos de distribuição configurados como pontos de distribuição de puxar:
1.  **A Administração implementa conteúdo para um ou mais pontos de distribuição num site.**  

    -   **Ponto de distribuição padrão:** O Gestor de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

    -   **Ponto de distribuição de puxar:** O Gestor de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

2.  **O Gestor de Distribuição faz verificações preliminares.**  

    -   **Ponto de distribuição padrão:** O Gestor de Distribuição executa uma verificação básica para confirmar que cada ponto de distribuição está pronto para receber o conteúdo. Após este check, o Gestor de Distribuição notifica o Gestor de Transferência de Pacotes para iniciar a transferência de conteúdos para o ponto de distribuição.  

    -   **Ponto de distribuição de puxar:** O Gestor de Distribuição inicia o Gestor de Transferência de Pacotes, que depois notifica o ponto de distribuição de puxar que existe um novo trabalho de transferência de conteúdos. O Gestor de Distribuição não verifica o estado dos pontos de distribuição remotos que são pontos de distribuição de puxar, porque cada ponto de distribuição de puxar gere as suas próprias transferências de conteúdo.  

3.  **O Gestor de Transferência de Pacotes prepara-se para transferir conteúdo.**  

    -   **Ponto de distribuição padrão:** O Gestor de Transferência de Pacotes examina a loja de conteúdos de cada ponto de distribuição remoto especificado. O objetivo disto é identificar quaisquer ficheiros que já estejam nesse ponto de distribuição. Em seguida, o Gestor de Transferência de Pacotes faz fila para transferência apenas dos ficheiros que ainda não estão presentes.  

        > [!NOTE]  
        >  Para copiar cada ficheiro na distribuição para o ponto de distribuição, mesmo que os ficheiros já estejam presentes na loja de uma instância única do ponto de distribuição, utilize a ação **redistribuir** para conteúdo.  

    -   **Ponto de distribuição de puxar:** Para cada ponto de distribuição na distribuição, o Gestor de Transferência de Pacotes verifica os pontos de distribuição de pontos de distribuição de pontos de distribuição, para confirmar se o conteúdo está disponível.  

        -   Quando o conteúdo está disponível em pelo menos um ponto de distribuição de origem, o Gestor de Transferência de Pacotes envia uma notificação para esse ponto de distribuição de puxar. A notificação direciona esse ponto de distribuição para iniciar o processo de transferência de conteúdos. A notificação inclui nomes de ficheiros e tamanhos, atributos e valores de haxixe.  

        -   Quando o conteúdo ainda não está disponível, o Gestor de Transferência de Pacotes não envia uma notificação para o ponto de distribuição. Em vez disso, repete o cheque a cada 20 minutos até que o conteúdo esteja disponível. Em seguida, quando o conteúdo está disponível, o Gestor de Transferência de Pacotes envia a notificação para esse ponto de distribuição de puxar.  

        > [!NOTE]  
        >  Para que o ponto de distribuição de puxar copie cada ficheiro na distribuição para o ponto de distribuição, mesmo que os ficheiros já estejam presentes na loja de uma instância única do ponto de distribuição de puxar, utilize a ação **de redistribuição** para conteúdo.  

4.  **O conteúdo começa a ser transferido.**  

    -   **Ponto de distribuição padrão:** O Gestor de Transferência de Pacotes copia ficheiros para cada ponto de distribuição remoto. Durante a transferência para um ponto de distribuição padrão:  

        -   Por padrão, o Gestor de Transferência de Pacotes pode simultaneamente processar três pacotes únicos e distribuí-los em cinco pontos de distribuição em paralelo. Coletivamente, estas são chamadas definições de **distribuição simultânea**. Para configurar a distribuição simultânea, nas Propriedades componentes de distribuição de **software** para cada site, vá ao separador **Geral.**  

        -   O Gestor de Transferência de Pacotes utiliza as configurações de marcação e largura de banda da rede de cada ponto de distribuição ao transferir conteúdo para esse ponto de distribuição. Para configurar estas definições, nas **propriedades** de cada ponto de distribuição remoto, vá aos separadores **Limites** de Agenda e **Tarifa.** Para mais informações, consulte Gerir a infraestrutura de conteúdo e conteúdo para O Gestor de [Configuração](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Ponto de distribuição de puxar:** Quando um ponto de distribuição de puxar recebe um ficheiro de notificação, o ponto de distribuição inicia o processo de transferência do conteúdo. O processo de transferência funciona de forma independente em cada ponto de distribuição de puxar:  

        1.   A distribuição de pull-distribution identifica os ficheiros na distribuição de conteúdos que ainda não possui na sua loja de instância única, e prepara-se para descarregar esse conteúdo a partir de um dos seus pontos de distribuição de origem.  

        2.   Em seguida, o ponto de distribuição de puxar verifica com cada um dos seus pontos de distribuição de origem, por ordem, até localizar um ponto de distribuição de fonte que tenha o conteúdo disponível. Quando o ponto de distribuição de puxar identifica um ponto de distribuição de origem com o conteúdo, inicia o download desse conteúdo.  

        > [!NOTE]  
        >  O processo de descarregamento de conteúdos pelo ponto de distribuição de pull é o mesmo que o utilizado pelos clientes do Gestor de Configuração. Para a transferência de conteúdo pelo ponto de distribuição de puxar, as definições de transferência simultâneas não são utilizadas. As opções de agendamento e estrangulamento que configura para pontos de distribuição padrão também não são utilizadas.  

5.  **A transferência de conteúdos completa.**  

    -   **Ponto de distribuição padrão:** Após o gestor de transferência de pacotes ser feito transferindo ficheiros para cada ponto de distribuição remoto designado, verifica o hash do conteúdo no ponto de distribuição. Em seguida, notifica o Gestor de Distribuição que a distribuição está completa.  

    -   **Ponto de distribuição de puxar:** Após o ponto de distribuição de puxar completar o download de conteúdo, o ponto de distribuição verifica o hash do conteúdo. Em seguida, submete uma mensagem de estado ao ponto de gestão do site para indicar sucesso. Se, passados 60 minutos, este estado não for recebido, o Gestor de Transferência saem novamente. Verifica com o ponto de distribuição de puxar para confirmar se o ponto de distribuição de puxar descarregou o conteúdo. Se o download de conteúdo estiver em andamento, o Gestor de Transferência de Pacotes dorme por mais 60 minutos antes de verificar novamente com o ponto de distribuição de puxar. Este ciclo continuará até o ponto de distribuição de extração concluir a transferência do conteúdo.  
