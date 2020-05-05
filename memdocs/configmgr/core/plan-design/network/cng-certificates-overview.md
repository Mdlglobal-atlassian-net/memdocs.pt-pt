---
title: Descrição geral dos certificados CNG
titleSuffix: Configuration Manager
description: Saiba mais sobre os certificados de Encriptação próxima geração (CNG) para clientes e servidores do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4574b7ae97e8200da248a0b798677eacadb6229f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719835"
---
# <a name="cng-certificates-overview"></a>Descrição geral dos certificados CNG
<!-- 1356191 --> 

O Gestor de Configuração tem suporte limitado para os certificados de Criptografia: Certificados de Próxima Geração (CNG). Os clientes do Gestor de Configuração podem utilizar o certificado de autenticação do cliente PKI com chave privada no Fornecedor de Armazenamento de Chaves CNG (KSP). Com suporte kSP, os clientes do Gestor de Configuração suportam a chave privada baseada em hardware, como tPM KSP para certificados de autenticação de clientes PKI.

## <a name="supported-scenarios"></a>Cenários suportados
Pode utilizar modelos de certificados de [Encriptação API: Próxima Geração (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) para os seguintes cenários:

- Registo e comunicação do cliente com um ponto de gestão HTTPS   
- Distribuição de software e implementação de aplicações com um ponto de distribuição HTTPS   
- Implementação do sistema operativo  
- SDK de mensagens de cliente (com a tualização mais recente) e Procuração ISV   
- Configuração de Gateway de Gestão de Nuvem  

A partir da versão 1802, utilize certificados CNG para as seguintes funções de servidor ativadas por HTTPS: <!-- 1357314 -->   
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado     

A partir da versão 1806, utilize certificados CNG para as seguintes funções de servidor ativadas por HTTPS:

- Ponto de registo de certificado, incluindo o servidor NDES com o módulo de política do Gestor de Configuração <!--1357314-->

> [!NOTE]
> O GnC é retrocompatível com a Crypto API (CAPI). Os certificados CAPI continuam a ser suportados mesmo quando o suporte cng é ativado no cliente.

## <a name="unsupported-scenarios"></a>Cenários não suportados

Os seguintes cenários não são atualmente suportados:

- As seguintes funções de servidor não estão operacionais quando instaladas no modo HTTPS com um certificado CNG ligado ao web site em Serviços de Informação da Internet (IIS): 
    - Serviço web de catálogo de aplicações
    - Site do catálogo de aplicações
    - Ponto de inscrição  
    - Ponto proxy de registo  

- O Software Center não exibe aplicações e pacotes disponíveis que sejam implantados para recolhas de utilizadores ou grupos de utilizadores.

- Utilização de certificados CNG para criar um Ponto de Distribuição de Nuvem.

- Se o módulo de política NDES estiver a utilizar um certificado CNG para autenticação do cliente, a comunicação ao ponto de registo do certificado falha. 
    - Isto é suportado a partir da versão 1806 do Gestor de Configuração.

- Se especificar um certificado cng ao criar meios de sequência de tarefas, o assistente não cria meios de arranque.
    - Isto é suportado a partir da versão 1806 do Gestor de Configuração.

## <a name="to-use-cng-certificates"></a>Para utilizar certificados De GNC

Para utilizar certificados CNG, a sua autoridade de certificação (CA) precisa fornecer modelos de certificadocng para máquinas-alvo. Os detalhes do modelo variam de acordo com o cenário; todavia, são necessárias as seguintes propriedades:

- **Guia** de compatibilidade

    - **A Autoridade de Certificados** deve ser o Windows Server 2008 ou mais tarde. (Recomenda-se o Windows Server 2012.)

    - **O destinatário do certificado** deve ser windows Vista/Server 2008 ou mais tarde. (Recomenda-se o Windows 8/Windows Server 2012.)

- **Separador de criptografia**

    - **A categoria de fornecedor** deve ser **o Fornecedor de Armazenamento chave.** (obrigatório)
    - **O pedido deve utilizar um dos seguintes fornecedores:** deve ser o Fornecedor de Armazenamento de Chaves do **Software da Microsoft**. 

> [!NOTE]
> Os requisitos para o seu ambiente ou organização podem ser diferentes. Contacte o seu perito em PKI. O ponto importante a considerar é que um modelo de certificado deve usar um Fornecedor de Armazenamento chave para tirar partido do GNC.

Para obter os melhores resultados, recomendamos a construção do Nome do Assunto a partir de informações de Diretório Ativo. Utilize o **formato** de nome DNS para nome de assunto e inclua o nome DNS no nome de assunto alternativo. Caso contrário, deve fornecer estas informações quando o dispositivo se inscrever no perfil do certificado.
