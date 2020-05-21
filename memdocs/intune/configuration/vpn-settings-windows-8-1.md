---
title: Configure as definições de VPN nos dispositivos Windows 8.1 no Microsoft Intune - Azure [ Microsoft Docs
description: Adicione ou crie um perfil de configuração VPN utilizando configurações de configuração de rede privada virtual (VPN), incluindo os detalhes da ligação, e as definições de procuração para incluir o endereço IP ou FQDN, e a porta TCP no Microsoft Intune em dispositivos que executam o Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556358"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Adicione as definições vpN nos dispositivos Do Windows 8.1 no Microsoft Intune

Este artigo mostra as definições do Intune que pode utilizar para configurar ligações VPN em dispositivos com o Windows 8.1.

Consoante as definições que escolher, nem todos os valores na lista seguinte serão configuráveis.

## <a name="before-you-begin"></a>Antes de começar

Crie um perfil de configuração do [dispositivo VPN do Windows 8.1](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Definições de VPN Base

- **Nome da ligação**: introduza um nome para esta ligação. Os utilizadores verão este nome quando procurarem a lista de ligações VPN disponíveis no dispositivo. Por exemplo, introduza `Contoso VPN`.
- **Servidores**: adicione um ou mais servidores VPN aos quais os dispositivos são ligados. Ao adicionar um servidor, introduza as seguintes informações:
  - **Descrição**: Introduza um nome descritivo para o servidor, tal como **o servidor Contoso VPN**.
  - **Endereço IP ou FQDN**: Introduza o endereço IP ou o nome de domínio totalmente qualificado (FQDN) do servidor VPN a que os dispositivos se ligam. Por exemplo, introduza: `192.168.1.1` ou `vpn.contoso.com`.
  - **Servidor predefinido**: **True** define este servidor como o servidor predefinido que os dispositivos utilizam para estabelecer a ligação. Defina apenas um servidor como o predefinido.
  - **Importação**: Navegue para um ficheiro separado de víramida com a lista de servidores no formato: descrição, endereço IP ou FQDN, servidor Predefinido. Escolha **OK** para importar estes servidores para a lista **Servidores**.
  - **Exportação**: Exporta a lista de servidores para um ficheiro de valores separados em vírem (csv).

- **Tipo de ligação**: selecione o tipo de ligação VPN. As opções são:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Grupo ou domínio** de login (apenas SonicWall Mobile Connect): Introduza o nome do grupo ou domínio de login a que pretende ligar.

- **Função** (apenas Pulse Secure): Introduza o nome da função do utilizador que pode aceder a esta ligação. Uma função de utilizador define opções e definições pessoais e ativa ou desativa funcionalidades de acesso específicas.

- **Reino** (apenas Pulse Secure): Introduza o nome do reino de autenticação que pretende utilizar. Um realm de autenticação é um agrupamento de recursos de autenticação utilizado pelo tipo de ligação Pulse Secure.

- **XML personalizado**: introduza todos os comandos XML personalizados que configuram a ligação VPN.

  **Exemplo seguro do pulso:**

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  Exemplo de **VPN móvel checkPoint:**

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Exemplo de Ligação Móvel SonicWall:**

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **Exemplo do Cliente F5 Edge:**

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Para obter mais informações sobre a escrita de comandos XML personalizados, consulte a documentação VPN do fabricante.

- **Túnel dividido**: **Ativar** os dispositivos permite que os dispositivos decidam qual a ligação a utilizar dependendo do tráfego. Por exemplo, um utilizador num hotel utiliza a ligação VPN para aceder aos ficheiros de trabalho, mas utiliza a rede padrão do hotel para a navegação normal na Internet. Se pretender que todo o tráfego utilize o túnel VPN quando a ligação VPN estiver ativa, em seguida, **desative**.

## <a name="proxy-settings"></a>Definições de proxy

- **Script de configuração automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy**, que contém o ficheiro de configuração. Por exemplo, introduza `http://proxy.contoso.com`.
- **Endereço**: Introduza o endereço do servidor proxy, como um endereço IP ou `vpn.contoso.com` .
- **Número**da porta : Introduza o número da porta TCP utilizado pelo seu servidor proxy.
- **Detetar automaticamente as definições de proxy**: se o seu servidor VPN precisar de um servidor proxy para a ligação, escolha se quer que os dispositivos detetem automaticamente as definições de ligação. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativar**: Deteta automaticamente as definições de ligação.
  - **Desativar**: Não deteta automaticamente as definições de ligação.
- **Procuração de bypass para endereços locais**: Escolha utilizar o servidor proxy para endereços locais. As opções são:
  - **Não configurado** (predefinido): Intune não altera nem atualiza esta definição.
  - **Ativar**: Não utilize um servidor proxy para endereços locais.
  - **Desativar**: Utilize um servidor proxy para endereços locais.

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Configure as definições de VPN nos dispositivos [Android](vpn-settings-android.md), [Android Enterprise,](vpn-settings-android-enterprise.md) [macOS](vpn-settings-macos.md)e [Windows 10.](vpn-settings-windows-10.md)
