---
title: Configurar alertas de proteção de pontofinal
titleSuffix: Configuration Manager
description: Saiba configurar alertas de proteção de pontos finais no Gestor de Configuração.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074865"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configure alertas para proteção de pontofinal no gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Pode configurar alertas de Proteção de Pontofinal no Microsoft Configuration Manager para notificar os utilizadores administrativos quando ocorrerem eventos específicos, como uma infeção por malware na sua hierarquia. As notificações exibem no painel de proteção de pontofinal na consola do Gestor de Configuração no nó de **Alertas** do espaço de trabalho de **monitorização** ou podem ser enviados por e-mail para utilizadores especificados.

 Utilize os seguintes passos e os procedimentos suplementares neste tópico para configurar alertas para a Proteção de Pontos Finais no Gestor de Configuração.

> [!IMPORTANT]
>  Deve ter a permissão de **segurança para** as coleções configurar alertas de proteção de pontos finais.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Passos para configurar alertas para proteção de pontofinal no gestor de configuração

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.

    > [!NOTE]
    >  Não é possível configurar alertas de coleções de utilizadores.

4.  No separador **Alertas** da caixa de diálogo _<Collection\> Name_ **Properties,** selecione Ver esta coleção no painel de proteção de **pontofinal** se quiser ver detalhes sobre operações antimalware para esta recolha no espaço de trabalho de **Monitorização** da consola Do Gestor de Configuração.

    > [!NOTE]
    >  Esta opção não está disponível para a coleção **Todos os Sistemas** .

5.  No separador **Alertas** da caixa de diálogo _<Collection Name\> _ **Properties,** clique em **Adicionar**.

6.  Na caixa de diálogo **Add New Collection Alerts,** na **Geração de um alerta quando estas condições se aplicam,** selecione os alertas que pretende que o Gestor de Configuração gere quando ocorrerem os eventos de proteção de pontofinal especificados e, em seguida, clique em **OK**.

7.  Na lista **de Condições** do separador **Alertas,** selecione cada alerta de proteção do ponto final e, em seguida, especifique as seguintes informações:

    -   **Nome do alerta** - Aceite o nome predefinido ou introduza um novo nome para o alerta.

    -   **Severidade de alerta** - Na lista, selecione o nível de alerta para visualizar na consola 'Gestor de Configuração'.

8.  Dependendo do alerta que selecionar, especifique as seguintes informações adicionais:

    -   **Deteção de malware** - Este alerta é gerado se for detetado malware em qualquer computador da recolha que monitoriza. O **limiar de deteção** de malware especifica os níveis de deteção de malware nos quais este alerta é gerado:

        -   **High - Todas as deteções** - O alerta é gerado quando existem um ou mais computadores na recolha especificada em que qualquer malware é detetado, independentemente da ação que o cliente endpoint Protection tome.

        -   **Médio - Detetado, pendente de ação** - O alerta é gerado quando há um ou mais computadores na recolha especificada em que o malware é detetado, e deve remover manualmente o malware.

        -   **Baixo - Detetado, ainda ativo** - O alerta é gerado quando há um ou mais computadores na recolha especificada em que o malware é detetado e ainda está ativo.

    -   **Surto de malware** - Este alerta é gerado se for detetado malware especificado numa percentagem especificada de computadores na recolha que monitoriza.

        -   **Percentagem de computadores com malware detetado** - O alerta é gerado quando a percentagem de computadores com malware que é detetado na recolha excede a percentagem que especifica. Especifique uma percentagem de **1** a **99**.

            > [!NOTE]
            >  O valor percentual baseia-se no número de computadores na coleção, mas exclui computadores que não tenham um cliente de Gestor de Configuração instalado. Inclui computadores que ainda não têm o cliente endpoint Protection instalado.

    -   **Deteção repetida de malware** - Este alerta é gerado se for detetado malware específico mais do que um número especificado de vezes ao longo de um número especificado de horas nos computadores da recolha que monitoriza. Especifique as seguintes informações para configurar este alerta:

        -   **Número de vezes que o software maligno foi detetado:** - O alerta é gerado quando o mesmo software maligno for detetado em computadores na coleção mais do que o número de vezes especificado. Especifique um número de **2** a **32**.

        -   **Intervalo de deteção (horas):** especifique o intervalo de deteção (em horas) em que o número de deteções de software maligno tem de ocorrer. Especifique um número de **1** a **168**.

    -   **Deteção de vários malwares** - Este alerta é gerado se forem detetados mais do que um número especificado de tipos de malware ao longo de um determinado número de horas em computadores na recolha que monitoriza. Especifique as seguintes informações para configurar este alerta:

        -   **Número de tipos de software maligno detetados:** - O alerta é gerado quando o número especificado de diferentes tipos de software maligno for detetado nos computadores na coleção. Especifique um número de **2** a **32**.

        -   **Intervalo para deteção (horas):** Especifique o intervalo de deteção, em horas, no qual deve ocorrer o número de deteções de malware. Especifique um número de **1** a **168**.

9. Clique **em OK** para fechar a caixa de diálogo<Collection _\> Name_ **Properties.**  

## <a name="alert-for-outdated-malware-client"></a>Alerta para cliente de malware desatualizado

Começando com a versão 1702 do Gestor de Configuração, pode configurar um alerta para garantir que os clientes endpoint Protection não estão desatualizados. De qualquer recolha de dispositivos, pode agora adicionar colunas à lista para os seguintes atributos **Versão antimalware client e** **Endpoint Protection Deployment State**. Por exemplo, na consola navegar para **Assets e Compliance** > **Overview** > **Device Collections** > Todos os**Desktops e Clientes servidores**. Clique no cabeçalho da coluna e selecione as colunas para adicionar. Para verificar se há um alerta, consulte **alertas** no espaço de trabalho **de Monitorização.** Se mais de 20% dos clientes geridos estiverem a executar uma versão expirada do software antimalware, a versão cliente Antimalware é desatualizada. Este alerta não aparece no separador **'Visão Geral** **de Monitorização'.** >  Para atualizar clientes antimalware expirados, ative atualizações de software para clientes antimalware.

Para configurar a percentagem em que o alerta é gerado, expandir**alertas** > de **monitorização** > **Todos os alertas,** clicar em dois **cliques em clientes Antimalware desatualizados** e modificar o **alerta De aumento se a percentagem de clientes geridos com uma versão desatualizada do cliente antimalware for mais do que** opção.

> [!div class="button"]
> [Próximo passo >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [>de volta](endpoint-protection-site-role.md)
