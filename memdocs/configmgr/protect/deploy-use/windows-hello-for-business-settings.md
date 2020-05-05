---
title: Definições do Windows Hello para Empresas
titleSuffix: Configuration Manager
description: Saiba como integrar o Windows Hello for Business com O Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722236"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Windows Olá para configurações de negócios em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1245704-->
O Gestor de Configuração integra-se com o Windows Hello for Business. (Esta funcionalidade era anteriormente conhecida como Microsoft Passport for Work.) O Windows Hello for Business é um método alternativo de sessão para dispositivos Windows 10. Utiliza o Ative Directory ou uma conta Azure Ative Directory (Azure AD) para substituir uma palavra-passe, cartão inteligente ou cartão inteligente virtual. Hello for Business permite-lhe usar um gesto de *utilizador* para iniciar sessão em vez de uma senha. Um gesto de utilizador pode ser um PIN, autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.

> [!Important]  
> A partir da versão 1910, a autenticação baseada em certificados com definições do Windows Hello for Business no 'Gestor de Configuração' não é suportada. Para mais informações, consulte [funcionalidades depreciadas.](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md) A autenticação baseada em chaves ainda é válida.
>
> A implantação da Ative Directory Federation Services Authority (ADFS RA) é mais simples, proporciona uma melhor experiência de utilizador e tem uma experiência de inscrição de certificados mais determinista. Utilize a ADFS RA para autenticação baseada em certificados com o Windows Hello for Business.
>
> Para dispositivos cogeridos, considere mover a carga de trabalho das políticas de acesso ao [ **Recurso** ](../../comanage/workloads.md#resource-access-policies) para Intune. Em seguida, utilize políticas intune para gerir estes certificados. Para mais informações, consulte [Como mudar as cargas de trabalho](../../comanage/how-to-switch-workloads.md).

Para mais informações, consulte [o Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

O Gestor de Configuração integra-se com o Windows Hello for Business das seguintes formas:  

- Controle quais os gestos que os utilizadores podem e não podem usar para iniciar sessão.  

- Guarde os certificados de autenticação no fornecedor de armazenamento de chaves Windows Hello for Business (KSP). Para mais informações, consulte [os perfis do Certificado](introduction-to-certificate-profiles.md).  

- Criar e implementar um perfil Windows Hello for Business para controlar as suas definições em dispositivos Windows 10 ligados ao domínio que executam o cliente do Gestor de Configuração. A partir da versão 1910, não pode utilizar a autenticação baseada em certificados. Ao utilizar a autenticação baseada na chave, não precisa de implementar um perfil de certificado.

## <a name="configure-a-profile"></a>Configurar um perfil  

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Expandir **as Definições**de Conformidade, expandir o Acesso aos Recursos da **Empresa**e selecionar o nó do Windows Hello para **Perfis empresariais.**

1. Na fita, selecione **Create Windows Hello for Business Profile** para iniciar o assistente de perfil.

1. Na página **Geral,** especifique um nome e uma descrição opcional para este perfil.

1. Na página **Plataformas Suportadas,** selecione as versões S a que este perfil deve ser aplicado.

1. Na página **Definições,** configure as seguintes definições:

    - **Configure o Windows Hello for Business**: Especifique se este perfil permite, desativa ou não configura o Hello for Business.

    - **Utilize um Módulo de Plataforma Fidedigna (TPM)**: Um TPM fornece uma camada adicional de segurança de dados. Escolha um dos seguintes valores:  

      - **Obrigatório**: Apenas dispositivos com um TPM acessível podem fornecer O Windows Hello para Negócios.  

      - **Preferência**: Os dispositivos tentam utilizar um TPM. Se não estiver disponível, podem usar encriptação de software.

    - **Método de autenticação**: Desloque esta opção para **não configurado** ou **baseado em chaves**.

        > [!NOTE]
        > A partir da versão 1910, a autenticação baseada em certificados com definições do Windows Hello for Business no 'Gestor de Configuração' não é suportada.

    - **Configurar**o comprimento pin mínimo : Se pretender exigir um comprimento mínimo para o PIN do utilizador, ative esta opção e especifique um valor. Quando ativado, o `4`valor predefinido é .

    - **Configurar**o comprimento máximo pin : Se pretender exigir um comprimento máximo para o PIN do utilizador, ative esta opção e especifique um valor. Quando ativado o `127`valor predefinido é .

    - **Requerer a expiração do PIN (dias)**: Especifica o número de dias antes de o utilizador alterar o PIN do dispositivo.

    - **Evite a reutilização de PINs anteriores**: Não permita que os utilizadores utilizem PINs que tenham utilizado anteriormente.

    - **Requerer letras maiúsculas no PIN**: Especifica se os utilizadores devem incluir letras maiúsculas no Windows Hello for Business PIN. Escolha entre:  

      - **Permitido**: Os utilizadores podem utilizar caracteres maiúsculos no seu PIN, mas não têm de o fazer.

      - **Requerido**: Os utilizadores devem incluir pelo menos um caracteres maiúsculos no seu PIN.  

      - **Não é permitido**: Os utilizadores não podem usar caracteres maiúsculos no seu PIN.  

    - **Requerer letras minúsculas no PIN**: Especifica se os utilizadores devem incluir letras minúsculas no Windows Hello for Business PIN. Escolha entre:  

      - **Permitido**: Os utilizadores podem utilizar caracteres minúsculos no seu PIN, mas não têm de o fazer.

      - **Requerido**: Os utilizadores devem incluir pelo menos um caracteres minúsculos no seu PIN.  

      - **Não é permitido**: Os utilizadores não podem usar caracteres minúsculos no seu PIN.  

    - **Configurar caracteres especiais:** Especifica a utilização de caracteres especiais no PIN. Escolha entre:  

        > [!NOTE]
        > Os caracteres especiais incluem o seguinte conjunto:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Permitido**: Os utilizadores podem usar caracteres especiais no seu PIN, mas não têm de o fazer.  

      - **Obrigatório**: Os utilizadores devem incluir pelo menos um carácter especial no seu PIN.  

      - **Não é permitido**: Os utilizadores não podem usar caracteres especiais no seu PIN. Este comportamento também é se a definição não estiver **configurada**.  

    - **Configure a utilização de dígitos no PIN**: Especifica a utilização dos números no PIN. Escolha entre:

      - **Permitido**: Os utilizadores podem utilizar números no seu PIN, mas não têm de o fazer.  

      - **Obrigatório**: Os utilizadores devem incluir pelo menos um número no seu PIN.  

      - **Não é permitido**: Os utilizadores não podem utilizar números no seu PIN.

    - **Ativar gestos biométricos**: Utilize a autenticação biométrica, como reconhecimento facial ou impressão digital. Estes modos são uma alternativa a um PIN para Windows Hello for Business. Os utilizadores ainda configuram um PIN caso a autenticação biométrica falhe.  

      Se definido para **Sim**, o Windows Hello for Business permite a autenticação biométrica. Se definido para **Não**, o Windows Hello for Business impede a autenticação biométrica para todos os tipos de conta.  

    - **Utilize uma anti-falsificação melhorada**: Configures reforços anti-falsificação em dispositivos que o suportam. Se definido para **Sim**, onde suportado, o Windows requer que todos os utilizadores utilizem anti-falsificação para funcionalidades faciais.  

    - **Utilizar o sinal do telefone**: Configura a autenticação de dois fatores com um telemóvel.

1. Conclua o assistente.

A seguinte imagem é um exemplo das definições de perfil do Windows Hello para negócios:  

![Windows Hello para assistente de política de negócios, mostrando a lista de definições disponíveis](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Configurar permissões

1. Como Administrador de Domínio ou credenciais equivalentes, inscreva-se numa estação de trabalho administrativa segura e com a seguinte funcionalidade opcional instalada: RSAT: Ative Directory Domain Services e Lightweight Directory Services Tools.

1. Abra a consola **Ative Directory Users and Computers.**

1. Selecione o domínio, vá ao Menu **de Ação** e selecione **Propriedades**.

1. Mude para o separador **Segurança** e selecione **Advanced**.

    > [!TIP]
    > Se não vir a conta de **segurança,** feche a janela das propriedades. Vá ao menu **'Ver'** e **selecione Funcionalidades Avançadas**.

1. Selecione **Adicionar**.

1. Escolha **Selecione um comitente** e introduza `Key Admins`.

1. Do **Aplicável à** lista, selecione **objetos de utilizador descendentes**.

1. Na parte inferior da página, selecione **Clear all**.

1. Na secção **Propriedades,** selecione **Ler msDS-KeyCredentialLink**.

1. Selecione **OK** para guardar as suas alterações e feche todas as janelas.

## <a name="next-steps"></a>Passos seguintes

[Perfis de certificado](introduction-to-certificate-profiles.md)
