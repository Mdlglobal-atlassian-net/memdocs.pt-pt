---
title: Configurar a integração móvel da Sophos com o Intune
titleSuffix: Intune on Azure
description: Como configurar a solução Sophos Mobile com a Microsoft Intune para controlar o acesso de dispositivos móveis aos seus recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3298c2759b14fd2579fc51513177033c792b9c83
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988272"
---
# <a name="integrate-sophos-mobile-with-intune"></a>Integrar o Sophos Mobile com Intune  

Complete os seguintes passos para integrar a solução de Defesa de Ameaças Móveis Sophos com intune.  

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="before-you-begin"></a>Antes de começar  

Antes de iniciar o processo de integração do Sophos Mobile com o Intune, certifique-se de que tem o seguinte:  
- Subscrição do Microsoft Intune  
- Credenciais de administrador do Azure Active Directory para conceder as seguintes permissões:  
  - Iniciar sessão e ler o perfil de utilizador  
  - Aceder ao diretório como o utilizador com sessão iniciada  
  - Ler os dados do diretório  
  - Enviar informações do dispositivo para o Intune  
- Credenciais de administrador para aceder à consola de administração Sophos Mobile.  


### <a name="sophos-mobile-app-authorization"></a>Autorização de aplicação Sophos Mobile  
  
Segue-se o processo de autorização da aplicação Sophos Mobile:  
- Permitir que o serviço Sophos Mobile comunique informações relacionadas com o estado de saúde do dispositivo de volta ao Intune.  
- A Sophos Mobile sincroniza-se com a adesão do Grupo de Inscrição AD Azure para preencher a base de dados do seu dispositivo.  
- Permitir que a consola de administração Sophos Mobile utilize um único sinal de AD Azure (SSO).  
- Permita que a aplicação Sophos Mobile assine com o Azure AD SSO.  


## <a name="to-set-up-sophos-mobile-integration"></a>Para criar a integração sophos Mobile  

1. Inscreva-se no [portal Azure]( https://portal.azure.com/), vá **Intune**  >  **Device compliance**Mobile Threat  >  **Defense** > e **selecione Add**.  
2. Na página **Add Connector,** utilize o dropdown e selecione **Sofos**. E, em seguida, **selecione Criar**.  
3. Selecione o link *Abra a consola de administração Sophos*.  
4. Inscreva-se na [consola de administração Sophos](https://central.sophos.com/) com as suas credenciais Sophos.  
5. Vá para configurações **móveis**  >  **Settings**  >  **Setup**  >  **Configuração de sofos configuração**.  
6. Na página de **configuração Sophos,** selecione o separador **Intune MTD.**  
   ![Configuração de sophos](./media/sophos-mtd-connector-integration/sophos-setup.png) 
 
7. Selecione **Ligar,** e, em seguida, **selecione Sim**. Sophos conecta-se a Intune e requer que você assine a sua subscrição Intune. 
8. Na janela de autenticação Intune da Microsoft, introduza as suas credenciais Intune e **aceite** o pedido de permissões para a *Defesa de Fios Móveis Sophos*.  
   ![Autenticação inoportuna](./media/sophos-mtd-connector-integration/intune-authentication.png)

9. Na página de **configuração sophos,** selecione **Guardar** para completar a configuração para Intune:  
   ![Salvar a configuração de Sophos](./media/sophos-mtd-connector-integration/save-sophos-configuration.png)  

1. Quando a mensagem **Integração Bem-sucedida** for apresentada, significa que a integração foi concluída.  
1. Na consola Intune, a Sophos já está disponível.  


## <a name="next-steps"></a>Passos Seguintes  
[Configure aplicativos de cliente Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
