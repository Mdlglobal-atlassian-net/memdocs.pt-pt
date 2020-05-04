---
title: Configure atualizações de definição
titleSuffix: Configuration Manager
description: Aprenda a selecionar e configurar métodos com endpoint Protection in Configuration Manager para manter as definições antimalware atualizadas nos computadores dos clientes.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715768"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Configurar atualizações de definições para o Endpoint Protection  

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Com a Endpoint Protection in Configuration Manager, pode utilizar qualquer um dos vários métodos disponíveis para manter as definições antimalware atualizadas nos computadores dos clientes na sua hierarquia. As informações contidas neste tópico podem ajudá-lo a selecionar e a configurar estes métodos.

 Para atualizar as definições de antimalware, pode utilizar um ou mais dos seguintes métodos:

- [Atualizações distribuídas pelo Gestor de Configuração](endpoint-definitions-configmgr.md) - Este método utiliza atualizações de software do Gestor de Configuração para fornecer atualizações de definição e motor a computadores da sua hierarquia.

- [Atualizações distribuídas a partir de Serviços de Atualização do Servidor do Windows (WSUS)](endpoint-definitions-wsus.md) - Este método utiliza a sua infraestrutura WSUS para fornecer atualizações de definição e motor aos computadores.

- [Atualizações distribuídas a partir do Microsoft Update](endpoint-definitions-microsoft-updates.md) - Este método permite que os computadores se conectem diretamente ao Microsoft Update para descarregar definições e atualizações do motor. Este método pode ser útil para computadores que não são muitas vezes ligados à rede empresarial.

- [Atualizações distribuídas pelo Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) - Este método irá descarregar atualizações de definição do Microsoft Malware Protection Center.

- [Atualizações de partilhas de ficheiros unc](endpoint-definitions-network.md) - Com este método, pode guardar as mais recentes atualizações de definição e motor para uma parte na rede. Em seguida, os clientes podem aceder à rede para instalar as atualizações.

  Pode configurar várias origens de atualização de definições e controlar a ordem pela qual são avaliadas e aplicadas. Isto é feito na caixa de diálogo **Configurar Origens de Atualização da Definição** quando cria uma política antimalware.

> [!IMPORTANT]
>  Para computadores Windows 10, é necessário configurar a Proteção de Pontofinal para atualizar definições de malware para o Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Como Configurar Origens de Atualização de Definições
 Utilize o procedimento seguinte para configurar as origens de atualização de definições para utilizar para cada política antimalware.

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Predefinida** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [como criar e implementar políticas antimalware para proteção de endpoint](endpoint-antimalware-policies.md).

4.  Na secção de **atualizações** da Inteligência de Segurança da caixa de diálogo de propriedades antimalware, clique em **set Source**.
    - A secção de **atualizações** de Definição foi renomeada para **atualizações de Inteligência** de Segurança a partir da versão 1902 do Gestor de Configuração.

5.  Na caixa de diálogo **Configurar Origens de Atualização da Definição** , selecione as origens a utilizar para atualizações de definições. Pode clicar em **Para cima** ou **Para baixo** para modificar a ordem pela qual estas origens são utilizadas.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização da Definição** .

## <a name="configure-endpoint-protection-definitions"></a>Configure definições de proteção de pontofinal

-   [Atualizações distribuídas pelo Gestor de Configuração](endpoint-definitions-configmgr.md) - Este método utiliza atualizações de software do Gestor de Configuração para fornecer atualizações de definição e motor a computadores da sua hierarquia.

-   [Atualizações distribuídas a partir de Serviços de Atualização do Servidor do Windows (WSUS)](endpoint-definitions-wsus.md) - Este método utiliza a sua infraestrutura WSUS para fornecer atualizações de definição e motor aos computadores.

-   [Atualizações distribuídas a partir do Microsoft Update](endpoint-definitions-microsoft-updates.md) - Este método permite que os computadores se conectem diretamente ao Microsoft Update para descarregar definições e atualizações do motor. Este método pode ser útil para computadores que não são muitas vezes ligados à rede empresarial.

-   Atualizações distribuídas pelo Microsoft Malware Protection Center - Este método irá descarregar atualizações de definição do Microsoft Malware Protection Center.

-   [Atualizações de partilhas de ficheiros unc](endpoint-definitions-network.md) - Com este método, pode guardar as mais recentes atualizações de definição e motor para uma parte na rede. Em seguida, os clientes podem aceder à rede para instalar as atualizações.
