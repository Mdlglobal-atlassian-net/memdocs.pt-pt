---
title: Aprovar aplicações
titleSuffix: Configuration Manager
description: Conheça as definições e comportamentos para aprovação de aplicações no Gestor de Configuração.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f725c1b7dc380a84cd94e666b98dbd309df3744c
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802060"
---
# <a name="approve-applications-in-configuration-manager"></a>Aprovar aplicações no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Ao [implementar uma aplicação](deploy-applications.md) no 'Gestor de Configuração', pode necessitar de aprovação antes da instalação. Os utilizadores solicitam a aplicação no Software Center e, em seguida, revê o pedido na consola Do Gestor de Configuração. Pode aprovar ou negar o pedido.

## <a name="approval-settings"></a><a name="bkmk_approval"></a>Definições de aprovação

O comportamento de aprovação da aplicação depende se você permite a experiência de [aprovação de aplicações opcional](#bkmk_opt)recomendada. Uma das seguintes definições de aprovação aparece na página de Definições de **Implementação** da implementação da aplicação:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a>Um administrador deve aprovar um pedido para este pedido no dispositivo

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade por defeito. Antes de a utilizar, ative a funcionalidade opcional Aprovar pedidos de **aplicação para utilizadores por dispositivo**. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Se não ativar esta funcionalidade, verá a [experiência anterior.](#bkmk_prior)  

O administrador aprova quaisquer pedidos de utilizador para a aplicação antes de o utilizador poder instalá-lo no dispositivo solicitado. Se o administrador aprovar o pedido, o utilizador só poderá instalar a aplicação nesse dispositivo. O utilizador deve submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é cinzenta quando o objetivo de implementação é **necessário**, ou quando você implementa a aplicação para uma recolha de dispositivos. <!--1357015-->  

> [!Note]  
> Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.<!--SCCMDocs issue 646-->  

Ver **Pedidos de Aplicação** sob gestão de **aplicações** no espaço de trabalho da Biblioteca de **Software** da consola De Configuração Manager. (Na versão 1902 e anterior, este nó chama-se Pedidos de **Aprovação**.) Há agora uma coluna de **dispositivos** na lista para cada pedido. Quando toma medidas sobre o pedido, o diálogo do Pedido de Pedido de Pedido também inclui o nome do dispositivo a partir do qual o utilizador submeteu o pedido.

Se um pedido não for aprovado dentro de 30 dias, é removido. A reinstalação do cliente pode cancelar quaisquer pedidos de aprovação pendentes.  

Quando necessita de aprovação numa implementação para uma coleção de dispositivos, a aplicação não é apresentada no Software Center. Se necessitar de aprovação numa implementação para uma coleção de utilizadores, a aplicação é apresentada no Software Center. Ainda pode escondê-lo dos utilizadores com a definição do cliente, **ocultar aplicações não aprovadas no Software Center**. Para mais informações, consulte [as definições do cliente do Software Center](../../core/clients/deploy/about-client-settings.md#software-center).

Depois de ter aprovado uma aplicação para instalação, pode **negar** o pedido na consola 'Gestor de Configuração'. Se os utilizadores ainda não instalaram a aplicação, esta ação impede-os de instalar novas cópias da aplicação a partir do Software Center. Se uma aplicação foi previamente aprovada e instalada, quando **nega** o pedido da aplicação, o cliente desinstala a aplicação a partir do dispositivo do utilizador.<!--1357891-->

A partir da versão 1906, se aprovar espetado um pedido de aplicação na consola e depois negá-lo, pode agora aprová-lo novamente. A aplicação é reinstalada no cliente depois de a aprovar.  <!-- 4224910 -->

Automatizar o processo de aprovação com o [CmDLet Approve-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) PowerShell. A partir da versão 1902, este cmdlet inclui o parâmetro **InstallActionBehavior.** Utilize este parâmetro para especificar se instala a aplicação imediatamente ou durante o horário não comercial.<!-- SCCMDocs-pr issue #3418 -->

A partir de 1906, pode ver quais as implementações que requerem aprovação. Selecione uma aplicação no nó de **Aplicações.** No painel de detalhes, mude para o separador **De implantação.** Há uma nova coluna exibida por defeito, **requer aprovação**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a>Voltar a instalar aplicações pré-aprovadas

<!--4336307-->
A partir da versão 1906, pode voltar a tentar a instalação de uma aplicação que aprovou anteriormente para um utilizador ou dispositivo. A opção de aprovação é apenas para implementações disponíveis. Se o utilizador desinstalar a aplicação, ou se o processo de instalação inicial falhar, o 'Gestor de Configuração' não reavalia o seu estado e reinstala-a. Esta funcionalidade permite que um técnico de suporte retente rapidamente a instalação da aplicação para um utilizador que pede ajuda.

1. Abra a consola 'Gestor de Configuração' como um utilizador que tenha a permissão **De aprovação** no objeto De aplicação. Por exemplo, o Administrador de **Aplicação** ou Autor de **Aplicação** tem esta permissão.

1. Implemente uma aplicação que requer aprovação e aprove-a.

    > [!Tip]  
    > Em alternativa, [instale uma aplicação para um dispositivo](install-app-for-device.md). Cria um pedido aprovado para a aplicação no dispositivo.  

Se a aplicação não instalar com sucesso, ou se o utilizador desinstalar a aplicação, utilize o seguinte processo para voltar a tentar:

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de Pedidos de **Aplicação.** (Na versão 1902 e anterior, este nó chama-se Pedidos de **Aprovação**.)

1. Selecione a aplicação previamente aprovada. No grupo De pedido de aprovação da fita, selecione **Retry instalar**.

#### <a name="other-app-approval-resources"></a>Outros recursos de aprovação de aplicativos

- [Melhoriada na aprovação de candidaturas na ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Atualizações do processo de aprovação da aplicação no Gestor de Configuração](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a>Exigir aprovação do administrador se os utilizadores solicitarem esta aplicação

> [!Note]  
> Esta experiência aplica-se se não permitir a experiência de [aprovação de aplicações opcional](#bkmk_opt)recomendada.

O administrador aprova quaisquer pedidos de utilizador para a aplicação antes de o utilizador poder instalá-la. Esta opção é cinzenta quando o objetivo de implementação é **necessário**, ou quando você implementa a aplicação para uma recolha de dispositivos.  

Os pedidos de aprovação de aplicações são apresentados no nó de Pedidos de **Aplicação,** no âmbito da Gestão de **Aplicações** no espaço de trabalho da Biblioteca de **Software.** (Na versão 1902 e anterior, este nó chama-se Pedidos de **Aprovação**.) Se um pedido não for aprovado dentro de 30 dias, é removido. A reinstalação do cliente pode cancelar quaisquer pedidos de aprovação pendentes.  

Depois de ter aprovado uma aplicação para instalação, pode **negar** o pedido na consola 'Gestor de Configuração'. Esta ação não faz com que o cliente desinstale a aplicação a partir de quaisquer dispositivos. Impede os utilizadores de instalarem novas cópias da aplicação a partir do Software Center.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a>Notificações por e-mail

<!--1321550-->

Pode configurar notificações de e-mail para pedidos de aprovação de pedidos de aplicação. Quando um utilizador solicita uma aplicação, recebe um e-mail. Clique em links no e-mail para aprovar ou negar o pedido, sem necessitar da consola 'Gestor de Configuração'.

Pode definir os endereços de e-mail dos utilizadores que podem aprovar ou negar o pedido enquanto cria uma nova implementação para a aplicação. Se precisar de alterar a lista de endereços de e-mail posteriormente, vá ao espaço de trabalho **de Monitorização,** expanda **Alertas**e selecione o nó **de Subscrições.** Selecione **Propriedades** a partir de uma das **aplicações De aprovação através** de subscrições de e-mail relacionadas com a implementação da sua aplicação.

Se houver mais de um alerta, pode determinar qual o alerta que vai com que implantação. Abra as propriedades de alerta e veja a lista de **alertas Selecionados** no separador Geral. A implementação está ativada como o alerta para esta subscrição.

Os utilizadores podem adicionar um comentário ao pedido do Software Center. Este comentário mostra o pedido de aplicação na consola Do Gestor de Configuração. A partir da versão de 1902, esse comentário também mostra no e-mail. Incluir este comentário no e-mail ajuda os aprovadores a tomar uma melhor decisão para aprovar ou negar o pedido.<!--3594063-->

### <a name="prerequisites"></a>Pré-requisitos

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Enviar notificações por e-mail e tomar medidas na rede interna

Com estes pré-requisitos, os destinatários recebem um e-mail com notificação do pedido. Se estiverem na rede interna, também podem aprovar ou negar o pedido do e-mail.

- Ativar a [funcionalidade opcional](../../core/servers/manage/install-in-console-updates.md#bkmk_options) Aprove os pedidos de **aplicação para utilizadores por dispositivo**.  

- Configure a notificação de [e-mail para alertas](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

    > [!NOTE]
    > O utilizador administrativo que implementa a aplicação necessita de autorização para criar um alerta e subscrição. Se este utilizador não tiver estas permissões, verá um erro no final do Assistente de **Software de Implementação:**"Não tem direitos de segurança para executar esta operação."<!-- 2810283 -->

- Ative o Fornecedor SMS no local principal para utilizar um certificado.<!--SCCMDocs-pr issue 3135--> Utilize uma das seguintes opções:  

  - (Recomendado) Ativar [http melhorado](../../core/plan-design/hierarchy/enhanced-http.md) para o local principal.

    > [!Note]  
    > Quando o site principal criar um certificado para o Fornecedor SMS, não será confiado pelo navegador web no cliente. Com base nas suas definições de segurança, ao responder a um pedido de pedido, pode ver um aviso de segurança.  

  - Ligue manualmente um certificado baseado em PKI à porta 443 no IIS no servidor que acolhe a função de Provedor de SMS no local principal.

> [!NOTE]
> Se tiver vários locais primários infantis numa hierarquia, configure estes pré-requisitos para cada local primário onde pretende ativar esta funcionalidade. Os links na notificação de e-mail são para o serviço de administração no site principal.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Para tomar medidas da internet

Com estes pré-requisitos opcionais adicionais, os destinatários podem aprovar ou negar o pedido de qualquer lugar que tenham acesso à Internet.

- Ative o serviço de administração do SMS Provider através do portal de gestão de nuvem. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione o nó de Funções de **Servidores e Derôs.** Selecione o servidor com a função SMS Provider. No painel de detalhes, selecione a função **De Fornecedor SMS** e selecione **Propriedades** na fita no separador Role do Site. Selecione a opção de permitir o tráfego de gateway de gestão de nuvem do Gestor de **Configuração para o serviço de administração**.  

- O Provedor de SMS requer **.NET 4.5.2** ou mais tarde.  

- Criar um portal de gestão de [nuvens.](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)

- A bordo do site para [os serviços Azure](../../core/servers/deploy/configure/azure-services-wizard.md) para gestão de **nuvem.**

- Ativar a descoberta do [utilizador da AD Azure](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Configure manualmente as definições em Azure AD:  

    1. Vá ao [portal Azure](https://portal.azure.com) como utilizador com permissões *global de administração.* Vá ao **Diretório Ativo Azure**e selecione registos de **Aplicativos.**  

    1. Selecione a aplicação que criou para a integração do Gestor de Configuração **cloud Management.**  

    1. No menu **Gerir,** **selecione Autenticação**.  

        1. Na secção **REdirecionamento de URIs,** cola no seguinte caminho:`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. `<CMG FQDN>`Substitua-a com o nome de domínio totalmente qualificado (FQDN) do seu serviço de gateway de gestão de nuvem (CMG). Por exemplo, GraniteFalls.Contoso.com.  

        1. Em seguida, selecione **Guardar**.  

    1. No menu **Gerir,** selecione **Manifesto**.  

        1. No painel de manifesto edite, encontre a propriedade **oauth2AllowImplicitFlow.**  

        1. Mude o seu valor para **verdadeiro.** Por exemplo, toda a linha deve parecer a seguinte linha:`"oauth2AllowImplicitFlow": true,`  

        1. Selecione **Guardar**.  

### <a name="configure-email-approval"></a>Configure a aprovação de e-mail

1. Na consola 'Gestor de Configuração', [implemente uma aplicação](deploy-applications.md) disponível para uma recolha de utilizadores. Na página Definições de **Implementação,** ative-a para aprovação. Em seguida, insira um ou mais endereços de e-mail para receber notificação. Endereços de e-mail separados com um ponto-semi-cólon `;` ().  

     > [!Note]  
     > Qualquer pessoa na sua organização Azure AD que receba o e-mail pode aprovar o pedido. Não envie o e-mail para os outros a menos que queira que tomem medidas.  

2. Como utilizador, solicite a aplicação no Centro de Software.  

3. Recebe uma notificação por e-mail dentro de cinco minutos. O conteúdo do e-mail é semelhante ao seguinte exemplo:  

![Notificação por e-mail de exemplo para aprovação de pedido](media/1321550-email.png)

> [!Note]  
> O link para aprovar ou negar é para uma utilização única. Por exemplo, configura um pseudónimo de grupo para receber notificações. Meg aprova o pedido. Agora bruce não pode negar o pedido.  

Reveja o ficheiro **NotiCtrl.log** no servidor do site para resolução de problemas.

## <a name="maintenance"></a>Manutenção

O Gestor de Configuração armazena as informações sobre o pedido de aprovação da aplicação na base de dados do site. Para pedidos que sejam cancelados ou negados, o site elimina o histórico de pedidos após 30 dias. Pode configurar este comportamento de eliminação com a tarefa de manutenção do [site](../../core/servers/manage/maintenance-tasks.md)de dados de pedido de pedido de **pedido de aplicação de formulário** . O site nunca elimina quaisquer pedidos de pedido aprovados ou pendentes.
