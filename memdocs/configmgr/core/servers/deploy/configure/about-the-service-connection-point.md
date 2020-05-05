---
title: Ponto de ligação de serviço
titleSuffix: Configuration Manager
description: Conheça esta função do sistema do site do Gestor de Configuração e compreenda e planeie a sua gama de utilizações.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721186"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Sobre o ponto de ligação de serviço no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O ponto de ligação ao serviço é uma função do sistema de site que fornece várias funções importantes para a hierarquia. Antes de configurar o ponto de ligação de serviço, compreenda e planeie a sua gama de utilizações. O planeamento para a utilização pode afetar a forma como configura este papel do sistema do site:

- Descarregue as atualizações aplicáveis à sua infraestrutura de Gestor de Configuração. Apenas são disponibilizadas atualizações relevantes para a sua infraestrutura com base nos dados de utilização que envia.

- Faça upload dos dados de utilização da sua infraestrutura de Gestor de Configuração. Pode controlar o nível ou a quantidade de detalhes que envia. Para mais informações, consulte os níveis e configurações dos [dados de utilização.](../install/setup-reference.md#bkmk_usage)

- Implementar uma porta de entrada de [gestão](../../../clients/manage/cmg/plan-cloud-management-gateway.md) de nuvem em Azure

- Sincronizar aplicações da [Microsoft Store para Negócios e Educação](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Descubra utilizadores e grupos no [Azure Ative Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Use [desktop Analytics](../../../../desktop-analytics/overview.md) para obter informações sobre atualização do Windows 10 e a prontidão da aplicação

Cada hierarquia apoia um único exemplo deste papel. Só pode ser instalado no local de topo da sua hierarquia, que é um site de administração central (CAS) ou um local primário autónomo. Se expandir um local primário autónomo para uma hierarquia maior, desinstale esta função a partir do local principal e, em seguida, instale-o no CAS.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>Modos de funcionamento

O ponto de ligação de serviço suporta dois modos de funcionamento:

- **Online**: O ponto de ligação ao serviço verifica automaticamente a cada 24 horas para obter atualizações. Descarrega novas atualizações que estão disponíveis para a sua atual versão de infraestrutura e produto para disponibilizá-las na consola 'Gestor de Configuração'.

- **Offline**: O ponto de ligação ao serviço não se liga ao serviço de nuvem da Microsoft. Para importar manualmente as atualizações disponíveis, utilize a ferramenta de [ligação](../../manage/use-the-service-connection-tool.md)de serviço .

### <a name="change-mode"></a>Alterar o modo

Se alterar entre modos online ou offline depois de instalar o ponto de ligação de serviço, reinicie a linha **SMS_DMP_DOWNLOADER** do serviço SMS_Executive. Reiniciar este fio torna a mudança eficaz. Para reiniciar este fio, utilize o Gestor de Serviço de Gestor de Configuração.

> [!TIP]
> Também pode reiniciar o serviço SMS_Executive para O Gestor de Configuração, que reinicia a maioria dos componentes do site. Em alternativa, aguarde uma tarefa programada como um backup do site, que para e reinicia o serviço de SMS_Executive para si.

Para utilizar o Gestor de Serviço de Gestor de Configuração para reiniciar o fio SMS_DMP_DOWNLOADER:

1. Na consola do Gestor de Configuração vá ao espaço de trabalho **de monitorização,** expanda o **Estado do Sistema**e selecione o nó de Estado do **Componente.** Na fita, escolha **Iniciar**, e, em seguida, selecione Gestor de Serviço de Gestor de **Configuração**.

1. No painel de navegação do gestor de serviços, expanda o site, expanda **componentes,** e depois escolha o componente que pretende reiniciar: **SMS_DMP_DOWNLOADER**.

1. Vá ao menu **Component** e escolha **Consulta.**

1. Confirme o estado atual do componente. Em seguida, vá ao menu **Component** e escolha **Parar**.  

1. **Consultar** o componente novamente para confirmar que parou. Em seguida, escolha a ação do componente **Iniciar** para reiniciá-lo.

## <a name="remote-site-system-requirements"></a>Requisitos do sistema de site remoto

Quando instalar o ponto de ligação de serviço num servidor de sistema de site que esteja afastado do servidor do site, configure os seguintes requisitos:

- A conta de computador do servidor do site deve ser uma administração local no computador que acolhe um ponto de ligação de serviço remoto.

- Configurar o servidor do sistema do site que acolhe esta função com uma conta de [instalação](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)do sistema de site . O gestor de distribuição no servidor do site utiliza a conta de instalação do sistema do site para transferir atualizações do ponto de ligação ao serviço.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a>Requisitos de acesso à Internet

Se a sua organização restringir a comunicação de rede com a internet utilizando um firewall ou dispositivo proxy, tem de permitir que o ponto de ligação de serviço aceda a pontos finais da Internet.

Para mais informações, consulte os requisitos de [acesso à Internet.](../../../plan-design/network/internet-endpoints.md#bkmk_scp)

## <a name="install"></a>Instalar

Quando executar a **Configuração** para instalar o local de topo de uma hierarquia, pode instalar o ponto de ligação de serviço.

Depois de ser executado o funcionamento da configuração, ou se estiver a reinstalar a função, utilize o assistente de **funções** do sistema do site adicionar ou o assistente do Servidor do Sistema de Criar o **Site.** (Instale apenas o ponto de ligação de serviço no local de topo da sua hierarquia.) Para mais informações, consulte [Instalar as funções](install-site-system-roles.md)do sistema do site.

## <a name="move-the-role"></a><a name="bkmk_move"></a>Mover o papel

<!-- SCCMDocs#922 -->
Existem vários cenários em que poderá ser necessário mover o ponto de ligação de serviço para outro servidor:

- [Recuperação](../../manage/recover-sites.md)
- [Elevada disponibilidade do servidor do site](site-server-high-availability.md)
- [Expansão do site](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Depois de mover o ponto de ligação de serviço, verifique todas as funções do site. Por exemplo, poderá ter de renovar a chave secreta para quaisquer ligações com os inquilinos do Azure Ative Directory (Azure AD). Para mais informações, consulte [Renovar a chave secreta.](azure-services-wizard.md#bkmk_renew)

## <a name="log-files"></a>Ficheiros de registo

Para visualizar informações sobre uploads para a Microsoft, veja o **Dmpuploader.log** no servidor que executa o ponto de ligação ao serviço. Para fazer o download de atualizações, consulte o **Dmpdownloader.log**. Para obter a lista completa de registos relacionados com o ponto de ligação ao serviço, consulte [ficheiros de registo - ponto de ligação](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog)de serviço .

## <a name="next-steps"></a>Passos seguintes

Utilize os seguintes fluxogramas para compreender o fluxo de processo e as entradas de registo chave. Este processo inclui downloads de atualização e replicação de atualizações para outros sites.

- [Fluxograma – Transferir atualizações](../../manage/download-updates-flowchart.md)

- [Fluxograma – Atualizar replicação](../../manage/update-replication-flowchart.md)
