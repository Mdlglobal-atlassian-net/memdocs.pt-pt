---
title: Como eliminar apenas os dados empresariais das aplicações
titleSuffix: Microsoft Intune
description: Aprenda a limpar seletivamente apenas dados corporativos de aplicações geridas por Intune com o Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 42605e6e-5b84-44ff-b86e-346ea123b53e
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1640928bfb1ca27d4ee72e014adad88db0976a2d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078350"
---
# <a name="how-to-wipe-only-corporate-data-from-intune-managed-apps"></a>Como eliminar apenas dados empresariais de aplicações geridas pelo Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Quando um dispositivo se perde ou é roubado ou se o empregado sair da sua empresa, quer ter a certeza de que os dados empresariais da aplicação são removidos do dispositivo. No entanto, é recomendável não remover os dados pessoais do dispositivo, especialmente se o dispositivo pertencer ao funcionário.

>[!NOTE]
> As plataformas iOS/iPadOS, Android e Windows 10 são as únicas plataformas atualmente suportadas para limpar dados corporativos de aplicações geridas pela Intune. As aplicações geridas intune são aplicações que incluem o Intune APP SDK e têm uma conta de utilizador licenciada para a sua organização. A implementação de políticas de proteção de aplicações não é necessária para permitir a limpeza seletiva da aplicação.

Para remover seletivamente os dados de aplicações da empresa, utilize os passos neste tópico para criar um pedido de eliminação de dados. Depois de concluir o pedido, da próxima vez que a aplicação for executada no dispositivo, os dados da empresa são removidos da aplicação. Para além de criar um pedido de eliminação, pode configurar uma eliminação seletiva dos dados da sua organização como uma nova ação, caso as definições de Acesso de Políticas de Proteção de Aplicações (APP) não sejam cumpridas. Esta funcionalidade ajuda-o a proteger e remover automaticamente dados confidenciais da organização de aplicações com base em critérios pré-configurados.

>[!IMPORTANT]
> Os contactos sincronizados diretamente da aplicação para o livro de endereços nativo são removidos. Não é possível eliminar contactos que sejam sincronizados do livro de endereços nativo para outra origem externa. Atualmente, é aplicável apenas à aplicação Microsoft Outlook.

## <a name="deployed-wip-policies-without-user-enrollment"></a>Políticas WIP implementadas sem inscrição do utilizador 
As políticas de Proteção de Informação do Windows (WIP) podem ser implementadas sem exigir que os utilizadores de MDM insuem o seu dispositivo Windows 10. Esta configuração permite que as empresas protejam os seus documentos empresariais com base na configuração do WIP, o que permite que o utilizador mantenha a gestão dos seus próprios dispositivos Windows. Uma vez protegidos os documentos com uma política wip, os dados protegidos podem ser limpos seletivamente por um administrador intune (administrador global ou administrador de[serviço intune).](../fundamentals/users-add.md#types-of-administrators) Ao selecionar o utilizador e o dispositivo, e ao enviar um pedido de eliminação de dados, todos os dados protegidos através da política WIP ficarão inutilizáveis. A partir do Intune no portal Azure, selecione **app** > cliente**app limpeza seletiva**. Para obter mais informações, veja [Criar e implementar a política de proteção de aplicações do Windows Information Protection (WIP) com o Intune](windows-information-protection-policy-create.md).

## <a name="create-a-device-based-wipe-request"></a>Criar um pedido de limpeza baseado em dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **App limpeza seletiva Criar pedido** > de**limpeza**.<br>
   O painel de pedido de **limpeza Create** é apresentado.
3. Clique em **Selecionar utilizador,** escolha o utilizador cujos dados da aplicação pretende limpar e clique em **Selecionar** na parte inferior do painel de **utilizadores Select.**

    ![Screenshot do painel 'Select user'](./media/apps-selective-wipe/apps-selective-wipe-01.png)

4. Clique **Em Selecione o dispositivo,** escolha o dispositivo e clique em **Selecionar** na parte inferior do painel **Select Device.**

    ![Screenshot do painel 'Create wipe request' onde o dispositivo é selecionado](./media/apps-selective-wipe/apps-selective-wipe-02.png)

5. Clique em **Criar** para fazer um pedido de limpeza.

O serviço cria e controla um pedido de eliminação separado para cada aplicação protegida no dispositivo, bem como o utilizador associado ao pedido de eliminação.

   ![Screenshot de 'Aplicativos cliente - App selective wipe' pane](./media/apps-selective-wipe/apps-selective-wipe-03.png)

## <a name="create-a-user-based-wipe-request"></a>Criar um pedido de limpeza baseado no utilizador

Ao adicionar mos um utilizador à limpeza ao nível do Utilizador, emitemos automaticamente comandos de limpeza a todas as aplicações em todos os dispositivos do utilizador.  O utilizador continuará a receber comandos de limpeza em todos os check-ins de todos os dispositivos.  Para voltar a ativar um utilizador, deve removê-lo da lista.  

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps** > **App limpeza seletiva Criar pedido** > de**limpeza**.<br>
   **Selecione a limpeza ao nível do utilizador**
3. Clique em **Adicionar** e **Selecione** painel de utilizador.
4. Escolheu o utilizador cujos dados da aplicação gostaria de limpar e clicar em **Select**.

## <a name="monitor-your-wipe-requests"></a>Monitorizar os pedidos de eliminação

Pode obter um relatório resumido que mostra o estado geral do pedido de eliminação e inclui o número de pedidos pendentes e de falhas. Para obter mais detalhes, siga estes passos:

1. No painel**de limpeza seletivo** da App **Apps,** > pode ver a lista dos seus pedidos agrupados pelos utilizadores. Uma vez que o sistema cria um pedido de eliminação para cada aplicação protegida em execução no dispositivo, poderá ver múltiplos pedidos para um utilizador. O estado indica se um pedido de eliminação está **pendente**, **falhou** ou se teve **êxito**.

    ![Captura de ecrã do estado do pedido de eliminação no painel Eliminação seletiva de aplicações](./media/apps-selective-wipe/wipe-request-status-1.png)

Além disso, pode ver o nome do dispositivo e o respetivo tipo de dispositivo, o que pode ser útil durante a leitura dos relatórios.

>[!IMPORTANT]
> O utilizador tem de abrir a aplicação para que a eliminação ocorra. Após efetuar o pedido, a eliminação pode durar até 30 minutos.

## <a name="delete-a-device-wipe-request"></a>Eliminar um pedido de limpeza de dispositivos

As eliminações em estado pendente são apresentadas até que as elimine manualmente. Para eliminar manualmente um pedido de eliminação:

1. No painel **Aplicações Cliente – Eliminação seletiva da aplicação**.

2. Na lista, clique com o botão direito do rato no pedido de eliminação que pretende eliminar e, em seguida, selecione **Eliminar pedido de eliminação**.

    ![Captura de ecrã da lista do pedido de eliminação no painel Eliminação seletiva de aplicações](./media/apps-selective-wipe/delete-wipe-request.png)

3. Quando lhe for pedido para confirmar a eliminação, escolha **Sim** ou **Não** e, em seguida, clique em **OK**.

## <a name="delete-a-user-wipe-request"></a>Eliminar um pedido de limpeza do utilizador

As toalhetes do utilizador permanecerão na lista até serem removidas por um administrador. Para remover um utilizador da lista:

1. Nas **Aplicações do Cliente - Painel** de limpeza seletiva da aplicação selecione **Limpeza ao Nível do Utilizador**
2. A partir da lista, clique à direita no utilizador que pretende eliminar e, em seguida, escolha **Eliminar**. 


## <a name="see-also"></a>Consulte também
[O que é uma política de proteção de aplicações](app-protection-policy.md)

[O que é a gestão de aplicações](app-management.md)
