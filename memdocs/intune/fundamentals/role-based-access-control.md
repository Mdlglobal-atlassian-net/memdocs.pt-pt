---
title: Controlo de acesso baseado em funções (RBAC) com microsoft Intune
description: Saiba como o RBAC permite controlar quem pode executar ações e fazer alterações no Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ca3de752-3caa-46a4-b4ed-ee9012ccae8e
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cb4631b31d33e53b6ef172f142735d24a5c3cb6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80220171"
---
# <a name="role-based-access-control-rbac-with-microsoft-intune"></a>Controlo de acesso baseado em funções (RBAC) com microsoft Intune

O controlo de acesso baseado em papéis (RBAC) ajuda-o a gerir quem tem acesso aos recursos da sua organização e o que pode fazer com esses recursos.  Ao [atribuir funções](assign-role.md) aos seus utilizadores Intune, pode limitar o que podem ver e alterar. Cada função tem um conjunto de permissões que determinam quais os utilizadores com essa função que podem aceder e alterar dentro da sua organização.

Para criar, editar ou atribuir funções, a sua conta tem de ter uma das seguintes permissões no Azure AD:
- **Administrador Global**
- **Administrador de Serviço Intune** (também conhecido como **Administrador Intune)**

Para conselhos e sugestões sobre intune RBAC, você pode conferir esta série de cinco vídeos que mostram exemplos e walkthroughs: [1](https://www.youtube.com/watch?v=5deXLMLcnKY), [2](https://www.youtube.com/watch?v=38dnMBLuxbQ), [3](https://www.youtube.com/watch?v=6vqg9cAkMbY), [4](https://www.youtube.com/watch?v=5yOLajFFMHE), [5](https://www.youtube.com/watch?v=P5DDvsSF4Wk).

## <a name="roles"></a>Funções
Uma função define o conjunto de permissões concedidas aos utilizadores atribuídos a essa função.
Você pode usar tanto os papéis incorporados como personalizados. Os papéis incorporados cobrem alguns cenários intune comuns. Pode [criar os seus próprios papéis personalizados](create-custom-role.md) com o conjunto exato de permissões de que necessita. Várias funções de Diretório Ativo Azure têm permissões para Intune.
Para ver um papel, escolha**Papéis** >  **Intune** > **Todos os papéis** > escolher um papel. Verá as seguintes páginas:

- **Propriedades**: O nome, descrição, tipo, atribuições e etiquetas de âmbito para o papel. 
- **Permissões**: Lista um longo conjunto de alternâncias que definem as permissões que o papel tem.
- **Atribuições**: Uma lista de atribuições de [funções]( assign-role.md) que definem quais os utilizadores têm acesso aos utilizadores/dispositivos. Um papel pode ter várias atribuições, e um utilizador pode estar em várias atribuições.

### <a name="built-in-roles"></a>Funções incorporadas
Pode atribuir funções incorporadas a grupos sem configuração adicional. Não é possível excluir ou editar o nome, descrição, tipo ou permissões de um papel incorporado.

- **Operador de Secretária**de Ajuda : Executa tarefas remotas em utilizadores e dispositivos e pode atribuir aplicações ou políticas a utilizadores ou dispositivos.
- **Policy and Profile Manager**: Gere a política de conformidade, perfis de configuração, inscrição da Apple, identificadores de dispositivos corporativos e linhas de base de segurança.
- **Operador Só de Leitura**: vê as informações do utilizador, do dispositivo, da inscrição, da configuração e da aplicação. Não posso fazer alterações ao Intune.
- **Gestor de Aplicações**: gere aplicações móveis e geridas, pode ler as informações do dispositivo e ver os perfis de configuração do dispositivo.
- Administrador de **funções intune**: Gere funções personalizadas intune e adiciona atribuições para funções intune incorporadas. É o único papel intune que pode atribuir permissões aos administradores.
- **Administrador escolar**: Gere os dispositivos Windows 10 em [Intune for Education](introduction-intune-education.md).
- **Endpoint Security Manager**: Gere funcionalidades de segurança e conformidade, tais como linhas de segurança, conformidade com dispositivos, acesso condicional e ATP do Microsoft Defender.

### <a name="custom-roles"></a>Funções personalizadas
Pode criar os seus próprios papéis com permissões personalizadas. Para mais informações sobre papéis personalizados, consulte [Criar um papel personalizado.](create-custom-role.md)

### <a name="azure-active-directory-roles-with-intune-access"></a>Funções de Diretório Ativo Azure com acesso Intune
| Papel de Diretório Ativo Azure | Todos os dados intune | Dados de auditoria insintonizados |
| --- | :---: | :---: |
| Administrador Global | Leitura/escrita | Leitura/escrita |
| Administrador de Serviços do Intune | Leitura/escrita | Leitura/escrita |
| Administrador de Acesso Condicional | Nenhuma | Nenhuma |
| Administrador de Segurança | Leia apenas (permissões administrativas completas para nó de segurança endpoint) | Só de leitura |
| Operador de Segurança | Só de leitura | Só de leitura |
| Leitor de Segurança | Só de leitura | Só de leitura |
| Administrador de Conformidade | Nenhuma | Só de leitura |
| Administrador de Dados de Conformidade | Nenhuma | Só de leitura |
| Leitor Global | Só de Leitura | Só de Leitura |

> [!TIP]
> Intune também mostra três extensões Azure AD: **Utilizadores**, **Grupos**, e **Acesso Condicional**, que são controlados usando O Azure AD RBAC. Além disso, o **Administrador da Conta de Utilizador** só executa as atividades do utilizador/grupo do AAD e não tem permissões completas para executar todas as atividades no Intune. Para mais informações, consulte [RBAC com Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles).

## <a name="role-assignments"></a>Atribuições de funções
Uma atribuição de funções define:

- que os utilizadores são atribuídos ao papel
- que recursos podem ver
- que recursos podem mudar.

Pode atribuir aos seus utilizadores funções personalizadas e incorporadas. Para ser atribuída uma função Intune, o utilizador deve ter uma licença Intune.
Para ver uma atribuição de papéis, escolha**Papéis** >  **Intune** > **Todos os papéis** > escolher um papel > escolher uma atribuição. Verá as seguintes páginas:

- **Propriedades**: O nome, descrição, função, membros, âmbitos e etiquetas da atribuição.
- **Membros**: Todos os utilizadores dos grupos de segurança Azure listados têm permissão para gerir os utilizadores/dispositivos listados no Scope (Grupos).
- **Âmbito (Grupos)**: Todos os utilizadores/dispositivos destes grupos de segurança Azure podem ser geridos pelos utilizadores em Membros.
- **[Âmbito (Etiquetas)](scope-tags.md)**: Os utilizadores dos Membros podem ver os recursos que têm as mesmas etiquetas de âmbito.

### <a name="multiple-role-assignments"></a>Atribuições de múltiplos papéis
Se um utilizador tiver múltiplas atribuições de funções, permissões e etiquetas de âmbito, essas atribuições de funções estendem-se a diferentes objetos da seguinte forma:

- Atribua permissões e etiquetas de âmbito apenas se aplicam aos objetos (como políticas ou aplicações) no âmbito de atribuição dessa função (Grupos). As permissões de atribuição e etiquetas de âmbito não se aplicam a objetos em outras atribuições de funções, a menos que a outra atribuição os conceda especificamente.
- Outras permissões (como Criar, Ler, Atualizar, Excluir) e etiquetas de âmbito aplicam-se a todos os objetos do mesmo tipo (como todas as políticas ou todas as aplicações) em qualquer uma das atribuições do utilizador.
- Permissões e etiquetas de âmbito para objetos de diferentes tipos (como políticas ou aplicações), não se aplicam entre si. A Read permission for a policy, por exemplo, não fornece uma permissão de Leitura para apps nas atribuições do utilizador.

## <a name="next-steps"></a>Passos seguintes
- [Atribuir uma função a um utilizador](assign-role.md)
- [Criar uma função personalizada](create-custom-role.md)
