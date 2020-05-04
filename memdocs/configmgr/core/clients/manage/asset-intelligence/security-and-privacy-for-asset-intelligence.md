---
title: Privacidade de segurança da Inteligência de Ativos
titleSuffix: Configuration Manager
description: Obtenha informações de segurança e privacidade para a Inteligência de Ativos no Gestor de Configuração.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714144"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Segurança e privacidade para Inteligência de Ativos em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém informações de segurança e privacidade para a Inteligência de Ativos no Gestor de Configuração.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Melhores práticas de segurança do Asset Intelligence  
 Utilize as seguintes melhores práticas de segurança quando utilizar o Asset Intelligence.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando importar um ficheiro de licença (ficheiro de Licenciamento em Volume da Microsoft ou um ficheiro da Declaração de Licença Geral), proteja o canal de comunicação e de ficheiros.|Utilize permissões do sistema de ficheiros NTFS para garantir que apenas os utilizadores autorizados podem aceder aos ficheiros de licença e utilizar a assinatura SMB (Server Message Block) para assegurar a integridade dos dados quando é transferido para o servidor do site durante o processo de importação.|  
|Utilize o princípio do menor número de permissões para importar os ficheiros de licença.|Utilize a administração baseada em funções para conceder a permissão Gerir Asset Intelligence para o utilizador administrativo que importa os ficheiros de licença. A função incorporada do Gestor do Asset Intelligence inclui esta permissão.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade para o Asset Intelligence  
 A Asset Intelligence alarga as capacidades de inventário do Gestor de Configuração para fornecer um nível mais elevado de visibilidade de ativos na empresa. A recolha de informações do Asset Intelligence não está ativada automaticamente. Pode ativar as classes de relatório de inventário de hardware para modificar o tipo de informações recolhidas. Para mais informações, consulte [Configurar a Inteligência](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)de Ativos .  

 A informação da Inteligência de Ativos é armazenada na base de dados do Gestor de Configuração da mesma forma que as informações de inventário. Quando os clientes estabelecem ligação aos pontos de gestão utilizando HTTPS, os dados são sempre encriptados durante a transferência para o ponto de gestão. Quando os clientes estabelecem ligação ao HTTP, pode configurar a transferência de dados de inventário para serem assinados e encriptados. Os dados de inventário não são armazenados em formato encriptado na base de dados. As informações são retidas na base de dados até que a tarefa de manutenção do site **Eliminar Histórico de Inventário Desatualizado** a elimine todos os 90 dias. Pode configurar o intervalo de eliminação.  

 O Asset Intelligence não envia informações sobre utilizadores e computadores nem sobre a utilização de licenças para a Microsoft. Pode optar por enviar pedidos do System Center Online para categorização, o que significa que pode identificar um ou mais títulos de software que não estejam categorizados e enviá-los para o System Center Online para pesquisa e categorização. Após o carregamento de um título de software, os investigadores da Microsoft identificam, categorizam e disponibilizam estes conhecimentos a todos os utilizadores que utilizam o serviço online. Deve estar ciente das seguintes implicações de privacidade quando submete informações para o System Center Online:  

- O carregamento aplica-se apenas a informações de título de software genérico (nome, publicador e assim sucessivamente) que optar por enviar para o System Center Online. As informações de inventário não são enviadas com um carregamento.  

- O carregamento nunca ocorre de forma automática e o sistema não foi concebido para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.  

- Uma caixa de diálogo mostra exatamente os dados que vão ser carregados, antes do processo de carregamento ser iniciado.  

- As informações de licença não são enviadas à Microsoft. As informações da licença são armazenadas numa área separada da base de dados do Gestor de Configuração, e não podem ser enviadas para a Microsoft.  

- Os títulos de software carregados passam a ser públicos, na medida em que o conhecimento dessa aplicação e a respetiva categorização passam a fazer parte integrante do catálogo do System Center Online Asset Intelligence, podendo assim ser transferidos por outros consumidores do catálogo.  

- A origem do título de software não está registada no catálogo do Asset Intelligence e não é disponibilizada para outros clientes. No entanto, deve certificar-se de que não carregou quaisquer títulos de aplicações que contenham informações privadas.  

- Não é possível resgatar os dados carregados.  

  Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para o System Center Online, tenha em consideração os requisitos de privacidade da sua empresa.  
