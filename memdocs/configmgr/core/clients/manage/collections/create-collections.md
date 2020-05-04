---
title: Criar coleções
titleSuffix: Configuration Manager
description: Crie coleções no Gestor de Configuração para gerir mais facilmente grupos de utilizadores e dispositivos.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3f178b41fbb305ef938063bd9b9743daa6b5c69
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714361"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Como criar coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As coleções são agrupamentos de utilizadores ou dispositivos. Utilize coleções para tarefas como gerir aplicações, implementar definições de conformidade ou instalar atualizações de software. Também pode utilizar coleções para gerir grupos de definições de cliente ou utilizá-las com a administração baseada em funções para especificar os recursos aos quais um utilizador administrativo pode aceder. O Gestor de Configuração contém várias coleções incorporadas. Para mais informações, consulte [Introdução às coleções.](introduction-to-collections.md)  

> [!NOTE]  
> Uma coleção pode conter utilizadores ou dispositivos, mas não ambos.  


As informações neste artigo podem ajudá-lo a criar coleções no Gestor de Configuração. Também pode importar coleções que foram criadas no site atual do Gestor de Configuração ou noutro. Para obter mais informações sobre como exportar e importar coleções, consulte [Como gerir as coleções.](manage-collections.md)  


## <a name="collection-rules"></a>Regras de cobrança

Existem diferentes tipos de regras que pode utilizar para configurar os membros de uma coleção em 'Gestor de Configuração'.  


### <a name="direct-rule"></a>Regra direta

Utilize regras diretas para escolher os utilizadores ou computadores que pretende adicionar a uma coleção. A adesão não muda a menos que remova um recurso do Gestor de Configuração. Antes de poder adicionar os recursos a uma recolha de regras diretas, o Gestor de Configuração deve tê-los descoberto ou deve tê-los importado. As coleções de regras diretas têm mais despesaadministrativa do que as coleções de regras de consulta porque requerem alterações manuais.


### <a name="query-rule"></a>Regra de consulta

Atualize dinamicamente a adesão a uma coleção com base numa consulta que o Gestor de Configuração executa numa programação. Por exemplo, pode criar uma coleção de utilizadores que são membros da unidade organizacional Recursos Humanos nos Serviços de Domínio do Active Directory. Esta recolha é automaticamente atualizada quando novos utilizadores são adicionados ou removidos da unidade organizacional dos Recursos Humanos.

Por exemplo, consultas que pode usar para construir coleções, ver [como criar consultas.](../../../servers/manage/create-queries.md)


### <a name="device-category-rule"></a>Regra da categoria do dispositivo

Pode facilitar a gestão dos seus dispositivos associando categorias de dispositivos com as coleções de dispositivos. 

Para mais informações, consulte [automaticamente categorizar dispositivos em coleções](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regra de inclusão de coleção

Inclua os membros de outra coleção numa coleção de Gestor de Configuração. Se a coleção incluída mudar, o Gestor de Configuração atualiza a adesão à coleção atual numa programação.

Pode adicionar várias regras de inclusão de coleção a uma coleção.


### <a name="exclude-collection-rule"></a>Regra de exclusão de coleção

Excluir regras de cobrança permitem excluir os membros de uma coleção de outra coleção do Gestor de Configuração. Se a recolha excluída mudar, o Gestor de Configuração atualiza a adesão à coleção atual numa programação.

Pode adicionar várias regras de exclusão de coleção a uma coleção. Se uma coleção inclui ambas incluir regras de recolha e excluir regras de recolha e há um conflito, a regra de exclusão de coleção tem prioridade.

#### <a name="example"></a>Exemplo
Cria-se uma coleção que tem uma regra de recolha e uma regra de recolha. A regra de inclusão de coleção destina-se a uma coleção de computadores de secretária Dell. A coleção de excluséis destina-se a uma coleção de computadores que tenham menos de 4 GB de RAM. A nova coleção contém desktops Dell que têm pelo menos 4 GB de RAM.



## <a name="create-a-collection"></a><a name="bkmk_create"></a>Criar uma coleção  

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.**  

    - Para criar uma recolha de *dispositivos,* selecione o nó de **Recolha de Dispositivos.** Em seguida, no separador **Home** da fita, no grupo **Criar,** selecione **Create Device Collection**.  

    - Para criar uma recolha de *utilizadores,* selecione o nó de **Recolha de Utilizadores.** Em seguida, no separador **Home** da fita, no grupo **Criar,** selecione **Criar a Recolha do Utilizador**.  

2. Na página **geral** do assistente, forneça um **Nome** e um **Comentário**. Na secção **limitativa,** selecione **Browse**, e, em seguida, selecione uma coleção limitativa. A coleção que está a criar conterá apenas membros da coleção limitativa.  

4. Na página Regras de **Adesão,** na lista **de Regra adicionar,** selecione o tipo de regra de adesão que pretende utilizar para a recolha. Pode configurar várias regras para cada coleção. A configuração para cada regra varia. Para obter mais informações sobre a configuração de cada regra, consulte as seguintes secções deste artigo:  
    - [Regra direta](#bkmk-direct)
    - [Regra de consulta](#bkmk-query)
    - [Regra da categoria do dispositivo](#bkmk-category)
    - [Regra de inclusão de coleção](#bkmk-include)
    - [Regra de exclusão de coleção](#bkmk-exclude)

5. Também na página Regras de **Adesão,** reveja as seguintes definições.

    - **Utilize atualizações incrementais para esta recolha**: Selecione esta opção para digitalizar periodicamente e atualizar apenas recursos novos ou alterados a partir da avaliação de recolha anterior. Este processo é independente de uma avaliação completa da recolha. Por predefinição, as atualizações incrementais ocorrem em intervalos de 5 minutos.  

        > [!IMPORTANT]  
        >  As coleções com regras de consulta que utilizam as seguintes aulas não suportam atualizações incrementais:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Agende uma atualização completa desta coleção**: Agendar uma avaliação completa regular da adesão à coleção.  

        A partir da versão 1810, estas alterações no comportamento de avaliação da coleção podem melhorar o desempenho do site:<!--3607726-->  

        - Anteriormente, quando configurava uma programação numa coleção baseada em consultas, o site continuaria a avaliar a consulta se permitia ou não a definição de recolha para **agendar uma atualização completa desta coleção.** Para desativar totalmente o horário, teve de alterar o horário para **Nenhum.**

            Agora o site limpa o horário quando desativa este cenário. Para especificar um calendário para avaliação de recolha, ative a opção de **agendar uma atualização completa sobre esta coleção.**  

            Quando atualiza o seu site, para qualquer recolha existente na qual especificou uma programação, o site permite a opção de **agendar uma atualização completa sobre esta coleção**. Embora esta configuração possa não ser a sua intenção, foi o comportamento real do horário antes de atualizar o site. Para impedir que o site avalie uma coleção num horário, desative esta opção.  

        - Não é possível desativar a avaliação de coleções incorporadas como **a All Systems,** mas agora pode configurar o horário. Este comportamento permite personalizar esta ação num momento que satisfaz os seus requisitos. 

            > [!TIP]  
            > Em coleções embutidas, apenas altere o **horário** do horário personalizado. Não mude o **padrão de recorrência.** As futuras iterações podem impor um padrão específico de recorrência.  

6. Conclua o assistente para criar a nova coleção. A nova coleção é apresentada no nó **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** .  

> [!NOTE]  
> Tem de atualizar ou recarregar a consola 'Gestor de Configuração' para ver os membros da coleção. Só aparecem na coleção depois da primeira atualização programada. Também pode selecionar manualmente a **Atualização para** a recolha. Pode levar alguns minutos para que uma atualização de recolha seja concluída.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a>Configurar uma regra direta  

1. Na página **Search for Resources** do Assistente de Regra de **Adesão Direta,** especifique as seguintes informações.  

    - **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicione à recolha. Por exemplo:
        - **Recursos do Sistema**: Procurar dados de inventário devolvidos a partir de computadores clientes.
        - **Computador desconhecido**: Selecione a partir de valores devolvidos por computadores desconhecidos.
        - **Recursos do Utilizador**: Procure informações do utilizador recolhidas pelo Gestor de Configuração.
        - **Recursos do Grupo do Utilizador**: Procure informações do grupo do utilizador recolhidas pelo Gestor de Configuração.

    - Nome do **atributo**: Selecione o atributo associado à classe de recursos selecionado seletiva que pretende procurar. Por exemplo:  

        - Se pretender selecionar computadores pelo seu nome NetBIOS, selecione **O Recurso do Sistema** na lista de classe **Recursos** e o **nome NetBIOS** na lista de **nomes do Atributo.**  

        - Se pretender selecionar utilizadores pelo nome da sua unidade organizacional (OU), selecione **User Resource** na lista de **classe Recurso** e Nome **user OU** na lista de **nomes do Atributo.**  

    - **Excluir recursos marcados como obsoletos**: Se um computador cliente for marcado como obsoleto, não inclua este valor nos resultados da pesquisa.  

    - Excluir recursos que não tenham o cliente do Gestor de **Configuração instalados**: Estes recursos não serão apresentados nos resultados da pesquisa.  

    - **Valor**: Insira um valor para pesquisar o nome do atributo selecionado. Use o caráter por cento (%) como um wildcard. Por exemplo:  
        - Para procurar computadores com um nome NetBIOS a partir de "M", insira **M%** neste campo.  
        - Para pesquisar por utilizadores no Contoso OU, entre **contoso** neste campo.

2. Na página **Select Resources,** selecione os recursos que pretende adicionar à recolha na lista **de Recursos** e, em seguida, selecione **Next**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a>Configurar uma regra de consulta  

Na caixa de diálogo **'Regra consulta' Properties,** especifique as seguintes informações.  

- **Nome**: Especifique um nome único para a consulta.  

- **Declaração de Consulta**de Importação : Abre a caixa de diálogo de consulta de **navegação.** Selecione uma consulta do Gestor de [Configuração](../../../servers/manage/create-queries.md) para usar como regra de consulta para a coleção.   

- **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicione à recolha. Selecione um valor do **Recurso do Sistema** para procurar dados de inventário devolvidos a computadores clientes ou de Computador **Desconhecido** para selecionar a partir de valores devolvidos por computadores desconhecidos.  

- **Editar Declaração de Consulta**: Abre a caixa de diálogo De Declaração de **Consulta Properties,** onde pode escrever uma consulta para usar como regra para a recolha. Para mais informações sobre consultas, consulte [Introdução a consultas](../../../servers/manage/introduction-to-queries.md).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a>Regra da categoria do dispositivo

As seguintes ações estão disponíveis na janela **Select Device Categories.**

- **Criar**: Especifique um nome para criar uma nova categoria.
- **Nome de novo**: Mude o nome da categoria selecionada.
- **Eliminar**: Selecione uma ou mais categorias e utilize esta ação para as retirar da lista.

Para mais informações, consulte [automaticamente categorizar dispositivos em coleções](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a>Configure uma regra de recolha de incluir  

Na caixa de diálogo **Select Collections,** selecione as coleções que pretende incluir na nova coleção e, em seguida, selecione **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a>Configure uma regra de exclusão de coleção  

Na caixa de diálogo **Select Collections,** selecione as coleções que pretende excluir da nova coleção e, em seguida, selecione **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a>Importar uma coleção  

Ao exportar uma coleção a partir de um site, o Gestor de Configuração guarda-a como um ficheiro De Formato de Objeto Gerido (MOF). Utilize este procedimento para importar esse ficheiro para a base de dados do seu site. Para completar este procedimento, precisa de **criar** permissões na aula de coleções.

> [!IMPORTANT]  
> - Certifique-se de que o ficheiro contém apenas dados de recolha, é de uma fonte fidedigna, e não foi adulterado.  
> 
> - Certifique-se de que o ficheiro foi exportado de um site com a mesma versão do Gestor de Configuração que está a usar.  

Para obter mais informações sobre exportação de coleções, consulte [Como gerir as coleções.](manage-collections.md)


1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Selecione as **Coleções** do Utilizador ou o nó de **Recolha de Dispositivos.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione **Import Collections**.  

3. Na página **geral** do Assistente de **Coleções de Importação,** selecione **Next**.  

4. Na página nome de **ficheiro MOF,** selecione **Browse**. Navegue no ficheiro MOF que contém as informações de recolha que pretende importar.  

5. Conclua o assistente para importar a coleção. A nova coleção é apresentada no nó **Coleções de Utilizadores** ou **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** . Refresque ou recarregue a consola Do Gestor de Configuração para ver os membros da coleção para a coleção recém-importada.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a>Sincronizar os resultados da adesão à coleção aos grupos de Diretórios Ativos da Azure

<!--3607475-->
> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1906 como uma [funcionalidade de pré-lançamento.](../../../servers/manage/pre-release-features.md) Começando com a versão 2002, já não é uma funcionalidade de pré-lançamento.  

Pode permitir a sincronização de membros da coleção a um grupo azure Ative Directory (Azure AD). Esta sincronização permite-lhe utilizar as suas regras de agrupamento de instalações na nuvem, criando membros do grupo Azure AD com base nos resultados da adesão à coleção. Pode sincronizar as coleções de dispositivos. Apenas os dispositivos com um registo de Diretório Ativo Azure refletem-se no Grupo Azure AD. Tanto os dispositivos Híbrido Azure AD AD e Azure Ative Diretor são suportados.

A sincronização da AD Azure acontece a cada cinco minutos. É um processo de ida, desde o Diretor de Configuração até ao Anúncio Azure. As alterações efetuadas em AD Azure não se refletem nas coleções do Gestor de Configuração, mas não são substituídas pelo Gestor de Configuração. Por exemplo, se a coleção Do Gestor de Configuração tiver dois dispositivos, e o grupo Azure AD tiver três dispositivos diferentes, após a sincronização, o grupo Azure AD tem cinco dispositivos.


### <a name="prerequisites"></a>Pré-requisitos

- [Gestão de Nuvem](../../../servers/deploy/configure/azure-services-wizard.md)
- [Descoberta de utilizador do Diretório Ativo Azure](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Crie um grupo e coloque o proprietário em Azure AD

1. Vai [https://portal.azure.com](https://portal.azure.com)para.
1. Navegue para > **grupos** > de **diretório ativo Azure****Todos os grupos**.
1. Clique em **Novo grupo** e escreva num nome **de grupo** e opcionalmente **descrição do Grupo.**
1. Certifique-se de que o **tipo de Membro** está **atribuído**.
1. Selecione **Proprietários,** em seguida, adicione a identidade que irá criar a relação de sincronização em 'Gestor de Configuração'.
1. Clique em **Criar** para terminar a criação do grupo Azure AD.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Permitir a sincronização da coleção para o serviço Azure

1. Na consola de Gestor de Configuração, vá ao **Administration** > **Overview** > **Cloud Services** > **Azure Services**.
1. Clique à direita no inquilino Azure AD onde criou o grupo e selecione **Propriedades**.
1. No separador **De Sincronização de Recolha,** verifique a caixa para o **Enable Azure Directy Group Sync**.
1. Clique **em OK** para salvar a definição.

### <a name="enable-the-collection-to-synchronize"></a>Ativar a coleção para sincronizar

1. Na consola de Configuração Manager, vá a Recolhas de**Dispositivos**de**Visão Geral** > de **Ativos e Conformidade.** > 
1. Clique na recolha para sincronizar e, em seguida, clique em **Propriedades**. 
1. No separador **AAD Group Sync,** clique em **Adicionar**.
1. A partir do menu suspenso, selecione o **Inquilino** onde criou o seu grupo Azure AD.
1. Digite os seus critérios de pesquisa no **nome começa com** o campo e, em seguida, clique em **Procurar**.
  - Se for solicitado que assine, utilize a identidade especificada como proprietária do grupo Azure AD.
1. Selecione o grupo alvo e, em seguida, clique em **OK** para adicionar o grupo e **OK** novamente para sair das propriedades da coleção.
1. Terá de esperar cerca de 5 a 7 minutos para poder verificar os membros do grupo no portal Azure.
   - Para iniciar uma sincronização completa, clique na recolha e, em seguida, selecione **Synchronize Membership**.


### <a name="verify-the-azure-ad-group-membership"></a>Verifique a adesão ao grupo Azure AD

1. Vai [https://portal.azure.com](https://portal.azure.com)para.
1. Navegue para > **grupos** > de **diretório ativo Azure****Todos os grupos**.
1. Encontre o grupo que criou e selecione **Membros**. 
1. Confirme que os membros refletem os membros na coleção 'Gestor de Configuração'.
   - Apenas dispositivos com identidade Azure AD aparecerão no grupo.


![Sincronizar coleções para a Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Usando powershell

Pode utilizar a PowerShell para criar e importar coleções. Para obter mais informações, consulte:

* [Coleção New-CM](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Passos seguintes

[Gerir coleções](manage-collections.md)
