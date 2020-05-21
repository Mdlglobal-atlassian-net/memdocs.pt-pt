---
title: Segurança de ponta Intune As definições de redução da superfície do ataque / Microsoft Docs
description: Definições de política de redução de superfície de ataque de ataque de ponto final no Microsoft Intune
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
ms.openlocfilehash: 7f200e5cb5bb4aa0f29cbd3adc0f177bb14e5476
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431319"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Ajustes de política de redução de superfície de ataque para segurança de ponto final em Intune

Ver as definições que pode configurar em perfis para a política de *redução* de superfície de ataque no nó de segurança de Ponto final de Intune como parte de uma política de [segurança endpoint](../protect/endpoint-security-policy.md).

Plataformas e perfis suportados:

- **Windows 10 e mais tarde:**
  - Perfil: **App e isolamento do navegador**
  - Perfil: **Proteção web**
  - Perfil: **Controlo de aplicações**
  - Perfil: Regras de **redução da superfície** de ataque
  - Perfil: **Controlo do dispositivo**
  - Perfil: **Explorar a proteção**

## <a name="app-and-browser-isolation-profile"></a>Perfil de isolamento de aplicativos e navegador

### <a name="app-and-browser-isolation"></a>App e isolamento do navegador

- **Ligue a Guarda de Aplicação para Edge (Opções)**  
  CSP: [Permitirguarda de Aplicações doWindowsDefender](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Não configurado** *(predefinido)*
  - **Ativado para Edge** - Application Guard abre sites não aprovados num recipiente de navegação virtualizado Hyper-V.

  Quando programado para *ativar para edge,* estão disponíveis as seguintes definições:
  
  - **Comportamento de clipboard**  
    CSP: Definições de [clipboard](https://go.microsoft.com/fwlink/?linkid=872351)

    Escolha quais as ações de cópia e pasta permitidas a partir do PC local e um navegador virtual Application Guard.
    - **Não configurado** *(predefinido)*
    - **Cópia e pasta de blocos entre PC e browser**
    - **Permitir copiar e colar do navegador para PC apenas**
    - **Permitir copiar e colar do PC para o navegador apenas**
    - **Permitir cópia e pasta entre PC e browser**

  - **Bloquear conteúdo externo de sites não aprovados pela empresa**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Não configurado** *(predefinido)*
    - **Sim** - Bloqueie o conteúdo de sites não aprovados a partir do carregamento.

  - **Recolher registos para eventos que ocorram dentro de uma sessão de navegação da Guarda de Aplicações**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Não configurado** *(predefinido)*
    - **Sim** - Recolher registos para eventos que ocorram dentro de uma sessão de navegação virtual do Application Guard.

  - **Permitir que os dados do navegador gerados pelo utilizador sejam guardados**  
    CSP: [Permitir a persistência](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Não configurado** *(predefinido)*
    - **Sim** - Permita que os dados do utilizador que são criados durante uma sessão de navegação virtual do Application Guard sejam guardados. Exemplos de dados de utilizadores incluem senhas, favoritos e cookies.

  - **Ativar a aceleração gráfica de hardware**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Não configurado** *(predefinido)*
    - **Sim** - Dentro da sessão de navegação virtual do Application Guard, utilize uma unidade de processamento de gráficos virtuais para carregar websites intensivos de gráficos mais rapidamente.

  - **Permitir que os utilizadores descarreguem ficheiros para o anfitrião**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Não configurado** *(predefinido)*
    - **Sim** - Permitir que os utilizadores descarreguem ficheiros do navegador virtualizado para o sistema operativo anfitrião.

- **Guarda de aplicação permite impressão para impressoras locais**  

  - **Não configurado** *(predefinido)*
  - **Sim** - Permitir imprimir impressões para impressoras locais.

- **O guarda de aplicações permite a impressão para impressoras de rede**  

  - **Não configurado** *(predefinido)*
  - **Sim** - Permitir imprimir impressões para impressoras de rede.

- **O resguardo de aplicação permite imprimir para PDF**  

  - **Não configurado** *(predefinido)*
  - **Sim**- Permitir imprimir impressão para PDF.

- **O resguardo de aplicação permite imprimir para XPS**  

  - **Não configurado** *(predefinido)*
  - **Sim** - - Permitir imprimir impressão para XPS.

- **Política de isolamento de rede Windows**  
  
  - **Não configurado** *(predefinido)*
  - **Sim** - Configure a política de isolamento da rede Windows.  
  
  Quando definido para *configurar,* pode configurar as seguintes definições.

  - **Gamas IP**  
    Expanda a gota, selecione **Adicionar**, e, em seguida, especificar um *endereço inferior* e, em seguida, um *endereço superior*.

  - **Recursos em nuvem**  
    Expanda a queda, selecione **Adicionar,** e depois especificar um *endereço IP ou FQDN* e um *Proxy*.

  - **Domínios de rede**  
   Expanda a queda, selecione **Adicionar**, e depois especificar *domínios*de rede .

  - **Servidores proxy**  
    Expanda a gota, selecione **Adicionar**, e depois especificar *servidores Proxy*.

  - **Servidores internos de procuração**  
    Expanda a gota, selecione **Adicionar**, e, em seguida, especificar *servidores internos proxy*.

  - **Recursos neutros**  
    Expanda a queda, selecione **Adicionar**, e depois especificar *recursos neutros*.

  - **Desativar a deteção automática de outros servidores de procuração da empresa**  
    - **Não configurado** *(predefinido)*
    - **Sim** - Desativar a deteção automática de outros servidores de procuração da empresa.

  - **Desativar a deteção automática de outras gamas IP da empresa**  
    - **Não configurado** *(predefinido)*
    - **Sim** - Desativar a deteção automática de outras gamas IP da empresa.

## <a name="web-protection-profile"></a>Perfil de proteção web

### <a name="web-protection"></a>Proteção Web

- **Ativar a proteção da rede**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desativado.
  - **Utilizador definido**
  - **Ativar** - A proteção da rede está ativada para todos os utilizadores do sistema.
  - **Modo** de auditoria - Os utilizadores não estão bloqueados de domínios perigosos e os eventos windows são levantados.

- **Requerer smartScreen para microsoft edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sim** - Utilize o SmartScreen para proteger os utilizadores de potenciais esquemas de phishing e software malicioso.
  - **Não configurado** *(predefinido)*

- **Bloqueie o acesso malicioso ao site**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sim** - Bloqueie os utilizadores de ignorar os avisos do Filtro SmartScreen do Microsoft Defender e impedi-los de ir ao site.
  - **Não configurado** *(predefinido)*

- **Bloquear o download de ficheiros não verificados**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sim** - Bloqueie os utilizadores de ignorar os avisos do Filtro SmartScreen do Microsoft Defender e bloqueá-los de descarregar ficheiros não verificados.
  - **Não configurado** *(predefinido)*

## <a name="application-control-profile"></a>Perfil de controlo de aplicações

### <a name="microsoft-defender-application-control"></a>Controlo de aplicações do Microsoft Defender

- **Controlo de aplicações de cacifo de aplicativos**  
  - **Não configurado** *(predefinido)*
  - **Impor componentes e armazenar aplicações**
  - **Componentes de auditoria e aplicações de loja**
  - **Impor componentes, apps de loja e Smartlocker**
  - **Componentes de auditoria, apps de loja e SMartlocker**

- **Bloqueie os utilizadores de ignorar os avisos do SmartScreen**  
  [PreventoverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  Esta definição requer a definição 'Impor o SmartScreen para aplicações e ficheiros'.
  - **Não configurado** *(predefinido*) - Devolve a definição à predefinição do Windows, o que permite que o utilizador se sobresseia.
  - **Sim** - - O SmartScreen não apresentará uma opção para o utilizador ignorar o aviso e executar a aplicação. O aviso é apresentado, mas o utilizador não poderá contorná-lo.

- **Ligue o Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Não configurado** *(predefinido*) - Devolva a definição para o predefinido do Windows, que é para ativar o SmartScreen, no entanto os utilizadores podem alterar esta definição. Para desativar o SmartScreen, utilize um URI personalizado.
  - **Sim** - Impor o uso do SmartScreen para todos os utilizadores.

## <a name="attack-surface-reduction-rules-profile"></a>Perfil de regras de redução de superfície de ataque

### <a name="attack-surface-reduction-rules"></a>Regras de redução de superfície de ataque

- **Roubo de credenciais bloqueadas do subsistema da autoridade de segurança local do Windows (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874499)

  Esta regra de redução da superfície de ataque (ASR) é controlada através do seguinte GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Utilizador definido**
  - **Ativar** - As tentativas de roubar credenciais através de lsass.exe estão bloqueadas.
  - **Modo** de auditoria - Os utilizadores não estão bloqueados de domínios perigosos e os eventos windows são levantados.

- **Block Adobe Reader de criar processos infantis**  
  [Reduzir superfícies de ataque com regras de redução da superfície de ataque](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Esta regra ASR é controlada através do seguinte GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Não configurado** *(predefinido)*- O predefinido do Windows é restaurado, é não bloquear a criação de processos infantis.
  - **Utilizador definido**
  - **Ativar** - O Adobe Reader está impedido de criar processos infantis.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear processos infantis.

- **Bloqueio de pedidos de injeção de código em outros processos**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872974)

  Esta regra ASR é controlada através do seguinte GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - As aplicações do escritório estão bloqueadas de injetar código noutros processos.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Aplicações do Block Office da criação de conteúdo executável**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872975)

  Esta regra ASR é controlada através do seguinte GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - As aplicações do escritório estão bloqueadas de criar conteúdo executável.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloqueie todas as candidaturas do Office à criação de processos infantis**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872976)

  Esta regra ASR é controlada através do seguinte GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - As candidaturas ao escritório estão bloqueadas de criar processos infantis.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Block Win32 API liga da macro do Office**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872977)

  Esta regra ASR é controlada através do seguinte GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - Os macros do escritório estão impedidos de usar chamadas Win32 API.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Block Office apps de comunicação de criação de processos infantis**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874499)  

  Esta regra ASR é controlada através do seguinte GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Não configurado** *(predefinido)*- O predefinido do Windows é restaurado, o que é não bloquear a criação de processos infantis.
  - **Utilizador definido**
  - **Enable** - Os pedidos de comunicação do escritório estão bloqueados da criação de processos infantis.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear processos infantis.

- **Execução por blocos de scripts potencialmente obfuscados (js/vbs/ps)**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872978)

  Esta regra ASR é controlada através do seguinte GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - Defensor bloqueia execução de scripts obfuscados.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloqueie o JavaScript ou o VBScript a partir do lançamento de conteúdo executável descarregado**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872979)

   Esta regra ASR é controlada através do seguinte GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - Defender bloqueia ficheiros JavaScript ou VBScript que foram descarregados da Internet a partir de serem executados.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Criações de processo sinuosos originários dos comandos PSExec e WMI**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874500)

  Esta regra ASR é controlada através do seguinte GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - A criação de processos por comandos PSExec ou WMI está bloqueada.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloqueie processos não confiáveis e não assinados que vão a partir de USB**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874502)

  Esta regra ASR é controlada através do seguinte GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco** - Processos não confiáveis e não assinados que funcionam a partir de uma unidade USB estão bloqueados.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloqueie ficheiros executáveis de executar a menos que cumpram critérios de prevalência, idade ou lista de confiança**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874503)

  Esta regra ASR é controlada através do seguinte GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Bloco**
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Bloquear o download de conteúdo executável a partir de clientes de e-mail e webmail**  
  [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Block** - Conteúdo executável descarregado de e-mail e clientes de webmail está bloqueado.
  - **Modo** de auditoria - Os eventos windows são levantados em vez de bloquear.

- **Use proteção avançada contra ransomware**  
   [Proteger dispositivos de explorações](https://go.microsoft.com/fwlink/?linkid=874504)

  Esta regra ASR é controlada através do seguinte GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Não configurado** *(predefinido*) - A definição volta ao predefinido do Windows, que está desligado.
  - **Utilizador definido**
  - **Ativar**
  - **Modo** de auditoria - - Os eventos windows são levantados em vez de bloquear.

- **Ativar a proteção das pastas**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Não configurado** *(predefinido*) - Esta definição retorna ao seu padrão, que não é leitura ou escrita sem bloqueio.
  - **Ativar** - Para aplicações não fidedignas, o Defender bloqueia as tentativas de modificar ou eliminar ficheiros em pastas protegidas ou escrever para sectores de disco. O Defender determina automaticamente quais as aplicações que podem ser confiáveis. Em alternativa, pode definir a sua própria lista de aplicações fidedignas.
  - **Modo** de auditoria - Os eventos do Windows são levantados quando aplicações não confiáveis acedem a pastas controladas, mas não são aplicados blocos.
  - **Modificação do disco de blocos** - Apenas as tentativas de escrever para os sectores do disco estão bloqueadas.
  - **Modificação de discos** de auditoria - Os eventos windows são levantados em vez de bloquear tentativas de escrever para sectores de discos.
  
- **Excluir ficheiros e caminhos das regras de redução da superfície de ataque**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Expanda a queda e, em seguida, selecione **Adicionar** para definir um **Caminho** para um ficheiro ou pasta para excluir das suas regras de redução da superfície de ataque.

## <a name="device-control-profile"></a>Perfil de controlo do dispositivo

### <a name="device-control"></a>Controlo de Dispositivos

- **Instalação de dispositivos de hardware por identificadores de dispositivos**  
  [Prevenir instalações de Dispositivos DeCorrespondênciaIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Esta definição permite especificar uma lista de IDs de hardware plug e play e IDs compatíveis para dispositivos que o Windows está impedido de instalar. Esta definição de política tem precedência sobre qualquer outra definição de política que permita ao Windows instalar um dispositivo.  Se ativar esta definição de política num servidor de ambiente de trabalho remoto, a definição de política afeta a reorientação dos dispositivos especificados de um cliente de ambiente de trabalho remoto para o servidor de ambiente de trabalho remoto.

  - **Não configurado**
  - Permitir a instalação de dispositivos de **hardware** - Os dispositivos podem ser instalados e atualizados conforme permitido ou impedido por outras definições de política.
  - Bloquear a **instalação** do dispositivo de hardware *(predefinido)*- O Windows está impedido de instalar um dispositivo cujo ID de hardware ou ID compatível aparece numa lista que define.

  Quando definido para bloquear a instalação do dispositivo de *hardware,* pode configurar as seguintes definições:

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

- **Digitalizar unidades amovíveis durante a varredura completa**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Não configurado** *(predefinido*) - A definição retorna ao padrão do cliente, que digitaliza unidades amovíveis, no entanto o utilizador pode desativar esta digitalização.
  - **Sim** - Durante uma varredura completa, as unidades amovíveis (como as pen USB) são digitalizadas.
  
## <a name="exploit-protection-profile"></a>Explorar o perfil de proteção

### <a name="exploit-protection"></a>Exploit Protection

- **Upload XML**  
  CSP: [Definições de Proteção de Exploração](https://go.microsoft.com/fwlink/?linkid=2067035)

  Permite ao administrador de TI empurrar uma configuração que representa o sistema desejado e opções de mitigação de aplicações a todos os dispositivos da organização. A configuração é representada por um ficheiro XML. A proteção de exploração pode ajudar a proteger dispositivos de malware que usam explorações para espalhar e infetar. Utiliza a aplicação De Segurança do Windows ou powerShell para criar um conjunto de atenuações (conhecida como configuração). Em seguida, pode exportar esta configuração como um ficheiro XML e partilhá-la com várias máquinas na sua rede para que todas tenham o mesmo conjunto de definições de mitigação. Também pode converter e importar um ficheiro XML de configuração EMET existente numa configuração de proteção de exploração XML.

  Escolha **selecione Ficheiro XML,** especifique o upload do ficheiro XML e, em seguida, clique em **Selecionar**.
  - **Não configurado** *(predefinido)*
  - **Sim**

- **Bloqueie os utilizadores de editar a interface de proteção Exploit Guard**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Não configurado** *(predefinido)*- Os utilizadores locais podem fazer alterações na área de definições de proteção de exploração.
  - **Sim** - Evite que os utilizadores eprenem alterações na área de definições de proteção de exploração no Microsoft Defender Security Center.

## <a name="next-steps"></a>Próximos passos

[Política de segurança do ponto final para a ASR](../protect/endpoint-security-asr-policy.md)
