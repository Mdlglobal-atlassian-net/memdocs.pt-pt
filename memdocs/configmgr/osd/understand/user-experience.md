---
title: Experiências do utilizador para implementação de OS
titleSuffix: Configuration Manager
description: Conheça as experiências do utilizador como o progresso da sequência de tarefas e o assistente de mídia para a implementação do sistema operativo no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719933"
---
# <a name="user-experiences-for-os-deployment"></a>Experiências do utilizador para implementação de OS

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de implementar uma sequência de [tarefas](../deploy-use/deploy-a-task-sequence.md), dependendo do cenário, existem diferentes formas de os utilizadores interagirem com a implementação. Este artigo mostra as principais experiências do utilizador com implementações de SO, e como pode configurá-las:

- Notificação do utilizador do Software Center para uma implementação de alto impacto
- Uma experiência de arranque PXE de amostra
- Assistente de sequência de tarefas a partir de meios de comunicação
- Janela de progresso quando a sequência de tarefas corre
- Janela de erro quando a sequência de tarefa falha

## <a name="software-center"></a>Centro de Software

Para uma implementação de alto impacto, pode personalizar a mensagem que o Software Center exibe. Quando o utilizador abre a implementação do OS no Centro de Software, eles vêem uma mensagem semelhante à seguinte janela:

![Notificação de sequência de tarefas personalizada ao utilizador final do Centro de Software](../media/user-notification-enduser.png)

Para obter mais informações sobre como personalizar a mensagem nesta janela, consulte [Criar uma notificação personalizada para implementações de alto risco](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Também pode personalizar o nome da organização no topo da janela. (O exemplo acima mostra `IT Organization`o valor predefinido, ). Altere a definição de cliente de **nome da Organização** no grupo Agente **Informático.** Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Para mais informações, consulte [o Use Software Center para implementar o Windows sobre a rede](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Diferentes modelos de hardware têm experiências diferentes para PXE. Para iniciar a rede, os dispositivos baseados `Enter` em UEFI normalmente utilizam `F12` a chave e os dispositivos baseados em BIOS usam a chave.

O exemplo que se segue mostra a experiência PXE Hyper-V Gen1 (BIOS):

![Exemplo ecrã PXE BIOS de uma máquina virtual Hyper-V](media/hyperv-pxe.png)

Depois de o dispositivo ter conseguido as botas via PXE, comporta-se de forma semelhante aos meios de arranque. Para mais informações, consulte a secção seguinte do assistente de [sequência de tarefas](#task-sequence-wizard).

Para mais informações, consulte [Use PXE para implementar o Windows sobre a rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> Se utilizar as implementações pXE e configurar o hardware do dispositivo com o adaptador de rede como o primeiro dispositivo de arranque, estes dispositivos podem iniciar automaticamente uma sequência de tarefas de implementação de SISTEMAS sem interação do utilizador. A verificação de implementação não gere esta configuração. Embora esta configuração possa simplificar o processo e reduzir a interação do utilizador, coloca o dispositivo em maior risco de reimagem acidental.

## <a name="task-sequence-wizard"></a>Assistente de sequência de tarefas

Quando utilizar os meios de sequência de [tarefas,](../deploy-use/create-task-sequence-media.md)o assistente de sequência de tarefas corre para orientar o processo.

### <a name="welcome-to-the-task-sequence-wizard"></a>Bem-vindo ao assistente de sequência de tarefas

![Screenshot da página principal do Assistente de Sequência de Tarefas](media/welcome-task-sequence-wizard.png)

- Se proteger a palavra-passe dos meios de comunicação, o utilizador tem de introduzir a palavra-passe nesta página de boas-vindas.

- **Selecione Configurar Definições** de Rede para especificar um endereço IP estático ou outras definições de rede personalizadas. Caso contrário, o dispositivo utiliza dHCP por defeito.

- Se a sua rede necessitar de um proxy, **selecione Configurar Definições de Procuração**.

### <a name="select-a-task-sequence-to-run"></a>Selecione uma sequência de tarefas para executar

Se implementar mais de uma sequência de tarefas no dispositivo, verá esta página para selecionar uma sequência de tarefas. Certifique-se de que utiliza um nome e descrição para a sua sequência de tarefas que os utilizadores possam compreender.

![Screenshot da página de seleção da sequência de tarefas do Assistente de Sequência de Tarefas](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Editar variáveis de sequência de tarefas

Se alguma variável de sequência de tarefas tiver valores vazios, o assistente mostra uma página para editar os valores variáveis.

![Screenshot da página de variáveis de sequência de tarefas de edição do Assistente de Sequência de Tarefas](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Comandos prestart

Pode personalizar os meios de sequência de tarefas ou imagens de arranque para executar um comando prestart. Um comando prestart corre antes da sequência de tarefas começar. As seguintes ações são algumas das mais comuns:

- Insime o utilizador para valores dinâmicos, como o nome do computador
- Especificar a configuração da rede
- Definir a finidade do dispositivo do utilizador

O comando prestart é uma linha de comando que especifica com um script ou programa. A experiência do utilizador é única para esse script ou programa.

Para obter mais informações, veja os artigos seguintes:

- [Comandos de pré-início para suporte de dados da sequência de tarefas](prestart-commands-for-task-sequence-media.md)
- [Gerir imagens de arranque](../get-started/manage-boot-images.md#customization)
- [Meios de sequência de tarefas](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Progresso da sequência de tarefas

Quando a sequência de tarefas funciona, exibe a janela de progresso da **instalação:**

![Exemplo da janela de progresso da sequência de tarefas](media/task-sequence-progress.png)

- Esta janela está sempre por cima; pode movê-lo, mas não pode fechá-lo ou minimizá-lo.

- Pode personalizar o nome da organização no topo da janela. (O exemplo acima mostra `IT Organization`o valor predefinido, ). Altere a definição de cliente de **nome da Organização** no grupo Agente **Informático.** Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > A sequência de tarefas armazena este valor na [variável _SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName)de leitura .

- Pode personalizar a subposição. (O exemplo acima mostra `Running: <task sequence name>`o valor predefinido, .) Nas propriedades da sequência de tarefas, selecione a opção de **utilizar texto personalizado** para o texto de notificação de progresso. Permite um máximo de 255 caracteres.

- **Ação de execução**: A primeira linha mostra o nome do passo da sequência de tarefas atual. A barra de progresso abaixo mostra a conclusão global da sequência de tarefas.

- A segunda linha apenas mostra alguns passos que proporcionam progressos mais detalhados.

- Utilize a variável de sequência de [tarefas TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) para controlar quando a sequência de tarefas apresentar progresso.

    Para desativar completamente a janela de progresso, desative a opção de mostrar o progresso da sequência de **tarefas** na página da Experiência do **Utilizador** da implementação da sequência de tarefas.

A partir da versão 2002, a janela de progresso da sequência de tarefas inclui as seguintes melhorias:<!--5932692-->

- Mostra o número atual de etapas, número total de etapas e por cento de conclusão

- Aumentou a largura da janela para lhe dar mais espaço para mostrar melhor o nome da organização numa única linha

![Janela de progresso da sequência de tarefas exemplo](media/2356386-task-sequence-progress.png)

Por padrão, a janela de progresso da sequência de tarefas utiliza o texto existente. Se não fizer alterações, continua a funcionar da mesma forma que na versão 1910 e anterior. Para mostrar as novas informações de progresso, especifique a variável de sequência de tarefas, [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel).

A contagem e a percentagem concluída destinam-se apenas a orientações gerais. Estes valores baseiam-se no número total de etapas na sequência de tarefas. Para uma sequência de tarefas mais complexa com passos que funcionam condicionalmente com base na lógica da sequência de tarefas, o progresso pode não ser linear.

A contagem de etapas totais não inclui os seguintes itens na sequência de tarefas:

- Grupos, grupos. Este item é um recipiente para outros passos, não um passo em si.

- Instâncias do passo da sequência de **tarefas run.** Este passo é um recipiente para outros passos.

- Passos que desativa explicitamente. Um passo desativado não funciona durante a sequência de tarefas.

    > [!NOTE]
    > Os passos ativados num grupo desativado ainda estão incluídos na contagem total.

## <a name="task-sequence-error"></a>Erro de sequência de tarefas

Se a sequência de tarefa falhar, apresenta a janela **error da sequência** de tarefas.

![Janela de erro de sequência de tarefas de exemplo](media/task-sequence-error.png)

- Personaliza a informação do cabeçalho da mesma forma que a janela de progresso da sequência de tarefas.

- Apresenta o nome da sequência de tarefas, um código de erro e uma mensagem geral para os utilizadores. Por exemplo: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- A janela fecha-se automaticamente após um período de tempo. Por defeito, este intervalo é de 15 minutos. Pode personalizar este valor com a variável de sequência de [tarefas SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout).
