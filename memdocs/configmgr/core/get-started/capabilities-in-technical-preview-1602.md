---
title: Capacidades na Pré-visualização Técnica 1602
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074474"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1602 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1602. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a>Melhorias na gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS  
 O Gestor de Configuração pode ajudá-lo a gerir o iOS Activation Lock, uma funcionalidade da aplicação Find My iPhone para dispositivos iOS 7.1 e posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

- Desativar a aplicação Encontrar o Meu iPhone  

- Apagar o dispositivo  

- Reativar o dispositivo  

  O Gestor de Configuração pode solicitar o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posteriormente. Para dispositivos supervisionados, o Intune pode obter o código de desativação do Bloqueio de Ativação e enviá-lo diretamente para o dispositivo.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a>Melhorias ao Centro de Software na versão 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de máquina seleção de PC e utilizador do Centro de Software  
 Uma nova opção, **A Política de Sincronização** foi adicionada à página de manutenção de**computadores** **opções** > do Centro de Software que faz com que o PC refresque a sua máquina de Configuração e a sua política de utilizador.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a>Melhorias na manutenção do Windows 10  
 Na Pré-Visualização Técnica de 1602 adicionámos as seguintes melhorias para a manutenção do Windows 10:  

-   Novas opções de filtro para planos de manutenção.  Agora pode filtrar para **Linguagem,** **Obrigatório**e **Título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Ao selecionar a classificação **de Upgrades** para atualizações de software, é apresentado um diálogo de aviso para que saiba que o [hotfix 3095113](https://support.microsoft.com/kb/3095113) da WSUS é necessário para sincronizar com sucesso as atualizações de software e para que o Serviço de Assistência do Windows 10 funcione corretamente.  A partir do diálogo, pode ir ao artigo da base de conhecimento para o hotfix.  

-   As atualizações disponíveis do Windows 10 passam a ser apresentadas apenas no **Windows 10 A servir** \ **todas as atualizações** do Windows 10 da consola Do Gestor de Configuração. Estas atualizações já não são apresentadas no nó de **Atualizações** \ de**Software Todas as atualizações** de software.  

-   Os utilizadores finais que iniciarem um pacote de upgrade do Windows 10 serão solicitados com um diálogo que os permite saber que irão atualizar o seu sistema operativo.  
