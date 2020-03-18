---
title: Criptografe o dispositivo Android para Intune Microsoft Docs
description: Passos para ativar encriptação do dispositivo Android quando exigido pela Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328309"
---
# <a name="encrypting-your-android-device"></a>Encriptar o seu dispositivo Android

A encriptação do dispositivo protege os seus ficheiros e pastas do acesso não autorizado se o seu dispositivo for perdido ou roubado. Depois de ligar a encriptação do dispositivo, apenas indivíduos com a senha ou pin o correto poderão iniciar sessão no seu dispositivo. 

Antes de poder aceder aos recursos escolares ou de trabalho, a sua organização poderá exigir que criptografe o seu dispositivo Android. Alguns dispositivos Android mais recentes são encriptados por padrão, fora da caixa.  

## <a name="turn-on-encryption"></a>Ativar encriptação

Se o Portal da Empresa ou a aplicação Microsoft Intune lhe pedirem para encriptar o seu dispositivo, complete os seguintes passos. 

> [!Note]
> Certos dispositivos Android da Huawei, Vivo e OPPO não podem ser encriptados. Saiba mais [aqui](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

1. Detete uma fechadura de ecrã do dispositivo.  
    a. Vá para **definições** > **bloquear o ecrã e > o** tipo de bloqueio do **ecrã** .  
    b. Selecione **PIN,** **Password,** ou **Pattern**.  
    c. Siga as instruções no ecrã para configurar o bloqueio do ecrã.  

2. Volte para **o ecrã e segurança lock** e selecione Secure **startup**.
3. Escolha **Exigir PIN quando o dispositivo ligar** > **OK**.
4. Introduza o seu PIN para confirmar e encriptar o seu dispositivo.
5. Abra o Portal da Empresa ou a aplicação Microsoft Intune.
    * Utilizadores do Portal da Empresa: Selecione o seu dispositivo e toque em **verificar as definições do dispositivo**. 
    * Utilizadores do Microsoft Intune: Terá de esperar até que a página atualização, mas quando isso acontecer, o seu estado de encriptação deve mudar para o seu conforme.  

Os dispositivos que executam o Android 4.4 e anteriormente podem não ter a opção de **arranque Secure.** Nesse caso, preencha os seguintes passos para encriptar o seu dispositivo.

1. Vá para **definições** > dispositivo de **encriptação**de > de **segurança** . As etiquetas no ecrã variam entre dispositivos Android. Se não vir a opção **Encrypt Device,** faça o check-in:
    * **Encriptação** de armazenamento de armazenamento > **armazenamento**
    * **Armazenamento** > **bloqueio e > de segurança** **Outras definições de segurança** 

2. Siga as instruções no ecrã. Durante a encriptação, o seu dispositivo pode reiniciar várias vezes.
3. Abra o Portal da Empresa ou a aplicação Microsoft Intune.
    * Utilizadores do Portal da Empresa: Selecione o seu dispositivo e toque em **verificar as definições do dispositivo**.  
    * Utilizadores do Microsoft Intune: Terá de esperar até que a página atualização, mas quando isso acontecer, o seu estado de encriptação deve mudar para o seu conforme.

## <a name="troubleshoot"></a>Resolver Problemas  
**Problema**: Já criptografou o seu dispositivo e

- O botão de encriptação está desativado.
- Vê uma mensagem a indicar que ainda tem de encriptar.
- Obtém erros ao tentar utilizar o Portal da Empresa ou a aplicação Microsoft Intune.

**Coisas a experimentar**

- Certifique-se de que o seu dispositivo está carregado e ligado.  
- Confirme se definiu uma palavra-passe ou um PIN no dispositivo.  

Ainda precisa de ajuda? Contacte o suporte da empresa (verifique as informações de contacto no [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980)) ou escreva para a <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">equipa Android da Microsoft</a>.  
