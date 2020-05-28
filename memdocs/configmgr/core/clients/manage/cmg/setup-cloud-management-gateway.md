---
title: Configurar o gateway de gestão na cloud
titleSuffix: Configuration Manager
description: Utilize este processo passo a passo para a criação de um gateway de gestão de nuvens (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 8c585473ec80ad4c6dfe49d22e527e99175bfbb4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877421"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar gateway de gestão de nuvem para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este processo inclui os passos necessários para a criação de um gateway de gestão de nuvem (CMG).

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="before-you-begin"></a>Antes de começar

Comece por ler o artigo Plano para gateway de gestão de [nuvens](plan-cloud-management-gateway.md). Use este artigo para determinar o seu design CMG.

Utilize a seguinte lista de verificação para se certificar de que dispõe das informações e pré-requisitos necessários para criar uma CMG:  

- O ambiente Azure para usar. Por exemplo, a Nuvem Pública Azure ou a Nuvem governamental azure dos EUA.  

- Precisa de um ou mais certificados para a CMG, dependendo do seu design. Para mais informações, consulte Certificados para gateway de [gestão de nuvem](certificates-for-cloud-management-gateway.md).  

- Precisa dos seguintes requisitos para uma implantação do Gestor de [Recursos Azure](plan-cloud-management-gateway.md#azure-resource-manager) da CMG:  

    - Integração com [AD Azure](../../../servers/deploy/configure/azure-services-wizard.md) para Gestão de **Nuvem.** A descoberta do utilizador da AD Azure não é necessária.  

    - O **Microsoft.ClassicCompute**  &  **Microsoft.Os** fornecedores de recursos de armazenamento devem ser registados dentro da subscrição Azure. Para mais informações, consulte [o Gestor de Recursos Azure.](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services)

    - Um administrador de subscrição precisa de assinar.  

- Um nome globalmente único para o serviço. Este nome é do certificado de autenticação do [servidor CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Se permitir a CMG como ponto de distribuição na nuvem, o mesmo nome de serviço CMG globalmente único escolhido também precisa estar disponível como um nome de conta de armazenamento globalmente único. Este nome é do certificado de autenticação do [servidor CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- A região de Azure para esta implantação cmg.  

- Quantas instâncias vm precisa para escala e redundância.  

- Se ainda precisar de utilizar a implementação de serviço clássico do Azure na versão 1810 do Gestor de Configuração, precisa dos seguintes requisitos:  

    > [!Important]  
    > A partir da versão 1810, as implementações clássicas de serviço sintetizadas em Azure são depreciadas no Gestor de Configuração. Utilize as implementações do Gestor de Recursos Azure para o gateway de gestão de nuvem. Para mais informações, consulte [Plano para CMG](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do gateway de gestão de nuvem.<!-- 3605704 -->

    - ID de subscrição azure  

    - Certificado de gestão Azure  


## <a name="set-up-a-cmg"></a>Criar um CMG

Faça este procedimento no site de alto nível. Esse site ou é um local primário autónomo, ou o site da administração central.

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud,** e selecione **Cloud Management Gateway**.  

2. Selecione Criar Gateway de **Gestão** de Nuvem na fita.  

3. Na página geral do assistente, selecione **Iniciar sessão**. Autenticar com uma conta de administrador de subscrição Azure. O assistente povoa automaticamente os restantes campos a partir da informação armazenada durante o pré-requisito de integração da AD Azure. Se possuir várias subscrições, selecione o ID de **subscrição** da subscrição desejada para utilizar.

    > [!Note]  
    > A partir da versão 1810, as implementações clássicas de serviço saem em Azure foram depreciadas no Gestor de Configuração. Na versão 1902 e anterior, selecione a implementação do Gestor de **Recursos Azure** como método de implementação cmg.
    >
    > Se precisar de utilizar uma implementação clássica do serviço, selecione essa opção nesta página. Introduza primeiro o seu ID de **Subscrição**Azure . Em seguida, selecione **Browse**, e escolha o . Ficheiro PFX para o certificado de gestão Azure.

4. Especifique o **ambiente Azure** para este CMG. As opções na lista de abandono podem variar consoante o método de implantação.  

5. Selecione **Seguinte**. Espere enquanto o site testa a ligação a Azure.  

6. Na página Definições do assistente, primeiro **selecione 'Navegar'** e escolher o . Ficheiro PFX para o certificado de autenticação do servidor CMG. O nome deste certificado preenche os campos de **nome** **fQDN** e serviço exigidos.  

   > [!NOTE]  
   > O certificado de autenticação do servidor CMG suporta wildcards. Se utilizar um certificado wildcard, substitua o asterisco `*` ( ) no campo **FQDN** de serviço com o nome de anfitrião desejado para o CMG.<!--491233-->  

7. Selecione a lista de abandono da **Região** para escolher a região azure para este CMG.  

8. Selecione uma opção **Grupo de Recursos.**
   1. Se escolher **o Uso existente,** então selecione um grupo de recursos existente na lista de drop-down. O grupo de recursos selecionados já deve existir na região selecionada no passo 7. Se selecionar um grupo de recursos existente e estiver numa região diferente da região previamente selecionada, a CMG não fornecerá.
   2. Se escolher **Criar novo,** introduza o novo nome do grupo de recursos.

9. No campo **VM Instance,** insira o número de VMs para este serviço. O padrão é um, mas pode escalar até 16 VMs por CMG.  

10. Selecione **Certificados** para adicionar certificados de raiz fidedignos do cliente. Adicione todos os certificados na cadeia de confiança.  

    > [!Note]  
    > A partir da versão 1806, quando cria um CMG, já não é necessário fornecer um certificado de raiz fidedigno na página Definições. Este certificado não é necessário quando se utiliza o Azure Ative Directory (Azure AD) para autenticação do cliente, mas costumava ser exigido no assistente. Se estiver a utilizar certificados de autenticação de clientes PKI, então ainda deve adicionar um certificado de raiz fidedigno à CMG.<!--SCCMDocs-pr issue #2872-->  
    >
    > Na versão 1902 e anterior, só pode adicionar dois CAs de raiz de confiança e quatro CAs intermédios (subordinados).<!-- SCCMDocs-pr#4022 -->

11. Por predefinição, o assistente permite a opção de verificar a **revogação do Certificado**de Cliente . Uma lista de revogação de certificados (CRL) deve ser publicamente publicada para que esta verificação funcione. Para mais informações, consulte [Publicar a lista de revogação do certificado](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. A partir da versão 1906, pode **impor TLS 1.2**. Esta definição aplica-se apenas ao vm de serviço de nuvem Azure. Não se aplica a servidores ou clientes do Diretor de Configuração no local. Para obter mais informações sobre TLS 1.2, consulte [Como ativar o TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. A partir da versão 1806, por padrão, o assistente permite a seguinte opção: Permitir que a CMG funcione como um ponto de distribuição na **nuvem e sirva conteúdo a partir do armazenamento Azure**. Agora, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure.  

14. Selecione **Seguinte**.  

15. Para monitorizar o tráfego cmg com um limiar de 14 dias, escolha a caixa de verificação para ligar o alerta de limiar. Em seguida, especifique o limiar e a percentagem para elevar os diferentes níveis de alerta. Escolha **o próximo** quando terminar.  

16. Reveja as definições e escolha **A Seguir**. O Gestor de Configuração começa a configurar o serviço. Depois de fechar o assistente, levará entre 5 a 15 minutos para fornecer o serviço completamente em Azure. Verifique a coluna **'Estado'** para determinar quando o serviço está pronto.  

    > [!Note]  
    > Para resolver as implementações cmg, utilize **CloudMgr.log** e **CMGSetup.log**. Para mais informações, consulte [ficheiros De registo](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configure o site principal para autenticação de certificado de cliente

Se estiver a utilizar certificados de [autenticação de clientes](certificates-for-cloud-management-gateway.md#bkmk_clientauth) para os clientes autenticarem com a CMG, siga este procedimento para configurar cada site primário.  

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione **Sites**.  

2. Selecione o site principal para o qual os seus clientes baseados na Internet são atribuídos, e escolha **Propriedades**.  

3. Mude para o separador **de comunicação** de computador cliente da folha de propriedade do site principal, verifique use o certificado de **cliente PKI (autenticação do cliente) quando disponível**.  

    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

4. Se não publicar um CRL, desmarque a opção para clientes, verifique a lista de **revogação do certificado (CRL) para os sistemas do site**.  


## <a name="add-the-cmg-connection-point"></a>Adicione o ponto de ligação CMG

O ponto de ligação CMG é a função do sistema de site para comunicar com a CMG. Para adicionar o ponto de ligação CMG, siga as instruções gerais para [instalar as funções](../../../servers/deploy/configure/install-site-system-roles.md)do sistema do local . Na página de seleção de funções do sistema do Assistente de Funções do Site add, selecione **Cloud management gateway line point**. Em seguida, selecione o nome de gateway de **gestão cloud** ao qual este servidor se liga. O assistente mostra a região para o CMG selecionado.

> [!Important]
> O ponto de ligação CMG deve ter um certificado de [autenticação do cliente](certificates-for-cloud-management-gateway.md#bkmk_clientauth) em alguns cenários.

Para resolver problemas a saúde do serviço CMG, utilize **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Para mais informações, consulte [ficheiros De registo](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configure funções viradas para o cliente para o tráfego cmg

Configure os sistemas de pontos de gestão e de atualização de software para aceitar o tráfego CMG. Faça este procedimento no site principal, para todos os pontos de gestão e pontos de atualização de software que reparam os clientes baseados na Internet.  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione o nó de Funções de **Servidores e Derôs.** No separador Home da fita, no grupo 'Ver', selecione **Servidores com Função**. Em seguida, selecione ponto de **gestão** da lista.  

2. Selecione o servidor do sistema de site que pretende configurar para o tráfego CMG. Selecione a função de **ponto de gestão** no painel de detalhes e, em seguida, selecione **Propriedades** na fita.  

3. Na folha de propriedades do ponto de gestão no âmbito das Ligações do Cliente, verifique a caixa ao lado do permitir o tráfego de gateway de gestão de nuvem do Gestor de **Configuração.**

    Dependendo da versão CMG de design e Configuração Manager, poderá ser necessário ativar a opção **HTTPS.** Para mais informações, consulte O ponto de [gestão enable para HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Selecione **OK** para fechar a janela de propriedades do ponto de gestão.  

Repita estes passos para pontos de gestão adicionais, conforme necessário, e para quaisquer pontos de atualização de software.


## <a name="configure-boundary-groups"></a>Configure grupos de fronteira

<!--3640932-->
A partir da versão 1902, pode associar um CMG a um grupo de limites. Esta configuração permite que os clientes faltem ou recuem para a CMG para comunicação do cliente de acordo com as relações de grupo de fronteira.

Para obter mais informações sobre grupos de fronteira, consulte [configure grupos de fronteira](../../../servers/deploy/configure/boundary-groups.md).

Quando [criar ou configurar um grupo de limites,](../../../servers/deploy/configure/boundary-group-procedures.md)no separador **Referências,** adicione um gateway de gestão de nuvem. Esta ação associa a CMG a este grupo de fronteiras.


## <a name="configure-clients-for-cmg"></a>Configure clientes para CMG

Uma vez que as funções cmg e do sistema de site estão em execução, os clientes obtêm a localização do serviço CMG automaticamente no próximo pedido de localização. Os clientes devem estar na intranet para receber a localização do serviço CMG, a menos que [instale e atribua clientes do Windows 10 usando a AD Azure para autenticação.](../../deploy/deploy-clients-cmg-azure.md) O ciclo de votação para pedidos de localização é a cada 24 horas. Se não quiser esperar pelo pedido de localização normalmente programado, pode forçar o pedido reiniciando o serviço de hospedamento de agente SMS (ccmexec.exe) no computador.  

> [!Note]
> Por predefinição, todos os clientes recebem a política cmg. Controle este comportamento com a configuração do cliente, Ative os clientes a utilizar um gateway de gestão de [nuvem.](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)

O cliente do Gestor de Configuração determina automaticamente se está na intranet ou na internet. Se o cliente puder contactar um controlador de domínio ou um ponto de gestão no local, define o seu tipo de ligação à **intranet atualmente**. Caso contrário, muda para **a Internet atualmente,** e utiliza a localização do serviço CMG para comunicar com o site.

>[!NOTE]
> Pode forçar o cliente a usar sempre o CMG, independentemente de estar na intranet ou na internet. Esta configuração é útil para fins de teste, ou para clientes que pretende forçar a usar sempre o CMG. Desinserie a seguinte chave de registo no cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Também pode especificar esta definição durante a instalação do cliente utilizando a propriedade [CCMALWAYSINF.](../../deploy/about-client-installation-properties.md#ccmalwaysinf)
>
> Esta definição aplicar-se-á sempre, mesmo que o cliente vagueie por um local onde as configurações de grupo sem limites alavancariam os recursos locais.


Para verificar se os clientes têm a política de especificação do CMG, abra um pedido de comando Windows PowerShell como administrador no computador cliente e execute o seguinte comando:`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Este comando exibe quaisquer pontos de gestão baseados na Internet que o cliente conheça. Embora o CMG não seja tecnicamente um ponto de gestão baseado na Internet, os clientes vêem-no como um só.

> [!Note]  
> Para resolver problemas o tráfego de clientes da CMG, utilize **CMGHttpHandler.log**, **CMGService.log**e **SMS_Cloud_ProxyConnector.log**. Para mais informações, consulte [ficheiros De registo](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

### <a name="install-off-premises-clients-using-a-cmg"></a>Instale clientes fora do local usando um CMG

Para instalar o agente cliente em sistemas não atualmente ligados à sua intranet, uma das seguintes condições deve ser verdadeira. Em todos os casos, é necessária uma conta de administrador local sobre os sistemas-alvo.

1. O site do Gestor de Configuração está devidamente configurado para utilizar certificados PKI para autenticação do cliente. Além disso, os sistemas de clientes têm cada um um certificado de autenticação de cliente válido, único e de confiança anteriormente emitido para os mesmos.

2. Os sistemas são unidos por domínio Azure AD ou híbridos unidos por domínio Azure.

3. O site está a executar a versão de 'Gestor de Configuração' em 2002 ou mais tarde.

Para as opções 1 e 2, utilize o parâmetro **/mp** para especificar o URL da CMG ao ligar **para ccmsetup.exe**. Para mais informações, consulte sobre os parâmetros e propriedades de [instalação do cliente.](../../deploy/about-client-installation-properties.md#mp)

Para a opção 3, a partir da versão De Configuração 2002, pode instalar o agente cliente em sistemas não ligados à sua intranet utilizando um símbolo de registo a granel. Para obter mais informações sobre este método, consulte [Criar um sinal de registo](../../deploy/deploy-clients-cmg-token.md#create-a-bulk-registration-token)a granel .

### <a name="configure-off-premises-clients-for-cmg"></a>Configure clientes fora do local para a CMG

Pode ligar os sistemas a um CMG recentemente configurado onde as seguintes condições são verdadeiras:  

- Os sistemas já têm o agente cliente do Gestor de Configuração instalado.

- Os sistemas não estão ligados e não podem ser ligados à sua intranet.

- Os sistemas satisfazem uma das seguintes condições:

  - Cada um tem um certificado de autenticação de cliente válido, único e de confiança anteriormente emitido.

  - Azure AD-joined domínio

  - Híbrido Azure AD-joined domínio.

- Não deseja ou não pode reinstalar completamente o agente cliente existente.

- Tem um método para alterar o valor do registo da máquina e reiniciar o serviço de hospedar o **Agente SMS** utilizando uma conta de administrador local.

Para forçar a ligação nestes sistemas, crie o valor de registo **CMGFQDNs** (do tipo REG_SZ) em **HKLM\Software\Microsoft\CCM**. Defino este valor para o URL do CMG (por exemplo, `https://contoso-cmg.contoso.com` ). Uma vez definido, reinicie o serviço de hospedagem do **Agente SMS** no sistema de cliente.

Se o cliente do Gestor de Configuração não tiver um atual CMG ou um ponto de gestão virado para a Internet definido no registo, verifica automaticamente o valor do registo **CMGFQDNs.** Esta verificação ocorre a cada 25 horas, quando o serviço de hospedeiro do **agente SMS** começa, ou quando deteta uma mudança de rede. Quando o cliente se conecta ao site e aprende de um CMG, atualiza automaticamente este valor.

## <a name="modify-a-cmg"></a>Modificar um CMG

Depois de criar um CMG, pode modificar algumas das suas definições. Selecione o CMG na consola 'Gestor de **Configuração'** e selecione Propriedades . Configure as definições nos seguintes separadores:  

#### <a name="general"></a>Geral

- Certificado de **gestão Azure:** alterar o certificado de gestão Azure para a CMG. Esta opção é útil ao atualizar o certificado antes de expirar.  

#### <a name="settings"></a>Definições

- **Ficheiro**de certificado : alterar o certificado de autenticação do servidor para o CMG. Esta opção é útil ao atualizar o certificado antes de expirar.  

- **VM Instance**: alterar o número de máquinas virtuais que o serviço utiliza no Azure. Esta definição permite-lhe escalar dinamicamente o serviço para cima ou para baixo com base em utilizações ou considerações de custos.  

- **Certificados:** adicionar ou remover certificados de raiz fidedignos ou ca intermédios. Esta opção é útil na adição de novos A Ou na reforma de certificados caducados.  

- Verifique a **Revogação**do Certificado de Cliente : se não tiver ativado originalmente esta definição ao criar o CMG, pode capacitá-la depois de publicar o CRL. Para mais informações, consulte [Publicar a lista de revogação do certificado](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Permitir que a CMG funcione como um ponto**de distribuição na nuvem e sirva conteúdo a partir do armazenamento Do Azure : A partir da versão 1806, esta nova opção é ativada por padrão. Agora, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados e o custo exigidos dos VMs Azure.<!--1358651-->  

#### <a name="alerts"></a>Alertas

Reconfigure os alertas a qualquer momento depois de criar o CMG.


### <a name="redeploy-the-service"></a>Reutilizar o serviço

Alterações mais significativas, como as seguintes configurações, exigem a reafectação do serviço:

- Método clássico de implantação para Gestor de Recursos Azure
- Subscrição
- Nome do Serviço
- Privado para público PKI
- Região

Mantenha sempre pelo menos um CMG ativo para que os clientes baseados na Internet recebam uma política atualizada. os clientes baseados na Internet não podem comunicar com um CMG removido. Os clientes não sabem de um novo até voltarem à intranet. Ao criar uma segunda instância CMG para eliminar a primeira, também crie outro ponto de ligação CMG.

Os clientes atualizam a política por defeito a cada 24 horas, por isso aguarde pelo menos um dia depois de criar um novo CMG antes de apagar o antigo. Se os clientes estiverem desligados ou sem ligação à Internet, poderá ter de esperar mais tempo.

Se tiver um CMG existente no método de implantação clássico, tem de implementar um novo CMG para utilizar o método de implementação do Gestor de Recursos Azure.<!--509753--> Existem duas opções:  

- Se quiser reutilizar o mesmo nome de serviço:  

    1. Primeiro apague o CLÁSSICO CMG, tendo em conta a orientação para ter sempre pelo menos um CMG ativo para clientes baseados na Internet.  

    2. Crie um novo CMG utilizando uma implementação do Gestor de Recursos. Reutilizar o mesmo certificado de autenticação do servidor.  

    3. Reconfigurar o ponto de ligação CMG para utilizar a nova instância CMG.  

- Se quiser usar um novo nome de serviço:  

    1. Crie um novo CMG utilizando uma implementação do Gestor de Recursos. Utilize um novo certificado de autenticação do servidor.  

    2. Crie um novo ponto de ligação CMG e ligue-se ao novo CMG.  

    3. Aguarde pelo menos um dia para que os clientes baseados na Internet recebam política sobre o novo CMG.  

    4. Apague o clássico CMG.  

> [!Tip]  
> Para determinar o atual modelo de implantação de um CMG:<!--SCCMDocs issue #611-->  
>
> 1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud**e selecione o nó Gateway de Gestão de **Nuvem.**  
> 2. Selecione a instância CMG.  
> 3. No painel Detalhes na parte inferior da janela, procure o atributo do Modelo de **Implantação.** Para uma implementação do Gestor de Recursos, este atributo é o Gestor de **Recursos Azure.** O modelo de implantação do legado com o certificado de gestão Azure apresenta-se como **Gestor de Serviços Azure.**
>
> Também pode adicionar o atributo do Modelo de **Implantação** como uma coluna à vista da lista.  

### <a name="modifications-in-the-azure-portal"></a>Modificações no portal Azure

Apenas modifique o CMG da consola 'Gestor de Configuração'. Não é suportado fazer modificações no serviço ou em VMs subjacentes diretamente no Azure. Quaisquer alterações podem perder-se sem aviso prévio. Como em qualquer PaaS, o serviço pode reconstruir os VMs a qualquer momento. Estas reconstruções podem acontecer para manutenção de hardware backend, ou para aplicar atualizações para o VM OS.

### <a name="delete-the-service"></a>Eliminar o serviço

Se precisar de eliminar o CMG, faça-o também a partir da consola 'Gestor de Configuração'. A remoção manual de quaisquer componentes em Azure faz com que o sistema seja inconsistente. Este estado deixa informações órfãs, e comportamentos inesperados podem ocorrer.


## <a name="next-steps"></a>Próximos passos

- [Monitorize os clientes para gateway de gestão de nuvem](monitor-clients-cloud-management-gateway.md)
- [Perguntas frequentes sobre o gateway de gestão de nuvens](cloud-management-gateway-faq.md)
