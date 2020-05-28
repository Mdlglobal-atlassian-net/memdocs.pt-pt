---
title: Ativar atualizações de terceiros
titleSuffix: Configuration Manager
description: Ativar atualizações de terceiros no Gestor de Configuração
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5461f888bfa2b749061eef4000f0d7c5f756b84
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906754"
---
# <a name="enable-third-party-updates"></a>Ativar as atualizações de terceiros 

*Aplica-se a: Gestor de Configuração (ramo atual)*

Começando com a versão 1806, o nó de Catálogos de Atualizações de **Software de Terceiros** na consola Do Gestor de Configuração permite-lhe subscrever catálogos de terceiros, publicar as suas atualizações no seu ponto de atualização de software (SUP), e depois implementá-los para os clientes.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade por defeito. Antes de o utilizar, ative a funcionalidade opcional Ativar suporte de **atualização de terceiros nos clientes**. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Pré-requisitos 
- Espaço suficiente para o disco na pasta WSUSContent do ponto de atualização de software de topo para armazenar o conteúdo binário de origem para atualizações de software de terceiros.
    - A quantidade de armazenamento necessário varia em função do fornecedor, tipos de atualizações e atualizações específicas que publica para implementação.
    - Se precisar de mover a pasta WSUSContent para outra unidade com mais espaço livre, consulte o Como alterar o local onde a [WSUS armazena atualizações de bloglocalmente.](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally)
- O serviço de sincronização de atualização de software de terceiros requer acesso à Internet.
    - Para a lista de catálogos de parceiros, é necessário download.microsoft.com sobre a porta HTTPS 443. 
    -  Acesso à Internet a quaisquer catálogos de terceiros e atualizar ficheiros de conteúdos. Podem ser necessários portos adicionais que não sejam 443.
    - As atualizações de terceiros utilizam as mesmas definições de procuração que o SUP.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Requisitos adicionais quando o SUP está remoto do servidor de topo do site 

1. O SSL deve ser ativado no SUP quando estiver remoto. Isto requer um certificado de autenticação do servidor gerado a partir de uma autoridade de certificados internos ou através de um fornecedor público.
    - [Configure sSL no WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Quando configurar o SSL no WSUS, note que alguns dos serviços web e diretórios virtuais são sempre HTTP e não HTTPS. 
        - O Gestor de Configuração descarrega conteúdo de terceiros para pacotes de atualização de software do seu diretório de conteúdo wSUS em HTTP.   
    - [Configure o SSL no SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Ao definir as atualizações de terceiros A configuração do certificado de assinatura WSUS para o Gestor de **Configuração gere o certificado** nas Propriedades componentes do ponto de atualização do software, são necessárias as seguintes configurações para permitir a criação do certificado de assinatura WSUS auto-assinado: 
   - O registo remoto deve ser ativado no servidor SUP.
   -  A conta de ligação do **servidor WSUS** deve ter permissões de registo remoto no servidor SUP/WSUS. 


3. Crie a seguinte chave de registo no servidor do site do Gestor de Configuração: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, criar um novo DWORD denominado **EnableSelfSignedCertificates** com um valor de `1` . 

4. Para permitir a instalação do certificado de assinatura WSUS auto-assinado para as Editoras Fidedignas e lojas Trust Root no servidor Remoto SUP:
   - A conta de ligação ao **servidor WSUS** deve ter permissões de administração remotas no servidor SUP.

     Se este artigo não for possível, exporte o certificado da loja WSUS do computador local para as lojas Trusted Publisher e Trusted Root. 

> [!NOTE] 
>A conta de ligação ao **servidor WSUS** pode ser identificada visualizando o **separador proxy e** as definições de conta nas propriedades de função do Sistema de Site do SUP. Se uma conta não for especificada, a conta de computador do servidor do site é utilizada.

## <a name="enable-third-party-updates-on-the-sup"></a>Ativar atualizações de terceiros no SUP
Se ativar esta opção, pode subscrever catálogos de atualizações de terceiros na consola 'Gestor de Configuração'. Pode então publicar essas atualizações na WSUS e implantá-las para clientes. Os seguintes passos devem ser executados uma vez por hierarquia para ativar e configurar a função para utilização. Os passos podem ter de ser reexecutados se alguma vez substituir o servidor WSUS de nível superior. 

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **Configuração**do Site, e selecionar o nó **de Sites.**
2. Selecione o site de alto nível na hierarquia. Na fita, clique em **Configurar componentes**do site , e selecione **Software Update Point**.
3. Mude para o separador **Atualizações de Terceiros.** Selecione a opção **Ativar atualizações de software de terceiros**.

    ![Imagens de propriedades SUP de terceiros](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configure o certificado de assinatura WSUS
Terá de decidir se pretende que o Gestor de Configuração gere automaticamente o certificado de assinatura WSUS de terceiros utilizando um certificado auto-assinado ou se precisa configurar manualmente o certificado. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Gerir automaticamente o certificado de assinatura WSUS
Se não tiver a obrigação de utilizar certificados PKI, pode optar por gerir automaticamente os certificados de assinatura para atualizações de terceiros. A gestão de certificados WSUS é feita como parte do ciclo de sincronização e é registada no `wsyncmgr.log` . 

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **Configuração**do Site, e selecionar o nó **de Sites.**
2. Selecione o site de alto nível na hierarquia. Na fita, clique em **Configurar componentes**do site , e selecione **Software Update Point**.
3. Mude para o separador **Atualizações de Terceiros.** Selecione o Gestor de **Configuração**da opção gere o certificado . 
4. Um novo certificado de **assinatura WSUS de terceiros** é criado no nó de **Certificados** sob **Segurança** no espaço de trabalho **da Administração.**  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Gerir manualmente o certificado de assinatura WSUS
Se precisar de configurar manualmente o certificado, como por exemplo a necessidade de utilizar um certificado PKI, terá de utilizar o Editor de [Atualizações](../tools/updates-publisher-options.md#update-server) do Centro de Sistema ou outra ferramenta para o fazer.  

1. Configure o certificado de assinatura utilizando o Editor de [Atualizações](../tools/updates-publisher-options.md#update-server)do Centro de Sistema .
2. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **Configuração**do Site, e selecionar o nó **de Sites.**
3. Selecione o site de alto nível na hierarquia. Na fita, clique em **Configurar componentes**do site , e selecione **Software Update Point**.
4. Mude para o separador **Atualizações de Terceiros.** Selecione a opção para **gerir manualmente o certificado**.


## <a name="enable-third-party-updates-on-the-clients"></a>Ativar atualizações de terceiros sobre os clientes
Ative atualizações de terceiros sobre os clientes nas definições do cliente. A definição define a política do agente De atualização do Windows para [permitir atualizações assinadas para uma localização do serviço de atualização intranet microsoft](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Esta definição de cliente também instala o certificado de assinatura WSUS para a loja Trusted Publisher no cliente. A sessão de registo de gestão de certificados é vista `updatesdeployment.log` nos clientes.  Faça estes passos para cada definição personalizada do cliente que pretende utilizar para atualizações de terceiros. Para mais informações, consulte o artigo [sobre as definições](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) do cliente.

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Definições do **Cliente.**
2. Selecione uma definição personalizada de cliente existente ou crie uma nova. 
3. Selecione o separador **Atualizações** de Software no lado esquerdo. Se não tiver este separador, certifique-se de que a caixa de **Atualizações** de Software está ativada.
4. Definir **Ativar atualizações de software de terceiros** para **Sim**. 


## <a name="add-a-custom-catalog"></a>Adicione um catálogo personalizado
*Os catálogos de parceiros* são catálogos de fornecedores de software que têm as suas informações já registadas na Microsoft. Com catálogos de parceiros, pode subscrever-os sem ter de especificar qualquer informação adicional. Os catálogos que adiciona são *chamados catálogos personalizados.* Pode adicionar um catálogo personalizado de um fornecedor de atualização de terceiros ao Gestor de Configuração. Os catálogos personalizados devem utilizar https e as atualizações devem ser assinadas digitalmente. 

1. Vá ao espaço de trabalho da Biblioteca de Atualizações de **Software,** expanda **as atualizações**de Software e selecione o nó de **Catálogos de Atualizações de Software de Terceiros.** 
   
     ![Imagem de nó de atualizações de terceiros](media/third-party-updates-node.PNG)
2. Clique em **Adicionar Catálogo Personalizado** na fita. 

     ![Atualizações de terceiros adicionam catálogo personalizado](media/third-party-updates-custom-catalog.png)
1. Na página **Geral,** especifique os seguintes itens: 
    - **Baixar URL**: Um endereço HTTPS válido do catálogo personalizado.
    - **Editor**: O nome da organização que publica o catálogo. 
    - **Nome**: O nome do catálogo a exibir na Consola de Gestor de Configuração. 
    - **Descrição**: Uma descrição do catálogo. 
    - **URL** de suporte (opcional): Um endereço HTTPS válido de um website para obter ajuda com o catálogo. 
    - **Contacto de Suporte** (opcional): Informações de contacto para obter ajuda com o catálogo. 
2. Clique em **Seguir** para rever o resumo do catálogo e para continuar a completar o Assistente personalizado de **catálogo de atualizações de software de terceiros**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Subscreva um catálogo de terceiros e atualizações de sincronização
Quando subscreve um catálogo de terceiros na consola 'Gestor de Configuração', os metadados de cada atualização do catálogo estão sincronizados nos servidores WSUS para os seus SUPs. A sincronização dos metadados permite que os clientes determinem se alguma das atualizações é aplicável. Execute os seguintes passos para cada catálogo de terceiros a que pretende subscrever:  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações** de software e selecionar o nó de **Catálogos de Atualizações de Software de Terceiros.**  
2. Selecione o catálogo para subscrever e clique **Em subscrever o Catálogo** na fita. 
    ![Atualizações de terceiros adicionam catálogo personalizado](media/third-party-updates-subscribe.png)
3. Reveja e aprove o certificado de catálogo.  
   > [!NOTE]
   > 
   > Quando subscreve um catálogo de atualizações de software de terceiros, o certificado que analisa e aprova no assistente é adicionado ao site. Este certificado é do tipo Catálogo **de Atualizações de Software de Terceiros.** Você pode geri-lo a partir do nó de **Certificados** sob **segurança** no espaço de trabalho **da Administração.**  
4. Conclua o assistente. Após a subscrição inicial, o catálogo deve começar a descarregar em poucos minutos. 
    - O catálogo sincroniza automaticamente a cada 7 dias.
    - Clique em **Sync agora** na fita para forçar uma sincronização.
5. Após o download do catálogo, os metadados do produto precisam de ser sincronizados a partir da base de dados wSUS para a base de dados do Gestor de Configuração. [Inicie manualmente as atualizações de software sincronizando](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) a informação do produto.
6. Assim que a informação do produto estiver sincronizada, [configure o SUP para sincronizar o produto desejado](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) no Configurmanager.  
7. [Inicie manualmente as atualizações de software sincronizando-se](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar as atualizações do novo produto no 'Gestor de Configuração'.  
8. Quando a sincronização estiver concluída, pode ver as atualizações de terceiros no nó **All Updates.** Estas atualizações são publicadas apenas como atualizações **apenas de metadados** até que opte por publicá-las. 
     - O ícone com a seta azul representa uma atualização de software apenas de metadados. ![Ícone de atualização de software apenas metadados](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publicar e implementar atualizações de software de terceiros 
Uma vez que as atualizações de terceiros estejam no nó **All Updates,** pode escolher quais as atualizações que devem ser publicadas para implementação. Quando publica uma atualização, os ficheiros binários são descarregados do fornecedor e colocados no diretório WSUSContent no SUP de alto nível. 

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expanda **as Atualizações** de Software e selecione o nó **de Atualizações** de Software.
2. Clique em **Adicionar Critérios** para filtrar a lista de atualizações. Por exemplo, adicione **o Fornecedor** para **HP**. para ver todas as atualizações da HP.  
3. Selecione as atualizações que são necessárias pela sua organização. Clique em **publicar conteúdo de atualização de software de terceiros**.
    - Esta ação descarrega os binários de atualização do fornecedor e depois armazena-os na pasta WSUSContent no ponto de atualização de software de alto nível. 
4. [Inicie manualmente a sincronização](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) das atualizações de software para alterar o estado das atualizações publicadas apenas de metadados para atualizações implantáveis com conteúdo. 
    >[!NOTE]
    >Quando publica conteúdo de atualização de software de terceiros, quaisquer certificados utilizados para assinar o conteúdo são adicionados ao site. Estes certificados são do tipo Conteúdo **de Atualizações de Software de Terceiros.** Você pode geri-los a partir do nó de **Certificados** sob **segurança** no espaço de trabalho **da Administração.**  

5. Reveja os progressos no SMS_ISVUPDATES_SYNCAGENT.log. O registo está localizado no ponto de atualização de software de topo na pasta Logs do sistema de site.
6. Implemente as atualizações utilizando o processo de atualizações de [software Deploy.](../deploy-use/deploy-software-updates.md) 
7. Na página de Localizações de **Descarregamento** do Assistente de Atualizações de **Software de Implementação,** selecione a opção padrão para **descarregar atualizações de software a partir da internet**. Neste cenário, o conteúdo já é publicado no ponto de atualização de software, que é usado para descarregar o conteúdo para o pacote de implementação.
8. Os clientes terão de fazer uma varredura e avaliar atualizações antes de poder ver os resultados da conformidade.  Pode acionar manualmente este ciclo a partir do painel de controlo do Gestor de Configuração num cliente, executando a ação **software Updates Scan Cycle.**


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a>Melhorias para atualizações de terceiros a partir de 1910
<!--4469002-->
Tem agora mais controlos granulares sobre a sincronização de catálogos de atualizações de terceiros. A partir da versão 1910 do Configurmanager de Configuração, pode configurar o calendário de sincronização de cada catálogo de forma independente. Ao utilizar catálogos que incluam atualizações categorizadas, pode configurar a sincronização para incluir apenas categorias específicas de atualizações para evitar sincronizar todo o catálogo. Com catálogos categorizados, quando estiver confiante de que irá implementar uma categoria, pode configurá-la para descarregar e publicar automaticamente para a WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Detete a programação para um catálogo numa nova subscrição de catálogo

1. Vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e, em seguida, selecione o nó de **Catálogos de Atualizações de Software de Terceiros.**
1. Selecione o catálogo para subscrever e clique **Em subscrever o Catálogo** na fita.
1. Escolha as suas opções na página **'Agendar'** caso pretenda anular o calendário de sincronização predefinido:
   - **Horário simples**: Escolha o intervalo de hora, dia ou mês.
   - **Horário personalizado**: Definir um horário complexo.

### <a name="update-the-schedule-per-catalog"></a>Atualizar o horário por catálogo

1. Vá ao espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e, em seguida, selecione o nó de **Catálogos de Atualizações de Software de Terceiros.**
1. Clique à direita no catálogo e selecione **Propriedades**.
1. Escolha as suas opções no separador Agendar: 
   - **Horário simples**: Escolha o intervalo de hora, dia ou mês.
   - **Horário personalizado**: Definir um horário complexo.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Nova subscrição de um catálogo v3 de terceiros

> [!IMPORTANT]
> Esta opção só está disponível para catálogos de atualizações de terceiros v3, que suportam categorias para atualizações. Estas opções são desativadas para catálogos que não sejam publicados no novo formato v3.


1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações** de software e selecionar o nó de **Catálogos de Atualizações de Software de Terceiros.**
1. Selecione o catálogo para subscrever e clique **Em subscrever o Catálogo** na fita.
1. Escolha as suas opções na página **Select Categories:**

   - **Sincronizar todas as categorias de atualização** (padrão)
       - Sincroniza todas as atualizações no catálogo de atualizações de terceiros para O Gestor de Configuração.
   -  **Selecione categorias para sincronização**
       - Escolha quais categorias e categorias infantis sincronizar em Gestor de Configuração.

      ![Selecione categorias de atualizações para sincronizar no Gestor de Configuração](./media/4469002-select-categories-for-sync.png)
1. Escolha se pretende encenar conteúdos de **atualização** para o catálogo. Quando você encenar o conteúdo, todas as atualizações nas categorias selecionadas são automaticamente descarregadas para o seu ponto de atualização de software de nível superior, o que significa que você não precisa garantir que eles já estão descarregados antes de ser implementado. Só deve encenar automaticamente o conteúdo para atualizações que é provável que as implemente para evitar requisitos excessivos de largura de banda e armazenamento.

   - **Não encere conteúdo, sincronize apenas para digitalização (recomendado)**
     - Não descarregue nenhum conteúdo para atualizações no catálogo de terceiros
   - **Fase do conteúdo para categorias selecionadas automaticamente**
     - Escolha as categorias de atualização que descarregarão automaticamente os conteúdos.
     - O conteúdo para atualizações em categorias selecionadas será descarregado para o diretório de conteúdo wSUS do ponto de atualização de software de topo.
      ![Selecione categorias de atualização para conteúdo sonoro](./media/4469002-stage-content.png)
1. Desgene a sua **Agenda** para a sincronização do catálogo e, em seguida, complete o assistente.

 

### <a name="edit-an-existing-subscription"></a>Editar uma subscrição existente

> [!IMPORTANT]
> Esta opção só está disponível para catálogos de atualizações de terceiros v3, que suportam categorias para atualizações. Estas opções são desativadas para catálogos que não sejam publicados no novo formato v3.

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações** de software e selecionar o nó de **Catálogos de Atualizações de Software de Terceiros.**
1. Clique à direita no catálogo e selecione **Propriedades**.
1. Escolha as suas opções no separador **Categorias Selecionadas.**
   - **Sincronizar todas as categorias de atualização** (padrão)
       - Sincroniza todas as atualizações no catálogo de atualizações de terceiros para O Gestor de Configuração.
   -  **Selecione categorias para sincronização**
       - Escolha quais categorias e categorias infantis sincronizar em Gestor de Configuração.
1. Escolha as suas opções para o separador de conteúdo da **atualização do Palco.**
   - **Não encere conteúdo, sincronize apenas para digitalização (recomendado)**
     - Não descarregue nenhum conteúdo para atualizações no catálogo de terceiros
   - **Fase do conteúdo para categorias selecionadas automaticamente**
     - Escolha as categorias de atualização que descarregarão automaticamente os conteúdos.
     - O conteúdo para atualizações em categorias selecionadas será descarregado para o diretório de conteúdo wSUS do ponto de atualização de software de topo. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorização do progresso das atualizações de software de terceiros 

A sincronização de atualizações de software de terceiros é tratada pelo componente SMS_ISVUPDATES_SYNCAGENT no ponto de atualização padrão de software de alto nível. Pode visualizar mensagens de estado deste componente ou ver o estado mais detalhado no registo SMS_ISVUPDATES_SYNCAGENT.log. Este registo encontra-se no ponto de atualização de software de topo na pasta Logs do sistema do site. Por defeito, este caminho é C:\Program Files\Microsoft Configuration Manager\Logs. Para obter mais informações sobre a monitorização do processo geral de gestão de atualizações de software, consulte [as atualizações](../deploy-use/monitor-software-updates.md) de software do Monitor 

## <a name="known-issues"></a>Problemas conhecidos

- A máquina onde a consola está a funcionar é utilizada para descarregar as atualizações da WSUS e adicioná-la ao pacote de atualizações. O certificado de assinatura WSUS deve ser confiado na máquina da consola. Caso não seja, poderá ver problemas com a verificação de assinaturas durante o download de atualizações de terceiros. 
- O serviço de sincronização de atualização de software de terceiros não pode publicar conteúdo em atualizações apenas de metadados que foram adicionados à WSUS por outra aplicação, ferramenta ou script, como o SCUP. A ação **de atualização de software de terceiros** não se aciona nestas atualizações. Se necessitar de implementar atualizações de terceiros que esta funcionalidade ainda não suporta, utilize o seu processo existente na íntegra para implementar essas atualizações.  
-  O Gestor de Configuração tem uma nova versão para o formato de ficheiro de cabine de catálogo. A nova versão inclui os certificados para os ficheiros binários do fornecedor. Estes certificados são adicionados ao nó de **Certificados** sob **segurança** no espaço de trabalho da **Administração** assim que você aprove e confie no catálogo.  
     - Ainda pode utilizar a versão de ficheiro de cabine de catálogo mais antigo, desde que o URL de descarregamento seja https e as atualizações estejam assinadas. O conteúdo não será publicado porque os certificados para os binários não estão no ficheiro da cabine e já estão aprovados. Pode contornar esta questão encontrando o certificado no nó dos **Certificados,** desbloqueando-o e publicando novamente a atualização. Se estiver a publicar várias atualizações assinadas com certificados diferentes, terá de desbloquear cada certificado que seja utilizado.
     - Para mais informações, consulte as mensagens de estado 11523 e 11524 na tabela de mensagens abaixo.
-  Quando o serviço de sincronização de atualização de software de terceiros no ponto de atualização de software de topo requer um servidor proxy para acesso à Internet, as verificações de assinatura digital podem falhar. Para mitigar este problema, configure as definições de proxy WinHTTP no sistema de site. Para mais informações, consulte os [comandos de Netsh para WinHTTP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)).
- Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a [definição](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) de cliente **disponível** estiver ativada. <!--6598587-->

## <a name="status-messages"></a>Mensagens de estado

| MensagemID       | Gravidade           | Descrição | Causa possível| Possível solução
| ------------- |-------------| -----|----|----|
| 11516     | Erro |Não publicou conteúdo para atualização "Update ID" porque o conteúdo não está assinado.  Só podem ser publicados conteúdos com assinaturas válidas.  |O Gestor de Configuração não permite que sejam publicadas atualizações não assinadas.| Publique a atualização de forma alternativa. </br></br>Veja se está disponível uma atualização assinada a partir do fornecedor.|
| 11523  | Aviso |  O catálogo "X" não inclui certificados de assinatura de conteúdo, as tentativas de publicar conteúdo sonoro para atualizações deste catálogo podem não ter sucesso até que os certificados de assinatura de conteúdo sejam adicionados e aprovados. | Esta mensagem pode ocorrer quando importa um catálogo que está a utilizar uma versão mais antiga do formato de ficheiro sinuoso.|Contacte o fornecedor do catálogo para obter um catálogo atualizado que inclua os certificados de assinatura de conteúdos. </br> </br> Os certificados para os binários não estão incluídos no ficheiro do táxi, pelo que o conteúdo não será publicado. Pode contornar esta questão encontrando o certificado no nó dos **Certificados,** desbloqueando-o e publicando novamente a atualização. Se estiver a publicar várias atualizações assinadas com certificados diferentes, terá de desbloquear cada certificado que seja utilizado.|
| 11524| Erro  | Não publicou a atualização "ID" devido à falta de metadados de atualização. | A atualização pode ter sido sincronizada para a WSUS fora do Gestor de Configuração.| Sincronizar a atualização com o Gestor de Configuração antes de tentar publicar o seu conteúdo.  </br> </br>Se uma ferramenta externa foi utilizada para publicar a atualização apenas como **Metadados,** utilize a mesma ferramenta para publicar o conteúdo da atualização.|



## <a name="working-with-third-party-updates-video"></a>Trabalhar com vídeo de atualizações de terceiros
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Deploy software updates](./deploy-software-updates.md)
