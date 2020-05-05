---
title: Novidades na versão 1902
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1902 do ramo atual do Gestor de Configuração.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4972f6e8689ad44dbd1a19adcde104cd5f59038c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719359"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Novidades na versão 1902 do gerente de configuração atual

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1902 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1802, 1806 ou 1810. <!-- baseline only statement:-->Ao instalar um novo site, também está disponível como uma versão de base. Este artigo resume as mudanças e novas funcionalidades no Gestor de Configuração, versão 1902.  

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 1902](../../servers/manage/checklist-for-installing-update-1902.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

Para tirar o máximo partido das novas funcionalidades do Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a>Funcionalidades e sistemas operativos degradados

Saiba mais sobre as alterações de suporte antes de serem implementadas em [itens removidos e depreciados](deprecated/removed-and-deprecated.md).

- A implementação para partilha de conteúdos do Azure mudou. Utilize um portal de gestão de nuvem ativado por conteúdo, permitindo que a opção de permitir que a CMG funcione como um ponto de distribuição na **nuvem e sirva conteúdo a partir do armazenamento Azure**. Não poderá criar um ponto tradicional de distribuição de nuvens no futuro.

A versão 1902 deixa cair o suporte para os seguintes produtos:  

- Linux e UNIX como cliente. A deprecation foi anunciada com a [versão 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infraestrutura do local

### <a name="client-health-dashboard"></a>Painel de saúde do cliente

<!--3599209-->
Implementa atualizações de software e outras aplicações para ajudar a proteger o seu ambiente, mas estas implementações apenas atingem clientes saudáveis. Os clientes do Gestor de Configuração Pouco Saudável afetam negativamente a conformidade geral. Determinar a saúde do cliente pode ser um desafio dependendo do denominador: quantos dispositivos totais devem estar no seu âmbito de gestão? Por exemplo, se descobrir todos os sistemas do Ative Directy, mesmo que alguns desses registos sejam para máquinas aposentadas, este processo aumenta o seu denominador.

Agora pode ver um dashboard com informações sobre a saúde dos clientes do Gestor de Configuração no seu ambiente. Veja a saúde do seu cliente, a saúde do cenário e os erros comuns. Filtre a vista por vários atributos para ver eventuais problemas por versões DE SO e cliente.

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização.** Expandir o **estado do Cliente**e selecionar o nó do dashboard de **saúde do Cliente.**

![Screenshot do painel de saúde do cliente](media/3599209-client-health-dashboard.png)

Para mais informações, consulte [Como monitorizar os clientes](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Novas regras de informação de gestão

O recurso de informação de gestão tem as seguintes novas regras:

- Múltiplas regras com recomendações sobre gestão de coleções. Use estes insights para simplificar a gestão e melhorar o desempenho. Reveja estas novas regras no grupo **De cobranças.**<!--3555752-->  

- Atualize os clientes para uma regra de **versão suportada do Windows 10** no grupo **De Gestão Simplificada.** Esta regra reporta sobre clientes que estão a executar uma versão do Windows 10 que já não é suportada. Também inclui clientes com uma versão do Windows 10 que está perto do fim do serviço (três meses).<!--3897268-->  

Para mais informações, consulte [a Management insights](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Melhoria para HTTP melhorado

<!--3798957-->

Agora pode ativar http melhorado por local primário ou para o site da administração central.

Nas propriedades do site da administração central, selecione a opção de **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**. Esta definição aplica-se apenas às funções do sistema de instalação no site da administração central. Não é um cenário global para a hierarquia.

Para mais informações, consulte [http enhanced](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Melhoria dos pré-requisitos de configuração

Quando instala ou atualiza para a versão 1902, a configuração do Gestor de Configuração inclui agora a seguinte verificação prévia:

- Pendente de **reinício do sistema no servidor Remoto SQL**: Esta verificação pré-requisito é semelhante à regra de reinício do **sistema Pendente,** mas verifica um Servidor SQL remoto. Para mais informações, consulte [A Lista de Verificações pré-requisitos](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Gestão ligada à nuvem

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Pare o serviço de nuvem quando exceder o limiar

<!--3735092-->
O Gestor de Configuração pode agora parar um serviço de gateway de gestão de nuvem (CMG) quando a transferência total de dados ultrapassar o seu limite. A CMG sempre teve alertas para desencadear notificações quando a utilização atingiu níveis de alerta ou críticos. Para ajudar a reduzir quaisquer custos inesperados do Azure devido a um pico de utilização, esta nova opção desliga o serviço de cloud.

Para mais informações, consulte [stop CMG quando exceder o limiar](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Utilize o Gestor de Recursos Azure para serviços na nuvem

<!--3605704-->
A partir da versão 1810, a implantação clássica de serviços em Azure foi depreciada para ser usada no Gestor de Configuração. Esta versão é a última a apoiar a criação destas implantações Azure.

As missões existentes continuam a funcionar. A partir desta versão atual do ramo, o Azure Resource Manager é o único mecanismo de implementação para novos casos do gateway de gestão da nuvem e do ponto de distribuição em nuvem.

Para mais informações, consulte o Gestor de Recursos Azure para o portal de [gestão de nuvem.](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Adicione porta de entrada de gestão de nuvem para grupos de fronteira

<!--3640932-->
Agora pode associar um portal de gestão de nuvem (CMG) a um grupo de fronteiras. Esta configuração permite que os clientes faltem ou recuem para a CMG para comunicação do cliente de acordo com as relações de grupo de fronteira. Este comportamento é especialmente útil em cenários de sucursais e VPN. Pode direcionar o tráfego de clientes para longe de ligações WAN caras e lentas para, em vez disso, utilizar links de internet mais rápidos para o Microsoft Azure.

Para mais informações, consulte o [design da hierarquia da CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) e [instale cmg](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a>Gestão em tempo real

### <a name="run-cmpivot-from-the-central-administration-site"></a>Executar CMPivot do site da administração central

<!--3610960-->
O Gestor de Configuração suporta agora a execução da CMPivot a partir do site da administração central numa hierarquia. O site principal ainda trata da comunicação ao cliente. Ao executar a CMPivot a partir do site da administração central, comunica com o site principal através do canal de subscrição de mensagens de alta velocidade. Esta comunicação não depende da replicação padrão da SQL entre os sites.

Para mais informações, consulte a [CMPivot para obter dados em tempo real](../../servers/manage/cmpivot.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>Editar ou copiar scripts PowerShell

<!--3705507-->
Agora pode **editar** ou **copiar** um script PowerShell existente usado com a funcionalidade Executar Scripts. Em vez de recriar um guião que precisa de mudar, agora edite-o diretamente. Ambas as ações usam a mesma experiência de feiticeiro que quando crias um novo script. Quando edita ou copia um script, o Gestor de Configuração não persiste no estado de aprovação.

Para mais informações, consulte [Executar Scripts](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a>Gestão de conteúdos

### <a name="distribution-point-maintenance-mode"></a>Modo de manutenção de pontos de distribuição

<!--3555754-->

Agora pode definir um ponto de distribuição no modo de manutenção. Ative o modo de manutenção quando estiver a instalar atualizações de software ou a fazer alterações de hardware no servidor.

Enquanto o ponto de distribuição está no modo de manutenção, tem os seguintes comportamentos:

- O site não distribui nenhum conteúdo.  

- Os pontos de gestão não devolvem a localização deste ponto de distribuição aos clientes.

- Ao atualizar o site, um ponto de distribuição no modo de manutenção ainda atualiza.

- As propriedades do ponto de distribuição são apenas de leitura. Por exemplo, não pode alterar o certificado ou adicionar grupos de fronteira.  

- Qualquer tarefa agendada, como a validação de conteúdos, ainda funciona no mesmo horário.

Para mais informações sobre esta funcionalidade, consulte o [modo de manutenção](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Para obter mais informações sobre automatizar este processo com o Gestor de Configuração SDK, consulte o [método SetDPMaintenanceMode na classe SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a>Gestão de clientes

### <a name="client-provisioning-mode-timeout"></a>Tempo de tempo de fornecimento de clientes

<!--3197824-->
A sequência de tarefas define um carimbo de tempo quando coloca o cliente no modo de provisionamento. Um cliente no modo de provisionamento verifica a cada 60 minutos a duração do tempo desde a hora marcada. Se estiver em modo de provisionamento há mais de 48 horas, o cliente sai automaticamente do modo de provisionamento e reinicia o seu processo.

Para mais informações, consulte [o modo de provisionamento](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Ver primeiro ecrã apenas durante o controlo remoto

<!--3231732-->
Ao ligar-se a um cliente com dois ou mais monitores, pode ser difícil vê-los todos no visualizador de controlo remoto do Gestor de Configuração. Um operador de ferramentas remotas pode agora escolher entre ver **todos os ecrãs** ou apenas o **primeiro ecrã.**

Para mais informações, consulte [Como administrar remotamente um computador cliente do Windows](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Especifique uma porta personalizada para despertar pelos pares

<!--3605925-->
Agora pode especificar um número de porta personalizado para procuração de despertar. Nas definições do cliente, no grupo **Power Management,** configure a definição para **wake on LAN número de porta (UDP)**.  

Para mais informações, consulte [Como configurar Wake on LAN](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a>Gestão de aplicações

### <a name="improvements-to-application-approvals-via-email"></a>Melhorias nas aprovações de candidaturas via e-mail

<!--3594063-->
Esta versão tem melhorias na funcionalidade para receber notificações de e-mail para pedidos de pedido de pedido. Os utilizadores podem sempre adicionar um comentário ao pedido do Software Center. Este comentário mostra o pedido de aplicação na consola Do Gestor de Configuração. Agora esse comentário também mostra no e-mail. Incluir este comentário no e-mail ajuda os aprovadores a tomar uma melhor decisão para aprovar ou negar o pedido.

Para mais informações, consulte [notificações por e-mail.](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

### <a name="improvements-to-package-conversion-manager"></a>Melhorias ao Gestor de Conversão de Pacotes

<!-- SCCMDocs-pr issue #3357 -->
Esta versão inclui as seguintes melhorias ao Gestor de Conversão de [Pacotes:](../../../apps/pcm/package-conversion-manager.md)

- A análise do pacote programado é feita a cada 7 dias por padrão
- PowerShell cmdlets para analisar e converter pacotes
- Correções e melhorias gerais de bugs


## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implantação de Os

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Estado de progresso durante a sequência de tarefas de atualização no local

<!--3747129-->
Agora vê uma barra de progresso mais detalhada durante uma sequência de tarefas de upgrade do Windows 10. Esta barra mostra o progresso da configuração do Windows, que de outra forma é silenciosa durante a sequência de tarefas. Os utilizadores têm agora alguma visibilidade no progresso subjacente. Ajuda com a preocupação de que o processo de atualização seja suspenso por falta de indicação de progresso.  

![Progresso da sequência de tarefas de exemplo com o progresso da atualização do Windows](media/3747129-installation-progress.png)

Esta funcionalidade funciona com qualquer versão suportada do Windows 10 e apenas com a sequência de tarefas de upgrade no local.

### <a name="improvements-to-task-sequence-media-creation"></a>Melhorias na criação de meios de sequência de tarefas

<!--3556027, fka 1359388-->
Esta versão inclui várias melhorias para ajudá-lo a criar e gerir melhor os meios de sequência de tarefas. Para mais informações, consulte os seguintes artigos para tipos específicos de meios de comunicação:

- [Criar suportes de dados autónomos](../../../osd/deploy-use/create-stand-alone-media.md)
- [Criar meios pré-encenados](../../../osd/deploy-use/create-prestaged-media.md)
- [Criar meios de comunicação sabotáveis](../../../osd/deploy-use/create-bootable-media.md)
- [Criar suportes de dados de captura](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Especificar armazenamento temporário

Quando criar meios de sequência de tarefas, personalize agora a localização que o site utiliza para armazenamento temporário de dados. Este processo pode requerer muito espaço de condução temporária. Esta alteração confere-lhe maior flexibilidade para escolher onde armazenar estes ficheiros temporários.

No Assistente de Mídia de sequência de **tarefas Create,** especifique a localização da **pasta Desordecência**. Por defeito, esta localização é `%UserProfile%\AppData\Local\Temp`semelhante ao seguinte caminho: .

#### <a name="add-a-label-to-the-media"></a>Adicione um rótulo aos meios de comunicação

Agora pode adicionar um rótulo aos meios de sequência de tarefas. Esta etiqueta ajuda-o a identificar melhor os meios de comunicação depois de o criar. No Assistente de Mídia de sequência de **tarefas Create,** especifique uma **etiqueta de media**.

### <a name="import-a-single-index-of-an-os-image"></a>Importar um único índice de uma imagem de OS

<!--3719699-->
Ao importar um ficheiro de imagem do Windows (WIM) para O Gestor de Configuração, pode agora especificar importar automaticamente um único índice em vez de todos os índices de imagem no ficheiro. Esta opção proporciona os seguintes benefícios:

- Ficheiro de imagem menor  
- Manutenção offline mais rápida  
- Otimizar a manutenção de imagem, para um ficheiro de imagem menor após manutenção offline

Quando importar uma imagem de OS, selecione a opção de extrair um índice de **imagem específico do ficheiro WIM especificado**. Em seguida, selecione o índice de imagem da lista.  

Para mais informações, consulte [Adicionar uma imagem de OS](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>Manutenção de imagem otimizada

<!--3555951-->
Quando aplica atualizações de software a uma imagem de OS, existe uma nova opção para otimizar a saída removendo quaisquer atualizações supersed. A otimização da manutenção offline aplica-se apenas a imagens com um único índice.

Quando criar uma programação para atualizar uma imagem de OS, selecione a opção de **Remover atualizações supersed após a imagem ser atualizada**.

Para mais informações, consulte [Aplicar atualizações](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase)de software numa imagem .

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Melhorias para executar passo de sequência de tarefas do Script PowerShell

<!--3556028, fka 1359389-->
O passo da sequência de tarefas **do Script PowerShell de execução** inclui agora as seguintes melhorias:  

- Pode agora introduzir diretamente o código Windows PowerShell neste passo. Esta alteração permite-lhe executar comandos PowerShell durante uma sequência de tarefas sem primeiro criar e distribuir um pacote com o script.

- Quando escolher a opção **de script PowerShell,** selecione **Editar Script**. A nova janela de script PowerShell fornece as seguintes ações:  

    - Editar o script diretamente  

    - Abra um script existente a partir de arquivo  

    - Navegue por um script aprovado existente no Gestor de Configuração

- Guarde a saída do script para uma variável de sequência de tarefas personalizada  

- Para incluir os parâmetros do script no registo da sequência de tarefas, defina a variável de sequência de tarefas **OSDLogPowerShellParâmetros** para **TRUE**. Por defeito, os parâmetros não estão no registo.  

- Outras melhorias que fornecem funcionalidades semelhantes à etapa da [Linha de Comando de Execução.](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) Por exemplo, especifique as credenciais alternativas do utilizador ou especifique um intervalo.

> [!Important]  
> Para aproveitar esta nova funcionalidade de Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

Para mais informações, consulte [Executar PowerShell Script](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>Outras melhorias na implantação do OS

<!--3633146,3641475,3654172,3734270-->
Esta versão inclui as seguintes melhorias na implementação do OS:

- Há uma nova ação padrão **da Visão** nas sequências de tarefas. <!--3633146-->  

- A janela de diálogo de erro da sequência de tarefas mostra agora mais informações. Mostra o nome do passo da sequência de tarefas que falhou. <!--3641475-->  

- Quando define a variável de sequência de tarefas **OSDDoNotLogCommand** para verdadeira, agora também esconde a linha de comando do passo da Linha de Comando de Execução no ficheiro de registo. Anteriormente, apenas mascarava o nome do programa do pacote de instalação passo em smsts.log.<!--3654172-->  

- Quando ativa um serviço PXE num ponto de distribuição sem o Windows Deployment Service, pode agora estar no mesmo servidor que o serviço DHCP. <!--3734270--> Para mais informações, consulte [Configure pelo menos um ponto de distribuição para aceitar pedidos de PXE](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a>Centro de Software

### <a name="replace-toast-notifications-with-dialog-window"></a>Substitua as notificações de torradas por janela de diálogo

<!--3555947-->
Por vezes, os utilizadores não vêem a notificação do Brinde do Windows sobre um reinício ou implementação necessária. Então não vêem a experiência para dormir o lembrete. Este comportamento pode levar a uma má experiência do utilizador quando o cliente atinge um prazo.

Agora, quando as implementações precisam de um reinício ou são necessárias alterações de software, tem a opção de utilizar uma janela de diálogo mais intrusiva.

Para mais informações, consulte [Plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)

### <a name="configure-user-device-affinity-in-software-center"></a>Configure a finção do dispositivo de utilizador no Centro de Software

<!--3485366-->
Com as melhorias na [infraestrutura](whats-new-in-version-1806.md#software-center-infrastructure-improvements) do Software Center a partir da versão 1806, as funções do servidor do catálogo de aplicações já não são necessárias para a maioria dos cenários. Alguns clientes ainda confiaram no catálogo de aplicações para permitir que os utilizadores definissem o seu dispositivo principal para a finidade do dispositivo de utilizador.

Agora os utilizadores podem definir o seu dispositivo principal no Software Center. Esta ação torna-os um utilizador primário do dispositivo no 'Gestor de Configuração'.

Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

### <a name="configure-default-views-in-software-center"></a>Configurar vistas padrão no Centro de Software

<!--3612112-->
Esta versão do Gestor de Configuração iterates ainda mais sobre como pode personalizar o Software Center:

- Definir o layout padrão das aplicações, seja como azulejos ou uma lista  

    - Se um utilizador alterar esta configuração, o Software Center persiste a preferência do utilizador no futuro  

- Configure o filtro de aplicação predefinido, total ou apenas as aplicações necessárias  

    - O Software Center utiliza sempre a definição predefinida. Os utilizadores podem alterar este filtro, mas o Software Center não persiste a sua preferência.

Especifique estas definições no grupo de definições do cliente do **Software Center.**

Para mais informações, consulte [as definições do cliente](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Especificar prioridade para atualizações de funcionalidades na manutenção do Windows 10

<!--3734525-->
Ajuste a prioridade com que os clientes instalam uma atualização de funcionalidade através da [manutenção do Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Por padrão, os clientes agora instalam atualizações de funcionalidades com maior prioridade de processamento.

Utilize as definições do cliente para configurar esta opção. No grupo Atualizações de **Software,** configure a seguinte definição: **Especifique a prioridade da linha para atualizações**de funcionalidades .

Para mais informações, consulte [as definições do cliente](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a>Gestão de escritórios

### <a name="redirect-windows-known-folders-to-onedrive"></a>Redirecione as pastas conhecidas do Windows para o OneDrive

<!--3556021-->
Utilize o Gestor de Configuração para mover as pastas conhecidas do Windows para o OneDrive para o Negócios. Estas pastas incluem Desktop, Documents e Pictures. Para simplificar as atualizações do Windows 10, implemente estas definições para os clientes do Windows 7 antes de implementar uma sequência de tarefas.

Para obter mais informações sobre esta funcionalidade do OneDrive para o Negócio, consulte [Redirecionar e mover as pastas conhecidas do Windows para oneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders).

Primeiro, [encontre a identificação do seu Escritório 365 inquilino.](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id) Em seguida, implemente a versão do cliente sincronizado OneDrive 18.111.0603.0004 ou posterior. Para mais informações, consulte [implementar aplicações OneDrive utilizando](https://docs.microsoft.com/onedrive/deploy-on-windows)o 'Gestor de Configuração'.  

Para criar e implementar um perfil OneDrive para negócios, na consola Do Gestor de Configuração, vá ao espaço de trabalho **De Ativos e Compliance.** Expandir **as Definições**de Conformidade e selecionar o nó **OneDrive para Perfis de Negócios.**  

Para mais informações, consulte as pastas conhecidas do Windows para a secção OneDrive no artigo [OneDrive for Business Profiles.](../../../compliance/deploy-use/onedrive-profile.md)

### <a name="integration-for-office-365-proplus-readiness"></a>Integração para prontidão do Office 365 ProPlus

<!--3735402-->
Utilize o Gestor de Configuração para identificar dispositivos com alta confiança que estão prontos para fazer upgrade para o Office 365 ProPlus. A integração fornece informações sobre quaisquer potenciais problemas de compatibilidade com add-ins e macros do Office utilizados no seu ambiente. Em seguida, utilize o Gestor de Configuração para implementar o Office em dispositivos prontos.

O painel de gestão de clientes do Office 365 existente inclui agora um novo azulejo, **office 365 ProPlus Upgrade Readiness**.

Para mais informações, consulte o Painel de Gestão de [Clientes do Office 365](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)

### <a name="additional-languages-for-office-365-updates"></a>Idiomas adicionais para atualizações do Office 365

<!--3555955-->
O Gestor de Configuração suporta agora todos os idiomas suportados para atualizações de clientes do Office 365. O fluxo de trabalho da atualização separa agora os 38 idiomas para **a Atualização** do Windows dos inúmeros idiomas para a Atualização do **Cliente do Office 365**.

Para mais informações, consulte [Manage Office 365 atualizações](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang)

### <a name="office-products-on-lifecycle-dashboard"></a>Produtos de escritório no painel de instrumentos de ciclo de vida

<!--3556026-->
O painel de instrumentos de vida do produto inclui agora informações para versões instaladas do Office 2003 através do Office 2016. Os dados aparecem depois de o site correr a tarefa de resumição do ciclo de vida, que é a cada 24 horas.

Para mais informações, consulte [Utilize o painel de instrumentos](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)do ciclo de vida do produto .


## <a name="phased-deployments"></a><a name="bkmk_pod"></a>Implantações faseadas

### <a name="dedicated-monitoring-for-phased-deployments"></a>Monitorização dedicada para implementações faseadas

<!--3555949-->
As implantações faseadas têm agora o seu próprio nó de monitorização dedicado. Este nó facilita a identificação de implementações faseadas que criou e, em seguida, navegar para a visão de monitorização de implementação faseada. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó de **Implementações Faseadas.** Mostra a lista de destacamentos faseados.

Para mais informações, consulte a visão de monitorização de [implementação faseada](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor).

### <a name="improvement-to-phased-deployment-success-criteria"></a>Melhoria dos critérios de sucesso de implantação faseados

<!--3555946-->
Especifique critérios adicionais para o sucesso de uma fase numa implantação faseada. Em vez de apenas uma percentagem, estes critérios podem agora ser também o número de dispositivos implementados com sucesso. Esta opção é útil quando o tamanho da coleção é variável, e você tem um número específico de dispositivos para mostrar sucesso antes de passar para a fase seguinte.

Criar uma implementação faseada para uma sequência de tarefas, atualização de software ou aplicação. Em seguida, na página Definições do assistente, selecione a seguinte opção como critérios para o sucesso da primeira fase: **Número de dispositivos implementados com sucesso**.

Para mais informações, consulte [Criar implementações faseadas](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Consola de Gestor de Configuração

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a>Melhorias na consola de Gestor de Configuração

<!--3594151-->
Com base no feedback dos clientes na Midwest Management Summit (MMS) Desert Edition 2018, esta versão inclui as seguintes melhorias na consola do Gestor de Configuração:

- Maximizar a janela de registo de navegação para métodos de deteção de aplicações
- Vá à coleção a partir de uma implementação de aplicação
- Remover o conteúdo do estado de monitorização
- Pontos de vista classificam por valores inteiros no nó de **implantação** do espaço de trabalho **de monitorização**
- Mova o aviso para um grande número de resultados

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md#tips)

### <a name="configuration-manager-console-notifications"></a>Notificações de consola do Gestor de Configuração

<!--3556016, fka 1318035-->
Para mantê-lo mais informado para que possa tomar as medidas apropriadas, a consola Do Gestor de Configuração agora o notifica para os seguintes eventos:

- Quando uma atualização está disponível para o próprio Gestor de Configuração
- Quando ocorrem eventos de ciclo de vida e manutenção no ambiente

Esta notificação é uma barra na parte superior da janela da consola abaixo da fita. Substitui a experiência anterior quando as atualizações do Gestor de Configuração estão disponíveis. Estas notificações na consola ainda apresentam informações críticas, mas não interferem com o seu trabalho na consola. Não pode descartar notificações críticas. A consola apresenta todas as notificações numa nova área de notificação da barra de títulos.

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md)

### <a name="confirmation-of-console-feedback"></a>Confirmação do feedback da consola

<!--3556010-->
Ao enviar [feedback](../../understand/find-help.md#product-feedback) na consola Do Gestor de Configuração, agora mostra uma mensagem de confirmação. Esta mensagem inclui um ID de **feedback**, que pode dar à Microsoft como identificador de rastreio.

Para mais informações, consulte o [feedback do Produto.](../../understand/find-help.md#bkmk_feedbackid)

### <a name="view-recently-connected-consoles"></a>Ver consolas recentemente conectadas

<!--3699367-->
Agora pode ver as ligações mais recentes para a consola 'Gestor de Configuração'. A vista inclui ligações ativas e as consolas que recentemente ligaram. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda **a Segurança**e selecione o nó de Ligações de **Consola.**

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md#bkmk_viewconnected)

### <a name="in-console-documentation-dashboard"></a>Painel de documentação na consola

<!--3556019, fka 1357546-->
Há um novo nó **documentação** no novo espaço de trabalho **comunitário.** Este nó inclui informações atualizadas sobre documentação do Gestor de Configuração e artigos de suporte.

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md#bkmk_doc-dashboard)

### <a name="search-device-views-using-mac-address"></a>Pontos de vista do dispositivo de pesquisa usando endereço MAC

<!--3600878-->
Agora pode pesquisar um endereço MAC numa visão do dispositivo da consola 'Gestor de Configuração'. Esta propriedade é útil para administradores de implementação de OS enquanto resolução de implementações baseadas em PXE. Quando visualizar uma lista de dispositivos, adicione a coluna **Mac Address** à vista. Utilize o campo de pesquisa para adicionar os critérios de pesquisa do **Endereço MAC.**

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md#tips)

### <a name="use-net-47-for-improved-console-accessibility"></a>Utilizar .NET 4.7 para uma melhor acessibilidade das consolas

<!-- SCCMDocs-pr issue #3228 -->
Para melhorar as funcionalidades de acessibilidade da consola 'Gestor de Configuração', atualize .NET para a versão 4.7 ou posteriormente no computador que executa a consola.

Para mais informações, consulte [funcionalidades de acessibilidade no Gestor](../../understand/accessibility-features.md)de Configuração .

### <a name="changes-to-console-setup-process"></a>Alterações no processo de configuração da consola

<!-- 3612513 -->
Existem novos componentes necessários para instalar a consola 'Gestor de Configuração'. Se criar uma embalagem para instalar a consola noutros computadores, certifique-se de que a embalagem inclui os seguintes ficheiros:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Quando instala ou atualiza um servidor de site, copia estes ficheiros de instalação e suporta pacotes de idiomas para o site para a subpasta **Tools\ConsoleSetup.** Para mais informações, consulte [Instalar a consola 'Gestor de Configuração'.](../../servers/deploy/install/install-consoles.md)


## <a name="other-updates"></a>Outras atualizações

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1902](https://support.microsoft.com/help/4498910).

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte [as notas de lançamento da versão PowerShell 1902](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps).

O rollup de atualização seguinte (4500571) está disponível na consola a partir de 17 de junho de 2019: Rollup de atualização para o ramo atual do Gestor de [Configuração, versão 1902](https://support.microsoft.com/help/4500571).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Passos seguintes

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)  

Para questões conhecidas e significativas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).
