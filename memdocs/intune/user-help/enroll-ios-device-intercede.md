---
title: Inscreva dispositivo iOS ou iPadOS com Intune Company Portal e Intercede
description: Saiba como inscrever um dispositivo iOS ou iPadOS e configurar a autenticação credencial derivada com a Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b83092521f1ab0058d47d599e7fd9c10c2fd6d35
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077772"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Configurar dispositivo iOS ou iPadOS com Portal da Empresa e Intercede

Inscreva o seu dispositivo na aplicação Intune Company Portal para obter acesso seguro e móvel aos e-mails, ficheiros e aplicações da sua organização.  Depois de o seu dispositivo estar matriculado, torna-se *gerido*. A sua organização pode atribuir políticas e aplicações ao dispositivo através de um fornecedor de gestão de dispositivos móveis (MDM), como o Intune.  

Durante a inscrição, também irá instalar uma credencial derivada no seu dispositivo. A sua organização poderá exigir que utilize a credencial derivada como método de autenticação ao aceder a recursos, ou para a assinatura e encriptação de e-mails. 

É provável que precise de configurar uma credencial derivada se utilizar um cartão inteligente para:

* Inscreva-se em apps escolares ou de trabalho, Wi-Fi e redes privadas virtuais (VPN)
* Assinar e encriptar e-mails escolares ou de trabalho usando certificados S/MIME  

Neste artigo, vai:  

* Inscreva um dispositivo iOS ou iPadOS móvel com o Intune Company Portal.  
* Obtenha uma credencial derivada do fornecedor credencial derivado da sua organização, [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>O que são credenciais derivadas?  
Uma credencial derivada é um certificado derivado das credenciais do seu cartão inteligente e instalado no seu dispositivo. Concede-lhe acesso remoto a recursos de trabalho, ao mesmo tempo que impede que utilizadores não autorizados acedam a informações sensíveis.  

As credenciais derivadas são utilizadas para: 
* Autenticar alunos e funcionários que se inscrevam na escola ou aplicações de trabalho, Wi-Fi e VPN
* Assinar e encriptar e-mails escolares ou de trabalho com certificados S/MIME  

As credenciais derivadas são uma implementação das diretrizes do Instituto Nacional de Normalização e Tecnologia (NIST) para credenciais de Verificação de Identidade Pessoal Derivada (PIV) como parte da Publicação Especial (SP) 800-157.  

## <a name="prerequisites"></a>Pré-requisitos

 Para completar a inscrição, deve ter:

* Sua escola ou cartão inteligente fornecido pelo trabalho
* Acesso a um computador ou quiosque de self-service onde pode iniciar sessão com o seu cartão inteligente
* O seu dispositivo móvel
* A aplicação Intune Company Portal para iOS e iPadOS instalada no seu dispositivo


## <a name="enroll-device"></a>Inscrever o dispositivo  
1. Abra a aplicação Portal da Empresa para iOS/iPadOS no seu dispositivo móvel e inscreva-se na sua conta de trabalho.  
2. Escreva o código que aparece no ecrã.  

    ![Imagem de exemplo da aplicação Do Portal da Empresa com mensagem e código no ecrã.](./media/copy-code-intercede.png)  
1. Mude para o seu dispositivo inteligente https://microsoft.com/deviceloginativado pelo cartão e vá para . 

1. Introduza o código que escreveu anteriormente.
 
2. Insira o seu cartão inteligente para iniciar sessão.   

3. Volte à aplicação Portal da Empresa no seu dispositivo móvel e siga as instruções no ecrã para inscrever o seu dispositivo.  
4. Após a inscrição estar concluída, o Portal da Empresa irá notificá-lo para configurar o seu cartão inteligente. Toque na notificação. Se não receber uma notificação, consulte o seu e-mail.   

    ![Exemplo de screenshot da notificação push do Portal da Empresa no ecrã principal do dispositivo.](./media/action-required-in-app-intercede.png)  

5. No ecrã de acesso ao **cartão inteligente configuração:**  
    a. Toque no link para as instruções de configuração da sua organização. Se a sua organização não fornecer instruções adicionais, será enviado para este artigo.  
    b. Toque **começar**.  

    ![Exemplo de screenshot do Portal da Empresa Configurar ecrã de acesso a cartões inteligentes móveis.](./media/smart-card-info-intercede.png)  

6. Mude para o seu dispositivo ou quiosque de self-service e abra a aplicação MyID. Inscreva-se com as suas credenciais de trabalho.  
7. Selecione a opção de solicitar o seu ID. 
8. Quando lhe perguntarem qual o perfil que pretende utilizar, selecione a opção de ativar com uma credencial móvel. Aparece um código QR.  
9. Volte ao seu dispositivo móvel. No Portal da Empresa > obter ecrã **de código QR,** toque **em Continuar**.  

    ![Exemplo de screenshot do portal da empresa Obter ecrã de código QR.](./media/get-qr-code-intercede.png) 
 
10. Toque bem **na câmara** > de utilização **.**  

    ![Exemplo de imagem de um pedido do Portal da Empresa, pedindo permissão para permitir o acesso à câmara.](./media/allow-cp-camera-access-intercede.png)  

11. Escaneie a imagem do código QR que está no seu dispositivo inteligente ativado pelo cartão. 
12. Aguarde que o Portal da Empresa termine de configurar o seu dispositivo.  

## <a name="next-steps"></a>Passos seguintes  
Após a inscrição estar concluída, terá acesso a recursos de trabalho, como e-mail, Wi-Fi e quaisquer aplicações que a sua organização disponibilize. Para mais informações sobre como obter, procurar, instalar e desinstalar aplicações no Portal da Empresa ver:

* [Gerir aplicações a partir do site do Portal da Empresa](manage-apps-cpweb.md)  
* [Utilizar aplicações geridas no dispositivo](use-managed-apps-on-your-device-ios.md)  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
