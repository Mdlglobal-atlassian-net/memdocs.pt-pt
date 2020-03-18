---
title: Utilize registos stageNow em dispositivos Android Zebra no Microsoft Intune - Azure Microsoft Docs
description: Consulte questões e resoluções comuns ao utilizar o StageNow em dispositivos Android com o Microsoft Intune. Também aprenda a obter registos e veja exemplos de como ler os registos para o sucesso ou erros.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8c7c60b4d9d1831aaabb9886345865234ce6351
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333181"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Problemas e ver potenciais problemas em dispositivos Android Zebra no Microsoft Intune



No Microsoft Intune, pode utilizar extensões de [mobilidade zebra (MX) para gerir dispositivos Android Zebra](android-zebra-mx-overview.md). Ao utilizar dispositivos Zebra, cria perfis no StageNow para gerir as definições e envia-os para Intune. Intune usa a aplicação StageNow para aplicar as definições nos dispositivos. A aplicação StageNow também cria um ficheiro de registo detalhado no dispositivo que é usado para resolver problemas.

Esta funcionalidade aplica-se a:

- Android

Por exemplo, cria-se um perfil no StageNow para configurar um dispositivo. Quando cria o perfil StageNow, o último passo gera um ficheiro para testar o perfil. Consome este ficheiro com a aplicação StageNow no dispositivo.

Noutro exemplo, cria-se um perfil no StageNow e testa-o. Intune, adicione o perfil StageNow e, em seguida, atribua-o aos seus dispositivos Zebra. Ao verificar o estado do perfil atribuído, o perfil mostra um estatuto de alto nível.

Em ambos os casos, pode obter mais detalhes do ficheiro de registo StageNow, que é guardado no dispositivo sempre que um perfil StageNow se aplica.

Algumas questões não estão relacionadas com o conteúdo do perfil StageNow, e não se refletem nos registos.

Este artigo mostra-lhe como ler os registos stageNow e enumera alguns outros problemas potenciais com dispositivos Zebra que podem não se refletir nos registos.

[Utilizar e gerir dispositivos Zebra com Extensões](android-zebra-mx-overview.md) de Mobilidade Zebra tem mais informações sobre esta funcionalidade.

## <a name="get-the-logs"></a>Pegue os registos

### <a name="use-the-stagenow-app-on-the-device"></a>Utilize a aplicação StageNow no dispositivo
Quando testa um perfil utilizando diretamente o StageNow no seu computador, em vez de utilizar o [Intune para implementar o perfil,](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow)a aplicação StageNow no dispositivo guarda os registos do teste. Para obter o ficheiro de registo, utilize a opção **Mais (...)** na aplicação StageNow no dispositivo.

### <a name="get-logs-using-android-debug-bridge"></a>Obtenha registos usando a Ponte Android Debug
Para obter registos depois de o perfil já estar implementado com o Intune, ligue o dispositivo a um computador com [o Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (abre o site do Android).

No dispositivo, os registos são guardados em `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Obtenha registos de e-mail
Para obter registos depois de o perfil já estar implementado com o Intune, os utilizadores finais podem enviar-lhe os registos através de uma aplicação de e-mail no dispositivo. No dispositivo Zebra, abra a aplicação Portal da Empresa e [envie os registos.](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android) A utilização da função de registo de envio também cria um ID de incidente powerLift, que pode fazer referência se contactar o suporte da Microsoft.

## <a name="read-the-logs"></a>Leia os registos

Ao olhar para os registos, há um erro sempre que vê a etiqueta `<characteristic-error>`. Os detalhes de erro são escritos para a `<parm-error>` tag > `desc` propriedade.

## <a name="error-types"></a>Tipos de erro

Os dispositivos zebra incluem diferentes níveis de relato de erros:

- O CSP não é suportado no dispositivo. Por exemplo, o dispositivo não é um dispositivo celular e não tem um gestor celular.
- A versão MX ou OSX é desajustada. Cada CSP é versão. Para obter uma matriz de suporte completo, consulte a [documentação da Zebra](http://techdocs.zebra.com/mx/) (abre o site da Zebra).
- O dispositivo relata outro problema ou erro.

## <a name="examples"></a>Exemplos

Por exemplo, tem o seguinte perfil de entrada:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

No registo, o XML é idêntico à entrada. Esta saída correspondente significa que o perfil aplicado com sucesso ao dispositivo sem erros:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

Noutro exemplo, tem a seguinte entrada:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

O registo mostra um erro, uma vez que contém uma etiqueta `<characteristic-error>`. Neste cenário, o perfil tentou instalar um pacote Android (APK) que não existe no caminho dado:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Outros problemas potenciais com dispositivos Zebra

Esta secção enumera outros problemas possíveis que poderá ver ao utilizar dispositivos Zebra com administrador de dispositivos. Estes problemas não são reportados nos registos do StageNow.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView está desatualizado

Quando os dispositivos mais antigos assinam a aplicação do Portal da Empresa, os utilizadores podem ver uma mensagem de que o componente Do Sistema WebView está desatualizado e precisa de ser atualizado. Se o dispositivo tiver o Google Play instalado, conecte-o à internet e verifique se há atualizações. Se o dispositivo não tiver o Google Play instalado, obtenha a versão atualizada do componente e aplique-o nos dispositivos. Ou, atualizar para o mais recente dispositivo OS emitido pela Zebra.

### <a name="management-actions-take-a-long-time"></a>As ações de gestão demoram muito tempo

Se os serviços do Google Play não estiverem disponíveis, algumas tarefas demoram até 8 horas a terminar. [As limitações da aplicação Intune Company Portal para Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (abre outro site da Microsoft) podem ser um bom recurso.

### <a name="device-spoofing-suspected-shows-in-intune"></a>"Engenho falsificação de suspeitos" mostra em Intune

Este erro significa que intune suspeita que um dispositivo Android não-Zebra esteja a reportar o seu modelo e fabricante como um dispositivo Zebra.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>App Portal da Empresa é mais antiga do que a versão mínima exigida

A Intune poderá atualizar a versão mínima exigida da aplicação Portal da Empresa. Se o Google Play não estiver instalado no dispositivo, a aplicação Portal da Empresa não será atualizada automaticamente. Se a versão mínima necessária for mais recente do que a versão instalada, a aplicação Portal da Empresa deixa de funcionar. Atualização para a mais recente aplicação do Portal da Empresa utilizando [sideloading em dispositivos Zebra](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Próximos passos

[Quadros de discussão](https://developer.zebra.com/community/home/discussions) de zebra (abre o site da Zebra)

[Utilizar e gerir dispositivos Zebra com Extensões de Mobilidade zebra em Intune](android-zebra-mx-overview.md)
