---
title: Privacidade de dados do Desktop Analytics
titleSuffix: Configuration Manager
description: Desktop Analytics está comprometido com a privacidade dos dados dos clientes
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd970dc1517a6fcc197b2bf39a141871b4999a02
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268424"
---
# <a name="desktop-analytics-data-privacy"></a>Privacidade de dados do Desktop Analytics

O Desktop Analytics está totalmente comprometido com a privacidade dos dados dos clientes, centrando-se nestes princípios:

- **Transparência:** Documentamos totalmente os eventos de diagnóstico do Windows. Reveja-os com as equipas de segurança e conformidade da sua empresa. O Windows Diagnostic Data Viewer permite-lhe ver os dados de diagnóstico enviados a partir de um determinado dispositivo. Para mais informações, consulte a visão geral do [Visualizador](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)de Dados de Diagnóstico .  

- **Controlo:** Controla o nível de dados de diagnóstico para partilhar com a Microsoft. O Windows 10, versão 1709, adiciona uma nova política para limitar os dados de diagnóstico melhorados ao mínimo exigido pelo Desktop Analytics.  

- **Segurança:** A Microsoft protege os seus dados com uma forte segurança e encriptação.  

- **Confiança:** Desktop Analytics suporta a Declaração de [Privacidade](https://privacy.microsoft.com/privacystatement) da Microsoft e [os Termos do Serviço Online](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

Para mais informações, consulte os [serviços do Windows onde a Microsoft é o processador sob o RGPD](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Fluxo de dados

A seguinte ilustração mostra como os dados de diagnóstico fluem de dispositivos individuais através do Serviço de Dados de Diagnóstico, armazenamento transitório e para o seu espaço de trabalho Log Analytics:

![Diagrama ilustrando fluxo de dados de diagnóstico de dispositivos](media/da-data-flow.png)

1. Inscrevo no portal Azure e a bordo do Desktop Analytics. Cria a aplicação Azure AD para se conectar com o Gestor de Configuração. Ao configurar o Desktop Analytics, cria-se um espaço de trabalho Azure Log Analytics na localização à sua escolha.  

2. Ligao O Gestor de Configuração e os dispositivos de inscrição  

    1. Configura o serviço de nuvem desktop Analytics em 'Configuração' com os detalhes da aplicação Azure AD.  

    2. Dentro de 15 minutos, o Gestor de Configuração sincroniza os seguintes dados com desktop Analytics usando o seu ID de inquilino. Repete este processo a cada hora.

      - Informações sobre recolhas de dispositivos necessárias para criar planos de [implementação.](create-deployment-plans.md) Estas informações incluem id de recolha, ID da hierarquia, nome de recolha e contagem de dispositivos. 
      - Informações necessárias para [inscrever dispositivos](enroll-devices.md). Estas informações incluem id de recolha, identificador exclusivo SMS, versão de construção de OS, nome do dispositivo e número de série.
      - Informações do painel de saúde de [ligação](monitor-connection-health.md) monitora. Estas informações incluem a contagem de dispositivos por estado de saúde e propriedades do dispositivo.
      - Informações sobre planos de implementação, que incluem o ID de recolha, id de implementação, tipo piloto ou de implantação de produção, e contagem de dispositivos por decisão de upgrade.

    3. O Gestor de Configuração define o ID comercial, o nível de dados de diagnóstico e outras definições para os dispositivos na recolha do alvo. Esta configuração especifica os dispositivos a aparecer no seu espaço de trabalho desktop Analytics.  

    4. Implementa atualizações de compatibilidade para todos os dispositivos-alvo.  

3. Os dispositivos enviam dados de diagnóstico para o serviço de Gestão de Dados de Diagnóstico da Microsoft para windows. Este serviço está hospedado nos Estados Unidos.  

4. Todos os dias, a Microsoft produz uma imagem de insights focados em TI. Este instantâneo combina os dados de diagnóstico do Windows com a sua entrada para os dispositivos matriculados. Este processo ocorre em armazenamento transitório, que é usado apenas pela Desktop Analytics. O armazenamento transitório está alojado em centros de dados da Microsoft nos Estados Unidos. Todos os dados são enviados num canal encriptado SSL (HTTPS). As fotos são segregadas por identificação comercial.  

5. As imagens são então copiadas para o seu espaço de trabalho Azure Log Analytics. Esta transferência de dados acontece através de HTTPS através do protocolo de ingestão de webhook, que é uma funcionalidade do Log Analytics. O Desktop Analytics não tem nenhuma leitura ou permissão para o seu armazenamento de Log Analytics. O Desktop Analytics chama a Webhook API com uma assinatura de acesso partilhado (SAS) URI. Em seguida, o Log Analytics obtém os dados das tabelas de armazenamento através de HTTPS.

6. Desktop Analytics armazena a sua entrada no armazenamento de Log Analytics. Estas configurações incluem planos de implementação e decisões de ativos para upgrade e importância.  

## <a name="other-resources"></a>Outros recursos

Para perguntas relacionadas com a privacidade frequentemente feitas para desktop Analytics, consulte [Privacy FAQ](faq.md#privacy).

Para obter mais informações sobre aspetos de privacidade relacionados, consulte os seguintes artigos:

- [Windows 10 e o RGPD para decisores de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8 e Windows 8.1 avaliam eventos e campos de diagnóstico](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versão 1809 de nível básico Eventos e campos de diagnóstico do Windows](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versão 1709 melhorado eventos de dados de diagnóstico e campos utilizados pelo Desktop Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Visão geral do visualizador de dados de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Termos de licenciamento e documentação](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Segurança de dados do Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Segurança e privacidade nos centros de dados do Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confiança na nuvem de confiança](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro de Confiança](https://www.microsoft.com/trustcenter)  

- [Escudo de Privacidade](https://www.privacyshield.gov/)  

Separado do Desktop Analytics, o Gestor de Configuração envia dados de diagnóstico e utilização para a Microsoft. A Microsoft utiliza estes dados para melhorar a experiência de instalação, qualidade e segurança de futuras versões do Gestor de Configuração. Para mais informações, consulte Diagnósticos e dados de [utilização para 'Gestor](../core/plan-design/diagnostics/diagnostics-and-usage-data.md)de Configuração'.
