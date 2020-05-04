---
title: Administrar remotamente o computador Windows
titleSuffix: Configuration Manager
description: Administrar um computador cliente remoto do Windows utilizando o Gestor de Configuração.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715110"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Como administrar remotamente um computador cliente do Windows utilizando o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)* O Gestor de Configuração permite-lhe ligar-se aos computadores clientes utilizando o Controlo Remoto do Gestor de **Configuração.** Antes de começar a utilizar o telecomando, certifique-se de que revê as informações nos seguintes artigos:  

-   [Pré-requisitos para controlo remoto](prerequisites-for-remote-control.md)  

-   [Configurar o controlo remoto](configuring-remote-control.md)  

Aqui estão três maneiras de iniciar o visualizador de controlo remoto:  

-   Na consola 'Gestor de Configuração'.  

-   Num pedido de comando do Windows.  

-   A partir do menu Windows **Start,** num computador que executa a consola do Gestor de Configuração, no grupo de programas do **Microsoft System Center.**  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar remotamente um computador cliente a partir da consola do Configuration Manager  

1.  Na consola do Gestor de Configuração, escolha**Dispositivos** **de Segurança e Conformidade** > ou **Coleções de Dispositivos.**  

3.  Selecione o computador que pretende administrar remotamente e, em seguida, no separador **Home,** no grupo **Dispositivo,** escolha **Iniciar** > **controlo remoto**.  

    > [!IMPORTANT]  
    >  Se a permissão de cliente **Solicitar ao utilizador permissão do Controlo Remoto** estiver definida como **Verdadeiro**, a ligação não inicia até o utilizador no computador remoto aceitar o pedido de controlo remoto. Para mais informações, consulte [Configurar o telecomando](configuring-remote-control.md).  

4.  Depois de a janela **Controlo Remoto do Configuration Manager** ser aberta, pode administrar remotamente o computador cliente. Utilize as opções seguintes para configurar a ligação.  

    > [!NOTE]  
    >  Se o computador a que se liga tiver vários monitores, o visor de todos os monitores é mostrado na janela de controlo remoto.  

    -   **Ficheiro**
        - **Ligar** - Ligar a outro computador. Esta opção não está disponível quando uma sessão de controlo remoto está ativa.  
        -   **Desconexão** - Desliga a sessão de controlo remoto ativo, mas não fecha a janela de controlo remoto do Gestor de **Configuração.**  
        - **Saída** - Desliga a sessão de controlo remoto ativo e fecha a janela de controlo remoto do Gestor de **Configuração.**  

        > [!NOTE]  
        >  Quando desligar uma sessão de controlo remoto, o conteúdo da Área de Transferência do Windows no computador que está a visualizar é eliminado.


    - **Ver**
      - **Profundidade de cor** - Escolha 16 bits ou 32 bits por pixel.
      -  **Ecrã completo** - Maximiza a janela de controlo remoto do Gestor de **Configuração.** Para sair do modo de ecrã inteiro, prima Ctrl+Alt+Break.  
      - **Otimize para uma ligação** de baixa largura de banda - Escolha esta opção se a ligação for de baixa largura de banda.
      - **Ecrã:**
        - **Todos os ecrãs** - Adicionados em Diretor de Configuração 1902. Se o computador a que se liga tiver vários monitores, o visor de todos os monitores é mostrado na janela de controlo remoto. **Todos os Ecrãs** são a única vista para computadores com vários monitores antes de 1902.
        -  **Primeiro Ecrã** - Adicionado no Gestor de Configuração 1902. O *primeiro ecrã* encontra-se na parte superior e extrema-esquerda, como mostra as definições do windows display. Não é possível selecionar um ecrã específico. Quando mudar a configuração do espectador, religue a sessão remota. O espectador guarda a sua preferência por futuras ligações.
        -  **Escala para ajuste** - Dimensiona o visor do computador remoto para se adaptar ao tamanho da janela de controlo remoto do Gestor de **Configuração.**
        - **Barra** de Estado - Alterna a visualização da barra de estado de controlo remoto do Gestor de **Configuração.**  

       > [!NOTE]  
       >  O espectador guarda a sua preferência por futuras ligações.

    -   **Ação**
        - **Envie chave Ctrl+Alt+Del** - Envia uma combinação de teclaCtrl+Alt+Del para o computador remoto. 
        - **Ativar a partilha de clipboard** - Permite copiar e colar itens de e para o computador remoto. Se alterar este valor, tem de reiniciar a sessão de controlo remoto para que a alteração tenha efeito.   
          - Se não quiser que a partilha de clipboard seja ativada na consola do Gestor de Configuração, no computador que executa a consola, detete o valor da chave de registo **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** to **0**.
        - **Ativar a Tradução do Teclado** - Traduz o esquema do teclado do computador que executa a consola para o layout do dispositivo conectado.
        - **Bloqueie** o teclado remoto e o rato - Bloqueia o teclado remoto e o rato para evitar que o utilizador opere o computador remoto.  

    -   **Help**
        - **Sobre controlo remoto** - Exibe a versão atual do espectador.  

5.  Os utilizadores do computador remoto podem ver mais informações sobre a sessão de controlo remoto quando clicarem no ícone de **Controlo Remoto** do Gestor de Configuração. O ícone encontra-se na área de notificação do Windows ou no ícone da barra de sessão de controlo remoto.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Para iniciar o visualizador de controlo remoto a partir da linha de comandos do Windows  

-   No pedido de comando do Windows, escreva _<Pasta\>de Instalação do Gestor_de Configuração**\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe suporta as seguintes opções da linha de comandos:  

- *Endereço* - Especifica o nome NetBIOS, o nome de domínio totalmente qualificado (FQDN) ou o endereço IP do computador cliente a que pretende ligar.
- *Nome* do servidor do site - Especifica o nome do servidor do site do Gestor de Configuração para o qual pretende enviar mensagens de estado relacionadas com a sessão de controlo remoto.
- **/?** - Exibe as opções da linha de comando para o visualizador de controlo remoto.  
     
**Exemplo: CmRcViewer.exe** *\><Endereço* * < \\\Nome do servidor do site>* 

> [!NOTE]  
> O visualizador de controlo remoto é suportado em todos os sistemas operativos que são suportados para a consola 'Gestor de Configuração'. Para obter mais informações, consulte [configurações suportadas para consolas](../../../plan-design/configs/supported-operating-systems-consoles.md) e [pré-requisitos](prerequisites-for-remote-control.md)do Gestor de Configuração para controlo remoto .

## <a name="next-steps"></a>Passos seguintes

[Auditoria de utilização de controlo remoto](audit-remote-control-usage.md)
