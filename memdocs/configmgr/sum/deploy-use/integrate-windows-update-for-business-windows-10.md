---
title: Integrar a tualização do Windows para negócios
titleSuffix: Configuration Manager
description: Utilize o Windows Update for Business (WUfB) para manter o Windows 10 atualizado para dispositivos ligados ao serviço Windows Update.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8bfd535c93cb9f1dcfc42705f3cce61874dfe226
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724420"
---
# <a name="integrate-with-windows-update-for-business"></a>Integrar com a Atualização do Windows para Negócios

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Windows Update for Business (WUfB) permite manter os dispositivos baseados no Windows 10 na sua organização sempre atualizados com as mais recentes defesas de segurança e funcionalidades do Windows quando estes dispositivos se ligam diretamente ao serviço Windows Update (WU). O Gestor de Configuração pode diferenciar os computadores do Windows 10 que utilizam wufb e WSUS para obter atualizações de software.  

> [!WARNING]
> Se estiver a utilizar a cogestão dos seus dispositivos e tiver mudado as políticas de [Atualização](../../comanage/workloads.md#windows-update-policies) do Windows para Intune, então os seus dispositivos receberão o [seu Windows Update para as políticas de Negócios a partir de Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Se o cliente do Gestor de Configuração ainda estiver instalado no dispositivo cogerido, as definições para Atualizações Cumulativas e Atualizações de Funcionalidades são geridas pela Intune. No entanto, o patching de terceiros, se ativado nas Definições do [**Cliente,**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)ainda é gerido pelo Gestor de Configuração.  

 Algumas funcionalidades do Gestor de Configuração já não estão disponíveis quando os clientes do Gestor de Configuração estão configurados para receber atualizações da WU, que inclui WUfB ou Windows Insiders:  

- Relatórios de conformidade do Windows Update:  
  - O Gestor de Configuração desconhece as atualizações que são publicadas na WU. Os clientes do Gestor de Configuração configurados para receber atualizações da WU apresentarão **desconhecidos** para estas atualizações na consola 'Gestor de Configuração'.  

  - A resolução de problemas no estado de conformidade geral é difícil porque o estado **desconhecido** era apenas para os clientes que não tinham reportado o estado de verificação da WSUS. Agora também inclui clientes do Gestor de Configuração que recebem atualizações da WU.  

  - Definição Atualizações a conformidade faz parte do relatório geral de conformidade da atualização e também não funcionará como esperado.

- O relatório global de proteção de endpoint para defender com base no estado de conformidade da atualização não retornará resultados precisos devido aos dados de digitalização em falta.  

- O Gestor de Configuração não será capaz de implementar atualizações da Microsoft, como Office, IE e Visual Studio para clientes ligados à WUfB para receber atualizações.  

- O Gestor de Configuração ainda pode implementar atualizações de terceiros que são publicadas no WSUS e geridas através do Gestor de Configuração para clientes que estão ligados ao WUfB para receber atualizações. Se não quiser que sejam instaladas atualizações de terceiros em clientes ligados ao WUfB, desative a definição do cliente chamada [Enable atualizações](../../core/clients/deploy/about-client-settings.md#software-updates)de software nos clientes .

- Configuração Manager implementação completa de clientes que usa a infraestrutura de atualizações de software não funcionará para clientes que estão ligados ao WUfB para receber atualizações.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifique clientes que usam WUfB para atualizações do Windows 10

Utilize o seguinte procedimento para identificar clientes que utilizam o WUfB para obter atualizações e atualizações do Windows 10. Em seguida, configure estes clientes para parar de usar o WSUS para obter atualizações, e implementar uma definição de agente cliente para desativar o fluxo de trabalho de atualizações de software para estes clientes.  

### <a name="prerequisites-for-wufb"></a>Pré-requisitos para o WUfB

- Clientes com Windows 10 Desktop Pro ou Windows 10 Enterprise Edition, versão 1511 ou posterior

- O[Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) é implementado e os clientes utilizam o WUfB para obter atualizações do Windows 10.  

### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que utilizam o WUfB  

1. Certifique-se de que o Agente de Atualização do Windows não está a analisar o WSUS, caso tenha sido previamente ativado. A seguinte tecla de registo pode ser utilizada para indicar se o computador está a digitalizar contra wSUS ou Windows Update. Se a chave de registo não existe, não é uma digitalização contra a WSUS.
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsUpdate\AU\UseWUServer**
1. Há um novo atributo, **UseWUServer,** sob o nó **de Atualização do Windows** no Explorador de Recursos do Gestor de Configuração.
1. Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos. Pode criar uma coleção baseada numa consulta semelhante à abaixo:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Crie uma definição de agente cliente para desativar o fluxo de trabalho da atualização de software. Desloque a definição para a recolha de computadores que estão ligados diretamente ao WUfB.
1. Os computadores que são geridos via WUfB apresentarão **Desconhecido** no estado de conformidade e não serão contados como parte da percentagem de conformidade global.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configure atualização do Windows para políticas de adiamento de negócios
<!-- 1290890 -->
A partir da versão 1706 do Gestor de Configuração, pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento no novo nó **de Atualização do Windows para Políticas Empresariais** no âmbito da Manutenção da **Biblioteca** > de Software**Windows 10**.

> [!NOTE]
> A partir da versão 1802 do Gestor de Configuração, pode definir políticas de diferimento para o Windows Insider. <!--507201-->  
Para mais informações sobre o programa Windows Insider, consulte [Iniciar-se com o programa Windows Insider para o Negócios](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites-for-deferral-policies"></a>Pré-requisitos para políticas de diferimento

- Windows 10 versão 1703 ou mais tarde
- Dispositivos Windows 10 geridos pelo Windows Update para o Negócios devem ter conectividade com a Internet

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma política de adiamento do Windows Update para negócios

1. Na **Biblioteca** > de Software**Windows 10 a servico** > **windows update para políticas empresariais**
1. No separador **Home,** no grupo **Create,** selecione **Create Windows Update for Business Policy** para abrir a Create Windows Update para o Assistente de Política de Negócios.
1. Na página **Geral,** forneça um nome e descrição para a apólice.
1. Na página **Deferral Policies,** configure se deve adiar ou interromper atualizações de funcionalidades. Geralmente, as Atualizações de Funcionalidades são novas funcionalidades do Windows. Depois de configurar a definição do nível de prontidão do **Branch,** pode então definir se, e por quanto tempo, gostaria de adiar receber Atualizações de Funcionalidades após a sua disponibilidade da Microsoft.
    - **Nível de prontidão**do ramo : Desajuste o ramo para o qual o dispositivo receberá atualizações do Windows. Escolha o Canal Semi-Anual (Direcionado), canal semi-anual ou uma construção do Windows Insider.

        > [!NOTE]
        > Implementar políticas para **o Canal Semi-Anual (Direcionado)** para o Windows 10, *versão 1903 ou posterior*. Implementar políticas para **o Canal Semi-Anual** para o Windows 10, *versão 1809 ou mais cedo*.
        >
        > Se implementar uma política para **o Canal Semi-Anual** para o Windows 10, versão 1903 ou posterior, a implementação falha com o erro **0x8004100c**.<!-- 5593139 -->

    - **Período de diferimento (dias)**: Especifique o número de dias para os quais as Atualizações de Funcionalidades serão adiadas. Pode adiar a receção destas Atualizações de Funcionalidades até 365 dias a partir do seu lançamento.
    - **Pausa funcionalidades Atualizações a partir**de início : Selecione se suspender os dispositivos de receber Atualizações de Funcionalidades durante um período máximo de 35 dias a partir do momento em que pausa as atualizações. Após ter decorrido o número máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações aplicáveis nas Atualizações do Windows. Após esta procura, pode colocar as atualizações em pausa novamente. Pode despausar atualizações de funcionalidades limpando a caixa de verificação.
1. Escolha se deve adiar ou parar as Atualizações de Qualidade. Geralmente, as Atualizações de Qualidade são correções e melhorias às funcionalidades do Windows existentes e, normalmente, são publicadas na primeira terça-feira de cada mês, embora possam ser lançadas em qualquer altura pela Microsoft. Pode definir se, e durante quanto tempo, gostaria de diferir a receção das Atualizações de Qualidade, após a sua disponibilidade.
    - Período de **diferimento (dias)**: Especifique o número de dias para os quais as Atualizações de Qualidade serão adiadas. Pode adiar a receção destas Atualizações de Qualidade até 30 dias a partir do seu lançamento.
    - **Pausa Atualizações de Qualidade a partir**de início : Selecione se suspender os dispositivos de receber Atualizações de Qualidade durante um período máximo de 35 dias a partir do momento em que pausa as atualizações. Após ter decorrido o número máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações aplicáveis nas Atualizações do Windows. Após esta procura, pode colocar as atualizações em pausa novamente. Pode despausar atualizações de qualidade limpando a caixa de verificação.
1. Selecione **Instalar atualizações de outros Produtos microsoft** para ativar a definição de política do grupo que torna as definições de diferimento aplicáveis ao Microsoft Update, bem como as Atualizações do Windows.
1. **Selecione Incluir controladores com Atualização do Windows** para atualizar automaticamente os controladores a partir de Atualizações do Windows. Se limpar esta definição, as atualizações do controlador não são descarregadas a partir de Atualizações do Windows.
1. Complete o assistente para criar a nova política de adiamento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implementar uma atualização do Windows para a política de adiamento de negócios

1. Na **Biblioteca** > de Software**Windows 10 a servico** > **windows update para políticas empresariais**
1. No separador **Home,** no grupo **implementação,** selecione Implementar a **Atualização do Windows para a Política de Negócios**.
1. Configure as seguintes definições:
    - Política de **configuração a implementar**: Selecione a atualização do Windows para a política de negócios que gostaria de implementar.
    - **Recolha**: Clique em **Navegar** para selecionar a coleção onde pretende implementar a apólice.
    - **Permitir a reparação fora da janela de manutenção**: Se tiver sido configurada uma janela de manutenção para a recolha à qual está a implementar a apólice, ative esta opção para permitir que as definições de política remediam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Horário**: Especifique o calendário de avaliação de conformidade através do qual a política implementada é avaliada em computadores clientes. O agendamento pode ser simples ou personalizado.
1. Complete o assistente para implementar a apólice.
