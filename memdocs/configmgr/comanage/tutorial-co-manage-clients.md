---
title: Tutoriais&#58; Permitir a cogestão dos clientes existentes
titleSuffix: Configuration Manager
description: Configure a cogestão com a Microsoft Intune quando já gere os dispositivos do Windows 10 com o Configurmanager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 918df2cded3fad48352fff6a2617b1133540c0eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712429"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Ativar a cogestão dos clientes existentes do Gestor de Configuração

Com a cogestão, pode manter os seus processos bem estabelecidos para usar o Gestor de Configuração para gerir Computadores na sua organização. Ao mesmo tempo, está a investir na nuvem através do uso de Intune para a segurança e o fornecimento moderno.  

Neste tutorial, configura a cogestão dos seus dispositivos Windows 10 que já estão inscritos no Gestor de Configuração. Este tutorial começa com a premissa de que já utiliza o 'Configuração Manager' para gerir os seus dispositivos Windows 10.

Utilize este tutorial quando:  

- Tem um Diretório Ativo no local que pode ligar ao Azure Ative Directory (Azure AD) numa configuração híbrida do Azure AD.

  Se não conseguir implementar um Azure Ative Directory híbrido (AD) que se junte ao seu AD no local com o Azure AD, recomendamos seguir o nosso tutorial companheiro, [Enable co-management para novos dispositivos Windows 10 baseados na Internet.](tutorial-co-manage-new-devices.md)
- Tem clientes de Gestor de Configuração existentes que pretende anexar em nuvem.

**Neste tutorial irá:**  
> [!div class="checklist"]
> * Reveja os pré-requisitos para o Azure e o seu ambiente no local
> * Configurar o Azure AD híbrido  
> * Configure Agentes clientes do Gestor de Configuração para se registar em Azure AD  
> * Configure Intune para dispositivos de inscrição automática  
> * Ativar a cogestão no Gestor de Configuração  

## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Serviços e ambiente azure

- Assinatura Azure[(teste gratuito)](https://azure.microsoft.com/free)
- Azure Active Directory Premium
- Subscrição do Microsoft Intune
  > [!TIP]  
  > Uma subscrição de Mobilidade Empresarial + Segurança (EMS) inclui tanto o Azure Ative Directory Premium como o Microsoft Intune. Subscrição EMS[(teste gratuito).](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)  

Se não estiver já presente no seu ambiente, durante este tutorial irá:

- Configure [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre o seu Diretório Ativo no local e o seu inquilino azure Ative Directory (AD).

> [!TIP]
> Já não precisa de adquirir e atribuir licenças individuais intune ou EMS aos seus utilizadores. Para mais informações, consulte o [Produto e licenciando as FAQ.](../core/understand/product-and-licensing-faq.md#bkmk_mem)

### <a name="on-premises-infrastructure"></a>Infraestrutura no local

- Uma [versão suportada](../core/servers/manage/updates.md#supported-versions) do ramo atual do Gestor de Configuração
- A autoridade de gestão de dispositivos móveis (MDM) deve ser definida para Intune.  

### <a name="permissions"></a>Permissões

Ao longo deste tutorial, utilize as seguintes permissões para completar tarefas:

- Uma conta que é *administradora global* no Azure Ative Directory (Azure AD) 
- Uma conta que é um administrador de *domínio* na sua infraestrutura no local  
- Uma conta que é um *administrador completo* para *todos os* âmbitos no Gestor de Configuração

## <a name="set-up-hybrid-azure-ad"></a>Configurar o Azure AD híbrido

Ao configurar um Azure AD híbrido, está realmente a criar uma integração de um AD no local com a Azure AD utilizando o Azure AD Connect e os Ative Directory Federated Services (ADFS). Com uma configuração bem sucedida, os seus trabalhadores podem iniciar sem problemas o acesso a sistemas externos utilizando as suas credenciais ad.

> [!IMPORTANT]  
> Este tutorial detalha um processo de ossos nus para configurar o Azure AD híbrido para um domínio gerido. Recomendamos que esteja familiarizado com o processo e não confie neste tutorial como seu guia para compreender e implementar a AD Azure híbrida.
>
> Para mais informações sobre o Azure AD híbrido, comece com os seguintes artigos na documentação do Diretório Ativo Azure:
>
> - [Planear a sua implementação de associação do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Planear a sua implementação de associação ao Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Controlar a associação híbrida do Azure AD dos seus dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Configurar a associação híbrida do Azure AD para os domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Configurar o Azure AD Connect

O Hybrid Azure AD requer a configuração do Azure AD Connect para manter as contas de computador no seu Diretório Ativo (AD) no local e o objeto do dispositivo em Azure AD em sincronização.

A partir da versão 1.1.819.0, o Azure AD Connect fornece um assistente para configurar a associação do Azure AD híbrido. A utilização desse assistente simplifica o processo de configuração.  

Para configurar o Azure AD Connect, precisa de credenciais de um administrador global para o Azure AD.  

> [!TIP]  
> O procedimento seguinte não deve ser considerado autoritário para a criação do Azure AD Connect, mas é fornecido aqui para ajudar a simplificar a configuração da cogestão entre Intune e O Gestor de Configuração. Para obter o conteúdo autoritário sobre este conteúdo e procedimentos conexos para a criação de Azure AD, consulte a [Configuração híbrida Azure AD para domínios geridos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) na documentação da AD Azure.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configure um Azure AD híbrido aderir usando Azure AD Connect

1. Obtenha e instale a [versão mais recente do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou superior).  
2. Lance o Azure AD Connect e, em seguida, **selecione Configurar**.
3. Na página de **tarefas Adicionais,** **selecione configurar as opções**do dispositivo , e, em seguida, selecione **Next**.
4. Na página **'Visão Geral',** selecione **Next**.
5. Na página **De Ligação ao Azure,** introduza as credenciais de um administrador global para a Azure AD.
6. Na página opções do **Dispositivo,** selecione **Configure Hybrid Azure AD join**, e, em seguida, selecione **Next**.
7. Na página dos **sistemas operativos do Dispositivo,** selecione os sistemas operativos utilizados pelos dispositivos no seu ambiente de Diretório Ativo e, em seguida, selecione **Next**.  

   Pode selecionar a opção de suportar dispositivos de domínio de nível inferior do Windows, mas lembre-se que a cogestão de dispositivos só é suportada para o Windows 10.
8. Na página **SCP,** para cada floresta no local, pretende-se que o Azure AD Connect configure o ponto de ligação de serviço (SCP), faça os seguintes passos e, em seguida, selecione **Seguinte:**  
   1. Selecione a floresta.  
   2. Selecione o serviço de autenticação.  Se tiver um domínio federado, selecione servidor AD FS a menos que a sua organização tenha clientes exclusivamente Do Windows 10 e tenha configurado a sincronização de computador/dispositivo ou a sua organização esteja a utilizar [o SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Clique em **Adicionar** para introduzir as credenciais de administrador da empresa.  
9. Se tiver um domínio gerido, ignore este passo.  

   Na página de configuração da **Federação,** introduza as credenciais do seu administrador AD FS e, em seguida, selecione **Next**.
10. Na página **Ready to configure,** selecione **Configure**.
11. Na página completa da **Configuração,** selecione **Saída**.

Se tiver problemas com a conclusão do Hybrid Azure AD para dispositivos Windows unidos por domínio, consulte a adesão híbrida azure a [um dos dispositivos atuais do Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Configure as Definições de Cliente para direcionar os clientes a registarem-se com a AD Azure

Utilize as Definições do Cliente para configurar os clientes do Gestor de Configuração para registar-se automaticamente com o Azure AD.  

1. Abra as**definições**do Cliente de**visão geral** > da**administração** > do Gestor > de **Configuração**e, em seguida, edite as **Definições padrão do cliente**.  

2. Selecione **Serviços cloud**.  

3. Na página **Definições Predefinidas,** delineie **automaticamente o registo de novos dispositivos de domínio Windows 10 com o Diretório Ativo Azure** para = **Sim**.  

4. Selecione **OK** para guardar esta configuração.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configure a inscrição automática de dispositivos para Intune

Em seguida, vamos configurar a inscrição automática de dispositivos com Intune. Com a inscrição automática, os dispositivos que gere com o Gestor de Configuração matriculam-se automaticamente com o Intune.

A inscrição automática também permite que os utilizadores matriculem os seus dispositivos Windows 10 para Intune. Os dispositivos matriculam-se quando um utilizador adiciona a sua conta de trabalho ao seu dispositivo pessoalmente propriedade, ou quando um dispositivo corporativo é unido ao Azure Ative Directory.  

1. Inscreva-se no [portal Azure](https://portal.azure.com/) e selecione **Azure Ative Directory** > **Mobility (MDM e MAM)** > **Microsoft Intune**.  

2. Configure o âmbito do **utilizador do MDM**. Especifique um dos seguintes para configurar quais os dispositivos dos utilizadores geridos pela Microsoft Intune e aceite as predefinições para os valores de URL.  

   - **Alguns**: Selecione os **Grupos** que podem inscrever automaticamente os seus dispositivos Windows 10  

   - **Tudo**: Todos os utilizadores podem inscrever automaticamente os seus dispositivos Windows 10

   - **Nenhum**: Desativar a inscrição automática do MDM

   > [!IMPORTANT]  
   > Se o **âmbito do utilizador MAM** e a inscrição na MDM automática (**âmbito do utilizador MDM**) estiverem ativados num grupo, apenas a MAM será ativada. Apenas a Mobile Application Management (MAM) é adicionada aos utilizadores desse grupo quando se juntam a dispositivos pessoais. Os dispositivos não estão automaticamente matriculados em MDM.  

3. Selecione **Guardar** para completar a configuração da inscrição automática.  

4. Volte à **Mobilidade (MDM e MAM)** e, em seguida, selecione **Microsoft Intune Registration**.  

    > [!NOTE]
    > Alguns inquilinos podem não ter estas opções para configurar.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** é como configura a aplicação MDM para Azure AD. **Microsoft Intune Registration** é uma aplicação específica do Azure AD que é criada quando aplica políticas de autenticação de vários fatores para a inscrição de iOS e Android. Para mais informações, consulte [Exigir autenticação de vários fatores para as matrículas](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication)do dispositivo Intune .

5. Para obter o alcance do utilizador do MDM, selecione **All**, e, em seguida, **Guardar**.  

## <a name="enable-co-management-in-configuration-manager"></a>Ativar a cogestão no Gestor de Configuração

Com configurações híbridas de configuração de anúncios de Anúncio azure e configurações de clientes do Gestor de Configuração, está pronto para ligar o interruptor e ativar a cogestão dos seus dispositivos Windows 10.  

> [!TIP]
> - Quando ativar a cogestão, atribuirá uma coleção como *grupo Piloto*. Este é um grupo que contém um pequeno número de clientes para testar as suas configurações de cogestão. Recomendamos que crie uma coleção adequada antes de iniciar o procedimento. Em seguida, pode selecionar essa coleção sem sair do procedimento para o fazer.
> - A partir da versão 1906 do Gestor de Configuração, poderá necessitar de várias coleções, uma vez que pode atribuir um *grupo Piloto* diferente para cada carga de trabalho.

### <a name="enable-co-management-starting-in-version-1906"></a>Permitir a cogestão a partir da versão 1906

Para permitir a cogestão a partir da versão 1906 do Gestor de Configuração, siga as instruções abaixo:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Permitir a cogestão na versão 1902 e anterior

Para permitir a cogestão para a versão 1902 e anterior do Gestor de Configuração, siga as instruções abaixo:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Passos seguintes

- Reveja o estado dos dispositivos cogeridos com o painel de [cogestão](how-to-monitor.md)
- Comece a obter [valor imediato](quickstarts.md#immediate-value) da cogestão
- Utilizar [regras de acesso condicional](quickstart-conditional-access.md) e conformidade insinapara gerir o acesso dos utilizadores aos recursos corporativos
