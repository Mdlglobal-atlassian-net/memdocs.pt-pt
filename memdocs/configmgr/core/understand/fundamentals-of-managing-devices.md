---
title: Noções básicas de gestão de dispositivos
titleSuffix: Configuration Manager
description: Aprenda a utilizar o Gestor de Configuração para gerir os dispositivos.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722845"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Fundamentos da gestão de dispositivos com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração pode gerir duas grandes categorias de dispositivos:

- *Os clientes* são dispositivos como estações de trabalho, portáteis, servidores e dispositivos móveis onde instala o software cliente do Gestor de Configuração. Algumas funções de gestão, como o inventário de hardware, requerem este software de cliente.  

- *Os dispositivos geridos* podem incluir *clientes,* mas normalmente é um dispositivo móvel onde o software cliente do Gestor de Configuração não está instalado. Neste tipo de dispositivo, você gere usando a gestão de dispositivos móveis incorporados no Local em Configuração Manager.

Também pode agrupar e identificar dispositivos com base no utilizador, e não apenas no tipo cliente.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager

Existem duas formas de usar o software cliente do Gestor de Configuração para gerir um dispositivo. A primeira forma é descobrir o dispositivo na sua rede e, em seguida, implementar o software do cliente para esse dispositivo. A outra forma é instalar manualmente o software do cliente num novo computador e, em seguida, fazer com que esse computador se junte ao seu site quando este se juntar à sua rede. Para descobrir dispositivos onde o software do cliente não está instalado, execute um ou mais dos métodos de descoberta incorporados. Depois de um dispositivo ser descoberto, utilize um dos vários métodos para instalar o software do cliente. Para obter informações sobre a utilização da descoberta, consulte a descoberta de Executar para O Gestor de [Configuração](../servers/deploy/configure/run-discovery.md).  

Depois de descobrir os dispositivos suportados para executar o software cliente Do Gestor de Configuração, pode utilizar um dos vários métodos para instalar o software. Depois de o software ser instalado e o cliente atribuído a um site primário, pode começar a gerir o dispositivo. Os métodos comuns de instalação incluem:

- Instalação push do cliente

- Instalação baseada em atualização de software

- Política de grupo

- Instalação manual num computador

- Incluindo o cliente como parte de uma imagem de OS que você implementa  

Depois de o cliente ser instalado, é possível simplificar as tarefas de gestão de dispositivos através da utilização de coleções. As coleções são grupos de dispositivos ou utilizadores que cria para que possa geri-las em grupo. Por exemplo, é melhor instalar uma aplicação de dispositivo móvel em todos os dispositivos móveis que o Gestor de Configuração matricula. Se for esse o caso, pode utilizar a coleção All Mobile Devices.  

Para obter mais informações, veja estes artigos:  

- [Escolher uma solução de gestão de dispositivos](../plan-design/choose-a-device-management-solution.md)  

- [Métodos de instalação de cliente](../clients/deploy/plan/client-installation-methods.md)  

- [Introdução às coleções](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Definições do cliente

Quando instala o Gestor de Configuração pela primeira vez, todos os clientes da hierarquia são configurados utilizando as definições padrão do cliente que pode alterar. As definições do cliente incluem estas opções de configuração:

- Com que frequência os dispositivos comunicam com o site.

- Se o cliente está configurado para atualizações de software e outras operações de gestão.

- Se os utilizadores podem inscrever os seus dispositivos móveis para que sejam geridos pelo Gestor de Configuração.  

Pode criar configurações personalizadas do cliente e, em seguida, atribuí-las a coleções. Os membros da coleção estão configurados para ter as configurações personalizadas, e pode criar várias configurações personalizadas do cliente que são aplicadas na ordem que especifica (por ordem numérica). Se houver conflitos, a definição que tiver o menor número de ordem substitui as outras definições.  

O diagrama seguinte mostra um exemplo de como cria e aplica as definições personalizadas do cliente.  

![Definições do cliente](media/ClientSettings.gif)  

Para saber mais sobre as definições do cliente, consulte os seguintes artigos:

- [Como configurar as definições do cliente](../clients/deploy/configure-client-settings.md)
- [Acerca das definições de cliente](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager

O Gestor de Configuração suporta a gestão de alguns dispositivos que não instalaram o software do cliente, e não são geridos pela Intune. Para mais informações, consulte [Gerir dispositivos móveis com infraestrutura no local no Gestor de Configuração](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [gerir dispositivos móveis com Gestor de Configuração e Troca](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestão baseada no utilizador

O Gestor de Configuração suporta coleções de utilizadores de Diretórios Ativos azure e de Serviços de Domínio de Diretório Ativo. Quando utiliza uma coleção de utilizadores, pode instalar software em todos os computadores que os membros da coleção utilizem. Para se certificar de que o software que implementa apenas instala nos dispositivos especificados como o dispositivo principal de um utilizador, configurar a afinidade do dispositivo do utilizador. Um utilizador pode ter um ou mais dispositivos primários.  

Uma das formas de os utilizadores controlarem a sua experiência de implementação de software é utilizar a interface cliente do **Software Center.** O **Software Center** é instalado automaticamente nos computadores dos clientes e é executado a partir do menu Windows **Start.** O **Software Center** permite que os utilizadores gerem o seu próprio software e façam as seguintes tarefas:  

- Instalar software  

- Agendar software para instalar automaticamente fora do horário de trabalho  

- Configure quando o Gestor de Configuração pode instalar software num dispositivo  

- Configure as definições de acesso para controlo remoto, se o controlo remoto for configurado no Gestor de Configuração  

- Configure opções para gestão de energia, se um administrador configurar esta opção  

- Navegue por, instale e solicite software

- Configurar as definições de preferência

- Quando estiver configurado, especifique um dispositivo primário para a finção do dispositivo de utilizador

Para obter mais informações, veja os artigos seguintes:

- [Planear o Centro de Software](../../apps/plan-design/plan-for-software-center.md)
- [Ligar utilizadores e dispositivos com afinidade do dispositivo do utilizador](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Manual do utilizador do Software Center](software-center.md)
