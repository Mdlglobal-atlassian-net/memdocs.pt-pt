---
title: Pré-visualização técnica 1803
titleSuffix: Configuration Manager
description: Conheça as novas funcionalidades disponíveis na versão de Pré-visualização Técnica do Gestor de Configuração 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719044"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1803 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1803. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja o artigo [de Pré-visualização Técnica](technical-preview.md) antes de instalar esta atualização. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pontos de distribuição suportam pontos de distribuição em nuvem como fonte  
<!--1321554-->
Muitos clientes usam [pontos de distribuição de puxar](../plan-design/hierarchy/use-a-pull-distribution-point.md) em agências remotas ou sucursais, que descarregam conteúdo de um ponto de distribuição de fonte através do WAN. Se os seus escritórios remotos tiverem uma melhor ligação à internet ou para reduzir a carga nas suas ligações WAN, pode agora utilizar um ponto de distribuição em [nuvem](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) no Microsoft Azure como fonte. Quando adiciona uma fonte no separador **Pull Distribution Point** das propriedades do ponto de distribuição, qualquer ponto de distribuição em nuvem no site está agora listado como um ponto de distribuição disponível. O comportamento de ambas as funções do sistema do site continua a ser o mesmo de outra forma. 

### <a name="prerequisites"></a>Pré-requisitos
- O ponto de distribuição de puxar precisa de acesso à Internet para comunicar com o Microsoft Azure.
- O conteúdo deve ser distribuído para o ponto de distribuição da nuvem de origem.

> [!Note]  
> Esta funcionalidade incorre em encargos para a sua subscrição Azure para armazenamento de dados e saída de rede. Para mais informações, consulte o [Custo da utilização da distribuição baseada na nuvem](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Suporte parcial de descarregamento na cache de pares de clientes para reduzir a utilização de WAN
<!--1357346-->
As fontes de cache dos clientes podem agora dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gestão fornece um rastreio mais detalhado das partes de conteúdo. Tenta eliminar mais do que um download do mesmo conteúdo por grupo de fronteiras. 

### <a name="example-scenario"></a>Cenário de exemplo
Contoso tem um único local primário com dois grupos de fronteira: Sede (Sede) e Filial. Há uma relação de recuo de 30 minutos entre os grupos de fronteira. O ponto de gestão e ponto de distribuição do site estão apenas no limite do QG. A sucursal não tem ponto de distribuição local. Dois dos quatro clientes da sucursal estão configurados como fontes de cache de pares. 

![Diagrama de configuração de rede como descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. Direciona-se para uma implantação com conteúdo para os quatro clientes da sucursal. Só distribuiu o conteúdo para o ponto de distribuição.
2. O Cliente3 e o Cliente4 não têm uma fonte local para a implantação. O ponto de gestão instrui os clientes a esperar 30 minutos antes de voltarem ao grupo de fronteira remoto.
3. O Cliente1 (PCS1) é a primeira fonte de cache de pares a refrescar a política com o ponto de gestão. Como este cliente está habilitado como uma fonte de cache de pares, o ponto de gestão instrui-o a começar imediatamente a descarregar a parte A a partir do ponto de distribuição.  
4. Quando o Cliente2 (PCS2) contacta o ponto de gestão, como parte A já está em andamento, mas ainda não está completo, o ponto de gestão instrui-o a começar imediatamente a descarregar a parte B a partir do ponto de distribuição.
5. PcS1 termina o download da parte A e imediatamente notifica o ponto de gestão. Como parte B já está em andamento, mas ainda não está completo, o ponto de gestão instrui-o a começar a descarregar a parte C a partir do ponto de distribuição.
6. PcS2 termina o download da parte B e imediatamente notifica o ponto de gestão. O ponto de gestão instrui-o a começar a descarregar a parte D a partir do ponto de distribuição. 
7. PcS1 termina o download da parte C e imediatamente notifica o ponto de gestão. O ponto de gestão informa que não há mais peças disponíveis a partir do ponto de distribuição remota. O ponto de gestão instrui-o a descarregar a parte B do seu par local, pcS2.
8. Este processo continua até que ambas as fontes de cache de pares de clientes tenham todas as peças umas das outras. O ponto de gestão prioriza as peças do ponto de distribuição remota antes de instruir as fontes de cache dos pares a descarregar peças de pares locais. 
9. O Cliente3 é o primeiro a atualizar a política após o período de recuo de 30 minutos expirar. Agora, volta a verificar o ponto de gestão, que informa o cliente de novas fontes locais. Em vez de descarregar o conteúdo na íntegra a partir do ponto de distribuição através do WAN, ele descarrega o conteúdo na íntegra a partir de uma das fontes de cache de pares do cliente. Os clientes priorizam fontes de pares locais. 

> [!Note]  
> Se o número de fontes de cache de pares de clientes for maior do que o número de peças de conteúdo, então o ponto de gestão instrui as fontes adicionais de cache de pares a esperar pelo recuo como um cliente normal. 


### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Criar [grupos de fronteira](../servers/deploy/configure/boundary-groups.md) e [fontes](../plan-design/hierarchy/client-peer-cache.md) de cache por normal.
2. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione **Sites**. Clique em **Definições de Hierarquia** na fita. 
3. No separador **Geral,** ative a opção de **configurar as fontes**de cache dos clientes para dividir o conteúdo em partes . 
4. Criar uma implementação necessária com conteúdo.  

   > [!Note]  
   > Esta funcionalidade só funciona quando o cliente descarrega conteúdo em segundo plano, como por exemplo com uma implementação necessária. Os downloads a pedido, como quando o utilizador instala uma implementação disponível no Software Center, comportam-se como de costume.  

1. Para vê-los a lidar com o download de conteúdos em partes, examine o **ContentTransferManager.log** na fonte de cache de pares do cliente e o **MP_Location.log** no ponto de gestão.  
 



## <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131-->
O Software Center apresenta agora a próxima janela de manutenção programada. No separador Estado de Instalação, altere a vista de All para Upcoming. Apresenta o intervalo de tempo e a lista de implementações que estão programadas. A lista está em branco se não houver futuras janelas de manutenção. 

![Centro de Software mostrando a lista de próximas implementações no separador Estado de Instalação](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Separador personalizado para página web no Centro de Software
<!--1358132-->
Agora pode criar um separador personalizado para abrir uma página web no Software Center. Esta funcionalidade permite-lhe mostrar conteúdo aos seus utilizadores finais de forma consistente e fiável. A lista seguinte inclui alguns exemplos:
- Contacte it: informações sobre como contactar o departamento de TI da sua organização
- It Support Center: Ações de self-service de TI, tais como pesquisar uma base de conhecimento ou abrir um bilhete de apoio.
- Documentação do utilizador final: artigos para utilizadores da sua organização sobre vários tópicos de TI, tais como a utilização de aplicações ou a atualização para o Windows 10.


### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Na consola de Gestor de Configuração, espaço de trabalho **de Administração,** nó de Definições de **Cliente,** abra a política **de Definições padrão** do cliente.
2. Selecione o grupo **Software Center.**
3. Para **configurações do Centro de Software,** clique em **Personalizar**.
4. Mude para o separador **Tabs.**
5. Ative a opção de **especificar um separador personalizado para o Centro**de Software .
    1. Introduza um nome no campo de texto **do nome Dom.** Este nome é o que exibe para o utilizador no Software Center.
    2. Introduza um URL válido no campo de texto URL do **Conteúdo.** Este URL é o conteúdo que o Software Center exibe quando os utilizadores clicam neste separador.

> [!Tip]  
> O Software Center utiliza componentes do Internet Explorer para renderizar a página web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Ativar suporte de atualização de software de terceiros em clientes

Agora pode ativar a configuração dos clientes do Gestor de Configuração para atualizações de software de terceiros. Quando **ativar atualizações** de software de terceiros para as propriedades dos componentes SUP, o SUP irá descarregar o certificado de assinatura utilizado pela WSUS para atualizações de terceiros. <!--1357605-->

Selecionar **ativar atualizações** de software de terceiros nas definições do cliente faz o seguinte: 
- No cliente, define a política para "Permitir atualizações assinadas para um local de serviço de atualização intranet microsoft" 
- Instala o certificado de assinatura na loja Trusted Publisher no cliente. 

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. No site mais alto da hierarquia do Gestor de Configuração, vá ao nó **da Administração,** expanda a Configuração do **Site,** depois **sites.**
2. Clique à direita no servidor de topo do site e **selecione Configurar os Componentes do Site** e, em seguida, ponto de **atualização**de software .
3. Clique no separador **Atualizações** de Terceiros e verifique **ativar atualizações**de software de terceiros .
4. Abra **as Definições do Cliente** e vá às definições para **Atualizações**de Software .
5. **Certifique-se de que as atualizações** de software de terceiros estão definidas para **Sim**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Ativar cópia/pasta de detalhes de ativos a partir de visualizações de monitorização
Como resultado do feedback de voz do [utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) Pode agora ativar a funcionalidade de cópia/pasta no painel de dados de dados do ativo nas vistas de monitorização do estado de implementação e distribuição.  <!--1357552-->

## <a name="scap-extensions"></a>Extensões SCAP
A versão pré-lançamento das Extensões SCAP está disponível na pasta Cd.mais recente em SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionforSCAP.msi. Esta versão pré-lançamento das extensões SCAP pode ser instalada em quaisquer versões atualmente suportadas do ramo atual do Gestor de Configuração e LTSB 1606.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
