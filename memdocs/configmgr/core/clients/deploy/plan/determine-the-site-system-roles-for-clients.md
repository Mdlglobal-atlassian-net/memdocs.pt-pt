---
title: Funções do sistema do site para clientes
titleSuffix: Configuration Manager
description: Determine as funções do sistema do site para clientes no Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713248"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Determine as funções do sistema do site para clientes do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo pode ajudá-lo a determinar as funções do sistema do site que precisa para implementar clientes do Gestor de Configuração.

Para obter mais informações sobre onde instalar estas funções na hierarquia, consulte [Design uma hierarquia de sites.](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

Para obter mais informações sobre como instalar e configurar estas funções, consulte [instalar as funções](../../../servers/deploy/configure/install-site-system-roles.md)do sistema do site.  

## <a name="management-point"></a>Ponto de gestão

Por padrão, todos os computadores clientes do Windows utilizam um ponto de distribuição para instalar o cliente Do Gestor de Configuração. Podem voltar a um ponto de gestão quando um ponto de distribuição não está disponível. No entanto, pode instalar clientes do Windows em computadores a partir de `/source:<Path>`uma fonte alternativa quando utilizar a propriedade da linha de comando CCMSetup . Por exemplo, pode fazer esta ação se instalar clientes na internet. Outro cenário é quando pretende evitar o envio de pacotes de rede entre o computador e o ponto de gestão durante a instalação do cliente. Este cenário deve-se ao facto de uma firewall bloquear as portas necessárias ou porque tem uma ligação de baixa largura de banda. No entanto, todos os clientes devem comunicar com um ponto de gestão para atribuir a um site e ser geridos pelo Gestor de Configuração.  

Para mais informações sobre as propriedades da linha de comando do cliente, consulte as propriedades de [instalação do cliente.](../about-client-installation-properties.md)  

Quando instala mais de um ponto de gestão na hierarquia, os clientes ligam-se automaticamente a um ponto com base na sua adesão à floresta e localização da rede. Não pode instalar mais do que um ponto de gestão num local secundário.  

Os clientes de computador Mac e clientes de dispositivos móveis que você se inscreve com O Gestor de Configuração sempre requerem um ponto de gestão para a instalação do cliente. Este ponto de gestão deve estar num site primário, deve ser configurado para suportar dispositivos móveis, e deve aceitar ligações do cliente a partir da Internet. Estes clientes não podem usar pontos de gestão em sites secundários ou conectar-se a pontos de gestão em outros sites primários.  

## <a name="distribution-point"></a>Ponto de distribuição

Não é necessário um ponto de distribuição para instalar clientes do Gestor de Configuração nos computadores Windows. Por predefinição, o Gestor de Configuração utiliza um ponto de distribuição para instalar os ficheiros de origem do cliente nos computadores Windows. Pode voltar a descarregar estes ficheiros a partir de um ponto de gestão. Os pontos de distribuição não são utilizados para instalar clientes de dispositivos móveis que estão matriculados pelo Gestor de Configuração, mas são utilizados se instalar o cliente legado do dispositivo móvel. Se instalar o cliente do Gestor de Configuração como parte de uma implementação de SO, a imagem de OS é armazenada e recuperada a partir de um ponto de distribuição.

Embora não precise de pontos de distribuição para instalar a maioria dos clientes do Gestor de Configuração, vai precisar deles para instalar software, como aplicações e atualizações de software nos clientes.  

## <a name="fallback-status-point"></a>Ponto de estado de contingência

Pode utilizar um ponto de estado de recuo para monitorizar a implementação do cliente para computadores Windows. Também pode identificar os clientes de computador windows que não são geridos porque não conseguem comunicar com um ponto de gestão.

Os seguintes tipos de clientes não usam um ponto de estado de recuo:

- Computadores Mac
- Dispositivos móveis que são matriculados pelo Gestor de Configuração
- Dispositivos móveis que são geridos utilizando o conector Exchange Server

Um ponto de estado de recuo não é necessário para monitorizar a atividade do cliente e a saúde do cliente.  

O ponto de estado de recuo comunica sempre com os clientes através do HTTP, que utiliza ligações não autenticadas e envia dados em texto claro. Este comportamento torna o ponto de situação de recuo vulnerável a ataques, especialmente quando é usado com a gestão de clientes baseada na Internet. Para ajudar a reduzir a superfície de ataque, dedique sempre um servidor a executar o ponto de estado de recuo. Não instale outras funções do sistema do site no mesmo servidor num ambiente de produção.  

Instale um ponto de estado de recuo se se aplicarem todas as seguintes condições:  

- Pretende que os erros de comunicação dos clientes dos computadores Windows sejam enviados para o site, mesmo que estes computadores clientes não possam comunicar com um ponto de gestão.  

- Deseja utilizar os relatórios de implementação do cliente do Gestor de Configuração, que exibem os dados enviados pelo ponto de estado de recuo.  

- Tem um servidor dedicado para este sistema de site e tem medidas de segurança adicionais para ajudar a proteger o servidor de ataques.  

- Os benefícios da utilização de um ponto de situação de recuo superam quaisquer riscos de segurança associados a ligações não autenticadas e transferências de texto claras sobre o tráfego HTTP.  

Não instale um ponto de estado de recuo se os riscos de segurança de executar um website com ligações não autenticadas e transferências claras de texto superam os benefícios de identificar problemas de comunicação do cliente.  

## <a name="reporting-services-point"></a>Ponto do Reporting Services

O Gestor de Configuração fornece muitos relatórios para o ajudar a monitorizar a instalação, atribuição e gestão de clientes na consola Do Gestor de Configuração. Alguns dos relatórios de implementação do cliente exigem que os clientes sejam designados para um ponto de estado de recuo.  

Os relatórios não são necessários para mobilizar clientes. Pode ver algumas informações de implementação na consola do Gestor de Configuração ou utilizar os ficheiros de registo do cliente para obter informações detalhadas. No entanto, os relatórios do cliente fornecem informações valiosas para ajudar a monitorizar e resolver problemas na implementação do cliente.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Ponto de registo e ponto proxy de registo

O Gestor de Configuração requer o ponto de inscrição e o ponto de procuração de inscrição para inscrever dispositivos móveis e inscrever certificados para computadores Mac. Não precisa destas funções do sistema do site nas seguintes situações:

- Planeia gerir dispositivos móveis utilizando o conector Exchange Server
- Instala o cliente legado do dispositivo móvel, por exemplo, para o Windows CE
- Solicita e instala o certificado de cliente em computadores Mac independentemente do Gestor de Configuração

## <a name="application-catalog"></a>Catálogo de aplicações

> [!Important]  
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Ponto de conector de gateway de gestão de nuvem

Você precisa de um ponto de conector de gateway de gestão de nuvem se você estiver configurando uma porta de entrada de [gestão](../../manage/cmg/plan-cloud-management-gateway.md) de nuvem para [gerir os clientes na internet](../../manage/manage-clients-internet.md).
