---
title: Integrar o Zimperium MTD com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Como configurar a solução de Defesa Contra Ameaças (MTD) do Zimperium com o Microsoft Intune para controlar o acesso aos seus recursos empresariais a partir de dispositivos móveis.
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
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4666c8c765f15ddd103727ccf2a7d840cb69bd20
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989358"
---
# <a name="integrate-zimperium-with-intune"></a>Integrar o Zimperium com o Intune

Tem de realizar os passos seguintes para integrar a solução de Defesa Contra Ameaças para Dispositivos Móveis do Zimperium com o Intune.

## <a name="before-you-begin"></a>Antes de começar

Os seguintes passos são feitos na [consola Zimperium MTD](https://www.zimperium.com/platform) e permitirão uma ligação ao serviço da Zimperium tanto para dispositivos inscritos intune (utilizando a conformidade do dispositivo) como para dispositivos não matriculados (utilizando políticas de proteção de aplicações).

Antes de iniciar o processo de integração do Zimperium com o Intune, certifique-se de que tem a seguinte subscrição e credenciais:

- Subscrição do Microsoft Intune

- Credenciais de administrador global do Diretório Ativo Azure para conceder as seguintes permissões:

  - Iniciar sessão e ler o perfil de utilizador

  - Aceder ao diretório como o utilizador com sessão iniciada

  - Ler os dados do diretório

  - Enviar informações do dispositivo para o Intune

- Credenciais do administrador para aceder à consola do Zimperium MTD.

### <a name="zimperium-app-authorization"></a>Autorização da aplicação Zimperium

O processo de autorização da aplicação Zimperium consiste no seguinte:

- Conceda ao serviço zimperium permissões para comunicar informações relacionadas com o estado de saúde do dispositivo de volta ao Intune. Para conceder estas permissões, deve utilizar credenciais do Administrador Global. Conceder permissões é uma operação única. Após a concessão das permissões, as credenciais do Administrador Global não são necessárias para o funcionamento do dia-a-dia.

- Zimperium sincroniza-se com a filiação do Grupo de Inscrição do Azure Ative Directory (AD) para preencher a base de dados do seu dispositivo.

- Permitir que a consola de administração do Zimperium utilize o Início de Sessão Único (SSO) do Azure AD.

- Permitir que a aplicação Zimperium inicie sessão através do SSO do Azure AD.

Para obter mais informações sobre o consentimento e as aplicações do Diretório Ativo Azure, consulte [Solicite as permissões de um administrador de diretório](https://docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) no artigo diretório ativo azure *Permissões e consentimento no Ponto final do Diretório Ativo Azure v2.0*.


## <a name="to-set-up-zimperium-integration"></a>Para configurar a integração do Zimperium

1. Aceda à [Consola do Zimperium MTD](https://www.zimperium.com/platform) e inicie sessão com as suas credenciais. Para realizar o processo de configuração de integração zimperium, deve iniciar sessão com um utilizador do Azure Ative Directory que tenha o papel de Administrador Global. Esta operação de configuração única utiliza os direitos do Administrador Global para conceder permissão na sua organização para que as aplicações zimperium se comuniquem com a Intune. 

2. Selecione **Gestão** a partir do menu esquerdo.

3. Selecione o separador **definições de MDM**.

4. Selecione **Adicionar MDM** e, em seguida, selecione **Microsoft Intune** a partir da lista **Fornecedor de MDM**.

5. Assim que definir o Microsoft Intune como serviço MDM, é apresentada a janela **Configuração do Microsoft Intune**, escolha **Adicionar Azure Active Directory** para cada opção: **Zimperium zConsole** e **Aplicações zIPS para iOS e Android** para autorizar o Zimperium a comunicar com o Intune e o Azure AD através do Início de Sessão Único do Azure AD.

    > [!IMPORTANT]  
    > Você deve adicionar as aplicações Zimperium zConsole, zIPS iOS e Android para completar o processo de integração com intune.

6. Selecione **Aceitar** para autorizar a aplicação Zimperium a comunicar com o Intune e o Azure Active Directory.

7. Depois de adicionar o **Zimperium zConsole** e as aplicações **zIPS iOS e Android** ao Azure AD, adicione os grupos de segurança Azure AD. Esta adição permite que o Zimperium sincronize o grupo de segurança do Azure AD com o seu serviço.

8. Selecione **Concluir** para guardar a configuração e iniciar a primeira sincronização do grupo de segurança do Azure AD.

9. Assine a consola Zimperium MTD.

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicativos Zimperium para dispositivos matriculados](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurar aplicativos Zimperium para dispositivos não matriculados](mtd-add-apps-unenrolled-devices.md)
