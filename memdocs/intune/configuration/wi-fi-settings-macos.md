---
title: Configurar as definições de Wi-Fi para dispositivos macOS no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Crie ou adicione um perfil de configuração de dispositivos Wi-Fi para dispositivos macOS. Veja as diferentes definições, incluindo a adição de certificados, a escolha de um tipo de EAP e a seleção de um método de autenticação no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e878294a9af6b80358aa495aa4d10ac6ed93404
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086352"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>Adicionar definições de Wi-Fi para dispositivos macOS no Microsoft Intune

Pode criar um perfil com definições de Wi-Fi específicas e, em seguida, implementar este perfil nos seus dispositivos macOS. O Microsoft Intune oferece muitas funcionalidades, incluindo a autenticação na rede, a adição de um certificado PKS ou SCEP e mais.

Estas definições de Wi-Fi estão separadas em duas categorias: Definições básicas e Definições de nível empresarial.

Este artigo descreve estas definições.

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil de dispositivo](wi-fi-settings-configure.md).

> [!NOTE]
> Estas configurações estão disponíveis para todos os tipos de inscrição. Para obter mais informações sobre os tipos de matrículas, consulte a [inscrição do macOS.](../enrollment/macos-enroll.md)

## <a name="basic-profiles"></a>Perfis básicos

- **Tipo de Wi-Fi**: escolha **Básico**.
- **Nome da rede**: introduza um nome para esta ligação Wi-Fi. Este valor é o nome que os utilizadores veem quando navegam na lista de ligações disponíveis nos seus dispositivos.
- **SSID**: sigla de **service set identifier** (identificador do conjunto de serviço). Esta propriedade é o nome real da rede sem fios à qual os dispositivos se ligam. No entanto, os utilizadores apenas veem o nome da rede configurada por si quando selecionam a ligação.
- **Ligar automaticamente**: escolha **Ativar** para ligar automaticamente a esta rede quando o dispositivo estiver dentro do alcance. Escolha **Desativar** para impedir que os dispositivos se liguem automaticamente.
- **Rede oculta**: escolha **Ativar** para ocultar esta rede da lista de redes disponíveis no dispositivo. O SSID não é difundido. Escolha **Desativar** para mostrar esta rede na lista de redes disponíveis no dispositivo.
- **Tipo de segurança**: selecione o protocolo de segurança para autenticar a rede Wi-Fi. As opções são:

  - **Abrir (sem autenticação)**: utilize esta opção apenas se a rede não estiver protegida.
  - **WPA/WPA2 – Pessoal**: introduza a palavra-passe na **Chave pré-partilhada**. Quando a rede da sua organização é configurada, uma chave de rede ou palavra-passe também é configurada. Introduza esta chave de rede ou palavra-passe para o valor PSK.
  - **WEP**

- **Definições de proxy**: as suas opções:
  - **Nenhuma**: não são configuradas definições de proxy.
  - **Manual**: introduza o **Endereço de servidor proxy** como um endereço IP e o **Número de porta** associado.
  - **Automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy** (por exemplo, `http://proxy.contoso.com`) que contém o ficheiro de configuração.

## <a name="enterprise-profiles"></a>Perfis empresariais

- **Tipo de Wi-Fi**: escolha **Empresarial**.
- **SSID**: sigla de **service set identifier** (identificador do conjunto de serviço). Esta propriedade é o nome real da rede sem fios à qual os dispositivos se ligam. No entanto, os utilizadores apenas veem o nome da rede configurada por si quando selecionam a ligação.
- **Ligar automaticamente**: escolha **Ativar** para ligar automaticamente a esta rede quando o dispositivo estiver dentro do alcance. Escolha **Desativar** para impedir que os dispositivos se liguem automaticamente.
- **Rede oculta**: escolha **Ativar** para ocultar esta rede da lista de redes disponíveis no dispositivo. O SSID não é difundido. Escolha **Desativar** para mostrar esta rede na lista de redes disponíveis no dispositivo.

- **Tipo de EAP**: escolha o tipo Protocolo EAP (Extensible Authentication Protocol) utilizado para autenticar as ligações sem fios protegidas. As opções são:

  - **EAP-FAST**: introduza as **Definições de PAC (Protected Access Credential)**. Esta opção utiliza credenciais de acesso protegido para criar um túnel autenticado entre o cliente e o servidor de autenticação. As opções são:
    - **Não utilizar (PAC)**
    - **Utilizar (PAC)**: se existir um ficheiro PAC, utilize-o.
    - **Utilizar e Aprovisionar PAC**: crie e adicione o ficheiro PAC aos seus dispositivos.
    - **Utilizar e Aprovisionar PAC Anonimamente**: crie e adicione o ficheiro PAC aos seus dispositivos sem autenticar no servidor.

  - **EAP-SIM**

  - **EAP-TLS**: introduza também:

    - **Nomes** - do servidor do**Certificado**de Confiança do Servidor : **Adicione** um ou mais nomes comuns utilizados nos certificados emitidos pela sua autoridade de certificados fidedignos (CA). Quando introduzir estas informações, pode ignorar a janela de confiança dinâmica apresentada nos dispositivos dos utilizadores quando estes se ligam a esta rede Wi-Fi.
    - **Certificado de raiz para a validação do servidor**: escolha um perfil de certificado de raiz fidedigna existente. Este certificado é apresentado ao servidor quando o cliente se liga à rede e serve para autenticar a ligação.

    - **Certificado** - cliente de autenticação do cliente**para autenticação do cliente (Certificado de identidade)**: Escolha o perfil de certificado de cliente SCEP ou PKCS que também está implantado no dispositivo. Este certificado é a identidade apresentada pelo dispositivo ao servidor para autenticar a ligação.

  - **EAP-TTLS**: introduza também:

    - **Nomes** - do servidor do**Certificado**de Confiança do Servidor : **Adicione** um ou mais nomes comuns utilizados nos certificados emitidos pela sua autoridade de certificados fidedignos (CA). Quando introduzir estas informações, pode ignorar a janela de confiança dinâmica apresentada nos dispositivos dos utilizadores quando estes se ligam a esta rede Wi-Fi.
    - **Certificado de raiz para a validação do servidor**: escolha um perfil de certificado de raiz fidedigna existente. Este certificado é apresentado ao servidor quando o cliente se liga à rede e serve para autenticar a ligação.

    - **Autenticação de Cliente** – escolha um **Método de autenticação**. As opções são:

      - **Nome de utilizador e Palavra-passe**: pedir ao utilizador um nome de utilizador e palavra-passe para autenticar a ligação. Introduza também:
        - **Método não EAP (identidade interna)**: escolha a forma como autentica a ligação. Garanta que escolhe o mesmo protocolo que está configurado na sua rede Wi-Fi.

          As suas opções: **Palavra-passe não encriptada (PAP)**, **Protocolo CHAP (Challenge Handshake Authentication Protocol)**, **Microsoft CHAP (MS-CHAP)** ou **Microsoft CHAP versão 2 (MS-CHAP v2)**

      - **Certificados**: escolha o perfil de certificado de cliente SCEP ou PKCS que também é implementado no dispositivo. Este certificado é a identidade apresentada pelo dispositivo ao servidor para autenticar a ligação.

      - **Privacidade de identidade (identidade externa)**: introduza o texto enviado em resposta a um pedido de identidade EAP. Este texto pode ser qualquer valor, como `anonymous`. Durante a autenticação, esta identidade anónima é inicialmente enviada, seguida pela identificação verdadeira enviada num túnel seguro.

  - **LEAP**

  - **PEAP**: introduza também:

    - **Nomes** - do servidor do**Certificado**de Confiança do Servidor : **Adicione** um ou mais nomes comuns utilizados nos certificados emitidos pela sua autoridade de certificados fidedignos (CA). Quando introduzir estas informações, pode ignorar a janela de confiança dinâmica apresentada nos dispositivos dos utilizadores quando estes se ligam a esta rede Wi-Fi.
    - **Certificado de raiz para a validação do servidor**: escolha um perfil de certificado de raiz fidedigna existente. Este certificado é apresentado ao servidor quando o cliente se liga à rede e serve para autenticar a ligação.

    - **Autenticação de Cliente** – escolha um **Método de autenticação**. As opções são:

      - **Nome de utilizador e Palavra-passe**: pedir ao utilizador um nome de utilizador e palavra-passe para autenticar a ligação. 

      - **Certificados**: escolha o perfil de certificado de cliente SCEP ou PKCS que também é implementado no dispositivo. Este certificado é a identidade apresentada pelo dispositivo ao servidor para autenticar a ligação.

      - **Privacidade de identidade (identidade externa)**: introduza o texto enviado em resposta a um pedido de identidade EAP. Este texto pode ser qualquer valor, como `anonymous`. Durante a autenticação, esta identidade anónima é inicialmente enviada, seguida pela identificação verdadeira enviada num túnel seguro.

- **Definições de proxy**: as suas opções:
  - **Nenhuma**: não são configuradas definições de proxy.
  - **Manual**: introduza o **Endereço de servidor proxy** como um endereço IP e o **Número de porta** associado.
  - **Automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy** (por exemplo, `http://proxy.contoso.com`) que contém o ficheiro de configuração.

## <a name="next-steps"></a>Passos seguintes

O perfil é criado, mas não faz nada. Em seguida, [atribua este perfil](device-profile-assign.md) e [monitorize o seu estado](device-profile-monitor.md).

Configure as definições de Wi-Fi nos dispositivos [Android,](wi-fi-settings-android.md) [Android Enterprise,](wi-fi-settings-android-enterprise.md) [iOS/iPadOS](wi-fi-settings-ios.md)e [Windows 10.](wi-fi-settings-windows.md)
