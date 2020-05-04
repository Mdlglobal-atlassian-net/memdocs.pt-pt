---
title: Introdução à gestão de aplicações
titleSuffix: Configuration Manager
description: Descubra as informações básicas que necessitará para gerir e implementar aplicações no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3cd21fe4b1d53ecbb0bc60818405cb795a4f289
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710763"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introdução à gestão de aplicações no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Neste artigo, você aprenderá o básico antes de começar a trabalhar com aplicações do Gestor de Configuração.  

> [!TIP]  
> Se já está familiarizado com a forma de gerir aplicações no Gestor de Configuração, ignore este artigo. Passe a criar uma aplicação de amostra: [Criar e implementar uma aplicação](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>O que é uma aplicação?

Embora *a aplicação* ou *app* seja um termo amplamente utilizado na computação, no Gestor de Configuração, significa algo específico. Pense numa aplicação como uma caixa. Esta caixa contém um ou mais conjuntos de ficheiros de instalação para um pacote de software (conhecido como um tipo de *implementação),* além de instruções sobre como implementar o software.  

Quando implementa a aplicação para dispositivos, **os requisitos** decidem qual o tipo de implementação que o Gestor de Configuração instala no dispositivo.  

Pode fazer muitas mais coisas com uma aplicação. Vais aprender sobre estas coisas enquanto lês este guia. As seguintes secções introduzem alguns conceitos que precisa de saber antes de começar a cavar mais profundamente:  

### <a name="deployment-type"></a>Tipo de implantação

Se a *aplicação* for a caixa, então o tipo de *implantação* é o conjunto de conteúdos na caixa. Uma aplicação precisa de pelo menos um tipo de implementação, uma vez que determina como instalar a aplicação. Utilize mais de um tipo de implementação para configurar diferentes conteúdos e programa de instalação para a mesma aplicação.

Por exemplo, a sua empresa tem uma aplicação de linha de negócio chamada Astoria. Os desenvolvedores de aplicações fornecem as seguintes formas de instalar a aplicação:

- Pacote de instalação do Windows para funcionalidade completa em dispositivos Windows 10
- Um pacote App-V para uso na fazenda de servidores de terminais
- Uma aplicação web para utilizadores móveis  

Cria uma única aplicação para a Astoria no Gestor de Configuração. A aplicação define os metadados de alto nível sobre a app que é comum em todos os métodos de instalação e plataformas. Em seguida, cria três tipos de implementação para os métodos de instalação disponíveis e implementa a aplicação para todos os utilizadores. Com base nos requisitos e outras configurações nos tipos de implementação, o Gestor de Configuração determina o método certo em cada caso de utilização.

Para mais informações, consulte Criar tipos de [implementação para a aplicação](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Requisitos

Em versões anteriores do 'Gestor de Configuração', criaria uma coleção de dispositivos para implementar uma aplicação para. Embora ainda possa criar uma recolha, utilize requisitos para especificar critérios mais *detalhados* para uma implementação de aplicações.

Por exemplo, especificar que uma aplicação só pode instalar em dispositivos que executam o Windows 10. Quando implementa a aplicação para todos os seus dispositivos, só instala em dispositivos que executam o Windows 10.

O Gestor de Configuração avalia os requisitos para determinar se instala uma aplicação e qualquer um dos seus tipos de implementação. Em seguida, determina o tipo de implementação correto para a instalação da aplicação. De sete em sete dias, por padrão, o cliente do Gestor de Configuração reavalia as regras de requisitos para determinar a conformidade de acordo com a configuração do cliente **Agenda reavaliação para implementações**.

Para mais informações, consulte [Criar e implementar uma aplicação](../get-started/create-and-deploy-an-application.md) e [requisitos do tipo de implementação](../deploy-use/create-applications.md#bkmk_dt-require).

### <a name="global-conditions"></a>Condições globais

Embora utilize requisitos com um tipo de implementação específico numa única aplicação, também pode criar *condições globais.* Estas condições são uma biblioteca de requisitos predefinidos que pode utilizar com qualquer tipo de aplicação e implementação. O Gestor de Configuração inclui um conjunto de condições globais incorporadas, ou pode criar o seu próprio.

Para mais informações, consulte [Criar condições globais.](../deploy-use/create-global-conditions.md)

### <a name="simulated-deployment"></a>Implementação simulada

Uma *implementação simulada* avalia os requisitos, método de deteção e dependências de uma aplicação. Um cliente reporta os resultados sem realmente instalar a aplicação.

Para mais informações, consulte [Simular implementações de aplicações](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Ação de implementação

Uma *ação de implementação* especifica se pretende instalar ou desinstalar a aplicação que está a implementar. Nem todos os tipos de implementação suportam a ação de desinstalação.

Para mais informações, consulte [aplicações de implementação](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Objetivo da implementação

O objetivo de *implementação* especifica se a aplicação de implementação é **necessária** ou **disponível:**  

- O cliente instala automaticamente uma implementação *necessária de* acordo com o horário que definiu. Se a aplicação não estiver oculta, um utilizador pode rastrear o seu estado de implementação. Também podem usar o Software Center para instalar a aplicação antes do prazo.  

- Se implementar a aplicação a um utilizador como *disponível,* vê-a no Centro de Software e pode solicitá-la a pedido.  

Para mais informações, consulte [aplicações de implementação](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Revisões

Quando faz *revisões* a uma aplicação ou a um tipo de implementação, o Gestor de Configuração cria uma nova versão da aplicação. Tome as seguintes ações na consola 'Gestor de Configuração':

- Mostrar o histórico de cada revisão de aplicações
- Veja as suas propriedades
- Restaurar uma versão anterior de uma aplicação
- Apagar uma versão antiga

Para mais informações, consulte [As aplicações De Atualização e de reforma.](../deploy-use/update-and-retire-applications.md)  

### <a name="detection-method"></a>Método de deteção

Utilize métodos de *deteção* para descobrir se um dispositivo já instalou uma aplicação. Se o método de deteção indicar que a aplicação está instalada, o Gestor de Configuração não tenta instalá-la novamente.

Para mais informações, consulte as opções do Método de Deteção do [Tipo de Implementação.](../deploy-use/create-applications.md#bkmk_dt-detect)

### <a name="dependencies"></a>Dependências

*As dependências* definem um ou mais tipos de implementação de outra aplicação que o cliente deve instalar antes de instalar este tipo de implementação.

Para mais informações, consulte [Dependências do tipo de implantação](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Substituição

O Gestor de Configuração permite-lhe atualizar ou substituir as aplicações existentes utilizando uma relação de *supersedência.* Ao substituir uma aplicação, especifica um novo tipo de implementação para substituir o tipo de implementação da aplicação supersed. Também pode decidir se deve atualizar ou desinstalar a aplicação supersed antes de o cliente instalar a aplicação de superseding.

Para mais informações, consulte [a supersedência da Aplicação.](../deploy-use/revise-and-supersede-applications.md#application-supersedence)  

### <a name="user-centric-management"></a>Gestão centrada no utilizador

As aplicações do Gestor de Configuração suportam a *gestão centrada no utilizador,* o que permite associar utilizadores específicos a dispositivos específicos. Em vez de ter de se lembrar do nome do dispositivo de um utilizador, implemente aplicações para o utilizador e para o dispositivo. Esta funcionalidade ajuda-o a certificar-se de que as aplicações mais importantes estão sempre disponíveis em cada um dos dispositivos do utilizador. Se um utilizador adquirir um novo computador, o 'Gestor de Configuração' instala automaticamente as suas aplicações no dispositivo antes de iniciar o seu acesso.

Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .  

### <a name="application-group"></a>Grupo de candidaturas

A partir da versão 1906, criar um conjunto de aplicações que pode enviar para um utilizador ou recolha de dispositivos como uma única implementação. Os metadados que especifica sobre o grupo de aplicações são vistos no Software Center como uma única entidade. Pode encomendar as aplicações no grupo para que o cliente as instale numa encomenda específica.

Para mais informações, consulte [Criar grupos](../deploy-use/create-app-groups.md)de aplicação .

## <a name="what-application-types-can-you-deploy"></a>Que tipos de aplicação pode implementar?

O Gestor de Configuração permite-lhe implementar os seguintes tipos de aplicações:  

- Instalador de Janelas (msi)  

- Pacote de aplicativos para windows e pacotes de aplicativos (appx, appxbundle, msix, msixbundle)  

- Pacote de aplicativos Windows na Microsoft Store  

- Instalador de scripts para instaladores de terceiros e invólucros de script

- Microsoft App-V v4 e v5  

- macOS  

- Uma sequência de tarefas de implementação não-OS para aplicações complexas

Além disso, quando gere os dispositivos através da [gestão de dispositivos](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)do Gestor de Configuração no local, gerencie estes outros tipos de aplicações:  

- Pacote de aplicativo seletiva Windows Phone (xap)  

- Pacote de aplicativo seleções do Windows Phone na Microsoft Store  

- Instalador de Janelas através do MDM (msi)  

- Aplicação Web

## <a name="state-based-applications"></a>Aplicações baseadas no estado  

As aplicações do Gestor de Configuração utilizam monitorização baseada no Estado. Pode rastrear o último estado de implementação de aplicações para utilizadores e dispositivos. As mensagens de estado apresentam informações sobre os dispositivos individuais. Por exemplo, se implementar uma aplicação para uma coleção de utilizadores, pode visualizar o estado de conformidade da implementação e o propósito de implementação na consola Do Gestor de Configuração. Monitorize a implementação de todo o software a partir do espaço de trabalho de **Monitorização** na consola 'Gestor de Configuração'. Para mais informações, consulte [as aplicações do Monitor](../deploy-use/monitor-applications-from-the-console.md).  

O cliente do Gestor de Configuração reavalia regularmente as implementações de aplicações. Por exemplo:  

- Um utilizador desinstala uma aplicação implantada. No próximo ciclo de avaliação, o Gestor de Configuração deteta que a aplicação não está presente. Em seguida, o cliente reinstala automaticamente a aplicação.  

- O Gestor de Configuração não instalou uma aplicação num dispositivo porque não cumpriu os requisitos. Posteriormente, é efetuada uma alteração ao dispositivo, que passa a satisfazer os requisitos. O Gestor de Configuração deteta esta alteração e o cliente instala a aplicação.  

Pode definir o intervalo de reavaliação para implementações de aplicações. Utilize a **reavaliação** do Calendário para a definição de clientes de implementações no grupo **de implementação** de software. Para mais informações, consulte [as definições do cliente](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Introdução à criação de uma aplicação  

Se quiser entrar e criar uma aplicação, encontrará uma passagem no Create e implementará um artigo de [aplicação.](../get-started/create-and-deploy-an-application.md)  

Se estiver familiarizado com o básico e procurando informações de referência mais detalhadas sobre todas as opções disponíveis, comece a [criar aplicações.](../deploy-use/create-applications.md)  

## <a name="software-center"></a>Centro de Software  

O Software Center é uma aplicação do Windows instalada com o cliente do Gestor de Configuração. Utilize-o para as seguintes ações:  

- Procure e solicite aplicações implementadas no dispositivo ou no utilizador
- Instalar e agendar instalações de software
- Ver estado de instalação para aplicações, atualizações de software e sistemas operativos
- Configurar definições de controlo remoto
- Configurar a gestão de energia

Para obter mais informações, veja os artigos seguintes:  

- [Planear e configurar a gestão de aplicações](../plan-design/plan-for-and-configure-application-management.md)
- [Planear o Centro de Software](../plan-design/plan-for-software-center.md)
- [Manual do utilizador do Software Center](../../core/understand/software-center.md)

> [!Note]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Pacotes e programas  

O Gestor de Configuração continua a apoiar pacotes e programas que foram utilizados em versões anteriores do produto.

Para mais informações, consulte [Pacotes e programas.](../deploy-use/packages-and-programs.md)  

## <a name="next-steps"></a>Passos seguintes

Agora que compreende os conceitos básicos de gestão de aplicações no Gestor de Configuração, continue com os seguintes artigos:

- [Criar e implementar uma aplicação de exemplo](../get-started/create-and-deploy-an-application.md)
- [Planear e configurar a gestão de aplicações](../plan-design/plan-for-and-configure-application-management.md)
- [Criar aplicações](../deploy-use/create-applications.md)
