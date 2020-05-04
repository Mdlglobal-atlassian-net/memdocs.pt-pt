---
title: CMG FAQ
titleSuffix: Configuration Manager
description: Use este artigo para responder a perguntas frequentes sobre o gateway de gestão de nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 2bd3824df18ecdf426720a99db8720ef4b678733
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714074"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas frequentes sobre o gateway de gestão de nuvens

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo responde às suas perguntas frequentes sobre o portal de gestão de nuvens. Para mais informações, consulte o plano para o gateway de gestão de [nuvens.](plan-cloud-management-gateway.md)


## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="what-certificates-do-i-need"></a>Que certificados preciso?

Para obter informações mais detalhadas, consulte certificados para gateway de [gestão de nuvem](certificates-for-cloud-management-gateway.md).


### <a name="do-i-need-azure-expressroute"></a>Preciso da Azure ExpressRoute?

Não. [O Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite-lhe estender a sua rede no local para a nuvem da Microsoft. ExpressRoute, ou outras ligações de rede virtuais não são necessárias para o gateway de gestão de nuvem do Gestor de Configuração. O design do portal de gestão de nuvem permite que os clientes baseados na Internet se comuniquem através do serviço Azure a sistemas de sites no local sem configuração adicional da rede. Para mais informações, consulte [Plan for cloud management gateway](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Preciso manter as máquinas virtuais Azure?

Não é necessária manutenção. O design do gateway de gestão de nuvem utiliza a plataforma Azure como um serviço (PaaS). Utilizando a subscrição que fornece, o Gestor de Configuração cria as máquinas virtuais necessárias (VMs), armazenamento e networking. O Azure protege e atualiza a máquina virtual. Estes VMs não fazem parte do seu ambiente no local, como é o caso da infraestrutura como serviço (IaaS). O portal de gestão de nuvem é um PaaS que estende o ambiente do Gestor de Configuração para a nuvem. Para mais informações, consulte a segurança das implementações do [PaaS](/azure/security/security-paas-deployments).


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Como posso garantir a continuidade do serviço durante as atualizações de serviço?

Ao escalonar a CMG para incluir duas ou mais instâncias, beneficia automaticamente dos Domínios de Atualização em Azure. Veja [como atualizar um serviço na nuvem](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estou a usar O CMC. Se eu adicionar CMG, como se comportam os clientes?

Se já implementou a [gestão de clientes baseada na Internet](../plan-internet-based-client-management.md) (IBCM), também pode implementar o portal de gestão de nuvem. Os clientes recebem política para ambos os serviços. À medida que vagueiam pela internet, selecionam e utilizam aleatoriamente um destes serviços baseados na Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a>As contas de utilizador têm de estar no mesmo inquilino Azure AD que o inquilino associado à subscrição que acolhe o serviço de nuvem CMG?
<!--SCCMDocs-pr issue #2873-->
Se o seu ambiente tiver mais de uma subscrição, pode implementar a CMG em qualquer subscrição que possa acolher serviços de nuvem Azure. 

Esta questão é comum nos seguintes cenários:  

- Quando você tem ambientes de teste e produção distintos Ative Directory e Azure AD, mas uma única subscrição centralizada do Azure hospedando  

- O seu uso do Azure cresceu organicamente em diferentes equipas  

Quando estiver a utilizar uma implementação do Gestor de Recursos, a bordo do inquilino Azure AD associado à subscrição. Esta ligação permite ao Gestor de Configuração autenticar o Azure para criar, implementar e gerir o CMG.  

Se estiver a utilizar a autenticação Azure AD para os utilizadores e dispositivos geridos através da CMG, a bordo desse inquilino azure AD. Para obter mais informações sobre os serviços azure para gestão de nuvem, consulte [os serviços da Configure Azure.](../../../servers/deploy/configure/azure-services-wizard.md) Quando você a bordo de cada inquilino DaD Azure, um único CMG pode fornecer autenticação Azure AD para vários inquilinos, independentemente da localização de hospedagem.

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Como é que a CMG afeta os meus clientes ligados via VPN?

Os clientes de roaming que se ligam ao seu ambiente através de uma VPN são geralmente detetados como virados para a intranet. Tentam ligar-se à sua infraestrutura no local, como pontos de gestão e pontos de distribuição. Alguns clientes preferem ter estes clientes de roaming geridos por serviços na nuvem mesmo quando ligados via VPN. A partir da versão 1902, associe o CMG a um grupo de fronteiras. Esta ação obriga estes clientes a não utilizar os sistemas de sites no local. Para mais informações, consulte [os grupos de fronteira configure](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Se eu ativar um CMG, os meus clientes só se ligarão ao ponto de gestão ativado pela CMG quando estiverem ligados à intranet?

Para garantir o tráfego sensível enviado através de um CMG, configure um ponto de gestão HTTPS ou utilize o Enhanced HTTP.

Se optar por implementar um CMG e utilizar certificados PKI para comunicação HTTPS sobre o ponto de gestão ativado pela CMG, selecione a opção de **permitir clientes apenas** à Internet nas propriedades do ponto de gestão. Esta definição garante que os clientes internos continuam a utilizar pontos de gestão HTTP no seu ambiente.

Se utilizar o ENHANCED HTTP, não precisa de configurar esta definição. Os clientes continuam a utilizar http quando comunicam diretamente com o ponto de gestão ativado pela CMG. Para mais informações, consulte [O HTTP Melhorado](../../../plan-design/hierarchy/enhanced-http.md).

## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](plan-cloud-management-gateway.md)
- [Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)
- [Certificados para o gateway de gestão na cloud](certificates-for-cloud-management-gateway.md)
- [Segurança e privacidade para o gateway de gestão na cloud ](security-and-privacy-for-cloud-management-gateway.md)
- [Tamanho do gateway de gestão da nuvem e números de escala](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
