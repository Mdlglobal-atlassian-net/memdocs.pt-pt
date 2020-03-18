---
title: Impulsionar a adoção do utilizador final com acesso condicional
titleSuffix: Microsoft Intune
description: Aprenda a utilizar o Acesso Condicional para conduzir a inscrição no Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c2d7ce3f-fe97-4044-ad9e-25ac8fa301c9
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: da332528854af2b53879d30d6de90c927b49a889
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331209"
---
# <a name="drive-end-user-adoption-with-conditional-access-in-microsoft-intune"></a>Drive end-user adoção com acesso condicional no Microsoft Intune

Ativar funcionalidades de Acesso Condicional com Intune, como bloquear e-mails para dispositivos não matriculados, pode ajudar a impulsionar a inscrição e a conformidade, mas não são necessários para que uma migração seja bem sucedida. Os requisitos de segurança e os objetivos de adoção da migração devem determinar a taxa de êxito.

## <a name="migration-campaign-with-conditional-access"></a>Campanha de migração com Acesso Condicional

Aqui está uma abordagem típica para melhorar uma campanha de migração com Acesso Condicional:

1. Estabeleça regras de acesso condicional a aplicar a todos os utilizadores, mas especificamente excluir os utilizadores que necessitem de migrar do antigo fornecedor de MDM. Pode criar um grupo de utilizadores Azure AD com todos os utilizadores excluídos do Acesso Condicional.

2. À medida que os utilizadores migram, remova-os do grupo de exclusão de Acesso Condicional.

3. Após a migração estar concluída, configure todas as políticas de Acesso Condicional para bloquear por padrão, a menos que Intune permita o acesso.

### <a name="advantages"></a>Vantagens

- Concede o controlo de acesso a novas contas de utilizador que não foram geridas pela solução anterior.

- Concede um período de tolerância para os utilizadores da solução anterior migrarem.

- Minimiza a perda de produtividade.

### <a name="disadvantages"></a>Desvantagens

- Os utilizadores de solução anterior poderiam potencialmente aceder a recursos utilizando dispositivos não geridos até que o Acesso Condicional esteja ativado para esses utilizadores.


Esta é uma abordagem entre muitas. Pode escolher um processo mais simples que adiem todo o Acesso Condicional até que todas as fases tenham sido instruídas a inscrever-se, ou um processo mais rigoroso que impeque o Acesso Condicional desde o início e exija o pleno cumprimento de todos os acessos.

- Saiba mais sobre o [Acesso Condicional](../protect/conditional-access.md).

## <a name="task-list-for-conditional-access"></a>Lista de tarefas para acesso condicional

### <a name="task-1-decide-how-you-are-going-to-implement-conditional-access"></a>Tarefa 1: Decida como vai implementar o Acesso Condicional

[Formas comuns de utilizar o Acesso Condicional.](../protect/conditional-access-intune-common-ways-use.md)

### <a name="task-2-set-up-intune-conditional-access"></a>Tarefa 2: Configurar o acesso condicional intune

Escolha uma das seguintes opções:

- [Configure acesso condicional no Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

- [Instalar o conector do Exchange no local com o Intune](../protect/exchange-connector-install.md)

- [Configurar políticas de acesso condicional baseadas em aplicativos para o Exchange Online](../protect/app-based-conditional-access-intune-create.md)

- [Configurar políticas de acesso condicional baseadas em aplicativos para o SharePoint Online](../protect/app-based-conditional-access-intune-create.md)

- [Bloquear aplicações que não utilizam autenticação moderna (ADAL)](../protect/app-modern-authentication-block.md)

## <a name="next-steps"></a>Próximos passos

Saiba mais sobre o [ciclo de migração típico](migration-guide-cycle.md).
