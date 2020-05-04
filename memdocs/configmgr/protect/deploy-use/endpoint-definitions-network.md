---
title: Baixar definições a partir de uma partilha de rede
titleSuffix: Configuration Manager
description: Saiba como descarregar manualmente as atualizações de definição mais recentes da Microsoft e, em seguida, configurar os clientes para descarregar estas definições.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715684"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Ativar definições de malware endpoint protection para descarregar a partir de uma partilha de rede

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Pode transferir manualmente as atualizações de definições mais recentes da Microsoft e, em seguida, configurar os clientes para transferirem estas definições a partir de uma pasta partilhada na rede. Os utilizadores também podem iniciar atualizações de definições quando utiliza esta origem de atualização.

> [!NOTE]
>  Os clientes têm de ter acesso de leitura à pasta partilhada para conseguirem transferir as atualizações de definições.

 Para obter mais informações sobre como descarregar a definição e as atualizações do motor para armazenar na partilha de ficheiros, consulte [Instalar o mais recente software antimalware e antispyware](https://www.microsoft.com/wdsi/definitions)da Microsoft.

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar transferências de definições a partir de uma partilha de ficheiros

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Predefinida** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [como criar e implementar políticas antimalware para proteção de endpoint](endpoint-antimalware-policies.md).

4.  Na secção de **atualizações** da Inteligência de Segurança da caixa de diálogo de propriedades antimalware, clique em **set Source**.
    - A secção de **atualizações** de Definição foi renomeada para **atualizações de Inteligência** de Segurança a partir da versão 1902 do Gestor de Configuração.

5.  Na caixa de diálogo **Configurar Origens de Atualização da Definição** , selecione **Atualizações a partir de partilhas de ficheiros UNC**.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização da Definição** .

7.  Clique em **Definir Caminhos**. Em seguida, na caixa de diálogo **Configurar Caminhos UNC de Atualização da Definição** , adicione um ou mais caminhos UNC para a localização dos ficheiros de atualizações de definições numa partilha de rede.

8.  Clique em **OK** para fechar a caixa de diálogo **Configurar Caminhos UNC de Atualização da Definição** .


> [!div class="button"]
> [Próximo passo >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [>de volta](endpoint-configure-alerts.md)
