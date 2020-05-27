---
title: Obter um Certificado Push de MDM da Apple para o Intune
titleSuffix: ''
description: Obtenha um certificado Apple MDM Push para gerir dispositivos iOS/iPadOS com Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a66171d678ffd19e424fb399633c3fed3db9a588
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987003"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Obter um certificado push de MDM da Apple

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

É necessário um certificado Apple MDM Push para a Intune gerir dispositivos iOS/iPadOS e macOS. Depois de adicionar o certificado ao Intune, o utilizadores podem inscrever os seus dispositivos com:

- A aplicação Portal da Empresa.

- Os métodos de inscrição em massa da Apple, como o Programa de Registo de Aparelho, o Apple School Manager ou o Apple Configurator.

Para mais informações sobre as opções de inscrição, consulte [Escolha como inscrever dispositivos iOS/iPadOS](ios-enroll.md).

Quando um certificado push expira, tem de renová-lo. Ao renovar, certifique-se de que utiliza o mesmo ID Apple que utilizou quando criou o certificado push.


## <a name="steps-to-get-your-certificate"></a>Passos para obter o seu certificado
Inscreva-se no centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **Devices**  >  **dispositivos de inscrição**de dispositivos  >  **Apple**MDM  >  **Push Certificate,** e siga estes passos.

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>Passo 1. conceder permissão à Microsoft para enviar informações sobre o utilizador e o dispositivo à Apple
Selecione, **concordo.** para conceder permissão à Microsoft para enviar dados para a Apple.

![O ecrã Configurar Certificado Push de MDM da Apple com o Push de MDM não configurado.](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>Passo 2. transferir o pedido de assinatura de certificado do Intune obrigatório para criar um Certificado Push de MDM da Apple
Selecione **Baixar o seu CSR** para descarregar e guardar o ficheiro de pedido localmente. O ficheiro é utilizado para pedir um certificado de relação de confiança a partir do Portal Apple Push Certificates.

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>Passo 3. criar um certificado push de MDM da Apple
Selecione **Criar o seu certificado** de push MDM para ir ao Portal dos Certificados de Impulso da Apple. Inscreva-se na sua empresa Apple ID e, em seguida, clique em **Criar um Certificado**. **Selecione Escolha O Ficheiro** e navegue no ficheiro de pedido de assinatura de certificado e, em seguida, escolha **enviar**. Na página de Confirmação, escolha **o Download** para o ficheiro de download do certificado (.pem) e guarde o ficheiro localmente.

> [!NOTE]
> O certificado está associado ao ID Apple utilizado para criá-lo. Como melhor prática, utilize um ID Apple da empresa para tarefas de gestão e certifique-se de que a caixa de correio é monitorizada por mais do que uma pessoa, como uma lista de distribuição. Nunca utilize um ID Apple pessoal.

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>Passo 4. introduzir o ID Apple que utilizou para criar o seu certificado push de MDM da Apple
Aponte este ID para tê-lo guardado quando precisar do mesmo para renovar o certificado.

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>Passo 5. navegar para o certificado push de MDM da Apple a carregar
Vá ao ficheiro certificado (.pem), escolha **Open,** e depois escolha **Upload**. Com o certificado push, o Intune pode inscrever e gerir dispositivos da Apple.

## <a name="renew-apple-mdm-push-certificate"></a>Renovar um certificado push de MDM da Apple
O certificado push Apple MDM é válido por um ano e deve ser renovado anualmente para manter a gestão do iOS/iPadOS e do dispositivo macOS. Se o certificado expirar, não será possível contactar os dispositivos Apple inscritos.

O certificado está associado ao ID Apple utilizado para criá-lo. Renove o certificado push de MDM com o mesmo ID Apple que utilizou para criá-lo.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), escolha **Devices**  >  **dispositivos de inscrição dispositivos**  >  **Apple MDM**Push  >  **Certificate**.
2. Escolha **o download da sua RSE** para descarregar e guardar o ficheiro de pedido localmente. O ficheiro é utilizado para pedir um certificado de relação de confiança a partir do Portal Apple Push Certificates.
3. Selecione **Criar o seu certificado** de push MDM para ir ao Portal dos Certificados de Impulso da Apple. Encontre o certificado que pretende renovar e selecione **Renovar**.
4. No ecrã **'Certificado 'Push' renovador,** forneça notas para o ajudar a identificar o certificado no futuro, selecione **Escolher File** para navegar no novo ficheiro de pedido que descarregou e escolher **upload**.
   > [!TIP]
   > Os certificados podem ser identificados pelo Identificador de Utilizador. Examine o ID do **sujeito** nos dados do certificado para encontrar a parte GUID do UID. Ou, num dispositivo iOS/iPadOS matriculado, vá para **definições**De Perfil de  >  **General**  >  **Gestão**geral de**Dispositivos** Mais Perfil de  >  **Management Profile**  >  **More Details**  >  **Gestão**de Detalhes . O item da segunda linha, **Tópico,** contém o GUID único que pode comparar com o certificado no portal Apple Push Certificates.
 
6. No ecrã **de Confirmação,** selecione **Download** e guarde o ficheiro .pem localmente.
7. Intune , selecione o ícone de navegação do **apple MDM push,** selecione o ficheiro .pem descarregado da Apple e escolha **upload**. [Intune](https://go.microsoft.com/fwlink/?linkid=2090973)

O seu certificado de push Apple MDM aparece **Ativo** e tem 365 dias até expirar.
