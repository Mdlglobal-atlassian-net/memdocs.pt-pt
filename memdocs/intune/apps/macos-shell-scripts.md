---
title: Utilize scripts de concha em dispositivos macOS no Microsoft Intune / Microsoft Docs
description: Crie, atribua, monitor e atire scripts de conchas para dispositivos macOS no Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
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
ms.openlocfilehash: ba099e3614c11e10ce4cd9ae94668a1648bfc150
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808051"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Utilize scripts de concha em dispositivos macOS em Intune (Pré-visualização pública)

> [!NOTE]
> Os scripts shell para dispositivos macOS estão atualmente em pré-visualização. Reveja a lista de [problemas conhecidos na pré-visualização](macos-shell-scripts.md#known-issues) antes de utilizar esta funcionalidade.

Utilize scripts shell para alargar as capacidades de gestão do dispositivo em Intune para além do que é suportado pelo sistema operativo macOS. 

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que os seguintes pré-requisitos são cumpridos ao compor scripts de conchae atribuindo-os aos dispositivos macOS. 
 - Os dispositivos estão a executar o macOS 10.12 ou mais tarde.
 - Os dispositivos são geridos pela Intune. 
 - Os scripts shell começam com `#!` e devem estar num local válido, como `#!/bin/sh` ou `#!/usr/bin/env zsh`.
 - São instalados intérpretes de linha de comando para as conchas aplicáveis.

## <a name="important-considerations-before-using-shell-scripts"></a>Considerações importantes antes de usar scripts de concha
 - Os scripts shell requerem que o Microsoft Intune MDM Agent seja instalado com sucesso no dispositivo macOS. Para mais informações, consulte [o Microsoft Intune MDM Agent para macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
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
6. Selecione **Atribuições** > **Selecione grupos para incluir**. É apresentada uma lista existente de grupos da AD Azure. Selecione um ou mais grupos de dispositivos que incluam os utilizadores cujos dispositivos macOS devem receber o script. Clique em **Selecionar**. Os grupos que escolher estão na lista e receberão a sua política de script.
   > [!NOTE]
   > - Os scripts shell em Intune só podem ser atribuídos a grupos de segurança de dispositivos AD Azure. A atribuição do grupo de utilizadores não é suportada na pré-visualização. 
   > - Atualizar as atribuições para scripts de concha também atualiza atribuições para [o Microsoft Intune MDM Agent for macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
7. Em **Review + add,** é mostrado um resumo das definições configuradas. Selecione **Adicionar** para salvar o script. Quando selecionar **Adicionar,** a política de scripts é implementada para os grupos que escolheu.

O guião que criou agora aparece na lista de guiões. 

## <a name="monitor-a-shell-script-policy"></a>Monitorize uma política de script shell
Pode monitorizar o estado de execução de todos os scripts atribuídos para utilizadores e dispositivos, escolhendo um dos seguintes relatórios:
- **Scripts** > **selecionar o script para monitorizar o** estado do **dispositivo** > 
- **Scripts** > **selecione o script para monitorizar** o estado do **utilizador** > 

>[!IMPORTANT]
> Independentemente da frequência do **Script**selecionada, o estado de execução do script é reportado apenas na primeira vez que um script é executado. O estado da execução do script não é atualizado em execuções subsequentes. No entanto, os scripts atualizados são tratados como novos scripts e reportarão novamente o estado de execução.

Uma vez executado um script, devolve um dos seguintes estatutos:
- Um estado de execução de script de **Failed** indica que o script devolveu um código de saída não-zero ou o script está mal formado. 
- Um estado de execução de script de **Sucesso** indicou que o script devolveu zero como código de saída. 

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Porque é que os scripts de conchas não estão a funcionar no dispositivo?
Pode haver várias razões:
* O agente pode precisar de fazer o check-in para receber scripts novos ou atualizados. Este processo de check-in ocorre a cada 8 horas e é diferente do check-in do MDM. Certifique-se de que o dispositivo está acordado e ligado a uma rede para um check-in de agente bem sucedido e aguarde que o agente faça o check-in.
* O agente não pode ser instalado. Verifique se o agente está instalado em `/Library/Intune/Microsoft Intune Agent.app` no dispositivo macOS.
* O agente pode não estar num estado saudável. O agente tentará recuperar durante 24 horas, remover-se-á e reinstalar-se-á se os scripts de concha ainda estiverem atribuídos.

### <a name="how-frequently-is-script-run-status-reported"></a>Com que frequência é reportado o estado do script?
O estado de execução do script é reportado à Consola de Administrador do Microsoft Endpoint Manager assim que a execução do script estiver concluída. Se um script estiver programado para ser executado periodicamente numa frequência definida, apenas reporta o estado da primeira vez que funciona.

### <a name="when-are-shell-scripts-run-again"></a>Quando é que os scripts da concha são executados de novo?
Um script é executado novamente apenas quando o **número max de vezes para retentar se** o script falhar a definição é configurado e o script falha em execução. Se o **número máximo de vezes para voltar a tentar se** o script falhar não estiver configurado e um script falhar em execução, não será executado novamente e o estado de execução será reportado como **falhado**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Que permissões de papéis intune são necessárias para scripts de concha?
A sua função de insintonização atribuída requer permissões de **configuração** do Dispositivo para eliminar, atribuir, criar, atualizar ou ler scripts de concha.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>Microsoft Intune MDM Agent for macOS
 ### <a name="why-is-the-agent-required"></a>Por que o agente é necessário?
 O Microsoft Intune MDM Agent é necessário para ser instalado em dispositivos macOS geridos de forma a permitir capacidades avançadas de gestão de dispositivos que não são suportadas pelo sistema operativo macOS nativo.
 
 ### <a name="how-is-the-agent-installed"></a>Como é instalado o agente?
 O agente é instalado automaticamente e silenciosamente em dispositivos macOS geridos por Intune a que atribui pelo menos um script de concha no Microsoft Endpoint Manager Admin Center. O agente é instalado em `/Library/Intune/Microsoft Intune Agent.app` quando aplicável e não aparece no **Finder** > **Aplicações** em dispositivos macOS. O agente aparece como `IntuneMdmAgent` no Monitor de **Atividade** quando funciona em dispositivos macOS.

### <a name="what-does-the-agent-do"></a>O que faz o agente?
 - O agente autentica silenciosamente os serviços Intune antes de fazer o check-in para receber scripts de concha atribuídos para o dispositivo macOS.
 - O agente recebe scripts de concha atribuídos e executa os scripts com base no horário configurado, tentativas de retry, definições de notificação e outras definições definidas pelo administrador.
 - O agente verifica scripts novos ou atualizados com serviços Intune geralmente a cada 8 horas. Este processo de check-in é independente do check-in do MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Como posso iniciar o check-in de um agente de um Mac?
Num Mac gerido que tenha o agente instalado, **terminal**aberto, execute o comando `sudo killall IntuneMdmAgent` para pôr termo ao processo `IntuneMdmAgent`. O processo `IntuneMdmAgent` recomeçará imediatamente, o que iniciará um check-in com intune.

Em alternativa, pode fazer o seguinte:
1. Monitor de **atividade** aberta > **Ver** > *selecionar todos os **processos**.* 
2. Procurar processos chamados `IntuneMdmAgent`. 
3. Desista do processo que corre para o utilizador **de raiz.** 

> [!NOTE]
> A ação **de definições de Check** no Portal da Empresa e a ação **Sync** para dispositivos na Consola de Administrador do Microsoft Endpoint Manager inicia um check-in do MDM e não obriga um check-in de agente.

 ### <a name="when-is-the-agent-removed"></a>Quando é que o agente é removido?
 Existem várias condições que podem fazer com que o agente seja removido do dispositivo, tais como:
 - Os scripts da shell já não estão atribuídos ao dispositivo. 
 - O dispositivo macOS já não é gerido.
 - O agente encontra-se em estado irrecuperável por mais de 24 horas (hora de despertar do dispositivo).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Como desligar os dados de utilização enviados para a Microsoft para scripts de concha?
 Para desativar os dados de utilização enviados para a Microsoft a partir do Intune MDM Agent, abra o Portal da Empresa e selecione **Menu** > **Preferências** > *descontrolar "permitem à Microsoft recolher dados de utilização".* Isto irá desligar os dados de utilização enviados tanto para o agente intune do MDM como para o Portal da Empresa.

## <a name="known-issues"></a>Problemas conhecidos
- **Atribuição do grupo de utilizadores:** Os scripts shell atribuídos a grupos de utilizadores não se aplicam aos dispositivos. A atribuição do grupo de utilizadores não é suportada atualmente na pré-visualização. Utilize a atribuição do grupo do dispositivo para atribuir scripts.
- **Recolher registos:** A ação "Recolher registos" é visível. Mas quando a recolha de registos é tentada, mostra "um erro ocorrido" e não captura registos. A recolha de registos não é suportada na pré-visualização.
- **Sem estado de execução** de script: No caso improvável de um script ser recebido no dispositivo e o dispositivo ficar offline antes de o estado de execução ser reportado, o dispositivo não reportará o estado de execução do script na consola de administração.
- **Relatório de estado do utilizador:** Existe uma questão de relatório vazio. No [Microsoft Endpoint Manager Admin Center,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Monitor**. O estado do utilizador mostra um relatório vazio.

## <a name="next-steps"></a>Próximos passos

- [Criar uma política de conformidade no Microsoft Intune](..\protect\create-compliance-policy.md)
