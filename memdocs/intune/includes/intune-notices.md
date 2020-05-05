---
title: incluir ficheiro
description: incluir ficheiro
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183058"
---
Estes avisos fornecem informações importantes que podem ajudá-lo a preparar-se para futuras alterações e funcionalidades intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Suporte para Microsoft Intune para o final do Windows 10 Mobile<!--3544938-->
O suporte mainstream da Microsoft para o Windows 10 Mobile terminou em dezembro de 2019. Tal como referido nesta declaração de suporte, os utilizadores do Windows 10 Mobile deixarão de poder receber novas atualizações de segurança, hotfixes não de segurança, opções de suporte assistido gratuitos ou atualizações de conteúdos técnicos online da Microsoft. Com base no suporte all-up Mobile OS, o Microsoft Intune vai agora terminar o suporte tanto para o Portal da Empresa para a aplicação Móvel Windows 10 como para o Sistema Operativo Móvel Windows 10 a 10 de agosto de 2020.

#### <a name="how-does-this-affect-me"></a>Como é que isto me afeta?
Se tiver dispositivos Windows 10 Mobile implantados na sua organização, entre hoje e 10 de agosto de 2020 pode inscrever novos dispositivos, adicionar ou remover políticas e apps, ou atualizar quaisquer definições de gestão. Depois de 10 de agosto, vamos parar novas matrículas e, eventualmente, remover a gestão móvel do Windows 10 da Intune UI. Os dispositivos deixarão de fazer o check-in no serviço Intune e eliminaremos os dados do dispositivo e da política.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso de fazer para me preparar para esta alteração?
Pode verificar o seu relatório Intune para ver quais os dispositivos ou utilizadores que podem ser afetados. Vá a **Dispositivos** > **Todos os dispositivos** e filtrar por OS. Pode adicionar colunas adicionais para ajudar a identificar quem na sua organização tem dispositivos que executam o Windows 10 Mobile. Solicite que os seus utilizadores finais atualizem os seus dispositivos ou desistam de utilizar os dispositivos para acesso corporativo.


### <a name="end-of-support-for-legacy-pc-management"></a>Fim do apoio à gestão do PC legado

A gestão do LEGACY PC vai sair do apoio no dia 15 de outubro de 2020. Atualize os dispositivos para o Windows 10 e reinscreva-os como dispositivos de Gestão de Dispositivos Móveis (MDM) para mantê-los geridos pela Intune.

[Mais informações](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Diminuição do suporte para administrador de dispositivos Android<!--5857738-->
O administrador de dispositivos Android (por vezes referido para a gestão "legacy" android e lançado com o Android 2.2) é uma forma de gerir dispositivos Android. No entanto, a melhoria da funcionalidade de gestão já está disponível com [o Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (lançado com o Android 5.0). Num esforço para se mudar para uma gestão moderna, mais rica e segura de dispositivos, a Google está a diminuir o suporte do administrador de dispositivos em novas versões Android.

#### <a name="how-does-this-affect-me"></a>Como é que isto me afeta?
Devido a estas alterações por parte da Google, os utilizadores intune serão impactados das seguintes formas:  
- A Intune só poderá fornecer suporte total para dispositivos Android geridos por administradorde dispositivos que executam o Android 10 e, posteriormente, através do Q2 CY2020. Os dispositivos geridos pelo administrador do dispositivo que estão a executar o Android 10 ou mais tarde depois desta altura não poderão ser totalmente geridos. Em particular, os dispositivos com impacto não receberão novos requisitos de senha.
    - Os dispositivos Samsung Knox não serão impactados neste prazo porque o suporte alargado é fornecido através da integração de Intune com a plataforma Knox. Isto dá-lhe mais tempo para planear a transição para fora da gestão de administração do dispositivo.    
- Os dispositivos Android geridos por administrador de dispositivos que permaneçam em versões Android abaixo do Android 10 não serão afetados e podem continuar a ser totalmente geridos com o administrador do dispositivo.    
- Para todos os dispositivos que executam o Android 10 e posteriormente, a Google restringiu a capacidade de agentes de gestão de administradores de dispositivos como o Portal da Empresa acederem à informação de identificador de dispositivos. Esta restrição afeta as seguintes funcionalidades Intune depois de um dispositivo ser atualizado para o Android 10 ou posteriormente:  
    - O controlo de acesso à rede para VPN deixará de funcionar.   
    - Identificar dispositivos como propriedade corporativa com um IMEI ou um número de série não marcará automaticamente os dispositivos como propriedade corporativa.  
    - O IMEI e o número de série deixarão de ser visíveis aos administradores de TI em Intune. 
        > [!NOTE]
        > Isto só afeta dispositivos geridos por administradores de dispositivos no Android 10 e posteriormente e não afeta dispositivos que estão a ser geridos como Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso de fazer para me preparar para esta alteração?
Para evitar a redução da funcionalidade que chega no 3º trimestre CY2020, recomendamos o seguinte:
- Não embarque em novos dispositivos na gestão de administrador de dispositivos.
- Se se espera que um dispositivo receba uma atualização para o Android 10, emigra-o da gestão do administrador do dispositivo para as políticas de gestão e/ou proteção de aplicações do Android Enterprise.

#### <a name="additional-information"></a>Informações adicionais
- [Orientação da Google para a migração de administrador de dispositivos para Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentação da Google sobre o plano para depreciar o administrador do dispositivo API](https://developers.google.com/android/work/device-admin-deprecation)