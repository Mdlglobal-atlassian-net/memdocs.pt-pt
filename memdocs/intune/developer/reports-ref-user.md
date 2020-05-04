---
title: Utilizador – Armazém de Dados do Intune
titleSuffix: Microsoft Intune
description: Tópico de referência para a categoria User das coleções de entidades na API do Armazém de Dados do Intune.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: C29A6EEA-72B7-427E-9601-E05B408F3BB0
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: b2bb18415cbebcef98ba6a7015872467c13eb231
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325569"
---
# <a name="reference-for-user-entity"></a>Referência para entidade utilizadora

A categoria **Utilizadores** contém a entidade **utilizadora** que define as propriedades dos utilizadores no modelo de dados.

## <a name="users"></a>utilizadores

A entidade **user** lista todos os utilizadores do Azure Active Directory (Azure AD) com licenças atribuídas na sua empresa.

A recolha da entidade **utilizadora** contém dados do utilizador. Estes registos incluem estados do utilizador durante o período de recolha dos dados, mesmo que o utilizador tenha sido removido. Por exemplo, um utilizador pode ser adicionado ao Intune e, em seguida, removido no decorrer do mês anterior. Apesar de este utilizador não estar presente no momento do relatório, o utilizador e o estado estão presentes nos dados do mês anterior. Pode criar um relatório que mostrará a duração da presença no histórico do utilizador nos seus dados.

|          Propriedade          |                                                                                                           Descrição                                                                                                          |                Exemplo               |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|
| userKey                    | Identificador exclusivo do utilizador no armazém de dados – chave de substituição.                                                                                                                                                         | 123                                  |
| userId                     | Identificador exclusivo do utilizador – semelhante a UserKey, mas é uma chave natural.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | Endereço de e-mail do utilizador.                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | O nome principal do utilizador.                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Nome a apresentar do utilizador.                                                                                                                                                                                                      | John                                 |
| intuneLicenciado             | Especifica se este utilizador tem ou não licença do Intune.                                                                                                                                                                              | Verdadeiro/Falso                           |
| isDeleted                  | Indica se todas as licenças do utilizador expiraram e se o utilizador foi, por conseguinte, removido do Intune. Para um único registo, este sinalizador não se altera. Em vez disso, é criado um novo registo para um novo estado do utilizador. | Verdadeiro/Falso                           |
| RowLastModifiedDateTimeUTC | Data e hora em UTC quando o registo foi modificado pela última vez no armazém de dados                                                                                                                                                 | 11/23/2016 0:00                      |


## <a name="next-steps"></a>Passos seguintes
- Pode utilizar a coleção de entidades **Utilizador Atual** para limitar os dados do utilizador aos utilizadores que estão atualmente ativos. Para obter mais informações, veja [Referência para a entidade do utilizador atual](reports-ref-data-model.md).
- Para saber mais sobre como o armazém de dados controla a duração de um utilizador no Intune, veja [Representação da duração do utilizador no Armazém de Dados do Intune](reports-ref-user-timeline.md).
