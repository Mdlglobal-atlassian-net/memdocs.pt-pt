---
title: Prepare-se para enviar o cliente para Macs
titleSuffix: Configuration Manager
description: Tarefas de configuração antes de implantar o cliente do Gestor de Configuração para Macs.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d0968a61be4e450bb145b309f61de0d6c212549
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713997"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Prepare-se para implementar software de cliente para Macs

*Aplica-se a: Gestor de Configuração (ramo atual)*

Siga estes passos para se certificar de que está pronto para implementar o cliente do Gestor de [Configuração para computadores Mac](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Pré-requisitos mac

O pacote de instalação do cliente Mac não é fornecido com os meios de configuração do Gestor de Configuração. Baixe os **Clientes para sistemas operativos adicionais** a partir do [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184).  

Para a lista de versões suportadas, consulte [sistemas operativos suportados para clientes e dispositivos.](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)



## <a name="certificate-requirements"></a>Requisitos de certificados

A instalação e gestão do cliente para computadores Mac requer certificados de infraestrutura de chave pública (PKI). Os certificados PKI asseguram a comunicação entre os computadores Mac e o site do Gestor de Configuração utilizando a autenticação mútua e transferências de dados encriptadas. O Gestor de Configuração pode solicitar e instalar um certificado de cliente do utilizador. Utiliza Serviços de Certificado com uma autoridade de certificação empresarial, e o ponto de inscrição do Gestor de Configuração e ponto de procuração de inscrição. Também pode solicitar e instalar um certificado de computador independentemente do Gestor de Configuração. Este certificado deve satisfazer os requisitos do certificado do Gestor de Configuração.  

Os clientes do Gestor de Configuração Mac verificam sempre a revogação do certificado. Não pode desativar esta função.  

Se os clientes Mac não conseguirem localizar a lista de revogação do certificado (CRL), não podem ligar-se aos sistemas de site do Gestor de Configuração. Especialmente para os clientes Mac numa floresta diferente da autoridade de certificação emissora, verifique o seu design CRL. Certifique-se de que os clientes Mac podem localizar e descarregar um CRL.  

Antes de instalar o cliente do Gestor de Configuração num computador Mac, decida como instalar o certificado de cliente:  

-   Utilize a inscrição do Gestor de Configuração utilizando a [ferramenta CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). O processo de inscrição não suporta a renovação automática do certificado. Reinscreva os computadores Mac antes que o certificado expire.  

-   Utilize um método de [pedido de certificado e de instalação independente do Gestor de Configuração](deploy-clients-to-macs.md#bkmk_external).  

Para obter mais informações sobre os requisitos do certificado de cliente Mac, consulte [os requisitos de certificado PKI para O Gestor](../../plan-design/network/pki-certificate-requirements.md)de Configuração .  

Os clientes Mac são automaticamente atribuídos ao site do Gestor de Configuração que os gere. Os clientes Mac instalam-se como clientes apenas para a Internet, mesmo que a comunicação seja restrita à intranet. Esta configuração significa que comunicam com pontos de gestão e pontos de distribuição ativados pela Internet no seu site designado. Os computadores Mac não comunicam com os sistemas do site fora do local designado.  

> [!IMPORTANT]  
>  O cliente do Gestor de Configuração para o macOS não pode ser usado para se ligar a um ponto de gestão configurado para usar uma réplica de base de [dados](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar um certificado de servidor web para servidores do sistema de site  

Se estes sistemas de site não o tiverem, implemente um certificado de servidor web para os computadores que têm estas funções do sistema do site:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

O certificado do servidor web deve incluir o FQDN de internet especificado nas propriedades do sistema do site. O servidor não tem de ser acessível a partir da internet para suportar computadores Mac. Se não necessitar de gestão de clientes baseada na Internet, pode especificar o valor intranet FQDN para a Internet FQDN.  

Especifique o valor FQDN da internet do sistema do site no certificado do servidor web para o ponto de gestão, o ponto de distribuição e o ponto de procuração de inscrição.

Para obter mais informações sobre uma implementação de exemplo, consulte [a implementação do certificado de servidor web para sistemas de site que executam o IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar um certificado de autenticação de clientes para servidores do sistema de sites  

Se estes sistemas de sites não o tiverem, implemente um certificado de autenticação do cliente para os computadores que acolhem estas funções do sistema do site:  

-   Ponto de gestão  

-   Ponto de distribuição  

Por exemplo, implementação que cria e instala o certificado de cliente para pontos de gestão, consulte a [implementação do certificado de cliente para computadores Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Por exemplo, implementação que cria e instala o certificado de cliente para pontos de distribuição, consulte a [Implementação do certificado de cliente para pontos de distribuição](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Para implantar o cliente em dispositivos que executam o macOS Sierra, o nome do ponto de gestão deve ser configurado corretamente. Por exemplo, utilize o FQDN do servidor de pontos de gestão.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Prepare o modelo de certificado de cliente para Macs  

O modelo de certificado deve ter permissões **de leitura** e **inscrição** para a conta de utilizador que inscreveu o certificado no computador Mac.  

Para mais informações, consulte [a implementação do certificado de cliente para computadores Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configure o ponto de gestão e ponto de distribuição  

Configure pontos de gestão para as seguintes opções:  

-   HTTPS  

-   Permitir ligações ao cliente a partir da internet. Este valor de configuração é necessário para gerir computadores Mac. No entanto, isso não significa que os servidores do sistema do site devem estar acessíveis a partir da internet.  

-   Permitir que os dispositivos móveis e computadores Mac utilizem este ponto de gestão  

Os pontos de distribuição não são necessários para instalar o cliente para o Mac. Se pretender implementar software para estes computadores depois de instalar o cliente, configure pontos de distribuição para permitir ligações ao cliente a partir da internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gestão e pontos de distribuição para apoiar macs  

Antes de iniciar este procedimento, certifique-se de configurar o ponto de gestão e ponto de distribuição com um FQDN de internet. Se estes servidores não apoiarem a gestão do cliente baseado na Internet, especifique a intranet FQDN como o valor FQDN da internet.

As funções do sistema do site devem estar num local primário.  

1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione o nó de Funções de **Servidores e Derôs.** Em seguida, selecione o servidor que tem as funções certas do sistema do site.  

2.  No painel de detalhes, selecione a função **ponto de gestão** e selecione **Propriedades** na fita. Na janela **'Propriedades' ponto de gestão,** configure estas opções:  

    1.  Escolha **HTTPS**.  

    2.  Escolha Permitir ligações de **clientes apenas à Internet** ou permitir **ligações intranet e clientes**de internet . Estas opções requerem uma Internet ou intranet FQDN.  

    3.  Escolha **Permitir que dispositivos móveis e computadores Mac utilizem este ponto de gestão**.  

    4. Selecione **OK** para guardar esta configuração.  

3.  No painel de detalhes do nó de Funções do Servidor e do Sistema do Site, selecione a função ponto **de distribuição** e selecione **Propriedades** na fita. Na janela ponto **de distribuição Propriedades,** configure estas opções:  

    -   Escolha **HTTPS**.  

    -   Escolha Permitir ligações de **clientes apenas à Internet** ou permitir **ligações intranet e clientes**de internet . Estas opções requerem uma Internet ou intranet FQDN.  

    -   Escolha **o certificado de importação,** navegue no ficheiro de certificado de ponto de distribuição do cliente exportado e, em seguida, especifique a palavra-passe.  

4.  Repita este procedimento para todos os pontos de gestão e pontos de distribuição em sites primários que gerem computadores Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configure o ponto de procuração de inscrição e o ponto de inscrição  

Instale ambas as funções no mesmo site. Não é preciso instalá-los no mesmo servidor do sistema de sites, ou na mesma floresta de Diretório Ativo.  

Para obter mais informações sobre a colocação e considerações do sistema do site, consulte as funções do [sistema do Site.](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)  

Para adicionar as funções do sistema do site para suportar computadores Mac, consulte [instalar as funções](../../servers/deploy/configure/install-site-system-roles.md)do sistema do site .

Na página de **Seleção** de Funções do Sistema, selecione ponto de procuração de **inscrição** e ponto de **inscrição** da lista de funções disponíveis.  



## <a name="install-the-reporting-services-point"></a>Instale o ponto de serviços de reporte  

Para mais informações, consulte [Instale o ponto de serviços de reporte](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Passos seguintes

[Implementar o cliente do Gestor de Configuração para computadores Mac](deploy-clients-to-macs.md)  
