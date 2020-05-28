---
title: Criar consultas
titleSuffix: Configuration Manager
description: Descubra como criar e importar consultas em 'Gestor de Configuração'. Inclui consultas de exemplo e dicas.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f815394414167ad4f887c5970538eab22c931a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906151"
---
# <a name="create-queries-in-configuration-manager"></a>Criar consultas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve como criar e importar consultas em Gestor de Configuração.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a>Criar uma consulta  
 Utilize este procedimento para criar uma consulta no Gestor de Configuração.  

1.  Na consola 'Gestor de Configuração', **selecione Monitorização**.  

2.  No espaço de trabalho **de monitorização,** selecione **Consultas**. No separador **Home,** no grupo **Criar,** selecione **Create Query**.  

3.  No separador **Geral** do Assistente de **Consulta de Criação,** especifique um nome único e, opcionalmente, um comentário para a consulta.  

4.  Se pretender importar uma consulta existente para usar como base para a nova consulta, selecione **Import Query Statement**. Na caixa de diálogo **Browse Query,** selecione uma consulta que pretende importar e, em seguida, selecione **OK**.  

5.  Na lista **do Tipo de Objeto,** selecione o tipo de objeto que pretende que a consulta volte. Esta tabela descreve alguns exemplos dos tipos de objetos que pode procurar:  

    |Tipo de Objeto|Descrição|  
    |-----------------|-----------------|  
    |**Recurso de Sistema**|Utilize para procurar atributos típicos do sistema, como o nome NetBIOS de um dispositivo, a versão cliente, o endereço IP do cliente e informações de Serviços de Domínio de Diretório Ativo.|  
    |**Recurso User**|Utilize para procurar informações típicas do utilizador, como nomes de utilizadores, nomes de grupos de utilizadores e nomes de grupos de segurança.|  
    |**Implementação**|Usar para procurar atributos típicos de uma implementação, como o nome de implementação, o horário e a coleção para a a que foi implementado.|  

6.  **Selecione Editar Declaração** de Consulta para abrir a caixa de diálogo De Denominação de Consulta &lt; \> **Propriedades.**  

7.  No separador **Geral** da caixa de diálogo De Denominação De &lt; Consulta \> **Properties,** especifique os atributos que a consulta retorna e como devem ser exibidos. Selecione o **novo** ícone para adicionar um novo atributo. Também pode selecionar **A Linguagem de Consulta** de Mostrar para introduzir ou editar a consulta diretamente na Linguagem de Consulta WMI (WQL). Por exemplo, em consultas de WMI, consulte a secção de [consultas De Exemplo WQL](#BKMK_Example) neste artigo.  

    > [!TIP]  
    > Pode utilizar a seguinte documentação de referência para o ajudar a construir as suas próprias consultas WQL:  
    >   
    > -   [WQL (SQL para WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [Cláusula ONDE](https://docs.microsoft.com/windows/win32/wmisdk/where-clause)  
    > -   [Operadores da WQL](https://docs.microsoft.com/windows/win32/wmisdk/wql-operators)  

8.  No separador **Critério** da caixa de diálogo De identificação de Denominações de &lt; \> **Statement Properties** Consulta, especifique critérios que sejam utilizados para refinar os resultados da consulta. Por exemplo, você poderia devolver apenas recursos que têm um código de site de **XYZ**. Pode configurar vários critérios para uma consulta.  

    > [!IMPORTANT]  
    > Se criar uma consulta sem critérios, a consulta devolverá todos os dispositivos da coleção **Todos os Sistemas** .  

9. No separador **Joins** da caixa de diálogo De nome de &lt; consulta \> **Properties,** pode combinar dados de dois atributos diferentes nos resultados da consulta. Embora o Gestor de Configuração crie automaticamente adesão de consultas quando escolhe diferentes atributos para o seu resultado de consulta, o separador Joins fornece opções mais **avançadas.** O Gestor de Configuração suporta estas classes de atributos:  

    |Tipo de associação|Descrição|  
    |---------------|-----------------|  
    |Interna|Apresenta apenas resultados correspondentes. Sempre utilizado por juntas que são criadas automaticamente.|  
    |Esquerda|Apresenta todos os resultados para o atributo base e apenas os resultados correspondentes ao atributo de associação.|  
    |Direita|Apresenta todos os resultados para o atributo de adesão de adesão e apenas os resultados correspondentes para o atributo base.|  
    |Completa|Apresenta todos os resultados tanto para o atributo base como para o atributo de adesão.|  

     Para obter mais informações sobre como utilizar as operações de adesão, consulte a documentação do SQL Server.  

10. Selecione **OK** para fechar a caixa de diálogo De Denominação de &lt; Consulta \> **Properties.**  

11. No separador **Geral** do Assistente de **Consulta de Criação,** especifique que os resultados da consulta não se limitam aos membros de uma coleção, que se limitam aos membros de uma coleção especificada, ou que um pedido para uma coleção aparece cada vez que a consulta é executada.  

12. Conclua o assistente para criar a consulta. A nova consulta aparece no nó **de Consultas** no espaço de trabalho **de Monitorização.**  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a>Importar uma consulta  
 Utilize este procedimento para importar uma consulta para o Gestor de Configuração. Para obter informações sobre como exportar consultas, consulte [Como gerir consultas](../../../core/servers/manage/manage-queries.md).  

1.  Na consola 'Gestor de Configuração', **selecione Monitorização**.  

2.  No espaço de trabalho **de monitorização,** selecione **Consultas**. No separador **Home,** no grupo **Criar,** selecione **Objetos de Importação**.  

3.  Na página de Nome de **Ficheiro MOF** do Assistente de **Objetos importados,** selecione **Browse** para selecionar o ficheiro Formato de Objeto Gerido (MOF) que contém a consulta que pretende importar.  

4.  Reveja as informações sobre a consulta a importar e, em seguida, complete o assistente. A nova consulta aparece no nó **de Consultas** no espaço de trabalho **de Monitorização.**  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Esta secção contém consultas de wQL exemplo que pode usar na sua hierarquia ou modificar para outros fins. Para utilizar estas consultas, selecione **Mostrar Linguagem de Consulta** na caixa de diálogo De Declaração de Consulta **Properties.** Em seguida, copie e cole a consulta no campo de Declaração de **Consulta.**  

> [!TIP]  
> Utilize o caráter universal `%` para indicar qualquer cadeia de carateres. Por exemplo, devolve o `%Visio%` Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Computadores que executam o Windows 10

Utilize a seguinte consulta para devolver a versão do sistema operativo e o nome NetBIOS de todos os computadores com o Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computadores com um pacote de software específico instalado  

Utilize a seguinte consulta para devolver o nome NetBIOS e o nome do pacote de software de todos os computadores que tenham um pacote de software específico instalado. Este exemplo devolve todos os computadores com uma versão do Microsoft Visio instalada. `Microsoft%Visio%`Substitua-o pelo pacote de software que pretende consultar.  

> [!TIP]  
> Para procurar o pacote de software, esta consulta utiliza os nomes que são apresentados na lista de programas do Painel de Controlo do Windows.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computadores numa unidade organizacional específica de Serviços de Domínio ativo

Utilize a seguinte consulta para devolver o nome NetBIOS e o nome da unidade organizacional (OU) de todos os computadores numa ou especificada. Substitua o texto `OU Name` pelo nome da Ou que pretende consultar.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computadores com um nome NetBIOS específico

Utilize a seguinte consulta para devolver o nome NetBIOS de todos os computadores que começam com uma cadeia de carateres específica. Neste exemplo, a consulta devolve todos os computadores com um nome NetBIOS que começa com `ABC` .  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Dispositivos de um tipo específico

Os tipos de dispositivos são armazenados na base de dados do Gestor de Configuração sob a classe de recursos **sms_r_system** e o nome de atributo **AgenteEdition**. Utilize esta consulta para recuperar apenas os dispositivos que correspondem à edição do agente do tipo de dispositivo que especifica:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Utilize um destes valores para &lt; id do \> dispositivo:  

|Tipo de Dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Computador de secretária do Windows ou computador portátil|0|  
|Dispositivo baseado em Windows ARM (com o Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Computador Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Sistema intel em um chip|12|  
|Servidores Unix e Linux|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Os valores que não estão listados nesta tabela estão associados a dispositivos que já não são suportados.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Por exemplo, se quiser devolver apenas computadores Mac, utilize esta consulta:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Próximos passos

[Como gerir consultas](manage-queries.md)
