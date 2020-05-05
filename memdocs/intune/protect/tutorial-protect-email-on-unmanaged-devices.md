---
title: Tutorial - Proteja o e-mail online de troca de dispositivos não geridos
titleSuffix: Microsoft Intune
description: Aprenda a garantir o Office 365 Exchange Online com políticas de proteção de aplicações Intune e Acesso Condicional Azure AD.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/30/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f32ced29b6bb53f8c091ba1a0f42261a2baa493
ms.sourcegitcommit: d05b1472385c775ebc0b226e8b465dbeb5bf1f40
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605223"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Tutorial: Proteja o e-mail online de troca de dispositivos não geridos

Saiba utilizar políticas de proteção de aplicações com acesso condicional para proteger o Exchange Online, mesmo quando os dispositivos não estão matriculados numa solução de gestão de dispositivos como o Intune. Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Crie uma política de proteção de aplicações Intune para a aplicação Outlook. Irá limitar o que o utilizador pode fazer com os dados da aplicação, prevenindo "Save As" e restringindo as ações de corte, cópia e pasta.
> * Crie políticas de Acesso Condicional azure Ative (Azure AD) que permitam apenas que a app Outlook aceda a emails da empresa no Exchange Online. Também necessitará de autenticação multifactor (MFA) para clientes de autenticação moderna, como o Outlook para iOS e Android.

## <a name="prerequisites"></a>Pré-requisitos

Precisará de um inquilino de teste com as seguintes subscrições para este tutorial:

- Azure Active Directory Premium ([avaliação gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Subscrição inoportuna[(teste gratuito)](../fundamentals/free-trial-sign-up.md)
- Microsoft 365 Apps para subscrição de negócios que inclui Exchange[(teste gratuito)](https://go.microsoft.com/fwlink/p/?LinkID=510938)

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Para este tutorial, quando iniciar sessão no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)inscreva-se como [administrador global](../fundamentals/users-add.md#types-of-administrators) ou administrador de [serviço](../fundamentals/users-add.md#types-of-administrators)intune . Se criou uma subscrição intune Trial, a conta com a qual criou a subscrição é o administrador global.

## <a name="create-the-app-protection-policy"></a>Criar a política de proteção de aplicações

Neste tutorial, vamos criar uma política de proteção de aplicações Intune para o iOS para a aplicação Outlook para colocar proteções no lugar ao nível da aplicação. Vamos exigir um PIN para abrir a aplicação num contexto de trabalho. Também limitaremos a partilha de dados entre apps e evitaremos que os dados da empresa sejam guardados para uma localização pessoal.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione > Políticas de**proteção**de **apps** > **Criar a política**e selecione **iOS/iPadOS** para a plataforma.

3. Na página **Basics,** configure as seguintes definições:

   - **Nome**: Entrar no teste de política da **aplicação Outlook**.
   - **Descrição**: Inserir o teste de política da **aplicação Outlook**.

   O valor **da Plataforma** está definido para a sua escolha anterior.

   Clique **em Seguir** para continuar.

4. A página **Apps** permite-lhe escolher como pretende aplicar esta política a aplicações em diferentes dispositivos. Configure as seguintes opções:

   - Para **o Target para todos os tipos de aplicações**: Selecione **No**, e depois para tipos de **aplicações,** selecione a caixa de verificação de **Apps em dispositivos não geridos**.
   - Clique em **Selecionar aplicações públicas**. Na lista de Apps, selecione **Outlook**, e depois escolha **Select**.  O Outlook aparece agora em *aplicações públicas.*

   Clique **em Seguir** para continuar.

5. A página de **proteção de Dados** fornece configurações que determinam como os utilizadores interagem com os dados nas aplicações que esta política de proteção de aplicações se aplica. Configure as seguintes opções:

   Abaixo *da Transferência de Dados,* configure as seguintes definições, deixando todas as outras definições nos seus valores predefinidos:

   - Para **enviar dados org para outras aplicações**, selecione **Nenhuma**.  
   - Para **receber dados de outras apps,** selecione **Nenhum**.  
   - Para **guardar cópias dos dados org,** selecione **Bloquear**.  
   - Para restringir o corte, a cópia e a **pasta entre outras aplicações,** selecione **Blocked**. 

   ![Selecione as definições de deslocalização de dados da política de proteção de aplicações Outlook](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Selecione **Seguinte** para continuar.

6. A página **de requisitos** de Acesso fornece configurações que lhe permitem configurar os requisitos PIN e credenciais que os utilizadores devem cumprir para aceder a apps num contexto de trabalho. Configure as seguintes definições, deixando todas as outras definições nos seus valores predefinidos:

   - Para **obter acesso**PIN, selecione **Exigir**.
   - Para **o trabalho ou credenciais de conta escolar para acesso,** selecione **Exigir**.

   ![Selecione as ações de acesso à política de proteção de aplicações Outlook](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Selecione **Seguinte** para continuar.

7. A página de **lançamento condicional** fornece definições para definir os requisitos de segurança de início de sessão para a sua política de proteção de aplicações. Para este tutorial, não precisa de configurar estas definições.

   Clique **em Seguir** para continuar.

8. Utilize a página **De atribuição** para atribuir a política de proteção de aplicações a grupos de utilizadores. Para este tutorial, não atribuirá esta apólice a um grupo.  

   Clique **em Seguir** para continuar.

9. No **Seguinte: Rever + criar** página, rever os valores e configurações que inseriu para esta política de proteção de aplicações. Clique em **Criar** para criar a política de proteção de aplicações em Intune.

A política de proteção de aplicações para o Outlook é criada. Em seguida, irá configurar o Acesso Condicional para exigir que os dispositivos utilizem a aplicação Outlook.

## <a name="create-conditional-access-policies"></a>Criar políticas de acesso condicional

Agora vamos criar duas políticas de Acesso Condicional para cobrir todas as plataformas de dispositivos.  

- A primeira política exigirá que os clientes da Autenticação Moderna utilizem a app 'Outlook' aprovada e a autenticação de vários fatores (MFA). Os clientes de Autenticação Moderna incluem Outlook para iOS e Outlook para Android.  

- A segunda política exigirá que os clientes Exchange ActiveSync utilizem a aplicação Outlook aprovada. (Atualmente, o Exchange Ative Sync não suporta outras condições que não a plataforma do dispositivo). Pode configurar as políticas de Acesso Condicional no portal Azure AD ou no portal Intune. Já que já estamos no portal Intune, vamos criar a apólice aqui.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Criar uma política de MFA para clientes de autenticação moderna  

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **segurança** >  endpoint**Acesso** > condicional**Nova política**.  

3. Para **Nome**, insira a política de **teste para clientes modernos auth**.  

4. Em **Atribuições**, selecione **Utilizadores e grupos**. No separador **Incluir**, selecione **Todos os utilizadores** e, em seguida, selecione **Concluído**.

5. Em **Atribuições,** selecione **aplicações ou ações cloud**. Uma vez que queremos proteger o e-mail do Office 365 Exchange Online, vamos selecioná-lo ao seguir estes passos:

   1. No separador **Incluir**, escolha **Selecionar aplicações**.
   2. Escolha **Selecionar**.
   3. Na lista de Aplicações, selecione **Office 365 Exchange Online**, e, em seguida, escolha **Select**.
   4. Selecione **Feito** para voltar ao novo painel de política.

   ![Selecionar a aplicação Office 365 Exchange Online](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

6. Em **Atribuições**, selecione **Condições** > **Plataformas de dispositivos**.

   1. Em **Configurar**, selecione **Sim**.
   2. No separador **Incluir,** selecione **Qualquer dispositivo**.
   3. Selecione **Done** (Concluído).

7. No painel **Condições,** selecione **aplicações do Cliente.**

   1. Em **Configurar**, selecione **Sim**.
   2. Selecione **aplicativos Móveis e clientes de desktop** e clientes de **autenticação moderna.**
   3. Limpe as outras caixas de verificação.
   4. Selecione **Done** > **Done** para voltar ao novo painel de política.

   ![Selecione aplicativos móveis e clientes](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. Em **Controlos de acesso**, selecione **Concessão**.

   1. No painel **Concessão**, selecione **Conceder acesso**.
   2. Selecione **Exigir autenticação de vários fatores.**
   3. Selecione **Requer aplicação aprovada do cliente**.
   4. Em **Para vários controlos**, selecione **Exigir todos os controlos selecionados**. Esta definição garantirá que ambos os requisitos que selecionou são impostos quando um dispositivo tentar aceder ao e-mail.
   5. Escolha **Selecionar**.

   ![Selecione controlos de acesso](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. Sob **a política ativar**, selecione **On**e, em seguida, selecione **Criar**.

   ![Criar política](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

É criada a política de Acesso Condicional para clientes de Autenticação Moderna. Agora pode criar uma política para clientes Exchange Ative Sync.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Criar uma política para clientes Exchange Ative Sync

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **segurança** > de fim de**ponta** > Acesso condicional**Nova política**.

3. Para **Nome**, insira a política de **teste para clientes EAS**.

4. Em **Atribuições**, selecione **Utilizadores e grupos**. No separador *Incluir*, selecione **Todos os utilizadores** e, em seguida, selecione **Concluído**.

5. Em **Atribuições,** selecione **aplicações ou ações cloud**. Selecione Office 365 Exchange Online com estes passos:

   1. No separador *Incluir*, escolha **Selecionar aplicações**.
   2. Escolha **Selecionar**.
   3. A partir da lista de *Aplicações,* selecione **Office 365 Exchange Online,** e depois escolha **Select**, e depois **Done**.
  
6. Em **Atribuições**, selecione **Condições** > **Plataformas de dispositivos**.

   1. Em **Configurar**, selecione **Sim**.
   2. No separador **Incluir,** selecione **Qualquer dispositivo**, e, em seguida, selecione **Done**.

7. No painel **Condições,** selecione **aplicações do Cliente.**

   1. Em **Configurar**, selecione **Sim**.
   2. Selecione **aplicativos Móveis e clientes de desktop.**
   3. Selecione **clientes Exchange ActiveSync** e **aplique a política apenas a plataformas suportadas**.  
   4. Desmarque todas as outras caixas de verificação.  
   5. Selecione **Concluído** e, em seguida, selecione **Concluído** novamente.  

   ![Aplicar a plataformas apoiadas](./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)  

8. Em **Controlos de acesso**, selecione **Concessão**.

   1. No painel **Concessão**, selecione **Conceder acesso**.
   2. Selecione **Requer aplicação aprovada do cliente**. Desmarque todas as outras caixas de verificação.
   3. Escolha **Selecionar**.

   ![Exigir aplicação de cliente aprovada](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. Sob **a política ativar**, selecione **On**e, em seguida, selecione **Criar**.

As suas políticas de proteção de aplicações e acesso condicional estão agora no lugar e prontas a testar.

## <a name="try-it-out"></a>Experimente

Com as políticas que criou, os dispositivos terão de se inscrever no Intune e usar a aplicação móvel Outlook para aceder ao email do Office 365. Para testar este cenário num dispositivo iOS, experimente iniciar sessão no Exchange Online com as credenciais para um utilizador no seu inquilino de teste.

1. Para testar um iPhone, aceda a **Definições** > **Palavras-passe & Contas** > Adicionar**Troca**de**Contas** > .

2. Introduza o endereço de e-mail de um utilizador no inquilino de teste e, em seguida, prima **Seguinte**.  
3. Prima **Iniciar Sessão**.

4. Introduza a palavra-passe do utilizador de teste e prima **Iniciar sessão**.

5. A mensagem **Mais informações são necessárias,** o que significa que está a ser solicitado para configurar o MFA. Vá em frente e estabeleça um método de verificação adicional.

6. Em seguida, você verá uma mensagem que diz que está a tentar abrir este recurso com uma app que não é aprovada pelo seu departamento de TI. A mensagem significa que está a ser impedido de usar a aplicação de correio nativo. Cancele o sinal.

7. Abra a aplicação Outlook e selecione **Definições** > **Adicionar Conta de****Email** > .

8. Introduza o endereço de e-mail de um utilizador no inquilino de teste e, em seguida, prima **Seguinte**.

9. Pressione **o Office 365**. Será solicitado para autenticação e registo adicionais. Uma vez que tenha assinado, pode testar ações como cortar, copiar, colar e "Salvar As".

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não precisar das políticas de teste, poderá removê-las.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **as políticas**de conformidade dos **dispositivos** .

3. Na lista **de Nomes** de Política, selecione o menu de contexto **(...**) para a sua política de teste e, em seguida, selecione **Delete**. Selecione **OK** para confirmar.

4. Selecione **segurança** > endpoint Acesso**condicional**.

5. Na lista **de Nomes** de Política, selecione o menu de contexto **(...**) para cada uma das suas políticas de teste e, em seguida, selecione **Delete**. Selecione **Sim** para confirmar.

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, criou políticas de proteção de aplicações para limitar o que o utilizador pode fazer com a aplicação Outlook, e criou políticas de Acesso Condicional para exigir a aplicação Outlook e exigir MFA para clientes de autenticação moderna. Para aprender sobre a utilização de Intune com Acesso Condicional para proteger outras aplicações e serviços, consulte [Configurar acesso condicional](conditional-access.md).
