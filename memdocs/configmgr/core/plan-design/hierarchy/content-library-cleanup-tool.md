---
title: Ferramenta de limpeza da biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Utilize a ferramenta de limpeza da biblioteca de conteúdos para remover conteúdo órfão que já não está associado a uma implementação do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720220"
---
# <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize a ferramenta de linha de comando de limpeza da biblioteca de conteúdos para remover conteúdo que já não esteja associado a qualquer embalagem ou aplicação num ponto de distribuição. Este tipo de conteúdo é chamado *de conteúdo órfão.* Esta ferramenta substitui versões mais antigas de ferramentas semelhantes lançadas para produtos anteriores do Gestor de Configuração.  

A ferramenta apenas afeta o conteúdo no ponto de distribuição que especifica quando executa a ferramenta. A ferramenta não pode remover o conteúdo da biblioteca de conteúdos no servidor do site.

Encontre **ContentLibraryCleanup.exe** `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` no servidor do site.



## <a name="requirements"></a>Requisitos  

- Apenas colocar a ferramenta contra um único ponto de distribuição de cada vez.  

- Execute-o diretamente no computador que acolhe o ponto de distribuição para limpeza, ou remotamente a partir de outro computador.  

- A conta de utilizador que executa a ferramenta deve ter permissões iguais à função de segurança **do Administrador Completo** no Gestor de Configuração.  



## <a name="modes-of-operation"></a>Modos de funcionamento

Executar a ferramenta nos dois modos seguintes: [E se](#what-if-mode) e [Apagar](#delete-mode).

> [!Tip]  
> Comece com o modo *e se.* Quando estiver satisfeito com os resultados, então execute a ferramenta no modo *de eliminação.*  


### <a name="what-if-mode"></a>O modo e se   

Se não especificar o `/delete` parâmetro, a ferramenta funciona no modo "e se". Este modo identifica o conteúdo que seria eliminado do ponto de distribuição.

- Quando executada neste modo, a ferramenta não elimina quaisquer dados.  

- A ferramenta escreve para as informações do ficheiro de registo sobre o conteúdo que iria eliminar. Não é solicitado que confirme cada possível eliminação.  


### <a name="delete-mode"></a>Eliminar o modo   

Quando executa a `/delete` ferramenta com o parâmetro, a ferramenta funciona no modo de eliminação.

- Quando executado neste modo, o conteúdo órfão que encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.  

- Antes de apagar cada ficheiro, confirme se a ferramenta deve eliminá-lo. Selecione **Y** para sim, **N** para não, ou **Sim para todos** para saltar mais solicitações e apagar todos os conteúdos órfãos.  


### <a name="log-file"></a>Ficheiro de registo

Quando a ferramenta funciona em ambos os modos, cria automaticamente um registo. Ele nomeia o ficheiro de registo com as seguintes informações: 
- O modo em que a ferramenta funciona  
- O nome do ponto de distribuição  
- A data e a hora de funcionamento  

Quando a ferramenta termina, abre automaticamente o ficheiro de registo no Windows. 

Por predefinição, a ferramenta escreve o ficheiro de registo na pasta temporária da conta de utilizador que executa a ferramenta. Esta localização está no computador onde executa a ferramenta, que nem sempre é o alvo da ferramenta. Utilize `/log` o parâmetro para redirecionar o ficheiro de registo para outro local, incluindo uma partilha de rede.



## <a name="run-the-tool"></a>Executar a ferramenta

Para executar a ferramenta: 

1. Abra uma linha de comandos como administrador. Mude o diretório para a pasta que contém **ContentLibraryCleanup.exe**.  

2. Introduza uma linha de comando que inclua os parâmetros de [linha de comando necessários,](#bkmk_params)e quaisquer parâmetros opcionais que queira utilizar.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a>Parâmetros da linha de comando  

Utilize estes parâmetros de linha de comando em qualquer ordem.   

### <a name="required-parameters"></a>Parâmetros necessários

|Parâmetro|Detalhes|
|---------|-------|
| `/dp <distribution point FQDN>`  | Especifique o nome de domínio totalmente qualificado (FQDN) do ponto de distribuição para limpar. |
| `/ps <primary site FQDN>` | *Só é necessário* quando se limpa o conteúdo de um ponto de distribuição num local secundário. A ferramenta liga-se ao local primário dos pais para executar consultas contra o Provedor de SMS. Estas consultas permitem à ferramenta determinar qual o conteúdo que deve estar no ponto de distribuição. Pode então identificar o conteúdo órfão para remover. Esta ligação ao local primário dos pais deve ser feita para pontos de distribuição num local secundário porque os detalhes necessários não estão disponíveis diretamente a partir do local secundário.|
| `/sc <primary site code>`  | *Só é necessário* quando se limpa o conteúdo de um ponto de distribuição num local secundário. Especifique o código do local do local principal dos pais. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Exemplo: Digitalizar e registar o conteúdo que iria apagar (e se)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Exemplo: Digitalizar e registar conteúdo para um DP num site secundário
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Parâmetros opcionais

|Parâmetro|Detalhes|
|---------|-------|
|`/delete`| Utilize este parâmetro quando estiver pronto para apagar o conteúdo do ponto de distribuição. Solicita-lhe antes de apagar o conteúdo. </br></br> Quando não utiliza este parâmetro, os registos da ferramenta resultam em que conteúdo iria eliminar. Sem este parâmetro, não apaga nenhum conteúdo do ponto de distribuição. |
| `/q` | Este parâmetro executa a ferramenta num modo silencioso que suprime todas as solicitações. Estas solicitações incluem quando elimina o conteúdo. Também não abre automaticamente o ficheiro de registo. |
| `/ps <primary site FQDN>` | Opcional apenas quando se limpa o conteúdo de um ponto de distribuição num local primário. Especifique o FQDN do local primário a que o ponto de distribuição pertence. |
| `/sc <primary site code>` | Opcional apenas quando se limpa o conteúdo de um ponto de distribuição num local primário. Especifique o código do site principal a que o ponto de distribuição pertence. |
| `/log <log file directory>` | Especifique a localização onde a ferramenta escreve o ficheiro de registo. Esta localização pode ser uma unidade local ou uma partilha de rede.</br></br> Quando não utiliza este parâmetro, a ferramenta coloca o ficheiro de registo no diretório temporário do utilizador no computador onde a ferramenta funciona.|

#### <a name="example-delete-content"></a>Exemplo: Eliminar conteúdo 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Exemplo: Eliminar conteúdo sem solicitações
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Exemplo: Faça log to local drive
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Exemplo: Iniciar sessão na partilha de rede
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problema conhecido

Quando qualquer embalagem ou implantação falhou, ou estiver em andamento, a ferramenta pode devolver o seguinte erro:`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Não há sobra para esta questão. A ferramenta não consegue identificar ficheiros órfãos de forma fiável quando o conteúdo está em andamento ou falhou a implementação. A ferramenta não lhe permitirá limpar o conteúdo até resolver esse problema.
