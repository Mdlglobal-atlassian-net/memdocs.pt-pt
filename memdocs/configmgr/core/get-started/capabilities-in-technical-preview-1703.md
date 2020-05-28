---
title: Capacidades na Pré-visualização Técnica 1703
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fb13844dd05049b9186909884aa0c457a8cfacd9
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428414"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1703 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1703. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

Agora pode implementar aplicações licenciadas para dispositivos e utilizadores. Dependendo da capacidade de aplicação para suportar o licenciamento do dispositivo, uma licença apropriada será reclamada quando a implementar, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Gestor de Configuração|App suporta licenciamento de dispositivos?|Tipo de recolha de implantação|Licença reclamada|
|Mais cedo que 1702|Sim|Utilizador|Licença de utilizador|
|Mais cedo que 1702|Não|Utilizador|Licença de utilizador|
|Mais cedo que 1702|Sim|Dispositivo|Licença de utilizador|
|Mais cedo que 1702|Não|Dispositivo|Licença de utilizador|
|1702 e mais tarde|Sim|Utilizador|Licença de utilizador|
|1702 e mais tarde|Não|Utilizador|Licença de utilizador|
|1702 e mais tarde|Sim|Dispositivo|Licença de dispositivo|
|1702 e mais tarde|Não|Dispositivo|Licença de utilizador|


## <a name="direct-links-to-applications-in-software-center"></a>Links diretos para aplicações no Centro de Software

Agora pode fornecer aos utilizadores finais uma ligação direta a uma aplicação no Software Center. Isto significa que já não devem abrir o Centro de Software e procurar uma aplicação antes de poderem instalá-la. Isto está disponível apenas para aplicações do Gestor de Configuração, não para pacotes e programas ou sequências de tarefas.

### <a name="try-it-out"></a>Experimente                 

Utilize o seguinte formato URL para abrir o Centro de Software a uma determinada aplicação:

**Centro de Software:SoftwareId=_Identificador de aplicações_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Como obter o identificador de aplicação de uma aplicação.

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho da Biblioteca de Software, expanda a Gestão de **Aplicações,** clique em **Aplicações.**
3. Na vista **Aplicações,** clique num dos cabeçalhos da coluna e, em seguida, a partir da lista, selecione **CI Unique ID**. Verá que a identificação única de cada aplicação está agora mostrada na lista.
4. Note o **CI Unique ID** da aplicação a que pretende fornecer um link, por exemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. Em seguida, remova qualquer texto que seguem a aplicação GUID, neste caso **/2**. Isto deixa-lhe o identificador de aplicação.
6. Finalmente, para terminar a construção do link, precede-o com **Softwarecenter:SoftwareID=**. Utilizando o exemplo acima, o link final será lido: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Ao utilizar este link, os utilizadores finais podem abrir o Software Center diretamente para a aplicação que especificou.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para configuração manager computadores clientes windows

Agora pode implementar perfis de certificadoPFX importados para computadores clientes do Gestor de Configuração que executam o Windows 10.

### <a name="try-it-out"></a>Experimente

Utilize as instruções em [Como criar perfis de certificadoS PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md) para importar um perfil PFX, implementar o perfil e, em seguida, verificar se o certificado foi instalado para o utilizador-alvo.



## <a name="configure-azure-services-wizard"></a>Assistente de Serviços Configure Azure
A pré-visualização técnica 1703 introduz o assistente de **Serviços Configure Azure.** Este assistente proporciona uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os serviços de nuvem que utiliza com o Gestor de Configuração. Isto é feito utilizando uma **aplicação web Azure** para fornecer os detalhes de subscrição e configuração que você de outra forma insere cada vez que configura um novo componente de Gestor de Configuração ou serviço com o Azure.

Com pré-visualização técnica 1703, apenas a Windows Store for Business (WSfB) é configurada utilizando este assistente.  Outros serviços na nuvem são configurados utilizando os seus fluxos de trabalho separados.

- Utilize as informações neste tópico de pré-visualização para substituir os passos de configuração encontrados na secção [de sincronização](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) da Loja do Windows para o Negócio do Negócio do Atual [Recurso.](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Para mais informações sobre aplicações web, consulte autenticação e autorização no Serviço de [Aplicações Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), e na visão geral das [Aplicações Web.](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)

### <a name="prerequisites-and-planning"></a>Pré-requisitos e planeamento
Quando configurar uma ligação entre o Gestor de Configuração e a Windows Store for Business, deve fornecer uma pasta onde os conteúdos da aplicação sincronizados a partir da loja serão mantidos. Para garantir que esta pasta está segura e que o seu conteúdo pode ser implantado nos dispositivos, certifique-se de que as seguintes permissões estão em vigor:
- O computador no qual instala a função do sistema de ponto de ligação de serviço (o site de alto nível na hierarquia) deve ter lido e escrito permissões à pasta que especificou ao utilizar a conta **Computer$.**  

- O autor da aplicação deve ter lido permissões à pasta que especificou.  

- A conta **Computer$** de cada computador que acolhe uma instância do Fornecedor SMS deve poder utilizar a pasta especificada.

No Diretório Ativo do Azure, registe o Gestor de Configuração como uma aplicação web ou uma ferramenta de gestão de API web. Isto cria a identificação do cliente de que vai precisar mais tarde.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Utilize o assistente para configurar o serviço de nuvem WSfB

1. Na consola, vá ao **Administration**  >  **Overview**  >  **Cloud Services Management**  >  **Azure**  >  **Azure Azure Services,** e depois escolha **os Serviços Configure Azure** para iniciar o **Assistente de Serviços Azure.**

2. Na página **dos Serviços Azure,** selecione o serviço que pretende configurar e, em seguida, clique em **Next**. Com esta pré-visualização, apenas o WSfB pode ser configurado.

3. Na página **Geral,** forneça um nome amigável para o nome de **serviço Azure** e uma descrição opcional, e, em seguida, clique em **Next**.

4. Na página da **App,** especifique o seu ambiente Azure e clique em **Navegar** para abrir a janela da App do Servidor.

5. Na janela **'Aplicação servidora',** selecione a aplicação do servidor que pretende utilizar e, em seguida, clique em **OK**.
   As aplicações do servidor são as aplicações web Azure que contêm as configurações para a sua conta Azure, incluindo o seu ID de Inquilino, ID do Cliente e uma chave secreta para os clientes. Se não tiver uma aplicação de servidor disponível, utilize uma das seguintes aplicações:
   - **Criar**: Para criar uma nova aplicação de servidor, clique em **Criar**. Forneça um nome amigável para a app e o inquilino. Depois de iniciar sessão no Azure, o Gestor de Configuração cria a aplicação web em Azure para si, incluindo o ID do Cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode vê-los a partir do portal Azure.
   - **Importação**: Para utilizar uma aplicação web que já existe na sua subscrição Azure, clique **em Importar**. Forneça um nome amigável para a app e o inquilino, e depois especifique o ID do Inquilino, id do cliente e a chave secreta para a aplicação web Azure que pretende utilizar o Gestor de Configuração. Depois de **verificar** a informação, clique em **OK** para continuar.  </br></br>

6. Reveja a página **informação** e complete quaisquer passos e configurações adicionais conforme direcionado. Estas configurações são necessárias para utilizar o serviço com o Gestor de Configuração.
   Por exemplo, para configurar o WSfB:

   1. No Azure deve registar o Gestor de Configuração como aplicação web ou Web API e registar o ID do cliente. Especifica também uma chave de cliente para utilização pela ferramenta de gestão (que é O Gestor de Configuração).

   2.    Na consola WSfB deve configurar o ConfigurManager de Configuração como a ferramenta de gestão da loja, ativar suporte para aplicações licenciadas offline e, em seguida, comprar pelo menos uma aplicação.   </br>

   Clique em **Seguir** quando estiver pronto para continuar.

7. Na página configurações da **aplicação,** complete o catálogo de aplicações e as configurações de idiomas para este serviço e, em seguida, clique em **Next**.
8. Após o completo do assistente, a consola do Gestor de Configuração mostra que configuraste a **Windows Store para o Negócio** como tipo de serviço em **nuvem**.

Agora pode utilizar o restante conteúdo da [Filial Atual](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) para gerir aplicações do WSfB para sincronizar, criar e implementar e monitorizar o Windows Store para Aplicações Empresariais.

### <a name="modify-a-cloud-service-configuration"></a>Modificar uma configuração de serviço na nuvem
Pode ver e editar as propriedades de um serviço na nuvem para modificar a configuração.

Na consola vá ao **Administration**  >  **Overview**  >  **Cloud Services Management**  >  **Azure**  >  **Azure Azure Services,** e depois escolha **Os Serviços Configure Azure, selecione**um Serviço cloud e, em seguida, escolha **Propriedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
A Atualização de Criadores do Windows 10 introduz uma ferramenta de conversão simples que automatiza o processo de repartição do disco rígido para hardware ativado pela UEFI e integra a ferramenta de conversão no processo de atualização do Windows 7 para o Windows 10. Quando combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para a Atualização de Criadores do Windows 10. Para mais detalhes, consulte os passos da [sequência de tarefas para gerir o BIOS até à conversão UEFI](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

## <a name="collapsible-task-sequence-groups"></a>Grupos de sequência de tarefas desmontáveis
Esta versão introduz a capacidade de expandir e colapsar grupos de sequência de tarefas. Pode expandir ou colapsar grupos individuais ou expandir ou colapsar todos os grupos de uma só vez.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Definições do cliente para configurar O Windows Analytics para a prontidão de upgrade
A partir desta versão, pode utilizar as definições do cliente do dispositivo para simplificar a configuração dos dados de diagnóstico do Windows necessários para utilizar soluções do Windows Analytics, como a Atualização de Prontidão com O Gestor de Configuração. O Gestor de Configuração pode recuperar dados do Windows Analytics que podem fornecer informações valiosas sobre o estado atual do seu ambiente com base nos dados de diagnóstico do Windows relatados pelos seus computadores clientes. Os dados de diagnóstico do Windows são reportados pelos computadores clientes ao serviço de diagnóstico do Windows e, em seguida, os dados relevantes são posteriormente transferidos para soluções Windows Analytics que estão alojadas num dos espaços de trabalho oMS da sua organização. A atualização de prontidão é uma solução Windows Analytics que pode ajudá-lo a priorizar decisões sobre atualizações do Windows para os seus dispositivos geridos.

### <a name="prerequisites"></a>Pré-requisitos
- Deve ter configurado o seu site para utilizar o serviço de cloud de atualização de prontidão.

### <a name="configure-windows-analytics-client-settings"></a>Configure as definições do cliente do Windows Analytics
Para configurar o Windows Analytics, na consola do Gestor de Configuração vai para as Definições do Cliente **de Administração,**  >  **Client Settings**clique em duplo clique em **Criar Definições de Cliente de DispositivoPersonalizado** e, em seguida, verifique **o Windows Analytics**.  

Em seguida, configure o seguinte depois de navegar para o separador de definições **do Windows Analytics:**
- **ID comercial**  
A chave de identificação comercial mapeia informações de dispositivos que gere para o espaço de trabalho OMS que acolhe os dados do Windows Analytics da sua organização. Se já configurou uma chave de identificação comercial para utilização com a Atualização de Prontidão, utilize esse ID. Se ainda não tiver uma chave de identificação comercial, gere a sua chave de identificação comercial.

- Definir um **nível de dados de diagnóstico para dispositivos Windows 10**

- Opte **por optar pela recolha de dados comerciais nos dispositivos Windows 7, 8 e 8.1**   

- **Configure a recolha** de dados da Internet Explore Nos dispositivos que executam o Windows 8.1 ou anterior, a recolha de dados do Internet Explorer pode permitir que a Prontidão de Upgrade detete incompatibilidades de aplicações web que possam impedir uma atualização suave para o Windows 10. A recolha de dados do Internet Explorer pode ser ativada numa base de zona de internet.
