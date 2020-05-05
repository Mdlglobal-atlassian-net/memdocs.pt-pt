---
title: Modo de aprovisionamento
titleSuffix: Configuration Manager
description: Conheça o modo de provisionamento do cliente durante a sequência de tarefas do Gestor de Configuração.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723951"
---
# <a name="provisioning-mode"></a>Modo de aprovisionamento

*Aplica-se a: Gestor de Configuração (ramo atual)*

Durante uma sequência de tarefas de implementação de SISTEMA, o Gestor de Configuração coloca o cliente no modo de provisionamento. (Uma sequência de tarefas de implementação do OS inclui a atualização no local para o Windows 10.) Neste estado, o cliente não processa a política a partir do site. Este comportamento permite que a sequência de tarefas seja executada sem o risco de implementações adicionais em execução no cliente. Quando a sequência de tarefas completa, ou o sucesso ou a falha manipulada, sai do modo de provisionamento do cliente.

Se a sequência de tarefa falhar inesperadamente, o cliente pode ser deixado no modo de provisionamento. Por exemplo, se o dispositivo recomeçar no meio do processamento da sequência de tarefas, e não conseguir recuperar. Um administrador deve identificar e fixar manualmente clientes neste estado.


## <a name="manually-remove-provisioning-mode"></a>Remova manualmente o modo de provisionamento

Se um cliente for deixado em modo de provisionamento, utilize este processo manual para devolver o cliente ao funcionamento normal.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Uma das alterações feitas por este método wmi é definir um valor de registo, mas também faz outras alterações. Mudar o valor do registo não tira totalmente o cliente do modo de provisionamento. Se editar manualmente o registo, o cliente poderá apresentar comportamentos inesperados.  


## <a name="client-provisioning-mode-timeout"></a>Tempo de tempo de fornecimento de clientes

A partir da versão 1902, a sequência de tarefas define um carimbo de tempo quando coloca o cliente em modo de provisionamento. A cada 60 minutos, um cliente no modo de provisionamento verifica a duração do tempo desde a hora marcada. Se estiver em modo de provisionamento há mais de 48 horas, o cliente sai automaticamente do modo de provisionamento e reinicia o seu processo.

48 horas é o valor de tempo de tempo de funcionamento do modo de fornecimento predefinido. Pode ajustar este temporizador num dispositivo, definindo o valor **ProvisioningMaxMinutes** na seguinte tecla de registo: `HKLM\Software\Microsoft\CCM\CcmExec`. Se este valor não existir `0`ou for, o cliente utiliza o padrão de 48 horas.

O prazo **ProvisioningTime** está localizado na seguinte tecla `HKLM\Software\Microsoft\CCM\CcmExec`de registo: . O carimbo tem um valor da última vez que a máquina entrou no modo de provisionamento. O formato é época (carimbo de tempo Unix) e está na UTC.

Esta marca de tempo também é redefinida para o tempo atual quando coloca manualmente a máquina no modo de provisionamento utilizando o seguinte comando:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Diagramas de fluxo de processo

Estes diagramas mostram o fluxo de processo para a sequência de tarefas e o cliente.

### <a name="task-sequence"></a>Sequência de tarefas

O diagrama seguinte mostra como a sequência de tarefas define o modo de fornecimento:

![Diagrama de fluxo do modo de definição de sequência de tarefas](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Reparação de clientes

O diagrama seguinte mostra como o cliente sai do modo de provisionamento:

![Diagrama de fluxo do modo de fornecimento de saída do cliente](media/3197824-client-flow.png)


## <a name="see-also"></a>Consulte também

[Configurar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Atualizar Sistema Operativo](task-sequence-steps.md#BKMK_UpgradeOS)
