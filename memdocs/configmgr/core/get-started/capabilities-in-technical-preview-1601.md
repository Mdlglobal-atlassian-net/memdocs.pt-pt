---
title: Capacidades na Pré-visualização Técnica 1601
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed3f53b6e2e9557def20fc459dfcf4641b0e396d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905829"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1601 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1601. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 **Questões Conhecidas para esta Pré-visualização Técnica:**  

-   Quando gere **as Opções** de Atualização de Clientes para promover um cliente de pré-produção à produção, o texto para a caixa de verificação apresenta uma versão cliente de zero (0) em vez do número real de construção do cliente. A versão correta do cliente pré-produção é mostrada na superfície acima desta opção, e é a versão cliente que é promovida à produção quando você seleciona esta opção.  

-   Ao atualizar para a Pré-Visualização Técnica 1601 e optar por testar o cliente do Gestor de Configuração numa coleção de pré-produção, o pacote de clientes para a recolha não será atualizado. Esta edição é apenas para Pré-visualização Técnica 1601.  

     Para contornar estas questões, faça uma das seguintes:  

    -   Executar o seguinte script SQL na base de dados do site principal:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Adicione uma nova função do sistema de site de pontos de distribuição ao seu site de laboratório. O novo ponto de distribuição irá atualizar a coleção de pré-produção com o novo pacote de clientes.  

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a>Melhorias na integração do Microsoft Intune  
Na Pré-Visualização Técnica de 1601, adicionámos suporte para as seguintes funcionalidades:  

### <a name="improvements-to-conditional-access"></a>Melhorias no Acesso Condicional  

-   **Suporte de acesso condicional para Computadores que são geridos pelo Gestor de Configuração**  

     Agora pode definir políticas de acesso condicional para Computadores geridos pelo Gestor de Configuração, o que exigirá que os Computadores estejam em conformidade com a política de conformidade de forma a aceder aos serviços Exchange Online e SharePoint Online.  Com esta nova funcionalidade, também pode registar Computadores com AD Azure através da política de conformidade, e monitorizar e reportar sobre o registo da AD Azure.  

    > [!NOTE]  
    >  O Acesso Condicional ainda não é suportado no Windows 10.  

    Seguem-se os pré-requisitos para utilizar esta funcionalidade:  

    -   Assinatura Azure Ative Directory Premium e ADFS Sync.  

    -   Uma Subscrição do Microsoft Intune. A subscrição Intune da Microsoft deve ser configurada na Consola de Gestor de Configuração.  

    -   [Pré-requisitos para a inscrição automática da AD Azure](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Para utilizar a opção, deve criar uma política de conformidade no Gestor de Configuração com regras específicas descritas abaixo e definir uma política de acesso condicional na consola Intune.  Além disso, para garantir que só são permitidos acessos a Computadores compatíveis, tem de definir o requisito do Windows PC para **dispositivos, devendo ser** uma opção conforme. Seguem-se as regras de política conformes aplicáveis aos Computadores geridos pelo Gestor de Configuração.  

    -   **Exigir inscrição no Azure ActiveDirectory:** Esta regra verifica se o dispositivo do utilizador é local de trabalho associado ao Azure AD e, caso contrário, o dispositivo é automaticamente registado em Azure AD. O registo automático é suportado apenas no Windows 8.1. Para PCs Windows 7, implemente um MSI para efetuar o registo automático. Para mais informações, consulte [aqui.](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

    -   **Todas as atualizações necessárias instaladas com um prazo superior a um determinado número de dias:** Esta regra verifica se o dispositivo do utilizador tem todas as atualizações necessárias (especificadas na regra de **atualizações automáticas necessárias)** dentro do prazo e do período de carência especificado por si, e instala automaticamente as atualizações pendentes.  

    -   **Requerer encriptação de unidade BitLocker:** Esta é uma verificação para ver se a unidade primária (por exemplo, C: \\ ) no dispositivo é encriptada pelo BitLocker. Se a encriptação Bitlocker não estiver ativada no dispositivo primário, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    -   **Requerer Antimalware:** Esta é uma verificação para ver se o software antimalware (System Center Endpoint Protection ou Windows Defender) está ativado e em funcionamento.  
         Se não estiver ativado, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    Os utilizadores finais que forem bloqueados devido à não conformidade verão informações de conformidade no Centro de Software e iniciarão uma nova avaliação de política quando os problemas de conformidade forem remediados.  

-   Acesso condicional ao Serviço de **Atestados de Saúde** Pode agora restringir o acesso a e-mails e serviços 0365 com base na saúde dos dispositivos, conforme reportado pelo Serviço de Atestados de Saúde.  Além disso, os dispositivos que são geridos pela Intune estão incluídos nos relatórios de saúde do dispositivo.  

    Foi adicionada uma nova regra de conformidade à consola do gestor de configuração que permite especificar se os dispositivos devem ser permitidos ou bloquear o acesso com base no seu estado de saúde.  Para criar esta regra, abra o Assistente de Política de **Conformidade,** e adicione uma nova regra.  Selecione o Reportado como Serviço de Atestado de **Saúde** para a circunstância e detetete o valor para **True**.  Isto irá garantir que apenas dispositivos que são reportados como saudáveis terão acesso aos recursos da sua empresa. Para mais detalhes sobre o Serviço de Atestado de Saúde e como a saúde dos dispositivos é reportada em Intune, consulte [Attestation de Saúde](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)do Dispositivo .  

-   **Novas definições de política** de conformidade: As novas definições de política de conformidade ajudam a melhorar a segurança e a proteção em dispositivos que são utilizados para aceder a e-mails da empresa e serviços SharePoint:  

    -   **Requerer atualizações automáticas:** Pode requerer dispositivos com o Windows 8.1 ou mais tarde para permitir a instalação automática de atualizações e também especificar a classe de atualizações que estão instaladas.  Pode optar por: instalar apenas atualizações marcadas como importantes ou instalar todas as atualizações recomendadas.  

         Para criar uma regra para atualizações automáticas, abra o Assistente de Política de **Conformidade Criar,** e adicione uma nova regra.  Selecione **classificação mínima das atualizações necessárias** como condição e detete o valor para um dos valores disponíveis: **Nenhum,** **recomendado**, e **importante**.  

        -   **Nenhuma:** As atualizações não são instaladas automaticamente.  

        -   **Recomendado:** Todas as atualizações recomendadas estão instaladas  

        -   **Importante:** Apenas são instaladas atualizações classificadas como importantes.  

    -   **Requerer uma palavra-passe para desbloquear dispositivos móveis:** Quando esta definição estiver definida para **Sim,** os utilizadores finais devem introduzir uma palavra-passe antes de poderem aceder ao seu dispositivo.  

         Para criar uma regra para a palavra-passe desbloquear dispositivos móveis, abra o Assistente de Política de **Conformidade criar**e adicione uma nova regra. Selecione **Exigir uma palavra-passe para desbloquear um dispositivo ocioso** como condição e definir o valor para **True**.  

    -   **Minutos de inatividade antes da palavra-passe ser necessária:**  Especifica o tempo de inatividade antes de o utilizador voltar a introduzir a sua palavra-passe.  

         Para criar esta regra, abra o Assistente de Política de **Conformidade,** e adicione uma nova regra. **Selecione Minutos de inatividade antes que a palavra-passe seja necessária** como condição, e delineie o valor para uma das opções disponíveis: 1 minuto, 5 minutos, 15 minutos, 30 minutos, hora.  

-   **Anulação da regra por defeito - Permita sempre que os dispositivos inscritos e conformes intune acedam à Exchange on-pre-presionéri:**  

     Quando verificar esta opção, os dispositivos que estão matriculados no Intune e em conformidade com as políticas de conformidade podem aceder ao Exchange on-pre-presion. Esta regra substitui a Regra padrão, o que significa que mesmo que estabeleça a Regra padrão para quarentena ou bloquear o acesso, os dispositivos matriculados e conformes ainda poderão aceder ao Exchange on-premis.  
     Utilize esta definição quando quiser que os dispositivos matriculados e conformes tenham sempre acesso a e-mail através do Exchange on-pre-preser.  

     Isto é suportado nas seguintes plataformas: Windows Phone 8 e posteriormente, iOS 6 e mais tarde. Android 4.0 e mais tarde, Samsung KNOX Standard 4.0 e mais tarde.  

     Para utilizar esta opção, aceda à página **geral** do Assistente de Política de **Acesso Condicional configurado** para o intercâmbio no local.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a>Estado on-line do cliente  
Começando com a pré-visualização técnica 1601, pode identificar de uma forma resumida se um cliente está online ou offline na consola Do Gestor de Configuração. Com ícones e colunas atualizados nas listas de dispositivos de consola, pode avaliar o estado dos clientes no seu ambiente para identificar áreas problemáticas e outros problemas que possam necessitar da sua atenção.  

Um cliente está on-line se está atualmente ligado a uma função de sistema de site de ponto de gestão de gestor de configuração. Enquanto o ponto de gestão estiver a receber mensagens semelhantes a ping do cliente, o seu estado está online. Se a gerência não receber uma mensagem durante 5 minutos ou mais, o estado do cliente muda para offline.  

### <a name="icons-for-client-status"></a>Ícones para o estado do cliente  

|||  
|-|-|  
|![ícone de estado online dos clientes](media/online-status-icon.png)|O cliente está online.|  
|![ícone de estado offline dos clientes](media/offline-status-icon.png)|O cliente está offline.|  
|![ícone de estado desconhecido dos clientes](media/unknown-status-icon.png)|O estado do cliente é desconhecido.|  

### <a name="prerequisites"></a>Pré-requisitos  
 O estado on-line do cliente não tem pré-requisitos. Pode começar a usá-lo assim que a pré-visualização técnica do Diretor de Configuração 1601 estiver instalada.  

### <a name="limitations"></a>Limitações  
 O estado on-line do cliente só está disponível para computadores Windows com o cliente Do Gestor de Configuração instalado. O estado on-line do cliente não é suportado para computadores Mac, computador Linux ou UNIX, ou dispositivos geridos com a \- On premises Mobile Device Management.  

### <a name="to-view-client-online-status"></a>Para ver o estado on-line do cliente  

1. Na consola do Gestor de Configuração, vá a **Ativos e Compliance > Visão Geral > Dispositivos.**  

2. Clique no cabeçalho da coluna e clique num dos campos de estado on-line do cliente para adicioná-lo à vista do dispositivo. Os campos são  

   -   **Estado Online do Dispositivo** indica se o cliente está atualmente online ou offline.  

   -   **O último Tempo Online** indica quando o estado online do cliente passou de offline para online.  

   -   **O tempo offline último** indica quando o estado mudou de online para offline.  

   Para mostrar alterações recentes no estado do cliente, refresque a consola.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a>Melhorias na gestão de aplicações  
 Na Pré-Visualização Técnica de 1601 adicionámos suporte para as seguintes funcionalidades:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Algumas lojas de aplicações permitem comprar várias licenças para uma aplicação que pretende executar na empresa. Isto ajuda a reduzir a sobrecarga administrativa de controlar várias cópias adquiridas de aplicações.  

 O Gestor de Configuração ajuda-o agora a gerir as aplicações que adquiriu através de um programa deste tipo, importando as informações da licença da loja de aplicações e rastreando quantas das licenças que utilizou.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - Configuração de aplicações para aplicações<br />Híbrido  
 Algumas aplicações iOS suportam a pré-configuração de definições, tais como um servidor ou base de dados a que a aplicação deve estabelecer ligação. O Gestor de Configuração suporta agora a implementação de políticas de configuração de apps para o dispositivo que permitem ao utilizador utilizar a aplicação imediatamente sem precisar de saber esta informação. Os desenvolvedores devem ativar esta funcionalidade nas suas apps.  

 Um número limitado de aplicações publicamente divulgadas suportam atualmente configurações pré-configuradas; você também pode ter uma linha de aplicativos de negócios desenvolvidos internamente que suportam estas.  

#### <a name="prerequisites-for-this-scenario"></a>Pré-requisitos para este cenário  

-   Deve ter adicionado uma subscrição intune da Microsoft ao 'Gestor de Configuração'.  

-   Deve ter adicionado um certificado apple APNs válido à subscrição Intune.  

-   Deve ter implementado uma aplicação iOS que suporta a configuração da aplicação.  

#### <a name="try-it-out"></a>Experimente!  
 Uma vez cumpridos os pré-requisitos acima, deve criar uma aplicação De Configuração Manager que utilize um tipo de implementação iOS. A aplicação que utiliza deve apoiar a configuração da aplicação. Consulte a documentação do fornecedor da aplicação para saber que itens específicos (pares de nome/valor), pode configurar.  

 Em seguida, associa a política de configuração da aplicação ao tipo de implementação do iOS durante a implementação da aplicação. Também pode implementar a política a partir do nó de Políticas de Configuração de **Aplicações,** direcionado para uma app e recolha existentes.  

 Tente completar as seguintes tarefas e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionavam:  

-   Se tiver uma aplicação iOS que suporte a configuração da aplicação, consulte a documentação do fornecedor de aplicações para saber o nome e os pares de valor que deve especificar para configurar a aplicação.  

-   Inicie o assistente de política de configuração de **aplicações.** Na página política do **iOS** do assistente, tente adicionar o nome e os pares de valor que encontrou na documentação do fornecedor de aplicações ou pode importar um ficheiro XML contendo os valores exigidos.  

-   No assistente de **software de implementação,** na página política de configuração de **aplicações,** associar a política de configuração da aplicação que criou com um tipo de implementação compatível a partir da aplicação.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a>Melhorias nas definições de conformidade  
 Na Pré-Visualização Técnica de 1601 adicionámos suporte para as seguintes funcionalidades:  

### <a name="microsoft-edge-browser-settings"></a>Configurações do navegador Microsoft Edge  
 Foram adicionadas novas definições para o navegador Microsoft Edge para o dispositivo de configuração **Do Windows 8.1 e Windows 10** (as definições aplicam-se apenas aos dispositivos do Windows 10).  

 Para ver as novas definições, escolha o **Microsoft Edge** na página de **definição** do dispositivo configuração do assistente de **configuração.**  

 Para mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Definições de conformidade para dispositivos da Equipa Windows 10  
 Utilize estas novas definições de conformidade para configurar dispositivos que executam a equipa do Windows 10, como dispositivos Surface Hub.  

 Para ver as novas definições, escolha o **Windows 10 Team** a partir da página de **definição** de configuração do dispositivo configuração do assistente de **configuração.**  

 Para mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - Modo quiosque para samsung KNOX Standard<br />Híbrido  
 O modo quiosque permite bloquear um dispositivo para permitir que certas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda. Estas definições não estão disponíveis para dispositivos Samsung KNOX Standard no dispositivo de configuração **Do Windows 8.1 e Windows 10** (as definições aplicam-se apenas aos dispositivos Windows 10).  

 Para ver as novas definições, escolha o **Modo Quiosque - Samsung KNOX** da página de **definição** de configuração do dispositivo configurar o assistente de **configuração.**  

 Para mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
