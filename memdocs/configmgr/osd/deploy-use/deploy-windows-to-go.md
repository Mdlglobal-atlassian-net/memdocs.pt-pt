---
title: Implementar janelas para ir
titleSuffix: Configuration Manager
description: Aprenda a fornecer o Windows To Go in Configuration Manager para criar um espaço de trabalho windows to go que botas a partir de uma unidade externa.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0174cea761da15cc57eeb55fba26070fe664bb76
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710966"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Implementar windows para ir com gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico fornece os passos para fornecer windows to go in Configuration Manager. O Windows To Go é uma funcionalidade empresarial do Windows 8 que permite a criação de uma área de trabalho do Windows To Go que pode arrancar a partir de uma unidade externa ligada por USB em computadores que cumpram os requisitos de certificação do Windows 7 ou do Windows 8, independentemente do sistema operativo em execução no computador. As áreas de trabalho do Windows To Go podem utilizar a mesma imagem que as empresas utilizam nos seus computadores de secretária e portáteis e podem ser geridas da mesma forma.  

 Para mais informações sobre o Windows To Go, consulte a visão geral da [funcionalidade Windows To Go](https://go.microsoft.com/fwlink/p/?LinkId=263433).  

## <a name="provision-windows-to-go"></a>Aprovisionar o Windows To Go  
 O Windows To Go é um sistema operativo armazenado numa unidade externa ligada por USB. Pode aprovisionar a unidade do Windows To Go tal como aprovisiona outras implementações de sistema operativo. No entanto, uma vez que o Windows To Go foi concebido para ser uma solução centrada no utilizador e com elevada mobilidade, tem de adotar uma abordagem ligeiramente diferente ao aprovisionamento destas unidades.  

 A um nível elevado, o Windows To Go é uma implementação de duas fases que lhe permite configurar o dispositivo do Windows To Go e pré-configurar conteúdo para a implementação do sistema operativo. Pode conseguir isso com o mínimo impacto para o utilizador e limitar o tempo de inatividade para o computador do utilizador. Depois de pré-configurar o computador, tem de concluir o processo de aprovisionamento para garantir que o computador fica pronto para o utilizador. O processo de aprovisionamento é semelhante ao processo de implementação do sistema operativo atual. Segue-se o fluxo de trabalho geral para pré-configurar conteúdo e aprovisionar o Windows To Go:  

1.  [Pré-requisitos para fornecer Windows To Go](#BKMK_Prereqs)  

2.  [Criar meios pré-encenados](#BKMK_CreatePrestagedMedia)  

3.  [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Atualizar a sequência de tarefas para ativar o BitLocker para o Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Implementar o pacote do Windows To Go Creator e a sequência de tarefas](#BKMK_Deployments)  

6.  [O utilizador executa o Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuração Manager configuras e encena a unidade Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [Utilizador inicia login no Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Pré-requisitos para aprovisionar o Windows To Go  
 Antes de fornecer o Windows To Go, deve completar o seguinte em 'Gestor de Configuração':  

-   **Distribuir uma imagem de arranque para um ponto de distribuição**  

     antes de criar o suporte de dados pré-configurado, tem de distribuir a imagem de arranque a um ponto de distribuição.  

    > [!NOTE]  
    >  As imagens de arranque são usadas para instalar o sistema operativo nos computadores de destino no ambiente do Gestor de Configuração. Contêm uma versão do Windows PE que instala o sistema operativo, bem como os controladores de dispositivo adicionais que sejam necessários. O Gestor de Configuração fornece duas imagens de boot: uma para suportar plataformas x86 e outra para suportar plataformas x64. Também pode criar imagens de arranque próprias. Para mais informações, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

-   **Distribuir a imagem do sistema operativo Windows 8 para um ponto de distribuição**  

     antes de criar o suporte de dados pré-configurado, tem de distribuir a imagem do sistema operativo Windows 8 a um ponto de distribuição.  

    > [!NOTE]  
    >  As imagens de sistema operativo são ficheiros com o formato .WIM e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para mais informações, consulte [Gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

-   **Criar uma Sequência de Tarefas para Implementar o Windows 8**  

     tem de criar uma sequência de tarefas para uma implementação do Windows 8 que será referenciar quando criar suportes de dados pré-configurados. Para obter mais informações, consulte Gerir sequências de [tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a> Criar suportes de dados pré-configurados  
 O suporte de dados pré-configurado contém a imagem de arranque utilizada para iniciar o computador de destino e a imagem de sistema operativo aplicada no computador de destino. O computador que for aprovisionado com um suporte de dados pré-configurado pode ser iniciado utilizando a imagem de arranque. Em seguida, o computador pode executar uma sequência de tarefas existente de implementação de sistema operativo para instalar uma implementação completa do sistema operativo. A sequência de tarefas que implementa o sistema operativo não está incluída no suporte de dados.  

 Pode adicionar conteúdo, como aplicações e controladores de dispositivo, para além da imagem do sistema operativo e da imagem de arranque, durante a fase de pré-configuração. Isto reduz o tempo de implementação de um sistema operativo e reduz o tráfego de rede porque o conteúdo já está na unidade.  

 Utilize o procedimento seguinte para criar o suporte de dados pré-configurado.  

#### <a name="to-create-prestaged-media"></a>Para criar um suporte de dados pré-configurado  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, clique em Sequências de **Tarefas**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4. Na página **Selecione o Tipo de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

   -   Selecione **Suporte de dados pré-configurado**.  

   -   Selecione **Permitir a implementação do sistema operativo autónoma** para arrancar a implementação do Windows To Go sem interação do utilizador.  

       > [!IMPORTANT]  
       >  Quando utiliza esta opção com a variável personalizada SMSTSPreferredAdvertID (definida mais adiante neste procedimento), não é necessária qualquer interação do utilizador e o computador arrancará automaticamente na implementação do Windows To Go quando detetar uma unidade do Windows To Go. Ainda assim, será solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe. Se utilizar a definição **Permitir a implementação do sistema operativo autónoma** sem configurar a variável SMSTSPreferredAdvertID, ocorrerá um erro quando implementar a sequência de tarefas.  

5. Na página **Gestão de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

   -   Selecione **Suporte de dados dinâmico** se pretender permitir que um ponto de gestão redirecione o suporte de dados para outro ponto de gestão, com base na localização do cliente nos limites do site.  

   -   Selecione **Suporte de dados baseado no site** se pretender que o suporte de dados entre em contacto apenas com o ponto de gestão especificado.  

6. Na página **Propriedades do Suporte de Dados**  , especifique as informações seguintes e, em seguida, clique em **Seguinte**.  

   -   **Criado por**: especifique quem criou o suporte de dados.  

   -   **Versão**: especifique o número de versão do suporte de dados.  

   -   **Comentário**: especifique uma descrição exclusiva da finalidade do suporte de dados.  

   -   **Ficheiro do suporte de dados**: especifique o nome e o caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo: ** \\\servername\folder\outputfile.wim**  

7. Na página **Segurança** , especifique as seguintes informações e clique em **Seguinte**.  

   -   Selecione **Ativar suporte de computador desconhecido** para permitir que os meios de comunicação implementem um sistema operativo para um computador que não seja gerido pelo Gestor de Configuração. Não há registo destes computadores na base de dados do Diretor de Configuração. Os computadores desconhecidos incluem o seguinte:  

       -   Um computador onde o cliente do Gestor de Configuração não está instalado  

       -   Um computador que não é importado para O Gestor de Configuração  

       -   Um computador que não é descoberto pelo Gestor de Configuração  

   -   Selecione **Proteger suporte de dados com uma palavra-passe** e introduza uma palavra-passe segura para ajudar a proteger o suporte de dados contra acesso não autorizado. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados pré-configurado.  

       > [!IMPORTANT]  
       >  Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados pré-configurado.  

       > [!NOTE]  
       >  Quando protege o suporte de dados pré-configurado com uma palavra-passe, esta é solicitada ao utilizador mesmo quando o suporte de dados está configurado com a definição **Permitir a implementação do sistema operativo autónoma** .  

   -   Para comunicações HTTP, selecione **Criar um certificado de suporte de dados autoassinado**e especifique as datas de início e de expiração do certificado.  

   -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a importar e a respetiva palavra-passe.  

        Para obter mais informações sobre este certificado de cliente que é utilizado para imagens de arranque, consulte [os requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Afinidade do Dispositivo do Utilizador**: Para apoiar a gestão centrada no utilizador no Gestor de Configuração, especifique como pretende que os meios de comunicação associem os utilizadores ao computador de destino. Para obter mais informações sobre como a implementação do sistema operativo suporta a afinidade do dispositivo do utilizador, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino .  

       -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação automática** se pretender que o suporte de dados associe automaticamente utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o sistema operativo no computador de destino.  

       -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação pendente pelo administrador** se pretender que o suporte de dados associe utilizadores ao computador de destino após concessão da aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do sistema operativo.  

       -   Especifique **Não permitir afinidade dispositivo/utilizador** se não pretender que o suporte de dados associe utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa utilizadores ao computador de destino durante a implementação do sistema operativo.  

8. Na página **Sequência de Tarefas** , especifique a sequência de tarefas do Windows 8 que criou na secção anterior.  

9. Na página **Imagem de arranque** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de arranque que é distribuída deve ser adaptada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86. Para computadores com certificação do Windows 8 no modo EFI, tem de utilizar uma imagem de arranque x64.  

    -   **Imagem de arranque**: especifique a imagem de arranque para iniciar o computador de destino.  

    -   **Ponto de distribuição**: especifique o ponto de distribuição que aloja a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  O utilizador administrativo tem de ter direitos de acesso de **Leitura** para o conteúdo da imagem de arranque no ponto de distribuição. Para mais informações, consulte a conta de acesso ao [pacote](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Se tiver selecionado **Suporte de dados baseado no site** na página **Gestão de Suporte de Dados** deste assistente, na caixa **Ponto de gestão** , especifique um ponto de gestão de um site primário.  

    -   Se tiver selecionado **Suporte de dados dinâmico** na página **Gestão de Suporte de Dados** do assistente, na caixa **Pontos de gestão associados** , especifique os pontos de gestão do site primário a utilizar e uma ordem de prioridades para as comunicações iniciais.  

10. Na página **Imagens** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Pacote de imagens**: especifique o pacote que contém a imagem do sistema operativo Windows 8.  

    -   **Índice de imagens**: especifique a imagem a implementar se o pacote contiver várias imagens de sistema operativo.  

    -   **Ponto de distribuição**: especifique o ponto de distribuição que aloja o pacote da imagem do sistema operativo. O assistente obtém a imagem do sistema operativo a partir do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  O utilizador administrativo tem de ter direitos de acesso de **Leitura** para o conteúdo da imagem de sistema operativo no ponto de distribuição. Para mais informações, consulte a conta de acesso ao [pacote](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. Na página **Selecionar Aplicação** , selecione conteúdo de aplicações a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

12. Na página **Selecionar Pacote** , selecione conteúdo de pacote adicional a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

13. Na página **Selecionar o Pacote do Controlador** , selecione conteúdo de pacote de controladores a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

14. Na página **Pontos de Distribuição** , selecione um ou vários pontos de distribuição que contenham o conteúdo exigido pela sequência de tarefas e clique em **Seguinte**.  

15. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    - **Variáveis**: especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo. Para o Windows To Go, utilize a variável SMSTSPreferredAdvertID para selecionar automaticamente a implementação do Windows To Go utilizando o seguinte formato:  

       SMSTSPreferredAdvertID = {*IDdaImplementação*}, em que IDdaImplementação é o ID da implementação associado à sequência de tarefas que irá utilizar para concluir o processo de aprovisionamento para a unidade do Windows To Go.  

      > [!TIP]  
      >  Quando utiliza esta variável com uma sequência de tarefas definida para execução automática (definida mais adiante neste procedimento), não é necessária qualquer interação do utilizador e o computador arranca automaticamente na implementação do Windows To Go quando detetar uma unidade do Windows To Go. Ainda assim, será solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

    - **Comandos de pré-início**: especifique os comandos de pré-início que pretende executar antes da execução da sequência de tarefas. Os comandos de pré-início podem ser um script ou um ficheiro executável que podem interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Configure as seguintes variáveis para a implementação do Windows To Go:  

      - **OSDBitLockerPIN**: o BitLocker para Windows To Go necessita de uma frase de acesso. Defina a variável **OSDBitLockerPIN** como parte de um comando de pré-início para definir a frase de acesso do BitLocker para a unidade do Windows To Go.  

        > [!WARNING]  
        >  Quando o BitLocker tiver a frase de acesso ativada, o utilizador terá de introduzir a frase de acesso sempre que o computador arrancar na unidade do Windows To Go.  

      - **SMSTSUDAUsers**: especifica o utilizador primário do computador de destino. Utilize esta variável para recolher o nome do utilizador, que pode então ser utilizado para associar o utilizador e o dispositivo. Para mais informações, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino.  

        > [!TIP]  
        >  Para obter o nome de utilizador, pode criar uma caixa de introdução como parte do comando de pré-início, para o utilizador introduzir o respetivo nome de utilizador, e, em seguida, definir a variável com o valor. Por exemplo, pode adicionar as seguintes linhas ao ficheiro de script do comando de pré-início:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Para obter mais informações sobre como criar um ficheiro script para usar como seu comando prestart, consulte [comandos Prestart para meios](../understand/prestart-commands-for-task-sequence-media.md)de sequência de tarefas .  

16. Conclua o assistente.  

    > [!NOTE]  
    >  A conclusão do ficheiro do suporte de dados pré-configurado pelo assistente poderá demorar bastante tempo.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a>Criar um pacote Windows To Go Creator  
 Como parte da implementação do Windows To Go, tem de criar um pacote para implementar o ficheiro de suporte de dados pré-configurado. O pacote tem de incluir a ferramenta que configura a unidade do Windows To Go e extrai o suporte de dados pré-configurado para a unidade. Utilize o procedimento seguinte para criar o pacote do Windows To Go Creator.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Para criar o pacote do Windows To Go Creator  

1. No servidor para alojar os ficheiros do pacote do Windows To Go Creator, crie uma pasta de origem para os ficheiros de origem do pacote.  

   > [!NOTE]  
   >  A conta de computador do servidor do site tem de ter direitos de acesso de **Leitura** para a pasta de origem.  

2. Copie o ficheiro de suporte de dados pré-configurado criado na secção [Create prestaged media](#BKMK_CreatePrestagedMedia) para a pasta de origem do pacote.  

3. Copie a ferramenta Windows To Go Creator (WTGCreator.exe) para a pasta de origem do pacote. A ferramenta criadora está disponível em qualquer servidor de site primário no seguinte local: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\Creator.  

4. Crie um pacote e um programa utilizando o Assistente para Criar Pacote e Programa.  

5. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

6. Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

7. No separador **Home Page** , no grupo **Criar** , clique em **Criar Pacote**.  

8. Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, introduza o **Windows To Go** para obter o nome do pacote e especifique o Pacote para configurar uma unidade windows to go utilizando o 'Gestor de **Configuração'** para a descrição do pacote.  

9. Selecione **Este pacote contém ficheiros de origem**, especifique o caminho da pasta de origem do pacote que criou no passo 1 e clique em **Seguinte**.  

10. Na página **Tipo de Programa** , selecione **Programa padrão**e clique em **Seguinte**.  

11. Na página **Programa Padrão** , especifique o seguinte:  

    -   **Nome**: especifique o nome do programa. Por exemplo, escreva **Creator** para o nome do programa.  

    -   **Linha de Comandos**: escreva **WTGCreator.exe /wim:PrestageName.wim**, em que PrestageName é o nome do ficheiro pré-configurado que criou e copiou para a pasta de origem do pacote, para o pacote do Windows To Go Creator.  

         Opcionalmente, pode adicionar as seguintes opções:  

        -   **enableBootRedirect**: opção da linha de comandos para alterar as opções de arranque do Windows To Go para permitir o redirecionamento do arranque. Quando utilizar esta opção, o computador arrancará a partir do USB sem ter de alterar a ordem de arranque no firmware do computador ou o utilizador ter de selecionar a partir de uma lista de opções durante o arranque. Se for detetada uma unidade do Windows To Go, o computador arrancará nessa unidade.  

    -   **Executar**: especifique **Normal** para executar o programa com base nas predefinições do sistema e programa.  

    -   **Programa pode ser executado**: especifique se o programa pode ser executado apenas quando um utilizador tiver sessão iniciada.  

    -   **Modo de execução**: especifique se o programa será executado com as permissões dos utilizadores com sessão iniciada ou com permissões administrativas. O Windows To Go Creator requer permissões elevadas para ser executado.  

    -   Selecione **Permitir que os utilizadores visualizem e interajam com a instalação do programa**e clique em **Seguinte**.  

12. Na página Requisitos, especifique o seguinte:  

    - **Requisitos da plataforma**: selecione as plataformas do Windows 8 aplicáveis, para permitir o aprovisionamento.  

    - **Espaço em disco estimado**: especifique o tamanho da pasta de origem do pacote do Windows To Go Creator.  

    - **Tempo máximo de execução permitido (minutos)**: especifica o tempo máximo que o programa poderá demorar a ser executado no computador cliente. Por predefinição, este valor é definido para 120 minutos.  

      > [!IMPORTANT]  
      >  Se estiver a utilizar janelas de manutenção para a coleção onde este programa é executado, pode ocorrer um conflito se o **Tempo máximo de execução permitido** for superior à janela de manutenção agendada. Se o tempo de execução máximo for definido para **Desconhecido**, começará durante a janela de manutenção, mas continuará a ser executado até concluir ou falhar depois de a janela de manutenção fechar. Se definir o tempo de execução máximo para um período específico (não definido para Desconhecido) que excede a duração de qualquer janela de manutenção, esse programa não será executado.  

      > [!NOTE]  
      >  Se o valor estiver definido para **Desconhecido,** o Gestor de Configuração define o tempo máximo de funcionamento permitido para 12 horas (720 minutos).  

      > [!NOTE]  
      >  Se o prazo máximo de execução (seja definido pelo utilizador ou como valor predefinido) for ultrapassado, o Gestor de Configuração para o programa se for **executado com direitos administrativos** e **permitir que os utilizadores vejam e interajam com a instalação do programa** não for selecionado na página do Programa **Padrão.**  

      Clique em **Seguinte** e conclua o assistente.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a>Atualize a sequência de tarefas para ativar o BitLocker para o Windows To Go  
 O Windows To Go ativa o BitLocker numa unidade de arranque externa sem a utilização do TPM. Por conseguinte, terá de utilizar uma ferramenta separada para configurar o BitLocker na unidade do Windows To Go. Para ativar o BitLocker, terá de adicionar uma ação à sequência de tarefas após o passo **Configurar Windows e ConfigMgr** .  

> [!NOTE]  
>  O BitLocker para Windows To Go necessita de uma frase de acesso. No passo [Create prestaged media](#BKMK_CreatePrestagedMedia) , defina a frase de acesso enquanto parte de um comando pré-arranque utilizando a variável OSDBitLockerPIN.  

 Utilize o seguinte procedimento para atualizar a sequência de tarefas do Windows 8 para ativar o BitLocker para Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Para atualizar a sequência de tarefas do Windows 8 para ativar o BitLocker  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Pacote**.  

4.  Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, escreva **BitLocker for Windows To Go** para o nome do pacote e especifique **Package to update BitLocker for Windows To Go** para a descrição do pacote.  

5.  Selecione **Este pacote contém ficheiros de origem**, especifique a localização para a ferramenta BitLocker para Windows To Go e clique em **Seguinte**. A ferramenta BitLocker está disponível em qualquer servidor de site primário do Gestor de Configuração no seguinte local: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\BitLocker\  

6.  Na página **Tipo de Programa** , selecione **Não criar um programa**.  

7.  Clique em **Seguinte** e conclua o assistente.  

8.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

9. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, clique em Sequências de **Tarefas**.  

10. Selecione a sequência de tarefas do Windows 8 que referencia nos suportes de dados pré-configurados.  

11. No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar**.  

12. Clique no passo **Configurar Windows e ConfigMgr** , clique em **Adicionar**, clique em **Geral**e, em seguida, clique em **Executar Linha de Comandos**. O passo Executar Linha de Comandos é adicionado após o passo Configurar Windows e ConfigMgr.  

13. No separador **Propriedades** para o passo **Executar Linha de Comandos** , adicione o seguinte:  

    1.  **Nome**: especifique um nome para a linha de comandos, como **Enable BitLocker for Windows To Go**.  

    2.  **Linha de Comando**: i386\osdbitlocker_wtg.exe /Ativar /pwd:< *Nenhum&#124;AD*>  

         Parâmetros:  

        -   /pwd:<Nenhum&#124;> ad - Especifique o modo de recuperação da palavra-passe BitLocker. Este parâmetro obriga que utilize o parâmetro /Enable na linha de comandos.  

             Selecione **AD** para configurar a Encriptação da Unidade do BitLocker para criar cópias de segurança das informações de recuperação para unidades protegidas pelo BitLocker para Serviços de Domínio do Active Directory (AD DS). Criar cópias de segurança de palavras-passe de recuperação para uma unidade protegida pelo BitLocker permite que os utilizadores administrativos recuperem a unidade se estiver bloqueada. Isto garante que os dados encriptados pertencentes à empresa podem ser sempre acedidos por utilizadores autorizados. Quando especificar **Nenhum**, o utilizador é responsável por manter uma cópia da palavra-passe de recuperação ou chave de recuperação. Se o utilizador perder essa informação ou negligenciar a desencriptação da unidade antes de abandonar a organização, os utilizadores administrativos não conseguem aceder facilmente à unidade.  

        -   /espera:<TRUE&#124;FALSO> - Especifique se a sequência de tarefa supor que a encriptação esteja concluída antes de completar.  

    3.  Selecione **pacote**e, em seguida, especifique o pacote que criou no início deste procedimento.  

    4.  No separador **Opções** , adicione as seguintes condições:  

        -   Condição = Variável de Sequência de Tarefas  

        -   Variável = _SMSTSWTG  

        -   Condição = Igual a  

        -   Valor = Verdadeiro  

    > [!NOTE]  
    >  O passo **Ativar o BitLocker** , o mais provável depois do novo passo da linha de comandos, não é utilizado para ativar o BitLocker para Windows To Go. No entanto, pode manter este passo na sequência de tarefas a utilizar para implementações do Windows 8 que não utilizem uma unidade do Windows To Go.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a>Implementar o pacote e sequência de tarefas do Criador do Windows To Go  
 O Windows To Go é um processo de implementação híbrido. Por conseguinte, terá de implementar o pacote do Windows To Go Creator e a sequência de tarefas do Windows 8. Utilize os seguintes procedimentos para concluir o processo de implementação.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Para implementar o pacote do Windows To Go Creator  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

3.  Selecione o pacote Windows To Go que criou no Windows no passo [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage) .  

4.  No separador **Home Page**, no grupo **Implementação**, clique em **Implementar**.  

5.  Na página **Geral** , especifique as seguintes definições:  

    1.  **Software**: certifique-se de que o pacote do Windows To Go está selecionado.  

    2.  **Coleção**: clique em **Procurar** para selecionar a coleção na qual pretende implementar o pacote do Windows To Go.  

    3.  **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: selecione esta opção se pretender armazenar o conteúdo do pacote no grupo de pontos de distribuição predefinido da coleção. Se não tiver associado a coleção selecionada a um grupo de pontos de distribuição, esta opção estará indisponível.  

6.  Na página **Conteúdo** , clique em **Adicionar** e, em seguida, selecione os pontos de distribuição ou os grupos de pontos de distribuição nos quais pretende implementar o conteúdo associado a este pacote e programa.  

7.  Na página **Definições de Implementação** , selecione **Disponível** para o tipo de implementação e, em seguida, clique em **Seguinte**.  

8.  No **Agendamento**, configure quando este pacote e programa serão implementados ou colocados à disposição dos dispositivos cliente.  

     As opções desta página serão diferentes consoante a ação de implementação esteja definida para **Disponível** ou **Necessária**.  

9. No **Agendamento**, confirme as seguintes definições e clique em **Seguinte**.  

    1.  **Agendar quando esta implementação ficará disponível**: especifique a data e a hora em que o pacote e o programa ficarão disponíveis para serem executados no computador de destino. Se selecionar **UTC**, esta definição garantirá que o pacote e programa ficarão disponíveis para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando esta implementação expirará**: especifique a data e a hora em que o pacote e o programa irão expirar no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefas expira em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

10. Na página **Experiência de Utilizador** do Assistente, especifique as seguintes informações:  

    -   **Instalação do software**: permite que o software seja instalado fora de quaisquer janelas de manutenção configuradas.  

    -   **Reinício do sistema (se necessário para concluir a instalação)**: permite que um dispositivo reinicie fora das janelas de manutenção configuradas, quando exigido pela instalação do software.  

    -   **Dispositivos Embedded**: quando implementa pacotes e programas em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalação de pacotes e programas na sobreposição temporária e confirmar as alterações mais tarde, ou confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

11. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implementação:** especificar **Transferir conteúdo do ponto de distribuição e executar localmente**.  

    -   **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: selecione esta opção para reduzir a carga de rede, ao permitir que os clientes transfiram conteúdos a partir de outros clientes na rede que já transferiram e colocaram o conteúdo na cache. Esta opção utiliza o Windows BranchCache e pode ser utilizada em computadores com o Windows Vista SP2 e posterior.  

    -   **Todos os clientes utilizam uma localização de origem de contingência para conteúdo**: especifique se pretende permitir que os clientes revertam e utilizem um ponto de distribuição não preferencial como localização de origem de conteúdo, quando o conteúdo não está disponível num ponto de distribuição preferencial.  

12. Conclua o assistente.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Para implementar a sequência de tarefas do Windows 8  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, clique em Sequências de **Tarefas**.  

3.  Selecione a sequência de tarefas do Windows 8 que criou no passo [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  No separador **Home Page**, no grupo **Implementação**, clique em **Implementar**.  

5.  Na página **Geral** , especifique as seguintes definições:  

    1.  **Sequência de tarefas**: certifique-se de que se encontra selecionada a sequência de tarefas do Windows 8.  

    2.  **Coleção**: clique em **Procurar** para selecionar a coleção que inclui todos os dispositivos para os quais um utilizador pode aprovisionar o Windows To Go.  

        > [!IMPORTANT]  
        >  Se os suportes de dados pré-configurados que criou na secção [Create prestaged media](#BKMK_CreatePrestagedMedia) utilizarem a variável SMSTSPreferredAdvertID, poderá implementar a sequência de tarefas na coleção **Todos os Sistemas** e especificar a definição **Apenas Windows PE (oculto)** na página **Conteúdo** . Porque a sequência de tarefas está oculta, só estará disponível para suportes de dados.  

    3.  **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: selecione esta opção se pretender armazenar o conteúdo do pacote no grupo de pontos de distribuição predefinido da coleção. Se não tiver associado a coleção selecionada a um grupo de pontos de distribuição, esta opção estará indisponível.  

6.  Na página **Definições de Implementação** , configure as seguintes definições e clique em **Seguinte**.  

    -   **Objetivo**: selecione **Disponível**. Quando implementar a sequência de tarefas num utilizador, este verá a sequência de tarefas publicada no Catálogo de Aplicações e poderá solicitá-la a pedido. Se implementar a sequência de tarefas num dispositivo, o utilizador irá ver a sequência de tarefas no Centro de Software e pode instalá-lo a pedido.  

    -   **Disponibilize-se para o seguinte**: Especifique se a sequência de tarefas está disponível para clientes, meios de comunicação ou PXE do Gestor de Configuração.  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Selecione **Permitir implementação de sistema operativo autónoma** e defina a variável SMSTSPreferredAdvertID como parte dos suporte de dados pré-configurados para que o computador arranque automaticamente para a implementação de Windows To Go, sem interação do utilizador quando deteta uma unidade do Windows To Go. Para mais informações sobre estas definições de suporte de dados pré-configurados, consulte a secção [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Na página **Agendamento** , confirme as seguintes definições e clique em **Seguinte**.  

    1.  **Agendar quando esta implementação ficará disponível**: especifique a data e a hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefa ficará disponível para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando esta implementação expirará**: especifique a data e a hora em que a sequência de tarefas irá expirar no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefas expira em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações:  

    -   **Mostrar o progresso**da sequência de tarefas : Especifique se o cliente do Gestor de Configuração apresenta o progresso da sequência de tarefas.  

    -   **Instalação de software**: especifique se o utilizador tem permissão para instalar o software fora das janelas de manutenção configuradas e depois da hora agendada.  

    -   **Reinício do sistema (se necessário para concluir a instalação)**: permite que um dispositivo reinicie fora das janelas de manutenção configuradas, quando exigido pela instalação do software.  

    -   **Dispositivos Embedded**: quando implementa pacotes e programas em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalação de pacotes e programas na sobreposição temporária e confirmar as alterações mais tarde, ou confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

    -   **Clientes baseados na Internet**: especifique se a sequência de tarefas pode ser executada num cliente baseado na Internet. As operações que instalam software, por exemplo um sistema operativo, não são suportadas por esta definição. Só deve utilizar esta opção para sequências de tarefas genéricas, baseadas em scripts, que executem operações padrão do sistema operativo.  

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implementação**: selecione **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**.  

    -   **Se não estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: especifique se os clientes poderão utilizar pontos de distribuição que se encontram em redes lentas e pouco fiáveis para a transferência de conteúdos que sejam necessários para a sequência de tarefas.  

    -   **Permitir que os clientes utilizem uma localização de origem de recuo para conteúdos:**
        - Antes da *versão 1610,* pode selecionar a localização de origem de recuo para a caixa de verificação de conteúdos para permitir que os clientes fora destes grupos de fronteira recuem e utilizem o ponto de distribuição como local de origem para conteúdos quando não existem outros pontos de distribuição disponíveis.
        - *Começando pela versão 1610,* já não é possível configurar a localização da **fonte de recuo para conteúdos**.  Em vez disso, configura relações entre grupos de fronteira que determinam quando um cliente pode começar a procurar grupos de limites adicionais para obter uma localização de fonte de conteúdo válida. 

11. Conclua o assistente.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a>Utilizador executa o Windows To Go Creator  
 Depois de implementar o pacote Windows To Go e a sequência de tarefas do Windows 8, o Windows To Go Creator fica disponível para o utilizador. O utilizador pode ir para o catálogo de software, ou o Centro de Software se o Windows To Go Creator foi implementado em dispositivos, e executar o programa Windows To Go Creator. Depois de o pacote de autor é transferido, será apresentado um ícone intermitente na barra de tarefas. Quando o utilizador clica no ícone, é apresentada uma caixa de diálogo para o utilizador selecionar a unidade do Windows To Go a aprovisionar (exceto se a /opção da linha de comandos da unidade for utilizada). Caso a unidade não satisfaça os requisitos para o Windows To Go ou caso a unidade não tenha espaço livre suficiente no disco para instalar a imagem, o programa de autor apresenta uma mensagem de erro. O utilizador pode verificar a unidade e a imagem que serão aplicadas a partir da página de confirmação. Enquanto o autor configura e prepara conteúdo para a unidade do Windows To Go, apresenta uma caixa de diálogo de progresso. Uma vez concluída a pré-configuração, o criador apresenta um aviso para reiniciar o computador para arrancar para a unidade do Windows To Go.  

> [!NOTE]  
>  Se não tiver ativado o redirecionamento do arranque enquanto parte da linha de comandos para o programa de autor na secção [Create a Windows To Go Creator package](#BKMK_CreatePackage) , é possível que o utilizador tenha de arrancar manualmente a unidade do Windows To Go em cada reinício do sistema.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> O Configuration Manager configura e prepara a unidade do Windows To Go  
 Depois de o computador reiniciar a unidade do Windows To Go, a unidade arrancará no Windows PE e ligar-se-á ao ponto de gestão para obter a política para concluir a implementação do sistema operativo. O Gestor de Configuração configura e encena a unidade. Depois de o Gestor de Configuração ter faseado a unidade, o utilizador pode reiniciar o computador para finalizar o processo de provisionamento (como por exemplo, aderir a um domínio ou instalar aplicações). Este processo é o mesmo para qualquer suporte de dados pré-configurado.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> O utilizador inicia sessão no Windows 8  
 Depois de o Gestor de Configuração completar o processo de provisionamento e o ecrã de bloqueio do Windows 8 ser apresentado, o utilizador pode iniciar sessão no sistema operativo.  
