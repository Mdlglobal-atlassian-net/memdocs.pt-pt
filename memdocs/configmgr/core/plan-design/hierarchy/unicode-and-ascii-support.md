---
title: Suporte de Unicode e ASCII
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte para caracteres Unicode e ASCII em objetos de Gestor de Configuração.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717553"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Suporte Unicode e ASCII no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração cria a maioria dos objetos utilizando caracteres Unicode. No entanto, vários objetos apenas suportam caracteres ASCII, ou têm outras limitações.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a>Objetos que usam caracteres ASCII

Quando cria os seguintes objetos, o Gestor de Configuração apenas suporta o conjunto de caracteres ASCII:  

- Código do site  

- Todos os nomes do servidor do sistema do site  

- As seguintes contas do Gestor de Configuração:  

    > [!NOTE]  
    > Estas contas suportam caracteres ASCII, e personagens RUS em um site que funciona em russo.  

    - Conta de instalação push do cliente  

    - Conta de ligação de pontode gestão  

    - Conta de acesso à rede  

    - Conta de acesso ao pacote  

    - Conta de remetente padrão  

    - Conta de instalação do sistema do site  

    - Conta de ligação de ponto de atualização de software  

    - Conta de servidor proxy de ponto de atualização de software  

    > [!NOTE]  
    > As contas que especifica para o suporte da administração baseada em papéis Unicode.  
    >
    > A conta de ponto de serviços de reporte suporta o Unicode, com exceção dos caracteres RUS.  

- Nome de domínio totalmente qualificado (FQDN) para servidores de sites e sistemas de site  

- Caminho de instalação para Gestor de Configuração  

- Nomes de instâncias do Servidor SQL  

- O caminho para as seguintes funções do sistema do site:  

    - Ponto de inscrição  

    - Ponto proxy de registo  

    - Ponto do Reporting Services  

    - Ponto de Migração de Estado  

- O caminho para as seguintes pastas:  

    - A pasta que armazena dados de migração do estado cliente  

    - A pasta que contém os relatórios do Gestor de Configuração  

    - A pasta que armazena a cópia de segurança do Gestor de Configuração  

    - A pasta que armazena os ficheiros de origem de instalação para configuração do site  

    - A pasta que armazena os downloads pré-requisitopara utilização por configuração  

- O caminho para os seguintes objetos:  

    - Site do IIS  

    - Caminho de instalação de aplicação virtual  

    - Nome de aplicação virtual  

- Boot media ISO nomes de ficheiros  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a>Limitações adicionais

Seguem-se limitações adicionais para conjuntos de caracteres suportados e versões linguísticas:  

- O Gestor de Configuração não suporta alterar o local do computador do servidor do site.  

- Uma autoridade de certificados empresariais (CA) não suporta nomes de computador de cliente que usam conjuntos de caracteres de duplo byte (DBCS). Os nomes de computador do cliente que pode utilizar são restringidos pela limitação pki do conjunto de caracteres IA5. O Gestor de Configuração não suporta nomes CA ou valores de nome de assunto que usam DBCS.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a>Objetos que não estão localizados

A base de dados do Gestor de Configuração suporta o Unicode para a maioria dos objetos que armazena. Sempre que possível, exibe esta informação na linguagem OS que corresponde ao local de um computador. Para que a interface do cliente ou a consola do Gestor de Configuração apresentem informações no idioma do SISTEMA do computador, o local do computador deve corresponder a um idioma de cliente ou servidor que instale num site.  

Vários objetos do Gestor de Configuração não suportam o Unicode. São armazenados na base de dados usando ASCII, ou têm limitações linguísticas adicionais. Esta informação é sempre exibida utilizando o conjunto de caracteres ASCII, ou na linguagem que estava em uso quando criou o objeto.  
