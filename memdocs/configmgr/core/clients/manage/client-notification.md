---
title: Notificação de cliente
titleSuffix: Configuration Manager
description: Gerencie os clientes tomando medidas imediatas a partir da consola central do Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714095"
---
# <a name="client-notification-in-configuration-manager"></a>Notificação do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para tomar medidas imediatas sobre clientes remotos, envie uma ação de notificação do cliente a partir da consola Do Gestor de Configuração. Inicie estas ações num dispositivo individual ou numa coleção de dispositivos.

## <a name="actions"></a>Ações

As seguintes ações estão na fita do grupo Dispositivo ou Recolha do separador Home.

### <a name="install-client"></a>Instalar cliente

Abre o **Assistente de Cliente de Instalação.** Este assistente utiliza a instalação de pressão do cliente para instalar um cliente do Gestor de Configuração. Para mais informações, consulte a [instalação do impulso do Cliente.](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)

#### <a name="permissions---install-client"></a>Permissões - Instalar cliente

Esta ação requer o **Recurso Modificado** e **permissões de Leitura** no objeto de **Recolha.**

As seguintes funções incorporadas têm estas permissões por defeito:

- Administrador da Aplicação  
- Administrador Total  
- Administrador de Infraestrutura  
- Administrador de Operações  
- Gestor de Implantação do OS  

Adicione estas permissões a quaisquer papéis personalizados que precisem de empurrar o cliente.

### <a name="run-script"></a>Executar o script

Abre o assistente **do Run Script** para executar um script PowerShell em todos os clientes da coleção. Para mais informações, consulte [Criar e executar scripts PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>Permissões - Executar script

Esta ação requer a permissão do **Script executar** no objeto **de recolha.**

As seguintes funções incorporadas têm esta permissão por defeito:

- Administrador Total  
- Administrador de Infraestrutura  
- Administrador de Operações  

Adicione esta permissão a quaisquer papéis personalizados que precisem de executar scripts.

### <a name="start-cmpivot"></a>Iniciar cmpivot

Inicia a **CMPivot**, que executa consultas em tempo real contra os dispositivos visados. Para mais informações, consulte [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>Permissões - Iniciar cmpivot

Esta ação requer as mesmas permissões que a ação do [guião Run.](#run-script)

A partir da versão 1906, pode utilizar a permissão **Run CMPivot** no objeto **Collection.**

## <a name="client-notification"></a>Notificação de cliente

Estas ações estão no menu de notificação do **Cliente,** na fita do grupo Dispositivo ou Recolha do separador Home.

Na versão 1806 ou anterior, a opção **notificação** do cliente só está disponível a partir do nó de Recolha de Dispositivos ou quando viu a adesão a uma Coleção de Dispositivos. A partir da versão 1810, pode iniciar uma **Notificação** do Cliente diretamente a partir do nó de **Dispositivos.** Não há mais um requisito para estar dentro de uma vista de membros da coleção. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Permissões - Notificação do cliente

<!--SCCMDocs-pr issue #2972-->
A partir da versão 1810, as ações de notificação do cliente exigem agora a permissão de **Recurso notificar** no objeto de Recolha. Esta permissão aplica-se a todas as ações no menu de notificação do **Cliente.**

As seguintes funções incorporadas têm esta permissão por defeito:

- Administrador Total  
- Administrador de Operações  

Adicione esta permissão a quaisquer funções personalizadas que precisem de usar ações de notificação do cliente.

### <a name="download-computer-policy"></a>Baixar a política do computador

Refresque a política do dispositivo. Para mais informações, consulte [Iniciar a recuperação de políticas para um cliente do Gestor de Configuração](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Baixar a política do utilizador

Refresque a política do utilizador.  

### <a name="collect-discovery-data"></a>Recolher dados de descoberta

Desencadear clientes para enviar um registo de dados de descoberta (DDR). Para mais informações, consulte a [descoberta do Heartbeat.](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)  

### <a name="collect-software-inventory"></a>Recolher inventário de software

Desencadear clientes para executar um ciclo de inventário de software. Para mais informações, consulte [Introdução ao inventário de software](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Recolher inventário de hardware

Desencadear clientes para executar um ciclo de inventário de hardware. Para mais informações, consulte Introdução ao inventário de [hardware](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Avaliar as implementações de aplicações

Desencadear clientes para executar um ciclo de avaliação de implementação de aplicações. Para mais informações, consulte [a reavaliação do Horário para as implementações](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Avaliar implementações de atualizações de software

Desencadear clientes para executar um ciclo de avaliação de implementação de atualizações de software. Para mais informações, consulte [Introdução a atualizações de software](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Mude para o próximo ponto de atualização de software

Desencadear clientes para mudar para o próximo ponto de atualização de software disponível. Para mais informações, consulte a comutação do ponto de [atualização](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)do Software .  

### <a name="evaluate-device-health-attestation"></a>Avaliar o atestado de saúde do dispositivo

Extoque os clientes do Windows 10 para verificar e enviar o seu mais recente estado de saúde do dispositivo. Para mais informações, consulte A [estação de saúde.](../../servers/manage/health-attestation.md)  

### <a name="wake-up"></a>Acordar

A partir da versão 1810, os dispositivos de disparo configurados para suportar o Wake-on-LAN acordam utilizando outros dispositivos na mesma subnet para enviar o pacote Wake-on-LAN. Para mais informações, consulte [Como configurar Wake on LAN](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Reiniciar

Acione os dispositivos selecionados para reiniciar. Para mais informações, consulte [os clientes Restart](manage-clients.md#restart-clients).

## <a name="client-diagnostics"></a>Diagnósticos de clientes
<!--4433455-->

A partir da versão 1910, existem novas ações de dispositivos para **diagnósticode cliente** na consola De Configuração Manager. Foram acrescentadas as seguintes ações:

- **Ativar a exploração verbosa**: Mude o nível de registo global para o componente CCM verbose e permita a exploração de depuração.
- **Desative a exploração verbosa**: Mude o nível de registo global para o padrão e desative a exploração de depuração.
- **Colete Registos de Clientes** (a partir de 2002): Uma mensagem de notificação do cliente é enviada aos clientes selecionados para recolher os registos de CCM. Os registos são devolvidos utilizando a recolha de ficheiros de inventário de software. <!--4226618-->
   - O limite de tamanho para os registos de clientes comprimidos é de 100 MB. <!--6366098-->
   - Utilize o [Resource Explorer](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) gerir e ver estes ficheiros.

   [![Recolher registos de clientes da consola](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Estas ações só mudam a verbosidade do registo, não o tamanho ou história. Mais registo sinuoso pode gerar mais conteúdo de registo.
> - A função do ponto de gestão também utiliza a componente CCM. Se o dispositivo-alvo for também um ponto de gestão, esta ação aplica-se também a essa função.

Para obter mais informações sobre estas definições, consulte [sobre ficheiros](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)de registo .

Acompanhe o estado da tarefa no **diagnóstico.log** no cliente. Quando os registos dos clientes são recolhidos, informações adicionais são registadas em **MP_SinvCollFile.log** no ponto de gestão e **sinvproc.log** no servidor do site.

### <a name="prerequisites---client-diagnostics"></a>Pré-requisitos - Diagnósticos de clientes

- Atualize o cliente-alvo para a versão mais recente.

- O utilizador administrativo do Seu Gestor de Configuração necessita da permissão de **recurso notificação.**

  As seguintes funções incorporadas têm esta permissão por defeito:

  - Administrador Total  
  - Administrador de Infraestrutura  

  Adicione esta permissão a quaisquer funções personalizadas que precisem de usar ações de notificação do cliente.


## <a name="endpoint-protection"></a>Endpoint Protection

As seguintes ações estão no menu **endpoint Protection.** Este menu está na fita do grupo Coleção do separador Home. Quando seleciona um ou mais dispositivos, estas ações estão no separador **Objeto Selecionado** da fita.

Para mais informações, consulte [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).

### <a name="permissions---endpoint-protection"></a>Permissões - Proteção do Ponto Final

Esta ação requer a permissão de **segurança no** objeto **de recolha.**

As seguintes funções incorporadas têm esta permissão por defeito:

- Administrador Total  
- Gestor de Endpoint Protection  
- Administrador de Operações  

Adicione esta permissão a quaisquer funções personalizadas que precisem de desencadear ações de Proteção de Pontofinal.

### <a name="full-scan"></a>Varredura completa

Trigger Endpoint Protection ou Windows Defender para executar uma varredura *antimalware completa.*  

### <a name="quick-scan"></a>Sondagem rápida

Trigger Endpoint Protection ou Windows Defender para executar uma *rápida* varredura antimalware.  

### <a name="download-definition"></a>Definição de Download

Trigger Endpoint Protection ou Windows Defender para descarregar as definições antimalware mais recentes.  

## <a name="see-also"></a>Consulte também

- [Como gerir clientes](manage-clients.md)
- [Como gerir coleções](collections/manage-collections.md)
