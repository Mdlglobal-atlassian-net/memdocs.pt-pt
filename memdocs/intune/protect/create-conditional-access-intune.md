---
title: Configurar acesso condicional baseado em dispositivos com Intune
titleSuffix: Microsoft Intune
description: Saiba como criar uma política de acesso condicional baseada em dispositivos com base na conformidade do dispositivo Microsoft Intune e na gestão de aplicações móveis.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e40f9bc84e4969e963629479f22a6f988e025c4e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985043"
---
# <a name="create-a-device-based-conditional-access-policy"></a>Criar uma política de acesso condicional baseada em dispositivos

Com o Intune, melhore o Acesso Condicional no Diretório Ativo Azure adicionando a conformidade do dispositivo móvel aos controlos de acesso. Com a política de conformidade intune que define os requisitos para que os dispositivos sejam conformes, pode utilizar o estado de conformidade de um dispositivo para permitir ou bloquear o acesso às suas apps e serviços. Pode fazê-lo criando uma política de acesso condicional que utilize a definição Exigir que o **dispositivo seja marcado como conforme**.

Uma política de Acesso Condicional especifica a app ou serviços que pretende proteger, as condições em que as aplicações ou serviços podem ser acedidos, e os utilizadores a que a apólice se aplica. Embora o Acesso Condicional seja uma funcionalidade premium Azure AD, o nó de Acesso Condicional a que acede a Partir de *Intune* é o mesmo nó a que o *Azure AD*acedido.

> [!IMPORTANT]
> Antes de configurar o Acesso Condicional, terá de configurar políticas de conformidade do dispositivo Intune para avaliar os dispositivos com base no cumprimento de requisitos específicos. Ver Iniciar com as políticas de [conformidade do dispositivo em Intune](device-compliance-get-started.md).

## <a name="create-conditional-access-policy"></a>Criar política de acesso condicional

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos**Políticas  >  **de acesso condicional**  >  **Policies**  >  **Nova política**.
  ![Criar uma nova política de acesso condicional](./media/create-conditional-access-intune/create-ca.png)

3. Em **Atribuições**, selecione **Utilizadores e grupos**.

4. No separador **Incluir,** identifique os utilizadores ou grupos a que esta política de Acesso Condicional se aplica. Depois de ter escolhido grupos ou utilizadores para incluir, utilize o separador **Excluir** se houver utilizadores, funções ou grupos que pretenda excluir desta política.

   - **Todos os utilizadores**: Selecione esta opção para aplicar a política a todos os utilizadores e grupos, incluindo utilizadores internos e convidados.

   - **Selecione utilizadores e grupos:** Selecione esta opção e especifique uma ou mais das seguintes opções:
  
     1. **Todos os utilizadores convidados**: Selecione esta opção para incluir ou excluir utilizadores externos (por exemplo, parceiros, colaboradores externos)

     2. **Funções de diretório**: Selecione uma ou mais funções de Anúncio Azure para incluir ou excluir utilizadores que sejam atribuídos a estas funções.

     3. **Utilizadores e grupos**: Selecione esta opção para procurar e selecione utilizadores ou grupos individuais que deseja incluir ou excluir.

        > [!TIP]
        > Teste a política contra um grupo mais pequeno de utilizadores para garantir que funciona como esperado.

5. Selecione **Done** (Concluído).

6. Em **Atribuições,** selecione **aplicações ou ações cloud**.

7. No separador **Incluir,** utilize as opções disponíveis para identificar as aplicações e serviços que pretende proteger com esta política de Acesso Condicional. Então pode utilizar o separador **Excluir** se houver alguma aplicação ou serviços que queira excluir desta política.

   - **Todas as aplicações na nuvem**: Selecione esta opção para aplicar a política a todas as aplicações.
     > [!IMPORTANT]
     > A aplicação Microsoft Azure Management para acesso ao portal Azure está incluída nesta lista. Certifique-se de que utiliza o separador **Excluir** aqui ou nas opções **de Utilizadores e grupos** para garantir que você (ou os utilizadores ou grupos que designa) poderão iniciar sessão no portal Azure. 

   - **Selecione aplicações**: Selecione esta opção, escolha **Selecionar**e, em seguida, use a lista de aplicações para procurar e selecione as aplicações ou serviços que pretende proteger.

   Quando estiver pronto, selecione **Done**.

8. Em **Atribuições,** selecione **Condições**.

   - **Risco de entrada**: Selecione *Sim* para utilizar a deteção de risco de deteção de risco de proteção de identidade Azure AD com esta política e, em seguida, escolha os níveis de risco de entrada a que a política deve aplicar.

   - **Plataformas**do dispositivo : No separador **Incluir,** identifique as plataformas do dispositivo a que pretende aplicar a esta política de Acesso Condicional. Utilize o separador **Excluir** para excluir plataformas desta política.

   - **Localizações**: No separador **Incluir,** especifique se a política se aplica a:
     - Qualquer local
     - Locais de rede confiáveis que estão sob o controlo do seu departamento de TI
     - Localizações específicas da rede.

     Utilize o separador **Excluir** para excluir as localizações da rede desta política.

   - **Aplicativos para clientes**: Selecione *Sim* para especificar se a política deve aplicar-se a aplicações de navegador, aplicações móveis e clientes de desktop.

   - **Estado**do dispositivo : A política de acesso condicional aplicar-se-á a todos os estados do dispositivo, a menos que escolha Sim e exclua especificamente os estados Dispositivo Híbrido Azure AD aderido ou Dispositivo marcado como conforme (ou ambos).

     > [!TIP]
     > Se quiser proteger tanto os clientes de **autenticação moderna** como os **clientes Exchange ActiveSync,** crie duas políticas de Acesso Condicional separadas, uma para cada tipo de cliente. Embora o Exchange ActiveSync suporte a autenticação moderna, a única condição que é suportada pelo Exchange ActiveSync é a plataforma. Outras condições, incluindo a autenticação multifactor, não são suportadas. Para proteger eficazmente o acesso ao Exchange Online do Exchange ActiveSync, crie uma política de Acesso Condicional que especifique a aplicação cloud Office 365 Exchange Online e a aplicação cliente Exchange ActiveSync com a política de Aplicação apenas para plataformas suportadas selecionadas.

9. Selecione **Done** (Concluído).

10. Em **Controlos de acesso**, selecione **Concessão**. Configure o que acontece com base nas condições que configura.  Pode selecionar entre as seguintes opções:

    - **Acesso ao bloco**: Os utilizadores especificados nesta política serão impedidos de aceder às aplicações nas condições que especificou.
    - **Acesso à concessão**: Os utilizadores especificados nesta política terão acesso, mas pode exigir qualquer uma das seguintes ações a seguir:
      - **Requerer a autenticação de vários fatores**: O utilizador terá de preencher requisitos de segurança adicionais, como uma chamada telefónica ou texto.
      - **Exigir que o dispositivo seja marcado como conforme:** O dispositivo deve ser intune compatível. Se o dispositivo não estiver em conformidade, o utilizador terá a opção de inscrever o dispositivo em Intune.
      - **Requerer dispositivo híbrido Azure AD:** Os dispositivos devem ser AD Hybrid Azure unidos.
      - **Requerer aplicação de cliente aprovada**: O dispositivo deve utilizar aplicações de clientes aprovadas. 
      - **Para vários controlos**: Selecione **Requerer todos os controlos selecionados** de modo a que todos os requisitos sejam aplicados quando um dispositivo tentar aceder à aplicação.

      ![Controlos de acesso Definições de subvenção](./media/create-conditional-access-intune/create-ca-grant-access-settings.png)

11. Em **Ativar política**, selecione **Ativado**.

12. Selecione **Criar**.

## <a name="next-steps"></a>Passos seguintes

[Acesso Condicional baseado em aplicativos com Intune](app-based-conditional-access-intune.md)

[Resolução de problemas Acesso Condicional Intune](https://support.microsoft.com/help/4456106)
