---
title: Saiba mais sobre a segurança do script PowerShell
titleSuffix: Configuration Manager
description: Recursos para ajudar a aprender sobre a segurança do script PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075868"
---
# <a name="learn-more-about-powershell-script-security"></a>Saiba mais sobre a segurança do script PowerShell

*Aplica-se a: Gestor de Configuração (ramo atual)*

É da responsabilidade do administrador validar a utilização proposta de parâmetros PowerShell e PowerShell no seu ambiente. Aqui estão alguns recursos úteis para ajudar a educar os administradores sobre o poder da PowerShell e potenciais superfícies de risco. Isto é para ajudar a mitigar potenciais superfícies de risco e permitir a aplicação de scripts seguros.

## <a name="powershell-script-security"></a>Segurança do Script PowerShell
Incorporado nos Scripts run é uma funcionalidade para rever visualmente e aprovar scripts que são solicitados para serem executados no ambiente. Os administradores devem estar cientes de que os scripts powerShell podem ter obscenizado script: script que é malicioso e difícil de detetar com inspeção visual durante o processo de aprovação do script. Como uma boa prática, usar certas ferramentas de inspeção, adicionais para rever visualmente scripts PowerShell, ajudará a detetar problemas de scripts suspeitos. Estas ferramentas nem sempre conseguem determinar a intenção do autor da PowerShell para que possa chamar a atenção para um script suspeito. No entanto, as ferramentas exigirão que o administrador julgue se é uma sintaxe maliciosa ou intencional.

## <a name="recommendations"></a>Recomendações
- Familiarize-se com as melhores práticas de segurança da PowerShell utilizando os vários links referenciados abaixo.
- **Assine os seus scripts**: Outro método para manter os scripts Seguros é tê-los verificados e depois assinados, antes de os importar para utilização.
- Não guarde segredos (como palavras-passe) em scripts PowerShell e saiba mais sobre como lidar com segredos.


## <a name="general-information-about-powershell-security-best-practices"></a>Informações gerais sobre as melhores práticas de segurança da PowerShell

Esta coleção de links foi escolhida para dar aos administradores do Gestor de Configuração um ponto de partida para aprender sobre as melhores práticas de segurança do script PowerShell.  

[Introdução às Melhores Práticas de Segurança PowerShell](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell Security Best Practices PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defendendo contra ataques powershell, blog da equipa PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Defendendo contra a PowerShell ataca o Twitter, de um microsoft PowerShell e advogado de segurança Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Proteção contra injeção de código malicioso](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell The Blue Team, discute a exploração de blocos de scriptprofundo, registo de eventos protegidos, interface de digitalização antimalware, APIs de geração de código seguro](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Para o Windows 10, existe uma API para uma interface de digitalização anti-malware](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Segurança dos parâmetros PowerShell
Passar parâmetros é uma forma de ter flexibilidade com os seus scripts e adiar decisões até o tempo de execução. Também abre outra superfície de risco. As melhores práticas para prevenir parâmetros maliciosos ou injeção de scriptsão:

- Apenas permita a utilização de parâmetros pré-definidos.
- Utilize a função de expressão regular, para validar os parâmetros que são permitidos.
    - Exemplo: Se for permitido apenas uma certa gama de valores, utilize uma expressão regular para verificar apenas os caracteres ou valores que podem compor a gama.
    - Os parâmetros de validação podem ajudar a evitar que os utilizadores experimentem certos caracteres que podem ser escapados, como citações. Esteja ciente de que pode haver vários tipos de citações, por isso usar expressões regulares para validar quais os caracteres que decidiu serem admissíveis é muitas vezes mais fácil do que tentar definir todas as inputs que não são admissíveis.
- Aproveite o módulo PowerShell ["caçador de injeção"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) na Galeria PowerShell.
    - Pode haver falsos positivos, por isso procure intenção quando algo é sinalizado como suspeito para determinar se é um problema real ou não. 
- O Microsoft Visual Studio tem um analisador de scripts, que pode ajudar a verificar a sintaxe powerShell.
- Este vídeo intitulado: "DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server" dá uma visão geral dos tipos de problemas contra os que pode supor (especialmente a secção 12:20-17:50):    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recomendações ambientais
Recomendações gerais para administradores da PowerShell.
1. Implementar a versão mais recente do PowerShell, como a versão 5 ou superior, incorporada no Windows 10. Em alternativa, pode implementar o Quadro de [Gestão](https://www.microsoft.com/download/details.aspx?id=54616)do Windows . 
2. Ativar e recolher registos PowerShell, incluindo opcionalmente a exploração de eventos protegidos. Incorpore estes registos nas suas assinaturas, caça e fluxos de trabalho de resposta a incidentes.
3. Implementar a Administração Just enough em sistemas de alto valor para eliminar ou reduzir o acesso administrativo ilimitado a esses sistemas.
4. Implemente as políticas de controlo de aplicações do Windows Defender para permitir que as tarefas administrativas pré-aprovadas utilizem a capacidade total da linguagem PowerShell, limitando ao mesmo tempo o uso interativo e não aprovado a um subconjunto limitado da linguagem PowerShell.
5. Implemente o Windows 10 para dar ao seu fornecedor antivírus acesso total a todos os conteúdos (incluindo conteúdo gerado ou desofusado no prazo de execução) processado pelos Anfitriões de Scripting do Windows, incluindo o PowerShell.
