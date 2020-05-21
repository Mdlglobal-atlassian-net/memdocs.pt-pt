---
title: Configurações de firewall de segurança de ponto final intune / Microsoft Docs
description: Definições de política de firewall de segurança endpoint para Windows e macOS no Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431291"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Definições de política de firewall para segurança de ponto final em Intune

Ver as definições que pode configurar em perfis para a política *firewall* no nó de segurança de Ponto final de Intune como parte de uma política de [segurança endpoint](../protect/endpoint-security-policy.md).

Plataformas e perfis suportados:

- **macOS**:
  - Perfil: **firewall macOS**

- **Windows 10 e mais tarde:**
  - Perfil: **Microsoft Defender Firewall**

## <a name="macos-firewall-profile"></a>perfil de firewall macOS

### <a name="firewall"></a>Firewall

As seguintes definições são configuradas como política de [segurança de ponto final para firewalls macOS](../protect/endpoint-security-firewall-policy.md)

- **Ativar firewall**

  - **Não configurado** *(predefinido)*
  - **Sim** - Ativar a firewall.
  
  Quando definido para *Sim,* pode configurar as seguintes definições.  

  - **Bloquear todas as ligações a receber**

    - **Não configurado** *(predefinido)*
    - **Sim** - Bloqueie todas as ligações de entrada, exceto ligações que são necessárias para serviços básicos de Internet tais como DHCP, Bonjour e IPSec. Isto bloqueia todos os serviços de partilha.

  - **Ativar o modo de stealth**

    - **Não configurado** *(predefinido)*
    - **Sim** - Evite que o computador responda a pedidos de sondagem. O computador continua a responder a pedidos recebidos de aplicações autorizadas.

  - **Aplicativos firewall** Expandir a queda e, em seguida, selecionar **Adicionar** para especificar aplicações e regras para ligações de entrada para a app.
    - **Permitir ligações de entrada**
      - Não configurado
      - Bloquear
      - Permitir

    - **Id do pacote** - O ID identifica a aplicação. Por exemplo: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Perfil de Firewall Do Microsoft Defender

### <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall

As seguintes definições são configuradas como a política de [segurança do ponto final para firewalls do Windows 10](../protect/endpoint-security-firewall-policy.md).

- **Desativar o protocolo de transferência de ficheiros (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Não configurado** *(predefinido*) - A firewall utiliza FTP para inspecionar e filtrar ligações de rede secundárias, o que pode fazer com que as suas regras de firewall sejam ignoradas.
  - **Sim**
  
- **Número de segundos uma associação de segurança pode ficar inativa antes de ser eliminada**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Especifique um tempo em segundos entre 300 e 3600, durante quanto tempo as associações de segurança são mantidas após o tráfego da rede não ser visto.
  
  Se não especificar qualquer valor, o sistema elimina uma associação de segurança depois de estar inativo durante 300 segundos.
  
- **Codificação de chaves pré-partilhadas**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Se não necessitar de *UTF-8,* as teclas pré-partilhadas são inicialmente codificadas utilizando o UTF-8. Depois disso, os utilizadores do dispositivo podem escolher outro método de codificação.

  - **Não configurado** *(predefinido)*
  - **Nenhum**
  - **UTF8**

- **Isenções ip sec firewall permitem descoberta de vizinhos**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Não configurado** *(predefinido)*
  - **Sim** - As isenções do Firewall IPsec permitem a descoberta do vizinho.

- **Isenções ip sec firewall permitem ICMP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Não configurado** *(predefinido)*
  - **Sim** - As isenções Do Firewall IPsec permitem o ICMP.

- **Isenções IP sec firewall permitem a descoberta do router**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Não configurado** *(predefinido)*
  - **Sim** - As isenções do Firewall IPsec permitem a descoberta do router.

- **Isenções ip sec firewall permitem DHCP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Não configurado** *(predefinido)*
  - **Sim** - Isenções ip sec firewall permitem DHCP

- **Verificação da lista de revogação do certificado (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Especifique como a verificação da lista de revogação do certificado (CRL) é executada.
  - **Não configurado** *(predefinido)*- O padrão do cliente é desativar a verificação de CRL.
  - **Nenhum**
  - **Tentativa**
  - **Requerer**

- **Exija mandamentos de teclas para apenas ignorar as suites de autenticação que não suportam**  
  CSP: [MdmStore/Global/OportunistaMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Não configurado** *(predefinido)*
  - **Sim** - Os módulos de chave ignoram as suites de autenticação não suportadas.

- **Fila de pacotes**  
  CSP: [Mdmstore/Global/EnablePacketqueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Especifique como permitir a escala para o software do lado de receção para a receção encriptada e limpar o texto para a frente para o cenário de gateway do túnel IPsec. Isto garante que a encomenda do pacote é preservada.
  - **Não configurado** *(predefinido)*- A fila de pacotes será devolvida ao padrão do cliente, que está desativada.
  - **Desativado**
  - **Fila Entrada**
  - **Fila saída**
  - **Fila Ambos**

- **Ligue o Microsoft Defender Firewall para redes de domínio**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Não configurado** *(predefinido*) - O cliente retorna ao padrão, que é ativar a firewall.
  - **Sim** - O Microsoft Defender Firewall para o tipo de **domínio** de rede é ligado e aplicado.
  - **Não** - Desativar a firewall.

- **Ligue o Microsoft Defender Firewall para redes privadas**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Não configurado** *(predefinido*) - O cliente retorna ao padrão, que é ativar a firewall.
  - **Sim** - O Microsoft Defender Firewall para o tipo **de** rede privado é ligado e aplicado.
  - **Não** - Desativar a firewall.

- **Ligue o Microsoft Defender Firewall para redes públicas**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Não configurado** *(predefinido*) - O cliente retorna ao padrão, que é ativar a firewall.
  - **Sim** - O Microsoft Defender Firewall para o tipo de rede de **público** é ligado e aplicado.
  - **Não** - Desativar a firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Regras do Microsoft Defender Firewall

*Este perfil está em Pré-visualização*.

As seguintes definições são configuradas como a política de [segurança do ponto final para firewalls do Windows 10](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Regra da firewall do Windows

- **Nome**  
  Especifique um nome amigável para a sua regra. Este nome aparecerá na lista de regras para ajudá-lo a identificá-lo.

- **Descrição**  
  Forneça uma descrição da regra.

- **Direção**  
  - **Não configurado** *(predefinido)*- Esta regra não se aplica ao tráfego de saída.
  - **out** - Esta regra aplica-se ao tráfego de saída.
  - **In** - Esta regra aplica-se ao tráfego de entrada.

- **Ação**  
  - **Não configurado** *(predefinido*) - A regra não se aplica para permitir o tráfego.
  - **Bloqueado** - O tráfego está bloqueado na *direção* que configura.
  - **Permitido** - O tráfego é permitido na *direção* que configura.

- **Tipo de rede**  
  Especifique o tipo de rede a que a regra pertence. Pode escolher um ou mais dos seguintes. Se não selecionar uma opção, a regra aplica-se a todos os tipos de rede.
  - **Domínio**
  - **Privado**
  - **Público**
  - **Não configurado**

- **Nome de família pacote**  
  [Pacote Get-Appx](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Os nomes de família dos pacotes podem ser recuperados executando o comando Get-AppxPackage da PowerShell.

- **Caminho do ficheiro**  
  CSP: [FirewallRules/FirewallRuleName/App/Filepath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Para especificar o caminho de ficheiro de uma aplicação, insira a localização das aplicações no dispositivo cliente. Por exemplo: `C:\Windows\System\Notepad.exe` ou`%WINDIR%\Notepad.exe`

- **Nome de serviço**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Utilize um nome curto do serviço Windows quando um serviço, não uma aplicação, está a enviar ou a receber tráfego. Os nomes curtos de serviço são recuperados executando o `Get-Service` comando da PowerShell.

- **Protocolo**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Especifique o protocolo para esta regra da porta.
  - Protocolos de camadas de transporte como *TCP(6)* e *UDP(17)* permitem especificar portas ou portas.
  - Para protocolos personalizados, insira um número entre *0* e *255* que represente o protocolo IP.
  - Quando nada é especificado, a regra não se aplica a **Qualquer**.

- **Tipos de interface**  
  Especifique os tipos de interface a que a regra pertence. Pode escolher um ou mais dos seguintes. Se não selecionar uma opção, a regra aplica-se a todos os tipos de interface:
  - **Acesso remoto**
  - **Sem fios**
  - **Rede local**
  - **Não configurado**

- **Utilizadores autorizados**  
  [FirewallRules/FirewallRuleName/Lista de Autorizações de Utilizadores Locais](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Especifique uma lista de utilizadores locais autorizados para esta regra. Não é possível especificar uma lista de utilizadores autorizados se o *nome do Serviço* nesta política for definido como um serviço Windows. Se nenhum utilizador autorizado for especificado, a predefinição é *de todos os utilizadores*.

- **Qualquer endereço local**  
  **Não configurado** *(predefinido*) - Utilize a seguinte definição, *gamas de endereços locais** para configurar uma gama de endereços para suportar.
  - **Sim** - Apoie qualquer endereço local e não configure um intervalo de endereços.

- **Intervalos de endereços locais**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Adicione um ou mais endereços como uma lista separada de vírinas de endereços locais que estão abrangidos pela regra. As entradas válidas (fichas) incluem as seguintes opções:
  - **Um asterisco** - Um asterisco ( \* ) indica qualquer endereço local. Se presente, o asterisco deve ser o único símbolo incluído.
  - **Uma sub-rede** - Especifique as sub-redes utilizando a máscara de sub-rede ou a notação prefixo da rede. Se não for especificada uma máscara de sub-rede ou prefixo de rede, a máscara de sub-rede desliga-se a 255.255.255.255.
  - **Um endereço IPv6 válido**
  - Uma gama de **endereços IPv4** - as gamas IPv4 devem estar no formato de endereço inicial *- endereço final* sem espaços incluídos, onde o endereço de início é inferior ao endereço final.
  - Uma gama de **endereços IPv6** - as gamas IPv6 devem estar no formato de endereço inicial *- endereço final* sem espaços incluídos, onde o endereço de início é inferior ao endereço final.

  Quando não é especificado qualquer valor, esta definição predefinido para utilizar *Qualquer endereço*.

- **Qualquer endereço remoto**  
  **Não configurado** *(predefinido*) - Utilize a seguinte definição, intervalos de *endereçoremotos** para configurar uma gama de endereços para suportar.
  - **Sim** - Apoie qualquer endereço remoto e não configure um intervalo de endereços.

- **Intervalos de endereços remotos**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Adicione um ou mais endereços como uma lista separada da vírgia de endereços remotos que estão abrangidos pela regra. As entradas válidas (fichas) incluem o seguinte e não são sensíveis aos casos:
  - **Um asterisco** - Um asterisco ( \* ) indica qualquer endereço remoto. Se presente, o asterisco deve ser o único símbolo incluído.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - Suportado em dispositivos que executam o Windows 1809 ou mais tarde.
  - **RmtIntranet** - Suportado em dispositivos que executam o Windows 1809 ou mais tarde.
  - **Ply2Renders** - Suportado em dispositivos que executam o Windows 1809 ou mais tarde.
  - **LocalSubnet** - Indica qualquer endereço local na subnet local.
  - **Uma sub-rede** - Especifique as sub-redes utilizando a máscara de sub-rede ou a notação prefixo da rede. Se não for especificada uma máscara de sub-rede ou um prefixo de rede, a máscara de sub-rede desliga-se a 255.255.255.255.
  - **Um endereço IPv6 válido**
  - Uma gama de **endereços IPv4** - as gamas IPv4 devem estar no formato de endereço inicial *- endereço final* sem espaços incluídos, onde o endereço de início é inferior ao endereço final.
  - Uma gama de **endereços IPv6** - as gamas IPv6 devem estar no formato de endereço inicial *- endereço final* sem espaços incluídos, onde o endereço de início é inferior ao endereço final.

  Quando não é especificado qualquer valor, esta definição predefinido para utilizar *Qualquer endereço*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Próximos passos

[Política de segurança do ponto final para firewalls](../protect/endpoint-security-firewall-policy.md)
