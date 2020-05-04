---
title: Utilize janelas de manutenção
titleSuffix: Configuration Manager
description: Utilize coleções e janelas de manutenção para gerir eficazmente os clientes no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714445"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Como utilizar janelas de manutenção no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As janelas de manutenção permitem definir um momento em que as operações do Gestor de Configuração podem ser realizadas numa recolha de dispositivos. Utiliza janelas de manutenção para ajudar a garantir que as mudanças de configuração do cliente ocorram durante períodos que não afetam a produtividade. A partir da versão 1806 do Gestor de Configuração, os utilizadores podem ver quando a sua próxima janela de manutenção é a partir do separador de estado de **instalação** no Centro de **Software**. <!--1358131-->

 As seguintes operações suportam janelas de manutenção:  

- Implementações de software  

- Implementações de atualizações de software  

- Avaliação e implementação das definições de compatibilidade  

- Implementações do sistema operativo  

- Implementações da sequência de tarefas  

  Configure as janelas de manutenção com uma data de início, um tempo de início e de chegada e um padrão de recorrência. A duração máxima de uma janela deve ser inferior a 24 horas. Por predefinição, os reinícios do computador causados por uma implementação não são permitidos fora de uma janela de manutenção, mas pode anular a predefinição. As janelas de manutenção afetam apenas o momento em que o programa de implantação funciona; aplicações configuradas para descarregar e executar localmente podem descarregar conteúdo fora da janela.  

  Quando um computador cliente é membro de uma coleção de dispositivos que tem uma janela de manutenção, um programa de implementação só funciona se o tempo máximo de execução permitido não exceder a duração configurada para a janela. Se o programa falhar a execução, é gerado um alerta e a implementação é executada novamente durante a próxima janela de manutenção agendada com tempo disponível.  

## <a name="using-multiple-maintenance-windows"></a>Utilizar várias janelas de manutenção  
 Quando um computador cliente é membro de várias coleções de dispositivos que têm janelas de manutenção, estas regras aplicam-se:  

- Se as janelas de manutenção não se sobrepuserem, são tratadas como duas janelas de manutenção independentes.  

- Se as janelas de manutenção se sobrepuserem, são tratadas como uma única janela de manutenção que engloba o período de tempo coberto por ambas as janelas de manutenção. Por exemplo, se duas janelas, cada uma de duração sobrepor em 30 minutos, a duração efetiva da janela de manutenção seria de 90 minutos.  

  Quando um utilizador inicia uma instalação de aplicação a partir do Centro de Software, a aplicação é instalada imediatamente, independentemente de quaisquer janelas de manutenção.  

  Se uma implementação de aplicação **Necessária** atingir o prazo de instalação durante as horas fora de expediente configuradas pelo utilizador no Centro de Software, a aplicação será instalada. 

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  Na consola De Configuração Manager, escolha**As Coleções**de Dispositivos de **Segurança e Conformidade.**>    

3.  Na lista de Coleções de **Dispositivos,** selecione uma coleção. Não é possível criar janelas de manutenção para a coleção **All Systems.**  

4.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

5.  No separador **Maintenance Windows** do nome **New** ** &lt;\> ** de recolha Properties, escolha o novo ícone.  

6.  Complete ** &lt;o\> novo** diálogo da Agenda.  

7.  Faça uma seleção a partir da **lista de lançamentos.**  

8.  Escolha **OK** e, em seguida, feche o nome ** &lt;\> ** de recolha Caixa de diálogo Properties.  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Usando powershell

PowerShell pode ser usado para configurar janelas de manutenção.  Para obter mais informações, consulte:

* [Set-CMJanela de manutenção](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Janela de manutenção get-CM](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [Janela de manutenção novo CM](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remover CMJanela de manutenção](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
