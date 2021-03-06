---
title: Configurar a integração da Symantec com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Como configurar a solução Symantec Endpoint Protection Mobile com o Microsoft Intune para controlar o acesso de dispositivos móveis aos seus recursos empresariais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 359448d9-2384-42ac-a21c-a25148c20a7b
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9ebd42a4603224004ab586fb6648dcd6360e2f94
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988302"
---
# <a name="set-up-symantec-endpoint-protection-mobile-integration-with-intune"></a>Configurar a integração do Symantec Endpoint Protection Mobile com o Intune

Conclua os seguintes passos para integrar a solução Symantec Endpoint Protection Mobile (SEP Mobile) com o Intune. Tem de adicionar aplicações do SEP Mobile ao Azure AD para ter capacidades de Início de Sessão Único.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="before-you-begin"></a>Antes de começar

### <a name="azure-ad-account-used-to-integrate-intune-and-sep-mobile"></a>A conta do Azure AD utilizada para integrar o Intune e o SEP Mobile

- Confirme se configurou corretamente a conta do Azure AD na [consola do Symantec Endpoint Protection Mobile Management](https://aad.skycure.com) antes de iniciar o processo de Configuração Básica do SEP Mobile.
- A conta do Azure AD tem de ser uma conta de administrador global para realizar a integração.
### <a name="network-setup"></a>Configuração da Rede

Pode certificar-se de que a sua rede está devidamente configurada para integração com a configuração do SEP Mobile, referindo-se ao artigo symantec [Configurando o SeP Manager após](http://techdocs.broadcom.com/content/broadcom/techdocs/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/Managing_a_Custom_Installation_3/Planning_the_Installation_0/network-architecture-considerations-v19543152-d23e65.html)a instalação .

### <a name="full-integration-vs-read-only"></a>Integração completa vs. Leitura

O SEP Mobile suporta dois modos de integração com o Intune:

- **Integração Só de leitura (Configuração básica):** apenas fará o inventário dos dispositivos do Azure Active Directory e preenche-os na consola do Symantec Endpoint Protection Mobile Management.
<br>
  - Se as caixas **Comunicar o estado de funcionamento e o risco dos dispositivos ao Intune** e **Comunicar também incidentes de segurança ao Intune** não estiverem selecionadas na consola do Symantec Endpoint Protection Mobile Management, a integração será só de leitura e, como tal, nunca irá alterar o estado dos dispositivos (conformes ou não conformes) no Intune.
<br></br>
- **Integração total:** permite ao SEP Mobile comunicar detalhes de incidentes de segurança e riscos dos dispositivos ao Intune, que cria uma comunicação bidirecional entre ambos os serviços cloud.

### <a name="how-are-the-sep-mobile-apps-used-with-azure-ad-and-intune"></a>Como são as aplicações do SEP Mobile utilizadas com o Azure AD e o Intune?

- **aplicativo iOS:** Permite que os utilizadores finais inscrevam-se no Azure AD através de uma aplicação iOS/iPadOS.

- **Aplicação Android:** permite que os utilizadores finais iniciem sessão no Azure AD com uma aplicação Android.

- **Aplicação de gestão:** esta é a aplicação multi-inquilino do Azure AD do SEP Mobile que permite a comunicação entre serviços com o Intune.

## <a name="to-set-up-the-read-only-integration-between-intune-and-sep-mobile"></a>Para configurar a integração só de leitura entre o Intune e o SEP Mobile

> [!IMPORTANT]
> As credenciais de administrador do SEP Mobile têm de ser uma conta de e-mail que pertença a um utilizador válido no Azure Active Directory. Caso contrário, o início de sessão falhará. O SEP Mobile utiliza o Azure Active Directory para autenticar o administrador através do Início de Sessão Único (SSO).

1. Aceda à [consola do Symantec Endpoint Protection Mobile Management](https://aad.skycure.com).

2. Introduza as **credenciais de administrador do SEP Mobile** e, em seguida, escolha **Continuar**.

3. Aceda a **Definições** e, em **Integração do Intune**, escolha **Configuração Básica**.

4. Junto a **Aplicação iOS**, escolha **Adicionar ao Active Directory**.

    ![Imagem da consola de gestão móvel de proteção de endpoint symantec](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

5. Quando for apresentada a página de início de sessão, introduza as suas credenciais do Intune e escolha **Aceitar**.

    ![Imagem da aplicação iOS/iPadOS Intune](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

6. Depois de a aplicação ser adicionada ao Azure AD, verá uma indicação de que a aplicação foi adicionada com êxito.

    ![Imagem do ecrã de conclusão da aplicação iOS/iPadOS](./media/skycure-mtd-connector-integration/symantec-portal-basic-added.png)

7. Repita estes passos para as aplicações **SEP móvel para Android** e **Gestão**.

### <a name="add-an-azure-ad-security-group-into-sep-mobile"></a>Adicionar um Grupo de segurança do Azure AD ao SEP Mobile

Tem de adicionar um grupo de segurança do Azure AD que contenha todos os dispositivos que executam o SEP Mobile.

- Introduza e selecione todos os grupos de segurança de dispositivos que executem o SEP Mobile e, em seguida, guarde as alterações.

    ![Imagem que mostra os grupos de utilizadores para aplicações do SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

O SEP Mobile sincroniza os dispositivos que executam o serviço Defesa Contra Ameaças para Dispositivos Móveis com os grupos de segurança do Azure AD.

![Imagem de configuração do grupo de segurança na consola de gestão SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.png)

## <a name="to-set-up-the-full-integration-between-intune-and-sep-mobile"></a>Para configurar a integração total entre o Intune e o SEP Mobile

### <a name="retrieve-the-directory-id-in-azure-ad"></a>Obter o ID do Diretório no Azure AD

1. Inicie sessão no [portal do Azure](https://portal.azure.com).

2. Escreva “Active Directory” na caixa de pesquisa e, em seguida, selecione **Azure Active Directory**.

3. Escolha **Propriedades**.

4. Junto a **ID do Diretório**, escolha o ícone de copiar e, em seguida, cole-o numa localização segura. Vai precisar deste identificador num passo posterior.

    ![Imagem que mostra o ID do Diretório no portal do Azure](./media/skycure-mtd-connector-integration/symantec-azure-portal-directory-ID.png)

### <a name="optional-create-a-dedicated-security-group-for-devices-that-need-to-run-the-sep-mobile-apps"></a>(Opcional) Criar um Grupo de Segurança dedicado para os dispositivos que têm de executar as aplicações do SEP Mobile
1. No [portal do Azure](https://portal.azure.com), em **Gerir**, escolha **Utilizadores e grupos** e, em seguida, **Todos os grupos**.

2. Escolha o botão **Adicionar**. Escreva um **Nome** de grupo. Em **Tipo de associação**, escolha **Atribuído**.

3. No painel **Membros**, selecione os membros do grupo e, em seguida, escolha o botão **Selecionar**.

4. No painel **Grupo**, escolha **Criar**.

### <a name="set-up-the-integration-between-symantec-endpoint-protection-mobile-and-intune"></a>Configurar a integração entre o Symantec Endpoint Protection Mobile e o Intune

1. Aceda à [consola do Symantec Endpoint Protection Mobile Management](https://aad.skycure.com).

2. Introduza as **credenciais de administrador do SEP Mobile** e, em seguida, escolha **Continuar**.

3. Vá à **Settings**secção de Seleção de  >  **Integrations**  >  Integração em EMM**intune.**  >  **EMM Integration Selection**

4. No caixa **ID do Diretório**, cole o ID do Diretório que copiou do Azure Active Directory na secção anterior e guarde as definições.

    ![Imagem que mostra o ID do Diretório no portal do SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-directory-ID.png)

5. Vá à **Settings**secção de  >  **Configurações Integrações**  >  **Intune**  >  **Basic Setup.**

6. Junto a **Aplicação iOS**, escolha o botão **Adicionar ao Active Directory**.

    ![Imagem mostrando adicionar a app iOS/iPadOS ao Diretório Ativo](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

7. Inicie sessão com as credenciais do Azure Active Directory na conta do Office 365 que gere o diretório.

8. Escolha o botão **Accept** para adicionar a aplicação SEP Mobile iOS/iPadOS ao Diretório Ativo Azure.

    ![Imagem que mostra o botão aceitar](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

9. Repita o mesmo processo para a **aplicação Android** e a **Aplicação Gestão**.

10. Selecione todos os grupos de utilizadores que precisam de executar as aplicações SEP Mobile, por exemplo, o grupo de segurança que criou anteriormente.

    ![Imagem que mostra os grupos de utilizadores para aplicações do SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

11. O SEP Mobile sincroniza os dispositivos nos grupos selecionados e começa a comunicar informações ao Intune. Pode ver estes dados na secção Integração Total. Vá à **Settings**  >  secção integrações de**definições**  >  **Intune**  >  **Full Integration.**

     ![Imagem que mostra a integração total do SEP Mobile concluída](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.PNG)
## <a name="next-steps"></a>Passos seguintes

[Configurar as aplicações do SEP Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)
