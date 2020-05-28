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
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427707"
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

## <a name="methods"></a>Métodos

### <a name="enable-or-disable"></a>Ativar ou desativar

Ativar ou desativar alguns de todos os atributos de uma classe que já existe no cliente. Esta ação instrui o agente de inventário de hardware a recolhê-lo em clientes. Pode fazer esta ação em definições padrão do cliente ou configurações personalizadas do cliente do dispositivo. Para mais informações, consulte [Enable ou desative as classes de inventário existentes](#BKMK_Enable).

### <a name="add"></a>Adicionar

Se existe uma classe WMI no cliente e é conhecida do site, esta ação inclui-a ao possível conjunto de aulas de inventário de hardware. Pode adicionar uma nova classe de inventário a partir do espaço de nomes WMI de outro dispositivo. Esta ação está apenas nas definições padrão do cliente. Para mais informações, consulte [Adicionar uma nova classe](#BKMK_Add)de inventário .

### <a name="extend"></a>Extensão

Adicione uma nova classe WMI ao cliente. Para estender manualmente o inventário de hardware, edite a configuração.mof no site de alto nível.<!-- SCCMDocs#1073 -->

Se a classe WMI já não existir no cliente, precisa de estender o esquema wMI:

1. Editar a configuração.mof no site de alto nível. Reveja **dataldr.log** para ver o site adicioná-lo.

1. Refresque a política de um cliente, e espere que a nova classe compile.

1. Utilize as definições padrão do cliente para [adicionar](#add) a nova classe ao inventário de hardware. Não tem de ativar esta classe nas definições padrão do cliente. Em seguida, pode activar-o numa definição personalizada do cliente do dispositivo.

### <a name="import-and-export"></a>Importação e exportação

Utilize a consola do Gestor de Configuração para importar e exportar ficheiros de formato de objeto gerido (MOF) que contenham classes de inventário. Para mais informações, consulte as classes de inventário de [hardware de importação](#BKMK_Import) e as aulas de inventário de [hardware de exportação.](#BKMK_Export)

### <a name="create-noidmif-files"></a>Criar Ficheiros NOIDMIF

Utilize ficheiros NOIDMIF para recolher informações sobre dispositivos clientes que o Gestor de Configuração não pode inventariar. Por exemplo, recolher informações sobre o número do ativo do dispositivo que existem apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é associado automaticamente ao dispositivo cliente a partir do qual foi recolhido. Para mais informações, consulte [Create NOIDMIF files](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>Criar Ficheiros IDMIF

Utilize ficheiros IDMIF para recolher informações sobre ativos na sua organização que não estejam associados a um cliente do Gestor de Configuração. Por exemplo, projetores, fotocopiadoras e impressoras de rede. Para mais informações, consulte [Create IDMIF files](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para expandir o inventário de hardware

Estes procedimentos ajudam a configurar as predefinições de cliente para o inventário de hardware e aplicam-se a todos os clientes na sua hierarquia. Se quiser que estas definições se apliquem apenas a alguns clientes, crie uma definição personalizada de dispositivo de cliente e atribua-a a uma coleção de clientes específicos. Para mais informações, consulte [Como configurar as definições do cliente](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Ativar ou desativar as classes de inventário existentes  

1. Na consola 'Gestor de Configuração', escolha as definições padrão do cliente de **'' ''' '',**  >  **Client Settings**  >  **configurações**padrão do cliente .  

1. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

1. Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

1. Na lista de Definições do **Dispositivo,** selecione **Definir Classes**.  

1. Na caixa de diálogo **Classes de Inventário de Hardware** , selecione ou desmarque as classes e propriedades de classes que pretende que sejam recolhidas pelo inventário de hardware. Pode expandir classes para selecionar ou desmarcar propriedades individuais dentro dessa classe. Utilize o campo **Procurar classes de inventário** para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando adicionar novas classes ao inventário de hardware do Gestor de Configuração, o tamanho do ficheiro de inventário que é recolhido e enviado para o servidor do site aumentará. Isto pode afetar negativamente o desempenho do site do seu gestor de rede e configuração. Ative apenas as classes de inventário que pretende recolher.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Adicione uma nova classe de inventário  

Só pode adicionar classes de inventário do servidor de alto nível da hierarquia modificando as definições padrão do cliente. Esta opção não está disponível quando cria definições personalizadas do dispositivo.

1. Na consola 'Gestor de Configuração', escolha as definições padrão do cliente de **'' ''' '',**  >  **Client Settings**  >  **configurações**padrão do cliente .  

1. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

1. Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

1. Na lista de Definições do **Dispositivo,** escolha **Definições**.  

1. Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Adicionar**.  

1. Na caixa de diálogo de classificação de **hardware Add,** selecione **Connect**.  

1. Na caixa de diálogo **Connect to Windows Management Instrumentation (WMI),** especifique o nome do computador a partir do qual irá recuperar as classes WMI e o espaço de nome WMI para a recuperação das aulas. Se quiser recuperar todas as classes abaixo do espaço de nome WMI que especificou, selecione **Recursive**. Se o computador a que está a ligar não for o computador local, forneça credenciais para uma conta que tenha permissão para aceder ao WMI no computador remoto.

1. Escolha **Connect** (Ligar).  

1. Na caixa de diálogo **Add Hardware Inventory Class,** na lista de **classes de Inventário,** selecione as classes WMI que pretende adicionar ao inventário de hardware do Gestor de Configuração.  

1. Se pretender editar informações sobre a classe WMI selecionada, escolha **Editar,** e na caixa de diálogo de **qualificação de classe,** forneça as seguintes informações:  

    - **Nome do ecrã**: Este nome será apresentado no Resource Explorer.  

    - **Propriedades**: Especifique as unidades em que cada propriedade da classe WMI será exibida.  

      Você também pode definir propriedades como uma propriedade chave para ajudar a identificar exclusivamente cada instância da classe. Se não for definida qualquer chave para a classe e várias instâncias da classe forem comunicadas a partir do cliente, apenas a instância mais recente encontrada é armazenada na base de dados.  

      Quando terminar de configurar as propriedades, selecione **OK** para fechar a caixa de diálogo de **qualificação classe** e os outros diálogos abertos.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Importações de classes de inventário de hardware

Só pode importar classes de inventário quando modificar as predefinições de cliente. No entanto, pode utilizar configurações personalizadas do cliente para importar informações que não incluam uma alteração de esquema, como alterar a propriedade de uma classe existente de **True** to **False**.  

1. Na consola 'Gestor de Configuração', escolha as definições padrão do cliente de **'' ''' '',**  >   **Client Settings**  >  **configurações**padrão do cliente .

1. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

1. Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

1. Na lista de Definições do **Dispositivo,** escolha **Definições**.  

1. Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Import**.  

1. Na caixa de diálogo **Import,** selecione o ficheiro 'Formato de Objeto Gerido' (MOF) que pretende importar e, em seguida, escolha **OK**. Reveja os itens que serão importados e, em seguida, selecione **Import**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Aulas de inventário de hardware de exportação  

1. Na consola 'Gestor de Configuração', escolha as definições padrão do cliente de **'' ''' '',**  >  **Client Settings**  >  **configurações**padrão do cliente .  

1. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.  

1. Na caixa de diálogo Predefinido de Definições de **Cliente,** escolha inventário de **hardware**.  

1. Na lista de Definições do **Dispositivo,** escolha **Definições**.  

1. Na caixa de diálogo de aulas de inventário de **hardware,** escolha **Export .**  

    > [!NOTE]  
    > Quando exporta classes, todas as classes atualmente selecionadas serão exportadas.  

1. Na caixa de diálogo **exportação,** especifique o ficheiro 'Formato de Objeto Gerido' (MOF) para o qual pretende exportar as classes e, em seguida, escolha **Guardar**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Configure o inventário de hardware para recolher cordas maiores que 255 caracteres

Pode especificar o comprimento das cordas a mais de 255 caracteres para propriedades de inventário de hardware. Esta ação aplica-se apenas a classes recém-adicionadas e a propriedades de inventário de hardware que não são chaves. <!-- 1357389 -->

1. No espaço de trabalho da **Administração,** selecione **Definições de Cliente**. Escolha uma definição de dispositivo cliente para editar e, em seguida, selecione **Propriedades**.

1. Selecione **inventário de hardware,** em **seguida, definir classes,** e **adicionar**.

1. Selecione **Ligar**.

1. Preencha o **nome do computador**, espaço de nome **WMI,** selecione **recursivo** se necessário. Forneça credenciais se necessário para se ligar. Selecione **Ligar** para visualizar as classes espaço de nome.

1. Selecione uma nova classe e, em seguida, **selecione Editar**.

1. Mude o **comprimento** da sua propriedade que é uma corda, além da chave, para ser maior que 255. Selecione **OK**.

1. Certifique-se de que a propriedade editada está selecionada para adicionar classe de inventário de **hardware,** e selecione **OK**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Utilize ficheiros MIF para alargar o inventário de hardware

Utilize ficheiros de Formato de Informação de Gestão (MIF) para alargar as informações de inventário de hardware recolhidas junto dos clientes pelo Gestor de Configuração. Durante o inventário de hardware, as informações armazenadas em ficheiros MIF são adicionadas ao relatório de inventário de cliente e armazenadas na base de dados do site, onde pode utilizar os dados da forma mesmo que utiliza dados de inventário de cliente predefinido. Existem dois tipos de ficheiros MIF: NOIDMIF e IDMIF.

> [!IMPORTANT]  
> Antes de poder adicionar informações dos ficheiros MIF à base de dados do Gestor de Configuração, tem de criar ou importar informações de classe para eles. Para mais informações, consulte as secções [Para adicionar uma nova classe](#BKMK_Add) de inventário e para importar aulas de inventário de [hardware](#BKMK_Import) neste artigo.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>Criar ficheiros NOIDMIF

Os ficheiros NOIDMIF podem ser usados para adicionar informações a um inventário de hardware do cliente que normalmente não pode ser recolhido pelo Gestor de Configuração e está associado a um determinado dispositivo cliente. Por exemplo, muitas empresas rotulam cada computador da organização com um número de ativo e, em seguida, catalogam estes números manualmente. Quando cria um ficheiro NOIDMIF, estas informações podem ser adicionadas à base de dados do Gestor de Configuração e ser utilizadas para consultas e reportagens. Para obter informações sobre a criação de ficheiros NOIDMIF, consulte a documentação SDK do Gestor de Configuração.  

> [!IMPORTANT]  
> Quando cria um ficheiro NOIDMIF, deve ser guardado num formato codificado ANSI. Os ficheiros NOIDMIF guardados no formato codificado UTF-8 não podem ser lidos pelo Gestor de Configuração.  

Depois de criar um ficheiro NOIDMIF, guarde-o na `%Windir%\CCM\Inventory\Noidmifs` pasta de cada cliente. O Gestor de Configuração irá recolher informações de ficheiros NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a>Criar ficheiros IDMIF

Os ficheiros IDMIF podem ser usados para adicionar informações sobre ativos que normalmente não poderiam ser inventariados pelo Gestor de Configuração e não estão associados a um determinado dispositivo cliente, à base de dados do Gestor de Configuração. Por exemplo, você poderia usar IDMIFS para recolher informações sobre projetores, leitores de DVD, fotocopiadoras ou outros equipamentos que não tenham um cliente de Configuração Manager. Para obter informações sobre a criação de ficheiros IDMIF, consulte a documentação SDK do Gestor de Configuração.  

Depois de criar um ficheiro IDMIF, guarde-o na `%Windir%\CCM\Inventory\Idmifs` pasta nos computadores dos clientes. O Gestor de Configuração irá recolher informações deste ficheiro durante o próximo ciclo de inventário de hardware agendado. Declarar novas classes para informações contidas no ficheiro, adicionando-as ou importando-as.  

> [!NOTE]
> Os ficheiros MIF podem conter grandes quantidades de dados e a recolha destes dados pode afetar negativamente o desempenho do seu site. Ative a recolha mif apenas quando necessário e configure a opção **Tamanho máximo de ficheiro personalizado MIF (KB)** nas definições de inventário de hardware. Para mais informações, consulte Introdução ao inventário de [hardware](introduction-to-hardware-inventory.md).
