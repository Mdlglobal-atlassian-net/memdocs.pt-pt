---
title: Notificações de reinício de dispositivo
titleSuffix: Configuration Manager
description: Reiniciar o comportamento de notificação para várias configurações do cliente no Gestor de Configuração.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713395"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Notificações de reinício do dispositivo no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As notificações que um utilizador recebe para um reinício do dispositivo pendente podem variar dependendo das [definições](about-client-settings.md#computer-restart) do cliente de reiniciar o Computador e qual a versão do Gestor de Configuração que está a ser utilizada. Este artigo ajuda os administradores a determinar qual é a experiência do utilizador para as notificações de reinício do dispositivo pendentes.

>[!NOTE]
> - Este artigo centra-se nas definições do cliente encontradas na versão 1902 do Gestor de Configuração e na versão 1906.


## <a name="deployment-types-for-restart-notifications"></a>Tipos de implementação para notificações de reinício

As definições do [cliente de reinício](about-client-settings.md#computer-restart) do Computador alteram a experiência do utilizador para todas as implementações necessárias que exijam o reinício dos seguintes tipos:

- [Aplicação](../../../apps/deploy-use/deploy-applications.md)
- [Sequência de tarefas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Atualização de software](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Reinício dos tipos de notificação

Quando é necessário reiniciar, o utilizador final recebe a notificação do reinício. Existem quatro notificações gerais que os utilizadores podem receber:

É necessária uma **notificação** de torrada informando-o de um recomeço. A informação na notificação de torradas pode ser diferente dependendo da versão do Gestor de Configuração que você está executando. Este tipo de notificação é nativo do Sistema operativo Windows e também pode ver software de terceiros usando este tipo de notificação.

![Notificação de torradas de reinício pendente](media/3555947-restart-toast.png)

Notificação do Software Center com uma opção de soneca mostrando o tempo restante antes de ser aplicado um reinício. A mensagem pode ser diferente dependendo da sua versão de 'Gestor de Configuração'.

![Notificação pendente do Centro de Software com botão de soneca](media/3976435-snooze-restart-countdown.png)

Notificação final do Software Center que não pode ser fechada pelo utilizador. O botão de soneca está acinzentado.

![Notificação final do Centro de Software](media/3976435-final-restart-countdown.png)

Se o utilizador instalar proativamente o software necessário que necessite de ser reiniciado antes do prazo, verá uma notificação diferente. A seguinte notificação ocorre quando tanto a definição da experiência do utilizador permite notificações e não utiliza notificações de torradas para a implementação. Para obter mais informações sobre a configuração destas definições, consulte as definições de [Experiência do **Utilizador** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) de Implementação e [as notificações do Utilizador para obter as implementações necessárias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Notificação para software instalado proactivamente](media/3976435-proactive-user-restart-notification.png)

- Quando não utiliza notificações de torradas, o diálogo para software marcado como **Disponível** é semelhante ao software instalado proactivamente.

  - Para o software **disponível,** a notificação não tem um prazo para o reinício e o utilizador pode escolher o seu próprio intervalo de soneca. Para mais informações, consulte [as definições](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)de aprovação .

    ![O software marcado como "Disponível" não tem um prazo para reiniciar a notificação.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Notificações de reinício do dispositivo na versão 1902

<!--3555947-->
Por vezes, os utilizadores não vêem a notificação do Brinde do Windows sobre um reinício ou implementação necessária. Então não vêem a experiência para dormir o lembrete. Este comportamento pode levar a uma má experiência do utilizador quando o cliente atinge um prazo.

A partir da versão 1902, quando são necessárias alterações de software ou as implementações precisam de ser reiniciadas, tem a opção de utilizar uma janela de diálogo mais intrusiva.

No grupo [de reiniciar](about-client-settings.md#computer-restart) computadores as definições do cliente, ative a seguinte opção: Quando **uma implementação necessitar de um reinício, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torrada**.  

Configurar esta definição de cliente altera a experiência do utilizador para todas as implementações necessárias que requerem um reinício das notificações de torradas:

![Notificação de torrada saque a que é necessário reiniciar](media/3555947-restart-toast-initial.png)  

Para a janela de diálogo mais intrusiva do Centro de Software:

![Janela de diálogo para reiniciar o seu computador](media/3976435-proactive-user-restart-notification.png)

Se o utilizador não reiniciar o dispositivo após a instalação, receberá uma notificação como lembrete. Este lembrete temporário aparecerá ao utilizador com base na definição do cliente: **Apresentar uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)**. Esta definição é o tempo total que o utilizador tem de reiniciar a máquina antes de ser forçado um reinício.

- Notificação temporária quando utiliza notificações de torradas:

  ![Notificação de torradas de reinício pendente](media/3555947-restart-toast.png)

- Notificação temporária quando utilizar janela de diálogo do Centro de Software, não torradas:

  ![Notificação pendente do Centro de Software com botão de soneca](media/3555947-1902-hide-notification.png)

Se o utilizador não reiniciar após a notificação temporária, será dada a notificação final de contagem regressiva que não pode fechar. O momento em que a notificação final aparece baseia-se na definição do cliente: **Exiba uma caixa de diálogo que o utilizador não pode fechar, que apresenta o intervalo de contagem regressiva antes de o utilizador ser desligado ou o computador reiniciar (minutos)**. Por exemplo, se a definição for de 60, então uma hora antes de um reboot ser forçado, a notificação final aparece ao utilizador:

![Notificação final do Centro de Software](media/3555947-1902-final-countdown.png)

As seguintes definições devem ser mais curtas em duração do que a janela de [manutenção](../manage/collections/use-maintenance-windows.md) mais curta aplicada ao computador:

- **Apresentar uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)**
- **Exiba uma caixa de diálogo que o utilizador não pode fechar, que apresenta o intervalo de contagem regressiva antes de o utilizador ser desligado ou o computador reiniciar (minutos)**

> [!IMPORTANT]
> Em Configuração Manager 1902, sob certas circunstâncias, a caixa de diálogo não substituirá as notificações de torradas. Para resolver este problema, instale o rollup da atualização para a [versão 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)do Gestor de Configuração . <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Notificações de reinício do dispositivo a partir da versão 1906
<!--3976435-->
Alguns administradores preferem notificações de reinício frequentes e um curto prazo para permitir o adiamento dos reinícios. Outros administradores permitem que os utilizadores adiem um reinício por períodos de tempo mais longos e desejam que os utilizadores sejam notificados do reinício pendente com pouca frequência. A versão 1906 do Gestor de Configuração dá um controlo adicional ao administrador sobre o tempo e a frequência das notificações de reinício. Os seguintes itens foram introduzidos em 1906 para conferir ao administrador um maior controlo:

- **Especifique a duração do soneto para as notificações de contagem regressiva do computador (minutos)** adicionadas às [definições](about-client-settings.md#computer-restart)do cliente de reiniciar o computador .
- O valor máximo para **exibir uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)** aumentou de 1440 minutos (24 horas) para 20160 minutos (duas semanas).
- O utilizador não verá uma barra de progresso na notificação de reinício até que o reinício pendente esteja a menos de 24 horas de distância.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Notificações quando o software necessário é instalado no prazo ou após o prazo

Quando o software necessário for instalado no prazo ou após o prazo, os seus utilizadores verão notificações dependendo das definições do cliente selecionadas.

Se a definição **Quando uma implementação necessitar de um reinício, mostre uma janela de diálogo ao utilizador em vez de uma notificação de torrada:**

- **Não** - As notificações de torradas são utilizadas até que a notificação final de contagem regressiva seja alcançada.
- **Sim** - Uma notificação do Centro de Software é vista.
  - Se o reinício for superior a 24 horas de distância, prevê-se um tempo estimado de reinício. O momento desta notificação baseia-se na definição: **Apresentar uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)**.

     ![O tempo de reinício é superior a 24 horas](media/3976435-notification-greater-than-24-hours.png)

  - Se o recomeço estiver a menos de 24 horas de distância, uma barra de progresso é vista. O momento desta notificação baseia-se na definição: **Apresentar uma notificação temporária ao utilizador que indique o intervalo antes de o utilizador ser desligado ou o computador reiniciar (minutos)**

     ![O tempo de reinício é a menos de 24 horas de distância](media/3976435-notification-less-than-24-hours.png)

Se o utilizador selecionar o botão **Snooze,** outra notificação temporária ocorrerá após o período de soneca decorrer, assumindo que ainda não chegaram à contagem decrescente final. O momento da próxima notificação baseia-se na definição: **Especifique a duração do soneto para as notificações de contagem regressiva do computador (horas)**. Se o utilizador selecionar **o Snooze** e o intervalo de dormir for de uma hora, o utilizador será novamente notificado em 60 minutos, assumindo que ainda não atingiu a contagem decrescente final.

Quando a contagem decrescente final é alcançada, o utilizador recebe uma notificação que não pode fechar. A barra de progresso está a vermelho e o utilizador não consegue bater **no Snooze.**

![Notificação final do Software Center na versão 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>O utilizador instala proativamente antes do prazo

Se o utilizador instalar proativamente o software necessário que necessite de ser reiniciado antes do prazo, verá uma notificação diferente. Para obter mais informações sobre a configuração destas definições, consulte as definições de [Experiência do **Utilizador** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) de Implementação e [as notificações do Utilizador para obter as implementações necessárias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

A seguinte notificação ocorre quando tanto a definição da experiência do utilizador permite notificações e não utiliza notificações de torradas para a implementação:

![Notificação para software instalado proactivamente](media/3976435-proactive-user-restart-notification.png)

Uma vez atingido o prazo para o software, as [Notificações quando](#notifications-when-required-software-is-installed-at-or-after-the-deadline) o software necessário é instalado no ou após o prazo de comportamento.

## <a name="log-files"></a>Ficheiros de registo

Utilize o **RebootCoordinator.log** e **sCNotify.log** para reiniciar o dispositivo de resolução de problemas. Também pode ter de utilizar [ficheiros](../../plan-design/hierarchy/log-files.md) de registo de clientes adicionais com base no tipo de implementação utilizado.

## <a name="next-steps"></a>Passos seguintes

- [Gestão de aplicações de introdução](../../../apps/understand/introduction-to-application-management.md)
- [Introdução à implementação de sistemas operativos](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Introdução à gestão de atualizações de software](../../../sum/understand/software-updates-introduction.md)
