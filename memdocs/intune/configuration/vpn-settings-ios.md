---
title: Configure as definições vpN para dispositivos iOS/iPadOS no Microsoft Intune - Azure Microsoft Docs
description: Adicione ou crie um perfil de configuração VPN em dispositivos iOS/iPadOS utilizando configurações de configuração de rede privada virtual (VPN). Configure os detalhes de ligação, métodos de autenticação, túneis divididos, configurações vpN personalizadas com os pares de identificador, chave e valor, configurações VPN por app que incluam URLs de Safari e VPNs a pedido com Domínios de pesquisa SSIDs ou DNS, configurações de proxy para incluir um script de configuração, endereço IP ou FQDN, e porta TCP no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74e889419dcaaa75c2a31fe16931dddd84d1a967
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086542"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Adicione as definições vpN em dispositivos iOS e iPadOS no Microsoft Intune

O Microsoft Intune inclui muitas definições de VPN que podem ser implementadas nos seus dispositivos iOS/iPadOS. Estas definições são utilizadas para criar e configurar ligações VPN à rede da sua organização. Este artigo descreve estas definições. Algumas definições só estão disponíveis para alguns clientes VPN, tais como o Citrix, Zscaler, entre outros.

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração do dispositivo](vpn-settings-configure.md).

> [!NOTE]
> Estas configurações estão disponíveis para todos os tipos de inscrição. Para obter mais informações sobre os tipos de matrículas, consulte a [inscrição do iOS/iPadOS.](../enrollment/ios-enroll.md)

## <a name="connection-type"></a>Tipo de ligação

Selecione o tipo de ligação VPN na seguinte lista de fornecedores:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: aplicável à versão 4.0.5x e versões anteriores da aplicação [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924).
- **Cisco AnyConnect**: aplicável à versão 4.0.7x e versões posteriores da aplicação [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690).
- **SonicWall Mobile Connect**
- **F5 Access Legacy**: aplicável a versão 2.1 e versões anteriores da aplicação F5 Access.
- **F5 Access**: aplicável a versão 3.0 e versões posteriores da aplicação F5 Access.
- **Palo Alto Networks GlobalProtect (Legacy)**: aplicável a versão 4.1 e versões anteriores da aplicação Palo Alto Networks GlobalProtect.
- **Palo Alto Networks GlobalProtect**: aplicável a versão 5.0 e versões posteriores da aplicação Palo Alto Networks GlobalProtect.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**: Para utilizar o Acesso Condicional, ou permitir que os utilizadores contornem o sinal de Zscaler no ecrã, então deve integrar o Acesso Privado zscaler (ZPA) com a sua conta Azure AD. Para obter passos detalhados, veja a [documentação do Zscaler](https://help.zscaler.com/zpa/configuration-example-microsoft-azure-ad). 
- **IKEv2**: [As definições IKEv2](#ikev2-settings) (neste artigo) descrevem as propriedades.
- **VPN Personalizada**

> [!NOTE]
> A Cisco, Citrix, F5 e Palo Alto anunciaram que os seus clientes legados não funcionam no iOS 12. Deverá migrar para as novas aplicações logo que possível. Para obter mais informações, veja o [Blogue da Equipa de Suporte do Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Definições de VPN Base

As definições apresentadas na seguinte lista são determinadas pelo tipo de ligação VPN que escolher.  

- **Nome da ligação**: os utilizadores finais verão este nome quando procurarem uma lista de ligações VPN disponíveis no dispositivo.
- **Nome de domínio personalizado** (apenas Zscaler): Pré-povoar o sinal da aplicação Zscaler no campo com o domínio a que os seus utilizadores pertencem. Por exemplo, se um nome de utilizador for `Joe@contoso.net`, o domínio `contoso.net` será apresentado estaticamente no campo ao abrir a aplicação. Se não introduzir um nome de domínio, será utilizada a parte do domínio do UPN no Azure Active Directory (AD).
- **Endereço IP ou FQDN**: o endereço IP ou nome de domínio completamente qualificado (FQDN) do servidor VPN ao qual os dispositivos são ligados. Por exemplo, introduza: `192.168.1.1` ou `vpn.contoso.com`.
- **Nome da cloud da organização** (apenas Zscaler): introduza o nome da cloud em que a sua organização está aprovisionada. O URL que utiliza para iniciar sessão no Zscaler contém o nome.  
- **Método de autenticação**: selecione como os dispositivos serão autenticados no servidor VPN. 
  - **Certificados**: em **Certificado de autenticação**, selecione um perfil de certificado SCEP ou PKCS existente para autenticar a ligação. O tópico [Configurar certificados](../protect/certificates-configure.md) fornece algumas orientações sobre perfis de certificado.
  - **Nome de utilizador e palavra-passe**: os utilizadores finais têm de introduzir um nome de utilizador e uma palavra-passe para iniciar sessão no servidor VPN.  

    > [!NOTE]
    > Se o nome de utilizador e a palavra-passe forem utilizados como o método de autenticação do Cisco IPsec VPN, os primeiros têm de enviar o parâmetro SharedSecret através de um perfil personalizado do Apple Configurator.

  - **Credencial derivada:** Utilize um certificado derivado do cartão inteligente de um utilizador. Se nenhum emitente credencial derivado estiver configurado, Intune pede-lhe para adicionar um. Para mais informações, consulte [Use credenciais derivadas no Microsoft Intune](../protect/derived-credentials.md).

- **URLs excluídos** (apenas Zscaler): quando estiver ligado à VPN do Zscaler, os URLs apresentados estarão acessíveis fora da cloud do Zscaler. 

- **Dividir túnel**: **ative** ou **desative** esta opção para permitir que os dispositivos decidam qual a ligação a utilizar consoante o tráfego. Por exemplo, um utilizador num hotel utiliza a ligação VPN para aceder aos ficheiros de trabalho, mas utiliza a rede padrão do hotel para a navegação normal na Internet.

- **Identificador VPN** (VPN personalizado, Zscaler e Citrix): Um identificador para a aplicação VPN que está a usar, e é fornecido pelo seu fornecedor VPN.
- **Introduza pares chave/valor para os atributos VPN personalizados da sua organização** (VPN personalizado, Zscaler e Citrix): Adicione ou importe **Chaves** e **Valores** que personalizem a sua ligação VPN. Lembre-se de que estes valores são habitualmente disponibilizados pelo seu fornecedor de VPN.

- Ativar o controlo de acesso à **rede (NAC)** (Cisco AnyConnect, Citrix SSO, Acesso F5): Quando **escolher, concordo,** o ID do dispositivo está incluído no perfil VPN. Este ID pode ser utilizado para autenticação na VPN para permitir ou impedir o acesso à rede.

  **Ao utilizar o Cisco AnyConnect com o ISE,** certifique-se de:

  - Se ainda não o fez, integre o ISE com o Intune para o NAC, como descrito na **Configure Microsoft Intune como um Servidor MDM** no Guia de Administrador de Motores de [Serviços](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)de Identidade da Cisco .
  - Ativar o NAC no perfil VPN.

  **Ao utilizar o Citrix SSO com gateway,** certifique-se de:

  - Confirme que está a usar citrix Gateway 12.0.59 ou superior.
  - Confirme que os seus utilizadores têm Citrix SSO 1.1.6 ou posteriormente instalados nos seus dispositivos.
  - Integrar citrix Gateway com Intune para NAC. Consulte o guia de implementação da Microsoft Intune/Enterprise Mobility com o Guia de Implementação da [Citrix NetScaler (LDAP+OTP Scenario).](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf)
  - Ativar o NAC no perfil VPN.

  Ao utilizar o **Acesso F5,** certifique-se de:

  - Confirme que está a usar F5 BIG-IP 13.1.1.5 ou mais tarde. 
  - Integrar big-IP com Intune para NAC. Consulte a [visão geral: Configurar o APM para verificação](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) da postura do dispositivo com o guia F5 dos sistemas de gestão de pontos finais.
  - Ativar o NAC no perfil VPN.

  Para os parceiros VPN que suportam o ID do dispositivo, o cliente VPN, como citrix SSO, pode obter o ID. Em seguida, pode consultar Intune para confirmar que o dispositivo está matriculado, e se o perfil VPN estiver em conformidade ou não.

  - Para remover esta definição, volte a criar o perfil e não selecione a opção **Concordo**. Em seguida, atribua novamente o perfil.

## <a name="ikev2-settings"></a>Definições IKEv2

Estas definições aplicam-se quando escolhe o **tipo** > de ligação**IKEv2**.

- **VPN sempre ligado**: **Ativar** configura um cliente VPN para ligar e voltar a ligar-se automaticamente à VPN. As ligações VPN Sempre Ativada permanecem ativadas ou ativam-se imediatamente quando o utilizador bloqueia o dispositivo, quando o dispositivo é reiniciado ou quando a rede sem fios é alterada. Quando definido para **Desativar** (predefinido), vpN sempre ligado para todos os clientes VPN é desativado. Quando ativado, configure também:

  - **Interface de rede**: Todas as definições IKEv2 aplicam-se apenas à interface de rede que escolher. As opções são:
    - **Wi-Fi e Cellular** (predefinido): As definições IKEv2 aplicam-se ao Wi-Fi e às interfaces celulares do dispositivo.
    - **Celular**: As definições IKEv2 aplicam-se apenas à interface celular do dispositivo. Selecione esta opção se estiver a implementar em dispositivos com a interface Wi-Fi desativada ou removida.
    - **Wi-Fi**: As definições IKEv2 aplicam-se apenas à interface Wi-Fi do dispositivo.
  - **Utilizador para desativar a configuração VPN**: **Ativar** permite que os utilizadores desliguem o VPN sempre ligado. **Desativar** (predefinido) impede os utilizadores de o desligarem. O valor predefinido para esta definição é a opção mais segura.
  - **Correio de voz**: Escolha o que acontece com o tráfego de correio de voz quando a VPN sempre ligado estiver ativada. As opções são:
    - Tráfego de rede de força através de **VPN** (predefinição): Esta definição é a opção mais segura.
    - **Permitir que o tráfego de rede passe para fora da VPN**
    - **Tráfego de rede de queda**
  - **AirPrint**: Escolha o que acontece com o tráfego AirPrint quando a VPN sempre ligado estiver ativada. As opções são:
    - Tráfego de rede de força através de **VPN** (predefinição): Esta definição é a opção mais segura.
    - **Permitir que o tráfego de rede passe para fora da VPN**
    - **Tráfego de rede de queda**
  - **Serviços celulares**: No iOS 13.0+, escolha o que acontece com o tráfego celular quando a VPN sempre ligado está ativada. As opções são:
    - Tráfego de rede de força através de **VPN** (predefinição): Esta definição é a opção mais segura.
    - **Permitir que o tráfego de rede passe para fora da VPN**
    - **Tráfego de rede de queda**
  - Permitir que o tráfego de aplicações de rede cativa não **nativas passe para fora da VPN**: Uma rede cativa refere-se a hotspots Wi-Fi tipicamente encontrados em restaurantes e hotéis. As opções são:
    - **Não**: Força todo o tráfego de aplicações de rede cativa (CN) através do túnel VPN.
    - **Sim, todas as aplicações**: Permite que todo o tráfego de aplicações CN contorne a VPN.
    - **Sim, aplicações específicas**: **Adicione** uma lista de aplicações CN cujo tráfego pode contornar a VPN. Introduza os identificadores de pacote da aplicação CN. Por exemplo, introduza `com.contoso.app.id.package`.

  - **Tráfego da aplicação Websheet Cativa para passar fora VPN**: WebSheet cativo é um navegador web incorporado que lida com o sinal cativo. **O Enable** permite que o tráfego de aplicações do navegador contorne a VPN. **Desativar** (predefinido) o tráfego webSheet para utilizar o VPN sempre ligado. O valor predefinido é a opção mais segura.
  - **A tradução de endereços de rede (NAT) mantém o intervalo vivo (segundos)**: Para se manter ligado à VPN, o dispositivo envia pacotes de rede para se manter ativo. Introduza um valor em segundos sobre a frequência com que estes pacotes são enviados, de 20-1440. Por exemplo, insira um valor para enviar os pacotes de `60` rede para a VPN a cada 60 segundos. Por predefinição, este `110` valor é definido para segundos.
  - **Descarregue o NAT mantenha-se vivo no hardware quando**o dispositivo estiver a dormir : Quando um dispositivo está a dormir, **o Enable** (padrão) tem o NAT a enviar pacotes de keep-alive para que o dispositivo permaneça ligado à VPN. **Desativar** desativa esta funcionalidade.

- **Identificador remoto**: Introduza o endereço IP da rede, FQDN, UserFQDN ou ASN1DN do servidor IKEv2. Por exemplo, introduza: `10.0.0.3` ou `vpn.contoso.com`. Normalmente, introduz-se no mesmo valor que o [**nome Ligação**](#base-vpn-settings) (neste artigo). Mas depende das definições do servidor IKEv2.

- Tipo de **Autenticação do Cliente**: Escolha como o cliente VPN autentica à VPN. As opções são:
  - **Autenticação do utilizador** (predefinido): As credenciais do utilizador autenticam-se na VPN.
  - **Autenticação da máquina**: As credenciais do dispositivo autenticam-se na VPN.

- Método de **autenticação**: Escolha o tipo de credenciais do cliente para enviar para o servidor. As opções são:
  - **Certificados**: Utiliza um perfil de certificado existente para autenticar a VPN. Certifique-se de que este perfil de certificado já está atribuído ao utilizador ou dispositivo. Caso contrário, a ligação VPN falha.
    - Tipo de **certificado:** Selecione o tipo de encriptação utilizado pelo certificado. Certifique-se de que o servidor VPN está configurado para aceitar este tipo de certificado. As opções são:
      - **RSA** (padrão)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Nome de utilizador e palavra-passe** (apenas autenticação do utilizador): Quando os utilizadores se ligam à VPN, são solicitados para o seu nome de utilizador e palavra-passe.
  - **Segredo partilhado** (apenas autenticação da máquina): Permite-lhe introduzir um segredo partilhado para enviar para o servidor VPN.
    - **Segredo partilhado**: Enter the shared secret, também conhecido como a chave pré-partilhada (PSK). Certifique-se de que o valor corresponde ao segredo partilhado configurado no servidor VPN.

- **Nome comum do emitente**do certificado do servidor : Permite que o servidor VPN autentique ao cliente VPN. Introduza o nome comum do emitente de certificado (CN) do certificado de servidor VPN que é enviado ao cliente VPN no dispositivo. Certifique-se de que o valor NC corresponde à configuração do servidor VPN. Caso contrário, a ligação VPN falha.
- **Nome comum**do certificado do servidor : Introduza o NC para o próprio certificado. Se ficar em branco, o valor do identificador remoto é utilizado.

- **Taxa de deteção**de pares mortos : Escolha com que frequência o cliente VPN verifica se o túnel VPN está ativo. As opções são:
  - **Não configurado:** Utiliza o predefinido do sistema iOS/iPadOS, que pode ser o mesmo que escolher **Medium**.
  - **Nenhum:** Desativa a deteção de pares mortos.
  - **Baixo:** Envia uma mensagem de manutenção viva a cada 30 minutos.
  - **Médio** (padrão): Envia uma mensagem de manutenção a cada 10 minutos.
  - **Alta:** Envia uma mensagem de manutenção viva a cada 60 segundos.

- Gama mínima da **versão TLS**: Introduza a versão TLS mínima para utilizar. Insira, `1.0` `1.1`ou `1.2`. Se ficar em branco, `1.0` o valor predefinido é utilizado.
- Gama máxima da **versão TLS**: Introduza a versão TLS máxima a utilizar. Insira, `1.0` `1.1`ou `1.2`. Se ficar em branco, `1.2` o valor predefinido é utilizado.

> [!NOTE]
> A gama de versão TLS é mínima e máxima deve ser definida quando utilizar a autenticação do utilizador e os certificados.

- **Sigilo perfeito para a frente**: Selecione **Ativar** para ativar o sigilo perfeito para a frente (PFS). O PFS é uma funcionalidade de segurança IP que reduz o impacto se uma chave de sessão estiver comprometida. **Desativar** (predefinido) não utiliza PFS.
- **Verificação de revogação**do certificado : Selecione **Ativar** para se certificar de que os certificados não são revogados antes de permitir que a ligação VPN tenha sucesso. Este cheque é o melhor esforço. Se o servidor VPN se esgotar antes de determinar se o certificado é revogado, o acesso é concedido. **Desativar** (predefinido) não verifica se há certificados revogados.

- **Configurar os parâmetros**da associação de segurança: **Não configurado** (predefinido) utiliza a predefinição do sistema iOS/iPadOS. Selecione **Ativar** para introduzir os parâmetros utilizados ao criar associações de segurança com o servidor VPN:
  - **Algoritmo de encriptação:** Selecione o algoritmo que deseja:
    - DES
    - 3DES
    - AES-128
    - AES-256 (padrão)
    - AES-128-GCM
    - AES-256-GCM
  - **Algoritmo de integridade:** Selecione o algoritmo que deseja:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (padrão)
    - SHA2-384
    - SHA2-512
  - **Grupo Diffie-Hellman**: Selecione o grupo que deseja. Padrão é `2`grupo .
  - **Duração da vida** (minutos): Escolha quanto tempo a associação de segurança permanece ativa até que as teclas sejam rodadas. Introduza um `10` valor `1440` inteiro entre e (1440 minutos são 24 horas). A predefinição é `1440`.

- **Configure um conjunto separado de parâmetros para associações de segurança infantil**: iOS/iPadOS permite configurar parâmetros separados para a ligação IKE e quaisquer ligações infantis. 

  **Não configurado** (predefinido) utiliza os valores que introduz na definição de parâmetros de associação de **segurança Configuração** anterior. Selecione **Ativar** para introduzir os parâmetros utilizados na criação de associações de segurança *infantil* com o servidor VPN:
  - **Algoritmo de encriptação:** Selecione o algoritmo que deseja:
    - DES
    - 3DES
    - AES-128
    - AES-256 (padrão)
    - AES-128-GCM
    - AES-256-GCM
  - **Algoritmo de integridade:** Selecione o algoritmo que deseja:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (padrão)
    - SHA2-384
    - SHA2-512
  - **Grupo Diffie-Hellman**: Selecione o grupo que deseja. Padrão é `2`grupo .
  - **Duração da vida** (minutos): Escolha quanto tempo a associação de segurança permanece ativa até que as teclas sejam rodadas. Introduza um `10` valor `1440` inteiro entre e (1440 minutos são 24 horas). A predefinição é `1440`.

## <a name="automatic-vpn-settings"></a>Definições Automáticas de VPN

- **VPN por aplicação**: ativa a VPN por aplicação. Permite que a ligação VPN seja acionada automaticamente quando determinadas aplicações forem abertas. Também associa as aplicações com este perfil VPN. A VPN por aplicação não é suportada no IKEv2. Para mais informações, consulte [as instruções para a configuração de VPN por aplicação para iOS/iPadOS](vpn-setting-configure-per-app.md). 
  - **Tipo de Fornecedor**: disponível apenas para o Pulse Secure e a VPN Personalizada.
  - Ao utilizar perfis **VPN** iOS/iPadOS por app com Pulse Secure ou uma VPN personalizada, escolha túneis de camada de aplicação (procuração de aplicações) ou túneis de nível de pacote (túnel de pacote). Defina o valor **ProviderType** para **proxy-da-aplicação**, para o túnel de camada de aplicação ou para **pacote-túnel**, para o túnel de camada de pacote. Se não tiver a certeza sobre o valor a utilizar, consulte a documentação do seu fornecedor de VPN.
  - **URLs do Safari que irão acionar esta VPN**: adicione um ou mais URLs de sites. Quando estes URLs são visitados através do browser Safari no dispositivo, a ligação VPN é estabelecida automaticamente.

- **VPN a pedido**: configure regras condicionais que controlam quando a ligação VPN é iniciada. Por exemplo, crie uma condição na qual a ligação VPN só é utilizada quando um dispositivo não estiver ligado a uma rede Wi-Fi da sua empresa. Ou criar uma condição. Por exemplo, se um dispositivo não conseguir aceder a um domínio de pesquisa DNS em que entra, então a ligação VPN não foi iniciada.

  - **SSIDs ou domínios de pesquisa DNS**: selecione se esta condição utiliza **SSIDs** de rede sem fios ou **domínios de pesquisa DNS**. Escolha **Adicionar** para configurar um ou mais SSIDs ou domínios de pesquisa.
  - **Pesquisa de cadeia de URL**: opcional. Introduza um URL para a regra utilizar como um teste. Se o dispositivo aceder a este URL sem reorientação, então a ligação VPN é iniciada. Além disso, o dispositivo será ligado ao URL de destino. O utilizador não vê o site de pesquisa de cadeia de URL.

    Por exemplo, uma sonda de cadeia de URL é um URL de servidor Web auditando que verifica a conformidade do dispositivo antes de ligar o VPN. Ou, o URL testa a capacidade da VPN de se ligar a um site antes de o dispositivo se ligar ao URL do alvo através da VPN.

  - **Ação de domínio**: selecione um dos seguintes itens:
    - Ligar se necessário
    - Nunca ligar
  - **Ação**: selecione um dos seguintes itens:
    - Ligar
    - Avaliar a ligação
    - Ignorar
    - Desligar

## <a name="proxy-settings"></a>Definições de proxy

Se estiver a utilizar um proxy, configure as definições seguintes. As definições de proxy não estão disponíveis para ligações VPN do Zscaler.  

- **Script de configuração automática**: utilize um ficheiro para configurar o servidor proxy. Introduza o **URL do servidor proxy** (por exemplo, `http://proxy.contoso.com`) que inclui o ficheiro de configuração.
- **Endereço**: introduza o endereço IP do nome do anfitrião totalmente qualificado do servidor proxy.
- **Número**da porta : Introduza o número de porta associado ao servidor proxy.

## <a name="next-steps"></a>Passos seguintes

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Configure as definições de VPN nos dispositivos [Android](vpn-settings-android.md), [Android Enterprise,](vpn-settings-android-enterprise.md) [macOS](vpn-settings-macos.md)e [Windows 10.](vpn-settings-windows-10.md)
