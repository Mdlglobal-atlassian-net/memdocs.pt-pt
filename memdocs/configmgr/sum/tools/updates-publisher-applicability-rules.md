---
title: Regras de aplicabilidade
titleSuffix: Configuration Manager
description: Gerir regras de aplicabilidade para system center updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078435"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gerir regras de aplicabilidade na Editora de Atualizações

*Aplica-se a: System Center Updates Publisher*

Com atualizações Editora, as regras de aplicabilidade definem requisitos que devem ser cumpridos antes de um dispositivo poder instalar uma atualização. As regras também são usadas para determinar se o computador tem uma atualização instalada. Uma regra de aplicabilidade que é complexa com várias partes é referida como um conjunto de regras.

Os pacotes de atualização não utilizam regras de aplicabilidade.

## <a name="overview-of-applicability-rules"></a>Visão geral das regras de aplicabilidade
Gere regras de aplicabilidade a partir do Espaço de Trabalho das **Regras.** Quando se cria uma regra, está a especificar uma ou mais condições. When multiple conditions are specified, you can configure relationships between the conditions so they are evaluated sequentially or combined into logical **And** or **Or** statements.

Por exemplo, o seguinte é um conjunto de regras que contém três regras. A primeira regra verifica que o ficheiro *MyFile* existe, e a segunda e terceira regras verificam que o idioma do sistema operativo Windows é inglês ou japonês.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Todas as atualizações requerem pelo menos uma regra de aplicabilidade. As atualizações que importa já têm regras de aplicabilidade aplicadas, e quando cria as suas próprias atualizações, tem de lhes adicionar uma ou mais regras. Pode modificar e expandir as regras para qualquer atualização em Updates Publisher.

Para ver as regras que criou, no Espaço de Trabalho das **Regras,** selecione uma regra da lista de **regras guardadas** pela Minha. As condições individuais e as operações lógicas para esse ecrã de regras no painel de Regras de **Aplicabilidade** da consola. As regras para atualizações que importa só podem ser vistas e modificadas quando editar essa atualização.

Pode criar regras em dois locais em Updates Publisher:

-   No **Espaço de Trabalho das Regras,** cria-se e **guarda** conjuntos de regras que pode utilizar mais tarde. Ao editar ou criar uma atualização, pode selecionar a **regra Guardar** como tipo de **regra**, e, em seguida, selecionar a partir de uma lista dos seus conjuntos de regras pré-criados.

-   Também pode criar novas regras no momento em que cria ou edita uma atualização. As regras que cria desta forma não são guardadas para uso futuro.

## <a name="create-applicability-rule"></a>Criar regra de aplicabilidade
As seguintes informações são semelhantes à forma como cria regras a partir do [assistente de Atualização de Criação](create-updates-with-updates-publisher.md#use-the-create-update-wizard). Mas ao contrário do assistente, tem a opção de guardar os seus conjuntos de regras para uso futuro.

1. No espaço de **trabalho das regras,** escolha **Criar** para abrir o assistente de **criar regras.**

2. Especifique um nome para ![a](media/newrule.png)regra e, em seguida, clique em Nova Regra . Isto abre a página da Regra da **Aplicabilidade** onde pode configurar regras.

3. Para **o tipo de regra,** selecione um dos seguintes. As opções que deve configurar variam para cada tipo:

   - **Arquivo** – Utilize esta regra para exigir que um dispositivo tenha um ficheiro com propriedades que satisfaçam um ou mais critérios que especifique antes de esta atualização poder ser aplicada.

   - **Registo –** Utilize este tipo para especificar os detalhes do registo que devem estar presentes antes de um dispositivo se qualificar para instalar esta atualização.

   - **Sistema –** Esta regra utiliza detalhes do sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão Windows, um idioma Windows, arquitetura de processador, ou especificar uma consulta wmi para identificar o sistema operativo dos dispositivos.

   - **Instalador de Janelas –** Utilize este tipo de regra para determinar a aplicabilidade com base num instalado . Patch de MSI ou Instalador de Janelas (. MSP). Também pode determinar se componentes ou funcionalidades específicas são instalados como parte da exigência.

     > [!IMPORTANT]   
     > Em degelos geridos, o Windows Update Agent não consegue detetar pacotes de instalação do Windows que são instalados por utilizador. Quando utilizar este tipo de regra, configure regras adicionais de aplicabilidade, como versões de ficheiros ou valores-chave de registo, para que o pacote do Instalador do Windows possa ser devidamente detetado independentemente de uma base por utilizador ou por sistema.

   - **Regra guardada –** Esta opção permite encontrar e utilizar regras que configurae e guardou anteriormente.

4. Continue a adicionar e configurar regras adicionais conforme desejado.

5. Utilize os botões de funcionamento lógicos para encomendar e agrupar diferentes regras para criar controlos pré-requisitos mais complexos.

6. Quando o conjunto de regras estiver completo, clique em **OK** para salvá-lo. A regra agora aparece na lista de **regras guardadas.**

## <a name="edit-applicability-rule-sets"></a>Editar conjuntos de regras de aplicabilidade
Para editar uma regra de aplicabilidade, no **Espaço de Trabalho** de Regras selecione qualquer regra que seja guardada na lista de regras **guardadas** pela My e, em seguida, escolha **Editar** a partir da fita. Isto abre o assistente de regra de **edição.**

O assistente da Regra de **Edição** apresenta as regras atuais para o conjunto de regras. Edita regras da mesma forma que usa o assistente **de Criar Regra** para criar novas regras. Pode utilizar este assistente para renomear o conjunto de regras, eliminar regras, reordenar regras e relacionamentos ou adicionar novas regras.

Depois de fazer alterações, escolha **OK** para guardar as alterações e feche o assistente.

Para mais detalhes sobre a utilização do assistente de regras, consulte o **Passo 7,** a página de aplicabilidade, do [assistente Create Update](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminar regras de aplicabilidade
Para eliminar uma regra de aplicabilidade guardada, no **Espaço de Trabalho** de Regras selecione a regra ou regra definida na lista de regras **guardadas** pela Minha e, em seguida, escolha **Apagar** a partir da fita. Isto remove a regra ou regra guardada definida pela Atualizações editora.

Para eliminar uma regra de uma atualização específica, tem de [editar a atualização](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
