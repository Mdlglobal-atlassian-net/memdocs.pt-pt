---
title: Configurar o inventário de software
titleSuffix: Configuration Manager
description: Configure o inventário de software e exclua pastas do inventário de software no Configurmanager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6fcf4736c30d8743d0d26b52aac60ef12b5c9cd
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906303"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Como configurar o inventário de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este procedimento configura as definições padrão do cliente para o inventário de software e aplica-se a todos os computadores da sua hierarquia. Se pretender aplicar estas definições apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-as a uma coleção. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte [como configurar as definições do cliente](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1. Na consola 'Gestor de Configuração', escolha as definições padrão do cliente de **'' ''' '',**  >  **Client Settings****configurações**padrão do cliente .    

2. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

3. Na caixa de diálogo **Definições Predefinidas,** escolha inventário de **software**.  

4. Na lista **Definições do Dispositivo** , configure os seguintes valores:  

   -   **Ativar o inventário** de software nos clientes - A partir da lista de drop-down, selecione **True**.  

   -   **Agendar o inventário de software e o calendário** de recolha de ficheiros - Configura o intervalo no qual os clientes recolhem inventário de software e ficheiros.   

5. Configure as definições de cliente de que necessita. A secção de inventário de [Software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) do artigo [sobre definições](../../../../core/clients/deploy/about-client-settings.md) do cliente tem uma lista das definições do cliente.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Como gerir os clientes.](../../../../core/clients/manage/manage-clients.md)  

   > [!TIP]
   >   Código de erro 80041006 em inventárioprovider.log significa que o fornecedor wMI está fora de memória. Ou seja, o limite de quota de memória para um fornecedor foi atingido e o fornecedor de inventário não pode continuar.
   > Neste caso, o agente de inventário cria um relatório com 0 entradas para que não sejam reportados itens de inventário. <br/>
   > Uma solução possível para este erro seria reduzir o âmbito da recolha de inventário de software. Em circunstâncias em que o erro ocorre após limitar o âmbito de inventário, o aumento da propriedade [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) definida na classe [_ProviderHostQuotaConfiguration](https://docs.microsoft.com/windows/win32/wmisdk/--providerhostquotaconfiguration) pode fornecer uma solução.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Excluir pastas do inventário de software  

1.  Utilizando o Notepad.exe, crie um ficheiro vazio designado **Skpswi.dat**.  

2.  Clique na direita no ficheiro **Skpswi.dat** e clique em **Propriedades**. Nas propriedades do ficheiro do ficheiro Skpswi.dat, selecione o atributo **Oculto** .  

3.  Coloque o ficheiro **Skpswi.dat** na raiz de cada unidade de disco rígido cliente ou estrutura de pasta que pretenda excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software só irá fazer de novo um inventário da unidade de cliente se este ficheiro for eliminado da unidade no computador cliente.
