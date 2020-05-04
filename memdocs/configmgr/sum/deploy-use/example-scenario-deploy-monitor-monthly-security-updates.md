---
title: Cenário de exemplo para implementar e monitorizar atualizações
titleSuffix: Configuration Manager
description: Como utilizar atualizações de software no Gestor de Configuração para implementar e monitorizar atualizações mensais de software.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714914"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Cenário de exemplo para implementar e monitorizar atualizações mensais de software

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico fornece um cenário de exemplo de como pode usar atualizações de software no 'Configuração Manager' para implementar e monitorizar as atualizações de software de segurança que a Microsoft lança mensalmente.  

 Neste cenário, acompanhamos as ações do administrador de Configuração do Woodgrove Bank. O administrador precisa de criar uma estratégia de implementação de atualização de software com as seguintes condições e requisitos:  

- A implementação ativa de atualizações de software ocorre uma semana após o lançamento das atualizações de software de segurança pela Microsoft, na segunda terça-feira de cada mês. Este evento é normalmente denominado "Patch Tuesday".  

- As atualizações de software são transferidas e configuradas nos pontos de distribuição. Em seguida, uma implementação é testada para um subconjunto de clientes antes que o ConfigMgr Admin implemente totalmente as atualizações de software no seu ambiente de produção.  

- O administrador deve poder monitorizar a conformidade das atualizações de software por mês ou por ano.  

  Este cenário pressupõe que a infraestrutura do ponto de atualização de software já foi implementada. Utilize as seguintes informações para planear e configurar atualizações de software no Configurmanager.  

|Processo|Referência|  
|-------------|---------------|  
|Rever os principais conceitos das atualizações de software.|[Introdução às atualizações de software](../understand/software-updates-introduction.md)|  
|Planear as atualizações de software. Estas informações ajudam a planear considerações em termos de capacidade e a determinar a infraestrutura do ponto de atualização de software, a instalação do ponto de atualização de software, as definições de sincronização e as definições de cliente para atualizações de software.|[Plano para atualizações de software](../plan-design/plan-for-software-updates.md)|  
|Configurar as atualizações de software. Estas informações ajudam a instalar e a configurar pontos de atualização de software na hierarquia e ajudam a configurar e a sincronizar atualizações de software.<br /><br /> Neste cenário, o nosso ConfigMgr Admin configura o calendário de sincronização de atualizações de software a ocorrer na segunda quarta-feira de cada mês para garantir que eles recuperam as mais recentes atualizações de software de segurança da Microsoft.|[Sincronizar atualizações de software](../get-started/synchronize-software-updates.md)|  

 As seguintes secções neste tópico fornecem passos de exemplo para ajudá-lo a implementar e monitorizar atualizações de software de segurança do Gestor de Configuração na sua organização.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>Passo 1: Criar um grupo de atualização de software para a conformidade anual  
 O administrador do Gestor de Configuração cria um grupo de atualização de software que pode ser usado para monitorizar a conformidade de todas as atualizações de software de segurança que lançam em 2016. O administrador executa os passos na tabela seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|A partir do nó de **Atualizações** de Software na consola do Gestor de Configuração, o administrador do Gestor de Configuração adiciona critérios para exibir apenas atualizações de software de segurança que são lançadas ou revistas no ano de 2015 que satisfaçam os seguintes critérios:<br /><br /><ul><li>**Critérios**. Data de Lançamento ou Revisão</li><li>**Condição**: é maior que ou igual à data específica<br />**Valor**: 1/1/2015</li><li>**Critérios**: Classificação da Atualização<br />**Valor**: Atualizações de Segurança</li><li>**Critérios**: Expirou <br />**Valor**: Não</li></ul>|Não existem informações adicionais|
|O Administrador ConfigMgr adiciona todas as atualizações de software filtradas a um novo grupo de atualização de software com os seguintes requisitos:<br /><br /><ul><li>**Nome**: Grupo de Compatibilidade - Atualizações de Segurança da Microsoft 2015</li><li>**Descrição**: atualizações de software|[Adicione atualizações de software a um grupo de atualização](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>Passo 2: Criar uma regra de implementação automática para o mês em curso  
 O administrador do Gestor de Configuração cria uma regra de implementação automática para as atualizações de software de segurança que são lançadas pela Microsoft para o mês em curso. O administrador executa os passos na tabela seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|A ConfigMgr Admin cria uma regra de implantação automática com os seguintes requisitos:<br /><br /><ol><li>No separador **Geral,** o Administrador ConfigMgr configura o seguinte:<br /> <ul><li>Especifica **atualizações mensais** de segurança para o nome.</li><li>Seleciona uma coleção de teste com clientes limitados.</li><li>Seleciona Criar um novo Grupo de **Atualização**de Software .</li><li>Verifica se **a implementação ativa após a execução desta regra** não é selecionada.</li></ul></li><li>No separador Definições de **Implementação,** o Administrador ConfigMgr seleciona as definições predefinidas.</li><li>Na página De atualizações de **software,** o ConfigMgr Admin configura os seguintes filtros de propriedade e critérios de pesquisa:<br /><ul><li>Data de lançamento ou revisão **Último 1 mês**.</li><li>Classificação da atualização **Atualizações de Segurança**.</li></ul></li><li>Na página de **Avaliação,** o Administrador ConfigMgr permite que a regra seja executada com um horário para a **segunda quinta-feira** de cada **mês**.  O Administrador ConfigMgr também verifica que o seu calendário de sincronização está previsto para ser executado na **segunda quarta-feira** de cada **mês.**</li><li>O Administrador ConfigMgr utiliza as definições predefinidas nas páginas de Definições de Implementação, Experiência de Utilizador, Alertas e Definições de Descarregamento.</li><li>Na página do Pacote de **Implementação,** o ConfigMgr Admin especifica um novo pacote de implementação.</li><li>O ConfigMgr Admin utiliza as definições predefinidas nas páginas de Descarregamento de Localização e Seleção de Idiomas.</li></ol>|[Automatically deploy software updates](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>Passo 3: Verifique se as atualizações de software estão prontas para ser implementadas  
 Na segunda quinta-feira de cada mês, o ConfigMgr Admin verifica que as atualizações de software estão prontas a ser implementadas. O administrador executa o seguinte passo.  

|Processo|Referência|  
|-------------|---------------|  
|O ConfigMgr Admin verifica que a sincronização de atualizações de software foi concluída com sucesso.|[Estado de sincronização de atualizações de software](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>Passo 4: Implementar o grupo de atualização de software  
 Depois de o ConfigMgr Admin verificar que as atualizações de software estão prontas a ser implementadas, implementam as atualizações de software. O administrador executa os passos na tabela seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|O ConfigMgr Admin cria duas implementações de teste para o novo grupo de atualização de software. O administrador considera os seguintes ambientes para cada implantação:<br /><br /> **Implantação**do teste de estação de trabalho: a ConfigMgr Admin considera o seguinte para a implantação do teste de estação de trabalho:<br /><br /><ul><li>Especifica uma coleção de implantação que contém um subconjunto de clientes da estação de trabalho para verificar a implantação.</li><li>Refigura as definições de implementação que são adequadas para os clientes da estação de trabalho no seu ambiente.</li></ul><br />**Implementação do teste**do servidor : o ConfigMgr Admin considera o seguinte para a implementação do teste do servidor:<br /><br /><ul><li>Especifica uma coleção de implementação que contém um subconjunto de clientes de servidores para verificar a implementação.</li><li>Configura as definições de implementação que são adequadas para os clientes do servidor no seu ambiente.</li></ul>|[Deploy software updates](deploy-software-updates.md)|  
|O Administrador ConfigMgr verifica que as implementações de testes foram implantadas com sucesso.|[Software atualiza o estado de implementação](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|O ConfigMgr Admin atualiza as duas implementações com novas coleções que incluem as suas estações de trabalho de produção e servidores.|Não existem informações adicionais|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>Passo 5: Monitorizar a conformidade com as atualizações de software implementadas  
 O ConfigMgr Admin monitoriza o cumprimento das suas implementações de atualização de software. O administrador executa o passo na tabela seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|O ConfigMgr Admin monitoriza o estado de implementação de atualizações de software na consola do Gestor de Configuração e verifica os relatórios de implementação de atualizações de software disponíveis a partir da consola.|[Monitorizar atualizações de software](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>Passo 6: Adicionar atualizações mensais de software ao grupo de atualização anual  
 O ConfigMgr Admin adiciona as atualizações de software do grupo de atualização mensal de software ao grupo anual de atualização de software. O administrador executa o passo na tabela seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|O ConfigMgr Admin seleciona as atualizações de software do grupo de atualização mensal de software e adiciona as atualizações de software ao grupo de atualizações de software que foram criados para a conformidade anual. O administrador rastreia a conformidade da atualização de software e cria vários relatórios para a sua gestão.|[Adicione atualizações de software a um grupo de atualização implementado](add-software-updates-to-an-update-group.md)|  

O ConfigMgr Admin concluiu com sucesso a sua implementação mensal para atualizações de software de segurança. O administrador continua a monitorizar e reportar sobre a conformidade da atualização de software para garantir que os clientes no seu ambiente estão dentro dos níveis de conformidade aceitáveis.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>Processo mensal recorrente para implementar atualizações de software  
 Após o primeiro mês em que o nosso ConfigMgr Admin implementa atualizações de software, o administrador executa passos de três a seis para implementar as atualizações mensais de software de segurança lançadas pela Microsoft.  
