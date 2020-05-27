---
title: Integrar o Windows Hello para Empresas com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Saiba como criar uma política para controlar a utilização do Windows Hello para Empresas em dispositivos geridos."
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/25/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 00f617d91541c1a580f6dec0b6b844abfc8d0d97
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990936"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integrar o Windows Hello para Empresas com o Microsoft Intune  

Pode integrar o Microsoft Hello para Empresas (anteriormente conhecido como Microsoft Passport for Work) com o Microsoft Intune.

 O Hello para Empresas é um método de início de sessão alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual. Pode utilizar um *gesto de utilizador* para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN, autenticação biométrica como o Windows Hello ou um dispositivo externo, como um leitor de impressões digitais.

O Intune integra o Hello para Empresas de duas formas:

- Pode ser criada uma política do Intune em **Inscrição de dispositivos**. Esta política destina-se a toda a organização (ao nível dos inquilinos). Suporta a experiência de configuração inicial (OOBE) do Windows AutoPilot e é aplicada quando um dispositivo é inscrito. 
- Pode ser criado um perfil de proteção de identidade em **Configuração do dispositivo**. Este perfil destina-se aos utilizadores e dispositivos atribuídos e é aplicado durante a entrada. 

Utilize este artigo para criar uma política do Windows Hello para Empresas predefinida destinada a toda a organização. Para criar um perfil de proteção de identidade utilizado para selecionar grupos de utilizadores e dispositivos, veja [Configurar um perfil de proteção de identidade](identity-protection-configure.md).  

<!--- - You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Secure resource access with certificate profiles in Microsoft Intune](secure-resource-access-with-certificate-profiles.md). --->

> [!IMPORTANT]
> Nas versões do Windows 10 para computadores e dispositivos móveis antes da Atualização de Aniversário, podia definir dois PINs diferentes que podiam ser utilizados para autenticar recursos:
> - O **PIN do dispositivo** podia ser utilizado para desbloquear o dispositivo e estabelecer ligação a recursos na cloud.
> - O PIN de **trabalho** foi utilizado para aceder aos recursos da Azure AD nos dispositivos pessoais do utilizador (BYOD).
> 
> Na Atualização de Aniversário, estes dois PINs foram unidos num único PIN do dispositivo.
> Agora, tanto as políticas de configuração do Intune que definiu para controlar o PIN do dispositivo, e adicionalmente, quaisquer políticas do Windows Hello para Empresas que tenha configurado, definem este novo valor PIN.
> Se tiver definido ambos os tipos de política para controlar o PIN, a política do Windows Hello para Empresas será aplicada tanto em computadores como em dispositivos móveis com Windows 10.
> Para garantir que os conflitos de políticas são resolvidos e que a política de PIN é aplicada corretamente, atualize a sua Política do Windows Hello para Empresas para corresponder às definições na sua política de configuração e peça aos seus utilizadores para sincronizarem os seus dispositivos na aplicação Portal da Empresa.



## <a name="create-a-windows-hello-for-business-policy"></a>Criar uma política do Windows Hello para Empresas

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vá para **dispositivos**  >   **de**  >  **inscrição Dispositivos De inscrição Dispositivos**  >  **Windows inscrição**Windows Hello for  >  **Business**. Abre o painel Windows Hello for Business.

3. Selecione entre as seguintes opções para **Configurar o Windows Hello for Business:**

    - **Desativado.** Se não pretender utilizar o Windows Hello para Empresas, selecione esta definição. Se desativado, os utilizadores não podem fornecer o Windows Hello for Business, exceto no Azure Ative Directory, onde o fornecimento pode ser necessário.
    - **Ativado**. Selecione esta definição se pretender configurar as definições do Windows Hello para Empresas.  Quando selecionar *Ativado,* as definições adicionais para WIndows Hello tornam-se visíveis.
    - **Não configurado.** Selecione esta definição se não pretender utilizar o Intune para controlar as definições do Windows Hello para Empresas. Quaisquer definições existentes do Windows Hello for Business nos dispositivos Windows 10 não são alteradas. Todas as outras definições no painel não estão disponíveis.

4. Se tiver selecionado **Ativado** no passo anterior, configure as definições obrigatórias que são aplicadas a todos os dispositivos Windows 10 e Windows 10 Mobile inscritos. Depois de configurar estas definições, selecione **Guardar**.

   - **Utilize um Módulo plataforma fidedigno (TPM)**:

     Um chip TPM fornece uma camada adicional de segurança de dados. Escolha um dos seguintes valores:

     - **Obrigatório** (predefinição). Apenas os dispositivos com um TPM acessível podem aprovisionar o Windows Hello para Empresas.
     - **Preferencial**. Os dispositivos tentam utilizar primeiro um TPM. Se esta opção não estiver disponível, podem usar encriptação de software.

   - **Comprimento mínimo pin** e **comprimento máximo pin:**

     Configura os dispositivos para utilizar os comprimentos mínimo e máximo do PIN que especificar para ajudar a garantir o início de sessão seguro. O comprimento predefinido do PIN é de seis carateres, mas pode impor um comprimento mínimo de quatro carateres. O comprimento máximo do PIN é de 127 carateres.

   - **Letras minúsculas em PIN,** **letras maiúsculas em PIN,** e **caracteres especiais em PIN**.

     Pode impor um PIN mais forte ao exigir a utilização de letras maiúsculas, letras minúsculas e carateres especiais no PIN. Para cada um, selecione a partir de:

     - **Permitido.** Os utilizadores podem usar o tipo de caracteres no seu PIN, mas não é obrigatório.

     - **Obrigatório**. Os utilizadores têm de incluir, pelo menos, um dos tipos de caráter no PIN. Por exemplo, é prática comum exigir pelo menos uma letra maiúscula e um caráter especial.

     - **Não permitido** (predefinição). Os utilizadores não devem utilizar estes tipos de carateres no seu PIN. (Este também é o comportamento se a configuração não estiver configurada.)

       Os caracteres especiais incluem: **! " # % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] _ _ &#96; { &#124; } ~**

   - **Expiração do PIN (dias)**:

     É recomendável especificar um período de expiração para um PIN, após o qual os utilizadores têm de alterá-lo. A predefinição é de 41 dias.

   - **Lembre-se da história do PIN:**

     Restringe a reutilização de PINs utilizados anteriormente. Por padrão, os últimos 5 PINs não podem ser reutilizados.

   - **Permitir a autenticação biométrica:**

     Permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como alternativa a um PIN, no Windows Hello para Empresas. Os utilizadores continuam a ter de configurar um PIN, para a eventualidade de a autenticação biométrica falhar. Escolha entre:

     - **Sim, é**um pouco. O Windows Hello para Empresas permite a autenticação biométrica.
     - **Não, não, não, não.** O Windows Hello para Empresas impede a autenticação biométrica (para todos os tipos de conta).

   - **Utilize uma maior anti-falsificação, quando disponível:**

     Desvenda se as funcionalidades anti-falsificação do Windows Hello são utilizadas em dispositivos que o suportam. Por exemplo, detetar uma fotografia de um rosto em vez de um rosto real.

     Quando definido para **Sim,** o Windows requer que todos os utilizadores utilizem anti-falsificação para funcionalidades faciais quando isso é suportado.

   - **Permitir o registo telefónico:**

     Se esta opção estiver definida como **Sim**, os utilizadores podem utilizar um passaporte remoto para servir de dispositivo complementar portátil para autenticação de computadores de secretária. O computador de secretária tem de estar associado ao Azure Active Directory e o dispositivo complementar tem de ser configurado com um PIN do Windows Hello para Empresas.

## <a name="windows-holographic-for-business-support"></a>Suporte do Windows Holographic for Business

O Windows Holographic for Business suporta as seguintes definições para Windows Hello for Business:

- Utilizar um Trusted Platform Module (TPM)
- Comprimento mínimo do PIN
- Comprimento máximo do PIN
- Letras em minúsculas no PIN
- Letras em maiúsculas no PIN
- Carateres especiais no PIN
- Expiração do PIN (dias)
- Memorizar histórico de PIN

## <a name="next-steps"></a>Passos seguintes

Para mais informações sobre o Windows Hello for Business, consulte [o guia](https://technet.microsoft.com/library/mt589441.aspx) na documentação do Windows 10.
