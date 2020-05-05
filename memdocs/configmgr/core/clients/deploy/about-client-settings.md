---
title: Definições do cliente
titleSuffix: Configuration Manager
description: Conheça as definições padrão e personalizadas para controlar comportamentos do cliente
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1435c1ab6be8c80178566ae9d354084fddebb22a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771359"
---
# <a name="about-client-settings-in-configuration-manager"></a>Sobre as definições do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Gerencie todas as definições do cliente na consola do Gestor de Configuração a partir do nó de **Definições** do Cliente no espaço de trabalho **da Administração.** O Gestor de Configuração vem com um conjunto de definições predefinidas. Quando altera as definições padrão do cliente, estas definições são aplicadas a todos os clientes da hierarquia. Também pode configurar as definições personalizadas do cliente, que sobrepõem as definições padrão do cliente quando as atribui às coleções. Para mais informações, consulte [Como configurar as definições do cliente](configure-client-settings.md).

As seguintes secções descrevem as definições e opções em mais detalhes.  


## <a name="background-intelligent-transfer-service-bits"></a>Serviço de Transferência Inteligente em Segundo Plano (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitar a largura de banda de rede máxima para transferências BITS em segundo plano

Quando esta opção é **Sim,** os clientes usam o estrangulamento da largura de banda BITS. Para configurar as outras definições deste grupo, tem de ativar esta definição.

### <a name="throttling-window-start-time"></a>Hora de início da janela de limitação

Especifique a hora de início local para a janela de estrangulamento BITS.  

### <a name="throttling-window-end-time"></a>Hora de fim da janela de limitação

Especifique o tempo final local para a janela de estrangulamento BITS. Se o tempo final for igual ao tempo de início da **janela throttling,** o estrangulamento BITS está sempre ativado.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Velocidade máxima de transferência durante a janela de limitação (Kbps)

Especifique a taxa de transferência máxima que os clientes podem usar durante a janela.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Permitir transferências BITS fora da janela de limitação

Permitir que os clientes utilizem definições BITS separadas fora da janela especificada.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Velocidade máxima de transferência fora da janela de limitação (Kbps)

Especifique a taxa de transferência máxima que os clientes podem usar fora da janela de estrangulamento BITS.  



## <a name="client-cache-settings"></a>Definições de cache do cliente

### <a name="configure-branchcache"></a>Configure BranchCache

Configurar o computador cliente para [o Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). Para permitir o cache da BranchCache no cliente, desempre **o 'Enable BranchCache** to **Yes**'

- **Ativar branchCache**: Ativa a BranchCache nos computadores dos clientes.

- Tamanho máximo da **cache BranchCache (percentagem do disco)**: A percentagem do disco que permite a utilização da BranchCache.

> [!TIP]
> Se definir **configure BranchCache** para **No**, então o Gestor de Configuração não configura nenhuma definição branchCache.
>
> Para desativar o BranchCache, **desative** o Conjunto De BranchCache para **Sim**e, em seguida, definir **o Enable BranchCache** para **No**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Configurar o tamanho da cache do cliente

O cache do cliente do Gestor de Configuração nos computadores Windows armazena ficheiros temporários utilizados para instalar aplicações e programas. Se esta opção estiver definida para **Não,** o tamanho padrão é de 5.120 MB.

Se escolher **Sim,** especifique:

- **Tamanho máximo da cache (MB)**
- Tamanho máximo da **cache (percentagem de disco)**: O tamanho da cache do cliente expande-se para o tamanho máximo em megabytes (MB), ou a percentagem do disco, o que for menor.

### <a name="enable-as-peer-cache-source"></a>Ativar como fonte de cache de pares

> [!Note]  
> Na versão 1902 e anterior, esta definição foi nomeada **cliente Enable Configuration Manager em pleno SISTEMA para partilhar conteúdo**. O comportamento da configuração não mudou.

Permite [cache de pares](../../plan-design/hierarchy/client-peer-cache.md) para clientes do Gestor de Configuração. Escolha **Sim**e, em seguida, especifique a porta através da qual o cliente comunica com o computador de pares.

- **Porta para transmissão inicial** de rede (Predefinido UDP 8004): O Gestor de Configuração utiliza esta porta no Windows PE ou no Sistema Operativo Completo do Windows. O motor de sequência de tarefas no Windows PE envia a transmissão para obter localizações de conteúdo antes de iniciar a sequência de tarefas.<!--SCCMDocs issue 910-->

- **Porta para download de conteúdo a partir de pares** (Padrão TCP 8003): O Gestor de Configuração configura automaticamente as regras do Windows Firewall para permitir este tráfego. Se utilizar uma firewall diferente, tem de configurar manualmente as regras para permitir este tráfego.  

    Para mais informações, consulte [as Portas utilizadas para ligações](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>A duração mínima antes do conteúdo em cache pode ser removida (minutos)

<!--4485509-->
A partir da versão 1906, especifique o tempo mínimo para o cliente do Gestor de Configuração manter o conteúdo em cache. Esta definição do cliente define a quantidade mínima de tempo que o agente do Gestor de Configuração deve esperar antes de poder remover o conteúdo da cache no caso de ser necessário mais espaço.

Por defeito, este valor é de 1.440 minutos (24 horas).
O valor máximo para esta definição é de 10.080 minutos (1 semana).

Esta definição confere-lhe um maior controlo sobre a cache do cliente em diferentes tipos de dispositivos. Pode reduzir o valor em clientes que têm pequenos discos rígidos e não precisam de manter o conteúdo existente antes de outra implementação ser executado.


## <a name="client-policy"></a>Política do cliente  

### <a name="client-policy-polling-interval-minutes"></a>Intervalo de consulta da política de cliente (minutos)

Especifica a frequência com que os seguintes clientes do Gestor de Configuração descarregam a política do cliente:

- Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  
- Dispositivos móveis que o Gestor de Configuração matricula  
- Computadores Mac  
- Computadores com o Linux ou UNIX  

Este valor é de 60 minutos por defeito. A redução deste valor faz com que os clientes investiguem o site com mais frequência. Com inúmeros clientes, este comportamento pode ter um impacto negativo no desempenho do site. A [orientação](../../plan-design/configs/size-and-scale-numbers.md) de tamanho e escala baseia-se no valor padrão. Aumentar este valor faz com que os clientes investiguem menos vezes o site. Quaisquer alterações às políticas dos clientes, incluindo novas implementações, demoram mais tempo para os clientes descarregarem e processarem.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Ativar a política do utilizador nos clientes

Quando define esta opção para **Sim**, e utiliza a descoberta do [utilizador,](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)os clientes recebem aplicações e programas direcionados para o utilizador inscrito.  

Se esta definição for **Não,** os utilizadores não recebem as aplicações necessárias que implementa para os utilizadores. Os utilizadores também não recebem quaisquer outras tarefas de gestão nas políticas dos utilizadores.  

Esta definição aplica-se aos utilizadores quando o seu computador está na intranet ou na internet. Tem de ser **Sim,** se também quiser ativar as políticas dos utilizadores na internet.  

> [!Note]  
> A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Não é possível instalar novas funções de catálogo de aplicações.
>
> Se ainda estiver a utilizar o catálogo de aplicações, recebe a lista de software disponível para utilizadores do servidor do site. Assim, esta definição não tem de ser **Sim** para os utilizadores verem e solicitarem aplicações do catálogo de aplicações. Se esta definição for **Não,** os utilizadores não podem instalar as aplicações que vêem no catálogo da aplicação.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Ativar pedidos de política de utilizadores de clientes da Internet

Detete esta opção para **Sim** para que os utilizadores recebam a política do utilizador em computadores baseados na Internet. Aplicam-se igualmente os seguintes requisitos:  

- O cliente e o site estão configurados para [gestão de clientes baseados na Internet](../manage/plan-internet-based-client-management.md) ou um [gateway de gestão](../manage/cmg/plan-cloud-management-gateway.md)de nuvem.  

- A **política de utilizador ativa na** definição de clientes é **Sim**.  

- O ponto de gestão baseado na Internet autentica com sucesso o utilizador utilizando a autenticação do Windows (Kerberos ou NTLM). Para mais informações, consulte [considerações para comunicações de clientes a partir da internet.](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)  

- O portal de gestão de nuvem autentica com sucesso o utilizador utilizando o Diretório Ativo Azure. Para mais informações, consulte [implementar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Se definir esta opção para **Não,** ou qualquer um dos requisitos anteriores não for cumprido, então um computador na internet apenas recebe políticas de computador. Neste cenário, os utilizadores ainda podem ver, solicitar e instalar aplicações a partir de um catálogo de aplicações baseado na Internet. Se esta definição for **Não,** mas ativar a política do **utilizador nos clientes** é **Sim,** os utilizadores não recebem políticas de utilizador até que o computador esteja ligado à intranet.  

> [!NOTE]  
> Para a gestão do cliente baseado na Internet, os pedidos de aprovação de aplicações dos utilizadores não requerem políticas de utilizador ou autenticação do utilizador. O portal de gestão de nuvem não suporta pedidos de aprovação de pedidos.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Ativar a política do utilizador para várias sessões de utilizador

<!--4737447-->

*Aplica-se à versão 1910*

Por predefinição, esta definição está desativada. Mesmo que ative as políticas do utilizador, a partir da versão 1906 o cliente desativa-as por padrão em qualquer dispositivo que permita múltiplas sessões de utilizador ativas simultâneas. Por exemplo, servidores de terminais ou multi-sessão do Windows 10 Enterprise no [Windows Virtual Desktop](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

O cliente só desativa a política do utilizador quando deteta este tipo de dispositivo durante uma nova instalação. Para um cliente existente deste tipo que atualiza para a versão 1906 ou posterior, o comportamento anterior persiste. Num dispositivo existente, configura a definição da política do utilizador mesmo que detete que o dispositivo permite várias sessões de utilizador.

Se necessitar da política do utilizador neste cenário e aceitar qualquer impacto potencial de desempenho, ative a definição do cliente.


## <a name="cloud-services"></a>Serviços em nuvem

### <a name="allow-access-to-cloud-distribution-point"></a>Permitir o acesso ao ponto de distribuição em nuvem

Detete esta opção para **Sim** para os clientes obterem conteúdo a partir de um ponto de distribuição na nuvem. Esta definição não requer que o dispositivo seja baseado na Internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registar automaticamente novos dispositivos de domínio Windows 10 com Diretório Ativo Azure

Quando configura o Diretório Ativo do Azure para suportar a adesão híbrida, o Gestor de Configuração configura os dispositivos do Windows 10 para esta funcionalidade. Para mais informações, consulte [Como configurar dispositivos híbridos Azure Ative Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Permitir que os clientes utilizem um portal de gestão de nuvem

Por padrão, todos os clientes que circulam pela Internet utilizam qualquer gateway de [gestão](../manage/cmg/plan-cloud-management-gateway.md)de nuvem disponível. Um exemplo de quando configurar esta definição para **Não** é para examinar a utilização do serviço, como durante um projeto-piloto ou para economizar custos.



## <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="enable-compliance-evaluation-on-clients"></a>Ativar a avaliação de compatibilidade nos clientes

Detete esta opção para **Sim** configurar as outras definições neste grupo.

### <a name="schedule-compliance-evaluation"></a>Agendar avaliação de compatibilidade

Selecione **Agenda** para criar o calendário predefinido para configurar as implementações de base. Este valor é configurável para cada linha de base na caixa de diálogo de base de **configuração de implementação.**  

### <a name="enable-user-data-and-profiles"></a>Ativar Dados e Perfis de Utilizador

Escolha **Sim** se pretender implementar itens de configuração de dados e perfis do [utilizador.](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md)



## <a name="computer-agent"></a>Agente informático  

### <a name="user-notifications-for-required-deployments"></a>Notificações dos utilizadores para implementações necessárias

Para obter mais informações sobre as seguintes três definições, consulte as [notificações do Utilizador para as implementações necessárias:](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)

- **Prazo de implementação superior a 24 horas, lembre o utilizador de cada (horas)**
- **Prazo de implementação inferior a 24 horas, lembre o utilizador de cada (horas)**
- **Prazo de implementação inferior a 1 hora, lembre o utilizador de cada (minutos)**

### <a name="default-application-catalog-website-point"></a>Ponto de Web sites Predefinido do Catálogo de Aplicações

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

O Gestor de Configuração utiliza esta definição para ligar os utilizadores ao catálogo de aplicações do Software Center. Selecione **Definir website** para especificar um servidor que acolhe o ponto do site do catálogo da aplicação. Introduza o seu nome NetBIOS ou FQDN, especifique a deteção automática ou especifique um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor escolha.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Se esta opção for **Sim,** o cliente adiciona automaticamente o URL do site de catálogo de aplicações padrão atual à zona de sites fidedignas do Internet Explorer.  

Esta definição garante que a definição do Internet Explorer para o Modo Protegido não está ativada. Se o Modo Protegido estiver ativado, o cliente do Gestor de Configuração poderá não ser capaz de instalar aplicações no catálogo da aplicação. Por predefinição, a zona de sites fidedignos também suporta o sessão de entrada do utilizador para o catálogo de aplicações, que requer a autenticação do Windows.  

Se deixar esta opção como **Não,** os clientes do Gestor de Configuração poderão não conseguir instalar aplicações a partir do catálogo de aplicações. Um método alternativo é configurar estas definições do Internet Explorer noutra zona para o URL do catálogo de aplicações que os clientes usam.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada

> [!Important]  
> O cliente não instala automaticamente silverlight.
>
> A partir da versão 1806, a experiência do **utilizador Silverlight** para o ponto de site do catálogo de aplicações já não é suportada. Os utilizadores devem utilizar o novo Centro de Software. Para mais informações, consulte [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Esta definição deve ser **Sim** para os utilizadores utilizarem o catálogo da aplicação.  

Se alterar esta definição, entra em vigor quando os utilizadores carregam o navegador ou atualização da janela do navegador aberta atualmente.  

Para obter mais informações sobre esta definição, consulte [Certificados para microsoft Silverlight 5 e modo](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5)de confiança elevado necessário para o catálogo de aplicações .  

### <a name="organization-name-displayed-in-software-center"></a>Nome da organização apresentada no Centro de Software

Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna. Para mais informações sobre a prioridade deste cenário, consulte [branding Software Center](../../../apps/plan-design/plan-for-software-center.md#branding-software-center).  

### <a name="use-new-software-center"></a>Utilizar o novo Centro de Software

A definição predefinida é **Sim**.

Quando define esta opção para **Sim,** então todos os computadores clientes usam o Centro de Software. O Software Center mostra software, atualizações de software e sequências de tarefas que implementa para utilizadores ou dispositivos.

### <a name="enable-communication-with-health-attestation-service"></a>Ativar a comunicação com o Serviço de Atestação de Saúde

Detete esta opção para **sim** para dispositivos Windows 10 para utilizar [o atestado Health](../../servers/manage/health-attestation.md). Quando ativa esta definição, a seguinte definição também está disponível para configuração.

### <a name="use-on-premises-health-attestation-service"></a>Serviço de Atestação sanitária no local

Detete esta opção para **Sim** para que os dispositivos utilizem um serviço no local. Set to **No** for devices to use the Microsoft cloud service.  

### <a name="install-permissions"></a>Permissões de instalação

Configure como os utilizadores podem instalar software, atualizações de software e sequências de tarefas:  

- **Todos os Utilizadores**: Utilizadores com qualquer permissão, exceto O Hóspede.  

- **Apenas Administradores**: Os utilizadores devem ser membros do grupo de Administradores locais.  

- **Apenas administradores e utilizadores primários:** Os utilizadores devem ser membros do grupo de Administradores locais ou um utilizador primário do computador.  

- **Sem Utilizadores**: Nenhum utilizador que assinou num computador cliente pode instalar software, atualizações de software e sequências de tarefas. As implementações necessárias para o computador instalam-se sempre no prazo limite. Os utilizadores não podem instalar software no Software Center.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Suspender a introdução do PIN do BitLocker após reiniciar

Se os computadores necessitarem de entrada BitLocker PIN, então esta opção ignora o requisito de introduzir um PIN quando o computador reiniciar após uma instalação de software.  

- **Sempre**: O Gestor de Configuração suspende temporariamente o BitLocker depois de ter instalado um software que requer um reinício e iniciou um reinício do computador. Esta definição aplica-se apenas a um reinício do computador iniciado pelo Gestor de Configuração. Esta definição não suspende a obrigação de introduzir o PIN BitLocker quando o utilizador reiniciar o computador. O requisito de entrada bitLocker PIN retoma após o arranque do Windows.

- **Nunca**: O Gestor de Configuração não suspende o BitLocker depois de ter instalado um software que requer um reinício. Neste cenário, a instalação do software não pode terminar até que o utilizador entre no PIN para completar o processo de arranque padrão e carregar o Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>O software adicional gere a implementação de aplicações e atualizações de software

Só ativa esta opção se uma das seguintes condições se aplicar:  

- Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

- Utiliza o kit de desenvolvimento de software Do Gestor de Configuração (SDK) para gerir as notificações do agente cliente e a instalação de aplicações e atualizações de software.  

> [!WARNING]  
> - Se escolher esta opção quando nenhuma destas condições se aplica, o cliente não instala atualizações de software e aplicações necessárias. Esta definição não impede que os utilizadores instalem software disponível a partir do Software Center, incluindo aplicações, pacotes e sequências de tarefas.  
> -  Quando ativar esta definição, as notificações de torradas para novos softwares ou software necessário não ocorrem nos clientes. <!--6347668-->

### <a name="powershell-execution-policy"></a>Política de execução do PowerShell

Configure como os clientes do Gestor de Configuração podem executar scripts Windows PowerShell. Pode utilizar estes scripts para ser detetado em itens de configuração para definições de conformidade. Também pode enviar os scripts numa implementação como um script padrão.  

- **Bypass**: O cliente do Gestor de Configuração contorna a configuração do Windows PowerShell no computador cliente, para que scripts não assinados possam ser executados.  

- **Restrito**: O cliente do Gestor de Configuração utiliza a configuração powerShell atual no computador cliente. Esta configuração determina se os scripts não assinados podem ser executados.  

- **All Signed**: O cliente do Gestor de Configuração só executa scripts se um editor de confiança os tiver assinado. Esta restrição aplica-se independentemente da configuração atual do PowerShell no computador cliente.  

Esta opção requer pelo menos o Windows PowerShell versão 2.0. O padrão é **All Signed**.  

> [!TIP]  
> Se os scripts não assinados não funcionarem devido à definição do cliente, o Gestor de Configuração informa este erro das seguintes formas:  
>
> - O espaço de trabalho **de monitorização** na consola apresenta o erro de erro de implementação ID **0x87D00327**. Também mostra a descrição **script não está assinado**.  
> - Os relatórios mostram o erro do tipo de erro **Discovery**Error . Em seguida, os relatórios mostram o código de erro **0x87D00327** e a descrição **Script não está assinada**, ou código de erro **0x87D00320** e a descrição **O anfitrião**do script ainda não foi instalado . Um relatório exemplo é: **Detalhes de erros de configuração de itens numa linha**de base de configuração para um ativo .  
> - O ficheiro **DcmWmiProvider.log** apresenta que o Script da mensagem **não está assinado (Erro: 87D00327; Fonte: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Mostrar notificações para novas implementações

Escolha **Sim** para apresentar uma notificação para implementações disponíveis por menos de uma semana. Esta mensagem aparece sempre que o agente cliente começa.

### <a name="disable-deadline-randomization"></a>Desativar a aleatoriedade de prazos

Após o prazo de implementação, esta definição determina se o cliente utiliza um atraso de ativação de até duas horas para instalar as atualizações de software necessárias. Por predefinição, o atraso de ativação está desativado.  

Para cenários de infraestrutura de ambiente de trabalho virtual (VDI), este atraso ajuda a distribuir o processamento de CPU e transferência de dados para uma máquina hospedeira com múltiplas máquinas virtuais. Mesmo que não utilize o VDI, ter muitos clientes a instalar as mesmas atualizações ao mesmo tempo pode aumentar negativamente o uso de CPU no servidor do site. Este comportamento também pode abrandar os pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

Se os clientes devem instalar as atualizações de software necessárias no prazo de implementação sem demora, então configure esta definição para **Sim**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Período de graça para execução após prazo de implantação (horas)

Se pretender dar mais tempo aos utilizadores para instalarem as implementações de aplicações ou atualizações de software necessárias para além do prazo, detete te desem a opção para **Sim**. Este período de carência é para um computador desligado por um longo período de tempo, e o utilizador precisa de instalar muitas implementações de aplicações ou atualizações. Por exemplo, esta definição é útil se um utilizador regressar de férias, e tem de esperar muito tempo enquanto o cliente instala implementações de aplicações em atraso.

Detete um período de graça de 1 a 120 horas. Utilize esta definição juntamente com a propriedade de implantação **Atrasar a execução desta implementação de acordo com as preferências do utilizador**. Para mais informações, consulte [aplicações de implementação](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).


## <a name="computer-restart"></a>Reiniciar computador

As seguintes definições devem ser mais curtas em duração do que a janela de manutenção mais curta aplicada ao computador:

- **Apresentar uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)**
- **Exiba uma caixa de diálogo que o utilizador não pode fechar, que apresenta o intervalo de contagem regressiva antes de o utilizador ser desligado ou o computador reiniciar (minutos)**


Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../manage/collections/use-maintenance-windows.md).

- **Especifique a duração do soneto para as notificações de contagem regressiva do computador (minutos)** (a partir da versão 1906)<!--3976435-->
  - O valor padrão é de 240 minutos.
  - O valor da duração do soneto deve ser inferior ao valor de notificação temporária menos o valor da notificação que o utilizador não pode dispensar.
  - Para mais informações, consulte [notificações de reinício do Dispositivo](device-restart-notifications.md).

**Quando uma implementação requer um reinício, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torrada**<!--3555947-->: A partir da versão 1902, configurar esta definição para **Sim** altera a experiência do utilizador para ser mais intrusiva. Esta definição aplica-se a todas as implementações de aplicações, sequências de tarefas e atualizações de software. Para mais informações, consulte [Plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> Em Configuração Manager 1902, sob certas circunstâncias, a caixa de diálogo não substituirá as notificações de torradas. Para resolver este problema, instale o rollup da atualização para a [versão 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)do Gestor de Configuração . <!--4404715-->


## <a name="delivery-optimization"></a>Otimização de Entrega 

<!-- 1324696 -->
Utiliza grupos de limites do Gestor de Configuração para definir e regular a distribuição de conteúdos através da sua rede corporativa e para escritórios remotos. A [Otimização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) de Entrega do Windows é uma tecnologia baseada em nuvem, peer-to-peer para partilhar conteúdos entre dispositivos Windows 10. Configure a Otimização da Entrega para utilizar os seus grupos de fronteira ao partilhar conteúdo entre pares.

> [!Note]
> - A Otimização de Entregas só está disponível nos clientes do Windows 10.
> - O acesso à Internet ao serviço de cloud de otimização de entregas é um requisito para utilizar a sua funcionalidade peer-to-peer. Para obter informações sobre os pontos finais da Internet necessários, consulte [frequentemente perguntas para otimização de entregas.](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
> - Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a [definição](#allow-clients-to-download-delta-content-when-available) de cliente **disponível** estiver ativada. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Utilize grupos de limites do Gestor de Configuração para id do Grupo de Otimização de Entrega

Escolha **Sim** para aplicar o identificador de grupo de limites como o identificador de grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os pares com o conteúdo pretendido.

> [!Note]
> A Microsoft recomenda permitir que o cliente configure esta definição através da política local e não da política de grupo. Isto permite que o identificador de grupo de limites seja definido como o identificador do grupo de otimização de entrega no cliente. Para mais informações, consulte [Otimização de Entrega](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Ativar os dispositivos geridos pelo Gestor de Configuração para utilizar servidores Microsoft Connected Cache para download de conteúdos

<!--3555764-->
Escolha **Sim** para permitir que os clientes descarreguem conteúdo a partir de um ponto de distribuição no local que você ativa como um servidor Microsoft Connected Cache. Para mais informações, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](../../plan-design/hierarchy/microsoft-connected-cache.md)


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> Além das seguintes informações, pode encontrar detalhes sobre a utilização das definições do cliente endpoint Protection no [cenário exemplo: Utilizar a Proteção de Pontofinal para proteger os computadores contra malware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gerir o cliente endpoint protection em computadores clientes

Escolha **Sim** se quiser gerir os clientes existentes de Proteção de Pontofinal e Windows Defender em computadores da sua hierarquia.  

Escolha esta opção se já instalou o cliente Endpoint Protection e pretende geri-la com o Gestor de Configuração. Esta instalação separada inclui um processo scripted que utiliza uma aplicação ou pacote e programa do Gestor de Configuração. Os dispositivos Windows 10 não precisam de ter o agente de proteção endpoint instalado. No entanto, estes dispositivos continuarão a necessitar do **cliente Manage Endpoint Protection em computadores clientes** ativados. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalar o cliente do Endpoint Protection nos computadores cliente

Escolha **Sim** para instalar e ativar o cliente Endpoint Protection em computadores clientes que ainda não estão a executar o cliente. Os clientes do Windows 10 não precisam de ter o agente de proteção endpoint instalado.  

> [!NOTE]  
> Se o cliente Endpoint Protection já estiver instalado, escolher **não** desinstalar o cliente Endpoint Protection. Para desinstalar o cliente Endpoint Protection, defina o **cliente Manage Endpoint Protection na** definição do cliente dos computadores clientes para **O**. Em seguida, implemente um pacote e programa para desinstalar o cliente de Proteção endpoint.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Permitir a instalação do cliente endpoint Protection e reiniciar as janelas de manutenção exteriores. As janelas de manutenção devem ter pelo menos 30 minutos de duração para a instalação do cliente

Detete esta opção para **Sim** para substituir comportamentos típicos de instalação com janelas de manutenção. Esta definição satisfaz os requisitos do negócio para a prioridade da manutenção do sistema para fins de segurança.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Para dispositivos Incorporados windows com filtros de escrita, comprometa a instalação do cliente endpoint Protection (requer reinício)

Escolha **Sim** para desativar o filtro de escrita no dispositivo Windows Embedded e reinicie o dispositivo. Esta ação compromete a instalação no dispositivo.  

Se escolher **O,** o cliente instala-se numa sobreposição temporária que se limpa quando o dispositivo reinicia. Neste cenário, o cliente Endpoint Protection não instala totalmente até que outra instalação cometa alterações no dispositivo. Esta configuração é a predefinição.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Suprimir qualquer reinício de computador necessário após a instalação do cliente Endpoint Protection

Escolha **Sim** para suprimir um reinício do computador após a instalação do cliente Endpoint Protection.  

> [!IMPORTANT]  
> Se o cliente endpoint Protection necessitar de um reinício do computador e esta definição for **Não,** então o computador reinicia independentemente de quaisquer janelas de manutenção configuradas.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>O período de tempo permitido pode adiar um reinício obrigatório para completar a instalação de proteção do ponto final (horas)

Se for necessário reiniciar após a instalação do cliente Endpoint Protection, esta definição especifica o número de horas que os utilizadores podem adiar o reinício necessário. Esta definição requer que a definição para **suprimir qualquer computador necessário reinicie após a instalação do cliente endpoint Protection** é **Nº**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Desative fontes alternativas (tais como Microsoft Windows Update, Microsoft Windows Server Update Services ou unC shares) para a atualização de definição inicial nos computadores dos clientes

Escolha **Sim** se quiser que o Gestor de Configuração instale apenas a atualização de definição inicial nos computadores dos clientes. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda da rede, durante a instalação inicial da atualização de definição.  



## <a name="enrollment"></a>Inscrição

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalo de sondagens para clientes legados de dispositivos móveis

Selecione **set Interval** para especificar o tempo, em minutos ou horas, que os dispositivos móveis legados pesquisam para a política. Estes dispositivos incluem plataformas como Windows CE, Mac OS X e Unix ou Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervalo de votação para dispositivos modernos (minutos)

Insira o número de minutos que os dispositivos modernos pesquisam para a política. Esta definição destina-se a dispositivos Windows 10 que são geridos através da gestão de dispositivos móveis no local.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Permitir que os utilizadores matriculem dispositivos móveis e computadores Mac

Para permitir a inscrição baseada no utilizador de dispositivos legados, defina esta opção para **Sim**, e, em seguida, configure a seguinte definição:

- **Perfil de inscrição**: Selecione **Definir Perfil** para criar ou selecionar um perfil de inscrição. Para mais informações, consulte as definições do [cliente configurar para inscrição.](deploy-clients-to-macs.md#configure-client-settings)

### <a name="allow-users-to-enroll-modern-devices"></a>Permitir que os utilizadores matriculem dispositivos modernos

Para permitir a inscrição baseada no utilizador de dispositivos modernos, defina esta opção para **Sim**, e, em seguida, configure a seguinte definição:

- Perfil de **inscrição de dispositivo moderno**: Selecione Definir **Perfil** para criar ou selecionar um perfil de inscrição. Para mais informações, consulte [Criar um perfil de inscrição que permita aos utilizadores inscreverem dispositivos modernos](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Inventário de Hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Ativar o inventário de hardware nos clientes

Por defeito, esta definição é **Sim**. Para mais informações, consulte Introdução ao inventário de [hardware](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Calendário de inventário de hardware

Selecione **Agenda** para ajustar a frequência que os clientes executam o ciclo de inventário de hardware. Por padrão, este ciclo ocorre a cada sete dias.

### <a name="maximum-random-delay-minutes"></a>Atraso aleatório máximo (minutos)

Especifique o número máximo de minutos para o cliente do Gestor de Configuração aleatoriamente o ciclo de inventário de hardware a partir do horário definido. Esta aleatoriedade em todos os clientes ajuda a processar o inventário de equilíbrio de carga no servidor do site. Pode especificar qualquer valor entre 0 e 480 minutos. Por predefinição, este valor é definido para 240 minutos (4 horas).

### <a name="maximum-custom-mif-file-size-kb"></a>Tamanho máximo do ficheiro MIF personalizado (KB)

Especifique o tamanho máximo, em kilobytes (KB), permitido para cada ficheiro personalizado de Formato de Informação de Gestão (MIF) que o cliente recolhe durante um ciclo de inventário de hardware. O agente de inventário de hardware do Gestor de Configuração não processa ficheiros MIF personalizados que excedam este tamanho. Pode especificar um tamanho de 1 KB a 5.120 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro regular de dados de inventário de hardware.  

> [!NOTE]  
> Esta definição está disponível apenas nas definições padrão do cliente.  

### <a name="hardware-inventory-classes"></a>Classes de inventário de hardware

Selecione **Definir Classes** para alargar as informações de hardware que recolhe dos clientes sem editar manualmente o ficheiro sms_def.mof. Para mais informações, consulte [Como configurar o inventário](../manage/inventory/configure-hardware-inventory.md)de hardware .  

### <a name="collect-mif-files"></a>Recolher ficheiros MIF

Utilize esta definição para especificar se recolhe ficheiros MIF dos clientes do Gestor de Configuração durante o inventário de hardware.  

Para que um ficheiro MIF seja recolhido por inventário de hardware, deve estar na localização correta no computador cliente. Por predefinição, os ficheiros encontram-se nos seguintes caminhos:  

- **Os ficheiros IDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Idmif.

- **Os ficheiros NOIDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
> Esta definição está disponível apenas nas definições padrão do cliente.



## <a name="metered-internet-connections"></a>Ligações de internet medidos  

Gerencie como o Windows 8 e os computadores posteriores utilizam ligações de internet medid para comunicar com o Gestor de Configuração. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que enviam e recebem quando estão numa ligação à Internet com medido.  

> [!NOTE]  
> A definição configurada do cliente não é aplicada nos seguintes cenários:  
>
> - Se o computador estiver numa ligação de dados de roaming, o cliente do Gestor de Configuração não executa quaisquer tarefas que exijam que os dados sejam transferidos para sites do Gestor de Configuração.  
> - Se as propriedades de ligação à rede Windows estiverem configuradas como não medidos, o cliente do Gestor de Configuração comporta-se como se a ligação não estivesse ser metida, transfere assim dados para o site.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicação do cliente sobre ligações à Internet medidos

Escolha uma das seguintes opções para esta definição:  

- **Permitir**: Todas as comunicações do cliente são permitidas através da ligação à Internet medido, a menos que o dispositivo cliente esteja usando uma ligação de dados de roaming.  

- **Limite**: Apenas são permitidas as seguintes comunicações de clientes através da ligação à Internet medido:  

    - Obtenção de políticas de cliente  

    - Mensagens de estado de cliente a enviar para o site  

    - Pedidos de instalação de software do Centro de Software  

    - Implementações necessárias (quando for atingido o prazo de instalação)  

    > [!IMPORTANT]  
    > O cliente permite sempre instalações de software do Software Center, independentemente das definições de ligação à Internet medidos.  

    Se o cliente atingir o limite de transferência de dados para a ligação à Internet medido, o cliente já não tenta comunicar com os sites do Gestor de Configuração.  

- **Bloco**: O cliente do Gestor de Configuração não tenta comunicar com sites do Gestor de Configuração quando está numa ligação de internet medido. Esta é a opção predefinida.  



## <a name="power-management"></a>Gestão de energia  

### <a name="allow-power-management-of-devices"></a>Permitir a gestão de energia dos dispositivos

Detete esta opção para **Sim** para ativar a gestão de energia nos clientes. Para mais informações, consulte [Introdução à gestão de energia.](../manage/power/introduction-to-power-management.md)

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia

Escolha **Sim** para permitir que os utilizadores do Software Center excluam o seu computador de quaisquer definições de gestão de energia configuradas.  

### <a name="allow-network-wake-up"></a>Permitir o despertar da rede

Adicionado em 1810. Quando definido para **ativar,** configura as definições de alimentação do adaptador de rede para permitir que o adaptador de rede acorde o dispositivo. Quando programado para **desativar,** as definições de alimentação do adaptador de rede estão configuradas para não permitir que o adaptador de rede acorde o dispositivo.

### <a name="enable-wake-up-proxy"></a>Ativar reativação proxy

Especifique **Sim** para complementar a definição wake on LAN do site, quando estiver configurado para pacotes unicast.  

Para mais informações sobre o wake-up proxy, consulte [Plan como acordar os clientes](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Não permita o wake-up proxy numa rede de produção sem primeiro entender como funciona e avaliá-lo em um ambiente de teste.  

Em seguida, configure as seguintes definições adicionais conforme necessário:

- Número de **porta de procuração de despertar (UDP)**: O número de porta que os clientes usam para enviar pacotes de despertar para computadores adormecidos. Mantenha a porta padrão 25536 ou mude o número para um valor à sua escolha.  

- Wake On LAN número de **porta (UDP)**: Mantenha o valor padrão de 9, a menos que tenha alterado o número da porta Wake On LAN (UDP) no separador **Ports** do site **Propriedades**.  

    > [!IMPORTANT]  
    > Este número tem de corresponder ao número nas **Propriedades**do site. Se alterar este número num só local, não é automaticamente atualizado no outro local.  

- **Exceção do Windows Defender Firewall para procuração de despertar**: O cliente do Gestor de Configuração configura automaticamente o número de porta proxy de despertar em dispositivos que executam o Windows Defender Firewall. **Selecione Configurar** para especificar os perfis de firewall desejados.  

    Se os clientes executarem uma firewall diferente, configure-a manualmente para permitir o número de porta de **procuração wake-up (UDP)**.  

- **Os prefixos IPv6 se necessário para o DirectAccess ou outros dispositivos de rede intervenientes. Utilize uma vírina para especificar várias entradas**: Introduza os prefixos IPv6 necessários para que o proxy de despertar funcione na sua rede.



## <a name="remote-tools"></a>Ferramentas remotas  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Ativar o Controlo Remoto nos clientes e perfis de exceção firewall

**Selecione Configurar** para ativar a função de controlo remoto do Gestor de Configuração. Opcionalmente, configure as definições de firewall para permitir que o controlo remoto funcione em computadores clientes.  

Por predefinição, o controlo remoto encontra-se desativado.  

> [!IMPORTANT]  
> Se não configurar as definições de firewall, o telecomando pode não funcionar corretamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software

Escolha se os utilizadores podem alterar opções de controlo remoto a partir do Centro de Software.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Permitir o Controlo Remoto de um computador autónomo

Escolha se um administrador pode usar o telecomando para aceder a um computador cliente que esteja desligado ou bloqueado. Apenas um computador ligado e desbloqueado pode ser controlado remotamente quando esta definição é desativada.  

### <a name="prompt-user-for-remote-control-permission"></a>Solicitar ao utilizador permissão do Controlo Remoto

Escolha se o computador cliente mostra uma mensagem pedindo a permissão do utilizador antes de permitir uma sessão de controlo remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Solicitação do utilizador para a permissão para transferir conteúdo de clipboard partilhado

Antes de transferir conteúdo da área de transferência partilhada numa sessão de controlo remoto, permita aos seus utilizadores aceitar ou negar transferências de ficheiros. Os utilizadores só precisam de conceder permissão uma vez por sessão. O espectador não pode dar-se permissão para transferir o ficheiro.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Conceder permissão de Controlo Remoto ao grupo de Administradores local

Escolha se os administradores locais no servidor que inicia maquete seleções de controlo remoto podem estabelecer sessões de controlo remoto para computadores clientes.  

### <a name="access-level-allowed"></a>Nível de acesso permitido

Especifique o nível de acesso ao telecomando para permitir. Escolha entre as seguintes definições:  

- **Sem Acesso**
- **Ver Apenas**
- **Controlo Total**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Espectadores autorizados de Controlo Remoto e Assistência Remota

Selecione **Definir Visualizações** para especificar os nomes dos utilizadores do Windows que podem estabelecer sessões de controlo remoto para computadores clientes.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostrar ícone de notificação de sessão na barra de tarefas

Configure esta definição para **Sim** para mostrar um ícone na barra de tarefas do Windows do cliente para indicar uma sessão de controlo remoto ativo.  

### <a name="show-session-connection-bar"></a>Mostrar barra de ligação da sessão

Detete esta opção para **Sim** para mostrar uma barra de conexão de sessão de alta visibilidade nos clientes, para indicar uma sessão de controlo remoto ativo.  

### <a name="play-a-sound-on-client"></a>Reproduzir um som no cliente

Detete esta opção para utilizar o som para indicar quando uma sessão de controlo remoto está ativa num computador cliente. Selecione uma das seguintes opções:

- **Sem som**
- **Início e fim da sessão** (padrão)
- **Repetidamente durante a sessão**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gerir definições da Assistência Remota não solicitada

Configure esta definição para **Sim** para permitir que o Gestor de Configuração gere sessões de assistência remota não solicitadas.  

Numa sessão de Assistência Remota Não Solicitada, o utilizador do computador cliente não solicitou assistência para iniciar a sessão.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gerir definições da Assistência Remota solicitada

Detete esta opção para **Sim** para permitir que o Gestor de Configuração gere as sessões de assistência remota solicitadas.  

Numa sessão de assistência remota solicitada, o utilizador do computador cliente enviou um pedido ao administrador para assistência remota.  

### <a name="level-of-access-for-remote-assistance"></a>Nível de acesso para a Assistência Remota

Escolha o nível de acesso a atribuir às sessões de Assistência Remota que são iniciadas na consola 'Gestor de Configuração'. Selecione uma das seguintes opções:

- **Nenhum** (predefinição)
- **Visualização remota**
- **Controlo Total**

> [!NOTE]  
> O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

### <a name="manage-remote-desktop-settings"></a>Gerir definições de Ambiente de Trabalho Remoto

Detete esta opção para **Sim** para permitir que o Gestor de Configuração gere as sessões de ambiente de trabalho remotos para computadores.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Permitir que os visualizadores autorizados estabeleçam ligação utilizando a ligação ao Ambiente de Trabalho Remoto

Detete esta opção para **Sim** adicionar utilizadores especificados na lista de espectadores permitida ao grupo de utilizadores local Remote Desktop nos clientes.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Exigir autenticação de nível de rede nos computadores com o sistema operativo Windows Vista e versões posteriores

Detete esta opção para **Sim** usar a autenticação de nível de rede (NLA) para estabelecer ligações de Ambiente de Trabalho Remoto aos computadores clientes. O NLA necessita inicialmente de menos recursos informáticos remotos, pois termina a autenticação do utilizador antes de estabelecer uma ligação remote Desktop. Usar o NLA é uma configuração mais segura. A NLA ajuda a proteger o computador de utilizadores ou software maliciosos, e reduz o risco de ataques de negação de serviço.  



## <a name="software-center"></a>Centro de Software

### <a name="select-these-new-settings-to-specify-company-information"></a>Selecione estas novas definições para especificar informações da empresa

Detete esta opção para **Sim**e, em seguida, especifique as seguintes definições para o Centro de Software da marca para a sua organização:

- **Nome**da empresa : Introduza o nome da organização que os utilizadores vêem no Centro de Software.  

- **Esquema de cores para Centro**de Software : Clique em **Selecionar Cor** para definir a cor primária utilizada pelo Centro de Software.  

- **Selecione um logótipo para Software Center**: Clique em **Navegar** para selecionar uma imagem para aparecer no Centro de Software. O logótipo deve ser um JPEG, PNG ou BMP de 400 x 100 pixels, com um tamanho máximo de 750 KB. O nome do logotipo não deve conter espaços.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a>Ocultar aplicações não aprovadas no Centro de Software

Quando ativa esta opção, as aplicações disponíveis pelo utilizador que requerem aprovação estão escondidas no Software Center.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a>Ocultar aplicações instaladas no Centro de Software

Quando ativa esta opção, as aplicações que já estão instaladas já não aparecem no separador Aplicações. Esta opção é definida como predefinição quando instala ou atualiza para O Gestor de Configuração 1802. As aplicações instaladas ainda estão disponíveis para revisão ao abrigo do separador de estado de instalação. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a>Ocultar link de catálogo de aplicações no Centro de Software

Especifique a visibilidade do link do site do catálogo de aplicações no Software Center. Quando esta opção for definida, os utilizadores não verão o link do site do catálogo de aplicações no nó de estado de instalação do Software Center. <!--1358214-->

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  

### <a name="software-center-tab-visibility"></a>Visibilidade do separador do Software Center

#### <a name="starting-in-version-1906"></a>Começando na versão 1906
<!--4063773-->

Escolha quais separadores devem ser visíveis no Centro de Software. Utilize o botão **Adicionar** para mover um separador para **separadores visíveis**. Utilize o botão **Remover** para movê-lo para a lista **de separadores escondidos.** Encomende os separadores utilizando os botões **Mover Para Cima** ou Mover para **baixo.** 

Separadores disponíveis:
- **Aplicações**
- **Updates**
- **Sistemas Operativos**
- **Estado de instalação**
- **Conformidade do Dispositivo**
- **Opções**
- Adicione até 5 separadores personalizados clicando no botão **'Adicionar'.**
  - Especifique o **nome do separador** e o **URL de Conteúdo** para o seu separador personalizado.
  - Clique em **Eliminar o Separador** para remover um separador personalizado.  

  >[!Important]  
  > - Algumas funcionalidades do site podem não funcionar ao usá-lo como um separador personalizado no Software Center. Certifique-se de testar os resultados antes de o implementar aos clientes. <!--519659-->
  > - Especifique apenas endereços de website fidedignos ou intranet quando adicionar um separador personalizado.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Versão 1902 e anterior

Configure as definições adicionais deste grupo para **Sim** para tornar visíveis os seguintes separadores no Centro de Software:

- **Aplicações**
- **Updates**
- **Sistemas Operativos**
- **Estado de instalação**
- **Conformidade do Dispositivo**
- **Opções**
- **Especifique um separador personalizado para o Centro de Software** <!--1358132-->
    - **Nome do separador**
    - **URL de conteúdo**

    >[!Important]  
    > Algumas funcionalidades do site podem não funcionar ao usá-lo como um separador personalizado no Software Center. Certifique-se de testar os resultados antes de o implementar aos clientes. <!--519659-->
    >
    > Especifique apenas endereços de website fidedignos ou intranet quando adicionar um separador personalizado.<!--SCCMDocs issue 1575-->

Por exemplo, se a sua organização não utilizar as políticas de conformidade e quiser ocultar o separador de conformidade do dispositivo no Centro de Software, defino o **separador Enable Device Compliance** para **No**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a>Configurar vistas padrão no Centro de Software
<!--3612112-->
*(Introduzido na versão 1902)*

- Configure o filtro de **aplicação Predefinido** como **todas** ou apenas aplicações **necessárias.**  

  - O Software Center utiliza sempre a definição predefinida. Os utilizadores podem alterar este filtro, mas o Software Center não persiste a sua preferência.  

- Detete a vista de **aplicação Predefinida** como **vista para azulejos** ou **para a visualização da lista**. 

  - Se um utilizador alterar esta configuração, o Software Center persiste a preferência do utilizador no futuro. 


## <a name="software-deployment"></a>Implementação de software  

### <a name="schedule-re-evaluation-for-deployments"></a>Agendar reavaliação das implementações

Configure um horário para quando o Gestor de Configuração reavaliar as regras de requisitos para todas as implementações. O valor padrão é a cada sete dias.  

> [!IMPORTANT]  
> Esta definição é mais invasiva para o cliente local do que para a rede ou servidor do site. Um calendário de reavaliação mais agressivo afeta negativamente o desempenho da sua rede e computadores clientes. A Microsoft não recomenda definir um valor inferior ao predefinido. Se alterar este valor, monitorize de perto o desempenho.  

Inicie esta ação a partir de um cliente da seguinte forma: no painel de controlo do Gestor de **Configuração,** a partir do separador **Ações,** selecione O Ciclo de Avaliação de Implementação de **Aplicações**.  



## <a name="software-inventory"></a>Inventário de software  

### <a name="enable-software-inventory-on-clients"></a>Ativar o inventário de software nos clientes

Esta opção está definida para **Sim** por padrão. Para mais informações, consulte [Introdução ao inventário de software](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Agendar inventário de software e recolha de ficheiros

Selecione **Agenda** para ajustar a frequência que os clientes executam os ciclos de inventário de software e recolha de ficheiros. Por padrão, este ciclo ocorre a cada sete dias.

### <a name="inventory-reporting-detail"></a>Inventariar detalhe de relatórios

Especifique um dos seguintes níveis de informação de ficheiros para o inventário:

- **Arquivar apenas**
- **Apenas produto**
- **Detalhes completos** (padrão)

### <a name="inventory-these-file-types"></a>Inventariar estes tipos de ficheiro

Se pretender especificar os tipos de ficheiros para o inventário, selecione Tipos de **Conjuntos**e, em seguida, configure as seguintes opções:  

> [!NOTE]  
> Se várias definições personalizadas do cliente forem aplicadas a um computador, o inventário de que cada definição devolve é fundido.  

- Selecione **Novo** para adicionar um novo tipo de ficheiro ao inventário. Em seguida, especifique as seguintes informações na caixa de diálogo **Inventariada File Properties:**  

    - **Nome**: Forneça um nome para o ficheiro que pretende inventariar. Utilize um wildcard`*`asterisco para representar qualquer série de`?`texto, e um ponto de interrogação ( ) para representar qualquer personagem único. Por exemplo, se pretender inventariar todos os ficheiros com `*.doc`a extensão .doc, especifique o nome do ficheiro .  

    - **Localização**: Selecione **set** para abrir a caixa de diálogo **Path Properties.** Configure o inventário de software para pesquisar todos os discos rígidos do `C:\Folder`cliente para o ficheiro especificado, `%windir%`procure um caminho especificado (por exemplo, ) ou procure uma variável especificada (por exemplo, ). Também pode pesquisar todas as subpastas sob o caminho especificado.  

    - **Excluir ficheiros encriptados e comprimidos**: Quando escolher esta opção, quaisquer ficheiros comprimidos ou encriptados não são inventariados.  

    - **Excluir ficheiros na pasta Windows**: Quando escolher esta opção, quaisquer ficheiros na pasta Windows e nas suas subpastas não são inventariados.  

    Selecione **OK** para fechar a caixa de diálogo **Inventoried File Properties.** Adicione todos os ficheiros que pretende inventariar e, em seguida, selecione **OK** para fechar a caixa de diálogo Configurar a Definição de **Cliente.**  

### <a name="collect-files"></a>Recolher ficheiros

Se pretender recolher ficheiros de computadores clientes, selecione **'Ficheiros'** e, em seguida, configure as seguintes definições:  

> [!NOTE]  
> Se várias definições personalizadas do cliente forem aplicadas a um computador, o inventário de que cada definição devolve é fundido.  

- Na caixa de diálogo Configurar definição de **cliente,** selecione **New** para adicionar um ficheiro a recolher.  

- Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

    - **Nome**: Forneça um nome para o ficheiro que pretende recolher. Utilize um wildcard`*`asterisco para representar qualquer série de`?`texto, e um ponto de interrogação ( ) para representar qualquer personagem único.  

    - **Localização**: Selecione **set** para abrir a caixa de diálogo **Path Properties.** Configure o inventário de software para pesquisar todos os discos rígidos do cliente para `C:\Folder`o ficheiro que pretende recolher, `%windir%`pesquisar um caminho especificado (por exemplo, ou procurar uma variável especificada (por exemplo, ). Também pode pesquisar todas as subpastas sob o caminho especificado.  

    - **Excluir ficheiros encriptados e comprimidos**: Quando escolher esta opção, não são recolhidos ficheiros comprimidos ou encriptados.  

    - Pare a **recolha de ficheiros quando o tamanho total dos ficheiros exceder (KB)**: Especifique o tamanho do ficheiro, em kilobytes (KB), após o que o cliente deixa de recolher os ficheiros especificados.  

    > [!NOTE]  
    > O servidor do site recolhe as cinco versões mais recentemente alteradas de ficheiros recolhidos e armazena-as no `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` diretório. Se um ficheiro não tiver mudado desde o último ciclo de inventário de software, o ficheiro não será recolhido novamente.  
    >
    > O inventário de software não recolhe ficheiros superiores a 20 MB.  
    >
    > O **valor Tamanho Máximo para todos os ficheiros recolhidos (KB)** na caixa de diálogo **Configurar** Definição de Cliente mostra o tamanho máximo para todos os ficheiros recolhidos. Quando este tamanho é atingido, a recolha de ficheiros para. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

    > [!IMPORTANT]
    > Se configurar o inventário de software para recolher muitos ficheiros grandes, esta configuração pode afetar negativamente o desempenho da sua rede e servidor de site.  

    Para obter informações sobre como visualizar ficheiros recolhidos, consulte [como utilizar o Resource Explorer para visualizar](../manage/inventory/use-resource-explorer-to-view-software-inventory.md)o inventário de software .  

    Selecione **OK** para fechar a caixa de diálogo **Collected File Properties.** Adicione todos os ficheiros que pretende recolher e, em seguida, selecione **OK** para fechar a caixa de diálogo Configurar a Definição de **Cliente.**  

### <a name="set-names"></a>Definir Nomes

O agente de inventário de software recupera os nomes do fabricante e do produto a partir de informações sobre o cabeçalho do ficheiro. Estes nomes nem sempre são padronizados na informação do cabeçalho do ficheiro. Quando vê o inventário de software no Resource Explorer, podem surgir versões diferentes do mesmo fabricante ou nome do produto. Para normalizar estes nomes de exibição, selecione **Definir Nomes**e, em seguida, configurar as seguintes definições:  

- **Tipo de nome**: O inventário de software recolhe informações sobre fabricantes e produtos. Escolha se pretende configurar os nomes de exibição para um **Fabricante** ou um **Produto**.  

- Nome do **mostrador**: Especifique o nome do visor que pretende utilizar no lugar dos nomes na lista de **nomes inventariados.** Para especificar um novo nome de exibição, selecione **New**.  

- **Nomes inventariados**: Para adicionar um nome inventariado, selecione **New**. Este nome é substituído no inventário de software pelo nome escolhido na lista de **nomes display.** Pode adicionar vários nomes para substituir.  



## <a name="software-metering"></a>Medição de Software

### <a name="enable-software-metering-on-clients"></a>Ativar a medição de software nos clientes

Esta definição está definida para **Sim** por padrão. Para mais informações, consulte a [medição do Software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Agendar recolha de dados

Selecione **Agenda** para ajustar a frequência que os clientes executam o ciclo de medição de software. Por padrão, este ciclo ocorre a cada sete dias.



## <a name="software-updates"></a>Atualizações de software  

### <a name="enable-software-updates-on-clients"></a>Ativar atualizações de software nos clientes

Utilize esta definição para permitir atualizações de software nos clientes do Gestor de Configuração. Quando desativa esta definição, o Gestor de Configuração remove as políticas de implementação existentes dos clientes. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

> [!IMPORTANT]  
> Quando desativar esta definição, as políticas de conformidade que dependem de atualizações de software deixarão de funcionar.  

### <a name="software-update-scan-schedule"></a>Agendamento da análise de atualização de software

Selecione **Agenda** para especificar com que frequência o cliente inicia uma avaliação de conformidade. Esta digitalização determina o estado para atualizações de software no cliente (por exemplo, necessárias ou instaladas). Para mais informações sobre a avaliação de compatibilidade, consulte [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Por padrão, esta varredura usa um simples horário para iniciar a cada sete dias. Pode criar um horário personalizado. Pode especificar um dia e hora exatos, utilizar o Tempo Coordenado Universal (UTC) ou a hora local, e configurar o intervalo recorrente para um dia específico da semana.  

> [!NOTE]  
> Se especificar um intervalo inferior a um dia, o Gestor de Configuração falha automaticamente num dia.  

> [!WARNING]  
> O tempo de início real nos computadores dos clientes é a hora de início mais uma quantidade aleatória de tempo, até duas horas. Esta aleatoriedade impede que os computadores clientes iniciem a verificação e simultaneamente se conectem ao ponto de atualização de software ativo.  

### <a name="schedule-deployment-re-evaluation"></a>Agendar a reavaliação de implementação

Selecione **Agenda** para configurar a frequência com que o agente cliente atualiza o agente cliente reavalia as atualizações de software para o estado de instalação nos computadores clientes do Gestor de Configuração. Quando as atualizações de software previamente instaladas já não são encontradas nos clientes, mas ainda são necessárias, o cliente reinstala as atualizações do software.

Ajuste este calendário com base na política da empresa para a conformidade com a atualização de software e se os utilizadores podem desinstalar atualizações de software. Cada ciclo de reavaliação de implementação resulta na atividade do processador de computador de rede e cliente. Por predefinição, esta definição utiliza um calendário simples para iniciar a reavaliação de implementação de sete em sete dias.  

> [!NOTE]  
> Se especificar um intervalo inferior a um dia, o Gestor de Configuração falha automaticamente num dia.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Quando qualquer prazo de implementação de atualização de software for atingido, instale todas as outras implementações de atualizações de software com prazo dentro de um período de tempo especificado

Detete esta opção para **Sim** instalar todas as atualizações de software a partir de implementações necessárias com prazos que ocorram dentro de um período de tempo especificado. Quando uma implementação de atualização de software necessária atinge um prazo, o cliente inicia a instalação para as atualizações de software na implementação. Esta definição determina se deve instalar atualizações de software a partir de outras implementações necessárias que tenham um prazo dentro do tempo especificado.  

Utilize esta definição para acelerar a instalação para atualizações de software necessárias. Esta definição também tem o potencial de aumentar a segurança do cliente, diminuir as notificações ao utilizador e diminuir o reinício do cliente. Por predefinição, esta definição encontra-se definida como **Não**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas

Utilize esta definição para especificar o período de tempo para a definição anterior. Pode introduzir um valor de 1 a 23 horas e de 1 a 365 dias. Por predefinição, esta definição está configurada durante sete dias.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Permitir que os clientes descarreguem conteúdo delta quando disponíveis

*(Introduzido na versão 1902)*

Detete esta opção para **Sim** para permitir que os clientes utilizem ficheiros de conteúdo delta. Esta definição permite ao Windows Update Agent no dispositivo determinar que conteúdo é necessário e descarregá-lo seletivamente. 

- Antes de ativar esta definição do cliente, certifique-se de que a Otimização de Entrega está configurada adequadamente para o seu ambiente. Para mais informações, consulte a [Otimização da Entrega do Windows](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) e a definição do cliente de Otimização de [Entrega.](#delivery-optimization)
 - Esta definição de cliente substitui **Ativar a instalação de ficheiros de instalação Express nos clientes.** Detete esta opção para **Sim** para permitir que os clientes utilizem ficheiros de instalação expresso. Para mais informações, consulte os ficheiros de [instalação do Manage Express para atualizações do Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - A partir da versão 1910 do 'Gestor de Configuração', quando esta opção está definida, o download da Delta é utilizado para todos os ficheiros de instalação de atualização do Windows, e não apenas para ficheiros de instalação expresso.
    - Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a definição de cliente **disponível** estiver ativada. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Porto que os clientes usam para receber pedidos de conteúdo delta

*(Introduzido na versão 1902)*

Esta configuração configura a porta local para o ouvinte HTTP para descarregar conteúdo delta. Está definido para 8005 por defeito. Não precisas de abrir este porto na firewall do cliente. 

> [!NOTE]
>Esta definição de cliente substitui a **Porta utilizada para descarregar conteúdos para ficheiros**de instalação Express .


### <a name="enable-management-of-the-office-365-client-agent"></a>Ativar a gestão do Agente Cliente do Office 365

Quando define esta opção para **Sim,** permite a configuração das definições de instalação do Office 365. Também permite descarregar ficheiros das Redes de Entrega de Conteúdos do Office (CDNs) e implementar os ficheiros como uma aplicação no Gestor de Configuração. Para mais informações, consulte Gerir o [Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a>Ativar a instalação de atualizações de software na janela de manutenção "Todas as implementações" quando estiver disponível a janela de manutenção "Software Update"

A partir da versão 1810, quando definir esta opção para **Sim** e o cliente tiver pelo menos uma janela de manutenção "Software Update" definida, as atualizações de software serão instaladas durante uma janela de manutenção "Todas as implementações".

Por predefinição, esta definição encontra-se definida como **Não**. Este valor usa o mesmo comportamento que antes: se ambos os tipos existirem, ignora a janela. <!--2839307-->

> [!NOTE]
> Esta definição também se aplica às janelas de manutenção que configura para aplicar às sequências de **tarefas**.<!-- SCCMDocs-pr #4596 -->
>
> Se o cliente tiver apenas uma janela **de implementações All** disponível, ainda instala atualizações de software ou sequências de tarefas nessa janela.

#### <a name="maintenance-window-example"></a>Exemplo de janela de manutenção

Por exemplo, configura as seguintes janelas de manutenção:

- **Todas as colocações**: 02:00 - 04:00
- **Atualizações de software**: 04:00 - 06:00

Por predefinição, o cliente apenas instala atualizações de software durante a segunda janela de manutenção. Ignora a janela de manutenção para todas as implementações neste cenário. Quando muda esta definição para **Sim,** o cliente instala atualizações de software entre as 02:00 e as 06:00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a>Especificar prioridade de linha para atualizações de funcionalidades

<!--3734525-->
A partir da versão 1902 do Gestor de Configuração, pode ajustar a prioridade com que os clientes do Windows 10 instalam uma atualização de funcionalidadeatravés da [manutenção do Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Esta definição não tem qualquer impacto nas sequências de tarefas de atualização do Windows 10 no local.

Esta definição de cliente fornece as seguintes opções:

- **Não Configurado**: O Gestor de Configuração não altera a definição. Os administradores podem pré-encenar o seu próprio ficheiro setupconfig.ini. este valor é a predefinição.

- **Normal**: O Windows Setup utiliza mais recursos do sistema e atualizações mais rapidamente. Utiliza mais tempo de processador, pelo que o tempo total de instalação é mais curto, mas a paragem do utilizador é mais longa.  

    - Configura o ficheiro configuraçãoconfig.ini no `/Priority Normal` dispositivo com a opção de [linha de comando de configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Baixo**: Pode continuar a trabalhar no dispositivo enquanto descarrega e atualiza em segundo plano. O tempo total de instalação é mais longo, mas a paragem do utilizador é mais curta. Pode ser necessário aumentar o tempo de execução máxima da atualização para evitar uma pausa na utilização desta opção.  

    - Remove a `/Priority` opção de [linha de comando de configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) a partir do ficheiro configuração config.ini.


### <a name="enable-third-party-software-updates"></a>Ativar atualizações de software de terceiros

Quando define esta opção para **Sim,** define a política de **Permitir atualizações assinadas para uma localização do serviço de atualização intranet microsoft** e instala o certificado de assinatura para a loja Trust Publisher no cliente.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Ativar a atualização dinâmica para atualizações de funcionalidades
<!--4062619-->
A partir da versão 1906 do Gestor de Configuração, pode configurar a [Atualização Dinâmica para o Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). A Dynamic Update instala pacotes de idiomas, funcionalidades a pedido, controladores e atualizações cumulativas durante a configuração do Windows, direcionando o cliente para o download destas atualizações a partir da internet. Quando esta definição está definida para **Sim** ou **Não,** o Gestor de Configuração modifica o ficheiro [configuração](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) que é utilizado durante a instalação da atualização da funcionalidade.

- **Não configurado** - O valor predefinido. Não são feitas alterações no ficheiro configuração config.
  - A Dynamic Update está ativada por padrão em todas as versões suportadas do Windows 10.
    - Para as versões 1803 e anteriores do Windows 1803 e anterior, a Dynamic Update verifica o servidor WSUS do dispositivo para atualizações dinâmicas aprovadas. Nos ambientes do Gestor de Configuração, as atualizações dinâmicas nunca são diretamente aprovadas no servidor WSUS para que estes dispositivos não os instalem.
    - A partir da versão 1809 do Windows 10, o Dynamic Update utiliza a ligação à Internet do dispositivo para obter atualizações dinâmicas a partir do Microsoft Update. Estas atualizações dinâmicas não são publicadas para uso wSUS.
- **Sim** - Ativa a atualização dinâmica.
- **Não** - Desativa a atualização dinâmica.


## <a name="state-messaging"></a>Mensagens estatais

### <a name="state-message-reporting-cycle-minutes"></a>Ciclo de relatórios de mensagens do Estado (minutos)

Especifica a frequência com que os clientes reportam mensagens de Estado. Esta definição é de 15 minutos por defeito.



## <a name="user-and-device-affinity"></a>Afinidade do utilizador e do dispositivo  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Limiar de utilização de afinidade de dispositivo e utilizador (minutos)

Especifique o número de minutos antes de o Gestor de Configuração criar um mapeamento de afinidade do dispositivo do utilizador. Por padrão, este valor é de 2880 minutos (dois dias).

### <a name="user-device-affinity-usage-threshold-days"></a>Limiar de utilização de afinidade de dispositivo e utilizador (dias)

Especifique o número de dias em que o cliente mede o limiar para a afinidade do dispositivo baseado na utilização. Por defeito, este valor é de 30 dias.

> [!NOTE]  
> Por exemplo, especifica o limiar de utilização da **afinidade do utilizador (minutos)** como **60** minutos, e o limiar de utilização da **afinidade do dispositivo utilizador (dias)** como **5** dias. Em seguida, o utilizador deve utilizar o dispositivo durante 60 minutos durante um período de 5 dias para criar afinidade automática com o dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurar automaticamente a afinidade de dispositivo e utilizador a partir dos dados de utilização

Escolha **Sim** para criar afinidade automática do dispositivo do utilizador com base nas informações de utilização que o Gestor de Configuração recolhe.  

### <a name="allow-user-to-define-their-primary-devices"></a>Permitir ao utilizador a definição dos seus dispositivos primários
<!--3485366-->
Quando esta definição é **Sim,** os utilizadores podem identificar os seus próprios dispositivos primários no Centro de Software. Para mais informações, consulte o guia de utilizador do Centro de [Software](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Análise do Windows

> [!Important]  
> O serviço Windows Analytics está reformado a partir de 31 de janeiro de 2020. Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics é a evolução do Windows Analytics. Para mais informações, consulte [o que é desktop Analytics](../../../desktop-analytics/overview.md).
