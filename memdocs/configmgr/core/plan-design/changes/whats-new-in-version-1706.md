---
title: Nova versão 1706
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1706 do Gestor de Configuração.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a8a4ce1c3d54311db18decc85f57d3e03298d339
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904683"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>O que&#39;novo na versão 1706 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1706 para o atual ramo do Gestor de Configuração está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1606, 1610 ou 1702.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de base do 'Gestor de Configuração'.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Instalação de atualizações nos sites](../../servers/manage/updates.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)  

As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1706 do Gestor de Configuração.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do local

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cliente Peer Cache para ficheiros de instalação expresso para Windows 10 e Office 365  
<!-- 1352486 -->
A partir desta versão, peer Cache suporta a distribuição de ficheiros de instalação expresso de conteúdo para o Windows 10 e de ficheiros de atualização para o Office 365. Não são necessárias configurações adicionais para suportar esta alteração.

### <a name="updates-for-the-data-warehouse"></a>Atualizações para o armazém de dados
<!-- 1277922 -->
O armazém de dados já não é uma funcionalidade de pré-lançamento. Também atualizámos os pré-requisitos para incluir suporte para a base de dados no SQL Server Sempre em grupos de disponibilidade e clusters failover. Para mais informações, consulte o ponto de [serviço do Data Warehouse](../../servers/manage/data-warehouse.md).

### <a name="accessibility-improvements"></a>Melhorias de acessibilidade
<!-- 1253000 -->
Adicionámos melhorias adicionais à acessibilidade para a consola Do Gestor de Configuração. Para mais detalhes, consulte [as funcionalidades de Acessibilidade.](../../understand/accessibility-features.md)

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Melhorias para o Servidor SQL sempre em grupos de disponibilidade
<!-- 1352094 -->
Com esta versão, pode agora utilizar réplicas de compromisso assíncronos nos grupos de disponibilidade do Servidor SQL Always On que utiliza com o Gestor de Configuração. Isto significa que pode adicionar réplicas adicionais aos seus grupos de disponibilidade para usar como backups off-site (remotos) e, em seguida, usá-las num cenário de recuperação de desastres.  
- O Gestor de Configuração suporta a utilização da réplica assíncrona para recuperar a sua réplica sincronizada. Consulte [as opções](../../servers/manage/recover-sites.md#site-database-recovery-options) de recuperação da base de dados do site no tópico de Backup e Recovery para obter informações sobre como o conseguir.
- Esta versão não suporta a falha na utilização da réplica de compromisso assíncrono como base de dados do site.
Para mais informações, consulte [Prepare-se para utilizar sempre em grupos de disponibilidade](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações
<!-- 1324589 -->
Começando com a versão 1706, os sites primários do Gestor de Configuração e os sites da administração central incluem a ferramenta de reset de reset do Gestor de Configuração, **CMUpdateReset.exe**. Utilize esta ferramenta com qualquer versão do ramo atual que permaneça no suporte, para corrigir problemas quando as atualizações na consola têm problemas em descarregar ou replicar. Para mais informações, consulte a [ferramenta de reset Do Update](../../servers/manage/update-reset-tool.md).

### <a name="high-dpi-console-support"></a>Suporte de consola DPI elevado  
<!-- 1353476 -->
Com esta versão, devem ser corrigidas questões com a forma como a consola do Gestor de Configuração se baseia e exibe diferentes partes do UI quando visualizadas em dispositivos DPI elevados (como um livro de Superfície).

### <a name="improved-boundary-groups-for-software-update-points"></a>Melhores grupos de fronteira para pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui melhorias na forma como os pontos de atualização de software funcionam com grupos de fronteira. O seguinte resume o novo comportamento de recuo:
- O fallback para pontos de atualização de software agora usa um tempo configurável para o recuo para grupos de fronteira vizinhos.
- Independentemente da configuração de recuo, um cliente tenta alcançar o último ponto de atualização de software que utilizou durante 120 minutos. Depois de não ter chegado ao servidor durante 120 minutos, o cliente verifica então o seu conjunto de pontos de atualização de software disponíveis, para que possa encontrar um novo.
- Depois de não ter atingido o seu servidor original durante duas horas, o cliente muda para um ciclo mais curto para contactar um novo ponto de atualização de software. Isto significa que se um cliente não se ligar a um novo servidor, ele rapidamente seleciona o próximo servidor a partir do seu conjunto de servidores disponíveis e tenta contactar esse.

Para mais informações, consulte pontos de [atualização](../../servers/deploy/configure/boundary-groups.md#software-update-points) de software no tópico dos Grupos de Fronteira para a Divisão Atual.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integração da AD Azure com Gestor de Configuração
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Com este lançamento, melhorámos a integração do Gestor de Configuração e do Diretório Ativo Azure (Azure AD).  Estas melhorias agilizam a forma como configura os serviços Azure que utiliza com o Gestor de Configuração, e ajudam-no a gerir clientes e utilizadores que autenticam aad.

A melhor integração torna possível o seguinte:  
- Assistente de Serviços Azure – Este Assistente proporciona uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os seguintes serviços Azure que utiliza com o Gestor de Configuração.
  - **Gestão de Nuvem** Permitir que os clientes autentiem utilizando o Azure Ative Directory (Azure AD). Também pode configurar a Descoberta do Utilizador de Anúncios Azure.
  - **Conector de análise de log** Ligue-se ao Azure Log Analytics e sincronizar dados de recolha.
  - **Atualização da Prontidão** Ligue-se à Prontidão de Upgrade e consulte os dados de atualização do cliente de compatibilidade.
  - **Loja windows para negócios** Conecte-se à loja on-line para Windows Store for Business e obtenha aplicações para a sua organização que pode implementar com o Gestor de Configuração.


  Isto é feito utilizando uma aplicação web do [servidor Azure](/azure/app-service/app-service-authentication-overview) para fornecer os detalhes de subscrição e configuração que de outra forma introduz sempre que configura rumum novo componente ou serviço de Gestor de Configuração com o Azure. Para mais informações, consulte [O Assistente de Serviços Azure.](../../servers/deploy/configure/azure-services-wizard.md)

- Utilize a AD Azure para autenticar clientes na internet para aceder aos seus sites de Gestor de Configuração. A Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação do cliente. Isto requer a função do sistema de gateway de gestão da nuvem. Para mais informações, consulte [Instalar e atribuir clientes do Gestor de Configuração da internet utilizando a AD Azure para autenticação.](../../clients/deploy/deploy-clients-cmg-azure.md)

- Instale e gerencie o cliente do Gestor de Configuração em computadores localizados na internet. Isto requer a utilização da função do sistema de sistema de gateway de gestão da nuvem. Para mais informações, consulte [Instalar e atribuir clientes do Gestor de Configuração da internet utilizando a AD Azure para autenticação.](../../clients/deploy/deploy-clients-cmg-azure.md)

- Configure Descoberta de Utilizador aD Azure.  Utilize o Assistente de Serviços Azure para configurar este novo método de descoberta. Este novo método consulta o seu AD Azure para os dados do utilizador que pode então utilizar juntamente com dados tradicionais de descoberta.  A sincronização completa e delta são apoiadas.  Para mais informações consulte a Descoberta do Utilizador da [AD Azure](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="peer-cache-improvements"></a>Melhorias na cache dos pares
<!-- 1252345 -->
A cache peer já não utiliza a Conta de Acesso à Rede para autenticar pedidos de descarregamento de pares. Há uma ressalva em que a conta permanece exigida pelos clientes. Isto continua a ser um requisito para os clientes que iniciam o WinPE e depois acedem a conteúdos a partir de uma fonte de cache de pares. Para mais informações, consulte [os requisitos e considerações para](../hierarchy/client-peer-cache.md#requirements)a cache dos pares .


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Novas configurações de configuração para dispositivos Windows 10 que não são geridas com o cliente do Gestor de Configuração
<!-- 1354715 -->
Nesta versão, adicionámos novas definições de itens de configuração para dispositivos Windows 10 que estão matriculados com o Intune, ou geridos nas instalações pelo Gestor de Configuração. As definições são:

- **Palavra-passe**
  - Encriptação do dispositivo
- **Dispositivo**
  - Modificação das definições da região (apenas no ambiente de trabalho)
  - Modificação das definições de potência e sono
  - Modificação de definições de idiomas
  - Modificação do tempo do sistema
  - Modificação do nome do dispositivo
- **Arquivo**
  - Aplicativos de atualização automática a partir da loja
  - Utilize apenas loja privada
  - Lançamento de app originada na loja
- **Microsoft Edge**
  - Bloqueie o acesso a cerca de:bandeiras
  - Substituição rápida do SmartScreen
  - Substituição de aviso do SmartScreen para ficheiros
  - Endereço IP local webRTC
  - Motor de busca padrão
  - OpenSearch XML URL
  - Homepages (apenas desktop)

Para mais detalhes de todas as definições do Windows 10, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Gestor](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)de Configuração .

### <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivos

* **Tipo de palavra-passe necessária**. Especifique se o utilizador deve criar uma palavra-passe alfanumérica ou uma palavra-passe numérica. Para senhas alfanuméricas, também especifica o número mínimo de conjuntos de caracteres que a palavra-passe deve ter. Os quatro conjuntos de caracteres são: minúsculas, letras maiúsculas, símbolos e números.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **Bloqueie a depuração USB no dispositivo**. Não é necessário configurar estas definições, uma vez que a depuração USB já está desativada em dispositivos Android for Work.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Bloqueie aplicações de fontes desconhecidas.** Exige que os dispositivos impeçam a instalação de aplicações de fontes desconhecidas. Não é preciso configurar esta definição, uma vez que os dispositivos Android for Work restringem sempre a instalação de fontes desconhecidas.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Requerer uma varredura de ameaças em apps**. Esta definição especifica que a funcionalidade de verificação de aplicações está ativada no dispositivo.

  **Suportado no:**
  * Android 4.2 a 4.4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Gestão de Aplicações

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Executar scripts PowerShell da consola De Configuração Manager
<!-- 1236459 -->

No 'Gestor de Configuração', pode implementar scripts para dispositivos clientes utilizando pacotes e programas. Neste lançamento, adicionámos uma nova funcionalidade que permite tomar as seguintes ações:

- Importar scripts PowerShell para gerente de configuração
- Editar os scripts da consola 'Gestor de Configuração' (apenas para scripts não assinados)
- Marque scripts como Aprovados ou Negados, para melhorar a segurança
- Execute scripts em coleções de computadores clientes windows e computadores geridos no local. Não se implantam scripts, em vez disso, são executados em quase tempo real em dispositivos de cliente.
- Examine os resultados devolvidos pelo script na consola 'Gestor de Configuração'.

Para mais informações, consulte [Criar e executar scripts PowerShell a partir da consola Do Gestor de Configuração](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis    
<!--1324760-->
A partir desta versão, pode utilizar três novas definições de política de gestão de aplicações móveis (MAM):

- Captura de ecrã de **blocos (apenas dispositivos Android):** Especifica que as capacidades de captura do ecrã do dispositivo estão bloqueadas ao utilizar esta aplicação.


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de Botas Seguras
O inventário de hardware agora recolhe informações sobre se o Secure Boot está ativado nos clientes. Esta informação é armazenada na classe **SMS_Firmware** (introduzida na versão 1702) e ativada no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../../clients/manage/inventory/configure-hardware-inventory.md)de hardware .

### <a name="collapsible-task-sequence-groups"></a>Grupos de sequência de tarefas desmontáveis
Esta versão introduz a capacidade de expandir e colapsar grupos de sequência de tarefas. Pode expandir ou colapsar grupos individuais ou expandir ou colapsar todos os grupos de uma só vez.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Recarregar imagens de boot com a versão atual do Windows PE
Quando executa Pontos de Distribuição de **Atualização** numa imagem de arranque selecionada, pode agora optar por recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. Para mais informações, consulte pontos de [distribuição de Atualização com a imagem do arranque](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Atualizações de software

### <a name="improvements-to-express-update-download-time"></a>Melhorias no tempo de download do Express Update
Neste lançamento, melhorámos significativamente o tempo de download para Express Updates. Para mais informações, consulte os ficheiros de [instalação do Manage Express para atualizações do Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Gerir as atualizações do controlador do Microsoft Surface
<!-- 1098490 -->
Agora pode utilizar o 'Gestor de Configuração' para gerir as atualizações do controlador do Microsoft Surface.    


#### <a name="prerequisites"></a>Pré-requisitos
- Todos os pontos de atualização de software devem executar o Windows Server 2016.    
- Esta é uma funcionalidade de pré-lançamento que deve ligar para que esteja disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Para gerir as atualizações do condutor do Surface

1. Ativar a sincronização para os controladores Microsoft Surface. Utilize o procedimento na [classificação e produtos da Configuração](../../../sum/get-started/configure-classifications-and-products.md) e selecione os **controladores Microsoft Surface e as atualizações de firmware** no separador **Classificações** para ativar os controladores de Superfície.
2. [Sincronizar os controladores Microsoft Surface](../../../sum/get-started/synchronize-software-updates.md).
3. [Implementar controladores sincronizados do Microsoft Surface](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configure atualização do Windows para políticas de adiamento de negócios
<!-- 1290890 -->
Agora pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento no novo nó **de Atualização do Windows para Políticas Empresariais** no âmbito da Manutenção da Biblioteca de **Software**  >  **Windows 10**.

Para mais detalhes, consulte [integração com a Atualização do Windows para Negócios no Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Melhores notificações dos utilizadores para as atualizações do Office 365
Foram feitas melhorias para alavancar a experiência do utilizador Click-to-Run do Office quando um cliente instala uma atualização do Office 365. Isto inclui notificações pop-up e in-app, e uma experiência de contagem regressiva. Para mais informações, consulte [O comportamento do Restart e notificações de clientes para atualizações do Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Relatórios

### <a name="use-windows-analytics-with-configuration-manager"></a>Utilize o Windows Analytics com o Gestor de Configuração
<!-- 1318608 -->
O Windows Analytics é um conjunto de soluções que lhe permitem formar informações sobre o estado atual do seu ambiente. Os dispositivos do seu ambiente reportam dados de telemetria do Windows. Os dados podem ser acedidos através do portal Azure. No caso de Preparação de Atualização, os dados estão diretamente disponíveis no nó de monitorização da consola 'Gestor de Configuração'.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="updates-to-android-for-work-sharing-configuration"></a>Atualizações para Android para configuração de partilha de trabalho
<!-- 1338403 -->
Com esta versão, foram atualizados os valores para a partilha de dados entre o trabalho e a definição de **perfil pessoal** no grupo de definição de Perfil de **Trabalho.** Também adicionámos uma configuração personalizada para bloquear a pasta de cópia entre o trabalho e os perfis pessoais.


### <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição android e iOS
<!-- 1290826 -->
Com esta versão, pode agora especificar que os utilizadores não podem inscrever dispositivos pessoais Android ou iOS. As novas definições de restrição de dispositivos permitem limitar a inscrição do dispositivo Android a dispositivos pré-declarados. Para dispositivos iOS, pode bloquear a inscrição de todos os dispositivos, exceto os inscritos no Programa de Inscrição de Dispositivos da Apple, no Configurator Apple ou na conta de gestor de inscrição do dispositivo Intune.

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclua confiança para ficheiros e pastas específicos numa política de Guarda de Dispositivos
<!--1324676-->
Neste comunicado, adicionámos mais capacidades à gestão da política da Guarda de Dispositivos.

Agora pode adicionar opcionalmente confiança para ficheiros específicos para pastas numa política de Guarda de Dispositivos. Isto permite-lhe:

- Superar problemas com comportamentos instaladores geridos
- Aplicativos de linha de negócio sintetizados que não podem ser implementados com O Gestor de Configuração
- Confie em aplicativos que estão incluídos numa imagem de implementação do sistema operativo

Para mais detalhes, consulte a gestão da Guarda de [Dispositivos com o Gestor de Configuração](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
