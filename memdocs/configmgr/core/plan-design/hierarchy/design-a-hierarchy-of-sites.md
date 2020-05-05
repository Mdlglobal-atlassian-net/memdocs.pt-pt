---
title: Desenhe uma hierarquia do site
titleSuffix: Configuration Manager
description: Compreenda as topoologias disponíveis e as opções de gestão para o Gestor de Configuração para planear a hierarquia do seu site.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073352"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Desenhe uma hierarquia de sites para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de instalar o primeiro site de uma nova hierarquia do Gestor de Configuração, é uma boa ideia entender:  

- As topoologias disponíveis para O Gestor de Configuração  

- Os tipos de sites disponíveis e as suas relações entre si  

- O âmbito de gestão que cada tipo de site fornece  

- As opções de gestão de conteúdos que podem reduzir o número de sites que precisa de instalar  

Em seguida, planeje uma topologia que sirva eficientemente as suas necessidades de negócio atual e possa expandir-se mais tarde para gerir o crescimento futuro.  

Ao planear, tenha em mente limitações para adicionar sites adicionais a uma hierarquia ou a um site autónomo:  

- Instale um novo local primário abaixo de um site de administração central, até ao [número suportado de locais primários](../configs/size-and-scale-numbers.md) para a hierarquia.  

- [Expandir um local primário autónomo para instalar um novo site de administração central,](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)para depois instalar locais primários adicionais.  

- Instale novos locais secundários abaixo de um local primário, até ao [limite suportado para o local primário](../configs/size-and-scale-numbers.md) e hierarquia geral.  

- Não é possível adicionar um site previamente instalado a uma hierarquia existente para fundir dois sites autónomos. O Gestor de Configuração apenas suporta a instalação de novos sites numa hierarquia de sites existente.  


> [!NOTE]  
> Ao planear uma nova instalação do Gestor de Configuração, esteja atento às notas de [lançamento](../../servers/deploy/install/release-notes.md), que detalham os problemas atuais nas versões ativas. As notas de lançamento aplicam-se a todos os ramos do Gestor de Configuração. Quando utilizar o ramo de [pré-visualização técnica,](../../get-started/technical-preview.md)encontre questões específicas dessa sucursal na documentação para cada versão da pré-visualização técnica.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a>Topologia hierárquica  

As topoologias da hierarquia variam de:  

- Simplest: Um único local primário autónomo  

- Mais complexo: Um grupo de locais primários e secundários conectados com um local de administração central no local de alto nível da hierarquia  

O principal impulsionador do tipo e contagem de sites que utiliza numa hierarquia é geralmente o número e o tipo de dispositivos que deve suportar.   

### <a name="standalone-primary-site"></a>Local primário autónomo

Utilize um site primário autónomo quando puder suportar a gestão de todos os dispositivos e utilizadores. Para mais informações, consulte [dimensionamento e números de escala](../configs/size-and-scale-numbers.md). Esta topologia também é bem sucedida quando as localizações geográficas da sua empresa podem ser servidas por um único local primário. Para ajudar a gerir o tráfego de rede, utilize vários pontos de gestão em grupos de fronteira, e uma infraestrutura de conteúdo cuidadosamente planeada. Para obter mais informações, consulte [grupos de fronteira configure](../../servers/deploy/configure/boundary-groups.md) e [conceitos fundamentais para gestão](fundamental-concepts-for-content-management.md)de conteúdos.  

Esta topologia proporciona os seguintes benefícios:  

- Overhead administrativo simplificado  

- Atribuição de site de cliente e deteção de recursos e serviços disponíveis simplificadas  

- Eliminação de eventuais atrasos introduzidos pela replicação da base de dados entre sites  

- Opção de expandir um local primário autónomo para uma hierarquia maior com um site de administração central. Esta opção permite-lhe então instalar novos locais primários para expandir a escala da sua implementação.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Site da administração central com um ou mais locais primários infantis 

Utilize esta topologia quando necessitar de mais de um site primário para apoiar a gestão de todos os seus dispositivos e utilizadores. É necessário quando se precisa usar mais do que um único local primário. 

Esta topologia proporciona os seguintes benefícios:  

- Suporta até 25 locais primários que lhe permitem estender a escala da sua hierarquia.    

- Utilize sempre o site da administração central, a menos que reinstale os seus sites. Esta opção é permanente. Não se pode separar um local primário para torná-lo um local primário autónomo.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a>Determine quando usar um site de administração central  

Utilize um site de administração central para configurar configurações de hierarquia e monitorizar todos os sites e objetos da hierarquia. Este tipo de site não gere os clientes diretamente. Coordena a replicação de dados site-to-site, que inclui a configuração de sites e clientes em toda a hierarquia.  

As informações seguintes podem ajudar a decidir quando instalar um site de administração central:  

- O site da administração central é o local de alto nível numa hierarquia.  

- Quando configurar uma hierarquia que tenha mais de um local primário, instale um site de administração central.  

     - Se precisar imediatamente de dois ou mais locais primários, instale primeiro o site da administração central.  

     - Quando já tiver um site primário, e quiser instalar um site de administração central, [expanda o local primário autónomo](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) para instalar o site da administração central.  

- O site da administração central apoia apenas locais primários como locais infantis.  

- O site da administração central não pode ter clientes atribuídos a ele.  

- O site da administração central não suporta funções do sistema do site que suportam diretamente os clientes, tais como pontos de gestão e pontos de distribuição.  

- Gerencie todos os clientes na hierarquia e execute todas as tarefas de gestão do site a partir da consola Do Gestor de Configuração que esteja ligada ao site da administração central. Estas tarefas incluem a instalação de pontos de gestão ou outras funções do sistema de sites em sites primários ou secundários infantis.  

- Quando se usa um site de administração central, é o único local onde se vê dados do site de todos os sites da sua hierarquia. Estes dados incluem informações como dados de inventário e mensagens de estado.  

- Configure operações de descoberta em toda a hierarquia a partir do local da administração central. A partir do local da administração central, atribua métodos de descoberta para executar em locais primários individuais.  

- Gerir a segurança em toda a hierarquia, atribuindo diferentes funções de segurança, âmbitos de segurança e coleções a diferentes utilizadores administrativos. Estas configurações aplicam-se em cada site da hierarquia.  

- Configure a replicação para controlar a comunicação entre os sites da hierarquia. Agendar a replicação da base de dados para os dados do site e gerir a largura de banda para a transferência de dados baseados em ficheiros entre sites.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a>Determine quando usar um local primário  

Utilize sites primários para gerir clientes. Instale um local primário como um local infantil abaixo de um site de administração central, ou como o primeiro local de uma nova hierarquia. Um local primário que é o primeiro local de uma hierarquia cria um local primário autónomo. Ambos os locais primários infantis e locais primários autónomos suportam locais secundários.  

Considere adicionar locais primários adicionais pelas seguintes razões:  

- Para aumentar o número de dispositivos, gerencie com uma única hierarquia.  

- Para satisfazer requisitos de gestão organizacional. Por exemplo, pode instalar um site primário num local remoto para gerir a transferência de conteúdo de implementação através de uma rede de baixa largura de banda.  

     - Considere, em vez disso, utilizar opções para acelerar a largura de banda da rede ao transferir dados para um ponto de distribuição. Essa capacidade de gestão de conteúdos pode substituir a necessidade de instalar sites adicionais.  


As seguintes informações podem ajudá-lo a decidir quando instalar um site primário:  

- Um site primário pode ser um site primário autónomo ou um site primário subordinado numa hierarquia de maiores dimensões. Quando um site primário é um membro de uma hierarquia com um site de administração central, os sites utilizam a replicação de base de dados para replicar dados entre os sites. A menos que precise de suportar mais clientes e dispositivos do que um único site primário, considere instalar um site primário autónomo. Depois de instalar um local primário autónomo, expanda-o se necessário no futuro para reportar a um novo site da administração central para aumentar a sua implantação.  

- Um site primário suporta apenas um site de administração central como um site de pais.  

- Um site primário suporta apenas locais secundários como locais infantis, e suporta vários locais secundários.  

- Os sites primários são responsáveis pelo tratamento de todos os dados do cliente dos seus clientes designados.  

- Os sites primários usam a replicação da base de dados para comunicar diretamente com o seu site de administração central. Este comportamento é configurado automaticamente quando um novo site instala.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a>Determine quando usar um site secundário  

Utilize sites secundários para gerir a transferência de conteúdos de implementação e dados de clientes através de redes de baixa largura de banda.  

Você gere um site secundário a partir de um site de administração central ou do local primário do local principal do site secundário. Os locais secundários estão ligados a um local primário. Não é possível movê-los para um local de pais diferente sem os desinstalar e depois reinstalá-los como um site infantil abaixo do novo local primário.

No entanto, pode encaminhar o conteúdo entre dois sites secundários para ajudar a gerir a replicação baseada em ficheiros de conteúdo de implementação. Para transferir dados do cliente para um site primário, o site secundário utiliza replicação baseada em ficheiros. Um site secundário também utiliza a replicação de base de dados para comunicar com o respetivo site primário principal.  

Considere a instalação de um site secundário se qualquer uma das seguintes condições se aplicar:  

- Não é necessário um ponto de conectividade local para um utilizador administrativo.  

- É obrigado a gerir a transferência de conteúdo de implantação para sites mais baixos na hierarquia.  

- É obrigado a gerir a informação do cliente que é enviada para sites mais altos na hierarquia.  

Se não quiser instalar um site secundário, e tiver clientes em locais remotos, considere as seguintes opções:  

- Utilize tecnologias peer-to-peer, como o Windows BranchCache  

- Ativar pontos de distribuição para controlo e agendamento de largura de banda   

Utilize estas opções de gestão de conteúdos com ou sem sites secundários. Ajudam a reduzir o tamanho da sua infraestrutura de Gestor de Configuração. Para obter mais informações sobre as opções de gestão de conteúdos no Gestor de Configuração, consulte [Determinar quando utilizar opções](#BKMK_ChooseSecondaryorDP)de gestão de conteúdos .  


As informações seguintes podem ajudar a decidir quando instalar um site secundário:  

- Se uma instância local do Servidor SQL não estiver disponível, os servidores secundários do site instalam automaticamente o SQL Server Express durante a instalação do local.  

- A instalação do local secundário é iniciada a partir da consola 'Gestor de Configuração', em vez de executar a configuração diretamente num computador.  

- Os sites secundários utilizam um subconjunto da informação na base de dados do site. Este comportamento reduz a quantidade de dados que a SQL replica entre o local primário dos pais e o local secundário.  

- Os sites secundários apoiam o encaminhamento de conteúdo baseado em ficheiros para outros sites secundários que têm um site primário comum dos pais.  

- As instalações secundárias do site instalam automaticamente as funções do sistema do site de ponto de gestão e ponto de distribuição no servidor do site secundário.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a>Determine quando usar opções de gestão de conteúdos  

Se tiver clientes em localizações de rede remotas, considere utilizar uma ou mais opções de gestão de conteúdo em vez de um site primário ou secundário. As seguintes opções muitas vezes removem a necessidade de instalar um site:  

- Otimização de entrega para o Windows 10  

- Cache de pares do Gestor de Configuração  

- Windows BranchCache  

- Configure pontos de distribuição para controlo de largura de banda  

- Copiar manualmente o conteúdo para pontos de distribuição (conteúdo pré-estágio)  


Se alguma das seguintes condições se aplicar, considere a implementação de um ponto de distribuição em vez de instalar outro site:  

- A largura de banda da sua rede é suficiente para que os computadores clientes no local remoto se comuniquem com um ponto de gestão no local principal. Os clientes comunicam com um ponto de gestão para baixar a política do cliente, enviar inventário, enviar o estado de reporte e enviar informações sobre descobertas.  

- O Serviço de Transferência Inteligente de Fundo (BITS) não fornece um controlo de largura de banda suficiente para os seus requisitos de rede.  

Para obter mais informações sobre opções de gestão de conteúdos no Gestor de Configuração, consulte [conceitos fundamentais para a gestão](fundamental-concepts-for-content-management.md)de conteúdos.  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a>Além da topologia da hierarquia  

Juntamente com a sua topologia de hierarquia inicial, considere também as seguintes questões:  

- Quais as funções do sistema do site que fornecem serviços ou capacidades de diferentes sites na hierarquia?  

- Como está a gerir configurações e capacidades em toda a hierarquia na sua infraestrutura?  


As seguintes considerações comuns são abrangidas por artigos separados. Esta informação é importante para influenciar ou ser influenciada pelo seu projeto de hierarquia:  

- Quando estiver a preparar-se para [gerir computadores e dispositivos,](../../clients/manage/manage-clients.md)considere se os dispositivos estão no local, na nuvem, ou se inclui dispositivos pertencentes ao utilizador (BYOD). Além disso, considere como irá gerir dispositivos que suportam múltiplas opções de gestão. Por exemplo, gerencie os dispositivos do Windows 10 com O Gestor de Configuração ou apesar da integração com o Microsoft Intune. Para mais informações, consulte [Escolha uma solução de gestão](../choose-a-device-management-solution.md)do dispositivo .  

- Compreenda como a sua infraestrutura de rede disponível pode afetar o fluxo de dados entre locais remotos. Para mais informações, consulte [Prepare o ambiente da sua rede.](../network/configure-firewalls-ports-domains.md) Considere também a localização geográfica dos seus utilizadores e dispositivos e se acedem à sua infraestrutura através da sua rede no local ou da internet.  

- Planeie uma infraestrutura de conteúdo para distribuir de forma eficiente o conteúdo que implementa para dispositivos que gere. Este conteúdo pode ser aplicações, atualizações de software ou sistemas operativos. Para mais informações, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)  

- Determine quais [as funcionalidades e capacidades do Gestor de Configuração](../changes/features-and-capabilities.md) que pretende utilizar. Diferentes funcionalidades requerem diferentes funções do sistema do site ou infraestruturas windows. Numa hierarquia de vários sites, decida onde os implementa para o uso mais eficiente da sua rede e recursos de servidor.  

- Considere a segurança dos dados e dispositivos, incluindo a utilização de uma infraestrutura de chaves públicas (PKI). Para mais informações, consulte os requisitos do [certificado PKI](../network/pki-certificate-requirements.md).  


Reveja os seguintes artigos para configurações específicas do site:  

- [Planear o Fornecedor de SMS](plan-for-the-sms-provider.md)  

- [Planear a base de dados do site](plan-for-the-site-database.md)  

- [Planear os servidores do sistema de sites e as funções do sistema de sites](plan-for-site-system-servers-and-site-system-roles.md)  

- [Plano de segurança](../security/plan-for-security.md)  

- [Gerir a largura de banda da rede](manage-network-bandwidth.md) ao implementar conteúdos num site  


Considere configurações que abrangem sites e hierarquias  

- [Opções de alta disponibilidade](../../servers/deploy/configure/high-availability-options.md) para sites e hierarquias

- [Alargar o esquema](../network/extend-the-active-directory-schema.md) de Diretório Ativo e configurar sites para publicar dados do [site](../../servers/deploy/configure/publish-site-data.md)  

- [Transferências de dados entre sites](data-transfers-between-sites.md)  

- [Noções básicas sobre a administração baseada em funções](../../understand/fundamentals-of-role-based-administration.md)  

- [Gerir clientes na internet](../../clients/manage/manage-clients-internet.md)  

