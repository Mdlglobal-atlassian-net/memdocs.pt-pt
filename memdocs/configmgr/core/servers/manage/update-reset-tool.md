---
title: Ferramenta de reposição de atualizações
titleSuffix: Configuration Manager
description: Utilize a ferramenta de reset da atualização para atualizações na consola para O Gestor de Configuração.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720752"
---
# <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações

*Aplica-se a: Gestor de Configuração (ramo atual)*  


Começando com a versão 1706, os sites primários do Gestor de Configuração e os sites da administração central incluem a ferramenta de reset de reset do Gestor de Configuração, **CMUpdateReset.exe**. Utilize a ferramenta para corrigir problemas quando as atualizações na consola têm problemas em descarregar ou replicar. A ferramenta encontra-se na pasta ***\cd.latest\SMSSETUP\TOOLS*** do servidor do site.

Pode utilizar esta ferramenta com qualquer versão do ramo atual que permaneça no suporte.

Utilize esta ferramenta quando uma [atualização na consola](install-in-console-updates.md) ainda não tiver sido instalada e se encontra em estado de falha. Um estado falhado significa que o download da atualização está em andamento, mas preso ou demorando um tempo excessivamente longo. Considera-se que há muito tempo mais do que as suas expectativas históricas de atualização de pacotes de tamanho semelhante. Também pode ser uma falha na replicação da atualização para sites primários infantis.  

Quando executa a ferramenta, esta passa contra a atualização que especifica. Por predefinição, a ferramenta não apaga atualizações instaladas ou descarregadas com sucesso.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
- **Leia** e **escreva** permissões na base de dados do site da administração central e em cada local primário da sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [funções de base](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) de dados fixas na base de dados do Gestor de Configuração de cada site. A ferramenta não interage com sites secundários.
- **Administrador local** no local de alto nível da sua hierarquia.
- **Administrador local** no computador que acolhe o ponto de ligação de serviço.

Precisa do GUIA do pacote de atualização que pretende repor. Para obter o GUID:
  1.   Na consola, vá a Atualizações de **Administração** > **e Manutenção.**
  2.   No painel de visualização, clique na direção de uma das colunas (como **Estado),** em seguida, selecione **O Guia** do Pacote para adicionar essa coluna ao visor.
  3.   A coluna mostra agora o pacote de atualização GUID.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende repor e, em seguida, utilize CTRL+C para copiar essa linha. Se colar a sua seleção copiada a um editor de texto, pode então copiar apenas o GUID para ser utilizado como parâmetro de linha de comando quando executa a ferramenta.

### <a name="run-the-tool"></a>Executar a ferramenta    
A ferramenta deve ser executada no local de alto nível da hierarquia.

Quando executar a ferramenta, utilize parâmetros de linha de comando para especificar:
- O Servidor SQL no site de topo da hierarquia.
- O nome da base de dados do site no site de topo.
- O GUIA do pacote de atualização que pretende repor.

Com base no estado da atualização, a ferramenta identifica os servidores adicionais a que necessita de aceder.   

Se o pacote de atualização estiver em estado de *descarregamento,* a ferramenta não limpa a embalagem. Como opção, pode forçar a remoção de uma atualização descarregada com sucesso utilizando o parâmetro de eliminação da força (Ver parâmetros de linha de comando mais tarde neste tópico).

Depois da ferramenta correr:
- Se um pacote for eliminado, reinicie o serviço SMS_Executive no site de topo. Em seguida, verifique se há atualizações para que possa baixar o pacote novamente.
- Se um pacote não foi apagado, não precisa de tomar qualquer medida. A atualização reinicia e, em seguida, reinicia a replicação ou instalação.

**Parâmetros da linha de comando:**  


|                        Parâmetro                         |                                                       Descrição                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN do Servidor SQL do seu site de topo>** | *Necessário* <br> Especifique o FQDN do Servidor SQL que acolhe a base de dados do site para o site de topo da sua hierarquia. |
|                **-Nome &lt;da base de dados -D>**                 |                          *Necessário* <br> Especifique o nome da base de dados no site de topo.                          |
|                 **-P &lt;Pacote GUIA>**                 |                        *Necessário* <br> Especifique o GUIA para o pacote de atualização que pretende repor.                        |
|           **-I &lt;Nome de instância do Servidor SQL>**           |                    *Opcional* <br> Identifique a instância do SQL Server que acolhe a base de dados do site.                     |
|                       **-FDELETE**                       |                       *Opcional* <br> Eliminação forçada de um pacote de atualização descarregado com sucesso.                        |

**Exemplos:**  
Num cenário típico, pretende repor uma atualização que tenha problemas de descarregamento. O seu SQL Servers FQDN é *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*, e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  ***Executa: CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

Num cenário mais extremo, pretende forçar a eliminação do pacote de atualização problemático. O seu SQL Servers FQDN é *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*, e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  ***Executa: CMUpdateReset.exe -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
