---
title: Antevisão Técnica 1712 [ Antevisão Técnica 1712 ] Microsoft Docs
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1712 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721277"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1712 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1712. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. 

Reveja a [pré-visualização técnica para o Gestor](technical-preview.md) de Configuração antes de instalar esta versão da pré-visualização técnica. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **A atualização para uma nova versão de pré-visualização falha quando tiver um servidor de site em modo passivo**. Se tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)então tem de desinstalar o servidor do site do modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site do modo passivo depois de o site completar a atualização.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola do Gestor de Configuração, vá a Servidores de**Configuração** > de Site de Visão**Geral** > da **Administração** > **e às Funções**do Sistema do Site, e, em seguida, selecione o servidor do site de modo passivo.
  2. No painel de **funções** do Sistema do Site, clique à direita na função do **servidor do Site** e, em seguida, escolha remover a **função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms489412-->


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualize automaticamente aplicações supersed
<!-- 1351266 -->
Com base no feedback de voz do [utilizador,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)nesta versão tem a opção de configurar uma implementação de aplicação para não atualizar automaticamente qualquer versão supersed. Agora, ao criar a implementação, na página de Definições de **Implementação** do **Assistente de Software de Implementação,** para uma finalção de instalação **disponível** ou **necessária,** pode ativar ou desativar a opção de **atualizar automaticamente quaisquer versões supersed desta aplicação**.


## <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 -->
Se um utilizador final ou técnico de desktop precisar de instalar várias aplicações num dispositivo, o Software Center suporta agora a instalação de várias aplicações selecionadas. Isto permite ao utilizador ser mais eficiente enquanto não espera que uma instalação termine antes de iniciar a seguinte.

Ao utilizar o modo multi-select no separador **Aplicações,** os seguintes critérios determinam quais as aplicações que o Software Center permite para várias seleções:
- A aplicação é visível para o utilizador
- A aplicação ainda não está instalada
- A aprovação do administrador não é necessária ou já está concedida
- O estado da aplicação está disponível (por exemplo, ainda não descarregamento de conteúdo)

### <a name="try-it-out"></a>Experimente!
**Na consola De Configuração Manager:** Implemente para um utilizador ou dispositivo múltiplas aplicações para instalação, conforme disponível ou necessário (com o prazo no futuro). Não requer aprovação do administrador. Para mais informações, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).

**No Centro de Software:**
 1. O separador **Aplicações** deve ser aberto por defeito. 
 2. Para introduzir o modo multi-select na vista da lista, clique no novo ícone ![Ícone multi-selecionado do Software Center](media/software-center-multi-select-apps.png) no canto superior direito.
 3. Selecione duas ou mais aplicações para instalar clicando na caixa de verificação à esquerda das aplicações na lista.
 4. Clique no botão **Instalar Selecionado.**

As aplicações instalam-se normalmente, só agora sucessivamente.


## <a name="client-based-pxe-responder-service"></a>Serviço de resposta PXE baseado no cliente
<!-- 1357148 -->
Um desafio comum para os clientes é fornecer serviços PXE em escritórios remotos/sucursais com pouca ou nenhuma infraestrutura de servidor. A função do ponto de distribuição suporta os sistemas operativos dos clientes, mas não pode ser ativada pelo PXE devido à dependência dos Serviços de Implementação do Windows.

As novas definições de cliente estão agora disponíveis para permitir um serviço de resposta PXE nos clientes do Gestor de Configuração. Uma imagem de arranque ativada por PXE deve residir na cache do cliente do resposta PXE.

### <a name="try-it-out"></a>Experimente!
Certifique-se de que não existem pontos de distribuição ativados por PXE existentes ou outros servidores PXE no ambiente de teste que possam entrar em conflito com este cliente PXE.

Na consola De Configuração Manager:
1. No espaço de trabalho da **Biblioteca** de Software em **sistemas operativos,** sequências de **tarefas:** criar uma sequência de tarefas utilizando o modelo personalizado.
   1. Clique em **Adicionar,** selecione **General,** e depois o passo variável de sequência de **tarefas definido.** Introduza **O SMSTSPersistContent** como variável de sequência de tarefas e introduza o valor **TRUE**.
   1. Clique em **Adicionar,** selecione **Software,** e depois a etapa de **conteúdo do pacote de transferência.** Clique no asterisco dourado e, em seguida, selecione uma imagem de arranque ativada por PXE. Inclua imagens de arranque x86 e x64. Configure o passo para colocá-lo na cache do cliente do Gestor de **Configuração**.
   1. Clique em **Adicionar,** selecione **General,** e depois o passo variável de sequência de **tarefas definido.** Introduza **o SMSTSPreserveContent** como variável de sequência de tarefas e introduza o valor **TRUE**.
2. No espaço de trabalho **da Administração** em Definições de **Cliente:** crie uma política personalizada de definições de dispositivos de cliente.
   1. Selecione o grupo De Configurações de Cache do **Cliente.**
   1. Defina o cliente do Gestor de **Configuração ativa em todo o SISTEMA para partilhar** a definição de conteúdo para **Sim**.
   1. Defina a definição de serviço de **resposta Enable PXE** para **Sim**.
   1. Para criar **um certificado auto-assinado ou importar uma** definição de certificado de cliente PKI, clique em Fornecer um **certificado**. Selecione **certificado de importação** se o seu ambiente de teste tiver PKI, caso contrário clique em **OK** para criar um certificado auto-assinado. 
   1. Configure as definições restantes conforme necessário para o seu ambiente de teste. (As definições predefinidas devem funcionar a menos que existam requisitos específicos de rede ou de segurança.)
3. Implemente a sequência de tarefas e as definições personalizadas do cliente para uma coleção de clientes-alvo para serem respostas PXE. Aguarde a aplicação das políticas e a sequência de tarefas será executada.
4. Inicie outro cliente na mesma subnet para PXE/bota de rede normal.

### <a name="known-issues"></a>Problemas conhecidos
- O editor da sequência de tarefas exibe um ícone de erro vermelho para o passo de conteúdo do **pacote de transferência** quando adiciona uma imagem de arranque, mas a sequência de tarefas salva com sucesso. A abertura desta sequência de tarefas novamente no editor também mostra um aviso inofensivo de que não podem ser encontrados objetos referenciados. <!-- sms427542 -->
- A imagem de arranque do passo de conteúdo do pacote de descarregamento não aparece na lista de referências da sequência de tarefas personalizadas. Também a ação **Distribute Content** não está disponível. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Alterar a instalação do cliente do Gestor de Configuração  
Como resultado do feedback de voz do utilizador, [silverlight já não está instalado nos clientes automaticamente.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Alterar para o painel de instrumentos do dispositivo Surface
O painel surface apresenta agora versões de firmware para dispositivos Surface em vez da versão do sistema operativo. Na consola, vá a**Dispositivos**de Superfície **de Monitorização** > . Pode ver os seguintes itens:
- Por cento das superfícies
- Por cento dos modelos Surface
- As cinco melhores versões de firmware
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Melhorias no painel de gestão de clientes do Office 365 
O painel de instrumentos de Gestão de Clientes do Office 365 apresenta agora uma lista de dispositivos relevantes quando são selecionadas secções de gráficos. Na consola, vá ao **Software Library** >**Overview** >Office**365 Client Management**. O painel de instrumentos é apresentado à direita. A seleção de critérios do gráfico mostra uma lista de dispositivos.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias na consola do Gestor de Configuração 
Fizemos as seguintes melhorias na consola Do Gestor de Configuração, que foram resultado do feedback de voz do utilizador.

- [A lista do dispositivo apresenta](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user)o utilizador principal : Listas de dispositivos em Ativos e Conformidade, Dispositivos, agora visualizar o utilizador principal por padrão. A última sessão registada no utilizador também pode ser adicionada como uma coluna opcional. <!-- 1357280 -->
- [Coleções renomeadas exibem as regras de adesão à coleção existentes](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Se uma coleção for membro de outra coleção e for renomeada, o novo nome é atualizado de acordo com as regras de adesão.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Fizemos as seguintes melhorias na implementação do sistema operativo, algumas das quais foram o resultado do feedback de voz do utilizador.
- [Visualizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a)de registo predefinido na imagem do arranque : No Windows PE, ao lançar cmtrace.exe, já não é solicitado a escolher se faz deste programa o visualizador predefinido para ficheiros de registo. <!-- SMS 500897 -->
- Descarregue passo de conteúdo de pacote: Pode agora adicionar imagens de arranque a este passo de sequência de tarefas.


## <a name="windows-10-feedback-hub-app-integration"></a>Integração de aplicações do Windows 10 Feedback Hub

Adoramos tanto feedback que estamos agora a permitir feedback através da [aplicação Feedback Hub](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporada no Windows 10. Quando **adicionar um novo feedback,** certifique-se de selecionar a categoria **de Gestão empresarial** e, em seguida, escolher entre uma das seguintes subcategorias:
- Cliente do Configuration Manager
- Consola do Configuration Manager
- Implantação do Sistema de Configuração OS
- Servidor de gestor de configuração

Continue a utilizar a nossa página de [voz do utilizador](https://configurationmanager.uservoice.com/) para votar em novas ideias de funcionalidade no Gestor de Configuração.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
