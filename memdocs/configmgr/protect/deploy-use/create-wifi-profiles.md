---
title: Como criar perfis Wi-Fi
titleSuffix: Configuration Manager
description: Saiba como utilizar perfis Wi-Fi no Gestor de Configuração para implementar definições de rede sem fios para utilizadores da sua organização.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710770"
---
# <a name="create-wi-fi-profiles"></a>Criar perfis Wi-Fi

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize perfis Wi-Fi no Gestor de Configuração para implementar definições de rede sem fios para os utilizadores da sua organização. Ao implementar estas definições, facilita a ligação dos seus utilizadores ao Wi-Fi.  

Por exemplo, tem uma rede Wi-Fi a que pretende permitir que todos os portáteis do Windows se conectem. Crie um perfil Wi-Fi contendo as definições necessárias para ligar à rede sem fios. Em seguida, implemente o perfil para todos os utilizadores que tenham portáteis Windows na sua hierarquia. Os utilizadores destes dispositivos vêem a sua rede na lista de redes sem fios e podem facilmente ligar-se a esta rede.  

Pode configurar perfis Wi-Fi para as seguintes versões de SO:

- Windows 8.1 32-bit ou 64-bit

- Windows RT 8.1

- Windows 10 ou Windows 10 Mobile

Também pode utilizar o Configuração Manager para implementar definições de rede sem fios em dispositivos móveis utilizando a gestão de dispositivos móveis no local (MDM). Para obter informações mais gerais, consulte [o que está no local do MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Ao criar um perfil Wi-Fi, pode incluir um vasto leque de definições de segurança. Estas definições incluem certificados para validação do servidor e autenticação do cliente que foram empurrados usando perfis de certificado sinuoso do Gestor de Configuração. Para obter mais informações sobre perfis de certificados, consulte [os perfis](introduction-to-certificate-profiles.md)de certificado .

## <a name="create-a-wi-fi-profile"></a>Criar um perfil Wi-Fi

1. Na consola de Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade, expanda o Acesso aos Recursos da **Empresa**e selecione o nó de **Perfis Wi-Fi.**

1. No separador **Home,** no grupo **Criar,** escolha **Criar perfil Wi-Fi**.

1. Na página **geral** do Assistente de Perfil Wi-Fi Criar, especifique as seguintes informações:

    - **Nome**: Introduza um nome único para identificar o perfil na consola.

    - **Descrição**: Adicione opcionalmente uma descrição para fornecer mais informações para o perfil Wi-Fi.

    - **Importar um item de perfil Wi-Fi existente a partir de um ficheiro**: Selecione esta opção para utilizar as definições a partir de outro perfil Wi-Fi. Ao selecionar esta opção, as páginas restantes do assistente simplificam para duas páginas: **Import Wi-Fi Profile** e **Plataformas Suportadas**.

        > [!IMPORTANT]
        > Certifique-se de que o perfil Wi-Fi que importa contém XML válido para um perfil Wi-Fi. Quando importa o ficheiro, o Gestor de Configuração não valida o perfil.

    - **Severidade de incumprimento dos relatórios**: Escolha um dos seguintes níveis de gravidade que o dispositivo reporta se avaliar o perfil Wi-Fi como incompatível. Por exemplo, se a instalação do perfil falhar, não é compatível.

        - **Nenhum**: Os computadores que falham nesta regra de conformidade não reportam uma falha nos relatórios do Gestor de Configuração.

        - **Informações**

        - **Aviso**

        - **Crítica**

        - **Crítico com evento**: Os computadores que falham nesta regra de conformidade reportam uma falha de falha dos relatórios **críticos** para o Gestor de Configuração. Os dispositivos também registam o estado não conforme como um evento do Windows no registo de eventos da aplicação.

1. Na página de **Perfil Wi-Fi** do assistente, especifique as seguintes informações:

    - **Nome da rede**: Forneça o nome que os dispositivos apresentarão como nome de rede.

        > [!IMPORTANT]
        > O Gestor de Configuração não suporta`'`a utilização dos`,`caracteres apóstrofo () ou vírfos no nome da rede.

    - **SSID:** Especifique a identificação sensível a casos da rede sem fios.

    - **Ligar automaticamente quando esta rede estiver dentro do alcance**
    - **Procure outra rede sem fios enquanto está ligado a esta rede**
    - **Ligar quando a rede não estiver a difundir o respetivo nome (SSID)**

1. Na página de Configuração de **Segurança,** especifique as seguintes informações:

    > [!IMPORTANT]
    > Se estiver a criar um perfil Wi-Fi para [o MDM no local,](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)o atual ramo do Gestor de Configuração apenas suporta as seguintes configurações de segurança Wi-Fi:  
    >
    > - Tipos de segurança: **WPA2 Enterprise** ou **WPA2 Personal**  
    > - Tipos de encriptação: **AES** ou **TKIP**  
    > - Tipos de EAP: **Smart Card ou outro certificado** ou **PEAP**  

    - **Tipo de segurança:** Selecione o protocolo de segurança que a rede sem fios utiliza ou selecione **Nenhuma autenticação (Aberta)** se a rede não estiver segura.

    - **Encriptação**: Se o tipo de segurança o suportar, detete o método de encriptação para a rede sem fios.

    - **Tipo EAP**: Selecione o protocolo de autenticação para o método de encriptação selecionado.

        > [!NOTE]
        > Apenas para dispositivos Windows Phone: os tipos EAP **LEAP** e **EAP-FAST** não são suportados.

        **Selecione Configurar** para especificar as propriedades para o tipo EAP selecionado. Esta opção não está disponível para alguns tipos EAP selecionados.

        > [!IMPORTANT]
        > A janela de configuração do tipo EAP é do Windows. Certifique-se de que executa a consola 'Gestor de Configuração' num computador que suporta o tipo EAP selecionado.

    - **Lembre-se das credenciais de utilizador em cada início**de sessão : Selecione esta opção para armazenar credenciais de utilizador para que os utilizadores não tenham de introduzir credenciais de rede sem fios sempre que iniciarem sessão no Windows.

1. Na página **Definições Avançadas** do assistente, especifique definições adicionais para o perfil Wi-Fi. As configurações avançadas podem não estar disponíveis, ou podem variar, dependendo das opções que selecionar na página de **Configuração** de Segurança do assistente. Por exemplo, modo de autenticação ou opções de inscrição simples.

1. Na página **Definições proxy,** se a sua rede sem fios utilizar um servidor proxy, selecione a opção de **configurar as definições de proxy para este perfil Wi-Fi**. Em seguida, forneça as informações de configuração para o representante.

1. Na página **Plataformas Suportadas,** selecione as versões S onde este perfil Wi-Fi é aplicável.

1. Conclua o assistente.

## <a name="next-step"></a>Passo seguinte

> [!div class="nextstepaction"]
> [Como implementar perfis Wi-Fi](deploy-wifi-vpn-email-cert-profiles.md)
