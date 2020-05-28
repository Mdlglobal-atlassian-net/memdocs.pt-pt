---
title: Instale pontos de distribuição em nuvem
titleSuffix: Configuration Manager
description: Utilize estes passos para configurar um ponto de distribuição em nuvem no Gestor de Configuração.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35379aed71544a25a98ec4dfa421be70c1bae851
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427751"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Instale um ponto de distribuição em nuvem para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A implementação para partilha de conteúdos do Azure mudou. Utilize um portal de gestão de nuvem ativado por conteúdo, permitindo que a opção de permitir que a CMG funcione como um ponto de distribuição na **nuvem e sirva conteúdo a partir do armazenamento Azure**. Para mais informações, consulte [Modificar um CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Não poderá criar um ponto tradicional de distribuição de nuvens no futuro. Para mais informações, consulte [funcionalidades removidas e depreciadas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Este artigo detalha os passos para instalar um ponto de distribuição em nuvem do Gestor de Configuração no Microsoft Azure. Inclui as seguintes secções:

- [Antes de começar](#bkmk_before)
- [Configurar](#bkmk_setup)
- [Configurar o DNS](#bkmk_dns)
- [Configurar proxy do servidor do site](#bkmk_proxy)
- [Distribuir conteúdo e configurar clientes](#bkmk_client)
- [Gerir e monitorizar](#bkmk_monitor)
- [Modificar](#bkmk_modify)
- [Resolução de problemas avançados](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a>Antes de começar

Comece por ler o artigo [Utilize um ponto](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)de distribuição em nuvem . Esse artigo ajuda-o a planear e a desenhar os seus pontos de distribuição em nuvem.

Utilize a seguinte lista de verificação para se certificar de que dispõe das informações e pré-requisitos necessários para criar um ponto de distribuição na nuvem:  

- O servidor do site pode ligar-se ao Azure. Se a sua rede utilizar um proxy, [configure a função do sistema do site](#bkmk_proxy).  

- O **ambiente Azure** para usar. Por exemplo, a Nuvem Pública Azure ou a Nuvem governamental azure dos EUA.  

- Começando na versão 1806 e *recomendado,* utilize a implementação do Gestor de **Recursos Azure.** Tem os seguintes requisitos:<!--1322209-->  

    - Integração com [o Diretório Ativo Azure](azure-services-wizard.md) para gestão de **nuvem.** A descoberta do utilizador da AD Azure não é necessária.  

    - O **ID de subscrição**Azure .  

    - O **Grupo de Recursos**Azure.  

    - Uma **conta de administradorde subscrição** precisa de iniciar sessão durante o assistente.  

- Um certificado de autenticação do **servidor,** exportado como a . Ficheiro PFX.  

- Um nome de **serviço** globalmente único para o ponto de distribuição em nuvem.  

    > [!TIP]  
    > Antes de solicitar o certificado de autenticação do servidor que utiliza este nome de serviço, confirme que o nome de domínio Desejado Do Azure é único. Por exemplo, *WallaceFalls.CloudApp.Net.*
    >
    > 1. Inicie sessão no [portal do Azure](https://portal.azure.com).
    > 1. **Selecione todos os recursos**e, em seguida, selecione **Adicionar**.
    > 1. Procure o **serviço Cloud**. Selecione **Criar**.
    > 1. No campo **de nome DNS,** escreva o prefixo que desejar, por exemplo *WallaceFalls*. A interface reflete se o nome de domínio está disponível ou já está a ser utilizado por outro serviço.
    >
    > Não crie o serviço no portal, basta utilizar este processo para verificar a disponibilidade do nome.

- A **região** de Azure para esta implantação.  

- Se ainda precisar de utilizar a **implementação** de serviço clássico do Azure na versão 1810 do Gestor de Configuração, precisa dos seguintes requisitos:  

    > [!Important]  
    > A partir da versão 1810, as implementações clássicas de serviço sintetizadas em Azure são depreciadas no Gestor de Configuração. Comece a utilizar as implementações do Gestor de Recursos Azure para o ponto de distribuição da nuvem. Para mais informações, consulte [o Gestor de Recursos Azure.](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager)  
    >
    > Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do ponto de distribuição da nuvem.<!-- 3605704 -->

    - O **ID de subscrição**Azure .  

    - Um certificado de **gestão**Azure, exportado como ambos. CER e . Ficheiros PFX. Um administrador de subscrição Azure precisa adicionar o . Certificado de gestão cer da assinatura no [portal Azure.](https://portal.azure.com)  

### <a name="branchcache"></a>BranchCache

Para permitir que um ponto de distribuição em nuvem utilize o Windows BranchCache, instale a funcionalidade BranchCache no servidor do site.<!-- SCCMDocs-pr#4054 -->

- Se o servidor do site tiver uma função de sistema de site de pontode distribuição no local, configure a opção nas propriedades dessa função para **ativar e configurar BranchCache**. Para mais informações, consulte [Configure um ponto de distribuição](install-and-configure-distribution-points.md#bkmk_config-general).

- Se o servidor do site não tiver uma função de ponto de distribuição, instale a funcionalidade BranchCache no Windows. Para mais informações, consulte [Instalar a função BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Se já distribuiu conteúdo para um ponto de distribuição na nuvem e, em seguida, decida ativar o BranchCache, instale primeiro a funcionalidade. Em seguida, redistribua o conteúdo para o ponto de distribuição da nuvem.

> [!NOTE]  
> Na versão 1810 do Gestor de Configuração e anterior, se tiver mais de um ponto de distribuição em nuvem, precisa de definir manualmente a palavra-passe da chave BranchCache. Para mais informações, consulte [o Microsoft Support KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a>Configurar  

Execute este procedimento no site para acolher este ponto de distribuição em nuvem, conforme determinado pelo seu [design](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud,** e selecione **Pontos**de Distribuição de Cloud . Na fita, selecione **Create Cloud Distribution Point**.  

2. Na página **geral** do Assistente de Ponto de Distribuição de Nuvem, configure as seguintes definições:  

    1. Primeiro especifique o **ambiente Azure.**  

    2. Começando na versão 1806 e *recomendado,* selecione a implementação do Gestor de **Recursos Azure** como método de implementação. Selecione **Iniciar sessão** para autenticar com uma conta de administrador de subscrição Azure. O assistente povoa automaticamente os restantes campos a partir da informação armazenada durante o pré-requisito de integração da AD Azure. Se possuir várias subscrições, selecione o ID de **subscrição** da subscrição desejada para utilizar.  

    > [!Note]  
    > A partir da versão 1810, as implementações clássicas de serviço sintetizadas em Azure são depreciadas no Gestor de Configuração.
    >
    > Se precisar de utilizar uma implementação clássica do serviço, selecione essa opção nesta página. Introduza primeiro o seu ID de **Subscrição**Azure . Em seguida, **selecione 'Navegar'** e selecione o . Ficheiro PFX para o certificado de gestão Azure.  

3. Selecione **Seguinte**. Espere enquanto o site testa a ligação a Azure.  

4. Na página **Definições,** especifique as seguintes definições e, em seguida, selecione **Seguinte**:  

    - **Região**: Selecione a região azure onde pretende criar o ponto de distribuição de nuvens.  

    - **Grupo de Recursos** (apenas método de implantação do Gestor de Recursos Azure)  

        - **Utilizar existentes**: Selecione um grupo de recursos existente da lista de abandono.  

        - **Criar novo**: Introduza o novo nome de grupo de recursos para criar na sua subscrição Azure.  

    - **Sítio primário**: Selecione o site principal para distribuir conteúdo para este ponto de distribuição.

    - **Ficheiro do certificado**: Selecione **Navegar** e selecione o . Ficheiro PFX para o certificado de autenticação do servidor deste ponto de distribuição em nuvem. O nome comum deste certificado preenche os campos de nome **fQDN** e **serviço** exigidos.  

        > [!NOTE]  
        > O certificado de autenticação do servidor de ponto de distribuição em nuvem suporta wildcards. Se utilizar um certificado wildcard, substitua o asterisco `*` ( ) no campo **FQDN** de serviço com o nome de anfitrião desejado para o serviço.  

5. Na página **Alertas,** configurar quotas de armazenamento, quotas de transferência e em que percentagem destas quotas pretende que o Gestor de Configuração gere alertas. Em seguida, selecione **Seguinte**.  

6. Conclua o assistente.  

### <a name="monitor-installation"></a>Instalação do monitor  

O site começa a criar um novo serviço hospedado para o ponto de distribuição em nuvem. Depois de fechar o assistente, monitorize o progresso da instalação do ponto de distribuição da nuvem na consola 'Gestor de Configuração'. Também monitorize o ficheiro **CloudMgr.log** no servidor do site principal. Se necessário, monitorize o fornecimento do serviço de nuvem no portal Azure.  

> [!NOTE]  
> Pode levar até 30 minutos para fornecer um novo ponto de distribuição em Azure. O ficheiro **CloudMgr.log** repete a seguinte mensagem até que a conta de armazenamento seja aprovisionada:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Depois de fornecer a conta de armazenamento, o serviço é criado e configurado.  

### <a name="verify-installation"></a>Verificar a instalação

Verifique se a instalação do ponto de distribuição da nuvem está completa utilizando os seguintes métodos:  

- Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **os Serviços cloud**e selecionar o nó pontos de distribuição em **nuvem.** Encontre o novo ponto de distribuição de nuvem na lista. A coluna 'Estado' deve estar **pronta**.  

- Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir **o Estado**do Sistema e selecionar o nó do Estado do **Componente.** Mostre todas as mensagens do componente **SMS_CLOUD_SERVICES_MANAGER** e procure a mensagem de estado ID **9409**.  

- Se necessário, vá ao portal Azure. A **implantação** para o ponto de distribuição da nuvem apresenta um estado de **Ready**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a>Configure DNS  

Antes que os clientes possam usar o ponto de distribuição da nuvem, devem ser capazes de resolver o nome do ponto de distribuição da nuvem para um endereço IP que o Azure gere. O ponto de gestão dá-lhes o **Serviço FQDN** do ponto de distribuição da nuvem. O ponto de distribuição da nuvem existe em Azure como o **nome de Serviço**. Consulte estes valores no separador **Definições** das propriedades do ponto de distribuição da nuvem.

> [!Note]  
> O nó **de Pontos** de Distribuição de Nuvem na consola inclui uma coluna chamada Nome de **Serviço,** mas na verdade mostra o valor **FQDN** do serviço. Para ver ambos os valores, abra **propriedades** para o ponto de distribuição da nuvem e mude para o separador **Definições.**  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

O nome comum do certificado de autenticação do servidor deve incluir o seu nome de domínio. Este nome é necessário quando compra um certificado a um fornecedor público. É recomendado ao emitir este certificado do seu PKI. Por exemplo, `WallaceFalls.contoso.com`. Quando especifica este certificado no Assistente de Ponto de Distribuição de Nuvem Create, o nome comum preenche a propriedade **FQDN** de serviço `WallaceFalls.contoso.com` (). O **nome de serviço** tem o mesmo nome de anfitrião e `WallaceFalls` anexa-o ao nome de domínio Azure, `cloudapp.net` . Neste cenário, os clientes precisam de resolver o **Serviço FQDN** do seu domínio `WallaceFalls.contoso.com` para o nome do **Serviço** Azure `WallaceFalls.cloudapp.net` (). Crie um pseudónimo CNAME para mapear estes nomes.

### <a name="create-cname-alias"></a>Criar pseudónimos CNAME

Crie um registo de nome canónico (CNAME) no DNS público e virado para a Internet da sua organização. Este registo cria um pseudónimo para a propriedade **FQDN** do ponto de distribuição da nuvem que os clientes recebem, para o nome do **Serviço**Azure. Por exemplo, crie um novo disco CNAME para `WallaceFalls.contoso.com` `WallaceFalls.cloudapp.net` .  

### <a name="client-name-resolution-process"></a>Processo de resolução de nome do cliente

O seguinte processo mostra como um cliente resolve o nome do ponto de distribuição da nuvem:  

1. O cliente obtém o **Serviço FQDN** do ponto de distribuição em nuvem na lista de fontes de conteúdo. Por exemplo, `WallaceFalls.contoso.com`.  

2. Consulta o DNS, que resolve o Serviço FQDN utilizando o pseudónimo CNAME para o **nome do Serviço**Azure . Por exemplo, `WallaceFalls.cloudapp.net`.  

3. Volta a questionar o DNS, que resolve o nome de serviço Azure para o endereço IP público do Azure.  

4. O cliente utiliza este endereço IP para iniciar a comunicação com o ponto de distribuição da nuvem.  

5. O ponto de distribuição em nuvem apresenta o certificado de autenticação do servidor ao cliente. O cliente usa a cadeia fiducida do certificado para validar.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a>Configurar proxy do servidor do site  

O servidor principal do site que gere o ponto de distribuição da nuvem precisa de comunicar com o Azure. Se a sua organização utilizar um servidor proxy para controlar o acesso à Internet, configure o servidor principal do site para utilizar este proxy.  

Para mais informações, consulte o [suporte do servidor Proxy](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a>Distribuir conteúdo e configurar clientes

Distribua o conteúdo para o ponto de distribuição da nuvem o mesmo que qualquer outro ponto de distribuição no local. O ponto de gestão não inclui o ponto de distribuição na nuvem na lista de locais de conteúdo, a menos que tenha o conteúdo que os clientes solicitam. Para mais informações, consulte [Distribuir e gerir conteúdos.](deploy-and-manage-content.md)

Gerencie um ponto de distribuição em nuvem o mesmo que qualquer outro ponto de distribuição no local. Estas ações incluem atribuí-lo a um grupo de pontos de distribuição e a gestão de pacotes de conteúdo. Para mais informações, consulte [Instalar e configurar pontos](install-and-configure-distribution-points.md)de distribuição .

As definições padrão do cliente permitem automaticamente que os clientes utilizem pontos de distribuição em nuvem. Controle o acesso a todos os pontos de distribuição na nuvem da sua hierarquia com a seguinte configuração de cliente:  

- No grupo **Cloud Settings,** modifique a definição **Permitir o acesso aos pontos**de distribuição em nuvem .  

    - Por defeito, esta definição está definida para **Sim**.  

    - Modifique e implemente esta definição tanto para utilizadores como para dispositivos.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a>Gerir e monitorizar  

Monitorize o conteúdo que distribui para um ponto de distribuição na nuvem o mesmo que com quaisquer outros pontos de distribuição no local. Para mais informações, consulte [o monitor de conteúdos](monitor-content-you-have-distributed.md).

Quando visualizar a lista de pontos de distribuição em nuvem na consola, pode adicionar colunas adicionais à lista. Por exemplo, a coluna **Data egress** mostra a quantidade de dados que os clientes descarregaram do serviço nos últimos 30 dias.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a>Alertas  

O Gestor de Configuração verifica periodicamente o serviço Azure. Se o serviço não estiver ativo, ou se houver problemas de subscrição ou certificado, o Gestor de Configuração levanta um alerta.

Configure limiares para a quantidade de dados que pretende armazenar no ponto de distribuição da nuvem e para a quantidade de dados que os clientes descarregam a partir do ponto de distribuição. Utilize alertas para estes limiares para o ajudar a decidir quando parar ou eliminar o serviço na nuvem, ajustar o conteúdo que armazena no ponto de distribuição da nuvem ou modificar quais os clientes que podem utilizar o serviço.

- **Limiar de alerta**de armazenamento : O limiar de alerta de armazenamento estabelece um limite superior em GB sobre a quantidade de dados ou conteúdos que pretende armazenar no ponto de distribuição da nuvem. Por padrão, este limiar é de 2.000 GB. O Gestor de Configuração gera alertas e alertas críticos quando o espaço livre restante atinge os níveis que especifica. Por padrão, estes alertas ocorrem a 50% e 90% do limiar.  

- **Limiar**de alerta de transferência mensal : O limiar de alerta de transferência mensal ajuda-o a monitorizar a quantidade de conteúdo que transfere do ponto de distribuição para os clientes durante um período de 30 dias. Por padrão, este limiar é de 10.000 GB. O site levanta alertas e alertas críticos quando as transferências atingem valores que define. Por padrão, estes alertas ocorrem a 50% e 90% do limiar.  

    > [!IMPORTANT]  
    > O Gestor de Configuração monitoriza a transferência de dados, mas não impede a transferência de dados para além do limiar de alerta de transferência especificado.  

Especifique os limiares para cada ponto de distribuição da nuvem durante a instalação ou use o separador **Alertas** das propriedades do ponto de distribuição da nuvem.  

> [!NOTE]  
> Os alertas para um ponto de distribuição na nuvem dependem das estatísticas de utilização do Azure, que podem demorar até 24 horas a ficar disponíveis. Para mais informações sobre o Storage Analytics para Azure, consulte [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Num ciclo de hora a hora, o site primário que monitoriza o ponto de distribuição em nuvem descarrega dados de transações do Azure. Armazena estes dados de transação no `CloudDP-<ServiceName>.log` ficheiro do servidor do site. O Gestor de Configuração avalia então esta informação contra as quotas de armazenamento e transferência para cada ponto de distribuição na nuvem. Quando a transferência de dados atinge ou excede o volume especificado para avisos ou alertas críticos, o Gestor de Configuração gera o alerta apropriado.  

> [!WARNING]  
> Uma vez que o site descarrega informações sobre transferências de dados do Azure a cada hora, o uso pode exceder um limiar de aviso ou crítico antes que o Gestor de Configuração possa aceder aos dados e levantar um alerta.  


## <a name="modify"></a><a name="bkmk_modify"></a>Modificar

Veja informações de alto nível sobre o ponto de distribuição no nó **pontos** de distribuição da nuvem sob **os Serviços cloud** no espaço de trabalho da **Administração** da consola De Configuração Manager. Selecione um ponto de distribuição e selecione **Propriedades** para ver mais detalhes.  

Ao editar as propriedades de um ponto de distribuição em nuvem, os seguintes separadores incluem definições para editar:  

#### <a name="settings"></a>Definições

- **Descrição**  

- **Ficheiro do certificado**: Antes de expirar o certificado de autenticação do servidor, emita um novo certificado com o mesmo nome comum. Em seguida, adicione o novo certificado aqui para que o serviço comece a usar. Se o certificado expirar, os clientes não confiarão e usarão o serviço.  

#### <a name="alerts"></a>Alertas

Ajuste os limiares de dados para armazenamento e alertas mensais de transferência.  

#### <a name="content"></a>Conteúdo

Gerir o conteúdo da mesma forma que para um ponto de distribuição no local.  

### <a name="redeploy-the-service"></a>Reutilizar o serviço

Alterações mais significativas, como as seguintes configurações, exigem a reafectação do serviço:

- Método clássico de implantação para Gestor de Recursos Azure
- Subscrição
- Nome do Serviço
- Privado para público PKI
- Região do Azure

A partir da versão 1806, se tiver um ponto de distribuição em nuvem existente no método de implementação clássico, de modo a utilizar o método de implementação do Gestor de Recursos Azure, precisa de implantar um novo ponto de distribuição em nuvem. Existem duas opções:

- Se quiser reutilizar o mesmo nome de serviço:  

    1. Primeiro apague o ponto clássico de distribuição de nuvens. Se não houver outro ponto de distribuição na nuvem, então os clientes podem não ser capazes de obter conteúdo.  

    2. Crie um novo ponto de distribuição de nuvem utilizando uma implementação do Gestor de Recursos. Reutilizar o mesmo certificado de autenticação do servidor.  

    3. Distribua o conteúdo necessário do pacote de software para o novo ponto de distribuição na nuvem.  

- Se quiser usar um novo nome de serviço:  

    1. Crie um novo ponto de distribuição de nuvem utilizando uma implementação do Gestor de Recursos. Utilize um novo certificado de autenticação do servidor.  

    2. Distribua o conteúdo necessário do pacote de software para o novo ponto de distribuição na nuvem.  

    3. Elimine o ponto clássico de distribuição de nuvens.

> [!Tip]  
> Para determinar o modelo atual de implantação de um ponto de distribuição em nuvem:<!--SCCMDocs issue #611-->  
>
> 1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud**e selecione o nó de Pontos de Distribuição de **Nuvem.**  
> 2. Adicione o atributo do Modelo de **Implantação** como uma coluna à vista da lista. Para uma implementação do Gestor de Recursos, este atributo é o Gestor de **Recursos Azure.**  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Parar ou iniciar o serviço de nuvem a pedido

Pare um ponto de distribuição em nuvem a qualquer momento na consola 'Gestor de Configuração'. Esta ação impede imediatamente os clientes de descarregarem conteúdo adicional do serviço. Reinicie o serviço de nuvem a partir da consola 'Gestor de Configuração' para restaurar o acesso aos clientes. Por exemplo, pare um serviço na nuvem quando atingir um limiar de dados.  

Quando para um ponto de distribuição na nuvem, o serviço de nuvem não apaga o conteúdo da conta de armazenamento. Também não impede que o servidor do site transere conteúdo adicional para o ponto de distribuição da nuvem. O ponto de gestão ainda devolve o ponto de distribuição na nuvem aos clientes como uma fonte de conteúdo válida.

Utilize o seguinte procedimento para parar um ponto de distribuição em nuvem:  

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir **os Serviços cloud**e selecionar o nó pontos de distribuição em **nuvem.**  

2. Selecione o ponto de distribuição da nuvem. Para parar o serviço de nuvem que funciona em Azure, selecione o **serviço Stop** na fita.  

3. Selecione **o serviço Iniciar** para reiniciar o ponto de distribuição da nuvem.  

### <a name="delete-a-cloud-distribution-point"></a>Eliminar um ponto de distribuição de nuvem

Para desinstalar um ponto de distribuição em nuvem, selecione o ponto de distribuição na consola 'Gestor de Configuração' e, em seguida, **selecione Delete**.  

Ao eliminar um ponto de distribuição em nuvem de uma hierarquia, o Gestor de Configuração remove o conteúdo do serviço de nuvem em Azure.

A remoção manual de quaisquer componentes em Azure faz com que o sistema seja inconsistente. Este estado deixa informações órfãs, e comportamentos inesperados podem ocorrer.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a>Resolução avançada de problemas

Se necessitar de recolher o registo de diagnóstico dos VMs Azure para ajudar a resolver problemas com o seu ponto de distribuição na nuvem, utilize a seguinte amostra PowerShell para ativar a extensão de diagnóstico do serviço para a subscrição:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

A amostra que se segue é um exemplo **de diagnósticos.wadcfgx** ficheiro supor como referenciado na **variável public_config** no script powerShell acima. Para mais informações, consulte o esquema de configuração de [extensão da extensão do Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
