---
title: Criar aplicações Windows
titleSuffix: Configuration Manager
description: Saiba mais informações sobre a criação e implementação de aplicações do Windows no 'Gestor de Configuração'.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9e59d850a78a8f45f93769003e7a1de99e5634b3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906389"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Criar aplicações do Windows no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Além dos outros requisitos e procedimentos do Gestor de Configuração para a criação de [uma aplicação,](../deploy-use/create-applications.md)também tenha em conta as seguintes considerações quando cria e implementa aplicações para dispositivos Windows.  

## <a name="general-considerations"></a><a name="bkmk_general"></a>Considerações gerais  

O Gestor de Configuração suporta a implementação de formatos de pacotes de aplicações Windows (.appx) e pacote de aplicações (.appxbundle) para dispositivos Windows 8.1 e Windows 10.

Quando criar uma aplicação na consola 'Gestor de Configuração', selecione o ficheiro de instalação de aplicação **Type** as **Windows app package \* (.appx, \* .appxbundle, \* .msix, \* .msixbundle)**. Para obter mais informações sobre a criação de apps em geral, consulte [Criar aplicações.](../deploy-use/create-applications.md) Para obter mais informações sobre o formato MSIX, consulte [suporte para formato MSIX](#bkmk_msix).

> [!Note]  
> Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a>Disponibilize pacotes de aplicativos Windows para todos os utilizadores num dispositivo
<!--1358310-->
Disponibilize uma aplicação com um pacote de aplicações Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é fornecer uma aplicação da Microsoft Store for Business and Education, como Minecraft: Education Edition, a todos os dispositivos utilizados pelos alunos de uma escola. Anteriormente, o Gestor de Configuração apenas suportava a instalação destas aplicações por utilizador. Depois de iniciar sessão num novo dispositivo, um aluno teria de esperar para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada para o dispositivo para todos os utilizadores, podem ser produtivas mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, fornecimento e atualização de diferentes versões do mesmo pacote de aplicações windows num dispositivo, o que pode causar resultados inesperados. Este comportamento pode ocorrer ao utilizar o 'Configuração Manager' para fornecer a aplicação, mas depois permite que os utilizadores atualizem a aplicação a partir da Microsoft Store. Para mais informações, consulte a próxima orientação de passos quando [gerir aplicações da Microsoft Store for Business](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Ao fornecer uma aplicação licenciada offline, o Gestor de Configuração não permite que o Windows a atualize automaticamente a partir da Microsoft Store.  

O Gestor de Configuração suporta o fornecimento de aplicações em todas as versões suportadas do Windows 10.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Para configurar um tipo de implementação de aplicações do Windows para esta funcionalidade, ative a opção de **fornecer esta aplicação a todos os utilizadores do dispositivo**. Para mais informações, consulte [Criar aplicações](../deploy-use/create-applications.md).

> [!Note]  
> Se necessitar de desinstalar uma aplicação aprovisionada a partir de dispositivos aos quais os utilizadores já assinaram, precisa de criar duas implementações de desinstaladas. Direcione a primeira implementação de sinstalação para uma coleção de dispositivos que contenha os dispositivos. Direcione a segunda implementação de saque para uma coleção de utilizadores que contenha os utilizadores que já assinaram em dispositivos com a aplicação provisionada. Ao desinstalar uma aplicação aprovisionada num dispositivo, o Windows atualmente não desinstala essa aplicação para os utilizadores.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a>Suporte para formato MSIX
<!--1357427-->

O Gestor de Configuração suporta o pacote de aplicações do Windows 10 (.msix) e o pacote de aplicações (.msixbundle). O Windows 10 versão 1809 ou posteriormente suporta estes formatos.

- Para uma visão geral do MSIX, veja [mais de perto o MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix).  

- Para como criar uma nova aplicação MSIX, consulte o [suporte MSIX introduzido no Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Converter aplicações para MSIX
<!--3607729, fka 1359029-->

Converta as aplicações existentes do Instalador do Windows (.msi) para o formato MSIX.

#### <a name="prerequisites-for-msix"></a>Pré-requisitos para MSIX

- Um dispositivo de referência que executa a versão 1809 do Windows 1809 ou mais tarde  

- Inscreva-se no Windows neste dispositivo como utilizador com direitos administrativos locais  

- Instale as seguintes aplicações neste dispositivo:  

  - Consola do Configuration Manager  

  - Instale a ferramenta de [embalagem MSIX](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) na Microsoft Store  

  - Instale o controlador de ferramentas de [embalagem MSIX](https://docs.microsoft.com/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Não instale quaisquer outras aplicações ou serviços neste dispositivo. É o seu sistema de referência.

#### <a name="process-to-convert-applications-to-msix-format"></a>Processo de conversão de aplicações para formato MSIX

1. Eleve a consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione o nó de **Aplicações.**  

2. Selecione uma aplicação que tenha um tipo de implementação do Instalador do Windows (.msi).  

    > [!Note]  
    > É necessário aceder ao conteúdo de origem da aplicação a partir do dispositivo de referência.  
    >
    > O nome da aplicação não pode ter personagens especiais. O Gestor de Configuração utiliza o nome da aplicação como nome do ficheiro de saída.  
    >
    > Não instale esta aplicação no dispositivo de referência com antecedência.  

3. Selecione **Converter para . MSIX** na fita.

Quando o assistente estiver concluído, a ferramenta de embalagem MSIX cria um ficheiro MSIX no local especificado no assistente. Durante este processo, o Gestor de Configuração instala silenciosamente a aplicação no dispositivo de referência.

Se o processo falhar, a página sumária aponta para o ficheiro de registo com mais informações. Se houver um erro em capturar o estado do utilizador, assine o Windows. A sessão pode resolver esta questão.

Para utilizar esta aplicação MSIX, primeiro é necessário assiná-la digitalmente para que os clientes confiem nela. Para obter mais informações sobre este processo, consulte os seguintes artigos:

- [MSIX – A Ferramenta de Embalagem MSIX – assinatura do pacote MSIX](https://docs.microsoft.com/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [Como assinar um pacote de aplicativos usando signTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Depois de assinar a aplicação, crie um novo tipo de implementação na aplicação no 'Gestor de Configuração'. Para mais informações, consulte Criar tipos de [implementação para a aplicação](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a>Tipo de implantação da sequência de tarefas

<!--3555953-->

> [!Note]  
> Nesta versão do 'Gestor de Configuração', o tipo de implementação da sequência de tarefas é uma função de pré-lançamento. Para o ativar, consulte [as funcionalidades de pré-lançamento](../../core/servers/manage/pre-release-features.md).  

A partir da versão 2002, pode instalar aplicações complexas utilizando sequências de tarefas através do modelo de aplicação. Adicione um tipo de implementação de sequência de tarefas a uma aplicação para instalar ou desinstalar a aplicação. Este tipo de implementação fornece os seguintes comportamentos:

<!-- - Deploy an app task sequence to a user collection -->

- Exiba a sequência de tarefas da aplicação com um ícone no Centro de Software. Um ícone facilita a descoberta e identificação da sequência de tarefas da aplicação.

- Defina metadados adicionais para a sequência de tarefas da aplicação, incluindo informações localizadas

Só é possível adicionar uma sequência de tarefas de implementação não-Scomo um tipo de implementação numa aplicação. Não são suportadas sequências de tarefas de alto impacto, de implantação de osso ou de atualização de osso. <!--A user-targeted deployment still runs in the user context of the local System account.-->

Quando adicionar este tipo de implementação a uma aplicação, configure as suas propriedades na página de **Sequência de Tarefas.** Para mais informações, consulte as opções de sequência de [ **tarefas** do tipo de implementação](../deploy-use/create-applications.md#bkmk_dt-ts).

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Pré-requisitos para um tipo de implantação de sequência de tarefas

Criar uma sequência de tarefas personalizada:

- Utilize apenas passos de implementação não-OS, por exemplo: **Instalar pacote,** executar linha de **comando,** ou **executar script PowerShell**. Para obter mais informações, incluindo a lista completa de passos suportados, consulte Criar uma sequência de [tarefas para implementações não-S](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- Nas propriedades da sequência de tarefas, o separador **user Notification,** não selecione a opção para uma sequência de tarefas de alto impacto.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Quando cria a aplicação, para adicionar um tipo de implementação de sequência de tarefas, a sua conta de utilizador necessita de permissão para ler sequências de tarefas.<!-- 6348976 --> Utilize uma das seguintes opções para configurar estas permissões:

- Adicione a conta de utilizador do administrador da aplicação ao papel de Analista de **Leitura** embutida. Esta função permite-lhes visualizar todos os objetos do Gestor de Configuração.

- Copie a função de Administrador de **Aplicação** incorporada para criar uma função personalizada. Adicione a permissão **de leitura** no objeto pacote de sequência de **tarefas.**

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Questões conhecidas para um tipo de implementação de sequência de tarefas

- Ainda não é possível implementar uma sequência de tarefas de aplicação para uma coleção de utilizadores

- Não utilize o passo de **instalação** nesta sequência de tarefas. Utilize o passo de pacote de [instalação](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) para instalar aplicações.

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a>Suporte para aplicações universal windows platform (UWP)  

Os dispositivos windows 10 não necessitam de uma chave de sideloading para instalar aplicações de linha de negócio. No entanto, para permitir a sideloading no Windows, a chave de registo `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` deve ter um valor de **1**.  

Se não configurar esta chave de registo, o Configurmanager define automaticamente este valor para **1** na primeira vez que implementa uma aplicação no dispositivo. Se definiu este valor para **0**, o Gestor de Configuração não pode alterar automaticamente o valor e a implementação da sua aplicação de linha de negócio falha.  

Assine digitalmente aplicações de linha de negócio da UWP. Utilize um certificado de assinatura de código que seja fidedigno em cada dispositivo ao qual implementa a aplicação. Utilize certificados do PKI da sua organização ou compre um certificado a um fornecedor de terceiros cujo certificado de raiz pública já é de confiança pelo Windows.  

Para assinar pacotes de aplicativos móveis, utilize a seguinte tabela para determinar o tipo de certificado de assinatura de código a utilizar:

| Pacote  | Symantec  | Não-Symantec  |
|---------|---------|---------|
| Pacotes universal **.appx** em dispositivos móveis do Windows 10 | Sim | Sim |
| **pacotes .xap** | Sim | Não |
| **.appx** pacotes construídos para Windows Phone 8.1 para instalar em dispositivos Móveis Windows 10 | Sim | Não |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a>Implemente aplicações do Instalador do Windows para dispositivos Windows 10 inscritos no MDM  

O tipo de implementação do Windows Installer através do **MDM \* (.msi)** permite criar e implementar aplicações baseadas no Windows Installer para dispositivos inscritos no MDM que executam o Windows 10.  

Quando utilizar este tipo de implantação, considere os seguintes pontos:

- Basta fazer o upload de um único ficheiro com a extensão MSI.  

- O Gestor de Configuração utiliza o código de produto do ficheiro e a versão do produto para deteção de aplicações.  

- O Windows utiliza o comportamento de reinício padrão da aplicação. O Gestor de Configuração não controla o comportamento de reinício da aplicação.  

- São instalados pacotes MSI por utilizador para um único utilizador.  

- Os pacotes MSI por máquina estão instalados para todos os utilizadores do dispositivo.  

- O Gestor de Configuração suporta atualizações de aplicações. O código de produto MSI de cada versão deve ser o mesmo.  
