---
title: Como matricular a granel dispositivos
titleSuffix: Configuration Manager
description: Dispositivos de inscrição a granel de forma automatizada com gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720682"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Como matricular dispositivos a granel com MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A inscrição a granel no Diretor de Configuração no local de gestão de dispositivos móveis (MDM) é um método automatizado para inscrever dispositivos. O outro método é a inscrição do utilizador, que exige que os utilizadores introduzam as suas credenciais para inscrever o dispositivo. A inscrição em massa utiliza um pacote de inscrição para autenticar o dispositivo durante a inscrição. O pacote é um ficheiro .ppkg, que também pode conter certificado e perfis Wi-Fi para apoiar a inscrição.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a>Criar um perfil de certificado

Inclua um perfil de certificado para instalar automaticamente um certificado de raiz fidedigno no dispositivo. Este certificado de raiz é necessário para uma comunicação fidedigna entre os dispositivos e as funções do sistema do site necessárias para o MDM no local.

Quando prepara o site para o MDM no local, exporta o certificado de raiz de confiança. Utilize este certificado no perfil de certificado do pacote de matrículas. Para obter mais informações sobre como obter o certificado de raiz fidedigno, consulte [Exportar o certificado raiz fidedigno](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Utilize o certificado exportado para criar um perfil de certificado. Para mais informações, consulte [Como criar perfis de certificado](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a>Criar um perfil Wi-Fi

Outro componente do pacote de matrículas a granel é um perfil Wi-Fi. Este perfil pode certificar-se de que o dispositivo tem a conectividade da rede para suportar a inscrição.

Para obter mais informações sobre como criar um perfil Wi-Fi no Gestor de Configuração, consulte [como criar perfis Wi-Fi](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Limitações de perfil Wi-Fi

Quando criar um perfil Wi-Fi para inscrição em massa no local do MDM, reveja as seguintes limitações.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Configurações de segurança Wi-Fi para MDM no local

O atual ramo do Gestor de Configuração apenas suporta as seguintes configurações de segurança Wi-Fi para o MDM no local:

- Tipos de segurança: **WPA2 Enterprise** ou **WPA2 Personal**

- Tipos de encriptação: **AES** ou **TKIP**

- Tipos de EAP: **Smart Card ou outro certificado** ou **PEAP**

#### <a name="proxy-server"></a>Servidor proxy

Embora o Gestor de Configuração tenha uma definição para informações do servidor proxy no perfil Wi-Fi, não configura o proxy quando o dispositivo se inscreve. Se precisar de configurar um servidor proxy em dispositivos matriculados a granel:

- Implemente as definições utilizando itens de configuração assim que os dispositivos se inscreverem.

- Crie um segundo pacote utilizando o Windows Image and Configuration Designer (ICD), em seguida, implemente-o juntamente com o pacote de matrículas a granel.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a>Criar um perfil de inscrição

O perfil de inscrição permite especificar as definições necessárias para a inscrição do dispositivo. Estas definições incluem um perfil de [certificado](#bkmk_createCert) e um [perfil Wi-Fi](#CreateWifi).

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance,** expanda **Todos os Dispositivos Corporativos,** expanda **o Windows**e selecione o nó de Perfis **de Inscrição.**

1. Na fita, selecione **Criar perfil de inscrição**.

1. Na página **Geral** do Assistente de Perfil de Inscrição Criar, especifique as seguintes informações:

    - **Nome**: Um nome único para identificar o perfil

    - **Descrição**: Um campo opcional para descrever ainda mais o perfil

    - **Autoridade de Gestão**: Selecione apenas **as instalações**

1. Na página de atribuição do **Site,** selecione o código do **site de gestão** com um ponto de gestão do dispositivo.

1. Na página **Select Registration Proxy Point,** selecione **Intranet Only**e, em seguida, selecione um ou mais pontos de procuração de inscrição. O dispositivo utilizará estes servidores para iniciar o processo de inscrição.

1. Na página **Select Trusted Root Certificate,** selecione o perfil do certificado que contém o certificado raiz fidedigno.

1. Na página de **perfis Wi-Fi,** selecione o perfil Wi-Fi que contém as definições de rede necessárias para os dispositivos se conectarem.

    > [!TIP]
    > Se não estiver a usar um perfil Wi-Fi para o seu pacote de matrículas, ignore este passo.

1. Conclua o assistente.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>Criar um pacote de inscrição

O pacote de inscrição (ppkg) é o ficheiro que utiliza para matricular dispositivos a granel para o MDM no local. Crie este ficheiro com o Gestor de Configuração. Embora possa criar tipos de pacotes semelhantes com o Windows ICD, apenas os pacotes que cria no 'Gestor de Configuração' podem ser utilizados para inscrever dispositivos para o MDM no local. Um pacote que cria com o Windows ICD só pode fornecer o nome principal do utilizador (UPN) necessário para a inscrição, não pode iniciar o processo de inscrição real.

O processo para criar o pacote de inscrição requer o Windows Assessment and Deployment Kit (ADK) para Windows 10. No computador que executa a consola 'Gestor de Configuração', instale a versão mais recente do Windows ADK. Selecione a função **De imagem e configuração (ICD)** e quaisquer dependências. (Esta versão não precisa de corresponder à versão utilizada para a implementação de SO pelo site do Gestor de Configuração.) Para mais informações, consulte [O Windows ADK para windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install).

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance,** expanda **Todos os Dispositivos Corporativos,** expanda **o Windows**e selecione o nó de Perfis **de Inscrição.**

1. Selecione um perfil de inscrição existente. Na fita, selecione **Exportação**.

1. Na janela do Pacote de Matrículas para Exportação, especifique as seguintes informações:

    - **Período de validade (dias)**: Por predefinição, o Gestor de Configuração define o pacote de inscrição para expirar em duas semanas (14 dias). Não pode utilizar o pacote para inscrição no dispositivo após o termo do período de validade. Introduza uma inteiro entre 1 e 30.

    - **Ficheiro de pacote**: Especifique um caminho de ficheiro local ou de rede e nome para o ficheiro .ppkg.

    - **Pacote de encriptação**: Ative esta opção para proteger a embalagem com palavra-passe. Depois de exportar o pacote, o Gestor de Configuração exibe a palavra-passe gerada. Copie e guarde a palavra-passe num local seguro. Não pode usar o pacote de matrículas exportado sem a senha.

        > [!IMPORTANT]
        > O Gestor de Configuração não guarda a palavra-passe e não pode personalizá-la ou alterá-la. Assim que fechares a janela que exibe a senha, não há como recuperar a senha.

1. Selecione **Export** (Exportar). O Gestor de Configuração utiliza o Windows ADK para criar o pacote de matrículas.

O Gestor de Configuração regista pacotes de inscrição válidos. Na consola, expanda o nó do **Perfil de Inscrição** e selecione **Pacotes Exportados**.

> [!TIP]
> Se remover um pacote de inscrição da consola 'Gestor de Configuração', não pode utilizá-lo para inscrever dispositivos. Utilize este método para gerir pacotes de inscrição que não quer que outros utilizem para a inscrição a granel.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>Inscrição a granel de um dispositivo

Pode utilizar uma embalagem para inscrever dispositivos antes ou depois do processo de experiência fora de caixa do dispositivo (OOBE). O pacote de inscrição também pode ser incluído como parte de um pacote original de fornecimento do fabricante de equipamentos (OEM).

Para utilizar o pacote para inscrição a granel, é necessário entregá-lo fisicamente ao dispositivo. Existem vários métodos dependendo das suas necessidades, por exemplo:

- Cópia do sistema de ficheiros

- Anexar a um e-mail

- Copiar através de uma ligação de comunicação de campo próximo (NFC)

- Cópia de um cartão de memória

- Scaneie um código de barras

- Copiar de um dispositivo tethered

- Incluir num pacote de provisionamento OEM

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Inscreva um dispositivo com pacote de inscrição a granel

1. Num dispositivo, abra o ficheiro .ppkg. Se necessário, corra como administrador.

1. O Windows pergunta se o pacote é de uma fonte fidedigna, selecione **Sim**.

O processo de inscrição começa.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>Verificar a inscrição

### <a name="verify-bulk-enrollment-on-the-device"></a>Verifique a inscrição a granel no dispositivo

1. No aparelho, abra **As Definições**.

1. Selecione **Contas,** e selecione **Trabalho de acesso ou escola.** Quando a inscrição é bem sucedida, você vê uma conta no **CompanyApps**.

1. Selecione a conta e, em seguida, selecione **Sync**. Esta ação começa a gestão com o Gestor de Configuração.

### <a name="verify-enrollment-in-the-console"></a>Verifique a inscrição na consola

Utilize a consola 'Gestor de Configuração' para verificar se os dispositivos estão matriculados com sucesso. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione **Dispositivos**. Navegue ou procure o dispositivo inscrito na lista de dispositivos.
