---
title: Suporte para domínios do Active Directory
titleSuffix: Configuration Manager
description: Conheça os requisitos para um sistema de site do Gestor de Configuração num domínio de Diretório Ativo.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709615"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Suporte para domínios de Diretório Ativo em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Todos os sistemas de site do Gestor de Configuração devem ser membros de um domínio de Diretório Ativo suportado. Os computadores clientes do Gestor de Configuração podem ser membros do domínio ou membros do grupo de trabalho.  

## <a name="requirements-and-limitations"></a>Requisitos e limitações

- A adesão ao domínio também se aplica a sistemas de site que suportam a gestão de clientes baseados na Internet numa rede de perímetro. (Estas redes também são conhecidas como DMZ, zona desmilitarizada e subrede selecionada).  

- Não é suportado para alterar as seguintes configurações para um computador que acolhe uma função do sistema de site:  

  - A desmembro do domínio, incluindo se remover um sistema de site do domínio, e depois voltar a juntar-se ao mesmo domínio.

  - Nome de domínio  

  - Nome do computador  

  Antes de efazer estas alterações, desinstale a função do sistema do site. Para efazer estas alterações num servidor de site, desinstale primeiro o site. Também pode considerar a criação de um servidor de [site em modo passivo](../../servers/deploy/configure/site-server-high-availability.md) para ajudar a gerir esta mudança num servidor de site.

- O Gestor de Configuração suporta o domínio e o nível funcional da floresta do Windows Server 2008 R2 ou posterior.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Espaço de nomes não contíguo

Pode instalar sistemas e clientes do Gestor de Configuração num domínio que tenha um espaço de *nome desarticulado.*  

Num espaço de nome disconjunto, o sufixo dNS primário de um computador não corresponde ao nome de domínio DNS do Diretório Ativo desse computador. Outro cenário de espaço de nome disconjunto ocorre se o nome de domínio NetBIOS de um controlador de domínio não corresponder ao nome de domínio DNS do Diretório Ativo.  

### <a name="disjoint-scenarios"></a>Cenários disconjuntos

As seguintes secções identificam os cenários suportados para um espaço de nome desarticulado.  

#### <a name="scenario-1"></a>Cenário 1

O sufixo DNS primário do controlador de domínio difere do nome de domínio DNS do Active Directory. Os computadores que são membros do domínio podem estar não contíguos ou contíguos.

O controlador de domínio está não contíguo neste cenário. Os computadores que são membros do domínio, tais como servidores de sites e computadores, podem ter um sufixo DNS primário que corresponde a ambos os jogos:

- O sufixo principal dNS do controlador de domínio
- O nome de domínio DNS do Diretório Ativo

#### <a name="scenario-2"></a>Cenário 2

Um computador membro num domínio de Diretório Ativo é disarticulado, mesmo que o controlador de domínio não seja desarticulado.

Neste cenário, o sufixo principal de DNS de um sistema de site difere do nome de domínio DNS do Diretório Ativo. O sufixo principal de DNS do controlador de domínio é o mesmo que o nome de domínio DNS do Diretório Ativo. Os computadores membros que são clientes do Gestor de Configuração podem ter um sufixo DNS primário que corresponde a ambos os jogos:

- O sufixo principal dNS do servidor do sistema de site disjoint
- O nome de domínio DNS do Diretório Ativo

### <a name="configure-disjoint-namespace"></a>Configurar espaço de nome sem articulação

Para permitir que um computador aceda a controladores de domínio que estejam desarticulados, altere o atributo ativo do Diretório Ativo **msDS-AllowedDNSSufixos** no recipiente de objetos de domínio. Adicione ambos os sufixos DNS ao atributo.  

Para se certificar de que a lista de pesquisa de *sufixo dNS* contém todos os espaços de nome DNS da organização, configure a lista de pesquisa de cada computador no domínio disconjunto. Incluir os seguintes sufixos na lista de espaços de nomes:

- O sufixo principal dNS do controlador de domínio
- O nome de domínio DNS
- Quaisquer espaços de nome adicionais para outros servidores com os quais o Gestor de Configuração possa comunicar

Pode utilizar a política de grupo para configurar a lista de pesquisa de sufixo do Sistema de **Nomede Domínio (DNS).**  

> [!IMPORTANT]  
> Quando fazer referência a um computador no 'Gestor de Configuração', introduza o computador utilizando o seu sufixo DNS primário. Este sufixo deve corresponder ao nome de domínio totalmente qualificado que está registado como o atributo **dnsHostName** no domínio do Diretório Ativo e o nome principal do serviço que está associado ao sistema.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Domínios de etiqueta única

O Gestor de Configuração suporta sistemas e clientes do site num domínio de etiqueta única quando os seguintes critérios são cumpridos:  

- Configure o domínio de etiqueta única nos Serviços de Domínio do Diretório Ativo com um espaço de nome DNS disconjunto que tenha um domínio de alto nível válido.  

  **Por exemplo:** O domínio de etiqueta única da Contoso está configurado para ter um espaço de nomes não contíguo no DNS de contoso.com. Quando especifica o sufixo DNS no Gestor de Configuração para um computador no domínio Contoso, especifice "Contoso.com" e não "Contoso".  

- As ligações do modelo de objeto de componente distribuído (DCOM) entre servidores do site no contexto do sistema devem ser bem sucedidas utilizando a autenticação Kerberos.  
