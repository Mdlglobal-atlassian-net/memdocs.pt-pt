---
title: Ligar utilizadores e dispositivos com afinidade do dispositivo do utilizador
titleSuffix: Configuration Manager
description: Ligue os utilizadores e dispositivos com a finção do dispositivo do utilizador e implemente automaticamente aplicações para todos os dispositivos associados a um utilizador.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710098"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Ligue os utilizadores e dispositivos com a finidade do dispositivo do utilizador no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A afinidade do dispositivo de utilizador no Gestor de Configuração associa um utilizador a um ou mais dispositivos. Este comportamento pode eliminar a necessidade de conhecer os nomes dos dispositivos de um utilizador para implementar uma aplicação ao utilizador. Em vez de implementar a aplicação em cada um dos dispositivos do utilizador, implementa a aplicação para o utilizador. Em seguida, a afinidade do dispositivo do utilizador automaticamente garante que a aplicação se instala em todos os dispositivos associados a esse utilizador.  

Defina os dispositivos primários que os utilizadores usam todos os dias para o seu trabalho. Quando cria uma afinidade entre um utilizador e um dispositivo, obtém mais opções de implementação de aplicações. Por exemplo, se um utilizador necessitar do Microsoft Visio, pode instalá-lo no dispositivo principal do utilizador utilizando uma implementação do Instalador do Windows. No entanto, num dispositivo que não seja um dispositivo primário, poderá implementar o Visio como uma aplicação virtual. Também pode utilizar a finção do dispositivo do utilizador para pré-implantar software no dispositivo de um utilizador quando o utilizador não está inscrito. Em seguida, quando o utilizador iniciar o início, a aplicação já está instalada e pronta a ser executada.  

Só gere informações sobre afinidade do dispositivo de utilizador para computadores. O Gestor de Configuração gere automaticamente as afinidades dos dispositivos de utilizador para os dispositivos móveis que matricula.  

## <a name="manually-set-up-user-device-affinity"></a>Configurar manualmente a afinidade do dispositivo do utilizador  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Dispositivos.**  

1. Selecione um dispositivo. No separador **Home** na fita, no grupo **Dispositivo,** escolha **Editar Utilizadores Primários**.  

1. Na caixa de diálogo **Editar Utilizadores Primários,** procure e, em seguida, selecione os utilizadores para adicionar como utilizadores primários para o dispositivo selecionado. Escolha **Adicionar**.  

    > [!NOTE]  
    > A lista **de Utilizadores Primários** mostra os utilizadores que já são utilizadores primários deste dispositivo e o método pelo qual cada relação utilizador-dispositivo foi atribuída.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurar dispositivos primários para um utilizador  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó dos **Utilizadores.**  

1. Selecione um utilizador. No separador **Dispositivo** na fita, escolha **Dispositivos Primários de Edição**.  

1. Na caixa de diálogo **de dispositivos primários editar,** procure e, em seguida, selecione os dispositivos para adicionar como dispositivos primários para o utilizador selecionado. Escolha **Adicionar**.  

    > [!NOTE]  
    > A lista de **Dispositivos Primários** mostra dispositivos que já estão configurados como dispositivos primários para este utilizador, e o método pelo qual cada relação utilizador-dispositivo foi atribuída.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Criar automaticamente afinidades de dispositivo do utilizador (apenas PCs Windows)

O Gestor de Configuração lê dados sobre os eventos de logon do utilizador a partir do registo de eventos do Windows. Para criar automaticamente afinidades de dispositivos de utilizador, ligue estas duas opções na política de segurança local nos computadores clientes para armazenar eventos de logon no registo de eventos do Windows:  

- **Auditar eventos de início de sessão de conta**  
- **Auditar eventos de início de sessão**  

Para configurar estas definições, utilize a Política do Grupo Windows.  

> [!IMPORTANT]  
> Se um erro fizer com que o registo de eventos do Windows gere um elevado número de entradas, poderá criar um novo registo de eventos. Se este comportamento ocorrer, os eventos de logon existentes podem não estar disponíveis para O Gestor de Configuração.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurar o site para criar automaticamente afinidades de dispositivos de utilizador  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Definições do **Cliente.**  

1. Para modificar as definições padrão do cliente, selecione **Definições de Cliente Padrão**. No separador **Casa** na fita, no grupo **Propriedades,** escolha **Propriedades**.

    Para criar configurações personalizadas do agente cliente, no separador **Home** na fita, no grupo **Criar,** escolha **Criar Definições personalizadas**de Dispositivo cliente .

    > [!NOTE]  
    > Se modificar as definições padrão do cliente, o site implementa-as em todos os computadores da hierarquia. Para mais informações, consulte [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md).  

1. No grupo **User and Device Affinity,** detete as seguintes definições:  

    - Limiar de **afinidade do dispositivo do utilizador (minutos)**: Desloque o número de minutos de utilização do dispositivo antes de o site criar uma afinidade do dispositivo do utilizador.  

    - Limiar de **afinidade do dispositivo do utilizador (dias)**: Desdefinido o número de dias sobre os quais o site mede o limiar de afinidade baseado na utilização.  

    - **Configure automaticamente a afinidade do dispositivo do utilizador**a partir de dados de utilização : Selecione **True** para permitir que o site crie automaticamente afinidades do dispositivo do utilizador. Se selecionar **Falso,** tem de aprovar manualmente todas as atribuições de afinidade do dispositivo do utilizador.  

    > [!TIP]  
    > Por exemplo, se definir o limiar de **afinidade do dispositivo utilizador (minutos)** para **60** minutos e definir o limiar de **afinidade do dispositivo utilizador (dias)** a **5** dias, o utilizador deve utilizar o dispositivo durante pelo menos 60 minutos durante um período de 5 dias para criar automaticamente uma afinidade do dispositivo de utilizador.  

Após o Configurar Manager criar uma afinidade automática do dispositivo de utilizador, continua a monitorizar os limiares de afinidade do dispositivo do utilizador. Se a atividade do utilizador para o dispositivo ficar abaixo dos limiares definidos, o site remove a afinidade do dispositivo do utilizador. Definir o limiar de **afinidade do dispositivo utilizador (dias)** para um valor de, pelo menos, sete dias. Esta configuração evita situações em que uma afinidade de dispositivo de utilizador configurada automaticamente pode perder-se enquanto o utilizador não é inscrito, por exemplo, durante o fim de semana.  


## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades de dispositivo do utilizador a partir de um ficheiro

Para criar muitas relações de uma só vez, importe um ficheiro que tenha os detalhes para várias afinidades de dispositivos de utilizador. Certifique-se de que os dispositivos-alvo já foram descobertos pelo site e existem como recursos na base de dados do Gestor de Configuração.  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e selecione o nó de **Utilizadores** ou **Dispositivos.**  

1. No separador **Home** na fita, no grupo **Criar,** escolha **a afinidade**do dispositivo de utilizador importado .  

1. No Assistente de Afinidade do Utilizador importado, na página **Choose Mapping,** delineie esta informação:  

    - **Nome do ficheiro**. Especifique um ficheiro de valores separados de vírem (CSV) que tenha uma lista de utilizadores e dispositivos entre os quais pretende criar uma afinidade. Neste ficheiro, cada par de utilizador e dispositivo deve estar na sua própria linha, com valores separados por uma vírem. Utilize este formato:`<domain>\<username>,<device NetBIOS name>`  

    - **Este ficheiro tem títulos**de coluna para fins de referência . Se o ficheiro .csv tiver um cabeçalho de primeira linha, selecione esta opção. O site ignora a linha do cabeçalho durante a importação.  

1. Se o ficheiro que importa tiver mais de dois itens em cada linha, utilize a **Coluna** e **o Signo** para especificar quais as colunas que representam utilizadores e dispositivos e quais as colunas a ignorar durante a importação.  

1. Conclua o assistente.  


## <a name="let-users-create-their-own-device-affinities"></a>Deixe que os utilizadores criem as suas próprias afinidades de dispositivos

Crie um utilizador para criar a finidade do seu próprio dispositivo de utilizador no Software Center.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar o site para permitir pedidos de afinidade de dispositivos de utilizador criados pelo utilizador  

1 Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Definições do **Cliente.**  

1. Para modificar as definições padrão do cliente, selecione **Definições de Cliente Padrão**. No separador **Casa** na fita, no grupo **Propriedades,** escolha **Propriedades**.

    Para criar configurações personalizadas do agente cliente, no separador **Casa** na fita, no grupo **Criar,** escolha **Criar Definições personalizadas de utilizador do cliente**.

    > [!NOTE]  
    > Se modificar as definições padrão do cliente, o site implementa-as em todos os computadores da hierarquia. Para mais informações, consulte as definições do [cliente Configurar](../../core/clients/deploy/configure-client-settings.md).  

1. No grupo **User and Device Affinity,** ative a definição para permitir que o **utilizador defina os seus dispositivos primários**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Configurar uma afinidade de dispositivo de utilizador no Centro de Software

A partir da versão 1902, use o Software Center para definir a finidade.

1. No Software Center, vá ao separador **Opções.**

1. Na secção de informação do **Trabalho,** selecione a opção **que uso regularmente neste computador para fazer o meu trabalho**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Configurar uma afinidade do dispositivo de utilizador no catálogo de aplicações

> [!Important]
> A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910.  
>
> Para obter mais informações, veja os artigos seguintes:
>
> - [Configure Software Center](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funcionalidades removidas e preteridas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. No catálogo de aplicações, escolha **My Systems**.  

1. Selecione a opção **que uso regularmente neste computador para fazer o meu trabalho.**  


## <a name="manage-user-device-affinity-requests-from-users"></a>Gerir pedidos de afinidade de dispositivo do utilizador a partir de utilizadores

Quando desativa a definição do cliente para configurar automaticamente a **afinidade do dispositivo do utilizador**a partir de dados de utilização, é necessário aprovar manualmente todas as atribuições de afinidade do dispositivo do utilizador.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprovar ou rejeitar um pedido de afinidade do dispositivo de utilizador  

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.**  

1. Selecione a recolha de utilizadores ou dispositivos para os quais pretende gerir pedidos de afinidade.  

1. No separador **Home** na fita, no grupo **Coleção,** escolha **Pedidos de Afinidade Gerir**.  

1. Na caixa de diálogo **'Gerir dispositivo utilizador',** selecione um pedido de afinidade e, em seguida, escolha **Aprovar** ou **Rejeitar**.  


## <a name="next-steps"></a>Passos seguintes

Também pode utilizar o Microsoft Intune para encontrar a utilização primária de um dispositivo matriculado. Para mais informações, consulte O utilizador principal de um dispositivo Intune na documentação [Intune.](https://docs.microsoft.com/intune/find-primary-user)
