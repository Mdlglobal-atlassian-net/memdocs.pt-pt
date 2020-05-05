---
title: Pré-visualização técnica 1705
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1705 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0a10726062d679666d14cbbb0b87510af5dfe30c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078809"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1705 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1705. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    

**Questões Conhecidas nesta Pré-Visualização Técnica:**
-   **O conector Suite gestor**de operações não atualiza . Ao atualizar a partir de uma versão anterior da Pré-visualização Técnica que tinha o conector OMS configurado, esse conector não é atualizado e já não está disponível na consola. Após a atualização, deve utilizar o assistente dos [Serviços Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e restabelecer a ligação ao seu espaço de trabalho OMS.
-   **Os condutores**de superfície não sincronizam com sucesso . Apesar de o suporte para os controladores de superfície estar listado na consola **What's New** na consola 'Configuração Manager' para a pré-visualização técnica, esta funcionalidade ainda não funciona como esperado.
-   **Incapaz de criar a Atualização do Windows para políticas**de diferimento de Negócios. Mesmo que a capacidade de configurar as políticas de diferimento do Windows Update para o Negócio esteja listada no **What's New** na consola 'Configurmanager' para a pré-visualização técnica, o assistente não abre e não consegue configurar quaisquer políticas.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações  
Pode utilizar a ferramenta de reset de reset do Gestor de Configuração, **CMUpdateReset.exe,** para corrigir problemas quando as atualizações na consola têm problemas em descarregar ou replicar. Esta ferramenta está incluída com a versão 1705 de Pré-visualização Técnica. Pode encontrá-lo no servidor do site do seu site de pré-visualização técnica depois de instalar a pré-visualização na pasta ***\cd.latest\SMSSETUP\TOOLS.***

Pode utilizar esta ferramenta com versões de pré-visualização técnica 1606 ou posteriores. Este suporte para trás é fornecido para que a ferramenta possa ser usada com uma gama de cenários de atualização de pré-visualização técnica, e sem ter que esperar até que a próxima pré-visualização técnica fique disponível.

Pode utilizar esta ferramenta quando uma atualização na consola ainda não tiver sido instalada e se encontra em estado de falha. Um estado falhado pode significar que o download da atualização permanece em andamento, mas está preso e demorando um tempo excessivamente longo, talvez horas mais do que as suas expectativas históricas para pacotes atualizados de tamanho semelhante. Também pode ser uma falha na replicação da atualização para sites primários infantis.  

Quando executa a ferramenta, esta passa contra a atualização que especifica. Por predefinição, a ferramenta não apaga atualizações instaladas ou descarregadas com sucesso.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
-   **Leia** e **escreva** permissões na base de dados do site da administração central e em cada site primário da sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [funções de base](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) de dados fixas na base de dados do Gestor de Configuração de cada site. A ferramenta não interage com sites secundários.
-   **Administrador local** no local de alto nível da sua hierarquia.
-   **Administrador local** no computador que acolhe o ponto de ligação de serviço.

Necessitará do GUIA do pacote de atualização que pretende repor. Para obter o GUID:
-   Na consola vá para**Atualizações de** **Administração** > e Manutenção e, em seguida, no painel de visualização, clique na cabeça de uma das colunas (como **Estado),** em seguida, selecione **Pacote Guia**. Isto adiciona essa coluna ao visor e a coluna mostra o pacote de atualização GUID.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende repor e, em seguida, utilize CTRL+C para copiar essa linha. Se colar a sua seleção copiada a um editor de texto, pode então copiar apenas o GUID para ser utilizado como parâmetro de linha de comando quando executa a ferramenta.

### <a name="run-the-tool"></a>Executar a ferramenta    
A ferramenta deve ser executada no local de alto nível da hierarquia.

Quando executa a ferramenta, utiliza parâmetros de linha de comando para especificar o Servidor SQL no site de topo da hierarquia, o nome da base de dados do site e o GUIA do pacote de atualização que pretende redefinir. A ferramenta identifica então os servidores adicionais a que necessita aceder, com base no estado das atualizações.   

Se o pacote de atualização estiver em estado de *descarregamento,* a ferramenta não limpa a embalagem. Como opção, pode forçar a remoção de uma atualização descarregada com sucesso utilizando o parâmetro de eliminação da força (Ver parâmetros da linha de comando mais tarde neste tópico).

Depois da ferramenta correr:
-   Se um pacote foi eliminado, reinicie os sites de topo SMS_Executive serviço e, em seguida, verifique se há atualizações para descarregar o pacote novamente.
-   Se um pacote não foi apagado, não precisa de tomar qualquer medida, uma vez que a atualização irá reinicializar e reiniciar a replicação ou instalação.

**Parâmetros da linha de comando:**  


|                        Parâmetro                         |                                                            Descrição                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN do Servidor SQL do seu site de topo>** | *Necessário* <br> Deve especificar o FQDN do Servidor SQL que acolhe a base de dados do site para o site de topo da sua hierarquia. |
|                **-Nome &lt;da base de dados -D>**                 |                             *Necessário* <br> Deve especificar o nome da base de dados de sites de topo.                             |
|                 **-P &lt;Pacote GUIA>**                 |                        *Necessário* <br> Deve especificar o GUIA para o pacote de atualização que pretende repor.                        |
|           **-I &lt;Nome de instância do Servidor SQL>**           |                   *Opcional* <br> Use isto para identificar a instância do Servidor SQL que acolhe a base de dados do site.                   |
|                       **-FDELETE**                       |                      *Opcional* <br> Use isto para forçar a eliminação de um pacote de atualização descarregado com sucesso.                      |

 **Exemplos:**  
 Num cenário típico, pretende repor uma atualização que tenha problemas de descarregamento. O seu SQL Servers FQDN é *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*, e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  ***Executa: CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Num cenário mais extremo, pretende forçar a eliminação do pacote de atualização problemático. O seu SQL Servers FQDN é *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*, e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  ***Executa: CMUpdateReset.exe -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Teste a ferramenta com a Pré-visualização Técnica  
Pode utilizar esta ferramenta com versões de pré-visualização técnica 1606 ou posteriores. Este suporte para trás é fornecido para que a ferramenta possa ser usada com um maior número de cenários de atualização de pré-visualização técnica, sem ter que esperar até que a próxima versão técnica de pré-visualização esteja disponível.

Execute a ferramenta num pacote de atualização para obter uma pré-visualização técnica antes de a atualização completar a verificação pré-requisito. Um estado de verificação pré-requisito preenchido é identificado pelo seguinte Estado para o pacote **em** > **Atualizações administrativas e manutenção:**  
-   **Verificação pré-requisito aprovada**
-   **Verificação pré-requisito passada com aviso**
-   **Verificação pré-requisito falhou**


## <a name="high-dpi-console-support"></a>Suporte de consola DPI elevado

Com esta versão, devem ser corrigidas questões com a forma como a consola do Gestor de Configuração se baseia e exibe diferentes partes do UI quando visualizadas em dispositivos DPI elevados (como um livro de Superfície).


## <a name="peer-cache-improvements"></a>Melhorias do Peer Cache
A partir desta pré-visualização técnica, peer Cache [já não utiliza a Conta](../plan-design/hierarchy/client-peer-cache.md) de Acesso à Rede para autenticar pedidos de descarregamento de pares.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Melhorias para o Servidor SQL sempre em grupos de disponibilidade  
Com esta versão, pode agora utilizar réplicas de compromisso assíncronos nos grupos de disponibilidade do Servidor SQL Always On que utiliza com o Gestor de Configuração.  Isto significa que pode adicionar réplicas adicionais aos seus grupos de disponibilidade para usar como backups off-site (remotos) e, em seguida, usá-las num cenário de recuperação de desastres.  

- O Gestor de Configuração suporta a utilização da réplica assíncrona para recuperar a sua réplica sincronizada.  Consulte [as opções](../servers/manage/recover-sites.md#site-database-recovery-options) de recuperação da base de dados do site no tópico de Backup e Recovery para obter informações sobre como o conseguir.

- Esta versão não suporta a falha na utilização da réplica de compromisso assíncrono como base de dados do site.
  > [!CAUTION]  
  > Como o Gestor de Configuração não valida o estado da réplica assíncrona compromete-se a confirmar a sua corrente, e [ao conceber tal réplica pode estar dessincronizada,](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes)o uso de uma réplica de compromisso assíncrono, uma vez que a base de dados do site pode colocar a integridade do seu site e os dados em risco.  

- Pode utilizar o mesmo número e tipo de réplicas num grupo de disponibilidade, tal como suportado pela versão do SQL Server que utiliza.   (O apoio prévio limitava-se a duas réplicas sincronizadas.)

### <a name="configure-an-asynchronous-commit-replica"></a>Configure uma réplica de compromisso assíncrono
Para adicionar uma réplica assíncrona a um grupo de [disponibilidade que utiliza com o Configurmanager,](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)não precisa de executar os scripts de configuração necessários para configurar uma réplica sincronizada. (Isto porque não há suporte para usar essa réplica assíncrona como base de dados do site.) Consulte [a documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias a grupos de disponibilidade.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Use a réplica assíncrona para recuperar o seu site
Antes de utilizar uma réplica assíncrona para recuperar a base de dados do site, tem de parar o site primário ativo para evitar mais escritos na base de dados do site. Depois de parar o site, pode utilizar uma réplica assíncrona no lugar da utilização de uma base de [dados recuperada manualmente](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).

Para parar o site, pode utilizar a ferramenta de manutenção da [hierarquia](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) para parar os serviços chave no servidor do site. Utilize a linha de comando: **Preinst.exe /stopsite**   

Parar o site equivale a parar o serviço do Gestor de Componentes do Site (sitecomp) seguido do serviço SMS_Executive, no servidor do site.


## <a name="improved-user-notifications-for-office-365-updates"></a>Melhores notificações dos utilizadores para as atualizações do Office 365
Foram feitas melhorias para alavancar a experiência do utilizador Click-to-Run do Office quando um cliente instala uma atualização do Office 365. Isto inclui notificações pop-up e in-app, e uma experiência de contagem regressiva. Antes deste lançamento, quando uma atualização do Office 365 foi enviada a um cliente, as aplicações do Office que estavam abertas foram automaticamente encerradas sem aviso prévio. Após esta atualização, as candidaturas do Office deixarão de ser encerradas inesperadamente.

### <a name="prerequisites"></a>Pré-requisitos
Esta atualização aplica-se aos clientes Do Office 365 ProPlus.

### <a name="known-issues"></a>Problemas conhecidos
Quando um cliente avalia pela primeira vez uma atribuição de atualização do Office 365 e a atualização tem um prazo agendado no passado, agendado imediatamente ou agendado dentro de 30 minutos, a experiência do utilizador do Office 365 pode ser inconsistente. Por exemplo, o cliente pode receber um diálogo de contagem regressiva de 30 minutos para a atualização, mas a aplicação real pode começar antes do final da contagem regressiva. Para evitar este comportamento, considere o seguinte:
- Implemente a atualização do Office 365 com um prazo que está agendado para mais de 60 minutos antes do tempo atual.
- Configure uma janela de manutenção durante o horário não comercial da recolha ou configure um período de carência de execução na implantação.

### <a name="try-it-out"></a>Experimente!
Tente completar as seguintes tarefas e, em seguida, envie-nos **feedback** do separador **Home** da Fita para nos informar como funcionava:
- Desloque para um cliente uma atualização do Office 365 com um prazo definido para um tempo mínimo 60 minutos antes do tempo atual. Observe o novo comportamento no cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configure e implemente as políticas de Guarda de Aplicações do Windows Defender

[O Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo web sites não confiáveis num recipiente isolado seguro que não é acessível por outras partes do sistema operativo. Nesta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de conformidade do Gestor de Configuração que configura e, em seguida, implantamos para uma coleção.
Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da Atualização do Criador do Windows 10. Para testar esta funcionalidade agora, deve utilizar uma versão de pré-visualização desta atualização.


### <a name="before-you-start"></a>Antes de começar

Para criar e implementar as políticas do Windows Defender Application Guard, os dispositivos Windows 10 para os quais implementa a política devem ser configurados com uma política de isolamento de rede. Para mais detalhes, consulte a publicação do blog referenciada mais tarde.
Esta capacidade funciona apenas com as atuais construções do Windows 10 Insider. Para testá-lo, os seus clientes devem estar a executar uma recente Construção insider do Windows 10.

### <a name="try-it-out"></a>Experimente!

Certifique-se de que leu o post do blog para entender o básico sobre o Windows Defender Application Guard.

Para criar uma política, e para navegar nas definições disponíveis:

1.  Na consola 'Gestor de Configuração', escolha **Ativos e Conformidade.**
2.  No espaço de trabalho **de Ativos e Compliance,** escolha **A** > Proteção de**Pontos Finais** > guarda de**aplicação Windows Defender**.
3.  No separador **Home,** no grupo **Criar,** clique em Criar a Política de Guarda de **Aplicações do Windows Defender**.
4.  Utilizando o post do blog como referência, pode navegar e configurar as definições disponíveis para experimentar a funcionalidade.
5.  Quando terminar, complete o assistente e implemente a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Mais recursos

Para ler mais sobre o Windows Defender Application Guard, consulte [esta publicação do blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Além disso, para saber mais sobre o modo autónomo de guarda de aplicação do Windows Defender, consulte [esta publicação de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Novas capacidades para a AD Azure e a gestão da nuvem

Nesta versão, pode configurar serviços em nuvem para utilizar o Azure AD para suportar o seguinte cenário:

- Instale manualmente o cliente do Gestor de Configuração a partir da internet e o designe para um site do Gestor de Configuração.
- Utilize o Intune para implementar o cliente Do Gestor de Configuração em dispositivos na internet.

### <a name="advantages"></a>Vantagens

Utilizando serviços na nuvem e AD Azure remove a necessidade de usar certificados de autenticação do cliente.

Pode descobrir utilizadores de Anúncios Azure no seu site para utilizar em coleções e outras operações do Gestor de Configuração.

### <a name="before-you-start"></a>Antes de começar

- Deve ter um inquilino da AD Azure.
- Os seus dispositivos devem executar o Windows 10 e ser a AD Azure.  Os clientes também podem ser de domínio adeferidos para além da adesão à Azure AD).
- Para além dos [pré-requisitos existentes](../plan-design/configs/site-and-site-system-prerequisites.md) para a função do sistema do site de pontos de gestão, deve ainda garantir que **ASP.NET 4.5** (e quaisquer outras opções que sejam automaticamente selecionadas com isto) estejam ativadas no computador que acolhe este papel no sistema do site.
- Para utilizar o Microsoft Intune para implementar o cliente do Gestor de Configuração:
    - Você deve ter um inquilino intune de trabalho (Gerente de Configuração e Intune não precisam de ser conectados).
    - Em Intune, criou e implementou uma aplicação contendo o cliente do Gestor de Configuração. Para mais detalhes sobre como fazê-lo, consulte como instalar clientes em dispositivos Windows geridos pelo MDM.
- Para utilizar o Gestor de Configuração para implementar o cliente:
    - Pelo menos um ponto de gestão deve ser configurado para o modo HTTPS.
    - Tens de montar um Portal de Gestão de Nuvem.


### <a name="set-up-the-cloud-management-gateway"></a>Configurar o Gateway de Gestão de Nuvem

Configurar o Gateway de Gestão de Nuvem para permitir que os clientes acedam ao seu site de Configuração da Internet sem utilizar certs.

Você encontrará ajuda sobre como fazer isso nos seguintes tópicos:

- [Plano para gateway](../clients/manage/cmg/plan-cloud-management-gateway.md)de gestão de nuvem em Gestor de Configuração .
- [Configurar gateway de gestão de nuvem para Gestor](../clients/manage/cmg/setup-cloud-management-gateway.md)de Configuração .
- [Monitorize o gateway de gestão](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md)de nuvem no Gestor de Configuração .

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurar a aplicação De Serviços Azure em Serviços de Nuvem de Gestor de Configuração

Isto liga o site do Gestor de Configuração ao Azure AD e é um pré-requisito para todas as outras operações nesta secção. Para efetuar este procedimento:

1. No espaço de trabalho da **Administração** da consola De Configuração Manager, expanda os **Serviços cloud,** e depois clique nos **Serviços Azure**.
2. No separador **Home,** no grupo **Serviços Azure,** clique em **Serviços Configure Azure**.
3. Na página dos **Serviços Azure** do Assistente de Serviços Azure, selecione **Cloud Management** para permitir que os clientes autentiem com a hierarquia usando a Azure AD.
4. Na página **geral** do assistente, especifique um nome e uma descrição para o seu serviço Azure.
5. Na página da **App** do assistente, selecione o seu ambiente Azure a partir da lista e, em seguida, clique em **Navegar** para selecionar as aplicações do servidor e cliente que serão usadas para configurar o serviço Azure:
   - Na janela **'Aplicação servidora',** selecione a aplicação do servidor que pretende utilizar e, em seguida, clique em **OK**. As aplicações do servidor são as aplicações web Azure que contêm as configurações para a sua conta Azure, incluindo o seu ID de Inquilino, ID do Cliente e uma chave secreta para os clientes. Se não tiver uma aplicação de servidor disponível, utilize uma das seguintes aplicações:
       - **Criar**: Para criar uma nova aplicação de servidor, clique em **Criar**. Forneça um nome amigável para a app e o inquilino. Depois de iniciar sessão no Azure, o Gestor de Configuração cria a aplicação web em Azure para si, incluindo o ID do Cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode vê-los a partir do portal Azure.
       - **Importação**: Para utilizar uma aplicação web que já existe na sua subscrição Azure, clique **em Importar**. Forneça um nome amigável para a app e o inquilino, e depois especifique o ID do Inquilino, id do cliente e a chave secreta para a aplicação web Azure que pretende utilizar o Gestor de Configuração. Depois de verificar a informação, clique em **OK** para continuar. Esta opção não está disponível neste momento nesta pré-visualização técnica.
   - Repita o mesmo processo para a aplicação do cliente.

   É necessário conceder a permissão de pedido de dados do *diretório De ler* quando utilizar a Importação de Aplicações, para definir as permissões corretas no portal. Se utilizar a Application Creation as permissões são automaticamente criadas com a aplicação, mas ainda precisa de dar o seu consentimento à aplicação no portal Azure.
6. Na página **Discovery** do assistente, faculte opcionalmente a descoberta do **utilizador ativo do Diretório Azure,** e, em seguida, clique em **Definições**.
   Na caixa de diálogo De definições de Definições de Definições de Descoberta de **Utilizadores De AD Azure,** configure um horário para quando ocorrer a descoberta. Também pode permitir a descoberta delta que verifica apenas novas, ou alteradas contas em Azure AD.
7. Conclua o assistente.

Neste momento, ligou o site do Gestor de Configuração ao Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instale o cliente CM a partir da Internet

Antes de começar, certifique-se de que os ficheiros de origem de instalação do cliente são armazenados localmente no dispositivo para o qual pretende instalar o cliente.
Em seguida, utilize as instruções em [Como implementar clientes para computadores Windows](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) utilizando a seguinte linha de comando de instalação (substitua os valores no exemplo com os seus próprios valores):

**ccmsetup.exe /NoCrlCheck /Source:C:CLIENTE CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID=\<GUID> AADRESOURCEURI=<https://contososerver>**

- **/NoCrlCheck**: Se o seu ponto de gestão de gestão ou gateway de gestão de nuvem utilizar um certificado de servidor não público, então o cliente pode não conseguir chegar à localização crl.
- **/Fonte**: Pasta local: Localização dos ficheiros de instalação do cliente.
- **CCMHOSTNAME**: O nome do seu ponto de gestão da Internet. Você pode encontrá-lo executando **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** a partir de um pedido de comando em um cliente gerido.
- **SMSMP**: O nome do seu ponto de gestão de procuração – isto pode estar na sua intranet.
- **SMSSiteCode**: O código de site do seu site de Configuração Manager.
- **AADTENANTID**, **AADTENANTNAME**: O ID e o nome do inquilino Azure AD que você ligou ao Gestor de Configuração. Pode encontrá-lo executando dsregcmd.exe /status a partir de um pedido de comando num dispositivo azure AD.
- **AADCLIENTAPPID**: O ID da aplicação de cliente Azure AD. Para ajudar a encontrar isto, consulte [o portal Use para criar uma aplicação e diretor idae-manete sinuoso e um diretor](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)de serviço que possa aceder a recursos.
- **AADResourceUri**: O identificador URI da aplicação de servidor AD Azure onboarded.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Utilize o Assistente de Serviços Azure para configurar uma ligação à OMS
A partir do lançamento de pré-visualização técnica de 1705, utiliza o **Assistente de Serviços Azure** para configurar a sua ligação desde o Diretor de Configuração até ao serviço de cloud Da Suite de Gestão de Operações (OMS). O assistente substitui os fluxos de trabalho anteriores para configurar esta ligação.

-   O assistente é utilizado para configurar serviços em nuvem para OMS, Windows Store for Business (WSfB) e Azure Ative Directory (Azure AD).  

-   O Gestor de Configuração conecta-se à OMS para funcionalidades como Log Analytics ou Upgrade Readiness.

### <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o Conector OMS
Os pré-requisitos para configurar uma ligação à OMS são inalterados dos [documentados para a versão 1702](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)do Ramo Atual . Essa informação é repetida aqui:  

-   Fornecendo permissão de Gestor de Configuração para OMS.

-   O conector OMS deve ser instalado no computador que acolhe um ponto de [ligação](../servers/deploy/configure/about-the-service-connection-point.md) de serviço que se encontra em [modo online](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

-   Deve instalar um Agente de Monitorização da Microsoft para OMS instalado no ponto de ligação de serviço juntamente com o conector OMS. O Agente e o conector OMS devem ser configurados para utilizar o mesmo espaço de **trabalho OMS**. Para instalar o agente, consulte [O Download e instale o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação OMS.
-   Depois de instalar o conector e o agente, tem de configurar o OMS para utilizar os dados do Gestor de Configuração. Para isso, no Portal OMS importa as coleções do Gestor de [Configuração.](/azure/log-analytics/log-analytics-sccm#import-collections)

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilize o Assistente de Serviços Azure para configurar a ligação à OMS

1.  Na consola, vá ao **Administration** > **Overview** > **Cloud Services** > **Azure Services**, e depois escolha os **Serviços Configure Azure** a partir do separador **Home** da fita, para iniciar o Assistente **de Serviços Azure**.

2.  Na página **dos Serviços Azure,** selecione o serviço de cloud Da Suite de Gestão da Operação. Forneça um nome amigável para o nome de **serviço Azure** e uma descrição opcional, e depois clique em **Seguinte**.

3.  Na página da **App,** especifique o seu ambiente Azure (a pré-visualização técnica suporta apenas a Nuvem Pública). Em seguida, clique em **Navegar** para abrir a janela da Aplicação do Servidor.

4.  Selecione uma aplicação web:

    -   **Importação**: Para utilizar uma aplicação web que já existe na sua subscrição Azure, clique **em Importar**. Forneça um nome amigável para a app e o inquilino, e depois especifique o ID do Inquilino, id do cliente e a chave secreta para a aplicação web Azure que pretende utilizar o Gestor de Configuração. Depois de **verificar** a informação, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando configura o OMS com esta pré-visualização, a OMS apenas suporta a função de *importação* para uma aplicação web. A criação de uma nova aplicação web não é suportada. Da mesma forma, não é possível reutilizar uma aplicação existente para OMS.

5.  Se realizou todos os outros procedimentos com sucesso, então as informações no ecrã de Configuração de **Ligação OMS** aparecerão automaticamente nesta página. As informações para as definições de ligação devem aparecer para a sua **subscrição Azure,** **grupo de recursos Azure**e Espaço de Trabalho suite de gestão de **operações.**

6.  O assistente liga-se ao serviço OMS utilizando a informação que insere. Selecione as coleções do dispositivo que pretende sincronizar com OMS e, em seguida, clique em **Adicionar**.

7.  Verifique as definições de ligação no ecrã **Resumo** e, em seguida, selecione **Next**. O ecrã **Progress** mostra o estado da ligação e, em seguida, deve **completar**.

8.  Após o fim do assistente, a consola do Gestor de Configuração mostra que configuraste a Suite de Gestão de **Funcionamento** como tipo de serviço em **nuvem**.
