---
title: Início Rápido – experimentar gratuitamente o Microsoft Intune
titleSuffix: ''
description: Neste início rápido, criará uma subscrição de avaliação gratuita, terá conhecimento das configurações suportadas e dos requisitos de rede e configurará opcionalmente o seu nome de domínio.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 893981700ede9587a980faa0e4d6b0384c24e3d4
ms.sourcegitcommit: e7fb8cf2ffce29548b4a33b2a0c33a3a227c6bc4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/30/2020
ms.locfileid: "80401489"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>Início Rápido: experimentar gratuitamente o Microsoft Intune

O Microsoft Intune ajuda-o a proteger os dados empresariais da sua força de trabalho através da gestão de dispositivos e aplicações. Neste início rápido, criará uma subscrição gratuita para experimentar o Intune num ambiente de teste.

A Intune fornece a gestão de dispositivos móveis (MDM) e a gestão de aplicações móveis (MAM) a partir de um serviço seguro baseado na nuvem que é administrado através do centro de administração do Microsoft Endpoint Manager. A utilização do Intune permite assegurar que os recursos empresariais da sua força de trabalho (dados, dispositivos e aplicações) são configurados, acedidos e atualizados corretamente de forma a cumprir os requisitos e as políticas de conformidade da sua empresa.

## <a name="prerequisites"></a>Pré-requisitos
Antes de configurar o Microsoft Intune, reveja os seguintes requisitos:

- [Browsers e sistemas operativos suportados](supported-devices-browsers.md)
- [Largura de banda e requisitos de configuração de rede](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Inscreva-se numa avaliação gratuita do Microsoft Intune

Pode experimentar o Intune de forma gratuita durante 30 dias. Se já tiver uma conta escolar ou profissional, **inicie sessão** com a mesma e adicione o Intune à sua subscrição. Caso contrário, pode **inscrever-se** numa conta nova e utilizar o Intune para a sua organização.

> [!IMPORTANT]
> Não pode combinar uma conta escolar ou profissional existente após inscrever-se numa conta nova.

1. Aceda à página da [Avaliação do Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2019088) e preencha o formulário.

    ![Captura de ecrã da página Web de inscrição numa conta de Avaliação do Microsoft Intune](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    Se a maioria das suas operações de TI e dos seus utilizadores estiverem numa região diferente da sua, é recomendado que selecione essa região em **País ou região**. O Azure utiliza as suas informações regionais para prestar os serviços corretos. Não é possível alterar esta definição posteriormente.

2. Utilize o nome da sua empresa seguido de **.onmicrosoft.com** para criar uma conta. 

    ![Screenshot da conta experimental Intune novo processo credencial](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    Se a sua organização tiver o seu próprio domínio personalizado que pretende utilizar sem **onmicrosoft.com**,, pode alterar isso no centro de administração da Microsoft 365 descrito mais tarde neste artigo.

3. Pode ver as novas informações da sua conta nova no final do processo de inscrição.

    ![Imagem das informações da conta](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Inscreva-se no Intune no Microsoft Endpoint Manager

Se ainda não se inscreveu no portal, complete os seguintes passos:

1. Abra uma nova janela do browser e introduza **https://endpoint.microsoft.com** na barra de endereço. 
2. Utilize o ID do utilizador que lhe foi dado nos passos acima para iniciar sessão *(yourID@yourdomain* .onmicrosoft.com).

    ![Imagem da página de inscrição do portal](./media/free-trial-sign-up/azure-portal-signin.png)

Quando se inscrever numa versão de avaliação, também receberá uma mensagem de e-mail com as informações da sua conta no endereço de e-mail que indicou durante o processo de inscrição. Este e-mail confirma que a sua versão de avaliação está ativa.

> [!TIP]
> Ao trabalhar com o Microsoft Endpoint Manager, poderá ter melhores resultados a trabalhar com um navegador em modo regular, em vez de em modo privado.

## <a name="confirm-the-mdm-authority-in-intune"></a>Confirme a autoridade do MDM em Intune

Por padrão, a autoridade do MDM é definida quando cria o seu teste gratuito. Pode confirmar que a autoridade do MDM é definida utilizando os seguintes passos:

1. Se ainda não se inscreveu, inscreva-se no Microsoft Endpoint Manager.
2. Clique na **administração do Inquilino.**
3. Veja os detalhes do inquilino. A **autoridade do MDM** deve ser definida para a Microsoft **Intune**.

Se depois de iniciar sessão no Microsoft Endpoint Manager, vir um banner laranja indicando que ainda não definiu a autoridade do MDM, pode ativá-lo neste momento. A definição da autoridade de gestão de dispositivos móveis (MDM) determina como gere os seus dispositivos. Tem de definir uma autoridade de MDM para que os utilizadores possam inscrever dispositivos para gestão.

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>Para definir a autoridade do MDM para Intune, siga estes passos:

1. Abra uma nova janela do browser e introduza **https://portal.azure.com** na barra de endereço. 
2. Selecione **Todos os serviços** > **Microsoft Intune**.
3. Selecione a faixa que indica que não ativou a gestão de dispositivos ou, se não vir imediatamente a faixa, selecione **Inscrição de dispositivos**. O painel **Escolher Autoridade de MDM** será apresentado, se ainda não tiver ativado a gestão de dispositivos.

    > [!NOTE]
    > Se tiver definido a Autoridade do MDM, verá o valor da autoridade do MDM na lâmina de inscrição do **Dispositivo.** A faixa cor de laranja só é apresentada se ainda não tiver configurado a autoridade de MDM. 

    ![Imagem do painel Escolher Autoridade de MDM](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. Se a sua Autoridade de MDM não estiver definida, ao abrigo da **Autoridade do MDM,** coloque a sua autoridade de MDM intune para **intune MDM Authority**.

Para obter mais informações sobre a autoridade de MDM, veja [Definir a autoridade de gestão de dispositivos móveis](mdm-authority-set.md).

## <a name="configure-your-custom-domain-name-optional"></a>Configurar o nome de domínio personalizado (opcional)

Como mencionado acima, se a sua organização tiver o seu próprio domínio personalizado que pretende utilizar sem **.onmicrosoft.com,** pode alterá-lo no centro de administração da Microsoft 365. Pode adicionar, verificar e configurar o seu nome de domínio personalizado utilizando os seguintes passos.  

> [!IMPORTANT]
> Não é possível renomear ou remover a parte *inicial* **onmicrosoft.com** do nome de domínio. No entanto, pode adicionar, verificar ou remover nomes de domínio *personalizados* utilizados com o Intune para manter a sua identidade comercial clara. Para mais informações, consulte [Configurar um nome](custom-domain-name-configure.md)de domínio personalizado .

1. Vá ao centro de [administração da Microsoft 365](https://admin.microsoft.com) e inscreva-se na sua conta de administrador.

2. No painel de navegação, selecione **Configuração** > **Domínios** > **Adicionar domínio**.

3. Escreva o seu nome de domínio personalizado. Depois, selecione **Seguinte**.

   ![Screenshot do centro de administração da Microsoft 365 - Adicionar domínio](./media/free-trial-sign-up/domain-custom-add.png)

4. Verifique se é o proprietário do domínio que inseriu no passo anterior. 
    
    A seleção de **enviar código por e-mail** fará com que seja enviado um e-mail para o contacto registado do seu domínio. Depois de receber o e-mail, copie o código e introduza-o no campo **Escreva o seu código de verificação aqui**. Se o código de verificação corresponder, o domínio será adicionado ao seu inquilino. O e-mail apresentado poderá não parecer familiar. Alguns registradores escondem o endereço de e-mail real. Além disso, o endereço de e-mail pode ser diferente do que foi fornecido quando o domínio foi registado.

   ![Screenshot do centro de administração da Microsoft 365 - Verifique o domínio](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > Para obter mais informações sobre a verificação de registo TXT, veja [Criar registos DNS em qualquer fornecedor de alojamento DNS para o Office 365](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166).

## <a name="admin-experiences"></a>Experiências de administrador

Existem dois portais que irá utilizar com mais frequência:
- O centro de administração do Microsoft Endpoint Manager[ (https://endpoint.microsoft.com/) ](https://endpoint.microsoft.com/)é onde pode explorar as [capacidades de Intune](what-is-intune.md). É aqui que um administrador trabalharia com intune.
- O centro de administração do Microsoft 365[ (https://admin.microsoft.com) ](https://admin.microsoft.com)é onde pode adicionar e gerir os utilizadores, caso não esteja a utilizar o Azure Ative Directory para o fazer. Também pode gerir outros aspetos da sua conta, incluindo faturação e suporte.

## <a name="next-steps"></a>Próximos passos

Neste guia de início rápido, criou uma subscrição gratuita para experimentar o Intune num ambiente de teste. Para obter mais informações sobre como configurar o Intune, veja [Configurar o Intune](setup-steps.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: criar um utilizador e atribuir uma licença ao mesmo](quickstart-create-user.md)
