---
title: Importar e exportar aplicações
titleSuffix: Configuration Manager
description: Aprenda a importar e exportar aplicações no Gestor de Configuração para partilhar entre hierarquias separadas.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710217"
---
# <a name="import-and-export-applications"></a>Importar e exportar aplicações

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o Gestor de Configuração para importar e exportar aplicações entre duas hierarquias. Por exemplo, copiar uma aplicação de um ambiente de teste para um ambiente de produção.

## <a name="export"></a>Exportar

1. Na consola 'Gestor de Configuração', selecione o nó de **Aplicações.** No grupo Criar a fita, escolha Pedido de **Exportação**.
1. No ecrã **Geral,** insira um caminho para um novo ficheiro ZIP para exportar. Opcionalmente, especifique se exporta *dependências, relações de supersedência, condições e ambientes virtuais,* bem como *conteúdo para as aplicações e dependências selecionadas.*  Introduza quaisquer comentários do administrador, se desejar, e selecione **Next**.
1. Verifique se a aplicação e quaisquer dependências estão listadas na página **Objetos Relacionados** e selecione **Next**.
1. Na página Resumo, selecione **Next**.
1. Uma vez concluído o processo, cria o ficheiro ZIP e pode fechar o assistente.

> [!IMPORTANT]
> Se vai copiar esta aplicação para outro ambiente, pegue tanto o ficheiro ZIP como a pasta que a acompanha. O ficheiro ZIP deve existir no mesmo diretório que a pasta criada.

## <a name="import"></a>Importar

> [!NOTE]
> Você só pode importar aplicações de caminhos unc, você não pode importar diretamente do seu disco local.

1. Na consola 'Gestor de Configuração', selecione o nó de **Aplicações.** No grupo Criar a fita, escolha pedido de **importação**.
1. Escolha o ficheiro ZIP que gostaria de importar e selecionar **Next**.
1. A janela de Conteúdo de Ficheiromostra o que acontece quando importa o pedido. Selecione **Seguinte**.
1. Reveja o ecrã resumo e selecione **Next**.
1. Feche o feiticeiro. A aplicação já está disponível no site.

## <a name="see-also"></a>Consulte também
 
Automatizar a importação e exportação de aplicações utilizando a PowerShell.

* [Importação-CMAplicação](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Exportação-CMAplicação](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
