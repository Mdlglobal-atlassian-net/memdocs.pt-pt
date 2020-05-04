---
title: Configurar o estado do cliente
titleSuffix: Configuration Manager
description: Selecione as definições de estado do cliente no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713577"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Como configurar o estado do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de poder monitorizar o estado do cliente do Gestor de Configuração e corrigir os problemas que são encontrados, tem de configurar o seu site para especificar os parâmetros que são utilizados para marcar os clientes como opções inativas e configuradas para o alertar se a atividade do cliente ficar abaixo de um limiar especificado. Também pode desativar os computadores de remediar automaticamente quaisquer problemas que o estado do cliente encontre.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a>Para configurar o estado do cliente  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  No espaço de trabalho **de Monitorização,** clique no **Estado do Cliente,** então, no separador **Casa,** no grupo Estado do **Cliente,** clique em **Definições**de Estado do Cliente .  

3.  Na caixa de diálogo de definições de estado do **cliente,** especifique os seguintes valores para determinar a atividade do cliente:  

    > [!NOTE]  
    >  Se nenhuma das configurações for satisfeita, o cliente será marcado como inativo.  

    -   Pedidos de **política do cliente durante os dias seguintes:** Especifique o número de dias desde que um cliente solicitou a apólice. O valor predefinido é **7** dias.  

    -   **Descoberta do batimento cardíaco durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de descoberta de batimentos cardíacos para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de hardware durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de hardware para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de software durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de software para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Mensagens de estado durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou mensagens de estado para a base de dados do site. O valor predefinido é **7** dias.  

4.  Na caixa de diálogo de definições de estado do **cliente,** especifique o seguinte valor para determinar quanto tempo os dados do histórico do estado do cliente são retidos:  

    -   **Mantenha o histórico de estado do cliente durante o seguinte número de dias:** Especifique quanto tempo pretende que o histórico do estado do cliente permaneça na base de dados do site. O valor padrão é de **31** dias.  

5.  Clique **em OK** para guardar as propriedades e para fechar a caixa de diálogo de definições de estado do cliente **Propriedades.**  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a>Para configurar a Agenda para o Estatuto do Cliente  

1.  Na consola 'Gestor de Configuração', clique em **Monitorização**.  

2.  No espaço de trabalho **de Monitorização,** clique no **Estado do Cliente,** então, no separador **Casa,** no grupo Estado do **Cliente,** clique em **Agendar a Atualização do Estado do Cliente**.  

3.  Na caixa de diálogo **'Agendar Estado do Cliente',** configure o intervalo em que pretende que o estado do cliente atualize e, em seguida, clique em OK.  

    > [!NOTE]  
    >  Quando alterar a programação para atualizações do estado do cliente, a atualização só entrará em vigor na próxima atualização de estado do cliente agendada (para a programação previamente configurada).  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a>Para configurar alertas para o estado do cliente  

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3. Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

   > [!NOTE]  
   >  Não é possível configurar alertas de coleções de utilizadores.  

4. No separador **Alertas** da**Properties** **Add** <em> &lt;\></em>caixa de diálogo Nome Properties de recolha, clique em Adicionar .  

   > [!NOTE]  
   >  O separador **Alertas** só está visível se a função de segurança a que o utilizador está associado tiver permissões para alertas.  

5. Na caixa de diálogo **Adicionar Novos Alertas da Coleção** , escolha os alertas que pretende que sejam gerados quando os limites do estado do cliente são inferiores a um valor específico e, em seguida, clique em **OK**.  

6. Na lista **Condições** do separador **Alertas** , selecione cada um dos alertas do estado do cliente e especifique as informações seguintes.  

   -   **Nome do alerta** - Aceite o nome predefinido ou introduza um novo nome para o alerta.  

   -   **Severidade de alerta** - A partir da lista de lançamentos, escolha o nível de alerta que será exibido na consola Do Gestor de Configuração.  

   -   **Aumentar o alerta** - Especifique a percentagem de limiar para o alerta.  

7. Clique **em OK** para fechar a <em> &lt;\></em>caixa de diálogo Name**Properties.**  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a>Excluir computadores da reparação automática  

1. Abra o editor de registo no computador cliente para o qual pretende desativar a reparação automática.  

   > [!WARNING]  
   >  Se utilizar incorretamente o Editor de Registo, poderá causar problemas graves que podem exigir que reinstale o seu sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

2. Navegue para **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3. Insira um dos seguintes valores para esta chave de registo:  

   -   **Verdade** - O computador cliente não irá remediar automaticamente quaisquer problemas que sejam encontrados. No entanto, ainda será alertado no espaço de trabalho **de Monitorização** sobre quaisquer problemas com este cliente.  

   -   **Falso** - O computador cliente irá automaticamente remediar os problemas quando estes forem encontrados e será alertado no espaço de trabalho **de Monitorização.** Esta é a predefinição.  

4. Feche o editor de registo.  

   Também pode instalar clientes utilizando a propriedade de instalação CCMSetup **NotifyOnly** para os excluir da reparação automática. Para mais informações sobre esta propriedade de instalação de cliente, consulte sobre as propriedades de [instalação do cliente.](../../../core/clients/deploy/about-client-installation-properties.md)  
