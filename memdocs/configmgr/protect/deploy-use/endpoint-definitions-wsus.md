---
title: Definições de malware de proteção de ponto final da WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Saiba como configurar os Serviços de Atualizações do Windows Server para aprovar automaticamente atualizações de definição.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126027"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Ativar definições de malware endpoint protection para baixar de WSUS para Gerente de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Se utilizar o WSUS para manter as definições de antimalware atualizadas, pode configurá-lo para aprovar automaticamente as atualizações de definições. Embora utilizar atualizações de software do Gestor de Configuração seja o método recomendado para manter as definições atualizadas, também pode configurar o WSUS como um método para permitir aos utilizadores atualizarmanualmente definições. Utilize os procedimentos seguintes para configurar o WSUS como uma origem de atualização de definições.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Sincronizar atualizações de definição para O Gestor de Configuração

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda a **Configuração do Site,** e depois selecione **Sites**.

1. Selecione o site que contém o ponto de atualização de software. No grupo **Definições** da fita, **selecione Configurar componentes**do site , e, em seguida, selecione **Software Update Point**.

1. Na janela propriedades do componente de ponto de atualização de **software,** mude para o separador **Classificações.** Selecione **Atualizações de Definição**.

1. Para especificar os **Produtos atualizados** com a WSUS, mude para o separador **Produtos.**

    - Para o Windows 10 e mais tarde: No Microsoft > Windows, selecione **Windows Defender**.

    - Para o Windows 8.1 e anterior: Sob a > Frontação da Microsoft, selecione **System Center Endpoint Protection**.

1. Selecione **OK** para fechar a janela Propriedades do Componente de Ponto de Atualização de **Software.**

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Sincronizar atualizações de definição para WSUS autónomo

Utilize o seguinte procedimento para configurar atualizações de proteção de pontos finais quando o seu servidor WSUS não estiver integrado no ambiente do Gestor de Configuração.

1. Na consola de administração WSUS, expanda **os Computadores,** selecione **Opções**e, em seguida, selecione **Produtos e Classificações**.

1. Para especificar os **Produtos atualizados** com a WSUS, mude para o separador **Produtos.**

    - Para o Windows 10 e mais tarde: No Microsoft > Windows, selecione **Windows Defender**.

    - Para o Windows 8.1 e anterior: Sob a > Frontação da Microsoft, selecione **System Center Endpoint Protection**.

1. Mude para o separador **Classificações.** Selecione Atualizações e **Atualizações**de **Definição** .

## <a name="approve-definition-updates"></a>Aprovar atualizações de definição

As atualizações de definição de proteção de pontos finais devem ser aprovadas e descarregadas para o servidor WSUS antes de serem oferecidas aos clientes que solicitem a lista de atualizações disponíveis. Os clientes ligam ao servidor WSUS para verificar se existem atualizações aplicáveis e, em seguida, solicitam as atualizações de definições aprovadas mais recentes.

### <a name="approve-definitions-and-updates-in-wsus"></a>Aprovar definições e atualizações no WSUS

1. Na consola de administração WSUS, selecione **Atualizações**. Em seguida, selecione **Todas as Atualizações** ou a classificação das atualizações que pretende aprovar.

1. Na lista de atualizações, clique na atualização ou atualizações que pretende aprovar para instalação e, em seguida, selecione **'Aprovar**' .

1. Na janela **'Actualizações',** selecione o grupo de computador para o qual pretende aprovar as atualizações e, em seguida, **selecione Aprovado para Instalação**.

### <a name="configure-an-automatic-approval-rule"></a>Configure uma regra de aprovação automática

Também pode definir uma regra de aprovação automática para atualizações de definição e atualizações de Proteção de Pontofinal. Esta ação confunde a WSUS para aprovar automaticamente as atualizações de definição de proteção de pontos finais descarregadas pela WSUS.

1. Na consola de administração WSUS, selecione **Opções**, e, em seguida, selecione **Aprovações Automáticas**.

1. No separador Regras de **Atualização,** selecione **Nova Regra**.

1. Na janela **Regra de Adição,** em **passo 1: Selecione propriedades,** selecione a opção: **Quando uma atualização estiver numa classificação específica**.

    1. Sob **o passo 2: Editar as propriedades,** selecione **qualquer classificação**.

    1. Limpe todas as opções, exceto Atualizações de **Definição,** e, em seguida, selecione **OK**.

1. Na janela **Regra de Adição,** em **passo 1: Selecione propriedades,** selecione a opção: **Quando uma atualização estiver num produto específico**.

    1. Sob **o passo 2: Editar as propriedades,** selecione **qualquer produto**.

    1. Limpe todas as opções, exceto **a Proteção do Ponto final** do System Center para o Windows 8.1 e anterior ou Windows **Defender** para windows 10 e posteriormente. Em seguida, selecione **OK**.

1. Segundo **o passo 3: Especifique um nome,** introduza um nome para a regra e, em seguida, selecione **OK**.

1. Na caixa de diálogo **de aprovações automáticas,** selecione a regra recém-criada e, em seguida, selecione a **regra executar**.

> [!NOTE]
> Para maximizar o desempenho no seu servidor WSUS e computadores cliente, recuse atualizações de definições antigas. Para realizar esta tarefa, pode configurar a aprovação automática de revisões e a recusa automática de atualizações expiradas. Para mais informações, consulte o [artigo 938947](https://support.microsoft.com/kb/938947)do Microsoft Support .

> [!div class="nextstepaction"]
> [Criar e implementar políticas antimalware](endpoint-antimalware-policies.md)
