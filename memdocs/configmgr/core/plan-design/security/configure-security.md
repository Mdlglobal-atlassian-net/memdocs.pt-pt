---
title: Configurar a segurança
titleSuffix: Configuration Manager
description: Configure opções relacionadas com a segurança para O Gestor de Configuração.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718666"
---
# <a name="configure-security-in-configuration-manager"></a>Configurar a segurança no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para o ajudar a configurar opções relacionadas com a segurança para o Gestor de Configuração. Abrange as seguintes opções de segurança:
- [Comunicação de computador cliente](#BKMK_ConfigureClientPKI) para certificados PKI cliente  
- [Assinatura e encriptação](#BKMK_ConfigureSigningEncryption)  
- [Administração baseada em funções](#BKMK_ConfigureRBA)  
- [Gerir contas](#BKMK_ManageAccounts)  
- [Configurar o Azure Active Directory](#bkmk_azuread)  
- [Configure a autenticação do Fornecedor sms](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Configurar definições para certificados PKI de cliente  

Se pretender utilizar certificados da infraestrutura de chaves públicas (PKI) para ligações de cliente aos sistemas de sites que utilizam os Serviços de Informação Internet (IIS), utilize o seguinte procedimento para configurar as definições destes certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para configurar as definições de certificados PKI de cliente  

1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site principal para configurar.  

2.  Na fita, escolha **Propriedades**. Em seguida, mude para o separador comunicação do **computador cliente.**  

    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

3.  Selecione as definições para sistemas de site que utilizam o IIS.  

    - **Apenas HTTPS:** Os clientes que são atribuídos ao site usam sempre um certificado PKI cliente quando se conectam aos sistemas do site que utilizam o IIS.  

    - **HTTPS ou HTTP:** Não é necessário que os clientes utilizem certificados PKI.  

    - **Utilize os certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**: Para obter mais informações sobre esta definição, consulte [Http Melhorado](../hierarchy/enhanced-http.md).  

4.  Selecione as definições para computadores clientes.  

    - Utilize o **certificado PKI do cliente (capacidade de autenticação do cliente) quando estiver disponível**: Se escolher a definição do servidor do site **HTTPS ou HTTP,** escolha esta opção para utilizar um certificado PKI do cliente para ligações HTTP. O cliente utiliza este certificado em vez de um certificado autoassinado para se autenticar perante os sistemas de site. Se escolheu **apenas HTTPS,** esta opção é escolhida automaticamente.  

    Quando estiver disponível mais de um certificado de cliente PKI válido num cliente, escolha **Modificar** para configurar os métodos de seleção de certificados de cliente.  

    Para mais informações sobre o método de seleção de certificados de cliente, consulte [Planning for PKI client certificate selection](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - Os clientes verificam a lista de revogação de **certificados (CRL) para os sistemas do site**: Ative esta definição para os clientes verificarem o CRL da sua organização para obter certificados revogados.  

    Para mais informações sobre a verificação CRL para clientes, consulte [Planning for PKI certificate revocation](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Para importar, visualizar e eliminar os certificados para as autoridades de certificação de raiz fidedignas, escolha **set**.  

    Para mais informações, consulte [O Planeamento dos certificados de raiz fidedignos do PKI e a Lista de Emitentes](plan-for-security.md#BKMK_PlanningForRootCAs)de Certificados .  


Repita este procedimento para todos os sites primários da hierarquia.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a>Configure a assinatura e a encriptação  

Configure as definições de assinatura e encriptação mais seguras para os sistemas de site que todos os clientes do site possam suportar. Estas definições são especialmente importantes quando permitir que os clientes comuniquem com os sistemas de site utilizando certificados autoassinados através de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar a assinatura e encriptação para um site  

1.  Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site principal para configurar.  

2.  Na fita, selecione **Propriedades**e, em seguida, mude para o separador **De Assinatura e Encriptação.**  

    Este separador apenas está disponível num site primário. Se não vir o separador **De Assinatura e Encriptação,** certifique-se de que não está ligado a um site de administração central ou a um site secundário.  

3.  Configure as opções de assinatura e encriptação para os clientes comunicarem com o site.  

    - **Requer a assinatura**: Os clientes assinam dados antes de enviar para o ponto de gestão.  

    - **Require SHA-256**: Os clientes usam o algoritmo SHA-256 ao assinar dados.  

    > [!WARNING]  
    >  Não **exija SHA-256** sem primeiro confirmar que todos os clientes suportam este algoritmo de hash. Estes clientes incluem aqueles que podem ser atribuídos ao site no futuro.  
    >   
    >  Se escolher esta opção, e os clientes com certificados auto-assinados não podem suportar sha-256, O Gestor de Configuração rejeita-os. O componente SMS_MP_CONTROL_MANAGER regista o ID da mensagem 5443.  

    - **Utilizar encriptação**: Os clientes encriptam dados de inventário do cliente e mensagens de estado antes de enviar para o ponto de gestão. Usam o algoritmo 3DES.  

Repita este procedimento para todos os sites primários da hierarquia.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a>Configurar a administração baseada em funções  

A administração baseada em funções combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo de cada utilizador administrativo. Um âmbito inclui os objetos que um utilizador pode ver na consola, e as tarefas relacionadas com os objetos que têm permissão para fazer. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

Para mais informações, consulte a [configuração da administração baseada em papéis](../../servers/deploy/configure/configure-role-based-administration.md). Este artigo detalha as seguintes ações:  

- Criar funções de segurança personalizadas  

- Configurar funções de segurança  

- Configurar âmbitos de segurança para um objeto  

- Configurar coleções para gerir a segurança  

-  Criar um novo utilizador administrativo  

-  Modificar o âmbito administrativo de um utilizador administrativo  

> [!IMPORTANT]  
>  O seu próprio âmbito administrativo define os objetos e definições que pode atribuir ao configurar a administração baseada em funções para outro utilizador administrativo. Para obter informações sobre o planeamento da administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis.](../../understand/fundamentals-of-role-based-administration.md)  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a>Gerir contas que o Gestor de Configuração utiliza  

O Gestor de Configuração suporta as contas do Windows para muitas tarefas e utilizações diferentes. Para visualizar contas configuradas para diferentes tarefas e para gerir a palavra-passe que o Gestor de Configuração utiliza para cada conta, utilize o seguinte procedimento:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Para gerir contas que o Gestor de Configuração utiliza  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda **a Segurança**e, em seguida, escolha o nó **de Contas.**  

2.  Para alterar a palavra-passe para uma conta, selecione a conta na lista. Em seguida, escolha **propriedades** na fita.  

3.  Escolha **definir** para abrir a caixa de diálogo **da Conta de Utilizador do Windows.** Especifique a nova palavra-passe para o Gestor de Configuração utilizar para esta conta.  

    > [!NOTE]  
    >  A palavra-passe que especifica deve corresponder à palavra-passe desta conta no Diretório Ativo.  

Para mais informações, consulte [contas utilizadas no Gestor](../hierarchy/accounts.md)de Configuração .



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a>Configure Azure Ative Diretório

Integre o Gestor de Configuração com o Diretório Ativo Azure (Azure AD) para simplificar e ativar o seu ambiente. Ative o site e os clientes a autenticar usando a Azure AD. Para mais informações, consulte o serviço **de Gestão de Nuvem** nos [serviços Configure Azure.](../../servers/deploy/configure/azure-services-wizard.md)



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a>Configure a autenticação do Fornecedor sms

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. Para mais informações, consulte [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Consulte também

- [Plano de segurança](plan-for-security.md)  

- [Segurança e privacidade para clientes do Gestor de Configuração](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Comunicação entre pontos finais](../hierarchy/communications-between-endpoints.md)  

- [Referência técnica de controlos criptográficos](cryptographic-controls-technical-reference.md)  

- [Requisitos do certificado PKI](../network/pki-certificate-requirements.md)  
