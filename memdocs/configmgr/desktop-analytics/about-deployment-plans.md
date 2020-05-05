---
title: Planos de implementação em Desktop Analytics
titleSuffix: Configuration Manager
description: Conheça os planos de implementação no Desktop Analytics.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c14eb9127b096f7fc4e4680735867913ea877f54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722537"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Sobre planos de implementação em Desktop Analytics

O Desktop Analytics recolhe e analisa dados de dispositivos, aplicações e controladores na sua organização. Com base nesta análise e na sua entrada, pode utilizar o serviço para criar planos de implementação para o Windows 10. Os planos de implantação têm as seguintes funcionalidades:  

- Recomendaautomaticamente quais os dispositivos a incluir nos pilotos  

- Identificar problemas de compatibilidade e sugerir atenuações  

- Avaliar a saúde da implantação antes, durante e após as atualizações  

- Acompanhe o progresso da sua implantação  

Como parte do seu plano de implantação, você faz as seguintes ações:  

- Defina quais as versões do Windows 10 que pretende implementar  

- Escolha quais os grupos de dispositivos para os quais pretende implementar  

- Criar regras de prontidão para a implantação  

- Defina a importância das suas apps  

- Escolha dispositivos-piloto com base em recomendações automáticas  

- Decida como corrigir problemas com apps com base em recomendações do Desktop Analytics  

Por padrão, desktop Analytics atualiza os dados do plano de implementação diariamente. Quaisquer alterações que faça dentro de um plano de implementação, como atribuir importância a uma app ou escolher um dispositivo para incluir num piloto, leva até 24 horas para processar. Para acelerar este processo, solicite uma atualização de dados a pedido. Para mais informações, consulte [desktop Analytics FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Depois de ligar o Desktop Analytics ao Gestor de Configuração, selecione as suas coleções nos planos de implementação. Esta integração permite então implementar o Windows para uma recolha com base nos dados do Desktop Analytics.



## <a name="readiness-rules"></a>Regras de prontidão

Estão disponíveis as seguintes regras de prontidão nos planos de implantação:

- Se os seus dispositivos recebem automaticamente os controladores do Windows Update. Se os dispositivos receberem as atualizações do controlador a partir do Windows Update, quaisquer problemas de controlador identificados como parte da avaliação de prontidão são automaticamente marcados como **Ready**.  

- Baixo limiar de contagem de instalações para as suas aplicações Windows. Se uma aplicação for instalada numa percentagem mais elevada de computadores do que este limiar, o plano de implementação marca a aplicação como **Noteworthy**. Esta etiqueta significa que pode decidir a importância da aplicação para testar durante a fase piloto.  


## <a name="plan-assets"></a>Plano de ativos

<!-- 4670224 -->

Embora a área [de Ativos](about-assets.md) também mostre dispositivos e aplicações, a área de ativos do **Plano** ao abrigo de um plano de implementação específico inclui informações adicionais.

### <a name="devices"></a>Dispositivos

Consulte a decisão de upgrade do **Windows** para cada dispositivo no plano de implementação.

A decisão de **atualização** do Windows para substituir o dispositivo pode ser devido a uma das seguintes razões:

- Falhou uma verificação necessária do processador do Windows 10. Para mais informações, consulte [os requisitos mínimos](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor)de hardware .
- Tem um bloco BIOS
- Não tem memória suficiente.
- Um componente crítico da bota no sistema tem um controlador bloqueado
- A característica e modelo específicos não conseguem atualizar
- Há um componente de classe de exibição com um bloco de condutor que tem todos os seguintes atributos:
    - Não se sobressapara.
    - Não há condutor na nova versão do SO
    - Ainda não está no Windows Update
- Há outro componente plug-and-play no sistema que bloqueia a atualização
- Há um componente sem fios que usa um condutor emulado xP
- Um componente de rede com uma ligação ativa perderá o seu condutor. Por outras palavras, após a atualização, pode perder a conectividade da rede.

A decisão **de atualização** do Windows para reinstalar indica que a atualização necessitará de uma reinstalação em oposição a uma atualização no local. 

Uma decisão de atualização **bloqueada** do Windows pode ser causada pelas seguintes razões:

- Define a decisão de atualização de um ou mais ativos para **Inable**.

- Os dados de inventário desse dispositivo estão incompletos e o Desktop Analytics não pode fazer uma avaliação completa da compatibilidade.

### <a name="apps"></a>Aplicações

Detete a decisão de **Upgrade** e a **Importância** para esta aplicação neste plano de implementação. Para mais informações, consulte [como criar planos de implantação](create-deployment-plans.md).

Nos detalhes da aplicação, pode também ver as seguintes informações: Recomendações, fatores de risco de compatibilidade e problemas conhecidos da Microsoft. Utilize estas informações para ajudar a definir a **decisão de upgrade**. Para mais informações, consulte a avaliação da [compatibilidade.](compat-assessment.md)

As aplicações que o Desktop Analytics mostra como *notáveis* baseiam-se no baixo limiar de contagem de instalações para as regras de prontidão do plano de implementação. Para mais informações, consulte [as regras de prontidão](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Para obter mais informações sobre a categoria de aplicações "Não importantes", consulte a [decisão de atualização automática do sistema e as aplicações de loja](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>Controladores

Consulte a lista de condutores incluídos neste plano de implantação. Desdefinir a **decisão de upgrade,** rever a recomendação da Microsoft e ver fatores de risco de compatibilidade.


## <a name="importance"></a>Importância

Como parte do plano de implementação, delineie a *importância* das aplicações. O Desktop Analytics deteta estas aplicações como instaladas nos dispositivos-alvo. Esta definição ajuda o Desktop Analytics a determinar quais os dispositivos que inclui na fase piloto da implementação.

Se uma aplicação for instalada em menos de 2% dos dispositivos visados, está marcada **a contagem de instalações Low**. Dois por cento é o valor padrão. Pode ajustar o limiar nas definições de prontidão de 0% a 10%. Desktop Analytics marca automaticamente estas aplicações como **Prontas a atualizar**.  

Para aplicações, escolha uma importância de **Critical**, **Important**, ou **Não importante.** Se marcar um como crítico ou importante, o Desktop Analytics inclui na implementação do piloto alguns dispositivos com essa aplicação. O serviço inclui no piloto mais instâncias de uma aplicação crítica. Se marcar uma aplicação como não importante, o Desktop Analytics automaticamente a define para **Ready to upgrade**.



## <a name="pilot-devices"></a>Dispositivos-piloto

Desktop Analytics combina a sua informação de importância com as configurações piloto globais. Cria então uma recomendação para a qual os dispositivos devem fazer parte da implantação do piloto. A implementação do piloto recomendado inclui dispositivos com diferentes configurações de hardware e um ou mais casos de todas as aplicações críticas e importantes. Se uma aplicação for marcada como crítica, o serviço recomenda mais dispositivos com essa aplicação no piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planos de implementação em Gestor de Configuração

Depois de criar um plano de implementação, utilize o Gestor de Configuração para implementar os produtos. Assim que a implementação começa, o Desktop Analytics monitoriza a implementação com base nas definições do plano.


## <a name="next-steps"></a>Passos seguintes

- [Conheça os ativos do Desktop Analytics](about-assets.md): dispositivos, controladores e apps  

- [Conheça a segurança e atualizações de funcionalidades](about-updates.md)  

- [Criar um plano de implantação](create-deployment-plans.md)  
