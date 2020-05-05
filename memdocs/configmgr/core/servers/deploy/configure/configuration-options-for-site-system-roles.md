---
title: Opções de roleta do sistema do site
titleSuffix: Configuration Manager
description: Consulte este artigo para mais informações sobre as funções do sistema do site do Gestor de Configuração que não são necessariamente autoexplicativas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721088"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opções de configuração para funções do sistema do site no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A maioria das opções de configuração para funções do sistema do Site Do Gestor de Configuração são autoexplicativas ou são explicadas nas caixas de assistente ou de diálogo quando as configurar. As seguintes secções explicam as funções do sistema do site cujas definições podem requerer informações adicionais.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a>Ponto de site do catálogo de aplicações  

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Para obter mais informações sobre como configurar o ponto de site do catálogo de aplicações, consulte plan para e configurar a gestão de [aplicações.](../../../../apps/plan-design/plan-for-and-configure-application-management.md)  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a>Ponto de serviço web de catálogo de aplicações  

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Para obter mais informações sobre como configurar o ponto de serviço web do Catálogo de Aplicações, consulte plan para e configurar a gestão de [aplicações.](../../../../apps/plan-design/plan-for-and-configure-application-management.md)  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a>Ponto de registo de certificado  

Para obter mais informações sobre como configurar o ponto de registo do certificado, consulte [introdução aos perfis de certificado](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a>Ponto de distribuição  

Para obter mais informações sobre como configurar o ponto de distribuição para a implementação de conteúdos, consulte Gerir a [infraestrutura](manage-content-and-content-infrastructure.md)de conteúdos e conteúdos.  

Para obter mais informações sobre como configurar o ponto de distribuição para implementações PXE, consulte [o Use PXE para implementar o Windows sobre a rede](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Para obter mais informações sobre como configurar o ponto de distribuição para implementações [multicast, consulte Utilizar o Multicast para implementar o Windows sobre a rede](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Instale e configure o IIS se necessário pelo Gestor de Configuração

Selecione esta opção para permitir instalar o Gestor de Configuração e configurar o IIS no sistema de site se ainda não estiver instalado. O IIS deve ser instalado em todos os pontos de distribuição e deve selecionar esta definição para continuar no assistente.  

### <a name="site-system-installation-account"></a>Conta de instalação do sistema do site

Para pontos de distribuição instalados num servidor de site, apenas a conta de computador do servidor do site é suportada para utilização como conta de instalação do sistema do site. Para mais informações, consulte [Contas](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a>Ponto de matrícula  

Os pontos de inscrição são utilizados para instalar computadores macOS e dispositivos de inscrição que gere com a gestão de dispositivos móveis no local. Para obter mais informações, veja os artigos seguintes:  

- [Como implementar clientes em Macs](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Como os utilizadores matriculam dispositivos com MDM no local](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Conexões permitidas

A definição HTTPS é automaticamente selecionada e requer um certificado PKI no servidor para autenticação do servidor ao ponto de procuração de inscrição e encriptação de dados sobre SSL. Para mais informações, consulte os requisitos do [certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Para um exemplo, a implementação do certificado do servidor e informações sobre como configurá-lo no IIS, consulte [a implementação do certificado de servidor web para sistemas de site que executam o IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a>Ponto de procuração de inscrição  

Para obter mais informações sobre como configurar um ponto de procuração de inscrição para dispositivos móveis, consulte [como os utilizadores matriculam dispositivos com MDM no local](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### <a name="client-connections"></a>Ligações de cliente

A definição HTTPS é automaticamente selecionada. Requer os seguintes certificados PKI no servidor:

- Para autenticação do servidor em dispositivos móveis e computadores Mac que você se inscreva com O Gestor de Configuração
- Para encriptação de dados sobre a camada de tomadas seguras (SSL)

Para obter mais informações sobre os requisitos do certificado, consulte [os requisitos do certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Para um exemplo, a implementação do certificado do servidor e informações sobre como configurá-lo no IIS, consulte [a implementação do certificado de servidor web para sistemas de site que executam o IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a>Ponto de estado de recuo  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Número de mensagens de Estado e intervalo de aceleração (em segundos)

As definições padrão para estas opções são 10.000 mensagens de estado e 3.600 segundos para o intervalo do acelerador. Embora estas configurações sejam suficientes para a maioria das circunstâncias, pode ter de as alterar quando ambas as condições são verdadeiras:  

- O ponto de estado de recuo aceita ligações apenas a partir da intranet.  

- Utiliza o ponto de estado de recuo durante o lançamento de uma implementação de clientes para muitos computadores.  

Neste cenário, um fluxo contínuo de mensagens estatais pode criar um atraso de mensagens estatais que causa uma alta utilização do processador no servidor do site por um período sustentado. Além disso, pode não ver informações atualizadas sobre a implementação do cliente na consola do Gestor de Configuração e nos relatórios de implementação do cliente.  

Estas definições de ponto de recuo foram concebidas para serem configuradas para mensagens estatais geradas durante a implementação do cliente. As configurações não são concebidas para serem configuradas para problemas de comunicação com clientes, como quando os clientes na internet não conseguem ligar-se ao seu ponto de gestão baseado na Internet. Como o ponto de estado de recuo não pode aplicar estas definições apenas às mensagens estatais que são geradas durante a implementação do cliente, não configura estas definições quando o ponto de estado de recuo aceita ligações a partir da internet.  

Cada computador que instala com sucesso o cliente do Gestor de Configuração envia as seguintes quatro mensagens de Estado para o ponto de estado de recuo:  

- Implantação de clientes iniciada  

- A implementação do cliente foi bem sucedida  

- Atribuição de clientes iniciada  

- Atribuição de clientes conseguiu  

Os computadores que não podem ser instalados ou que atribuem ao cliente do Gestor de Configuração enviam mensagens adicionais do Estado.  

Por exemplo, se implementar o cliente do Gestor de Configuração para 20.000 computadores, a implementação poderá enviar 80.000 mensagens de Estado para o ponto de estado de recuo. Uma vez que a configuração de estrangulamento padrão permite que 10.000 mensagens estatais sejam enviadas para o ponto de estado de recuo a cada 3.600 segundos (1 hora), as mensagens de Estado podem ficar bloqueadas no ponto de estado de recuo. Considere também a largura de banda de rede disponível entre o ponto de estado de retorno de retorno e o servidor do site e o poder de processamento do servidor do site para processar muitas mensagens de estado.  

Para ajudar a prevenir estas questões, considere um aumento no número de mensagens estatais e uma diminuição do intervalo do acelerador.  

Repor os valores do acelerador para o ponto de estado de recuo se uma das seguintes condições for verdadeira:  

- Calcula-se que os valores atuais do acelerador são superiores aos necessários para processar mensagens estatais a partir do ponto de estado de recuo.  

- Descobre que as definições atuais do acelerador criam uma utilização elevada do processador no servidor do site.  

Não altere as definições para as definições do acelerador do ponto de recuo a menos que compreenda as consequências. Por exemplo, quando aumenta as definições do acelerador para alta, o uso do processador no servidor do site pode aumentar para alto, o que atrasa todas as operações do site.  
