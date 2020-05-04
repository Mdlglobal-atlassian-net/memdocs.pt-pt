---
title: Instale o cliente com AD Azure
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do Gestor de Configuração em dispositivos Windows 10 utilizando o Diretório Ativo Azure para autenticação
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a55440e7ba61ec62d9f0c91c0a23b98bab5884c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713500"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalar e atribuir clientes do Gestor de Configuração do Windows 10 utilizando a AD Azure para autenticação

Para instalar o cliente do Gestor de Configuração em dispositivos Windows 10 utilizando a autenticação Azure AD, integre o Gestor de Configuração com o Diretório Ativo Azure (Azure AD). Os clientes podem estar na intranet comunicando diretamente com um ponto de gestão ativado por HTTPS ou qualquer ponto de gestão num site habilitado para O HTTP Melhorado. Também podem ser comunicadores baseados na Internet através da CMG ou com um ponto de gestão baseado na Internet. Este processo utiliza a AD Azure para autenticar clientes no site do Gestor de Configuração. A Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação do cliente.

A criação de Anúncios Azure pode ser mais fácil para alguns clientes do que criar uma infraestrutura de chave pública para autenticação baseada em certificados. Existem funcionalidades que o requerem a bordo do site para a Azure AD, mas não exigem necessariamente que os clientes sejam ad-joined Azure.<!-- SCCMDocs issue 1259 --> Para obter mais informações, veja os artigos seguintes:

- [Plano para O Diretório Ativo Azure](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Utilizar a AD Azure para cogestão](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Antes de começar

- Um inquilino da AD Azure é um pré-requisito  

- Requisitos do dispositivo:  

  - Windows 10  

  - Juntou-se ao Azure AD, quer em nuvem pura, ou híbrido Azure-joined  

- Requisitos do utilizador:  

  - O utilizador registado deve ser uma identidade Azure AD.

  - Se o utilizador tiver uma identidade federada ou sincronizada, deve utilizar a descoberta do [utilizador Ative Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) do Directory do Directory do Directory do Gestor de Configuração, bem como a descoberta do utilizador [Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). Para obter mais informações sobre identidades híbridas, consulte Definir uma estratégia híbrida de [adoção](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)de identidade.<!--497750-->  

- Além dos [pré-requisitos existentes](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) para a função do sistema de site de pontode gestão, também permitem **ASP.NET 4.5** neste servidor. Inclua quaisquer outras opções que sejam automaticamente selecionadas ao permitir ASP.NET 4.5.  

- Determine se o seu ponto de gestão precisa de HTTPS. Para mais informações, consulte O ponto de [gestão enable para HTTPS](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Opcionalmente, criou um portal de [gestão](../manage/cmg/plan-cloud-management-gateway.md) de nuvem (CMG) para implantar clientes baseados na Internet. Para clientes no local que autenticam com AD Azure, você não precisa de um CMG.  

> [!TIP]
> Começando na versão 2002,<!--5686290--> O Gestor de Configuração alarga o seu suporte a dispositivos baseados na Internet que muitas vezes não se ligam à rede interna, não conseguem aderir ao Azure Ative Directory (Azure AD), e não têm um método para instalar um certificado emitido pelo PKI. Para mais informações, consulte [a autenticação baseada em Token para CMG](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Configure Serviços Azure para Gestão de Nuvem

Ligue o site do gestor de configuração ao Azure AD como o primeiro passo. Para mais detalhes sobre este processo, consulte [os serviços da Configure Azure.](../../servers/deploy/configure/azure-services-wizard.md) Criar uma ligação ao serviço **de Gestão** de Nuvem.

Ativar a Descoberta do [Utilizador aD Azure](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) como parte do embarque na **Cloud Management**.

Depois de concluir estas ações, o site do Gestor de Configuração está ligado ao Azure AD.

## <a name="configure-client-settings"></a>Configurar definições do cliente

Estas definições de cliente ajudam a juntar dispositivos Windows 10 com AD Azure. Também permitem que os clientes baseados na Internet utilizem o CMG e o ponto de distribuição na nuvem.

1. Configure as seguintes definições de cliente na secção **Serviços cloud** utilizando as informações em [Como configurar as definições](configure-client-settings.md)do cliente .  

    - **Permitir o acesso ao ponto**de distribuição em nuvem : Ative esta definição para ajudar os dispositivos baseados na Internet a obter o conteúdo necessário para instalar o cliente Do Gestor de Configuração. Se o conteúdo não estiver disponível no ponto de distribuição da nuvem, os dispositivos podem recuperar o conteúdo do CMG. A instalação do cliente tenta novamente o ponto de distribuição da nuvem durante quatro horas antes de voltar ao CMG.<!--495533-->  

    - **Registe automaticamente novos dispositivos de domínio Windows 10 com Diretório Ativo Azure**: set to **Yes** or **No**. A definição predefinida é **Sim**. Este comportamento é também o padrão no Windows 10, versão 1709.

    - **Ativar os clientes para utilizar um portal**de gestão de nuvem : Definir para **Sim** (padrão), ou **Não**.  

2. Implemente as definições do cliente na recolha de dispositivos necessárias. Não implemente estas definições nas coleções dos utilizadores.

Para confirmar que o dispositivo está unido `dsregcmd.exe /status` ao Azure AD, corra num pedido de comando. O campo **AzureAdjoind** nos resultados mostra **SIM** se o dispositivo for azure ad-joined.

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instale e registe o cliente utilizando a identidade Azure AD

Para instalar manualmente o cliente utilizando a identidade Azure AD, primeiro reveja o processo geral sobre [como instalar os clientes manualmente](deploy-clients-to-windows-computers.md#BKMK_Manual).

 > [!Note]  
 > O dispositivo precisa de acesso à internet para contactar a Azure AD, mas não precisa de ser baseado na Internet.

O exemplo seguinte mostra a estrutura geral da linha de comando:`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Para mais informações, consulte as propriedades de [instalação do Cliente.](about-client-installation-properties.md)

O parâmetro **/mp** e a propriedade **CCMHOSTNAME** especificam um dos seguintes, dependendo do cenário:

- Ponto de gestão no local. Especifique apenas o parâmetro **/mp.** A propriedade **CCMHOSTNAME** não é necessária.
- Gateway de gestão da cloud
- Ponto de gestão baseado na Internet

A propriedade **SMSMP** especifica o ponto de gestão no local ou baseado na Internet.

Este exemplo usa um portal de gestão de nuvens. Substitui os valores da amostra:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

O site publica informações adicionais da Azure AD para o gateway de gestão de nuvem (CMG). Um cliente azure-joined ad obtém esta informação da CMG durante o processo ccmsetup, usando o mesmo inquilino ao qual se juntou. Este comportamento simplifica ainda a instalação do cliente num ambiente com mais de um inquilino da AD Azure. As duas únicas propriedades ccmsetup necessárias são **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

Para automatizar a instalação do cliente utilizando a identidade Azure AD via Microsoft Intune, consulte [como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## <a name="next-steps"></a>Passos seguintes

Uma vez concluído, pode continuar a [monitorizar e gerir os clientes.](../manage/monitor-clients.md)
