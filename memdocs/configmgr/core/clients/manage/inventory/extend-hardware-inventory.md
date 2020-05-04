---
title: Alargar o inventário de hardware
titleSuffix: Configuration Manager
description: Aprenda formas de alargar o inventário de hardware no Gestor de Configuração.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714417"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Como alargar o inventário de hardware no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O inventário de hardware lê informações de Computadores windows utilizando instrumentação de gestão do Windows (WMI). O WMI é a implementação da Microsoft de Gestão Empresarial (WBEM), um padrão da indústria para aceder a informações de gestão numa empresa. Em versões anteriores do 'Gestor de Configuração', alargou o inventário de hardware modificando o ficheiro sms_def.mof no servidor do site. Este ficheiro continha uma lista de classes wMI que podiam ser lidas através do inventário de hardware. Editar este ficheiro, pode ativar e desativar as classes existentes, e também criar novas classes para o inventário.  

O ficheiro Configuração.mof é utilizado para definir as classes de dados a serem inventariadas por inventário de hardware no cliente e não é alterada do Gestor de Configuração 2012. Pode criar classes de dados para inventariar classes de dados existentes ou personalizados do repositório WMI ou chaves de registo presentes em sistemas cliente.  

 O ficheiro Configuration.mof também define e regista os fornecedores WMI que acedem a informações de dispositivos durante o inventário de hardware. Registar fornecedores define o tipo de fornecedor a utilizar e as classes que o fornecedor suporta.  

 Quando os clientes do Gestor de Configuração solicitam a política, o Configuração.mof está ligado ao órgão de política. Em seguida, este ficheiro é transferido e compilado pelos clientes. Quando adicionar, modificar ou eliminar classes de dados a partir do ficheiro Configuration.mof, os clientes compilam automaticamente estas alterações efetuadas em classes de dados relacionadas com o inventário. Não são necessárias mais medidas para inventariar novas ou modificadas classes de dados nos clientes do Gestor de Configuração. Este ficheiro está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores de site primários.  

 No 'Gestor de Configuração', já não edita o ficheiro sms_def.mof como fez no Gestor de Configuração 2007. Em vez disso, pode ativar e desativar classes WMI e adicionar novas classes para recolher pelo inventário de hardware, utilizando as definições do cliente. O Gestor de Configuração fornece os seguintes métodos para alargar o inventário de hardware.  

> [!NOTE]  
>  Se alterou manualmente o ficheiro Configuração.mof para adicionar classes de inventário personalizadas, estas alterações serão substituídas quando atualizar para a versão 1602. Para continuar a utilizar as classes personalizadas após a atualização, deve adicioná-las à secção "Extensões Adicionadas" do ficheiro Configuração.mof após a atualização para 1602.  
> No entanto, não deve modificar nada acima desta secção, uma vez que estas secções são reservadas para modificação pelo Gestor de Configuração. Está disponível uma cópia de segurança do Configuration.mof em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Ativar ou desativar classes de inventário existentes|Ative ou desative as classes de inventário padrão ou crie configurações personalizadas do cliente que lhe permitam recolher diferentes classes de inventário de hardware a partir de coleções especificadas de clientes. Consulte o procedimento [de habilitação ou desativação](#BKMK_Enable) das classes de inventário existentes neste artigo.|  
|Adicionar uma nova classe de inventário|Adicione uma nova classe de inventário do espaço de nome WMI de outro dispositivo. Consulte o [To adicionar um novo](#BKMK_Add) procedimento de classe de inventário neste artigo.|  
|Importar e exportar classes de inventário de hardware|Importar e exportar ficheiros de formato de objeto gerido (MOF) que contenham classes de inventário da consola Do Gestor de Configuração. Consulte as classes de inventário de [hardware para importar](#BKMK_Import) e exportar procedimentos de inventário de [hardware](#BKMK_Export) neste artigo.|  
|Criar Ficheiros NOIDMIF|Utilize ficheiros NOIDMIF para recolher informações sobre dispositivos clientes que não podem ser inventariados pelo Gestor de Configuração. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é associado automaticamente ao dispositivo cliente a partir do qual foi recolhido. Consulte [para criar ficheiros NOIDMIF](#BKMK_NOIDMIF) neste artigo.|  
|Criar Ficheiros IDMIF|Utilize ficheiros IDMIF para recolher informações sobre ativos na sua organização que não estejam associados a um cliente do Gestor de Configuração, por exemplo, projetores, fotocopiadoras e impressoras de rede. Consulte [para criar ficheiros IDMIF](#BKMK_IDMIF) neste artigo.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para expandir o inventário de hardware  
Estes procedimentos ajudam a configurar as predefinições de cliente para o inventário de hardware e aplicam-se a todos os clientes na sua hierarquia. Se quiser que estas definições se apliquem apenas a alguns clientes, crie uma definição personalizada de dispositivo de cliente e atribua-a a uma coleção de clientes específicos. Ver [Como configurar as definições do cliente](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Para ativar ou desativar as classes de inventário existentes  

1.  Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

4.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

5.  Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

6.  Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware** , selecione ou desmarque as classes e propriedades de classes que pretende que sejam recolhidas pelo inventário de hardware. Pode expandir classes para selecionar ou desmarcar propriedades individuais dentro dessa classe. Utilize o campo **Procurar classes de inventário** para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando adicionar novas classes ao inventário de hardware do Gestor de Configuração, o tamanho do ficheiro de inventário que é recolhido e enviado para o servidor do site aumentará. Isto pode afetar negativamente o desempenho do site do seu gestor de rede e configuração. Ative apenas as classes de inventário que pretende recolher.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

Só pode adicionar classes de inventário do servidor de nível superior da hierarquia modificando as definições padrão do cliente. Esta opção não está disponível quando criar definições personalizadas do dispositivo.

1. Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

2. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

3. Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

4. Na lista de Definições do **Dispositivo,** escolha **Definições**.  

5. Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Adicionar**.  

6. Na caixa de diálogo **Adicionar Classe de Inventário de Hardware** , clique em **Ligar**.  

7. Na caixa de diálogo **Ligar à Windows Management Instrumentation (WMI)** , especifique o nome do computador a partir do qual irá obter as classes WMI e o espaço de nomes WMI a utilizar para obter as classes. Se pretender obter todas as classes abaixo do espaço de nomes WMI que especificou, clique em **Recursiva**. Se o computador ao qual está a ligar não for o computador local, forneça as credenciais de início de sessão para uma conta que tenha permissão para aceder ao WMI no computador remoto.  

8. Escolha **Connect** (Ligar).  

9. Na caixa de diálogo **Add Hardware Inventory Class,** na lista de **classes de Inventário,** selecione as classes WMI que pretende adicionar ao inventário de hardware do Gestor de Configuração.  

10. Se pretender editar informações sobre a classe WMI selecionada, escolha **Editar,** e na caixa de diálogo de **qualificação de classe,** forneça as seguintes informações:  

    - **Nome** do ecrã - Este nome será exibido no Resource Explorer.  

    - **Propriedades** - Especifique as unidades em que cada propriedade da classe WMI será exibida.  

      Também pode designar propriedades como uma propriedade de chave para o ajudar a identificar exclusivamente cada instância da classe. Se não for definida qualquer chave para a classe e várias instâncias da classe forem comunicadas a partir do cliente, apenas a instância mais recente encontrada é armazenada na base de dados.  

      Quando terminar de configurar as propriedades, clique em **OK** para fechar a caixa de diálogo de **qualificação de classe** e os outros diálogos abertos. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

Só pode importar classes de inventário quando modificar as predefinições de cliente. No entanto, pode utilizar configurações personalizadas do cliente para importar informações que não incluam uma alteração de esquema, como alterar a propriedade de uma classe existente de **True** to **False**.  

1.  Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** >  **configurações**padrão do cliente .  

4.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

5.  Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

6.  Na lista de Definições do **Dispositivo,** escolha **Definições**.  

7.  Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Import**.  

8.  Na caixa de diálogo **Import,** selecione o ficheiro 'Formato de Objeto Gerido' (MOF) que pretende importar e, em seguida, escolha **OK**. Reveja os itens que serão importados e, em seguida, clique **em Importar**.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  Na consola 'Gestor de Configuração', escolha as**definições** > padrão do cliente de **'' ''' '',** > **configurações**padrão do cliente .  

4.  No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

5.  Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

6.  Na lista de Definições do **Dispositivo,** escolha **Definições**.  

7.  Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Export .**  

    > [!NOTE]  
    >  Quando exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  Na caixa de diálogo **exportação,** especifique o ficheiro 'Formato de Objeto Gerido' (MOF) para o qual pretende exportar as classes e, em seguida, escolha **Guardar**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Configure o inventário de hardware para recolher cordas maiores que 255 caracteres
A partir do Diretor de Configuração 1802, pode especificar o comprimento das cordas a ser superior a 255 caracteres para propriedades de inventário de hardware. Esta alteração aplica-se apenas a classes recém-adicionadas e a propriedades de inventário de hardware que não são chaves. <!-- 1357389 -->

1. No espaço de trabalho **da Administração,** clique em **Definições de Cliente** realçar uma definição de dispositivo cliente para editar, clique no clique direito e, em seguida, selecione **Propriedades**.

2. Selecione **inventário de hardware,** em **seguida, definir classes,** e **adicionar**.

3. Clique no botão **Ligar.**

4. Preencha o **nome do computador**, espaço de nome **WMI,** selecione **recursivo** se necessário. Forneça credenciais se necessário para se ligar. Clique em **Ligar** para ver as classes espaço de nome.

5. Selecione uma nova classe e, em seguida, clique em **Editar**.

6. Altere o **comprimento** da sua propriedade que é uma corda, além da chave, para ser superior a 255. Clique em **OK**. 

7. Certifique-se de que a propriedade editada é selecionada para Adicionar Classe de Inventário de **Hardware** e clique em **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como Utilizar Ficheiros MIF (Management Information Files) para expandir o inventário de hardware  
 Utilize ficheiros de Formato de Informação de Gestão (MIF) para alargar as informações de inventário de hardware recolhidas junto dos clientes pelo Gestor de Configuração. Durante o inventário de hardware, as informações armazenadas em ficheiros MIF são adicionadas ao relatório de inventário de cliente e armazenadas na base de dados do site, onde pode utilizar os dados da forma mesmo que utiliza dados de inventário de cliente predefinido. Existem dois tipos de ficheiros MIF, NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Antes de poder adicionar informações dos ficheiros MIF à base de dados do Gestor de Configuração, tem de criar ou importar informações de classe para eles. Para mais informações, consulte as secções [Para adicionar uma nova classe](#BKMK_Add) de inventário e para importar aulas de inventário de [hardware](#BKMK_Import) neste artigo.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Para criar ficheiros NOIDMIF  
 Os ficheiros NOIDMIF podem ser usados para adicionar informações a um inventário de hardware do cliente que normalmente não pode ser recolhido pelo Gestor de Configuração e está associado a um determinado dispositivo cliente. Por exemplo, muitas empresas rotulam cada computador da organização com um número de ativo e, em seguida, catalogam estes números manualmente. Quando cria um ficheiro NOIDMIF, estas informações podem ser adicionadas à base de dados do Gestor de Configuração e ser utilizadas para consultas e reportagens. Para obter informações sobre a criação de ficheiros NOIDMIF, consulte a documentação SDK do Gestor de Configuração.  

> [!IMPORTANT]  
>  Quando cria um ficheiro NOIDMIF, deve ser guardado num formato codificado ANSI. Os ficheiros NOIDMIF guardados no formato codificado UTF-8 não podem ser lidos pelo Gestor de Configuração.  

 Depois de criar um ficheiro NOIDMIF, guarde-o na pasta _%Windir%_**\CCM\Inventory\Noidmifs** em cada cliente. O Gestor de Configuração irá recolher informações de ficheiros NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> Para criar ficheiros IDMIF  
 Os ficheiros IDMIF podem ser usados para adicionar informações sobre ativos que normalmente não poderiam ser inventariados pelo Gestor de Configuração e não estão associados a um determinado dispositivo cliente, à base de dados do Gestor de Configuração. Por exemplo, você poderia usar IDMIFS para recolher informações sobre projetores, leitores de DVD, fotocopiadoras ou outros equipamentos que não tenham um cliente de Configuração Manager. Para obter informações sobre a criação de ficheiros IDMIF, consulte a documentação SDK do Gestor de Configuração.  

 Depois de criar um ficheiro IDMIF, guarde-o na pasta _%Windir%_**\CCM\Inventory\Idmifs** nos computadores dos clientes. O Gestor de Configuração irá recolher informações deste ficheiro durante o próximo ciclo de inventário de hardware agendado. Tem de declarar as novas classes relativamente a informações incluídas no ficheiro adicionando ou importando as mesmas.  

> [!NOTE]
> Os ficheiros MIF podem conter grandes quantidades de dados e a recolha destes dados pode afetar negativamente o desempenho do seu site. Ative a recolha mif apenas quando necessário e configure a opção **Tamanho máximo de ficheiro personalizado MIF (KB)** nas definições de inventário de hardware. Para mais informações, consulte Introdução ao inventário de [hardware](introduction-to-hardware-inventory.md).
