---
title: Definições de malware de proteção de ponto final
titleSuffix: Configuration Manager
description: Aprenda a configurar atualizações de software do Gestor de Configuração para fornecer atualizações de definição aos computadores dos clientes.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126082"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Utilize o Gestor de Configuração para fornecer atualizações de definição

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode configurar atualizações de software do Gestor de Configuração para fornecer automaticamente atualizações de definição aos computadores dos clientes. Antes de começar a criar regras de implementação automáticas, certifique-se de configurar as atualizações de software do Gestor de Configuração. Para mais informações, consulte [Introdução a atualizações de software](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Este procedimento é específico para a Proteção do Ponto Final. Para obter informações mais gerais sobre as regras de implementação automática, consulte [a implementação automática](../../sum/deploy-use/automatically-deploy-software-updates.md)de atualizações de software .

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **atualizações**de software e, em seguida, selecionar **regras de implementação automáticas**.

1. No separador **Home** da fita, no grupo **Criar,** selecione Criar regra de **implantação automática**.

1. Na página **General** do **Assistente de Criação de Regra de Implementação Automática**, especifique as seguintes informações:

    - **Nome**: introduza um nome exclusivo para a regra de implementação automática.

    - **Recolha**: Selecione a recolha do dispositivo para a qual pretende implementar atualizações de definição.

        > [!NOTE]
        > Não é possível implementar atualizações de definição para uma coleção de utilizadores.

1. **Selecione Adicionar a um grupo de atualização**de software existente .

1. Selecione **Ativar a implementação depois de executada esta regra**.

1. Na página **definições** de implementação do assistente, para o **nível de detalhe,** selecione **apenas mensagens de erro**.

    > [!NOTE]
    > Ao selecionar **Apenas mensagens**de erro, reduz o número de mensagens estatais que a implementação de definição envia. Esta configuração ajuda a reduzir o processamento do CPU nos servidores do Gestor de Configuração.

1. Na página **de Atualizações** de Software:

    1. Selecione o filtro de propriedade **'Atualização classificação'.** Na lista de **critérios** de pesquisa, selecione **<itens para encontrar\>**.

        Na janela **Critérios** de Pesquisa, selecione **Atualizações de Definição**e, em seguida, selecione **OK**.

    1. Selecione o filtro de propriedade **do Produto.** Na lista de **critérios** de pesquisa, selecione **<itens para encontrar\>**.

        Na janela **Critérios** de Pesquisa, selecione **System Center Endpoint Protection** para Windows 8.1 e anterior ou Windows **Defender** para windows 10 e, mais tarde, selecione **OK**.

    > [!NOTE]
    > Opcionalmente, pode filtrar atualizações supersed. Selecione o filtro de propriedade **Superseded.** Na lista de **critérios** de pesquisa, selecione **<itens para encontrar\>**. Na janela Critérios de **Pesquisa,** selecione **Não,** em seguida, selecione **OK**.

1. Na página **de Programação** de Avaliação do assistente, selecione **Executar a regra após qualquer sincronização**do ponto de atualização de software .

1. Na página **Agenda de Implementação** do assistente, configure as seguintes definições:

    - **Tempo baseado em**: Se quiser que todos os clientes instalam as definições mais recentes ao mesmo tempo, selecione **UTC**. O tempo real de instalação variará dentro de duas horas.

    - **Tempo disponível**para o software : Especifique o tempo disponível para a implementação que esta regra cria. A hora especificada tem de ser, pelo menos, uma hora após a execução da regra de implementação automática. Esta configuração garante que o conteúdo tem tempo suficiente para se replicar aos pontos de distribuição. Algumas atualizações de definições também podem incluir atualizações de motores antimalware, que podem demorar mais tempo a chegar aos pontos de distribuição.

    - **Prazo de instalação**: selecione **Logo que possível**.

        > [!NOTE]
        > Os prazos de atualização de software variam ao longo de um período de duas horas. Este comportamento impede todos os clientes de solicitarem uma atualização ao mesmo tempo.

1. Na página experiência do **utilizador** do assistente, para notificações do **Utilizador,** selecione Ocultar no Centro de **Software e todas as notificações**. Com esta configuração, as atualizações de definição instalam-se silenciosamente.

1. Na página pacote de **implementação** do assistente, selecione um pacote de implementação existente ou crie um novo.

    > [!NOTE]
    > Considere colocar atualizações de definição num pacote que não contenha outras atualizações de software. Esta estratégia mantém o tamanho do pacote de atualizações de definições mais pequeno, o que lhe permite replicar para pontos de distribuição mais rapidamente.

1. Se criar um novo pacote de implementação, na página **pontos** de distribuição do assistente, selecione um ou mais pontos de distribuição. O site copia o conteúdo deste pacote para estes pontos de distribuição.

1. Na página **Descarregamento,** selecione **descarregue as atualizações de software a partir da Internet**.

1. Na página Escolha de **Idiomas,** selecione cada versão idioma das atualizações para descarregar.

1. Na página Definições de **Descarregamento,** selecione o comportamento de descarregamento de atualizações de software necessário.

1. Conclua o assistente.

Verifique se o nó de Regras de **Implementação Automática** da consola do Gestor de Configuração apresenta a nova regra.

> [!div class="nextstepaction"]
> [Criar e implementar políticas antimalware](endpoint-antimalware-policies.md)
