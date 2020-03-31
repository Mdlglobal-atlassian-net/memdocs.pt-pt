---
title: Definições de restrição de dispositivos Windows 8.1 no Microsoft Intune - Azure Microsoft Docs
titleSuffix: ''
description: Saiba que definições do Intune pode utilizar para controlar as definições e funcionalidades em dispositivos com o Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407674"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Microsoft Intune Windows 8.1 definições de restrição de dispositivos

Este artigo mostra-lhe que o dispositivo Microsoft Intune configura as definições que pode configurar para dispositivos que executam o Windows 8.1.

## <a name="general"></a>Geral

- **Partilhar dados de utilização**: **O bloco** impede que os dispositivos enviem informações de telemetria de diagnóstico e utilização à Microsoft. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Firewall**: **Exija que** a Firewall do Windows seja ligada. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Controlo da conta do utilizador**: Configures o Controlo de Conta do Utilizador (UAC). Escolha como os utilizadores são notificados das alterações nos dispositivos. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Notificar sempre**
  - **Notificar sobre alterações de aplicativos**
  - **Notifique as alterações das aplicações, mas não diminua o ambiente de trabalho**
  - **Nunca notificar**

## <a name="password"></a>Palavra-passe

- Tipo de **palavra-passe necessário**: Escolha se o utilizador deve introduzir uma palavra-passe para aceder ao dispositivo. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Alfanumérico:** A palavra-passe deve ser uma mistura de números e letras.
  - **Numérico:** A palavra-passe só deve ser números.
- Comprimento mínimo da **palavra-passe**: Introduza o número mínimo de caracteres necessários, de 6 a 16. Por exemplo, insira `6` para exigir pelo menos seis números ou caracteres no comprimento da palavra-passe.
- **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de o dispositivo ser limpo, de 1 a 14.
- **Minutos máximos de inatividade até que o ecrã bloqueie (em minutos)** : Introduza o tempo de tempo em que um dispositivo deve ficar inativo antes de o ecrã estar automaticamente bloqueado, a partir de 1-60 minutos. Por exemplo, introduza `5` para bloquear o aparelho após 5 minutos de inativo. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.
- **Expiração da palavra-passe (dias)** : Introduza o tempo de tempo nos dias em que a palavra-passe do dispositivo deve ser alterada, de 1 a 255. Por exemplo, insira `90` para expirar a senha após 90 dias. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Evite a reutilização de senhas anteriores**: Introduza o número de senhas anteriormente utilizadas que não podem ser utilizadas, de 1 a 24. Por exemplo, introduza `5` para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Imagem palavra-passe e PIN**: **Bloquear** impede a utilização de uma imagem ou PIN como palavra-passe. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Uma palavra-passe por imagem permite ao utilizador iniciar sessão com gestos numa imagem. Um PIN permite aos utilizadores iniciar sessão rapidamente com um código de quatro dígitos.
- **Encriptação**: **Requer** encriptação em dispositivos, incluindo ficheiros. Nem todos os dispositivos suportam encriptação. Quando definido para **Não configurado**, Intune não altera nem atualiza esta definição.

  Para configurar esta definição e reportar corretamente a conformidade, configurar também:
  - **Tipo de palavra-passe requerida**: Definir para pelo menos **numérico**.
  - **Comprimento mínimo da palavra-passe**: Definir para pelo menos `4`.

  Para impor a encriptação nos dispositivos que executam o Windows 8.1, tem de instalar a [atualização de cliente MDM para Windows de dezembro de 2014](https://support.microsoft.com/kb/3013816) em cada dispositivo.

  Se ativar esta definição em dispositivos com o Windows 8.1, todos os utilizadores do dispositivo têm de ter uma conta Microsoft.

  Para que a encriptação funcione, os dispositivos devem satisfazer os requisitos de certificação de hardware [Do Microsoft InstantGo.](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97)

  Quando impõe a encriptação a um dispositivo, a chave de recuperação só é acessível a partir da conta Microsoft do utilizador, que é acedida a partir da respetiva conta do OneDrive. Não pode recuperar esta chave para um utilizador.

## <a name="browser"></a>Browser

- **Preenchimento automático**: **O bloco** impede que os utilizadores alterem as definições autocompletas no navegador e que povoem automaticamente os campos de formulários. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode permitir a auto-enchimento.
- **Avisos de fraude**: **Requer** avisos de fraude no navegador para potenciais sites fraudulentos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **SmartScreen para Microsoft Edge**: **O bloco** desliga o Microsoft Defender SmartScreen. O SmartScreen procura potenciais esquemas de phishing e software malicioso ao aceder a sites e downloads de ficheiros. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Por predefinição, o SISTEMA pode ligar o SmartScreen.
- **JavaScript**: **Bloco** impede que scripts, como javaScript, sejam executados no navegador. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Pop-ups**: **Block** liga O Blocker Pop-up para evitar pop-ups no navegador web. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Cabeçalhos não-rastreados**: **O bloco** impede que os dispositivos enviem cabeçalhos de não-rastrepara sites que solicitem informações de rastreio. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Plugins**: **O bloco** impede que os utilizadores adicionem plug-ins no Internet Explorer. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- Entrada de palavra única **no site da intranet**: A entrada de palavra única permite que os utilizadores se desloque a um site intranet, inserindo uma única palavra, como `hr` ou `benefits`. **Bloquear** impede esta funcionalidade. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Deteção automática do site intranet**: **O bloco** impede que o navegador detete automaticamente os sites intranet. As regras de mapeamento intranet estão bloqueadas. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Nível de segurança**na Internet : Define o nível de segurança dos sites da Internet. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Média**
  - **Médio-alto**
  - **Alta**
- **Nível de segurança intranet**: Define o nível de segurança para os sites intranet. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Baixa**
  - **Médio-baixo**
  - **Média**
  - **Médio-alto**
  - **Alta**
- **Nível de segurança de sites fidedignos**: Configura o nível de segurança para a zona de sites fidedignos. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Baixa**
  - **Médio-baixo**
  - **Média**
  - **Médio-alto**
  - **Alta**
- **Alta segurança para sites restritos**: Configura o nível de segurança para a zona de sites restritos. **Configurado** impõe alta segurança para sites restritos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Acesso ao menu do modo enterprise**: O **bloco** impede que os utilizadores acedam às opções do menu do Modo Empresarial no Internet Explorer. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Quando estiver definido para **bloquear,** introduza também:
  - **URL**de localização do relatório de registo : Insira um local de URL onde obter relatórios que mostrem os websites com acesso ao Modo Empresarial ligado.
- Localização da lista de sites do **modo enterprise (apenas desktop)** : Introduza a localização da lista de websites que podem ser abertos no Modo Enterprise.

## <a name="cellular"></a>Rede móvel

- **Roaming de dados**: **O bloco** impede o roaming de dados quando os dispositivos estão numa rede celular. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

- URL das **pastas**de trabalho : Introduza o URL da pasta de trabalho para permitir que os documentos sejam sincronizados entre os dispositivos. Quando definido para **Não configurado** (predefinido) ou deixado em branco, Intune não altera nem atualiza esta definição.
- **Acesso à aplicação Windows Mail sem conta Microsoft**: **O Bloco** impede o acesso à aplicação Windows Mail sem uma conta Microsoft. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="next-steps"></a>Próximos passos

Criar um perfil de restrições de dispositivos no [Windows 10 e mais recente](device-restrictions-windows-10.md).
