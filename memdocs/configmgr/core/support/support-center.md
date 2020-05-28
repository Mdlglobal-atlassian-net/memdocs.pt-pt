---
title: Centro de Suporte
titleSuffix: Configuration Manager
description: Clientes do Gestor de Configuração de Resolução de Problemas com o Centro de Suporte.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da2fe2ad66617ffb5ad3058011f111b0aaf9e9ae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903900"
---
# <a name="support-center-for-configuration-manager"></a>Centro de Suporte para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357489-->
A partir da versão 1810, utilize o Support Center para resolução de problemas com o cliente, visualização de registoem em tempo real ou capturando o estado de um computador cliente do Gestor de Configuração para análise posterior. O Centro de Suporte é uma única ferramenta para consolidar muitas ferramentas de resolução de problemas do administrador.


## <a name="about"></a>Acerca de

O Support Center tem como objetivo reduzir os desafios e a frustração ao resolver os computadores clientes do Gestor de Configuração. Anteriormente, ao trabalhar com suporte para resolver um problema com clientes do Gestor de Configuração, teria de recolher manualmente ficheiros de registo e outras informações para ajudar a resolver problemas. Foi fácil esquecer acidentalmente um ficheiro de registo crucial, causando dores de cabeça adicionais para si e para o pessoal de apoio com quem está a trabalhar.

Utilize o Centro de Suporte para agilizar a experiência de suporte. Permite-lhe:

- Crie um pacote de resolução de problemas (.ficheiro zip) que contenha os ficheiros de registo do cliente do Gestor de Configuração. Em seguida, tem um único ficheiro para enviar para o pessoal de apoio.  

- Ver Ficheiros de registo de clientes do Gestor de Configuração, certificados, definições de registo, despejos de depurados, políticas de cliente.  

- Diagnóstico em tempo real do inventário (substitui ContentSpy), política (substitui PolicySpy) e cache do cliente.  

### <a name="support-center-viewer"></a>Espectador do Centro de Suporte

O Centro de Suporte inclui o Espectador do Centro de Suporte, uma ferramenta que suporta o uso do pessoal para abrir o conjunto de ficheiros que cria utilizando o Centro de Suporte. O colecionador de dados do Support Center recolhe e embala registos de diagnóstico de um cliente local ou remoto do Gestor de Configuração. Para visualizar pacotes de recolha de dados, utilize a aplicação do espectador.

### <a name="support-center-log-file-viewer"></a>Espectador de ficheiro sonorde do Centro de Suporte

O Centro de Suporte inclui um espectador de registo moderno. Esta ferramenta substitui o CMTrace e fornece uma interface personalizável com suporte para separadores e janelas dockable. Tem uma camada de apresentação rápida e pode carregar ficheiros de registo grandes em segundos.

### <a name="support-center-onetrace-preview"></a>OneTrace do Centro de Suporte (Pré-visualização)

<!--3555962-->
A partir da versão 1906, o **OneTrace** é um novo espectador de log com Support Center. Funciona da mesma forma com a CMTrace, com melhorias. Para mais informações, consulte [o Suporte Center OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>Cmdlets do PowerShell

O Centro de Suporte também inclui [cmdlets PowerShell](https://docs.microsoft.com/powershell/sccm/overview?view=sccm-ps). Utilize estes cmdlets para criar uma ligação remota a outro cliente do Gestor de Configuração, para configurar as opções de recolha de dados e para iniciar a recolha de dados.


## <a name="prerequisites"></a>Pré-requisitos

Instale os seguintes componentes no servidor ou computador cliente no qual instala o Centro de Suporte:

- Uma versão OS suportada pelo Gestor de Configuração. Para mais informações, consulte [versões De SO suportadas para clientes.](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) O Centro de Suporte não suporta dispositivos móveis.  

- .NET A estrutura 4.5.2 é necessária no computador onde executa o Centro de Suporte e os seus componentes.  


## <a name="install"></a>Instalar

Encontre o instalador do Centro de Suporte no servidor do site no seguinte caminho: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Depois de o instalar, encontre os seguintes itens no menu Iniciar no grupo **Microsoft System Center:**  

- Centro de Suporte (ConfigMgrSupportCenter.exe)  
- Espectador de ficheiros de registo do centro de suporte (CMLogViewer.exe)  
- Espectador do Centro de Suporte (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>Problemas conhecidos

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Não é possível instalar a versão mais recente se uma versão mais antiga já estiver instalada

<!--SCCMDocs-pr issue #3090-->
*Aplica-se às versões 1810 e 1902*

Se já tiver uma versão mais antiga do Support Center instalada, o novo instalador falha. Este problema deve-se à forma como os ficheiros são versonizados entre a versão original e a versão mais recente. Para resolver este problema, desinstale primeiro a versão mais antiga do Support Center. Em seguida, instale a versão mais recente.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>As ligações remotas devem incluir o nome ou domínio do computador como parte do nome do utilizador

Se se ligar a um cliente remoto do Centro de Suporte, deve fornecer o nome da máquina ou nome de domínio para a conta de utilizador ao estabelecer a ligação. Se utilizar um nome de computador ou nome de domínio de curta duração (por `.\administrator` exemplo), a ligação tem sucesso, mas o Centro de Suporte não recolhe dados do cliente.

Para evitar este problema, utilize os seguintes formatos de nome de utilizador para se ligar a um cliente remoto:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>As ligações de blocode mensagens do servidor scripted para clientes remotos podem exigir remoção

Ao ligar-se a clientes remotos utilizando o cmdlet PowerShell de [New-CMMachineConnection,](https://go.microsoft.com/fwlink/p/?linkid=390542) o Support Center cria uma ligação de bloco de mensagens de servidor (SMB) a cada cliente remoto. Mantém essas ligações depois de concluir a recolha de dados. Para evitar exceder o número máximo de ligações remotas para windows, utilize o `net use` comando para ver o conjunto atualmente ativo de ligações remotas. Em seguida, desative quaisquer ligações desnecessárias utilizando o seguinte comando:`net use <connection_name> /d`
onde `<connection_name>` está o nome da ligação remota.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>O pedido de avaliação do ciclo de implementação de aplicações não é enviado corretamente para máquinas remotas

<!--2849356-->
*Aplica-se à versão 1810*

No Centro de Suporte, se selecionar a **avaliação** de implementação da Aplicação a partir da ação **de gatilho invocada** no separador **Conteúdo,** esta ação inicia uma tarefa que avalia as aplicações implementadas. Se estiver ligado a um cliente local, avalia as implementações de aplicações de máquinas e utilizadores. No entanto, se estiver ligado a um cliente remoto, apenas avalia as implementações de aplicações de máquinas.


## <a name="next-steps"></a>Próximos passos

[Arranque rápido do Centro de Apoio](support-center-quickstart.md)
