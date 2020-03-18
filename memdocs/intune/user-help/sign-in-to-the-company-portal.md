---
title: Como iniciar sessão na aplicação Portal da Empresa | Documentos da Microsoft
description: Saiba como iniciar sessão na aplicação Portal da Empresa em várias plataformas.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79324321"
---
# <a name="sign-in-to-company-portal"></a>Inscreva-se no Portal da Empresa  

Existem três formas de iniciar sessão na aplicação Portal da Empresa:

* Inscreva-se com o seu endereço de e-mail de trabalho e senha.  
* Inscreva-se com autenticação baseada em certificado.  
* Inscreva-se noutro dispositivo.    


## <a name="sign-in-with-your-email-address-and-password"></a>Inscreva-se com o seu endereço de e-mail e senha
Os seguintes passos mostram imagens do Portal da Empresa para iOS.  

1. Abra a aplicação no seu dispositivo e toque em **Iniciar sessão .**  

   ![Exemplo de imagem da página de inscrição do Portal da Empresa.](./media/intune-ios-cp-signin-1908.png)


2. Introduza a sua **Conta escolar ou profissional** e toque em **Seguinte**.

   ![É pedido ao utilizador que indique apenas o endereço de e-mail, em vez do e-mail e palavra-passe no mesmo ecrã.](./media/cp_ios_aad_signin_after_1804_002.png)

3. Introduza a sua palavra-passe e toque em **Iniciar Sessão**.

   ![É pedido ao utilizador que indique a palavra-passe depois de ter sido aceite o endereço de e-mail.](./media/cp_ios_aad_signin_after_1804_003.png)

4. A aplicação verificará as suas credenciais. Quando feito, pode aceder aos recursos da sua organização e instalar aplicações disponíveis.  

   ![Depois de passar pelo processo de autenticação, a aplicação do Portal da Empresa entra, mostra uma barra de carregamento.](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>Inscreva-se com autenticação baseada em certificado
Só verá esta opção de início de sessão se a sua organização permitir a autenticação baseada em certificados e tiver um certificado disponível para usar.  

1. Abra a aplicação Portal da Empresa no dispositivo.  

2. Introduza a sua **Conta escolar ou profissional**.  

3. Toque na ligação **Iniciar sessão com um certificado**.  

4. Toque em **Continuar** para utilizar o certificado.  

## <a name="sign-in-from-another-device"></a>Inscreva-se noutro dispositivo

Se a sua empresa utilizar smartcards para aceder aos seus computadores, é provável que tenha de autenticar ao iniciar sessão a partir de outro dispositivo.  

1. Abra a aplicação Portal da Empresa no dispositivo. Certifique-se de que é o dispositivo que vai usar para aceder aos seus recursos de trabalho.       

1. Selecione **Iniciar sessão noutro dispositivo**.  

   ![A página de sessão do Portal da Empresa solicita ao utilizador o endereço de e-mail.  Mostra o botão "Seguinte" e um link para "Iniciar sessão a partir de outro dispositivo". Além disso, inclui uma ligação para "Não consegue aceder à conta?" Uma ligação na parte inferior direciona para as informações de Privacidade e Cookies da Microsoft.](./media/cp_ios_aad_signin_after_1804_005.png)

2. Receberá um código único e exclusivo para iniciar sessão no Portal da Empresa. Copie o código.

   ![As instruções indicam para ir para a página https://microsoft.com/devicelogin com um código de acesso exclusivo a partir do computador de trabalho e, em seguida, para utilizar o código para iniciar sessão.](./media/cp_ios_aad_signin_after_1804_006.png)

3. No outro dispositivo (o que está a usar para autenticar), abra o seu navegador e vá para [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin). Insira ou colhe o código.  

   ![Uma imagem do browser do utilizador no computador de trabalho em vez da aplicação Portal da Empresa. A página “Início de sessão do dispositivo” apresentada solicita ao utilizador o código que recebeu na aplicação Portal da Empresa.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. Selecione __Continuar__ a permitir que o Portal da Empresa inscrete no seu dispositivo de trabalho.   

   ![O utilizador introduziu o seu código exclusivo no campo e o site “Início de sessão do dispositivo” pediu a confirmação de que o Portal da Empresa do Intune foi a aplicação correta para receber a autorização para iniciar sessão.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. Assim que o código for verificado, pode fechar a janela.  

   ![Uma página de confirmação que indica que o utilizador tem agora sessão iniciada na aplicação Portal da Empresa no seu dispositivo e que esta página pode ser fechada.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. A aplicação Portal da Empresa assina-o no seu dispositivo de trabalho.  

   ![Depois do processo de autenticação, a aplicação Portal da Empresa inicia sessão, apresentando o respetivo processo com uma barra de carregamento.](./media/cp_ios_aad_signin_after_1804_007.png)

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [Web site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
