---
title: Gerir definições de deteção e resposta de ponto final com políticas de segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Configure e implemente políticas para dispositivos que gere com a política de deteção e resposta final de ponto final no Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 063d7fbbd5572e1ff2399efc161d319c6c9c5c1b
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824122"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Política de deteção e resposta de ponto final para segurança de ponto final em Intune

Quando integrar a Microsoft Defender Advanced Threat Protection (Defender ATP) com o Intune, pode utilizar políticas de segurança de ponto final para deteção e resposta de pontofinal (EDR) para gerir as definições edr e dispositivos de bordo para o Defender ATP.

As capacidades de deteção e resposta de ponto final atp defender fornecem deteções avançadas de ataque que são quase em tempo real e acionáveis. Os analistas de segurança podem priorizar os alertas de forma eficaz, ganhar visibilidade em todo o âmbito de uma violação e tomar medidas de resposta para remediar ameaças.

As políticas edr incluem perfis específicos da plataforma para gerir as definições para edr. Os perfis incluem automaticamente um pacote de *embarque* para o AtP defender. Os pacotes de embarque são como os dispositivos são configurados para trabalhar com o Defender ATP. Depois de um dispositivo a bordo, pode começar a utilizar dados de ameaça a partir desse dispositivo.

As políticas EDR implementam para grupos de dispositivos no Azure Ative Directory (Azure AD) que gere com a Intune, e para coleções de dispositivos no local que gere com o Gestor de Configuração, incluindo servidores Windows. As políticas EDR para as diferentes vias de gestão requerem diferentes pacotes de embarque. Por isso, irá criar políticas EDR separadas para os diferentes tipos de dispositivos que gere.

> [!TIP]
> O suporte para dispositivos que gere com o Gestor de Configuração está em *pré-visualização pública*.

Encontre as políticas de segurança de ponto final para o EDR no *âmbito do Manage* no nó de segurança **Endpoint** do centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Ver definições para perfis de [deteção e resposta de Ponto Final](../protect/endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Pré-requisitos para as políticas edr

**Geral:**

- **Inquilino da Microsoft Defender Advanced Threat Protection** – O seu inquilino ATP defender deve ser integrado ao seu inquilino microsoft Endpoint Manager (subscrição Intune) antes de poder criar políticas EDR. Consulte [o Microsoft Defender ATP](../protect/advanced-threat-protection.md) na documentação Intune.

**Para suportar dispositivos do Gestor de Configuração:**

Para suportar a utilização de políticas EDR com dispositivos De Configuração Manager, o ambiente do Gestor de Configuração requer as seguintes configurações adicionais. Neste artigo, são fornecidas [orientações de configuração:](#set-up-configuration-manager-to-support-edr-policy)

- **Gestor de Configuração com versão 2002 ou posterior** – O seu site deve executar o Gestor de Configuração 2002 ou mais tarde.

- **Instale a atualização do Gestor** de Configuração - Para ativar o suporte no Gestor de Configuração 2002 para utilizar a política EDR que cria no centro de administração do Microsoft Endpoint Manager, instale a seguinte atualização a partir da consola do Gestor de Configuração:
  - **Gestor de Configuração 2002 Hotfix (KB4563473)**

- **Configurar anexação de Inquilino** - A anexação do Inquilino permite sincronizar coleções de dispositivos desde o Configur Manager até ao centro de administração do Microsoft Endpoint Manager. Em seguida, pode utilizar o centro de administração para implementar políticas EDR para essas coleções.

  A anexação do inquilino é frequentemente configurada com cogestão, mas você pode configurar o anexo do inquilino por si só.

- **Sincronizar as coleções do Gestor** de Configuração – Quando configurar a anexação do inquilino, pode selecionar as coleções de dispositivos Do Gestor de Configuração para sincronizar com o centro de administração do Microsoft Endpoint Manager. Também pode voltar mais tarde para modificar as coleções do dispositivo que sincroniza. A política EDR para dispositivos De Configuração Manager só pode ser atribuída a coleções que tenha sincronizado.

  Depois de selecionar coleções para sincronizar, deve capacitá-las para utilização com o Microsoft Defender ATP.

- **Permissões para O Anúncio De Azure** - Para completar a configuração do anexo de inquilinos e configurar as coleções do Gestor de Configuração que sincronizará com o centro de administração do Microsoft Endpoint Manager, vai precisar de uma conta com permissões do Administrador Global para a sua subscrição do Azure.

## <a name="edr-profiles"></a>Perfis EDR

[Ver as definições](../protect/endpoint-security-edr-profile-settings.md) que pode configurar para as seguintes plataformas e perfis.

**Intune** – Os seguintes são suportados para dispositivos que gere com Intune:

- Plataforma: **Windows 10 e mais tarde** - Intune implementa a política para dispositivos nos seus grupos AD Azure.
- Perfil: **Deteção e resposta de ponto final (MDM)**

**Gestor de Configuração** *(Na pré-visualização)* - Os seguintes são suportados para dispositivos que gere com o Gestor de Configuração:

- Plataforma: **Windows 10 e Windows Server** - O Gestor de Configuração implementa a política para dispositivos nas suas coleções de Gestor de Configuração.
- Perfil: **Deteção e resposta de ponto final (ConfigMgr) (Pré-visualização)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configurar o Gestor de Configuração para apoiar a política EDR

Antes de poder implementar as políticas EDR para dispositivos De Configuração Manager, complete as configurações detalhadas nas seguintes secções.

Estas configurações são feitas dentro da consola do Gestor de Configuração e na implementação do Gestor de Configuração. Se não estiver familiarizado com o Gestor de Configuração, planeie trabalhar com um administrador do Gestor de Configuração para completar estas tarefas.  

As seguintes secções cobrem as tarefas necessárias:

1. [Instale a atualização para 'Gestor de Configuração'](#task-1-install-the-update-for-configuration-manager)
2. [Ativar a anexação do inquilino](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Selecione coleções para sincronizar](#task-3-select-collections-to-synchronize)
4. [Ativar coleções para o Microsoft Defender ATP](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Para saber mais sobre a utilização do Microsoft Defender ATP com O Gestor de Configuração, consulte os seguintes artigos no conteúdo do Gestor de Configuração:
>
> - [Clientes do Gestor de Configuração a bordo do Microsoft Defender ATP através do centro de administração do Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Anexo de inquilino do Microsoft Endpoint Manager: As ações de sincronização e dispositivos do dispositivo](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Tarefa 1: Instale a atualização para O Gestor de Configuração

A versão de 2002 do Gestor de Configuração requer uma atualização para suportar o uso com as políticas de deteção e resposta de Endpoint que implementa a partir do centro de administração do Microsoft Endpoint Manager.

**Detalhes da atualização:**

- **Gestor de Configuração 2002 Hotfix (KB4563473)**

Encontrará esta atualização como uma *atualização na consola* para O Gestor de Configuração 2002.

Para instalar esta atualização, siga as orientações da [Instalação de atualizações na consola](../../configmgr/core/servers/manage/install-in-console-updates.md) na documentação do Gestor de Configuração.

Depois de instalar a atualização, volte aqui para continuar a configurar o seu ambiente para suportar a política EDR a partir do centro de administração do Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Tarefa 2: Configure a anexação e sincronização das coleções

Se a cogestão foi previamente ativada, então o anexo de inquilino já está configurado e você pode saltar para a frente para a [Tarefa 3](#task-3-select-collections-to-synchronize).

Com o Tenant anexado, especifice coleções de dispositivos a partir da implementação do Seu Gestor de Configuração para sincronizar com o centro de administração do Microsoft Endpoint Manager. Após a sincronização das coleções, utilize o centro de administração para visualizar informações sobre esses dispositivos e implementar a política EDR de Intune para eles.  

Para obter mais informações sobre o cenário de anexação do Arrendatário, consulte [o anexo do inquilino Enable](../../configmgr/tenant-attach/device-sync-actions.md) no conteúdo do Gestor de Configuração.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Ativar o anexo do inquilino quando a cogestão não foi ativada

> [!TIP]
> Utiliza o **Assistente de Configuração de Cogestão** na consola do Gestor de Configuração para permitir a anexação do inquilino, mas não precisa de ativar a cogestão.

Se está a planear permitir a cogestão, esteja familiarizado com a cogestão, os seus pré-requisitos e como gerir as cargas de trabalho antes de continuar. Ver [O que é a cogestão na](../../configmgr/comanage/overview.md) documentação do Gestor de Configuração.

1. Na consola de administração do Gestor de Configuração, vá à **Administração**  >  **Visão Geral**  >  da Cogestão dos**Serviços cloud.**  >  **Co-management**
2. Na fita, clique em **Configurar co-management** para abrir o assistente.
3. Na página de embarque do **Tenant,** selecione **AzurePublicCloud** para o seu ambiente. A nuvem do Governo Azure não é apoiada.
   1. Clique **em Iniciar sessão**. Use a sua conta *De Administrador Global* para iniciar sessão.

   2. Certifique-se de que a opção Upload para o centro de administração do **Microsoft Endpoint Manager** é selecionada na página de embarque do **Tenant.**

   3. Retire o cheque de **Ativação automática de inscrição automática do cliente para cogestão**.

      Quando esta opção é selecionada, o Assistente apresenta páginas adicionais para completar a configuração da cogestão. Para mais informações, consulte [a cogestão do Enable](../../configmgr/comanage/how-to-enable.md) no conteúdo do Gestor de Configuração.

     ![Configure anexação de inquilino](./media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Clique **em Seguinte** e, em **seguida, sim** para aceitar a notificação de **Aplicação Create AAD.** Esta ação prevê um diretor de serviço e cria um registo de aplicação Azure AD para facilitar a sincronização das coleções ao centro de administração do Microsoft Endpoint Manager.

5. Na página de upload do **Configure,** configure quais as coleções que pretende sincronizar. Pode limitar a sua configuração a uma ou poucas coleções de dispositivos ou utilizar a definição de upload recomendada para **todos os meus dispositivos geridos pelo Microsoft Endpoint Configuration Manager**.

6. Clique em **Resumo** para rever a sua seleção e, em seguida, clique em **Next**.

7. Quando o assistente estiver completo, clique em **Fechar**.

   A anexação do inquilino está agora configurada e as coleções selecionadas sincronizam-se com o centro de administração do Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Ativar o anexo do inquilino quando utilizar a cogestão

1. Na consola de administração do Gestor de Configuração, vá à **Administração**  >  **Visão Geral**  >  da Cogestão dos**Serviços cloud.**  >  **Co-management**

2. Clique à direita nas definições de cogestão e selecione **Propriedades**.

3. No **separador de upload Configure,** selecione Upload para o centro de administração do **Microsoft Endpoint Manager**. Clique em **Aplicar**.
   - A definição predefinida para o upload do dispositivo é **todos os meus dispositivos geridos pelo Microsoft Endpoint Configuration Manager**. Também pode optar por limitar a sua configuração a uma ou poucas coleções de dispositivos.

     ![Ver o separador de propriedades de cogestão](./media/endpoint-security-edr-policy/configure-upload.png)

4. Inscreva-se na sua conta *De Administrador Global* quando solicitado.

5. Clique **em Sim** para aceitar a notificação de **Aplicação Create AAD.** Esta ação prevê um diretor de serviço e cria um registo de aplicação da AD Azure para facilitar a sincronização.

6. Clique em **OK** para sair das propriedades de cogestão uma vez que tenha feito alterações.

   A anexação do inquilino está agora configurada e as coleções selecionadas sincronizam-se com o centro de administração do Microsoft Endpoint Manager.

### <a name="task-3-select-collections-to-synchronize"></a>Tarefa 3: Selecione coleções para sincronizar

Quando a anexação do inquilino estiver configurada, pode selecionar coleções para sincronizar. Se ainda não sincronizou as coleções ou precisa de reconfigurar quais as que sincroniza, pode editar as propriedades da cogestão na consola do Gestor de Configuração para o fazer.

#### <a name="select-collections"></a>Selecione coleções

1. Na consola de administração do Gestor de Configuração, vá à **Administração**  >  **Visão Geral**  >  da Cogestão dos**Serviços cloud.**  >  **Co-management**

2. Clique à direita nas definições de cogestão e selecione **Propriedades**.

3. No **separador de upload Configure,** selecione Upload para o centro de administração do **Microsoft Endpoint Manager**. Clique em **Aplicar**.

   A definição predefinida para o upload do dispositivo é **todos os meus dispositivos geridos pelo Microsoft Endpoint Configuration Manager**. Também pode optar por limitar a sua configuração a uma ou poucas coleções de dispositivos.

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Tarefa 4: Ativar coleções para o Microsoft Defender ATP

Depois de configurar as coleções para sincronizar com o centro de administração do Microsoft Endpoint Manager, ainda deve permitir que essas coleções sejam elegíveis para as políticas ATP de embarque e Microsoft Defender.  Para isso, edita as propriedades de cada coleção na consola 'Gestor de Configuração'.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Ativar coleções para uso com Proteção avançada de ameaças

1. A partir de uma consola de Configuração Manager ligada ao seu site de nível superior, clique à direita numa coleção de dispositivos que sincroniza para o centro de administração do Microsoft Endpoint Manager e selecione **Properties**.

2. No separador **Cloud Sync,** ative a opção de **disponibilizar esta coleção para atribuir as políticas ATP**do Microsoft Defender em Intune .

   - Não pode selecionar esta opção se a sua hierarquia do Gestor de Configuração não for arrendatária.
  
   ![Configurar sincronização de nuvem](./media/endpoint-security-edr-policy/cloud-sync.png)

3. Selecione **OK** para salvar a configuração.

   Os dispositivos desta coleção podem agora receber a política ATP do Microsoft Defender.

## <a name="create-and-deploy-edr-policies"></a>Criar e implementar políticas EDR

Quando a subscrição ATP do Microsoft Defender estiver integrada no Intune, pode criar e implementar políticas EDR. Há dois tipos distintos de política EDR que pode criar. Um tipo de política para dispositivos que gere com Intune através de MDM. O segundo tipo é para dispositivos que gere com O Gestor de Configuração.

Você vai escolher o tipo de política que você cria enquanto cria uma nova política EDR quando você escolher a plataforma para a política.

Antes de poder implementar a política para dispositivos geridos pelo Gestor de Configuração, [configura o Gestor de Configuração para suportar a política EDR](#set-up-configuration-manager-to-support-edr-policy) a partir do centro de administração do Microsoft Endpoint Manager.

### <a name="create-edr-policies"></a>Criar políticas EDR

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **a**  >  **deteção e resposta**de fim de ponta de segurança de fim de ponta  >  **Create Policy**.

3. Selecione a plataforma e o perfil para a sua apólice. As seguintes informações identificam as suas opções:

   - Intune - Intune implementa a política para dispositivos nos seus grupos De AD Azure. Quando criar a apólice, selecione:
     - Plataforma: **Windows 10 e mais tarde**
     - Perfil: **Deteção e resposta de ponto final (MDM)**

   - Gestor de Configuração - Gestor de Configuração implementa a política para dispositivos nas suas coleções de Gestor de Configuração. Quando criar a apólice, selecione:
     - Plataforma: **Windows 10 e Windows Server**
     - Perfil: **Deteção e resposta de ponto final (ConfigMgr) (Pré-visualização)**

4. Selecione **Criar**.

5. Na página **Basics,** introduza um nome e descrição para o perfil e, em seguida, escolha **Seguinte**.

6. Na página de definições de **Configuração,** configure as definições que pretende gerir com este perfil. O pacote de embarque é automaticamente incluído e não é algo que se possa configurar.

   Quando terminar as definições de configuração, selecione **Next**.

7. *Este passo aplica-se apenas ao perfil de **deteção e resposta do Ponto Final (MDM):** *  

   Na página **scope tags,** escolha **Selecione etiquetas** de âmbito para abrir o painel *de etiquetas Select para* atribuir etiquetas de âmbito ao perfil.
  
   Selecione **Seguinte** para continuar.

8. Na página **de Atribuiçãos,** selecione os grupos ou coleções que receberão esta política. A escolha depende da plataforma e perfil que selecionou:

   - Para Intune, você irá selecionar grupos de Azure AD.
   - Para o Gestor de Configuração, irá selecionar coleções do Gestor de Configuração que sincronizou com o centro de administração do Microsoft Endpoint Manager e habilitado para a política ATP do Microsoft Defender.

   Pode optar por não atribuir grupos ou coleções neste momento e, mais tarde, editar a política para adicionar uma atribuição.

   Quando estiver pronto para continuar, selecione **Next**.

9. Na página **Review + criar** página, quando terminar, escolha **Criar**.

   O novo perfil é apresentado na lista quando seleciona o tipo de política para o perfil que criou.

## <a name="edr-policy-reports"></a>Relatórios políticos edr

Pode visualizar detalhes sobre as políticas EDR que implementa no centro de administração do Microsoft Endpoint Manager. Para ver detalhes, vá à implementação e resposta de **endpoint de segurança**  >  **endpoint**, e selecione uma política para a qual você deseja ver detalhes de conformidade:

- Para políticas que visam o **Windows 10 e posterior** plataforma (Intune), verá uma visão geral do cumprimento da política. Também pode selecionar o gráfico para visualizar uma lista de dispositivos que receberam a apólice e perfurar em dispositivos individuais para obter mais detalhes.

- Para políticas que visam a plataforma **Windows 10 e Windows Server** (Gestor de Configuração), você verá uma visão geral da conformidade com a política, mas não pode perfurar para ver detalhes adicionais. A vista é limitada porque o centro de administração recebe detalhes de estado limitados do Gestor de Configuração, que gere a implementação da apólice para dispositivos De Configuração Manager.

[Ver as definições](../protect/endpoint-security-edr-profile-settings.md) que pode configurar tanto para plataformas como para perfis.

## <a name="next-steps"></a>Passos seguintes

- [Configure políticas de segurança de Endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
- Saiba mais sobre [deteção e resposta](https://docs.microsoft.com/windows/security/-threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) de ponto final na documentação ATP do Microsoft Defender.
