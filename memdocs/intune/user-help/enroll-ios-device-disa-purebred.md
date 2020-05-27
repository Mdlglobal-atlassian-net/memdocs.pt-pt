---
title: Inscreva dispositivo iOS ou iPadOS com Intune Company Portal e DISA Purebred
description: Saiba como inscrever um dispositivo iOS ou iPadOS e configurar a autenticação credencial derivada com DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
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
ms.openlocfilehash: 50330bbdc61eeeada022c44f4d1f2f68b31f19a4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881546"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Configurar dispositivo iOS ou iPadOS com portal da empresa e DISA Purebred  

Inscreva o seu dispositivo na aplicação Intune Company Portal para obter acesso seguro e móvel aos e-mails, ficheiros e aplicações da sua organização. Depois de o seu dispositivo estar matriculado, torna-se *gerido*. A sua organização pode atribuir políticas e aplicações ao dispositivo através de um fornecedor de gestão de dispositivos móveis (MDM), como o Intune.  

Durante a inscrição, também irá instalar uma credencial derivada no seu dispositivo. A sua organização poderá exigir que utilize a credencial derivada como método de autenticação ao aceder a recursos, ou para a assinatura e encriptação de e-mails. 

É provável que precise de configurar uma credencial derivada se utilizar um cartão inteligente para:

* Inscreva-se em apps escolares ou de trabalho, Wi-Fi e redes privadas virtuais (VPN)
* Assinar e encriptar e-mails escolares ou de trabalho usando certificados S/MIME  

Neste artigo, vai:  

   * Inscreva um dispositivo iOS ou iPadOS móvel com o Intune Company Portal.  
   * Obtenha uma credencial derivada do fornecedor credencial derivado da sua organização, DISA Purebred: https: \/ /cyber.mil/pki-pke/purebred/.  

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
* O seu dispositivo móvel
* A aplicação Intune Company Portal para iOS e iPadOS instalada no seu dispositivo   

Também terá de contactar um agente ou representante da Purebred durante a instalação.      

## <a name="enroll-device"></a>Inscrever o dispositivo  
1. Abra a aplicação Portal da Empresa para iOS/iPadOS no seu dispositivo móvel e inscreva-se na sua conta de trabalho.  

2. Escreva o código no ecrã.  

    ![Imagem de exemplo da aplicação Do Portal da Empresa com mensagem e código no ecrã.](./media/copy-code-intercede.png)  
3. Mude para o seu dispositivo inteligente ativado pelo cartão e vá para https://microsoft.com/devicelogin . 
4. Introduza o código que escreveu anteriormente.  

    ![Exemplo de screenshot do site do Portal da Empresa "Introduzir código".](./media/enter-code-intercede.png)   

5. Insira o seu cartão inteligente para iniciar sessão.  
6. Volte à aplicação Portal da Empresa no seu dispositivo móvel e siga as instruções no ecrã para inscrever o seu dispositivo.  
7. Após a inscrição estar concluída, o Portal da Empresa irá notificá-lo para configurar o seu cartão inteligente. Toque na notificação. Se não receber uma notificação, consulte o seu e-mail.   

    ![Exemplo de screenshot da notificação push do Portal da Empresa no ecrã principal do dispositivo.](./media/action-required-in-app-intercede.png)  
8. No ecrã de acesso ao **cartão inteligente configuração:**  
    a. Toque no link para as instruções de configuração da sua organização. Se a sua organização não fornecer instruções adicionais, será enviado para este artigo.  
    b. Clique **em Abrir** para abrir a app Purebred.  

    ![Exemplo de screenshot do Portal da Empresa Configurar ecrã de acesso a cartões inteligentes móveis.](./media/smart-card-open-disa-purebred.png)  
9. Quando solicitado para permitir que o Portal da Empresa abra a aplicação Purebred Registration, **selecione Open**.   

    ![Exemplo de screenshot do Portal da Empresa solicita-se a abertura da app DISA Purebred.](./media/open-app-prompt-disa-purbred.png)  
10. Quando a aplicação funcionar, trabalhe com o agente Purebred da sua organização para configurar e descarregar o perfil de configuração pré-inscrição purebred.   
11. Aceda à aplicação Definições > **General**  >  **Perfis Gerais & Gestão de Dispositivos**  >  **Instalar perfil** e tocar na **instalação**.  
12. Introduza a sua senha de dispositivo.  
13. Instale o perfil. Pode ser necessário tocar para **instalar** mais de uma vez para iniciar a instalação. 
14. Volte à aplicação Purebred Registration. Siga as instruções do seu agente Purebred para continuar.  
 
15. Depois de descarregar o perfil de configuração, aceda à aplicação Definições > Perfis **Gerais**& Perfil de Instalação de  >  **Dispositivos**  >  **Install Profile** e toque na **instalação**.   
16.  Introduza a sua senha de dispositivo.
17. Instale o perfil. Pode ser necessário tocar para **instalar** mais de uma vez para iniciar a instalação. 
18. Depois de concluída a instalação, volte à aplicação Portal da Empresa.  
19.  No ecrã de acesso ao **cartão inteligente Configuração,** toque em **Continuar**.  

20. A partir do ecrã dos **certificados de importação,** você vai recuperar e importar a credencial derivada que obteve da DISA Purebred.  

    a. Toque **em Continuar**.   

    ![Exemplo de screenshot do ecrã de certificados de importação do Portal da Empresa.](./media/import-certificate-disa-purebred.png)  
    b. Vá ao iCloud Drive **Procurar**  >  **locais** e toque **em Mais Localizações**.  

    ![Exemplo de screenshot do iCloud Drive, menu De navegação destacando a opção Mais Localizações.](./media/icloud-drive-more-locations.png)  
    c. Toque no interruptor para ativar a corrente de **tecla purebred**.  

    ![Exemplo de screenshot do iCloud Drive, vista de navegação, realçando que o interruptor purebred Key Chain está ativado.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Toque **no Pacote Credencial Purebred**.  

    ![Exemplo de screenshot de um ecrã iOS com uma opção selectível Purebred Credential Package.](./media/purebred-credential-package.png)  
    f. Aparece uma lista de certificados. Selecione um e, em seguida, toque na **tecla Import**.  

    ![Exemplo de screenshot de uma lista de certificados selecionáveis, com um já selecionado.](./media/import-purebred-keychain.png) 
21. Volte à aplicação Portal da Empresa e aguarde que o Portal da Empresa termine a configuração do seu dispositivo.   

## <a name="next-steps"></a>Passos seguintes  
Após a inscrição estar concluída, terá acesso a recursos de trabalho, como e-mail, Wi-Fi e quaisquer aplicações que a sua organização disponibilize. Para mais informações sobre como obter, procurar, instalar e desinstalar aplicações no Portal da Empresa ver:

* [Gerir aplicações a partir do site do Portal da Empresa](manage-apps-cpweb.md)  
* [Utilizar aplicações geridas no dispositivo](use-managed-apps-on-your-device-ios.md)  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
