---
title: Criar um perfil de certificado no Microsoft Intune – Azure | Microsoft Docs
description: Saiba utilizar certificados e perfis de certificados simples (SCEP) ou Detrípgios de Chave Pública (PKCS) e perfis de certificado sintonizados.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ab229e0ef0d2cdefe41f991efc8c45c988979db
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80085051"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Utilize certificados para autenticação no Microsoft Intune

Utilize certificados com Intune para autenticar os seus utilizadores a aplicações e recursos corporativos através de VPN, Wi-Fi ou perfis de e-mail. Quando utiliza certificados para autenticar estas ligações, os utilizadores finais não precisarão de introduzir nomes de utilizador e palavras-passe, o que pode tornar o seu acesso sem problemas. Os certificados também são usados para a assinatura e encriptação de e-mail usando S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Certificados e utilização suportados insintonizados

| Tipo              | Autenticação | Assinatura S/MIME | Encriptação S/MIME  |
|--|--|--|--|
| Certificado importado de criptografia de chaves públicas (PKCS) |  | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png)|
| PKCS#12 (ou PFX)    | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) |  |
| Protocolo SCEP (Simple Certificate Enrollment Protocol)  | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | |

Para implementar estes certificados, irá criar e atribuir perfis de certificado aos dispositivos.

Cada perfil de certificado individual que cria suporta uma única plataforma. Por exemplo, se utilizar certificados PKCS, irá criar o perfil de certificado PKCS para Android e um perfil de certificado PKCS separado para iOS/iPadOS. Se também utilizar certificados SCEP para essas duas plataformas, irá criar um perfil de certificado SCEP para Android e outro para iOS/iPadOS.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Considerações gerais quando se utiliza uma Autoridade de Certificação da Microsoft

Quando utiliza uma Autoridade de Certificação da Microsoft (CA):

- Para utilizar os perfis de certificado SCEP, tem de configurar um servidor do Serviço de Inscrição de Dispositivos de [Rede (NDES)](certificates-scep-configure.md#set-up-ndes) para utilização com o Intune.
- Para utilizar os seguintes tipos de perfis de certificado, deve [instalar o Conector](certificates-scep-configure.md#install-the-intune-certificate-connector)de Certificado Intune da Microsoft:
  - Perfil de certificação SCEP
  - Perfil de certificado PKCS

- Utilizar certificados importados pKCS:
  - [Instale o Conector de Certificado PFX para o Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Certificados de exportação da autoridade de certificação e, em seguida, importá-los para microsoft Intune. Consulte [o projeto PFXImport PowerShell](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Utilizar certificados utilizando os seguintes mecanismos:
  - Perfis de [certificado fidedignos](certificates-configure.md#create-trusted-certificate-profiles) para implantar o certificado de AC raiz fidedigna da sua raiz ou ca intermédia (emissão) para dispositivos
  - Perfis de certificado de SCEP
  - Perfis de certificados PKCS
  - Perfis de certificados importados pKCS

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Considerações gerais quando se utiliza uma Autoridade de Certificação de Terceiros

Quando utiliza uma Autoridade de Certificação de Terceiros (não Microsoft) (CA):

- Para utilizar perfis de certificadoS SCEP:
  - Estabelecer a integração com um AC de terceiros de [um dos nossos parceiros apoiados.](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners) A configuração inclui o seguimento das instruções da AC de terceiros para completar a integração do seu CA com o Intune.
  - [Crie uma aplicação em Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) que delega os direitos de Intune para fazer a validação do desafio do certificado SCEP.

- Os certificados importados pKCS exigem que [instale o Conector de CertificadoPFX para o Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Utilizar certificados utilizando os seguintes mecanismos:
  - Perfis de [certificado fidedignos](certificates-configure.md#create-trusted-certificate-profiles) para implantar o certificado de AC raiz fidedigna da sua raiz ou ca intermédia (emissão) para dispositivos
  - Perfis de certificado de SCEP
  - Perfis de certificadoS PKCS *(suportados apenas com a [Plataforma Digicert PKI)](certificates-digicert-configure.md)*
  - Perfis de certificados importados pKCS

## <a name="supported-platforms-and-certificate-profiles"></a>Plataformas suportadas e perfis de certificados

| Platform              | Perfil de certificado fidedigno | Perfil de certificado PKCS | Perfil de certificado SCEP | Perfil de certificado importado pKCS  |
|--|--|--|--|---|
| Administrador de dispositivos Android | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png)|  ![Suportado](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - Totalmente gerido (Proprietário do dispositivo)   | ![Suportado](./media/certificates-configure/green-check.png) |   | ![Suportado](./media/certificates-configure/green-check.png) |   |
| Android Enterprise <br> - Dedicado (Proprietário de Dispositivos)   | ![Suportado](./media/certificates-configure/green-check.png)  |   | ![Suportado](./media/certificates-configure/green-check.png)  |   |
| Android Enterprise <br> - Perfil de trabalho    | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) |
| macOS                 | ![Suportado](./media/certificates-configure/green-check.png) |  ![Suportado](./media/certificates-configure/green-check.png) |![Suportado](./media/certificates-configure/green-check.png)|![Suportado](./media/certificates-configure/green-check.png)|
| Wnodows Phone 8.1     |![Suportado](./media/certificates-configure/green-check.png)  |  | ![Suportado](./media/certificates-configure/green-check.png)| ![Suportado](./media/certificates-configure/green-check.png) |
| Windows 8.1 e posterior |![Suportado](./media/certificates-configure/green-check.png)  |  |![Suportado](./media/certificates-configure/green-check.png) |   |
| Windows 10 e posterior  | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) | ![Suportado](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Exportar o certificado de ac raiz de confiança

Para utilizar certificados importados PKCS, SCEP e PKCS, os dispositivos devem confiar na sua Autoridade de Certificação de Raiz. Para estabelecer a confiança, exportar o certificado de Ca de raiz fidedigna, e quaisquer certificados intermédios ou emitidos da Autoridade de Certificação, como certificado público (.cer). Pode obter estes certificados da AC emissora, ou de qualquer dispositivo que confie na sua Emissão.

Para exportar o certificado, consulte a documentação para a sua Autoridade de Certificação. Terá de exportar o certificado público como ficheiro .cer.  Não exporte a chave privada, um ficheiro .pfx.

Utilizará este ficheiro .cer quando criar perfis de [certificado fidedignos](#create-trusted-certificate-profiles) para implementar esse certificado nos seus dispositivos.

## <a name="create-trusted-certificate-profiles"></a>Criar perfis de certificado fidedignos

Crie um perfil de certificado fidedigno antes de poder criar um perfil de certificado importado SCEP, PKCS ou PKCS. A implementação de um perfil de certificado fidedigno garante que cada dispositivo reconhece a legitimidade do seu CA. Os perfis de certificado SCEP referem diretamente um perfil de certificado fidedigno. Os perfis de certificadoPKCS não referenciam diretamente o perfil de certificado fidedigno, mas referenciam diretamente o servidor que acolhe o seu CA. Os perfis de certificados importados do PKCS não referenciam diretamente o perfil de certificado fidedigno, mas podem utilizá-lo no dispositivo. A implementação de um perfil de certificado fidedigno para dispositivos garante que esta confiança é estabelecida. Quando um dispositivo não confia na raiz ca, a política de perfil de certificado SCEP ou PKCS falhará.

Crie um perfil de certificado fidedigno separado para cada plataforma de dispositivo que pretenda suportar, tal como fará para perfis de certificados importados sCEP, PKCS e PKCS.

### <a name="to-create-a-trusted-certificate-profile"></a>Para criar um perfil de certificado fidedigno

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione e vá aos perfis de **configuração** de **dispositivos** >  > **Criar perfil**.

   ![Navegue para Intune e crie um novo perfil para um certificado de confiança](./media/certificates-configure/certificates-configure-profile-new.png)

3. Introduza as seguintes propriedades:
   - **Plataforma**: Escolha a plataforma dos dispositivos que receberão este perfil.
   - **Perfil**: Selecione **certificado fidedigno**
  
4. Selecione **Criar**.

5. No Básico, insira as **seguintes**propriedades:
   - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes aos perfis de forma que possa identificá-los facilmente mais tarde. Por exemplo, um bom nome de perfil é *perfil de certificado fidedigno para toda a empresa*.
   - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.

6. Selecione **Seguinte**.

7. Nas definições de **Configuração,** especifique o ficheiro .cer para o certificado root CA fidedigno que exportou anteriormente. 

   Apenas para os dispositivos Windows 8.1 e Windows 10, selecione o **Arquivo de Destino** do certificado fidedigno em:

   - **Arquivo de certificados no computador – Raiz**
   - **Arquivo de certificados no computador – Intermédio**
   - **Armazenamento de certificados de utilizador – Intermédio**

   ![Criar um perfil e carregar um certificado fidedigno](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Selecione **Seguinte**.

9. Nas **etiquetas scope** (opcional), atribua uma etiqueta para filtrar o perfil a grupos de TI específicos, tais como `US-NC IT Team` ou `JohnGlenn_ITDepartment`. Para obter mais informações sobre etiquetas de âmbito, consulte [Use RBAC e etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

   Selecione **Seguinte**.

10. Em **Atribuições,** selecione o utilizador ou grupos que receberão o seu perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](../configuration/device-profile-assign.md).

    Selecione **Seguinte**.

11. (*Aplica-se apenas ao Windows 10)* Nas Regras de **Aplicabilidade,** especifique as regras de aplicabilidade para refinar a atribuição deste perfil. Pode optar por atribuir ou não atribuir o perfil com base na edição ou versão de um dispositivo.

  Para mais informações, consulte as regras de [aplicabilidade](../configuration/device-profile-create.md#applicability-rules) em Criar um perfil de *dispositivo no Microsoft Intune*.

12. Em **Review + criar,** reveja as suas definições. Quando selecionar Criar, as suas alterações são guardadas e o perfil é atribuído. A política também está na lista de perfis.

## <a name="additional-resources"></a>Recursos adicionais

- [Atribuir perfis de dispositivo](../configuration/device-profile-assign.md)  
- [Use S/MIME to sign and encrypt emails (Utilizar S/MIME para assinar e encriptar e-mails)](certificates-s-mime-encryption-sign.md)  
- [Utilize autoridade de certificação de terceiros](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Próximos passos

Crie perfis de certificados importados SCEP, PKCS ou PKCS para cada plataforma que pretenda utilizar. Para continuar, consulte os seguintes artigos:

- [Configure infraestrutura para apoiar certificados SCEP com Intune](certificates-scep-configure.md)  
- [Configurar e gerir certificados PKCS com o Intune](certficates-pfx-configure.md)  
- [Criar um perfil de certificado importado PKCS](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
