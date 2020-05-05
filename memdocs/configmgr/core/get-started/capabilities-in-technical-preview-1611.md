---
title: Capacidades na Pré-visualização Técnica 1611
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721550"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1611 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*



Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1611. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    

**Questões Conhecidas nesta Pré-Visualização Técnica:**   
- ***Estado pré-requisito***: Quando instalar a versão 1611, o estado global dos pré-requisitos pode mostrar como passado com avisos, mas não enumera quais os pré-requisitos que causaram os avisos. Isto pode ser causado pelos dois pré-requisitos seguintes:
  - Índice SQL Criar opções de memória
  - Verifica a versão suportada do SQL Server  

  Porque estes são apenas avisos, podem ser ignorados.

- ***PowerShell***: Quando ligar ao Windows PowerShell a partir da consola 'Gestor de Configuração', poderá receber o seguinte erro: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml não está assinado digitalmente**.  

   Pode resolver este problema substituindo certos ficheiros por versões assinadas a partir da versão 1610. Copie todos os ficheiros com as seguintes extensões do ** &lt;diretório de\\ instalação>\AdminConsole\bin** na sua instalação versão 1610: **.psd1**, **.ps1xml**, e **.psm1**. Repasse estes ficheiros no ** &lt;diretório de instalação>\AdminConsole\bin\\ ** na instalação De pré-visualização técnica 1611, sobressonando a versão 1611 dos ficheiros.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo pré-cache para implementações disponíveis e sequências de tarefas
Nesta pré-visualização técnica, para implementações disponíveis e sequências de tarefas, pode optar por utilizar a funcionalidade de pré-cache para que os clientes descarreguem apenas conteúdo relevante antes de um utilizador instalar o conteúdo.

Por exemplo, digamos que pretende implementar uma sequência de tarefas de upgrade do Windows 10 no local, apenas quer uma única sequência de tarefas para todos os utilizadores, e tem múltiplas arquiteturas e/ou idiomas. No Ramo Atual, se criar uma implementação disponível, e depois o utilizador clicar em **Instalar** no Centro de Software, o conteúdo descarrega nessa altura. Isto adiciona tempo adicional antes de a instalação estar pronta para arrancar. Em alternativa, no Ramo Atual se criar uma implementação de sequência de tarefas disponível, todos os conteúdos referenciados na sequência de tarefas são descarregados. Isto inclui o pacote de upgrade do sistema operativo para todas as línguas e arquiteturas. Se cada um tiver aproximadamente 3 GB de tamanho, o pacote de descarregamento pode ser bastante grande.

A funcionalidade de conteúdo pré-cache dá-lhe a opção de permitir que o cliente descarregue apenas o conteúdo aplicável assim que receber a implementação. Portanto, quando o utilizador clica **em Instalar** no Centro de Software, o conteúdo está pronto e a instalação começa rapidamente porque o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar a função pré-cache

1. Crie pacotes de atualização do sistema operativo para arquiteturas e línguas específicas. Especifique a arquitetura e a linguagem no separador **Data Source** do pacote. Para a língua, utilize a conversão decimal (por exemplo, 1033 é a decimal para inglês e 0x0409 é o equivalente hexadecimal). Para mais detalhes, consulte Criar uma sequência de [tarefas para atualizar um sistema operativo](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    A arquitetura e os valores linguísticos são usados para corresponder às condições de etapa da sequência de tarefas que irá criar no próximo passo para determinar se o pacote de atualização do sistema operativo deve ser pré-cache.
2. Crie uma sequência de tarefas com passos condicionais para as diferentes línguas e arquiteturas. Por exemplo, para a versão em inglês pode criar um passo como o seguinte:

    ![propriedades pré-cache](media/precacheproperties2.png)

    ![opções pré-cache](media/precacheoptions2.png)  

3. Implante a sequência de tarefas. Para a função pré-cache, configure o seguinte:
    - No separador **Geral,** selecione **o conteúdo de pré-descarregamento para esta sequência de tarefas**.
    - No separador de definições de **implementação,** configure a sequência de tarefas com a **disponível** para **o efeito**. Se criar uma implementação **necessária,** a funcionalidade de pré-cache não funcionará.
    - No separador **Agendamento,** para o **Horário quando esta implementação estará disponível,** escolha uma hora no futuro que dê aos clientes tempo suficiente para pré-cache o conteúdo antes da implementação ser disponibilizada aos utilizadores. Por exemplo, pode definir o tempo disponível para ser de 3 horas no futuro para permitir tempo suficiente para que o conteúdo seja pré-cache.  
    - No separador Pontos de **Distribuição,** configure as definições das opções de **implementação.** Se o conteúdo não estiver pré-cache de um cliente antes de um utilizador iniciar a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente receber a política de implementação, começará a pré-cache o conteúdo. Isto inclui todos os conteúdos referenciados (quaisquer outros tipos de pacotes) e apenas o pacote de atualização do sistema operativo que corresponde ao cliente com base nas condições que definiu na sequência de tarefas.
- Quando a implementação é disponibilizada aos utilizadores (definição no **separador de agendamento** da implementação), uma notificação mostra informar os utilizadores sobre a nova implementação e a implementação torna-se visível no Software Center. O utilizador pode ir ao Centro de Software e clicar **em Instalar** para iniciar a instalação.
- Se o conteúdo não estiver totalmente pré-cached, então utilizará as definições especificadas no separador Opção de **Implementação** da implementação. Recomendamos que haja tempo suficiente entre quando a implementação é criada e o tempo em que a implementação se torna disponível para os utilizadores para permitir aos clientes tempo suficiente para pré-cache o conteúdo.


## <a name="see-also"></a>Veja também
[Pré-visualização técnica para gestor de configuração](../../core/get-started/technical-preview.md)
