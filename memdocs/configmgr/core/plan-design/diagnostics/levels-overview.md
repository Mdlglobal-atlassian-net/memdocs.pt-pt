---
title: Níveis de dados de utilização de diagnóstico
titleSuffix: Configuration Manager
description: Conheça os níveis de diagnóstico e dados de utilização que o Gestor de Configuração recolhe
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720339"
---
# <a name="levels-of-diagnostic-usage-data"></a>Níveis de dados de utilização de diagnóstico

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração recolhe três níveis de diagnóstico e dados de utilização: **Básico,** **Melhorado,** e **Completo**. Por predefinição, esta funcionalidade está definida no nível Avançado.

> [!IMPORTANT]
> O Gestor de Configuração não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis Básico ou Melhorado. Qualquer recolha desta informação a nível completo não é propositada. Está potencialmente incluído em informações avançadas de diagnóstico, como ficheiros de registo ou fotos de memória. A Microsoft não utiliza estas informações para o identificar, contactar ou desenvolver publicidade.

## <a name="levels"></a>Níveis

### <a name="basic"></a>Básico

O nível Básico inclui dados sobre a sua hierarquia. É necessário ajudar a melhorar a sua experiência de instalação ou upgrade. Estes dados também ajudam a determinar as atualizações do Gestor de Configuração aplicáveis à sua hierarquia.

### <a name="enhanced"></a>Melhorada

O nível melhorado é o padrão após os acabamentos de configuração. Este nível inclui dados recolhidos no nível básico e dados específicos da funcionalidade. Mostra frequência e duração da utilização de diferentes características. Também inclui dados de configurações do cliente do Gestor de Configuração: nome do componente, estado e certas configurações, como intervalos de votação. A informação sobre as atualizações de software é básica no uso da funcionalidade, não inclui dados sobre a conformidade da atualização a este nível.

A Microsoft recomenda este nível porque fornece os dados mínimos para fazer melhorias no produto e no serviço.

Alguns exemplos de dados que este nível não recolhe incluem:

- Nomes de sites, utilizadores, computadores ou outros objetos

- Detalhes de objetos relacionados com a segurança

- Vulnerabilidades como contagens de sistemas que requerem atualizações de software

### <a name="full"></a>Completa

O nível completo inclui todos os dados nos níveis Básico e Melhorado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações avançadas de diagnóstico, como ficheiros do sistema e instantâneos de memória. Estes dados avançados podem incluir informações pessoais existentes na memória ou ficheiros de registo no momento da captura.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Como alterar o nível

Para alterar o nível de recolha de dados, precisa de **modificar** permissões na classe de objetos **do Site.**

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**
1. **Selecione Definições de hierarquia** na fita.
1. Mude para o separador Dados de **Diagnóstico e Utilização** e, em seguida, escolha o nível de dados.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a>Detalhes específicos da versão

Os seguintes artigos detalham os dados específicos que o Gestor de Configuração recolhe a cada nível com cada versão suportada:

- [Dados de diagnóstico e utilização para 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Dados de diagnóstico e utilização para 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Dados de diagnóstico e utilização para 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Dados de diagnóstico e utilização para 1902](levels-of-diagnostic-usage-data-collection-1902.md)
- [Dados de diagnóstico e utilização para 1810](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Perguntas mais frequentes](frequently-asked-questions.md)
