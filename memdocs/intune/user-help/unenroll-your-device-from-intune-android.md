---
title: Como remover o seu dispositivo Android do Intune | Documentos da Microsoft
description: Remova o seu dispositivo Android do Portal da Empresa Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f40aab26-7613-48cc-a74e-de83df9465a4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0715cce163d999ef0c978f9c085ce9df10b5155a
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881683"
---
# <a name="unenroll-your-android-device-from-management"></a>Anular a inscrição do seu dispositivo Android na gestão  

Remova um dispositivo Android inscrito para que deixe de ser gerido pela sua organização. Este artigo descreve como remover o dispositivo da aplicação Portal da Empresa. Depois de remover o dispositivo:  

* O dispositivo perde o acesso aos dados e aos recursos protegidos da sua organização.
* O dispositivo deixa de ser apresentado no Portal da Empresa.
* Não é possível instalar aplicações no Portal da Empresa.
* As definições alteradas no seu dispositivo quando o adicionou (por exemplo, a desativação da câmara ou o comprimento necessário específico de uma palavra-passe) deixam de ser aplicáveis.  

> [!NOTE]
> Não pode desinscrever ou remover o seu dispositivo corporativo da aplicação Microsoft Intune. O dispositivo foi matriculado durante a configuração inicial do dispositivo e deve ser matriculado para aceder aos recursos da sua organização.  

1. No Portal da Empresa, no canto superior direito, toque nos três pontos verticais. É aberto o menu de ação.

   ![Uma imagem da aplicação Portal da Empresa Android, com o menu de ação aberto no canto superior direito. A nova opção “Remover Portal da Empresa” está disponível como a terceira opção, abaixo de “O Meu Perfil” e “Definições” e acima de “Termos e Condições”, “Ajuda e Comentários” e “Acerca de”.](./media/android_remove_cp_menu_action_after_1705.png)

2. Toque em **Remover Portal da Empresa**.  

3. É apresentada uma mensagem com informações sobre o que acontece depois de anular a inscrição do seu dispositivo. Toque em **OK** para confirmar que quer remover o dispositivo do Portal da Empresa.

   ![Uma imagem da confirmação disponível após a seleção da nova opção "remover o portal da empresa" do menu de ação.](./media/android_remove_cp_menu_confirmation_after_1705.png)

## <a name="remove-data-collected-by-the-company-portal-app"></a>Remover os dados recolhidos pela app Portal da Empresa  

Para remover todos os dados que a aplicação Portal da Empresa para Android armazena no seu dispositivo:

- Limpar os dados da aplicação tocando **em Aplicações**  >  **[ nome da*app*]** Dados  >  **claros**.
- Elimine a seguinte pasta: \storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal.

## <a name="uninstall-the-company-portal-app"></a>Desinstalar a aplicação Portal da Empresa

O Portal da Empresa é uma aplicação de gestão de dispositivos. Não pode ser desinstalado até desinstalar o seu dispositivo da sua gestão. Depois de concluir esse procedimento, toque sem soltar no ícone da aplicação Portal da Empresa, até surgir **Desinstalar**. Toque em **Desinstalar** para remover a aplicação do seu dispositivo.  

Em alternativa, toque em **Definições**  >  **Apps**  >  **Portal empresa**  >  **Desinstalar**.  

### <a name="remove-the-company-portal-app-as-a-device-administrator"></a>Remova a aplicação Portal da Empresa como administrador de dispositivos

Como último recurso, pode desinstalar a aplicação a partir do seu dispositivo como administrador de dispositivos.  

Se tiver um dispositivo da empresa, a sua organização poderá exigir que o Portal da Empresa esteja sempre no seu dispositivo. Se desinstalar, poderá perder acesso a recursos protegidos da empresa, tais como e-mail, apps, Wi-Fi ou VPN, até que a aplicação seja reinstalada. Para obter mais informações sobre a instalação, atualização ou remoção de aplicações necessárias, consulte [adicionar aplicações ao Microsoft Intune](/intune/apps/apps-add#apps-that-are-added-automatically-by-intune).

Aqui está como desativar o Portal da Empresa como administrador de dispositivos. Os nomes reais de cada definição podem variar no seu dispositivo Android.  

**Opção 1:**  

1. Selecione **Definições**de  >  **segurança**  >  **adicionais**  >  **Conselhos de**Segurança Administradores .  
2. Limpe a seleção do Portal da **Empresa.**  

**Opção 2**:

1. Selecione **Definições**  >  **Bloquear ecrã e segurança**  >  **Outras definições**de segurança  >  **Aplicações de administração**do dispositivo .
2. Limpe a seleção do Portal da **Empresa.**

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
