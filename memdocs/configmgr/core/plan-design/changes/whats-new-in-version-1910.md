---
title: Novidades na versão 1910
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1910 do ramo atual do Gestor de Configuração.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 04981e944b838f89af2383678c94e620aaefd7f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719324"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Novidades na versão 1910 do ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1910 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola. Aplique esta atualização em sites que executam a versão 1806 ou posterior. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Este artigo resume as mudanças e novas funcionalidades no Gestor de Configuração, versão 1910.

Reveja sempre a mais recente lista de verificação para instalar esta atualização. Para mais informações, consulte a Lista de [Verificação para instalar a atualização 1910](../../servers/manage/checklist-for-installing-update-1910.md). Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Para tirar o máximo partido das novas funcionalidades do Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.

> [!TIP]
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a>Microsoft Endpoint Configuration Manager

<!--4960084-->

O Gestor de Configuração faz agora parte do Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

O Microsoft Endpoint Manager é uma solução integrada para gerir todos os seus dispositivos. A Microsoft reúne o Gestor de Configuração e insoniza com licenciamento simplificado. Continue a utilizar os investimentos existentes do Gestor de Configuração enquanto aproveita a potência da nuvem da Microsoft ao seu próprio ritmo.

As seguintes soluções de gestão da Microsoft fazem agora parte da marca Microsoft Endpoint Manager:

- [Gestor de configuração](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Análise de Computadores](../../../desktop-analytics/overview.md)
- [Piloto automático](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Outras funcionalidades na [Consola de Gestão](https://go.microsoft.com/fwlink/?linkid=2109094) de Dispositivos

Para mais informações, consulte as seguintes publicações de Brad Anderson, vice-presidente corporativo da Microsoft para a Microsoft 365:

- [Post de blog de anúncio](https://aka.ms/cmannounce)
- [Papel de visão](https://aka.ms/MEMVisionPaper)
- [Vídeo resumo de anúncio](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Que coisas mudam no Gestor de Configuração com o Microsoft Endpoint Manager?

Na versão 1910, para além da mudança de nome, o Gestor de Configuração ainda funciona da mesma forma. Algumas das alterações de nome podem ter impacto na utilização dos seguintes componentes:

- **Consola de Gestor**de Configuração : Encontre atalhos para a consola e para o **Visualizador** de Controlo Remoto no menu Windows Start na pasta **Microsoft Endpoint Manager.**

- **Centro de Software**: Encontre o atalho do Centro de Software no menu Windows Start na pasta **Microsoft Endpoint Manager.**

![Ícones do menu do Microsoft Endpoint Manager Iniciar](media/microsoft-endpoint-manager-start-menu.png)

Certifique-se de atualizar qualquer documentação interna que mantenha para incluir estes novos locais.

> [!TIP]
> No Windows 10, quando abrir o menu Iniciar, escreva o nome para encontrar o ícone. Por exemplo, introduza: `Configuration Manager` ou `Software Center`.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infraestrutura do local

### <a name="reclaim-sedo-lock"></a>Recuperar a fechadura SEDO

<!--4786915-->

A partir da versão atual do [ramo 1906,](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)pode limpar o bloqueio numa sequência de tarefas. Agora pode limpar o bloqueio de qualquer objeto na consola 'Gestor de Configuração'.

Para mais informações, consulte [A utilização da consola 'Gestor de Configuração'.](../../servers/manage/admin-console.md#bkmk_sedo)

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Alargar e migrar o site no local para o Microsoft Azure
<!--3556022-->

Esta nova ferramenta ajuda-o a criar programáticamente máquinas virtuais Azure (VMs) para O Gestor de Configuração. Pode instalar com as definições padrão do site funções como um servidor de site passivo, pontos de gestão e pontos de distribuição. Depois de validar as novas funções, use-as como sistemas adicionais do site para uma elevada disponibilidade. Também pode remover a função do sistema de site no local e apenas manter a função Azure VM.

Para mais informações, consulte [extend e emigrar no site para](../../support/azure-migration-tool.md)o Microsoft Azure .

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

Para obter mais informações sobre as alterações mensais no serviço de cloud Desktop Analytics, consulte [as novidades no Desktop Analytics](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a>Gestão em tempo real

### <a name="optimizations-to-the-cmpivot-engine"></a>Otimizações para o motor CMPivot
<!--3197353-->
Adicionámos algumas otimizações significativas ao motor CMPivot. Agora pode empurrar mais do processamento para o cliente ConfigMgr. As otimizações reduzem drasticamente a carga CPU de rede e servidor necessária para executar consultas CMPivot. Com estas otimizações, agora pode vasculhar os gigabytes de dados do cliente em tempo real. 

Para mais informações, consulte [Otimizações para o motor CMPivot](../../servers/manage/cmpivot.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Entidades e melhoramentos adicionais da CMPivot
<!--5410930-->
Adicionámos uma série de novas entidades cmpivot e melhorias de entidades para ajudar na resolução de problemas e na caça. Incluímos as seguintes entidades para consultar:

- Registos de eventos windows[(WinEvent)](../../servers/manage/cmpivot.md#bkmk_WinEvent)
- Conteúdo de ficheiros[(Conteúdo de Ficheiros)](../../servers/manage/cmpivot.md#bkmk_File)
- DLLs carregados por processos[(ProcessModule)](../../servers/manage/cmpivot.md#bkmk_ProcessModule)
- Informação de Diretório Ativo Azure[(AADStatus)](../../servers/manage/cmpivot.md#bkmk_AadStatus)
- Estado de proteção do ponto final[(EPStatus)](../../servers/manage/cmpivot.md#bkmk_EPStatus)

Esta versão inclui ainda várias [outras melhorias](../../servers/manage/cmpivot.md#bkmk_Other) para a CMPivot. Para mais informações, consulte a [CMPivot a partir da versão 1910](../../servers/manage/cmpivot.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a>Gestão de conteúdos

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Suporte à Cache conectada da Microsoft para aplicações Intune Win32

<!--5032900-->

Quando ativa o Microsoft Connected Cache nos pontos de distribuição do Gestor de Configuração, podem agora servir aplicações Microsoft Intune Win32 a clientes cogeridos.

Para mais informações, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](../hierarchy/microsoft-connected-cache.md#bkmk_intune)

> [!NOTE]
> A versão atual do gestor de configuração 1906 incluía a Otimização de [Otimização](../hierarchy/microsoft-connected-cache.md) de Entregas em Cache (DOINC), uma aplicação instalada no Windows Server que ainda está em desenvolvimento. A partir da versão atual do ramo 1910, esta funcionalidade chama-se Microsoft Connected Cache.
>
> Quando instala a Cache Conectada num ponto de distribuição do Gestor de Configuração, descarrega o tráfego do serviço de otimização de entregas para fontes locais. A Cache Conectada faz este comportamento apertando eficientemente o conteúdo ao nível do byte-range.

## <a name="client-management"></a><a name="bkmk_client"></a>Gestão de clientes

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Incluir linhas de base de configuração personalizadas como parte da avaliação da política de conformidade
<!--3608345-->

Agora pode adicionar a avaliação das linhas de base de configuração personalizadacomo regra de avaliação da política de conformidade. Quando criar ou editar uma linha de base de configuração, pode agora utilizar a Base de Avaliação como parte da opção **de avaliação da política de conformidade.** Ao adicionar ou editar uma regra de política de conformidade, tem uma condição chamada **Incluir linhas de base configuradas na avaliação**da política de conformidade .

Para dispositivos cogeridos, e quando configura o Intune para obter os resultados da avaliação de conformidade do Gestor de Configuração como parte do estado de conformidade global, esta informação é enviada para o Diretório Ativo do Azure. Em seguida, pode usá-lo para acesso condicional aos recursos do seu Office 365.

Para mais informações, consulte Incluir as linhas de [base de configuração personalizadas como parte da avaliação da política de conformidade.](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Ativar a política de utilizador para a multi-sessão do Windows 10 Enterprise

<!--4737447-->

Configuração Manager versão atual 1906 introduziu suporte para [Windows Virtual Desktop](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Este ambiente Microsoft Azure suporta várias versões DE, algumas das quais permitem múltiplas sessões de utilizadores ativos simultâneos. Por exemplo, a multi-sessão do Windows 10 Enterprise é uma destas versões DE SO.

Se necessitar da política do utilizador nestes dispositivos multisminários e aceitar qualquer potencial impacto de desempenho, pode agora configurar uma definição de cliente para ativar a política do utilizador. No grupo **Política do Cliente,** configure a política de utilizador Ativar para a definição **de várias sessões de utilizador.**

Para mais informações, consulte [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a>Gestão de aplicações

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Implementar o Microsoft Edge, versão 77 e posterior
<!--4561024-->
O novo Microsoft Edge está pronto para o negócio. Agora pode implementar o Microsoft Edge, versão 77 e mais tarde, para os seus utilizadores. Os administradores podem escolher o canal Beta, Dev ou Estável, juntamente com uma versão do cliente do Microsoft Edge para implementar.

Para mais informações, consulte [Implementar o Microsoft Edge, versão 77 e mais tarde](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Melhorias nos grupos de aplicação

<!--4760058-->

A partir da versão atual do ramo 1906, pode criar um grupo de aplicações para enviar para uma coleção de dispositivos como uma única implementação. Esta versão melhora esta funcionalidade:

- Os utilizadores podem selecionar **Desinstalar** para o grupo de aplicações no Software Center.
- Pode implantar um grupo de aplicações numa recolha de **utilizadores.**

Para obter informações mais gerais, consulte [Criar grupos](../../../apps/deploy-use/create-app-groups.md)de aplicações .


## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implantação de Os

### <a name="improvements-to-the-task-sequence-editor"></a>Melhorias ao editor da sequência de tarefas

 O editor da sequência de tarefas inclui as seguintes melhorias:

- **Pesquise o editor da sequência de tarefas:**<!--4621085--> Se tiver uma grande sequência de tarefas com muitos grupos e passos, pode ser difícil encontrar passos específicos. Agora pode pesquisar no editor da sequência de tarefas. Esta ação permite localizar mais rapidamente os passos na sequência de tarefas.
- **Condições de sequência de tarefas de cópia e pasta:**<!--4621098--> Se quiser reutilizar as condições de um passo de sequência de tarefa para outro, pode agora copiar e colar as condições no editor da sequência de tarefas.

Para mais informações, consulte o novo artigo sobre como utilizar o editor da sequência de [tarefas](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Melhorias no desempenho da sequência de tarefas: Planos de potência

<!--3555926-->

Agora pode executar uma sequência de tarefas com o plano de poder de alto desempenho. Esta opção melhora a velocidade global da sequência de tarefas. Confunde o Windows para usar o seu plano de potência de alto desempenho incorporado, que proporciona o máximo desempenho em detrimento de um maior consumo de energia.

Para mais informações, consulte melhorias de [desempenho para planos](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf)de energia .

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Transferência de sequência de tarefas a pedido através da internet

<!--3601238-->

Pode utilizar a sequência de tarefas para implementar uma atualização no local do Windows 10 através do gateway de gestão da nuvem (CMG). No entanto, requer a implementação para descarregar todos os conteúdos localmente antes de iniciar a sequência de tarefas.

A partir desta versão, o motor de sequência de tarefas pode descarregar pacotes a pedido a partir de um CMG ativado por conteúdo ou de um ponto de distribuição em nuvem. Esta alteração proporciona flexibilidade adicional com as implementações de upgrade do Windows 10 para dispositivos baseados na Internet.

Para mais informações, consulte [a atualização do Windows 10 no local via CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Melhorias na implantação do OS

Esta versão inclui as seguintes melhorias na implementação do OS.

#### <a name="boot-image-keyboard-layout"></a>Layout do teclado da imagem de arranque

<!--4910348-->

Configure o layout padrão do teclado para uma imagem de arranque. No separador **de personalização** de uma imagem de arranque, utilize o novo esquema de teclado padrão set na opção **WinPE.** Se selecionar um idioma diferente do en-us, o Gestor de Configuração ainda inclui en-us nos locais de entrada disponíveis. No dispositivo, o layout inicial do teclado é o local selecionado, mas o utilizador pode mudar o dispositivo para en-us, se necessário.

Para mais informações, consulte [Gerir imagens](../../../osd/get-started/manage-boot-images.md#customization)de arranque .

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importar um único índice de um pacote de atualização do OS

<!--4931110-->

Quando importar um pacote de upgrade de OS, pode utilizar o Extrato um índice de **imagem específico do ficheiro install.wim da** opção de pacote de upgrade selecionado. Este comportamento é semelhante ao das [imagens de S](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), exceto que substitui a instalação.wim existente no pacote de upgrade do OS. Extrai o índice de imagem para um local temporário e, em seguida, move-o para o diretório de origem original.

Para mais informações, consulte [gerir pacotes](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs)de upgrade do OS .

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Saída dos resultados de uma linha de comando de execução passo para uma variável durante uma sequência de tarefas

<!--user story 4977616/bug 4798352-->

O passo **da Linha de Comando de Execução** inclui agora uma opção variável de sequência de **tarefas.** Quando ativa esta opção, a sequência de tarefas salva a saída do comando para uma variável de sequência de tarefas personalizada que especifica.

Para mais informações, consulte [executar linha](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)de comando .

#### <a name="improvements-to-task-sequence-debugger"></a>Melhorias na sequência de tarefas debugger

Esta versão inclui as seguintes melhorias na sequência de tarefas:

- Utilize a nova variável de sequência de **tarefas TSDebugOnError** para iniciar automaticamente o desbugger quando a sequência de tarefas devolve um erro.<!-- 5012536 -->
- Se criarum ponto de rutura no debugger e a sequência de tarefas reiniciar o computador, o debugger mantém os pontos de rutura após o reinício.<!-- 5012509 -->

Para obter mais informações, consulte as variáveis de [debugger](../../../osd/deploy-use/debug-task-sequence.md) e de sequência de [tarefas - TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Melhor suporte linguístico na sequência de tarefas

<!--5411057, 5138936-->

Esta versão adiciona controlo sobre a configuração do idioma durante a implementação do SISTEMA. Se já estiver a aplicar estas definições linguísticas, esta alteração pode ajudá-lo a simplificar a sua sequência de tarefas de implementação de SO. Em vez de utilizar vários passos por idioma ou scripts separados, utilize uma instância por idioma do passo de Definições do **Windows embutida** com uma condição para esse idioma.

Utilize o passo de sequência de **definições do Windows para** configurar as seguintes novas definições:

- Local de entrada (layout padrão do teclado)
- Localização do sistema
- Língua ui
- Recuo da língua da UI
- Local do utilizador

Para mais informações, consulte [Apply Windows Settings](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Nova variável para atualização no local do Windows 10

<!--4680263-->

Para resolver problemas de tempo com a sequência de tarefas de atualização no local da Janela 10 em dispositivos de alto desempenho quando a configuração do Windows estiver concluída, pode agora definir uma nova variável de sequência de tarefas, **ConfiguraçãoCompletePause**. Quando atribui um valor em segundos a esta variável, o processo de configuração do Windows atrasa esse tempo antes de iniciar a sequência de tarefas. Este tempo de tempo proporciona ao cliente do Gestor de Configuração tempo adicional para inicializar.

Para mais informações, consulte variáveis de sequência de [tarefas - ConfiguraçãoCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Atualizações de software

### <a name="additional-options-for-third-party-update-catalogs"></a>Opções adicionais para catálogos de atualizações de terceiros
<!--4469002-->
Agora tem mais controlos granulares sobre a sincronização de catálogos de atualizações de terceiros. A partir da versão 1910 do Configurmanager de Configuração, pode configurar o calendário de sincronização de cada catálogo de forma independente. Quando utiliza catálogos que incluam atualizações categorizadas, pode configurar a sincronização para incluir apenas categorias específicas de atualizações para evitar sincronizar todo o catálogo. Com catálogos categorizados, quando estiver confiante de que irá implementar uma categoria, pode configurá-la para descarregar e publicar automaticamente para o Windows Server Update Services (WSUS).

Para mais informações, consulte [Permitir atualizações de terceiros](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Utilizar otimização de entrega para todas as atualizações do Windows
<!--4699118-->
Anteriormente, só poderia utilizar a Otimização da Entrega para atualizações expressas. Com a versão 1910 do Gestor de Configuração, é agora possível utilizar a Otimização de Entrega para a distribuição de todos os conteúdos do Windows Update para clientes que executam a versão 1709 do Windows 10 ou mais tarde.

Para obter mais informações, consulte:
- [Optimize Windows 10 update delivery (Otimizar a entrega das atualizações do Windows 10)](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Definições de cliente para atualizações de software](../../clients/deploy/about-client-settings.md#software-updates)
- [Definições do cliente para otimização de entrega](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Filtro adicional de atualização de software para ADRs
<!--4852033-->
Agora pode utilizar **o Deploy como** filtro de atualização para as suas regras de implementação automática (ADRs). Este filtro ajuda a identificar novas atualizações que possam ter de ser implementadas para as suas coleções piloto ou de teste.

Para mais informações, consulte [a implementação automática](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)de atualizações de software .

## <a name="office-management"></a><a name="bkmk_o365"></a>Gestão de escritórios


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 ProPlus Pilot and Health Dashboard
<!--4488272, 4488301-->

O Office 365 ProPlus Pilot and Health Dashboard ajuda-o a planear, pilotar e implementar o Office 365 ProPlus. O dashboard fornece informações de saúde para dispositivos com o Office 365 ProPlus para ajudar a identificar possíveis problemas que possam afetar os seus planos de implementação. O Office 365 ProPlus Pilot and Health Dashboard fornece uma recomendação para dispositivos piloto baseados em inventário de adição.

Para mais informações, consulte o piloto do [Office 365 ProPlus e o painel de saúde](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a>Proteção

### <a name="bitlocker-management"></a>Gestão do BitLocker

<!--3601034-->

O Gestor de Configuração fornece agora as seguintes capacidades de gestão para encriptação de unidade BitLocker:

- Implemente o cliente BitLocker para gerir dispositivos Windows.
- Gerir as políticas de encriptação do dispositivo.
- Gerar relatórios de conformidade.
- Utilize um site de administração e monitorização para a recuperação da chave.
- Aceda a um portal de auto-atendimento ao utilizador.

Para mais informações, consulte [Plan for BitLocker management](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Consola de Gestor de Configuração

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Ver consolas ativas e administradores de mensagens através de Ligações de Consola
<!--4923997-->
Fizemos as seguintes **melhorias**nas Ligações de Consola:

- A capacidade de enviar mensagens a outros administradores do Gestor de Configuração através das Equipas Microsoft.
- A **coluna Heartbeat da última consola** substituiu a coluna Última Hora **Conectada.**
  - Uma consola aberta em primeiro plano envia um batimento cardíaco a cada 10 minutos para ajudar a determinar quais as ligações de consola que estão atualmente ativas.

Para mais informações, consulte [o View recentemente conectado consolas](../../servers/manage/admin-console.md#bkmk_viewconnected) e [administradores de Mensagens](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Ações de diagnóstico do cliente

<!--4433455-->

Existem novas ações de dispositivos para **diagnósticos de clientes** na consola Do Gestor de Configuração:

- Ativar a **exploração madeireira verbosa:** Altere o nível de registo global para o componente CCM para *verboso,* e permita a exploração de depuração.
- **Desativar a exploração madeireira verbosa:** Mude o nível de registo global para *padrão*e desative a exploração de depuração.

Para mais informações, consulte [diagnósticos do Cliente.](../../clients/manage/client-notification.md#client-diagnostics)

### <a name="improvements-to-console-search"></a>Melhorias na pesquisa de consolas
<!--4640570-->

Esta versão inclui as seguintes melhorias para pesquisar na consola 'Gestor de Configuração':

- Agora pode utilizar a opção de pesquisa **de Todas as Subpastas** a partir dos nós de Pacotes e **Consultas** de **Condutor.**<!--2841181,5424892-->
- Quando uma pesquisa retornar mais de 1.000 resultados, selecione **OK** na barra de aviso para ver mais resultados.<!--4640570-->

## <a name="other-updates"></a>Outras atualizações

Para obter mais informações sobre as alterações nas cmdlets do Windows PowerShell para O Gestor de Configuração, consulte [as notas de lançamento da versão PowerShell 1910](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps).

Para obter mais informações sobre as alterações ao serviço de administração REST API, consulte as notas de lançamento do [serviço de administração.](../../../develop/adminservice/release-notes.md#bkmk_1910)

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
O rollup de atualização seguinte (4537079) está disponível na consola a partir de 18 de fevereiro de 2020: [Rollup de atualização para o Microsoft Endpoint Configuration Manager, versão 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Passos seguintes

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
A partir de 20 de dezembro de 2019, a versão 1910 está globalmente disponível para todos os clientes instalarem.

Quando estiver pronto para instalar esta versão, consulte [a instalação de atualizações para O Gestor](../../servers/manage/updates.md) de Configuração e lista de [verificação para instalar a atualização 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Para instalar um novo site, utilize uma versão de base do Gestor de Configuração.
>
> Saiba mais sobre:
>
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md) 
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines) 

Para questões significativas conhecidas, consulte as notas de [lançamento.](../../servers/deploy/install/release-notes.md)

Depois de atualizar um site, consulte também a [lista de verificação pós-actualização](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).
