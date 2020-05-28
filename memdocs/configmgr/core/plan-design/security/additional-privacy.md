---
title: Informações de privacidade adicionais
titleSuffix: Configuration Manager
description: Saiba como a Microsoft recolhe e utiliza dados do 'Gestor de Configuração'.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f877de32c9915f91d1e2d7f2d90b9b40ab69df11
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906574"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Informações adicionais sobre privacidade para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


## <a name="updates-and-servicing"></a>Atualizações e manutenção

O Gestor de Configuração utiliza um modelo de atualização que ajuda a manter o ambiente atual com as mais recentes atualizações e funcionalidades. Esta funcionalidade utiliza uma função do sistema de site chamada ponto de ligação de serviço. Escolha o servidor onde instalar esta função. 

Para obter mais informações sobre informações recolhidas e como é utilizada, consulte [os dados de utilização.](#usage-data)



## <a name="usage-data"></a>Dados de utilização

O Gestor de Configuração recolhe dados de diagnóstico e utilização sobre si mesmo, que a Microsoft utiliza para melhorar a experiência de instalação, qualidade e segurança de futuras versões.
Os diagnósticos e os dados de utilização estão ativados para cada hierarquia do Gestor de Configuração. É composto por consultas do SQL Server que funcionam semanalmente em cada site primário e no site da administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de alto nível da sua hierarquia, o ponto de ligação de serviço submete esta informação quando verifica as atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.

O Gestor de Configuração recolhe dados apenas a partir da base de dados do servidor SQL do site, e não recolhe dados diretamente de clientes ou servidores do site.

Os administradores podem alterar o nível de dados recolhidos indo para a secção de Dados de **Utilização** da consola Do Gestor de Configuração.

Para obter mais informações sobre os níveis e configurações de dados de utilização, consulte [diagnósticos e dados](../diagnostics/diagnostics-and-usage-data.md)de utilização .



## <a name="log-analytics-connector"></a>Conector de análise de log

O Conector Log Analytics sincroniza dados, tais como coleções, desde o Gestor de Configuração até ao serviço de nuvem Azure. O ID de subscrição Azure e a chave secreta são armazenados na base de dados do Gestor de Configuração quando um administrador configura a funcionalidade. Tanto o segredo do cliente do Azure Ative Directory como a chave partilhada do espaço de trabalho Azure estão armazenados na base de dados do Gestor de Configuração no local. Todas as comunicações entre O Gestor de Configuração e o Azure utilizam https. Não são fornecidas informações adicionais sobre as coleções à Microsoft fora dos diagnósticos aleatórios e dados de utilização. 

Para obter mais informações sobre as informações que o Log Analytics recolhe, consulte a [segurança dos dados de análise de registo](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

A Inteligência de Ativos permite que os administradores definam, rastreiem e gerem proativamente a conformidade com os padrões de configuração. A medição e elaboração de relatórios relativamente à implementação e utilização de aplicações físicas e virtuais permitem que as empresas tomem decisões comerciais mais corretas em termos de licenciamento de software e mantenham a compatibilidade com os contratos de licenciamento. Depois de recolher dados de utilização de clientes do Gestor de Configuração, pode utilizar diferentes funcionalidades para visualizar os dados, incluindo coleções, consultas e reportagens.

Durante cada sincronização, um catálogo de software conhecido é descarregado da Microsoft. Pode optar por enviar informações da Microsoft sobre títulos de software não categorizados que são descobertos dentro da sua organização para serem pesquisados e adicionados ao catálogo. Antes de enviar esta informação, uma caixa de diálogo mostra dados que vão ser carregados. Os dados enviados não podem ser recolhidos. A Asset Intelligence não envia informações sobre utilizadores e computadores ou utilização de licenças para a Microsoft.

Depois de um título de software ser carregado, os investigadores da Microsoft identificam, categorizam e depois disponibilizam esse conhecimento a todos os outros clientes que utilizam esta funcionalidade e a outros consumidores do catálogo. Qualquer título de software carregado torna-se público. A aplicação e a sua categorização tornam-se parte do catálogo e depois podem ser transferidas para outros consumidores do catálogo. Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para a Microsoft, tenha em consideração os requisitos de privacidade da sua empresa.

A Inteligência de Ativos não é ativada por padrão no Gestor de Configuração. O upload de títulos não categorizados nunca ocorre automaticamente, e o sistema não foi concebido para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.



## <a name="endpoint-protection"></a>Endpoint Protection

O Microsoft Cloud Protection Service era anteriormente conhecido como Microsoft Ative Protection Service ou MAPS.

Os produtos aplicáveis são a Proteção de Pontofinal do System Center e a funcionalidade de proteção de pontos finais do Gestor de Configuração (para gerir a Proteção de Pontofinal do Centro de Sistema e o Windows Defender para o Windows 10). Esta funcionalidade não é implementada para proteção de ponto final do System Center para o Linux ou para a Proteção de Pontofinal do Centro de Sistema para Mac.

A comunidade antimalware do Microsoft Cloud Protection Service é uma comunidade online voluntária em todo o mundo que inclui utilizadores de Proteção de Endpoint do System Center. Quando se junta ao Microsoft Cloud Protection Service, o System Center Endpoint Protection envia automaticamente informações para a Microsoft. A Microsoft utiliza a informação para determinar o software para investigar potenciais ameaças e para ajudar a melhorar a eficácia da Proteção do Ponto Final do System Center. Esta comunidade ajuda a parar a propagação de novas infeções de software malicioso. Se um relatório do Microsoft Cloud Protection Service incluir detalhes sobre malware ou software potencialmente indesejado que o cliente endpoint Protection possa remover, o Microsoft Cloud Protection Service descarrega a mais recente assinatura para o resolver. O Microsoft Cloud Protection Service também pode encontrar "falsos positivos" e corrigi-los. (Falsos positivos são onde algo originalmente identificado como malware acaba por não ser.) 

Os relatórios do Microsoft Cloud Protection Service incluem informações sobre potenciais ficheiros de malware, como nomes de ficheiros, hash criptográfico, fornecedor, tamanho e selos de data. Além disso, o Microsoft Cloud Protection Service poderá recolher URLs completos para indicar a origem do ficheiro. Estes URLs podem ocasionalmente ter informações pessoais como termos de pesquisa ou dados que foram introduzidos em formulários. Os relatórios também podem incluir ações que tomou quando endpoint Protection o notificou sobre software indesejado. Os relatórios do Microsoft Cloud Protection Service incluem estas informações para ajudar a Microsoft a avaliar a eficácia da Proteção endpoint pode detetar e remover malware e software potencialmente indesejado e tentar identificar novos malwares.

Pode aderir ao Microsoft Cloud Protection Service se tiver uma adesão básica ou avançada. Os relatórios básicos dos membros têm as informações descritas anteriormente. Os relatórios avançados dos membros são mais abrangentes e podem incluir detalhes adicionais sobre o software que a Endpoint Protection deteta, como a localização de tal software, nomes de ficheiros, como o software funciona e como afetou o seu computador. Estes relatórios e relatórios de outros utilizadores da Endpoint Protection que participam no Microsoft Cloud Protection Service ajudam os investigadores da Microsoft a descobrir novas ameaças mais rapidamente. As definições de malware são então criadas para programas que satisfaçam os critérios de análise, e as definições atualizadas são disponibilizadas a todos os utilizadores através do Microsoft Update.

Para ajudar a detetar e corrigir certos tipos de infeções por malware, o produto envia regularmente informações do Microsoft Cloud Protection Service sobre o estado de segurança do seu PC. Estas informações incluem informações sobre as definições de segurança do seu PC e ficheiros de registo que descrevem os controladores e outros softwares que carregam enquanto as suas botas para PC.

Um número que identifica exclusivamente o seu PC também é enviado. Além disso, o Microsoft Cloud Protection Service poderá recolher os endereços IP a que os potenciais ficheiros de malware se ligam.

Os relatórios do Microsoft Cloud Protection Service são usados para melhorar o software e os serviços da Microsoft. Os relatórios podem também ser utilizados para fins estatísticos ou outros ensaios ou analíticos e para gerar definições. Apenas os colaboradores da Microsoft, empreiteiros, parceiros e fornecedores que tenham um negócio precisam de usar os relatórios podem aceder-lhes.

O Microsoft Cloud Protection Service não recolhe intencionalmente informações pessoais. Na medida em que o Microsoft Cloud Protection Service recolhe quaisquer informações pessoais, a Microsoft não utiliza as informações para o identificar ou contactar.

Para mais informações, consulte [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do site – vista geográfica com Bing Maps

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** selecione o nó **da Hierarquia** do Site e mude para a Vista **Geográfica**. Esta vista permite-lhe utilizar mapas que o Microsoft Bing Maps fornece para visualizar a topologia do seu servidor físico do Gestor de Configuração. Para ativar esta funcionalidade, as informações de localização que fornece são enviadas do seu servidor para o serviço Web Bing Maps.

A Microsoft utiliza as informações para explorar e melhorar o Microsoft Bing Maps e outros serviços e sites da Microsoft. Para mais informações, consulte a [Declaração de Privacidade](https://privacy.microsoft.com/privacystatement)da Microsoft .

Pode optar por não utilizar a Vista Geográfica da Hierarquia do Site. A visão padrão do Diagrama da Hierarquia permite-lhe ver a hierarquia e não utiliza o serviço Bing Maps.
