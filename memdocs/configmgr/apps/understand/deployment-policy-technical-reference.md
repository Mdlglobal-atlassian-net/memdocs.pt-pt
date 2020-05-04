---
title: Referência técnica da política de implementação de aplicações
titleSuffix: Configuration Manager
description: Resolução de problemas de políticas de implementação de aplicações de referência técnica para Gestor de Configuração.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709790"
---
# <a name="application-deployment-policy"></a>Política de Implementação de Aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

## <a name="policy-creation"></a>Criação política

Quando se implementa uma aplicação, é criada uma instância de [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) classe que representa a atribuição de uma aplicação a uma coleção. Esta atividade pode ser rastreada no **sMSProv.log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

Na base de dados do Gestor de `CI_CIAssignments` Configuração, esta informação é armazenada na tabela onde `AssignmentType` 2 representa uma implementação de aplicação. Quando a atribuição é criada, o componente SMS Database Monitor deteta uma alteração na tabela e, em seguida, notifica o Gestor de Replicação de Objetos para processar a política de atribuição de CI (CIA). O componente do Gestor de Replicação de Objetos cria então `Policy` a política para a atribuição de aplicações na base de dados, que está armazenada na tabela na base de dados, e o ID de Política baseia-se no ID exclusivo da aplicação. Esta atividade pode ser rastreada no **objreplmgr.log,** referindo-se ao ID Exclusivo de Atribuição, que pode ser obtido a partir da consulta SQL referenciada na secção [Antes de Começar.](app-deployment-technical-reference.md#before-you-begin)

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

A política para a atribuição de candidaturas pode ser vista na base de dados utilizando uma consulta SQL semelhante à abaixo.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Orientação política

Após a geração da política, a componente Policy Provider atribui esta política aos recursos da recolha que é alvo da implementação da aplicação. A informação de orientação `ResPolicyMap` política está armazenada na tabela na base de dados. Pode utilizar o PADBID devolvido pela consulta acima para acompanhar esta atividade em **policypv.log**. No entanto, o PADBID registado no registo pode nem sempre corresponder ao PADBID devolvido pela consulta acima referida se várias políticas forem processadas simultaneamente.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap`o quadro não contém qualquer informação de orientação para aplicações que sejam implementadas como **Disponíveis** nas coleções do Utilizador. O Software Center questiona uma lista destas aplicações do Ponto de Gestão, e a informação de orientação política para estas aplicações é gerada dinamicamente quando um utilizador solicita uma aplicação do Software Center.

## <a name="next-steps"></a>Passos Seguintes

- [Implementação de aplicações para coleções de dispositivos](device-deployment-technical-reference.md)
- [Implementação de aplicações para coleções de utilizadores](user-deployment-technical-reference.md)
