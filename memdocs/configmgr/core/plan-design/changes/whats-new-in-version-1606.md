---
title: Novo na versão 1606
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1606 do Gestor de Configuração.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4298a6a66d60d79d05f8b5cdc9ff8caa0e7f4426
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074032"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>O que&#39;novo na versão 1606 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1606 para O Gestor de Configuração está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1511 ou 1602. A versão 1511 é a versão inicial de base que utiliza para instalar novos sites do Gestor de Configuração.
> [!TIP]  
> Saiba mais sobre:  
>   
> - [Instalação de novos sites](../../servers/deploy/install/prepare-to-install-sites.md) (utilizando uma versão de base como 1511)  
> - [Instalação de atualizações em sites](../../servers/manage/updates.md) (como a atualização 1602 ou 1606)  

 As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1606 do Gestor de Configuração.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Atualizações e manutenção

### <a name="changes-for-the-updates-and-servicing-node"></a>Alterações para as Atualizações e nó de Manutenção
Seguem-se as alterações ao nó de Atualizações e De Manutenção na consola Do Gestor de Configuração:
> [!NOTE]
> Estas alterações só estão disponíveis depois de instalar a versão 1606.

- **Mudança de nome do nó:**

    No espaço de trabalho **de monitorização,** o nó de estado de manutenção do **site** foi renomeado para **Atualizações e Estado de Manutenção**.
- **Mais detalhes do estado da instalação:**

    Quando visualiza o estado de instalação da atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Download** (Isto aplica-se apenas ao site de topo onde a função do sistema de ponto de ligação de serviço é instalada.)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, existem agora informações mais detalhadas para cada passo, incluindo qual o ficheiro de registo que pode ver para mais informações.  
-   **Nova opção para voltar a tentar falhas pré-requisitos:**

    Tanto nos espaços de trabalho da **Administração** como da **Monitorização,** as **Atualizações e** o nó de Manutenção incluem um novo botão na fita chamada **Avisos pré-requisitos de ignorar**.

    Quando instala atualizações sem utilizar a opção de ignorar avisos pré-requisitos (a partir do Assistente de Atualizações), e essa instalação de atualização para devido a um aviso, pode então selecionar **ignorar avisos pré-requisitos** da fita. Isto desencadeia uma continuação automática da instalação da atualização.  



- **Visão mais limpa das atualizações:**

    Nas **Atualizações e** no nó de Manutenção, vê agora apenas a atualização mais recente mente instalada e quaisquer novas atualizações que estejam disponíveis para instalar. Para visualizar atualizações previamente instaladas, clique no novo botão **Histórico** que aparece na fita.  

-   **Opção renomeada para pré-produção:**

    No nó **de Atualizações e Manutenção,** o botão de **opções do Cliente** chama-se Cliente de **Pré-produção .**


###  <a name="pre-release-features"></a>Funcionalidades de pré-lançamento
A partir de 1606, deve dar o seu consentimento para utilizar funcionalidades de pré-lançamento no 'Gestor de Configuração' antes de poder selecionar e ativar a sua utilização. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Novo comportamento de atualização de pontode distribuição
A atualização 1606 introduz alterações que melhoram a disponibilidade de pontos de distribuição quando instala futuras atualizações.

Após a atualização 1606 ser instalada, quando instalar uma atualização nesse site que requer a reinstalação automática das funções padrão e de distribuição de pontos de distribuição, todos os pontos de distribuição já não ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor do site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização a um subconjunto de pontos de distribuição a qualquer momento. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Isto permite que pontos de distribuição que ainda não tenham começado a atualizar, ou que tenham completado a atualização, permaneçam online e capazes de fornecer conteúdo aos clientes.



## <a name="accessibility"></a><a name="accessibility"></a>Acessibilidade
Para navegar entre os diferentes nós de um espaço de trabalho, pode agora introduzir a primeira letra do nome de um nó. Cada tecla de pressão move o cursor para o próximo nó que começa com essa letra. Para os utilizadores que têm um leitor de ecrã, o leitor lê o nome desse nó. Para mais informações sobre opções de Acessibilidade, consulte [as funcionalidades de Acessibilidade.](../../../core/understand/accessibility-features.md)

## <a name="administration"></a><a name="administration"></a>Administração
Seguem-se as alterações à Administração na consola 'Gestor de Configuração':
### <a name="oms-connector"></a>Conector OMS

Agora pode ligar o Gestor de Configuração como coleções do Gestor de Configuração à [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/). Isto torna visíveis dados como as coleções da implementação do seu Gestor de Configuração em OMS. Encontre mais informações, consulte [os dados sincronizados do Gestor de Configuração para a Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)de Gestão de Operações da Microsoft aqui .

O Conector OMS é uma função de pré-lançamento. Para o ativar, consulte [utilize as funcionalidades de pré-lançamento a partir de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Suporte para tamanho de cache nas definições do cliente

Agora pode configurar o tamanho da pasta cache nos computadores do cliente com **as Definições** do Cliente na consola 'Gestor de Configuração'. Anteriormente, só podia definir o tamanho da cache do cliente ao instalar ou reinstalar o software do cliente. Agora pode especificar o tamanho da cache como uma definição de cliente (padrão ou personalizado), e depois ter essas definições aplicadas com a próxima atualização de política no cliente, sem exigir a reinstalação de um cliente. Para obter mais informações, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local

### <a name="support-for-multiple-device-management-points"></a>Suporte para vários pontos de gestão de dispositivos

A gestão de dispositivos móveis no local (MDM) suporta agora uma nova capacidade na Atualização de Aniversário do Windows 10 que configura automaticamente um dispositivo matriculado para ter mais de um ponto de gestão de dispositivos disponíveis para utilização. Esta capacidade permite que o dispositivo recue para outro ponto de gestão do dispositivo, quando o que normalmente utiliza não está disponível. Esta capacidade funciona apenas para Computadores e dispositivos com a Atualização de Aniversário do Windows 10 instalada.


## <a name="application-management"></a>Gestão de aplicações

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gerir aplicações a partir da Loja Windows para Empresas

O [Windows Store for Business](https://www.microsoft.com/business-store) é onde pode encontrar e comprar aplicativos Windows para a sua organização, individualmente ou em volume. Ao ligar a loja ao Gestor de Configuração, pode sincronizar a lista de aplicações que adquiriu com o Gestor de Configuração, vê-las na consola do Gestor de Configuração e implementá-las como qualquer outra aplicação.

Para mais detalhes, consulte [Gerir aplicações da Windows Store para Negócios com Gestor de Configuração](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gerir aplicações iOS compradas em grandes volumes

O fluxo de trabalho para gerir aplicações iOS adquiridas em volume e implementá-las com o Gestor de Configuração foi melhorado.


### <a name="software-center-user-interface"></a>Interface de utilizador do Centro de Software

A interface de utilizador do Software Center foi simplificada para uma descoberta mais fácil.
*  O **Estado de Instalação** e os separadores de **software instaladoforam** combinados num único separador estado de **instalação.**
*  **Atualizações, Sistemas** **Operativos**e **Aplicações** foram separadas em três separadores separados.
* Várias atualizações podem agora ser selecionadas para instalação imediatamente, ou todas as atualizações podem ser instaladas imediatamente clicando em **Instalar Tudo**.

### <a name="content-status-links"></a>Links de estado de conteúdo
Sobre as propriedades de uma aplicação ou pacote, existe agora um link que o leva ao estado desse objeto.

## <a name="software-updates"></a>Atualizações de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Definição de cliente para gerir o Agente cliente do Office 365
Agora pode utilizar um ajuste de cliente do Gestor de Configuração para gerir o agente cliente do Office 365. Depois de configurar e implementar as atualizações do Office 365, o agente cliente do Gestor de Configuração trabalha com o agente cliente do Office 365 para descarregar e instalar atualizações do Office 365 a partir de um ponto de distribuição.

Para mais detalhes, consulte [as atualizações do Manage Office 365 ProPlus com o Gestor de Configuração](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Mude manualmente os clientes para um novo ponto de atualização de software
Agora pode ativar uma opção que permite que os clientes do Gestor de Configuração mudem para um novo ponto de atualização de software quando há problemas com o ponto de atualização de software ativo. Depois de ativada, os clientes irão procurar outro ponto de atualização de software na análise seguinte.

Para mais detalhes, consulte Plan para atualizações de [software no Gestor de Configuração](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software
Quando uma atualização de software que requer um reinício é implementada utilizando o 'Gestor de Configuração' e é instalada num computador, está agendado um reinício pendente. Também é apresentada uma caixa de diálogo de reinício. Começando na versão 1606 do Gestor de Configuração, as opções **Atualizar e Reiniciar** e Atualizar e **Desligar** estão disponíveis sempre que houver um reinício pendente para uma atualização de software do Gestor de Configuração. Estes estão disponíveis nas opções de energia do Windows dos computadores Windows 10. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será exibida após o reinício do computador.

Para mais detalhes, consulte [Plan para atualizações](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)de software .

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Executar atualizações de software scan imediatamente após um cliente instalar atualizações de software e reiniciar
Agora pode executar uma varredura de conformidade imediatamente após um cliente instalar atualizações de software e reiniciar. Para configurar isto para uma implementação, na página **user Experience** do Desenvolvedor de Atualizações de Software, selecione Se qualquer atualização nesta implementação necessitar de um reinício do sistema, executar o ciclo de avaliação da **implementação de atualizações após o reinício**. Isto permite ao cliente verificar se há atualizações adicionais de software que se tornam aplicáveis após o reinício do cliente e, em seguida, instalá-las (e tornar-se conformes) durante a mesma janela de manutenção. Para mais detalhes, consulte [a implementação automática de atualizações](../../../sum/deploy-use/automatically-deploy-software-updates.md) de software ou [implemente manualmente atualizações](../../../sum/deploy-use/manually-deploy-software-updates.md)de software .

## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Melhorias na etapa da sequência de tarefas: Instalar Atualizações de Software
Uma nova definição, **Avaliar as atualizações de software a partir de resultados de digitalização em cache,** dá-lhe a opção de fazer uma varredura completa para atualizações de software, em vez de usar os resultados da varredura em cache. Para mais detalhes, consulte os passos da [sequência de tarefas](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Além disso, uma nova variável de sequência de tarefas, **SMSTSSoftwareUpdateScanTimeout,** está disponível. Esta variável permite controlar o tempo limite para as atualizações de software durante o passo de sequência de tarefas de Atualizações de Software. O valor predefinido é 30 minutos. Para mais detalhes, consulte [variáveis incorporadas](../../../osd/understand/task-sequence-variables.md)na sequência de tarefas .

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Variável de sequência de tarefas OSDPreserveDriveLetter foi depreciada
A variável de sequência de tarefas OSDPreserveDriveLetter foi depreciada. A partir da versão 1606 do Gestor de Configuração, o Windows Setup determina a melhor letra de unidade a utilizar (tipicamente C:) durante uma implantação do sistema operativo, por padrão.

Para mais detalhes, consulte [variáveis incorporadas](../../../osd/understand/task-sequence-variables.md)na sequência de tarefas .

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalize o tamanho da janela RamDisk TFTP para pontos de distribuição ativados por PXE
Agora pode personalizar o tamanho da janela RamDisk para pontos de distribuição ativados por PXE. Se tiver personalizado a sua rede, pode fazer com que o download da imagem de arranque falhe com um erro de tempo, porque o tamanho da janela é demasiado grande. A personalização do tamanho da janela RamDisk Trivial File Transfer Protocol (TFTP) permite otimizar o tráfego TFTP quando estiver a utilizar o PXE para satisfazer os seus requisitos de rede específicos.

Para mais detalhes, consulte [Prepare as funções do sistema](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)do site para implementações do sistema operativo com o Gestor de Configuração .

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="smart-lock-setting-for-android-devices"></a>Definição de smart lock para dispositivos Android
Uma nova configuração, **Allow Smart Lock e outros agentes fidedignos,** foi adicionada ao item de configuração Android e Samsung KNOX Standard.

Esta definição permite controlar a funcionalidade Smart Lock em dispositivos Android compatíveis. Esta capacidade do telefone, por vezes conhecida como "agentes fidedignos", permite-lhe desativar ou contornar a palavra-passe do ecrã de bloqueio do dispositivo se o dispositivo estiver num local de confiança. Por exemplo, uma localização fidedigna pode ser quando está ligada a um dispositivo Bluetooth específico, ou quando está perto de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores configurem o Smart Lock.


## <a name="device-configuration-and-protection"></a>Configuração e proteção do dispositivo

### <a name="product-name-changes"></a>Alterações no nome do produto

* O Microsoft Passport for Work é agora conhecido como **Windows Hello for Business**.
* A Proteção de dados da empresa é agora conhecida como **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementação do Windows Hello for Business (Passaporte para trabalho)

Agora pode implementar políticas do Windows Hello for Business para dispositivos Windows 10 juntos ao domínio geridos pelo cliente Do Gestor de Configuração.

A consola 'Gestor de Configuração' foi atualizada para refletir estas alterações.

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS
O Gestor de Configuração pode ajudá-lo a gerir o iOS Activation Lock, uma funcionalidade da aplicação Find My iPhone para dispositivos iOS 7.1 e posteriores. Quando o Bloqueio de Ativação está ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:
* Desligue encontrar o meu iPhone.
* Apagar o dispositivo.
* Reativar o dispositivo.

O Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação de duas formas:

- Ative o Bloqueio de Ativação em dispositivos supervisionados.
- Ignore o Bloqueio de Ativação em dispositivos supervisionados.


### <a name="microsoft-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Microsoft Defender

A Proteção do Ponto Final pode ajudar a gerir e monitorizar a Proteção avançada de ameaças do Microsoft Defender (ATP). O Microsoft Defender ATP é um novo serviço que ajudará as empresas a detetar, investigar e responder a ataques avançados nas suas redes. As políticas do Gestor de Configuração podem ajudá-lo a bordo e monitorizar computadores geridos com o Windows 10, versão 1607 (construir 14328) ou mais tarde.

Para mais detalhes, consulte [a Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorias de dispositivos
Pode criar categorias de dispositivos, que podem ser usados para colocar dispositivos nas coleções dos dispositivos automaticamente quando estiver a utilizar o 'Configuração Manager' com o Microsoft Intune. Os utilizadores são então obrigados a escolher uma categoria de dispositivo quando matriculam um dispositivo em Intune. Além disso, pode alterar a categoria de um dispositivo a partir da consola 'Gestor de Configuração'.

Para mais detalhes, consulte [Como categorizar automaticamente os dispositivos em coleções com o Gestor](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)de Configuração .

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série IMEI ou iOS

Pode identificar dispositivos corporativos importando os números de identidade de equipamento móvel da estação internacional (IMEI) ou números de série iOS. Pode fazer o upload de um ficheiro de valores separados da vírem (.csv) contendo números IMEI do dispositivo, ou pode introduzir manualmente as informações do dispositivo. A informação importada define a propriedade dos dispositivos que se inscrevem como "Corporate" em listas de dispositivos. É ainda necessária uma licença Intune para cada utilizador que aceda ao serviço.

### <a name="on-premises-health-attestation-service-communication"></a>Comunicação de serviço de attestation de saúde no local

Agora pode ativar a monitorização dos serviços de Attestation de Saúde para computadores Windows 10 utilizando apenas infraestruturas no local, para que os computadores sem acesso à Internet possam reportar attestation de saúde do dispositivo (DHA).

Para mais detalhes, consulte [A estação de saúde para O Gestor de Configuração](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Controlo Remoto
Permita aos seus utilizadores a oportunidade de aceitar ou negar transferências de ficheiros antes de transferir conteúdo da área partilhada numa sessão de controlo remoto. Os utilizadores só precisam de conceder permissão uma vez por sessão, e o espectador não tem a capacidade de se dar permissão para avançar com a transferência de ficheiros. Você pode encontrar este novo cenário no espaço de trabalho **da Administração.** Vá às **Definições do Cliente**, e depois nas **Definições predefinidas,** abra o painel **de ferramentas remotas.**
