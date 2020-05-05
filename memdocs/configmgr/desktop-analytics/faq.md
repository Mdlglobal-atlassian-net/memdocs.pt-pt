---
title: FAQ para Desktop Analytics
titleSuffix: Configuration Manager
description: Perguntas frequentes para desktop Analytics.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 29f063da47dc26789493b2a83ad8e0cfa6885270
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693296"
---
# <a name="desktop-analytics-faq"></a>FAQ da Análise de Computadores

## <a name="prerequisites"></a>Pré-requisitos

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a>Posso usar análises ativadas por nuvem com dispositivos geridos por Intune?

Ainda não hoje, mas veja o anúncio da Microsoft Ignite 2019 sobre a [gestão de dispositivos orientados por insights.](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions) Esta solução planeada é sucessora da Saúde do Dispositivo e da Prontidão de Upgrade.

A grande maioria dos clientes que podem beneficiar do workflow desktop Analytics usam o Gestor de Configuração para implementar o Windows. Sabemos que os clientes intune adoram as informações adicionais dos dados de análise, e estamos a trabalhar em formas de partilhar informações com eles também.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Já se passaram mais de 72 horas e o portal ainda está a processar dados, o que vem a seguir?

Quando configurar pela primeira vez o Desktop Analytics, os relatórios no Diretor de Configuração e no portal Desktop Analytics podem não apresentar imediatamente dados completos. Pode levar 2 a 3 dias para o serviço processar os dados. Se já passaram mais de 72 horas, e o portal ainda está a processar dados, siga estes passos:

- Para confirmar que os dispositivos ativos estão corretamente configurados, utilize o painel de [instrumentos de saúde](monitor-connection-health.md)de ligação . Este painel não atualiza em tempo real.
- Certifique-se de que os dispositivos estão a enviar dados de diagnóstico para o serviço Desktop Analytics. Para mais informações, consulte [Permitir a partilha de dados.](enable-data-sharing.md)
- Provisão [De aplicações aD Azure](troubleshooting.md#bkmk_AzureADApps) no seu Anúncio Azure.
- Verifique os dispositivos que associou à sua organização nos últimos sete dias. No [portal Desktop Analytics,](https://aka.ms/desktopanalytics)vá ao painel de **serviços Conectados.** Selecione **dispositivos de inscrição**e **ver dados recentes**

  > [!IMPORTANT]
  > A opção Desktop Analytics para **ver dados recentes** é depreciada. Esta ação será removida num futuro lançamento do serviço Desktop Analytics. Para mais informações, consulte [as funcionalidades deprecatadas.](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)<!--7080949-->  

Se os dispositivos estiverem corretamente configurados e ainda não estiver a ver dados no seu espaço de trabalho, [contacte](https://support.microsoft.com/hub/4343728/support-for-business)o suporte da Microsoft .

## <a name="connect-configuration-manager"></a>Ligar Gestor de Configuração

### <a name="can-i-change-the-target-or-additional-collections"></a>Posso mudar o alvo ou coleções adicionais?

Sim, use o seguinte processo:

- Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** Abra as propriedades para a entrada associada ao seu serviço Desktop Analytics.

- No separador **desktop Analytics Connection,** altere a **Coleção Target** ou gere as coleções adicionais.

> [!IMPORTANT]  
> O Gestor de Configuração utiliza uma política de definições para configurar dispositivos na recolha do alvo. Esta política inclui as definições de dados de diagnóstico para permitir que os dispositivos enviem dados para a Microsoft. Alterar a recolha de alvos não desfaz a política de definições dos dispositivos que já não se encontra na recolha do alvo. Se não quiser que os seus dispositivos continuem a enviar dados de diagnóstico, [reconfigure os dispositivos](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Atualização do Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Posso atualizar o Windows e mudar de arquitetura?

O Desktop Analytics foi concebido para melhor suportar as atualizações no local. As atualizações no local não suportam migrações de arquitetura de 32 a 64 bits. Se precisar de migrar computadores neste cenário, utilize o cenário de atualização. As informações do Desktop Analytics ainda são valiosas neste cenário, mas pode ignorar a orientação específica da atualização.

Para mais informações, consulte [Refresh um computador existente com uma nova versão do Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Posso mudar de BIOS para UEFI ao atualizar o Windows?

Sim. Para mais informações, consulte [Converter de BIOS para UEFI durante uma atualização no local](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Posso usar desktop analytics com Windows 10 LTSC?

O Desktop Analytics não suporta dispositivos do Canal de Manutenção de Longo Prazo (LTSC) do Windows 10. Para mais informações, consulte o [Windows como uma visão geral](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)do serviço .

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Posso reduzir o tempo que os dados demoram a atualizar no meu portal Desktop Analytics?

Existem dois tipos de dados no portal Desktop Analytics: Dados do administrador e dados de diagnóstico. Para atualizar os dados do administrador a pedido, abra a moeda de dados e selecione **Aplicar alterações**. Esta ação desencadeia imediatamente uma atualização única de quaisquer alterações pendentes de administrador nos seus espaços de trabalho. As alterações propagam-se e estão geralmente disponíveis dentro de 15-60 minutos. O tempo depende do tamanho do seu espaço de trabalho e do âmbito de alterações pendentes. Pode solicitar uma atualização de dados a pedido até seis vezes num período de 24 horas.

Todos os dados são atualizados automaticamente uma vez por dia, mesmo que não solicite uma atualização de dados on-demand. Não há como desencadear uma atualização a pedido de dados de diagnóstico. Para obter mais informações sobre os diferentes tipos de dados no Desktop Analytics, consulte [a latência de dados](troubleshooting.md#data-latency).

## <a name="privacy"></a>Privacidade

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>O Desktop Analytics pode ser utilizado sem uma ligação direta do cliente ao Serviço de Gestão de Dados da Microsoft?

Não, todo o serviço é alimentado por dados de diagnóstico do Windows, o que requer que os dispositivos tenham esta conectividade direta.

### <a name="can-i-choose-the-data-center-location"></a>Posso escolher a localização do centro de dados?

Para O Analítico de Log Azure: Sim, quando configurar desktop Analytics e criar o espaço de trabalho do Log Analytics.

Para o Microsoft Data Management Service e Analytics Azure Storage: Não, estes dois serviços estão hospedados nos Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>Onde estão armazenados os dados da minha organização?

Os dados de diagnóstico do Windows dos seus computadores são encriptados, enviados e processados em centros de dados seguros geridos pela Microsoft localizados nos Estados Unidos. A Microsoft fornece-lhe a análise dos dados relacionados com o Desktop Analytics através da solução Desktop Analytics no portal Azure. O Desktop Analytics é suportado na maioria das regiões onde [o Log Analytics está disponível.](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all) Se selecionar uma região internacional do Azure, os seus dados de diagnóstico ainda são enviados e processados nos centros de dados seguros da Microsoft nos Estados Unidos.

## <a name="existing-windows-analytics-customers"></a>Clientes existentes do Windows Analytics

> [!Important]  
> O serviço Windows Analytics está reformado a partir de 31 de janeiro de 2020.
>
> Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Posso usar a conformidade da atualização juntamente com o Desktop Analytics?

Sim. Se utilizar a [Atualização do Portal](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) Azure hoje, pode continuar a fazê-lo agora e além de janeiro de 2020.

Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Existem funcionalidades do Windows Analytics que não estejam disponíveis no Desktop Analytics?

<!-- 3616924 -->
Sim, as seguintes funcionalidades do Windows Analytics foram reformadas ou ainda não estão disponíveis no Desktop Analytics:

#### <a name="general"></a>Geral

- Suporte para cenários que não requerem Gestor de Configuração. Por exemplo, [suporte Intune](#bkmk_intune).
- Pré-requisito de licenciamento de qualquer licença válida do Windows contra E3, E5
- Apoio a vários espaços de trabalho por inquilino da AD Azure
- Capacidade de executar consultas personalizadas e exportar dados de soluções cruas
- Documentação do modelo de dados para relatórios personalizados

#### <a name="upgrade-readiness"></a>Preparação de Atualizações

- Dados da Descoberta do Site do Explorador da Internet
- Informações adicionais de escritório (agora disponíveis no Gestor de [Configuração)](#bkmk_office)
- Insights do Feedback Hub

#### <a name="update-compliance"></a>Conformidade de Atualizações

- Suporte para Atualização do Windows para Negócios
- Insights de otimização de entrega
- Suporte para canal de manutenção de longo prazo do Windows 10 (LTSC)
- Relatórios do Windows Insider
- Estado do Windows Defender

> [!Note]
> Todas as funcionalidades de conformidade de atualização existentes, incluindo as que não estão disponíveis no Desktop Analytics, permanecem disponíveis na solução de conformidade de [atualização](/windows/deployment/update/update-compliance-get-started) no portal Azure.

#### <a name="device-health"></a>Estado de Funcionamento do Dispositivo

- Saúde do condutor
- Saúde da aplicação (fora de um plano de implantação)
- Frequentemente, dispositivos de colisão ou acidentes induzidos pelo condutor
- Saúde de inscrição nas janelas
- Windows Information Protection
- Suporte para Servidor Windows

## <a name="other"></a>Outros

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a>Posso usar desktop Analytics para as minhas atualizações Do Office 365 ProPlus?

Não, desktop Analytics está focado no Windows. A Microsoft desenvolveu o Desktop Analytics em estreita colaboração com muitos clientes. O feedback do cliente é sobre como o Desktop Analytics melhora a sua capacidade de gerir com confiança as implementações do Windows. Também nos dizem que querem disponibilidade do [Office 365 ProPlus](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) mais intimamente integrada com ferramentas de gestão do Office em Configuração Manager e Intune. A Microsoft continua a investir nessas áreas, ao mesmo tempo que se foca nos cenários do Windows no Desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Como posso fornecer feedback sobre desktop Analytics?

Para partilhar o seu feedback sobre desktop Analytics, selecione o ícone **Enviar um Sorriso** no topo do portal. Inclua uma imagem com a sua submissão para ajudar a Microsoft a entender melhor o seu feedback. Também pode submeter sugestões de produtos e dar voz a outras ideias no [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Nunca partilhe informações privadas via Enviar um Sorriso ou UserVoice. Tais informações privadas incluem o seu Id de Inquilino ou Id Comercial. A Microsoft não fornece suporte através dos canais Send a Smile ou UserVoice. Para obter ajuda com o seu espaço de trabalho desktop Analytics, selecione o link **de ajuda e suporte** no menu de navegação para abrir um bilhete de suporte.
