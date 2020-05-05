---
title: Utilize scripts de concha em dispositivos macOS no Microsoft Intune / Microsoft Docs
description: Crie, atribua, monitor e atire scripts de conchas para dispositivos macOS no Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5839154ab0c884e933e8d11055e745d54503433
ms.sourcegitcommit: 8a8378b685a674083bfb9fbc9c0662fb0c7dda97
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619547"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Utilize scripts de concha em dispositivos macOS em Intune (Pré-visualização pública)

> [!NOTE]
> Os scripts shell para dispositivos macOS estão atualmente em pré-visualização. Reveja a lista de [problemas conhecidos na pré-visualização](macos-shell-scripts.md#known-issues) antes de utilizar esta funcionalidade.

Utilize scripts shell para alargar as capacidades de gestão do dispositivo em Intune para além do que é suportado pelo sistema operativo macOS. 

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que os seguintes pré-requisitos são cumpridos ao compor scripts de conchae atribuindo-os aos dispositivos macOS. 
 - Os dispositivos estão a executar o macOS 10.12 ou mais tarde.
 - Os dispositivos são geridos pela Intune. 
 - Os scripts `#!` da concha começam e devem `#!/bin/sh` `#!/usr/bin/env zsh`estar num local válido, como ou .
 - São instalados intérpretes de linha de comando para as conchas aplicáveis.

## <a name="important-considerations-before-using-shell-scripts"></a>Considerações importantes antes de usar scripts de concha
 - Os scripts shell exigem que o agente de gestão Microsoft Intune seja instalado com sucesso no dispositivo macOS. Para mais informações, consulte o agente de [gestão Microsoft Intune para o macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Os scripts de concha saem em paralelo em dispositivos como processos separados.
 - Os scripts shell que são executados como o utilizador inscrito serão executados para todas as contas de utilizador atualmente assinadas no dispositivo no momento da execução.
 - É necessário um utilizador final para iniciar sessão no dispositivo para executar scripts em funcionamento como utilizador inscrito.
 - São necessários privilégios de utilizador raiz se o script exigir alterações que uma conta de utilizador padrão não pode.
 - Os scripts shell tentarão executar com mais frequência do que a frequência de script escolhida para determinadas condições, como se o disco estiver cheio, se o local de armazenamento for adulterado, se a cache local for eliminada ou se o dispositivo Mac reiniciar.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Criar e atribuir uma política de script shell
1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > **macOS** > **Scripts** > **Adicionar**.
3. No Básico, introduza as **seguintes**propriedades e selecione **Seguinte:**
   - **Nome**: Introduza um nome para o script da concha.
   - **Descrição**: Introduza uma descrição para o script da concha. Esta definição é opcional, mas recomendada.
4. Nas **definições do Script,** introduza as seguintes propriedades e selecione **Seguinte:**
   - **Upload script**: Navegue para o script da concha. O ficheiro do guião deve ter menos de 200 KB de tamanho.
   - **Executar o script como utilizador inscrito**: Selecione **Sim** para executar o script com as credenciais do utilizador no dispositivo. Escolha **Não** (predefinido) para executar o script como utilizador de raiz. 
   - **Ocultar notificações de script em dispositivos:** Por padrão, as notificações do script são mostradas para cada script que é executado. Os utilizadores finais vêem que um *TI está a configurar a notificação* do seu computador a partir de Intune em dispositivos macOS.
   - **Frequência do script:** Selecione quantas vezes o script deve ser executado. Escolha **Não configurado** (predefinido) para executar um script apenas uma vez.
   - **Número máximo de vezes para voltar a tentar se o guião falhar:** Selecione quantas vezes o script deve ser executado se devolver um código de saída não zero (zero significando sucesso). Escolha **Não configurado** (predefinido) para não voltar a tentar quando um script falha.
5. Nas **tags de Âmbito,** adicione opcionalmente etiquetas de âmbito para o script e selecione **Next**. Pode utilizar etiquetas de mira para determinar quem pode ver scripts em Intune. Para mais detalhes sobre etiquetas de âmbito, consulte [Use o controlo de acesso baseado em funções e as etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .
6. Selecione **Tarefas** > **Selecione grupos para incluir**. É apresentada uma lista existente de grupos da AD Azure. Selecione um ou mais grupos de dispositivos que incluam os utilizadores cujos dispositivos macOS devem receber o script. Escolha **Selecionar**. Os grupos que escolher estão na lista e receberão a sua política de script.
   > [!NOTE]
   > - Os scripts shell em Intune só podem ser atribuídos a grupos de segurança de dispositivos AD Azure. A atribuição do grupo de utilizadores não é suportada na pré-visualização. 
   > - Atualizar as atribuições para scripts shell também atualiza atribuições para o agente de [gestão Microsoft Intune para o macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
7. Em **Review + add,** é mostrado um resumo das definições configuradas. Selecione **Adicionar** para salvar o script. Quando selecionar **Adicionar,** a política de scripts é implementada para os grupos que escolheu.

O guião que criou agora aparece na lista de guiões. 

## <a name="monitor-a-shell-script-policy"></a>Monitorize uma política de script shell
Pode monitorizar o estado de execução de todos os scripts atribuídos para utilizadores e dispositivos, escolhendo um dos seguintes relatórios:
- **Scripts** > **selecionam o script para monitorizar** > o**estado do Dispositivo**
- **Scripts** > **selecionam o script para monitorizar** > o estado do**utilizador**

>[!IMPORTANT]
> Independentemente da frequência do **Script**selecionada, o estado de execução do script é reportado apenas na primeira vez que um script é executado. O estado da execução do script não é atualizado em execuções subsequentes. No entanto, os scripts atualizados são tratados como novos scripts e reportarão novamente o estado de execução.

Uma vez executado um script, devolve um dos seguintes estatutos:
- Um estado de execução de script de **Failed** indica que o script devolveu um código de saída não-zero ou o script está mal formado. 
- Um estado de execução de script de **Sucesso** indicou que o script devolveu zero como código de saída. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Políticas de script de concha macOS de resolução de problemas usando a recolha de registos

Pode recolher registos de dispositivos para ajudar a resolver problemas de scripts em dispositivos macOS. 

### <a name="requirements-for-log-collection"></a>Requisitos para recolha de registos
São necessários os seguintes itens para recolher registos num dispositivo macOS:
- Deve especificar o caminho completo do ficheiro de registo absoluto.
- Os caminhos dos ficheiros devem ser separados utilizando apenas um ponto evío (;).
- O tamanho máximo de recolha de registos para carregar é de 60 MB (comprimido) ou 25 ficheiros, o que ocorrer primeiro.
- Os tipos de ficheiros que são permitidos para a recolha de registos incluem as seguintes extensões: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

#### <a name="collect-device-logs"></a>Recolher registos de dispositivos
1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. No **estado do Dispositivo** ou no relatório do estado do **utilizador,** selecione um dispositivo.
3. Selecione **Registos De Recolha**, forneça os caminhos das pastas dos ficheiros de registo separados apenas por um ponto e vírgula (;) sem espaços ou linhas novas entre caminhos.<br>Por exemplo, devem ser escritos `/Path/to/logfile1.zip;/Path/to/logfile2.log`múltiplos caminhos como . 

   >[!IMPORTANT]
   > Vários caminhos de ficheiros de registo separados usando vírvia, período, marcas de novalinha ou de aspas com ou sem espaços resultarão em erro de recolha de registos. Os espaços também não são permitidos como separadores entre caminhos.

4. Selecione **OK**. Os registos são recolhidos da próxima vez que o agente de gestão Intune no dispositivo entrar em Intune. Este check-in ocorre geralmente a cada 8 horas.

   >[!NOTE]
   > 
   > - Os registos recolhidos são encriptados no dispositivo, transmitidos e armazenados no armazenamento do Microsoft Azure durante 30 dias. Os registos armazenados são desencriptados a pedido e descarregados através do centro de administração do Microsoft Endpoint Manager.
   > - Para além dos registos especificados pela administração, os registos do agente `/Library/Logs/Microsoft/Intune` `~/Library/Logs/Microsoft/Intune`de gestão Intune também são recolhidos destas pastas: e . Os nomes dos `IntuneMDMDaemon date--time.log` ficheiros de registo do agente são e `IntuneMDMAgent date--time.log`. 
   > - Se faltar algum ficheiro especificado pela administração ou tiver a extensão de `LogCollectionInfo.txt`ficheiro errada, encontrará estes nomes de ficheirolistados em .     

### <a name="log-collection-errors"></a>Erros de recolha de log
A recolha de registos pode não ser bem sucedida devido a qualquer uma das seguintes razões previstas na tabela abaixo. Para resolver estes erros, siga as etapas de reparação.

| Código de erro (hex) | Código de erro (dez) | Mensagem de erro | Passos de reparação |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | O tamanho do ficheiro de registo não pode exceder 60 MB. | Certifique-se de que os troncos comprimidos têm menos de 60 MB de tamanho. |
| 0X87D300D1 | 2016214831 | O caminho de ficheiro de registo fornecido deve existir. A pasta do utilizador do sistema é uma localização inválida para ficheiros de registo. | Certifique-se de que o caminho de ficheiro fornecido é válido e acessível. |
| 0X87D300D2 | 2016214830 | O upload do ficheiro de recolha de registo falhou devido à expiração do URL de upload. | Tente novamente a ação de **registos da Collect.** |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | O upload do ficheiro de recolha de registo falhou devido a falha de encriptação. Retry log upload. | Tente novamente a ação de **registos da Collect.** |
| | 2016214828 | O número de ficheiros de registo ultrapassou o limite permitido de 25 ficheiros. | Apenas 25 ficheiros de registo podem ser recolhidos de cada vez. |
| 0X87D300D6 | 2016214826 | O upload do ficheiro de recolha de registo falhou devido a um erro de fecho. Retry log upload. | Tente novamente a ação de **registos da Collect.** |
| | 2016214740 | Os registos não podiam ser encriptados porque os troncos comprimidos não foram encontrados. | Tente novamente a ação de **registos da Collect.** |
| | 2016214739 | Os troncos foram recolhidos, mas não puderam ser armazenados. | Tente novamente a ação de **registos da Collect.** |

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Porque é que os scripts de conchas não estão a funcionar no dispositivo?
Pode haver várias razões:
* O agente pode precisar de fazer o check-in para receber scripts novos ou atualizados. Este processo de check-in ocorre a cada 8 horas e é diferente do check-in do MDM. Certifique-se de que o dispositivo está acordado e ligado a uma rede para um check-in de agente bem sucedido e aguarde que o agente faça o check-in.
* O agente não pode ser instalado. Verifique se o agente `/Library/Intune/Microsoft Intune Agent.app` está instalado no dispositivo macOS.
* O agente pode não estar num estado saudável. O agente tentará recuperar durante 24 horas, remover-se-á e reinstalar-se-á se os scripts de concha ainda estiverem atribuídos.

### <a name="how-frequently-is-script-run-status-reported"></a>Com que frequência é reportado o estado do script?
O estado de execução do script é reportado à Consola de Administrador do Microsoft Endpoint Manager assim que a execução do script estiver concluída. Se um script estiver programado para ser executado periodicamente numa frequência definida, apenas reporta o estado da primeira vez que funciona.

### <a name="when-are-shell-scripts-run-again"></a>Quando é que os scripts da concha são executados de novo?
Um script é executado novamente apenas quando o **número max de vezes para retentar se** o script falhar a definição é configurado e o script falha em execução. Se o **número máximo de vezes para voltar a tentar se** o script falhar não estiver configurado e um script falhar em execução, não será executado novamente e o estado de execução será reportado como **falhado**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Que permissões de papéis intune são necessárias para scripts de concha?
A sua função de insintonização atribuída requer permissões de **configuração** do Dispositivo para eliminar, atribuir, criar, atualizar ou ler scripts de concha.

## <a name="microsoft-intune-management-agent-for-macos"></a>Agente de gestão da Microsoft Intune para macOS
 ### <a name="why-is-the-agent-required"></a>Por que o agente é necessário?
O agente de gestão Microsoft Intune é necessário para ser instalado em dispositivos macOS geridos de forma a permitir capacidades avançadas de gestão de dispositivos que não são suportadas pelo sistema operativo macOS nativo.
 
 ### <a name="how-is-the-agent-installed"></a>Como é instalado o agente?
 O agente é instalado automaticamente e silenciosamente em dispositivos macOS geridos por Intune a que atribui pelo menos um script de concha no Microsoft Endpoint Manager Admin Center. O agente é `/Library/Intune/Microsoft Intune Agent.app` instalado quando aplicável e não aparece nas**Aplicações** **Finder** > em dispositivos macOS. O agente aparece `IntuneMdmAgent` como no Monitor de **Atividade** quando funciona em dispositivos macOS.

### <a name="what-does-the-agent-do"></a>O que faz o agente?
 - O agente autentica silenciosamente os serviços Intune antes de fazer o check-in para receber scripts de concha atribuídos para o dispositivo macOS.
 - O agente recebe scripts de concha atribuídos e executa os scripts com base no horário configurado, tentativas de retry, definições de notificação e outras definições definidas pelo administrador.
 - O agente verifica scripts novos ou atualizados com serviços Intune geralmente a cada 8 horas. Este processo de check-in é independente do check-in do MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Como posso iniciar o check-in de um agente de um Mac?
Num Mac gerido que tenha o agente **Terminal**instalado, `sudo killall IntuneMdmAgent` terminal aberto, `IntuneMdmAgent` execute o comando para encerrar o processo. O `IntuneMdmAgent` processo recomeçará imediatamente, o que iniciará um check-in com intune.

Em alternativa, pode fazer o seguinte:
1. Open **Activity Monitor** > **Ver** > *selecionar todos os **processos**.* 
2. Procurar processos `IntuneMdmAgent`nomeados. 
3. Desista do processo que corre para o utilizador **de raiz.** 

> [!NOTE]
> A ação **de definições de Check** no Portal da Empresa e a ação **Sync** para dispositivos na Consola de Administrador do Microsoft Endpoint Manager inicia um check-in do MDM e não obriga um check-in de agente.

 ### <a name="when-is-the-agent-removed"></a>Quando é que o agente é removido?
 Existem várias condições que podem fazer com que o agente seja removido do dispositivo, tais como:
 - Os scripts da shell já não estão atribuídos ao dispositivo. 
 - O dispositivo macOS já não é gerido.
 - O agente encontra-se em estado irrecuperável por mais de 24 horas (hora de despertar do dispositivo).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Como desligar os dados de utilização enviados para a Microsoft para scripts de concha?
 Para desativar os dados de utilização enviados para a Microsoft a partir do agente de gestão Intune, abra o Portal da Empresa e selecione **Menu** > **Preferences** > *desmarca "permitir que a Microsoft recolha dados de utilização".* Isto irá desligar os dados de utilização enviados tanto para o agente como para o Portal da Empresa.

## <a name="known-issues"></a>Problemas conhecidos
- **Atribuição do grupo de utilizadores:** Os scripts shell atribuídos a grupos de utilizadores não se aplicam aos dispositivos. A atribuição do grupo de utilizadores não é suportada atualmente na pré-visualização. Utilize a atribuição do grupo do dispositivo para atribuir scripts.
- **Recolher registos:** A ação "Recolher registos" é visível. Mas quando a recolha de registos é tentada, mostra "um erro ocorrido" e não captura registos. A recolha de registos não é suportada na pré-visualização.
- **Sem estado de execução** de script: No caso improvável de um script ser recebido no dispositivo e o dispositivo ficar offline antes de o estado de execução ser reportado, o dispositivo não reportará o estado de execução do script na consola de administração.
- **Relatório de estado do utilizador:** Existe uma questão de relatório vazio. No [Microsoft Endpoint Manager Admin Center,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Monitor**. O estado do utilizador mostra um relatório vazio.

## <a name="next-steps"></a>Passos seguintes

- [Criar uma política de conformidade no Microsoft Intune](..\protect\create-compliance-policy.md)
