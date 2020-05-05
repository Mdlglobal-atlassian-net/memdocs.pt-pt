---
title: Atualização da base de dados de teste
titleSuffix: Configuration Manager
description: Teste atualizar a base de dados do site ao instalar atualizações para O Gestor de Configuração.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719982"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Teste a atualização da base de dados ao instalar uma atualização

*Aplica-se a: Gestor de Configuração (ramo atual)*

As informações neste tópico podem ajudá-lo a executar uma atualização da base de dados de testes antes de instalar uma atualização na consola para o atual ramo do Gestor de Configuração. No entanto, a atualização do teste já não é uma etapa necessária ou recomenda a apenas que a sua base de dados seja suspeita, ou seja modificada por personalizações não explicitamente suportadas pelo Gestor de Configuração.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Preciso fazer uma atualização de teste?
A depreciação deste teste de atualização é possível devido a alterações introduzidas com o ramo atual do Gestor de Configuração. Estas alterações simplificam o processo e a rapidez com que um ambiente de produção pode ser atualizado para versões mais recentes. Este redesenho foi feito para ajudar os clientes a manterem-se atuais com menos risco e menos despesas operacionais na instalação de cada nova atualização.

As alterações são sobre a forma como as atualizações se instalam, incluindo a lógica que automaticamente reverte uma atualização falhada sem a necessidade de executar uma recuperação do site. Estas alterações permitem a utilização da consola para gerir as instalações da atualização e incluem uma opção para voltar a tentar a [instalação de uma atualização falhada](install-in-console-updates.md#bkmk_retry).

> [!TIP]
> Ao atualizar para o ramo atual do Gestor de Configuração a partir de um produto mais antigo, como system center 2012 Configuration Manager, as [atualizações](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test)da base de dados de teste continuam a ser um passo recomendado .

Se ainda planeia testar a atualização de uma base de dados do site quando instalar uma atualização na consola, as seguintes informações complementam as [orientações sobre a instalação de uma atualização na consola](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Prepare-se para executar uma atualização da base de dados de testes  
Antes de instalar uma nova atualização na sua hierarquia, como a atualização 1702, pode testar a atualização da base de dados do seu site.

Para executar o teste de atualização, utilize a Configuração do Gestor de Configuração a partir dos ficheiros de origem [do CD. A mais recente pasta](the-cd.latest-folder.md) de um site que executa a versão do Gestor de Configuração a que está a atualizar. Este requisito significa que para testar a atualização da base de dados para a atualização para 1702:
-   Deve ter pelo menos um site que executa a versão 1702 a partir do qual pode obter esse CD. Última pasta.
-   Se não tiver um site que execute a versão necessária, considere instalar um site em ambiente de laboratório e, em seguida, atualizar esse site para a nova versão. Isto cria o CD. Última pasta com a versão correta dos ficheiros de origem.

O teste de atualização é executado contra uma cópia de segurança da base de dados do seu site que restaurou numa instância separada do Servidor SQL.  Executa a configuração do **CD. Última** pasta com o interruptor de linha de comando **testdbupgrade** para testar a atualização que restaurou a cópia da base de dados. Após a atualização do teste estar concluída, a base de dados atualizada é descartada. Não pode ser utilizado por um site do Gestor de Configuração.

Se uma instalação de atualização falhar, não deverá ser necessário recuperar o site. Em vez disso, pode voltar a tentar a instalação da atualização a partir da consola.

##  <a name="run-the-test-upgrade"></a>Executar a atualização do teste    
1. Utilize a Configuração do Gestor de Configuração e os ficheiros de origem do **CD. A última** pasta de um site que executa a versão a que planeia atualizar.  

2. Copie o **CD. Última** pasta para uma localização na instância Do Servidor SQL que utilizará para executar a atualização da base de dados de teste.

3. Crie uma cópia de segurança da base de dados do site que pretende testar a atualização. Em seguida, restaure uma cópia dessa base de dados para uma instância do Servidor SQL que não acolhe um site do Gestor de Configuração. A instância Do Servidor SQL deve utilizar a mesma edição do SQL Server que a base de dados do seu site.  

4. Depois de restaurar a cópia da base de dados, faça a **configuração** do CD. A última pasta que contém os ficheiros de origem da versão para a a sua atualização. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância Do Servidor SQL que acolhe a cópia da base de dados não for a instância padrão, forneça os argumentos da linha de comando para identificar a instância que acolhe a cópia da base de dados do site.   

   Por exemplo, tem uma base de dados de site com o nome da base de dados *SMS_ABC*. Restaure uma cópia desta base de dados do site para uma instância suportada do Servidor SQL com o nome de instância *DBTest*. Para testar uma atualização desta cópia da base de dados do site, utilize a seguinte linha de comando: **Configuração.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   Pode encontrar Setup.exe no seguinte local nos meios de origem para O Gestor de Configuração: **SMSSETUP\BIN\X64**.  

5. Na instância do SQL Server onde executa o teste de atualização, monitorize o *log ConfigMgrSetup na* raiz da unidade do sistema para progresso e sucesso.  

    Se a atualização do teste falhar, corrija quaisquer problemas relacionados com a falha de atualização da base de dados do site. Em seguida, crie uma nova cópia de segurança da base de dados do site e teste a atualização da nova cópia da base de dados.  



## <a name="next-steps"></a>Passos seguintes
Depois de a atualização da base de dados de teste estar concluída com sucesso, elimine a base de dados atualizada. Não pode ser utilizado por um site do Gestor de Configuração. Em seguida, pode voltar ao seu site ativo e [iniciar a instalação da atualização.](install-in-console-updates.md)
