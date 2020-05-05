---
title: Configurar a inscrição para o MDM no local
titleSuffix: Configuration Manager
description: Conceda aos utilizadores permissão para inscreverem os seus dispositivos para a gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721844"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Configurar a inscrição do dispositivo para o MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O passo final para a criação de dispositivos móveis no local (MDM) é permitir que os utilizadores matriculem os seus dispositivos. Utilize as definições do cliente do Gestor de Configuração para conceder aos utilizadores permissão para inscrever dispositivos no MDM no local.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a>Criar um perfil de inscrição

Para pressionar as definições necessárias para permitir que os utilizadores matriculem dispositivos móveis, adicione um novo perfil de inscrição às definições padrão do cliente. Este perfil aplica-se então a todos os utilizadores no site do Gestor de Configuração.

> [!NOTE]
> Este processo utiliza as Definições padrão **do cliente,** que se aplicarão automaticamente a todos os dispositivos e utilizadores. Em alternativa, pode criar configurações personalizadas do cliente e, em seguida, implementar para coleções à sua escolha. Este método alternativo requer pelo menos duas definições personalizadas do cliente, uma para as definições do *dispositivo* e outra para as definições *do utilizador.* Para mais informações, consulte [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md).

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Definições do **Cliente.** Abra **as Definições do Cliente Predefinido** e selecione o grupo **de inscrição.**

1. Em definições do dispositivo, especifique o **intervalo de votação para dispositivos modernos (minutos)**. Por defeito, este intervalo é de 60 minutos.

1. Em definições do utilizador, ative a opção de **permitir que os utilizadores matriculem dispositivos modernos**.

1. Para o perfil de inscrição do **dispositivo moderno,** selecione **set Profile**. Na janela perfil de inscrição, selecione **Criar**.

1. Na janela Criar perfil de inscrição, especifique as seguintes informações:

    - Um **nome** único e descritivo para o perfil de inscrição.

    - Uma **Descrição** opcional para fornecer informações adicionais sobre o perfil.

    - Escolha o código do **site de gestão** que contenha o ponto de gestão do dispositivo. Selecione **OK** para guardar e fechar.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Configurar as definições adicionais do cliente

Existem configurações adicionais do cliente para configurar os dispositivos depois de se matricularem. Para obter informações mais gerais, consulte [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md).

O Gestor de Configuração suporta as seguintes definições de cliente para o MDM no local:

- **Política**do cliente : Estas configurações especificam a frequência para descarregar a política do cliente para o dispositivo. Também pode ativar as definições para a política do utilizador. Para mais informações, consulte [sobre as definições do cliente - Política de Cliente](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Implementação do software**: Detete o intervalo para avaliar as implementações de software. Para mais informações, consulte [sobre as definições do cliente - Implementação de Software](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > Para o MDM no local, as definições de implementação de software só podem ser utilizadas como definições padrão do cliente.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Descubra os utilizadores

Para que os utilizadores recebam as definições do cliente com o perfil de inscrição para o MDM no local, o site descobre a sua conta de utilizador em Diretório Ativo. Para assegurar que todas as pessoas que necessitam do perfil de inscrição o obtêm, execute a deteção de utilizadores do Active Directory. Para mais informações, consulte Ative [Directory User Discovery](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Instale o certificado de raiz de confiança

Os dispositivos unidos pelo domínio obtêm o certificado de raiz fidedigna para comunicação fidedigna com os servidores que hospedam as funções do sistema do site. Os Serviços de Certificado de Diretório Ativo distribuem automaticamente o certificado raiz fidedigno. Computadores e dispositivos móveis não-domínio precisam deste certificado instalado através de outros meios para permitir a inscrição.

> [!NOTE]
> Se os certificados de servidor web forem emitidos por uma autoridade de certificados públicos, a maioria dos dispositivos já confiava nestes CAs. Se o seu design inclui o uso de um destes CAs públicos, você não precisa fazer este passo.

Depois de exportar o certificado de [raiz de confiança,](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)precisa instalá-lo em dispositivos que necessitem dele para se inscrever. Por exemplo, dispositivos que não estão unidos ao domínio e não podem obtê-lo automaticamente a partir do Diretório Ativo. O processo que utilizar dependerá dos seguintes fatores:

- Tipos específicos de dispositivos e capacidades técnicas
- Versão do SO
- Os seus requisitos de negócio, segurança e experiência do utilizador

A lista que se segue inclui alguns métodos de exemplo para entregar e instalar o certificado de raiz fidedigno nos dispositivos:

- Partilha de ficheiros

- Anexo de e-mail

- Cartão de memória

- Dispositivo tethered

- Armazenamento na nuvem (por exemplo, o OneDrive)

- Ligação de comunicação de proximidade (NFC)

- Scanner de código de barras

- Pacote de aprovisionamento OOBE (out of box experience)

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Instale manualmente o certificado de raiz fidedigno no Windows

1. No dispositivo a ser matriculado, navegue no File Explorer até ao **Open** ficheiro de certificado de raiz confiável (.cer) e abra-o.

1. Na janela do Certificado, selecione **Certificado de Instalação**.

1. No Assistente de Importação de Certificado, selecione **Local Machine**, e, em seguida, selecione **Next** para continuar como administrador.

1. Na página da Loja de Certificados, selecione **Colocar todos os certificados na seguinte loja,** e, em seguida, selecione **Browse**.

1. Na janela Select Certificate Store, selecione **Trusted Root Certification Authorities**, e selecione **OK**.

1. Completo e feiticeiro.

## <a name="next-step"></a>Passo seguinte

> [!div class="nextstepaction"]
> [Inscrever dispositivos](../deploy-use/enroll-devices-on-premises-mdm.md)
