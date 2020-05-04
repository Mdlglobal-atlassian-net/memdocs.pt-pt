---
title: Windows Hello for Business definições em Microsoft Intune - Azure [ Microsoft Docs
description: Consulte uma lista de todas as definições pin, biométrica e anti-falsificação num perfil de proteção de identidade para utilizar e configurar o Windows Hello for Business em dispositivos Windows 10 no Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: b4581ba6bdc8b5be41d5cf567c631ffaad40d418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329289"
---
# <a name="windows-10-device-settings-to-enable-windows-hello-for-business-in-intune"></a>Definições do dispositivo Windows 10 para ativar o Windows Hello for Business em Intune

Este artigo lista e descreve as definições do Windows Hello for Business que pode controlar nos dispositivos do Windows 10 em Intune. Como administrador intune, pode configurar e atribuir estas definições aos dispositivos Windows 10 como parte da sua solução de gestão de dispositivos móveis (MDM). 

Pode encontrar informações adicionais sobre estas definições na [Configuração do Windows Hello para definições](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings)de Política De Negócios, na documentação do Windows Hello.


Para saber mais sobre os perfis do Windows Hello for Business em Intune, consulte a [configuração da proteção de identidade](identity-protection-configure.md).

## <a name="before-you-begin"></a>Antes de começar

Criar um perfil de [configuração.](identity-protection-configure.md#create-the-device-profile)

## <a name="windows-hello-for-business"></a>Windows Hello para empresas
- **Configure o Windows Hello for Business**:
  - **Não configurado** - Selecione esta definição se não quiser utilizar insinopara controlar as definições do Windows Hello for Business. Nenhuma das definições do Windows Hello para Empresas existentes em dispositivos Windows 10 será alterada. Todas as outras definições no painel não estão disponíveis.

  - **Desativado** - Se não quiser utilizar o Windows Hello for Business, selecione esta definição. Todas as outras definições no ecrã não estão disponíveis.
  - **Ativado** - Selecione esta definição se pretender configurar as definições do Windows Hello for Business.  
  
  **Predefinição**: Não configurado

  Quando programado para *ativar,* estão disponíveis as seguintes definições:

  - **Comprimento mínimo do PIN**  
    Especifique um comprimento PIN mínimo para os dispositivos, para ajudar a fixar o sessão. As predefinições do dispositivo Windows são de seis caracteres, mas esta definição pode impor um mínimo de quatro a 127 caracteres. 

    **Predefinição**: *Não configurado*

  - **Comprimento máximo do PIN**  
  Especifique um comprimento PIN máximo para os dispositivos, para ajudar a fixar o sessão. As predefinições do dispositivo Windows são de seis caracteres, mas esta definição pode impor um mínimo de quatro a 127 caracteres.  

    **Predefinição**: *Não configurado*  

  - **Letras em minúsculas no PIN**  
    Pode impor um PIN mais forte, exigindo que os utilizadores finais incluam letras minúsculas. As opções são:

    - **Não é permitido** - Bloqueie os utilizadores de utilizarem letras minúsculas no PIN. Este comportamento também ocorre se a configuração não estiver configurada.
    - **Permitido** - Permitir que os utilizadores utilizem letras minúsculas no PIN, mas não é necessário.
    - **Obrigatório** - Os utilizadores devem incluir pelo menos uma letra minúscula no PIN. Por exemplo, é prática comum exigir pelo menos uma letra maiúscula e um caráter especial.

  - **Letras em maiúsculas no PIN**  
    Pode impor um PIN mais forte, exigindo que os utilizadores finais incluam letras maiúsculas. As opções são:

    - **Não é permitido** - Bloqueie os utilizadores de utilizarem letras maiúsculas no PIN. Este comportamento também ocorre se a configuração não estiver configurada.
    - **Permitido** - Permitir que os utilizadores utilizem letras maiúsculas no PIN, mas não é necessário.
    - **Obrigatório** - Os utilizadores devem incluir pelo menos uma letra maiúscula no PIN. Por exemplo, é prática comum exigir pelo menos uma letra maiúscula e um caráter especial.

  - **Carateres especiais no PIN**  
    Pode impor um PIN mais forte, exigindo que os utilizadores finais incluam caracteres especiais. Os caracteres especiais incluem:`! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    As opções são:
    - **Não é permitido** - Bloqueie os utilizadores de usar caracteres especiais no PIN. Este comportamento também ocorre se a configuração não estiver configurada.
    - **Permitido** - Permitir que os utilizadores utilizem letras maiúsculas no PIN, mas não é necessário.
    - **Obrigatório** - Os utilizadores devem incluir pelo menos uma letra maiúscula no PIN. Por exemplo, é prática comum exigir pelo menos uma letra maiúscula e um caráter especial.

    **Padrão**: Não é permitido

  - **Expiração do PIN (dias)**  
    É recomendável especificar um período de expiração para um PIN, após o qual os utilizadores têm de alterá-lo. As predefinições do dispositivo Windows são de 41 dias.

    **Predefinição**: Não configurado

  - **Lembre-se da história do PIN**  
    Restringe a reutilização de PINs utilizados anteriormente. Os dispositivos Windows não para matem para impedir a reutilização dos últimos cinco PINs.  

    **Predefinição**: Não configurado  

  - **Ativar a recuperação pin**   
    Permite ao utilizador utilizar o serviço de recuperação Do Windows Hello para business PIN. 
    
    - **Ativado** - O segredo de recuperação PIN é armazenado no dispositivo e o utilizador pode alterar o PIN se necessário.  
    - **Deficientes** - O segredo de recuperação não é criado ou armazenado.

    **Predefinição**: Não configurado

  - **Utilize um Módulo de Plataforma Fidedigna (TPM)**   
    Um chip TPM fornece uma camada adicional de segurança de dados.  

    - **Ativado** - Apenas dispositivos com um TPM acessível podem fornecer O Windows Hello para Negócios.
    - **Não configurado** - Os dispositivos tentam primeiro utilizar um TPM. Se não estiver disponível, podem utilizar a encriptação de software.
    
    **Predefinição**: Não configurado

  - **Permitir a autenticação biométrica**  
     Permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como alternativa a um PIN, no Windows Hello para Empresas. Os utilizadores continuam a ter de configurar um PIN, para a eventualidade de a autenticação biométrica falhar. Escolha entre:

    - **Ativar** - O Windows Hello for Business permite a autenticação biométrica.
    - **Não configurado** - O Windows Hello for Business impede a autenticação biométrica (para todos os tipos de conta).

    **Predefinição**: Não configurado

  - **Utilizar anti-spoofing avançado, quando disponível**  
    Configura se as funcionalidades de anti-spoofing do Windows Hello são utilizadas nos dispositivos que o suportam (por exemplo, detetar uma fotografia de um rosto em vez de um rosto real).  
    - **Ativar** - O Windows requer que todos os utilizadores utilizem anti-falsificação para funcionalidades faciais quando isso é suportado.
    - **Não configurado** - O Windows honra as configurações anti-falsificação no dispositivo.

    **Predefinição**: Não configurado

  - **Certificado para recursos no local**  

    - **Enable** - Permite que o Windows Hello for Business utilize certificados para autenticar recursos no local.
    - **Não configurado** - Impede o Windows Hello for Business de utilizar certificados para autenticar recursos no local. Em vez disso, os dispositivos utilizam o comportamento padrão da *autenticação*de confiança de chave no local . Para mais informações, consulte o [certificado de utilizador para autenticação no local](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) na documentação do Windows Hello.  

  **Predefinição**: Não configurado

- **Utilize as chaves de segurança para iniciar sessão**  
  Esta definição está disponível para dispositivos que executam a versão 1903 do Windows 10 ou posteriormente. Utilize-o para gerir o suporte para utilizar as teclas de segurança Do Windows Hello para iniciar sessão.  

  - **Ativado** - Os utilizadores podem utilizar uma chave de segurança Windows Hello como credencial de logon para Computadores direcionados para esta política. 
  - **Desativado** - As chaves de segurança estão desativadas e os utilizadores não podem usá-las para iniciar sessão em Computadores.   

  **Predefinição**: Não configurado

## <a name="next-steps"></a>Passos seguintes

[Atribua o perfil](../configuration/device-profile-assign.md) e [monitorize o respetivo estado](../configuration/device-profile-monitor.md).
