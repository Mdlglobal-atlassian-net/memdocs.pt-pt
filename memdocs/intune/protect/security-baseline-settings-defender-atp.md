---
title: Definições de base de segurança insinadas para proteção de ameaças avançadas do Microsoft Defender
titleSuffix: Microsoft Intune
description: Definições de base de segurança suportadas pela Intune para gerir a Proteção avançada de ameaças do Microsoft Defender
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: e1081395c733807c38dc940ebd1b7c2765da7a9a
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693402"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Microsoft Defender Definições de base de proteção de ameaças avançadas para Intune

Ver as definições de base de proteção de ameaças avançadas do Microsoft Defender que são suportadas pela Microsoft Intune. As predefinições de base de proteção de ameaças avançadas (ATP) representam a configuração recomendada para ATP, e podem não corresponder às predefinições de base para outras linhas de segurança.

::: zone pivot="atp-april-2020"

Os detalhes deste artigo aplicam-se à versão 4 da linha de base ATP do Microsoft Defender, que foi lançada a 21 de abril de 2020. Para entender o que mudou com esta versão da linha de base de versões anteriores, use a ação [compare baselines](../protect/security-baselines.md#compare-baseline-versions) que está disponível ao visualizar o painel *veras versões* para esta linha de base.

::: zone-end
::: zone pivot="atp-march-2020"

Os detalhes deste artigo aplicam-se à versão 3 da linha de base ATP do Microsoft Defender, que foi lançada a 1 de março de 2020. Para entender o que mudou com esta versão da linha de base de versões anteriores, use a ação [compare baselines](../protect/security-baselines.md#compare-baseline-versions) que está disponível ao visualizar o painel *veras versões* para esta linha de base.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


A linha de base de proteção contra ameaças avançada do Microsoft Defender está disponível quando o seu ambiente satisfaz os pré-requisitos para a utilização de [proteção de ameaças avançadas do Microsoft Defender](advanced-threat-protection.md#prerequisites).

Esta linha de base está otimizada para dispositivos físicos e não é atualmente recomendada para utilização em máquinas virtuais (VMs) ou pontos finais VDI. Certas definições de base podem ter impacto em sessões interativas remotas em ambientes virtualizados. Para mais informações, consulte Aumentar a conformidade com a linha de [segurança ATP do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) na documentação do Windows.


## <a name="application-guard"></a>Guarda de Aplicações

Para mais informações, consulte o [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) na documentação do Windows.  

Ao utilizar o Microsoft Edge, o Microsoft Defender Application Guard protege o seu ambiente de sites que não são confiáveis pela sua organização. Quando os utilizadores visitam sites que não estão listados no limite da rede isolada, os sites abrem-se numa sessão de navegação virtual Hyper-V. Os sites fidedignos são definidos por um limite de rede.  

- **Ligue a Guarda de Aplicação para Edge (Opções)**  
  CSP: [Definições/Permitirguarda de AplicaçõesdoWindowsDefender](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Ativado para Edge** *(predefinido)*- O Protetor de Aplicações abre sites não aprovados num recipiente de navegação virtualizado Hyper-V.
  - **Não configurado** - Qualquer site (confiável e não confiável) abre no dispositivo e não num recipiente virtualizado.  
  
  Quando definido para *ativar o Edge,* pode configurar *o bloquear conteúdos externos a partir de sites não aprovados pela empresa* e comportamento de *clipboard*.

  - **Bloquear conteúdo externo de sites não aprovados pela empresa**  
    CSP: [Definições/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Sim** *(padrão)*- Bloqueie o conteúdo de sites não aprovados a partir do carregamento.
    - **Não configurado** - Sites não empresariais podem abrir no dispositivo

  - **Comportamento de clipboard**  
    CSP: [Definições/Definições de clipboard](https://go.microsoft.com/fwlink/?linkid=872351)

    Escolha quais as ações de cópia e pasta que são permitidas entre o PC local e o navegador virtual Application Guard. As opções incluem:
    - **Não configurado**  
    - **Cópia do bloco e pasta entre PC e browser** *(predefinido*) - Bloqueie ambos. Os dados não podem ser transferidos entre o PC e o navegador virtual.
    - **Permitir copiar e colar do navegador apenas para PC** - Os dados não podem ser transferidos do PC para o navegador virtual.
    - **Permitir copiar e colar do PC para o navegador apenas** - Os dados não podem ser transferidos do navegador virtual para o PC anfitrião.
    - **Permitir copiar e colar entre PC e browser** - Não existe nenhum bloco para conteúdos.

- **Política de isolamento de rede Windows**  
  CSP: [Política CSP - Networkisolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Especifique uma lista de domínios de *Rede,* que são recursos da Enterprise que estão hospedados na nuvem que a Application Guard trata como sites empresariais
  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *configurar* pode então definir *domínios*de rede .

  - **Domínios de rede**  
    Selecione **Adicionar** e especificar domínios, intervalos de endereços IP e limites de rede. Por padrão, *securitycenter.windows.com* está configurado.

## <a name="bitlocker"></a>BitLocker

Para mais informações, as definições da [Política do Grupo BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) na documentação do Windows.

- **Exigir que os cartões de armazenamento sejam encriptados (apenas para dispositivos móveis)**  
  CSP: [RequirerStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Esta definição aplica-se apenas aos dispositivos Windows Mobile e Mobile Enterprise SKU.
  - **Sim** *(padrão)*- A encriptação nos cartões de armazenamento é necessária para dispositivos móveis.
  - **Não configurado** - A definição retorna ao padrão DE SO, que não é para exigir encriptação do cartão de armazenamento.

- **Ativar encriptação completa do disco para OS e unidades de dados fixas**  
  CSP: [RequirerDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Se a unidade foi encriptada antes desta política aplicada, não são tomadas medidas adicionais. Se o método de encriptação e as opções corresponderem ao desta política, a configuração deve devolver o sucesso. Se uma opção de configuração BitLocker em vigor não corresponder a esta política, a configuração provavelmente devolverá um erro.
  
  Para aplicar esta política a um disco já encriptado, desencriptar a unidade e reaplicar a política de MDM. O predefinido do Windows não é necessário para não exigir encriptação de unidade BitLocker, no entanto, no Azure AD Join e microsoft Account (MSA) a encriptação automática de login pode aplicar-se permitindo o BitLocker na encriptação xTS-AES de 128 bits.

  - **Sim** *(padrão)*- Impor a utilização do BitLocker.
  - **Não configurado** - Não ocorre nenhuma aplicação bitLocker.

- **Política de condução do sistema BitLocker**  
  [Definições de Política de Grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *configurar,* pode configurar o método de *encriptação configure para unidades do Sistema Operativo*.

  - **Configurar o método de encriptação para unidades do Sistema Operativo**  
    CSP: [EncriptaçãoMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta definição está disponível quando a política de *acionamento do sistema BitLocker* está definida para *configurar*.  

    Configure o método de encriptação e a força da cifra para as unidades do sistema.  *XTS- AES 128-bit* é o método de encriptação padrão do Windows e o valor recomendado.

    - **Não configurado** *(predefinido)*
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **Política de unidade fixa BitLocker**  
  [Definições de Política de Grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *Configurar,* pode configurar o acesso de *escrita do Bloco a unidades de dados fixas não protegidas pelo método de* encriptação BitLocker e *Configure para unidades de dados fixas*.

  - **Bloquear o acesso a unidades de dados fixas não protegidas pelo BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Esta definição está disponível quando a política de *unidade fixa BitLocker* está definida para *configurar*.

    - **Não configurados** *(predefinido*) - Os dados podem ser escritos em unidades fixas não encriptadas.
    - **Sim** - O Windows não permitirá que quaisquer dados sejam escritos a unidades fixas que não estejam protegidas pelo BitLocker. Se uma unidade fixa não for encriptada, o utilizador terá de completar o assistente de configuração BitLocker para a unidade antes de ser concedido o acesso à escrita.

  - **Configurar o método de encriptação para unidades de dados fixas**  
    CSP: [EncriptaçãoMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta definição está disponível quando a política de *unidade fixa BitLocker* está definida para *configurar*.

    Configure o método de encriptação e a força da cifra para discos de discos de discos fixos de unidades de dados. *XTS- AES 128-bit* é o método de encriptação padrão do Windows e o valor recomendado.

    - **Não configurado** *(predefinido)*
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **Política de unidade amovível BitLocker**  
  [Definições de Política de Grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *Configurar,* pode configurar o método de *encriptação Configure para unidades de dados amovíveis* e *bloquear o acesso a unidades de dados amovíveis não protegidas pelo BitLocker*.

  - **Configurar o método de encriptação para unidades de dados amovíveis**  
    CSP: [EncriptaçãoMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta definição está disponível quando a política de *unidade amovível BitLocker* está definida para *configurar*.

    Configure o método de encriptação e a força da cifra para discos de unidades de dados amovíveis. *XTS- AES 128-bit* é o método de encriptação padrão do Windows e o valor recomendado.

    - **Não configurado**
    - **AES 128bit CBC**
    - **AES 256bit CBC** *(padrão)*
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Block write acesso a unidades de dados amovíveis não protegidos pelo BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Esta definição está disponível quando a política de *unidade amovível BitLocker* está definida para *configurar*.

    - **Não configurados** *(predefinido*) - Os dados podem ser escritos para unidades amovíveis não encriptadas.  
    - **Sim** - O Windows não permitirá que quaisquer dados sejam escritos para unidades amovíveis que não estejam protegidas pelo BitLocker. Se uma unidade amovível não estiver encriptada, o utilizador deve completar o assistente de configuração BitLocker para a unidade antes de ser concedido o acesso à escrita.

## <a name="browser"></a>Browser

- **Requerer smartScreen para microsoft edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sim** *(padrão)*- Utilize o SmartScreen para proteger os utilizadores de potenciais esquemas de phishing e software malicioso.
  - **Não configurado**

- **Bloqueie o acesso malicioso ao site**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sim** *(predefinido*) - Bloqueie os utilizadores de ignorar os avisos do Filtro SmartScreen do Microsoft Defender e impedi-los de ir para o site.
  - **Não configurado**

- **Bloquear o download de ficheiros não verificados**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sim** *(padrão*) - Bloqueie os utilizadores de ignorar os avisos do Filtro SmartScreen do Microsoft Defender e bloqueá-los de descarregar ficheiros não verificados.
  - **Não configurado**

## <a name="data-protection"></a>Proteção de Dados

- **Bloquear o acesso à memória direta**  
  CSP: Proteção de [Dados/PermitirAcesso de Memória Direta](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Esta definição de política só é aplicada quando o BitLocker ou a encriptação do dispositivo estiverem ativadas.

  - **Sim** *(predefinido*) - Bloqueie o acesso à memória direta (DMA) para todas as portas a jusante do PCI pluggable a quente até que um utilizador inicie sessão no Windows. Depois de um utilizador iniciar sessão, o Windows enumera os dispositivos PCI ligados às portas PCI plug do hospedeiro. Sempre que o utilizador bloqueia a máquina, o DMA é bloqueado em portas PCI de ficha quente sem dispositivos para crianças até que o utilizador volte a entrar. Os dispositivos que já estavam enumerados quando a máquina foi desbloqueada continuarão a funcionar até desligarem a tomada.
  - **Não configurado**

## <a name="device-guard"></a>Guarda de Dispositivos  

- **Ligue a guarda credencial**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  A Credential Guard utiliza o Windows Hypervisor para fornecer proteções, o que requer proteções Secure Boot e DMA para funcionar, o que requer que os requisitos de hardware sejam cumpridos.

  - **Não configurado** - Desative a utilização da Guarda Credencial, que é a falha do Windows.
  - **Ativar com o bloqueio UEFI** *(predefinido)*- Ativar a Guarda Credencial e não permitir que seja desativada remotamente, uma vez que a configuração do UEFI deve ser manualmente desobstruída.
  - **Ativar sem bloqueio UEFI** - Ativar a Guarda Credencial e permitir que seja desligada sem acesso físico à máquina.

## <a name="device-installation"></a>Instalação de Dispositivos

- **Instalação de dispositivos de hardware por identificadores de dispositivos**  
  [Instalação/Prevenção de Instalações de Dispositivos DeCorrespondênciaIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Esta definição de política permite especificar uma lista de IDs de hardware plug e play e IDs compatíveis para dispositivos que o Windows está impedido de instalar. Esta definição de política tem precedência sobre qualquer outra definição de política que permita ao Windows instalar um dispositivo.  Se ativar esta definição de política num servidor de ambiente de trabalho remoto, a definição de política afeta a reorientação dos dispositivos especificados de um cliente de ambiente de trabalho remoto para o servidor de ambiente de trabalho remoto.

  - **Não configurado**
  - Permitir a instalação de dispositivos de **hardware** - Os dispositivos podem ser instalados e atualizados conforme permitido ou impedido por outras definições de política.
  - Bloquear a **instalação** do dispositivo de hardware *(predefinido)*- O Windows está impedido de instalar um dispositivo cujo ID de hardware ou ID compatível aparece numa lista que define.

  Quando definido para bloquear a instalação do dispositivo de *hardware,* pode configurar Remover dispositivos de *hardware correspondentes* e identificadores de dispositivos de *hardware que estão bloqueados*.

  - **Remover dispositivos de hardware correspondentes**

    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*.
    - **Sim**
    - **Não configurado**

  - **Identificadores de dispositivos de hardware que estão bloqueados**  
    
    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*.

    Selecione **Adicionar**, e, em seguida, especificar o identificador de dispositivo de hardware que pretende bloquear.

- **Instalação de dispositivos de hardware por classes de configuração**  
  CSP: [Instalação/instalação de dispositivosOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Esta definição de política permite especificar uma lista de identificadores de configuração de dispositivos globalmente únicos (GUIDs) para os controladores de dispositivos que o Windows está impedido de instalar. Esta definição de política tem precedência sobre qualquer outra definição de política que permita ao Windows instalar um dispositivo. Se ativar esta definição de política num servidor de ambiente de trabalho remoto, a definição de política afeta a reorientação dos dispositivos especificados de um cliente de ambiente de trabalho remoto para o servidor de ambiente de trabalho remoto.

  - **Não configurado**
  - **Permitir a instalação** de dispositivos de hardware - O Windows pode instalar e atualizar dispositivos conforme permitido ou impedido por outras definições de política.
  - Bloquear a instalação do dispositivo de **hardware** *(predefinido*) - O Windows está impedido de instalar um dispositivo cuja classe DE CONFIGURAÇÃO GUIDs aparece numa lista que define.

  Quando definido para bloquear a instalação do dispositivo de *hardware,* pode configurar Remover dispositivos de *hardware correspondentes* e identificadores de dispositivos de *hardware que estão bloqueados*.

  - **Remover dispositivos de hardware correspondentes**

    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*.
    - **Sim**
    - **Não configurado**

  - **Identificadores de dispositivos de hardware que estão bloqueados**

    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*.

    Selecione **Adicionar**, e, em seguida, especificar o identificador de dispositivo de hardware que pretende bloquear.

## <a name="dma-guard"></a>Guarda DMA

- **Enumeração de dispositivos externos incompatíveis com a Proteção Kernel DMA**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Esta política pode fornecer segurança adicional contra dispositivos externos capazes de DMA. Permite um maior controlo sobre a enumeração de dispositivos externos capazes de DMA incompatíveis com o isolamento da memória de DMA/dispositivo e o sandboxing.
  
  Esta política só entra em vigor quando a Kernel DMA Protection é suportada e ativada pelo firmware do sistema. Kernel DMA Protection é uma funcionalidade de plataforma que deve ser suportada pelo sistema no momento da fabricação. Para verificar se o sistema suporta a Proteção Kernel DMA, verifique o campo de proteção Kernel DMA na página sumária de MSINFO32.exe.

  - **Não configurado** -*(padrão)*
  - **Bloqueie tudo**
  - **Permitir que todos**

## <a name="endpoint-detection-and-response"></a>Deteção e Resposta de Ponto Final

Para obter mais informações sobre as seguintes definições, consulte o [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP na documentação do Windows.

- **Partilha de amostras para todos os ficheiros**  
  CSP: [Configuração/Partilha de Amostras](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Devoluções ou configurações do parâmetro de partilha de amostras de proteção de ameaças avançada do Microsoft Defender.  
  
  - **Sim** *(padrão)*
  - **Não configurado**

- **Frequência de relatório de telemetria expedita**  
  CSP: [Configuração/TelemettryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Acelere a frequência de relatório de telemetria avançada de telemetria do Microsoft Defender.  

  - **Sim** *(padrão)*
  - **Não configurado**

## <a name="firewall"></a>Firewall

Para mais informações, consulte o [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) na documentação do Windows.

- **Desativar o protocolo de transferência de ficheiros (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Sim** *(padrão)*
  - **Não configurado** - A firewall utilizará FTP para inspecionar e filtrar ligações de rede secundárias, o que pode fazer com que as suas regras de firewall sejam ignoradas.

- **Número de segundos uma associação de segurança pode ficar inativa antes de ser eliminada**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Especifique quanto tempo as associações de segurança são mantidas após o tráfego da rede deixar de ser visto. Quando não está configurado, o sistema elimina uma associação de segurança depois de estar inativo durante *300* segundos (a predefinição).
  
  O número deve ser de **300** a **3600** segundos.

- **Codificação de chaves pré-partilhadas**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Se não necessitar de UTF-8, as teclas pré-partilhadas serão inicialmente codificadas utilizando o UTF-8. Depois disso, os utilizadores do dispositivo podem escolher outro método de codificação.

  - **Não configurado**
  - **Nenhum**
  - **UTF8** *(padrão)*

- **Verificação da lista de revogação do certificado (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Especifique como a verificação da lista de revogação do certificado (CRL) é executada.  

  - **Não configurado** *(predefinido)*- A verificação de CRL é desativada.
  - **Nenhum**
  - **Tentativa**
  - **Requerer**

- **Fila de pacotes**  
  CSP: [Mdmstore/Global/EnablePacketqueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Especifique como a escala para o software no lado de receção está ativada para a receção encriptada e texto claro para a frente para o cenário de gateway do túnel IPsec. Esta definição garante que a encomenda do pacote seja preservada.

  - **Não configurado** *(predefinido)*- O pacote de filas devolve ao padrão do cliente, que está desativado.
  - **Desativado**
  - **Fila Entrada**
  - **Fila saída**
  - **Fila Ambos**

- **Perfil de firewall privado**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *configurar,* pode configurar as seguintes definições adicionais.

  - **Ligações de entrada bloqueadas**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Respostas unicast às emissões multicast necessárias**  
    CSP: [/DisableUnicastResponsesTo MulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Modo furtivo necessário**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Ligações de saída necessárias**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Notificações de entrada bloqueadas**  
    CSP: [/Desativar Notificações](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras portuárias globais da política do grupo fundidas**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Modo furtivo bloqueado**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Firewall ativado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Não configurado**
    - **Bloqueado**
    - **Permitido** *(padrão)*

  - **Regras de aplicação autorizadas da política do grupo não fundidas**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Tráfego de entrada necessário**  
    CSP: [/Blindado](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras políticas da política de grupo não fundidas**  
    CSP: [/Permitir fusão política local](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sim** *(padrão)*
    - **Não configurado**

- **Público de perfil firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Configurar** *(padrão)*
  - **Não configurado**

  Quando definido para *configurar,* pode configurar as seguintes definições adicionais.

  - **Ligações de entrada bloqueadas**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Respostas unicast às emissões multicast necessárias**  
    CSP: [/DisableUnicastResponsesTo MulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Modo furtivo necessário**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Ligações de saída necessárias**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras de aplicação autorizadas da política do grupo não fundidas**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Notificações de entrada bloqueadas**  
    CSP: [/Desativar Notificações](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras portuárias globais da política do grupo fundidas**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Modo furtivo bloqueado**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Firewall ativado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Não configurado**
    - **Bloqueado**
    - **Permitido** *(padrão)*

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Tráfego de entrada necessário**  
    CSP: [/Blindado](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras políticas da política de grupo não fundidas**  
    CSP: [/Permitir fusão política local](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sim** *(padrão)*
    - **Não configurado**

- **Domínio de perfil de firewall**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Respostas unicast às emissões multicast necessárias**  
    CSP: [/DisableUnicastResponsesTo MulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Regras de aplicação autorizadas da política do grupo não fundidas**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sim** *(padrão)*
    - **Não configurado**  

  - **Notificações de entrada bloqueadas**  
    CSP: [/Desativar Notificações](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras portuárias globais da política do grupo fundidas**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Modo furtivo bloqueado**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Firewall ativado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Não configurado**
    - **Bloqueado**
    - **Permitido** *(padrão)*

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sim** *(padrão)*
    - **Não configurado**

  - **Regras políticas da política de grupo não fundidas**  
    CSP: [/Permitir fusão política local](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sim** *(padrão)*
    - **Não configurado**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Executar varredura rápida diária em**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Configure quando a varredura rápida diária for executado. Por defeito, a execução da varredura está definida para **2 AM**.

- **Hora de início da varredura agendada**  
  
  Por defeito, isto está definido para **2 AM**.

- **Configure baixa prioridade da CPU para digitalizações programadas**  
  CSP: [Defender/EnablelowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Sim** *(padrão)*
  - **Não configurado**

- **Block Office apps de comunicação de criação de processos infantis**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874499)  

  Esta regra ASR é controlada através do seguinte GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Não configurado** - O predefinido do Windows é restaurado, é para não bloquear a criação de processos infantis.
  - **Utilizador definido**
  - **Ativar** (*padrão*) - As aplicações de comunicação do escritório estão bloqueadas de criar processos infantis.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear processos infantis.

- **Block Adobe Reader de criar processos infantis**  
  [Reduzir superfícies de ataque com regras de redução da superfície de ataque](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Não configurado** - O predefinido do Windows é restaurado, é para não bloquear a criação de processos infantis.
  - **Utilizador definido**
  - **Ativar** *(predefinido*) - O Adobe Reader está impedido de criar processos infantis.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear processos infantis.

- **Digitalizar mensagens de e-mail de entrada**  
  CSP: [Defender/PermitirEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Sim** *(predefinido)*- Caixas de correio eletrónico e ficheiros de correio eletrónico como PST, DBX, MNX, MIME e BINHEX são digitalizados.
  - **Não configurado** - A definição retorna ao padrão do cliente de ficheiros de e-mail não sendo digitalizados.

- **Ativar a proteção em tempo real**  
  CSP: [Monitorização de Tempo Real/Defensor](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Sim** (*predefinido)*- A monitorização em tempo real é executada e o utilizador não pode desativá-lo.
  - **Não configurado** - A definição é devolvida ao padrão do cliente, que está ligado, mas o utilizador pode troco.pode mudá-la. Para desativar a monitorização em tempo real, utilize um URI personalizado.

- **Número de dias (0-90) para manter malware em quarentena**  
  CSP: [Defender/DaysToReterMalware Limpo](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Configure o número de dias que os itens devem ser mantidos na pasta de quarentena antes de serem removidos. O padrão é zero (**0),** o que resulta em ficheiros em quarentena nunca removidos.

- **Calendário de scan do sistema de defesa**  
  CSP: [Defender/AgendasScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Agenda risa da data Que o Defender digitaliza os dispositivos. Por predefinição, a digitalização é definida pelo **Utilizador,** mas pode ser definida para *o Everyday*, qualquer dia da semana, ou para não ter *uma varredura programada*.

- **Quantidade adicional de tempo (0-50 segundos) para prolongar o tempo de proteção da nuvem**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  O Antivírus Defensor bloqueia automaticamente ficheiros suspeitos durante 10 segundos para que possa digitalizar os ficheiros na nuvem para se certificar de que estão seguros. Com esta definição, pode adicionar até 50 segundos adicionais a este intervalo.  Por predefinição, o tempo de paragem é definido para zero (**0**).

- **Scan mapeado unidades de rede durante uma varredura completa**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Sim** *(padrão)*- Durante uma varredura completa, as unidades de rede mapeadas estão incluídas.
  - **Não configurado** - O cliente regressa ao seu padrão, que desativa a digitalização em unidades de rede mapeadas.

- **Ativar a proteção da rede**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Sim** *(padrão)*- Bloqueie o tráfego malicioso detetado por assinaturas no Sistema de Inspeção de Rede (NIS).
  - **Não configurado**

- **Scaneie todos os ficheiros e anexos descarregados**  
  CSP: [Defender/AllowioAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Sim** *(predefinido)*- Todos os ficheiros e anexos descarregados são digitalizados. A definição é devolvida ao padrão do cliente, que está ligado, mas o utilizador pode troco. Para desativar esta definição, utilize um URI personalizado.
  - **Não configurado** - A definição é devolvida ao padrão do cliente, que está ligado, mas o utilizador pode troco.pode mudá-la. Para desativar esta definição, utilize um URI personalizado.

::: zone-end
::: zone pivot="atp-april-2020"

- **Bloquear a proteção de acesso**  
  CSP: [Proteção de Acessos defensor/permitir](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sim**
  - **Não configurado** *(predefinido)*

::: zone-end
::: zone pivot="atp-march-2020"

- **Bloquear a proteção de acesso**  
  CSP: [Proteção de Acessos defensor/permitir](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sim** *(padrão)*
  - **Não configurado**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Scan scripts de navegador**  
  CSP: [Defender/PermitirScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Sim** *(predefinido*) - A funcionalidade de digitalização do Script Microsoft Defender é executada e o utilizador não pode desligá-los.
  - **Não configurado** - A definição é devolvida ao padrão do cliente, que é para ativar a verificação do script, no entanto o utilizador pode desligá-lo.

- **Bloqueie o acesso dos utilizadores à aplicação Microsoft Defender**  
  CSP: [Defender/Permitir acesso userui](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Sim** *(padrão)*- A Interface de Utilizador do Microsoft Defender (UI) é inacessível e as notificações são surpreendidas
  - **Não configurado** Quando definido para Sim, a Interface de Utilizador do Windows Defender (UI) será inacessível e as notificações ficarão surpreendidas. Quando definido para Não configurado, a definição voltará ao padrão do cliente em que UI e notificações serão permitidas

- **Máximo permitido uso de CPU (0-100 por cento) por digitalização**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Especifique em percentagem o montante máximo de CPU para utilizar para uma varredura. O padrão é **de 50**.

- **Tipo de digitalização**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Utilizador definido**
  - **Desativado**
  - **Digitalização rápida** *(padrão)*
  - **Análise completa**

- **Insira quantas vezes (0-24 horas) para verificar se há atualizações de inteligência de segurança**  
  CSP: [Intervalo de atualização de defender/assinatura](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Especifique com que frequência verificar se há assinaturas atualizadas, em horas. Por exemplo, um valor de 1 verificará a cada hora. Um valor de 2 verificará a cada duas horas, e assim por diante.

  Se não for definido qualquer valor, os dispositivos utilizam o padrão do cliente de **8** horas.

- **Consentimento de submissão da amostra de defender**  
  CSP: [Defender/SubmeterSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Verifica o nível de consentimento do utilizador no Microsoft Defender para enviar dados. Se o consentimento exigido já tiver sido concedido, o Microsoft Defender submete-os. Caso contrário (e se o utilizador tiver especificado nunca pedir), a UI é lançada para pedir o consentimento do utilizador (quando a *proteção entregue pela Cloud* for definida para *Sim)* antes de enviar dados.

  - **Enviar amostras seguras automaticamente** *(predefinido)*
  - **Sempre rápido**
  - **Nunca enviar**
  - **Enviar todas as amostras automaticamente**

- **Nível de proteção entregue em nuvem**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Configure o quão agressivo o Antivírus defensor está em bloquear e digitalizar ficheiros suspeitos.
  - **Não configurado** *(predefinido*) - Padrão Defender blocking level.
  - **High** - Bloqueie agressivamente desconhecidos ao mesmo tempo que otimiza o desempenho do cliente, o que inclui uma maior chance de falsos positivos.
  - **High plus** - Bloqueie agressivamente as incógnitas e aplique medidas de proteção adicionais que possam ter impacto no desempenho do cliente.
  - **Tolerância zero** - Bloqueie todos os ficheiros executáveis desconhecidos.

- **Analisar ficheiros de arquivo**  
  CSP: [Defender/PermitirArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Sim** *(padrão)*- A digitalização de ficheiros de arquivo, tais como ficheiros ZIP ou CAB, é executada.
  - **Não configurado** - A definição será devolvida ao padrão do cliente, que é digitalizar ficheiros arquivados, no entanto o utilizador pode desativar a digitalização.

- **Ativar a monitorização do comportamento**  
  CSP: [Monitorização de Comportamento de Defesa/Permitir](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Sim** (*predefinido)*- A monitorização do comportamento é executada e o utilizador não pode desativá-lo.
  - **Não configurado** - A definição é devolvida ao padrão do cliente, que está ligado, mas o utilizador pode troco.pode mudá-la. Para desativar a monitorização em tempo real, utilize um URI personalizado.
  
- **Digitalizar unidades amovíveis durante a varredura completa**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Sim** *(predefinido*) - Durante uma varredura completa, as unidades amovíveis (como as pen USB) são digitalizadas.
  - **Não configurado** - A definição retorna ao padrão do cliente, que digitaliza unidades amovíveis, no entanto o utilizador pode desativar esta digitalização.
  
- **Scan ficheiros de rede**  
  CSP: [Defender/Permitirficheiros de Redes de Digitalização](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Sim** *(padrão)*- O Microsoft Defender digitaliza ficheiros de rede.
  - **Não configurado** - O cliente retorna ao seu padrão, o que desativa a digitalização de ficheiros de rede.
  
- **Defender ação de aplicação potencialmente indesejada**  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Especifique o nível de deteção de aplicações potencialmente indesejadas (APA). O Defender alerta os utilizadores quando o software potencialmente indesejado está a ser descarregado ou tenta instalar-se num dispositivo.
  - **Predefinição do dispositivo**
  - **Bloco** (*padrão*) - Os itens detetados estão bloqueados e mostram na história juntamente com outras ameaças.
  - **Auditoria** - Defender deteta aplicações potencialmente indesejadas, mas não toma medidas. Pode rever informações sobre as aplicações que o Defender teria tomado medidas contra a procura de eventos criados pela Defender no Observador de Eventos.

- **Ligue a proteção entregue em nuvem**  
  CSP: [Permitir proteção em nuvem](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Por padrão, o Defender nos dispositivos de desktop do Windows 10 envia informações à Microsoft sobre quaisquer problemas que encontre. A Microsoft analisa essa informação para saber mais sobre problemas que afetam o seu e outros clientes, para oferecer soluções melhoradas.

  - **Sim** (*padrão)*- A proteção entregue em nuvem é ligada.  Os utilizadores do dispositivo não podem alterar esta definição.
  - **Não configurado** - A definição é restaurada à defeito do sistema.

- **Bloqueio de pedidos de injeção de código em outros processos**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872974)

  Esta regra ASR é controlada através do seguinte GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** *(predefinido*) - As aplicações do escritório estão bloqueadas de injetar código noutros processos.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Aplicações do Block Office da criação de conteúdo executável**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872975)

  Esta regra ASR é controlada através do seguinte GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** *(predefinido*) - As aplicações do escritório estão bloqueadas de criar conteúdo executável.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.
  
- **Bloqueie o JavaScript ou o VBScript a partir do lançamento de conteúdo executável descarregado**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872979)

   Esta regra ASR é controlada através do seguinte GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** *(predefinido*) - O defender bloqueia ficheiros JavaScript ou VBScript que foram descarregados da Internet a partir da execução.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.
  
- **Ativar a proteção da rede**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Não configurado** - A definição volta à predefinição do Windows, que está desativada.
  - **Utilizador definido**
  - **Ativar** - A proteção da rede está ativada para todos os utilizadores do sistema.
  - **Modo** de auditoria *(predefinido)*- Os utilizadores não estão bloqueados de domínios perigosos e os eventos windows são levantados.

- **Bloqueie processos não confiáveis e não assinados que vão a partir de USB**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874502)

  Esta regra ASR é controlada através do seguinte GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloquear** *(predefinido*) - Processos não confiáveis e não assinados que funcionam a partir de uma unidade USB estão bloqueados.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Roubo de credenciais bloqueadas do subsistema da autoridade de segurança local do Windows (lsass.exe)**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874499)

  Esta regra ASR é controlada através do seguinte GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Utilizador definido**
  - **Ativar** (*padrão)*- As tentativas de roubar credenciais através de lsass.exe estão bloqueadas.
  - **Modo** de auditoria - Os utilizadores não estão bloqueados de domínios perigosos e os eventos windows são levantados.

- **Bloquear o download de conteúdo executável a partir de clientes de e-mail e webmail**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Block** *(predefinido*) - O conteúdo executável descarregado de e-mail e clientes de webmail está bloqueado.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloqueie todas as candidaturas do Office à criação de processos infantis**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872976)

  Esta regra ASR é controlada através do seguinte GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** *(predefinido)*
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Execução por blocos de scripts potencialmente obfuscados (js/vbs/ps)**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872978)

  Esta regra ASR é controlada através do seguinte GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** (*padrão*) - O Defensor bloqueará a execução de scripts obfuscados.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Block Win32 API liga da macro do Office**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872977)

  Esta regra ASR é controlada através do seguinte GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Não configurado** - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** *(padrão*) - Os macro's do office serão bloqueados de usar chamadas Win32 API.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

## <a name="microsoft-defender-security-center"></a>Centro de Segurança Microsoft Defender

- **Bloqueie os utilizadores de editar a interface de proteção Exploit Guard**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Sim** *(predefinido*) - Evite que os utilizadores epretem alterações na área de definições de proteção de exploração no Microsoft Defender Security Center.
  - **Não configurado** - Os utilizadores locais podem fazer alterações na área de definições de proteção de exploração.

## <a name="smart-screen"></a>Tela Inteligente

- **Bloqueie os utilizadores de ignorar os avisos do SmartScreen**  
  CSP: [SmartScreen/PreventoverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Esta definição requer a definição 'Impor o SmartScreen para aplicações e ficheiros'.
  - **Sim** (*predefinido)*- O SmartScreen não apresentará uma opção para o utilizador ignorar o aviso e executar a aplicação. O aviso será apresentado, mas o utilizador poderá contorná-lo.
  - **Não configurado** - Devolve a definição à predefinição do Windows, o que permite que o utilizador se sobressea.

- **Exigir aplicações apenas da loja**  

  - **Sim** *(padrão)*
  - **Não configurado**

- **Ligue o Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Sim** *(predefinido*) - Impor a utilização do SmartScreen para todos os utilizadores.
  - **Não configurado** - Devolva a definição para o predefinido do Windows, que é para ativar o SmartScreen, no entanto os utilizadores podem alterar esta definição. Para desativar o SmartScreen, utilize um URI personalizado.

## <a name="windows-hello-for-business"></a>Windows Hello para empresas

Para mais informações, consulte [o PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) na documentação do Windows.

- **Bloqueie janelas Olá para negócios**  

   O Windows Hello for Business é um método alternativo para iniciar sessão no Windows substituindo palavras-passe, Smart Cards e Cartões Inteligentes Virtuais.

  - **Não configurado** - Dispositivos de fornecimento de dispositivos Windows Hello for Business, que é o predefinido do Windows.
  - **Desativado** *(predefinido)*- Fornecimento de dispositivos Windows Hello for Business.
  - **Ativado** - Os dispositivos não disponibilizam o Windows Hello for Business para qualquer utilizador.

  Quando definido para *desativar,* pode configurar as seguintes definições:

  - **Letras em minúsculas no PIN**  
    - **Não permitido**
    - **Necessário**
    - **Permitido** *(padrão)*

  - **Carateres especiais no PIN**
    - **Não permitido**
    - **Necessário**
    - **Permitido** *(padrão)*

  - **Letras em maiúsculas no PIN**
    - **Não permitido**
    - **Necessário**
    - **Permitido** *(padrão)*

::: zone-end

## <a name="next-steps"></a>Passos seguintes

- [Conheça as linhas de base de segurança](security-baselines.md)
- [Evitar conflitos](security-baselines.md#avoid-conflicts)
- [Resolução de problemas de políticas e perfis no Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)