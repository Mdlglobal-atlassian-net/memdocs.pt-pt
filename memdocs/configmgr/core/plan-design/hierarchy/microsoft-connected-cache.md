---
title: Cache Ligada da Microsoft
titleSuffix: Configuration Manager
description: Utilize o seu ponto de distribuição do Gestor de Configuração como um servidor de cache local para otimização de entrega
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dead573e1744a5c8b84ff954e85be43af644486
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878500"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Cache conectado da Microsoft no gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3555764-->

A partir da versão 1906, pode instalar um servidor Microsoft Connected Cache nos seus pontos de distribuição. Ao gravar este conteúdo no local, os seus clientes podem beneficiar da funcionalidade de Otimização de Entrega, mas pode ajudar a proteger os links WAN.

> [!NOTE]
> A partir da versão 1910, esta funcionalidade chama-se **Microsoft Connected Cache**. Anteriormente era conhecido como Delivery Optimization In-Network Cache.

Este servidor de cache funciona como uma cache transparente a pedido para conteúdos descarregados pela Otimização da Entrega. Utilize as definições do cliente para se certificar de que este servidor é oferecido apenas aos membros do grupo de limites do Gestor de Configuração local.

Esta cache é separada do conteúdo do ponto de distribuição do Gestor de Configuração. Se escolher a mesma unidade que a função do ponto de distribuição, armazena conteúdo separadamente.

> [!Note]  
> O servidor 'Cache' conectado é uma aplicação instalada no Windows Server. Esta aplicação ainda está em desenvolvimento.

## <a name="how-it-works"></a>Como funciona

Quando configura os clientes para utilizar o servidor Connected Cache, já não solicitam conteúdo gerido pela Microsoft na internet. Os clientes solicitam este conteúdo a partir do servidor cache instalado no ponto de distribuição. O servidor no local caches este conteúdo usando a função IIS para o Pedido de Pedido de Pedido de Pedido de Pedido de Pedido de Pedido de Solicitação (ARR). Em seguida, o servidor cache pode responder rapidamente a quaisquer pedidos futuros para o mesmo conteúdo. Se o servidor 'Cache Connected' estiver indisponível ou o conteúdo ainda não estiver em cache, os clientes descarregam o conteúdo a partir da internet. Os clientes também usam a Otimização de Entrega, por isso descarrega partes do conteúdo dos pares na sua rede.

![Diagrama de como a cache conectada funciona](media/3555764-microsoft-connected-cache.png)

1. O cliente verifica as atualizações e obtém o endereço da rede de entrega de conteúdos (CDN).

2. O Gestor de Configuração configura as definições de Otimização de Entrega (DO) no cliente, incluindo o nome do servidor cache.

3. Cliente A solicita conteúdo do servidor de cache DO.

4. Se a cache não incluir o conteúdo, então o servidor de cache DO obtém-o do CDN.

5. Se o servidor cache não responder, o cliente descarrega o conteúdo a partir do CDN.

6. Os clientes usam DO para obter peças do conteúdo dos pares.

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações

- Um ponto de distribuição *no local,* com as seguintes configurações:

  - Executar o Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 ou Windows Server 2019

  - O web site predefinido ativado na porta 80

  - Não pré-instale a função De [Encaminhamento](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) de Pedido de Pedido de Pedido de Aplicação IIS (ARR). O Cache Conectado instala ARR e configura as suas definições. A Microsoft não pode garantir que a configuração ARR do Connected Cache não entrará em conflito com outras aplicações no servidor que também utilizam esta funcionalidade.

  - O ponto de distribuição requer acesso à Internet à nuvem da Microsoft. Os URLs específicos podem variar dependendo do conteúdo específico ativado pela nuvem. Para mais informações, consulte os requisitos de [acesso à Internet.](../network/internet-endpoints.md)

  - A partir da versão 2002, a aplicação Connected Cache pode utilizar um servidor proxy não autenticado para acesso à Internet. Para mais informações, consulte [Configure o proxy para um servidor](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)de sistema de site .<!-- 5856396 -->

- Clientes com execução da versão 1709 do Windows 10 ou mais tarde

## <a name="enable-connected-cache"></a>Ativar a cache conectada

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.**

1. Selecione um ponto de distribuição *no local* e, em seguida, na fita selecione **Propriedades**.

1. Nas propriedades da função ponto de distribuição, no separador **Geral,** configure as seguintes definições:  

    1. Ativar a opção de ativar este ponto de **distribuição para ser usado como servidor Cache ligado ao Microsoft**  

        Ver e aceitar os termos da licença.

    2. **Unidade local a utilizar**: Selecione o disco para utilizar para a cache. **Automático** é o valor padrão, que utiliza o disco com o espaço mais livre. <sup> [Nota 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Pode mudar esta unidade mais tarde. Qualquer conteúdo em cache perde-se, a menos que o copie para a nova unidade.

    3. **Espaço**do disco : Selecione a quantidade de espaço em disco para reservar em GB ou uma percentagem do espaço total do disco. Por padrão, este valor é de 100 GB.

        > [!Note]  
        > O tamanho da cache padrão deve ser suficiente para a maioria dos clientes. Pode ajustar o tamanho da cache mais tarde.
        >
        > Se o tamanho da cache no disco exceder o espaço atribuído, a ARR limpa o espaço removendo conteúdo com base na sua heurística incorporada.<!-- SCCMDocs#2045 -->

    4. **Reter a cache ao desativar o servidor 'Cache' Conectado**: Se remover o servidor de cache e ativar esta opção, o servidor mantém o conteúdo da cache no disco.  

1. Nas definições do cliente, no grupo **de Otimização** de Entregas, configure a definição para **ativar os dispositivos geridos pelo Gestor de Configuração para utilizar servidores De Cache ligados ao Microsoft para download**de conteúdos .  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a>Nota 1: Sobre a seleção de unidades

Se selecionar **Automático**, quando o Gestor de Configuração instala o componente 'Cache Connected', ele honra o ficheiro **no_sms_on_drive.sms.** Por exemplo, o ponto de distribuição tem o ficheiro `C:\no_sms_on_drive.sms` . Mesmo que o C: unidade tenha o espaço mais livre, o Gestor de Configuração configura a Connected Cache para utilizar outra unidade para a sua cache.

Se selecionar uma unidade específica que já tenha o ficheiro **no_sms_on_drive.sms,** o Gestor de Configuração ignora o ficheiro. Configurar a Cache Conectada para utilizar essa unidade é uma intenção explícita. Por exemplo, o ponto de distribuição tem o ficheiro `F:\no_sms_on_drive.sms` . Quando configura explicitamente as propriedades do ponto de distribuição para utilizar o **F:** unidade, Configuração Gestor de Configuração configura Cache Conectada para utilizar o F: unidade para a sua cache.

Para alterar a unidade depois de instalar a Cache Conectada:

- Configure manualmente as propriedades do ponto de distribuição para utilizar uma letra de unidade específica.

- Se for definido como automático, crie primeiro o ficheiro **no_sms_on_drive.sms.** Em seguida, faça algumaalteração nas propriedades do ponto de distribuição para desencadear uma mudança de configuração.

### <a name="automation"></a>Automatização

<!-- SCCMDocs#1911 -->

Pode utilizar o Gestor de Configuração SDK para automatizar a configuração das definições de Cache conectadas pelo Microsoft num ponto de distribuição. Como é o caso de todas as funções do site, utilize a [classe SMS_SCI_SysResUse WMI](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md). Para mais informações, consulte [programação das funções do site.](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles)

Quando atualizar o **SMS_SCI_SysResUse** instância para o ponto de distribuição, detete as seguintes propriedades:

- **AcordoDOINCLicença**: Desemlicença `1` para aceitar os termos da licença.
- **Bandeiras**: `|= 4` Ativar, desativar`&= ~4`
- **DiskSpaceDOINC**: Definido para `Percentage` ou`GB`
- **RetençãoDOINCCache**: Definido para `0` ou`1`
- **LocalDriveDOINC**: Definir `Automatic` para, ou uma carta de unidade específica, como `C:` ou`D:`

## <a name="verify"></a>Verificar

Quando os clientes descarregam conteúdo gerido pela nuvem, utilizam a Otimização de Entrega a partir do servidor de cache instalado no seu ponto de distribuição. O conteúdo gerido pela nuvem inclui os seguintes tipos:

- Aplicações da Loja Microsoft
- Funcionalidades do Windows a pedido, como idiomas
- Se ativar o [Windows Update para as políticas empresariais](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md): funcionalidade do Windows 10 e atualizações de qualidade
- Para [trabalhos de cogestão:](../../../comanage/workloads.md)
  - Atualização do Windows para Negócios: funcionalidades do Windows 10 e atualizações de qualidade
  - Aplicações click-to-run do Office: Aplicações e atualizações do Office
  - Aplicativos para clientes: aplicações e atualizações da Microsoft Store
  - Proteção do Ponto Final: atualizações de definição do Windows Defender

Na versão 1809 do Windows 10, verifique este comportamento com o **CmDLet Get-DeliveryOptimizationStatus** Windows PowerShell. Na saída cmdlet, reveja o valor **BytesFromCacheServer.** Para mais informações, consulte [a Otimização da Entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)do Monitor .

Se o servidor cache devolver qualquer falha HTTP, o cliente de Otimização de Entrega recai para a fonte original da nuvem.

Para obter informações mais detalhadas, consulte [Troubleshoot Microsoft Connected Cache no Gestor de Configuração](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a>Suporte para aplicações Intune Win32

<!--5032900-->

A partir da versão 1910, quando activao Cache Conectado nos pontos de distribuição do Gestor de Configuração, podem servir aplicações Microsoft Intune Win32 a clientes cogeridos.

### <a name="prerequisites"></a>Pré-requisitos

#### <a name="client"></a>Cliente

- Atualize o cliente para a versão mais recente.

- O dispositivo cliente precisa de ter pelo menos 4 GB de memória.

    > [!TIP]
    > Utilize a seguinte definição de política de grupo: Configuração de computador > modelos administrativos > Componentes do Windows > Otimização de Entrega > capacidade mínima de **RAM (inclusiva) necessária para permitir a utilização de Peer Caching (em GB)**.

#### <a name="site"></a>Site

- Ativar a Cache Conectada num ponto de distribuição. Para mais informações, consulte [o Microsoft Connected Cache](microsoft-connected-cache.md).

- O cliente e o ponto de distribuição ativado por Cache conectado saem do mesmo grupo de fronteiras.

- Ativar as seguintes definições de cliente no grupo [**de Otimização**](../../clients/deploy/about-client-settings.md#delivery-optimization) de Entrega:

  - **Utilize grupos de limites do Gestor de Configuração para id do Grupo de Otimização de Entrega**
  - **Ativar os dispositivos geridos pela Configuração Manger para utilizar servidores Microsoft Connected Cache para download de conteúdos**

- Ativar a funcionalidade de pré-lançamento **Aplicações cliente para dispositivos cogeridos**. Para mais informações, consulte [as funcionalidades de pré-lançamento](../../servers/manage/pre-release-features.md).

- Ative a cogestão e mude a carga de trabalho das **aplicações do Cliente** para **Pilot Intune** ou **Intune**. Para obter mais informações, veja os seguintes artigos:

  - [Cargas de trabalho - Aplicativos de clientes](../../../comanage/workloads.md#client-apps)
  - [Como permitir a cogestão](../../../comanage/how-to-enable.md)
  - [Trocar as cargas de trabalho para o Intune](../../../comanage/how-to-switch-workloads.md)

    Se em piloto, adicione o cliente à coleção piloto para Aplicações de Clientes.

#### <a name="intune"></a>Intune

- Esta funcionalidade apenas suporta o tipo de aplicação Intune Win32.

  - Criar e atribuir (implementar) uma nova aplicação em Intune para o efeito. (As aplicações criadas antes da versão Intune 1811 não funcionam.) Para mais informações, consulte a gestão de [aplicações Intune Win32.](https://docs.microsoft.com/intune/apps/apps-win32-app-management)

  - A aplicação precisa de ter pelo menos 100 MB de tamanho.
  
    > [!TIP]
    > Utilize a seguinte definição de política de grupo: Configuração de computador > modelos administrativos > Componentes do Windows > Otimização de entrega > tamanho mínimo de ficheiro de conteúdo de cache de **pares (em MB)**.

## <a name="see-also"></a>Consulte também

[Otimizar as atualizações do Windows 10 com otimização de entrega](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Problemas de resolução de cache conectados da Microsoft no gestor de configuração](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
