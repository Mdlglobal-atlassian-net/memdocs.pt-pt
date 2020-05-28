---
title: Rever e substituir aplicações
titleSuffix: Configuration Manager
description: Saiba como trabalhar com versões de aplicação do Gestor de Configuração e aplicações de supersede.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343138"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Revise e substitui aplicações no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Neste tópico, aprenderá a trabalhar com versões de aplicação do Gestor de Configuração e como substituir aplicações com uma nova versão.  

##  <a name="application-revisions"></a> Revisões de aplicações  
 Quando faz revisões a uma aplicação ou a um tipo de implementação que está contido numa aplicação, o Gestor de Configuração cria uma nova revisão da aplicação. É possível visualizar o histórico de cada revisão da aplicação. Também é possível ver as suas propriedades, restaurar uma revisão anterior de uma aplicação ou eliminar uma revisão antiga.  

### <a name="to-display-an-application-revision-history"></a>Para visualizar um histórico de revisão da aplicação  

1.  Na consola de Configuração Manager, escolha aplicações de gestão de **Software Library**aplicações da Biblioteca de Software  >  **Application Management**  >  **Applications**e, em seguida, escolha a aplicação que deseja.  

3.  No separador **Home,** no grupo **Aplicação,** escolha **'História de Revisão'** para abrir a caixa de diálogo do Histórico de Revisão de **Aplicações.**  

### <a name="to-view-an-application-revision"></a>Para visualizar uma revisão da aplicação  

1.  Na caixa de diálogo História da Revisão de **Aplicações,** selecione uma revisão da aplicação e, em seguida, escolha **'Ver**' .  

2.  Na caixa de diálogo **Propriedades** , examine as propriedades da aplicação selecionada.  

    > [!NOTE]  
    >  As propriedades da aplicação que são apresentadas são só de leitura.  

3.  Feche a caixa de diálogo **Propriedades** .  

### <a name="to-restore-an-application-revision"></a>Para restaurar uma revisão da aplicação  

1.  Na caixa de diálogo História da Revisão de **Aplicações,** selecione uma revisão da aplicação e, em seguida, escolha **Restaurar**.  

2.  Na caixa de diálogo **Confirmar Revisação restaurar,** escolha **Sim** para restaurar a revisão da aplicação selecionada.  

### <a name="to-delete-an-application-revision"></a>Para eliminar uma revisão da aplicação  

1.  Na caixa de diálogo História da Revisão de **Aplicações,** selecione uma revisão da aplicação e, em seguida, escolha **Eliminar**.  

2.  Na caixa de diálogo de revisão de **aplicações Eliminar,** escolha **Sim**.  

> [!IMPORTANT]  
>  Só é possível eliminar a revisão da aplicação em vigor se a aplicação estiver reformada e não tiver referências.  

##  <a name="application-supersedence"></a> Substituição de aplicações  
 A gestão de aplicações no Gestor de Configuração permite-lhe atualizar ou substituir as aplicações existentes utilizando uma relação de supersedência. Quando substitui uma aplicação, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação superseded e também decidir se deve atualizar ou desinstalar a aplicação supersedantes da instalação da aplicação de substituição. De um modo geral, recomendamos limitar as cadeias de supersedência a cinco níveis de profundidade no máximo.
 
> [!IMPORTANT]  
>  Quando é selecionada a opção para desinstalar o tipo de implementação substituído, não é possível substituir um tipo de implementação por outro que foi implementado num tipo de coleção diferente.  Por exemplo, um tipo de implementação que foi implementado numa coleção de dispositivos não pode ser substituído por um tipo de implementação que foi implementado numa coleção de utilizadores se a opção para desinstalar o tipo de implementação substituído estiver selecionada.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Decidir se é melhor atualizar ou substituir uma aplicação  
 O utilizador especifica se quer atualizar ou substituir uma aplicação na caixa de diálogo **Especificar Relação de Substituição** das propriedades da aplicação. O tipo de substituição depende se seleciona a opção **Desinstalar** na caixa de diálogo:  

-   Se pretender atualizar para uma versão mais recente da mesma aplicação (com o mesmo ID de aplicação), **não** verifique **Desinstalar**.  

-   Se pretende alterar para uma aplicação diferente (com um ID de aplicação diferente), selecione **Desinstalar**. Precisa remover a versão supersed da aplicação.  

### <a name="supersede-dependent-applications"></a>Aplicações dependentes de sobressede  
 Neste exemplo, a **aplicação principal** refere-se à app que está a implementar e que tem as dependências.  

 Pode criar uma relação de substituição que atualize a aplicação dependente para uma nova versão.  

1. Certifique-se de que a nova aplicação dependente e a aplicação dependente estão no mesmo grupo de dependência da aplicação global.  

2. Crie uma relação de substituição que substitua a aplicação dependente original pela nova aplicação dependente.  

   Durante novas instalações da aplicação principal, a nova aplicação dependente é instalada. As instalações existentes da aplicação principal são atualizadas com a nova aplicação dependente.  

   O resultado final é que todas as implementações da aplicação principal utilizam a nova aplicação dependente.  

### <a name="further-considerations"></a>Considerações adicionais  

-   Pode especificar múltiplas relações de substituição para aplicações dependentes. A aplicação dependente na localização superior na cadeia de substituição será a aplicação instalada.  

-   As aplicações dependentes devem ser implantadas no dispositivo onde a aplicação principal está instalada ou a aplicação dependente não será instalada.  

-   Para novas instalações da aplicação global, se tiver múltiplas dependências, a ordem da dependência determina qual a versão da aplicação dependente que é instalada.  

### <a name="to-specify-a-supersedence-relationship"></a>Para especificar uma relação de substituição  

1.  Na consola de Configuração Manager, escolha aplicações de gestão de aplicações da **Biblioteca**  >  **Application Management**  >  **Applications**de Software, e depois escolha a aplicação que substitui outra aplicação.  

3.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades** para abrir o nome de aplicação Caixa de diálogo **Properties.**  

4.  No separador **De Supersedência** da caixa de diálogo<Nome de *Aplicação \> * **Properties,** escolha **Adicionar**.  

5.  Na caixa de diálogo **Especificar Relação de Substituição** , clique em **Procurar**.  

6.  Na caixa de diálogo **Escolha aplicação,** escolha a aplicação que pretende substituir e, em seguida, escolha **OK**.  

7.  Na caixa de diálogo **'Relação de Supersedência Especificação',** selecione o tipo de implementação que substitui o tipo de implementação da aplicação sobresed.  

    > [!NOTE]  
    >  Por predefinição, o novo tipo de implementação não desinstala o tipo de implementação da aplicação supersed. Este cenário é utilizado normalmente quando se pretende implementar uma atualização numa aplicação existente. Selecione **Desinstalar** para remover o tipo de implementação existente antes da instalação do novo tipo de implementação. Se optar por atualizar uma aplicação, certifique-se de que testa primeiro este procedimento num ambiente de laboratório.  

8.  Escolha **OK** para fechar a caixa de diálogo especificação da relação de **supersedência.**  

9. Escolha **OK** para fechar a caixa de **diálogo** *<\> Nome* Properties.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Para apresentar as aplicações que substituem a aplicação atual  

1.  Na consola De Configuração, escolha a Biblioteca de **Software.**  

2.  No espaço de trabalho da Biblioteca de **Software,** expandir a Gestão de **Aplicações,** escolher **Aplicações**e, em seguida, escolher a aplicação que deseja.  

3.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades** para abrir a caixa de diálogo<Nome * \> * de Aplicação **Propriedades.**  

4.  No separador **Referências** da caixa de **diálogo**<Nome * \> de Aplicação,* escolha **aplicações que sobressaem esta aplicação** da lista de abandono do **tipo Relacionamento.**  

5.  Reveja a lista de aplicações que substituia a aplicação selecionada e, em seguida, escolha **OK** para fechar a caixa de diálogo *<Nome \> * Properties. **Properties**  
