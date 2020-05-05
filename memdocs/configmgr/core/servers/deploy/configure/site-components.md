---
title: Componentes do site
titleSuffix: Configuration Manager
description: Aprenda a configurar os componentes do site para modificar o comportamento das funções do sistema do site e relatórios de estado do site.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718330"
---
# <a name="site-components-for-configuration-manager"></a>Componentes do site para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para cada site do Gestor de Configuração, pode configurar os componentes do site para modificar o comportamento das funções do sistema do site e do relatório do estado do site. As configurações dos componentes do site aplicam-se a um site e a cada instância de uma função do sistema de site aplicável no site.  

Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione um site. No grupo **Definições** da fita, escolha Componentes do **Site Configurar**. Selecione uma das seguintes opções:

- [Distribuição de software](#software-distribution)  
- [Ponto de atualização de software](#software-update-point) 
- [Implementação do sistema operativo](#operating-system-deployment)
- [Ponto de gestão](#management-point)  
- [Relatório de estado](#status-reporting)  
- [Notificação por e-mail](#email-notification)
- [Avaliação de adesão à coleção](#bkmk_colleval)


## <a name="about-site-components"></a>Acerca dos componentes do site  

 A maioria das opções para os vários componentes do site são autoexplicativas quando vistas na consola Do Gestor de Configuração. No entanto, os seguintes detalhes podem ajudar a explicar algumas das configurações mais complexas, ou direcioná-lo para conteúdo adicional.  

> [!Note]  
> As opções disponíveis para alguns componentes variam se você seleciona o site da administração central, um site primário ou um site secundário. Alguns componentes não estão disponíveis para certos tipos de sites.  



### <a name="software-distribution"></a>Distribuição de software  

#### <a name="content-distribution-settings"></a>Definições de distribuição de conteúdos
No separador **Geral,** especifique as definições que modificam a forma como o servidor do site transfere o conteúdo para os seus pontos de distribuição. Quando aumenta os valores que utiliza para as definições de distribuição simultânea, a distribuição de conteúdo pode utilizar mais largura de banda de rede.  

#### <a name="pull-distribution-point"></a>Ponto de distribuição de puxar
Para mais informações, consulte [Utilize um ponto de distribuição de puxar](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### <a name="network-access-account"></a>Conta de acesso à rede
Para mais informações, consulte [a conta](../../../plan-design/hierarchy/accounts.md#network-access-account)de acesso à Rede .  


### <a name="software-update-point"></a>Ponto de atualização de software  

Para mais informações, consulte [Instale um ponto](../../../../sum/get-started/install-a-software-update-point.md)de atualização de software .  


### <a name="operating-system-deployment"></a>Implementação do sistema operativo

Para mais informações, consulte [Especifique a unidade para manutenção de imagem de osso offline](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Ponto de gestão  

No separador **Geral,** criou o site para publicar informações sobre os seus pontos de gestão para serviços de domínio de diretório ativo.  

Os clientes do Gestor de Configuração utilizam pontos de gestão para localizar serviços e para encontrar informações do site, tais como a desminagem do grupo de fronteira e opções de seleção de certificados PKI. Os clientes também usam pontos de gestão para encontrar outros pontos de gestão no site, bem como pontos de distribuição a partir dos quais descarregar software. Os pontos de gestão também ajudam os clientes a completar a atribuição do site, e a descarregar a política do cliente e a carregar informações sobre o cliente.  

O método mais seguro para os clientes encontrarem pontos de gestão é publicá-los em Ative Directory Domain Services. Este método de localização de serviço requer que o seguinte seja verdade:

- O esquema é estendido para O Gestor de Configuração.
- Há um contentor de **Gestão** de Sistemas, com permissões de segurança apropriadas para o servidor do site publicar neste contentor.
- O site do Gestor de Configuração está configurado para publicar nos Serviços de Domínio do Diretório Ativo.
- Os clientes pertencem à mesma floresta de Diretório Ativo que a floresta do servidor do site.  

Quando os clientes na intranet não puderem usar os Serviços de Domínio do Diretório Ativo para encontrar pontos de gestão, utilize [a publicação dNS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

Para obter informações gerais sobre a localização do serviço, consulte [entenda como os clientes encontram recursos e serviços](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)do site.  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publique pontos de gestão intranet selecionados no DNS
Especifique esta opção quando os clientes na intranet não conseguem encontrar pontos de gestão dos Serviços de Domínio do Diretório Ativo. Em vez disso, podem usar um registo de recursos de localização de serviço DNS (SRV RR) para encontrar um ponto de gestão no seu site designado.  

Para que o Gestor de Configuração publique pontos de gestão intranet para dNS, todas as seguintes condições devem ser satisfeitas:  

-   Os servidores DNS possuem uma versão de BIND 8.1.2 ou posterior.  

-   Os seus servidores DNS estão configurados para atualizações automáticas e registos de recursos de localização de suporte.  

-   Os nomes de domínio totalmente qualificados especificados (FQDNs) para os pontos de gestão no Gestor de Configuração têm entradas de anfitriões (registos A ou AAA) em DNS.  

> [!WARNING]  
>  Para que os clientes encontrem pontos de gestão publicados no DNS, deve atribuir os clientes a um site específico (em vez de utilizar a atribuição automática do site). Configurar estes clientes para utilizar o código do site com o sufixo de domínio do seu ponto de gestão. Para mais informações, consulte [a localização de pontos de gestão.](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points)  

Se os clientes do Gestor de Configuração não puderem utilizar os Serviços de Domínio de Diretório Ativo ou dNS para encontrar pontos de gestão na intranet, utilizam [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). O primeiro ponto de gestão que está instalado para o site é automaticamente publicado para WINS quando é configurado para aceitar conexões de clientes HTTP na intranet.  


### <a name="status-reporting"></a>Relatório de estado  

Estas configurações configuram diretamente o nível de detalhe que está incluído nos relatórios de estado de sites e clientes.  


### <a name="email-notification"></a>Notificação por e-mail  

Especifique detalhes do servidor de conta e de e-mail para permitir ao Gestor de Configuração enviar notificações de e-mail para alertas.  

Para mais informações, consulte [Alertas de Utilização e o sistema de estado](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a>Avaliação de adesão à coleção  

Utilize este componente para definir a frequência com que a adesão à coleção é avaliada de forma incremental. A avaliação incremental atualiza uma associação da coleção apenas com recursos novos ou alterados.  

Para mais informações, consulte [as melhores práticas para recolhas.](../../../clients/manage/collections/best-practices-for-collections.md)



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Utilizar o Gestor do Serviço do Configuration Manager para gerir componentes do site  

Pode utilizar o Gestor de Serviço sinuoso de Configuração para controlar os serviços do Gestor de Configuração e para ver o estado de qualquer serviço de Gestor de Configuração ou linha de trabalho. Estes serviços e fios são referidos coletivamente como componentes do Gestor de Configuração. Compreenda as seguintes declarações sobre componentes do Gestor de Configuração:  

-   Os componentes podem ser executados em qualquer sistema de site.  

-   Os componentes são geridos da mesma forma que gere os serviços no Windows. Pode iniciar, parar, parar, retomar ou consultar componentes do Gestor de Configuração.  

Um serviço de Gerente de Configuração funciona quando há algo para fazer. Esta ação é normalmente quando um ficheiro de configuração é escrito na caixa de entrada de um componente. 


### <a name="use-the-configuration-manager-service-manager"></a>Utilize o Gestor de Serviço de Gestor de Configuração  

1.  Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o **Estado do Sistema**e selecione o nó de Estado do **Componente.**  

2.  No grupo **Componente** da fita, selecione **Iniciar**, e, em seguida, escolha o Gestor de Serviço de Gestor de **Configuração**.  

3.  Quando o Gestor do Serviço do Configuration Manager for aberto, estabeleça a ligação ao site que pretende gerir.  

     Se não vir o site que pretende gerir, vá ao menu **do Site** e selecione **Connect**. Em seguida, introduza o nome do servidor do site do local correto.  

4.  Expandir o site e navegar para **Componentes** ou **Servidores,** dependendo de onde estão localizados os componentes que pretende gerir.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, no menu **Componente,** selecione **Consulta** para atualizar o estado da sua seleção.  

6.  Depois de atualizado o estado do componente, utilize uma das quatro opções baseadas em ação no menu **Componente** para modificar o funcionamento do componente. Após solicitar uma ação, deve consultar o componente para apresentar o novo estado do componente.  

7.  Feche o Gestor de Serviço de Gestor de Configuração quando terminar de modificar o estado operacional dos componentes.  
