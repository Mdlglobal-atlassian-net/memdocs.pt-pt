---
title: Fazer manutenção a um grupo de servidores
titleSuffix: Configuration Manager
description: A consola 'Gestor de Configuração' fornece alertas e estados para monitorizar as atualizações e a conformidade.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7d6d8bef145e14547e5e6a726a93cb9470b94afd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724329"
---
# <a name="service-a-server-group"></a>Fazer manutenção a um grupo de servidores

*Aplica-se a: Gestor de Configuração (ramo atual)*

>[!IMPORTANT]
> - A partir da versão de 2002 do Diretor de Configuração, os grupos de servidores foram substituídos por grupos de orquestração. Para mais informações, consulte [os grupos de Orquestração.](orchestration-groups.md)
> - As funcionalidades de pré-lançamento são características que estão no Ramo Atual para testes precoces em ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda estão em desenvolvimento ativo e podem receber alterações até saírem da categoria de pré-lançamento. Tem de ligar esta funcionalidade para que esteja disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

Começando na versão 1606 do Configurmanager, pode configurar as definições do grupo de servidores para uma recolha para definir quantas, que percentagem ou em que encomenda os computadores da coleção irão instalar atualizações de software. Também pode configurar scripts PowerShell pré-implantação e pós-implantação para executar ações personalizadas.

Quando implementa atualizações de software para uma coleção que tem configurações de grupo de servidores configuradas, o ConfigurManager determina quantos computadores na coleção podem instalar as atualizações de software a qualquer momento e disponibiliza o mesmo número de bloqueios de implementação. Apenas os computadores que obtêm um bloqueio de implementação iniciarão a instalação de atualização de software. Quando um bloqueio de implementação está disponível, um computador obtém o bloqueio de implementação, instala as atualizações de software e, em seguida, lança o bloqueio de implementação quando a instalação de atualizações de software completa com sucesso. Em seguida, o bloqueio de implantação fica disponível para outros computadores. Se um computador não conseguir lançar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação do grupo do servidor para a recolha.

>[!IMPORTANT]
>Todos os computadores da coleção devem ser atribuídos ao mesmo local.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  
As definições do grupo do servidor estão configuradas nas propriedades para uma recolha de dispositivos. Para servir um grupo de servidores, todos os membros da coleção devem ser atribuídos ao mesmo site. Utilize os seguintes passos para criar uma recolha e configurar as definições do grupo do servidor:
1.  [Crie uma coleção](../../core/clients/manage/collections/create-collections.md) de dispositivos que contenha os computadores do grupo de servidores.  

2.  No espaço de trabalho **de Ativos e Compliance,** clique em Coleções de **Dispositivos,** clique à direita na recolha que contém os computadores no grupo do servidor e, em seguida, clique em **Propriedades**.  

3.  No separador **Geral,** selecione **Todos os dispositivos fazem parte do mesmo grupo de servidores**e, em seguida, clique em **Definições**.  

4.  Na página definições do **Grupo servidor,** especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem de máquinas seja atualizada ao mesmo tempo**: Especifica que apenas uma determinada percentagem de clientes é atualizada a qualquer momento. Se, por exemplo, a coleção tiver 10 clientes, e a coleção estiver configurada para atualizar 30% dos clientes ao mesmo tempo, então apenas 3 clientes irão instalar atualizações de software a qualquer momento.  

    -   **Permitir que uma série de máquinas sejam atualizadas ao mesmo tempo**: Especifica que apenas um certo número de clientes são atualizados a qualquer momento.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes da coleção serão atualizados um de cada vez na sequência que configura. Um cliente só irá instalar atualizações de software depois de o cliente que está à sua frente na lista ter terminado de instalar as suas atualizações de software.  

5.  Especifique se utilizar á função de um script pré-implantação (drenagem do nó) ou de uma script pós-implantação (resumo do nó).  

    > [!WARNING]
    > Os scripts personalizados não são assinados pela Microsoft. É sua responsabilidade manter a integridade destes guiões.

    > [!TIP]  
    > Seguem-se exemplos que pode utilizar em testes para scripts de pré-implantação e pós-implantação que escrevam o tempo atual num ficheiro de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implementar atualizações de software para o grupo de servidores e monitorizar o estado  
Implementa atualizações de software para a recolha do grupo de servidores utilizando o processo típico de implementação. Depois de implementar as atualizações de software, pode monitorizar a implementação da atualização de software na consola 'Gestor de Configuração'.
1.  [Implemente atualizações](manually-deploy-software-updates.md) de software para a coleção do grupo de servidores.   

2.  [Monitorize a implementação da atualização do software](monitor-software-updates.md). Além das vistas padrão de monitorização para a implementação de atualizações de software, o estado de **espera para bloqueio** é apresentado quando um cliente aguarda a sua vez de instalar as atualizações de software. Pode rever o ficheiro UpdatesDeployment.log para obter mais informações.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Limpe os bloqueios de implementação de computadores num grupo de servidores  
Quando um computador não consegue lançar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação do grupo do servidor para a recolha. As fechaduras limpas só quando uma implementação está presa a atualizar computadores na recolha e existem computadores que ainda não estão em conformidade.  
1.  No espaço de trabalho **de Ativos e Compliance,** clique em **Coleções de Dispositivos**e clique na recolha para limpar fechaduras de implementação.  

2.  No separador **Home,** no grupo **de implementação,** clique em **Clear Server Group Deployment Locks**. Quando os clientes não instalaram as atualizações do software e estão a impedir outros clientes de instalarem as suas atualizações de software, os bloqueios de implementação podem ser manualmente apurados.  
