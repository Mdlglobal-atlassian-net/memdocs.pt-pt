---
title: Definições da política de grupo
titleSuffix: Configuration Manager
description: Compreender as definições de política locais e de grupo no Windows utilizadas pelo Gestor de Configuração e pelo Desktop Analytics
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8251e21c7eccb87b764af75e883018bdc894ca37
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268679"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Definições de política de grupo para Desktop Analytics

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo detalha as definições de política locais e de grupo no Windows que o Gestor de Configuração e o Desktop Analytics utilizam.

Quando o Gestor de Configuração inscreve os dispositivos no Desktop Analytics, define as políticas do Windows para configurar o dispositivo. Na maioria das circunstâncias, utilize apenas o Configuro Diretor de Configuração para configurar estas definições.

## <a name="windows-settings"></a>Definições do Windows

O Gestor de Configuração define as políticas do Windows numa ou em ambas as seguintes teclas de registo:

- Objeto de política de grupo **(GPO):**`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preferência política **local:**`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Política | Caminho | Aplica-se a | Valor |
|--------|------|------------|-------|
| **Comercialid** | Localização | Todas as versões do Windows | Para que um dispositivo apareça no Desktop Analytics, configure-o com o ID Comercial da sua organização. |
| **Permitir Telemetria**  | GPO | Windows 10 | Definido `1` para **Básico,** `2` para Dados de Diagnóstico **Melhorados,** ou para dados de `3` diagnóstico **completos.** Desktop Analytics requer pelo menos dados básicos de diagnóstico. A Microsoft recomenda que utilize o nível Enhanced (Limited) com desktop Analytics. Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, versão 1803 e mais tarde | Esta definição só se aplica quando a definição de AllowTelemettry é `2` . Limita os eventos de dados de diagnóstico melhorados enviados à Microsoft apenas para os eventos necessários pelo Desktop Analytics. Para obter mais informações, consulte os eventos e campos de [dados de diagnóstico do Windows 10 recolhidos através da política de dados](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)de diagnóstico reforçado. |
| **PermitirNomeNameInTelemetria** | GPO | Windows 10, versão 1803 e mais tarde | Ativar os dispositivos para enviar o nome do dispositivo. O nome do dispositivo não é enviado para a Microsoft por padrão. Se não enviar o nome do dispositivo, aparece no Desktop Analytics como "Desconhecido". Para mais informações, consulte [o nome do dispositivo](enroll-devices.md#device-name). |
| **CommercialDataOptin** | Localização | Windows 8.1 e mais cedo | Desktop Analytics requer um valor de `1` . Para mais informações, consulte [O Opt-in de Dados Comerciais no Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Ambos | Windows 8.1 e mais cedo | Desktop Analytics requer um valor para a recolha de `1` dados funcionar corretamente. |
| **DisableEnterpriseAuthProxy** | GPO | Todas as versões do Windows | Se o seu ambiente necessitar de um proxy autenticado pelo utilizador com autenticação integrada do Windows para acesso à Internet, o Desktop Analytics requer um valor para que a recolha de `0` dados funcione corretamente. Para mais informações, consulte a [autenticação](enable-data-sharing.md#proxy-server-authentication)do servidor Proxy . |

> [!IMPORTANT]
> Na maioria das circunstâncias, utilize apenas o Configuro Diretor de Configuração para configurar estas definições. Não aplique também estas definições em objetos de política de grupo de domínio. Para mais informações, consulte [a resolução de conflitos.](enroll-devices.md#conflict-resolution)

### <a name="settings-from-upgrade-readiness"></a>Definições da prontidão de upgrade

O Windows Analytics também definiu as seguintes políticas através do script de preparação de upgrade:

- Comercialid
- PermitirNomeNameInTelemetria
- CommercialDataOptin
- RequestAllAppraiserVersions

Se executasse o script de embarque de atualização de um dispositivo, estas definições de política podem ainda existir. Não use o guião do legado. Antes de inscrever o dispositivo no Desktop Analytics, remova estas definições de política anteriores.

## <a name="group-policy-settings"></a>Definições da política de grupo

Em geral, utilize as coleções do Gestor de Configuração para direcionar as definições e inscrições do Desktop Analytics. Utilize adesão direta ou consultas para incluir ou excluir dispositivos da recolha. Para mais informações, consulte [Como criar coleções.](../core/clients/manage/collections/create-collections.md)

O Gestor de Configuração configura as definições de ID comerciais e de diagnóstico na sua recolha de alvos. Se precisar de configurar diferentes definições de dados de diagnóstico para diferentes grupos de dispositivos, utilize as definições de política do grupo para anular as definições do Gestor de Configuração. Por exemplo, é necessário definir o nível **Melhorado (Limitado)** para alguns dispositivos e **Basic** para outros. Alguns dispositivos podem ter diferentes definições de autenticação do [servidor proxy.](enable-data-sharing.md#proxy-server-authentication)

As definições de política de grupo relevantes estão no seguinte caminho: **Configuração**de computador  >  **Administrative Templates**  >  **Modelos Administrativos De Recolha**de Dados de Componentes Windows  >  **e Visualização**de Visualizações .

As definições de política do grupo apenas modificam as definições de registo na seguinte tecla:`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Quando utilizar as definições de política de grupo para permitir cenários complexos, preste especial atenção às definições de políticas que podem causar conflitos de configuração. O Gestor de Configuração só configura [as definições do Windows](#windows-settings) se o valor já não *existir*. As definições de política do grupo têm precedência sobre as definições do Gestor de Configuração, para que certas configurações de política do grupo possam causar problemas com desktop Analytics.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Definições de política de grupo que podem entrar em conflito com as definições do Gestor de Configuração para Desktop Analytics

As definições de política do grupo na tabela a seguir têm o maior potencial para causar conflito com as definições do Windows que o Gestor de Configuração define nos dispositivos que se inscreve no Desktop Analytics:

| Nome a apresentar | Valor de registo | Efeito nos dispositivos matriculados no Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configure o ID Comercial** | Comercialid | Se definir esta política para um valor diferente, substitui o ID Comercial definido pelo Gestor de Configuração. Se não for o mesmo ID, os dispositivos configurados podem não aparecer no Desktop Analytics. |
| **Permitir telemetria** | Permitir Telemetria | Se definir esta política para um valor diferente, sobrepõe-se ao nível global de dados de diagnóstico que definiu no Gestor de Configuração para a recolha do alvo. |
| **Limite dados de diagnóstico melhorados ao mínimo exigido pelo Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Esta política depende da definição anterior de AllowTelemettry. Dependendo do nível definido no Gestor de Configuração ou com a política de grupo, esta política pode alterar o nível de dados de diagnóstico no dispositivo para **Melhorado** ou **Melhorado (Limitado)**. Esta política só se aplica se a AllowTelemettry estiver definida `2` para (**Melhorado).** |
| **Permitir que o nome do dispositivo seja enviado em dados de diagnóstico do Windows** | PermitirNomeNameInTelemetria | Se optar por enviar nomes de dispositivos no 'Gestor de Configuração', pode anulá-lo b configurando esta política para Desativado. Quando desativa esta definição, os nomes do dispositivo aparecem como "Desconhecidos" no Desktop Analytics. Para mais informações, consulte [o nome do dispositivo](enroll-devices.md#device-name). |
| **Configure o uso de Proxy autenticado para o serviço de experiência e telemetria do utilizador conectado** | DisableEnterpriseAuthProxy | Se configurar os dispositivos Do Gestor de Configuração para utilizar o proxy autenticado pelo utilizador ( `0` ), se configurar esta política para **desativar** a utilização do Proxy Autenticado ( ), então o dispositivo envia dados de `1` diagnóstico no contexto do sistema em vez do contexto do utilizador. Se não configurar o dispositivo com um proxy no contexto do sistema, ou se o dispositivo não conseguir autenticar o proxy, o Windows não pode enviar dados de diagnóstico para desktop Analytics. |

> [!NOTE]
> A política antiga **Configure Connected User Experiences and Telemettry** (TelemettryProxy) permite que o Windows reencaminhoos dados de diagnóstico para um representante dedicado, em vez de utilizar o utilizador (WinINET) ou proxy do dispositivo (WinHTTP). Alguns componentes do Windows não suportam esta política. Se utilizar esta política, pode causar problemas de qualidade de dados no Desktop Analytics.

#### <a name="behavior-of-disabled-settings"></a>Comportamento das definições de deficientes

Se configurar estas definições de política de grupo para **Desativar,** tem efeitos diferentes no comportamento do sistema.

- Quando desativa a política **CommercialId,** o Windows remove o valor do registo. A definição do Gestor de Configuração para o ID comercial, que está definida na trajetória de registo de políticas locais, aplica-se depois ao dispositivo.

- Para as políticas que o Gestor de Configuração define no mesmo local de registo que a política do grupo, quando desativa a definição na política do grupo, o Windows remove o valor do registo. O Gestor de Configuração irá redefini-lo no seu próximo ciclo de processamento de políticas e, em seguida, o Windows irá removê-lo na próxima atualização da política do grupo. Esta constante alteração na configuração pode causar comportamentos indesejados com desktop Analytics.

  - Se definir estas definições de política de grupo para **Não configuradas,** o Windows remove o valor uma vez, mas não continua a removê-lo. Esta configuração permite que o Gestor de Configuração aplique os seus valores como esperado.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Definições de política de grupo para personalizar a experiência do utilizador

Estas definições de política de grupo não são exigidas pelo Gestor de Configuração ou pelo Desktop Analytics. Pode configurá-los na política de grupo para configurar a experiência dos seus utilizadores com dados de diagnóstico do Windows.

| Nome a apresentar | Valor de registo | Efeito nos dispositivos matriculados no Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configure notificações de opt-in de alteração de telemetria** | DesativarTelemettryOptInChangeNotification | A partir do Windows 10, versão 1803, o Windows notifica os utilizadores quando o nível de dados de diagnóstico muda. Utilize esta política para desativar notificações. |
| **Configure a interface de opt-in de definição de telemetria** | DesactivarTelemettryOptInSettingsUx | Quando configurar o nível de dados de diagnóstico, define o limite superior para o dispositivo. A partir do Windows 10, versão 1803, os utilizadores podem definir um nível mais baixo. Utilize esta política para evitar que os utilizadores mudem o nível de diagnóstico. Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Desativar a apagando dados de diagnóstico** | Desativação de dispositivos | A partir do Windows 10, versão 1809, os utilizadores podem eliminar dados de diagnóstico da página de definições **de feedback de Diagnóstico &.** Utilize esta política para evitar a eliminação de dados de diagnóstico que a Microsoft recolhe do dispositivo. |
| **Desativar o visualizador de dados de diagnóstico** | DesativarOVisualizador de Dados deDiagnóstico | A partir do Windows 10, versão 1809, os utilizadores podem ativar e abrir o Visualizador de Dados de Diagnóstico a partir da página de definições de **feedback de Diagnóstico &.** Utilize esta política para desativar o Visualizador de Dados de Diagnóstico nas definições do Windows e evite que mostre os dados de diagnóstico que a Microsoft recolhe do dispositivo.|
