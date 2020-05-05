---
title: Capacidades na Pré-visualização Técnica 1604
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074457"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1604 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1604. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a>Gerir aplicações compradas em volume a partir da Windows Store for Business  
 O [Windows Store for Business](https://www.microsoft.com/business-store) é onde pode encontrar e comprar aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Gestor de Configuração, pode gerir aplicações adquiridas em volume a partir da consola 'Gestor de Configuração', por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Gestor de Configuração  

-   Aplicações sincronizadas aparecem na consola Do Gestor de Configuração e pode supor estas como quaisquer outras aplicações  

-   Pode rastrear quantas licenças estão disponíveis e quantas estão a ser usadas na consola Do Gestor de Configuração  

### <a name="try-it-out"></a>Experimente!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Cenário 1: Configurar a Windows Store para sincronização de negócios  

1.  No Diretório Ativo do Azure, registe o Gestor de Configuração como uma ferramenta de gestão "Web Application and/ou Web API". Isto lhe dará uma identificação do cliente de que precisará mais tarde.  

    1.  No nó de **Diretório Ativo** de [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Diretório Ativo Azure e, em seguida, clique em **Aplicações** > **Adicionar**.  

    2.  Clique **Em adicionar uma aplicação que a minha organização está a desenvolver.**  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API,** em seguida, clique na seta Seguinte.  

    4.  Introduza o mesmo URL tanto para o **URL de inscrição** como para o **ID de aplicação URI**.  O URL pode ser qualquer coisa e não precisa de resolver um endereço real. Por exemplo, pode introduzir **https://&lt;seu domínio\>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Ative Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **Configurar**.  

    2.  Em **Teclas,** selecione uma duração da lista e clique em **Guardar**.  Isto criará uma nova chave de cliente.  Não navegue para longe desta página até ter embarcado com sucesso na Windows Store para Business to Configuration Manager.  

3.  Na Windows Store for Business, configure o Gestor de Configuração como a ferramenta de gestão da loja.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e inscreva-se, se solicitado.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Em **Ferramentas de Gestão,** clique **em Adicionar uma ferramenta de gestão**.  

    4.  Em **Procurar a ferramenta pelo nome,** digite o nome da aplicação que criou anteriormente em AAD e, em seguida, clique em **Adicionar**.  

    5.  Clique em **Ativar** ao lado da aplicação que acabou de importar.  

    6.  No assistente de **apps licenciadas offline,** clique **em Sim** se quiser permitir a compra de aplicações licenciadas offline.  

4.  Compre pelo menos uma aplicação na Windows Store para Negócios.  

5.  No espaço de trabalho da **Administração** da consola De Configuração Manager, expanda os **Serviços Cloud**e, em seguida, clique na **Windows Store para negócios**.  

6.  No separador **Home,** no grupo **Criar,** clique em **Adicionar Windows Store para Conta De Negócios**.  

7.  Adicione o seu ID de inquilino, identificação do cliente e chave de cliente do Azure Ative Directory, em seguida, complete o assistente.  

8.  Uma vez feito, verá a conta configurada na lista **da Windows Store para Contas Empresariais** na consola 'Gestor de Configuração'.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Cenário 2: Criar e implementar uma aplicação de Gestor de Configuração a partir de uma aplicação licenciada de Windows Store para Empresas offline  

1.  No espaço de trabalho da Biblioteca de **Software** da consola Do Gestor de Configuração, expanda a **Gestão**de Aplicações e, em seguida, clique em Informações de **Licença para Aplicações de Loja**.  

2.  A lista de **aplicações do Windows Store para Empresas adquiridas** mostra uma lista de aplicações que foram sincronizadas a partir da loja. Escolha a aplicação que pretende implementar, então, no separador **Home,** no grupo **Criar,** clique em **Criar Aplicação**.  

3.  É criada uma aplicação 'Gestor de Configuração' que contém a aplicação Windows Store for Business. Em seguida, pode implementar e monitorizar esta aplicação como faria qualquer outra aplicação do Gestor de Configuração.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a>Melhorias no Passaporte da Microsoft para gestão do trabalho  
 Agora pode implementar políticas de Passport for Work para dispositivos Windows 10 juntos ao domínio geridos pelo cliente do Gestor de Configuração.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a>Opção para os clientes mudarem para um novo ponto de atualização de software  
 Na Pré-visualização Técnica de 1604, pode permitir que a opção para os clientes do Gestor de Configuração mudar para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Para esta opção, deve ter vários pontos de atualização de software disponíveis num site primário. Permite esta opção numa recolha de dispositivos, e uma vez ativado, os clientes da coleção procurarão outro ponto de atualização de software na próxima digitalização quando o cliente não conseguir ligar-se com sucesso ao ponto de atualização de software ativo. Dependendo das definições de configuração do WSUS (classificações de atualização, produtos, etc.), o interruptor para um novo ponto de atualização de software gerará tráfego de rede adicional. Por conseguinte, só deve utilizar esta opção quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para ativar a opção para mudar pontos de atualização de software  

1.  Na consola do Configuration Manager, aceda a **Ativos e Compatibilidade > Descrição geral > Coleções de dispositivos**.  

2.  No separador **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e, em seguida, clique em **Mudar para o Ponto de Atualização de Software seguinte**.  

> [!NOTE]  
>  Esta opção só está disponível em sites que tenham vários pontos de atualização de software.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a>Configurações do cliente para gerir as Definições de Cache do Cliente e cache de pares de clientes  
 A versão de pré-visualização técnica 1604 introduz duas novas definições de cliente de dispositivoque afetam a utilização da cache de um cliente. Ambos podem ser usados individualmente, mas estão configurados na mesma folha de propriedades para configurações do cliente e combinam-se para ajudá-lo a gerir a implementação de conteúdo para os seus clientes em locais remotos.  

-   Em primeiro lugar, o **cliente Peer Cache**, uma solução de Gestor de Configuração incorporada para os clientes partilharem conteúdo com outros clientes diretamente a partir da sua cache local. Para que os clientes da Peer Cache partilhem conteúdos, devem ser membros do mesmo grupo de fronteiras. Peer Cache não substitui o uso de outras soluções como bracnchCache, mas em vez disso trabalha lado a lado para lhe dar mais opções para estender as soluções tradicionais de implementação de conteúdo, como pontos de distribuição.  

     Depois de implementar as definições de cliente que permitem a Peer Cache uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo de pares para outros clientes no seu grupo de fronteira.  O cliente que opera como fonte de conteúdo de pares apresentará uma lista de conteúdos disponíveis que tem em cache para o seu ponto de gestão. Então, quando o próximo cliente nesse grupo de fronteira supõe que o conteúdo, a fonte de cache de pares é oferecida como uma fonte de conteúdo potencial, juntamente com todos os pontos de distribuição que estão configurados para serem rápidos. O cliente seleciona uma fonte de conteúdo aleatória a partir deste conjunto combinado de fontes de conteúdo. Os clientes apenas procurarão conteúdo a partir de um ponto de distribuição que esteja configurado para ser lento quando não houver pontos de distribuição rápida ou fontes de cache de pares presentes no grupo de fronteira.  

-   A segunda nova definição permite-lhe **gerir o tamanho da cache** nos clientes. Pode definir a cache para ter um tamanho máximo em megabytes e um tamanho máximo em percentagem dos clientes que conduzem o espaço.  O cliente aplica a definição que é alcançada primeiro.  

Para ajudá-lo a compreender o uso do cliente Peer Cache, pode ver o dashboard Fontes de Dados do **Cliente.** Na consola vai para **a Monitorização > Estado**do Cliente > Fontes de Dados do Cliente. Aqui pode selecionar um período de tempo para se aplicar ao painel de instrumentos. Em seguida, no visor, pode selecionar o grupo ou pacote de limites para o qual pretende visualizar informações. Ao visualizar informações, pode pairar sobre o rato sobre a superfície para ver mais detalhes sobre os diferentes conteúdos ou fontes políticas.  

 Também pode utilizar um novo relatório, Fontes de **Dados do Cliente - Summarization**, para ver uma resumição das fontes de dados do cliente para cada grupo de fronteiras.   
**Requisitos para utilizar peer cache:**  

-   Tem de configurar o seu site com uma Conta de Acesso à **Rede** que tenha **controlo total** na pasta cache de cada cliente. Por padrão, isto é **%windir%\ccmcache**  

-   Os clientes só podem transferir conteúdo usando o Peer Cache quando são membros do mesmo grupo de fronteiras.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições do cliente Peer Cache  

1.  Ambas as definições estão configuradas na mesma página das definições do cliente. Na consola 'Gestor de Configuração', vá à **Administração > Definições**de Cliente e, em seguida, abra as definições do cliente do dispositivo que pretende utilizar. Também pode modificar o objeto de Definições de Cliente Predefinido.  

2.  A partir da lista de definições disponíveis, selecione **Definições**de Cache do Cliente .  

3.  Para gerir o tamanho da cache, detete o tamanho da cache do **cliente configure** igual a **Sim**. Em seguida, pode configurar o tamanho máximo da cache tanto para megabytes como em percentagem dos clientes que conduzem o espaço.  

4.  Para permitir que os clientes participem no Cliente Peer Cache, detete **o cliente Enable Configuration Manager em pleno SISTEMA para partilhar conteúdo** igual a **Sim**. Em seguida, pode configurar as portas que os clientes usam, incluindo se forem HTTP ou HTTPS.  

### <a name="try-it-out"></a>Experimente!  
 Tente completar as seguintes tarefas e, em seguida, use as informações de feedback perto do topo deste tópico para nos informar como funcionava:  

1.  Modifique as definições do cliente para especificar um novo tamanho para a cache do cliente e, em seguida, confirme esta definição num cliente.  

2.  Utilize as definições do cliente para configurar vários clientes para usar o Peer Cache  

3.  Implemente conteúdo para clientes para que alguns ou a maioria dos clientes obtenha esse conteúdo de outro cliente utilizando o Peer Cache.  Pode confirmar a fonte de conteúdo que é utilizada através da visualização de um novo dashboard.  

    > [!NOTE]  
    >  Para completar esta tarefa com a pré-visualização técnica e um único ponto de distribuição, configure o ponto de distribuição para ser lento para a localização da rede de todos os seus clientes. Em seguida, distribua o conteúdo a um único cliente.  Depois desse cliente obter o conteúdo, pode distribuir o conteúdo a clientes adicionais que deverão encontrar os pares locais a usar como fonte de conteúdo antes de utilizar o ponto de distribuição que é considerado lento a partir da localização do cliente.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a>Suporte para Passaporte para Trabalho como KSP  
 O Gestor de Configuração permite-lhe integrar-se com o Microsoft Passport for Work, que é um método alternativo de entrada que utiliza o Ative Directory, ou uma conta de Diretório Ativo Azure para substituir uma palavra-passe, cartão inteligente ou cartão inteligente virtual.  
Com o Passport, pode utilizar um gesto de utilizador para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica, como o Windows Hello, ou um dispositivo externo, como um leitor de impressões digitais.  

-   Pode utilizar o Configurmanager de configuração para controlar quais os gestos que os utilizadores podem e não podem usar para iniciar sessão e configurar os requisitos de complexidade pin.  

-   Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Passport for Work.  

Quando um utilizador cria um PIN de Passaporte, o Windows envia uma notificação que o Gestor de Configuração ouve.  Isto permite que o Gestor de Configuração se apercebam rapidamente dos utilizadores que criaram um PIN de Passaporte. O Gestor de Configuração também pode emitir novos certificados para esses utilizadores se o Passport for utilizado como Fornecedor de Armazenamento chave num perfil de certificado.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a>Atestação de saúde do dispositivo no local  
 O atestado de saúde para dispositivos Windows 10 pode agora ser configurado para comunicar utilizando a infraestrutura no local.  Os administradores podem especificar se o relatório é feito através da nuvem ou dos recursos no local.  Se **no local** for selecionado para reporte de atestado de saúde, então um URI pode ser especificado para o serviço. Isto permite aos clientes pCs sem acesso à Internet para usar e gerir dispositivos usando atestado de saúde.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Permitir o atestado de saúde para dispositivos no local  

1.  Na consola do Gestor de Configuração, navegue nas**definições**do Cliente de**Visão Geral** > da **Administração** > e, em seguida, coloque **o Serviço de Atestado Saudável no local** para **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

Para experimentá-lo, configure no local o Serviço de Attestation de Saúde utilizando as definições do agente cliente.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a>Definição smartLock para dispositivos Android  
 Uma nova definição, **Allow SmartLock e outros agentes fidedignos** foi adicionada ao item de configuração **Android e Samsung KNOX** que permite controlar a funcionalidade SmartLock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe de bloqueio do ecrã do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para evitar que os utilizadores finais configurem o SmartLock.  
