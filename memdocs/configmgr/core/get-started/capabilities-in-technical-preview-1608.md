---
title: Capacidades na Pré-visualização Técnica 1608
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074185"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1608 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1608. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas  
O passo do Cliente Prepare ConfigMgr irá agora remover completamente o cliente do Gestor de Configuração, em vez de apenas remover informações chave. Quando a sequência de tarefas implementar a imagem do sistema operativo capturado, instalará sempre um novo cliente do Gestor de Configuração.  


## <a name="improvements-to-software-center"></a>Melhorias no Centro de Software
* Os **separadores**de Software Center, **Updates**e **Sistemas Operativos** mostram agora que software foi recentemente adicionado. Os números no painel de navegação mostram quantas novas peças de software estão em cada separador.
* Os utilizadores podem agora solicitar a aprovação de aplicações e, em seguida, ver o histórico de pedidos na visão de Detalhes da **Aplicação** no Centro de Software. O botão **Request** em Detalhes de **Aplicação** já não redireciona para o Catálogo de Aplicações baseado na Web.

## <a name="improvements-to-asset-intelligence"></a>Melhorias na Inteligência de Ativos
Adicionámos um campo às propriedades do software inventariado que permite definir uma relação entre pais e filhos com outro software. Na lista de Software Inventariado, pode então ver o pai de qualquer software e também esconder todo o software infantil.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar um relacionamento entre pais e filhos
  1. Para definir o software dos pais, no nó de Software Inventariado, clique à direita num item de software na lista **de Software Inventariado** e escolha **Propriedades**.
  2. Na caixa de diálogo que se abre, selecione o software que pretende definir como o software-mãe para a sua seleção inicial.

### <a name="filter-the-software-display"></a>Filtrar o ecrã do software
Depois de definir as relações entre pais e filhos, pode filtrar a sua visão apenas para mostrar software que é pai ou que não tem relação definida. Isto esconde todo o software que é definido como uma criança de outro software inventariado. Para tal:
   1. Para a barra de pesquisa, escolha **adicionar critérios**
   2. Selecione **O Software dos Pais** e, em seguida, altere o valor dos critérios para que esteja **vazio**e, em seguida, clique em **Procurar**.

O ecrã mostra agora apenas os itens de software dos pais, ou software que não tem relações definidas. O software que é apenas uma criança de outro título não é exibido.

## <a name="remote-control-keyboard-translation"></a>Tradução de teclado de controlo remoto
No passado, o Gestor de Configuração transmitiu a posição chave da localização do espectador para a localização do participante. Isto era problemático para configurações de teclado que diferem de espectador para compartilhista. Por exemplo, um espectador com um teclado inglês escreveria um "A", mas o teclado francês do comum forneceria um "Q". Estamos a mudar o comportamento padrão para que o personagem em si seja transmitido do teclado do espectador para o comedor, e o que o espectador pretende escrever chega ao comum.

Este comportamento pode ser desligado pelo espectador se preferir escrever de acordo com o arranjo de teclado do comum. Para alterar o comportamento, no Controlo Remoto do Gestor de **Configuração,** escolha **Ação**e escolha **a tradução do teclado Para** transmitir a posição chave.

> [!NOTE]
>
> Chaves especiais, tais como ~!#@$, não serão traduzidas corretamente.
