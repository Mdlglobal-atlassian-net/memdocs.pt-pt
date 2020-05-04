---
title: Atualizar o Windows 10
titleSuffix: Configuration Manager
description: Atualizar dispositivos para a versão 1709 do Windows 10 ou posterior, o que é necessário para a cogestão
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711463"
---
# <a name="upgrade-windows-10-for-co-management"></a>Atualizar o Windows 10 para cogestão

À medida que trabalha para embarcar na sua organização para cogestão, a corrente é um obstáculo significativo para alguns clientes. A cogestão requer o [Windows 10 versão 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou mais tarde. Assim que atualizar o Windows e configurar a inscrição automática, os seus clientes estão automaticamente inscritos na cogestão.

No vídeo seguinte, o gestor de programas sénior Rob York e o gestor de marketing de produtos Locky Ainley discutem e demo upgrade para o Windows 10 para cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Por que fazer upgrade?

Entre outros avanços na plataforma, a versão 1709 do Windows 10 e mais tarde suporta a inscrição automática. Este comportamento faz com que um dispositivo se inscreva automaticamente para Intune quando se juntou ao Azure Ative Directory (Azure AD). 

Para mais informações, consulte Ativar o [Windows 10 de inscrição automática.](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)


## <a name="how-to-do-it"></a>Como fazê-lo

Aqui estão algumas dicas que aprendemos ao ajudar milhares de clientes a obter a corrente rapidamente:

- Utilize implementações faseadas para lançar esta atualização para as pessoas certas nos momentos certos. Para mais informações, consulte [Criar implementações faseadas](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Utilize pré-cache para reduzir os tempos de espera do utilizador. Para mais informações, consulte o [conteúdo pré-cache da Configure](../osd/deploy-use/configure-precache-content.md).  

- Utilize o modelo de sequência de tarefas de atualização predefinido. Em seguida, configure os seus passos para pré-e pós-actualização, e quaisquer ações de falha. Para mais informações, consulte [os passos recomendados de sequência de tarefas para pós-processamento](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Se o seu ambiente tiver uma mão de obra altamente móvel, o Gestor de Configuração suporta a atualização no local sobre o gateway de gestão de nuvem (CMG). Esta funcionalidade permite-lhe atualizar os seus clientes do Windows 10 quando estes são baseados na Internet. Para obter mais informações sobre o CMG, consulte [a atualização do Windows 10 no local via CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Ofereça um opt-in à cogestão para os utilizadores que pretendam ser adotantes precoces. Esta abordagem acelera a adoção inicial. Identificando estas pessoas com antecedência, você pode garantir uma boa cobertura nos primeiros dias de um lançamento. Também recebe validação e feedback de utilizadores que estão felizes com a mudança e interessados em lançamentos mais frequentes. Os primeiros programas de adoção geram interesse nas novas tecnologias e crescem em tamanho ao longo do tempo.  


## <a name="case-studies"></a>Estudos de caso

O Microsoft IT implementou o Windows 10 para 96.000 utilizadores distribuídos na Microsoft. A implementação incluiu utilizadores remotos e utilizadores na rede corporativa. O destacamento terminou em nove semanas. Para obter mais informações sobre a sua experiência, consulte [a implementação do Windows 10 na Microsoft como uma atualização no local](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Um grande fabricante europeu de software usa com sucesso um grupo de adotantes precoces. Após os primeiros grupos de testes e pilotagem, aproximadamente 2.000 funcionários recebem a primeira atualização, atualizações e software. Este grupo inclui pessoal de TI e voluntários de opt-in. Este nível de envolvimento com os seus utilizadores dá-lhes um maior nível de confiança ao testar, e mais credibilidade quando os lançamentos em massa começam.



## <a name="contact-fasttrack"></a>Contato fasttrack

Se precisar de assistência com a sua atualização do Windows 10 em qualquer ponto do processo, vá ao [Microsoft FastTrack,](https://Microsoft.com/FastTrack/)faça o início e solicite assistência. 

Para mais informações, consulte [obter ajuda do FastTrack](quickstart-fasttrack.md). 

