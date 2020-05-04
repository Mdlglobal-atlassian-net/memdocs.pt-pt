---
title: Avaliar em ambiente de laboratório
titleSuffix: Configuration Manager
description: Crie um ambiente de laboratório para avaliar o Gestor de Configuração para uso na sua organização.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd238319ba064f57911eee58e1299e17a2ce5b60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713843"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o Gestor de Configuração construindo o seu próprio ambiente de laboratório

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Aprenda a criar um ambiente de laboratório para avaliar o Gestor de Configuração para uso na sua organização.  

 O Gestor de Configuração é uma ferramenta complexa e poderosa para gerir os seus utilizadores, dispositivos e software. É uma boa ideia avaliar cuidadosamente o Gestor de Configuração antes da implementação completa, para que possa sacar a compreensão conceptual com exercícios práticos.  

 Este guia destina-se principalmente a administradores que estão a avaliar a utilização do Gestor de Configuração em ambientes corporativos:  

-   Administradores que querem uma solução para gerir totalmente Computadores, servidores e dispositivos móveis  

-   Administradores em indústrias de alta segurança que exigem a segurança da gestão de dispositivos no local com a flexibilidade da gestão de dispositivos baseados na nuvem  

-   Administradores que querem gerir a escala ção da sua arquitetura de servidor no local  

## <a name="what-this-lab-does"></a>O que faz este laboratório  
 O principal objetivo de criar este ambiente de laboratório é dar-lhe o conhecimento geral para começar a trabalhar com o Gestor de Configuração, e melhorar a sua compreensão do Gestor de Configuração. Você vai passar por um conjunto acelerado da versão atual do Gestor de Configuração, usando dois servidores:  

-   Um que acolhe o Ative Directory, o controlador de domínio e o servidor DNS  

-   Um que acolhe o Gestor de Configuração e todos os componentes associados do Servidor SQL  

As máquinas cliente estão instaladas no Hyper-V. O próprio laboratório também pode ser executado como um sistema totalmente virtualizado num único servidor.  

## <a name="what-this-lab-does-not-do"></a>O que não faz este laboratório  
 Este laboratório não vai levá-lo a todos os cenários do Diretor de Configuração. Não foi concebido para ser imediatamente migrado para um ambiente ativo.  

 Quando criar este laboratório, terá um ambiente funcional para utilizar. Mas este ambiente não será otimizado para fatores como o desempenho do sistema, a gestão do espaço em disco rígido e o armazenamento do SQL Server.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a>Leitura recomendada antes de construir o laboratório  
 Existe uma grande quantidade de conteúdos disponíveis em Documentação para Gestor de [Configuração.](https://docs.microsoft.com/sccm/) Recomendamos que leia os seguintes tópicos desta biblioteca antes de começar a construir o laboratório:  

-   Conheça conceitos fundamentais sobre a consola do Gestor de Configuração, portais de utilizador final e cenários de exemplo na [Introdução ao Gestor de Configuração](../../core/understand/introduction.md).  

-   Conheça as principais capacidades de gestão do Gestor de Configuração em [Funcionalidades e capacidades de Configuração Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Reforce os seus conhecimentos com [fundamentos de Gestor de Configuração.](../../core/understand/fundamentals.md)  

-   Saiba a importância das funções de segurança nos [fundamentos da administração baseada em papéis para o Gestor de Configuração](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Conheça a gestão de conteúdos em [Conceitos para gestão](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)de conteúdos.  

-   Saiba como suportar com sucesso tarefas diárias durante a sua implementação em [Compreender como os clientes encontram recursos e serviços](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)do site para O Gestor de Configuração .  
