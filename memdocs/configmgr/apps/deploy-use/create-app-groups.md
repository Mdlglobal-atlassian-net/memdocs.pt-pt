---
title: Criar grupos de aplicações
titleSuffix: Configuration Manager
description: Crie um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação no Gestor de Configuração.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643120"
---
# <a name="create-application-groups"></a>Criar grupos de aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3555907-->

A partir da versão 1906, criar um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação. Os metadados que especifica sobre o grupo de aplicações são vistos no Software Center como uma única entidade. Pode encomendar as aplicações no grupo para que o cliente as instale numa encomenda específica.

> [!Note]  
> Nesta versão do 'Gestor de Configuração', os grupos de aplicações são uma funcionalidade de pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../core/servers/manage/pre-release-features.md).  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **a Gestão** de Aplicações e selecionar o nó **do Grupo de Aplicação.**  

1. No grupo Criar na fita, selecione **Create Application Group**.

1. Na página **Informação Geral,** especifique informações sobre o grupo de aplicações.  

1. Na página do Centro de **Software,** inclua informações que mostram no Software Center.  

1. Na página do **Grupo de Aplicação,** selecione **Adicionar**. Selecione uma ou mais aplicações para este grupo. Reordene-os usando as ações **move up** e **move down.**  

1. Conclua o assistente.  

Implementar o grupo de aplicações utilizando o mesmo processo que para uma aplicação. Para mais informações, consulte [aplicações de implementação](deploy-applications.md). A partir da versão 1910, pode implementar um grupo de aplicações para dispositivos ou coleções de utilizadores.

Depois de implantar o grupo:

- Se adicionar uma nova aplicação ao grupo, tem de distribuir separadamente o novo conteúdo da aplicação para pontos de distribuição.

- Se modificar uma aplicação no grupo de aplicações, redistribua o conteúdo.

Para resolver problemas com uma implementação de grupo de aplicações, utilize os seguintes ficheiros de registo no cliente:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **DefiniçõesAgente.log**

> [!Important]  
> Não crie ou implemente um grupo de aplicações até atualizar toda a hierarquia e clientes direcionados para pelo menos a versão 1906.

### <a name="known-issues"></a>Problemas conhecidos

- *Versão 1906*: As aplicações no grupo só podem conter tipos de implementação do **Instalador do Windows** ou do **Script.**
  - *Versão 1906*: Desnove o comportamento de instalação do tipo de implementação para **instalar para o sistema**.
- As seguintes opções de implantação podem não funcionar: alertas, aprovação, implantação faseada, reparação.
- Não pode exportar ou importar grupos de aplicações.
- Não inclua no grupo quaisquer aplicações que exijam o reinício, ou a implementação do grupo pode falhar.
- *Versão 1906*: Não pode implantar o grupo de aplicações numa coleção de utilizadores.
- *Versão 1906*: Os utilizadores não podem **desinstalar** o grupo de aplicações no Software Center.
- Se eliminar uma aplicação que faça parte de um grupo de aplicações, verá o seguinte aviso quando vir as propriedades do grupo de aplicações: "Incapaz de carregar informações sobre todas as aplicações do grupo." Faça uma simples alteração no grupo de aplicações e guarde-a. Por exemplo, adicione um espaço aos comentários do **Administrador**. Quando guarda a alteração, remove a aplicação eliminada do grupo.<!-- 7099542 -->
