---
title: Configurar VPN por app para dispositivos iOS/iPadOS no Microsoft Intune - Azure Microsoft Docs
description: Consulte os pré-requisitos, crie um grupo para os utilizadores da rede privada virtual (VPN), adicione um perfil de certificado SCEP, configure um perfil VPN por app e atribua algumas aplicações ao perfil VPN no Microsoft Intune em dispositivos iOS/iPadOS. Também indica os passos para verificar a ligação VPN no dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24663f8338f03fab53369689b4a61b5bd1bec63f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83991224"
---
# <a name="set-up-per-app-virtual-private-network-vpn-for-iosipados-devices-in-intune"></a>Configurar a Rede Privada Virtual (VPN) por aplicação para dispositivos iOS/iPadOS em Intune

No Microsoft Intune, pode criar e utilizar redes privadas virtuais (VPNs) atribuídas a uma aplicação. Esta funcionalidade chama-se "VPN por app". Escolha as aplicações geridas que podem utilizar o seu VPN em dispositivos geridos pela Intune. Ao utilizar em vpNs por aplicação, os utilizadores finais conectam-se automaticamente através da VPN e têm acesso a recursos organizacionais, como documentos.

Esta funcionalidade aplica-se a:

- iOS 9 e mais recente
- iPadOS 13.0 e mais recente

Verifique a documentação do seu fornecedor VPN para ver se o seu VPN suporta VPN por app.

Este artigo mostra-lhe como criar um perfil VPN por app e atribuir este perfil às suas apps. Utilize estes passos para criar uma experiência VPN por app perfeita para os seus utilizadores finais. Para a maioria das VPNs que suportam VPN por app, o utilizador abre uma aplicação e liga-se automaticamente à VPN.

Algumas VPNs permitem o nome de utilizador e a autenticação de senha com VPN por app. Ou seja, os utilizadores precisam de introduzir um nome de utilizador e uma senha para se conectarem à VPN.

> [!IMPORTANT]
> A VPN por aplicação não é suportada para perfis VPN IKEv2 para iOS/iPadOS.

## <a name="per-app-vpn-with-zscaler"></a>VPN por app com Zscaler

A Zscaler Private Access (ZPA) integra-se com o Azure Ative Directory (Azure AD) para autenticação. Ao utilizar o ZPA, não necessita do [certificado fidedigno](#create-a-trusted-certificate-profile) ou dos perfis de [certificadoS SCEP ou PKCS](#create-a-scep-or-pkcs-certificate-profile) (descritos neste artigo). Se tiver um perfil VPN por aplicação configurado para zscaler, abrir uma das aplicações associadas não se liga automaticamente ao ZPA. Em vez disso, o utilizador precisa de assinar primeiro a aplicação Zscaler. Em seguida, o acesso remoto é limitado às aplicações associadas.

## <a name="prerequisites-for-per-app-vpn"></a>Pré-requisitos para a VPN por aplicação

> [!IMPORTANT]
> O seu fornecedor VPN pode ter outros requisitos para VPN por app, tais como hardware específico ou licenciamento. Certifique-se de que consulta a documentação do fornecedor e de que cumpre os pré-requisitos antes de configurar a VPN por aplicação no Intune.

Para provar a identidade, o servidor VPN apresenta o certificado que tem de ser aceite sem um pedido pelo dispositivo. Para confirmar a aprovação automática do certificado, crie um perfil de certificado fidedigno que inclua o certificado raiz do servidor VPN emitido pela Autoridade de Certificação (CA).

### <a name="export-the-certificate-and-add-the-ca"></a>Exportar o certificado e adicionar o CA

1. No seu servidor VPN, abra a consola de administração.
2. Confirme que o seu servidor VPN utiliza autenticação baseada em certificados. 
3. Exporte o ficheiro de certificado de raiz fidedigno. Tem uma extensão .cer e tem de adicioná-la ao criar um perfil de certificado fidedigno.
4. Adicione o nome da AC que emitiu o certificado para autenticação ao servidor VPN.

    Se o CA apresentado pelo dispositivo corresponder a um CA na lista DE Fidedigna no servidor VPN, então o servidor VPN autentica com sucesso o dispositivo.

## <a name="create-a-group-for-your-vpn-users"></a>Criar um grupo para os utilizadores de VPN

Crie ou escolha um grupo existente no Azure Ative Directory (Azure AD) para os utilizadores ou dispositivos que utilizem VPN por app. Para criar um novo grupo, consulte [grupos Add para organizar utilizadores e dispositivos](../fundamentals/groups-add.md).

## <a name="create-a-trusted-certificate-profile"></a>Criar um perfil de certificado fidedigno

Importe o certificado de raiz do servidor VPN emitido pela AC para um perfil criado no Intune. O perfil de certificado fidedigno instrui o dispositivo iOS/iPadOS a confiar automaticamente no CA que o servidor VPN apresenta.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **iOS/iPadOS**.
    - **Perfil**: Selecione **certificado fidedigno**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **iOS/iPadOS perfil VPN fidedigno para toda**a empresa .
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.
7. Nas definições de **Configuração,** selecione o ícone da pasta e navegue para o seu certificado VPN (ficheiro.cer) que exportou da sua consola de administração VPN.
8. Selecione **Next**, e continue a criar o seu perfil. Para mais informações, consulte [Criar um perfil VPN](vpn-settings-configure.md#create-the-profile).

    > [!div class="mx-imgBorder"]
    > ![Criar um perfil de certificado fidedigno para dispositivos iOS/iPadOS no Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-or-pkcs-certificate-profile"></a>Criar um perfil de certificado SCEP ou PKCS

O perfil de certificado de raiz fidedigno permite que o dispositivo confie automaticamente no Servidor VPN. O certificado SCEP ou PKCS fornece credenciais do cliente VPN iOS/iPadOS ao servidor VPN. O certificado permite que o dispositivo autentica silenciosamente sem pedir um nome de utilizador e senha. 

Para configurar e atribuir o certificado de autenticação do cliente, consulte um dos seguintes artigos:

- [Configure infraestruturas para apoiar o SCEP com Intune](../protect/certificates-scep-configure.md)
- [Configurar e gerir certificados PKCS com o Intune](../protect/certficates-pfx-configure.md)

Certifique-se de configurar o certificado para autenticação do cliente. Pode definir a autenticação do cliente diretamente nos perfis de certificadoS SCEP (lista**de utilização de chaves alargadas** > **autenticação do Cliente).** Para pKCS, detete tese de autenticação do cliente no modelo de certificado na autoridade do certificado (CA).

> [!div class="mx-imgBorder"]
> ![Criar um perfil de certificado SCEP no Microsoft Intune, incluindo formato de nome de assunto, utilização de chaves, utilização alargada de chaves e muito mais](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>Criar um perfil de VPN por aplicação

O perfil VPN inclui o certificado SCEP ou PKCS que possui as credenciais do cliente, as informações de ligação VPN e a bandeira VPN por app que permite a VPN por app utilizada pela aplicação iOS/iPadOS.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione perfis de configuração de **Devices**  >  **dispositivos**  >  **Criar perfil**.
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Plataforma**: Selecione **iOS/iPadOS**.
    - **Perfil**: Selecione **VPN**.

4. Selecione **Criar**.
5. No Básico, insira as **seguintes**propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil personalizado. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **o perfil VPN iOS/iPadOS por app para toda**a empresa .
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Nas definições de **Configuração,** configure as seguintes definições:

    - Tipo de **ligação:** Selecione a sua aplicação de cliente VPN.
    - **VpN base**: Configure as suas definições. [As definições de VPN iOS/iPadOS](vpn-settings-ios.md) listam e descrevem todas as definições. Ao utilizar VPN por app, certifique-se de que define as seguintes propriedades listadas:

      - **Método de autenticação**: Selecione **Certificados**. 
      - **Certificado de autenticação**: Selecione um certificado SCEP ou PKCS existente > **OK**.
      - **Túnel dividido**: Selecione **Desativar** para forçar todo o tráfego a utilizar o túnel VPN quando a ligação VPN estiver ativa. 

      > [!div class="mx-imgBorder"]
      > ![Num perfil VPN por aplicação, introduza uma ligação, endereço IP ou FQDN, método de autenticação e túnel dividido no Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    Para obter informações sobre as outras definições, consulte [as definições de VPN iOS/iPadOS](vpn-settings-ios.md).

    - **VPN**  >  automática **Tipo de VPN**  >  automática **VPN por app**

      > [!div class="mx-imgBorder"]
      > ![Intune, defina vpn automática para VPN por app em dispositivos iOS/iPadOS](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. Selecione **Next**, e continue a criar o seu perfil. Para mais informações, consulte [Criar um perfil VPN](vpn-settings-configure.md#create-the-profile).

## <a name="associate-an-app-with-the-vpn-profile"></a>Associar uma aplicação ao perfil VPN

Depois de adicionar o perfil VPN, associe a aplicação e o grupo do Azure AD ao perfil.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Apps**Todas  >  **as aplicações**.
2. Selecione uma aplicação da lista > **Properties**  >  **Assignments**  >  **Add grupo**.
3. No **tipo de Atribuição,** selecione **Necessário** ou **Disponível para dispositivos matriculados**.
4. Selecione **grupos**  >  **incluídos Selecione grupos para incluir** > Selecione o grupo que [criou](#create-a-group-for-your-vpn-users) (neste artigo) > **Selecione**.
5. Em **VPNs,** selecione o perfil VPN por app [que criou](#create-a-per-app-vpn-profile) (neste artigo).

    > [!div class="mx-imgBorder"]
    > ![Atribuir uma aplicação ao perfil VPN por app no Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. Selecione **OK**  >  **Guardar**.

Uma associação entre uma aplicação e um perfil é removida durante o check-in do próximo dispositivo, quando todas as seguintes condições existem:

- A aplicação foi direcionada com a intenção "Instalação obrigatória".
- O perfil e a aplicação foram direcionados para o mesmo grupo.
- Removeu a configuração da VPN por aplicação da atribuição de aplicações.

Uma associação entre uma app e um perfil persiste até que o utilizador solicite uma reinstalação do Portal da Empresa, quando existem todas as seguintes condições:

- A aplicação foi direcionada com a intenção "Instalação disponível".
- O perfil e a aplicação foram direcionados para o mesmo grupo.
- O utilizador final solicitou a instalação da aplicação no Portal da Empresa, o que resulta na instalação de apps e perfis no dispositivo.
- Removeu ou alterou a configuração da VPN por aplicação da atribuição de aplicações.

## <a name="verify-the-connection-on-the-iosipados-device"></a>Verifique a ligação no dispositivo iOS/iPadOS

Com a configuração de VPN por aplicação associada à sua aplicação, verifique se a ligação funciona a partir de um dispositivo.

### <a name="before-you-attempt-to-connect"></a>Antes de tentar estabelecer ligação

- Certifique-se de que implementa todas as políticas acima mencionadas para o mesmo grupo. Caso contrário, a experiência VPN por app não funcionará.
- Se estiver a utilizar a aplicação Pulse Secure VPN ou uma aplicação personalizada para cliente VPN, pode optar por utilizar um túnel de camada de aplicação ou de camada de pacote. Defina o valor **ProviderType** para **proxy-da-aplicação**, para o túnel de camada de aplicação ou para **pacote-túnel**, para o túnel de camada de pacote. Verifique a documentação do seu fornecedor VPN para se certificar de que está a usar o valor certo.

### <a name="connect-using-the-per-app-vpn"></a>Estabelecer ligação com a VPN por aplicação

Verifique a experiência sem contacto ao estabelecer ligação sem ter de selecionar a VPN ou escrever as suas credenciais. A experiência sem contacto significa que:

- O dispositivo não lhe pede para confiar no servidor VPN. Ou seja, o utilizador não vê a caixa de diálogo **Dynamic Trust.**
- O utilizador não tem de escrever credenciais.
- O dispositivo do utilizador está ligado à VPN quando o utilizador abre uma das aplicações associadas.

## <a name="next-steps"></a>Passos seguintes

- Para rever as definições do iOS/iPadOS, consulte [as definições vpN para dispositivos iOS/iPadOS no Microsoft Intune](vpn-settings-ios.md).
- Para saber mais sobre a definição de VPN e Intune, consulte [configurar as definições de VPN no Microsoft Intune](vpn-settings-configure.md).
