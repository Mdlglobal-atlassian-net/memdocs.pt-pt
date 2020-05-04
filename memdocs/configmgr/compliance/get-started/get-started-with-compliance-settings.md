---
title: Introdução às definições de compatibilidade
titleSuffix: Configuration Manager
description: Saiba sobre conceitos fundamentais e como as definições de conformidade funcionam
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 59b0b799fd54e0e613f78b11b48b53b19d20ddbf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712226"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Começar com as definições de conformidade no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de criar as definições de conformidade do Gestor de Configuração, primeiro aprenda sobre conceitos fundamentais e compreenda como funcionam.  



## <a name="how-compliance-settings-work"></a>Como funcionam as definições de conformidade  
As definições de conformidade permitem-lhe gerir a configuração e cumprimento dos clientes na sua organização.  

Os itens de configuração enquadram-se em duas categorias principais:  

- **Definições para dispositivos que são geridos com o cliente Do Gestor** de Configuração - normalmente dispositivos nos quais instalou software cliente Do Gestor de Configuração para permitir a gestão do dispositivo.  

- **Definições para dispositivos que são geridos sem o cliente Do Gestor** de Configuração - normalmente dispositivos que são geridos com o Microsoft Intune, ou com a gestão do dispositivo do Gestor de Configuração no local.  



## <a name="what-devices-are-supported"></a>Quais são os dispositivos suportados?  

| Tipo de Dispositivo | Mais informações |  
|------------|----------------------|  
| PCs do Windows (com o cliente do Gestor de Configuração) | Crie itens de configuração personalizados para avaliar objetos como chaves de registo, ficheiros e atributos de Diretório Ativo.<br /><br /> Quando utilizar o tipo de artigo de configuração do Windows 10, selecione definições de uma lista predefinida. |  
| PCs windows (matriculados com MDM no local) | Selecione definições a partir de uma lista predefinida. |  
| Dispositivos Windows Phone (matriculados com MDM no local) | Selecione definições a partir de uma lista predefinida. |  
| Computadores Mac (com o cliente do Gestor de Configuração) | Crie itens de configuração personalizados para avaliar objetos como preferências de macOS e resultados devolvidos por um script. |  



## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
Um item de configuração é um recipiente que armazena informações específicas. A informação que configura risa do tipo de artigo de configuração. Os itens de configuração podem incluir as seguintes informações:

- **A informação do método** de deteção é apenas para itens de configuração do Windows que contêm definições de aplicação. Deteta se uma aplicação está instalada. Esta deteção utiliza o ficheiro instalador do Windows para a aplicação ou utilizando um script personalizado.  

- **As configurações** representam as condições comerciais ou técnicas para avaliar a conformidade com os dispositivos do cliente. Configure uma nova definição ou navegue para uma definição existente num computador de referência.  

- **As regras** de conformidade especificam as condições que definem a conformidade de uma definição de item de configuração. Antes de o cliente avaliar um ajuste para o cumprimento, deve ter pelo menos uma regra de conformidade. Algumas definições remediam valores não conformes. Crie novas regras ou navegue para uma configuração existente em qualquer item de configuração e selecione regras nele.  

- **As plataformas suportadas** são as plataformas do dispositivo que define em que o cliente avalia a conformidade dos itens de configuração. Se implementar um item de configuração para um dispositivo que não esteja na lista de plataformas suportadas, não avalia a conformidade.  



## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base da configuração?  
Defina uma linha de base de configuração que inclua os itens de configuração para avaliar. Inclua também as definições e regras que descrevem o nível de conformidade exigido. Importe estes dados de configuração a partir de pacotes de configuração do Gestor de Configuração. A Microsoft e outros fornecedores definem estes pacotes de configuração. Ou criar novos itens de configuração e linhas de base de configuração.  

Depois de definir uma linha de base de configuração, desemfina-a para as coleções de utilizadores e dispositivos. O cliente avalia então as definições de base para o cumprimento de um horário. Pode implantar mais do que uma linha de base de configuração para dispositivos. Esta granularidade proporciona um maior controlo da conformidade. 

Os dispositivos cliente avaliam a compatibilidade em relação a cada linha de base da configuração implementada e comunicam imediatamente os resultados ao site, utilizando mensagens de estado. Se um dispositivo estiver atualmente desligado da rede, mas descarregado a linha de base de configuração, ainda avalia a conformidade dos itens de configuração. Envia a informação de conformidade quando se reconecta.  

### <a name="monitoring-configuration-baselines"></a>Monitorização de linhas de base de configuração
- Monitorize os resultados da avaliação de conformidade na consola Do Gestor de Configuração, no espaço de trabalho de **Monitorização,** no nó de **Implementações.** Por exemplo:
  - Causas comuns de incumprimento
  - Erros
  - O número de utilizadores e dispositivos afetados
- Executar relatórios de definições de conformidade com detalhes adicionais. Por exemplo:
  - Quais os dispositivos que são compatíveis ou não conformes
  - Que elemento da linha de base de configuração está a fazer com que um computador não cumpra
- Ver os resultados da avaliação de conformidade dos computadores Windows que executam o cliente do Gestor de Configuração. Abra o painel de controlo do Gestor de **Configuração** e mude para o separador **Configurações.**  



## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de dados e perfis de utilizador  
Os itens de configuração para dados e perfis do utilizador incluem definições que controlam a forma como os utilizadores em computadores que executam o Windows 8 e posteriormente gerem:  
- Redirecionamento de pastas
- Ficheiros offline
- Perfis de roaming  

Implemente estes itens de configuração para as coleções dos utilizadores. Monitorize a sua conformidade a partir do nó de **Monitorização** da consola 'Gestor de Configuração'. Ao contrário de outros itens de configuração, não os adicione às linhas de base de configuração antes de os implementar. Desloque-as diretamente clicando em **colocar** na fita.  

Para mais informações, consulte Criar dados do utilizador e itens de [configuração](../deploy-use/create-user-data-and-profiles-configuration-items.md)de perfis .  



## <a name="remote-connection-profiles"></a>Perfis de ligação remota  
Os perfis de ligação remota fornecem um conjunto de ferramentas e recursos para ajudá-lo a criar, implementar e monitorizar as definições de ligação remota. Ao implementar estas definições para dispositivos, minimiza o esforço que os utilizadores finais necessitam para ligar os seus computadores à rede corporativa.  

Para mais informações, consulte Criar perfis de [ligação remota](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Atualização da edição do Windows
A política de upgrade da edição atualiza automaticamente os dispositivos que executam determinadas versões do Windows 10 para uma edição mais recente. Esta política fornece uma nova chave de produto ou ficheiro de licença que o dispositivo consome para atualizar.

Para mais informações, consulte [os dispositivos Dotados Windows com a política](../deploy-use/upgrade-windows-version.md) de upgrade da edição



## <a name="microsoft-edge-browser-profiles"></a>Perfis de navegador do Microsoft Edge
<!-- 1357310 -->
A partir da versão 1802, para os clientes que utilizam o navegador Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nos clientes do Windows 10, criar uma política de definições de conformidade para configurar várias definições do Microsoft Edge. 

Para mais informações, consulte os perfis do [navegador Microsoft Edge.](../deploy-use/browser-profiles.md)

