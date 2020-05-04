---
title: Interoperabilidade entre versões
titleSuffix: Configuration Manager
description: Aprenda a evitar conflitos entre várias hierarquias do Gestor de Configuração na mesma rede.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713087"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Interoperabilidade entre diferentes versões do Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode instalar e operar várias hierarquias independentes de Configuração Manager na mesma rede. No entanto, como diferentes hierarquias de Gestor de Configuração não operam fora do processo de migração, cada hierarquia requer configurações para prevenir conflitos entre eles. Além disso, pode criar certas configurações para ajudar os recursos que gere a interagir com os sistemas do site a partir da hierarquia correta.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a>Interoperabilidade entre ramo atual e versões anteriores  

Sites de diferentes versões não podem coexistir na mesma hierarquia do Gestor de Configuração. As únicas exceções são durante o processo dos seguintes cenários de atualização:

- Do System Center 2012 Configuration Manager ao gerente de configuração da filial atual
- De uma versão atual do Gestor de Configuração para uma versão mais recente usando atualizações na consola

Pode implantar um site de ramificação e hierarquia do Gestor de Configuração lado a lado com um site ou hierarquia do System Center 2012 existente. Planeie evitar que os clientes de qualquer uma das versões tentem aderir a um site a partir da outra versão.

Por exemplo, se duas ou mais hierarquias do Gestor de Configuração tiverem [limites sobrepostos](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) que incluam as mesmas localizações de rede, atribuam cada novo cliente a um site específico em vez de utilizar a atribuição automática do site. Para mais informações, consulte [Como atribuir clientes a um site](../../clients/deploy/assign-clients-to-a-site.md).  

Além disso, não é possível instalar um cliente do System Center 2012 Configuration Manager num computador que acolhe uma função de sistema de site a partir da secção atual do Gestor de Configuração. Também não pode instalar um cliente de sucursal do Gestor de Configuração num computador que acolhe uma função do sistema de site a partir do System Center 2012 Configuration Manager.  

Os seguintes clientes e ligações não são suportados:  

- Qualquer Gestor de Configuração do System Center 2012 ou versão anterior do cliente do computador  

- Qualquer Gestor de Configuração do System Center 2012 ou cliente anterior de gestão de dispositivos  

- Cliente de gestão de dispositivos Windows CE Platform Builder (qualquer versão)  

- Ligação VPN do System Center Mobile Device Manager  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre a atribuição de sites a clientes  

Os clientes do Gestor de Configuração podem ser atribuídos apenas a um único site primário. Não se pode prever a atribuição real do site de um cliente quando todas as seguintes condições são verdadeiras:

- Utiliza a atribuição automática do site para atribuir clientes a um site durante a instalação do cliente
- Mais de um grupo de fronteiras inclui a mesma fronteira
- Os grupos de fronteira têm diferentes locais atribuídos

Se os limites se sobrepuserem a vários sites e hierarquias do Gestor de Configuração, os clientes podem não ser atribuídos ao site que espera, ou podem não ser atribuídos a um site.  

Os clientes da filial atual do Gestor de Configuração verificam a versão do site antes de completarem a atribuição do site. Se os limites do site se sobrepõem, não pode atribuir clientes a um site com uma versão anterior. No entanto, os clientes anteriores do System Center 2012, os clientes do Gestor de Configuração 2012 podem ser incorretamente atribuídos a um site de sucursal do Gestor de Configuração posterior.  

Para evitar que os clientes sejam atribuídos involuntariamente ao local errado quando duas hierarquias têm limites sobrepostos, configure os parâmetros de instalação do cliente para atribuir clientes a um site específico.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a>Limitações do Gestor de Configuração numa hierarquia de versão mista  

Quando atualiza si a hierarquia atual do 'Gestor de Configuração', há momentos em que diferentes sites terão versões diferentes. Por exemplo, primeiro atualiza o site da administração central. Devido às janelas de manutenção do site, não atualiza os locais primários até uma hora e data posteriores.  

Quando diferentes sites numa única hierarquia executam versões diferentes, algumas funcionalidades não estão disponíveis. Este comportamento pode afetar a forma como gere os objetos do Gestor de Configuração na consola do Gestor de Configuração e qual a funcionalidade disponível para os clientes. Normalmente, a funcionalidade a partir da versão mais recente do 'Gestor de Configuração' não é acessível em sites ou clientes que executam uma versão de pacote de serviço mais baixa.  

### <a name="network-access-account"></a>Conta de acesso à rede

Atualiza o site da administração central para a filial atual do Gestor de Configuração. Você vê os dados da conta de acesso à rede a partir de uma consola do Gestor de Configuração que está ligada a este site atualizado. Não exibe detalhes da conta de sites que ainda gerem o System Center 2012 Configuration Manager.

Depois de atualizar o site principal para a mesma versão do site da administração central, os detalhes da conta são visíveis na consola.

O mesmo comportamento aplica-se quando atualiza entre versões do 'Gestor de Configuração'.

### <a name="boot-images-for-os-deployment"></a>Imagens de arranque para implementação de OS

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>Ao atualizar do System Center 2012 Configuração Manager para o gerente de configuração da filial atual

Quando o site de alto nível de uma hierarquia atualiza para o ramo atual do Gestor de Configuração, atualiza automaticamente as imagens de boot padrão para utilizar a versão 10 do Windows Assessment and Deployment Kit (ADK). Utilize estas imagens de boot apenas para implementações para clientes nos sites de sucursais atuais do Gestor de Configuração. Para mais informações, consulte [Planeamento para interoperabilidade](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)de implantação de OS .

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Ao atualizar entre as versões atuais do 'Gestor de Configuração'

Enquanto as novas versões do 'Gestor de Configuração' não atualizarem a versão do Windows ADK que está a ser utilizada, não há qualquer efeito nas imagens de arranque.

### <a name="new-task-sequence-steps"></a>Novos passos de sequência de tarefas

Quando criauma sequência de tarefas com um passo introduzido numa versão do 'Gestor de Configuração' que não está disponível numa versão anterior, pode ter os seguintes problemas:

- Ocorre um erro quando se tenta editar a sequência de tarefas a partir de um site que está a executar uma versão anterior do 'Gestor de Configuração'.

- A sequência de tarefas não funciona num computador que executa uma versão anterior do cliente do Gestor de Configuração.

### <a name="client-to-down-level-management-point-communications"></a>Comunicações de ponto de gestão de baixo nível

Um cliente do Gestor de Configuração que comunica com um ponto de gestão a partir de um site que executa uma versão mais baixa do que o cliente só pode usar a funcionalidade que a versão de baixo nível do Gestor de Configuração suporta. Por exemplo, se implementar conteúdo a partir de um site de sucursais do Gestor de Configuração que foi recentemente atualizado para um cliente que comunica com um ponto de gestão que ainda não atualizou para essa versão, esse cliente não pode utilizar novas funcionalidades a partir da versão mais recente.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Implementações de sequências de pacotes e tarefas para clientes legados

<!-- SCCMDocs-pr issue #3493 -->

A partir da versão 1902, não é possível implementar um pacote ou sequência de tarefas para uma versão cliente 5.7730 ou mais cedo. Para contornar esta limitação, atualize o cliente para uma versão posterior.

## <a name="software-updates"></a>Atualizações de software

### <a name="orchestration-groups"></a>Grupos de orquestração

Grupos de orquestração, introduzidos na versão 2002, não podem ser usados numa hierarquia de versão mista. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a>Interoperabilidade para a consola De Configuração Manager  

Esta secção contém informações sobre a utilização da consola 'Gestor de Configuração' num ambiente que tem uma mistura de versões de Gestor de Configuração.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Um ambiente com o Gestor de Configuração do System Center 2012 e o gerente de configuração atual

Para gerir um site de Configuração Manager, tanto a consola como o site a que a consola se conecta devem executar a mesma versão do Gestor de Configuração. Por exemplo, não pode utilizar uma consola de Configuração System Center 2012 para gerir um site de ramificação atual do Gestor de Configuração, ou o contrário.

Não é suportado para instalar tanto a consola System Center 2012 Configuration Manager como a consola de ramificação atual do Gestor de Configuração no mesmo computador.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Um ambiente com múltiplas versões do Gestor de Configuração

O ramo atual do Gestor de Configuração não suporta instalar mais do que uma única consola de Configuração manager num computador. Para utilizar várias consolas específicas para diferentes versões do 'Gestor de Configuração', instale as diferentes consolas em computadores separados.

Durante o processo de atualização de sites numa hierarquia para uma nova versão, pode ligar uma consola a um site que executa uma versão mais recente e visualizar informações sobre outros sites nessa hierarquia. No entanto, esta configuração não é recomendada. É possível que as diferenças entre a versão da consola e a versão do site do Configuration Manager possam resultar em problemas de dados. Algumas funcionalidades que estão disponíveis na versão mais recente do produto não estarão disponíveis na consola.

Não é suportado para gerir um site quando se utiliza uma consola com uma versão que não corresponde à versão do site. Fazê-lo pode causar perda de dados e pode colocar o seu site em risco. Por exemplo, não é suportado para usar uma consola a partir da versão 1610 para gerir um site que executa a versão 1606.
