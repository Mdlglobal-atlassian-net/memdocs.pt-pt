---
title: Configure as definições vpN nos dispositivos Windows Phone 8.1 no Microsoft Intune - Azure Microsoft Docs
description: Adicione ou crie um perfil de configuração VPN utilizando configurações de configuração de rede privada virtual (VPN), incluindo os detalhes da ligação, e as definições de procuração para incluir o endereço IP ou FQDN, e a porta TCP no Microsoft Intune em dispositivos que executam o Windows Phone 8.1.
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
ms.openlocfilehash: df05c4b1a7a5ee3f30d33e40620a8a116f508333
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086486"
---
# <a name="add-vpn-settings-on-windows-phone-81-devices-in-microsoft-intune"></a>Adicione as definições vpN nos dispositivos Do Windows Phone 8.1 no Microsoft Intune

Este artigo mostra as definições do Intune que pode utilizar para configurar ligações VPN em dispositivos com o Windows Phone 8.1. 

Consoante as definições que escolher, nem todos os valores na lista seguinte serão configuráveis.

>[!IMPORTANT]
>Os perfis VPN do Windows Phone 8.1 também são aplicados aos dispositivos do Windows 10.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de configuração do [dispositivo VPN](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Definições de VPN Base

- **Aplique todas as definições apenas no Windows Phone 8.1:** Configure esta definição no portal clássico Intune. No centro de administração do Microsoft Endpoint Manager, esta definição não pode ser alterada. Quando definido para **configurar,** quaisquer definições são aplicadas apenas aos dispositivos Windows Phone 8.1. Quando definidas para **não configurar,** estas definições também se aplicam aos dispositivos Móveis do Windows 10.
- **Nome da ligação**: introduza um nome para esta ligação. Os utilizadores verão este nome quando procurarem a lista de ligações VPN disponíveis no dispositivo.
- **Método de autenticação**: escolha como os dispositivos serão autenticados no servidor VPN em:
  - **Certificados**: Sob **certificado de autenticação,** escolha um perfil de certificado SCEP ou PKCS que criou anteriormente para autenticar a ligação. Para obter mais informações sobre os perfis de certificado, veja [Como configurar certificados](../protect/certificates-configure.md).
  - **Nome de utilizador e palavra-passe**: Os utilizadores finais devem fornecer um nome de utilizador e uma senha para iniciar sessão no servidor VPN.
- **Servidores**: adicione um ou mais servidores VPN aos quais os dispositivos são ligados.
  - **Adicionar**: Abre a lâmina **Add Row** onde pode especificar as seguintes informações:
    - **Descrição**: Especificar um nome descritivo para o servidor como **o servidor Contoso VPN**.
    - **Endereço IP ou FQDN**: Forneça o endereço IP ou o nome de domínio totalmente qualificado do servidor VPN a que os dispositivos se ligam. Exemplos: **192.168.1.1,** **vpn.contoso.com**.
    - **Servidor predefinido**: define este servidor como o servidor predefinido que os dispositivos utilizam para estabelecer a ligação. Confirme que predefine apenas um servidor.
  - **Importação**: Navegue para um ficheiro separado de víramida com uma lista de servidores na descrição do formato, endereço IP ou FQDN, servidor Predefinido. Escolha **OK** para importar estes servidores para a lista **Servidores**.
  - **Exportação**: Exporta a lista de servidores para um ficheiro de valores separados em vírem (csv).

- **Bypass VPN na rede Wi-Fi**da empresa : Ative esta opção para especificar que as ligações VPN não são utilizadas quando o dispositivo está ligado à rede Wi-Fi da empresa.
- **Bypass VPN na rede Wi-Fi doméstica**: Ative esta opção para especificar que a ligação VPN não é utilizada quando o dispositivo está ligado a uma rede Wi-Fi doméstica.

- **Tipo de ligação**: selecione o tipo de ligação VPN. As opções são:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

- **Grupo ou domínio** de login (apenas SonicWall Mobile Connect): Especifique o nome do grupo ou domínio de login a que pretende ligar.
- **Função** (apenas Pulse Secure): Especifique o nome da função do utilizador que tenha acesso a esta ligação. Uma função de utilizador define opções e definições pessoais e ativa ou desativa funcionalidades de acesso específicas.
- **Reino** (apenas Pulse Secure): Especifique o nome do reino de autenticação que pretende utilizar. Um realm de autenticação é um agrupamento de recursos de autenticação utilizado pelo tipo de ligação Pulse Secure.

- Lista de pesquisa de **sufixo DNS**: **Adicione** um ou mais DNS suficientes. Cada sufixo DNS especificado é procurado ao ligar-se a um site com um nome abreviado. Por exemplo, especifique os sufixos DNS **domain1.contoso.com** e **domain2.contoso.com**, visite o URL `http://mywebsite` e os URLs `http://mywebsite.domain1.contoso.com` e `http://mywebsite.domain2.contoso.com` são pesquisados.

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

- **Túnel dividido**: **Ativar** os dispositivos permite que os dispositivos decidam qual a ligação a utilizar dependendo do tráfego. Por exemplo, um utilizador num hotel utiliza a ligação VPN para aceder aos ficheiros de trabalho, mas utiliza a rede padrão do hotel para a navegação normal na Internet. Se pretender que todo o tráfego utilize o túnel VPN quando a ligação VPN estiver ativa, em seguida, **desative**.

## <a name="proxy-settings"></a>Definições de proxy

- **Detete automaticamente as definições**de procuração : Se o seu servidor VPN necessitar de um servidor proxy para a ligação, especifique se pretende que os dispositivos detetem automaticamente as definições de ligação.
- **Script de configuração automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy** (por exemplo, `http://proxy.contoso.com`) que contém o ficheiro de configuração.
- **Utilize o servidor proxy**: Ative esta opção se pretender introduzir manualmente as definições do servidor proxy.
  - **Endereço**: Introduza o endereço do servidor proxy (como endereço IP).
  - **Número**da porta : Introduza o número de porta associado ao servidor proxy.
- **Procuração de bypass para endereços locais**: Se o seu servidor VPN necessitar de um servidor proxy para a ligação, e não quiser utilizar o servidor proxy para endereços locais que introduz, então selecione esta opção.

## <a name="next-steps"></a>Passos seguintes

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Configure as definições de VPN nos dispositivos [Android](vpn-settings-android.md), [Android Enterprise,](vpn-settings-android-enterprise.md) [macOS](vpn-settings-macos.md)e [Windows 10.](vpn-settings-windows-10.md)
