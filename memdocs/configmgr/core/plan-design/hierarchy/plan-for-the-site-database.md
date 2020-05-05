---
title: Planeie a base de dados do site
titleSuffix: Configuration Manager
description: Considere a base de dados do site e a função do servidor de base de dados do site enquanto planeia a sua hierarquia do Gestor de Configuração.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a32f0a59a0b3ce3ad864fecf61fe7281b8ebbdd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720815"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Plano para a base de dados do site para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O servidor de base de dados do site é um computador que executa uma versão suportada do Microsoft SQL Server. O SQL Server é utilizado para armazenar informações para sites do Gestor de Configuração. Cada site numa hierarquia do Gestor de Configuração contém uma base de dados do site e um servidor que é atribuído ao servidor de base de dados do site.  

-   Para sites de administração central e sites primários, pode instalar o SQL Server no servidor do site, ou pode instalar o SQL Server num computador diferente do servidor do site.  

-   Para sites secundários, pode utilizar o SQL Server Express em vez de uma instalação completa do Servidor SQL. O servidor de base de dados deve, no entanto, ser executado no servidor de site secundário.  

-  Para a utilização do Grupo de Disponibilidade SQL, o Modelo de Recuperação da Base de Dados deve ser definido para FULL  

-  Para utilização do Grupo de Disponibilidade Não-SQL, o Modelo de Recuperação da Base de Dados deve ser definido como SIMPLE  

Mais informações sobre os modos de recuperação do SQL podem ser encontradas em Modelos de [Recuperação (Servidor SQL)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

As seguintes configurações do SQL Server podem ser utilizadas para alojar a base de dados do site:  

-   A instância predefinida do SQL Server  

-   Uma instância nomeada num único computador com o SQL Server  

-   Uma instância nomeada numa instância em cluster do SQL Server  

-   Um grupo de disponibilidade sQL Server AlwaysOn (começando com a versão 1602 do Gestor de Configuração)


Para alojar a base de dados do site, o Servidor SQL deve satisfazer os requisitos detalhados no [Suporte para versões SQL Server para O Gestor](../../../core/plan-design/configs/support-for-sql-server-versions.md)de Configuração .  



## <a name="remote-database-server-location-considerations"></a>Considerações de localização remota do servidor de dados  

Se utilizar um computador de servidor de base de dados remoto, certifique-se de que a ligação de rede interveniente é uma ligação de rede de alta disponibilidade e largura de banda. O servidor do site e algumas funções do sistema do site devem comunicar constantemente com o servidor remoto que está hospedando a base de dados do site.

-   A quantidade de largura de banda necessária para as comunicações para o servidor de base de dados depende de uma combinação de várias configurações diferentes de site e cliente. Por conseguinte, a largura de banda real necessária não pode ser adequadamente prevista.  

-   O número de computadores a executar o fornecedor de SMS e a ligar à base de dados do site aumenta os requisitos de largura de banda da rede.  

-   O computador que executa o Servidor SQL deve estar localizado num domínio que tenha confiança bidirecional com o servidor do site e todos os computadores que executam o Provedor SMS.  

-   Não é possível utilizar um SQL Server agrupado para o servidor de base de dados do site se a base de dados do site estiver localizada conjuntamente com o servidor do site.  


Normalmente, um servidor de sistema de site suporta funções do sistema do site a partir de apenas um único site do Gestor de Configuração. Pode, no entanto, utilizar diferentes instâncias do SQL Server, em servidores agrupados ou não agrupados que executam o SQL Server, para alojar uma base de dados de diferentes sites do Gestor de Configuração. Para suportar bases de dados de diferentes sites, é necessário configurar cada instância do SQL Server para utilizar portas exclusivas para a comunicação.  
