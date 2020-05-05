---
title: Alterações a partir da versão 2012
titleSuffix: Configuration Manager
description: Identifique as alterações e novas capacidades no Configuration Manger versus System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720829"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>O que mudou do System Center 2012 Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

O atual ramo do Gestor de Configuração introduz mudanças importantes do System Center 2012 Configuration Manager. Este artigo identifica alterações significativas e novas capacidades encontradas na versão original 1511 do ramo atual do Gestor de Configuração. Para saber sobre as alterações introduzidas em atualizações recentes para O Gestor de Configuração, consulte [as novidades nas versões incrementais do Gestor de Configuração.](whats-new-incremental-versions.md)

> [!NOTE]
> A partir da versão 1910, o Gestor de Configuração faz agora parte do Microsoft Endpoint Manager. Para mais informações, consulte [o Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

O lançamento de dezembro de 2015 (versão 1511) do Configuration Manager foi o lançamento inicial do atual produto Do Gestor de Configuração da Microsoft. É tipicamente referido como configuração gerente atual filial. *O ramo atual* indica que esta versão suporta atualizações incrementais do produto. Também fornece uma forma de distinguir entre este lançamento e os lançamentos anteriores do Gestor de Configuração.  

Sucursal atual do Gestor de Configuração:  

- Não utiliza um ano ou identificador de produto no nome do produto, ao contrário de versões anteriores como O Gestor de Configuração 2007 ou O Gestor de Configuração do System Center 2012.  

- Suporta atualizações incrementais e in-product, também chamadas versões de atualização. O lançamento inicial foi a versão 1511. Versões posteriores são lançadas várias vezes por ano como atualizações na consola, como a versão 1910.  

- É instalado com uma versão de base. Embora 1511 tenha sido a versão original da linha de base, as novas versões de base também são lançadas de vez em quando, como em 2002. As versões de base podem ser usadas para instalar um novo site e hierarquia do Gestor de Configuração, ou para atualizar a partir de uma versão suportada do System Center 2012 Configuration Manager.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a>Atualizações na consola

O Gestor de Configuração utiliza um método de serviço na consola chamado **Updates and Servicing** que facilita a localização e instalação de atualizações recomendadas.  

Algumas versões só estão disponíveis como atualizações para sites existentes a partir da consola 'Gestor de Configuração'. Não é possível utilizar estas atualizações para instalar um novo site do Gestor de Configuração. Por exemplo, a atualização de 1910 só está disponível a partir da consola 'Gestor de Configuração'. É usado para atualizar um site que já executa uma versão suportada do Gestor de Configuração.

Periodicamente, uma versão de atualização também é lançada como uma nova versão *de base.* Por exemplo, a versão atualizada de 2002 também é uma linha de base. Utilize uma versão de base para instalar um novo site ou hierarquia. Não comece com uma versão de base mais antiga como 1802, e atualize o seu caminho para a versão mais atual. Use sempre a última linha de base.

Para obter mais informações, veja os artigos seguintes:

- [Atualizações para o Configuration Manager](../../servers/manage/updates.md)
- [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>Ponto de ligação de serviço  

O ramo atual do Gestor de Configuração inclui uma nova função do sistema de site, o ponto de ligação ao **serviço:**  

- Um ponto de contacto para muitas funcionalidades ativadas pela nuvem

- Descarrega atualizações para o seu site

- Upload de diagnósticos e dados de utilização sobre o seu site para a nuvem da Microsoft

Esta função do sistema de site suporta modos de funcionamento online e offline. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a>Diagnósticos e dados de utilização

O Gestor de Configuração recolhe dados de diagnóstico e utilização sobre os seus sites e infraestruturas. Estas informações são compiladas e submetidas ao serviço de nuvem da Microsoft pelo ponto de ligação ao serviço. O Gestor de Configuração requer estes dados para descarregar atualizações aplicáveis ao seu ambiente. Quando configurar o ponto de ligação ao serviço, pode especificar tanto o nível de dados que recolhe, como se automaticamente (online) ou manualmente (offline) submete os dados.

Para mais informações, consulte [Diagnósticos e dados de utilização](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> Funcionalidades preteridas  

Algumas funcionalidades, como os computadores baseados em Suporte Nativo para tecnologia de [gestão ativa da Intel (AMT),](#bkmk_AMT) são removidas da consola Do Gestor de Configuração. Outras funcionalidades, como a Network Access Protection, são totalmente removidas. Além disso, alguns produtos mais antigos da Microsoft, como o Windows Vista, Windows Server 2008 e SQL Server 2008, já não são suportados.  

Para obter uma lista de funcionalidades depreciadas, consulte [itens removidos e depreciados](deprecated/removed-and-deprecated.md).  

Para mais detalhes sobre produtos suportados, sistemas operativos e configurações, consulte [configurações suportadas](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Suporte para Active Management Technology (AMT) da Intel  

O ramo atual do Gestor de Configuração remove o suporte nativo para computadores baseados em AMT a partir da consola 'Gestor de Configuração'. Os computadores baseados em AMT permanecem totalmente geridos quando utiliza o [Add-on Intel SCS para](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)o Microsoft Configuration Manager . O addon fornece-lhe acesso às mais recentes capacidades de gestão da AMT, ao mesmo tempo que elimina as limitações introduzidas até que o Gestor de Configuração possa incorporar essas alterações.  

A remoção de AMT integrado para Gerente de Configuração inclui gestão fora da banda. O papel do sistema de site de pontos de gestão fora da banda já não está disponível.  

> [!Note]
> Esta alteração não afeta a gestão fora da banda no System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Alterações na funcionalidade

As secções seguintes resumem algumas das mudanças significativas nas áreas de funcionalidade entre o System Center 2012 R2 Configuration Manager e a versão 1511 versão da secção atual do Gestor de Configuração. Para obter mais informações sobre as mudanças mais recentes na funcionalidade, consulte [o que há de novo em versões incrementais.](whats-new-incremental-versions.md)

### <a name="client-deployment"></a>Implementação de clientes  

O Gestor de Configuração introduz uma nova funcionalidade para testar novas versões do cliente do Gestor de Configuração antes de atualizar o resto do site com o novo software. Pode configurar uma coleção de pré-produção para pilotar um novo cliente. Uma vez satisfeito com o novo software de cliente em pré-produção, pode promover o cliente a atualizar automaticamente o resto do site com a nova versão.  

Para obter mais informações sobre como testar os clientes, consulte como testar as atualizações dos [clientes numa coleção pré-produção.](../../clients/manage/upgrade/test-client-upgrades.md)  

### <a name="os-deployment"></a>Implementação de SO  

Esteja atento às seguintes alterações à implementação do OS:

- No Assistente de Sequência de Tarefas Create, existe um novo tipo de sequência de tarefas: **Atualize um sistema operativo a partir do pacote de atualização**. Cria os passos para atualizar computadores do Windows 7 ou Windows 8.1 para o Windows 10. Para mais informações, consulte [o Upgrade Windows para a versão mais recente.](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  

- A cache de pares do Windows PE já está disponível quando implementa sistemas operativos. Os computadores que executam uma sequência de tarefas para implementar um SISTEMA podem utilizar a cache de pares do Windows PE para obter conteúdo a partir de uma fonte de cache de pares, em vez de descarregar conteúdo a partir de um ponto de distribuição. Este comportamento ajuda a minimizar o tráfego de WAN em cenários de sucursais onde não há ponto de distribuição local. Para mais informações, consulte Prepare a [cache dos pares do Windows PE para reduzir o tráfego de WAN](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Agora pode ver o estado do Windows como um serviço no seu ambiente. Também pode criar planos de manutenção para formar anéis de implementação e certificar-se de que os computadores de ramificação atuais do Windows 10 são mantidos atualizados quando forem lançadas novas construções. Além disso, pode ver alertas quando os clientes do Windows 10 estão perto do fim do suporte para a sua construção. Para mais informações, consulte [Gerir o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Gestão de aplicações  

Esteja atento às seguintes alterações à gestão da aplicação:

- O Gestor de Configuração permite-lhe implementar aplicações universal windows platform (UWP) para dispositivos que executam o Windows 10 e posteriormente. Para mais informações, consulte [Criar aplicações windows](../../../apps/get-started/creating-windows-applications.md).  

- O Centro de Software tem um aspeto novo e moderno. As aplicações disponíveis pelo utilizador que anteriormente só apareceram no catálogo de aplicações aparecem agora no Software Center sob o separador Aplicações. Este comportamento torna estas implementações mais detetáveis, e torna desnecessário que os utilizadores se refiram ao catálogo de aplicações separado. Além disso, um navegador ativado por Silverlight já não é necessário. Para mais informações, consulte Plan para e configure a gestão de [aplicações.](../../../apps/plan-design/plan-for-and-configure-application-management.md)  

- O novo Windows Installer através do tipo de aplicação MDM permite criar e implementar aplicações baseadas no Windows Installer em PCs inscritos que estejam a executar o Windows 10. Para mais informações, consulte [Criar aplicações windows](../../../apps/get-started/creating-windows-applications.md).  

- No 'Configuração Manager 2012', para especificar um link para uma aplicação na Windows Store, pode especificar o link diretamente, ou navegar para um computador remoto que tenha a aplicação instalada. No ramo atual do Gestor de Configuração, ainda pode introduzir o link diretamente, mas agora, em vez de navegar para um computador de referência, pode navegar na loja para a app diretamente a partir da consola 'Gestor de Configuração'.  

### <a name="software-updates"></a>Atualizações de software  

Esteja ciente das seguintes alterações às atualizações de software:

- O Gestor de Configuração pode agora detetar a diferença entre os métodos de gestão de atualizações de software para computadores. Especificamente, pode diferenciar entre um computador Windows 10 que se conecta ao Windows Update for Business (WUfB) e um computador ligado ao WSUS. O atributo **UseWUServer** é novo e especifica se o computador é gerido com WUfB. Pode utilizar esta definição numa coleção para remover estes computadores da gestão de atualizações de software. Para obter mais informações, veja [Integration with Windows Update for Business in Windows 10 (Integração com o Windows Update for Business no Windows 10)](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- Agora pode agendar e executar a tarefa de limpeza WSUS a partir da consola Do Gestor de Configuração. Nas propriedades do Componente de Ponto de Atualização de **Software,** quando se leciona para executar a tarefa de limpeza WSUS, executa nas próximas atualizações de software a sincronização. As atualizações de software expiradas estão definidas para um estado de recusa no servidor WSUS, e o Windows Update Agent em computadores já não verifica estas atualizações de software. Para obter mais informações, veja [Agendar e executar a tarefa de limpeza do WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Definições de compatibilidade  

Esteja atento às seguintes alterações às definições de conformidade:

- O Gestor de Configuração melhora o fluxo de trabalho para a criação de itens de configuração. Agora, quando cria um item de configuração e seleciona as plataformas suportadas, apenas estão disponíveis as definições relevantes para essa plataforma. Ver [Começar com as definições de conformidade](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- O assistente de **configuração Create Configuração** agora facilita a escolha do tipo de item de configuração que pretende criar. Além disso, estão disponíveis itens de configuração novos e atualizados para:  

    - Dispositivos do Windows 10 geridos com o cliente do Gestor de Configuração  

    - Dispositivos Mac OS X geridos com o cliente do Gestor de Configuração  

    - Computadores de desktop e servidor do Windows geridos com o cliente do Gestor de Configuração  

    - Dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor de Configuração  

    Para mais informações, consulte [Como criar itens de configuração](../../../compliance/deploy-use/create-configuration-items.md).  

- Suporte para gestão de configurações em computadores Mac OS X que são geridos sem o cliente Do Gestor de Configuração.

### <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local  

Agora pode gerir dispositivos móveis utilizando a infraestrutura do Gestor de Configuração no local. Todos os dados de dispositivos e gestão são tratados no local, e não fazem parte do Microsoft Intune ou de outros serviços na nuvem. Este tipo de gestão de dispositivos não requer software cliente. O Gestor de Configuração gere dispositivos com funcionalidade incorporada no sistema operativo OPERATIVO do dispositivo.  

Para mais informações, consulte [Gerir dispositivos móveis com infraestrutura no local.](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)

## <a name="next-steps"></a>Passos seguintes

[O que há de novo em versões incrementais](whats-new-incremental-versions.md)
