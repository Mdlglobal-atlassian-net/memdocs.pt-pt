---
title: Inscrição de administrador de dispositivos Android no Microsoft Intune
titleSuffix: ''
description: Inscreva dispositivos Android em Intune utilizando a inscrição do administrador do dispositivo.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5200f0476e3f692b02cbac9b0934c35e522ee906
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983624"
---
# <a name="android-device-administrator-enrollment"></a>Inscrição de administrador de dispositivos Android

O administrador de dispositivos Android (por vezes referido para a gestão "legacy" android e lançado com o Android 2.2) é uma forma de gerir dispositivos Android. No entanto, a melhoria da funcionalidade de gestão já está disponível com [o Android Enterprise](https://www.android.com/enterprise/management/) (lançado com o Android 5.0). Num esforço para se mudar para uma gestão moderna, mais rica e segura de dispositivos, a Google está a diminuir o suporte do administrador de dispositivos em novas versões Android.

Por isso, para evitar essa funcionalidade reduzida, aconselhamos a não inscrever novos dispositivos utilizando o processo de administrador do dispositivo descrito abaixo.

Pelas mesmas razões, recomendamos também que emigra dispositivos da gestão de administrador de dispositivos se os dispositivos forem atualizados para o Android 10. 

Se ainda decidir que os utilizadores matriculam os seus dispositivos Android com a gestão do administrador do dispositivo, continue para a próxima secção.  

Para obter mais informações sobre as funcionalidades do Android Enterprise da Google, consulte estes artigos:
- [Orientação da Google para a migração de administrador de dispositivos para Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentação da Google sobre o plano para depreciar o administrador do dispositivo API](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Configurar a inscrição do administrador do dispositivo

1. Para se preparar para gerir dispositivos móveis, tem de definir a autoridade de gestão de dispositivos móveis (MDM) para o **Microsoft Intune**. Veja [Set the MDM authority (Definir a autoridade de MDM)](../fundamentals/mdm-authority-set.md) para obter instruções. Este item só é definido uma vez, quando está a configurar pela primeira vez o Intune para a gestão de dispositivos móveis.
2. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e escolha > **dispositivos**Android de  >  **Android**  >  **inscrição Android**  >  **Dispositivos pessoais e corporativos com privilégios**de administração de dispositivos Utilize o administrador do dispositivo para gerir  >  **dispositivos.**
3. [Indique aos seus utilizadores como devem inscrever os dispositivos](../user-help/enroll-device-android-company-portal.md).  

Depois de um utilizador concluir a inscrição, pode começar a gerir os respetivos dispositivos no Intune, incluindo [atribuir políticas de conformidade](../protect/compliance-policy-create-android.md), [gerir aplicações](../apps/app-management.md) e mais.

Para obter informações sobre outras tarefas do utilizador, veja estes artigos:
- [Recursos sobre a experiência do utilizador final com o Microsoft Intune](../fundamentals/end-user-educate.md)
- [Utilizar o dispositivo Android com o Intune](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>Inscrição de administrador de dispositivo de bloco
Para bloquear dispositivos de administrador de dispositivos Android ou bloquear apenas dispositivos de administrador de dispositivos Android pessoalmente a partir da inscrição, consulte [as restrições](enrollment-restrictions-set.md)do tipo de dispositivo set .


## <a name="next-steps"></a>Passos seguintes
- [Atribuir políticas de conformidade](../protect/compliance-policy-create-android.md)
- [Gestão de apps](../apps/app-management.md)
