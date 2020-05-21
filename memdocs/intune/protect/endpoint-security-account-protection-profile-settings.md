---
title: Intune endpoint security Account protection policy settings [ Microsoft Docs
description: Definições de política de proteção de conta de segurança endpoint no Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431411"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Definições de política de proteção de conta para segurança de ponto final em Intune

Ver as definições que pode configurar nos perfis da política de *proteção* de conta no nó de segurança de Ponto final de Intune como parte de uma política de [segurança endpoint](../protect/endpoint-security-policy.md).

Plataformas e perfis suportados:

- **Windows 10 e mais tarde:**
  - Perfil: **Proteção de Conta** *(Pré-visualização)*


## <a name="account-protection-profile"></a>Perfil de proteção de conta

### <a name="account-protection"></a>Account protection (Proteção de contas)

- **Bloqueie janelas Olá para negócios**

  O Windows Hello for Business é um método alternativo para iniciar sessão no Windows substituindo palavras-passe, Smart Cards e Cartões Inteligentes Virtuais.
  - **Não configurado** *(predefinido)*- Fornecimento de dispositivos Windows Hello for Business.
  - **Desativado** - Fornecimento de dispositivos Windows Hello for Business.
  - **Enabled** - Os dispositivos não disponibilizam o Windows Hello for Business para qualquer utilizador
  
- **Ativar a utilização de chaves de segurança para iniciar sessão**

  Ative a chave de segurança Windows Hello como uma credencial de inscrição para todos os Computadores do inquilino.
  - **Não configurado** *(predefinido)*
  - **Sim**

- **Ligue a guarda credencial**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  A Guarda Credencial utiliza o Windows Hypervisor para fornecer proteções. A Guarda Credencial requer suporte de hardware para proteções Secure Boot e DMA. Esta definição só é bem sucedida em dispositivos que satisfaçam os requisitos de hardware.
  - **Não configurado** *(predefinido)*- Desative a utilização da Guarda Credencial, que é a falha do Windows.
  - **Ativar com o bloqueio UEFI** - Ativar a Guarda Credencial e bloqueá-la de ser desligada remotamente, uma vez que a configuração da UEFI deve ser manualmente desobstruída.
  - **Ativar sem bloqueio UEFI** - Ativar a Guarda Credencial e permitir que seja desligada sem acesso físico à máquina.

## <a name="next-steps"></a>Próximos passos

[Política de segurança do ponto final para a proteção de conta](../protect/endpoint-security-account-protection-policy.md)
