---
title: Tutorial - Utilize o Apple Business Manager ou o Programa de Inscrição de Dispositivos para inscrever dispositivos iOS/iPadOS em Intune
titleSuffix: Microsoft Intune
description: Neste tutorial, irá configurar as funcionalidades de inscrição de dispositivos corporativos da Apple a partir da ABM para inscrever dispositivos iOS/iPadOS em Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/30/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to set up the Apple's corporate device enrollment features so that corporate devices can automatically enroll in Intune.
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40dd24c281f00fce71a98413ab2666cca2bab2ce
ms.sourcegitcommit: 10578b5a631f9148e59389a1ce4e7d4892f772a0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80979210"
---
# <a name="tutorial-use-apples-corporate-device-enrollment-features-in-apple-business-manager-abm-to-enroll-iosipados-devices-in-intune"></a>Tutorial: Utilize as funcionalidades de inscrição de dispositivos corporativos da Apple no Apple Business Manager (ABM) para inscrever dispositivos iOS/iPadOS em Intune
As funcionalidades de Inscrição de Dispositivos no Apple Business Manager simplificam os dispositivos de inscrição. Intune também suporta o portal de inscrição de dispositivos mais antigo (DEP) da Apple, mas encorajamo-lo a começar de novo com o Apple Business Manager. Com a Microsoft Intune e a Apple Corporate Device Registration, os dispositivos estão automaticamente matriculados de forma segura na primeira vez que o utilizador liga o dispositivo. Por isso, pode enviar dispositivos para muitos utilizadores sem ter de configurar cada dispositivo individualmente. 

Neste tutorial, ficará a saber como:
> [!div class="checklist"]
> * Obtenha um símbolo de inscrição de dispositivo apple
> * Sync gerido dispositivos para Intune
> * Criar um perfil de Inscrição
> * Atribuir o perfil de Inscrição a dispositivos

Se não tiver uma subscrição do Intune, [inscreva-se numa conta de avaliação gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Pré-requisitos
- Dispositivos adquiridos no [Apple Business Manager](https://business.apple.com) ou no Programa de [Inscrição de Dispositivos da Apple](http://deploy.apple.com)
- Desloque a autoridade de gestão de [dispositivos móveis](../fundamentals/mdm-authority-set.md)
- Obtenha um [certificado Apple MDM Push](apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-device-enrollment-token"></a>Obtenha um símbolo de inscrição de dispositivo apple
Antes de inscrever dispositivos iOS/iPadOS com as funcionalidades de inscrição corporativa da Apple, precisa de um ficheiro apple device registration (.pem). Este token permite à Intune sincronizar informações sobre dispositivos apple que a sua empresa possui. Também permite ao Intune carregar perfis de inscrição para a Apple e atribuir dispositivos a esses perfis.

Usa o portal apple para criar um token de inscrição de dispositivos. Também utiliza os portais para atribuir dispositivos à Intune para gestão.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > iOS > **iOS matricula** do **iOS** > Programa de **Inscrição Tokens** > **Add**.

2. Conceda permissão à Microsoft para enviar informações sobre o utilizador e o dispositivo à Apple, ao selecionar **Concordo**.

   ![Captura de ecrã a mostrar o painel Token do Programa de Inscrição, na área de trabalho Certificados da Apple, para transferir a chave pública.](./media/tutorial-use-device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Selecione **Transferir a chave pública** para transferir e guardar o ficheiro da chave de encriptação (.pem) localmente. O ficheiro .pem é utilizado para pedir um certificado de relação de confiança a partir do portal da Apple.

4. Selecione **Criar um token para o Programa de Registo de Aparelho da Apple** para abrir o portal Programa de Implementação da Apple e inicie sessão com o Apple ID da sua empresa. Pode utilizar este Apple ID para renovar o token.

5. No [portal dos Programas de Implementação](https://deploy.apple.com) da Apple, selecione **Começar** em **Programa de Registo de Aparelho**. O seu processo pode ser ligeiramente diferente dos seguintes passos no [Apple Business Manager](https://business.apple.com).

4. Na página **Gerir Servidores**, selecione **Adicionar Servidor MDM**.

5. Para **nome do servidor MDM,** introduza o *TestMDMServer* e, em seguida, escolha **o Seguinte**. O nome do servidor é uma referência para identificar o servidor de gestão de dispositivos móveis (MDM). Não é o nome nem o URL do servidor do Microsoft Intune.

6. A caixa de diálogo **Adicionar &lt;NomeDoServidor&gt;** é aberta e pede para **Atualizar a Chave Pública**. Selecione **Escolher Ficheiro…** para carregar o ficheiro .pem e, em seguida, selecione **Seguinte**.

6. Aceda a **Programas de Implementação** > **Programa de Inscrição de Dispositivos** > **Gerir Dispositivos**.
7. Em **dispositivos escolha**por , escolha **número de série**. <!--ask Tiffany about this-->

8. Em **Selecionar Ação**, selecione **Atribuir ao Servidor**, selecione o &lt;NomeDoServidor&gt; especificado no Microsoft Intune e, em seguida, selecione **OK**. O portal da Apple atribui os dispositivos especificados para o servidor do Intune para gestão e, em seguida, apresenta a mensagem **Atribuição Concluída**.

   No portal da Apple, vá a Programas de **Implementação** &gt; Programa de **Inscrição de Dispositivos** &gt; **ver o Histórico** de Atribuição para ver uma lista de dispositivos e a sua atribuição de servidores MDM.

9. Para referência futura, em Intune no portal Azure, forneça o APPLE ID usado para criar este símbolo.

    ![Captura de ecrã a mostrar a especificação do ID Apple utilizado para criar o token do programa de inscrição e o acesso ao token do programa de inscrição.](./media/tutorial-use-device-enrollment-program-enroll-ios/image03.png)

10. Na caixa **Token da Apple**, procure o ficheiro de certificado (.pem), escolha **Abrir** e, em seguida, escolha **Criar**. 

11. Se pretender aplicar etiquetas de âmbito para limitar quais os administradores que têm acesso a este token, selecione os âmbitos.

## <a name="create-an-apple-enrollment-profile"></a>Criar um perfil de inscrição da Apple
Agora que instalou o seu símbolo, pode criar um perfil de inscrição para dispositivos iOS/iPadOS de propriedade corporativa. Um perfil de inscrição de dispositivos especifica as definições aplicadas a um grupo de dispositivos durante a inscrição.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > iOS > **iOS matricula** do **iOS** > **Tokens**do Programa de Inscrição .

2. Selecione o token que acaba de instalar, escolha **Perfis** > **Criar perfis** > **iOS**.

3. Na página **Basics,** introduza *testProfile* para **nome** e *teste ADE para dispositivos iOS/iPadOS* para **Descrição**. Os utilizadores não verão estes detalhes.

4. Selecione **Seguinte**.

5. Na página Definições de **Gestão,** decida se deseja que os seus dispositivos se inscrevam com ou sem **Afinidade**do Utilizador . A Affinity do Utilizador foi concebida para dispositivos que serão utilizados por utilizadores específicos. Se os seus utilizadores pretenderem utilizar o Portal da Empresa para serviços como instalar aplicações, escolha **Inscrever-se com a Finha do Utilizador**. Se os seus utilizadores não precisarem do Portal da Empresa ou pretenderem fornecer o dispositivo a muitos utilizadores, escolha **Matricular-se sem afinidade**do utilizador .

6. Se optou por se inscrever na User Affinity, aparece o **Select onde os utilizadores devem autenticar** a opção. Decida se pretende autenticar com o Portal da Empresa ou com o Apple Setup Assistant.
   - **Portal da Empresa**: Selecione esta opção para utilizar a Autenticação Multi-Factor, permita que os utilizadores alterem as palavras-passe no primeiro início de sessão ou invistam os utilizadores a redefinir as suas palavras-passe expiradas durante a inscrição. Se pretender que a aplicação do Portal da Empresa atualize automaticamente nos dispositivos dos utilizadores finais, implemente separadamente o Portal da Empresa como uma aplicação necessária a estes utilizadores através do Programa de Compra de Volume (VPP) da Apple.
   - **Assistente de configuração**: Selecione esta opção para utilizar a autenticação http fornecida pela Apple através do Apple Setup Assistant
  
7. Se optou por inscrever-se na User Affinity e Autenticar com o Portal da Empresa, aparece o Portal da Empresa de Instalação com opção **VPP.** Se instalar o Portal da Empresa com um token VPP, o utilizador não terá de introduzir um Apple ID e Password para descarregar o Portal da Empresa a partir da loja de aplicações durante a inscrição. Escolha **o Use Token:** em **Install Company Portal com VPP** para selecionar um token VPP que tenha licenças gratuitas do Portal da Empresa disponível. Se não quiser utilizar o VPP para implementar o Portal da Empresa, escolha **Não utilize vPP**. 

8. Se optou por inscrever-se na User Affinity, Authenticate with Company Portal e Instalar o Portal da Empresa com vPP, decida se pretende executar o Portal da Empresa em Modo De Aplicação Única até à Autenticação. Esta definição permite-lhe garantir que o utilizador não terá acesso a outras aplicações até que termine a inscrição corporativa. Se pretender restringir o utilizador a este fluxo até que a inscrição esteja concluída, escolha **Sim** ao **portal da empresa run no modo de aplicação única até**à autenticação . 

9. Em definições de gestão do **dispositivo,** escolha **Sim** sob **supervisão** (se escolheu **Inscrever-se com a finidade**do utilizador, isto é automaticamente definido para **Sim).** Os dispositivos supervisionados dão-lhe as opções de gestão mais opções de gestão para os seus dispositivos corporativos iOS/iPadOS.

10. Escolha **Sim** sob **inscrição bloqueada** para garantir que os seus utilizadores não podem remover a gestão do dispositivo corporativo. 

11. Escolha uma opção em **Sync with Computers** para determinar se os dispositivos iOS/iPadOS serão capazes de sincronizar com computadores.

12. Por padrão, a Apple dá nomes ao dispositivo com o tipo de dispositivo (isto é, iPad). Se quiser fornecer um modelo de nome diferente, escolha **Sim** sob o modelo de nome do **dispositivo Apply**. Introduza o nome que pretende aplicar nos dispositivos, onde as cordas *{{SERIAL}}* e *{{DEVICETYPE}}* substituirão o número de série e o tipo de dispositivo de cada dispositivo. Caso contrário, escolha **não** sob o modelo de nome do **dispositivo Apply**.

13. Escolha **Seguinte**.

14. Na página de Assistente de **Configuração,** *Departamento tutorial* para Nome **do Departamento**. Esta cadeia é o que os utilizadores vêem quando tocam **na configuração** durante a ativação do dispositivo.

15. Sob **o Telefone do Departamento,** insira um número de telefone. Este número aparece quando os utilizadores tocam no botão **de ajuda Need** durante a ativação.

16. Pode **mostrar** ou **ocultar** uma variedade de ecrãs durante a ativação do dispositivo. Para a experiência de inscrição mais perfeita, coloque todos os ecrãs para **Hide**.

17. Escolha **O Próximo** para ir à página Review + **Criar.** Selecione **Criar**.

## <a name="sync-managed-devices-to-intune"></a>Sync gerido dispositivos para Intune

Depois de configurar um programa de inscrição com o portal ABM, ASM ou ADE e atribuir dispositivos ao servidor MDM, pode esperar que estes dispositivos sincroniem ao serviço Intune ou empurrem manualmente uma sincronização. Sem sincronização manual, os dispositivos podem demorar até 24 horas a aparecer no portal Azure.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > **iOS** > **inscrição do iOS** > Programa de **Inscrição Tokens** > escolha um símbolo na lista > **Dispositivos** > **Sync**.

## <a name="assign-an-enrollment-profile-to-iosipados-devices"></a>Atribuir um perfil de inscrição aos dispositivos iOS/iPadOS

Tem de atribuir um perfil do programa de inscrição aos dispositivos para poder inscrevê-los. Estes dispositivos estão sincronizados com intune da Apple, e devem ser atribuídos ao token de servidor MDM adequado no portal ABM, ASM ou ADE.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > **iOS** > inscrição do **iOS** > Programa de **Inscrição Tokens** > escolha o seu símbolo na lista.
2. Escolha **Dispositivos** > escolha dispositivos na lista > **Atribuir perfil**.
3. Em **Atribuir perfil**, escolha um perfil para os dispositivos > **Atribuir**.

## <a name="distribute-devices-to-users"></a>Distribuir dispositivos pelos utilizadores

Criou a gestão e a sincronização entre a Apple e a Intune, e atribuiu um perfil para permitir que os seus dispositivos ADE se inscrevam. Agora pode distribuir os dispositivos aos utilizadores. Os dispositivos com afinidade do utilizador necessitam que seja atribuída uma licença do Intune a cada utilizador.

## <a name="next-steps"></a>Próximos passos

Pode encontrar mais informações sobre outras opções disponíveis para a inscrição de dispositivos iOS/iPadOS.

> [!div class="nextstepaction"]
> [Artigo de inscrição em profundidade iOS/iPadOS ADE](device-enrollment-program-enroll-ios.md)

<!--commenting out because inaccurate>
## Clean up resources
<!--If you don't want to use iOS/iPadOS corporate enrolled devices anymore, you can delete them.>
<!--- If the devices are enrolled in Intune, you must first [delete them from the Azure Active Directory portal](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).>
