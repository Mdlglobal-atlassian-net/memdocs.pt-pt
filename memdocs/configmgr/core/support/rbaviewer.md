---
title: Ferramenta de Administração baseada em funções
titleSuffix: Configuration Manager
description: Utilize a Ferramenta de Administração e Auditoria baseada em Funções para modelar e auditar funções e âmbitos de segurança no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723188"
---
# <a name="role-based-administration-and-auditing-tool"></a>Ferramenta de Administração e Auditoria Baseadas em Funções

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Ferramenta de Administração e Auditoria baseada em Funções é uma das ferramentas do Gestor de [Configuração.](tools.md) Utilize esta ferramenta para as seguintes tarefas:

- Funções de segurança do modelo com permissões específicas  

- Audite os âmbitos de segurança e as funções de segurança que outros utilizadores possuem



## <a name="requirements"></a>Requisitos

- Executa-o no mesmo computador que a consola do Gestor de Configuração  

- Tem o papel de **Administrador Completo,** **Analista de Leitura**ou Administrador de **Segurança**  

- Atribuir a sua conta ao âmbito de segurança **All** e todas as coleções  

- *(Opcional)* Para analisar a segurança da pasta de relatório, deve ter acesso SQL  

- *(Opcional)* Para analisar o relatório drill-through, execute esta ferramenta no servidor do sistema do site com a função ponto de reporte



## <a name="procedures"></a>Procedimentos


### <a name="model-permissions-for-a-new-role"></a>Autorizações de modelo para um novo papel

Utilize o seguinte procedimento para modelar permissões para um novo papel que pretende criar: 

1. Executar **RBAViewer.exe**.  

2. Selecione as funções de segurança base que pretende construir ou comece a partir de um conjunto de permissão vazia. Selecione as permissões necessárias.  

3. Clique em **Analisar** para ver a interface do utilizador que esta função personalizada verá.  

    > [!Note]  
    > Para ver se existe uma função de segurança existente que satisfaça os seus requisitos, mude para o separador **Similaridade.**  

4. Clique em **Exportar** para salvar o papel como ficheiro XML. Em seguida, importe-o para a consola Do Gestor de Configuração. Para mais informações, consulte [Criar funções de segurança personalizadas.](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)


### <a name="audit-existing-security-scopes"></a>Auditar os âmbitos de segurança existentes

Utilize o seguinte procedimento para auditar todos os utilizadores administrativos, coleções e âmbitos de segurança existentes no Gestor de Configuração:

1. Executar **RBAViewer.exe**.  

2. Selecione o botão **AUDIT RBA** na barra de ferramentas.  

    1. Para ver as relações limitadas de recolha numa vista para a árvore, mude para o separador Resumo da **Coleção.**  

    2. Para visualizar objetos atribuídos a uma função de segurança, mude para o separador **Resumo** scope.  


### <a name="audit-a-specific-user"></a>Auditar um utilizador específico

Utilize o seguinte procedimento para auditar a configuração de administração baseada em funções para um utilizador específico:

1. Executar **RBAViewer.exe**.  

2. Selecione o botão **Executar As** na barra de ferramentas.  

3. Insera o nome de utilizador específico para verificar as permissões dessa conta.  

4. A ferramenta apresenta as funções de segurança atribuídas ao utilizador ou ao grupo de segurança a que o utilizador pertence. Também exibe os objetos que este utilizador pode ver e as ações que pode tomar na consola.  



## <a name="see-also"></a>Consulte também

- [Noções básicas sobre a administração baseada em funções](../understand/fundamentals-of-role-based-administration.md)
- [Configurar a administração baseada em funções](../servers/deploy/configure/configure-role-based-administration.md)
