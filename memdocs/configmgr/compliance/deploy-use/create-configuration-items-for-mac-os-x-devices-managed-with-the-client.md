---
title: 'Criar itens de configuração para Macs geridos pelo cliente '
titleSuffix: Configuration Manager
description: Utilize o item de configuração Do Gestor de Configuração Mac OS X para gerir as definições dos dispositivos Mac OS X.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 219ddd4c828cdabd022deb9fe372718184a4c024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713024"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Criar itens de configuração para dispositivos Mac OS X
Utilize o artigo de configuração Do Gestor de Configuração **Mac OS X (personalizado)** para gerir as definições para dispositivos Mac OS X que são geridos pelo cliente do Gestor de Configuração.  
  
O sistema operativo Mac OS X utiliza ficheiros da lista de propriedades (.plist) para armazenar as definições de aplicação. Utilize as definições de compatibilidade para avaliar e corrigir as definições num ficheiro de lista de propriedades. Também pode gerir as definições do Mac OS X escrevendo um script de concha que devolve um valor que pode avaliar e remediar para a conformidade.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Crie um item de configuração Personalizado Mac OS X  
  
1. Na consola 'Gestor de Configuração', selecione **Ativos e conformidade.**  
  
2. No espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e, em seguida, selecione Itens de **Configuração**.  
  
3. No separador **Home,** no grupo **Criar,** selecione **Create Configuration Item**.  
  
4. Na página **geral** do assistente de **configuração criar,** especifique um nome e descrição opcional para o item de configuração.  
  
5. Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Mac OS X (personalizado)**.  
  
6. Se criar e atribuir categorias para ajudá-lo a pesquisar e filtrar itens de configuração na consola do Gestor de Configuração, selecione **Categorias**.  
  
7. Na página **Plataformas Suportadas** do assistente, selecione as versões do Mac OS X específicas que irão avaliar o item de configuração.  
  
8. Na página **Definições** do assistente, adicione novas definições que são avaliadas para a conformidade nos computadores Mac. Selecione **Novo** para abrir a caixa de diálogo **Create Definição.**  
  
9. Na caixa de diálogo **Criar Definição**, introduza um nome único e uma descrição para a definição.  
  
10. Escolha o **tipo Definição** que deseja e, em seguida, forneça as informações necessárias:  
  
    -   **Preferências do Mac OS X**  
  
        -   **ID da aplicação**: Especifique o ID de aplicação do ficheiro da lista de propriedades a partir do qual pretende avaliar uma chave para o cumprimento.  
  
             Por exemplo, se pretender editar as definições do browser Safari, poderá utilizar **com.apple.Safari.plist**.  
  
        -   **Chave**: Especifique o nome da chave que pretende avaliar para a conformidade dos computadores Mac. Utilize a sintaxe */<dictionary\>/<keyname\>*.  
  
            > [!IMPORTANT]  
            >  O nome chave é sensível ao caso, e não será avaliado se difere do nome chave no computador Mac. Além disso, não pode editar o nome chave depois de o ter especificado. Se precisar de editar o nome-chave, elimine e recrie a definição.  
  
    -   **Script**  
  
        -   **Discovery Script**: Selecione **Adicionar script**, e, em seguida, introduza um script de concha para avaliar as definições no computador Mac para a conformidade. Utilize o comando **eco** no script shell para devolver valores ao Gestor de Configuração para o cumprimento. O Gestor de Configuração utiliza os resultados devolvidos no **STDOUT** para avaliar a conformidade.  
  
            > [!IMPORTANT]  
            >  Não inclua o comando de **reinicialização** no guião de descoberta. Como o script de descoberta funciona cada vez que o cliente reinicia, isto faz com que o computador Mac reinicie continuamente.  
  
        -   **Script de reparação (opcional)**: Opcionalmente, selecione **Adicionar Script**, e, em seguida, introduza um script de concha que é usado para remediar quaisquer definições não conformes encontradas nos computadores do cliente Mac.  
  
            > [!IMPORTANT]  
            >  Para garantir que não introduz caracteres de formatação que o computador Mac não consegue interpretar, não utilize cópia e pasta. Em vez disso, escreva o guião.  
  
11. Escolha o **tipo Data**, que é o formato em que a condição devolve os dados antes de ser utilizado para avaliar a definição.  
  
    > [!NOTE]  
    >  O tipo de dados **Vírgula flutuante** suporta apenas três dígitos depois da casa decimal.  
    >   
    >  O Gestor de Configuração não suporta a utilização do tipo de dados **Boolean** para as definições de script de configuração do Conjunto Mac. Em vez disso, detete o tipo de dados para **Integer**, e certifique-se de que o script devolve um valor inteiro.  
  
12. Selecione **OK** para salvar a definição e feche a caixa de diálogo **Create Definição.** Em seguida, continue a adicionar as definições que precisar.  
  
13. Na página Regras de **Conformidade** do assistente, especifique as condições que definem a conformidade de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, esta tem de ter, pelo menos, uma regra de compatibilidade. Selecione **Novo** para adicionar uma nova regra.  
  
14. Na caixa de diálogo **Criar Regra**, forneça as seguintes informações:  
  
    -   **Nome**: Introduza um nome para a regra de conformidade.  
  
    -   **Descrição**: Introduza uma descrição para a regra de conformidade.  
  
    -   **Definição selecionada**: **Selecione Procurar** para abrir a caixa de diálogo **Select Setting.** Selecione a definição para a qual pretende definir uma regra ou selecione **New Setting**. Quando terminar, escolha **Selecionar**.  
  
        > [!TIP]  
        >  Também pode selecionar **Propriedades** para visualizar informações sobre a definição atualmente selecionada.  
  
    -   **Tipo**de regra : Selecione o tipo de regra de conformidade que pretende utilizar:  
  
        -   **Valor**: Crie uma regra que compare o valor devolvido pelo item de configuração com um valor que especifica.  
  
        -   **Existencial**: Crie uma regra que avalie a definição dependendo se existe num dispositivo.  
  
    -   Num tipo de regra de **Valor**, especifique as seguintes informações:  
  
        -   **A definição deve cumprir a seguinte regra**: Selecione um operador e um valor avaliado para o cumprimento da definição selecionada. Pode utilizar os seguintes operadores:  
  
            -   **É igual a**  
  
            -   **Diferente de**  
  
            -   **Maior do que**  
  
            -   **Menos do que**  
  
            -   **Entre as**  
  
            -   **Maior que ou igual a**  
  
            -   **Menor ou igual a**  
  
            -   **Uma das**: Na caixa de texto, especifique uma entrada em cada linha.  
  
            -   **Nenhum de**: Na caixa de texto, especifique uma entrada em cada linha.  
  
        -   **Remediar regras não conformes quando suportadas**: Selecione esta opção se pretender que o Gestor de Configuração remediaautomaticamente as regras não conformes.  
  
            > [!IMPORTANT]  
            >  Só pode remediar regras incompatíveis quando o operador de regra estiver definido como **É igual a**.  
  
        -   **Reportar incumprimento se esta definição não for encontrada**: O item de configuração reporta incumprimento se esta definição não for encontrada no computador Mac.  
  
        -   **Severidade do incumprimento dos relatórios**: Especifique o nível de gravidade reportado se esta regra de conformidade falhar. Os níveis de gravidade disponíveis são:  
  
            -   **Nenhum**: Os computadores que falham nesta regra de conformidade não reportam uma falha nos relatórios do Gestor de Configuração.  
  
            -   **Informação**: Os computadores que falham nesta regra de conformidade reportam uma falha de **informação** para relatórios do Gestor de Configuração.  
  
            -   **Aviso**: Os computadores que falham nesta regra de conformidade reportam uma falha de **aviso** para relatórios do Gestor de Configuração.  
  
            -   **Crítico**: Os computadores que falham nesta regra de conformidade reportam uma falha dos relatórios **críticos** para o Gestor de Configuração.  
  
            -   **Crítico com evento**: Os computadores que falham nesta regra de conformidade reportam uma falha de falha dos relatórios **críticos** para o Gestor de Configuração. O computador cliente Mac também regista este nível de gravidade.  
  
    -   Para um tipo de regra **Existencial**, especifique as seguintes informações:  
  
        -   Escolha qualquer um:  
  
            -   **A definição tem de existir nos dispositivos cliente**  
  
            -   **A definição não pode existir nos dispositivos cliente**  
  
        -   **Severidade do incumprimento dos relatórios**: Especifique o nível de gravidade que é reportado se esta regra de conformidade falhar. Os níveis de gravidade disponíveis são:  
  
            -   **Nenhum**: Os computadores que falham nesta regra de conformidade não reportam uma falha nos relatórios do Gestor de Configuração.  
  
            -   **Informação**: Os computadores que falham nesta regra de conformidade reportam uma falha de **informação** para relatórios do Gestor de Configuração.  
  
            -   **Aviso**: Os computadores que falham nesta regra de conformidade reportam uma falha de **aviso** para relatórios do Gestor de Configuração.  
  
            -   **Crítico**: Os computadores que falham nesta regra de conformidade reportam uma falha dos relatórios **críticos** para o Gestor de Configuração.  
  
            -   **Crítico com evento**: Os computadores que falham nesta regra de conformidade reportam uma falha de falha dos relatórios **críticos** para o Gestor de Configuração. O computador cliente Mac também regista este nível de gravidade.  
  
        > [!NOTE]  
        >  As opções apresentadas podem variar, dependendo do tipo de definição para o que está a configurar uma regra.  
  
15. Selecione **OK** para fechar a caixa de diálogo **'Criar Regra'.**  
  
16. Na página **Resumo,** confirme as definições para o novo item de configuração. Então, completa o feiticeiro.  
  
Consulte o novo item de configuração no nó de Itens de **Configuração** do espaço de trabalho **De Ativos e Compliance.**  
  
Se agora pretende adicionar este item de configuração a uma linha de base de configuração, consulte como criar linhas de [base de configuração](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Passos seguintes

 [Itens de configuração para dispositivos geridos com o cliente do Gestor de Configuração](../../compliance/deploy-use/create-configuration-items.md)
