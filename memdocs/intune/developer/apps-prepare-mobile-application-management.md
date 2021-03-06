---
title: Prepare aplicativos para gestão de aplicações móveis com a Microsoft Intune
description: As informações neste tópico ajudam-no a decidir quando deve utilizar a ferramenta de encapsulamento de aplicações e o SDK da Aplicação para permitir que as suas aplicações de linha de negócio personalizadas utilizem políticas de gestão de aplicações móveis.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 863e6e540fcb79ff18accc40142a8e50c1406943
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078078"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>Preparar aplicações de linha de negócios para as políticas de proteção de aplicações

Pode utilizar a Ferramenta de Encapsulamento de Aplicações do Intune ou o SDK da Aplicação do Intune para ativar as suas aplicações para que utilizem políticas de proteção de aplicações. Utilize estas informações para saber mais sobre estes dois métodos e como os utilizar.

## <a name="intune-app-wrapping-tool"></a>Ferramenta de Encapsulamento de Aplicações do Intune

A Ferramenta de Embrulho de Aplicações é usada principalmente para aplicações **internas** de linha de negócio (LOB). A ferramenta é uma aplicação de linha de comandos que cria um wrapper em torno da aplicação, que permite que a aplicação seja, então, gerida por uma política de proteção de aplicações do Intune. Ao proteger uma aplicação fornecida por um fabricante independente de software (ISV), é importante esclarecer se o ISV continuará a suportar a aplicação encapsulada.

Não precisa do código de origem para utilizar a ferramenta, mas precisa das credenciais de início de sessão. Para obter mais informações sobre as credenciais de início de sessão, consulte o [Blogue do Intune](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). Para obter a documentação da ferramenta de embrulho de aplicativos, consulte a ferramenta de embrulho de [aplicativos Android](app-wrapper-prepare-android.md) e a ferramenta de embrulho de [aplicações iOS.](app-wrapper-prepare-ios.md)

A Ferramenta de Encapsulamento de Aplicações **não** suporta aplicações da Apple App Store ou da Google Play Store. Também não suporta determinadas funcionalidades que requerem integração do programador (consulte a tabela de comparação de funcionalidades seguinte).

Para obter mais informações sobre a Ferramenta de Encapsulamento de Aplicações para as políticas de proteção de aplicações de dispositivos que não estão inscritos no Intune, veja [Proteger aplicações de linha de negócio e dados em dispositivos não inscritos no Microsoft Intune](../apps/apps-add.md).

### <a name="reasons-to-use-the-app-wrapping-tool"></a>Motivos para utilizar a Ferramenta de Encapsulamento de Aplicações

* A aplicação não possui funcionalidades de proteção de dados incorporadas
* A aplicação é implementada internamente
* Não tem acesso ao código de origem da aplicação
* Não desenvolveu a aplicação
* A aplicação tem uma experiência mínima de autenticação de utilizador

### <a name="supported-app-development-platforms"></a>Plataformas de desenvolvimento de aplicações suportadas

|**Ferramenta de Encapsulamento de Aplicações num Wrapper** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Sim|Sim|
|**Android**|Não – utilizar os [Enlaces Xamarin do SDK da Aplicação Intune](app-sdk-xamarin.md).|Sim|

## <a name="intune-app-sdk"></a>SDK da Aplicação do Intune

O SDK da Aplicação Intune foi concebido principalmente para clientes com aplicações na App Store da Apple ou na Google Play Store e que pretendem conseguir gerir essas aplicações no Intune. No entanto, qualquer aplicação pode tirar partido da integração com o SDK, inclusive as aplicações de linha de negócio.

Para mais informações sobre o SDK, consulte [Descrição Geral](app-sdk.md). Para começar a utilizar o SDK, consulte [Introdução ao Microsoft Intune App SDK](app-sdk-get-started.md).

### <a name="reasons-to-use-the-sdk"></a>Motivos para utilizar o SDK

* A aplicação não possui funcionalidades de proteção de dados incorporadas
* A aplicação foi implementada numa loja de aplicações públicas, tais como o Google Play ou a App Store da Apple
* É um programador de aplicações e tem a formação técnica para utilizar o SDK
* A aplicação tem outras integrações SDK
* A aplicação é frequentemente atualizada

### <a name="supported-app-development-platforms"></a>Plataformas de desenvolvimento de aplicações suportadas

|**SDK da Aplicação do Intune** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Sim – utilizar os [Enlaces Xamarin do SDK da Aplicação Intune](app-sdk-xamarin.md).|Não|
|**Android**| Sim - use as [Ligações Intune App SDK Xamarin](app-sdk-xamarin.md).|Não|

## <a name="not-using-an-app-development-platform-listed-above"></a>Não está a usar uma plataforma de desenvolvimento de aplicações listada acima?

A equipa de desenvolvimento intune SDK testa e mantém ativamente o suporte para aplicações construídas com as plataformas nativas android, iOS (Obj-C, Swift), Xamarin e Xamarin.Forms. Embora alguns clientes tenham tido sucesso com a integração do Intune SDK com outras plataformas, como o React Native e o NativeScript, não fornecemos orientação explícita ou plugins para desenvolvedores de aplicações usando qualquer outra coisa que não as nossas plataformas suportadas. 

## <a name="feature-comparison"></a>Comparação de funcionalidades

Esta tabela lista as definições que estão ativadas se uma aplicação utilizar o App SDK ou a Ferramenta de Embrulho de Aplicações. Algumas funcionalidades exigem que os desenvolvedores de aplicações apliquem alguma lógica fora da integração básica com o Intune SDK, e como tal, não estão ativados se a aplicação utilizar a Ferramenta de Embrulho de Aplicações. 

|Funcionalidade|SDK da Aplicação|Ferramenta de Encapsulamento de Aplicações num Wrapper|
|-----------|---------------------|-----------|
|Restringir o conteúdo Web a apresentar num browser gerido pela empresa|X|X|
|Impedir cópias de segurança do Android, do iTunes ou do iCloud|X|X|
|Permitir que a aplicação transfira dados para outras aplicações|X|X|
|Permitir que a aplicação receba dados de outras aplicações|X|X|
|Restringir cortar, copiar e colar com outras aplicações|X|X|
|Especifique o número de caracteres que podem ser cortados ou copiados de uma aplicação gerida|X|X|
|Exigir PIN simples para acesso|X|X|
|Especificar o número de tentativas antes da redefinição do PIN|X|X|
|Permitir impressões digitais em vez do PIN|X|X|
|Permitir o reconhecimento facial em vez de PIN (apenas iOS)|X|X|
|Exigir credenciais da empresa para obter acesso|X|X|
|Definir uma expiração PIN|X|X|
|Bloquear a execução de aplicações geridas em dispositivos com jailbreak ou root|X|X|
|Encriptar dados da aplicação|X|X|
|Verificar novamente os requisitos de acesso após um número de minutos especificado|X|X|
|Especificar o período de tolerância offline|X|X|
|Bloquear captura de ecrã (apenas Android)|X|X|
|Suporte para MAM sem a inscrição de dispositivos|X|X|
|Limpeza completa dos dados da aplicação|X|X|
|Limpeza seletiva do trabalho e dados escolares em cenários multi-identidade <br><br>**Nota:** Para iOS/iPadOS, quando o perfil de gestão é removido, a aplicação também é removida.|X||
|Evitar "Guardar como"|X||
|Configuração de aplicação direcionada (ou config de aplicação através do "canal MAM")|X|X|
|Suporte para Identidades Múltiplas|X||
|Estilo Personalizável |X|||
|Ligações de VPN de aplicação a pedido com o mVPN da Citrix|X|X| 
|Desativar a sincronização de contactos|X|X|
|Desativar a impressão|X|X|
|Exigir versão mínima da aplicação|X|X|
|Exigir o sistema operativo mínimo|X|X|
|Exigir versão de patch de segurança mínima para Android (apenas Android)|X|X|
|Exigir SDK do Intune mínimo para iOS (apenas iOS)|X|X|
|Atestação de dispositivos SafetyNet (apenas Android)|X|X|
|Scan de ameaça em apps (apenas Android)|X|X|
|Exigir o nível máximo de risco do dispositivo de dispositivo de defesa de ameaça móvel|X||
|Configurar conteúdo de notificação de aplicativos para contas de organização|X|X|
|Exigir a utilização de teclados aprovados (apenas Android)|X|X|
|Exigir política de proteção de aplicativos (Acesso Condicional)|X||
|Exigir aplicação de cliente aprovada (Acesso Condicional)|X||

## <a name="next-steps"></a>Passos seguintes

Para saber mais sobre as políticas de proteção de aplicações e o Intune, veja os seguintes tópicos:

- [Ferramenta de encapsulamento de aplicações para Android](app-wrapper-prepare-android.md)<br>
- [Ferramenta de encapsulamento de aplicações para iOS](app-wrapper-prepare-ios.md)<br>
- [Utilizar o SDK para ativar aplicações para gestão de aplicações móveis](app-sdk.md)
