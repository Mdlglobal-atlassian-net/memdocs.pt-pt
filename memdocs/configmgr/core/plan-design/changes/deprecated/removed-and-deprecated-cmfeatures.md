---
title: Características depreciadas
titleSuffix: Configuration Manager
description: Conheça as funcionalidades que o Gestor de Configuração já não suporta.
ms.date: 05/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 184c836a601378fcb8e58f78debb80a3cd48857c
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693108"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Funcionalidades removidas e depreciadas para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo lista as funcionalidades que são depreciadas ou removidas do suporte para O Gestor de Configuração. As funcionalidades depreciadas serão removidas numa futura atualização. Estas futuras alterações podem afetar a sua utilização do Gestor de Configuração.  

Esta informação está sujeita a alterações com futuras versões. Pode não incluir cada funcionalidade de Gestor de Configuração depreciada.

## <a name="deprecated-features"></a>Características depreciadas

As seguintes características são depreciadas. Ainda pode usá-los agora, mas a Microsoft planeia acabar com o suporte no futuro.

|Funcionalidade|Preterição anunciada pela primeira vez|Suporte&nbsp;removido|
|-----------|---|--------------|
| Opção Desktop Analytics para **visualizar dados recentes** para a inscrição do dispositivo e atualizações de segurança.<!-- 7080949 --> Para mais informações, consulte [a latência de Dados](../../../../desktop-analytics/troubleshooting.md#data-latency).|maio de 2020|julho de 2020|
|A implementação para partilha de conteúdos do Azure mudou. Utilize um gateway de gestão de nuvem ativado por conteúdo. Não poderá criar um ponto tradicional de distribuição de nuvens no futuro.|Fevereiro de 2019|<sup>[Nota TBD 1](#bkmk_note1)</sup>|
|Implantação de serviço clássico para Azure para gateway de gestão de nuvem e ponto de distribuição de nuvem. Para mais informações, consulte [Plano para CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|Novembro de 2018|<sup>[Nota TBD 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a>Nota 1: Suporte removido TBD

O prazo específico deve ser determinado (TBD). A Microsoft recomenda que altere o novo processo ou funcionalidade, mas pode continuar a utilizar o processo ou funcionalidade depreciado num futuro próximo.

## <a name="unsupported-and-removed-features"></a>Características não suportadas e removidas

As seguintes características já não são suportadas. Em alguns casos, já não estão no produto.

|Funcionalidade|Preterição anunciada pela primeira vez|Suporte&nbsp;removido|  
|-----------|---|--------------|  
| Integração de Analítico sonérs e Atualização. Para mais informações, consulte [KB 4521815: Reforma do Windows Analytics a 31 de janeiro de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14 de outubro de 2019 | 31 de janeiro de 2020 |
| Avaliação de atestado de saúde dos dispositivos para políticas de conformidade de acesso condicional <!--1235616 aka 3608202--> Para mais informações, veja [o que aconteceu ao MDM híbrido.](../../../../mdm/understand/what-happened-to-hybrid.md)| 3 de julho de 2019 | Versão 1910 |
| A aplicação Portal do Portal do Gestor de Configuração | 21 de maio de 2019 | Versão 1910 |
| O catálogo de aplicações, incluindo ambas as funções do sistema do site: o ponto de site do catálogo de aplicações e o ponto de serviço web. Para mais informações, consulte [Remova o catálogo de aplicações](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21 de maio de 2019 | Versão 1910 |
|Autenticação baseada em certificado com definições do Windows Hello para negócios no Gestor de Configuração<br>Para mais informações, consulte [as definições do Windows Hello for Business](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Dezembro de 2017|Versão 1910|
|Proteção de ponto final do centro do sistema para Mac e Linux<br>Para mais informações, consulte [End of support blog post](https://go.microsoft.com/fwlink/?linkid=870182).|Outubro de 2018|31 de dezembro de 2018|
|Acesso condicional no local<br>Para mais informações, veja [o que aconteceu ao MDM híbrido.](../../../../mdm/understand/what-happened-to-hybrid.md)|30 de janeiro de 2019|1 de setembro de 2019|
|Gestão de dispositivos móveis híbridos (MDM)<br>Para mais informações, veja [o que aconteceu ao MDM híbrido.](../../../../mdm/understand/what-happened-to-hybrid.md)<br><br>A partir do lançamento do serviço Intune de 1902, previsto para o final de fevereiro de 2019, os novos clientes não conseguem criar uma nova ligação híbrida.<!--Intune feature 2683117-->|14 de agosto de 2018|1 de setembro de 2019|
|Extensões do Protocolo de Automação de Conteúdos de Segurança (SCAP). <!--3607889--><br>A versão certificada anterior ainda está disponível no [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=48741).|Setembro de 2018|Versão 1810|
|A experiência do **utilizador Silverlight** para o ponto de site do catálogo de aplicações já não é suportada. Os utilizadores devem utilizar o novo Centro de Software. Para mais informações, consulte [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11 de agosto de 2017| Versão 1806|
|A versão anterior do Software Center.<br><br>Para mais informações sobre o novo Centro de Software, consulte Plan para e configurar a gestão de [aplicações.](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex)|13 de dezembro de 2016|Versão 1802|
|Gestão de Discos Rígidos Virtuais (VHDs) com Gestor de Configuração. <br><br>Esta depreciação inclui a remoção de opções para criar um novo VHD ou gerir um VHD utilizando uma sequência de tarefas, e a remoção do nó de Discos Rígidos Virtuais da consola do Gestor de Configuração. <br><br>Os VHDs existentes não são eliminados, mas já não são acessíveis a partir da consola Do Gestor de Configuração.  |6 de janeiro de 2017 |Versão 1710|
|Sequências de tarefas: <br /> - Converter disco para dinâmico <br /> - Instalar ferramentas de implantação |18 de novembro de 2016|Versão 1710|
|Ferramenta de avaliação de upgrade<br><br>A ferramenta de avaliação de upgrade depende tanto do Gestor de Configuração como do Kit de Ferramentas de Compatibilidade de Aplicações (ACT) 6.x. A versão final da ACT foi enviada no ADK do Windows 10 v1511. Como não há mais atualizações para a ACT, o suporte para a Ferramenta de Avaliação de Upgrade é descontinuado. O aviso de depreciação foi adicionado à página de [descarregamento da UAT](https://www.microsoft.com/software-download/windows10) no dia 12 de setembro de 2016. | 12 de setembro de 2016  | 11 de julho de 2017 |
|Pontos de atualização de software com um cluster de equilíbrio de carga de rede (NLB) | 27 de fevereiro de 2016 | Versão 1702 |
|Sequências de tarefas: <br /> - OsdPreserveDriveLetter  <br /><br /> Durante uma implementação do sistema operativo, por padrão, o Windows Setup determina agora a melhor letra de acionamento a utilizar (tipicamente C:). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização na sequência de sequência de tarefas do Sistema Operativo Aplicar. Vá ao Select o local onde pretende aplicar esta definição do **sistema operativo.** Selecione **a letra de unidade lógica específica** e escolha a unidade que pretende utilizar. |20 de junho de 2016 |Versão 1606 |
|Proteção de Acesso de Rede (NAP) - conforme encontrado no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Out of Band Management - como encontrado no System Center 2012 Diretor de Configuração|16 de outubro de 2015|Versão 1511|

### <a name="features-removed-in-version-1511"></a>Características removidas na versão 1511

As seguintes secções incluem detalhes adicionais para funcionalidades removidas com a versão 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a>Fora da Gestão de Bandas  

Com o Gestor de Configuração, foi removido o suporte nativo para computadores baseados em AMT a partir da consola 'Gestor de Configuração'.  

- Os computadores baseados em AMT permanecem totalmente geridos quando utiliza o [Add-on Intel SCS para O Gestor de Configuração](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O addon fornece-lhe acesso às mais recentes capacidades de gestão da AMT, ao mesmo tempo que elimina as limitações introduzidas até que o Gestor de Configuração possa incorporar essas alterações.  

- Fora da Gestão de Bandas no System Center 2012 O Gestor de Configuração não é afetado por esta alteração.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a>Proteção de Acesso à Rede

O Gestor de Configuração removeu o suporte para a Proteção de Acesso à Rede. A funcionalidade foi depreciada no Windows Server 2012 R2 e foi removida do Windows 10.  

Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="see-also"></a>Consulte também

- [Removidas e preteridas](removed-and-deprecated.md)
- [Ciclo de vida do suporte da Microsoft](https://support.microsoft.com/lifecycle)
- [Suporte para versões de ramificação atuais do Gestor de Configuração](../../../servers/manage/current-branch-versions-supported.md)
