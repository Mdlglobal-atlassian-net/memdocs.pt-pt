---
title: Segurança migratória e privacidade
titleSuffix: Configuration Manager
description: Obtenha as melhores práticas de segurança e informações de privacidade para migração para o seu ambiente de filial do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ba1f41af778602fb95d268c071b5f0d1dde158c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712996"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Segurança e privacidade para migração para o gerente de configuração filial atual

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém boas práticas de segurança e informações de privacidade para migração para o seu ambiente de filial do Gestor de Configuração.  

## <a name="security-best-practices-for-migration"></a>Boas Práticas de Segurança para a Migração  
 Utilize as seguintes boas práticas de segurança para a migração.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Utilize a conta do computador para a conta de fornecedor de SMS do Site Fonte e a Conta de Servidor SQL do Site Fonte em vez de uma conta de utilizador.|Se tiver de utilizar uma conta de utilizador para a migração, remova os dados da conta quando a migração estiver concluída.|  
|Utilize o IPsec quando migrar conteúdo de um ponto de distribuição num site de origem para um ponto de distribuição no seu site de destino.|Embora o conteúdo migrado seja hashed para detetar adulteração, se os dados forem modificados durante a sua transferência, a migração falhará.|  
|Restringir e monitorizar os utilizadores administrativos que possam criar postos de trabalho migratórios.|A integridade da base de dados da hierarquia de destino depende da integridade dos dados que o utilizador administrativo opta por importar da hierarquia de origem. Além disso, este utilizador administrativo pode ler todos os dados da hierarquia de origem.|  

### <a name="security-issues-for-migration"></a>Questões de Segurança para as Migrações  
A migração tem as seguintes questões de segurança:  

-   Os clientes que estão bloqueados de um site de origem podem atribuir com sucesso à hierarquia de destino antes de o seu registo de clientes ser migrado.  

     Embora o Gestor de Configuração mantenha o estatuto bloqueado dos clientes que migra, o cliente pode atribuir com sucesso à hierarquia de destino se a atribuição ocorrer antes da migração do registo do cliente estar concluída.  

-   As mensagens de auditoria não são migradas.  

Quando migra dados de um site de origem para um site de destino, perde-se qualquer informação de auditoria da hierarquia de origem.  

## <a name="privacy-information-for-migration"></a>Informações sobre privacidade para migração  
 A migração descobre informações das bases de dados do site que identifica numa infraestrutura de origem e armazena estes dados na base de dados da hierarquia de destino. A informação que o Gestor de Configuração pode descobrir a partir de um site de origem ou hierarquia depende das funcionalidades que foram ativadas no ambiente de origem, bem como das operações de gestão que foram realizadas naquele ambiente de origem.  

 Para obter mais informações sobre segurança e privacidade, consulte um dos seguintes tópicos:  

-   Para obter mais informações sobre as informações de privacidade para O Gestor de Configuração 2007, consulte Segurança e Privacidade para O Gestor de [Configuração 2007](https://go.microsoft.com/fwlink/p/?LinkId=216450) na biblioteca de documentação Do Gestor de Configuração 2007.  

-   Para obter mais informações sobre as informações de privacidade para system center 2012 Configuration Manager, consulte [Security and Privacy for System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) na biblioteca de documentação do System Center 2012 Configuration Manager.  

-   Para mais informações sobre as informações de privacidade para O Gestor de Configuração, consulte segurança e privacidade para O Gestor de [Configuração](../../core/plan-design/security/security-and-privacy.md).  

Pode migrar alguns ou todos os dados suportados de um site de origem para uma hierarquia de destino.  

A migração não é ativada por padrão e requer vários passos de configuração. As informações sobre migração não são enviadas para a Microsoft.  

Antes de migrar dados de uma hierarquia de origem, considere os seus requisitos de privacidade.  
