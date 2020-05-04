---
title: Gerir clientes
titleSuffix: Configuration Manager
description: Saiba como gerir os clientes no Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d7697f8b5a2017aa732c52512bf31598c070fbc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714879"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Como gerir clientes em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando o cliente do Gestor de Configuração instala num dispositivo e atribui com sucesso a um site, vê-se o dispositivo no espaço de trabalho **De Ativos e Compliance** no nó dos **Dispositivos** e numa ou mais coleções no nó de Recolhas de **Dispositivos.** Selecione o dispositivo ou uma coleção e, em seguida, executar operações de gestão. No entanto, existem outras formas de gerir o cliente, que podem envolver outros espaços de trabalho na consola, ou tarefas fora da consola.  

> [!NOTE]  
> Se instalar o cliente do Gestor de Configuração, mas ainda não foi designado com sucesso para um site, poderá não ser exibido na consola. Depois de o cliente atribuir a um site, atualizar a adesão à recolha e, em seguida, refrescar a vista da consola.  
>
> Um dispositivo também pode ser exibido na consola quando o cliente do Gestor de Configuração não estiver instalado. Este comportamento acontece se o site descobrir um dispositivo, mas o cliente não está instalado e atribuído.
>
> Os dispositivos móveis geridos com o [conector Exchange Server](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) ou [no local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) o MDM não instalam o cliente do Gestor de Configuração.  
>
> Para gerir um dispositivo a partir da consola, utilize a coluna **Cliente** no nó **de Dispositivos** para determinar se o cliente está instalado.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a>Gerir clientes a partir do nó de **Dispositivos**  

Dependendo do tipo de dispositivo, algumas destas opções poderão não estar disponíveis.  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Dispositivos.**  

2. Selecione um ou mais dispositivos e, em seguida, selecione uma destas tarefas de gestão do cliente a partir da fita. Também pode clicar no dispositivo.)  

### <a name="import-user-device-affinity"></a>Importe afinidade do dispositivo de utilizador

Configure as associações entre utilizadores e dispositivos, para que possa implementar software de forma eficiente para os utilizadores.  

Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

### <a name="import-computer-information"></a>Importar informações informáticas

Lance o Assistente de Informação de **Computador esbanjádo** para importar novas informações de computador na base de dados do Gestor de Configuração. Pode importar vários computadores usando um ficheiro ou especificar informações para um único computador.

### <a name="add-selected-items"></a>Adicionar itens selecionados

Fornece as seguintes opções:

- **Adicione itens selecionados à recolha de dispositivos existentes**: Abre a caixa de diálogo **Select Collection.** Selecione a coleção à qual pretende adicionar este dispositivo. O dispositivo está incluído nesta coleção utilizando uma regra de adesão **direta.**  

- **Adicione itens selecionados à nova recolha**de dispositivos : Abre o Assistente de Recolha de **Dispositivos Create** onde pode criar uma nova coleção. A coleção selecionada está incluída nesta coleção utilizando uma regra de adesão **direta.**  

Para mais informações, consulte [Como criar coleções.](collections/create-collections.md)

### <a name="install-client"></a>Instalar cliente

Abre o **Assistente de Cliente de Instalação.** Este assistente utiliza a instalação de pressão do cliente para instalar ou reinstalar o cliente Do Gestor de Configuração no dispositivo selecionado.

> [!TIP]  
> Existem muitas formas diferentes de instalar o cliente do Gestor de Configuração. Embora o cliente Push wizard ofereça um método de instalação de cliente conveniente a partir da consola, este método tem muitas dependências e não é adequado para todos os ambientes. Para obter mais informações sobre as dependências, consulte [os pré-requisitos para a implementação](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation)de clientes para computadores Windows . Para obter mais informações sobre os outros métodos de instalação do cliente, consulte os métodos de [instalação do Cliente.](../deploy/plan/client-installation-methods.md)

Para mais informações, consulte [como instalar clientes do Gestor de Configuração utilizando o impulso do cliente](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### <a name="run-script"></a>Executar o script

Abre o assistente **do Script executar** para executar um script PowerShell no dispositivo selecionado.

Para mais informações, consulte [Criar e executar scripts PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Instalar aplicação

Instale uma aplicação num dispositivo em tempo real. Esta funcionalidade pode ajudar a reduzir a necessidade de coleções separadas para cada aplicação.

Para mais informações, consulte [Instalar aplicações para um dispositivo](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Site de reatribuição

Reatribui um ou mais clientes, incluindo dispositivos móveis geridos, a outro site primário da hierarquia. Pode reatribuir individualmente clientes ou selecionar mais de um para os reatribuir a granel.  

### <a name="client-settings---resultant-client-settings"></a>Definições do cliente - Definições de cliente resultantes

Quando implementa várias definições de cliente para o mesmo dispositivo, a priorização e combinação de configurações é complexa. Utilize esta opção para visualizar o conjunto resultante de definições de cliente implementadas neste dispositivo.

Para mais informações, consulte [Como configurar as definições do cliente](../deploy/configure-client-settings.md).

### <a name="start"></a>Iniciar

- Executar **o Explorer de Recursos** para ver as informações de inventário de hardware e software de um cliente windows. Para obter mais informações, veja os artigos seguintes:

  - [Como utilizar o Explorador de Recursos para ver o inventário de hardware](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Como utilizar o Explorador de Recursos para ver o inventário de software](inventory/use-resource-explorer-to-view-software-inventory.md)

- Administrar remotamente o dispositivo utilizando **controlo remoto,** **assistência remota**ou cliente de ambiente de **trabalho remoto.** Para mais informações, consulte [Como administrar remotamente um computador cliente do Windows](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Aprovar

Quando o cliente comunica com os sistemas do site utilizando http e um certificado auto-assinado, deve aprovar estes clientes para identificá-los como computadores fidedignos. Por padrão, a configuração do site aprova automaticamente clientes da mesma floresta de Diretório Ativo e florestas fidedignas. Este comportamento padrão significa que não tem de aprovar manualmente cada cliente. Aprove manualmente computadores de grupo de trabalho em que confie, e quaisquer outros computadores não aprovados em que confie.

> [!IMPORTANT]  
> Embora algumas funções de gestão possam funcionar para clientes não aprovados, este é um cenário não suportado para O Gestor de Configuração.  

Não é preciso aprovar clientes que comuniquem sempre aos sistemas do site utilizando HTTPS, ou clientes que utilizem um certificado PKI quando comunicam aos sistemas do site utilizando http. Estes clientes estabelecem confiança utilizando os certificados PKI.

### <a name="block-or-unblock"></a>Bloquear ou desbloquear

Bloqueie um cliente em quem já não confia. O bloqueio impede o cliente de receber a política e impede que os sistemas do site se comuniquem com o cliente.  

> [!IMPORTANT]  
> Bloquear um cliente apenas impede a comunicação do cliente para os sistemas de site do Gestor de Configuração. Não impede a comunicação com outros dispositivos. Quando o cliente comunica aos sistemas do site utilizando HTTP em vez de HTTPS, existem algumas limitações de segurança.  

Também pode desbloquear um cliente que está bloqueado.

Para mais informações, consulte [Determinar se bloqueia clientes](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Implementações PXE claras necessárias

Pode reimplantar uma implementação PXE necessária, limpando o estado da última implementação pXE atribuída a uma coleção de Gestor de Configuração ou a um computador. Esta ação repõe o estado dessa implementação e reinstala as mais recentes implementações necessárias.

Para mais informações, consulte [Use PXE para implementar o Windows sobre a rede](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### <a name="client-notification"></a>Notificação de cliente

Para mais informações, consulte [notificações do Cliente](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Endpoint Protection

Para mais informações, consulte [notificações do Cliente](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Editar utilizadores primários

Veja os utilizadores deste dispositivo nos últimos 90 dias ou especifique os principais utilizadores deste dispositivo.

Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

### <a name="wipe-a-mobile-device"></a>Eliminar os dados de um dispositivo móvel

É possível eliminar os dados de dispositivos móveis que suportem o comando de eliminação de dados. Esta ação remove permanentemente todos os dados do dispositivo móvel, incluindo configurações pessoais e dados pessoais. Normalmente, esta ação repõe as predefinições de fábrica do dispositivo móvel. Limpe um dispositivo móvel quando já não é de confiança. Por exemplo, se o dispositivo for perdido ou roubado.  

> [!TIP]  
> Verifique a documentação do fabricante para obter mais informações sobre como o dispositivo móvel processa um comando de limpeza remota.  

Muitas vezes há um atraso até que o dispositivo móvel receba o comando de limpeza:  

- Se o dispositivo móvel for matriculado pelo Gestor de Configuração, o cliente recebe o comando quando descarrega a sua política de cliente.

- Se o dispositivo móvel for gerido pelo conector Exchange Server, recebe o comando quando sincroniza com o Exchange.  

Para monitorizar quando o dispositivo recebe o comando de limpeza, utilize a coluna **Wipe Status.** Até que o dispositivo envie um reconhecimento de limpeza ao Diretor de Configuração, pode cancelar o comando de limpeza.  

### <a name="retire-a-mobile-device"></a>Extinguir um dispositivo móvel

A opção **Aposentadoria** é suportada apenas por dispositivos móveis matriculados no local do MDM.  

Para mais informações, consulte [Ajude a proteger os seus dados com limpeza remota, bloqueio remoto ou reset](../../../mdm/deploy-use/wipe-lock-reset-devices.md)da código de acesso .

### <a name="change-ownership"></a>Alterar a propriedade

Se um dispositivo não estiver unido ao domínio e não tiver o cliente do Gestor de Configuração instalado, utilize esta opção para alterar a propriedade para **Empresa** ou **Pessoal**.  

Pode utilizar este valor nos requisitos de aplicação para controlar as implementações e controlar a quantidade de inventário recolhido dos dispositivos dos utilizadores.  

Pode ser necessário adicionar a coluna **Dono** do Dispositivo à vista clicando na direção da coluna e escolhendo-a.

### <a name="delete"></a>Eliminar

> [!WARNING]  
> Não apague um cliente se pretender desinstalar o cliente do Gestor de Configuração ou removê-lo de uma coleção.  

A ação **Delete** remove manualmente o registo do cliente da base de dados do Gestor de Configuração. Use esta ação para resolver um problema. Se eliminar o objeto, mas o cliente ainda está instalado e a comunicar com o site, a Heartbeat Discovery recria o registo do cliente. Reaparece na consola Do Gestor de Configuração, embora o histórico do cliente e quaisquer associações anteriores estejam perdidas.  
> [!NOTE]  
> Ao eliminar um cliente de dispositivo móvel que foi inscrito pelo Gestor de Configuração, esta ação também revoga o certificado PKI emitido. Este certificado é então rejeitado pelo ponto de gestão, mesmo que o IIS não verifique a lista de revogação do certificado (CRL).
>
> Os certificados em clientes legados de dispositivos móveis não são revogados quando elimina esses clientes.

Para desinstalar o cliente, consulte [Desinstalar o cliente Do Gestor](#BKMK_UninstalClient)de Configuração .  

Para atribuir o cliente a um novo site primário, consulte [como atribuir clientes a um site](../deploy/assign-clients-to-a-site.md).

Para remover o cliente de uma coleção, reconfigure as propriedades da coleção. Para mais informações, consulte [Como gerir as coleções.](collections/manage-collections.md)

### <a name="refresh"></a>Atualizar

Refresque a visão da consola com os dados mais recentes na base de dados. Por exemplo, se um dispositivo aparecer na lista a partir da descoberta, mas não aparecer como instalado. Depois de instalar o cliente e certificar-se de que está atribuído ao site, selecione **Refresh**.

### <a name="properties"></a>Propriedades

Veja os dados e implementações de descobertas direcionados para o cliente.

Também pode configurar variáveis que as sequências de tarefas usam para implantar um SISTEMA no dispositivo. Para mais informações, se Criar variáveis de sequência de [tarefas para dispositivos e coleções](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a>Gerir clientes a partir do nó **de Coleções** de Dispositivos

Muitas das tarefas disponíveis para dispositivos no nó de **Dispositivos** também estão disponíveis em coleções. A consola aplica automaticamente a operação a todos os dispositivos elegíveis da recolha. Esta ação em toda uma coleção gera pacotes de rede adicionais e aumenta o uso do CPU no servidor do site.  

Considere as seguintes perguntas antes de executar tarefas de nível de recolha. Uma vez iniciado, não se pode parar a tarefa da consola.

- Quantos dispositivos estão na coleção?
- Os dispositivos estão ligados por ligações de rede de baixa largura de banda?
- Quanto tempo esta tarefa precisa de ser completada para todos os dispositivos?

Para mais informações, consulte [Como gerir as coleções.](collections/manage-collections.md)


## <a name="restart-clients"></a>Reiniciar clientes

Utilize a consola 'Gestor de Configuração' para identificar clientes que necessitem de reiniciar. Em seguida, utilize uma ação de notificação do cliente para reiniciá-las.

> [!Tip]
> Ative a atualização automática do cliente para manter os seus clientes atualizados com menos esforço. Para mais informações, consulte sobre a [atualização automática do cliente](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Para identificar dispositivos que estejam pendentes de um reinício, vá ao espaço de trabalho **De Ativos e Compliance** na consola Do Gestor de Configuração e selecione o nó de **Dispositivos.** Em seguida, veja o estado de cada dispositivo no painel de detalhes numa nova coluna chamada **Pendente de Reinício**. Cada dispositivo tem um ou mais dos seguintes valores:

- **Não:** não há reinício pendente
- **Gestor de Configuração**: este valor provém do componente coordenador de reinicialização do cliente (RebootCoordinator.log)
- **Nome de ficheiro**: este valor vem do Windows reportando uma operação pendente de renome de ficheiro (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendenteFileRenameOperations)
- **Atualização do Windows**: este valor vem do Agente de Atualização do Windows a informar que é necessário um reinício pendente para uma ou mais atualizações (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Adicionar ou remover funcionalidade**: este valor vem da manutenção baseada em componentes do Windows, reportando a adição ou remoção de uma funcionalidade do Windows, que requer um reinício (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pendente)

### <a name="create-the-client-notification-to-restart-a-device"></a>Criar a notificação do cliente para reiniciar um dispositivo

1. Selecione o dispositivo que pretende reiniciar dentro de uma coleção no nó de Recolha de **Dispositivos** da consola.
2. Na fita, selecione **Notificação**do Cliente , e, em seguida, selecione **Reiniciar**. Abre-se uma janela de informação sobre o recomeço. Selecione **OK** para confirmar o pedido de reinício.

Quando a notificação é recebida por um cliente, abre-se uma janela de notificação do **Software Center** para informar o utilizador sobre o reinício. Por defeito, o reinício ocorre após 90 minutos. Pode modificar o tempo de reinício configurando [as definições do cliente](../deploy/configure-client-settings.md). As definições para o comportamento de reinício são encontradas no separador de [reinício](../deploy/about-client-settings.md#computer-restart) do Computador das definições predefinidas.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a>Configure a cache do cliente

O cache do cliente armazena ficheiros temporários para quando os clientes instalam aplicações e programas. As atualizações de software também usam a cache do cliente, mas tentam sempre descarregar para a cache independentemente da definição de tamanho. Configure as definições de cache, como tamanho e localização, quando instalar manualmente o cliente, quando utilizar a instalação de impulso do cliente, ou após a instalação.

Pode especificar o tamanho da pasta cache utilizando as definições do cliente na consola 'Gestor de Configuração'. Para mais informações, consulte [as definições de cache do Cliente](../deploy/about-client-settings.md#client-cache-settings).

A localização padrão para a `%windir%\ccmcache` cache do cliente do Gestor de Configuração é e o espaço padrão do disco é de 5120 MB.  

> [!IMPORTANT]  
> Não criptografe a pasta usada para a cache do cliente. O Gestor de Configuração não pode transferir conteúdo para uma pasta encriptada.  

### <a name="about-the-client-cache"></a>Sobre a cache do cliente  

O cliente do Gestor de Configuração descarrega o conteúdo para o software necessário logo após a sua implementação, mas aguarda para executá-lo até a hora programada de implementação. Na hora programada, o cliente do Gestor de Configuração verifica se o conteúdo está disponível na cache. Se o conteúdo estiver na cache e for a versão correta, o cliente utiliza o conteúdo em cache. Quando a versão necessária do conteúdo muda, ou se o cliente apagar o conteúdo para dar espaço a outro pacote, o cliente transfere novamente o conteúdo para a cache.  

Se o cliente tentar descarregar conteúdo para um programa ou aplicação superior ao tamanho da cache, a implementação falha devido ao tamanho insuficiente da cache. O cliente gera mensagem de estado 10050 por tamanho de cache insuficiente. Se aumentar o tamanho da cache mais tarde, o resultado é:  

- Para um programa necessário: O cliente não se recandidata automaticamente a descarregar o conteúdo. Redistribuir o pacote e o programa para o cliente.  
- Para uma aplicação necessária: O cliente tenta automaticamente descarregar o conteúdo quando descarrega a sua política de cliente.  

Se o cliente tentar descarregar um pacote inferior ao tamanho da cache, mas a cache está cheia, todas as implementações *necessárias* continuam a tentar até:

- O espaço cache está disponível
- O download vezes fora
- A contagem de retry atinge o seu limite

Se aumentar mais tarde o tamanho da cache, o cliente tenta descarregar novamente o pacote durante o intervalo de repetição seguinte. O cliente tenta descarregar o conteúdo a cada quatro horas até tentar 18 vezes.  

O conteúdo em cache não é automaticamente apagado. Permanece na cache pelo menos um dia depois do cliente usar esse conteúdo. Se configurar as propriedades do pacote com a opção de persistir o conteúdo na cache do cliente, o cliente não o apaga automaticamente. Se o espaço cache for utilizado por pacotes que foram descarregados nas últimas 24 horas, e o cliente tiver de descarregar novos pacotes, ou aumentar o tamanho da cache ou escolher a opção de eliminar conteúdo de cache persistente.  

Utilize os procedimentos seguintes para configurar a cache do cliente durante a instalação manual do cliente ou após a instalação do cliente.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Configure a cache durante a instalação manual do cliente  

Execute o comando CCMSetup.exe a partir da localização de origem da instalação e, entre as seguintes propriedades, especifique as que forem necessárias, separadas por espaços:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Utilize as definições de tamanho de cache disponíveis nas **Definições** do Cliente na consola 'Gestor de Configuração' em vez de SMSCACHESIZE. Para mais informações, consulte [as definições de cache do Cliente](../deploy/about-client-settings.md#client-cache-settings).

Para obter mais informações sobre como utilizar estas propriedades de linha de comando para CCMSetup.exe, consulte sobre as propriedades de [instalação do cliente](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>Configure a cache durante a instalação push do cliente  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o local apropriado. No separador **Casa** da fita, no grupo **Definições,** selecione Definições de **Instalação do Cliente**, e escolha a **instalação de impulso**do cliente . Mude para o separador Propriedades de **Instalação.**  

3. Especifique as seguintes propriedades, separadas por espaços:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Utilize as definições de tamanho de cache disponíveis nas **Definições** do Cliente na consola 'Gestor de Configuração' em vez de SMSCACHESIZE. Para mais informações, consulte [as definições de cache do Cliente](../deploy/about-client-settings.md#client-cache-settings).

     Para obter mais informações sobre como utilizar estas propriedades de linha de comando para CCMSetup.exe, consulte sobre as propriedades de [instalação do cliente](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>Configure a cache no computador cliente  

1. No computador cliente, abra o painel de controlo do Gestor de **Configuração.**  

2. Mude para o separador **Cache.** Desloque as propriedades de espaço e localização. A localização `%windir%\ccmcache`padrão é .  

3. Para eliminar os ficheiros na pasta cache, escolha **Apagar Ficheiros**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Configure o tamanho da cache do cliente nas definições do cliente

Ajuste o tamanho da cache do cliente sem ter de reinstalar o cliente. Utilize as definições de tamanho de cache disponíveis nas **Definições** do Cliente na consola 'Gestor de Configuração'. Para mais informações, consulte [as definições de cache do Cliente](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a>Desinstalar o cliente

Pode desinstalar o software cliente do Gestor de Configuração a partir de um computador utilizando **CCMSetup.exe** com a propriedade **/Desinstalar.** Executar CCMSetup.exe num computador individual a partir do pedido de comando ou implementar um pacote para desinstalar o cliente para uma recolha de computadores.  

> [!NOTE]  
> Não é possível desinstalar o cliente do Gestor de Configuração a partir de um dispositivo móvel. Se tiver de remover o cliente do Gestor de Configuração de um dispositivo móvel, tem de limpar o dispositivo, que elimina todos os dados do dispositivo móvel.  

1. Abra um pedido de comando windows como administrador. Mude a pasta para o local onde está localizada CCMSetup.exe, por exemplo:`cd %windir%\ccmsetup`

2. Executar o seguinte comando:`CCMSetup.exe /uninstall`

> [!TIP]  
> O processo de desinstalação não apresenta resultados no ecrã. Para verificar se o cliente desinstala com sucesso, consulte o seguinte ficheiro de registo:`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Se precisar de esperar que o processo de desinstalação esteja concluído antes de fazer outra coisa, corra `Wait-Process CCMSetup` no PowerShell. Este comando pode interromper um script até que o processo CCMSetup esteja concluído.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a>Gerir registos contraditórios

O Gestor de Configuração utiliza o identificador de hardware para tentar identificar clientes que possam ser duplicados e alertá-lo para os registos contraditórios. Por exemplo, se reinstalar um computador, o identificador de hardware seria o mesmo, mas o GUID utilizado pelo Gestor de Configuração pode ser alterado.  

O Gestor de Configuração resolve automaticamente os conflitos utilizando a autenticação do Windows da conta de computador ou um certificado PKI a partir de uma fonte fidedigna. Quando o Gestor de Configuração não consegue resolver o conflito de identificadores de hardware duplicados, uma definição de hierarquia determina o comportamento.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Alterar a definição de hierarquia para gerir registos contraditórios  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**

1. Na fita, selecione **Definições de Hierarquia**.

1. Mude para o separador De Aprovação de **Clientes e Registos Contraditórios** e selecione uma das seguintes opções:

    - **Resolver automaticamente registos contraditórios**
    - **Resolver registos conflituosos manualmente**

### <a name="manually-resolve-conflicting-records"></a>Resolver registos conflituosos manualmente  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda o **Status do Sistema**e selecione o nó de **Registos Contraditórios.**  

1. Selecione um ou mais registos contraditórios e, em seguida, escolha **O Registo Contraditório**.  

1. Selecione uma das seguintes opções:  

    - **Fusão**: Combine o registo recentemente detetado com o registo de cliente existente.  

    - **Novo**: Criar um novo recorde para o registo de clientes em conflito.  

    - **Bloco**: Crie um novo recorde para o registo de clientes em conflito, mas marque-o como bloqueado.  


## <a name="manage-duplicate-hardware-identifiers"></a>Gerir identificadores de hardware duplicados

Pode fornecer uma lista de identificadores de hardware que o Gestor de Configuração ignora para o arranque de PXE e registo de cliente. Esta lista ajuda a resolver duas questões comuns:

1. Muitos novos dispositivos não incluem uma porta Ethernet a bordo. Os técnicos utilizam um adaptador USB-to-Ethernet para estabelecer uma ligação com fios para efeitos de implantação de SISTEMA. Estes adaptadores são frequentemente partilhados devido ao custo e à usabilidade geral. O site utiliza o endereço MAC deste adaptador para identificar o dispositivo. Assim, a reutilização do adaptador torna-se problemática sem ações adicionais de administrador entre cada implantação. Para reutilizar o adaptador neste cenário, exclua o seu endereço MAC.

2. Embora o atributo SMBIOS deva ser único, alguns dispositivos de hardware especializados têm identificadores duplicados. Exclua este identificador duplicado e confie no endereço MAC único de cada dispositivo.

Utilize o seguinte processo para adicionar identificadores de hardware para o Gestor de Configuração ignorar:

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**

2. No separador **Home** da fita, no grupo **Sites,** escolha **Definições de Hierarquia**.

3. Mude para o **separador De Aprovação de Clientes e Registos Contraditórios.** Para adicionar novos identificadores de hardware, escolha **Adicionar** na secção **de identificadores de hardware Duplicate.**

> [!TIP]
> A partir da versão 1910, utilize os seguintes cmdlets PowerShell para automatizar a gestão de identificadores de hardware duplicados:<!-- 4852819 -->
>
> - Novo CMDuplicateHardwareIdGuid
> - Remover-CMDuplicateHardwareIdGuid
> - Novo CMDuplicateHardwareIdMacAddress
> - Remover-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a>Iniciar a recuperação de políticas

Um cliente do Gestor de Configuração descarrega a sua política de cliente numa programação que configura como uma definição de cliente. Também pode iniciar a recuperação de políticas a pedido do cliente. Por exemplo, para situações de resolução de problemas ou de testes.  

- [Notificação do cliente](#bkmk_policy-notify)
- [O painel de controlo do cliente](#bkmk_policy-manual)
- [Centro de Suporte](#bkmk_policy-support)
- [Um roteiro](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a>Iniciar a recuperação da política do cliente com a notificação do cliente  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione **Dispositivos**.  

1. Selecione o dispositivo que pretende descarregar. No separador **Home** da fita, no grupo **Dispositivo,** selecione Notificação do **Cliente,** e depois escolha baixar a **política do computador**.  

    > [!NOTE]  
    > Também pode utilizar a notificação do cliente para iniciar a recuperação de políticas para todos os dispositivos numa coleção.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a>Inicie a recuperação da política do cliente do painel de controlo do cliente do Gestor de Configuração

1. Abra o painel de controlo do Gestor de **Configuração** no computador.  

2. Mude para o separador **Ações.** Selecione o **Ciclo de Recuperação de & avaliação** da política da máquina para iniciar a política do computador e, em seguida, selecione **Run Now**.  

3. Selecione **OK** para confirmar a solicitação.  

4. Repita os passos anteriores para quaisquer outras ações. Por exemplo, **o Ciclo de Recuperação de & avaliação** da política do utilizador para as definições do cliente do utilizador.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a>Iniciar a recuperação da política do cliente com o Centro de Apoio

Use o Centro de Apoio para solicitar e ver a política do cliente. Para mais informações, consulte a [referência do Centro](../../support/support-center-ui-reference.md#bkmk_support-policy)de Suporte .

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a>Iniciar a recuperação da política do cliente por script  

1. Abra um editor de scripts, como o Notepad ou o Windows PowerShell ISE.  

2. Copiar e inserir o seguinte código PowerShell<!-- SCCMDocs#1591 --> no ficheiro:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Para obter mais informações sobre os iDs de horário, consulte [IDs de mensagem](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Guarde o ficheiro com uma extensão .ps1.  

4. Executa o guião no cliente.
