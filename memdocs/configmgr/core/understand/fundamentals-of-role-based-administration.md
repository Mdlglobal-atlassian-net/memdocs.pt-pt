---
title: Fundamentos da administração baseados em papéis
titleSuffix: Configuration Manager
description: Utilize uma administração baseada em papéis para controlar o acesso administrativo ao Gestor de Configuração e objetos que gere.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 62faf2fd736f9751e8b33e821cb814f527a1197c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722859"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Fundamentos da administração baseada em funções para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração, utiliza a administração baseada em papéis para garantir o acesso necessário para administrar o Gestor de Configuração. Também assegura o acesso aos objetos que gere, como coleções, implementações e sites. Depois de compreender os conceitos introduzidos neste artigo, pode configurar a [administração baseada em funções para O Gestor de Configuração](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 O modelo de administração baseado em papéis define e gere centralmente as definições de acesso à segurança em toda a hierarquia para todos os sites e configurações do site, utilizando os seguintes itens:  

- *As funções* de segurança são atribuídas aos utilizadores administrativos para fornecer aos utilizadores (ou grupos de utilizadores) permissão para diferentes objetos do Gestor de Configuração. Por exemplo, permissão para criar ou alterar as definições do cliente.  

- *Os âmbitos* de segurança são utilizados para agrupar instâncias específicas de objetos que um utilizador administrativo é responsável por gerir, como uma aplicação que instala o Microsoft Office 2010.  

- *As coleções* são utilizadas para especificar grupos de recursos de utilizador e dispositivo que o utilizador administrativo pode gerir.  

  Com a combinação de papéis de segurança, âmbitos de segurança e coleções, segrega as atribuições administrativas que cumprem os requisitos da sua organização. Utilizados em conjunto, definem o âmbito administrativo de um utilizador, que é o que esse utilizador pode visualizar e gerir na implementação do Seu Gestor de Configuração.  

## <a name="benefits-of-role-based-administration"></a>Benefícios da administração baseada em papéis  

- Os sites não são usados como limites administrativos.  
- Cria-se utilizadores administrativos para uma hierarquia e só precisa de lhes atribuir segurança uma vez.  
- Todas as missões de segurança são replicadas e disponíveis em toda a hierarquia.  
- Existem funções de segurança incorporadas que são usadas para atribuir as tarefas típicas de administração. Crie as suas próprias funções de segurança personalizadas para suportar os seus requisitos de negócio específicos.  
- Os utilizadores administrativos vêem apenas os objetos que têm permissões para gerir.  
- É possível auditar as ações de segurança administrativa.  

Quando concebe e implementa a segurança administrativa para o Gestor de Configuração, utiliza o seguinte para criar uma *margem administrativa* para um utilizador administrativo:  

- [Funções de segurança](#bkmk_Planroles)  

- [Coleções](#bkmk_planCol)  

- [Âmbitos de segurança](#bkmk_PlanScope)  

 O âmbito administrativo controla os objetos que um utilizador administrativo vê na consola do Gestor de Configuração, e controla as permissões que um utilizador tem nesses objetos. As configurações da administração baseada em funções são replicadas para cada site da hierarquia como dados globais e são depois aplicadas a todas as ligações administrativas.  

> [!IMPORTANT]  
> Os atrasos na replicação entre sites podem impedir que um site receba alterações para a administração baseada em funções. Para obter informações sobre como monitorizar a replicação da base de dados intersite, consulte as [transferências de Dados entre o](../plan-design/hierarchy/data-transfers-between-sites.md) tópico dos sites.  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a>Funções de segurança

 Utilize funções de segurança para conceder permissões de segurança a utilizadores administrativos. As funções de segurança são grupos de permissões de segurança que são atribuídas aos utilizadores administrativos para que estes possam desempenhar as suas tarefas administrativas. Estas permissões de segurança definem as ações administrativas que um utilizador administrativo pode executar e as permissões que são concedidas para tipos de objetos específicos. Como melhor prática de segurança, atribua as funções de segurança que proporcionam menos permissões.  

 O Gestor de Configuração tem várias funções de segurança incorporadas para suportar agrupamentos típicos de tarefas administrativas, e pode criar as suas próprias funções de segurança personalizadas para suportar os seus requisitos de negócio específicos. Exemplos das funções de segurança incorporadas:  

- *O Administrador Completo* concede todas as permissões no Gestor de Configuração.  

- *O Gestor de Ativos* concede permissões para gerir o Ponto de Sincronização de Inteligência de Ativos, aulas de relatórios de Inteligência de Ativos, inventário de software, inventário de hardware e regras de medição.  

- *O Gestor de Atualização* de Software concede permissões para definir e implementar atualizações de software. Os utilizadores administrativos que estejam associados a esta função podem criar coleções, grupos de atualizações de software, implementações e modelos.  

- *O Administrador de Segurança* concede permissões para adicionar e remover utilizadores administrativos e associar utilizadores administrativos a funções de segurança, coleções e âmbitos de segurança. Os utilizadores administrativos associados a esta função também podem criar, modificar e eliminar funções de segurança e os seus âmbitos e coleções de segurança atribuídos.

> [!TIP]  
> Pode visualizar a lista de funções de segurança incorporadas e funções de segurança personalizadas que cria, incluindo as suas descrições, na consola Do Gestor de Configuração. Para visualizar as funções, no espaço de trabalho da **Administração,** expandir **segurança,** e, em seguida, selecionar **Funções**de Segurança .  

 Cada função de segurança tem permissões específicas para tipos de objetos diferentes. Por exemplo, a função de segurança do Autor da *Aplicação* tem as seguintes permissões para aplicações: Aprovar, Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Executar Relatório e Definir âmbito de segurança.

 Não pode alterar as permissões para as funções de segurança incorporadas, mas pode copiar o papel, fazer alterações e, em seguida, guardar essas mudanças como uma nova função de segurança personalizada. Também pode importar papéis de segurança que exportou de outra hierarquia, por exemplo, de uma rede de testes. Reveja as funções de segurança e as suas permissões para determinar se irá utilizar as funções de segurança incorporadas ou se tem de criar as suas próprias funções de segurança personalizadas.  

### <a name="to-help-you-plan-for-security-roles"></a>Para ajudá-lo a planear funções de segurança  

1. Identifique as tarefas que os utilizadores administrativos executam no 'Gestor de Configuração'. Estas tarefas podem estar relacionadas com um ou mais grupos de tarefas de gestão, tais como a implementação de aplicações e pacotes, a implementação de sistemas operativos e definições de compatibilidade, a configuração de sites e da segurança, auditorias, o controlo remoto de computadores e a recolha de dados de inventário.  

2. Mapeie estas tarefas administrativas para uma ou mais das funções de segurança incorporadas.  

3. Se alguns dos utilizadores administrativos executarem as tarefas de múltiplas funções de segurança, atribuir as múltiplas funções de segurança a estes utilizadores administrativos em vez de criar uma nova função de segurança que combine as tarefas.  

4. Se as tarefas que identificou não mapearem as funções de segurança incorporadas, criem e testem novas funções de segurança.  

Para obter informações sobre como criar e configurar funções de segurança para administração baseada em papéis, consulte [Criar funções](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) de segurança personalizadas e [configurar funções](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) de segurança no artigo [de Configuração baseado em funções para Configuração Manager.](../../core/servers/deploy/configure/configure-role-based-administration.md)  

##  <a name="collections"></a><a name="bkmk_planCol"></a>Coleções

 As coleções especificam os recursos de utilizador e de computador que um utilizador administrativo pode ver ou gerir. Por exemplo, para poderem implementar aplicações ou efetuar o controlo remoto, os utilizadores administrativos devem ter atribuída uma função de segurança que conceda acesso a uma coleção que contenha esses recursos. É possível selecionar coleções de utilizadores ou dispositivos.  

 Para obter mais informações sobre coleções, consulte [Introdução a coleções.](../../core/clients/manage/collections/introduction-to-collections.md)  

 Antes de configurar a administração baseada em funções, verifique se criou novas coleções por qualquer um dos seguintes motivos:  

- Organização funcional. Por exemplo, coleções separadas de servidores e de estações de trabalho.  
- Alinhamento geográfico. Por exemplo, coleções separadas para a América do Norte e para a Europa.  
- Requisitos de segurança e processos empresariais. Por exemplo, coleções separadas para computadores de produção e de teste.  
- Alinhamento organizacional. Por exemplo, coleções separadas para cada unidade de negócio.  

Para obter informações sobre como configurar coleções para administração baseada em papéis, consulte [coleções configure para gerir a segurança](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) no artigo de [Configure baseado em funções para configuração manager.](../../core/servers/deploy/configure/configure-role-based-administration.md)  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a> Âmbitos de segurança

 Utilize âmbitos de segurança para fornecer aos utilizadores administrativos acesso a objetos com capacidade de segurança. Um âmbito de segurança é um conjunto nomeado de objetos securáveis que são atribuídos aos utilizadores administradores como um grupo. Todos os objetos com capacidade de segurança têm de ser atribuídos a um ou mais âmbitos de segurança. O Gestor de Configuração tem dois âmbitos de segurança incorporados:  

- O âmbito de segurança *integrado* permite o acesso a todos os âmbitos. Não é possível atribuir objetos a esta área de segurança.  

- O âmbito de segurança incorporado *predefinido* é utilizado para todos os objetos, por padrão. Quando instalar pela primeira vez o 'Gestor de Configuração', todos os objetos são atribuídos a este âmbito de segurança.  

Se pretender restringir os objetos que os utilizadores administrativos podem ver e gerir, tem de criar e utilizar os seus próprio âmbitos de segurança personalizados. Os âmbitos de segurança não suportam uma estrutura hierárquica e não podem ser aninhados. Os âmbitos de segurança podem conter um ou mais tipos de objetos, que incluem os seguintes itens:  

- Subscrições de alertas  
- Aplicações  
- Imagens de arranque  
- Grupos de limites  
- Itens de configuração  
- Definições de cliente personalizadas  
- Pontos de distribuição e grupos de pontos de distribuição  
- Pacotes de controladores
- Pastas (a partir da versão 1906) <!--3600867-->
- Condições globais  
- Tarefas de migração
- Imagens de sistema operativo
- Pacotes de instalação de sistema operativo  
- Pacotes  
- Consultas  
- Sites  
- Regras de medição de software  
- Grupos de atualizações de software  
- Pacotes de atualizações de software  
- Pacotes de sequências de tarefas  
- Pacotes e itens de definição de dispositivos Windows CE  

Há também alguns objetos que não pode incluir em âmbitos de segurança porque só estão protegidos por funções de segurança. O acesso administrativo a estes objetos não se limita a um subconjunto dos objetos disponíveis. Por exemplo, pode ter um utilizador administrativo que cria grupos de limites que são utilizados para um site específico. Como o objeto de fronteira não suporta os âmbitos de segurança, não pode atribuir a este utilizador um âmbito de segurança que dá acesso apenas aos limites que podem estar associados a esse site. Como um objeto de fronteira não pode ser associado a um âmbito de segurança, quando você atribui uma função de segurança que inclui o acesso a objetos de fronteira a um utilizador, esse utilizador pode aceder a todas as fronteiras da hierarquia.  

Objetos que não são limitados por âmbitos de segurança incluem os seguintes itens:  

- Florestas do Active Directory  
- Utilizadores administrativos  
- Alertas  
- Políticas anti-malware  
- Limites  
- Associações de computador  
- Predefinições de cliente  
- Modelos de implementação  
- Controladores de dispositivo  
- Conector do Exchange Server  
- Mapeamentos site a site de migração  
- Perfis de inscrição de dispositivos móveis  
- Funções de segurança  
- Âmbitos de segurança  
- Endereços de sites  
- Funções do sistema de sites  
- Títulos de software  
- Atualizações de software  
- Mensagens de estado  
- Afinidades de dispositivo do utilizador  

Crie âmbitos de segurança quando tiver de limitar o acesso a instâncias de objetos separadas. Por exemplo:  

- Tem um grupo de utilizadores administrativos que deve poder ver aplicações de produção e não aplicações de teste. Crie um âmbito de segurança para aplicações de produção e outro para as aplicações de teste.  

- Utilizadores administrativos diferentes necessitam de acesso diferente a algumas instâncias de um tipo de objeto. Por exemplo, um grupo de utilizadores administrativos necessita da permissão de Leitura para grupos de atualizações de software específicos e outro grupo de utilizadores administrativos necessita das permissões Modificar e Eliminar para outros grupos de atualização de software. Crie âmbitos de segurança diferentes para estes grupos de atualizações de software.  

Para obter informações sobre como configurar os âmbitos de segurança para a administração baseada em funções, consulte os âmbitos de [segurança do Configure para um objeto](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) no artigo de configuração baseado em funções para [configuração.](../../core/servers/deploy/configure/configure-role-based-administration.md)  

## <a name="next-steps"></a>Passos seguintes

[Configure a administração baseada em funções para o Gestor de Configuração](../../core/servers/deploy/configure/configure-role-based-administration.md)
