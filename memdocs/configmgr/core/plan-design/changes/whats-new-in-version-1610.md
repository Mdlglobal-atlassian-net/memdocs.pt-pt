---
title: Nova versão 1610
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1610 do Gestor de Configuração.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d154dc0ba681a37ebb2155bfa1bcdb6d8734965f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073964"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>O que&#39;novo na versão 1610 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1610 para o espaço atual do Gestor de Configuração está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1511, 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de base do 'Gestor de Configuração'.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
> - [Instalação de atualizações nos sites](https://technet.microsoft.com/library/mt607046.aspx)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1610 do Gestor de Configuração.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitorização in-consola do estado de instalação da atualização  
Começando com a versão 1610, quando instala um pacote de atualização e monitoriza a instalação na consola, existe uma nova fase: **Instalação de Postes**. Esta fase inclui o estatuto de tarefas como o reinício dos serviços-chave e a inicialização da monitorização da replicação. (Esta fase só está disponível na consola depois das atualizações do site para a versão 1610.) Para obter mais informações sobre o estado da instalação da atualização, consulte [a instalação de atualizações na consola](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
Pode excluir os clientes do Windows de serem atualizados com novas versões do software do cliente. Para isso, inclui os computadores clientes numa coleção especificada para ser excluída da atualização. Os clientes da coleção excluída ignoram os pedidos para atualizar o software do cliente.  Para mais informações, consulte [Excluir os clientes do Windows de atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Melhorias para os grupos de fronteira
A versão 1610 introduz mudanças importantes nos grupos de fronteira e como funcionam com pontos de distribuição. Estas alterações podem simplificar o design da sua infraestrutura de conteúdo, ao mesmo tempo que lhe conferem mais controlo sobre como e quando os clientes recuam para pesquisar pontos de distribuição adicionais como localizações de fonte de conteúdo. Isto inclui tanto no local como nos pontos de distribuição baseados na nuvem.
Estas melhorias substituem conceitos e comportamentos que você pode estar familiarizado (como configurar pontos de distribuição para ser rápido ou lento). O novo modelo deve ser mais fácil de configurar e manter. Estas alterações também estabelecem as bases para futuras alterações que melhorarão outras funções do sistema de sites que associa a grupos de fronteira.

Quando atualiza para a versão 1610, a atualização converte as configurações atuais do grupo de limites para se adaptar ao novo modelo para que estas alterações não perturbem as configurações de distribuição de conteúdos existentes.

Para mais informações, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Peer Cache para distribuição de conteúdos aos clientes
Começando com a versão 1610, o cliente **Peer Cache** ajuda-o a gerir a implementação de conteúdos para clientes em locais remotos. Peer Cache é uma solução de Gestor de Configuração incorporada para os clientes partilharem conteúdo com outros clientes, diretamente a partir da sua cache local.

Depois de implementar as definições de cliente que permitem a Peer Cache uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo de pares para outros clientes no mesmo grupo de fronteira.

Também pode utilizar o novo dashboard **Fontes** de Dados do Cliente para compreender a utilização de fontes de conteúdo de Peer Cache no seu ambiente.

> [!TIP]  
> Com a versão 1610, peer Cache e o dashboard De Dados do Cliente são funcionalidades de pré-lançamento. Para as ativar, consulte [utilize as funcionalidades de pré-lançamento a partir de atualizações](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Para mais informações, consulte peer Cache para clientes do Gestor de [Configuração](../hierarchy/client-peer-cache.md)e [dashboard De Dados](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)de Clientes .


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhadaao mesmo tempo
Agora pode utilizar a opção de **Reassign Distribution Point** para ter o processo de Gestor de Configuração em paralelo a reatribuição de até 50 pontos de distribuição partilhadas ao mesmo tempo. Antes desta libertação, os pontos de distribuição reatribuídos eram processados um de cada vez. Para mais informações consulte, [migrar vários pontos](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time)de distribuição partilhadas ao mesmo tempo .

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gestão de nuvem para gestão de clientes baseados na Internet

O gateway de gestão de nuvem fornece uma forma simples de gerir os clientes do Gestor de Configuração na Internet. O serviço de gateway de gestão de nuvem, que é implantado para o Microsoft Azure e requer uma subscrição do Azure, conecta-se à sua infraestrutura de Configuração no local utilizando uma nova função chamada ponto de ligação de gateway de gestão de nuvem. Uma vez completamente implantado e configurado, os clientes podem comunicar com as funções do sistema de configuração do site do Gestor de Configuração no local e pontos de distribuição baseados na nuvem, independentemente de estarem ligados à rede privada interna ou à Internet. Para mais informações e para ver como o gateway de gestão de nuvem se compara com a gestão de clientes baseada na Internet, consulte [Gerir clientes na Internet](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhoramentos à Política de Atualização de Edição do Windows 10
Nesta versão, foram introduzidas as seguintes melhorias neste tipo de política:

- Agora pode utilizar a política de upgrade da edição com PCs Windows 10 que executam o cliente do Gestor de Configuração, além dos PCs do Windows 10 que estão inscritos no Microsoft Intune.
- Pode fazer o upgrade do Windows 10 Professional para qualquer uma das plataformas do assistente compatível com o seu hardware.

## <a name="manage-hardware-identifiers"></a>Gerir identificadores de hardware
Agora pode fornecer uma lista de IDs de hardware que o Gestor de Configuração deve ignorar para efeitos de arranque pXE e registo de cliente. Há duas questões comuns que isto ajuda a resolver:

1. Muitos dispositivos, como o Surface Pro 3, não incluem uma porta Ethernet a bordo. Um adaptador USB-to-Ethernet é geralmente utilizado para estabelecer uma ligação com fios com o propósito de implantar um sistema operativo. No entanto, devido ao custo e à usabilidade geral, estes são frequentemente adaptadores partilhados. Uma vez que o endereço MAC deste adaptador é utilizado para identificar o dispositivo, a reutilização do adaptador torna-se problemática sem ações adicionais de administrador entre cada implementação. Agora, na versão 1610 do Gestor de Configuração, pode excluir o endereço MAC deste adaptador para que possa ser facilmente reutilizado neste cenário.
2. O SMBIOS ID é suposto ser um identificador de hardware único, mas alguns dispositivos de hardware especializados são construídos com IDs duplicados. Este problema pode não ser tão comum como o cenário adaptador USB-to-Ethernet apenas descrito, mas pode abordá-lo usando a lista de IDs de hardware excluídos.

Para mais detalhes, consulte [Gerir identificadores de hardware duplicados](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhorias na Windows Store para integração de negócios com Gestor de Configuração
Alterações nesta versão:
- Anteriormente, só podia implementar aplicações gratuitas a partir da Windows Store for Business. O Gestor de Configuração suporta agora ainda a implementação de aplicações licenciadas online pagas (apenas para dispositivos matriculados no Intune).
- Pode agora iniciar uma sincronização imediata entre a Windows Store para Business e Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Ative Directory.
- Pode eliminar uma subscrição da loja.

Para mais detalhes, consulte [Gerir aplicações da Windows Store para Negócios com Gestor de Configuração](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de políticas para dispositivos matriculados no Intune
Agora pode solicitar uma sincronização de política para um dispositivo intune inscrito na consola Do Gestor de Configuração, em vez de precisar de solicitar uma sincronização da aplicação Portal da Empresa no próprio dispositivo. As informações do estado do pedido de sincronização estão disponíveis como uma nova coluna nas vistas do dispositivo, chamada **Remote Sync State**. A informação também está disponível na secção de dados de descoberta do diálogo **Properties** para cada dispositivo.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Utilize as definições de conformidade para configurar as definições do Windows Defender
Agora pode configurar as definições do cliente do Windows Defender nos computadores Windows 10 matriculados no Intune utilizando itens de configuração na consola 'Gestor de Configuração'.
Para mais detalhes, consulte a secção **Windows Defender** em Criar itens de [configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Melhorias gerais no Centro de Software
- Os utilizadores podem agora solicitar aplicações ao Centro de Software, bem como ao Catálogo de Aplicações.
- Melhorias para ajudar os utilizadores a entender que software é novo e relevante.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas em vistas de recolha de dispositivos
Agora pode apresentar colunas para **IMEI** e **Número de Série** (para dispositivos iOS) nas vistas de recolha do dispositivo.

## <a name="customizable-branding-for-software-center-dialogs"></a>Marca personalizável para diálogos do Software Center
A marca personalizada para o Software Center foi introduzida na versão 1602 do Gestor de Configuração. Na versão 1610, essa marca é agora estendida a todas as caixas de diálogo associadas para proporcionar uma experiência mais consistente aos utilizadores do Software Center.

A marca personalizada para o Centro de Software é aplicada de acordo com as seguintes regras:

- Se a função de site de ponto do site do Catálogo de Aplicações não for instalada, então o Software Center exibe o nome da organização especificado no nome de organização de definição de cliente do **Agente informático** exibido no Centro de **Software**. Para obter instruções, consulte [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md).

- Se a função do site do site do Catálogo de Aplicações for instalada, então o Software Center exibe o nome e a cor da organização especificados nas propriedades do servidor do site do site do Catálogo de Aplicações. Para mais informações, consulte opções de configuração para o ponto de site do Catálogo de [Aplicações.](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)

- Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Gestor de Configuração, então o Software Center exibe o nome, cor e logotipo da empresa especificado nas propriedades de subscrição intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de tolerância de imposição para implementações de atualizações de aplicações e de software
Em alguns casos, é melhor dar mais tempo aos utilizadores para instalarem as implementações de aplicações necessárias ou atualizações de software para além de quaisquer prazos que configurassem. Por exemplo, isto pode ser necessário quando um computador foi desligado por um longo período de tempo e precisa de instalar um grande número de aplicações ou implementações de atualizações. Por exemplo, se um utilizador final acaba de regressar de férias, poderá ter de esperar por muito tempo, uma vez que as implementações de aplicações em atraso são instaladas. Para ajudar a resolver este problema, pode agora definir um período de carência de execução, implementando as definições do cliente do Gestor de Configuração para uma coleção. 

Para configurar o período de graça, tome as seguintes ações:
1. Na página do **Agente Informático** das definições do cliente, configure o novo período de graça da propriedade para aplicação após o prazo de **implementação (horas)** com um valor entre **1** e **120** horas.
2. Numa nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, na página **de Agendamento,** selecione a caixa de verificação **Atrasar a execução desta implementação de acordo com as preferências do utilizador, até ao período de carência definido nas definições**do cliente . Todas as implementações que tenham esta caixa de verificação selecionada, e que sejam direcionadas para dispositivos aos quais também implementou a definição do cliente, utilizarão o período de carência de execução.

Se configurar um período de carência de execução e selecionar a caixa de verificação, uma vez atingido o prazo de instalação da aplicação, será instalado na primeira janela não-empresarial que o utilizador configuraaté esse período de carência. No entanto, o utilizador ainda pode abrir o Software Center e instalar a aplicação a qualquer momento que queira. Uma vez expirado o período de graça, a aplicação reverte para o comportamento normal para implementações em atraso. Opções semelhantes foram adicionadas ao assistente de implementação de atualizações de software, assistente de regras de implementação automática e páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Melhor funcionalidade em caixas de diálogo sobre software necessário
Quando um utilizador recebe o software necessário, a partir do **Snooze e lembre-me:** definição, eles podem selecionar a partir da seguinte lista de valores: 
- **Mais tarde.** Especifica que as notificações são agendadas com base nas definições de notificação configuradas nas definições do Cliente.
- **Tempo fixo**. Especifica que a notificação será programada para ser exibida novamente após o tempo selecionado (por exemplo, em 30 minutos).

![Página do Agente de Computador estoirar nas definições do Agente Cliente](media/client-notification-settings.png)

O tempo máximo de soneca baseia-se nos valores de notificação configurados nas definições do Cliente. Por exemplo, se o prazo de implementação for superior a **24 horas, lembre os utilizadores de que cada definição (horas)** na página do Agente Informático estiver configurada durante 10 horas, e está mais de 24 horas antes do prazo, o utilizador veria um conjunto de opções de soneca até, mas nunca superior a 10 horas. À medida que o prazo se aproxima, há menos opções disponíveis, em conformidade com as definições relevantes do Agente cliente para cada componente da linha temporal de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é agora mais intrusiva. Em vez de uma notificação transitória da barra de tarefas, cada vez que o utilizador é notificado de que é necessária manutenção crítica do software, uma caixa de diálogo como os seguintes ecrãs no computador do utilizador:

![Diálogo de software obrigatório](media/client-toast-notification.png)


Para obter mais informações:
- [Configurações para gerir implementações de alto risco](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Painel de atualizações de software
Utilize o painel de atualizações de software para visualizar o estado de conformidade atual dos dispositivos na sua organização e analise rapidamente os dados para ver quais os dispositivos em risco. Para visualizar o dashboard, navegue para **monitorizar o** > **Painel de Atualizações**de Software de**Segurança** > de**Visão Geral** > .

Para mais detalhes, consulte [as atualizações](../../../sum/deploy-use/monitor-software-updates.md)de software do Monitor .


## <a name="improvements-to-the-application-request-process"></a>Melhorias no processo de pedido de pedido de pedido
Depois de ter aprovado uma aplicação para instalação, pode posteriormente optar por negar o pedido clicando em **Negar** na consola Do Gestor de Configuração. Anteriormente, este botão estava acinzentado após a aprovação.

Esta ação não faz com que a aplicação seja desinstalada a partir de nenhum dispositivo. No entanto, impede os utilizadores de instalarem novas cópias da aplicação a partir do Software Center.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar pelo tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software em regras de implementação automática. Por exemplo, para descarregar apenas atualizações de software inferiores a 2 MB, pode definir o filtro Tamanho de **Conteúdo (KB)** para **< 2048**. A utilização deste filtro impede que as grandes atualizações de software descarreguem automaticamente, o que suporta melhor a manutenção simplificada do Nível Inferior do Windows quando a largura de banda da rede é limitada. Para obter mais detalhes, veja:
- [Gestor de configuração e manutenção simplificada do Windows em sistemas operativos de nível inferior](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Automatically deploy software updates](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Para configurar o campo Tamanho do **Conteúdo (KB),** faça um dos seguintes:
- Quando criar uma regra de implementação automática, no assistente de regra de implementação automática Create, vá para a página **de Atualizações** de Software.
- Nas propriedades para uma regra de implementação automática existente, vá ao separador Atualizações de **Software.**

## <a name="office-365-client-management-dashboard"></a>Painel de gestão de clientes do Office 365
O painel de gestão de clientes do Office 365 já se encontra disponível na consola Do Gestor de Configuração. Para ver o dashboard, vá ao **Software Library** > **Overview** > Office**365 Client Management**.

O painel de instrumentos exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de clientes do Office 365
- Escritório 365 línguas de cliente
- Escritório 365 canais de clientes     

Para mais detalhes, consulte as atualizações do [Manage Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o passo **do Restart Computer** prepare uma partição FAT32 no disco rígido para a transição para o UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para a conversão BIOS para A UEFI. Para mais detalhes, consulte os passos da [sequência de tarefas para gerir o BIOS até à conversão UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhorias na etapa da sequência de tarefas: Prepare o Cliente ConfigMgr para captura  
O passo do Cliente Prepare ConfigMgr irá agora remover completamente o cliente do Gestor de Configuração, em vez de apenas remover informações chave. Quando a sequência de tarefas implementar a imagem do sistema operativo capturado, instalará sempre um novo cliente do Gestor de Configuração. Para mais detalhes, consulte os passos da [sequência de tarefas](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de política de conformidade intune
Agora pode obter uma visão rápida da conformidade geral dos dispositivos e das principais razões para o incumprimento, utilizando novas tabelas sob o espaço de trabalho **de Monitorização** na consola De Configuração Manager. Pode clicar numa secção da tabela para perfurar até uma lista dos dispositivos dessa categoria. Para mais detalhes, consulte [Monitorize a política](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)de conformidade .


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração de procura para implementações híbridas para proteger dispositivos iOS e Android
A Microsoft está a integrar a solução de proteção contra ameaças móveis da Lookout para proteger dispositivos móveis iOS e Android através da deteção de malware, aplicações de risco e muito mais, em dispositivos. A solução do Lookout ajuda-o a determinar o nível de ameaça, que é configurável. Pode criar uma regra de política de conformidade no Gestor de Configuração para determinar a conformidade do dispositivo com base na avaliação de risco por Lookout. Ao utilizar políticas de acesso condicional, pode permitir ou bloquear o acesso a recursos da sua empresa com base no estado de conformidade do dispositivo.

Os utilizadores de dispositivos iOS não conformes serão solicitados a inscreverem-se. Serão obrigados a instalar a aplicação Lookout for Work nos seus dispositivos, ativar a aplicação e remediar as ameaças relatadas na aplicação Lookout for Work para ter acesso aos dados da empresa.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração
Existem muitas definições novas que pode utilizar nos seus itens de configuração para várias plataformas de dispositivos. Estas são configurações que existiam anteriormente no Microsoft Intune numa configuração autónoma, e estão agora disponíveis quando utiliza o Intune com o 'Configuração Manager'.
Para mais detalhes, consulte itens de [Configuração para dispositivos geridos sem o cliente do Gestor de Configuração](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android
#### <a name="password-settings"></a>Definições de palavra-passe
- **Memorizar histórico de palavras-passe**
- **Permitir desbloqueio por impressão digital**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir browser**
- **Permitir preenchimento automático**
- **Permitir bloqueador de janelas de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação
- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo
- **Permitir armazenamento amovível**
- **Permitir partilha de Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir chamadas em roaming**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**

### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe ser exigida**
- **Memorizar histórico de palavras-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**
- **Minutos de inatividade antes de a proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos desktop e mobile do Windows 10
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavras-passe**
- **Exija uma senha quando o dispositivo regressar de um estado ocioso**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória no dispositivo móvel**
- **Permitir anular inscrições manualmente**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo
- **Permitir VPN sobre redes móveis**
- **Permitir roaming do VPN sobre redes móveis**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações de centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos da Equipa Windows 10
#### <a name="device-settings"></a>Definições do dispositivo
- **Ativar as Informações Operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolher as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL da imagem de fundo do ecrã de bloqueio**

### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Tipo obrigatório de palavra-passe**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas permitidas antes de o dispositivo ser apagado**
- **Minutos de inatividade antes de o ecrã se desligar**
- **Expiração da Palavra-passe (dias)**
- **Memorizar histórico de palavras-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe por imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir deteção automática de rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo
- **Permitir ligação automática a hotspots Wi-Fi**
