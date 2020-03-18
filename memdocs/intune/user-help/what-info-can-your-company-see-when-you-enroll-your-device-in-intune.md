---
title: Que informações é que a sua empresa pode ver quando inscreve o seu dispositivo?
description: Explica o que o departamento de TI pode e não pode ver no seu dispositivo gerido.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: ccef2c10f4baaac9e417dd4952b1ea6d6cf47e5c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327713"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Que informações é que a minha organização pode ver quando inscrevo o meu dispositivo?

Quando inscreve um dispositivo no Microsoft Intune, a sua organização não consegue ver as suas informações pessoais. Ao inscrever um dispositivo, dá permissão à sua organização para ver partes de informações do seu dispositivo, tal como o modelo e o número de série. A sua organização utiliza estas informações para ajudar a proteger os dados empresariais no dispositivo.

**O que a sua organização nunca conseguirá ver:**

- Histórico de chamadas e navegação na Web
- Mensagens de e-mail e texto
- Contactos
- Calendário
- Palavras-passe
- Imagens, incluindo o que está na aplicação de fotografias ou câmara
- Ficheiros

**O que a sua organização conseguirá sempre ver:**

- Modelo do dispositivo, como o Google Pixel
- Fabricante do dispositivo, como Microsoft
- Sistema operativo e versão, por exemplo iOS 12.0.1
- Inventário de aplicativos e nomes de aplicativos, como o Microsoft Word. Em dispositivos pessoais, a sua organização só pode ver o seu inventário de aplicações gerido. Nos dispositivos pertencentes à empresa, a sua organização consegue ver todo o seu inventário de aplicações.
- Proprietário do dispositivo
- Nome do dispositivo
- Número de série do dispositivo
- IMEI

**Informações que a sua organização poderá conseguir ver:**

- Número de telefone: Para dispositivos corporativos, o seu número de telefone completo pode ser visto. Para dispositivos pessoais, apenas os últimos quatro dígitos do seu número de telefone são visíveis para a sua organização. Pode ver o tipo de propriedade de cada dispositivo individual na sua página de Detalhes do **Dispositivo.**
- Espaço de armazenamento do dispositivo: se não conseguir instalar uma aplicação necessária, a sua organização poderá ver o espaço de armazenamento do seu dispositivo para verificar se o espaço é insuficiente.  
- Localização: A sua organização nunca poderá ver a localização do seu dispositivo, a menos que precise de recuperar um dispositivo iOS perdido e supervisionado. Visite a documentação do [Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) para saber mais sobre dispositivos supervisionados.  
- Detalhes do inventário da aplicação: Se a sua organização utilizar a Mobile Threat Defense, poderão visualizar detalhes sobre as aplicações que se encontram no seu dispositivo iOS. Saiba mais sobre a [Defesa Contra Ameaças para Dispositivos Móveis](you-are-prompted-to-install-mtd-ios.md). Se tiver um dispositivo pessoal, a sua organização só pode ver o seu inventário de aplicações gerido. Se tiver um dispositivo corporativo, a sua organização pode ver todo o inventário da sua aplicação.
- Informações de rede: algumas informações sobre ligações de rede para dispositivos Android podem estar disponíveis para o suporte da sua organização. Por exemplo, se a sua organização precisar que os dispositivos permaneçam num determinado edifício, o dispositivo identificará a rede à qual está ligado. 