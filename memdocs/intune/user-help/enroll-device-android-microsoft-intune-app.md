---
title: Inscreva dispositivo corporativo com app Microsoft Intune Microsoft Docs
description: Descreve como inscrever um dispositivo Android corporativo em Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 58af7bfc0cb7521ef73f32322db7bc148492645a
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881678"
---
# <a name="enroll-your-corporate-device-with-the-microsoft-intune-app"></a>Inscreva o seu dispositivo corporativo com a aplicação Microsoft Intune

Inscreva o seu dispositivo Android corporativo para obter acesso seguro a e-mails, aplicações e outros dados da empresa que a sua organização disponibiliza. A aplicação Microsoft Intune suporta dispositivos corporativos que executam o Android 6.0 e mais tarde. Será automaticamente instalado em dispositivos novos e de reset de fábrica durante a inscrição. 

Há quatro maneiras de se inscrever. A sua organização deve informá-lo sobre qual a opção a usar.
 
* Comunicação de Campo Próximo (NFC)  
* Certificado de  
* Código QR   
* Google Zero Touch  

## <a name="enroll-device"></a>Inscrever o dispositivo 
Complete estes passos para configurar e inscrever o seu dispositivo.  

> [!NOTE]
> A versão Android ou fabricante de dispositivos pode exigir que você complete passos adicionais que não estão cobertos neste procedimento. As cores e texto que vê nas imagens também podem parecer diferentes no seu dispositivo.  

1. Ligue o seu novo dispositivo de reset de fábrica.  
2. No ecrã **Bem-vindo**, selecione o seu idioma.   Se tiver sido instruído a inscrever-se com um código QR ou NFC, siga o passo abaixo que corresponda ao método.  
     * NFC: Toque no seu dispositivo apoiado pelo NFC contra um dispositivo programador para se ligar à rede da sua organização. Siga as indicações no ecrã. Quando chegar ao ecrã para os Termos de Serviço do Chrome, continue a pisar 5.  

     * Código QR: Complete os passos na inscrição do [código QR](#qr-code-enrollment).  

     Se foi instruído a usar outro método, continue a passo 3.    

3. Ligue-se ao Wi-Fi e toque em **NEXT**. Siga o passo que corresponde ao seu método de inscrição. 

    * Token: Quando chegar ao ecrã de sessão do Google, complete os passos na inscrição de [Token](#token-enrollment).  
    * Google Zero Touch: Depois de ligar ao Wi-Fi, o seu dispositivo será reconhecido pela sua organização. Continue a passo 4 e siga as instruções no ecrã até que a configuração esteja completa.    
 
       ![Exemplo da imagem do ecrã de termos do Google que vê se está a usar o Google Zero Touch, destacando o botão Accept & Continuar.](./media/google-zero-touch-intune-app-01.png)   
   
4. Reveja os termos do Google. Em seguida, toque em **ACEITAR & CONTINUE**.  

      ![Exemplo da imagem do ecrã de termos do Google, realçando o botão Aceitar & Continuar.](./media/fully-managed-intune-app-04.png)   

6. Reveja os Termos de Serviço do Chrome. Em seguida, toque em **ACEITAR & CONTINUE**.  

   ![Exemplo da imagem do ecrã Chrome Terms of Service, realçando o botão Aceitar & Continuar.](./media/fully-managed-intune-app-06.png)   

7. No sinal nos ecrãs, inscreva-se com o seu trabalho ou conta escolar.   

    a. Insira o seu e-mail e toque **em Next**.      
    b. Insira a sua palavra-passe e toque **em Iniciar sessão**.  

8. Dependendo dos requisitos da sua organização, poderá ser solicitado a atualizar definições, tais como bloqueio de ecrã ou encriptação. Se vir estas indicações, toque em **SET** e siga as instruções no ecrã.  

   ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão set.](./media/fully-managed-intune-app-10.png)   

9. Para instalar aplicações de trabalho no seu dispositivo, toque em **INSTALAR**. Depois de a instalação estar concluída, toque em **NEXT**.  

   ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão Instalar.](./media/fully-managed-intune-app-11.png)   

10. Toque no **START** para abrir a aplicação Microsoft Intune e registar o seu dispositivo. 

    ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão Iniciar.](./media/fully-managed-intune-app-17.png)   

11. Toque **em INICIAR SESSÃO** E, em seguida, toque em **NEXT** para iniciar a inscrição. Quando vir a mensagem de que o registo está completo, toque em **DONE**.  

    ![Exemplo de imagem de Configurar o acesso, registar o ecrã do seu dispositivo, realçando o botão Done.](./media/fully-managed-intune-app-19.png)   

10. Quando vir a mensagem de que o seu dispositivo está pronto, toque em **DONE**.  

    ![Exemplo da imagem de Configurar o ecrã do telefone de trabalho, realçando o botão Done.](./media/fully-managed-intune-app-18.png)   

Se tiver problemas em aceder aos recursos da sua organização, poderá necessitar de atualizar definições adicionais no seu dispositivo. Inscreva-se na aplicação Microsoft Intune para verificar se há atualizações necessárias.   


## <a name="qr-code-enrollment"></a>Inscrição do código QR  
Nesta secção, você vai digitalizar o seu código QR fornecido pela empresa.  Quando terminar, vamos redirecioná-lo de volta para as etapas de inscrição do dispositivo.     
  
1. No ecrã **Welcome,** toque no ecrã cinco vezes para iniciar a configuração do código QR.  

   ![Exemplo da imagem da configuração do dispositivo Ecrã de boas-vindas, realçando instruções para tocar no ecrã.](./media/qr-code-intune-app-01.png)  

2. Siga quaisquer instruções no ecrã para ligar ao Wi-Fi.  
3. Se o seu dispositivo não tiver um scanner de código QR, os ecrãs de configuração mostrarão o progresso à medida que um scanner é instalado. Aguarde pela conclusão da instalação.  
4. Quando solicitado, scaneie o código QR do perfil de inscrição que a sua organização lhe deu.  
5. Volte ao [dispositivo De Inscrição](#enroll-device), passo 4 para continuar a configuração.  

## <a name="token-enrollment"></a>Inscrição em Token  
Nesta secção, você vai inserir o seu símbolo fornecido pela empresa. Quando terminar, vamos redirecioná-lo de volta para as etapas de inscrição do dispositivo.  

1. No ecrã de entrada do Google, no Email ou na cabine **telefónica,** **digite afw#setup**. Toque **em Seguida**. 

   ![Exemplo da imagem do ecrã de entrada do Google, mostrando que "afw#setup" é dactilografado no campo.](./media/token-intune-app-01.png)   

2. Escolha **instalar** para a aplicação Política de **Dispositivos Android.** Continue através da instalação. Dependendo do seu dispositivo, poderá ter de rever e aceitar termos adicionais.    

3. No **ecrã de inscrição deste dispositivo,** selecione **Next**.  

4. Selecione **Introduzir código**.  

5. No ecrã de **código Scan ou introduza,** digite o código que a sua organização lhe deu.  Em seguida, clique em **Seguinte**.  

   ![Imagem de exemplo de Digitalizar ou introduzir ecrã de código, realçando o próximo botão.](./media/token-intune-app-04.png)  

6. Volte ao [dispositivo De Inscrição](#enroll-device), passo 4 para continuar a configuração.  



## <a name="next-steps"></a>Passos seguintes   
Ainda precisa de ajuda? Contacte o suporte da empresa (verifique as informações de contacto no [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980)) ou escreva para a <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">equipa Android da Microsoft</a>.  
