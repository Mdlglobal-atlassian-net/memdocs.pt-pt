---
title: Inscreva dispositivo Android com Intune Company Portal [ Intune Company Portal ] Microsoft Docs
description: Descreve como inscrever um dispositivo Android com o Intune Company Portal
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/01/2020
ms.topic: article
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
ms.openlocfilehash: 0c9bf96188e27afeaf66e7b2897f8cda19f9df37
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551658"
---
# <a name="enroll-your-device-with-company-portal"></a>Inscreva o seu dispositivo com o Portal da Empresa  
Inscreva o seu dispositivo Android pessoal ou corporativo para obter acesso seguro a e-mails, aplicações e dados da empresa. O Portal da Empresa suporta dispositivos Android, incluindo samsung Knox, com o Android 4.4 e mais tarde.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> A Samsung Knox é um tipo de segurança que certos dispositivos da Samsung usam para proteção adicional fora do que o Android nativo fornece. Para verificar se tem um dispositivo Samsung Knox, > ir para **Definições** > **Sobre o dispositivo**. Se não vir a **versão Knox** listada lá, tem um dispositivo Android nativo.

## <a name="enroll-device"></a>Inscrever o dispositivo  
Certifique-se de instalar a aplicação Intune Company Portal [a partir do Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Consulte a [aplicação Install Company Portal na China continental](install-company-portal-android-china.md) para obter uma lista de lojas que oferecem a app na China continental.    

Durante a inscrição, pode ser-lhe pedido que escolha uma categoria que melhor descreva como utiliza o seu dispositivo. O suporte da sua empresa utiliza a sua resposta para verificar as aplicações a que tem acesso.  

1. Abra a aplicação Portal da Empresa e inicie sessão com a sua conta escolar ou profissional.  

2. Se for solicitado que aceite os termos e condições da sua organização, toque em **ACCEPT ALL**.  

   ![Imagem de exemplo do Portal da Empresa, ecrã de Termos, destacando o botão "Aceitar tudo".](./media/accept-terms-1911.png)  


3. Reveja o que a sua organização pode ou não ver. Em seguida, toque **EM CONTINUAR**.


    ![Exemplo da imagem do Portal da Empresa, preocupamo-nos com o seu ecrã de privacidade, destacando o botão Continuar.](./media/android-privacy-screen-1911.png)  
4. Reveja o que esperar nos próximos passos. Em seguida, toque **EM NEXT**.  

    ![Exemplo da imagem do Portal da Empresa, Qual é o próximo ecrã, destacando o botão Seguinte.](./media/android-whats-next-1911.png)  


5. Dependendo da sua versão do Android, poderá ser solicitado que permita o acesso a certas partes do seu dispositivo. Estas solicitações são exigidas pela Google e não são controladas pela Microsoft.  

    Toque **em permitir** as seguintes permissões:  
    * **Permitir que o Portal da Empresa efaça e gere chamadas telefónicas**: Esta permissão permite ao seu dispositivo partilhar o seu número de identidade de equipamento de estação móvel internacional (IMEI) com a Intune, fornecedora de gestão de dispositivos da sua organização. É seguro permitir esta permissão. A Microsoft nunca fará ou gerirá chamadas telefónicas.  
    * **Permitir que o Portal da Empresa aceda aos seus contactos**: Esta permissão permite que a aplicação Portal da Empresa crie, utilize e gere a sua conta de trabalho.  É seguro permitir esta permissão. A Microsoft nunca acederá aos seus contactos. 

    Se negar permissão, será solicitado novamente da próxima vez que assinar no Portal da Empresa. Para desligar estas mensagens, selecione **Nunca mais pergunte**. Para gerir permissões de aplicações, vá à aplicação Definições > **Apps** > **Company Portal** > **Permissions** > **Phone**.  

6. Ativar a aplicação de administração do dispositivo. 

    O Portal da Empresa necessita de permissões de administrador de dispositivos para gerir de forma segura o seu dispositivo. Ativar a aplicação permite à sua organização identificar possíveis problemas de segurança, tais como tentativas repetidas falhadas de desbloquear o seu dispositivo e responder adequadamente.  

    ![Exemplo da imagem do ecrã do administrador do dispositivo Activate, realçando o botão de ativação.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> A Microsoft não controla as mensagens neste ecrã. Entendemos que a sua frase pode parecer um pouco drástica. O Portal da Empresa não pode especificar quais as restrições e acessos relevantes para a sua organização. Se tiver dúvidas sobre como a sua organização utiliza a aplicação, contacte a pessoa de suporte de TI. Vá ao site do Portal da [Empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para encontrar os contactos da sua organização.  


7. O seu dispositivo começa a matricular-se. Se estiver a usar um dispositivo Samsung Knox, será solicitado a rever e reconhecer primeiro a política de privacidade do Elm Agent.   

    ![Imagem de exemplo do ecrã de política de privacidade Samsung Knox que aparece durante a inscrição.](./media/and-enroll-7-knox-privacy-policy.png)  

8. No ecrã de Configuração de Acesso da **Empresa,** verifique se o seu dispositivo está matriculado. Em seguida, toque **EM CONTINUAR**.  

    ![Exemplo de imagem do Portal da Empresa, ecrã de Configuração de Acesso da Empresa, mostrando que o Get o seu dispositivo gerido está completo.](./media/update-settings-1911.png)  

9. A sua organização poderá necessitar de atualizar as definições do seu dispositivo. Toque no **RESOLVE** para ajustar uma regulação. Quando terminar de atualizar as definições, toque em **CONTINUAR**.  

   ![Exemplo da imagem do Portal da Empresa, definições do dispositivo de atualização, realçando os botões Resolve e Continue.](./media/resolve-settings-1911.png)  

10. Quando a configuração estiver concluída, toque em **DONE**.    

    ![Imagem de exemplo do Portal da Empresa, ecrã de configuração de acesso da empresa, mostrando configuração completa e realce botão Feito.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Passos seguintes  

Antes de tentar instalar uma escola ou uma aplicação de trabalho, vá à **Definições** > **de Segurança**e ligue **fontes desconhecidas.** Se não ligar esta opção, verá a seguinte mensagem quando tentar instalar uma aplicação: "Instale bloqueado. Por motivos de segurança, o dispositivo está definido para bloquear as instalações de aplicações obtidas a partir de origens desconhecidas." Pode tocar em **Definições** na mensagem para ir diretamente a **fontes desconhecidas**.  

> [!Note]
> Se a sua organização utilizar software de gestão de despesas de telecomunicações, terá de completar alguns passos adicionais antes de o dispositivo ficar totalmente inscrito. Saiba mais [aqui](enroll-your-device-with-telecom-expense-management-android.md).

Se tiver um erro enquanto tenta inscrever o seu dispositivo em Intune, pode [enviar um e-mail](send-logs-to-your-it-admin-by-email-android.md)para o suporte da sua empresa.  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  