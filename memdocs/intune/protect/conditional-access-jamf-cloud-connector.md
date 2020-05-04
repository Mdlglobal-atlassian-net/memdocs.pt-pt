---
title: Integrar o Conector Jamf Pro Cloud com a Microsoft Intune
titleSuffix: Microsoft Intune
description: Utilize o Conector Jamf Cloud com as políticas de conformidade da Microsoft Intune com o Azure Ative Directory Conditional Access para ajudar a integrar e proteger dispositivos geridos pelo Jamf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538405"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Utilize o Conector Jamf Cloud com a Microsoft Intune

Este artigo pode ajudá-lo a instalar o Conector Jamf Cloud para integrar o Jamf Pro com o Microsoft Intune. O Cloud Connector automatiza muitos dos passos necessários quando configura manualmente a integração como documentado no [Integrate Jamf Pro com Intune para a conformidade](../protect/conditional-access-integrate-jamf.md).

Quando configurar o Conector cloud:

- A configuração cria automaticamente as aplicações Jamf Pro em Azure, substituindo a necessidade de configurá-las manualmente.
- Pode integrar várias instâncias do Jamf Pro com o mesmo inquilino Azure que acolhe a sua subscrição Intune.

A ligação de várias instâncias do Jamf Pro com um único inquilino Azure só é suportada quando utilizar o Cloud Connector. Quando utiliza uma ligação manualmente configurada, apenas uma instância de Jamf pode integrar-se com um inquilino Azure.

A utilização do Conector cloud é opcional:

- Para novos inquilinos que ainda não se integram com o Jamf, pode optar por configurar o Cloud Connector como descrito neste artigo. Ou pode configurar manualmente a integração conforme descrito no [Integrate Jamf Pro com Intune para a conformidade](../protect/conditional-access-integrate-jamf.md)
- Para os inquilinos que já têm uma configuração manual, pode optar por remover essa integração e, em seguida, configurar o Cloud Connector. Tanto a remoção de uma integração existente como a criação do Cloud Connector são descritas neste artigo.

Se planeia substituir a sua integração anterior pelo Conector De Nuvem Jamf:

- Utilize o [procedimento para remover a configuração atual](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), que inclui eliminar as aplicações enterprise para o Jamf Pro e desativar a integração manual. Em seguida, pode utilizar o [procedimento para configurar o Conector cloud](#configure-the-cloud-connector-for-a-new-tenant).
- Não precisa de voltar a registar dispositivos. Os dispositivos já estão registados podem utilizar o Cloud Connector sem configuração adicional.
- Certifique-se de configurar o Cloud Connector no prazo de 24 horas após a remoção da sua integração manual para garantir que os seus dispositivos registados podem continuar a reportar o seu estado.

Para obter mais informações sobre o Conector de Nuvem Jamf, consulte [configurar a integração intune macOS utilizando o Cloud Connector](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) no docs.jamf.com.

## <a name="prerequisites"></a>Pré-requisitos

**Produtos e serviços:**  
- Jamf Pro 10.18 ou mais tarde
- Uma conta de utilizador Jamf Pro com privilégios de acesso condicional  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Aplicação Portal da Empresa para macOS](https://aka.ms/macoscompanyportal)
- dispositivos macOS com OS X 10.12 Yosemite ou posteriormente

**Rede**:  
As seguintes portas e pontos finais devem ser acessíveis à Jamf e ao Intune para integrar corretamente:

- **Insinton :** Porto 443
- **Apple**: Portos 2195, 2196 e 5223 (notificações push to Intune)
- **Jamf**: Portas 80 e 5223

- Pontos finais:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Para que a APNS funcione corretamente na rede, deve ativar as ligações de saída e redirecionar a partir das seguintes portas:

- O bloco Apple 17.0.0.0/8 sobre as portas TCP 5223 e 443 de todas as redes de clientes.
- Portas 2195 e 2196 dos servidores Jamf Pro.

Para obter mais informações sobre estes portos, consulte os seguintes artigos:

- [Requisitos de configuração de rede intonantes e largura de banda.](../fundamentals/network-bandwidth-use.md)
- Portas de [rede utilizadas pelo Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) na jamf.com.
- [Portas TCP e UDP utilizadas por produtos de software da Apple](https://support.apple.com/HT202944) em support.apple.com

**Contas:**  
Os procedimentos deste artigo requerem a utilização de contas com as seguintes permissões:

- **Consola Jamf Pro**: Uma conta com permissões para gerir o Jamf Pro
- **Microsoft Endpoint Management centro**de administração : Administrador Global
- **Portal Azure**: Administrador Global

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Remova a integração do Jamf Pro para um inquilino previamente configurado

Utilize o seguinte procedimento para remover uma integração manualmente configurada do Jamf Pro do seu inquilino Azure *antes* de poder configurar o Cloud Connector.

Se não tiver previamente estabelecido uma ligação entre o Jamf Pro e o Intune, ou se tiver uma ou mais ligações que já utilizem o Cloud Connector, ignore este procedimento e comece por [configurar o Cloud Connector para um novo inquilino.](#configure-the-cloud-connector-for-a-new-tenant)

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Remova uma integração jamf Pro manualmente configurada

1. Inscreva-se na consola Jamf Pro.

2. Selecione **Definições** (o ícone de engrenagem no canto superior direito) e, em seguida, vá ao**Acesso Condicional**de **Gestão** > Global .

   ![Navegar para acesso condicional](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selecione **Editar**.

4. Desselecione a caixa de verificação para ativar a **integração intune para o macOS**.

   Quando desseleccionar esta definição, desativa a ligação, mas guarde a configuração.

5. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e vá para a gestão de**dispositivos parceiros**de **administração** > do inquilino.

   No nó de gestão do **dispositivo Partner,** elimine o ID da **aplicação** no **'Especificar' Id da aplicação de diretório ativo Azure para** o campo Jamf e, em seguida, selecione **Save**.

   O ID de aplicação é o ID da aplicação Azure Enterprise que foi criada em Azure quando você estabeleceu uma integração manual se jamf Pro.

6. Inscreva-se no [portal Azure](https://portal.azure.com/) com uma conta que tenha permissões global de administrador, e vá às aplicações da **Azure Ative Directory** > **Enterprise.**

   Localize as duas aplicações do Jamf e elimine-as. Novas aplicações serão automaticamente criadas quando configurar o Conector De Nuvem Jamf no próximo procedimento.

   ![Selecione as aplicações do Jamf para eliminar](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Depois de ter desativado a integração no Jamf Pro e eliminado as aplicações enterprise, o nó de **gestão** do dispositivo Partner apresenta o estado de ligação de **Terminated**.

   ![Estado de ligação rescindido](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Agora que removeu com sucesso a configuração manual para a integração do Jamf Pro, pode configurar a integração utilizando o Cloud Connector. Para tal, consulte [configure o Cloud Connector para um novo inquilino](#configure-the-cloud-connector-for-a-new-tenant) neste artigo.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Configure o Conector de Nuvem para um novo inquilino

Utilize o seguinte procedimento para configurar o Conector Jamf Cloud para integrar o Jamf Pro e o Microsoft Intune quando:

- Você não tem qualquer integração entre Jamf Pro e Intune configurado para o seu inquilino Azure.
- Já tem um Cloud Connector montado entre o Jamf Pro e o Intune no seu inquilino Azure e pretende integrar uma instância de Jamf adicional com a sua subscrição.

Se tem atualmente uma integração manualmente configurada entre intune e jamf Pro, consulte [Remover a integração do Jamf Pro para um inquilino previamente configurado](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) neste artigo para remover essa integração antes de prosseguir. É necessária a remoção de uma integração manualmente configurada antes de poder configurar com sucesso o Conector de Nuvem do Jamf.

### <a name="create-a-new-connection"></a>Criar uma nova ligação

1. Inscreva-se na consola Jamf Pro.

2. Selecione **Definições** (o ícone de engrenagem no canto superior direito 0 e, em seguida, vá para o**Acesso Condicional**de **Gestão** > Global .

   ![Navegar para acesso condicional](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selecione **Editar**.

4. Selecione a caixa de verificação para **ativar a integração intune para o macOS**.
   - Selecione esta definição para que o Jamf Pro envie atualizações de inventário para o Microsoft Intune.
   - Pode desseleccionar esta definição para desativar a ligação, mas guardar a sua configuração.

   > [!IMPORTANT]
   > Se a **integração enable Intune para macOS** já estiver selecionada e o Tipo de *Ligação* estiver definido para **Manual,** deve remover essa integração antes de continuar. Consulte [A integração do Jamf Pro para um inquilino previamente configurado](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) neste artigo antes de continuar.

5. No tipo de *ligação,* selecione **Cloud Connector**.

   ![Selecione Cloud Connector na consola Jamf Pro](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. A partir do menu pop-up **Da Nuvem Soberana,** selecione a localização da sua Nuvem Soberana da Microsoft.

7. Selecione uma das seguintes opções de página de aterragem para computadores que não sejam reconhecidos pelo Microsoft Azure:
   - A página de Registo de **Dispositivos Default Jamf Pro** - Dependendo do estado do dispositivo macOS, esta opção redireciona os utilizadores para o portal de inscrição do dispositivo Jamf Pro (para se inscrever no Jamf Pro) ou na aplicação Intune Company Portal (para se registar com a AD Azure).
   - **A página Access Negado**
   - **URL personalizado**

8. Selecione **Ligar**. É redirecionado para registar as aplicações do Jamf Pro em Azure.

   Quando solicitado, especifique as suas credenciais Microsoft Azure e siga as instruções no ecrã para conceder as permissões solicitadas. Concederá permissões para o **Cloud Connector,** e depois novamente para a aplicação de registo de utilizadores do **Cloud Connector.** Ambas as aplicações estão registadas no Azure como Aplicações Empresariais.

   Após a concessão de permissões para ambas as aplicações, a página de ID da **aplicação** abre.

9. Na página id da **aplicação,** selecione **Copiar e abrir Intune**.

   ![ID da aplicação](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   O ID da *aplicação* é copiado para a sua área de reprodução do sistema para utilização no próximo passo, e o nó de **gestão** do dispositivo Partner no centro de administração do *Microsoft Endpoint Manager* abre. **(Administração** > de**Inquilinos Gestão de dispositivos**parceiros).

10. No nó de gestão do **dispositivo Partner,** *colhe* o ID da **aplicação** no **Especio do Id da aplicação de diretório ativo Azure para** o campo Jamf e, em seguida, selecione **Save**.

    ![Configure gestão de dispositivos parceiros](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Volte à página de ID da aplicação no Jamf Pro e selecione **Confirmar**.

12. O Jamf Pro completa e testa a configuração e mostra o sucesso ou falha da ligação na página de definições de Acesso Condicional. A seguinte imagem é um exemplo de sucesso:

    ![A configuração bem sucedida está confirmada no Jamf Pro](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. No centro de administração do Microsoft Endpoint Manager, refresque o nó de gestão do **dispositivo Partner.** A ligação deve agora mostrar como **Ativa:**

    ![O estado de ligação está ativo](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Quando a ligação entre o Jamf Pro e o Microsoft Intune for estabelecida com sucesso, o Jamf Pro envia informações de inventário para o Microsoft Intune para cada computador que está registado com a AD Azure (registar-se com a AD Azure é um fluxo de trabalho de utilizador final). Pode visualizar o Estado de Inventário de Acesso Condicional para um utilizador e um computador na categoria de Conta de Utilizador Local de informações de inventário de um computador no Jamf Pro.

Depois de integrar uma instância do Jamf Pro utilizando o Jamf Cloud Connector, pode utilizar este mesmo procedimento para configurar instâncias adicionais do Jamf Pro com a mesma subscrição Intune no seu inquilino Azure.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Definir as políticas de conformidade e registar dispositivos

Depois de configurar a integração entre intune e Jamf, tem de aplicar políticas de [conformidade a dispositivos geridos pelo Jamf](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Desligar Jamf Pro e Intune

Caso necessite de remover a integração do Jamf Pro com o Intune, utilize os seguintes passos para remover a ligação dentro da consola Jamf Pro. Esta informação aplica-se tanto ao Cloud Connector como a uma integração manualmente configurada.

1. No Jamf Pro, vá ao **Global Management** > **Conditional Access.** No separador **macOS Intune Integração,** selecione **Editar**.

2. Limpe a **Integração Enable Intune para a** caixa de verificação macOS.

3. Selecione **Guardar**. Jamf Pro envia a sua configuração para Intune e a integração será terminada

4. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

5.  >  **Selecione****Conectores e tokens** > Administração de**dispositivos parceiros** para verificar se o estado está agora **terminado**.

   > [!NOTE]
   > Os dispositivos Mac da sua organização serão removidos na data (3 meses) mostrada na sua consola.

## <a name="get-support-for-the-cloud-connector"></a>Obtenha suporte para o Conector cloud

Uma vez que o conector de nuvem cria automaticamente as aplicações Da Azure Enterprise necessárias para a integração, o seu primeiro ponto de contacto para suporte deve ser **o Jamf**. As opções incluem:

- Suporte por e-mail em`support@jamf.com`
- Use o portal de apoio na Jamf Nation:https://www.jamf.com/support/ 


Antes de contactar o suporte:

- Reveja os pré-requisitos, tais como portas e versão do produto que utiliza.
- Confirme que as permissões para as seguintes duas aplicações Do Jamf Pro criadas no Azure não foram modificadas. As alterações às permissões da aplicação não são suportadas pela Intune e podem fazer com que a integração falhe.

  Aplicação de registo do **utilizador do Cloud Connector:**
  - Nome API: Microsoft Graph
    - Permissão: Iniciar sessão e ler o perfil do utilizador
    - Tipo: Delegado
    - Concedido através de: Consentimento do Administrador
    - Concedido por: Um administrador

  **Aplicativo Cloud Connector**:
  - Nome API: Microsoft Graph (instância 1)
    - Permissão: Iniciar sessão e ler o perfil do utilizador
    - Tipo: Delegado
    - Concedido através de: Consentimento do Administrador
    - Concedido por: Um administrador

  - Nome API: Microsoft Graph (instância 2)
    - Permissão: Ler dados de diretório
    - Tipo: Aplicação
    - Concedido através de: Consentimento do Administrador
    - Concedido por: Um administrador

  - Nome API: Intune API
    - Permissão: Enviar atributo do dispositivo ao Microsoft Intune
    - Tipo: Aplicação
    - Concedido através de: Consentimento do Administrador
    - Concedido por: Um administrador

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Perguntas comuns sobre o Conector Jamf Cloud

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Que dados são partilhados através do Cloud Connector?

O Cloud Connector autentica com o Microsoft Azure e envia dados de inventário do dispositivo do Jamf Pro para o Azure. Além disso, o Cloud Connector gere a descoberta de serviços em Azure, troca de fichas, erros de comunicação e recuperação de desastres.

### <a name="where-is-device-inventory-data-stored"></a>Onde é que os dados do inventário do dispositivo são armazenados?

Os dados do inventário do dispositivo são armazenados na base de dados do Jamf Pro.

### <a name="what-credentials-are-stored"></a>Que credenciais estão armazenadas?

Não há credenciais armazenadas. Ao configurar o Cloud Connector, os administradores devem consentir em adicionar a app de multi-inquilinos Jamf e a aplicação de conector macOS nativo ao seu inquilino Azure AD. Uma vez adicionada a aplicação multi-inquilino, o Cloud Connector solicita fichas de acesso para interagir com a API Azure. O acesso à aplicação pode ser revogado no Microsoft Azure a qualquer momento para restringir o acesso.

### <a name="how-is-data-encrypted"></a>Como é encriptado os dados?

O Cloud Connector utiliza a Segurança da Camada de Transporte (TLS) para os dados enviados entre o Jamf Pro e o Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Como é que a Jamf sabe qual o dispositivo que está associado a que instância do Jamf Pro?

O Jamf Pro utiliza microserviços no AWS para encaminhar corretamente as informações do dispositivo para a instância correta.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Posso mudar de utilização do Conector Cloud para o tipo de ligação manual?

Sim. Pode alterar o tipo de ligação de volta ao manual e seguir os passos para a configuração manual. Se tiver perguntas, devem ser encaminhados para jamf para ajuda.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>As permissões foram modificadas numa ou em ambas as aplicações necessárias (*Cloud Connector* e *Cloud Connector*user registration app ) e o registo não está a funcionar, é suportado?

A modificação das permissões nas aplicações não é suportada.

## <a name="next-steps"></a>Passos seguintes

- [Aplicar políticas de conformidade a dispositivos geridos pelo Jamf](../protect/conditional-access-assign-jamf.md)
- [Data Jamf envia para Intune](../protect/data-jamf-sends-to-intune.md)
