---
title: Instale e configure um ponto de atualização de software
titleSuffix: Configuration Manager
description: Os sites primários requerem um ponto de atualização de software no site da administração central para atualizações de software avaliação de conformidade e para implementar atualizações de software para os clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 0cddb8df51624a562597da17ea310db0a26081f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715474"
---
# <a name="install-and-configure-a-software-update-point"></a>Instale e configure um ponto de atualização de software  

*Aplica-se a: Gestor de Configuração (ramo atual)*


> [!IMPORTANT]  
>  Antes de instalar a função do sistema de pontode atualização de software (SUP), deve verificar se o servidor satisfaz as dependências necessárias e determina a infraestrutura de pontos de atualização de software no site. Para obter mais informações sobre como planear atualizações de software e determinar a sua infraestrutura de pontos de atualização de software, consulte [plan para atualizações](../plan-design/plan-for-software-updates.md)de software .  

 O ponto de atualização de software é necessário no site da administração central e nos sites primários para permitir a avaliação de conformidade de atualizações de software e implementar atualizações de software para os clientes. O ponto de atualização de software é opcional em site secundários. A função do sistema de sites do ponto de atualização de software tem de ser criada num servidor com o WSUS instalado. O ponto de atualização de software interage com os serviços WSUS para configurar as definições de atualização de software e para solicitar a sincronização de metadados de atualizações de software. Quando tiver uma hierarquia do Gestor de Configuração, instale e configure primeiro o ponto de atualização do software no site da administração central, depois nos sites primários infantis e, em seguida, opcionalmente, em sites secundários. Quando tiver um site primário autónomo, não um site de administração central, comece por instalar e configurar o ponto de atualização de software no site primário e, depois, como opção, em sites secundários. Algumas definições só estão disponíveis quando configura o ponto de atualização de software num site de nível superior. Existem diferentes opções que tem de considerar dependendo de onde instalou o ponto de atualização de software.  

> [!IMPORTANT]  
>  Pode instalar mais do que um ponto de atualização de software num site. O primeiro ponto de atualização de software que instala é configurado como a origem de sincronização, que sincroniza as atualizações do Microsoft Update ou da origem de sincronização a montante. Os outros pontos de atualização de software no site são configurados como réplicas do primeiro ponto de atualização de software. Por conseguinte, algumas definições não estão disponíveis depois de instalar e configurar o ponto de atualização de software inicial.  

> [!IMPORTANT]  
>  Não é suportado para instalar a função do sistema de ponto de atualização de software num servidor que foi configurado e utilizado como um servidor WSUS autónomo ou usando um ponto de atualização de software para gerir diretamente os clientes wSUS. Os servidores WSUS existentes são suportados apenas como fontes de sincronização a montante para o ponto de atualização de software ativo. Ver [Synchronize a partir de uma localização](#BKMK_wsussync) de fonte de dados a montante

 Pode adicionar a função do sistema de sites do ponto de atualização de software a um servidor de sistema de sites existente ou pode criar uma nova. Na página de **seleção** de funções do sistema do Desenvolvedor do Servidor do **Site criar** ou adicionar o assistente de funções do sistema do **site,** dependendo se adiciona a função do sistema do site a um servidor de site novo ou existente, selecione o ponto de **atualização**do Software e, em seguida, configure as definições de ponto de atualização de software no assistente. As definições são diferentes dependendo da versão do 'Gestor de Configuração' que utiliza. Para obter mais informações sobre como instalar as funções do sistema do site, consulte [instalar as funções](../../core/servers/deploy/configure/install-site-system-roles.md)do sistema do site.  

 Utilize as secções seguintes para obter informações sobre as definições do ponto de atualização de software num site.  

## <a name="proxy-server-settings"></a>Definições do servidor proxy  
 Pode configurar as definições do servidor proxy em diferentes páginas do Assistente do Servidor do **Sistema do Site criar** ou adicionar funções do sistema de **localização,** dependendo da versão do Gestor de Configuração que utiliza.  

-   Tem de configurar o servidor proxy e, em seguida, especificar quando utilizar o servidor proxy para atualizações de software. Configure as seguintes definições:  

    -   Configure as definições do servidor proxy na página **Proxy** do assistente ou no separador **Proxy** em Propriedades do sistema de sites. As definições do servidor proxy são específicas do sistema do site, o que significa que todas as funções do sistema do site utilizam as definições do servidor proxy que especifica.  

    -   Especifique se utilizar o servidor proxy quando o Gestor de Configuração sincroniza as atualizações do software e quando descarrega conteúdo utilizando uma regra de implementação automática. Configure as definições do servidor proxy do ponto de atualização de software na página **Definições de Proxy e de Conta** do assistente ou no separador **Definições de Proxy e de Conta** em Propriedades do ponto de atualização de software.  

        > [!NOTE]  
        >  A definição **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática** está disponível, mas não é utilizada para um ponto de atualização de software num site secundário. Apenas o ponto de atualização de software no site de administração central e site primário transfere conteúdo a partir da página do Microsoft Update.  

> [!IMPORTANT]  
>  Por predefinição, a conta **Sistema Local** para o servidor onde foi criada uma regra de implementação automática serve para ligar à Internet e transferir atualizações de software quando são executadas as regras de implementação automática. Quando esta conta não tem acesso à Internet, as atualizações de software não são transferidas e a entrada seguinte é registada em ruleengine.log: **Não foi possível transferir a atualização a partir da Internet. Erro = 12007**. Configure as credenciais para ligar ao servidor proxy quando a conta do Sistema Local não tem acesso à Internet.  


## <a name="wsus-settings"></a>Definições de WSUS  
 Deve configurar as definições do WSUS em diferentes páginas do Assistente do Servidor do **Sistema do Site Create System** ou adicionar funções de sistema de **site,** dependendo da versão do Gestor de Configuração que utiliza, e em alguns casos, apenas nas propriedades para o ponto de atualização do software, também conhecido como Propriedades componentes de ponto de atualização de software. Utilize as informações nas secções seguintes para configurar as definições de WSUS.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>Definições da porta WSUS  
 Tem de configurar as definições da porta WSUS na página Ponto de Atualização de Software do assistente ou nas propriedades do ponto de atualização de software. Utilize o procedimento seguinte para determinar as definições de porta utilizadas pelo WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Para determinar as definições de porta utilizadas no IIS  

 1.  No servidor WSUS, abra o Gestor de Serviços de Informação Internet (IIS).  

 2.  Expanda **Web Sites**, clique com o botão direito do rato no Web site do servidor WSUS e, em seguida, clique em **Editar Enlaces**. Na caixa de diálogo Enlaces de Site, os valores das portas HTTP e HTTPS são apresentados na coluna **Porta** .


### <a name="configure-ssl-communications-to-wsus"></a>Configurar comunicações SSL para WSUS  
 Pode configurar a comunicação SSL na página **Geral** do assistente ou no separador **Geral** nas propriedades do ponto de atualização de software.  

 Para obter mais informações sobre como utilizar o SSL, veja [Decidir se pretende configurar o WSUS para utilizar SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>Conta de Ligação ao Servidor WSUS  
 Pode configurar uma conta para ser utilizada pelo servidor de sites quando estabelece ligação com o WSUS que é executado no ponto de atualização de software. Quando não configura esta conta, o Gestor de Configuração utiliza a conta do computador para o servidor do site ligar ao WSUS. Configure a Conta de Ligação ao Servidor WSUS na página **Definições de Proxy e de Conta** do assistente ou no separador **Definições de Proxy e de Conta** em Propriedades do ponto de atualização de software.  Pode configurar a conta em diferentes locais do assistente, dependendo da versão do Gestor de Configuração que utiliza.  

 Para obter mais informações sobre as contas do Gestor de Configuração, consulte [contas utilizadas.](../../core/plan-design/hierarchy/accounts.md)  

## <a name="synchronization-source"></a>Origem de sincronização  
 Pode configurar a fonte de sincronização a montante para atualizações de software sincronização na página Fonte de **Sincronização** do assistente ou no separador Definições de **Sincronização** nas Propriedades componentes do ponto de atualização de software. As opções de origem de sincronização disponíveis variam consoante o site.  

 Utilize a seguinte tabela para obter as opções disponíveis para configurar o ponto de atualização de software num Web site.  

|Site|Opções de origem de sincronização disponíveis|  
|----------|----------------------------------------------|  
|-   Site de administração central<br />-   Site primário autónomo|-   Sincronizar a partir do site do Microsoft Update<br />-   Sincronizar a partir de uma localização de origem de dados a montante<br />-   Não sincronizar a partir do Microsoft Update nem da origem de dados a montante|  
|-   Pontos de atualização de software adicionais num site<br />-   Site primário subordinado<br />-   Site secundário|-   Sincronizar a partir de uma localização de origem de dados a montante|  

 A seguinte lista contém mais informações sobre cada uma das opções que pode utilizar como origem de sincronização:  

-   **Sincronizar a partir do Microsoft Update**: utilize esta definição para sincronizar os metadados de atualizações de software a partir do Microsoft Update. O site de administração central necessita de ter acesso à Internet, caso contrário a sincronização irá falhar. Esta definição apenas está disponível se configurar o ponto de atualização de software no site de nível superior.  

    > [!NOTE]  
    >  Se existir uma firewall entre o ponto de atualização de software e a Internet, a firewall poderá ter de ser configurada para aceitar as portas HTTP e HTTPS utilizadas pelo Web site do WSUS. Também pode optar por restringir o acesso a domínios limitados na firewall. Para obter mais informações sobre como planear a utilização de uma firewall que suporte atualizações de software, veja [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   Sincronizar a partir de uma localização de fonte de dados a montante : Utilize esta definição para sincronizar as atualizações de software de metadados a partir da fonte de sincronização a montante. ** <a name="BKMK_wsussync"> </a>** Os sites primários subordinados e sites secundários são automaticamente configurados para utilizar o URL do site principal para esta definição. Pode optar por sincronizar as atualizações de software a partir de um servidor WSUS existente. Especifique um `https://WSUSServer:8531`URL, como, onde 8531 é a porta que é usada para ligar ao servidor WSUS.  

-   **Não sincronizar a partir do Microsoft Update nem da origem de dados a montante**: utilize esta definição para sincronizar manualmente as atualizações de software quando o ponto de atualização de software no site de nível superior estiver desligado da Internet. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Se existir uma firewall entre o ponto de atualização de software e a Internet, a firewall poderá ter de ser configurada para aceitar as portas HTTP e HTTPS utilizadas pelo Web site do WSUS. Também pode optar por restringir o acesso a domínios limitados na firewall. Para obter mais informações sobre como planear a utilização de uma firewall que suporte atualizações de software, veja [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Também pode configurar se criar eventos de reporte WSUS na página Fonte de **Sincronização** do assistente ou no separador Definições de **Sincronização** em Propriedades componentes de ponto de atualização de software. O Gestor de Configuração não utiliza estes eventos; portanto, normalmente, escolherá a definição predefinida **Não crie eventos de reporte WSUS**.  

## <a name="synchronization-schedule"></a>Agenda de sincronização  
 Configure o agendamento da sincronização na página **Agendamento da Sincronização** do assistente ou nas Propriedades do Componente do Ponto de Atualização de Software. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

 Se ativar a agenda, poderá configurar uma agenda de sincronização periódica simples ou personalizada. Quando configura um horário simples, a hora de início baseia-se na hora local do computador que executa a consola Do Gestor de Configuração no momento em que cria a programação. Quando configura a hora de início para uma programação personalizada, baseia-se na hora local para o computador que executa a consola Do Gestor de Configuração.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executada num período de tempo que seja adequado ao seu ambiente. Um cenário de típico é a definição da agenda de sincronização de atualizações de software para iniciar a execução poucos instantes após a edição de atualização de segurança regular da Microsoft, na segunda terça-feira de cada mês, vulgarmente designada Patch Terça. Outro cenário típico possível consiste em definir a agenda de sincronização de atualizações de software para ser executada diariamente, caso sejam utilizadas atualizações de software para a entrega de atualizações de definições e de motor do Endpoint Protection.  

> [!NOTE]  
>  Se optar por não ativar a sincronização de atualizações de software com base num agendamento, poderá sincronizar manualmente as atualizações de software a partir do nó **Todas as Atualizações de Software** ou **Grupos de Atualização de Software** na área de trabalho Biblioteca de Software. Para mais informações, consulte [sincronizar atualizações](synchronize-software-updates.md)de software .  

## <a name="supersedence-rules"></a>Regras de substituição  
 Configure as definições de substituição na página **Regras de Substituição** do assistente ou no separador **Regras de Substituição** das Propriedades do Componente do Ponto de Atualização de Software. Apenas pode configurar as regras de substituição no site de nível superior. A partir da versão 1810 do Gestor de Configuração, pode especificar o comportamento das regras de supersedência para **atualizações** de funcionalidades separadamente de **atualizações não-funcionalidades**. <!--3098809, 2977644-->

 Esta página permite especificar que as atualizações de software substituídas expiram de imediato, o que evitará que sejam incluídas nas novas implementações e instrui as implementações existentes para informar que as atualizações de software substituídas contêm uma ou mais atualizações de software expiradas. Em alternativa, pode especificar um prazo para que as atualizações de software substituídas expirem, permitindo-lhe continuar a implementá-las. Para mais informações, consulte [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  A página **Regras de Substituição** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

## <a name="classifications"></a>Classificações  
 Configure as definições de classificações na página de **Classificações** do assistente ou no separador **Classificações** nas Propriedades componentes do ponto de atualização de software. Para obter mais informações sobre as classificações das atualizações de software, veja [Classificações de atualizações](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  A página **Classificações** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Quando instalar o ponto de atualização de software no site de nível superior pela primeira vez, desmarque todas as classificações de atualizações de software. Após a sincronização inicial de atualizações de software, configure as classificações a partir de uma lista atualizada e, em seguida, reinicie o processo de sincronização. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

## <a name="products"></a>Produtos  
 Configure as definições do produto na página de **Produtos** do assistente, ou no separador **Produtos** em Propriedades componentes de ponto de atualização de software.  

> [!NOTE]  
>  A página **Produtos** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Quando instalar o ponto de atualização de software no site de nível superior pela primeira vez, desmarque todos os produtos. Após a sincronização inicial de atualizações de software, configure os produtos a partir de uma lista atualizada e, em seguida, reinicie a sincronização. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

## <a name="languages"></a>Linguagens  
 Configure as definições de idioma na página de **Idioms** do assistente ou no separador **Idiomas** nas propriedades do componente de ponto de atualização de software. Especifique os idiomas e detalhes de resumo que pretende incluir nos ficheiros de sincronização da atualização de software. A definição de Ficheiro de **Atualização** de Software está configurada em cada ponto de atualização de software na hierarquia do Gestor de Configuração. As definições de **Detalhes do Resumo** apenas são configuradas no ponto de atualização de software de nível superior. Para obter mais informações, veja [Idiomas](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  A página **Idiomas** do assistente apenas estará disponível se instalar o ponto de atualização de software no site de administração central. Pode configurar os idiomas do Ficheiro de Atualização do Software em sites subordinados a partir do separador **Idiomas** das Propriedades do Componente do Ponto de Atualização de Software.  

## <a name="third-party-updates"></a>Atualizações de terceiros
Começando na versão 1802 do Gestor de Configuração, pode ativar atualizações de terceiros para clientes do Gestor de Configuração. Quando ativar atualizações de software de terceiros nas propriedades dos componentes SUP, o SUP irá descarregar o certificado de assinatura utilizado pela WSUS para atualizações de terceiros. Esta opção não está disponível durante a instalação do ponto de atualização do software e deve ser configurada após a instalação do SUP. Para ativar as definições do cliente para atualizações de terceiros, consulte o artigo [sobre as definições](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) do cliente.

## <a name="next-steps"></a>Passos seguintes
Instalou o ponto de atualização de software a partir do site mais alto da hierarquia do Gestor de Configuração. Repita os procedimentos deste artigo para instalar o ponto de atualização do software em sites infantis.

Assim que tiver os pontos de atualização do software instalados, vá [sincronizar atualizações](synchronize-software-updates.md)de software .
