---
title: Definições de base de segurança insinadas para proteção de ameaças avançadas do Microsoft Defender
titleSuffix: Microsoft Intune
description: Definições de base de segurança suportadas pela Intune para gerir a Proteção avançada de ameaças do Microsoft Defender
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/05/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7ebea853ac536b182a9cfe35e8b291aea3a776f0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329053"
---
# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Microsoft Defender Definições de base de proteção de ameaças avançadas para Intune

Ver as definições de linha de base da Microsoft Defender Advanced Threat Protection (anteriormente Windows Defender Advanced Threat Protection) que são suportadas pela Microsoft Intune. As predefinições de base de proteção de ameaças avançadas (ATP) representam a configuração recomendada para ATP, e podem não corresponder às predefinições de base para outras linhas de segurança.  

A linha de base de proteção contra ameaças avançada do Microsoft Defender está disponível quando o seu ambiente satisfaz os pré-requisitos para a utilização de [proteção de ameaças avançadas do Microsoft Defender](advanced-threat-protection.md#prerequisites). 

Esta linha de base está otimizada para dispositivos físicos e não é atualmente recomendada para utilização em máquinas virtuais (VMs) ou pontos finais VDI. Certas definições de base podem ter impacto em sessões interativas remotas em ambientes virtualizados. Para mais informações, consulte Aumentar a conformidade com a linha de [segurança ATP do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) na documentação do Windows.

## <a name="application-guard"></a>Guarda de Aplicações  
Para mais informações, consulte o [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) na documentação do Windows.  

Ao utilizar o Microsoft Edge, o Microsoft Defender Application Guard protege o seu ambiente de sites que não são confiáveis pela sua organização. Quando os utilizadores visitam sites que não estão listados no limite da rede isolada, os sites abrem-se numa sessão de navegação virtual Hyper-V. Os sites fidedignos são definidos por um limite de rede.  

- **Guardião de aplicações** - *definições/AllowWindowsDefenderApplicationGuard*  
  Selecione *Sim* para ativar esta funcionalidade, que abre sites não confiáveis num recipiente de navegação virtualizado Hyper-V. Quando definido para *Não configurado,* qualquer site (confiável e não confiável) abre no dispositivo e não num recipiente virtualizado.  

  **Padrão**: Sim
 
  - **Conteúdo externo em sites empresariais** - *Definições/BlockNonEnterpriseContent*  
    Selecione *Sim* para bloquear conteúdo de websites não aprovados a partir de carregamento. Quando definido para *Não configurado,* os sites não empresariais podem abrir no dispositivo. 
 
    **Padrão**: Sim

  - **Comportamento de clipboard** - *Definições/Definições de clipboard*  
    Escolha quais as ações de cópia e pasta que são permitidas entre o PC local e o navegador virtual Application Guard.  As opções incluem:
    - Não Configurado  
    - Cópia do bloco e pasta entre PC e browser - Bloqueie ambos. Os dados não podem ser transferidos entre o PC e o navegador virtual.  
    - Permitir copiar e colar do navegador apenas para PC - Os dados não podem ser transferidos do PC para o navegador virtual.
    - Permitir copiar e colar do PC para o navegador apenas - Os dados não podem ser transferidos do navegador virtual para o PC anfitrião.
    - Permitir copiar e colar entre PC e browser - Não existe nenhum bloco para conteúdos.  

    **Predefinição**: Cópia do bloco e pasta entre PC e browser  

- **Política de isolamento de rede Windows – Nomes de domínio da rede Enterprise**  
  Para mais informações, consulte [Policy CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation) na documentação do Windows.
  
  Especifique uma lista de recursos da Enterprise como domínios, intervalos de endereços IP e limites de rede que estão alojados na nuvem que a Application Guard trata como sites empresariais.  

  **Predefinição**: securitycenter.windows.com

## <a name="application-reputation"></a>Reputação de aplicação  

Para mais informações, consulte [Policy CSP - SmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen) na documentação do Windows.

- **Bloquear a execução de ficheiros não verificados**  
    Bloqueie o utilizador de executar ficheiros não verificados. Quando definido para *não configurado,* os funcionários podem ignorar os avisos do SmartScreen e executar ficheiros maliciosos. Set to *Yes* para que os funcionários não possam ignorar os avisos do SmartScreen e executar ficheiros maliciosos.  
  
    **Padrão**: Sim

- **Requerer smartScreen para apps e ficheiros**  
  Configurar para *Sim* para ativar o SmartScreen para windows.  

  **Padrão**: Sim

## <a name="attack-surface-reduction"></a>Redução da Superfície de Ataque  

- **Aplicativos de escritório lançam tipo de processo infantil**  
  [Regra de redução da superfície](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) de ataque – Quando definido para *bloquear,* as aplicações do Office não serão autorizadas a criar processos infantis. As aplicações de escritório incluem Word, Excel, PowerPoint, OneNote e Access. A criação de um processo infantil é um comportamento típico de malware, especialmente para ataques macro-baseados que tentam usar aplicações do Office para lançar ou descarregar executáveis maliciosos.  

  **Predefinição**: Bloco

- **Script descarregado tipo de execução de carga útil**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – Especifique um nível de deteção para aplicações potencialmente indesejadas que descarreguem ou tentem instalar.  

  **Predefinição**: Bloco 

- **Prevenir o tipo de roubo de credenciais**  
  Configurado para *permitir* [proteger as credenciais de domínio derivadas com a Guarda Credencial](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard). A Microsoft Defender Credential Guard usa segurança baseada em virtualização para isolar segredos para que apenas o software privilegiado do sistema possa aceder aos mesmos. O acesso não autorizado a estes segredos pode levar a ataques de roubo de credenciais, como pass-the-Hash ou Pass-The-Ticket. A Microsoft Defender Credential Guard impede estes ataques protegendo as hashes de senha NTLM, os bilhetes de concessão de bilhetes Kerberos e credenciais armazenadas por aplicações como credenciais de domínio.  

  **Padrão**: Ativar

- **Execução de conteúdo de e-mail**  
  [Regra de redução da superfície](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) de ataque – Quando definido para *bloquear*, esta regra bloqueia que os seguintes tipos de ficheiros sejam executados ou lançados a partir de um e-mail visto no Microsoft Outlook ou no webmail (como Gmail.com ou Outlook.com):  

  - Ficheiros executáveis (tais como .exe, .dll ou .scr)  
  - Ficheiros script (tais como um ficheiro PowerShell .ps, VisualBasic .vbs ou JavaScript .js)  
  - Arquivo de script  

  **Predefinição**: Bloco

- **Adobe Reader lança-se num processo infantil**  
  Regra de [redução](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) da superfície de ataque – *Permita que* esta regra impeça o Adobe Reader de criar um processo infantil. Através de engenharia social ou explorações, o malware pode descarregar e lançar cargas adicionais e sair do Adobe Reader.  

  **Padrão**: Ativar

- **Script código macro obfuscado**  
  [Regra de redução da superfície](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) de ataque – Malware e outras ameaças podem tentar obstar ou esconder o seu código malicioso em alguns ficheiros de script. Esta regra impede que os scripts que parecem estar obfuscados de correr.  
    
  **Predefinição**: Bloco

- **Processo USB não confiável**  
  [Regra de redução](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) da superfície de ataque – Quando definido para *bloquear,* ficheiros executáveis não assinados ou não confiáveis de unidades amovíveis USB e cartões SD não podem ser executados.

  Os ficheiros executáveis incluem:
  - Ficheiros executáveis (tais como .exe, .dll ou .scr)
  - Ficheiros script (tais como um ficheiro PowerShell .ps, VisualBasic .vbs ou JavaScript .js)  

  **Predefinição**: Bloco

- **Aplicativos de escritório outra injeção de processo**  
  [Regra de redução](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) da superfície de ataque - Quando definido para *bloquear,* aplicações do Office, incluindo Word, Excel, PowerPoint e OneNote, não podem injetar código em outros processos. A injeção de código é normalmente usada por malware para executar código malicioso numa tentativa de ocultar a atividade dos motores de digitalização antivírus.  

  **Predefinição**: Bloco

- **O código macro do escritório permite importações win32**  
  [Regra de redução da superfície](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) de ataque - Quando definido para *bloquear*, esta regra tenta bloquear ficheiros do Office que contêm código macro que pode importar Win32 DLLs. Os ficheiros do escritório incluem Word, Excel, PowerPoint e OneNote. O malware pode usar o código macro nos ficheiros do Office para importar e carregar DLLs Win32, que são então usados para fazer chamadas API para permitir mais infeções em todo o sistema.  

  **Predefinição**: Bloco

- **Aplicativos de comunicação do escritório lançam-se num processo infantil**  
  [Regra de redução](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) da superfície de ataque – Quando definido para *ativar,* esta regra impede o Outlook de criar processos infantis. Ao bloquear a criação de um processo infantil, esta regra protege contra ataques de engenharia social e impede a exploração do código de abusar de uma vulnerabilidade no Outlook.  

  **Padrão**: Ativar

- **Aplicações de escritório executáveis criação ou lançamento de conteúdo**  
  [Regra de redução da superfície](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) de ataque – Quando definido para *bloquear,* as aplicações do Office não podem criar conteúdo executável. As aplicações de escritório incluem Word, Excel, PowerPoint, OneNote e Access.  

  Esta regra visa comportamentos típicos usados por addons e scripts suspeitos e maliciosos (extensões) que criam ou lançam ficheiros executáveis. Esta é uma técnica típica de malware. As extensões estão bloqueadas de serem usadas por aplicações do Office. Normalmente, estas extensões utilizam o Windows Scripting Host (ficheiros.wsh) para executar scripts que automatizam determinadas tarefas ou fornecem funcionalidades adicionais criadas pelo utilizador.

  **Predefinição**: Bloco

## <a name="bitlocker"></a>BitLocker  

Para mais informações, as definições da [Política do Grupo BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) na documentação do Windows.  

- **Encriptar dispositivos**  
  Selecione *Sim* para ativar a encriptação do dispositivo BitLocker. Dependendo do hardware do dispositivo e versão do Windows, os utilizadores do dispositivo podem ser convidados a confirmar que não existe encriptação de terceiros no dispositivo. Ligar a encriptação do Windows enquanto a encriptação de terceiros está ativa tornará o dispositivo instável.  

   **Padrão**: Sim

- **Política de unidade amovível de armário bit**  
  Os valores desta política determinam a força da cifra que o BitLocker utiliza para encriptação de unidades amovíveis. As empresas controlam o nível de encriptação para uma maior segurança (a AES-256 é mais forte que a AES-128). Se selecionar *Sim* para ativar esta definição, pode configurar um algoritmo de encriptação e uma força de cifra chave para unidades de dados fixas, unidades do sistema operativo e unidades de dados amovíveis individualmente. Para unidades fixas e funcionais do sistema, recomendamos que utilize o algoritmo XTS-AES. Para unidades amovíveis, deve utilizar AES-CBC 128-bit ou AES-CBC 256-bit se a unidade for utilizada noutros dispositivos que não estejam a executar o Windows 10, versão 1511 ou mais tarde. A alteração do método de encriptação não tem qualquer efeito se a unidade já estiver encriptada ou se a encriptação estiver em curso. Nestes casos, esta definição de política é ignorada. 

  Para a política de unidade amovível bit locker, configure as seguintes definições:

  - **Exigir encriptação para o acesso à escrita**  
    **Padrão**: Sim

  - **Método de encriptação**  
    **Padrão**: AES 128bit CBC

- **Encriptar cartão de armazenamento (apenas para dispositivos móveis)** Selecionando *Sim* irá encriptar o cartão de armazenamento do dispositivo móvel.  

   **Padrão**: Sim

- **Política de unidade fixa de armário bit**  
  Os valores desta política determinam a força da cifra que o BitLocker utiliza para encriptação de unidades fixas. As empresas podem controlar o nível de encriptação para uma maior segurança (a AES-256 é mais forte que a AES-128). Se ativar esta definição, pode configurar um algoritmo de encriptação e a força de cifra chave para unidades de dados fixas, unidades do sistema operativo e unidades de dados amovíveis individualmente. Para unidades fixas e funcionais do sistema, recomendamos que utilize o algoritmo XTS-AES. Para unidades amovíveis, deve utilizar AES-CBC 128-bit ou AES-CBC 256-bit se a unidade for utilizada noutros dispositivos que não estejam a executar o Windows 10, versão 1511 ou mais tarde. A alteração do método de encriptação não tem qualquer efeito se a unidade já estiver encriptada ou se a encriptação estiver em curso. Nestes casos, esta definição de política é ignorada.

  Para a política de unidade fixa bit locker, configure as seguintes definições:

  - **Exigir encriptação para o acesso à escrita**  
    **Padrão**: Sim

  - **Método de encriptação**  
    **Padrão**: AES 128bit XTS

- **Política de condução do sistema de armários bit**  
  Os valores desta política determinam a força da cifra que o BitLocker utiliza para encriptação da unidade do sistema. As empresas podem querer controlar o nível de encriptação para uma maior segurança (a AES-256 é mais forte do que a AES-128). Se ativar esta definição, pode configurar um algoritmo de encriptação e a força de cifra chave para unidades de dados fixas, unidades do sistema operativo e unidades de dados amovíveis individualmente. Para unidades fixas e funcionais do sistema, recomendamos que utilize o algoritmo XTS-AES. Para unidades amovíveis, deve utilizar AES-CBC 128-bit ou AES-CBC 256-bit se a unidade for utilizada noutros dispositivos que não estejam a executar o Windows 10, versão 1511 ou mais tarde. A alteração do método de encriptação não tem qualquer efeito se a unidade já estiver encriptada ou se a encriptação estiver em curso. Nestes casos, esta definição de política é ignorada.  

  Para a política de acionamento do sistema bit, configure as seguintes definições:  

  - **Método de encriptação**  
    **Padrão**: AES 128bit XTS

## <a name="device-control"></a>Controlo de Dispositivos  

- **Digitalizar unidades amovíveis durante uma varredura completa**  
  [Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning) - Quando definido para *Sim,* O Defender procura software malicioso e indesejado em unidades amovíveis, como pen drives, durante uma varredura completa. O Antivírus Defender digitaliza todos os ficheiros em dispositivos USB antes que os ficheiros do dispositivo USB possam ser executados.

  Definição relacionada nesta lista: *Defender/AllowFullScanOnMappedNetworkDrives*  

  **Padrão**: Sim

- **Enumeração de dispositivos externos incompatíveis com a Proteção Kernel DMA**  
   Ver *DmaGuard/DeviceEnumerationPolicy* in [Policy CSP - DmaGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Esta política proporciona segurança adicional contra dispositivos externos capazes de DMA. Permite um maior controlo sobre a enumeração de dispositivos externos capazes de DMA que são incompatíveis com o isolamento da memória do dispositivo DMA e o sandboxing.

  Esta política só entra em vigor quando a Kernel DMA Protection é suportada e ativada pelo firmware do sistema. Kernel DMA Protection é uma funcionalidade de plataforma que não pode ser controlada por política ou pelo utilizador de um dispositivo. Deve ser apoiado pelo sistema no momento da fabricação. 

  Para verificar se o sistema suporta a Proteção Kernel DMA, execute mSINFO32.exe no sistema e reveja o campo de *proteção Kernel DMA* na página Resumo.  

  As opções incluem: 
  - *Predefinição do dispositivo* - Depois de iniciar sessão ou desbloquear o ecrã, os dispositivos com controladores compatíveis com o dma de remapeamento podem enumerar a qualquer momento. Os dispositivos com dma remapeando controladores incompatíveis só serão enumerados após o utilizador desbloquear o ecrã
  - *Permitir tudo* - Todos os dispositivos PCIE capazes de DMA externos serão enumerados a qualquer momento
  - *Bloqueie tudo* - Os dispositivos com remapeamento de DMA podem enumerar a qualquer momento. Os dispositivos com DMA a remapear condutores incompatíveis nunca serão autorizados a iniciar e executar DMA em nenhum momento.

  **Predefinição**: Predefinição do dispositivo

- **Instalação de dispositivos de hardware por identificadores de dispositivos**  
  [Instalação/Prevenção de InstalaçõesOfMatchingDeviceIDs](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids) - Com esta política, especifica uma lista de IDs de hardware plug e play e IDs compatíveis para dispositivos que o Windows está impedido de instalar. Esta definição de política tem precedência sobre qualquer outra definição de política que permita ao Windows instalar um dispositivo. Se ativar esta definição de política (definida para bloquear a instalação de dispositivos de *hardware),* o Windows está impedido de instalar um dispositivo cujo ID de hardware ou ID compatível aparece na lista que cria. Se ativar esta definição de política num servidor de ambiente de trabalho remoto, a política afeta a reorientação dos dispositivos especificados de um cliente de ambiente de trabalho remoto para o servidor de ambiente de trabalho remoto. Se desativar ou não configurar esta definição de política (definida para permitir a instalação de dispositivos de *hardware),* os dispositivos podem instalar e atualizar conforme permitido ou impedido por outras definições de política.  

  **Predefinição**: Bloquear a instalação de dispositivos de hardware  

  Quando a instalação do *dispositivo de hardware block* for selecionada, as seguintes definições estão disponíveis.
  - **Remover dispositivos de hardware correspondentes**  
    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*.  

    **Padrão**: Sim

  - **Identificadores de dispositivos de hardware que estão bloqueados**  
    Esta definição só está disponível quando a instalação de dispositivos de *hardware por identificadores* de dispositivo saem definidas para bloquear a instalação do dispositivo de *hardware*. Para configurar esta definição, expanda a opção, selecione **+ Adicionar**, e depois especificar o identificador de dispositivo de hardware que pretende bloquear.  

    **Predefinição**: PCI\CC_0C0A

- **Bloquear o acesso à memória direta**  
  [DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess) - Utilize esta definição de política para bloquear o acesso à memória direta (DMA) para todas as portas a jusante do PCI pluggable a quente num dispositivo, até que um utilizador inicie sessão no Windows. Assim que um utilizador iniciar sessão, o Windows enumerará os dispositivos PCI ligados às portas PCI plug do hospedeiro. Sempre que o utilizador bloqueia a máquina, o DMA é bloqueado em portas PCI de ficha quente sem dispositivos para crianças até que o utilizador volte a entrar. Os dispositivos que já estavam enumerados quando a máquina foi desbloqueada continuarão a funcionar até desligarem a tomada. 

  Esta definição de política só é aplicada quando o BitLocker ou a encriptação do dispositivo estiverem ativadas.  

  **Padrão**: Sim


- **Instalação de dispositivos de hardware por classes de configuração**  
  [Instalação de Dispositivos/InstalaçãoOfMatchingDeviceSetupClasses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses) - Com esta política pode especificar uma lista de identificadores exclusivos da classe de configuração do dispositivo (GUIDs) para controladores de dispositivos que o Windows está impedido de instalar. Esta definição de política tem precedência sobre qualquer outra definição de política que permita ao Windows instalar um dispositivo. Se ativar esta definição de política (definida para bloquear a instalação de dispositivos de *hardware),* o Windows está impedido de instalar ou atualizar os controladores de dispositivos cuja classe GUIDs de configuração do dispositivo aparece na lista que cria. Se ativar esta definição de política num servidor de ambiente de trabalho remoto, a definição de política afeta a reorientação dos dispositivos especificados de um cliente de ambiente de trabalho remoto para o servidor de ambiente de trabalho remoto. Se desativar ou não configurar esta definição de política (definida para permitir a instalação de dispositivos de *hardware),* o Windows pode instalar e atualizar dispositivos conforme permitido ou impedido por outras definições de política.  

  **Predefinição**: Bloquear a instalação de dispositivos de hardware

  Quando a instalação do *dispositivo de hardware block* for selecionada, as seguintes definições estão disponíveis.  

  - **Remover dispositivos de hardware correspondentes**  
    Esta definição só está disponível quando a instalação do *dispositivo de hardware por classes* de configuração estiver definida para bloquear a instalação de dispositivos de *hardware*.  
 
    **Padrão**: Sim  

  - **Identificadores de dispositivos de hardware que estão bloqueados**  
    Esta definição só está disponível quando a instalação do dispositivo de hardware por classes de configuração estiver definida para bloquear a instalação de dispositivos de hardware. Para configurar esta definição, expanda a opção, selecione **+ Adicionar**, e depois especificar o identificador de dispositivo de hardware que pretende bloquear.  
 
    **Predefinição**: {d48179be-ec20-11d1-b6b8-00c04fa372a7}

## <a name="endpoint-detection-and-response"></a>Deteção e Resposta de Ponto Final  
Para mais informações, consulte o [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) na documentação do Windows.  

- **Acelere a frequência** de reporte de telemetria - *Configuração/TelemettryReportingFrequency*

  Acelere a frequência de relatório de telemetria avançada de telemetria do Microsoft Defender.  

  **Padrão**: Sim

- **Partilha de amostras para todos os ficheiros** - *Configuração/Partilha de Amostras* 

  Devoluções ou configurações do parâmetro de partilha de amostras de proteção de ameaças avançada do Microsoft Defender.  

  **Padrão**: Sim

## <a name="exploit-protection"></a>Explorar Proteção  

- **Explorar a proteção XML**  
  Para mais informações, consulte [Import, exporte e implemente configurações](/windows/security/threat-protection/microsoft-defender-atp/import-export-exploit-protection-emet-xml) de proteção na documentação do Windows.  

  Permite ao administrador de TI empurrar uma configuração que representa o sistema desejado e opções de mitigação de aplicações a todos os dispositivos da organização. A configuração é representada por um XML. 

  A proteção de exploração aplica-se ajuda a proteger dispositivos de malware que usam explorações para espalhar e infetar. Utiliza a aplicação De Segurança do Windows ou powerShell para criar um conjunto de atenuações (conhecida como configuração). Em seguida, pode exportar esta configuração como um ficheiro XML e partilhá-la com várias máquinas na sua rede para que todas tenham o mesmo conjunto de definições de mitigação.
 
  Também pode converter e importar um ficheiro XML de configuração EMET existente numa configuração de proteção de exploração XML.

- **Substituição de proteção de exploração de blocos**  
  [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride) – set to *Yes* para evitar que os utilizadores elegam alterações na área de definições de proteção de exploração no Microsoft Defender Security Center. Se desativar ou não configurar esta definição, os utilizadores locais podem fazer alterações na área de definições de proteção de exploração.  
  **Padrão**: Sim  

## <a name="microsoft-defender-antivirus"></a>Antivírus Do Microsoft Defender  

Para mais informações, consulte [Policy CSP - Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) na documentação do Windows.

- **Scan scripts carregados nos navegadores web da Microsoft**  
  [Defender/PermitirScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning) – Definir para *Sim* para permitir a funcionalidade de digitalização do Script Do Microsoft Defender.  

  **Padrão**: Sim

- **Digitalizar mensagens de correio de entrada**  
  [Defender/PermitirEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning) – Definir para *Sim* para permitir que o Microsoft Defender digitale o email.  

  **Padrão**: Sim

- **Consentimento de submissão da amostra de defender**  
  [Defender/SubmeterSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent) - Verifica o nível de consentimento do utilizador no Microsoft Defender para enviar dados. Se o consentimento exigido já tiver sido concedido, o Microsoft Defender submete-os. Caso contrário (e se o utilizador tiver especificado nunca pedir), a UI é lançada para pedir o consentimento do utilizador (quando a *proteção entregue pela Cloud* for definida para *Sim)* antes de enviar dados.  

  **Predefinição**: Enviar amostras seguras automaticamente

- **Sistema de Inspeção de Rede (NIS)**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) - Bloqueie tráfego malicioso detetado por assinaturas no Sistema de Inspeção de Rede (NIS).  
 
  **Padrão**: Sim

- **Intervalo de atualização de assinatura (em horas)**  
  [Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) – Especifique em horas, com que frequência o dispositivo verifica as novas atualizações de assinatura do Defender.  
 
  **Padrão**: 4

- **Configure baixa prioridade da CPU para digitalizações programadas**  
  [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority) – Quando definido para *Sim*, a prioridade do CPU para digitalização está definida para baixo. Quando *não configurado,* não são feitas alterações à prioridade da CPU para as digitalizações programadas.  

    **Padrão**: Sim

- **Bloco de defesa na proteção de acesso**  
  [Defender/AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection) – Quando definido para *Sim*, o Microsoft Defender na Proteção de Acesso está ativado.  

  **Padrão**: Sim

- **Tipo de digitalização do sistema para realizar**  
  [Defender/ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter) - Tipo de scan de defesa.  

  **Padrão**: Digitalização rápida

- **Analisar todas as transferências**  
  [Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection) - Quando definido para *Sim,* o Defender digitaliza todos os ficheiros e anexos descarregados.  

  **Padrão**: Sim

- **Dias antes de apagar malware em quarentena**  
  [Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) - Especifique quantos dias para manter os itens de quarentena no sistema antes de serem automaticamente eliminados. Quando definidos a zero, os itens em quarentena nunca são automaticamente eliminados.  

  **Padrão**: 0

- **Hora de início da varredura agendada**  
  [Defender/ScheduleScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime) – Marque uma hora do dia para o Defender digitalizar dispositivos. 
  
  Opção relacionada nesta lista: *Defender/AgendasScanDay*   

  **Padrão**: 2 AM

- **Proteção entregue em nuvem**  
  [Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection) – Quando definido para *Sim,* o Microsoft Defender envia informações à Microsoft sobre quaisquer problemas que encontre. A Microsoft analisará essa informação, aprenderá mais sobre problemas que afetam o mesmo e outros clientes e oferecerá soluções melhoradas.

  Quando esta política estiver definida para *Sim,* pode utilizar o tipo de consentimento de *submissão* da amostra Defender para dar aos utilizadores o controlo sobre o envio de informações a partir do seu dispositivo.  

  **Padrão**: Sim

- **Defender ação de aplicação potencialmente indesejada**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – O Microsoft Defender Antivirus pode identificar e bloquear *aplicações potencialmente indesejadas* (API) de descarregar e instalar em pontos finais da sua rede. 
 
  - Quando definido para *bloquear,* o Microsoft Defender bloqueia os API, e lista-os na história juntamente com outras ameaças.
  - Quando definido para *auditoria,* o Microsoft Defender deteta APIs mas não os bloqueia. As informações sobre as aplicações que o Microsoft Defender teria tomado medidas podem ser encontradas através da procura de eventos criados pelo Microsoft Defender no Observador de Eventos.  
  - Quando definido para a *predefinição do Dispositivo,* a proteção PUA está desligada.  
 
  **Predefinição**: Bloco

- **Nuvem de defensor prolonga tempo de tempo**  
  [Defender/CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout) - Especifique a quantidade máxima de tempo adicional que o Microsoft Defender Antivirus deve bloquear um ficheiro enquanto aguarda um resultado da nuvem. O valor base de tempo que o Microsoft Defender espera é de 10 segundos. Qualquer tempo adicional que especifique aqui (até 50 segundos) é adicionado a esses 10 segundos. Na maioria dos casos, a varredura leva menos tempo do que o máximo. Alargar o período de tempo permite que a cloud investigue ficheiros suspeitos de forma mais minuciosa.  

  Por predefinição, o valor de tempo expandido é 0 (desativado). Intune recomenda que ative esta definição e especifique pelo menos 20 segundos adicionais.  
 
  **Padrão**: 0

- **Analisar ficheiros de arquivo**  
  [Defender/PermitirArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning) – Definir para *Sim* para ter ficheiros de arquivo do Microsoft Defender.  

  **Padrão**: Sim

- **Calendário de scan do sistema de defesa**  
  [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday) - Agendar em que dia os dispositivos defender scans. 
 
  Opção relacionada nesta lista: *Defender/ScheduleScanTime*

  **Predefinição**: Utilizador definido

- **Monitorização do comportamento**  
  [Defender/Permitir A Monitorização do Comportamento](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring) – Definir para *Sim* para ativar a funcionalidade de Monitorização de Comportamento do Microsoft Defender. Incorporados no Windows 10, os sensores de monitorização de comportamento do Microsoft Defender recolhem e processam sinais comportamentais do sistema operativo e enviam estes dados de sensores para a sua instância privada, isolada e cloud do MICROSOFT Defender ATP.  

  **Padrão**: Sim

- **Scan ficheiros abertos a partir de pastas de rede**  
  [Defender/Permitir a digitalizaçãoDeNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles) – set to *Yes* para ter ficheiros de digitalização do Microsoft Defender na rede. O utilizador não conseguirá remover malware detetado a partir de ficheiros apenas de leitura.  

  **Padrão**: Sim

- **Nível de bloco de nuvem de defensor**  
  [Defender/CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel) – Utilize esta política para determinar a agressividade do Antivírus do Microsoft Defender em bloquear e digitalizar ficheiros suspeitos. As opções incluem:

  - High - Bloqueie agressivamente ficheiros desconhecidos ao mesmo tempo que otimiza o desempenho do cliente (maior probabilidade de falsos positivos)
  - High plus - Bloqueie agressivamente ficheiros desconhecidos e aplique medidas de proteção adicionais (pode afetar o desempenho do cliente)
  - Tolerância zero - Bloqueie todos os ficheiros executáveis desconhecidos

  **Predefinição**: Não configurado

- **Monitorização em tempo real**  
  [Defender/Permitir Monitorização Realtime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring) - Definir para *Sim* para permitir a monitorização real do Microsoft Defender.  

  **Padrão**: Sim

- **Limite de utilização do CPU durante uma varredura**  
  [Defender/AvgCPULoadFactor](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor) – Especifique a utilização máxima média do CPU % que o Microsoft Defender pode utilizar durante uma varredura.  

  **Padrão**: 50

- **Scan mapeado unidades de rede durante uma varredura completa**  
  [Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives) - set to *Yes* para ter ficheiros de digitalização do Microsoft Defender na rede. O utilizador não pode remover malware detetado a partir de ficheiros apenas de leitura,

  Definição relacionada nesta lista: *Defender/PermitirFicheiros de Redes de Digitalização*

  **Padrão**: Sim

- **Bloqueie o acesso do utilizador final ao Defender**  
  [Defender/PermitirUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess) – Definir para *Sim* bloquear o acesso dos utilizadores finais ao Microsoft Defender UI no seu dispositivo.  

  **Padrão**: Sim

- **Hora de início da varredura rápida**  
  [Defender/ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) - Agende uma hora do dia para o Defender fazer uma sondagem rápida.  

  **Padrão**: 2 AM

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall
Para mais informações, consulte o [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) na documentação do Windows.

- **Tempo inativo da associação de segurança antes da eliminação** - *MdmStore/Global/SaIdleTime*   
  As associações de segurança são eliminadas depois de o tráfego da rede não ser visto durante este número de segundos.  
  **Padrão**: 300

- **Protocolo de transferência de ficheiros** - *MdmStore/Global/DisableStatefulFtp*   
  Bloqueia o protocolo de transferência de ficheiros (FTP).  
  **Padrão**: Sim

- **Pacote de fila** - *MdmStore/Global/EnablePacketQueue*    
  Especifique como a escala para o software no lado de receção está ativada para a receção encriptada e texto claro para a frente para o cenário de gateway do túnel IPsec. Isto garante que a encomenda do pacote seja preservada.  
  **Predefinição**: Predefinição do dispositivo

- **Domínio de perfil de firewall** - *FirewallRules/FirewallRuleName/Perfis*  
  Especifica os perfis a que a regra pertence: Domínio, Privado, Público. Este valor representa o perfil para redes ligadas a domínios.  

  Definições disponíveis:  
  - **Respostas unicast às emissões multicast necessárias**  
    **Padrão**: Sim

  - **Regras de aplicação autorizadas da política do grupo fundidas**  
    **Padrão**: Sim

  - **Notificações de entrada bloqueadas**  
    **Padrão**: Sim

  - **Regras portuárias globais da política do grupo fundidas**  
    **Padrão**: Sim

  - **Modo furtivo bloqueado**  
    **Padrão**: Sim

  - **Firewall ativado**  
    **Padrão**: Permitido

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    **Padrão**: Sim

  - **Regras políticas da política de grupo não fundidas**  
    **Padrão**: Sim

- **Perfil de firewall público** - *FirewallRules/FirewallRuleName/Perfis*  
  Especifica os perfis a que a regra pertence: Domínio, Privado, Público. Para nós, este número é um eixo de uma comunidade que quer saber para onde vai e quer saber para onde vai e quer saber para onde vai e quer saber Estas redes são classificadas como públicas pelos administradores do servidor. A classificação acontece na primeira vez que o anfitrião se conecta à rede. Normalmente, estas redes estão em aeroportos, cafés e outros locais públicos onde os pares da rede ou o administrador da rede não são de confiança.  

  Definições disponíveis:

  - **Ligações de entrada bloqueadas**  
    **Padrão**: Sim 

  - **Respostas unicast às emissões multicast necessárias**  
    **Padrão**: Sim  

  - **Modo furtivo necessário**  
    **Padrão**: Sim 
 
  - **Ligações de saída necessárias**  
    **Padrão**: Sim  

  - **Regras de aplicação autorizadas da política do grupo fundidas**  
    **Padrão**: Sim  

  - **Notificações de entrada bloqueadas**  
    **Padrão**: Sim  

  - **Regras portuárias globais da política do grupo fundidas**  
    **Padrão**: Sim

  - **Modo furtivo bloqueado**  
    **Padrão**: Sim

  - **Firewall ativado**  
    **Padrão**: Permitido  

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    **Padrão**: Sim  

  - **Tráfego de entrada necessário**  
    **Padrão**: Sim

  - **Regras políticas da política de grupo não fundidas**  
    **Padrão**: Sim  

- **Perfil de firewall privado** - *FirewallRules/FirewallRuleName/Perfis*  
  Especifica os perfis a que a regra pertence: Domínio, Privado, Público. Este valor representa o perfil para redes privadas.  

  Definições disponíveis: 

  - **Ligações de entrada bloqueadas**  
    **Padrão**: Sim

  - **Respostas unicast às emissões multicast necessárias**  
    **Padrão**: Sim

  - **Modo furtivo necessário**  
    **Padrão**: Sim

  - **Ligações de saída necessárias**  
    **Padrão**: Sim

  - **Notificações de entrada bloqueadas**  
    **Padrão**: Sim

  - **Regras portuárias globais da política do grupo fundidas**  
    **Padrão**: Sim

  - **Modo furtivo bloqueado**  
    **Padrão**: Sim  

  - **Firewall ativado**  
    **Padrão**: Permitido

  - **Regras de aplicação autorizadas da política do grupo não fundidas**  
    **Padrão**: Sim

  - **Regras de segurança de ligação da política do grupo não fundidas**  
    **Padrão**: Sim

  - **Tráfego de entrada necessário**  
    **Padrão**: Sim

  - **Regras políticas da política de grupo não fundidas**  
    **Padrão**: Sim  

- **Método de codificação de chaves pré-partilhadas firewall**  
  **Padrão**: UTF8

- **Verificação da lista de revogação do certificado**  
  **Predefinição**: Predefinição do dispositivo

## <a name="web--network-protection"></a>Proteção web e rede  

- **Tipo de proteção de rede**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) - Esta política permite-lhe ligar ou desligar a proteção da rede no Microsoft Defender Exploit Guard. A proteção de rede é uma funcionalidade do Microsoft Defender Exploit Guard que protege os funcionários que usam qualquer aplicação para aceder a esquemas de phishing, sites de hospedagem de exploração e conteúdo malicioso na Internet. Isto inclui impedir que os navegadores de terceiros se conectem a sites perigosos.  

  Quando definido para o modo *Ativa* ou *Audit,* os utilizadores não podem desligar a proteção da rede e pode utilizar o Microsoft Defender Security Center para visualizar informações sobre tentativas de ligação.  
 
  - *O Enable* irá bloquear utilizadores e aplicações da ligação a domínios perigosos.  
  - *O modo de auditoria* não impede utilizadores e aplicações de se conectarem a domínios perigosos.  

  Quando *definidos*para o Utilizador definidos, os utilizadores e aplicações não estão impedidos de se conectarem a domínios perigosos, e as informações sobre ligações não estão disponíveis no Microsoft Defender Security Center.  

  **Predefinido**: Modo de auditoria

- **Requerer smartScreen para microsoft edge**  
  [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen) - O Microsoft Edge utiliza o Microsoft Defender SmartScreen (ligado) para proteger os utilizadores de potenciais esquemas de phishing e software malicioso por padrão. Por predefinição, esta política está ativada (definida para *Sim),* e quando ativada impede os utilizadores de desligarem o Microsoft Defender SmartScreen.  Quando a política eficaz de um dispositivo é igual a Não configurada, os utilizadores podem desligar o Microsoft Defender SmartScreen, o que deixa o dispositivo desprotegido.  

  **Padrão**: Sim
  
- **Bloqueie o acesso malicioso ao site**  
  [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride) - Por padrão, o Microsoft Edge permite que os utilizadores contornem (ignore) os avisos do Microsoft Defender SmartScreen sobre sites potencialmente maliciosos, permitindo que os utilizadores continuem no site. Com esta política ativada (definida para *Sim),* o Microsoft Edge impede os utilizadores de contornarem os avisos e impede-os de continuarem no site.  

  **Padrão**: Sim

- **Bloquear o download de ficheiros não verificados**  
  [Browser/PreventSmartScreenOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles) - Por padrão, o Microsoft Edge permite que os utilizadores contornem (ignore) os avisos do Microsoft Defender SmartScreen sobre ficheiros potencialmente maliciosos, permitindo-lhes continuar a descarregar ficheiros não verificados. Com esta política ativada (definida para *Sim),* os utilizadores são impedidos de contornar os avisos e não podem descarregar ficheiros não verificados.  

  **Padrão**: Sim

## <a name="windows-hello-for-business"></a>Windows Hello para Empresas  

Para mais informações, consulte [o PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) na documentação do Windows.

- **Configure o Windows Hello para o - de Negócios** *Inquilino/Políticas/UsePassportForWork*    
  O Windows Hello for Business é um método alternativo para iniciar sessão no Windows substituindo palavras-passe, Smart Cards e Cartões Inteligentes Virtuais.  


  > [!IMPORTANT]
  > As opções para esta definição são invertidas do seu significado implícito. Embora invertido, um valor de *Sim* não permite o Windows Hello e, em vez disso, é tratado como *Não configurado*. Quando esta definição está definida para *Não configurar,* o Windows Hello está ativado em dispositivos que recebem esta linha de base.
  >
  > As seguintes descrições foram revistas para refletir este comportamento. A inversão das definições será corrigida numa futura atualização desta linha de base de segurança.

  - Quando definido para *Não configurado,* o Windows Hello está ativado e o dispositivo disponibiliza o Windows Hello for Business.
  - Quando definido para *Sim,* a linha de base não afeta a definição de política do dispositivo. Isto significa que, se o Windows Hello for Business estiver desativado num dispositivo, permanece desativado. Se estiver ativado, permanece ativado.
  <!-- expected behavior 
  - When set to *Yes*, you  enable this policy and the device provisions Windows Hello for Business.  
  - When set to *Not configured*, the baseline does not affect the policy setting of the device. This means that if Windows Hello for Business is disabled on a device, it remains disabled. If its enabled, it remains enabled. 
  -->

  Não é possível desativar o Windows Hello for Business através desta linha de base. Pode desativar o Windows Hello for Business quando configurar a [inscrição](windows-hello.md)do Windows, ou como parte de um perfil de configuração do dispositivo para [proteção de identidade](identity-protection-configure.md).  

O Windows Hello for Business é um método alternativo para iniciar sessão no Windows substituindo palavras-passe, Smart Cards e Cartões Inteligentes Virtuais.  

  Se ativar ou não configurar esta definição de política, o dispositivo disponibiliza o Windows Hello for Business. Se desativar esta definição de política, o dispositivo não disponibiliza o Windows Hello for Business para qualquer utilizador.

  Intune não suporta desativar o Windows Hello. Em vez disso, pode configurar a política para ativar o Windows Hello for Business (Sim), ou não configurar o Windows Hello diretamente (não configurado). Quando não configurado, um dispositivo pode receber a configuração através de outra suposição, que pode ativar ou desativar esta funcionalidade.  

  **Padrão**: Sim  

- **Requerer letras minúsculas em PIN** - *TenantId/Policies/PINComplexity/LowercaseLetters*  
  **Padrão**: Permitido  

- **Requerer caracteres especiais em PIN** - *TenantId/Policies/PINComplexity/SpecialCharacters*  
  **Padrão**: Permitido  

- **Exija letras maiúsculas em PIN** - *TenantId/Policies/PINComplexity/UppercaseLetters*   
  **Padrão**: Permitido  

