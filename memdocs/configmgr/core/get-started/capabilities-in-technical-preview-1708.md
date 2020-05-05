---
title: Pré-visualização técnica 1708
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1708 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721333"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1708 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1708. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **A atualização para pré-visualizar a versão 1708 falha quando tem um servidor**de site em modo passivo . Quando executar a versão de pré-visualização 1706 ou 1707, e tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)tem de desinstalar o servidor do site do modo passivo antes de poder atualizar com sucesso o seu site de pré-visualização para a versão 1708. Pode reinstalar o servidor do site do modo passivo depois de o seu site ser executado na versão 1708.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola, vá para **a Administração** > **Resumo** > servidores de**configuração** > do site**e funções**do sistema do site, e, em seguida, selecione o servidor de site de modo passivo.
  2. No painel de funções do **Sistema do Site,** clique à direita na função **do servidor do Site** e, em seguida, escolha remover **a função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.




**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Melhorias para especificar parâmetros de script quando implementa scripts PowerShell do Gestor de Configuração
<!-- 1236459 -->

A partir do Diretor de Configuração 1706, [podes criar e executar scripts PowerShell a partir da consola do Gestor de Configuração](../../apps/deploy-use/create-deploy-scripts.md).

Na [Pré-visualização Técnica 1707,](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)expandimos esta capacidade para permitir que o Gestor de Configuração leia os parâmetros do script.

Nesta Pré-visualização Técnica, expandimos a capacidade de parâmetros do script para detetar quais os parâmetros obrigatórios, e que são opcionais, e pedimos-lhe que entre nestes.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executar scripts PowerShell a partir da consola 'Gestor](../../apps/deploy-use/create-deploy-scripts.md)de Configuração'.
2. Na nova página de **Parâmetros** do Script do Assistente de **Script Criar,** escolha um parâmetro e, em seguida, edite os seus valores.
O assistente exibe quais os parâmetros obrigatórios e que são opcionais.
4. Quando terminar os parâmetros de edição, complete o assistente.

Quando o script estiver em funcionação, utilizará todos os valores do parâmetro configurado. Se não configurar um parâmetro obrigatório, o utilizador final será solicitado a fornecer o parâmetro quando o script estiver em funcionação.

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 -->
Agora pode obter informações sobre o estado atual do seu ambiente com base na análise de dados na base de dados do site. As ideias ajudam-no a entender melhor o seu ambiente e a tomar medidas com base na perceção. Rever insights de gestão na consola de Gestor de Configuração na Management > Insights**De Gestão**de > **Administração**Todos os Insights . **Administration** Neste comunicado, estão agora disponíveis os seguintes insights:

- **Aplicações sem implementações**: Lista as aplicações no seu ambiente que não possuem implementações ativas. Isto ajuda-o a encontrar e eliminar aplicações não utilizadas para simplificar a lista de aplicações apresentadas na consola.
- **Coleções vazias**: Lista as coleções no seu ambiente que não têm membros. Pode eliminar estas coleções para simplificar a lista de coleções apresentadas ao implementar objetos, por exemplo.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Reiniciar computadores a partir da consola 'Gestor de Configuração'   
<!-- 1356283 -->
A partir desta versão, pode utilizar a consola 'Gestor de Configuração' para identificar dispositivos clientes que requerem um reinício e, em seguida, utilizar uma ação de notificação do cliente para os reiniciar.

Para identificar dispositivos que estejam pendentes de um reinício, vá a**Dispositivos** **de Ativos e Compliance** > e selecione uma coleção com dispositivos que possam necessitar de um reinício. Depois de selecionar uma coleção, pode visualizar o estado de cada dispositivo no painel de detalhes numa nova coluna chamada **Pendente Reboot**. Cada dispositivo tem um valor de **Sim,** ou **Não**.

Para criar a notificação do cliente para reiniciar um dispositivo:
1. Localize o dispositivo que pretende reiniciar no nó de Dispositivos da consola.
2. Clique à direita no dispositivo, selecione **Notificação**do Cliente e, em seguida, **selecione Reboot**. Isto abre uma janela de informação sobre o recomeço. Clique **em OK** para confirmar o pedido de reinício.

Quando a notificação é recebida por um cliente, abre-se uma janela de notificação do **Software Center** para informar o utilizador sobre o reinício. Por defeito, o reinício ocorre após 90 minutos. Pode modificar o tempo de reinício configurando [as definições do cliente](../clients/deploy/configure-client-settings.md). As definições para o comportamento de reinício são encontradas no separador de [reinício](../clients/deploy/about-client-settings.md#computer-restart) do Computador das definições predefinidas.


### <a name="try-it-out"></a>Experimente!
Tente completar as seguintes tarefas e, em seguida, envie-nos **feedback** do separador **Home** da Fita para nos informar como funcionava:
1. Implemente uma aplicação ou atualização para um dispositivo que exija que o dispositivo reinicie para concluir a instalação.
2. Localize o dispositivo no nó de**Dispositivos** de **Segurança e Conformidade** > da consola e confirme que apresenta **Sim** na coluna Pendente **de Reboot.** Pode levar até 20 minutos para que o estado de Reinício pendente seja refletido na consola.
3. Monitorize o dispositivo para confirmar que a notificação do Centro de Software abre e que o dispositivo reinicia com sucesso.


## <a name="software-center-customization"></a>Personalização do Centro de Software
<!-- 1351224 -->
Pode adicionar elementos de marca empresarial e especificar a visibilidade dos separadores no Software Center. Pode adicionar o nome específico da empresa do Software Center, definir um tema de cores de configuração do Software Center, definir um logotipo da empresa e definir os separadores visíveis para dispositivos clientes.

### <a name="customize-software-center"></a>Personalizar centro de software

Para modificar o Centro de Software:

1. Na consola **'Gestor de Configuração',** escolha**as Definições**do Cliente **de Administração** > . Clique na sua instância de definição de cliente desejada.
2. No separador **Casa,** no grupo **Propriedades,** escolha **Propriedades**.
3. Na caixa de diálogo **Definições Predefinidas,** escolha **O Centro**de Software .
4. Selecione **Sim** para **Selecionar novas definições para especificar as informações da empresa** para ativar as definições de personalização do Software Center.
5. Digite o nome da **sua Empresa.**
6. Selecione o seu **Esquema de Cores para Centro**de Software .
7. Clique em **Navegar** para navegar para o seu logótipo para O Centro de Software. O logótipo deve ser um JPEG ou PNG de 400 x 100 pixels com um tamanho máximo de 750 KB.
8. Selecione **SIM** para tornar os separadores visíveis no Centro de Software para dispositivos clientes. Pelo menos um separador deve ser visível:

    -  Ativar o separador Aplicações
    -  Ativar o separador Atualizações
    -  Ativar o separador Sistemas Operativos
    -  Ativar o separador estado de instalação
    -  Ativar o separador de conformidade do dispositivo
    -  Ativar o separador Opções

### <a name="next-steps"></a>Passos seguintes

Para saber mais sobre a gestão de aplicações no Gestor de Configuração, consulte [introdução à gestão de aplicações.](../../apps/understand/introduction-to-application-management.md)
