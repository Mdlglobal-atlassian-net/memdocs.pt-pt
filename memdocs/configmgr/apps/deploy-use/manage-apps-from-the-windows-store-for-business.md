---
title: Aplicações da Loja Microsoft
titleSuffix: Configuration Manager
description: Gerir e implementar aplicações a partir da Microsoft Store para Negócios e Educação com O Gestor de Configuração.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d6a61324f8c777ba5ed09dd26816152d6f17af9
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643209"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Gerir aplicativos a partir da Microsoft Store para negócios e educação com gestor de configuração

A [Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/) é onde encontra e adquire aplicativos Windows para a sua organização. Quando liga a loja ao Gestor de Configuração, sincroniza a lista de aplicações que adquiriu. Veja estas aplicações na consola Do Gestor de Configuração e implemente-as como implementar qualquer outra aplicação.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a>Aplicativos online e offline

A Microsoft Store for Business and Education suporta dois tipos de aplicações:

- **Online**: Este tipo de licença requer que os utilizadores e dispositivos se conectem à loja para obter uma app e a sua licença. Os dispositivos Windows 10 devem ser unidos pelo Azure Ative Directory (Azure AD) ou híbridos Azure AD.  

- **Offline**: Este tipo permite-lhe cache apps e licenças para implementar diretamente dentro da sua rede no local. Os dispositivos não precisam de se ligar à loja ou ter uma ligação à internet.

Para mais informações, consulte a visão geral da [Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Resumo das capacidades

O Gestor de Configuração suporta a gestão de aplicações da Microsoft Store para empresas e educação em ambos os dispositivos do Windows 10 com o cliente Do Gestor de Configuração, e também dispositivos Windows 10 matriculados no Microsoft Intune. O Gestor de Configuração oferece as seguintes capacidades para aplicações online e offline:

|Capacidade|Aplicativos offline|Aplicativos online|
|------------|------------|------------|
|Sincronizar os dados da aplicação para o Gestor de Configuração<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicações do Gestor de Configuração a partir de aplicações de loja|Sim|Sim|
|Suporte para aplicações gratuitas da loja|Sim|Sim|
|Suporte para aplicações pagas da loja|Não|Nota sim<sup>[1](#bkmk_note1)</sup>|
|Suporte necessário implementações para recolhas de utilizadores ou dispositivos|Sim|Sim|
|Suporte implementações disponíveis para recolhas de utilizadores ou dispositivos|Sim|Sim|
|Apoiar aplicativos de linha de negócio saem da loja|Sim|Sim|
|Disponibilização de uma aplicação de loja para todos os utilizadores num dispositivo<sup>[Note 2](#bkmk_note2)</sup><!--1358310-->|Sim|Sim|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a>Nota 1: Requisito de versão de apps licenciadas online

Para implementar aplicações licenciadas online para dispositivos Windows 10 com o cliente Do Gestor de Configuração, devem estar a executar o Windows 10, versão 1703 ou mais tarde.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a>Nota 2: Versão mínima do Gestor de Configuração

Começando na versão 1806. Para mais informações, consulte [Create Windows aplicações](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Implementação de aplicações online utilizando a Microsoft Store para negócios e educação para dispositivos que executam o cliente do Gestor de Configuração

Antes de implementar aplicações da Microsoft Store para empresas e educação para dispositivos que executem todo o cliente do Gestor de Configuração, considere os seguintes pontos:

- Para uma funcionalidade completa, os dispositivos devem estar a executar o Windows 10, versão 1703 ou mais tarde.  

- Registe-se ou junte dispositivos ao mesmo inquilino da AD Azure onde registou a Microsoft Store for Business and Education como uma ferramenta de gestão.  

- Quando a conta do Administrador local entra no dispositivo, não pode aceder às aplicações da Microsoft Store for Business and Education.  

- Os dispositivos devem ter uma ligação à Internet ao vivo à Microsoft Store para negócios e educação. Para obter mais informações, incluindo a configuração de procuração, consulte [os pré-requisitos](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Notas para dispositivos que executam versões anteriores do Windows 10

Nos dispositivos com o cliente do Gestor de Configuração e executando a versão 1607 do Windows 1607 ou anterior, aplica-se a seguinte funcionalidade:  

Quando impor a instalação da aplicação no dispositivo por um dos seguintes métodos:  

- O utilizador instala a aplicação  

- A implementação atinge o seu prazo de instalação

- Reavaliação pós-instalação para implementações necessárias  

Em seguida, ocorrem os seguintes comportamentos:  

- O cliente do Gestor de Configuração "aplica" através do lançamento da aplicação Microsoft Store  

- O utilizador deve concluir a instalação a partir da loja  

- Na consola Do Gestor de Configuração, o status de implementação da aplicação reporta falha com o seguinte erro: "A aplicação da Microsoft Store foi aberta no PC cliente e está à espera que o utilizador complete a instalação."  

No próximo ciclo de avaliação de candidaturas:  

- Se o utilizador instalou a aplicação a partir da loja, a aplicação reporta o estado **Sucesso**  

- Se o utilizador não tentou instalar a aplicação a partir da loja:  

  - Para implementações necessárias, o cliente do Gestor de Configuração tenta lançar novamente a app da loja  

  - O Gestor de Configuração não reforça as implementações disponíveis

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Dispositivos que executam versões anteriores do Windows 10

- Não pode implementar aplicações de linha de negócio sada da Microsoft Store para negócios e educação

- Quando implementa aplicações pagas a partir da loja, os utilizadores devem iniciar sessão na loja e adquirir a própria app  

- Se implementar uma política de grupo para desativar o acesso à versão de consumo da Microsoft Store, as implementações da Microsoft Store for Business and Education não funcionam. Este comportamento ocorre mesmo que ative a Microsoft Store para negócios e educação.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a>Configurar a sincronização

Ao sincronizar a lista de aplicações da Microsoft Store para empresas e de educação que a sua organização adquiriu, vê estas aplicações na consola Do Gestor de Configuração.

Ligue o site do Gestor de Configuração ao Azure AD e à Microsoft Store para negócios e educação. Para mais informações e detalhes deste processo, consulte os [serviços da Configure Azure.](../../core/servers/deploy/configure/azure-services-wizard.md) Criar uma ligação à Microsoft Store para o serviço **De Negócios.**

Certifique-se de que o ponto de ligação de serviço e os dispositivos direcionados podem aceder ao serviço de cloud. Para mais informações, consulte [os pré-requisitos para a Microsoft Store para negócios e educação - configuração proxy](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a>Informação e configuração suplementares

Na página da **App** do Assistente de Serviços Azure, primeiro configurar o **ambiente Azure** e a **aplicação Web.** Em seguida, leia a secção **Mais Informação** na parte inferior da página. Estas informações incluem as seguintes ações adicionais no portal Microsoft Store for Business and Education:  

- Configure o Gestor de Configuração como a ferramenta de gestão da loja. Para mais informações, consulte o [fornecedor de gestão Configure.](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business)  

- Ativar suporte para aplicações licenciadas offline. Para mais informações, consulte [Distribute aplicativos offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Adquira pelo menos uma aplicação. Para mais informações, consulte [Encontrar e adquirir apps.](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview)  

Na página **de Configurações** do Assistente de Serviços Azure, especifique as seguintes informações:  

- Caminho para o armazenamento de conteúdo de **aplicações da Microsoft Store for Business**: Especifique um caminho de rede partilhado, incluindo uma pasta. Por exemplo, `\\server\share\folder`. Quando o servidor do site sincroniza com a loja, ele caches conteúdo neste local. Quando cria uma aplicação no 'Gestor de Configuração', o servidor do site copia o conteúdo da aplicação desta cache local para a biblioteca de conteúdos do site.  

- **Idiomas selecionados**: Selecione os idiomas para sincronizar a partir da loja e exibir para os utilizadores no Centro de Software. Por exemplo, se o utilizador configura o Windows para alemão, então o Software Center mostra cordas alemãs para a aplicação da loja. Este comportamento requer que essa linguagem seja sincronizada e exista para a aplicação específica.

- **Idioma predefinido**: Se o idioma do utilizador não estiver disponível, selecione um idioma predefinido para utilizar.  

> [!NOTE]
> O Gestor de Configuração não sincroniza o ícone da aplicação a partir da loja. Se precisar de um ícone para exibir para esta aplicação no Software Center, adicione-a manualmente nas propriedades da aplicação. Para mais informações, consulte [Manualmente a informação sobre a aplicação.](create-applications.md#bkmk_manual-app)<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a>Criar e implementar a app

Após a sincronização, crie e implemente a Microsoft Store para aplicações de Negócios e Educação semelhantes a qualquer outra aplicação de Configuração Manager.

1. No espaço de trabalho da Biblioteca de **Software** da consola Do Gestor de Configuração, expanda a Gestão de **Aplicações**e, em seguida, selecione o nó de Informações de **Licença para Apps de Loja.**  

2. Escolha a aplicação que pretende implementar e, em seguida, selecione **Criar aplicação** na fita.  

O site cria uma aplicação De Configuração Manager contendo a aplicação Microsoft Store for Business and Education.

Em seguida, implemente e monitorize esta aplicação como faria qualquer outra aplicação do Gestor de Configuração. Para obter mais informações, veja os artigos seguintes:  

- [Implementar aplicações](deploy-applications.md)
- [Monitorizar aplicações a partir da consola](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Passos seguintes

No espaço de trabalho da Biblioteca de **Software,** expandir a Gestão de **Aplicações,** em seguida, selecione a Informação de Licença para O Nó de Apps de **Loja.**

Para cada aplicação de loja que gere, consulte as seguintes informações sobre a aplicação:

- Nome da aplicação
- Plataforma de aplicações
- O número de licenças para a app que possui
- O número de licenças disponíveis

Depois de implementar aplicações online, quaisquer atualizações para essa aplicação vêm diretamente da Microsoft Store. Além disso, o Gestor de Configuração não verifica a conformidade da versão das aplicações online, apenas que o Windows reporta a aplicação como instalada.  

Ao implementar aplicações offline para dispositivos Windows 10 com o cliente Do Gestor de Configuração, não permite que os utilizadores atualizem aplicações externas para implementações do Gestor de Configuração. O controlo de atualizações para aplicações offline é especialmente importante em ambientes multiutilizadores, como salas de aula. Uma opção para desativar a Microsoft Store é utilizando a política do [grupo.](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy)

Depois de o administrador da Microsoft Store for Business and Education adquirir uma aplicação offline, não publique a app aos utilizadores através da loja. Esta configuração garante que os utilizadores não podem instalar ou atualizar online. Os utilizadores só recebem atualizações de aplicações offline através do 'Gestor de Configuração'.

## <a name="see-also"></a>Consulte também

[Troubleshoot a Microsoft Store para integração de negócios e educação com Gestor de Configuração](troubleshoot-microsoft-store-for-business-integration.md)
