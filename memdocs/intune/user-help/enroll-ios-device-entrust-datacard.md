---
title: Inscreva o dispositivo iOS ou iPadOS com O Portal da Empresa Intune e Confie o Cartão de Dados
description: Inscreva um dispositivo iOS ou iPadOS e instale autenticação credencial derivada com cartão de dados de confia.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 763d67c393eede1920f356e54d6ab422bc75a480
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328221"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Configurar dispositivo iOS ou iPadOS com portal da empresa e cartão de dados de confiar

Inscreva o seu dispositivo na aplicação Intune Company Portal para obter acesso seguro e móvel aos e-mails, ficheiros e aplicações da sua organização. Depois de o seu dispositivo estar matriculado, torna-se *gerido*. A sua organização pode atribuir políticas e aplicações ao dispositivo através de um fornecedor de gestão de dispositivos móveis (MDM), como o Intune.  

Durante a inscrição, também irá instalar uma credencial derivada no seu dispositivo. A sua organização poderá exigir que utilize a credencial derivada como método de autenticação ao aceder a recursos, ou para a assinatura e encriptação de e-mails. 

É provável que precise de configurar uma credencial derivada se utilizar um cartão inteligente para:  

* Inscreva-se em apps escolares ou de trabalho, Wi-Fi e redes privadas virtuais (VPN)
* Assinar e encriptar e-mails escolares ou de trabalho usando certificados S/MIME  

Neste artigo, irá:  

   * Inscreva um dispositivo iOS ou iPadOS móvel com o Intune Company Portal.  
   * Obtenha uma credencial derivada do fornecedor credencial derivado da sua organização, [Entrust Datacard](https://www.entrustdatacard.com/).  

### <a name="what-are-derived-credentials"></a>O que são credenciais derivadas?  
Uma credencial derivada é um certificado derivado das credenciais do seu cartão inteligente e instalado no seu dispositivo. Concede-lhe acesso remoto a recursos de trabalho, ao mesmo tempo que impede que utilizadores não autorizados acedam a informações sensíveis.  

As credenciais derivadas são utilizadas para: 
* Autenticar alunos e funcionários que se inscrevam na escola ou aplicações de trabalho, Wi-Fi e VPN
* Assinar e encriptar e-mails escolares ou de trabalho com certificados S/MIME

As credenciais derivadas são uma implementação das diretrizes do Instituto Nacional de Normalização e Tecnologia (NIST) para credenciais de Verificação de Identidade Pessoal Derivada (PIV) como parte da Publicação Especial (SP) 800-157.  

## <a name="prerequisites"></a>Pré-requisitos

 Para completar a inscrição, deve ter:

* Sua escola ou cartão inteligente fornecido pelo trabalho
* Acesso a um computador ou quiosque onde pode iniciar sessão com o seu cartão inteligente
* O seu dispositivo móvel
* A aplicação Intune Company Portal para iOS e iPadOS instalada no seu dispositivo  


## <a name="enroll-device"></a>Dispositivo de inscrição  
1. Abra a aplicação Portal da Empresa para iOS/iPadOS no seu dispositivo móvel e inscreva-se na sua conta de trabalho.  

2. Escreva o código no ecrã.  

    ![Imagem de exemplo da aplicação Do Portal da Empresa com mensagem e código no ecrã.](./media/copy-code-intercede.png)   

3. Mude para o seu dispositivo inteligente ativado pelo cartão e vá para https://microsoft.com/devicelogin. 
4. Introduza o código que escreveu anteriormente.  

    ![Exemplo de screenshot do site do Portal da Empresa "Introduzir código".](./media/enter-code-intercede.png)   

5. Insira o seu cartão inteligente para iniciar sessão.   
6. Volte à aplicação Portal da Empresa no seu dispositivo móvel e siga as instruções no ecrã para inscrever o seu dispositivo.  
7. Após a inscrição estar concluída, o Portal da Empresa irá notificá-lo para configurar o seu cartão inteligente. Toque na notificação. Se não receber uma notificação, consulte o seu e-mail.   

    ![Exemplo de screenshot da notificação push do Portal da Empresa no ecrã principal do dispositivo.](./media/action-required-in-app-intercede.png)  

8. No ecrã de acesso ao **cartão inteligente configuração:**   
    a. Toque no link para as instruções de configuração da sua organização. Se a sua organização não fornecer instruções adicionais, será enviado para este artigo.  
    b. Toque **começar**.  

    ![Exemplo de screenshot do Portal da Empresa Configurar ecrã de acesso a cartões inteligentes móveis.](./media/smart-card-info-intercede.png)

9. Mude para o seu dispositivo inteligente ativado por cartões e abra o IdentityGuard. 
10. Encontre a área de inscrição de credencial inteligente e selecione o botão de iniciar sessão.  
11. Quando lhe for solicitado que selecione um certificado, escolha as credenciais do seu cartão inteligente. Em seguida, selecione **OK**. 
12. Insira o seu PIN de cartão inteligente.  
13. Será convidado a escolher entre uma lista de ações. Selecione aquele que lhe permite inscrever-se para uma credencial móvel derivada. O link ou botão pode dizer **que gostaria de me inscrever para uma credencial de cartão inteligente móvel derivada.**  
14. Selecione que descarregou e instalou com sucesso a aplicação inteligente ativada pela credencial. Em seguida, continue para o próximo ecrã.   
15. Introduza informações sobre a credencial do seu cartão inteligente derivado.  
    a. Para o nome de identidade, insira qualquer nome, como *O Crédito Derivado da Entrust .*  
    b. No menu suspenso, **selecione Entrust IdentityGudard Mobile Smart Credential**.  
    c. Continue para o próximo ecrã. Verá um código QR com uma senha numérica.  

16. Volte ao seu dispositivo móvel. No Portal da Empresa > Obtenha o ecrã **de código QR,** toque **em Continuar**. 

    ![Exemplo de screenshot do portal da empresa Obter ecrã de código QR.](./media/get-qr-code-intercede.png)  
17. Toque na câmara de **utilização** > **OK**.  

    ![Exemplo de imagem de um pedido do Portal da Empresa, pedindo permissão para permitir o acesso à câmara.](./media/allow-cp-camera-access-intercede.png)  
18. Escaneie a imagem do código QR que está no seu dispositivo inteligente ativado pelo cartão.  
19. Introduza a palavra-passe numérica que aparece sob o código QR.  

    ![Exemplo de screenshot do ecrã exigido pelo Portal da Empresa, introduza o campo de palavra-passe.](./media/enter-password-derived-credentials.png)   

20. Aguarde que o Portal da Empresa termine de configurar o seu dispositivo.  


## <a name="next-steps"></a>Próximos passos  
Após a inscrição estar concluída, terá acesso a recursos de trabalho, como e-mail, Wi-Fi e quaisquer aplicações que a sua organização disponibilize. Para mais informações sobre como obter, procurar, instalar e desinstalar aplicações no Portal da Empresa ver:

* [Gerir aplicações a partir do site do Portal da Empresa](manage-apps-cpweb.md)  
* [Utilizar aplicações geridas no dispositivo](use-managed-apps-on-your-device-ios.md)  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [Web site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
