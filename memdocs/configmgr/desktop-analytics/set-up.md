---
title: Configurar a Análise de Computadores
titleSuffix: Configuration Manager
description: Um guia de como configurar e embarcar para desktop Analytics.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91a65f240a20e30af1610670c79182dee744e77b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714907"
---
# <a name="how-to-set-up-desktop-analytics"></a>Como configurar desktop Analytics

Utilize este procedimento para iniciar sessão no Desktop Analytics e configurá-lo na sua subscrição. Este procedimento é um processo único para configurar desktop Analytics para a sua organização.  

> [!Important]  
> Para obter informações sobre os pré-requisitos gerais para desktop Analytics com Configuração Manager, consulte [pré-requisitos](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Embarque inicial

1. Abra o [portal Desktop Analytics](https://aka.ms/desktopanalytics) na Microsoft 365 Device Management como utilizador com a função Global **Admin.** Selecione **Iniciar**. Alternativamente, na consola Do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** selecione o nó de manutenção do **Desktop Analytics** e selecione **implementações**de Plano .

2. Na página do contrato de **serviço Aceitar,** reveja o contrato de serviço e selecione **Aceitar**.  

3. Na página **confirmar a sua subscrição,** reveja a lista das licenças de qualificação necessárias. Mude a definição para **Sim** ao lado **de Ter uma das subscrições suportadas ou superiores,** e depois selecione **Next**.  

4. Na página de acesso dos **utilizadores Dar:**

    - Permitir que o Desktop Analytics gere as funções de **Diretório em seu nome:** Desktop Analytics atribui automaticamente aos Proprietários do Espaço de **Trabalho** a função de Administrador de Análise de **Desktop.** Se esses grupos já são um **Administrador Global,** não há mudança.

        Caso não selecione esta opção, o Desktop Analytics continua a adicionar utilizadores como membros do grupo de segurança. Um **Administrador Global** precisa atribuir manualmente a função de Administrador de Análise de **Desktop** para os utilizadores.

        Para obter mais informações sobre a atribuição de permissões de funções de administrador no Diretório Ativo do Azure e as permissões atribuídas aos Administradores de Análise de **Desktop,** consulte [permissões de funções de administrador no Diretório Ativo do Azure](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics reconfigura o grupo de segurança **Workspace Owners** no Azure Ative Directory para criar e gerir espaços de trabalho e planos de implementação.

        Para adicionar um utilizador ao grupo, escreva o seu nome ou endereço de e-mail na secção **'Nome De entrada'.** Quando terminar, selecione **Next**.

5. Na página para **configurar o seu espaço de trabalho:**  

    > [!NOTE]  
    > Para completar este passo, o utilizador necessita de permissões **do Proprietário do Workspace** e acesso adicional à subscrição e Grupo de Recursos Azure. Para mais informações, consulte [os pré-requisitos.](overview.md#prerequisites)  

    - Para utilizar um espaço de trabalho existente para desktop Analytics, selecione-o e continue com o próximo passo.  

        > [!TIP]  
        > Você só pode ter um espaço de trabalho desktop Analytics por inquilino Azure AD. Os dispositivos só podem enviar dados de diagnóstico para um espaço de trabalho.  

    - Para criar um espaço de trabalho para desktop Analytics, **selecione Adicionar espaço de trabalho**.  

        1. Introduza um **nome**espaço de trabalho globalmente único.

        2. Selecione a lista de drop-down para Selecionar o nome de **subscrição Azure para este espaço**de trabalho , e escolha a subscrição Azure para este espaço de trabalho.  

        3. **Criar novos** Grupo de recursos ou **Utilização existente**.

        4. Selecione a **Região** da lista e, em seguida, selecione **Adicionar**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione set como espaço de **trabalho desktop Analytics**.  Em seguida, selecione **Continuar** no diálogo **de acesso confirmar e conceder** acesso.  

7. No novo separador de navegador, escolha uma conta para usar para iniciar sessão. Selecione a opção de **Consentimento em nome da sua organização** e selecione **Aceitar**.  

    > [!Note]  
    > Este consentimento é atribuir à aplicação MALogAnalyticsReader a função Log Analytics Reader para o espaço de trabalho. Esta função de aplicação é exigida pelo Desktop Analytics. Para mais informações, consulte a [função de aplicação MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Volte à página para **configurar o seu espaço de trabalho,** selecione **Next**.  

9. Na página **dos últimos passos,** selecione **Ir para desktop Analytics**.

O portal Azure mostra a página **inicial** do Desktop Analytics Home.

## <a name="next-steps"></a>Passos seguintes

Avance para o próximo artigo para ligar o Gestor de Configuração ao Desktop Analytics.
> [!div class="nextstepaction"]  
> [Ligar Gestor de Configuração](connect-configmgr.md)  
