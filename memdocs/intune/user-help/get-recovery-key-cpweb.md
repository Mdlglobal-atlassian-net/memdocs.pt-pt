---
title: Obtenha uma chave de recuperação para um dispositivo macOS a partir do site do Portal da Empresa Intune
description: Consulte a chave de recuperação de um dispositivo macOS matriculado e gerido.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79324609"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>Obtenha uma chave de recuperação para um dispositivo macOS

Utilize o site do Portal da Empresa para obter uma chave de recuperação para o seu dispositivo macOS bloqueado. Se esquecer a sua senha de dispositivo, pode iniciar sessão no Portal da Empresa a partir de outro dispositivo para recuperar a sua chave.  

## <a name="get-recovery-key-from-company-portal-website"></a>Obtenha a chave de recuperação do site do Portal da Empresa

Esta opção está disponível para dispositivos que foram encriptados pela sua organização usando fileVault. Não está disponível para dispositivos que encriptou pessoalmente.

1. Em qualquer dispositivo, inscreva-se no site do Portal da [Empresa](https://portal.manage.microsoft.com) e selecione o botão **Menu** > **Dispositivos**.  
2. Selecione o dispositivo macOS encriptado.  
3. Selecione **Obter tecla de recuperação**.  

    ![Screenshot do site do Portal da Empresa, destacando a secção chave de recuperação Get.](./media/1907-recovery2-cpweb-intune.PNG)  

4. A sua chave de recuperação vai aparecer.

    ![Screenshot do site do Portal da Empresa, mostrando a chave de recuperação.](./media/1907-recovery-cpweb-intune.PNG)  

    Por razões de segurança, a chave desaparecerá após cinco minutos. Para ver novamente a chave, selecione **A tecla de recuperação Get**.

Se não for encontrada uma chave, mas o seu dispositivo estiver devidamente encriptado, contacte a pessoa de apoio da sua organização. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>Obtenha a chave de recuperação da app Do Portal da Empresa para iOS

Pode recuperar a sua chave de recuperação pessoal (chave FileVault) utilizando a aplicação Portal da Empresa para iOS. O seu dispositivo que tenha a chave de recuperação pessoal deve ser matriculado com Intune e encriptado com fileVault através de Intune. Esta opção não está disponível para dispositivos que tenha encriptado pessoalmente. 

Utilizando a aplicação Portal da Empresa, pode abrir a vista web do Safari e recuperar a sua chave de recuperação pessoal. 

1. Portal da Empresa Aberta.
2. Clique na **tecla de recuperação Get**.

    ![Screenshot da app Portal da Empresa para iOS, mostrando chave de recuperação](./media/get-recovery-key-cpweb-02.png)  

O site do Portal da Empresa abre na vista web do Safari e exibe a chave. 

## <a name="it-pro-support"></a>Suporte de TI pro

Se é uma pessoa de suporte de TI e pretende configurar e gerir a encriptação FileVault para dispositivos macOS, consulte a encriptação do [dispositivo Use com Intune](/intune/protect/encrypt-devices).

## <a name="next-steps"></a>Passos seguintes

Descubra o que mais pode fazer a partir do site do Portal da Empresa. Consulte [a utilização do site Intune Company Portal](using-the-intune-company-portal-website.md) para a lista de ações.  

Ainda precisa de ajuda? Contacte a sua pessoa de suporte de TI. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
