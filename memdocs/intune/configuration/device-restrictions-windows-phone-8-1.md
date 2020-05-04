---
title: Definições de restrição de dispositivos no Microsoft Intune para dispositivos Windows Phone 8.1
titleSuffix: ''
description: Saiba que definições do Intune pode utilizar para controlar as definições e funcionalidades em dispositivos Windows Phone 8.1.
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
ms.openlocfilehash: 285144e42f2a029bf2d24b96493c54922727d6dc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407650"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Definições de restrição de dispositivos Windows Phone 8.1 no Microsoft Intune

Este artigo mostra-lhe as definições de restrição de dispositivos do Microsoft Intune que pode configurar para dispositivos Windows Phone 8.1.

## <a name="general"></a>Geral

- **Câmara**: **Bloco** impede o acesso à câmara do dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

  Intune só consegue o acesso à câmara do dispositivo. Não tem acesso a fotografias ou vídeos.

- **Cópia e pasta**: **O bloco** evita a utilização de cópia e pasta entre aplicações no dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Armazenamento amovível**: **O bloco** evita a utilização de dispositivos de armazenamento externos em dispositivos, como cartões SD. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Geolocalização**: **Bloco** impede a ativação de serviços de localização em dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Conta Microsoft**: **O bloco** impede os utilizadores de associarem uma conta Microsoft ao dispositivo. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Captura do ecrã**: **O bloco** evita obter imagens nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Submissão de dados**de diagnóstico : **Bloqueia** os dispositivos de enviar dados de telemetria de diagnóstico e utilização para a Microsoft. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Sincronização de contas de e-mail personalizadas:** **O bloco** impede que os dispositivos se conectem a contas de e-mail não microsoft. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="password"></a>Palavra-passe

- **Palavra-passe**: **Exigir** que os utilizadores introduzam uma palavra-passe para aceder aos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Aplica-se apenas às contas locais. As palavras-passe da conta de domínio permanecem configuradas por Ative Directory (AD) e Azure AD.
  - Tipo de **palavra-passe necessário:** Escolha o tipo de senha. As opções são:
    - **Predefinição do dispositivo:** A palavra-passe pode incluir números e letras.
    - **Alfanumérico:** A palavra-passe deve ser uma mistura de números e letras.
    - **Numérico:** A palavra-passe só deve ser números.
  - Comprimento mínimo da **palavra-passe**: Introduza o número mínimo de caracteres necessários, de 4 a 16. Por exemplo, `6` introduza para exigir pelo menos seis caracteres no comprimento da palavra-passe.
  - **Palavras-passe simples**: **O bloco** impede os `1234` `1111`utilizadores de criarem senhas simples, tais como ou . Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
  - **Número de falhas de entrada antes de limpar o dispositivo**: Introduza o número de senhas erradas permitidas antes de os dispositivos serem limpos.
  - **Minutos máximos de inatividade até que o ecrã bloqueie**: Introduza o tempo de tempo em que um dispositivo deve ficar inativo antes de o ecrã estar automaticamente bloqueado. Por exemplo, `5` introduza os dispositivos de bloqueio após 5 minutos de inatividade. Quando definido para **Não configurado** ou deixado em branco, Intune não altera nem atualiza esta definição.
  - **Expiração da palavra-passe (dias)**: Introduza o tempo de tempo nos dias em que a palavra-passe do dispositivo deve ser alterada, de 1 a 255. Por exemplo, `90` introduza para expirar a palavra-passe após 90 dias. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
  - **Evite a reutilização de senhas anteriores**: Introduza o número de senhas anteriormente utilizadas que não podem ser utilizadas, de 1 a 24. Por exemplo, `5` introduza para que os utilizadores não possam definir uma nova senha para a sua senha atual ou qualquer uma das suas quatro senhas anteriores. Quando o valor está em branco, o Intune não altera nem atualiza esta definição.
- **Encriptação**: **Requer** encriptação no dispositivo, incluindo ficheiros. Nem todos os dispositivos suportam encriptação. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição. Para configurar esta definição e reportar corretamente a conformidade, configurar também:
  - **Requerer a palavra-passe**: Definir a **Requerer**.
  - **Tipo de palavra-passe requerida**: Definir para pelo menos **numérico**.
  - **Comprimento mínimo da palavra-passe**: Definir para pelo menos `4`.

## <a name="app-store"></a>App Store

- **Loja de aplicações**: **O bloco** impede que os utilizadores acedam à loja de aplicações. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="restricted-apps"></a>Aplicações restritas

Na lista de aplicações restritas, pode configurar uma das seguintes listas:

- **Aplicações bloqueadas**: Lista as aplicações (não geridas pela Intune) que os utilizadores não estão autorizados a instalar e executar.
- **Aplicações permitidas**: Lista as aplicações que os utilizadores estão autorizados a instalar. As aplicações geridas pelo Intune são automaticamente permitidas.

Para configurar a lista, clique em **Adicionar** e, em seguida, especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Como especificar o URL para uma aplicação na loja

Para especificar um URL de aplicação na lista de aplicações permitidas e bloqueadas, utilize o seguinte formato:

Na página [Loja Windows Phone](https://www.microsoft.com/store/apps/windows-phone), procure a aplicação que pretende utilizar.

Abra a página da aplicação e copie o URL para a área de redação. Agora pode usar este URL como URL na lista de aplicações permitidas ou bloqueadas.

Exemplo: procure a aplicação Skype na loja. O URL que deve utilizar é `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Opções adicionais

Também pode clicar **em Importar** para preencher a lista a partir de um ficheiro csv no formato <url de *aplicação*>, <nome de *aplicação*>, <editor de *aplicações*>, ou clicar na **Export** para criar um ficheiro csv contendo o conteúdo da lista de aplicações restritas no mesmo formato.

## <a name="browser"></a>Browser

- **Navegador web**: **O bloco** desliga o navegador web incorporado nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="cellular-and-connectivity"></a>Rede Móvel e Conectividade

- **Wi-Fi**: **O bloco** desativa a funcionalidade Wi-Fi nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Wi-Fi tethering**: **O bloco** evita a utilização de teters Wi-Fi nos dispositivos. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Ligue-se automaticamente aos hotspots Wi-Fi**: Permite que os dispositivos se conectem automaticamente a hotspots Wi-Fi gratuitos e aceitem automaticamente quaisquer termos de utilização.
- **Relatório sacar-se wi-fi**: **O bloco** impede que os dispositivos enviem informações de ligação de hotspot Wi-Fi. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **NFC**: **Bloquear** desativa operações que utilizam comunicações de campo (NFC) em dispositivos que o suportam. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.
- **Bluetooth**: **O bloco** impede os utilizadores de ativarem bluetooth. Quando definido para **Não configurado** (predefinido), Intune não altera nem atualiza esta definição.

## <a name="next-steps"></a>Passos seguintes

Para uma visão geral do perfil de restrições do dispositivo, consulte as definições de restrição do [dispositivo Configure no Microsoft Intune](device-restrictions-configure.md).
