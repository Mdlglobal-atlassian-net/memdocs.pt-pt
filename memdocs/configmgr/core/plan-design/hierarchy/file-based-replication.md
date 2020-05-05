---
title: Replicação baseada em ficheiros
titleSuffix: Configuration Manager
description: Saiba como o Gestor de Configuração utiliza replicação baseada em ficheiros para transferir dados entre sites da sua hierarquia
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720171"
---
# <a name="file-based-replication"></a>Replicação baseada em ficheiros

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração utiliza replicação baseada em ficheiros para transferir dados baseados em ficheiros entre sites da sua hierarquia. Estes dados incluem aplicações e pacotes que pretende implementar para pontos de distribuição em sites infantis. Também lida com os registos de dados de descoberta não processados que o site transfere para o seu site-mãe e, em seguida, processa.  

A comunicação baseada em ficheiros entre os sites utiliza o protocolo do bloco de *mensagens* do servidor (SMB) na porta TCP/IP 445. Para controlar a quantidade de dados que o site transfere através da rede, especifique o modo de estrangulamento e pulso da largura de banda. Utilize os horários para controlar quando enviar dados através da rede.  

## <a name="routes"></a><a name="bkmk_routes"></a>Rotas

As seguintes informações podem ajudá-lo a configurar e utilizar rotas de replicação de ficheiros.  

### <a name="file-replication-route"></a>Rota de replicação de ficheiros

Cada rota de replicação de ficheiros identifica um site de destino para o qual um site transfere dados baseados em ficheiros. Cada site suporta uma rota de replicação de ficheiros para um local de destino específico.  

Para gerir uma rota de replicação de ficheiros, dirija-se ao espaço de trabalho da **Administração.** Expanda o nó de **Configuração da Hierarquia** e, em seguida, selecione replicação de **ficheiros**.  

Pode alterar as seguintes definições para as rotas de replicação de ficheiros:  

#### <a name="file-replication-account"></a>Conta de replicação de ficheiros

Esta conta liga-se ao site de destino e escreve dados à **SMS_Site** partilha desse site. O site recetor processa os dados escritos a esta parte. Por predefinição, quando adiciona um site à hierarquia, o Gestor de Configuração atribui a conta de computador do novo servidor como conta de replicação de ficheiros. Em seguida, adiciona esta conta `SMS_SiteToSiteConnection_<sitecode>` ao grupo do site de destino. Este grupo é local para o computador que dá acesso à SMS_Site parte. Pode alterar esta conta para uma conta de utilizador do Windows. Se alterar a conta, certifique-se de adicionar a `SMS_SiteToSiteConnection_<sitecode>` nova conta ao grupo do site de destino.  

> [!NOTE]  
> Os sites secundários utilizam sempre a conta de computador do servidor do site secundário como a **Conta de Replicação de Ficheiros**.  

#### <a name="schedule"></a>Agenda

Detete o horário de cada rota de replicação de ficheiros. Esta ação restringe o tipo de dados e o tempo em que os dados podem ser transferidos para o local de destino.  

#### <a name="rate-limits"></a>Limites de taxas

Especifique os limites de taxa para cada rota de replicação de ficheiros. Esta ação controla a largura de banda da rede que o site utiliza quando transfere dados para o local de destino:  

- **Modo de pulsação**: Especifique o tamanho dos blocos de dados que o site envia para o local de destino. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede de baixa largura de banda para o local de destino.

    Por exemplo, tem restrições para enviar 1 KB de dados a cada cinco segundos, mas não 1 KB a cada três segundos. Esta restrição é independenteda da velocidade do link ou da sua utilização num dado momento.

- **Limitado a taxas máximas**de transferência por hora : O site envia dados para um local de destino utilizando apenas a percentagem de tempo que especifica. O Gestor de Configuração não identifica a largura de banda disponível da rede. Divide o tempo que pode enviar dados em fatias de tempo. Em seguida, envia os dados num curto bloco de tempo, que é seguido por blocos de tempo quando não envia dados.

    Por exemplo, fixa-se a taxa máxima para **50%.** O Gestor de Configuração transmite dados por um período de tempo seguido de um período de tempo igual quando não envia dados. Não gere o tamanho real do bloco de dados que envia. O site gere apenas a quantidade de tempo durante o qual envia dados.  

    > [!CAUTION]  
    > Por predefinição, um site pode utilizar até três **envios simultâneos** para transferir dados para um site de destino. Quando ativa os limites de taxa para uma rota de replicação de ficheiros, limita os **envios simultâneos** para esse site a um. Este comportamento aplica-se mesmo quando a largura de **banda disponível (%)** é fixada em **100%**. Por exemplo, se utilizar as definições predefinidas para o remetente, isto reduz a taxa de transferência para o local de destino para um terço da capacidade padrão.  

#### <a name="routes-between-secondary-sites"></a>Rotas entre locais secundários

Configure uma rota de replicação de ficheiros entre dois sites secundários para encaminhar conteúdo baseado em ficheiros entre esses sites.  


### <a name="sender"></a>Remetente

Cada site tem um remetente. O remetente gere a ligação de rede de um site para um site de destino. Pode estabelecer ligações a vários locais ao mesmo tempo. Para ligar a um site, o remetente utiliza a rota de replicação de ficheiros para o site e identifica a conta que utiliza para estabelecer a ligação à rede. O remetente também usa esta conta para escrever dados para a SMS_Site partilha do site de destino.  

Por padrão, o remetente escreve dados para um site de destino utilizando múltiplos **envios simultâneos**, ou um *fio*. Cada fio pode transferir um objeto diferente baseado em ficheiros para o local de destino. Quando o remetente começa a enviar um objeto, continua a escrever blocos de dados para esse objeto até que envie todo o objeto. Depois de enviar todos os dados para o objeto, um novo objeto pode começar a enviar nesse fio.  

Para gerir o remetente para um site, vá ao espaço de trabalho da **Administração** e expanda o nó de Configuração do **Site.** Selecione o nó **de Sites** e, em seguida, selecione **Propriedades** para o site que pretende gerir. Mude para o **separador Remetente** para alterar as definições do remetente.  

Pode alterar as seguintes definições para um remetente:  

#### <a name="maximum-concurrent-sendings"></a>Envios simultâneos máximos

Por padrão, cada site utiliza cinco envios simultâneos (fios). Três fios estão disponíveis para uso quando envia dados para qualquer site de destino. Ao aumentar este número, pode aumentar a entrada de dados entre sites. Mais fios significam que o Gestor de Configuração pode transferir mais ficheiros ao mesmo tempo. Aumentar este número também aumenta a necessidade de largura de banda de rede entre sites.  

#### <a name="retry-settings"></a>Definições de retry

Por padrão, cada site tenta uma ligação de problemaduas vezes, com um atraso de um minuto entre as tentativas de ligação. Pode modificar o número de tentativas de ligação que o site faz e quanto tempo esperar entre tentativas.  


## <a name="next-steps"></a>Passos seguintes

[Database replication](database-replication.md)
