---
title: Plano de gestão de aplicações
titleSuffix: Configuration Manager
description: Implementar e configurar as dependências necessárias para a implementação de aplicações no Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709944"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Plano para e configurar gestão de aplicações em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para ajudá-lo a implementar as dependências necessárias para implementar aplicações no Gestor de Configuração.  



## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  


### <a name="internet-information-services-iis"></a>Serviços de Informação de Internet (IIS)

O IIS é necessário nos servidores que executam as seguintes funções do sistema do site:

- Ponto de gestão  
- Ponto de distribuição  

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> O catálogo de aplicações também requer IIS. No entanto, a sua experiência de utilizador Silverlight não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificados relativos a pedidos assinados por código para dispositivos móveis

Quando assinar códigos de aplicações para as implementar em dispositivos móveis, não utilize um certificado que tenha sido gerado utilizando um modelo versão 3 **(Windows Server 2008, Enterprise Edition).** Este modelo de certificado cria um certificado incompatível com aplicações do Gestor de Configuração para dispositivos móveis.

Se utilizar serviços de certificadode diretório ativo para assinar aplicações de código para aplicações de dispositivos móveis, não utilize um modelo de certificado versão 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditar eventos de inscrição para afinidade do dispositivo de utilizador  

Se pretender criar automaticamente afinidades de dispositivos de utilizador, configure os clientes para auditar eventos de login.

Para determinar as afinidades automáticas do dispositivo do utilizador, o cliente do Gestor de Configuração lê eventos de log de tipo **Sucesso** a partir do registo de eventos de segurança do Windows. Ativar estes eventos com as seguintes duas políticas de auditoria:

- **Auditar eventos de início de sessão de conta**
- **Auditar eventos de início de sessão**

Para criar automaticamente relações entre utilizadores e dispositivos, certifique-se de que estas duas definições estão ativadas nos computadores cliente. Pode utilizar a Política de Grupo do Windows para configurar estas definições.

Para obter mais informações sobre a finidade do dispositivo do utilizador, consulte [os utilizadores e dispositivos do Link com a finidade](../deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .  



## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager


### <a name="management-point"></a>Ponto de gestão

Os clientes contactam um ponto de gestão para descarregar a política do cliente, para localizar conteúdos.

A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador.

Na versão 1902 e anterior, os clientes usam o ponto de gestão para se conectarem ao catálogo de aplicações. Se os clientes não conseguem aceder a um ponto de gestão, não podem usar o catálogo de aplicações.

> [!Note]  
> A partir da versão 1806, as funções de catálogo de aplicações deixaram de ser necessárias para exibir aplicações disponíveis pelo utilizador no Software Center. Para mais informações, consulte [Configure Software Center](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> A partir da versão 1906, não é possível instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
  

### <a name="distribution-point"></a>Ponto de distribuição

Antes de poder implementar aplicações para clientes, precisa de pelo menos um ponto de distribuição na hierarquia. Por predefinição, durante uma instalação padrão, o servidor do site tem uma função de site do ponto de distribuição ativada. O número e a localização dos pontos de distribuição variam de acordo com os requisitos específicos do seu ambiente.

Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdos, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  


### <a name="reporting-services-point"></a>Ponto do Reporting Services

Para utilizar os relatórios no Configurmanager para gestão de aplicações, instale primeiro e configure um ponto de serviços de reporte.

Para mais informações, consulte [Introdução a relatórios.](../../core/servers/manage/introduction-to-reporting.md)  


### <a name="client-settings"></a>Definições do cliente

Muitas configurações do cliente controlam a forma como o cliente instala aplicações e a experiência do utilizador no dispositivo. Estas definições de cliente incluem os seguintes grupos:

- Agente informático  
- Reiniciar computador  
- Centro de Software  
- Implementação de software  
- Afinidade do utilizador e do dispositivo  

Para obter mais informações, veja os artigos seguintes:

- [Acerca das definições de cliente](../../core/clients/deploy/about-client-settings.md)  
- [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Permissões de segurança para gestão de aplicações

- A função de segurança do Autor da **Aplicação** inclui as permissões necessárias para criar, alterar e reformar candidaturas.  

- A função de segurança do Gestor de Implementação de **Aplicações** inclui permissões necessárias para implementar aplicações.  

- A função de segurança do Administrador de **Aplicação** tem todas as permissões tanto do Autor da **Aplicação** como das funções de segurança do Gestor de Implementação de **Aplicações.**  

Para mais informações, consulte a [configuração da administração baseada em papéis](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Cliente de App-V 4.6 SP1 ou posterior para executar aplicações virtuais

Para criar aplicações virtuais no Gestor de Configuração, instale o App-V 4.6 SP1 ou posteriormente nos dispositivos.

Antes de implementar aplicações virtuais, também atualize o cliente App-V com o hotfix descrito no artigo de Suporte da [Microsoft 2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Catálogo de aplicações

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910.. Para mais informações, consulte [Remova o catálogo de aplicações](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Ponto de serviço web de catálogo de aplicações

O ponto de serviço web do catálogo de aplicações é uma função do sistema de site que fornece informações sobre software disponível desde a sua biblioteca de software para o site do catálogo de aplicações a que os utilizadores acedem.

Para obter mais informações sobre como configurar a função do sistema do site, consulte [Instalar e configurar o Catálogo de Aplicações](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Ponto de site do catálogo de aplicações

O ponto do site do catálogo de aplicações é uma função do sistema de site que fornece aos utilizadores uma lista de software disponível.

Para obter mais informações sobre como configurar a função do sistema do site, consulte [Instalar e configurar o Catálogo de Aplicações](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Contas de utilizador descobertas para catálogo de aplicações

O Gestor de Configuração deve primeiro descobrir as contas dos utilizadores antes que os utilizadores possam visualizar e solicitar aplicações do catálogo da aplicação. Para mais informações, consulte [a Descoberta de Run.](../../core/servers/deploy/configure/run-discovery.md)  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Configure Software Center  

Para obter mais informações sobre configuração e branding Software Center, consulte [Plan for Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a>Remova o catálogo de aplicações

<!-- SCCMDocs-pr issue 3051 -->

O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [funcionalidades removidas e depreciadas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). A lista seguinte resume as alterações:

- A partir da versão 1806, a experiência do **utilizador Silverlight** para o ponto de site do catálogo de aplicações já não é suportada.<!--1358309--> A função de ponto de serviço web do catálogo de aplicações já não é *necessária,* mas continua *a ser suportada.*

- A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações.

- O suporte termina para as funções de catálogo de aplicações com a versão 1910.  

Estas melhorias iterativas para o Software Center e o ponto de gestão são para simplificar a sua infraestrutura e remover a necessidade do catálogo de aplicações para implementações disponíveis pelo utilizador. O Software Center pode fornecer todas as implementações de aplicações sem o catálogo de aplicações. Além disso, se ativar o TLS 1.2 e utilizar o HTTP com o catálogo de aplicações, os utilizadores não podem ver as implementações disponíveis e direcionadas ao utilizador. Update Configuration Manager para a versão 1906 ou mais tarde para beneficiar destas melhorias.

1. Atualize todos os clientes para a versão 1806 ou mais tarde. A versão 1906 é recomendada.  

1. Deset branding para Software Center, em vez de nas propriedades da função do site do catálogo de aplicações. Para mais informações, consulte [as definições do cliente do Software Center](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Reveja as definições padrão e de cliente personalizado. No grupo **de Agente informático,** certifique-se `(none)`de que o ponto de site do Catálogo de **Aplicações Padrão** é .  

    Na versão 1902 e anterior, o cliente apenas muda para usar o ponto de gestão quando não há funções de catálogo de aplicações na hierarquia. Caso contrário, os clientes continuam a utilizar uma das instâncias do catálogo de aplicações na hierarquia. Este comportamento aplica-se em locais primários separados.  

1. Remova o site do catálogo de **aplicações** e as funções do site do site do catálogo de **aplicações** de todos os sites primários.

Depois de remover as funções de catálogo de aplicações, o Software Center começa a utilizar o ponto de gestão para implementações disponíveis e orientadas para o utilizador. Na versão 1902 e anterior, pode levar até 65 minutos para que esta mudança aconteça. Para verificar este comportamento num cliente `SCClient_<username>.log`específico, reveja a entrada semelhante à seguinte linha:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a>Instalar e configurar o catálogo de aplicações  

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Passo 1: Certificado de servidor web para HTTPS

Se utilizar as ligações HTTPS, implemente um certificado de servidor web para os servidores do sistema do site para o ponto de página do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações.

Se pretender que os clientes utilizem o catálogo de aplicações a partir da internet, implemente um certificado de servidor web para pelo menos um ponto de gestão. Configure-o para ligações de clientes a partir da internet.

Para obter mais informações sobre os requisitos do certificado, consulte [os requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Passo 2: Certificado de autenticação do cliente para HTTPS

Se utilizar um certificado PKI cliente para ligações a pontos de gestão, implemente um certificado de autenticação de clientes para computadores clientes. Embora os clientes não utilizem um certificado PKI cliente para se conectarem ao catálogo de aplicações, devem ligar-se a um ponto de gestão antes de poderem utilizar o catálogo de aplicações.

Implementar um certificado de autenticação de clientes para computadores clientes nos seguintes cenários:

- Todos os pontos de gestão na intranet aceitam apenas ligações de clientes HTTPS.
- Os clientes ligam-se ao catálogo de aplicações a partir da internet.

Para obter mais informações sobre os requisitos do certificado, consulte [os requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Passo 3: Instalar e configurar as funções do catálogo da aplicação

Instale tanto o ponto de serviço web do catálogo de aplicações como as funções do site do catálogo de aplicações no mesmo site. Não é preciso instalá-los no mesmo servidor ou na mesma floresta de DirectórioActivo. No entanto, o ponto de serviço web do catálogo de aplicações deve estar na mesma floresta que a base de dados do site.

Para obter mais informações sobre a colocação do servidor, consulte Plan para servidores do [sistema do site e funções](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)do sistema do site .

> [!NOTE]  
> Instale o catálogo de aplicações num local primário. Não pode instalá-lo num local secundário ou no site da administração central.  

Instale o catálogo de aplicações num novo servidor de sistema de site ou num servidor existente no site. Para obter mais informações sobre o procedimento geral, consulte [instalar as funções](../../core/servers/deploy/configure/install-site-system-roles.md)do sistema do site . No assistente para adicionar uma função de sistema de site ou criar um servidor de sistema de site, selecione as seguintes funções da lista:  

- **Ponto de serviço web de catálogo de aplicações**  
- **Ponto de site do catálogo de aplicações**  

> [!TIP]  
> Se pretender que os computadores clientes utilizem o catálogo de aplicações através da internet, especifique o nome de domínio totalmente qualificado (FQDN).  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verifique a instalação destas funções do sistema do site  

- Mensagens de estado: utilize os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, o status ID **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que o Gestor de Componentes do Site instalou com sucesso o ponto do site do catálogo da aplicação.  

- Ficheiros de registo: procure **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Para mais informações, procure os **ficheiros awebsvcMSI.log** e **portlwebMSI.log.**  


### <a name="step-4-configure-client-settings"></a>Passo 4: Configurar as definições do cliente

Se pretender que todos os utilizadores tenham as mesmas definições, configure as definições padrão do cliente. Caso contrário, configure definições do cliente personalizadas para coleções específicas.

Para obter mais informações, veja os artigos seguintes:

- [Acerca das definições de cliente](../../core/clients/deploy/about-client-settings.md)  
    - Agente informático  
    - Reiniciar computador  
    - Centro de Software  
    - Implementação de software  
    - Afinidade do utilizador e do dispositivo  
- [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)  

O cliente do Gestor de Configuração configura dispositivos com estas definições quando descarregue a política do cliente. Para desencadear a recuperação de políticas para um único cliente, consulte [como gerir os clientes.](../../core/clients/manage/manage-clients.md)


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passo 5: Verificar se o catálogo de aplicações está operacional

Utilize os seguintes procedimentos para verificar se o catálogo de aplicações está operacional.

> [!NOTE]  
> A experiência do utilizador do catálogo de aplicações requer o Microsoft Silverlight. Se utilizar o catálogo de aplicações diretamente a partir de um browser, verifique primeiro se o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
> Os pré-requisitos em falta estão entre as razões mais típicas para que o catálogo de aplicações funcione incorretamente após a instalação. Confirme os pré-requisitos para as funções do sistema do catálogo de aplicações. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

Num browser, insira o endereço do site do catálogo de aplicações. Confirme que a página web mostra os três separadores: Catálogo de **Aplicações,** Meus Pedidos de **Aplicação**e **Meus Dispositivos**.  

Utilize o endereço adequado para o catálogo `<server>` de aplicações a partir da seguinte lista, onde está o nome do computador, a intranet FQDN ou a Internet FQDN:  

- Conexões de clientes HTTPS e definições de funções de sistema de site padrão:`https://<server>/CMApplicationCatalog`  

- Ligações ao cliente HTTP e definições de funções de sistema de site padrão:`http://<server>/CMApplicationCatalog`  

- Conexões de clientes HTTPS e definições de funções de sistema de site personalizado:`https://<server>:<port>/<web application name>`  

- Conexões de clientes HTTP e definições de funções de sistema de site personalizado:`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Se inscreveu no dispositivo com uma conta de Administrador de Domínio, o cliente do Gestor de Configuração não exibe mensagens de notificação. Por exemplo, mensagens que indicam que está disponível um novo software.  
