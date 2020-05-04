---
title: Criar perfis de certificado PFX
titleSuffix: Configuration Manager
description: Saiba como utilizar ficheiros PFX no Gestor de Configuração para gerar certificados específicos do utilizador que suportam a troca de dados encriptado.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711176"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Criar perfis de certificadoS PFX utilizando uma autoridade de certificado

*Aplica-se a: Gestor de Configuração (ramo atual)*

Aprenda a criar um perfil de certificado que utilize uma autoridade de certificação para credenciais. Este artigo destaca informações específicas sobre perfis de certificados de troca de informações pessoais (PFX). Para obter mais informações sobre como criar e configurar estes perfis, consulte os perfis de [Certificado.](../../protect/deploy-use/introduction-to-certificate-profiles.md)

O Gestor de Configuração permite-lhe criar um perfil de certificado PFX utilizando credenciais emitidas por uma autoridade de certificados. Pode escolher a Microsoft ou confiar como autoridade de certificados. Quando implantados em dispositivos de utilizador, os ficheiros PFX geram certificados específicos do utilizador para suportar a troca de dados encriptada.

Para importar credenciais de certificado saqueados de ficheiros de certificados existentes, consulte os perfis de [certificados De Importação PFX](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar a criar um perfil de certificado, certifique-se de que os pré-requisitos necessários estão prontos. Para mais informações, consulte [os pré-requisitos para](../../protect/plan-design/prerequisites-for-certificate-profiles.md)os perfis de certificados . Por exemplo, para perfis de certificados PFX, você precisa de uma função de sistema de site de ponto de registo de [certificado.](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point)

## <a name="create-a-profile"></a>Criar um perfil  

1. Na consola de Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade, expanda o Acesso aos **Recursos da Empresa,** e depois selecione Perfis de **Certificado.**

1. No separador **Home** da fita, no grupo **Criar,** selecione **Criar Perfil**de Certificado .

1. Na página **geral** do Assistente de Perfil de **Certificado,** especifique as seguintes informações:  

    - **Nome**: introduza um nome exclusivo para o perfil do certificado. Pode utilizar até 256 carateres.  

    - **Descrição**: Forneça uma descrição que dê uma visão geral do perfil do certificado que ajude a identificá-lo na consola Do Gestor de Configuração. Pode utilizar até 256 carateres.  

1. Selecione **Troca de Informações Pessoais - Definições de #12 PKCS (PFX) - Criar**. Esta opção solicita um certificado em nome de um utilizador de uma autoridade de certificados ligadono local (CA). Escolha a autoridade do seu certificado: **Microsoft** ou **Confie o Cartão de Dados**.

    > [!NOTE]
    > A opção **Import** obtém informações de um certificado existente para criar um perfil de certificado. Para mais informações, consulte os perfis de [certificados Import PFX](import-pfx-certificate-profiles.md).

1. Na página **Plataformas Suportadas,** selecione as versões S que este perfil de certificado suporta. Para obter mais informações sobre as versões de SISTEMA suportadas para a sua versão de 'Gestor de Configuração', consulte [versões De SO suportadas para clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. Na página **das Autoridades** de Certificados, escolha o ponto de registo do certificado (CRP) para processar os certificados PFX:

    1. **Sítio Primário**: Escolha o servidor que contém a função CRP para o CA.
    1. **Autoridades de certificação**: Selecione o CA relevante.

    Para mais informações, consulte infraestrutura de [certificados.](../../protect/deploy-use/certificate-infrastructure.md)

As definições na página do **Certificado PFX** variam consoante o CA selecionado na página **geral:**

- [Microsoft CA](#bkmk_microsoft)
- [Confiar datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Configure as definições de **certificado PFX** para microsoft CA

1. Para o nome do **modelo de certificado,** escolha o modelo de certificado.

1. Para utilizar o perfil do certificado para a assinatura ou encriptação S/MIME, ative a **utilização do Certificado**.

    Quando ativa esta opção, entrega todos os certificados PFX associados ao utilizador-alvo a todos os seus dispositivos. Se não ativar esta opção, cada dispositivo recebe um certificado único.  

1. Definir **o formato** de nome do assunto para **o nome comum** ou **nome totalmente distinto**. Se não tiver a certeza de qual usar, contacte o seu administrador da AC.

1. Para o **nome alternativo do Assunto,** ative o **endereço de e-mail** e o **nome principal do utilizador (UPN)** conforme apropriado para a sua CA.

1. **Limiar de renovação**: Determina quando os certificados são automaticamente renovados, com base na percentagem de tempo restante antes da expiração.

1. Definir o prazo de validade do **Certificado** ao tempo de validade do certificado.

1. Quando o ponto de registo do certificado especificar credenciais de Diretório Ativo, ative **a publicação do Diretório Ativo**.

1. Se selecionou uma ou mais plataformas suportadas pelo Windows 10:

    1. Detete a loja de **certificados Windows** para **User**. (A opção **Computador Local** não implementa certificados, não o escolhe.)

    1. Selecione um dos seguintes Fornecedores de Armazenamento de **Chaves (KSP)**:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Módulo plataforma fidedigno (TPM) de outra forma falhar**
        - **Instalar no Windows Hello for Business falha de outra forma**
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software**

1. Conclua o assistente.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Configure as definições de **certificado PFX** para confiar cartão de dados CA

1. Para a **configuração de ID digital,** escolha o perfil de configuração. O administrador entrust cria as opções de configuração de ID digitais.

1. Para utilizar o perfil do certificado para a assinatura ou encriptação S/MIME, ative a **utilização do Certificado**.

    Quando ativa esta opção, entrega todos os certificados PFX associados ao utilizador-alvo a todos os seus dispositivos. Se não ativar esta opção, cada dispositivo recebe um certificado único.  

1. Para mapear fichas de **formato** de nome de assunto de confiar aos campos de Gestor de Configuração, selecione **Formato**.

    O diálogo **formatação de nome** do certificado lista as variáveis de configuração de ID digital entrust. Para cada variável Entrust, escolha os campos de Gestor de Configuração apropriados.

1. Para mapear fichas **alternativas** de assunto de confiar às variáveis LDAP suportadas, selecione **Formato**.

    O diálogo **formatação de nome** do certificado lista as variáveis de configuração de ID digital entrust. Para cada variável Entrust, escolha a variável LDAP apropriada.

1. **Limiar de renovação**: Determina quando os certificados são automaticamente renovados, com base na percentagem de tempo restante antes da expiração.

1. Definir o prazo de validade do **Certificado** ao tempo de validade do certificado.

1. Quando o ponto de registo do certificado especificar credenciais de Diretório Ativo, ative **a publicação do Diretório Ativo**.

1. Se selecionou uma ou mais plataformas suportadas pelo Windows 10:

    1. Detete a loja de **certificados Windows** para **User**. (A opção **Computador Local** não implementa certificados, não o escolhe.)

    1. Selecione um dos seguintes Fornecedores de Armazenamento de **Chaves (KSP)**:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Módulo plataforma fidedigno (TPM) de outra forma falhar**
        - **Instalar no Windows Hello for Business falha de outra forma**
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software**

1. Conclua o assistente.

## <a name="deploy-the-profile"></a>Implementar o perfil

Depois de criar um perfil de certificado, está agora disponível no nó de Perfis de **Certificado.** Para obter mais informações sobre como implementá-lo, consulte [os perfis](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)de acesso aos recursos .

## <a name="see-also"></a>Consulte também

[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md)

[Importar perfis de certificado PFX](import-pfx-certificate-profiles.md)

[Implementar perfis Wi-Fi, VPN, de e-mail e de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
