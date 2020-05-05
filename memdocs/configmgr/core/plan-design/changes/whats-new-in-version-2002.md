---
title: Novidades na versão 2002
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 2002 do ramo atual do Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f760e70b1896700fa08bdb27c68794d2dec8c192
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719296"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Novidades na versão 2002 do ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Update 2002 for Configuration Manager current branch está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1806 ou posterior. <!-- baseline only statement:-->Ao instalar um novo site, também está disponível como uma versão de base. Este artigo resume as mudanças e novas funcionalidades no Gestor de Configuração, versão 2002.

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 2002](../../servers/manage/checklist-for-installing-update-2002.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Para tirar o máximo partido das novas funcionalidades do Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

> [!TIP]
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Anexo de inquilino do Microsoft Endpoint Manager

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Ações de sincronização e dispositivo do dispositivo
<!--3555758-->
O Microsoft Endpoint Manager é uma solução integrada para gerir todos os seus dispositivos. A Microsoft reúne o Gestor de Configuração e o Intune numa única consola chamada **Microsoft Endpoint Manager .** A partir desta versão pode enviar os seus dispositivos De Configuração para o serviço de cloud e tomar ações da lâmina **de Dispositivos** no centro de administração.

Para mais informações, consulte o inquilino do [Microsoft Endpoint Manager anexado](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infraestrutura do local

### <a name="remove-a-central-administration-site"></a>Remover um site de administração central
<!-- 3607277 -->

Se a sua hierarquia for constituída por um site de administração central (CAS) e um único local primário para crianças, pode agora remover o CAS. Esta ação simplifica a sua infraestrutura de Gestor de Configuração para um único local primário autónomo. Remove as complexidades da replicação site-to-site, e centra as suas tarefas de gestão no único local primário.

Para mais informações, consulte [Remova o CAS](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Novas regras de informação de gestão

Esta versão inclui as seguintes regras de insight de gestão:

- Nove regras no grupo de avaliação de gestor de **configuração** cortesia da Microsoft Premier Field Engineering. Estas regras são uma amostra dos muitos mais cheques que a Microsoft Premier fornece no Services Hub.<!-- 3607758 -->

  - Ative Directory Security Group Discovery está configurado para funcionar com demasiada frequência
  - Ative Directory System Discovery está configurado para funcionar com demasiada frequência
  - A Descoberta do Utilizador do Diretório Ativo está configurada para ser executada com demasiada frequência
  - Coleções limitadas a Todos os Sistemas ou Todos os Utilizadores
  - A Descoberta do Batimento Cardíaco está desativada
  - Consultas de recolha de longa duração ativadas para atualizações incrementais
  - Reduzir o número de aplicações e pacotes em pontos de distribuição
  - Problemas de instalação do local secundário
  - Atualize todos os sites para a mesma versão

- Duas regras adicionais no grupo **Cloud Services** para ajudá-lo a configurar o seu site para adicionar comunicação HTTPS segura:<!-- 6268489 -->

  - Sites que não têm configuração HTTPS adequada
  - Dispositivos não enviados para AD Azure

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Melhorias no serviço de administração

<!-- 5728365 -->

O serviço de administração é uma API REST para o Provedor de SMS. Anteriormente, tinha de implementar uma das seguintes dependências:

- Ativar HTTP melhorado para todo o site
- Ligue manualmente um certificado baseado em PKI ao IIS no servidor que acolhe a função de Provedor de SMS

A partir desta versão, o serviço de administração utiliza automaticamente o certificado auto-assinado do site. Esta alteração ajuda a reduzir o atrito para uma utilização mais fácil do serviço de administração. O site sempre gera este certificado. A definição de site http melhorada para **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP** apenas controla se os sistemas de site o utilizam ou não. Agora, o serviço de administração ignora esta definição do site, uma vez que usa sempre o certificado do site, mesmo que nenhum outro sistema de site esteja a utilizar o Enhanced HTTP. Ainda pode utilizar um certificado de autenticação de servidor baseado em PKI.

Para mais informações, consulte os seguintes novos artigos:

- [O que é o serviço de administração?](../../../develop/adminservice/overview.md)
- [Como criar o serviço de administração](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Apoio proxy para descoberta de Diretório Ativo Azure e sincronização de grupo

<!-- 5913817 -->

As definições de procuração do sistema de site, incluindo a autenticação, são agora utilizadas por:

- Descoberta de utilizadores do Azure Ative Directory (Azure AD)
- Descoberta do grupo de utilizadores da AD Azure
- Sincronização de resultados de adesão à coleção para grupos de Diretórios Ativos Azure

Para mais informações, consulte o [suporte do servidor Proxy](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Gestão ligada à nuvem

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>A mensagem de estado crítico mostra erros de ligação do servidor aos pontos finais necessários

<!-- 5566763 -->

Se o servidor do site do Gestor de Configuração não ligar aos pontos finais necessários para um serviço na nuvem, aumenta uma mensagem de estado crítico ID 11488. Quando o servidor do site não consegue ligar-se ao serviço, o estado do componente SMS_SERVICE_CONNECTOR muda para crítico. Ver estado detalhado no nó de Estado do Componente da consola 'Gestor de Configuração'.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticação baseada em token para gateway de gestão de nuvem

<!-- 5686290 -->

O gateway de gestão de nuvem (CMG) suporta muitos tipos de clientes, mas mesmo com o Enhanced HTTP, estes clientes requerem um certificado de autenticação de cliente. Este requisito de certificado pode ser um desafio para a disponibilização de clientes baseados na Internet que muitas vezes não se conectam à rede interna, não são capazes de aderir ao Azure Ative Directory (Azure AD), e não têm um método para instalar um certificado emitido pelo PKI.

O Gestor de Configuração alarga o suporte do dispositivo com os seguintes métodos:

- Registe-se na rede interna para um símbolo único
- Criar um símbolo de registo a granel para dispositivos baseados na Internet

Para mais informações, consulte [a autenticação baseada em Token para CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Funcionalidades de cloud do Microsoft Endpoint Configuration Manager

<!--5834830-->

Quando novas funcionalidades baseadas na nuvem estiverem disponíveis no centro de administração do Microsoft Endpoint Manager, ou outros serviços de cloud anexados para a instalação do Gestor de Configuração no local, pode agora optar por estas novas funcionalidades na consola Do Gestor de Configuração. Para obter mais informações sobre as funcionalidades de habilitação na consola 'Gestor de Configuração', consulte [funcionalidades opcionais ativas a partir de atualizações](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

Para obter mais informações sobre as alterações mensais no serviço de cloud Desktop Analytics, consulte [as novidades no Desktop Analytics](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Painel de saúde de conexão mostra problemas de ligação ao cliente

Utilize o painel de saúde de conexão desktop Analytics no Gestor de Configuração para monitorizar a saúde de conectividade dos clientes. Agora ajuda-o a identificar mais facilmente os problemas de configuração de procuração de clientes em duas áreas:

- **Verificações**de conectividade endpoint : Se os clientes não conseguirem alcançar um ponto final necessário, você vê um alerta de configuração no painel de instrumentos. Faça uma aperte para ver os pontos finais aos quais os clientes não podem ligar devido a problemas de configuração por procuração.<!-- 4963230 -->

- **Estado da conectividade**: Se os seus clientes utilizarem um servidor proxy para aceder ao serviço de nuvem desktop Analytics, o Gestor de Configuração apresenta agora problemas de autenticação por procuração dos clientes. Faça um aperte para ver clientes que não possam inscrever-se por causa da autenticação por procuração.<!-- 4963383 -->

Para mais informações, consulte [Monitor de saúde](../../../desktop-analytics/monitor-connection-health.md)de ligação .

## <a name="real-time-management"></a><a name="bkmk_real"></a>Gestão em tempo real

### <a name="improvements-to-cmpivot"></a>Melhorias à CMPivot

<!-- 5870934 -->

Tornámos mais fácil navegar em entidades cmpivot. Agora pode pesquisar entidades CMPivot. Novos ícones também foram adicionados para diferenciar facilmente as entidades e os tipos de objetos da entidade.

Para mais informações, consulte [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a>Gestão de conteúdos

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Excluir certas subredes para download de conteúdo por pares

<!-- 3555777 -->

Os grupos de fronteira incluem a seguinte opção para downloads de pares: Durante os **downloads de pares, utilize apenas pares dentro da mesma sub-rede**. Se ativar esta opção, a lista de localização de conteúdos do ponto de gestão apenas inclui fontes de pares que se encontram na mesma subnet e grupo de limites que o cliente. Dependendo da configuração da sua rede, pode agora excluir determinadas subredes para correspondência. Por exemplo, você quer incluir um limite, mas excluir uma sub-rede VPN específica.

Para mais informações, consulte [as opções do grupo Boundary](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Suporte proxy para Microsoft Connected Cache

<!-- 5856396 -->

Se o seu ambiente utilizar um servidor proxy não autenticado para acesso à Internet, agora que ativa um ponto de distribuição do Gestor de Configuração para o Microsoft Connected Cache, pode comunicar através do proxy. Para mais informações, consulte [o Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a>Gestão de clientes

### <a name="client-log-collection"></a>Coleção de registo de clientes

<!-- 4226618 -->

Pode agora ativar um dispositivo cliente para fazer o upload dos registos dos seus clientes para o servidor do site, enviando uma ação de notificação do cliente a partir da consola Do Gestor de Configuração.

Para mais informações, consulte a [notificação do Cliente.](../../clients/manage/client-notification.md#client-diagnostics)

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Acorde um dispositivo do site da administração central

<!-- 6030715 -->

A partir do site da administração central (CAS), no nó de Dispositivos ou Recolhas de Dispositivos, pode agora utilizar a ação de notificação do cliente para dispositivos Wake Up. Esta ação estava anteriormente disponível apenas a partir de um local primário.

Para mais informações, consulte [Como configurar Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Melhorias no suporte para dispositivos ARM64

<!--5954175-->

A plataforma **All Windows 10 (ARM64)** está disponível na lista de versões de OS suportadas em objetos com regras de requisitos ou listas de aplicabilidade.

> [!NOTE]
> Se selecionou anteriormente a plataforma de topo **do Windows 10,** esta ação selecionou automaticamente **tanto o Windows 10 (64-bit)** como **o All Windows 10 (32-bits).** Esta nova plataforma não é selecionada automaticamente. Se quiser adicionar **todos os Windows 10 (ARM64)**, selecione-o manualmente na lista.

Para obter mais informações sobre o suporte do Gestor de Configuração para dispositivos ARM64, consulte [o Windows 10 no ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Reparações de itens de configuração de rastreio
<!--4261411-->
Agora pode rastrear o histórico de **reparação quando suportado** nas regras de conformidade do seu item de configuração. Quando esta opção está ativada, qualquer reparação que ocorra no cliente para o item de configuração gera uma mensagem de estado. O histórico está armazenado na base de dados do Gestor de Configuração.

Para obter mais informações sobre esta definição, consulte Criar itens de [configuração personalizados para computadores de ambiente de trabalho e servidor escedidos com o cliente Do Gestor](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track)de Configuração .

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>Gestão de aplicações

### <a name="microsoft-edge-management-dashboard"></a>Painel de gestão do Microsoft Edge

<!-- 3871913 -->

O dashboard de gestão do Microsoft Edge fornece-lhe informações sobre a utilização do Microsoft Edge e de outros navegadores. Neste painel, pode:

- Veja quantos dos seus dispositivos têm Microsoft Edge instalado
- Veja quantos clientes têm versões diferentes do Microsoft Edge instaladas
- Tenha uma visão dos navegadores instalados em todos os dispositivos
- Tenha uma visão do navegador preferido por dispositivo

A partir do espaço de trabalho da Biblioteca de Software, clique na Microsoft Edge Management para ver o painel de instrumentos. Altere a recolha para os dados do gráfico clicando em Navegar e escolhendo outra coleção. Por defeito, as suas cinco maiores coleções estão na lista de lançamentos. Quando seleciona uma coleção que não está na lista, a coleção recém-seleccionada ocupa o lugar de baixo da sua lista de drop-down.

Para mais informações, consulte a [gestão do Microsoft Edge.](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash)

### <a name="improvements-to-microsoft-edge-management"></a>Melhorias na gestão do Microsoft Edge

<!-- 4561024 -->

Agora pode criar uma aplicação Microsoft Edge que está configurada para receber atualizações automáticas em vez de ter atualizações automáticas desativadas. Esta alteração permite-lhe optar por gerir as atualizações para o Microsoft Edge com o 'Configuração', ou permitir que o Microsoft Edge atualize automaticamente. Ao criar a aplicação, selecione Permitir que o Microsoft Edge atualize automaticamente a versão do cliente no dispositivo do utilizador final na página de Definições do Microsoft Edge.

Para mais informações, consulte a [gestão do Microsoft Edge.](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate)

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Sequência de tarefas como um tipo de implementação de modelo de aplicação

<!-- 3555953 -->

Agora pode instalar aplicações complexas utilizando sequências de tarefas através do modelo de aplicação. Adicione um tipo de implementação a uma aplicação que é uma sequência de tarefas, quer para instalar ou desinstalar a aplicação. Esta funcionalidade fornece os seguintes comportamentos:

- Exiba a sequência de tarefas da aplicação com um ícone no Centro de Software. Um ícone facilita a descoberta e identificação da sequência de tarefas da aplicação.

- Defina metadados adicionais para a sequência de tarefas da aplicação, incluindo informações localizadas

Para mais informações, consulte [Create Windows aplicações](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implantação de Os

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Bootstrap uma sequência de tarefa imediatamente após o registo do cliente

<!-- 5526972 -->

Quando instala e regista um novo cliente do Gestor de Configuração, e também implementa uma sequência de tarefas, é difícil determinar em quanto tempo após o registo irá executar a sequência de tarefas. Este lançamento introduz uma nova propriedade de configuração de clientes que pode usar para iniciar uma sequência de tarefas num cliente depois de se registar com sucesso no site.

Para mais informações, consulte sobre as propriedades de [instalação do cliente - PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Melhorias para verificar passo de sequência de tarefas de prontidão

<!-- 6005561 -->

Agora pode verificar mais propriedades do dispositivo na etapa de sequência de tarefas de prontidão de **verificação.** Utilize este passo numa sequência de tarefas para verificar se o computador-alvo satisfaz as condições pré-requisitos.

- Arquitetura do sistema operativo atual
- Versão mínima do SO
- Versão máxima do SO
- Versão mínima do cliente
- Linguagem do sistema operativo atual
- Alimentação ca-eléctrica ligada
- O adaptador de rede está ligado e não sem fios

Para mais informações, consulte os passos da [sequência de tarefas - Verifique a prontidão](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Melhorias no progresso da sequência de tarefas

<!-- 5932692 -->

A janela de progresso da sequência de tarefas inclui agora as seguintes melhorias:

- Você pode permitir-lhe mostrar o número atual de passo, número total de passos, e por cento de conclusão
- Aumentou a largura da janela para lhe dar mais espaço para mostrar melhor o nome da organização numa única linha

Para mais informações, consulte as [experiências do Utilizador para a implementação do OS](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Melhorias na implantação do OS

Esta versão inclui as seguintes melhorias na implementação do OS:

- O ambiente de sequência de tarefas `_TSSecureBoot`inclui uma nova variável apenas de leitura, .<!--5842295--> Utilize esta variável para determinar o estado da bota segura num dispositivo ativado pela UEFI. Para mais informações, consulte [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Delineie as variáveis da sequência de tarefas para configurar o contexto do utilizador para os passos de **Script run Command Line** e Run **PowerShell.**<!-- 5573175 --> Para mais informações, consulte [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) e [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- No passo **do Script Run PowerShell,** agora pode definir a propriedade **Dos Parâmetros** para uma variável.<!-- 5690481 --> Para mais informações, consulte [Executar PowerShell Script](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- O responsável pelo Gestor de Configuração PXE envia agora mensagens de estado para o servidor do site. Esta alteração facilita a resolução de problemas de implementações de SO que utilizam este serviço.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

### <a name="orchestration-groups"></a>Grupos de orquestração

<!-- 3098816 -->

Crie um grupo de orquestração para controlar melhor a implementação de atualizações de software para dispositivos. Muitos administradores de servidores precisam de gerir cuidadosamente as atualizações para cargas de trabalho específicas e automatizar comportamentos pelo meio.

Um grupo de orquestração dá-lhe a flexibilidade para atualizar dispositivos com base numa percentagem, num número específico ou numa ordem explícita. Também pode executar um script PowerShell antes e depois de os dispositivos executarem a implementação da atualização.

Membros de um grupo de orquestração podem ser qualquer cliente do Gestor de Configuração, não apenas servidores. As regras do grupo de orquestração aplicam-se aos dispositivos para todas as implementações de atualizações de software para qualquer coleção que contenha um membro do grupo de orquestração. Outros comportamentos de implantação ainda se aplicam. Por exemplo, janelas de manutenção e horários de implantação.

Para mais informações, consulte [os grupos de Orquestração.](../../../sum/deploy-use/orchestration-groups.md)

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Avaliar atualizações de software após uma atualização de pilha de manutenção

<!-- 4639943 -->

O Gestor de Configuração agora deteta se uma atualização de pilha de manutenção (SSU) faz parte de uma instalação para várias atualizações. Quando uma SSU é detetada, é instalada primeiro. Após a instalação da SSU, um ciclo de avaliação de atualização de software funciona para instalar as restantes atualizações. Esta alteração permite instalar uma atualização cumulativa dependente após a atualização da pilha de manutenção. O dispositivo não precisa de reiniciar entre instalações e não precisa de criar uma janela de manutenção adicional. As SSUs são instaladas primeiro apenas para instalações não-utilizadoradas. Por exemplo, se um utilizador iniciar uma instalação para várias atualizações do Software Center, a SSU pode não ser instalada primeiro.

Para mais informações, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu)de software .

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Atualizações do Office 365 para pontos de atualização de software desligados

<!-- 4065163 -->

Pode utilizar uma nova ferramenta para importar atualizações do Office 365 de um servidor WSUS ligado à Internet para um ambiente de Configuração desligado. Anteriormente, quando exportou e importou metadados para software atualizado em ambientes desligados, não foi capaz de implementar atualizações do Office 365. As atualizações do Office 365 requerem metadados adicionais descarregados de uma API do Office e do Office CDN, o que não é possível para ambientes desligados.

Para mais informações, consulte [as atualizações do Synchronize Office 365 a partir de um ponto](../../../sum/get-started/synchronize-office-updates-disconnected.md)de atualização de software desligado .

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>Proteção

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Expandir o Microsoft Defender Advanced Threat Protection (ATP) onboarding

<!-- 5229962 -->
O Gestor de Configuração expandiu o seu suporte para dispositivos de embarque para o Microsoft Defender ATP. Para mais informações, consulte a [Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md#onboard-devices).

### <a name="improvements-to-bitlocker-management"></a>Melhorias na gestão bitLocker

- A política de gestão BitLocker inclui agora configurações adicionais, incluindo políticas para unidades fixas e amovíveis.<!-- 5925683 --> Para mais informações, consulte a referência das [definições do BitLocker](../../../protect/tech-ref/bitlocker/settings.md).

- Na versão atual do 'Gestor de Configuração' 1910, para integrar o serviço de recuperação BitLocker teve de ativar um ponto de gestão. A ligação HTTPS é necessária para encriptar as chaves de recuperação através da rede desde o cliente do Gestor de Configuração até ao ponto de gestão. Configurar o ponto de gestão e todos os clientes para HTTPS pode ser um desafio para muitos clientes.

    A partir desta versão, o requisito HTTPS é para o site do IIS que acolhe o serviço de recuperação, e não todo o papel de ponto de gestão. Esta alteração relaxa os requisitos do certificado e ainda encripta as chaves de recuperação em trânsito.<!-- 5925660 --> Para mais informações, consulte [encriptar dados de recuperação](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a>Reportagem

### <a name="integrate-with-power-bi-report-server"></a>Integrar com o Power BI Report Server

<!-- 3721603 -->

Agora pode integrar o Power BI Report Server com relatório sinuoso do Gestor de Configuração. Esta integração confere-lhe uma visualização moderna e um melhor desempenho. Adiciona suporte de consola para relatórios Power BI semelhantes ao que já existe com os Serviços de Reporte de Servidores SQL.

Para mais informações, consulte [Integrar com o Power BI Report Server](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Consola de Gestor de Configuração

### <a name="show-boundary-groups-for-devices"></a>Mostrar grupos de fronteira para dispositivos

<!--6521835-->

Para ajudá-lo a resolver melhor os comportamentos dos dispositivos com grupos de fronteira, agora pode ver os grupos de fronteira para dispositivos específicos. No nó dos **Dispositivos** ou quando mostrar os membros de uma Coleção de **Dispositivos,** adicione a nova coluna **do Grupo Limite** na vista da lista.

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Enviar uma melhoria do sorriso

<!-- 5891852 -->

Quando envia um sorriso ou envia uma testa, é criada uma mensagem de estado quando o feedback é submetido. Esta melhoria fornece um registo de:

- Quando o feedback foi submetido
- Quem submeteu o feedback
- O ID de feedback
- Se a submissão do feedback foi bem sucedida ou não

Uma mensagem de estado com uma identificação de 53900 é uma submissão bem sucedida e 53901 é uma submissão falhada.

Para mais informações, consulte o [feedback do Produto.](../../understand/find-help.md#BKMK_1806Feedback)

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Procure todas as subpastas para obter itens de configuração e linhas de base de configuração

<!--5891241-->

Semelhante a melhorias em lançamentos anteriores, pode agora utilizar a opção de pesquisa **de Todas as Subpastas** a partir dos nós de **Configuração** e Planos de Base de **Configuração.**

## <a name="tools"></a><a name="bkmk_tools"></a>Ferramentas

### <a name="onetrace-log-groups"></a>Grupos de registo OneTrace

<!-- 5559993 -->

O OneTrace suporta agora grupos de registo personalizáveis, semelhantes ao recurso no Centro de Suporte. Os grupos de registo permitem-lhe abrir todos os ficheiros de registo para um único cenário. O OneTrace inclui atualmente grupos para os seguintes cenários:

- Gestão de aplicações
- Definições de conformidade (também referidas como Gestão de Configuração Desejada)
- Atualizações de software

Para mais informações, consulte [o Suporte Center OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Melhorias para estender e migrar no local para o Microsoft Azure
<!--5665775, 6307931-->
A ferramenta para estender e migrar o site para o Microsoft Azure suporta agora o fornecimento de várias funções do sistema de sites numa única máquina virtual Azure. Pode adicionar funções do sistema do site após a implementação inicial da máquina virtual Azure ter concluído.

Para mais informações, consulte [extend e emigrar no site para](../../support/azure-migration-tool.md#bkmk_add_role)o Microsoft Azure .

## <a name="other-updates"></a>Outras atualizações

A partir desta versão, as seguintes funcionalidades deixaram de ser [pré-lançamento:](../../servers/manage/pre-release-features.md)

- [Descoberta do grupo de utilizadores do Diretório Ativo Azure](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Sincronizar os resultados da adesão à coleção para o Azure Ative Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot autónomo](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Aplicativos de clientes para dispositivos cogeridos](../../../comanage/workloads.md#client-apps) (anteriormente conhecidos como *aplicativos Móveis para dispositivos cogeridos)*<!-- 1357892/3600959 -->

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte as notas de lançamento da [versão PowerShell 2002](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Para obter mais informações sobre as alterações ao serviço de administração REST API, consulte as notas de lançamento do [serviço de administração.](../../../develop/adminservice/release-notes.md#bkmk_2002)

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2002](https://support.microsoft.com/help/nnnnn).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Passos seguintes

Neste momento, a versão 2002 é lançada para o anel de atualização precoce. Para instalar esta atualização, tem de optar por entrar. Para mais informações, consulte o anel de [atualização precoce](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring).
<!-- As of December 20, 2019, version 2002 is globally available for all customers to install. -->

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização de 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.
>
> Saiba mais sobre:
>
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

Para questões significativas conhecidas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
