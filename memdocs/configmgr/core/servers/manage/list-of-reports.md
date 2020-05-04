---
title: Lista de relatórios
titleSuffix: Configuration Manager
description: Reveja uma lista de relatórios fornecidos com O Gestor de Configuração. Os relatórios são apresentados em várias categorias.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713766"
---
# <a name="list-of-reports-in-configuration-manager"></a>Lista de relatórios no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração fornece muitos relatórios incorporados que cobrem muitas das tarefas de reporte que você pode querer fazer. Também pode utilizar as instruções SQL nestes relatórios para ajudá-lo a escrever os seus próprios relatórios.   

Os seguintes relatórios estão incluídos no Gestor de Configuração. Os relatórios são apresentados em várias categorias.  



## <a name="administrative-security"></a>Segurança administrativa  

Os seis relatórios seguintes constam da categoria **de Segurança Administrativa.**  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Registo de atividade de administrativa**|Apresenta um registo de alterações administrativas efetuadas para utilizadores administrativos, funções de segurança, âmbitos de segurança e coleções.|  
|**Atribuições de segurança dos utilizadores administrativos**|Mostra utilizadores administrativos, os respetivos direitos de acesso associados e os âmbitos de segurança associados a cada direito de acesso de cada utilizador.|  
|**Objetos protegidos por um único âmbito de segurança**|Exibe objetos que um administrador atribuiu apenas ao âmbito de segurança especificado. Este relatório não apresenta objetos que um administrador associa com mais de um âmbito de segurança.|  
|**Segurança para um ou múltiplos objetos do Configuration Manager**|Mostra objetos com capacidade de segurança, os âmbitos de segurança associados aos objetos e os utilizadores administrativos com acesso aos objetos.|  
|**Resumo das funções de segurança**|Apresenta funções de segurança e administradores do Gestor de Configuração associados a cada função.|  
|**Resumo dos âmbitos de segurança**|Apresenta âmbitos de segurança e os utilizadores administrativos do Gestor de Configuração e grupos de segurança associados a cada âmbito.|  



## <a name="alerts"></a>Alertas  

Os dois relatórios seguintes constam da categoria **Alertas.**  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Tabela de indicadores de alertas**|Mostra um resumo de todos os alertas adiados que foram gerados entre o início especificado e a data de conclusão.|  
|**Alertas Gerados Mais Frequentemente**|Mostra um resumo dos alertas gerados mais frequentemente entre o dia de hoje e a data anterior especificada na área de função especificada.|  



## <a name="asset-intelligence"></a>Asset Intelligence  

Os seguintes 67 relatórios estão listados na categoria De Inteligência de **Ativos.**  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Hardware 01A - resumo de computadores numa coleção específica**|Mostra uma vista de resumo de Asset Intelligence dos computadores numa coleção especificada por si.|  
|**Hardware 03A - utilizadores primários do computador**|Exibe os utilizadores e a contagem de computadores em que são o utilizador principal.|  
|**Hardware 03B - computadores com um utilizador primário específico da consola**|Mostra todos os computadores em que um utilizador especificado é o utilizador primário da consola.|  
|**Hardware 04A - computadores com vários utilizadores (partilhados)**|Exibe computadores que não têm um utilizador primário porque nenhum utilizador tem um tempo de início de sinuoso superior a 66%.|  
|**Hardware 05A - utilizadores de consola num computador específico**|Mostra todos os utilizadores da consola num computador especificado.|  
|**Hardware 06A - computadores para os quais não foi possível determinar os utilizadores de consola**|Ajuda os utilizadores administrativos a identificar computadores que têm de ter o registo de segurança ativado.|  
|**07A - dispositivos USB por fabricante**|Mostra os dispositivos USB agrupados por fabricante.|  
|**Hardware 07B - dispositivos USB por fabricante e descrição**|Mostra os dispositivos USB agrupados por fabricante e descrição.|  
|**Hardware 07C - computadores com um dispositivo USB específico**|Mostra todos os computadores com um dispositivo USB especificado.|  
|**Hardware 07D - dispositivos USB num computador específico**|Mostra todos os dispositivos USB num computador especificado.|  
|**Hardware 08A - hardware que não está pronto para uma atualização de software**|Exibe hardware que não cumpre os requisitos mínimos de hardware.|  
|**Hardware 09A - procurar computadores**|Apresenta um resumo de computadores que combinam filtros de palavras-chave. Estes filtros são nome de computador, site de Configuração, domínio, utilizador de consola superior, sistema operativo, fabricante ou modelo.|  
|**Hardware 10A - computadores numa coleção especificada que foram alterados durante um período de tempo especificado**|Mostra uma lista de computadores numa coleção especificada onde uma classe de hardware foi alterada durante um período de tempo especificado.|  
|**Hardware 10B - alterações num computador especificado durante um período de tempo especificado**|Mostra as classes alteradas num computador especificado durante um período de tempo especificado.|  
|**Licença 01A - ledger de Licenciamento em Volume da Microsoft para instruções de licença Microsoft**|Mostra um inventário de todos os títulos de software da Microsoft que estão disponíveis no programa de Licenciamento em Volume da Microsoft.|  
|**Licença 01B - item de ledger de Licenciamento em Volume da Microsoft por canal de vendas**|Identifica e mostra o canal de vendas para software Microsoft Volume Licensing inventariado.|  
|**Licença 01C - computadores com um item de ledger de Licenciamento em Volume da Microsoft específico e canal de vendas**|Identifica e mostra os computadores com um item especificado a partir do ledger de licenciamento em Volume da Microsoft.|  
|**Licença 01D - produtos de ledger de Licenciamento em Volume da Microsoft num computador específico**|Identifica e mostra todos os itens de ledger de Licenciamento em Volume da Microsoft num computador especificado.|  
|**Licença 02A - contagem de licenças prestes a expirar por intervalos de tempo**|Mostra uma contagem das licenças prestes a expirar por um intervalo de tempo especificado. Os produtos apresentados têm as suas licenças geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 02B - computadores com licenças prestes a expirar**|Mostra os computadores especificados com licenças prestes a expirar.|  
|**Licença 02C - informações de licença num computador específico**|Mostra os produtos num computador especificado cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 03A - contagem de licenças por estado de licença**|Mostra os produtos, por estado de licença, cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 03B - computadores com um estado específico de licença**|Mostra os produtos, com um estado de licença especificado, cujas licenças são geridas pelo serviço de licenciamento de Software.|  
|**Licença 04A - contagem de produtos geridos pelo licenciamento de software**|Mostra uma contagem de produtos cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 04B - computadores com um produto específico geridos pelo Serviço de Licenciamento de Software**|Exibe computadores, geridos pelo Serviço de Licenciamento de Software, que incluem um produto especificado.|  
|**Licença 05A - computadores que fornecem o Serviço De Gestão De Chaves**|Mostra os computadores que atuam como Servidores de Gestão de Chaves.|  
|**Licença 06A - contagens de processador para produtos licenciados por processador**|Mostra o número de processadores em computadores com produtos Microsoft que suportam o licenciamento por processador.|  
|**Licença 06B - computadores com um produto específico que suporta o licenciamento por processador**|Mostra uma lista dos computadores onde um produto Microsoft especificado que suporta o licenciamento por processador está instalado.|  
|**Licença 14A - relatório de reconciliação de Licenciamento em Volume da Microsoft**|Apresenta a reconciliação nas licenças de software adquiridas através do Microsoft Volume License Agreement e na contagem real de inventário.|  
|**Licença 14B - lista do inventário de software da Microsoft não encontrado no Contrato de Licenciamento em Volume da Microsoft**|Este relatório exibe títulos de software da Microsoft em uso que não estão encontrados no Microsoft Volume License Agreement.|  
|**License 15A - relatório de reconciliação de licenças gerais**|Exibe a reconciliação nas licenças gerais de software adquiridas e na contagem real de inventários.|  
|**License 15B - relatório de reconciliação de licenças gerais por computador**|Mostra os computadores com o produto licenciado com uma versão especificada instalado.|  
|**Software 01A - resumo do software instalado numa coleção específica**|Mostra um resumo do software instalado ordenado pelo número de instâncias encontradas no inventário.|  
|**Software 02A - famílias de produtos para uma coleção específica**|Mostra as famílias de produtos e a contagem de software na família para uma coleção especificada.|  
|**Software 02B - categorias de produto para uma família específica de produtos**|Mostra as categorias de produtos numa família de produto especificada e a contagem de software na categoria.|  
|**Software 02C - software numa família e categoria específica de produtos**|Mostra todos os softwares que se encontram na categoria e família de produtos especificadas.|  
|**Software 02D - computadores com software específico instalado**|Mostra todos os computadores com um software especificado instalado.|  
|**Software 02E - software instalado num computador específico**|Mostra todos os softwares instalados num computador especificado.|  
|**Software 03A - software sem categoria**|Mostra o software categorizado como desconhecido ou sem categorização.|  
|**Software 04A - software configurado para ser executado automaticamente em computadores**|Mostra uma lista do software configurado para ser executado automaticamente em computadores.|  
|**Software 04B - computadores com software específico configurado para ser executado automaticamente**|Mostra todos os computadores com software específico configurado para ser executado automaticamente.|  
|**Software 04C - software configurado para ser executado automaticamente num computador específico**|Mostra o software instalado que está configurado para ser executado automaticamente num computador especificado.|  
|**Software 05A - Objetos de Programa Auxiliar de Browser**|Exibe os objetos auxiliares do navegador instalados em computadores numa coleção especificada.|  
|**Software 05B - computadores com um Objeto de Programa Auxiliar de Browser específico**|Exibe todos os computadores com um objeto de ajuda de navegador especificado.|  
|**Software 05C - Objetos de Programa Auxiliar de Browser num computador específico**|Exibe todos os objetos auxiliares do navegador no computador especificado.|  
|**Software 06A - procurar software instalado**|Este relatório fornece um resumo do software instalado. Procura com base nos seguintes critérios: nome do produto, editor ou versão.|  
|**Software 06B - software por nome de produto**|Apresenta um resumo do software instalado com base num nome de produto especificado.|  
|**Software 07A - programas executáveis utilizados recentemente pela contagem de computadores**|Exibe programas executáveis que os utilizadores utilizaram recentemente. Inclui também a contagem de computadores em que os utilizadores utilizaram o programa. Para ver este relatório, a medição de software deve estar ativada para este site.|  
|**Software 07B - computadores que utilizaram recentemente um programa executável especificado**|Exibe os computadores nos quais os utilizadores utilizaram recentemente um programa executável especificado. Este relatório requer que permita a definição de cliente de medição de software.|  
|**Software 07C - programas executáveis utilizados recentemente num computador específico**|Apresenta ficheiros executáveis que os utilizadores usaram recentemente num computador especificado. Este relatório requer que permita a definição de cliente de medição de software.|  
|**Software 08A - programas executados recentemente pela contagem de utilizadores**|Exibe programas executáveis que os utilizadores utilizaram recentemente. Inclui também uma contagem de utilizadores que mais recentemente utilizaram o programa. Este relatório requer que permita a definição de cliente de medição de software.|  
|**Software 08B - utilizadores que utilizaram recentemente um programa executável especificado**|Exibe os utilizadores que mais recentemente utilizaram um programa executável especificado. Este relatório requer que permita a definição de cliente de medição de software.|  
|**Software 08C - programas executáveis utilizados recentemente por um utilizador especificado**|Apresenta programas executáveis que o utilizador especificado utilizou recentemente. Este relatório requer que permita a definição de cliente de medição de software.|  
|**Software 09A - software raramente utilizado**|Exibe títulos de software que os utilizadores não utilizaram durante um determinado período de tempo.|  
|**Software 09B - computadores com software raramente utilizado instalado**|Exibe computadores com software instalado que os utilizadores não utilizaram durante um determinado período de tempo. O período de tempo especificado é baseado no valor especificado no relatório " Software 09A - Software raramente utilizado".|  
|**Software 10A - títulos de software com várias etiquetas personalizadas específicas definidas**|Mostra os títulos de software com base na correspondência de todos os critérios das etiquetas personalizadas especificadas. Pode selecionar até três etiquetas personalizadas para refinar uma pesquisa de títulos de software.|  
|**Software 10B - computadores com um título de software com etiqueta personalizada específico instalado**|Mostra todos os computadores nesta coleção que têm o título de software com etiqueta personalizada especificado instalado.|  
|**Software 11A - títulos de software com uma etiqueta personalizada específica definida**|Mostra os títulos de software com base na correspondência de, pelo menos, um dos critérios especificados da etiqueta personalizada.|  
|**Software 12A - títulos de software sem uma etiqueta personalizada**|Exibe todos os títulos de software que não têm uma etiqueta personalizada definida.|  
|**Software 14A - procurar software ativado por etiqueta de identificação de software**|Mostra a contagem do software instalado com uma etiqueta de identificação de software ativada.|  
|**Software 14B - computadores com software instalado com uma etiqueta de identificação de software específica ativada**|Mostra todos os computadores com software instalado com uma etiqueta de identificação de software especificada ativada.|  
|**Software 14C - software instalado com uma etiqueta de identificação de software num computador específico**|Mostra todos os softwares instalados com uma etiqueta de identificação de software especificada ativada num computador especificado.|  
|**Lifecycle 01A - Computadores com um produto de software específico**|Ver uma lista de computadores em que é detetado um produto especificado.|
|**Lifecycle 02A - Lista de máquinas com produtos caducados na organização**|Veja computadores que tenham expirado os produtos neles. Pode filtrar este relatório pelo nome do produto.|
|**Lifecycle 03A - Lista de produtos caducados encontrados na organização**|Consulte detalhes sobre produtos no seu ambiente que tenham datas de ciclo de vida expiradas.|
|**Lifecycle 04A - Visão geral do ciclo de vida do produto**|Veja uma lista de ciclos de vida do produto. Filtre a lista pelo nome do produto e dias até à expiração.|
|**Lifecycle 05A - Painel de instrumentos de ciclo de vida do produto**|A partir da versão 1810, este relatório inclui informações semelhantes às do painel de instrumentos na consola.|



## <a name="client-push"></a>Impulso do cliente  

Os quatro relatórios seguintes estão listados na categoria Push do **Cliente.**  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Detalhes do estado da instalação push do cliente**|Mostra as informações sobre o processo da instalação push do cliente para todos os sites.|  
|**Detalhes do estado da instalação push do cliente para um site especificado**|Mostra as informações sobre o processo da instalação push do cliente para um site especificado.|  
|**Resumo do estado da instalação push do cliente**|Mostra uma vista de resumo do estado da instalação push do cliente para todos os sites.|  
|**Resumo do estado da instalação push do cliente para um site especificado**|Mostra uma vista de resumo do estado da instalação push do cliente para um site especificado.|  



## <a name="client-status"></a>Estado do cliente  

Os seguintes sete relatórios estão listados na categoria **Estado do Cliente.**  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Detalhes de remediação do cliente**|Mostra os detalhes de remediação do cliente para uma coleção que especificar.|  
|**Resumo da remediação do cliente**|Mostra um resumo das ações de remediação do cliente para uma coleção especificada.|  
|**Histórico do estado de cliente**|Mostra uma apresentação do histórico do estado geral de cliente no site.|  
|**Resumo do estado de cliente**|Mostra os resultados da verificação de clientes ativos para uma coleção específica.|  
|**Pedido do cliente para efetuar um pedido de política**|Exibe a percentagem de clientes que solicitaram a apólice pelo menos uma vez nos últimos 30 dias. Cada dia representa uma percentagem do total de clientes que solicitaram a política desde o primeiro dia do ciclo.|  
|**Clientes com detalhes de verificação de cliente falhada**|Mostra os detalhes sobre clientes cuja verificação de cliente falhou numa coleção especificada.|  
|**Detalhes de clientes inativos**|Mostra uma lista detalhada dos clientes inativos para uma determinada coleção.|  



## <a name="company-resource-access"></a>Acesso aos recursos da empresa  

Os três relatórios seguintes constam da categoria de Acesso a Recursos da **Empresa.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico de emissão de certificados**|Apresenta o histórico de certificados emitidos pelo ponto de registo do certificado aos utilizadores e dispositivos para a gama de datas especificada.|  
|**Lista de recursos por estado de emissão de certificados**|Mostra os utilizadores ou dispositivos num estado de emissão de certificados especificado depois da avaliação de um perfil de certificado especificado.|  
|**Lista de recursos com certificados prestes a expirar**|Mostra os dispositivos ou utilizadores com certificados que expiram na data especificada ou antes.|  



## <a name="compliance-and-settings-management"></a>Gestão de conformidade e configurações  

Os seguintes 22 relatórios estão listados na categoria **Compliance and Settings Management.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico de conformidade de uma linha de base da configuração**|Mostra o histórico de alterações da conformidade de uma linha de base da configuração no período de tempo especificado.|  
|**Histórico de conformidade de um item de configuração**|Mostra o histórico de alterações da conformidade de um item de configuração no período de tempo especificado.|  
|**Detalhes de regras de compatibilidade dos itens de configuração numa linha de base da configuração para um recurso**|Apresenta informações sobre as regras avaliadas como conformes para um determinado item de configuração para um dispositivo ou utilizador especificado.|  
|**Detalhes das regras dos itens de configuração em conflito numa linha de base da configuração para um recurso**|Exibe informações sobre regras num item de configuração implementado que entram em conflito com outras regras. Inclua as outras regras no mesmo ou noutro item de configuração implantado.|  
|**Detalhes de erros de itens de configuração numa linha de base da configuração para um recurso**|Mostra informações sobre erros gerados por um item de configuração especificado num dispositivo ou utilizador especificado.|  
|**Detalhes de regras de incompatibilidade de itens de configuração numa linha de base da configuração para um recurso**|Mostra informações sobre regras que foram consideradas incompatíveis para um item de configuração especificado, para um dispositivo ou utilizador especificado.|  
|**Detalhes de regras remediadas de itens de configuração numa linha de base da configuração para um recurso**|Mostra informações sobre regras que foram remediadas por um item de configuração especificado para um dispositivo ou utilizador especificado.|  
|**Lista de recursos por estado de conformidade para uma linha de base da configuração**|Mostra os utilizadores ou dispositivos num estado de conformidade especificado depois da avaliação de uma linha de base da configuração especificada.|  
|**Lista de recursos por estado de conformidade para um item de configuração numa linha de base de configuração**|Mostra os dispositivos ou utilizadores num estado de conformidade especificado depois da avaliação de um item de configuração especificado.|  
|**Lista de Aplicações e Dispositivos não compatíveis para utilizadores específicos**|Exibe informações sobre utilizadores e dispositivos que tenham aplicações instaladas que não estejam em conformidade com uma política que especificou.|  
|**Lista das regras em conflito com uma regra especificada para um recurso**|Apresenta uma lista de regras que entram em conflito com uma regra especificada para um item de configuração implantado.|  
|**Lista de recursos desconhecidos para uma linha de base da configuração**|Apresenta uma lista de dispositivos ou utilizadores que ainda não reportaram quaisquer dados de conformidade para uma linha de base de configuração especificada.|  
|**Lista de recursos desconhecidos para uma linha de base de configuração**|Apresenta uma lista de dispositivos ou utilizadores que ainda não reportaram quaisquer dados de conformidade para um determinado item de configuração.|  
|**Resumo de regras e erros de itens de configuração numa linha de base da configuração para um recurso**|Apresenta um resumo do estado de conformidade das regras e de quaisquer erros de definição para um determinado item de configuração. O item de configuração deve ser implantado num dispositivo ou utilizador.|  
|**Resumo de conformidade por linha de base da configuração**|Mostra um resumo da conformidade geral das linhas de bases da configuração implementadas na hierarquia.|  
|**Resumo de conformidade por itens de configuração para uma linha de base da configuração**|Mostra um resumo da conformidade dos itens de configuração numa linha de base da configuração especificada.|  
|**Resumo de conformidade por políticas de configuração**|Mostra um resumo da conformidade das políticas de configuração.|  
|**Resumo de conformidade de uma linha de base da configuração para uma coleção**|Apresenta um resumo da conformidade geral de uma linha de base de configuração especificada. O item de configuração deve ser implantado na recolha especificada.|  
|**Resumo dos Utilizadores que têm Aplicações Não Compatíveis**|Exibe informações sobre utilizadores que tenham apps instaladas que não estejam em conformidade com uma política que especificou.|  
|**Aceitar os Termos e Condições**|Apresenta os itens de Termos e Condições e que versão foi aceite por cada utilizador.|  



## <a name="data-warehouse"></a>Armazém de dados  

Os seguintes sete relatórios constam da categoria **data warehouse.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Implementação de Aplicação**|Histórico: Veja detalhes para a implementação de aplicações para uma aplicação e máquina específicas.|
|**Conformidade com a proteção de pontos finais e a tualização de software**|Histórico: Ver computadores que faltam atualizações de software.|
|**Inventário Geral de Hardware**|Histórico: Veja todo o inventário de hardware para uma máquina específica.|
|**Inventário Geral de Software**|Histórico: Veja todo o inventário de software para uma máquina específica.|
|**Visão geral da saúde das infraestruturas**|Histórico: Exibe uma visão geral da saúde da sua infraestrutura de Gestor de Configuração.|
|**Lista de Malware Detetado**|Histórico: Veja o malware que foi detetado na organização.|
|**Resumo da Distribuição de Software**|Histórico: Um resumo da distribuição de software para um anúncio e máquina específicos.|


## <a name="device-management"></a>Gestão de dispositivos  

Os seguintes 37 relatórios estão listados na categoria **gestão** de dispositivos. 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os dispositivos móveis corporativos**|Exibe todos os dispositivos móveis corporativos.|
|**Todos os clientes de dispositivos móveis**|Mostra informações sobre todos os clientes de dispositivos móveis. Os dispositivos que são geridos pelo conector Exchange Server não estão incluídos.|  
|**Problemas de certificadoem dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para windows CE e que não são saudáveis**|Apresenta informações detalhadas sobre problemas de certificados em dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Falha na implementação do cliente para dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para windows CE**|Apresenta informações detalhadas sobre falha de implementação de dispositivos móveis que são geridas pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Detalhes do estado de implementação do cliente para dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para windows CE**|Exibe informações sobre o estado dos dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Êxito da implementação do cliente em dispositivos móveis geridos pelo cliente do Configuration Manager para o Windows CE**|Apresenta informações detalhadas sobre o sucesso da implementação de dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Problemas de comunicação em dispositivos móveis geridos pelo cliente do Configuration Manager para o Windows CE e que não estão em bom estado de funcionamento**|Este relatório contém informações detalhadas sobre problemas de comunicação em dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Estado de conformidade da política de caixa de correio ActiveSync padrão para os dispositivos móveis que são geridos pelo conector Exchange Server**|Apresenta um resumo do estado de conformidade com a política de caixa de correio Default Exchange ActiveSync para os dispositivos móveis geridos pelo conector Exchange Server.|  
|**Contagem de dispositivos móveis por configurações de visualização**|Este relatório mostra o número de dispositivos móveis por definições de visualização.|  
|**Contagem de dispositivos móveis por sistema operativo**|Este relatório mostra o número de dispositivos móveis por sistema operativo.|  
|**Contagem de dispositivos móveis por memória de programa**|Este relatório mostra o número de dispositivos móveis por memória de programa.|  
|**Contagem de dispositivos móveis por configurações da memória de armazenamento**|Contagem de dispositivos móveis por configurações da memória de armazenamento|  
|**Informações sobre o estado de funcionamento dos dispositivos móveis geridos pelo cliente do Configuration Manager para o Windows CE**|Apresenta informações detalhadas sobre saúde para dispositivos móveis que são geridas pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Resumo do estado de funcionamento dos dispositivos móveis geridos pelo cliente do Configuration Manager para o Windows CE**|Apresenta informações de resumo de saúde para dispositivos móveis que são geridas pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Dispositivos móveis inativos geridos pelo conector do Exchange Server**|Apresenta os dispositivos móveis geridos pelo conector Exchange Server que não ligaram a um Servidor de Câmbio num número determinado de dias.|  
|**Lista de dispositivos por Estado da Atesta de Saúde**|Apresenta uma lista de dispositivos com atributos relatados pelo Serviço de Atestados de Saúde|
|**Lista de Dispositivos inscritos por utilizador no Microsoft Intune**|Exibe todos os dispositivos que um utilizador inscreveu no Microsoft Intune.|  
|**Lista de dispositivos numa categoria específica de dispositivos**|Apresenta informações para todos os dispositivos dentro de uma categoria específica do dispositivo.|
|**Problemas do cliente local em dispositivos móveis geridos pelo cliente do Configuration Manager para o Windows CE e que não estão em bom estado de funcionamento**|Este relatório contém informações detalhadas sobre problemas de clientes locais em dispositivos móveis que são geridos pelo cliente do Gestor de Configuração para o Windows CE.|  
|**Informações de cliente de dispositivos móveis**|Exibe informações sobre os dispositivos móveis que têm o cliente do Gestor de Configuração instalado. Pode utilizar este relatório para verificar que dispositivos móveis conseguem comunicar com um ponto de gestão com êxito.|  
|**Detalhes de conformidade do dispositivo móvel para o conector do Exchange Server**|Mostra os detalhes da conformidade do dispositivo móvel para uma política de caixa de correio predefinida do Exchange ActiveSync, configurada com o conector do Exchange Server.|  
|**Dispositivos móveis por sistema operativo**|Mostra os dispositivos móveis por sistema operativo.|  
|**Dispositivos móveis desbloqueados por jailbreak ou rooting**|Mostra os dispositivos móveis desbloqueados com jailbreak ou rooting.|  
|**Dispositivos móveis sem gestão porque concluíram a inscrição, mas que não concluíram a atribuição de site**|Os ecrãs dos dispositivos móveis que completaram a inscrição com o Gestor de Configuração, têm um certificado, mas não completaram a atribuição do site.|  
|**Dispositivos móveis com uma quantidade específica de memória de programa livre**|Mostra todos os dispositivos móveis com a quantidade especificada de memória de programa livre.|  
|**Dispositivos móveis com uma quantidade específica de memória de armazenamento amovível livre**|Mostra todos os dispositivos móveis com a quantidade especificada de memória de armazenamento amovível livre.|  
|**Dispositivos móveis com problemas de renovação de certificado**|Mostra os dispositivos móveis inscritos cuja renovação de certificado falhou. Se não renovar o certificado antes do termo, os dispositivos móveis ficam desgeridos.|  
|**Dispositivos móveis com pouco espaço livre na memória do programa (inferior a um tamanho em KB especificado)**|Mostra os dispositivos móveis com memória de programa inferior a um tamanho em KB especificado.|  
|**Dispositivos móveis com pouco espaço livre na memória de armazenamento amovível (inferior a um tamanho em KB especificado)**|Mostra os dispositivos móveis com memória de armazenamento amovível inferior a um tamanho em KB especificado.|  
|**Número de dispositivos matriculados por utilizador no Microsoft Intune**|Apresenta os utilizadores ativados para a subscrição Microsoft Intune. Mostra também o número total de dispositivos matriculados para cada utilizador.|  
|**Pendente de aposentação e pedido de limpeza de dispositivos móveis**|Mostra os pedidos para a ação apagar pendentes para dispositivos móveis.|  
|**Dispositivos móveis inscritos e atribuídos recentemente**|Exibe dispositivos móveis que recentemente se inscreveram no Gestor de Configuração e que foram atribuídos com sucesso a um site.|  
|**Dispositivos móveis apagados recentemente**|Mostra a lista de dispositivos móveis apagados com êxito recentemente.|  
|**Resumo das definições para os dispositivos móveis geridos pelo conector do Exchange Server**|Apresenta o número de dispositivos móveis que aplicam as definições para cada política de caixa de correio Default Exchange ActiveSync gerida pelo conector Exchange Server.|  
|**Estado Detalhado das Chaves de Sideload do Windows RT**|Mostra informações de estado detalhadas para uma chave de sideload especificada do Windows RT.|  
|**Resumo das Chaves de Sideload do Windows RT**|Mostra o estado das chaves de sideload do Windows RT.|  



## <a name="driver-management"></a>Gestão do condutor  

Os seguintes 13 relatórios constam da categoria **gestão do condutor.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os controladores**|Mostra a lista de todos os controladores.|  
|**Todos os controladores de uma plataforma específica**|Mostra todos os controladores de uma plataforma especificada.|  
|**Todos os controladores numa imagem de arranque específica**|Mostra todos os controladores numa imagem de arranque especificada.|  
|**Todos os controladores numa categoria específica**|Mostra todos os controladores numa categoria especificada.|  
|**Todos os controladores num pacote específico**|Mostra todos os controladores num pacote especificado.|  
|**Categorias para um controlador específico**|Mostra as categorias para um controlador especificado.|  
|**Computadores nos quais ocorreu um erro ao instalar os controladores para uma coleção específica**|Mostra os computadores nos quais ocorreu um erro ao instalar os controladores para uma coleção especificada.|  
|**Relatório de correspondência do catálogo de controladores de uma coleção específica**|Mostra o relatório de correspondência do catálogo de controladores de uma coleção especificada.|  
|**Relatório de correspondência do catálogo de controladores de um computador específico**|Mostra o relatório de correspondência do catálogo de controladores de um computador especificado.|  
|**Relatório de correspondência do catálogo de controladores de um dispositivo específico num computador específico**|Mostra o relatório de correspondência do catálogo de controladores de um dispositivo especificado num computador especificado.|  
|**Relatório de correspondência do catálogo de controladores de computadores numa coleção específica com um dispositivo específico**|Mostra o relatório de correspondência do catálogo de controladores de computadores numa coleção especificada com um dispositivo especificado.|  
|**Controladores cuja instalação falhou num computador específico**|Mostra os controladores cuja instalação falhou num computador especificado.|  
|**Plataformas suportadas por um controlador específico**|Mostra as plataformas suportadas por um controlador especificado.|  



## <a name="endpoint-protection"></a>Endpoint Protection  

Os seis relatórios seguintes constam da categoria de Proteção do **Ponto Final.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de atividade antimalware**|Mostra uma descrição geral da atividade antimalware.|  
|**Descrição geral do estado e histórico da atividade antimalware**|Mostra uma descrição geral do estado e histórico da atividade antimalware.|  
|**Detalhes do software maligno do computador**|Mostra detalhes sobre um computador especificado e a lista de software maligno encontrado no mesmo.|  
|**Computadores infetados**|Mostra uma lista de computadores com uma ameaça especificada detetada.|  
|**Utilizadores de topo por ameaças**|Mostra a lista de utilizadores com o maior número de ameaças detetadas.|  
|**Lista de ameaças ao utilizador**|Mostra a lista de ameaças encontradas para uma conta de utilizador especificada.|  



## <a name="hardware---cd-rom"></a>Hardware - CD-ROM  

Os quatro relatórios seguintes estão listados na categoria **Hardware - CD-ROM.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações de CD-ROM relativamente a computador específico**|Mostra informações sobre as unidades de CD-ROM num computador especificado.|  
|**Computadores com um fabricante de CD-ROM específico**|Mostra uma lista dos computadores com uma unidade de CD-ROM criada por um fabricante especificado por si.|  
|**Contagem de unidades CD-ROM por fabricante**|Mostra o número de unidades CD-ROM inventariadas por fabricante.|  
|**História - História do CD-ROM para um computador específico**|Mostra o histórico de inventário das unidades CD-ROM num computador especificado.|  



## <a name="hardware---disk"></a>Hardware - Disco  

Os oito relatórios seguintes estão listados na categoria **Hardware - Disk.** 

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com um tamanho de disco rígido específico**|Mostra uma lista dos computadores com discos rígidos de um tamanho especificado.|  
|**Computadores com pouco espaço livre em disco (menos do que a percentagem livre especificada)**|Mostra uma lista de computadores numa coleção especificada que têm menos espaço livre em disco do que o especificado.|  
|**Computadores com pouco espaço livre em disco (menos do que os MB livres especificados)**|Mostra uma lista de computadores e discos com pouco espaço livre em disco. A quantidade de espaço livre a verificar é especificada em MB.|  
|**Contagem das configurações físicas do disco**|Mostra o número de discos rígidos inventariados por capacidade de disco.|  
|**Informações sobre disco para um computador específico - Discos lógicos**|Mostra informações de resumo sobre os discos lógicos num computador especificado.|  
|**Informações do disco para um computador específico - partições**|Mostra informações de resumo sobre as partições do disco num computador especificado.|  
|**Informações do disco para um computador específico - discos físicos**|Mostra informações de resumo sobre os discos físicos num computador especificado.|  
|**Histórico - histórico do espaço do disco lógico para um computador específico**|Mostra o histórico de inventário para unidades de disco lógicas num computador especificado.|  



## <a name="hardware---general"></a>Hardware - General  

Os seguintes cinco relatórios estão listados na categoria **Hardware - Categoria Geral.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações do computador para um computador específico**|Mostra informações de resumo de um computador especificado.|  
|**Computadores num grupo de trabalho ou domínio específico**|Mostra uma lista de computadores num Grupo de Trabalho ou domínio especificado.|  
|**Classes de inventário atribuídas a uma coleção específica**|Mostra as classes de inventário que estão atribuídas a uma coleção especificada.|  
|**Classes de inventário ativadas num computador específico**|Mostra as classes de inventário ativadas num computador especificado.|  
|**Informações sobre dispositivos autopiloto do Windows**|Apresenta informações do dispositivo cliente que são necessárias para o registo do Windows AutoPilot.|



## <a name="hardware---memory"></a>Hardware - Memória  

Os seguintes cinco relatórios estão listados na categoria **Hardware - Memória.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores onde a memória física foi alterada**|Mostra uma lista de computadores onde a quantidade de RAM foi alterada desde o último ciclo de inventário.|  
|**Computadores com uma quantidade específica de memória**|Mostra uma lista de computadores com uma quantidade especificada de RAM (Memória Física Total arredondada para o MB mais próximo).|  
|**Computadores com pouca memória (menor ou igual aos MB especificados)**|Mostra uma lista de computadores com memória insuficiente. A quantidade de memória a verificar é especificada em MB.|  
|**Contagem de configurações de memória**|Mostra o número de computadores inventariados por quantidade de RAM.|  
|**Informações de memória para um computador específico**|Mostra informações de resumo sobre a memória num computador especificado.|  



## <a name="hardware---modem"></a>Hardware - Modem  

Os três relatórios seguintes estão listados na categoria **Hardware - Modem.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores para um fabricante de modems específico**|Mostra uma lista de computadores com um modem criado por um fabricante especificado.|  
|**Contagem de modems por fabricante**|Mostra o número de modems inventariados para cada fabricante de modems.|  
|**Informações do modem relativamente a computador específico**|Mostra informações de resumo sobre o modem num computador especificado.|  



## <a name="hardware---network-adapter"></a>Hardware - Adaptador de rede  

Os três relatórios seguintes estão listados na categoria **Hardware - Adaptador** de Rede.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma placa de rede específica**|Mostra uma lista de computadores com uma placa de rede especificada.|  
|**Contagem de placas de rede por fabricante**|Mostra o número de placas de rede inventariadas de cada tipo.|  
|**Informações da placa de rede para um computador específico**|Mostra informações sobre as placas de rede instaladas num computador especificado.|  



## <a name="hardware---processor"></a>Hardware - Processador  

Os seguintes cinco relatórios estão listados na categoria **Hardware - Processador.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma velocidade de processador específica**|Mostra uma lista de computadores que têm um processador com uma velocidade especificada.|  
|**Computadores com processadores rápidos (maior ou igual a uma velocidade de relógio especificada)**|Mostra uma lista de computadores com processadores com uma velocidade que é mais rápida do que a velocidade especificada.|  
|**Computadores com processadores lentos (menor ou igual a uma velocidade de relógio especificada)**|Mostra uma lista de computadores com processadores que são executados com uma velocidade de relógio igual ou mais lenta do que a especificada.|  
|**Contagem de velocidades de processador**|Mostra o número de computadores inventariados por velocidade de processador.|  
|**Informações do processador de um computador específico**|Mostra informações sobre os processadores instalados num computador especificado.|  



## <a name="hardware---scsi"></a>Hardware - SCSI  

Os seguintes cinco relatórios estão listados na categoria **Hardware - SCSI.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com um tipo de cartão SCSI específico**|Mostra uma lista de computadores com um cartão de SCSI especificado instalado.|  
|**Contagem dos tipos de cartão SCSI**|Mostra o número de cartões de SCSI inventariados por tipo de cartão.|  
|**Informações do cartão SCSI de um computador específico**|Mostra informações sobre os cartões SCSI instalados num computador especificado.|  



## <a name="hardware---security"></a>Hardware - Segurança

O seguinte relatório está listado na categoria **Hardware - Segurança.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Detalhes dos estados firmware nos dispositivos**|Exibe os detalhes dos estados de UEFI, SecureBoot e TPM. **Nota:** Este relatório não está na versão 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Hardware - Cartão de som  

Os três relatórios seguintes estão listados na categoria **Hardware - SCSI.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma placa de som específica**|Mostra uma lista de computadores com uma placa de som especificada.|  
|**Contagem de placas de som**|Mostra o número de computadores inventariados por cada tipo de placa de som.|  
|**Informações da placa de som de um computador específico**|Mostra informações de resumo sobre as placas de som num computador especificado.|  



## <a name="hardware---video-card"></a>Hardware - Cartão de vídeo  

Os três relatórios seguintes estão listados na categoria **Hardware - Cartão** de Vídeo.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma placa gráfica específica**|Mostra uma lista de computadores com uma placa gráfica especificada.|  
|**Contagem de placas gráficas por tipo**|Apresenta uma lista de todos os cartões de vídeo instalados em computadores. Também mostra o número de cada tipo de cartão de vídeo.|  
|**Informações da placa gráfica de um computador específico**|Mostra informações de resumo sobre as placas gráficas instaladas num computador especificado.|  



## <a name="migration"></a>Migração  

Os cinco relatórios seguintes constam da categoria **migração.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Clientes na lista de exclusão**|Mostra os clientes excluídos da migração.|  
|**Dependência de uma coleção do Configuration Manager**|Mostra os objetos que dependem de uma coleção da hierarquia de origem.|  
|**Propriedades da tarefa de migração**|Este relatório mostra os conteúdos da tarefa de migração especificada.|  
|**Tarefas de migração**|Este relatório mostra a lista de tarefas de migração.|  
|**Objetos cuja migração falhou**|Mostra uma lista de objetos cuja migração falhou durante a última tentativa.|  



## <a name="network"></a>Rede  

Os seis relatórios seguintes constam da categoria **Rede.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Contagem de endereços IP por sub-rede**|Mostra o número de endereços IP inventariados para cada sub-rede IP.|  
|**IP - Todas as subredes por máscara de sub-rede**|Mostra uma lista de sub-redes IP e de máscaras de sub-rede.|  
|**IP - Computadores numa sub-rede específica**|Mostra uma lista de computadores e informações de IP de uma sub-rede IP especificada.|  
|**IP - Informação para um computador específico**|Mostra informações de resumo sobre o IP de um computador especificado.|  
|**IP - Informações para um endereço IP específico**|Mostra informações de resumo sobre um endereço IP especificado.|  
|**MAC - Computadores para um endereço MAC específico**|Mostra o nome do computador e o endereço IP dos computadores com o endereço MAC especificado.|  



## <a name="operating-system"></a>Sistema operativo  

Os seguintes 10 relatórios estão listados na categoria **Sistema Operativo.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico da versão do sistema operativo do computador**|Mostra o histórico de inventário do sistema operativo num computador especificado.|  
|**Computadores com um sistema operativo específico**|Mostra os computadores com um sistema operativo especificado.|  
|**Computadores com um sistema operativo e service pack específicos**|Mostra os computadores com um sistema operativo e service pack especificados.|  
|**Contagem de versões do sistema operativo**|Mostra o número de computadores inventariados por sistema operativo.|  
|**Contagem de sistemas operativos e service packs**|Mostra o número de computadores inventariados por combinações de sistema operativo e service pack.|  
|**Serviços - computadores a executar um serviço específico**|Mostra uma lista de computadores a executar um serviço especificado.|  
|**Serviços - computadores a executar o Servidor de Acesso Remoto**|Mostra uma lista de computadores a executar o Servidor de Acesso Remoto.|  
|**Serviços - informações dos serviços de um computador específico**|Mostra informações de resumo sobre os serviços num computador especificado.|  
|**Windows 10 Detalhes de manutenção para uma coleção específica**|Exibe informações gerais sobre a manutenção do Windows 10 para uma recolha específica.|
|**Computadores Windows Server**|Mostra uma lista de computadores que executam os sistemas operativos Windows Server.|  


## <a name="power-management"></a>Gestão de energia  

Os seguintes 18 relatórios constam da categoria **power management.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gestão de Energia - Atividade informática**|Apresenta um gráfico que mostra o monitor, o computador e a atividade do utilizador para uma recolha especificada durante um período de tempo especificado.|  
|**Gestão de Energia - Atividade informática por computador**|Apresenta um gráfico que mostra o monitor, o computador e a atividade do utilizador para um computador especificado numa data especificada.|  
|**Gestão de Energia - Detalhes da atividade informática**|Mostra uma lista das funcionalidades de suspensão e reativação dos computadores na coleção especificada numa data e hora especificadas.|  
|**Gestão de Energia - Detalhes do computador**|Apresenta informações detalhadas sobre as capacidades de potência, configurações de potência e planos de potência aplicados a um computador especificado.|  
|**Gestão de Energia - Computador não reportando detalhes**|Mostra uma lista de computadores que não reportam atividade de energia numa data e hora especificadas.|  
|**Gestão de Energia - Computadores excluídos**|Mostra uma lista de computadores excluídos do esquema de energia.|  
|**Power Management - Computadores com múltiplos planos de potência**|Mostra uma lista de computadores com múltiplas definições de energia em conflito aplicadas.|  
|**Gestão de Energia - Consumo de energia**|Mostra o consumo mensal total de energia (em kWh) de uma coleção especificada num período de tempo especificado.|  
|**Gestão de Energia - Consumo de energia durante o dia**|Mostra o consumo de energia total (em kWh) de uma coleção especificada nos últimos 31 dias.|  
|**Gestão de Energia - Custo energético**|Mostra o custo do consumo mensal total de energia de uma coleção especificada num período de tempo especificado.|  
|**Gestão de Energia - Custo energético por dia**|Mostra o custo do consumo de energia total de uma coleção especificada nos últimos 31 dias.|  
|**Gestão de Energia - Impacto ambiental**|Mostra um gráfico com as emissões de dióxido de carbono (CO2) geradas por uma coleção específica num dado período de tempo.|  
|**Gestão de Energia - Impacto ambiental durante o dia**|Mostra um gráfico com as emissões de CO2 geradas por uma coleção específica nos últimos 31 dias.|  
|**Gestão de Energia - Detalhes do computador insomnia**|Apresenta informações detalhadas sobre computadores que não dormiram ou hibernam num período de tempo especificado.|  
|**Gestão de Energia - Relatório de Insónias**|Apresenta uma lista de causas comuns que impediram os computadores de dormir ou hibernar. Mostra também o número de computadores afetados por cada causa durante um período de tempo especificado.|  
|**Gestão de Energia - Capacidades de energia**|Mostra as funcionalidades de gestão de energia dos computadores na coleção especificada.|  
|**Gestão de Energia - Definições de potência**|Mostra uma lista agregada de definições de energia utilizadas pelos computadores numa coleção especificada.|  
|**Gestão de Energia - Detalhes de definições de energia**|Usado para mostrar mais informações sobre computadores especificados no relatório de definições de **power management - Power.**|  



## <a name="replication-traffic"></a>Tráfego de replicação  

Os seguintes 10 relatórios constam da categoria de Tráfego de **Replicação.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Tráfego de Replicação de Dados Globais por Ligação (gráfico de linhas)**|Mostra o tráfego total de replicação de dados globais numa ligação especificada para um número especificado de dias.|  
|**Tráfego de Replicação de Dados Globais por Ligação (gráfico circular)**|Mostra o tráfego total de replicação de dados globais numa ligação especificada para um número especificado de dias.|  
|**Tráfego de Replicação de Hierarquia por Ligação**|Mostra o tráfego total de replicação para cada ligação na hierarquia para um número especificado de dias.|  
|**Tráfego dos Dez Principais Grupos de Replicação de Hierarquia por Ligação (gráfico circular)**|Exibe o tráfego de replicação para os 10 principais grupos de replicação em toda a hierarquia identificada por ligação.|  
|**Tráfego de Replicação da Ligação**|Mostra o tráfego total de replicação para todos os dados relativamente a um número especificado de dias.|  
|**Tráfego do grupo de replicação por ligação**|Mostra o tráfego de rede do grupo de replicação através de uma ligação de replicação da base de dados especificada para um número especificado de dias.|  
|**Tráfego de Replicação de Dados do Site Por Ligação (gráfico de linhas)**|Mostra o tráfego de replicação total de dados do site numa ligação especificada para um número especificado de dias.|  
|**Tráfego de Replicação dos Dados do Site por Ligação (gráfico circular)**|Mostra o tráfego de replicação total de dados do site numa ligação especificada para um número especificado de dias.|  
|**Tráfego de Replicação da Hierarquia Total (gráfico de linhas)**|Mostra a replicação de dados do site e os dados globais agregados da hierarquia para cada direção de cada ligação relativamente a um número especificado de dias.|  
|**Tráfego de Replicação da Hierarquia Total (gráfico circular)**|Mostra a replicação de dados do site e os dados globais agregados da hierarquia para cada direção de cada ligação relativamente a um número especificado de dias.|  



## <a name="site---client-information"></a>Site - Informações do cliente  

Os seguintes 19 relatórios estão listados na categoria **Site - Informação** do Cliente.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório detalhado sobre o estado da atribuição do cliente**|Mostra informações detalhadas sobre o estado da atribuição do cliente.|  
|**Detalhes sobre a falha da atribuição do cliente**|Mostra informações detalhadas sobre as falhas da atribuição do cliente.|  
|**Detalhes do estado da atribuição do cliente**|Mostra informações gerais sobre o estado da atribuição do cliente.|  
|**Detalhes sobre o sucesso das atribuições do cliente**|Mostra informações detalhadas sobre os clientes cujas atribuições tiveram êxito.|  
|**Relatório sobre a falha na implementação do cliente**|Mostra informações detalhadas para clientes cujas implementações falharam.|  
|**Detalhes do estado da implementação do cliente**|Mostra informações de resumo do estado das instalações do cliente.|  
|**Relatório sobre a implementação do cliente com êxito**|Mostra informações detalhadas de clientes cujas implementações tiveram êxito.|  
|**Clientes sem capacidade de comunicação HTTPS**|Exibe informações detalhadas sobre cada cliente que executa a Ferramenta de Prontidão de Comunicação HTTPS, e informa para ser incapaz de comunicar através do HTTPS.|  
|**Computadores atribuídos mas não instalados num site específico**|Apresenta uma lista de computadores atribuídos a um determinado site, mas não estão a reportar a esse site.|  
|**Computadores com uma versão específica do cliente do Configuration Manager**|Apresenta uma lista de computadores que executam uma versão especificada do software cliente do Gestor de Configuração.|  
|**Contagem de clientes e protocolos utilizados para a comunicação**|Mostra um resumo dos métodos de comunicação utilizados pelos clientes (HTTP ou HTTPS).|  
|**Contagem de clientes atribuídos e instalados em cada site**|Mostra o número de computadores atribuídos e instalados em cada site. Os clientes com uma localização de rede associada a vários sites só são contados como instalados se estiverem a reportar a esse site.|  
|**Contagem de clientes com capacidade de comunicar por HTTPS**|Apresenta informações detalhadas sobre cada cliente que executa a Ferramenta de Prontidão de Comunicação HTTPS, e informa para ser capaz ou incapaz de comunicar através de HTTPS.|  
|**Contagem de clientes de cada site**|Apresenta o número de clientes do Gestor de Configuração instalados pelo código do site.|  
|**Contagem de clientes do Configuration Manager por versões de cliente**|Apresenta o número de computadores descobertos pela versão cliente do Gestor de Configuração.|  
|**Detalhes dos problemas reportados ao ponto de estado de contingência numa coleção especificada**|Apresenta informações detalhadas sobre questões relatadas pelos clientes numa coleção especificada. Estes clientes devem ter um ponto de situação de recuo atribuído.|  
|**Detalhes dos problemas reportados ao ponto de estado de contingência num site especificado**|Exibe informações detalhadas sobre problemas relatados pelos clientes num site especificado. Estes clientes devem ter um ponto de situação de recuo atribuído.|  
|**Resumo dos problemas reportados ao ponto de estado de contingência**|Exibe informações sobre todos os problemas reportados pelos clientes. Estes clientes devem ter um ponto de situação de recuo atribuído.|  
|**Resumo dos problemas reportados ao ponto de estado de contingência numa coleção específica**|Exibe informações sumárias para problemas relatados pelos clientes numa coleção especificada. Estes clientes devem ter um ponto de situação de recuo atribuído.|  



## <a name="site---discovery-and-inventory-information"></a>Site - Informações de descoberta e inventário  

Os seguintes 10 relatórios estão listados na categoria **Site - Discovery and Inventory Information.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Clientes que não reportaram recentemente (num número especificado de dias)**|Apresenta uma lista de clientes que não reportaram dados de descoberta, inventário de hardware ou inventário de software num número determinado de dias.|  
|**Computadores detetados por um site específico**|Apresenta uma lista de todos os computadores que o site especificado descobriu. Também mostra a data da descoberta mais recente.|  
|**Computadores detetados recentemente pelo método de deteção**|Apresenta uma lista de computadores que o site descobriu dentro do número especificado de dias. Também lista os agentes que os descobriram. Se vários agentes descobrirem um computador, pode aparecer mais de uma vez na lista.|  
|**Computadores não detetados recentemente (num número especificado de dias)**|Apresenta uma lista de computadores que o site não descobriu recentemente. Também mostra o número de dias desde que o site descobriu o computador.|  
|**Computadores não inventariados recentemente (num número especificado de dias)**|Apresenta uma lista de computadores que o site não inventou recentemente. Também mostra as últimas vezes que o cliente inventou o computador.|  
|**Computadores que podem partilhar o mesmo identificador exclusivo do Configuration Manager**|Mostra uma lista de computadores cujos nomes foram alterados. Uma mudança de nome é um possível sintoma de que um computador partilha um Identificador Único do Gestor de Configuração com outro computador.|  
|**Computadores com endereços MAC duplicados**|Mostra os computadores que partilham o endereço MAC.|  
|**Contagem de computadores nos domínios de recurso ou grupos de trabalho**|Mostra o número de computadores em cada domínio de recurso ou grupo de trabalho.|  
|**Informações de deteção para um computador específico**|Mostra uma lista dos agentes e sites que detetaram um computador especificado.|  
|**Datas de inventário para um computador específico**|Mostra a data e hora da execução mais recente do inventário num computador especificado.|  



## <a name="site---general"></a>Site - geral  

Os três relatórios seguintes constam do Site - Categoria **Geral.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores num site específico**|Mostra uma lista dos computadores cliente num site especificado.|  
|**Estado do site para a hierarquia**|Mostra a lista de sites na hierarquia com informações da versão do site e do estado do site.|  
|**Estado da atualização do Configuration Manager na hierarquia.**|Exibe informações sobre as atualizações do site do Gestor de Configuração para a hierarquia.|  



## <a name="site---server-information"></a>Site - Informações do Servidor  

O seguinte relatório está listado na categoria **Site - Informação** do Servidor.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Funções do sistema de sites e servidores do sistema de sites num site específico**|Mostra uma lista do servidor do sistema de sites e as respetivas funções do sistema de sites num site especificado.|  



## <a name="software---companies-and-products"></a>Software - Empresas e produtos  

Os seguintes 15 relatórios estão listados na categoria **Software - Empresas e Produtos.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os produtos inventariados numa empresa de software específica**|Mostra uma lista dos produtos e versões de software inventariados de uma empresa de software especificada.|  
|**Todas as empresas de software**|Mostra uma lista de todas as empresas que fabricam software inventariado.|  
|**Todas as aplicações do Windows**|Apresenta um resumo das aplicações do Windows instaladas. Procura utilizando os seguintes critérios: nome da aplicação, arquitetura ou editor.|  
|**Computadores com um produto específico**|Apresenta uma lista dos computadores em que um produto especificado é inventariado e as versões desse produto.|  
|**Computadores com um nome de produto e versão específicos**|Mostra uma lista dos computadores nos quais uma versão especificada de um produto está inventariada.|  
|**Computadores com software específico registado em Adicionar/Remover Programas**|Mostra um resumo de todos os computadores com software especificado e registado em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Contagem de todos os produtos e versões inventariados**|Mostra uma lista dos produtos e versões de software inventariados e o número de computadores nos quais estão instalados.|  
|**Contagem de produtos e versões inventariados de um produto específico**|Mostra uma lista das versões inventariadas de um produto especificado e o número de computadores nos quais estão instaladas.|  
|**Contagem de todas as instâncias de software registadas em Adicionar/Remover Programas**|Mostra um resumo de todas as instâncias do software instalado e registado em Adicionar/Remover Programas ou em Programas e Funcionalidades nos computadores da coleção especificada.|  
|**Contagem das instâncias de software específico registadas em Adicionar/Remover Programas.**|Mostra uma contagem das instâncias dos pacotes de software especificados instalados e registados em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Contagem de navegador padrão**|Mostra a contagem de clientes com um navegador web específico como o padrão do Windows. <br>Utilize a seguinte referência para browserProgIDs comuns:<br> - AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> Ou não, não é? HTTP: Microsoft Internet Explorer<br> - ChromeHTML: Google Chrome<br> - OperaStable: OperaSoftware<br> - FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> - Desconhecido: o cliente OS não suporta a consulta, a consulta não correu, ou um utilizador não registou|
|**Instalações de aplicações do Windows 8 especificadas**|Este relatório mostra uma lista de todos os computadores com uma aplicação especificada do Windows|  
|**Produtos num computador específico**|Mostra um resumo dos produtos de software inventariados e os seus fabricantes num computador especificado.|  
|**Software registado em Adicionar/Remover Programas num computador específico**|Mostra um resumo do software instalado num computador especificado que esteja registado em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Aplicações do Windows instaladas para o utilizador especificado**|Mostra todas as aplicações do Windows instaladas para o utilizador especificado|  



## <a name="software---files"></a>Software - Ficheiros  

Os seguintes cinco relatórios estão listados na categoria **Software - Ficheiros.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os ficheiros inventariados de um produto específico**|Mostra um resumo dos ficheiros inventariados associados a um produto de software especificado.|  
|**Todos os ficheiros inventariados num computador específico**|Mostra um resumo de todos os ficheiros inventariados num computador especificado.|  
|**Comparar o inventário de software em dois computadores**|Mostra as diferenças entre os inventários de software reportados em dois computadores especificados.|  
|**Computadores com um ficheiro específico**|Mostra uma lista de computadores que recolheram o inventário de software de um nome de ficheiro especificado. Se um computador contiver várias cópias do ficheiro, pode aparecer mais de uma vez na lista.|  
|**Contagem de computadores com um nome de ficheiro específico**|Mostra o número de computadores que recolheram o inventário de software de um ficheiro especificado.|  



## <a name="software-distribution---application-monitoring"></a>Distribuição de software - Monitorização de aplicações  

Os seguintes 10 relatórios estão listados na categoria **de Distribuição de Software - Monitorização de Aplicações.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as implementações de aplicações (avançado)**|Mostra informações de resumo detalhadas de todas as implementações de aplicações.|  
|**Todas as implementações de aplicações (básico)**|Mostra as informações de resumo de todas as implementações de aplicações.|  
|**Compatibilidade da aplicação**|Mostra as informações de compatibilidade da aplicação especificada na coleção especificada.|  
|**Implementações da aplicação por recurso**|Mostra as aplicações implementadas num dispositivo ou utilizador especificado.|  
|**Erros da infraestrutura da aplicação**|Mostra os erros da infraestrutura da aplicação. Estes erros incluem problemas de infraestrutura interna, ou erros resultantes de regras de requisitos inválidos.|  
|**Estado Detalhado da Utilização da Aplicação**|Mostra os detalhes de utilização das aplicações instaladas.|  
|**Estado do Resumo de Utilização da Aplicação**|Mostra um resumo da utilização das aplicações instaladas.|  
|**Implementações de sequência de tarefas que contêm uma aplicação**|Mostra as implementações de sequência de tarefas que instalam uma aplicação especificada.|  


## <a name="software-distribution---collections"></a>Distribuição de software - Coleções  

Os três relatórios seguintes estão listados na categoria Distribuição de **Software - Recolhas.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as coleções**|Mostra todas as coleções na hierarquia.|  
|**Todos os recursos de uma coleção específica**|Mostra todos os recursos numa coleção especificada.|  
|**Janelas de manutenção disponíveis para um cliente especificado**|Mostra todas as janelas de manutenção aplicáveis ao cliente especificado.|  



## <a name="software-distribution---content"></a>Distribuição de software - Conteúdo  

Os seguintes 16 relatórios estão listados na categoria **Distribuição de Software - Conteúdo.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as distribuições de conteúdos ativas**|Mostra todos os pontos de distribuição nos quais estão a ser atualmente instalados ou removidos conteúdos.|  
|**Todos os conteúdos**|Mostra todas as aplicações e pacotes num site.|  
|**Todos os conteúdos num ponto de distribuição específico**|Mostra todos os conteúdos atualmente instalados no ponto de distribuição especificado.|  
|**Todos os pontos de distribuição**|Mostra informações sobre os pontos de distribuição de cada site.|  
|**Todas as mensagens de estado de um pacote específico num ponto de distribuição específico**|Mostra todas as mensagens de estado de um pacote especificado num ponto de distribuição especificado.|  
|**Estado de distribuição dos conteúdos da aplicação**|Mostra informações sobre o estado de distribuição dos conteúdos da aplicação.|  
|**Aplicações direcionadas para um grupo de pontos de distribuição**|Mostra informações sobre os conteúdos da aplicação implementada num grupo de pontos de distribuição especificado.|  
|**Aplicações não sincronizadas num grupo de pontos de distribuição especificado**|Apresenta as aplicações para as quais os ficheiros de conteúdo associados não foram atualizados com a versão mais recente de um determinado grupo de pontos de distribuição.|  
|**Grupo de pontos de distribuição**|Mostra informações sobre um grupo de pontos de distribuição especificado.|  
|**Resumo da utilização do ponto de distribuição**|Mostra o resumo da utilização do ponto de distribuição para cada ponto de distribuição.|  
|**Estado da distribuição do pacote especificado**|Mostra o estado da distribuição dos conteúdos do pacote especificado em cada ponto de distribuição.|  
|**Pacotes direcionados para o grupo de pontos de distribuição**|Mostra informações sobre os pacotes que visam um grupo de pontos de distribuição especificado.|  
|**Pacotes não sincronizados num grupo de pontos de distribuição especificado**|Os ecrãs mostram pacotes para os quais os ficheiros de conteúdo associados não foram atualizados com a versão mais recente de um determinado grupo de pontos de distribuição.|  
|**Rejeição do conteúdo da fonte de cache peer**|Apresenta o número de rejeições de fonte de cache por grupo de fronteira.|
|**Rejeição do conteúdo da fonte de cache peer por condição**|Exibe as fontes de cache dos pares que rejeitaram servir conteúdo com base numa condição.|
|**Detalhes de rejeição de conteúdo de fonte de cache peer**|Mostra o nome do conteúdo que foi rejeitado por uma fonte de pares.|



## <a name="software-distribution---package-and-program-deployment"></a>Distribuição de software - Implementação de pacotes e programas 

Os seguintes cinco relatórios estão listados na categoria de Distribuição de **Software - Pacote e Implementação de Programas.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as implementações de um pacote e programa especificados**|Mostra informações sobre todas as implementações de um pacote e programa especificados.|  
|**Todas as implementações de pacotes e programas**|Mostra todas as implementações de pacotes e programas neste site.|  
|**Todas as implementações de pacotes e programas numa coleção especificada**|Mostra todas as implementações de pacotes e programas de uma coleção especificada.|  
|**Todas as implementações de pacotes e programas de um computador especificado**|Mostra todas as implementações de pacotes e programas aplicáveis a um computador especificado.|  
|**Todas as implementações de pacotes e programas de um utilizador especificado**|Mostra todas as implementações de pacotes e programas de um utilizador especificado.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Distribuição de software - Estado de implementação de pacotes e programas  

Os seguintes cinco relatórios estão listados na categoria de Distribuição de Software - Estado de **Distribuição de Pacotes e Programas.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as implementações de pacotes e programas de recurso do sistema com indicação de estado**|Mostra as implementações dos pacotes e programas no site com o estado de resumo de cada implementação.|  
|**Todos os recursos do sistema numa implementação de pacote e programa especificada num estado especificado**|Mostra uma lista de recursos num estado especificado para uma implementação de pacote e programa especificada.|  
|**Gráfico - Estado de conclusão de pacote sinuoso e de implementação do programa**|Exibe a percentagem de computadores que instalaram com sucesso a embalagem. A lista organiza-se por cada hora desde que um administrador cria o pacote e a implementação do programa. Pode ser utilizado para monitorizar o tempo médio de implementação de um pacote e programa.|  
|**Estado da implementação do pacote e programa de um cliente e implementação especificados**|Mostra as mensagens de estado reportadas para um computador e implementação de pacote e programa especificados.|  
|**Estado de uma implementação do pacote e programa especificada**|Mostra o estado de resumo de uma implementação do pacote e programa especificada.|  



## <a name="software-metering"></a>Medição de software  

Os seguintes 13 relatórios estão listados na categoria **De Medição** de Software.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as regras de medição de software aplicadas a este site**|Mostra uma lista de todas as regras de medição de software no site.|  
|**Computadores que tenham um programa medido instalado mas que não executam o programa desde uma data especificada**|Apresenta todos os computadores com a aplicação medido especificada, mas nenhum utilizador executou o programa desde a data especificada.|  
|**Computadores que executaram um programa de software medido específico**|Mostra uma lista de computadores que executaram programas correspondentes à regra de medição do software selecionada no mês e ano especificados.|  
|**Utilização em simultâneo de todos os programas de software medido**|Mostra o número máximo de utilizadores que executaram simultaneamente cada programa de software medido no mês e ano especificados.|  
|**Análise de tendências da utilização simultânea de um programa de software medido específico**|Mostra o número máximo de utilizadores que executaram simultaneamente o programa de software medido especificado durante cada mês do ano passado.|  
|**Base de instalação para todos os programas de software medidos**|Mostra o número de computadores que têm programas de software medido instalados, como reportado pelo inventário de software. Este relatório requer que o computador recolha o inventário de software.|  
|**Progresso do resumo de medição de software**|Mostra a hora do último processamento de dados de medição resumidos no servidor do site. Os relatórios de medição de software apenas refletem os dados de medição processados antes destas datas.|  
|**Resumo de utilização por hora do dia de um programa de software medido especificado**|Mostra o número médio de utilizações de um programa em particular nos últimos 90 dias apresentadas por hora e dia|  
|**Utilização total de todos os programas de software medidos**|Apresenta o número de utilizadores que executaram programas dentro do mês e ano especificados, e que correspondem a cada regra de medição de software. Estas regras são para software instalado localmente, ou para a utilização de Serviços Terminais.|  
|**Utilização total de todos os programas de software medidos em Servidores de Terminal do Windows**|Mostra o número de utilizadores que executaram programas correspondentes a cada regra de medição do software com Serviços de Terminal no mês e ano especificados.|  
|**Análise das tendências da utilização total de um programa de software medido específico**|Apresenta o número de utilizadores que executaram programas durante cada mês durante o ano passado, e que correspondem à regra de medição de software especificada. Estas regras são para software instalado localmente, ou para a utilização de Serviços Terminais.|  
|**Análise das tendências da utilização total de um programa de software medido específico nos Servidores de Terminal do Windows**|Apresenta o número de utilizadores que executaram programas durante cada mês durante o ano passado, e que correspondem à regra de medição de software especificada. Estas regras são para usar os Serviços Terminais.|  
|**Utilizadores que executaram um programa de software medido específico**|Apresenta uma lista de utilizadores que executaram programas dentro do mês e ano especificados, e que correspondem à regra de medição de software especificada.|  



## <a name="software-updates---a-compliance"></a>Atualizações de software - A Compliance  

Os oito relatórios seguintes estão listados na categoria Atualizações de **Software - Uma Conformidade.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Conformidade 1 - conformidade geral**|Mostra os dados gerais de conformidade para um grupo de atualização de software.|  
|**Conformidade 2 - atualização do software específico**|Mostra os dados de conformidade de uma atualização de software especificada.|  
|**Conformidade 3 - grupo de atualização (por atualização)**|Mostra os dados de conformidade das atualizações de software definidas num grupo de atualização de software.|  
|**Conformidade 4 - atualizações por fornecedor - mês e ano**|Mostra os dados de conformidade das atualizações de software disponibilizadas por um fornecedor durante um mês e ano especificados.|  
|**Conformidade 5 - computador específico**|Este relatório devolve os dados de conformidade da atualização de software de um computador especificado. Para limitar a quantidade de informações devolvidas, pode especificar a classificação do fabricante e da atualização de software.|  
|**Conformidade 6 - estados da atualização de software específica (secundário)**|Mostra a contagem e a percentagem de computadores em cada estado de conformidade para a atualização de software especificada.|  
|**Conformidade 7 - computadores num estado de conformidade específico para um grupo de atualização (secundário)**|Mostra todos os computadores numa coleção com um estado de conformidade geral especificado relativamente a um grupo de atualização de software.|  
|**Conformidade 8 - computadores num estado de conformidade específico para uma atualização (secundário)**|Mostra todos os computadores numa coleção com um estado de conformidade especificado de uma atualização de software.|  
|**Conformidade 9 - Saúde geral e conformidade**|Apresenta os dados globais de saúde e conformidade de um grupo de atualização de software. (a partir da versão 1806)| 


## <a name="software-updates---b-deployment-management"></a>Atualizações de software - B Gestão de Implementação  

Os oito relatórios seguintes estão listados na categoria De Gestão de **Implementação de Software - B.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gestão 1 - implementações de um grupo de atualização**|Apresenta todas as implementações que incluem todas as atualizações de software definidas num grupo de atualização de software especificado.|  
|**Gestão 2 - atualizações obrigatórias mas não implementadas**|Apresenta todas as atualizações de software específicas do fornecedor que os clientes detetam conforme necessário, mas um administrador não implementou para uma recolha especificada.|  
|**Gestão 3 - atualizações numa implementação**|Mostra as atualizações de software que estão contidas numa implementação especificada.|  
|**Gestão 4 - Implementações direcionadas a uma coleção**|Mostra todas as implementações de atualização de software que visam uma coleção especificada.|  
|**Gestão 5 - Implementações direcionadas a um computador**|Mostra todas as implementações de atualização de software que estão implementadas num computador especificado.|  
|**Gestão 6 - implementações que contêm uma atualização específica**|Apresenta todas as implementações que incluem uma atualização de software especificada e a coleção de alvos associada para a implementação.|  
|**Gestão 7 - atualizações numa implementação com conteúdos em falta**|Apresenta as atualizações de software numa implementação especificada que não tem todo o conteúdo associado recuperado. Este estado impede os clientes de instalarem a atualização, o que impede que a implementação atinja 100% de conformidade.|  
|**Gestão 8 - computadores com conteúdos em falta (secundário)**|Apresenta todos os computadores que necessitam da atualização de software especificada, mas o conteúdo associado ainda não está distribuído para um ponto de distribuição.|  



## <a name="software-updates---c-deployment-states"></a>Atualizações de software - C Deployment states  

Os seis relatórios seguintes estão listados na categoria **De atualizações de software - C Deployment States.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Estados 1 - estados de imposição de uma implementação**|Mostra os estados de imposição de uma implementações de atualização de software, que é tipicamente a segunda fase de uma avaliação da implementação.|  
|**Estados 2 - estados de avaliação de uma implementação**|Mostra o estado de avaliação de uma implementação de atualização de software específica, que é tipicamente a primeira fase de uma avaliação da implementação.|  
|**Estados 3 - estados de uma implementação e de um computador**|Mostra os estados de todas as atualizações de software na implementação especificada de um computador especificado.|  
|**Estados 4 - computadores num estado específico de uma implementação (secundário)**|Mostra todos os computadores num estado especificado de uma implementação de atualização de software.|  
|**Estados 5 - estados de atualização numa implementação (secundário)**|Mostra um resumo dos estados de uma atualização de software especificada visada por uma implementação especificada.|  
|**Estados 6 - computadores num estado de imposição específico de uma atualização (secundário)**|Mostra todos os computadores num estado de imposição especificado de uma atualização de software especificada.|  



## <a name="software-updates---d-scan"></a>Atualizações de software - D Scan  

Os quatro relatórios seguintes estão listados na categoria **De scan de Software - D Scan.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Análise 1 - estados da última análise por coleção**|Especifique uma recolha para exibir a contagem de computadores em cada estado de conformidade. Os clientes devolvem o estado durante a última varredura de conformidade.|  
|**Análise 2 - estados da última análise por site**|Especifique um site para exibir a contagem de computadores em cada estado de conformidade. Os clientes devolvem o estado durante a última varredura de conformidade.|  
|**Análise 3 - clientes de uma coleção a comunicar um estado específico (secundário)**|Mostra todos os computadores de uma coleção especificada e um estado de análise da conformidade especificado durante a última análise de compatibilidade.|  
|**Análise 3 - clientes de um site a comunicar um estado específico (secundário)**|Especifique um site para exibir todos os computadores com um estado de conformidade especificado. Os clientes devolvem o Estado durante a sua última varredura de conformidade.|  



## <a name="software-updates---e-troubleshooting"></a>Atualizações de software - E Resolução de Problemas  

Os quatro relatórios seguintes estão listados na categoria **Desinformação de Software - E Troubleshooting.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Resolução de problemas 1 - Erros de digitalização**|Mostra os erros de análise no site e uma contagem dos computadores com cada erro.|  
|**Resolução de problemas 2 - Erros de implantação**|Mostra os erros de implementação no site e uma contagem dos computadores com cada erro.|  
|**Resolução de problemas 3 - Computadores falham com um erro específico de digitalização (secundário)**|Mostra uma lista dos computadores cuja análise falhou devido a um erro especificado.|  
|**Resolução de Problemas 4 - computadores em falha com um erro de implementação específico (secundário)**|Mostra uma lista dos computadores nos quais a implementação da atualização está a falhar devido a um erro especificado.|  



## <a name="state-migration"></a>Migração estatal  

Os três relatórios seguintes constam da categoria **emigração estatal.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações de migração de estado de um computador de origem específico**|Mostra informações de migração de estado de um computador de origem especificado.|  
|**Informações de migração de estado de um ponto de migração de estado específico**|Mostra informações de migração de estado de um ponto de migração de estado especificado.|  
|**Pontos de migração de estado de um site específico**|Mostra os pontos de migração de estado de um site específico|  



## <a name="status-messages"></a>Mensagens de estado  

Os seguintes 12 relatórios estão listados na categoria Mensagens de **Estado.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as mensagens com um ID de mensagem específico**|Mostra uma lista de mensagens de estado com um ID de mensagem especificado.|  
|**Clientes que reportaram erros nas últimas 12 horas num site específico**|Mostra uma lista de computadores e componentes que reportaram erros nas últimas 12 horas e o número de erros reportados.|  
|**Mensagens de componente nas últimas 12 horas**|Mostra uma lista de mensagens de componente nas últimas 12 horas para um código de site, computador e componente específicos.|  
|**Mensagens de componente na última hora**|Apresenta uma lista das mensagens de estado criadas na última hora por um componente especificado num computador especificado num determinado site.|  
|**Contagem de mensagens de componente na última hora num site específico**|Mostra o número de mensagens de estado por componente e gravidade reportadas na última hora num site especificado.|  
|**Contagem de erros nas últimas 12 horas**|Mostra o número de mensagens de estado de erro do componente de servidor nas últimas 12 horas.|  
|**Erros fatais (por componente)**|Mostra uma lista de computadores que reportaram erros fatais por componente.|  
|**Erros fatais (por nome de computador)**|Mostra uma lista de computadores que reportaram erros fatais por nome do computador.|  
|**Últimas 1 000 mensagens de um computador específico (Erros e Avisos)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro e aviso do componente num computador especificado.|  
|**Últimas 1 000 mensagens de um computador específico (Avisos, Erros e Informações)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro, aviso e informativas do componente num computador especificado.|  
|**Últimas 1 000 mensagens de um computador específico (Erros)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro de servidor do componente num computador especificado.|  
|**Últimas 1 000 mensagens de um componente do servidor específico**|Mostra um resumo das 1 000 mensagens de estado mais recentes de um componente de servidor especificado.|  



## <a name="status-messages---audit"></a>Mensagens de estado - Auditoria  

Os três relatórios seguintes constam da categoria Mensagens de **Estado - Auditoria.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as mensagens de auditoria para um utilizador específico**|Mostra um resumo de todas as mensagens de estado de auditoria para um utilizador especificado. As mensagens de auditoria descrevem as ações tomadas na consola do Gestor de Configuração que adicionam, modificam ou eliminam objetos no 'Gestor de Configuração'.|  
|**Controlo Remoto - Todos os computadores controlados à distância por um utilizador específico**|Mostra um resumo das mensagens de estado a indicar o controlo remoto dos computadores cliente por um utilizador especificado.|  
|**Controlo Remoto - Todas as informações de controlo remoto**|Mostra um resumo das mensagens de estado relacionadas com o controlo remoto dos computadores cliente.|  



## <a name="task-sequence---deployment-status"></a>Sequência de tarefas - Estado de implantação  

Os seguintes 11 relatórios estão listados na categoria **De Suposição de Tarefas - Estado de Implantação.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os recursos do sistema para uma implementação de sequência de tarefas num site específico**|Mostra uma lista de computadores de destino para a implementação da sequência de tarefas especificada num estado de implementação especificado.|  
|**Todos os recursos do sistema para uma implementação de sequência de tarefas num estado específico e que está disponível para computadores desconhecidos**|Mostra uma lista de computadores de destino para a implementação da sequência de tarefas especificada que está no estado de implementação especificado.|  
|**Contagem de recursos do sistema com implementações de sequência de tarefas atribuídas mas não executadas**|Apresenta o número de computadores que aceitaram sequências de tarefas, mas não executaram a sequência de tarefas.|  
|**Histórico da implementação de uma sequência de tarefas num computador**|Mostra o estado de cada passo da implementação da sequência de tarefas especificada no computador de destino especificado. Se nenhum registo for devolvido, a sequência de tarefas ainda não começou no computador.|  
|**Lista de computadores que excederam um limite de tempo específico para a execução de uma sequência de tarefas**|Mostra a lista de computadores de destino que excederam o limite de tempo especificado para a execução de uma sequência de tarefas.|  
|**Tempo de execução de uma implementação de sequência de tarefas específica no computador de destino específico**|Mostra o tempo total que uma sequência de tarefas especificada num computador especificado levou a ser concluída com êxito.|  
|**Tempo de execução de cada passo de uma implementação de sequência de tarefas num computador de destino específico**|Mostra o tempo que cada passo da implementação da sequência de tarefas especificada levou a ser concluído no computador de destino especificado.|  
|**Estado da implementação de uma sequência de tarefas específica num computador específico**|Mostra o resumo do estado de uma implementação de sequência de tarefas especificada num computador especificado.|  
|**Estado de implementação de sequência de tarefas num computador de destino desconhecido**|Mostra o estado da implementação da sequência de tarefas especificada no computador de destino desconhecido especificado.|  
|**Resumo de estado de uma implementação de sequência de tarefas específica**|Mostra um resumo do estado de todos os recursos que foram visados por uma implementação.|  
|**Resumo de estado de uma implementação de sequência de tarefas específica que está disponível para computadores desconhecidos**|Apresenta o resumo do estado de todos os recursos visados pela implementação especificada que está disponível para uma coleção que contenha computadores desconhecidos.|  



## <a name="task-sequence---deployments"></a>Sequência de tarefas - Implantações  

Os seguintes 11 relatórios estão listados na categoria Sequência de **Tarefas - Implementações.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os recursos do sistema num grupo ou fase específicos de uma implementação de sequência de tarefas específica**|Mostra uma lista de computadores que estão atualmente a ser executados num grupo ou fase especificado de uma implementação de sequência de tarefas especificada.|  
|**Todos os recursos de sistema onde uma implementação de sequência de tarefas falhou num grupo ou fase específicos**|Mostra uma lista de computadores nos quais ocorreu um erro no grupo/fase especificada da implementação da sequência de tarefas especificada.|  
|**Todas as implementações de sequência de tarefas**|Mostra detalhes de todas as implementações de sequência de tarefas iniciadas a partir do site atual.|  
|**Todas as implementações de sequência de tarefas disponíveis em computadores desconhecidos**|Apresenta detalhes de todas as implementações da sequência de tarefas iniciadas a partir do site e implementadas em coleções que contenham computadores desconhecidos.|  
|**Contagem de falhas em cada fase ou grupo da sequência de tarefas específica**|Mostra o número de falhas em cada fase ou grupo da sequência de tarefas especificada.|  
|**Contagem de falhas em cada fase ou grupo de uma implementação de sequência de tarefas**|Mostra o número de falhas em cada fase ou grupo da implementação de sequência de tarefas especificada.|  
|**Estado da implementação de todas as implementações de sequência de tarefas**|Mostra o progresso geral de todas as implementações de sequência de tarefas.|  
|**Progresso de uma sequência de tarefas em execução**|Mostra o progresso da sequência de tarefas especificada.|  
|**Progresso de uma implementação de sequência de tarefas em execução**|Mostra as informações de resumo da implementação da sequência de tarefas especificada.|  
|**Progresso de todas as implementações de uma sequência de tarefas específica**|Mostra o progresso de todas as implementações de sequência de tarefas especificada.|  
|**Relatório de resumo de uma implementação de sequência de tarefas**|Mostra as informações de resumo da implementação da sequência de tarefas especificada.|  



## <a name="task-sequence---progress"></a>Sequência de tarefas - Progresso  

Os seguintes cinco relatórios estão listados na categoria Sequência de **Tarefas - Progress.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gráfico - Progresso semanal de uma sequência de tarefas**|Mostra o progresso semanal de uma sequência de tarefas iniciado na data de implementação.|  
|**Progresso de uma sequência de tarefas**|Mostra o progresso da sequência de tarefas especificada.|  
|**Progresso de uma sequência de tarefas**|Mostra um resumo do progresso de todas as sequências de tarefas.|  
|**Progresso da sequências de tarefas de implementações do sistema operativo**|Mostra o progresso de todas as sequências de tarefas que implementam sistemas operativos.|  
|**Estado de todos os computadores desconhecidos**|Apresenta uma lista de computadores desconhecidos no momento em que executaram uma sequência de tarefas, e se agora são computadores conhecidos.|  



## <a name="task-sequences---references"></a>Sequências de tarefas - Referências  

O seguinte relatório é listado na categoria sequências de **tarefas - categoria de referências.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Conteúdos referenciados por uma sequência de tarefas específica**|Mostra os conteúdos referenciados por uma sequência de tarefas especificada.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Utilizador - Afinidade do dispositivo  

Os dois seguintes relatórios estão listados na categoria **User - Device Affinity.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Associações de afinidade dispositivo/utilizador por coleção que estão pendentes**|Este relatório mostra todas as atribuições de afinidade dispositivo/utilizador pendentes, com base nos dados de utilização, para membros de uma coleção.|  
|**Associações de afinidade dispositivo/utilizador por coleção**|Exibe todas as associações de dispositivos de utilizador para a recolha especificada e agrupa os resultados por tipo de recolha (por exemplo, utilizador ou dispositivo).|  



## <a name="user-data-and-profiles-health"></a>Saúde dos dados dos utilizadores e perfis  

Os quatro relatórios seguintes estão listados na categoria De dados e perfis do **utilizador.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório do Estado de Funcionamento do Redirecionamento da Pasta - Detalhes**|Apresenta os detalhes do estado de saúde da reorientação da pasta para cada uma das pastas redirecionadas para um determinado utilizador.|  
|**Relatório de Funcionamento de Perfis de Utilizador Itinerantes - Detalhes**|Apresenta os detalhes do estado de saúde do perfil do utilizador de roaming para um utilizador especificado.|  
|**Relatório do Estado de Funcionamento de Perfis e Dados de Utilizador - Detalhes**|Apresenta os detalhes de erro ou aviso de reorientação da pasta ou perfis de utilizador de roaming. Este relatório é o objetivo dos pormenores do relatório sumário.|  
|**Relatório do Estado de Funcionamento de Perfis e Dados de Utilizador - Resumo**|Mostra o resumo dos estados de funcionamento do redirecionamento de pastas e perfis de utilizador itinerante.|  



## <a name="users"></a>Utilizadores  

Os três relatórios seguintes estão listados na categoria **Utilizadores.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com um nome de utilizador específico**|Mostra uma lista dos computadores que foram utilizados por um utilizador especificado.|  
|**Contagem de utilizadores por domínio**|Mostra o número de utilizadores em cada domínio.|  
|**Utilizadores num domínio específico**|Mostra uma lista de utilizadores e os respetivos computadores num domínio especificado.|  



## <a name="virtual-applications"></a>Aplicações virtuais  

Os seguintes sete relatórios estão listados na categoria **Aplicações Virtuais.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Resultados do Ambiente Virtual de App-V**|Mostra informações sobre um ambiente virtual especificado que está num estado especificado para uma coleção especificada.|  
|**Resultados do Ambiente Virtual de App-V Para Ativo**|Exibe informações sobre um ambiente virtual especificado para um ativo especificado. Também mostra quaisquer tipos de implantação para o ambiente virtual especificado.|  
|**Estado do Ambiente Virtual de App-V**|Mostra informações de compatibilidade num ambiente virtual especificado para uma coleção especificada.|  
|**Computadores com uma aplicação virtual específica**|Mostra um resumo dos computadores com o atalho da aplicação App-V especificada, criado com o Application Virtualization Management Sequencer.|  
|**Computadores com um pacote específico de aplicação virtual**|Apresenta um resumo de computadores que possuem o pacote de aplicações App-V especificado.|  
|**Contagem de todas as instâncias de pacotes de aplicações virtuais**|Mostra uma contagem dos pacotes de aplicações App-V detetados.|  
|**Contagem de todas as instâncias de aplicações virtuais**|Mostra uma contagem das aplicações App-V detetadas.|  



## <a name="vulnerability-assessment"></a>Avaliação de vulnerabilidades

O seguinte relatório é listado na categoria **de Avaliação** de Vulnerabilidades.

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório Geral de Avaliação de Vulnerabilidades**|Identifica vulnerabilidades de segurança, administrativa e conformidade para um computador específico|  



## <a name="wake-on-lan"></a>Reativação Por LAN  

Os seguintes sete relatórios estão listados na categoria **Wake On LAN.**

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os computadores visados para atividade de Reativação por LAN**|Especifique o tipo de implementação para exibir uma lista de computadores direcionados para a atividade wake on LAN.|  
|**Todos os objetos pendentes de atividade de reativação**|Mostra os objetos agendados para reativação.|  
|**Todos os sites com capacidade para Reativação por LAN**|Mostra uma lista de todos os sites na hierarquia com capacidade para Reativação por LAN.|  
|**Erros recebidos durante o envio de pacotes de reativação durante um período de tempo definido**|Mostra os erros recebidos durante o envio de pacotes de reativação para computadores durante um período de tempo definido|  
|**Histórico da atividade de Reativação por LAN**|Mostra um histórico da atividade de reativação ocorrida desde um determinado período.|  
|**Detalhes do estado de implementação do proxy de reativação**|Mostra informações sobre o estado de implementação do Proxy de Reativação de cada dispositivo de uma coleção especificada.|  
|**Resumo do estado de implementação do proxy de reativação**|Mostra um resumo do estado de implementação do Proxy de Reativação numa coleção especificada.|  
