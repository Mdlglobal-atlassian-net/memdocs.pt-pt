---
title: Encontre recursos do site
titleSuffix: Configuration Manager
description: Saiba como e quando os clientes do Gestor de Configuração usam a localização do serviço para encontrar recursos do site.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b012dd1e7da0d6a3efb4d1cc33b8a79ef319bc0a
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83269002"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Saiba como os clientes encontram recursos e serviços do site para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os clientes do Gestor de Configuração utilizam um processo chamado localização do *serviço* para localizar servidores do sistema do site com os quais podem comunicar e que fornecem serviços que os clientes são direcionados para o uso. Compreender como e quando os clientes usam a localização do serviço para encontrar recursos do site pode ajudá-lo a configurar os seus sites para suportar com sucesso as tarefas do cliente. Estas configurações podem exigir que o site interaja com configurações de domínio e rede como Ative Directory Domain Services (AD DS) e DNS. Ou podem exigir que configure alternativas mais complexas.  

Exemplos de funções do sistema de sites que fornecem serviços incluem:

- O servidor do sistema do site principal para os clientes.
- O ponto de gestão.
- Servidores adicionais do sistema do site com os quais o cliente pode comunicar, como pontos de distribuição e pontos de atualização de software.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a>Fundamentos da localização do serviço  
 Um cliente avalia a sua localização atual da rede, preferência de protocolo de comunicação e site atribuído quando está a usar a localização do serviço para encontrar um ponto de gestão com o qual possa comunicar.  

**Um cliente comunica com um ponto de gestão para:**  
- Descarregue informações sobre outros pontos de gestão para o site, para que possa construir uma lista de pontos de gestão conhecidos (conhecida como *lista de MP)* para futuros ciclos de localização de serviços.  
- Carregar detalhes de configuração, como inventário e estado.  
- Descarregue uma política que estabeleça configurações no cliente e possa informar o cliente de software que pode ou deve instalar, e outras tarefas relacionadas.  
- Solicite informações sobre funções adicionais do sistema do site que forneçam serviços que o cliente foi configurado para usar. Exemplos incluem pontos de distribuição para software que o cliente pode instalar, ou um ponto de atualização de software a partir do qual obter atualizações.  

**Um cliente do Gestor de Configuração faz um pedido de localização de serviço:**  
- A cada 25 horas de operação contínua.  
- Quando o cliente detetar uma alteração na sua configuração ou localização de rede.  
- Quando o serviço **ccmexec.exe** no computador (o serviço principal do cliente) começar.  
- Quando o cliente deve localizar uma função do sistema do site que forneça um serviço necessário.  

**Quando um cliente está a tentar encontrar servidores que acolhem funções**de sistema de site, ele utiliza a localização do serviço para encontrar uma função de sistema de site que suporte o protocolo do cliente (HTTP ou HTTPS). Por padrão, os clientes utilizam o método mais seguro de que dispõem. Considere o seguinte:  

- Para utilizar HTTPS, tem de ter uma infraestrutura de chaves públicas (PKI) e instalar certificados PKI nos clientes e servidores. Para obter informações sobre como utilizar certificados, consulte [os requisitos de certificado PKI para O Gestor](../../../core/plan-design/network/pki-certificate-requirements.md)de Configuração .  

- Ao implementar uma função do sistema de sites que utiliza Serviços de Informação Internet (IIS) e suporta comunicações de clientes, tem de especificar se os clientes ligam ao sistema de sites através de HTTP ou HTTPS. Se utilizar HTTP, também tem de considerar as opções de assinatura e encriptação. Para mais informações, consulte [Planeamento para Assinatura e Encriptação](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) no Plano de [Segurança](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a>Localização do serviço e como os clientes determinam o seu ponto de gestão atribuído  
Quando um cliente é atribuído pela primeira vez a um site primário, ele seleciona um ponto de gestão padrão para esse site. Os sites primários suportam vários pontos de gestão, e cada cliente identifica independentemente um ponto de gestão como o seu ponto de gestão padrão. Este ponto de gestão padrão torna-se então o ponto de gestão atribuído ao cliente. (Também pode utilizar comandos de instalação do cliente para definir o ponto de gestão atribuído a um cliente quando este estiver instalado.)  

Um cliente seleciona um ponto de gestão para comunicar com base na localização atual da rede do cliente e configurações de grupo de limites. Apesar de ter um ponto de gestão atribuído, este pode não ser o ponto de gestão que o cliente usa.  

> [!NOTE]  
> Um cliente utiliza sempre o ponto de gestão atribuído para mensagens de registo e determinadas mensagens de política, mesmo quando são enviadas outras comunicações para um ponto de gestão local ou de proxy.

Pode utilizar pontos de gestão preferenciais. Os pontos de gestão preferidos são pontos de gestão do site atribuído a um cliente que estão associados a um grupo de limites que o cliente está a usar para encontrar servidores do sistema do site. A associação de um ponto de gestão preferencial com um grupo de fronteiras como servidor de sistema de site é semelhante à forma como os pontos de distribuição ou pontos de migração do Estado estão associados a um grupo de fronteiras. Se ativar pontos de gestão preferenciais para a hierarquia, quando um cliente utilizar um ponto de gestão a partir do site atribuído, este tentará utilizar um ponto de gestão preferencial antes de utilizar outros pontos de gestão a partir do site atribuído.  

Também pode usar a informação no blog de [afinidade](https://docs.microsoft.com/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3) do ponto de gestão para configurar a afinidade do ponto de gestão. A afinidade do ponto de gestão sobrepõe-se ao comportamento padrão dos pontos de gestão atribuídos e permite ao cliente utilizar um ou mais pontos de gestão específicos.  

Cada vez que um cliente precisa de contactar um ponto de gestão, verifica a lista de MP, que armazena localmente na Instrumentação de Gestão do Windows (WMI). O cliente cria uma lista de MP inicial quando é instalado. Em seguida, o cliente atualiza periodicamente a lista com detalhes sobre cada ponto de gestão na hierarquia.  

Quando o cliente não encontra um ponto de gestão válido na sua lista de MP, procura as seguintes fontes de localização de serviço, por ordem, até encontrar um ponto de gestão que possa utilizar:  

1.  Ponto de gestão  
2.  AD DS  
3.  DNS  
4.  WINS  

Depois de um cliente localizar e contactar com sucesso um ponto de gestão, descarrega a lista atual de pontos de gestão que estão disponíveis na hierarquia, e atualiza a lista de MP locais. O mesmo aplica-se a clientes com um domínio associado e aos que não têm.  

Por exemplo, quando um cliente do Gestor de Configuração que está na internet se conecta a um ponto de gestão baseado na Internet, o ponto de gestão envia a esse cliente uma lista de pontos de gestão disponíveis na Internet no site. Do mesmo modo, os clientes com um domínio associado ou em grupos de trabalho também recebem uma lista dos pontos de utilização que podem utilizar.  

Um cliente que não esteja configurado para a internet não é fornecido pontos de gestão virados para a Internet. Os clientes do grupo de trabalho configurados para a internet comunicam apenas com pontos de gestão virados para a Internet.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a>A lista de deputados  
A lista de MP é a fonte de localização de serviço preferencial para um cliente, porque é uma lista prioritária de pontos de gestão que o cliente previamente identificou. Esta lista é ordenada por cada cliente com base na respetiva localização de rede quando o cliente atualiza a lista e, em seguida, é armazenada localmente no cliente no WMI.  

### <a name="building-the-initial-mp-list"></a>Construção da lista inicial de MP  
Durante a instalação do cliente, são utilizadas as seguintes regras para a construção da lista inicial de MP do cliente:  

- A lista inicial inclui pontos de gestão especificados durante a instalação do cliente (quando utiliza a opção **SMSMP**= **ou/MP).**  
- O cliente consulta a AD DS para pontos de gestão publicados. Para ser identificado a partir da AD DS, o ponto de gestão deve ser do site designado pelo cliente, e deve ser da mesma versão do produto que o cliente.  
- Se nenhum ponto de gestão foi especificado durante a instalação do cliente, e o esquema de Diretório Ativo não for alargado, o cliente verifica DNS e WINS para pontos de gestão publicados.  
- Quando o cliente constrói a lista inicial, a informação sobre alguns pontos de gestão na hierarquia pode não ser conhecida.  

### <a name="organizing-the-mp-list"></a>Organizar a lista de MP  
Os clientes organizam a sua lista de pontos de gestão utilizando as seguintes classificações:  

- **Proxy**: Um ponto de gestão num local secundário.  
- **Local**: Qualquer ponto de gestão associado à localização atual da rede do cliente, conforme definido pelos limites do site. Note as seguintes informações sobre limites:
  - Quando um cliente pertence a mais de um grupo de limites, a lista de pontos de gestão locais é determinada a partir da união de todos os limites que incluem a localização de rede atual do cliente.  
  - Os pontos de gestão local são tipicamente um subconjunto dos pontos de gestão atribuídos a um cliente, a menos que o cliente esteja numa localização de rede que esteja associada a outro site com pontos de gestão que servem os seus grupos de fronteira.   


- **Atribuído**: Qualquer ponto de gestão que seja um sistema de site para o site atribuído ao cliente.  

Pode utilizar pontos de gestão preferenciais. Os pontos de gestão num site que não estejam associados a um grupo de fronteiras, ou que não estejam num grupo de fronteiraassociado à localização atual da rede de um cliente, não são considerados preferidos. Serão utilizados quando o cliente não conseguir identificar um ponto de gestão preferido disponível.  

### <a name="selecting-a-management-point-to-use"></a>Selecionar um ponto de gestão a utilizar  
Para comunicações típicas, um cliente tenta utilizar um ponto de gestão a partir das classificações na seguinte ordem, com base na localização da rede do cliente:  

1.  Proxy  
2.  Localização  
3.  Atribuída  

No entanto, o cliente utiliza sempre o ponto de gestão atribuído para o registo de mensagens e determinadas políticas de mensagens, mesmo quando são enviadas outras comunicações para um ponto de gestão local ou de um proxy.  

Dentro de cada classificação (procuração, local ou atribuída), o cliente tenta utilizar um ponto de gestão baseado nas preferências, na seguinte ordem:  

1.  Compatível com HTTPS numa floresta local ou fidedigna (quando o cliente está configurado para comunicação HTTPS)  
2.  HTTPS não capaz de não estar numa floresta de confiança ou local (quando o cliente está configurado para comunicação HTTPS)  
3.  HTTP capaz de uma floresta de confiança ou local  
4.  HTTP capaz não em uma floresta de confiança ou local  

A partir do conjunto de pontos de gestão classificados por preferências, o cliente tenta utilizar o primeiro ponto de gestão da lista. Esta lista ordenada de pontos de gestão é aleatória e não pode ser encomendada. A ordem da lista pode alterar cada vez que o cliente atualiza a sua lista de MP.  

Quando um cliente não consegue estabelecer contacto com o primeiro ponto de gestão, tenta cada ponto de gestão sucessivo na sua lista. Tenta cada ponto de gestão preferido na classificação antes de experimentar os pontos de gestão não preferidos. Se um cliente não conseguir comunicar com sucesso com qualquer ponto de gestão na classificação, tenta contactar um ponto de gestão preferido a partir da próxima classificação, e assim por diante, até encontrar um ponto de gestão a utilizar.  

Depois de um cliente estabelecer comunicação com um ponto de gestão, continua a utilizar esse mesmo ponto de gestão até:  

- Passaram-se 25 horas.  
- O cliente não consegue comunicar com o ponto de gestão por cinco tentativas num período de 10 minutos.

Em seguida, o cliente seleciona aleatoriamente um novo ponto de gestão a usar.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a>Diretório Ativo  
Os clientes que têm um domínio associado podem utilizar o AD DS para a localização de serviços. Isto requer que os sites [publiquem dados no Active Directory](../../servers/deploy/configure/publish-site-data.md).  

Um cliente pode utilizar AD DS para localização de serviço quando todas as seguintes condições forem verdadeiras:  

- O esquema de Diretório Ativo [foi alargado](../network/extend-the-active-directory-schema.md) ou foi estendido para System Center 2012 Configuration Manager.  
- A [floresta de Diretório Ativo está configurada para publicação](../../servers/deploy/configure/publish-site-data.md), e os sites do Gestor de Configuração estão configurados para publicar.  
- O computador cliente é membro de um domínio do Active Directory e consegue aceder a um servidor de catálogo global.  

Se um cliente não encontrar um ponto de gestão para usar para a localização do serviço a partir de AD DS, tenta utilizar DNS.  

##  <a name="dns"></a><a name="bkmk_dns"></a>DNS  
Os clientes na intranet podem utilizar o DNS para localização de serviços. Isto requer que, pelo menos, um site numa hierarquia publique informações sobre os pontos de gestão no DNS.  

Considere a utilização do DNS para localização de serviços quando se verificar qualquer das seguintes condições:
- O esquema AD DS não é estendido para suportar o Gestor de Configuração.
- Os clientes na intranet estão localizados numa floresta que não está habilitada para a publicação do Gestor de Configuração.  
- Tem clientes em computadores de grupo de trabalho, e esses clientes não estão configurados para gestão de clientes apenas na Internet. (Um cliente de grupo de trabalho configurado para a internet comunicará apenas com pontos de gestão virados para a Internet e não utilizará DNS para a localização do serviço.)  
- Pode [configurar clientes para encontrar pontos de gestão do DNS](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Quando um site publica registos de localização de serviços para pontos de gestão no DNS:  

- A publicação é aplicável apenas a pontos de gestão que aceitem ligações de clientes a partir da Internet.  
- A publicação adiciona um registo de recurso de localização de serviços (SRV RR) na zona DNS do computador do ponto de gestão. Tem de existir uma entrada de anfitrião correspondente no DNS desse computador.  

Por padrão, os clientes unidos pelo domínio procuram DNS para obter registos de pontos de gestão a partir do domínio local do cliente. Pode configurar uma propriedade do cliente que especifica um sufixo de domínio para um domínio que tenha informações de ponto de gestão publicadas no DNS.  

Para obter mais informações sobre como configurar a propriedade do cliente sufixo DNS, consulte [como configurar os computadores dos clientes para encontrar pontos de gestão utilizando a publicação dNS](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Se um cliente não encontrar um ponto de gestão para usar para a localização do serviço a partir do DNS, tenta utilizar WINS.  

### <a name="publish-management-points-to-dns"></a>Publicar pontos de gestão no DNS  
Para publicar pontos de gestão no DNS, terão de se verificar as duas condições seguintes:  

- Os servidores de DNS suportam registos de recursos de localização de serviço, utilizando a versão 8.1.2 ou superior do BIND.  
- As FQDNs intranet especificadas para os pontos de gestão no Gestor de Configuração têm entradas de anfitriões (por exemplo, registos A) em DNS.  

> [!IMPORTANT]  
> A publicação dNS do Gestor de Configuração não suporta um espaço de nome desarticulado. Se tiver um espaço de nome desarticulado, pode publicar manualmente pontos de gestão para dNS ou utilizar um dos outros métodos de localização do serviço que estão documentados nesta secção.  

**Quando os seus servidores DNS suportam atualizações automáticas,** pode configurar o Configuro Diretor de Configuração para publicar automaticamente pontos de gestão na intranet para DNS, ou pode publicar manualmente estes registos para dNS. Quando os pontos de gestão são publicados no DNS, o respetivo FQDN da intranet e número de porta são publicados no registo de localização de serviço (SRV). Configura a publicação de DNS num site nas Propriedades componentes de ponto de gestão do site. Para mais informações, consulte os componentes do Site para O Gestor de [Configuração](../../../core/servers/deploy/configure/site-components.md).  

Quando a **sua zona DNS está definida como "Secure only" para atualizações dinâmicas,** apenas o primeiro ponto de gestão a publicar no DNS pode fazê-lo com sucesso com permissões por defeito.

Se apenas um ponto de gestão puder publicar e alterar com sucesso o seu registo DNS, e o servidor de ponto de gestão estiver saudável, os clientes podem obter a lista completa de MP desse ponto de gestão e, em seguida, encontrar o seu ponto de gestão preferido.


**Se os servidores DNS não suportarem atualizações automáticas, mas suportarem registos de localização de serviço**, poderá publicar manualmente os pontos de gestão no DNS. Para tal, terá de especificar manualmente o registo de recursos de localização de serviço (SRV RR) no DNS.  

O Gestor de Configuração suporta o RFC 2782 para registos de localização de serviço. Estes registos têm o seguinte formato: *_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

Para publicar um ponto de gestão ao Gestor de Configuração, especifique os seguintes valores:  

- **_Service**: Insira **_mssms_mp**_ &lt; sitecode, onde o código de site é o código de \> site do ponto &lt; \> de gestão.  
- **._Proto**: Especifique **._tcp**.  
- **.Name**: Introduza o sufixo DNS do ponto de gestão, como, por exemplo, **contoso.com**.  
- **TTL**: Introduza **14400**, que corresponde a quatro horas.  
- **Classe**: Especifique **IN** (em conformidade com RFC 1035).  
- **Prioridade**: O Gestor de Configuração não utiliza este campo.
- **Peso**: O Gestor de Configuração não utiliza este campo.  
- **Porta**: Introduza o número de porta utilizado pelo ponto de gestão, como, por exemplo, **80** para HTTP e **443** para HTTPS.  

  > [!NOTE]  
  >  A porta de registo SRV deve corresponder à porta de comunicação que o ponto de gestão utiliza. Por padrão, este é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

- **Destino**: Introduza o FQDN da intranet especificado para o sistema de sites que está configurado com a função de site do ponto de gestão.  

Se utilizar o DNS do Windows Server, poderá utilizar o procedimento seguinte para introduzir este registo DNS para pontos de gestão da intranet. Se utilizar outra implementação para DNS, utilize as informações desta secção relativas aos valores dos campos e consulte a documentação do DNS para adaptar este procedimento.  

##### <a name="to-configure-automatic-publishing"></a>Para configurar a publicação automática:  

1.  Na consola de Configuração Manager, expanda os Sites de Configuração do Site **da Administração.**  >  **Site Configuration**  >  **Sites**  

2.  Selecione o seu site e, em seguida, escolha os Componentes do **Site Configurar**.  

3.  Escolha **o Ponto de Gestão.**  

4.  Selecione os pontos de gestão que pretende publicar. (Esta seleção aplica-se à publicação de AD DS e DNS.)  

5.  Verifique a caixa para publicar no DNS. Esta caixa:  

    - Permite-lhe selecionar quais os pontos de gestão a publicar no DNS.  

    - Não configura a publicação para AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Para publicar manualmente pontos de gestão no DNS no Windows Server  

1.  Na consola 'Gestor de Configuração', especifique as FQDNs intranet dos sistemas do site.  

2.  Na consola de gestão de DNS, selecione a zona DNS do computador do ponto de gestão.  

3.  Verifique se existe um registo de anfitrião (A ou AAAA) para o FQDN da intranet do sistema de sites. Se o registo não existir, crie-o.  

4.  Utilizando a opção **New Other Records,** escolha a Localização do **Serviço (SRV)** na caixa de diálogo do Tipo de Registo de **Recursos,** escolha **Criar O Registo,** introduza as seguintes informações e, em seguida, escolha **Done:**  

    - **Domínio**: Se necessário, introduza o sufixo DNS do ponto de gestão, como, por exemplo, **contoso.com**.  
    - **Serviço**: Tipo **_mssms_mp**_ &lt; sitecode, onde o código de site é o código de \> site do ponto &lt; \> de gestão.  
    - **Protocolo**: Escreva **_tcp**.  
    - **Prioridade**: O Gestor de Configuração não utiliza este campo.  
    - **Peso**: O Gestor de Configuração não utiliza este campo.  
    - **Porta**: Introduza o número de porta utilizado pelo ponto de gestão, como, por exemplo, **80** para HTTP e **443** para HTTPS.  

      > [!NOTE]  
      > A porta de registo SRV deve corresponder à porta de comunicação que o ponto de gestão utiliza. Por padrão, este é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

    - **Anfitrião que ofereça este serviço**: Introduza a intranet FQDN especificada para o sistema de site que está configurado com a função do site do ponto de gestão.  

Repita estes passos para cada ponto de gestão da intranet que pretenda publicar no DNS.  

##  <a name="wins"></a><a name="bkmk_wins"></a>GANHA  
Se os outros mecanismos de localização de serviço falharem, os clientes poderão encontrar um ponto de gestão inicial consultando o WINS.  

Por padrão, um site primário publica para WINS o primeiro ponto de gestão no site que está configurado para HTTP e o primeiro ponto de gestão que está configurado para HTTPS.  

Se não pretender que os clientes encontrem um ponto de gestão HTTP no WINS, configure-os com a propriedade CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  
