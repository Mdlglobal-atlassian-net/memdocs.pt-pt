---
title: Segurança e privacidade cmg
titleSuffix: Configuration Manager
description: Conheça orientações e recomendações para segurança e privacidade com o portal de gestão de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712891"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Segurança e privacidade para o gateway de gestão de nuvem

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo inclui informações de segurança e privacidade para o gateway de gestão de nuvem do Gestor de Configuração (CMG). Para mais informações, consulte [Plan for cloud management gateway](plan-cloud-management-gateway.md).

## <a name="cmg-security-details"></a>Detalhes de segurança da CMG

- A CMG aceita e gere ligações a partir de pontos de ligação CMG. Utiliza autenticação SSL mútua utilizando certificados e iDs de ligação.
- A CMG aceita e reencaminha os pedidos dos clientes utilizando os seguintes métodos:
    - Pré-autentica ligações utilizando SSL mútuo com o certificado de autenticação de cliente baseado em PKI ou Azure AD.
      - O IIS nas instâncias cmg VM verifica o caminho do certificado com base nos certificados de raiz fidedignos enviados para a CMG.
      - O IIS na instância VM também verifica a revogação do certificado de cliente, se ativado. Para mais informações, consulte [Publicar a lista de revogação do certificado](#bkmk_crl).
    - A lista de fidedignidade saem da raiz do certificado de autenticação do cliente. Também realiza a mesma validação que o ponto de gestão do cliente. Para mais informações, consulte as entradas de [Revisão na lista de fidedignidade de certificados do site](#bkmk_ctl).
    - Valida e filtra pedidos de clientes (URLs) para verificar se algum ponto de ligação CMG pode atender o pedido.  
    - Verifique o comprimento do conteúdo para cada ponto final de publicação.
    - Usa o comportamento de robin redondo para carregar pontos de ligação CMG no mesmo site.
- O ponto de ligação CMG utiliza os seguintes métodos:
    - Constrói ligações HTTPS/TCP consistentes a todas as instâncias VM da CMG. Verifica e mantém estas ligações a cada minuto.
    - Utiliza a autenticação SSL mútua com a CMG utilizando certificados.
    - Reencaminha os pedidos dos clientes com base em mapeamentos de URL.
    - Reporta o estado de ligação para mostrar o estado de saúde do serviço na consola.
    - Reporta tráfego por ponto final a cada cinco minutos.

### <a name="configuration-manager-client-facing-roles"></a>Funções viradas para o cliente do Gestor de Configuração

O ponto de gestão e o ponto de atualização de software apontam pontos finais no IIS para atender pedidos de clientes. A CMG não expõe todos os pontos finais internos. Cada ponto final publicado para o CMG tem um mapeamento URL.

- O URL externo é o que o cliente usa para comunicar com a CMG.
- O URL interno é o ponto de ligação CMG utilizado para encaminhar pedidos para o servidor interno.

#### <a name="url-mapping-example"></a>Exemplo de mapeamento de URL

Quando ativa o tráfego CMG num ponto de gestão, o Gestor de Configuração cria um conjunto interno de mapeamentos de URL para cada servidor de ponto de gestão. Por exemplo: ccm_system, ccm_incoming e sms_mp. O URL externo para o ponto de gestão ccm_system ponto final pode parecer:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
O URL é único para cada ponto de gestão. O cliente do Gestor de Configuração coloca então o nome do ponto de gestão ativado pela CMG na sua lista de pontos de gestão da Internet. Este nome parece:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
O site envia automaticamente todos os URLs externos publicados para o CMG. Este comportamento permite ao CMG fazer filtragem de URL. Todos os mapeamentos de URL replicam-se ao ponto de ligação CMG. Em seguida, encaminha a comunicação para servidores internos de acordo com o URL externo do pedido do cliente.


## <a name="security-guidance-for-cmg"></a>Orientação de segurança para cmg

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicar a lista de revogação do certificado

Publique a lista de revogação de certificados da Sua PKI (CRL) para que os clientes baseados na Internet tenham acesso. Ao implementar um CMG utilizando o PKI, configure o serviço para verificar a **revogação** do certificado de cliente no separador Definições. Esta definição configura o serviço para utilizar uma lista de revogação de certificados publicado (CRL). Para mais informações, consulte [Plano de revogação](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)do certificado PKI .

Esta opção CMG verifica o certificado de autenticação do cliente.

- Se o cliente estiver a usar a autenticação Azure AD, o CRL não importa.
- Se utilizar o PKI e publicar externamente o CRL, então ative esta opção (recomendada).
- Se utilizar o PKI, não publique o CRL e desative esta opção.
- Se configurar mal esta opção, pode causar tráfego adicional dos clientes à CMG. Este tráfego adicional pode aumentar os dados de saída do Azure, o que pode aumentar os seus custos Azure.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Rever as entradas na lista de fidedignidade de certificados do site

<!--503739-->
Cada site do Gestor de Configuração inclui uma lista de autoridades de certificação de raiz fidedigna, a lista de fidedignidade de certificados (CTL). Ver e modificar a lista indo para o espaço de trabalho da Administração, expandir a Configuração do Site e selecionar Sites. Selecione um site e clique em Propriedades na fita. Mude para o separador **comunicação** do computador cliente e, em seguida, clique em **set** sob as Autoridades de Certificação de Raiz Fidedignas.

> [!Note]
> A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

Utilize um CTL mais restritivo para um site com CMG utilizando a autenticação do cliente PKI. Caso contrário, os clientes com certificados de autenticação do cliente emitidos por qualquer raiz de confiança que já exista no ponto de gestão são automaticamente aceites para o registo do cliente.

Este subconjunto proporciona aos administradores mais controlo sobre a segurança. O CTL restringe o servidor apenas a aceitar certificados de cliente emitidos pelas autoridades de certificação do CTL. Por exemplo, os navios Windows com uma série de certificados bem conhecidos da autoridade de certificação de terceiros (CA), tais como VeriSign e Thawte. Por padrão, o computador que executa o IIS confia em certificados que acorrentam a estes conhecidos CAs. Sem configurar o IIS com um CTL, qualquer computador que tenha um certificado de cliente emitido destes CAs é aceite como um cliente de Gestor de Configuração válido. Se configurar o IIS com um CTL que não incluiu estes CAs, as ligações do cliente são recusadas se o certificado acorrentado a estes CAs.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>Impor TLS 1.2

<!-- SCCMDocs-pr#4021 -->

A partir da versão 1906, utilize a definição CMG para **impor tLS 1.2**. Aplica-se apenas ao serviço de nuvem Azure VM. Não se aplica a servidores ou clientes do Diretor de Configuração no local. Para obter mais informações sobre TLS 1.2, consulte [Como ativar o TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](plan-cloud-management-gateway.md)
- [Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)
- [Perguntas frequentes sobre o gateway de gestão de nuvens](cloud-management-gateway-faq.md)
- [Certificados para o gateway de gestão na cloud](certificates-for-cloud-management-gateway.md)
