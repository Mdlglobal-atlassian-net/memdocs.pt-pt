---
title: Configure Wake na LAN
titleSuffix: Configuration Manager
description: Selecione as definições de Wake On LAN no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 512d942d79d11178f010c4f0adb41a25ee432743
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713507"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Como configurar Wake on LAN no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Especifique as definições de Wake nas definições LAN para Configuração De Gerente quando pretender tirar computadores de um estado de sono.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a>Acorde na LAN a partir da versão 1810
<!--3607710-->
Começando no Diretor de Configuração 1810, há uma nova forma de acordar máquinas de dormir. Pode acordar os clientes a partir da consola Do Gestor de Configuração, mesmo que o cliente não esteja na mesma sub-rede que o servidor do site. Se precisar de fazer dispositivos de manutenção ou consulta, não se limita a clientes remotos que estão a dormir. O servidor do site utiliza o canal de notificação do cliente para identificar outros clientes que estão acordados na mesma subnet remota, e depois utiliza esses clientes para enviar um aviso sobre o pedido da LAN (pacote mágico). A utilização do canal de notificação do cliente ajuda a evitar retalhos MAC, o que pode fazer com que a porta seja desligada pelo router. A nova versão de Wake on LAN pode ser ativada ao mesmo tempo que a [versão mais antiga](#bkmk_wol-previous).

### <a name="limitations"></a>Limitações

- Pelo menos um cliente na sub-rede alvo deve estar acordado.
- Esta funcionalidade não suporta as seguintes tecnologias de rede:
   - IPv6
   - 802.1x autenticação da rede
    >[!NOTE]
    > A autenticação da rede 802.1x pode funcionar com configuração adicional dependendo do hardware e da sua configuração.
- As máquinas só acordam quando as notificam através da notificação do cliente **Wake Up.**
    - Para despertar quando ocorre um prazo, a versão mais antiga de Wake on LAN é usada.
    -  Se a versão mais antiga não estiver ativada, o despertar do cliente não ocorrerá para implementações criadas com as definições **Use Wake-on-LAN para acordar os clientes para implementações necessárias** ou **enviar pacotes de despertar**.  

> [!IMPORTANT]
> Recomenda-se a utilização da função Wake On LAN numa quantidade limitada de dispositivos (100) de cada vez.
>
> Quando utiliza a funcionalidade Wake On LAN para acordar máquinas da consola de administração do Diretor de Configuração, os pedidos de despertar são colocados numa fila interna que é partilhada por outras funcionalidades de ação em tempo real. Exemplos dessas outras funcionalidades são Executar Scripts, CMPivot e outras notificações de clientes de canal rápido. Dependendo do desempenho dos sistemas do seu site, as ações de despertar podem demorar muito tempo e atrasar a outra ação em tempo real. Sugere-se que não acorde mais de 100 máquinas de uma só vez. Para saber se está a receber um atraso nesta área que pode causar atrasos, pode consultar o diretório de ...\inboxes\objmgr.box para ver se há um grande número de ficheiros com . Extensão OPA.


### <a name="security-role-permissions"></a>Permissões de papel de segurança

- **Notificar recurso** na categoria Coleção

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Configure os clientes para usar Wake on LAN a partir da versão 1810

Anteriormente, teve de ativar manualmente o cliente para acordar na LAN nas propriedades do adaptador de rede. O Gestor de Configuração 1810 inclui uma nova definição de cliente chamada **Permitir despertar da rede**. Configure e implemente esta definição em vez de modificar as propriedades do adaptador de rede.

1. Sob **Administração,** vá para **as Definições do Cliente.**
1. Selecione as definições do cliente que pretende editar ou crie novas definições personalizadas do cliente para implementar. Para mais informações, consulte [Como configurar as definições do cliente](configure-client-settings.md).
1. De acordo com as definições do cliente **de Gestão de Energia,** selecione **Enable** para a configuração de despertar da **rede Permitir.** Para mais informações sobre esta definição, consulte [as definições do cliente](about-client-settings.md#power-management).

4. A partir do Diretor de Configuração 1902, a nova versão de Wake on LAN homenageia a porta UDP personalizada que especifica para a [definição](about-client-settings.md#power-management)do número de cliente Wake **On LAN (UDP).** Este cenário é partilhado tanto pela nova e mais antiga versão de Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Acorde um cliente usando a notificação do cliente a partir de 1810
 
Você pode acordar um único cliente ou qualquer cliente adormecido em uma coleção. Para dispositivos que já estão acordados na coleção, não são tomadas medidas para eles. Apenas os clientes que estão a dormir serão enviados um Wake a pedido da LAN. Para mais informações sobre como notificar um cliente para acordar, consulte a [notificação do Cliente.](../manage/client-notification.md)

- **Para acordar um único cliente:** Clique no cliente, vá à **Notificação**do Cliente e, em seguida, selecione **Acordar**.

   ![Awakee a notificação do cliente na consola](media/wol-wake-up-client-notification.png)

- **Para acordar todos os clientes adormecidos numa coleção:** Clique à direita na recolha do dispositivo, vá à **Notificação**do Cliente e, em seguida, selecione **Acordar**.
   - Esta ação não pode ser executada em coleções embutidas.
   - Quando você tem uma mistura de clientes adormecidos e acordados em uma coleção, apenas os clientes que estão a dormir são enviados um Wake a pedido da LAN.
   - A partir de 2002, a partir de uma consola ligada a um site da Administração Central, a um site autónomo ou ao site principal infantil.
   - Nas versões 1910 e anteriores, esta ação só está ativa quando a consola Do Gestor de Configuração está ligada a um site autónomo ou primário infantil. Quando ligado a um Sítio da Administração Central, a ação não está disponível.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>O que esperar quando apenas a nova versão de Wake on LAN está ativada

Quando tem apenas a nova versão do Wake on LAN ativada, apenas a notificação do cliente **Wake Up** está ativada. Os clientes não são enviados uma notificação quando um prazo é recebido em implementações como sequências de tarefas, distribuição de software ou instalação de atualizações de software. Uma vez que uma máquina de dormir esteja novamente on-line, ela será refletida na consola quando ele verificar com o Ponto de Gestão.

A partir da versão 1902 do Gestor de Configuração, pode especificar a porta Wake na lan. Este cenário é partilhado tanto pela nova e mais antiga versão de Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>O que esperar quando ambas as versões de Wake on LAN estiverem ativadas

Quando tiver ambas as versões de Wake on LAN ativadas, pode utilizar a notificação do cliente **Wake Up** e acordar no prazo. A notificação do cliente funciona de forma um pouco diferente da tradicional Wake on LAN. Para uma breve explicação de como funciona a notificação do cliente, consulte o Wake on LAN a partir da versão [1810.](#bkmk_wol-1810) A nova definição de cliente **Permitir á despertar** da rede irá alterar as propriedades NIC para permitir o Wake on LAN. Já não é necessário troque-o manualmente para novas máquinas que são adicionadas ao seu ambiente. Todas as outras funcionalidades de Wake on LAN não foram alteradas.

A partir da versão 1902, a notificação do cliente **Wake Up** honra a definição existente de número de **porta Wake On LAN (UDP).**


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a>Acorde na LAN para a versão 1806 e mais cedo

Especifique as definições de Wake on LAN para O Gestor de Configuração quando pretender tirar computadores de um estado de sono para instalar software necessário, tais como atualizações de software, aplicações, sequências de tarefas e programas.

Pode complementar o Wake on LAN utilizando as definições de cliente de procuração de despertar. No entanto, para utilizar o proxy de despertar, primeiro deve ativar o Wake on LAN para o site e especificar **utilize apenas pacotes de despertar** e a opção **Unicast** para o método de transmissão Wake on LAN. Esta solução de despertar também suporta ligações ad-hoc, como uma ligação remota de ambiente de trabalho.

Utilize o primeiro procedimento para configurar um local primário para acordar na LAN. Em seguida, utilize o segundo procedimento para configurar as definições do cliente proxy de despertar. Este segundo procedimento configura as definições padrão do cliente para as definições de procuração de despertar para aplicar a todos os computadores da hierarquia. Se pretender que estas definições se apliquem apenas a computadores selecionados, crie uma definição personalizada do dispositivo e atribua-a a uma coleção que contenha os computadores que pretende configurar para procuração de despertar. Para obter mais informações sobre como criar configurações personalizadas do cliente, consulte [como configurar as definições do cliente](../../../core/clients/deploy/configure-client-settings.md).

Um computador que receba as definições do cliente proxy wake-up provavelmente interromperá a sua ligação de rede durante 1-3 segundos. Isto ocorre porque o cliente deve redefinir o cartão de interface de rede para ativar o controlador proxy de despertar nele.

> [!WARNING]
> Para evitar perturbações inesperadas nos seus serviços de rede, avalie primeiro o proxy de despertar numa infraestrutura de rede isolada e representativa. Em seguida, utilize as definições personalizadas do cliente para expandir o seu teste para um grupo selecionado de computadores em várias subredes. Para obter mais informações sobre como funciona o wake-up proxy, consulte [Plan como acordar os clientes](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Para configurar Wake on LAN para um site para a versão 1806 e anterior

 Para utilizar o Wake on LAN, é necessário capacitá-lo para cada site numa hierarquia.

1. Na consola do Gestor de Configuração, vá à **Administração > Site de Configuração do Site**> Sites .
2. Clique no site principal para configurar e, em seguida, clique em **Propriedades**.
3. Clique **no** separador Wake no LAN e configure as opções que necessita para este site. Para apoiar o proxy de despertar, certifique-se de que seleciona **utilize apenas pacotes de despertar** e **Unicast**. Para mais informações, consulte [Plan como acordar os clientes.](../../../core/clients/deploy/plan/plan-wake-up-clients.md)
4. Clique em **OK** e repita o procedimento para todos os locais primários da hierarquia.

![Ativar Wake On LAN nas propriedades do site](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Para configurar as definições do cliente proxy wake-up

1. Na consola de Gestor de Configuração, vá à **Administração > Definições**de Cliente.
2. Clique em **Definições de Cliente Predefinidos**e, em seguida, clique em **Propriedades**.
3. Selecione **Power Management** e, em seguida, escolha **Sim** para ativar proxy **de despertar**.
4. Reveja e, se necessário, configure as outras definições de procuração de despertar. Para obter mais informações sobre estas definições, consulte as definições de [gestão de energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Clique **em OK** para fechar a caixa de diálogo e, em seguida, clique em **OK** para fechar a caixa de diálogo Predefinido do cliente.

Pode utilizar os seguintes relatórios Wake On LAN para monitorizar a instalação e configuração do procura-bordo:

- Resumo do estado de implementação do proxy de reativação
- Detalhes do estado de implementação do proxy de reativação

> [!TIP]
> Para testar se o representante de despertar está a funcionar, teste uma ligação a um computador adormecido. Por exemplo, ligue-se a uma pasta partilhada nesse computador ou tente ligar-se ao computador utilizando o Remote Desktop. Se utilizar o Acesso Direto, verifique se os prefixos do IPv6 funcionam testando os mesmos testes para um computador adormecido que está atualmente na Internet.
