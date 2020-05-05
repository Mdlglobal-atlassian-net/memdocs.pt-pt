---
title: Noções básicas de segurança
titleSuffix: Configuration Manager
description: Conheça as camadas de segurança no Gestor de Configuração.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722838"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Fundamentos de segurança para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo resume os seguintes componentes de segurança fundamentais de qualquer ambiente do Gestor de Configuração:
- [Camadas de segurança](#bkmk_layers)
- [Administração baseada em funções](#bkmk_rba)
- [Proteger pontos finais de cliente](#bkmk_endpoints)
- [Contas e grupos do Configuration Manager](#bkmk_accounts)
- [Privacidade](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a>Camadas de segurança

A Segurança para O Gestor de Configuração consiste nas seguintes camadas: 
- [Windows OS e segurança da rede](#bkmk_layer-windows)
- [Infraestrutura de rede: firewalls, deteção de intrusões, infraestrutura de chave pública (PKI)](#bkmk_layer-network)
- [Controlos de segurança do Gestor de Configuração](#bkmk_layer-cm)
- [Fornecedor de SMS](#bkmk_layer-provider)
- [Permissões de base de dados do site](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a>Windows OS e segurança da rede
A primeira camada é fornecida por funcionalidades de segurança do Windows tanto para o SISTEMA como para a rede. Esta camada inclui os seguintes componentes:  

-   Partilha de ficheiros para transferir ficheiros entre componentes do Gestor de Configuração  

-   Listas de Controlo de Acesso (ACL) para ajudar a proteger ficheiros e chaves de registo  

-   Segurança do Protocolo de Internet (IPsec) para ajudar a garantir comunicações  

-   Política de grupo para definir política de segurança  

-   Permissões do Modelo de Objetos de Componentes Distribuídos (DCOM) para aplicações distribuídas, como a consola do Gestor de Configuração  

-   os Serviços de Domínio do Active Directory para armazenar as entidades de segurança  

-   Segurança da conta do Windows, incluindo alguns grupos que o Gestor de Configuração cria durante a configuração  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a>Infraestrutura de rede

Componentes de segurança adicionais, como firewalls e deteção de intrusões, ajudam a fornecer defesa para todo o ambiente. Os certificados emitidos pelas implementações de infraestruturas de chave pública padrão do setor (PKI) ajudam a fornecer autenticação, assinatura e encriptação.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a>Controlos de segurança do Gestor de Configuração

Além da segurança fornecida pelo servidor windows e pela infraestrutura de rede, o Gestor de Configuração controla o acesso à sua consola e recursos de várias formas. Por predefinição, apenas os administradores locais têm direitos sobre os ficheiros e as teclas de registo que a consola do Gestor de Configuração necessita nos computadores onde a instala.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a>Provedor de SMS

A próxima camada de segurança baseia-se no acesso através do WMI (Windows Management Instrumentation), nomeadamente o Fornecedor de SMS. O Fornecedor SMS é um componente do Gestor de Configuração que concede a um utilizador acesso à consulta da base de dados do site para obter informações. Por predefinição, o acesso ao fornecedor é restringido aos membros do grupo Admins de SMS . Este grupo contém inicialmente apenas o utilizador que instalou o Gestor de Configuração. Para conceder permissão a outras contas no repositório CIM (Common Information Model) e no fornecedor de SMS, adicione-as ao grupo de Administradores de SMS.  

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. <!--1357013-->  

Para mais informações, consulte [Plan for the SMS Provider](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a>Permissões de base de dados do site

A camada final de segurança baseia-se nas permissões para objetos da base de dados do site. Por predefinição, a conta do Sistema Local e a conta de utilizador que usou para instalar o Gestor de Configuração podem administrar todos os objetos na base de dados do site. Conceda e restrinja permissões a utilizadores administrativos adicionais na consola do Gestor de Configuração utilizando a administração baseada em papéis.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>Administração baseada em funções  

 O Gestor de Configuração utiliza uma administração baseada em papéis para ajudar a proteger objetos como coleções, implementações e sites. Este modelo de administração define e gere de forma centralizada as definições de acesso de segurança de toda a hierarquia para todos os sites e definições do site. 

 Um administrador atribui *funções de segurança* a utilizadores administrativos e permissões de grupo. As permissões estão ligadas a diferentes tipos de objetos do Gestor de Configuração, por exemplo, para criar ou alterar as definições do cliente. 

 Os âmbitos de segurança agrupam *casos específicos* de objetos que um utilizador administrativo é responsável por gerir, como uma aplicação que instala o Microsoft Office. 

 A combinação de funções de segurança, âmbitos de segurança e coleções define os objetos que um utilizador administrativo pode ver e gerir. O Gestor de Configuração instala algumas funções de segurança padrão para tarefas de gestão típicas. Crie as suas próprias funções de segurança para apoiar os seus requisitos de negócio específicos.  

 Para mais informações, consulte a [configuração da administração baseada em papéis](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a>Garantir pontos finais do cliente  

 O Gestor de Configuração assegura a comunicação do cliente às funções do sistema do site utilizando certificados auto-assinados ou PKI, ou fichas de Diretório Ativo Azure (Azure AD). Alguns cenários requerem a utilização de certificados PKI. Por exemplo, [a gestão de clientes baseada na Internet,](../clients/manage/plan-internet-based-client-management.md)e para clientes de [dispositivos móveis.](../../mdm/plan-design/plan-on-premises-mdm.md)  

 Pode configurar as funções do sistema do site às quais os clientes se conectam para a comunicação do cliente HTTPS ou HTTP. Os computadores clientes comunicam-se sempre utilizando o método mais seguro que está disponível. Os computadores clientes só recuam para usar o método de comunicação menos seguro se tiver funções de sistemas de site que permitem a comunicação HTTP.  

 Para mais informações, consulte [o Plano de Segurança.](../plan-design/security/plan-for-security.md)



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a>Contas e grupos do Gestor de Configuração  

 O Gestor de Configuração utiliza a conta do Sistema Local para a maioria das operações do site. Algumas tarefas de gestão podem exigir que crie e mantenha contas adicionais. O Gestor de Configuração cria vários grupos predefinidos e funções do Servidor SQL durante a configuração. Pode ter de adicionar manualmente contas de computador ou utilizador aos grupos predefinidos e às funções do Servidor SQL.  

 Para mais informações, consulte [contas utilizadas no Gestor](../plan-design/hierarchy/accounts.md)de Configuração .  



## <a name="privacy"></a><a name="bkmk_privacy"></a>Privacidade  

 Antes de implementar o Gestor de Configuração, considere os seus requisitos de privacidade. Embora os produtos de gestão empresarial ofereçam muitas vantagens porque podem gerir efetivamente muitos clientes, este software pode afetar a privacidade dos utilizadores na sua organização. O Gestor de Configuração inclui muitas ferramentas para recolher dados e monitorizar dispositivos. Algumas ferramentas podem levantar preocupações de privacidade na sua organização.  

 Por exemplo, quando instala o cliente Do Gestor de Configuração, permite muitas definições de gestão por padrão. Esta configuração faz com que o software do cliente envie informações para o site do Gestor de Configuração. O site armazena informações de clientes na base de dados do site. A informação do cliente não é enviada diretamente para a Microsoft. Para mais informações, consulte [Diagnósticos e dados de utilização](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Consulte também

- [Plano de segurança](../plan-design/security/plan-for-security.md)  

- [Segurança e privacidade para clientes do Gestor de Configuração](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar a segurança](../plan-design/security/configure-security.md)   

- [Comunicação entre pontos finais](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Referência técnica de controlos criptográficos](../plan-design/security/cryptographic-controls-technical-reference.md)  
