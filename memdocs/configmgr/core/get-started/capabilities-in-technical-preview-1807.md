---
title: Pré-visualização técnica 1807
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de pré-visualização técnica do Gestor de Configuração 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 398f16b8f75d894030d76406807f74bdaa4be9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714788"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Capacidades na versão técnica de pré-visualização do Gestor de Configuração 1807 

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na pré-visualização técnica para O Gestor de Configuração, versão 1807. Instale esta versão para atualizar e adicione novas funcionalidades ao seu site de pré-visualização técnica. 

Reveja o artigo de [pré-visualização técnica](technical-preview.md) antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problemas conhecidos 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a>Problemas com atualizações de software do Office 365
<!--521365-->
Se gerir as atualizações do Office 365 utilizando as versões técnicas do ramo de pré-visualização 1806 e 1806.2, podem não conseguir instalar nos clientes. 

#### <a name="workaround"></a>Solução
- Elimine os pacotes de implementação existentes e os grupos de atualização de software para o Office 365.  

- A partir de 31 de julho de 2018, sincronize as atualizações de software do Office 365 e implemente apenas as últimas atualizações.  



</br>

**As seguintes secções descrevem as novas funcionalidades para experimentar nesta versão:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a>Centro Comunitário
<!--1357766-->

O Centro Comunitário é um local centralizado para a partilha de objetos úteis do Gestor de Configuração com outros. Consulte o novo espaço de trabalho **comunitário** na consola Do Gestor de Configuração e selecione o nó **Hub.** Utilize o Centro Comunitário para descarregar os seguintes tipos de objetos do Gestor de Configuração: 
- Scripts
- Itens de configuração

![Consola de Gestor de Configuração, espaço de trabalho comunitário, nó hub](media/1357766-hub.png)

Para ver mais detalhes sobre um item disponível, clique no centro. Na página de detalhes, clique em **Baixar** para adquirir o item. Quando descarrega um item do centro, é adicionado automaticamente ao seu site. 

![Consola de Gestor de Configuração, espaço de trabalho comunitário, nó hub, página de detalhes](media/1357766-hub-details.png)

O espaço de trabalho **comunitário** inclui também os seguintes nódosos:

- **Documentação**: Exibe a biblioteca de [documentação](https://docs.microsoft.com/sccm/) do Gestor de Configuração  

- **Feedback**: Exibe o [site uservoice](https://configurationmanager.uservoice.com/) do Gestor de Configuração  


### <a name="prerequisites"></a>Pré-requisitos

- Utilize a consola 'Gestor de Configuração' num OS do cliente.  

    - Alternativamente, mas não recomendado: num sistema operativo OS, desative o [Internet Explorer: Configuração de segurança melhorada](https://go.microsoft.com/fwlink/?LinkId=253461).  

- O computador com a consola requer acesso à Internet e conectividade aos seguintes sites:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problema conhecido

Os itens que contribuem para o hub não estão atualmente disponíveis nesta versão. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a>Especifique a unidade para manutenção de imagem offline do OS  
<!--1358924-->

Com base no feedback do [UserVoice,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)especifique agora a unidade que o Gestor de Configuração utiliza durante a manutenção offline das imagens OS. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários, pelo que esta opção lhe dá flexibilidade para selecionar a unidade a utilizar. 


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Em seguida, envie [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) com os seus pensamentos sobre a funcionalidade.

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Na fita, clique em **Configurar componentes** do site e selecione **Software Update Point**.  

2. Mude para o separador de **assistência offline** e especifique a opção para uma unidade local a utilizar através da manutenção offline **de imagens**.  

Por predefinição, esta definição é **Automática**. Com este valor, o Gestor de Configuração seleciona a unidade em que está instalada. 

Durante a manutenção offline, o Gestor de `<drive>:\ConfigMgr_OfflineImageServicing`Configuração armazena ficheiros temporários na pasta, . Também monta as imagens de S nesta pasta. 

Reveja o ficheiro de registo **OfflineServicingMgr.log.** 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a>Atividade sincronizada de dispositivos cogerido sintetizada a partir de Intune
<!--1358565-->

Mostrar na consola do Gestor de Configuração se um dispositivo cogerido está ativo com o Microsoft Intune. Este estado baseia-se em dados do [Intune Data Warehouse](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). O dashboard status do **cliente** na consola do Gestor de Configuração mostra **clientes inativos usando Intune**. Esta nova categoria destina-se a dispositivos cogeridos que estão inativos com o Gestor de Configuração, mas que se sincronizaram com o serviço Intune na última semana.


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Em seguida, envie [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) com os seus pensamentos sobre a funcionalidade.

Se já criou o seu site para cogestão: 

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.** Clique em **Propriedades** na fita.  

2. Mude para o separador **Reportar.** Clique **em Iniciar sessão** e autenticar. Em seguida, clique em **Atualizar** para ativar as permissões de leitura para o Armazém de Dados Intune.  

3. Depois de o site sincronizar com intune, vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Estado do Cliente.** Na secção Geral de **Estatuto do Cliente,** consulte a linha para **clientes Inativos que utilizem o Intune**.  

Para obter mais informações sobre a capacidade de cogestão, consulte [a Co-management para dispositivos Windows 10](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a>Aplicações de reparação
<!--1357866-->

Com base no feedback do [UserVoice,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)especifique agora uma linha de comando de reparação para os tipos de instalação do Instalador do Windows e do Instalador de Scripts. 


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Em seguida, envie [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) com os seus pensamentos sobre a funcionalidade.

1. Na consola 'Gestor de Configuração', abra as propriedades de um instalador do Windows ou do tipo de implementação do instalador de scripts.  

2. Mude para o separador **Programas.** Especifique o comando do **programa de reparação.**  

3. Implementar a aplicação. No separador **Definições** de Implementação da implementação, ative a opção de permitir que **os utilizadores finais tentem reparar esta aplicação**.  


### <a name="known-issue"></a>Problema conhecido

O novo botão no Software Center para os utilizadores **repararem** a aplicação não é visível nesta versão.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a>Aprovar pedidos de pedido por e-mail
<!--1321550-->

Configure notificações de e-mail para pedidos de aprovação de pedidos de aplicação. Quando um utilizador solicita uma aplicação, recebe um e-mail. Clique em links no e-mail para aprovar ou negar o pedido, sem necessitar da consola 'Gestor de Configuração'.


### <a name="prerequisites"></a>Pré-requisitos

#### <a name="to-send-email-notifications"></a>Para enviar notificações por e-mail
- Ativar a [funcionalidade opcional](../servers/manage/install-in-console-updates.md#bkmk_options) Aprove os pedidos de **aplicação para utilizadores por dispositivo**.  

- Configure a notificação de [e-mail para alertas](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Para aprovar ou negar pedidos de e-mail
Caso não configure estes pré-requisitos, o site envia notificação por e-mail para pedidos de pedido sem links para aprovar ou negar o pedido.  

- Nas propriedades do site, **enable REST endpoint para todos os fornecedores funções neste site e permitir**o tráfego de gateway de gestão de nuvem do Gestor de Configuração . Para mais informações, consulte o acesso de dados do Ponto final do [OData](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Reinicie o serviço SMS_EXEC depois de permitir o ponto final do REST

- [Gateway de gestão da cloud](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- A bordo do site para [serviços Azure](../servers/deploy/configure/azure-services-wizard.md) para **Gestão de Nuvem**  

    - Ativar a descoberta do [utilizador da AD Azure](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

    - Configure manualmente as seguintes definições para esta aplicação nativa em Azure AD:  

        - **Redirecione o URI:** `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Utilize o nome de domínio totalmente qualificado (FQDN) do serviço de gateway de gestão de nuvem (CMG), por exemplo, GraniteFalls.Contoso.com.   

        - **Manifesto**: definir **oauth2AllowImplicitImplicitFlow** para verdadeiro:`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Em seguida, envie [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) com os seus pensamentos sobre a funcionalidade.

1. Na consola 'Gestor de Configuração', implemente uma aplicação disponível para uma recolha de utilizadores. Na página Definições de **Implementação,** ative-a para aprovação. Em seguida, insira um *único* endereço de e-mail para receber a notificação.  

     > [!Note]  
     > Qualquer pessoa na sua organização Azure AD que receba o e-mail pode aprovar o pedido. Não envie o e-mail para os outros a menos que queira que tomem medidas.  

2. Como utilizador, solicite a aplicação no Centro de Software.  

3. Recebe uma notificação de e-mail semelhante ao seguinte exemplo:  

![Notificação por e-mail de exemplo para aprovação de pedido](media/1321550-email.png)

> [!Note]  
> O link para aprovar ou negar é para uma utilização única. Por exemplo, configura um pseudónimo de grupo para receber notificações. Meg aprova o pedido. Agora bruce não pode negar o pedido.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a>Melhoria da saída do script
<!--1236459-->

Agora pode ver a saída detalhada do script em formato JSON cru ou estruturado. Esta formatação facilita a leitura e análise da saída. Se o script devolver texto formado por JSON válido, então veja a saída detalhada como **Saída JSON** ou **Saída Bruta**. Caso contrário, a única opção é a **Saída do Script.** 

#### <a name="example-script-output-is-valid-json"></a>Exemplo: A saída do script é válida JSON
Comando:`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Exemplo: A saída de script não é válida JSON
Comando:`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Experimente!

Tente completar as tarefas. Em seguida, envie [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) com os seus pensamentos sobre a funcionalidade.

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de Recolhas de **Dispositivos.** Clique na direita numa coleção e selecione **Executar Script**. Para obter mais informações sobre a criação e execução de scripts, consulte [Criar e executar scripts PowerShell a partir da consola Do Gestor de Configuração](../../apps/deploy-use/create-deploy-scripts.md).  

2. Executa um guião na coleção do alvo.  

3. Na página de **Monitorização** do Estado do Script do assistente do Script executar, selecione o separador **Resumo** na parte inferior. Altere as duas listas de drop-down na parte superior para **A Saída** do Script e tabela de **dados**. Em seguida, clique duas vezes na linha de resultados para abrir a caixa de diálogo de **saída detalhada.**  

4. Na página de **Monitorização** do Estado do Script do assistente do Script executar, selecione o separador **'Dados** de execução' na parte inferior. Clique duas vezes numa linha de resultados para abrir a caixa de diálogo de saída detalhada para esse dispositivo.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a>Melhoria das atualizações de software de terceiros
<!--1358714-->

Agora pode modificar as propriedades dos catálogos personalizados.

Para mais informações, consulte o suporte de [atualizações de software de terceiros para catálogos personalizados](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Passos seguintes

Para mais informações sobre a instalação ou atualização do ramo técnico de pré-visualização, consulte [a pré-visualização técnica](technical-preview.md).    

Para obter mais informações sobre os diferentes ramos do Gestor de Configuração, consulte qual o [ramo do Gestor de Configuração que devo utilizar?](../understand/which-branch-should-i-use.md)
