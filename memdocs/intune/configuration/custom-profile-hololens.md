---
title: Utilize o Controlo de Aplicações do Windows Defender em dispositivos HoloLens 2 no Microsoft Intune - Azure [ Microsoft Docs
description: Configure o CSP do Windows Defender Application Control (WDAC) para permitir ou bloquear aplicações de abertura em dispositivos HoloLens 2 no Microsoft Intune. Utilize o PowerShell e um perfil de configuração personalizado.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990121"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Utilize o WDAC e o Windows PowerShell para permitir ou bloquear aplicações em dispositivos HoloLens 2 com o Microsoft Intune

Os dispositivos Microsoft HoloLens 2 suportam o [CSP de Controlo de Aplicações do Windows Defender (WDAC),](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp)que substitui o [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Utilizando o Windows PowerShell e o Microsoft Intune, pode utilizar o CSP WDAC para permitir ou bloquear aplicações específicas a partir da abertura nos dispositivos Microsoft HoloLens 2. Por exemplo, pode querer permitir ou impedir que a aplicação Cortana abram nos dispositivos HoloLens 2 da sua organização.

Esta funcionalidade aplica-se a:

- Dispositivos HoloLens 2 que executam o Windows Holographic para negócios

O CSP WDAC baseia-se na função De Controlo de [Aplicações do Windows Defender (WDAC).](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) Também pode [utilizar várias políticas wDAC.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies)

Este artigo mostra-lhe como:

1. Utilize o Windows PowerShell para criar políticas WDAC.
2. Utilize o Windows PowerShell para converter as regras de política do WDAC para XML, atualize o XML e, em seguida, converta o XML num ficheiro binário.
3. No Microsoft Intune, crie um [perfil de configuração de dispositivo personalizado,](custom-settings-windows-holographic.md)adicione este ficheiro binário de política WDAC e aplique a política nos seus dispositivos HoloLens 2.

Em Intune, deve criar um perfil de configuração personalizado para utilizar o CSP de Controlo de Aplicações do Windows Defender (WDAC). 

Utilize os passos deste artigo como modelo para permitir ou negar que aplicações específicas abram nos dispositivos HoloLens 2.

## <a name="prerequisites"></a>Pré-requisitos

- Esteja familiarizado com o Windows PowerShell.
- Inscreva-se em Intune como membro de:

  - **Policy and Profile Manager** ou **Intune Role Administrator** Intune Função

    OU

  - **Papel** de Administrador Global ou **Administrador de Serviço Intune** Azure

  [O controlo de acesso baseado em funções (RBAC) com intune](../fundamentals/role-based-access-control.md) tem mais informações.

- Crie um grupo de utilizadores ou grupo de dispositivos com os seus dispositivos HoloLens 2. Para mais informações, consulte [grupos de utilizadores vs. grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Exemplo

Este exemplo utiliza o Windows PowerShell para criar uma política de Controlo de Aplicações do Windows Defender (WDAC). A política impede a abertura de aplicações específicas. Em seguida, use Intune para implementar a política para dispositivos HoloLens 2.

1. No seu computador de secretária, abra a aplicação **Windows PowerShell.**
2. Obtenha informações sobre o pacote de aplicações instalado no seu computador de secretária:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Por exemplo, introduza: 

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Em seguida, confirme que o pacote tem atributos de aplicação:

    ```powershell
    $package1
    ```

    Verá atributos semelhantes aos seguintes detalhes da aplicação:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Crie uma política WDAC e adicione o pacote de aplicações à regra DENY:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Repita os passos 2 e 3 para quaisquer outras aplicações que deseja negar:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Por exemplo, introduza: 

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Converter a política wDAC para **newPolicy.xml:**

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Para direcionar todas as versões de uma aplicação, em newPolicy.xml, certifique-se `PackageVersion="65535.65535.65535.65535"` de que está no nó De Nega:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Para, `PackageFamilyNameRules` pode utilizar as seguintes versões:

    - **Permitir**: Entrar `PackageVersion, 0.0.0.0` , que significa "Permitir esta versão e acima".
    - **Negue**: Enter `PackageVersion, 65535.65535.65535.65535` , que significa "Negar esta versão e abaixo".

6. Misture **newPolicy.xml** com a política predefinida que está no seu computador de secretária. Este passo cria **fusãoPolicy.xml**. Por exemplo, permitir que os controladores assinados pelo Windows, WHQL e aplicações assinadas pela Store executem:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Desative a regra do **modo auditoria** em **fusãoPolicy.xml**. Quando se funde, o modo de auditoria é automaticamente ligado:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Ativar os **InvalidaEAs numa** regra de reinício em **fusãoPolicy.xml:**

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Para obter mais informações sobre estas regras, consulte [Compreender as regras políticas do WDAC e as regras de arquivo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Converter **fusãoPolicy.xml** para formato binário. Este passo cria **compiladaPolicy.bin**. Você vai adicionar este ficheiro binário **Policy.bin compilado** ao Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Crie o perfil de configuração do dispositivo personalizado em Intune:

    1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)crie um perfil de configuração de dispositivo personalizado do Windows 10.

        Para os passos específicos, consulte [Criar um perfil personalizado utilizando OMA-URI em Intune](custom-settings-configure.md).

    2. Quando criar o perfil, introduza as seguintes definições:

      - **OMA-URI**: introduza `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. `<PolicyGUID>`Substitua-o pelo nó PolicyTypeID no ficheiro **fusãoPolicy.xml** que criou no passo 6.

        Usando o nosso exemplo, insira `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076` .

        O GUID da política **deve coincidir com** o nó PolicyTypeID no ficheiro **fusãoPolicy.xml** (criado no passo 6).

      - **Tipo**de dados : Definir para **o ficheiro Base64**. Converte automaticamente o ficheiro do caixote para o base64.
      - **Ficheiro do certificado**: Faça upload do ficheiro binário **compiladoPolicy.bin** (criado no passo 9).

      As suas definições são semelhantes às seguintes definições:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Adicione um OMA-URI personalizado para configurar o ApplicationControl CSP no Microsoft Intune.":::

11. Quando o perfil for [atribuído](device-profile-assign.md) ao seu grupo HoloLens 2, verifique o estado do perfil. Depois de o perfil se aplicar com sucesso, reinicie os dispositivos HoloLens 2.

## <a name="next-steps"></a>Passos seguintes

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

[Saiba mais sobre perfis personalizados em Intune](custom-settings-configure.md).
