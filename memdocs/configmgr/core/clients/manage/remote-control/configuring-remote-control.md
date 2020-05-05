---
title: Configurar o controlo remoto
titleSuffix: Configuration Manager
description: Instale um controlo remoto no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076735"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Configurar o controlo remoto no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Este procedimento descreve a configuração das definições padrão do cliente para controlo remoto. Estas definições aplicam-se a todos os computadores da sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, atribua uma definição personalizada do cliente do dispositivo a uma coleção que contenha esses computadores. Para mais informações consulte [Como configurar as definições](../../../../core/clients/deploy/configure-client-settings.md)do cliente . 

Para utilizar a Assistência Remota ou o Ambiente de Trabalho Remoto, este deve ser instalado e configurado no computador que executa a consola do Gestor de Configuração. Para mais informações sobre como instalar e configurar a Assistência Remota ou o Ambiente de Trabalho Remoto, consulte a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para ativar o controlo remoto e configurar as definições de cliente  

1. Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

2. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

3. Na caixa de diálogo **Predefinido,** escolha **Ferramentas Remotas**.  

4. Configure as definições do cliente do telecomando, da Assistência Remota e do cliente do Ambiente de Trabalho Remoto. Para obter uma lista de configurações de clientes de ferramentas remotas que possa configurar, consulte [Ferramentas Remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Pode alterar o nome da empresa apresentado na caixa de diálogo **Controlo Remoto do ConfigMgr** ao configurar um valor para **Nome da organização apresentada no Centro de Software** nas definições de cliente do **Agente do Computador** .  

   Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Como gerir os clientes.](../../../../core/clients/manage/manage-clients.md)  

#### <a name="enable-keyboard-translation"></a>Ativar a tradução do teclado

Por predefinição, o Gestor de Configuração transmite a posição chave da localização do espectador para a localização do participante. Isto pode apresentar um problema para configurações de teclado que diferem de espectador para compartilhista. Por exemplo, um espectador com um teclado inglês escreveria um "A", mas o teclado francês do comum forneceria um "Q". Tem agora a opção de configurar o telecomando para que o próprio personagem seja transmitido do teclado do espectador para o comedor, e o que o espectador pretende digitar chega ao comum.

Para ligar a tradução do teclado, no Controlo Remoto do Gestor de **Configuração,** escolha **Ação**e escolha **a tradução do teclado Activapara** transmitir a posição chave.

> [!NOTE]
>
> Chaves especiais, tais como ~!#@$, não serão traduzidas corretamente.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Atalhos de teclado para o visualizador de controlo remoto

|Atalho de teclado|Descrição|  
|-----------------------|-----------------|  
|Alt+Page Up|Alterna entre executar programas da esquerda para a direita.|  
|Alt+Page Down|Alterna entre executar programas da direita para a esquerda.|  
|Alt+Insert|Percorre a execução de programas pela ordem em que foram abertos.|  
|Alt+Home|Apresenta o menu **Início** .|  
|Ctrl+Alt+End|Apresenta a caixa de diálogo Segurança do Windows (Ctrl+Alt+Del).|  
|Alt+Delete|Apresenta o menu do Windows.|  
|Ctrl+Alt+Sinal de Subtração (no teclado numérico)|Copia a janela ativa no computador local para a Área de transferência do computador remoto.|  
|Ctrl+Alt+Sinal de Adição (no teclado numérico)|Copia toda a área da janela do computador local para a Área de transferência do computador remoto.|  
