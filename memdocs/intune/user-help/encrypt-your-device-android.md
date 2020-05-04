---
title: Criptografe o dispositivo Android para Intune Microsoft Docs
description: Passos para ativar encriptação do dispositivo Android quando exigido pela Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696267"
---
# <a name="encrypting-your-android-device"></a>Encriptar o seu dispositivo Android

A encriptação do dispositivo protege os seus ficheiros e pastas do acesso não autorizado se o seu dispositivo for perdido ou roubado. Torna os dados do seu dispositivo inacessíveis e ilegíveis a pessoas sem senha. 

Antes de poder aceder aos recursos escolares ou de trabalho, a sua organização pode exigir que:

* [Encriptar o dispositivo](#encrypt-device)
* [Ativar arranque seguro](#enable-secure-startup)
* [Definir código de acesso inicial, PIN ou outro método de autenticação](#set-startup-passcode)  

> [!Note]
> Certos dispositivos Android da Huawei, Vivo e OPPO não podem ser encriptados. Para mais informações, consulte [o Dispositivo encriptado, mas a aplicação diz o contrário.](your-device-appears-encrypted-but-cp-says-otherwise-android.md)  

## <a name="encrypt-device"></a>Encriptar dispositivo

Siga estes passos para encriptar o seu dispositivo. O seu dispositivo pode reiniciar várias vezes. 

O nome e a localização da opção de encriptação variarão consoante o fabricante do seu dispositivo e a versão Android. 

1. Abra a aplicação **Definições**.
2. Digite **a segurança** ou **criptografe** na barra de pesquisa da aplicação para encontrar configurações relacionadas.
3. Toque na opção de encriptar o seu dispositivo. Siga as instruções no ecrã.  
4. Quando solicitado, detete uma palavra-passe de ecrã de bloqueio, PIN ou outro método de autenticação (se permitido pela sua organização). 
5. Para voltar a verificar as definições, abra o Portal da Empresa ou a aplicação Microsoft Intune.
    * Utilizadores do Portal da Empresa: Selecione o seu dispositivo e toque em **verificar as definições do dispositivo**. 
    * Utilizadores do Microsoft Intune: Terá de esperar até que a página atualização, mas quando isso acontecer, o seu estado de encriptação deve mudar para o seu conforme. 

## <a name="enable-secure-startup"></a>Ativar arranque seguro

A sua organização pode exigir que você ative uma startup segura como parte da sua política de encriptação. Esta funcionalidade protege ainda mais o seu dispositivo, exigindo que seja introduzido uma palavra-passe ou PIN antes de o telefone arrancar. Muitos têm opções adicionais de autenticação, mas variarão dependendo do que a sua organização permite. 

O nome e a localização da opção de arranque segura variarão consoante o fabricante do seu dispositivo e a versão Android. Em alguns dispositivos, esta definição pode ser chamada de **proteção forte**. 

1. Abra a aplicação **Definições**.
2. Digite **startup segura** na barra de pesquisa da aplicação.
3. Toque **no arranque** > **seguro, exija PIN quando o dispositivo ligar**.
4. Quando solicitado, introduza o PIN do seu dispositivo.   
5. Para voltar a verificar as definições, abra o Portal da Empresa ou a aplicação Microsoft Intune.
    * Utilizadores do Portal da Empresa: Selecione o seu dispositivo e toque em **verificar as definições do dispositivo**. 
    * Utilizadores do Microsoft Intune: Terá de esperar até que a página atualização, mas quando isso acontecer, o seu estado de encriptação deve mudar para o seu conforme.  


## <a name="set-startup-passcode"></a>Definir código de acesso de arranque   
Quando [encriptar o seu dispositivo](#encrypt-device) e ativar o [arranque seguro,](#enable-secure-startup)será solicitado a definir o seu dispositivo PIN, palavra-passe ou outro método de autenticação (se permitido pela sua organização). Não são necessários mais passos. 

Para escolher ou alterar o tipo de ecrã de bloqueio:

1. Abra a aplicação **Definições**.
2. Digite **o bloqueio** do ecrã na barra de pesquisa da aplicação.
3. Toque no tipo de bloqueio do ecrã de **toque**.
4. Toque no tipo de bloqueio do ecrã que pretende utilizar e siga as instruções no ecrã para confirmar.  

## <a name="troubleshoot"></a>Resolução de problemas    
**Problema**: O botão de encriptação está desativado.   

**Coisa a tentar:** 
* Certifique-se de que o seu dispositivo está completamente carregado e ligado. A encriptação pode demorar um pouco e requer uma bateria completa.   

**Problema**: Vê uma mensagem a dizer que ainda precisa de encriptar o seu dispositivo.  

**Coisas para tentar:**
   *  [Coloque um ecrã de bloqueio](#set-startup-passcode) no seu dispositivo. 
   * [Ativar arranque seguro](#enable-secure-startup).

Ainda precisa de ajuda? Contacte o suporte da empresa (verifique as informações de contacto no [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980)) ou escreva para a <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">equipa Android da Microsoft</a>.  
