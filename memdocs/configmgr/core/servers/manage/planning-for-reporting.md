---
title: Planear relatórios
titleSuffix: Configuration Manager
description: Desde detalhes de instalação até largura de banda de segurança e rede, é importante planear reportagens no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713682"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Plano para reportagem em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Relatório no Gestor de Configuração fornece um conjunto de ferramentas e recursos que o ajudam a usar as capacidades avançadas de reporte dos Serviços de Reporte do Servidor SQL ou do Power BI Report Server. Utilize as seguintes secções para o ajudar a planear reporte no 'Gestor de Configuração'.

## <a name="where-to-install-the-reporting-services-point"></a>Onde instalar o ponto de serviços de reporte

Quando executa relatórios do Gestor de Configuração num site, os relatórios têm acesso à informação na base de dados do site em que se conecta. Utilize as secções seguintes para o ajudar a determinar onde deve instalar o ponto do Reporting Services e qual a origem de dados a utilizar.

> [!NOTE]
> Para obter mais informações sobre o planeamento de sistemas de sites no Gestor de Configuração, consulte [adicionar funções](../deploy/configure/add-site-system-roles.md)do sistema do site .

### <a name="supported-site-system-servers"></a> Servidores do sistema de sites suportados

Pode instalar o ponto de serviços de reporte num site de administração central (CAS) e locais primários. Funciona em vários sistemas de sites num site, e em outros locais da hierarquia. O Gestor de Configuração não suporta o ponto de serviços de reporte em sites secundários. O primeiro ponto de serviços de reporte num site é definido como o servidor de relatório padrão. Pode adicionar mais pontos de serviços de reporte num site, mas o Gestor de Configuração informa que utiliza ativamente o servidor de relatório predefinido em cada site. Instale o ponto de serviços de reporte no servidor do site ou num sistema de site remoto. Para um melhor desempenho, utilize os Serviços de Relato do Servidor SQL num servidor de sistema de site remoto.

### <a name="data-replication-considerations"></a> Considerações sobre replicação de dados

Considere os seguintes fatores para o ajudar a determinar onde instalar os pontos do Reporting Services:

- Um ponto de serviços de reporte com a base de dados cas como a sua fonte de dados reporte tem acesso a todos os dados globais e do site na hierarquia do Gestor de Configuração. Se necessitar de relatórios que contenham dados do site para vários sites numa hierarquia, considere instalar o ponto de serviços de reporte num sistema de site no CAS. Em seguida, utilize a sua base de dados como fonte de dados de reporte.

- Um ponto de serviços de reporte com uma base de dados do site primário infantil como a sua fonte de dados reporte tem acesso a dados globais e dados do site apenas para o local primário local e quaisquer sites secundários para crianças. Os dados do site para outros sites primários na hierarquia do Gestor de Configuração não se replicam para este site primário. Os Serviços de Informação não podem aceder aos dados do site para outros sites primários. Se necessitar de relatórios que contenham dados do site para um determinado site primário ou dados globais, e não pretenda que o utilizador tenha acesso aos dados do site de outros sites primários, instale um ponto de serviços de reporte num sistema de site no local principal. Em seguida, use a base de dados do site principal como fonte de dados de reporte.

Para obter mais informações sobre os dados globais e do site, consulte [tipos de dados](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Considerações sobre a largura de banda de rede

Dependendo da configuração do site, os sistemas do site no mesmo site comunicam entre si utilizando o bloco de mensagens do servidor (SMB), HTTP ou HTTPS. O Gestor de Configuração não gere esta comunicação. Pode ocorrer a qualquer momento sem controlo de largura de banda da rede. Reveja a largura de banda da rede disponível antes de instalar a função de ponto de ponto de serviços de reporte num sistema de site.

Para obter mais informações sobre o planeamento dos sistemas do site, consulte [adicionar funções](../deploy/configure/add-site-system-roles.md)do sistema do site .

## <a name="plan-for-role-based-administration"></a>Plano para a administração baseada em funções

A segurança para reportar é muito parecida com outros objetos no Gestor de Configuração onde pode atribuir funções de segurança e permissões aos utilizadores administrativos. Os utilizadores administrativos só podem executar e modificar relatórios para os quais têm direitos de segurança adequados. Para executar relatórios na consola Do Gestor de Configuração, os utilizadores precisam do **Direito de Leitura** para a permissão do **Site** e as permissões configuradas para objetos específicos.

Ao contrário de outros objetos no Configurmanager, os direitos de segurança que definiu para utilizadores administrativos na consola Do Gestor de Configuração também estão configurados em Serviços de Reporte. Quando configura os direitos de segurança na consola do Gestor de Configuração, o ponto de serviços de reporte liga-se aos Serviços de Informação e define permissões adequadas para relatórios.

Por exemplo, a função de segurança do Gestor de **Atualização** de Software tem as permissões **do Relatório de Execução** e modificação do **Relatório.** Os utilizadores com a função de Gestor de **Atualização** de Software só podem executar e modificar relatórios para atualizações de software. A consola 'Gestor de Configuração' não exibe relatórios para outros objetos desta função. A exceção a este comportamento é que alguns relatórios não estão associados a objetos securíveis do Gestor de Configuração específicos. Para esses relatórios, o utilizador administrativo deve possuir o direito **Ler** para a permissão do **Site** para executar os relatórios e o direito **Modificar** para a permissão do **Site** para modificar os relatórios.  

> [!IMPORTANT]
> Para os utilizadores de um domínio diferente do da conta de ponto saque de serviços de reporte para executar relatórios com sucesso, estabeleça uma confiança bidirecional entre os dois domínios.

Os relatórios têm o suporte de administração baseada em funções ativado. O Gestor de Configuração filtra os dados para todos os relatórios incluídos com base nas permissões do utilizador que executa o relatório. Os utilizadores com funções específicas só podem visualizar informações definidas para as suas funções.

Para obter mais informações sobre os direitos de segurança para reporte, consulte [o relatório Configure](configuring-reporting.md).

Para obter mais informações sobre a administração baseada em papéis no Gestor de Configuração, consulte a [administração baseada em funções configurar](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Recomendações de reporte

Considere as seguintes recomendações e dicas para reporte no Gestor de Configuração:

- Para um melhor desempenho, instale o ponto de serviços de reporte num sistema de site remoto. Embora possa instalá-lo no servidor do site, o ponto de serviços de reporte tem o melhor desempenho quando o instala num sistema de site remoto. Quando este papel faz o processamento de antecedentes, pode competir por recursos do sistema com outras funções. Existem muitas variáveis a considerar com o desempenho do site e do papel, mas em geral esta configuração melhora o reporte e o desempenho geral do site.

- Otimizar consultas de serviços de reporte de servidores SQL. Normalmente, quaisquer atrasos de reporte devem-se ao tempo que demora a fazer consultas e recuperar os resultados. As ferramentas do Microsoft SQL Server, como o Query Analyzer e o Profiler, podem ajudá-lo a otimizar consultas.

- Agendar o processamento de assinatura supor relatório para executar fora do horário normal de escritório. Sempre que possível, o processamento de subscrições durante o horário de folga pode minimizar o processamento do CPU no servidor de base de dados do Site Do Gestor de Configuração. Esta prática melhora também a disponibilidade para pedidos imprevistos de relatórios.

- As atualizações do site preservam relatórios incorporados. Se modificar um relatório padrão, quando o site atualiza, rebatiza`_`o relatório com um prefixo de sublinhado ( ). Este comportamento garante que a atualização do site não substitui o relatório modificado pelo relatório padrão.

## <a name="security-and-privacy"></a>Segurança e privacidade

O Gestor de Configuração informa as informações que recolhe durante as operações padrão de gestão do Gestor de Configuração. Por exemplo, pode apresentar um relatório de informação que o Gestor de Configuração recolheu da descoberta ou do inventário. Os relatórios também podem conter as informações de estado atuais para operações de gestão de clientes, tais como implementação de software e verificação de compatibilidade.

Para mais informações sobre quaisquer recomendações de segurança e informações de privacidade para operações do Gestor de Configuração que possam gerar dados que possa ver nos relatórios, consulte segurança e privacidade para O Gestor de [Configuração](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Passos seguintes

[Pré-requisitos para elaboração de relatórios](prerequisites-for-reporting.md)
