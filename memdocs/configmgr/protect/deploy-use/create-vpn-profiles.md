---
title: Como criar perfis VPN
titleSuffix: Configuration Manager
description: Saiba como criar perfis VPN no Gestor de Configuração.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713598"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Como criar perfis VPN em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração suporta vários tipos de ligação VPN. Para obter mais informações sobre os tipos de ligação disponíveis para as diferentes plataformas de dispositivos, consulte [os perfis VPN](vpn-profiles.md).

Para ligações VPN de terceiros, distribua a aplicação VPN antes de implementar o perfil VPN. Se não implementar a aplicação, os utilizadores serão solicitados a fazê-lo quando tentarem ligar-se à VPN. Para mais informações, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Criar um perfil da VPN

1. Na consola de Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade, expanda o Acesso aos Recursos da **Empresa**e selecione o nó de **Perfis VPN.**

1. No separador **Home** da fita, no grupo **Criar,** escolha **Criar perfil VPN**.

1. Na página **geral** do Assistente de Perfil VPN Create VPN, especifique as seguintes informações:

    - **Nome**: Introduza um nome único para identificar o perfil VPN na consola.

        > [!NOTE]
        > Não utilize os seguintes caracteres no nome `\/:*?<>|; `do perfil VPN: . O perfil VPN do Windows não suporta estes caracteres especiais.

    - **Descrição**: Introduza opcionalmente uma descrição para fornecer mais informações sobre o perfil VPN.

    - **Tipo de perfil VPN**: Selecione a plataforma apropriada.

        Se selecionar a plataforma **Windows 8.1,** também pode **importar a partir de ficheiros**. Esta ação importa informações de perfil VPN de um ficheiro XML. Se selecionar esta opção, o resto do assistente simplifica para as seguintes páginas: **Plataformas Suportadas** e **Perfil VPN de Importação**.

1. Na página **Plataformas Suportadas,** selecione as versões OS que este perfil VPN suporta.

1. Na página **Ligação,** especifique as seguintes informações:

    - Tipo de **ligação:** Escolha o tipo de ligação VPN. Para obter mais informações sobre os tipos suportados, consulte [os perfis VPN](vpn-profiles.md).

    - **Lista do servidor**: Adicione um novo servidor para utilizar para a ligação VPN. Dependendo do tipo de ligação, pode adicionar um ou mais servidores VPN e especificar qual o servidor que é o padrão.

    - Contornar a **VPN quando ligado à rede da empresa**: Configure os clientes para não utilizarem a VPN quando estiverem na sua rede interna. Se necessário, especifique um nome DNS específico da ligação.

1. Na página método de **autenticação** do assistente, escolha um método suportado pelo tipo de ligação. As definições e opções disponíveis nesta página variam consoante o tipo de ligação selecionado. Para mais informações, consulte a referência do [método de autenticação.](#bkmk_auth)

1. Na página **Definições proxy,** se o seu VPN utilizar um servidor proxy, selecione uma das opções conforme apropriado para o seu ambiente. Em seguida, forneça as informações de configuração para o representante.

1. A página **Aplicações** aplica-se apenas aos perfis do Windows 10. Adicione aplicativos de ambiente de trabalho e universais que se ligam automaticamente a esta VPN. O tipo de aplicação determina o identificador da aplicação:

    - Para uma aplicação de ambiente de *trabalho,* forneça o caminho de ficheiro da aplicação.

    - Para uma *aplicação universal,* forneça o nome da família do pacote (PFN). Para aprender a encontrar o PFN para uma aplicação, consulte [Encontrar um pacote de nome de família para VPN por app](find-a-pfn-for-per-app-vpn.md).

    Também pode configurar uma opção para que **apenas as aplicações listadas possam utilizar este VPN**.

    > [!IMPORTANT]
    > Proteja todas as listas de aplicações associadas que compila para configurar uma VPN por app. Se um utilizador não autorizado alterar a sua lista e a importar para a lista de aplicações VPN por aplicação, pode autorizar o acesso vpN a apps que não deveriam ter acesso.

1. A página **Limites** aplica-se apenas aos perfis do Windows 10 para configurar os limites VPN. Pode adicionar as seguintes opções:

    - **Regras de tráfego**de rede : Definir os protocolos, porto local, porta remota e intervalos de endereços para permitir a ligação VPN.  

        > [!Note]
        > Se não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços estão ativados. Depois de criar uma regra, apenas os protocolos, portas e endereços que especifica nessa regra ou em regras adicionais são utilizados pela ligação VPN.

    - **Nomes e servidores DNS**: Servidores DNS que são utilizados pela ligação VPN após o dispositivo estabelecer a ligação.

    - **Rotas**: Rotas de rede que utilizam a ligação VPN. A criação de mais de 60 rotas pode fazer com que a política falhe.

1. Conclua o assistente.

O novo perfil VPN é apresentado no nó **Perfis VPN** da área de trabalho **Ativos e Compatibilidade** .

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Referência do método de autenticação

Os métodos de autenticação VPN disponíveis dependem do tipo de ligação:

### <a name="certificates"></a>Certificados

Se o certificado de cliente autenticar num servidor RADIUS, como um Servidor de Política de Rede, detete o Nome Alternativo sujeito no certificado para o Nome Principal do Utilizador.

Tipos de ligação suportados:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN Móvel do Ponto de Verificação

### <a name="username-and-password"></a>Utilizername e Password

Tipos de ligação suportados:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN Móvel do Ponto de Verificação

### <a name="microsoft-eap-ttls"></a>EAP-TTLS Microsoft

Tipos de ligação suportados:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft protegido EAP (PEAP

Tipos de ligação suportados:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Palavra-passe com segurança Microsoft (EAP-MSCHAP v2)

Tipos de ligação suportados:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Smart Card ou outro certificado

Tipos de ligação suportados:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Tipos de ligação suportados:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Utilizar certificados do computador

Tipos de ligação suportados:

- IKEv2

### <a name="additional-authentication-options"></a>Opções adicionais de autenticação

Quando a versão cliente do Windows a suporta, está disponível a opção de **configurar** o método de autenticação. Esta opção abre a janela de propriedades do Windows para configurar o método de autenticação.

Dependendo das opções selecionadas, pode ser-lhe pedido que especifique mais informações, por exemplo:

- **Lembre-se das credenciais de utilizador em cada início**de sessão : As credenciais do utilizador são lembradas para que os utilizadores não tenham de as introduzir sempre que se conectam.  

- **Selecione um certificado**de cliente para autenticação do cliente : Selecione um perfil de certificado SCEP de cliente previamente criado para autenticar a ligação VPN. Para mais informações, consulte Criar perfis de [certificadoS PFX](create-certificate-profiles.md).

## <a name="next-steps"></a>Passos seguintes

- Para ligações VPN de terceiros, distribua a aplicação VPN antes de implementar o perfil VPN. Se não implementar a aplicação, os utilizadores serão solicitados a fazê-lo quando tentarem ligar-se à VPN. Para mais informações, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).

- Implante o perfil VPN. Para mais informações, consulte [Como implementar perfis](deploy-wifi-vpn-email-cert-profiles.md).
