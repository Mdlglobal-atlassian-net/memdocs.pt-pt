---
title: Detalhes de largura de banda e requisitos de rede do Microsoft Intune
titleSuffix: ''
description: Reveja os detalhes de largura de banda e requisitos de configuração de rede do Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/17/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f737d48-24bc-44cd-aadd-f0a1d59f6893
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b3052d8d213ce3190ed29b43f580a8de9c840b7
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943846"
---
# <a name="intune-network-configuration-requirements-and-bandwidth"></a>Largura de banda e requisitos de configuração de rede do Intune

Pode utilizar estas informações para compreender os requisitos de largura de banda para as suas implementações Intune.

## <a name="average-network-traffic"></a>Tráfego de rede médio

A tabela lista o tamanho e frequência aproximados dos conteúdos comuns que circulam na rede para cada cliente.

> [!NOTE]
> Para garantir que os dispositivos recebem as atualizações e conteúdos do Intune, estes têm de ser regularmente ligados à Internet. O tempo necessário para receber as atualizações ou conteúdos pode variar, mas deverão manter uma ligação ininterrupta à Internet durante, pelo menos, uma hora por dia.

|Tipo do conteúdo|Tamanho aproximado|Frequência e detalhes|
|----------------|--------------------|-------------------------|
|Instalação do cliente Intune<br /><br />**São aplicáveis os seguintes requisitos, para além da instalação do cliente do Intune**|125 MB|**Problema isolado**<br /><br />O tamanho da transferência do cliente varia consoante o sistema operativo do computador cliente.|
|Pacote de inscrição de clientes|15 MB|**Problema isolado**<br /><br />São possíveis transferências adicionais quando existirem atualizações para este tipo de conteúdo.|
|Agente do Endpoint Protection|65 MB|**Problema isolado**<br /><br />São possíveis transferências adicionais quando existirem atualizações para este tipo de conteúdo.|
|Agente do Operations Manager|11 MB|**Problema isolado**<br /><br />São possíveis transferências adicionais quando existirem atualizações para este tipo de conteúdo.|
|Agente de políticas|3 MB|**Problema isolado**<br /><br />São possíveis transferências adicionais quando existirem atualizações para este tipo de conteúdo.|
|Assistência Remota através do agente Microsoft Easy Assist|6 MB|**Problema isolado**<br /><br />São possíveis transferências adicionais quando existirem atualizações para este tipo de conteúdo.|
|Operações diárias de clientes|6 MB|**Diárias**<br /><br />O cliente Intune comunica regularmente com o serviço Intune para verificar se há atualizações e políticas, e para reportar o estado do cliente ao serviço.|
|Atualizações de definições de software maligno do Endpoint Protection|Varia<br /><br />Normalmente, entre 40 KB a 2 MB|**Diárias**<br /><br />Até três vezes por dia.|
|Atualização do motor do Endpoint Protection|5 MB|**Mensal**|
|Atualizações de software|Varia<br /><br />O tamanho depende das atualizações que implementar.|**Mensal**<br /><br />Normalmente, as atualizações de software são lançadas na segunda terça-feira de cada mês.<br /><br />Um computador inscrito ou implementado recentemente pode utilizar mais largura de banda de rede ao transferir todas as atualizações lançadas anteriormente.|
|Service packs|Varia<br /><br />O tamanho varia consoante o service pack que implementar.|**Varia**<br /><br />Depende da altura em que implementar os service packs.|
|Distribuição de software|Varia<br /><br />O tamanho depende do software que implementar.|**Varia**<br /><br />Depende da altura em que implementar o software.|

## <a name="ways-to-reduce-network-bandwidth-use"></a>Formas de reduzir a utilização da largura de banda de rede

Pode utilizar um ou mais dos seguintes métodos para reduzir a utilização da largura de banda de rede dos clientes do Intune.

### <a name="use-a-proxy-server-to-cache-content-requests"></a>Utilizar um servidor proxy para colocar os pedidos de conteúdo em cache

Um servidor proxy pode colocar conteúdos em cache para reduzir as transferências em duplicado e reduzir a largura de banda de rede dos conteúdos da Internet.

Um servidor proxy de colocação em cache que recebe pedidos de conteúdo de clientes pode obter esses conteúdos e colocar em cache tanto as respostas Web como as transferências. O servidor utiliza os dados colocados em cache para responder a pedidos posteriores dos clientes.

Seguem-se as definições típicas para utilizar um servidor proxy que coloca conteúdos em cache para os clientes do Intune.


|          Definição           |           Valor recomendado           |                                                                                                  Detalhes                                                                                                  |
|----------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Tamanho da cache         |             De 5 GB até 30 GB             | O valor varia com base no número de computadores clientes na sua rede e nas configurações que utiliza. Para impedir que os ficheiros sejam eliminados demasiado cedo, ajuste o tamanho da cache do seu ambiente. |
| Tamanho do ficheiro de cache individual |                950 MB                 |                                                                     Esta definição pode não estar disponível em todos os servidores proxy com colocação em cache.                                                                     |
|   Tipos de objeto a colocar em cache    | HTTP<br /><br />HTTPS<br /><br />BITS |                                               Os pacotes Intune são ficheiros CAB obtidos através de uma transferência do Serviço de Transferência Inteligente em Segundo Plano (BITS) através de HTTP.                                               |
> [!NOTE]
> Se utilizar um servidor proxy para colocar em cache pedidos de conteúdo, a comunicação só será encriptada entre o cliente e o proxy e do proxy para o Intune. A ligação do cliente para o Intune não será encriptada ponto a ponto.

Para obter informações sobre como utilizar um servidor proxy para colocar conteúdos em cache, consulte a documentação da sua solução de servidor proxy.


### <a name="delivery-optimization"></a>Otimização de Entrega

A Otimização de Entrega permite-lhe utilizar o Intune para reduzir o consumo de largura de banda quando os seus dispositivos Windows 10 descarregam aplicações e atualizações. Utilizando uma cache distribuída auto-organizadora, os downloads podem ser retirados de servidores tradicionais e fontes alternativas (como pares de rede).

Para ver a lista completa de versões e tipos de conteúdos do Windows 10 suportados pela Otimização da Entrega, consulte o artigo de Otimização de [Entregas para atualizações do Windows 10.](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#requirements)

Pode [configurar](../configuration/delivery-optimization-settings.md) a Otimização de Entrega como parte dos perfis de configuração do seu dispositivo.


### <a name="background-intelligent-transfer-service-bits-and-branchcache"></a>Serviço de Transferência Inteligente de Fundo (BITS) e BranchCache 

Pode utilizar o Microsoft Intune para gerir os PCs do Windows, quer [como dispositivos móveis com gestão de dispositivos móveis (MDM)](../enrollment/windows-enroll.md) quer como computadores com o cliente do software Intune. A Microsoft recomenda que os clientes utilizem a solução de [gestão do MDM](../enrollment/windows-enroll.md) sempre que possível. Quando geridos desta forma, branchCache e BITS não são suportados. Para obter mais informações, consulte [Compare gerindo computadores windows como computadores ou dispositivos móveis](pc-management-comparison.md).

#### <a name="use-bits-on-computers-requires-intune-software-client"></a>Utilização (BITS) em computadores (requer cliente de software Intune)

Durante as horas que configurar, pode utilizar o BITS num computador Windows para reduzir a largura de banda da rede. Pode configurar uma política do BITS na página **Largura de banda de rede** da política do Agente do Intune.

> [!NOTE]
> Para a gestão do MDM no Windows, apenas a interface de gestão do OS para o tipo de aplicação MobileMSI utiliza BITS para descarregar. O AppX/MsiX utiliza a sua própria pilha de transferência não BITS e as aplicações Win32 através do agente do Intune utilizam a Otimização de Entrega em vez do BITS.

Para saber mais sobre o BITS e computadores Windows, veja [Background Intelligent Transfer Service (Serviço de Transferência Inteligente em Segundo Plano)](https://technet.microsoft.com/library/bb968799.aspx) na Biblioteca TechNet.


#### <a name="use-branchcache-on-computers-requires-intune-software-client"></a>Utilizar branchCache em computadores (requer cliente de software Intune)

Os clientes Intune podem utilizar o BranchCache para reduzir o tráfego da rede alargada (WAN). O BranchCache é suportado pelos seguintes sistemas operativos:

- Windows 7
- Windows 8.0
- Windows 8.1
- Windows 10

Para utilizar o BranchCache, o computador cliente tem de ter o BranchCache ativado e, em seguida, ser configurado para o **modo de cache distribuída**.

Quando o cliente do Intune é instalado nos computadores, o BranchCache e o modo de cache distribuída são ativados, por predefinição. No entanto, se a Política de Grupo tiver desativado o BranchCache, o Intune não substituirá essa política e o BranchCache permanecerá desativado.

Se utiliza o BranchCache, trabalhe em conjunto com outros administradores na sua organização para gerir a Política de Grupo e a política de Firewall do Intune. Confirme que não implementam políticas que desativem o BranchCache ou exceções da Firewall. Para obter mais informações sobre o BranchCache, consulte [Descrição Geral do BranchCache](https://technet.microsoft.com/library/hh831696.aspx).


## <a name="next-steps"></a>Passos seguintes

[Pontos finais de revisão para Intune](intune-endpoints.md)
