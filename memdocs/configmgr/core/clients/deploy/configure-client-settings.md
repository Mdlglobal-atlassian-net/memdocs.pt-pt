---
title: Configurar definições do cliente
titleSuffix: Configuration Manager
description: Selecione as definições do cliente no Gestor de Configuração.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713591"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Como configurar as definições do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Gere todas as definições de cliente no Gestor de Configuração a partir de**Definições**de Cliente de **Administração** > . Modifique as predefinições quando pretender configurar definições para todos os utilizadores e dispositivos da hierarquia que não têm definições personalizadas aplicadas. Se pretender aplicar diferentes definições aapenas a alguns utilizadores ou dispositivos, crie configurações personalizadas e implemente para coleções.  

Para obter informações sobre cada definição de cliente, consulte [sobre as definições do cliente](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Também pode utilizar itens de configuração a fim de gerir os clientes para avaliar, controlar e retificar a compatibilidade de configuração dos dispositivos. Para mais informações, consulte Garantir o [cumprimento do dispositivo com o Gestor de Configuração](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configure as definições padrão do cliente    

1. Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

2. No separador **Casa,** escolha **Propriedades**.  

3. Veja e configure as definições do cliente de cada grupo de definições do painel de navegação.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Iniciar a Recuperação](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) de Políticas para um Cliente de Gestor de Configuração em [Como gerir os clientes](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Criar e implementar configurações personalizadas do cliente  
Quando implementar estas definições personalizadas, elas substituirão as predefinições do cliente. Antes de iniciar este procedimento, certifique-se de que tem uma coleção com os utilizadores ou dispositivos que necessitam destas definições personalizadas de cliente.  

1. Na consola 'Gestor de Configuração', escolha**as Definições**do Cliente **de Administração** > .  

2. No separador **Casa,** no grupo **Criar,** escolha **Criar Definições personalizadas de Cliente,** e depois escolher qualquer um:  

   -   **Criar Definições Personalizadas do Dispositivo Cliente**  

   -   **Criar Definições Personalizadas do Utilizador Cliente**  

3. Especifique um nome e descrição de opção únicas.  

4. Selecione uma ou mais caixas de verificação que apresentem um grupo de definições.  

5. Escolha cada grupo de definições a partir do painel de navegação e configure as definições disponíveis e, em seguida, clique **EM OK**.   

6. Selecione a definição personalizada do cliente que criou. No separador **Casa,** no grupo Definições do **Cliente,** escolha **Implementar**.  

7. Na caixa de diálogo **Select Collection,** selecione a recolha apropriada e, em seguida, escolha **OK**. Pode verificar a coleção selecionada clicando no separador **Implementações** do painel de detalhes.  

8. Veja a ordem do ambiente personalizado do cliente que criou. Quando tem várias definições personalizadas de cliente, estas são aplicadas de acordo com o seu número de ordem. Se existirem conflitos, a definição que tiver o menor número de ordem substitui as outras definições. Para alterar o número de encomenda, no separador **Home,** no grupo Definições do **Cliente,** escolha **Mover item Up** ou Mover **item para baixo**.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Iniciar a Recuperação](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) de Políticas para um Cliente de Gestor de Configuração em [Como gerir os clientes](../../../core/clients/manage/manage-clients.md).  



##  <a name="view-client-settings"></a>Ver as definições do cliente  
 Quando implementa várias definições de cliente para o mesmo dispositivo, utilizador ou grupo de utilizadores, a priorização e combinação de definições é complexa. Para ver as definições do cliente:  

1.  Na consola 'Gestor de Configuração', escolha**Os Utilizadores** de**Dispositivos** >  **de Segurança e Conformidade** > ou **As Coleções dos Utilizadores**.  

3.  Selecione um dispositivo, um utilizador ou um grupo de utilizadores e, no grupo **Definições do Cliente** , selecione **Definições de Cliente Resultantes**.  

4.  Selecione uma definição de cliente a partir do painel esquerdo e as definições são apresentadas. Nesta perspetiva, as definições são apenas para leitura. 

    > [!NOTE]  
    >  Para ver as definições do cliente, deve ter lido o acesso às Definições do Cliente.  

    
