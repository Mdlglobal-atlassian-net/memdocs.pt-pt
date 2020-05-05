---
title: Desinstalar sites
titleSuffix: Configuration Manager
description: Um guia para remover funções e desinstalar sites e hierarquias
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718050"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Desinstalar funções, sites e hierarquias em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize este artigo como um guia para desinstalar uma função, site ou hierarquia do sistema do Site do Gestor de Configuração.

A partir da versão 2002, também pode remover o site da administração central (CAS) de uma hierarquia, mas manter o local principal.

## <a name="site-system-role"></a><a name="bkmk_role"></a>Função do sistema do site

É melhor remover uma função de um servidor de sistema de site pelas seguintes razões:

- Mudança de infraestrutura mais ampla, como rede ou locais físicos
- Desmantelar o servidor subjacente
- Consolidar funções para reduzir custos e complexidade
- Reconfigurar ou redesenhar as funções do site
- Interromper a utilização da funcionalidade que o papel suporta

Quando decidir que precisa de remover um papel, primeiro considere as suas respostas para as seguintes perguntas:

- Ainda precisa do papel no site? Em caso afirmativo, outro sistema de site já tem o papel?

- Outros sistemas de sites com esta função são devidamente dimensionados para suportar os seus requisitos de negócio para desempenho e disponibilidade?

- Todos os clientes já estão reconfigurados para usar outro papel? Vai confiar nos comportamentos padrão do cliente para recuar ou descobrir outro servidor?

### <a name="procedure-to-remove-a-site-system-role"></a>Procedimento para remover uma função do sistema de site

Utilize o seguinte procedimento para eliminar uma função:

1. Na consola De **Configuração Manager,** vá ao espaço de trabalho da **Administração.** Expandir a **configuração**do site e, em seguida, selecionar o nó de **Funções de Servidores e Do Sistema do Site.**

1. Selecione o servidor do sistema do site com a função de remover. No painel de detalhes do sistema do **site,** selecione a função alvo.

1. Na fita, no separador **Role** site, no grupo **Role site,** selecione **Remover Função**. Confirme que quer remover o papel.

### <a name="additional-information-for-specific-roles"></a>Informações adicionais para funções específicas

Algumas funções podem ter passos e considerações adicionais.

#### <a name="software-update-point"></a>Ponto de atualização de software

Depois de remover o ponto de atualização do software, o Gestor de Configuração atualiza a política do cliente para remover o ponto de atualização de software da lista. Ao remover o último ponto de atualização de software no site, a lista de pontos de atualização de software não contém pontos de atualização de software. Sem funções disponíveis, a gestão de atualizações de software é essencialmente desativada no site.

Quando tiver mais de um ponto de atualização de software num site primário e remover o ponto de atualização de software que é a fonte de sincronização, escolha outro ponto de atualização de software no site para ser a nova fonte de sincronização.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a>Local secundário  

Além de estar [a desmantelar uma hierarquia,](#bkmk_hierarchy)a principal razão para remover um local secundário deve-se a uma mudança de infraestrutura mais ampla, como a rede ou locais físicos. Consulte também as razões para [escolher um site secundário](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Quando decidir que precisa de remover um site secundário, primeiro considere as suas respostas para as seguintes perguntas:

- Removeu todas as funções do sistema do site do servidor do site?

- Existem limites ou grupos de fronteiras associados ao local secundário? Reconfigurar os limites antes de remover o local.

- Algum cliente ainda está no local?

- Já configuraste outras opções de gestão de conteúdos, como [o caching dos pares?](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)

### <a name="options-to-delete-secondary-sites"></a>Opções para eliminar sites secundários

Não pode mover ou reatribuir um local secundário para outro local primário. Quando remover um site secundário do seu site direct parent, escolha se deve desinstalar ou apagar.

#### <a name="uninstall-the-secondary-site"></a>Desinstalar o local secundário

Utilize esta opção para remover um site secundário funcional que esteja acessível a partir da rede. Esta opção desinstala o Gestor de Configuração a partir do servidor de site secundário. Em seguida, elimina toda a informação sobre o site e os seus recursos do site do Gestor de Configuração.

Se o Gestor de Configuração instalou o SQL Server Express para o local secundário, o Gestor de Configuração também desinstala o SQL Express. Se instalou o SQL Server Express antes de instalar o site secundário, o Gestor de Configuração não desinstala o SQL Server Express.

#### <a name="delete-the-secondary-site"></a>Eliminar o local secundário

Utilize esta opção nas seguintes situações:

- Falhou em instalar

- Depois de desinstalá-lo, a consola 'Gestor de Configuração' ainda mostra o site secundário

    Esta opção elimina todas as informações sobre o site e os seus recursos da hierarquia do Gestor de Configuração, mas não faz alterações no servidor do site.

    > [!TIP]
    >  Também pode utilizar a Ferramenta de Manutenção da Hierarquia com a opção **/DELSITE** para eliminar um site secundário. Para mais informações, consulte A Ferramenta de [Manutenção da Hierarquia (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Pré-requisitos para apagar um site secundário

O utilizador administrativo que executa a configuração do Gestor de Configuração precisa dos seguintes direitos de segurança:

- **Direitos** do Administrador Local no servidor de site secundário

- Se o servidor de base de dados do site primário estiver remoto do servidor do site principal, os direitos do **Administrador** local no servidor de base de dados do site remoto para o site principal.

- **Administrador de Infraestrutura** ou papel de segurança **do Administrador Completo** no local principal dos pais

- **Direitos de sisadmina** na base de dados do site secundário

### <a name="procedure-to-delete-a-secondary-site"></a>Procedimento para apagar um local secundário

Utilize o seguinte procedimento para desinstalar ou eliminar um local secundário:

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó **de Sites.**

1. Selecione o servidor de site secundário que pretende remover. Na fita, no separador **Home,** no grupo **Site,** selecione **Delete**.

1. Na página **Geral,** selecione se desinstalar ou eliminar o site secundário.

1.  Conclua o assistente.

## <a name="primary-site"></a><a name="bkmk_primary"></a>Local primário  

Pode querer desinstalar um site primário da sua hierarquia pelas seguintes razões:

- Consolidar sítios para reduzir custos e complexidade
- Reconfigurar ou redesenhar os sítios da hierarquia

Antes de desinstalar um site primário infantil que utiliza [vistas distribuídas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) para a sua ligação de replicação ao CAS, desligue primeiro as vistas distribuídas na sua hierarquia. Para obter mais informações, veja [Desinstalar um site primário configurado com vistas distribuídas](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a>Plano para desinstalar um local primário

Antes de desinstalar um site primário, reveja as seguintes tarefas:

- Rever limites, grupos de fronteiras e relações de recuo. Se atribuir clientes a um novo site, mas não alterar os limites, podem ser considerados roaming. Para mais informações, consulte Definir os limites do [site e os grupos de fronteira.](../configure/define-site-boundaries-and-boundary-groups.md)

- Certifique-se de que todos os clientes ativos são transferidos para outro local primário da hierarquia. Caso contrário, os clientes não serão geridos depois de desinstalar o site. Para mais informações, consulte [Como atribuir clientes a um site](../../../clients/deploy/assign-clients-to-a-site.md).

  - Reveja a lista de funções do site para garantir que o novo site fornece o mesmo nível de serviço.

  - Certifique-se de que dimensionou corretamente os outros sistemas do site com este papel no outro site. Terão de suportar os seus requisitos de negócio para o desempenho e disponibilidade com os clientes adicionais.

  - Se este site tiver muitos clientes, reatribua-os por etapas. Monitorize a replicação da base de dados à medida que os clientes atualizam o inventário completo e outros dados específicos do site. Se gerir atualizações de software, os clientes atribuirão a um novo ponto de atualização de software. Este comportamento causa uma varredura completa para a conformidade da atualização.

  - A reatribuição do cliente pode ter impacto em relatórios e consultas que dependem de dados de inventário e de conformidade baseada no Estado. Considere ajustar temporariamente quaisquer ciclos de cliente durante a transição.

  - Reveja todos os métodos de atribuição do cliente para se certificar de que nenhum se refere a este site primário.

- Verifique se algum objeto usado ativamente na hierarquia tem referências estáticas ao código do local. Por exemplo, consultas de recolha, sequências de tarefas ou scripts administrativos.

- Se a hierarquia usar um site de [recuo](../configure/boundary-group-procedures.md#bkmk_site-fallback) para a atribuição automática do site, certifique-se de que não faz referência a este local primário.

- Reconfigure quaisquer métodos de [instalação](../../../clients/deploy/plan/client-installation-methods.md) do cliente que possam fazer referência a um código de site estático.

- Se este site principal tiver algum serviço específico em nuvem, certifique-se de removê-los. Se ainda precisar dos recursos da nuvem, desloque-os para outro local primário da hierarquia. Remova-os do local principal que vai desinstalar e adicioná-los a outro local primário.

- Se este local primário tiver [algum método](../configure/run-discovery.md) de descoberta para a hierarquia, mova-os para outro local.

- Retire qualquer meio de [implantação de SISTEMA](../../../../osd/deploy-use/create-task-sequence-media.md)baseado no site.

- Desinstale todas as funções do sistema do site a partir do site e do servidor do site. Para mais informações, consulte [Desinstalar as funções](#bkmk_role)do sistema do site . Embora este passo de preparação não seja necessário, ajuda a identificar quaisquer dependências adicionais antes de desinstalar o site.

- Desinstale quaisquer locais secundários sob este local primário. Para mais informações, consulte a secção de [sítio seleção secundária.](#bkmk_secondary)

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a>Pré-requisitos para desinstalar um local primário

O utilizador administrativo que executa a configuração do Gestor de Configuração precisa dos seguintes direitos de segurança:

- **Direitos** do Administrador Local no servidor CAS

- Se o servidor de base de dados CAS estiver remoto do servidor do site, os direitos do **Administrador** local no servidor de base de dados do site remoto para o CAS.

- **Direitos de sisadmina** na base de dados do site CAS

- **Direitos** do Administrador Local no servidor do site principal

- Se o servidor de base de dados do site primário estiver remoto do servidor do site principal, os direitos do **Administrador** local no servidor de base de dados do site remoto para o site principal.

- **Administrador de Infraestruturas** ou papel de segurança **do Administrador Completo** no CAS

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a>Procedimento para desinstalar um local primário

Executa a configuração do Gestor de Configuração para desinstalar um site primário que não tenha um site secundário associado. Utilize o seguinte procedimento para desinstalar um local primário:

> [!TIP]
> Se o servidor do site principal já não estiver disponível, utilize a Ferramenta de Manutenção da Hierarquia no CAS para eliminar o local principal da base de dados do site. Para mais informações, consulte A Ferramenta de [Manutenção da Hierarquia (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Configurar o Gestor de Configuração no servidor principal do site utilizando um dos seguintes métodos:

    - No menu **Iniciar,** selecione Configuração do Gestor de **Configuração**.

    - No diretório para os meios de `\SMSSETUP\BIN\X64\setup.exe`instalação do Gestor de *Configuração,* aberto. Certifique-se de que esta versão é a mesma que a versão do site.

    - No diretório onde o Gestor de `\BIN\X64\setup.exe`Configuração está *instalado,* aberto.

1. Reveja as informações na página **Antes de Começar.**

1. Na página **Getting Started,** selecione **Desinstalar um site do Gestor**de Configuração .

    > [!IMPORTANT]  
    >  Quando um site secundário está associado ao site primário, tem de remover o site secundário antes de poder desinstalar o site primário.  

1. Na página **Desinstalar a** página do Site do Gestor de Configuração, ambas as seguintes opções são ativadas por predefinição:

    - Remova a base de dados do site do servidor principal do site
    - Remova a consola do Gestor de Configuração

1. Selecione **Sim** para confirmar a não instalação do site principal do Gestor de Configuração.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a>Desinstale um site primário que utilize vistas distribuídas

1. Antes de desinstalar um local primário para crianças, desligue as vistas distribuídas em cada elo na hierarquia entre o CAS e um local primário.

1. Depois de desligar as vistas distribuídas em cada link, confirme que os dados do site primário terminam a reinicialização no CAS. Para monitorizar a inicialização dos dados, consulte [a replicação do Monitor](../../manage/monitor-replication.md).

1. Depois de os dados reinicializarem com sucesso com o CAS, pode [desinstalar o local principal](#bkmk_pri-process).

1. Quando o local principal estiver desinstalado, pode reconfigurar as vistas distribuídas em links do CAS para outros locais primários.

    > [!IMPORTANT]
    > Se desinstalar o site principal antes de desativar as vistas distribuídas em cada site, ou antes que os dados do site primário reininicializem com sucesso no CAS, a replicação de dados pode falhar.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a>Desmantelar uma hierarquia

Algumas organizações têm múltiplas hierarquias devido a fusões, aquisições, ambientes de teste ou outros requisitos de negócio. Se consolidar a gestão numa única hierarquia, esta ação pode ajudar a reduzir custos e complexidade. Outra razão para desativar a hierarquia é que está a migrar para um serviço de gestão apenas na nuvem, como o Microsoft Intune, e está pronto para remover a sua infraestrutura no local.

Para desmantelar uma hierarquia com vários locais, a sequência de remoção é importante. Comece por desinstalar os locais na parte inferior da hierarquia e, em seguida, mover-se para cima:

1. Remova os locais secundários anexados aos locais primários.
2. Desinstale os locais primários.
3. Depois de desinstalar todos os locais primários, pode desinstalar o CAS.

Para mais informações, consulte as seguintes secções:

- [Remover um local secundário](#bkmk_secondary)
- [Desinstalar um local primário](#bkmk_primary)
- [Desinstalar o CAS](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a>Desinstalar o CAS

O passo final para desmantelar uma hierarquia é desinstalar o CAS. Executar Configuração do Gestor de Configuração para desinstalar o CAS que não tem sites primários para crianças.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Pré-requisitos para desinstalar o CAS

O utilizador administrativo que executa a configuração do Gestor de Configuração precisa dos seguintes direitos de segurança:

- **Direitos** do Administrador Local no servidor CAS

- Se o servidor de base de dados CAS estiver remoto do servidor do site, os direitos do **Administrador** local no servidor de base de dados do site remoto para o CAS.

#### <a name="procedure-to-uninstall-the-cas"></a>Procedimento para desinstalar o CAS

1. Configurar o Gestor de Configuração no servidor CAS utilizando um dos seguintes métodos:

    - No menu **Iniciar,** selecione Configuração do Gestor de **Configuração**.

    - No diretório para os meios de `\SMSSETUP\BIN\X64\setup.exe`instalação do Gestor de *Configuração,* aberto. Certifique-se de que esta versão é a mesma que a versão do site.

    - No diretório onde o Gestor de `\BIN\X64\setup.exe`Configuração está *instalado,* aberto.

1. Reveja as informações na página **Antes de Começar.**

1. Na página **Getting Started,** selecione **Desinstalar um site do Gestor**de Configuração .

    > [!IMPORTANT]  
    >  Remova todos os locais primários da criança antes de poder desinstalar o CAS.  

1. Na página **Desinstalar a** página do Site do Gestor de Configuração, ambas as seguintes opções são ativadas por predefinição:

    - Remova a base de dados do site do servidor CAS
    - Remova a consola do Gestor de Configuração

1. Selecione **Sim** para confirmar a não instalação do site central de administração do Gestor de Configuração (CAS).

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a>Remover o CAS

<!-- 3607277 -->

A partir da versão 2002, se a hierarquia for constituída pelo CAS e por um único local primário infantil, pode remover o CAS. Esta ação simplifica a sua infraestrutura de Gestor de Configuração para um único local primário autónomo. Remove as complexidades da replicação site-to-site, e centra as suas tarefas de gestão no único site.

Para mais informações, consulte [Remova o CAS](remove-central-administration-site.md).
