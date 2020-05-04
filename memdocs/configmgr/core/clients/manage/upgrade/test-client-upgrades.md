---
title: Teste de atualizações de clientes antes da produção
titleSuffix: Configuration Manager
description: Teste as atualizações do cliente numa coleção de pré-produção no Gestor de Configuração.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715411"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Como testar as atualizações do cliente numa coleção de pré-produção no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode testar uma nova versão cliente do Gestor de Configuração numa coleção de pré-produção antes de atualizar o resto do site com o mesmo.  Quando o fizer, apenas os dispositivos que fazem parte da recolha de testes são atualizados. Uma vez que tenha tido a oportunidade de testar o cliente, pode promover o cliente, o que disponibiliza a nova versão do software do cliente para o resto do site.

> [!NOTE]
> Para promover um cliente de teste à produção, deve ser registado como utilizador com função de segurança de **administrador completo** e um âmbito de segurança de **All**. Para obter mais informações, consulte os [fundamentos da administração baseada no papel.](../../../understand/fundamentals-of-role-based-administration.md) Também deve ser ligado a um servidor ligado ao site da administração central ou a um local primário autónomo de alto nível.

 Existem 3 passos básicos para testar clientes na pré-produção.  

1.  Configure atualizações automáticas do cliente para utilizar uma coleção de pré-produção.  

2.  Instale uma atualização do Gestor de Configuração que inclua uma nova versão do cliente.  

3.  Promover o novo cliente à produção.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar atualizações automáticas de clientes para usar uma coleção de pré-produção  
> [!IMPORTANT]
> A implantação de clientes de pré-produção não é suportada para computadores de grupo de trabalho. Não podem usar a autenticação necessária para o ponto de distribuição aceder ao pacote de clientes pré-produção.  Receberão o mais recente cliente quando for promovido a cliente de produção.

1. [Configurar uma coleção](../collections/create-collections.md) que contenha os computadores para os os seus dados que pretende implementar o cliente de pré-produção.   

2. No Gestor de Configuração, abra**os sites**de**configuração** > do site **da administração** > e escolha **as Definições da Hierarquia.**  

    No separador **Atualização de Clientes** nas **Propriedades das Definições de Hierarquia**:  

   -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente ao utilizar o cliente de pré-produção**  

   -   Introduza o nome de uma coleção para utilizar como coleção de pré-produção  

![Teste de atualizações de clientes](media/test-client-upgrades.png)

>[!NOTE]
>Para alterar estas definições, a sua conta deve ser membro da função de segurança **do Administrador Completo** e do âmbito de segurança **All.**


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar uma atualização do Configuration Manager que inclua uma nova versão do cliente  

1.  Na consola do Gestor de Configuração, abra**as Atualizações de** **Administração** > e a Manutenção, selecione uma atualização **disponível** e, em seguida, escolha **instalar o Pack de Atualização**. (Antes da versão 1702, atualizações e manutenção estava **sob** > **serviços**de cloud administration .)

     Para mais informações sobre a instalação de atualizações, consulte [Atualizações para Gestor de Configuração](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, na página **Opções** do Cliente do assistente, selecione **Teste na recolha pré-produção**.  

3.  Conclua o resto do assistente e instale o pacote de atualizações.  

     Depois de concluído o assistente, os clientes na coleção de pré-produção começarm a implementar o cliente atualizado. Pode monitorizar a implementação de clientes **atualizados, indo** > para monitorizar o**Estado** > do Cliente**Pré-produção.** Para mais informações, consulte Como monitorizar o estado de [implementação](../../../../core/clients/deploy/monitor-client-deployment-status.md)do cliente .

    > [!NOTE]
    > O estado de implementação em computadores que hospedam funções do sistema do site numa recolha pré-produção pode ser reportado como **não conforme** mesmo quando o cliente foi implementado com sucesso. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover o novo cliente para produção  

1.  Na consola de Configuração Manager, abra atualizações de **administração** > **e manutenção,** e escolha Promover o Cliente de **Pré-produção.** (Antes da versão 1702, atualizações e manutenção estava **sob** > **serviços**de cloud administration .)

    > [!TIP]
    > Também está disponível o botão **Promover Cliente de Pré-produção** quando está a monitorizar implementações de cliente na consola em **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**.

2.  Reveja as versões do cliente em produção e pré-produção, certifique-se de que a recolha pré-produção está especificada e, em seguida, clique em **Promover**, em **seguida, Sim**.  

3.  Após o fecho da caixa de diálogo, a versão atualizada do cliente substituirá a versão cliente em uso na sua hierarquia. Em seguida, pode atualizar os clientes para todo o site. Consulte [como atualizar os clientes para computadores Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) para obter mais informações.  

>[!NOTE]
>Para permitir ao cliente de pré-produção, ou promover um cliente de pré-produção a um cliente de produção, a sua conta deve ser membro de uma função de segurança que tenha **lido** e **modificado** permissões para o objeto **Update Packages.**
>As atualizações do cliente honram quaisquer janelas de manutenção do Gestor de Configuração que tenha configurado.
