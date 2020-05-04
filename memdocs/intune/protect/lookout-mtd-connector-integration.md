---
title: Configurar a sua integração do Lookout com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Aprenda a integrar intune com a Lookout Mobile Endpoint Security, como uma solução de Defesa de Ameaças Móveis, para controlar o acesso de dispositivos móveis aos seus recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/11/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5b0d7644-3183-45ba-a165-0d82d70cb71e
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54e81a7b9614e1633fe9061fd13d1b99810ce43c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329221"
---
# <a name="set-up-lookout-mobile-endpoint-security-integration-with-intune"></a>Configurar a integração de segurança de ponto supérno móvel lookout com intune
Com um ambiente que satisfaça os [pré-requisitos,](lookout-mobile-threat-defense-connector.md#prerequisites)pode integrar a Lookout Mobile Endpoint Security com o Intune. As informações deste artigo irão guiá-lo na configuração da integração e configurar configurações importantes no Lookout para utilização com o Intune.  

> [!IMPORTANT]
> Um inquilino do Lookout Mobile Endpoint Security que ainda não esteja associado ao seu inquilino do Azure AD não pode ser utilizado na integração com o Azure AD e o Intune. Contacte o suporte do Lookout para criar um novo inquilino do Lookout Mobile Endpoint Security. Utilize o novo inquilino para integrar os seus utilizadores do Azure AD.

## <a name="collect-azure-ad-information"></a>Recolher informações do Azure AD  
Para integrar o Lookout com o Intune, associa o seu inquilino de Segurança de Ponto final de Mobilidade À Sua Assinatura Azure Ative Directory (AD).

Para permitir a integração da subscrição de subscrição de Lookout Mobileenterprisesupport@lookout.comEndpoint Security com a Intune, fornece as seguintes informações ao suporte de Vigia ():  

- **Id do diretório do inquilino da Azure AD**  

- Id de objeto do **grupo Azure AD** para o grupo com acesso **completo** à consola Lookout Mobile Endpoint Security (MES).  
  Cria este grupo de utilizadores em Azure AD para conter os utilizadores que têm *acesso total* para iniciar sessão na **consola Lookout**. Os utilizadores devem ser membros deste grupo, ou do grupo de *acesso restrito* opcional, para iniciar sessão na Consola de Vigia. 

- Id de objeto do **grupo Azure AD** para o grupo com acesso **restrito** à consola MES *(grupo opcional)*. 
  Cria este grupo de utilizadores opcional no Azure AD para conter utilizadores que não devam ter acesso a várias configurações e módulos relacionados com as inscrições da consola Lookout. Em vez disso, estes utilizadores têm acesso apenas ao módulo de Política de **Segurança** da consola Lookout. Os utilizadores devem ser membros deste grupo opcional, ou do grupo de *acesso completo* necessário, para iniciar sessão na Consola de Vigia.

 > [!TIP] 
 > Para obter mais detalhes sobre as permissões, consulte [este artigo](https://personal.support.lookout.com/hc/articles/114094105653) no site do Lookout.

### <a name="collect-information-from-azure-ad"></a>Recolher informações da Azure AD 

1. Inscreva-se no [portal Azure](https://portal.azure.com) com uma conta de Administrador Global.

2. Vá à **Azure Ative Directory** > **Properties** e localize o seu ID **de Diretório**. Utilize o botão *Copiar* para copiar o ID do Diretório e, em seguida, guarde-o num ficheiro de texto.

   ![Propriedades da AD Azure](./media/lookout-mtd-connector-integration/azure-ad-properties.png)  

3. Em seguida, encontre o ID do Grupo Azure AD para as contas que utiliza para conceder aos utilizadores de AD Azure acesso à Consola de Vigia. Um grupo é para *acesso total*, e o segundo grupo, para *acesso restrito* é opcional. Para obter o ID do *Objeto,* para cada conta:  
   1. Vá a **Azure Ative Directory** > **Groups** para abrir os *Grupos - Todos os grupos* painel.  

   2. Selecione o grupo que criou para *o acesso total* para abrir o seu painel de visão *geral.*  

   3. Utilize o botão *Copiar* para copiar o ID do objeto e, em seguida, guarde-o num ficheiro de texto.  

   4. Repita o processo para o grupo de *acesso restrito* se utilizar esse grupo.  

      ![Id de objeto do grupo Azure AD](./media/lookout-mtd-connector-integration/azure-ad-group-id.png)  

   Depois de recolher esta informação, contacte o suporte do Lookout (e-mail: enterprisesupport@lookout.com). O Lookout Support trabalhará com o seu contacto principal para embarcar na sua subscrição e criar a sua conta Lookout Enterprise, utilizando a informação que fornece.  

## <a name="configure-your-lookout-subscription"></a>Configure a sua subscrição de Vigia  

Os seguintes passos serão concluídos na consola de administração da Lookout Enterprise e permitirão uma ligação ao serviço da Lookout para dispositivos matriculados intune (através da conformidade do dispositivo) **e** dispositivos não matriculados (através de políticas de proteção de aplicações).

Depois de o suporte da Lookout criar a sua conta Lookout Enterprise, o suporte lookout envia https://aad.lookout.com/les?action=consentum e-mail para o contacto principal da sua empresa com um link para o url de login: . 

### <a name="initial-sign-in"></a>Iniciação de inscrição  
O primeiro sessão na Consola MES Lookouthttps://aad.lookout.com/les?action=consent)apresenta uma página de consentimento ( . Um Administrador Global da AD Azure apenas se inscreva e **aceite**. O subsequente início de inscrição não requer que o utilizador tenha este nível de privilégio da AD Azure. 

 É apresentada uma página de consentimento. Escolha **Aceitar** completar o registo. 
   ![screenshot da primeira página de início de sessão da consola Lookout](./media/lookout-mtd-connector-integration/lookout_mtp_initial_login.png)

Quando aceitas e consentidos, és redirecionado para a Consola de Vigia.

Após o acesso inicial e o consentimento estarem https://aad.lookout.com completos, os utilizadores que iniciarem sessão são redirecionados para a Consola MES. Se o consentimento ainda não foi concedido, todas as tentativas de inscrição resultam num erro de login grave.

### <a name="configure-the-intune-connector"></a>Configurar o Conector Intune  
O seguinte procedimento pressupõe que criou anteriormente um grupo de utilizadores em Azure AD para testar a sua implementação de Lookout. A melhor prática é começar com um pequeno grupo de utilizadores para permitir que os seus administradores de Lookout e Intune se familiarizecom as integrações do produto. Depois de familiares, pode estender a inscrição a grupos adicionais de utilizadores.

1. Inscreva-se na [Consola MES lookout](https://aad.lookout.com) e vá para**os Conectores**do **Sistema,** > e, em seguida, selecione **Add Connector**.  Selecione **Intune**.

   ![Imagem da consola Lookout com a opção Intune no separador de conectores](./media/lookout-mtd-connector-integration/lookout_mtp_setup-intune-connector.png)

2. No painel *Microsoft Intune,* selecione Definições de **Ligação** e especifique a **frequência heartbeat** em minutos. 

   ![Imagem do separador de definições de ligação com frequência de batimentocardíaco configurada](./media/lookout-mtd-connector-integration/lookout-mtp-connection-settings.png)

3. Selecione Gestão de **Inscrições**, e para **utilizar os seguintes grupos de segurança Azure AD para identificar dispositivos que devem ser matriculados no Lookout for Work,** especifique o nome do *Grupo* de um grupo Azure AD para utilizar com o Lookout e, em seguida, selecione **alterações de Guardar**.

    ![captura de ecrã da página de inscrição do conector do Intune](./media/lookout-mtd-connector-integration/lookout-mtp-enrollment.png)  

   **Sobre os grupos que utiliza:**
   - Como uma boa prática, comece com um grupo de segurança Azure AD que contém um pequeno número de utilizadores para testar a integração do Lookout.
   - O **nome do Grupo** é sensível a casos, como mostra as **propriedades** do grupo de segurança no portal Azure.  
   - Os grupos que especifica para **a Gestão** de Inscrições definem o conjunto de utilizadores cujos dispositivos serão matriculados no Lookout. Quando um utilizador está num grupo de inscrições, os seus dispositivos em Azure AD estão matriculados e elegíveis para ativação em MES de vigia. A primeira vez que um utilizador abre a aplicação *Lookout for Work* num dispositivo suportado, é-lhes solicitado que o ative.

4. Selecione **State Sync** e certifique-se de que o estado do *dispositivo* e o estado de *ameaça* estão definidos para **On**.  Ambos são necessários para que a integração de Lookout Intune funcione corretamente.  

5. Selecione **Error Management,** especifique o endereço de e-mail que deve receber os relatórios de erro e, em seguida, selecione **Guardar alterações**.
 
   ![Captura de ecrã da página de gestão de erros do conector do Intune](./media/lookout-mtd-connector-integration/lookout-mtp-connector-error-notifications.png)

6. Selecione **Criar conector** para completar a configuração do conector. Mais tarde, quando estiver satisfeito com os seus resultados, pode alargar a inscrição a grupos de utilizadores adicionais.

## <a name="configure-intune-to-use-lookout-as-a-mobile-threat-defense-provider"></a>Configure Intune para usar Lookout como um fornecedor de defesa de ameaças móveis
Depois de configurar o Lookout MES, tem de estabelecer uma ligação com [o Lookout em Intune](mtd-connector-enable.md).  

## <a name="additional-settings-in-the-lookout-mes-console"></a>Configurações adicionais na Consola MES Lookout
Seguem-se as definições adicionais que pode configurar na Consola MES Lookout.  

### <a name="configure-enrollment-settings"></a>Configurar as definições de inscrição
Na consola MES Lookout, selecione **system** > **Manage De inscrição** > **definições**.  

- Para o **Estado desligado,** especifique o número de dias antes de um dispositivo não ligado estar marcado como desligado.  

  Considera-se que os dispositivos desligados não estão em conformidade e o acesso às aplicações da empresa a partir dos mesmos será bloqueado com base nas políticas de acesso condicional do Intune. Pode especificar valores entre 1 e 90 dias.

  ![Definições de inscrição de vigia no módulo Sistema](./media/lookout-mtd-connector-integration/lookout-console-enrollment-settings.png)

### <a name="configure-email-notifications"></a>Configure notificações de e-mail
Para receber alertas de e-mail para ameaças, inscreva-se na [Consola MES Lookout](https://aad.lookout.com) com a conta de utilizador que deverá receber notificações.  

- Vá às **Preferências** e, em seguida, detete as notificações que pretende receber para **ON**e, em seguida, **Guarde** as alterações.  

- Se já não quiser receber notificações por e-mail, detete as notificações para **OFF** e guarde as suas alterações.

  ![screenshot da página de preferências com a conta de utilizador apresentada](./media/lookout-mtd-connector-integration/lookout-mtp-email-notifications.png)

## <a name="configure-threat-classifications"></a>Configurar classificações de ameaças  
Lookout Mobile Endpoint Security classifica ameaças móveis de vários tipos. As classificações de ameaças do Lookout apresentam níveis de risco predefinidos inerentes às mesmas. Os níveis de risco podem ser alterados a qualquer momento para atender aos requisitos da sua empresa.

Para obter informações sobre as classificações de nível de ameaça e como gerir os níveis de risco associados, consulte a Referência de [Ameaça de Vigia](https://enterprise.support.lookout.com/hc/articles/360011812974).

>[!IMPORTANT]
> Os níveis de risco são um aspeto importante da Segurança do Ponto Final Móvel porque a integração Intune calcula a conformidade do dispositivo de acordo com estes níveis de risco no tempo de execução.  
> 
> O administrador intune estabelece uma regra na política para identificar um dispositivo como incompatível se o dispositivo tiver uma ameaça ativa com um nível mínimo de **Alto,** **Médio**ou **Baixo**. A política de classificação de ameaças na Lookout Mobile Endpoint Security impulsiona diretamente o cálculo da conformidade do dispositivo em Intune.  

## <a name="monitor-enrollment"></a>Monitorizar a inscrição
Após a configuração estar concluída, a Lookout Mobile Endpoint Security começa a sondar o Azure AD para dispositivos que correspondam aos grupos de matrículaespecificados.  Pode encontrar informações sobre dispositivos matriculados indo para **Dispositivos** na Consola MES Lookout.  
- O estado inicial dos dispositivos está *pendente*.  
- O estado do dispositivo atualiza-se após a instalação, abertura e ativação da aplicação *Lookout for Work* no dispositivo.

Para mais detalhes sobre como colocar a aplicação *Lookout for Work* implementada num dispositivo, consulte [Add Lookout para aplicações de trabalho com Intune](mtd-apps-ios-app-configuration-policy-add-assign.md).

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicativos de vigia para dispositivos matriculados](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurar aplicativos de vigia para dispositivos não matriculados](mtd-add-apps-unenrolled-devices.md)
