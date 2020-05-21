---
title: Inscreva dispositivo Android com Intune Company Portal e Intercede
description: Inscreva um dispositivo Android e instale autenticação credencial derivada com a Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: f48fb487df6a1b20e333ee6a2154490a59d220a9
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551951"
---
# <a name="set-up-android-device-with-company-portal-and-intercede"></a>Configurar dispositivo Android com Portal da Empresa e Intercede

Inscreva o seu dispositivo na aplicação Intune Company Portal para obter acesso seguro e móvel aos e-mails, ficheiros e aplicações da sua organização. Depois de o seu dispositivo estar matriculado, torna-se *gerido*. A sua organização pode atribuir políticas e aplicações ao dispositivo através de um fornecedor de gestão de dispositivos móveis (MDM), como o Intune.

Durante a inscrição, também irá instalar uma credencial derivada no seu dispositivo. A sua organização poderá exigir que utilize a credencial derivada como método de autenticação ao aceder a recursos, ou para a assinatura e encriptação de e-mails.

É provável que precise de configurar uma credencial derivada se utilizar um cartão inteligente para:

* Inscreva-se em apps escolares ou de trabalho, Wi-Fi e redes privadas virtuais (VPN)
* Assinar e encriptar e-mails escolares ou de trabalho usando certificados S/MIME

Neste artigo, vai:

* Inscreva um dispositivo Android móvel com o Intune Company Portal.
* Instale o seu cartão inteligente instalando uma credencial derivada do fornecedor de credenciais derivado da sua organização, [intercede](https://www.intercede.com/).  

## <a name="what-are-derived-credentials"></a>O que são credenciais derivadas?

Uma credencial derivada é um certificado derivado das credenciais do seu cartão inteligente e instalado no seu dispositivo. Concede-lhe acesso remoto a recursos de trabalho, ao mesmo tempo que impede que utilizadores não autorizados acedam a informações sensíveis.

As credenciais derivadas são utilizadas para:

* Autenticar alunos e funcionários que se inscrevam na escola ou aplicações de trabalho, Wi-Fi e VPN
* Assinar e encriptar e-mails escolares ou de trabalho com certificados S/MIME

As credenciais derivadas são uma implementação das diretrizes do Instituto Nacional de Normalização e Tecnologia (NIST) para credenciais de Verificação de Identidade Pessoal Derivada (PIV) como parte da Publicação Especial (SP) 800-157.

## <a name="prerequisites"></a>Pré-requisitos

 Para completar a inscrição, deve ter:

* Sua escola ou cartão inteligente fornecido pelo trabalho
* Acesso a um computador ou quiosque onde pode iniciar sessão com o seu cartão inteligente
* Um novo dispositivo de reset de fábrica que executa o Android 7.0 ou mais tarde
* A aplicação Microsoft Intune instalada no seu dispositivo

## <a name="enroll-device"></a>Inscrever o dispositivo  

1. Ligue o seu novo dispositivo de reset de fábrica.  
2. No ecrã **Bem-vindo**, selecione o seu idioma. Se tiver sido instruído a inscrever-se com um código QR ou NFC, siga o passo abaixo que corresponda ao método.  
     * NFC: Toque no seu dispositivo apoiado pelo NFC contra um dispositivo programador para se ligar à rede da sua organização. Siga as indicações no ecrã. Quando chegar ao ecrã para os Termos de Serviço do Chrome, continue a pisar 5.  

     * Código QR: Complete os passos na inscrição do [código QR](#qr-code-enrollment).  

     Se foi instruído a usar outro método, continue a passo 3.    

3. Ligue-se ao Wi-Fi e toque em **NEXT**. Siga o passo que corresponde ao seu método de inscrição. 

    * Token: Quando chegar ao ecrã de sessão do Google, complete os passos na inscrição de [Token](#token-enrollment).  
    * Google Zero Touch: Depois de ligar ao Wi-Fi, o seu dispositivo será reconhecido pela sua organização. Continue a passo 4 e siga as instruções no ecrã até que a configuração esteja completa.    
 
       ![Exemplo da imagem do ecrã de termos do Google que vê se está a usar o Google Zero Touch, destacando o botão Accept & Continuar.](./media/google-zero-touch-intune-app-01.png)   
   
4. Reveja os termos do Google. Em seguida, toque em **ACEITAR & CONTINUE**.  

      ![Exemplo da imagem do ecrã de termos do Google, realçando o botão Aceitar & Continuar.](./media/fully-managed-intune-app-04.png)   

5. Reveja os Termos de Serviço do Chrome. Em seguida, toque em **ACEITAR & CONTINUE**.  

   ![Exemplo da imagem do ecrã Chrome Terms of Service, realçando o botão Aceitar & Continuar.](./media/fully-managed-intune-app-06.png)  

6. No ecrã de entrada, toque nas **opções de iniciar sessão** e, em seguida, **iniciar sessão a partir de outro dispositivo**. 

7. Escreva o código no ecrã.  

8. Mude para o seu dispositivo smart card ativado e vá para o endereço web que está mostrado no seu ecrã. 

9. Introduza o código que escreveu anteriormente.

   > [!div class="mx-imgBorder"]
   > ![Screenshot do site do Portal da Empresa "Introduzir código".](./media/enter-code-intercede.png)

10. Insira o seu cartão inteligente para iniciar sessão.  

11. No ecrã de iniciar sessão, selecione o seu trabalho ou conta escolar. Em seguida, volte a ligar para o seu dispositivo móvel.

12. Dependendo dos requisitos da sua organização, poderá ser solicitado a atualizar definições, tais como bloqueio de ecrã ou encriptação. Se vir estas indicações, toque em **SET** e siga as instruções no ecrã.  

       ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão set.](./media/fully-managed-intune-app-10.png)   

13. Para instalar aplicações de trabalho no seu dispositivo, toque em **INSTALAR**. Depois de a instalação estar concluída, toque em **NEXT**.  

       ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão Instalar.](./media/fully-managed-intune-app-11.png)    

14. Toque no **START** para abrir a aplicação Microsoft Intune. 

    ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão Iniciar.](./media/fully-managed-intune-app-17.png)   
 

15. Volte à aplicação Intune no seu dispositivo móvel e siga as instruções no ecrã até que a inscrição esteja terminada. 

    ![Exemplo de imagem de Configurar o acesso, registar o ecrã do seu dispositivo, realçando o botão Done.](./media/fully-managed-intune-app-19.png)   

16. Continue a configurar a sua secção de [cartões inteligentes](enroll-android-device-intercede.md#set-up-smart-card) neste artigo para terminar a configuração do seu dispositivo.  

### <a name="qr-code-enrollment"></a>Inscrição do código QR  
Nesta secção, você vai digitalizar o seu código QR fornecido pela empresa.  Quando terminar, vamos redirecioná-lo de volta para as etapas de inscrição do dispositivo.     
  
1. No ecrã **Welcome,** toque no ecrã cinco vezes para iniciar a configuração do código QR.  

   ![Exemplo da imagem da configuração do dispositivo Ecrã de boas-vindas, realçando instruções para tocar no ecrã.](./media/qr-code-intune-app-01.png)  

2. Siga quaisquer instruções no ecrã para ligar ao Wi-Fi.  
3. Se o seu dispositivo não tiver um scanner de código QR, os ecrãs de configuração mostrarão o progresso à medida que um scanner é instalado. Aguarde pela conclusão da instalação.  
4. Quando solicitado, scaneie o código QR do perfil de inscrição que a sua organização lhe deu.  
5. Volte ao [dispositivo De Inscrição](#enroll-device), passo 4 para continuar a configuração.  

### <a name="token-enrollment"></a>Inscrição em Token  
Nesta secção, você vai inserir o seu símbolo fornecido pela empresa. Quando terminar, vamos redirecioná-lo de volta para as etapas de inscrição do dispositivo.  

1. No ecrã de entrada do Google, no Email ou na cabine **telefónica,** **digite afw#setup**. Em seguida, toque **em Seguida.** 

   ![Exemplo da imagem do ecrã de entrada do Google, mostrando que "afw#setup" é dactilografado no campo.](./media/token-intune-app-01.png)   

2. Escolha **instalar** para a aplicação Política de **Dispositivos Android.** Continue através da instalação. Dependendo do seu dispositivo, poderá ter de rever e aceitar termos adicionais.    

3. No **ecrã de inscrição deste dispositivo,** selecione **Next**.  

4. Selecione **Introduzir código**.  

5. No ecrã de **código Scan ou introduza,** digite o código que a sua organização lhe deu.  Em seguida, clique em **Seguinte**.  

   ![Imagem de exemplo de Digitalizar ou introduzir ecrã de código, realçando o próximo botão.](./media/token-intune-app-04.png)  

6. Volte ao [dispositivo De Inscrição](#enroll-device), passo 4 para continuar a configuração.

## <a name="set-up-smart-card"></a>Configurar cartão inteligente  

1. Após a inscrição estar concluída, a aplicação Intune irá notificá-lo para configurar o seu cartão inteligente. Toque na notificação. Se não receber uma notificação, consulte o seu e-mail.

   > [!div class="mx-imgBorder"]
   > ![Exemplo de screenshot da notificação push do Portal da Empresa no ecrã principal do dispositivo.](./media/action-required-in-app-android.png)

2. No ecrã **do cartão inteligente Configurar:**

   1. Toque no link para as instruções de configuração da sua organização. Se a sua organização não fornecer instruções adicionais, será enviado para este artigo.

   2. Toque NO **BEGIN**.  

   > [!div class="mx-imgBorder"]
   > ![Exemplo de screenshot do Portal da Empresa Configurar ecrã de acesso a cartões inteligentes móveis.](./media/smart-card-open-entrust-android.png)

3. Mude para o seu dispositivo ou quiosque de self-service e abra a aplicação MyID. Inscreva-se com as suas credenciais de trabalho.

4. Selecione a opção de solicitar o seu ID.

5. Quando lhe perguntarem qual o perfil que pretende utilizar, selecione a opção de ativar com uma credencial móvel. Aparece um código QR.  

6. Volte ao seu dispositivo Android. No Portal da Empresa > obter ecrã **de código QR,** toque em **NEXT**.

    > [!div class="mx-imgBorder"]
    > ![Exemplo de screenshot do portal da empresa Obter ecrã de código QR.](./media/get-qr-code-entrust-android.png)

7. Se for solicitado que permita que a aplicação Intune utilize a sua câmara, toque **em Permitir**.

8. Escaneie a imagem do código QR que está no seu dispositivo inteligente ativado pelo cartão.

9. A aplicação Intune começará a descarregar e instalar os certificados necessários para aceder ao trabalho ou aos recursos escolares. Dependendo da sua ligação à Internet, este processo pode demorar algum tempo. Não feche a aplicação durante este tempo.

    > [!div class="mx-imgBorder"]
    > ![Exemplo de screenshot do ecrã "Descarregamento e instalação de certificados" do Portal da Empresa](./media/install-certificates-entrust-android.png)

10. Uma vez processados todos os certificados, aguarde que a aplicação Intune termine de configurar o seu dispositivo. Saberá que a configuração está completa quando vir o **"You're All set"!** aplicações.

    > [!div class="mx-imgBorder"]
    > ![Exemplo de imagem do ecrã "You're all set"](./media/all-set-android.png)

## <a name="next-steps"></a>Próximos passos

Após a inscrição estar concluída, terá acesso a recursos de trabalho, como e-mail, Wi-Fi e quaisquer aplicações que a sua organização disponibilize. Para mais informações sobre como obter, procure, instale e desinstale aplicações na aplicação Intune ver:

* [Utilizar aplicações geridas no dispositivo](use-managed-apps-on-your-device-android.md)  
* [Gerir aplicações a partir do site do Portal da Empresa](manage-apps-cpweb.md)  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
