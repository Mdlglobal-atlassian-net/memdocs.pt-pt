---
title: Gerir implementações de alto risco
titleSuffix: Configuration Manager
description: Configure as definições do site de verificação de implementação no Gestor de Configuração para avisar os administradores se criarem uma implementação de alto risco.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719989"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Definições para gerir implementações de alto risco para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração, pode configurar as definições do site de verificação de *implementação.* Estas definições avisam os administradores se criarem uma sequência de tarefas de alto risco. Uma implementação de alto risco é:  

- Uma implementação que é automaticamente instalada  

- Tem a probabilidade de causar resultados indesejados  

Por exemplo, uma sequência de tarefas com um propósito de **Exigido** que implementa um sistema operativo é considerada de alto risco.  

> [!WARNING]
> Se utilizar as implementações pXE e configurar o hardware do dispositivo com o adaptador de rede como o primeiro dispositivo de arranque, estes dispositivos podem iniciar automaticamente uma sequência de tarefas de implementação de SISTEMAS sem interação do utilizador. A verificação de implementação não gere esta configuração. Embora esta configuração possa simplificar o processo e reduzir a interação do utilizador, coloca o dispositivo em maior risco de reimagem acidental.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>Definições de verificação de implementação

Para reduzir o risco de uma implementação indesejada de alto risco, pode configurar limites de tamanho nestas definições de verificação de implementação:  

- **Limites de tamanho**da coleção : Quando criar uma implementação, esconda coleções que incluam mais clientes do que o seu limite.  

  - **Tamanho predefinido**: Quando cria uma implementação, esta definição esconde coleções por padrão que incluem mais clientes do que este limite. Ainda é possível ver estas coleções ao criar a implementação, mas estão escondidas por defeito. O valor predefinido é **de 100**. Para ignorar esta definição, insira um valor de **0**.  

  - **Tamanho máximo**: Quando cria uma implantação, esta definição esconde sempre coleções com mais clientes do que este limite. O valor predefinido é **0,** que ignora esta definição. O valor **Tamanho máximo** tem de ser superior ao valor **Tamanho predefinido** .  

    Por exemplo, define o **tamanho padrão** para 100 e o **tamanho máximo** para 1000. Quando cria uma implementação de alto risco, a janela **Select Collection** apenas exibe coleções que incluem menos de 100 clientes. Se limpar a configuração para ocultar coleções com uma contagem de **membros maior do que a configuração de tamanho mínimo do site,** a janela exibe coleções que incluem menos de 1000 clientes.  

- **Coleções com servidores**do sistema do site : Quando a recolha do alvo inclui um computador com uma função de sistema de site, bloqueie implementações ou exija verificação antes de criar a implementação. Quando uma implementação estiver bloqueada, selecione uma coleção diferente que satisfaça os critérios de verificação de implementação para continuar a criar a implementação.  

> [!NOTE]
> As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não se pode selecionar uma coleção incorporada, como **a All Systems**.  

## <a name="configure-deployment-verification"></a>Configure a verificação de implementação

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** selecione **Sites**e, em seguida, selecione o site principal para configurar.

2. Na fita, selecione **Propriedades**e, em seguida, mude para o separador Verificação de **Implementação.**

3. Configure as [definições](#bkmk_settings) que pretende utilizar e, em seguida, selecione **OK** para guardar a configuração e fechar as propriedades.

## <a name="next-steps"></a>Passos seguintes

[Gerir sequências de tarefas - configurações de alto impacto](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Configurar sites e hierarquias](../deploy/configure/configure-sites-and-hierarchies.md)
