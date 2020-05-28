---
title: Nova versão 1702
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1702 do Gestor de Configuração.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eacf64245f4cfc779dc92be73e8d7e387b34f909
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427930"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>O que&#39;novo na versão 1702 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1702 para o ramo atual do Gestor de Configuração está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1602, 1606 ou 1610. Também está disponível como uma versão de base que pode utilizar na instalação de uma nova implementação.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de base do 'Gestor de Configuração'.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Instalação de atualizações nos sites](../../servers/manage/updates.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1702 do Gestor de Configuração.  

## <a name="deprecated-features-and-operating-systems"></a>Funcionalidades e sistemas operativos degradados
Saiba mais sobre as alterações de suporte antes de serem implementadas em [itens removidos e depreciados](deprecated/removed-and-deprecated.md).

A versão 1702 deixa cair o suporte para os seguintes produtos:
- **SQL Server 2008 R2,** para servidores de base de dados do site. A depreciação do apoio foi [anunciada pela primeira vez](deprecated/removed-and-deprecated-server.md#sql-server) em 10 de julho de 2015. Esta versão do SQL Server permanece suportada quando utiliza uma versão Do Gestor de Configuração antes da versão 1702.
- **Windows Server 2008 R2,** para servidores do sistema de site e a maioria das funções do sistema do site. A depreciação do apoio foi [anunciada pela primeira vez](deprecated/removed-and-deprecated-server.md#server-os) em 10 de julho de 2015. Esta versão do Windows continua a ser suportada quando utiliza uma versão 'Gestor de Configuração' antes da versão 1702.  
- **Windows Server 2008**, para servidores do sistema de site e a maioria das funções do sistema do site. A depreciação do apoio foi [anunciada pela primeira vez](deprecated/removed-and-deprecated-server.md#server-os) em 10 de julho de 2015.
- **Windows XP Incorporado,** como um sistema operativo cliente. A depreciação foi [anunciada pela primeira vez](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) em 10 de julho de 2015. Esta versão do Windows continua a ser suportada quando utiliza uma versão 'Gestor de Configuração' antes da versão 1702.




## <a name="site-infrastructure"></a>Infraestrutura do local

### <a name="improvements-for-in-console-search"></a>Melhorias para pesquisa na consola
Seguem-se melhorias na utilização da pesquisa na consola 'Gestor de Configuração':
- **Caminho do objeto:**  
  Muitos objetos suportam agora uma coluna chamada **Caminho do Objeto.**  Quando pesquisar e incluir esta coluna nos resultados do seu visor, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa de apps no nó de Aplicações e também estiver procurando sub-nós, a coluna *Object Path* no painel de resultados mostrar-lhe-á o caminho para cada objeto que é devolvido.   

- **Preservação do texto de pesquisa:**  
  Quando introduzir texto na caixa de texto de pesquisa e, em seguida, alternar entre procurar um sub-nó e o nó atual, o texto que digitou irá agora persistir e permanecer disponível para uma nova pesquisa sem ter que reentrar nela.

- **Preservação da sua decisão de pesquisar sub-nódosos:**  
  A opção que escolhe para pesquisar o *nó atual* ou todos *os sub-nós* agora persiste quando muda o nó em que está a trabalhar. Este novo comportamento significa que não precisa de redefinir constantemente esta decisão à medida que se desloca em torno da consola. Por predefinição, quando abre a consola, a opção é pesquisar apenas o nó atual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar feedback da consola 'Gestor de Configuração'

Pode utilizar as opções de feedback na consola para enviar feedback diretamente para a equipa de desenvolvimento.

Pode encontrar a opção **Feedback:**
- Na fita, na esquerda do separador Home de cada nó.  
  ![Fita](./media/feedback-home.png)

- Quando clicar em qualquer objeto na consola.   
   ![Opção righ-click](./media/feedback-option.png)   

  Escolher **o Feedback** abre o seu navegador para o site de feedback do UserVoice do Gestor de [Configuração.](https://configurationmanager.uservoice.com/forums/300492-ideas)


###  <a name="changes-for-updates-and-servicing"></a>Alterações para Atualizações e Manutenção
Seguem-se as alterações para Atualizações e Assistência:

- **Localização do nó**   
  Depois de instalar a versão 1702, o nó **de Atualizações e Manutenção** aparece como um nó de alto nível sob **administração**. Já não é um nó infantil abaixo **dos Serviços cloud.**

- **Novos estados de atualização**  
  Quando vê as atualizações disponíveis na consola, existem dois novos estados:  
  - **Disponível para instalação** - Esta é uma atualização que foi descarregada e pronta a instalar.
  - **Pronto para download** - Esta atualização está disponível, mas não foi descarregada. Pode optar por descarregar esta atualização, mas foi substituído por uma atualização mais recente.


- **Escolhas de atualização mais simples**  
  Da próxima vez que a sua infraestrutura se qualificar para duas ou mais atualizações, apenas a última atualização é descarregada. Por exemplo, se a versão atual do site for duas ou mais mais antiga do que a versão mais recente que está disponível, apenas que a versão de atualização mais recente é descarregada automaticamente.  

  Pode optar por descarregar e instalar as outras atualizações disponíveis, mesmo quando não são a versão mais atual. Se descarregar uma atualização mais antiga, receberá um aviso de que a atualização foi substituída por uma mais recente. Para descarregar uma atualização *disponível para descarregar,* selecione a atualização na consola e clique em **Baixar**.

- **Melhor limpeza de atualizações mais antigas**   
  Adicionámos uma função de limpeza automática que elimina os downloads desnecessários da pasta 'EasySetupPayload' no servidor do seu site. Uma vez que isto é introduzido com a versão 1702, a limpeza começa a funcionar depois de instalar uma atualização subsequente como uma versão de rollup de atualização ou futura atualização.  


### <a name="data-warehouse-service-point"></a>Ponto de serviço data Warehouse
Utilize o ponto de serviço data Warehouse para armazenar e reportar sobre dados históricos a longo prazo para a sua implementação do Gestor de Configuração.

O armazém de dados suporta até 2 TB de dados, com carimbos temporais para rastreio de alterações. O armazenamento de dados é realizado por sincronizações automatizadas desde a base de dados do Site Do Gestor de Configuração até à base de dados do armazém de dados. Esta informação é então acessível a partir do ponto de Serviços de Informação.

Para mais informações, consulte o ponto de [serviço do Data Warehouse](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Melhorias do Peer Cache
A partir da versão 1702, um computador de origem de cache peer rejeitará um pedido de conteúdo quando o computador de origem de cache peer satisfaz qualquer uma das seguintes condições:  
-  Está em modo de bateria baixa.
-  A carga de CPU ultrapassa os 80% no momento em que o conteúdo é solicitado.
-  O disco I/O tem um *AvgDiskQueueLength* que ultrapassa 10.
-  Não há mais ligações disponíveis ao computador.   
Para mais informações, consulte **acesso limitado a uma fonte** de cache de pares em Peer Cache para clientes de Gestor de [Configuração](../hierarchy/client-peer-cache.md).   

Além disso, são adicionados três novos relatórios ao seu ponto de reporte. Pode utilizar estes relatórios para compreender mais detalhes sobre pedidos de conteúdo rejeitados, incluindo qual o grupo de limites, computador e conteúdo envolvido. Consulte [a monitorização](../hierarchy/client-peer-cache.md#monitoring) no tópico de cache dos pares.

### <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
Utilize a ferramenta de limpeza da biblioteca de [conteúdos](../hierarchy/content-library-cleanup-tool.md) para remover o conteúdo dos pontos de distribuição quando esse conteúdo já não estiver associado a uma aplicação.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Utilize o conector OMS com a nuvem do Governo Azure
Pode utilizar o conector OMS para ligar ao OMS Log Analytics na nuvem do Governo microsoft Azure. Isto requer que modifique um ficheiro de configuração antes de instalar o conector OMS para que o conector possa funcionar com a nuvem do Governo. Para mais informações, consulte [Utilize o conector OMS com a nuvem do Governo Azure](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Os pontos de atualização de software são adicionados aos grupos de fronteira
Começando com a versão 1702, os clientes usam grupos de limites para encontrar um novo ponto de atualização de software, e para recuar e encontrar um novo ponto de atualização de software se o seu atual já não estiver acessível. Pode adicionar pontos de atualização de software individuais a diferentes grupos de limites para controlar quais os servidores que um cliente pode encontrar. Para mais informações, consulte pontos de [atualização](../../servers/deploy/configure/boundary-groups.md#software-update-points) de software no tópico de grupos de [fronteira configurantes.](../../servers/deploy/configure/boundary-groups.md)


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-compliance-settings-for-ios"></a>Novas definições de conformidade para iOS

Adicionámos muitas novas definições para dispositivos iOS que correspondam às disponíveis com o Microsoft Intune.


## <a name="application-management"></a>Gestão de Aplicações

### <a name="improved-support-for-windows-store-for-business-apps"></a>Melhor suporte para windows store para aplicações empresariais

Pode agora implementar aplicações licenciadas online a partir da Windows Store for Business para PCs Windows 10 que gere utilizando o cliente do Gestor de Configuração.
Para mais informações, consulte [Gerir aplicações a partir da Windows Store para Negócios](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique se executa ficheiros executáveis antes de instalar uma aplicação

Na caixa de diálogo **Properties** de um tipo de implementação, no separador 'Comportamento de **Instalação',** pode agora especificar um dos ficheiros mais executáveis que, se estiver em execução, bloqueará a instalação do tipo de implementação. O utilizador deve fechar o ficheiro executável em execução (ou pode ser fechado automaticamente para implementações com o objetivo necessário) antes de o tipo de implementação poder ser instalado.

Se a aplicação foi implementada como **Disponível**, e um utilizador final tentar instalar uma aplicação, serão solicitados a encerrar quaisquer executíveis de execução especificados antes de poderem prosseguir com a instalação.

Se a aplicação foi implementada conforme **necessário,** e a opção **fechar automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa** de diálogo de propriedades de implementação é selecionada, eles verão uma caixa de diálogo que os informa que executáveis que especificou serão automaticamente fechados quando o prazo de instalação da aplicação for atingido.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Melhorias na gestão de aplicações para MDM híbrido

- [Implementar aplicações iOS compradas em volume para coleções de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Apoio ao Programa de Compra de Volume iOS para A Educação](#support-for-ios-volume-purchase-program-for-education)
- [Suporte para múltiplos tokens do programa de compra de volume](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="expire-stand-alone-media"></a>Expire meios autónomos
Quando cria meios de comunicação autónomos, existem novas opções para definir datas de início e expiração opcionais nos meios de comunicação. Estas definições são desativadas por defeito. As datas são comparadas com o tempo de sistema no computador antes que os meios de comunicação autónomos sejam executados. Quando o tempo de sistema é mais cedo do que o tempo de início ou mais tarde do que o tempo de validade, os meios de comunicação autónomos não são iniciados. Estas opções também estão disponíveis utilizando o cmdlet New-CMStandaloneMedia PowerShell. Para mais detalhes, consulte [Criar meios de comunicação autónomos.](../../../osd/deploy-use/create-stand-alone-media.md)

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID do pacote apresentado em passos de sequência de tarefas
Qualquer passo de sequência de tarefas que refira um pacote, pacote de controlador, imagem do sistema operativo, imagem de arranque ou pacote de atualização do sistema operativo irá agora apresentar o ID do pacote do objeto referenciado. Quando uma sequência de tarefas faz referência a uma aplicação, apresentará o ID do objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Suporte a conteúdos adicionais em meios autónomos
Conteúdos adicionais são agora suportados em meios autónomos. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações a serem encenadas nos meios de comunicação, juntamente com os outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas o conteúdo referenciado na sequência de tarefas era encenado em meios autónomos. Para mais detalhes, consulte [Criar meios de comunicação autónomos.](../../../osd/deploy-use/create-stand-alone-media.md)

### <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações da UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e propriedade **(UEFI**) estão disponíveis para ajudá-lo a determinar se um computador começa no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** está definida para **TRUE**. Isto é ativado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../../clients/manage/inventory/configure-hardware-inventory.md)de hardware .

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Melhorias nas mensagens de aviso do Software Center para sequências de tarefas de alto impacto
Esta versão inclui as seguintes melhorias para mensagens de aviso do Software Center para sequências de tarefas de implementação de alto impacto:

- Nas propriedades da sequência de tarefas, pode agora configurar qualquer sequência de tarefas, incluindo sequências de tarefas do sistema não operacional, como uma implementação de alto risco. Qualquer sequência de tarefa que satisfaça determinadas condições é automaticamente definida como de alto impacto. Para mais detalhes, consulte [Gerir implementações de alto risco](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- Nas propriedades da sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinida ou criar a sua própria mensagem de notificação personalizada para implementações de alto impacto.
- Nas propriedades da sequência de tarefas, pode configurar as propriedades do Software Center, que incluem fazer um reinício necessário, o tamanho de descarregamento da sequência de tarefas e o tempo estimado de execução.
- A mensagem de implementação padrão de alto impacto para atualizações no local indica agora que as suas aplicações, dados e configurações são automaticamente migradas. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicava que todas as aplicações, dados e configurações seriam perdidos, o que não era verdade para uma atualização no local.

Para mais detalhes, consulte [configurar definições de sequência de tarefas de alto impacto](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volte à página anterior quando uma sequência de tarefas falhar
Agora pode voltar a uma página anterior quando executar uma sequência de tarefas e houver uma falha. Antes desta libertação, teve de reiniciar a sequência de tarefas quando houve uma falha. Por exemplo, pode utilizar o botão **Anterior** nos seguintes cenários:

- Quando um computador começa no Windows PE, o diálogo de armadilha de sequência de tarefas pode ser exibido antes da sequência de tarefas estar disponível. Quando clicar em Next neste cenário, a página final da sequência de tarefas mostra com uma mensagem que não existem sequências de tarefas disponíveis. Agora, pode clicar em **Anteriorpara** procurar novamente as sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdo dependente ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falha. Agora pode distribuir o conteúdo em falta (se ainda não foi distribuído) ou esperar que o conteúdo esteja disponível nos pontos de distribuição e, em seguida, clique **em Anterior** para ter a sequência de tarefas novamente pesquisado para o conteúdo.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo pré-cache para implementações disponíveis e sequências de tarefas
A partir da versão 1702, para implementações disponíveis de sequências de tarefas, pode optar por utilizar conteúdo pré-cache. O conteúdo pré-cache dá-lhe a opção de permitir que o cliente descarregue apenas o conteúdo aplicável assim que receber a implementação. Portanto, quando o utilizador clica **em Instalar** no Centro de Software, o conteúdo está pronto e a instalação começa rapidamente porque o conteúdo está no disco rígido local. Para mais detalhes, consulte o [conteúdo pré-cache da Configuração](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
A Atualização de Criadores do Windows 10 introduz uma ferramenta de conversão simples que automatiza o processo de repartição do disco rígido para hardware ativado pela UEFI e integra a ferramenta de conversão no processo de atualização do Windows 7 para o Windows 10. Quando combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para a Atualização de Criadores do Windows 10. Para mais detalhes, consulte os passos da [sequência de tarefas para gerir o BIOS até à conversão UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Melhorias na etapa de sequência de tarefas de instalação de aplicações
Esta versão introduziu as seguintes melhorias:
- Aumentou o número máximo de aplicações que pode instalar para 99 na etapa de sequência de **tarefas de Instalação de Aplicações.** O número máximo anterior era de 9 candidaturas.
- Quando adicionar aplicações ao passo de sequência de **tarefas de Instalação** de Aplicações no editor da sequência de tarefas, pode agora selecionar várias aplicações da **aplicação Select the application para instalar** o painel.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Melhorias na sequência de tarefas do condutor de aplicação automática
Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor limite na fase de sequência de tarefas do Condutor de Aplicação Automática ao fazer pedidos de catálogo HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
- SMSTSDriverRequestResolveTimeout  
  Padrão: 60
- SMSTSDriverRequestConnectTimeout  
  Padrão: 60
- SMSTSDriverRequestSendTimeout  
  Padrão: 60
- SMSTSDriverRequestReceberTimeout  
  Padrão: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK rastreado por versão build
O Windows 10 ADK é agora rastreado por versão build para garantir uma experiência mais suportada ao personalizar as imagens de boot do Windows 10. Por exemplo, se o site utilizar o Windows ADK para o Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola. Para mais detalhes sobre personalizar as versões WinPE, consulte [Personalizar imagens de boot](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>O caminho de origem de imagem de arranque padrão já não pode ser alterado
As imagens de boot padrão são geridas pelo Gestor de Configuração e o caminho de origem de imagem de arranque padrão já não pode ser alterado na consola do Gestor de Configuração ou utilizando o SDK do Gestor de Configuração. Pode continuar a configurar um caminho de origem personalizado para imagens de boot personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>As imagens de boot padrão são regeneradas após atualizar o Gestor de Configuração para uma nova versão
A partir desta versão, quando atualiza a versão ADK do Windows e depois utiliza atualizações e manutenção para instalar a versão mais recente do 'Gestor de Configuração', o Gestor de Configuração regenera as imagens de boot predefinidas. Isto inclui a nova versão Window PE do Windows ADK atualizado, a nova versão do cliente do Gestor de Configuração, controladores, personalizações, etc. As imagens de arranque personalizadas não são modificadas. Para mais detalhes, consulte [Gerir imagens de arranque](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Atualizações de software

### <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 para clientes
A partir da versão 1702, a partir do painel de gestão de clientes do Office 365, pode iniciar o Instalador office 365 que lhe permite configurar as definições de instalação do Office 365, transferir ficheiros das Redes de Entrega de Conteúdos do Office (CDNs) e implementar os ficheiros como aplicação no Gestor de Configuração. Para mais detalhes, consulte as atualizações do [Manage Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).

> [!IMPORTANT]
> A aplicação Office 365 que cria e implementa utilizando o Assistente de Aplicação do Office 365 no Gestor de Configuração não é gerida automaticamente pelo Gestor de Configuração até ativar a **gestão ativa do software Do Office 365 Client Again** atualiza a definição de agente cliente. Para mais detalhes, consulte [as definições do cliente](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir Ficheiros de instalação rápida para as atualizações do Windows 10
A partir da versão 1702, o Gestor de Configuração suporta ficheiros de instalação expresso para atualizações do Windows 10. Quando utilizar uma versão suportada do Windows 10, pode utilizar as definições do 'Gestor de Configuração' para descarregar apenas as alterações entre a Atualização Cumulativa do Windows 10 do mês em curso e a atualização do mês anterior. Sem ficheiros de instalação expresso, o Gestor de Configuração descarrega a atualização cumulativa completa do Windows 10 (incluindo todas as atualizações dos meses anteriores) todos os meses. A utilização de ficheiros de instalação expresso fornece transferências menores e tempos de instalação mais rápidos nos clientes. Para mais detalhes, consulte ['Gerir ficheiros de instalação expresso' para atualizações do Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>As versões Android e iOS já não são direcionadas para os assistentes de criação de MDM híbrido

A partir da versão 1702 para a gestão de dispositivos móveis híbridos (MDM), já não é necessário direcionar versões específicas do Android e iOS na criação de novas políticas e perfis para dispositivos geridos pela Intune. Em vez disso, escolhe um dos seguintes tipos de dispositivos:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Esta alteração afeta os assistentes para a criação dos seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificado
- Perfis de e-mail
- Perfis VPN
- Perfis Wi-Fi

Com esta mudança, as implementações híbridas podem fornecer suporte mais rapidamente para novas versões Android e iOS sem precisar de um novo lançamento ou extensão do Gestor de Configuração. Uma vez que uma nova versão é suportada em Intune autónoma, os utilizadores poderão atualizar os seus dispositivos móveis para essa versão.

Para evitar problemas ao atualizar a partir de versões anteriores do 'Gestor de Configuração', as versões do sistema operativo móvel ainda estão disponíveis nas páginas de propriedades para estes itens. Se ainda precisar de direcionar uma versão específica, pode criar o novo item e, em seguida, especificar a versão direcionada na página de propriedades do item recém-criado. 

> [!NOTE]
> A última versão do sistema operativo móvel disponível nas páginas de propriedades aplica-se a essa versão e a todas as versões subsequentes. As páginas de propriedades fornecem as seguintes opções para direcionar os sistemas operativos mais tarde do que o Android 7 e o iOS 10: 
> - **Android 7 e superior**
> - **Todos os iOS 10 e dispositivos de toque de iPhone ou iPod mais altos**
> - **Todos os dispositivos iOS 10 e iPad mais altos**

### <a name="android-for-work-support"></a>Suporte do Android for Work
A partir de 1702, a gestão de dispositivos móveis Híbridos com a Microsoft Intune suporta agora a inscrição e gestão de dispositivos Android for Work.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

Agora pode implementar aplicações licenciadas para dispositivos e utilizadores. Dependendo da capacidade de aplicação para suportar o licenciamento do dispositivo, uma licença apropriada será reclamada quando a implementar, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Gestor de Configuração|App suporta licenciamento de dispositivos?|Tipo de recolha de implantação|Licença reclamada|
|Mais cedo que 1702|Sim|Utilizador|Licença de utilizador|
|Mais cedo que 1702|Não|Utilizador|Licença de utilizador|
|Mais cedo que 1702|Sim|Dispositivo|Licença de utilizador|
|Mais cedo que 1702|Não|Dispositivo|Licença de utilizador|
|1702 e mais tarde|Sim|Utilizador|Licença de utilizador|
|1702 e mais tarde|Não|Utilizador|Licença de utilizador|
|1702 e mais tarde|Sim|Dispositivo|Licença de dispositivo|
|1702 e mais tarde|Não|Dispositivo|Licença de utilizador|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Apoio ao Programa de Compra de Volume iOS para A Educação

Agora também pode implementar e rastrear aplicações que adquiriu no programa de compra de volume do iOS para educação.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Suporte para múltiplos tokens do programa de compra de volume

Agora pode associar várias fichas do programa de compra de volume da Apple ao Gestor de Configuração.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Suporte para apps de linha de negócios na Windows Store para Negócios

Agora já pode sincronizar aplicações de negócios personalizadas a partir da Windows Store for Business.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Melhorias da política de conformidade do dispositivo de acesso condicional

Uma nova regra de política de conformidade de dispositivos está disponível para ajudá-lo a bloquear o acesso a recursos corporativos que suportam o acesso condicional, quando os utilizadores estão a usar apps que fazem parte de uma lista não conforme de aplicações. A lista não conforme de aplicações pode ser definida pelo administrador ao adicionar a nova regra de conformidade **Apps que não podem ser instaladas**. Esta regra requer que o administrador introduza o Nome da **Aplicação,** o ID da **Aplicação**e o Editor de **Aplicações** (opcional) ao adicionar uma aplicação à lista não conforme. Esta definição aplica-se apenas aos dispositivos iOS e Android.

Além disso, isto ajuda as organizações a mitigar a fuga de dados através de aplicações não seguras e a prevenir o consumo excessivo de dados através de certas apps.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Novas ferramentas de monitorização da Defesa de Ameaças Móveis

A partir da versão 1702, tem novas formas de monitorizar o estado de conformidade com o seu fornecedor de serviços de Defesa de Ameaças Móveis.


## <a name="protect-devices"></a>Proteger dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detetar versões de clientes antimalware desatualizadas
A partir da versão 1702, pode configurar um alerta para garantir que os clientes endpoint Protection não estão desatualizados. Para mais informações, consulte [Alerta para cliente de malware desatualizado](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Atualizações de atesta de saúde do dispositivo
O serviço de atestação de saúde do dispositivo para clientes no local pode agora ser configurado e gerido a partir do ponto de gestão. Para mais informações, consulte [A Estação de Saúde.](../../servers/manage/health-attestation.md)

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfis de certificado saléris para Windows Hello for Business

Se pretender armazenar perfis de certificado no porta-chaves do Windows Hello for Business e o perfil do certificado utilizar o Smart Card Logon EKU, tem de configurar permissões para o registo da chave para garantir que o certificado é validado corretamente.
Para mais informações, consulte [as definições do Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nova notificação do Windows Hello para negócios para utilizadores finais
Uma nova notificação do Windows 10 informa os utilizadores finais de que devem tomar medidas adicionais para completar a configuração do Windows Hello for Business (por exemplo, configurar um PIN).
