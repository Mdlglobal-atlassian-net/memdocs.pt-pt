---
title: Interoperabilidade de implantação de Os
titleSuffix: Configuration Manager
description: Compreenda problemas de interoperabilidade quando diferentes sites do Gestor de Configuração numa única hierarquia usam versões diferentes.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723552"
---
# <a name="plan-for-os-deployment-interoperability"></a>Plano para a interoperabilidade da implantação do OS

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando diferentes sites do Gestor de Configuração numa única hierarquia usam versões diferentes, alguma funcionalidade do Gestor de Configuração não está disponível. Normalmente, a funcionalidade a partir da versão mais recente do 'Gestor de Configuração' não é acessível em sites ou por clientes que executam uma versão mais baixa. Para mais informações, consulte [Interoperabilidade entre diferentes versões do Gestor de Configuração](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Objetos

Considere os seguintes objetos quando atualizar o site de alto nível na sua hierarquia e outros sites na sua hierarquia executar Configuração Manager com uma versão mais baixa:  

### <a name="client-installation-package"></a>Pacote de instalação de clientes  

- A fonte do pacote de instalação do cliente predefinido é automaticamente atualizada. Todos os pontos de distribuição da hierarquia são atualizados com o novo pacote de instalação de clientes. Este comportamento acontece mesmo em pontos de distribuição em sites da hierarquia que estão numa versão mais baixa.  

- Não pode atribuir novos clientes de versão a sites que ainda não atualizou para a nova versão. A atribuição está bloqueada no ponto de gestão.  

### <a name="boot-images"></a>Imagens de arranque  

- Ao atualizar o site de alto nível para a versão mais recente do 'Gestor de Configuração', atualiza automaticamente as imagens de boot padrão (x86 e x64). A atualização utiliza o Windows ADK para o Windows 10, que inclui o Windows PE 10. Os ficheiros associados às imagens de boot predefinidas são atualizados com a versão mais recente do 'Gestor de Configuração' dos ficheiros. O site não atualiza automaticamente as imagens de boot personalizadas. É necessário atualizar manualmente as imagens de boot personalizadas, que incluem versões mais antigas do Windows PE.  

- Quando a hierarquia do site contiver sites com diferentes versões de 'Gestor de Configuração', evite a utilização de meios dinâmicos. Em vez disso, utilize meios baseados no site para contactar um ponto de gestão específico. Depois de atualizar todos os sites para a mesma versão do 'Gestor de Configuração', pode voltar a utilizar meios dinâmicos.

- Verifique se as imagens de boot do Gestor de Configuração mais recentes incluem as suas personalizações. Em seguida, atualize todos os pontos de distribuição nos novos sites da versão com a versão mais recente das novas imagens de arranque.  

### <a name="user-state-migration-tool-usmt"></a>User State Migration Tool (USMT)  

Ao atualizar o site de alto nível para a versão mais recente do 'Gestor de Configuração', atualiza automaticamente o pacote USMT padrão para a versão mais recente. Não atualiza automaticamente quaisquer pacotes USMT personalizados. Precisa atualizar manualmente estes pacotes.  

### <a name="new-task-sequence-steps"></a>Novos passos de sequência de tarefas  

Periodicamente, são introduzidos novos passos de sequência de tarefas com novas versões do Diretor de Configuração. Quando implementa uma sequência de tarefas com um novo passo para clientes mais velhos, o passo da sequência de tarefas falha. Antes de implementar uma sequência de tarefas com um novo passo, certifique-se de que os clientes da coleção de destino são atualizados para a nova versão.  

### <a name="os-deployment-media"></a>Meios de implantação do OS  

Quando o site for atualizado para uma nova versão, atualize todos os meios com o novo pacote de cliente do Gestor de Configuração. Estes tipos de meios de comunicação incluem saqueado, captura, pré-encenação e autónomo.

### <a name="third-party-extensions-to-os-deployment"></a>Extensões de terceiros à implantação do OS  

Quando tiver extensões de terceiros para a implementação de OS e tiver versões diferentes de sites de Gestor de Configuração ou clientes do Gestor de Configuração, pode haver problemas com as extensões.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente dos sites do Gestor de Configuração numa hierarquia mista  

Ao atualizar um site para versão mais recente do Gestor de Configuração, as sequências de tarefas que referem o pacote de instalação padrão do cliente começam automaticamente a implementar a versão cliente mais recente do Gestor de Configuração.

Sequências de tarefas que referenciam um pacote de instalação de cliente personalizado continuam a implementar a versão do cliente que está contida nesse pacote personalizado. Os pacotes personalizados provavelmente incluem uma versão anterior do cliente do Gestor de Configuração. Para evitar falhas na implementação da sequência de tarefas, atualize quaisquer pacotes de instalação personalizados do cliente para a versão mais recente.

Quando configurar uma sequência de tarefas para utilizar um pacote de instalação personalizado do cliente, faça uma das seguintes ações:

- Atualize o passo da sequência de tarefas para utilizar a versão mais recente do Gestor de Configuração do pacote de instalação do cliente
- Atualize o pacote personalizado para utilizar a mais recente fonte de instalação do cliente do Gestor de Configuração

> [!IMPORTANT]  
> Não implemente uma sequência de tarefas que refira o mais recente pacote de instalação de clientes do Gestor de Configuração aos clientes num site mais antigo do Gestor de Configuração. Quando os clientes atribuídos a um site de Gestor de Configuração mais antigo são atualizados para a versão cliente do Mais recente Gestor de Configuração, o Gestor de Configuração bloqueia a atribuição ao site do Gestor de Configuração mais antigo. Estes clientes já não estão atribuídos a nenhum site. Até que atribua manualmente o cliente ao mais recente site do Gestor de Configuração, ou reinstale a versão mais antiga do Gestor de Configuração do cliente no computador, estes clientes não são geridos.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Gestor de Configuração numa hierarquia mista  

Ao atualizar o seu site de administração central para a versão mais recente do Gestor de Configuração, certifique-se de que as sequências de tarefas de implementação de SO que implementa não deixam esses clientes num estado não gerido. Por exemplo, se implementar para clientes atribuídos a um site de Configuração mais antigo que ainda não atualizou para a versão mais recente do Gestor de Configuração.

Faça uma cópia de uma sequência de tarefas que utiliza para implementar para os clientes na versão mais recente do site do Gestor de Configuração. Em seguida, modifique a sequência de tarefas para que possa implantá-la para os clientes num site mais antigo do Gestor de Configuração. Configure a sequência de tarefas para fazer referência a um pacote de instalação personalizado do cliente que utiliza a fonte de instalação do cliente do Gestor de Configuração mais antigo. Se ainda não tiver um pacote de instalação personalizado para clientes que refira a fonte de instalação do cliente do Gestor de Configuração mais antigo, crie manualmente um.  

> [!Important]  
> A partir da versão 1902, não é possível implementar um pacote ou sequência de tarefas para uma versão cliente 5.7730 ou mais cedo. Para contornar esta limitação, atualize o cliente para uma versão posterior.<!-- SCCMDocs-pr issue #3493 -->
