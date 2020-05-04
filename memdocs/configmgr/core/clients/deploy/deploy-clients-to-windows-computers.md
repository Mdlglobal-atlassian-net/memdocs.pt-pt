---
title: Implementar clientes para windows
titleSuffix: Configuration Manager
description: Saiba como implementar o cliente do Gestor de Configuração para computadores Windows.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07c5488b0ea28f37f7f8a07b532c67fb64aad810
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713430"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Como implementar clientes para computadores Windows em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece detalhes sobre como implementar o cliente do Gestor de Configuração para computadores Windows. Para obter mais informações sobre planeamento e preparação para a implementação do cliente, consulte estes artigos:

- [Métodos de instalação de cliente](plan/client-installation-methods.md)  
- [Pré-requisitos para implementar clientes em computadores Windows](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Segurança e privacidade para clientes do Gestor de Configuração](plan/security-and-privacy-for-clients.md)  
- [Melhores práticas para a implementação do cliente](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a>Instalação push do cliente

Existem três formas principais de usar o impulso do cliente:  

- Quando configura a instalação push do cliente para um site, a instalação do cliente funciona automaticamente em computadores que o site descobre. Este método é traçado para os limites configurados do site quando esses limites são configurados como um grupo de limites.  

- Inicie a instalação push do cliente executando o Assistente de Instalação push do cliente para uma recolha ou recurso específico dentro de uma coleção.  

- Utilize o Assistente de Instalação de Impulso do Cliente para instalar o cliente Do Gestor de Configuração, que pode utilizar para [consultar](../../servers/manage/introduction-to-queries.md) o resultado. A instalação só terá sucesso se um dos itens devolvidos pela consulta for o atributo **ResourceID** da classe Recursos do **Sistema.**

Se o servidor do site não conseguir contactar o computador cliente ou iniciar o processo de configuração, ele automaticamente retenta a instalação a cada hora. O servidor continua a tentar novamente por até sete dias.  

Para ajudar a acompanhar o processo de instalação do cliente, instale um ponto de estado de recuo antes de instalar os clientes. Quando instala um ponto de estado de recuo, é automaticamente atribuído aos clientes quando são instalados pelo método de instalação push do cliente. Para acompanhar o progresso da instalação do cliente, consulte os relatórios de implantação e atribuição do cliente.

Os ficheiros de registo do cliente fornecem informações mais detalhadas para resolução de problemas. Os ficheiros de registo não requerem um ponto de estado de recuo. Por exemplo, o ficheiro CCM.log no servidor do site regista quaisquer problemas que ocorram quando o servidor do site se conecta ao computador. O ficheiro CCMSetup.log no cliente regista o processo de instalação.  

> [!IMPORTANT]  
> O impulso do cliente só tem sucesso se todos os pré-requisitos forem cumpridos. Para mais informações, consulte dependências do método de [instalação](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configure o site para utilizar automaticamente o impulso do cliente para computadores descobertos

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site para o qual pretende configurar a instalação automática de impulso seletiva do cliente em todo o site.  

3. No separador **Casa** da fita, no grupo **Definições,** selecione Definições de **Instalação do Cliente**, e, em seguida, selecione a **instalação de impulso**do cliente .  

4. No separador **Geral** da janela Propriedades de Instalação push do cliente, selecione **Ativar a instalação automática de impulsos**do cliente em todo o site .

5. A partir da versão 1806, quando atualizar o site, está ativado um check-up Kerberos para obter pressão do cliente. A opção de permitir o recuo da **ligação ao NTLM** é ativada por padrão, o que é consistente com o comportamento anterior. Se o site não conseguir autenticar o cliente utilizando a Kerberos, ele retenta a ligação utilizando a NTLM. A configuração recomendada para uma melhor segurança é desativar esta definição, que requer Kerberos sem recuo ntLM.<!--1358204-->  

    > [!NOTE]  
    > Quando utiliza o impulso do cliente para instalar o cliente do Gestor de Configuração, o servidor do site cria uma ligação remota ao cliente. A partir da versão 1806, o site pode exigir a autenticação mútua kerberos, não permitindo o recuo à NTLM antes de estabelecer a ligação. Esta melhoria ajuda a garantir a comunicação entre o servidor e o cliente.  
    >
    > Dependendo das suas políticas de segurança, o seu ambiente pode já preferir ou exigir kerberos em vez da autenticação NTLM mais antiga. Para obter mais informações sobre as considerações de segurança destes protocolos de autenticação, leia sobre a definição da política de [segurança do Windows para restringir a NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Para utilizar esta funcionalidade, os clientes devem estar numa floresta de Diretório Ativo de confiança. Kerberos no Windows conta com Diretório Ativo para autenticação mútua.  

6. Selecione os tipos de sistema para os quais o Gestor de Configuração deve empurrar o software do cliente. Selecione se pretende instalar o cliente em controladores de domínio.  

7. No separador **Contas,** especifique uma ou mais contas para o Gestor de Configuração utilizar quando se ligar ao computador-alvo. Selecione o ícone **Criar,** introduza o nome de **utilizador** e **a palavra-passe** (não mais de 38 caracteres), confirme a palavra-passe e, em seguida, selecione **OK**. Especifique pelo menos uma conta de instalação push do cliente. Esta conta deve ter direitos de administrador local no computador alvo para instalar o cliente. Se não especificar uma conta de instalação push do cliente, o Gestor de Configuração tenta utilizar a conta de computador do sistema do site. O impulso do cliente de domínio cruzado falha ao utilizar a conta de computador do sistema do site.  

    > [!NOTE]  
    > Para utilizar o impulso do cliente a partir de um site secundário, especifique a conta no site secundário que inicia o impulso do cliente.  
    >
    > Para mais informações sobre a conta de instalação push do cliente, consulte o procedimento seguinte, [Use o Assistente de Instalação push do cliente](#use-the-client-push-installation-wizard).  

8. Especifique quaisquer propriedades de instalação necessárias no separador Propriedades de **Instalação.**

    Se estendeu o esquema de Diretório Ativo para Gestor de Configuração, o site publica as propriedades de [instalação](about-client-installation-properties.md) especificadas para Serviços de Domínio de Diretório Ativo. Quando o CCMSetup funciona sem propriedades de instalação, lê estas propriedades a partir do Diretório Ativo.  

    > [!NOTE]  
    > Se ativar a instalação de impulso do cliente num site secundário, detete a propriedade **SMSSITECODE** para o código de site do Gestor de Configuração do seu site principal principal. Se estendeu o esquema de Diretório Ativo para O Gestor de Configuração, para encontrar automaticamente a atribuição correta do site, defina esta propriedade para **AUTO**.

### <a name="use-the-client-push-installation-wizard"></a>Utilize o assistente de instalação push do cliente

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site para o qual pretende configurar a instalação automática de impulso seletiva do cliente em todo o site.  

3. No separador **Casa** da fita, no grupo **Definições,** selecione Definições de **Instalação do Cliente**, e, em seguida, selecione a **instalação de impulso**do cliente .  

4. Especifique quaisquer propriedades de instalação necessárias no separador Propriedades de **Instalação.**  

    Se estendeu o esquema de Diretório Ativo para Gestor de Configuração, o site publica as propriedades de [instalação](about-client-installation-properties.md) especificadas para Serviços de Domínio de Diretório Ativo. Quando o CCMSetup funciona sem propriedades de instalação, lê estas propriedades a partir do Diretório Ativo.

5. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.**  

6. No nó dos **Dispositivos,** selecione um ou mais computadores. Ou selecione uma coleção de computadores no nó de **Recolha de Dispositivos.**  

7. No separador **Home** da fita, escolha uma destas opções:  

    - Para empurrar o cliente para um ou mais dispositivos, no grupo **Dispositivo,** selecione **Instalar cliente**.  

    - Para empurrar o cliente para uma coleção de dispositivos, no grupo **Coleção,** selecione **Instalar cliente**.  

8. Na página **Antes de Iniciar** o Cliente do Gestor de Configuração, reveja as informações e, em seguida, selecione **Next**.  

9. Selecione as opções adequadas na página Opções de **Instalação.**  

10. Reveja as definições de instalação e, em seguida, complete o assistente.  

> [!NOTE]  
> Utilize este assistente para instalar clientes mesmo que o site não esteja configurado para empurrar o cliente.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a>Instalação baseada em atualização de software  

A instalação de clientes baseada em atualizações de software publica o cliente num ponto de atualização de software como uma atualização de software. Utilize este método para uma primeira instalação ou atualização.  

Se o cliente do Gestor de Configuração for instalado num computador, o computador recebe a política do cliente a partir do site. Esta política inclui o nome do servidor de pontode atualização de software e a porta a partir da qual obter atualizações de software.

> [!IMPORTANT]  
> Para a instalação baseada em atualizações de software, utilize o mesmo servidor do Windows Server Update Services (WSUS) para atualizações de instalação e software do cliente. Este servidor deverá ser o ponto de atualização de software ativo num site primário. Para mais informações, consulte [Instale um ponto](../../../sum/get-started/install-a-software-update-point.md)de atualização de software .

Se o cliente do Gestor de Configuração não estiver instalado num computador, configure e atribua um Objeto de Política de Grupo. A Política de Grupo especifica o nome do servidor do ponto de atualização do software.  

Não é possível adicionar propriedades da linha de comando a uma instalação de cliente baseada em atualizações de software. Se estendeu o esquema de Diretório Ativo para Gestor de Configuração, a instalação do cliente consulta automaticamente os Serviços de Domínio do Diretório Ativo para as propriedades de instalação.  

Se não alargou o esquema de Diretório Ativo, utilize a Política do Grupo para fornecer definições de instalação de clientes. Estas definições são automaticamente aplicadas a qualquer instalação de cliente baseada em atualizações de software. Para mais informações, consulte a secção de [como fornecer propriedades de instalação de clientes](#BKMK_Provision) e o artigo sobre como atribuir clientes a um [site](assign-clients-to-a-site.md).  

Utilize os seguintes procedimentos para configurar computadores sem um cliente do Gestor de Configuração para utilizar o ponto de atualização do software. Há também um procedimento para publicar o software do cliente no ponto de atualização de software.  

> [!TIP]  
> Se os computadores estiverem em estado de reinício pendente após uma instalação de software anterior, uma instalação de cliente baseada em atualizações de software pode fazer com que o computador reinicie.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configure um Objeto de Política de Grupo para especificar o ponto de atualização do software  

1. Utilize a Consola de **Gestão** de Políticas de Grupo para abrir um novo ou existente Objeto de Política de Grupo.  

2. Expandir **a configuração do computador,** **os modelos administrativos**e os **componentes do Windows,** e depois selecionar a **atualização do Windows.**  

3. Abra as propriedades da definição **Especifique**a localização do serviço de atualização intranet microsoft , e depois selecione **Ativado**.  

4. **Detete o serviço de atualização intranet para detetar atualizações**: Especifique o nome e a porta do servidor de pontos de atualização do software.  

    - Se configurar o sistema de site do Gestor de Configuração para utilizar um nome de domínio totalmente qualificado (FQDN), utilize esse formato.  

    - Se o sistema de site do Gestor de Configuração não estiver configurado para utilizar um FQDN, utilize um formato de nome curto.

    > [!TIP]  
    > Para determinar o número da porta, consulte [Como determinar as definições de porta utilizadas pela WSUS](../../../sum/plan-design/plan-for-software-updates.md).

    Exemplo no formato FQDN:`http://server1.contoso.com:8530`  

5. **Defina o servidor de estatísticas intranet**: Esta definição é tipicamente configurada com o mesmo nome de servidor.

6. Atribuir o Objeto de Política de Grupo aos computadores nos quais pretende instalar o cliente e receber atualizações de software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publique o cliente do Gestor de Configuração no ponto de atualização de software  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site para o qual pretende configurar a instalação de clientes baseada em atualizações de software.  

3. No separador **Home** da fita, no grupo **Definições,** selecione Definições de **Instalação do Cliente**, e, em seguida, selecione a **instalação do cliente baseado em atualizações de software**.  

4. **Selecione ativar a instalação do cliente baseado em atualizações de software.**  

5. Se a versão cliente do site for mais recente do que a versão no ponto de atualização do software, abre-se a caixa de diálogo detetada pela **Versão Posterior do Pacote cliente.** Selecione **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    > Se ainda não publicou o software do cliente no ponto de atualização de software, esta caixa de diálogo está em branco.

A atualização de software para o cliente do Gestor de Configuração não é atualizada automaticamente quando há uma nova versão. Quando atualizar o site, repita este procedimento para atualizar o cliente.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a>Instalação política de grupo

Utilize a Política de Grupo nos Serviços de Domínio de Diretório Ativo para publicar ou atribuir o cliente do Gestor de Configuração. O cliente instala-se quando o computador começa. Quando utiliza a Política de Grupo, o cliente aparece em **Adicionar ou Remover Programas** no Painel de Controlo. O utilizador pode instalá-lo a partir daí.  

Utilize o pacote do Instalador windows CCMSetup.msi para instalações baseadas em políticas de grupo. Este ficheiro encontra-se na `<ConfigMgr installation directory>\bin\i386` pasta no servidor do site. Não é possível adicionar propriedades a este ficheiro para alterar o comportamento da instalação.  

> [!IMPORTANT]  
> Deve ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

- Se este nitido estendeu o esquema de Diretório Ativo para Gestor de Configuração, e selecionou o domínio no separador **Editorial** da caixa de diálogo **Do Site Properties,** os computadores clientes procuram automaticamente serviços de domínio de diretório ativo para propriedades de instalação. Para mais informações, consulte sobre as propriedades de [instalação do cliente publicadas nos Serviços de Domínio de Diretório Ativo.](about-client-installation-properties-published-to-active-directory-domain-services.md)  

- Se não tiver ampliado o esquema de Diretório Ativo, consulte a secção sobre o fornecimento de propriedades de [instalação](#BKMK_Provision) de clientes para obter informações sobre o armazenamento de propriedades de instalação no registo windows de computadores. O cliente utiliza estas propriedades de instalação quando instala.  

Para mais informações, consulte Como utilizar a Política de [Grupo para instalar remotamente o software](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a>Instalação manual

Instale manualmente o software do cliente nos computadores utilizando CCMSetup.exe. Pode encontrar este programa e os seus ficheiros de suporte na pasta Cliente na pasta de instalação do Gestor de Configuração no servidor do site. O site partilha esta pasta para a rede como:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>`é o nome principal do servidor do site. `<site code>`é o código principal do site ao qual o cliente é atribuído. Para executar CCMSetup.exe a partir da linha de comando do cliente, ligue-se a esta localização da rede e, em seguida, executar o comando.  

> [!IMPORTANT]  
> Deve ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e liga para o pacote Instalador do Windows (Client.msi) para instalar o cliente. Não pode dirigir o Cliente.msi diretamente.  

Para modificar o comportamento da instalação do cliente, especifique as opções da linha de comando tanto para ccMSetup.exe como Client.msi. Certifique-se de que especifica os parâmetros `/` CCMSetup que começam antes de especificar as propriedades do Cliente.msi. Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

Neste exemplo, o cliente instala com as seguintes opções:  

|Opção|Descrição|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Este parâmetro CCMSetup especifica o ponto de gestão SMSMP01 para descarregar os ficheiros de instalação do cliente necessários.|  
|`/logon`|Este parâmetro CCMSetup especifica que a instalação deve parar se um cliente do Gestor de Configuração existente for encontrado no computador.|  
|`SMSSITECODE=AUTO`|Esta propriedade Client.msi especifica que o cliente tenta localizar o código de site do Gestor de Configuração para usar, utilizando serviços de domínio de diretório ativo, por exemplo.|  
|`FSP=SMSFP01`|Esta propriedade Client.msi especifica que o ponto de estado de recuo chamado SMSFP01 é usado para receber mensagens estatais enviadas do computador cliente.|  

Para mais informações, consulte sobre os parâmetros e propriedades de [instalação do cliente.](about-client-installation-properties.md)  

> [!TIP]  
> Para que o procedimento instale o cliente do Gestor de Configuração num dispositivo moderno do Windows 10 utilizando a identidade do Diretório Ativo Azure (Azure AD), consulte instalar e atribuir clientes do Gestor de [Configuração do Windows 10 utilizando a AD Azure para autenticação.](deploy-clients-cmg-azure.md) Este procedimento é para clientes numa intranet ou na internet.  

### <a name="manual-installation-examples"></a>Exemplos de instalação manual

Estes exemplos são para clientes ligados ao Diretório Ativo numa intranet. Utilizam os seguintes valores:  

- **MPSERVER**: servidor que acolhe o ponto de gestão
- **FSPSERVER**: servidor que acolhe o ponto de estado do recuo  
- **ABC**: código de site  
- **contoso.com**: nome de domínio  

Assuma que configurou todos os servidores do sistema do site com uma Intranet FQDN e publicou as informações do site para Ative Directory.  

Comece com os seguintes passos no computador cliente:  

1. Inscreva-se como administrador local.  
2. Unidade de `\\MPSERVER\SMS_ABC\Client`mapa Z para .  
3. Mude o pedido de comando para dirigir Z.  

Em seguida, executar um dos seguintes comandos:  

#### <a name="manual-example-1"></a>Exemplo manual 1  

`CCMSetup.exe`  

Este comando instala o cliente sem parâmetros ou propriedades adicionais. O cliente é configurado automaticamente com as propriedades de instalação do cliente publicadas nos Serviços de Domínio do Diretório Ativo, incluindo estas configurações:  

- Código do site: Esta definição requer que a localização da rede do cliente seja incluída num grupo de limites que configurapara a atribuição do cliente.  
- Ponto de gestão.
- Ponto de estado de recuo.
- Comunicar apenas com HTTPS.  

Para mais informações, consulte sobre as propriedades de [instalação do cliente publicadas nos Serviços de Domínio de Diretório Ativo.](about-client-installation-properties-published-to-active-directory-domain-services.md)  

#### <a name="manual-example-2"></a>Exemplo manual 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Este comando sobrepõe-se à configuração automática que os Serviços de Domínio de Diretório Ativo fornecem. Não requer que inclua a localização da rede do cliente num grupo de limites configurado para atribuição de clientes. Em vez disso, a instalação especifica estas definições:

- Código do site
- Ponto de gestão intranet
- Ponto de gestão baseado na Internet
- Ponto de estado de recuo que aceita ligações da internet
- Utilize um certificado de infraestrutura de chave pública do cliente (PKI) (se disponível) que tenha o período de validade mais longo

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a>Instalação de script son

O Gestor de Configuração suporta a utilização de scripts de logon para instalar o software cliente do Gestor de Configuração. Utilize o ficheiro do programa CCMSetup.exe num script de logon para desencadear a instalação do cliente.  

A instalação com script de início de sessão utiliza os mesmos métodos da instalação manual de cliente. Especifique o parâmetro de `/logon` instalação para CCMSsetup.exe. Se alguma versão do cliente já existir no computador, este parâmetro impede o cliente de instalar. Este comportamento impede a reinstalação do cliente sempre que o script de logon é executado.  

Se não especificar uma fonte de `/Source` instalação utilizando o parâmetro e nenhum ponto de `/MP` gestão a partir do qual a instalação é especificado pelo parâmetro, ccMSetup.exe localiza o ponto de gestão pesquisando Ative Directory Domain Services. Este comportamento só ocorre se tiver ampliado o esquema para O Gestor de Configuração e publicado o site para Ative Directory Domain Services. Em alternativa, o cliente pode utilizar DNS ou WINS para localizar um ponto de gestão.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a>Instalação de pacotes e programas

Utilize o Gestor de Configuração para criar e implementar um pacote e programa que atualize o software do cliente para dispositivos selecionados. O Gestor de Configuração fornece um ficheiro de definição de pacote que povoa as propriedades do pacote com valores tipicamente utilizados. Personalize o comportamento da instalação do cliente especificando parâmetros e propriedades adicionais da linha de comando.  

> [!NOTE]  
> Não é possível atualizar os clientes do Gestor de Configuração 2007 utilizando este método. Em vez disso, utilize a atualização automática de cliente, que cria e implementa automaticamente um pacote com a versão mais recente do cliente. Para mais informações, consulte [os clientes de Upgrade](../manage/upgrade/upgrade-clients.md).  
>
> Para obter mais informações sobre como migrar de versões mais antigas do cliente do Gestor de Configuração, consulte Planeamento de uma estratégia de [migração de clientes.](../../migration/planning-a-client-migration-strategy.md)  

### <a name="create-a-package-and-program-for-the-client-software"></a>Criar um pacote e programa para o software do cliente  

Utilize o seguinte procedimento para criar um pacote e programa de Configuração Manager que pode implementar para computadores clientes do Gestor de Configuração para atualizar o software do cliente.  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Pacotes.**  

2. No separador **Casa** da fita, no grupo **Criar,** selecione **Criar pacote a partir de Definição**.  

3. Na página **Definição** de Pacote do assistente, selecione a **Microsoft** da lista **de Editores** e selecione Upgrade de Cliente do Gestor de **Configuração** da lista de definição de **Pacote.**  

4. Na página **Ficheiros Fonte,** selecione **Sempre obtenha ficheiros a partir de uma pasta fonte**.  

5. Na página **da Pasta Fonte,** selecione **o caminho da rede (Nome UNC)**. Em seguida, introduza o caminho de rede do servidor e partilhe que contenha os ficheiros de instalação do cliente.  

    > [!NOTE]  
    > O computador em que funciona a implementação do Gestor de Configuração deve ter acesso à pasta de rede especificada. Caso contrário, a instalação do cliente falha.  

    Para alterar qualquer uma das propriedades de instalação do cliente, modifique a linha de comando CCMSetup.exe no separador **Geral** do agente de configuração caixa de diálogo **de atualização silenciosa Propriedades.** As propriedades de `/noservice SMSSITECODE=AUTO`instalação predefinidas são .  

6. Distribua o pacote por todos os pontos de distribuição que pretende que alojem o pacote de atualização de cliente. Em seguida, implemente o pacote para coleções de dispositivos que contenham clientes que pretende fazer upgrade.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a>Dispositivos Windows geridos pelo MDM intune

Implemente o cliente do Gestor de Configuração para dispositivos matriculados com o Microsoft Intune.

Este procedimento é para um cliente tradicional que está ligado a uma intranet. Utiliza métodos tradicionais de autenticação do cliente. Para garantir que o dispositivo permanece em estado gerido após a instalação do cliente, este deve estar na intranet e dentro do limite do site do Gestor de Configuração.  

Para que o procedimento instale o cliente do Gestor de Configuração num dispositivo moderno do Windows 10 utilizando a identidade Azure AD, consulte instalar e atribuir clientes do Gestor de [Configuração do Windows 10 utilizando a AD Azure para autenticação.](deploy-clients-cmg-azure.md)

Depois de instalar o cliente do Gestor de Configuração, os dispositivos não se matriculam no Intune. Podem utilizar o cliente do Gestor de Configuração e a inscrição de MDM ao mesmo tempo. Para mais informações, consulte a [visão geral da cogestão.](../../../comanage/overview.md)  

> [!Note]
> Pode utilizar outros métodos de instalação do cliente para instalar o cliente do Gestor de Configuração num dispositivo gerido por Intune. Por exemplo, se um dispositivo gerido pela Intune estiver na intranet e se juntar ao domínio do Diretório Ativo, pode utilizar a política do grupo para instalar o cliente do Gestor de Configuração.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Instale o cliente do Gestor de Configuração utilizando o Intune

1. Intune, [adicione uma aplicação de linha de negócio do Windows](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) que contém o ficheiro de instalação do cliente Do Gestor de Configuração **CCMSetup.msi**. Pode encontrar este ficheiro `\bin\i386` na pasta do diretório de instalação do Gestor de Configuração no servidor do site.  

2. Na Intune Software Publisher, introduza parâmetros de linha de comando. Por exemplo, utilize este comando com um cliente tradicional numa intranet:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Para um exemplo de um comando a utilizar com um cliente moderno do Windows 10 usando a autenticação Azure AD, consulte [como preparar dispositivos baseados na Internet para cogestão](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Atribuir a aplicação](https://docs.microsoft.com/mem/intune/apps/apps-deploy) a um grupo de computadores Windows matriculados.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a>Instalação de imagem osso

Pré-instale o cliente do Gestor de Configuração num computador de referência que utiliza para criar uma imagem de OS.

> [!IMPORTANT]  
> Quando utiliza a sequência de tarefas do Gestor de Configuração para implementar uma imagem de OS, o passo [do Cliente Prepare ConfigMgr](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) remove completamente o cliente do Gestor de Configuração.  

### <a name="prepare-the-client-computer-for-imaging"></a>Prepare o computador cliente para imagens  

1. Instale manualmente o software cliente do Gestor de Configuração no computador de referência. Para mais informações, consulte [como instalar os clientes do Gestor de Configuração manualmente](#BKMK_Manual).  

    > [!IMPORTANT]  
    > Não especifique um código de site do Gestor de Configuração para o cliente nas propriedades da linha de comando CCMSetup.exe.  

2. Num pedido de `net stop ccmexec` comando, digite para parar o serviço de hospedeiro do agente SMS (CcmExec.exe) no computador de referência.  

3. Eliminar o SMSCFG. Ficheiro INI da pasta Windows no computador de referência.  

4. Remova quaisquer certificados armazenados na loja de computadorlocal no computador de referência. Por exemplo, se utilizar certificados PKI, antes de imagem do computador, remova os certificados na loja **Pessoal** para **Computador** e **Utilizador**.  

5. Se os clientes forem instalados numa hierarquia de Gestor de Configuração diferente da hierarquia do computador de referência, remova a chave raiz fidedigna do computador de referência.  

    > [!NOTE]  
    > Se os clientes não podem consultar os Serviços de Domínio do Diretório Ativo para localizar um ponto de gestão, eles usam a chave de raiz confiável para determinar pontos de gestão fidedignos. Se colocar todos os clientes em imagem na mesma hierarquia que a do computador principal, deixe a chave de raiz fidedigna no lugar.
    >
    > Se colocar os clientes em diferentes hierarquias, remova a chave de raiz fidedigna. Também fornecer estes clientes com a nova chave raiz de confiança. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Utilize o seu software de imagem para capturar uma imagem do computador de referência.  

7. Desloque a imagem para os computadores de destino.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a>Computadores de grupo de trabalho

O Gestor de Configuração suporta a instalação do cliente para computadores em grupos de trabalho. Instale o cliente em computadores de grupo de trabalho utilizando o método especificado em [Como instalar os clientes do Gestor de Configuração manualmente](#BKMK_Manual).  

### <a name="prerequisites"></a>Pré-requisitos  

- Instale manualmente o cliente em cada computador do grupo de trabalho. Durante a instalação, o utilizador interativo deve ter direitos de administrador local.  

- Para aceder aos recursos no domínio do servidor do Site Do Gestor de Configuração, configure a conta de acesso à rede para o site. Especifique esta conta no componente do site de distribuição de software. Para mais informações, consulte [os componentes do Site.](../../servers/deploy/configure/site-components.md)  

### <a name="limitations"></a>Limitações  

- Os clientes do grupo de trabalho não conseguem localizar pontos de gestão dos Serviços de Domínio do Diretório Ativo. Em vez disso, usam DNS, WINS ou outro ponto de gestão.  

- O roaming global não é apoiado. Os clientes do grupo de trabalho não podem consultar os Serviços de Domínio do Diretório Ativo para obter informações sobre o site.  

- Métodos de descoberta de Diretório ativo não podem descobrir computadores em grupos de trabalho.  

- Não é possível implementar software para utilizadores de computadores de grupo de trabalho.  

- Não é possível utilizar o método de instalação de impulso do cliente para instalar o cliente em computadores de grupo de trabalho.  

- Os clientes do grupo de trabalho não podem usar kerberos para autenticação, e podem precisar de aprovação manual.  

- Não se pode configurar um cliente de grupo de trabalho como ponto de distribuição. O Gestor de Configuração requer que os computadores de ponto de distribuição sejam membros de um domínio.  

### <a name="install-the-client-on-workgroup-computers"></a>Instale o cliente em computadores de grupo de trabalho  

Verifique os pré-requisitos e, em seguida, siga as instruções na secção [Como instalar os clientes do Gestor de Configuração manualmente](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Grupo de trabalho exemplo 1

Este exemplo faz as seguintes ações:

- Instala o cliente para gestão de clientes intranet
- Especifica o código do site
- Especifica o sufixo DNS para localizar um ponto de gestão  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Grupo de trabalho exemplo 2

Este exemplo requer que o cliente esteja num local de rede configurado num grupo de fronteiras. Se este requisito não for cumprido, a atribuição automática do site não funcionará. O comando inclui um ponto de estado de recuo no servidor FSPSERVER. Esta propriedade ajuda a rastrear a implementação do cliente e a identificar quaisquer problemas de comunicação do cliente.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a>Gestão de clientes baseada na Internet  

> [!NOTE]  
> Esta secção não se aplica a clientes que usam um portal de gestão de [nuvem.](../manage/cmg/plan-cloud-management-gateway.md) Para instalar clientes baseados na Internet utilizando um portal de gestão de nuvem, consulte instalar e atribuir clientes do Gestor de [Configuração do Windows 10 utilizando a AD Azure para autenticação.](deploy-clients-cmg-azure.md)  

Quando o site Do Gestor de Configuração suporta a [gestão de clientes baseadona na Internet](../manage/plan-internet-based-client-management.md) para clientes que às vezes estão numa intranet e às vezes na internet, você tem duas opções quando você instala clientes na intranet:  

- Inclua a propriedade `CCMHOSTNAME=<internet FQDN of the internet-based management point>` Client.msi quando instalar o cliente, utilizando a instalação manual ou o impulso do cliente, por exemplo. Quando utilizar este método, atribua diretamente o cliente ao site. Não pode usar a atribuição automática do site. Consulte a secção manual de [Como instalar os clientes do Gestor de Configuração,](#BKMK_Manual) o que fornece um exemplo deste método de configuração.  

- Instale o cliente para gestão de clientes intranet e, em seguida, atribua um ponto de gestão de clientes baseado na Internet ao cliente. Altere o ponto de gestão utilizando as propriedades do cliente na página do Gestor de **Configuração** no Painel de Controlo, ou utilizando um script. Se utilizar este método, pode utilizar a atribuição automática de clientes. Para mais informações, consulte a forma de [configurar os clientes para a gestão de clientes baseados na Internet após](#BKMK_ConfigureIBCM_MP) a secção de instalação do cliente.  

Para instalar clientes que estejam na internet, escolha um dos seguintes métodos suportados:  

- Forneça um mecanismo para estes clientes se conectarem temporariamente à intranet com uma VPN. Em seguida, instale o cliente utilizando qualquer método de instalação do cliente apropriado.  

- Utilize um método de instalação independente do Gestor de Configuração. Por exemplo, embaas se os ficheiros de origem de instalação do cliente para meios amovíveis e envie os meios de comunicação para os utilizadores. Os ficheiros de origem `<installation path>\Client` de instalação do cliente estão localizados na pasta no servidor do site do Gestor de Configuração. Nos meios de comunicação, inclua um script para copiar manualmente sobre a pasta do cliente. A partir desta pasta, instale o cliente utilizando CCMSetup.exe e todas as propriedades de linha de comando CCMSetup apropriadas.  

> [!NOTE]  
> O Gestor de Configuração não suporta instalar um cliente diretamente a partir do ponto de gestão baseado na Internet ou a partir do ponto de atualização de software baseado na Internet.

Os clientes que são geridos através da internet devem comunicar com sistemas de sites baseados na Internet. Certifique-se de que estes clientes também possuem certificados de infraestrutura de chave pública (PKI) antes de instalar o cliente. Instale estes certificados independentemente do Gestor de Configuração. Para mais informações, consulte os requisitos do [certificado PKI](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instale clientes na internet especificando propriedades da linha de comando CCMSetup  

1. Siga as instruções na secção [Como instalar os clientes do Gestor de Configuração manualmente](#BKMK_Manual). Inclua sempre as seguintes opções:  

    - Parâmetro de linha de comando CCMSetup`/source:<local path of the copied Client folder>`  

    - Parâmetro de linha de comando CCMSetup`/UsePKICert`  

    - Propriedade Cliente.msi`CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Propriedade Cliente.msi`SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Propriedade Cliente.msi`SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Se o site tem mais de um ponto de gestão baseado na `CCMHOSTNAME` Internet, não importa qual especifica para a propriedade. Quando um cliente do Gestor de Configuração se conecta ao ponto de gestão especificado baseado na Internet, envia ao cliente uma lista de pontos de gestão disponíveis baseados na Internet no site. O cliente seleciona aleatoriamente um da lista.

2. Se não quiser que o cliente verifique a lista de revogação do certificado (CRL), especifique o parâmetro `/NoCRLCheck`da linha de comando CCMSetup .  

3. Se estiver a utilizar um ponto de estado de recuo baseado `FSP=<internet FQDN of the internet-based fallback status point>`na Internet, especifique a propriedade Client.msi .  

4. Se estiver a instalar o cliente para gestão de clientes apenas `CCMALWAYSINF=1`na Internet, especifique a propriedade Client.msi .  

5. Determine se tem de especificar parâmetros adicionais da linha de comando CCMSetup. Por exemplo, se o cliente tiver mais de um certificado PKI válido, poderá ter de especificar um critério de seleção de certificados. Para obter uma lista de propriedades disponíveis, consulte [sobre os parâmetros e propriedades](about-client-installation-properties.md)de instalação do cliente.  

#### <a name="internet-based-example"></a>Exemplo baseado na Internet

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

Este exemplo instala o cliente com os seguintes comportamentos:

- Utilize ficheiros de origem a partir de uma pasta na unidade D.
- Use um certificado PKI cliente.
- Selecione o certificado com o período de validade mais longo.
- Gestão de clientes só para internet.
- Designar o cliente para usar o ponto de gestão baseado na Internet chamado SERVER1.
- Atribuir o ponto de estado de recuo baseado na Internet no domínio contoso.com.
- Designar o cliente para o site da ABC.  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para gestão de clientes baseados na Internet após a instalação do cliente  

Para atribuir o ponto de gestão baseado na Internet após a instalação do cliente, utilize um destes procedimentos. O primeiro requer configuração manual e é apropriado para alguns clientes. A segunda é mais apropriada para configurar muitos clientes.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configure clientes para gestão de clientes baseados na Internet após instalação do cliente do painel de controlo do Gestor de Configuração  

1. Abra o painel de controlo do Gestor de **Configuração** no cliente.  

2. No separador **Internet,** introduza o nome de domínio totalmente qualificado (FQDN) do ponto de gestão baseado na Internet como o **Internet FQDN**.  

    > [!NOTE]  
    > O separador **Internet** só está disponível se o cliente tiver um certificado PKI cliente.  

3. Se o cliente aceder à internet utilizando um servidor proxy, introduza as definições do servidor proxy.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configure clientes para gestão de clientes baseados na Internet após a instalação do cliente usando um script  

##### <a name="powershell"></a>PowerShell

1. Abra um editor em linha PowerShell, como PowerShell ISE ou Visual Studio Code. Também pode utilizar um editor de texto, como o Notepad.

2. Copie e insira as seguintes linhas de código no editor. Substitua-a `'mp.contoso.com'` pela Internet FQDN do seu ponto de gestão baseado na Internet.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > A última linha está lá apenas para verificar o novo valor do ponto de gestão da Internet.
    >
    > Para eliminar um determinado ponto de gestão baseado na Internet, remova o valor FQDN do servidor dentro das marcas de cotação. A linha `$newInternetBasedManagementPointFQDN = ''`torna-se.

3. Guarde o ficheiro com uma extensão .ps1.  

4. Execute o script com direitos elevados em computadores clientes. Utilize um destes métodos:  

    - Implemente o ficheiro nos clientes existentes do Configuration Manager, utilizando um pacote e um programa.  

    - Execute o ficheiro localmente nos clientes do Gestor de Configuração existentes clicando duas vezes no ficheiro script no File Explorer.  

Pode ter de reiniciar o cliente para que as alterações entrem em vigor.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a>Propriedades de instalação de clientes provisioniosas

Provisão de propriedades de instalação de clientes para instalações de clientes baseadas em políticas de grupo e atualização de software. Utilize a Política do Grupo Windows para fornecer computadores com propriedades de instalação de clientes do Gestor de Configuração. Estas propriedades estão armazenadas no registo do computador. O cliente lê-os quando instala. Este procedimento não é normalmente necessário, mas pode ser necessário para alguns cenários de instalação do cliente, tais como:  

- Está a utilizar as definições de política de grupo ou métodos de instalação de clientes baseados em atualização de software. Não estendeu o esquema de Diretório Ativo para Diretor de Configuração.  

- Pretende substituir propriedades de instalação de cliente em computadores específicos.  

> [!NOTE]  
> Se forem fornecidas propriedades de instalação na linha de comando CCMSetup.exe, as propriedades de instalação fornecidas nos computadores não são utilizadas.

Um modelo administrativo `ConfigMgrInstallation.adm` de política de grupo nomeado é fornecido nos meios de instalação do Gestor de Configuração. Utilize este modelo para fornecer computadores clientes com propriedades de instalação.

> [!TIP]
> Por padrão, `ConfigMgrInstallation.adm` não suporta cordas maiores do que 255 caracteres. Esta configuração pode impactar a adição de múltiplos parâmetros ou parâmetros com valores longos, tais como CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> Para contornar esta questão:
>
> 1. Editar `ConfigMgrInstallation.adm` em Bloco de Notas.
> 2. Para o `VALUENAME SetupParameters`imóvel, altere o `MAXLEN` valor para um inteiro maior. Por exemplo, `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configure e atribua propriedades de instalação do cliente usando um objeto de política de grupo  

1. Importe o modelo administrativo ConfigMgrInstallation.adm num objeto de política de grupo novo ou existente (GPO) utilizando um editor como O Editor de Objetos políticos do Grupo Windows. Pode encontrar este ficheiro `TOOLS\ConfigMgrADMTemplates` na pasta no suporte de instalação do Gestor de Configuração.  

2. Abra as propriedades da definição importada **Configurar Definições de Implementação de Cliente**.  

3. Selecione **Ativado**.  

4. Na caixa **CCMSetup**, introduza as propriedades da linha de comandos CCMSetup necessárias. Para obter uma lista de todas as propriedades da linha de comando CCMSetup e exemplos da sua utilização, consulte [sobre os parâmetros e propriedades](about-client-installation-properties.md)de instalação do cliente .  

5. Atribua o GPO aos computadores que pretende fornecer com propriedades de instalação de clientes do Gestor de Configuração.  
