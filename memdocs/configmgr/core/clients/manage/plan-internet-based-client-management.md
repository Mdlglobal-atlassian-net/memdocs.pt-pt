---
title: Gestão de clientes baseada na Internet
titleSuffix: Configuration Manager
description: Crie um plano para gerir clientes baseados na Internet no Gestor de Configuração.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587229"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Plano para gestão de clientes baseado na Internet em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize a gestão de clientes baseada na Internet (IBCM) para gerir os clientes do Gestor de Configuração quando não estão ligados à sua rede interna. Vantagens da utilização do CMA:

- Controlo total dos servidores e funções que fornecem o serviço
- Sem dependência do serviço de nuvem
- Pode não exigir uma rede privada virtual (VPN)
- Todos os custos estão associados ao serviço no local

Devido aos requisitos de segurança mais elevados da gestão dos computadores clientes numa rede pública, o IBCM requer a utilização de certificados PKI. Esta configuração garante que as ligações são autenticadas por uma autoridade independente. Quando os clientes ibcm e servidores de site enviam dados, é encriptado e seguro.  

## <a name="client-communications"></a>Comunicação do cliente

As seguintes funções do sistema do site nos sites primários suportam ligações de clientes que se encontram em locais não confiáveis:

> [!NOTE]
> Enquanto o IBCM se concentra principalmente no cenário baseado na Internet, os mesmos comportamentos aplicam-se aos clientes numa floresta de Diretório Ativo não confiável. Sites secundários não suportam ligações de clientes de locais não confiáveis.

- Ponto de registo de certificado para o módulo de política do Gestor de Configuração (NDES)

- Ponto de distribuição

- Ponto de distribuição baseado na nuvem

- Ponto proxy de registo

- Ponto de estado de contingência

- Ponto de gestão

- Ponto de atualização de software

> [!NOTE]
> O suporte terminou para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Para versões de Configuração Manager 1906 e anteriores que ainda estão em suporte, o ponto de site do catálogo de aplicações pode aceitar ligações de clientes baseados na Internet.

### <a name="about-internet-facing-site-systems"></a>Sobre sistemas de sites virados para a Internet

Não há necessidade de ter uma confiança entre a floresta de um cliente e a do servidor do sistema do site. No entanto, quando a floresta que contém um sistema de site virado para a Internet confia na floresta que contém as contas do utilizador, esta configuração suporta políticas baseadas no utilizador para dispositivos na internet quando permite a definição de cliente **de Política de Cliente** Ativar pedidos de política de utilizador de clientes da **Internet.**

Por exemplo, as seguintes configurações ilustram quando o IBCM suporta as políticas dos utilizadores para dispositivos na internet:

- O ponto de gestão baseado na Internet está na rede do perímetro. Esta rede também tem um controlador de domínio apenas para autenticar o utilizador. Uma firewall entre o perímetro e as redes internas permite pacotes de Diretório Ativo.

- A conta de utilizador está na floresta intranet. O ponto de gestão baseado na Internet está na floresta baseada no perímetro. A floresta do perímetro confia na floresta interna. Uma firewall entre o perímetro e as redes internas permite os pacotes de autenticação.

- A conta de utilizador e o ponto de gestão baseado na Internet estão ambos na floresta baseada em intranet. Publica o ponto de gestão para a internet com um servidor de procuração web.

### <a name="use-a-web-proxy-server"></a>Use um servidor de proxy web

Pode colocar sistemas de sites baseados na Internet na intranet quando os publicar na internet com um servidor de procuração web. Configure estes sistemas de sites apenas para ligações de clientes a partir da internet, ou ligações de clientes a partir da internet e intranet. Quando utilizar um servidor de proxy web, pode configurá-lo para a camada de tomadas seguras (SSL) que faz a ponte com o túnel SSL ou SSL.

#### <a name="ssl-bridging-to-ssl"></a>Ponte SSL para SSL

A ponte SSL para o SSL é a configuração recomendada e mais segura, pois utiliza a terminação SSL com autenticação. Autentica computadores clientes com autenticação de computador. Os dispositivos móveis que se inscreve mintuado no Configuração Manager não suportam a ponte SSL.

Com a rescisão do SSL no proxy, inspeciona pacotes da internet antes de os encaminhar para a rede interna. O representante autentica a ligação do cliente, termina-a e abre uma nova ligação autenticada aos sistemas de sites baseados na Internet. Quando os clientes do Gestor de Configuração usam um proxy, o cliente contém de forma segura a sua identidade (GUID) na carga útil do pacote. O ponto de gestão não considera o representante como o cliente. O Gestor de Configuração não suporta a ponte com HTTP para HTTPS, ou de HTTPS para HTTP.

> [!NOTE]
> O Gestor de Configuração não suporta configurações de pontes SSL de terceiros. Por exemplo, Citrix Netscaler ou F5 BIG-IP. Por favor, trabalhe com o fornecedor do seu dispositivo para configurá-lo para uso com o Gestor de Configuração.

#### <a name="tunneling"></a>Túnel

Se o seu servidor web proxy não conseguir suportar os requisitos para a ponte SSL, o Gestor de Configuração também suporta a escavação SSL. Também pode utilizar túneis SSL para suportar dispositivos móveis que se inscreva no Gestor de Configuração. É uma opção menos segura porque o proxy reencaminha os pacotes SSL da internet para os sistemas do site sem a rescisão do SSL. O representante não inspeciona os pacotes para obter conteúdo malicioso. Quando utiliza o protocolo de túnel SSL, não existem requisitos de certificado para o servidor Web proxy.

## <a name="plan-for-internet-based-clients"></a>Plano para clientes baseados na Internet

Decida se configura os seus clientes baseados na Internet para gestão tanto na intranet como na internet, ou para gestão de clientes apenas na Internet. Só é possível configurar esta opção de gestão durante a instalação do cliente. Para o alterar mais tarde, reinstale o cliente.

> [!NOTE]
> Se configurar um ponto de gestão para apoiar clientes baseados na Internet, os clientes que se ligam a este ponto de gestão tornar-se-ão capazes de internet quando atualizarem a sua lista de pontos de gestão disponíveis.
>
> Não é preciso restringir a configuração da gestão de clientes apenas à Internet. Também pode usá-lo na intranet.

Os clientes que configura para gestão apenas pela Internet apenas comunicam com os sistemas do site que configura para ligações ao cliente a partir da internet. Utilize esta configuração nos seguintes cenários:

- Para computadores que sabe nunca se ligarão à sua intranet. Por exemplo, computadores de ponto de venda em locais remotos.
- Para restringir a comunicação do cliente apenas ao HTTPS. Por exemplo, apoiar a firewall e as políticas de segurança restritas.
- Quando instala sistemas de site baseados na Internet numa rede de perímetro, e pretende gerir estes servidores como clientes do Gestor de Configuração.

> [!NOTE]
> Quando quiser gerir clientes de grupos de trabalho na internet, instale-os como apenas internet.
>
> Ao configurar um dispositivo móvel para utilizar um ponto de gestão baseado na Internet, ele automaticamente configura como apenas internet.

Pode configurar outros clientes para a gestão de clientes de internet e intranet. Quando detetam uma mudança de rede, mudam automaticamente entre a GEM IMC e a gestão do cliente intranet. Se estes clientes puderem encontrar e ligar-se a um ponto de gestão que suporta as ligações do cliente na intranet, estes clientes são geridos como clientes intranet. Os clientes intranet têm a funcionalidade completa do Gestor de Configuração. Se os clientes não conseguem encontrar ou ligar-se a um ponto de gestão que suporta as ligações do cliente na intranet, tentam ligar-se a um ponto de gestão baseado na Internet. Se esta ação for bem sucedida, estes clientes são então geridos pelos sistemas de sites baseados na Internet no seu site designado.

O benefício na comutação automática é que os clientes podem usar todas as funcionalidades quando se conectam à intranet, e receber uma gestão essencial quando estão na internet. O download de conteúdos que começa na internet pode ser retomado na intranet e ao contrário.

## <a name="prerequisites"></a>Pré-requisitos

O IBCM no Gestor de Configuração tem as seguintes dependências:

- Os clientes requerem uma ligação à Internet. O Gestor de Configuração utiliza a ligação à Internet existente do dispositivo. Os dispositivos móveis devem ter uma ligação direta à Internet. Os computadores completos do cliente podem ter uma ligação direta à Internet ou ligar-se utilizando um servidor web proxy.

- Os sistemas de site que suportam o IBCM requerem uma ligação à Internet, e devem estar num domínio de Diretório Ativo. Os sistemas de sites baseados na Internet não requerem uma relação de confiança com a floresta de Diretório Ativo do servidor do site. No entanto, quando o ponto de gestão baseado na Internet pode autenticar o utilizador utilizando a autenticação do Windows, suporta as políticas dos utilizadores. Se a autenticação do Windows falhar, apenas suporta as políticas do dispositivo.

    > [!NOTE]
    > Para apoiar as políticas dos utilizadores, também ative as seguintes definições de cliente no grupo **Política do Cliente:**
    >
    > - **Ativar consulta de política de utilizador nos clientes**
    > - **Ativar pedidos da política do utilizador dos clientes Internet**  

- Uma infraestrutura de chave pública (PKI) para implementar e gerir os certificados necessários para clientes baseados na Internet e servidores de sistemas de sites. Para mais informações, consulte os requisitos do [certificado PKI](../../plan-design/network/pki-certificate-requirements.md).

- Registe as entradas públicas de anfitriões do DNS para os nomes de domínio totalmente qualificados da Internet (FQDN) dos sistemas de site que suportam o IBCM.

### <a name="client-communication-requirements"></a>Requisitos de comunicação do cliente

Firewalls ou servidores proxy intervenientes devem permitir a comunicação do cliente para sistemas de sites baseados na Internet:

- Suportar HTTP 1.1  

- Permitir que o tipo de conteúdo HTTP do anexo multiparte de MIME (multiparte/misto e aplicação/sequência de octetos)  

#### <a name="verbs"></a>Verbos

Permitir os seguintes verbos para as funções do servidor do sistema de site baseado na Internet:

| Função | Verbos |
|------|-------|
| Ponto de gestão | - CABEÇA<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Ponto de distribuição | - CABEÇA<br>- GET<br>- PROPFIND |
| Ponto de estado de contingência | POST |
| Ponto de site do catálogo de aplicações | -POST<br>- GET |

#### <a name="http-headers"></a>Cabeçalhos HTTP

Permitir os seguintes cabeçalhos HTTP para as funções do servidor do sistema de site baseado na Internet:

| Função | Cabeçalhos HTTP |
|------|--------------|
| Ponto de gestão | - Intervalo:<br>- CCMClientID:<br>- CCMClientIDAssinatura:<br>- CCMClientTimestamp:<br>- CCMClientTimesesAssinatura: |
| Ponto de distribuição | Intervalo: |

Para obter requisitos de comunicação semelhantes quando utilizar o ponto de atualização de software para ligações ao cliente a partir da internet, consulte a documentação para os Serviços de Atualização do Servidor do Windows (WSUS).

## <a name="unsupported-features"></a>Características não suportadas

Nem todas as funcionalidades de gestão de clientes são apropriadas para a internet. O Gestor de Configuração não suporta algumas funcionalidades para clientes na internet. Estas funcionalidades não suportadas normalmente dependem de Serviços de Domínio de Diretório Ativo ou não são apropriadas para uma rede pública.

As seguintes funcionalidades não são suportadas quando gere clientes na internet com IBCM:

- Implementação de clientes através da internet, como o push do cliente e a implementação de clientes baseados em atualizações de software. Utilize a instalação manual do cliente.

- Atribuição automática de site

- Wake-on-LAN

- Implantação de SO. No entanto, pode implementar sequências de tarefas que não implementem um Sistema Operativo.

- Controlo remoto

- Implementação de software para utilizadores. Esta funcionalidade baseia-se no catálogo de aplicações, que é depreciado.

- Cliente a vaguear. O roaming permite aos clientes localizar sempre os pontos de distribuição mais próximos para transferir conteúdo. Os clientes não selecionam determinicamente um dos sistemas de site baseados na Internet, qualquer que seja a largura de banda ou a localização física.

Quando configura um ponto de atualização de software para aceitar ligações a partir da internet, os clientes baseados na Internet sempre digitalizam contra este ponto de atualização de software para determinar quais as atualizações de software necessárias. Quando estes clientes estão na internet, primeiro tentam descarregar as atualizações de software a partir do Microsoft Update, em vez de um ponto de distribuição baseado na Internet. Se este comportamento falhar, tentam então descarregar as atualizações de software necessárias a partir de um ponto de distribuição baseado na Internet.

> [!TIP]
> O cliente do Gestor de Configuração determina automaticamente se está na intranet ou na internet. Se o cliente puder contactar um controlador de domínio ou um ponto de gestão no local, define o seu tipo de ligação para "Atualmente *intranet".* Caso contrário, muda para "Atualmente *internet",* e comunica com os sistemas do site atribuídos ao seu site.
