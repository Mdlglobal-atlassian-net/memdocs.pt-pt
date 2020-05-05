---
title: Pré-visualização técnica 1709
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1709 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bedb515c8446e13189fb84644bc0ce7563cc1574
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078775"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1709 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1709. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **A atualização para pré-visualizar a versão 1709 falha quando tem um servidor**de site em modo passivo . Quando executar a versão de pré-visualização 1706, 1707 ou 1708 e tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)tem de desinstalar o servidor do site do modo passivo antes de poder atualizar com sucesso o seu site de pré-visualização para a versão 1709. Pode reinstalar o servidor do site do modo passivo depois de o seu site ser executado na versão 1709.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola, vá para **a Administração** > **Resumo** > servidores de**configuração** > do site**e funções**do sistema do site, e, em seguida, selecione o servidor de site de modo passivo.
  2. No painel de funções do **Sistema do Site,** clique à direita na função **do servidor do Site** e, em seguida, escolha remover **a função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência melhorada de perfil VPN na consola de Gestor de Configuração
<!-- 1313282 -->
Com esta versão, atualizámos o assistente de perfil VPN e as páginas de propriedades para exibir as definições apropriadas para a plataforma selecionada. Mais concretamente:

- Cada plataforma tem o seu próprio fluxo de trabalho, o que significa que os novos perfis VPN contêm apenas a definição suportada pela plataforma.
- As páginas **das Plataformas Suportadas** aparecem agora após a página **geral.**  Agora escolhe a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida para **Android**, **Android for Work**, ou Windows Phone **8.1**, a página de **plataformas suportadas** não é necessária e não é exibida.
- O fluxo de trabalho baseado no cliente do Gestor de Configuração foi combinado com os fluxos de trabalho do Dispositivo Móvel Híbrido (MDM) baseados no cliente do Windows 10; suportam as mesmas configurações.
- Cada fluxo de trabalho da plataforma inclui apenas as definições adequadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém configurações adequadas para Android; As definições adequadas para iOS ou Windows 10 Mobile já não aparecem no fluxo de trabalho Android.
- Para dispositivos Windows 8.1, as definições geridas pelo Gestor de Configuração estão claramente marcadas.
- A página VPN automática é obsoleta e foi removida.

Estas alterações aplicam-se aos novos perfis VPN.  

Para minimizar o risco de compatibilidade, os perfis VPN existentes são inalterados.  Quando edita um perfil existente, as definições aparecem como quando o perfil foi criado.  

### <a name="try-it-out"></a>Experimente!

Crie um novo perfil VPN utilizando o processo habitual. Note que a primeira página das opções do assistente de perfil VPN mudou.

1. Aceda a **Ativos e Conformidade** > **Visualizar** > **Definições** > de Conformidade Os**perfis VPN** de acesso > a recursos da**empresa**e, em seguida, escolha Criar **perfil VPN**.
2. Introduza um nome na página **geral** e escolha uma das seguintes opções em **especificar o tipo de perfil VPN que pretende criar:**

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS e macOS  
    - Android  
    - Android for Work  

3. Se escolher o **Windows 8.1,** também tem a opção de **Criar novo perfil** ou Importar a partir do **ficheiro**.
4. Complete o assistente para terminar de criar o perfil.

Ao selecionar diferentes plataformas, note que apenas as definições relevantes para o ecrã da plataforma selecionada.

## <a name="co-management-for-windows-10-devices"></a>Cogestão para os dispositivos com Windows 10    
<!-- 1350871 -->
Muitos clientes querem gerir os dispositivos do Windows 10 da mesma forma que gerem dispositivos móveis utilizando uma solução simplificada, de baixo custo e baseada na nuvem. No entanto, fazer a transição da gestão tradicional para a gestão moderna pode ser um desafio. A partir do Windows 10, versão 1607 (também conhecido como Atualização de Aniversário), pode juntar-se a um dispositivo Windows 10 para o Ative Directory (AD) e azure AD baseado na nuvem ao mesmo tempo (AD Azure híbrido). A cogestão tira partido desta melhoria e permite-lhe gerir simultaneamente os dispositivos do Windows 10 utilizando tanto o Gestor de Configuração como o Intune. É uma solução que fornece uma ponte da gestão tradicional à gestão moderna e lhe dá um caminho para fazer a transição usando uma abordagem faseada. 

### <a name="prerequisites"></a>Pré-requisitos
Deve ter os seguintes pré-requisitos em vigor antes de poder permitir a cogestão. Existem pré-requisitos gerais, e diferentes pré-requisitos para clientes e dispositivos do Gestor de Configuração existentes que não são clientes.

### <a name="known-issues"></a>Problemas conhecidos
Depois de criar uma política de cogestão, não pode editar a política. Para alterar a política, apague-a e recriá-la com as definições de que necessita. 

#### <a name="general-prerequisites"></a>Pré-requisitos gerais
Seguem-se os pré-requisitos gerais para que permita a cogestão:  

- Pré-visualização técnica para a versão 1709 do Gestor de Configuração
- Azure AD 
- Licença EMS ou Intune para todos os utilizadores
- Subscrição intonizada &#40;autoridade do MDM em Intune definida para **Intune**&#41;

   > [!Note]  
   > Se tiver um ambiente híbrido de MDM (Intune integrado com o Gestor de Configuração), não pode permitir a cogestão.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Pré-requisitos adicionais para os clientes do Gestor de Configuração existentes
- Windows 10, versão 1709 (Atualização de Criadores de outono) e mais tarde
- Hybrid Azure AD juntou-se (juntou-se à AD e Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Pré-requisitos adicionais para novos dispositivos Windows 10
- Windows 10, versão 1709 (Atualização de Criadores de outono) e mais tarde
- [Gateway de gestão de nuvem](../clients/manage/manage-clients-internet.md#cloud-management-gateway) em gestor de configuração

### <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho pode mudar para Intune
Depois de ativar a cogestão, o Gestor de Configuração continua a gerir todas as cargas de trabalho. Quando decidir que está pronto, pode ter Intune a gerir as cargas de trabalho disponíveis. Nesta versão, pode ter Intune a gerir as seguintes cargas de trabalho.   

#### <a name="compliance-policies"></a>Políticas de conformidade
As políticas de conformidade definem as regras e configurações que um dispositivo deve cumprir para serem consideradas conformes pelas polícias de acesso condicional. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional.

#### <a name="windows-update-for-business-policies"></a>Atualização do Windows para políticas empresariais
O Windows Update for Business permite configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridas diretamente pelo Windows Update for Business. Para mais detalhes, consulte [Configure Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remotas disponíveis em Intune em Azure para dispositivos cogeridos
Quando um dispositivo Windows 10 está ativado para cogestão, tem as seguintes ações remotas disponíveis a partir de Intune no Azure:  
- [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Limpeza seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar o dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Novo começo](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Prepare intune para cogestão
Antes de mudar as cargas de trabalho do Gestor de Configuração para Intune, crie os perfis e políticas de que necessita em Intune para garantir que os seus dispositivos continuam protegidos.
Pode criar objetos em Intune com base nos objetos que tem no 'Gestor de Configuração'. Ou, se a sua estratégia atual se baseia no legado ou na gestão tradicional, talvez queira dar um passo atrás para repensar que políticas e perfis precisa para uma gestão moderna. Utilize os seguintes recursos para criar as políticas e perfis.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Atualização do Windows para políticas empresariais](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Perfis de configuração de dispositivos](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Visão geral arquitetónica para cogestão
O diagrama seguinte fornece uma visão arquitetónica da cogestão e como se encaixa nas infraestruturas de Configuração e Intune existentes.

![Diagrama arquitetónico de cogestão](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Cenários que permitam a cogestão  
Pode ativar a cogestão de ambos os dispositivos Windows 10 inscritos no Microsoft Intune e clientes existentes do Gestor de Configuração do Windows 10. Ambos os cenários resultam em dispositivos Do Windows 10 geridos simultaneamente pelo Configuração Manager e Intune, bem como a adesão à AD e ÀA Azure.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos no Intune  
Quando os dispositivos do Windows 10 estiverem matriculados no Intune, pode instalar o cliente Do Gestor de Configuração nos dispositivos (utilizando um argumento específico de linha de comando) para preparar os clientes para a cogestão. Em seguida, permite que a cogestão a partir da consola Do Gestor de Configuração comece a mover cargas de trabalho específicas para Intune para dispositivos específicos do Windows 10.  

Para dispositivos Windows 10 que ainda não estejam matriculados em Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, pode utilizar o Windows AutoPilot para configurar o out of Box Experience (OOBE), que inclui a inscrição automática que inscreve dispositivos em Intune.  

#### <a name="configuration-manager-clients"></a>Clientes do Gestor de Configuração
Quando tiver dispositivos Windows 10 que sejam clientes do Gestor de Configuração, pode inscrever estes dispositivos e ativar a cogestão a partir da consola Do Gestor de Configuração. O Gestor de Configuração aciona a inscrição automática em Intune com base nas informações do inquilino da AD Azure.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparar os dispositivos com Windows 10 para a cogestão
Pode ativar a cogestão em dispositivos Windows 10 que se juntam à AD e À AD Azure, e matriculados em Intune e um cliente em 'Gestor de Configuração'. Para novos dispositivos Windows 10, e para dispositivos já matriculados no Intune, instale o cliente do Gestor de Configuração antes de poderem ser cogeridos. Para dispositivos Windows 10 que já são clientes do Gestor de Configuração, pode inscrever os dispositivos com Intune e ativar a cogestão na consola Do Gestor de Configuração.

#### <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar cliente do Gestor de Configuração
Crie uma aplicação em Intune para dispositivos Windows 10 que ainda não sejam clientes do Gestor de Configuração. Quando criar a aplicação nas secções seguintes, utilize a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL do gateway de gestão da nuvem ponto final*&#62;/ CCMHOSTNAME=&#60;URL do gateway de *gestão de nuvem ponto final*&#62; SMSSiteCode=&#60;*Sitecode*&#62; SMSMP=https:&#47;/&#60;*FQDN do MP*&#62; AADTENANTID=&#60;ID do inquilino *AAD*&#62; AADTENANTNAME=&#60;nome do *inquilino*&#62; AADCLIENTAPPID=&#60;*Server AppID para integração aAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*O ID* de recursos&#62;"

Por exemplo, se tivesse os seguintes valores:

- **URL da cloud management gateway ponto final auth endpoint**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilize o valor **MutualAuthPath** na **vProxy_Roles** vista SQL para o URL de valor final de gateway **de gestão de nuvem.**

- **FQDN do ponto de gestão (MP)**: sccmmp.corp.contoso.com    
- **Sitecode**: PS1    
- **ID do inquilino Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- Nome do **inquilino da AD Azure**: contoso    
- Id da **aplicação de cliente Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **Id de recurso AAD URI**: ConfigMgrServer    

  > [!Note]    
  > Utilize o valor **IdentifierUri** encontrado na vista SQL **vSMS_AAD_Application_Ex** para o valor **DE ID de Recursos AAD.**

Utilizaria a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
>Pode encontrar os parâmetros da linha de comando para o seu site utilizando os seguintes passos:     
> 1. Na consola de Gestor de Configuração, vá à **Administração** > **Visão Geral** > **da Cogestão**de**Serviços** > cloud.  
> 2. No separador Home, no grupo Gerir, escolha **a cogestão da Configuração** para abrir o Assistente de Embarque de Cogestão.    
> 3. Na página de Subscrição, clique **em Iniciar sessão** e iniciar sessão no seu inquilino Intune e, em seguida, clique em **Next**.    
> 4. Na página de Habilitação, clique em **Copiar** nos **Dispositivos inscritos na** secção Intune para copiar a linha de comando para a área de comando e, em seguida, guardar a linha de comando para usar no procedimento para criar a aplicação.  
> 5. Clique **em Cancelar** para sair do assistente.

#### <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para novos dispositivos Windows 10, pode utilizar o serviço Autopilot para configurar a experiência fora da caixa, que inclui a junção do dispositivo à AD e à Azure AD, bem como a inscrição do dispositivo em Intune. Em seguida, crie uma aplicação em Intune para implementar o cliente Do Gestor de Configuração.  
1. Ativar o AutoPilot para os novos dispositivos Windows 10. Para mais detalhes, consulte a [visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure a inscrição automática em Azure AD para que os seus dispositivos sejam automaticamente matriculados no Intune. Para mais detalhes, consulte [Os dispositivos Do Windows para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Crie uma aplicação em Intune com o pacote de clientes do Gestor de Configuração e implemente a aplicação para dispositivos Windows 10 que pretende cogerir. Utilize a linha de comando para instalar o cliente do Gestor de [Configuração](#command-line-to-install-configuration-manager-client) quando passar pelas etapas para [instalar clientes a partir da internet utilizando o Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não matriculados no Intune ou num cliente do Gestor de Configuração
Para dispositivos Windows 10 que não estejam matriculados no Intune ou que tenham o cliente do Gestor de Configuração, pode utilizar a inscrição automática para inscrever o dispositivo em Intune. Em seguida, crie uma aplicação em Intune para implementar o cliente Do Gestor de Configuração.
1. Configure a inscrição automática em Azure AD para que os seus dispositivos sejam automaticamente matriculados no Intune. Para mais detalhes, consulte [Os dispositivos Do Windows para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Crie uma aplicação em Intune com o pacote de clientes do Gestor de Configuração e implemente a aplicação para dispositivos Windows 10 que pretende cogerir. Utilize a linha de comando para instalar o cliente do Gestor de [Configuração](#command-line-to-install-configuration-manager-client) quando passar pelas etapas para [instalar clientes a partir da internet utilizando o Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 matriculados em Intune
Para dispositivos Windows 10 já matriculados no Intune, crie uma aplicação em Intune para implementar o cliente Do Gestor de Configuração. Utilize a linha de comando para instalar o cliente do Gestor de [Configuração](#command-line-to-install-configuration-manager-client) quando passar pelas etapas para [instalar clientes a partir da internet utilizando o Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune
Na secção anterior, preparou dispositivos Windows 10 para cogestão. Estes dispositivos estão agora associados à AD e à AD Azure, estando matriculados em Intune e com o cliente do Gestor de Configuração. É provável que ainda tenha dispositivos Windows 10 que se juntem à AD e tenham o cliente do Gestor de Configuração, mas que não se juntem ao Azure AD ou matriculados no Intune. O procedimento seguinte fornece os passos para permitir a cogestão, preparar o resto dos seus dispositivos Windows 10 (Clientes De Gerente de Configuração sem inscrição Intune) para cogestão, e permite-lhe começar a mudar cargas específicas do Gestor de Configuração para Intune.

1. Na consola de Gestor de Configuração, vá à **Administração** > **Visão Geral** > **da Cogestão**de**Serviços** > cloud.    
2. No separador Home, no grupo Gerir, escolha **a cogestão da Configuração** para abrir o Assistente de Embarque de Cogestão.    
3. Na página de Subscrição, clique **em Iniciar sessão** e iniciar sessão no seu inquilino Intune e, em seguida, clique em **Next**.   
4. Na página de Encenação, configure as seguintes definições e, em seguida, clique **em Seguinte:**
    - **Grupo piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte do seu lançamento faseado de cogestão. Pode começar com uma pequena coleção de testes e, em seguida, adicionar mais coleções ao grupo piloto à medida que lança a cogestão a mais utilizadores e dispositivos. Pode alterar as coleções do grupo piloto a qualquer momento a partir das propriedades de cogestão.
    - **Produção**: Quando selecionar esta definição, todos os dispositivos suportados pelo Windows 10 estão ativados para cogestão. Configure o **grupo Exclusão** com uma ou mais coleções. Os dispositivos que sejam membros de qualquer uma das coleções deste grupo estão excluídos da utilização da cogestão. 
5. Na página de Habilitação, escolha **piloto** ou **tudo** (dependendo das definições configuradas na página de encenação) para ativar a inscrição automática no Intune e, em seguida, clique em **Seguinte**. Quando escolher o **Pilot**, apenas os clientes do gestor de configuração que são membros do grupo Piloto estão automaticamente matriculados no Intune. Isto permite-lhe permitir a cogestão de um subconjunto de clientes para testar inicialmente a cogestão e a cogestão do rollout usando uma abordagem faseada. 
6. Na página Workloads, escolha se muda as cargas de trabalho do Gestor de Configuração para ser gerida por Intune e, em seguida, clique em **Seguinte**. Utilize os sliders para selecionar se muda a carga de trabalho para o grupo Piloto ou para todos os clientes do Windows 10 (dependendo das definições configuradas na página de Encenação). 
7. Para permitir a cogestão, complete o assistente.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Consulte também
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md). 
