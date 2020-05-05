---
title: Capacidades na Pré-visualização Técnica 1606
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721620"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1606 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1606. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    

**Questões Conhecidas nesta Pré-Visualização Técnica:**  
*  Quando atualiza si de Pré-visualização Técnica 1604 a 1605 e, em seguida, para a versão 1606, a atualização pode falhar e um erro semelhante ao seguinte é registado no **cmupdate.log**:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Se isto ocorrer, no nó **de Atualizações e Manutenção** clique em verificar **atualizações** **e,** em seguida, volte a tentar a instalação da atualização.
    ***

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a>Categorize automaticamente os dispositivos em coleções
Pode criar categorias de dispositivos, que podem ser usados para colocar automaticamente dispositivos nas coleções dos dispositivos quando estiver a utilizar o 'Configuração Manager' com o Microsoft Intune. Os utilizadores são então obrigados a escolher uma categoria de dispositivo quando matriculam um dispositivo em Intune. Pode ainda alterar a categoria de um dispositivo a partir da consola 'Gestor de Configuração'.

**Importante:** Esta capacidade funciona com o lançamento de junho de **2016** do Microsoft Intune. Certifique-se de que foi atualizado para esta libertação antes de experimentar estes procedimentos.

### <a name="try-it-out"></a>Experimente!

### <a name="create-a-set-of-device-categories"></a>Criar um conjunto de categorias de dispositivos
1.  No espaço de trabalho **de Ativos e Compliance** da consola De Configuração Manager, expanda a visão **geral**e, em seguida, clique em **Coleções de Dispositivos**.
2.  No separador **Home,** no grupo **Categorias,** clique em **Gerir categorias**de dispositivos .
3.  Na caixa de diálogo **'Gerir categorias de dispositivos',** pode criar, editar ou remover categorias. Tente criar uma nova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo
Quando associar uma coleção a uma categoria de dispositivo, todos os dispositivos da categoria que especificaserão serão adicionados a essa recolha.
1.  No diálogo **Properties** para uma recolha de dispositivos, clique em Adicionar Regra de Categoria**de Dispositivo de** **Regra** > .
2.  Na caixa de diálogo **"Create Device Category Membership Rule",** selecione a categoria que será aplicada a todos os dispositivos da recolha.
3.  Feche a caixa de diálogo de regras de **adesão à categoria de dispositivo supérrico** e a caixa de diálogo das propriedades de recolha.

### <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo
1.  No espaço de trabalho **de Ativos e Compliance** da consola De Configuração Manager, expanda a visão **geral**e, em seguida, clique em **Dispositivos**.
2.  Selecione um dispositivo na lista de **Dispositivos** e, em seguida, no separador **Home,** no grupo **Dispositivo,** clique na **categoria Change**.
3.  Na caixa de diálogo **da categoria editar** dispositivo, escolha a categoria a aplicar a este dispositivo e, em seguida, clique EM **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a>Período de carência de execução para implementações de aplicações e atualizações de software necessárias

Em alguns casos, poderá desejar aos utilizadores mais tempo para instalarem as implementações de aplicações necessárias ou atualizações de software para além de quaisquer prazos configurados. Isto pode normalmente ser necessário quando um computador foi desligado por um longo período de tempo e precisa de instalar um grande número de aplicações ou implementações de atualizações.
Por exemplo, se um utilizador final acaba de regressar de férias, poderá ter de esperar por muito tempo, uma vez que as implementações de aplicações em atraso são instaladas.
Para ajudar a resolver este problema, pode agora definir um período de carência de execução, implementando as definições do cliente do Gestor de Configuração para uma coleção.

### <a name="try-it-out"></a>Experimente!

Para configurar o período de graça, tome as seguintes ações:

1.  Na página do **Agente Informático** das definições do cliente, configure o novo período de graça da propriedade para aplicação após o prazo de **implementação (horas)** com um valor entre **1** e **120** horas.
2.  Numa nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, na página **de Agendamento,** selecione a execução do atraso da caixa de verificação **desta implementação**de acordo com as preferências do utilizador, até ao período de carência definido nas definições do cliente.
Todas as implementações que tenham esta caixa de verificação selecionada e que sejam direcionadas para dispositivos aos quais também implementou a definição do cliente utilizarão o período de carência de execução.

Se configurar um período de carência de execução e selecionar a caixa de verificação, uma vez atingido o prazo de instalação da aplicação, será instalado na primeira janela não-empresarial que o utilizador configuraaté esse período de carência. No entanto, o utilizador ainda pode abrir o Software Center e instalar a aplicação a qualquer momento que queira. Uma vez expirado o período de graça, a aplicação reverte para o comportamento normal para implementações em atraso.
Opções semelhantes foram adicionadas ao assistente de implementação de atualizações de software, assistente de regras de implementação automática e páginas de propriedades.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Utilizando o Gestor de Configuração como instalador gerido com o Dispositivo Guard

Device Guard é uma funcionalidade do Windows 10 que utiliza funcionalidades de hardware e software para controlar rigorosamente o que é permitido executar no dispositivo.

Pode ler uma visão detalhada do que a Guarda de Dispositivos faz e como funciona [neste artigo da Technet.](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview)

Nesta versão, o Gestor de Configuração pode interoperar com o Dispositivo Guard e [o Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) para que os ficheiros executáveis e DLL que são implementados com o Gestor de Configuração sejam automaticamente fidedignos, uma vez que provêm de um Instalador Gerido, o que significa que serão autorizados a funcionar no dispositivo-alvo e outros softwares não serão autorizados a funcionar a menos que sejam explicitamente autorizados a executar outras regras do AppLocker.  

Atualmente, esta capacidade não é configurável a partir da consola Do Gestor de Configuração. Para configurar a apólice requer que configure uma chave de registo em cada cliente e configure os serviços windows no cliente.
Uma vez feito isto, configure o ficheiro de política appLocker. Depois de configurar o ficheiro de política, pode implantá-lo em qualquer dispositivo cliente compatível.


Como todas as políticas do AppLocker, as políticas com regras de instalação geridas podem ser executadas em dois modos:

- Modo de auditoria – As aplicações são registadas impedidas de funcionar, mas quaisquer aplicações que teriam sido bloqueadas são reportadas num ficheiro de registo (isto será suportado numa versão posterior do 'Gestor de Configuração').
- Aplicações ativadas - As aplicações estão bloqueadas de funcionamento.

Mais informações sobre como usar o Dispositivo Guard com O Gestor de Configuração podem ser encontradas no [blog De Mobilidade e Segurança Empresarial.](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10)

Continuar a ler:

- [Introdução do Dispositivo Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Certificação e conformidade da Guarda de Dispositivos](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guia de implantação da Guarda de Dispositivos](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a>Vários pontos de gestão de dispositivos para a Gestão de Dispositivos Móveis no local  
  Com a Pré-visualização\-Técnica 1606, no local a Gestão de Dispositivos Móveis (MDM) suporta uma nova capacidade na Atualização de Aniversário do Windows 10 que configura automaticamente um dispositivo matriculado para ter mais de um ponto de gestão de dispositivos disponíveis para utilização. Esta capacidade permite que o dispositivo recue para outro ponto de gestão do dispositivo quando o que utiliza normalmente não está disponível. Esta capacidade funciona apenas para Computadores com a Atualização de Aniversário do Windows 10 instalada.  

### <a name="try-it-out"></a>Experimente!  

1.  Instale mais de um ponto de gestão de dispositivos na sua hierarquia.  

2.  Inscreva um dispositivo de atualização\-de aniversário do Windows 10 para gestão de dispositivos móveis no local.  

Para obter informações sobre como preparar o\-seu site e inscrever dispositivos para a Gestão de Dispositivos Móveis no local, consulte [Gerir dispositivos móveis com infraestrutura no local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Serviço de Procuração de Nuvem para gestão de clientes na Internet

O Cloud Proxy Service fornece uma forma simples de gerir os clientes do Gestor de Configuração na Internet. O serviço, que é implantado no Microsoft Azure e requer uma subscrição do Azure, conecta-se à sua infraestrutura de Configuração no local utilizando uma nova função chamada ponto de conector proxy cloud proxy. Uma vez completamente implantado e configurado, os clientes poderão aceder às funções do sistema de configuração do Site do Gestor de Configuração no local, independentemente de estarem ligados à rede privada interna ou à Internet.

Utiliza a consola Do Gestor de Configuração para implementar o serviço para o Azure, adicionar a função de ponto de ponto de conector de procuração de nuvem e configurar as funções do sistema do site para permitir o tráfego de proxy em nuvem. O Cloud Proxy Service atualmente apenas suporta as funções de ponto de gestão, ponto de distribuição e ponto de atualização de software.

Os certificados de cliente e os certificados Secure Socket Layer (SSL) são necessários para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço. Os computadores clientes normalmente recebem um certificado de cliente através da aplicação da política do grupo. Para encriptar o tráfego entre clientes e servidor de sistema de site que acolhe as funções, precisa de criar um certificado SSL personalizado a partir do CA. Além destes dois tipos de certificados, também precisa de configurar um certificado de gestão no Azure que permita ao Gestor de Configuração implementar o Serviço de Procuração de Nuvem.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos para serviço de procuração de nuvem em TP 1606
- Computadores clientes e o servidor do sistema do site executando o ponto de conector proxy da nuvem.
- Certificados SSL personalizados da CA interna - usados para encriptar comunicação dos computadores clientes e autenticar a identidade do Serviço de Procuração cloud.
- Assinatura Azure para serviços na nuvem.
- Certificado de gestão Azure - usado para autenticar O Gestor de Configuração com o Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitações do Serviço de Procuração de Nuvem em TP 1606

- Apenas suporta as funções de ponto de gestão, ponto de distribuição e ponto de atualização de software.
- As políticas dos utilizadores não são suportadas.
- Não pode ser utilizado com [a Gestão de Dispositivos Móveis no Local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no Gestor de Configuração.
- Apenas apoiado na plataforma pública de nuvem pública do Azure.


### <a name="try-it-out"></a>Experimente!

O processo de implementação do Serviço de Procuração de Nuvem inclui os seguintes passos:

1. Crie e emita um certificado SSL personalizado para o Serviço de Procuração de Nuvem.
1. Exportar a raiz do certificado de cliente.
2. Faça o upload do certificado de gestão para o Azure.
3. Configurar o Serviço de Procuração de Nuvem na consola do Gestor de Configuração.
4. Configure o site principal para utilizar a autenticação do certificado de cliente.
5. Adicione o ponto de conector proxy da nuvem ao seu site.
6. Configure as funções do sistema do site para aceitar o tráfego de procuração em nuvem.

As seguintes secções fornecem mais informações para completar estes passos.

#### <a name="create-a-custom-ssl-certificate"></a>Criar um certificado SSL personalizado

Pode criar um certificado SSL personalizado para o Serviço de Procuração de Nuvem da mesma forma que o faria para um ponto de distribuição baseado na nuvem. Siga as instruções para a implementação do Certificado de [Serviço para pontos de distribuição baseados na nuvem,](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) mas faça as seguintes coisas de forma diferente:

* Ao configurar o novo modelo de certificado, dê permissões **de Leitura** e **Inscrição** ao grupo de segurança que configura para servidores do Gestor de Configuração.

#### <a name="export-the-client-certificates-root"></a>Exportar a raiz do certificado de cliente

A forma mais fácil de exportar a raiz dos certificados de cliente utilizados na rede, é abrir um certificado de cliente numa das máquinas unidas ao domínio que tem um e copiá-lo.

>[!NOTE]
>Os certificados de cliente são necessários em qualquer computador que pretenda gerir com o Cloud Proxy Service e no servidor do sistema do site que acolhe o ponto de conector proxy da nuvem. Se precisar de adicionar um certificado de cliente a qualquer uma destas máquinas, consulte [a implementação do Certificado de Cliente para Computadores Windows](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. Na janela Run, digite **mmc** e prima Return.
2. No menu Ficheiro na consola de gestão, clique em **Adicionar/Remover snap-in...**.
3. Na caixa de diálogo Adicionar ou Remover Snap-ins, clicar em **Certificados,** clicar em **Adicionar >, **clicar na **conta de computador,** clicar **em Seguinte,** clicar em **Computador Local**e, em seguida, clicar em **Terminar**. Clique em **OK** para fechar a caixa de diálogo.
4. Ir a **Certificados > Certificados de > Pessoais.**
5. Clique duas vezes no certificado para autenticação do cliente no computador, clique no separador Caminho de Certificação e clique duas vezes na autoridade radicular (na parte superior do caminho).
6.  Clique no separador Detalhes e clique em **Copiar para Arquivar...**.
7. Complete o Assistente de Exportação do Certificado utilizando o formato de certificado predefinido. Tome nota do nome e localização do certificado de raiz que cria. Você precisará dele para configurar o Serviço de Procuração de Nuvem em um passo posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Faça upload do certificado de gestão para o Azure

É necessário um certificado de gestão Azure para o Gestor de Configuração aceder à API Azure e configurar o Serviço de Procuração de Nuvem. Para obter mais informações e instruções sobre como fazer o upload de um certificado de gestão, consulte os seguintes artigos na documentação do Azure:
- [Certificates overview for Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/) (Descrição geral dos certificados para os Serviços Cloud do Azure)
- [Faça upload de um Certificado de Gestão Azure Management API](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Certifique-se de copiar o ID de subscrição associado ao certificado de gestão. Vais precisar dele para configurar o Serviço proxy da Cloud na consola do Gestor de Configuração.

#### <a name="set-up-cloud-proxy-service"></a>Configurar o Serviço de Procuração de Nuvem

1. Na consola de Configuração Manager, vá à **Administração > Serviços cloud > serviço**de procuração em nuvem.
2. Clique em Criar serviço de **procuração de nuvem**.
3. No Create Cloud Proxy Service Wizard, introduza o id de subscrição azure (copiado do portal de gestão Azure), clique em Navegar e selecione o ficheiro de certificado que usou para carregar como certificado de gestão Azure. Clique em **Seguinte**. Aguarde alguns momentos para que a consola se ligue ao Azure.
4. Preencha os detalhes adicionais no assistente:
    - Especifique a chave privada (ficheiro.pfx) que exportou do certificado SSL personalizado.
    - Especifique o certificado de raiz exportado do certificado de cliente.
    - Especifique o mesmo nome de serviço FQDN que usou quando criou o novo modelo de certificado.
    - Limpe a caixa ao lado da Verificação da **Revogação** do Certificado de Cliente (a menos que publique publicamente as suas informações crl).
    - Clique em **Seguida** quando terminar.
5. Reveja as definições e clique **em Seguinte**. O Gestor de Configuração começa a configurar o serviço. Quando o assistente estiver concluído, pode clicar em **Close**, no entanto levará entre 5 a 15 minutos para fornecer o serviço completamente em Azure. Verifique a coluna **'Estado'** para o recém-configurado Serviço de Procuração de Nuvem para determinar quando o serviço está pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configure o site principal para autenticação de certificação do cliente

1. Na consola do Gestor de Configuração, vá à **Administração > Site de Configuração do Site**> Sites .
2. Selecione o site principal para os clientes que pretende gerir através do Serviço de Procuração de Nuvem e clique em **Propriedades**.
3. No separador Cliente Computer Comunicações da folha de propriedade do site principal, verifique a caixa ao lado do certificado de **cliente PKI (autenticação do cliente) quando disponível**.
4. Certifique-se de limpar a caixa ao lado dos Clientes, verifique a lista de **revogação do certificado (CRL) para os sistemas do site**. Esta opção só seria necessária se publicasse publicamente o seu CRL.
5. Clique em **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Adicione o ponto de conector proxy da nuvem

O ponto de conector proxy de nuvem é uma nova função do sistema de site para comunicar com o Serviço de Procuração de Nuvem. Para adicionar o ponto de conector proxy da nuvem, siga as instruções em Adicionar as funções do sistema do [site para Configuração Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configure funções para tráfego de procuração em nuvem

O passo final na criação do Serviço de Procuração de Nuvem é configurar as funções do sistema do site para aceitar o tráfego de procuração em nuvem. Para a Tech Preview 1606, apenas as funções de ponto de gestão, ponto de distribuição e ponto de atualização de software são suportadas para o Serviço de Procuração de Nuvem. Deve configurar cada função separadamente.

1. Na consola do Gestor de Configuração, vá à **Administração > Configuração do Site > Servidores e Funções**do Sistema do Site .
2. Clique no servidor do sistema do site para obter a função que pretende configurar para o tráfego de procuração em nuvem.
3. Clique na função e, em seguida, clique em **Propriedades**.
4. Na folha de propriedades, sob ligações com o cliente, escolha **HTTPS,** verifique a caixa ao lado de permitir o tráfego de Proxy de Proxy do Gestor de **Configuração,** e, em seguida, clique EM **OK**. Repita estes passos para as restantes funções.

#### <a name="check-status-on-a-client-on-the-internet"></a>Verifique o estado de um cliente na Internet

Depois de o serviço e as funções estarem completamente configurados, os clientes internos obterão a localização do Serviço de Procuração cloud no próximo pedido de localização. Os clientes com informações de localização atualizadas podem então comunicar com o Gestor de Configuração na Internet. O ciclo de votação para pedidos de localização é a cada 24 horas. Se não quiser esperar pelo pedido de localização normalmente programado, pode forçar o pedido reiniciando o serviço de hospedamento de agente SMS (ccmexec.exe) no computador.

Depois de os clientes terem as novas informações de localização para o Cloud Proxy Service, tente verificar o estado dos clientes que já não estão na rede privada interna, mas que têm acesso à Internet. Também pode monitorizar o tráfego no Serviço de Procuração de Nuvem, indo para **a Administração > Serviços**de Nuvem > Serviço de Procuração em Nuvem, selecionando o serviço no painel de listas e visualizando as informações de tráfego no painel de detalhes.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Gerir o agente de cliente do Office 365 no Configuration Manager  

Iniciando a Pré-visualização Técnica 1606, pode utilizar uma definição de agente de cliente do Gestor de Configuração, em vez da política de grupo, para permitir que os clientes do Office 365 recebam atualizações do Gestor de Configuração. Depois de configurar esta definição e implementar atualizações do Office 365, o agente cliente do Gestor de Configuração comunica com o agente cliente do Office 365 para descarregar as atualizações do Office 365 a partir de um ponto de distribuição e instalá-las. O Gestor de Configuração também faz o inventário da definição do agente cliente.

Para mais informações, consulte as atualizações do [Manage Office 365 ProPlus.](https://technet.microsoft.com/library/mt741983.aspx)

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Defina a definição de cliente do Gestor de Configuração para gerir o agente cliente do Office 365
1.  Na consola 'Gestor de Configuração', clique em**Configurar** > **As Definições**do Cliente de Visão Geral da **Administração** > .
2. Abra as definições apropriadas do dispositivo para ativar o agente cliente. Para obter mais informações sobre as definições de clientes padrão e personalizadas, consulte [como configurar as definições](../../core/clients/deploy/configure-client-settings.md)do cliente .
3. Clique em **Atualizações de Software** e selecione **Sim** para a gestão ativa da definição de Agente cliente do **Office 365.**  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>A variável da sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter determina se a sequência de tarefas utiliza ou não a letra de unidade capturada no ficheiro WIM de imagem do sistema operativo ao aplicar essa imagem a um computador de destino.
- Esta variável de sequência de tarefas foi depreciada na Pré-visualização Técnica 1606.

Durante uma implementação do sistema operativo, por padrão, o Windows Setup determina agora a melhor letra de acionamento a utilizar (tipicamente C:). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização na sequência de sequência de tarefas do Sistema Operativo Aplicar. Vá ao Select o local onde pretende aplicar esta definição do **sistema operativo,** selecione **a letra de unidade lógica específica**e escolha a unidade que pretende utilizar. Deve haver uma unidade atribuída com a carta que escolher no computador de destino. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Alterações do Nó Atualizações e Manutenção
Com a Pré-visualização Técnica 1606 foram introduzidas várias alterações que se aplicam a Atualizações e Manutenção na consola do Gestor de Configuração:
- **Mudança de nome do nó:**

    No espaço de trabalho **de monitorização,** o nó de estado de manutenção do **site** foi renomeado para **Atualizações e Estado de Manutenção**.
- **Mais estado de instalação:**

    Quando visualiza o estado de instalação da atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Download** (Isto aplica-se apenas ao site de topo onde a função do sistema de ponto de ligação de serviço está instalada)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, existem agora informações mais detalhadas para cada passo, incluindo no qual o ficheiro de registo pode ver para mais informações.  
-   **Nova opção para voltar a tentar falhas pré-requisitos:**

    Tanto nos espaços de trabalho da **Administração** como da **Monitorização,** as **Atualizações e** o nó de Manutenção incluem um novo botão na fita denominada **Ignorar avisos pré-requisitos**.

    Quando instala atualizações sem utilizar a opção de ignorar avisos pré-requisitos (a partir do Assistente de Atualizações), e essa instalação de atualização para com um aviso de Estado de **Prereq,** pode então selecionar **avisos de pré-requisito** da fita para desencadear uma continuação automática dessa instalação de atualização que ignora as advertências pré-requisitos.  



- **Visão mais limpa das atualizações:**

    Ao visualizar as **Atualizações e** o nó de Manutenção, vê agora apenas a atualização mais recente instalada e quaisquer novas atualizações que estejam disponíveis para instalar. Para visualizar atualizações previamente instaladas, clique no novo botão **Histórico** que aparece na Fita.  

-   **Opção renomeada para pré-produção:**

    No nó de Atualizações e Manutenção, o botão que foi nomeado **opções de Cliente** é agora renomeado para Promover o **Cliente de Pré-produção.**
