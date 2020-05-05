---
title: Localização da fonte de conteúdo
titleSuffix: Configuration Manager
description: Conheça as definições do Gestor de Configuração que permitem aos clientes encontrar conteúdo numa rede lenta.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720241"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Cenários de localização de fonte de conteúdo no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes da versão 1610, o Gestor de Configuração suportava várias definições que combinavam para definir como e onde os clientes encontram conteúdo quando estão numa rede lenta. As possíveis combinações afetam a localização do conteúdo que os clientes utilizam e se podem utilizar com sucesso um local de recuo quando não existe uma fonte preferida de conteúdo.  

> [!IMPORTANT]  
> **Se os seus sites executarem a versão 1511, 1602 ou 1606,** a informação neste tópico aplica-se à sua infraestrutura. Consulte também [os grupos de fronteira para versões 1511.1602 e 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) para informações específicas para grupos de fronteira com estas versões de Configuração Manager.
>
> **Se os seus sites executarem a versão 1610 ou posterior,** utilize as informações nos limites do [site Define e grupos de limites para o Gestor](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) de Configuração para entender como os seus clientes encontram pontos de distribuição que tenham conteúdo disponível.





**As três definições seguintes definem o comportamento quando os clientes solicitam conteúdo:**

- **Permitir** a localização da fonte de recuo para o conteúdo (ativado ou não ativado): Esta é uma opção que pode ativar no separador **De grupos** de fronteira de um ponto de distribuição. Isto permite ao cliente usar um ponto de distribuição configurado como um local de recuo quando o conteúdo não está disponível num ponto de distribuição preferido.  

  - **Comportamento de implementação para**a velocidade de ligação da rede : Cada implementação é configurada com um dos seguintes comportamentos a utilizar quando a ligação ao ponto de distribuição é lenta:  

    -   **Descarregue o conteúdo do ponto de distribuição e execute-o localmente**  

    -   **Não descarregue o conteúdo**: Esta opção só é utilizada quando um cliente utiliza um local de recuo para obter conteúdo.  

    A velocidade de ligação para um ponto de distribuição está configurada no separador **Referências** de um grupo de limites, e é específica desse grupo de fronteira.  

  - **Distribuição de pacotes** a pedido (para pontos de distribuição preferidos): Isto é ativado quando seleciona a opção **Distribuir o conteúdo deste pacote para pontos** de distribuição preferenciais no separador **Definições** de Distribuição das propriedades de um pacote ou aplicação. Quando ativada, esta opção direciona o Gestor de Configuração para copiar automaticamente o conteúdo para um ponto de distribuição preferido que ainda não tenha o conteúdo depois de um cliente solicitar esse conteúdo a partir desse ponto de distribuição.  


 **Os seguintes requisitos aplicam-se a todos os cenários:**


-   O conteúdo está disponível num ponto de distribuição de recuo  

-   Os pontos de distribuição estão online e acessíveis  


## <a name="scenario-1"></a>Cenário 1  
 Aplica-se quando existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferido**  

-   **Permitir recuo**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que contêm o conteúdo.  

3.  O cliente descarrega o conteúdo a partir de um ponto de distribuição preferido da lista.  

## <a name="scenario-2"></a>Cenário 2  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferido**  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não descarregue conteúdos  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo são permitidos.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que contêm o conteúdo.  

3.  O cliente descarrega o conteúdo a partir de um ponto de distribuição preferido da lista.  

## <a name="scenario-3"></a>Cenário 3  
 Existem as seguintes configurações:  

-   **O conteúdo está disponível num ponto de distribuição preferido**  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Descarregue e instale conteúdo  


**Detalhes:** (A configuração para distribuição de pacotes a pedido não é relevante neste cenário.)  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo são permitidos.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que contêm o conteúdo.  

3.  O cliente descarrega o conteúdo a partir de um ponto de distribuição preferido da lista.  

## <a name="scenario-4"></a>Cenário 4  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos não está ativado  

-   **Permitir recuo**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que têm o conteúdo. Não há pontos de distribuição preferidos na lista.  

3.  O cliente falha com a mensagem **O conteúdo não está disponível** e entra em modo de retry. Um novo pedido de conteúdo é iniciado a cada hora.  

## <a name="scenario-5"></a>Cenário 5  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos não está ativado  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não descarregue conteúdos  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo são permitidos.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que têm o conteúdo. Não existem pontos de distribuição preferidos que tenham o conteúdo, mas pelo menos um ponto de distribuição de recuo tem o conteúdo.  

3.  O conteúdo não é descarregado porque a propriedade de implementação para quando o cliente usa um ponto de distribuição de recuo está definida para **Não descarregar conteúdo** (que é usado quando os clientes recuam para obter o conteúdo). O cliente falha com a mensagem **O conteúdo não está disponível** e entra em modo de retry. O cliente faz um novo pedido de conteúdo a cada hora.  

## <a name="scenario-6"></a>Cenário 6  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos não está ativado  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Descarregue e instale conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo estão ativados.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que têm o conteúdo. Não existem pontos de distribuição preferidos que tenham o conteúdo, mas pelo menos um ponto de distribuição de recuo que tenha o conteúdo.  

3.  O conteúdo é descarregado a partir de um ponto de distribuição de recuo na lista porque a propriedade de implementação para quando o cliente usa um ponto de distribuição de recuo está definida para **descarregar e instalar o conteúdo**.  

## <a name="scenario-7"></a>Cenário 7  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos está ativado  

-   **Permitir recuo**: Não ativado  

-   **Comportamento de implementação para uma rede lenta**: Qualquer configuração  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que têm o conteúdo. Não existem pontos de distribuição preferidos que tenham o conteúdo.  

3.  O cliente falha com a mensagem **O conteúdo não está disponível** e entra em modo de retry. Um novo pedido de conteúdo é feito a cada hora.  

4.  O ponto de gestão cria um gatilho para o Gestor de Distribuição distribuir o conteúdo por todos os pontos de distribuição preferidos para o cliente que fez o pedido de conteúdo.  

5.  O Gestor de Distribuição distribui o conteúdo a todos os pontos de distribuição preferidos. Na maioria dos casos, o conteúdo é distribuído com sucesso para os pontos de distribuição preferidos dentro de uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente até ao ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que têm o conteúdo. O cliente descarrega o conteúdo a partir de um ponto de distribuição preferido da lista.  

## <a name="scenario-8"></a>Cenário 8  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos está ativado  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Não descarregue conteúdos  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo são permitidos.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que têm o conteúdo. Não existem pontos de distribuição preferidos que tenham o conteúdo, mas pelo menos um ponto de distribuição de recuo tem o conteúdo.  

3.  O conteúdo não é descarregado porque a propriedade de implementação para quando o cliente usa um ponto de distribuição de recuo está definida para **Não descarregar**. O cliente falha com a mensagem **O conteúdo não está disponível** e entra em modo de retry. O cliente faz um novo pedido de conteúdo a cada hora.  

4.  O ponto de gestão cria um gatilho para o Gestor de Distribuição distribuir o conteúdo por todos os pontos de distribuição preferidos para o cliente que fez o pedido de conteúdo.  

5.  O Gestor de Distribuição distribui o conteúdo a todos os pontos de distribuição preferidos. Na maioria dos casos, o conteúdo é distribuído com sucesso para os pontos de distribuição preferidos dentro de uma hora.  

6.  Um novo pedido de conteúdo é iniciado pelo cliente até ao ponto de gestão.  

7.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos que têm o conteúdo.  

8.  O cliente descarrega o conteúdo a partir de um ponto de distribuição preferido da lista.  

## <a name="scenario-9"></a>Cenário 9  
 Existem as seguintes configurações:  

-   **O conteúdo não está disponível num ponto de distribuição preferido**  

-   **Distribuir o conteúdo deste pacote para pontos** de distribuição preferidos está ativado  

-   **Permitir o recuo**: Ativado  

-   **Comportamento de implementação para uma rede lenta**: Descarregue e instale conteúdo  


**Detalhes:**  

1.  O cliente envia um pedido de conteúdo para o ponto de gestão. O cliente inclui uma bandeira com o pedido que indica que os pontos de distribuição de recuo são permitidos.  

2.  Uma lista de localização de conteúdo é devolvida ao cliente a partir do ponto de gestão com os pontos de distribuição preferidos e pontos de distribuição de recuo que têm o conteúdo. Não existem pontos de distribuição preferidos que tenham o conteúdo, mas pelo menos um ponto de distribuição de recuo tem o conteúdo.  

3.  O conteúdo é descarregado a partir de um ponto de distribuição de recuo na lista porque a propriedade de implementação para quando o cliente usa um ponto de distribuição de recuo está definida para **descarregar e instalar o conteúdo**. Esta definição de implementação permite a um cliente que deve utilizar um local de conteúdo de recuo para obter o conteúdo a partir desse local.  

4.  O ponto de gestão cria um gatilho para o Gestor de Distribuição distribuir o conteúdo por todos os pontos de distribuição preferidos para o cliente que fez o pedido de conteúdo.  

5.  O Gestor de Distribuição distribui o conteúdo a todos os pontos de distribuição preferidos, o que permite que clientes adicionais obtenham o conteúdo sem utilizar um ponto de distribuição de recuo.  
