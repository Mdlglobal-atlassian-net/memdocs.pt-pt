---
title: Pré-requisitos para perfis Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos para gerir perfis Wi-Fi e perfis VPN no Gestor de Configuração
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722131"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Pré-requisitos para perfis Wi-Fi e VPN no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os perfis Wi-Fi e VPN no Gestor de Configuração têm dependências apenas dentro do produto.

Necessita das seguintes permissões de segurança para gerir as definições de acesso aos recursos da empresa, tais como perfis de certificado, perfis Wi-Fi e perfis VPN:  

- Para visualizar e gerir alertas e relatórios para Wi-Fi e perfis: **Criar**, **Eliminar,** **Modificar,** **Modificar Relatório,** **Ler**e **Executar relatório** para o objeto **alertas.**  

- Para criar e gerir perfis de certificado: **Política de Autor,** **Relatório de Modificação,** **Ler**e **Executar Relatório** para o objeto de perfil de **certificado.**  

- Para gerir as implementações de perfis Wi-Fi, certificado e VPN: Implementar políticas de **configuração,** modificar o alerta de **estado do cliente,** **ler**e **ler recursos** para o objeto **de recolha.**  

- Para gerir todas as políticas de configuração: **Criar**, **Eliminar,** **Modificar,** **Ler**e **Definir o âmbito** de segurança para o objeto de política de **configuração.**  

- Para executar consultas relacionadas com perfis Wi-Fi e VPN: **Leia** a permissão para o objeto **Deconsulta.**  

- Para ver informações de perfis Wi-Fi e VPN na consola Do Gestor de Configuração: **Leia** a permissão para o objeto **do Site.**  

- Para visualizar mensagens de estado para perfis Wi-Fi e VPN: **Leia** a permissão para o objeto **'Mensagens** de Estado'.  

- Para criar e modificar o perfil de certificado DE CA fidedigno: Política de **Autor,** **Relatório de Modificação,** **Leitura**e Relatório **de Execução** para o objeto de perfil de **certificado de certificado de CA fidedigno.**  

- Para criar e gerir perfis VPN: **Política de Autor,** **Modificar Relatório,** **Ler**e **Executar Relatório** para o objeto de **perfil VPN.**  

- Para criar e gerir perfis Wi-Fi: Política de **Autor,** **Modificar relatório,** **Ler**e **Executar relatório** para o objeto de **perfil Wi-Fi.**  

A função de segurança incorporada do Gestor de Acesso a Recursos da **Empresa** inclui estas permissões que são necessárias para gerir perfis Wi-Fi no Gestor de Configuração. Para mais informações, consulte [a configuração de segurança](../../core/plan-design/security/configure-security.md).
