---
title: Ativar a partilha de dados
titleSuffix: Configuration Manager
description: Um guia de referência para a partilha de dados de diagnóstico com desktop Analytics.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0811c695acba4859bf32de535a28ea55cf8eee07
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268747"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Ativar a partilha de dados para desktop Analytics

Para inscrever dispositivos no Desktop Analytics, precisam de enviar dados de diagnóstico para a Microsoft. Se o seu ambiente utilizar um servidor proxy, use estas informações para ajudar a configurar o proxy.

## <a name="diagnostic-data-levels"></a>Níveis de dados de diagnóstico

![Diagrama dos níveis de dados de diagnóstico para Desktop Analytics](media/diagnostic-data-levels.png)

Quando integra o Gestor de Configuração com desktop Analytics, também o utiliza para gerir o nível de dados de diagnóstico nos dispositivos. Para obter a melhor experiência, utilize o Gestor de Configuração.

> [!Important]  
> Na maioria das circunstâncias, utilize apenas o Configuro Diretor de Configuração para configurar estas definições. Não aplique também estas definições em objetos de política de grupo de domínio. Para mais informações, consulte [a resolução de conflitos.](enroll-devices.md#conflict-resolution)

A funcionalidade básica do Desktop Analytics funciona ao nível **básico** de dados de [diagnóstico.](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) Se não configurar o nível **Melhorado (Limitado)** no Gestor de Configuração, não obterá as seguintes funcionalidades do Desktop Analytics:

- Utilização de aplicativos
- [Insights adicionais de aplicativos](compat-assessment.md#additional-insights)
- Dados do estado de implantação
- Dados de monitorização da saúde

A Microsoft recomenda que ative o nível de dados de diagnóstico **Melhorado (Limitado)** com o Desktop Analytics para maximizar os benefícios que obtém dele.

> [!Tip]
> A definição **avançada (Limitada)** no Gestor de Configuração é a mesma definição que os dados de **diagnóstico limit Enhanced ao mínimo exigido pela** política do Windows Analytics disponível nos dispositivos que executam o Windows 10, versão 1709 e posteriormente.
>
> Os dispositivos que executam o Windows 10, a versão 1703 e anterior, o Windows 8.1 ou o Windows 7 não têm esta definição de política. Quando configura a definição **avançada (limitada)** no 'Gestor de Configuração', estes dispositivos voltam ao nível **Básico.**
>
> Os dispositivos que executam o Windows 10, versão 1709 têm esta definição de política. No entanto, quando configura a definição **avançada (limitada)** no Gestor de Configuração, estes dispositivos também recuam para o nível **Básico.**

Para obter mais informações sobre dados de diagnóstico partilhados com a Microsoft com **o Enhanced (Limited)** consulte o [Windows 10 para melhorar os eventos e campos](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)de dados de diagnóstico .

> [!Important]
> A Microsoft tem um forte compromisso em fornecer as ferramentas e recursos que o colocam no controlo da sua privacidade. Como resultado, enquanto o Desktop Analytics suporta dispositivos Windows 8.1, a Microsoft não recolhe dados de diagnóstico do Windows a partir de dispositivos Windows 8.1 localizados em países europeus (EEE e Suíça).

Para mais informações, consulte a [privacidade desktop Analytics](privacy.md).

Os seguintes artigos também são bons recursos para uma melhor compreensão dos níveis de dados de diagnóstico do Windows:

- [Windows 10 e o RGPD para decisores de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Os clientes configurados para limitar os dados de diagnóstico melhorados enviarão aproximadamente 2 MB de dados para a nuvem da Microsoft na digitalização completa inicial. O delta diário varia entre 250-400 KB por dia.
>
> A varredura diária do delta acontece às 3:00 da manhã (hora do dispositivo local). Alguns eventos são enviados à primeira hora disponível ao longo do dia. Estes tempos não são configuráveis.
>
> Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Pontos Finais

Para permitir a partilha de dados, configure o seu servidor proxy para permitir os seguintes pontos finais da Internet.

> [!Important]  
> Para a privacidade e integridade dos dados, o Windows verifica um certificado Microsoft SSL (fixação de certificado) ao comunicar com os pontos finais de dados de diagnóstico. Interceção e inspeção ssl não são possíveis. Para utilizar o Desktop Analytics, exclua estes pontos finais da inspeção SSL.<!-- BUG 4647542 -->

A partir da versão 2002, se o site do Gestor de Configuração não ligar aos pontos finais necessários para um serviço na nuvem, eleva uma mensagem de estado crítico ID 11488. Quando não consegue ligar-se ao serviço, o SMS_SERVICE_CONNECTOR o estado do componente muda para crítico. Ver estado detalhado no nó de [Estado do Componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) da consola 'Gestor de Configuração'.<!-- 5566763 -->

> [!NOTE]
> Para obter mais informações sobre as gamas de endereços IP da Microsoft, consulte [o Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Estes endereços atualizam-se regularmente. Não há granularidade por serviço, qualquer endereço IP nestas gamas poderia ser usado.

### <a name="server-connectivity-endpoints"></a>Pontos finais de conectividade do servidor

O ponto de ligação ao serviço tem de comunicar com os seguintes pontos finais:

| Ponto Final  | Função  |
|-----------|-----------|
| `https://aka.ms` | Usado para localizar o serviço |
| `https://graph.windows.net` | Usado para recuperar automaticamente definições como CommercialId ao anexar a sua hierarquia ao Desktop Analytics (na função De Servidor de Configuração). Para mais informações, consulte [Configure o proxy para um servidor](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)de sistema de site . |
| `https://*.manage.microsoft.com` | Usado para sincronizar membros de recolha de dispositivos, planos de implementação e estado de prontidão do dispositivo com desktop Analytics (apenas na função de Servidor de Configuração). Para mais informações, consulte [Configure o proxy para um servidor](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)de sistema de site . |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Experiência do utilizador e pontos finais de componentes de diagnóstico

Os dispositivos clientes precisam de comunicar com os seguintes pontos finais:

| Ponto Final  | Função  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Experiência do utilizador conectada e ponto final do componente de diagnóstico. Utilizado por dispositivos que executam o Windows 10, versão 1809 ou posterior, ou versão 1803 com a atualização cumulativa 2018-09 ou posteriormente instalado. |
| `https://v10.events.data.microsoft.com` | Experiência do utilizador conectada e ponto final do componente de diagnóstico. Utilizado por dispositivos que executam o Windows 10, versão 1803 _sem_ a atualização cumulativa de 2018-09 instalada. |
| `https://v10.vortex-win.data.microsoft.com` | Experiência do utilizador conectada e ponto final do componente de diagnóstico. Utilizado por dispositivos que executam o Windows 10, versão 1709 ou mais cedo. |
| `https://vortex-win.data.microsoft.com` | Experiência do utilizador conectada e ponto final do componente de diagnóstico. Utilizado por dispositivos que executam o Windows 7 e o Windows 8.1 |

### <a name="client-connectivity-endpoints"></a>Pontos finais da conectividade do cliente

Os dispositivos clientes precisam de comunicar com os seguintes pontos finais:

| Índice | Ponto Final  | Função  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Permite que a atualização de compatibilidade envie dados para a Microsoft. |
| 2 | `http://adl.windows.com` | Permite que a atualização de compatibilidade receba os dados mais recentes da compatibilidade da Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1803 ou mais cedo. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário para relatórios de saúde do dispositivo no Windows 10, versão 1809 ou mais tarde. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Relatório de Erros do Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessário monitorizar a saúde de implementação no Windows 10, versão 1809 ou posterior. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Análise de acidentes online (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Necessário para relatórios de saúde do dispositivo no Windows 10, versão 1809 ou mais tarde. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Análise de acidentes online (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Necessário monitorizar a saúde de implementação no Windows 10, versão 1803 ou mais cedo. |
| 13 | `https://login.live.com` | Necessário para fornecer uma identidade de dispositivo mais fiável para desktop Analytics. <br> <br>Para desativar o acesso à conta da Microsoft no utilizador final, utilize as definições de política em vez de bloquear este ponto final. Para mais informações, consulte [a conta da Microsoft na empresa.](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication) |
| 14 | `https://v20.events.data.microsoft.com` | Experiência do utilizador conectada e ponto final do componente de diagnóstico. |

## <a name="proxy-server-authentication"></a>Autenticação do servidor proxy

Se a sua organização utilizar a autenticação do servidor proxy para acesso à Internet, certifique-se de que não bloqueia os dados de diagnóstico por causa da autenticação. Se o seu representante não permitir que os dispositivos enviem estes dados, não aparecerão no Desktop Analytics.

### <a name="bypass-recommended"></a>Bypass (recomendado)

Configure os seus servidores proxy para não exigir a autenticação por procuração para o tráfego para os pontos finais de dados de diagnóstico. Esta opção é a solução mais abrangente. Funciona para todas as versões do Windows 10.  

### <a name="user-proxy-authentication"></a>Autenticação por procuração do utilizador

Configure os dispositivos para utilizar o contexto do utilizador inscrito para autenticação por procuração. Este método requer as seguintes configurações:

- Os dispositivos têm a atual atualização de qualidade para uma versão suportada do Windows

- Configure o proxy de nível de utilizador (proxy WinINET) nas **definições proxy** na Rede & grupo de Definições do Windows. Também pode utilizar o painel de controlo de opções de Internet legado.

- Certifique-se de que os utilizadores têm permissão de procuração para chegar aos pontos finais dos dados de diagnóstico. Esta opção requer que os dispositivos possuam utilizadores de consolas com permissões por procuração, pelo que não pode utilizar este método com dispositivos sem cabeça.

> [!IMPORTANT]
> A abordagem de autenticação por procuração do utilizador é incompatível com a utilização da Proteção avançada de ameaças do Microsoft Defender. Este comportamento deve-se ao facto de esta autenticação se basear na chave de registo **DisableEnterpriseAuthProxy** definida para , enquanto o `0` Microsoft Defender ATP exige que seja definido para `1` . Para mais informações, consulte configurações de [proxy de máquina seleção e conectividade](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)de internet no MICROSOFT Defender ATP .

### <a name="device-proxy-authentication"></a>Autenticação por procuração de dispositivo

Esta abordagem apoia os seguintes cenários:

- Dispositivos sem cabeça, onde nenhum utilizador entra ou utilizadores do dispositivo não têm acesso à Internet

- Proxies autenticados que não usam autenticação integrada do Windows

- Se também utilizar a Proteção avançada de ameaças do Microsoft Defender

Esta abordagem é a mais complexa porque requer as seguintes configurações:

- Certifique-se de que os dispositivos podem chegar ao servidor proxy através do WinHTTP no contexto do sistema local. Utilize uma das seguintes opções para configurar este comportamento:

  - A linha de comando`netsh winhttp set proxy`

  - Protocolo de auto-descoberta de procuração web (WPAD)

  - Procuração transparente

  - Configure o proxy WinINET em todo o dispositivo utilizando a seguinte definição de política de grupo: Faça definições de **procuração por máquina (em vez de por utilizador)** (ProxySettingsPerUser = `1` )

  - Ligação direcionada ou que utiliza tradução de endereços de rede (NAT)

- Configure servidores proxy para permitir que as contas de computador no Ative Directory acedam aos pontos finais dos dados de diagnóstico. Esta configuração requer servidores proxy para suportar a Autenticação Integrada do Windows.  
