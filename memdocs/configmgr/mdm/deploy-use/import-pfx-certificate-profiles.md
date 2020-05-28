---
title: Importar perfis de certificado PFX
titleSuffix: Configuration Manager
description: Saiba como utilizar ficheiros PFX no Gestor de Configuração para gerar certificados específicos do utilizador que suportam a troca de dados encriptado.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3304d480f0650191a784a9152ae464e81c2207a1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906404"
---
# <a name="import-pfx-certificate-profiles"></a>Importar perfis de certificado PFX

*Aplica-se a: Gestor de Configuração (ramo atual)*

Aprenda a criar um perfil de certificado importando credenciais de certificados externos. Este artigo destaca informações específicas sobre perfis de certificados de troca de informações pessoais (PFX). Para obter mais informações sobre como criar e configurar estes perfis, consulte os perfis de [Certificado.](../../protect/deploy-use/introduction-to-certificate-profiles.md)

O Gestor de Configuração suporta diferentes tipos de lojas de certificados para diferentes dispositivos e versões DES. Por exemplo, Windows 10 e Windows 10 Mobile. Para mais informações, consulte os [pré-requisitos](../../protect/plan-design/prerequisites-for-certificate-profiles.md)do perfil do certificado .

Utilize o Gestor de Configuração para importar credenciais de certificados e, em seguida, fornecer ficheiros PFX para dispositivos. Pode utilizar estes ficheiros para gerar certificados específicos do utilizador para suportar a troca de dados encriptada.

> [!TIP]  
> Para uma caminhada passo a passo deste processo, consulte a publicação do blog Como Criar e Implementar Perfis de [Certificado PFX no Gestor](https://docs.microsoft.com/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager)de Configuração .  

## <a name="create-a-profile"></a>Criar um perfil

1. Na consola de Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade, expanda o Acesso aos **Recursos da Empresa,** e depois selecione Perfis de **Certificado.**

1. No separador **Home** da fita, no grupo **Criar,** selecione **Criar Perfil**de Certificado .

1. Na página **geral** do Assistente de Perfil de **Certificado,** especifique as seguintes informações:  

    - **Nome**: introduza um nome exclusivo para o perfil do certificado. Pode utilizar até 256 carateres.  

    - **Descrição**: Forneça uma descrição que dê uma visão geral do perfil do certificado que ajude a identificá-lo na consola Do Gestor de Configuração. Pode utilizar até 256 carateres.  

1. Selecione As definições de Troca de **Informações Pessoais - Definições de #12 PKCS (PFX) - Importar**. Esta opção importa informações de um certificado existente para criar um perfil de certificado.

    > [!NOTE]
    > A opção **Criar** solicita um certificado em nome de um utilizador de uma autoridade de certificados ligadono local (CA). Este processo entrega então o certificado de forma segura aos clientes como ficheiros PFX. Para mais informações, consulte Criar perfis de [certificadoS PFX utilizando uma autoridade de certificados](create-pfx-certificate-profiles.md).

1. Na página de **Certificado PFX** do Assistente de **Perfil de Certificado criar,** especifique o fornecedor de armazenamento chave do dispositivo (KSP):

    - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
    - **Instalar no Módulo plataforma fidedigno (TPM) de outra forma falhar**
    - **Instalar no Windows Hello for Business falha de outra forma**
    - **Instalar no Fornecedor de Armazenamento de Chaves de Software**

1. Na página **Plataformas Suportadas,** escolha as plataformas de dispositivos suportadas.

1. Conclua o assistente.

## <a name="deploy-the-profile"></a>Implementar o perfil

Depois de criar e fornecer um perfil de certificado, está agora disponível no nó de Perfis de **Certificado.** Para obter mais informações sobre como implementá-lo, consulte [os perfis](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)de acesso aos recursos .

## <a name="assign-primary-users"></a>Atribuir utilizadores primários

Atribuir os utilizadores-alvo como utilizadores primários nos dispositivos Windows 10 onde necessita de instalar os certificados PFX. Para mais informações, consulte a [finta do dispositivo do utilizador](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Provisão de um script PFX criar

Para importar um certificado PFX, utilize os seguintes cmdlets powerShell do Gestor de Configuração para fornecer um script Create PFX:

- [Get-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Importação-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remover CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Script de exemplo

Para fornecer um ficheiro PFX a um perfil de certificado para um utilizador, abra o PowerShell num computador com a consola 'Gestor de Configuração'. Mude as variáveis com valores do seu ambiente.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Consulte também

[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md)

[Criar perfis de certificadoS PFX utilizando uma autoridade de certificado](create-pfx-certificate-profiles.md)

[Implementar perfis Wi-Fi, VPN, de e-mail e de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
