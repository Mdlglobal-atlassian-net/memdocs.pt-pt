---
title: Utilize credenciais derivadas para dispositivos móveis no Microsoft Intune - Azure / Microsoft Docs
description: Utilize credenciais derivadas em dispositivos móveis como um método de autenticação para Intune VPN, email, perfis Wi-Fi, aplicações e S/MIME e encriptação. As credenciais derivadas são uma implementação das diretrizes do NIST para a Publicação Especial 800-157.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 5/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1b13d29f42778d73d4df4a86127b070db5dc601
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989813"
---
# <a name="use-derived-credentials-in-microsoft-intune"></a>Use credenciais derivadas no Microsoft Intune

*Este artigo aplica-se ao iOS/iPadOS, e o Android Enterprise geriu totalmente os dispositivos que executam a versão 7.0 e acima*

Num ambiente em que os cartões inteligentes são necessários para autenticação ou encriptação e assinatura, pode agora utilizar o Intune para fornecer dispositivos móveis com um certificado derivado do cartão inteligente de um utilizador. Este certificado chama-se *credencial derivada.* Intune [suporta vários emitentes credenciais derivados,](#supported-issuers)embora você possa usar apenas um único emitente por inquilino de cada vez.

As credenciais derivadas são uma implementação das diretrizes do Instituto Nacional de Normalização e Tecnologia (NIST) para credenciais de Verificação de Identidade Pessoal Derivada (PIV) como parte da Publicação Especial (SP) 800-157.

**Com a implementação de Intune:**

- O administrador intune confunde o seu inquilino para trabalhar com um emitente credencial derivado apoiado. Não é necessário configurar quaisquer definições específicas intune no sistema do emitente de credencial derivado.
- O administrador intune especifica a **credencial derivada** como método de *autenticação* para os seguintes objetos:
  
  **Para iOS/iPadOS:**
  - Tipos de perfil comuns como Wi-Fi, VPN e Email, que inclui a aplicação de correio nativo iOS/iPadOS
  - Autenticação de aplicativos
  - Assinatura e encriptação S/MIME

  **Para dispositivos geridos pela Android Enterprise:**
  - Tipos de perfil comuns como Wi-Fi e VPN
  - Autenticação de aplicativos
  
- Os utilizadores obtêm uma credencial derivada utilizando o seu cartão inteligente num computador para autenticar o emitente credencial derivado. O emitente emite então para o dispositivo móvel um certificado derivado do seu cartão inteligente.
- Após a receção do dispositivo à credencial derivada, é utilizado para autenticação e para a assinatura e encriptação S/MIME quando apps ou perfis de acesso a recursos requerem a credencial derivada.

## <a name="prerequisites"></a>Pré-requisitos

Reveja as seguintes informações antes de configurar o seu inquilino para utilizar credenciais derivadas.

### <a name="supported-platforms"></a>Plataformas suportadas

Intune suporta credenciais derivadas nas seguintes plataformas:

- iOS/iPadOS
- Android Enterprise - dispositivos totalmente geridos (versão 7.0 e acima)

### <a name="supported-issuers"></a>Emitentes apoiados

Intune apoia um único emitente de credencial derivado por inquilino. Pode configurar insintonização para trabalhar com os seguintes emitentes:

- **DISA Purebred** (apenas iOS):https://public.cyber.mil/pki-pke/purebred/
- **Cartão de dados de confiar:**https://www.entrustdatacard.com/
- **Interceto:**https://www.intercede.com/

Para detalhes importantes sobre a utilização dos diferentes emitentes, reveja as orientações para esse emitente. Para mais informações, consulte [o Plano de Credenciais derivadas](#plan-for-derived-credentials) neste artigo.

> [!IMPORTANT]
> Se eliminar um emitente credencial derivado do seu inquilino, as credenciais derivadas que foram criadas através desse emitente deixarão de funcionar.
>
> Consulte [a Alteração do emitente credencial derivado](#change-the-derived-credential-issuer) mais tarde neste artigo.

### <a name="company-portal-app"></a>Aplicação do Portal da Empresa

Planeie implementar a aplicação Intune Company Portal para dispositivos que se inscrevam para uma credencial derivada. Os utilizadores de dispositivos utilizam a aplicação Portal da Empresa para iniciar o processo de inscrição credencial.

- Para dispositivos iOS, consulte [adicionar aplicações de loja iOS ao Microsoft Intune](../apps/store-apps-ios.md).
- Para dispositivos Android, consulte [adicionar aplicativos de loja Android para Microsoft Intune](../apps/store-apps-android.md).

## <a name="plan-for-derived-credentials"></a>Plano de credenciais derivadas

Compreenda as seguintes considerações antes de criar um emitente credencial derivado.

### <a name="1-review-the-documentation-for-your-chosen-derived-credential-issuer"></a>1) Reveja a documentação do seu emitente credencial derivado escolhido

Antes de configurar um emitente, reveja a documentação desse emitente para entender como o seu sistema fornece credenciais derivadas aos dispositivos.

Dependendo do emitente que escolher, poderá necessitar de pessoal disponível no momento da inscrição para ajudar os utilizadores a completar o processo. Consulte também as configurações intune atuais para garantir que não bloqueiam o acesso necessário para que dispositivos ou utilizadores completem o pedido de credencial.

Por exemplo, pode utilizar acesso condicional para bloquear o acesso a e-mail para dispositivos não conformes. Se contar com notificações de e-mail para informar o utilizador para iniciar o processo de inscrição credencial derivado, os seus utilizadores podem não receber essas instruções até que estejam em conformidade com a política.

Da mesma forma, alguns fluxos de trabalho de pedido de credencial derivados requerem a utilização da câmara do dispositivo para digitalizar um código QR no ecrã. Este código liga esse dispositivo ao pedido de autenticação que ocorreu contra o emitente credencial derivado com as credenciais de cartão inteligente do utilizador. Se a configuração do dispositivo bloquear o uso da câmara, o utilizador não pode completar o pedido de inscrição credencial derivado.

**Informações gerais:**

- Você só pode configurar um único emitente por inquilino de cada vez, e esse emitente está disponível para todos os utilizadores e dispositivos suportados no seu inquilino.

- Os utilizadores não serão notificados de que devem inscrever-se para credenciais derivadas até que as direcionem com uma política que exija credenciais derivadas.

- A notificação pode ser através da notificação de apps para o Portal da Empresa, através de e-mail, ou ambos. Se optar por utilizar notificações de e-mail e utilizar o acesso condicional habilitado, os utilizadores podem não receber a notificação por e-mail se o seu dispositivo não estiver em conformidade.

### <a name="2-review-the-end-user-workflow-for-your-chosen-issuer"></a>2) Reveja o fluxo de trabalho do utilizador final para o seu emitente escolhido

Seguem-se considerações fundamentais para cada parceiro apoiado.  Familiarize-se com esta informação para que possa garantir que as suas políticas e configurações intune não bloqueiem os utilizadores e dispositivos de completar em sucesso a inscrição para uma credencial derivada desse emitente.

#### <a name="disa-purebred"></a>DISA Purebred

Reveja o fluxo de trabalho específico do utilizador para os dispositivos que utilizará com credenciais derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-disa-purebred)
- [Dispositivos geridos pela Android Enterprise](https://docs.microsoft.com/mem/intune/user-help/enroll-android-device-disa-purebred)

**Os requisitos-chave incluem:**

- Os utilizadores precisam de acesso a um computador ou quiosque onde possam usar o seu cartão inteligente para autenticar o emitente.
- Os dispositivos que se inscreverão para uma credencial derivada devem instalar a aplicação Intune Company Portal.
- Utilize o Intune para [implementar a aplicação DISA Purebred](#deploy-the-disa-purebred-app) em dispositivos que se inscrevam para uma credencial derivada. Esta aplicação deve ser implementada através do Intune para que seja gerida e possa depois trabalhar com a aplicação Intune Company Portal. Esta aplicação é utilizada pelos utilizadores do dispositivo para completar o pedido de credencial derivado.
- A aplicação DISA Purebred requer uma [VPN por app](../configuration/vpn-settings-configure.md) para garantir que a aplicação pode aceder a DISA Purebred durante a inscrição para a credencial derivada.
- Os utilizadores do dispositivo devem trabalhar com um agente vivo durante o processo de inscrição. Durante a inscrição, são fornecidas códigos de acesso únicos limitados ao utilizador à medida que prosseguem através do processo de inscrição.
- Quando são feitas alterações a uma política que utiliza credenciais derivadas, como a criação de um novo perfil Wi-Fi, os utilizadores do iOS e iPadOS são notificados para abrir a aplicação Portal da Empresa.
- Os utilizadores são notificados para abrir em caso de renovação da sua credencial derivada.

Para obter informações sobre a obtenção e configuração da app DISA Purebred, consulte [A aplicação DISA Purebred](#deploy-the-disa-purebred-app) mais tarde neste artigo.

#### <a name="entrust-datacard"></a>Entrust Datacard

Reveja o fluxo de trabalho específico do utilizador para os dispositivos que utilizará com credenciais derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-entrust-datacard)
- [Dispositivos geridos pela Android Enterprise](../user-help/enroll-android-device-entrust-datacard.md)

**Os requisitos-chave incluem:**

- Os utilizadores precisam de acesso a um computador ou quiosque onde possam usar o seu cartão inteligente para autenticar o emitente.
- Os dispositivos que se inscreverão para uma credencial derivada devem instalar a aplicação Intune Company Portal.
- Utilização de uma câmara de dispositivo para digitalizar um código QR que ligue o pedido de autenticação ao pedido de credencial derivado do dispositivo móvel.
- Os utilizadores são solicitados pela aplicação Portal da Empresa ou por e-mail para se inscreverem para credenciais derivadas.
- Quando são feitas alterações a uma política que utiliza credenciais derivadas, como a criação de um novo perfil Wi-Fi:
  - **iOS e iPadOS** - Os utilizadores são notificados para abrir a aplicação Portal da Empresa.
  - **Dispositivos geridos pela Android Enterprise** - A aplicação Portal da Empresa não precisa de ser aberta.
- Os utilizadores são notificados para abrir em caso de renovação da sua credencial derivada.

#### <a name="intercede"></a>Interceto

Reveja o fluxo de trabalho específico do utilizador para os dispositivos que utilizará com credenciais derivadas.

- [iOS e iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-intercede)
- [Dispositivos geridos pela Android Enterprise](../user-help/enroll-android-device-intercede.md)

**Os requisitos-chave incluem:**

- Os utilizadores precisam de acesso a um computador ou quiosque onde possam usar o seu cartão inteligente para autenticar o emitente.
- Os dispositivos que se inscreverão para uma credencial derivada devem instalar a aplicação Intune Company Portal.
- Utilização de uma câmara de dispositivo para digitalizar um código QR que ligue o pedido de autenticação ao pedido de credencial derivado do dispositivo móvel.
- Os utilizadores são solicitados pela aplicação Portal da Empresa ou por e-mail para se inscreverem para credenciais derivadas.
- Quando são feitas alterações a uma política que utiliza credenciais derivadas, como a criação de um novo perfil Wi-Fi:
  - **iOS e iPadOS** - Os utilizadores são notificados para abrir a aplicação Portal da Empresa.
  - **Dispositivos geridos pela Android Enterprise** - A aplicação Portal da Empresa não precisa de ser aberta.
- Os utilizadores são notificados para abrir em caso de renovação da sua credencial derivada.

### <a name="3-deploy-a-trusted-root-certificate-to-devices"></a>3) Implementar um certificado de raiz fidedigno para dispositivos

É utilizado um certificado de raiz fidedigno com credenciais derivadas para verificar se a cadeia de certificados de credencial derivada é válida e fidedigna. Mesmo quando não é diretamente referenciado pela política, é necessário um certificado de raiz fidedigno. Consulte configurar um perfil de [certificado para os seus dispositivos no Microsoft Intune](certificates-configure.md).

### <a name="4-provide-end-user-instructions-for-how-to-get-the-derived-credential"></a>4) Fornecer instruções sobre como obter a credencial derivada

Crie e forneça orientações aos seus utilizadores sobre como iniciar o processo de inscrição credencial derivado e navegar-lhe o fluxo de trabalho de inscrição credencial derivado para o seu emitente escolhido.

Recomendamos que forneça um URL que apresente a sua orientação. Especifica este URL quando configura o emitente credencial derivado para o seu inquilino, e esse URL é disponibilizado a partir da aplicação Portal da Empresa. Se não especificar o seu próprio URL, intune fornece um link para detalhes genéricos. Estes detalhes não podem cobrir todos os cenários e podem não ser precisos para o seu ambiente.

### <a name="dive-idsupported-objects-5-deploy-intune-policies-that-require-derived-credentials"></a><dive id="supported-objects">5) Implementar políticas intune que requerem credenciais derivadas

Crie novas políticas ou edite as políticas existentes para usar credenciais derivadas. As credenciais derivadas substituem outros métodos de autenticação pelos seguintes objetos:

- Autenticação de aplicativos
- Wi-Fi
- VPN
- e-mail (apenas iOS)
- Assinatura e encriptação S/MIME, incluindo Outlook (apenas iOS)

Evite exigir a utilização de uma credencial derivada para aceder a um processo que utilizará como parte do processo para obter a credencial derivada, uma vez que isso pode impedir que os utilizadores completem o pedido.

## <a name="set-up-a-derived-credential-issuer"></a>Criar um emitente credencial derivado

Antes de criar políticas que exijam a utilização de uma credencial derivada, crie um emitente credencial na consola Intune. Um emitente credencial derivado é um cenário em todo o inquilino. Os inquilinos apoiam apenas um único emitente de cada vez.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Tenant administration**  >  **Conectores e fichas**de administração do  >  **Derived Credentials**Inquilino.

    > [!div class="mx-imgBorder"]
    > ![Configure credenciais derivadas na consola](./media/derived-credentials/configure-provider.png)

3. Especifique um nome de **exibição** amigável para a política de emitente de credencial derivada.  Este nome não é mostrado aos utilizadores do seu dispositivo.

4. Para o **emitente credencial derivado,** selecione o emitente credencial derivado que escolheu para o seu inquilino:
   - DISA Purebred (apenas iOS)
   - Entrust Datacard
   - Interceto  

5. Especifique um URL de **ajuda credencial derivada** para fornecer um link para um local que inclui instruções personalizadas para ajudar os utilizadores a obter credenciais derivadas para a sua organização. As instruções devem ser específicas da sua organização e do fluxo de trabalho necessário para obter uma credencial do seu emitente escolhido. O link aparece na aplicação Portal da Empresa e deve estar acessível a partir do dispositivo.

   Se não especificar o seu próprio URL, intune fornece um link para detalhes genéricos que não podem cobrir todos os cenários. Esta orientação genérica pode não ser exata para o seu ambiente.

6. Selecione uma ou mais opções para o tipo de **Notificação**. Os tipos de notificação são os métodos que utiliza para informar os utilizadores sobre os seguintes cenários:

   - Inscreva um dispositivo com um emitente para obter uma nova credencial derivada.
   - Obtenha uma nova credencial derivada quando a credencial atual estiver perto de expirar.
   - Utilize uma credencial derivada com um [objeto suportado](#supported-objects).

7. Quando estiver pronto, selecione **Guardar** para completar a configuração do emitente credencial derivado.

Depois de guardar a configuração, pode fazer alterações em todos os campos, exceto no *emitente de credencial Derivado*.  Para alterar o emitente, consulte [Alterar o emitente credencial derivado](#change-the-derived-credential-issuer).

## <a name="deploy-the-disa-purebred-app"></a>Implementar a app DISA Purebred

*Esta secção só se aplica quando utiliza O Puro-Sangue DISA*.

Para utilizar o **DISA Purebred** como seu emitente credencial derivado para Intune, você deve obter a app DISA Purebred e, em seguida, usar Intune para implementar a app em dispositivos. Os utilizadores do dispositivo utilizam a aplicação no seu dispositivo para solicitar a credencial derivada da DISA Purebred.

Além da implementação da aplicação com Intune, configure uma VPN intune por app para a aplicação DISA Purebred.

**Complete as seguintes tarefas:**
  
1. Descarregue a aplicação DISA Purebred: https: \/ /cyber.mil/pki-pke/purebred/.

2. Implementar a aplicação DISA Purebred em Intune. 

   - Consulte [adicionar uma aplicação iOS de linha de negócio sintetizador a Microsoft Intune](../apps/lob-apps-ios.md).
   - Ver [Adicionar uma aplicação de linha de negócios Android à Microsoft Intune](../apps/lob-apps-android.md)

3. [Crie uma VPN por app](../configuration/vpn-settings-configure.md) para a aplicação DISA Purebred.

## <a name="use-derived-credentials-for-authentication-and-smime-signing-and-encryption"></a>Utilize credenciais derivadas para autenticação e assinatura e encriptação S/MIME

Pode especificar **a credencial derivada** para os seguintes tipos e propósitos de perfil:

- [Aplicações](#use-derived-credentials-for-app-authentication)
- Email (E-mail):
  - [iOS e iPadOS](../configuration/email-settings-ios.md)
  - [Android Enterprise](../configuration/email-settings-android-enterprise.md)
- VPN:
  - [iOS e iPadOS](../configuration/vpn-settings-ios.md)
  - [Android Enterprise](../configuration/vpn-settings-android-enterprise.md)
- [Assinatura e encriptação S/MIME](certificates-s-mime-encryption-sign.md)
- Wi-Fi:
  - [iOS e iPadOS](../configuration/wi-fi-settings-ios.md)
  - [Android Enterprise](../configuration/wi-fi-settings-android-enterprise.md)

  Para perfis Wi-Fi, o método de *autenticação* só está disponível quando o **tipo EAP** estiver definido para um dos seguintes valores:
  - EAP - TLS
  - EAP-TTLS
  - PEAP

### <a name="use-derived-credentials-for-app-authentication"></a>Utilize credenciais derivadas para autenticação de apps

Utilize credenciais derivadas para autenticação baseada em certificados em web sites e aplicações. Para entregar uma credencial derivada para autenticação de aplicações:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes definições:

   Para iOS e iPadOS:
   - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **credencial derivada para o perfil de dispositivos iOS**.
   - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
   - **Plataforma**: Selecione **iOS/iPadOS**.
   - **Tipo de perfil**: Selecione **credencial derivada**.

   Para Android Enterprise:
   - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é **credencial derivada para o perfil**de dispositivos Android Enterprise .
   - **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
   - **Plataforma**: Selecione **Android Enterprise**.
   - **Tipo de perfil**: Apenas no *proprietário do dispositivo,* selecione **credencial derivada**.

4. Selecione **OK** para guardar as alterações.
5. Quando terminar, selecione **OK**  >  **Criar** para criar o perfil Intune. Quando estiver concluído, o seu perfil é mostrado na lista de perfis de configuração - **Configuração.**
6. Selecione o seu novo perfil > **Atribuições**. Selecione os grupos que devem receber a apólice.

Os utilizadores recebem a aplicação ou notificação de e-mail dependendo das definições especificadas quando configurar o emitente credencial derivado. A notificação informa o utilizador para o lançamento do Portal da Empresa para que as políticas de credenciais derivadas possam ser processadas.

## <a name="renew-a-derived-credential"></a>Renovar uma credencial derivada

As credenciais derivadas não podem ser estendidas ou renovadas. Em vez disso, os utilizadores devem utilizar o fluxo de trabalho de pedido de credencial para solicitar uma nova credencial derivada para o seu dispositivo.

Se configurar um ou mais métodos para o tipo de **Notificação,** insino notificar automaticamente os utilizadores quando a credencial derivada atual atingir 80% do seu tempo de vida útil. A notificação direciona os utilizadores a passarem pelo processo de pedido de credencial para obterem uma nova credencial derivada.

Depois de um dispositivo receber uma nova credencial derivada, as políticas que utilizam credenciais derivadas reimplantam-se para esse dispositivo.

## <a name="change-the-derived-credential-issuer"></a>Alterar o emitente credencial derivado

Ao nível do inquilino, você pode mudar o seu emitente credencial, embora apenas um emitente seja apoiado para um inquilino de cada vez.

Depois de alterar o emitente, os utilizadores são solicitados a obter uma nova credencial derivada do novo emitente. Devem fazê-lo antes de poderem utilizar uma credencial derivada para autenticação.

### <a name="change-the-issuer-for-your-tenant"></a>Mude o emitente para o seu inquilino

> [!IMPORTANT]
> Se eliminar um emitente e reconfigurar imediatamente o mesmo emitente, ainda deve atualizar perfis e dispositivos para utilizar credenciais derivadas desse emitente. As credenciais derivadas que foram obtidas antes de eliminar o emitente já não são válidas.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Tenant administration**  >  **Conectores e fichas**de administração do  >  **Derived Credentials**Inquilino.
3. **Selecione Eliminar** para remover o emitente credencial derivado da corrente.
4. Configure um novo emitente.

### <a name="update-profiles-that-use-derived-credentials"></a>Atualizar perfis que usam credenciais derivadas

Depois de apagar um emitente e, em seguida, adicionar um novo, editar cada perfil que utiliza credenciais derivadas. Esta regra aplica-se mesmo que restaure o emitente anterior. Qualquer edição do perfil irá desencadear uma atualização, incluindo uma simples edição para o perfil *Descrição*.

### <a name="update-derived-credentials-on-devices"></a>Atualizar credenciais derivadas em dispositivos

Depois de apagar um emitente e depois adicionar um novo, os utilizadores do dispositivo devem solicitar uma nova credencial derivada. Esta regra aplica-se mesmo quando adiciona o mesmo emitente que removeu. O processo de solicitação da nova credencial derivada é o mesmo que para a inscrição de um novo dispositivo ou a renovação de uma credencial existente.

## <a name="next-steps"></a>Passos seguintes

Criar perfis de configuração do [dispositivo.](../configuration/device-profile-create.md)
