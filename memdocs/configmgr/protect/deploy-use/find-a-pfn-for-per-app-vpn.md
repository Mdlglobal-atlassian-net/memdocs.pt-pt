---
title: Localizar o nome da família de pacotes (PFN) para VPN por aplicação
titleSuffix: Configuration Manager
description: Saiba mais sobre as duas formas de encontrar um nome de família pacote para que possa configurar uma VPN por app.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f109e4ea4bee4a1de767508d62bc3f080d24f625
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715607"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Localizar o nome da família de pacotes (PFN) para VPN por aplicação

*Aplica-se a: Gestor de Configuração (ramo atual)*


Existem duas formas de localizar um PFN, de modo a que possa configurar uma VPN por aplicação.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Localizar um PFN para uma aplicação que está instalada num computador Windows 10

Se a aplicação com que está a trabalhar já estiver instalada num computador Windows 10, pode utilizar o cmdlet [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) do PowerShell para obter o PFN.

A sintaxe de Get-AppxPackage é:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Você pode ter que executar PowerShell como um administrador para recuperar o PFN

Por exemplo, para obter informações sobre todas as aplicações universais instaladas no computador, utilize `Get-AppxPackage`.

Para obter informações sobre uma aplicação da qual sabe o nome, ou parte deste, utilize `Get-AppxPackage *<app_name>`. Tenha em atenção a utilização do caráter universal, particularmente útil se não tiver a certeza do nome completo da aplicação. Por exemplo, para obter as informações para o OneNote, utilize `Get-AppxPackage *OneNote`.


Eis as informações obtidas para o OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Localizar um PFN se a aplicação não estiver instalada num computador

1. Ir para https://www.microsoft.com/store/apps
2. Introduza o nome da aplicação na barra de procura. No nosso exemplo, procure OneNote.
3. Clique na ligação para a aplicação. Tenha em atenção que o URL a que acede tem uma série de letras no final. No nosso exemplo, o URL é assim:`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. Num separador diferente, colhe `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`o seguinte `<app id>` URL, substituindo pelo https://www.microsoft.com/store/apps id da aplicação obtido - essa série de letras no final do URL no passo 3. No nosso exemplo, o exemplo do OneNote, teria de colar: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

No Edge, são apresentadas as informações que pretende; no Internet Explorer, clique em **Abrir** para ver as informações. O valor de PFN é atribuído na primeira linha. Eis o aspeto dos resultados para o nosso exemplo:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
