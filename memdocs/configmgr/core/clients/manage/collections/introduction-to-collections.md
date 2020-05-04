---
title: Introdução de coleções
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao uso de coleções no Gestor de Configuração.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0665c6378ac81d6f6f254501760647048ce66b0b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714354"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Introdução a coleções em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As coleções ajudam-no a organizar recursos em unidades manejáveis. Pode criar coleções que correspondam às necessidades de gestão do seu cliente e realizar operações em vários recursos ao mesmo tempo. 

A maioria das tarefas de gestão dependem ou exigem a utilização de uma ou mais coleções. Embora possa utilizar a coleção incorporada de Todos os Sistemas, usá-la para tarefas de gestão não é uma boa prática. Crie coleções personalizadas para identificar mais especificamente os dispositivos ou utilizadores para uma tarefa.  

 As coleções incorporadas e personalizadas aparecem nos nós de **Recolha seleções** e Recolhas de **Dispositivos** do Utilizador na consola **De formação e** conformidade.  

 As coleções que viu recentemente aparecem no nó **dos Utilizadores** e no nó de **Dispositivos** no espaço de trabalho **De Ativos e Compliance.**  

Aqui estão alguns exemplos de uso de recolha:  

|Operação|Exemplo|  
|---------|-------|  
|Agrupar recursos|Pode criar coleções que agrupam recursos com base na hierarquia da sua organização.<br /><br /> Por exemplo, você poderia criar uma coleção de todos os computadores na Unidade De Gestão Ativa do Diretório Ativo (SEDe de Londres) (OU). Para obter mais informações sobre como criar este tipo de recolha, consulte [Como criar coleções.](../../../../core/clients/manage/collections/create-collections.md)<br /><br /> Pode utilizar esta recolha para operações como configurar as definições de Proteção de Pontofinal, configurar as definições de gestão de energia do dispositivo ou instalar o cliente do Gestor de Configuração.|  
|Implementação de aplicações|Pode criar uma coleção de todos os computadores que não tenham o Microsoft Office 2013 instalado e depois implementá-lo em todos os computadores dessa coleção.<br /><br /> Também pode utilizar os requisitos da aplicação para efetuar esta tarefa. Para mais informações, consulte [Como criar aplicações com o Gestor de Configuração](../../../../apps/deploy-use/create-applications.md).|  
|[Gerir definições de cliente](../../../../core/clients/deploy/about-client-settings.md)|Embora as predefinições de cliente no Configuration Manager sejam aplicadas a todos os dispositivos e todos os utilizadores, pode criar definições de cliente personalizadas e aplicáveis a uma coleção de dispositivos ou a uma coleção de utilizadores.<br /><br /> Por exemplo, se pretender que o controlo remoto esteja disponível em todos os dispositivos, mas em alguns dispositivos, configure as definições padrão do cliente para permitir o controlo remoto e, em seguida, configurar as definições personalizadas do cliente que não permitem o controlo remoto, e implemente-as para a recolha de clientes excecionais. |  
|[Gestão de energia](../power/introduction-to-power-management.md)|Pode configurar definições de potência específicas por coleção.|  
|[Administração baseada em funções](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Utilize coleções para controlar quais os grupos de utilizadores que têm acesso a várias funcionalidades na consola 'Gestor de Configuração'.|  
|[Janelas de manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Com janelas de manutenção pode definir um período de tempo em que várias operações do Gestor de Configuração podem ser realizadas em membros de uma coleção de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de coleções no Configuration Manager  
 O Gestor de Configuração tem coleções incorporadas para operações comuns, e também pode criar coleções personalizadas.   

### <a name="built-in-collections"></a>Coleções incorporadas  
 Por predefinição, o Gestor de Configuração inclui as seguintes coleções, que não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os Grupos de Utilizadores**|Contém os grupos de utilizadores que são detetados com a Deteção de Grupos de Segurança do Active Directory.|  
|**Todos os Utilizadores**|Contém os utilizadores que são detetados com a Deteção de Utilizadores do Active Directory.|  
|**Todos os Utilizadores e Grupos de Utilizadores**|Contém as coleções Todos os Utilizadores e Todos os Grupos de Utilizadores. Esta coleção contém o maior âmbito de recursos do grupo de utilizadores e utilizadores.|  
|**Todos os Clientes de Servidor e de Ambiente de Trabalho**|Contém os dispositivos de servidor e ambiente de trabalho que têm o cliente do Gestor de Configuração instalado. A associação é mantida pela Deteção Heartbeat.|  
|**Todos os Dispositivos Móveis**|Contém os dispositivos móveis que são geridos pelo Gestor de Configuração. A associação é restrita a esses dispositivos móveis atribuídos com êxito a um site ou detetados pelo conector do Exchange Server.|  
|**Todos os Sistemas**|Contém os Clientes All Desktop e Server, os All Mobile Devices e as coleções All Unknown Computers, e todos os dispositivos móveis que estão matriculados pela Microsoft Intune. Esta coleção contém o maior âmbito de recursos do dispositivo.|  
|**Todos os Computadores Desconhecidos**|Contém os registos de computadores genéricos para várias plataformas de computadores. Pode utilizar esta coleção para implementar um sistema operativo ao utilizar uma sequência de tarefas e arranque PXE, suportes de dados de arranque ou suportes de dados pré-configurados.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando cria uma coleção personalizada no Gestor de Configuração, a adesão a essa coleção é determinada por uma ou mais regras de recolha, como descrito em [Como criar coleções.](../../../../core/clients/manage/collections/create-collections.md) 

