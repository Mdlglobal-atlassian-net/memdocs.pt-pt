---
title: Bloquear clientes
titleSuffix: Configuration Manager
description: Bloqueie o acesso do cliente à segurança do sistema utilizando o Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713241"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Determine se bloqueia clientes no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Se um computador cliente ou dispositivo móvel cliente deixar de ser confiável, pode bloquear o cliente na consola System Center 2012 Configuration Manager. Os clientes bloqueados são rejeitados pela infraestrutura do Gestor de Configuração para que não possam comunicar com os sistemas do site para descarregar a política, carregar dados de inventário ou enviar mensagens de estado ou estado.  

 O cliente deve ser bloqueado e desbloqueado a partir do site atribuído e não de um site secundário ou de um site de administração central.  

> [!IMPORTANT]  
>  Embora o bloqueio no 'Gestor de Configuração' possa ajudar a proteger o site do Gestor de Configuração, não confie nesta funcionalidade para proteger o site de computadores ou dispositivos móveis não confiáveis se permitir que os clientes se comuniquem com os sistemas do site utilizando http, porque um cliente bloqueado poderia voltar a juntar-se ao site com um novo certificado auto-assinado e ID de hardware. Em vez disso, utilize a funcionalidade de bloqueio para bloquear suportes de dados de arranque perdidos ou comprometidos, que utiliza para implementar sistemas operativos, e quando os sistemas de sites aceitam ligações de cliente por HTTPS.  

 Os clientes que acedem ao site utilizando o certificado de Proxy ISV não podem ser bloqueados. Para obter mais informações sobre o certificado ISV Proxy, consulte o Kit de Desenvolvimento de Software do Gestor de Configuração (SDK).  

 Se os seus sistemas do site aceitarem ligações de cliente por HTTPS e a sua infraestrutura de chaves públicas (PKI) suportar uma lista de revogação de certificados (CRL), considere sempre a revogação de certificados como a primeira linha de defesa contra certificados potencialmente comprometidos. Bloquear clientes no Gestor de Configuração oferece uma segunda linha de defesa para proteger a sua hierarquia.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Considerações para bloquear clientes  

-   Esta opção está disponível para ligações de cliente por HTTP e HTTPS, mas tem segurança limitada quando os clientes ligam aos sistemas do site por HTTP.  

-   Os utilizadores administrativos do Gestor de Configuração têm a autoridade para bloquear um cliente, e a ação é tomada na consola do Gestor de Configuração.  

-   A comunicação do cliente é rejeitada apenas da hierarquia do Gestor de Configuração.  

    > [!NOTE]  
    >  O mesmo cliente poderia registar-se com uma hierarquia de Gestor de Configuração diferente.  

-   O cliente está imediatamente bloqueado do site do Gestor de Configuração.  

-   Ajuda a proteger os sistemas do site contra computadores e dispositivos móveis potencialmente comprometidos.  

## <a name="considerations-for-using-certificate-revocation"></a>Considerações sobre como utilizar a revogação de certificados  

-   Esta opção está disponível para ligações de cliente do Windows por HTTPS se a infraestrutura de chaves públicas suportar uma lista de revogação de certificados (CRL).  

     Os clientes Mac efetuam sempre a verificação CRL e esta funcionalidade não pode ser desativada.  

     Embora os clientes de dispositivos móveis não utilizem listas de revogação de certificados para verificar os certificados dos sistemas do site, os seus certificados podem ser revogados e verificados pelo Gestor de Configuração.  

-   Os administradores de infraestruturas de chaves públicas têm autoridade para revogar um certificado, e a ação é tomada fora da consola do Gestor de Configuração.  

-   A comunicação do cliente a partir de qualquer computador ou dispositivo móvel que requeira este certificado de cliente pode ser rejeitada.  

-   É provável que haja um atraso entre a revogação de um certificado e a transferência pelos sistemas do site da lista de revogação de certificados (CRL) modificada.  

-   Para muitas implementações de PKI, este atraso pode demorar um dia ou mais. Por exemplo, nos Serviços de Certificados do Active Directory, o período de validade predefinido é uma semana para uma CRL completa e um dia para uma CRL de diferenças.  

-   Ajuda a proteger os sistemas do site e os clientes contra computadores e dispositivos móveis potencialmente comprometidos.  

    > [!NOTE]  
    >  É possível proteger ainda mais os sistemas do site que executam o IIS contra clientes desconhecidos, configurando uma lista fidedigna de certificados (CTL) no IIS.  
