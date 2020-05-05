---
title: Pré-visualização técnica 1707
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1707 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721319"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1707 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1707. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **A atualização para pré-visualizar a versão 1707 falha quando tem um servidor**de site em modo passivo . Quando executar a versão de pré-visualização 1706 e tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)tem de desinstalar o servidor do site do modo passivo antes de poder atualizar com sucesso o seu site de pré-visualização para a versão 1707. Pode reinstalar o servidor do site do modo passivo depois de o seu site correr a versão 1707.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola, vá para **a Administração** > **Resumo** > servidores de**configuração** > do site**e funções**do sistema do site, e, em seguida, selecione o servidor de site de modo passivo.
  2. No painel de funções do **Sistema do Site,** clique à direita na função **do servidor do Site** e, em seguida, escolha remover **a função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.



**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cliente Peer Cache para ficheiros de instalação expresso para Windows 10 e Office 365
<!-- 1352486 -->
A partir desta versão, peer Cache suporta a distribuição de ficheiros de instalação expresso de conteúdo para o Windows 10 e de ficheiros de atualização para o Office 365. Não são necessárias configurações adicionais.

## <a name="surface-device-dashboard"></a>Painel de instrumentos do Dispositivo de Superfície
<!--1355788-->
O dashboard Surface Device fornece informações sobre os dispositivos Surface encontrados no seu ambiente. Na consola, vá a**Dispositivos**de Superfície **de Monitorização** > . Pode ver o seguinte:
- por cento das Superfícies
- por cento dos modelos Surface
- top cinco versões do sistema operativo

Clique numa secção da tabela **Surface Models** para obter uma lista completa dos dispositivos.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configure e implemente as políticas de Guarda de Aplicações do Windows Defender
<!-- 1351960 -->

[O Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo web sites não confiáveis num recipiente isolado seguro que não é acessível por outras partes do sistema operativo. Nesta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de conformidade do Gestor de Configuração que configura e, em seguida, implantamos para uma coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da Atualização do Criador de outono do Windows 10 (nome de código: RS3). Para testar esta funcionalidade agora, deve utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar

Para criar e implementar as políticas do Windows Defender Application Guard, os dispositivos Windows 10 para os quais implementa a política devem ser configurados com uma política de isolamento de rede. Para mais detalhes, consulte [esta publicação de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Esta capacidade funciona apenas com as atuais construções do Windows 10 Insider. Para testá-lo, os seus clientes devem estar a executar uma recente Construção insider do Windows 10.

### <a name="try-it-out"></a>Experimente!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Para criar uma política, e para navegar nas definições disponíveis:

1. Na consola 'Gestor de Configuração', escolha **Ativos e Conformidade.**
2. No espaço de trabalho **de Ativos e Compliance,** escolha **A** > Proteção de**Pontos Finais** > guarda de**aplicação Windows Defender**.
3. No separador **Home,** no grupo **Criar,** clique em Criar a Política de Guarda de **Aplicações do Windows Defender**.
4. Utilizando o post do blog como referência, pode navegar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Neste lançamento, adicionámos a nova página de **Definição** de Rede ao assistente. Nesta página, especifique a identidade corporativa e defina o limite da sua rede corporativa.<br>Os PCs windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma da Windows Information Protection e outra do Windows Defender Application Guard), e implantá-las para o cliente. Se implementar ambas as políticas, estas listas de isolamento da rede devem coincidir. Se implementar listas que não correspondam ao mesmo cliente, a implementação falhará.
Pode encontrar mais informações sobre como especificar definições de rede na documentação de [Proteção de Informação do Windows](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Quando terminar, complete o assistente e implemente a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Mais recursos
Para ler mais sobre o Windows Defender Application Guard, consulte [esta publicação do blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autónomo de guarda de aplicação do Windows Defender, consulte [esta publicação de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Adicione parâmetros quando implementar scripts PowerShell do Gestor de Configuração

<!-- 1236459 --->

Na última Pré-visualização Técnica, introduzimos uma nova capacidade que permite [criar e executar scripts PowerShell a partir da consola Do Gestor de Configuração](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
Nesta Pré-visualização Técnica, expandimos esta capacidade. O Gestor de Configuração agora lê o script PowerShell e exibe quaisquer parâmetros no Assistente de Script Create. Pode fornecer um valor para o parâmetro no assistente que será utilizado quando o script for executado. Em alternativa, pode deixar o parâmetro em branco. Se o fizer, terá de fornecer um valor para o parâmetro quando executar o script.
Nesta pré-visualização técnica, deve fornecer todos os parâmetros que um script exija. Num lançamento futuro, planeamos tornar opcional o fornecimento de parâmetros de script.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executar scripts PowerShell a partir da consola 'Gestor](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)de Configuração'.
2. Na nova página de **Parâmetros** do Script do Assistente de **Script Criar,** escolha um parâmetro e, em seguida, clique em **Editar**.
3. Forneça um valor de parâmetro para o parâmetro selecionado **e,** em seguida, clique OK .
4. Conclua o assistente.

Quando o script estiver em funcionação, utilizará todos os valores do parâmetro configurado.
