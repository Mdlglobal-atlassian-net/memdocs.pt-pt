---
title: O dispositivo Android parece estar encriptado | Microsoft Docs
description: Resolver o estado de encriptação na aplicação Portal da Empresa e Microsoft Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4fd08ba190654db5678766e34e3340330dcf3ca8
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327481"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Dispositivo encriptado mas aplicações dizem o contrário

Se o Portal da Empresa ou a aplicação Microsoft Intune disserem que o seu dispositivo não está encriptado, mas tem a certeza de que está, experimente os passos deste artigo.  

## <a name="add-a-startup-pin"></a>Adicionar um PIN de arranque

Determinados dispositivos Android exigem que crie um PIN de arranque para garantir que o dispositivo está seguro. A localização desta definição estará na aplicação **Definições** do seu dispositivo. O nome e a localização da definição podem variar. Por exemplo, no Samsung Galaxy S7, a definição é referida como **Secure Startup**. Para o ativar e criar uma senha, aceda a **Definições** > **Lock Screen e Security** > Secure **Startup**.  

## <a name="encrypt-the-entire-device"></a>Encriptar todo o dispositivo

Esta secção aplica-se apenas à aplicação Portal da Empresa. Alguns dispositivos permitem-lhe optar por encriptar todo o dispositivo ou apenas o espaço utilizado do mesmo. Escolha a opção de encriptar todo o dispositivo. Se selecionou para encriptar apenas o espaço usado:

1. [Retire este dispositivo do Portal da Empresa](unenroll-your-device-from-intune-android.md).
2. Desencriptar o espaço usado.  
3. Criptografe todo o dispositivo.  
4. Reinscreva o dispositivo.  

## <a name="downgrade-your-version-of-android"></a>Mudar a versão do Android para uma versão anterior

Esta secção aplica-se apenas à aplicação Portal da Empresa. Se o seu dispositivo lhe oferecer a opção de desvalorizar para o Android 6.0 e mais tarde, então faça-o. Existe o risco de perda de dados se tentar desvalorizar o seu dispositivo. Em alternativa, recomendamos que contacte o suporte da empresa para resolver este problema. Obtenha informações de contacto para o suporte da sua empresa no site do Portal da [Empresa.](https://go.microsoft.com/fwlink/?linkid=2010980)  

## <a name="specific-manufacturer-issues"></a>Problemas de um fabricante específico

Alguns dispositivos Android na versão 7.0 e posteriormente encriptam dados de formas inconsistentes com certos padrões da plataforma Android. Estes métodos de encriptação colocam a informação do dispositivo em risco. Como resultado, estes dispositivos não são suportados.

Para obter uma lista não exaustiva de dispositivos Android suportados, consulte o artigo [Sistemas operativos e navegadores suportados em Intune](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Se o seu dispositivo não estiver listado, consulte o fabricante do dispositivo ou contacte a pessoa de suporte.

> [!Note]
> A Microsoft trabalha com os fabricantes para resolver quaisquer problemas que encontremos durante os testes ou que os utilizadores nos reportem. Atualizaremos este artigo sempre que estiverem disponíveis novas informações.

## <a name="update-devices"></a>Atualizar dispositivos

Se ainda não atualizou o seu dispositivo para a versão mais recente do Android, vá à aplicação **Definições** do seu dispositivo e selecione **Update**.  

## <a name="next-steps"></a>Próximos passos

Ainda precisa de ajuda? Contacte o suporte da empresa (verifique as informações de contacto no [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980)) ou escreva para a <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">equipa Android da Microsoft</a>.  
