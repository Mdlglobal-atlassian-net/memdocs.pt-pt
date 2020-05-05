---
title: Inscreva o seu Mac com o Portal da Empresa Intune [ Microsoft Docs
description: Aprenda a inscrever o seu Mac em Intune com a aplicação Portal da Empresa.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a069a70077a2b6b1b484bb8a88960c314488cc70
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075919"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Inscreva o seu dispositivo macOS utilizando a app Portal da Empresa  

Inscreva o seu dispositivo macOS na aplicação Intune Company Portal para obter acesso seguro ao seu trabalho ou e-mail escolar, ficheiros e aplicações.

As organizações normalmente exigem que você inscreva o seu dispositivo antes de ter acesso a dados proprietários. Depois de o seu dispositivo estar matriculado, torna-se *gerido*. A sua organização pode atribuir políticas e aplicações ao dispositivo através de um fornecedor de gestão de dispositivos móveis (MDM), como o Intune. Para obter acesso contínuo a informações laborais ou escolares no seu dispositivo, tem de configurar o seu dispositivo para corresponder às definições políticas da sua organização.  

Este artigo descreve como usar a aplicação Portal da Empresa para o macOS para se inscrever, configurar e manter o seu dispositivo para que cumpra os requisitos da sua organização.  


## <a name="what-to-expect-from-the-company-portal-app"></a>O que esperar da aplicação Portal da Empresa

Durante a configuração inicial, a aplicação Portal da Empresa requer que você assine e autentica-se com a sua organização. O Portal da Empresa informa-o então de quaisquer configurações do dispositivo que necessite de configurar para satisfazer os requisitos da sua organização. Muitas vezes, por exemplo, as organizações definem requisitos de palavra-passe com limites de carateres mínimos e máximos que terá de cumprir.    

Depois de inscrever o seu dispositivo, o Portal da Empresa certificar-se-á sempre de que o seu dispositivo está protegido de acordo com os requisitos da sua organização. Por exemplo, se instalar uma aplicação a partir de uma fonte não confiável, o Portal da Empresa irá alertá-lo e poderá restringir o acesso aos recursos da sua organização. Políticas de proteção de aplicações como esta são comuns. Para recuperar o acesso, provavelmente precisará de desinstalar a aplicação não confiável. 

Se após a inscrição a sua organização impor um novo requisito de segurança, como a autenticação de vários fatores, o Portal da Empresa irá notificá-lo. Terá a oportunidade de ajustar as suas definições para que possa continuar a trabalhar a partir do seu dispositivo.  

Para saber mais sobre a inscrição, veja [o que acontece quando instalo a app Portal da Empresa e inscrevi o meu dispositivo?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md)  

## <a name="get-your-macos-device-managed"></a>Gerencie o seu dispositivo macOS  
Utilize os seguintes passos para inscrever o seu dispositivo macOS na sua organização. O seu dispositivo deve estar a funcionar com o macOS 10.12 ou mais tarde.   

> [!NOTE]
> Ao longo deste processo, poderá ser solicitado a permitir que o Portal da Empresa utilize informações confidenciais armazenadas no seu porta-chaves. Estas solicitações fazem parte da segurança da Apple. Quando receber o pedido, escreva a sua palavra-passe de porta-chaves de login e selecione **Sempre permita**. Se premir **Enter** ou **Return** no teclado, o pedido irá, em vez disso, selecionar **Permitir**, o que pode resultar em indicações adicionais.  

### <a name="install-company-portal-app"></a>Instalar app Portal da Empresa  
1. Vai para [o Matricular o Meu Mac.](https://go.microsoft.com/fwlink/?linkid=853070)  
2. O ficheiro instalador do Portal da Empresa .pkg será descarregado. Abra o instalador e continue pelos degraus. 
3. Concordo com o acordo de licença de software. 
4. Introduza a palavra-passe do seu dispositivo ou digital registado para instalar o software.  
5. Portal da Empresa Aberta. 

> [!IMPORTANT]
> O Microsoft AutoUpdate poderá estar aberto para atualizar o seu software microsoft. Depois de todas as atualizações serem instaladas, abra a aplicação Portal da Empresa. Para a melhor experiência de configuração, instale as versões mais recentes do Microsoft AutoUpdate e do Portal da Empresa.  


### <a name="enroll-your-mac"></a>Inscreva o seu Mac  


1. Inscreva-se no Portal da Empresa com o seu trabalho ou conta escolar.  
2. Quando a aplicação abrir, selecione **Iniciar**.  
3. Reveja o que a sua organização pode ou não ver no seu dispositivo matriculado. Em seguida, selecione **Continuar**.
4.  Se for solicitado, introduza a palavra-passe do seu dispositivo no ecrã de perfil de **gestão Instalar.**

    ![Exemplo de screenshot do Portal da Empresa, Instale o ecrã de perfil de gestão, realçando o pedido de senha.](./media/install-management-profile-macos-1912.PNG)   
5. No ecrã de gestão do **dispositivo Confirmar,** selecione **Preferências**do Sistema Aberto .  

    ![Exemplo de screenshot do ecrã de gestão do dispositivo Confirm, destacando o botão "Preferências do Sistema Aberto".](./media/confirm-device-management-macos-1912.PNG)  
6. As preferências do sistema do seu dispositivo serão abertas. Selecione o Perfil de **Gestão** da lista de perfis do dispositivo e, em seguida, selecione **Aprovar** > **Approve**.  
    ![Exemplo de screenshot das preferências do sistema, ecrã de perfil de gestão, realçando o botão "Aprovar".](./media/management-profile-approve-macos-1912.PNG)   
1. Volte ao Portal da Empresa e selecione **Continuar**.    
2. A sua organização poderá necessitar de atualizar as definições do seu dispositivo. Quando terminar de atualizar as definições, selecione **'Verificar definições**' .  

    ![Exemplo de screenshot do Portal da Empresa, ecrã de definições de dispositivo de atualização, realçando o botão "Verificar definições".](./media/update-settings-mac-1911.PNG)  
9. Quando a configuração estiver concluída, selecione **Done**.  


 ## <a name="troubleshooting-and-feedback"></a>Resolução de problemas e feedback   

Se tiver problemas durante a inscrição, vá **ao Help** > **Send Diagnostic Report** para reportar o problema aos desenvolvedores de aplicações da Microsoft. Esta informação é usada para ajudar a melhorar a aplicação. Também usarão esta informação para ajudar a resolver o problema se a sua pessoa de suporte de TI os pedir ajuda.  

Depois de reportar o problema à Microsoft, pode enviar os detalhes da sua experiência para a sua pessoa de suporte de TI. Selecione **Detalhes do e-mail**. Digite o que experimentou no corpo do e-mail. Para encontrar o endereço de e-mail da pessoa de suporte, dirija-se à aplicação portal da empresa > **Contact**. Ou consulte o site do [Portal da Empresa.](https://go.microsoft.com/fwlink/?linkid=2010980)  
 

Além disso, a equipa do Portal da Microsoft Intune Company adoraria ouvir o seu feedback. Vá para **ajudar a** > **Enviar Feedback** para partilhar os seus pensamentos e ideias.  

## <a name="unverified-profiles"></a>Perfis não verificados  
Quando visualiza os perfis instalados de gestão de dispositivos móveis (MDM) nos**Perfis**de **Preferências** > do Sistema, alguns perfis podem mostrar um estado não verificado. Desde que o perfil de gestão mostre um estatuto verificado, não precisa de se preocupar.  

O perfil de gestão é o que define a ligação de canal MDM. Enquanto o perfil de gestão for verificado, quaisquer outros perfis entregues à máquina através desse canal herdam os traços de segurança do perfil de gestão.  

## <a name="updating-the-company-portal-app"></a>Atualizar a aplicação Portal da Empresa

A atualização da aplicação Portal da Empresa é feita da mesma forma que qualquer outra aplicação do Office, através do Microsoft AutoUpdate para o macOS. Saiba mais sobre a atualização de [aplicações da Microsoft para o macOS.](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1)  

## <a name="next-steps"></a>Passos Seguintes  
Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  


