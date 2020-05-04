---
title: Suporte para funcionalidades windows
titleSuffix: Configuration Manager
description: Saiba quais os suportes do Windows e do Networking Configuração Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e8e65571a3902661176ca3840690c159faef416
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709622"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Suporte para funcionalidades e redes do Windows no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo identifica o suporte do Gestor de Configuração para funcionalidades comuns do Windows e de rede.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  

Utilize o Windows BranchCache com o Configuror quando o ativar em pontos de distribuição e configure os clientes para o utilizarem no modo de cache distribuído.

Configure as definições do BranchCache num tipo de implementação para aplicações, na implementação de um pacote e para sequências de tarefas. A partir da versão 1802, a BranchCache está ativada por padrão.

Quando os requisitos para branchCache são cumpridos, esta funcionalidade permite aos clientes em locais remotos obter conteúdo de clientes locais que tenham uma cache atual do conteúdo.  

Por exemplo, quando o primeiro cliente ativado pela BranchCache solicita conteúdo a partir de um ponto de distribuição configurado como um servidor BranchCache, o cliente descarrega e cache o conteúdo. Este conteúdo é então disponibilizado aos clientes na mesma subnet que solicitou este conteúdo.

Estes clientes também cache o conteúdo. Outros clientes na mesma subnet não têm de descarregar conteúdo a partir do ponto de distribuição. O conteúdo é distribuído por vários clientes para futuras transferências.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Requisitos para apoiar BranchCache com Gestor de Configuração

#### <a name="configure-distribution-points"></a>Configure pontos de distribuição

Adicione a funcionalidade **Windows BranchCache** ao servidor do sistema do site que está configurado como um ponto de distribuição.

- Os pontos de distribuição nos servidores configurados para suportar branchCache não requerem configuração adicional.
- Não é possível adicionar o Windows BranchCache a um ponto de distribuição baseado na nuvem. Os pontos de distribuição baseados na nuvem suportam o download de conteúdos por clientes que estão configurados para o Windows BranchCache.  

#### <a name="configure-clients"></a>Configure clientes

- Os clientes que podem suportar branchCache devem ser configurados para o modo de cache distribuído BranchCache.  
- A definição de OS para configurações de cliente BITS deve ser ativada para suportar branchCache.  

Para obter informações, consulte os [clientes configurados para BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) na documentação do Windows.

Todos os Gestores de Configuração suportavam versões do Suporte do Windows BranchCache por padrão.

Para mais informações, consulte [BranchCache para Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) na documentação do Windows Server.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a>Computadores em grupos de trabalho  

O Gestor de Configuração fornece suporte para clientes em grupos de trabalho.  

- O Gestor de Configuração suporta a mudança de um cliente de um grupo de trabalho para um domínio ou de um domínio para um grupo de trabalho. Para mais informações, consulte [como instalar clientes do Gestor de Configuração em computadores de grupo de trabalho](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> Embora os clientes em grupos de trabalho sejam apoiados, todos os sistemas de site devem ser membros de um domínio de Diretório Ativo suportado.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a>Deduplicação de dados

O Gestor de Configuração suporta a utilização de duplicação de dados com pontos de distribuição no Windows Server 2012 ou posterior.

> [!IMPORTANT]  
> O volume que acolhe ficheiros de origem de pacotes não pode ser marcado para a duplicação de dados. Esta limitação deve-se ao facto de a desduplicação de dados utilizar pontos de reparse. O Gestor de Configuração não suporta a utilização de uma localização de fonte de conteúdo com ficheiros armazenados em pontos reparsos.  

Para mais informações, consulte os seguintes posts:

- Pontos de distribuição do Gestor de [Configuração e deduplicação de dados do Windows Server 2012](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) no blog da equipa do Gestor de Configuração

- Visão [geral da deduplicação de dados](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) na documentação do Servidor do Windows

## <a name="directaccess"></a><a name="bkmk_DA"></a>Acesso Direto  

O Gestor de Configuração suporta a funcionalidade DirectAccess para comunicação entre clientes e sistemas de servidores do site.  

- Quando todos os requisitos para o DirectAccess são cumpridos, permite que os clientes do Gestor de Configuração na internet comuniquem com o seu site designado como se estivessem na intranet.  

- Para ações iniciadas pelo servidor, tais como controlo remoto e instalação de impulso do cliente, o computador de iniciação deve estar a executar o IPv6. Este protocolo deve ser suportado em todos os dispositivos de rede intervenientes.  

O Gestor de Configuração não suporta a seguinte funcionalidade sobre o DirectAccess:  

- Implementação de SO

- Comunicação entre sites do Gestor de Configuração  

- Comunicação entre servidores do sistema do Gestor de Configuração dentro de um site  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a>Computadores de dupla bota  

O Gestor de Configuração não consegue gerir mais do que um SISTEMA num único computador. Se houver mais de um SISTEMA num computador para gerir, ajuste os métodos de descoberta e instalação do cliente do site para garantir que o cliente do Gestor de Configuração esteja instalado apenas no SISTEMA que tem de ser gerido.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a>IPv6  

Além da versão 4 do Protocolo de Internet (IPv4), o Gestor de Configuração suporta a versão 6 do Protocolo de Internet (IPv6), com as seguintes exceções:  

|Função| Exceção no suporte de IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados na nuvem|O IPv4 é necessário para suportar pontos de distribuição baseados na nuvem e do Microsoft Azure.|  
|Gateway de gestão da cloud|O IPv4 é necessário para suportar o Microsoft Azure e o portal de gestão de nuvem.|  
|Dispositivos móveis que estão matriculados pela Microsoft Intune e pelo conector de serviço da Microsoft|O IPv4 é necessário para suportar dispositivos móveis que estejam matriculados pela Microsoft Intune e pelo conector de serviço da Microsoft.|  
|Deteção de Redes|O IPv4 é necessário quando configura o servidor DHCP para procurar na Deteção de Redes.|  
|Implementação de SO|Na versão 1802 e anterior, o IPv4 é necessário para suportar a implementação do OS.  </br> </br> A partir da versão 1806, ative um resposta PXE num ponto de distribuição sem o Windows Deployment Service. Este novo serviço de resposta PXE suporta o IPv6. Outros aspetos da função de implementação do OS, tais como capturar ou definir endereços IP estáticos durante a sequência de tarefas, continuam a exigir IPv4. |  
|Comunicação do proxy de reativação|O IPv4 é necessário para suportar os pacotes do proxy de reativação do cliente.|  
|Windows CE|O IPv4 é necessário para suportar o cliente do Gestor de Configuração nos dispositivos CE do Windows.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a>Tradução de endereçode rede  

A Tradução de Endereços de Rede (NAT) não é suportada no Gestor de Configuração, a menos que o site suporte clientes que estão na internet e o cliente detete que está ligado à internet. Para obter mais informações sobre a gestão de clientes baseados na Internet, consulte [o Plano de Gestão de Clientes baseados na Internet.](../../clients/manage/plan-internet-based-client-management.md)  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a>Tecnologia de armazenamento especializada  

O Gestor de Configuração trabalha com qualquer hardware certificado na Lista de Compatibilidade de Hardware do Windows para a versão do SISTEMA em que o componente De Configuração manager está instalado.

As funções do servidor do site requerem NTFS, para que o Gestor de Configuração possa definir permissões de diretório e ficheiros. O Gestor de Configuração assume que tem a propriedade completa de uma unidade lógica. Os sistemas de sites que funcionam em computadores separados não podem partilhar uma partilha lógica em qualquer tecnologia de armazenamento. No entanto, os computadores conseguem utilizar uma partição lógica na mesma partição física de um dispositivo de armazenamento.  

### <a name="support-considerations"></a>Considerações de apoio

- **Rede de Área**de Armazenamento : Uma Rede de Área de Armazenamento (SAN) é suportada quando um servidor baseado no Windows suportado é ligado diretamente ao volume que é hospedado pelo SAN.  

- **Armazenamento de instância única**: O Gestor de Configuração não suporta a configuração do pacote de pontos de distribuição e das pastas de assinatura num volume de armazenamento de instância única (SIS).  

     Além disso, a cache de um cliente do Gestor de Configuração não é suportada num volume ativado pelo SIS.  

- **Unidade de disco amovível**: O Gestor de Configuração não suporta a instalação de sistemas de site do Gestor de Configuração ou clientes numa unidade de disco amovível.  
