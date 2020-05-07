---
title: Definições de política antivírus do Windows 10 para o Antivírus Do Microsoft Defender para Intune [ Microsoft Docs
description: Consulte uma lista das definições no perfil Antivírus Microsoft Defender para windows 10. Pode configurar estas definições como parte da política antivírus de segurança endpoint no Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/05/2020
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
ms.openlocfilehash: 7d8ea221b6c1768055e3ca1839c20ed64e2e3838
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802026"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Definições para a política antivírus do Microsoft Defender do Windows 10 no Microsoft Intune

Ver as definições da política Antivírus que pode configurar para o perfil Antivírus Microsoft Defender para windows 10 no Microsoft Intune.

## <a name="cloud-protection"></a>Proteção de nuvens

- **Ligue a proteção entregue em nuvem**  
  CSP: [Permitir proteção em nuvem](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Por padrão, o Defender nos dispositivos de desktop do Windows 10 envia informações à Microsoft sobre quaisquer problemas que encontre. A Microsoft analisa essa informação para saber mais sobre problemas que afetam o seu e outros clientes, para oferecer soluções melhoradas.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - A proteção entregue em nuvem está ligada.  Os utilizadores do dispositivo não podem alterar esta definição.

- **Nível de proteção entregue em nuvem**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure o quão agressivo o Antivírus defensor está em bloquear e digitalizar ficheiros suspeitos.
  - **Não configurado** *(predefinido*) - Padrão Defender blocking level.
  - **High** - Bloqueie agressivamente desconhecidos ao mesmo tempo que otimiza o desempenho do cliente, o que inclui uma maior chance de falsos positivos.
  - **High plus** - Bloqueie agressivamente as incógnitas e aplique medidas de proteção adicionais que possam ter impacto no desempenho do cliente.
  - **Tolerância zero** - Bloqueie todos os ficheiros executáveis desconhecidos.

- **Nuvem de defensor prolongou o tempo em segundos**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  O Antivírus Defensor bloqueia automaticamente ficheiros suspeitos durante 10 segundos para que possa digitalizar os ficheiros na nuvem para se certificar de que estão seguros. Com esta definição, pode adicionar até 50 segundos adicionais a este intervalo.

## <a name="microsoft-defender-antivirus-exclusions"></a>Exclusões antivírus do Microsoft Defender

Para cada definição deste grupo, pode expandir a definição, selecionar **Adicionar,** e depois especificar um valor para a exclusão.

- **Processos de defesa para excluir**  
  CSP: [Processos Excluídos](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Especifique uma lista de ficheiros abertos por processos a ignorar durante uma verificação. O processo em si não está excluído da tomografia.

- **Extensões de ficheiros para excluir de exames e proteção em tempo real**  
  CSP: [Exclusões](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Especifique uma lista de extensões do tipo de ficheiro para ignorar durante uma verificação.

- **Defender ficheiros e pastas para excluir**  
  CSP: [Caminhos Excluídos](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Especifique uma lista de ficheiros e caminhos de diretório para ignorar durante uma verificação.

## <a name="real-time-protection"></a>Proteção em tempo real

- **Ativar a proteção em tempo real**  
  CSP: [Permitir monitorização em tempo real](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Exija que o Defender em dispositivos de ambiente de trabalho do Windows 10 utilize a funcionalidade de Monitorização em tempo real.
  - **Não configurado** *(predefinido)*- A definição é restaurada à defeito do sistema
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Impor o uso da monitorização em tempo real. Os utilizadores do dispositivo não podem alterar esta definição.

- **Ativar a proteção do acesso**  
  CSP: [Permitir a proteção de acessos](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configure a proteção contra vírus que seja continuamente ativa, em oposição à procura.

  - **Não configurado** *(predefinido)*- Esta política não altera o estado desta definição num dispositivo. O estado existente no dispositivo permanece inalterado.
  - **Não** - Bloquear a proteção de acesso nos dispositivos. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - A Proteção de Acesso está ativa em dispositivos.

- **Monitorização de ficheiros de entrada e saída**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configure esta definição para determinar qual o ficheiro NTFS e a atividade do programa monitorizadas.
  - **Monitorize todos os ficheiros** *(predefinido)*
  - **Só monitorizar os ficheiros de entrada**
  - **Só monitorizar ficheiros de saída**

- **Ativar a monitorização do comportamento**  
  CSP: [Permitir a Monitorização do Comportamento](https://go.microsoft.com/fwlink/?linkid=2114048)

  Por predefinição, os dispositivos de desktop Do Windows 10 utilizam a funcionalidade De Monitorização de Comportamentos.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Impor o uso da monitorização do comportamento em tempo real. Os utilizadores do dispositivo não podem alterar esta definição.

- **Ativar a proteção da rede**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Proteja os utilizadores de dispositivos que utilizem qualquer aplicação de aceder a esquemas de phishing, sites de hospedagem de exploração e conteúdo malicioso na Internet. A proteção inclui impedir que os navegadores de terceiros se conectem a sites perigosos.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - A proteção da rede está ligada. Os utilizadores do dispositivo não podem alterar esta definição.

- **Scaneie todos os ficheiros e anexos descarregados**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configure o Defender para digitalizar todos os ficheiros e anexos descarregados.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - O Defender digitaliza todos os ficheiros e anexos descarregados. Os utilizadores do dispositivo não podem alterar esta definição.

- **Scanscripts que são usados nos navegadores da Microsoft**  
  CSP: [Permitir a digitalização](https://go.microsoft.com/fwlink/?linkid=2114054) do ScriptS

  Configure defender para digitalizar scripts.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Defender digitaliza guiões. Os utilizadores do dispositivo não podem alterar esta definição.

- **Scan ficheiros de rede**  
  CSP: [Permitir Ficheiros de Redes](https://go.microsoft.com/fwlink/?linkid=2114049&) de Digitalização

  Configure o Defender para digitalizar ficheiros de rede.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Ligue a digitalização dos ficheiros da rede. Os utilizadores do dispositivo não podem alterar esta definição.

- **E-mails de digitalização**  
  CSP: [Permitir emailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configure defender para digitalizar o e-mail de entrada.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Ligue a digitalização de e-mails. Os utilizadores do dispositivo não podem alterar esta definição.

## <a name="remediation"></a>Remediação

- **Número de dias (0-90) para manter malware em quarentena**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Especifique alguns dias de zero a 90 que o sistema armazena itens em quarentena antes de serem removidos automaticamente. Um valor de zero mantém os itens em quarentena e não os remove automaticamente.

- **Submeter consentimento de amostras**  

  - **Não configurado** *(predefinido)*
  - **Enviar amostras seguras automaticamente**
  - **Sempre rápido**
  - **Nunca enviar**
  - **Enviar todas as amostras automaticamente**

- **Ação para assumir aplicações potencialmente indesejadas**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Especifique o nível de deteção de aplicações potencialmente indesejadas (APA). O Defender alerta os utilizadores quando o software potencialmente indesejado está a ser descarregado ou tenta instalar-se num dispositivo.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema, que é a Proteção DE PUA OFF.
  - **Desativar**
  - **Ativar** - Os itens detetados estão bloqueados e mostram na história juntamente com outras ameaças.
  - **Modo** de auditoria - Defender deteta aplicações potencialmente indesejadas, mas não toma medidas. Pode rever informações sobre as aplicações que o Defender teria tomado medidas contra a procura de eventos criados pela Defender no Observador de Eventos.

- **Ações para ameaças detetadas**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Especifique a ação que o Defender toma para o malware detetado com base no nível de ameaça do malware.
  
  O Defender classifica o malware que deteta como um dos seguintes níveis de gravidade:
  - **Baixa gravidade**
  - **Gravidade moderada**
  - **Alta severidade**
  - **Gravidade severa**

  Para cada nível, especifique a ação a tomar. O padrão para cada nível de gravidade não está *configurado*.

  - **Não configurado**
  - **Clean** - O serviço tenta recuperar ficheiros e tentar desinfetar.
  - **Quarentena** - Move ficheiros para a quarentena.
  - **Remover** - Remove ficheiros do dispositivo.
  - **Permitir** - Permite o ficheiro e não toma outras ações.
  - **Utilizador definido** - O utilizador do dispositivo toma a decisão sobre que medidas tomar.
  - **Bloco** - Bloqueia a execução de ficheiros.

## <a name="scan"></a>Digitalizar

- **Analisar ficheiros de arquivo**  
  CSP: [Permitir a digitalização do Arquivo](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configure o Defender para digitalizar ficheiros de arquivo, como ficheiros ZIP ou CAB.

  - **Não configurado** *(predefinido*) - A definição retorna ao predefinido do cliente, que é digitalizar ficheiros arquivados, no entanto o utilizador pode desativar isto.
Saiba mais
  - **Não- Arquivos** não são digitalizados. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Ativar digitalizações de ficheiros de arquivo. Os utilizadores do dispositivo não podem alterar esta definição.

- **Use baixa prioridade da CPU para exames agendados**  
  CSP: [EnablelowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configure a prioridade do CPU para as digitalizações programadas.
  - **Não configurado** *(predefinido*) - A definição retorna à predefinição do sistema, na qual não são feitas alterações à prioridade do CPU.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - A baixa prioridade da CPU será usada durante as verificações programadas. Os utilizadores do dispositivo não podem alterar esta definição.

- **Desativar a captura completa**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configure as tomografias para os exames completos programados. Uma tomografia é uma tomografia que é iniciada porque uma varredura regular foi perdida. Normalmente, estas tomografias programadas são perdidas porque o computador foi desligado na hora programada.

  - **Não configurado** *(predefinido*) - A definição é devolvida ao padrão do cliente, que é para permitir a captura de digitalizações completas, no entanto o utilizador pode desligá-los.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - As tomografias de atualização para exames completos programados são executadas e o utilizador não pode desativá-los. Se um computador estiver offline para duas varreduras programadas consecutivas, uma varredura de recuperação é iniciada da próxima vez que alguém entrar no computador. Se não houver uma varredura programada configurada, não haverá nenhuma varredura de recuperação. Os utilizadores do dispositivo não podem alterar esta definição.

- **Desativar a sondagem rápida da catchup**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configure as análises de recuperação para exames rápidos programados. Uma tomografia é uma tomografia que é iniciada porque uma varredura regular foi perdida. Normalmente, estas tomografias programadas são perdidas porque o computador foi desligado na hora programada.

  - **Não configurado** *(predefinido*) - A definição é devolvida ao padrão do cliente, que é para permitir a captação de exames rápidos, no entanto o utilizador pode desligá-los.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - As análises de recuperação para exames rápidos programados são executadas e o utilizador não pode desativá-los. Se um computador estiver offline para duas varreduras programadas consecutivas, uma varredura de recuperação é iniciada da próxima vez que alguém entrar no computador. Se não houver uma varredura programada configurada, não haverá nenhuma varredura de recuperação. Os utilizadores do dispositivo não podem alterar esta definição.

- **Limite de utilização do CPU por digitalização**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Especifique como um por cento de zero a 100, o fator médio de carga cpu para a varredura do Defender.

- **Scan mapeado unidades de rede durante a varredura completa**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configure defender para digitalizar unidades de rede mapeadas.

  - **Não configurado** *(predefinido*) - A definição é restaurada à defeito do sistema, que desativa a digitalização das unidades de rede mapeadas.
  - **Não** - A regulação está desativada. Os utilizadores do dispositivo não podem alterar esta definição.
  - **Sim** - Ative digitalizações de unidades de rede mapeadas. Os utilizadores do dispositivo não podem alterar esta definição.

- **Executar varredura rápida diária em**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Selecione a hora do dia que o Defender faz exames rápidos.
  Por padrão, isto não está **configurado**

- **Tipo de digitalização**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Selecione o tipo de digitalização que o Defender executa.

  - **Não configurado** *(predefinido)*
  - **Sondagem rápida**
  - **Análise completa**

- **Dia da semana para fazer uma varredura programada**  
  - **Não configurado** *(predefinido)*

- **Hora do dia para fazer uma varredura programada**  
  - **Não configurado** *(predefinido)*

- **Verifique as atualizações de assinatura antes de executar o exame**  
  - **Não configurado** *(predefinido)*
  - **Não**
  - **Sim**

## <a name="updates"></a>Atualizações

- **Insira quantas vezes (0-24 horas) para verificar se há atualizações de inteligência de segurança**  
  CSP: [Intervalo de Atualização de Assinaturas](https://go.microsoft.com/fwlink/?linkid=2113936)

  Especifique o intervalo de zero a 24 (em horas) que é utilizado para verificar se há assinaturas. Um valor de zero resulta em nenhum cheque para novas assinaturas. Um valor de 2 verificará a cada duas horas, e assim por diante.

## <a name="user-experience"></a>Experiência de utilizador

- **Permitir o acesso do utilizador à aplicação Microsoft Defender**  
  CSP: [Permitir o acesso userui](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Não configurado** *(predefinido)*- A definição devolve ao padrão do cliente em que ui e notificações são permitidas.
  - **Não** - A Interface de Utilizador do Defender (UI) é inacessível e os produtos de notificação suprimidos.
  - **Sim**

