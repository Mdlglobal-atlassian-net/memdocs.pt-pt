---
title: Adicione definições de ficheiros preferenciais aos dispositivos macOS no Microsoft Intune - Azure / Microsoft Docs
titleSuffix: ''
description: Adicione um ficheiro xml ou plist que inclui informações chave sobre a sua aplicação. Utilize um perfil de configuração de ficheiro preferencial para alterar as informações chave no ficheiro da lista de propriedades e atribuí-la aos seus dispositivos macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331993"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Adicione um ficheiro de lista de propriedades a dispositivos macOS usando o Microsoft Intune

Utilizando o Microsoft Intune, pode adicionar um ficheiro de lista de propriedades (.plist) para dispositivos macOS ou aplicações em dispositivos macOS.

Esta funcionalidade aplica-se a:

- dispositivos macOS com 10,7 e mais recentes

Os ficheiros da lista de propriedades normalmente incluem informações sobre aplicações macOS. Para mais informações, consulte [sobre ficheiros](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) de lista de propriedades de informação (site da Apple) e [definições de carga personalizada](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

Este artigo lista e descreve as diferentes definições de ficheiros da lista de propriedades que pode adicionar aos dispositivos macOS. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para adicionar o pacote de aplicações ID (`com.company.application`) e adicionar o seu ficheiro .plist.

Estas definições são adicionadas a um perfil de configuração do dispositivo no Intune e, em seguida, atribuídas ou implementadas nos dispositivos macOS.

## <a name="before-you-begin"></a>Antes de começar

[Criar o perfil.](device-profile-create.md)

## <a name="what-you-need-to-know"></a>O que tem de saber

- Estas definições não são validadas. Certifique-se de testar as suas alterações antes de atribuir o perfil aos seus dispositivos.
- Se não tiver a certeza de como introduzir uma chave de aplicação, altere a definição dentro da aplicação. Em seguida, reveja o ficheiro preferencial da aplicação usando [o Xcode](https://developer.apple.com/xcode/) para ver como a definição está configurada. A Apple recomenda a remoção de configurações não manejáveis utilizando o Xcode antes de importar o ficheiro.
- Apenas algumas aplicações funcionam com preferências geridas, e podem não permitir-lhe gerir todas as definições.
- Certifique-se de que faz o upload de ficheiros da lista de propriedades que visam as definições do canal do dispositivo, e não as definições do canal do utilizador. Os ficheiros da lista de propriedades visam todo o dispositivo.

## <a name="preference-file"></a>Ficheiro de preferência

- **Nome**de domínio preferencial : Os ficheiros da lista de propriedades são normalmente utilizados para navegadores web (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)e aplicações personalizadas. Quando se cria um domínio preferencial, também é criado um pacote de IDENTIFICAção. Introduza o ID do pacote, como `com.company.application`. Por exemplo, insira `com.Contoso.applicationName`, `com.Microsoft.Edge`ou `com.microsoft.wdav`.
- **Ficheiro da lista de propriedades**: Selecione o ficheiro da lista de propriedades associado à sua aplicação. Certifique-se de que é um ficheiro `.plist` ou `.xml`. Por exemplo, faça o upload de um ficheiro `YourApp-Manifest.plist` ou `YourApp-Manifest.xml`.
- **Conteúdo**do ficheiro : A informação chave no ficheiro da lista de propriedades é mostrada. Se precisar de alterar as informações chave, abra o ficheiro da lista noutro editor e, em seguida, recarregue o ficheiro em Intune.

Certifique-se de que o seu ficheiro está devidamente formatado. O ficheiro deve ter apenas pares de valor-chave, e não deve ser embrulhado em `<dict>`, `<plist>`ou etiquetas `<xml>`. Por exemplo, o ficheiro da sua lista de propriedades deve ser semelhante ao seguinte ficheiro:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Selecione **OK** > **Criar** para guardar as alterações. O perfil é criado e mostrado na lista de perfis.

## <a name="next-steps"></a>Próximos passos

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Para obter mais informações sobre os ficheiros preferenciais do Microsoft Edge, consulte as definições de política do [Microsoft Edge no macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).