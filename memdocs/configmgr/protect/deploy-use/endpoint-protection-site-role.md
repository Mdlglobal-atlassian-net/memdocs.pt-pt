---
title: Criar a função do sistema de sistema de pontos de proteção do ponto final
titleSuffix: Configuration Manager
description: Saiba como configurar a Proteção de Pontofinal para gerir a segurança e malware nos computadores clientes do Gestor de Configuração.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710833"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Criar uma função de sistema de sites do ponto do Endpoint Protection

*Aplica-se a: Gestor de Configuração (ramo atual)*

A função de sistema de sites de ponto do Endpoint Protection tem de ser instalada antes de poder utilizar o Endpoint Protection. Tem de ser instalada apenas num servidor do sistema de sites e tem de ser instalada na parte superior da hierarquia num site de administração central ou num site primário autónomo.

Utilize um dos seguintes procedimentos dependendo se pretende instalar um novo servidor de sistema de site para proteção de pontos finais ou utilizar um servidor de sistema de site existente:
- [Instalar num novo servidor de sistema de site](#new-site-system-server)
- [Instalar num servidor de sistema de site existente](#existing-site-system-server)

> [!IMPORTANT]
>  Quando instala um ponto de proteção de ponto final, um cliente de Proteção de Pontofinal é instalado no servidor que acolhe o ponto de proteção do ponto final. Os serviços e análises estão desativados neste cliente para permitir que coexista com qualquer solução antimalware existente que esteja instalada no servidor. Se posteriormente ativar este servidor para gestão pela Endpoint Protection e selecionar a opção de remover qualquer solução antimalware de terceiros, o produto de terceiros não será removido. Tem de desinstalar este produto manualmente.

## <a name="new-site-system-server"></a>Novo servidor do sistema de sites

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Servidores e Funções de Sistema de Sites**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**.

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.

5.  Na página **Seleção da Função do Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Seguinte**.

6.  Na página **Endpoint Protection** , selecione a caixa de verificação **Aceito os termos de licenciamento do Endpoint Protection** e clique em **Seguinte**.

    > [!IMPORTANT]
    >  Não pode utilizar a Proteção de Pontofinal no Gestor de Configuração a menos que aceite os termos da licença.

7.  Na página do Serviço de Proteção de **Nuvem,** selecione o nível de informação que pretende enviar para a Microsoft para ajudar a desenvolver novas definições e, em seguida, clique em **Next**.

    > [!NOTE]
    >  Esta opção configura as definições do Serviço de Proteção de Nuvem (anteriormente conhecida como Microsoft Ative Protection Service ou MAPS) que são utilizadas por padrão. Em seguida, pode configurar definições personalizadas para cada política antimalware que criar. Junte-se ao Serviço de Proteção de Nuvem, para ajudar a manter os seus computadores mais seguros, fornecendo à Microsoft amostras de malware que podem ajudar a Microsoft a manter as definições antimalware mais atualizadas. Além disso, quando se junta ao Serviço de Proteção de Nuvem, o cliente Endpoint Protection pode utilizar o serviço de assinatura dinâmica para descarregar novas definições antes de serem publicadas no Windows Update. Para mais informações, consulte [Como criar e implementar políticas antimalware para proteção de pontos finais](endpoint-antimalware-policies.md).

8.  Conclua o assistente.


## <a name="existing-site-system-server"></a>Servidor de sistema de site existente

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  No espaço de trabalho **da Administração,** expanda a Configuração do **Site,** clique em **Servidores e Funções**do Sistema do Site, e, em seguida, selecione o servidor que pretende utilizar para proteção de pontofinal.

3.  No separador **Home Page** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Sites**.

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.

5.  Na página **Seleção da Função do Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Seguinte**.

6.  Na página **Endpoint Protection** , selecione a caixa de verificação **Aceito os termos de licenciamento do Endpoint Protection** e clique em **Seguinte**.

    > [!IMPORTANT]
    >  Não pode utilizar a Proteção de Pontofinal no Gestor de Configuração a menos que aceite os termos da licença.

7.  Na página do Serviço de Proteção de **Nuvem,** selecione o nível de informação que pretende enviar para a Microsoft para ajudar a desenvolver novas definições e, em seguida, clique em **Next**.

    > [!NOTE]
    >  Esta opção configura as definições do Serviço de Proteção de Nuvens (anteriormente conhecida como MAPS) que são utilizadas por padrão. Pode configurar definições personalizadas para cada política antimalware que configurar. Para mais informações, consulte [Como criar e implementar políticas antimalware para proteção de pontos finais](endpoint-antimalware-policies.md).

8.  Conclua o assistente.
