---
title: Resolução de problemas do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como resolver problemas com o Windows Defender e endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724490"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Resolver problemas do cliente do Windows Defender ou do Endpoint Protection

*Aplica-se a: Gestor de Configuração (ramo atual)*

Se encontrar problemas com o Windows Defender ou endpoint Protection, use este artigo para resolver os seguintes problemas:  

- [Atualizar o Windows Defender ou a Proteção de Pontofinal](#update-windows-defender-or-endpoint-protection)  
- [Iniciar o serviço de proteção do Windows Defender ou Endpoint](#starting-windows-defender-or-endpoint-protection-service)  
- [Problemas de ligação à Internet](#internet-connection-issues)  
- [Ameaça detetada não pode ser remediada](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a> Atualizar o Windows Defender ou o Endpoint Protection

### <a name="symptoms"></a>Sintomas

O Windows Defender ou endpoint Protection funciona automaticamente com o Microsoft Update para garantir que as definições do seu vírus e spyware são mantidas atualizadas.  

Esta secção aborda questões comuns com atualizações automáticas, incluindo as seguintes situações:  

- Vê mensagens de erro a indicar que as atualizações falharam.  

- Quando verifica as atualizações, recebe uma mensagem de erro de que as atualizações de definição de vírus e spyware não podem ser verificadas, descarregadas ou instaladas.  

- Mesmo que o seu dispositivo esteja ligado à internet, as atualizações falham.  

- As atualizações não estão a instalar-se automaticamente como programado.  

### <a name="causes"></a>Causas

As causas mais comuns para problemas de atualização são problemas com a conectividade da Internet. Se souber que o seu dispositivo está ligado à internet porque pode navegar para outros Web sites, o problema pode ser causado por conflitos com as definições da internet no Windows.  

### <a name="options-to-resolve"></a>Opções para resolver

#### <a name="step-1-reset-your-internet-settings"></a>Passo 1: Redefinir as definições da internet  

1. Sapre todos os programas abertos, incluindo o navegador web.  

    > [!NOTE]  
    > Ao redefinir estas definições de internet, poderá eliminar os ficheiros temporários do seu navegador, cookies, histórico de navegação e senhas online. Não apaga os seus favoritos.  

2. Vá ao menu **Iniciar** `inetcpl.cpl`e abra.  

3. Mude para o separador **Avançado.**  

4. Na secção para **redefinir as definições**do Internet Explorer, selecione **Reset**e, em seguida, selecione **Reset** novamente para confirmar.  

5. Selecione **OK** quando as definições forem redefinidas.

6. Tente atualizar novamente o Windows Defender.

Se a questão persistir, continue até ao próximo passo.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Passo 2: Certifique-se de que a data e a hora estão corretamente definidas no seu computador  

Se a mensagem de erro contiver o código 0x80072f8f, o problema é provavelmente causado por uma data ou definição de hora incorreta no seu computador. Vá ao menu **Iniciar,** selecione **Definições,** selecione **O tempo & idioma,** e selecione **Hora de Data &**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Passo 3: Mude o nome da pasta de Distribuição de Software no seu computador  

1. Pare o serviço **de Atualização do Windows.**  

    1. Ir para **Iniciar**, e **serviços abertos.msc**.  

    2. Selecione o serviço **Deatualização do Windows.** Vá ao menu **Ação** e selecione **Parar**.

2. Mude o nome do diretório de Distribuição de **Software.**  

    1. Abra uma linha de comandos como administrador.  

    2. Insira os seguintes comandos:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Reiniciar o serviço **de Atualização do Windows.**

    1. Volte para a janela **dos Serviços.**  

    2. Selecione o serviço **Deatualização do Windows.** Vá ao menu **Ação** e selecione **Iniciar**.

    3. Feche a janela Serviços.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Passo 4: Redefinir o motor de atualização antivírus da Microsoft no seu computador  

1. Abra uma linha de comandos como administrador.

2. Insira os seguintes comandos:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Reinicie o computador.  

4. Tente atualizar novamente o Windows Defender.

Se a questão persistir, continue até ao próximo passo.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Passo 5: Instale manualmente as atualizações de definição  

[Faça o download manual das últimas atualizações.](https://www.microsoft.com/en-us/wdsi/defenderupdates)  

#### <a name="step-6-contact-microsoft-support"></a>Passo 6: Contacte o suporte da Microsoft  

Se estes passos não resolverem o problema, contacte o suporte da Microsoft. Para mais informações, consulte opções de [suporte e recursos comunitários.](../../core/understand/find-help.md#BKMK_SupportOptions)  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a> Iniciar o serviço Windows Defender ou Endpoint Protection

### <a name="symptom"></a>Sintoma

Recebe uma mensagem a informar-lhe que o **Windows Defender ou endpoint Protection não está a monitorizar o computador porque o serviço do programa parou. Devia reiniciá-lo agora.**

### <a name="solution"></a>Solução

#### <a name="step-1-restart-your-computer"></a>Passo 1: Reiniciar o computador

Feche todas as aplicações e reinicie o seu computador.  

#### <a name="step-2-check-the-windows-service"></a>Passo 2: Verifique o serviço Windows

1. Ir para **Iniciar**, e **serviços abertos.msc**.  

2. Selecione o **Serviço Antivírus Do Windows Defender**.  

3. Certifique-se de que o **Tipo de Arranque** está definido para **Automático**.

4. Vá ao menu **Ação** e selecione **Iniciar**.

    1. Se esta ação não estiver disponível, selecione **Stop**. Aguarde que o serviço pare e, em seguida, selecione a ação **Iniciar** para reiniciar o serviço.  

Note quaisquer erros que possam aparecer durante este processo. [Contacte](../../core/understand/find-help.md#BKMK_SupportOptions) o Microsoft Support e forneça as informações de erro.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Passo 3: Remover quaisquer programas de segurança de terceiros  

> [!NOTE]  
> Algumas aplicações de segurança não desinstalam completamente. Poderá ser necessário descarregar e executar um utilitário de limpeza para a sua aplicação de segurança anterior para removê-lo completamente.  

1. Vá **iniciar** e abra **appwiz.cpl**.  

2. Na lista de programas instalados, desinstale quaisquer programas de segurança de terceiros.

3. Reinicie o computador.  

> [!CAUTION]  
> Quando remove os programas de segurança, o computador pode estar desprotegido. Se tiver problemas em instalar o Windows Defender depois de remover os programas de segurança existentes, contacte o [Microsoft Support](https://support.microsoft.com/supportforbusiness/productselection). Selecione a família do produto **Security** e, em seguida, o produto **Windows Defender.**

## <a name="internet-connection-issues"></a>Problemas de ligação à Internet

Para que o seu computador receba as mais recentes atualizações do Windows Update, conecte-o à internet.  

1. Vá **iniciar** e abra **ncpa.cpl**.  

2. Abra o nome de ligação para ver o **Estado**de ligação .  

3. Se o seu computador estiver ligado, o estado de **conectividade IPv4** e/ou **iPv6** é **internet**.  

4. Se o seu computador não parecer estar ligado, selecione o nome da ligação e **selecione Diagnosticar esta ligação**.

Feche quaisquer programas abertos e reinicie o seu computador.  

## <a name="detected-threat-cant-be-remediated"></a> Não é possível remediar a ameaça detetada

Quando o Windows Defender ou endpoint Protection deteta uma ameaça potencial, tenta mitigar a ameaça colocando ou removendo a ameaça. Estas ameaças podem esconder-se dentro`.zip`de um arquivo comprimido ( ) ou numa partilha de rede.

### <a name="remove-or-scan-the-file"></a>Remover ou analisar o ficheiro  

- Se a ameaça detetada estiver num ficheiro de arquivo comprimido, navegue para o ficheiro. Elimine o ficheiro ou digitaliza-o manualmente. Clique no ficheiro e selecione **Scan com Windows Defender**. Se o Windows Defender detetar ameaças adicionais no ficheiro, ele o notifica. Então pode escolher uma ação apropriada.  

- Se a ameaça detetada estiver numa partilha de rede, abra a parte e o scaneie manualmente. Clique no ficheiro e selecione **Scan com Windows Defender**. Se o Windows Defender detetar ameaças adicionais na partilha da rede, o mesmo o notifica. Então pode escolher uma ação apropriada.  

- Se não tiver a certeza da origem do ficheiro, faça uma varredura completa no seu computador. Uma varredura completa pode levar algum tempo para completar.  

## <a name="see-also"></a>Consulte também

[Cliente endpoint protection frequentemente fez perguntas](endpoint-protection-client-faq.md)

[Ajuda ao cliente do Endpoint Protection](endpoint-protection-client-help.md)
