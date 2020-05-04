---
title: Configurar o Azure AD híbrido
titleSuffix: Configuration Manager
description: Se o seu ambiente tiver atualmente dispositivos Windows 10 unidos pelo domínio, configurar o Azure AD híbrido antes de ativar a cogestão
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711477"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurar anúncio híbrido Azure para cogestão

Se tiver dispositivos Windows 10 unidos ao Ative Directory no local, antes de ativar a cogestão no Diretor de Configuração, junte-se primeiro a estes dispositivos ao Azure Ative Directory (Azure AD). Este processo chama-se aadesada híbrida Azure AD. 

No vídeo seguinte, o gestor sénior de programas Sandeep Deo e o gestor de marketing de produtos Adam Harbour discutem e demo configurando dispositivos em Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

O processo híbrido de adesão a AD do Azure regista automaticamente os seus dispositivos ligados ao domínio no local com a AD Azure. Para obter mais informações sobre este processo, consulte os seguintes artigos:
- [Introduction to device management in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) (Introdução à gestão de dispositivos no Azure Active Directory) 
- [Como planear a sua adiazur híbrida azure](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

A adesão à Hybrid Azure AD é uma das principais bases para a cogestão. Este processo pode ser um desafio para alguns clientes, por exemplo:
- A sua organização usa uma solução de identidade de terceiros 
- As complexidades da criação de Serviços da Federação de Diretórios Ativos (ADFS)

Resolver estes desafios pode ter alguma orientação. Este artigo ajuda a atenuar quaisquer atrasos.


## <a name="how-to-do-it"></a>Como fazê-lo

Os dispositivos são semelhantes aos utilizadores quando criam uma identidade que pretende proteger. Para proteger a identidade de um dispositivo a qualquer momento e em qualquer local, é necessário trazer a identidade desse dispositivo para a AD Azure.

Com base no tipo de domínio que estás a usar, há duas maneiras primárias de o fazer. Configure hybrid Azure AD junte-se para um dos seguintes tipos de domínio:  
- [Domínios Federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domínios geridos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Os dois métodos anteriores proporcionam a melhor experiência. Para obter informações mais detalhadas, incluindo o processo manual, consulte os seguintes artigos:
- [Configurar manualmente dispositivos híbridos Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticação pass-through da ADFS para a AD Azure híbrida,](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview)que inclui a descoberta da Azure AD  

Para obter orientações de resolução de problemas, consulte o Anúncio [Azure híbrido do Windows 10, junte-se ao guia de resolução de problemas](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Estudo de caso

Uma grande empresa europeia de software com mais de 100.000 utilizadores na sua rede teve uma abordagem granular e faseada para permitir a adesão híbrida azure AD.

Durante a fase de planeamento, uma vez que a adesão híbrida do Azure AD é um elemento-chave de apoio à cogestão, os administradores do Gestor de Configuração trabalharam com a equipa de identidade. Esta empresa de software tinha muitas regras ADFS, e algumas eram complexas. Para responder a este desafio, a equipa de identidade reviu as regras atuais da ADFS antes de permitir a adesão híbrida azure AD. A equipa de TI também optou por atualizar o Azure AD Connect para a versão mais recente. O Azure AD Connect oferece agora um fluxo de processo automatizado para permitir a adesão híbrida azure AD.

Após a implantação e teste bem sucedidos no seu ambiente de pré-produção, este cliente permitiu que a AD Hybrid Hybrid se juntasse a toda a propriedade de produção. Dentro de uma semana, tinham todos os dispositivos Windows 10 cogeridos.



## <a name="contact-fasttrack"></a>Contato fasttrack

Se precisar de assistência para configurar o Azure AD em qualquer ponto do processo, vá ao [Microsoft FastTrack,](https://Microsoft.com/FastTrack/)faça o sinal de assistência e solicite assistência. 

Para mais informações, consulte [obter ajuda do FastTrack](quickstart-fasttrack.md). 

