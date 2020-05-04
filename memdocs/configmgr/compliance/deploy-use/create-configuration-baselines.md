---
title: Criar linhas de base de configuração
titleSuffix: Configuration Manager
description: Crie linhas de base de configuração no Gestor de Configuração que pode implementar para uma coleção.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2028974c166e060f445b255db6c5af707725a3f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712926"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Criar linhas de base de configuração no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


As linhas de base de configuração no Gestor de Configuração contêm itens de configuração predefinidos e, opcionalmente, outras linhas de base de configuração. Depois de criar uma linha de base de configuração, pode implementá-la numa coleção, para que os dispositivos nessa coleção a transfiram e avaliem a compatibilidade com a mesma.  

## <a name="configuration-baselines"></a>Linhas de base de configuração

 As linhas de base de configuração no Configurmanager podem conter revisões específicas de itens de configuração ou podem ser configuradas para utilizar sempre a versão mais recente de um item de configuração. Para obter mais informações sobre as revisões do item de configuração, consulte [as tarefas de Gestão para dados](../../compliance/deploy-use/management-tasks-for-configuration-data.md)de configuração .  

 Existem dois métodos que pode usar para criar linhas de base de configuração:  

- Importar dados de configuração de um ficheiro. Para iniciar o **Assistente de Importação de Dados de Configuração**, no nó **Itens de Configuração** ou **Linhas de Base de Configuração** , na área de trabalho **Recursos e Compatibilidade** , clique em **Importar Dados de Configuração**. Para mais informações, consulte os dados de [configuração da Importação](import-configuration-data.md).

- Utilize a caixa de diálogo **Criar Linha de Base de Configuração** para criar uma nova linha de base de configuração.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração

Para criar uma linha de base de configuração utilizando a caixa de diálogo **Create Configuration Baseline,** utilize o seguinte procedimento:  

1. Na consola do Gestor de Configuração, clique em **Ativos e** > **Definições** > de Conformidade **.**  

2. No separador **Base** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3. Na caixa de diálogo **Criar Linha de Base de Configuração** , introduza um nome único e uma descrição para a linha de base de configuração. Pode utilizar um máximo de 255 carateres para o nome e 512 carateres para a descrição.  

4. A lista **Dados de configuração** apresenta todos os itens de configuração ou linhas de base de configuração que estão incluídos nesta linha de base de configuração. Clique em **Adicionar** para adicionar um novo item de configuração ou linha base de configuração à lista. Pode escolher entre os seguintes itens:  

   - **Itens de configuração**  

   - **Atualizações de software**  

   - **Linhas de Base de Configuração**  
     > [!IMPORTANT]
     > Deve limitar cada linha de base de configuração a não mais de 1000 atualizações de software.
5. Utilize a lista **'Change Purpose'** para especificar o comportamento de um item de configuração que selecionou na lista de dados de **Configuração.** Pode selecionar entre os seguintes itens:  

   -   **Requerida**: A linha de base de configuração é avaliada como incompatível se o item de configuração não for detetado num dispositivo cliente. Se for detetado, é avaliado para conformidade  

   -   **Opcional**: O item de configuração só é avaliado para o cumprimento se a aplicação que refere for encontrada nos computadores dos clientes. Se a aplicação não for encontrada, a linha de base de configuração não está marcada como incompatível (apenas aplicável aos itens de configuração da aplicação).  

   -   **Proibido**: A linha de base de configuração é avaliada como incompatível se o item de configuração for detetado nos computadores do cliente (apenas aplicável aos itens de configuração da aplicação).  

   > [!NOTE]
   >  A lista **Alterar Objetivo** só está disponível se tiver clicado na opção **Este item de configuração contém as definições da aplicação** na página **Geral** do **Assistente de Criação de Item de Configuração**.  

6. Utilize a lista **Alterar Revisão** para selecionar uma revisão específica ou a revisão mais recente do item de configuração para avaliar a compatibilidade nos dispositivos cliente ou selecione **Utilizar Sempre Mais Recente** para utilizar sempre a revisão mais recente. Para obter mais informações sobre as revisões do item de configuração, consulte [as tarefas de Gestão para dados](../../compliance/deploy-use/management-tasks-for-configuration-data.md)de configuração .  

7. Para remover um item de configuração da linha de base de configuração, selecione um item de configuração e, em seguida, clique em **Remover**.  

8. A partir da versão 1806, selecione se quiser **aplicar sempre esta linha de base para clientes cogeridos**. Quando verificado, esta linha de base aplicar-se-á mesmo aos clientes que são geridos pela Intune.  Esta exceção pode ser usada para configurar configurações que são exigidas pela sua organização, mas ainda não disponíveis em Intune.

9. Opcionalmente, clique em **Categorias** para atribuir categorias à linha de base para pesquisa e filtragem. 

10. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** e para criar a linha de base de configuração.  

>[!NOTE]
> Modificar uma linha de base existente, como a definição **Aplicar sempre esta linha de base para clientes cogeridos,** irá incrementar a versão de conteúdo de base. Os clientes terão de avaliar a nova versão para atualizar o relatório de base.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a>Incluir linhas de base de configuração personalizadas como parte da avaliação da política de conformidade
<!--3608345-->
*(Introduzido na versão 1910)*

A partir da versão 1910, pode adicionar avaliação das linhas de base de configuração personalizadas como regra de avaliação da política de conformidade. Quando cria ou edita uma linha de base de configuração, tem a opção de **avaliar esta linha de base como parte da avaliação da política de conformidade.** Ao adicionar ou editar uma regra de política de conformidade, tem uma condição chamada **Incluir linhas de base configuradas na avaliação da política**de conformidade . Para dispositivos cogeridos, e quando configura o Intune para obter os resultados da avaliação de conformidade do Gestor de Configuração como parte do estado de conformidade global, esta informação é enviada para a AD Azure. Em seguida, pode usá-lo para acesso condicional aos recursos do seu Office 365. Para mais informações, consulte [Acesso condicional com cogestão.](../../comanage/quickstart-conditional-access.md)

Para incluir as linhas de base de configuração personalizadas como parte da avaliação da política de conformidade, faça o seguinte:

- Criar e implementar uma política de conformidade para uma recolha de utilizadores com uma regra para [**incluir linhas de base configuradas na avaliação da política**](#bkmk_CA)de conformidade.
- [**Selecione Avaliar esta linha de base como parte da avaliação da política de conformidade**](#bkmk_eval-baseline) numa linha de base de configuração implantada para uma recolha de dispositivos.

> [!IMPORTANT]
> Ao direcionar os dispositivos cogeridos, certifique-se de que cumpre os [pré-requisitos de cogestão](../../comanage/overview.md#prerequisites).

### <a name="example-evaluation-scenario"></a>Cenário de avaliação de exemplo

Quando um utilizador faz parte de uma coleção direcionada a uma política de conformidade que inclua a condição de regra **Inclua linhas de base configuradas na avaliação**da política de conformidade, quaisquer linhas de base com a **Avaliação desta linha de base como parte da** opção de avaliação da política de conformidade selecionada que são implementadas para o utilizador ou o dispositivo do utilizador são avaliados para o cumprimento. Por exemplo:

- `User1`faz parte `User Collection 1`de .
- `User1`utilizações `Device1`, `Device Collection 1` que `Device Collection 2`está dentro e .
- `Compliance Policy 1`tem as **linhas de base configuradas incluir na** condição `User Collection 1`da regra da avaliação da política de conformidade e é implantada para .
- `Configuration Baseline 1`tem **Avaliar esta linha de base como parte da avaliação da política de conformidade** selecionada e está implantada para `Device Collection 1`.
- `Configuration Baseline 2`tem **Avaliar esta linha de base como parte da avaliação da política de conformidade** selecionada e está implantada para `Device Collection 2`.

Neste cenário, `Compliance Policy 1` quando avalia `User1` `Device1`para `Configuration Baseline 1` utilização , tanto e `Configuration Baseline 2` são avaliados também.

- `User1`às `Device2`vezes usa.
- `Device2`é membro `Device Collection 2` do `Device Collection 3`e .
- `Device Collection 3`tem `Configuration Baseline 3` implantado para ele, mas **Avaliar esta linha de base como parte da avaliação da política de conformidade** não é selecionado.

Quando `User1` `Device2`as `Configuration Baseline 2` utilizações , `Compliance Policy 1` só é avaliada quando avalia.

> [!NOTE]
><!--5582516-->
> Se a política de conformidade avaliar uma nova linha de base que nunca foi avaliada no cliente antes, pode reportar incumprimento. Isto ocorre se a avaliação de base ainda estiver em execução quando a conformidade é avaliada. Para contornar este problema, clique em Verificar a **conformidade** no Centro de **Software**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>Criar e implementar uma política de conformidade com uma regra de avaliação da política de conformidade de base

1. No espaço de trabalho **de Ativos e Compliance,** expandir **as Definições**de Conformidade e, em seguida, selecionar o nó de **Compliance Polices.**
1. Clique em **Criar política** de conformidade na fita para criar o Assistente de Política de **Conformidade .** 
1. Na página **Geral,** selecione regras de **conformidade para dispositivos geridos com o cliente do Gestor**de Configuração .
   - Os dispositivos devem ser geridos com o cliente do Gestor de Configuração para incluir as linhas de base de configuração personalizadas como parte da avaliação da política de conformidade.
1. Selecione as suas plataformas nas páginas **plataformas suportadas.**
1. Na página **Regras,** selecione **New**, em seguida, selecione as **linhas de base configuradas em** condições de avaliação da política de conformidade.

   ![Incluir linhas de base configuradas na condição de avaliação da política de conformidade](./media/3608345-create-compliance-policy-rule.png)

1. Clique **OK** **e, em** seguida, ao lado para chegar à página **resumo.**
1. Verifique as suas seleções e clique em **Seguinte,** **em seguida, Feche**.
1. No nó compliance **Polices,** clique à direita na política que criou e selecione **Deploy**.
1. Escolha a sua recolha, configurações de geração de alerta e o seu calendário de avaliação de conformidade para a apólice.
1. Clique em **OK** para implementar a política de conformidade.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Selecione uma linha de base de configuração e verifique "Avaliar esta linha de base como parte da avaliação da política de conformidade"

1. No espaço de trabalho **de Ativos e Conformidade,** expanda **as Definições**de Conformidade e, em seguida, selecione o nó de Base de **Configuração.**
1. Clique à direita numa linha de base existente que é implantada para uma coleção de dispositivos e, em seguida, selecione **Propriedades**. Se necessário, pode criar uma nova linha de base.
   - A linha de base deve ser implantada para uma recolha de dispositivos, não para uma recolha de utilizadores.
1. Ativar a Avaliação desta linha de **base como parte da definição de avaliação da política de conformidade.**
   - Para dispositivos cogeridos que tenham Intune como a autoridade de configuração do **Dispositivo,** certifique-se de que sempre é selecionada esta linha de **base mesmo para clientes cogeridos.**
1. Clique **em OK** para guardar as alterações na sua linha de base de configuração.

   ![Caixa de diálogo de propriedades de base de configuração](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Ficheiros de registo para linhas de base de configuração personalizadas como parte da avaliação da política de conformidade

- ComplianceHandler.log
- DefiniçõesAgente.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Passos seguintes

[Importar dados de configuração](import-configuration-data.md)
