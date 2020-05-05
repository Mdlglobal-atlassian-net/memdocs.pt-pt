---
title: Site de administração e monitorização BitLocker
titleSuffix: Configuration Manager
description: Como utilizar o website de administração e monitorização bitLocker (portal de helpdesk) no Gestor de Configuração
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84725ac494e1d9497524303b841207bd05cd3859
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717511"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Site de administração e monitorização BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

O site de administração e monitorização BitLocker é uma interface administrativa para encriptação bitLocker drive. Também é referido como o portal de mesa de ajuda. Utilize este website para rever relatórios, recuperar as unidades dos utilizadores e gerir os TPMs do dispositivo.

[![Screenshot da administração padrão BitLocker e site de monitorização](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Antes de o utilizar, instale este componente num servidor web. Para mais informações, consulte [Configurar relatórios e portais BitLocker](setup-websites.md).

Aceda ao site de administração e monitorização através do seguinte URL:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Pode ver o Relatório de Auditoria de **Recuperação** no site de administração e monitorização. Adiciona outros relatórios de gestão BitLocker ao ponto de serviços de reporte. Para mais informações, consulte os [relatórios do View BitLocker](view-reports.md).

## <a name="groups"></a>Grupos

Para aceder a áreas específicas do site de administração e monitorização, a sua conta de utilizador tem de estar num dos seguintes grupos. Crie estes grupos em Diretório Ativo usando qualquer nome que queira. Ao instalar este website, especifice estes nomes de grupo. Para mais informações, consulte [Configurar relatórios e portais BitLocker](setup-websites.md).

|Grupo|Descrição|
|--- |--- |
|Administrações de mesa de ajuda BitLocker|Fornece acesso a todas as áreas do site de administração e monitorização. Quando ajuda um utilizador a recuperar os seus discos, introduz apenas a chave de recuperação e não o domínio e o nome do utilizador. Se um utilizador for membro deste grupo e do grupo de utilizadores de secretária bitLocker, as permissões do grupo de administração anulam as permissões do grupo de utilizadores.|
|Utilizadores de mesa de ajuda BitLocker|Fornece acesso às áreas de **Gestão TPM** e **Drive Recovery** do site de administração e monitorização. Quando utiliza qualquer uma das áreas, tem de preencher todos os campos, incluindo o domínio do utilizador e o nome da conta. Se um utilizador for membro deste grupo e do grupo de administração de secretária seletiva BitLocker, as permissões do grupo de administração anulam as permissões do grupo de utilizadores.|
|BitLocker reportar utilizadores|Fornece acesso à área de **Relatórios** da administração e site de monitorização.|

## <a name="manage-tpm"></a>Gerir o TPM

Se um utilizador introduzir o PIN incorreto demasiadas vezes, pode bloquear o TPM. O número de vezes que um utilizador pode introduzir um PIN incorreto antes das fechaduras TPM variar de fabricante para fabricante. A partir da área de **Gestão TPM** da administração e site de monitorização, aceda ao sistema centralizado de dados de recuperação.

Para mais informações sobre a propriedade do TPM, consulte [configure MBAM para estermar as palavras-passe do ProprietárioAuth.](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm)

> [!NOTE]
> A partir do Windows 10, versão 1607, o Windows não mantém a senha do proprietário do TPM ao fornecer o TPM.

1. Vá ao site de administração e monitorização `https://webserver.contoso.com/HelpDesk`no navegador web, por exemplo.

1. No painel esquerdo, selecione a área **Manage TPM.**

    ![Página de gestão e monitorização bitLocker Gerencie a página TPM](media/bitlocker-admin-manage-tpm.png)

1. Introduza o nome de domínio totalmente qualificado para o computador e o nome do computador.

1. Se necessário, introduza o domínio e o nome de utilizador do utilizador para recuperar o ficheiro de palavra-passe do proprietário do TPM.

1. Escolha uma das seguintes opções para a **Razão para solicitar o ficheiro de palavra-passe do proprietário da TPM:**

    - Redefinir bloqueio PIN
    - Ligue o TPM
    - Desligue o TPM
    - Alterar a palavra-passe do TPM
    - TPM claro
    - Outros

    Depois de **submeter** o formulário, o site devolve uma das seguintes respostas:

    - Se não encontrar um ficheiro de palavra-passe do proprietário tpm correspondente, devolve uma mensagem de erro.

    - O ficheiro de senha do proprietário do TPM para o computador submetido

    Depois de recuperar o ficheiro de palavra-passe do proprietário do TPM, o site exibe a palavra-passe do proprietário.

1. Para guardar a palavra-passe para um ficheiro, selecione **Guardar**.

1. Na área **Manage TPM,** selecione a opção de **bloqueio De Reset TPM** e forneça o ficheiro de palavra-passe do proprietário do TPM.

    O bloqueio do TPM é reposto. O BitLocker restaura o acesso do utilizador ao dispositivo.

    > [!IMPORTANT]
    > Não partilhe o valor do haxixe tpm ou o ficheiro de senha do proprietário do TPM.

## <a name="drive-recovery"></a>Recuperação de unidades

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a>Recuperar uma unidade em modo de recuperação

As unidades entram em modo de recuperação nos seguintes cenários:

- O utilizador perde ou esquece o seu PIN ou palavra-passe
- A Plataforma de Módulos Fidedignos (TPM) deteta alterações no BIOS ou ficheiros de arranque do computador

Para obter uma senha de recuperação, utilize a área de **recuperação** drive da administração e do site de monitorização.

> [!IMPORTANT]
> As palavras-passe de recuperação expiram após uma única utilização. Nas unidades de S e unidades de dados fixas, a regra de utilização única aplica-se automaticamente. Em unidades amovíveis, aplica-se quando remove e reinsere a unidade.

1. Vá ao site de administração e monitorização `https://webserver.contoso.com/HelpDesk`no navegador web, por exemplo.

1. No painel esquerdo, selecione a área de **recuperação** de unidades.

    ![Página de recuperação de controladores e monitorização bitLocker](media/bitlocker-admin-drive-recovery.png)

1. Se necessário, introduza o domínio e o nome do utilizador do utilizador para ver as informações de recuperação.

1. Para ver uma lista de possíveis chaves de recuperação correspondentes, introduza os primeiros oito dígitos do ID da chave de recuperação. Para obter a chave de recuperação exata, insira toda a chave de recuperação ID.

1. Escolha uma das seguintes opções como **a razão para desbloquear**a unidade:

    - Ordem de arranque do sistema operativo alterada
    - BIOS alterado
    - Ficheiros do sistema operativo modificados
    - Chave de arranque perdida
    - PIN perdido
    - Reset TPM
    - Frase de passe perdida
    - Smartcard perdido
    - Outros

    Depois de **submeter** o formulário, o site devolve uma das seguintes respostas:

    - Se o utilizador tiver várias palavras-passe de recuperação correspondentes, devolve várias correspondências possíveis.

    - A palavra-passe de recuperação e o pacote de recuperação para o utilizador submetido.

        > [!NOTE]
        > Se estiver a recuperar uma unidade danificada, a opção do pacote de recuperação fornece ao BitLocker informações críticas de que necessita para recuperar a unidade.

    - Se não encontrar uma senha de recuperação correspondente, devolve uma mensagem de erro.

    Depois de recuperar a palavra-passe de recuperação e o pacote de recuperação, o site exibe a palavra-passe de recuperação.

1. Para copiar a palavra-passe, selecione **Copy Key**. Para guardar a palavra-passe de recuperação de um ficheiro, selecione **Guardar**.

Para desbloquear a unidade, introduza a palavra-passe de recuperação ou utilize o pacote de recuperação.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a>Recuperar uma unidade móvel

Quando se move uma unidade para um novo computador, porque o TPM é diferente, o BitLocker não aceita o PIN anterior. Para recuperar a unidade em movido, obtenha a chave de recuperação ID para recuperar a senha de recuperação.

Para recuperar uma unidade móvel, utilize a área de **recuperação** drive da administração e do site de monitorização.

1. No computador com a unidade móvel, ligue o computador no modo Ambiente de Recuperação do Windows (WinRE).

1. No WinRE, o BitLocker trata a unidade de OS em movido como uma unidade de dados fixa. O BitLocker exibe o ID da palavra-passe de recuperação da unidade e solicita a palavra-passe de recuperação.

    > [!NOTE]
    > Em algumas situações, durante o processo de arranque, **esqueci-me do PIN** se a opção estiver disponível. Em seguida, introduza o modo de recuperação para visualizar o ID da chave de recuperação.

1. Utilize o ID da chave de recuperação para obter a senha de recuperação do site de administração e monitorização. Para mais informações, consulte [Recuperar uma unidade no modo de recuperação](#bkmk_recovery).

Se configurar a unidade móvel para utilizar um chip TPM no computador original, complete os seguintes passos. Caso contrário, o processo de recuperação está concluído.

1. Depois de desbloquear a unidade, ligue o computador no modo WinRE. Abra um pedido de comando em `manage-bde` WinRE e use o comando para desencriptar a unidade. Esta ferramenta é a única forma de remover o protetor **TPM + PIN** sem o chip TPM original. Para mais informações sobre este comando, consulte [Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Quando estiver completo, ligue o computador normalmente. O Gestor de Configuração aplicará a política BitLocker para encriptar a unidade com o TPM plus PIN do novo computador.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a>Recuperar uma unidade corrompida

Utilize o ID da chave de recuperação para obter um pacote chave de recuperação do site de administração e monitorização. Para mais informações, consulte [Recuperar uma unidade no modo de recuperação](#bkmk_recovery).

1. Guarde o pacote de chaves de **recuperação** no seu computador e, em seguida, copie-o para o computador com a unidade corrompida.

1. Abra um pedido de comando como administrador e escreva o seguinte comando:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Substitua os seguintes valores:

    - `<corrupted drive>`: A letra de unidade da unidade corrompida, por exemplo`D:`
    - `<fixed drive>`: A letra de unidade de acionamento de um disco rígido disponível de tamanho semelhante ou maior do que a unidade corrompida. O BitLocker recupera e move dados sobre a unidade corrompida para a unidade especificada. Todos os dados desta unidade estão sobreescritos.
    - `<key package>`: A localização do pacote chave de recuperação
    - `<recovery password>`: A senha de recuperação associada

    Por exemplo:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Para mais informações sobre este comando, consulte [Repair-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Relatórios

O site de administração e monitorização inclui o Relatório de Auditoria de **Recuperação.** Outros relatórios estão disponíveis no ponto de prestação de serviços do Gestor de Configuração. Para mais informações, consulte os [relatórios do View BitLocker](view-reports.md).

1. Vá ao site de administração e monitorização `https://webserver.contoso.com/HelpDesk`no navegador web, por exemplo.

1. No painel esquerdo, selecione a área **de Relatórios.**

1. A partir da barra de menu superior, selecione o Relatório de Auditoria de **Recuperação**.

Para mais informações sobre este relatório, consulte relatório de auditoria de [recuperação](view-reports.md#bkmk-audit)

> [!TIP]
> Para guardar os resultados do relatório, selecione **Export** on the **Reports** menu bar.
