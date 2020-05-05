---
title: Anexo de inquilino do Microsoft Endpoint Manager
titleSuffix: Configuration Manager
description: Faça upload dos seus dispositivos De Gestor de Configuração para o serviço de nuvem e tome ações do centro de administração.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e2b8c07a64265d33ade0b1c2c08c2d9c4096b741
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693469"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Anexo de inquilino do Microsoft Endpoint Manager: As ações de sincronização e dispositivos do dispositivo
<!--3555758 live 3/4/2020-->
*Aplica-se a: Gestor de Configuração (ramo atual)*

O Microsoft Endpoint Manager é uma solução integrada para gerir todos os seus dispositivos. A Microsoft reúne o Gestor de Configuração e o Intune numa única consola chamada **Microsoft Endpoint Manager .**

A partir da versão De Configuração Manager 2002, pode carregar os seus dispositivos De Configuração para o serviço de cloud e tomar ações da lâmina **de Dispositivos** no centro de administração.

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta que é um *Administrador Global* para iniciar sessão na aplicação desta alteração. Para mais informações, consulte as funções de administrador do [Azure Ative Directory (Azure AD).](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)
   - O onboarding cria uma app de terceiros e um primeiro diretor de serviço de festas no seu inquilino Azure AD.
- Um ambiente de nuvem pública Azure.
- As contas de utilizador que desencadeiam as ações do dispositivo têm os seguintes pré-requisitos:
   - Foi descoberto com a descoberta do [utilizador Azure Ative Directory](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) e com a descoberta do [utilizador Ative Directory.](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)
      - Isto significa que a conta de utilizador tem de ser um objeto de utilizador sincronizado no Azure AD.
   - A permissão de ação do Gestor de **Configuração Iniciado** sob **tarefas remotas** no centro de administração do Microsoft Endpoint Manager.


## <a name="internet-endpoints"></a>Pontos finais da Internet

- `https://aka.ms/configmgrgateway`
- `https://gateway.configmgr.manage.microsoft.com`
- `https://us.gateway.configmgr.manage.microsoft.com`
- `https://eu.gateway.configmgr.manage.microsoft.com`


## <a name="enable-device-upload"></a>Ativar o upload do dispositivo

- Se tiver a cogestão ativada atualmente, [editar propriedades de cogestão](#bkmk_edit) para ativar o upload do dispositivo.
- Se não tiver a cogestão ativada, [utilize o assistente de **cogestão Configure** ](#bkmk_config) para ativar o upload do dispositivo.
   - Pode fazer o upload dos seus dispositivos sem permitir a inscrição automática para cogestão ou troca de cargas de trabalho para Intune.
- Todos os Dispositivos geridos pelo Gestor de Configuração que tenham **Sim** na coluna **cliente** serão carregados. Se necessário, pode limitar o upload para uma única coleção de dispositivos.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Editar propriedades de cogestão para ativar o upload do dispositivo

Se tiver a cogestão ativada atualmente, edite as propriedades de cogestão para permitir o upload do dispositivo usando as instruções abaixo:

1. Na consola de administração do Gestor de Configuração, vá à **Administração** > **Visão Geral** > **da Cogestão**dos**Serviços** > cloud.
1. Clique à direita nas definições de cogestão e selecione **Propriedades**.
1. No **separador de upload Configure,** selecione Upload para o centro de administração do **Microsoft Endpoint Manager**. Clique em **Aplicar**.
   - A definição predefinida para o upload do dispositivo é **todos os meus dispositivos geridos pelo Microsoft Endpoint Configuration Manager**. Se necessário, pode limitar o upload para uma única coleção de dispositivos.

   [![Assistente de configuração de cogestão](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Inscreva-se na sua conta *De Administrador Global* quando solicitado.
1. Clique **em Sim** para aceitar a notificação de **Aplicação Create AAD.** Esta ação prevê um diretor de serviço e cria um registo de aplicação da AD Azure para facilitar a sincronização.
1. Clique em **OK** para sair das propriedades de cogestão uma vez que tenha feito alterações.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Utilize o assistente de cogestão Configure para ativar o upload do dispositivo
Se não tiver a cogestão ativada, utilize o assistente **de cogestão Configure** para ativar o upload do dispositivo. Pode fazer o upload dos seus dispositivos sem permitir a inscrição automática para cogestão ou troca de cargas de trabalho para Intune. Ativar o upload do dispositivo utilizando as instruções abaixo:

1. Na consola de administração do Gestor de Configuração, vá à **Administração** > **Visão Geral** > **da Cogestão**dos**Serviços** > cloud.
1. Na fita, clique em **Configurar co-management** para abrir o assistente.
1. Na página de embarque do **Tenant,** selecione **AzurePublicCloud** para o seu ambiente. A nuvem do Governo Azure não é apoiada.
1. Clique **em Iniciar sessão**. Use a sua conta *De Administrador Global* para iniciar sessão.
1. Certifique-se de que a opção **de centro de administração** do Microsoft Endpoint Manager é selecionada na página de embarque do **Tenant.**
   - Certifique-se de que a opção Ativar a **inscrição automática do cliente para cogestão** não é verificada se não quiser ativar a cogestão agora. Se pretender ativar a cogestão, selecione a opção.
   - Se ativar a cogestão juntamente com o upload do dispositivo, receber-lhe-á páginas adicionais no assistente para completar. Para mais informações, consulte [Enable co-management](../comanage/how-to-enable.md).

   [![Assistente de configuração de cogestão](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Clique **em Seguinte** e, em **seguida, sim** para aceitar a notificação de **Aplicação Create AAD.** Esta ação prevê um diretor de serviço e cria um registo de aplicação da AD Azure para facilitar a sincronização.
1. Na página de upload do **Configure,** selecione a definição de upload recomendada para **todos os meus dispositivos geridos pelo Microsoft Endpoint Configuration Manager**. Se necessário, pode limitar o upload para uma única coleção de dispositivos.
1. Clique em **Resumo** para rever a sua seleção e, em seguida, clique em **Next**.
1. Quando o assistente estiver completo, clique em **Fechar**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Reveja o seu upload

1. Abra **cmGatewaySyncUploadWorker.log** da &lt;ConfigMgr instale diretório>\Logs.
1. O tempo de sincronização seguinte é `Next run time will be at approximately: 02/28/2020 16:35:31`notado por entradas de registo semelhantes a .
1. Para uploads do dispositivo, procure `Batching N records`entradas de registo semelhantes a . **N** é o número de dispositivos enviados para a nuvem. 
1. O upload ocorre a cada 15 minutos para alterações. Uma vez que as alterações são enviadas, pode levar mais 5 a 10 minutos para que as alterações do cliente apareçam no **centro de administração do Microsoft Endpoint Manager**.

## <a name="perform-device-actions"></a>Realizar ações de dispositivo

1. Em um navegador, navegar para`endpoint.microsoft.com`
1. Selecione **Dispositivos** e, em seguida, **Todos os dispositivos** para ver os dispositivos carregados. Verá **configMgr** na **Coluna Gerida por** coluna para dispositivos carregados.
   [![Todos os dispositivos no centro de administração do Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Clique num dispositivo para carregar a sua página **de Visão Geral.**
1. Clique em qualquer uma das seguintes ações:
   - **Política de Máquina sincronizada**
   - **Política de Utilizador sincronizado**
   - **Ciclo de Avaliação de Aplicações**

   [![Visão geral do dispositivo no centro de administração do Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Problemas conhecidos

### <a name="specific-devices-dont-synchronize"></a>Dispositivos específicos não sincronizam

<!--7099564-->
É possível que dispositivos específicos, que são clientes do Gestor de Configuração, não sejam enviados para o serviço.

**Dispositivos impactados:** Se um dispositivo for um ponto de distribuição que utilize o mesmo certificado PKI tanto para a funcionalidade do ponto de distribuição como para o seu agente cliente, então o dispositivo não será incluído no dispositivo de anexação do inquilino.

**Comportamento:** Ao realizar a fixação do inquilino durante a fase de embarque, é realizada uma sincronização completa pela primeira vez. Os ciclos de sincronização subsequentes são sincronizações delta. Qualquer atualização dos dispositivos afetados fará com que o dispositivo seja removido da sincronização.

## <a name="log-files"></a>Ficheiros de registo
Utilize os seguintes registos localizados no ponto de ligação de serviço:

- **CMGatewaySyncUploadWorker.log**
- **CMGatewayNotificationWorker.log**

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o inquilino anexar ficheiros de registo, consulte [o inquilino da Troubleshoot anexado](technical-reference.md).
