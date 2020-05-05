---
title: Configurar a administração baseada em funções
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078622"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configure a administração baseada em funções para o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

No Gestor de Configuração, a administração baseada em papéis combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo para cada utilizador administrativo. Um âmbito administrativo inclui os objetos que um utilizador administrativo pode visualizar na consola do Gestor de Configuração e as tarefas relacionadas com os objetos que o utilizador administrativo tem permissão para executar. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

 Se ainda não está familiarizado com conceitos de administração baseada em papéis, consulte [os fundamentos da administração baseada em papéis.](../../../understand/fundamentals-of-role-based-administration.md)  

 As informações nos seguintes procedimentos podem ajudá-lo a criar e configurar a administração baseada em papéis e configurações de segurança relacionadas:  

- [Criar funções de segurança personalizadas](#BKMK_CreateSecRole)  
- [Configurar funções de segurança](#BKMK_ConfigSecRole)  
- [Configurar âmbitos de segurança para um objeto](#BKMK_ConfigSecScope)  
- [Configurar coleções para gerir a segurança](#BKMK_ConfigColl)  
- [Criar um novo utilizador administrativo](#BKMK_Create_AdminUser)  
- [Modificar o âmbito administrativo de um utilizador administrativo](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a>Criar funções de segurança personalizadas

 O Gestor de Configuração fornece várias funções de segurança incorporadas. Se precisar de funções de segurança adicionais, poderá criar uma função de segurança personalizada fazendo uma cópia de uma função existente e modificando-a em seguida. Você pode criar uma função de segurança personalizada para conceder aos utilizadores administrativos as permissões de segurança adicionais que eles exigem que não estão incluídas numa função de segurança atualmente atribuída. Ao utilizar uma função de segurança personalizada, poderá conceder-lhes apenas as permissões de que necessitam, sem ter de atribuir uma função de segurança que conceda permissões adicionais.  

 Utilize o procedimento seguinte para criar uma nova função de segurança utilizando uma função de segurança existente como modelo.  

### <a name="to-create-custom-security-roles"></a>Para criar funções de segurança personalizadas

1. Na consola de Gestor de Configuração, vá para **a Administração.**  

2. No espaço de trabalho da **Administração,** expandir **a Segurança,** e depois escolher funções de **segurança.**  

   Utilize um dos seguintes processos para criar a nova função de segurança:  

    - Para criar uma nova função de segurança personalizada, execute as seguintes ações:  

      1. Selecione uma função de segurança existente para utilizar como origem da nova função de segurança.
      2. No separador **Home,** no grupo **'Papel de Segurança',** escolha **Copy**. Esta ação cria uma cópia do papel de segurança de origem.  
      3. No assistente Copiar Função de Segurança, especifique um **Nome** para a nova função de segurança personalizada.  
      4. Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  
      5. Para alterar a definição para uma operação de segurança, escolha a seta para baixo na coluna **Valor** e escolha **sim** ou **não**.

            > [!CAUTION]  
            > Quando configurar uma função de segurança personalizada, certifique-se de que não concede permissões que não são exigidas pelos utilizadores administrativos que estão associados à nova função de segurança. Por exemplo, o valor **Modificado** para a operação de segurança de **Papéis** de Segurança concede aos utilizadores administrativos permissão para editar qualquer função de segurança acessível – mesmo que não estejam associados a essa função de segurança.  

      6. Depois de configurar as permissões, escolha **OK** para salvar a nova função de segurança.  

    - Para importar uma função de segurança que foi exportada de outra hierarquia do Gestor de Configuração, execute as seguintes ações:  

        1. No separador **Home,** no grupo **Criar,** escolha a **Função**de Segurança da Importação .  
        2. Especifique o ficheiro .xml que contém a configuração da função de segurança que pretende importar. Escolha **aberto** para completar o procedimento e salvar a função de segurança.  

            > [!NOTE]  
            > Após importar uma função de segurança, poderá editar as propriedades da mesma para alterar as permissões de objetos associadas à função.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a>Configurar funções de segurança

 Os grupos de permissões de segurança definidos para uma função de segurança são designados atribuições de operações de segurança. As atribuições de operações de segurança representam uma combinação de tipos de objetos e ações disponíveis para cada tipo de objeto. Pode modificar quais as operações de segurança disponíveis para qualquer função de segurança personalizada, mas não pode modificar as funções de segurança incorporadas que o Gestor de Configuração fornece.  

 Utilize o procedimento seguinte para modificar as operações de segurança de uma função de segurança.  

### <a name="to-modify-security-roles"></a>Para modificar funções de segurança

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança,** e depois escolher funções de **segurança.**  
3. Selecione a função de segurança personalizada que pretende modificar.  
4. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  
5. Escolha o separador **Permissões.**  
6. Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  
7. Para alterar a definição para uma operação de segurança, escolha a seta para baixo na coluna **Valor** e, em seguida, escolha **sim** ou **não**.  

    > [!CAUTION]  
    > Quando configurar uma função de segurança personalizada, certifique-se de que não concede permissões que não são exigidas pelos utilizadores administrativos que estão associados à nova função de segurança. Por exemplo, o valor **Modificado** para a operação de segurança de **Papéis** de Segurança concede aos utilizadores administrativos permissão para editar qualquer função de segurança acessível – mesmo que não estejam associados a essa função de segurança.  

8. Quando terminar de configurar as tarefas de operação de segurança, escolha **OK** para salvar a nova função de segurança.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a>Configure os âmbitos de segurança para um objeto
 Gere a associação de uma mira de segurança para um objeto do objeto- não do âmbito de segurança. As únicas configurações diretas suportadas pelos âmbitos de segurança são as alterações ao respetivo nome e descrição. Para alterar o nome e descrição de um âmbito de segurança ao visualizar as propriedades do âmbito, terá de possuir a permissão **Modificar** no objeto com capacidade de segurança **Âmbitos de Segurança** .  

 Quando cria um novo objeto no Gestor de Configuração, está associado a cada âmbito de segurança associado às funções de segurança da conta utilizada para criar o objeto. Este comportamento ocorre quando essas funções de segurança fornecem a permissão **Criar** ou Definir a permissão de Âmbito de **Segurança.** Pode alterar os âmbitos de segurança do objeto depois de o criar.  

 Como exemplo, é-lhe atribuído um papel de segurança que lhe dá permissão para criar um novo grupo de fronteiras. Ao criar um novo grupo de limites, não tem opção para atribuir âmbitos de segurança específicos. Em vez disso, os âmbitos de segurança disponíveis a partir das funções de segurança a que está associado são automaticamente atribuídos ao novo grupo de fronteiras. Depois de salvar o novo grupo de fronteiras, pode editar os âmbitos de segurança que estão associados ao novo grupo de fronteiras.  

 Utilize o seguinte procedimento para configurar os âmbitos de segurança atribuídos a um objeto.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a>Para configurar os âmbitos de segurança de um objeto  

1. Na consola 'Gestor de Configuração', selecione um objeto que suporta ser atribuído a um âmbito de segurança.  
2. No separador **Home,** no grupo **'Classificar',** escolha **Definir âmbitos**de segurança .
3. Na caixa de diálogo **Definir Âmbitos de Segurança** , selecione ou desmarque os âmbitos de segurança a que este objeto se encontra associado. Cada objeto que suporte âmbitos de segurança tem de ser atribuído a pelo menos um âmbito de segurança.  
4. Escolha **OK** para salvar os âmbitos de segurança atribuídos.  

    > [!NOTE]  
    > Ao criar um novo objeto, poderá atribuir o objeto a vários âmbitos de segurança. Para modificar o número de âmbitos de segurança associados ao objeto, tem de alterar esta atribuição após a criação do objeto.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a>Para configurar os âmbitos de segurança de uma pasta (a partir da versão 1906)
<!--3600867-->

1. Na consola 'Gestor de Configuração', selecione uma pasta.  
1. No separador **pasta** na fita, escolha **Definir Âmbitos de Segurança**.
   - Também pode clicar na pasta para a direita e escolher**os âmbitos**de segurança do conjunto de **pastas** > .
1. Na caixa de diálogo **'Scopes'** de segurança definida, selecione ou limpe os âmbitos de segurança da pasta. Cada pasta deve ser atribuída a pelo menos um âmbito de segurança. Todas as pastas são atribuídas ao âmbito de segurança **Predefinido** até que o altere.
1. Escolha **OK** para salvar os âmbitos de segurança atribuídos.  

    > [!IMPORTANT]  
    > - As funções de segurança existentes obterão automaticamente permissões **de Classe de Pasta** adicionadas quando instalar a versão 1906 do Gestor de Configuração. Terá de adicionar permissões **de Classe pasta** para quaisquer novas funções de segurança e verificar se as funções existentes têm as permissões adequadas para o seu ambiente.
    > 
    > - Um item é pesquisável na pasta fora do âmbito de segurança de um utilizador se esse utilizador partilhar um âmbito de segurança com a pessoa que criou o objeto. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a>Configure coleções para gerir a segurança

 Não existem procedimentos para configurar coleções para administração baseada em funções. As coleções não têm uma configuração de administração baseada em papéis. Em vez disso, atribui coleções a um utilizador administrativo quando configura o utilizador administrativo. As operações de segurança de recolha que estão ativadas nas funções de segurança atribuídas pelo utilizador determinam as permissões que um utilizador administrativo tem para recolhas e recursos de recolha (membros da recolha).  

 Quando um utilizador administrativo tem permissões para uma coleção, também tem permissões para coleções que estejam limitadas a essa coleção. Como exemplo, a sua organização usa uma coleção chamada All Desktops. Há também uma coleção chamada All North America Desktops que está limitada à coleção All Desktops. Se um utilizador administrativo tiver permissões para Todos os Ambientes de Trabalho, também terá as mesmas permissões para a coleção Todos os Ambientes de Trabalho da América do Norte.

 Além disso, um utilizador administrativo não pode utilizar a permissão **Eliminar** ou **Modificar** numa coleção que lhes seja atribuída diretamente. Mas podem usar estas permissões nas coleções que se limitam a essa coleção. No exemplo anterior, o utilizador administrativo pode eliminar ou modificar a coleção All North America Desktops, mas não pode excluir ou modificar a coleção All Desktops.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Criar um novo utilizador administrativo

 Para conceder a indivíduos ou membros de um grupo de segurança acesso para gerir o Gestor de Configuração, crie um utilizador administrativo no Gestor de Configuração e especifique a conta Windows do Utilizador ou Grupo utilizador. Cada utilizador administrativo do Gestor de Configuração deve ser atribuído pelo menos uma função de segurança e um âmbito de segurança. Também é possível atribuir coleções para limitar o âmbito administrativo do utilizador administrativo.  

 Utilize os procedimentos seguintes para criar novos utilizadores administrativos.  

### <a name="to-create-a-new-administrative-user"></a>Para criar um novo utilizador administrativo  

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança**e, em seguida, escolher **Utilizadores Administrativos.**  
3. No separador **Home,** no grupo **Criar,** escolha **Adicionar utilizador ou Grupo**.  
4. Escolha **'Navegar'** e, em seguida, selecione a conta ou grupo de utilizador para utilizar para este novo utilizador administrativo.  

    > [!NOTE]  
    > Para a administração baseada em consolas, apenas podem ser especificados utilizadores de domínio ou grupos de segurança como utilizadores administrativos.

5. Para **funções de segurança associadas,** escolha **Adicionar** para abrir uma lista das funções de segurança disponíveis, verifique a caixa para obter uma ou mais funções de segurança e, em seguida, escolha **OK**.  

6. Escolha uma das duas opções seguintes para definir o comportamento do objeto titular para o novo utilizador:  

    - **Todas as instâncias dos objetos que estão relacionados com as funções**de segurança atribuídas : Esta opção associa o utilizador administrativo ao âmbito de segurança **All,** e as coleções **de Todos os Sistemas** e **Todos os Utilizadores e Grupos de Utilizadores.** As funções de segurança atribuídas ao utilizador definem o acesso aos objetos. Os novos objetos criados por este utilizador administrativo são atribuídos ao âmbito de segurança **Predefinido** .  

    - **Apenas as instâncias de objetos que são atribuídos aos âmbitos e coleções**de segurança especificados : Por padrão, esta opção associa o utilizador administrativo ao âmbito de segurança **Predefinido** e às coleções **de Todos os Sistemas** e **Todos os Utilizadores e Grupos de Utilizadores.** No entanto, os âmbitos de segurança e coleções reais estão limitados aos que estão associados à conta utilizada para criar o novo utilizador administrativo. Esta opção suporta a adição ou remoção de âmbitos de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

    > [!IMPORTANT]  
    > As opções anteriores associam cada âmbito de segurança atribuído a cada função de segurança que seja atribuída ao utilizador administrativo. Pode utilizar uma terceira opção, **a Associate atribuiu funções de segurança com âmbitos e coleções de segurança específicos,** para associar funções de segurança individuais a âmbitos e coleções de segurança específicas. Esta terceira opção está disponível após a criação do novo utilizador administrativo, quando este é modificado.  

7. Dependendo da seleção no passo 6, execute a ação seguinte:  

    - Se selecionar **Todas as instâncias dos objetos relacionados com as funções**de segurança atribuídas, escolha **OK** para completar este procedimento.  

    - Se selecionou **Apenas as instâncias de objetos atribuídos aos âmbitos e coleções de segurança especificados,** pode escolher **adicionar** para selecionar coleções adicionais e âmbitos de segurança. Ou selecione um ou mais objetos na lista e, em seguida, escolha **Remover** para removê-los. Escolha **OK** para completar este procedimento.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modificar o âmbito administrativo de um utilizador administrativo

 Para modificar o âmbito administrativo de um utilizador administrativo, adicione ou remova funções de segurança, âmbitos de segurança e coleções que estejam associados ao utilizador. Cada utilizador administrativo tem de estar associado, pelo menos, a uma função de segurança e a um âmbito de segurança. Poderá ser necessário atribuir uma ou mais coleções ao âmbito administrativo do utilizador. A maioria das funções de segurança interagem com coleções e não funcionam corretamente sem uma coleção atribuída.  

 Quando modifica um utilizador administrativo, pode alterar o comportamento para a forma como os objetos com capacidade de segurança são associados às funções de segurança atribuídas. Os três comportamentos que pode selecionar são os seguintes:  

- **Todas as instâncias dos objetos que estão relacionados com as funções**de segurança atribuídas : Esta opção associa o utilizador administrativo com o âmbito **de todos os** sistemas e **todas** as coleções de Utilizadores **e Grupos de Utilizadores.** As funções de segurança atribuídas ao utilizador definem o acesso aos objetos.  

- **Apenas os casos de objetos que são atribuídos aos âmbitos e coleções**de segurança especificados : Esta opção associa o utilizador administrativo aos mesmos âmbitos de segurança e coleções que estão associados à conta que utiliza para configurar o utilizador administrativo. Esta opção suporta a adição ou remoção de funções de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

- **Associar funções de segurança atribuídas com âmbitos e coleções de segurança específicos**: Esta opção permite criar associações específicas entre funções de segurança individuais e âmbitos de segurança específicos e coleções para o utilizador.  

    > [!NOTE]  
    > Esta opção está disponível apenas quando modificar as propriedades de um utilizador administrativo.  

A configuração atual do comportamento do objeto com capacidade de segurança altera o processo utilizado para atribuir funções de segurança adicionais. Utilize os procedimentos seguintes que são baseados nas diferentes opções para objetos com capacidade de segurança para o ajudar a gerir um utilizador administrativo.  

Utilize o seguinte procedimento para visualizar e gerir a configuração de objetos securáveis para um utilizador administrativo.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para ver e gerir o comportamento de objetos com capacidade de segurança de um utilizador administrativo  

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança**e, em seguida, escolher **Utilizadores Administrativos.**  
3. Selecione o utilizador administrativo que pretende modificar.  
4. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  
5. Escolha o separador **'Âmbitos de Segurança'** para visualizar a configuração atual de objetos securáveis para este utilizador administrativo.  
6. Para modificar o comportamento do objeto com capacidade de segurança, selecione uma nova opção para o comportamento do objeto com capacidade de segurança. Depois de alterar esta configuração, consulte o procedimento adequado para obter mais orientações para configurar os âmbitos e coleções de segurança e as funções de segurança para este utilizador administrativo.  
7. Escolha **OK** para completar o procedimento.  

Utilize o seguinte procedimento para modificar um utilizador administrativo que tenha o comportamento do objeto titular definido em **todas as instâncias dos objetos que estejam relacionados com as funções**de segurança atribuídas .  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Por opção: Todos os casos dos objetos que estão relacionados com as funções de segurança atribuídas  

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança**e, em seguida, escolher **Utilizadores Administrativos.**  
3. Selecione o utilizador administrativo que pretende modificar.  
4. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  
5. Escolha o separador **'Âmbitos de Segurança'** para confirmar que o utilizador administrativo está configurado para **todos os casos dos objetos que estão relacionados com as funções**de segurança atribuídas .  
6. Para modificar as funções de segurança atribuídas, escolha o separador Funções de **Segurança.**  

    - Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **Adicionar**, verifique a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  
    - Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e, em seguida, escolha **Remover**.

7. Para modificar o comportamento do objeto titular, escolha o separador **'Scopes de Segurança'** e escolha uma nova opção para o comportamento do objeto titular. Depois de alterar esta configuração, consulte o procedimento adequado para obter mais orientações para configurar os âmbitos e coleções de segurança e as funções de segurança para este utilizador administrativo.  

    > [!NOTE]  
    > Quando o comportamento do objeto titular é definido para **Todas as instâncias dos objetos que estão relacionados com as funções**de segurança atribuídas, não pode adicionar ou remover âmbitos e coleções de segurança específicos.  

8. Escolha **OK** para completar este procedimento.  

Utilize o seguinte procedimento para modificar um utilizador administrativo que tenha o comportamento do objeto titular definido apenas para **as instâncias de objetos que são atribuídos aos âmbitos e coleções**de segurança especificados .  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Por opção: Apenas as instâncias de objetos atribuídos aos âmbitos e coleções de segurança especificados  

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança**e, em seguida, escolher **Utilizadores Administrativos.**  
3. Selecione o utilizador administrativo que pretende modificar.  
4. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  
5. Escolha o separador **'Âmbitos** de Segurança' para confirmar que o utilizador está configurado apenas para **as instâncias de objetos que são atribuídos aos âmbitos e coleções**de segurança especificados .  
6. Para modificar as funções de segurança atribuídas, escolha o separador Funções de **Segurança.**  

    - Para atribuir funções de segurança adicionais a este utilizador, escolha **Adicionar**, verifique a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  
    - Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e, em seguida, escolha **Remover**.  
7. Para modificar os âmbitos de segurança e coleções que estão associados a funções de segurança, escolha o separador **Security Scopes.**  

    - Para associar novos âmbitos de segurança ou coleções com todas as funções de segurança atribuídas a este utilizador administrativo, escolha **Adicionar** e selecione uma das quatro opções. Se selecionar **O Âmbito** de Segurança ou a **Recolha,** verifique se a caixa tem um ou mais objetos para completar essa seleção e, em seguida, escolha **OK**.  
    - Para remover um âmbito de segurança ou recolha, escolha o objeto e, em seguida, escolha **Remover**.

8. Escolha **OK** para completar este procedimento.  

Utilize o seguinte procedimento para modificar um utilizador administrativo que tenha o comportamento de objeto sinuoso definido para **a Associate assinou funções de segurança com âmbitos e coleções de segurança específicos.**  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Para opção: Associado asfunções de segurança atribuídas com âmbitos e coleções de segurança específicos  

1. Na consola De Configuração, escolha **Administração**.  
2. No espaço de trabalho da **Administração,** expandir **a Segurança**e, em seguida, escolher **Utilizadores Administrativos.**  
3. Selecione o utilizador administrativo que pretende modificar.  
4. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  
5. Escolha o separador **Security Scopes** para confirmar que o utilizador administrativo está configurado para as funções de segurança atribuídas à **Associate com âmbitos e coleções de segurança específicos**.  
6. Para modificar as funções de segurança atribuídas, escolha o separador Funções de **Segurança.**  

    - Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **Adicionar**. Na caixa de diálogo **Add Security Role,** selecione uma ou mais funções de segurança disponíveis, escolha **Adicionar**, e selecione um tipo de objeto para associar com as funções de segurança selecionadas. Se selecionar **O Âmbito** de Segurança ou a **Recolha,** verifique se a caixa tem um ou mais objetos para completar essa seleção e, em seguida, escolha **OK**.  

        > [!NOTE]  
        > Tem de configurar, pelo menos, um âmbito de segurança para que as funções de segurança selecionadas possam ser atribuídas ao utilizador administrativo. Quando seleciona várias funções de segurança, cada coleção e âmbito de segurança que configura são associados a cada um dos perfis de segurança selecionados.  

    - Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e, em seguida, escolha **Remover**.  

7. Para modificar os âmbitos de segurança e coleções que estão associados a uma função de segurança específica, escolha o separador **Security Scopes,** selecione a função de segurança e, em seguida, escolha **Editar**.  

    - Para associar novos objetos a esta função de segurança, escolha **Adicionar**, e selecione um tipo de objeto para associar com as funções de segurança selecionadas. Se selecionar **O Âmbito** de Segurança ou a **Recolha,** verifique se a caixa tem um ou mais objetos para completar essa seleção e, em seguida, escolha **OK**.  

        > [!NOTE]  
        > Deve configurar pelo menos uma mira de segurança.  

    - Para remover um âmbito de segurança ou recolha associado a esta função de segurança, selecione o objeto e, em seguida, escolha **Remover**.  

    - Quando terminar de modificar os objetos associados, escolha **OK**.  

8. Escolha **OK** para completar este procedimento.  

    > [!CAUTION]  
    > Quando uma função de segurança concede a utilizadores administrativos a permissão de implementação de coleção, esses utilizadores administrativos podem distribuir objetos de qualquer âmbito de segurança para o qual possuam permissões de **leitura** de objetos, mesmo que esse âmbito de segurança esteja associado a outra função de segurança.  

## <a name="next-steps"></a>Passos seguintes

[Contas utilizadas no Gestor de Configuração](../../../plan-design/hierarchy/accounts.md)
