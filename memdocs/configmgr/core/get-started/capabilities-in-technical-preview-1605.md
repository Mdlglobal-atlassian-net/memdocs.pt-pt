---
title: Capacidades na Pré-visualização Técnica 1605
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: c38230b44f7f18e3f60cb4c88b31a03e10a37d30
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721641"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1605 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1605. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 **Questões Conhecidas nesta Pré-Visualização Técnica:**  

- Com a Pré-visualização Técnica 1605, se atualizar as propriedades de um ponto de gestão após a sua instalação, poderá ver um erro de consola que obriga a consola a fechar.  Se isso acontecer, pode desinstalar o ponto de gestão e, em seguida, reinstalar o ponto de gestão utilizando as definições desejadas. Em alternativa, pode modificar o ponto de gestão antes da instalação de Pré-visualização Técnica 1605.  

- Quando utiliza a funcionalidade Windows Store for Business com a Pré-visualização Técnica 1604 e, em seguida, o upgrade para A Pré-visualização Técnica 1605, já não pode ver os dados de embarque. Todos os outros funcionalmente continuam a funcionar. Se embarcar com a Pré-visualização Técnica 1604, permanece a bordo depois de instalar a Pré-visualização Técnica 1605 e não precisa de mais medidas.  

  **Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a>VPN por app para dispositivos Windows 10  
 No caso dos dispositivos Do Windows 10 geridos utilizando o 'Configurmanager' com o Intune, pode adicionar uma lista de aplicações que abrem automaticamente uma ligação VPN que configuraste através da consola de administração do Gestor de Configuração. Tem a opção de restringir o tráfego VPN a essas aplicações, ou pode continuar a permitir todo o tráfego através da ligação VPN.  

 **Requisitos:**  

-   Gestor de configuração com Intune  

-   Um perfil VPN do Windows 10 que foi implementado para pelo menos um dispositivo  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a>Melhorias na sequência de tarefas de atualizações de software  
 Foram feitas as seguintes melhorias na sequência de tarefas de Atualizações de Software de Instalação:  

-   Uma nova variável de sequência de tarefas, SMSTSSoftwareUpdateScanTimeout, está disponível para lhe dar a capacidade de controlar o tempo limite na varredura de atualizações de software durante o passo de sequência de atualizações de software. O valor predefinido é 30 minutos.  

-   Houve melhorias na exploração madeireira. O ficheiro de registo smsts.log conterá novas entradas de registo que referenciam outros ficheiros de registo que o ajudarão a resolver problemas durante o processo de instalação de atualizações de software.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a>Melhorias ao Cliente Prepare ConfigMgr para a captura passo de sequência de tarefas  
 O passo do Cliente Prepare ConfigMgr irá agora remover completamente o cliente do Gestor de Configuração, em vez de apenas remover informações chave. Quando a sequência de tarefas implementar a imagem do sistema operativo capturado, instalará sempre um novo cliente do Gestor de Configuração.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a>Período de graça para implementações de aplicações necessárias  
 Em alguns casos, pode querer dar mais tempo aos utilizadores para instalarem as implementações de aplicações necessárias para além de quaisquer prazos configurados. Por exemplo, se um utilizador final acaba de regressar de férias, poderá ter de esperar por muito tempo, uma vez que as implementações de aplicações em atraso são instaladas. No entanto, ainda podem instalar imediatamente a aplicação a qualquer momento que queiram.  

 Para ajudar a resolver este problema, pode agora definir um período de **carência** implementando as definições do cliente do Gestor de Configuração para uma coleção.  

 Para configurar o período de graça, tome as seguintes ações:  

1. Na página do **Agente Informático** das definições do cliente, configure o novo período de graça da propriedade para aplicação após o prazo de **implementação (horas)** com um valor entre **1** e **120** horas.  

2. Numa nova implementação de aplicações, ou nas propriedades de uma implementação existente, na página **de Agendamento,** selecione a execução do atraso da caixa de verificação **desta implementação**de acordo com as preferências do utilizador, até ao período de carência definido nas definições do cliente.  

    Todas as implementações que tenham esta caixa de verificação selecionada e que sejam direcionadas para dispositivos aos quais também implementou a definição do cliente utilizarão o período de carência.  

   Nesta versão, o período de graça que configura não é utilizado pelos dispositivos do cliente. Se configurar um período de carência e selecionar a caixa de verificação, a aplicação será instalada na primeira janela não comercial que o utilizador configurado após o prazo.  

   Opções semelhantes foram adicionadas ao assistente de implementação de atualizações de software, assistente de regras de implementação automática e páginas de propriedades. No entanto, estes não são atualmente implementados nesta pré-visualização técnica.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a>Nova experiência para ações de dispositivos remotos  
 A experiência para realizar ações de dispositivos remotos a partir da consola Do Gestor de Configuração foi melhorada.  
As ações comuns como **Aposentado/Limpeza,** **Código de Reset,** **Bloqueio Remoto**e Bloqueio de **Ativação** de Bypass podem agora ser encontradas no menu Remote **Device Actions** acessado a partir do espaço de trabalho De ativos **e conformidade.**  

 ![Nova imagem de ações de dispositivo remoto](media/New-Remote-Device-Actions.png)  

 Pode encontrar o estado de cada uma destas operações nos seguintes locais:  

- No painel de detalhes quando selecionar um dispositivo a partir do nó de **Dispositivos.**  

- Na página **Propriedades** para um dispositivo.  

- Na página principal do nó dos **Dispositivos** (nem todas as colunas podem ser visíveis por padrão).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a>Windows Store para aplicativos de negócios  
 O [Windows Store for Business](https://www.microsoft.com/business-store) é onde pode encontrar e comprar aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Gestor de Configuração, pode gerir aplicações adquiridas em volume a partir da consola 'Gestor de Configuração', por exemplo:  

- Pode sincronizar a lista de aplicações adquiridas com o Gestor de Configuração  

- Aplicações sincronizadas aparecem na consola Do Gestor de Configuração e pode supor estas como quaisquer outras aplicações  

- A cada 24 horas, o Gestor de Configuração descarrega informações de licenciamento de aplicações a partir da loja, e pode rever isso na consola Do Gestor de Configuração  

  Na versão de pré-visualização técnica de 1604, poderá sincronizar e ver aplicações a partir da Windows Store for Business na consola 'Gestor de Configuração'. Neste lançamento, adicionámos a capacidade de criar e implementar aplicações do Gestor de Configuração a partir de aplicações de loja sincronizadas.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a Windows Store para sincronização de negócios  

1.  No Diretório Ativo do Azure, registe o Gestor de Configuração como uma ferramenta de gestão "Web Application and/ou Web API". Isto lhe dará uma identificação do cliente de que precisará mais tarde.  

    1.  No nó de Diretório [https://manage.windowsazure.com](https://manage.windowsazure.com)Ativo de , selecione o seu Diretório Ativo Azure e, em seguida, clique em **Aplicações** > **Adicionar**.  

    2.  Clique **Em adicionar uma aplicação que a minha organização está a desenvolver.**  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API,** em seguida, clique na seta **Seguinte.**  

    4.  Introduza o mesmo URL tanto para o **URL de inscrição** como para o **ID de aplicação URI**. O URL pode ser qualquer coisa e não precisa de resolver um endereço real. Por exemplo, pode introduzir **https://&lt;seu domínio>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Ative Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **Configurar**.  

    2.  Em **Teclas,** selecione uma duração da lista e clique em **Guardar**. Isto criará uma nova chave de cliente. Não navegue para longe desta página até ter embarcado com sucesso na Windows Store para Business to Configuration Manager.  

3.  Na Windows Store for Business, configure o Gestor de Configuração como a ferramenta de gestão da loja.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) e inscreva-se, se solicitado.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Em **Ferramentas de Gestão,** clique **em Adicionar uma ferramenta de gestão**.  

    4.  Em **Procurar a ferramenta pelo nome,** digite o nome da aplicação que criou anteriormente em AAD e, em seguida, clique em **Adicionar**.  

    5.  Clique em **Ativar** ao lado da aplicação que acabou de importar.  

    6.  No assistente de **apps licenciadas offline,** clique **em Sim** se quiser permitir a compra de aplicações licenciadas offline.  

4.  Compre pelo menos uma aplicação na Windows Store para Negócios.  

5.  No espaço de trabalho da **Administração** da consola De Configuração Manager, expanda os **Serviços Cloud**e, em seguida, clique na **Windows Store para Negócios.**  

6.  No separador **Home,** no grupo **Criar,** clique em **Adicionar Windows Store para Conta De Negócios**.  

7.  Adicione o seu ID de inquilino, identificação do cliente e chave de cliente do Azure Ative Directory, em seguida, complete o assistente.  

8.  Uma vez feito, verá a conta configurada na lista **da Windows Store para Contas Empresariais** na consola 'Gestor de Configuração'.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar a seguinte tarefa e, em seguida, deixe-nos saber como funcionou usando o nosso formulário de feedback na página do programa de feedback do Gestor de [Configuração](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) no site do Microsoft Connect:  

 Crie e implemente uma aplicação de Gestor de Configuração a partir de uma aplicação licenciada de Windows Store para Negócios offline.  

1. No espaço de trabalho da Biblioteca de **Software** da consola Do Gestor de Configuração, expanda a **Gestão**de Aplicações e, em seguida, clique em Informações de **Licença para Aplicações de Loja**.  

2. Escolha a aplicação que pretende implementar, então, no separador **Home,** no grupo **Criar,** clique em **Criar Aplicação**.  

   É criada uma aplicação 'Gestor de Configuração' que contém a aplicação Windows Store for Business. Em seguida, pode implementar e monitorizar esta aplicação como faria qualquer outra aplicação do Gestor de Configuração.  

> [!IMPORTANT]  
>  Quando cria uma aplicação de Gestor de Configuração com um único tipo de implementação a partir de uma aplicação licenciada offline, esta pode ser implementada para dispositivos geridos pelo MDM e também geridos com o cliente do Gestor de Configuração. Se tentar implementar uma aplicação com vários tipos de implementação, a instalação falhará.  
>   
>  Não é possível implementar atualmente aplicações licenciadas online com o Gestor de Configuração.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a>Melhorias gerais para aplicações compradas em volume  

-   Neste lançamento, as aplicações compradas em volume da Windows Store for Business e a loja de aplicações iOS foram consolidadas na mesma vista, **Informações**de Licença para Apps de Loja .  

-   Para aplicações adquiridas em volume iOS, o separador Apple Volume Purchase Program foi removido do Pacote de **Aplicações para a** caixa de diálogo do navegador iOS no assistente de aplicação Create. Para criar uma aplicação comprada em volume para iOS, utilize estes passos:  

    1.  1.  No espaço de trabalho da Biblioteca de **Software** da consola Do Gestor de Configuração, expanda a **Gestão**de Aplicações e, em seguida, clique em Informações de **Licença para Aplicações de Loja**.  

    2.  2.  Escolha a aplicação que pretende implementar, então, no separador **Home,** no grupo **Criar,** clique em **Criar Aplicação**.  

-   A localização que usa para obter e carregar um token Apple VPP para aplicações compradas em volume na consola Do Gestor de Configuração mudou. Agora pode fazê-lo no espaço de trabalho **da Admin** no âmbito do nó do Programa de Compra de Volume apple de **serviços** > **Apple Volume Purchase Program Tokens** na nuvem.  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a>Proteção de Dados empresariais (EDP)  
 Pode criar itens de configuração que lhe permitem implementar as suas políticas de proteção de dados da empresa (EDP), incluindo permitir-lhe escolher as suas aplicações protegidas, o seu nível de proteção EDP e como encontrar dados empresariais na rede. Para mais informações sobre a EDP, consulte os seguintes tópicos:  

- [Proteja os seus dados empresariais utilizando a Proteção de Informação do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Criar e implementar uma política de Proteção de Informação do Windows (WIP) utilizando o Gestor de Configuração](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a>Utilizadores finais podem instalar aplicações a partir do Portal da Empresa  
 No local, o MDM foi introduzido na versão 1511 do Gestor de Configuração. Em versões anteriores, poderia implementar aplicações para dispositivos Windows 10 geridos pelo MDM com um objetivo de implementação de instalação **necessária** para dispositivos geridos por MDM no local.  

 Neste lançamento, já é possível implementar aplicações com um objetivo de implementação de **disponíveis** para utilizadores de computadores geridos no local do MDM 10, e os utilizadores podem agora instalar estas próprias aplicações a partir do Portal da Empresa.
Nesta pré-visualização técnica, se o Portal da Empresa estiver aberto por mais de 15 minutos, o utilizador final verá uma mensagem de erro. Para contornar o problema, reinicie o Portal da Empresa.  

### <a name="before-you-start"></a>Antes de começar  

#### <a name="server-prerequisites"></a>Pré-requisitos do servidor  

-   .NET 4.5 ou superior (requer reinício)  

-   PowerShell 3.0 para script de configuração (requer reinício)  

#### <a name="client-prerequisites"></a>Pré-requisitos do cliente  

-   Windows 10 Desktop 1511 (OS build 10586.218) ou mais tarde  

#### <a name="general-prerequisites"></a>Pré-requisitos gerais  

-   Certifique-se de que completou as [etapas de Preparação para a Gestão de Dispositivos Móveis no local](https://technet.microsoft.com/library/mt613153.aspx) e [inscreveu os seus dispositivos.](https://technet.microsoft.com/library/mt627870.aspx)  

-   Para obter a melhor experiência de instalação de aplicações ao utilizar o Portal da Empresa, certifique-se de que o Gestor de Configuração tem uma ligação ativa com o Microsoft Intune.  

-   Se escolher a opção de inscrição a granel, configure a afinidade do dispositivo do utilizador para o dispositivo inscrito antes de experimentar este cenário.  

### <a name="configuration-steps"></a>Passos de configuração  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instale as funções do Catálogo de Aplicações e ative o suporte à Gestão de Dispositivos Móveis  

1.  Adicione as funções do Web Service do Catálogo de Aplicações e do Web Site  

    1.  Selecione **o modo HTTPS** e os dispositivos móveis para utilizar esta opção de ponto de ponto do Serviço Web do catálogo de **aplicações.**  

    2.  Limitações nesta Pré-visualização Técnica:  

        -   Tem de desinstalar quaisquer funções de Catálogo de Aplicações existentes antes de selecionar a opção para permitir a ligação de dispositivos móveis.  

        -   Certifique-se de que existe apenas um conjunto de funções de Catálogo de Aplicações e as funções são co-localizadas no mesmo sistema de site com as funções de ponto de inscrição e proxy de inscrição.  

2.  Verifique se os seguintes componentes estão operacionais a partir do nó de Estado do Componente na consola do Gestor de Configuração:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar limites  
 Configure os limites necessários para pontos de distribuição apenas intranet.  

> [!NOTE]  
>  Apenas os limites de gama IPv4 são suportados neste momento para a gestão de dispositivos móveis.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implementar a aplicação e configuração do Portal da Empresa  

1. Utilize o script de configuração incluído com a pré-visualização técnica para preparar a implementação e configuração do Portal da Empresa:  

   1. Abra uma janela de comando PowerShell elevada.  

   2. Executar **set-execuçãoPolítica RemoteSigned**  

   3. Da pasta ** &lt;SCCM diretor\>de instalação \cd.latest\SMSSETUP\TOOLS\MDM** executar **.\ConfiguraçãoScript.ps1**  

      O script de configuração faz o seguinte:  

   4. Cria uma aplicação De Configuração Manager com um tipo de implementação de pacotes de aplicativos Windows utilizando o **CompanyPortalOnPremisesMDM.appx** na mesma pasta.  

   5. Cria um item de configuração e linha de base de configuração que configura o Portal da Empresa.  

   6. Implementa tanto a linha de base de configuração como a aplicação, e adiciona a aplicação a todos os pontos de distribuição.  

   > [!NOTE]
   >  Se as funções do Catálogo de Aplicações não forem co-localizadas com o site principal, tome as seguintes ações:  
   > 
   > - No espaço de trabalho **de Ativos e Compliance,** localize o CI de configuração do **portal OnPremMDM -** item de configuração de urls de servidores  
   >   -   Alterar o valor **das Regras** de Conformidade para o nome de domínio totalmente qualificado do sistema de site onde estão localizadas as funções do Catálogo de Aplicações.  

2. Uma vez implementada a aplicação do Portal da Empresa e a sua configuração, verifique se a linha de base de aplicação e configuração está em conformidade com o dispositivo que utiliza a secção de **Implementações** da consola 'Gestor de Configuração'. O Portal da Empresa aparecerá como **Portal da Empresa (Pré-visualização Técnica)** no menu Iniciar no dispositivo.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar as seguintes tarefas e, em seguida, deixe-nos saber como funcionou usando o nosso formulário de feedback na página do programa de feedback do Gestor de [Configuração](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) no site do Microsoft Connect:  

1.  Implementar várias aplicações com tipos de implementação suportados para uma recolha de utilizadores com um objetivo de implementação de **Disponível**. Para esta pré-visualização técnica, as candidaturas que requeiram aprovação administrativa não são suportadas e não serão apresentadas no Portal da Empresa.  

2.  Os utilizadores podem então procurar e instalar aplicações a partir do Portal da Empresa.  

     Depois de abrir o Portal da Empresa, verá uma caixa de diálogo de autenticação chamada Gestor user@domain de **Configuração** Especificar as credenciais de Diretório Ativo do utilizador (sob a forma de utilizador ou de domínio\utilizador) para iniciar sessão.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a>Novos separadores para atualizações e sistemas operativos no Centro de Software  
 Nesta versão, foram feitas as seguintes alterações para melhorar o layout da aplicação do Centro de Software:  

-   O separador **Aplicações** foi dividido em três separadores separados para **Atualizações,** **Sistemas operativos** (que foram ambos previamente encontrados na lista de **Filtros)** e **Aplicações**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a>Serviço de um grupo de servidores  
 A Pré-visualização técnica para O Gestor de Configuração, versão 1511, incluiu a capacidade de criar uma coleção onde todos os dispositivos da coleção compõem um grupo de servidores. Em seguida, pode configurar as definições do grupo do servidor para utilizar quando implementa atualizações de software para o grupo de servidores, controlar a percentagem de computadores que são atualizados a qualquer momento, e configurar scripts PowerShell pré-implementação e pós-implementação para executar ações personalizadas.  

 A Pré-visualização técnica para o Gestor de Configuração, versão 1605, adiciona a capacidade de atualizar os computadores do grupo de servidores numa ordem especificada que define, adiciona uma monitorização melhorada para visualizar o estado dos computadores no grupo do servidor, e fornece a capacidade de limpar os bloqueios de implementação que são úteis quando os clientes não instalaram as atualizações do software e estão a impedir outros clientes de instalarem as suas atualizações de software.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar as seguintes tarefas e, em seguida, deixe-nos saber como funcionou usando o nosso formulário de feedback na página do programa de feedback do Gestor de [Configuração](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) no site do Microsoft Connect:  

-   Posso criar uma coleção que represente um grupo de servidores. Para este teste, pode configurar as suas regras de adesão para ter 2 máquinas nesta coleção.   

-   Posso especificar que os computadores do grupo de servidores instalam atualizações de software numa ordem específica com base nas definições do grupo do servidor para a recolha. Utilize as scripts da amostra no procedimento para especificar os scripts de pré-implantação e pós-implantação.  

-   Posso implementar uma atualização de software para esta coleção. Reveja os ficheiros start.txt e end.txt (criados a partir dos scripts de amostra) em C:\temp e verifique os tempos de início e fim para a implementação nos computadores do grupo do servidor. Reveja o ficheiro UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  

1.  [Crie uma coleção](https://technet.microsoft.com/library/gg712295.aspx) de dispositivos que contenha os computadores do grupo de servidores.  

2.  No espaço de trabalho **de Ativos e Compliance,** clique em Coleções de **Dispositivos,** clique à direita na recolha que contém os computadores no grupo do servidor e, em seguida, clique em **Propriedades**.  

3.  No separador **Geral,** selecione **Todos os dispositivos fazem parte do mesmo grupo de servidores**e, em seguida, clique em **Definições**.  

4.  Na página definições do **Grupo servidor,** especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem de máquinas seja atualizada ao mesmo tempo**: Especifica que apenas uma determinada percentagem de clientes é atualizada a qualquer momento. Se, por exemplo, a coleção tiver 10 clientes, e a coleção estiver configurada para atualizar 30% dos clientes ao mesmo tempo, então apenas 3 clientes irão instalar atualizações de software a qualquer momento.  

    -   **Permitir que uma série de máquinas sejam atualizadas ao mesmo tempo**: Especifica que apenas um certo número de clientes são atualizados a qualquer momento.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes da coleção serão atualizados um de cada vez na sequência que configura. Um cliente só irá instalar atualizações de software depois de o cliente que está à sua frente na lista ter terminado de instalar as suas atualizações de software.  

5.  Especifique se utilizar á função de um script pré-implantação (drenagem do nó) ou de uma script pós-implantação (resumo do nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar em testes para scripts de pré-implantação e pós-implantação que escrevam o tempo atual num ficheiro de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implementar atualizações de software para o grupo de servidores e monitorizar o estado  

1.  [Implemente atualizações](https://technet.microsoft.com/library/gg712304.aspx) de software para a coleção do grupo de servidores.  

2.  [Monitorize a implementação da atualização do software](https://technet.microsoft.com/library/gg712304.aspx). Além das vistas padrão de monitorização para a implementação de atualizações de software, uma nova descrição do estado é exibida quando um cliente aguarda a sua vez de instalar as atualizações de software. **À espera de fechadura** é exibido para este novo estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para limpar os bloqueios de implementação de computadores num grupo de servidores  

1.  No espaço de trabalho **de Ativos e Compliance,** clique em **Coleções de Dispositivos**e clique na recolha para limpar fechaduras de implementação.  

2.  No separador **Home,** no grupo **de implementação,** clique em **Clear Server Group Deployment Locks**. Quando os clientes não instalaram as atualizações do software e estão a impedir outros clientes de instalarem as suas atualizações de software, os bloqueios de implementação podem ser manualmente apurados.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a>Suporte para serviço de proteção de ameaças avançadas Microsoft Defender  
 O Microsoft Defender Advanced Threat Protection (ATP) é um serviço que ajudará as empresas a detetar, investigar e responder a ataques avançados nas suas redes. O Microsoft Defender ATP é anteriormente conhecido como Windows Defender ATP. Saiba mais sobre [o Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). O Gestor de Configuração pode ajudá-lo a bordo e monitorizar os dispositivos clientes geridos pelo Windows 10 Anniversary Edition.  

### <a name="try-it-now"></a>Tente agora!  
 Tente completar as seguintes tarefas e, em seguida, deixe-nos saber como funcionou usando o nosso formulário de feedback na página do programa de feedback do Gestor de [Configuração](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) no site do Microsoft Connect:  

- Dispositivos de bordo para o serviço online Microsoft Defender Advanced Threat Protection (ATP)  

- Monitorize a implementação ATP do Microsoft Defender para dispositivos geridos  

  **Pré-requisitos**  

- Subscrição do serviço online Microsoft Defender Advanced Threat Protection  

- Clientes com windows 10, Edição de Aniversário (construção 14328 ou maior)  

- Criar um ficheiro de configuração de embarque de cliente  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um ficheiro de configuração de embarque  

  1.  Logon para o serviço on-line ATP Microsoft Defender  

  2.  Clique no item do menu de **embarque do cliente**  

  3.  Selecione **'Gestor de Configuração'** e clique no **pacote de descarregamento**.  

  4.  Descarregue o ficheiro de arquivo comprimido (.zip) e extrai o conteúdo.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Dispositivos de bordo para Microsoft Defender ATP  

1. Na consola de Configuração Manager, navegue **nos Ativos e** > na**visão geral** > de conformidade**As** > **políticas ATP do Windows Defender** e clique em Criar a Política **ATP do Windows Defender**. Abre o Assistente de Política ATP da Microsoft Defender.  

2. Digite o **nome** e **descrição** para a política ATP do Microsoft Defender e selecione **Onboarding**. Clique em Seguinte.  

3. **Navegue** no ficheiro Configuração fornecido pelo inquilino do serviço de nuvem ATP da sua organização. Clique em **Seguinte**.  

4. Especifique as amostras de ficheiro que são recolhidas e partilhadas a partir de dispositivos geridos para análise.  

   - **Nenhum** – Nenhum - Não são recolhidos ficheiros de amostra supor para análise  

   - **Ficheiros executáveis portáteis** – Ficheiros como ficheiros de programas (.exe), ficheiros de link de biblioteca dinâmica (.dll), ficheiros de fontes e ficheiros semelhantes que podem ser explorados em ciberataques são recolhidos e partilhados para análise  

     Clique em **Seguinte**.  

5. Reveja o resumo e complete o assistente.  

6. Agora pode implementar a política ATP do Microsoft Defender para gerir computadores de cliente clicando em **Implementar**.  

##### <a name="monitor-microsoft-defender-atp"></a>Monitor Microsoft Defender ATP  

1.  Na consola 'Gestor de Configuração', navegue na **Monitorização** > da**Visão Geral** > **segurança** e, em seguida, clique no Windows **Defender ATP**.  

2.  Reveja o painel de proteção de ameaças avançada do Microsoft Defender.  

    -   **Windows Defender Agent Deployment Status** – O número e percentagem de computadores de clientes geridos elegíveis com a política ATP ativa do Microsoft Defender a bordo  

    -   **Windows Defender ATP Agent Health** – Percentagem de clientes de computador que reportam o estado do seu agente ATP Microsoft Defender  

        -   **Saudável** - Trabalhar corretamente  

        -   **Inativo** - Não há dados enviados ao serviço durante o período de tempo  

        -   **Estado do agente** - O serviço de sistema para o agente no Windows não está a funcionar  

        -   **Sem bordo** - A política foi aplicada, mas o agente não comunicou a política a bordo  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a>Atestação de saúde do dispositivo no local  
 O atestado de saúde para dispositivos Windows 10 pode agora ser configurado para comunicar utilizando a infraestrutura no local. Os administradores podem especificar se o relatório é feito através da nuvem ou dos recursos no local. Se no local for selecionado para reporte de atestado de saúde, então um URL pode ser especificado para o serviço. Isto permite aos clientes pCs sem acesso à Internet para ativar e gerir dispositivos usando atestado de saúde.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Permitir o atestado de saúde para dispositivos no local  
 Em 1605, corrigimos alguns bugs descobertos em 1604 De Pré-visualização Técnica.  Para experimentá-lo, configure no local o Serviço de Attestation de Saúde utilizando as definições do agente cliente.  

1.  Na consola do Gestor de Configuração, navegue nas**definições**do Cliente de**Visão Geral** > da **Administração** > e, em seguida, coloque **o Serviço de Atestado** de Saúde no local para **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a>Novas opções de reinício para clientes do Windows 10 após instalação de atualização de software  
 Quando uma atualização de software que requer um reinício é implementada utilizando o 'Gestor de Configuração' e instalada num computador, está programado um reinício pendente e é apresentada uma caixa de diálogo de reinício. Atualmente, para o Windows 8 ou acima, se desligar ou reiniciar o computador utilizando as opções de Energia do Windows (em vez do diálogo de reinício), o diálogo de reinício permanece após o reinício do computador e o computador terá de reiniciar no prazo configurado. Nesta pré-visualização técnica, a opção de **Atualizar e Reiniciar** e Atualizar e **Desligar** estará disponível nos computadores do Windows 10 nas opções de Energia do Windows sempre que exista um reinício pendente para uma atualização de software do Gestor de Configuração. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será apresentada depois do reinício do computador.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a>Pré-declarar dispositivos corporativos com número de série IMEI ou iOS  
 Pode agora identificar dispositivos corporativos importando os seus números de identidade de equipamento móvel de estação internacional (IMEI). Pode fazer o upload de um ficheiro de valores separados da vírem (.csv) contendo números IMEI do dispositivo ou pode introduzir manualmente as informações do dispositivo.  Também pode importar números de série para dispositivos iOS.  As informações importadas definirão a propriedade dos dispositivos que se inscrevem como "Corporate".  É ainda necessária uma licença Intune para cada utilizador que aceda ao serviço.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar as seguintes tarefas e, em seguida, deixe-nos saber como funcionou usando o nosso formulário de feedback na página do programa de feedback do Gestor de [Configuração](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) no site do Microsoft Connect:  

-   Importar um conjunto de números IMEI num ficheiro .csv. Cada linha pode conter o número IMEI seguido de um campo de detalhes.  

-   Importar manualmente os números IMEI da consola 'Gestor de Configuração'.  

-   Importar um conjunto de números de série iOS num ficheiro .csv. Mais uma vez, cada linha contém um número seguido de quaisquer detalhes para o dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS  

1. Na consola do Gestor de Configuração, vá **Assets e Compliance** > **Overview** > **Todos os dispositivos** > **pré-declarados**de propriedade corporativa, e, em seguida, clique em Criar **Dispositivos Pré-declarados**. O assistente pré-declarado dos dispositivos abre.  

2. Especifique como pretende adicionar informações do dispositivo:  

   -   **Faça upload de um ficheiro .csv contendo números e detalhes IMEI** - Para fazer upload de uma lista de números, consulte o Passo #3.  

   -   **Adicione manualmente os números e detalhes IMEI** - Para introduzir manualmente informações, digite o número iMEI ou o número de série iOS IOS e detalhes para os dispositivos, e depois proceda ao Passo #4.  

3. Para ficheiros carregados, navegue para o ficheiro .csv contendo informações para pré-declarar dispositivos corporativos. O ficheiro deve ter o seguinte formato, excluindo a linha superior (prevista apenas para orientação):  

   |**IMEI #**|**iOS Serial**|**OS**|**Detalhes**|
   |---|---|---|---|
   |123456789012345||JANELAS|Dispositivo Windows da empresa|
   |123456789012|A0BCD0EFGH0J|iOS|Dispositivos iOS pertencentes à empresa|
   |123456789012346||ANDROID|Dispositivo Android da empresa|

    **Colunas:**  

   - Coluna 1: Número IMEI – Ou é necessário um número IMEI ou um número de série iOS para cada linha  

   - Coluna 2: número de série iOS – Apenas os números de série iOS podem ser pré-declarados. Utilize o número IMEI para outras plataformas de dispositivos  

   - Coluna 3: Sistema operativo do dispositivo (capitalização necessária):  

     -   iOS – Todos os dispositivos iOS  

     -   WINDOWS – Inclui Windows Phone, Janela 10 Mobile e PCs Windows  

     -   ANDROID – Todos os dispositivos Android  

   - Coluna 4: Detalhes – Informações adicionais do dispositivo que aparecem na consola do Gestor de Configuração  

     Clique em **Seguinte**.  

4. Reveja os resultados da importação de ficheiros. Os números de IMEI ou de série previamente importados terão os seus dados atualizados com novos detalhes.  Clique em **Next** para continuar ou **voltar** para preservar detalhes atualizados e, em seguida, completar o assistente.  
