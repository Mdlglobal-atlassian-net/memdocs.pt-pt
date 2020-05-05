---
title: Funções do sistema do site do site de planos
titleSuffix: Configuration Manager
description: Considere servidores de sistema de site e funções do sistema do site enquanto planeia a sua hierarquia do Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722446"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Plano para servidores de sistema de site e funções do sistema do site no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Cada site do Gestor de Configuração que instala inclui um servidor de site que é um servidor de sistema de **site**. O site também pode incluir servidores do sistema de sites adicionais em computadores que são remotos em relação ao servidor do site. Os servidores do sistema de sites (o servidor do site ou um servidor do sistema de sites remoto) suportam **funções do sistema de sites**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a>Servidores do sistema do site  

Quando instala uma função do sistema de site num computador, esse computador torna-se um servidor de sistema de site. Em cada site, pode instalar um ou mais servidores adicionais do sistema de site. Não tem de instalar servidores adicionais do sistema do site e pode optar por executar todas as funções do sistema do site diretamente no computador do servidor do site. Cada servidor do sistema do site suporta uma ou mais funções do sistema do site. Servidores adicionais podem ajudar a expandir as capacidades e a capacidade de um site partilhando a carga de processamento que as funções do sistema do site colocam num servidor.  

Ao considerar a adição de um servidor de sistema de site, certifique-se de que o servidor cumpre os pré-requisitos para a utilização pretendida. Adicione-o também numa localização de rede que tenha largura de banda suficiente para comunicar com os pontos finais esperados. Estes pontos finais incluem o servidor do site, recursos de domínio, uma localização baseada na nuvem, servidores de sistemas de site e clientes.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a>Funções do sistema do site  

Instale as funções do sistema do site num servidor para fornecer capacidades adicionais ao site. Os exemplos incluem:  

- Pontos de gestão adicionais para que o site possa suportar mais dispositivos, até à capacidade suportada do site.  

- Pontos de distribuição adicionais para expandir a sua infraestrutura de conteúdo, melhorando o desempenho das distribuições de conteúdos para dispositivos.  

- Uma ou mais funções específicas do sistema do site. Por exemplo, um ponto de atualização de software permite-lhe gerir atualizações de software para dispositivos geridos. Um ponto de serviços de reporte permite-lhe executar relatórios para monitorizar, compreender e partilhar informações sobre o seu ambiente.  

Diferentes sites do Gestor de Configuração podem suportar diferentes conjuntos de funções do sistema do site. O conjunto suportado de funções do sistema do site depende do tipo de site. (Os tipos de sítios incluem um site de administração central, locais primários ou locais secundários.) A topologia da sua hierarquia pode limitar a colocação de alguns papéis em certos tipos de site. Por exemplo, o ponto de ligação de serviço só é suportado no local de topo da hierarquia. O site de topo pode ser um site de administração central ou um local primário autónomo. Este papel não é suportado num local primário infantil ou em locais secundários.  

Depois de um site ser instalado, pode mover a localização de algumas funções do sistema do site da sua localização padrão no servidor do site para outro servidor. Por exemplo, as funções de ponto de gestão ou ponto de distribuição são instaladas por padrão num servidor de site primário ou secundário. Instale também instâncias adicionais de algumas funções do sistema do site para expandir as capacidades do seu site e para satisfazer os seus requisitos de negócio. Alguns papéis são necessários, enquanto outros são opcionais.  

### <a name="configuration-manager-site-server"></a>Servidor de site do Gestor de Configuração

Esta função identifica o servidor onde é executada a configuração do Gestor de Configuração para instalar um site, ou o servidor no qual instala um site secundário. Não pode mover ou desinstalar esta função até que o site esteja desinstalado.  

### <a name="configuration-manager-site-system"></a>Sistema de site do Gestor de Configuração

Esta função é atribuída a qualquer computador no qual instale um site ou instale uma função do sistema do site. Não pode mover ou desinstalar esta função até remover a última função do sistema do site do computador.  

### <a name="configuration-manager-component-site-system-role"></a>Função do sistema de sistema de componentes do Gestor de Configuração

Esta função identifica um sistema de site que executa uma instância do serviço **SMS Executive.** É necessário apoiar outras funções, como pontos de gestão. Não pode mover ou desinstalar esta função até remover a última função do sistema de site aplicável do computador.  

### <a name="configuration-manager-site-database-server"></a>Servidor de base de dados do Gestor de Configuração

O site atribui esta função aos servidores do sistema do site que possuem uma instância da base de dados do site. Apenas move esta função para um novo servidor executando a configuração para modificar o site para usar uma instância diferente do SQL Server para hospedar a base de dados do site.  

### <a name="sms-provider"></a>Fornecedor de SMS

O site atribui esta função a cada computador que acolhe uma instância do Provedor de SMS. O fornecedor é a interface entre uma consola do Gestor de Configuração e a base de dados do site. Por predefinição, esta função instala-se automaticamente no servidor do site do site da administração central e nos principais sites. Instale instâncias adicionais em cada site para fornecer acesso a utilizadores administrativos adicionais ou para despedimento.  

Para instalar fornecedores adicionais, executar configuração do Gestor de Configuração para [Gerir o Fornecedor SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Em seguida, instale fornecedores adicionais em computadores adicionais. Instale apenas uma instância do Fornecedor sms num computador. O computador deve estar no mesmo domínio que o servidor do site.  

### <a name="application-catalog-web-service-point"></a>Ponto de serviço web de catálogo de aplicações

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Uma função do sistema de site que fornece informações de software para o site do catálogo de aplicações a partir da biblioteca de software. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

### <a name="application-catalog-website-point"></a>Ponto de site do catálogo de aplicações

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Uma função do sistema de site que fornece aos utilizadores uma lista de software disponível a partir do catálogo de aplicações. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence

Uma função do sistema de site que se conecta à Microsoft para descarregar informações para o catálogo de Inteligência de Ativos. Este papel também envia títulos não categorizados, para que a Microsoft possa considerá-los para futura inclusão no catálogo. Uma hierarquia apoia apenas uma única instância deste papel no local de topo da sua hierarquia. Se expandir um local primário autónomo para uma hierarquia maior, desinstale esta função a partir do local principal. Em seguida, instale-o no site da administração central.

Para mais informações, consulte [a Inteligência do Ativo no Gestor de Configuração](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Ponto de registo de certificados

Uma função do sistema de site que comunica com um servidor que executa o Serviço de Inscrição de Dispositivos de Rede (NDES). Esta função gere os pedidos de certificadodo dispositivo que utilizam o Protocolo de Inscrição de CertificadoSimples (SCEP). Esta função só é suportada em sites primários e no site de administração central.

Embora um único ponto de registo de certificado possa fornecer funcionalidade a toda uma hierarquia, pode querer instalar várias instâncias desta função num site, e em vários sites da mesma hierarquia. Este design ajuda no equilíbrio de carga. Quando existem várias instâncias numa hierarquia, os clientes são atribuídos aleatoriamente a um dos pontos de registo de certificados.  

Cada ponto de registo de certificado requer acesso a uma instância DeS separada. Não é possível configurar dois ou mais pontos de registo de certificados para utilizar a mesma instância NDES. Além disso, não instale o ponto de registo do certificado no mesmo servidor que executa o NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Ponto de ligação de gateway de gestão de nuvem

Uma função do sistema de site para comunicar com o gateway de gestão de [nuvem.](../../clients/manage/cmg/plan-cloud-management-gateway.md)  

### <a name="data-warehouse-service-point"></a>Ponto de serviço de armazém de dados

Utilize o ponto de serviço de armazém de dados para armazenar e reportar sobre dados históricos a longo prazo no seu ambiente de Gestor de Configuração. Para mais informações, consulte [data warehouse](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Ponto de distribuição

Uma função do sistema de site que contém ficheiros de origem para os clientes descarregarem, por exemplo:

- Conteúdo de aplicação
- Pacotes de software
- Atualizações de software
- Imagens do SO
- Imagens de arranque  

Por predefinição, esta função instala-se no servidor do site quando instala um novo site primário ou secundário. Este papel não é apoiado num site da administração central. Instale vários casos desta função num site apoiado, e em vários locais da mesma hierarquia. Para mais informações, consulte [conceitos fundamentais para a gestão](fundamental-concepts-for-content-management.md)de conteúdos, e gerir a infraestrutura de [conteúdos e conteúdos.](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)  

### <a name="endpoint-protection-point"></a>Ponto de Endpoint Protection

Uma função de sistema de site que o Gestor de Configuração usa para aceitar os termos da licença de proteção de pontofinal, e para configurar a subscrição padrão para o Serviço de Proteção de Nuvem. Uma hierarquia apenas apoia uma única instância deste papel, e isso deve estar no local de topo. Se expandir um local primário autónomo para uma hierarquia maior, desinstale esta função a partir do local principal e, em seguida, instale-o no local da administração central. Para mais informações, consulte [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Ponto de inscrição

Uma função do sistema de site que utiliza certificados PKI para Configuração Manager para inscrever dispositivos móveis e computadores macOS. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

Se um utilizador inscrever dispositivos móveis utilizando o 'Gestor de Configuração' e a conta de Diretório Ativo do utilizador estiver numa floresta que não é fidedigna pela floresta do servidor do site, instale um ponto de inscrição na floresta do utilizador. Em seguida, o Gestor de Configuração pode autenticar o utilizador.  

### <a name="enrollment-proxy-point"></a>Ponto proxy de registo

Uma função do sistema de site que gere os pedidos de inscrição do Gestor de Configuração de dispositivos móveis e computadores macOS. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

Quando apoiar dispositivos móveis na internet, instale um ponto de procuração de matrículanuma rede de perímetro e instale um na intranet.

### <a name="exchange-server-connector"></a>Conector do Exchange Server

Para obter informações sobre esta função, consulte [Gerir dispositivos móveis com Gestor de Configuração e Troca](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Ponto de estado de contingência

Uma função do sistema de site que o ajuda a monitorizar a instalação do cliente. Identifica clientes que não são geridos porque não conseguem comunicar com o seu ponto de gestão. Embora esta função seja suportada apenas em locais primários, você pode instalar vários casos deste papel em um site, e em vários sites na mesma hierarquia.

### <a name="management-point"></a>Ponto de gestão

Uma função do sistema de site que fornece informações de política e localização de serviço aos clientes. Também recebe dados de configuração de clientes.  

Por predefinição, esta função instala-se no servidor do site quando instala um novo site primário ou secundário. Os sites primários apoiam várias instâncias deste papel. Os sites secundários apoiam um único ponto de gestão. Também referido como um ponto de gestão de procuração, este papel num site secundário fornece um ponto de contacto local para os clientes obterem políticas de computador e utilizador.  

Configurar pontos de gestão para apoiar http ou HTTPs. Também podem suportar dispositivos móveis que gere com o Gestor de Configuração no local de gestão de dispositivos móveis (MDM). Para ajudar a reduzir a carga de processamento colocada no servidor de base de dados do site por pontos de gestão, uma vez que eles serviços pedidos dos clientes, use réplicas de Base de [dados para pontos](../../servers/deploy/configure/database-replicas-for-management-points.md)de gestão .  

### <a name="reporting-services-point"></a>Ponto do Reporting Services

Uma função do sistema de site que se integra com os Serviços de Relato de Servidores SQL para criar e gerir relatórios para O Gestor de Configuração. Esta função é suportada em locais primários e no site da administração central, e você pode instalar vários casos desta função em um site apoiado. Para mais informações, consulte [Planeamento para reportagem](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Ponto de ligação de serviço

Uma função do sistema do site que faz upload dos dados de utilização do seu site, e é necessária para disponibilizar atualizações para O Gestor de Configuração na consola. Uma hierarquia só suporta uma única instância deste papel, e isso deve estar no local de topo da sua hierarquia. Se expandir um local primário autónomo para uma hierarquia maior, desinstale esta função a partir do local principal e, em seguida, instale-o no local da administração central. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Ponto de atualização de software

Uma função de sistema de site que se integra com os Serviços de Atualização do Servidor do Windows (WSUS) para fornecer atualizações de software aos clientes do Gestor de Configuração. Este papel é apoiado em todos os sites:  

- Instale este sistema de site no site da administração central para sincronizar com a WSUS.  

- Configurar cada instância deste papel em locais primários infantis para sincronizar com o site da administração central.  

- Quando a transferência de dados através da rede for lenta, considere instalar um ponto de atualização de software em sites secundários.  

Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md)de software .  

### <a name="state-migration-point"></a>Ponto de Migração de Estado

Quando se migra um computador para um novo sistema operativo, este sistema de site armazena dados do estado do utilizador. Este papel é apoiado em locais primários e em locais secundários. Instale vários casos desta função num site, e em vários locais da mesma hierarquia. Para obter mais informações sobre o estado de armazenamento do utilizador quando implementar um Sistema operativo, consulte gerir o [estado do utilizador](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Passos seguintes

Algumas funções do sistema do site do Gestor de Configuração requerem ligações à internet. Se o seu ambiente necessitar de tráfego de internet para utilizar um servidor proxy, configure estas funções do sistema do site para usar o proxy. Para mais informações, consulte o [suporte do servidor Proxy](../network/proxy-server-support.md).  
