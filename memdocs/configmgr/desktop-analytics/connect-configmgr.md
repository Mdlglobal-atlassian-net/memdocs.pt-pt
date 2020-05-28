---
title: Ligar Gestor de Configuração
titleSuffix: Configuration Manager
description: Um guia de como ligar o Gestor de Configuração ao Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c7bb6d01a35ce42002207d57d27fc41c37646d15
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268866"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Como ligar o Gestor de Configuração ao Desktop Analytics

O Desktop Analytics está fortemente integrado com o Gestor de Configuração. Em primeiro lugar, certifique-se de que o site está atualizado para suportar as funcionalidades mais recentes. Em seguida, crie a ligação Desktop Analytics no Gestor de Configuração. Finalmente, monitorize a saúde da ligação.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a>Atualizar o site

Primeiro, certifique-se de que o site do Gestor de Configuração está a funcionar pelo menos na versão 1902. Para mais informações, consulte [Instalar atualizações na consola](../core/servers/manage/install-in-console-updates.md).

Também precisa de instalar o rollup da atualização versão 1902 (4500571) para apoiar a integração com o Desktop Analytics. Para mais informações sobre esta atualização, consulte [o rollup atualizado para o atual ramo do Gestor de Configuração, versão 1902](https://support.microsoft.com/help/4500571).

1. Atualize o site com a atualização rollup para a versão 1902. Para mais informações, consulte [Instalar atualizações na consola](../core/servers/manage/install-in-console-updates.md).

2. Atualizar clientes. Para simplificar este processo, considere utilizar a atualização automática do cliente. Para mais informações, consulte [os clientes de Upgrade](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a>Ligue-se ao serviço

> [!TIP]
> Antes de iniciar o assistente, crie a coleção de alvos mencionada no passo 8, uma vez que não pode selecionar fora do assistente uma vez que o inicie.

Utilize este procedimento para ligar o Gestor de Configuração ao Desktop Analytics e configurar as definições do dispositivo. Este procedimento é um processo único para anexar a sua hierarquia ao serviço de nuvem.

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** **Selecione Configure Azure Services** na fita.

    > [!TIP]
    > Ligue-se ao serviço diretamente a partir do nó de manutenção desktop **Analytics.** Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software** e selecione o nó de manutenção desktop **Analytics.** Na caixa *New to Desktop Analytics?* *Connect Configuration Manager to the Desktop Analytics service*

2. Na página de **Serviços Azure** do Assistente de Serviços Azure, configure as seguintes definições:

    - Especifique um **nome** para o objeto no Gestor de Configuração.

    - Especifique uma **Descrição** opcional para o ajudar a identificar o serviço.

    - Selecione **Desktop Analytics** da lista de serviços disponíveis.

   Selecione **Seguinte**.

3. Na página da **App,** selecione o **ambiente Azure**apropriado . Em seguida, selecione **Browse** para a aplicação web.

4. Se tiver uma aplicação existente que deseja reutilizar para este serviço, escolha-a na lista e selecione **OK**.

5. Na maioria dos casos, pode criar uma aplicação para a ligação Desktop Analytics com este assistente. Selecione **Criar**.<!-- 3572123 -->

    > [!TIP]
    > Se não conseguir criar a aplicação a partir deste assistente, pode criar manualmente a aplicação em Azure AD e, em seguida, importar para O Gestor de Configuração. Para mais informações, consulte criar e importar app para O Gestor de [Configuração](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Configure as seguintes definições na janela **Create Server Application:**

    - **Nome da aplicação**: Um nome amigável para a aplicação em Azure AD.

    - **URL homePage**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por predefinição, este valor é `https://ConfigMgrService`.

    - **App ID URI**: Este valor tem de ser único no seu inquilino Azure AD. Está no sinal de acesso usado pelo cliente do Gestor de Configuração para solicitar o acesso ao serviço. Por predefinição, este valor é `https://ConfigMgrService`.

    - **Período**de validade da chave secreta : escolha 1 **ano** ou **2 anos** da lista de abandono. Um ano é o valor padrão.

    Selecione **Iniciar sessão** . Depois de autenticar com sucesso o Azure, a página mostra o Nome de **Inquilino AD Azure** para referência.

    > [!NOTE]
    > Complete este passo como **administrador global.** Estas credenciais não são guardadas pelo Diretor de Configuração. Esta persona não requer permissões no Gestor de Configuração, e não precisa de ser a mesma conta que gere o Assistente de Serviços Azure.

    Selecione **OK** para criar a aplicação web em Azure AD e fechar o diálogo create server application. No diálogo da Aplicação servidor, selecione **OK**. Em seguida, selecione **Next** na página da App do Assistente de Serviços Azure.

7. Na página dados de **diagnóstico,** configure as seguintes definições:

    - **ID Comercial**: este valor deve povoar automaticamente com o ID da sua organização. Se não o fizer, certifique-se de que o seu servidor proxy está configurado para permitir todos os [pontos finais necessários](enable-data-sharing.md#endpoints) antes de continuar. Em alternativa, recupere o seu ID Comercial manualmente a partir do [portal Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Nível de dados de diagnóstico do Windows 10:** selecione pelo menos **Basic**. Ver [Níveis de dados de diagnóstico](enable-data-sharing.md#diagnostic-data-levels)
  
    - **Permitir o nome do dispositivo em dados de diagnóstico:** selecione **Enable**

        > [!NOTE]
        > A partir da versão 1803 do Windows 10, o nome do dispositivo não é enviado para a Microsoft por padrão. Se não enviar o nome do dispositivo, aparece no Desktop Analytics como "Desconhecido". Este comportamento pode dificultar a identificação e avaliação dos dispositivos.

   Selecione **Seguinte**. A página de **funcionalidades disponíveis** mostra a funcionalidade Desktop Analytics que está disponível com as definições de dados de diagnóstico da página anterior. Selecione **Next** para continuar ou **Anterior** para fazer alterações.

    ![Exemplo Página de Funcionalidade disponível no Assistente de Serviços Azure](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Na página **Coleções,** configure as seguintes definições:

    - **Nome do ecrã**: O portal Desktop Analytics apresenta esta ligação de Gestor de Configuração utilizando este nome. Use-o para diferenciar entre diferentes hierarquias, e para identificar coleções de hierarquias separadas. Use termos para distinguir facilmente várias hierarquias no seu ambiente, por exemplo: laboratório de *teste* ou *produção.*

    - **Recolha do alvo**: Esta recolha inclui todos os dispositivos que o Gestor de Configuração configura com as definições de ID comerciais e dados de diagnóstico. É o conjunto completo de dispositivos que o Gestor de Configuração liga ao serviço Desktop Analytics.

    - **Os dispositivos na recolha do alvo utilizam um proxy autenticado**pelo utilizador para comunicação de saída : Por defeito, este valor é **Nº**. Se necessário no seu ambiente, **deponha-se**a Sim.

    - **Selecione coleções específicas para sincronizar com desktop Analytics**: Selecione **Adicionar** para incluir coleções adicionais da sua hierarquia de **recolha Target.** Estas coleções estão disponíveis no portal Desktop Analytics para agrupar com planos de implementação. Certifique-se de incluir coleções de exclusão de pilotos e pilotos.  <!-- 4097528 -->

        > [!TIP]
        > A janela Select Collections exibe apenas as coleções que são limitadas pela **coleção Target**.
        >
        > No exemplo seguinte, selecione CollectionA como a sua coleção de alvos. Depois, quando adiciona coleções adicionais, vê-se collectiona, collectionB e CollectionC. Não pode adicionar CollectionD.
        >
        > - CollectionA: limitada pela coleção **All Systems**
        >     - ColeçãoB: limitada pela CollectionA
        >         - ColeçãoC: limitada pela CollectionB
        > - ColeçãoD: limitada pela coleção **All Systems**
        >
        > Para gerir as coleções disponíveis no portal Desktop Analytics para agrupar com planos de implementação, na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó dos **Serviços Azure.** Selecione a entrada associada ao Serviço **Desktop Analytics** Azure e atualize as suas definições na página de Recolha de Análise de **Desktop.**

        > [!IMPORTANT]
        > Estas coleções continuam a sincronizar-se à medida que a sua adesão muda. Por exemplo, a sua coleção Target utiliza uma coleção com uma regra de subscrição do Windows 7. À medida que estes dispositivos atualizam para o Windows 10, e o Gestor de Configuração avalia a adesão à recolha, esses dispositivos abandonam a recolha e desktop Analytics.

9. Conclua o assistente.

O Gestor de Configuração cria uma política de definições para configurar dispositivos na Coleção Target. Esta política inclui as definições de dados de diagnóstico para permitir que os dispositivos enviem dados para a Microsoft. Por padrão, os clientes atualizam a política a cada hora. Depois de receber as novas definições, pode demorar várias horas a mais até que os dados estejam disponíveis no Desktop Analytics.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a>Monitorizar a saúde da ligação

Monitorize a configuração dos seus dispositivos para Desktop Analytics. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o nó de manutenção desktop **Analytics** e selecione o painel de assistência à saúde de **ligação.**

Para mais informações, consulte [Monitor de saúde](monitor-connection-health.md)de ligação .

O Gestor de Configuração sincroniza as suas coleções no prazo de 60 minutos após a criação da ligação. No portal Desktop Analytics, vá ao**Global Pilot**e consulte as coleções do seu dispositivo De Configuração Manager.

> [!NOTE]
> A ligação do Gestor de Configuração ao Desktop Analytics baseia-se no ponto de ligação do serviço. Quaisquer alterações na função do sistema do site podem ter impacto na sincronização com o serviço de nuvem. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Próximos passos

Avance para o próximo artigo para inscrever dispositivos para desktop Analytics.
> [!div class="nextstepaction"]
> [Inscrever dispositivos](enroll-devices.md)
