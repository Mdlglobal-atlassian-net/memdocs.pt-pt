---
title: Definições de dispositivos Holográficos do Windows Business - Microsoft Intune - Azure [ Microsoft Docs
description: Leia e configure as definições de restrição de dispositivos no Microsoft Intune para Windows Holographic for Business, incluindo não-inscrição, geolocalização, palavras-passe, instalar aplicações a partir de app store, cookies e pop ups no Microsoft Edge, Microsoft Defender, pesquisa, nuvem e armazenamento, conectividade bluetooth, tempo do sistema e dados de utilização no Azure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/13/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a207c34c0d46b423eda44abf953e9c084cc9b2d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078231"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Windows Holographic for Business device definições para permitir ou restringir funcionalidades usando Intune



Este artigo lista e descreve as diferentes definições que pode controlar no Windows Holographic para dispositivos Empresariais, como o Microsoft Hololens. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para permitir ou desativar funcionalidades, segurança de controlo e muito mais.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](device-restrictions-configure.md#create-the-profile).

## <a name="general"></a>Geral

- **Desinscrição manual**: Permite ao utilizador apagar manualmente a conta do local de trabalho do dispositivo.
- **Cortana**: Ativar ou desativar o assistente de voz cortana.
- **Geolocalização**: Especifica se o dispositivo pode utilizar informações sobre os serviços de localização.

## <a name="password"></a>Palavra-passe

- **Palavra-passe**: Exija que o utilizador final introduza uma senha para aceder ao dispositivo.
- **Requerer uma palavra-passe quando o dispositivo regressar do estado inativo**: Especifica que o utilizador deve introduzir uma palavra-passe para desbloquear o dispositivo.

## <a name="app-store"></a>App Store

- **Aplicações de atualização automática a partir da loja**: Permite que as aplicações instaladas a partir da Microsoft Store sejam atualizadas automaticamente.
- **Instalação de aplicativos fidedignos**: Permite que as aplicações assinadas com um certificado de confiança sejam carregadas de lado.
- **Desbloqueio do desenvolvedor**: Permitir configurações de desenvolvedores do Windows, tais como permitir que as aplicações paradas sejam modificadas pelo utilizador final.

## <a name="microsoft-edge-browser"></a>Browser Microsoft Edge

- **Cookies**: Permite que o navegador guarde os cookies de internet para o dispositivo.
- **Pop-ups**: Bloqueia janelas pop-up no navegador (aplica-se apenas ao Windows 10).
- **Sugestões de pesquisa**: Permite que o seu motor de pesquisa sugira sites à medida que escreve frases de pesquisa.
- **Gestor de passwords**: Ative ou desative a funcionalidade Microsoft Edge Password Manager.
- **Envie cabeçalhos de não-rastreio**: Configures o navegador Microsoft Edge para enviar não rastreie os cabeçalhos para os websites que os utilizadores visitam.

## <a name="microsoft-defender-smart-screen"></a>Ecrã Inteligente Microsoft Defender

- **SmartScreen para Microsoft Edge**: Ative o Microsoft Edge SmartScreen para aceder ao site e aos downloads de ficheiros.

## <a name="search"></a>Pesquisa

- **Procurar localização** – especifica se a pesquisa pode utilizar informações de localização. informações

## <a name="cloud-and-storage"></a>Cloud e Armazenamento

- **Conta Microsoft**: Permite ao utilizador associar uma conta Microsoft ao dispositivo.

## <a name="cellular-and-connectivity"></a>Rede Móvel e Conectividade

- **Bluetooth**: Controla se o utilizador pode ativar e configurar Bluetooth no dispositivo.
- **Descoberta Bluetooth**: Permite que o dispositivo seja descoberto por outros dispositivos ativados por Bluetooth.
- **Publicidade Bluetooth**: Permite que o dispositivo receba anúncios sobre Bluetooth.

## <a name="control-panel-and-settings"></a>Painel de Controlo e Definições

- **Modificação do tempo**do sistema : Impede o utilizador final de alterar a data e a hora do dispositivo.

## <a name="kiosk---obsolete"></a>Quiosque – Obsoleto

Estas definições são só de leitura e não podem ser alteradas. Para configurar o modo de quiosque, veja [Definições de quiosque](kiosk-settings-holographic.md).

Normalmente, um dispositivo de quiosque executa uma aplicação específica. Os utilizadores são impedidos de aceder a funcionalidades ou funções no dispositivo fora da aplicação de quiosque.

- **Modo quiosque**: Identifica o tipo de modo quiosque suportado pela apólice. As opções incluem:

  - **Não configurado** (predefinição): a política não ativa um modo de quiosque. 
  - Quiosque de **aplicações únicas**: O perfil permite que o dispositivo execute apenas uma aplicação. Quando um utilizador inicia sessão, uma aplicação específica é iniciada. Este modo também impede que o utilizador abra novas aplicações ou mude a aplicação em execução.
  - **Quiosque multi-aplicativos**: O perfil permite que o dispositivo execute várias aplicações. Apenas as aplicações que adicionar estão disponíveis para o utilizador. A vantagem de um quiosque de várias aplicações ou dispositivos de objetivo fixo é o facto de proporcionar uma experiência fácil de compreender pelos utilizadores através do acesso às aplicações de que precisam. E, removendo as aplicações de que não precisam da sua visão. 
  
    Ao adicionar aplicações a uma experiência de quiosque de várias aplicações, também adiciona um ficheiro de esquema do menu Iniciar. O [ficheiro de esquema do menu Iniciar](/hololens/hololens-kiosk#start-layout-file-for-mdm-intune-and-others) inclui um XML de exemplo que pode ser utilizado no Intune. 

### <a name="single-app-kiosks"></a>Quiosques de uma aplicação

Introduza as seguintes definições:

- **Conta de utilizador**: Introduza a conta de utilizador local (no dispositivo) ou o login da conta Azure AD associado à aplicação do quiosque. Para contas associadas a domínios do Azure AD, introduza a conta com o formato `domain\username@tenant.org`. 

    Para ambientes de quiosque com início de sessão automático ativado, deve ser utilizado um tipo de utilizador com o menor privilégio (tal como a conta de utilizador padrão local). Para configurar uma conta do Azure Active Directory (AD) para o modo de quiosque, utilize o formato `AzureAD\user@contoso.com`.

- Id do **modelo de utilizador da aplicação (AUMID) da aplicação**: Introduza o AUMID da aplicação de quiosque. Para saber mais, veja [Find the Application User Model ID of an installed app (Localizar o ID de Modelo do Utilizador da Aplicação de uma aplicação instalada)](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

## <a name="reporting-and-telemetry"></a>Relatórios e Telemetria

- **Partilhar dados de utilização**: Selecione o nível de submissão de dados de diagnóstico.

## <a name="next-steps"></a>Passos seguintes

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
