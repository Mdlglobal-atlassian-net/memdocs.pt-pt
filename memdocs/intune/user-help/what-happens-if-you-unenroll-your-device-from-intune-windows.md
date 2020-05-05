---
title: O que acontece se anular a inscrição do seu dispositivo Windows? | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 47e03edb-0c57-4e25-8e89-4a1069267b8c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: bea6ab16baa923d4cc38dee421342636de9e1942
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076803"
---
# <a name="what-happens-if-you-unenroll-your-windows-device-from-intune"></a>O que acontece se anular a inscrição do seu dispositivo Windows no Intune?

Utilize os links do lado direito desta página, sob **este artigo,** para encontrar informações sobre o tipo de dispositivo que está a utilizar.


## <a name="windows-10-windows-81-windows-8-windows-7-windows-vista"></a>Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista

- O seu dispositivo já não aparece no Portal da Empresa e já não é possível instalar aplicações no Portal da Empresa.

- Se instalou o software do cliente Intune, é removido do seu computador.

- O software do Endpoint Protection do Intune é removido do computador. Se o seu computador tiver outro software de proteção contra vírus instalado e este estiver desativado, esse software poderá ser reativado após a remoção do Endpoint Protection do Intune. Analise o seu computador depois de ser removido do Portal da Empresa.

    > [!IMPORTANT]
    > Se o outro software de proteção contra vírus não for novamente ativado ou não existir outro software de proteção contra vírus instalado, o seu computador pode estar vulnerável a vírus e software maligno.

- Todas as definições que tenham sido alteradas no seu dispositivo quando o adicionou (por exemplo, a desativação da câmara) deixam de ser aplicáveis.

- O seu computador deixará de receber atualizações de software automáticas ou atualizações de software antivírus do serviço do Intune. No entanto, dependendo da configuração, o seu computador poderá continuar a receber atualizações do Windows Server Update Services, Windows Update ou Microsoft Update.

Além disso, no Windows 8.1:

- Já não é possível utilizar aplicações da empresa e dados da empresa no seu dispositivo.

- Algumas aplicações de email, como o Windows Mail, já não conseguem aceder a emails da empresa que estão armazenados no seu dispositivo.

- Pode não conseguir ligar-se à rede da sua empresa através de Wi-Fi ou de uma rede privada virtual.

- É possível que deixe de ter acesso a alguns recursos da empresa, como partilhas de ficheiros ou sites internos, no seu dispositivo.

## <a name="windows-10-mobile-and-windows-phone-81"></a>Windows 10 para dispositivos móveis e Windows Phone 8.1

- A aplicação Portal da Empresa é desinstalada do seu dispositivo. Isto significa que o seu dispositivo já não aparece no Portal da Empresa e não pode instalar aplicações a partir da aplicação Portal da Empresa ou do website do Portal da Empresa.

- Já não é possível utilizar aplicações da empresa e dados da empresa no seu dispositivo.

- As definições alteradas no seu dispositivo quando o adicionou (por exemplo, a desativação da câmara ou o comprimento necessário específico de uma palavra-passe) deixam de ser aplicáveis.

    > [!IMPORTANT]
    > A única exceção são as políticas de encriptação, que ainda são aplicáveis. Se a política da sua empresa exige a encriptação do seu Windows Phone, a única forma de desencriptar o seu telemóvel implica a reposição do mesmo através do menu **Definições**.

## <a name="windows-rt-running-windows-81"></a>Windows RT a executar o Windows 8.1

- A aplicação Portal da Empresa é desinstalada do seu dispositivo. Isto significa que o seu dispositivo já não aparece no Portal da Empresa e não pode instalar aplicações a partir do Portal da Empresa.

- Já não é possível utilizar aplicações da empresa e dados da empresa no seu dispositivo.

- As definições alteradas no seu dispositivo quando o adicionou (por exemplo, a desativação da câmara ou o comprimento necessário específico de uma palavra-passe) deixam de ser aplicáveis.

- É possível que deixe de conseguir ligar-se à rede da sua empresa através de Wi-Fi ou de uma rede privada virtual.

- É possível que deixe de ter acesso a alguns recursos da empresa, como partilhas de ficheiros ou sites internos, no seu dispositivo.

- Algumas aplicações de email, como o Windows Mail, já não conseguem aceder a emails da empresa que estão armazenados no seu dispositivo.

Ao remover o seu dispositivo Windows RT, ocorrerá o seguinte:

- A aplicação Portal da Empresa é desinstalada do seu dispositivo. Isto significa que o seu dispositivo já não aparece no Portal da Empresa e não pode instalar aplicações a partir do Portal da Empresa.

- Já não é possível utilizar aplicações da empresa e dados da empresa no seu dispositivo.

- As definições alteradas no seu dispositivo quando o adicionou (por exemplo, a desativação da câmara ou o comprimento necessário específico de uma palavra-passe) deixam de ser aplicáveis.

Se tiver dúvidas, contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
