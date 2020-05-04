---
title: Recomendações para a gestão de energia
titleSuffix: Configuration Manager
description: Conheça as recomendações da Microsoft para a gestão de energia no Gestor de Configuração.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715264"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Recomendações para gestão de energia em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as seguintes recomendações para a gestão de energia no Gestor de Configuração.  

## <a name="monitor-at-a-representative-time"></a>Monitor em um momento representativo

A fase de monitorização da gestão de energia fornece-lhe as seguintes informações dos computadores da sua organização:

- Consumo de energia
- Atividade
- Capacidades de gestão de energia
- Impacto ambiental

Escolha um tempo representativo para monitorizar os dispositivos. Por exemplo, a monitorização durante um feriado não fornece um relatório realista sobre o uso de energia do computador.

## <a name="create-a-control-collection"></a>Criar uma coleção de controlo

Crie duas coleções de computadores para o ajudar a monitorizar os efeitos de aplicação de esquemas de energia em computadores. A primeira recolha deve conter a maioria dos computadores aos quais pretende aplicar as definições de potência. A recolha de *controlo* deve conter os restantes computadores. Aplique o plano de gestão de energia necessário à primeira coleção. Em seguida, executar relatórios para comparar o impacto entre as duas coleções.  

## <a name="run-reports-before-you-apply-a-plan"></a>Faça relatórios antes de aplicar um plano

Antes de aplicar um plano de gestão de energia a uma coleção de computadores, execute o relatório Definições de **Energia.** Utilize este relatório para o ajudar a compreender as definições de gestão de energia que já estão configuradas em computadores da coleção. Se aplicar novas definições de gestão de energia aos computadores sem primeiro examinar as definições existentes, poderá aumentar o seu consumo de energia.  

## <a name="exclude-servers"></a>Excluir servidores

A gestão de energia para computadores que executam o Windows Server não é suportada. Adicione servidores a uma coleção e exclua-os da gestão de energia.  

> [!NOTE]
> Embora o Gestor de Configuração não suporte a gestão de energia do Windows Server, ainda recolhe dados de utilização de energia para análise e reporte.

## <a name="exclude-other-computers"></a>Excluir outros computadores

Se tiver computadores que não queira gerir com a gestão de energia, adicione estes computadores a uma coleção de exclusão.  

É melhor excluir da gestão de energia os seguintes tipos de computadores:

- Computadores que têm de permanecer ligados.  

- Computadores que os utilizadores precisam de ligar remotamente.  

- Computadores que não podem usar a gestão de energia.  

- Computadores que tenham a função de sistema de sites de ponto de distribuição.  

- Computadores públicos, tais como computadores de quiosque, ecrãs de informação ou consolas de monitorização onde o computador e o monitor devem ser sempre ligados.  

Para mais informações, consulte a Configuração da [gestão de energia.](configuring-power-management.md)  

## <a name="apply-power-plans-to-a-test-collection"></a>Aplicar planos de energia para uma coleção de teste

Teste sempre o efeito de aplicar um esquema de gestão de energia a uma coleção de teste de computadores antes de aplicar o esquema de energia a uma coleção maior de computadores.  

Quando se exclui um computador da gestão de energia, todas as definições de potência revertem para os seus valores originais. Não é possível reverter as definições de potência individuais para os seus valores originais.  

## <a name="apply-power-plan-settings-individually"></a>Aplicar as definições do plano de energia individualmente

Monitorize o efeito de aplicar cada regulação de potência antes de aplicar a próxima. Este processo assegura-se de que cada definição tem o efeito necessário. Para obter mais informações sobre as definições do plano de energia, consulte as definições do plano de [gestão de energia disponível](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Monitorizar regularmente computadores para múltiplos planos de energia

A gestão de energia inclui um relatório que exibe computadores que têm mais do que um plano de potência aplicado: **Computadores com Múltiplos Planos**de Potência .

Se um computador é membro de várias coleções, cada uma aplica diferentes planos de potência, então aplicam-se os seguintes comportamentos:  

- **Plano de alimentação**: Se aplicar vários valores para as definições de potência num computador, utiliza o valor menos restritivo.  

- **Hora do despertar**: Se aplicar vários tempos de despertar a um computador de secretária, utiliza o tempo mais próximo da meia-noite.  

Para mais informações, consulte [Computadores com múltiplos planos](monitor-and-plan-for-power-management.md#BKMK_Multiple)de energia.  

## <a name="save-or-export-power-management-information"></a>Informação sobre a gestão de energia de poupança ou exportação

Quando executar relatórios durante as fases de monitorização e conformidade, guarde ou exporte os resultados. Guarde os dados para posterior comparação caso o Gestor de Configuração remova mais tarde os dados.  

O Gestor de Configuração mantém na base de dados do site as seguintes informações de gestão de energia:

- Informação de gestão de energia utilizada por relatórios diários: 31 dias

- Informação de gestão de energia utilizada por relatórios mensais: 13 meses
