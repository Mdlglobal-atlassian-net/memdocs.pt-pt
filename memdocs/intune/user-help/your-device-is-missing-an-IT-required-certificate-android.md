---
title: O dispositivo tem um certificado em falta | Documentos da Microsoft
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b4a16204afc99169183e02eb269ab24d7f63cc49
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327469"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Instale certificado em falta exigido pela sua organização  

Se o seu dispositivo não estiver matriculado no Intune, e faltando um certificado necessário, não poderá entrar na aplicação Portal da Empresa. Ao tentar iniciar sessão, verá a seguinte mensagem:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Existem duas opções que pode tentar descarregar o certificado necessário e inscrever o seu dispositivo. 

- Ativar o acesso ao navegador na aplicação Portal da Empresa.
- Identifique o certificado em falta numa empresa ou pc escolar. Em seguida, procure na internet para descarregar o certificado em falta. 

Complete os passos para permitir primeiro o acesso ao navegador. Depois disso, se ainda não conseguir inscrever o seu dispositivo, siga os passos para localizar o certificado na internet. 

## <a name="enable-browser-access"></a>Ativar o acesso ao navegador
Complete estas etapas para permitir o acesso ao navegador. Depois de ter ativado o acesso, o Portal da Empresa instalará o certificado apropriado e continuará a matricular-se.    

1. Na aplicação Portal da Empresa, vá ao canto direito e selecione o menu.  
2. Selecione **Definições**.  
3. Ao lado de ativar o acesso ao **navegador,** selecione **.**  
4. No ecrã do Administrador do Dispositivo, **selecione ATIVAÇÃO**. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Identifique e descarregue o certificado em falta através da pesquisa na Web
Complete estes passos para identificar e instalar manualmente o certificado no seu dispositivo.  

1. Num PC, abra o Internet Explorer. Se não tiver um PC para utilizar para esta finalidade, contacte o suporte da empresa. Para encontrar as informações de contacto do suporte da empresa, consulte o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).

2. Aceda ao [Web site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980) e inicie sessão com as credenciais profissionais ou escolares.

3. Na extremidade mais à direita da barra de endereço do browser, selecione o símbolo semelhante a um cadeado, conforme mostrado na captura de ecrã seguinte.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Se não vir o símbolo de cadeado, pare e contacte o suporte da empresa. O cadeado significa que tem sessão iniciada em segurança, pelo que só deve avançar se ver este símbolo.

4. Selecione **Ver certificados**.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Escolha o separador de percurso de **certificação** e, em seguida, identifique o certificado que precisa obter da Internet. O nome do certificado necessário estará na mesma posição que aquele que está realçado na captura de ecrã de exemplo anterior.

6. Num motor de busca como o Bing ou o Google, procure o nome do certificado em falta que identificou na secção anterior. O certificado pode terminar com diferentes "extensões," como ".crt", “.pem", etc.

7. Transfira o certificado de raiz do Web site.

8. Depois de transferido o certificado, arraste desde a parte superior do dispositivo para baixo para abrir as notificações e toque no nome do certificado na lista de notificações.

4. Na caixa de diálogo **Nomear o Certificado** mostrada na captura de ecrã seguinte, aceite o nome predefinido do certificado.

5. Certifique-se de que a **Utilização da Credencial** está definida como **Utilizada para VPN e aplicações** e, em seguida, toque em **OK**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Feche a aplicação Portal da Empresa.

7. Reabra a aplicação Portal da Empresa. Agora deverá conseguir iniciar sessão na aplicação do Portal da Empresa. Se precisar de ajuda, contacte o suporte da empresa.

Se vir a mesma mensagem que diz "certificado em falta", como mostrado anteriormente, e já tiver seguido os passos, significa que, provavelmente, ainda há outro certificado que o suporte da empresa o vai ter de ajudar a instalar. Contacte o suporte da empresa para obter ajuda, ao utilizar as informações de contacto disponibilizadas no [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).

## <a name="next-steps"></a>Próximos passos  

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [Web site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
