---
title: Configure as definições de VPN nos dispositivos Windows 8.1 no Microsoft Intune - Azure  Microsoft Docs
description: Adicione ou crie um perfil de configuração VPN utilizando configurações de configuração de rede privada virtual (VPN), incluindo os detalhes da ligação, e as definições de procuração para incluir o endereço IP ou FQDN, e a porta TCP no Microsoft Intune em dispositivos que executam o Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 76813e4634e55651b44712fb486e0b1babcfba09
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331885"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Adicione as definições vpN nos dispositivos Do Windows 8.1 no Microsoft Intune



Este artigo mostra as definições do Intune que pode utilizar para configurar ligações VPN em dispositivos com o Windows 8.1.

Consoante as definições que escolher, nem todos os valores na lista seguinte serão configuráveis.

## <a name="base-vpn-settings"></a>Definições de VPN Base

- **Aplique todas as definições apenas no Windows 8.1:** Configure esta definição no portal clássico Intune. No centro de administração do Microsoft Endpoint Manager, esta definição não pode ser alterada. Quando definido para **configurar,** quaisquer definições são aplicadas apenas aos dispositivos Do Windows 8.1. Quando definidos para **não configurados,** estas definições também se aplicam aos dispositivos do Windows 10.
- **Nome da ligação**: introduza um nome para esta ligação. Os utilizadores verão este nome quando procurarem a lista de ligações VPN disponíveis no dispositivo.
- **Servidores**: adicione um ou mais servidores VPN aos quais os dispositivos são ligados.
  - **Adicionar**: Abre a página **Add Row** onde pode especificar as seguintes informações:
    - **Descrição**: Especificar um nome descritivo para o servidor como **o servidor Contoso VPN**.
    - **Endereço IP ou FQDN**: Forneça o endereço IP ou o nome de domínio totalmente qualificado do servidor VPN a que os dispositivos se ligam. Exemplos: **192.168.1.1**, **vpn.contoso.com**.
    - **Servidor predefinido**: define este servidor como o servidor predefinido que os dispositivos utilizam para estabelecer a ligação. Certifique-se de que predefine apenas um servidor.
  - **Importação**: Navegue para um ficheiro separado de víramida com a lista de servidores na descrição do formato, endereço IP ou FQDN, servidor Predefinido. Escolha **OK** para importar estes servidores para a lista **Servidores**.
  - **Exportação**: Exporta a lista de servidores para um ficheiro de valores comunados (csv).

- **Tipo de ligação**: selecione o tipo de ligação VPN a partir da seguinte lista de fornecedores:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn’t already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Grupo ou domínio** de login (apenas SonicWall Mobile Connect): Especifique o nome do grupo ou domínio de login a que pretende ligar.

- **Função** (apenas Pulse Secure): Especifique o nome da função do utilizador que tenha acesso a esta ligação. Uma função de utilizador define opções e definições pessoais e ativa ou desativa funcionalidades de acesso específicas.

- **Reino** (apenas Pulse Secure): Especifique o nome do reino de autenticação que pretende utilizar. Um realm de autenticação é um agrupamento de recursos de autenticação utilizado pelo tipo de ligação Pulse Secure.

- **XML personalizado**: Especifique quaisquer comandos XML personalizados que configurem a ligação VPN.

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

## <a name="proxy-settings"></a>Definições de proxy

- **Detete automaticamente as definições**de procuração : Se o seu servidor VPN necessitar de um servidor proxy para a ligação, especifique se pretende que os dispositivos detetem automaticamente as definições de ligação.
- **Script de configuração automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy**, que contém o ficheiro de configuração. Por exemplo, introduza `http://proxy.contoso.com`.
- **Utilize o servidor proxy**: Ative esta opção se pretender introduzir manualmente as definições do servidor proxy.
  - **Endereço**: Introduza o endereço do servidor proxy (como endereço IP).
  - **Número de porta**: introduza o número de porta associado ao servidor proxy.
- **Procuração de bypass para endereços locais**: Se o seu servidor VPN necessitar de um servidor proxy para a ligação, e não quiser utilizar o servidor proxy para endereços locais que introduz, então selecione esta opção.

## <a name="next-steps"></a>Próximos passos

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Configure as definições de VPN nos dispositivos [Android](vpn-settings-android.md), [Android Enterprise,](vpn-settings-android-enterprise.md) [macOS](vpn-settings-macos.md)e [Windows 10.](vpn-settings-windows-10.md)
