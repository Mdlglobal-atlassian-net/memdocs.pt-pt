---
title: Planear o Centro de Software
titleSuffix: Configuration Manager
description: Decida como pretende configurar e marcar o Centro de Software para os utilizadores interagirem com o ConfigurManager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15da90b12504fdaf7a4dd0a36704391eead877cd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709930"
---
# <a name="plan-for-software-center"></a>Planear o Centro de Software

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os utilizadores alteram as definições, navegam para aplicações e instalam aplicações a partir do Software Center. Quando instala o cliente do Gestor de Configuração num dispositivo Windows, também instala automaticamente o Centro de Software.

Para obter mais informações sobre as outras funcionalidades do Software Center, consulte o guia de utilizador do Centro de [Software](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Configure Software Center  

Atualize os seus sites e clientes do Gestor de Configuração para a versão 1906 ou mais tarde para beneficiar das mais recentes melhorias.

Reveja as seguintes melhorias para o Centro de Software:

> [!Important]  
> Estas melhorias iterativas para o Software Center e o ponto de gestão são para reformar as funções de catálogo de aplicações.
>
> - A experiência do utilizador Silverlight não é suportada a partir da versão atual do ramo 1806.
> - A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações.
> - O suporte termina para as funções de catálogo de aplicações com a versão 1910.  

### <a name="starting-in-version-1802"></a>Começando na versão 1802

- A definição do cliente **Utilize o novo Centro** de Software no grupo Agente **Informático** está ativado por padrão. A versão anterior do Software Center já não é suportada. Para mais informações, consulte [funcionalidades removidas e depreciadas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

- Os utilizadores podem navegar e instalar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure Ative Directory (Azure AD). Para mais informações, consulte [implementar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure AD](../deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

### <a name="starting-in-version-1806"></a>Começando na versão 1806

- Especifique a visibilidade do link do site do catálogo de aplicações no separador Estado de **Instalação** do Centro de Software. Para mais informações, consulte as definições do cliente [do Software Center.](../../core/clients/deploy/about-client-settings.md#software-center)  

- As funções de catálogo de aplicações já não são necessárias para exibir aplicações disponíveis pelo utilizador no Software Center. Esta alteração ajuda-o a reduzir a infraestrutura de servidores necessária para entregar aplicações aos utilizadores. O Software Center conta agora com o ponto de gestão para obter esta informação, o que ajuda a maiores ambientes a escalar melhor, atribuindo-os a [grupos de fronteira.](../../core/servers/deploy/configure/boundary-groups.md#management-points)<!--1358309-->  

    > [!Note]  
    > Se está a utilizar o catálogo de aplicações e atualize o 'Gestor de Configuração' para a versão 1806, continua a funcionar. As funções de ponto de página do catálogo de aplicações e do ponto de serviço web já não são *necessárias,* mas ainda *suportadas.* A experiência do **utilizador Silverlight** para o ponto de *site* do catálogo de aplicações já não é suportada. Para mais informações, consulte [funcionalidades removidas e depreciadas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).
    >
    > Comece a planear remover as funções de catálogo de aplicações da sua infraestrutura no futuro. Aproveite as melhorias do Software Center para utilizar o ponto de gestão e simplificar o ambiente do Gestor de Configuração.  

### <a name="starting-in-version-1902"></a>Começando na versão 1902

- Configure a afinidade do dispositivo do utilizador. Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

### <a name="starting-in-version-1906"></a>Começando na versão 1906

- O Software Center comunica agora com um ponto de gestão para aplicações direcionadas aos utilizadores conforme disponível. Já não usa o catálogo de aplicações. Esta alteração facilita a sua remoção do catálogo de aplicações do site.

- Anteriormente, o Software Center escolheu o primeiro ponto de gestão da lista de servidores disponíveis. A partir deste lançamento, utiliza o mesmo ponto de gestão que o cliente utiliza. Esta alteração permite ao Software Center utilizar o mesmo ponto de gestão do site primário atribuído que o cliente.

- O ponto de gestão tem pontos finais do Software Center para suportar estas novas funcionalidades. Verifica agora a saúde destes pontos finais a cada cinco minutos. Reporta quaisquer problemas através de mensagens de estado para o componente do site SMS_MP_CONTROL_MANAGER.

- Não é possível adicionar novas funções de catálogo de aplicações ao site. Os papéis existentes continuam a funcionar. Apenas os clientes existentes utilizam o catálogo de aplicações para implementações disponíveis pelo utilizador. Os clientes atualizados utilizam automaticamente o ponto de gestão para todas as implementações.

- Pode adicionar até 5 separadores personalizados ao Centro de Software. Para mais informações, consulte [as definições do cliente do Software Center](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>Resumo dos requisitos de infraestrutura por versão

Utilize a tabela seguinte para ajudar a compreender os requisitos para o Centro de Software, dependendo da versão específica do Gestor de Configuração:

| Tipo de Dispositivo | Versão do site | Infraestrutura |
|-----------------|--------------|----------------|
| Dispositivo azure ad-join<br>(ou "cloud domínio-joined") | 1802 ou 1806 | Ponto de gestão para todas as implementações de aplicações |
| [Dispositivo híbrido azure ad-join na](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) internet | 1802 ou 1806 | Gateway de gestão de nuvem e ponto de gestão para todas as implementações de aplicações |
| Dispositivo de domínio ative diretório no local | 1802 | Catálogo de aplicações necessário para aplicações disponíveis pelo utilizador através do Centro de Software |
| Dispositivo de domínio ative diretório no local | 1806 | Ponto de gestão para todas as implementações de aplicações |

> [!Important]  
> Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.


## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a>Substitua as notificações de torradas por janela de diálogo

<!--3555947-->
Por vezes, os utilizadores não vêem a notificação do Brinde do Windows sobre um reinício ou implementação necessária. Então não vêem a experiência para dormir o lembrete. Este comportamento pode levar a uma má experiência do utilizador quando o cliente atinge um prazo.

A partir da versão 1902, quando [são necessárias alterações](#software-changes-are-required) de software ou as implementações [precisam de ser reiniciadas,](#restart-required)tem a opção de utilizar uma janela de diálogo mais intrusiva.

### <a name="software-changes-are-required"></a>Alterações de software são necessárias

Quando [implementar uma aplicação](../deploy-use/deploy-applications.md) conforme necessário com um prazo no futuro, na página **da Experiência** do Utilizador do Assistente de Software de Implementação, selecione as seguintes opções de notificação do utilizador:

- **Exibir no Centro de Software e mostrar todas as notificações**
- **Quando forem necessárias alterações de software, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torradas**

Configurar esta definição de implementação altera a experiência do utilizador para este cenário.

A partir da seguinte notificação de torrada:

![Notificação de torradas de que são necessárias alterações de Software](media/3555947-required-toast.png)  

Para a seguinte janela de diálogo:

![Janela de diálogo para alterações de software necessárias](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Reiniciar necessário

No grupo [de reiniciar](../../core/clients/deploy/about-client-settings.md#computer-restart) computadores as definições do cliente, ative a seguinte opção: Quando **uma implementação necessitar de um reinício, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torrada**.  

Configurar esta definição de cliente altera a experiência do utilizador para todas as implementações necessárias que requerem um reinício dos seguintes tipos:

- [Aplicação](../deploy-use/deploy-applications.md)
- [Sequência de tarefas](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Atualização de software](../../sum/deploy-use/deploy-software-updates.md)

A partir da seguinte notificação de torrada:

![Notificação de torrada saque a que é necessário reiniciar](media/3555947-restart-toast.png)  

Para a seguinte janela de diálogo:

![Janela de diálogo para reiniciar o seu computador](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> Em Configuração Manager 1902, sob certas circunstâncias, a caixa de diálogo não substituirá as notificações de torradas. Para resolver este problema, instale o rollup da atualização para a [versão 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)do Gestor de Configuração . <!--4404715-->

## <a name="branding-software-center"></a>Centro de Software de Branding

Altere a aparência do Software Center para satisfazer os requisitos de marca da sua organização. Esta configuração ajuda os utilizadores a confiar no Software Center.

### <a name="configure-software-center-branding"></a>Marca configure Software Center

<!-- 1351224 -->
Personalize a aparência do Software Center adicionando os elementos de marca da sua organização e especificando a visibilidade dos separadores.

Para obter mais informações, veja os artigos seguintes:

- [Grupo](../../core/clients/deploy/about-client-settings.md#software-center) de software center de configurações de clientes  
- [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Prioridades de marcação

O Gestor de Configuração aplica a marca personalizada para o Centro de Software de acordo com as seguintes prioridades:  

1. **Configurações** do cliente do Software Center. Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#software-center).  

2. **Configuração** de cliente de nome de organização no grupo **de agente informático.** Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Prioridades de marca de catálogo de aplicações

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  

Se estiver a utilizar o catálogo de aplicações, a marca segue estas prioridades:  

1. **Configurações** do cliente do Software Center. Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#software-center).  

2. O nome e *a cor* da *organização* que especifica no site do catálogo de aplicações apontam propriedades. Para mais informações, consulte opções de Configuração para o ponto do site do catálogo de [aplicações.](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)  

3. **Configuração** de cliente de nome de organização no grupo **de agente informático.** Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).  


## <a name="see-also"></a>Consulte também

- [Manual do utilizador do Software Center](../../core/understand/software-center.md)
- [Planear e configurar a gestão de aplicações](plan-for-and-configure-application-management.md)
