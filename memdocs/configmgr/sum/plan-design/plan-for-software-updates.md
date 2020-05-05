---
title: Planear atualizações de software
titleSuffix: Configuration Manager
description: Um plano para a infraestrutura de pontos de atualização de software é essencial antes de utilizar atualizações de software num ambiente de produção do Gestor de Configuração.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: dca6f3e4bf67ac4c947f785016d781e538ee0a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724021"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Plano para atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de utilizar atualizações de software num ambiente de produção do Gestor de Configuração, é importante que passe pelo processo de planeamento. Ter um bom plano para a infraestrutura de pontos de atualização de software é a chave para uma implementação de atualizações de software bem-sucedida. Para obter informações sobre o planeamento de capacidade para atualizações de software, consulte [tamanho e números de escala](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a>Determine a infraestrutura de pontos de atualização de software  

Esta secção inclui os seguintes subtópicos:    
- [Lista de pontos de atualização de software](#BKMK_SUPList)
- [Mudança do ponto de atualização de software](#BKMK_SUPSwitching)
- [Mude manualmente os clientes para um novo ponto de atualização de software](#BKMK_ManuallySwitchSUPs)
- [Pontos de atualização de software numa floresta não fidedigna](#BKMK_SUP_CrossForest)
- [Utilize um servidor WSUS existente como fonte de sincronização no site de alto nível](#BKMK_WSUSSyncSource)
- [Ponto de atualização de software num site secundário](#BKMK_SUPSecSite)  
- [Plano para clientes baseados na Internet](#bkmk_internet-clients)  
- [Planeie conteúdo de atualização de software](#bkmk_content)  
- [Plano para atualizações de terceiros](#bkmk_thirdparty)  


O site da administração central e todos os sites primários para crianças devem ter um ponto de atualização de software. Enquanto planeia a infraestrutura de pontos de atualização de software, determine as seguintes dependências:
- Onde instalar o ponto de atualização de software para o site  
- Quais os sites que requerem um ponto de atualização de software que aceita a comunicação de clientes baseados na Internet
- Se precisa de um ponto de atualização de software em sites secundários  

> [!IMPORTANT]  
>  Para obter mais informações sobre as dependências internas e externas que são necessárias para atualizações de software, consulte [pré-requisitos para atualizações](prerequisites-for-software-updates.md)de software .  

Adicione vários pontos de atualização de software num site primário do Gestor de Configuração para fornecer tolerância a falhas. O design failover do ponto de atualização de software é diferente do modelo de randomização pura que é usado no design para pontos de gestão. Ao contrário do design de pontos de gestão, existem custos de desempenho de clientes e rede no design de ponto de atualização de software quando os clientes mudam para um novo ponto de atualização de software. Quando o cliente muda para um novo servidor WSUS para analisar a existência de atualizações de software, o resultado é um aumento do tamanho do catálogo e exigências associadas do lado do cliente e a nível do desempenho da rede. Portanto, o cliente preserva a afinidade com o último ponto de atualização de software a partir do qual digitalizou com sucesso.  

O primeiro ponto de atualização de software que instalar num site principal é a origem de sincronização para todos os pontos de atualização de software adicionais que adicionar no site primário. Depois de adicionar pontos de atualização de software e iniciar a sincronização, veja o estado dos pontos de atualização do software e a fonte de sincronização do nó de Sincronização do Ponto de Sincronização do Ponto de **Atualização** de Software no espaço de trabalho de **Monitorização.**  

Quando houver uma falha do ponto de atualização do software configurado como a fonte de sincronização para o site, remova manualmente a função falhada. Em seguida, selecione um novo ponto de atualização de software para usar como fonte de sincronização. Para mais informações, consulte [Remova uma função](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role)do sistema do site .  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Lista de pontos de atualização de software  

O Gestor de Configuração fornece ao cliente uma lista de pontos de atualização de software nos seguintes cenários:  

- Um novo cliente recebe a política para ativar atualizações de software  

- Um cliente não pode contactar o seu ponto de atualização de software atribuído e precisa de mudar para outro  

O cliente seleciona aleatoriamente um ponto de atualização de software da lista. Dá prioridade aos pontos de atualização de software na mesma floresta. O Gestor de Configuração fornece aos clientes uma lista diferente dependendo do tipo de cliente:  

-   **Clientes baseados em intranet**: Receba uma lista de pontos de atualização de software que pode configurar para permitir ligações apenas a partir da intranet, ou uma lista de pontos de atualização de software que permitem ligações à Internet e à intranet do cliente.  

-   **Clientes baseados na Internet**: Receba uma lista de pontos de atualização de software que configura para permitir ligações apenas a partir da internet, ou uma lista de pontos de atualização de software que permitem ligações à Internet e à intranet.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a>Comutação de ponto de atualização de software  

> [!NOTE]  
> Os clientes usam grupos de fronteira para encontrar um novo ponto de atualização de software. Se o seu atual ponto de atualização de software já não for acessível, também usam grupos de fronteira para recuar e encontrar um novo. Adicione pontos de atualização de software individuais a diferentes grupos de limites para controlar quais servidores que um cliente pode encontrar. Para mais informações, consulte os pontos de [atualização do Software](../../core/servers/deploy/configure/boundary-groups.md#software-update-points).  

Se tiver vários pontos de atualização de software num site, e um falhar ou ficar indisponível, os clientes ligar-se-ão a um ponto de atualização de software diferente. Com este novo servidor, os clientes continuam a procurar as mais recentes atualizações de software. Quando um cliente é atribuído pela primeira vez a um ponto de atualização de software, permanece atribuído a esse ponto de atualização de software, a menos que não apareça.  

A análise da existência de atualizações de software pode falhar com uma série de diferentes códigos de erro de repetições e não repetições. Quando a análise falha com um código de erro de repetição, o cliente inicia um processo de repetição para procurar as atualizações de software no ponto de atualização de software. As condições de alto nível que resultam num código de erro de repetição são normalmente causadas porque o servidor WSUS está indisponível ou porque está temporariamente sobrecarregado. Quando o cliente não procura atualizações de software, utiliza o seguinte processo:  

1.  O cliente procura atualizações de software:  
    - Na hora marcada
    - Quando é executado manualmente a partir do painel de controlo do cliente
    - Quando é executado manualmente a partir da consola Do Gestor de Configuração através de uma ação de notificação do cliente
    - Quando é executado a partir de um método SDK de Gestor de Configuração  

2.  Se a tomografia falhar, o cliente espera 30 minutos para voltar a tentar a tomografia. Usa o mesmo ponto de atualização de software.  

3.  O cliente tenta um mínimo de quatro vezes a cada 30 minutos. Após a quarta falha, e depois de esperar mais dois minutos, o cliente passa para o próximo ponto de atualização de software na sua lista.  

4.  O cliente repete este processo com o novo ponto de atualização de software. Após uma varredura bem sucedida, o cliente continua a ligar-se ao novo ponto de atualização de software.  

A lista seguinte fornece informações adicionais a considerar para a retry de pontode atualização de software e cenários de comutação:  

-   Se um cliente estiver desligado da intranet e não conseguir obter atualizações de software, não muda para outro ponto de atualização de software. Esta falha é esperada, porque o cliente não consegue chegar à rede interna ou a um ponto de atualização de software que permite ligações a partir da intranet. O cliente do Gestor de Configuração determina a disponibilidade do ponto de atualização do software intranet.  

-   Se estiver a gerir clientes na internet e tiver configurado vários pontos de atualização de software para aceitar a comunicação dos clientes na internet, o processo de comutação segue o processo de retry padrão previamente descrito.  

-   Se o processo de digitalização começar, mas o cliente é desligado antes do exame ser concluído, não é considerado uma falha de digitalização e não conta como uma das quatro tentativas.  

Quando o Gestor de Configuração recebe qualquer um dos seguintes códigos de erro do Windows Update Agent, o cliente retenta a ligação:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Para procurar o significado de um código de erro, converter o código de erro decimal para hexadecimal, e depois procurar o valor hexadecimal num site como o [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). Por exemplo, o código de erro decimal 2149842970 é hexadecimal 8024001A , o que significa WU_E_POLICY_NOT_SET uma política de valor não foi definida.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a>Mude manualmente os clientes para um novo ponto de atualização de software

Altere os clientes do Gestor de Configuração para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Esta alteração só acontece quando um cliente recebe vários pontos de atualização de software a partir de um ponto de gestão.

> [!IMPORTANT]    
> Quando muda de dispositivopara utilizar um novo servidor, os dispositivos utilizam o backback para encontrar o novo servidor. Os clientes mudam para o novo ponto de atualização de software durante o seu próximo ciclo de atualizações de software.<!-- SCCMDocs#1537 -->
>
> Antes de iniciar esta alteração, reveja as configurações do seu grupo de limites para se certificar de que os pontos de atualização do software estão nos grupos de limites corretos. Para mais informações, consulte os pontos de [atualização do Software](../../core/servers/deploy/configure/boundary-groups.md#software-update-points).  
>
> Mudar para um novo ponto de atualização de software gera tráfego adicional de rede. A quantidade de tráfego depende das definições de configuração do WSUS, por exemplo, das classificações e produtos sincronizados ou da utilização de uma base de dados WSUS partilhada. Se planeia mudar vários dispositivos, considere fazê-lo durante as janelas de manutenção. Este timing reduz o impacto na sua rede quando os clientes digitalizam com o novo ponto de atualização de software.  

#### <a name="process-to-switch-software-update-points"></a>Processo para mudar pontos de atualização de software  
Inicie esta alteração numa coleção de dispositivos. Uma vez acionados, os clientes procuram outro ponto de atualização de software na próxima digitalização.  

1.  Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de Recolhas de **Dispositivos.**  

2.  Selecione a coleção de alvos. No separador **Home** da fita, no grupo **Coleção,** clique na **Notificação**do Cliente e clique em Switch para o próximo Ponto de **Atualização**de Software .  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Pontos de atualização de software numa floresta não fidedigna  

Crie um ou mais pontos de atualização de software num site para apoiar os clientes numa floresta não confiável. Para adicionar um ponto de atualização de software em outra floresta, primeiro instale e configure um servidor WSUS nessa floresta. Em seguida, inicie o assistente para adicionar um servidor de site do Gestor de Configuração com a função do sistema de ponto de atualização do software. No assistente, configure as seguintes definições para ligar com êxito ao WSUS na floresta não fidedigna:  

-   Especifique uma conta de **instalação** do sistema do site que possa aceder ao servidor WSUS na floresta não confiável.  

-   Especifique uma **conta wSUS Server Connection** para ligar ao servidor WSUS.  

Por exemplo, dispõe de um site principal na floresta A com pontos de atualização de software (SUP01 e SUP02). Para o mesmo site primário, você também tem dois pontos de atualização de software (SUP03 e SUP04) na floresta B. Ao mudar para o próximo ponto de atualização de software, os clientes priorizam os servidores da mesma floresta.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a>Utilize um servidor WSUS existente como fonte de sincronização no site de alto nível  

Normalmente, o site de nível superior na sua hierarquia está configurado para sincronizar metadados de atualizações de software com o Microsoft Update. Quando a sua política de segurança organizacional não permite que o site de alto nível aceda à internet, configure a fonte de sincronização para o site de alto nível usar um servidor WSUS existente. Este servidor WSUS não está na hierarquia do Gestor de Configuração. Por exemplo, tem um servidor WSUS numa rede ligada à Internet (DMZ), mas o seu site de alto nível está numa rede interna sem acesso à Internet. Configure o servidor WSUS no DMZ como a sua fonte de sincronização para atualizações de software metadados. Configure o servidor WSUS no DMZ para sincronizar atualizações de software com os mesmos critérios que necessita no Configuror Manager. Caso contrário, o site de nível superior poderá não sincronizar as atualizações de software que espera. Quando instalar o ponto de atualização do software, configure uma conta de ligação ao servidor WSUS. Esta conta precisa de acesso ao servidor WSUS no DMZ. Confirme também que a firewall permite o tráfego para as portas apropriadas. Para obter mais informações, consulte as [portas utilizadas pela atualização do software apontar para a fonte de sincronização](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a>Ponto de atualização de software em um site secundário  

O ponto de atualização de software é opcional num site secundário. Instale apenas um ponto de atualização de software num site secundário. Quando um ponto de atualização de software não é instalado no site secundário, os dispositivos dentro dos limites de um site secundário usam um ponto de atualização de software no seu site primário designado. Normalmente instala-se um ponto de atualização de software num site secundário quando há uma largura de banda de rede limitada entre os dispositivos no site secundário e os pontos de atualização de software no site principal dos pais. Também pode utilizar esta configuração quando o ponto de atualização do software no site primário se aproximar do limite de capacidade. Depois de instalar e configurar com sucesso um ponto de atualização de software no site secundário, uma política a nível do site é atualizada para os clientes, e eles começam a usar o novo ponto de atualização de software.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a>Plano para clientes baseados na Internet

Quando necessitar de gerir dispositivos que circulam fora da sua rede para a internet, desenvolva um plano para gerir atualizações de software nestes dispositivos. O Gestor de Configuração suporta várias tecnologias para este cenário. Utilize uma ou uma combinação necessária para satisfazer os requisitos da sua organização.

#### <a name="cloud-management-gateway"></a>Gateway de gestão da cloud
Crie um portal de gestão de nuvem no Microsoft Azure e ative pelo menos um ponto de atualização de software no local para permitir o tráfego de clientes baseados na Internet. À medida que os clientes circulam pela internet, continuam a digitalizar os pontos de atualização do software. Todos os clientes baseados na Internet obtêm sempre conteúdo do serviço de cloud microsoft Update. 

Para mais informações, consulte [Plan para o portal de gestão de nuvens](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).  

#### <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet
Coloque um ponto de atualização de software numa rede virada para a Internet e permita-lhe o tráfego de clientes baseados na Internet. À medida que os clientes vagueiam pela internet, mudam para este ponto de atualização de software para digitalização. Todos os clientes baseados na Internet obtêm sempre conteúdo do serviço de cloud microsoft Update.

Para obter mais informações sobre as vantagens e desvantagens da gestão de clientes baseadas na Internet, consulte [Gerir os clientes na internet.](../../core/clients/manage/manage-clients-internet.md)

#### <a name="windows-update-for-business"></a>Windows Update para Empresas
O Windows Update for Business permite manter os dispositivos Windows 10 sempre atualizados com as mais recentes atualizações de qualidade e funcionalidade. Estes dispositivos ligam-se diretamente ao serviço de cloud Windows Update. O Gestor de Configuração pode diferenciar os computadores do Windows 10 que utilizam wufb e WSUS para obter atualizações de software.

Para mais informações, consulte [Integração com Atualização do Windows para Negócios](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a>Planeie conteúdo de atualização de software

Os clientes precisam de descarregar os ficheiros de conteúdo para atualizações de software para os instalar. O Gestor de Configuração fornece várias tecnologias para apoiar a gestão e entrega deste conteúdo. Ou configurar implementações de atualizações de software para permitir ou exigir que os clientes obtenha conteúdo diretamente do serviço de cloud microsoft Update.

#### <a name="download-and-distribute-content"></a>Descarregue e distribua conteúdo 
Por padrão, o processo de gestão de atualizações de software no Gestor de Configuração utiliza as funcionalidades de gestão de conteúdos incorporados. Estas funcionalidades incluem a biblioteca centralizada de conteúdos de loja de uma instância e o design distribuído da função do sistema do site de pontos de distribuição. Utiliza estas funcionalidades quando descarrega e distribui pacotes de implementação de atualizações de software. 

Para mais informações, consulte [as atualizações](../deploy-use/download-software-updates.md)do software de download .

#### <a name="manage-express-installation-files-for-windows-10"></a>Gerir ficheiros de instalação expresso para windows 10
O Gestor de Configuração suporta a utilização de ficheiros de instalação expresso para atualizações do Windows 10. Ficheiros de atualização expresso e tecnologias de suporte como a Otimização de Entrega podem ajudar a reduzir o impacto da rede de grandes ficheiros de conteúdo descarregados para os clientes. 

Para mais informações, consulte [otimize a entrega da atualização do Windows 10.](../deploy-use/optimize-windows-10-update-delivery.md)

#### <a name="clients-download-content-from-the-internet"></a>Clientes descarregam conteúdo da internet
Quando implementar atualizações de software para clientes, configure a implementação para os clientes descarregarem conteúdo do serviço cloud microsoft Update. Quando os clientes não conseguem descarregar conteúdo de outra fonte de conteúdo, ainda podem descarregar o conteúdo a partir da internet. 

A partir da versão 1806, não é preciso criar um pacote de implementação ao implementar atualizações de software. Quando seleciona a opção **de pacote de não implementação,** os clientes ainda podem descarregar conteúdo de fontes locais, se disponível, mas normalmente descarregam a partir do serviço Microsoft Update.<!--1357933-->

Os clientes baseados na Internet descarregam sempre conteúdos do serviço cloud microsoft Update. Não distribua pacotes de implementação de atualizações de software para um ponto de distribuição na nuvem. É cobrado pelo armazenamento com o ponto de distribuição na nuvem, mas os clientes não descarregam estes pacotes. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a>Plano para atualizações de terceiros
O Gestor de Configuração integra-se com a WSUS, que suporta de forma nativa as atualizações de software publicadas pela Microsoft. A maioria dos clientes utiliza outras aplicações de terceiros que também precisam de atualizações. Existem várias opções a considerar para manter as candidaturas de terceiros atualizadas.

#### <a name="supersede-applications-to-update"></a>Aplicações de supersede para atualizar
Utilize uma relação de supersedência com a funcionalidade de gestão de aplicações no Gestor de Configuração para atualizar ou substituir as aplicações existentes. Quando substituir uma aplicação, especifique um novo tipo de implementação para substituir o tipo de implementação da aplicação supersed. Também decida se deve atualizar ou desinstalar a aplicação supersed antes da instalação da aplicação de superseding.

Para mais informações, consulte [revise e substitui aplicações.](../../apps/deploy-use/revise-and-supersede-applications.md)

#### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
A partir da versão 1806, utilize o nó de Catálogos de **Atualizações de Software de Terceiros** na consola do Gestor de Configuração para subscrever catálogos de terceiros, publicar as suas atualizações no seu ponto de atualização de software e, em seguida, implementá-los para clientes.<!--1352101-->

Para mais informações, consulte [atualizações de software de terceiros.](../deploy-use/third-party-software-updates.md)

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) é uma ferramenta autónoma que permite a fornecedores de software independentes ou desenvolvedores de aplicações line-of-business gerir atualizações personalizadas. Estas atualizações incluem as que têm dependências, como motoristas e pacotes de atualização.

Para mais informações, consulte [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a>Plano para instalação de ponto de atualização de software  

Esta secção inclui os seguintes subtópicos:  
- [Requisitos para o ponto de atualização de software](#BKMK_SUPSystemRequirements)
- [Plano para instalação wsus](#BKMK_PlanningForWSUS)
- [Configurar firewalls](#BKMK_ConfigureFirewalls)  


Esta secção fornece informações sobre as medidas a tomar para planear e preparar com sucesso a instalação do ponto de atualização de software. Antes de criar uma função de sistema de site para o ponto de atualização de software no Gestor de Configuração, existem vários requisitos a considerar. Os requisitos específicos dependem da sua infraestrutura de Gestor de Configuração. Quando configura o ponto de atualização do software para comunicar utilizando HTTPS, esta secção é especialmente importante para rever. Os servidores ativados por HTTPS requerem passos adicionais para funcionar corretamente.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Requisitos do ponto de atualização de software  

Instale a função de ponto de atualização de software num sistema de site que cumpra os requisitos mínimos para o WSUS e as configurações suportadas para sistemas de site do Gestor de Configuração.  

-   Para obter mais informações sobre os requisitos mínimos para o papel do servidor WSUS no Windows Server, consulte considerações de [Revisão e requisitos do sistema](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Para obter mais informações sobre as configurações suportadas para sistemas de site do Gestor de Configuração, consulte os [pré-requisitos](../../core/plan-design/configs/site-and-site-system-prerequisites.md)do sistema de site e do site.  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Planear a instalação do WSUS  

Instale uma versão suportada do WSUS em todos os servidores do sistema do site que configura para a função de ponto de atualização de software. Quando não instalar o ponto de atualização do software no servidor do site, instale a Consola de Administração WSUS no servidor do site. Este componente permite que o servidor do site se comunique com o WSUS que funciona no ponto de atualização do software.  

Quando utilizar o WSUS no Windows Server 2012 ou mais tarde, configure permissões adicionais para permitir que o componente do Gestor de **Configuração wSUS** no Gestor de Configuração se conectem ao WSUS. Este componente realiza verificações de saúde periódicas. Escolha uma das seguintes opções para configurar a permissão necessária:  

-   Adicionar a conta **SYSTEM** ao grupo **Administradores WSUS**  

-   Adicione a conta **NT AUTHORITY\SYSTEM** como utilizador da base de dados WSUS (SUSDB). Configure um mínimo da base de dados webService.  
  
Para obter mais informações sobre como instalar o WSUS no Windows Server, consulte [Instalar a Função do Servidor WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. Partilhar a mesma base de dados melhora o desempenho quando os clientes mudam para um novo ponto de atualização de software. Para mais informações, consulte [Utilize uma base de dados WSUS partilhada para pontos](software-updates-best-practices.md#bkmk_shared-susdb)de atualização de software .  

#### <a name="configuring-the-wsus-content-directory-path"></a>Configurar o caminho do diretório de conteúdos wSUS

Quando instalar o WSUS, terá de fornecer um caminho de direção de conteúdo. O diretório de conteúdos wSUS é usado principalmente para armazenar os ficheiros Microsoft Software License Terms necessários pelos clientes durante a digitalização. O Diretor de Configuração O diretório de conteúdos wSUS não deve sobrepor-se ao seu diretório de fonte de conteúdo para pacotes de implementação de software do Gestor de Configuração. Sobrepor-se ao diretório de conteúdo wSUS e à fonte do pacote Do Gestor de Configuração resultará na remoção incorreta de ficheiros do diretório de conteúdo wSUS.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a>Configure o WSUS para usar um site personalizado  
Quando instala o WSUS, pode optar por utilizar o Web site predefinido existente do IIS ou criar um Web site personalizado do WSUS. Crie um website personalizado para o WSUS para que o IIS administe os serviços WSUS num site virtual dedicado. Caso contrário, partilha o mesmo website que é utilizado pelos outros sistemas ou aplicações do Site Do Gestor de Configuração. Esta configuração é especialmente necessária quando instala a função de ponto de atualização de software no servidor do site. Quando executa o WSUS no Windows Server 2012 ou mais tarde, o WSUS está configurado por padrão para utilizar a porta 8530 para HTTP e a porta 8531 para HTTPS. Especifique estas portas quando criar o ponto de atualização de software num site.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Utilizar uma infraestrutura do WSUS existente  
Selecione um servidor WSUS que estivesse ativo no seu ambiente antes de instalar o Gestor de Configuração como ponto de atualização de software. Quando o ponto de atualização do software estiver configurado, especifique as definições de sincronização. O Gestor de Configuração conecta-se ao servidor WSUS que funciona no servidor de pontos de atualização de software e configura o WSUS com as mesmas definições. 

Antes de configurar o servidor como um ponto de atualização de software, compare a sua configuração para produtos e classificações com as definições do Gestor de Configuração. Se sincronizar o servidor WSUS existente antes de o configurar como um ponto de atualização de software, e as listas de produtos e classificações forem diferentes, sincroniza todos os metadados de atualizações de software, independentemente das configurações configuradas. Este comportamento resulta em atualizações inesperadas de software na base de dados do site. 

Experimenta o mesmo comportamento quando adiciona produtos ou classificações diretamente na consola da Administração WSUS e, em seguida, inicia imediatamente uma sincronização. Por predefinição, o Gestor de Configuração de cada hora liga-se ao WSUS e repõe quaisquer definições modificadas fora do 'Gestor de Configuração'. As atualizações de software que não satisfazem os produtos e classificações que especifica nas definições de sincronização estão definidas para expirar. Depois são removidos da base de dados do site.  

Quando um servidor WSUS é configurado como um ponto de atualização de software, já não é capaz de usá-lo como um servidor WSUS autónomo. Se precisar de um servidor WSUS autónomo separado que não seja gerido pelo Configurmanager, configure-o num servidor diferente.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Configurar o WSUS como servidor de réplica  
Quando adiciona a função de ponto de atualização de software num servidor de site primário, não pode utilizar um servidor WSUS que esteja configurado como uma réplica. Quando o servidor WSUS é configurado como uma réplica, o Gestor de Configuração falha na configuração do servidor WSUS e a sincronização wSUS falha. O primeiro ponto de atualização de software que instalar num site primário será o ponto de atualização de software predefinido. Os pontos de atualização de software adicionais no site serão configurados como réplicas do ponto de atualização de software predefinido.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Decidir se pretende configurar o WSUS para utilizar SSL  
Utilize o protocolo SSL para ajudar a proteger o ponto de atualização do software. O WSUS utiliza SSL para autenticar computadores cliente e servidores WSUS a jusante para o servidor WSUS. O WSUS também utiliza SSL para encriptar os metadados de atualização de software. Quando optar por proteger o WSUS com SSL, prepare o servidor WSUS antes de instalar o ponto de atualização do software. Para mais informações, consulte o [Configure SSL no artigo do servidor WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) na documentação para o WSUS. 

Quando instalar e configurar o ponto de atualização do software, selecione a opção de **ativar as comunicações SSL para o Servidor WSUS**. Caso contrário, o Gestor de Configuração confunde a WSUS para não utilizar o SSL. Quando ativa o SSL num ponto de atualização de software, também configurar quaisquer pontos de atualização de software em sites infantis para utilizar o SSL.  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a>Configurar firewalls  

O ponto de atualização de software num site de administração central do Gestor de Configuração comunica com a WSUS no ponto de atualização do software. A WSUS comunica com a fonte de sincronização para sincronizar os metadados das atualizações de software. Pontos de atualização de software num site infantil comunicam com o ponto de atualização de software no site principal. Quando há mais de um ponto de atualização de software num site primário, os pontos de atualização de software adicionais comunicam com o ponto de atualização de software padrão. A função padrão é o primeiro ponto de atualização de software que está instalado no site.  

Pode ser necessário configurar a firewall para permitir o tráfego HTTP ou HTTPS que a WSUS utiliza nos seguintes cenários: 
- Entre o ponto de atualização de software e a internet
- Entre um ponto de atualização de software e a sua fonte de sincronização a montante
- Entre pontos adicionais de atualização de software  

A ligação ao Microsoft Update é sempre configurada para utilizar a porta 80 para HTTP e a porta 443 para HTTPS. Utilize uma porta personalizada para a ligação da WSUS no ponto de atualização de software num site infantil para a WSUS no ponto de atualização do software no site principal. Quando a sua política de segurança não permitir a ligação, utilize o método de sincronização de exportação e importação. Para mais informações, consulte a secção [De Sincronização Fonte](#BKMK_SyncSource) deste artigo. Para obter mais informações sobre as portas que a WSUS utiliza, consulte como determinar as definições de [porta utilizadas pela WSUS no 'Gestor](../get-started/install-a-software-update-point.md#wsus-settings)de Configuração'.  


#### <a name="restrict-access-to-specific-domains"></a>Restringir o acesso a domínios específicos  

Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, tem de permitir que o ponto de atualização de software ativo aceda a pontos finais da Internet. Em seguida, wSUS e Atualizações Automáticas podem comunicar com o serviço de cloud Microsoft Update.

Para mais informações, consulte os requisitos de [acesso à Internet.](../../core/plan-design/network/internet-endpoints.md#bkmk_sum)


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planear as definições de sincronização  

Esta secção inclui os seguintes subtópicos:  
- [Fonte de sincronização](#BKMK_SyncSource)
- [Calendário de sincronização](#BKMK_SyncSchedule)
- [Classificações de atualizações](#BKMK_UpdateClassifications)
- [Produtos](#BKMK_UpdateProducts)
- [Regras de substituição](#BKMK_SupersedenceRules)
- [Linguagens](#BKMK_UpdateLanguages)  
- [Tempo máximo de execução](#bkmk_maxruntime)


O software atualiza a sincronização no Configurmanager descarregamentos os metadados de atualizações de software com base em critérios que configura. O site de alto nível da sua hierarquia sincroniza as atualizações de software a partir do Microsoft Update. Tem a opção de configurar o ponto de atualização de software no site de alto nível para sincronizar com um servidor WSUS existente, e não na hierarquia do Gestor de Configuração. Os sites subordinados principais sincronizam os metadados de atualizações de software a partir do ponto de atualização de software no site de administração central. Antes de instalar e configurar um ponto de atualização de software, utilize esta secção para planear as definições de sincronização.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Origem de sincronização  

As definições de fonte de sincronização para o ponto de atualização do software especificam a localização para onde o ponto de atualização de software recupera metadados de software. Também especifica se o processo de sincronização cria eventos de reporte wSUS.  

-   Fonte de **sincronização**: Por padrão, o ponto de atualização do software no site de alto nível configura a fonte de sincronização para o Microsoft Update. Tem a opção de sincronizar o site de nível superior com um servidor WSUS existente. O ponto de atualização do software num site primário infantil configura a fonte de sincronização como o ponto de atualização de software no site da administração central.  

    -  O primeiro ponto de atualização de software que instalar num site primário, que é o ponto de atualização de software predefinido, sincroniza com o site de administração central. Os pontos de atualização de software adicionais no site primário sincronizam-se com o ponto de atualização de software predefinido no site primário.  

    - Quando um ponto de atualização de software estiver desligado do Microsoft Update ou do servidor de atualização a montante, configure a fonte de sincronização para não sincronizar com uma fonte de sincronização configurada. Em vez disso, configure-a para utilizar a função de exportação e importação da ferramenta **WSUSUtil** para sincronizar atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventos de reporte da WSUS:** O Windows Update Agent nos computadores dos clientes pode criar mensagens de evento sustéticas. Estes eventos não são usados pelo Diretor de Configuração. Assim, a opção, **Não crie eventos de reporte WSUS,** é selecionada por padrão. Quando estes eventos não são criados, a única altura em que o cliente deve ligar-se ao servidor WSUS é durante a avaliação da atualização de software e os exames de conformidade. Se estes eventos forem necessários para reportar fora do Gestor de Configuração, modifique esta configuração para criar eventos de reporte WSUS.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Agenda de sincronização  

Configure o calendário de sincronização apenas no ponto de atualização de software no site de alto nível na hierarquia do Gestor de Configuração. Quando configura a agenda de sincronização, o ponto de atualização de software sincroniza-se com a origem de sincronização à data e à hora que especificar. A programação personalizada permite sincronizar atualizações de software para otimizar para o seu ambiente. Considere as exigências de desempenho do servidor WSUS, servidor de site e rede. Por exemplo, 2:00 am uma vez por semana. Em alternativa, inicie manualmente a sincronização no site de alto nível utilizando a ação de Atualizações de Software de **Sincronização** a partir dos nós de **Atualizações** de Software ou **de Grupos** de Atualização de Software na consola do Gestor de Configuração.  

> [!TIP]  
>  Agende a sincronização das atualizações de software para executar utilizando um tempo adequado para o seu ambiente. Um cenário comum é definir o calendário de sincronização a ser executado pouco depois da versão regular da atualização de software da Microsoft na segunda terça-feira de cada mês. Este dia é tipicamente referido como *Patch Tuesday*. Se utilizar o Gestor de Configuração para fornecer definições de Proteção de Pontofinal e Definições do Windows Defender e atualizações do motor, considere definir o calendário de sincronização para funcionar diariamente.  

Após o ponto de atualização do software sincronizar com sucesso, envia um pedido de sincronização para sites infantis. Se tiver pontos de atualização de software adicionais num site primário, envia um pedido de sincronização para cada ponto de atualização de software. Este processo é repetido em todos os sites da hierarquia.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a>Classificações de atualização  

Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, o site sincroniza os metadados para as classificações especificadas. 

O Gestor de Configuração suporta a sincronização das seguintes classificações de atualização:  

-   **Atualizações Críticas**: Uma atualização amplamente lançada para um problema específico que aborda um bug crítico e não relacionado com a segurança.  

-   **Atualizações de Definição**: Uma atualização para ficheiros de vírus ou outras definições.  

-   **Pacotes de funcionalidades**: Novas funcionalidades que são distribuídas fora de um lançamento do produto e que são normalmente incluídas na próxima versão completa do produto.  

-   **Atualizações de Segurança**: Uma atualização amplamente lançada para um problema específico do produto e relacionado com a segurança.  

-   **Pacotes de serviços**: Um conjunto cumulativo de hotfixos que é aplicado a um SISTEMA ou aplicação. Estes hotfixes incluem atualizações de segurança, atualizações críticas e atualizações de software.  

-   **Ferramentas**: Um utilitário ou recurso que ajuda a completar uma ou mais tarefas.  

-   **Atualização Rollups**: Um conjunto cumulativo de hotfixes que é embalado em conjunto para uma fácil implantação. Estes hotfixes incluem atualizações de segurança, atualizações críticas e atualizações de software. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  

-   **Atualizações**: Uma atualização de uma aplicação ou ficheiro que está atualmente instalado.  

-   **Upgrades**: Uma atualização de funcionalidade para uma nova versão do Windows 10.  

Configure as definições de classificação da atualização apenas no site de alto nível. As definições de classificação da atualização não estão configuradas no ponto de atualização do software em sites infantis, porque os metadados de atualizações de software são replicados a partir do site de alto nível. Quando selecionar as classificações da atualização, esteja ciente de que mais classificações seleciona, mais tempo demora a sincronizar os metadados das atualizações de software.  

> [!WARNING]  
>  Como uma boa prática, limpe todas as classificações antes de sincronizar pela primeira vez. Após a sincronização inicial, selecione as classificações desejadas e, em seguida, reexecutar a sincronização.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a>Produtos  

Os metadados de cada atualização de software definem um ou mais produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um SISTEMA ou aplicação. Um exemplo de um produto é o Microsoft Windows 10. Uma família de produtos é a base de OS ou aplicação a partir da qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Microsoft Windows, do qual o Windows 10 e o Windows Server 2016 são membros. Selecione uma família de produtos ou produtos individuais dentro de uma família de produtos.  

Quando as atualizações de software são aplicáveis a vários produtos, e pelo menos um dos produtos é selecionado para sincronização, todos os produtos aparecem na consola Do Gestor de Configuração mesmo que alguns produtos não tenham sido selecionados. Por exemplo, apenas seleciona o produto Windows Server 2012. Se uma atualização de software se aplica ao Windows Server 2012 e ao Windows Server 2012 Datacenter Edition, ambos os produtos estão na base de dados do site.  

Configure as definições do produto apenas no site de alto nível. As definições do produto não estão configuradas no ponto de atualização do software para sites infantis porque os metadados de atualizações de software são replicados a partir do site de alto nível. Quanto mais produtos selecionar, mais tempo demora a sincronizar os metadados das atualizações de software.  

> [!IMPORTANT]  
>  O Gestor de Configuração armazena uma lista de produtos e famílias de produtos que escolhe quando instala o ponto de atualização do software. Os produtos e famílias de produtos que são lançados após a libertação do Gestor de Configuração podem não estar disponíveis para selecionar até completar a sincronização. O processo de sincronização atualiza a lista de produtos disponíveis e famílias de produtos a partir das quais pode escolher. Limpe todos os produtos antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione os produtos desejados e, em seguida, reexecutar a sincronização.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a>Regras de supersedência  

Normalmente, uma atualização de software que substitui outra atualização de software executa uma ou mais das seguintes ações:  

-   Melhora ou atualiza a correção que foi fornecida por uma ou mais atualizações publicadas anteriormente.  

-   Melhora a eficiência do pacote de ficheiros de atualização substituído, que é instalado nos clientes se a atualização for aprovada para instalação. Por exemplo, a atualização supersed pode conter ficheiros que já não são relevantes para a correção ou para os sistemas operativos que são suportados pela nova atualização. Esses ficheiros não estão incluídos no pacote de ficheiros de superseding da atualização.  

-   Atualiza as versões mais recentes de um produto. Por outras palavras, atualiza versões que já não são aplicáveis a versões ou configurações antigas de um produto. As atualizações também podem substituir outras atualizações se tiverem sido efetuadas modificações para expandir o suporte de idiomas. Por exemplo, uma revisão posterior de uma atualização de produto para o Microsoft Office pode remover o suporte para um SISTEMA mais antigo, mas pode adicionar suporte adicional para novos idiomas na versão inicial da atualização.  

Nas propriedades do ponto de atualização do software, especifique que as atualizações de software substituídos estão imediatamente expiradas. Esta definição impede que sejam incluídos em novas implementações. Também assinala as implementações existentes para indicar que contêm uma ou mais atualizações de software expiradas. Ou especificar um período de tempo antes de expirarem as atualizações de software substituídos. Esta ação permite-lhe continuar a implantá-los. 

Considere os seguintes cenários em que poderá ser necessário implementar uma atualização de software substituída:  

-   Uma atualização de software substituindo suporta apenas versões mais recentes de um SISTEMA. Alguns dos seus computadores clientes executam versões anteriores do Sistema Operativo.  

-   Uma atualização de software de superseding tem aplicabilidade mais restrita do que a atualização de software que substitui. Este comportamento tornaria isto inapropriado para alguns clientes.  

-   Se não foi aprovada uma atualização de software de superseding para implantação no seu ambiente de produção.  

    > [!NOTE]  
    > - Antes da versão 1806 do Gestor de Configuração, quando o Gestor de Configuração define uma atualização de software supersed para **Expirado,** não define a atualização para **Declinada** no WSUS. Os clientes continuam a procurar uma atualização expirada até que a atualização seja recusada manualmente ou através de um script personalizado.  Após a versão 1806 do Gestor de Configuração, o Gestor de Configuração também recusará as atualizações supersed no WSUS. Para obter mais informações sobre a tarefa de limpeza wSUS, consulte a [manutenção das atualizações](../deploy-use/software-updates-maintenance.md)de Software.
    > - A partir da versão 1810 do Gestor de Configuração, pode especificar o comportamento das regras de supersedência para **atualizações** de funcionalidades separadamente de **atualizações não-funcionalidades**.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a>Idiomas  

As definições de idioma para o ponto de atualização do software permitem-lhe configurar: 
- Os idiomas para os quais os detalhes sumários (atualizações de software metadados) são sincronizados para atualizações de software  
- Os idiomas de ficheiros de atualização de software que são descarregados para atualizações de software  

#### <a name="software-update-file"></a>Ficheiro de atualização de software  
Configure os idiomas para a definição de ficheiros de **atualização** de Software nas propriedades para o ponto de atualização do software. Esta definição fornece os idiomas padrão que estão disponíveis quando descarrega atualizações de software num site. Modifique os idiomas que são selecionados por padrão cada vez que as atualizações do software são descarregadas ou implementadas. Durante o processo de transferência, os ficheiros de atualização de software dos idiomas configurados são transferidos para a localização da origem do pacote de implementação se os ficheiros de atualização de software estiverem disponíveis no idioma selecionado. Em seguida, são copiados para a biblioteca de conteúdos no servidor do site. Depois são distribuídos pelos pontos de distribuição que estão configurados para o pacote.  

Configure as definições de idiomas de ficheiros de atualização de software com os idiomas mais utilizados no seu ambiente. Por exemplo, os clientes no seu site usam principalmente inglês e japonês para Windows ou aplicações. Há poucas outras línguas que são usadas no site. Selecione apenas inglês e japonês na coluna **'Ficheiro de Atualização** de Software' quando descarregar ou implementar a atualização de software. Esta ação permite-lhe utilizar as definições predefinidas na página de Seleção de **Idiomas** da implementação e descarregamento dos assistentes. Esta ação também impede que ficheiros de atualização desnecessários sejam descarregados. Configure esta definição em cada ponto de atualização de software na hierarquia do Gestor de Configuração.  



#### <a name="summary-details"></a>Detalhes de resumo  
Durante o processo de sincronização, as informações dos detalhes de resumo (metadados de atualizações de software) são atualizadas para as atualizações de software nos idiomas especificados. Os metadados fornecem informações sobre a atualização do software, por exemplo:
- Nome
- Descrição
- Produtos que a atualização suporta
- Classificação de atualização
- Id do artigo
- Baixar URL
- Regras de aplicabilidade

Configure as definições de detalhes sumários apenas no site de nível superior. Os detalhes sumários não estão configurados no ponto de atualização de software em sites infantis porque os metadados de atualizações de software são replicados a partir do site da administração central usando replicação baseada em ficheiros. Ao selecionar os idiomas de detalhes de resumo, selecione apenas os idiomas de que necessita no seu ambiente. Quanto mais idiomas forem selecionados, mais tempo demorará a sincronização dos metadados de atualizações de software. O Gestor de Configuração apresenta os metadados de atualização de software no local do SISTEMA em que a consola do Gestor de Configuração funciona. Se as propriedades localizadas para as atualizações de software não estiverem disponíveis no local deste SISTEMA, o software atualiza os ecrãs de informação em inglês.  

> [!IMPORTANT]  
>  Selecione todos os detalhes sumários que precisa. Quando o ponto de atualização do software no site de alto nível sincroniza com a fonte de sincronização, os detalhes sumários selecionados determinam os metadados de atualizações de software que recupera. Se modificar os detalhes sumários idiomas após a sincronização ter sido decorrido pelo menos uma vez, ele recupera os metadados de atualizações de software para os detalhes sumários modificados idiomas apenas para atualizações de software novas ou atualizadas. As atualizações de software que já foram sincronizadas não são atualizadas com novos metadados para os idiomas modificados, a menos que haja uma alteração na atualização de software na fonte de sincronização.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a>Tempo máximo de execução
<!--3734426-->
*(Introduzido na versão 1906)*

A partir da versão 1906, pode especificar o tempo máximo que uma instalação de atualização de software tem de ser concluída. Pode especificar o tempo máximo de execução para o seguinte:

- **O tempo máximo de execução para as atualizações de funcionalidades do Windows (minutos)**
  - **Atualizações** de funcionalidades - Uma atualização que está numa destas três classificações:
    - Upgrades
    - Update rollups
    - Service packs

- **O tempo máximo de execução para as atualizações do Office 365 e as atualizações sem recurso para windows (minutos)**
  - **Atualizações sem recurso** - Uma atualização que não é uma atualização de funcionalidades e cujo produto está listado como uma das seguintes:
    - Windows 10 (todas as versões)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Estas definições apenas alteram o prazo máximo de execução para novas atualizações que são sincronizadas a partir do Microsoft Update. Não altera o tempo de execução nas atualizações de funcionalidades existentes ou não-funcionalidades.
- Todos os outros produtos e classificações não são configuráveis com esta definição. Se precisar de alterar o tempo máximo de execução de uma destas atualizações, [configure as definições](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings) de atualização de software

> [!NOTE]
> Na versão 1906, o prazo máximo de execução não está disponível quando instalar o ponto de atualização de software de alto nível. Após a instalação, edite o tempo máximo de execução no seu ponto de atualização de software de topo.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a>Plano para uma janela de manutenção de atualizações de software  

Adicione uma janela de manutenção dedicada à instalação de atualizações de software. Esta ação permite configurar uma janela de manutenção geral e uma janela de manutenção diferente para atualizações de software. Quando configura uma janela de manutenção geral e atualiza uma janela de manutenção de software, os clientes instalam atualizações de software apenas durante a janela de manutenção de atualizações de software. 

Começando pela versão 1810 do Gestor de Configuração, pode alterar este comportamento e permitir que as atualizações de software se instalem durante uma janela de manutenção geral. Para obter mais informações sobre esta definição de cliente, consulte as definições do cliente de Atualizações de [Software.](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)

Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a>Reinicie opções para clientes do Windows 10 após instalação de atualização de software

Quando uma atualização de software que requer um reinício é implementada e instalada utilizando o Gestor de Configuração, o cliente agenda um reinício pendente e exibe uma caixa de diálogo de reinício.

Quando há um reinício pendente para uma atualização de software do Gestor de Configuração, a opção de **Atualizar e Reiniciar** e Atualizar e **Desligar** está disponível nos computadores do Windows 10 nas opções de energia do Windows. Depois de utilizar uma destas opções, o diálogo de reinício não é apresentado após o reinício do computador. Em determinadas circunstâncias, o sistema operativo pode remover as opções de reinício pendentes. Isto pode acontecer se a funcionalidade Fast Startup no Windows 10 estiver ativada. Para mais informações, consulte [as Atualizações que podem não ser instaladas com o Fast Startup no Windows 10](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a>Avaliar atualizações de software após uma atualização de pilha de manutenção
<!--4639943-->
A partir da versão 2002, o Gestor de Configuração deteta se uma atualização de pilha de serviços (SSU) faz parte de uma instalação para várias atualizações. Quando uma SSU é detetada, é instalada primeiro. Após a instalação da SSU, um ciclo de avaliação de atualização de software funciona para instalar as restantes atualizações. Esta alteração permite instalar uma atualização cumulativa dependente após a atualização da pilha de manutenção. O dispositivo não precisa de reiniciar entre instalações e não precisa de criar uma janela de manutenção adicional. As SSUs são instaladas primeiro apenas para instalações não-utilizadoradas. Por exemplo, se um utilizador iniciar uma instalação para várias atualizações do Software Center, a SSU pode não ser instalada primeiro.


## <a name="next-steps"></a>Passos seguintes
Assim que planeia atualizações de software, consulte [prepare-se para a gestão](../get-started/prepare-for-software-updates-management.md)de atualizações de software.  

Para obter mais informações sobre a gestão do Windows como um serviço, consulte os [Fundamentos do Gestor de Configuração como um serviço e o Windows como um serviço](../../core/understand/configuration-manager-and-windows-as-service.md).
