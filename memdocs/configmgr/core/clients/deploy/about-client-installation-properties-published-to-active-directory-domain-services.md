---
title: Propriedades de instalação de clientes em Diretório Ativo
titleSuffix: Configuration Manager
description: Publique propriedades de instalação de clientes do Gestor de Configuração para Serviços de Domínio de Diretório Ativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712072"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Sobre propriedades de instalação de clientes publicadas nos Serviços de Domínio de Diretório Ativo

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando estende o esquema de Diretório Ativo para Gestor de Configuração, e o site é publicado para Ative Directory Domain Services, muitas propriedades de instalação de clientes são publicadas para Ative Directory Domain Services. Se um computador conseguir localizar estas propriedades de instalação do cliente, pode usá-las durante a implementação do cliente do Gestor de Configuração.  

 As vantagens da utilização dos Serviços de Domínio do Active Directory para publicação das propriedades de instalação do cliente incluem:  

-   As instalações de clientes baseadas em pontos de atualização de software e as instalações de clientes da Política de Grupo não requerem parâmetros de configuração em cada computador.  

-   Como estas informações são geradas automaticamente, o risco de erro humano associado à introdução manual das propriedades de instalação é eliminado.  

> [!NOTE]  
>  Para obter mais informações sobre como estender o esquema de Diretório Ativo para Gestor de Configuração e como publicar um site, consulte [as extensões schema para O Gestor](../../plan-design/network/schema-extensions.md)de Configuração .  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propriedades de instalação de clientes publicadas nos Serviços de Domínio de Diretório Ativo  
Segue-se uma lista de propriedades de instalação de clientes. Para mais informações sobre cada item listado abaixo, consulte sobre as propriedades de [instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

- O código de site do Gestor de Configuração.  

- O certificado de assinatura do servidor do site.  

- A chave de raiz fidedigna.  

- As portas de comunicação de cliente para HTTP e HTTPS.  

- O ponto de estado de contingência. Se o site tiver vários pontos de estado de recuo, apenas o primeiro que foi instalado é publicado nos Serviços de Domínio do Diretório Ativo.  

- Uma definição para indicar que o cliente terá de comunicar utilizando apenas HTTPS.  

- Definições relacionadas com os certificados PKI:  

  -   Se deverá ser utilizado um certificado PKI de cliente.  

  -   Os critérios de seleção para a seleção de certificados. Isto pode ser exigido porque o cliente tem mais do que um certificado PKI válido que pode ser usado para O Gestor de Configuração.  

  -   Uma definição para determinar qual o certificado a utilizar se o cliente tiver vários certificados válidos após o processo de seleção de certificados.  

  -   A lista de emissores de certificados que contém uma lista de certificados de AC de raiz fidedigna.  

- As propriedades de instalação client.msi especificadas no separador **Cliente** da caixa de diálogo **Propriedades da Instalação Push do Cliente** .

A instalação do cliente (CCMSetup) utiliza as propriedades que são publicadas nos Serviços de Domínio de Diretório Ativo apenas se nenhuma outra propriedade for especificada utilizando qualquer uma das seguintes propriedades:  

-   O método de instalação manual (descrito mais tarde neste artigo)

-   O método de instalação da política de grupo (descrito mais tarde neste artigo)

> [!NOTE]  
>  As propriedades de instalação do cliente são usadas para instalar o cliente. Estas propriedades podem ser substituídas com novas definições do seu site atribuído após a instalação do cliente e foi atribuída com sucesso a um site do Gestor de Configuração.  

 Utilize os detalhes nas seguintes secções para determinar quais os métodos de instalação do cliente do Gestor de Configuração que utilizam os Serviços de Domínio do Diretório Ativo para obter propriedades de instalação do cliente.  

## <a name="client-push-installation"></a>Instalação push do cliente  
 A instalação push do cliente não utiliza Serviços de Domínio do Active Directory para obter as propriedades de instalação.  

 Em vez disso, pode especificar as propriedades de instalação do cliente no separador Propriedades de **Instalação** da caixa de diálogo **Client Push Installation Properties.** Estas opções e definições do site relacionadas com o cliente são armazenadas num ficheiro lido pelo cliente durante a instalação de cliente.  

> [!NOTE]  
>  Não tem de especificar quaisquer propriedades CCMSetup para a instalação do impulso do cliente, ou o ponto de estado de recuo, ou a chave raiz fidedigna no separador Propriedades de **Instalação.** Estas definições são automaticamente fornecidas aos clientes quando são instaladas utilizando a instalação de impulso do cliente.
Além das propriedades Client.msi, a CCMSetup suporta os seguintes parâmetros: /forcereboot, /skipprereq, /logon, /BITSPriority, /downloadtimeout, /forceinstall

 Quaisquer propriedades que especifique no separador Propriedades de **Instalação** são publicadas nos Serviços de Domínio do Diretório Ativo se o site for publicado nos Serviços de Domínio do Diretório Ativo. Estas definições são lidas pelas instalações de cliente em que o CCMSetup seja executado sem propriedades de instalação.  

## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  
 O método de instalação baseada em pontos de atualizações de software não suporta a adição de propriedades de instalação à linha de comandos CCMSetup.  

 Se não tiverem sido aprovisionadas propriedades de linha de comandos no computador cliente utilizando a Política de Grupo, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio do Active Directory.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 O método de instalação de Política de Grupo não suporta a adição de propriedades de instalação à linha de comandos CCMSetup.  

 Se não tiverem sido aprovisionadas propriedades de linha de comandos no computador cliente, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio do Active Directory.  

## <a name="manual-installation"></a>Instalação manual  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="software-distribution-installation"></a>Instalação de distribuição de software  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Instalações para clientes que não podem aceder a Serviços de Domínio de Diretório Ativo  
Estes computadores clientes não conseguem ler ou aceder às propriedades de instalação publicadas dos Serviços de Domínio do Diretório Ativo.

 Estes clientes incluem:  

-   Computadores de grupo de trabalho.  

-   Clientes que são atribuídos a um site de Gestor de Configuração que não seja publicado nos Serviços de Domínio do Diretório Ativo.  

-   Clientes que são instalados quando estão na Internet.  
