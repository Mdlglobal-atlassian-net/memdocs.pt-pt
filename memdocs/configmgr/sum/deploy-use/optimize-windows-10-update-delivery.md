---
title: Otimizar a entrega de atualizações do Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Gestor de Configuração para gerir os conteúdos da atualização para se manter atual com o Windows 10.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7edd05a7b1ce105e81fd4f594d95c9dfb45f472
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771376"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Otimizar a entrega da atualização do Windows 10 com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para muitos clientes, um caminho bem sucedido para obter e manter-se atual com as atualizações mensais do Windows 10 começa com uma boa estratégia de distribuição de conteúdo usando o Gestor de Configuração. A dimensão das atualizações mensais de qualidade pode ser motivo de preocupação para as grandes organizações. Existem algumas tecnologias disponíveis que se destinam a ajudar a reduzir a largura de banda e a carga de rede para otimizar a entrega da atualização. Este artigo explica estas tecnologias, compara-as e fornece recomendações para ajudá-lo a tomar decisões sobre qual usar.  
 
O Windows 10 fornece vários tipos de atualizações. Para mais informações, consulte [os tipos de Atualização do Windows para O Negócios](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Este artigo foca-se nas atualizações de *qualidade* do Windows 10 com o Gestor de Configuração. 


## <a name="express-update-delivery"></a>Entrega de atualização expressa

Os downloads de atualização de qualidade do Windows 10 podem ser grandes. Cada pacote contém todas as correções previamente lançadas para garantir a consistência e a simplicidade. A Microsoft conseguiu reduzir o tamanho do conteúdo de atualização do Windows 10 que cada cliente descarrega com uma funcionalidade chamada express. O Expresso é hoje utilizado por milhões de dispositivos que retiram atualizações diretamente do serviço Windows Update e reduzsignificativamente o tamanho do download. Este benefício também está disponível para clientes cujos clientes não descarregam diretamente do serviço Windows Update. 

O Gestor de Configuração adicionou suporte para ficheiros de [instalação expresso](manage-express-installation-files-for-windows-10-updates.md) de atualizações de qualidade do Windows 10 na versão 1702. No entanto, para a melhor experiência, recomenda-se que utilize a versão 1802 do Gestor de Configuração. Para obter o melhor desempenho nas velocidades de descarregamento, recomenda-se também que utilize o Windows 10, a versão 1703 ou mais tarde. 

> [!NOTE]  
> O conteúdo da versão expressa é consideravelmente maior do que a versão completa. Um ficheiro de instalação expresso contém todas as variações possíveis para cada ficheiro que pretende atualizar. Como resultado, a quantidade necessária de espaço em disco aumenta para atualizações na fonte do pacote de atualização e nos pontos de distribuição quando ativa o suporte expresso no Gestor de Configuração. Embora o requisito de espaço do disco nos pontos de distribuição aumente, o tamanho do conteúdo que os clientes descarregam a partir destes pontos de distribuição diminui. Os clientes apenas descarregam os bits que necessitam (deltas) mas não toda a atualização.


## <a name="peer-to-peer-content-distribution"></a>Distribuição de conteúdo entre pares

Mesmo que os clientes descarreguem apenas as partes do conteúdo que necessitam, acelere as atualizações do Windows no seu ambiente utilizando a distribuição de conteúdos peer-to-peer. Aproveitar os pares como fonte de descarregamento para atualizações de qualidade pode ser benéfico para ambientes onde os pontos de distribuição locais não estão presentes em escritórios remotos. Este comportamento impede a necessidade de todos os clientes descarregarem conteúdo de um ponto de distribuição remoto através de um link WAN lento. A utilização de pares também pode ser benéfica quando os clientes recaem para o serviço Deatualização do Windows. Apenas um par é necessário para descarregar conteúdo de atualização a partir da nuvem antes de o disponibilizar para outros dispositivos.

O Gestor de Configuração suporta muitas tecnologias peer-to-peer, incluindo as seguintes:
- Otimização de Entrega de Janelas
- Cache de pares do Gestor de Configuração
- Windows BranchCache  

As secções seguintes fornecem mais informações sobre estas tecnologias.

### <a name="windows-delivery-optimization"></a>Otimização de Entrega de Janelas

[A Otimização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) da Entrega é a principal tecnologia de descarregamento e método de distribuição peer-to-peer incorporado no Windows 10. Os clientes do Windows 10 podem obter conteúdos de outros dispositivos na sua rede local que descarregam as mesmas atualizações. Utilizando as [opções do Windows disponíveis para otimização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)de entrega, pode configurar os clientes em grupos. Este agrupamento permite à sua organização identificar dispositivos que são possivelmente os melhores candidatos para satisfazer pedidos peer-to-peer. A Otimização da Entrega reduz significativamente a largura de banda geral que é usada para manter os dispositivos atualizados enquanto acelera o tempo de descarregamento.

> [!NOTE]  
> Otimização de Entrega é uma solução gerida pela nuvem. O acesso à Internet ao serviço de cloud de otimização de entregas é um requisito para utilizar a sua funcionalidade peer-to-peer. Para obter informações sobre os pontos finais da Internet necessários, consulte [frequentemente perguntas para otimização de entregas.](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions) 

Para obter os melhores resultados, poderá ser necessário definir o modo de [descarregamento](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) de Otimização de Entrega para **grupo (2)** e definir *IDs do Grupo*. No modo de grupo, o peering pode cruzar subredes internas entre dispositivos que pertencem ao mesmo grupo, incluindo dispositivos em escritórios remotos. Utilize a [opção id do grupo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) para criar o seu próprio grupo personalizado independentemente de domínios e sites AD DS. O modo de descarregamento de grupo é a opção recomendada para a maioria das organizações que procuram alcançar a melhor otimização da largura de banda com otimização de entrega.

Configurar manualmente estes IDs do Grupo é um desafio quando os clientes vagueiam por diferentes redes. A versão 1802 do Gestor de Configuração adicionou uma nova funcionalidade para simplificar a gestão deste [processo, integrando grupos de fronteira com otimização](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)de entrega . Quando um cliente acorda, fala com o seu ponto de gestão para obter políticas, e fornece a sua rede e informações de grupo de fronteiras. O Gestor de Configuração cria um ID único para cada grupo de fronteiras. O site utiliza as informações de localização do cliente para configurar automaticamente o ID do Grupo de Otimização de Entrega do cliente com o ID de limite do Gestor de Configuração. Quando o cliente vagueia para outro grupo de fronteiras, fala até ao seu ponto de gestão, e é automaticamente reconfigurado com um novo ID de grupo de limites. Com esta integração, a Otimização de Entrega pode utilizar as informações do grupo de limites do Gestor de Configuração para encontrar um par a partir do qual descarregar atualizações.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a>Otimização de Entrega a partir da versão 1910
<!--4699118-->
A partir da versão 1910 do Gestor de Configuração, pode utilizar a Otimização de Entrega para a distribuição de todos os conteúdos de atualização do Windows para clientes que executem a versão 1709 do Windows 10 ou mais tarde, e não apenas ficheiros de instalação expresso.

Para utilizar a Otimização da Entrega para todos os ficheiros de instalação de atualizações do Windows, ative as [seguintes atualizações](../../core/clients/deploy/about-client-settings.md#software-updates)de software do cliente:

- **Permitir que os clientes descarreguem conteúdo delta quando disponível** definido para **Sim**.
- **Porta que os clientes usam para receber pedidos de conteúdo delta** definido para 8005 (padrão) ou um número de porta personalizado.

> [!IMPORTANT]
> - A otimização da entrega deve ser ativada (predefinida) e não ignorada. Para mais informações, consulte a referência da [Otimização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference)da Entrega do Windows .
> - Verifique [as definições](../../core/clients/deploy/about-client-settings.md#delivery-optimization) do cliente da Otimização da Entrega ao alterar as definições do cliente de [atualizações](../../core/clients/deploy/about-client-settings.md#software-updates) de software para conteúdo delta.
> - A Otimização da Entrega não pode ser utilizada para atualizações de clientes do Office 365 se o Office COM estiver ativado. O Office COM é utilizado pelo Gestor de Configuração para gerir atualizações para clientes do Office 365. Pode desregistar o Office COM para permitir a utilização da Otimização de Entregas para as atualizações do Office 365. Quando o Office COM é desativado, as atualizações de software para o Office 365 são geridas pela tarefa programada de Atualizações Automáticas do Office 2.0. Isto significa que o Gestor de Configuração não dita ou monitoriza o processo de instalação para atualizações do Office 365. O Gestor de Configuração continuará a recolher informações do inventário de hardware para preencher o Office 365 Client Management Dashboard na consola. Para obter informações sobre como desregistrar o Office COM, consulte [enable Office 365 clientes para receber atualizações do Office CDN em vez de Configuração Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - Ao utilizar um CMG para armazenamento de conteúdo, o conteúdo para atualizações de terceiros não será descarregado para os clientes se o conteúdo delta de Download quando a [definição](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) de cliente **disponível** estiver ativada. <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Cache de pares do Gestor de Configuração

[O cache peer](../../core/plan-design/hierarchy/client-peer-cache.md) é uma funcionalidade do Gestor de Configuração que permite aos clientes partilhar em conjunto com outros conteúdos de clientes diretamente a partir do seu cache local de Configuração Manager. A cache dos pares não substitui o uso de outras soluções de cache de pares como o Windows BranchCache. Trabalha em conjunto com eles para fornecer mais opções para alargar as soluções tradicionais de implementação de conteúdos, como pontos de distribuição. A cache dos pares não depende da BranchCache. Se não ativar ou utilizar branchCache, a cache dos pares ainda funciona.

> [!NOTE]  
> Os clientes só podem descarregar conteúdo de clientes de cache peer que estão no seu atual grupo de limites.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia de otimização de largura de banda no Windows. Cada cliente tem uma cache, e atua como uma fonte alternativa para o conteúdo. Os dispositivos da mesma rede podem solicitar este conteúdo. [O Gestor de Configuração pode utilizar](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) o BranchCache para permitir que os pares obtem conteúdo uns dos outros versus sempre ter de contactar um ponto de distribuição. Utilizando a BranchCache, os ficheiros são em cache em cada cliente individual, e outros clientes podem recuperá-los conforme necessário. Esta abordagem distribui a cache em vez de ter um único ponto de recuperação. Este comportamento poupa uma quantidade significativa de largura de banda, reduzindo ao mesmo tempo o tempo para os clientes receberem o conteúdo solicitado.



## <a name="selecting-the-right-peer-caching-technology"></a>Selecionando a tecnologia de cache de pares certos

A seleção da tecnologia de cache de pares adequado para ficheiros de instalação expresso depende do seu ambiente e requisitos. Mesmo que o Gestor de Configuração suporte todas as tecnologias par-a-par acima, deve utilizar aquelas que fazem mais sentido para o seu ambiente. Para a maioria dos clientes, assumindo que os clientes podem cumprir os requisitos de Internet para otimização de entregas, o Windows 10 incorporado peer caching com otimização de entrega deve ser suficiente. Se os seus clientes não conseguirem satisfazer estes requisitos de internet, considere utilizar a funcionalidade de cache de pares do Gestor de Configuração. Se está a utilizar o BranchCache com o Gestor de Configuração e ele satisfaz todas as suas necessidades, então expresse ficheiros com branchCache pode ser a opção certa para si. 

### <a name="peer-cache-comparison-chart"></a>Gráfico de comparação de cache peer


| Funcionalidade  | Otimização de Entrega  | Cache de pares  | BranchCache  |
|---------|---------|---------|---------|
| Suportado através de subredes | Sim | Sim | Não |
| Estrangulamento da largura de banda | Sim (Nativo) | Sim (via BITS) | Sim (via BITS) |
| Suporte parcial de conteúdo | Sim, para todos os tipos de conteúdo suportados listados na próxima linha desta coluna. | Apenas para Office 365 e Express Updates | Sim, para todos os tipos de conteúdo suportados listados na próxima linha desta coluna. |
| Tipos de conteúdo suportado | **Através da ConfigMgr:** </br> - Atualizações expressas </br> - Todas as atualizações do Windows (versão inicial de 1910). Isto não inclui atualizações do Office.</br> </br> **Através da nuvem da Microsoft:**</br> - Atualizações de janelas e segurança</br> - Motoristas</br> - Aplicativos Windows Store</br> - Windows Store for Business apps | Todos os tipos de conteúdo da ConfigMgr, incluindo imagens descarregadas no [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Todos os tipos de conteúdo configMgr, exceto imagens |
| Tamanho da cache no controlo do disco | Sim | Sim | Sim |
| Descoberta de uma fonte de pares | Automático | Manual (definição de agente cliente) | Automático |
| Descoberta de pares | Através do serviço de nuvem de otimização de entrega (requer acesso à Internet) | Através de ponto de gestão (baseado em grupos de fronteira de clientes) | Multicast |
| Relatórios | Sim (usando desktop analytics) | Painel de dados de dados do cliente ConfigMgr | Painel de dados de dados do cliente ConfigMgr |
| Controlo de utilização wan | Sim (nativo, pode ser controlado através de definições políticas de grupo) | Grupos de limites | Suporte de sub-rede apenas |
| Gestão através da ConfigMgr | Parcial (definição de agente cliente) | Sim (definição de agente cliente) | Sim (definição de agente cliente) |



## <a name="conclusion"></a>Conclusão

A Microsoft recomenda que otimize a entrega de atualizações de qualidade do Windows 10 utilizando o Configurador com ficheiros de instalação expresso e uma tecnologia de cache de pares, conforme necessário. Esta abordagem deverá aliviar os desafios associados aos dispositivos do Windows 10 que descarregam grandes conteúdos para instalar atualizações de qualidade. É também recomendado manter os dispositivos Windows 10 atualizados, implementando atualizações de qualidade todos os meses. Esta prática reduz o delta dos conteúdos de atualização de qualidade necessários pelos dispositivos todos os meses. A redução deste conteúdo delta provoca transferências de tamanho menor a partir de pontos de distribuição ou fontes de pares. 

Devido à natureza dos ficheiros de instalação expresso, o seu tamanho de conteúdo é consideravelmente maior do que os ficheiros tradicionais autossuficientes. Este tamanho resulta em tempos de descarregamento de atualização mais longos do serviço de Atualização do Windows para o servidor do site Do Configuração. A quantidade de espaço em disco necessário tanto para o servidor do site como para os pontos de distribuição também aumenta. O tempo total necessário para descarregar e distribuir atualizações de qualidade pode ser mais longo. No entanto, os benefícios do dispositivo devem ser percetíveis durante o download e instalação de atualizações de qualidade pelos dispositivos Windows 10. Para mais informações, consulte [A Utilização de Ficheiros](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files)de Instalação Expresso .

Se as trocas do lado do servidor de atualizações de maior dimensão forem bloqueadores para a adoção de suporte expresso, mas os benefícios do lado do dispositivo são cruciais para o seu negócio e ambiente, a Microsoft recomenda que utilize o [Windows Update para Negócios](integrate-windows-update-for-business-windows-10.md) com O Gestor de Configuração. O Windows Update for Business fornece todos os benefícios do expresso sem a necessidade de descarregar, armazenar e distribuir ficheiros de instalação expresso em todo o seu ambiente. Os clientes descarregam conteúdos diretamente do serviço Windows Update, pelo que ainda podem utilizar a Otimização de Entrega.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Perguntas frequentes

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Como é que os downloads do Windows express funcionam com o Gestor de Configuração?

O agente de atualização do Windows (WUA) solicita primeiro conteúdo expresso. Se não instalar a atualização expressa, pode voltar à atualização completa do ficheiro.  

1. O cliente do Gestor de Configuração diz à WUA para descarregar o conteúdo da atualização. Quando a WUA inicia um download expresso, primeiro descarrega `Windows10.0-KB1234567-<platform>-express.cab`um stub (por exemplo, que faz parte do pacote expresso.  

2. WuA passa este stub para o instalador de atualização windows, manutenção baseada em componentes (CBS). A CBS usa o canhoto para fazer um inventário local, comparando os deltas do ficheiro no dispositivo com o necessário para chegar à versão mais recente do ficheiro que está a ser oferecido.  

3. A CBS pede então à WUA que descarregue as gamas necessárias a partir de um ou mais ficheiros expresso .psf.  

4. A Otimização da Entrega coordena com o Gestor de Configuração e descarrega as gamas a partir de um ponto de distribuição local ou pares, se disponível. Se a Otimização da Entrega estiver desativada, o Serviço de Transferência Inteligente de Fundo (BITS) é utilizado da mesma forma que o Gestor de Configuração coordena as fontes de cache dos pares. Otimização de Entrega ou BITS passa as gamas para WUA, o que os coloca à disposição da CBS para aplicar e instalar.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Por que os ficheiros expressos (.psf) são tão grandes quando armazenados em fontes de pares do Gestor de Configuração na pasta ccmcache?

Os ficheiros expresso (.psf) são ficheiros escassos. Para determinar o espaço real utilizado no disco pelo ficheiro, verifique o **tamanho na** propriedade do disco do ficheiro. O tamanho da propriedade do disco deve ser consideravelmente menor do que o valor tamanho.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>O Gestor de Configuração suporta ficheiros de instalação expresso com atualizações de funcionalidades do Windows 10?

Não, o Gestor de Configuração atualmente apenas suporta ficheiros de instalação expresso com atualizações de qualidade do Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quanto espaço em disco é necessário por atualização de qualidade no servidor do site e pontos de distribuição?

Depende. Para cada atualização de qualidade, tanto a versão completa como a versão expressa da atualização são armazenadas nos servidores. As atualizações de qualidade do Windows 10 são cumulativas, pelo que o tamanho destes ficheiros aumenta todos os meses. Planeie um mínimo de 5 GB por atualização por idioma. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Os clientes do Gestor de Configuração ainda beneficiam de ficheiros de instalação expresso quando voltam ao serviço de Atualização do Windows?

Sim. Se utilizar a seguinte opção de implementação de atualização de software, os clientes ainda utilizam atualizações expressas e otimização de entrega quando voltam ao serviço de nuvem:  

**Se as atualizações de software não estiverem disponíveis no ponto de distribuição em grupos atuais, vizinhos ou sites, descarregue o conteúdo a partir de Microsoft Updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Porque é que o conteúdo de ficheiro expresso não é descarregado para atualizações existentes depois de eu ativar o suporte de ficheiroexpresso? 

As alterações só surtam efeito para quaisquer novas atualizações sincronizadas e implementadas após o suporte de habilitação.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Existe alguma forma de ver quanto conteúdo é descarregado dos pares usando a Otimização de Entrega?
O Windows 10, a versão 1703 (e mais tarde) inclui dois novos cmdlets PowerShell, **Get-DeliveryOptimizationPerfSnap** e **Get-DeliveryOptimizationStatus**. Estes cmdlets fornecem mais informações sobre a otimização da entrega e o uso da cache. Para mais informações, consulte [otimização de entrega para atualizações do Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Como é que os clientes comunicam com a Otimização de Entrega através da rede?
Para obter mais informações sobre as portas de rede, requisitos de procuração e nomes de anfitriões para firewalls, consulte [faQs para otimização de entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Ficheiros de registo

Utilize os seguintes ficheiros de registo para monitorizar os downloads delta:

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>Passos seguintes

- [Deploy software updates](deploy-software-updates.md)
- [Automatically deploy software updates](automatically-deploy-software-updates.md)
