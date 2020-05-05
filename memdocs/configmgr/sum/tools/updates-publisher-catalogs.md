---
title: Gerir catálogos de atualizações
titleSuffix: Configuration Manager
description: Gerir catálogos de atualizações de software para System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717770"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gerir catálogos de atualizações de software na Editora updates

*Aplica-se a: System Center Updates Publisher*

Utilize o **Workspace** dos **Catálogos** para gerir catálogos de atualizações de software. Isto inclui a adição de novos catálogos, a gestão de subscrições de catálogos existentes e a importação de informações sobre as atualizações de um catálogo para o repositório updates Publisher.

Os catálogos de atualizações de software contêm informações sobre atualizações relacionadas que são criadas por outras organizações que não a Microsoft. Outras organizações incluem a sua própria organização e fornecedores de software de terceiros que registaram os seus catálogos com a Microsoft. Os catálogos registados de fornecedores de software são *chamados catálogos de parceiros.* Os catálogos que cria, e que não estão registados na Microsoft, são chamados catálogos de *utilizadores.*

## <a name="add-software-update-catalogs"></a>Adicionar catálogos de atualizações de software
Tem de adicionar um catálogo de atualizações ao Updates Publisher antes de poder gerir as atualizações que contém. Quando adiciona um catálogo, atualiza o Editor:
-   Cria uma subscrição desse catálogo, para que possa verificar as atualizações para esse catálogo.
-   Adiciona o catálogo a uma lista na janela **My Software Update Catalogs** do **Workspace catálogos**.  

Informações sobre cada catálogo subscrito estão disponíveis na consola. As informações incluem o URL de descarregamento ou localização, o nome da empresa ou organização que criou o catálogo, e quando foi importado ou modificado pela última vez.

Atualizações O Editor pode verificar automaticamente as suas subscrições para obter alterações sempre que começar. Isto está configurado como uma [opção Avançada.](updates-publisher-options.md#advanced) Quando configurado, o Updates Publisher refere o URL de descarregamento ou informações de localização para a subscrição e alerta-o quando há alterações no catálogo que foram feitas desde a última vez que o importapara o repositório.

Para verificar manualmente se há uma atualização do catálogo, selecione o catálogo da lista de **Catálogos my Software Update** e, em seguida, escolha **Refresh** a partir da fita.

Além de adicionar catálogos e visualizar informações sobre catálogos subscritos, pode:
-  **Editar** informações para catálogos de *utilizadores.*
-  **Eliminar** (remover) um catálogo da Atualizações Publisher.
-  **Importa** atualizações de um catálogo para o repositório updates Publisher. Quando importa atualizações, importa todas as atualizações contidas nesse catálogo. Pode então visualizar as atualizações no espaço de trabalho das Atualizações, onde poderá selecionar e publicar atualizações no seu servidor de atualizações.

> [!NOTE]   
> A eliminar um catálogo da Updates Publisher resulta nas atualizações desse catálogo a serem removidas do seu repositório. Isto não afeta as atualizações que publicou no seu servidor de atualização. Para remover atualizações do seu servidor de atualização que já não se encontram no seu repositório, consulte as atualizações de [software não referenciadas expiradas](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gerir catálogos de atualizações
Pode ver os catálogos da lista que importou na janela **My Software Update Catalogs** do **Workspace catalogs**. Deste espaço de trabalho pode:

-   **Adicione um catálogo de parceiros:** Utilize um dos seguintes catálogos para encontrar novos catálogos de parceiros:

    -   Na consola, vá a **Atualizações Workspace** > **Overview**. Na janela **Getting Started,** escolha **Adicionar Catálogos**de Atualizações de Software do Parceiro .

    -   Na consola, vá ao Workspace > My **Catalogs.****My Catalogs** Em seguida, a partir da fita, escolha **Adicionar Catálogos**.

-   **Adicione um catálogo** de utilizadores: Na consola, vá ao Workspace > My **Catalogs.****My Catalogs** Em seguida, a partir da fita, escolha **Adicionar Catálogos**. Além da localização do ficheiro .cab, deve especificar um Editor, Nome e Descrição para identificar o catálogo.


-   **Verifique as atualizações para os catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **Refresh** a partir da fita.

-   **Editar um catálogo de utilizadores:** Selecione um catálogo de *utilizadores* e, em seguida, escolha **editar** a partir da fita. Em seguida, pode modificar as propriedades definidas pelo utilizador.

-   **Eliminar catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **Remover** da fita. Isto remove o catálogo, a sua subscrição e as atualizações desses catálogos do seu repositório Updates Publisher.

-   **Adicione atualizações de um catálogo ao seu repositório**: Escolha **importar** a partir da fita para iniciar o assistente do **Catálogo de Importação.** Para mais informações, consulte [as atualizações de Importação](#import-updates)

## <a name="import-updates"></a>Atualizações de importação
Ao importar um catálogo, o Updates Manager adiciona as atualizações desse catálogo ao repositório updates Publisher. Depois de importadas as atualizações, pode publicá-las no seu servidor de atualização para disponibilizá-las a dispositivos geridos.

### <a name="to-import-updates"></a>Para importar atualizações
1. Para iniciar o assistente do **Catálogo de Importação,** escolha **importar** a partir da fita num dos seguintes espaços de trabalho:

   -   Espaço de trabalho de catálogos

   -   Atualizações Espaço de Trabalho

2. Na página **'Import Type',** selecione um ou mais catálogos adicionados ao Updates Publisher ou especifique um caminho para um catálogo que ainda não tenha adicionado como subscrição. Escolha **Next** para ver o ecrã resumo, e quando estiver pronto, escolha **Next** para iniciar a importação.

3. No **Aviso de Segurança –** Janela de Validação do Catálogo, reveja o certificado de catálogo e, quando estiver pronto, optou por **aceitar** importar as atualizações.

   > [!CAUTION]
   > Aceite atualizações apenas de editores em quem confia. As atualizações de software de editores que não são de confiança podem potencialmente prejudicar os computadores dos clientes ao pesquisar em atualizações.
   > 
   >  Se já não confia numa editora, retire essa editora da lista de editores de confiança. Para mais informações sobre a aceitação de catálogos, clique em **Tell Me More** na caixa de diálogo de validação de **catálogo.**

   Se optar por aceitar sempre catálogos de uma editora, essa editora é adicionada à lista de [editores fidedignos.](updates-publisher-options.md#trusted-publishers) Pode rever e editar esta lista como uma opção Updates Publisher.

4. A importação ignora a importação de uma atualização quando a atualização já se encontra no repositório e uma das seguintes é verdadeira:

   -   A atualização mantém-se inalterada desde a última vez que foi importada.

   -   A atualização foi editada e tem um novo hash digital. Editar uma atualização impede que uma nova atualização sobreaprete o original, pois isso substituiria as alterações que poderia ter implementado.

5. Na página de **confirmação,** reveja os resultados da importação.

6. Clique **perto** para completar o assistente. Pode agora ver as atualizações deste catálogo no Espaço de Trabalho de Atualizações.

## <a name="next-steps"></a>Passos seguintes
Depois de importar atualizações, as ações comuns incluem:
-   [Gerencie as atualizações](manage-updates-with-updates-publisher.md) para agregar, atribuir e implementá-las no seu servidor de atualização.
-   [Crie regras](updates-publisher-applicability-rules.md) de aplicabilidade para ajudar a determinar quando as atualizações se desdobram no seu servidor de atualizações.
