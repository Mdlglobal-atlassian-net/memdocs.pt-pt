---
title: Visão geral dos cenários orientados
titleSuffix: Microsoft Intune
description: Conheça os cenários guiados intune disponíveis no portal de Gestão de Dispositivos Microsoft 365.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa70d5881a60d159ca668751ab2e1de9cf0cbd07
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076106"
---
# <a name="intune-guided-scenarios-overview"></a>Visão geral dos cenários guiados insinados 

Um cenário guiado é uma série personalizada de passos centrados em torno de um caso de uso de ponta a ponta. Os cenários comuns baseiam-se no papel que um administrador, utilizador ou dispositivo desempenha na sua organização. Estas funções normalmente requerem uma coleção de perfis cuidadosamente orquestrados, configurações, aplicações e controlos de segurança para fornecer a melhor experiência e segurança do utilizador.    

Se não estiver familiarizado com todos os passos e recursos necessários para implementar um determinado cenário Intune, os cenários guiados podem ser usados como ponto de partida. O cenário guiado reunirá automaticamente políticas, apps, atribuições e outras configurações de gestão. Além disso, os cenários guiados podem deliberadamente omiti-lo certas opções não aplicáveis ou incomuns para o cenário determinado. 

Os cenários guiados não são um espaço de gestão diferente dos fluxos de trabalho normais de Intune. Estes fluxos de trabalho destinam-se a ser utilizados em conjunto com os fluxos de trabalho existentes da Intune para perfis, apps e políticas. Ao completar um cenário orientado, toda a gestão futura do cenário deve ter lugar nos menus existentes para políticas, apps e perfis. Um cenário guiado não salva um tipo de recurso "guiado" nem acompanha futuras alterações feitas aos recursos. Todos os recursos criados por um cenário guiado aparecerão na sua respetiva carga de trabalho. Todas as opções, mesmo as opções omitidas no cenário guiado, estarão disponíveis para edição nos menus existentes.  

## <a name="types-of-guided-scenarios"></a>Tipos de cenários guiados 

Por uma questão de simplicidade, todos os cenários guiados omitem a deteção complexa apresenta tais Tags de Âmbito, grupos de exclusão e atribuições de grupo sinuosos. Todos os recursos criados por um cenário guiado herdarão todas as etiquetas de âmbito do administrador que completam o cenário. Certos cenários oferecem algum nível de personalização para uma configuração comum para cobrir cenários intimamente relacionados. Estes cenários, a atribuição de grupos de apoio apenas a grupos de inclusão. Para outros cenários guiados, todo o cenário garante uma experiência consistente, não oferecendo personalização e gera automaticamente um novo grupo para receber todas as atribuições. Uma vez que o cenário guiado esteja concluído, você é livre de usar tarefas mais sofisticadas diretamente através de trabalhos de política, app e perfil existentes.  

Os seguintes cenários são guiados: 
- Implementar microsoft edge para celular 
- Experimente um PC gerido pela nuvem
- Secure Microsoft Office para celular 

## <a name="guided-scenario-functionality"></a>Funcionalidade de cenário guiado 

Os cenários guiados oferecem uma funcionalidade específica. Os seguintes detalhes ajudam a explicar o que pode e não pode fazer enquanto segue um cenário guiado.

### <a name="launching"></a>Lançamento  

Todos os cenários guiados estão disponíveis no portal > de **[Gestão](https://endpoint.microsoft.com)** de Dispositivos**Resolução de Problemas + suporte** > **cenários guiados**. 

O cenário guiado começa com uma introdução explicando o propósito do cenário e quaisquer pré-requisitos necessários para completar a configuração. Neste ponto, as suas permissões de administração são verificadas para verificar se tem todos os privilégios necessários para completar o cenário.  

Depois de passar em verificações pré-requisitos, o cenário oferece configurações adequadas para personalização. Os cenários guiados visam apenas exigir entrada para o número mínimo de configurações e ocultar configurações incomuns ou avançadas até que seja necessário, ou com base em circunstâncias especiais. Cada cenário guiado liga-se à documentação que fornece detalhes adicionais. 

Depois de todas as configurações obrigatórias serem inseridas, o cenário guiado apresenta um resumo das definições introduzidas e os recursos que o cenário requer. Neste momento, nada foi salvo a menos que se note explicitamente.

O próximo passo é implementar o cenário. A implementação de um cenário cria e poupa todos os recursos necessários e configurações selecionadas. O tempo que leva para completar uma implantação varia de acordo com o cenário. Uma vez concluída a implantação, o cenário guiado apresenta uma lista dos recursos criados com ligações à visão de gestão de cada recurso, à carga de trabalho normal do recurso e à documentação. 

> [!IMPORTANT]
> A lista apresentada no final do cenário guiado não é guardada e só é visível enquanto o cenário guiado está aberto.  
Se houver um erro de implementação do cenário, todas as alterações serão revertidas. 

### <a name="editing"></a>Editar 

Os cenários guiados não podem ser utilizados para editar os recursos existentes. Uma vez criados, todos os recursos, grupos e atribuições devem ser editados utilizando as cargas de trabalho existentes.

### <a name="monitoring"></a>Monitorização 

Os cenários guiados não podem ser utilizados para monitorizar os recursos existentes, para além do processo inicial de criação. Uma vez criados, todos os recursos, grupos e atribuições devem ser monitorizados utilizando as cargas de trabalho existentes. 

### <a name="retiring"></a>Aposentação 

Os cenários guiados não podem ser utilizados para retirar os recursos existentes, para além da limpeza automatizada durante um erro na implementação inicial. Uma vez criados, todos os recursos, grupos e atribuições devem ser retirados utilizando as cargas de trabalho existentes. 

### <a name="updating"></a>Atualização

À medida que a tecnologia evolui, Intune pode atualizar de vez em quando um cenário guiado para melhorar a experiência do utilizador, segurança ou outros aspetos do cenário. Esta atualização só afetará novas implementações feitas pelo cenário guiado. A Intune não atualizará os recursos existentes anteriormente gerados pelo cenário guiado para corresponder às novas boas práticas ou recomendações.  

## <a name="next-steps"></a>Passos seguintes

Para começar a correr rapidamente no Microsoft Intune, passe pelos cenários guiados do Intune. Se você é novo em Intune, instale o seu inquilino Intune seguindo o início rápido do [teste gratuito](free-trial-sign-up.md).
