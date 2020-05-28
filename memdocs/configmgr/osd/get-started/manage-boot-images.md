---
title: Gerir imagens de arranque
titleSuffix: Configuration Manager
description: No 'Gestor de Configuração', aprenda a gerir as imagens de arranque do Windows PE que utiliza durante uma implementação do SISTEMA.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4403c8d0c57fba8fb63e3df729fb8a48ff123362
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83732878"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Gerir imagens de boot com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Uma imagem de arranque no Gestor de Configuração é uma imagem [do Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) que é usada durante uma implementação de OS. As imagens de arranque são usadas para iniciar um computador no WinPE. Este Sistema operativo mínimo contém componentes e serviços limitados. O Gestor de Configuração utiliza o WinPE para preparar o computador de destino para a instalação do Windows.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a>Imagens de arranque padrão

O Gestor de Configuração fornece duas imagens de boot padrão: uma para suportar plataformas x86 e outra para suportar plataformas x64. Estas imagens são armazenadas nas pastas *x64* ou *i386* na seguinte partilha no servidor do site: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\` . As imagens de boot padrão são atualizadas ou regeneradas dependendo da ação que tomar.

Considere os seguintes comportamentos para qualquer uma das ações descritas para imagens de boot padrão:

- Os objetos do condutor de origem devem ser válidos. Estes objetos incluem os ficheiros de origem do condutor. Se os objetos não forem válidos, o site não adiciona os controladores às imagens do arranque.  

- As imagens de arranque que não se baseiam nas imagens de boot predefinidas, mesmo que utilizem a mesma versão do Windows PE, não são modificadas.  

- Redistribua as imagens de boot modificadas para pontos de distribuição.  

- Recrie todos os meios que usem as imagens de boot modificadas.  

- Se não quiser que as suas imagens de arranque personalizadas/predefinidas sejam atualizadas automaticamente, não as guarde no local predefinido.  

> [!NOTE]
> A ferramenta de registo do Gestor de Configuração **(CMTrace)** é adicionada a todas as imagens de arranque na Biblioteca de **Software**. Quando estiver no Windows PE, inicie a ferramenta digitando `cmtrace` a partir do pedido de comando.
>
> CMTrace é o espectador predefinido para ficheiros de registo no Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utilize atualizações e manutenção para instalar a versão mais recente do Gestor de Configuração

Ao atualizar a versão do Windows Assessment and Deployment Kit (ADK) e, em seguida, utilizar atualizações e manutenção para instalar a versão mais recente do 'Gestor de Configuração', o site regenera as imagens de boot predefinidas. Esta atualização inclui a nova versão WinPE a partir do Windows ADK atualizado, a nova versão do cliente, controladores e personalizações do Gestor de Configuração. O site não modifica imagens de boot personalizadas.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Upgrade do Gestor de Configuração 2012 para o ramo atual

Ao atualizar o Gestor de Configuração 2012 para o ramo atual, o site regenera as imagens de boot padrão. Esta atualização inclui a nova versão WinPE a partir do Windows ADK atualizado e a nova versão do cliente do Gestor de Configuração. Todas as personalizações de imagem de arranque permanecem inalteradas. O site não modifica imagens de boot personalizadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de arranque

Quando utiliza a ação Pontos de Distribuição de **Atualização** a partir do nó **Boot Images** na consola, o site atualiza a imagem de arranque do alvo com os componentes do cliente, controladores e personalizações.

Pode recarregar a imagem de arranque com a versão mais recente do WinPE a partir do diretório de instalação do Windows ADK. A página **geral** do assistente de Pontos de Distribuição de Atualizações fornece as seguintes informações:

- A versão ADK atual do Windows instalada no servidor do site
- A versão atual do cliente de produção
- A versão Windows ADK do WinPE na imagem de arranque
- A versão do cliente do Gestor de Configuração na imagem de arranque

Se as versões na imagem de arranque estiverem desatualizadas, utilize a opção de **recarregar esta imagem de arranque com a versão atual do Windows PE a partir do Windows ADK**.

> [!Important]  
> Esta ação está disponível para imagens de arranque padrão e personalizadas. Durante este processo para recarregar a imagem de arranque, o site não retém quaisquer personalizações manuais feitas fora do 'Gestor de Configuração'. Estas personalizações incluem extensões de terceiros. Esta opção reconstrói a imagem de arranque utilizando a versão mais recente do WinPE e a versão mais recente do cliente. Apenas as configurações que especifica sobre as propriedades da imagem do arranque são reaplicadas. <!--SCCMDocs issue #1283-->

O nó **Boot Images** também inclui uma nova coluna para (**Versão cliente).** Utilize esta coluna para visualizar rapidamente a versão cliente do Gestor de Configuração em cada imagem de arranque.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a>Personalize uma imagem de arranque  

Quando uma imagem de arranque é baseada na versão WinPE a partir da versão suportada do Windows ADK, pode personalizar ou [modificar uma imagem](#BKMK_ModifyBootImages) de boot da consola. Quando atualiza um site e instala uma nova versão do Windows ADK, as imagens de boot personalizadas não são atualizadas com a nova versão do Windows ADK. Quando isso acontece, não é possível personalizar as imagens de boot na consola 'Gestor de Configuração'. No entanto, continuam a trabalhar como antes da atualização.  

Quando uma imagem de arranque é baseada numa versão diferente do Windows ADK instalada num site, deve personalizar as imagens de arranque. Utilize outro método para personalizar estas imagens de arranque, como a utilização da ferramenta de linha de comando de imagem de implementação (DISM). O DISM faz parte do Windows ADK. Para mais informações, consulte [Personalizar imagens de arranque.](customize-boot-images.md)  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a>Adicione uma imagem de bota  

Durante a instalação do site, o Gestor de Configuração adiciona automaticamente imagens de boot que são baseadas numa versão WinPE a partir da versão suportada do Windows ADK. Dependendo da versão do 'Gestor de Configuração', pode adicionar imagens de arranque com base numa versão WinPE diferente da versão suportada do Windows ADK. Ocorre um erro quando se tenta adicionar uma imagem de arranque que contém uma versão não suportada do WinPE. A lista a seguir é a versão ADK e WinPE suportada atualmente:

|  |  |
|---------|---------|
| Versão do Windows ADK | Windows ADK para Windows 10 |
| Versões Windows PE para imagens de arranque personalizáveis a partir da consola Do Gestor de Configuração | Windows PE 10 |
| Versões suportadas pelo Windows PE para imagens de arranque *não personalizáveis* a partir da consola Do Gestor de Configuração | - Windows PE 3.1<sup>[Nota 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

Por exemplo, utilize a consola 'Gestor de Configuração' para personalizar imagens de boot com base no Windows PE 10 a partir do Windows ADK para windows 10. Para uma imagem de arranque baseada no Windows PE 5, personalize-a a partir de um computador diferente utilizando a versão do DISM do Windows ADK para windows 8. Em seguida, adicione a imagem de boot personalizada à consola 'Gestor de Configuração'. Para obter mais informações, veja os seguintes artigos:

- [Personalizar imagens de arranque](customize-boot-images.md)
- [Suporte para Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [Plataformas apoiadas pelo DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Nota 1: Suporte para Windows PE 3.1**
>
> Adicione apenas uma imagem de arranque ao Gestor de Configuração com base na *versão 3.1 do*Windows PE . Atualize o Windows AIK para o Windows 7 (com base no Windows PE 3.0) com o Suplemento Windows AIK para windows 7 SP1 (com base no Windows PE 3.1). Baixe o suplemento Windows AIK para windows 7 SP1 a partir do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó **Boot Images.**  

2. No separador **Casa** da fita, no grupo **Criar,** selecione **Adicionar Imagem de Bota**. Esta ação inicia o Assistente de Imagem add boot.  

3. Na página Fonte de **Dados,** especifique as seguintes opções:  

    - Na caixa **Caminho**, especifique o caminho do ficheiro WIM da imagem de arranque. O caminho especificado tem de ser um caminho de rede válido no formato UNC. Por exemplo: `\\ServerName\ShareName\BootImageName.wim`

    - Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de boot, selecione a imagem apropriada.  

4. Na página **Geral,** especifique as seguintes opções:  

    - Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

    - Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

    - Na caixa **de comentários,** especifique uma breve descrição de como utiliza a imagem do arranque.  

5. Conclua o assistente.  

A imagem de arranque está agora listada no nó **boot Image.** Antes de utilizar a imagem de arranque para implantar um SISTEMA, distribua a imagem do arranque para pontos de distribuição.

> [!Tip]  
> No nó boot **Image** da consola, a coluna **Size (KB)** apresenta o tamanho descomprimido para cada imagem de arranque. Quando o site envia uma imagem de arranque sobre a rede, envia uma cópia comprimido. Esta cópia é tipicamente menor do que o tamanho listado na coluna **Tamanho (KB).**  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a>Distribua imagens de boot  

As imagens de arranque são distribuídas para pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Antes de implementar um SISTEMA ou criar meios de comunicação, distribua a imagem do arranque para pelo menos um ponto de distribuição.

Para obter mais informações sobre como distribuir uma imagem de arranque, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Para utilizar o PXE para implementar um SISTEMA, considere os seguintes pontos antes de distribuir a imagem de arranque:  

- Configure o ponto de distribuição para aceitar pedidos de PXE.  
- Distribua um x86 e uma imagem de bota ativada por X64 PXE para pelo menos um ponto de distribuição ativado por PXE.  
- O Gestor de Configuração distribui as imagens de boot para a pasta **RemoteInstall** no ponto de distribuição ativado pelo PXE.  
  
Para obter mais informações sobre a utilização do PXE para implementar sistemas operativos, consulte [o Use PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a>Modificar uma imagem de arranque  

Adicione ou remova os controladores do dispositivo à imagem ou edite as propriedades da imagem do arranque. Os condutores que adiciona ou remove podem incluir condutores de rede ou armazenamento. Ao modificar imagens de arranque, considere os seguintes fatores:  

- Antes de adicionar os condutores à imagem do arranque, importe e ative-os no catálogo do controlador do dispositivo.  

- Quando modifica uma imagem de arranque, a imagem de arranque não altera nenhum dos pacotes associados que a imagem do arranque refere.  

- Depois de efazer alterações na imagem de arranque, **atualize** a imagem de arranque nos pontos de distribuição que já a têm. Este processo disponibiliza a versão mais atual da imagem de arranque aos clientes. Para mais informações, consulte [Gerir o conteúdo que distribuiu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Modificar as propriedades de uma imagem de arranque  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó **Boot Images.**  

2. Selecione a imagem de arranque que pretende modificar.  

3. No separador **Casa** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

4. Defina qualquer uma das seguintes definições para alterar o comportamento da imagem de arranque:  

#### <a name="images"></a>Imagens

No separador **Imagens,** se alterar as propriedades da imagem da bota utilizando uma ferramenta externa, selecione **Recarregar**.  

#### <a name="drivers"></a>Controladores

No separador **Controladores,** adicione os controladores do dispositivo Windows que o WinPE necessita para arrancar. Considere os seguintes pontos quando adicionar controladores de dispositivos:  

- Certifique-se de que os condutores que adiciona à imagem do arranque correspondem à arquitetura da imagem do arranque.  

- Para apenas exibir os condutores para a arquitetura da imagem do arranque, selecione **Ocultar condutores que não correspondam à arquitetura da imagem do arranque**. A arquitetura do condutor baseia-se na arquitetura relatada no INF do fabricante.  

- WinPE já vem com muitos condutores embutidos. Adicione apenas controladores de rede e armazenamento que não estejam incluídos no WinPE.  

- Adicione apenas controladores de rede e armazenamento à imagem de arranque, a menos que existam requisitos para outros condutores no WinPE.  

- Para apenas exibir controladores de armazenamento e rede, selecione Ocultar controladores que não estejam numa classe de **armazenamento ou rede (para imagens de arranque)**. Esta opção também esconde outros condutores que normalmente não são necessários para imagens de arranque, como condutores de vídeo ou modem.  

- Para ocultar condutores que não tenham uma assinatura digital válida, selecione **Ocultar condutores que não estejam assinados digitalmente**.  

> [!NOTE]  
> Importe os condutores de dispositivos no catálogo de condutores antes de os adicionar a uma imagem de arranque. Para obter informações sobre como importar condutores de dispositivos, consulte [Gerir condutores](manage-drivers.md).  

#### <a name="customization"></a>Personalização

No separador **Personalização**, selecione qualquer uma das seguintes definições:  

- Selecione a opção **Comandos Enable Prestart** para especificar um comando a executar antes da sequência de tarefas ser executada. Quando ativar esta opção, especifique também a linha de comando a executar e quaisquer ficheiros de suporte necessários pelo comando.  

    > [!WARNING]  
    > Adicione `cmd /c` ao início da linha de comando. Se não `cmd /c` especificar, o comando não fecha depois de ser executado. O destacamento continua à espera que o comando termine e não iniciará quaisquer outros comandos ou ações configurados.  

    > [!TIP]  
    > Durante a criação de meios de sequência de tarefas, o assistente escreve a linha de comando id do pacote e prestat para o ficheiro **CreateTSMedia.log.** Esta informação inclui o valor para quaisquer variáveis de sequência de tarefas. Este registo está no computador que executa a consola 'Gestor de Configuração'. Reveja este ficheiro de registo para verificar os valores das variáveis da sequência de tarefas.  

- Configure as definições de **Fundo do Windows PE** para especificar se pretende utilizar o fundo predefinido do WinPE ou um fundo personalizado.  

- Configure o espaço de **risco Windows PE (MB)**, que é armazenamento temporário (unidade RAM) utilizado pela WinPE. Por exemplo, quando uma aplicação é executada no WinPE e tem de escrever ficheiros temporários, o WinPE redireciona os ficheiros para o espaço scratch na memória, para simular a presença de um disco rígido. Por predefinição, este valor é de 512 MB para dispositivos com mais de 1 GB de RAM, caso contrário a predefinição é de 32 MB.  

- Selecione **Ativar suporte de comando (apenas teste)** para abrir uma linha de comandos com a tecla **F8** quando a imagem de arranque estiver a ser implementada. Esta opção é útil para resolução de problemas enquanto está a testar a sua implementação. A utilização deste cenário numa implantação de produção não é aconselhada por questões de segurança.  

- **Desdefinido o layout padrão do teclado no WinPE:** <!--4910348-->A partir da versão 1910, configure o layout padrão do teclado para uma imagem de arranque. Se selecionar um idioma diferente do en-us, o Gestor de Configuração ainda inclui en-us nos locais de entrada disponíveis. No dispositivo, o layout inicial do teclado é o local selecionado, mas o utilizador pode mudar o dispositivo para en-us, se necessário.

> [!Tip]
> Utilize o cmdlet [Set-CMBootImage](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) PowerShell para configurar estas definições a partir de um script.

#### <a name="optional-components"></a>Componentes Opcionais

No separador **Componentes Opcionais,** especifique os componentes adicionados ao Windows PE para utilização com o Gestor de Configuração. Para obter mais informações sobre os componentes opcionais disponíveis, veja [WinPE: adicionar pacotes (Referência dos Componentes Opcionais)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Os seguintes componentes são exigidos pelo Gestor de Configuração e sempre adicionados às imagens de arranque:

- Scripting (WinPE-Scripting)
- Arranque (WinPE-SecureStartup)
- Rede (WinPE-WDS-Tools)
- Scripting (WinPE-WMI)

A lista **de Componentes** mostra itens adicionais que são adicionados a esta imagem de arranque. Para adicionar mais componentes, selecione o asterisco dourado. Para remover um componente, selecione-o da lista e, em seguida, selecione o X vermelho.

Os seguintes componentes são comumente utilizados pelos clientes:

- Microsoft .NET (WinPE-NetFX): Este componente é um pré-requisito para a PowerShell. É um dos maiores componentes opcionais.  
- Windows PowerShell (WinPE-PowerShell): Este componente requer .NET e adiciona suporte limitado powerShell. Se executar scripts PowerShell personalizados durante a fase WinPE da sua sequência de tarefas, adicione este componente. Existem outros componentes que podem ser necessários para outros cmdlets PowerShell.
- HTML (WinPE-HTA): Se executar aplicações HTML personalizadas durante a fase WinPE da sua sequência de tarefas, adicione este componente.

Para mais informações sobre a adição de idiomas, consulte [Configurar várias línguas](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>Origem de Dados

No separador **Origem de Dados**, atualize qualquer uma das seguintes definições:  

- Para alterar o ficheiro fonte da imagem do arranque, detete o **caminho de imagem** e o índice de **imagem**.  

- Para criar uma programação para quando o site atualizar a imagem de arranque, selecione Pontos de **distribuição de Atualização numa programação**.  

- Se não quiser que o conteúdo deste pacote esmalte fora da cache do cliente para dar espaço a outros conteúdos, selecione **conteúdo Persist na cache**do cliente .  

- Para especificar que o site só distribui ficheiros alterados quando atualiza o pacote de imagem de arranque no ponto de distribuição, selecione **A replicação diferencial binária de Ativação** (BDR). Esta definição minimiza o tráfego de rede entre os sites. BDR é especialmente útil quando o pacote de imagem de arranque é grande e as alterações são relativamente pequenas.  

- Se utilizar a imagem de arranque numa implementação ativada pelo PXE, selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado pelo PXE**. Para mais informações, consulte [Use PXE para implementar o Windows sobre a rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Acesso a Dados

No separador **Data Access,** pode configurar as definições de partilha de pacotes. Se necessário no seu ambiente, dejuste a opção de copiar o conteúdo deste pacote para uma partilha de **pacote saque em pontos**de distribuição . Em seguida, tem a opção adicional de **usar um nome personalizado para a partilha do pacote** e especificar o nome de **partilha**personalizado . É necessário um espaço adicional em disco nos pontos de distribuição quando ativar esta opção. Aplica-se a todos os pontos de distribuição que recebem esta imagem de arranque.

#### <a name="distribution-settings"></a>Definições de distribuição

No separador **Definições de Distribuição**, selecione qualquer uma das seguintes definições:  

- Na lista **de prioridades** de Distribuição, especifique o nível prioritário. O Gestor de Configuração utiliza esta lista de prioridades quando o site distribui vários pacotes para o mesmo ponto de distribuição.  

- Se pretender ativar a distribuição de conteúdos a pedido para pontos de distribuição preferidos, selecione **Enable para distribuição a pedido**. Quando ativa esta definição, se um cliente solicitar o conteúdo para o pacote e o conteúdo não estiver disponível em quaisquer pontos de distribuição, então o ponto de gestão distribui o conteúdo. Para mais informações, consulte a [distribuição de conteúdos a pedido.](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)  

- Para especificar como pretende que o site distribua a imagem de arranque em pontos de distribuição que estejam ativados para conteúdo pré-encenado, detete as definições de ponto de **distribuição pré-encenada**. Para obter mais informações sobre conteúdo pré-configurado, veja [Pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>Localização de Conteúdos

No separador **Localização de Conteúdo,** selecione o grupo de pontos de distribuição ou ponto de distribuição e utilize as seguintes ações:  

- **Validar**: Verifique a integridade do pacote de imagem de arranque no ponto de distribuição selecionado ou no grupo de pontos de distribuição.  

- **Redistribuição**: Distribua novamente a imagem de arranque para o ponto de distribuição selecionado ou grupo de pontos de distribuição.  

- **Remover**: Elimine a imagem de arranque do ponto de distribuição selecionado ou do grupo de pontos de distribuição.  

#### <a name="security"></a>Segurança

No separador **Segurança,** consulte os utilizadores administrativos que tenham permissões a este objeto.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a>Configure uma imagem de bota para PXE  

Antes de poder utilizar uma imagem de arranque para uma implementação baseada em PXE, configure a imagem de arranque para ser implementada a partir de um ponto de distribuição ativado por PXE.  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó **Boot Images.**  

2. Selecione a imagem de arranque que pretende modificar.  

3. No separador **Casa** da fita, no grupo **Propriedades,** selecione **Propriedades**.  

4. No separador **Origem de Dados**, selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE**. Para mais informações, consulte [Use PXE para implementar o Windows sobre a rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a>Configurar vários idiomas

> [!TIP]
> A partir da versão 1910, configure o layout padrão do teclado nas propriedades de uma imagem de arranque. Para mais informações, consulte [Personalização](#customization).<!--4910348-->

As imagens de arranque são independentes de idiomas. Esta funcionalidade permite-lhe utilizar uma imagem de boot para exibir o texto da sequência de tarefas em vários idiomas enquanto estiver no WinPE. Inclua o suporte linguístico apropriado do separador Componentes **Opcionais** da imagem de arranque. Em seguida, detete a variável de sequência de tarefa apropriada para indicar qual o idioma a apresentar. A linguagem do Sistema operativo é independente da língua em WinPE. O idioma que o WinPE exibe ao utilizador é determinado da seguinte forma:  

- Quando um utilizador executa a sequência de tarefas a partir de um SISTEMA existente, o Gestor de Configuração utiliza automaticamente o idioma configurado para o utilizador. Quando a sequência de tarefas funciona automaticamente como resultado de um prazo de implementação obrigatório, o Gestor de Configuração utiliza o idioma do SISTEMA.  

- Para implementações de OS que utilizem PXE ou meios de comunicação, detete o valor de ID de idioma na variável **SMSTSLanguageFolder** como parte de um comando prestart. Quando o computador inicia o WinPE, as mensagens são apresentadas no idioma que especificou na variável. Se houver um erro de acesso ao ficheiro de recursos linguísticos na pasta especificada, ou se não definir a variável, o WinPE exibe mensagens no idioma predefinido.  

    > [!NOTE]  
    > Quando protege os meios de comunicação com uma palavra-passe, o texto que solicita ao utilizador a palavra-passe é sempre apresentado no idioma WinPE.  

Utilize o seguinte procedimento para definir a linguagem WinPE para implementações de OS PXE ou iniciadas pelos meios de comunicação.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Detete o idioma DO Windows PE para uma implementação de SO pXE ou iniciado pelos meios de comunicação  

1. Antes de atualizar a imagem de arranque, verifique se o ficheiro de recurso de sequência de tarefas apropriado (tsres.dll) está na pasta de idioma correspondente no servidor do site. Por exemplo, o ficheiro de recursos ingleses encontra-se no seguinte local:`<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Como parte do seu comando prestart, detete a variável ambiente **SMSTSLanguageFolder** para o ID de idioma apropriado. O ID de idioma deve ser especificado utilizando o formato decimal e não hexadecimal. Por exemplo, para definir o ID linguístico para inglês, especifique o valor decimal **1033**, e não o valor hexadecimal 00000409 do nome da pasta.  
