---
title: Tutorial&#58; Permitir a cogestão de dispositivos de internet
titleSuffix: Configuration Manager
description: Saiba como configurar a cogestão de novos dispositivos Windows 10 baseados na Internet com O Gestor de Configuração e Microsoft Intune.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712716"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutorial: Permitir a cogestão de novos dispositivos baseados na Internet

Com a cogestão, pode manter os seus processos bem estabelecidos para usar o Gestor de Configuração para gerir Computadores na sua organização. Ao mesmo tempo, está a investir na nuvem através do uso de Intune para a segurança e o fornecimento moderno.

Neste tutorial, você configura a cogestão de dispositivos Windows 10 num ambiente onde você usa tanto o Azure Ative Directory (AD) como um AD no local, mas não tem um [Azure Ative Directory híbrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD). O ambiente do Gestor de Configuração inclui um único site primário com todas as funções do sistema do site localizadas no mesmo servidor, o servidor do site. Este tutorial começa com a premissa de que os seus dispositivos Windows 10 já estão matriculados no Intune. 

Se tiver um Azure AD híbrido que se junte ao seu Anúncio no local com a Azure AD, recomendamos seguir o nosso tutorial de acompanhante, [Enable co-management para clientes de Gestor de Configuração.](tutorial-co-manage-clients.md)

Utilize este tutorial quando:
  
- Tem dispositivos Windows 10 para fazer cogestão. Estes dispositivos podem ter sido fornecidos através do Windows Autopilot ou são diretamente do seu hardware OEM.
- Tem dispositivos Windows 10 na internet que gere atualmente com o Intune ao qual pretende adicionar o cliente do Gestor de Configuração.

**Neste tutorial irá:**  
> [!div class="checklist"]  
> * Reveja os pré-requisitos para o Azure e o seu ambiente no local
> * Solicitar um certificado SSL público para o gateway de gestão de nuvem (CMG)
> * Ativar serviços Azure em Gestor de Configuração
> * Implementar e configurar um gateway de gestão de nuvem  
> * Configure o ponto de gestão e os clientes para usar o CMG
> * Ativar a cogestão no Gestor de Configuração
> * Configure Intune para instalar o cliente do Gestor de Configuração

## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Serviços e ambiente azure

- Assinatura Azure[(teste gratuito)](https://azure.microsoft.com/free)
- Azure Active Directory Premium
- Subscrição do Microsoft Intune
  > [!TIP]  
  > Uma subscrição de Mobilidade e Segurança Empresarial (EMS) inclui tanto o Azure Ative Directory Premium como o Microsoft Intune. Subscrição EMS[(teste gratuito).](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)  

- Intune está configurado para [dispositivos de inscrição automática](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  

> [!TIP]
> Já não precisa de adquirir e atribuir licenças individuais intune ou EMS aos seus utilizadores. Para mais informações, consulte o [Produto e licenciando as FAQ.](../core/understand/product-and-licensing-faq.md#bkmk_mem)

### <a name="on-premises-infrastructure"></a>Infraestrutura no local

- Configuração Manager atual ramo, versão 1810 ou mais tarde.
  
  A versão 1810 introduz [o Enhanced HTTP,](../core/plan-design/hierarchy/enhanced-http.md)que é utilizado neste tutorial para evitar requisitos PKI mais complexos. Através da utilização do Enhanced HTTP, o site principal que utiliza para gerir os clientes deve ser configurado para utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP.  

  A versão 1810 também introduz uma linha de comando mais simples para a instalação baseada na Internet do cliente Do Gestor de Configuração.

- A autoridade do MDM deve ser definida para Intune  

### <a name="external-certificates"></a>Certificados externos

- Certificado de autenticação do servidor CMG. Este certificado é um certificado SSL de um fornecedor de certificados de confiança pública e global. Por exemplo, mas não se limitando a, DigiCert, Thawte ou VeriSign. Exportará este certificado como. Ficheiro PFX com Chave Privada.  

- Mais tarde neste tutorial fornecemos orientações sobre como configurar o pedido para este certificado.

### <a name="permissions"></a>Permissões

Ao longo deste tutorial, utilize as seguintes permissões para completar tarefas:

- Uma conta que é *administradora global* da Azure Ative Directory (Azure AD)
- Uma conta que é um administrador de *domínio* na sua infraestrutura no local  
- Uma conta que é um *administrador completo* para *todos os* âmbitos no Gestor de Configuração

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Solicite um certificado público para o gateway de gestão de nuvem

Quando os seus dispositivos estão na internet, a cogestão requer o gateway de gestão de nuvem do Gestor de Configuração (CMG). O CMG permite que os seus dispositivos Windows 10 baseados na Internet comuniquem com a implementação do Gestor de Configuração no local. Para estabelecer uma confiança entre os dispositivos e o ambiente do Seu Gestor de Configuração, o CMG necessita de um certificado SSL.

Este tutorial utiliza um certificado público chamado certificado de autenticação de **servidor CMG** que obtém autoridade de um fornecedor de certificados de confiança global. Embora seja possível configurar a cogestão usando certificados que obtenham autoridade da sua autoridade de certificados microsoft no local, o uso de certificados auto-assinados está fora do âmbito deste tutorial.

O certificado de autenticação do **servidor CMG** é utilizado para encriptar o tráfego de comunicações entre o cliente do Gestor de Configuração e o CMG. O certificado remonta a uma Raiz fidedigna para verificar a identidade do servidor ao cliente. O certificado público inclui uma Raiz fidedigna em que os clientes do Windows já confiam.

Sobre este certificado: 

- Identifica um nome único para o seu serviço CMG em Azure e, em seguida, especifica esse nome no seu pedido de certificado.  
- Gera o seu pedido de certificado num servidor específico e, em seguida, submete o pedido a um fornecedor de certificados públicos para obter o certificado SSL necessário.  
- Importa para o sistema que gerou o pedido do certificado que recebe do fornecedor. Usa o mesmo computador para exportar o certificado para utilização quando posteriormente implanta o CMG para o Azure.  
- Quando a CMG instala, cria um serviço CMG em Azure utilizando o nome especificado no certificado.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identifique um nome único para o seu gateway de gestão de nuvem em Azure

Ao solicitar o certificado de autenticação do servidor CMG, especifice qual deve ser um nome único para identificar o seu *serviço Cloud (clássico)* em Azure. Por padrão, a nuvem pública Azure utiliza *cloudapp.net*, e o CMG está hospedado dentro do domínio cloudapp.net como * \<YourUniqueDnsName>.cloudapp.net*.  

> [!TIP]  
> Neste tutorial, o certificado de autenticação do **servidor CMG** utiliza um FQDN que termina em *contoso.com*.  Depois de criarmos o CMG, configuraremos um registo de nome canónico (CNAME) no DNS público da nossa organização. Este registo cria um pseudónimo para a CMG que mapeia o nome que usamos no certificado público.  

Antes de solicitar o seu certificado público, confirme que o nome que pretende utilizar está disponível no Azure. Não se cria diretamente o serviço em Azure. Em vez disso, o nome especificado no certificado público que solicita é utilizado pelo Gestor de Configuração para criar o serviço de nuvem quando instalar o CMG.  

1. Inscreva-se no [portal Microsoft Azure](https://portal.azure.com/).  

2. Selecione **Criar um recurso,** escolha a categoria **Compute** e, em seguida, selecione **Cloud Service**. A página de serviço Cloud (clássica) abre.

3. Para **o nome DNS,** especifique o nome prefixo para o serviço de nuvem que utilizará. Este prefixo deve ser o mesmo que utiliza mais tarde quando solicitar um certificado de publicação para o certificado de autenticação do servidor CMG. Utilizamos *o MyCSG,* que cria o espaço de nome de *MyCSG.cloudapp.net*. A interface confirma se o nome está disponível ou já está a ser utilizado por outro serviço.  
 Depois de confirmar que o nome que pretende utilizar está disponível, está pronto para submeter o Pedido de Assinatura de Certificado (CSR).

### <a name="request-the-certificate"></a>Solicitar o certificado

Utilize as seguintes informações para submeter um pedido de assinatura de certificado para o seu CMG a um fornecedor de certificados públicos. Altere os seguintes valores para ser relevante para o seu ambiente.  

- *MyCMG* para identificar o nome de serviço do gateway de gestão de nuvem
- *Contoso* como nome da empresa
- *Contoso.com* como domínio público

Recomendamos que utilize o seu servidor principal do site para gerar os pedidos de assinatura de certificados (CSR). Quando obtém o certificado, deve instá-lo no mesmo servidor que gerou a RSE ou não pode exportar a chave privada dos certificados, o que é necessário.  

Solicite um tipo de fornecedor de teclas de versão 2 quando gerar uma RSE. Apenas os certificados de versão 2 são suportados.  

> [!TIP]  
> Quando implementarmos o CMG, também instalaremos um ponto de distribuição em nuvem (CDP) ao mesmo tempo. Por predefinição, ao implementar um CMG, é selecionada a opção Permitir que a CMG funcione como ponto de distribuição em **nuvem e servir conteúdo do armazenamento Do Azure.** Co-localizar o CDP no servidor com o CMG remove a necessidade de certificados e configurações separados para suportar o CDP. Mesmo que o CDP não seja obrigado a usar a cogestão, é útil na maioria dos ambientes.  
>
> Se utilizar pontos adicionais de distribuição em nuvem para cogestão, terá de solicitar certificados separados para cada servidor adicional. Para solicitar um certificado público para o CDP, utilize os mesmos detalhes que para o gateway de gestão de nuvem CSR. Basta alterar o nome comum para que seja único para cada CDP.  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Detalhes para o gateway de gestão de nuvem CSR

- **Nome Comum**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Exemplo: MyCSG.contoso.com  
- Nome alternativo do **sujeito:** O mesmo que o Nome Comum (CN)  
- **Organização**: O nome da sua organização  
- **Departamento**: Pela sua organização  
- **Cidade**: Por sua organização  
- **Estado**: Por sua organização  
- **País**: Pela sua organização  
- **Tamanho da chave: 2048**  
- **Fornecedor: Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Importar o certificado

Depois de receber o certificado público, importe-o para o certificado local do computador que criou a RSE. Em seguida, exportar o certificado como . Ficheiro PFX para que possa usá-lo para o seu CMG em Azure.  

Os prestadores de certificados públicos normalmente fornecem instruções para a importação do certificado. O processo de importação do certificado deve assemelhar-se às seguintes orientações:  

1. No computador para o que o certificado deve ser importado, localize o ficheiro certificado .pfx.  

2. Clique no ficheiro para a direita e, em seguida, **selecione Instalar PFX**  

3. Quando o Assistente de Importação de Certificado sairá, selecione **Seguinte**.  

4. Na página **Ficheiro para Importar,** selecione **Seguinte**.

5. Na página **Password,** introduza a palavra-passe para a chave privada na caixa password e, em seguida, selecione **Seguinte**.  
  
   Selecione a opção para tornar a chave exportável.

6. Na **página**da Loja de Certificados, **escolha automaticamente o certificado com base no tipo de certificado**e, em seguida, selecione **Seguinte**.  

7. Selecione **Concluir**.

### <a name="export-the-certificate"></a>Exportar o certificado

Exporte o certificado de autenticação do *servidor CMG* a partir do seu servidor. A reexportação do certificado torna-o utilizável para o seu portal de gestão de nuvens em Azure.  

1. No servidor onde importou o certificado SSL público, execute **certlm.msc** para abrir a consola Do Gestor de Certificados.  

2. Na consola Do Gestor de Certificados, selecione **Certificados de > Pessoais**. Em seguida, clique à direita no certificado de autenticação do *servidor CMG* que inscreveu no procedimento anterior e, em seguida, selecione **Todas as Tarefas > Exportação**.  

3. No Certificado De Saúde-Exportador, selecione **Seguinte**, selecione **Sim, exporte a chave privada,** e depois **seguinte**.  

4. Na página formato de formato de ficheiros de exportação, selecione **Personal Information Exchange - PKCS #12 (. PFX)**, selecione **Next,** e forneça uma senha. Para o nome do ficheiro, especifique um nome como **C:\ConfigMgrCloudMGServer**. Vai fazer referência a este ficheiro quando criar o CMG em Azure.  

5. Selecione **A seguir**, e, em seguida, confirme as seguintes definições antes de selecionar **Terminar** para completar a exportação:  

   - Chaves de exportação = Sim  
   - Incluir todos os certificados na via de certificação = Sim  
   - Formato de ficheiro = Troca de Informações Pessoais (*.pfx)  

6. Depois de concluir a exportação, localize o ficheiro .pfx e coloque uma cópia no **c:\Certs** no servidor principal do site do Gestor de Configuração que irá gerir os clientes baseados na Internet. A pasta Certs é uma pasta temporária para usar ao mover certificados entre servidores. Acede ao ficheiro de certificado do servidor principal do site quando implementa a porta de entrada de gestão de nuvem para o Azure.  

Depois de copiar o certificado para o servidor do site principal, pode eliminar o Certificado da loja de CertificadoS Pessoais no servidor membro.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Ativar serviços de nuvem Azure em Gestor de Configuração

Para configurar os serviços Azure a partir da consola Do Gestor de Configuração, utilize o assistente de Serviços Configure Azure e crie duas aplicações azure Ative Directory (Azure AD).  

- **Aplicação server** – uma *aplicação Web* em Azure AD  
- **Aplicativo de** *cliente* – uma aplicação de Cliente Nativo em Azure AD  

Executar o seguinte procedimento a partir do servidor do site principal.  

1. A partir do servidor principal do site, abra a consola do Gestor de Configuração e vá à **Administração > Serviços Cloud > Serviços Azure,** e selecione **Configure Azure Services**.  

   Na página do Serviço Configure Azure, especifique um nome amigável para o serviço de gestão de nuvem que está a configurar. Por exemplo: O meu serviço de *gestão de nuvem.*

   Em seguida, selecione **Cloud Management**, e, em seguida, selecione **Next**.  

   > [!TIP]  
   > Para obter mais informações sobre as configurações que faz no assistente, consulte [Iniciar o assistente de Serviços Azure](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)

2. Na página 'Propriedades da **Aplicação',** para **aplicação Web,** selecione **Browse** para abrir o diálogo da **Aplicação do Servidor** e, em seguida, selecione **Criar**. Configure os seguintes campos:

   - **Nome da aplicação**: Especifique um nome amigável para a aplicação, como a *aplicação web Cloud Management*.  

   - **URL homePage**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por defeito, `https://ConfigMgrService`este valor é .  

   - **App ID URI**: Este valor tem de ser único no seu inquilino Azure AD. Está no sinal de acesso utilizado pelo cliente do Gestor de Configuração para solicitar o acesso ao serviço. Por defeito, `https://ConfigMgrService`este valor é .  

   Em seguida, selecione **Iniciar sessão**e especificar uma conta de Administrador Global Azure AD. Estas credenciais não são guardadas pelo Diretor de Configuração. Esta persona não requer permissões no Gestor de Configuração e não precisa de ser a mesma conta que gere o Assistente de Serviços Azure.

   Depois de iniciar sessão, o visor de resultados. Selecione **OK** para fechar o diálogo da Aplicação Create Server e volte à página De aplicações.

3. Para **a aplicação Cliente Nativo,** selecione **Browse** para abrir o diálogo da **aplicação Cliente.**

4. Selecione **Criar** para abrir o diálogo **Create Client Application** e, em seguida, configurar os seguintes campos:  

   - **Nome da aplicação**: Especifique um nome amigável para a aplicação, como a *aplicação de clientes nativos da Cloud Management*.

   - **URL de resposta**: Este valor não é utilizado pelo Gestor de Configuração, mas é exigido pelo Azure AD. Por defeito, `https://ConfigMgrClient`este valor é .
   Em seguida, selecione **Iniciar sessão**e especificar uma conta de Administrador Global Azure AD. Tal como a aplicação Web, estas credenciais não são guardadas e não requerem permissões no 'Gestor de Configuração'.

   Depois de iniciar sessão, os resultados são apresentados. Selecione **OK** para fechar o diálogo da Aplicação Do Cliente Criar e voltar à página App Properties. Em seguida, selecione **Next** para continuar.

5. Na página **Configurar as Definições** de Descoberta, verifique a caixa para ativar a Descoberta do Utilizador ativo do **Diretório Ativo,** selecione **Next**, e, em seguida, complete a configuração dos diálogos Discovery para o seu ambiente.  

6. Continue através das páginas Resumo, Progresso e Conclusão e, em seguida, feche o assistente.  

   Os Serviços Azure para a descoberta do Utilizador AD Azure estão agora ativados no Gestor de Configuração.  Deixe a consola aberta por enquanto.  

7. Abra um navegador e inscreva-se no [portal Azure.](https://portal.azure.com/)  

8. Selecione **todos os serviços > Registos de > App do Diretório Ativo do Azure,** e depois:

   1. Selecione a aplicação Web que criou.

   2. Vá a **Definições > Permissões Necessárias,** selecione **permissões de concessão**e, em seguida, selecione **Sim**.  

   3. Selecione a aplicação Cliente Nativo que criou.

   4. Vá a **Definições > Permissões Necessárias,** selecione **permissões de concessão**e, em seguida, selecione **Sim**.  

9. Na consola de Configuração Manager, vá à **Administração > visão geral > Serviços de Nuvem > Serviços Azure,** e selecione o seu Serviço Azure. Em seguida, clique à direita no **Utilizador de Diretório Ativo Azure Discover** e selecione Executar Full Discovery **Now**. Selecione **Sim** para confirmar a ação.  

10. No servidor do site principal, abra o Gestor de Configuração **SMS_AZUREAD_DISCOVERY_AGENT.log** e procure a seguinte entrada para confirmar que a descoberta está a funcionar: *UDX publicado com sucesso para utilizadores de Diretório Ativo Azure*  

    Por predefinição, o ficheiro de registo está em *%Program_Files%\Microsoft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Crie os serviços de nuvem em Azure

**Nesta secção do tutorial irá:**

- Crie o serviço de nuvem CMG  
- Criar registos DNS CNAME para ambos os serviços  

### <a name="create-the-cmg"></a>Criar o CMG

Utilize este procedimento para instalar um portal de gestão de nuvem como serviço em Azure. A CMG instala-se no local de topo da hierarquia. Neste tutorial, continuamos a utilizar o local primário onde os certificados foram matriculados e exportados.

1. No servidor principal do site, abra a consola do Gestor de Configuração e, em seguida, vá **administração > visão geral > Cloud Services > Cloud Management Gateway**, e, em seguida, selecione Create Cloud Management **Gateway**.  

2. Na página **Geral**:  

   1. Selecione o seu ambiente em nuvem para **ambiente Azure**. Este tutorial utiliza **o AzurePublicCloud.**  

   2. Selecione **implementação do Gestor de Recursos Azure**.  
  
   3. **Inscreva-se na** sua assinatura Azure. O Gestor de Configuração preenche informações adicionais com base nas informações que configuraste quando ativou os serviços de nuvem Azure para O Gestor de Configuração.  

   Selecione **Seguinte** para continuar.  

3. Na página **Definições,** navegue e selecione o ficheiro denominado **ConfigMgrCloudMGServer.pfx,** que é o ficheiro que exportou após importar o certificado de autenticação do servidor CMG. Depois de especificar a palavra-passe, o nome do **Serviço** e o nome de **implantação** preenchem automaticamente, com base nos detalhes do ficheiro de certificado .pfx.

4. Desloque a sua **Região.**

5. Para **o Grupo de Recursos,** utilize um grupo de recursos existente ou crie um grupo com um nome amigável que não utilize espaços, como **cofigMgrCloudServices**. Se optar por criar um grupo, o grupo é adicionado como um grupo de recursos em Azure.  

6. A menos que esteja pronto para configurar à escala, utilize um (1) para o número de **Instâncias VM**. O número de Casos VM permite que um único serviço cloud management Gateway (CMG) Cloud para escalar para suportar mais ligações de clientes. Mais tarde, pode utilizar a consola 'Gestor de Configuração' para devolver e editar o número de casos vm que utiliza.  

7. Ative a caixa de verificação para verificar a **revogação do certificado**de cliente.

8. Ative a caixa de verificação para permitir que a CMG funcione como um ponto de distribuição em **nuvem e sirva conteúdo do armazenamento Azure** se pretender implantar um ponto de distribuição em nuvem com o CMG.

9. Selecione **Seguinte** para continuar.

10. Reveja os valores na página **alerta** e, em seguida, selecione **Next**.

11. Reveja a página **Sumária** e clique **em Next** para criar o serviço cloud management gateway Cloud Service. Selecione **Perto** para completar o Assistente.  

12. No nó Gateway de Cloud Management da consola De Configuração Manager, já pode ver o novo serviço.  

### <a name="create-dns-cname-records"></a>Criar registos DNS CNAME

Quando cria uma entrada DNS para o CMG, permite que os seus dispositivos Windows 10, tanto dentro como fora da sua rede corporativa, utilizem resolução de nomes para encontrar o serviço de nuvem CMG em Azure.

O nosso exemplo de registo CNAME utiliza os seguintes detalhes:  

- O nome da empresa é **Contoso** com um espaço público de nome DNS de ***Contoso.com.***  

- O nome de serviço CMG é **MyCMG,** que se torna ***MyCMG.CloudApp.Net*** em Azure.  

Exemplo de registo CNAME: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configure o ponto de gestão e os clientes para usar o CMG

Configure configurações que permitem que pontos de gestão no local e clientes utilizem o gateway de gestão de nuvem.

Como utilizamos o Enhanced HTTP para comunicações com clientes, não há necessidade de utilizar um ponto de gestão HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Criar o ponto de ligação CMG

Configure o site para suportar o HTTP melhorado.  

1. Na consola do Gestor de Configuração, vá à **Administração > visão geral > Configuração**do Site > Sites, e abra as propriedades do site principal.  

2. No separador comunicação do **computador cliente,** selecione a opção *HTTPS ou HTTP* para utilizar os certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP**e, em seguida, selecione **OK** para guardar a configuração.

    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

3. Agora vá ao > > Configuração do Site > Funções de Sistema de > e **servidores e sistema** de site e selecione o servidor com um ponto de gestão onde pretende instalar o ponto de ligação de gateway de gestão da nuvem.  

4. **Selecione Adicionar funções**do sistema do site, e **depois**> **seguinte**.  

5. Selecione o ponto de ligação de gateway de **gestão cloud** e, em seguida, selecione **Next** para continuar.  

6. Reveja as seleções predefinidas na página de ponto de ligação de gateway de **gestão** cloud e certifique-se de que o CMG correto é selecionado. Se tiver vários gateways de gestão de nuvem, pode utilizar a lista de dropdown para especificar um CMG diferente. Também pode alterar o CMG em utilização, após a instalação. Selecione **Seguinte** para continuar.

7. Selecione **Next** para iniciar a instalação e, em seguida, ver os resultados na página Conclusão.  Selecione **Perto** para completar a instalação do ponto de ligação.

8. Agora vá à **Administração > visão geral > configuração do site > Servidores e Funções** do Sistema do Site e abra as **Propriedades** para o ponto de gestão onde instalou o ponto de ligação. No separador **Geral,** verifique a caixa para permitir o tráfego de gateway de gateway de gestão de nuvem do Gestor de **Configuração,** e, em seguida, selecione **OK** para salvar a configuração.
   > [!TIP]  
   > Apesar de não ser necessário para permitir a cogestão, recomendamos que faça esta mesma edição para quaisquer pontos de atualização de software.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Configure as Definições de Cliente para direcionar os clientes para usar o CMG

Utilize as Definições do Cliente para configurar os clientes do Gestor de Configuração para comunicar com o CMG.  

1. Abra a consola do Gestor de **Configuração > Administração > visão geral > Definições**do cliente, e depois editar as **Definições padrão do cliente**.  

2. Selecione **Serviços cloud**.

3. Na página **Definições Predefinidas,** delineie as seguintes definições para = **Sim**.  

   - **Registar automaticamente novos dispositivos de domínio Windows 10 com Diretório Ativo Azure**  

   - **Permitir que os clientes utilizem um portal de gestão de nuvem**

   - **Permitir o acesso ao ponto de distribuição em nuvem**

4. Na página Política do **Cliente,** delineie **os pedidos de política do utilizador dos clientes** = da Internet**Sim**.

5. Selecione **OK** para guardar esta configuração.

## <a name="enable-co-management-in-configuration-manager"></a>Ativar a cogestão no Gestor de Configuração

Com as configurações do Azure, as funções do sistema do site e as configurações do cliente no lugar, pode configurar o Gestor de Configuração para permitir a cogestão. No entanto, ainda terá de fazer algumas configurações em Intune depois de permitir a cogestão antes de este tutorial estar completo. Uma dessas tarefas é configurar o Intune para implementar o cliente do Gestor de Configuração. Esta tarefa é facilitada através da poupança da linha de comando para implementação do cliente que está disponível dentro do Assistente de Configuração de Cogestão. É por isso que agora permitimos a cogestão, antes de completarmos as configurações para Intune.

> [!TIP]
> - Quando ativar a cogestão, atribuirá uma coleção como *grupo Piloto*. Este é um grupo que contém um pequeno número de clientes para testar as suas configurações de cogestão. Recomendamos que crie uma coleção adequada antes de iniciar o procedimento. Em seguida, pode selecionar essa coleção sem sair do procedimento para o fazer.
> - A partir da versão 1906 do Gestor de Configuração, poderá necessitar de várias coleções, uma vez que pode atribuir um *grupo Piloto* diferente para cada carga de trabalho.

### <a name="enable-co-management-starting-in-version-1906"></a>Permitir a cogestão a partir da versão 1906

Para permitir a cogestão a partir da versão 1906 do Gestor de Configuração, siga as instruções abaixo:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Permitir a cogestão na versão 1902 e anterior

Para permitir a cogestão para a versão 1902 e anterior do Gestor de Configuração, siga as instruções abaixo:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Use Intune para implementar o cliente de Gestor de Configuração

Pode utilizar o Intune para instalar o cliente Do Gestor de Configuração em dispositivos Windows 10 que atualmente só são geridos com o Intune.  

Em seguida, quando um dispositivo Windows 10 anteriormente não gerido se inscreve no Intune, instala automaticamente o cliente Do Gestor de Configuração.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Criar uma aplicação Intune para instalar o cliente do Gestor de Configuração

1. A partir do servidor principal do site, inscreva-se no [portal Azure](https://portal.azure.com/) e vá às **aplicações intune > Cliente > Apps > Add**.

2. Para o tipo de **aplicações**: Selecione **app Line-of-business**.

3. Selecione ficheiro de pacote de **aplicativos**, e, em seguida, navegue para a localização do ficheiro 'Gestor de Configuração **ccmsetup.msi'** e, em seguida, selecione **Abrir > OK**.
Por exemplo, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*

4. Selecione Informações de **aplicações**e, em seguida, especifique os seguintes detalhes:
   - **Descrição**: Cliente do Gestor de Configuração  

   - **Editor**: Microsoft  

   - **Argumentos da linha de comando**: * \<Especifique a linha de comando **CCMSETUPCMD.** Pode utilizar a linha de comando que guardou na* página de ativação do Assistente de Configuração de *Cogestão. Esta linha de comando inclui os nomes do seu serviço na nuvem e valores adicionais que permitem aos dispositivos instalar o software cliente Do Gestor de Configuração.>*  

     A estrutura da linha de comando deve assemelhar-se a este exemplo utilizando apenas os parâmetros CCMSETUPCMD e SMSSiteCode:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Se não tiver a linha de comando disponível, pode visualizar as propriedades de *CoMgmtSettingsProd* na consola 'Gestor de Configuração' para obter uma cópia da linha de comando.

5. Selecione **OK > Adicionar**.  A aplicação é criada e fica disponível na consola Intune. Depois de a aplicação estar disponível, pode utilizar a seguinte secção para configurar o Intune para atribuí-la aos dispositivos do Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Atribuir a app Intune para instalar o cliente do Gestor de Configuração

O procedimento seguinte implementa a aplicação para instalar o cliente Do Gestor de Configuração que criou no procedimento anterior.

1. Inicie sessão no [portal do Azure](https://portal.azure.com/).  Selecione **todos os serviços > Intune > Aplicações do Cliente > Apps**, e, em seguida, selecione **ConfigMgr Client Setup Bootstrap**, a app que criou para implementar o cliente De Configuração Manager.  

2. Selecione **Atribuições > Adicionar grupo**.  Definir **o tipo** de atribuição como **necessário**, e depois utilizar **Grupos Incluídos** e **Grupos Excluídos** para definir os grupos de Diretório Ativo Azure (AD) que têm utilizadores e dispositivos que pretende participar na cogestão.  

3. Selecione **OK** e, em seguida, **guarde** a configuração.
A aplicação é agora exigida pelos utilizadores e dispositivos a que a atribuiu. Depois de a aplicação instalar o cliente do Gestor de Configuração num dispositivo, é gerido por cogestão.

## <a name="summary"></a>Resumo

Depois de completar os passos de configuração deste tutorial, pode começar a cogerir os seus dispositivos.

## <a name="next-steps"></a>Passos seguintes

- Reveja o estado dos dispositivos cogeridos com o painel de [cogestão](how-to-monitor.md)
- Utilize o [Windows Autopilot](quickstart-autopilot.md) para fornecer novos dispositivos
- Utilizar [regras de acesso condicional](quickstart-conditional-access.md) e conformidade insinapara gerir o acesso dos utilizadores aos recursos corporativos
