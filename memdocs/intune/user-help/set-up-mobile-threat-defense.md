---
title: Instale a Defesa de Ameaças Móveis no seu dispositivo móvel
description: Aprenda a instalar a Mobile Threat Defense no seu dispositivo móvel.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/27/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 676af3373acd399056a0ebdc77c9152442a72101
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182281"
---
# <a name="install-mobile-threat-defense"></a>Instalar defesa de ameaça móvel   

Como parte dos requisitos de segurança da sua organização, poderá ser necessário instalar uma aplicação de fornecedor de aplicação de aplicação de aplicação de aplicação de aplicação de aplicação de aplicação de aplicação de defesa de ameaças móveis (MTD). Este tipo de aplicação deteta e alerta para ameaças no seu dispositivo, tais como aplicações suspeitas, redes ou vulnerabilidades de SO.  

Se não tiver a aplicação MTD necessária, estará impedido de iniciar sessão em aplicações protegidas com o seu trabalho ou conta escolar. Neste artigo, você vai aprender [a instalar uma aplicação MTD](set-up-mobile-threat-defense.md#install-app) para ser desbloqueada.  

Existem uma variedade de aplicações de fornecedores MTD disponíveis para instalar, todas com nomes diferentes. A sua organização vai dizer-lhe qual usar. Se for solicitado a instalar a aplicação, mas não tiver mais instruções ou um link para obter a aplicação, contacte a pessoa de suporte de TI. 


## <a name="information-your-organization-can-see"></a>Informação que a sua organização pode ver   

A sua organização não consegue ver quaisquer dados, tais como textos, e-mails e imagens, nas suas aplicações pessoais. A aplicação MTD reporta informações sobre as suas apps, como nome e versão, à sua organização. A informação real reportada depende do fornecedor MTD que a sua empresa utiliza. A sua organização pode ver:   

* Nome da aplicação  
* Id da aplicação: O nome único que identifica a aplicação no Google Play.  
* Versão de aplicativo e número de versão curta: Os números de lançamento específicos para uma aplicação.  
* Pacote de aplicativos e tamanho dinâmico: A quantidade de espaço que uma aplicação utiliza no seu dispositivo. 


## <a name="install-app"></a>Instalar a aplicação    
Quando iniciar sessão numa aplicação protegida, será automaticamente solicitado a instalar uma aplicação MTD. Siga os passos no ecrã para concluir a instalação. Utilize os passos nesta secção para obter ajuda adicional.  
 
Pode também ser solicitado a registar o seu dispositivo. As inscrições são necessárias para confirmar a sua identidade e ligar a sua escola ou conta de trabalho ao seu dispositivo. Se não estiver registado, será automaticamente guiado através dessa configuração antes de instalar a aplicação MTD. Quando chegar ao ecrã de **acesso Get,** pode iniciar os passos de instalação.  

Para obter mais informações sobre o registo do dispositivo, consulte [Registar o seu dispositivo pessoal na rede da sua organização](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>configuração iOS  

1. No ecrã de **acesso Get,** siga as instruções para instalar a aplicação MTD que é exigida pela sua organização.   
2. Volte ao ecrã de **acesso Get** e selecione **Open**.  
3. A aplicação MTD pede permissão para abrir o Microsoft Authenticator. Selecione **Open** (Abrir). 
4. Selecione a sua conta de trabalho para iniciar sessão. 
5. Espere enquanto a aplicação MTD digitaliza o seu dispositivo para ameaças de segurança. 
6. Volte para a escola ou app de trabalho a que estava inicialmente a tentar aceder. Neste momento, a sua organização pode instá-lo a configurar outros requisitos de segurança da aplicação, tais como a criação de um PIN.   
7. Agora deve ter acesso à aplicação. Se ainda estiver bloqueado,  
    * No ecrã de **acesso Get,** selecione **Reverificar**.  
    * Vá à aplicação MTD e verifique se existem ameaças existentes. Complete os passos recomendados para resolver a ameaça e recuperar o acesso.    

### <a name="android-setup"></a>Configuração do Android 

1. No ecrã de **acesso Get,** siga as instruções para instalar a aplicação MTD que é exigida pela sua organização.  
2. Volte ao ecrã de **acesso Get** e selecione **Open**.  
3. A aplicação MTD pede a sua permissão para aceder a determinadas áreas do seu dispositivo, caso seja necessário. Para que esta aplicação funcione corretamente, deve **permitir** o acesso aos contactos. As permissões solicitadas variarão entre os fornecedores de MTD.  
4. Selecione a sua conta de trabalho para iniciar sessão.  
5. Espere enquanto a aplicação MTD digitaliza o seu dispositivo para ameaças de segurança.  
6. Volte para a escola ou app de trabalho a que estava inicialmente a tentar aceder. Neste momento, a sua organização pode instá-lo a configurar outros requisitos de segurança da aplicação, tais como a criação de um PIN.  
7. Agora deve ter acesso à aplicação. Se ainda estiver bloqueado,  
    * No ecrã de **acesso Get,** selecione **Reverificar**.  
    * Vá à aplicação MTD e verifique se existem ameaças existentes. Complete os passos recomendados para resolver a ameaça e recuperar o acesso.  

### <a name="installation-failed"></a>Falha na instalação  

Se a instalação falhar, contacte a pessoa de suporte de TI. Vá ao site do Portal da [Empresa](https://go.microsoft.com/fwlink/?linkid=2010980) para encontrar os contactos da sua organização.  

Também pode enviar os registos da sua aplicação para a sua pessoa de suporte de TI para lhes fornecer mais contexto sobre a instalação.  
* Utilizadores Android: [Faça upload e envie os seus registos](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) do Portal da Empresa.   

* utilizadores de dispositivos iOS: [Recupere e envie os seus registos](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) do Microsoft Edge para iOS.  

## <a name="resolve-a-threat"></a>Resolver uma ameaça  
Se uma ameaça exceder o nível de ameaça definido da sua organização, a sua organização também:  
   
* Acesso ao bloco: Impede-o de usar as aplicações protegidas da sua organização enquanto se inscreve na sua conta de trabalho ou escola.  
* Eliminar dados: Elimina o seu trabalho ou dados escolares de uma ou mais aplicações protegidas da sua organização.  

Para resolver uma ameaça e recuperar o acesso, abra a aplicação MTD no seu dispositivo. Leia as informações fornecidas para saber como a ameaça pode afetar o seu dispositivo e como resolvê-lo. Depois de seguir os passos para resolver a ameaça, volte à aplicação MTD e inicie uma nova digitalização. Pode levar alguns minutos para recuperar o acesso à sua organização.  

## <a name="next-steps"></a>Passos seguintes  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).

